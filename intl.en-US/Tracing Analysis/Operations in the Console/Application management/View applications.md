# View applications

On the Applications page of the Tracing Analysis console, you can view key metrics of all monitored applications, including the numbers of requests and errors in the current day and the health status. You can also attach custom tags to applications and filter applications by tag.

The Applications page displays various key metrics of all monitored applications. The score for the health status of an application is measured by Application Performance Index \(APDEX\). For more information, see [APDEX](http://www.apdex.org/). APDEX is an internationally agreed standard that is used to measure the performance of applications. APDEX defines the following three levels of user satisfaction with application performance:

-   Satisfied \(0 to T\)
-   Tolerating \(T to 4T\)
-   Frustrated \(greater than 4T\)

The following formula is used to calculate the APDEX score:

```
APDEX score = (Number of satisfied samples + Number of tolerating samples/2)/Total number of samples
```

Tracing Analysis uses the average response time of an application in calculation, and defines T as 500 ms.

## Go to the Applications page

To go to the Applications page, perform the following steps:

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **Applications**. At the top of the Applications page, select a region as required.

    ![Page Applications](../images/p53837.png "Applications")


## Sort applications

You can click the up or down arrow next to one of the following columns to sort applications in ascending or descending order based on the specific column:

-   **Health Rate**
-   **Requests Today**
-   **Errors Today**
-   **Response Time**

## Attach tags to an application

You can attach custom tags to applications and filter applications by tag.

1.  Move the pointer over the application to which you want to attach tags, click the pencil icon in the **Labels** column, and then select Manage Labels. On the Labels tab, click Manage Application Labels.

2.  In the Manage Application Labels dialog box, click the **plus icon** and enter a custom tag. You can click the **plus icon** to create more custom tags. Then, click **Determine**.

    ![Manage Tabs](../images/p53838.png)

    **Note:** If you delete a tag in the Manage Application Labels dialog box, the tag is detached from all applications to which the tag is previously attached.


## Filter applications by tag

On the Applications page, you can click one or more tags in the **Select Label** section to find out all applications that have at least one of the selected tags.

![Example of Tags](../images/p53839.png)

**Related topics**  


[Overview](/intl.en-US/Before you begin/Overview.md)

[Manage applications and tags](/intl.en-US/Operations in the Console/Application management/Manage applications and tags.md)

