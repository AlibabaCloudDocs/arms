# Use Jaeger to perform Nginx tracing.

Nginx is a free, open-source, and high-performance HTTP and reverse proxy server. Tracing Nginx can help users better understand the health status of their application services. This topic describes how to install link tracing for Nginx.

## Overview

When the microservice of Nginx proxy experiences fake death, it cannot evaluate the impact because no data is collected. With tracing analysis, we track the upstream Nginx of microservices and quickly calculate the page view affected by the suspended animation phenomenon.

## Preparations

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **cluster configuration**.

3.  On the cluster configuration page, click the **endpoint information** tab. Turn on cluster information in the **display Token** section.

4.  In the client collection tools section, click **Jaeger**.

5.  In the access point information column, click the duplicate icon.

    **Note:** If the application is deployed in the Alibaba Cloud production environment, select an endpoint. Otherwise, select a public endpoint.


## Procedure

1.  Pull the mirror from Registry.

    ```
    
            docker pull registry.cn-hangzhou.aliyuncs.com/public-community/jaeger-nginx:0.1 
          
    ```

2.  Run Nginx Docker.

    ```
    
            docker run --rm  -p 80:80 -e "GRPC_HOST=${GRPC_HOST}" -e "GRPC_AUTH=${GRPC_AUTH}" -d registry.cn-hangzhou.aliyuncs.com/public-community/jaeger-nginx:0.1 
          
    ```

    `Environment variable grpc_host}` and `environment variable grpc_auth}` are the information of the Agent access point saved in the [Preparations](#section_bq8_6au_kwl).

    For example,

    ```
    
            docker run --rm  -p 80:80 -e "GRPC_HOST=tracing-analysis-dc-hz.aliyuncs.com:1883" -e "GRPC_AUTH=123abc@123abc_789abc@456abc}" -d jaeger-nginx:0.1 
          
    ```

3.  Visit the Nginx page.

    Visit localhost/nginx.conf or curl "localhost/nginx.conf" in a browser.

4.  View the Nginx link data.

    Log on to the In the [Tracing Analysis console](https://tracing-sg.console.aliyun.com/), you can view the trace data of the application nginx-jaeger.


## Deploy and track Nginx on Docker

1.  Download the Dockerfile, compile it, and deploy it.

    ```
    
            wget https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/nginx-jaeger-docker.tgz tar -xzvf nginx-jaeger-docker.tgz cd nginx-jaeger // compilation docker docker build --rm --tag nginx-jaeger:0.1. 
          
    ```

2.  Run Docker.

    ```
    
            docker run --rm -p 80:80 -e "GRPC_HOST=${GRPC_HOST}" -e "GRPC_AUTH=${DRPC_AUTH}" -d jaeger-nginx:0.1 
          
    ```

    `Environment variable grpc_host}` and `environment variable grpc_auth}` are the information of the Agent access point saved in the [Preparations](#section_bq8_6au_kwl).

    For example,

    ```
    
            docker run --rm -p 80:80 -e "GRPC_HOST=tracing-analysis-dc-hz.aliyuncs.com:1883" -e "GRPC_AUTH=123abc@123abc_789abc@456abc}" -d jaeger-nginx:0.1 
          
    ```


## Deploy and track Nginx on ECS

1.  Install NGINX.

    1.  Download and decompress the Nginx source code.

        ```
        
                  wget http://nginx.org/download/nginx-1.14.2.tar.gz tar -xzvf nginx-1.14.2.tar.gz 
                
        ```

    2.  Compile the Nginx source code.

        ```
        
                  cd nginx-1.14.2 ./configure --with-compat make sudo make install 
                
        ```

2.  Install the OpenTracing plug-in.

    1.  Download the OpenTracing plug-in and decompress it.

        ```
        
                  wget https://github.com/opentracing-contrib/nginx-opentracing/releases/download/v0.7.0/linux-amd64-nginx-1.14.0-ngx_http_module.so.tgz tar -xzvf linux-amd64-nginx-1.14.0-ngx_http_module.so.tgz 
                
        ```

    2.  Copy the. so file to the modules directory of Nginx. If the directory does not exist, create it first.

        ```
        
                  sudo mkdir /usr/local/nginx/modules sudo cp ngx_http_opentracing_module.so /usr/local/nginx/modules/ngx_http_opentracing_module.so 
                
        ```

3.  Use Jaeger for link tracing.

    1.  Download the Jaeger plug-in to your working directory.

        ```
        
                  wget https://github.com/jaegertracing/jaeger-client-cpp/releases/download/v0.4.2/libjaegertracing_plugin.linux_amd64.so sudo cp libjaegertracing_plugin.linux_amd64_042.so /usr/local/lib/libjaegertracing.so 
                
        ```

    2.  The configuration file is generated.

        ```
        
                  load_module modules/ngx_http_opentracing_module.so; events {} http { opentracing on; opentracing_load_tracer /usr/local/lib/libjaegertracing_plugin.so /etc/jaeger-config.json; server { error_log /var/log/nginx/debug.log debug; listen 80; location ~ { opentracing_operation_name $uri; opentracing_trace_locations off; # the service to which the proxy is redirected. Replace as needed. proxy_pass http://127.0.0.1:8081; opentracing_propagate_context; } } } 
                
        ```

        **Note:** For more information, see [configure opentracing](https://github.com/opentracing-contrib/nginx-opentracing/blob/ea9994d7135be5ad2e3009d0f270e063b1fb3b21/doc/Reference.md).

    3.  Configure the Jaeger parameter in the /etc/jaeger-config.json file.

        ```
        
                  {"service_name": "nginx", // Configure sampling "sampler": { "type": "const", "param": 1 }, "reporter": { "localAgentHostPort": "localhost:6831" } } 
                
        ```

    4.  Use either of the following methods to configure the Jaeger Agent.

        -   If you use an on-premises Jaeger service, download the native [JaegerAgent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent) and configure collector.host-port.

            ```
            
                        nohup ./jaeger-agent --collector.host-port=10.100. **. **:142** 1>1.log 2>2.log & 
                      
            ```

        -   If you use Alibaba Cloud Jaeger, download [tracing-analysis-agent](http://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/tracing-analysis-agent-linux-amd64), start the Agent process, and use the following parameters to report data to Tracing Analysis.

            Replace the <endpoint\> nameof the access point that you saved in [Preparations](#section_bq8_6au_kwl) with that of the security center Agent. Delete "/api/traces" at the end of the endpoint information displayed on the page, for example `, http://tracing-analysis-dc-sh.aliyuncs.com/adapt_abc123@abc123_efg123@efg123 )`.

            ```
            
                        // collector.host-port is used to configure the Gateway, which varies with regions. Example: nohup ./tracing-analysis-agent-linux-amd64 --collector.host-port=<endpoint> 
                      
            ```

    5.  Run Nginx and access Nginx.

        ```
        
                  sudo /usr/local/nginx/sbin/nginx curl "http://localhost" 
                
        ```


## View the execution result

Wait for a moment for the tracing record to appear in the tracing console. If the monitoring data is found, the tracing is successful. If you have any questions about Nginx monitoring, you are welcome to exchange them through DingTalk account osprovider.

[nginx-opentracing project](https://github.com/opentracing-contrib/nginx-opentracing)

[jaeger-client-cpp project](https://github.com/jaegertracing/jaeger-client-cpp)

[zipkin-cpp-opentracing](https://github.com/rnburn/zipkin-cpp-opentracing)

[The Nginx Example of Jaeger](https://github.com/opentracing-contrib/nginx-opentracing/tree/master/example/trivial/jaeger)

[Zipkin's Nginx Example](https://github.com/opentracing-contrib/nginx-opentracing/tree/master/example/trivial/zipkin)

