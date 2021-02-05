# Use SDK for iOS for performance analysis

You can use SDK for app monitoring to obtain comprehensive performance analysis results for mobile apps.

An app monitoring task is created for the app. For more information, see [Create an app monitoring task](/intl.en-US/App monitoring/Create an app monitoring task.md).

This topic applies to Xcode projects that use CocoaPods to manage dependencies. Apps that support iOS 8.0 or later are supported.

## Step 1: Add dependencies

Add pod dependencies.

1.  Specify the official CocoaPods repository and the Alibaba Cloud repository.

    ```
    source "https://github.com/CocoaPods/Specs.git"
    source "https://github.com/aliyun/aliyun-specs.git"
    ```

2.  Add the dependencies.

    ```
    pod 'AlicloudAPM', '~> 1.0.0'
    ```

    ~\> indicates a fuzzy match of the SDK version. ~\> 1.0.0 indicates that the SDK is of the latest version from 1.0.0 to 1.1.0 \(excluding the 1.1.0 version itself\). For more information about SDK versions, visit [Podfile Syntax Reference](https://guides.cocoapods.org/syntax/podfile.html#pod).

3.  Run the `pod update` command.

    **Note:** If the RuntimeError - \[Xcodeproj\] Unknown object version. error is reported when you run the command in Xcode 9, change Project Format to Xcode 8.0-compatible.


## Step 2: Integrate the SDK

Initialize the SDK in the `application:didFinishLaunchingWithOptions:` method of the AppDelegate.m file. Run the following commands to import header files:

```
#import <AlicloudAPM/AlicloudAPMProvider.h>
#import <AlicloudHAUtil/AlicloudHAProvider.h>
```

Sample code:

```
    NSString *appVersion = @"x.x"; // The app version, which is reported after the code is executed.
    NSString *channel = @"xx";     // The custom channel ID, which is reported after the code is executed.
    NSString *nick = @"xx";        //The custom nickname, which is reported after the code is executed.

    [[AlicloudAPMProvider alloc] autoInitWithAppVersion:appVersion channel:channel nick:nick];
    [AlicloudHAProvider start];
```

## Step 3: Compile the project

If an error is reported when the project is being compiled, change Allow Non-modular Includes In Framework Modules to Yes in the Build Setting file of the project.

If a duplicate symbol error occurs, check whether local dependencies and CocoaPods-managed dependencies are duplicate. If yes, delete the duplicate local dependencies. We recommend that you use CocoaPods to manage all dependencies.

## Verification

After you perform the preceding steps, you can test your app and log on to the [ARMS console](https://arms-intl.console.aliyun.com/#/home) to view the data reports.

