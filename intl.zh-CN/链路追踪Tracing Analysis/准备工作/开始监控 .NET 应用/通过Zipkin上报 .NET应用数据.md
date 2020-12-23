# 通过Zipkin上报 .NET应用数据

Zipkin是一款开源的分布式实时数据追踪系统（Distributed Tracking System），由Twitter公司开发和贡献。其主要功能是聚合来自各个异构系统的实时监控数据。在链路追踪Tracing Analysis中，您可以通过Zipkin上报 .NET应用数据（此方法同样适用于使用C\#语言开发的应用）。





## 通过ASP.NET Core组件自动埋点

请按照以下步骤通过ASP.NET Core组件埋点。

**说明：** 下载[Demo源码](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinDotnetNetcore.zip)，并按照Readme的说明运行程序。

1.  安装NuGet包。

    ```
    // 添加以下组件。
    // zipkin4net.middleware.aspnetcore（aspnetcore中间件）
    // zipkin4net（追踪器）
    
    dotnet add  package zipkin4net.middleware.aspnetcore
    dotnet add  package zipkin4nete
    ```

2.  注册和启动Zipkin。

    ```
    lifetime.ApplicationStarted.Register(() => {
        TraceManager.SamplingRate = 1.0f;
        var logger = new TracingLogger(loggerFactory, "zipkin4net");
        // 在链路追踪控制台获取Zipkin Endpoint,注意Endpoint中不包含“/api/v2/spans”。
        var httpSender = new HttpZipkinSender("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_your_token", "application/json");
    
        var tracer = new ZipkinTracer(httpSender, new JSONSpanSerializer());
        TraceManager.RegisterTracer(tracer);
        TraceManager.Start(logger);
     });
    lifetime.ApplicationStopped.Register(() => TraceManager.Stop());
    app.UseTracing(applicationName);
    ```

3.  在发送Get/Post请求的HttpClient中添加tracinghandler（追踪处理者）。

    ```
    public override void ConfigureServices(IServiceCollection services)
    {
        services.AddHttpClient("Tracer").AddHttpMessageHandler(provider =>
            TracingHandler.WithoutInnerHandler(provider.GetService<IConfiguration>()["applicationName"]));
    }
    ```


## 通过Owin组件自动埋点

请按照以下步骤通过Owin组件埋点。

**说明：** 下载[Demo源码](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinDotnetOwin.zip)，并按照Readme的说明运行程序。

1.  安装NuGet包。

    ```
    // 添加以下组件。
    // zipkin4net.middleware.aspnetcore（aspnetcore中间件）
    // zipkin4net（追踪器）
    
    dotnet add  package zipkin4net.middleware.aspnetcore
    dotnet add  package zipkin4nete
    ```

2.  注册和启动Zipkin。

    ```
    // 设置Tracing。
    TraceManager.SamplingRate = 1.0f;
    var logger = new ConsoleLogger();
    // 在链路追踪控制台获取Zipkin Endpoint,注意Endpoint中不包含“/api/v2/spans”。var httpSender = new HttpZipkinSender("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_your_token", "application/json");
    
    var tracer = new ZipkinTracer(httpSender, new JSONSpanSerializer());
    TraceManager.RegisterTracer(tracer);
    TraceManager.Start(logger);
    
    //Stop TraceManager on app dispose
    var properties = new AppProperties(appBuilder.Properties);
    var token = properties.OnAppDisposing;
    
    if (token != CancellationToken.None)
    {
    token.Register(() =>
    {
    TraceManager.Stop();
    });
    }
    //
    
    // Setup Owin Middleware
    appBuilder.UseZipkinTracer(System.Configuration.ConfigurationManager.AppSettings["applicationName"]);
    //
                            
    ```

3.  在发送Get/Post请求的HttpClient中添加tracinghandler（追踪处理者）。

    ```
    using (var httpClient = new HttpClient(new TracingHandler(applicationName)))
        {
           var response = await httpClient.GetAsync(callServiceUrl);
           var content = await response.Content.ReadAsStringAsync();
    
           await context.Response.WriteAsync(content);
        }
    ```


## 手动埋点

要通过Zipkin将Java应用数据上报至链路追踪控制台，除了利用各种现有插件实现埋点的目的，也可以手动埋点。

**说明：** 下载[Demo源码](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinDotnetManual.zip)，并按照Readme的说明运行程序。

1.  安装NuGet包。

    ```
    // 添加zipkin4net（追踪器）。
    
    dotnet add  package zipkin4nete
    ```

2.  注册和启动Zipkin。

    ```
    TraceManager.SamplingRate = 1.0f;
    var logger = new ConsoleLogger();
    // 在链路追踪控制台获取Zipkin Endpoint,注意Endpoint中不包含“/api/v2/spans”。
    var httpSender = new HttpZipkinSender("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_your_token", "application/json");
    
    var tracer = new ZipkinTracer(httpSender, new JSONSpanSerializer());
    TraceManager.RegisterTracer(tracer);
    TraceManager.Start(logger);
    ```

3.  记录请求数据。

    ```
    var trace = Trace.Create();
    
    Trace.Current = trace;
    trace.Record(Annotations.ClientSend());
    
    trace.Record(Annotations.Rpc("client"));
    trace.Record(Annotations.Tag("mytag", "spanFrist"));
    trace.Record(Annotations.ServiceName("dotnetManual"));
    // ...do something
    testCall();
    
    trace.Record(Annotations.ClientRecv());
    ```

    **说明：**

    以上代码用于记录请求的根操作，如果需要记录请求的上一步和下一步操作，则需要调用ChildOf方法。示例：

    ```
    var trace = Trace.Current.Child();
    Trace.Current = trace;
    trace.Record(Annotations.ServerRecv());
    trace.Record(Annotations.Rpc("server"));
    trace.Record(Annotations.Tag("mytag", "spanSecond"));
    trace.Record(Annotations.ServiceName("dotnetManual"));
    // ...do something
    trace.Record(Annotations.ServerSend());
    ```

4.  为了快速排查问题，您可以为某个记录添加一些自定义标签，例如记录是否发生错误、请求的返回值等。

    ```
    tracer.activeSpan().setTag("http.status_code", "200");
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

    1.  在客户端调用Inject方法传入Context信息。

        ```
        _injector.Inject(clientTrace.Trace.CurrentSpan, request.Headers);
        ```

    2.  在服务端调用Extract方法解析Context信息。

        ```
        Ivar traceContext = traceExtractor.Extract(context.Request.Headers);
        var trace = traceContext == null ? Trace.Create() : Trace.CreateFromId(traceContext);
        ```


## 常见问题

问：Demo程序执行成功，为什么控制台上没有上报数据？

答：请检查senderConfiguration配置中的Endpoint是否填写正确。

```
// 在链路追踪控制台获取Zipkin Endpoint,注意Endpoint中不包含“/api/v2/spans”。
var httpSender = new HttpZipkinSender("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_your_token", "application/json");
```

[Zipkin官网](https://zipkin.io/)

[Zipkin的dotnet客户端](https://github.com/openzipkin/zipkin4net)

