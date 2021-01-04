# 通过阿里云Prometheus监控ZooKeeper

通过在ZooKeeper中埋点来暴露数据，使用阿里云Prometheus监控抓取数据，并借助Prometheus Grafana大盘来展示数据，即可实现通过Prometheus监控ZooKeeper的目的。

本教程的操作流程如图所示。

![How It Works](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4350633061/p64447.png)

## 步骤一：启动JMX服务

首先需要在ZooKeeper中启用JMX服务以获取资源信息。

1.  修改/opt/zk/zookeeper-3.4.10/bin/zkServer.sh，在第44行添加`JMXPORT=8999`。具体添加位置如下所示。

    ```
    if [ "x$JMXLOCALONLY" = "x" ]
    then
        JMXLOCALONLY=false
    fi
    
    JMXPORT=8999 ## 添加在此处第44行
    if [ "x$JMXDISABLE" = "x" ] || [ "$JMXDISABLE" = 'false' ]
    then
      echo "ZooKeeper JMX enabled by default $JMXPORT ..." >&2
      if [ "x$JMXPORT" = "x" ]
      then
    ```

2.  重启ZooKeeper。

    ```
    /opt/zk/zookeeper-3.4.10/bin/zkServer.sh start /opt/zk/zookeeper-3.4.10/conf/zoo_sample.cfg &
    ```


## 步骤二：在ZooKeeper中启动jmx\_exporter

其次需要启动jmx\_exporter，让JMX信息可以直接通过HTTP方式访问，以便Prometheus监控抓取。

1.  下载[zookeeper.yaml](https://raw.githubusercontent.com/prometheus/jmx_exporter/master/example_configs/zookeeper.yaml)到/opt/exporter\_zookeeper/目录下。

2.  修改下载的/opt/exporter\_zookeeper/zookeeper.yaml文件，在第一行添加`hostPort: localhost:8999`，将JMX服务运行的端口暴露给jmx\_exporter。

3.  下载jmx\_exporter的[可执行文件](https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/0.12.0/jmx_prometheus_httpserver-0.12.0-jar-with-dependencies.jar)到opt/exporter\_zookeeper/目录下。

4.  启动jmx\_exporter。

    ```
    java -Dcom.sun.management.jmxremote.ssl=false -
    Dcom.sun.management.jmxremote.authenticate=false -
    Dcom.sun.management.jmxremote.port=8998 -cp /opt/exporter_zookeeper/jmx_prometheus_httpserver-0.12.0-jar-with-dependencies.jar 
    io.prometheus.jmx.WebServer 8997 /opt/exporter_zookeeper/zookeeper_exporter.yaml &
    ```

    至此应用部分配置完成。可通过运行如下命令验证jmx\_exporter是否可以正常工作。

    ```
    curl http://<jmx_exporter所在机器的IP>:9997/metrics
    ```


## 步骤三：配置Prometheus监控以抓取ZooKeeper的数据

接下来需要在Prometheus控制台配置Prometheus监控以抓取ZooKeeper的数据。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在**Prometheus监控**页面左上角选择容器服务K8s集群所在的地域，并在目标集群右侧的**操作**列单击**设置**。

4.  在**设置**页面单击**Prometheus设置**页签。

5.  在**Prometheus设置**页签中输入以下代码，然后单击**保存**。

    ```
      global:
      scrape_interval:     15s # Set the scrape interval to every 15 seconds. 
    Default is every 1 minute.
      evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
    scrape_configs:
      - job_name: 'zookeeper'    
        static_configs:    
        - targets: ['121.40.124.46:8997']
    ```


## 步骤四：通过Grafana大盘展示ZooKeeper的数据

最后需要在Prometheus控制台导入Grafana大盘模板并指定Prometheus数据源所在的容器服务K8s集群。

1.  打开[Prometheus Grafana大盘概览页](http://g.console.aliyun.com/)。

2.  在左侧导航栏中选择**+** \> **Import**，并在**Grafana.com Dashboard**文本框输入10981，然后单击**Load**。

    ![Import Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6247219951/p61709.png)

3.  在Import页面输入以下信息，然后单击**Import**。

    ![Import Grafana Dashboard with Options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5484298951/p64454.png)

    1.  在**Name**文本框中输入自定义的大盘名称。

    2.  在**Folder**下拉框中选择您的阿里云容器服务K8s集群。

    3.  在最下方的下拉框中选择您的阿里云容器服务K8s集群。

    配置完毕后的Prometheus Grafana ZooKeeper大盘如图所示。

    ![prom-zoo gra](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5484298951/p63907.png)


## 步骤五：创建Prometheus监控报警

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

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


Prometheus Grafana ZooKeeper大盘配置完毕后，您可以查看Prometheus监控指标和进一步自定义大盘，详见相关文档。

[查看Prometheus监控指标]()

[通过阿里云Prometheus自定义Grafana大盘]()

[创建报警](/cn.zh-CN/大盘和报警/创建报警.md)

