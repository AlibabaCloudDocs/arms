# Features

This topic describes the features that are supported by Prometheus Service.

## Prometheus Operator

You can install Prometheus Operator only by using a Helm chart. Relevant documentation provides the command to install the Helm chart. The command contains the version information about Prometheus Operator. For more information, see [Connect a self-managed Kubernetes cluster to Prometheus Service]().

## Prometheus Service console

-   Provides default Kubernetes dashboards, including overview dashboards, pod dashboards, and node dashboards.

## Alerting

-   Allows you to create and maintain alerts by using Custom Resource Definitions \(CRDs\), and enable and disable CRD-based alerts by using Helm commands.
-   Allows you to create alert contacts and modify information about alert contacts.
-   Allows you to use the basic features of PagerDuty. For example, you can enable label pass-through, set severity levels for events, and configure notification for the ending of alert events.

