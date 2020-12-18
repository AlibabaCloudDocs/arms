# Install the ARMS agent for Java applications in Function Compute

After you install the Application Real-Time Monitoring Service \(ARMS\) agent, you can use it to monitor Java applications in Function Compute. You can view the monitoring data of application topology, API requests, abnormal transactions, and slow transactions. This topic describes how to install the ARMS agent for Java applications in Function Compute.

[Create a function in the Function Compute console]()

## Obtain a License Key

1.  Log on to the[ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
2.  On the Applications page, select the destination region in the top navigation bar, and click **Add Application** in the upper-right corner.
3.  At the top of the Add Application page, click the copy icon to the right of the License Key and save the Key.

    ![Section LicenseKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6076728061/p45312.png)


## Procedure

1.  Log on to the [Function Compute console](https://fc.console.aliyun.com).

2.  In the top navigation bar, select a region.

3.  In the left-side navigation pane, click **Service/Function**. On the **Service/Function** page, find the function, and click **Modify Configurations** in the Actions column.

4.  On the Modify Configurations page, set Environment Variables to Key value.

5.  Set the key to FC\_EXTENSIONS\_ARMS\_LICENSE\_KEY, set the value to the License Key that is obtained in [Obtain a License Key](#section_h12_i6i_iti), and then click **Submit**.


## Verify the result

1.  Log on to the[ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
2.  At the top of the Applications page, select the destination region.

If your Java application is displayed in the application list and data is imported after you call the function multiple times in the [Function Compute console](https://fc.console.aliyun.com), the Java application is connected to ARMS.

**Related topics**  


[Create a function in the Function Compute console]()

