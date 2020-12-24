# 开始监控部署在其他环境（如ECS和Docker集群）的应用

ARMS业务监控以代码无侵入的方式，可视化定义业务请求，并为您提供贴合业务的丰富性能指标与诊断能力。在使用业务监控之前，您需要先为您的Java应用完成安装探针或升级探针这一准备工作。

## 限制条件

-   业务监控仅支持监控Java应用。
-   只有2.6.2+版本的应用探针支持ARMS业务监控功能。

## 操作流程

![dg_business_workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7067197951/p103004.png)

**说明：** 扫描以下二维码图片加入钉钉答疑群。

![dg__business_dingding](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7067197951/p92785.png)

## 为ECS中的Java应用安装或升级探针

1.  如果您是初次使用业务监控，并且未使用过应用监控的新用户，则按照应用监控的文档说明安装最新版本的探针，详情请参见[为Java应用手动安装Agent](/intl.zh-CN/应用监控/开始监控 Java 应用/为Java应用手动安装Agent.md)。

2.  如果您是初次使用业务监控，并且已使用过应用监控的老用户，则需在使用业务监控前，将应用探针版本升级至2.6.2+版本。

    1.  升级探针前，需要先卸载探针后再重新安装探针，详情请参见[卸载Agent](/intl.zh-CN/应用监控/开始监控 Java 应用/为Java应用手动安装Agent.md)。

    2.  重新安装探针，详情请参见[为Java应用手动安装Agent](/intl.zh-CN/应用监控/开始监控 Java 应用/为Java应用手动安装Agent.md)。


## 为Docker中的Java应用安装或升级探针

1.  如果您是初次使用业务监控，并且未使用过应用监控的新用户，则按照应用监控的文档说明安装最新版本的探针，详情请参见[为Docker中的Java应用安装Agent](/intl.zh-CN/应用监控/开始监控 Java 应用/为Docker中的Java应用安装Agent.md)。

2.  如果您是初次使用业务监控，并且已使用过应用监控的老用户，则需在使用业务监控前，将应用探针版本升级至2.6.2+版本。

    1.  升级探针前，需要先卸载探针后再重新安装探针，详情请参见[卸载Agent](/intl.zh-CN/应用监控/开始监控 Java 应用/为Docker中的Java应用安装Agent.mdsection_f5i_71i_rtn)。

    2.  重新安装探针，详情请参见[为Docker中的Java应用安装Agent](/intl.zh-CN/应用监控/开始监控 Java 应用/为Docker中的Java应用安装Agent.md)。


## 使用脚本为Java应用快速安装或升级探针

1.  如果您是初次使用业务监控，并且未使用过应用监控的新用户，则按照应用监控的文档说明安装最新版本的探针，详情请参见[使用脚本为Java应用快速安装探针](/intl.zh-CN/应用监控/开始监控 Java 应用/使用脚本为Java应用快速安装探针.md)。

2.  如果您是初次使用业务监控，并且已使用过应用监控的老用户，则需在使用业务监控前，将应用探针版本升级至2.6.2+版本。

    1.  升级探针前，需要先卸载探针后再重新安装探针，详情请参见[卸载探针](/intl.zh-CN/应用监控/开始监控 Java 应用/使用脚本为Java应用快速安装探针.md)。

    2.  重新安装探针，详情请参见[使用脚本为Java应用快速安装探针](/intl.zh-CN/应用监控/开始监控 Java 应用/使用脚本为Java应用快速安装探针.md)。


