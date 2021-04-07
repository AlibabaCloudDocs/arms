# Python SDK

本文说明如何使用Python SDK向SDK数据源写入数据。

-   [创建 SDK 数据源](/cn.zh-CN/自定义监控/管理数据源/SDK数据源/SDK 数据源概述.md)
-   [安装Python开发环境](https://www.python.org/downloads/?spm=a2c4g.11186623.2.8.36c5d51c3zWcZO)

    **说明：**

    -   日志服务Python SDK支持Pypy2、Pypy3、Python2.6、Python2.7、Python3.3、Python3.4、Python3.5、Python3.6和Python3.7版本。
    -   您可以执行`python -V`命令检查您已安装的Python版本。
-   [安装Python的包管理工具Pip](https://pip.pypa.io/en/latest/installing/?spm=a2c4g.11186623.2.9.36c5d51c3zWcZO)

    **说明：** 您可以执行`pip -V`命令检查您已安装的Pip版本。


## 安装Python SDK

1.  安装Python SDK。

    ```
    pip install -U aliyun-log-python-sdk
    ```


## 安装Python SDK的依赖库

Python SDK依赖于一组第三方的Python库。您在使用该SDK前必须安装以下依赖库：

-   Google Protocol Buffer

    Python SDK依赖于Protocol Buffer协议向服务端写入日志。

    安装命令如下。

    ```
    sudo pip install protobuf==2.5.0
    ```

    **说明：** 使用pip命令安装Protobuf需要连接Python Package Index网站，请确保您的机器能够访问该网站。如果因为网络问题无法安装成功，您可以从Protocol Buffer的Github官方网站手动下载安装。具体安装步骤，请参见[protobuf](https://github.com/protocolbuffers/protobuf)。

-   Python-Requests：

    Python SDK依赖于Python-Requests类进行HTTP通信。

    安装命令如下。

    ```
    sudo pip install requests
    ```

-   SimpleJson

    Python SDK依赖于SimpleJson处理API的JSON格式返回结果。

    安装命令如下。

    ```
    sudo pip install simplejson
    ```


## 通过Python SDK向SDK数据源写入数据

1.  创建示例程序sendmessage.py。

    ```
    #!/usr/bin/env python
    #encoding: utf-8
    import datetime
    from aliyun.log.logclient import LogClient
    from aliyun.log.logitem import LogItem
    from aliyun.log.putlogsrequest import PutLogsRequest
    def main():
        endpoint = "cn-hangzhou.log.aliyuncs.com"
        project = "proj-arms-7dd6ecb06d21e02aed9eeb56b7****"
        logstore = "logstore-56f96ec5546fb6555ef97dd057ac****"
        accessKeyId = "utmxiro7BYtT****"
        accessKeySecret = "PyjsffdlggBoYcrgpr69w023b9****"
        logGroupSize = 10
        examples = []
        examples.append('|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=男装&区域=杭州&eventTeyp=1&性别=1&价格=2140|')
        examples.append('|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=家居&区域=上海&eventTeyp=3&性别=0&价格=8305|')
        examples.append('|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=食品&区域=深圳&eventTeyp=3&性别=1&价格=7121|')
        examples.append('|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=男装&区域=上海&eventTeyp=3&性别=1&价格=2917|')
        examples.append('|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=食品&区域=上海&eventTeyp=1&性别=1&价格=4285|')
        examples.append('|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=男装&区域=杭州&eventTeyp=3&性别=1&价格=7864|')
        examples.append('|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=女装&区域=杭州&eventTeyp=5&性别=0&价格=2983|')
        examples.append('|c0a895e114526786450161001d1ed9|9|EADS|BIZ-MONITOR|0|类目=食品&区域=深圳&eventTeyp=5&性别=1&价格=3201|')
        # 构建一个client。
        client = LogClient(endpoint, accessKeyId, accessKeySecret)
        for i in range(0, 10):
            logGroup = []
            for j in range(0, 10):
                logItem = LogItem()
                logItem.push_back("content", datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S') + examples[j % len(examples)])
                logGroup.append(logItem)
            req = PutLogsRequest(project, logstore, "", "", logGroup)
            client.put_logs(req)
        print "send data success"
    if __name__ == '__main__':
        main()
    ```

    示例程序中各参数说明如下：

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
2.  执行sendmessage.py发送消息。


