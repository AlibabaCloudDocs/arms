# SDK for Python {#concept_52356_zh .concept}

本文为 Python 示例。

## 安装 Python 环境 {#section_vwq_sts_gfb .section}

Python SDK 是一个纯 Python 的库，支持所有运行 Python 的操作系统，目前主要为 Linux 和 Windows。

请按以下步骤安装 Python：

1.  下载并安装最新的 [Python 2 安装包](https://www.python.org/downloads/)。

    目前，Python SDK 支持 Python 2.6/2.7环境。可以运行 `python -V` 查询当前 Python 版本。

2.  下载并安装 Python 的包管理工具 pip。

    完成 pip 安装后，你可以运行 `pip -V` 确认 pip 是否安装成功和查看当前 pip 版本。


## 安装 Python SDK 的依赖库 {#section_gkd_wts_gfb .section}

Python SDK 依赖于一组第三方的 Python 库。在使用该 SDK 前必须安装好以下依赖库：

-   Google Protocol Buffer：Python SDK 依赖于 Protocol Buffer 协议向服务端写入日志。执行以下命令进行安装：

    ``` {#codeblock_v1o_ace_oq6}
    sudo pip install protobuf==2.5.0
    ```

    pip 安装 Protobuf 需要连接 Python Package Index 网站，请确保机器能够访问该网站。如果因为网络问题无法安装成功，可以考虑从 Protocol Buffer 的 Github 官方网站手动下载安装（具体安装步骤请参考下载包的 Readme 文档）。

-   Python-Requests：Python SDK 依赖于 Python-Requests 类进行 HTTP 通信。执行以下命令进行安装：

``` {#codeblock_dh9_qfa_kus}
sudo pip install requests
```

-   SimpleJson：Python SDK 依赖于 SimpleJson 处理 API 的 JSON 格式返回结果。执行以下命令进行安装：

    ``` {#codeblock_nuz_85i_ix7}
    sudo pip install simplejson
    ```


## 安装 Python SDK {#section_x5s_yts_gfb .section}

安装好上述环境后，需要下载 Python SDK。

1.  从 GitHub 下载最新的 Python SDK 包。
2.  解压完整下载的包到指定目录。
3.  在解压后的目录运行以下命令安装 Python SDK。

    ``` {#codeblock_ndw_dir_jtu}
    python setup.py install
    ```


## 开始一个 Python 程序 {#section_lh4_15s_gfb .section}

``` {#codeblock_rku_8jf_xxp}
#!/usr/bin/env python
#encoding: utf-8
import datetime
from aliyun.log.logclient import LogClient
from aliyun.log.logitem import LogItem
from aliyun.log.putlogsrequest import PutLogsRequest
def main():
    #endpoint: 数据写入存储所在区域
    #project,logstore: 构成基本数据存储目标
    #accessKeyId,accessKeySecret: 构成访问密钥
    #注意: 请用户根据实际情况填写
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
    # 构建一个client
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

## 重要参数说明 {#section_ol9_o1z_8s7 .section}

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


