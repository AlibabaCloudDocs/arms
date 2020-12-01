# 为开源Kubernetes环境中的应用安装探针

借助ARMS应用监控，您可以对开源Kubernetes环境的应用进行应用拓扑、接口调用、异常事务和慢事务监控、SQL分析等监控。本文将帮助您将开源Kubernetes环境中的应用接入ARMS应用监控。

-   [开通ARMS服务](/cn.zh-CN/快速入门/开通和升级ARMS.md)。
-   [安装Helm](https://helm.sh/docs/intro/install/)。
-   确保您的Kubernetes api-server组件接口版本在1.10及以上。
-   确保您的集群连通公网。
-   如果JDK版本为1.8.0\_25或者1.8.0\_31，可能会出现无法安装探针的情况，请升级至1.8.X最新版本。


## 步骤一：安装探针

ARMS应用监控目前仅支持无状态（Deployment）和有状态（StatefulSet）两种类型的应用接入。将开源Kubernetes环境中的无状态（Deployment）类型的应用接入ARMS应用监控的操作步骤如下。

1.  采用以下方法之一下载arms-pilot。

    -   方法一：手动下载[最新安装包](http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-pilot/arms-pilot-0.1.1-community.tgz)。
    -   方法二： 执行以下`Wget`命令下载arms-pilot安装包。

        ```
        wget 'http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-pilot/arms-pilot-0.1.1-community.tgz' -O arms-pilot-0.1.1.tgz                                
        ```

2.  执行以下命令解压arms-pilot安装包。

    ```
    tar zxvf arms-pilot-0.1.1.tgz                         
    ```

3.  执行以下命令安装arms-pilot。

    ```
    helm install ./arms-pilot --namespace arms-pilot-system                        
    ```


## 步骤二：获取Licensekey

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)，在左侧导航栏中选择**应用监控** \> **应用列表**。
2.  在应用列表页面顶部选择杭州地域，在右上角单击**接入应用**。

    **说明：** 开源Kubernetes环境中的应用默认接入杭州地域，因此您需在杭州地域获取以下的License Key。

3.  在接入应用页面顶部单击License Key右侧的复制图标。

    ![Section LicenseKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4166600061/p45312.png)


## 步骤三：修改应用的YAML文件

1.  执行以下命令查看目标无状态（Deployment）应用的配置。

    ```
    ### 查看指定无状态（Deployment）类型应用的配置kubectl get deployment {deployment名称} -o yaml                            
    ```

    **说明：** 若您不清楚`{deployment名称}`，请先执行以下命令查看所有无状态（Deployment）应用，在执行结果中找到目标无状态（Deployment）应用，再查看目标无状态（Deployment）应用的配置。

    ```
    ### 查看所有无状态（Deployment）类型应用的配置kubectl get deployments --all-namespace                
    ```

2.  启动编辑目标无状态（Deployment）应用的YAML文件。

    ```
    kubectl edit deployment {Deployment名称} -o yaml                        
    ```

3.  在YAML文件中的spec -\> template -\> metadata -\> labels层级下加入以下内容。

    ```
    ARMSApmAppName: xxx
    ARMSApmLicenseKey: xxx                           
    ```

    **说明：**

    -   请将`xxx`分别替换成您的LicenseKey和应用名称，应用名暂不支持中文。
    -   将LicenseKey中的符号`@`替换为符号`_`。
    在开源环境中创建一个无状态（Deployment）应用并接入ARMS应用监控的完整YAML文件如下。

    ```
    apiVersion: apps/v1beta1 # for versions before 1.8.0 use apps/v1beta1
    kind: Deployment
    metadata:
      name: arms-springboot-demo
      labels:
        app: arms-springboot-demo
    spec:
      replicas: 2
      selector:
        matchLabels:
          app: arms-springboot-demo
      template:
        metadata:
          labels:
            app: arms-springboot-demo
            ARMSApmLicenseKey: "xxx_xxx"
            ARMSApmAppName: "arms-k8s-demo"
        spec:
          containers:
            - resources:
                limits:
                  cpu: 0.5
              image: registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1
              imagePullPolicy: Always
              name: arms-springboot-demo
              env:
                - name: MYSQL_SERVICE_HOST
                  value: "arms-demo-mysql"
                - name: MYSQL_SERVICE_PORT
                  value: "3306"
    ---
    apiVersion: apps/v1beta1 # for versions before 1.8.0 use apps/v1beta1
    kind: Deployment
    metadata:
      name: arms-demo-mysql
      labels:
        app: mysql
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: mysql
      template:
        metadata:
          labels:
            app: mysql
        spec:
          containers:
            - resources:
                limits:
                  cpu: 0.5
              image: registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-demo-mysql:v0.1
              name: mysql
              ports:
                - containerPort: 3306
                  name: mysql
    ---
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        name: mysql
      name: arms-demo-mysql
    spec:
      ports:
        # the port that this service should serve on
        - name: arms-mysql-svc
          port: 3306
          targetPort: 3306
      # label keys and values that must match in order to receive traffic for this service
      selector:
        app: mysql
    ---
    ```

4.  保存配置后，应用将自动重启，以上配置生效。

    2 ~ 5分钟后，若您的应用出现在ARMS控制台的**应用监控** \> **应用列表**中且有数据上报，则说明接入成功。


## 卸载探针

1.  当您不需要再监控开源Kubernetes环境中的Java应用时，可执行以下命令卸载arms-pilot。

    ```
    helm del --purge arms-pilot
    ```

2.  重启您的业务Pod。


## 更多信息

**相关文档**  


[应用监控常见问题](/cn.zh-CN/应用监控/应用监控常见问题.md)

