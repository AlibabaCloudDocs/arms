# Service linked role for Tracing Analysis

This topic describes the service linked role AliyunServiceRoleForXtrace for Tracing Analysis, and how to delete this role.

## Background information

The service linked role for Tracing Analysis, AliyunServiceRoleForXtrace, is a RAM role that is defined by Tracing Analysis to access other Alibaba Cloud services in specific scenarios. For more information, see [Service-linked roles](/intl.en-US/RAM Role Management/Service-linked roles.md).

## Scenarios for using the AliyunServiceRoleForXtrace role

The service linked role AliyunServiceRoleForXtrace is automatically created. Tracing Analysis uses the AliyunServiceRoleForXtrace role to obtain the permissions to use the resources of the [Container Service for Kubernetes \(ACK\)](/intl.en-US/Product Introduction/What is Container Service for Kubernetes?.md), [Log Service](/intl.en-US/Product Introduction/What is Log Service?.md), [Elastic Compute Service \(ECS\)](/intl.en-US/Product Introduction/What is ECS?.md), and [Virtual Private Cloud \(VPC\)](/intl.en-US/Product Introduction/What is a VPC?.md) services.

## Permissions of the AliyunServiceRoleForXtrace role



The AliyunServiceRoleForXtrace role has the following permissions on relevant Alibaba Cloud services:

## Delete the AliyunServiceRoleForXtrace role

For security reasons, you may want to delete the service linked role AliyunServiceRoleForXtrace after you use the monitoring feature of Tracing Analysis. In this case, you must be aware that data within the current account cannot be stored or displayed after you delete the AliyunServiceRoleForXtrace role.

To delete the AliyunServiceRoleForXtrace role, perform the following steps:

**Note:** If application data exists within the current account, you must delete all applications before you can delete the AliyunServiceRoleForXtrace role.

1.  Log on to the [Resource Access Management \(RAM\) console](http://ram.console.aliyun.com/). In the left-side navigation pane, click **RAM Roles**.
2.  On the RAM Roles page, enter AliyunServiceRoleForXtrace in the search box. The RAM role named AliyunServiceRoleForXtrace is returned in the search result.
3.  Click **Delete** in the **Actions** column.
4.  In the Delete RAM Role message, click **OK**.
    -   If applications of Tracing Analysis exist within the current account, you must delete the applications before you can delete the AliyunServiceRoleForXtrace role. Otherwise, an error message appears.
    -   If all applications within the current account are deleted, you can directly delete the AliyunServiceRoleForXtrace role.

## FAQ

Why is my RAM user unable to automatically create the AliyunServiceRoleForXtrace role?

You must obtain the specified permission to automatically create or delete the AliyunServiceRoleForXtrace role. To authorize your RAM user to automatically create the AliyunServiceRoleForXtrace role, add the following permission policy for your RAM user:

```
{
    "Statement": [
        {
            "Action": [
                "ram:CreateServiceLinkedRole"
            ],
            "Resource": "acs:ram:*:ID of your Alibaba Cloud account:role/*",
            "Effect": "Allow",
            "Condition": {
                "StringEquals": {
                    "ram:ServiceName": [
                        "xtrace.aliyuncs.com"
                    ]
                }
            }
        }
    ],
    "Version": "1"
}
```

