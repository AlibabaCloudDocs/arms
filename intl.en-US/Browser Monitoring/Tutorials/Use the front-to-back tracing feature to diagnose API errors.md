# Use the front-to-back tracing feature to diagnose API errors

In frontend monitoring, you do not know the performance of the network transmission or the trace and performance of backend services even if you know the API response time. Therefore, you cannot immediately troubleshoot API errors in applications. The front-to-back tracing feature can resolve this issue. This feature connects the frontend and backend traces of an API request to reproduce the code execution process.

The frontend monitoring and application monitoring features of Application Real-Time Monitoring Service \(ARMS\) are enabled. For more information, see [Activate and upgrade ARMS](/intl.en-US/Quick Start/Activate and upgrade ARMS.md). The version of application monitoring is 2.4.5 or later. For more information, see [Overview](/intl.en-US/Application Monitoring/Overview.md).

The application monitoring feature provides the backend processing performance and traces of API requests. However, the data does not reflect real user experience. The frontend monitoring feature can monitor the overall response time and statuses of API requests, but cannot provide the traces or performance of backend services. In this case, the front-to-back tracing feature connects the frontend and backend to provide you with a one-stop troubleshooting experience.

## Configure ARMS frontend monitoring



1.  Check whether the frontend connects to the backend.

2.  Do not select the Disable Automatic API Reporting option. Enable the automatic API reporting feature.

3.  Set the enableLinkTrace parameter to `true` to enable the front-to-back tracing feature. The following sample code shows how to enable this feature:

    ```
    <script>
    !(function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxx",imgUrl:"https://arms-retcode.aliyuncs.com/r.png?", enableLinkTrace: true};
    with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
    })(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
    </script>                         
    ```


1.  Check whether the frontend connects to the backend.

2.  Set the enableLinkTrace and enableApiCors parameters to `true`.

    ```
    <script>
    !(function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxx",imgUrl:"https://arms-retcode.aliyuncs.com/r.png?", 
    enableLinkTrace: true, enableApiCors: true};
    with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
    })(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
    </script>
    ```

    **Note:** If the enableApiCors parameter is set to `true`, the backend service must also support cross-origin requests and custom header values. Make sure that all requests can be called in combinations as expected. Otherwise, these requests may fail. The following sample code shows how to configure NGINX:

    ```
    upstream test {
            server 192.168.220.123:9099;
            server 192.168.220.123:58080;
        }
        server {
            listen    5800;
            server_name  192.168.220.123;
            root         /usr/share/nginx/html;
            include /etc/nginx/default.d/*.conf;
            location / {
                proxy_pass http://test;
                proxy_set_header Host $host:$server_port;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Real-PORT $remote_port;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header   EagleEye-TraceID $eagleeye_traceid;
                proxy_set_header   EagleEye-SessionID $eagleEye_sessionid;
                proxy_set_header   EagleEye-pAppName $eagleeye_pappname;
            }
    ```

3.  Configure the Ignore method. For more information, see [ignore](/intl.en-US/Browser Monitoring/SDK reference.md). The following sample code shows how to configure the Ignore method:

    ```
    let whitelist = ['api.xxx','source3']; // Set the whitelist. 
    let blacklist = ['source2','source6']; // Set the blacklist. 
    // You can set a blacklist and a whitelist based on your business requirements. The whitelist and blacklist are controlled by the returned true and false values of the method. 
    ignore: {
                ignoreApis: [
                    function(str) {   // Configure the method. 
                        if (whitelist.includes(str)) {
                            return false;
                        }
                        return true; // Ignore if true is returned. 
                    }]
             }
    ```

    **Note:** The Ignore method is similar to blacklists and whitelists. This method prevents header modifications against unauthorized third-party resource requests and errors of resource requests.


## Principle

-   If automatic API reporting is enabled and the API and the domain name of the application have the same origin, the EagleEye-TraceID and EagleEye-SessionID custom headers are added to the API request headers. EagleEye-TraceID is the identifier of the trace that connects the frontend and backend.
-   If the API and the domain name of the application do not have the same origin, no custom headers are added to the API request headers. This ensures that the application can send requests as expected.
-   To check whether the front-to-back tracing configurations have taken effect, go to the ARMS console and view the API request headers. If the EagleEye-TraceID and EagleEye-SessionID headers are included in the API request headers, the configurations have taken effect.

    **Warning:** The values of the EagleEye-TraceID and EagleEye-SessionID headers are automatically generated. We recommend that you do not manually set the values.

    ![operating principle](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8491758061/p43707.png)


## Scenarios and cases

If a request takes a longer time than expected, you can determine whether the cause is network transmission or backend call process based on the call timeline. You can also click the thread profiling of the backend application to view the complete backend trace of the request. In this case, you can identify the cause of an API error based on the business.

-   Perform the following operations to identify the error cause if the API returns an error code or a business logic error occurs:
    1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
    2.  In the left-side navigation pane, click **Browser Monitoring**. On the Browser Monitoring page, click the name of the application for which you want to diagnose API errors.
    3.  In the left-side navigation pane, choose Application \> **API Request**.
    4.  On the **API Failure List** tab of the **API Link Trace\(TOP20\)** section, find the relevant API or trace ID, and click **Link Trace**. You can then view the overall response time of frontend monitoring and the call sequence chart of the backend application.

        ![API failure list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5700362851/p43709.png)

    5.  Determine whether the network transmission or backend call process takes a longer time based on the call timeline.
    6.  Click the Magnifier icon in the **Method Stack** column of the backend application to view the overall backend trace of the request. You can then identify the cause of the API error based on the business.

        ![ application-Invocation-trace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8092576751/p43710.png)

-   Perform the following operations to identify the error cause if the response time of the API is longer than expected:
    1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
    2.  In the left-side navigation pane, click **Browser Monitoring**. On the Browser Monitoring page, click the name of the application for which you want to diagnose API errors.
    3.  In the left-side navigation pane, choose Application \> **API Request**.
    4.  In the **API Link Trace\(TOP20\)** section, the APIs are sorted in descending order by response time. Find the API or trace ID whose response time is longer than expected.
    5.  Click **Link Trace**. Then, view the overall response time of frontend monitoring and the call sequence chart of the backend application.
        -   If the processing time of the backend application is short but the overall response time is long, the time consumed from API request sending to the server to data returning to the frontend is long. In this case, click **View Details**. On the details page, view the network, region, browser, device, and operating system of the access request.
        -   If the backend application takes a long time to process the access request, the backend processing performance is poor. In this case, click the magnifier icon in the **Method Stack** column. In the Method Stack dialog box, check which part of backend tracing is time-consuming to locate the issue.

