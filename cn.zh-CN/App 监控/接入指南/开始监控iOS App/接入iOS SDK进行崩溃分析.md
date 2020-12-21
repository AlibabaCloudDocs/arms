# 接入iOS SDK进行崩溃分析

借助App监控的SDK，您可以获取完备的移动端崩溃分析监控，具体包括Crash监控、Abort监控、崩溃问题聚合、影响面分析等。

-   已将应用接入App监控。请参见[快速入门：创建监控任务](/cn.zh-CN/App 监控/快速入门：创建监控任务.md)。
-   获取应用的AppKey和AppSecret。

    在**App监控**页面中单击目标应用所在行最右侧的**查看配置**。

    ![查看app配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3567063951/p74081.png)

    在弹出的对话框中复制AppKey和AppSecret。

    ![添加APP监控](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4567063951/p111714.png)


本文档适用于使用cocoaPods管理依赖的Xcode项目，以及支持iOS 8.0或以上版本的App。

## 步骤一：添加依赖

您可以选择Pod依赖接入和本地依赖接入两种方式：

-   Pod依赖接入
    1.  指定官方仓库和阿里云仓库。

        ```
        source "https://github.com/CocoaPods/Specs.git"
        source "https://github.com/aliyun/aliyun-specs.git"
        ```

    2.  添加依赖。

        ```
          pod 'AlicloudCrash' , '~> 1.1.0'
        ```

        `~>`为模糊指定版本号方式，`~> 1.1.0`表明引用位于1.1.0 <= version < 1.2.0之间的最新版本SDK，请参见[Podfile Syntax Reference](https://guides.cocoapods.org/syntax/podfile.html#pod)。

    3.  执行`pod update`。

        **说明：** 如果在Xcode 9上出现报错：RuntimeError - \[Xcodeproj\] Unknown object version.，请将Project Format改成Xcode 8.0-compatible。

-   本地依赖接入
    1.  单击**App监控**页面右上角的**SDK下载**，下载**崩溃分析**、**iOS版**对应的SDK，并复制下载包内所有库文件放在项目工程中。
    2.  引入Framework。
        1.  在Xcode中，把下载的SDK目录中的framework拖入对应Target下，在弹出的对话框中勾选**Copy items if needed**。framework如下：
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
        2.  在**Build Phases** \> **Link Binary With Libraries**中，添加以下公共包：
            -   libc++.tbd
            -   SystemConfiguration.framework

## 步骤二：接入服务

在[ARMS控制台](https://arms.console.aliyun.com/#/home)下载AliyunEmasServices-Info.plist并复制至项目根目录。在AppDelegate.m文件的`application:didFinishLaunchingWithOptions:`方法中初始化SDK。引入头文件：

```
#import <AlicloudCrash/AlicloudCrashProvider.h>
#import <AlicloudHAUtil/AlicloudHAProvider.h>
```

示例代码：

```
    NSString *appVersion = @"x.x"; //App版本，会上报
    NSString *channel = @"xx";     //渠道标记，自定义，会上报
    NSString *nick = @"xx";        //昵称，自定义，会上报

    [[AlicloudCrashProvider alloc] autoInitWithAppVersion:appVersion channel:channel nick:nick]; 
    [AlicloudHAProvider start];
```

## 步骤三：编译

如果编译报错，请在项目的build setting里设置`Allow Non-modular Includes In Framework Modules`为YES。

如果出现包含`duplicate symbol`的错误，请确认其他本地依赖和CocoaPods管理的依赖是否有重复。如有重复，请删除本地依赖。强烈建议所有依赖都通过CocoaPods管理。

## 结果验证

在完成上述步骤之后，您可以对您的App进行测试，并登录[ARMS控制台](https://arms.console.aliyun.com/#/home)查看数据报表。

