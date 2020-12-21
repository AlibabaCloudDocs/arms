# 15-day free trial of ARMS

Application Real-Time Monitoring Service \(ARMS\) provides a free trial for application monitoring, browser monitoring, and Prometheus Service. This topic describes the usage notes for the Trial Edition of ARMS.

For more information about the comparison between the Trial Edition and Pro Edition, see [Edition comparison](/intl.en-US/Pricing/Edition comparison.md).

-   Trial Edition of application monitoring: The trial is valid until 00:00 on the 15th day after ARMS is activated. During this period, ARMS provides a free quota of 240 hours for agents per day. For example, 10 agents are deployed and each agent can run for 24 hours free of charge.

    **Note:** Each agent can monitor one application, such as a Tomcat instance or a Java process.

-   Trial Edition of browser monitoring: The trial is valid until 00:00 on the 15th day after ARMS is activated. During the trial, ARMS provides a free quota of 20,000 reports per day.
-   Trial Edition of Prometheus Service: The trial is valid until 00:00 on the 15th day after ARMS is activated. During the trial, ARMS provides you with free quota of 2,000,000 reports for custom metrics per day.

## Usage notes

-   Application monitoring: The traffic is calculated based on the total length of time that all applications are online. Bills are settled on a daily basis. The monitoring data of the application monitoring feature is cached for 60 days by default.
-   Browser monitoring: Billable items include the number of page view \(PV\) reports, the number of API reports, and the number of custom reports. Bills are settled on a daily basis. The basic unit is 1,000. If the number of reports is not a multiple of 1,000, the number of reports is rounded up to the nearest multiple of 1,000. For example, if the number of reports is 1,350, you are billed for 2,000 reports. The monitoring data of the browser monitoring feature is cached for 30 days by default.
-   Traffic of daily reports = Daily PV reports + \(Daily API reports - 500,000\) × 0.1 + Daily custom reports
-   Prometheus Service: Basic metrics and custom metrics are supported. The monitoring data of the Prometheus Service is cached for 15 days by default.
-   If you do not activate the Pro Edition, no fees are incurred, and the service is suspended when the quota is used up. The monitoring service can be manually or automatically enabled the next day. Disabling or restarting the monitoring service does not affect your applications.
-   In the Trial Edition, the free quota is reset at 00:00 every day and is valid only within 24 hours.

