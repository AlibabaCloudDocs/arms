# Remote logs

The remote logs feature of the App Monitoring module can be used to pull, collect, and analyze exception logs of mobile terminals.

The remote logs feature mainly analyzes and locates issues after apps are published:

-   You can pull all exception logs from mobile terminals, bring back the scene, and quickly locate complex problems.
-   You can pull logs for exceptions of a single customer for troubleshooting.

## Prerequisites

[Create an app monitoring task](/intl.en-US/App monitoring/Create an app monitoring task.md)

## Procedure

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **App Monitoring**.
3.  On the App monitoring page, click the name of the app.
4.  In the top navigation bar, **Crash Analysis**, **Performance Analysis**, and **Remote Logs** buttons are displayed. Click each button and then you can select the subfeatures.

## Overview

The Overview page allows you to view the summary of exceptions of each terminal in a list. You can filter data by selecting values from the drop-down lists such as App Version, Time Range, Device, and Region.

![Remote Logs 1](../images/p77008.png)

## Task Management

Displays the list of tasks for pulling logs. You can filter data by selecting values from the **Originating Module****Status** drop-down lists.

-   **Originating Module**: provides options of **User Pull** and **Crash Analysis**. **User Pull** means that you pull logs in the console. **Crash Analysis** indicates that the Crash Analysis feature pulls logs.
-   **Status**: provides options of **Normal Tasks** and **Terminated Tasks**. The former refers to tasks where logs are obtained and the latter refers to tasks where logs are not obtained.

![Task Management](../images/p77011.png)

## Pulling Device List

Displays the list of the terminals that pull logs. You can filter data by selecting values from the UTDID, Originator, Update Time, and Status drop-down lists.

![Pulling Device List](../images/p77020.png)

