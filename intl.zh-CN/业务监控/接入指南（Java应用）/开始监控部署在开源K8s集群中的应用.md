# 开始监控部署在开源K8s集群中的应用

ARMS业务监控以代码无侵入的方式，可视化定义业务请求，并为您提供贴合业务的丰富性能指标与诊断能力。在使用业务监控之前，您需要先为您的Java应用完成安装探针或升级探针这一准备工作。

## 限制条件

-   业务监控仅支持监控Java应用。
-   只有2.6.2+版本的应用探针支持ARMS业务监控功能。

## 操作流程

![dg_business_workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7067197951/p103004.png)

**说明：** 扫描以下二维码图片加入钉钉答疑群。

![dg__business_dingding](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7067197951/p92785.png)

## 为开源Kubernetes环境中的应用安装探针

如果您是初次使用业务监控，并且未使用过应用监控的新用户，则按照应用监控的文档说明安装最新版本的探针，详情请参见[为开源Kubernetes环境中的应用安装探针](/intl.zh-CN/应用监控/开始监控 Java 应用/为开源Kubernetes环境中的应用安装探针.md)。

## 为开源Kubernetes环境中的应用升级探针

如果您是初次使用业务监控，并且已使用过应用监控的老用户，则在使用业务监控前，需将应用探针版本升级至2.6.2+版本。升级探针前，需要先卸载探针后再重新安装探针。

具体步骤如下所示：

1.  卸载探针，详情请参见[卸载探针](/intl.zh-CN/应用监控/开始监控 Java 应用/为开源Kubernetes环境中的应用安装探针.mdsection_anc_ksu_mmw)。

2.  重新安装探针，详情请参见[为开源Kubernetes环境中的应用安装探针](/intl.zh-CN/应用监控/开始监控 Java 应用/为开源Kubernetes环境中的应用安装探针.md)。

3.  重启您的业务Pod。

    应用探针自动升级。

4.  在容器内执行`cat /home/admin/.opt/ArmsAgent/version`命令，查看应用探针的版本号。

    若版本号以2.6.2开头，则表示应用探针版本已成功升级至2.6.2+ 版本，此时您可以创建业务监控任务监控您的应用。


**相关文档**  


[准备工作概述]()

