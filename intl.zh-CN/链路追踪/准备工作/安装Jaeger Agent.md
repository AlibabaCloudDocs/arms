# 安装Jaeger Agent

本文介绍安装Jaeger Agent的方法。

## 步骤一：在ARMS控制台获取接入点信息

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)，在左侧导航栏单击**链路追踪** \> **集群配置**。

2.  在**集群配置**页面顶部选择地域，然后单击**接入点信息**页签，在**集群信息**区域打开**显示Token**开关。

3.  在**客户端采集工具**区域单击需要使用的链路数据采集客户端。

4.  在下方表格的**相关信息**列中，单击接入点信息末尾的复制图标。

    ![Jaeger接入点信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3069784261/p289796.png)

    **说明：** 如果应用部署于阿里云生产环境，则选择私网接入点，否则选择公网接入点。


## 步骤二：下载并启动Jaeger Agent

**ECS环境**

若您使用ECS，则可以通过如下方式启动Jaeger Agent。

1.  下载[Jaeger Agent安装包](https://github.com/jaegertracing/jaeger/tags)并完成解压。

    **说明：** 建议使用最新Jaeger Agent版本。

2.  使用以下命令行启动Jaeger Agent。

    ```
    nohup ./jaeger-agent --reporter.grpc.host-port=<endpoint> --agent.tags=<token>
    ```

    **说明：**

    -   对于Jaeger Agent v1.15.0及以下版本，请将启动命令中`--agent.tags`替换为`--jaeger.tags`。
    -   `<endpoint>`为链路追踪控制台概览页面上相应客户端和相应地域的接入点。
    -   `<token>`为[步骤一](#section_poz_e1n_cmn)中获取的接入点信息。

**Docker环境**

若您使用Docker部署，则建议使用容器方式启动Jaeger Agent，以减少您的运维成本。启动命令如下：

```
docker run \
  --rm \
  -p5775:5775/udp \
  -p6831:6831/udp \
  -p6832:6832/udp \
  -p5778:5778/tcp \
  jaegertracing/jaeger-agent:<version> \
  --reporter.grpc.host-port=<endpoint> \
  --agent.tags=<token>
```

**说明：** 在上述启动命令中：

-   对于Jaeger Agent v1.15.0及以下版本，请将启动命令中`--agent.tags`替换为`--jaeger.tags`。
-   `<version>`为Jaeger Agent版本，例如1.23。其他可用版本，请参见[Docker Hub](https://hub.docker.com/r/jaegertracing/jaeger-agent/tags?page=1&ordering=last_updated)。
-   `<endpoint>`为链路追踪控制台概览页面上相应客户端和相应地域的接入点。
-   `<token>`为[步骤一](#section_poz_e1n_cmn)中获取的接入点信息。

