# Logs of. NET applications are reported through Zipkin.

Zipkin is an open source Distributed real-time data tracing System \(Distributed Tracking System\) developed and contributed by Twitter. This function aggregates real-time monitoring data from multiple heterogeneous systems. In Tracing Analysis, you can use Zipkin to report data to. NET applications. This method also applies to applications that are developed with C\#.



## Automatic tracking through ASP.NET Core components

Follow these steps to ASP.NET Core component burial points.

**Note:** Download the [Demo source](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinDotnetNetcore.zip) code and follow Readme to run the program.

1.  Install the NuGet Package.

    ```
    
            // Add the following components. // zipkin4 net.middleware.aspnetcore(aspnetcore middleware) // zipkin4net dotnet add package zipkin4net.middleware.aspnetcore dotnet add package zipkin4nete 
          
    ```

2.  Register and start Zipkin.

    ```
    
            lifetime.ApplicationStarted.Register () => { TraceManager.SamplingRate = 1.0f; var logger = new TracingLogger(loggerFactory, "zipkin4net"); // Obtain the Zipkin Endpoint in the tracing analysis console. Make sure that the Endpoint does not contain "/api/v2/spans". var httpSender = new HttpZipkinSender("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_your_token", "application/json"); var tracer = new ZipkinTracer(httpSender, new JSONSpanSerializer()); TraceManager.RegisterTracer(tracer); TraceManager.Start(logger); }); lifetime.ApplicationStopped.Register(() => TraceManager.Stop()); app.UseTracing(applicationName); 
          
    ```

3.  Add tracinghandler \(tracing handler\) to the HttpClient that sends a Get or Post request.

    ```
    
            public override void ConfigureServices(IServiceCollection services) { services.AddHttpClient("Tracer").AddHttpMessageHandler(provider => TracingHandler.WithoutInnerHandler(provider.GetService<IConfiguration>()["applicationName"])); } 
          
    ```


## Automatic tracking through the Owen component

Follow these steps to track data through the Owen component.

**Note:** Download the [Demo source](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinDotnetOwin.zip) code and follow Readme to run the program.

1.  Install the NuGet Package.

    ```
    
            // Add the following components. // zipkin4 net.middleware.aspnetcore(aspnetcore middleware) // zipkin4net dotnet add package zipkin4net.middleware.aspnetcore dotnet add package zipkin4nete 
          
    ```

2.  Register and start Zipkin.

    ```
    
            // Set up Tracing. TraceManager.SamplingRate = 1.0f; var logger = new ConsoleLogger(); // Obtain the Zipkin Endpoint from the tracing analysis console. Note that the Endpoint does not contain "/api/v2/spans". var httpSender = new HttpZipkinSender("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_your_token", "application/json"); var tracer = new ZipkinTracer(httpSender, new JSONSpanSerializer()); TraceManager.RegisterTracer(tracer); TraceManager.Start(logger); //Stop TraceManager on app dispose var properties = new AppProperties(appBuilder.Properties); var token = properties.OnAppDisposing; if (token ! = CancellationToken.None) { token.Register(() => { TraceManager.Stop(); }); } // // Setup Owin Middleware appBuilder.UseZipkinTracer(System.Configuration.ConfigurationManager.AppSettings["applicationName"]); // 
          
    ```

3.  Add tracinghandler \(tracing handler\) to the HttpClient that sends a Get or Post request.

    ```
    
            using (var httpClient = new HttpClient(new TracingHandler(applicationName))) { var response = await httpClient.GetAsync(callServiceUrl); var content = await response.Content.ReadAsStringAsync(); await context.Response.WriteAsync(content); } 
          
    ```


## Manual burial point

To report Java application data to the link tracking console through Zipkin, in addition to using various existing plug-ins to implement tracking, you can also manually track points.

**Note:** Download the [Demo source](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinDotnetManual.zip) code and follow Readme to run the program.

1.  Install the NuGet Package.

    ```
    
            // Add zipkin4net (tracker). dotnet add package zipkin4nete 
          
    ```

