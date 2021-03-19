# Diagnostics by Arthas

Arthas is a tool that enables developers to diagnose online issues of Java applications. It adopts the bytecode enhancement technology, which allows developers to check the status of applications without the need to restart the running Java virtual machine \(JVM\) processes. The Application Real-Time Monitoring Service \(ARMS\) console supports the general features of Arthas. Such features include JVM overview, time consumption analysis for threads, analysis of function execution, and performance analysis.

Before you use Arthas to diagnose an application, make sure that the following requirements are met:

-   The application is monitored by ARMS. For more information, see [Overview](/intl.en-US/Application Monitoring/Quick start/Overview.md).
-   The application is deployed in a Kubernetes cluster.

    **Note:** This topic uses Container Service for Kubernetes \(ACK\) as an example.

-   The application is developed in Java.
-   Port 3658 or 8563 is not occupied.

Arthas is an open source Java diagnostics tool developed by Alibaba Cloud. It is popular among developers. For more information about Arthas, see the [Arthas Documentation](https://arthas.aliyun.com/doc/en/).

## Upgrade arms-pilot and restart your application

Before you use Arthas to diagnose your application, you must upgrade arms-pilot and restart your application.

To upgrade arms-pilot for an ACK cluster and restart an application, perform the following steps:

1.  Upgrade arms-pilot.

    1.  Log on to the [ACK console](https://cs.console.aliyun.com/).

    2.  In the left-side navigation pane, click **Clusters**.

    3.  On the **Clusters** page, click the name of the cluster that you want to manage, or click **Details** in the **Actions** column of the cluster.

    4.  In the left-side navigation pane, choose **Workloads** \> **Deployments**.

    5.  On the **Deployments** page, select arms-pilot-system or arms-pilot from the **Namespace** drop-down list. Find the deployment where the ARMS agent is installed and choose **More** \> **Redeploy** in the **Actions** column.

    6.  In the **Redeploy** message, click **Confirm**.

2.  If the process identifier \(PID\) of the application is 1, add an annotation of ArthasEnable: "on" to the spec/template/metadata path in the YAML configuration file of the application.

    1.  On the **Deployments** page, select the namespace of the application from the **Namespace** drop-down list. Find the deployment that you want to manage and choose **More** \> **Edit Annotations** in the **Actions** column.

    2.  In the **Edit** dialog box, click the plus icon, enter ArthasEnable in the **Name** field and on in the **Value** field, and then click **OK**.

3.  Restart the application.

    1.  On the **Deployments** page, select the namespace of the application from the **Namespace** drop-down list. Find the deployment that you want to manage and choose **More** \> **Redeploy** in the **Actions** column.

    2.  In the **Redeploy** message, click **Confirm**.


## Go to the Arthas Diagnosis page

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  In the left-side navigation pane, choose **Application Diagnosis** \> **Application Diagnosis-Arthas Diagnosis**.

6.  On the Arthas Diagnosis page, select the pod of the application.

    -   If Arthas has not been downloaded, you must redeploy the ARMS agent to download Arthas. For more information, see [Step 1](#step_yrk_ul5_ywh).
    -   If Arthas has not been mounted, ARMS automatically redeploys the application to mount Arthas to the application. You can also manually redeploy the application. For more information, see [Step 3](#step_uyy_p4u_17w).
    -   If the attempt to mount Arthas failed, you must check the PID of the application and perform one of the following operations as required:
        -   If the application PID is 1, modify the YAML configuration file of the application. For more information, see [Step 2](#step_fbo_ip4_7ab).
        -   If the application PID is not 1, contact the ARMS team for technical support. For more information, see [t152375.md\#](/intl.en-US/.md).

## JVM overview tab

On the JVM overview tab, you can view the JVM information about the application, including the statistics on JVM memory and the information about the operating system and variables. This tab provides an overview of the JVM of the application.

1.  By default, after you go to the Arthas Diagnosis page, the **JVM overview** tab appears. The **JVM overview** tab displays information in the following sections:

    -   **JVM Memory**: the information about JVM memory, such as the usage of heap memory and non-heap memory and the information about garbage collection \(GC\).
    -   **Operating system information**: the information about the operating system, such as the average system load, the name and version of the operating system, and the Java version.
    -   **Variable information**: the information about system variables and environment variables.
    -   **Thread TOP-10**: the information about the 10 threads with highest CPU utilization, including the name, ID, CPU utilization, and status of each thread.

        To view the stack information about a thread, click **View** in the **Actions** column of the thread.


## Thread time-consuming analysis tab

On the Thread time-consuming analysis tab, you can view all the threads of the application and the stack information about each thread. This tab helps you efficiently identify the threads that consume a long time.

1.  On the Arthas Diagnosis page, click the **Thread time-consuming analysis** tab.

    The **Thread time-consuming analysis** tab displays all the threads of the application sorted by CPU utilization in descending order. This tab also displays the details of each thread, including the name, ID, CPU utilization, and status.

2.  To view the stack information about a thread, click **View** in the **Actions** column of the thread.


## Method execution analysis tab

On the Method execution analysis tab, you can view the information about a function execution that is randomly captured by the system, such as the duration, input parameters, and return value. You can also drill down to an internal function that is executed within the function. The analysis of function execution is applicable to scenarios in which a function execution is difficult to reproduce in the offline environment or logs are missing.

1.  On the Arthas Diagnosis page, click the **Method execution analysis** tab.

2.  On the **Method execution analysis** tab, select a service and click **OK**.

    **Note:** After you select a service, ARMS attempts to identify the class and function that the service code corresponds to. If the attempt fails, you must specify the corresponding class and function.

    The details tab of a function displays the information about a random execution of the function, including the name, duration, input parameters, errors, and internal functions. The internal function whose execution consumes the most time is highlighted in red in the Timeline\(ms\) column.

3.  To drill down to an internal function, click **Drill in** in the **Actions** column of the internal function.

    The details tab of an internal function displays the information about the captured execution of the internal function, including the name, duration, input parameters, errors, and deeper-level internal functions. The deeper-level internal function whose execution consumes the most time is highlighted in red in the Timeline\(ms\) column.

4.  To set filter conditions for capturing a specific function execution, perform the following steps:

    1.  On the details tab of the selected function, click **Modify diagnostic parameters** in the upper-right corner.

    2.  In the **Diagnostic parameter setting** dialog box, set the parameters as required and click **OK**.

        |Parameter|Description|Example|
        |---------|-----------|-------|
        |Only when an exception is thrown|Specifies whether to capture only a function execution that returns an error. Valid values:        -   True: captures only a function execution that returns an error.
        -   False: captures a function execution regardless of whether it returns an error.
|False|
        |Time consuming is greater than|The execution duration. A function execution can be captured only when its duration exceeds the specified value. Unit: ms.|30|
        |Object deserialization level|The deserialization level of a function execution whose parameters and return value are complex objects. A greater value indicates a deeper deserialization level, which means that more internal fields of complex objects can be displayed.|5|
        |Add parameters|The filter condition to set an limit on the parameters of a function execution. Example:        -   Sample function: The `createOrder` function is used as an example. This function contains the following code snippet:

            ```
class User {
    private int userId;
    private String userName;
    private boolean isVIP;
    }
    public void createOrder(User user, String productId, double price)
            ```

        -   Sample filter condition: Capture a function execution whose `userId` parameter is set to 8753.
        -   Sample parameter configuration: params\[0\].userId ; = ; 8753.
|params\[0\].userId ; = ; 8753|

    3.  Click the ![Refresh icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0573825161/p245128.png) icon.

        Then, the details tab of the selected function displays the information about the function execution that meets the filter conditions.

5.  To view the source code of the function, click **View method source code** in the upper-right corner of the details tab.

    The execution duration of each internal function is displayed in the annotations of the source code. The internal function whose execution consumes the most time is highlighted in red in the source code.


## Performance analysis tab

On the Performance analysis tab, you can generate a flame graph based on the collected samples within a specific period, such as CPU time consumption and memory allocation. The flame graph helps you efficiently identify the performance bottlenecks of the application.

1.  On the Arthas Diagnosis page, click the **Performance analysis** tab.

2.  On the **Performance analysis** tab, click **New flame graph** in the upper-right corner.

3.  In the **New flame graph** dialog box, select a sampling object type, specify a sampling duration, enter a description, and then click **OK**.

    |Parameter|Description|Example|
    |---------|-----------|-------|
    |Flame graph type|The type of the sampling objects. Valid values:    -   cpu time consuming
    -   Memory allocation
    -   Lock time consuming
    -   itimer
|cpu time consuming|
    |Input sampling time \(unit: second\)|The sampling duration. Valid values: 10 to 1800.|30|

    Then, the **Performance analysis** tab displays the task information about the generated flame graph, such as the time when the task started, the time consumed for sampling, and the pod where the task was run.

    ![Performance analysis](../images/p245049.png)

4.  On the **Performance analysis** tab, find the task for which you want to view the flame graph and click **View the flame graph** in the **Task status** column. Download the flame graph in the SVG format as prompted and open the SVG file in the browser to view the flame graph.

    ![Flame graph](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0573825161/p245047.png)


