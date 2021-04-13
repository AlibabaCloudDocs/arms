# Consumption management

This topic describes how to view billing information,view resource consumption, set consumption limits, and enable or disable monitoring for all applications or a single application in the Application Real-Time Monitoring Service \(ARMS\) console. You can perform these operations to manage resource consumption.

## View billing information

-   View pay-as-you-go bills

    For pay-as-you-go services, you can view your bills by performing the following steps:

    1.  Log on to the [Billing Management console](https://usercenter2-intl.aliyun.com/).
    2.  In the left-side navigation pane, choose **Spending Summary** \> **Spending Summary**.
    3.  On the Bills page, click the **Bills** tab.
    4.  On the Bills tab, set filters such as **Billing Cycle** and **Order/Bill No.** and click **Search**. In the bill list, you can click the ![Filter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2615828161/p241635.png) icon on the right of Product Name, Product Detail, Subscription Type, Item, and Status and select options to further filter your bills.

        ![pg_consumer_detail](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1996316161/p86224.png)

-   View resource plan usage

    If you have purchased resource plans, you can view the usage of the resource plans by performing the following steps:

    1.  View the summary of resource plan usage.
        1.  Log on to the [Billing Management console](https://usercenter2-intl.aliyun.com/).
        2.  In the left-side navigation pane, choose **Resource Packages** \> **Overview**.
        3.  On the Overview tab, set filters such as **Effective Time** and **Resource Package Instance ID** and click **Search**. In the resource plan list, you can click the ![Filter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2615828161/p241635.png) icon on the right of Product Name, Resource Package Name, and Status and select options to further filter your resource plans.

            ![pg_resource_overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1996316161/p86230.png)

    2.  View the details of resource plan usage.
        1.  Log on to the [Billing Management console](https://usercenter2-intl.aliyun.com/).
        2.  In the left-side navigation pane, choose **Resource Packages** \> **Overview**.
        3.  Click the Details tab.
        4.  On the Details tab, set filters such as **Deducted Time**, **Resource Package Instance ID**, and **Deducted instance ID** and click **Search**. In the resource plan list, you can click the ![Filter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2615828161/p241635.png) icon on the right of Product Name, Resource Package Name, Usage Type, and Deducted Product and select options to further filter your resource plans.

## View resource consumption

The ARMS console provides the feature that allows Pro Edition users to view resource consumption. You can set filters to view the resources consumed by an individual application or all applications within a specific period of time.

|Sub-service|Resource definition|
|-----------|-------------------|
|Application monitoring|One resource is consumed when one agent runs for one hour.|
|Browser monitoring|One resource is consumed when a data reporting action is performed to report a PV, an API call, or custom information.|

-   View resource consumption of application monitoring
    1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
    2.  On the Applications page, click **Resource Consumption**.
    3.  In the **Resource Consumption** section, set filters such as **Application**, **Time Interval**, and **Time Range** and click **Query**.

        **Note:** In the following figure, the Y-axis indicates the number of consumed resources. One resource is consumed when one agent runs for one hour.

        ![sc_application_resource_consumption_statistics](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1996316161/p86252.png)

-   View resource consumption of browser monitoring
    1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/). In the left-side navigation pane, click **Browser Monitoring**.
    2.  On the Browser Monitoring page, click **Resource Consumption**.
    3.  In the **Resource Consumption** section, set filters such as **Application**, **Time Range**, **Report type**, and **Time Interval** and click **Query**.

        **Note:** In the following figure, the Y-axis indicates the number of consumed resources. One resource is consumed when a data reporting action is performed to report a PV, an API call, or custom information. You can move the pointer over the bar chart to view the specific number of resources.

        ![sc_frontend_resource_consumption_statistics](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0145828161/p86253.png)


## Set consumption limits

To prevent resources from being unexpectedly consumed, you can use the consumption limit feature to control daily consumption. After you set a daily consumption limit, ARMS continuously monitors your applications until the consumption limit is reached. Then, ARMS stops monitoring your applications, and the billing stops. ARMS resumes the monitoring at 00:00 the next day, and the billing continues.

-   Set a consumption limit for application monitoring
    1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
    2.  In the upper-right corner of the Applications page, choose **Settings** \> **Consumption Limit**.
    3.  In the Custom Limit dialog box, set your daily consumption limit and click **OK**.

        ![db_limited_consumption](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1996316161/p86276.png)

-   Set a consumption limit for browser monitoring
    1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/). In the left-side navigation pane, click **Browser Monitoring**.
    2.  In the upper-right corner of the Browser Monitoring page, choose **Settings** \> **Consumption Limit**.
    3.  In the Custom Limit dialog box, set your daily consumption limit and click **OK**.

        ![db_PV_limited_consumption](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1996316161/p86277.png)


## Start or stop monitoring all applications

If your applications do not need to be monitored all day, you can start and stop monitoring all applications based on your business requirements.

You need to select the sub-service that you want to start or stop.

-   Start or stop application monitoring
    1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
    2.  In the upper-right corner of the Applications page, choose **Settings** \> **Application Start/Stop Settings**.
    3.  In the Start/Stop All Applications dialog box, select an option and click **OK**.

        ![db_stop_all_applications](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1996316161/p86289.png)

-   Start or stop browser monitoring
    1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/). In the left-side navigation pane, click **Browser Monitoring**.
    2.  In the upper-right corner of the Browser Monitoring page, choose **Settings** \> **Application Start/Stop Settings**.
    3.  In the Start/Stop All Applications dialog box, select an option and click **OK**.

        ![Start/Stop All Applications-Browser Monitoring](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3052946161/p242226.png)


