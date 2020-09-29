# 接入iOS SDK进行性能分析

借助App监控的SDK，您可以获取完备的移动应用性能分析。

已将应用接入App监控。请参见[快速入门：创建监控任务](/cn.zh-CN/App 监控/快速入门：创建监控任务.md)。

本文档适用于使用cocoaPods管理依赖的Xcode项目，以及支持iOS 8.0或以上版本的App。

## 步骤一：添加依赖

Pod依赖接入：

1.  指定官方仓库和阿里云仓库。

    ```
    source "https://github.com/CocoaPods/Specs.git"
    source "https://github.com/aliyun/aliyun-specs.git"
    ```

2.  添加依赖。

    ```
    pod 'AlicloudAPM', '~> 1.0.0'
    ```

    ~\> 为模糊指定版本号方式，~\> 1.0.0表明版本位于1.0.0 <= version < 1.1.0之间的最新版本SDK，SDK版本请参见[Podfile Syntax Reference](https://guides.cocoapods.org/syntax/podfile.html#pod)。

3.  执行`pod update`。

    **说明：** 如果在Xcode 9上出现报错：RuntimeError - \[Xcodeproj\] Unknown object version.，请将Project Format改成Xcode 8.0-compatible。


## 步骤二：接入服务

在AppDelegate.m文件的`application:didFinishLaunchingWithOptions:`方法中初始化SDK。引入头文件：

```
#import <AlicloudAPM/AlicloudAPMProvider.h>
#import <AlicloudHAUtil/AlicloudHAProvider.h>
```

示例代码：

```
    NSString *appVersion = @"x.x"; //App版本，会上报
    NSString *channel = @"xx";     //渠道标记，自定义，会上报
    NSString *nick = @"xx";        //昵称，自定义，会上报

    [[AlicloudAPMProvider alloc] autoInitWithAppVersion:appVersion channel:channel nick:nick];
    [AlicloudHAProvider start];
```

## 步骤三：编译

如果编译报错，请在项目的build setting里设置Allow Non-modular Includes In Framework Modules为YES。

如果出现包含duplicate symbol的错误，请确认其他本地依赖和CocoaPods管理的依赖是否有重复。如有重复，请删除本地依赖。强烈建议所有依赖都通过CocoaPods管理。

## 结果验证

在完成上述步骤之后，您可以对您的App进行测试，并登录[ARMS控制台](https://arms.console.aliyun.com/#/home)查看数据报表。

