# Report Java application data by using Open Telemetry

Before using the tracing analysis console to trace tracing data, you need to report the data to the tracing analysis console from the client. This topic describes how to perform application tracking through Open Telemetry SDK and report link data through Jaeger Export.



## Procedure

1.  Open the pom.xml file and add Jar dependencies.

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

2.  Use Jaeger Export to report data.

    Use inittracer\(\) parameter initialization Tracer object using mywonderfulusecase\(\) parameters by Tracer object generation Span to code buried...

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

3.  Download the [Alibaba Cloud](https://yuque.alibaba-inc.com/docs/share/78105bd6-a7a1-4476-85a1-9b896ac4cefe?#) demo project, and replace the Token information in the project with the Token obtained in the prerequisites.

4.  Run the following command to run the Demo.

    ```
    mvn clean compile exec:java -Dexec.mainClass=com.demo.OpenTelemetryExample      
    ```


## View data

In the , Select the new application \(application in this example is otel-jaeger-example\) on the [Tracing Analysis console](https://tracing-sg.console.aliyun.com/) page in the application list to view the trace data.

**Related topics**  


[Open Telemetry official documentation](https://github.com/open-telemetry/opentelemetry-java/tree/master/examples/jaeger)

