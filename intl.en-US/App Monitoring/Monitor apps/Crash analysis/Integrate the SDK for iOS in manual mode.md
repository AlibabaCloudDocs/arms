Integrate the SDK for iOS in manual mode 
=============================================================

This topic describes how to integrate the crash analysis SDK for iOS in manual mode.

Prerequisites 
----------------------------------

* The configuration file of the app is downloaded. For more information, see [Create an app monitoring task](/intl.en-US/App Monitoring/Create an app monitoring task.md).

  

* The crash analysis SDK for iOS is downloaded. For more information, see [Quick Start](https://help.aliyun.com/document_detail/169962.html#title-fvd-ozh-524).

  




Limits 
---------------------------

Only apps that run on iOS 8.0 and later are supported.

Procedure 
------------------------------

1. **Integrate the SDK.** 

   1. In Xcode, drag the FRAMEWORK files from the directory that stores the downloaded SDK files to the Target directory. In the dialog box that appears, select `Copy items if needed`.

      
   
   2. Choose **Build Phases \> Link Binary With Libraries** and add the following public packages of Xcode:

      * libc++.tbd

        
      
      * SystemConfiguration.framework

        
      

      
   

   

2. **Integrate the service.** 

   1. Copy the configuration file `AliyunEmasServices-Info.plist` of the app to the root directory of the project.

      
   
   2. Add the code for initializing the SDK to the `application:didFinishLaunchingWithOptions` method in the `AppDelegate.m` file.

      Add the following code for importing header files:

          #import <AlicloudCrash/AlicloudCrashProvider.h>
          #import <AlicloudHAUtil/AlicloudHAProvider.h>

      

      Add the following code segment:

          NSString *appVersion = @"x.x"; // The version number of the app, which is reported.
          NSString *channel = @"xx";     // The custom identifier of the channel, which is reported.
          NSString *nick = @"xx";        // The custom nickname of the user, which is reported.
          [[AlicloudCrashProvider alloc] autoInitWithAppVersion:appVersion channel:channel nick:nick];
          [AlicloudHAProvider start];

      

      The following table describes the parameters.
      

      | Parameter  |                                                                                                                                                                                                                                                                                                                                                                  Description                                                                                                                                                                                                                                                                                                                                                                  |
      |------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
      | appVersion | The version number of the app. Version numbers are sent to the server to distinguish versions. Data type: string. Format: user-defined. Valid value: a string of infinite length. **Note** In the console, the parameter value is displayed in a drop-down list. Therefore, we recommend that you specify a value as short as possible. Required: yes. Whether the parameter can be left empty: no. Default value: none. Case-sensitive: yes. For example, vx.x and Vx.x do not indicate the same version. Character type: letters and digits. **Note** Special characters are not supported. |
      | channel    | The identifier of the channel. Channel identifiers are sent to the server to distinguish channels. Data type: string. Valid value: a string of infinite length. Required: yes. Whether the parameter can be left empty: no. Default value: none. Character type: letters and digits. **Note** Special characters are not supported.                                                                                                                                                                                                                                                                                           |
      | nick       | The nickname of the user. Nicknames are sent to the server to distinguish users. You can query data later based on this parameter. Data type: string. Valid value: a string of infinite length. Required: yes. Whether the parameter can be left empty: no. Default value: none. Character type: letters and digits. **Note** Special characters are not supported. Naming conventions: user-defined.                                                                                                                                                                                                                         |

      
   

   

3. **Add advanced settings.** 

   The SDK for iOS provides methods that allow you to report custom information or errors.

       // Report custom information.
       [AlicloudCrashProvider configCustomInfoWithKey:@"key" value:@"value"];   // Configuration item: the custom environment information (configCustomInfoWithKey and value).
       
       // Report custom information based on the exception type.
       [AlicloudCrashProvider setCrashCallBack:^NSDictionary * _Nonnull(NSString * _Nonnull type) {
           return @{@"key":@"value"};   // Configuration item: the exception information (key and value).
       }];
       
       // Report a custom error.
       NSError *error = [NSError errorWithDomain:@"customError" code:10001 userInfo:@{@"errorInfoKey":@"errorInfoValue"}];
       [AlicloudCrashProvider reportCustomError:error];   // Configuration item: the custom error information (errorWithDomain, code, and userInfo).

   

   For more information, see [Reference of the SDK for iOS]().
   

4. **Compile the app.** 

   1. Set the `Allow Non-modular Includes In Framework Modules` parameter to `Yes` in the build settings of the project.

      
   
   2. Perform compilation.

      **Note**

      
      * If the `duplicate symbol` error is reported during compilation, check whether your local dependencies are included in the dependencies that are managed by CocoaPods. If so, delete the local dependencies.

        
      
      * If you have integrated SDKs of other Alibaba Cloud services, you may fail to compile the app because of a UTDID conflict. For more information about how to resolve this issue, see [How do I resolve a UTDID conflict of SDKs?](https://help.aliyun.com/document_detail/172616.html)

        
      

      
      
   

   

5. **Verify the features of the SDK.** 

   After you integrate the SDK for iOS, you must check whether the SDK works as expected.
   1. Write and run test code to simulate or trigger an app crash on a mobile terminal. Example:

          NSMutableArray *array = @[];
          [array addObject:nil];

      
      **Note**

      For more information, see the Sample code section.
      
   
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

For more information about the sample code on how to integrate the crash analysis SDK for iOS, visit [Demo project](https://github.com/aliyun/alicloud-android-demo/tree/master/ha_android_demo?spm=a2c4g.11186623.2.27.789073c8I6rfk5).
