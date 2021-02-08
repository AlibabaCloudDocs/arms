# Use SkyWalking to perform tracing analysis on NGINX

Before you can view the trace data of NGINX in the Tracing Analysis console, you must report the trace data to Tracing Analysis. This topic shows you how to use the SkyWalking NGINX LUA module to report the trace data of NGINX.

SkyWalking is a popular application performance monitoring \(APM\) service developed in China. SkyWalking is designed for microservices, cloud-native architectures, and container-based architectures. Container-based architectures include Docker, Kubernetes, and Mesos. The core of SkyWalking is a distributed tracing system, which is a top-level project of Apache Software Foundation.

To use SkyWalking to report Java application data to the Tracing Analysis console, you must first instrument the application. SkyWalking provides auto-instrument agents such as Dubbo, gRPC, JDBC, OkHttp, Spring, Tomcat, Struts, and Jedis. SkyWalking also allows you to manually instrument applications based on the OpenTracing standard. This topic shows you how to automatically instrument applications.

## Preparations

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **Cluster Configurations**. In the top navigation bar, select a region.

3.  On the Cluster Configurations page, click the **Access point information** tab. Then, turn on **Show Token** for the Cluster Information parameter.

4.  Set the Client parameter to **SkyWalking**.

5.  In the Related Information column of the table in the lower part, click the copy icon next to the endpoint that you want to use.

    **Note:** If you deploy your application in an Alibaba Cloud production environment, select a VPC endpoint. Otherwise, select a public endpoint.


## Configure the SkyWalking NGINX LUA module by using a Docker image

Use a pre-built Docker image to configure the SkyWalking NGINX LUA module.

1.  Pull the image from the registry.

    ```
    docker pull registry.cn-hangzhou.aliyuncs.com/public-community/skywalking-nginx-lua:0.2
    ```

