# Manage applications and tags

On the Application Settings page of an application in the Tracing Analysis console, you can manage the application and related tags. For example, you can specify whether to configure servers to be represented by server names and whether to enable data collection for the application. You can also manage custom tags for the application and delete the application.

## Background information

By default, the servers of an application are represented by IP addresses in the Tracing Analysis console. However, on the Application Settings page, you can configure servers to be represented by server names.

**Note:** The configuration applies only to data that is collected after the configuration takes effect. After you configure servers to be represented by server names, server names will be displayed to represent servers. However, IP addresses are retained in the data collected before the configuration change.

![Machine IP](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/xtrace/ex_machine_ip.png "The following figure shows that servers are represented by IP addresses.")

![Machine Name](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/xtrace/ex_machine_name.png "The following figure shows that servers are represented by server names.")

To stop billing for an application, disable data collection.

On the Application Settings page, you can specify whether to enable specific tags for an application and manage all tags that belong to your account. If you no longer need an application, you can delete the application.

## Go to the Application Settings page

To go to the Application Settings page, perform the following steps:

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **Applications**. At the top of the Applications page, select a region as required.

3.  On the Applications page, find the application that you want to manage and click **Settings** in the **Actions** column.


## Configure servers to be represented by server names

To configure the servers of an application to be represented by server names, perform the following steps:

1.  On the Application Settings page, click the **Custom Configuration** tab. By default, this tab is displayed.

2.  In the **Display Settings** section of the **Custom Configuration** tab, select Enable for the **Show Host Name** parameter.

3.  In the lower part of the page, click **Save**.


**Note:** The configuration applies only to data that is collected after the configuration takes effect. After you configure servers to be represented by server names, server names will be displayed to represent servers. However, IP addresses are retained in the data collected before the configuration change.

## Stop collecting application data

To stop billing for an application, perform the following steps:

1.  On the Application Settings page, click the **Custom Configuration** tab. By default, this tab is displayed.

2.  In the **Data Capturing Settings** section, select Disable for the **Capture Data** parameter.

3.  In the lower part of the page, click **Save**.


## Enable or disable tags for an application

To enable or disable tags for an application, perform the following steps:

1.  On the Application Settings page, click the **Labels** tab.

2.  In the **Manage Application Labels** section, select the tags that you want to enable and clear the tags that you want to disable.

3.  In the lower part of the page, click **Save**.


## Manage the tags of your account

To manage the tags of your account, such as adding tags for all applications or globally deleting a tag, perform the following steps:

1.  On the Application Settings page, click the **Labels** tab.

2.  In the **Manage Application Labels** section, click **Manage Application Labels**.

3.  In the Manage Application Labels dialog box, perform the following operations as needed:

    ![Manage Tags Dialog Box](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/xtrace/db_manage_tags_setting.png "Manage Application Labels dialog box")

    -   To create a tag, click the Plus icon and enter a tag in the field.
    -   To delete a tag, move the pointer over the tag and click the Delete icon on the left.

        **Note:** If you delete a tag in the Manage Application Labels dialog box, the tag is globally deleted.

4.  In the lower part of the dialog box, click **Determine**.


## Delete an application

To delete an application that you no longer need, perform the following steps:

1.  On the Application Settings page, click the **Delete** tab.

2.  In the **Delete Application** section, click **Delete**. The **Delete an application** message appears. Then, click **Delete**.


