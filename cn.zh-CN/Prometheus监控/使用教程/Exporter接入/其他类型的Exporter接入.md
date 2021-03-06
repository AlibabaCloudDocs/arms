# 其他类型的Exporter接入

阿里云Prometheus监控提供一键安装和配置数据库类型、消息类型、HTTP服务器类型以及其他类型Exporter的功能，并提供开箱即用的专属监控大盘。

阿里云Prometheus将陆续支持其他各种类型的Exporter的一键接入功能，如您所需的Exporter还未支持，请先使用手动方式安装Exporter、配置服务发现并创建大盘。本文MySQL为例，演示其他阿里云Prometheus暂未支持的开源Exporter的接入操作。

Prometheus Exporter列表请参见[Exporters and integrations](https://prometheus.io/docs/instrumenting/exporters/)。

## 前提条件

-   已创建阿里云容器服务K8s集群。具体操作，请参见[创建Kubernetes专有版集群](/cn.zh-CN/Kubernetes集群用户指南/集群/创建集群/创建Kubernetes专有版集群.md)。
-   阿里云容器服务K8s集群已接入阿里云Prometheus监控。具体操作，请参见[容器服务Kubernetes版集群]()。

## 操作流程

通过阿里云Prometheus手动监控MySQL的操作流程如下图所示。

![How It Works](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6467545161/p149087.png)

## 步骤一：部署应用

将Prometheus官方提供的mysqld-exporter镜像部署至容器服务K8s集群，以便抓取MySQL数据。操作步骤如下：

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

2.  在左侧导航栏，选择**集群**。

3.  在集群列表页面，找到目标集群，在其右侧**操作**列单击**应用管理**。

4.  创建容器组。

    1.  在左侧导航栏，选择**工作负载** \> **无状态**。

    2.  在**无状态**页面，单击**使用YAML创建资源**。

    3.  在**创建**页面的**模板**代码框输入以下内容，然后单击**创建**。

        **说明：** 请将<yourMySQLUsername\>、<yourMySQLPassword\>、<IP\>、<port\>替换为MySQL的对应值。

        ```
        apiVersion: apps/v1 # for versions before 1.8.0 use apps/v1beta1
        kind: Deployment
        metadata:
          name: mysqld-exporter
          labels:
            app: mysqld-exporter
        spec:
          replicas: 1
          selector:
            matchLabels:
              app: mysqld-exporter
          template:
            metadata:
              labels:
                app: mysqld-exporter
            spec:
              containers:
              - name: mysqld-exporter
                imagePullPolicy: Always
                env:
                  - name: DATA_SOURCE_NAME
                    value: "<yourMySQLUsername>:<yourMySQLPassword>@(<IP>:<port>)/"
                image: prom/mysqld-exporter
                ports:
                - containerPort: 9104
                  name: mysqld-exporter
        ```

    **无状态**页面显示创建的容器组。

    ![mysqld-exporter应用](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6467545161/p248753.png)

5.  创建服务。

    1.  在左侧导航栏，选择**服务与路由** \> **服务**。

    2.  在**服务**页面，单击**使用YAML创建资源**。

    3.  在**创建**页面的**模板**代码框输入以下内容，然后单击**创建**。

        ```
        apiVersion: v1
        kind: Service
        metadata:
          labels:
            app: mysqld-exporter
          name: mysqld-exporter
        spec:
          ports:
          - name: mysqld-exporter
            port: 9104
            protocol: TCP
            targetPort: 9104
          type: NodePort
          selector:
            app: mysqld-exporter
        ```

    **服务**页面显示创建的服务。

    ![mysqld-exporter服务](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6467545161/p248756.png)


## 步骤二：配置服务发现

配置阿里云Prometheus监控的服务发现以接收MySQL数据的操作步骤如下：

**说明：** 请确认阿里云容器服务K8s集群已接入Prometheus监控。具体操作，请参见[容器服务Kubernetes版集群]()。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择K8s集群所在的地域，并在目标集群右侧的**操作**列单击**设置**。

4.  在设置页面，单击**服务发现**页签，在**服务发现**页签下，单击**ServiceMonitor**页签。

5.  在**ServiceMonitor**页签下，单击**添加ServiceMonitor**。

6.  在**添加ServiceMonitor**对话框中输入以下内容，然后单击**确定**。

    ```
    apiVersion: monitoring.coreos.com/v1
    kind: ServiceMonitor
    metadata:
      labels:
        app: mysqld-exporter
        release: p
      # 填写一个唯一名称
      name: mysqld-exporter
      # 填写目标命名空间
      namespace: default
    spec:
      endpoints:
      - interval: 30s
        # Mysqld Grafana模版ID为7362
        # 填写service.yaml中Prometheus Exporter对应的Port的Name字段的值
        port: mysqld-exporter
        # 填写Prometheus Exporter代码中暴露的地址
        path: /metrics
      namespaceSelector:
        any: true
        # Demo的命名空间
        matchLabels:
          app: mysqld-exporter
    ```

    **ServiceMonitor**页签下显示配置的服务发现。

    ![mysqld-exporter-ServiceMonitor](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6467545161/p248763.png)


## 步骤三：配置大盘

配置Grafana大盘以展示数据的操作步骤如下：

1.  打开[Grafana大盘概览页](http://g.console.aliyun.com/)。

2.  在左侧导航栏选择**+** \> **Import**。

3.  在Import页面的**Import via grafna.com**文本框，输入Prometheus提供的MySQL大盘模板的ID7362，然后在其右侧单击**Load**。

    ![Import Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6316294161/p61709.png)

4.  在Import页面设置以下信息，然后单击**Import**。

    ![Import Grafana Dashboard with Options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8592975161/p62645.png)

    1.  在**Name**文本框中输入自定义的大盘名称。

    2.  在**Folder**下拉列表中选择您的阿里云容器服务K8s集群。

    3.  在**prometheus**下拉列表中选择您的阿里云容器服务K8s集群。

    配置完毕后的Grafana大盘如图所示。

    ![ARMS Prometheus Grafana MySQL](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1208873161/p62727.png)


## 步骤四：创建Prometheus监控报警

为监控指标创建报警的操作步骤如下：

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，选择**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择K8s集群所在的地域，单击目标K8s集群的名称。

4.  在左侧导航栏，选择**报警配置**。

5.  在报警配置页面右上角，单击**创建报警**。

6.  在**创建报警**面板，执行以下操作：

    1.  从**告警模板**下拉列表，选择模板。

    2.  在**规则名称**文本框，输入规则名称，例如：网络接收压力报警。

    3.  在**告警表达式**文本框，输入告警表达式。例如：`(sum(rate(kube_state_metrics_list_total{job="kube-state-metrics",result="error"}[5m])) / sum(rate(kube_state_metrics_list_total{job="kube-state-metrics"}[5m]))) > 0.01`。

        **说明：** PromQL语句中包含的`$`符号会导致报错，您需要删除包含$符号的语句中`=`左右两边的参数及`=`。例如：将`sum (rate (container_network_receive_bytes_total{instance=~"^$HostIp.*"}[1m]))`修改为`sum (rate (container_network_receive_bytes_total[1m]))`。

    4.  在**持续时间**文本框，输入时间，例如：1分钟，当告警条件连续1分组都满足时才会发送告警。

    5.  在**告警消息**文本框，输入告警消息。

    6.  在**高级配置**的**标签**区域，单击**创建标签**可以设置报警标签，设置的标签可用作分派规则的选项。

    7.  在**高级配置**的**注释**区域，单击**创建注释**，设置键为message，设置值为\{\{变量名\}\}告警信息。设置完成后的格式为：`message:{{变量名}}告警信息`，例如：`message:{{$labels.pod_name}}重启`。

        您可以自定义变量名，也可以选择已有的标签作为变量名。已有的标签包括：

        -   报警规则表达式指标中携带的标签。
        -   通过报警规则创建的标签，请参见[创建报警]()。
        -   ARMS系统自带的默认标签，默认标签说明如下。

            |标签|说明|
            |--|--|
            |alertname|告警名称，格式为：告警名称\_集群名称。|
            |\_aliyun\_arms\_alert\_level|告警等级。|
            |\_aliyun\_arms\_alert\_type|告警类型。|
            |\_aliyun\_arms\_alert\_rule\_id|告警规则对应的ID。|
            |\_aliyun\_arms\_region\_id|地域ID。|
            |\_aliyun\_arms\_userid|用户ID。|
            |\_aliyun\_arms\_involvedObject\_type|关联对象子类型，如ManagedKubernetes，ServerlessKubernetes。|
            |\_aliyun\_arms\_involvedObject\_kind|关联对象分类，如app，cluster。|
            |\_aliyun\_arms\_involvedObject\_id|关联对象ID。|
            |\_aliyun\_arms\_involvedObject\_name|关联对象名称。|

    8.  从**通知策略**下拉列表，选择通知策略。

        如何创建通知策略，请参见[设置报警通知策略]()。

    9.  单击**确定**。

    报警配置页面显示创建的报警。

    ![8](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0242584161/p245624.png)


