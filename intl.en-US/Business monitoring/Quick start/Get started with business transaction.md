# Get started with business transaction

The business transaction feature of Application Real-Time Monitoring Service \(ARMS\) allows you to define business requests in a visualized manner by using non-intrusive methods. This feature provides abundant performance metrics and diagnostic capabilities to meet specific business needs. After you enable the business transaction feature, you can create business transaction tasks and view business transaction data.

## Scenarios

Business transaction is applicable to the following scenarios:

-   Business personnel need to monitor their services, but the existing monitoring system cannot express business semantics.
-   The application system contains many business semantics, so O&M personnel must configure and monitor the traffic data for each service.
-   After a new service API is published, the API is unstable and causes exceptions or errors. Developers must analyze and find the problems for each call of the API.
-   A business leader wants to figure out dependencies of a service and optimize the service based on the dependencies to ensure the stability of the service.

The following figure shows a typical scenario where business transaction is used.

In the middle end-based architecture of an e-commerce company, the transaction center supports the order processing logic for all upper-layer services. The order processing logic varies greatly depending on the type of transactions. This leads to different business traces. The increasing complexity of business makes it more difficult to manually sort out the business traces of related transactions. Transactions of different commodities also vary. For example, the transactions of service A declined significantly today, but the transactions of business A make up a small portion of the overall transaction flow. Therefore, you cannot precisely identify problems based on the traffic change of overall orders alone.

In this scenario, you can use ARMS to configure commodity category-specific business transaction at the ordering portal of the transaction center. For example, after you group the women's clothing and home appliance categories, you can monitor the transactions of either category and quickly find out the transaction traces of a category.

![dg_business_typical_case](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8244674161/p94338.png)

## Limits

-   The business transaction feature can only monitor Java applications.
-   Only the ARMS agent V2.6.2 or later supports the business transaction feature.

## Procedure

![dg_business_workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8684574161/p103004.png)

**Note:** Scan the following QR code to join the DingTalk group.

![dg__business_dingding](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7037258061/p92785.png)

## Create a business transaction task

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Scenario-based Traces** \> **Application Metric**. In the top navigation bar of the Application Metric page, select a region.

3.  On the Application Metric page, click **Create Business monitoring** in the upper-right corner.

4.  On the New business monitoring page, set the parameters in the Basic information section.

    ![dg_business_create_btask](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1662758061/p94339.png)

    |Parameter|Description|Example|
    |---------|-----------|-------|
    |**Business Name**|Required. The name of the business transaction task.|Ordering portal|
    |**Entry application**|Required. The **Entry application** drop-down list displays all the Java applications that have the ARMS agent installed. After you select the required application, ARMS automatically detects the version number of the agent. **Note:** You can use the business transaction feature only after you upgrade the ARMS agent to a version later than 2.6.2. If the detected agent version is not later than 2.6.2, upgrade the agent first. For more information, see [Update the ARMS agent for Java applications](/intl.en-US/Application monitoring/Update the ARMS agent for Java applications.md).

|arms-k8s-demo|
    |**Service type**|The type of the service.    -   **HTTP entry**: suitable for scenarios where business traces are dyed based on HTTP traffic features.
    -   **Kubernetes Pod Metadata**: suitable for scenarios where business traces are dyed based on the environment features of Kubernetes pods. This parameter is displayed only when you set the **Entry application** parameter to Kubernetes.
|**HTTP entry**|
    |**Service name**|Required. The API name that is provided by the application. This parameter is displayed only when you set the **Service type** parameter to HTTP entry. ARMS automatically detects a list of APIs that are recently provided by this application based on the **entry application** you specify for your choices. If the recommended APIs do not meet your requirements, you can edit the APIs. The following four types of matching patterns of **Service name** are supported:

    -   **Equal**: matches the business API that uses the value of the **Service name** parameter as the API name. This pattern is the default matching pattern.
    -   **Start equal**: matches the business APIs whose names are prefixed with the value of the **Service name** parameter. If you need to monitor the business APIs that have the same prefix, select this pattern.
    -   **Contains**: matches the business APIs whose names contain the value of the **Service name** parameter. If your application provides a large number of business APIs, you can select this pattern to quickly monitor the business APIs that you need.
    -   **End =**: matches the business APIs whose names are suffixed with the value of the **Service name** parameter. This pattern is suitable for typical web frameworks that end with the .do and .action configurations.
    -   **Pattern matching**: matches dynamic URI paths and supports matching rules for Ant-style path patterns. This allows you to monitor and analyze the URIs of a specific type of patterns.
|**Equal** /api/buy|
    |**Filter rule relationships**|You can select **Meet the following rules at the same time** or **Meet the following rule**.|**Meet the following rules at the same time**|
    |**Filter rules**|Optional. Further filter the business APIs that you specify.    -   If the **Service type** parameter is set to HTTP entry: To specify **Filter rules**, you must specify a parameter to be matched \(**Parameter**, **Cookie**, **Method**, **PathVariable**, or **Header**\), a key value to be matched, a matching pattern \(**==**, **!=**, or **contains**\), and a threshold. Among the preceding information, the **PathVariable** option appears for the parameter to be matched only if you select **Pattern matching** for the **Service name** parameter and the input string includes braces \{\} as placeholders.

    -   If the **Service type** parameter is set to **Kubernetes Pod Metadata**: To specify **Filter rules**, you must specify a parameter to be matched \(**podLabel**, **podAnnotation**, **podName**, **podNamespace**, **podUID**, **podIp**, **nodeName**, **hostIp**, or **podServiceAccount**\), a matching pattern \(**==**, **!=**, or **contains**\), and a threshold.
