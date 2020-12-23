# Query trace

This paper introduces how to use multi-dimensional query function to query call chain.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **multidimensional query**.

    ![Page Trace Query](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5970368061/p53848.png)

3.  On the multidimensional query page, enter values for the following parameters as needed, and click **query**.

    -   Fixed query parameters

        -   TraceID
        -   Time consumed: greater than \(milliseconds\)
        -   Server Name
        -   RPC name
    -   Optional query parameters: Tag key

        Select the key of the Tag from the **Tag key** drop-down list and fill in the **Tag value** field with the value of the Tag. To add a Tag key or Tag value as a query condition, click the blue plus sign icon to the right of the field.

4.  In the search results, click the TraceID to go to the invocation trace tab and view the trace details.


-   To save the current parameter configurations, click **favorites**. The parameter configurations of favorite queries are displayed in **the favorite queries** section.
-   To delete all the query parameter configurations from your favorite, click **the favorite query** on the right side of **clear**.

**Related topics**  


[Before you begin](/intl.en-US/Preparations/Before you begin.md)

[View applications](/intl.en-US/Console guide/Application management/View applications.md)

