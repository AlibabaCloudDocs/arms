# ARMS与链路追踪Tracing Analysis的区别

应用实时监控服务ARMS与链路追踪Tracing Analysis都可以解决分布式环境下的链路追踪问题，那么二者有什么区别呢？本文将介绍ARMS与链路追踪的区别。

## 背景信息

应用实时监控服务ARMS是一款阿里云应用性能管理（Application Performance Management，简称APM）类监控产品。借助本产品，您可以基于前端、应用、业务自定义等维度，迅速便捷地为企业构建秒级响应的应用监控能力。

链路追踪为分布式应用的开发者提供了完整的调用链路还原、调用请求量统计、链路拓扑和应用依赖分析等工具。链路追踪能够帮助开发者快速分析和诊断分布式应用架构下的性能瓶颈，提高微服务时代下的开发诊断效率，并省去您搭建各类链路监控应用（Jaeger、Zipkin等）和相关存储服务（Hbase、ElasticSearch等）的成本。

## 整体对比

|差异项|ARMS|链路追踪|
|---|----|----|
|产品定位|APM工具类产品，产品本身含应用性能监控、用户体验监控、调用链追踪和问题诊断等多项功能。|专注分布式链路追踪功能|
|接入方式|无侵入式Agent加载方式接入|侵入式SDK编程方式接入|
|计费模式|按探针数量付费，极具竞争力的产品价格。|按请求数付费，极具竞争力的产品价格。|
|应用程序语言支持|Java和PHP|Java、PHP、Go、Python、JS、.NET、C++ 等|
|线程和内存诊断|支持|不支持|
|本地方法堆栈|支持|不支持|

下文将从产品定位、接入方式以及计费模式三个方面来详细介绍ARMS与链路追踪的区别。

## 产品定位对比

从功能定位上看，ARMS定位于重量级的应用性能管理类工具，功能相对丰富。应用程序通过挂载Agent方式接入监控，并且Agent提供性能监控、用户体验监控、调用链追踪以及故障诊断等多种功能。

而链路追踪定位于分布式链路追踪解决方案工具，功能比较专一，面向专业解决分布式环境下的链路追踪问题。您可以通过接入链路追踪SDK来实现分布式链路追踪，SDK本身只负责链路监控，功能相对专注。

![ARMS and xTrace Differences](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5520496851/p65778.png)

## 接入方式对比

定位于应用性能管理的ARMS的监控接入方式是业界商用APM工具中比较流行的无侵入式接入方案，您无需改动代码，即可接入。一般需要在应用程序中加载Agent，并且修改程序启动方式。以ARMS为例，在启动Java程序时需要增加-javaagent启动参数。

定位于分布式链路追踪的链路追踪是基于[Jaeger](https://github.com/jaegertracing/jaeger)和[Zipkin](https://github.com/openzipkin/zipkin)等开源产品和[Opentracing](https://github.com/opentracing)开源标准的监控产品。您可以使用基于以上任意一种标准的SDK接入到链路追踪中，这种方式的优势在于：

-   已使用Jaeger、Zipkin或其他Opentracing标准SDK的应用可无缝迁移到链路追踪中，无需修改代码。
-   由于链路追踪SDK是基于开源标准的，因此您无需担心Lock-in问题。
-   借助社区力量，您可以一次性大量支持多种开发语言，使得面向异构环境的开发者在链路监控方面的接入门槛大幅降低。

![Access Difference](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5520496851/p65793.png)

## 计费模式对比

和其他APM工具类产品类似，无论是应用监控还是前端监控等功能，ARMS采用的是按探针数量付费的收费模式，占用户总体预算的较大比例。但从整体来看，ARMS收费远低于业界平均水平，仅占业界水平的10%~20%左右，这得益于其优秀的高性能和高效率架构。

而链路追踪专注于解决分布式环境下的链路诊断问题，其功能相对专注，产品精简，按请求数计费，价格低廉。

## 更多信息

虽然两个产品定位不同，但都同样定位于阿里云上的开发者工具监控类产品，两款产品未来会进行互通：

-   ARMS将支持链路追踪的SDK方式进行分布式链路追踪的定制化。
-   链路追踪将会在ARMS的控制台中进行查询，优化用户诊断体验。

**相关文档**  


[链路追踪Tracing Analysis](https://www.aliyun.com/product/xtrace)

[链路追踪Tracing Analysis](https://www.alibabacloud.com/zh/products/tracing-analysis)

