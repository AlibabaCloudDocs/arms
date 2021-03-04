# Why is no data displayed in Application Monitoring after the ARMS agent is installed on a Java application in a cluster of Container Service for Kubernetes \(ACK\)?

## Condition

No data is displayed in Application Monitoring after the Application Real-Time Monitoring Service \(ARMS\) agent is installed on a Java application in an ACK cluster.

## Cause

The pod of the application is not injected to arms-init-container, the YAML file of the application contains no annotations, or Security Token Service \(STS\) is not authorized.

## Remedy

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  In the left-side navigation pane, click **Clusters**. On the Clusters page, find the required cluster, and click **Applications** in the **Actions** column.

3.  In the upper part of the Pods tab, select the namespace in which your application resides. Click **Edit** next to the application.

4.  In the Edit YAML dialog box, check whether the YAML file contains initContainers.

    -   If the YAML file does not contain initContainers, the pod has not been injected to arms-init-container. Perform [5](#step_tph_c0c_gi0).
    -   If the YAML file contains initContainers, the pod has been injected to arms-init-container. Perform [8](#step_j7i_e2c_v3r).
5.  In the upper part of the Pods tab, set Namespace to **arms-pilot**. Check whether any pods that have the **arms-pilot** prefix exist in the Pod list.

    -   If any pods that have the arms-pilot prefix exist in the Pod list, perform [6](#step_5rl_wvs_v3k).
    -   Otherwise, install arms-pilot in the application market. For more information, see [Install the ARMS agent for Java applications in Container Service for Kubernetes](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Install the ARMS agent for a Java application deployed in Container Service for Kubernetes.md).
6.  On the Deployments or StatefulSets tab, choose **More** \> **View in YAML** in the Actions column. In the Edit YAML dialog box, check whether the YAML file contains the following annotations:

    ```
    annotations:
      armsPilotAutoEnable: 'on'
      armsPilotCreateAppName: <your-deployment-name>                  
    ```

    -   If the YAML file contains these annotations, perform [7](#step_6iy_617_3e6).
    -   If the YAML file does not contain these annotations, add the preceding annotations to the spec \> template \> metadata section in the Edit YAML dialog box, replace `<your-deployment-name>` with your application name, and then click **Update**.
7.  On the Pods tab, click **Logs**, next to the required pod to check whether the pod logs of arms-pilot report an STS error in the `"Message":"STS error"`format.

    -   If the pod logs of arms-pilot report an STS error, authorize the cluster of the application and restart the pod of the application. For more information, see [Install the ARMS agent for Java applications in Container Service for Kubernetes](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Install the ARMS agent for a Java application deployed in Container Service for Kubernetes.md).
    -   If the pod logs of arms-pilot do not report an STS error, contact the ARMS DingTalk account arms160804.
8.  On the Pods tab, click **Edit** next to the required pod. In the Edit YAML dialog box, check whether the YAML file contains the following javaagent parameter:

    ```
    -javaagent:/home/admin/.opt/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar
    ```

    -   If the YAML file contains the javaagent parameter, find the pod of the application on the Pods tab, and click **Terminal** next to the required pod to go to the Shell page. Run the following command to check whether any log file name is suffixed with .log, and then contact the ARMS DingTalk accoun arms160804.

        ```
        cd /home/admin/.opt/ArmsAgent/logs
        ```

    -   If the YAML file does not contain the javaagent parameter, contact the ARMS DingTalk account arms160804.

