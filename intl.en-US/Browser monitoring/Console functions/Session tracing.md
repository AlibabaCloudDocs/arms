# Session tracing

If you want to reproduce the situation where an error occurred based on the context to identify the cause of the error, you can use the session tracing feature of Application Real-Time Monitoring Service \(ARMS\) Browser Monitoring. This feature implements distributed tracing based on a username or user ID to show a comprehensive list of user behavior traces, including page loading, API calls, JS errors, and user operations. This helps identify and analyze the cause of an error.

## Procedure

1.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the application.

2.  In the left-side navigation pane, choose **Application** \> **Session Traces**.


## View session details

1.  On the Session Traces page, set **User ID** or **Username** and click **Search** to search for the corresponding session.

    **Note:** For information about how to set a username, see [t152280.md\#sc\_arms\_bm\_sdk\_setUsername](/intl.en-US/Browser monitoring/SDK reference.md).

2.  In the Session List section, find the session and click its ID in the **Session ID** column. The Session Details page appears.

3.  In the **Overview** section, view basic information of the session such as the username, user ID, session ID, number of page views \(PVs\), number of JS errors, number of API calls, number of API failures, number of slow loads, device, region, browser, IP address, and network system.

4.  In the **Session Path** section, view the access path of the user.

    1.  Click the **+** icon on the left of the page to show the user behavior traces.

        ![pg_retcode_session_detail](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3304227951/p86747.png)

    2.  Click **Details** on the right of a user behavior to view the details such as details about API calls, slow loads, and JS errors.


## Other methods to view session details

-   In the left-side navigation pane, choose **Application** \> **Page Speed**. On the page that appears, click a session ID in the **Session ID** column of the **Slow Page Session Trace \(TOP20\)** section.
-   In the left-side navigation pane, choose **Application** \> **JS Error Diagnosis**. On the Frequent Errors tab, click **Diagnose** in the **Actions** column that corresponds to an error. On the page that appears, click **View Session** in the User behavior backtracking section.
-   In the left-side navigation pane, choose **Application** \> **API Details**. On the **API Requests** tab, click the number of errors in the **Error Number** column. On the page that appears, click **View Session** in the **Network Request Information** section.
-   In the left-side navigation pane, choose **Application** \> **View Details**. On the All Logs tab, click **View Session** in the **Actions** column in the Log List section.

**Related topics**  


[Slow session tracing](/intl.en-US/Browser monitoring/Tutorials/Slow session tracing.md)

