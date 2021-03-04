# Use Zipkin to perform tracing analysis on NGINX

NGINX is a free, open source, and high-performance server that serves as an HTTP server and reverse proxy. You can perform tracing analysis on NGINX to better understand the running status of your application services. This topic shows you how to perform tracing analysis on NGINX.

## Overview

If a slow response occurs in a microservice that uses NGINX as a proxy, you cannot estimate the impact of the slow response because no data is collected. In this case, you can use Tracing Analysis to trace NGINX requests for the microservice and calculate the number of page views that are affected by slow responses.

## Preparations

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **Cluster Configurations**.

3.  On the Cluster Configurations page, click the **Access point information** tab. Then, turn on **Show Token** for the Cluster Information parameter.

4.  Set the Client parameter to **Zipkin**.

5.  In the Related Information column of the table in the lower part, click the copy icon next to the endpoint that you want to use.

    ![Endpoint: Zipkin](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8324484161/p188458.png)

    **Note:** If you deploy your application in an Alibaba Cloud production environment, select a private endpoint. Otherwise, select a public endpoint.


## Procedure

1.  Pull an image from the registry.

    ```
    sudo docker pull registry.cn-hangzhou.aliyuncs.com/public-community/nginx-zipkin:0.1
    ```

2.  Run NGINX in a Docker container.

    ```
    docker run --rm  -p 80:80 -e "COLLECTOR_HOST=${ZIPKIN_ENDPOINT}?" -d registry.cn-hangzhou.aliyuncs.com/public-community/nginx-zipkin:0.1
    ```

    Set the `${ZIPKIN_ENDPOINT}` variable to the version 1 endpoint of Zipkin that you copy in [Preparations](#section_hst_9gl_yew), but remove "http://" and suffix the value with a question mark \(?\).

    Example:

    ```
    docker run --rm  -p 80:80 -e "COLLECTOR_HOST=tracing-analysis-dc-hz.aliyuncs.com/adapt_******_******/api/v1/spans?" -d registry.cn-hangzhou.aliyuncs.com/public-community/nginx-zipkin:0.1
    ```

3.  Visit NGINX in a browser.

    Enter localhost/nginx.conf or curl "localhost/nginx.conf" in the address bar of a browser to visit NGINX.

4.  View the trace data of NGINX.

    Log on to the [Tracing Analysis console](https://tracing-sg.console.aliyun.com/) to view the trace data of the nginx-jaeger application.


## Deploy and trace NGINX in a Docker container

1.  Download, build, and then deploy a Dockerfile.

    ```
    wget https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/nginx-zipkin-docker.tgz
    tar -xzvf nginx-zipkin-docker.tgz
    cd nginx-zipkin
    // Build the Dockerfile.
    docker build --rm --tag nginx-jaeger:0.1 .
    ```

2.  Run Docker.

    ```
    docker run --rm  -p 80:80 -e "COLLECTOR_HOST=${ZIPKIN_ENDPOINT}?" -d nginx-zipkin:0.1
    ```

    Set the `${ZIPKIN_ENDPOINT}` variable to the version 1 endpoint of Zipkin that you copy in [Preparations](#section_hst_9gl_yew), but remove "http://" and suffix the value with a question mark \(?\).

    Example:

    ```
    docker run --rm  -p 80:80 -e "COLLECTOR_HOST=tracing-analysis-dc-hz.aliyuncs.com/adapt_123@abc_456@efg/api/v1/spans?" -d nginx-zipkin:0.1
    ```


## Deploy and trace NGINX on an ECS instance

1.  Use Zipkin to perform tracing analysis.

    1.  Download Zipkin to a working directory.

        ```
        wget  https://github.com/rnburn/zipkin-cpp-opentracing/releases/download/v0.5.2/linux-amd64-libzipkin_opentracing_plugin.so.gz
        gunzip linux-amd64-libzipkin_opentracing_plugin.so.gz
        sudo cp linux-amd64-libzipkin_opentracing_plugin.so /usr/local/lib/libzipkin_opentracing_plugin.so 
        ```

    2.  Configure the /usr/local/nginx/conf/nginx.conf file.

        ```
        load_module modules/ngx_http_opentracing_module.so;
        
        events {}
        
        http {
          opentracing on;
        
          opentracing_load_tracer /usr/local/lib/libzipkin_opentracing.so /etc/zipkin-config.json;
          
          server {
            error_log /var/log/nginx/debug.log debug;
            listen 80;
        
            location  ~ {
              opentracing_operation_name $uri;
              opentracing_trace_locations off;
              # Navigate to the proxy service. Set this parameter to a proper value as required.
              proxy_pass http://127.0.0.1:8081;
              opentracing_propagate_context;
            }
          }
        }
        ```

        **Note:** For more information, see the configuration in [opentracing-contrib](https://github.com/opentracing-contrib/nginx-opentracing/blob/ea9994d7135be5ad2e3009d0f270e063b1fb3b21/doc/Reference.md).

    3.  Set the Zipkin parameters in the /etc/zipkin-config.json file.

        ```
        {
          "service_name": "nginx",
          "collector_host": "zipkin"
        }
        ```

        If you use the Zipkin service that is managed by Alibaba Cloud, set the collector\_host parameter to the endpoint of Zipkin.

        **Note:** Enter the version 1 endpoint of Zipkin that you copy in [Preparations](#section_hst_9gl_yew), but remove "http://" and suffix the value with a question mark \(?\).

        ```
        "collector_host": "tracing-analysis-dc-hz.aliyuncs.com/adapt_abc123@abc456_abc123@abc356/api/v1/spans?"
        ```

    4.  Set the sample\_rate parameter to specify the sampling rate.

        ```
        // Set the sampling rate to 10%.
        "sample_rate":0.1
        ```

    5.  Run NGINX and request the NGINX service.

        ```
        sudo /usr/local/nginx/sbin/nginx
        curl "http://localhost"
        ```


## View the results

Wait for a moment. Then, log on to the Tracing Analysis console. If monitoring data appears, the tracing is successful. If you have questions about how to monitor NGINX, contact the DingTalk account osfriend.

[nginx-opentracing project](https://github.com/opentracing-contrib/nginx-opentracing)

[jaeger-client-cpp project](https://github.com/jaegertracing/jaeger-client-cpp)

[zipkin-cpp-opentracing](https://github.com/rnburn/zipkin-cpp-opentracing)

[Example of using Jaeger to perform tracing analysis on NGINX](https://github.com/opentracing-contrib/nginx-opentracing/tree/master/example/trivial/jaeger)

[Example of using Zipkin to perform tracing analysis on NGINX](https://github.com/opentracing-contrib/nginx-opentracing/tree/master/example/trivial/zipkin)

