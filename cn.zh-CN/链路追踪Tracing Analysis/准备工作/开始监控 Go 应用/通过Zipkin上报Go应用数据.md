# 通过Zipkin上报Go应用数据

Zipkin是一款开源的分布式实时数据追踪系统（Distributed Tracking System），由Twitter公司开发和贡献。其主要功能是聚合来自各个异构系统的实时监控数据。在链路追踪Tracing Analysis中，您可以通过Zipkin上报Go应用数据。





## 代码埋点

要通过Zipkin将Go应用数据上报至链路追踪控制台，首先需要完成埋点工作。

1.  添加组件依赖。

    ```
    [[constraint]]
      name = "github.com/openzipkin/zipkin-go"
      version = "0.1.1"
    
    [[constraint]]
      name = "github.com/gorilla/mux"
      version = "1.6.2"
    ```

2.  创建Tracer。Tracer对象可以用来创建Span对象（记录分布式操作时间）。Tracer对象还配置了上报数据的网关地址、本机IP、采样频率等数据，您可以通过调整采样率来减少因上报数据产生的开销。

    ```
    func getTracer(serviceName string, ip string) *zipkin.Tracer {
      // create a reporter to be used by the tracer
      reporter := httpreporter.NewReporter("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_aokcdqnxyz@123456ff_abcdef123@abcdef123/api/v2/spans")
      // set-up the local endpoint for our service
      endpoint, _ := zipkin.NewEndpoint(serviceName, ip)
      // set-up our sampling strategy
      sampler := zipkin.NewModuloSampler(1)
      // initialize the tracer
      tracer, _ := zipkin.NewTracer(
        reporter,
        zipkin.WithLocalEndpoint(endpoint),
        zipkin.WithSampler(sampler),
      )
      return tracer;
    }
    ```

3.  记录请求数据。

    ```
    // tracer can now be used to create spans.
    span := tracer.StartSpan("some_operation")
    // ... do some work ...
    span.Finish()
    // Output:
    ```

    **说明：**

    以上代码用于记录请求的根操作，如果需要记录请求的上一步和下一步操作，则需要传入上下文。示例：

    ```
    childSpan := tracer.StartSpan("some_operation2", zipkin.Parent(span.Context()))
        // ... do some work ...
    childSpan.Finish()
    ```

4.  为了快速排查问题，您可以为某个记录添加一些自定义标签，例如记录是否发生错误、请求的返回值等。

    ```
    childSpan.Tag("http.status_code", statusCode)
    ```

5.  在分布式系统中发送RPC请求时会带上Tracing数据，包括TraceId、ParentSpanId、SpanId、Sampled等。您可以在HTTP请求中使用Extract/Inject方法在HTTP Request Headers上透传数据。总体流程如下：

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

    **说明：** 目前Zipkin已有组件支持以HTTP、gRPC这两种RPC协议透传Context信息。

    1.  在客户端调用Inject方法传入Context信息。

        ```
        req, _ := http.NewRequest("GET", "/", nil)
        // configure a function that injects a trace context into a reques
        injector := b3.InjectHTTP(req)
        injector(sp.Context())
        ```

    2.  在服务端调用Extract方法解析Context信息。

        ```
        req, _ := http.NewRequest("GET", "/", nil)
                b3.InjectHTTP(req)(sp.Context())
        
                b.ResetTimer()
                _ = b3.ExtractHTTP(copyRequest(req))
        ```


## 快速入门

接下来以一个示例演示如何通过Zipkin上报Go应用数据。

1.  下载[示例文件](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingGoTest.zip)。

2.  在utils.go文件中修改上报数据的网关地址（endpointURL）。

    **说明：** 请将`<endpoint>`替换成链路追踪控制台概览页面上相应客户端和相应地域的接入点。关于获取接入点信息的方法，请参见前提条件中的[获取接入点信息](#tab2)。

3.  安装依赖包。

    ```
    dep ensure
    ```

4.  运行测试程序。

    ```
    go run main.go
    ```

5.  在[链路追踪控制台](https://tracing-analysis.console.aliyun.com/)查看上报的数据。


## 常见问题

问：为什么按照快速入门的步骤操作没有上报数据？

答：请检查运行过程中是否有提示，并检查endpoint\_url的配置是否正确。例如，错误`failed the request with status code 403`表明用户名或密码不正确。

## 更多信息

[Zipkin官网](https://zipkin.io/)

[Zipkin-go源码](https://github.com/openzipkin/zipkin-go)

