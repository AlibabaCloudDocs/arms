# SDK for Java {#concept_52318_zh .concept}

本文为 Java 示例。

## 引入 POM 依赖 {#section_jjn_wss_gfb .section}

```
<dependency>
  <groupId>com.aliyun.openservices</groupId>
  <artifactId>aliyun-log</artifactId>
  <version>0.6.6</version>
</dependency>
```

## 开始一个 Java 程序 { .section}

```
public class LogstashForJavaDemo {
    public static void main(String[] args) throws LogException {
        DateFormat dateFormat = new java.text.SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        /**
         * endpoint: 数据写入存储所在区域 
         * project,logstore: 构成基本数据存储目标
         * accessKeyId,accessKeySecret: 构成访问密钥
         * 
         * 注意: 请用户根据实际情况填写
         */
        String endpoint = "cn-hangzhou.log.aliyuncs.com";
        String project = "proj-arms-7dd6ecb06d21e02aed9eeb56b79e9f";
        String logstore = "logstore-56f96ec5546fb6555ef97dd057acb4e9";
        String accessKeyId = "xxx";
        String accessKeySecret = "yyy";
        int logGroupSize = 10;// 建议100-2000，每个batch发送数据上限
        List<String> examples = new ArrayList<String>();
        examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=男装&区域=杭州&eventTeyp=1&性别=1&价格=2140|");
        examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=家居&区域=上海&eventTeyp=3&性别=0&价格=8305|");
        examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=食品&区域=深圳&eventTeyp=3&性别=1&价格=7121|");
        examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=男装&区域=上海&eventTeyp=3&性别=1&价格=2917|");
        examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=食品&区域=上海&eventTeyp=1&性别=1&价格=4285|");
        examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=男装&区域=杭州&eventTeyp=3&性别=1&价格=7864|");
        examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=女装&区域=杭州&eventTeyp=5&性别=0&价格=2983|");
        examples.add("|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=食品&区域=深圳&eventTeyp=5&性别=1&价格=3201|");
        // 构建一个客户端实例
        Client client = new Client(endpoint, accessKeyId, accessKeySecret);
        // 连续发送10个数据包，每个数据包有10条日志
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

## 重要参数说明 { .section}

|参数|说明|
|--|--|
|endpoint|数据写入区域（[表 1](intl.zh-CN/自定义监控/管理数据源/Logstash SDK 数据源/SDK 数据源概述.md#table_ow2_prs_gfb)）|
|accessKeyId|写入数据时的密钥 ID|
|accessKeySecret|写入数据时的密钥密码|
|project|写入数据的 Project ID|
|logstore|写入数据的 Logstore ID|

**说明：** 

-   ARMS 颁发的 accessKeyId、accessKeySecret 非阿里云 AK/SK，需要从 ARMS 获取，详情参见[SDK 数据源概述](intl.zh-CN/自定义监控/管理数据源/Logstash SDK 数据源/SDK 数据源概述.md#)。

-   Project ID 和 Logstore ID 标识一个唯一的数据源。


