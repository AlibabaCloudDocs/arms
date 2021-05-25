# Use Jaeger to report .NET application data

Before you can view the trace data of your application in the Tracing Analysis console, use a client to report the trace data to Tracing Analysis. This topic describes how to use Jaeger to report the data of .NET applications. The method also applies to C\# applications.

[Jaeger](https://www.jaegertracing.io/) is an open source distributed tracing system. This tracing system is created and used at Uber. It is compatible with the OpenTracing API and is a member of the [Cloud Native Computing Foundation \(CNCF\)](https://www.cncf.io/blog/2017/09/13/cncf-hosts-jaeger/). Jaeger is used to aggregate real-time monitoring data that is collected from multiple heterogeneous systems.

The OpenTracing community provides multiple components that support the following .NET Framework:

-   [ASP.NET Core](https://github.com/opentracing-contrib/csharp-netcore)
-   [Entity Framework Core](https://github.com/opentracing-contrib/csharp-netcore)
-   [.NET Core BCL types \(HttpClient\)](https://github.com/opentracing-contrib/csharp-netcore)
-   [gRPC](https://github.com/opentracing-contrib/csharp-netcore)

## Use ASP.NET Core to instrument a .NET application

Use ASP.NET Core to instrument an application by performing the following steps:

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerDotNetDemo.zip). Go to the ManualDemo directory and run the program as instructed in the README.md file.

1.  Install NuGet packages.

    ```
    // Adds the following components: 
    // OpenTracing.Contrib.NetCore: the ASP.NET Core middleware
    // Jaeger: an implementation component of OpenTracing
    // Microsoft.Extensions.Logging.Console: a log component
    
    dotnet add  package OpenTracing.Contrib.NetCore
    dotnet add  package Jaeger
    dotnet add  package Microsoft.Extensions.Logging.Console
    ```

2.  Use the Configure method in the Startup.cs file of the project to register the middleware.

    ```
    // Registers OpenTracing.Contrib.NetCore to instrument the application. 
    services.AddOpenTracing();
    // Filters requests that are collected by HttpClient to obtain requests for using Jaeger to report data. 
    var httpOption = new HttpHandlerDiagnosticOptions();
    httpOption.IgnorePatterns.Add(req => req.RequestUri.AbsolutePath.Contains("/api/traces"));
    services.AddSingleton(Options.Create(httpOption));
    ```

3.  Initialize and register Jaeger.

    ```
    // Adds a Jaeger tracer. 
    services.AddSingleton<ITracer>(serviceProvider =>
    {
        string serviceName = serviceProvider.GetRequiredService<IHostingEnvironment>().ApplicationName;
        ILoggerFactory loggerFactory = serviceProvider.GetRequiredService<ILoggerFactory>();
         Configuration.SenderConfiguration senderConfiguration = new Configuration.SenderConfiguration(loggerFactory)
         // Obtains the Jaeger endpoint in the Tracing Analysis console. 
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


## Use gRPC to instrument a .NET application

Use gRPC to instrument an application by performing the following steps:

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerDotNetDemo.zip) and run the program as instructed in the README.md file.

1.  Install NuGet packages.

    ```
    // Adds the following components: 
    // OpenTracing.Contrib.Grpc: the gRPC middleware
    // Jaeger: an implementation component of OpenTracing
    // Microsoft.Extensions.Logging.Console: a log component
    
    dotnet add  package OpenTracing.Contrib.grpc
    dotnet add  package Jaeger
    ```

2.  Create an ITracer object.

    ```
    public static Tracer InitTracer(string serviceName, ILoggerFactory loggerFactory)
            {
                Configuration.SamplerConfiguration samplerConfiguration = new Configuration.SamplerConfiguration(loggerFactory)
                    .WithType(ConstSampler.Type)
                    .WithParam(1);
                Configuration.SenderConfiguration senderConfiguration = new Configuration.SenderConfiguration(loggerFactory)
                        // Obtains the Jaeger endpoint in the Tracing Analysis console. 
                       .WithEndpoint("http://tracing-analysis-dc-sz.aliyuncs.com/adapt_your_token/api/traces");
                Configuration.ReporterConfiguration reporterConfiguration = new Configuration.ReporterConfiguration(loggerFactory)
                    .WithSender(senderConfiguration);
    
                return (Tracer)new Configuration(serviceName, loggerFactory)
                    .WithSampler(samplerConfiguration)
                    .WithReporter(reporterConfiguration)
                    .GetTracer();
            }
    ```

3.  Add instrumentation on the server. Create the ServerTracingInterceptor object that is used to add instrumentation and bind the ServerTracingInterceptor object to the specified service.

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

4.  Add instrumentation on the client. Create the ClientTracingInterceptor object that is used to add instrumentation and bind the ClientTracingInterceptor object to the specified channel.

    ```
    ILoggerFactory loggerFactory = new LoggerFactory().AddConsole();
    ITracer tracer = TracingHelper.InitTracer("dotnetGrpcClient", loggerFactory);
    ClientTracingInterceptor tracingInterceptor = new ClientTracingInterceptor(tracer);
    Channel channel = new Channel("127.0.0.1:50051", ChannelCredentials.Insecure);
    
    var client = new Greeter.GreeterClient(channel.Intercept(tracingInterceptor));
    ```


## Manually instrument a .NET application

The preceding sections describe how to use existing components to instrument .NET applications. You can also manually instrument .NET applications. In this case, you can use Jaeger to report the data of the applications to the Tracing Analysis console.

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerDotNetDemo.zip). Go to the ManualDemo directory and run the program as instructed in the README.md file.

1.  Install NuGet packages.

    ```
    // Jaeger: an implementation component of OpenTracing
    // Microsoft.Extensions.Logging.Console: a log component
    
    dotnet add  package Microsoft.Extensions.Logging.Console
    dotnet add  package Jaeger
    ```

2.  Create an ITracer object. The ITracer object is an object defined by OpenTracing. You can use Jaeger to create this object. When you create this object, you must configure the endpoint and sample rate.

    ```
    public static ITracer InitTracer(string serviceName, ILoggerFactory loggerFactory)
     {
        Configuration.SamplerConfiguration samplerConfiguration = new Configuration.SamplerConfiguration(loggerFactory)
              .WithType(ConstSampler.Type)
              .WithParam(1);
        Configuration.SenderConfiguration senderConfiguration = new Configuration.SenderConfiguration(loggerFactory)
               // Obtains the Jaeger endpoint in the Tracing Analysis console. 
              .WithEndpoint("http://tracing-analysis-dc-sz.aliyuncs.com/adapt_your_token/api/traces");
    
       Configuration.ReporterConfiguration reporterConfiguration = new Configuration.ReporterConfiguration(loggerFactory)
              .WithSender(senderConfiguration);
    
       return (Tracer)new Configuration(serviceName, loggerFactory)
              .WithSampler(samplerConfiguration)
              .WithReporter(reporterConfiguration)
            .GetTracer();
    }
    ```

3.  Register the ITracer object with GlobalTracer to facilitate code calling.

    ```
    GlobalTracer.Register(InitTracer("dotnetManualDemo", loggerFactory ));
    ```

4.  Record the request data.

    ```
    ITracer tracer = GlobalTracer.Instance;
    ISpan span = tracer.BuildSpan("parentSpan").WithTag("mytag","parentSapn").Start();
    tracer.ScopeManager.Activate(span, false);
    // ... do something
    span.Finish();
    ```

    **Note:** You can run the preceding code to record the root operation of a request. If you want to record the previous and next operations of the request, call the AsChildOf method.

    Sample code:

    ```
    ITracer tracer = GlobalTracer.Instance;
    ISpan parentSpan = tracer.ActiveSpan;
    ISpan childSpan =tracer.BuildSpan("childSpan").AsChildOf(parentSpan).WithTag("mytag", "spanSecond").Start();
    tracer.ScopeManager.Activate(childSpan, false);
    // ... do something
    childSpan.Finish();
    ```

5.  Optional. Add custom tags to a span for quick troubleshooting. For example, you can add a custom tag to record the return value of a request or check whether an error occurs.

    ```
    tracer.activeSpan().setTag("http.status_code", "200");
    ```

6.  In a distributed system, remote procedure call \(RPC\) requests are sent together with trace data. Trace data contains the values of the TraceId, ParentSpanId, SpanId, and Sampled parameters. You can call the Extract or Inject method to specify data in HTTP request headers. The following example shows the entire process:

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

    1.  Call the Inject method on the client to specify the context information.

        ```
        Tracer.Inject(span.Context, BuiltinFormats.HttpHeaders, new HttpHeadersInjectAdapter(request.Headers));
        ```

    2.  Call the Extract method on the server to extract the context information.

        ```
        ISpanContext extractedSpanContext = _tracer.Extract(BuiltinFormats.HttpHeaders, new RequestHeadersExtractAdapter(request.Headers));
        ISpan childSpan = _tracer.BuildSpan(operationName).AsChildOf(extractedSpanContext);
        ```


## FAQ

Q: What can I do if no data is reported to the console after I run the demo program?

A: Check whether the endpoint in senderConfiguration is valid.

```
Configuration.SenderConfiguration senderConfiguration = new Configuration.SenderConfiguration(loggerFactory)
           // Obtains the Jaeger endpoint in the Tracing Analysis console. 
          .WithEndpoint("http://tracing-analysis-dc-sz.aliyuncs.com/adapt_your_token/api/traces");
```

[Jaeger official website](https://www.jaegertracing.io/)

[jaeger-client-csharp](https://github.com/jaegertracing/jaeger-client-csharp)

[ASP.NET Core component library for Jaeger](https://github.com/opentracing-contrib/csharp-netcore)

[gRPC components that are used to add instrumentation for Jaeger](https://github.com/opentracing-contrib/csharp-grpc)

