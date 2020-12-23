# View applications

On the Applications page of the Tracing Analysis console, you can check key metrics of all monitored applications, including the request count and error count in the current day, and the health status. You can also set custom tags for your app and use tags to filter.

The applications page displays multiple key metrics of the monitored Application. The scores of these metrics are calculated based on the [APDEX](http://www.apdex.org/) Performance Index \(Application Performance Index\). It is an international standard for evaluating the performance of applications. The user experience of an application includes the following aspects:

-   - Satisfied \(0 to T\)
-   - Tolerating \(T to 4T\)
-   - Frustrated \(greater than 4T\)

The following formula is used to calculate the APDEX score:

```

     APDEX = (satisfactory number + tolerable number /2) /Total sample size 
   
```

Tracing analysis uses the average response time of an application as a calculation metric and defines T as 500 milliseconds.

## Procedure

Follow these steps to enter the application list page.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, choose **application list**, and select the target region at the top of the application list page.

    ![Page Applications](../images/p53837.png "Applications page")


## Sorting application

You can sort all apps in ascending or descending order by clicking the arrow next to the column headers:

-   **Health Score**
-   **Number of requests today**
-   **Number of errors today**
-   **Response time**

## Set application tags

After you set custom tags for an application, you can use these tags to filter the application.

1.  Place the pointer over the **label** column and click the pencil icon.

2.  In the manage account labels dialog box, enter custom labels in the **add labels** field and click **add**. Click one or more labels at the top, and click **OK**.

    ![Manage Tabs](../images/p53838.png)

    **Note:** If you delete an existing tag in the manage account tags dialog box, the app that previously added the tag will lose it.


## Filter applications by tag

In the **select tags** section, click one or more tags to filter all applications that have at least one tag.

![Example of Tags](../images/p53839.png)

**Related topics**  


[Before you begin](/intl.en-US/Preparations/Before you begin.md)

[Manage apps and tags](/intl.en-US/Console guide/Application management/Manage applications and tags.md)

