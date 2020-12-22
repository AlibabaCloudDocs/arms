# Use ARMS Prometheus Monitoring to monitor Go applications

Prometheus Monitoring of Application Real-Time Monitoring Service \(ARMS\) allows you to monitor the running status of Go applications deployed in Alibaba Cloud Container Service Kubernetes clusters, view various monitoring data on the dashboard, and configure monitoring jobs and alerts. This tutorial describes how to expose data by using instrumentation points in Go applications, capture data by using ARMS Prometheus Monitoring, and display data on the ARMS Prometheus Grafana dashboard, to ultimately monitor Go applications with ARMS Prometheus Monitoring.

Ensure that you have completed the following operations:

-   Download the [demo project](https://github.com/liguozhong/prometheus-arms-aliyun-go-demo)
-   [Create a managed Kubernetes cluster](/intl.en-US/Quick Start/Basic operations/Create a managed Kubernetes cluster.md)
-   [Create an application from a private image repository](/intl.en-US/Quick Start/Advanced operations/Create an application from a private image repository.md)

## Step 1: Expose application data by instrumentation points in Go applications

Use Prometheus Exporter in Go applications to expose application data.

1.  Import the monitoring package to your Go application.

    ```
    import (
        "fmt"
        "github.com/prometheus/client_golang/prometheus/promhttp"
        "net/http"
        "strconv"
    )
    ```

2.  Bind the monitoring interface to promhttp.Handler\(\).

    ```
    http.Handle(path, promhttp.Handler()) //Initializes an HTTP handler.
    ```


## Step 2: Deploy the application to the Container Service Kubernetes cluster

Deploy the application to the Container Service Kubernetes cluster so that ARMS Prometheus Monitoring can monitor and capture the application data.

1.  Run the following commands in the buildDockerImage.sh file by row:

    ```
    mvn clean install -DskipTests
    docker build -t <name of the local temporary Docker image>:<version of the local temporary Docker image> . --no-cache
    sudo docker tag <name of the local temporary Docker image>:<version of the local temporary Docker image> <registry domain name>/<namespace>/<image name>:<image version>
    sudo docker push <registry domain name>/<namespace>/<image name>:<image version>
    ```

    Example:

    ```
    mvn clean install -DskipTests
    docker build -t promethues-arms-aliyun-go-demo:v0.1 . --no-cache
    sudo docker tag promethues-arms-aliyun-go-demo:v0.1 registry.cn-hangzhou.aliyuncs.com/fuling/prometheus-arms-aliyun-go-demo-amd64:dev-v0.1
    sudo docker push registry.cn-hangzhou.aliyuncs.com/fuling/promethues-demo:v0.1
    ```

    In this step, a Docker image named promethues-arms-aliyun-go-demo is created, and the image is pushed to Alibaba Cloud Docker Registry.

2.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

3.  In the left-side navigation pane, choose **Clusters** \> **Clusters**. On the Clusters page, find the target cluster, and click **Dashboard** in the **Actions** column.

    ![Kubernetes cluster console button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61754.png)

4.  In the left-side navigation pane, choose **Workloads** \> **Deployments**. In the upper-right corner, click **CREATE**, and enter the following information in the **CREATE FROM TEXT INPUT** section:

    ```
    apiVersion: extensions/v1beta1
    kind: Deployment
    metadata:
      name: promethues-arms-aliyun-go-demo
    spec:
      replicas: 2
      template:
        metadata:
          labels:
            app: promethues-arms-aliyun-go-demo
        spec:
          containers:
          - name: promethues-arms-aliyun-go-demo
            imagePullPolicy: Always
            image: registry.cn-hangzhou.aliyuncs.com/fuling/prometheus-arms-aliyun-go-demo-amd64:dev-v0.1
            ports:
            - containerPort: 8077
              name: arms-go-demo
    ```

    In this step, the Docker image created in [1](#step_20d_hjh_aor) is deployed to the Container Service Kubernetes cluster.

5.  In the left-side navigation pane, choose **Discovery and Load Balancing** \> **Services**. In the upper-right corner, click **CREATE**, and enter the following information in the **CREATE FROM TEXT INPUT** section:

    ```
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        app: promethues-arms-aliyun-go-demo
      name: promethues-arms-aliyun-go-demo
    spec:
      ports:
      - name: arms-go-demo
        port: 8077
        protocol: TCP
        targetPort: 8077
      type: NodePort
      selector:
        app: promethues-arms-aliyun-go-demo
    ```


## Step 3: Configure ARMS Prometheus Monitoring to capture the data of Go applications

Configure ARMS Prometheus Monitoring in the ARMS console to capture the data of Go applications.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  On the top of the **Prometheus monitoring** page, select the region where the Container Service Kubernetes cluster is located. Find the target cluster, and click **Installation** in the **Actions** column.

4.  After the ARMS Prometheus agent is installed, find the target cluster, and click **Settings** in the **Actions** column.

5.  On the **Details** tab, click **Add ServiceMonitor**. In the **Add ServiceMonitor** dialog box, enter the following information:

    ```
    apiVersion: monitoring.coreos.com/v1
    kind: ServiceMonitor
    metadata:
      # Enter a unique name.
      name: promethues-arms-aliyun-go-demo
      # Enter the target namespace.
      namespace: default
    spec:
      endpoints:
      - interval: 30s
        # Enter the value of the Name field for Port of Prometheus Exporter.
        port: arms-go-demo
        # Enter the value of the Path field for Prometheus Exporter.
        path: /metrics
      namespaceSelector:
        any: true
        # The namespace of the NGINX Demo.
      selector:
        matchLabels:
          app: promethues-arms-aliyun-go-demo
    ```


## Step 4: Display the data of Go applications on the Grafana dashboard

Import the Grafana dashboard template in the ARMS console and specify the Container Service Kubernetes cluster where the Prometheus data source is located.

1.  Go to [Host Dashboard](http://grafana.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Import**, enter 6671 in the **Grafana.com Dashboard** field, and click **Load**.

    ![Import Grafana dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61709.png)

3.  On the Import page, set the following information and click **Import**.

    ![Import Grafana dashboard with options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0128468061/p63196.png)

    1.  Enter a custom dashboard name in the **Name** field.

    2.  Select your Container Service Kubernetes cluster from the **Folder** drop-down list.

    3.  Select your Container Service Kubernetes cluster from the **prometheus-apl** drop-down list.

    After the configuration is complete, the ARMS Prometheus Grafana Go dashboard appears, as shown in the following figure.

    ![ARMS Prometheus Grafana Go](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1128468061/p63054.png)


## Step 5: Create an alert

1.  You can select one of the two available methods to go to the Create Alarm page.

    -   On the [Prometheus Grafana dashboard](http://grafana.console.aliyun.com/) page of the NewDashBoard, click And jump to the Prometheus create alarm dialog box.
    -   In the left-side navigation pane of the arms console, choose **Alarm management** \> **Alert policy management** On the alert policies page. Click **Create alarms** \> **Prometheus**.
2.  In the **create alarm** dialog box, enter all required information and click **save**.

    1.  Enter an alert name, for example, Received\_Bytes.

    2.  Select the **cluster** for which you want to create an alert.

    3.  Select **type** as the **grafana**.

    4.  Select a specific **dashboard** and **chart** to be monitored.

    5.  Configure an alert rule.

        1.  Select **meet the following rules**.
        2.  Edit the alert rule. For example, an alert is triggered when the value of N is 5 and the average value of network receiving bytes \(MB\) is at least 3.

            **Note:** A Grafana chart may contain data of Curve A, Curve B, and Curve C. You can select one of them to monitor.

        3.  Edit or re-enter the PromQL statement in the **PromQL** input box.

            **Note:** An error may be reported if a PromQL statement contains a dollar sign \($\). You must delete the equal sign \(=\) and the parameters on both sides of the dollar sign \($\) from the statement that contains the dollar sign \($\). For example, to change a `folder` to a `folder`

    6.  Set Notification Mode. For example, select SMS.

    7.  Select the notification receivers. In the **all contact groups** box, click the name of a contact group. If the contact group appears in the **selected groups** box, the setting succeeds.

    ![Prometheus Monitoring Alarm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3608828061/p61774.png)


After the ARMS Prometheus Grafana Go dashboard is configured, you can view Prometheus Monitoring metrics and customize the dashboard. For more information, see the following documents.

[View the metrics of Prometheus Service]()

[Use Alibaba Cloud Prometheus to customize the Grafana dashboard]()

**Related topics**  


[What is Prometheus Service?]()

