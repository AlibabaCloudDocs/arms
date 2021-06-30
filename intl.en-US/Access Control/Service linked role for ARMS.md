---
keyword: [RAM role, service linked role]
---

# Service linked role for ARMS

This topic describes the service linked role AliyunServiceRoleForARMS for Application Real-Time Monitoring Service \(ARMS\), and how to delete this role.

The service linked role for ARMS, AliyunServiceRoleForARMS, is a Resource Access Management \(RAM\) role that is defined by ARMS to access other Alibaba Cloud services in specific scenarios. For more information about service linked roles, see [Service-linked roles](/intl.en-US/RAM Role Management/Service-linked roles.md).

## AliyunServiceRoleForARMS application scenarios

When ARMS Prometheus Monitoring needs to access other Alibaba Cloud resources such as [Alibaba Cloud Container Service for Kubernetes \(ACK\)](/intl.en-US/Product Introduction/What is Container Service for Kubernetes?.md), [Log Service \(SLS\)](/intl.en-US/Product Introduction/What is Log Service?.md), [Elastic Compute Service \(ECS\)](/intl.en-US/Product Introduction/What is ECS?.md), and [Virtual Private Cloud \(VPC\)](/intl.en-US/Product Introduction/What is a VPC?.md), ARMS Prometheus Monitoring can use the automatically created AliyunServiceRoleForARMS role to get access permissions.

## Permissions of the AliyunServiceRoleForARMS role

AliyunServiceRoleForARMS has permissions to access the following cloud services:

## Delete the AliyunServiceRoleForARMS role

After you have enabled ARMS Prometheus Monitoring, if you need to delete the AliyunServiceRoleForARMS role for security purposes, make sure that you understand the impact of deleting the role. After the AliyunServiceRoleForARMS role is deleted, the Kubernetes cluster under the current account cannot be synchronized to the Kubernetes cluster list in [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home), and the ARMS console stops obtaining and writing relevant monitoring data.

To delete the AliyunServiceRoleForARMS role, perform the following steps:

**Note:** If an ARMS Prometheus Monitoring agent has been installed for the Kubernetes cluster under the current account, delete the agent first. Otherwise, the AliyunServiceRoleForARMS role cannot be deleted. For more information, see [Uninstall the Prometheus agent]().

1.  Log on to the [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, click **RAM Roles**.

2.  On the RAM Roles page, enter **AliyunServiceRoleForARMS** in the search box. The RAM role named AliyunServiceRoleForARMS is returned in the search result.

3.  In the **Actions** column on the right, click **Delete**.

4.  In the Delete RAM Role dialog box, click **OK**.

    -   If an ARMS Prometheus Monitoring agent has been installed for the Kubernetes cluster under the current account, delete the agent first. Otherwise, the AliyunServiceRoleForARMS role cannot be deleted. For more information, see [Uninstall the Prometheus agent]().
    -   If the ARMS Prometheus Monitoring agent for the Kubernetes cluster under the current account has been uninstalled, you can directly delete the AliyunServiceRoleForARMS role.

## FAQ

Why is my RAM user unable to automatically create the AliyunServiceRoleForARMS role?

You must get the specified permission to automatically create or delete the AliyunServiceRoleForARMS role. To authorize your RAM user to automatically create the AliyunServiceRoleForARMS role, add the following permission policy for your RAM user.

```
{
    "Statement": [
        {
            "Action": [
                "ram:CreateServiceLinkedRole"
            ],
            "Resource": "acs:ram:*:Alibaba Cloud account ID:role/*",
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

**Note:** Replace the `Alibaba Cloud account ID` with your Alibaba Cloud account ID.

**Related topics**  


[Service-linked roles](/intl.en-US/RAM Role Management/Service-linked roles.md)

