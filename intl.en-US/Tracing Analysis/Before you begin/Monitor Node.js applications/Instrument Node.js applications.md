# Instrument Node.js applications

This topic shows you how to instrument a Node.js application to perform tracing analysis.

Jaeger dependencies are added to the package of the Node.js project.

```
"dependencies": {
    "jaeger-client": "^3.12.0"
  }
```





## Procedure

1.  Set parameters for initialization.

    **Note:** Replace `<endpoint>` with the corresponding endpoint in the corresponding region that is displayed on the Overview page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    const initTracer = require("jaeger-client").initTracer;
    
    const config = {
        serviceName: 'node-service',
        sampler: {
            type: "const",
            param: 1
        },
        reporter: {
            collectorEndpoint: "<endpoint>"
        },
    };
    ```

2.  Create a Tracer object.

    ```
    const tracer = initTracer(config);
    ```

3.  Create a span.

    ```
    const span = tracer.startSpan("say-hello");
    
    // Optional. Set one or more tags.
    span.setTag("tagKey-01", "tagValue-01");
    
    // Optional. Set one or more logs.
    span.log({event: "timestamp", value: Date.now()});
    
    // Finish the span.
    span.finish();
    ```

4.  Log on to the Tracing Analysis console and view the trace.


## Complete sample code based on Express

```
const express = require("express");
const initTracer = require("jaeger-client").initTracer;
const app = express();

const config = {
    serviceName: 'node-service',
    sampler: {
        type: "const",
        param: 1
    },
    reporter: {
        collectorEndpoint: "<endpoint>"
    },
};
const tracer = initTracer(config);

app.all('*', function (req, res, next) {
    req.span = tracer.startSpan("say-hello");
    next();
});

app.get("/api", function (req, res) {
    const span = req.span;
    span.log({event: "timestamp", value: Date.now()});
    req.span.finish();
    res.send({code: 200, msg: "success"});
});

app.listen(3000, '127.0.0.1', function () {
    console.log('start');
});
```

[jaeger-client-node](https://github.com/jaegertracing/jaeger-client-node)

[opentracing-javascript](https://github.com/opentracing/opentracing-javascript)

