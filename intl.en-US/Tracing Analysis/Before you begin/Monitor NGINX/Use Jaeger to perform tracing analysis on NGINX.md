# Use Jaeger to perform tracing analysis on NGINX

NGINX is a free, open source, and high-performance server that serves as an HTTP server and reverse proxy. You can perform tracing analysis on NGINX to better understand the running status of your application services. This topic shows you how to perform tracing analysis on NGINX.

## Overview

If a slow response occurs in a microservice that uses NGINX as a proxy, you cannot estimate the impact of the slow response because no data is collected. In this case, you can use Tracing Analysis to trace NGINX requests for the microservice and calculate the number of page views that are affected by slow responses.

## Preparations

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **Cluster Configurations**.

3.  On the Cluster Configurations page, click the **Access point information** tab. Then, turn on **Show Token** for the Cluster Information parameter.

4.  Set the Client parameter to **Jaeger**.

5.  In the Related Information column of the table in the lower part, click the copy icon next to the endpoint that you want to use.

    ![Endpoints of Tracing Analysis](../images/p188451.png)

    **Note:** If you deploy your application in an Alibaba Cloud production environment, select a private endpoint. Otherwise, select a public endpoint.


## Procedure

1.  Pull an image from the registry.

    ```
    docker pull registry.cn-hangzhou.aliyuncs.com/public-community/jaeger-nginx:0.1
    ```

2.  Run NGINX in a Docker container.

    ```
    docker run --rm  -p 80:80 -e "GRPC_HOST=${GRPC_HOST}" -e "GRPC_AUTH=${GRPC_AUTH}" -d registry.cn-hangzhou.aliyuncs.com/public-community/jaeger-nginx:0.1
    ```

    Set the `${GRPC_HOST}` and `${GRPC_AUTH}` variables to the values that are specified in the endpoint that you copy in [Preparations](#section_bq8_6au_kwl).

    Example:

    ```
    docker run --rm  -p 80:80 -e "GRPC_HOST=tracing-analysis-dc-hz.aliyuncs.com:1883" -e "GRPC_AUTH=123abc@123abc_789abc@456abc}" -d jaeger-nginx:0.1
    ```

3.  Visit NGINX in a browser.

    Enter localhost/nginx.conf or curl "localhost/nginx.conf" in the address bar of a browser to visit NGINX.

4.  View the trace data of NGINX.

    Log on to the [Tracing Analysis console](https://tracing-sg.console.aliyun.com/) to view the trace data of the nginx-jaeger application.


## Deploy and trace NGINX in a Docker container

1.  Download, build, and then deploy a Dockerfile.

    ```
    wget https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/nginx-jaeger-docker.tgz
    tar -xzvf nginx-jaeger-docker.tgz
    cd nginx-jaeger
    // Build the Dockerfile.
    docker build --rm --tag nginx-jaeger:0.1 .
    ```

2.  Run Docker.

    ```
    docker run --rm  -p 80:80 -e "GRPC_HOST=${GRPC_HOST}" -e "GRPC_AUTH=${DRPC_AUTH}" -d jaeger-nginx:0.1
    ```

    Set the `${GRPC_HOST}` and `${GRPC_AUTH}` variables to the values that are specified in the endpoint that you copy in [Preparations](#section_bq8_6au_kwl).

    Example:

    ```
    docker run --rm  -p 80:80 -e "GRPC_HOST=tracing-analysis-dc-hz.aliyuncs.com:1883" -e "GRPC_AUTH=123abc@123abc_789abc@456abc}" -d jaeger-nginx:0.1
    ```


## Deploy and trace NGINX on an ECS instance

1.  Install NGINX.

    1.  Download the NGINX source code package and decompress it.

        ```
        wget http://nginx.org/download/nginx-1.14.2.tar.gz
        tar -xzvf nginx-1.14.2.tar.gz
        ```

    2.  Compile the NGINX source code.

        ```
        cd nginx-1.14.2
        ./configure --with-compat
        make
        sudo make install
        ```

2.  Install OpenTracing.

    1.  Download the OpenTracing package and decompress it.

        ```
        wget https://github.com/opentracing-contrib/nginx-opentracing/releases/download/v0.7.0/linux-amd64-nginx-1.14.0-ngx_http_module.so.tgz
        tar -xzvf linux-amd64-nginx-1.14.0-ngx_http_module.so.tgz
        ```

    2.  Copy the .so file to the modules folder of NGINX. If the folder does not exist, create one.

        ```
        sudo mkdir /usr/local/nginx/modules
        sudo cp ngx_http_opentracing_module.so /usr/local/nginx/modules/ngx_http_opentracing_module.so
        ```

3.  Use Jaeger to perform tracing analysis.

    1.  Download Jaeger to a working directory.

        ```
        wget https://github.com/jaegertracing/jaeger-client-cpp/releases/download/v0.4.2/libjaegertracing_plugin.linux_amd64.so
        sudo cp libjaegertracing_plugin.linux_amd64_042.so /usr/local/lib/libjaegertracing.so
        ```

    2.  Configure the /usr/local/nginx/conf/nginx.conf file.

        ```
        load_module modules/ngx_http_opentracing_module.so;
        
        events {}
        
        http {
          opentracing on;
        
          opentracing_load_tracer /usr/local/lib/libjaegertracing_plugin.so /etc/jaeger-config.json;
        
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

    3.  Set the Jaeger parameters in the /etc/jaeger-config.json file.

        ```
        {
          "service_name": "nginx",
          // Specify the sampling rate.
          "sampler": {
            "type": "const",
            "param": 1
          },
          "reporter": {
            "localAgentHostPort": "localhost:6831"
          }
        }
        ```

    4.  Use one of the following methods to configure the Jaeger agent:

        -   If you use a self-managed Jaeger service, download the native [Jaeger agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent) and set the collector.host-port parameter.

            ```
            nohup ./jaeger-agent  --collector.host-port=10.100. **. **:142**   1>1.log 2>2.log &
            ```

        -   If you use the Jaeger service that is managed by Alibaba Cloud, download the [Tracing Analysis agent](http://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/tracing-analysis-agent-linux-amd64). Then, set the collector.host-port parameter to start the agent, so as to report data to Tracing Analysis.

            Set the <endpoint\> parameter to the endpoint that you copy in [Preparations](#section_bq8_6au_kwl). Delete "/api/traces" at the end of the endpoint that is copied from the console. For example, you can set the <endpoint\> parameter to `http://tracing-analysis-dc-sh.aliyuncs.com/adapt_abc123@abc123_efg123@efg123)`.

            ```
            // collector.host-port specifies the endpoint. The endpoint differs in different regions. Example:
            nohup ./tracing-analysis-agent-linux-amd64 --collector.host-port=<endpoint>
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

