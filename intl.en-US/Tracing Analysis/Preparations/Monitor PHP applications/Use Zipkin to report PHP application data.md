# Use Zipkin to report PHP application data

Zipkin is an open source Distributed real-time data tracing System \(Distributed Tracking System\) developed and contributed by Twitter. This function aggregates real-time monitoring data from multiple heterogeneous systems. In Tracing Analysis, you can use Zipkin to report PHP application data.



## Code tracking

To report the PHP application data to the tracing analysis console through Zipkin, you must first perform tracking.

1.  Install Zipkin for PHP.

    ```
    
            composer require openzipkin/zipkin 
          
    ```

2.  Create a Tracer. A Tracer object can be used to create a Span \(a record of distributed operations\). The Tracer object also has configured the Gateway address, local IP address, sampling frequency, and other data for the reported data. You can reduce the overhead caused by the reported data by adjusting the sample rate.

    ```
    
            function create_tracing($endpointName, $ipv4) { $endpoint = Endpoint::create($endpointName, $ipv4, null, 2555); /* Do not copy this logger into production. * Read https://github.com/Seldaek/monolog/blob/master/doc/01-usage.md#log-levels */ $logger = new \Monolog\Logger('log'); $logger->pushHandler(new \Monolog\Handler\ErrorLogHandler()); $reporter = new Zipkin\Reporters\Http(\Zipkin\Reporters\Http\CurlFactory::create()); $sampler = BinarySampler::createAsAlwaysSample(); $tracing = TracingBuilder::create() ->havingLocalEndpoint($endpoint) ->havingSampler($sampler) ->havingReporter($reporter) ->build(); return $tracing; } 
          
    ```

3.  Record the request data.

    ```
    
            $rootSpan = $tracer->newTrace(); $rootSpan->setName('encode') $rootSpan->start(); try { doSomethingExpensive(); } finally { $rootSpan->finish(); } 
          
    ```

    **Note:**

    The preceding code is used to record the root operation of the request. If you need to record the previous and next operations of the request, you need to pass in the context. Example:

    ```
    
             $span = $tracer->newChild($parentSpan->getContext()); $span->setName('encode'); $span->start(); try { doSomethingExpensive(); } finally { $span->finish(); } 
           
    ```

4.  You can add custom tags to a record for quick troubleshooting. For example, you can add custom tags to a record to check whether an error occurs or whether the request returns a value.

    ```
    
            $span->tag('http.status_code', $resultCode); 
          
    ```

5.  The sample rate of requests is determined by the root operation. Generally, a sampling policy is created when a Tracer object is created. However, you can replace the sampling policy locally. For example,

    ```
    
            private function newTrace(Request $request) { $flags = SamplingFlags::createAsEmpty(); if (strpos($request->getUri(), '/experimental') === 0) { $flags = DefaultSamplingFlags::createAsSampled(); } else if (strpos($request->getUri(), '/static') === 0) { $flags = DefaultSamplingFlags::createAsSampled(); } return $tracer->newTrace($flags); } 
          
    ```

6.  When an RPC request is sent in a distributed system, Tracing data \(such as TraceId, ParentSpanId, SpanId, and Sampled\) will be attached to the request. When sending an HTTP Request, you can use the Extract/Inject method to pass data through to the HTTP Request Headers. The overall process is as follows:

    ```
    
            Client Span Server Span ┌──────────────────┐ ┌──────────────────┐ │ │ │ │ │ TraceContext │ Http Request Headers │ TraceContext │ │ ┌──────────────┐ │ ┌───────────────────┐ │ ┌──────────────┐ │ │ │ TraceId │ │ │ X-B3-TraceId │ │ │ TraceId │ │ │ │ │ │ │ │ │ │ │ │ │ │ ParentSpanId │ │ Inject │ X-B3-ParentSpanId │Extract │ │ ParentSpanId │ │ │ │ ├─┼─────────>│ ├────────┼>│ │ │ │ │ SpanId │ │ │ X-B3-SpanId │ │ │ SpanId │ │ │ │ │ │ │ │ │ │ │ │ │ │ Sampled │ │ │ X-B3-Sampled │ │ │ Sampled │ │ │ └──────────────┘ │ └───────────────────┘ │ └──────────────┘ │ │ │ │ │ └──────────────────┘ └──────────────────┘ 
          
    ```

    1.  Call the Inject method on the client to pass in Context information.

        ```
        
                  // configure a function that injects a trace context into a request $injector = $tracing->getPropagation()->getInjector(new RequestHeaders); // before a request is sent, add the current span's context to it $injector->inject($span->getContext(), $request); 
                
        ```

    2.  The Extract method parses Context information.

        ```
        
                  // configure a function that extracts the trace context from a request $extracted = $tracing->getPropagation()->extractor(new RequestHeaders); $span = $tracer->newChild($extracted) $span->setKind(Kind\SERVER); 
                
        ```


## Quick Start

The following example uses Zipkin to demonstrate how to use Zipkin to report PHP Data.

1.  Download the [sample file](https://github.com/openzipkin/zipkin-php-example/archive/master.zip).

2.  Modify the Gateway address of the report data in the functions. Php file. Replace `reporter = new reporter` with the following content:

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    
            reporter = new Zipkin\Reporters\Http(\Zipkin\Reporters\Http\CurlFactory::create(), ['endpoint_url' => '<endpoint> ',]); 
          
    ```

3.  Install the dependency.

    ```
    
            // As of zipkin php is still in 1.0.0-betaX rm composer.lock && composer install 
          
    ```

4.  Start the service.

    ```
    
            # Execute composer run-frontend on Terminal 1# execute composer run-backend on Terminal 2 
          
    ```

5.  Visit the report result page and view the reported data in the [tracing analysis console](https://tracing-analysis.console.aliyun.com/).

    ```
    
            curl http://localhost:8081 
          
    ```


## FAQ

Q: Why is no data reported according to the steps in the quick start?

A: Check whether the endpoint\_url is correctly configured.

[Zipkin official website](https://zipkin.io/)

[Zipkin-php for the source code of the OSS Java](https://github.com/openzipkin/zipkin-php)

[zipkin-php-example](https://github.com/openzipkin/zipkin-php-example)

