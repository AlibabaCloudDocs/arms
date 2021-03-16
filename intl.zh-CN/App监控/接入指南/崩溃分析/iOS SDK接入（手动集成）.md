iOS SDK接入（手动集成） 
====================================

本文介绍如何使用手动集成方式接入崩溃分析服务的iOS SDK。

前提条件 
-------------------------

* 已下载应用配置文件，请参见[快速入门：创建监控任务](/intl.zh-CN/App监控/快速入门：创建监控任务.md)。

  

* 已下载崩溃分析SDK，请参见[下载SDK](https://help.aliyun.com/document_detail/169962.html#title-fvd-ozh-524)。

  




使用限制 
-------------------------

仅支持iOS 8.0及以上的App。

操作步骤 
-------------------------

1. **集成SDK。** 

   1. 在Xcode中，将下载好的SDK目录中的framework文件拖入Target目录，在弹出框选中`Copy items if needed`选项。

      
   
   2. 打开 **Build Phases \> Link Binary With Libraries** ，添加Xcode自带的公共包文件：

      * libc++.tbd

        
      
      * SystemConfiguration.framework

        
      

      
   

   

2. **接入服务。** 

   1. 将iOS配置文件`AliyunEmasServices-Info.plist`拷贝至项目根目录。

      
   
   2. 在`AppDelegate.m`文件的`application:didFinishLaunchingWithOptions`方法中初始化SDK。

      引入头文件：

          #import <AlicloudCrash/AlicloudCrashProvider.h>
          #import <AlicloudHAUtil/AlicloudHAProvider.h>

      

      添加代码段：

          NSString *appVersion = @"x.x"; //app版本，会上报。
          NSString *channel = @"xx";     //渠道标记，自定义，会上报。
          NSString *nick = @"xx";        //nick 昵称，自定义，会上报。
          [[AlicloudCrashProvider alloc] autoInitWithAppVersion:appVersion channel:channel nick:nick];
          [AlicloudHAProvider start];

      

      参数说明：
      

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

        
      
      * 未捕获：崩溃信息未上报。可能原因：SDK接入失败；SDK未捕获崩溃；数据发送失败。请联系[技术支持](/intl.zh-CN/.md)解决。

        
      

      
   

   




样例代码 
-------------------------

崩溃分析服务Android SDK接入工程样例参见：[Demo工程](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo?spm=a2c4g.11186623.2.27.789073c8I6rfk5)
