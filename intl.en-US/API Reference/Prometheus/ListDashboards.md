# ListDashboards

Queries Grafana dashboards of a Container Service Kubernetes cluster.

********

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=ListDashboards&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListDashboards|The operation that you want to perform. Set the value to `ListDashboards`. |
|ClusterId|String|Yes|cc7a37ee31aea4ed1a059eff8034b\*\*\*\*|The ID of the Container Service Kubernetes cluster. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DashboardVos|Array| |The information about the Grafana dashboard. |
|Exporter|String|Nginx|The type of the exporter access source. Valid values:

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
|Id|String|1100\*\*|The ID of the Grafana dashboard. The value is unique only when you install the Grafana dashboard. |
|IsArmsExporter|Boolean|false|Indicates whether the exporter is provided by Application Real-Time Monitoring Service \(ARMS\).

-   `true:` The exporter is provided by ARMS.
-   `false:`: The exporter is not provided by ARMS. |
|Tags|List|\["arms-k8s","ccc8ce1fe0c9543629e39ee657e34\*\*\*\*"\]|The tag of the Grafana dashboard. |
|Time|String|1590136924|The timestamp when the Grafana dashboard was created. |
|Title|String|ApiServer|The name of the Grafana dashboard. |
|Type|String|dash-db|The type of the Grafana dashboard. Valid values:

-   `dash-db`: indicates a dashboard.
-   `dash-folder`: indicates a folder that can include a dashboard. |
|Uid|String|1131971649496228-\*\*\*\*\*-59|The unique identifier of a dashboard when multiple Grafana dashboards are installed. It is a unique business ID on the page. |
|Url|String|http://g.console.aliyun.com/d/1131971649496228-\*\*\*\*\*-59/ApiServer?orgId=3\*\*&refresh=60s|The complete URL of the Grafana dashboard. |
|RequestId|String|2A0CEDF1-06FE-44AC-8E21-21A5BE65\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=ListDashboards
&ClusterId=cc7a37ee31aea4ed1a059eff8034b****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

