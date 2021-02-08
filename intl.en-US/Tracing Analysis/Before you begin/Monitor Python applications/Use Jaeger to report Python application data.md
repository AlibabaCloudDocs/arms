# Use Jaeger to report Python application data

Before you can view the trace data of your application in the Tracing Analysis console, you must use a client to report the trace data to Tracing Analysis. This topic shows you how to use Jaeger to report Python application data.





## Procedure

1.  Run the following command to install Jaeger:

    ```
    pip install jaeger-client
    ```

2.  Create a Tracer object. Then, use the Tracer object to create spans to trace workflows.

    ```
    import logging
    import time
    from jaeger_client import Config
    
    if __name__ == "__main__":
        log_level = logging.DEBUG
        logging.getLogger('').handlers = []
        logging.basicConfig(format='%(asctime)s %(message)s', level=log_level)
    
        config = Config(
            config={ # usually read from some yaml config
                'sampler': {
                    'type': 'const',
                    'param': 1,
                },
                'logging': True,
            },  
            service_name='your-app-name',
        )
        # this call also sets opentracing.tracer
        tracer = config.initialize_tracer()
    
        with tracer.start_span('TestSpan') as span:
            span.log_kv({'event': 'test message', 'life': 42})
    
            with tracer.start_span('ChildSpan', child_of=span) as child_span:
                span.log_kv({'event': 'down below'})
    
        time.sleep(2)   # yield to IOLoop to flush the spans - https://github.com/jaegertracing/jaeger-client-python/issues/50
        tracer.close()  # flush any buffered spans
    ```

3.  Download the native Jaeger agent [jaeger-agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent) and set the reporter.grpc.host-port parameter to start the agent. This way, data can be reported to Tracing Analysis.

    **Note:** Replace `<endpoint>` with the corresponding endpoint in the corresponding region that is displayed on the Overview page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    // Reporter. grpc. host-port is used to set the gateway. The Gateway varies according to the region. Example:
    $ nohup. /jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=<endpoint>
    ```


## Use of Jaeger

-   Create a Tracer object

    ```
    from jaeger_client import Config
    
    def init_jaeger_tracer(service_name='your-app-name'):
        config = Config(config={}, service_name=service_name)
        return config.initialize_tracer()
    ```

-   Create and finish a span

    ```
    // Start a span that does not have a parent span.
    tracer.start_span('TestSpan') 
    // Start a span that has a parent span.
    tracer.start_span('ChildSpan', child_of=span)
    // Finish the span.
     span.finish()
    ```

-   Pass a SpanContext

    ```
    // Serialization: Inject a SpanContext and pass it to the next span.
    tracer.inject(
            span_context=span.context, format=Format.TEXT_MAP, carrier=carrier
        )
    // Deserialization: Extract a SpanContext that is passed.
    span_ctx = tracer.extract(format=Format.TEXT_MAP, carrier={})
    ```


[OpenTracing Tutorial](https://github.com/yurishkuro/opentracing-tutorial/tree/master/python)

[jaeger-client-python](https://github.com/jaegertracing/jaeger-client-python)

