Android SDK接入（本地集成） 
========================================

本文介绍如何通过本地集成方式添加依赖接入性能分析服务的Android SDK。
**说明**

* 性能分析服务的Android SDK接入可采用Maven集成和本地集成2种方式添加依赖。推荐使用Maven集成方式添加依赖，可大幅简化接入操作。

  

* 如需使用Maven集成方式添加依赖，操作方法参见：[Android SDK接入（Maven集成）]()

  




**前提条件** 
-----------------------------

已下载Android配置文件，并在文件中获取AppKey、AppSecret和PackageName。具体操作，请参见[快速入门：创建监控任务](/intl.zh-CN/App监控/快速入门：创建监控任务.md)。

**使用限制** 
-----------------------------

* 仅支持Android 4.2及以上版本。

  

* 仅支持arm64-v8a、armeabi、armeabi-v7a和x86架构。

  

* 仅支持gradle 3.0.0及以上版本。

  

* 仅支持以下网络库版本：

  * okhttp2：2.0.0-2.7.5

    
  
  * okhttp3: 3.0.0-3.14.7

    
  
  * okhttp4: 4.0.0-4.8.1

    
  

  




**接入概述** 
-----------------------------

1. [准备](#section-yf7-0kk-klr)：获取公钥；下载SDK包。

   

2. [应用插件](#section-8k1-0s2-y4y)：添加插件依赖；应用插件。

   

3. [添加依赖](#section-rjc-6c4-fgb)：采用本地方式集成SDK。SDK功能变更历史参见：[SDK版本变更](#section-vxx-a3n-ffx)

   

4. [接入服务](#section-bfc-lb6-yqo)：添加自定义Application，以及SDK初始化代码。

   

5. [混淆配置](#section-i7h-4cw-mwt)：如App对代码进行乱序混淆，则修改混淆配置文件。

   

6. [编译](#section-5x5-0m3-h8l)：常见编译问题排查。

   




**准备** 
---------------------------

**获取性能分析公钥** 

打开Android配置文件，查询`appmonitor.rsaSecret`字段内容，即为性能分析公钥。
**说明**

Android配置文件的获取方式参见：[前提条件](#section-rby-od8-oxf)

![1605495739150-3cef02d5-dc19-466d-b89b-3c7bd4ed865f](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6493065061/p183076.png)

**下载SDK包** 

1. 登录移动研发平台的[管理控制台](https://emas.console.aliyun.com/#/productList)，默认打开 **我的工作空间** 页面。

   

2. 在 **我的工作空间** 页面，单击工作空间标签的 **进入** 按钮，打开指定工作空间的概览页面。

   

3. 在工作空间概览页面，单击 **SDK下载** 区域，打开 **SDK下载** 右侧栏。![1 (2)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4367785161/p247489.png)

   

4. 在 **SDK下载** 右侧栏，选中 **性能分析** 复选框，单击 **下载Android版本** 按钮，下载性能分析服务的SDK包。

   **说明**

   在 **性能分析** 行的 **Android版** 列，单击版本号链接，可查看版本变更记录。

   ![SDK下载右侧栏1548](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5400442161/p238811.png)
   

5. 检查SDK包，确保内容完整。SDK包文件列表如下：

   




* alicloud-android-apm-1.0.8.2-open.aar

  

* alicloud-android-ha-adapter-1.1.3.8-open.aar

  

* alicloud-android-ha-apm-impl-1.0.7.1-open.aar

  

* alicloud-android-ha-core-1.1.0.6.1-open.aar

  

* alicloud-android-ha-fulltrace-1.0.1.12.aar

  

* alicloud-android-ha-protocol-1.1.1.0-open.aar

  

* alicloud-android-ha-tbrest-1.1.1.0-open.aar

  

* alicloud-android-networkmonitor-1.4.0.aar

  

* alicloud-android-rest-1.4.0-open.aar

  

* alicloud-android-utdid-2.5.1-proguard.jar

  

* fastjson-1.1.54.android.jar

  




应用插件 
-------------------------

1. 在项目级`build.gradle`项目文件的`buildscript{}`代码段添加插件依赖。

   **说明**

   此处仅添加插件依赖，应用依赖须添加至`build.gradle`项目文件的`dependencies{}`代码段。具体说明参见：[添加依赖](#section-rjc-6c4-fgb)

       buildscript {
           repositories {
               google()
               jcenter()
           }
       dependencies {
           classpath 'com.android.tools.build:gradle:${gradle-version}'
           classpath 'com.aliyun.ams:alicloud-android-networkmonitor-plugin:1.2.0-open'}
       }

   

   配置说明如下：
   

   |      配置项       |                                             说明                                              |
   |----------------|---------------------------------------------------------------------------------------------|
   | gradle-version | 用于指定实际开发环境的gradle版本。 【示例】`classpath 'com.android.tools.build:gradle:4.8.1'` |

   

2. 在应用级`build.gradle`项目文件中添加代码段应用插件。

       apply plugin: 'com.aliyun.emas.networkmonitor'

   




**添加依赖** 
-----------------------------

1. 将SDK包内所有文件拷贝至项目的libs目录下。

   

2. 在项目级`build.gradle`项目文件中，添加本地SDK文件目录地址。

       repositories {
          flatDir {
              dirs 'libs'
          }
       }

   

3. 在应用级`build.gradle`项目文件的`dependencies{}`代码段，添加SDK依赖。

           //1、本地jar库引入。
           compile fileTree(include: ['*.jar'], dir: 'libs')
           //2、公共库。
           compile (name: 'alicloud-android-ha-adapter-1.1.3.8-open', ext: 'aar')
           compile (name: 'alicloud-android-ha-core-1.1.0.6.1-open', ext: 'aar')
           compile (name: 'alicloud-android-ha-protocol-1.1.1.0-open', ext: 'aar')
           compile (name: 'alicloud-android-ha-tbrest-1.1.1.0-open', ext: 'aar')
           compile (name: 'alicloud-android-utdid-2.5.1-proguard', ext: 'jar')
           compile (name: 'fastjson-1.1.54.android', ext: 'jar')
           //3、性能监控，不接入可注释掉。
           compile (name: 'alicloud-android-ha-apm-1.0.8.2-open', ext: 'aar')
           compile (name: 'alicloud-android-ha-apm-impl-1.0.7.1-open', ext: 'aar')
           compile (name: 'alicloud-android-ha-fulltrace-1.0.1.12', ext: 'aar')
           compile (name: 'alicloud-android-networkmonitor-1.4.0', ext: 'aar)
           compile (name: 'alicloud-android-rest-1.4.0-open', ext: 'aar)

   




**接入服务** 
-----------------------------

1. 定义`Application`类，编写`onCreate`方法，启动服务。

       public class MyApplication extends Application {
               @Override
               public void onCreate() {
                   initHa();
               }
               private void initHa() {
                    AliHaConfig config = new AliHaConfig();
                    config.appKey = "xxxxxxxx";
                    config.appVersion = "x.xx"; 
                    config.appSecret = "xxxxxxxxxxxx";
                    config.channel = "mqc_test"; 
                    config.userNick = null; 
                    config.application = this; 
                    config.context = getApplicationContext(); 
                    config.isAliyunos = false;
                    config.rsaPublicKey = "xxxxxxx";
                    AliHaAdapter.getInstance().addPlugin(Plugin.apm);
                    AliHaAdapter.getInstance().start(config);
               }
           }

   

   配置说明如下：

   
   

   |      参数      |                                                                                                                                                            说明                                                                                                                                                             |
   |--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | appKey       | 用于指定App的AppKey。 【数据类型】字符串 【获取方式】参见：[前提条件](#section-rby-od8-oxf) 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                   |
   | appVersion   | 用于设置App的版本号。 【数据类型】字符串 【格式要求】自定义 【取值范围】任意长度 **说明** 该参数值将在控制台显示为下拉列表选项，建议短小凝练。 【是否必选】是 【是否可为空】否 【默认值】无 【大小写敏感】是。例如，vx.x和Vx.x不是一个版本。 【字符类型】英文大小写、数字 **说明** 该参数不支持中文字符、特殊字符。 |
   | appSecret    | 用于指定App的AppSecret。 【数据类型】字符串 【获取方式】参见：[前提条件](#section-rby-od8-oxf) 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                |
   | channel      | 用于设置渠道标识，上报至服务端，进行渠道区分。 【数据类型】字符串 【取值范围】任意长度 【是否必选】否 【是否可为空】是 【默认值】无 【字符类型】英文大小写、数字 **说明** 该参数不支持中文字符、特殊字符。                                                                                               |
   | userNick     | 用于设置用户昵称，上报至服务端，进行用户区分。后续可能依据该参数，进行数据检索。 【数据类型】字符串 【取值范围】任意长度 【是否必选】否 【是否可为空】是 【默认值】无 【字符类型】英文大小写、数字。 **说明** 该参数不支持中文字符、特殊字符。 【命名规范】自定义                                                                   |
   | application  | 用于指定本应用。 **注意** 该参数不能指向其他应用。 【数据类型】对象 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                                                                             |
   | context      | 用于指定App的上下文对象，设置`getApplicationContext();`即可。【数据类型】对象 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                                                                             |
   | isAliyunos   | 用于判断App所在平台是否为YunOS。 【数据类型】布尔型 【取值范围】false或true 【是否必选】否 【是否可为空】是 【默认值】false                                                                                                                                                               |
   | rsaPublicKey | 用于指定性能分析公钥。 【数据类型】字符串 【获取方式】参见：[准备](#section-yf7-0kk-klr) 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                         |

   

2. 在`AndroidManifest.xml`中添加代码段注册Application。

       <application
               android:name=".MyApplication"
               android:icon="@mipmap/ic_launcher"
               android:label="@string/app_name"
               android:supportsRtl="true"
               android:theme="@style/AppTheme" >
       </application>

   




**混淆配置** 
-----------------------------

如App对代码进行乱序混淆，则在混淆配置文件中添加代码段：

    -keep class com.taobao.monitor.APMLauncher{*;}
    -keep class com.taobao.monitor.impl.logger.Logger{*;}
    -keep class com.taobao.monitor.impl.logger.IDataLogger{*;}
    -keep class com.taobao.monitor.impl.data.AbsWebView{*;}
    -keep class com.taobao.monitor.impl.data.GlobalStats{*;}
    -keep class com.taobao.monitor.impl.common.Global{*;}
    -keep class com.taobao.monitor.impl.data.WebViewProxy{*;}
    -keep class com.taobao.monitor.impl.logger.Logger{*;}
    -keep class com.taobao.monitor.impl.processor.pageload.IProcedureManager{*;}
    -keep class com.taobao.monitor.impl.processor.pageload.ProcedureManagerSetter{*;}
    -keep class com.taobao.monitor.impl.util.TimeUtils{*;}
    -keep class com.taobao.monitor.impl.util.TopicUtils{*;}
    -keep class com.taobao.monitor.impl.common.DynamicConstants{*;}
    -keep class com.taobao.application.common.data.DeviceHelper{*;}
    -keep class com.taobao.application.common.impl.AppPreferencesImpl{*;}
    -keep class com.taobao.monitor.impl.processor.launcher.PageList{*;}
    -keep class com.taobao.monitor.impl.processor.fragmentload.FragmentInterceptorProxy{*;}
    -keep class com.taobao.monitor.impl.processor.fragmentload.IFragmentInterceptor{*;}
    -keep class com.taobao.monitor.impl.logger.DataLoggerUtils{*;}
    -keep interface com.taobao.monitor.impl.data.IWebView{*;}
    -keep interface com.taobao.monitor.impl.processor.IProcessor{*;}
    -keep interface com.taobao.monitor.impl.processor.IProcessorFactory{*;}
    -keep interface com.taobao.monitor.impl.logger.IDataLogger{*;}
    -keep interface com.taobao.monitor.impl.trace.IDispatcher{*;}
    -keepattributes Exceptions,InnerClasses,Signature,Deprecated,SourceFile,LineNumberTable,*Annotation*,EnclosingMethod



**编译** 
---------------------------

如同时使用其他阿里云产品，可能会因为依赖中存在UTDID冲突，造成编译失败。解决办法参见：[SDK UTDID冲突解决方案]()

**样例代码** 
-----------------------------

性能分析服务Android SDK接入工程样例参见：[Demo工程](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo "Demo工程")

**功能验证** 
-----------------------------

Android SDK接入操作完成后，可操作App，查看性能分析服务控制台显示数据，进行功能验证。

1. 手机端：启动App。（2分钟后）控制台：查看 **概览** 页签的 **启动速度** 是否显示数据。

   

2. 手机端：在App中跳转几个页面。（2分钟后）控制台：查看 **概览** 页签的 **加载时间** 是否显示数据。

   



**说明**

数据从App采集到控制台显示，存在大约2分钟延迟。

如数据显示正常，则Android SDK接入成功；

否则，可能的原因是：SDK接入失败、SDK未获取数据、数据发送失败、后端问题，请联系[技术支持](/intl.zh-CN/.md)解决。



SDK版本说明 
----------------------------



|     版本号      |    发布日期    |    变更说明     |
|--------------|------------|-------------|
| 1.0.8.2-open | 2020-12-18 | 代码优化。       |
| 1.0.8.1-open | 2020-11-24 | 优化编译构建问题。   |
| 1.0.8.0-open | 2020-11-12 | 新增网络异常分析功能。 |
| 其他历史版本。                               |||