2.  Register and start Zipkin.

    ```
    
            TraceManager.SamplingRate = 1.0f; var logger = new ConsoleLogger(); // Obtain the Zipkin Endpoint from the tracing analysis console. Note that the Endpoint does not contain "/api/v2/spans". var httpSender = new HttpZipkinSender("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_your_token", "application/json"); var tracer = new ZipkinTracer(httpSender, new JSONSpanSerializer()); TraceManager.RegisterTracer(tracer); TraceManager.Start(logger); 
          
    ```

3.  Record the request data.

    ```
    
            var trace = Trace.Create(); Trace.Current = trace; trace.Record(Annotations.ClientSend()); trace.Record(Annotations.Rpc("client")); trace.Record(Annotations.Tag("mytag", "spanFrist")); trace.Record(Annotations.ServiceName("dotnetManual")); // ...do something testCall(); trace.Record(Annotations.ClientRecv()); 
          
    ```

    **Note:**

    The preceding code is used to record the root operation of the request. To record the previous and next operations of the request, you must call the ChildOf method. Example:

    ```
    
             var trace = Trace.Current.Child(); Trace.Current = trace; trace.Record(Annotations.ServerRecv()); trace.Record(Annotations.Rpc("server")); trace.Record(Annotations.Tag("mytag", "spanSecond")); trace.Record(Annotations.ServiceName("dotnetManual")); // ...do something trace.Record(Annotations.ServerSend()); 
           
    ```

4.  You can add custom tags to a record for quick troubleshooting. For example, you can add custom tags to a record to check whether an error occurs or whether the request returns a value.

    ```
    
            tracer.activeSpan().setTag("http.status_code", "200"); 
          
    ```

5.  When an RPC request is sent in a distributed system, Tracing data \(such as TraceId, ParentSpanId, SpanId, and Sampled\) will be attached to the request. When sending an HTTP Request, you can use the Extract/Inject method to pass data through to the HTTP Request Headers. The overall process is as follows:

    ```
    
            Client Span Server Span ┌──────────────────┐ ┌──────────────────┐ │ │ │ │ │ TraceContext │ Http Request Headers │ TraceContext │ │ ┌──────────────┐ │ ┌───────────────────┐ │ ┌──────────────┐ │ │ │ TraceId │ │ │ X-B3-TraceId │ │ │ TraceId │ │ │ │ │ │ │ │ │ │ │ │ │ │ ParentSpanId │ │ Inject │ X-B3-ParentSpanId │Extract │ │ ParentSpanId │ │ │ │ ├─┼─────────>│ ├────────┼>│ │ │ │ │ SpanId │ │ │ X-B3-SpanId │ │ │ SpanId │ │ │ │ │ │ │ │ │ │ │ │ │ │ Sampled │ │ │ X-B3-Sampled │ │ │ Sampled │ │ │ └──────────────┘ │ └───────────────────┘ │ └──────────────┘ │ │ │ │ │ └──────────────────┘ └──────────────────┘ 
          
    ```

    1.  Call the Inject method on the client to pass in Context information.

        ```
        
                  _injector.Inject(clientTrace.Trace.CurrentSpan, request.Headers); 
                
        ```

    2.  Call the Extract method on the server to parse Context Information.

        ```
        
                  Ivar traceContext = traceExtractor.Extract(context.Request.Headers); var trace = traceContext == null ? Trace.Create() : Trace.CreateFromId(traceContext); 
                
        ```


## FAQ

Q: Why does the Demo program fail to be executed but no data is reported from the console?

Check whether you have configured the correct Endpoint for the senderConfiguration.

```

     // Obtain the Zipkin Endpoint from the tracing analysis console. Note that the Endpoint does not contain "/api/v2/spans". var httpSender = new HttpZipkinSender("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_your_token", "application/json"); 
   
```

[Zipkin official website](https://zipkin.io/)

[Zipkin's dotnet client](https://github.com/openzipkin/zipkin4net)

