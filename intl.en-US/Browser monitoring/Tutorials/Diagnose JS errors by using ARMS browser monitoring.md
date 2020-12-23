# Diagnose JS errors by using ARMS browser monitoring

JavaScript \(JS\) errors directly affect the quality of front-end applications. Therefore, it is particularly important to locate and diagnose JS errors. The JS error diagnosis feature provided by browser monitoring of Application Real-Time Monitoring Service \(ARMS\) can quickly and accurately locate and diagnose JS errors.

Developers have generated a source map by using the builder.

In practice, you may encounter the following difficulties during JS error diagnosis:

-   Difficult to replicate

    For example, when User A accesses a page, the page is loaded on the local browser of User A. Because the loading duration of the page is affected by factors such as the region, network, browser, or carrier, the actual situation occurred when User A accessed the page cannot be replicated.

-   Lack of monitoring information for in-depth investigation

    Most browser monitoring services use the PerformanceTiming object to obtain the full page loading time, which does not include loading information of static resources. As a result, the performance bottleneck cannot be located.


ARMS browser monitoring can use the source map to find the real location of the error in code and use the user behavior backtracking feature to replicate the JS error. This allows developers to quickly locate errors in source code and corresponding code blocks.

## Step 1: Install the ARMS agent

To comprehensively monitor frontend applications, you must install the ARMS agent for your frontend applications. Select a method to install the ARMS agent as needed. For more information, see [Access overview of browser monitoring](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/Access overview of browser monitoring.md).

## Step 2: View the error overview

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  On the Browser Monitoring page, click the name of the application that you want to manage.

3.  In the left-side navigation pane, click **JS Error Diagnosis**.

    ![JS Error Diagnosis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3227278061/p60924.png)

    -   View the total number of errors, error rate, number of affected users, and percentage of affected users in **Error Overview**.
    -   Determine the JS error trend based on the line chart.
    -   Filter frequent errors in **Frequent Errors**.
    -   Determine the global JS errors based on the information in **Page Ranked by Error Rate** and **Error View**.

## Step 3: Diagnose a specific error

After you have determined any global errors, you must troubleshoot specific errors. You can use the following two methods to diagnose JS errors in ARMS browser monitoring. The second method is used as an example in this topic.

-   On the **Frequent Errors** tab, click **Diagnose** to access the diagnosis page.
-   In the error chart, go to the **Exception Insight** dialog box at a specific time point and then access the diagnosis page.

1.  When you find that the error rate at a specific time point on the error chart suddenly increases, place the pointer over the turning point of the curve. When the pointer is displayed as a hand shape, click the turning point to display the Exception Insight dialog box for that time point. For more information, see [JS error diagnosis](/intl.en-US/Browser monitoring/Console functions/JS error diagnosis.md).

    ![Exception Insight](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3227278061/p60925.png)

2.  Click the **Frequent Errors Top 5** tab. On the tab that appears, select an error and click **Diagnose** in the **Actions** column. The JS Error Diagnosis page appears.


## Step 4: View error details

Onsite JS error information includes the first occurrence time, first occurrence version \(optional\), error name, error type, device, operating system, browser, and the page, file, row, and column where the error resides. As shown in [Figure 1](#fig_2hx_7ul_nvx), the map module on the real-time dashboard reported an invalid data error during the update, and the error occurred in line 1 and column 79585.

![Error Details](../images/p60929.png "Error details page")

## Step 5: Locate the error code

The information acquired from the JS error details is insufficient for problem diagnosis, because online code is unreadable after being compiled, compressed, and obfuscated. Although you can see the error occurred in line 1 and column 79585, this is not the actual location in the source code. In this case, you must use the source map for source code mapping.

1.  In the **Stack Info** section, click the triangle icon on the left of a stack to expand the row, and click **Choose Sourcemap**.

2.  In the Sourcemap File dialog box, select an existing source map or upload a new one, and click **OK**.

3.  ARMS browser monitoring uses the source map to locate the exact JS error location. If the selected source map matches the error in the source code, the original error location is marked in red in the **Source Code** section.


## Step 6: View the backtracked user behaviors

The source code error occurred when invalid data was loaded during the creation of the map component. However, invalid data may appear in a variety of forms. Null judgment and fault tolerance have been performed for data in the preceding code, but the invalid data exception is still triggered. If a snapshot of the data at the time of the error can be taken, you can locate the problem more accurately. However, onsite data is usually unavailable in global exception capture, and troubleshooting depends on only the data information reported with the exception.

Is there any other way available to help troubleshooting? The best way is to replicate the problem. ARMS browser monitoring defines each event node on the page as user behavior, such as page loading, route jumps, page clicks, API requests, and console output. User behavior is connected in chronological order to form a behavior link. Behavior backtracking upon the error can help developers replicate the problem.

The user behavior backtracking upon the error shows that there is an API request before the error. This API request tries to request real-time update of the map module. However, the returned data is ConsoleNeedLogin, indicating logout from the page. This is the root cause of invalid data.

**Related topics**  


[JS error diagnosis](/intl.en-US/Browser monitoring/Console functions/JS error diagnosis.md)

[Script error causes and solutions](/intl.en-US/Browser monitoring/Script error causes and solutions.md)

