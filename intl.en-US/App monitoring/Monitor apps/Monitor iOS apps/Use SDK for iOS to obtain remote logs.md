# Use SDK for iOS to obtain remote logs

You can use SDK for app monitoring to obtain comprehensive remote logs.

An app monitoring task is created for the app. For more information, see [Create an app monitoring task](/intl.en-US/App monitoring/Create an app monitoring task.md).

This topic applies to Xcode projects that use CocoaPods to manage dependencies. Apps that support iOS 8.0 or later are supported.

**Note:** Logs can be stored on mobile clients for a maximum of seven days.

## Step 1: Add dependencies

Add pod dependencies.

1.  Specify the official CocoaPods repository and the Alibaba Cloud repository.

    ```
    source "https://github.com/CocoaPods/Specs.git"
    source "https://github.com/aliyun/aliyun-specs.git"
    ```

2.  Add the dependencies.

    ```
    pod 'AlicloudTLog', '~> 1.0.0'
    ```

    `~>` indicates a fuzzy match of the SDK version. `~> 1.0.0` indicates that the SDK is of the latest version from 1.0.0 to 1.1.0 \(excluding the 1.1.0 version itself\).

    For more information about SDK versions, visit [Podfile Syntax Reference](https://guides.cocoapods.org/syntax/podfile.html#pod).

3.  Run the `pod update` command.

    **Note:** If the RuntimeError - \[Xcodeproj\] Unknown object version. error is reported when you run the command in Xcode 9, change Project Format to Xcode 8.0-compatible.


## Step 2: Integrate the SDK

Initialize the SDK in the `application:didFinishLaunchingWithOptions:` method of the AppDelegate.m file. Run the following commands to import header files:

```
#import <AlicloudTLog/AlicloudTlogProvider.h>
#import <AlicloudHAUtil/AlicloudHAProvider.h>
```

Sample code:

```
NSString *appVersion = @"x.x"; 
//The app version to be reported. 
NSString *channel = @"xx";     
//The custom channel ID to be reported. 
NSString *nick = @"xx";        
//The custom nickname to be reported.

[[AlicloudTlogProvider alloc] autoInitWithAppVersion:appVersion channel:channel nick:nick];
[AlicloudHAProvider start];
```

## Step 3: Compile the project

If an error is reported during compilation, change Allow Non-modular Includes In Framework Modules to Yes in the Build Setting file of the project.

If a duplicate symbol error occurs, check whether local dependencies and CocoaPods-managed dependencies are duplicate. If the dependencies are duplicate, delete the duplicate local dependencies that are not managed by CocoaPods. We recommend that you use dependencies that are managed by CocoaPods.

## Step 4: Obtain remote logs

Run the following commands to import header files:

```
#import <TRemoteDebugger/TLogBiz.h>
#import <TRemoteDebugger/TLogFactory.h>
```

Sample code:

```
TLogBiz *log = [TLogFactory createTLogForModuleName:@"YourModuleName"];
[log error:@"error message"];
[log warn:@"warn message"];
[log debug:@"debug message"];
[log info:@"info message"];
```

## Verification

After you perform the preceding steps, you can test your app and log on to the [ARMS console](https://arms-intl.console.aliyun.com/#/home) to view the data reports.

