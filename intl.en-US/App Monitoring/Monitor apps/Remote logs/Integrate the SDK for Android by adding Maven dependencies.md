Integrate the SDK for Android by adding Maven dependencies 
===============================================================================

This topic describes how to integrate the remote logs SDK for Android by adding Maven dependencies.
**Note**



* You can integrate the remote logs SDK for Android by adding Maven dependencies or local dependencies. We recommend that you integrate the SDK by adding Maven dependencies, which greatly simplifies the integration.

  

* For more information about how to integrate the SDK by adding local dependencies, see [Integrate the SDK for Android by adding local dependencies]().

  




Prerequisites 
----------------------------------

The configuration file of the app is downloaded, and the AppKey, AppSecret, and PackageName are obtained from the configuration file. For more information, see [Create an app monitoring task](/intl.en-US/App Monitoring/Create an app monitoring task.md).

Limits 
---------------------------

* Only Android 4.2 and later are supported.

  

* Only the architectures of armeabi, armeabi-v7a and x86 are supported.

  

* Logs can be stored on mobile terminals for a maximum of seven days.

  




Integration process 
----------------------------------------

1. 

2. [Prepare for the integration](#section-j9o-zby-llm): Obtain the public key.

   

3. [Add dependencies](#section-02t-297-szf): Integrate the SDK by adding Maven dependencies.

   

4. [Integrate the service](#section-2k6-1na-37h): Define the custom Application class and initialize the code. Configure the Application Binary Interface (ABI). Set the level of logs that can be pulled in the console.

   

5. [Add the code for exporting logs](#section-sur-n4a-0td): Import a header file and add the code for exporting logs.

   

6. [Configure obfuscation rules](#section-nv9-gdo-ze9): If you need to obfuscate the app code, you must modify the obfuscation configuration file.

   

7. [Compile the app](#section-2jt-n88-hk9).

   




Prepare for the integration 
------------------------------------------------

Open the configuration file of the app and find the `appmonitor.tlog.rsaSecret` field. The value of this field is the public key of the remote logs service.

![Public key](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5467545161/p181557.png)



Add dependencies 
-------------------------------------

1. Add the URL of the Alibaba Cloud Maven repository to the `repositories{}` code segment in the project-level `build.gradle` file.

       repositories {
           maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
       }

   

2. Add the SDK dependencies to the `dependencies{}` code segment in the app-level `build.gradle` file.

       implementation('com.aliyun.ams:alicloud-android-ha-adapter:1.1.3.8-open@aar') {
           transitive=true
       }
       implementation('com.aliyun.ams:alicloud-android-tlog:1.1.3.1-open@aar') {
           transitive=true
       }

   

3. Configure the ABI in the `defaultConfig{}` code segment in the app-level `build.gradle` file.

       ndk {
               abiFilters 'armeabi'    // Configuration item: the ABI. Valid values: armeabi, armeabi-v7a, and x86.
       }

   

   
   **Notice**

   The remote logs service supports only the architectures of armeabi, armeabi-v7a, and x86.
   




Integrate the service 
------------------------------------------

1. Define the `Application` class. Write the `onCreate` method to start the service.

       public class MyApplication extends Application {
           @Override
           public void onCreate() {
               initHa();
           }
           private void initHa() {
                AliHaConfig config = new AliHaConfig();
                config.appKey = "xxxxxxxx"; // Configuration item: 
        the AppKey 
       .
                config.appVersion = "x.xx"; // Configuration item: the version number of the app.
                config.appSecret = "xxxxxxxxxxxx"; // Configuration item: the AppSecret.
                config.channel = "mqc_test"; // Configuration item: the user-defined identifier of the channel.
                config.userNick = null; // Configuration item: the nickname of the user.
                config.application = this; // Configuration item: the pointer of the app.
                config.context = getApplicationContext(); // Configuration item: the context of the app.
                config.isAliyunos = false; // Configuration item: specifies whether the platform where the app resides is YunOS.
                config.rsaPublicKey = "xxxxxxx"; // Configuration item: the public key of the remote logs service.
                AliHaAdapter.getInstance().addPlugin(Plugin.tlog);
                AliHaAdapter.getInstance().openDebug(true);
                AliHaAdapter.getInstance().start(config);
                TLogService.updateLogLevel(TLogLevel.XXXXXX); // Configuration item: the level of logs that can be pulled in the console.
           }
       }

   

   The following table describes the parameters.
   

   |      Parameter      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   |---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | config.appKey       | The AppKey of the app. Data type: string. Method for obtaining the value: For more information, see [Prerequisites](#section-eyb-u7r-lhc). Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   | config.appVersion   | The version number of the app. Data type: string. Format: user-defined. Valid value: a string of infinite length. **Note** In the console, the parameter value is displayed in a drop-down list. Therefore, we recommend that you specify a value as short as possible. Required: yes. Whether the parameter can be left empty: no. Default value: none. Case-sensitive: yes. For example, vx.x and Vx.x do not indicate the same version. Character type: letters and digits. **Note** Special characters are not supported.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
   | config.appSecret    | The AppSecret of the app. Data type: string. Method for obtaining the value: For more information, see [Prerequisites](#section-eyb-u7r-lhc). Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   | config.channel      | The identifier of the channel. Channel identifiers are sent to the server to distinguish channels. Data type: string. Valid value: a string of infinite length. Required: no. Whether the parameter can be left empty: yes. Default value: none. Character type: letters and digits. **Note** Special characters are not supported.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   | config.userNick     | The nickname of the user. Nicknames are sent to the server to distinguish users. You can query data later based on this parameter. Data type: string. Valid value: a string of infinite length. Required: no. Whether the parameter can be left empty: yes. Default value: none. Character type: letters and digits. **Note** Special characters are not supported. Naming conventions: user-defined.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
   | config.application  | The pointer of the app. **Notice** This parameter cannot be used to point to another app. Data type: object. Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
   | config.context      | The context of the app. Set the value to `getApplicationContext()`. Data type: object. Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   | config.isAliyunos   | Specifies whether the platform where the app resides is YunOS. Data type: Boolean. Valid value: true or false. Required: no. Whether the parameter can be left empty: yes. Default value: false.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   | config.rsaPublicKey | The public key of the remote logs service. Data type: string. Method for obtaining the value: For more information, see [Prepare for the integration](#section-j9o-zby-llm). Required: yes. Whether the parameter can be left empty: no. Default value: none.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
   | TLogLevel.XXXXXX    | The level of logs that can be pulled in the console. This parameter is a global setting. Data type: enumeration. Valid values: * VERBOSE: indicates that logs of all levels can be pulled.   * DEBUG: indicates that logs of the DEBUG, INFO, WARN, and ERROR levels can be pulled.   * INFO: indicates that logs of the INFO, WARN, and ERROR levels can be pulled.   * WARN: indicates that logs of the WARN and ERROR levels can be pulled.   * ERROR: indicates that logs of the ERROR level can be pulled.    Required: yes. Default value: ERROR. Configuration note: * The `TLogService.updateLogLevel()` function is optional to call. If this function is not called, the globally default level of logs that can be pulled is ERROR.   * For more information about log levels, see [Terms]().    |

   

2. In the `AndroidManifest.xml` file, add the code segment that is used to register the app.

       <application
           android:name=".MyApplication"
           android:icon="@mipmap/ic_launcher"
           android:label="@string/app_name"
           android:supportsRtl="true"
           android:theme="@style/AppTheme" >
           ...
       </application>

   




Add the code for exporting logs 
----------------------------------------------------

1. Import the header file to allow the app to trigger log export.

       import com.alibaba.ha.adapter.service.tlog.TLogService;

   

2. Add the code for exporting logs to an appropriate location. Sample code:

       TLogService.logv("MODEL","TAG","MESSAGE");
       TLogService.logd("MODEL","TAG","MESSAGE");
       TLogService.logi("MODEL","TAG","MESSAGE");
       TLogService.logw("MODEL","TAG","MESSAGE");
       TLogService.loge("MODEL","TAG","MESSAGE");

   




**Function** : `TLogService. <LogLevel>(<MODEL>,<TAG,<MESSAGE>);`

**Description** : specifies the level of logs to be exported.


| Parameter |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| LogLevel  | The level of logs to be exported. For more information about log levels, see [Terms](). Data type: enumeration. Valid values: * logv: indicates that logs of the VERBOSE level are exported.   * logd: indicates that logs of the DEBUG level are exported.   * logi: indicates that logs of the INFO level are exported.   * logw: indicates that logs of the WARN level are exported.   * loge: indicates that logs of the ERROR level are exported.    Configuration note: Whether exported logs can be pulled by the console depends on the parameter setting of the `TLogService.updateLogLevel()` function. For example, if `TLogService.updateLogLevel(TLogLevel.WARN)` is specified in the Application class, logs that are exported based on the logv, logd, and logi options cannot be pulled in the console. |
| MODEL     | The module for which logs are exported. This parameter allows you to filter logs later by source. Data type: string. Character type: letters, digits, and special characters. Required: yes. Case-sensitive: no. Example: "Push"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| TAG       | The keywords of logs to be exported. This parameter allows you to filter logs later by tags. Data type: string. Character type: letters, digits, and special characters. Required: yes. Case-sensitive: no. Example: "Push.receive, Push.click"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| MESSAGE   | The log information to be exported. Data type: string. Character type: letters, digits, and special characters. Required: yes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |



Configure obfuscation rules 
------------------------------------------------

If you need to obfuscate the app code, add the following code segment to the obfuscation configuration file:

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
    -keep class com.taobao.tao.log.monitor. **{*;}
    # Compatible with GodEye
    -keep class com.taobao.tao.log.godeye.core.module.*{*;}
    -keep class com.taobao.tao.log.godeye.GodeyeInitializer{*;}
    -keep class com.taobao.tao.log.godeye.GodeyeConfig{*;}
    -keep class com.taobao.tao.log.godeye.core.control.Godeye{*;}
    -keep interface com.taobao.tao.log.godeye.core.GodEyeAppListener{*;}
    -keep interface com.taobao.tao.log.godeye.core.GodEyeReponse{*;}
    -keep interface com.taobao.tao.log.godeye.api.file.FileUploadListener{*;}
    -keep public class * extends com.taobao.android.tlog.protocol.model.request.base.FileInfo{*;}
    -keepattributes Exceptions,InnerClasses,Signature,Deprecated,SourceFile,LineNumberTable,*Annotation*,EnclosingMethod



Compile the app 
------------------------------------

If you have integrated SDKs of other Alibaba Cloud services, you may fail to compile the app because of a UTDID conflict. For more information about how to resolve this issue, see [How do I resolve a UTDID conflict of SDKs?](https://help.aliyun.com/document_detail/172646.html)

Sample code 
--------------------------------

For more information about the sample code on how to integrate the remote logs SDK for Android, visit [Demo project](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo "Demo project").
