---
keyword: [业务监控, Restful API解析]
---

# 业务监控通过支持解析RESTful API配置监控规则

业务监控支持对RESTful API的解析，配置业务监控规则时，支持HTTP Method解析和URI Path解析。

您的应用已接入应用监控，详情请参见[应用监控概述](/intl.zh-CN/应用监控/应用监控概述.md)。

REST是用URI表示资源，用HTTP方法（GET、POST、PUT和DELETE）描述对资源的操作，而RESTful API就是REST风格的API。随着REST架构的流行，越来越多的互联网应用开始采用RESTful API这种比较成熟的API设计理念。

相对于传统API设计，行为和资源分离的RESTful API带来了以下变化：

-   HTTP Method

    REST架构的核心是资源，并且通过HTTP动词即HTTP Method来实现资源的状态转换：

    -   GET：用来获取资源
    -   POST：用来新建资源
    -   PUT：用来更新资源
    -   DELETE：用来删除资源
-   URI Path

    资源是网络上的一个实体，例如文本、图片和音视频等。而URI是统一资源标识符，可以唯一标识一个资源。因此，设计URI时，仅需将资源通过合理方式暴露出来即可。一些典型的URI设计如下：

    ```
    GET /orders：列出所有订单
    POST /orders：新建一个订单
    GET /orders/ID：获取某个指定订单的信息
    PUT /orders/ID：更新某个指定订单的信息（提供该订单的全部信息）
    PATCH /orders/ID：更新某个指定订单的信息（提供该订单的部分信息）
    DELETE /orders/ID：删除某个订单
    GET /orders/ID/goods：列出某个指定订单的所有商品
    DELETE /zoos/ID/goods/ID：删除某个指定订单的指定商品
    ```


## 业务监控通过支持HTTP Method解析配置监控规则

业务监控支持对HTTP Method的解析能力，可解析常用的GET、POST、PUT、DELETE和PATCH等HTTP Method。使用方式如下：

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**业务监控** \> **自定义**。

3.  在**自定义**页面的右上角单击**创建业务监控**。

4.  在新建业务监控页面，**服务类型**选择**HTTP入口**，从**过滤规则**或**分组规则**下拉列表中选择**Method**。

    **说明：**

    -   **过滤规则**选择**Method**时，**阈值**文本框允许输入GET、POST、PUT、DELETE和PATCH（需大写）等常见的HTTP Method，表示按照指定Method进行过滤。
    -   **分组规则**选择**Method**时，表示按照指定Method分组展示监控数据。
    ![pg_business_create_task_http](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9067197951/p127993.png)

    其他参数配置请参见以下参数列表。

    |参数|描述|示例|
    |--|--|--|
    |**业务名称**|业务监控任务的名称，必填。|下单入口。|
    |**入口应用**|**入口应用**列表显示所有已安装应用监控探针的Java应用，必选。选中所需应用后，ARMS自动检测其应用探针的版本号。 **说明：** 应用探针升级至2.6.2+版本才能使用业务监控功能，若检测到探针版本非2.6.2+时，请您先升级探针，具体操作，请参见[升级探针](/intl.zh-CN/应用监控/升级探针.md)。

|arms-k8s-demo。|
    |**服务类型**|设置服务类型。    -   **HTTP入口**：适用于按HTTP流量特征进行业务链路染色场景。
    -   **Kubernete Pod Metadata**： 适用于按照K8s Pod环境特征进行业务链路染色场景。当选择的**入口应用**为K8s部署时才会显示此参数。
|**HTTP入口**。|
    |**服务名称**|即应用提供的接口名称，必填。仅当**服务器类型**设置为HTTP入口时才会显示此参数。ARMS会根据您设置的**入口应用**自动匹配出该应用最近提供的接口列表以便您选择。如果推荐的接口不满足需求时，您也可以编辑修改。 **服务名称**的匹配模式支持以下4种类型：

    -   **等于**：完全匹配**服务名称**的业务接口，默认匹配模式。
    -   **开始等于**：匹配以**服务名称**为前缀的业务接口。若您需要监控具备相同前缀的业务接口时，可选择此模式。
    -   **包含**：匹配包含**服务名称**的业务接口。若您的应用提供大量业务接口时，可选择此模式快速监控您所需的业务接口。
    -   **结束等于**：匹配以**服务名称**为后缀的业务接口。以“.do”和“.action”配置结尾的典型Web框架比较适合使用此模式。
    -   **模式匹配**：匹配动态URI Path，支持Ant-style路径模式匹配规则，可实现对某一类模式的URI的监控及分析。
|**等于** /api/buy。|
    |**过滤规则关系**|可以选择**同时满足下述规则**或**满足下述一条规则**。|**同时满足下述规则**。|
    |**过滤规则**|对配置的业务接口进一步筛选过滤，选填。    -   当**服务器类型**设置为HTTP入口时：**过滤规则**需要设置匹配参数（**Parameter**、**Cookie**、**Method**、**PathVariable**和**Header**）、匹配Key值、匹配方式（**==**、**!=**和**contains**）和阈值，其中，只有在**服务名称**选择**模式匹配**时，且输入的字符串中包含占位符大括号（\{\}），则匹配参数会出现**PathVariable**选项。

    -   当**服务器类型**设置为**Kubernete Pod Metadata**时：**过滤规则**需要设置匹配参数（**podLabel**、**podAnnotation**、**podName**、**podNamespace**、**podUID**、**podIp**、**nodeName**、**hostIp**和**podServiceAccount**）、匹配方式（**==**、**!=**和**contains**）和阈值。
