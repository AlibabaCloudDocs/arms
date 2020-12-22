---
keyword: [PHP, application monitoring, Container Service]
---

# Install the ARMS agent for a PHP application deployed in Container Service for Kubernetes

After you install the Application Real-Time Monitoring Service \(ARMS\) agent for a PHP application that is deployed in Container Service for Kubernetes, ARMS starts to monitor the PHP application. You can view the monitoring data of application topology, API requests, abnormal transactions, slow transactions, and SQL analysis. This topic describes how to install the ARMS agent for a PHP application that is deployed in Container Service for Kubernetes.

## Obtain the license key

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

3.  On the Applications page, click **Add Application** in the upper-right corner.

4.  Copy the license key at the top of the **Add Application** page.

    ![Obtain the license key](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8283548061/p132858.png)


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


## Install the Hercules Deploy component to transfer the data of the PHP application

1.  Create a local YAML file, name it hercules.yaml, and then copy the following content to the YAML file:

    You must replace the value of the image parameter with one of the following addresses based on the region.

    |Region|Download URL|
    |------|------------|
    |China \(Hangzhou\)|    ```
registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |China \(Shanghai\)|    ```
registry.cn-shanghai.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |China \(Qingdao\)|    ```
registry.cn-qingdao.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |China \(Beijing\)|    ```
registry.cn-beijing.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |China \(Zhangjiakou-Beijing Winter Olympics\)|    ```
registry.cn-zhangjiakou.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |China \(Shenzhen\)|    ```
registry.cn-shenzhen.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |China \(Hong Kong\)|    ```
registry.cn-hongkong.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |Singapore \(Singapore\)|    ```
registry.ap-southeast-1.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |

2.  Run the following command to install the Hercules Deploy component:

    ```
    kubectl create -f hercules.yaml
    ```

    **Note:** If a message indicating that the namespace already exists is displayed in the command output, ignore the message.


## Enable ARMS to monitor a PHP application

1.  Log on to the [Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview). In the left-side navigation pane, click **Clusters**. On the **Clusters** page, click **Applications** in the **Actions** column of the cluster where your application is deployed.

2.  On the Deployments tab, click **Create from Template** in the upper-right corner.

3.  On the page that appears, select a template from the **Sample Template** drop-down list, and add the following `annotations` to the spec \> template \> metadata section.****

    ```
    annotations:
      armsPilotAutoEnable: "on"
      armsPilotCreateAppName: "<your-deployment-name>"
      armsAppType: PHP                                
    ```

    **Note:** Replace <your-deployment-name\> with the name of your Deployment application.

4.  \(This step is required only when you install the ARMS agent for the first time.\) In the namespace of your application, create a ConfigMap file named arms-<yourAppName\>.ini and copy the following content to the file:

    ```
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: arms-<yourAppName>.ini
      namespace: <yourAppNamespace>
    data:
      arms.ini: |
        extension=/usr/local/arms/arms-php-agent/arms-[x.y].so
        [ARMS]
        arms.enable=1
        arms.app_name=<yourAppName>
        arms.license_key=<yourLicenseKey>
        arms.agent_env=PHPK8S
        arms.network_type=tcp
        arms.tcp_host=arms-hercules-service.arms-pilot
        arms.tcp_port=11234
    ```

    **Note:**

    -   Replace <yourAppName\> with the name of your application.
    -   Replace <yourAppNamespace\> with the namespace of your application.
    -   Replace <yourLicenseKey\> with the license key that you obtained on the **Add Application** page in the ARMS console.
    -   In the `extension=/usr/local/arms/arms-php-agent/arms-[x.y].so` configuration, `[x.y]` in `arms-[x.y].so` is the version of the PHP application. The supported versions are 5.4, 5.5, 5.6, 7.0, 7.1, 7.2, and 7.3.
    -   If your container image is an Alpine Linux system, change `arms-[x.y].so` to `arms-[x.y]-alpine.so`. `[x.y]` can be 5.5, 5.6, 7.0, 7.1, 7.2, or 7.3.
    -   A ConfigMap file has a one-to-one mapping with an application. To connect to another application, create another ConfigMap file and delete the file when the application is no longer needed.
5.  Add ConfigMap of arms-<yourAppName\>.ini to the spec \> template \> spec \> containers section of the Deployment application. Set mountPath to the path of the PHP configuration file.

    ```
    volumeMounts:
    - mountPath: /etc/php/7.2/fpm/conf.d/arms.ini
      name: arms-ini
      subPath: arms.ini
    ```

    In the preceding information, `/etc/php/7.2/fpm/conf.d/` is the configuration loading directory of the PHP application. Add the following content to the spec \> template \> spec \> volumes section:

    ```
    volumes:
    - name: arms-ini
      configMap:
        name: arms-<yourAppName>.ini
    ```

    **Note:** If the PHP application does not have a configuration file path, add the content of arms-<yourAppName\>.ini to the php.ini configuration file of the application.

    Log on to the [Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview). On the Deployments or StatefulSets tab, if **ARMS Console** appears in the **Actions** column of the application, the ARMS agent is installed.

    ![ARMS Console Button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4546658061/p53712.png)

    **Note:** If you cannot find **ARMS Console** in the **Actions** column, check whether you have authorized Container Service to access ARMS.


## Uninstall the ARMS agent

1.  If you need to pause the ARMS agent, delete the ConfigMap file that you added in [Step 5](#step_ha3_6ov_alh) and deploy the application again.

2.  If you need to uninstall the ARMS agent, delete the Hercules Deploy component that you added in [Step 2](#step_y4n_031_gfg) and the ConfigMap file that you added in [Step 5](#step_ha3_6ov_alh).


## More information

If you have other questions, you can join the DingTalk Q&A group: 23328286.

