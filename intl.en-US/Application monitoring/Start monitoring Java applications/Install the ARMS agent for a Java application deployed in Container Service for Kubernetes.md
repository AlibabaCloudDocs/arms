# Install the ARMS agent for a Java application deployed in Container Service for Kubernetes

After you install the Application Real-Time Monitoring Service \(ARMS\) agent for a Java application that is deployed in Container Service for Kubernetes, ARMS starts to monitor the Java application. You can view the monitoring data of application topology, API requests, abnormal transactions, slow transactions, and SQL analysis. This topic describes how to install the ARMS agent for a Java application that is deployed in Container Service for Kubernetes.

-   [Create a dedicated Kubernetes cluster](/intl.en-US/User Guide for Kubernetes Clusters/Cluster management/Create Kubernetes clusters/Create a dedicated Kubernetes cluster.md)
-   [Create a namespace](/intl.en-US/User Guide for Kubernetes Clusters/Namespace management/Create a namespace.md): The namespace in this example is arms-demo.
-   If the JDK Version is 1.8.0\_25 or 1.8.0\_31, you may fail to install the arms Agent. In this case, upgrade the JDK to the latest version in 1.8.X.


## Install the ARMS application monitoring agent

Install ARMS application monitoring components ack-arms-pilot.

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  In the left-side navigation pane, choose **Market** \> **Application catalog** On the right of the page, click **ack-arms-pilot**.

3.  On the app catalog-ack-arms-pilot page, select the target cluster in the create pane, and click **create**.


## Authorize Alibaba Cloud Container Service for Kubernetes

Use the following steps to authorize Alibaba Cloud Container Service for Kubernetes to access ARMS resources.

1.  Log on to the [container service console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, choose **clusters**. On the **clusters** page, find the target cluster, and click **actions** in the **details** column.

    ![Manage Cluster](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9546658061/p53701.png)

3.  On the cluster information page of the target cluster, click the **cluster resources** tab. Click the link on the right of the **Worker RAM role**.

    ![Worker RAM Link](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2092658061/p53704.png)

4.  On the RAM roles page of the RAM console, click the policy name on the **permissions** tab.

5.  On the **policy document** tab, click **modify policy document**, add the following content to the **policy document** section, and then click **OK**.

    ```
    
            { "Action": "arms:*", "Resource": "*", "Effect": "Allow" } 
          
    ```

    ![Modify RAM Authorization](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2092658061/p53703.png)


## Enable ARMS application monitoring for Java applications

The following steps demonstrate how to enable ARMS application monitoring for a new application or an existing application.

To enable ARMS application monitoring when you create an application, perform the following steps.

1.  In the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview), choose **clusters** from the left-side navigation pane. On the **clusters** page, find the target cluster, and click **actions** in the **application management** column.

2.  On the deployments page, click **create from template** in the upper-right corner.

3.  On the create from template page, select a **sample template**, and in **template** \(YAML format\), add the following `annotations` to the spectimtemplatewithmetadata section:

    **Note:** Replace <your-deployment-name\> withyour application name.

    ```
    
            annotations: armsPilotAutoEnable: "on" armsPilotCreateAppName: "<your-deployment-name>" 
          
    ```

    ![YAML Example](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5354934061/p53707.png)

    The following YAML template shows how to create an application and enable ARMS application monitoring for the application.


To enable ARMS application monitoring for an existing application, perform the following steps.

1.  In the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview), choose **clusters** from the left-side navigation pane. On the **clusters** page, find the target cluster, and click **actions** in the **application management** column.

2.  On the stateless or stateful page, Select **More** \> **View Yaml** in the **actions** column for the target application.

    ![View YAML](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9814268061/p43106.png)

3.  In the edit YAML dialog box, add the following `annotations` to the speckettemplatewithmetadata section and then click **update**.

    **Note:** Replace <your-deployment-name\> withyour application name.

    ```
    
            annotations: armsPilotAutoEnable: "on" armsPilotCreateAppName: "<your-deployment-name>" 
          
    ```


## Execution result

On the Deployments or StatefulSets tab, **ARMS Console** appears in the **Actions** column of the application.

![ARMS Console Button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4546658061/p53712.png)

**Note:** If you cannot find **ARMS Console** in the **Actions** column, check whether you have authorized Container Service to access ARMS.

## Uninstall the ARMS agent

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  In the left-side navigation pane, click **Clusters**. On the **Clusters** page, click **Applications** in the **Actions** column corresponding to the cluster that contains the Java application from which you want to uninstall the ARMS agent.

3.  In the left-side navigation pane, select Releases.

4.  On the Helm tab, select the release name **arms-pilot** of the ARMS agent, and click **Delete** in the **Actions** column.

5.  In the Delete dialog box, click **OK**.

6.  Restart your business pod.


## Change the application name

You can change the application name without restarting the application or reinstalling the agent. For example, if you forget to change the sample name Java-Demo to a custom name, you can edit the armsPilotCreateAppName parameter in the Deployment application and then restart the pod. For more information, see [How can I change the name of a Java application that is deployed in a Container Service for Kubernetes cluster?](/intl.en-US/Application monitoring/FAQ.md)

**Related topics**  


[Create a dedicated Kubernetes cluster](/intl.en-US/User Guide for Kubernetes Clusters/Cluster management/Create Kubernetes clusters/Create a dedicated Kubernetes cluster.md)

[Create a namespace](/intl.en-US/User Guide for Kubernetes Clusters/Namespace management/Create a namespace.md)

[Install the ARMS agent for PHP applications in Container Service for Kubernetes](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for a PHP application deployed in Container Service for Kubernetes.md)

