---
keyword: access control
---

# Overview

You can create different permissions for different RAM users, and avoid security risks caused by exposing the accesskey of your Alibaba cloud account.

## Scenarios

The following examples describe how to use RAM to implement access control:

-   Grant different permissions to RAM users

    Enterprise A has purchased various Alibaba cloud services, such as Elastic Compute Service \(ECS\) instances, apsaradb for RDS instances, server load balancer \(SLB\) instances, and Object Storage Service \(OSS\) buckets, to migrate A Project-X to the cloud. Certain employees need to perform operations on these cloud resources. Different employees require different permissions to fulfill their duties. Enterprise A has the following requirements:

    -   For security reasons, Enterprise A does not want to disclose the accesskey of its Alibaba Cloud account to its employees. Instead, enterprise A prefers to create different Ram user accounts for its employees and grant different permissions to these user accounts.
    -   The RAM users can only perform operations on resources after they are granted the corresponding permissions. Enterprise A can revoke the permissions granted to Ram users and delete Ram user accounts at any time.
    -   Ram does not need to perform independent metering and billing for Ram users. All expenses are billed to account A.
    You can use the authorization management function of RAM to centrally manage user permissions and resources.

-   Use RAM roles to enable cross-account resource access

    Account A and Account B are created respectively for Enterprise A and Enterprise B. Enterprise A has purchased various Alibaba cloud resources, such as ECS instances, apsaradb for RDS instances, SLB instances, and OSS buckets.

    -   Enterprise A wants to focus on its business system and entrust tasks such as cloud resource O&M, monitoring, and management to Enterprise B.
    -   Enterprise B is allowed to grant access permissions for the resources owned by Enterprise A to one or more employees, implementing fine-grained control on the resources of Enterprise A.
    -   If either party terminates the entrustment agreement, enterprise A can revoke the permissions of Enterprise B at any time.
    RAM roles can be used to implement cross-account authorization and resource access control.


## Policies

The following table lists the system policies supported by ARMS.

|Policy|Type|Description|
|------|----|-----------|
|AliyunARMSFullAccess|System|ARMS full access permissions|
|AliyunARMSReadOnlyAccess|System|ARMS read-only permissions|

## References

-   [Grant different permissions to RAM users](/intl.en-US/Access control/Grant different permissions to RAM users.md)
-   [Use a RAM role to access resources across Alibaba Cloud accounts](/intl.en-US/Access control/Use RAM roles to access resources across Alibaba cloud accounts.md)
-   [What is RAM?](/intl.en-US/Product Introduction/What is RAM?.md)

