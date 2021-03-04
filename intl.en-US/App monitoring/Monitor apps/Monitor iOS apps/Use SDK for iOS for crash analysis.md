# Use SDK for iOS for crash analysis

You can use App Monitoring SDK to obtain complete crash analysis data for mobile terminals, such as crash, abort, crash aggregation, and impact analysis.

-   App Monitoring is accessed. For more information, see [Create an app monitoring task](/intl.en-US/App monitoring/Create an app monitoring task.md).
-   The AppKey and AppSecret of the application are obtained.

    On the **App Monitoring** page, find the app and click **View Configuration** in the Operation column.

    ![View Configuration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8760758061/p74081.png)

    In the dialog box that appears, copy the AppKey and AppSecret.


This topic applies to Xcode projects that use CocoaPods to manage dependencies and apps that support iOS 8.0 or later.

## Step 1: Add dependencies

You can select Pod dependencies or local dependencies:

-   Add Pod dependencies
    1.  Specify the official CocoaPods repository and Alibaba Cloud repository.

        ```
        source "https://github.com/CocoaPods/Specs.git"
        source "https://github.com/aliyun/aliyun-specs.git"
        ```

    2.  Add the dependencies.

        ```
          pod 'AlicloudCrash' , '~> 1.1.0'
        ```

        `~>` indicates a fuzzy match of the SDK version. `~> 1.1.0` indicates that the SDK is of the latest version from 1.1.0 to 1.2.0 \(excluding the 1.2.0 version itself\). For more information about SDK versions, visit [Podfile Syntax Reference](https://guides.cocoapods.org/syntax/podfile.html#pod).

    3.  Run the `pod update` command.

        **Note:** If the RuntimeError - \[Xcodeproj\] Unknown object version. error is prompted when you run the command in Xcode 9, change Project Format to Xcode 8.0-compatible.

-   Add local dependencies
    1.  Click **Download SDK** in the upper-right corner of the **App monitoring** page to download SDK for **Crash Analysis** and **iOS**. Copy all the library files in the downloaded package to the project.
    2.  Import the FRAMEWORK files.
        1.  In Xcode, drag the FRAMEWORK files from the downloaded SDK directory to Target directory. In the dialog box that appears, select **Copy items if needed**. The following FRAMEWORK files are involved:
            -   AlicloudCrash.framework
            -   AliHACore.framework
            -   AliHALogEngine.framework
            -   AliHAProtocol.framework
            -   AlicloudHAUtil.framework
            -   AlicloudUtils.framework
            -   AlicloudUT.framework
            -   CrashReporter.framework
            -   JDYThreadTrace.framework
            -   TBCrashReporter.framework
            -   TBJSONModel.framework
            -   TBRest.framework
            -   UTDID.framework
            -   ZipArchive.framework
        2.  In the **Build Phases** \> **Link Binary With Libraries** directory, add the following public packages:
            -   libc++.tbd
            -   SystemConfiguration.framework

## Step 2: Integrate SDK

In the [ARMS console](https://arms-intl.console.aliyun.com/#/home), Download aliyunmasseses-info.plist and copy it to the root directory of the project. Initialize the SDK in `application:didFinishLaunchingWithOptions:` of the AppDelegate.m file. Run the following commands to import header files:

```
#import <AlicloudCrash/AlicloudCrashProvider.h>
#import <AlicloudHAUtil/AlicloudHAProvider.h>
```

Sample code:

```
    NSString *appVersion = @"x.x"; // The app version, which is reported.
    NSString *channel = @"xx";     // The custom channel ID, which is reported.
    NSString *nick = @"xx";        //The custom nickname, which is reported.

    [[AlicloudCrashProvider alloc] autoInitWithAppVersion:appVersion channel:channel nick:nick]; 
    [AlicloudHAProvider start];
```

## Step 3: Compile

If an error is prompted, change `Allow Non-modular Includes In Framework Modules` to Yes in the Build Setting file of the project.

If an error that contains `duplicate symbol` is prompted, check whether local dependencies and CocoaPods-managed dependencies are duplicate. If yes, delete the duplicate local dependencies that are not managed by CocoaPods. We recommend that you use CocoaPods to manage all dependencies.

## Verification

After you perform the preceding steps, you can test your app and log on to the [ARMS console](https://arms-intl.console.aliyun.com/#/home) to view the data reports.

