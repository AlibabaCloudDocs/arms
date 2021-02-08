# Use Jaeger to report C++ application data

Before you can view the trace data of your application in the Tracing Analysis console, you must use a client to report the trace data to Tracing Analysis. This topic shows you how to use Jaeger to report the data of C++ applications.





## Directly report data

1.  Run the following command to obtain [jaeger-client-cpp](https://github.com/jaegertracing/jaeger-client-cpp) from the official website:

    ```
    wget https://github.com/jaegertracing/jaeger-client-cpp/archive/master.zip && unzip master.zip
    ```

2.  Run the following commands to compile jaeger-client-cpp:

    **Note:** The compilation depends on CMake. The GCC version must be 4.9.2 or later.

    ```
    mkdir build
        cd build
        cmake ..
        make
    ```

3.  Download the native Jaeger agent [jaeger-agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent). Then, set the following parameter to start the agent. This way, you can report data to Tracing Analysis.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    // Reporter. grpc. host-port is used to set the gateway. The Gateway varies according to the region. Example:
    $ nohup. /jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=<endpoint>
    ```

4.  Go to the examples directory of jaeger-client-cpp and run the test case.

    ```
    ./app ../examples/config.yml
    ```

5.  Log on to the [Tracing Analysis](https://tracing-analysis.console.aliyun.com/) console and view the reported data.


## Use the Jaeger agent to report data

1.  Install a Jaeger client. For more information about how to download a Jaeger client, visit [jaeger-client-cpp](https://github.com/jaegertracing/jaeger-client-cpp).

2.  Create a Tracer object.

    For example, you can create a Tracer object based on the YAML configuration.

    ```
    void setUpTracer(const char* configFilePath)
    {
        auto configYAML = YAML::LoadFile(configFilePath);
        // Import the configuration from the YAML file.
        auto config = jaegertracing::Config::parse(configYAML);
        // Set the service name and logger of the Tracer object.
        auto tracer = jaegertracing::Tracer::make(
            "example-service", config, jaegertracing::logging::consoleLogger());
        // Set the Tracer object as a global variable.
        opentracing::Tracer::InitGlobal(
            std::static_pointer_cast<opentracing::Tracer>(tracer));
    }
    ```

    Example of the YAML configuration:

    ```
    disabled: false
    reporter:
        logSpans: true
    sampler:
      type: const
      param: 1
    ```

3.  Create a span.

    ```
    // Create a span when a parent span exists.
    void tracedSubroutine(const std::unique_ptr<opentracing::Span>& parentSpan)
    {
        auto span = opentracing::Tracer::Global()->StartSpan(
            "tracedSubroutine", { opentracing::ChildOf(&parentSpan->context()) });
    }
    
    // Create a span when no parent span exists.
    void tracedFunction()
    {
        auto span = opentracing::Tracer::Global()->StartSpan("tracedFunction");
        tracedSubroutine(span);
    }
    ```

4.  Download the native Jaeger agent [jaeger-agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent). Then, set the following parameter to start the agent. This way, you can report data to Tracing Analysis.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    // Reporter. grpc. host-port is used to set the gateway. The Gateway varies according to the region. Example:
    $ nohup. /jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=<endpoint>
    ```


