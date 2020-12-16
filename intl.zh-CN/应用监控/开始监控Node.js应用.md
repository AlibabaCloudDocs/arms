# 开始监控Node.js应用

借助ARMS应用监控，您可以对Node.js应用进行应用拓扑、接口调用、异常事务和慢事务监控、SQL分析等。本文介绍了如何通过Egg.js将Node.js应用接入ARMS应用监控。

## 步骤一：获取License key

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)，在左侧导航栏中选择**应用监控** \> **应用列表**。
2.  在应用列表页面顶部选择目标地域，在右上角单击**接入应用**。
3.  在接入应用页面顶部单击License Key右侧的复制图标保存License Key值。

    ![Section LicenseKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9141208061/p45312.png)


## 步骤二：安装插件

1.  执行以下命令安装Pandora的Egg.js插件和ARMS组件。

    ```
    $ npm install @pandorajs/egg-pandora @pandorajs/component-reporter-arms --save
    ```

2.  安装并保存到package.json中后，在app/config/plugin.js中执行以下命令启用Pandora插件。

    ```
    exports.pandora = {
      enable: true,
      package: '@pandorajs/egg-pandora',
    };
    ```


## 步骤三：配置ARMS授权信息

1.  在app/config/config.default.js中配置ARMS的Service name和[步骤一：获取License key](#section_pu1_j5a_lp8)中获取的License key。

    ```
    exports.pandora = {
      components: {
        reporterArms: {
          path: require.resolve('@pandorajs/component-reporter-arms'),
        },
      },
      arms: {
        licenseKey: '<从ARMS控制台获取到的License Key>',
        serviceName: '<应用服务名>',
      },
    };
    ```

2.  配置完成后，即可通过egg的命令行指令`egg-bin dev`或通过脚手架的开发指令`npm run dev`本地启用应用，测试ARMS数据连接正确性。

    ```
    $ npx egg-bin dev
    [egg-ts-helper] create typings/app/controller/index.d.ts (2ms)
    [egg-ts-helper] create typings/config/index.d.ts (12ms)
    [egg-ts-helper] create typings/config/plugin.d.ts (0ms)
    [egg-ts-helper] create typings/app/index.d.ts (0ms)
    2020-09-15 14:50:45,499 INFO 40994 [master] node version v14.9.0
    2020-09-15 14:50:45,500 INFO 40994 [master] egg version 2.28.0
    [Pandora.js] IPC Hub Server started
    [Pandora.js] IPC Hub Client started at PID 40996
    [Pandora.js] Indicator manager published on IPC hub at PID 40996
    Some modules (grpc) were already required when their respective plugin was loaded, some plugins might not work. Make sure the SDK is setup before you require in other modules.
    2020-09-15 14:50:48,546 INFO 40994 [master] agent_worker#1:40996 started (3043ms)
    [Pandora.js] IPC Hub Client started at PID 41046
    [Pandora.js] Indicator manager published on IPC hub at PID 41046
    Some modules (grpc) were already required when their respective plugin was loaded, some plugins might not work. Make sure the SDK is setup before you require in other modules.
    PluginLoader#load: trying to load http@14.9.0
    PluginLoader#load: trying to load https@14.9.0
    2020-09-15 14:50:50,720 INFO 40994 [master] egg started on http://127.0.0.1:7001 (5220ms)
    
    # 现在可以访问http://127.0.0.1:7001使用应用。
    ```


## 结果验证

启动Node.js应用，约15s后，若Node.js应用出现在应用列表中且有数据上报，则说明接入成功。

