# 通过Jaeger上报C++ 应用数据

在使用链路追踪控制台追踪应用的链路数据之前，需要通过客户端将应用数据上报至链路追踪。本文介绍如何通过Jaeger客户端上报C++ 应用数据。

## 直接上报数据

1.  运行以下命令，从官方网站获取[jaeger-client-cpp](https://github.com/jaegertracing/jaeger-client-cpp)。

    ```
    wget https://github.com/jaegertracing/jaeger-client-cpp/archive/master.zip && unzip master.zip
    ```

2.  运行以下命令，编译jaeger-client-cpp。

    **说明：** 编译依赖CMake，gcc版本不低于4.9.2。

    ```
    mkdir build
        cd build
        cmake ..
        make
    ```

3.  下载原生Jaeger Agent [jaeger-agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent)，并用以下参数启动Agent，以将数据上报至链路追踪Tracing Analysis。

    **说明：** 请将`<endpoint>`替换成链路追踪控制台概览页面上相应客户端和相应地域的接入点。关于获取接入点信息的方法，请参见前提条件中的[获取接入点信息](#tab2)。

    ```
    // reporter.grpc.host-port用于设置网关，网关因地域而异。 例如：
    $ nohup ./jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=<endpoint>
    ```

4.  进入jaeger-client-cpp的example目录，运行测试用例。

    ```
    ./app ../examples/config.yml
    ```

5.  登录[链路追踪控制台](https://tracing-analysis.console.aliyun.com/)，查看上报的数据。


## 通过Agent上报数据

1.  安装Jaeger Client（[官方下载地址](https://github.com/jaegertracing/jaeger-client-cpp)）。

2.  创建Trace。

    例如，我们可以根据YAML配置生成Trace对象。

    ```
    void setUpTracer(const char* configFilePath)
    {
        auto configYAML = YAML::LoadFile(configFilePath);
        // 从YAML文件中导入配置。
        auto config = jaegertracing::Config::parse(configYAML);
        // 设置Trace的serviceName和日志。
        auto tracer = jaegertracing::Tracer::make(
            "example-service", config, jaegertracing::logging::consoleLogger());
        //将Tracer设置为全局变量。
        opentracing::Tracer::InitGlobal(
            std::static_pointer_cast<opentracing::Tracer>(tracer));
    }
    ```

    YAML配置参考：

    ```
    disabled: false
    reporter:
        logSpans: true
    sampler:
      type: const
      param: 1
    ```

3.  创建Span。

    ```
    // 有parentSpan的情况下创建Span。
    void tracedSubroutine(const std::unique_ptr<opentracing::Span>& parentSpan)
    {
        auto span = opentracing::Tracer::Global()->StartSpan(
            "tracedSubroutine", { opentracing::ChildOf(&parentSpan->context()) });
    }
    
    // 无parentSpan的情况下创建Span。
    void tracedFunction()
    {
        auto span = opentracing::Tracer::Global()->StartSpan("tracedFunction");
        tracedSubroutine(span);
    }
    ```

4.  下载原生Jaeger Agent [jaeger-agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent)，并用以下参数启动Agent，以将数据上报至链路追踪Tracing Analysis。

    **说明：** 请将`<endpoint>`替换成链路追踪控制台概览页面上相应客户端和相应地域的接入点。关于获取接入点信息的方法，请参见前提条件中的[获取接入点信息](#tab2)。

    ```
    // reporter.grpc.host-port用于设置网关，网关因地域而异。 例如：
    $ nohup ./jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=<endpoint>
    ```


## 更多信息

