# 通过Open Telemetry上报Java应用数据

在使用链路追踪控制台追踪应用的链路数据之前，需要通过客户端将应用数据上报至链路追踪。本文介绍如何通过Open Telemetry SDK进行应用埋点，并通过Jaeger Export上报链路数据。



## 操作步骤

1.  打开pom.xml文件，添加Jar包依赖。

    ```
    <io.opentelemetry.version>0.12.0</io.opentelemetry.version>
    ...
    <dependency>
                <groupId>io.opentelemetry</groupId>
                <artifactId>opentelemetry-api</artifactId>
                <version>${io.opentelemetry.version}</version>
            </dependency>
    
            <dependency>
                <groupId>io.opentelemetry</groupId>
                <artifactId>opentelemetry-sdk-metrics</artifactId>
                <version>${io.opentelemetry.version}</version>
            </dependency>
    
            <dependency>
                <groupId>io.opentelemetry</groupId>
                <artifactId>opentelemetry-sdk-trace</artifactId>
                <version>${io.opentelemetry.version}</version>
            </dependency>
    
            <dependency>
                <groupId>io.opentelemetry</groupId>
                <artifactId>opentelemetry-sdk</artifactId>
                <version>${io.opentelemetry.version}</version>
            </dependency>
    
            <dependency>
                <groupId>io.opentelemetry</groupId>
                <artifactId>opentelemetry-exporter-jaeger</artifactId>
                <version>${io.opentelemetry.version}</version>
            </dependency>
    ```

2.  通过Jaeger Export上报数据。

    使用initTracer\(\)参数初始化Tracer对象，使用myWonderfulUseCase\(\)参数通过Tracer对象生成Span来进行代码埋点。

    ```
    import io.grpc.*;
    import io.opentelemetry.api.trace.Span;
    import io.opentelemetry.api.trace.Tracer;
    import io.opentelemetry.exporter.jaeger.JaegerGrpcSpanExporter;
    import io.opentelemetry.sdk.OpenTelemetrySdk;
    import io.opentelemetry.sdk.trace.export.SimpleSpanProcessor;
    
    public class OpenTelemetryExample {
        // OTel API
        private Tracer tracer = null;
    
    
        private void initTracer(String name, int port, String auth) {
            // Create a channel towards Jaeger end point
            ManagedChannel jaegerChannel = ManagedChannelBuilder.forAddress(name, port).intercept(new ClientInterceptor() {
                @Override
                public <ReqT, RespT> ClientCall<ReqT, RespT> interceptCall(MethodDescriptor<ReqT, RespT> methodDescriptor, CallOptions callOptions, Channel channel) {
                    return new ForwardingClientCall.SimpleForwardingClientCall<ReqT, RespT>(
                            channel.newCall(methodDescriptor, callOptions)) {
                        @Override
                        public void start(Listener<RespT> responseListener, final Metadata headers) {
                            Metadata.Key<String> headerKey = Metadata.Key.of("Authentication", Metadata.ASCII_STRING_MARSHALLER);
                            headers.put(headerKey, auth);
                            super.start(responseListener, headers);
                        }
                    };
                }
            }).usePlaintext().build();
    
            // Export traces to Jaeger
            JaegerGrpcSpanExporter jaegerExporter =
                    JaegerGrpcSpanExporter.builder()
                            .setServiceName("otel-jaeger-example")
                            .setChannel(jaegerChannel)
                            .setDeadlineMs(30000)
                            .build();
    
            // Set to process the spans by the Jaeger Exporter
            OpenTelemetrySdk openTelemetry = OpenTelemetrySdk.builder().build();
            openTelemetry
                    .getTracerManagement()
                    .addSpanProcessor(SimpleSpanProcessor.builder(jaegerExporter).build());
    
    
            openTelemetry.getTracerManagement();
            tracer = openTelemetry.getTracer("io.opentelemetry.example.JaegerExample");
    
        }
    
        private void myWonderfulUseCase() {
            // Generate a span
            Span span = this.tracer.spanBuilder("Start my wonderful use case").startSpan();
            span.addEvent("Event 0");
            // execute my use case - here we simulate a wait
            doWork();
            span.addEvent("Event 1");
            span.end();
        }
    
        private void doWork() {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
            }
        }
    
        public static void main(String[] args) {
    
            OpenTelemetryExample example = new OpenTelemetryExample();
            // please replease token from "http://tracing.console.aliyun.com/"
            example.initTracer("tracing-analysis-dc-bj.aliyuncs.com", 1883, "123@0yourToken_123@0yourToken");
            example.myWonderfulUseCase();
            // wait some seconds
            try {
                Thread.sleep(10000);
            } catch (InterruptedException e) {
            }
            System.out.println("Bye");
        }
    }
    ```

3.  下载[\[Demo\]](https://yuque.alibaba-inc.com/docs/share/78105bd6-a7a1-4476-85a1-9b896ac4cefe?#)工程，并将工程中的Token信息替换为前提条件中获取的Token。

4.  执行以下命令运行Demo。

    ```
    mvn clean compile exec:java -Dexec.mainClass=com.demo.OpenTelemetryExample
    ```


## 查看数据

在[链路追踪Tracing Analysis控制台](https://tracing-sg.console.aliyun.com/)的应用列表页面选择新创建的应用（本示例中的应用为“otel-jaeger-example“），查看链路数据。

**相关文档**  


[Open Telemetry官方文档](https://github.com/open-telemetry/opentelemetry-java/tree/master/examples/jaeger)

