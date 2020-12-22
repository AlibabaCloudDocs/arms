# Diagnose JS errors by backtracking user actions

In the JS error diagnosis process, Application Real-Time Monitoring Service \(ARMS\) Browser Monitoring provides the user action backtracking feature to shows you a comprehensive list of the user actions leading up to the error.

ARMS Browser Monitoring defines all events on the page as user actions, including console actions, page jumps, user clicks, user inputs, and API calls. You can connect user actions in chronological order to form an action trace. Then, you can backtrack and analyze the action trace to reproduce the situation in which the error occurred.

## Step 1: Install the ARMS agent

After you install the ARMS agent, your frontend applications can be fully monitored. Select a method to install the ARMS agent as needed. For more information, see [Access overview of browser monitoring](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/Access overview of browser monitoring.md).

## Step 2: View frequent errors

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/#/home). In the left-side navigation pane, click **Browser Monitoring**.

2.  On the Browser Monitoring page, click the name of the target application.

3.  In the left-side navigation pane, click **JS Error Diagnosis**.

4.  On the JS Error Diagnosis page, click the **Frequent Errors** tab.

    ![](../images/p60698.png)


## Step 3: Diagnose causes of the error

Use the user action backtracking feature to reproduce the situation in which the JS error occurred and diagnose causes of the error.

1.  Click **Diagnose** in the **Operation** column on the right.

2.  On the **Error Detail** tab, analyze user behaviors in the **User Behavior Trace** section to determine which operation causes the error.

    ![](../images/p60700.png)


**Related topics**  


[Script error causes and solutions](/intl.en-US/Browser monitoring/Script error causes and solutions.md)

