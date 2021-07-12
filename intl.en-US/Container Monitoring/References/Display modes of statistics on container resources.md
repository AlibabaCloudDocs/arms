# Display modes of statistics on container resources

Container monitoring displays the statistics on container resources that are in different states by using different colors and graphic sizes. This topic describes the states of container resources and how their statistics are displayed.

## Display modes

Container monitoring uses different colors and graphic sizes to distinguish between container resources in different states.

-   Colors:
    -   Blue: indicates that the container resource is normal.
    -   Orange: indicates that the container resource is abnormal and a warning alert is generated. For more information about the conditions that trigger alerts, see [Trigger conditions of alerts](#section_zif_bv5_hfo).
    -   Red: indicates that the container resource is abnormal and a fatal alert is generated. For more information about the conditions that trigger alerts, see [Trigger conditions of alerts](#section_zif_bv5_hfo).
-   Graphic sizes: The size of a graphic for a type of container resources indicates the number of the container resources in a specific state, as shown in the following figure.

    ![Container monitoring - Resource overview - Namespace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5200544261/p254105.png)


## Trigger conditions of alerts

The trigger conditions of alerts vary with the types of container resources.

|Resource type|Alert severity|Trigger condition|
|-------------|--------------|-----------------|
|Service|Warning|-   A request error occurs.
-   The average response time is greater than 500 ms.
-   No Server Load Balancer \(SLB\) instance is specified for the Service. This condition does not apply to headless Services. |
|Ingress|Warning|No SLB instance is specified for the Ingress.|
|Deployment|Warning|-   A request error occurs.
-   The average response time is greater than 500 ms.
-   `spec.Replicas != status.AvailableReplicas` |
|StatefulSet|Warning|-   A request error occurs.
-   The average response time is greater than 500 ms.
-   `spec.Replicas != status.ReadyReplicas` |
|DaemonSet|Warning|-   A request error occurs.
-   The average response time is greater than 500 ms.
-   `#nodes != status.NumberReady` |
|Pod|Fatal|`phase == Failed`|
|Warning|-   A request error occurs.
-   The average response time is greater than 500 ms.
-   The CPU utilization is greater than 70%.
-   The memory usage is greater than 70%.
-   `Type=Ready & Status == False` |
|Container|Warning|-   A request error occurs.
-   The average response time is greater than 500 ms.
-   The CPU utilization is greater than 70%.
-   The memory usage is greater than 70%.
-   `ready == false`
-   The container is restarted at least once within the past 24 hours. |
|Node|Fatal|-   `Type == Ready && Status == False`
-   `Type == NetworkUnavailable && Status == True` |
|Warning|-   The CPU utilization is greater than 70%.
-   The memory usage is greater than 70%.
-   `Type == MemoryPressure | DiskPressure | PIDPressure & Status == True` |

## Contact us

If you have questions when you use container monitoring, you can join the official DingTalk group for container monitoring \(group ID: `31588365`\) to seek help.

