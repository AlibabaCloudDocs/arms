Android SDK接入（本地集成） 
========================================

本文介绍如何通过本地集成方式添加依赖接入远程日志服务。
**说明**



* 接入远程日志服务的Android SDK可采用Maven集成和本地集成2种方式添加依赖。推荐使用Maven集成方式添加依赖，可大幅简化接入操作。

  

* 如需使用Maven集成方式添加依赖，操作方法参见：[Android SDK接入（Maven集成）](/cn.zh-CN/App监控/接入指南/远程日志/Android SDK接入（Maven集成）.md)

  




前提条件 
-------------------------

已下载Android配置文件，并在文件中获取AppKey、AppSecret和PackageName。具体操作，请参见[快速入门：创建监控任务](/cn.zh-CN/App监控/快速入门：创建监控任务.md)。

使用限制 
-------------------------

* 仅支持Android 4.2及以上版本。

  

* 仅支持armeabi、armeabi-v7a和x86架构。

  

* 日志在手机端最多存储7天。

  




接入概述 
-------------------------

1. [准备](#section-c4a-nbj-82v)：获取公钥；下载SDK包。

   

2. [添加依赖](#section-igf-jrx-56h)：采用本地集成方式。

   

3. [接入服务](#section-8bb-0y9-qyw)：添加自定义Application，以及初始化代码；配置ABI；设置日志拉入级别。

   

4. [打印日志](#section-xjm-8ii-926)：引入头文件；在代码中打印日志信息。

   

5. [混淆配置](#section-jke-u6j-4cg)：如App对代码进行乱序混淆，则修改混淆配置文件。

   

6. [编译](#section-e0r-rf4-0tp)。

   




准备 
-----------------------

**获取性能分析公钥** 

打开配置文件，查询`appmonitor.tlog.rsaSecret`字段内容，即为远程日志公钥。

![公钥](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8374572161/p181562.png)

**下载SDK包** 

1. 登录移动研发平台的[管理控制台](https://emas.console.aliyun.com/#/productList)，默认打开 **我的工作空间** 页面。

   

2. 在 **我的工作空间** 页面，单击工作空间标签的 **进入** 按钮，打开指定工作空间的概览页面。

   

3. 在工作空间概览页面，单击 **SDK下载** 区域，打开 **SDK下载** 右侧栏。![1 (2)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4367785161/p247489.png)

   

4. 在 **SDK下载** 右侧栏，选中 **远程日志** 复选框，单击 **下载Android版本** 按钮，下载远程日志服务的SDK包。

   
   **说明**

   在 **远程日志** 行的 **Android版** 列，单击版本号链接，可查看版本变更记录。

   ![SDK下载右侧栏1558](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9406268061/p204370.png)
   

5. 检查SDK包，确保内容完整。

   




SDK包文件列表如下：

* alicloud-android-ha-adapter-1.1.3.8-open.aar

  

* alicloud-android-ha-core-1.1.0.6.1-open.aar

  

* alicloud-android-ha-protocol-1.1.1.0-open.aar

  

* alicloud-android-ha-tbrest-1.1.1.0-open.aar

  

* alicloud-android-ha-telescopebase-1.1.1-open.aar

  

* alicloud-android-ha-telescopesdk-1.1.3-open.aar

  

* alicloud-android-ha-tlog-message-rpc-1.1.3.1-open.aar

  

* alicloud-android-ha-tlog-native-1.1.0.7-open.aar

  

* alicloud-android-ha-tlog-protocol-1.1.0.8-open.aar

  

* alicloud-android-ha-tlog-uploader-oss-1.1.0.6.3-open.aar

  

* alicloud-android-tlog-1.1.3.1-open.aar

  

* alicloud-android-utdid-2.5.1-proguard.jar

  

* fastjson-1.1.54.android.jar

  

* okhttp-3.4.1.jar

  

* okio-1.9.0.jar

  

* oss-android-sdk-2.9.3.aar

  



**说明**

如存在名称相同，版本号不同的包文件，添加最高版本的包文件即可。



添加依赖 
-------------------------

1. 将SDK包内所有文件拷贝至项目的libs目录下。

   

2. 在项目级`build.gradle`项目文件中，添加本地SDK文件目录地址。

       repositories {
           flatDir {
               dirs 'libs'
           }
       }

   

3. 在应用级`build.gradle`项目文件的`dependencies{}`代码段，添加SDK依赖。

       //1、本地jar库引入。
       compile fileTree(include:['*.jar'],dir:'libs')
       
       //2、公共库。
       compile(name:'alicloud-android-ha-adapter-1.1.3.8-open',ext:'aar')
       compile(name:'alicloud-android-ha-core-1.1.0.6.1-open',ext:'aar')
       compile(name:'alicloud-android-ha-protocol-1.1.1.0-open',ext:'aar')
       compile(name:'alicloud-android-ha-tbrest-1.1.1.0-open',ext:'aar')
       compile(name:'alicloud-android-utdid-2.5.1-proguard',ext:'jar')
       compile(name:'fastjson-1.1.54.android',ext:'jar')
       
       
       //3、移动日志，不接入可注释掉。
       compile(name:'alicloud-android-tlog-1.1.3.1-open',ext:'aar')
       compile(name:'alicloud-android-ha-tlog-message-rpc-1.1.3.1-open',ext:'aar')
       compile(name:'alicloud-android-ha-telescopebase-1.1.1-open',ext:'aar')
       compile(name:'alicloud-android-ha-tlog-uploader-oss-1.1.0.6.3-open',ext:'aar')
       compile(name:'alicloud-android-ha-tlog-protocol-1.1.0.8-open',ext:'aar')
       compile(name:'alicloud-android-ha-telescopesdk-1.1.3-open',ext:'aar')
       compile(name:'alicloud-android-ha-tlog-native-1.1.0.7-open',ext:'aar')
       compile(name:'okhttp-3.4.1',ext:'jar')
       compile(name:'okio-1.9.0',ext:'jar')
       compile(name:'oss-android-sdk-2.9.3',ext:'aar')

   




接入服务 
-------------------------

1. 定义`Application`类，并编写`onCreate`方法启动服务：

       public class MyApplication extends Application {
           @Override
           public void onCreate() {
               initHa();
           }
           private void initHa() {
                AliHaConfig config = new AliHaConfig();
                config.appKey = "xxxxxxxx"; //配置项：appkey。
                config.appVersion = "x.xx"; //配置项：应用的版本号。
                config.appSecret = "xxxxxxxxxxxx"; //配置项：appsecret。
                config.channel = "mqc_test"; //配置项：应用的渠道号标记，自定义。
                config.userNick = null; //配置项：用户的昵称。
                config.application = this; //配置项：应用指针。
                config.context = getApplicationContext(); //配置项：应用上下文。
                config.isAliyunos = false; //配置项：是否为yunos。
                config.rsaPublicKey = "xxxxxxx"; //配置项：tlog公钥。
                AliHaAdapter.getInstance().addPlugin(Plugin.tlog);
                AliHaAdapter.getInstance().openDebug(true);
                AliHaAdapter.getInstance().start(config);
                TLogService.updateLogLevel(TLogLevel.XXXXXX); //配置项：控制台可拉取的日志级别。
           }
       }

   

   配置说明如下：
   

   |         参数          |                                                                                                                                                                                                                                                                                                                                                      说明                                                                                                                                                                                                                                                                                                                                                      |
   |---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | config.appKey       | 用于指定App的AppKey。 【数据类型】字符串 【如何获取】参见：[前提条件](#section-cj0-5wv-7ku) 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   | config.appVersion   | 用于设置App的版本号。 【数据类型】字符串 【格式要求】自定义 【取值范围】任意长度 **说明** 该参数值将在控制台显示为下拉列表选项，建议短小凝练。 【是否必选】是 【是否可为空】否 【默认值】无 【大小写敏感】是。例如，vx.x和Vx.x不是一个版本。 【字符类型】英文大小写、数字。 **说明** 该参数不支持中文字符、特殊字符。                                                                                                                                                                                                                                                                                                                                                                                   |
   | config.appSecret    | 用于指定App的AppSecret。 【数据类型】字符串 【如何获取】参见：[前提条件](#section-cj0-5wv-7ku) 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   | config.channel      | 用于设置渠道标识，上报至服务端，进行渠道区分。 【数据类型】字符串 【取值范围】任意长度 【是否必选】否 【是否可为空】是 【默认值】无 【字符类型】英文大小写、数字。 **说明** 该参数不支持中文字符、特殊字符。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   | config.userNick     | 用于设置用户昵称，上报至服务端，进行用户区分。后续可能依据该参数，进行数据检索。 【数据类型】字符串 【取值范围】任意长度 【是否必选】否 【是否可为空】是 【默认值】无 【字符类型】英文大小写、数字。 **说明** 该参数不支持中文字符、特殊字符。 【命名规范】自定义                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   | config.application  | 用于指定本应用。 **注意** 不能指向其他应用。 【数据类型】对象 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   | config.context      | 用于指定App的上下文对象，设置`getApplicationContext();`即可。 【数据类型】对象 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   | config.isAliyunos   | 用于判断App所在平台是否为YunOS。 【数据类型】布尔型 【取值范围】false或true 【是否必选】否 【是否可为空】是 【默认值】false                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   | config.rsaPublicKey | 用于指定远程日志公钥。 【数据类型】字符串 【如何获取】参见：[准备](#section-c4a-nbj-82v) 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   | TLogLevel.XXXXXX    | 用于全局设置控制台可拉取的日志的级别。 【数据类型】枚举型 【取值范围】 * VERBOSE：可拉取所有级别的日志。   * DEBUG：可拉取DEBUG、INFO、WARN和ERROR级别的日志。   * INFO：可拉取INFO、WARN和ERROR级别的日志。   * WARN：可拉取WARN和ERROR级别的日志。   * ERROR：可拉取ERROR级别的日志。    【是否必选】是 【默认取值】ERROR 【配置说明】 * `TLogService.updateLogLevel()`函数可选调用，如未调用，则全局默认可拉取的日志级别为ERROR。   * 日志级别说明参见：[术语解释]()    |

   

2. 在`AndroidManifest.xml`中添加代码段注册`Application`。

       <application
           android:name=".MyApplication"
           android:icon="@mipmap/ic_launcher"
           android:label="@string/app_name"
           android:supportsRtl="true"
           android:theme="@style/AppTheme" >
           ...
       </application>

   




打印日志 
-------------------------

1. 如业务流程触发日志输出，需引入头文件：

       import com.alibaba.ha.adapter.service.tlog.TLogService;

   

2. 在适当位置添加代码，输出日志信息。示例代码：

       TLogService.logv("MODEL","TAG","MESSAGE");
       TLogService.logd("MODEL","TAG","MESSAGE");
       TLogService.logi("MODEL","TAG","MESSAGE");
       TLogService.logw("MODEL","TAG","MESSAGE");
       TLogService.loge("MODEL","TAG","MESSAGE");

   




**函数** ：`TLogService.<LogLevel>(<MODEL>,<TAG,<MESSAGE>);`

**说明** ：用于输出指定级别的日志信息。


|    参数    |                                                                                                                                                                                                                                                                                                  说明                                                                                                                                                                                                                                                                                                  |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| LogLevel | 指定拉取的日志级别。日志级别说明参见：[术语解释]() 【数据类型】枚举型 【取值范围】 * logv：输出VERBOSE（调试详情）级别的日志。   * logd：输出DEBUG（调试信息）级别的日志。   * logi：输出INFO（一般信息）级别的日志。   * logw：输出WARN（警告信息）级别的日志。   * loge：输出ERROR（错误信息）级别的日志。    【配置说明】输出的日志是否可以被控制台拉取，取决`于TLogService.updateLogLevel()`函数的参数设置。例如，当`TLogService.updateLogLevel(TLogLevel.WARN)`时，则控制台拉取不到通过logv、logd和logi输出的日志。 |
| MODEL    | 用于设置输出日志内容的功能模块，便于后续根据来源筛选日志。 【数据类型】字符串 【字符类型】英文大小写、中文、数字、特殊字符 【是否必选】是 【是否大小写敏感】否 【示例】"推送功能模块Push"                                                                                                                                                                                                                                                                                                                                                                                                                   |
| TAG      | 用于设置日志的关键字，便于后续根据标签筛选日志。 【数据类型】字符串 【字符类型】英文大小写、中文、数字、特殊字符 【是否必选】是 【是否大小写敏感】否 【示例】"推送功能模块收到了推送Push.receive，推送功能模块点击了推送Push.click"                                                                                                                                                                                                                                                                                                                                                                                     |
| MESSAGE  | 用于输出日志信息。 【数据类型】字符串 【字符类型】英文大小写、中文、数字、特殊字符 【是否必选】是                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |



混淆配置 
-------------------------

如App对代码进行乱序混淆，则在混淆配置文件中添加代码段：

    #keep class
    -keep interface com.taobao.tao.log.ITLogController{*;}
    -keep class com.taobao.tao.log.upload.*{*;}
    -keep class com.taobao.tao.log.message.*{*;}
    -keep class com.taobao.tao.log.LogLevel{*;}
    -keep class com.taobao.tao.log.TLog{*;}
    -keep class com.taobao.tao.log.TLogConstant{*;}
    -keep class com.taobao.tao.log.TLogController{*;}
    -keep class com.taobao.tao.log.TLogInitializer{public *;}
    -keep class com.taobao.tao.log.TLogUtils{public *;}
    -keep class com.taobao.tao.log.TLogNative{*;}
    -keep class com.taobao.tao.log.TLogNative$*{*;}
    -keep class com.taobao.tao.log.CommandDataCenter{*;}
    -keep class com.taobao.tao.log.task.PullTask{*;}
    -keep class com.taobao.tao.log.task.UploadFileTask{*;}
    -keep class com.taobao.tao.log.upload.LogFileUploadManager{public *;}
    -keep class com.taobao.tao.log.monitor.**{*;}
    #兼容godeye
    -keep class com.taobao.tao.log.godeye.core.module.*{*;}
    -keep class com.taobao.tao.log.godeye.GodeyeInitializer{*;}
    -keep class com.taobao.tao.log.godeye.GodeyeConfig{*;}
    -keep class com.taobao.tao.log.godeye.core.control.Godeye{*;}
    -keep interface com.taobao.tao.log.godeye.core.GodEyeAppListener{*;}
    -keep interface com.taobao.tao.log.godeye.core.GodEyeReponse{*;}
    -keep interface com.taobao.tao.log.godeye.api.file.FileUploadListener{*;}
    -keep public class * extends com.taobao.android.tlog.protocol.model.request.base.FileInfo{*;}
    -keepattributes Exceptions,InnerClasses,Signature,Deprecated,SourceFile,LineNumberTable,*Annotation*,EnclosingMethod



编译 
-----------------------

如同时使用其他阿里云产品，可能会因为依赖中存在UTDID冲突，造成编译失败。解决办法参见：[SDK UTDID冲突解决方案](https://help.aliyun.com/document_detail/172646.html)

样例代码 
-------------------------

远程日志服务Android SDK接入工程样例参见：[Demo工程](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo "Demo工程")
