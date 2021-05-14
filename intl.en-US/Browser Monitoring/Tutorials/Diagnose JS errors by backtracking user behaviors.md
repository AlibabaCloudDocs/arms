# Diagnose JS errors by backtracking user behaviors

In the process of JavaScript \(JS\) error diagnostics, Application Real-Time Monitoring Service \(ARMS\) frontend monitoring provides the user behavior backtracking feature to show you a comprehensive list of the user behaviors that lead up to the errors.

ARMS frontend monitoring defines all events on the page as user behaviors, including console behaviors, page jumps, user clicks, user inputs, and API calls. You can connect user behaviors in chronological order to form a behavior trace. Then, you can backtrack and analyze the behavior trace to reproduce the situation in which a specific error occurred.

## Step 1: Install an ARMS agent

After you install the ARMS agent, your frontend applications can be fully monitored. Select a method to install the ARMS agent as needed. For more information, see [Browser monitoring overview](/intl.en-US/Browser Monitoring/Quick start/Browser monitoring overview.md).

## Step 2: Diagnose an error

Use the user behavior backtracking feature to reproduce the situation in which a specific JS error occurred and diagnose causes of the error.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Browser Monitoring**.

3.  On the Browser Monitoring page, click the name of the application for which you want to diagnose the error.

4.  In the left-side navigation pane, choose Application \> **JS Error Diagnosis**.

5.  On the JS Error Diagnosis page, click the **Frequent Errors** tab.

    ![JS Error Diagnosis - Frequent Errors](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7502601161/p60698.png)

6.  Click **Diagnose** in the **Actions** column of the error that you want to diagnose.

7.  On the **Error Detail** page, analyze user behaviors in the **User Behavior Trace** section to determine the behaviors that cause the error.

    ![Section Behavior](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5190458061/p60498.png)


**Related topics**  


[Causes and solutions for script errors](/intl.en-US/Browser Monitoring/Causes and solutions for script errors.md)

