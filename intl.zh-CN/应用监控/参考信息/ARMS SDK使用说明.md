# ARMS SDK使用说明

借助ARMS提供的SDK，您可以在业务代码中动态获取TraceId及相关调用链属性。

## 前提条件

-   已在ARMS控制台上创建应用监控，并已在Java程序中挂载和启动应用监控的Agent。具体操作，请参见[为Java应用手动安装Agent](/intl.zh-CN/应用监控/开始监控 Java 应用/为Java应用手动安装Agent.md)。
-   程序中已引入arms-sdk-1.7.3.jar依赖。

    ```
    <dependency>
        <groupId>com.alibaba.arms.apm</groupId>
        <artifactId>arms-sdk</artifactId>
        <version>1.7.3</version>
    </dependency>
    ```

    **说明：** 如果无法获取pom.xml中的依赖，请直接下载[arms-sdk-1.7.3.jar](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/arms-sdk-1.7.3.jar)。


## 获取TraceId与RpcId

您可通过以下代码获取TraceId与RpcId。

```
Span span = Tracer.builder().getSpan();
String traceId = span.getTraceId();
String rpcId = span.getRpcId();
```

## 透传业务自定义标签baggage

若您要透传业务自定义标签，则需要在代码中写入添加和获取自定义标签，具体操作步骤如下：

1.  在业务代码中添加自定义标签baggage。

    ```
    Map<String, String> baggage = new HashMap<String, String>();
    baggage.put("key-01", "value-01");
    baggage.put("key-02", "value-02");
    baggage.put("key-03", "value-03");
    Span span = Tracer.builder().getSpan();
    span.withBaggage(baggage);
    ```

2.  在业务代码中获取自定义标签baggage。

    ```
    Span span = Tracer.builder().getSpan();
    Map<String, String> baggage = span.baggageItems();
    ```


## 为Span设置自定义标签tag

为Span设置自定义标签只会在当前Span中有效，并不会透传。您需要在代码中写入添加和获取自定义的标签，具体操作步骤如下：

1.  在业务代码中为Span添加自定义标签tag，可以添加多个标签。

    ```
    Span span = Tracer.builder().getSpan();
    // Add a tag to the Span.
    span.setTag("tag-key1", "tag-value1");
    span.setTag("tag-key2", "tag-value2");
    ```

2.  在业务代码中获取Span自定义标签tag。

    ```
    Span span = Tracer.builder().getSpan();
    // Inspect the Span's tags.
    Map<String, String> tags = span.tags();
    ```


## 根据自定义标签baggage和tag查询调用链

通过Span设置的自定义标签baggage和tag可以用来按标签维度查询调用链。

-   baggage上的标签具有透传到下游效果，一般用于业务染色，标签项不建议设置过多。
-   tag上的标签只在本Span作用域内有效，可以设置多个业务项。

1.  登录[ARMS控制台](https://arms-intl.console.aliyun.com/)。
2.  在左侧导航栏选择**应用监控** \> **调用链路查询**，并在顶部菜单栏选择目标地域。
3.  在调用链路查询页面选择**参数名**，在**参数值**中填入自定义标签，单击**查询**。
4.  在**调用链路查询**列表中单击目标链路的**TraceID**。

    ![trace_query_with_tag](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7290348951/p142195.png)

5.  在调用链路详情页面，鼠标移动至**服务名称**，会显示当前Span对应的Tags信息（baggage内容会自动加入到每个Span的Tags上）。

    ![trace_span_with_tags](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8290348951/p142196.png)


