# How do I distinguish between the production environment and the test environment?

Tracing Analysis does not distinguish between the production environment and the test environment. However, you can distinguish between the environments based on the regions or tags.

## Distinguish between the environments based on the regions

To distinguish between the environments, you can select the current region or a region closest to you for the production environment, and select a remote region for the test environment. For example, you can select the China \(Beijing\) region for the production environment and the China \(Zhangjiakou\) region for the test environment.

-   Advantage: Resources from different regions are isolated. This helps you conveniently isolate different environments.
-   Disadvantage: Some Virtual Private Cloud \(VPC\) users of Alibaba Cloud cannot report data across regions over the internal network. In this case, we recommend that you distinguish between the environments based on the tags.

## Distinguish between the environments based on the tags

For applications in the same region, you can add a tag after the token in the endpoint, in the format of `_<tag>`. The following effects are achieved:

-   A pair of parentheses \(\) is automatically added after the application name. The content of `<tag>` is enclosed in the parentheses.
-   Tracing Analysis automatically creates the `<tag>` tag for the application. This tag can be used to filter applications.

Assume that the application name is `demo`. Add the `_prod` and `_test` tags after the token, as shown in the following figure.

![Token and Label](../images/p53868.png)

**Note:** On the Application Settings page, you can modify or delete a tag. For more information, see [Manage applications and tags](/intl.en-US/Operations in the Console/Application management/Manage applications and tags.md).

A token is the red characters in the endpoint that is displayed on the Cluster Configuration page of the Tracing Analysis console.

![Token Example](../images/p53870.png)

The following example shows how to add the `test` tag after the token:

-   Report data by using the Jaeger client

    -   The endpoint before you add the tag

        ```
        http://tracing-analysis-dc-hz.aliyuncs.com/adapt_abcefg123@abcefg123_abcefg456@abcefg456/api/traces
        ```

    -   The endpoint after you add the tag

        ```
        http://tracing-analysis-dc-hz.aliyuncs.com/adapt_abcefg123@abcefg123_abcefg456@abcefg456_test/api/traces
        ```

-   Report data by using the Zipkin client

    -   The endpoint before you add the tag

        ```
        http://tracing-analysis-dc-hz.aliyuncs.com/adapt_abcefg123@abcefg123_abcefg456@abcefg456/api/v2/spans
        ```

    -   The endpoint after you add the tag

        ```
        http://tracing-analysis-dc-hz.aliyuncs.com/adapt_abcefg123@abcefg123_abcefg456@abcefg456_test/api/v2/spans
        ```

-   Report data by using the SkyWalking client

    -   The agent.authentication parameter before you add the tag

        ```
        agent.authentication=abcefg123@abcefg123_abcefg456@abcefg456
        ```

    -   The agent.authentication parameter after you add the tag

        ```
        agent.authentication=abcefg123@abcefg123_abcefg456@abcefg456_test
        ```


[Overview](/intl.en-US/Before you begin/Overview.md)

[View applications](/intl.en-US/Operations in the Console/Application management/View applications.md)

[Manage applications and tags](/intl.en-US/Operations in the Console/Application management/Manage applications and tags.md)

