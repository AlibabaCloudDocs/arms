# Browser monitoring FAQ

This topic provides answers to commonly asked questions about browser monitoring.

## Overview

-   [Why do I see asterisks \(\*\) in the names of some monitored pages or API operations?](#section_sky_g2y_g2b)
-   [Why is the page view list different from the page speed list?](#section_vqb_h2y_g2b)
-   [TraceId is not found in the API logs, and as a result, the system cannot redirect me to the application monitoring page. Why?](#section_wxb_s5c_b6a)
-   [Why is the Source Map file error displayed when I am troubleshooting JS errors?](#section_aqp_vqy_svi)
-   [What are the differences between console setting and SetConfig?](#section_9i9_3y6_bdo)
-   [What is the relationship between resource consumption and charged traffic shown in the resource consumption chart?](#section_h09_obl_u88)
-   [How do I configure the environment and version in an SDK?](#section_qrc_oud_6hf)
-   [How do I view the version number of the configuration?](#section_gi2_19f_0ez)
-   [How do I view the time on page \(TP\) of a user for a page?](#section_ad7_a2u_1q5)
-   [What do I do if the ARMS configuration does not take effect?](#section_3cp_y4v_p7s)
-   [Why are JS errors on mini programs not reported?](#section_bq0_sla_43t)
-   [Can JS errors of console.error be listened to?](#section_00c_ong_nfg)
-   [In the Weex environment, why does a UID set in a mini program not take effect?](#section_i5k_9k6_l2z)
-   [How long can logs be stored?](#section_cnt_xx6_6ky)
-   [After I activate the expert edition, can I continue to use sites that are created during the trial period?](#section_w67_rn5_qtk)
-   [Why are the page views on the same page different among modules in the console?](#section_1y7_gr1_fcu)
-   [Why is the value of duration less than the value of connect download?](#section_m0j_njc_kh3)

## Why do I see asterisks \(\*\) in the names of some monitored pages or API operations?

The page statistics of Application Real-Time Monitoring Service \(ARMS\) browser monitoring are retrieved based on actual page URLs and calculated by dimension. The asterisks \(\*\) included in the names of monitored pages or API operations are not a part of the page URLs. The asterisks \(\*\) indicate the result of URL convergence. Therefore, a name that includes an asterisk \(\*\) is not a specific URL, but a group of similar URLs.

How URL convergence works

-   Problem: Variables make it difficult to monitor or analyze similar URLs.
-   Objective: Group similar URLs by replacing variables with asterisks \(\*\).
-   Solution: Use the Alibaba Cloud proprietary URL convergence algorithm to group similar URLs and decrease the number of URLs. This way, you can keep as much semantic information as possible and decrease the number of URLs. This is done in two steps:
    -   Aggregation: Aggregate similar URLs into one group.
    -   Variable identification: Extract the variables from the URLs in the same group, and replace the variables with asterisks \(\*\).

The following figure shows the URL convergence process.

Solution

For information about how to disable URL convergence, see [urlHelper](/intl.en-US/Browser monitoring/SDK reference.md).

[\[Back to the top\]](#sc_index)

## Why is the page view list different from the page speed list?

This is because your application is a single-page application \(SPA\), and the SPA auto-resolution is enabled. In the SPA application scenario, page views and page speed are measured by using the following methods:

-   Page views: When a hashchange event is triggered, the page views are automatically reported to record the page views of the page based on the hash value. Therefore, when you view the page view list of an SPA, you can view the exact page views of the hash pages.
-   Page speed: When the hash value of an SPA application changes, the page speed does not change. Therefore, the page speed is not recorded based on the hash. This way, unnecessary reports are avoided and page performance is clear.

[\[Back to the top\]](#sc_index)

## TraceId is not found in the API logs, and as a result, the system cannot redirect me to the application monitoring page. Why?

1.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the target application.

2.  In the left-side navigation pane, choose **Settings** \> **Application Settings**.

3.  On the Precondition tab, check whether **Associate with Application Monitoring** is selected for the ARMS agent configuration items. If Associate with Application Monitoring is not selected, select it. Then, connect the ARMS agent to the frontend application again.

    Check whether the TraceId parameter is generated in the API logs. If no TraceId is generated, perform the operations described in [this](#step_thx_955_m4j) section.

4.  Check whether the domain name used in your page request is the same as the domain name used in your API request. If the domain name used in your page request is different from the domain name in your API request, this is a cross-domain access. In this case, TraceId cannot be generated to prevent API request failure caused by cross-domain authentication.

    For information about how to solve this problem, see [Front-to-back tracing](/intl.en-US/Browser monitoring/Tutorials/Use the front-to-back tracing feature to diagnose causes of API errors.md).


[\[Back to the top\]](#sc_index)

## Why is the Source Map file error displayed when I am troubleshooting JS errors?

1.  Make sure that the file suffix is .js.map.

2.  Make sure that your account has the permissions to write data to ARMS. If your account has no write permissions, contact your administrator.


[\[Back to the top\]](#sc_index)

## What are the differences between console setting and SetConfig?

Console setting can accelerate only the generation of configuration code, and the generated code takes effect only after the code is published. However, modifications to SetConfig immediately take effect.

In addition, console setting is valid only when a project is connected to SDK code. After the project is connected to SDK code, you must use SetConfig to modify configurations.

[\[Back to the top\]](#sc_index)

## What is the relationship between resource consumption and charged traffic shown in the resource consumption chart?

The resource consumption chart shows the actual resource consumption. You can also configure only the actual consumption limit. For more information, see [设置消费限制](). You are charged for only part of the actual consumed traffic.

[\[Back to the top\]](#sc_index)

## How do I configure the environment and version in an SDK?

You can set the release parameter to compare versions. For more information, see [release](/intl.en-US/Browser monitoring/SDK reference.md). You can also set environment to distinguish different environments. For more information, see [.](/intl.en-US/Browser monitoring/SDK reference.md)

-   prod indicates an online environment.
-   gray indicates a phased-release environment.
-   pre indicates a staging environment.
-   daily indicates a daily environment.
-   local indicates a local environment.

[\[Back to the top\]](#sc_index)

## How do I view the version number of the configuration?

1.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the target application.

2.  In the left-side navigation pane, choose **Application** \> **View Details**.

    The version number of a log is displayed in the **Version Number** column in the **Log List** section.

3.  You can also filter logs by environment and version in the menu bar.**** You can filter logs only after PV logs are set with the version number.


[\[Back to the top\]](#sc_index)

## How do I view the time on page \(TP\) of a user for a page?

1.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the target application.

2.  In the left-side navigation pane, choose **Application** \> **Session Traces**.

3.  In the Session List section, find the target session and click its ID in the **Session ID** column. The Session Details page appears.

4.  Move the pointer over the **Timeline** area in the Visit Timeline column to view the time on page of a user for a page.


[\[Back to the top\]](#sc_index)

## How do I view the browser custom performance metrics of ARMS?

1.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the target application.

2.  In the left-side navigation pane, choose **Application** \> **Page Speed**.

3.  Custom performance metrics are displayed in the **Page Speed** section.


[\[Back to the top\]](#sc_index)

## What do I do if the ARMS configuration does not take effect?

The possible reason is that the browser cache is not updated. In the left-side navigation pane, click View Details. Switch to the latest version to view the trend chart. If the version number is not configured, you can configure the release parameter in the SDK. For more information, see [release](/intl.en-US/Browser monitoring/SDK reference.md). After the release parameter is configured, check whether the value that you specified is displayed as the latest version.

[\[Back to the top\]](#sc_index)

## Why are JS errors on mini programs not reported?

This may be because error messages are captured by try catch at the underlying layer of the mini programs, and the error messages fail to upload. You can try to manually report error messages. For more information, see [t152281.md\#section\_qe7\_9uq\_4a1](/intl.en-US/Browser monitoring/API reference.md).

[\[Back to the top\]](#sc_index)

## Can JS errors of console.error be listened to?

-   Yes, JS errors of console.error can be listened to. Web browsers report the error messages that meet the format of JS errors.
-   On the mini program side, you can try to manually report error messages. For more information, see [t152281.md\#section\_qe7\_9uq\_4a1](/intl.en-US/Browser monitoring/API reference.md).

[\[Back to the top\]](#sc_index)

## In the Weex environment, why does a UID set in a mini program not take effect?

-   If you have not called SetConfig, check whether you specified a UID during initialization configuration. If you did not specify a UID, specify one.
-   If you have called SetConfig, re-specify a UID in SetConfig.

[\[Back to the top\]](#sc_index)

## How long can logs be stored?

Logs can be stored for up to one month.

[\[Back to the top\]](#sc_index)

## After I activate the expert edition, can I continue to use sites that are created during the trial period?

-   No, you cannot continue to use the sites. Within 15 days after the trial period expires, the sites are suspended due to overdue payments. You can try to restart the application.
-   If the expert edition is not activated for the sites within 15 days after the trial period expires, the sites are deleted to save your computing and storage resources. Relevant resources are released and the data on the resources cannot be recovered.

[\[Back to the top\]](#sc_index)

## What version numbers are used by application edition and host edition of ARMS?

-   The application edition uses the version number of the current online project. You can configure the release parameter of the SDK to specify the version number of application edition. For more information, see [release](/intl.en-US/Browser monitoring/SDK reference.md).
-   The host edition uses the version number of the app where the current project resides. The version number of the host edition is automatically obtained by the SDK. The version of a hosted app cannot be resolved. Only versions of Taobao, Alipay, or WeChat are resolved.

[\[Back to the top\]](#sc_index)

## Why are the page views on the same page different among modules in the console?

On the Page Speed page, the number of page views is equal to the product of entries in the performance log and sample rate.

On the Page page under Dimensions, the number of page views is equal to the value shown in the PV log.

Automatically reported performance logs are reported only after pages are loaded. A performance log is reported each time the page is refreshed.

After the SPA mode is enabled, PV logs are reported every time routes are switched. In the SPA mode, the number of performance logs is less than the number of PV logs, which results in a large difference in the page views for different modules.

[\[Back to the top\]](#sc_index)

## Why is the value of duration less than the value of connect download?

The performance data loaded to ARMS resources is obtained from `performance.getEntriesByType('resource')`. The domain name of a third party ARMS resource must be the same as the domain name of the site of the current requested resource. By default, the value of 0 is obtained from `performance.getEntriesByType('resource')` for the following parameters of the performance data of cross-domain resources:

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

Some time properties may be inaccurate or abnormal because the preceding parameters are used in the calculation. For example, in `connect download：responseEnd - responseStart`, the value of duration is less than the value of connect download because the timestamp of responseStart is 0.

-   To solve this problem, for the CDN resources, you can configure the response header Timing-Allow-Origin to specify the time to obtain the resource time.
-   For third-party resources, we recommend that you take the value of the duration parameter as the major reference.

[\[Back to the top\]](#sc_index)

