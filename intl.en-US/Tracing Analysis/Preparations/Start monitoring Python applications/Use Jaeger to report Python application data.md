# Use Jaeger to report Python application data

Before using the tracing analysis console to trace tracing data, you need to report the data to the tracing analysis console from the client. This topic describes how to use the Jaeger client to report Python application data.





## Procedure

1.  Run the following command to install the jaeger client.

    ```
    
            pip install jaeger-client 
          
    ```

2.  Create a Tracer object, and create a Span based on the Tracer object to trace workflow.

    ```
    
            import logging import time from jaeger_client import Config if __name__ == "__main__": log_level = logging.DEBUG logging.getLogger('').handlers = [] logging.basicConfig(format='%(asctime)s %(message)s', level=log_level) config = Config( config={ # usually read from some yaml config 'sampler': { 'type': 'const', 'param': 1, }, 'logging': True, }, service_name='your-app-name', ) # this call also sets opentracing.tracer tracer = config.initialize_tracer() with tracer.start_span('TestSpan') as span: span.log_kv({'event': 'test message', 'life': 42}) with tracer.start_span('ChildSpan', child_of=span) as child_span: span.log_kv({'event': 'down below'}) time.sleep(2) # yield to IOLoop to flush the spans - https://github.com/jaegertracing/jaeger-client-python/issues/50 tracer.close() # flush any buffered spans 
          
    ```

3.  Download the native Jaeger Agent [jaeger-agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent), and start the Agent with the following parameters to report data to Tracing Analysis.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    // Reporter. grpc. host-port is used to set the gateway. The Gateway varies according to the region. Example:
    $ nohup. /jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=<endpoint>
    ```


## Jaeger usage

-   Create a Trace

    ```
    
           from jaeger_client import Config def init_jaeger_tracer(service_name='your-app-name'): config = Config(config={}, service_name=service_name) return config.initialize_tracer() 
         
    ```

-   Create and end Span

    ```
    
           // Start Span without Parent. tracer.start_span('TestSpan') // indicates that the Span of the Parent object exists. tracer.start_span('ChildSpan', child_of=span) // end Span. span.finish() 
         
    ```

-   Passthrough The SpanContext.

    ```
    
           // Passthrough The spanContext to the next Span (serialization). tracer.inject( span_context=span.context, format=Format.TEXT_MAP, carrier=carrier ) // Parse the passthrough spanContxt (deserialization). span_ctx = tracer.extract(format=Format.TEXT_MAP, carrier={}) 
         
    ```


[OpenTracing guide](https://github.com/yurishkuro/opentracing-tutorial/tree/master/python)

[jaeger-client-python](https://github.com/jaegertracing/jaeger-client-python)

