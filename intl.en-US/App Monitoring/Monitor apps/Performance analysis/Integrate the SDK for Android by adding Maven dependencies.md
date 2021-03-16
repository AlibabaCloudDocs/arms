Integrate the SDK for Android by adding Maven dependencies 
===============================================================================

This topic describes how to integrate the performance analysis SDK for Android by adding Maven dependencies.
**Note**

* You can integrate the performance analysis SDK for Android by adding Maven dependencies or local dependencies. We recommend that you integrate the SDK by adding Maven dependencies, which greatly simplifies the integration.

  

* For more information about how to integrate the SDK by adding local dependencies, see [Integrate the SDK for Android by adding local dependencies](/intl.en-US/App Monitoring/Monitor apps/Performance analysis/Integrate the SDK for Android by adding local dependencies.md).

  




**Prerequisites** 
--------------------------------------

The configuration file of the app is downloaded, and the AppKey, AppSecret, and PackageName are obtained from the configuration file. For more information, see [Create an app monitoring task](/intl.en-US/App Monitoring/Create an app monitoring task.md).

**Limits** 
-------------------------------

* Only Android 4.2 and later are supported.

  

* Only the architectures of arm64-v8a, armeabi, armeabi-v7a, and x86 are supported.

  

* Only Gradle 3.0.0 and later are supported.

  

* Only the following network libraries are supported:

  * okhttp2: 2.0.0-2.7.5

    
  
  * okhttp3: 3.0.0-3.14.7

    
  
  * okhttp4: 4.0.0-4.8.1

    
  

  




**Integration process** 
--------------------------------------------

