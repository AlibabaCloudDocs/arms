# Manage apps and tags

On the Application Settings page, you can specify whether to display the machine name and collect application data. You can also manage the custom tags of applications and delete applications.

## Background

In the link Tracing Analysis console, when you need to display the IP address of the host that is deployed by application, the IP address of the host is displayed by default. However, you can select the host name on the application settings page.

**Note:** Only the data that is generated after the setting takes effect is affected. For example, if the **display machine name** switch is turned on and saved, the machine name will only be displayed in the new data generated thereafter, and the IP address will still be displayed in the previously generated data.

![Machine IP](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/xtrace/ex_machine_ip.png "Example: Display the IP address of the machine")

![Machine Name](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/xtrace/ex_machine_name.png "Example: Display Machine name")

To stop billing for an application, disable data collection.

On the application settings page, you can also configure whether to use all tags for the current application and manage all tags under your account. You can delete an application when you no longer need it.

## Open Application Settings

Follow these steps to open the application settings page.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, choose **application list**, and select a region at the top of the application list page.

3.  On the applications page, click **actions** in the **settings** column of an application.


## Display Machine name

Perform the following steps to display the name of the host where the application is deployed:

1.  On the application settings page, click the **custom configuration** tab \(displayed by default\).

2.  On the **custom configuration** tab, turn on **display configuration** switch in the **display configuration** area.

3.  Click **save** at the bottom of the page.


**Note:** Only the data that is generated after the setting takes effect is affected. For example, if the **display machine name** switch is turned on and saved, the machine name will only be displayed in the new data generated thereafter, and the IP address will still be displayed in the previously generated data.

## Stop Collecting application data

To stop application billing, perform the following steps to stop application data collection.

1.  On the application settings page, click the **custom configuration** tab \(displayed by default\).

2.  In the **collection configuration** section, turn on **disable data collection**.

3.  Click **save** at the bottom of the page.


## Enable or disable labels for an application

Follow these steps to enable or disable an existing label for your app.

1.  On the application settings page, click the **labels** tab.

2.  In the **apply tags** section, select the tags to be enabled and clear the corresponding tags.

3.  Click **save** at the bottom of the page.


## Manage all tags of an account

To manage all tags under an account, such as adding tags for all applications or deleting all existing tags, perform the following steps:

1.  On the application settings page, click the **labels** tab.

2.  Under **apply tags**, click **manage account tags**.

3.  In the manage account tags dialog box, perform the following operations as needed.

    ![Manage Tags Dialog Box](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/xtrace/db_manage_tags_setting.png "Manage account labels dialog box")

    -   To create a new tag, click the plus icon and enter a tag in the text box.
    -   To delete an existing tag, move the pointer over the tag and click the X icon on the left.

        **Note:** If you delete an existing tag in the manage account tags dialog box, all applications that have enabled the tag will lose it.

4.  Click **confirm** at the bottom of the dialog box.


## Delete an application

Follow these steps to delete unnecessary applications.

1.  On the application settings page, click **delete**.

2.  In the **delete application** section, click **delete**. In the **note** dialog box that appears, click **OK**.


