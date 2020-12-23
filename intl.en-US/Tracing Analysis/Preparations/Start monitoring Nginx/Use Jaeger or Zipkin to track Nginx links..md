# Use Jaeger or Zipkin to track Nginx links.

Nginx is an open-source high-performance HTTP server and reverse proxy server. It provides link tracking to help you better understand the running status of application services. This tutorial describes how to install Nginx and OpenTracing plug-ins, and use Jaeger or Zipkin to trace Nginx links.

## Overview

When the Nginx proxy microservice is suspended, the impact cannot be evaluated because no data is collected. With link tracing, we track Nginx, the upstream of microservices, and quickly count the number of visits affected by the fake death.

## Preparation



## Step 1: install Nginx

Follow these steps to install Nginx.

1.  Download and decompress the Nginx source code.

    ```
    wget http://nginx.org/download/nginx-1.14.0.tar.gz
    tar -xzvf nginx-1.14.0.tar.gz
    ```

2.  Compile the Nginx source code.

    ```
    cd nginx-1.14.0
    . /configure --with-compat
    Make
    sudo make install
    ```


## Step 2: install the OpenTracing plug-in

Follow these steps to install the OpenTracing plug-in.

1.  Download and decompress the OpenTracing plug-in.

    ```
    wget https://github.com/opentracing-contrib/nginx-opentracing/releases/download/v0.7.0/linux-amd64-nginx-1.14.0-ngx_http_module.so.tgz
    tar -xzvf linux-amd64-nginx-1.14.0-ngx_http_module.so.tgz
    ```

2.  Copy. So to the NginxmodulesDirectory. If the directory does not exist, create one first.

    ```
    sudo mkdir /usr/local/nginx/modules
    sudo cp ngx_http_opentracing_module.so /usr/local/nginx/modules/ngx_http_opentracing_module.so
    ```


## Step 3 \(solution 1\): use Jaeger for link tracing

You can use Jaeger for link tracing.

1.  Download the Jaeger plug-in and copy it to any working directory.

    ```
    wget https://github.com/jaegertracing/jaeger-client-cpp/releases/download/v0.4.2/libjaegertracing_plugin.linux_amd64.so
    sudo cp libjaegertracing_plugin.linux_amd64_042.so /usr/local/lib/libjaegertracing.so
    ```

