# Use the front-to-back tracing feature to diagnose causes of API errors

In browser monitoring, you do not know the performance of the network transmission or the trace and performance of backend services even if you know the API response time. Therefore, you cannot immediately troubleshoot API errors in applications. The front-to-back tracing feature can resolve this issue. This feature connects the frontend and backend traces of an API request to reproduce the code execution process.

The browser monitoring and application monitoring features of Application Real-Time Monitoring Service \(ARMS\) are activated. For more information, see [Activate and upgrade ARMS](/intl.en-US/Quick start/Activate and upgrade ARMS.md). The version of application monitoring is 2.4.5 or later. For more information, see [Overview](/intl.en-US/Application monitoring/Overview.md).

Application monitoring provides the backend processing performance and traces of API requests. However, the data does not reflect real user experience. Browser monitoring can monitor only the overall response time and statuses of API requests, but cannot provide the traces or performance of backend services. In this case, the front-to-back tracing feature connects the frontend and backend to provide you with a one-stop troubleshooting experience.

## Configure ARMS browser monitoring

The API and the domain name of the application have the same origin.

1.  Check whether the frontend connects to the backend.

2.  Do not select the Disable Automatic API Reporting option. Enable the automatic API reporting.

3.  Set enableLinkTrace to `true` to enable the front-to-back tracing feature. The following sample code shows how to enable the front-to-back tracing feature:

    ```
    <script>
    !( function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxx",imgUrl:"https://arms-retcode.aliyuncs.com/r.png?", enableLinkTrace: true};
    with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
    })(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
    </script>                         
    ```


The API and the domain name of the application do not have the same origin.

1.  Check whether the frontend connects to the backend.

2.  Set enableLinkTrace and enableApiCors to `true`.

    ```
    <script>
    !( function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxx",imgUrl:"https://arms-retcode.aliyuncs.com/r.png?", 
    enableLinkTrace: true, enableApiCors: true};
    with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
    })(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
    </script>
    ```

    **Note:** If enableApiCors is set to `true`, the backend service must also support cross-domain requests and custom header values. Make sure that all requests can be called in combinations as expected. Otherwise, these requests may fail. The following sample code shows how to configure NGINX:

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

3.  Configure the Ignore method. For more information, see [.](/intl.en-US/Browser monitoring/Configuration items of the browser monitoring SDK.md) The following sample code shows how to configure the Ignore method:

    ```
    let whitelist = ['api.xxx','source3']; // The whitelist.
    let blacklist = ['source2','source6']; // The blacklist.
    // You can select a blacklist and whitelist based on your business requirements. The whitelist and blacklist are controlled by the returned true and false values of the method.
    ignore: {
                ignoreApis: [
                    function(str) {   // The method.
                        if (whitelist.includes(str)) {
                            return false;
                        }
                        return true; // Ignore if true is returned.
                    }]
             }
    ```

    **Note:** The Ignore method is similar to blacklists and whitelists. This method prevents header modifications against unauthorized third-party resource requests and errors of resource requests.


Principle

-   If automatic API reporting is enabled and the API and the domain name of the application have the same origin, the EagleEye-TraceID and EagleEye-SessionID custom headers are added to the API request headers. EagleEye-TraceID is the identifier of the trace that connects the frontend and backend.
-   If the API and the domain name of the application do not have the same origin, no custom headers are added to the API request headers. This ensures that the application can send requests as expected.
-   To check whether the front-to-back tracing configurations have taken effect, go to the console and view the API request headers. If the EagleEye-TraceID and EagleEye-SessionID headers are included in the API request headers, the configurations have taken effect.

    **Warning:** The values of EagleEye-TraceID and EagleEye-SessionID are automatically generated. We recommend that you do not manually set the values.

    ![operating principle](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8491758061/p43707.png)


## Scenarios and cases

If a request takes a longer time than expected, you can determine whether the cause is network transmission or backend call process based on the call timeline. You can also click thread profiling of the backend application to view the complete backend trace of the request. In this case, you can identify the cause of an API error based on the business.

-   Locate the error if the API returns an error code or a business logic error occurs.

    1.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the application. In the left-side navigation pane, click **API Request**.
    2.  On the **API Failure List** tab of the **API Link Trace\(Top20\)** section, find the API or trace ID, and click **Link Trace**. You can then view the overall response time of browser monitoring and the call sequence chart of the backend application.

        ![API failure list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5700362851/p43709.png)

    3.  Determine whether the network transmission or backend call process takes a longer time based on the call timeline.

    4.  Click the Magnifier icon in the **Method Stack** column of the backend application to view the overall backend trace of the request. You can then locate the cause of the API error based on the business.

        ![ application-Invocation-trace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8092576751/p43710.png)

-   Locate the error if the response time of the API is longer than expected.

    1.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the application. In the left-side navigation pane, click **API Request**.
    2.  In the **API Link Trace\(Top20\)** section, the APIs are sorted in descending order by response time. or trace ID. You can find the API or trace ID whose response time is longer than expected,

    3.  and click **Link Trace**. You can then view the overall response time of browser monitoring and the call sequence chart of the backend application.

        -   If the processing time of the backend application is short but the overall response time is long, the network transmission takes a longer time. Click **View Details**. On the details page, view the network, region, browser, device, and operating system of the access request.
        -   If the backend application takes a long time to process the access request, the backend processing performance is poor. Click the Magnifier icon in the **Method Stack** column. In the dialog box that appears, check which part of backend tracing is time-consuming to locate the problem.

