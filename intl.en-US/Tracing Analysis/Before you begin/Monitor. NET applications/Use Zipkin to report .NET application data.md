# Use Zipkin to report .NET application data

Zipkin is a distributed tracing system. It is an open source system that is developed by Twitter to trace real-time data. Zipkin is used to aggregate real-time monitoring data that is collected from multiple heterogeneous systems. You can use Zipkin to report the data of .NET applications in Tracing Analysis. The method also applies to C\# applications.



## Use ASP.NET Core to instrument a .NET application

Perform the following steps to use ASP.NET Core to instrument an application:

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinDotnetNetcore.zip) and run the program as instructed in the README.md file.

1.  Install NuGet packages.

    ```
    // Add the following components:
    // zipkin4net.middleware.aspnetcore, the ASP.NET Core middleware
    // zipkin4net, a tracer
    
    dotnet add  package zipkin4net.middleware.aspnetcore
    dotnet add  package zipkin4nete
    ```

2.  Register and start Zipkin.

    ```
    lifetime.ApplicationStarted.Register(() => {
        TraceManager.SamplingRate = 1.0f;
        var logger = new TracingLogger(loggerFactory, "zipkin4net");
        // Obtain the Zipkin endpoint in the Tracing Analysis console. Note that the endpoint does not contain /api/v2/spans.
        var httpSender = new HttpZipkinSender("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_your_token", "application/json");
    
        var tracer = new ZipkinTracer(httpSender, new JSONSpanSerializer());
        TraceManager.RegisterTracer(tracer);
        TraceManager.Start(logger);
     });
    lifetime.ApplicationStopped.Register(() => TraceManager.Stop());
    app.UseTracing(applicationName);
    ```

3.  Add TracingHandler to HttpClient that sends GET or POST requests.

    ```
    public override void ConfigureServices(IServiceCollection services)
    {
        services.AddHttpClient("Tracer").AddHttpMessageHandler(provider =>
            TracingHandler.WithoutInnerHandler(provider.GetService<IConfiguration>()["applicationName"]));
    }
    ```


## Use OWIN to instrument a .NET application

Perform the following steps to use Open Web Interface for .NET \(OWIN\) to instrument an application:

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinDotnetOwin.zip) and run the program as instructed in the README.md file.

1.  Install NuGet packages.

    ```
    // Add the following components:
    // zipkin4net.middleware.aspnetcore, the ASP.NET Core middleware
    // zipkin4net, a tracer
    
    dotnet add  package zipkin4net.middleware.aspnetcore
    dotnet add  package zipkin4nete
    ```

2.  Register and start Zipkin.

    ```
    // Configure tracing.
    TraceManager.SamplingRate = 1.0f;
    var logger = new ConsoleLogger();
    // Obtain the Zipkin endpoint in the Tracing Analysis console. Note that the endpoint does not contain /api/v2/spans.
    var httpSender = new HttpZipkinSender("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_your_token", "application/json");
    
    var tracer = new ZipkinTracer(httpSender, new JSONSpanSerializer());
    TraceManager.RegisterTracer(tracer);
    TraceManager.Start(logger);
    
    //Stop TraceManager on app dispose
    var properties = new AppProperties(appBuilder.Properties);
    var token = properties.OnAppDisposing;
    
    if (token ! = CancellationToken.None)
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

3.  Add TracingHandler to HttpClient that sends GET or POST requests.

    ```
    using (var httpClient = new HttpClient(new TracingHandler(applicationName)))
        {
           var response = await httpClient.GetAsync(callServiceUrl);
           var content = await response.Content.ReadAsStringAsync();
    
           await context.Response.WriteAsync(content);
        }
    ```


## Manually instrument a .NET application

The preceding sections describe how to use existing components to instrument .NET applications. You can also manually instrument .NET applications so that you can use Zipkin to report the data of the applications to the Tracing Analysis console.

**Note:** Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinDotnetManual.zip) and run the program as instructed in the README.md file.

1.  Install a NuGet package.

    ```
    // Add zipkin4net, a tracer.
    
    dotnet add  package zipkin4nete
    ```

2.  Register and start Zipkin.

    ```
    TraceManager.SamplingRate = 1.0f;
    var logger = new ConsoleLogger();
    // Obtain the Zipkin endpoint in the Tracing Analysis console. Note that the endpoint does not contain /api/v2/spans.
    var httpSender = new HttpZipkinSender("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_your_token", "application/json");
    
    var tracer = new ZipkinTracer(httpSender, new JSONSpanSerializer());
    TraceManager.RegisterTracer(tracer);
    TraceManager.Start(logger);
    ```

3.  Record the request data.

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

    **Note:**

    You can run the preceding code to record the root operation of a request. If you need to record the previous and next operations of the request, call the Child method. Sample code:

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

4.  Add custom tags to a span for quick troubleshooting. For example, you can add a custom tag to check whether an error occurs or to record the return value of a request.

    ```
    tracer.activeSpan().setTag("http.status_code", "200");
    ```

5.  In a distributed system, remote procedure call \(RPC\) requests are sent along with trace data. Trace data contains the values of the TraceId, ParentSpanId, SpanId, and Sampled parameters. You can call the Extract or Inject method to pass data in HTTP request headers. The following figure shows the overall process.

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

    1.  Call the Inject method on the client to inject the context information.

        ```
        _injector.Inject(clientTrace.Trace.CurrentSpan, request.Headers);
        ```

    2.  Call the Extract method on the server to extract the context information.

        ```
        Ivar traceContext = traceExtractor.Extract(context.Request.Headers);
        var trace = traceContext == null ? Trace.Create() : Trace.CreateFromId(traceContext);
        ```


## FAQ

Q: Why is no data reported to the console after the demo program is run?

A: Check whether you have configured the correct endpoint in senderConfiguration.

```
// Obtain the Zipkin endpoint in the Tracing Analysis console. Note that the endpoint does not contain /api/v2/spans.
var httpSender = new HttpZipkinSender("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_your_token", "application/json");
```

[Zipkin official website](https://zipkin.io/)

[.NET client for Zipkin](https://github.com/openzipkin/zipkin4net)

