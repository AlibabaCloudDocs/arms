Android SDK接入（Maven集成） 
===========================================

本文介绍如何通过Maven集成方式添加依赖接入性能分析服务的Android SDK。
**说明**

* 性能分析服务的Android SDK接入可采用Maven集成和本地集成2种方式添加依赖。推荐使用Maven集成方式添加依赖，可大幅简化接入操作。

  

* 如需使用本地集成方式添加依赖，操作方法参见：[Android SDK接入（本地集成）](/cn.zh-CN/App监控/接入指南/性能分析/Android SDK接入（本地集成）.md)

  




**前提条件** 
-----------------------------

已下载Android配置文件，并在文件中获取了AppKey、AppSecret和PackageName。具体操作，请参见[快速入门：创建监控任务](/cn.zh-CN/App监控/快速入门：创建监控任务.md)

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

1. [准备](#section-j4u-h11-dd8)：获取公钥。

   

2. [应用插件](#section-34w-k26-jh2)：添加插件依赖；应用插件。

   

3. [添加依赖](#section-uqp-h2c-8jv)：采用Maven方式集成SDK。SDK功能变更历史参见：[SDK版本说明](#section-tzi-1dr-dw4)

   

4. [接入服务](#section-uwn-a37-4ul)：添加自定义Application，以及SDK初始化代码。

   

5. [混淆配置]()：如App对代码进行乱序混淆，则修改混淆配置文件。

   

6. [编译](#section-olk-7bm-q7z)：常见编译问题排查。

   




**准备** 
---------------------------

打开Android配置文件，查询`appmonitor.rsaSecret`字段内容，即为性能分析公钥。
**说明**

Android配置文件的获取方式参见：[前提条件](#section-3jg-dl7-zny)

![1605495739150-3cef02d5-dc19-466d-b89b-3c7bd4ed865f](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0320765061/p183052.png)

应用插件 
-------------------------

1. 在项目级`build.gradle`项目文件的`buildscript{}`代码段添加插件依赖。

   
   **注意**

   此处仅添加插件依赖，应用依赖须添加至`build.gradle`项目文件的`dependencies{}`代码段。具体说明参见：[添加依赖](#section-uqp-h2c-8jv)

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

1. 在项目级`build.gradle`项目文件的`repositories{}`代码段中添加阿里云Maven仓库地址。

       repositories {
           maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
       }

   

2. 在应用级`build.gradle`项目文件的`android{}`代码段中设置应用包名和.so库。

       android {
           ......
           defaultConfig {
               applicationId "com.xxx.xxx" 
               ......
               ndk {
                   //选择要添加的对应cpu类型的.so库，当前支持四种。
                   abiFilters 'arm64-v8a', 'armeabi', 'armeabi-v7a', 'x86' 
               }
               ......
           }
           ......
       }

   

   配置说明如下：
   

   |      参数       |                                                                                                                                                                                          说明                                                                                                                                                                                          |
   |---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | applicationId | 用于指定App的PackageName。 【数据类型】字符串 【获取方式】参见：[前提条件](#section-3jg-dl7-zny) 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                                                                         |
   | ndk           | 用于指定App的架构，添加对应CPU类型的.so库。 【数据类型】枚举型 【取值范围】 * arm64-v8a   * armeabi   * armeabi-v7a   * x86    【是否必选】是 【是否可为空】否 【默认值】无 【大小写敏感】否 |

   

3. 在应用级`build.gradle`项目文件的`dependencies{}`代码段中添加SDK依赖。

       dependencies {
           ......
           implementation fileTree(dir: 'libs', include: ['*.jar'])
           implementation "com.squareup.okhttp3:okhttp:${okhttp3version}"
       
           //线上测试。
           implementation 'com.aliyun.ams:alicloud-android-ha-adapter:1.1.3.8-open'
           implementation 'com.aliyun.ams:alicloud-android-apm:1.0.8.2-open'
           ......
       }

   

   配置说明如下：
   

   |       参数       |                                              说明                                               |
   |----------------|-----------------------------------------------------------------------------------------------|
   | okhttp3version | 用于设置本地开发环境可支持的网络库版本。 【示例】`implementation "com.squareup.okhttp3:okhttp:4.8.1"` |

   




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
   

   |       参数       |                                              说明                                               |
   |----------------|-----------------------------------------------------------------------------------------------|
   | okhttp3version | 用于设置本地开发环境可支持的网络库版本。 【示例】`implementation "com.squareup.okhttp3:okhttp:4.8.1"` |

   

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

如数据显示正常，则Android SDK接入成功。

否则，可能的原因是：SDK接入失败、SDK未获取数据、数据发送失败、后端问题，请联系[技术支持](/cn.zh-CN/.md)解决。

SDK版本说明 
----------------------------



|     版本号      |    发布日期    |    变更说明     |
|--------------|------------|-------------|
| 1.0.8.2-open | 2020-12-18 | 代码优化。       |
| 1.0.8.1-open | 2020-11-24 | 优化编译构建问题。   |
| 1.0.8.0-open | 2020-11-12 | 新增网络异常分析功能。 |
| 其他历史版本。                               |||



