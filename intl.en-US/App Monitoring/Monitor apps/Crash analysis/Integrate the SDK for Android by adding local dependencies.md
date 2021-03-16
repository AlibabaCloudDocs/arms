Integrate the SDK for Android by adding local dependencies 
===============================================================================

This topic describes how to integrate the crash analysis SDK for Android by adding local dependencies.
**Note**



* You can integrate the crash analysis SDK for Android by adding Maven dependencies or local dependencies. We recommend that you integrate the SDK by adding Maven dependencies, which greatly simplifies the integration.

  

* For more information about how to integrate the SDK by adding Maven dependencies, see [Integrate the SDK for Android by using Maven dependencies](/intl.en-US/App Monitoring/Monitor apps/Crash analysis/Integrate the SDK for Android by adding Maven dependencies.md).

  

* The network monitoring feature of crash analysis has been released in canary mode. If you want to try this feature, contact Alibaba Cloud technical support to obtain the SDK package. For more information, see [Technical support](/intl.en-US/.md).

  




Prerequisites 
----------------------------------

* 

* 

* The AppKey and AppSecret are obtained from the configuration file of the app. For more information, see [Create an app monitoring task](/intl.en-US/App Monitoring/Create an app monitoring task.md).

  

* The crash analysis SDK for Android is downloaded. For more information, see the Download the SDK section in [Quick Start](https://help.aliyun.com/document_detail/169962.html#title-fvd-ozh-524).

  




Limits 
---------------------------

* Only Android 4.0 and later are supported.

  

* Only the architectures of arm64-v8a, armeabi, armeabi-v7a, and x86 are supported.

  




Procedure 
------------------------------

1. **Add dependencies.** 

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
              compile (name: 'alicloud-android-ha-adapter-1.1.3.7-open', ext: 'aar')
              compile (name: 'alicloud-android-ha-core-1.1.0.6.1-open', ext: 'aar')
              compile (name: 'alicloud-android-ha-protocol-1.1.1.0-open', ext: 'aar')
              compile (name: 'alicloud-android-ha-tbrest-1.1.1.0-open', ext: 'aar')
              compile (name: 'alicloud-android-utdid-2.5.1-proguard', ext: 'jar')
              compile (name: 'fastjson-1.1.54.android', ext: 'jar')
              //3. Import libraries of the crash analysis service.
              compile (name: 'alicloud-android-ha-crashreporter-1.2.4', ext: 'aar')
              compile (name: 'alicloud-android-ha-watch-1.1.0.6.1-open', ext: 'aar')
              compile (name: 'alicloud-android-ha-bizerrorreporter-1.1.0.9-open', ext: 'aar')
              compile (name: 'alicloud-android-ha-olympic-1.0.4.37', ext: 'aar')

      
   

   

2. **Integrate the service.** 

   1. Define the Application class. Write the onCreate method to start the service.

      **Note**

      We recommend that you place the code segment that is used to initialize the crash analysis SDK before business code. This ensures that the crash analysis service is preferentially loaded when the app starts. This way, subsequent crash information can be collected and uploaded to the console at the earliest opportunity.

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
                  // Start CrashReporter.
                  AliHaAdapter.getInstance().addPlugin(Plugin.crashreporter);
                  AliHaAdapter.getInstance().start(config);
             }
          }

      

      The following table describes the parameters.
      

      |  Parameter  |                                                                                                                                                                                                                                                                                                                                  Description                                                                                                                                                                                                                                                                                                                                  |
      |-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
      | appKey      | The AppKey of the app. Data type: string. Method for obtaining the value: For more information, see [Prerequisites](#section-1je-j5a-e53). Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                   |
      | appVersion  | The version number of the app. Data type: string. Format: user-defined. Valid value: a string of infinite length. **Note** In the console, the parameter value is displayed in a drop-down list. Therefore, we recommend that you specify a value as short as possible. Required: yes. Whether the parameter can be left empty: no. Default value: none. Case-sensitive: yes. For example, vx.x and Vx.x do not indicate the same version. Character type: letters and digits. **Note** Special characters are not supported. |
      | appSecret   | The AppSecret of the app. Data type: string. Method for obtaining the value: For more information, see [Prerequisites](#section-1je-j5a-e53). Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                |
      | channel     | The identifier of the channel. Channel identifiers are sent to the server to distinguish channels. Data type: string. Valid value: a string of infinite length. Required: no. Whether the parameter can be left empty: yes. Default value: none. Character type: letters and digits. **Note** Special characters are not supported.                                                                                                                                                                                                                           |
      | userNick    | The nickname of the user. Nicknames are sent to the server to distinguish users. You can query data later based on this parameter. Data type: string. Valid value: a string of infinite length. Required: no. Whether the parameter can be left empty: yes. Default value: none. Character type: letters and digits. **Note** Special characters are not supported. Naming conventions: user-defined.                                                                                                                                                         |
      | application | The pointer of the app. This parameter cannot be used to point to another app. Data type: object. Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                                                                                            |
      | context     | The context of the app. Set the value to getApplicationContext(). Data type: object. Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                                                                                                         |
      | isAliyunos  | Specifies whether the platform where the app resides is YunOS. Data type: Boolean. Valid value: true or false. Required: no. Whether the parameter can be left empty: yes. Default value: false.                                                                                                                                                                                                                                                                                                                                                                                              |

      
   
   2. In the AndroidManifest.xml file, add the code segment that is used to register the app.

          <application
                  android:name=".MyApplication"
                  android:icon="@mipmap/ic_launcher"
                  android:label="@string/app_name"
                  android:supportsRtl="true"
                  android:theme="@style/AppTheme" >
          </application>

      
   

   

3. **Add advanced settings.** 

   The SDK for Android provides methods that allow you to report custom information or errors.

       // Report custom information.
       AliHaAdapter.getInstance().addCustomInfo("key", "value");     // Configuration item: the custom environment information.
       
       // Report custom information based on the exception type.
       AliHaAdapter.getInstance().setErrorCallback(new ErrorCallback() {
           @Override
           public Map<String, String> onError(ErrorInfo callbackInfo) {
               Map<String, String> infos = new HashMap<>();
               infos.put("key", "value");     // Configuration item: the exception information.
               return infos;
           }
       });
       
       // Report a custom error.
       AliHaAdapter.getInstance().reportCustomError(new RuntimeException("custom error"));     // Configuration item: the custom error information.

   

   For more information, see [Reference of the SDK for Android]().
   

4. **Configure obfuscation rules.** 

   If you need to obfuscate the app code, add the following code segment to the obfuscation configuration file:

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

   

5. **Compile the app.** 

   If you have integrated SDKs of other Alibaba Cloud services, you may fail to compile the app because of a UTDID conflict. For more information about how to resolve this issue, see [How do I resolve a UTDID conflict of SDKs?](https://help.aliyun.com/document_detail/172616.html)
   

6. **Verify the features of the SDK.** 

   After you integrate the SDK for Android, you must check whether the SDK works as expected.
   1. Write and run test code to simulate or trigger an app crash on a mobile terminal. Example:

          throw new NullPointerException();

      
   
   2. Restart the mobile terminal. After about 2 minutes, check whether crash information is displayed in the console.

      **Note**

      It takes about 2 to 3 minutes to upload the collected crash information to the console.
      * If crash information is displayed, the SDK is properly integrated.

        
      
      * If crash information is not displayed, troubleshoot the issue by performing the operations that are described in Step c.

        
      

      
   
   3. When you simulate or trigger a crash, or restart the mobile terminal, use Charles to capture packets to check whether the HTTP request that contains `https://adash-emas.cn-hangzhou.aliyuncs.com/upload` can be captured.

      * If such an HTTP request is captured, crash information is reported. In this case, crash information is not displayed because the crash analysis service is disabled on the server, or the AppKey or AppSecret is invalid.

        
      
      * If no such HTTP request is captured, crash information is not reported. In this case, the crash information is not displayed because the SDK fails to be integrated, the SDK fails to capture the crash information, or the crash information fails to be sent. To resolve this issue, contact Alibaba Cloud technical support. For more information, see [Technical support](/intl.en-US/.md).

        
      

      
   

   




Sample code 
--------------------------------

For more information about the sample code on how to integrate the crash analysis SDK for Android, visit [Demo project](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo?spm=a2c4g.11186623.2.27.789073c8I6rfk5).