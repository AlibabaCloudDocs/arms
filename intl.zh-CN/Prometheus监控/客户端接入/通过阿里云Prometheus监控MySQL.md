# 通过阿里云Prometheus监控MySQL

使用阿里云Prometheus监控抓取MySQL数据，并借助Prometheus Grafana大盘来展示MySQL数据，即可实现通过Prometheus监控MySQL的目的。

-   [快速创建Kubernetes托管版集群](/intl.zh-CN/快速入门/基础入门/快速创建Kubernetes托管版集群.md)
-   [使用私有镜像仓库创建应用](/intl.zh-CN/快速入门/高阶入门/使用私有镜像仓库创建应用.md)

本教程的操作流程如图所示。

![How It Works](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4268762161/p149087.png)

## 步骤一：通过外部应用抓取MySQL数据

将Prometheus官方提供的mysqld-exporter镜像部署至容器服务K8s集群，以便抓取MySQL数据。

1.  登录[容器服务Kubernetes版控制台](https://cs.console.aliyun.com/#/k8s/overview)。

2.  在左侧导航栏选择**集群**，在集群列表页面上的目标集群右侧**操作**列单击**应用管理**。

    ![K8s Cluster Console Button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1230633061/p61754.png)

3.  在**工作负载**页面单击**无状态**页签，在**无状态**页签中，单击**使用模板创建**。

4.  在**使用模板创建**页签中，选择示例模板为自定义，并在文本框中填写以下内容，然后单击**创建**，将mysqld-exporter应用部署至容器服务K8s集群中。

    **说明：** 请将<yourMySQLUsername\>、<yourMySQLPassword\>、<IP\>、<port\>替换为MySQL的对应值。

    ```
    apiVersion: extensions/v1beta1
    kind: Deployment
    metadata:
      name: mysqld-exporter
    spec:
      replicas: 1
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

5.  在左侧导航栏选择**服务**，在页面右上角单击**使用YAML创建资源**。

6.  在**工作负载**对应页签中填写以下内容，然后单击**创建**。

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


## 步骤二：配置Prometheus监控以接收MySQL数据

1.  登录[容器服务Kubernetes版控制台](https://cs.console.aliyun.com/#/k8s/overview)。

2.  为目标容器服务K8s集群开启阿里云Prometheus监控。具体操作，请参见[开始使用Prometheus监控]()。

3.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

4.  在左侧导航栏单击**Prometheus监控**。

5.  在**Prometheus监控**页面左上角选择容器服务K8s集群所在的地域，并在目标集群右侧的**操作**列单击**设置**。

6.  在**设置**页面单击**服务发现**页签，在**服务发现**页签上单击**添加ServiceMonitor**，在**添加ServiceMonitor**对话框中填写以下内容，然后单击**确定**。

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
        # Demo的命名空间selector:
        matchLabels:
          app: mysqld-exporter
    ```


## 步骤三：通过Grafana大盘展示MySQL数据

最后需要在Prometheus控制台导入Grafana大盘模板并指定Prometheus数据源所在的容器服务K8s集群。

1.  打开[Prometheus Grafana大盘概览页](http://g.console.aliyun.com/)。

2.  在左侧导航栏中选择**+** \> **Import**，并在**Grafana.com Dashboard**文本框输入7362，然后单击**Load**。

    ![Import Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6247219951/p61709.png)

3.  在Import页面输入以下信息，然后单击**Import**。

    ![Import Grafana Dashboard with Options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8776498951/p62645.png)

    1.  在**Name**文本框中输入自定义的大盘名称。

    2.  在**Folder**下拉框中选择您的阿里云容器服务K8s集群。

    3.  在**prometheus**下拉框中选择您的阿里云容器服务K8s集群。

    配置完毕后的Prometheus Grafana MySQL大盘如图所示。

    ![ARMS Prometheus Grafana MySQL](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9776498951/p62727.png)


## 步骤四：创建Prometheus监控报警

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在顶部菜单栏选择目标地域，然后单击目标K8s集群名称。

4.  在左侧导航栏中选择**报警配置Beta**，然后在右上角单击**创建报警**。

5.  在**创建报警**对话框中输入以下信息，完成后单击**确认**。

    **说明：** **时间**设置功能暂不支持。

    1.  填写**规则名称**，例如：网络接收压力报警。

    2.  输入报警规则表达式，表达式需要使用PromQL语句。例如：`(sum(rate(kube_state_metrics_list_total{job="kube-state-metrics",result="error"}[5m])) / sum(rate(kube_state_metrics_list_total{job="kube-state-metrics"}[5m]))) > 0.01`。

        **说明：** PromQL语句中包含的`$`符号会导致报错，您需要删除包含$符号的语句中`=`左右两边的参数及`=`。例如：将`sum (rate (container_network_receive_bytes_total{instance=~"^$HostIp.*"}[1m]))`修改为`sum (rate (container_network_receive_bytes_total[1m]))`。

    3.  在标签区域单击**创建标签**可以设置报警标签，设置的标签可用作分派规则的选项。

    4.  在注释区域可以编辑告警信息发送模板。单击**创建注释**，设置键为message，设置值为\{\{变量名\}\}告警信息。设置完成后的格式为：message:\{\{变量名\}\}告警信息，例如：message:\{\{$labels.pod\_name\}\}重启。

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

    ![Prometheus-Create alarm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5347955061/p182018.png)


Prometheus Grafana MySQL大盘配置完毕后，您可以查看Prometheus监控指标和进一步自定义大盘，详见相关文档。

[查看Prometheus监控指标]()

[通过阿里云Prometheus自定义Grafana大盘]()

[创建报警](/intl.zh-CN/大盘和报警/创建报警.md)

