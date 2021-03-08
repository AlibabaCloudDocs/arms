# 通过Jaeger上报Java应用数据

在使用链路追踪控制台追踪应用的链路数据之前，需要通过客户端将应用数据上报至链路追踪。本文介绍如何通过Jaeger客户端上报Java应用数据。

[Jaeger](https://www.jaegertracing.io/)是一款开源分布式追踪系统，兼容OpenTracing API，且已[加入CNCF开源组织](https://www.cncf.io/blog/2017/09/13/cncf-hosts-jaeger/)。其主要功能是聚合来自各个异构系统的实时监控数据。目前OpenTracing社区已有许多组件可支持各种Java框架，例如：

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

要通过Jaeger将Java应用数据上报至链路追踪控制台，首先需要完成埋点工作。您可以手动埋点，也可以利用各种现有插件实现埋点的目的。本文介绍以下三种埋点方法。

-   手动埋点
-   通过Spring Cloud组件埋点
-   通过gRPC组件埋点

## 为Java应用手动埋点

要通过Jaeger将Java应用数据上报至链路追踪控制台，首先需要完成埋点工作。本示例为手动埋点。

1.  下载[Demo工程](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerTracingDemo.zip)，进入manualDemo目录，并按照Readme的说明运行程序。

2.  打开pom.xml，添加对Jaeger客户端的依赖。

    ```
    <dependency>
        <groupId>io.jaegertracing</groupId>
        <artifactId>jaeger-client</artifactId>
        <version>0.31.0</version>
    </dependency>
    ```

3.  配置初始化参数并创建Tracer对象。

    Tracer对象可以用来创建Span对象以便记录分布式操作时间、通过Extract/Inject方法跨机器透传数据、或设置当前Span。Tracer对象还配置了上报数据的网关地址、本机IP地址、采样率、服务名等数据。您可以通过调整采样率来减少因上报数据产生的开销。

    **说明：** 请将`<endpoint>`替换成链路追踪控制台集群配置页面相应客户端和地域的接入点。获取接入点信息的方法，请参见前提条件中的[获取接入点信息](#tab2)。

    ```
    // 将manualDemo替换为您的应用名称。
    io.jaegertracing.Configuration config = new io.jaegertracing.Configuration("manualDemo");
    io.jaegertracing.Configuration.SenderConfiguration sender = new io.jaegertracing.Configuration.SenderConfiguration();
    // 将 <endpoint> 替换为控制台概览页面上相应客户端和地域的接入点。
    sender.withEndpoint("<endpoint>");
    config.withSampler(new io.jaegertracing.Configuration.SamplerConfiguration().withType("const").withParam(1));
    config.withReporter(new io.jaegertracing.Configuration.ReporterConfiguration().withSender(sender).withMaxQueueSize(10000));
    GlobalTracer.register(config.getTracer());
    ```

4.  记录请求数据。

    ```
    Tracer tracer = GlobalTracer.get();
    // 创建Span。
    Span span = tracer.buildSpan("parentSpan").withTag("myTag", "spanFirst").start();
    tracer.scopeManager().activate(span, false);
    tracer.activeSpan().setTag("methodName", "testTracing");
    // 业务逻辑。
    secondBiz();
    span.finish();
    ```

5.  上一步用于记录请求的根操作，如果需要记录请求的上一步和下一步操作，则需要传入上下文。

    ```
    Tracer tracer = GlobalTracer.get();
    Span parentspan = tracer.activeSpan();
    Tracer.SpanBuilder spanBuilder = tracer.buildSpan("childSpan").withTag("myTag", "spanSecond");
    if (parentspan !=null) {
        spanBuilder.asChildOf(parentspan).start();
    }
    Span childSpan = spanBuilder.start();
    tracer.scopeManager().activate(childSpan, false);
    // 业务逻辑。
    childSpan.finish();
    tracer.activeSpan().setTag("methodName", "testCall");
    ```

6.  为了方便排查问题，您可以为某个记录添加一些自定义标签（Tag），例如记录是否发生错误、请求的返回值等。

    ```
    tracer.activeSpan().setTag("methodName", "testCall");
    ```

7.  在分布式系统中发送RPC请求时会带上Tracing数据，包括TraceId、ParentSpanId、SpanId、Sampled等。您可以在HTTP请求中使用Extract/Inject方法在HTTP Request Headers上透传数据。总体流程如下：

    ```
       Client Span                                                Server Span
    ┌──────────────────┐                                       ┌──────────────────┐
    │                  │                                       │                  │
    │   TraceContext   │           Http Request Headers        │   TraceContext   │
    │ ┌──────────────┐ │          ┌───────────────────┐        │ ┌──────────────┐ │
    │ │ TraceId      │ │          │ X-B3-TraceId      │        │ │ TraceId      │ │
    │ │              │ │          │                   │        │ │              │ │
    │ │ ParentSpanId │ │ Inject   │ X-B3-ParentSpanId │Extract │ │ ParentSpanId │ │
    │ │              ├─┼─────────>│                   ├────────┼>│              │ │
    │ │ SpanId       │ │          │ X-B3-SpanId       │        │ │ SpanId       │ │
    │ │              │ │          │                   │        │ │              │ │
    │ │ Sampled      │ │          │ X-B3-Sampled      │        │ │ Sampled      │ │
    │ └──────────────┘ │          └───────────────────┘        │ └──────────────┘ │
    │                  │                                       │                  │
    └──────────────────┘                                       └──────────────────┘
    ```

    1.  在客户端调用Inject方法传入Context信息。

        ```
        private void attachTraceInfo(Tracer tracer, Span span, final Request request) {
                tracer.inject(span.context(), Format.Builtin.TEXT_MAP, new TextMap() {
                    @Override
                    public void put(String key, String value) {
                        request.setHeader(key, value);
                    }
                    @Override
                    public Iterator<Map.Entry<String, String>> iterator() {
                        throw new UnsupportedOperationException("TextMapInjectAdapter should only be used with Tracer.inject()");
                    }
                });
            }
        ```

    2.  在服务端调用Extract方法解析Context信息。

        ```
        protected Span extractTraceInfo(Request request, Tracer tracer) {
            Tracer.SpanBuilder spanBuilder = tracer.buildSpan("/api/xtrace/test03");
            try {
                SpanContext spanContext = tracer.extract(Format.Builtin.TEXT_MAP, new TextMapExtractAdapter(request.getAttachments()));
                if (spanContext != null) {
                    spanBuilder.asChildOf(spanContext);
                }
            } catch (Exception e) {
                spanBuilder.withTag("Error", "extract from request fail, error msg:" + e.getMessage());
            }
            return spanBuilder.start();
        }
                                        
        ```


## 通过Spring Cloud组件为Java应用埋点

要通过Jaeger将Java应用数据上报至链路追踪控制台，首先需要完成埋点工作。本示例为通过Spring Cloud组件埋点。Spring Cloud提供了下列组件的埋点：

-   @Async, @Scheduled, Executors
-   Feign, HystrixFeign
-   Hystrix
-   JDBC
-   JMS
-   Mongo
-   RabbitMQ
-   Redis
-   RxJava
-   Spring Messaging - 链路消息通过消息通道发送
-   Spring Web \(RestControllers, RestTemplates, WebAsyncTask\)
-   Standard Logging - 日志被添加至当前Span
-   WebSocket STOMP
-   Zuul

请按照以下步骤通过Spring Cloud组件埋点。

**说明：** 请下载[Demo工程](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerTracingDemo.zip)，进入springMvcDemo/webmvc4-boot目录，并按照Readme的说明运行程序。

1.  打开pom.xml，添加Jar包依赖。

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

2.  添加OpenTracing Tracer Bean。

    **说明：** 请将`<endpoint>`替换成链路追踪控制台集群配置页面相应客户端和地域的接入点。获取接入点信息的方法，请参见前提条件中的[获取接入点信息](#tab2)。

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


## 通过gRPC组件为Java应用埋点

要通过Jaeger将Java应用数据上报至链路追踪控制台，首先需要完成埋点工作。本示例为通过gRPC组件埋点。

请按照以下步骤通过gRPC组件埋点。

**说明：** 请下载[Demo工程](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerTracingDemo.zip)，进入grpcDemo目录，并按照Readme的说明运行程序。

1.  打开pom.xml，添加Jar包依赖。

    ```
    <dependency>
        <groupId>io.opentracing.contrib</groupId>
        <artifactId>opentracing-grpc</artifactId>
        <version>0.0.7</version>
    </dependency>
    ```

2.  在服务端初始化Tracing对象，创建ServerTracingInterceptor，并添加对Server的拦截。

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

3.  在客户端初始化Tracing对象，创建ClientTracingInterceptor，并添加对Client Channel的拦截。

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


## 常见问题

问：Demo程序执行成功，为什么控制台上没有上报数据？

答：请调试方法io.jaegertracing.thrift.internal.senders.HttpSender.send\(Process process, List<Span\> spans\)，并查看上报数据时的返回值。如果报403错误，则表明接入点配置不正确，请检查并修改。

## 更多信息

[通过Zipkin上报Java应用数据](/cn.zh-CN/准备工作/开始监控Java应用/通过Zipkin上报Java应用数据.md)

[Jaeger官网](https://www.jaegertracing.io/)

[Jaeger的Java Client](https://github.com/jaegertracing/jaeger-client-java)

[OpenTracing的组件库](https://github.com/opentracing-contrib)

[OpenTracing的Sping Cloud组件](https://github.com/opentracing-contrib/java-spring-cloud)

