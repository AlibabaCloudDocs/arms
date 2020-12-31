# Use ARMS Prometheus Monitoring to customize Grafana dashboards

Prometheus Monitoring of Application Real-Time Monitoring Service \(ARMS\) allows you to display monitoring data on the Prometheus Grafana dashboard. You can customize a Grafana dashboard or import the dashboard from the official Grafana website. This topic describes how to customize a Grafana dashboard to display monitoring data.

[Create a managed Kubernetes cluster](/intl.en-US/Quick Start/Basic operations/Create a managed Kubernetes cluster.md)

## Step 1: Deploy an application to a Container Service for Kubernetes cluster

Deploy an application to a Container Service for Kubernetes \(ACK\) cluster so that ARMS Prometheus Monitoring can monitor and capture the JVM data.

1.  Run the following commands in the buildDockerImage.sh file by row:

    ```
    mvn clean install -DskipTests
    docker build -t <Name of the local temporary Docker image>:<Version of the local temporary Docker image> . --no-cache
    sudo docker tag <Name of the local temporary Docker image>:<Version of the local temporary Docker image> <Registry domain name>/<Namespace>/<Image name>:<Image version>
    sudo docker push <Registry domain name>/<Namespace>/<Image name>:<Image version>
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

3.  In the left-side navigation pane, click **Clusters**. On the Clusters page, click **Applications** in the **Actions** column corresponding to a cluster.

    ![K8s Cluster Console Button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9273229061/p61754.png)

4.  On the **Workloads** page, click the **Deployments** tab. On the **Deployments** tab, click **Create from Template**.

5.  On the **Create from Template** tab, select Custom from the Sample Template drop-down list, enter the following content in the Template text editor, and then click **Create** to deploy the promethues-demo image to the cluster.

    **Note:** In the following configuration file, the values of prometheus.io/port and prometheus.io/path are the Prometheus Monitoring port and path exposed in the application.

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

6.  In the left-side navigation pane, choose Services and Ingresses \> **Services**. On the Services page, click **Create Resources in YAML**.

7.  Enter the following content in the text editor and click **Create**:

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


## Step 2: Install a Prometheus agent for the application

Enable ARMS Prometheus Monitoring for the cluster where the application is deployed. For more information, see [Get started with Prometheus Service]().

## Step 3: Configure data collection rules for ARMS Prometheus Monitoring to monitor the application

By default, after the Prometheus agent is installed, the agent monitors the CPU, memory, and network information. If you want to monitor non-default data, such as order information, you must configure data collection rules for ARMS Prometheus Monitoring to monitor the application.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  On the **Prometheus Monitoring** page, click **Settings** in the **Actions** column corresponding to the cluster.

4.  Configure data collection rules for ARMS Prometheus Monitoring to monitor the application in the following scenarios:

    -   To monitor the business data of the application deployed in the cluster, such as order information, you can click **Add ServiceMonitor** on the **Service Discovery** tab. In the **Add ServiceMonitor** dialog box, reference the following content to enter the text and click **OK**:

        ```
        apiVersion: monitoring.coreos.com/v1
        kind: ServiceMonitor
        metadata:
          #  Enter a unique name.
          name: tomcat-demo
          #  Enter a namespace.
          namespace: default
        spec:
          endpoints:
          - interval: 30s
            #  Enter the value of the Name field for Port of Prometheus Exporter in the service.yaml file.
            port: tomcat-monitor
            #  Enter the value of the Path field for Prometheus Exporter.
            path: /metrics
          namespaceSelector:
            any: true
            #  The namespace of Demo.
          selector:
            matchLabels:
              # Enter the value of the Label field in the service.yaml file to find the service.yaml file.
              app: tomcat
        ```

    -   To monitor business data outside the cluster, such as the number of Redis connections, you can reference the following content to enter the text on the **Prometheus Settings** tab and click **Save**:

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

1.  Go to [Host Dashboard](http://g.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Dashboard**. Click **Add Query** in the **New Panel** section.

    ![Create Grafana DashBoard](../images/p62533.png)

3.  Select a cluster from the drop-down list next to **Query**. On the **A** collapse panel, select a metric from the **Metrics** drop-down list. Example: **go\_gc\_duration\_seconds**.

    ![Grafana Add Query](../images/p62736.png)

4.  Click the chart icon on the left side of the page to select the visualization type of the dashboard, such as a chart, table, or heatmap, and configure other parameters.

    ![Create Dashboard Visualization](../images/p62560.png)

5.  Click the setting icon on the left side of the page and enter a chart name.

    ![Set Visualization General](../images/p62566.png)

6.  Create an ARMS Prometheus Monitoring alert. For more information, see [Create an alert]().

7.  Click the save icon in the upper-right corner. In the Save As... dialog box, enter the dashboard name, select a cluster, and then click **Save** to save the dashboard and chart. Create multiple dashboards and charts to suit your needs.

    ![Save Grafana Dashboard](../images/p62581.png)


## Step 5: Debug data and monitor complex metrics

To monitor metrics that involve complex operations, debug data in ARMS Prometheus Monitoring to obtain the corresponding PromQL statement.

1.  Go to [Host Dashboard](http://g.console.aliyun.com/).

2.  In the left-side navigation pane, click **Explore**.

3.  On the Explore page, enter the PromQL statement in the **Metrics** field for debugging.

    ![Prometheus Data Debug](../images/p62734.png)

4.  After debugging is successful, repeat the preceding steps to create more dashboards or charts. For more information, see [Step 4: Create a Grafana dashboard](#section_8t5_8w4_779).


After the configuration is complete, the Prometheus Grafana dashboard appears, as shown in the following figure.

![ARMS Prometheus Grafana Dashboard to Customize](../images/p62691.png)

[View Prometheus Monitoring metrics]()

[Use ARMS Prometheus Monitoring to monitor JVM applications]()

