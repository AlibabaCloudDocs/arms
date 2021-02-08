# Use Jaeger to report Java application data

Before you can view the trace data of your application in the Tracing Analysis console, you must use a client to report the trace data to Tracing Analysis. This topic shows you how to use Jaeger to report Java application data.



[Jaeger](https://www.jaegertracing.io/) is an open source distributed tracing system. It is compatible with the OpenTracing API and has joined the [Cloud Native Computing Foundation \(CNCF\)](https://www.cncf.io/blog/2017/09/13/cncf-hosts-jaeger/). Jaeger is used to aggregate real-time monitoring data that is collected from multiple heterogeneous systems. The OpenTracing community provides many components that support the following Java frameworks:

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

To use Jaeger to report Java application data to the Tracing Analysis console, you must first instrument your application. You can instrument the application manually or by using existing components. This topic describes three methods that you can use to instrument an application:

-   Manually instrument an application.
-   Use Spring Cloud to instrument an application.
-   Use gRPC to instrument an application.



## Manual tracking for Java applications

To use Jaeger to report Java application data to the link tracking console, you must complete tracking. This example uses manual instrumentation.

1.  Download the[Demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerTracingDemo.zip) , enter pathmanualDemo, and run the program according to the Readme instructions.

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


## Use Spring Cloud to instrument a Java application

To use Jaeger to report Java application data to the Tracing Analysis console, you must first instrument your application. This example shows you how to use Spring Cloud to instrument an application. You can use Spring Cloud to instrument the following applications:

-   @Async, @Scheduled, Executors
-   Feign, HystrixFeign
-   Hystrix
-   JDBC
-   JMS
-   Mongo
-   RabbitMQ
-   Redis
-   RxJava
-   Spring Messaging: Trace messages are sent by using message channels.
-   Spring Web \(RestControllers, RestTemplates, WebAsyncTask\)
-   Standard Logging: Logs are added to the current span.
-   WebSocket STOMP
-   Zuul

Perform the following steps to use Spring Cloud to instrument an application:

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerTracingDemo.zip). Go to the springMvcDemo/webmvc4-boot directory and run the program as instructed in the README.md file.

1.  Open the pom.xml file and add JAR dependencies.

    ```
    <dependency>
       <groupId>io.opentracing.contrib</groupId>
      <artifactId>opentracing-spring-cloud-starter</artifactId>
      <version>0.2.0</version>
    </dependency>
    <dependency>
      <groupId>io.jaegertracing</groupId>
      <artifactId>jaeger-client</artifactId>
      <version>0.31.0</version>
    </dependency>
    ```

2.  Add an OpenTracing Tracer bean.

    **Note:** Please replace `<endpoint>` with corresponding endpoints of clients and regions on the Overview page of Tracing Analysis console. For more information about how to obtain endpoint information, please see [Obtain access point information](#tab2).

    ```
    @Bean
    public io.opentracing.Tracer tracer() {
        io.jaegertracing.Configuration config = new io.jaegertracing.Configuration("springFrontend");
        io.jaegertracing.Configuration.SenderConfiguration sender = new io.jaegertracing.Configuration.SenderConfiguration();
        sender.withEndpoint("<endpoint>");
        config.withSampler(new io.jaegertracing.Configuration.SamplerConfiguration().withType("const").withParam(1));
        config.withReporter(new io.jaegertracing.Configuration.ReporterConfiguration().withSender(sender).withMaxQueueSize(10000));
        return config.getTracer();
    }
    ```


## Use gRPC to instrument a Java application

To use Jaeger to report Java application data to the Tracing Analysis console, you must first instrument your application. This example shows you how to use gRPC to instrument an application.

Perform the following steps to use gRPC to instrument an application:

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerTracingDemo.zip). Go to the grpcDemo directory and run the program as instructed in the README.md file.

1.  Open the pom.xml file and add JAR dependencies.

    ```
    <dependency>
        <groupId>io.opentracing.contrib</groupId>
        <artifactId>opentracing-grpc</artifactId>
        <version>0.0.7</version>
    </dependency>
    ```

2.  Initialize the Tracer object on the server, create the ServerTracingInterceptor class, and then add an interceptor to the server.

    ```
    import io.opentracing.Tracer;
    
        public class YourServer {
    
            private int port;
            private Server server;
            private final Tracer tracer;
    
            private void start() throws IOException {
                ServerTracingInterceptor tracingInterceptor = new ServerTracingInterceptor(this.tracer);
    
                // If GlobalTracer is used: 
                // ServerTracingInterceptor tracingInterceptor = new ServerTracingInterceptor();
    
                server = ServerBuilder.forPort(port)
                    .addService(tracingInterceptor.intercept(someServiceDef))
                    .build()
                    .start();
            }
        }
    ```

3.  Initialize the Tracer object on the client, create the ClientTracingInterceptor class, and then add an interceptor to the client.

    ```
    import io.opentracing.Tracer;
    
        public class YourClient {
    
            private final ManagedChannel channel;
            private final GreeterGrpc.GreeterBlockingStub blockingStub;
            private final Tracer tracer;
    
            public YourClient(String host, int port) {
    
                channel = ManagedChannelBuilder.forAddress(host, port)
                    .usePlaintext(true)
                    .build();
    
                ClientTracingInterceptor tracingInterceptor = new ClientTracingInterceptor(this.tracer);
    
                // If GlobalTracer is used: 
                // ClientTracingInterceptor tracingInterceptor = new ClientTracingInterceptor();
    
                blockingStub = GreeterGrpc.newBlockingStub(tracingInterceptor.intercept(channel));
            }
        }
                            
    ```


## FAQ

Q: Why is no data reported to the console after the demo program is run?

A: Debug the io.jaegertracing.thrift.internal.senders.HttpSender.send\(Process process, List<Span\> spans\) method and check the return value of data reporting. If an HTTP 403 error is returned, you have specified an invalid endpoint. Change the endpoint to a valid one.

[Use Zipkin to report Java application data](/intl.en-US/Before you begin/Monitor Java applications/Use Zipkin to report Java application data.md)

[Jaeger official website](https://www.jaegertracing.io/)

[Jaeger client for Java](https://github.com/jaegertracing/jaeger-client-java)

[Component library of OpenTracing](https://github.com/opentracing-contrib)

[OpenTracing Spring Cloud](https://github.com/opentracing-contrib/java-spring-cloud)

