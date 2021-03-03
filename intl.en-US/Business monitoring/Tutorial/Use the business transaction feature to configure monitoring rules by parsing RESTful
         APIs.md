---
keyword: [business transaction, parse RESTful APIs]
---

# Use the business transaction feature to configure monitoring rules by parsing RESTful APIs

The business transaction feature can parse RESTful APIs. When you configure monitoring rules, this feature can parse HTTP methods and Uniform Resource Identifier \(URI\) paths.

The application monitoring feature is enabled for your application. For more information, see [Overview](/intl.en-US/Application monitoring/Overview.md).

REST uses URIs to represent resources and uses HTTP methods such as GET, POST, PUT, and DELETE to describe operations on resources. RESTful APIs are APIs that follow the REST architectural style. As the REST architectural style becomes popular, more and more Internet applications apply RESTful APIs.

RESTful APIs can separate operations from resources. Compared with traditional APIs, RESTful APIs have the following features:

-   HTTP Method

    Resources are the core of REST architectures. REST architectures use HTTP methods to perform operations on resources.

    -   GET: obtains resources.
    -   POST: creates resources.
    -   PUT: updates resources.
    -   DELETE: deletes resources.
-   URI Path

    A resource is an entity on the Internet, such as a text file, an image, and an audio or video file. A URI is a uniform resource identifier that can uniquely identify a resource. Therefore, when you design URIs, you only need to present resource information in a reasonable way. The following list provides some typical URI designs:

    ```
    GET /orders: lists all orders.
    POST /orders: creates an order.
    GET /orders/ID: obtains information about a specific order.
    PUT /orders/ID: updates information about a specific order. All information about the order is provided.
    PATCH /orders/ID: updates information of a specific order. Some information about the order is provided.
    DELETE /orders/ID: deletes a specific order.
    GET /orders/ID/goods: lists all products contained in a specific order.
    DELETE /zoos/ID/goods/ID: deletes a specific product contained in a specific order.
    ```


## Use the business transaction feature to configure monitoring rules by parsing HTTP methods

The business transaction feature can parse HTTP methods such as GET, POST, PUT, DELETE, and PATCH. To use this feature, perform the following steps:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Scenario-based Traces** \> **Application Metric**.

3.  In the top navigation bar, select a region.

4.  On the **Application Metric** page, click **Create Business monitoring** in the upper-right corner.

5.  On the **New business monitoring** page, set the **Service type** parameter to **HTTP entry**and select **Method** from the **Filter rules** or **Grouping Rules** drop-down list.

    **Note:**

    -   If you select **Method** from the **Filter rules** drop-down list, you can enter common HTTP methods such as GET, POST, PUT, DELETE, and PATCH \(all in uppercase\) in the **Threshold** field. This indicates that data is filtered based on the specified method.
    -   If you select **Method** from the **Grouping Rules** drop-down list, data is displayed in groups based on the specified method.
    ![pg_business_create_task_http](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1148412161/p127993.png)

    The following table describes the configurations of other parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Business Name**|Required. The name of the business transaction task.|
    |**Entry application**|Required. The **Entry application** drop-down list displays all the Java applications that have the ARMS agent installed. After you select the required application, ARMS automatically detects the version number of the agent. **Note:** You can use the business transaction feature only after you upgrade the ARMS agent to a version later than 2.6.2. If the detected agent version is not later than 2.6.2, upgrade the agent first. For more information, see [Update the ARMS agent for Java applications](/intl.en-US/Application monitoring/Update the ARMS agent for Java applications.md). |
    |**Service type**|The type of the service. The value of **HTTP entry** is suitable for scenarios where business traces are dyed based on HTTP traffic features.|
    |**Service name**|Required. The API name that is provided by the application. This parameter is displayed only when you set the **Service type** parameter to HTTP entry. ARMS automatically detects a list of APIs that are recently provided by this application based on the **entry application** you specify for your choices. If the recommended APIs do not meet your requirements, you can edit the APIs. The following four types of matching patterns of **Service name** are supported:

    -   **Equal**: matches the business API that uses the value of the **Service name** parameter as the API name. This pattern is the default matching pattern.
    -   **Start equal**: matches the business APIs whose names are prefixed with the value of the **Service name** parameter. If you need to monitor the business APIs that have the same prefix, select this pattern.
    -   **Contains**: matches the business APIs whose names contain the value of the **Service name** parameter. If your application provides a large number of business APIs, you can select this pattern to quickly monitor the business APIs that you need.
    -   **End =**: matches the business APIs whose names are suffixed with the value of the **Service name** parameter. This pattern is suitable for typical web frameworks that end with the .do and .action configurations.
    -   **Pattern matching**: matches dynamic URI paths and supports matching rules for Ant-style path patterns. This allows you to monitor and analyze the URIs of a specific type of patterns. |
    |**Filter rule relationships**|You can select **Meet the following rules at the same time** or **Meet the following rule**.|
    |**Filter rules**|Optional. Further filter the business APIs that you specify.Assume that the **Service type** parameter is set to HTTP entry. To specify **Filter rules**, you must specify a parameter to be matched \(**Parameter**, **Cookie**, **Method**, **PathVariable**, or **Header**\), a key value to be matched, a matching pattern \(**==**, **!=**, or **contains**\), and a threshold. Among the preceding information, the **PathVariable** option appears for the parameter to be matched only if you select **Pattern matching** for the **Service name** parameter and the input string includes braces \{\} as placeholders.

