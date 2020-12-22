# FAQ about updating the ARMS agent for Java applications

This topic describes how to update the Application Real-Time Monitoring Service \(ARMS\) agent for monitoring Java applications in Enterprise Distributed Application Service \(EDAS\) and Container Service, and on other platforms.

## How do I update the ARMS agent for applications in EDAS?

To update the ARMS agent for Java applications in EDAS, re-deploy the applications.

## How do I update the ARMS agent for applications in Container Service?

To update the ARMS agent for applications in Container Service, restart the pods of the applications.

## How do I update the ARMS agent for applications on other platforms?

To update the ARMS agent for other applications than those in EDAS and Container Service, uninstall the ARMS agent and then install it again.

To uninstall the ARMS agent, perform the following steps as needed:

-   Uninstall the ARMS agent for Java applications on Elastic Compute Service \(ECS\) instances

-   Uninstall the ARMS agent for Java applications on other platforms

    Delete the parameters related to AppName and LicenseKey in the configuration file or startup script. For more information, see[t152228.md\#uninstall](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for a Java application.md) .


