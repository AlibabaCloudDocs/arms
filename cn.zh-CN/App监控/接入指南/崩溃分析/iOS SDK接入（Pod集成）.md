iOS SDK接入（Pod集成） 
=====================================

本文介绍如何使用Pod集成方式接入崩溃分析服务的iOS SDK。
**说明**



* iOS SDK接入可采用Pod集成和手动集成2种方式。推荐使用Pod集成方式接入崩溃分析服务，可大幅简化接入操作。

  

* 如需使用手动集成方式接入崩溃分析服务的iOS SDK，操作方法参见[iOS SDK接入（手动集成）]()。

  




前提条件 
-------------------------

已下载配置文件，请参见[快速入门：创建监控任务](/cn.zh-CN/App监控/快速入门：创建监控任务.md)。

使用限制 
-------------------------

* 仅支持iOS 8.0及以上的App。

  

* 推荐使用CocoaPods管理依赖的Xcode项目。

  




操作步骤 
-------------------------

1. **添加** **依赖。** 

   1. 指定官方仓库和阿里云仓库。

          source "https://github.com/CocoaPods/Specs.git"
          source "https://github.com/aliyun/aliyun-specs.git"

      
   
   2. 添加崩溃分析服务依赖。

          pod 'AlicloudCrash' , '~> 1.2.0'

      
      **说明**

      执行`pod search AlicloudCrash`命令，查询AlicloudCrash最新版本。
      
   
   3. 执行`pod update`命令，保存设置。

      
   

   

2. **接入服务。** 

   1. 将iOS配置文件AliyunEmasService-Info.plist拷贝至项目根目录。

      
   
   2. 在AppDelegate文件的application:didFinishLaunchingWithOptions方法中初始化SDK。

      引入头文件：

          #import <AlicloudCrash/AlicloudCrashProvider.h>
          #import <AlicloudHAUtil/AlicloudHAProvider.h>

      

      添加代码段：

          NSString *appVersion = @"x.x"; //app版本，会上报。
          NSString *channel = @"xx";     //渠道标记，自定义，会上报。
          NSString *nick = @"xx";        //nick 昵称，自定义，会上报。
          [[AlicloudCrashProvider alloc] autoInitWithAppVersion:appVersion channel:channel nick:nick];
          [AlicloudHAProvider start];

      

      |     参数     |                                                                                                                                                                  说明                                                                                                                                                                  |
      |------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
      | appVersion | 用于指定App的版本，上报至服务端，进行版本区分。 【数据类型】字符串 【格式要求】自定义 【取值范围】任意长度 **说明** 该参数值将在控制台显示为下拉列表选项，建议短小凝练。 【是否必选】是 【是否可为空】否 【默认值】无 【大小写敏感】是。例如，vx.x和Vx.x不是一个版本。 【字符类型】英文大小写、数字。 **说明** 不支持中文字符、特殊字符。 |
      | channel    | 用于指定渠道标识，上报至服务端，进行渠道区分。 【数据类型】字符串 【取值范围】任意长度 【是否必选】是 【是否可为空】否 【默认值】无 【字符类型】英文大小写、数字。 **说明** 不支持中文字符、特殊字符。                                                                                                            |
      | nick       | 用于指定用户昵称，上报至服务端，进行用户区分。后续可能依据该参数，进行数据检索。 【数据类型】字符串 【取值范围】任意长度 【是否必选】是 【是否可为空】否 【默认值】无 【字符类型】英文大小写、数字。 **说明** 不支持中文字符、特殊字符。 【命名规范】自定义                                                                                 |

      
   

   

3. **添加高级设置。** 

   iOS SDK提供接口，用于上报自定义信息或错误。

       //上报自定义信息。
       [AlicloudCrashProvider configCustomInfoWithKey:@"key" value:@"value"];   //配置项：自定义环境信息（configCustomInfoWithKey/value）。
       
       //按异常类型上报自定义信息。
       [AlicloudCrashProvider setCrashCallBack:^NSDictionary * _Nonnull(NSString * _Nonnull type) {
           return @{@"key":@"value"};   //配置项：异常信息（key/value）。
       }];
       
       //上报自定义错误。
       NSError *error = [NSError errorWithDomain:@"customError" code:10001 userInfo:@{@"errorInfoKey":@"errorInfoValue"}];
       [AlicloudCrashProvider reportCustomError:error];   //配置项：自定义错误信息（errorWithDomain/code/userInfo）。

   

   具体说明参见：[iOS SDK接口说明]()
   

4. **编译。** 

   1. 在项目的`Build Setting`中，将`Allow Non-modular Includes In Framework Modules`设置为`YES`。

      
   
   2. 执行编译。

      
   

   
   **说明**

   
   * 编译过程中如出现`duplicate symbol`类型错误，确认本地依赖与CocoaPods管理的依赖是否重复；如是，则删除本地依赖。

     
   
   * 如同时使用其他阿里云产品，可能会因为依赖中存在UTDID冲突，造成编译失败。解决办法参见：[SDK UTDID冲突解决方案](https://help.aliyun.com/document_detail/172616.html)。

     
   

   
   

5. **功能验证。** 

   iOS SDK接入操作完成后，需进行功能验证。
   1. 编写测试代码，模拟或触发移动端崩溃。例如：

          NSMutableArray *array = @[];
          [array addObject:nil];

      
      **说明**

      更多内容参考样例代码。
      
   
   2. 重启移动端大概2分钟后在控制台查看是否显示崩溃信息。

      **说明**

      崩溃数据从采集到上传到控制台显示，存在大约2\~3分钟延迟。
      * 显示崩溃数据：SDK接入成功

        
      
      * 数据未显示：按照c步骤进行排查

        
      

      
   
   3. 在模拟或触发崩溃及重启移动设备期间，使用Charles抓包，查看能否捕获包含`https://adash-emas.cn-hangzhou.aliyuncs.com/upload`的HTTP请求：

      * 捕获：崩溃信息已上报。可能原因：后端未接入；Appkey或Secret信息有误。

        
      
      * 未捕获：崩溃信息未上报。可能原因：SDK接入失败；SDK未捕获崩溃；数据发送失败。请联系[技术支持](/cn.zh-CN/.md)解决。

        
      

      
   

   




样例代码 
-------------------------

崩溃分析服务Android SDK接入工程样例参见：[Demo工程](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo?spm=a2c4g.11186623.2.27.789073c8I6rfk5)
