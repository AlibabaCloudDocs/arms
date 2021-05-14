# Install the ARMS agent for an application deployed in an open source Kubernetes environment

You can use Application Real-Time Monitoring Service \(ARMS\) to monitor applications that are deployed in open source Kubernetes environments. ARMS allows you to monitor applications based on various performance metrics, such as the topology, API requests, abnormal transactions, slow transactions, and SQL analysis. This topic describes how to enable ARMS to monitor an application that is deployed in an open source Kubernetes environment.

-   ARMS is activated. For more information, see [Activate and upgrade ARMS](/intl.en-US/Quick Start/Activate and upgrade ARMS.md).
-   Helm is installed. For more information, see [Installing Helm](https://helm.sh/docs/intro/install/).
-   The version of your Kubernetes api-server is 1.10 or later.
-   Your cluster is accessible over the Internet.
-   If the JDK Version is 1.8.0\_25 or 1.8.0\_31, you may fail to install the arms Agent. In this case, upgrade the JDK version to the latest version, which is 1.8.X.




## Step 1: Install the ARMS agent

ARMS can monitor only the following two types of applications: Deployment and StatefulSet. A Deployment application that is deployed in an open source Kubernetes environment is used as an example. To enable ARMS to monitor the Deployment application, perform the following steps:

1.  Download the arms-pilot installation package by using one of the following methods:

    -   Method 1: Click [here](http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-pilot/arms-pilot-0.1.1-community.tgz) to download the arms-pilot installation package of the latest version.
    -   Method 2: Run the following `wget` command to download the arms-pilot installation package:

        ```
        wget 'http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-pilot/arms-pilot-0.1.1-community.tgz' -O arms-pilot-0.1.1.tgz                                
        ```

2.  Run the following command to decompress the arms-pilot installation package:

    ```
    tar zxvf arms-pilot-0.1.1.tgz                         
    ```

3.  Open the values.yaml file in the installation package. Change the values of the `uid` and `region_id` parameters as needed and save the edit.

    ```
    userId: __USER_ID__
    regionId: __REGION_ID__
    ```

4.  Run the following command to install arms-pilot:

    ```
    helm install ./arms-pilot --namespace arms-pilot-system                        
    ```


## Step 2: Obtain the license key

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

3.  On the Applications page, click **Add Application** in the upper-right corner.

4.  In the upper part of the Add Application page, click the copy icon to the right of the license key and save the key.

    ![Section LicenseKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6076728061/p45312.png)


## Step 3: Edit the YAML file of the application

1.  Run the following command to view the YAML file of the Deployment application:

    ```
    kubectl get deployment {Name of the Deployment application} -o yaml                            
    ```

    **Note:** If you do not know the `name of the Deployment application`, run the following command to view all Deployment applications. Then, you can find the required Deployment application in the results, and view the YAML file of the application.

    ```
    kubectl get deployments --all-namespace                
    ```

2.  Run the following command to edit the YAML file of the Deployment application:

    ```
    kubectl edit deployment {Name of the Deployment application} -o yaml                        
    ```

3.  In the YAML file, go to the spec -\> template -\> metadata -\> labels directory and append the following content:

    ```
    ARMSApmAppName: xxx
    ARMSApmLicenseKey: xxx                           
    ```

    **Note:**

    -   Replace `xxx` with your application name and license key. The application name cannot contain Chinese characters.
    -   Replace the at sign \(`@`\) in the license key with an underscore \(`_`\).
    The following example shows a complete YAML file for creating a Deployment application in an open source environment and enabling ARMS to monitor the application:

4.  After the preceding configurations are saved, the application automatically restarts and then the configurations take effect.

    After 2 to 5 minutes, if your application is displayed on the **Application Monitoring** \> **Applications** page in the ARMS console and specific data records are sent, your application is monitored by ARMS.


## Uninstall the ARMS agent

1.  If you no longer want to use ARMS to monitor your Java applications in an open-source Kubernetes environment, run the following command to uninstall arms-pilot:

    ```
    helm del --purge arms-pilot
    ```

2.  Restart your business pod.


**Related topics**  


[FAQ](/intl.en-US/Application Monitoring/FAQ.md)