You can set multiple filter rules. The logical relationship between multiple filter rules is determined by the **Filter rule relationships** parameter that you specify. |
    |**Grouping Rules**|Required. Further group the business APIs that you specify.Assume that the **Service type** parameter is set to HTTP entry. To specify **Grouping Rules**, you must specify a parameter to be matched \(**Parameter**, **Cookie**, **Method**, **PathVariable**, or **Header**\) and a key value to be matched. Among the preceding information, the **PathVariable** option appears for the parameter to be matched only if you select **Pattern matching** for the **Service name** parameter and the input string includes braces \{\} as placeholders.

You can set only one grouping rule. This rule can be set together with filter rules.

**Note:** The parameter specified in a grouping rule must be of an enumerated type. If the values of the parameter cannot be enumerated, the runtime memory usage will increase. The parameter that specifies the ID of a business model is a common example of a parameter whose values cannot be enumerated. |

6.  Click **Advanced Settings**. In the Advanced Settings section, set related parameters. Then, click **Save**.

    ![Advanced Settings section](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1662758061/p190117.png)

    |Parameter|Description|
    |---------|-----------|
    |**Pass through to downstream**|Specifies whether to pass through dye labels in the traces to downstream application nodes.|
    |**Dump business parameters**|Specifies whether to record business parameters in the traces that have dye labels.|
    |**Whether full collection**|Specifies whether to collect all the traces that have dye labels.|

    The business transaction task that you create appears on the **Application Metric** page.

7.  On the **Application Metric** page, click the name of the business transaction task that you create.

    On the **Business monitoring details** page, you can view the metrics of the business transaction task.


## Use the business transaction feature to configure monitoring rules by parsing URI paths

For dynamic URI paths, you cannot accurately match the URIs by using the **Equal**, **Start equal**, **Contains**, or **End =** matching pattern. Therefore, the **Pattern matching** option is added to the business transaction feature to support Ant-style path patterns for monitoring and analyzing URIs of a specific mode.

|Character|Description|Example|
|---------|-----------|-------|
|?|Matches a single character.|com/t?st.jsp: matches com/test.jsp, com/tast.jsp, or com/txst.jsp, excluding com/tst.jsp.|
|\*|Matches none or multiple characters.|com/\*.jsp: matches files in the .jsp format under the com directory.|
|\*\*|Matches none or multiple directories in a path.|com/\*\*/test.jsp: matches all test.jsp files under the com directory, such as com/test.jsp, com/foo/test.jsp, or com/foo/bar/test.jsp.|
|\{example:\[a-z\]+\}|Searches for a string that matches the regular expression \[a-z\]+ and assigns the string to the path variable example. The colon \(:\) and the regular expression are optional.|com/\{filename:\\w+\}.jsp: matches com/test.jsp. In this example, test is assigned to the path variable filename.|

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Scenario-based Traces** \> **Application Metric**.

3.  In the top navigation bar, select a region.

4.  On the **Application Metric** page, click **Create Business monitoring** in the upper-right corner.

