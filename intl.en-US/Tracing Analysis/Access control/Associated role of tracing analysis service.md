# Associated role of tracing analysis service

This topic describes how to AliyunServiceRoleForXtrace and delete a role associated with tracing analysis services.

## Background

Tracing analysis AliyunServiceRoleForXtrace roles that are bound to resource access management \(RAM\) users. In some cases, to implement some functions of tracing analysis, you must obtain the access permissions of other cloud services. For more information about service-associated roles, see [Service linked roles](/intl.en-US/RAM Role Management/Service linked roles.md).

## Scenarios for AliyunServiceRoleForXtrace

Link tracking monitoring access [container service](https://help.aliyun.com/document_detail/86737.html#concept-cbm-1zc-l2b), [log service](https://help.aliyun.com/document_detail/48869.html#concept-mt2-ykn-vdb), [Elastic Compute Service \(ECS](https://help.aliyun.com/document_detail/25367.html#EcsWelcome) and [Virtual Private Cloud](https://help.aliyun.com/document_detail/34217.html#concept-kbk-cpz-ndb) cloud service resources allows you to automatically create the link tracking service associate roles AliyunServiceRoleForXtrace gain access.

## AliyunServiceRoleForXtrace permissions



AliyunServiceRoleForXtrace have access permissions on the following cloud services:

## Delete AliyunServiceRoleForXtrace

If you are using the tracing analysis monitoring function and want to delete a AliyunServiceRoleForXtrace that is associated with tracing analysis services, for the sake of security, you must clarify the impact of deletion. For example, if you want to delete a role, make sure that data under the current account cannot be stored or displayed after the AliyunServiceRoleForXtrace is deleted.

To delete a AliyunServiceRoleForXtrace, follow these steps:

**Note:** If data of any applications exists in the current account, you need to delete all applications before you can delete AliyunServiceRoleForXtrace.

1.  Log on to the [RAM console](http://ram.console.aliyun.com/). In the left-side navigation pane, click **RAM roles**.
2.  On the RAM roles page, enter the AliyunServiceRoleForXtrace in the search box to locate the RAM role named AliyunServiceRoleForXtrace.
3.  In the **actions** column, click **delete**.
4.  In the delete RAM role dialog box, click **OK**.
    -   If you have trace tracking applications, you need to delete all applications before deleting the AliyunServiceRoleForXtrace. Otherwise, a message appears, indicating that the deletion fails.
    -   If all applications under the current account have been deleted, you can directly delete AliyunServiceRoleForXtrace.

## FAQ

Why can't my XTRACE user automatically create ARMS Service Association role AliyunServiceRoleForXtrace?

You must have the specified permissions to automatically create or delete AliyunServiceRoleForXtrace. If the RAM user cannot automatically create AliyunServiceRoleForXtrace, you must add the following policy.

```

     {"Statement": [ { "Action": [ "ram:CreateServiceLinkedRole" ], "Resource": "acs:ram:*: primary account ID:role/*", "Effect": "Allow", "Condition": { "StringEquals": { "ram: serviceName": [ "xtrace.aliyuncs.com" ] } } } ], "Version": "1"} 
   
```

