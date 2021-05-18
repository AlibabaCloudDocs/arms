# SearchEvents

Queries alert event records.

Alert event records are different from alert notification records. Alert events are recorded every minute after an alert rule filters data. Alert events can be classified based on whether they are triggered or not. If a triggered event is not in the silence period, an alert notification is sent.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchEvents&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchEvents|The operation that you want to perform. Set the value to `SearchEvents`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|AlertId|Long|No|123|The ID of the alert rule. You can call the SearchAlertRules operation and view the `Id` parameter in the response. For more information, see [SearchAlertRules](~~175825~~). |
|Pid|String|No|atc889zkcf@d8deedfa9bf\*\*\*\*|The process identifier \(PID\) of the application that is associated with the alert rule. |
|CurrentPage|Integer|No|1|The number of the page to return. Default value: `1`. |
|PageSize|Integer|No|10|The number of entries to return on each page. Default value: `10`. |
|AppType|String|No|TRACE|The type of the application that is associated with the alert rule. Valid values:

 -   `TRACE`: application monitoring
-   `RETCODE`: frontend monitoring |
|AlertType|Integer|No|4|The type of the alert rule. Valid values:

 -   `1`: custom alert rules to monitor drill-down data sets
-   `3`: custom alert rules to monitor tiled data sets
-   `4`: alert rules to monitor the frontend, including the default frontend alert rules
-   `5`: alert rules to monitor applications, including the default application alert rules
-   `6`: the default frontend alert rules
-   `7`: the default application alert rules
-   `8`: Tracing Analysis alert rules
-   `101`: Prometheus alert rules |
|IsTrigger|Integer|No|1|Specifies whether the alert event is triggered. If you do not set this parameter, all alert events are queried. Valid values:

 -   `1`: The event is triggered.
-   `0`: The event is not triggered. |
|StartTime|Long|No|1595565300000|The beginning of the time range to query. Specify a UNIX timestamp of the LONG data type, in milliseconds. The default value is 10 minutes before the current time. |
|EndTime|Long|No|1595568970000|The end of the time range to query. Specify a UNIX timestamp of the LONG data type, in milliseconds. The default value is the current time. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsTrigger|Integer|0|Indicates whether the alert event is triggered. It is an internal parameter. |
|PageBean|Struct| |The struct returned. |
|Event|Array of Event| |The information about the alert events. |
|AlertId|Long|123|The ID of the alert rule that is associated with the event. |
|AlertName|String|alertName|The name of the alert rule that is associated with the event. |
|AlertRule|String|\{\\"operator\\":\\"&\\",\\"rules\\":\[\{\\"aggregates\\":\\"AVG\\",\\"alias\\":\\"JVM\_ThreadCount\\",\\"measure\\":\\"appstat.jvm.ThreadCount\\",\\"nValue\\":1,\\"operator\\":\\"HOH\_DOWN\\",\\"value\\":50.0\}\]\}|The condition of the alert rule. |
|AlertType|Integer|4|The type of the alert rule. This parameter is not returned. Valid values:

 -   `1`: custom alert rules to monitor drill-down data sets
-   `3`: custom alert rules to monitor tiled data sets
-   `4`: alert rules to monitor the frontend, including the default frontend alert rules
-   `5`: alert rules to monitor applications, including the default application alert rules
-   `6`: the default frontend alert rules
-   `7`: the default application alert rules
-   `8`: Tracing Analysis alert rules
-   `101`: Prometheus alert rules |
|EventLevel|String|1|The severity of the event. |
|EventTime|Long|1595569020000|The timestamp when the event occurred. |
|Id|Long|123|The ID of the event record. |
|Links|List|\[ "http://arms.console.aliyun.com/apm?startTime=1595565300000&endTime=1595569246633&regionId=cn-hangzhou&pid=\*\*\*\*" \]|The list of event URLs. |
|Message|String|Unknown emergency alert\\nIP address:172.27.XX.XX\\nApplication name = test\\nRegion = cn-shenzhen\\nAbnormal data = \{\\"timestamp\\":\\"1615447972235\\"\}|The event content. The parameter value is a JSON string. Each key indicates a dimension and each value indicates the alert content in the dimension. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|TotalCount|Integer|2|The total number of entries returned. |
|RequestId|String|32940175-181B-4B93-966E-4BB69176\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=SearchEvents
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SearchEventsResponse>
	  <PageBean>
 	       <TotalCount>2</TotalCount>
	        <PageSize>10</PageSize>
	        <PageNumber>1</PageNumber>
	        <Event>
	              <EventLevel>1</EventLevel>
	              <AlertType>4</AlertType>
 	             <AlertId>123</AlertId>
	              <AlertName>alertName</AlertName>
	              <Message>Unknown emergency alert\nIP address:172.27.XX.XX\nApplication name = test\nRegion = cn-shenzhen\nAbnormal data = {\"timestamp\":\"1615447972235\"}</Message>
	              <EventTime>1595569020000</EventTime>
	              <Id>123</Id>
	              <AlertRule>{\"operator\":\"&\",\"rules\":[{\"aggregates\":\"AVG\",\"alias\":\"JVM_ThreadCount\",\"measure\":\"appstat.jvm.ThreadCount\",\"nValue\":1,\"operator\":\"HOH_DOWN\",\"value\":50.0}]}</AlertRule>
	              <Links>[                     "http://arms.console.aliyun.com/apm?startTime=1595565300000&amp;endTime=1595569246633&amp;regionId=cn-hangzhou&amp;pid=****"                 ]</Links>
	        </Event>
	  </PageBean>
	  <RequestId>32940175-181B-4B93-966E-4BB69176****</RequestId>
	  <IsTrigger>0</IsTrigger>
</SearchEventsResponse>
```

`JSON` format

```
{
    "PageBean": {
        "TotalCount": 2,
        "PageSize": 10,
        "PageNumber": 1,
        "Event": {
            "EventLevel": 1,
            "AlertType": 4,
            "AlertId": 123,
            "AlertName": "alertName",
            "Message": "Unknown emergency alert\\nIP address:172.27.XX.XX\\nApplication name = test\\nRegion = cn-shenzhen\\nAbnormal data = {\\\"timestamp\\\":\\\"1615447972235\\\"}",
            "EventTime": 1595569020000,
            "Id": 123,
            "AlertRule": "{\\\"operator\\\":\\\"&amp;\\\",\\\"rules\\\":[{\\\"aggregates\\\":\\\"AVG\\\",\\\"alias\\\":\\\"JVM_ThreadCount\\\",\\\"measure\\\":\\\"appstat.jvm.ThreadCount\\\",\\\"nValue\\\":1,\\\"operator\\\":\\\"HOH_DOWN\\\",\\\"value\\\":50.0}]}",
            "Links": "[                     \"http://arms.console.aliyun.com/apm?startTime=1595565300000&amp;endTime=1595569246633&amp;regionId=cn-hangzhou&amp;pid=****\"                 ]"
        }
    },
    "RequestId": "32940175-181B-4B93-966E-4BB69176****",
    "IsTrigger": 0
}
```

