# Install the ARMS agent for Java applications in Container Service for Kubernetes

After installing the Application Real-Time Monitoring Service \(ARMS\) agent, you can use it to monitor Java applications in Container Service for Kubernetes. For example, you can view the monitoring data of application topology, API requests, abnormal transactions, and slow transactions. This topic describes how to install the ARMS agent for Java application in Container Service for Kubernetes.

-   [Create a dedicated Kubernetes cluster](/intl.en-US/User Guide for Kubernetes Clusters/Cluster management/Create Kubernetes clusters/Create a dedicated Kubernetes cluster.md)
-   [Create a namespace](/intl.en-US/User Guide for Kubernetes Clusters/Namespace management/Create a namespace.md): The namespace in this example is arms-demo.

## Uninstall the ARMS agent

If you no longer need ARMS to monitor the Java application in the Container Service Kubernetes cluster, you can uninstall the ARMS agent as follows:

1.  In the left-side navigation pane, choose **Applications** \> **Releases**.

2.  On the Releases page, click the Helm tab, and select the cluster from which the ARMS agent needs to be uninstalled in the **Cluster** list.

3.  Select the release name **arms-pilot** of the ARMS agent, and click **Delete** in the **Actions** column.

4.  In the Delete Application dialog box, click **OK**.

5.  Restart your business pod.


If you want to change the name of an application, such as if you forget to change the name of the sample application Java-Demo to a custom name, change armsPilotCreateAppName in the Deployment application and restart the pod. You can then change the application name without restarting the application or reinstalling the agent.

[Create a dedicated Kubernetes cluster](/intl.en-US/User Guide for Kubernetes Clusters/Cluster management/Create Kubernetes clusters/Create a dedicated Kubernetes cluster.md)

[Create a namespace](/intl.en-US/User Guide for Kubernetes Clusters/Namespace management/Create a namespace.md)

