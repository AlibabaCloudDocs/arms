Integrate the SDK for iOS in manual mode 
=============================================================

This topic describes how to integrate the remote logs SDK for iOS by adding dependencies in manual mode.
**Note**



* You can integrate the remote logs SDK for iOS in pod mode or manual mode. We recommend that you integrate the SDK in pod mode, which greatly simplifies the integration.

  

* For more information about how to integrate the SDK in pod mode, see [Integrate the SDK for iOS in pod mode](/intl.en-US/App Monitoring/Monitor apps/Remote logs/Integrate the SDK for iOS in pod mode.md).

  




Prerequisites 
----------------------------------

The configuration file of the app is downloaded. For more information, see [Create an app monitoring task](/intl.en-US/App Monitoring/Create an app monitoring task.md).

Limits 
---------------------------

* Only apps that run on iOS 8.0 and later are supported.

  

* Logs can be stored on mobile terminals for a maximum of seven days.

  




Integration process 
----------------------------------------

1. [Prepare for the integration](#section-iqt-3k8-wix): Download the SDK package.

   

2. [Add dependencies](#section-f48-x1u-5bn): Integrate the SDK in manual mode.

   

3. [Integrate the service](#section-ek1-jis-fjw): Add the configuration file of the app, import header files, initialize the SDK, and set the level of logs that can be pulled.

   

4. [Compile the app](#section-rgt-nkx-aor): Add compilation settings and perform compilation.

   

5. [Add the code for exporting logs](#section-45i-qor-oqy).

   




Prepare for the integration 
------------------------------------------------

1. Log on to the [EMAS console](https://emas.console.aliyun.com/productLis#/overview). On the **Workspace Overview** page, click **SDK Download** . The **SDK Download** panel appears.

   

2. In the **SDK Download** panel, select **Remote Logging** and click **Download iOS Version** to download the SDK package of the remote logs service.

   
   **Note**

   In the **iOS Version** column of the **Remote Logging** row, click a version number to view the changes of the SDK.

   

3. Check the SDK package to ensure its integrity.

   The SDK package contains the following files:
   




* AlicloudHAUtil.framework

  

* AlicloudTLog.framework

  

* AlicloudUtils.framework

  

* AliHACore.framework

  

* AliHALogEngine.framework

  

* AliHAMethodTrace.framework

  

* AliHAProtocol.framework

  

* AliHASecurity.framework

  

* AliyunOSSiOS.framework

  

* RemoteDebugChannel.framework

  

* TBJSONModel.framework

  

* TBRest.framework

  

* TRemoteDebugger.framework

  

* UTDID.framework

  

* UTMini.framework

  

* ZipArchive.framework

  




Add dependencies 
-------------------------------------

1. In Xcode, drag the FRAMEWORK files from the directory that stores the downloaded SDK files to the Target directory. In the dialog box that appears, select `Copy items if needed`.

   

2. Choose **Build Phases** \> **Link Binary With Libraries** and add the following public packages of Xcode:

   




* libc++.tbd

  

* libresolv.tbd

  

* SystemConfiguration.framework

  




Integrate the service 
------------------------------------------

1. Copy the configuration file `AliyunEmasServices-Info.plist` of the app to the root directory of the project.

   For more information about how to obtain the configuration file of the app, see [Prerequisites](#section-og0-e1z-b5e).
   

2. In the `AppDelegate.m` file, add the code for importing header files.

       #import <AlicloudTLog/AlicloudTlogProvider.h>
       #import <AlicloudHAUtil/AlicloudHAProvider.h>
       #import <TRemoteDebugger/TRDManagerService.h>

   

3. Add the code for initializing the SDK to the `application:didFinishLaunchingWithOptions` method in the `AppDelegate.m` file.

       NSString *appVersion = @"x.x"; // Configuration item: the version number of the app.
       NSString *channel = @"xx"; // Configuration item: the identifier of the channel.
       NSString *nick = @"xx"; // Configuration item: the nickname of the user.
       [[AlicloudTlogProvider alloc] autoInitWithAppVersion:appVersion channel:channel nick:nick];
       [AlicloudHAProvider start];
       [TRDManagerService updateLogLevel:TLogLevelXXX]; // Configuration item: the level of logs that can be pulled in the console.

   




The following table describes the parameters.


|  Parameter   |                                                                                                                                                                                                                                                                                                                                                                                                                               Description                                                                                                                                                                                                                                                                                                                                                                                                                               |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| appVersion   | The version number of the app. Version numbers are sent to the server to distinguish versions. Data type: string. Format: user-defined. Valid value: a string of infinite length. **Note** In the console, the parameter value is displayed in a drop-down list. Therefore, we recommend that you specify a value as short as possible. Required: yes. Whether the parameter can be left empty: no. Default value: none. Case-sensitive: yes. For example, vx.x and Vx.x do not indicate the same version. Character type: letters and digits. **Note** Special characters are not supported. Example: `NSString *appVersion = @"1.0";`                                                                                 |
| channel      | The identifier of the channel. Channel identifiers are sent to the server to distinguish channels. Data type: string. Valid value: a string of infinite length. Required: yes. Whether the parameter can be left empty: no. Default value: none. Character type: letters and digits. **Note** Special characters are not supported. Example: `NSString *channel = @"appstore";`                                                                                                                                                                                                                                                                                                                                                                         |
| nick         | The nickname of the user. Nicknames are sent to the server to distinguish users. You can query data later based on this parameter. Data type: string. Valid value: a string of infinite length. Required: yes. Whether the parameter can be left empty: no. Default value: none. Character type: letters and digits. **Note** Special characters are not supported. Naming conventions: user-defined. Example: `NSString *nick = @"wldtest";`                                                                                                                                                                                                                                                                                           |
| TLogLevelXXX | The level of logs that can be pulled in the console. For more information about log levels, see [Terms](). Data type: enumeration. Valid values: * TLogLevelError: indicates that logs of the Error level can be pulled.   * TLogLevelWarn: indicates that logs of the Warn and Error levels can be pulled.   * TLogLevelInfo: indicates that logs of the Warn, Error, and Info levels can be pulled.   * TLogLevelDebug: indicates that logs of the Warn, Error, Info, and Debug levels can be pulled.    Required: no. Default value: TLogLevelInfo Example: `[TRDManagerService updateLogLevel:TLogLevelInfo];` |


**Note**

We recommend that you use the `autoInitWithAppVersion` method to integrate the service. If you want to use the `initWithAppKey` method to integrate the service, you must specify the `appKey`, `secret`, and `tlogRsaSecret` parameters.

Open the configuration file of the app to query the parameters.


|   Parameter   | Field in the configuration file |                   Description                    |
|---------------|---------------------------------|--------------------------------------------------|
| appKey        | emas.appKey                     | The identifier of the app.                       |
| secret        | emas.appSecret                  | The secret that is used to authenticate the app. |
| tlogRsaSecret | appmonitor.tlog.rsaSecret       | The public key of the remote logs service.       |



Compile the app 
------------------------------------

1. Set the `Allow Non-modular Includes In Framework Modules` parameter to `Yes` in the build settings of the project.

   

2. Perform compilation.

   



**Note**



* If the `duplicate symbol` error is reported during compilation, check whether your local dependencies are included in the dependencies that are managed by CocoaPods. If so, delete the local dependencies.

  

* If you have integrated SDKs of other Alibaba Cloud services, you may fail to compile the app because of a UTDID conflict. For more information about how to resolve this issue, see [How do I resolve a UTDID conflict of SDKs?](https://help.aliyun.com/document_detail/172653.html)

  




Add the code for exporting logs 
----------------------------------------------------

1. Import the header file to allow the app to trigger log export.

       #import <TRemoteDebugger/TLogBiz.h>
       #import <TRemoteDebugger/TLogFactory.h>
       #import <TRemoteDebugger/TRDManagerService.h>

   

2. Add the code for exporting logs to an appropriate location. Sample code:

       TLogBiz *log = [TLogFactory createTLogForModuleName:@"YourModuleName"];
       [log error:@"error message"];
       [log warn:@"warn message"];
       [log debug:@"debug message"];
       [log info:@"info message"];

   




|           Parameter           |                                                                    Description                                                                    |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| YourModuleName                | The module for which logs are exported.                                                                                                           |
| error/warn/debug/info message | The logs that are exported by log level. You can query logs later by level. For more information about log levels, see [Terms](). |



Sample code 
--------------------------------

For more information about the sample code on how to integrate the remote logs SDK for iOS, see [Demo project](https://github.com/aliyun/alicloud-ios-demo/tree/master/tlog_ios_demo "Demo project").
