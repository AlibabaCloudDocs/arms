# 使用前后端链路追踪诊断API错误原因

在前端监控中，即便已知API的请求耗时，也无从知晓准确的网络传输性能、后端服务的调用链路及性能，因而无法快速准确地排查应用API问题。前后端链路追踪功能可以解决此类问题，它会将API请求从前端发出到后端调用的链路串联起来，真实还原代码执行的完整现场。

您已经开通ARMS前端监控和ARMS应用监控，请参见[开通和升级ARMS](/intl.zh-CN/快速入门/开通和升级ARMS.md)。阿里云ARMS应用监控需要2.4.5或更高版本，关于其配置，请参见[应用监控概述](/intl.zh-CN/应用监控/应用监控概述.md)。

应用监控可提供API在后端的处理性能及调用链路，但这些数据未必能准确反映用户的真实体验。前端监控只能监控到API从发送到返回的整体耗时及状态，无法提供后端服务的调用链路及性能数据。在这种情况下，前后端链路追踪功能可将前端与后端串联起来，给您一站式的问题排查体验。

## 配置ARMS前端监控



1.  确认前端站点和应用之间是否存在对应关系。

2.  不关闭API自动上报，允许API自动上报。

3.  配置enableLinkTrace为`true`，允许前后端链路追踪。具体配置为：

    ```
    <script>
    !(function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxx",imgUrl:"https://arms-retcode.aliyuncs.com/r.png?", enableLinkTrace: true};
    with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
    })(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
    </script>                         
    ```


1.  确认前端站点和应用之间是否存在对应关系。

2.  配置enableLinkTrace和enableApiCors为`true`。

    ```
    <script>
    !(function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxx",imgUrl:"https://arms-retcode.aliyuncs.com/r.png?", 
    enableLinkTrace: true, enableApiCors: true};
    with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
    })(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
    </script>
    ```

    **说明：** 配置enableApiCors为`true`，后端服务也需要支持跨域请求及自定义header值，请确认所有请求都配合联调正常，否则会出现请求失败的问题。Nginx配置参考如下：

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

3.  配置ignore，请参见[ignore](/intl.zh-CN/前端监控/SDK参考.md)。 具体配置为：

    ```
    let whitelist = [‘api.xxx’,’source3’]; // 白名单。
    let blacklist = [‘source2’,’source6’]; // 黑名单。
    // 可根据需求，选择黑白名单（在方法中return true或者false去控制）。
    ignore: {
                ignoreApis: [
                    function(str) {   // 方法。
                        if (whitelist.includes(str)) {
                            return false;
                        }
                        return true; // 返回true则忽略。
                    }]
             }
    ```

    **说明：** ignore类似于黑白名单，可以避免部分第三方资源请求的header值被修改，从而防止资源请求出现错误。


## 工作原理

-   在允许API自动上报的前提下，如果API与当前应用的域名同源，则会在API请求头（Request Header）加入两个自定义Header：EagleEye-TraceID和EagleEye-SessionID。EagleEye-TraceID即串联前后端链路的标识。
-   如果API与当前应用的域名不同源，则不会在请求头添加自定义Header，以保证应用请求可以正常发送。
-   如需验证前后端链路追踪配置是否生效，可以打开控制台查看对应API请求的Request Headers中是否有EagleEye-TraceID和EagleEye-SessionID这两个标识。

    **警告：** EagleEye-TraceID和EagleEye-SessionID的值有相应的含义，请勿自行生成。

    ![operating principle](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3430873061/p43707.png)


## 使用场景和案例

通过调用的时间轴，可以知道是网络传输还是后端调用导致请求耗时时间过长，同时单击后端应用中的线程剖析，可以看到本次请求后端的完整调用链路。从而根据业务定位是什么原因导致API错误：

-   当API返回错误码或者业务逻辑错误时，定位问题操作如下：
    1.  登录[ARMS控制台](https://arms-intl.console.aliyun.com/)。
    2.  在左侧导航栏单击**前端监控**，然后单击目标应用名称。
    3.  在左侧导航栏单击**API请求**。
    4.  在右侧的**API链路追踪（TOP 20）**区域的**API失败列表**中，找到相关的API或者TraceID，并单击右侧的**链路追踪**，以查看前端监控的整体耗时和后端应用的调用时序图。

        ![API failure list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3430873061/p43709.png)

    5.  根据调用的时间轴判断，耗时长的是网络传输还是后端调用。
    6.  对后端应用单击**方法栈**列中的放大镜图标，可以查看本次请求的完整后端调用链，并根据业务定位导致API错误的原因。

        ![ application-Invocation-trace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3430873061/p43710.png)

-   当API耗时较长时，定位问题操作如下：
    1.  登录[ARMS控制台](https://arms-intl.console.aliyun.com/)。
    2.  在左侧导航栏单击**前端监控**，然后单击目标应用名称。
    3.  在左侧导航栏单击**API请求**。
    4.  在右侧的**API链路追踪（TOP20）**区域中，按照请求耗时对API进行降序排列，找到耗时较长的API或者TraceID。
    5.  单击右侧的**链路追踪**链接，以查看前端监控的整体耗时和后端应用的调用时序图。
        -   如果后端应用处理时间较短，而整体耗时较长，则说明API请求从发送到服务端以及从服务端返回数据到浏览器端的网络传输耗时较长。此时可以单击**访问明细**，并在查看详情页面上查看本次访问的网络、地域、浏览器、设备、操作系统等信息。
        -   如果后端应用处理时间较长，则说明后端处理的性能较差。此时可以单击**方法栈**栏中的放大镜图标，并在本地方法栈对话框中查看后端链路上哪部分内容耗时较长，继而定位问题。

