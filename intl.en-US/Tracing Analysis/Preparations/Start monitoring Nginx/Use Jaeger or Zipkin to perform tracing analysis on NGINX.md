# Use Jaeger or Zipkin to perform tracing analysis on NGINX

NGINX is an open source and high-performance server that serves as an HTTP server and reverse proxy. You can perform tracing analysis on NGINX to better understand the running status of your application services. This topic shows you how to perform tracing analysis on NGINX. The process includes the following steps: install NGINX, install OpenTracing, and use Jaeger or Zipkin to perform tracing analysis on NGINX.

## Overview

If a slow response occurs in a microservice that uses NGINX as a proxy, you cannot estimate the impact of the slow response because no data is collected. In this case, you can use Tracing Analysis to trace NGINX requests for the microservice and calculate the number of page views that are affected by slow responses.

## Preparations



## Step 1: Install NGINX

Perform the following steps to install NGINX:

1.  Download the NGINX source code package and decompress it.

    ```
    wget http://nginx.org/download/nginx-1.14.0.tar.gz
    tar -xzvf nginx-1.14.0.tar.gz
    ```

2.  Compile the NGINX source code.

    ```
    cd nginx-1.14.0
    ./configure --with-compat
    make
    sudo make install
    ```


## Step 2: Install OpenTracing

Perform the following steps to install OpenTracing:

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


## Step 3 \(Solution 1\): Use Jaeger to perform tracing analysis

You can use Jaeger to perform tracing analysis.

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

    -   If you use the Jaeger service that is managed by Alibaba Cloud, download the native [Jaeger agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent). Then, set the reporter.grpc.host-port parameter to start the agent, so as to report data to Tracing Analysis.

        **Note:** You can use the following sample code. For more information about how to obtain the endpoint information, see [Obtain endpoint information](#tab4) in [Preparations](#section_bq8_6au_kwl).

        ```
        // reporter.grpc.host-port specifies the endpoint. The endpoint differs in different regions. Example:
        $ nohup ./jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=Authentication=abc123@789abc_abc123f@789***
        ```

5.  Run NGINX and request the NGINX service.

    ```
    sudo /usr/local/nginx/sbin/nginx
    curl "http://localhost"
    ```


## Step 3 \(Solution 2\): Use Zipkin to perform tracing analysis

You can use Zipkin to perform tracing analysis.

1.  Download Zipkin to a working directory.

    ```
    wget https://github.com/rnburn/zipkin-cpp-opentracing/releases/download/v0.5.2/linux-amd64-libzipkin_opentracing_plugin.so.gz
    $ gunzip linux-amd64-libzipkin_opentracing_plugin.so.gz
    $ sudo cp linux-amd64-libzipkin_opentracing_plugin.so /usr/local/lib/libzipkin_opentracing_plugin.so
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

    -   If you use a self-managed Zipkin service, set the collector\_host parameter to the IP address of Zipkin.
    -   If you use the Zipkin service that is managed by Alibaba Cloud, set the collector\_host parameter to the endpoint of Zipkin. Example:

        **Note:** Enter the endpoint of Zipkin by removing `http://` from the version 1 endpoint of Zipkin. You can obtain the latter from the Overview page of the Tracing Analysis console. For more information about how to obtain the endpoint information, see [Obtain endpoint information](#tab4) in [Preparations](#section_bq8_6au_kwl).

        ```
        "collector_host": "tracing-analysis-dc-hz.aliyuncs.com/adapt_abc123@abc456_abc123@abc***/api/v1/spans?"
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

## 更多信息

[nginx-opentracing project](https://github.com/opentracing-contrib/nginx-opentracing)

[jaeger-client-cpp project](https://github.com/jaegertracing/jaeger-client-cpp)

[zipkin-cpp-opentracing](https://github.com/rnburn/zipkin-cpp-opentracing)

[Example of using Jaeger to perform tracing analysis on NGINX](https://github.com/opentracing-contrib/nginx-opentracing/tree/master/example/trivial/jaeger)

[Example of using Zipkin to perform tracing analysis on NGINX](https://github.com/opentracing-contrib/nginx-opentracing/tree/master/example/trivial/zipkin)

