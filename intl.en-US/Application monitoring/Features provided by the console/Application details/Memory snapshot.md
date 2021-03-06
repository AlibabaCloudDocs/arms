---
keyword: [ARMS, JVM, memory analysis, Memory Analyzer]
---

# Memory snapshot

JVM monitoring can display multiple memory metrics within a specified period of time. However, although the charts can reflect excessive memory usage, specific information cannot be displayed. Therefore, it cannot help you to troubleshoot problems. You can create a memory snapshot and view detailed memory usage in logs. This can help you troubleshoot memory problems such as memory leakage and memory waste.

## Create memory snapshot

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.
3.  On the Applications page, click the name of the application that you want to manage.
4.  In the left-side navigation pane, click **Application Details**, and click **JVM Monitoring** tab on the right side.

    ![jvm_1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4312658061/p203846.png)

5.  In the upper-right corner of the JVM Monitoring tab, click **Create Memory Snapshot**.

    **Note:** When you click **Create Memory Snapshot**, if the previous snapshot task is still running, an error message is prompted. Wait until the previous snapshot task is finished. You can only create memory snapshots for the Linux system.

6.  In the Create Memory Snapshot dialog box, select an IP address and click **Save**.

    **Warning:** The running time of a snapshot task varies from a few minutes to half an hour. The application stops responding during a dump. Proceed with caution.

    **Note:** If you have selected an instance on the left side of the Application Details page, the IP address of the instance is selected by default in the **IP** field.


## View memory snapshot details

1.  In the upper-right corner of the JVM Monitoring tab, click **Historical Snapshots**.

    The Number of Snapshot Jobs section displays the task execution status. Green indicates that the snapshot task is successful, blue indicates that the snapshot task is executing, and red indicates that the snapshot task fails.

    The name of a snapshot task contains the following information:

    -   Memory analysis status
    -   The ID of the snapshot task. It consists of an IP address and a timestamp.
    -   Snapshot creation time
    ![ARMS JVM Monitoring-memory snapshot history](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0140458061/p43133.png)

2.  Click **Start Analysis**. In the Note message, click **OK**.

3.  Click **Analysis Results**. On the memory analysis page that appears, you can view memory analysis details. This can help you troubleshoot memory leaks and reduce memory waste.

    -   Click the Overview tab to view the heap usage, the number of classes, the number of objects, the number of class loaders, and the number of root objects. You can also view the memory usage displayed in a circular bar.
    -   Click the Leakage Report tab to view suspicious memory-consuming objects. Click **Problem Suspect** at the lower part of the page to view the corresponding instances, memory usage, and class loading information of a suspect object.
    -   Click the GC Root Object tab to view all root objects classified by root type and Java class type. Root objects are objects referenced by the GC root, such as static variables or threaded stacks
    -   Click the Dominator Tree tab to view the dominator relationships among objects in a heap. You can identify objects that consume large amounts of memory and their object dependencies.
    -   Click the Class View tab to view the heap usage and the number of instances for each heap type.
    -   Click the Unreachable Class View tab to view the size and type of objects that are not referenced in the heap.
    -   Click the Duplicate Class View tab to view the type of objects loaded by multiple class loaders.
    -   Click the Class Loader View tab to view all class loaders used by the application and the loaded classes, such as the types of loaded classes and the number of instances in a class.
    -   Click the Off-heap Memory View tab to view all java.nio.DirectByteBuffer and off-heap memory information used by applications. You can use this information to troubleshoot excessive physical memory consumption caused by the off-heap memory.
    -   Click the System Properties tab to view system parameters and environment variables.
    -   Click the Thread Information tab to view thread information such as thread name, heap usage, call stack information, and local variables. You can use this view to analyze problems such as too many threads, deadlocks, and deep call stacks.
    -   Click the OQL tab to view heap information such as all strings greater than 2,000 characters in length.

