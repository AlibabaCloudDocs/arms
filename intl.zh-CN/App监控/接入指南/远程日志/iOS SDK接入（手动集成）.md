iOS SDK接入（手动集成） 
====================================

本文介绍如何通过手动集成方式添加依赖接入远程日志服务。
**说明**



* 接入远程日志服务的iOS SDK可采用Pod集成和手动集成2种方式添加依赖。推荐使用Pod集成方式添加依赖，可大幅简化接入操作。

  

* 如需使用Pod集成方式添加依赖，操作方法参见：[iOS SDK接入（Pod集成）](/intl.zh-CN/App监控/接入指南/远程日志/iOS SDK接入（Pod集成）.md)

  




前提条件 
-------------------------

已下载iOS配置文件，具体操作，请参见[快速入门：创建监控任务](/intl.zh-CN/App监控/快速入门：创建监控任务.md)。

使用限制 
-------------------------

* 仅支持iOS 8.0及以上的App。

  

* 日志在手机端上最多存储7天。

  




接入概述 
-------------------------

1. [准备](#section-iqt-3k8-wix)：下载SDK包。

   

2. [添加依赖](#section-f48-x1u-5bn)：采用手动集成方式。

   

3. [接入服务](#section-ek1-jis-fjw)：添加iOS配置文件；引入头文件；初始化SDK；设置日志拉取级别。

   

4. [执行编译](#section-rgt-nkx-aor)：添加编译设置。

   

5. [打印日志](#section-45i-qor-oqy)：在业务代码中输出日志信息。

   




准备 
-----------------------

1. 登录移动研发平台的[管理控制台](https://emas.console.aliyun.com/#/productList)，默认打开 **我的工作空间** 页面。

   

2. 在 **我的工作空间** 页面，单击工作空间标签的 **进入** 按钮，打开指定工作空间的概览页面。

   

3. 在工作空间概览页面，单击 **SDK下载** 区域，打开 **SDK下载** 右侧栏。![1 (2)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4367785161/p247489.png)

   

4. 在 **SDK下载** 右侧栏，选择 **远程日志** 前的复选框，单击 **下载iOS版本** 按钮，下载远程日志的SDK包。

   
   **说明**

   在 **远程日志** 行的 **iOS版** 列，单击版本号链接，可查看版本变更记录。

   ![iOS SDK](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2841036061/p181539.png)
   

5. 检查SDK包，确保内容完整无缺失。

   SDK包文件列表如下：
   




* AlicloudHAUtil.framework

  

* AlicloudTLog.framework

  

* AlicloudUtils.framework

  

* AliHACore.framework

  

* AliHALogEngine.framework

  

* AliHAMethodTrace.framework

  

* AliHAProtocol.framework

  

* AliHASecurity.framework

  

* AliyunOSSiOS.framework

  

* RemoteDebugChannel.framework

  

* TBJSONModel.framework

  

* TBRest.framework

  

* TRemoteDebugger.framework

  

* UTDID.framework

  

* UTMini.framework

  

* ZipArchive.framework

  




添加依赖 
-------------------------

1. 在Xcode中，将SDK目录中的framework文件拖入Target目录，在弹出框选中`Copy items if needed`选项。

   

2. 选择 **Build Phases** \> **Link Binary With Libraries** ，添加Xcode自带的公共包文件：

   




* libc++.tbd

  

* libresolv.tbd

  

* SystemConfiguration.framework

  




接入服务 
-------------------------

1. 将iOS配置文件`AliyunEmasServices-Info.plist`拷贝至项目根目录。

   iOS配置文件获取方式参见：[前提条件](#section-og0-e1z-b5e)
   

2. 在`AppDelegate.m`文件中引入头文件：

       #import <AlicloudTLog/AlicloudTlogProvider.h>
       #import <AlicloudHAUtil/AlicloudHAProvider.h>
       #import <TRemoteDebugger/TRDManagerService.h>

   

3. 在`AppDelegate.m`文件的`application:didFinishLaunchingWithOptions`方法中，添加代码段，初始化SDK。

       NSString *appVersion = @"x.x"; //配置项：App版本
       NSString *channel = @"xx"; //配置项：渠道标记
       NSString *nick = @"xx"; //配置项：用户昵称
       [[AlicloudTlogProvider alloc] autoInitWithAppVersion:appVersion channel:channel nick:nick];
       [AlicloudHAProvider start];
       [TRDManagerService updateLogLevel:TLogLevelXXX]; //配置项：控制台可拉取的日志级别

   




参数说明：


|      参数      |                                                                                                                                                                                                                                                                              说明                                                                                                                                                                                                                                                                               |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| appVersion   | 用于指定App的版本，上报至服务端，进行版本区分。 【数据类型】字符串 【格式要求】自定义 【取值范围】任意长度。 **说明** 该参数值将在控制台显示为下拉列表选项，建议短小凝练。 【是否必选】是 【是否可为空】否 【默认值】无 【大小写敏感】是。例如，vx.x和Vx.x不是一个版本。 【字符类型】英文大小写、数字。 **说明** 该参数不支持中文字符、特殊字符。 【示例】`NSString *appVersion = @"1.0"; `                                                                                                                                                                                |
| channel      | 用于指定渠道标识，上报至服务端，进行渠道区分。 【数据类型】字符串 【取值范围】任意长度 【是否必选】是 【是否可为空】否 【默认值】无 【字符类型】英文大小写、数字。 **说明** 该参数不支持中文字符、特殊字符。 【示例】`NSString *channel = @"appstore";`                                                                                                                                                                                                                                                                                           |
| nick         | 用于指定用户昵称，上报至服务端，进行用户区分。后续可能依据该参数，进行数据检索。 【数据类型】字符串 【取值范围】任意长度 【是否必选】是 【是否可为空】否 【默认值】无 【字符类型】英文大小写、数字。 **说明** 该参数不支持中文字符、特殊字符。 【命名规范】自定义 【示例】`NSString *nick = @"wldtest";`                                                                                                                                                                                                                                                    |
| TLogLevelXXX | 用于设置控制台可拉取的日志级别。日志级别说明参见：[术语解释]() 【数据类型】枚举型 【取值范围】 * TLogLevelError：拉取Error级别的日志。   * TLogLevelWarn：拉取Warn和Error级别的日志。   * TLogLevelInfo：拉取Warn、Error和Info级别的日志。   * TLogLevelDebug：拉取Warn、Error、Info和Debug级别的日志。    【是否必选】否 【默认取值】TLogLevelInfo 【示例】`[TRDManagerService updateLogLevel:TLogLevelInfo];` |


**说明**

推荐使用`autoInitWithAppVersion`接口接入服务。如需使用`initWithAppKey`接口接入服务，须手动配置`appKey`、`secret`和`tlogRsaSecret`参数。

打开iOS配置文件，查询参数取值：


|      参数       |          配置文件字段           |    说明    |
|---------------|---------------------------|----------|
| appKey        | emas.appKey               | App标识。   |
| secret        | emas.appSecret            | App认证信息。 |
| tlogRsaSecret | appmonitor.tlog.rsaSecret | 远程日志公钥。  |



![8E1483EC-CB20-45B3-BB90-12F43F4D7B4B ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7171625061/p181780.png)![A8CBDA37-F704-4B5E-818F-405E04ECE5CB ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7171625061/p181778.png)

执行编译 
-------------------------

1. 在项目的Build Setting中，将`Allow Non-modular Includes In Framework Modules`设置为`YES`。

   ![编译设置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2841036061/p181541.png)
   

2. 执行编译。

   



**说明**



* 编译过程中如出现`duplicate symbol`类型错误，确认本地依赖与CocoaPods管理的依赖是否重复；如是，则删除本地依赖。

  

* 如同时使用其他阿里云产品，可能会因为依赖中存在UTDID冲突，造成编译失败。解决办法参见：[SDK UTDID冲突解决方案](https://help.aliyun.com/document_detail/172653.html)

  




打印日志 
-------------------------

1. 如业务流程触发日志输出，需引入头文件：

       #import <TRemoteDebugger/TLogBiz.h>
       #import <TRemoteDebugger/TLogFactory.h>
       #import <TRemoteDebugger/TRDManagerService.h>

   

2. 在适当位置添加代码，输出日志信息。示例代码：

       TLogBiz *log = [TLogFactory createTLogForModuleName:@"YourModuleName"];
       [log error:@"error message"];
       [log warn:@"warn message"];
       [log debug:@"debug message"];
       [log info:@"info message"];

   




|              选项               |                                  说明                                  |
|-------------------------------|----------------------------------------------------------------------|
| YourModuleName                | 指定保存日志信息的模块的名称。                                                      |
| error/warn/debug/info message | 根据实际场景，区分级别输出日志信息，便于后续按照级别进行日志信息查询。日志级别说明参见：[术语解释]() |



样例代码 
-------------------------

远程日志服务iOS SDK接入工程样例参见：[Demo工程](https://github.com/aliyun/alicloud-ios-demo/tree/master/tlog_ios_demo "Demo工程")
