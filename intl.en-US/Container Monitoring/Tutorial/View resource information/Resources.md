# Resources

This article describes the basic information of all resources in a namespace, including Service, Ingress, Pod, Deployment, StatefulSet, and DaemonSet resources.

## Go to the API Details page

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Container Monitoring**.

3.  In the top navigation bar, select the region where your instance is located.

4.  Log on to the **Container Monitoring**On the page that appears, click the name of the target Kubernetes cluster.

5.  On the overview page NamespacesIn the area, click the intersection of the target namespace and resource.

    **Note:**

    -   Click the blue area to enter all resource list.
    -   Click the red area to enter the exception resource list.
6.  Set the time period to be viewed in the time selection box in the upper right corner of the resource list page, and select the resource tab to be viewed.

    On each resource tab page, you can view the name, label, number of requests in time overture line, number of errors in time overture line, average response time in time overture line, status and other data of each resource.

    **Note:**

    -   When the number of errors is greater than 0, the timing curve of the number of errors is red.
    -   When the average response time is greater than 500 ms, the time series curve of the average response time is red.
    resource list are sorted by status by default. The Statuscolumn shows the abnormal degree of the current resource. The corresponding color is as follows:

    -   Red: Severe \(Fatal\).
    -   Blue: Normal.
    **Note:** Click to the right of the number of requests, number of errors, and average response time. ![Sort order](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0079606261/p278362.png) icons that can be sorted by number of requests, number of errors, and average response time.


## Service list

The **Service**tab shows all Service name of the resource, labels, requests in a timely manner the overture, the number of errors in a timely manner overture line, the average response time overture, state.

![Container monitoring-service list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2144706261/p254338.png)

Log on to the **Service**tab, you can perform the following operations:

-   Service can be filtered by setting resource names, statuses, and tags.
-   Click the service name to view the details of the target service and associated resources. For more information, see [Service details](/intl.en-US/Container Monitoring/Tutorial/View resource information/Service details.md).
-   hover over the time series curve of the number of requests, the number of errors, and the average response time to view the specific value of the corresponding time point.
-   Click Target Service Operationscolumn **Enable health inspection**to enable health inspection for the target service. After the monitoring inspection is turned on, click Operationscolumn **View health inspection**to view health inspection checkpoints. For more information, see [ACK service inspection]().

## Ingress list

The**Ingress** tab shows the names, tags, IP addresses, and statuses of all Ingress resources.

Log on to the **Ingress**tab, you can perform the following operations:

-   Ingress can be filtered by setting resource names, statuses, and tags.
-   Click the target Ingress Operationscolumn **Turn on cloud dialing**, you can enable cloud dialing for the target Ingress. After you turn on the cloud dial test, click Operationscolumn **View cloud dialing**to view the list of cloud dialing tasks. For more information, see [Create a task](/intl.en-US/Synthetic Monitoring/Quick start/Create a task.md).

## Pod list

The **Pod** tab page displays the names, running nodes, tags, timely overturns for requests, timely overturns for errors, timely overturns for average response time, timely overturns for average response time, status, number of restarts, and duration of all pod resources.

![Container Monitoring-Pod List](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2144706261/p273290.png)

Log on to the **Pod**tab, you can perform the following operations:

-   by setting the resource name, status, and tags may be Pod filter
-   Click the pod name to view the details of the target pod and associated resources. For more information, see [Pod details](/intl.en-US/Container Monitoring/Tutorial/View resource information/Pod details.md).
-   hover over the time series curve of the number of requests, the number of errors, and the average response time to view the specific value of the corresponding time point.
-   Click the target pod Operationscolumn **View YAML**to view the YAML file content of the target pod.

## Deployment list

The **Deployment**tab shows the names, tags, timely overturns for requests, timely overturns for errors, timely overturns for average response time, and status of all Depresources.

![Container Monitoring DepList](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2144706261/p273285.png)

Log on to the **Deployment**tab, you can perform the following operations:

-   Depcan be filtered by setting the resource name, status, and label.
-   Click the Depname to view the details of the target Depand associated resources. For more information, see [Depdetails](/intl.en-US/Container Monitoring/Tutorial/View resource information/Depdetails.md).
-   hover over the time series curve of the number of requests, the number of errors, and the average response time to view the specific value of the corresponding time point.
-   Click the target Dep Operationscolumn **Open application monitoring**, click **Confirm**, you can open application monitoring for the target Dep. After opening the application monitoring, click Operationscolumn **View application performance**to view the application performance of the deployment. For more information, see [Application overview](/intl.en-US/Application Monitoring/Console functions/Application overview.md).

## StatefulSet list

The **StatefulSet**tab shows the names, tags, timely overturns for requests, timely overturns for errors, timely overturns for average response time, and status of all StatefulSet resources.

Log on to the **StatefulSet**tab, you can perform the following operations:

-   StatefulSet can be filtered by setting the resource name, status, and label.
-   Click the StatefulSet name to view the details of the target StatefulSet and associated resources. For more information, see [StatefulSet details](/intl.en-US/Container Monitoring/Tutorial/View resource information/StatefulSet details.md).
-   hover over the time series curve of the number of requests, the number of errors, and the average response time to view the specific value of the corresponding time point.
-   Click the target StatefulSet Operationscolumn **View YAML**to view the YAML file content of the target StatefulSet.

## DaemonSet list

The **DaemonSet**tab shows the names, tags, timely overturns for requests, timely overturns for errors, timely overturns for average response time, and status of all DaemonSet resources.

![Container Monitoring-DaemonSet List](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2144706261/p273289.png)

Log on to the **DaemonSet**tab, you can perform the following operations:

-   DaemonSet can be filtered by setting the resource name, status, and label.
-   Click the DaemonSet name to view the details of the target DaemonSet and associated resources. For more information, see [DaemonSet details](/intl.en-US/Container Monitoring/Tutorial/View resource information/DaemonSet details.md).
-   hover over the time series curve of the number of requests, the number of errors, and the average response time to view the specific value of the corresponding time point.
-   Click the target DaemonSet Operationscolumn **View YAML**to view the YAML file of the target DaemonSet.

