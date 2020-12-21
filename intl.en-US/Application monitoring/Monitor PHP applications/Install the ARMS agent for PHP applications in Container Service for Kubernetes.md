---
keyword: [PHP, Application Monitoring, Container Service]
---

# Install the ARMS agent for PHP applications in Container Service for Kubernetes

After you install the Application Real-Time Monitoring Service \(ARMS\) agent for a PHP application deployed in Container Service for Kubernetes, you can use it to monitor the PHP application. For example, you can view the monitoring data of application topology, traces, abnormal transactions, and slow transactions, and conduct SQL analysis. This topic describes how to install the ARMS agent for a PHP application in Container Service for Kubernetes.

## Install the Hercules Deploy component to report PHP application data

1.  Create a local YAML file, name it hercules.yaml, and copy the following content to the YAML file:

    You must replace the value of `image` with any of the following addresses based on the region.

    ```
    # China (Hangzhou)
    registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    # China (Shanghai)
    registry.cn-shanghai.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    # China (Qingdao)
    registry.cn-qingdao.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    # China (Beijing)
    registry.cn-beijing.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    # China (Zhangjiakou-Beijing Winter Olympics)
    registry.cn-zhangjiakou.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    # China (Shenzhen)
    registry.cn-shenzhen.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    # China (Hong Kong)
    registry.cn-hongkong.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    # Singapore (Singapore)
    registry.ap-southeast-1.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ```

2.  Run the following command to install the Hercules Deploy component:

    ```
    kubectl create -f hercules.yaml
    ```

    **Note:** If a message indicating that the namespace already exists is displayed after the command is run, skip it.


## Enable ARMS Application Monitoring for a PHP application

1.  Log on to the [Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview). In the left-side navigation pane, choose **Applications** \> **Deployments**.

2.  On the Deployments page, click **Create from Template** in the upper-right corner.

3.  On the Create from Template page, set **Cluster**, **Namespace**, and **Sample Template**, and add the following `annotations` to spec \> template \> metadata in the **Template** \(YAML file format\) field.

    ```
    annotations:
      armsPilotAutoEnable: "on"
      armsPilotCreateAppName: "<your-deployment-name>"
      armsAppType: PHP                                
    ```

    **Note:** Replace <your-deployment-name\> with your deployment name.

4.  \(Only for initial installation\) In the same namespace as your deployment, create the arms-<yourAppName\>.ini ConfigMap file and copy the following content to the file:

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

    -   Replace <yourAppName\> with your deployment name.
    -   Replace <yourAppNamespace\> with the namespace of your deployment.
    -   Replace <yourLicenseKey\> with the license key that you obtained on the Add Application page in the ARMS console.
    -   In the `extension=/usr/local/arms/arms-php-agent/arms-[x.y].so` configuration, `[x.y]` in `arms-[x.y].so` is the version of your PHP application. The supported versions are 5.4, 5.5, 5.6, 7.0, 7.1, 7.2, and 7.3.
    -   If your container image is an Alpine Linux system, change `arms-[x.y].so` to `arms-[x.y]-alpine.so`, where `[x.y]` can be 5.5, 5.6, 7.0, 7.1, 7.2, or 7.3.
    -   A ConfigMap file has a one-to-one mapping with an application. To connect to another application, create another ConfigMap file and delete the file when the application is no longer needed.
5.  Mount the arms-php.ini ConfigMap to the spec \> template \> spec \> containers section in the php.ini file. Set mountPath to the path of the php.ini file.

    ```
    volumeMounts:
    - mountPath: /etc/php/7.2/fpm/conf.d/arms.ini
      name: arms-ini
      subPath: arms.ini
    ```

    In the preceding information, `/etc/php/7.2/fpm/conf.d/` is the configuration loading directory of your PHP application. Add the following content to the spec \> template \> spec \> volumes section:

    ```
    volumes:
    - name: arms-ini
      configMap:
        name: arms-<yourAppName>.ini
    ```

    Log on to the [Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview). In the left-side navigation pane, click Deployments or StatefulSets. If **ARMS Console** appears in the **Actions** column of the target application, the ARMS agent is installed.

    ![ARMS Console button](../images/p53712.png)

    **Note:** If you cannot find **ARMS Console** in the **Actions** column, check whether you have authorized Container Service to access ARMS.


## Uninstall the ARMS agent

1.  If you need to pause the ARMS agent, delete the ConfigMap file added in [Step](#step_ha3_6ov_alh)[5](#step_ha3_6ov_alh) and redeploy the application.

2.  If you need to uninstall the ARMS agent, delete the Hercules Deploy component added in [Step](#step_y4n_031_gfg)[2](#step_y4n_031_gfg) and the ConfigMap file added in [Step](#step_ha3_6ov_alh)[5](#step_ha3_6ov_alh).


