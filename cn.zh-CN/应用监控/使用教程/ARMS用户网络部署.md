# ARMS用户网络部署

本文介绍如何通过Gateway组件将用户网络中的应用接入公有云ARMS应用监控服务中。

## 使用场景

Gateway组件主要解决混合云场景下，由于网络不通原因，导致应用无法接入公有云ARMS应用监控服务问题，将其部署在阿里云环境（经典网络或VPC网络）充当代理角色。

## 部署原理

![ARMS部署图](../images/p188912.png "ARMS部署图")

1.  部署在DMZ中的ARMS Gateway集群A对阿里云专有云和用户网络暴露内网地址，部署在专有云中的ARMS探针和WebLogic上的ARMS探针把采集的监控数据发送到Gateway上。
2.  DMZ通过专线和阿里云公有云打通，部署在公有云VPC内的ARMS Gateway集群B通过专线连接Gateway集群A，起桥接作用。
3.  ARMS Gateway集群B把收集到的ARMS监控数据发送到公有云服务端。
4.  阿里云公有云上的ARMS探针，包括部署在页面上的前端探针，将数据发送到ARMS公有云服务端。

## ARMS混合云监控部署要求

-   按照采集专有云和用户网络500个节点来规划，需要6台规格为2核8 G的虚拟机，部署2个包含3台Gateway组件的集群。
-   Gateway向阿里公有云传输的监控数据量比较小，可以控制在1 M/s内，所以利用现有的专线带宽，专有云EDAS和WebLogic都可以通过安装ARMS探针开启应用监控，无需修改代码。

## 安装ARMS

1.  下载[Gateway软件包](https://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-gateway-1.7.0.jar)，此处以杭州地域为例。
2.  将Gateway部署在代理机器上，通过如下命令启动。

    ```
    java -jar arms-gateway-1.7.0.jar
    ```

    **说明：** JDK版本需要为JDK 1.7+。

    Gateway默认连接杭州地域的ARMS服务，如需连接其它地域，可通过-D参数修改地域，命令如下：

    ```
    java -jar -Darms.server.endpoint=arms-dc-bj.aliyuncs.com arms-gateway-1.7.0.jar
    ```

    -   华东1（杭州）：arms-dc-hz.aliyuncs.com
    -   华北2（北京）：arms-dc-bj.aliyuncs.com
    -   华东2（上海）：arms-dc-sh.aliyuncs.com
    -   华北1（青岛）：arms-dc-qd.aliyuncs.com
    -   华南1（深圳）：arms-dc-sz.aliyuncs.com
3.  下载Agent。

    可以在[ARMS控制台](https://arms.console.aliyun.com/#/home)的接入应用页面下载，具体操作，请参见[为Java应用手动安装Agent](/cn.zh-CN/应用监控/接入应用监控/开始监控Java应用/为Java应用手动安装Agent.md)。

4.  解压Agent安装包。
5.  在arms-agent.config文件中，修改profiler.collector.ip指定的服务地址为代理机器地址。

    ```
    profiler.collector.ip={代理机器IP}
    ```

6.  启动应用，在[ARMS控制台](https://arms.console.aliyun.com/#/home)的**应用监控** \> **应用列表**页面查看监控数据是否正常上报，如果有数据上报，则说明接入成功。