You can set multiple filter rules. The logical relationship between multiple filter rules is determined by the **Filter rule relationships** parameter that you specify.

|Assume that your application provides the /api/buy?brand=\*\*\* URL and you want to monitor the API calls of brand=Alibaba. You can set the **Service name** parameter to **Equal** /api/buy and the **Filter rules** parameter to **Parameter** brand **==** Alibaba in the form.|
    |**Grouping Rules**|Required. Further group the business APIs that you specify.    -   If the **Service type** parameter is set to HTTP entry: To specify **Grouping Rules**, you must specify a parameter to be matched \(**Parameter**, **Cookie**, **Method**, **PathVariable**, or **Header**\) and a key value to be matched. Among the preceding information, the **PathVariable** option appears for the parameter to be matched only if you select **Pattern matching** for the **Service name** parameter and the input string includes braces \{\} as placeholders.
    -   If the **Service type** parameter is set to **Kubernetes Pod Metadata**: To specify **Grouping Rules**, you must specify a parameter to be matched \(**podLabel**, **podAnnotation**, **podName**, **podNamespace**, **podUID**, **podIp**, **nodeName**, **hostIp**, or **podServiceAccount**\).
You can set only one grouping rule. This rule can be set together with filter rules.

**Note:** The parameter specified in a grouping rule must be of an enumerated type. If the values of the parameter cannot be enumerated, the runtime memory usage will increase. The parameter that specifies the ID of a business model is a common example of a parameter whose values cannot be enumerated.

|Assume that your application provides the /api/buy?brand=\*\*\* URL and you want to monitor the API calls of the /api/buy URL by brand, you can set the **Service name** parameter to **Equal** /api/buy and the **Grouping Rules** parameter to **Parameter** brand.|

5.  Click **Advanced Settings**. In the Advanced Settings section, set related parameters. Then, click **Save**.

    ![Advanced Settings section](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1662758061/p190117.png)

    |Parameter|Description|
    |---------|-----------|
    |**Pass through to downstream**|Specifies whether to pass through dye labels in the traces to downstream application nodes.|
    |**Dump business parameters**|Specifies whether to record business parameters in the traces that have dye labels.|
    |**Whether full collection**|Specifies whether to collect all the traces that have dye labels.|


## View business transaction data

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Scenario-based Traces** \> **Application Metric**. In the top navigation bar of the Application Metric page, select a region.

3.  On the Application Metric page, click the entry of the business transaction task that you want to view. View the time series graphs of response time, requests, and errors of the application.

4.  On the Application Metric page, click the name of the business transaction task that you want to view.

5.  On the Business monitoring details page, view the call typology of the application. You can further filter the results by specifying the **Application name**, **API Name**, and **Business Parameters** parameters.

    ![dg_business_detail_overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1662758061/p94811.png)

    -   Click the SQL analysis tab to view the SQL request list. On this tab, you can discover which SQL request caused the long response time of a service. You can also click an interface snapshot of an SQL request to view the complete trace where the corresponding SQL request is executed.
    -   Click the Exception analysis tab to view the Java exceptions in the application. You can also click an interface snapshot of an exception to view the complete trace where the exceptional stack resides.
    -   Click the Error analysis tab to view errors and HTTP status codes of the application. You can also click a trace ID to view the information about a trace.
    -   Click the Upstream link or Downstream link tab to view the upstream or downstream APIs of the application and the performance metrics of API calls.
    -   Click the Interface snapshot tab to view the snapshots of API calls. This allows you to query the call history of an API based on the API name. You can also click a trace ID to view the information about a trace.

## Modify a business transaction task

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Scenario-based Traces** \> **Application Metric**. In the top navigation bar of the Application Metric page, select a region.

3.  On the Application Metric page, click the name of the business transaction task that you want to modify.

4.  In the left-side navigation pane, click Business monitoring settings.

5.  Click the Rule configuration tab. Modify the business transaction parameters and click **Save**.


## Disable business transaction

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar of the Applications page, select a region.

3.  On the Applications page, find the application for which you want to disable business transaction and click **Settings** in the **Actions** column.

4.  On the Application Settings page, click the **Custom Configuration** tab.

5.  In the **Scenario settings** section, turn off **Scenario switch**.

    ![sc_business_close_switch](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1662758061/p128882.png)


## Delete a business transaction task

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Scenario-based Traces** \> **Application Metric**. In the top navigation bar of the Application Metric page, select a region.

3.  On the Application Metric page, click the name of the business transaction task that you want to delete.

4.  In the left-side navigation pane, click Business monitoring settings. Click the **Delete** tab on the right side of the page.

5.  On the Delete tab, click **Delete**. In the Cue message, click **Determine**.

    **Note:** All data of the current business transaction task is deleted and cannot be restored.


