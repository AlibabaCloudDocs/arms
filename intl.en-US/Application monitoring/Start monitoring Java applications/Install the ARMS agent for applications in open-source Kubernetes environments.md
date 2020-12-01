# Install the ARMS agent for applications in open-source Kubernetes environments

You can use the application monitoring function of Application Real-Time Monitoring Service \(ARMS\) to monitor the topology, API requests, abnormal transactions, and slow transactions, and conduct SQL analysis of applications in open-source Kubernetes environments. This topic describes how to connect applications in open-source Kubernetes environments to ARMS application monitoring.

-   [ARMS is activated.](/intl.en-US/Quick start/Activate ARMS.md)
-   Your Kubernetes api-server version is V1.10 or later.
-   Your cluster can access the public network.

## Step 1: Install the ARMS agent

Currently, only Deployment and StatefulSet applications can access ARMS. Perform the following steps to connect Deployment applications in the open-source Kubernetes environment to ARMS application monitoring:

1.  Download the arms-pilot installation package by using either of the following two methods:

    -   Method 1: Manually download the [latest arms-pilot installation package](http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-pilot/arms-pilot-0.1.1-community.tgz).
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


## Step 2: Obtain Licensekey

## Step 3: Modify the YAML file of the application

1.  Run the following command to view the configurations of the target Deployment application:

    ```
    ### View the configuration of the specified Deployment application
    kubectl get deployment {Name of the Deployment application} -o yaml                            
    ```

    **Note:** If you do not know the `{Name of the Deployment application}`, run the following command to view all Deployment applications. Then you can find the target Deployment application in the results, and view the application configurations.

    ```
    ### View the configurations of all Deployment applications
    kubectl get deployments --all-namespace                
    ```

2.  Start editing the YAML file of the target Deployment application.

    ```
    kubectl edit deployment {the name of the Deployment application} -o yaml                        
    ```

3.  In the YAML file, append the following content to spec -\> template -\> metadata -\> labels:

    ```
    ARMSApmAppName: xxx
    ARMSApmLicenseKey: xxx                           
    ```

    **Note:**

    -   Replace `xxx` with your LicenseKey and application name respectively. Chinese characters currently cannot be used in application names.
    -   Replace `@` in the LicenseKey with `_`.
    The following is a complete YAML file for creating a Deployment application in an open-source environment and connecting the application to ARMS application monitoring.

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
        app: MySQL
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: MySQL
      template:
        metadata:
          labels:
            app: MySQL
        spec:
          containers:
            - resources:
                limits:
                  cpu: 0.5
              image: registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-demo-mysql:v0.1
              name: MySQL
              ports:
                - containerPort: 3306
                  name: MySQL
    ---
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        name: MySQL
      name: arms-demo-mysql
    spec:
      ports:
        # the port that this service should serve on
        - name: arms-mysql-svc
          port: 3306
          targetPort: 3306
      # label keys and values that must match in order to receive traffic for this service
      selector:
        app: MySQL
    ---
                            
    ```

4.  After the configuration is saved, the application is restarted automatically and the configuration is applied.

    If your application is listed on the **Application Monitoring** \> **Applications** page in the ARMS console and data is reported within two to five minutes, your application is connected to ARMS.


## Uninstall the ARMS agent

1.  If you no longer need ARMS to monitor the Java application in the open-source Kubernetes environment, you can run the following command to uninstall arms-pilot:

    ```
    helm del --purge arms-pilot
    ```

2.  Restart your business pod.


