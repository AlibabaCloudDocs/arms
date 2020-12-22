# Get started with business transaction

The business transaction feature provided by ARMS allows you to define business requests in a visualized manner by using non-intrusive methods. This feature provides abundant business-specific performance metrics and diagnostic capabilities. After you enable business transaction, you can create business transaction tasks and view business transaction data.

## Scenarios

Business transaction is applicable to the following scenarios:

-   Business personnel want to monitor their services, but existing monitoring systems cannot express business semantics.
-   The application system contains many business semantics, so O&M personnel must quickly configure and monitor the traffic data for each service.
-   After a new service API is published, the API is unstable and causes exceptions or errors. Developers must analyze and find the problems for each call of the API.
-   A business leader wants to figure out dependencies of a service and optimize the service based on the dependencies to ensure the stability of the service.

The following figure shows a typical business transaction scenario.

In the middle end-based architecture of an e-commerce company, the transaction center supports the order processing logics for all upper-layer services. Different commodity transaction processing logics may vary greatly, resulting in completely different business links. As the complexity of business development increases, it is difficult to quickly find out the transaction links of related transactions by using the traditional manual method. Transactions of different commodities also vary. For example, the transactions of service A declined significantly today, but the transactions of business A make up a small portion of the overall transaction flow. Therefore, the traffic change of overall orders alone cannot precisely identify problems.

In this scenario, you can use ARMS to configure commodity category-specific business transaction at the ordering portal of the transaction center. For example, after you group the women's clothing and home appliance categories, on this page, you can monitor the transactions of either category and quickly find out the transaction links of a category.

## Limits

-   The business transaction feature only can monitor Java applications.
-   Only the ARMS agent V2.6.2 or later supports the business transaction feature.

## Create a business transaction task

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose Business Transaction \> Application Metric. In the top navigation bar of the Application Metric page, select the region.

3.  On the Application Metric page, click **Create Business Transaction** in the upper-right corner.

4.  In the Create Business Transaction dialog box, configure the parameters in the Basic Information section.

    ![dg_business_create_btask](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1662758061/p94339.png)

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

5.  Click **Advanced Settings**. In the Advanced Settings section, configure the parameters and click **Save**.

    ![Advanced Settings section](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1662758061/p190117.png)

    |Parameter|Description|
    |---------|-----------|
    |**Passthrough to Downstream**|Indicates whether to pass through packets to the downstream application nodes in the coloring marker call chain.|
    |**Dump Business Parameters**|Indicates whether to record business parameters in the coloring marker call chain.|
    |**Full Collection**|Indicates whether to collect all the coloring marker call chain.|


## View business transaction data

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose Business Transaction \> Application Metric. In the top navigation bar of the Application Metric page, select the region.

3.  On the Application Metric page, click the line of the task in the business transaction task list. View the time sequence charts of **Response Time**, **Requests**, and **Errors** of the application.

4.  On the Application Metric page, click the name of the task in the business transaction task list.

5.  On the Business transaction details page, view the detailed API call topology of the application. You can also filter the results by specifying **Application Name**,**API**, and **Condition**.

    ![dg_business_detail_overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1662758061/p94811.png)

    -   Click the SQL analysis tab to view the SQL request list. On this tab, you can discover which SQL request caused the long response time of a service. You can also click an **interface snapshot** of an SQL request to view the complete trace where the corresponding SQL statement is executed.
    -   Click the Exception analysis tab to view the Java exceptions caused by the application. You can also click an **interface snapshot** of an exception to view the complete trace where the exception stack is located.
    -   Click the Error analysis tab to view the number of errors and the HTTP status code data of the application. You can also click TraceId to view the trace information.
    -   Click the Upstream link or Downstream link tab to view the upstream or downstream APIs of the application and their call performance metrics.
    -   Click the Interface snapshot tab to view the snapshots of API calls. This allows you to query the call history of an API based on the API name. You can also click TraceId to view the trace information.

## Modify a business transaction task

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose Business Transaction \> Application Metric. In the top navigation bar of the Application Metric page, select the region.

3.  On the Application Metric page, click the name of the task in the business transaction task list.

4.  In the left-side navigation pane, click Business Transaction Settings.

5.  Click the Rule Configuration tab. Modify the business transaction parameters and then click **Save**.


## Disable business transaction

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose Application Monitoring \> Applications. In the top navigation bar of the Applications page, select the region.

3.  On the Applications page, find the application and click **Settings** in the **Actions** column.

4.  On the Settings page, click the Custom configuration tab.

5.  In the **Business Transaction** section, turn off the **Business transaction** switch.

    ![sc_business_close_switch](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1662758061/p128882.png)


## Delete a business transaction task

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose Business Transaction \> Application Metric. In the top navigation bar of the Application Metric page, select the region.

3.  On the Application Metric page, click the name of the task in the business transaction task list.

4.  In the left-side navigation pane, click Business Transaction Settings. On the page that appears, click **Delete**.

5.  On the Delete tab, click **Delete**. In the Prompt message, click **OK**.

    **Note:** All data of the current business transaction task is deleted and cannot be restored.


