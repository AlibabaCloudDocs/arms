# Quick Start with Tracing Analysis

This topic uses a Java application as an example to describe the process from activating and authorizing link tracing and related dependent services to connecting applications to link tracing, helping you get started with link tracing quickly.

-   Enable link tracking
-   Activate log service
-   Enable Access control

## Authorize Tracinng Analysis to read and write your log service data

1.  Log on [Link tracing console](https://tracing-analysis.console.aliyun.com/).

2.  In Overview Page, click **Authorization** to authorize Tracing Analysis to read and write your log service.

3.  In Cloud resource access authorization, select the required permissions and click **Agree to authorize**.

    ![Accessing Log Role](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1436676951/p53825.png)


## Report Java application data through the Jaeger client

This topic describes how to report data to Java applications by using the Jaeger client. For more information about how to report data and application data in other languages through other clients, see the relevant documents at the end of this topic.

1.  [Download the Demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerTracingDemo.zip)In the left-side navigation pane.manualDemoAnd run the program according to the Readme instructions.

2.  Open the pom. xml file and add the dependency on the Jaeger client.

    ```
    <dependency>
        <groupId>io.jaegertracing</groupId>
        <artifactId>jaeger-client</artifactId>
        <version>0.31.0</version>
    </dependency>
    ```

3.  Configure the initialization parameters and create a Tracer object.

    A Tracer object can be used to create a Span object to record the distributed operation time, pass data across machines through the Extract/Inject method, or set the current Span. The Tracer object is also configured with data such as the gateway address, local IP address, sampling rate, and service name. You can adjust the sampling rate to reduce the overhead caused by data reporting.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewAccess points of corresponding clients and regions on the page.

    ```
    // Replace terminaldemo with the name of your application.
    io.jaegertracing.Configuration config = new io.jaegertracing.Configuration(&quot;manualDemo&quot;);
    io.jaegertracing.Configuration.SenderConfiguration sender = new io.jaegertracing.Configuration.SenderConfiguration();
    // Replace <endpoint> with the endpoint of the corresponding client and region on the console overview page.
    sender.withEndpoint(&quot;<endpoint>&quot;);
    config.withSampler(new io.jaegertracing.Configuration.SamplerConfiguration().withType(&quot;const&quot;).withParam(1));
    config.withReporter(new io.jaegertracing.Configuration.ReporterConfiguration().withSender(sender).withMaxQueueSize(10000));
    GlobalTracer.register(config.getTracer());
    ```

4.  Record request data.

    ```
    Tracer tracer = GlobalTracer.get();
    // Create a Span
    Span span = tracer.buildSpan(&quot;parentSpan&quot;).withTag(&quot;myTag&quot;, &quot;spanFirst&quot;).start();
    tracer.scopeManager().activate(span, false);
    tracer.activeSpan().setTag(&quot;methodName&quot;, &quot;testTracing&quot;);
    // Business logic
    secondBiz();
    span.finish();
    ```

5.  Wait 2 ~ After three minutes, log on[Tracing Analysis console](https://tracing-sg.console.aliyun.com/), InApplication ListAnd view the reported link data.


After reporting application data to the link tracing console, you can perform the following operations in the link tracing console:

-   [View SQL performance analysis](/intl.en-US/Console guide/Application management/View SQL performance analysis.md)
-   [Manage apps and tags](/intl.en-US/Console guide/Application management/Manage applications and tags.md)