支持设置多条过滤规则，多条过滤规则之间逻辑关系由您设置的**过滤规则关系**决定。

|假设您的应用提供 /api/buy?brand=\*\*\* 这样的URL，您希望监控brand=Alibaba的接口调用时，可在表单中设置**服务名称****等于** /api/buy，**过滤规则**为**Parameter** brand **==** Alibaba。|
    |**分组规则**|对配置的业务接口进一步细化统计并分组，必填。    -   当**服务器类型**设置为HTTP入口时：**分组规则**需要设置匹配参数（**Parameter**、**Cookie**、**Method**、**PathVariable**和**Header**）和匹配Key值，其中，只有在**服务名称**选择**模式匹配**时，且输入的字符串中包含占位符大括号（\{\}），则匹配参数会出现**PathVariable**选项。
    -   当**服务器类型**设置为**Kubernete Pod Metadata**时：**分组规则**需要设置匹配参数（**podLabel**、**podAnnotation**、**podName**、**podNamespace**、**podUID**、**podIp**、**nodeName**、**hostIp**和**podServiceAccount**）。
**分组规则**仅支持设置单条规则，可与**过滤规则**同时设置。

**说明：** **分组规则**设置的参数需是枚举类型。如果参数无法枚举，则运行时会增加应用内存占用率。常见的无法枚举的字段例如某个业务模型的ID字段。

|假设您的应用提供 /api/buy?brand=\*\*\* 这样的URL，您希望对接口 /api/buy的调用按brand分别统计时，可在表单中设置**服务名称****等于** /api/buy，**分组规则**为**Parameter** brand。|

5.  配置完成后，单击**保存**。

6.  在左侧导航栏单击**业务监控** \> **自定义**，单然后在**自定义**页面单击刚才创建的业务监控名称。

    在业务监控详情页面，查看此监控任务对应的指标数据。

    ![sc_business_detail_metric](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9067197951/p127998.png)


## 业务监控通过支持URI Path解析配置监控规则

对于动态URI Path，使用**等于**、**开始等于**、**包含**和**结束等于**匹配模式都无法准确匹配。因此，业务监控新增**模式匹配**匹配模式，可支持Ant-style路径模式匹配规则，帮助您实现对某一类模式的URI的监控及分析。

|字符|描述|示例|
|--|--|--|
|?|匹配任意单个字符|com/t?st.jsp：表示匹配com/test.jsp、com/tast.jsp或com/txst.jsp， 但不包括com/tst.jsp。|
|\*|匹配任意零个或多个字符|com/\*.jsp：表示匹配com目录下的.jsp文件。|
|\*\*|匹配路径中的零个或多个目录|com/\*\*/test.jsp：表示匹配com/test.jsp、com/foo/test.jsp或com/foo/bar/test.jsp，即com目录下任一层级的test.jsp文件。|
|\{example:\[a-z\]+\}|匹配符合正则表达式\[a-z\]+的字符，并将对应的路径变量命名为example。英文冒号（:）及正则表达式为非必填项。|com/\{filename:\\w+\}.jsp：表示匹配com/test.jsp，并将test赋值给路径变量filename。|

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**业务监控** \> **自定义**。

3.  在**自定义**页面的右上角单击**创建业务监控**。

4.  在新建业务监控页面，**服务名称**选择**模式匹配**，在**服务名称**的文本框中输入Ant-style路径模式的字符串。

    **说明：**

    -   **服务名称**选择**模式匹配**时，如果输入的字符串中包含占位符大括号（\{\}），则**过滤规则**和**分组规则**可以选择配置路径变量，即**PathVariable**。
    -   **过滤规则**选择**PathVariable**时，**key值**下拉列表会自动识别出路径变量，选择所需路径变量并在**阈值**文本框输入路径参数后，则可以按照指定的路径变量进行过滤。
    -   **分组规则**选择**PathVariable**时，**key值**下拉列表会自动识别出路径变量，选择所需路径变量后，则可以按照指定的路径变量分组展示监控数据。
    -   其他参数配置请参见以上[新建业务监控任务参数列表](#table_6v9_nfa_z0p)。
    ![pg_business_create_task_uri](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9067197951/p128432.png)

5.  配置完成后，单击**保存**。

6.  在左侧导航栏单击**业务监控** \> **自定义**，然后在**自定义**页面单击刚才创建的业务监控名称。

    在业务监控详情页面，查看此监控任务对应的指标数据。

    ![sc_business_detail_metric_uri](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9067197951/p128433.png)


**相关文档**  


[开始使用业务监控](/intl.zh-CN/业务监控/快速入门/开始使用业务监控.md)