1. [Prepare for the integration](#section-j4u-h11-dd8): Obtain the public key.

   

2. [Apply a plug-in](#section-34w-k26-jh2): Add plug-in dependencies to apply a plug-in.

   

3. [Add dependencies](#section-uqp-h2c-8jv): Integrate the SDK by adding Maven dependencies. For more information about the changes of the SDK, see [Release notes of the SDK for Android](#section-tzi-1dr-dw4).

   

4. [Integrate the service](#section-uwn-a37-4ul): Define the custom Application class and add the code for initializing the SDK.

   

5. [Configure obfuscation rules](): If you need to obfuscate the app code, you must modify the obfuscation configuration file.

   

6. [Compile the app](#section-olk-7bm-q7z): Troubleshoot common issues that may occur when you compile the app.

   




**Prepare for the integration** 
----------------------------------------------------

Open the configuration file of the app and find the `appmonitor.rsaSecret` field. The value of this field is the public key of the performance analysis service.
**Note**

For more information about how to obtain the configuration file of the app, see [Prerequisites](#section-3jg-dl7-zny).

Apply a plug-in 
------------------------------------

1. In the project-level `build.gradle` file, add plug-in dependencies to the `buildscript{}` code segment.

   
   **Notice**

   In this section, you only add plug-in dependencies to the buildscript{} code segment. To actually apply the plug-in, you must add plug-in dependencies to the `dependencies{}` code segment in the app-level `build.gradle` file. For more information, see [Add dependencies](#section-uqp-h2c-8jv).

       buildscript {
           repositories {
               google()
               jcenter()
           }
       dependencies {
           classpath 'com.android.tools.build:gradle:${gradle-version}'
           classpath 'com.aliyun.ams:alicloud-android-networkmonitor-plugin:1.2.0-open'}
       }

   

   The following table describes the parameter.
   

   |   Parameter    |                                                           Description                                                           |
   |----------------|---------------------------------------------------------------------------------------------------------------------------------|
   | gradle-version | The Gradle version in the development environment. Example: `classpath 'com.android.tools.build:gradle:4.8.1'`. |

   

2. In the app-level `build.gradle` file, add the following code segment to apply the plug-in:

       apply plugin: 'com.aliyun.emas.networkmonitor'

   




**Add dependencies** 
-----------------------------------------

1. Add the URL of the Alibaba Cloud Maven repository to the `repositories{}` code segment in the project-level `build.gradle` file.

       repositories {
           maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
       }

   

2. Set the .so libraries and the name of the app package in the `android{}` code segment in the app-level `build.gradle` file.

       android {
           ......
           defaultConfig {
               applicationId "com.xxx.xxx" 
               ......
               ndk {
                   // Select the .so libraries to be added based on the CPU types. Four libraries are supported.
                   abiFilters 'arm64-v8a', 'armeabi', 'armeabi-v7a', 'x86' 
               }
               ......
           }
           ......
       }

   

   The following table describes the parameters.
   

   |   Parameter   |                                                                                                                                                                                                                                                                 Description                                                                                                                                                                                                                                                                 |
   |---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | applicationId | The name of the app package. Data type: string. Method for obtaining the value: For more information, see [Prerequisites](#section-3jg-dl7-zny). Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                           |
   | ndk           | The architecture of the app. It is used to add the .so libraries based on the CPU types. Data type: enumeration. Valid values: * arm64-v8a   * armeabi   * armeabi-v7a   * x86    Required: yes. Whether the parameter can be left empty: no. Default value: none. Case-sensitive: no. |

   

3. In the app-level `build.gradle` file, add SDK dependencies to the `dependencies{}` code segment.

       dependencies {
           ......
           implementation fileTree(dir: 'libs', include: ['*.jar'])
           implementation "com.squareup.okhttp3:okhttp:${okhttp3version}"
       
           // Online test.
           implementation 'com.aliyun.ams:alicloud-android-ha-adapter:1.1.3.8-open'
           implementation 'com.aliyun.ams:alicloud-android-apm:1.0.8.2-open'
           ......
       }

   

   The following table describes the parameter.
   

   |   Parameter    |                                                                               Description                                                                                |
   |----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | okhttp3version | The version of the network library that is supported by the local development environment. Example: `implementation "com.squareup.okhttp3:okhttp:4.8.1"` |

   




**Integrate the service** 
----------------------------------------------

1. Define the `Application` class. Write the `onCreate` method to start the service.

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

   

   The following table describes the parameter.
   

   |   Parameter    |                                                                               Description                                                                                |
   |----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | okhttp3version | The version of the network library that is supported by the local development environment. Example: `implementation "com.squareup.okhttp3:okhttp:4.8.1"` |

   

2. In the `AndroidManifest.xml` file, add the code segment that is used to register the app.

       <application
               android:name=".MyApplication"
               android:icon="@mipmap/ic_launcher"
               android:label="@string/app_name"
               android:supportsRtl="true"
               android:theme="@style/AppTheme" >
       </application>

   




**Configure obfuscation rules** 
----------------------------------------------------

If you need to obfuscate the app code, add the following code segment to the obfuscation configuration file:

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



**Compile the app** 
----------------------------------------

If you have integrated SDKs of other Alibaba Cloud services, you may fail to compile the app because of a UTDID conflict. For more information about how to resolve this issue, see [How do I resolve a UTDID conflict of SDKs?]()

**Sample code** 
------------------------------------

For more information about the sample code on how to integrate the performance analysis SDK for Android, visit [Demo project](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo "Demo project").

**Verify the features of the SDK** 
-------------------------------------------------------

After you integrate the SDK for Android, you must check whether the SDK works as expected. To do so, perform operations on the app and view performance data in the performance analysis console.

1. Start the app. After 2 minutes, log on to the console. Check whether data is displayed on the **Startup Speed** page.

   

2. Switch pages in the app. After 2 minutes, log on to the console. Check whether data is displayed on the **Load Time** page.

   



**Note**

It takes about 2 minutes to upload the collected data to the console.

If the data is displayed as expected, the SDK for Android is properly integrated.

If the data is not displayed as expected, one of the following issues may exist: The SDK is not integrated, the data is not collected by the SDK, the data is not sent, or a server issue exists. To resolve this issue, contact Alibaba Cloud technical support. For more information, see [Technical support](/intl.en-US/.md).

Release notes of the SDK for Android 
---------------------------------------------------------



|   Version    | Release date |                        Description                        |
|--------------|--------------|-----------------------------------------------------------|
| 1.0.8.2-open | 2020-12-18   | The code is improved.                                     |
| 1.0.8.1-open | 2020-11-24   | Code compilation is improved.                             |
| 1.0.8.0-open | 2020-11-12   | The feature of analyzing network exceptions is supported. |
| Other historical versions.                                                            |||



