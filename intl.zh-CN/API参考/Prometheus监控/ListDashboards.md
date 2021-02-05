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

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DashboardVos|Array| |Grafana大盘信息。 |
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
-   Kubernates
-   Client Library
-   ElasticSearch |
|Id|String|1100\*\*|Grafana大盘ID，仅在安装Grafana大盘时是唯一的。 |
|IsArmsExporter|Boolean|false|是否属于ARMS提供的Exporter：

 -   `true`：是ARMS提供的Exporter
-   `false`：不是ARMS提供的Exporter |
|Tags|List|\["arms-k8s","ccc8ce1fe0c9543629e39ee657e34\*\*\*\*"\]|Grafana大盘标签。 |
|Time|String|1590136924|Grafana大盘创建时间的时间戳。 |
|Title|String|ApiServer|Grafana大盘名称。 |
|Type|String|dash-db|Grafana大盘类型，包括：

 -   `dash-db`：大盘
-   `dash-folder`：文件夹（可包含大盘） |
|Uid|String|1131971649496228-\*\*\*\*\*-59|安装多个Grafana大盘时的大盘唯一标识符，是展示在页面上的唯一业务ID。 |
|Url|String|http://g.console.aliyun.com/d/1131971649496228-\*\*\*\*\*-59/ApiServer?orgId=3\*\*&refresh=60s|Grafana大盘的完整URL。 |
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

`XML` 格式

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

`JSON` 格式

```
{
	"DashboardVos": [
		{
			"Uid": "1131971649496228-*****-59",
			"Type": "dash-db",
			"Title": "ApiServer",
			"Time": "",
			"Id": "1100**",
			"Exporter": "Nginx",
			"Url": "http://g.console.aliyun.com/d/1131971649496228-*****-59/ApiServer?orgId=3**&refresh=60s",
			"Tags": [
				"arms-prom",
				"ce1887373d0204999835904236961a83d",
				"api-server"
			],
			"IsArmsExporter": true
		}
	],
	"RequestId": "2A0CEDF1-06FE-44AC-8E21-21A5BE65****"
}
```

