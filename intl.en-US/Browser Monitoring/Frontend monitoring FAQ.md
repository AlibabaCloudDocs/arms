# Frontend monitoring FAQ

This topic provides answers to frequently asked questions about frontend monitoring.

## Overview

-   [Why do I see asterisks \(\*\) in the names of some monitored pages or APIs?](#section_sky_g2y_g2b)
-   [Why is the PV list different from the page speed list?](#section_vqb_h2y_g2b)
-   [No trace ID is found in the API logs, and as a result, the system fails to redirect me to the application monitoring page. Why this happens?](#section_wxb_s5c_b6a)
-   [Why is the Source Map file error displayed when I am troubleshooting JavaScript \(JS\) errors?](#section_aqp_vqy_svi)
-   [What are the differences between console setting and the setConfig method?](#section_9i9_3y6_bdo)
-   [How do I configure the environment and version in an SDK?](#section_qrc_oud_6hf)
-   [How do I view the version number of a configuration?](#section_gi2_19f_0ez)
-   [How do I view the TP of a user for a page?](#section_ad7_a2u_1q5)
-   [What do I do if the ARMS configuration does not take effect?](#section_3cp_y4v_p7s)
-   [Why are JS errors on mini programs not reported?](#section_bq0_sla_43t)
-   [Can JS errors returned by the console.error method be listened to?](#section_00c_ong_nfg)
-   [In the Weex environment, why does a UID set for a mini program not take effect?](#section_i5k_9k6_l2z)
-   [How long can logs be stored?](#section_cnt_xx6_6ky)
-   [After I activate the expert edition for ARMS, can I continue to use the sites that are created during the trial period?](#section_w67_rn5_qtk)
-   [Why are the PVs on the same page different among modules in the ARMS console?](#section_1y7_gr1_fcu)
-   [Why is the value of the duration parameter smaller than that of the connect download parameter?](#section_m0j_njc_kh3)

## Why do I see asterisks \(\*\) in the names of some monitored pages or APIs?

The page statistics of Application Real-Time Monitoring Service \(ARMS\) frontend monitoring are retrieved based on actual page URLs and calculated by dimension. The asterisks \(\*\) included in the names of monitored pages or APIs are not a part of the page URLs. The asterisks \(\*\) indicate the result of URL convergence. Therefore, a name that includes an asterisk \(\*\) is not a specific URL, but a group of similar URLs.

![Satisfaction Trend](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6189278061/p111353.png)

How URL convergence works

-   Problem: Variables make it difficult to monitor or analyze similar URLs.
-   Objective: Group similar URLs by replacing variables with asterisks \(\*\).
-   Solution: Use the Alibaba Cloud proprietary URL convergence algorithm to group similar URLs and decrease the number of URLs. This way, you can keep as much semantic information as possible and decrease the number of URLs. This is done in two steps:
    -   Aggregation: Aggregate similar URLs into one group.
    -   Variable identification: Extract the variables from the URLs in the same group, and replace the variables with asterisks \(\*\).

The following figure shows the URL convergence process.

![Convergence Process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6189278061/p111355.png)

Solution to URL convergence

For information about how to disable URL convergence, see [urlHelper](/intl.en-US/Browser Monitoring/SDK reference.md).

[\[Back to the top\]](#sc_index)

## Why is the PV list different from the page speed list?

This is because your application is a single-page application \(SPA\), and the SPA auto-resolution feature is enabled. In the SPA application scenario, page views \(PVs\) and the page speed are measured by using the following methods:

-   PVs: When a hashchange event is triggered, the PV data is automatically reported to record the PVs of the page based on the hash value. Therefore, when you view the PV list of an SPA, you can view the exact PVs of the hash pages.
-   Page speed: When the hash value of an SPA changes, the page speed does not change. Therefore, the page speed is not recorded based on the hash value. This way, unnecessary reports are avoided and page performance is clear.

[\[Back to the top\]](#sc_index)

## No trace ID is found in the API logs, and as a result, the system fails to redirect me to the application monitoring page. Why this happens?

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the target application.

3.  In the left-side navigation pane, choose **Settings** \> **Application Settings**.

4.  On the Precondition tab, check whether **Associate with Application Monitoring** is selected for the ARMS agent configuration. If Associate with Application Monitoring is not selected, select it. Then, connect the ARMS agent to the frontend application again.

    ![tab_retcode_settings_precondition](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6189278061/p111356.png)

    Check whether the trace IDs are generated in the API logs. If no trace ID is not generated, perform the operations described in the [following step](#step_thx_955_m4j).

5.  Check whether the domain name used in your page request is the same as the domain name used in your API request. If the domain name used in your page request is different from the domain name in your API request, this is a cross-domain access. In this case, trace IDs fail to be generated to prevent API request failure caused by cross-domain authentication.

    For information about how to resolve this problem, see [Use the front-to-back tracing feature to diagnose causes of API errors](/intl.en-US/Browser Monitoring/Tutorials/Use the front-to-back tracing feature to diagnose API errors.md).


[\[Back to the top\]](#sc_index)

## Why is the Source Map file error displayed when I am troubleshooting JavaScript \(JS\) errors?

1.  Make sure that the file suffix is .js.map.

2.  Make sure that your account has the permissions to write data to ARMS. If your account has no write permissions, contact your administrator.


[\[Back to the top\]](#sc_index)

## What are the differences between console setting and the setConfig method?

Console setting can accelerate only the generation of configuration code, and the generated code takes effect only after the code is published. However, modifications made by calling the setConfig method immediately take effect.

![Generate code in the ARMS console](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6189278061/p125266.png)

In addition, console setting is valid only when you initialize ARMS to monitor an application. When the application is being monitored by ARMS, you must call the setConfig method to modify configurations.

[\[Back to the top\]](#sc_index)

## How do I configure the environment and version in an SDK?

You can set the release parameter to compare versions. For more information, see [release](/intl.en-US/Browser Monitoring/SDK reference.md). You can also set the environment parameter to distinguish different environments. For more information, see [environment](/intl.en-US/Browser Monitoring/SDK reference.md).

-   The value prod indicates an online environment.
-   The value gray indicates a phased-release environment.
-   The value pre indicates a staging environment.
-   The value daily indicates a daily environment.
-   The value local indicates a local environment.

[\[Back to the top\]](#sc_index)

## How do I view the version number of a configuration?

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the target application.

3.  In the left-side navigation pane, choose **Application** \> **View Details**.

    The version number in a log is displayed in the **Version** column in the **Log List** section.

    ![View the version number](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6189278061/p125276.png)

4.  You can also filter logs by environment and version in the menu bar. You can filter logs only after PV logs are set with a version number.

    ![Filter logs by environment or version](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6189278061/p125274.png)


[\[Back to the top\]](#sc_index)

## How do I view the TP of a user for a page?

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the target application.

3.  In the left-side navigation pane, choose **Application** \> **Session Traces**.

4.  In the Session List section, find the target session and click its ID in the **Session ID** column. The Session Details page appears.

5.  Move the pointer over the timeline area in the Visit Timeline column to view the time on page \(TP\) of a user for a page.


[\[Back to the top\]](#sc_index)

## How do I view the custom performance metrics for frontend monitoring of ARMS?

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the target application.

3.  In the left-side navigation pane, choose **Application** \> **Page Speed**.

4.  Custom performance metrics are displayed in the **Page Speed** section.


[\[Back to the top\]](#sc_index)

## What do I do if the ARMS configuration does not take effect?

The possible reason is that the browser cache is not updated. To resolve this issue, perform the following operations: In the left-side navigation pane of the ARMS console, choose Application \> View Details. Switch to the latest version to view the trend chart. If the version number is not configured, you can set the release parameter of the ARMS SDK. For more information, see [release](/intl.en-US/Browser Monitoring/SDK reference.md). After the release parameter is set, check whether the value that you specified is displayed as the latest version.

[\[Back to the top\]](#sc_index)

## Why are JS errors on mini programs not reported?

This may be because error messages are captured by the trycatch statement at the underlying layer of the mini programs in asynchronous mode, and the error messages fail to upload. You can try to manually report error messages. For more information, see [t152281.md\#section\_qe7\_9uq\_4a1](/intl.en-US/Browser Monitoring/API reference.md).

[\[Back to the top\]](#sc_index)

## Can JS errors returned by the console.error method be listened to?

-   Yes, JS errors returned by the console.error method can be listened to. Web browsers report the error messages that meet the format requirements of JS errors.
-   On the mini program side, you can try to manually report error messages. For more information, see [t152281.md\#section\_qe7\_9uq\_4a1](/intl.en-US/Browser Monitoring/API reference.md).

[\[Back to the top\]](#sc_index)

## In the Weex environment, why does a UID set for a mini program not take effect?

-   If you have not called the setConfig method, check whether you specified a UID during initialization configuration. If you did not specify a UID, specify one.
-   If you have called the setConfig method, specify another UID and call the method again.

[\[Back to the top\]](#sc_index)

## How long can logs be stored?

Logs can be stored for up to one month.

[\[Back to the top\]](#sc_index)

## After I activate the expert edition for ARMS, can I continue to use the sites that are created during the trial period?

-   No, you cannot continue to use those sites. Within 15 days after the trial period expires, the sites are suspended due to overdue payments. You can try to restart the application.
-   If the expert edition is not activated within 15 days after the trial period expires, the sites are deleted to save your computing and storage resources. Relevant resources are released and the data on the resources cannot be recovered.

[\[Back to the top\]](#sc_index)

## What version numbers are used by the application edition and host edition of ARMS?

-   The application edition uses the version number of the current online project. You can set the release parameter of the ARMS SDK to specify the version number of the application edition. For more information, see [release](/intl.en-US/Browser Monitoring/SDK reference.md).
-   The host edition uses the version number of the app where the current project resides. The version number of the host edition is automatically obtained by the SDK. The version of a hosted app cannot be resolved. Only versions of Taobao, Alipay, or WeChat are resolved.

[\[Back to the top\]](#sc_index)

## Why are the PVs on the same page different among modules in the ARMS console?

On the Page Speed page, the number of PVs is equal to the product of the number of entries in the performance log and the sample rate.

On the Page page under Dimensions, the number of PVs is equal to the value shown in the PV log.

Performance logs to be automatically reported are reported only after pages are loaded. A performance log is reported each time the page is refreshed.

After the SPA mode is enabled, PV logs are reported every time routes are switched. In the SPA mode, the number of performance logs is smaller than the number of PV logs, which results in a large difference in the PVs for different modules.

[\[Back to the top\]](#sc_index)

## Why is the value of the duration parameter smaller than that of the connect download parameter?

The performance data loaded to ARMS resources is obtained from the `performance.getEntriesByType('resource')` method. The domain name of a third-party ARMS resource must be the same as that of the site of the resource being requested. By default, the value of 0 is obtained from the `performance.getEntriesByType('resource')` method for the following parameters of the performance data of cross-domain resources:

```
redirectStart
redirectEnd
domainLookupStart
domainLookupEnd
connectStart
connectEnd
secureConnectionStart
requestStart
responseStart
```

Some time properties may be inaccurate or abnormal because the preceding parameters are used in the calculation. For example, in `connect download:responseEnd - responseStart`, the value of the duration parameter is smaller than the value of the connect download parameter because the timestamp of the responseStart parameter is 0.

-   To resolve this issue, for self-managed CDN resources, you can configure the response header Timing-Allow-Origin to specify the time allowed to obtain the resources.
-   For third-party resources, we recommend that you take the value of the duration parameter as the major reference.

[\[Back to Top\]](#sc_index)