2.  Configuration/usr/local/nginx/conf/nginx.confFile.

    ```
    load_module modules/ngx_http_opentracing_module.so;
    
    events {}
    
    http {
      opentracing on;
    
      opentracing_load_tracer /usr/local/lib/libjaegertracing_plugin.so /etc/jaeger-config.json;
    
      server {
    
        error_log /var/log/nginx/debug.log debug;
        listen 80;
    
        location ~ {
          opentracing_operation_name $uri;
          opentracing_trace_locations off;
          # Jump to the proxy service. Replace it with the required value.
          proxy_pass http://127.0.0.1:8081;
          Opentrating_procate_context;
        }
      }
    }
    ```

    **Note:** For more information, see[Opentracing-contribute configuration](https://github.com/opentracing-contrib/nginx-opentracing/blob/ea9994d7135be5ad2e3009d0f270e063b1fb3b21/doc/Reference.md).

3.  In/etc/jaeger-config.jsonSet the Jaeger parameter in the file.

    ```
    {
      &quot;service_name&quot;: &quot;nginx&quot;,
      // Configure sampling.
      &quot;sampler&quot;: {
        &quot;type&quot;: &quot;const&quot;,
        &quot;param&quot;: 1
      },
      &quot;reporter&quot;: {
        &quot;localAgentHostPort&quot;: &quot;localhost:6831&quot;
      }
    }
    ```

4.  Use either of the following methods to configure the Jaeger Agent:

    -   If you use a self-built Jaeger service, download the native[Jaeger Agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent), And configurecollector.host-port.

        ```
        nohup. /jaeger-agent --collector.host-port=10.100. Cause *. **: 142 ** 1> 1.log 2> 2.log &
        ```

    -   If you use the Jaeger hosting service of Alibaba Cloud, download the native[Jaeger Agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent)Start the Agent with the following parameters to report the data to the link Tracing Analysis.

        **Note:** The following is an example configuration. For more information about how to obtain the endpoint information, see[Preparation](#section_bq8_6au_kwl)In[Obtain access point information](#tab4).

        ```
        // Reporter. grpc. host-port is used to set the gateway. The Gateway varies according to the region. Example:
        $ nohup. /jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=Authentication=abc123@789abc_abc123f@789***
        ```

5.  Run Nginx and access the Nginx service.

    ```
    sudo /usr/local/nginx/sbin/nginx
    curl &quot;http://localhost&quot;
    ```


## Step 3 \(solution 2\): use Zipkin for link tracking

You can also choose to use Zipkin for link tracking.

1.  Download the Zipkin plug-in and copy it to any working directory.

    ```
    wget https://github.com/rnburn/zipkin-cpp-opentracing/releases/download/v0.5.2/linux-amd64-libzipkin_opentracing_plugin.so.gz
    $ gunzip linux-amd64-libzipkin_opentracing_plugin.so.gz
    $ sudo cp linux-amd64-libzipkin_opentracing_plugin.so /usr/local/lib/libzipkin_opentracing_plugin.so
    ```

2.  Configuration/usr/local/nginx/conf/nginx.confFile.

    ```
    load_module modules/ngx_http_opentracing_module.so;
    
    events {}
    
    http {  
        opentracing on;  
        opentracing_load_tracer /usr/local/lib/libzipkin_opentracing.so /etc/zipkin-config.json;  
        server {    
              error_log /var/log/nginx/debug.log debug; 
              listen 80;    
              location ~ {      
                     opentracing_operation_name $uri;      
                     opentracing_trace_locations off;     
                     # Jump to the proxy service. Replace it with the required value.      
                     proxy_pass http://127.0.0.1:8081;      
                     Opentrating_procate_context;    
            }
      }
    }
    ```

    **Note:** For more information, see[Opentracing-contribute configuration](https://github.com/opentracing-contrib/nginx-opentracing/blob/ea9994d7135be5ad2e3009d0f270e063b1fb3b21/doc/Reference.md).

3.  In/etc/zipkin-config.jsonConfigure Zipkin parameters in the file.

    ```
    {
      &quot;service_name&quot;: &quot;nginx&quot;,
      &quot;collector_host&quot;: &quot;zipkin&quot;
    }
    ```

    -   If you use a self-built Zipkin service,Connector\_hostConfigure Zipkin IP addresses.
    -   If you use Alibaba Cloud Zipkin hosting service,Connector\_hostConfigure a Zipkin interface. Example:

        **Note:** Zipkin interface value is consoleOverviewRemove the Zipkin v1 interface of the page.`http://`After. For more information about how to obtain access point information, see[Preparation](#section_bq8_6au_kwl)In[Obtain access point information](#tab4).

        ```
        &quot;Connector_host&quot;: &quot;hostname &quot;
        ```

4.  PassSample\_rateSet the sampling ratio.

    ```
    // 10% sampling ratio
    &quot;Sample_rate&quot;: 0.1
    ```

5.  Run Nginx and access the Nginx service.

    ```
    sudo /usr/local/nginx/sbin/nginx
    curl &quot;http://localhost&quot;
    ```


## View Results

Wait a moment and check in the link tracing console. If monitoring data is displayed, the tracing is successful. If you have any questions about Nginx monitoring, feel free to contact you through the DingTalk account osriend.

[Nginx-opentracing project](https://github.com/opentracing-contrib/nginx-opentracing)

[Jaeger-client-cpp project](https://github.com/jaegertracing/jaeger-client-cpp)

[zipkin-cpp-opentracing](https://github.com/rnburn/zipkin-cpp-opentracing)

[Nginx Example of Jaeger](https://github.com/opentracing-contrib/nginx-opentracing/tree/master/example/trivial/jaeger)

[Zipkin Nginx Example](https://github.com/opentracing-contrib/nginx-opentracing/tree/master/example/trivial/zipkin)

