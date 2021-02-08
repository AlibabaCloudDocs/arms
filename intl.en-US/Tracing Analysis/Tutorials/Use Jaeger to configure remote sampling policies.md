# Use Jaeger to configure remote sampling policies

You can directly configure remote sampling policies in the Tracing Analysis console, without the need to modify the code.

Sampling refers to the process in which partial data is sampled from all collected trace data for analysis. Jaeger can make a sampling decision to sample or not to sample data. Jaeger can implement sampling in the following stages:

-   Before the visit: Jaeger can implement sampling before a user visits a service.
-   After the visit: Jaeger can implement sampling after a user visits a service or when a user is visiting a service.

## Sampling process

In this example, the following call process is used: A \> B \> C. In this process, Service A calls Service B and Service B calls Service C. Service A is the head node of the process. When Service A receives a request that contains no trace data, the Jaeger tracer starts a new trace.

1.  The Jaeger tracer creates a random trace ID for Service A, Service B, and Service C. Then, Jaeger makes a sampling decision based on the current sampling policy.
2.  The sampling decision is sent to Service B and Service C along with the request. The two services then make no sampling decision but accept the sampling decision of the head node Service A.

This way, all the spans can be recorded at the backend. If each service makes its own sampling decision, you may have difficulty in obtaining complete trace data for service calls at the backend.

**Note:** Only the sampling policy of the head node takes effect. Assume that you have configured sampling policies for Service A, Service B, and Service C:

-   If the service call is in the sequence of A \> B \> C, only the sampling policy of Service A takes effect.
-   If the service call is in the sequence of B \> C \> A, only the sampling policy of Service B takes effect.

## Configure the client

When you create a Tracer object, you must set the sampling type to remote and set the endpoint that is used for sampling to the sampling endpoint of Tracing Analysis. For more information, see [Use Jaeger to report Java application data](/intl.en-US/Before you begin/Monitor Java applications/Use Jaeger to report Java application data.md). You can obtain the sampling endpoint of Tracing Analysis by modifying the endpoint that is obtained from the console:

-   Replace `/api/traces` with `/api/sampling`.
-   Omit `http://`.

For example, the original endpoint is:

```
http://tracing-analysis-dc-hz.aliyuncs.com/adapt_******_******/api/traces
```

The sampling endpoint is:

```
tracing-analysis-dc-hz.aliyuncs.com/adapt_******_******/api/sampling
```

Sample code:

```
 io.jaegertracing.Configuration config = new io.jaegertracing.Configuration("your application name");
config.withSampler(new Configuration.SamplerConfiguration().withType("remote")
.withManagerHostPort("tracing-analysis-dc-hz.aliyuncs.com/adapt_ao123458@abcdefg_ao123458@fghijklm/api/sampling")
.withParam(0.1));
```

**Note:** If you have configured remote sampling policies on the client but have not configured sampling policies on the server, the system samples data at the fixed sampling proportion of 0.001 \(0.1%\).

## Configure the server

You must configure the client before you can configure sampling policies on the server. Your configuration on the server takes effect on all the Jaeger clients where remote sampling policies are configured.

The following levels of sampling policies are supported:

-   `default_strategy`: the default sampling policy, which is required. The default sampling policy includes the shared per-operation policies that apply to all the services that are excluded from the configuration and have no sampling policies at the service or span level.
-   `service_strategies`: the sampling policies at the service level. This policy level is optional.
-   `operation_strategies`: the sampling policies at the span level. This policy level is optional.

The following types of sampling policies are supported:

-   Sampling by proportion: applies to the `default_strategy`, `service_strategies`, and `operation_strategies` levels.
-   Sampling by speed: applies to the `default_strategy` and `service_strategies` levels.

Example:

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

In the example:

-   Data of the foo service is sampled at the sampling proportion of 0.8. However, data of the op1 span is sampled at the sampling proportion of 0.2 and data of the op2 span is sampled at the sampling proportion of 0.4.
-   Data of all the spans of the bar service is sampled at the speed of five traces per second.
-   Data of other services is sampled at the sampling proportion of 0.5 that is specified by the default\_strategy level.

In addition, in this example, the sampling proportion 0 is used to disable the tracing of the /health and /metrics spans for all services.

