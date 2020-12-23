# 使用 Jaeger 或 Zipkin 对 Nginx 进行链路追踪

Nginx 是一款开源的高性能 HTTP 服务器和反向代理服务器，对其进行链路追踪可以帮助我们更好地了解应用服务的运行状况。本教程详细介绍了从安装 Nginx、安装 OpenTracing 插件，到使用 Jaeger 或 Zipkin 对 Nginx 进行链路追踪的步骤。

## 教程概述

当 Nginx 代理的微服务出现假死现象时，因为采集不到任何数据，所以无法评估造成的影响。借助链路追踪，我们追踪微服务的上游 Nginx，并快速统计出假死现象影响的访问量。

## 准备工作



## 步骤一：安装 Nginx

请按照以下步骤安装 Nginx。

1.  下载并解压 Nginx 源码。

    ```
    wget http://nginx.org/download/nginx-1.14.0.tar.gz
    tar -xzvf nginx-1.14.0.tar.gz
    ```

2.  编译 Nginx 源码。

    ```
    cd nginx-1.14.0
    ./configure --with-compat
    make
    sudo make install
    ```


## 步骤二：安装 OpenTracing 插件

请按照以下步骤安装 OpenTracing 插件。

1.  下载 OpenTracing 插件并解压。

    ```
    wget https://github.com/opentracing-contrib/nginx-opentracing/releases/download/v0.7.0/linux-amd64-nginx-1.14.0-ngx_http_module.so.tgz
    tar -xzvf linux-amd64-nginx-1.14.0-ngx_http_module.so.tgz
    ```

2.  拷贝 .so 文件至 Nginx 的 modules 目录。如果不存在该目录则需要先创建。

    ```
    sudo mkdir /usr/local/nginx/modules
    sudo cp ngx_http_opentracing_module.so /usr/local/nginx/modules/ngx_http_opentracing_module.so
    ```


## 步骤三（方案一）：使用 Jaeger 进行链路追踪

您可以选择使用 Jaeger 进行链路追踪。

1.  下载 Jaeger 插件并将其拷贝至任意工作目录。

    ```
    wget https://github.com/jaegertracing/jaeger-client-cpp/releases/download/v0.4.2/libjaegertracing_plugin.linux_amd64.so
    sudo cp libjaegertracing_plugin.linux_amd64_042.so /usr/local/lib/libjaegertracing.so
    ```

2.  配置 /usr/local/nginx/conf/nginx.conf 文件。

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
          # 跳转到代理的服务，请替换为需要的值。
          proxy_pass http://127.0.0.1:8081;
          opentracing_propagate_context;
        }
      }
    }
    ```

    **说明：** 详细配置说明参见 [opentracing-contrib 配置](https://github.com/opentracing-contrib/nginx-opentracing/blob/ea9994d7135be5ad2e3009d0f270e063b1fb3b21/doc/Reference.md)。

3.  在 /etc/jaeger-config.json 文件中配置 Jaeger 参数。

    ```
    {
      "service_name": "nginx",
      // 配置采样
      "sampler": {
        "type": "const",
        "param": 1
      },
      "reporter": {
        "localAgentHostPort": "localhost:6831"
      }
    }
    ```

4.  采用以下方法之一配置 Jaeger Agent。

    -   若使用自建的 Jaeger 服务，则下载原生 [Jaeger Agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent)，并配置 collector.host-port。

        ```
        nohup ./jaeger-agent  --collector.host-port=10.100.**.**:142**   1>1.log 2>2.log &
        ```

    -   若使用阿里云的 Jaeger 托管服务，则下载原生 [Jaeger Agent](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/jaeger-agent)，并用以下参数启动 Agent，以将数据上报至链路追踪 Tracing Analysis。

        **说明：** 以下为示例配置，接入点信息的获取方法参见[准备工作](#section_bq8_6au_kwl)中的[获取接入点信息](#tab4)。

        ```
        // reporter.grpc.host-port 用于设置网关，网关因地域而异。 例如：
        $ nohup ./jaeger-agent --reporter.grpc.host-port=tracing-analysis-dc-sz.aliyuncs.com:1883 --jaeger.tags=Authentication=abc123@789abc_abc123f@789***
        ```

5.  运行 Nginx 并访问 Nginx 服务。

    ```
    sudo /usr/local/nginx/sbin/nginx
    curl "http://localhost"
    ```


## 步骤三（方案二）：使用 Zipkin 进行链路追踪

您也可以选择使用 Zipkin 进行链路追踪。

1.  下载 Zipkin 插件并将其拷贝至任意工作目录。

    ```
    wget https://github.com/rnburn/zipkin-cpp-opentracing/releases/download/v0.5.2/linux-amd64-libzipkin_opentracing_plugin.so.gz
    $ gunzip linux-amd64-libzipkin_opentracing_plugin.so.gz
    $ sudo cp linux-amd64-libzipkin_opentracing_plugin.so /usr/local/lib/libzipkin_opentracing_plugin.so
    ```

2.  配置 /usr/local/nginx/conf/nginx.conf 文件。

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
                     # 跳转到代理的服务，请替换为需要的值。      
                     proxy_pass http://127.0.0.1:8081;      
                     opentracing_propagate_context;    
            }
      }
    }
    ```

    **说明：** 详细配置说明参见 [opentracing-contrib 配置](https://github.com/opentracing-contrib/nginx-opentracing/blob/ea9994d7135be5ad2e3009d0f270e063b1fb3b21/doc/Reference.md)。

3.  在 /etc/zipkin-config.json 文件中配置 Zipkin 参数。

    ```
    {
      "service_name": "nginx",
      "collector_host": "zipkin"
    }
    ```

    -   若使用自建的 Zipkin 服务，则将 collector\_host 配置成 Zipkin 的 IP 即可。
    -   若使用阿里云的 Zipkin 托管服务，则将 collector\_host 配置为 Zipkin 接口。例如：

        **说明：** Zipkin 接口的值为控制台概览页面的 Zipkin v1 接口去掉 `http://` 之后的部分。接入点信息的获取方法参见[准备工作](#section_bq8_6au_kwl)中的[获取接入点信息](#tab4)。

        ```
        "collector_host": "tracing-analysis-dc-hz.aliyuncs.com/adapt_abc123@abc456_abc123@abc***/api/v1/spans?"
        ```

4.  通过 sample\_rate 配置采样比例。

    ```
    // 10% 的采样比例
    "sample_rate":0.1
    ```

5.  运行 Nginx 并访问 Nginx 服务。

    ```
    sudo /usr/local/nginx/sbin/nginx
    curl "http://localhost"
    ```


## 查看结果

稍等片刻后到链路追踪控制台查看，如果有监控数据则表示追踪成功。如有关于 Nginx 监控的疑问，欢迎通过钉钉账号 osfriend 交流。

[nginx-opentracing 项目](https://github.com/opentracing-contrib/nginx-opentracing)

[jaeger-client-cpp 项目](https://github.com/jaegertracing/jaeger-client-cpp)

[zipkin-cpp-opentracing](https://github.com/rnburn/zipkin-cpp-opentracing)

[Jaeger 的 Nginx Example](https://github.com/opentracing-contrib/nginx-opentracing/tree/master/example/trivial/jaeger)

[Zipkin 的 Nginx Example](https://github.com/opentracing-contrib/nginx-opentracing/tree/master/example/trivial/zipkin)

