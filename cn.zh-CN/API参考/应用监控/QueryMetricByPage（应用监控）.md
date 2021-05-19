# QueryMetricByPage（应用监控）

调用QueryMetricByPage接口分页查询应用监控的相关监控指标。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=QueryMetricByPage&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryMetricByPage|系统规定参数，取值为`QueryMetricByPage`。 |
|EndTime|Long|是|1596183532000|结束时间的时间戳，精确到毫秒。 |
|IntervalInSec|Integer|是|60000|数据片的时间间隔，单位为毫秒，最小值为60000。 |
|Measures.N|RepeatList|是|youngGcCount|指标对应的测量数据，请参见[可查询的应用监控指标](#section_tq8_ysr_srb)。最多可添加5个。|
|Metric|String|是|appstat.vm|需要查询的指标，不可自定义输入，请参见[可查询的应用监控指标](#section_tq8_ysr_srb)。|
|StartTime|Long|是|1595319532000|起始时间的时间戳，精确到毫秒。 |
|OrderBy|String|否|rpc|排序依据，可设为任一测量数据。 |
|Filters.N.Key|String|是|pid|筛选条件组合，必须添加`pid`和`regionId`条件，`pid`获取方式，请参见[如何获取应用pid](#section_bkl_3j6_ezg)。|
|Filters.N.Value|String|是|atc889zkcf@d8deedfa9\*\*\*\*\*\*|筛选条件组合，必须添加`pid`和`regionId`条件，`pid`获取方式，请参见[如何获取应用pid](#section_bkl_3j6_ezg)。|
|Dimensions.N|RepeatList|否|\["detector\_browser","detector\_device"\]|指标对应的维度，请参见[可查询的应用监控指标](#section_tq8_ysr_srb)。最多可添加5个。|
|Order|String|否|ASC|排序标准：

-   `ASC`：升序
-   `DESC`：降序 |
|RegionId|String|否|cn-hangzhou|地域ID。 |
|CurrentPage|Integer|否|1|查询结果的页码。非必填参数，如果不填写则默认为`1`。 |
|PageSize|Integer|否|10|查询结果的每页项目数量。 |

## 如何获取应用pid

在[ARMS控制台](https://arms.console.aliyun.com/#/home)左侧导航栏中单击**应用监控** \> **应用列表**，并在顶部菜单栏选择目标地域，然后在**应用列表**页面单击目标应用名称，进入该应用总览页面。

此时浏览器地址栏中的URL即包含应用的pid，格式为`pid=xxx`。由于浏览器进行了编码，除EDAS应用之外的其他应用需要对pid稍作修改。例如，如果URL中包含的pid为`xxx%4074xxx`，则需要将`%40`替换为`@`，即：`xxx@74xxx`。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态，取值说明如下：

-   2XX：成功
-   3XX：重定向
-   4XX：请求错误
-   5XX：服务器错误 |
|Data|Struct| |返回结构体 |
|Items|List|\[\]|返回数据的数据结构体列表 |
|Page|Integer|1|查询结果的页码 |
|PageSize|Integer|10|查询结果的每页项目数量 |
|Total|Integer|0|查询结果的总项目数量 |
|Message|String|StartTime is mandatory for this action.|请求参数有误时返回的信息 |
|RequestId|String|626037F5-FDEB-45B0-804C-B3C92797\*\*\*\*|请求ID |
|Success|Boolean|true|查询是否成功：

-   `true`：成功
-   `false`：失败 |

## 可查询的应用监控指标

您可以使用QueryMetricByPage接口查询应用监控的以下指标。

**说明：**

-   filters参数必须添加`pid`和`regionId`条件。
-   已知具体的查询条件时，应将值传入filters参数中，用于限定查询结果的范围。如果不知道具体的查询条件，可以将下表中的维度传入dimensions参数，从而获得该维度所有可能值的列表。

|指标集（Metric）|描述（Description）|维度（Dimensions）|测量数据（Measures）|
|-----------|---------------|--------------|--------------|
|appstat.vm|通用指标，对应应用详情下的JVM监控图表，包括GC指标、堆内存和非堆内存详情以及线程数。|-   pid
-   rootIp

|GC指标： -   youngGcCount：JVM监控Young GC次数
-   oldGcCount：JVM监控Full GC次数
-   youngGcTime：JVM监控Young GC耗时
-   oldGcTime：JVM监控Full GC耗时
-   youngGcCountInstant：JVM监控Young GC次数瞬时值
-   oldGcCountInstant：JVM监控Full GC次数瞬时值
-   youngGcTimeInstant：JVM监控Young GC耗时瞬时值
-   oldGcTimeInstant：JVM监控Full GC耗时瞬时值 |
|堆内存和非堆内存详情：-   edenSpace：年轻代eden区
-   oldGen：老年代
-   survivorSpace：年轻代survivor区
-   metaSpace
-   nonHeapCommitted：非堆内存
-   nonHeapInit：非堆内存初始值
-   nonHeapMax：非堆内存最大值
-   nonHeapUsed：非堆内存使用量
-   directUsed：对外内存中direct\_buffer已使用的大写
-   directCapacity：对外内存中direct\_buffer的总大小 |
|线程数： -   threadCount：线程总数
-   threadNewCount：新建线程数
-   threadDeadlockCount：JVM内死锁的个数
-   threadRunnableCount：JVM处于Runnable的线程个数
-   threadTerminatedCount：终结线程数
-   threadTimedWaitCount：处于timed\_waiting状态的线程个数
-   threadWaitCount：处于waiting状态的线程个数
-   threadBlockedCount：阻塞线程数 |
|appstat.host|主机监控，包括实例数、CPU、物理内存、磁盘、负载、网络流量（Bytes）和网络数据包数量。|-   pid
-   rootIp

|实例数： -   instanceCount |
|CPU： -   systemCpuIdle：最近5s的空闲CPU使用率，控制台页面未展示
-   systemCpuSystem：最近5s的系统CPU使用率
-   systemCpuUser：最近5s的用户CPU使用率
-   systemCpuIoWait：最近5s的等待IO完成的CPU使用率 |
|物理内存： -   systemMemFree：当前系统的空闲内存
-   systemMemUsed：当前系统的已经使用的内存
-   systemMemTotal：当前系统的总内存，控制台页面未展示
-   systemMemBuffers：当前系统的buffer cache的内存数
-   systemMemCached：当前系统的page cache里的内存数 |
|磁盘： -   systemDiskFree：磁盘空闲字节数
-   systemDiskUsedRatio：磁盘使用率
-   systemDiskTotal：磁盘总字节数，公共云控制台页面未展示 |
|负载： -   systemLoad |
|网络： -   systemNetInPackets：最近30秒平均每秒网络接收到的报文数
-   systemNetOutPackets：最近30秒平均每秒网络发送的字节数
-   systemNetInErrs：最近30秒平均每秒网络Frame错误数
-   systemNetOutErrs：最近30秒平均每秒网络发送的错误数
-   systemNetInBytes：最近30秒平均每秒网络接收到的字节数
-   systemNetOutBytes：最近30秒平均每秒网络发送的字节数 |
|appstat.database|数据库调用。|-   pid
-   rpcType：调用类型
-   endpoint：数据库地址为localhost: 3306
-   destId：库名为`arms`

|-   rt：响应时间
-   count：请求数
-   error：错误数 |
|appstat.txn|接口调用。|-   pid
-   rpcType
-   rpc：接口为`/demo/oracleTwo`

|-   rt
-   count
-   error
-   errRate：错误率 |
|appstat.incall|应用详情。|-   pid
-   rpcType
-   rootIp
-   rpc
-   ppid

|-   rt
-   count
-   error |
|appstat.exception|异常。|-   pid
-   rpc
-   endpoint
-   excepType
-   excepInfo

|-   rt
-   count |
|appstat.sql|慢SQL。|-   pid
-   rpc
-   endpoint
-   sqlId

|-   rt
-   count
-   error
-   slow

**说明：** slow=true时，limit条件不生效。 |
|appstat.mq.send|MQ发送。|无|-   rt
-   count
-   error |
|appstat.mq.receive|MQ接收。|无|-   rt
-   count
-   error |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=QueryMetricByPage
&EndTime=1596183532000
&IntervalInSec=60000
&Measures.1=youngGcCount
&Metric=appstat.vm
&StartTime=1595319532000
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryMetricByPageResponse>
      <RequestId>626037F5-FDEB-45B0-804C-B3C92797****</RequestId>
      <Data>
            <PageSize>10</PageSize>
            <Total>0</Total>
            <Page>1</Page>
            <Items>[]</Items>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</QueryMetricByPageResponse>
```

`JSON` 格式

```
{
    "RequestId": "626037F5-FDEB-45B0-804C-B3C92797****",
    "Data": {
        "PageSize": 10,
        "Total": 0,
        "Page": 1,
        "Items": "[]"
    },
    "Code": 200,
    "Success": true
}
```

