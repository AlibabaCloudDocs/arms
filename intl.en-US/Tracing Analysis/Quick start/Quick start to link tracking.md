# Quick start to link tracking

This topic uses a Java application as an example to describe how to connect the Java application to tracing analysis, from activating tracing analysis, granting necessary permissions on ECS instances, and connecting the application to tracing analysis, helping you quickly get started with tracing analysis.

-   Enable link tracking
-   Activate log service
-   Activate access control

## Authorize Tracinng Analysis to read and write your log service data

1.  Log on [Link tracing console](https://tracing-analysis.console.aliyun.com/).

2.  In Overview Page, click **Authorization** to authorize Tracing Analysis to read and write your log service.

3.  In Cloud resource access authorization, select the required permissions and click **Agree to authorize**.

    ![Accessing Log Role](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1436676951/p53825.png)


## Use the Jaeger client to report Java application data

This topic describes how to use the Jaeger client to report data to a Java application as an example. For more information about how to use other clients to report data and applications using other languages, see the documentation at the end of this topic.

1.  [Download the Demo project](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/jaegerTracingDemo.zip), go to the manualDemo directory, and run the program following the instructions in Readme.

2.  Open the pom. xml file and add the dependency on the Jaeger client.

    ```
    <dependency>
        <groupId>io.jaegertracing</groupId>
        <artifactId>jaeger-client</artifactId>
        <version>0.31.0</version>
    </dependency>
    ```

3.  Configure initialization parameters and create a Tracer object.

    A Tracer object can be used to create spans to record distributed operation times, transparently transmit data across machines using the Extract/Inject method, or set the current Span. The Tracer object is also configured with data such as the gateway address, local IP address, sample rate, and service name. You can adjust the sample rate to reduce the overhead due to upstream data.

    **Note:** I should be grateful if you would have `<endpoint>`replaces the link trace console cluster setup page of the respective client and region of the access point.

    ```
    
            // Replace manualDemo with the name of your application io.jaegertracing.Configuration config = new io.jaegertracing.Configuration("manualDemo"); io.jaegertracing.Configuration.SenderConfiguration sender = new io.jaegertracing.Configuration.SenderConfiguration(); // replace manualDemo with the <endpoint> name of the application that is sent by the access point of the corresponding client and region on the overview page of the console. withEndpoint("<endpoint>"); config.withSampler(new io.jaegertracing.Configuration.SamplerConfiguration().withType("const").withParam(1)); config.withReporter(new io.jaegertracing.Configuration.ReporterConfiguration().withSender(sender).withMaxQueueSize(10000)); GlobalTracer.register(config.getTracer()); 
          
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

5.  After two to three minutes, log on to the . [Tracing Analysis console](https://tracing-sg.console.aliyun.com/). View the reported Tracing data on the applications page.


After reporting application data to the tracing analysis console, you can perform the following operations:

-   [View key application performance metrics and topology](/intl.en-US/Console guide/Application management/View key application performance metrics and topology.md)
-   [View application details](/intl.en-US/Console guide/Application management/View application details.md)
-   [View API usage](/intl.en-US/Console guide/Application management/View API usage.md)
-   [View SQL performance analysis](/intl.en-US/Console guide/Application management/View SQL performance analysis.md)
-   [Manage apps and tags](/intl.en-US/Console guide/Application management/Manage applications and tags.md)

