# Monitor Node.js applications

You can use Application Real-Time Monitoring Service \(ARMS\) to monitor the topology, API requests, abnormal transactions, slow transactions, and slow SQL queries of Node.js applications. This topic describes how to connect Node.js applications to ARMS by using the Egg.js plug-in.

## Step 1: Obtain the License Key

1.  Log on to the[ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
2.  On the Applications page, select the destination region in the top navigation bar, and click **Add Application** in the upper-right corner.
3.  At the top of the Add Application page, click the copy icon to the right of the License Key and save the Key.

    ![Section LicenseKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6076728061/p45312.png)


## Step 2: Install the plug-in

1.  Run the following command to install the Egg.js plug-in and ARMS components of Pandora:

    ```
    $ npm install @pandorajs/egg-pandora @pandorajs/component-reporter-arms --save
    ```

2.  After you install the plug-in and save the settings in the package.json file, run the following command in the app/config/plugin.js directory to enable the plug-in:

    ```
    exports.pandora = {
      enable: true,
      package: '@pandorajs/egg-pandora',
    };
    ```


## Step 3: Specify ARMS authorization information

1.  Go to the app/config/config.default.js file, and specify the service name of ARMS and the License Key that is obtained in [Step 1: Obtain the License Key](#section_pu1_j5a_lp8).

    ```
    exports.pandora = {
      components: {
        reporterArms: {
          path: require.resolve('@pandorajs/component-reporter-arms'),
        },
      },
      arms: {
        licenseKey: '<The License Key that is obtained from the ARMS console>',
        serviceName: '<The service name>',
      },
    };
    ```

2.  Run the `egg-bin dev` command or the `npm run dev` command to start the application on premises and check whether the connection to ARMS is valid.

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
    
    # You can visit http://127.0.0.1:7001 to use the application.
    ```


## Verify the result

Start the Node.js application and wait about 15 seconds. If the application is displayed in the application list and data is imported, the application is connected to ARMS.

