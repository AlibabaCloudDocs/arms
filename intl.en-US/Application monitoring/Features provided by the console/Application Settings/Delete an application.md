# Delete an application

When you no longer use Application Real-Time Monitoring Service \(ARMS\) to monitor your application and want to delete the application from ARMS, you can delete it on the Application Settings page.

## Procedure

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the upper part of the Applications page, select a region.

2.  On the Applications page, click the name of the required application.

3.  In the left-side navigation pane, click **Application Settings**. On the page that appears, click the Custom Configuration tab.

4.  On the Custom Configuration tab, turn off **Probe Master Switch** in the **Agent Switch Settings** section. Click **Save**.

    **Note:** The modification takes effect immediately without the need to restart the application. After you turn off Probe Master Switch, the system cannot monitor your application, and no fees are incurred. Proceed with caution when you perform this operation.

5.  Uninstall the ARMS agent. For more information, see [FAQ about ARMS agent uninstallation](/intl.en-US/Application monitoring/Application monitoring FAQ.mdli-dab-lbz-7ss).

6.  After the ARMS agent is uninstalled, click the **Delete** tab on the Application Settings page.

    **Warning:** This operation clears all monitoring data of the application, and the monitoring data cannot be restored.

    ![tab_am_delete_application](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5574658061/p82432.png)

7.  On the Delete tab, click **Delete Application**. In the Delete Application dialog box, set **Reasons** and click **OK** to permanently delete the application.

    ![db_am_delete_application](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5574658061/p82433.png)


You can find that the deleted application no longer appears on the Applications page.

**Related topics**  


[FAQ](/intl.en-US/Application monitoring/Application monitoring FAQ.md)

