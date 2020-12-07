# 为什么容器服务Kubernetes版集群中的Java应用安装Agent后，应用监控没有数据呢？

## Condition

阿里云容器服务Kubernetes版集群中的Java应用安装Agent后，应用监控没有数据。

## Cause

应用所在Pod未被注入arms-init-container、应用YAML文件中无Annotations注解以及STS服务未正确授权等原因都可能导致应用监控无数据。

## Remedy

1.  登录[容器服务Kubernetes版控制台](https://cs.console.aliyun.com/#/k8s/overview)。

2.  在左侧导航栏选择**集群**，在集群列表页面上的目标集群右侧**操作**列单击**应用管理**。

3.  在容器组页签顶部选择您的应用所在的命名空间，然后单击目标应用右侧单击**编辑**。

4.  在编辑YAML对话框中查看YAML文件中是否存在initContainers。

    ![db_am_ack_apppod_yaml](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5947736061/p111799.png)

    -   如果不存在，则说明未被注入arms-init-container，执行[5](#step_tph_c0c_gi0)。
    -   如果存在，则说明已被注入arms-init-container，执行[8](#step_j7i_e2c_v3r)。
5.  在容器组页签顶部选择命名空间为**arms-pilot**。查看Pod列表中是否存在名称前缀为**arms-pilot**的Pod。

    -   如果存在，则执行[6](#step_5rl_wvs_v3k)。
    -   如果不存在，则在应用市场中安装arms-pilot。具体操作，请参见[安装ARMS应用监控组件](/cn.zh-CN/应用监控/开始监控 Java 应用/为容器服务Kubernetes版Java应用安装探针.md)。
6.  在无状态或有状态页签目标应用右侧操作列中选择**更多** \> **查看Yaml**，在编辑YAML对话框查看YAML文件中是否存在以下Annotations注解。

    ```
    annotations:
      armsPilotAutoEnable: 'on'
      armsPilotCreateAppName: <your-deployment-name>
    ```

    -   如果存在，则执行[7](#step_6iy_617_3e6)。
    -   如果不存在，则在编辑YAML对话框中的spec \> template \> metadata层级下添加以上Annotations注解，并将`<your-deployment-name>`替换为您的应用名称，然后单击**更新**。
7.  在容器组页签目标应用右侧单击**日志**，查看arms-pilot的Pod日志是否报STS错误，即提示`"Message":"STS错误"`。

    -   如果报STS错误，则需为应用所在集群授权，并重启应用所在Pod。具体操作，请参见[为容器服务Kubernetes版授权](/cn.zh-CN/应用监控/开始监控 Java 应用/为容器服务Kubernetes版Java应用安装探针.md)。
    -   如果未报STS错误，则联系ARMS钉钉服务账号：arms160804。
8.  在容器组页签目标应用右侧单击**编辑**，在编辑YAML对话框中查看YAML文件中是否存在以下javaagent参数。

    ```
    -javaagent:/home/admin/.opt/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar
    ```

    -   如果存在，则单击容器组页签右侧的**终端**进入命令行页面，执行以下命令查看是否存在以.log为后缀的日志文件，然后联系ARMS钉钉服务账号：arms160804。

        ```
        cd /home/admin/.opt/ArmsAgent/logs
        ```

    -   如果不存在，则联系ARMS钉钉服务账号：arms160804。

