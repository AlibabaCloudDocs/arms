# QueryDataset（下钻数据集）

调用QueryDataset查询下钻数据集中的数据。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=QueryDataset&type=RPC&version=2019-08-08)

## 描述

QueryDataSet可用于查询ARMS下钻数据集中的数据。

**说明：** 关于下钻数据集和通用数据集的区别，请参见[通用维度与下钻维度](/cn.zh-CN/自定义监控/基本概念/通用维度与下钻维度.md)。

|API名称|Request|Response|
|-----|-------|--------|
|QueryDataSet|QueryDataSetRequest|QueryDataSetResponse|

## 请求参数

请求参数包含公共参数和业务参数。

**公共参数**

公共请求参数请参见[公共参数](/cn.zh-CN/API参考/公共参数.md)。

**业务参数**

阿里云将用户所有的请求参数封装在一个Request中，返回一个Response。QueryDataSetRequest包含以下字段：

|字段名称|字段类型|设置方法|字段含义|是否必选|备注|
|----|----|----|----|----|--|
|datasetId|Long|setDatasetId|数据集ID|是|请参见[如何获取datasetId](#obtain-datasetid)。|
|minTime|Long|setMinTime|查询数据的起始时间|是|-   单位：ms
-   取值为13位时间戳 |
|maxTime|Long|setMaxTime|查询数据的截止时间|是|-   单位：ms
-   取值为13位时间戳 |
|intervalInSec|Integer|setIntervalInSec|数据片的时间间隔|是|-   单位：s
-   取值范围：≥60 |
|measures|List\[String\]|setMesures|查询指标列表|否|列表最长支持3个元素。如果为空，则返回所有指标数据。|
|dimensions|List\[Dimension\]|setDimensions|查询维度列表|否|下钻数据集字段，dimensions为复合参数，列表最长支持3个元素。Dimension的定义见下方表格。|
|orderByKey|String|setOrderByKey|orderBy指标|否|N/A|
|limit|Integer|setLimit|限制的返回个数|否|N/A|
|reduceTail|Boolean|setReduceTail|是否把limit之外的数据合并到一起|否|N/A|
|securityToken|String|setSecurityToken|STS securityToken|否|采用RAM用户角色模式时需要设置该字段。详情参见[借助RAM角色实现跨云账号访问资源](/cn.zh-CN/访问控制/借助RAM角色实现跨云账号访问资源.md)。|

Dimensions复合字段说明

|字段名称|字段类型|设置方法|字段含义|备注|
|----|----|----|----|--|
|key|String|setKey|维度名称|如：区域|
|value|String|setValue|维度值|如：北京|
|type|String|setType|取值方式|分别为：STATIC、All和DISABLED|

-   当您想选择该维度下面的所有的维度值时，type设置为ALL，value为null。
-   当您想选择该维度下面的其中某个维度值时，type设置为STATIC（静态值），value为输入维度值。
-   当您不想选择该维度时候，可以直接忽略，或者将type设置为DISABLED。

**如何获取datasetId**

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。
2.  在左侧导航栏选择**自定义监控** \> **数据集管理**，在实例列表页面顶部选择目标地域。
3.  在数据集管理页签的数据集列表中，查看目标**数据集名称**对应的**数据集ID**，即可获取datasetId。

## 返回参数

返回值为JSON串形式返回，可通过`ARMSQueryDataSetResponse.getdata()`获取。

ARMSQueryDataSetResponse主要字段有：

|字段名称|字段含义|备注|
|----|----|--|
|dimensions|时序数据的维度值|当该维度选为ALL时，会有多个。|
|measures|数据点中的指标|N/A|
|resultSize|返回的所有数据点个数|N/A|
|dimData|多条时序数据|N/A|

## 完整使用示例

1.  在不选择维度情况下，查询所有数据的汇总信息。
2.  选择第一个维度，将维度值设为空字符串（“”），类型为ALL（全部）。结果返回按第一维度分组的数据。
3.  选择第一个维度，将维度值设为固定值，如hangzhou，类型为STATIC（固定值）。结果返回按第一维度的hangzhou数据。
4.  选择要查询的指标列表，返回结果只返回您指定的指标。

**相关文档**  


[公共参数](/cn.zh-CN/API参考/公共参数.md)

