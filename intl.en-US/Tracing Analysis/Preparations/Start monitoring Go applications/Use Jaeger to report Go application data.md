# Use Jaeger to report Go application data

Before using the tracing analysis console to trace tracing data, you need to report the data to the tracing analysis console from the client. This topic describes how to use the Jaeger client to report data to a Go application.





## Quick start

1.  Run the following command to download the GOPATH/src in the [Demo file](http://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/tracingtest.zip) Directory:

    ```
    
            wget http://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/tracingtest.zip && unzip tracingtest.zip 
          
    ```

2.  Modify the configuration.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    
            sender := transport.NewHTTPTransport( // specify the gateway. The Gateway varies with regions. "<endpoint>", ) 
          
    ```

3.  Run the following command to upload data:

    ```
    
            go run main.go http done grpc done 
          
    ```

    **Note:**

    If the following error occurs, the user name and password are incorrect, please correct it and try again.

    ```
    
             go run main.go http done 2018/09/17 21:11:54 ERROR: error when flushing the buffer: error from collector: 403 2018/09/17 21:11:54 ERROR: error when flushing the buffer: error from collector: 403 
           
    ```

4.  Log on to the [tracing analysis console](https://tracing-analysis.console.aliyun.com/). After you run the previous step, wait 30 seconds to view the reported data.


## Data Reporting

1.  Introduce jaeger-client-go.

    -   Package path: github.com/uber/jaeger-client-go
    -   Version number: EMR=2.11.0
    For example, you need to add the following configuration to the glide.yaml file.

    ```
    
            package: github.com/uber/jaeger-client-go version: ^2.11.0 subpackages: transport 
          
    ```

2.  Create a Trace object.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    
            func NewJaegerTracer(service string) (opentracing.Tracer, io.Closer) { sender := transport.NewHTTPTransport( // Set the gateway. The Gateway varies depending on regions. "<endpoint>", ) tracer, closer:= jaeger.NewTracer(service, jaeger.NewConstSampler(true), jaeger.NewRemoteReporter(sender)) return tracer, closer } 
          
    ```

3.  Create a span instance object and configure data passthrough.

    -   If there is no parentSpan

        ```
        
                 // Create a Span. span := tracer.StartSpan("myspan") // Set the Tag. clientSpan.SetTag("mytag", "123") // pass the traceId through. tracer.Inject(span.Context(), opentracing.HTTPHeaders, opentracing.HTTPHeadersCarrier(req.Header)) ... defer span.Finish() 
               
        ```

    -   If there is parentSpan

        ```
        
                 // Resolve the spantx from the HTTP/RPC object. spanCtx, _ := tracer.Extract(opentracing.HTTPHeaders, opentracing.HTTPHeadersCarrier(r.Header)) span := tracer.StartSpan("myspan", opentracing.ChildOf(spanCtx)) ... defer span.Finish() 
               
        ```


## Report data through Agent

1.  Introduce jaeger-client-go.

    -   Package path: github.com/uber/jaeger-client-go
    -   Version number: EMR=2.11.0
    For example, you need to add the following configuration to the glide.yaml file.

    ```
    
            package: github.com/uber/jaeger-client-go version: ^2.11.0 subpackages: transport 
          
    ```

2.  Create a Trace object.

    ```
    
            func NewJaegerTracer(serviceName string) (opentracing.Tracer, io.Closer) { sender, _ := jaeger.NewUDPTransport("",0) tracer, closer:= jaeger.NewTracer(serviceName, jaeger.NewConstSampler(true), jaeger.NewRemoteReporter(sender)) return tracer, closer } 
          
    ```

3.  Download the native Jaeger Agent [jaeger-agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent), and start the Agent with the following parameters to report data to Tracing Analysis.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    // Reporter. grpc. host-port is used to set the gateway. The Gateway varies according to the region. Example:
    $ nohup. /jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=<endpoint>
    ```


