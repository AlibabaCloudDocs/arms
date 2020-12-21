# Install the ARMS agent for a Java application deployed in a Docker cluster

After you install the Application Real-Time Monitoring Service \(ARMS\) agent for a Java application that is deployed in a Docker cluster, ARMS starts to monitor the Java application. ARMS automatically adapts to the environment where the application runs. You do not need to set up the runtime environment for Tomcat, Jetty, or Spring Boot applications. This topic describes how to install the ARMS agent for a Java application that is deployed in a Docker cluster.

-   ARMS is activated. For more information, see [Activate and upgrade ARMS](/intl.en-US/Quick start/Activate and upgrade ARMS.md).
-   A Java application is deployed in a Docker cluster.

ARMS Application Monitoring allows you to monitor Java applications by using the \{original-docker-image:tag\} image. To do so, edit the Dockerfile file to integrate an existing image. Then, build and start a new image.

## Step 1: Obtain the license key

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

2.  On the Applications page, click **Add Application** in the upper-right corner.

3.  Copy the license key at the top of the **Add Application** page.

    ![License key for Application Monitoring](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8283548061/p132858.png)


## Step 2: Integrate an existing image

Edit the Dockerfile file to integrate the \{original-docker-image:tag\} image, as shown in the following example.

```
###################################
##                              ###
##      ARMS APM DEMO Docker    ###
##          For Java            ###
##      withAgent   V0.1        ###
##                              ###
###################################
# Replace {original-docker-image:tag} with your own image address.
FROM {original-docker-image:tag}
WORKDIR /root/
# Replace the link for downloading the ARMS agent based on your region.
RUN wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
RUN unzip ArmsAgent.zip -d /root/
# Obtain the license key, as shown in Step 1.
# {AppName} is the name of the application that is monitored by ARMS. The application name cannot contain Chinese characters.
# If all images are connected to the same application monitoring job, you only need to specify the arms_licenseKey and arms_appName parameters.
# To connect the image to another application monitoring job, run the docker run command and use the -e parameter to specify the arms_licenseKey and arms_appName parameters. This overwrites the configurations in the Dockerfile file.
ENV arms_licenseKey={LicenseKey}
ENV arms_appName={AppName}
ENV JAVA_TOOL_OPTIONS ${JAVA_TOOL_OPTIONS} '-javaagent:/root/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey='${arms_licenseKey}' -Darms.appName='${arms_appName}
### for check the args
RUN env | grep JAVA_TOOL_OPTIONS
### Add custom Dockerfile logic.
### ......
```

Replace the example values in the preceding configuration file based on the following instructions.

-   Replace `{original-docker-image:tag}` with your own image address. If you do not have a custom image, use a system image instead.
-   Replace the link for downloading the ARMS agent based on your region.
-   Replace `{LicenseKey}` with your license key. Replace `{AppName}` with the name of your application. The application name cannot contain Chinese characters.

## Step 3: Build and start a new image

1.  Run the `docker build` command to build an image.

    ```
    docker build -t registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1 -f /{workspace}/Dockerfile /{workspace}/
    ```

    **Note:** Replace `registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1` with the actual image name.

2.  Run the `docker run` command to start the image. To connect the image to another application monitoring job, run the docker run command and use the -e parameter to specify the arms\_licenseKey and arms\_appName parameters. This overwrites the configurations in the Dockerfile file.

    ```
    docker run -d -e "arms_licenseKey={LicenseKey}" -e "arms_appName={AppName}" -p 8081:8080 registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1
    ```

    **Note:** Replace `{LicenseKey}` with your license key. Replace `{AppName}` with the name of your application. The application name cannot contain Chinese characters. Replace `registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1` with the actual image name.


## Verify the result

After about 1 minute, if your application is displayed in the application list and some data records are sent, it indicates that your application is monitored by ARMS.

## Uninstall the ARMS agent

If you no longer need to monitor the Java application in the Docker cluster, perform the following steps to uninstall the ARMS agent.

1.  Delete the configurations that you added to the Dockerfile file in [Step 2: Integrate an existing image](#section_trt_vzp_n2b).

2.  Run the `docker build` command to build an image.

3.  Run the `docker run` command to start the image.


**Related topics**  


[FAQ](/intl.en-US/Application monitoring/Application monitoring FAQ.md)

