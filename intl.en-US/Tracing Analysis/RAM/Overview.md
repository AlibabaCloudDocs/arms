# Overview

If multiple users in your enterprise need to collaborate on resources, RAM allows you to avoid sharing the accesskey of your Alibaba Cloud primary account with other users, and grant users the minimum permissions needed. this reduces the information security risks of your enterprise.

## Scenarios

The following examples describe how to use RAM to implement access control:

-   Use RAM users to delegate permissions

    Assume that enterprise A Buys A variety of Alibaba Cloud products, such as ECS instances, RDS instances, server load balancer instances, and OSS buckets, for Project-X. Multiple employees in a project need to perform operations on these cloud resources. Different employees require different permissions because they have different responsibilities. Enterprise A wants to meet the following requirements:

    -   For security reasons, Enterprise A does not want to disclose the accesskey of its Alibaba Cloud account to its employees. Instead, it wants to create independent accounts for its employees.
    -   User accounts can only operate on resources under authorization. Enterprise A can revoke permissions on and delete user accounts at any time.
    -   User accounts do not need to be measured and billed independently, and all expenses are borne by A.
    In response to the above requirements, the authorization management function of RAM can be used to implement user authorization and unified resource management.


## Policies

The following table describes the system policies supported by Tracing Analysis.

|Policy|Type|Description|
|------|----|-----------|
|AliyunTracingAnalysisFullAccess|System policy|Full permissions on Tracing Analysis|
|AliyunTracingAnalysisReadOnlyAccess|System policy|Read-only permissions on Tracing Analysis|

**Related topics**  


[Grant different permissions to RAM users](/intl.en-US/Access control/Grant different permissions to RAM users.md)

