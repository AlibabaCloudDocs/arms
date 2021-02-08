# Use Zipkin to report PHP application data

Zipkin is a distributed tracing system. It is an open source system that is developed by Twitter to trace real-time data. Zipkin is used to aggregate real-time monitoring data that is collected from multiple heterogeneous systems. In Tracing Analysis, you can use Zipkin to report PHP application data.



## Add instrumentation to the code

To use Zipkin to report PHP application data to the Tracing Analysis console, you must first add instrumentation to the code.

1.  Install Zipkin PHP.

    ```
    composer require openzipkin/zipkin
    ```

2.  Create a Tracer object. The Tracer object can be used to create spans that record the time of distributed operations. The Tracer object contains information such as the endpoint for data reporting, IP address of the on-premises server, and sampling rate. You can adjust the sampling rate to reduce the overheads that are generated in data reporting.

    ```
    function create_tracing($endpointName, $ipv4)
    {
        $endpoint = Endpoint::create($endpointName, $ipv4, null, 2555);
        /* Do not copy this logger into production.
         * Read https://github.com/Seldaek/monolog/blob/master/doc/01-usage.md#log-levels
         */
        $logger = new \Monolog\Logger('log');
        $logger->pushHandler(new \Monolog\Handler\ErrorLogHandler());
        $reporter = new Zipkin\Reporters\Http(\Zipkin\Reporters\Http\CurlFactory::create());
        $sampler = BinarySampler::createAsAlwaysSample();
        $tracing = TracingBuilder::create()
            ->havingLocalEndpoint($endpoint)
            ->havingSampler($sampler)
            ->havingReporter($reporter)
            ->build();
        return $tracing;
    }   
    ```

3.  Record the request data.

    ```
    $rootSpan = $tracer->newTrace();
    $rootSpan->setName('encode')
    $rootSpan->start();
    
    try {
      doSomethingExpensive();
    } finally {
      $rootSpan->finish();
    }
    ```

    **Note:**

    You can run the preceding code to create a root span that records the root operation of a request. If you need to record the previous and next operations of a request, inject a context. Sample code:

    ```
    $span = $tracer->newChild($parentSpan->getContext());
    $span->setName('encode');
    $span->start();
    try {
      doSomethingExpensive();
    } finally {
      $span->finish();
    }
    ```

4.  Add custom tags to a span for quick troubleshooting. For example, you can add a custom tag to check whether an error occurs or to record the return value of a request.

    ```
    $span->tag('http.status_code', $resultCode);
    ```

5.  The root operation determines the sampling rate of requests. In general, a sampling policy is created together with the Tracer object. However, you can apply custom sampling policies to specific operations. Sample code:

    ```
    private function newTrace(Request $request) {
      $flags = SamplingFlags::createAsEmpty();
      if (strpos($request->getUri(), '/experimental') === 0) {
        $flags = DefaultSamplingFlags::createAsSampled();
      } else if (strpos($request->getUri(), '/static') === 0) {
        $flags = DefaultSamplingFlags::createAsSampled();
      }
      return $tracer->newTrace($flags);
    }
    ```

6.  In a distributed system, remote procedure call \(RPC\) requests are sent along with trace data. Trace data contains the values of the TraceId, ParentSpanId, SpanId, and Sampled parameters. You can call the Extract or Inject method to pass data in HTTP request headers. The following figure shows the overall process.

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
        // configure a function that injects a trace context into a request
        $injector = $tracing->getPropagation()->getInjector(new RequestHeaders);
        
        // before a request is sent, add the current span's context to it
        $injector->inject($span->getContext(), $request);
        ```

    2.  Call the Extract method to extract the context information.

        ```
        // configure a function that extracts the trace context from a request
        $extracted = $tracing->getPropagation()->extractor(new RequestHeaders);
        
        $span = $tracer->newChild($extracted)
        $span->setKind(Kind\SERVER);
        ```


## Quick start

The following official Zipkin PHP example shows you how to use Zipkin to report PHP application data.

1.  Download the [Demo](https://github.com/openzipkin/zipkin-php-example/archive/master.zip) file.

2.  Change the endpoint for data reporting in the functions.php file. Replace `$reporter = new Zipkin\Reporters\Http(\Zipkin\Reporters\Http\CurlFactory::create());` with the following code:

    **Note:** Replace `<endpoint>` with the corresponding endpoint in the corresponding region that is displayed on the Overview page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    reporter = new Zipkin\Reporters\Http(\Zipkin\Reporters\Http\CurlFactory::create(), 
    ['endpoint_url' => '<endpoint>
    ',]);
    ```

3.  Install dependencies.

    ```
    // As of zipkin php is still in 1.0.0-betaX
    rm composer.lock && composer install
    ```

4.  Start services.

    ```
    # Run the composer run-frontend command on Terminal 1.
    
    # Run the composer run-backend command on Terminal 2.
    ```

5.  Visit the frontend page to report data. You can view the reported data in the [Tracing Analysis console](https://tracing-analysis.console.aliyun.com/).

    ```
    curl http://localhost:8081
    ```


## FAQ

Q: Why is no data reported after I follow the steps in Quick start?

A: Check whether the endpoint is valid.

[Zipkin official website](https://zipkin.io/)

[Zipkin source code for PHP](https://github.com/openzipkin/zipkin-php)

[zipkin-php-example](https://github.com/openzipkin/zipkin-php-example)

