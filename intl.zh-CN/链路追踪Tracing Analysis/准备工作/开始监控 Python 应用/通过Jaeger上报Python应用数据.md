# 通过Jaeger上报Python应用数据

在使用链路追踪控制台追踪应用的链路数据之前，需要通过客户端将应用数据上报至链路追踪。本文介绍如何通过Jaeger客户端上报Python应用数据。





## 操作步骤

1.  运行以下命令安装jaeger-client。

    ```
    pip install jaeger-client
    ```

2.  创建Tracer对象，并通过Tracer对象创建Span来追踪业务流程。

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

3.  下载原生Jaeger Agent [jaeger-agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent)，并用以下参数启动Agent，以将数据上报至链路追踪Tracing Analysis。

    **说明：** 请将`<endpoint>`替换成链路追踪控制台概览页面上相应客户端和相应地域的接入点。关于获取接入点信息的方法，请参见前提条件中的[获取接入点信息](#tab2)。

    ```
    // reporter.grpc.host-port用于设置网关，网关因地域而异。 例如：
    $ nohup ./jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=<endpoint>
    ```


## Jaeger使用方法

-   创建Trace

    ```
    from jaeger_client import Config
    
    def init_jaeger_tracer(service_name='your-app-name'):
        config = Config(config={}, service_name=service_name)
        return config.initialize_tracer()
    ```

-   创建和结束Span

    ```
    // 开始无Parent的Span。
    tracer.start_span('TestSpan') 
    // 开始有Parent的Span。
    tracer.start_span('ChildSpan', child_of=span)
    // 结束Span。
     span.finish()
    ```

-   透传SpanContext

    ```
    // 将spanContext透传到下一个Span中（序列化）。
    tracer.inject(
            span_context=span.context, format=Format.TEXT_MAP, carrier=carrier
        )
    // 解析透传过来的spanContxt（反序列化）。
    span_ctx = tracer.extract(format=Format.TEXT_MAP, carrier={})
    ```


[OpenTracing指南](https://github.com/yurishkuro/opentracing-tutorial/tree/master/python)

[jaeger-client-python](https://github.com/jaegertracing/jaeger-client-python)

