# Access Node.js applications

This topic describes how to connect a Node.js application to tracing analysis.

Configure the dependencies on the Jaeger Client in the Package of the Node project.

```

     "dependencies": { "jaeger-client": "^3.12.0" } 
   
```





## Procedure

1.  Configure parameters for metadata recovery.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

    ```
    
            const initTracer = require("jaeger-client").initTracer; const config = { serviceName: 'node-service', sampler: { type: "const", param: 1 }, reporter: { collectorEndpoint: "<endpoint>" }, }; 
          
    ```

2.  Create a Tracer instance object.

    ```
    
            const tracer = initTracer(config); 
          
    ```

3.  Create a Span instance object.

    ```
    
            const span = tracer.startSpan("say-hello"); // set one or more tags. This parameter is optional. span.setTag("tagKey-01", "tagValue-01"); // set one or more events. span.log({event: "timestamp", value: Date.now()}); // marks the end of Span. finish(); 
          
    ```

4.  Log on to the tracing analysis console and view the trace.


## Express-based Complete example

```

     const express = require("express"); const initTracer = require("jaeger-client").initTracer; const app = express(); const config = { serviceName: 'node-service', sampler: { type: "const", param: 1 }, reporter: { collectorEndpoint: "<endpoint>" }, }; const tracer = initTracer(config); app.all('*', function (req, res, next) { req.span = tracer.startSpan("say-hello"); next(); }); app.get("/api", function (req, res) { const span = req.span; span.log({event: "timestamp", value: Date.now()}); req.span.finish(); res.send({code: 200, msg: "success"}); }); app.listen(3000, '127.0.0.1', function () { console.log('start'); }); 
   
```

[jaeger-client-node](https://github.com/jaegertracing/jaeger-client-node)

[opentracing-javascript](https://github.com/opentracing/opentracing-javascript)

