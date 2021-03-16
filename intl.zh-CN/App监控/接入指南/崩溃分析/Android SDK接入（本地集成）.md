Android SDK接入（本地集成） 
========================================

本文介绍如何通过本地集成方式添加依赖接入崩溃分析服务的Android SDK。
**说明**



* 崩溃分析服务的Android SDK接入可采用Maven集成和本地集成2种方式添加依赖。推荐使用Maven集成方式添加依赖，可大幅简化接入操作。

  

* 如需使用Maven集成方式添加依赖，操作方法参见[Android SDK接入（Maven集成）](/intl.zh-CN/App监控/接入指南/崩溃分析/Android SDK接入（Maven集成）.md)。

  

* 崩溃分析服务新增网络性能监控功能已进行灰度发布，如需体验，可联系[技术支持](/intl.zh-CN/.md)获取SDK包。

  




前提条件 
-------------------------

* 已获取AppKey、AppSecret，请参见[快速入门：创建监控任务](/intl.zh-CN/App监控/快速入门：创建监控任务.md)中下载的配置文件。

  

* 已下载崩溃分析SDK，具体操作，请参见[下载SDK](https://help.aliyun.com/document_detail/169962.html#title-fvd-ozh-524)。

  




使用限制 
-------------------------

* 仅支持Android 4.0及以上版本。

  

* 仅支持arm64-v8a、armeabi、armeabi-v7a和x86架构。

  




操作步骤 
-------------------------

1. **添加依** **赖。** 

   1. 将SDK包内所有文件拷贝至项目libs目录下。

      
   
   2. 在项目级`build.gradle`项目文件中，添加本地SDK文件目录地址。

          repositories {
             flatDir {
                 dirs 'libs'
             }
          }

      
   
   3. 在应用级`build.gradle`项目文件的`dependencies{}`代码段添加SDK依赖。

              //1、本地jar库引入。
              compile fileTree(include: ['*.jar'], dir: 'libs')
              //2、公共库。
              compile (name: 'alicloud-android-ha-adapter-1.1.3.7-open', ext: 'aar')
              compile (name: 'alicloud-android-ha-core-1.1.0.6.1-open', ext: 'aar')
              compile (name: 'alicloud-android-ha-protocol-1.1.1.0-open', ext: 'aar')
              compile (name: 'alicloud-android-ha-tbrest-1.1.1.0-open', ext: 'aar')
              compile (name: 'alicloud-android-utdid-2.5.1-proguard', ext: 'jar')
              compile (name: 'fastjson-1.1.54.android', ext: 'jar')
              //3、崩溃分析。
              compile (name: 'alicloud-android-ha-crashreporter-1.2.4', ext: 'aar')
              compile (name: 'alicloud-android-ha-watch-1.1.0.6.1-open', ext: 'aar')
              compile (name: 'alicloud-android-ha-bizerrorreporter-1.1.0.9-open', ext: 'aar')
              compile (name: 'alicloud-android-ha-olympic-1.0.4.37', ext: 'aar')

      
   

   

2. **接入服务。** 

   1. 定义Application类，编写onCreate方法，启动服务。

      **说明**

      建议将崩溃分析服务的SDK初始化代码段，放在所有业务代码之前，确保App在启动时，优先加载崩溃分析服务，保障后续崩溃的信息，可以即时获取并上传至控制台。

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
                  //启动CrashReporter。
                  AliHaAdapter.getInstance().addPlugin(Plugin.crashreporter);
                  AliHaAdapter.getInstance().start(config);
             }
          }

      

      配置说明如下：
      

      |     参数      |                                                                                                                                                            说明                                                                                                                                                            |
      |-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
      | appKey      | 用于指定App的AppKey。 【数据类型】字符串 【如何获取】参见：[前提条件](#section-1je-j5a-e53) 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                  |
      | appVersion  | 用于设置App的版本号。 【数据类型】字符串 【格式要求】自定义 【取值范围】任意长度。 **说明** 该参数值将在控制台显示为下拉列表选项，建议短小凝练。 【是否必选】是 【是否可为空】否 【默认值】无 【大小写敏感】是。例如，vx.x和Vx.x不是一个版本。 【字符类型】英文大小写、数字。 **说明** 不支持中文字符、特殊字符。 |
      | appSecret   | 用于指定App的AppSecret。 【数据类型】字符串 【如何获取】参见：[前提条件](#section-1je-j5a-e53) 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                               |
      | channel     | 用于设置渠道标识，上报至服务端，进行渠道区分。 【数据类型】字符串 【取值范围】任意长度 【是否必选】否 【是否可为空】是 【默认值】无 【字符类型】英文大小写、数字。 **说明** 不支持中文字符、特殊字符。                                                                                                |
      | userNick    | 用于设置用户昵称，上报至服务端，进行用户区分。后续可能依据该参数，进行数据检索。 【数据类型】字符串 【取值范围】任意长度 【是否必选】否 【是否可为空】是 【默认值】无 【字符类型】英文大小写、数字。 **说明** 不支持中文字符、特殊字符。 【命名规范】自定义                                                                     |
      | application | 用于指定本应用。注意：不能指向其他应用。 【数据类型】对象 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                                                                                    |
      | context     | 用于指定App的上下文对象，设置getApplicationContext();即可。 【数据类型】对象 【是否必选】是 【是否可为空】否 【默认值】无                                                                                                                                                                             |
      | isAliyunos  | 用于判断App所在平台是否为YunOS。 【数据类型】布尔型 【取值范围】false或true 【是否必选】否 【是否可为空】是 【默认值】false                                                                                                                                                              |

      
   
   2. 在Androidmanifest.xml中添加代码段注册Application。

          <application
                  android:name=".MyApplication"
                  android:icon="@mipmap/ic_launcher"
                  android:label="@string/app_name"
                  android:supportsRtl="true"
                  android:theme="@style/AppTheme" >
          </application>

      
   

   

3. **添加高级设置。** 

   Android SDK提供接口，用于上报自定义信息或错误。

       //上报自定义信息。
       AliHaAdapter.getInstance().addCustomInfo("key", "value");     //配置项：自定义环境信息。
       
       //按异常类型上报自定义信息。
       AliHaAdapter.getInstance().setErrorCallback(new ErrorCallback() {
           @Override
           public Map<String, String> onError(ErrorInfo callbackInfo) {
               Map<String, String> infos = new HashMap<>();
               infos.put("key", "value");     //配置项：异常信息。
               return infos;
           }
       });
       
       //上报自定义错误。
       AliHaAdapter.getInstance().reportCustomError(new RuntimeException("custom error"));     //配置项：自定义错误。

   

   具体说明参见：[Android SDK接口说明](/intl.zh-CN/App监控/接入指南/崩溃分析/Android SDK接口说明.md)
   

4. **混淆配置。** 

   如App对代码进行乱序混淆，则在混淆配置文件中添加代码段：

       #keep crashreporter
       -keep class com.alibaba.motu.crashreporter.MotuCrashReporter{ *;}
       -keep class com.alibaba.motu.crashreporter.ReporterConfigure{*;}
       -keep class com.alibaba.motu.crashreporter.utrestapi.UTRestReq{*;}
       -keep interface com.alibaba.motu.crashreporter.IUTCrashCaughtListener{*;}
       -keep interface com.alibaba.motu.crashreporter.ICrashReportSendListener{*;}
       -keep interface com.alibaba.motu.crashreporter.ICrashReportDataListener{*;}
       -keep interface com.ut.mini.crashhandler.*{*;}
       -keep class com.uc.crashsdk.**{*;}
       -keep class com.alibaba.motu.crashreporter.YouKuCrashReporter{public *;}
       -keepattributes Exceptions,InnerClasses,Signature,Deprecated,SourceFile,LineNumberTable,*Annotation*,EnclosingMethod

   

5. **编译。** 

   如同时使用其他阿里云产品，可能会因为依赖中存在UTDID冲突，造成编译失败，请参见[SDK UTDID冲突解决方案](https://help.aliyun.com/document_detail/172616.html)解决。
   

6. **接入验证。** 

   Android SDK接入操作完成后，需进行功能验证。
   1. 编写测试代码，模拟或触发移动端崩溃。例如：

          throw new NullPointerException();

      
   
   2. 重启移动端，大概2分钟后在控制台查看是否显示崩溃信息。

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
