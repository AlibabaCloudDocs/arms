# Performance analysis

The performance analysis feature in the Application Monitoring module of Application Real-time Monitoring Service \(ARMS\) can collect statistics and analyze the performance of apps.

## Prerequisites

[Create an app monitoring task](/intl.en-US/App monitoring/Create an app monitoring task.md)

## Procedure

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **App Monitoring**.
3.  On the **App Monitoring** page, click the name of the app.
4.  In the top navigation bar, **Crash Analysis**, **Performance Analysis**, and **Remote Logs** buttons are displayed. Click each button and then you can select the subfeatures.

## Overview

The Overview module allows you to view the summary of and analyze the startup speed and page performance of apps.

-   **Startup Speed**
    -   Collects the distribution of the startup time of each app and displays the results in a table.
    -   Analyzes the number of terminals and the trend of startup time of each app and displays the results in a chart.
    -   You can filter data by selecting values from the **App Version**, **Time**, **Device**, and **Region** drop-down lists.
-   **Page Performance**
    -   Click the **Loading Time - Average** tab. Then, the distribution of the loading time of each app page for each terminal is collected and the results are displayed in a table.
    -   Click the **Sliding Frame Rate - Average** tab. Then, the distribution of the average frame rate of each app page for each terminal is collected and the results are displayed in a table.
    -   You can filter data by selecting values from the **App Version**, **Time**, **Device**, and **Region** drop-down lists.

## Startup

The Startup module details the startup speed of each app.

-   **Top 100 Models**
    -   Displays the startup performance of apps on 100 different terminal models. You can sort the results by multiple dimensions and analyze the effects of these models on the startup speed of apps.
    -   You can filter data by selecting values from the **App Version** and **Time** drop-down lists.
-   **Carriers**
    -   Displays the startup performance of apps in different carrier environments. You can analyze the effects of carrier environments on the startup speed of apps.
    -   A long tail analysis is performed on carriers if it takes over 8,000ms to start apps.
    -   You can filter data by selecting values from the **App Version** and **Time** drop-down lists.

## Pages

The Pages module details the page performance of each app.

-   Click the **Loading Time** tab. Then, the distribution of the loading time of each app page is collected and the results are displayed in a table.

    Click the name of a page to go to the [Startup](#section_ujw_zrn_c2d) module of the page.

-   Click the **Sliding Frame Rate** tab. Then, the distribution of the average frame rate of each app page is collected and the results are displayed in a table.

    Click the name of a page to go to the [Startup](#section_ujw_zrn_c2d) module of the page.

-   You can filter data by selecting values from the **App Version**, **Time**, **Device**, and **Region** drop-down lists.

## Regions

-   Click the **Startup Time** tab. Then, the startup time of each app in each region is collected and the results are displayed in a chart.
-   Click the **Page Loading** tab. Then, the loading time of each app page in each region is collected and the results are displayed in a chart.
-   You can filter data by selecting values from the **App Version**, **Time**, **Device**, and **Region** drop-down lists.

