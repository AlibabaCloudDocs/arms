# Diagnose JS errors by using the ARMS frontend monitoring feature

JavaScript \(JS\) errors directly affect the quality of applications. Therefore, JS errors must be located and diagnosed. The JS error diagnostics capability provided by the frontend monitoring feature of Application Real-Time Monitoring Service \(ARMS\) can accurately locate and diagnose JS errors with efficiency.

A source map is generated with a builder.

In practice, you may encounter the following difficulties during JS error diagnostics:

-   Difficult to replicate.

    For example, when User A visits a page, the page is loaded on the browser of User A. The time consumed for loading the page is affected by factors such as the region, network, browser, and carrier. Therefore, the actual situation that occurred when User A accessed the page is difficult to be replicated.

-   Lack of monitoring information for in-depth investigation.

    Most frontend monitoring projects use the PerformanceTiming object to obtain the loading time of the full page, which excludes the loading time of static resources. Therefore, performance bottlenecks cannot be identified.


The ARMS frontend monitoring feature can use the source map to find the real location of the error in code and use the user behavior backtracking feature to replicate the JS error. This allows developers to locate errors in the source code and corresponding code blocks with efficiency.

## Step 1: Install an ARMS agent

To comprehensively monitor applications, you must install the ARMS agent for your applications. Select a method to install the ARMS agent as needed. For more information, see [Browser monitoring overview](/intl.en-US/Browser Monitoring/Quick start/Browser monitoring overview.md).

## Step 2: View the error overview

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Browser Monitoring**.

3.  On the Browser Monitoring page, click the name of the application that you want to view.

4.  In the left-side navigation pane, click **JS Error Diagnosis**.

    ![JS Error Diagnosis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5502601161/p60924.png)

    -   View the total number of errors, JS error rate, and quantity and percentage of affected users in the **Error Overview** section.
    -   Determine the JS error trend based on the curve chart.
    -   Filter frequent errors on the **Frequent Errors** tab.
    -   Determine the global JS errors based on the information on the **Page Ranked by Error Rate** and **Error View** tabs.

## Step 3: Diagnose a specific error

After you determine global errors, you must troubleshoot specific errors. You can use the following two methods to diagnose JS errors in the ARMS console:

-   On the **Frequent Errors** tab, click **Diagnose** to go to the diagnostics page.
-   In the curve chart, go to the **Exception Insight** dialog box at a specific point in time and then go to the diagnostics page.

The second method is used as an example in this topic.

1.  When you find that the error rate at a specific point in time on the curve chart suddenly increases, move the pointer over the turning point of the curve. When the pointer changes to a hand shape, click the turning point. The Exception Insight dialog box for that point in time appears. For more information, see [View exception insight](/intl.en-US/Browser Monitoring/Console functions/JS error diagnostics.md).

    ![Insight into JS errors](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5190458061/p187070.png)

2.  Click the **Frequent Errors Top 5** tab. On this tab, select an error and click **Diagnose** in the **Operation** column.

    The Error Detail tab appears.


## Step 4: View error details

JS error details include the first occurrence time, version for the first occurrence \(optional\), error name, error type, point in time of the occurrence, device, operating system, browser, IP address, connection type, region, error URL, and application version. The details also include the file, line, and column where the error occurs. The map module on the real-time dashboard reported an error of invalid data during the update, and the error occurred in Line 1 and Column 79585, as shown in the following figure.

![Error Details](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5502601161/p60929.png)

## Step 5: Locate the error in the source code

The information acquired from the JS error details is insufficient for error diagnostics, because online code is unreadable after compilation, compression, and obfuscation. Although you can see the error occurred in Line 1 and Column 79585, this does not specify the actual location in the source code. In this case, you must use the source map for source code mapping.

1.  In the **Stack Info** section, click the triangle icon on the left side of a stack to show the line, and then click **Choose Sourcemap**.

2.  In the Sourcemap File dialog box, select an existing source map file or upload a new source map file, and click **OK**.

    ![Source map file](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1907772161/p212641.png)

    The ARMS frontend monitoring feature uses the source map to identify the exact error location. If the selected source map matches the error in the source code, the original error location is marked in red in the **Source Code** section. After the analysis, you can clearly see the file and the line where the error occurred. In addition, you can use a source map for source code mapping for each line in the error stack.


## Step 6: View the backtracked user behaviors

As shown in the source code mapping, the source code error occurred when invalid data was loaded during the creation of the map component. However, invalid data may appear in a variety of forms. Null judgment and fault tolerance have been performed for data in the source code, but the exception of invalid data is still triggered. If a snapshot can be taken for the data of the error, you can locate the error more accurately. However, onsite data is usually unavailable in global exception capture, and troubleshooting depends only on the data information that is reported with the exception.

The best way is to replicate the error. The ARMS frontend monitoring feature defines event nodes on a page as user behaviors, such as page loading, route jumps, page clicks, API requests, and console output. User behaviors are connected in chronological order to form a behavior trace. Behavior backtracking upon the error can help developers replicate the error.

The user behavior backtracking upon the error shows that an API request was made before the error occurred, as shown in the following [Figure 1](#fig_jkr_1e8_zea) figure. This API request tried to request the real-time update of the map module, but the returned data is ConsoleNeedLogin. This indicates that the user has logged off from the page. This is the root cause of invalid data.

![User Behavior Trace](../images/p60700.png "User behavior backtracking")



**Related topics**  


[JS error diagnostics](/intl.en-US/Browser Monitoring/Console functions/JS error diagnostics.md)

[Causes and solutions for script errors](/intl.en-US/Browser Monitoring/Causes and solutions for script errors.md)

