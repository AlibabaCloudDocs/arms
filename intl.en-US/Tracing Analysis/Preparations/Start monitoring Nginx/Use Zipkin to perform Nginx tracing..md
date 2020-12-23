# Use Zipkin to perform Nginx tracing.

Nginx is a free, open-source, and high-performance HTTP and reverse proxy server. Tracing Nginx can help users better understand the health status of their application services. This topic describes how to install link tracing for Nginx.

## Overview

When the microservice of Nginx proxy experiences fake death, it cannot evaluate the impact because no data is collected. With tracing analysis, we track the upstream Nginx of microservices and quickly calculate the page view affected by the suspended animation phenomenon.

## Preparations

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **cluster configuration**.

3.  On the cluster configuration page, click the **endpoint information** tab. Turn on cluster information in the **display Token** section.

4.  In the collection tools section, click **Zipkin**.

5.  In the access point information column, click the duplicate icon.

    **Note:** If the application is deployed in the Alibaba Cloud production environment, select an endpoint. Otherwise, select a public endpoint.


## Procedure

1.  Pull the mirror from Registry.

    ```
    
            sudo docker pull registry.cn-hangzhou.aliyuncs.com/public-community/nginx-zipkin:0.1 
          
    ```

2.  Run Nginx Docker.

    ```
    
            docker run --rm  -p 80:80 -e "COLLECTOR_HOST=${ZIPKIN_ENDPOINT}?" -d registry.cn-hangzhou.aliyuncs.com/public-community/nginx-zipkin:0.1 
          
    ```

    `Environment variable zipkin_endpoint}` is the Agent access point of version v1 saved in [Preparations](#section_hst_9gl_yew). The "http://" part is not included and is marked with an English question mark \(?\) a question mark \(?\).

    For example,

    ```
    
            docker run --rm  -p 80:80 -e "COLLECTOR_HOST=tracing-analysis-dc-hz.aliyuncs.com/adapt_******_******/api/v1/spans?" -d registry.cn-hangzhou.aliyuncs.com/public-community/nginx-zipkin:0.1 
          
    ```

3.  Visit the Nginx page.

    Visit localhost/nginx.conf or curl "localhost/nginx.conf" in a browser.

4.  View the Nginx link data.

    Log on to the In the [Tracing Analysis console](https://tracing-sg.console.aliyun.com/), you can view the trace data of the application nginx-jaeger.


## Deploy and track Nginx on Docker

1.  Download the Dockerfile, compile it, and deploy it.

    ```
    
            wget https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/nginx-zipkin-docker.tgz tar -xzvf nginx-zipkin-docker.tgz cd nginx-zipkin // compilation docker docker build --rm --tag nginx-jaeger:0.1. 
          
    ```

2.  Run Docker.

    ```
    
            docker run --rm -p 80:80 -e "COLLECTOR_HOST=${ZIPKIN_ENDPOINT}?" -d nginx-zipkin:0.1 
          
    ```

    `Environment variable zipkin_endpoint}` is the Agent access point of version v1 saved in [Preparations](#section_hst_9gl_yew). The "http://" part is not included and is marked with an English question mark \(?\) a question mark \(?\).

    For example,

    ```
    
            docker run --rm -p 80:80 -e "COLLECTOR_HOST=tracing-analysis-dc-hz.aliyuncs.com/adapt_123@abc_456@efg/api/v1/spans?" -d nginx-zipkin:0.1 
          
    ```


## Deploy and track Nginx on ECS

1.  Use Zipkin for link tracing.

    1.  Download the Zipkin plug-in to a working directory.

        ```
        
                  wget https://github.com/rnburn/zipkin-cpp-opentracing/releases/download/v0.5.2/linux-amd64-libzipkin_opentracing_plugin.so.gz gunzip linux-amd64-libzipkin_opentracing_plugin.so.gz sudo cp linux-amd64-libzipkin_opentracing_plugin.so /usr/local/lib/libzipkin_opentracing_plugin.so 
                
        ```

    2.  The configuration file is generated.

        ```
        
                  load_module modules/ngx_http_opentracing_module.so; events {} http { opentracing on; opentracing_load_tracer /usr/local/lib/libzipkin_opentracing.so /etc/zipkin-config.json; server { error_log /var/log/nginx/debug.log debug; listen 80; location ~ { opentracing_operation_name $uri; opentracing_trace_locations off; # the service to which the proxy is redirected. Replace as needed. proxy_pass http://127.0.0.1:8081; opentracing_propagate_context; } } } 
                
        ```

        **Note:** For more information, see [configure opentracing](https://github.com/opentracing-contrib/nginx-opentracing/blob/ea9994d7135be5ad2e3009d0f270e063b1fb3b21/doc/Reference.md).

    3.  Configure the Zipkin parameter in the /etc/zipkin-config.json file.

        ```
        
                  { "service_name": "nginx", "collector_host": "zipkin" } 
                
        ```

        If you are using Alibaba Cloud Zipkin hosting service, set collector\_host to the Zipkin API.

        **Note:** The value of the Zipkin interface is the access point information of the v1 version saved in [Preparations](#section_hst_9gl_yew), excluding the "http://" part, and is indicated by an English question mark \(?\) a question mark \(?\).

        ```
        
                  "collector_host": "tracing-analysis-dc-hz.aliyuncs.com/adapt_abc123@abc456_abc123@abc356/api/v1/spans?" 
                
        ```

    4.  Use sample\_rate to configure the sampling ratio.

        ```
        
                  // 10% sampling ratio "sample_rate":0.1 
                
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

