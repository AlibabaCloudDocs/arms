# Report Go application data through Zipkin

Zipkin is an open-source Distributed real-time data Tracking System developed and contributed by Twitter. It aggregates real-time monitoring data from various heterogeneous systems. In Link tracking Tracing Analysis, you can use Zipkin to report Go application data.





## Code burial point

Tracking is required to report Go application data to the link tracking console through Zipkin.

1.  Add component dependencies.

    ```
    [[constraint]]
      name = &quot;github.com/openzipkin/zipkin-go&quot;
      version = &quot;0.1.1&quot;
    
    [[constraint]]
      name = &quot;github.com/gorilla/mux&quot;
      version = &quot;1.6.2&quot;
    ```

2.  Create a Tracer. A Tracer object can be used to create a Span object \(recording distributed operation time\). The Tracer object is also configured with data such as the gateway address, local IP address, and sampling frequency. You can adjust the sampling rate to reduce the overhead caused by data reporting.

    ```
    func getTracer(serviceName string, ip string) *zipkin.Tracer {
      // create a reporter to be used by the tracer
      reporter := httpreporter.NewReporter(&quot;http://tracing-analysis-dc-hz.aliyuncs.com/adapt_aokcdqnxyz@123456ff_abcdef123@abcdef123/api/v2/spans&quot;)
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

3.  Record request data.

    ```
    // tracer can now be used to create spans.
    span := tracer.StartSpan(&quot;some_operation&quot;)
    /// ..... do some work...
    span.Finish()
    // Output:
    ```

    **Note:**

    The preceding code is used to record the root operation of the request. To record the previous and next operations of the request, enter the context. Example:

    ```
    childSpan := tracer.StartSpan(&quot;some_operation2&quot;, zipkin.Parent(span.Context()))
        /// ..... do some work...
    childSpan.Finish()
    ```

4.  To quickly troubleshoot problems, you can add custom tags to a record, such as records for errors and returned values of requests.

    ```
    childSpan.Tag(&quot;http.status_code&quot;, statusCode)
    ```

5.  When a distributed system sends an RPC request, it carries Tracing data, including TraceId, ParentSpanId, SpanId, and Sampled. You can use the Extract/Inject method in an HTTP Request to transparently transmit data to HTTP Request Headers. The overall process is as follows:

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

    **Note:** Currently, Zipkin components support passthrough Context information using HTTP and gRPC RPC protocols.

    1.  Call the Inject method on the client to pass in Context information.

        ```
        req, _ := http.NewRequest(&quot;GET&quot;, &quot;/&quot;, nil)
        // configure a function that injects a trace context into a reques
        injector := b3.InjectHTTP(req)
        injector(sp.Context())
        ```

    2.  Call the Extract method on the server to parse the Context information.

        ```
        req, _ := http.NewRequest(&quot;GET&quot;, &quot;/&quot;, nil)
                b3.InjectHTTP(req)(sp.Context())
        
                B .ResetTimer()
                _ = b3.ExtractHTTP(copyRequest(req))
        ```


## Quick start

The following example shows how to report application data through Zipkin.

1.  Download[Sample file](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingGoTest.zip).

2.  Modify the Gateway address \(endpointURL\) of the reported data in the utils. go file.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

3.  Install the dependency package.

    ```
    dep ensure
    ```

4.  Run the test program.

    ```
    go run main.go
    ```

5.  In[Link tracing console](https://tracing-analysis.console.aliyun.com/)View the reported data.


## FAQ

Q: Why does the quick start procedure fail to report data?

A: check whether any prompt is displayed during the running process.Endpoint\_urlIs configured correctly. For example, an error`failed the request with status code 403`The username or password is incorrect.

[Zipkin official website](https://zipkin.io/)

[Zipkin-go source code](https://github.com/openzipkin/zipkin-go)

