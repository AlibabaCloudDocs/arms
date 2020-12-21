---
keyword: [ARMS, thread, thread profiling, profiling]
---

# Thread profiling

The thread profiling feature provides statistics on the CPU time consumption at the thread level and the number of threads per type. ARMS records and aggregates the method stacks of threads every 5 minutes, which helps you review the code execution process and find out thread problems. When the CPU utilization of a cluster is high or a large number of slow methods are detected, the thread profiling feature can be used to find out the thread or method that consumes the most CPU resources.

## Procedure

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

2.  On the Applications page, click the name of the application.

3.  In the left-side navigation pane, choose **Application Diagnosis** \> **Threads Profiling**.


## Perform thread profiling

On the Threads Profiling page, all threads of the application are listed on the left. You can detect abnormal threads based on statistics in the **CPU Time Consumption \(ms\)** section. Select an abnormal thread and analyze the changes of the CPU time consumption and thread count based on the graphs in the **CPU Time Consumption \(ms\)** and **Thread Count** sections. For example, you can analyze whether the total number of threads per minute is overlarge.

![pg_am_threads_profiling](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5289262851/p82887.png)

You can also click **Method Stack** to view the method stack that is actually running within a specified period of time. For example, you can view the method stack of the threads in the BLOCKED state and optimize the specified code block to reduce CPU utilization.

![pg_am_method_stack](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5289262851/p84725.png)

**Note:** If no data appears after you click **Method Stack**, click **Application Settings** in the left-side navigation pane. On the page that appears, click the Custom Configuration tab and check whether **Thread Profiling Method Stack** in the Thread settings section is turned on. If Thread Profiling Method Stack is turned off, the method stack information cannot be recorded. If Thread Profiling Method Stack is turned on, the method stack information is collected every 5 minutes.

**Related topics**  


[Analyze errors in code by using ARMS thread profiling](/intl.en-US/Application monitoring/Tutorials/Analyze errors in code by using ARMS thread profiling.md)

