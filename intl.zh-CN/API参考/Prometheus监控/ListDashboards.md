# ListDashboards

调用ListDashboards接口获取集群的Grafana大盘的列表。

********

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=ListDashboards&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListDashboards|系统规定参数，取值为`ListDashboards`。 |
|ClusterId|String|是|cc7a37ee31aea4ed1a059eff8034b\*\*\*\*|阿里云容器服务Kubernetes版的Kubernetes集群的ID。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|ClusterType|String|否|Node|集群类型。虚拟集群可通过集群类型查询大盘列表。 |
|Title|String|否|ApiServer|指定大盘标题。大盘标题可能会修改，建议使用dashboardName查询。 |
|Product|String|否|xxxx|云产品Code。 |
|RecreateSwitch|Boolean|否|false|创建/查询虚拟集群开关参数，可以对老数据兼容控制。 |
|DashboardName|String|否|k8s-node-overview|大盘唯一名称，可筛选查询指定名称的大盘。相对于title参数，title可能会发生变化，name不会。并且支持指定多个name，以逗号分割，例如：k8s-event,k8s-overview。同一个大盘名称会有多个版本，如果要指定版本，可以在name后面增加版本信息，例如：k8s-event:v1,k8s-overview:latest。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DashboardVos|Array of DashboardVos| |Grafana大盘信息。 |
|DashboardType|String|Node|大盘类型，作用与exporter一致，但是字段含义更明确。 |
|Exporter|String|Nginx|Exporter接入源的类型，包括：

 -   Prometheus
-   Node
-   GPU
-   Redis
-   Mysql
-   Kafka
-   NginxV2
-   Nginx
-   Zk
-   Mongo
-   RabbitMq
-   PostgreSQL
-   Kubernetes
-   Client Library
-   ElasticSearch |
|Id|String|1100\*\*|Grafana大盘ID，仅在安装Grafana大盘时是唯一的。 |
|IsArmsExporter|Boolean|false|是否属于ARMS提供的Exporter：

 -   `true`：是ARMS提供的Exporter
-   `false`：不是ARMS提供的Exporter |
|Kind|String|BASIC|大盘种类，为BASIC、THIRD、LIMIT、CUSTOM的其中一种。 |
|Name|String|k8s-node-overview|大盘名称，与title不同，不会修改 |
|NeedUpdate|Boolean|false|大盘是否有新版本可以升级。 |
|Tags|List|\["arms-k8s","ccc8ce1fe0c9543629e39ee657e34\*\*\*\*"\]|Grafana大盘标签。 |
|Time|String|1590136924|Grafana大盘创建时间的时间戳。 |
|Title|String|ApiServer|Grafana大盘名称。 |
|Type|String|dash-db|Grafana大盘类型，包括：

 -   `dash-db`：大盘
-   `dash-folder`：文件夹（可包含大盘） |
|Uid|String|1131971649496228-\*\*\*\*\*-59|安装多个Grafana大盘时的大盘唯一标识符，是展示在页面上的唯一业务ID。 |
|Url|String|http://g.console.aliyun.com/d/1131971649496228-\*\*\*\*\*-59/ApiServer?orgId=3\*\*&refresh=60s|Grafana大盘的完整URL。 |
|Version|String|v2|大盘版本，与name形成唯一键，确定一个大盘。 |
|RequestId|String|2A0CEDF1-06FE-44AC-8E21-21A5BE65\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListDashboards
&ClusterId=cc7a37ee31aea4ed1a059eff8034b****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListDashboardsResponse>
	  <DashboardVos>
		    <Uid>1131971649496228-*****-59</Uid>
		    <Type>dash-db</Type>
		    <Title>ApiServer</Title>
		    <Time></Time>
		    <Id>1100**</Id>
		    <Exporter>Nginx</Exporter>
		    <Url>http://g.console.aliyun.com/d/1131971649496228-*****-59/ApiServer?orgId=3**&amp;refresh=60s</Url>
		    <Tags>arms-prom</Tags>
		    <Tags>ce1887373d0204999835904236961a83d</Tags>
		    <Tags>api-server</Tags>
		    <IsArmsExporter>true</IsArmsExporter>
	  </DashboardVos>
	  <RequestId>2A0CEDF1-06FE-44AC-8E21-21A5BE65****</RequestId>
</ListDashboardsResponse>
```

`JSON`格式

```
{"DashboardVos":[{"Uid":"1131971649496228-*****-59","Type":"dash-db","NeedUpdate":"false","Version":"v2","Kind":"BASIC","Title":"ApiServer","Time":"1590136924","Id":"1100**","DashboardType":"Node","Exporter":"Nginx","Url":"http://g.console.aliyun.com/d/1131971649496228-*****-59/ApiServer?orgId=3**&refresh=60s","Name":"k8s-node-overview","IsArmsExporter":"false","Tags":"[\"arms-k8s\",\"ccc8ce1fe0c9543629e39ee657e34****\"]"}],"RequestId":"2A0CEDF1-06FE-44AC-8E21-21A5BE65****"}
```

