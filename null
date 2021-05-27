# 使用ARMS监控异步任务

ARMS默认支持监控通过Spring @Async标签实现的异步任务，同时还可以通过添加异步透传扫描包和使用ARMS SDK进行手动透传对自定义异步任务实现监控。若您的异步任务出现接口超时等异常，可以通过调用链路查看详细异常堆栈信息以便及时处理潜在问题。

该功能要求ARMS探针版本为公测版本v2.7.1.2及以上。如果您是EDAS或者ACK用户，请联系ARMS钉钉服务账号arms160804，为您进行探针新版本升级。

## 方式一：默认支持Spring @Async标签

ARMS默认支持监控使用Spring @Async标签实现的异步任务。对于下列Spring框架中默认的Executor和Task，ARMS会自动完成增强：

-   Executor：
    -   org.springframework.scheduling.concurrent.ConcurrentTaskExecutor
    -   org.springframework.core.task.SimpleAsyncTaskExecutor
    -   org.springframework.scheduling.quartz.SimpleThreadPoolTaskExecutor
    -   org.springframework.core.task.support.TaskExecutorAdapter
    -   org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor
    -   org.springframework.scheduling.concurrent.ThreadPoolTaskScheduler
    -   org.springframework.jca.work.WorkManagerTaskExecutor
    -   org.springframework.scheduling.commonj.WorkManagerTaskExecutor
-   Task：
    -   org.springframework.aop.interceptor.AsyncExecutionInterceptor$1
    -   org.springframework.aop.interceptor.AsyncExecutionInterceptor$$Lambda$

## 方式二：添加异步透传扫描包

您可以选择在应用设置中添加异步透传扫描包实现异步任务监控。异步透传扫描包中的Runnable、Callable和Supplier接口在创建新对象时会自动捕获当前线程调用链的上下文，并在异步线程中执行时使用该调用链上下文，完成串联。

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏，选择**应用监控** \> **应用列表**。

3.  在顶部菜单栏，选择地域。

4.  在**应用列表**页面，单击应用名称。

5.  在左侧导航栏，单击**应用设置**，然后单击**自定义配置**页签。

6.  在高级设置区域的异步透传扫描包名对话框中，添加异步透传扫描包。


**说明：** 配置后需重启应用才能使功能生效。如需添加多个异步透传扫描包，可以使用半角逗号（,）分隔。

## 方式三：使用ARMS SDK手动透传

当您的使用方式比较复杂，上述场景无法满足需求时，您还可以选择使用ARMS SDK进行手动透传。通过手动增强Runnable接口、Callable接口和Executor，在异步线程中完成调用链串联，实现异步任务监控。

1.  在Maven项目的pom.xml中添加以下依赖。

    ```
    <dependency>
     <groupId>com.alibaba.arms.apm</groupId>
     <version>1.7.5</version>
     <artifactId>arms-sdk</artifactId>
    </dependency>
    ```

2.  增强Runnable接口、Callable接口和Executor。您可以按需选择以下任意一种增强方式。

    -   **方式一：增强Runnable接口和Callable接口**

        使用`TraceRunnable.asyncEntry()`增强Runnable接口，使用`TraceCallable.asyncEntry()`增强Callable接口。示例代码如下：

        ```
        public class AsyncEntryExample {
        
            private final ExecutorService executor = Executors.newSingleThreadExecutor();
        
            @GetMapping(value = "/sdk-async-plugin/asyncEntry-propagation")
            public String asyncEntryAndExecute() throws Exception {
                CompletableFuture<String> future = new CompletableFuture<>();
                Runnable command = TraceRunnable.asyncEntry(() -> future.complete("asyncEntry-execute"));
                executor.execute(command);
                Thread.sleep(1000);
                return future.get();
            }
        }
        ```

    -   **方式二：增强Executor**

        使用`TraceExecutors.wrapExecutorService(executr, true)`增强Executor。示例代码如下：

        ```
        public class AutoExample {
        
            private final ExecutorService contextPropagationExecutor
                    = TraceExecutors.wrapExecutorService(Executors.newSingleThreadExecutor(), true);
        
            @GetMapping(value = "/sdk-async-plugin/auto-context-propagation")
            public String autoWrapAndExecute() throws Exception {
                CompletableFuture<String> future = new CompletableFuture<>();
                contextPropagationExecutor.execute(() -> future.complete("auto-execute"));
                Thread.sleep(1000);
                return future.get();
            }
        }
        ```

    -   **方式三：同时增强Runnable接口、Callable接口和Executor**

        示例代码如下：

        ```
        public class ManualExample {
            private final ExecutorService traceExecutor
                    = TraceExecutors.wrapExecutorService(Executors.newSingleThreadExecutor());
        
            @GetMapping(value = "/sdk-async-plugin/manual-context-propagation")
            public String manualWrapAndExecute() throws Exception {
                CompletableFuture<String> future = new CompletableFuture<>();
                traceExecutor.execute(TraceRunnable.wrap(() -> future.complete("manual-execute")));
                traceExecutor.execute(() -> "Not captured");
                Thread.sleep(1000);
                return future.get();
            }
        }
        ```


配置完成后，您可以在调用链路详情页查看异步任务的调用链详情。具体详情，请参见[调用链路查询](/intl.zh-CN/应用监控/控制台功能/调用链路查询.md)。

![异步调用详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5381012261/p278209.png)

