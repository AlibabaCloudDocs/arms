# 通过Jaeger上报Go应用数据

在使用链路追踪控制台追踪应用的链路数据之前，需要通过客户端将应用数据上报至链路追踪。本文介绍如何通过Jaeger客户端上报Go应用数据。





## 快速开始

1.  运行以下命令，在GOPATH/src目录下载[Demo文件](http://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/tracingtest.zip)。

    ```
    wget http://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/tracingtest.zip && unzip tracingtest.zip
    ```

2.  修改配置。

    **说明：** 请将`<endpoint>`替换成链路追踪控制台概览页面上相应客户端和相应地域的接入点。关于获取接入点信息的方法，请参见前提条件中的[获取接入点信息](#tab2)。

    ```
    sender := transport.NewHTTPTransport(
            // 设置网关，网关因地域而异。
            "<endpoint>",
            )
    ```

3.  运行以下命令上传数据。

    ```
    go run main.go
    http done
    grpc done
    ```

    **说明：**

    如果出现以下错误，说明用户名和密码不正确，请更正并重试。

    ```
    go run main.go
    http done
    2018/09/17 21:11:54 ERROR: error when flushing the buffer: error from collector: 403
    2018/09/17 21:11:54 ERROR: error when flushing the buffer: error from collector: 403
    ```

4.  登录[链路追踪控制台](https://tracing-analysis.console.aliyun.com/)。执行上一步骤后等待30秒，即可查看上报的数据。


## 直接上报数据

1.  引入jaeger-client-go。

    -   包路径：github.com/uber/jaeger-client-go
    -   版本号：\>=2.11.0
    以glide为例，您需要在glide.yaml中加入以下配置：

    ```
    package: github.com/uber/jaeger-client-go
    version: ^2.11.0
    subpackages:
    transport
    ```

2.  创建Trace对象。

    **说明：** 请将`<endpoint>`替换成链路追踪控制台概览页面上相应客户端和相应地域的接入点。关于获取接入点信息的方法，请参见前提条件中的[获取接入点信息](#tab2)。

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

    -   如果没有parentSpan

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

    -   如果有parentSpan

        ```
        // 从HTTP/RPC对象解析出spanCtx。
        spanCtx, _ := tracer.Extract(opentracing.HTTPHeaders, opentracing.HTTPHeadersCarrier(r.Header))
        span := tracer.StartSpan("myspan", opentracing.ChildOf(spanCtx))
        ...
        defer  span.Finish()
        ```


## 通过Agent上报数据

1.  引入jaeger-client-go。

    -   包路径：github.com/uber/jaeger-client-go
    -   版本号：\>=2.11.0
    以glide为例，您需要在glide.yaml中加入以下配置：

    ```
    package: github.com/uber/jaeger-client-go
    version: ^2.11.0
    subpackages:
    transport
    ```

2.  创建Trace对象。

    ```
    func NewJaegerTracer(serviceName string) (opentracing.Tracer, io.Closer) {
       sender, _ := jaeger.NewUDPTransport("",0)
       tracer, closer:= jaeger.NewTracer(serviceName,
            jaeger.NewConstSampler(true),
            jaeger.NewRemoteReporter(sender))
        return tracer, closer
    }
    ```

3.  下载原生Jaeger Agent [jaeger-agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent)，并用以下参数启动Agent，以将数据上报至链路追踪Tracing Analysis。

    **说明：** 请将`<endpoint>`替换成链路追踪控制台概览页面上相应客户端和相应地域的接入点。关于获取接入点信息的方法，请参见前提条件中的[获取接入点信息](#tab2)。

    ```
    // reporter.grpc.host-port用于设置网关，网关因地域而异。 例如：
    $ nohup ./jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=<endpoint>
    ```


## 更多信息

