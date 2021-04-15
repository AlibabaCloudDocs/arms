# 为什么RAM用户查看应用详情时出现错误？

## Condition

RAM用户在[ARMS控制台](https://arms.console.aliyun.com/#/home)的App监控页面查看应用详情时，提示错误：**对不起，您没有权限执行操作**。

## Cause

默认情况下，阿里云账号拥有自己所创建的App资源的完整操作权限，但是新创建的RAM用户没有权限操作阿里云账号的资源。

## Remedy

需要通过RAM授权的方式，给予RAM用户操作阿里云账号资源的权限。

1.  创建主体。

    您可基于用户、用户组或RAM角色任一主体进行访问控制，请根据实际需求进行相应设置。

    -   创建用户。具体操作，请参考[创建RAM用户](/cn.zh-CN/用户管理/创建RAM用户.md)。
    -   创建用户组。具体操作，请参考[创建用户组](/cn.zh-CN/用户组管理/创建用户组.md)。
    -   创建RAM角色。具体操作，请参考[RAM角色概览](/cn.zh-CN/角色管理/RAM角色概览.md)。
2.  登录[RAM控制台](http://ram.console.aliyun.com)。

3.  在左侧导航栏中选择**权限管理** \> **授权**。

4.  在授权页面，单击**新增授权**。

5.  在添加权限面板，执行以下操作：

    ![RAM授权-添加权限](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1158648161/p264270.png)

    1.  设置授权应用范围为整个云账号。

    2.  在被授权主体区域的文本框内输入关键字，选择已创建的用户、用户组或RAM角色。

    3.  在选择权限区域，执行以下操作：

        1.  选择系统策略选项。
        2.  在文本框中输入关键字emas，搜索移动研发平台（EMAS）的系统策略，包括：
            -   AliyunEmasDevOpsFullAccess：管理Mobile DevOps的权限。
            -   AliyunEmasDevOpsReadOnlyAccess：只读访问Mobile DevOps的权限。
            -   AliyunEMASAppMonitorFullAccess：管理EMAS崩溃分析、性能分析和远程日志服务的权限。
            -   AliyunEMASAppMonitorReadOnlyAccess：只读访问EMAS崩溃分析、性能分析和远程日志服务的权限。
        3.  根据实际需要，单击移动研发平台（EMAS）的权限策略名称，添加至右侧已选择列表。

            **说明：**

            -   Mobile DevOps的系统策略至少选择一个。
            -   崩溃分析、性能分析和远程日志的系统策略至少选择一个。
6.  单击**确定**。


