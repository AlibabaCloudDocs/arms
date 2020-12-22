# Monitor applications deployed in open source Kubernetes environments

The business transaction feature provided by ARMS allows you to define business requests in a visualized manner by using non-intrusive methods and provides abundant business-specific performance metrics and diagnostic capabilities. Before you use the business transaction feature, you must install or upgrade the ARMS agent for Java applications.

## Limits

-   The business transaction feature only can monitor Java applications.
-   Only the ARMS agent V2.6.2 or later supports the business transaction feature.

## Install the ARMS agent for applications in open source Kubernetes environments

If you are using the business transaction feature for the first time and have not used the application monitoring feature, you must install the latest version of the ARMS agent. For more information, see [Install the ARMS agent for an application deployed in an open source Kubernetes environment](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for an application deployed in an open source Kubernetes environment.md).

## Upgrade the ARMS agent for applications in open source Kubernetes environments

If you are using the business transaction feature for the first time and have used the application monitoring feature, you must upgrade the ARMS agent to V2.6.2 or later. To upgrade the ARMS agent, you must uninstall the existing ARMS agent and install a new one.

Perform the following steps:

1.  Uninstall the existing ARMS agent. For more information, see [Uninstall the ARMS agent](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for an application deployed in an open source Kubernetes environment.mdsection_anc_ksu_mmw).

2.  Install a new ARMS agent. For more information, see [Install the ARMS agent for an application deployed in an open source Kubernetes environment](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for an application deployed in an open source Kubernetes environment.md).

3.  Restart your business pod.

    The ARMS agent is automatically updated.

4.  Run the `cat /home/admin/.opt/ArmsAgent/version` command in the container to check the version of the ARMS agent.

    If the version number starts with 2.6.2, the ARMS agent has been upgraded to V2.6.2 or later. You can create a business transaction task to monitor your applications.


