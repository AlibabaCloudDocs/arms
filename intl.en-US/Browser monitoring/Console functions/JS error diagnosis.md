# JS error diagnosis

The browser monitoring module of Application Real-Time Monitoring Service \(ARMS\) provides a JavaScript \(JS\) error diagnosis function, to display basic information and distribution about JS errors and backtrack user behavior, helping you quickly locate the errors.

## Portal

1.  In the left-side navigation pane, choose **Browser Monitoring**. On the **Browser Monitoring** page, find the target application and click the application name.
2.  In the left-side navigation pane, choose **Application** \> **JS Error Diagnosis**.

## View error overview

In the **Error Overview** section, the statistics and trends of JS errors within the selected period of time appear, including the following metrics:

-   **Errors**: the total number of JS errors that occurred within the selected period of time.
-   **JS Error Rate**: the number of page views \(PVs\) with JS errors to the total PVs within the selected period of time.
-   **Affected Users**: the quantity and percentage of users that are affected by JS errors.

![应用层面的错误总览](../images/p187064.png "Application-specific error overview")

In the **Error Overview** section, perform the following operations:

-   Place the pointer over the curve. The number of errors, error rate, and number of affected users at the time point corresponding to the curve turning point appear in a floating manner.

-   Place the pointer over the turning point of the curve. When the pointer changes to a hand shape, click the turning point. The **Exception Insight** dialog box appears. For more information, see [Source map file](#sc_js_error_insight).

-   In the curve section, hold down the left mouse button and drag the mouse to select an area to zoom in and view the selected part of the curve. Double-click the curve. The original curve is restored.


**Note:** On the JS Error Diagnosis page, the **Error Overview** section displays the application-specific error overview. On the **Page Ranked by Error Rate** or **Page Error Rate Top 5** tab, click **Analyze**. The overview information of the corresponding tab appears.

![页面层面的错误总览](../images/p187065.png "Page-specific error overview")

## View pages ranked by error rate

On the **Page Ranked by Error Rate** tab, pages are ranked by JS error rate within the selected period of time in descending order. Error metrics are as follows:

-   **Page**: the page on which the JS error occurs.
-   **JS Error Rate**: the number of PVs with JS errors on the page to the total PVs within the selected period of time.
-   **Page View**: the number of views of the page.

![页面层面的错误总览](../images/p187065.png "Page ranked by error rate")

On the **Page Ranked by Error Rate** tab, you can perform the following operations:

**Analyze**: Click **Analyze** in the **Actions** column to go to the page-specific error overview.

## View exception insight

In the **Exception Insight** dialog box, information about the JS errors at a specific time point appears, including the following metrics:

-   **Errors**: the total number of JS errors at the specific time point.
-   **JS Error Rate**: the number of PVs with JS errors to the total PVs at the specific time point.
-   **Affected Users**: the quantity and percentage of users that are affected by JS errors.
-   **Frequent Errors Top 5**: the top 5 JS errors that occur the most frequently at the specific time point, including the information about the JS errors, the number of errors, and the number of affected users that are captured by ARMS.
-   **Page Error Rate Top 5**: the top 5 pages with the highest JS error rate at the specific time point, including the names of the pages with JS errors, the JS error rates of the pages, and the number of page views.

![JS错误异常洞察](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5190458061/p187070.png)

In the **Exception Insight** dialog box, you can perform the following operations:

-   Click the **Frequent Errors Top 5** tab, and then click **Diagnose** in the **Actions** column. The JS Error Diagnosis page appears.
-   Click the **Page Error Rate Top 5** tab, and then click **Analyze** in the **Actions** column. The page-specific error overview page appears.

## View frequent errors

On the **Frequent Errors** tab, JS errors are ranked by number within the selected period of time in descending order. Error metrics are as follows:

-   **Error Information**: the information captured by ARMS about the JS error.
-   **Page**: the page on which the JS error occurs.
-   **Errors**: the number of JS errors.
-   **Affected Users**: the quantity and percentage of users that are affected by JS errors.

On the **Frequent Errors** tab, you can perform the following operations:

**Diagnose**: Click **Diagnose** in the **Actions** column to go to the **Error Detail** tab.

**Note:** On the JS Error Diagnosis page, the JS errors of applications are displayed by default on the **Frequent Errors** tab. On the **Page Ranked by Error Rate** or **Page Error Rate Top 5** tab, click **Analyze**. The page-specific JS errors appear on the **Frequent Errors** tab.

## View error details

The following information is displayed on the **Error Detail** tab:

-   **Summary**
    -   **Name**
    -   **Type**
    -   **Time**: the time when the JS error is detected
    -   **Device**
    -   **OS**
    -   **Browser**
    -   **IP**
    -   **Region**
    -   **Row**
    -   **Column**
    -   **URL**
    -   **File**: the path of the file that has the JS error
-   **Stack Info**: the information related to the location of the JS error
-   **User Behavior Trace**: the user behavior trace, which is used to backtrack the error

![JS错误详情页面](../images/p203704.png "JS error details page")

On the **Error Details** tab, you can perform the following operations:

-   To specify the exact location of the JS error, click the triangle icon to the left of a stack in the **Stack Info** section to expand the row. Click **Choose Sourcemap**. In the Sourcemap File dialog box, select an existing source map file or upload a new source map file, and then click **OK**.

    ARMS uses the source map file to retrieve the exact location of the JS error.

-   To view the user behavior trace, see the [Backtrack user behavior](#sc_behavior) section.
-   To view the distribution of the JS error, click the **Error View** tab.


## Backtrack user behavior

On the **Error View** tab, the **User Behavior Trace** section displays the user behavior trace, helping to backtrack the error.

![Section Behavior](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5190458061/p60498.png)

## View error distribution

On the **Error View** tab of the JS Error Diagnosis page, the distribution of a specific JS error is displayed by the following metrics:

-   **Time**: the last 24 hours and last 30 days.
-   **Browser**.
-   **OS**.
-   **Device**.
-   **Geographical View**: Statistics are collected by province, municipality, or autonomous region in China View, and are collected by country or region in World View.

![JS错误分布页面](../images/p203745.png "JS error view page")

On the **Error View** tab, you can perform the following operations:

-   In the **Time View** section, place the pointer over the curve. The number of errors at the time point corresponding to the turning point of the curve appears in a floating manner.

-   On the **China View** or **World View** tab in the **Geographical View** section, click the **Errors** column name in the table on the right to switch the sorting order between ascending and descending.

    ![JS错误分布-地理](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5190458061/p203750.png)


## FAQ

-   How can I enable or disable user behavior backtracking?

    This feature is enabled by default. To disable the feature, add the behavior: false SDK configuration item to config. For more information about the SDK configuration items, see [Configuration items of the browser monitoring SDK](/intl.en-US/Browser monitoring/Configuration items of the browser monitoring SDK.md).

-   After user behavior backtracking is enabled, the error in the ARMS SDK code bl.js rather than the source code is located based on the printed information in console.log. How can I solve the problem?

    The reason is that ARMS rewrites log of the console object to monitor the content printed by the browser console. Solution:

    -   Method 1 \(recommended\): Set blackboxing for the Chrome browser.

        1.  Open the Chrome browser, press Ctrl + Shift + I to open the developer tools panel, and click **Settings**.

        2.  In the left-side navigation pane of **Settings**, choose **Blackboxing**. On the page that appears, click **Add pattern**. In the **Pattern** field, enter /bl. \*\\.js$ and then click **Add**.

    -   Method 2: Use the behavior: false SDK configuration item to disable user behavior backtracking.

        ```
        <script>
            ! (function ( c , b, d, a ) {
                c [a] || ( c[a] = {});
                c [a].config = {
                    pid: "xxxxx",
                    imgUrl: "https://arms-retcode.aliyuncs.com/r.png?",
                    sendResource: true,
                    enableLinkTrace: true,
                    behavior: false
                };
                with(b) with(body) with(insertBefore(createElement("script"), firstChild)) setAttribute("crossorigin", "", src = d)
            })(window, document, "https://retcode.alicdn.com/retcode/bl.js", "__bl");
        </script>
        ```

    After the preceding handling, the error in the source code can be located based on the printed information in console.log.


**Related topics**  


[Configuration items of the browser monitoring SDK](/intl.en-US/Browser monitoring/Configuration items of the browser monitoring SDK.md)

