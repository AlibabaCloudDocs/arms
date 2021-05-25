# 通过阿里云Prometheus监控Kafka应用

通过在应用中埋点来暴露应用数据，使用阿里云Prometheus监控采集Kafka应用数据，借助Prometheus Grafana大盘来展示Kafka应用数据，并创建报警，即可实现利用Prometheus监控Kafka应用的目的。

容器服务K8s集群已接入阿里云Prometheus监控。如何接入，请参见[容器服务Kubernetes版集群]()。

## 操作流程

通过阿里云Prometheus监控Kafka应用的操作流程如下图所示。

![How It Works](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0253455161/p64446.png)

## 步骤一：配置JMX端口

在Kafka应用中启用JMX服务以获取资源信息，操作步骤如下：

1.  修改/opt/kafka/kafka\_2.11-0.8.2.1/bin/kafka-server-start.sh文件，在第一行添加`export JMX_PORT="9999"`。

2.  重启Kafka。


## 步骤二：为应用埋点

启动jmx\_exporter，让JMX信息可以直接通过HTTP方式访问，以便Prometheus监控抓取。

1.  下载[kafka.yml](https://raw.githubusercontent.com/prometheus/jmx_exporter/master/example_configs/kafka-0-8-2.yml)文件到/opt/exporter\_kafka/目录下。

2.  修改下载的/opt/exporter\_kafka/kafka-0.8.2.yml文件，在第一行添加`hostPort: localhost:9999`。

    将JMX服务运行的端口暴露给jmx\_exporter。

3.  下载jmx\_exporter的[可执行文件](https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/0.12.0/jmx_prometheus_httpserver-0.12.0-jar-with-dependencies.jar)到/opt/exporter\_kafka/目录下。

4.  执行以下命令启动jmx\_exporter。

    ```
    java -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.port=9998 -cp /opt/exporter_kafka/jmx_prometheus_httpserver-0.12.0-jar-with-dependencies.jar io.prometheus.jmx.WebServer 9997 /opt/exporter_kafka/kafka-0-8-2.yml &
    ```

    通过运行以下命令验证jmx\_exporter是否可以正常工作。

    ```
    curl http://<jmx_exporter所在机器的IP>:9997/metrics
    ```

    Kafka各指标的含义请参见[Monitoring Kafka](https://docs.confluent.io/current/kafka/monitoring.html)。


## 步骤三：配置Prometheus

配置Prometheus.yaml文件以采集Kafka数据的操作步骤如下：

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择K8s集群所在的地域，并在目标集群右侧的**操作**列单击**设置**。

4.  在设置页面，单击**Prometheus设置**页签。

5.  在Prometheus.yaml中输入以下内容，然后单击**保存**。

    ```
    global:
      scrape_interval:     15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
      evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
    scrape_configs:
      - job_name: 'kafka'
        static_configs:
        - targets: ['121.40.XX.XX:9997']
    ```


## 步骤四：配置大盘

配置Grafana大盘以展示数据的操作步骤如下：

1.  打开[Grafana大盘概览页](http://g.console.aliyun.com/)。

2.  在左侧导航栏，选择**+** \> **Import**。

3.  在Import页面的**Import via grafna.com**文本框，输入Prometheus提供的Kafka大盘模板的ID10973，然后单击**Load**。

    ![Import Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6316294161/p61709.png)

4.  在Import页面输入以下信息，然后单击**Import**。

    ![Prometheus-Kafka](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2155864161/p245115.png)

    1.  在**Name**文本框中输入自定义的大盘名称。

    2.  在**Folder**下拉框中选择您的阿里云容器服务K8s集群。

    3.  在**Select a Prometheus data source**下拉框中选择您的阿里云容器服务K8s集群。

    配置完毕后的Grafana大盘如图所示。

    ![prometheus_kafka_grafana](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3155864161/p63693.png)


## 步骤五：创建报警

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


