Integrate the SDK for Android by adding local dependencies 
===============================================================================

This topic describes how to integrate the performance analysis SDK for Android by adding local dependencies.
**Note**

* You can integrate the performance analysis SDK for Android by adding Maven dependencies or local dependencies. We recommend that you integrate the SDK by adding Maven dependencies, which greatly simplifies the integration.

  

* For more information about how to integrate the SDK by adding Maven dependencies, see [Integrate the SDK for Android by adding Maven dependencies]().

  




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

1. [Prepare for the integration](#section-yf7-0kk-klr): Obtain the public key and download the SDK package.

   

2. [Apply a plug-in](#section-8k1-0s2-y4y): Add plug-in dependencies to apply a plug-in.

   

3. [Add dependencies](#section-rjc-6c4-fgb): Integrate the SDK by adding local dependencies. For more information about the changes of the SDK, see [Release notes of the SDK for Android](#section-vxx-a3n-ffx).

   

4. [Integrate the service](#section-bfc-lb6-yqo): Define the custom Application class and add the code for initializing the SDK.

   

5. [Configure obfuscation rules](#section-i7h-4cw-mwt): If you need to obfuscate the app code, you must modify the obfuscation configuration file.

   

6. [Compile the app](#section-5x5-0m3-h8l): Troubleshoot common issues that may occur when you compile the app.

   




**Prepare for the integration** 
----------------------------------------------------

**Obtain the public key of the performance analysis service** 

Open the configuration file of the app and find the `appmonitor.rsaSecret` field. The value of this field is the public key of the performance analysis service.
**Note**

For more information about how to obtain the configuration file of the app, see [Prerequisites](#section-rby-od8-oxf).

**Download the SDK package** 

1. Log on to the [Enterprise Mobile Application Studio (EMAS) console](https://emas.console.aliyun.com/productLis#/overview). On the **Workspace Overview** page, click **SDK Download** . The **SDK Download** panel appears.

   

2. In the **SDK Download** panel, select **Performance Analysis** and click **Download Android Version** to download the SDK package of the performance analysis service.

   **Note**

   In the **Android Version** column of the **Performance Analysis** row, click a version number to view the changes of the SDK.

   

3. Check the SDK package to ensure its integrity. The SDK package contains the following files:

   




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

  




Apply a plug-in 
------------------------------------

1. In the project-level `build.gradle` file, add plug-in dependencies to the `buildscript{}` code segment.

   **Note**

   In this section, you only add plug-in dependencies to the buildscript{} code segment. To actually apply the plug-in, you must add plug-in dependencies to the `dependencies{}` code segment in the app-level `build.gradle` file. For more information, see [Add dependencies](#section-rjc-6c4-fgb).

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

1. Copy all the files in the SDK package to the libs directory of your project.

   

2. In the project-level `build.gradle` file, add the path of the directory that stores local SDK files.

       repositories {
          flatDir {
              dirs 'libs'
          }
       }

   

3. In the app-level `build.gradle` file, add SDK dependencies to the `dependencies{}` code segment.

           //1. Import local JAR libraries.
           compile fileTree(include: ['*.jar'], dir: 'libs')
           //2. Import public libraries.
           compile (name: 'alicloud-android-ha-adapter-1.1.3.8-open', ext: 'aar')
           compile (name: 'alicloud-android-ha-core-1.1.0.6.1-open', ext: 'aar')
           compile (name: 'alicloud-android-ha-protocol-1.1.1.0-open', ext: 'aar')
           compile (name: 'alicloud-android-ha-tbrest-1.1.1.0-open', ext: 'aar')
           compile (name: 'alicloud-android-utdid-2.5.1-proguard', ext: 'jar')
           compile (name: 'fastjson-1.1.54.android', ext: 'jar')
           // 3. Import the libraries of the performance analysis service. If you do not want to integrate the performance analysis service, comment out the following code:
           compile (name: 'alicloud-android-ha-apm-1.0.8.2-open', ext: 'aar')
           compile (name: 'alicloud-android-ha-apm-impl-1.0.7.1-open', ext: 'aar')
           compile (name: 'alicloud-android-ha-fulltrace-1.0.1.12', ext: 'aar')
           compile (name: 'alicloud-android-networkmonitor-1.4.0', ext: 'aar)
           compile (name: 'alicloud-android-rest-1.4.0-open', ext: 'aar)

   




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

   

   The following table describes the parameters.

   
   

   |  Parameter   |                                                                                                                                                                                                                                                                                                                                  Description                                                                                                                                                                                                                                                                                                                                  |
   |--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | appKey       | The AppKey of the app. Data type: string. Method for obtaining the value: For more information, see [Prerequisites](#section-rby-od8-oxf). Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                   |
   | appVersion   | The version number of the app. Data type: string. Format: user-defined. Valid value: a string of infinite length. **Note** In the console, the parameter value is displayed in a drop-down list. Therefore, we recommend that you specify a value as short as possible. Required: yes. Whether the parameter can be left empty: no. Default value: none. Case-sensitive: yes. For example, vx.x and Vx.x do not indicate the same version. Character type: letters and digits. **Note** Special characters are not supported. |
   | appSecret    | The AppSecret of the app. Data type: string. Method for obtaining the value: For more information, see [Prerequisites](#section-rby-od8-oxf). Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                |
   | channel      | The identifier of the channel. Channel identifiers are sent to the server to distinguish channels. Data type: string. Valid value: a string of infinite length. Required: no. Whether the parameter can be left empty: yes. Default value: none. Character type: letters and digits. **Note** Special characters are not supported.                                                                                                                                                                                                                           |
   | userNick     | The nickname of the user. Nicknames are sent to the server to distinguish users. You can query data later based on this parameter. Data type: string. Valid value: a string of infinite length. Required: no. Whether the parameter can be left empty: yes. Default value: none. Character type: letters and digits. **Note** Special characters are not supported. Naming conventions: user-defined.                                                                                                                                                         |
   | application  | The pointer of the app. **Notice** This parameter cannot be used to point to another app. Data type: object. Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                                                                                 |
   | context      | The context of the app. Set the value to `getApplicationContext()`. Data type: object. Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   | isAliyunos   | Specifies whether the platform where the app resides is YunOS. Data type: Boolean. Valid value: true or false. Required: no. Whether the parameter can be left empty: yes. Default value: false.                                                                                                                                                                                                                                                                                                                                                                                              |
   | rsaPublicKey | The public key of the performance analysis service. Data type: string. Method for obtaining the value: For more information, see [Prepare for the integration](#section-yf7-0kk-klr). Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                        |

   

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

For more information about the sample code on how to integrate the performance analysis SDK for Android, see [Demo project](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo "Demo project").

**Verify the features of the SDK** 
-------------------------------------------------------

After you integrate the SDK for Android, you must check whether the SDK works as expected. To do so, perform operations on the app and view performance data in the performance analysis console.

1. Start the app. After 2 minutes, log on to the console. Check whether data is displayed on the **Startup Speed** page.

   

2. Switch pages in the app. After two minutes, log on to the console. Check whether data is displayed on the **Load Time** page.

   



**Note**

It takes about 2 minutes to upload the collected data to the console.

If data is displayed as expected, the SDK for Android is properly integrated.

If data is not displayed as expected, one of the following issues may exist: The SDK is not integrated, the data is not collected by the SDK, the data is not sent, or a server issue exists. To resolve this issue, contact Alibaba Cloud technical support. For more information, see [Technical support](/intl.en-US/.md).



Release notes of the SDK for Android 
---------------------------------------------------------



|   Version    | Release date |                        Description                        |
|--------------|--------------|-----------------------------------------------------------|
| 1.0.8.2-open | 2020-12-18   | The code is improved.                                     |
| 1.0.8.1-open | 2020-11-24   | Code compilation is improved.                             |
| 1.0.8.0-open | 2020-11-12   | The feature of analyzing network exceptions is supported. |
| Other historical versions.                                                            |||


