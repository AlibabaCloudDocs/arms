Integrate the SDK for iOS in pod mode 
==========================================================

This topic describes how to integrate the remote logs SDK for iOS in pod mode.
**Note**



* You can integrate the remote logs SDK for iOS in pod mode or manual mode. We recommend that you integrate the SDK in pod mode, which greatly simplifies the integration.

  

* For more information about how to add dependencies in manual mode, see [Integrate the SDK for iOS in manual mode]().

  




Prerequisites 
----------------------------------

The configuration file of the app is downloaded. For more information, see [Create an app monitoring task](/intl.en-US/App Monitoring/Create an app monitoring task.md).

Limits 
---------------------------

* Only apps that run on iOS 8.0 and later are supported.

  

* We recommend that you use CocoaPods to manage dependencies in Xcode projects.

  

* Logs can be stored on mobile terminals for a maximum of seven days.

  




Integration process 
----------------------------------------

1. [Add dependencies](#section-co8-1mu-uru): Add dependencies in pod mode.

   

2. [Integrate the service](#section-xhu-0uw-dhr): Add the configuration file of the app, import header files, initialize the SDK, and set the level of logs that can be pulled.

   

3. [Compile the app](#section-7in-758-eqm): Add compilation settings and perform compilation.

   

4. [Add the code for exporting logs](#section-bfh-c77-5bb).

   




Add dependencies 
-------------------------------------

1. Specify the official CocoaPods repository and the Alibaba Cloud repository.

       sou 
       rce " 
       https://github.com/CocoaPods/Specs.git"
       source "https://github.com/aliyun/aliyun-specs.git"

   

2. Add dependencies.

       pod 'AlicloudTLog', '~> 1.0.0.2'

   
   **Note**

   Run the `pod search AlicloudTLog` command to query the latest version of `AlicloudTLog`.
   

3. Run the `pod install` or `pod update` command to import the SDK package to the project.

   




Integrate the service 
------------------------------------------

1. Copy the configuration file `AliyunEmasServices-Info.plist` of the app to the root directory of the project.

   For more information about how to obtain the configuration file of the app, see [Prerequisites](#section-mh7-4ng-ixk).
   

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

  

* If you have integrated SDKs of other Alibaba Cloud services, you may fail to compile the app because of a UTDID conflict. For more information about how to resolve this issue, see [How do I resolve a UTDID conflict of SDKs?](https://help.aliyun.com/document_detail/172646.html)

  




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

For more information about the sample code on how to integrate the remote logs SDK for iOS, visit [Demo project](https://github.com/aliyun/alicloud-ios-demo/tree/master/tlog_ios_demo "Demo project").
