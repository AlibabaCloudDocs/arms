# OpenTelemetry Java SDK支持

本文主要介绍如何通过OpenTelemetry开源SDK手动埋点监控您的应用。

该功能要求ARMS探针版本为公测版本v2.7.1.3及以上。请联系ARMS钉钉服务账号`arms160804`，为您进行探针新版本升级。

云原生背景下，由OpenTracing演进而来的[OpenTelemetry](https://opentelemetry.io)提供了多达数十种语言的SDK ，基于一套规范的API和统一的数据格式，成为可观测的事实标准。

ARMS Java Agent从版本v2.7.1.3开始，内置对[OpenTelemetry Java SDK](https://github.com/open-telemetry/opentelemetry-java)的支持。如果您的应用已经通过OpenTelemetry Java SDK手动埋点，则无需任何改动，ARMS会将相关的Span记录作为独立入口或者内部方法栈，从而监控您的应用。如果您的应用尚未埋点，请先通过依赖OpenTelemetry Java SDK，实现手动埋点。

## 手动埋点

如果您的应用尚未埋点，请先通过引入以下Maven依赖，实现手动埋点。更多信息，请参见[OpenTelemetry官方文档](https://opentelemetry.io/docs/java/manual_instrumentation/)。

```
<dependencies>   
    <dependency>
        <groupId>io.opentelemetry</groupId>
        <artifactId>opentelemetry-api</artifactId>
    </dependency>
    <dependency>
          <groupId>io.opentelemetry</groupId>
        <artifactId>opentelemetry-sdk-trace</artifactId>
    </dependency>
    <dependency>
          <groupId>io.opentelemetry</groupId>
        <artifactId>opentelemetry-sdk</artifactId>
    </dependency>
    <dependency>
          <groupId>io.opentelemetry</groupId>
        <artifactId>opentelemetry-exporter-logging</artifactId>
    </dependency>
</dependencies>

<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>io.opentelemetry</groupId>
      <artifactId>opentelemetry-bom</artifactId>
      <version>1.2.0</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
```

## ARMS对OpenTelemetry埋点的兼容

ARMS对OpenTelemetry埋点的兼容的介绍涉及以下名词，OpenTelemetry相关的其他名称解释，请参见[OpenTelemetry Specification](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/trace/api.md)。

-   Span：一次请求的一个具体操作，比如远程调用入口或者内部方法调用。
-   SpanContext：一次请求追踪的上下文，用于关联该次请求下的具体操作。
-   Attribute：Span的附加属性字段，用于记录关键信息。

OpenTelemetry的Span可以分为三类：

-   入口Span：会创建新的SpanContext，例如Server、Consumer。

    **说明：** 对于此类Span，ARMS的埋点入口多位于框架内部，手动埋点时链路上下文已存在，ARMS会将OpenTelemetry的入口Span作为内部Span处理。对于ARMS没有埋点的入口，则OpenTelemetry的入口Span保持不变，例如异步调用或者自定义RPC框架入口，同时ARMS会在客户端聚合，生成相关统计数据。

-   内部Span：会复用已经创建的SpanContext，作为内部方法栈记录。
-   出口Span：会将SpanContext透传下去，例如Client、Producer。

目前，ARMS对于入口Span和内部Span做了兼容。对于出口Span，ARMS暂不支持按照OpenTelemetry标准透传，而是按照ARMS自定义格式透传。

例如以下代码：

```
package com.alibaba.arms.brightroar.console.controller;

import io.opentelemetry.api.OpenTelemetry;
import io.opentelemetry.api.common.AttributeKey;
import io.opentelemetry.api.common.Attributes;
import io.opentelemetry.api.trace.Span;
import io.opentelemetry.api.trace.SpanKind;
import io.opentelemetry.api.trace.StatusCode;
import io.opentelemetry.api.trace.Tracer;
import io.opentelemetry.api.trace.propagation.W3CTraceContextPropagator;
import io.opentelemetry.context.Scope;
import io.opentelemetry.context.propagation.ContextPropagators;
import io.opentelemetry.exporter.logging.LoggingSpanExporter;
import io.opentelemetry.sdk.OpenTelemetrySdk;
import io.opentelemetry.sdk.trace.SdkTracerProvider;
import io.opentelemetry.sdk.trace.export.BatchSpanProcessor;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.bind.annotation.RestController;

import javax.annotation.PostConstruct;
import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;

@RestController
@RequestMapping("/ot")
public class OpenTelemetryController {

    private Tracer tracer;

    private ScheduledExecutorService ses = Executors.newSingleThreadScheduledExecutor();

    @PostConstruct
    public void init() {
        SdkTracerProvider sdkTracerProvider = SdkTracerProvider.builder()
                .addSpanProcessor(BatchSpanProcessor.builder(new LoggingSpanExporter()).build())
                .build();

        OpenTelemetry openTelemetry = OpenTelemetrySdk.builder()
                .setTracerProvider(sdkTracerProvider)
                .setPropagators(ContextPropagators.create(W3CTraceContextPropagator.getInstance()))
                .buildAndRegisterGlobal();

        tracer = openTelemetry.getTracer("manual-sdk", "1.0.0");

        ses.scheduleAtFixedRate(new Runnable() {
            @Override
            public void run() {
                Span span = tracer.spanBuilder("schedule")
                        .setAttribute("schedule.time", System.currentTimeMillis())
                        .startSpan();
                try (Scope scope = span.makeCurrent()) {
                    System.out.println("scheduled!");
                    Thread.sleep(500L);
                    span.setAttribute("schedule.success", true);
                } catch (Throwable t) {
                    span.setStatus(StatusCode.ERROR, t.getMessage());
                } finally {
                    span.end();
                }
            }
        }, 10, 30, TimeUnit.SECONDS);
    }

    @ResponseBody
    @RequestMapping("/parent")
    public String parent() {
        Span span = tracer.spanBuilder("parent").setSpanKind(SpanKind.SERVER).startSpan();
        try (Scope scope = span.makeCurrent()) {
            child();
            span.setAttribute("http.method", "GET");
            span.setAttribute("http.uri", "/parent");
        } finally {
            span.end();
        }
        return "parent";
    }

    private void child() {
        Span span = tracer.spanBuilder("child").startSpan();
        try (Scope scope = span.makeCurrent()) {
            span.addEvent("Sleep Start");
            Thread.sleep(1000);
            Attributes attr = Attributes.of(AttributeKey.longKey("cost"), 1000L);
            span.addEvent("Sleep End", attr);
        } catch (Throwable e) {
            span.setStatus(StatusCode.ERROR, e.getMessage());
        } finally {
            span.end();
        }
    }

}
```

以上示例代码中通过OpenTelemetry SDK创建了三个Span：

-   `parent`：按照OpenTelemetry标准是HTTP入口，但是由于ARMS在Tomcat内置代码中已经创建了链路上下文，因此这里会作为一个内部方法记录在ARMS方法栈上。
-   `child`：`parent` Span的内部Span，作为内部方法记录在方法栈上。
-   `schedule`：独立线程入口Span，默认情况下ARMS没有为此类入口创建上下文，因此这里会作为一个自定义方法入口，并生成相应的统计数据。

**在ARMS控制台查看`parent`和`child`**

在ARMS控制台找到/ot/parent的HTTP入口的内部方法栈，可以看到多了以下Span的展示。更多信息，请参见[调用链路查询](/intl.zh-CN/应用监控/控制台功能/调用链路查询.md)。

![OTel埋点内部Span](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9578223261/p282368.png)

**在ARMS控制台查看`schedule`**

ARMS控制台支持通过以下几个页面查看：

-   可以在ARMS控制台应用总览页面看到自定义入口的统计。更多信息，请参见[应用总览](/intl.zh-CN/应用监控/控制台功能/应用总览.md)。

    ![OTel埋点出口Span](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9578223261/p282372.png)

-   可以在接口调用页面查看Span详细信息。更多信息，请参见[接口调用](/intl.zh-CN/应用监控/控制台功能/接口调用.md)。

    ![Otel接口调用页面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9578223261/p282375.png)

-   可以在调用链路页面看到独立的入口。更多信息，请参见[调用链路查询](/intl.zh-CN/应用监控/控制台功能/调用链路查询.md)。

    ![OTel埋点调用链查询](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9578223261/p282381.png)

    单击详情列的放大镜图标，可以查看入口的详细信息。

    ![Otel埋点调用链详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9578223261/p282420.png)

    目前ARMS支持将OpenTelemetry Span的Attribute作为Tags展示，将鼠标悬浮于Span名称后面的**Tags**即可看到Span的Attribute。

    ![Span的Attribute](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9578223261/p282430.png)


