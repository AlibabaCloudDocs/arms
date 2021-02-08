# Use Jaeger to report Go application data

Before you can view the trace data of your application in the Tracing Analysis console, you must use a client to report the trace data to Tracing Analysis. This topic shows you how to use Jaeger to report Go application data.





## Quick start

1.  Run the following command to download the [Demo](http://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/tracingtest.zip) file to the GOPATH/src directory:

    ```
    wget http://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/tracingtest.zip && unzip tracingtest.zip
    ```

2.  Modify the configuration.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    sender := transport.NewHTTPTransport(
            // Specify the endpoint. The endpoint differs in different regions.
            "<endpoint>",
            )
    ```

3.  Run the following command to upload data:

    ```
    go run main.go
    http done
    grpc done
    ```

    **Note:**

    The following errors indicate an invalid endpoint. Change the endpoint and try again.

    ```
    go run main.go
    http done
    2018/09/17 21:11:54 ERROR: error when flushing the buffer: error from collector: 403
    2018/09/17 21:11:54 ERROR: error when flushing the buffer: error from collector: 403
    ```

4.  Log on to the [Tracing Analysis console](https://tracing-analysis.console.aliyun.com/). After you perform the previous steps, wait 30 seconds. Then, you can view the reported data.


## Directly report data

1.  Import jaeger-client-go.

    -   Package path: github.com/uber/jaeger-client-go
    -   Version: 2.11.0 or later
    For example, if you use Glide, you must add the following code to the glide.yaml file:

    ```
    package: github.com/uber/jaeger-client-go
    version: ^2.11.0
    subpackages:
    transport
    ```

2.  Create a Tracer object.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    func NewJaegerTracer(service string) (opentracing.Tracer, io.Closer) {
    
        sender := transport.NewHTTPTransport(
           // Specify the endpoint. The endpoint differs in different regions.
            "<endpoint>",
        )
       tracer, closer:= jaeger.NewTracer(service,
            jaeger.NewConstSampler(true),
       jaeger.NewRemoteReporter(sender))
       return tracer, closer
    }
    ```

3.  Create a span and pass data.

    -   If no parent span is available, use the following code:

        ```
        // Create a span.
        span := tracer.StartSpan("myspan")
        // Set a tag.
        clientSpan.SetTag("mytag", "123")
        // Pass the ID of the trace.
        tracer.Inject(span.Context(), opentracing.HTTPHeaders, opentracing.HTTPHeadersCarrier(req.Header))
        ...
        defer  span.Finish()
        ```

    -   If a parent span is available, use the following code:

        ```
        // Extract a SpanContext from an HTTP request or a remote procedure call (RPC) request.
        spanCtx, _ := tracer.Extract(opentracing.HTTPHeaders, opentracing.HTTPHeadersCarrier(r.Header))
        span := tracer.StartSpan("myspan", opentracing.ChildOf(spanCtx))
        ...
        defer  span.Finish()
        ```


## Use an agent to report data

1.  Import jaeger-client-go.

    -   Package path: github.com/uber/jaeger-client-go
    -   Version: 2.11.0 or later
    For example, if you use Glide, you must add the following code to the glide.yaml file:

    ```
    package: github.com/uber/jaeger-client-go
    version: ^2.11.0
    subpackages:
    transport
    ```

2.  Create a Tracer object.

    ```
    func NewJaegerTracer(serviceName string) (opentracing.Tracer, io.Closer) {
       sender, _ := jaeger.NewUDPTransport("",0)
       tracer, closer:= jaeger.NewTracer(serviceName,
            jaeger.NewConstSampler(true),
            jaeger.NewRemoteReporter(sender))
        return tracer, closer
    }
    ```

3.  Download the native Jaeger agent [jaeger-agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent) and set the reporter.grpc.host-port parameter to start the agent. This way, data can be reported to Tracing Analysis.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    // Reporter. grpc. host-port is used to set the gateway. The Gateway varies according to the region. Example:
    $ nohup. /jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=<endpoint>
    ```


