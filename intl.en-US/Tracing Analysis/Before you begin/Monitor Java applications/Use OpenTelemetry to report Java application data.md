# Use OpenTelemetry to report Java application data

Before you can view the trace data of your application in the Tracing Analysis console, you must use a client to report the trace data to Tracing Analysis. This topic shows you how to use OpenTelemetry SDK to instrument your application. This topic also shows you how to use a Jaeger exporter to report the trace data.

## Procedure

1.  Open the pom.xml file and add JAR dependencies.

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

2.  Use a Jaeger exporter to report data.

    Use the initTracer\(\) method to initialize the Tracer object. Then, use the myWonderfulUseCase\(\) method to create a span based on the Tracer object and add instrumentation to the code.

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

3.  Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/openTelemetryDemo.zip) and replace the token in the project with the token that you obtain in the "Prerequisites" section of this topic.

4.  Run the following command to run the demo:

    ```
    mvn clean compile exec:java -Dexec.mainClass=com.demo.OpenTelemetryExample
    ```


## View data

Log on to the [Application Real-Time Monitoring Service \(ARMS\) console](https://arms-ap-southeast-1.console.aliyun.com/#/home). In the left-side navigation pane, choose **Tracing Analysis** \> Applications. On the Applications page, click the newly created application. In this example, click the otel-jaeger-example application. Then, view the trace data of the application.

**Related topics**  


[OpenTelemetry official documentation](https://github.com/open-telemetry/opentelemetry-java/tree/master/examples/jaeger)

