# 通过ServiceMonitor创建服务发现

阿里云Prometheus支持使用CRD ServiceMonitor的方式来满足您自定义服务发现的采集需求。通过使用ServiceMonitor，您可以自行定义Pod发现的Namespace范围以及通过`matchLabel`来选择监听的Service。本文将基于SpringBoot框架演示如何通过ServiceMonitor创建服务发现。

## Demo

您可以通过下载[Demo工程](https://github.com/Zheaoli/micrometer-prometheus-demo)，同步体验通过ServiceMonitor创建服务发现的完整过程。

## 步骤一：创建基础代码依赖

1.  创建一个Maven应用，并在pom.xml文件中添加以下依赖。

    ```
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-actuator</artifactId>
            </dependency>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-web</artifactId>
            </dependency>
            <dependency>
                <groupId>io.micrometer</groupId>
                <artifactId>micrometer-registry-prometheus</artifactId>
                <version>1.6.6</version>
            </dependency>
    
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-configuration-processor</artifactId>
                <optional>true</optional>
            </dependency>
            <dependency>
                <groupId>org.projectlombok</groupId>
                <artifactId>lombok</artifactId>
                <optional>true</optional>
            </dependency>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-test</artifactId>
                <scope>test</scope>
            </dependency>
        </dependencies>
    ```

2.  在项目的src/resources/applications.properties文件中添加以下配置。

    ```
    management.endpoints.web.exposure.include=prometheus
    ```

3.  启动项目，通过浏览器访问`http://{host}:{port}/actuator/prometheus`。

    获取到对应的JVM监控，返回示例如下：

    ![ServiceMonitor返回示例](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5039113261/p280930.png)


## 步骤二：部署Kubernetes集群

1.  构建一个镜像，并将构建镜像的Dockerfile文件上传至镜像仓库。

2.  参考以下内容创建Deployment。

    ```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: micrometer-prometheus
      namespace: default
      labels:
        app: demo-prometheus
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: demo-prometheus
      template:
        metadata:
          labels:
            app: demo-prometheus
        spec:
          containers:
            - name: micrometer-prometheus
              image: manjusakalza/micrometer-prometheus:latest
              ports:
                - containerPort: 8080
    ```

3.  参考以下内容创建Service。

    ```
    apiVersion: v1
    kind: Service
    metadata:
      name: prometheus-metrics-demo
      namespace: default
      labels:
        micrometer-prometheus-discovery: 'true'
    spec:
      selector:
        app: demo-prometheus
      ports:
        - protocol: TCP
          port: 8080
          targetPort: 8080
          name: metrics
    ```


## 步骤三：创建ServiceMonitor

ServiceMonitor的YAML文件示例如下：

```
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: micrometer-demo
  namespace: default
spec:
  endpoints:
    - interval: 15s
      path: /actuator/prometheus
      port: metrics
  namespaceSelector:
    any: true
  selector:
    matchLabels:
      micrometer-prometheus-discovery: 'true'
      app: tomcat
```

在这段YAML文件中，各代码段的含义如下：

-   `metadata`下的`name`和`namespace`将指定ServiceMonitor所需的一些关键元信息。
-   `spec`的`endpoints`为服务端点，代表Prometheus所需的采集Metrics的地址。`endpoints`为一个数组，同时可以创建多个`endpoints`。每个`endpoints`包含三个字段，每个字段的含义如下：
    -   `interval`：指定Prometheus对当前`endpoints`采集的周期。单位为秒，在本次示例中设定为`15s`。
    -   `path`：指定Prometheus的采集路径。在本次示例中，指定为`/actuator/prometheus`。
    -   `port`：指定采集数据需要通过的端口，设置的端口为[步骤二](#section_g7o_4zu_k4w)创建Service时端口所设置的`name`。在本次示例中，设定为`metrics`。
-   `spec`的`namespaceSelector`为需要发现的Service的范围。`namespaceSelector`包含两个互斥字段，字段的含义如下：
    -   `any`：有且仅有一个值`true`，当该字段被设置时，将监听所有符合Selector过滤条件的Service的变动。
    -   `matchNames`：数组值，指定需要监听的`namespace`的范围。例如，只想监听default和arms-prom两个命名空间中的Service，那么`matchNames`设置如下：

        ```
        namespaceSelector:
          matchNames:
          - default
          - arms-prom
        ```

-   `spec`的`selector`用于选择Service。更多信息，请参见[labelselector-v1-meta](https://v1-17.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.17/#labelselector-v1-meta)。

    在本次示例所使用的Service有micrometer-prometheus-discovery: 'true' Label，所以`selector`设置如下：

    ```
    selector:
      matchLabels:
        micrometer-prometheus-discovery: 'true'
    ```


阿里云Prometheus可以通过以下两种方式创建ServiceMonitor，请选择其中一种方式创建。

**通过控制台创建ServiceMonitor**

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**Prometheus监控**。

3.  在顶部菜单栏，选择地域。

4.  在**Prometheus监控**页面，单击目标Kubernetes集群名称。

5.  在左侧导航栏，单击**设置**。

6.  在右侧页面，单击**服务发现**页签。

7.  在**服务发现**页签，单击**ServiceMonitor**页签，然后单击**添加ServiceMonitor**。

8.  在**添加ServiceMonitor**对话框，输入YAML文件内容，然后单击**确定**。


**通过命令创建ServiceMonitor**

1.  将写好的YAML文件保存至本地。

2.  执行以下命令使YAML文件生效。

    ```
    kubectl apply -f {YAML文件所在的路径}
    ```


## 步骤四：验证ServiceMonitor

通过以下操作，验证Prometheus是否成功进行服务发现。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**Prometheus监控**。

3.  在顶部菜单栏，选择地域。

4.  在**Prometheus监控**页面，单击目标Kubernetes集群名称。

5.  在左侧导航栏，单击**设置**。

6.  在右侧页面，单击**Targets（beta）**页签。

    在**Targets（beta）**页签，查看是否存在名称为\{namespace\}/\{serviceMonitorName\}/x的Target。

    ![ServiceMonitor在Target页签显示](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6039113261/p281054.png)

7.  单击\{namespace\}/\{serviceMonitorName\}/x所在行展开Target，然后单击Endpoint链接。

    验证Metrics是否正常。

    ![ServiceMonitor的Target的endpoint](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6039113261/p281057.png)


**相关文档**  


[通过阿里云Prometheus自定义Grafana大盘]()

[创建报警]()

