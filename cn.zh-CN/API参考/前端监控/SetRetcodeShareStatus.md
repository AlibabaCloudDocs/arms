# SetRetcodeShareStatus

调用SetRetcodeShareStatus接口打开或关闭前端监控站点的免登录分享开关。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SetRetcodeShareStatus&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetRetcodeShareStatus|系统规定参数，取值为`SetRetcodeShareStatus`。 |
|Pid|String|是|atc889zkcf@d8deedfa9bf\*\*\*\*|应用的ID标识串。获取方式请参见[如何获取应用PID](https://help.aliyun.com/document_detail/186100.html?spm=a2c4g.11186623.6.792.1b50654cqcDPyk#title-imy-7gj-qhr)。 |
|Status|Boolean|是|true|设置前端监控站点的免登录分享开关的状态。取值：

 -   `true`：开启。
-   `false`：关闭。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|IsSuccess|Boolean|true|操作是否成功：

 -   `true`：操作成功
-   `false`：操作失败 |
|RequestId|String|40B10E04-81E8-4643-970D-F1B38F2E\*\*\*\*|请求ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SetRetcodeShareStatus
&Pid=atc889zkcf@d8deedfa9bf****
&Status=true
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<SetRetcodeShareStatusResponse>
      <IsSuccess>true</IsSuccess>
      <RequestId>40B10E04-81E8-4643-970D-F1B38F2E****</RequestId>
</SetRetcodeShareStatusResponse>
```

`JSON`格式

```
{
    "IsSuccess": true,
    "RequestId": "40B10E04-81E8-4643-970D-F1B38F2E****"
}
```

