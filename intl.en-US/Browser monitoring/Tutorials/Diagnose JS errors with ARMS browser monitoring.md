# Diagnose JS errors with ARMS browser monitoring

JavaScript \(JS\) errors directly affect the quality of front-end applications. Therefore, it is particularly important to locate and diagnose JS errors. The JS error diagnosis function provided by browser monitoring of Application Real-Time Monitoring Service \(ARMS\) can accurately locate and quickly diagnose JS errors.

Developers have generated a source map with the builder.

In practice, you may encounter the following difficulties during JS error diagnosis:

-   Difficult to recur

    For example, when user A accesses a page, the page is loaded on user A's local browser. As the page loading duration is affected by factors such as the region, network, browser, or carrier, the actual situation when user A accesses the page cannot recur.

-   Lack of monitoring information for in-depth investigation

    Most browser monitoring services use the PerformanceTiming object to obtain the full page loading time, which does not include the static resource loading information. As a result, the performance bottleneck cannot be located.


ARMS browser monitoring can use the source map to find the real error location in code, and use the user behavior backtracking function to recur the JS error. This allows developers to quickly locate the error location in the source code and the corresponding code blocks.

## Step 1: Install the ARMS agent

After you install the ARMS agent, your front-end applications can be fully monitored. Select a method to install the ARMS agent as needed. For more information, see [Overview of Getting Started with Browser Monitoring](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/Overview of Getting Started with Browser Monitoring.md).

## Step 2: View the error overview

1.  On the Browser Monitoring page, click the name of your application.

2.  In the left-side navigation pane, choose **JS Error Diagnosis**.

    -   View the total number of errors, error rate, number of affected users, and percentage of affected users in **Error Overview**.
    -   Determine the JS error trend according to the line chart.
    -   Filter frequent errors in **Frequent Errors**.
    -   Judge the global JS errors according to the information in **Page Ranked by Error Rate** and **Error View**.

## Step 3: Diagnose a specific error

After judging the global errors, you need to troubleshoot the specific error. You can use the following two methods to diagnose JS errors in ARMS browser monitoring. The second method is used as an example in this article.

-   On the **Frequent Errors** tab, click **Diagnose** to access the diagnosis page.
-   In the error chart, go to the **Exception Insight** dialog box at a specific time point and then access the diagnosis page.

1.  When you find that the error rate at a specific time point on the error chart suddenly increases, place the pointer over the turning point of the curve. When the mouse is displayed as a hand shape, click the turning point to display the Exception Insight dialog box for that time point. For more information, see [View exception insight](/intl.en-US/Browser monitoring/Console functions/JS error diagnosis.md).

2.  Click the **Frequent Errors Top 5** tab. On the tab that appears, select an error and click **Diagnose** in the **Actions** column. The JS Error Diagnosis page appears.


## Step 4: View error details

Onsite JS error information includes the first occurrence time, first occurrence version \(optional\), error name, error type, device, operating system, browser, and the page, file, row, and column where the error resides. The map module on the real-time dashboard reported an invalid data error during the update, and the error occurred in line 1 and column 79585.

## Step 5: Locate the error code

The information acquired from the JS error details is insufficient for problem diagnosis, because online code is unreadable after being compiled, compressed, and obfuscated. Although you can see the error occurred in line 1 and column 79585, this is not the actual location in the source code. In this case, you need to use the source map for source code mapping.

1.  In the **Stack Info** section, click the triangle icon on the left of a stack to expand the row, and click **Choose Sourcemap**.

2.  In the Sourcemap File dialog box, select an existing source map or upload a new one, and click **OK**.

3.  ARMS browser monitoring uses the source map to locate the exact JS error location. If the selected source map matches the error in the source code, the original error location is marked in red in the **Source Code** section. You can easily find that the error occurred in line 51 in the geog-map.js file. In addition, you can use a source map for source code mapping for each line in the error stack.


## Step 6: View the backtracked user behaviors

The source code error occurred when invalid data was loaded during the creation of the map component. However, there are many possibilities of invalid data. Null judgment and fault tolerance have been performed for data in the preceding code, but the invalid data exception is still triggered. If a snapshot of the data upon the error can be taken, the problem can be located more accurately. However, onsite data is usually unavailable in global exception capture, and troubleshooting depends on only the data information reported with the exception.

Is there any other way available to help troubleshooting? The best way is to recur the problem. ARMS browser monitoring defines each event node on the page as user behavior, such as page loading, route jumps, page clicks, API requests, and console output. User behavior is connected in chronological order to form a behavior link. Behavior backtracking upon the error can help developers recur the problem.

The user behavior backtracking upon the error shows that there is an API request before the error. This API request tries to request real-time update of the map module. However, the returned data is ConsoleNeedLogin, indicating logout from the page. This is the root cause of invalid data.

**Related topics**  


[JS error diagnosis](/intl.en-US/Browser monitoring/Console functions/JS error diagnosis.md)

[Script error causes and solutions](/intl.en-US/Browser monitoring/Script error causes and solutions.md)

