# 自建Kubernetes集群

本文说明如何将自建或非阿里云的Kubernetes集群接入Prometheus监控，从而使用预定义的大盘监控主机和Kubernetes集群的众多性能指标。

-   已自建Kubernetes集群。具体操作，请参见[创建集群](https://kubernetes.io/zh/docs/tutorials/kubernetes-basics/create-cluster/)。
-   已开通ARMS。具体操作，请参见[开通和升级ARMS](/intl.zh-CN/快速入门/开通和升级ARMS.md)。

## 开启阿里云Prometheus监控

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择地域，然后单击**新建prometheus实例**。

4.  在**新建prometheus实例**页面，单击**自建Kubernetes集群**区域。

5.  在**自建Kubernetes集群接入**配置向导对话框，完成以下操作：

    1.  在**第1步**页签下，输入自建Kubernetes集群的名称，然后单击**下一步**。

        ![custom-test-1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6280416161/p253266.png)

    2.  执行**第2步**页签下的命令，然后单击**下一步**。

        ![custom-test-2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6280416161/p253268.png)

    3.  执行**第3步**页签下的命令。

        ![custom-3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6280416161/p253271.png)

        **说明：** 关于Helm命令的参数说明，请参见[Helm命令参数说明]()。

    **Prometheus监控**页面显示接入的自建Kubernetes集群。


## 查看Prometheus监控数据

开启阿里云Prometheus监控后，您可以在Grafana大盘上查看Prometheus监控数据。

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择地域，然后在**已安装大盘**列，单击需要查看的大盘。

    **说明：** 关于Grafana大盘的说明，请参见[基础大盘说明]()。


## 卸载监控插件

如需停止对自建Kubernetes集群的Prometheus监控，请按照以下步骤卸载Prometheus监控插件。

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择地域，找到要卸载监控插件的K8s集群，然后在其右侧**操作**列，单击**卸载**，并在**确认**对话框单击**确认**。

    卸载插件完毕后，**Prometheus监控**页面不再显示该自建Kubernetes集群。


