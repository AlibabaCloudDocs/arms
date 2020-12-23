# Use Jaeger to report Java application data

Before using the tracing analysis console to trace tracing data, you need to report the data to the tracing analysis console from the client. This topic describes how to use the Jaeger client to report data to applications.



[Jaeger](https://www.jaegertracing.io/) is an open-source distributed tracing system that is compatible with OpenTracing APIs. This open- [source organization has joined CNCF](https://www.cncf.io/blog/2017/09/13/cncf-hosts-jaeger/). This function aggregates real-time monitoring data from multiple heterogeneous systems. Currently, many components in the OpenTracing community support various Java frameworks.

-   [Apache HttpClient](https://github.com/opentracing-contrib/java-apache-httpclient)
-   [Elasticsearch](https://github.com/opentracing-contrib/java-elasticsearch-client)
-   [JDBC](https://github.com/opentracing-contrib/java-jdbc)
-   [Kafka](https://github.com/opentracing-contrib/java-kafka-client)
-   [Memcached](https://github.com/opentracing-contrib/java-memcached-client)
-   [Mongo](https://github.com/opentracing-contrib/java-mongo-driver)
-   [OkHttp](https://github.com/opentracing-contrib/java-okhttp)
-   [Redis](https://github.com/opentracing-contrib/java-redis-client)
-   [Spring Boot](https://github.com/opentracing-contrib/java-spring-web)
-   [Spring Cloud](https://github.com/opentracing-contrib/java-spring-cloud)

To use Jaeger to report Java application data to the tracing analysis console, you must first perform tracking. You can manually record points or use various existing plug-ins to implement tracking. This article introduces the following three tracking methods.

-   Manual burial point
-   Burial points through Spring Cloud components
-   Tracking through gRPC components



## Manual tracking for Java applications

To use Jaeger to report Java application data to the link tracking console, you must complete tracking. This example uses manual instrumentation.

1.  [Download the Demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerTracingDemo.zip) in the left-side navigation pane.manualDemoAnd run the program according to the Readme instructions.

2.  Open the pom. xml file and add the dependency on the Jaeger client.

    ```
    <dependency>
        <groupId>io.jaegertracing</groupId>
        <artifactId>jaeger-client</artifactId>
        <version>0.31.0</version>
    </dependency>
    ```

3.  Configure the initialization parameters and create a Tracer object.

    A Tracer object can be used to create a Span object to record the distributed operation time, pass data across machines through the Extract/Inject method, or set the current Span. The Tracer object is also configured with data such as the gateway address, local IP address, sampling rate, and service name. You can adjust the sampling rate to reduce the overhead caused by data reporting.

    **Note:** Please replace `<endpoint>` with corresponding endpoints of clients and regions on the Overview page of Tracing Analysis console. For more information about how to obtain endpoint information, please see [Obtain access point information](#tab2).

    ```
    // Replace terminaldemo with the name of your application.
    io.jaegertracing.Configuration config = new io.jaegertracing.Configuration(&quot;manualDemo&quot;);
    io.jaegertracing.Configuration.SenderConfiguration sender = new io.jaegertracing.Configuration.SenderConfiguration();
    // Replace <endpoint> with the endpoint of the corresponding client and region on the console overview page.
    sender.withEndpoint(&quot;<endpoint>&quot;);
    config.withSampler(new io.jaegertracing.Configuration.SamplerConfiguration().withType(&quot;const&quot;).withParam(1));
    config.withReporter(new io.jaegertracing.Configuration.ReporterConfiguration().withSender(sender).withMaxQueueSize(10000));
    GlobalTracer.register(config.getTracer());
    ```

4.  Record request data.

    ```
    Tracer tracer = GlobalTracer.get();
    // Create a Span
    Span span = tracer.buildSpan(&quot;parentSpan&quot;).withTag(&quot;myTag&quot;, &quot;spanFirst&quot;).start();
    tracer.scopeManager().activate(span, false);
    tracer.activeSpan().setTag(&quot;methodName&quot;, &quot;testTracing&quot;);
    // Business logic
    secondBiz();
    span.finish();
    ```

5.  The previous step is used to record the root operation of the request. If you need to record the previous and next operations of the request, enter the context.

    ```
    Tracer tracer = GlobalTracer.get();
    Span parentspan = tracer.activeSpan();
    Tracer.SpanBuilder spanBuilder = tracer.buildSpan(&quot;childSpan&quot;).withTag(&quot;myTag&quot;, &quot;spanSecond&quot;);
    if (parentspan! =null) {
        spanBuilder.asChildOf(parentspan).start();
    }
    Span childSpan = spanBuilder.start();
    tracer.scopeManager().activate(childSpan, false);
    // Business logic
    childSpan.finish();
    tracer.activeSpan().setTag(&quot;methodName&quot;, &quot;testCall&quot;);
    ```

6.  To facilitate troubleshooting, you can add custom tags to a record, such as records for errors and returned values of requests.

    ```
    tracer.activeSpan().setTag(&quot;methodName&quot;, &quot;testCall&quot;);
    ```

7.  When a distributed system sends an RPC request, it carries Tracing data, including TraceId, ParentSpanId, SpanId, and Sampled. You can use the Extract/Inject method in an HTTP Request to transparently transmit data to HTTP Request Headers. The overall process is as follows:

    ```
       Client Span Server Span
    ┌ ── ── ── ── ── ┐ ┌ ── ── ── ──
    Number of failed migration tasks
    │ TraceContext │ Http Request Headers │ TraceContext │
    │ ┌ ── ── ── ── ┐ │ ── ── ── ── ── ── ┐ ┌ ── ── ── ┐ │
    │ │ TraceId │ │ │ X-B3-TraceId │ │ │ TraceId │ │
    │ │ │ │ │ │ │ │ │ │ │
    │ │ ParentSpanId │ │ Inject │ X-B3-ParentSpanId │Extract │ │ ParentSpanId │ │
    │ │ ── ── ── ── ──> │ ├ ── ── ┼> │ │ │
    │ │ SpanId │ │ │ X-B3-SpanId │ │ │ SpanId │ │
    │ │ │ │ │ │ │ │ │ │ │
    │ │ Sampled │ │ │ X-B3-Sampled │ │ │ Sampled │ │
    │ └ ── ── ── ── ┘ │ ── ── ── ── ── ── ┘ └ ── ── ── ┘ │
    Number of failed migration tasks
    └ ── ── ── ── ── ┘ └ ── ── ── ──
    ```

    1.  Call the Inject method on the client to pass in Context information.

        ```
        private void attachTraceInfo(Tracer tracer, Span span, final Request request) {
                tracer.inject(span.context(), Format.Builtin.TEXT_MAP, new TextMap() {
                    @Override
                    public void put(String key, String value) {
                        request.setHeader(key, value);
                    }
                    @Override
                    public Iterator<Map.Entry<String, String>> iterator() {
                        throw new UnsupportedOperationException(&quot;TextMapInjectAdapter should only be used with Tracer.inject()&quot;);
                    }
                });
            }
        ```

    2.  Call the Extract method on the server to parse the Context information.

        ```
        protected Span extractTraceInfo(Request request, Tracer tracer) {
            Tracer.SpanBuilder spanBuilder = tracer.buildSpan(&quot;/api/xtrace/test03&quot;);
            try {
                SpanContext spanContext = tracer.extract(Format.Builtin.TEXT_MAP, new TextMapExtractAdapter(request.getAttachments()));
                if (spanContext! = null) {
                    spanBuilder.asChildOf(spanContext);
                }
            } catch (Exception e) {
                spanBuilder.withTag(&quot;Error&quot;, &quot;extract from request fail, error msg:&quot; + e.getMessage());
            }
            return spanBuilder.start();
        }
                                        
        ```


## Using Spring Cloud components to track Java applications

To use Jaeger to report Java application data to the tracing analysis console, you must first perform tracking. This example uses the Spring Cloud component tracking. Spring Cloud provides the burial points for the following components.

-   @Async, @Scheduled, Executors
-   Feign, HystrixFeign
-   Hystrix
-   JDBC
-   JMS
-   Mongo
-   RabbitMQ
-   Redis
-   RxJava
-   Spring Messaging-send link messages through message channels
-   Spring Web \(RestControllers, RestTemplates, WebAsyncTask\)
-   Standard Logging-a log is added to the current Span
-   WebSocket STOMP
-   Zuul

With the Spring Cloud component, perform the following steps:

**Note:** Download the [Demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerTracingDemo.zip), go to springMvcDemo/webmvc4-boot directory, and follow the instructions in Readme to run the program.

1.  Open pom.xml and add Jar dependencies.

    ```
    
            <dependency> <groupId>io.opentracing.contrib <artifactId>opentracing-spring-cloud-starter</artifactId> <version>0.2.0</version> </dependency> <dependency> <groupId>io.jaegertracing <artifactId>jaeger-client</artifactId> <version>0.31.0</version> </dependency> 
          
    ```

2.  Add OpenTracing Tracer Bean.

    **Note:** Please replace `<endpoint>` with corresponding endpoints of clients and regions on the Overview page of Tracing Analysis console. For more information about how to obtain endpoint information, please see [Obtain access point information](#tab2).

    ```
    
            @Bean public io.opentracing.Tracer tracer() { io.jaegertracing.Configuration config = new io.jaegertracing.Configuration("springFrontend"); io.jaegertracing.Configuration.SenderConfiguration sender = new io.jaegertracing.Configuration.SenderConfiguration(); sender.withEndpoint("<endpoint>"); config.withSampler(new io.jaegertracing.Configuration.SamplerConfiguration().withType("const").withParam(1)); config.withReporter(new io.jaegertracing.Configuration.ReporterConfiguration().withSender(sender).withMaxQueueSize(10000)); return config.getTracer(); } 
          
    ```


## Use gRPC to track Java applications

To use Jaeger to report Java application data to the tracing analysis console, you must first perform tracking. This example uses the gRPC component tracking.

Follow these steps to track data through the gRPC component.

**Note:** Download the [Demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerTracingDemo.zip), go to the grpcDemo directory, and run the program according to Readme.

1.  Open pom.xml and add Jar dependencies.

    ```
    
            <dependency> <groupId>io.opentracing.contrib <artifactId>opentracing-grpc</artifactId> <version>0.0.7</version> </dependency> 
          
    ```

2.  The Tracing object is initialized in the Server, and the ServerTracingInterceptor is created.

    ```
    
            import io.opentracing.Tracer; public class YourServer { private int port; private Server server; private final Tracer tracer; private void start() throws IOException { ServerTracingInterceptor tracingInterceptor = new ServerTracingInterceptor(this.tracer); // If GlobalTracer is used: // ServerTracingInterceptor tracingInterceptor = new ServerTracingInterceptor(); server = ServerBuilder.forPort(port) .addService(tracingInterceptor.intercept(someServiceDef)) .build() .start(); } } 
          
    ```

3.  Initialize the Tracing object on the Client, create a ClientTracingInterceptor, and block the Client Channel.

    ```
    
            import io.opentracing.Tracer; public class YourClient { private final ManagedChannel channel; private final GreeterGrpc.GreeterBlockingStub blockingStub; private final Tracer tracer; public YourClient(String host, int port) { channel = ManagedChannelBuilder.forAddress(host, port) .usePlaintext(true) .build(); ClientTracingInterceptor tracingInterceptor = new ClientTracingInterceptor(this.tracer); // If GlobalTracer is used: // ClientTracingInterceptor tracingInterceptor = new ClientTracingInterceptor(); blockingStub = GreeterGrpc.newBlockingStub(tracingInterceptor.intercept(channel)); } } 
          
    ```


## FAQ

Q: Why does the Demo program fail to be executed but no data is reported from the console?

A: Please debugging methods io.jaegertracing.thrift.internal.senders.httpsender.send\(processprocess,list <Span\> spans\) and view the report when the return value of. If a 403 error is reported, the access point is configured incorrectly, please check and modify.

[Use Zipkin to report Java application data](/intl.en-US/Preparations/Start monitoring Java applications/Use Zipkin to report Java application data.md)

[Jaeger official website](https://www.jaegertracing.io/)

[Jaeger Java Client](https://github.com/jaegertracing/jaeger-client-java)

[Component library of OpenTracing](https://github.com/opentracing-contrib)

[Spnew Cloud component of OpenTracing](https://github.com/opentracing-contrib/java-spring-cloud)

