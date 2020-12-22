---
keyword: [business transaction, parse RESTful APIs]
---

# Use the business transaction feature to configure monitoring rules by parsing RESTful APIs

The business transaction feature allows you to parse RESTful APIs. When you configure business monitoring rules, you can parse HTTP methods and Uniform Resource Identifier \(URI\) paths.

Your application has access to the business transaction feature. For more information, see [Preparations]().

REST uses URIs to represent resources and uses HTTP methods such as GET, POST, PUT, and DELETE to describe operations on resources. RESTful APIs are APIs that follow the REST architectural style. As the REST architectural style gains popularity, more and more Internet applications are using RESTful APIs.

Compared with traditional APIs, RESTful APIs that separate operations from resources have the following differences:

-   HTTP Method

    Resources are the core of REST architectures. HTTP methods are used in REST architectures to perform operations on resources.

    -   GET: used to obtain resources.
    -   POST: used to create resources.
    -   PUT: used to update resources.
    -   DELETE: used to delete resources.
-   URI Path

    A resource is an Internet entity, such as a text, an image, or an audio or video file. A URI is a uniform resource identifier that can identify a resource uniquely. Therefore, you only need to present resource information in a reasonable way when you design URIs. The following list provides some typical URI designs:

    ```
    GET /orders: lists all orders.
    POST /orders: creates an order.
    GET /orders/ID: obtains information about a specific order.
    PUT /orders/ID: updates information of a specific order (all information of the order is provided).
    PATCH /orders/ID: updates information of a specific order (some information of the order is provided).
    DELETE /orders/ID: deletes a specific order.
    GET /orders/ID/goods: lists all products contained in a specific order.
    DELETE /zoos/ID/goods/ID: deletes a specific product contained in a specific order.
    ```


## Use the business transaction feature to configure monitoring rules by parsing HTTP methods

The business transaction feature allows you to parse HTTP methods such as GET, POST, PUT, DELETE, and PATCH. Perform the following steps to use the feature:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Scenario-based Traces** \> **Application Metric**.

3.  On the **Application Metric** page, click **Create Business monitoring** in the upper-right corner.

4.  On the New business monitoring page, set **Service type** to **HTTP entry** and select **Method** from the **Filter rules** or **Grouping Rules** drop-down list.

    **Note:**

    -   If you select **Method** from the **Filter rules** drop-down list, you can enter common HTTP methods such as GET, POST, PUT, DELETE, and PATCH \(all in uppercase\) in the **Threshold** field. This indicates that data is filtered based on the specified method.
    -   If you select **Method** from the **Grouping Rules** drop-down list, data displayed is grouped based on the specified method.
    ![pg_business_create_task_http](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8564758061/p127993.png)

    The following table describes the configurations of other parameters.

    |Parameter|Description|Example|
    |---------|-----------|-------|
    |**Business Name**|Required. The name of the business monitoring task.|Order portal|
    |**Entry application**|Required. The **Entry application** drop-down list displays all Java applications that have application agents installed. After you select an application, ARMS automatically detects the version of the application agent. **Note:** You can use the business monitoring feature only when you upgrade the application agent to version 2.6.2 or later. If the version of the application agent is earlier than 2.6.2, you must upgrade the application agent first. For more information, see [Preparations]().

|arms-k8s-demo|
    |**Service type**|The type of the service.    -   **HTTP entry**: suitable for scenarios where business links are colored based on HTTP traffic characteristics.
    -   **Kubernetes Pod Metadata**: suitable for scenarios where business links are colored based on the characteristics of the Kubernetes pod environment. This parameter is displayed only when you set **Entry application** to Kubernetes.
|**HTTP entry**|
    |**Service name**|Required. The name of the API provided by the application. This parameter is displayed only when you set **Service type** to HTTP entry. Based on the **entry application** that you select, ARMS automatically obtains a list of the latest APIs for the application. If the recommended APIs do not meet your requirements, you can modify the APIs. The **Service name** field supports the following matching modes:

    -   **Equal**: matches the APIs that are equal to the **Service name** value. By default, this matching mode is selected.
    -   **Start equal**: matches the APIs prefixed with the **Service name** value. You can select this mode if you want to monitor APIs that have the same prefix.
    -   **Contains**: matches the APIs that contain the **Service name** value. You can select this mode if your applications provides a large number of APIs.
    -   **End equal**: matches the APIs suffixed with the **Service name** value. This mode is suitable for web frameworks that use the .do and .action extensions.
    -   **Pattern matching**: matches dynamic URI path. This mode supports Ant-style path pattern matching rules and can be used to monitor and analyze URIs of a specified pattern.
|**Equal** /api/buy|
    |**Filter rule relationships**|You can select **Meet the following rules at the same time** or **Meet the following rule**.|**Meet the following rules at the same time**|
    |**Filter rules**|Optional. Used to further filter the APIs.    -   When you set **Service type** to HTTP entry, a **filtering rule** contains matching parameters \(**Parameter**, **Cookie**, **Method**, **PathVariable**, and **Header**\), matching key values, matching method \(**==**, **! =**, and **contains**\), and thresholds. Only if you set **Service name** to **Pattern matching** and the input string contains braces \(\{\}\), the **PathVariable** option is displayed.

    -   When you set **Service type** to **Kubernetes Pod Metadata**, a **filtering rule** contains matching parameters \(**podLabel**, **podAnnotation**, **podName**, **podNamespace**, **podUID**, **podIp**, **nodeName**, **hostIp**, and **podServiceAccount**\), matching method \(**==**, **! =**, and **contains**\), and thresholds.
