# Query traces

This topic shows you how to use the multi-dimensional query feature to query traces.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **Advanced Query**.

    ![Page Trace Query](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4613239061/p53848.png)

3.  On the Advanced Query page, set the following parameters as needed and click **Search**:

    -   Required query parameters

        -   TraceId
        -   Takes Longer Than \(ms\)
        -   Application Name
        -   Span Name
    -   Optional query parameter: Tag Key

        Select the key of a tag from the **Tag Key** drop-down list. Then, select the value of the tag from the **Tag Value** drop-down list. To add more tag keys and tag values as query conditions, click the blue plus sign to the right of the Tag Value drop-down list.

4.  In the search results, click the ID of a trace to go to the Traces tab and view the trace details.


-   To save the current configuration of query parameters, click **Favorite** and set an alias.
-   To delete the favorite configuration of query parameters, click the Delete icon to the right of the alias.

**Related topics**  


[Overview](/intl.en-US/Before you begin/Overview.md)

[View applications](/intl.en-US/Operations in the Console/Application management/View applications.md)

