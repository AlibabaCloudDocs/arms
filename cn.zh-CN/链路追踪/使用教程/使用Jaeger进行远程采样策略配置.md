# 使用Jaeger进行远程采样策略配置

通过远程采样策略配置，您可以直接在链路追踪控制台上配置采样策略，而不需要修改代码。

采样指从全量采集的所有链路数据中，采集部分数据进行分析。采样决策包括采集数据和不采集数据。采样有以下类型：

-   事前采样：在用户访问开始时进行采样决策，Jaeger的采样是事前采样。
-   事后采样：在用户访问执行过程或者访问过程中进行采样决策。

## 采样流程

以一个简单的调用关系为例：A-\>B-\>C（服务A调用服务B，同时，服务B调用服务C），服务A为头节点。当服务A收到不包含跟踪信息的请求时，Jaeger跟踪器将开始新的跟踪：

1.  Jaeger跟踪器将为服务A、服务B以及服务C分配一个随机跟踪ID，并根据当前配置的采样策略做出采样决策。
2.  采样决策将与请求一起传播到服务B和服务C，这些服务将不做采样决策，而是接受头节点服务A的采样决策。

这种方法保证链路上所有Span都被记录在后端。 如果每个服务都做出自己的采样决策，那么您将很难在后端获得完整的调用链路。

**说明：** 只有头节点的采样策略会生效，例如服务A、B、C中都配置采样策略：

-   对于调用链路为A-\>B-\>C，只有A的采样策略会生效。
-   对于调用链路为B-\>C-\>A，只有B的采样策略会生效。

## 配置客户端

您需要在构建Trace对象时，将采样类型配置成Remote，采样的服务地址配置成链路追踪的采样地址。详情请参见[通过Jaeger上报Java应用数据](/cn.zh-CN/准备工作/开始监控Java应用/通过Jaeger上报Java应用数据.md)。将控制台上的接入点信息做简单修改后，您可以得到采样地址：

-   将`api/traces`改成`/api/sampling`。
-   去掉`http://`。

例如，将

```
http://tracing-analysis-dc-hz.aliyuncs.com/adapt_******_******/api/traces
```

修改为

```
tracing-analysis-dc-hz.aliyuncs.com/adapt_******_******/api/sampling
```

代码示例如下：

```
 io.jaegertracing.Configuration config = new io.jaegertracing.Configuration("your application name");
config.withSampler(new Configuration.SamplerConfiguration().withType("remote")
.withManagerHostPort("tracing-analysis-dc-hz.aliyuncs.com/adapt_ao123458@abcdefg_ao123458@fghijklm/api/sampling")
.withParam(0.1));
```

**说明：** 如果您在客户端配置成远程采样方式，但是没有在服务端未配置采样策略，系统将会按照固定比例0.001（0.1%）进行采样。

## 配置服务端

您需要先在客户端完成配置，才能在服务端配置采样策略。您的配置将对所有配置了远程采样方式的Jaeger client生效。

有以下级别的采样策略：

-   `default_strategy`：默认策略，必须配置。它还包括共享的per-operation策略，这些per-operation策略将适用于配置中未列出的，没有Service级别和Span级别的任何所有服务。
-   `service_strategies`：Service级别的采样策略，可选。
-   `operation_strategies`：Span级别的采样策略，可选。

有以下类型的采样策略：

-   比例采样：`default_strategy`、`service_strategies`以及`operation_strategies`可配置。
-   速率采样：`default_strategy`以及`service_strategies`可配置。

以下是一个示例：

```
{
  "service_strategies": [
    {
      "service": "foo",
      "type": "probabilistic",
      "param": 0.8,
      "operation_strategies": [
        {
          "operation": "op1",
          "type": "probabilistic",
          "param": 0.2
        },
        {
          "operation": "op2",
          "type": "probabilistic",
          "param": 0.4
        }
      ]
    },
    {
      "service": "bar",
      "type": "ratelimiting",
      "param": 5
    }
  ],
  "default_strategy": {
    "type": "probabilistic",
    "param": 0.5,
    "operation_strategies": [
      {
        "operation": "/health",
        "type": "probabilistic",
        "param": 0.0
      },
      {
        "operation": "/metrics",
        "type": "probabilistic",
        "param": 0.0
      }
    ]
  }
}
```

在示例中：

-   应用foo的所有操作均以0.8的比例进行采样，但op1和op2分别以0.2的比例和0.4的比例进行采样。
-   应用bar的所有Span埋点均以每秒5条链路的速率进行采样。
-   其他应用将以default\_strategy定义的概率0.5进行采样。

另外，在此示例中，我们通过使用概率0禁用了对所有服务的/health和/metrics端点的跟踪。

