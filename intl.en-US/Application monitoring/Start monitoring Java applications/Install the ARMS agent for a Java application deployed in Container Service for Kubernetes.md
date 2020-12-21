# Install the ARMS agent for a Java application deployed in Container Service for Kubernetes

After you install the Application Real-Time Monitoring Service \(ARMS\) agent for a Java application that is deployed in Container Service for Kubernetes, ARMS starts to monitor the Java application. You can view the monitoring data of application topology, API requests, abnormal transactions, slow transactions, and SQL analysis. This topic describes how to install the ARMS agent for a Java application that is deployed in Container Service for Kubernetes.

-   [Create a dedicated Kubernetes cluster](/intl.en-US/User Guide for Kubernetes Clusters/Cluster management/Create Kubernetes clusters/Create a dedicated Kubernetes cluster.md)
-   [Create a namespace](/intl.en-US/User Guide for Kubernetes Clusters/Namespace management/Create a namespace.md): The namespace in this example is arms-demo.

## Execution result

On the Deployments or StatefulSets tab, **ARMS Console** appears in the **Actions** column of the application.

![ARMS Console Button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4546658061/p53712.png)

**Note:** If you cannot find **ARMS Console** in the **Actions** column, check whether you have authorized Container Service to access ARMS.

## Uninstall the ARMS agent

1.  In the left-side navigation pane, click **Clusters**. On the **Clusters** page, click **Applications** in the **Actions** column corresponding to the cluster that contains the Java application from which you want to uninstall the ARMS agent.

2.  In the left-side navigation pane, select Releases.

3.  On the Helm tab, select the release name **arms-pilot** of the ARMS agent, and click **Delete** in the **Actions** column.

4.  In the Delete dialog box, click **OK**.

5.  Restart your business pod.


## Change the application name

You can change the application name without restarting the application or reinstalling the agent. For example, if you forget to change the sample name Java-Demo to a custom name, you can edit the armsPilotCreateAppName parameter in the Deployment application and then restart the pod. For more information, see [How can I change the name of a Java application that is deployed in a Container Service for Kubernetes cluster?](/intl.en-US/Application monitoring/Application monitoring FAQ.md)

**Related topics**  


[Create a dedicated Kubernetes cluster](/intl.en-US/User Guide for Kubernetes Clusters/Cluster management/Create Kubernetes clusters/Create a dedicated Kubernetes cluster.md)

[Create a namespace](/intl.en-US/User Guide for Kubernetes Clusters/Namespace management/Create a namespace.md)

[Install the ARMS agent for PHP applications in Container Service for Kubernetes](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for PHP applications in Container Service for Kubernetes.md)

