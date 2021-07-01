# View applications

On the Applications page of the Tracing Analysis console, you can view key metrics of all monitored applications, including the numbers of requests and errors in the current day and the health status. You can also attach custom tags to applications and filter applications by tag.

The Applications page displays various key metrics of all monitored applications. The score for the health status of an application is measured by Application Performance Index \(APDEX\). For more information, see [APDEX](http://www.apdex.org/). APDEX is an internationally agreed standard that is used to measure the performance of applications. APDEX defines the following three levels of user satisfaction with application performance:

-   Satisfied \(0 to T\)
-   Tolerating \(T to 4T\)
-   Frustrated \(greater than 4T\)

The following formula is used to calculate the APDEX score:

```
APDEX score = (Number of satisfied samples + Number of tolerating samples/2)/Number of total samples
```

Tracing Analysis uses the average response time of an application in calculation, and defines T as 500 ms.

## Go to the Applications page

To go to the Applications page, perform the following steps:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Tracing Analysis** \> **Applications**. At the top of the Applications page, select a region as required.


## Sort applications

You can click the up or down arrow next to one of the following columns to sort applications in ascending or descending order based on the specific column:

-   **Health Rate**
-   **Requests Today**
-   **Errors Today**
-   **Response Time**

## Attach tags to an application

You can attach custom tags to applications and filter applications by tag.

1.  Move the pointer over the application to which you want to attach tags, click the pencil icon in the **Labels** column, and then select **Manage Labels**.

    The **Labels** tab of the **Application Settings** page appears.

    ![Label settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8429015261/p269958.png)

2.  On the **Labels** tab, click **Manage Application Labels**.

3.  In the Manage Application Labels dialog box, click the ![Add Tag icon](../images/p269959.png) icon and enter a custom tag. Then, click **Determine**.

4.  In the Success message, click Determine. Then, click **Save** on the Labels tab.


## Filter applications by tag

On the Applications page, you can click one or more tags in the **Select Label** section to find out all applications that have at least one of the selected tags.

**Related topics**  


[Overview](/intl.en-US/Before You Begin/Overview.md)

[Manage applications and tags](/intl.en-US/Tutorials/Application management/Manage applications and tags.md)

