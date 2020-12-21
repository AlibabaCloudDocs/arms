# Remote storage

Alibaba Cloud Prometheus provides the RemoteWrite feature. You can use this feature to store monitoring data of Prometheus to remote databases. This topic describes how to use the RemoteWrite feature of Prometheus to connect with open source Prometheus and provide an efficient solution to store monitoring data.

## Step 1: Configure RemoteWrite and obtain the read and write URL

1.  Select the destination region in the upper-left corner of the page. On the Prometheus Monitoring page, click **Access Prometheus monitoring**.

2.  On the Access Prometheus monitoring page, click **Remote Write Prometheus**.

3.  In Step 1 of the wizard, specify the **RemoteWrite Name** parameter and click **Next**.

4.  In Step 2, copy and save the generated value of the Prometheus Remote Write Url parameter, and then click **Next**.

5.  In Step 3, copy and save the generated value of the Prometheus Remote Read Url parameter, and then close the wizard.


## Step 2: Configure Prometheus

1.  Install Prometheus. For information about how to install Prometheus, see [Official documentation](https://prometheus.io/download/).

2.  Open the Prometheus.yaml configuration file and add the following content to the file. Replace the `remote_write` and `remote_read` URLs with the URLs that are obtained in[Step 1: Configure RemoteWrite and obtain the read and write URL](#section_fnr_zrt_2dg). Then, save the file.

    ```
    global:
    
    ```


