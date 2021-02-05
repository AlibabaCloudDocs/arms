# Get started with Tracing Analysis

This topic shows you how to activate Tracing Analysis and dependent services, grant permissions, and report application data to Tracing Analysis. This helps you get started with Tracing Analysis. In the example demonstrated in this topic, a Java application is used.

-   Tracing Analysis is activated.
-   Log Service is activated.
-   Resource Access Management \(RAM\) is activated.

## Authorize Tracinng Analysis to read and write your log service data

1.  Log on [Link tracing console](https://tracing-analysis.console.aliyun.com/).

2.  In Overview Page, click **Authorization** to authorize Tracing Analysis to read and write your log service.

3.  In Cloud resource access authorization, select the required permissions and click **Agree to authorize**.

    ![Accessing Log Role](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1436676951/p53825.png)


## Use Jaeger to report data of a Java application

In the following example, Jaeger is used to report data of a Java application. For more information about how to use other clients to report data and how to report data of applications that are developed in other languages, see the references at the end of this topic.

1.  Download the [demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerTracingDemo.zip). Go to the manualDemo directory and run the program as instructed in the README.md file.

2.  Open the pom. xml file and add the dependency on the Jaeger client.

    ```
    <dependency>
        <groupId>io.jaegertracing</groupId>
        <artifactId>jaeger-client</artifactId>
        <version>0.31.0</version>
    </dependency>
    ```

3.  Set initialization parameters and create a tracer.

    A tracer can be used to create spans to record distributed operation time, transmit data across servers in pass-through mode by using the Extract or Inject method, or set the current span. The tracer also contains data such as the endpoint used for data reporting, local IP address, sample rate, and service name. You can adjust the sample rate to reduce the overhead that is caused by data reporting.

    **Note:** Replace `<endpoint>` with the endpoint for your client and region. You can log on to the Tracing Analysis console and obtain the endpoint on the Access point information tab of the Cluster Configurations page.

    ```
    // Replace manualDemo with your application name.
    io.jaegertracing.Configuration config = new io.jaegertracing.Configuration("manualDemo");
    io.jaegertracing.Configuration.SenderConfiguration sender = new io.jaegertracing.Configuration.SenderConfiguration();
    // Replace <endpoint> with the endpoint for your client and region. You can log on to the Tracing Analysis console and obtain the endpoint on the Access point information tab of the Cluster Configurations page.
    sender.withEndpoint("<endpoint>");
    config.withSampler(new io.jaegertracing.Configuration.SamplerConfiguration().withType("const").withParam(1));
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

5.  Wait for 2 to 3 minutes. Then, log on to the [Tracing Analysis console](https://tracing-sg.console.aliyun.com/) and view the trace data that has been reported on the Applications page.


After the application data is reported to Tracing Analysis, you can perform the following operations in the Tracing Analysis console:

-   [View the key performance metrics and topology of an application](/intl.en-US/Operations in the Console/Application management/View the key performance metrics and topology of an application.md)
-   [View application details](/intl.en-US/Operations in the Console/Application management/View application details.md)
-   [View the details of span calls](/intl.en-US/Operations in the Console/Application management/View the details of span calls.md)
-   [View the analysis results of SQL performance](/intl.en-US/Operations in the Console/Application management/View the analysis results of SQL performance.md)
-   [Manage applications and tags](/intl.en-US/Operations in the Console/Application management/Manage applications and tags.md)

