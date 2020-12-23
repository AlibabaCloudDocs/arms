# How are production environments and test environments distinguished?

Tracing Analysis does not distinguish between the production environment and the Test environment. However, you can use regions or labels to distinguish between environments.

## Use regions to distinguish environments

You can use the current region or the nearest region for the production environment, and use the nearest region for the Test environment. For example, select China \(Beijing\) for the production environment and China \(Zhangjiakou\) for the Test environment.

-   Advantage: resources in different regions are isolated from each other, which helps to easily isolate various environments.
-   Disadvantages: users of Alibaba Cloud VPCs cannot report data across regions through intranet. If this is the case, it is recommended to use the label to distinguish the environment.

## Use labels to distinguish environments

If your application resides in the same region, add a tag in the Token field to the `_format <label> of`the Token.

-   The name of the application is automatically enclosed in a pair of parentheses \(\). The `<label> name`is enclosed in parentheses \(\).
-   Tracing Analysis automatically creates a `label for the application. This label can be used <label> to`filter applications.

Assume that an application name is `demo` and the tags `_prod` and `_test` are added to the end of the Token parameter. Then, after the data is successfully reported, the following results are displayed:

![Token and Label](../images/p53868.png)

**Note:** You can modify or delete tags on the application management page. For more information, see [Manage apps and tags](/intl.en-US/Console guide/Application management/Manage applications and tags.md).

A Token is a red character in the access point information displayed on the overview page of the Tracing Analysis console.

![Token Example](../images/p53870.png)

The following example shows how to add the `test` tag to the access Token field:

-   When you use the Jaeger client to report data

    -   Before adding a tag

        ```
        
                 http://tracing-analysis-dc-hz.aliyuncs.com/adapt_abcefg123@abcefg123_abcefg456@abcefg456/api/traces 
               
        ```

    -   After adding tags

        ```
        
                 http://tracing-analysis-dc-hz.aliyuncs.com/adapt_abcefg123@abcefg123_abcefg456@abcefg456_test/api/traces 
               
        ```

-   When using the Zipkin client to report data

    -   Before adding a tag

        ```
        
                 http://tracing-analysis-dc-hz.aliyuncs.com/adapt_abcefg123@abcefg123_abcefg456@abcefg456/api/v2/spans 
               
        ```

    -   After adding tags

        ```
        
                 http://tracing-analysis-dc-hz.aliyuncs.com/adapt_abcefg123@abcefg123_abcefg456@abcefg456_test/api/v2/spans 
               
        ```

-   When using the SkyWalking client to report data

    -   agent.authentication field before adding tags

        ```
        
                 agent.authentication=abcefg123@abcefg123_abcefg456@abcefg456 
               
        ```

    -   agent.authentication field after the tag is added

        ```
        
                 agent.authentication=abcefg123@abcefg123_abcefg456@abcefg456_test 
               
        ```


[Before you begin](/intl.en-US/Preparations/Before you begin.md)

[View applications](/intl.en-US/Console guide/Application management/View applications.md)

[Manage apps and tags](/intl.en-US/Console guide/Application management/Manage applications and tags.md)