2.  Run NGINX in a Docker container.

    ```
    docker run --rm  -p 80:80 -e "BACKEND_URL=$skywalking-nginx-lua"  -d registry.cn-hangzhou.aliyuncs.com/public-community/skywalking-nginx-lua:0.2
    ```

    Replace `$skywalking-nginx-lua` with the NGINX LUA endpoint that you copy and save in [Preparations](#section_hst_9gl_yew).

    Example:

    ```
    docker run --rm  -p 80:80 -e "BACKEND_URL=http://tracing-analysis-dc-hz.aliyuncs.com/adapt_123@abc_456@efg"  -d registry.cn-hangzhou.aliyuncs.com/public-community/skywalking-nginx-lua:0.2
    ```

3.  Visit NGINX.

    -   Enter `localhost/nginx.conf` in the address bar of a browser.
    -   Run the `curl "localhost/nginx.conf"` command.

## Configure the SkyWalking NGINX LUA module by using a Dockerfile

1.  Download a Dockerfile.

    ```
    wget https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/nginx-skywalking-docker.tgz
    tar -xzvf nginx-skywalking-docker.tgz
    cd nginx-lua
    ```

2.  Build the Dockerfile.

    ```
    docker build --rm --tag skywalking-nginx-lua:0.2 .
    ```

3.  Run NGINX in a Docker container.

    ```
    docker run --rm  -p 80:80 -e "BACKEND_URL=$skywalking-nginx-lua"  -d skywalking-nginx-lua:0.2
    ```

    Replace `$skywalking-nginx-lua` with the NGINX LUA endpoint that you copy and save in [Preparations](#section_hst_9gl_yew).

    Example:

    ```
    docker run --rm  -p 80:80 -e "BACKEND_URL=http://tracing-analysis-dc-hz.aliyuncs.com/adapt_123@abc_456@efg"  -d skywalking-nginx-lua:0.2
    ```

4.  Visit NGINX.

    -   Enter `localhost/nginx.conf` in the address bar of a browser.
    -   Run the `curl "localhost/nginx.conf"` command.

## Configure the SkyWalking NGINX LUA module on an ECS instance

In this example, CentOS 7.0 is installed on the Elastic Compute Service \(ECS\) instance.

1.  Configure the runtime environment for LUA.

    1.  Install required tools.

        ```
        yum install gcc gcc-c++ kernel-devel -y
        yum install readline-devel -y
        yum install ncurses-devel -y
        ```

    2.  Download and install LUA 5.3.5.

        ```
        cd /usr/local/src
        wget http://www.lua.org/ftp/lua-5.3.5.tar.gz
        tar -zxvf lua-5.3.5.tar.gz
        cd /usr/local/src/lua-5.3.5 && echo "INSTALL_TOP= /usr/local/lua_5.3.5" >> Makefile && make linux && make install
        ```

    3.  Download and install LuaRocks 2.2.2.

        ```
        cd /usr/local/src
        wget http://keplerproject.github.io/luarocks/releases/luarocks-2.2.2.tar.gz
        tar -xzvf luarocks-2.2.2.tar.gz
        cd luarocks-2.2.2
        ./configure --prefix=/usr/local/luarocks_2.2.2 --with-lua=/usr/local/lua_5.3.5
        make build
        make install
        ```

    4.  Add the following lines to the /etc/profile file:

        ```
        export LUA_HOME=/data/software/lua_install/lua_5.3.5
        export LUALOCKS_HOME=/data/software/lua_install/luarocks_2.2.2
        PATH=$PATH:$HOME/bin:$LUALOCKS_HOME/bin:$LUA_HOME/bin
        export PATH
        export LUA_PATH="$LUALOCKS_HOME/share/lua/5.3/?.lua;?.lua;;"
        export LUA_CPATH="$LUALOCKS_HOME/lib/lua/5.3/?.so;?.so;;"
        ```

    5.  Update the /etc/profile file.

        ```
        source /etc/profile
        ```

    6.  Install LUA.

        ```
        luarocks install luasocket
        luarocks install lua-resty-jit-uuid
        luarocks install luaunit
        luarocks install lua-cjson 2.1.0-1
        ```

    7.  Verify that LUA is installed.

        ```
        luarocks list
        ```

2.  Download and install OpenResty NGINX.

    ```
    yum install pcre-devel openssl-devel gcc curl postgresql-devel
    cd /usr/local/src
    wget -c https://openresty.org/download/openresty-1.15.8.1rc2.tar.gz
    tar -zxvf openresty-1.15.8.1rc2.tar.gz
    cd openresty-1.15.8.1rc2
    ./configure --prefix=/usr/local/openresty/ --with-http_stub_status_module --with-luajit --without-http_redis2_module --with-http_iconv_module --with-http_postgres_module --with-stream && gmake && gmake install
    export PATH=/usr/local/openresty/nginx/sbin:$PATH
    ```

3.  Download and install the SkyWalking NGINX LUA module.

    1.  Download and decompress the installation package of the SkyWalking NGINX LUA module.

        ```
        cd /usr/local/skywalking-nginx-lua
        wget https://mirrors.bfsu.edu.cn/apache/skywalking/nginx-lua/0.3.0/skywalking-nginx-lua-0.3.0-src.tgz
        tar -xzvf skywalking-nginx-lua-0.3.0-src.tgz
        ```

    2.  Modify the lua\_package\_path and startBackendTimer variables in the nginx.conf file.

        Example:

        -   Set the lua\_package\_path variable to `/usr/local/skywalking-nginx-lua/lib/?.lua;;"`.
        -   Set the startBackendTimer variable to `require("skywalking.client"):startBackendTimer("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_***")`.
    3.  Start the SkyWalking NGINX LUA module.

        ```
        nginx -c /usr/local/skywalking-nginx-lua/examples/nginx.conf
        ```


## View the results

Wait a moment. Then, log on to the [Tracing Analysis console](https://tracing-sg.console.aliyun.com/). If monitoring data is displayed, the tracing is successful. If you have questions about how to monitor NGINX, contact the DingTalk account osfriend.

