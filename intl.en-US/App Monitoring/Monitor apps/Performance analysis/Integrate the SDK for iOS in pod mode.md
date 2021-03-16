Integrate the SDK for iOS in pod mode 
==========================================================

This topic describes how to integrate the performance analysis SDK for iOS in pod mode.
**Note**



* You can integrate the performance analysis SDK for iOS in pod mode or manual mode. We recommend that you integrate the SDK in pod mode, which greatly simplifies the integration.

  

* For more information about how to integrate the SDK in manual mode, see [Integrate the SDK for iOS in manual mode]().

  




**Prerequisites** 
--------------------------------------

The configuration file of the app is downloaded. For more information, see [Create an app monitoring task](/intl.en-US/App Monitoring/Create an app monitoring task.md).

**Limits** 
-------------------------------

* Only apps that run on iOS 8.0 and later are supported.

  




**Integration process** 
--------------------------------------------

To integrate the performance analysis SDK for iOS, perform the following steps:

1. [Add dependencies](#section-55e-8q3-x3x): Add dependencies in pod mode.

   

2. [Integrate the service](#section-kjj-wq2-uim): Initialize the SDK and integrate the service.

   

3. [Compile the app](#section-bd5-cjc-um5): Add compilation settings and perform compilation.

   




**Add dependencies** 
-----------------------------------------

1. Specify the official CocoaPods repository and the Alibaba Cloud repository.

       source "https://github.com/CocoaPods/Specs.git"
       source "https://github.com/aliyun/aliyun-specs.git"

   

2. Add dependencies.

       pod 'AlicloudAPM', '1.1.1'

   
   **Note**

   Run the `pod search AlicloudAPM` command to query the latest version of AlicloudAPM.
   

3. Run the `pod update` command and save the settings.

   




**Integrate the service** 
----------------------------------------------

1. Copy the configuration file `AliyunEmasServices-Info.plist` of the app to the root directory of the project.

   **Note**

   For more information about how to obtain the configuration file of the app, see [Prerequisites](#section-c1s-lki-6og).
   

2. Add the code for initializing the SDK to the `application:didFinishLaunchingWithOptions` method in the `AppDelegate.m` file.

   Add the following code for importing header files:

       #import <AlicloudAPM/AlicloudAPMProvider.h>
       #import <AlicloudHAUtil/AlicloudHAProvider.h>

   

   Add the following code segment:

       NSString *appVersion = @"xxx";  
       NSString *channel = @"xxx";  
       NSString *nick = @"xxx"; 
       [[AlicloudAPMProvider alloc] autoInitWithAppVersion:appVersion channel:channel nick:nick];
       [AlicloudHAProvider start];

   

   The following table describes the parameters.
   

   | Parameter  |                                                                                                                                                                                                                                                                                                                                                                                       Description                                                                                                                                                                                                                                                                                                                                                                                       |
   |------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | appVersion | The version number of the app. Version numbers are sent to the server to distinguish versions. Data type: string. Format: user-defined. Valid value: a string of infinite length. **Note** In the console, the parameter value is displayed in a drop-down list. Therefore, we recommend that you specify a value as short as possible. Required: yes. Whether the parameter can be left empty: no. Default value: none. Case-sensitive: yes. For example, vx.x and Vx.x do not indicate the same version. Character type: letters and digits. **Note** Special characters are not supported. Example: `NSString *appVersion = @"2.3";` |
   | channel    | The identifier of the channel. Channel identifiers are sent to the server to distinguish channels. Data type: string. Valid value: a string of infinite length. Required: yes. Whether the parameter can be left empty: no. Default value: none. Character type: letters and digits. **Note** Special characters are not supported. Example: `NSString *channel = @"appstore";`                                                                                                                                                                                                                                                                                         |
   | nick       | The nickname of the user. Nicknames are sent to the server to distinguish users. You can query data later based on this parameter. Data type: string. Valid value: a string of infinite length. Required: yes. Whether the parameter can be left empty: no. Default value: none. Character type: letters and digits. **Note** Special characters are not supported. Naming conventions: user-defined. Example: `NSString *nick = @"john";`                                                                                                                                                                                                              |

   




**Compile the app** 
----------------------------------------

1. Set the `Allow Non-modular Includes In Framework Modules` parameter to `Yes` in the build settings of the project.

   

2. Perform compilation.

   



**Note**



* If the `duplicate symbol` error is reported during compilation, check whether your local dependencies are included in the dependencies that are managed by CocoaPods. If so, delete the local dependencies.

  

* If you have integrated SDKs of other Alibaba Cloud services, you may fail to compile the app because of a UTDID conflict. For more information about how to resolve this issue, see [How do I resolve a UTDID conflict of SDKs?](https://help.aliyun.com/document_detail/172645.html)

  




**Sample code** 
------------------------------------

For more information about the sample code on how to integrate the performance analysis SDK for iOS, see [Demo project](https://github.com/aliyun/alicloud-ios-demo/tree/master/apm_ios_demo "Demo project").

**Verify the features of the SDK** 
-------------------------------------------------------

After you integrate the SDK for iOS, you must check whether the SDK works as expected. To do so, perform operations on the app and view performance data in the performance analysis console.

1. Start the app. After 2 minutes, log on to the console. Check whether data is displayed on the **Startup Speed** page.

   

2. Switch pages in the app. After 2 minutes, log on to the console. Check whether data is displayed on the **Load Time** page.

   



**Note**

It takes about 2 minutes to upload the collected data to the console.

If data is displayed as expected, the SDK for iOS is properly integrated.

If data is not displayed as expected, one of the following issues may exist: The SDK is not integrated, the data is not collected by the SDK, the data is not sent, or a server issue exists. To resolve this issue, contact Alibaba Cloud technical support. For more information, see [Technical support](/intl.en-US/.md).
