# 通过Jaeger上报 .NET应用数据

在使用链路追踪控制台追踪应用的链路数据之前，需要通过客户端将应用数据上报至链路追踪。本文介绍如何通过Jaeger客户端上报 .NET应用数据（此方法同样适用于使用C\#语言开发的应用）。



[Jaeger](https://www.jaegertracing.io/)是Uber推出的一款开源分布式追踪系统，兼容OpenTracing API，已在Uber大规模使用，且已加入[CNCF开源组织](https://www.cncf.io/blog/2017/09/13/cncf-hosts-jaeger/)。其主要功能是聚合来自各个异构系统的实时监控数据。

目前OpenTracing社区已有许多组件可支持各种 .NET框架，例如：

-   [ASP.NET Core](https://github.com/opentracing-contrib/csharp-netcore)
-   [Entity Framework Core](https://github.com/opentracing-contrib/csharp-netcore)
-   [.NET Core BCL types \(HttpClient\)](https://github.com/opentracing-contrib/csharp-netcore)
-   [gRPC](https://github.com/opentracing-contrib/csharp-netcore)



## 通过netcore组件自动埋点

请按照以下步骤通过netcore组件埋点。

**说明：** 下载[Demo源码](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerDotNetDemo.zip)，并进入webapi.dotnetcore目录，按照Readme的说明运行程序。

1.  安装NuGet包。

    ```
    // 添加以下组件。
    // OpenTracing.Contrib.NetCore（aspnetcore中间件）
    // Jaeger（OpenTracing的实现组件）
    // Microsoft.Extensions.Logging.Console（日志组件）
    
    dotnet add  package OpenTracing.Contrib.NetCore
    dotnet add  package Jaeger
    dotnet add  package Microsoft.Extensions.Logging.Console
    ```

2.  用项目中Startup.cs里面的Configure方法注册中间件。

    ```
    // 注册OpenTracing组件埋点。
    services.AddOpenTracing();
    // 过滤httpclient采集中的Jaeger数据上报请求。
    var httpOption = new HttpHandlerDiagnosticOptions();
    httpOption.IgnorePatterns.Add(req => req.RequestUri.AbsolutePath.Contains("/api/traces"));
    services.AddSingleton(Options.Create(httpOption));
    ```

3.  初始化和注册Jaeger。

    ```
    // 添加Jaeger Tracer。
    services.AddSingleton<ITracer>(serviceProvider =>
    {
        string serviceName = serviceProvider.GetRequiredService<IHostingEnvironment>().ApplicationName;
        ILoggerFactory loggerFactory = serviceProvider.GetRequiredService<ILoggerFactory>();
         Configuration.SenderConfiguration senderConfiguration = new Configuration.SenderConfiguration(loggerFactory)
         // 在链路追踪控制台获取Jaeger Endpoint。
              .WithEndpoint("http://tracing-analysis-dc-sz.aliyuncs.com/adapt_your_token/api/traces");
    
          // This will log to a default localhost installation of Jaeger.
          var tracer = new Tracer.Builder(serviceName)
              .WithSampler(new ConstSampler(true))
              .WithReporter(new RemoteReporter.Builder().WithSender(senderConfiguration.GetSender()).Build())
               .Build();
    
          // Allows code that can't use DI to also access the tracer.
          GlobalTracer.Register(tracer);
    
          return tracer;
    });
    ```


## 通过gRPC组件自动埋点

请按照以下步骤通过gRPC组件埋点。

**说明：** 下载[Demo源码](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerDotNetDemo.zip)，并按照Readme的说明运行程序。

1.  安装NuGet包。

    ```
    // 添加以下组件。
    // OpenTracing.Contrib.Grpc（gRPC中间件）
    // Jaeger（OpenTracing的实现组件）
    // Microsoft.Extensions.Logging.Console（日志组件）
    
    dotnet add  package OpenTracing.Contrib.grpc
    dotnet add  package Jaeger
    ```

2.  初始化ITracer对象。

    ```
    public static Tracer InitTracer(string serviceName, ILoggerFactory loggerFactory)
            {
                Configuration.SamplerConfiguration samplerConfiguration = new Configuration.SamplerConfiguration(loggerFactory)
                    .WithType(ConstSampler.Type)
                    .WithParam(1);
                Configuration.SenderConfiguration senderConfiguration = new Configuration.SenderConfiguration(loggerFactory)
                        // 在链路追踪控制台获取Jaeger Endpoint。
                       .WithEndpoint("http://tracing-analysis-dc-sz.aliyuncs.com/adapt_your_token/api/traces");
                Configuration.ReporterConfiguration reporterConfiguration = new Configuration.ReporterConfiguration(loggerFactory)
                    .WithSender(senderConfiguration);
    
                return (Tracer)new Configuration(serviceName, loggerFactory)
                    .WithSampler(samplerConfiguration)
                    .WithReporter(reporterConfiguration)
                    .GetTracer();
            }
    ```

3.  在服务端埋点。构建用于埋点的ServerTracingInterceptor对象，并将ServerTracingInterceptor绑定到服务上。

    ```
    ILoggerFactory loggerFactory = new LoggerFactory().AddConsole();
    ITracer tracer = TracingHelper.InitTracer("dotnetGrpcServer", loggerFactory);
    ServerTracingInterceptor tracingInterceptor = new ServerTracingInterceptor(tracer);
    Server server = new Server
     {
        Services = { Greeter.BindService(new GreeterImpl()).Intercept(tracingInterceptor) },
         Ports = { new ServerPort("localhost", Port, ServerCredentials.Insecure) }
     };
    ```

4.  在客户端埋点。构建用于埋点的ClientTracingInterceptor对象，并将ClientTracingInterceptor绑定到Channel上。

    ```
    ILoggerFactory loggerFactory = new LoggerFactory().AddConsole();
    ITracer tracer = TracingHelper.InitTracer("dotnetGrpcClient", loggerFactory);
    ClientTracingInterceptor tracingInterceptor = new ClientTracingInterceptor(tracer);
    Channel channel = new Channel("127.0.0.1:50051", ChannelCredentials.Insecure);
    
    var client = new Greeter.GreeterClient(channel.Intercept(tracingInterceptor));
    ```


## 手动埋点

要通过Jaeger将 .NET应用数据上报至链路追踪控制台，除了利用各种现有插件实现埋点的目的，也可以手动埋点。

**说明：** 下载[Demo源码](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerDotNetDemo.zip)，并进入ManualDemo目录，按照Readme的说明运行程序。

1.  安装NuGet包。

    ```
    // Jaeger（OpenTracing的实现组件）
    // Microsoft.Extensions.Logging.Console（日志组件）
    
    dotnet add  package Microsoft.Extensions.Logging.Console
    dotnet add  package Jaeger
    ```

2.  构建ITracer对象。ITracer是OpenTracing定义的对象，我们用Jaeger来构建该对象（配置网关、采样率等）。

    ```
    public static ITracer InitTracer(string serviceName, ILoggerFactory loggerFactory)
     {
        Configuration.SamplerConfiguration samplerConfiguration = new Configuration.SamplerConfiguration(loggerFactory)
              .WithType(ConstSampler.Type)
              .WithParam(1);
        Configuration.SenderConfiguration senderConfiguration = new Configuration.SenderConfiguration(loggerFactory)
               // 在链路追踪控制台获取Jaeger Endpoint。
              .WithEndpoint("http://tracing-analysis-dc-sz.aliyuncs.com/adapt_your_token/api/traces");
    
       Configuration.ReporterConfiguration reporterConfiguration = new Configuration.ReporterConfiguration(loggerFactory)
              .WithSender(senderConfiguration);
    
       return (Tracer)new Configuration(serviceName, loggerFactory)
              .WithSampler(samplerConfiguration)
              .WithReporter(reporterConfiguration)
            .GetTracer();
    }
    ```

3.  将ITreacer注册到GlobalTracer中，方便调用代码。

    ```
    GlobalTracer.Register(InitTracer("dotnetManualDemo", loggerFactory ));
    ```

4.  记录请求数据。

    ```
    ITracer tracer = GlobalTracer.Instance;
    ISpan span = tracer.BuildSpan("parentSpan").WithTag("mytag","parentSapn").Start();
    tracer.ScopeManager.Activate(span, false);
    // ...do something
    ..
    span.Finish();
    ```

    **说明：** 以上代码用于记录请求的根操作，如果需要记录请求的上一步和下一步操作，则需要调用AsChildOf方法。

    示例：

    ```
    ITracer tracer = GlobalTracer.Instance;
    ISpan parentSpan = tracer.ActiveSpan;
    ISpan childSpan =tracer.BuildSpan("childSpan").AsChildOf(parentSpan).WithTag("mytag", "spanSecond").Start();
    tracer.ScopeManager.Activate(childSpan, false);
    // ... do something。。。childSpan.Finish();
    ```

5.  （可选）为了快速排查问题，您可以为某个记录添加一些自定义标签，例如记录是否发生错误、请求的返回值等。

    ```
    tracer.activeSpan().setTag("http.status_code", "200");
    ```

6.  在分布式系统中发送RPC请求时会带上Tracing数据，包括TraceId、ParentSpanId、SpanId、Sampled等。您可以在HTTP请求中使用Extract/Inject方法在HTTP Request Headers上透传数据。总体流程如下：

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
        Tracer.Inject(span.Context, BuiltinFormats.HttpHeaders, new HttpHeadersInjectAdapter(request.Headers));
        ```

    2.  在服务端调用Extract方法解析Context信息。

        ```
        ISpanContext extractedSpanContext = _tracer.Extract(BuiltinFormats.HttpHeaders, new RequestHeadersExtractAdapter(request.Headers));
        ISpan childSpan = _tracer.BuildSpan(operationName).AsChildOf(extractedSpanContext);
        ```


## 常见问题

问：Demo程序执行成功，为什么控制台上没有上报数据？

答：请检查senderConfiguration配置中的Endpoint是否填写正确。

```
Configuration.SenderConfiguration senderConfiguration = new Configuration.SenderConfiguration(loggerFactory)
           // 在链路追踪控制台获取Jaeger Endpoint。
          .WithEndpoint("http://tracing-analysis-dc-sz.aliyuncs.com/adapt_your_token/api/traces");
```

## 更多信息

[Jaeger官网](https://www.jaegertracing.io/)

[jaeger-client-csharp](https://github.com/jaegertracing/jaeger-client-csharp)

[Jaeger对asp.net core组件库](https://github.com/opentracing-contrib/csharp-netcore)

[Jaeger对gRPC埋点组件](https://github.com/opentracing-contrib/csharp-grpc)

