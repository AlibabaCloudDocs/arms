# Use Jaeger to configure remote sampling policies

You can configure the remote sampling policy in the link trace console without modifying the code.

Sampling refers to the process in which partial data is collected from all link data for analysis. Sampling decisions include collecting data and not collecting data. The following types of sampling are available:

-   Pre-sampling: the sampling decision is made at the beginning of the user visit, and the Jaeger sampling is pre-sampling.
-   Post-event sampling: samples are taken during user access to the execution or decision-making process.

## Sampling process

Take A simple call relationship as an example: Service A- \> Service B- \> service C \(service A Calls Service B, and service B calls service C\). Service A is the head node. When service A receives A request that does not contain tracking information, the Jaeger tracker starts A new tracking:

1.  The Jaeger tracker assigns A random tracking ID to service A, service B, and service C, and makes A sampling decision based on the currently configured sampling policy.
2.  The sampling decision will be propagated to services B and C along with the request, and these services will not make the sampling decision, but accept the sampling decision of the head Node Service A.

This method ensures that all spans on the link are recorded at the back end. If each service makes its own sampling decision, then it will be very difficult for you to get a complete Call link on the back end.

**Note:** Only the sampling policy of the head node takes effect. For example, the sampling policy is configured for services A, B, and C:

-   For the trace A- \>B-\>C, only the sampling policy of A takes effect.
-   For the trace B- \>C-\>A, only the sampling policy of B takes effect.

## Configure the client

When creating the Trace object, you must set the sampling type to Remote and the sampling service address to the sampling address of the link tracing. For more information, see [Use Jaeger to report Java application data](/intl.en-US/Preparations/Start monitoring Java applications/Use Jaeger to report Java application data.md). After simply modifying the access point information on the console, you can obtain the sampling address:

-   Replace `api/traces` with `/api/sampling`.
-   Remove `http://`.

For example, the

```

      http://tracing-analysis-dc-hz.aliyuncs.com/adapt_******_******/api/traces 
    
```

to

```

      tracing-analysis-dc-hz.aliyuncs.com/adapt_******_******/api/sampling 
    
```

Sample code:

```

     io.jaegertracing.Configuration config = new io.jaegertracing.Configuration("your application name"); config.withSampler(new Configuration.SamplerConfiguration().withType("remote") .withManagerHostPort("tracing-analysis-dc-hz.aliyuncs.com/adapt_ao123458@abcdefg_ao123458@fghijklm/api/sampling") .withParam(0.1)); 
   
```

**Note:** If you have configured the remote sampling method on the client but have not configured the sampling policy on the server, the system takes the sampling according to a fixed ratio of 0.001\(0.1%\).

## Configure Server

You must complete the configuration on the client before you can configure the sampling policy on the server. The configuration takes effect on all Jaeger clients that have configured remote sampling.

There are the following levels of sampling policies:

-   `default_strategy`: the default policy. This parameter is required. It also includes shared per-operation policies that will apply to any Service not listed in the configuration that does not have the Service level and Span level.
-   `Service_clusters`: the Service-level sampling policy. This parameter is optional.
-   `operation_strategies`: the Span-level sampling policy. This parameter is optional.

There are the following types of sampling policies:

-   Proportional sampling: you can set the `default_strategy`, `service_strategies`, and `operation_strategies` parameters.
-   Rate Sampling: you can set the `default_strategy` and `service_clusters` parameters.

The following is an example:

```

     { "service_strategies": [ { "service": "foo", "type": "probabilistic", "param": 0.8, "operation_strategies": [ { "operation": "op1", "type": "probabilistic", "param": 0.2 }, { "operation": "op2", "type": "probabilistic", "param": 0.4 } ] }, { "service": "bar", "type": "ratelimiting", "param": 5 } ], "default_strategy": { "type": "probabilistic", "param": 0.5, "operation_strategies": [ { "operation": "/health", "type": "probabilistic", "param": 0.0 }, { "operation": "/metrics", "type": "probabilistic", "param": 0.0 } ] } } 
   
```

In the example:

-   All operations in which foo is applied are sampled in a ratio of 0.8, but op1 and op2 are sampled in a ratio of 0.2 and a ratio of 0.4 respectively.
-   All Span burial points of the application bar are sampled at a rate of 5 links per second.
-   Other applications will sample with a probability of 0.5 defined by the default\_strategy.

In addition, in this example, we disable tracking of /health and /metrics endpoints for all services by using probability 0.

