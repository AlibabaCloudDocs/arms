# Monitor other mini programs

This topic describes how to use the browser monitoring function of Application Real-Time Monitoring Service \(ARMS\) to monitor the standards-compliant mini programs, except for DingTalk, Alipay, and WeChat mini programs. It also demonstrates the general configurations, methods, and advanced scenarios.

## Basic usage

To monitor the mini programs, you need to perform at least the three steps: introducing and initialize the npm \(Node Package Manager\) package, reporting logs, and setting security domains.

1.  Introduce and initialize the npm package.

    1.  In your mini program project, introduce the npm package named `alife-logger` to facilitate log reporting.

        ```
        npm install alife-logger
                                    
        ```

    2.  Add the following information to the monitor.js file in the /utils directory to initialize the npm package.

        **Note:** You can specify the name and storage path of the JS file.

        ```
        import MiniProgramLogger from 'alife-logger/miniprogram';
        const Monitor = MiniProgramLogger.init({
            pid: 'xxx',
            uid: 'userxxx', // The ID of the user, which is used to collect the unique visitor (UV) data.
            region: 'cn', // The region where the application is deployed. Set it to cn if the application is deployed in China and to sg if the application is deployed outside China. The default value is cn.
            // You need to specify the remote procedure call (RPC) method to perform browser monitoring of mini programs. Write the implementation method as needed. The following example takes the method of DingTalk E-App as an example.
            sendRequest: (url, resData) => {
                  // This parameter must be configured by the business side. The GET or POST method is supported.
                // demo in dingding
                var method = 'GET';
                var data;
                if (resData) {
                    method = 'POST';
                    data = JSON.stringify(resData);
                }
                dd.httpRequest({
                    url: url,
                    method: method,
                    data: data,
                    fail: function (error) {
                        //...
                    }
                });
            },
             // Manually enter the method to get the path of the current page. Write the implementation method as needed. The following example takes the method of DingTalk E-App as an example.
             getCurrentPage: () => {
                  // This parameter must be configured by the business side.
                if (typeof getCurrentPages ! == 'undefined' && typeof getCurrentPages === 'function') {
                    var pages = (getCurrentPages() || []);
                    var pageLength = pages.length;
                    var currPage = pages[pageLength - 1];
                    return (currPage && currPage.route) || null;
                }
             }
        });
        
        export default Monitor;
                                    
        ```

        **Note:** For more information about parameter configurations, see [Common parameters](#Configuration).

2.  Report logs.

    1.  In app.js, use either of the following two methods to report logs:

        -   Use the **Monitor.hookApp\(options\)** method to automatically capture error logs. The **options** parameter is the app-specific object.

            ```
            import Monitor from '/utils/monitor';
            
                App(Monitor.hookApp({
                  onError(err) {
                    console.log('Trigger onError:', err);
                  },
                  onLaunch() {
                    console.log('Trigger onLaunch');
                  }
            
                  onShow(options) {
                  },
                  onHide() {
                  }
                }));
            
                                                
            ```

        -   Use the **Monitor.error\(err\)** method to manually report error logs.

            ```
            import Monitor from '/utils/monitor';
            
                App({
                  onError(err) {
                      Monitor.error(err);
                    console.log('Trigger onError:', err);
                  },
                  onLaunch() {
                    console.log('Trigger onLaunch');
                  }
            
                  onShow(options) {
                  },
                  onHide() {
                  }
                });
                                                
            ```

    2.  In, page.js, use either of the following two methods to report logs:

        -   Use the **Monitor.hookPage\(options\)** method to automatically report the PV and health data.

            **Note:** Automatic report of API request results is not supported in this method.

            ```
            import Monitor from '/utils/monitor';
            
                Page(Monitor.hookPage({
                   data: {},
                    onLoad(query) {
                    },
                    onReady() {
                        // Page loaded.
                    },
                    onShow() {
            
                    },
                    onLoad(query) {
            
                    },
                    onHide() {
            
                    },
                    onUnload() {
            
                    },
                    onTitleClick() {
                        /**
                         * Collects instrumentation data and performs instrumentation in a custom manner.
                         * @desc
                         */
                        Monitor.sum('titleClick');
                    }       
                }));
                                                
            ```

        -   Call a method to start instrumentation actively.

            **Note:** For more information about the methods, see [Methods](#API)[Methods](#API).

            ```
            import Monitor from './util/monitor';
            
                Page({
                   data: {},
                    onShow() {
                        Monitor.pageShow();
                    },
                    onHide() {
                        Monitor.pageHide();
                    },
                    onUnload() {
                        Monitor.pageHide();
                    },
                    onTitleClick() {
                        /**
                         * Collects instrumentation data and performs instrumentation in a custom manner.
                         * @desc
                         */
                        Monitor.sum('titleClick');
                    }       
                });
                                                
            ```

3.  Set security domains.

    -   If the **region** is set to `cn`, add `https://arms-retcode.aliyuncs.com` to the valid domain of the request.

    -   If the **region** is set to `sg`, add `https://arms-retcode-sg.aliyuncs.com` to the valid domain of the request.


## Common parameters

The following table lists the common parameters that are used for initializing the NPM package.

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|pid|String|The ID of the site.|Yes|null|
|uid|String|The ID of the user, which is used to collect the UV data.|No|Storage setting|
|tag|String|The input tag. Each log carries a tag.|No|None|
|disabled|Boolean|Specifies whether the log reporting function is disabled.|No|false|
|sample|Integer|The log sampling rate. Valid values: 1, 10, and 100. Performance logs and successful API request logs are reported in a 1/number of samples ratio.|No|1|
|disableHook|Boolean|Specifies whether to disable monitoring my.httpRequest. By default, the request is monitored, and the API request success rate is reported.|No|false|
|sendRequest|Function|The method for sending logs. If this parameter is not configured, the logs cannot be sent.|Yes|None|
|getCurrentPage|Function|The method for obtaining the current page.|Yes|None|

**Fields in `sendRequest`**

The sendRequest parameter is used to send logs and must support the GET or POST method. The POST method is used to report error logs. The method parameters are described as follows.

|Parameter|Type|Description|
|---------|----|-----------|
|url|String|The URL to which the log is reported.|
|resData|Object|The content that you want to report in the POST method. When a value is set for this parameter, the log must be reported in the POST method. Otherwise, the log must be reported in the GET method.|

**`sendRequest` configuration example**

```
sendRequest: (url, resData) => {
          // This parameter must be configured by the business side. The GET or POST method is supported.
        // demo in dingding
        var method = 'GET';
        var data;
        if (resData) {
            method = 'POST';
            data = JSON.stringify(resData);
        }
        dd.httpRequest({
            url: url,
            method: method,
            data: data,
            fail: function (error) {
                //...
            }
        });
    }
            
```

## Methods

|Method|Parameter|Remarks|
|------|---------|-------|
|hookApp|\{\}|Enter the source app parameters. The app lifecycle API automatically starts instrumentation.|
|hookPage|\{\}|Enter the source page parameters. The page lifecycle API automatically starts instrumentation.|
|setCommonInfo|\{\[key: string\]: string;\}|Set basic log fields for the scenarios such as phased release.|
|setConfig|\{\[key: string\]: string;\}|Set the config field.|
|pageShow|\{\}|Report the PV data.|
|pageHide|\{\}|Report the health data.|
|error|String/Object|Report error logs.|
|api|See also [t152281.md\#section\_k3o\_jn0\_k38](/intl.en-US/Browser monitoring/API reference.md)|Report the API request logs.|
|sum/avg|String|Report the custom sum and average logs.|

**Note:** If the lifecycle API calls the hookApp or hookPage method for instrumentation in monitoring mini program projects, the projects must conform to the app and page regulations of standard mini programs. In other words, the projects must support **onError** under App, and **onShow**, **onHide**, and **onUnload** under Page. For usage examples, see [Basic usage](#section_j2f_cx2_jhb).

Most log report methods achieve the same purposes as the browser monitoring SDKs. The following section describes how to call other methods:

-   To send the PV data of the current page, call **pageShow\(\)** under **onShow** of Page.

    **Note:** Do not call pageShow\(\) together with **hookPage\(\)**. Otherwise, the PV logs are reported repeatedly.

    ```
    import Monitor from '/util/monitor';
    Page({
        onShow: function() {
            Monitor.pageShow();
        }
    })
                        
    ```

-   To send the health data \(health and browsing time\) of the current page, call **pageHide\(\)** under **onHide** and **onUnload** of Page.

    **Note:** Do not call pageHide\(\) together with **hookPage\(\)**. Otherwise, the logs are reported repeatedly.

    ```
    import Monitor from '/util/monitor';
      Page({
    
          onHide: function() {
              Monitor.pageHide();
          },
          onUnload: function() {
              Monitor.pageHide();
          }
          ... 
      })
                        
    ```


## Advanced scenarios

When the basic usage cannot meet your needs, see the following advanced scenarios.

-   Set the **uid**, which is used to collect the UV data.

    -   If you can obtain the user information before initializing the monitoring SDK, you can directly set the **uid**.

    -   Otherwise, you can obtain the user information before onShow is triggered for the application and then call **setCommonInfo\(\{uid: 'xxx'\}\)** to set the **uid**.

-   Set common information for mini programs.

    Call **setCommonInfo** to set common information for mini programs. ARMS browser monitoring performs statistical analysis of the following fields:

    -   sr: the size of the screen.
    -   vp: the visible section in the browser window.
    -   dpr: the pixel ratio of the screen.
    -   ul: the language of the document.
    -   dr: the reference of the document.
    -   ct: the network connection type, for example, Wi-Fi or 3G.

        **Warning:** Do not call **setCommonInfo** to set too many fields at a time. Otherwise, the request length may exceed the constraints, causing request failures.


## More information

-   [Access overview of browser monitoring](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/Access overview of browser monitoring.md)
-   [Monitor DingTalk mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor DingTalk mini programs.md)
-   [Monitor Alipay mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor Alipay mini programs.md)
-   [Monitor WeChat mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor WeChat mini programs.md)

