# Use ARMS Prometheus Monitoring to customize the Grafana dashboard

Prometheus Monitoring of Application Real-Time Monitoring Service \(ARMS\) allows you to display monitoring data on the ARMS Prometheus Grafana dashboard. You can customize a Grafana dashboard or import the dashboard from the Grafana official website. This topic describes how to customize the Grafana dashboard to display monitoring data.

[Create a managed Kubernetes cluster](/intl.en-US/Quick Start/Basic operations/Create a managed Kubernetes cluster.md)

## Step 1: Deploy the application to the Container Service Kubernetes cluster

Deploy the application to the Container Service Kubernetes cluster so that ARMS Prometheus Monitoring can monitor and capture the JVM data.

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
    docker build -t promethues-demo:v0 . --no-cache
    sudo docker tag promethues-demo:v0 registry.cn-hangzhou.aliyuncs.com/fuling/promethues-demo:v0
    sudo docker push registry.cn-hangzhou.aliyuncs.com/fuling/promethues-demo:v0
    ```

    In this step, a Docker image named promethues-demo is created, and the image is pushed to Alibaba Cloud Docker Registry.

2.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

3.  In the left-side navigation pane, choose **Clusters** \> **Clusters**. On the Clusters page, find the target cluster, and click **Dashboard** in the **Actions** column.

4.  In the left-side navigation pane, choose **Workloads** \> **Deployments**. In the upper-right corner, click **CREATE**, and enter the following information in the **CREATE FROM TEXT INPUT** section:

    **Note:** In the following configuration file, the values of prometheus.io/port and prometheus.io/path are the ARMS Prometheus Monitoring port and path exposed in applications:

    ```
    apiVersion: extensions/v1beta1
    kind: Deployment
    metadata:
      name: prometheus-demo
    spec:
      replicas: 2
      template:
        metadata:
          annotations:
            prometheus.io/scrape: 'true'
            prometheus.io/path: '/prometheus-metrics'
            prometheus.io/port: '8081'
          labels:
            app: tomcat
        spec:
          containers:
          - name: tomcat
            imagePullPolicy: Always
            image: registry.cn-hangzhou.aliyuncs.com/fuling/promethues-demo:v0
            ports:
            - containerPort: 8080
              name: tomcat-normal
            - containerPort: 8081
              name: tomcat-monitor
    ```

    In this step, the promethues-demo Docker image is deployed to the Container Service Kubernetes cluster.

5.  In the left-side navigation pane, choose **Discovery and Load Balancing** \> **Services**. In the upper-right corner, click **CREATE**, and enter the following information in the **CREATE FROM TEXT INPUT** section:

    ```
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        name: tomcat
      name: tomcat
      namespace: default
    spec:
      ports:
      - name: tomcat-normal
        port: 8080
        protocol: TCP
        targetPort: 8080
      - name: tomcat-monitor
        port: 8081
        protocol: TCP
        targetPort: 8081
      type: NodePort
      selector:
        app: tomcat
    ```


## Step 2: Install the ARMS Prometheus agent for the application

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  On the top of the **Prometheus monitoring** page, select the region where the Container Service Kubernetes cluster is located. Find the target cluster, and click **Installation** in the **Actions** column.

    **Note:** If the installation fails, retry until it is successful. If the installation still fails after several attempts, contact us at our DingTalk account `23148410`.


## Step 3: Configure the data collection rule for Prometheus Monitoring to monitor the application

After the ARMS Prometheus agent is installed, it monitors CPU information, memory information, and network information by default. If you want to monitor non-default data, such as order information, you need to configure the data collection rule for Prometheus Monitoring to monitor the application.

1.  Find the target cluster, and click **Settings** in the **Actions** column.

2.  You can configure the data collection rule for Prometheus Monitoring to monitor the application in the following scenarios:

    -   To monitor the business data of applications deployed in the Kubernetes cluster, such as order information, you can click **Add ServiceMonitor** on the **Details** tab. In the **Add ServiceMonitor** dialog box, enter the following information:

        ```
        apiVersion: monitoring.coreos.com/v1
        kind: ServiceMonitor
        metadata:
          # Enter a unique name.
          name: tomcat-demo
          # Enter the target namespace.
          namespace: default
        spec:
          endpoints:
          - interval: 30s
            # Enter the value of the Name field for Port of Prometheus Exporter.
            port: tomcat-monitor
            # Enter the value of the Path field for Prometheus Exporter.
            path: /prometheus-metrics
          namespaceSelector:
            any: true
          selector:
            matchLabels:
              # Enter the label field of service.yaml to locate the target service.yaml file.
              app: tomcat
        ```

    -   To monitor business data outside the Kubernetes cluster, such as the number of Redis connections, you can click **Edit prometheus.yaml** on the **Details** tab to configure the native prometheus.yaml file. In the **Edit prometheus.yaml** dialog box, enter the following information:

        ```
        global:
          scrape_interval:     15s
          evaluation_interval: 15s
        scrape_configs:
          - job_name: 'prometheus'
            static_configs:
            - targets: ['localhost:9090']
        ```


## Step 4: Create a Grafana dashboard

1.  Go to [Host Dashboard](http://grafana.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Dashboard**, and click **Add Query** in the **New Panel** section.

3.  Select a cluster from the drop-down list next to **Query**. On the **A** collapse panel, select a monitoring metric, for example, **go\_gc\_duration\_seconds**, from the **Metrics** drop-down list.

4.  Click the chart icon on the left side of the page to select the visualization type of the dashboard, such as a chart, table, or heatmap, and configure other parameters as needed.

5.  Click the setting icon on the left side of the page and enter a chart name.

6.  Click the bell icon on the left side of the page. Click **Create Alert** in the **Alert** section to configure alerts. The subsequent alert configuration page will jump to the alert configuration page in ARMS Prometheus Monitoring.

7.  Click the save icon in the upper-right corner. In the Save As... dialog box, enter the dashboard name, select a cluster, and click **Save** to save the dashboard and chart. You can create multiple dashboards and charts as needed.


## Step 5: Debug data and monitor complex metrics

To monitor metrics that involve complex operations, debug data in ARMS Prometheus Monitoring to acquire the corresponding PromQL statement.

1.  On the **Prometheus monitoring** page, click **Settings** in the **Actions** column.

2.  Click **Data debugging**. On the Explore page of ARMS Prometheus Grafana, you can enter the PromQL statement in the **Metrics** field for debugging.

3.  After successful debugging, you can repeat the preceding steps to add more dashboards or charts. For more information, see [Step 4: Create a Grafana dashboard](#section_8t5_8w4_779).


The ARMS Prometheus Grafana dashboard after the configuration is complete is shown in the following figure.

[View the metrics of Prometheus Service]()

[Use ARMS Prometheus Monitoring to monitor JVM data]()