You can set multiple filter rules. The logical relationship between multiple filter rules is determined by the **Filter rule relationships** value that you specify.

|If your application provides the /api/buy? brand=\*\*\* URL and you want to monitor the API calls of brand=Alibaba, you can set **Service name** to **Equal** /api/buy, and **Filtering rules** to **Parameter** brand **==** Alibaba.|
    |**Grouping Rules**|Required. Used to further group the APIs.    -   When you set **Service type** to HTTP entry, a **filtering rule** contains matching parameters \(**Parameter**, **Cookie**, **Method**, **PathVariable**, and **Header**\) and matching key values. Only if you set **Service name** to **Pattern matching** and the input string contains braces \(\{\}\), the **PathVariable** option is displayed.
    -   When you set **Service type** to **Kubernetes Pod Metadata**, a **filtering rule** contains matching parameters \(**podLabel**, **podAnnotation**, **podName**, **podNamespace**, **podUID**, **podIp**, **nodeName**, **hostIp**, and **podServiceAccount**\).
Only a single **grouping rule** can be added. This rule can be configured together with **filter rules**.

**Note:** The key values specified in a **grouping rule** must be of the enumerated type. If the key values cannot be enumerated, the runtime memory usage is increased. A common example of the key value that cannot be enumerated is the ID of a business model.

|If your application provides the /api/buy? brand=\*\*\* URL and you want to monitor the API calls of the /api/buy URL by brand, you can set **Service name** to **Equal** /api/buy, and **Grouping Rules** to **Parameter** brand.|

5.  Click **Save**.

6.  In the left-side navigation pane, choose **Scenario-based Traces** \> **Application Metric**. On the **Application Metric** page, click the name of the created monitoring task.

    On the Business monitoring details page, you can view the metrics of the monitoring task.

    ![sc_business_detail_metric](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1363468061/p127998.png)


## Use the business transaction feature to configure monitoring rules by parsing URI paths

For dynamic URI paths, you cannot match the URIs accurately by using the **Equal**, **Start equal**, **Contains**, or **End =** mode. Therefore, the **Pattern matching** mode is added to the business transaction feature to support Ant-Style path patterns for monitoring and analyzing URIs of a specific mode.

|Character|Description|Example|
|---------|-----------|-------|
|?|Matches any single character.|com/t? st.jsp: indicates that com/test.jsp, com/tast.jsp, or com/txst.jsp is matched, excluding com/tst.jsp.|
|\*|Matches none or multiple characters.|com/\*.jsp: indicates that files in the .jsp format under the com directory are matched.|
|\*\*|Matches none or multiple directories in a path.|com/\*\*/test.jsp: indicates that com/test.jsp, com/foo/test.jsp, or com/foo/bar/test.jsp is matched. This means that all test.jsp files under the com directory are matched.|
|\{example:\[a-z\]+\}|Matches characters that match the regular expression \[a-z\]+ and names the corresponding path variable as example. The colon \(:\) and the regular expression are optional.|com/\{filename:\\w+\}.jsp: indicates that com/test.jsp is matched and test is assigned to the path variable, which is filename in the example.|

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Scenario-based Traces** \> **Application Metric**.

3.  On the **Application Metric** page, click **Create Business monitoring** in the upper-right corner.

4.  On the New business monitoring page, select **Pattern matching** from the **Service name** drop-down list. In the **Service name** field, enter a string that matches an Ant-style path pattern.

    **Note:**

    -   When you select **Pattern matching** from the **Service name** drop-down list and enter a string that contains braces \(\{\}\), you can select **PathVariable** from the **Filter rules** and **Grouping Rules** drop-down lists.
    -   When you select **PathVariable** from the **Filter rules** drop-down list, the system parses the path variables and present them in a drop-down list format in the **key value** field. After you select a specific path variable and enter the path parameter in the **Threshold** field, data is filtered based on the specified path variable.
    -   When you select **PathVariable** from the **Grouping Rules** drop-down list, the system parses the path variables and presents them in a drop-down list format in the **key value** field. After you select a specific path variable, data displayed is grouped based on the specified path variable.
    -   For more information about configurations of other parameters, see the [parameter table](#table_6v9_nfa_z0p) in the preceding section.
    ![pg_business_create_task_uri](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8564758061/p128432.png)

5.  Click **Save**.

6.  In the left-side navigation pane, choose **Scenario-based Traces** \> **Application Metric**. On the **Application Metric** page, click the name of the created monitoring task.

    On the Business monitoring details page, you can view the metrics of the monitoring task.

    ![sc_business_detail_metric_uri](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5173468061/p128433.png)


**Related topics**  


[Preparations]()

[Get started with business transaction](/intl.en-US/Business Monitoring/Quick Start/Get started with business transaction.md)

