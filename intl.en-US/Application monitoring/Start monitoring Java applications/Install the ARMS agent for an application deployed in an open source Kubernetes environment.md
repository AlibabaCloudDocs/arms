# Install the ARMS agent for an application deployed in an open source Kubernetes environment

You can use Application Real-Time Monitoring Service \(ARMS\) to monitor applications that are deployed in open source Kubernetes environments. ARMS allows you to monitor applications based on various performance metrics, such as topology, API requests, abnormal transactions, slow transactions, and SQL analysis. This topic describes how to enable ARMS to monitor an application that is deployed in an open source Kubernetes environment.

-   ARMS is activated. For more information, see [Activate ARMS](/intl.en-US/Quick start/Activate and upgrade ARMS.md).
-   Helm is installed. For more information, see [Installing Helm](https://helm.sh/docs/intro/install/).
-   The version of your Kubernetes api-server is V1.10 or later.
-   Your cluster is accessible over the Internet.
-   If the JDK Version is 1.8.0\_25 or 1.8.0\_31, you may fail to install the arms Agent. In this case, upgrade the JDK to the latest version in 1.8.X.


## Step 1: Install the ARMS agent

ARMS can monitor only the following two types of applications: Deployment and StatefulSet. To enable ARMS to monitor a Deployment application that is deployed in an open source Kubernetes environment, perform the following steps:

1.  Download the arms-pilot installation package by using one of the following methods:

    -   Method 1: Click [here](http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-pilot/arms-pilot-0.1.1-community.tgz) to download the latest arms-pilot installation package.
    -   Method 2: Run the following `wget` command to download the arms-pilot installation package:

        ```
        wget 'http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-pilot/arms-pilot-0.1.1-community.tgz' -O arms-pilot-0.1.1.tgz                                
        ```

2.  Run the following command to decompress the arms-pilot installation package:

    ```
    tar zxvf arms-pilot-0.1.1.tgz                         
    ```

3.  Run the following command to install arms-pilot:

    ```
    helm install ./arms-pilot --namespace arms-pilot-system                        
    ```


## Step 2: Obtain the license key

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
2.  On the Applications page, select China \(Hangzhou\) in the top navigation bar, and click **Add Application** in the upper-right corner.

    **Note:** By default, applications that are deployed in open source Kubernetes environments reside in the China \(Hangzhou\) region. Therefore, you must obtain the license key for the China \(Hangzhou\) region.

3.  Copy the license key at the top of the Add Application page.

    ![Section LicenseKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6076728061/p45312.png)


## Step 3: Edit the YAML file of the application

1.  Run the following command to view the configurations of the Deployment application:

    ```
    ### Run the following command to view the configurations of a specified Deployment application: kubectl get deployment {Name of the Deployment application} -o yaml                            
    ```

    **Note:** If you do not know the `{Name of the Deployment application}`, run the following command to view all Deployment applications. Then you can find the target Deployment application in the results, and view the application configurations.

    ```
    ### Run the following command to view the configurations of all Deployment applications: kubectl get deployments --all-namespace                
    ```

2.  Run the following command to edit the YAML file of the Deployment application:

    ```
    kubectl edit deployment {Name of the Deployment application} -o yaml                        
    ```

3.  In the YAML file, go to the spec -\> template -\> metadata -\> labels directory and append the following content:

    ```
    ARMSApmAppName: xxx
    ARMSApmLicenseKey: xxx                           
    ```

    **Note:**

    -   Replace `xxx` with your application name and license key. The application name cannot contain Chinese characters.
    -   Replace the at sign \(`@`\) in the license key with an underscore \(`_`\).
    The following example shows a complete YAML file for creating a Deployment application in an open source environment and enabling ARMS to monitor the application.

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

4.  After the preceding configurations are saved, the application automatically restarts and then the configurations take effect.

    After 2 to 5 minutes, if your application is displayed on the **Application Monitoring** \> **Applications** page in the ARMS console and some data records are sent, it indicates that your application is monitored by ARMS.


## Uninstall the ARMS agent

1.  If you no longer want to use ARMS to monitor your Java applications in an open-source Kubernetes environment, run the following command to uninstall arms-pilot:

    ```
    helm del --purge arms-pilot
    ```

2.  Restart your business pod.


**Related topics**  


[FAQ](/intl.en-US/Application monitoring/FAQ.md)

