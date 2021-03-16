iOS SDK接入（手动集成） 
====================================

本文介绍如何使用手动集成方式接入性能分析服务的iOS SDK。
**说明**



* iOS SDK接入可采用Pod集成和手动集成2种方式。推荐使用Pod集成方式接入性能分析服务，可大幅简化接入操作。

  

* 如需使用Pod集成方式接入性能分析服务的iOS SDK，操作方法参见：[iOS SDK接入（Pod集成）](/intl.zh-CN/App监控/接入指南/性能分析/iOS SDK接入（Pod集成）.md)

  




**前提条件** 
-----------------------------

已下载iOS配置文件，具体操作，请参见[快速入门：创建监控任务](/intl.zh-CN/App监控/快速入门：创建监控任务.md)。

**使用限制** 
-----------------------------

* 仅支持iOS 8.0及以上的App。

  




**接入概述** 
-----------------------------

通过iOS SDK接入性能分析服务的操作步骤如下：

1. [准备](#section-88c-455-xxb)：下载SDK包；下载开源库文件。

   

2. [添加依赖](#section-da1-e74-n14)：采用手动方式集成SDK。

   

3. [接入服务](#section-y3e-207-ax2)：接入服务。

   

4. [编译](#section-659-yxm-yim)：修改编译设置。

   




**准备** 
---------------------------

下载SDK包和开源库文件。

**下载SDK包** 

1. 登录移动研发平台的[管理控制台](https://emas.console.aliyun.com/#/productList)，默认打开 **我的工作空间** 页面。

   

2. 在 **我的工作空间** 页面，单击工作空间标签的 **进入** 按钮，打开指定工作空间的概览页面。

   

3. 在工作空间概览页面，单击 **SDK下载** 区域，打开 **SDK下载** 右侧栏。![1 (2)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4367785161/p247489.png)

   

4. 在 **SDK下载** 右侧栏，选择 **性能分析** 复选框，单击 **下载iOS版本** 按钮，下载性能分析服务的iOS SDK包。

   
   **说明**

   在 **SDK列表** 中，单击 **性能分析** 行 **iOS版** 列的版本号链接，查看性能分析iOS SDK更新记录。

   ![图片替换文本](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4220765061/p183018.png)
   

5. 检查SDK包，确保内容完整无缺失。SDK包文件（24个）列表如下：

   




* AliAPMInterface.framework

  

* AlicloudAPM.framework

  

* AlicloudHAUtil.framework

  

* AliCloudNetworkMonitor.framework

  

* AlicloudUtils.framework

  

* AliHACore.framework

  

* AliHADataHub4iOS.framework

  

* AliHADataHubAssembler.framework

  

* AliHADeviceEvaluation.framework

  

* AliHALogEngine.framework

  

* AliHAMemoryMonitor.framework

  

* AliHAMethodTrace.framework

  

* AliHAPerformanceMonitor.framework

  

* AliHAProtocol.framework

  

* AliHASecurity.framework

  

* AliRemoteDebugInterface.framework

  

* BizErrorReporter4iOS.framework

  

* EMASRest.framework

  

* JDYThreadTrace.framework

  

* TBJSONModel.framework

  

* TBRest.framework

  

* UTDID.framework

  

* UTMini.framework

  

* ZipArchive.framework

  




**下载开源库文件** 

性能分析服务须引用的开源库文件包括：

* FBAllocationTracker：[下载](https://github.com/facebook/FBAllocationTracker)

  

* FBMemoryProfiler：[下载](https://github.com/facebook/FBMemoryProfiler)

  

* FBRetainCycleDetector：[下载](https://github.com/facebook/FBRetainCycleDetector)

  




**添加依赖** 
-----------------------------

1. 在Xcode中，将SDK目录中的framework文件拖入Target目录，在弹出框选中 **Copy items if needed** 选项。

   

2. 相同方式引入开源库文件：

   




* FBAllocationTracker

  

* FBMemoryProfiler

  

* FBRetainCycleDetector

  

* rcd_fishhook

  



**说明**

`rcd_fishhook`在`FBRetainCycleDetector`工程目录下。

3. 选择 **Build Phases** \> **Link Binary With Libraries** ，添加Xcode自带的公共包文件：

* libc++.tbd

  

* SystemConfiguration.framework

  




4. 选择 **Build Phases** \> **Compile Sources** ，为下列文件添加Compiler Flags：`-fno-objc-arc`

* FBAssociationManager.mm

  

* FBBlockStrongRelationDetector.m

  

* FBBlockStrongLayout.m

  

* FBClassStrongLayoutHelpers.m

  

* NSObject+FBAllocationTracker.mm

  

* FBAllocationTrackerNSZombieSupport.mm

  




**接入服务** 
-----------------------------

1. 将iOS配置文件`AliyunEmasServices-Info.plist`拷贝至项目根目录。
**说明**

iOS配置文件的获取方式参见：[前提条件](#section-9j5-q9g-jmx)

2. 在`AppDelegate.m`文件的`application:didFinishLaunchingWithOptions`方法中初始化SDK。

引入头文件：

    #import <AlicloudAPM/AlicloudAPMProvider.h>
    #import <AlicloudHAUtil/AlicloudHAProvider.h>



添加代码段：

    NSString *appVersion = @"xxx"; 
    NSString *channel = @"xxx"; 
    NSString *nick = @"xxx";  
    [[AlicloudAPMProvider alloc] autoInitWithAppVersion:appVersion channel:channel nick:nick];
    [AlicloudHAProvider start];



配置说明如下：


|    配置项     |                                                                                                                                                                                      说明                                                                                                                                                                                      |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| appVersion | 用于指定App的版本，上报至服务端，进行版本区分。 【数据类型】字符串 【格式要求】自定义 【取值范围】任意长度 **说明** 该参数值将在控制台显示为下拉列表选项，建议短小凝练。 【是否必选】是 【是否可为空】否 【默认值】无 【大小写敏感】是。例如，vx.x和Vx.x不是一个版本。 【字符类型】英文大小写、数字。 **说明** 该参数不支持中文字符、特殊字符。 【示例】`NSString *appVersion = @"2.3";` |
| channel    | 用于指定渠道标识，上报至服务端，进行渠道区分。 【数据类型】字符串 【取值范围】任意长度 【是否必选】是 【是否可为空】否 【默认值】无 【字符类型】英文大小写、数字。 **说明** 该参数不支持中文字符、特殊字符。 【示例】`NSString *channel = @"appstore";`                                                                                                          |
| nick       | 用于指定用户昵称，上报至服务端，进行用户区分。后续可能依据该参数，进行数据检索。 【数据类型】字符串 【取值范围】任意长度 【是否必选】是 【是否可为空】否 【默认值】无 【字符类型】英文大小写、数字。 **说明** 该参数不支持中文字符、特殊字符。 【命名规范】自定义 【示例】`NSString *nick = @"john";`                                                                      |



**编译** 
---------------------------

1. 在项目的`Build Setting`中，将`Allow Non-modular Includes In Framework Modules`设置为`YES`。

![编译设置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4220765061/p183019.png)

2. 执行编译。
**说明**



* 编译过程中如出现`duplicate symbol`类型错误，确认本地依赖与CocoaPods管理的依赖是否重复；如是，则删除本地依赖。

  

* 如同时使用其他阿里云产品，可能会因为依赖中存在UTDID冲突，造成编译失败。解决办法参见：[SDK UTDID冲突解决方案](https://help.aliyun.com/document_detail/172645.html)

  




**样例代码** 
-----------------------------

性能分析服务iOS SDK接入工程样例参见：[Demo工程](https://github.com/aliyun/alicloud-ios-demo/tree/master/apm_ios_demo "Demo工程")

**功能验证** 
-----------------------------

iOS SDK接入操作完成后，可操作App，查看性能分析服务控制台显示数据，进行功能验证。

1. 手机端：启动App。（2分钟后）控制台：查看 **概览** 页签的 **启动速度** 是否显示数据。

   

2. 手机端：在App中跳转几个页面。（2分钟后）控制台：查看 **概览** 页签的 **加载时间** 是否显示数据。

   



**说明**

数据从App采集到控制台显示，存在大约2分钟延迟。

如数据显示正常，则iOS SDK接入成功。

否则，可能的原因是：SDK接入失败、SDK未获取数据、数据发送失败、后端问题，请联系[技术支持](/intl.zh-CN/.md)解决。
