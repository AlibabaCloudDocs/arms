# Install the ARMS agent for applications in Docker

After installing the Application Real-Time Monitoring Service \(ARMS\) agent, you can use it to monitor Java applications in Docker. For example, you can view the monitoring data of application topology, traces, abnormal transactions, and slow transactions, and conduct SQL analysis.

-   [Activate and upgrade ARMS](/intl.en-US/Quick start/Activate ARMS.md)
-   You have deployed Java applications in Docker.

-   [Docker](https://docs.docker.com/) is a set of platform-as-a-service \(PaaS\) products that use Linux OS-level virtualization to automatically deploy applications in packages called containers. Docker creates independent containers by using resource separation mechanisms, such as cgroups and namespace in Linux cores.
-   After you install the ARMS agent for applications in Docker, ARMS automatically adapts to the environment where these applications run. There is no need to specifically set up the runtime environment for Tomcat, Jetty, and Spring Boot applications.

## Step 1: Integrate an existing image

If there is an image \{original-docker-image:tag\} to which Java applications are deployed, integrate this image to form a new image by editing Dockerfile. Then, you can connect Java applications to ARMS application monitoring by constructing and starting the new image. The procedure is as follows:

1.  Edit Dockerfile to integrate the \{original-docker-image:tag\} image. The following is an example of Dockerfile:

    ```
    #####################################
    ##                              ###
    ##      ARMS APM DEMO Docker    ###
    ##          For Java            ###
    ##      withAgent   V0.1        ###
    ##                              ###
    ###################################
    FROM {original-docker-image:tag}
    WORKDIR /root/
    # Replace the link for downloading the ARMS agent based on your region.
    RUN wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    RUN unzip ArmsAgent.zip -d /root/
    # View the LicenseKey on the Application Monitoring page of the console.
    # AppName is the user-defined name of the application monitored by ARMS. Chinese characters currently cannot be used in application names.
    # If all images are connected to the same application monitoring job, you only need to set up the arms_licenseKey and arms_appName.
    # To connect the image to another application monitoring job, use the -e parameter in the docker run command to specify the arms_licenseKey and arms_appName parameters of the application to overwrite this configuration.
    ENV arms_licenseKey=xxx
    ENV arms_appName=xxx
    ENV JAVA_TOOL_OPTIONS ${JAVA_TOOL_OPTIONS} '-javaagent:/root/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey='${arms_licenseKey}' -Darms.appName='${arms_appName}
    ### for check the args
    RUN env | grep JAVA_TOOL_OPTIONS
    ### Now you can add your custom Dockerfile logic.
    ### ......
    ```

    1.  Replace `original-docker-image:tag` with your own image address. If you do not have a custom image, use a system image instead.
    2.  Replace the link for downloading the ARMS agent based on your region.

        ```
        # China (Hangzhou)
        wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # China (Shanghai)
        wget "http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # China (Qingdao)
        wget "http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # China (Beijing)
        wget "http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # China (Shenzhen)
        wget "http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # Singapore
        wget "http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/ArmsAgent.zip" -O ArmsAgent.zip
        # Finance Cloud
        wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/finance/ArmsAgent.zip" -O ArmsAgent.zip`
        ```

    3.  Replace `arms_licenseKey` and `arms_appName` with your LicenseKey and application name, respectively. Perform the following steps to obtain the LicenseKey:

## Step 2: Build and start a new image

1.  Run the docker build command to construct the image. The following command is an example:

    ```
    docker build -t registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1 -f /{workspace}/Dockerfile /{workspace}/
    ```

    **Note:** The image name is `registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1`. Replace it with your image name.

2.  Use the docker run command of the original image \{original-docker-image:tag\} to start the image. To connect the image to another application monitoring job, use `-e` to specify the `arms_licenseKey` and `arms_appName` of this application in the docker run command. This will overwrite the configurations in Dockerfile. The following command is an example:

    ```
    docker run -d -e "arms_licenseKey=<LicenseKey>" -e "arms_appName=<AppName>" -p 8081:8080 registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1
    ```

    **Note:**

    -   Replace `<LicenseKey>` with your LicenseKey and replace `<AppName>` with the name of your application. Application names in Chinese currently cannot be used as application names.
    -   The image name is `registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1`. Replace it with your image name.

## Verification

After about one minute, if your application is displayed in the application list and has data reported, it is connected to ARMS.

## Uninstall the ARMS Agent

1.  If you no longer need ARMS to monitor the Java application in the Docker cluster, you can delete the Dockerfile content edited in [Step 1](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for applications in Docker.md) in the "Install the ARMS agent for Java applications."

2.  Run the docker build command to construct an image.

3.  Run the docker run command to start the image.


