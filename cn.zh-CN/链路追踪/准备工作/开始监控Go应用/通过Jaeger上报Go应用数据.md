# 通过Jaeger上报Go应用数据

在追踪应用的链路数据之前，您需要通过客户端将应用数据上报至链路追踪服务端。本文介绍如何通过Jaeger客户端上报Go应用数据，包括使用Jaeger SDK上报和使用Jaeger Agent上报两种方式，并在文末提供示例。

## 方式一：通过Jaeger SDK上报数据

此处以依赖管理工具Go Modules为例，您可以通过Jaeger SDK埋点直接将数据上报到链路追踪服务端。若使用其他依赖管理工具，请按实际情况操作。

1.  引入[jaeger-client-go](https://github.com/jaegertracing/jaeger-client-go)。

    ```
    go get github.com/uber/jaeger-client-go
    ```

2.  创建Tracer对象。

    **说明：** 请将`<endpoint>`替换成链路追踪控制台概览页面上相应客户端和相应地域的接入点。关于获取接入点信息的方法，请参见本文前提条件。

    ```
    func NewJaegerTracer(service string) (opentracing.Tracer, io.Closer) {
    
        sender := transport.NewHTTPTransport(
           // 设置网关，网关因地域而异。
            "<endpoint>",
        )
       tracer, closer:= jaeger.NewTracer(service,
               jaeger.NewConstSampler(true),
               jaeger.NewRemoteReporter(sender))
       return tracer, closer
    }
    ```

3.  创建span实例对象和数据透传。

    -   如果没有parentSpan：

        ```
        // 创建Span。
        span := tracer.StartSpan("myspan")
        // 设置Tag。
        clientSpan.SetTag("mytag", "123")
        // 透传traceId。
        tracer.Inject(span.Context(), opentracing.HTTPHeaders, opentracing.HTTPHeadersCarrier(req.Header))
        ...
        defer  span.Finish()
        ```

    -   如果有parentSpan：

        ```
        // 从HTTP/RPC对象解析出spanCtx。
        spanCtx, _ := tracer.Extract(opentracing.HTTPHeaders, opentracing.HTTPHeadersCarrier(r.Header))
        span := tracer.StartSpan("myspan", opentracing.ChildOf(spanCtx))
        ...
        defer  span.Finish()
        ```

    更多详细使用方法，请参见[Go Doc](https://pkg.go.dev/github.com/jaegertracing/jaeger-client-go)。


## 方式二：通过Jaeger Agent上报数据

1.  启动Jaeger Agent。具体操作，请参见[安装Jaeger Agent](/cn.zh-CN/准备工作/安装Jaeger Agent.md)。

2.  引入[jaeger-client-go](https://github.com/jaegertracing/jaeger-client-go)。

    ```
    go get github.com/uber/jaeger-client-go
    ```

3.  创建Tracer对象。

    ```
    func NewJaegerTracer(serviceName string) (opentracing.Tracer, io.Closer) {
       sender, _ := jaeger.NewUDPTransport("",0)
       tracer, closer:= jaeger.NewTracer(serviceName,
            jaeger.NewConstSampler(true),
            jaeger.NewRemoteReporter(sender))
        return tracer, closer
    }
    ```

4.  创建span实例对象和数据透传。

    -   如果没有parentSpan：

        ```
        // 创建Span。
        span := tracer.StartSpan("myspan")
        // 设置Tag。
        clientSpan.SetTag("mytag", "123")
        // 透传traceId。
        tracer.Inject(span.Context(), opentracing.HTTPHeaders, opentracing.HTTPHeadersCarrier(req.Header))
        ...
        defer  span.Finish()
        ```

    -   如果有parentSpan：

        ```
        // 从HTTP/RPC对象解析出spanCtx。
        spanCtx, _ := tracer.Extract(opentracing.HTTPHeaders, opentracing.HTTPHeadersCarrier(r.Header))
        span := tracer.StartSpan("myspan", opentracing.ChildOf(spanCtx))
        ...
        defer  span.Finish()
        ```

    更多详细使用方法，请参见[Go Doc](https://pkg.go.dev/github.com/jaegertracing/jaeger-client-go)。


## 使用示例

**通过Jaeger SDK直接上报**

1.  获取接入点信息。具体操作方法，请参见本文前提条件。

2.  运行以下命令，下载[示例文件](https://arms-apm-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/demo/tracing-demo.zip)。

    ```
    wget https://arms-apm-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/demo/tracing-demo.zip && unzip tracing-demo.zip
    ```

3.  打开示例文件夹中的examples/settings.go文件，配置TracingAnalysisEndpoint，将图示①替换为[步骤1](#step_gjw_c8o_zwk)中获取的接入点信息。

    ![jaeger_demo](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4324884261/p289809.png)

4.  使用`go mod tidy`命令整理依赖。

5.  使用`go run tracingdemo`命令运行示例。


**通过Jaeger Agent上报**

1.  获取接入点信息。具体操作方法，请参见本文前提条件。

2.  运行以下命令，下载[示例文件](https://arms-apm-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/demo/tracing-demo.zip)。

    ```
    wget https://arms-apm-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/demo/tracing-demo.zip && unzip tracing-demo.zip
    ```

3.  启动Jaeger Agent。具体操作，请参见[安装Jaeger Agent](/cn.zh-CN/准备工作/安装Jaeger Agent.md)。

4.  打开示例文件夹中的examples/settings.go文件，将`AgentSwitch`修改为`true`。

    ![jaeger_demo](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0071884261/p289900.png)

5.  使用`go mod tidy`命令整理依赖。

6.  使用`go run tracingdemo`命令运行示例。


## 常见问题

Q：在运行过程中，为什么会出现以下报错？

```
2021/06/28 21:11:54 ERROR: error when flushing the buffer: error from collector: 403
2021/06/28 21:11:54 ERROR: error when flushing the buffer: error from collector: 403
```

A：出现上述报错，说明输入的接入点信息不正确。请更正并重试。

## 更多信息

