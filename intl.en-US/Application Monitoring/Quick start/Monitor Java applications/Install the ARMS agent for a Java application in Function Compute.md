# Install the ARMS agent for a Java application in Function Compute

After you install the Application Real-Time Monitoring Service \(ARMS\) agent for a Java application in Function Compute, you can use the agent to monitor the application. Then, you can view the monitoring data of the application, including the application topology, API requests, abnormal transactions, and slow transactions. This topic describes how to install the ARMS agent for a Java application in Function Compute.

[Create a function in the Function Compute console]()

## Obtain a license key

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
2.  On the Applications page, select a region in the top navigation bar, and click **Add Application** in the upper-right corner.
3.  In the upper part of the Add Application page, click the copy icon to the right of the license key and save the key.

    ![Section LicenseKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6076728061/p45312.png)


## Procedure

1.  Log on to the [Function Compute console](https://fc.console.aliyun.com).

2.  In the top navigation bar, select a region.

3.  In the left-side navigation pane, click **Services and Functions**.

4.  In the Services pane, click the required service in Function Compute.

5.  On the Functions tab, find the function that you want to modify and click **Modify Configurations** in the Actions column.

6.  On the Modify Configurations page, set the Environment Variables parameter to Key Value.

7.  Set the key to FC\_EXTENSIONS\_ARMS\_LICENSE\_KEY, set the value to the license key that is obtained in [Obtain a license key](#section_h12_i6i_iti), and then click **Submit**.

    ![Connect a Java application in Function Compute to ARMS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9550463161/p200496.png)


## Verify the result

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
2.  On the Applications page, select the destination region in the top navigation bar.

If your Java application is displayed in the application list and data is imported after you call the function multiple times in the [Function Compute console](https://fc.console.aliyun.com), the Java application is connected to ARMS.

**Related topics**  


[Create a function in the Function Compute console]()

