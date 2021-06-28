---
keyword: [RAM角色, 服务关联角色]
---

# ARMS服务关联角色

本文介绍ARMS服务关联角色AliyunServiceRoleForARMS以及如何删除该角色。

ARMS服务关联角色AliyunServiceRoleForARMS是ARMS在某些情况下，为了完成自身的某个功能，需要获取其他云服务的访问权限而提供的RAM角色。更多关于服务关联角色的信息请参见[服务关联角色](/cn.zh-CN/角色管理/服务关联角色.md)。

## AliyunServiceRoleForARMS应用场景

ARMS Prometheus监控功能需要访问[容器服务ACK](/cn.zh-CN/产品简介/什么是容器服务Kubernetes版.md)、[日志服务SLS](/cn.zh-CN/产品简介/什么是日志服务.md)、[云服务器ECS](/cn.zh-CN/产品简介/什么是云服务器ECS.md)和[专有网络VPC](/cn.zh-CN/产品简介/什么是专有网络.md)云服务的资源时，可通过自动创建的ARMS服务关联角色AliyunServiceRoleForARMS获取访问权限。

## AliyunServiceRoleForARMS权限说明

AliyunServiceRoleForARMS具备以下云服务的访问权限：



## 删除AliyunServiceRoleForARMS

如果您使用了ARMS Prometheus监控功能，然后需要删除ARMS服务关联角色AliyunServiceRoleForARMS，例如您出于安全考虑，需要删除该角色，则需要先明确删除后的影响：删除AliyunServiceRoleForARMS后，无法将当前账号下的K8s集群同步至[ARMS控制台](https://arms.console.aliyun.com/#/home)的K8s集群列表中，与此同时，ARMS控制台将停止获取及写入相关监控数据。

删除AliyunServiceRoleForARMS的操作步骤如下：

**说明：** 如果当前账号下的K8s集群安装了ARMS Prometheus监控Agent，则需先删除Agent后才能删除AliyunServiceRoleForARMS，否则提示删除失败，详情请参见[卸载Prometheus监控插件]()。

1.  登录[RAM控制台](http://ram.console.aliyun.com)，在左侧导航栏中单击**RAM角色管理**。

2.  在RAM角色管理页面的搜索框中，输入**AliyunServiceRoleForARMS**，自动搜索到名称为AliyunServiceRoleForARMS的RAM角色。

3.  在右侧**操作**列，单击**删除**。

4.  在删除RAM角色对话框，单击**确定**。

    -   如果当前账号下的K8s集群安装了ARMS Prometheus监控Agent，则需先删除Agent后才能删除AliyunServiceRoleForARMS，否则提示删除失败，详情请参见[卸载Prometheus监控插件]()。
    -   如果当前账号下的K8s集群已卸载ARMS Prometheus监控Agent，则可直接删除AliyunServiceRoleForARMS。

## 常见问题

为什么我的RAM用户无法自动创建ARMS服务关联角色AliyunServiceRoleForARMS？

您需要拥有指定的权限，才能自动创建或删除AliyunServiceRoleForARMS。因此，在RAM用户无法自动创建AliyunServiceRoleForARMS时，您需为其添加以下权限策略。

```
{
    "Statement": [
        {
            "Action": [
                "ram:CreateServiceLinkedRole"
            ],
            "Resource": "acs:ram:*:主账号ID:role/*",
            "Effect": "Allow",
            "Condition": {
                "StringEquals": {
                    "ram:ServiceName": [
                        "arms.aliyuncs.com"
                    ]
                }
            }
        }
    ],
    "Version": "1"
}
```

**说明：** 请将`主账号ID`替换为您实际的阿里云账号（主账号）ID。

**相关文档**  


[服务关联角色](/cn.zh-CN/角色管理/服务关联角色.md)