5.  On the **New business monitoring** page, select **Pattern matching** from the **Service name** drop-down list. In the **Service name** field, enter a string that matches an Ant-style path pattern.

    **Note:**

    -   If you select **Pattern matching** from the **Service name** drop-down list and enter a string that contains braces \{\}, you can select **PathVariable** from the **Filter rules** and **Grouping Rules** drop-down lists.
    -   If you select **PathVariable** from the **Filter rules** drop-down list, the path variables appear in the **key value** drop-down list. If you select a specific path variable and enter the path parameter in the **Threshold** field, data is filtered based on the specified path variable.
    -   If you select **PathVariable** from the **Grouping Rules** drop-down list, the path variables appear in the **key value** drop-down list. If you select a specific path variable, data is displayed in groups based on the specified path variable.
    ![pg_business_create_task_uri](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8564758061/p128432.png)

    The following table describes the configurations of other parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Business Name**|Required. The name of the business transaction task.|
    |**Entry application**|Required. The **Entry application** drop-down list displays all the Java applications that have the ARMS agent installed. After you select the required application, ARMS automatically detects the version number of the agent. **Note:** You can use the business transaction feature only after you upgrade the ARMS agent to a version later than 2.6.2. If the detected agent version is not later than 2.6.2, upgrade the agent first. For more information, see [Update the ARMS agent for Java applications](/intl.en-US/Application monitoring/Update the ARMS agent for Java applications.md). |
    |**Service type**|The type of the service. The value of **HTTP entry** is suitable for scenarios where business traces are dyed based on HTTP traffic features.|
    |**Service name**|Required. The API name that is provided by the application. This parameter is displayed only when you set the **Service type** parameter to HTTP entry. ARMS automatically detects a list of APIs that are recently provided by this application based on the **entry application** you specify for your choices. If the recommended APIs do not meet your requirements, you can edit the APIs. The following four types of matching patterns of **Service name** are supported:

    -   **Equal**: matches the business API that uses the value of the **Service name** parameter as the API name. This pattern is the default matching pattern.
    -   **Start equal**: matches the business APIs whose names are prefixed with the value of the **Service name** parameter. If you need to monitor the business APIs that have the same prefix, select this pattern.
    -   **Contains**: matches the business APIs whose names contain the value of the **Service name** parameter. If your application provides a large number of business APIs, you can select this pattern to quickly monitor the business APIs that you need.
    -   **End =**: matches the business APIs whose names are suffixed with the value of the **Service name** parameter. This pattern is suitable for typical web frameworks that end with the .do and .action configurations.
    -   **Pattern matching**: matches dynamic URI paths and supports matching rules for Ant-style path patterns. This allows you to monitor and analyze the URIs of a specific type of patterns. |
    |**Filter rule relationships**|You can select **Meet the following rules at the same time** or **Meet the following rule**.|
    |**Filter rules**|Optional. Further filter the business APIs that you specify.Assume that the **Service type** parameter is set to HTTP entry. To specify **Filter rules**, you must specify a parameter to be matched \(**Parameter**, **Cookie**, **Method**, **PathVariable**, or **Header**\), a key value to be matched, a matching pattern \(**==**, **!=**, or **contains**\), and a threshold. Among the preceding information, the **PathVariable** option appears for the parameter to be matched only if you select **Pattern matching** for the **Service name** parameter and the input string includes braces \{\} as placeholders.

You can set multiple filter rules. The logical relationship between multiple filter rules is determined by the **Filter rule relationships** parameter that you specify. |
    |**Grouping Rules**|Required. Further group the business APIs that you specify.Assume that the **Service type** parameter is set to HTTP entry. To specify **Grouping Rules**, you must specify a parameter to be matched \(**Parameter**, **Cookie**, **Method**, **PathVariable**, or **Header**\) and a key value to be matched. Among the preceding information, the **PathVariable** option appears for the parameter to be matched only if you select **Pattern matching** for the **Service name** parameter and the input string includes braces \{\} as placeholders.

You can set only one grouping rule. This rule can be set together with filter rules.

**Note:** The parameter specified in a grouping rule must be of an enumerated type. If the values of the parameter cannot be enumerated, the runtime memory usage will increase. The parameter that specifies the ID of a business model is a common example of a parameter whose values cannot be enumerated. |

6.  Click **Advanced Settings**. In the Advanced Settings section, set related parameters. Then, click **Save**.

    ![Advanced Settings section](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1662758061/p190117.png)

    |Parameter|Description|
    |---------|-----------|
    |**Pass through to downstream**|Specifies whether to pass through dye labels in the traces to downstream application nodes.|
    |**Dump business parameters**|Specifies whether to record business parameters in the traces that have dye labels.|
    |**Whether full collection**|Specifies whether to collect all the traces that have dye labels.|

    The business transaction task that you create appears on the **Application Metric** page.

7.  On the **Application Metric** page, click the name of the business transaction task that you create.

    On the **Business monitoring details** page, you can view the metrics of the business transaction task.


**Related topics**  


[Preparations](/intl.en-US/Business monitoring/Monitor Java applications/Preparations.md)

[Get started with business transaction](/intl.en-US/Business monitoring/Quick start/Get started with business transaction.md)

