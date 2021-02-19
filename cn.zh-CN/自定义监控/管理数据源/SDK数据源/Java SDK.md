# Java SDK

本文说明如何使用Java SDK向SDK数据源写入数据。

-   [创建 SDK 数据源](/cn.zh-CN/自定义监控/管理数据源/SDK数据源/SDK 数据源概述.md)
-   [安装Java开发环境](https://www.oracle.com/java/technologies/javase-downloads.html)

    **说明：** Java运行环境必须为Java SE 6或以上。

-   [安装Maven](http://maven.apache.org/download.cgi?__hstc=200028081.1bb630f9cde2cb5f07430159d50a3c91.1524009600081.1524009600082.1524009600083.1&__hssc=200028081.1.1524009600084&__hsfp=1773666937#)

## 安装Java SDK

1.  在Maven项目的pom.xml中添加以下依赖。

    ```
    <dependency>
      <groupId>com.aliyun.openservices</groupId>
      <artifactId>aliyun-log</artifactId>
      <version>0.6.6</version>
    </dependency>
    ```


## 通过Java SDK向SDK数据源写入数据

1.  创建示例程序LogstashForJavaDemo.java。

    示例代码如下。

    ```
    import com.aliyun.openservices.log.Client;
    import com.aliyun.openservices.log.common.LogItem;
    import com.aliyun.openservices.log.exception.LogException;
    import com.aliyun.openservices.log.request.PutLogsRequest;
    
    import java.text.DateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;
    import java.util.Vector;
    import java.util.UUID;
    
    public class LogstashForJavaDemo {
        public static void main(String[] args) throws LogException {
            DateFormat dateFormat = new java.text.SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
            String endpoint = "cn-hangzhou.log.aliyuncs.com";
            String project = "proj-arms-7dd6ecb06d21e02aed9eeb56b79e9f";
            String logstore = "logstore-56f96ec5546fb6555ef97dd057acb4e9";
            String accessKeyId = "xxx";
            String accessKeySecret = "yyy";
            int logGroupSize = 10;
            // 建议100-2000，每个batch发送数据上限。
            List<String> examples = new ArrayList<String>();
            examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=男装&区域=杭州&eventTeyp=1&性别=1&价格=2140|");
            examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=家居&区域=上海&eventTeyp=3&性别=0&价格=8305|");
            examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=食品&区域=深圳&eventTeyp=3&性别=1&价格=7121|");
            examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=男装&区域=上海&eventTeyp=3&性别=1&价格=2917|");
            examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=食品&区域=上海&eventTeyp=1&性别=1&价格=4285|");
            examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=男装&区域=杭州&eventTeyp=3&性别=1&价格=7864|");
            examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=女装&区域=杭州&eventTeyp=5&性别=0&价格=2983|");
            examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=食品&区域=深圳&eventTeyp=5&性别=1&价格=3201|");
            // 构建一个客户端实例。
            Client client = new Client(endpoint, accessKeyId, accessKeySecret);
            // 连续发送10个数据包，每个数据包有10条日志。
            long currentTime = System.currentTimeMillis();
            String formatedTime = dateFormat.format(new Date(currentTime));
            for (int i = 0; i < 10; i++) {
                Vector<LogItem> logGroup = new Vector<LogItem>();
                for (int j = 0; j < logGroupSize; j++) {
                    LogItem logItem = new LogItem();
                    logItem.PushBack("content", formatedTime + examples.get(j % examples.size()) + UUID.randomUUID());
                    logGroup.add(logItem);
                }
                PutLogsRequest req = new PutLogsRequest(project, logstore, "", "", logGroup);
                client.PutLogs(req);
            }
            System.out.println("send data success");
        }
    }
    ```

    -   endpoint：各个地域的Endpoint如下表所示。

        |地域|Endpoint|
        |--|--------|
        |北京|cn-beijing.log.aliyuncs.com|
        |青岛|cn-qingdao.log.aliyuncs.com|
        |上海|cn-shanghai.log.aliyuncs.com|
        |杭州|cn-hangzhou.log.aliyuncs.com|
        |深圳|cn-shenzhen.log.aliyuncs.com|

    -   accessKeyId：在ARMS控制台的**实例列表**页面，找到目标SDK数据源，在其右侧**操作**列，单击**获取AccessKey**，在**获取AccessKey**对话框的**AccessKey**右侧获取。
    -   accessKeySecret：在ARMS控制台的**实例列表**页面，找到目标SDK数据源，在其右侧**操作**列，单击**获取AccessKey**，在**获取AccessKey**对话框的**AccessKey Secret**右侧获取。
    -   project：在ARMS控制台的**实例列表**页面，找到目标SDK数据源，在其右侧**项目**列获取。
    -   logStore：在ARMS控制台的**实例列表**页面，找到目标SDK数据源，在其右侧**LogStore**列获取。
2.  执行LogstashForJavaDemo.java写入数据。