|Option|Description|
|------|-----------|
|Stop all applications \(Automatically start at 00:00 the next day\)|If you select this option, ARMS immediately stops monitoring all applications and resumes the monitoring at 00:00 the next day.|
|Stop all applications \(Won't automatically start the next day\)|If you select this option, ARMS immediately stops monitoring all applications but does not resume the monitoring the next day.|
|Remain running \(Automatically stop applications upon reaching consumption limit and won't automatically start the next day\)|If you select this option, ARMS continuously monitors your applications until the consumption limit is reached. Then, ARMS stops monitoring all applications but does not resume the monitoring the next day.**Note:** If you need to select the option **Remain running \(Automatically stop applications upon reaching consumption limit and won't automatically start the next day\)**, [set a consumption limit first](#section_ika_s65_olg). |

## Start or stop monitoring a single application

-   Start or stop application monitoring

    If you want to stop monitoring an application, you can disable the ARMS agent for this application. If you want to resume monitoring of the application by using the ARMS agent, you can enable the ARMS agent again for this application.

    1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
    2.  In the top navigation bar, select the region where the application resides.
    3.  On the Applications page, click the name of the application.
    4.  In the left-side navigation pane, click **Application Settings**.
    5.  On the Application Settings page, click the Custom Configuration tab. In the **Agent Switch Settings** section, turn on or off **Probe Master Switch** to enable or disable the ARMS agent. Then, ARMS starts or stops monitoring this application.

        ![sc_stop_a_application](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1996316161/p86331.png)

-   Stop browser monitoring

    If you want to disable browser monitoring for an application, delete the application from the monitored application list.

    **Note:** You cannot recover a deleted application. Exercise caution when you perform this operation. If you need to monitor the application again by using browser monitoring, you must enable browser monitoring for the application. For more information, see [Browser monitoring overview](/intl.en-US/Browser Monitoring/Quick start/Browser monitoring overview.md).

    1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/). In the left-side navigation pane, click **Browser Monitoring**.
    2.  In the application list, find the application and click **Settings** in the **Actions** column.
    3.  On the Application Settings page, click the Other Settings tab.
    4.  On the Other Settings tab, click **Delete Site**. In the Confirmation message, click **OK**. Then, ARMS stops monitoring this application.

        ![sc_delete_website](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1996316161/p86338.png)


