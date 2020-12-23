# 接入Node.js应用

本文介绍了如何将Node.js应用接入链路追踪。

在Node工程的Package中配置对Jaeger Client的依赖。

```
"dependencies": {
    "jaeger-client": "^3.12.0"
  }
```





## 操作步骤

1.  初始化配置。

    **说明：** 请将`<endpoint>`替换成链路追踪控制台概览页面上相应客户端和相应地域的接入点。关于获取接入点信息的方法，请参见前提条件中的[获取接入点信息](#tab2)。

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

2.  创建Tracer实例对象。

    ```
    const tracer = initTracer(config);
    ```

3.  创建Span实例对象。

    ```
    const span = tracer.startSpan("say-hello");
    
    // 设置标签（可选，支持多个）。
    span.setTag("tagKey-01", "tagValue-01");
    
    // 设置事件（可选，支持多个）。
    span.log({event: "timestamp", value: Date.now()});
    
    // 标记Span结束span.finish();
    ```

4.  登录链路追踪控制台并查看调用链。


## 基于Express的完整示例

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

