# Monitor other mini programs

This topic describes how to use the browser monitoring feature of Application Real-Time Monitoring Service \(ARMS\) to monitor the standards-compliant mini programs, excluding DingTalk, Alipay, and WeChat mini programs. This topic also describes the related general configurations, API methods, and advanced scenarios.

## Basic usage

To monitor mini programs, you must perform the following operations to introduce and initialize the npm package, report logs, and configure security domain names.

1.  Introduce and initialize the npm package.

    1.  In your mini program project, introduce the npm package named `alife-logger` to facilitate log reporting.

        ```
        npm install alife-logger
        ```

    2.  Add the following information to the monitor.js file in the /utils directory to initialize the package.

        **Note:** You can specify the name and storage path of the JavaScript \(JS\) file.

        ```
        import MiniProgramLogger from 'alife-logger/miniprogram';
        const Monitor = MiniProgramLogger.init({
            pid: 'xxx',
            uid: 'userxxx', // The ID of the user, which is used to collect the unique visitor (UV) data.
            region: 'cn', // The region where the application is deployed. Set region to cn if the application is deployed in China and set region to sg if the application is deployed outside China. The default value is cn.
            // You must specify the remote procedure call (RPC) method to perform browser monitoring of mini programs. Write the implementation method. The method of DingTalk E-App is used in the following example.
            sendRequest: (url, resData) => {
                  // The following snippet must be configured by the business side. The GET or POST method is supported.
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
             // Manually enter the method to obtain the path of the current page. Write the implementation method. The method of DingTalk E-App is used in the following example.
             getCurrentPage: () => {
                  // The following snippet must be configured by the business side.
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

        **Note:** For more information about parameter configurations, see [Common SDK parameters](#section_vo9_hoe_9w4).

2.  Report logs.

    1.  In app.js, use one of the following methods to report logs:

        -   Use the **Monitor.hookApp\(options\)** method to automatically capture error logs. The **options** parameter is an app-specific object.

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

    2.  In page.js, use one of the following methods to report logs:

        -   Use the **Monitor.hookPage\(options\)** method to automatically report the page view \(PV\) and health data.

            **Note:** This method does not support automatic report of API requests.

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

        -   Call an API method to actively perform instrumentation.

            **Note:** For more information about API methods, see [API methods](#API).

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

3.  Configure security domain names.

    -   If **region** is set to `cn`, add `https://arms-retcode.aliyuncs.com` to the valid domain name.

    -   If **region** is set to `sg`, add `https://arms-retcode-sg.aliyuncs.com` to the valid domain name.


## API methods

|Method|Parameter|Remarks|
|------|---------|-------|
|hookApp|\{\}|Enter the source app parameters. This method is used to automatically perform instrumentation during the lifecycle of the app.|
|hookPage|\{\}|Enter the source page parameters. This method is used to automatically perform instrumentation during the lifecycle of the page.|
|setCommonInfo|\{\[key: string\]: string;\}|Set basic log fields for scenarios such as phased release.|
|setConfig|\{\[key: string\]: string;\}| |
|pageShow|\{\}|Report the PV data.|
|pageHide|\{\}|Report the health data.|
|error|String/Object|Report error logs.|
|api|For more information, see [API reference](/intl.en-US/Browser monitoring/Methods user guide.md).|Report the API request logs.|
|sum/avg|String|Report the custom sum and average logs.|

**Note:** If you want to call the hookApp or hookPage method for instrumentation in mini program monitoring projects, the projects must conform to the app and page regulations of standard mini programs. The projects must support **onError** for apps, and **onShow**, **onHide**, and **onUnload** for pages. For examples of the method, see [Basic usage](#section_j2f_cx2_jhb).

Most log reporting methods serve the same purposes as the browser monitoring SDKs. The following section describes how to call other methods:

-   To send the PV data of the current page, call **pageShow\(\)** under **onShow** of pages.

    **Note:** Do not call pageShow\(\) together with **hookPage\(\)**. Otherwise, the PV logs are reported repeatedly.

    ```
    import Monitor from '/util/monitor';
    Page({
        onShow: function() {
            Monitor.pageShow();
        }
    })
    ```

-   To send the health data such as health level and time on page, call **pageHide\(\)** under **onHide** and **onUnload** of pages.

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

If the basic usage cannot meet your requirements, refer to the following advanced scenarios:

-   Set **uid** to collect the UV data.

    -   If you can obtain the user information before the monitoring SDK is initialized, you can set **uid**.

    -   If you cannot obtain the user information before the monitoring SDK is initialized, you can obtain the user information before onShow is triggered for the application, and then call **setCommonInfo\(\{uid: 'xxx'\}\)** to set **uid**.

-   Configure common information for mini programs.

    Call **setCommonInfo** to conigure common information for mini programs. ARMS browser monitoring performs statistical analysis on the following parameters:

    -   sr: the size of the screen
    -   vp: the visible section in the browser window
    -   dpr: the pixel ratio of the screen
    -   ul: the language of the document
    -   dr: the reference of the document
    -   ct: the network connection type, such as Wi-Fi or 3G

        **Warning:** Do not call **setCommonInfo** to configure excess parameters at a time. Otherwise, the request length may exceed the constraints and request failures occur.


## Common SDK parameters

ARMS browser monitoring provides a series of SDK parameters. You can configure the parameters to meet additional requirements. The following table describes the common parameters suitable for the scenarios described in this topic. |
| |
| |
| |
| |

ARMS browser monitoring also provides other SDK parameters. For more information, see [SDK reference](/intl.en-US/Browser monitoring/Configuration items of the browser monitoring SDK.md).

**Related topics**  


[Access overview of browser monitoring](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/Access overview of browser monitoring.md)

[Monitor DingTalk mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor DingTalk mini programs.md)

[Monitor WeChat mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor WeChat mini programs.md)

[Monitor Alipay mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor Alipay mini programs.md)

