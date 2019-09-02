# ARMS-SDK 使用说明 {#concept_95081_zh .concept}

借助 ARMS 提供的 SDK，您可以在业务代码中动态获取 TraceId 及相关调用链属性。

## 前提条件 {#section_eb3_bsw_fgb .section}

-   您已在 ARMS 控制台上创建应用监控，并已在 Java 程序中挂载和启动应“”用监控的 Agent。详情请参考[为 Java 应用安装探针](intl.zh-CN/应用监控/开始监控 Java 应用/以普通方式安装探针/为 Java 应用安装探针.md#)中关于安装 Java 探针的步骤。

-   程序中已引入 arms-sdk-1.7.1.jar。

    ``` {#codeblock_opb_ghs_40w}
     <dependency>
    <groupId>com.alibaba.arms.apm</groupId>
    <artifactId>arms-sdk</artifactId>
    <version>1.7.1</version>
    </dependency>
    ```

    **说明：** 如果无法获取 Pom，请直接下载 [arms-sdk-1.7.1.jar](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/arms-sdk-1.7.1.jar)。


## 获取 TraceId 与 RpcId {#section_o1l_dsw_fgb .section}

满足前提条件后，即可通过以下代码获取上下文的 TraceId 与 RpcId。

``` {#codeblock_9yf_i8n_0ys}
Span span = Tracer.builder().getSpan();
String traceId = span.getTraceId();
String rpcId = span.getRpcId();
```

## 透传业务自定义标签 {#section_djy_gsw_fgb .section}

要透传业务自定义标签，需要在代码中写入添加和获取自定义标签的步骤。

1.  在业务代码中添加自定义标签（baggage）。

    ``` {#codeblock_4mt_pns_90h}
    Map<String, String> baggage = new HashMap<String, String>();
    baggage.put("key-01", "value-01");
    baggage.put("key-02", "value-02");
    baggage.put("key-03", "value-03");
    Span span = Tracer.builder().getSpan();
    span.withBaggage(baggage);
    ```

2.  在业务代码中获取自定义标签（baggage）。

    ``` {#codeblock_5w1_zqi_117}
    Span span = Tracer.builder().getSpan();
    Map<String, String> baggage = span.baggageItems();
    ```


