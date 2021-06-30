# 使用Skywalking对Nginx进行链路追踪

在使用链路追踪控制台追踪Nginx的链路数据之前，需要将链路数据上报至链路追踪服务台。本文介绍如何通过SkyWalking Nginx LUA module上报Nginx的链路追踪数据。

SkyWalking是一款广受欢迎的国产应用性能监控APM（Application Performance Monitoring）产品，主要针对微服务、Cloud Native和容器化（Docker、Kubernetes、Mesos）架构的应用。SkyWalking的核心是一个分布式追踪系统，且目前是Apache基金会的顶级项目。

要通过SkyWalking将Java应用数据上报至链路追踪控制台，首先需要完成埋点工作。SkyWalking既支持自动埋点（Dubbo、gRPC、JDBC、OkHttp、Spring、Tomcat、Struts、Jedis等），也支持手动埋点（OpenTracing）。本文介绍自动埋点方法。

## 准备工作

1.  登录[链路追踪Tracing Analysis控制台](https://tracing-sg.console.aliyun.com/)。

2.  在左侧导航栏单击**集群配置**，并在顶部菜单栏选择目标地域。

3.  在集群配置页面上单击**接入点信息**页签，在集群信息区域打开**显示Token**开关。

4.  在客户端采集工具区域单击**SkyWalking**。

5.  在下方表格的相关信息列中，单击接入点信息末尾的复制图标。

    ![Skywalking接入点信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6357049061/p207267.png)

    **说明：** 如果应用部署于阿里云生产环境，则选择阿里云VPC网络接入点，否则选择公网接入点。


## 通过Docker镜像快速配置skywalking-nginx-lua

使用打包好的Docker配置skywalking-nginx-lua。

1.  从Registry中拉取镜像。

    ```
    docker pull registry.cn-hangzhou.aliyuncs.com/public-community/skywalking-nginx-lua:0.2
    ```

2.  运行Nignx Docker。

    ```
    docker run --rm  -p 80:80 -e "BACKEND_URL=$skywalking-nginx-lua"  -d registry.cn-hangzhou.aliyuncs.com/public-community/skywalking-nginx-lua:0.2
    ```

    `$skywalking-nginx-lua`是[准备工作](#section_hst_9gl_yew)中保存的nginx-lua接入点信息。

    例如：

    ```
    docker run --rm  -p 80:80 -e "BACKEND_URL=http://tracing-analysis-dc-hz.aliyuncs.com/adapt_123@abc_456@efg"  -d registry.cn-hangzhou.aliyuncs.com/public-community/skywalking-nginx-lua:0.2
    ```

3.  访问Nginx页面。

    -   在浏览器上访问`localhost/nginx.conf`。
    -   执行命令`curl "localhost/nginx.conf"`。

## 通过Dockerfile配置skywalking-nginx-lua

1.  下载Dockerfile。

    ```
    wget https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/nginx-skywalking-docker.tgz
    tar -xzvf nginx-skywalking-docker.tgz
    cd nginx-lua
    ```

2.  编译Docker。

    ```
    docker build --rm --tag skywalking-nginx-lua:0.2 .
    ```

3.  运行Docker。

    ```
    docker run --rm  -p 80:80 -e "BACKEND_URL=$skywalking-nginx-lua"  -d skywalking-nginx-lua:0.2
    ```

    `$skywalking-nginx-lua`是[准备工作](#section_hst_9gl_yew)中保存的nginx-lua接入点信息。

    例如：

    ```
    docker run --rm  -p 80:80 -e "BACKEND_URL=http://tracing-analysis-dc-hz.aliyuncs.com/adapt_123@abc_456@efg"  -d skywalking-nginx-lua:0.2
    ```

4.  访问Nginx页面。

    -   在浏览器上访问`localhost/nginx.conf`。
    -   执行命令`curl "localhost/nginx.conf"`。

## 在ECS上配置skywalking-nginx-lua

此处以在CentOS 7.0上的操作为例。

1.  配置Lua运行环境。

    1.  安装工具库。

        ```
        yum install gcc gcc-c++ kernel-devel -y
        yum install readline-devel -y
        yum install ncurses-devel -y
        ```

    2.  下载并安装Lua 5.3.5。

        ```
        cd /usr/local/src
        wget http://www.lua.org/ftp/lua-5.3.5.tar.gz
        tar -zxvf lua-5.3.5.tar.gz
        cd /usr/local/src/lua-5.3.5 && echo "INSTALL_TOP= /usr/local/lua_5.3.5" >> Makefile && make linux && make install
        ```

    3.  下载并安装LuaRocks 2.2.2。

        ```
        cd /usr/local/src
        wget http://keplerproject.github.io/luarocks/releases/luarocks-2.2.2.tar.gz
        tar -xzvf luarocks-2.2.2.tar.gz
        cd luarocks-2.2.2
        ./configure --prefix=/usr/local/luarocks_2.2.2 --with-lua=/usr/local/lua_5.3.5
        make build
        make install
        ```

    4.  在/etc/profile文件中添加以下内容。

        ```
        export LUA_HOME=/data/software/lua_install/lua_5.3.5
        export LUALOCKS_HOME=/data/software/lua_install/luarocks_2.2.2
        PATH=$PATH:$HOME/bin:$LUALOCKS_HOME/bin:$LUA_HOME/bin
        export PATH
        export LUA_PATH="$LUALOCKS_HOME/share/lua/5.3/?.lua;?.lua;;"
        export LUA_CPATH="$LUALOCKS_HOME/lib/lua/5.3/?.so;?.so;;"
        ```

    5.  刷新/etc/profile配置文件。

        ```
        source /etc/profile
        ```

    6.  安装Lua组件。

        ```
        luarocks install luasocket
        luarocks install lua-resty-jit-uuid
        luarocks install luaunit
        luarocks install lua-cjson 2.1.0-1
        ```

    7.  确认Lua组件是否安装成功。

        ```
        luarocks list
        ```

2.  下载并安装OpenResty Nginx。

    ```
    yum install pcre-devel openssl-devel gcc curl postgresql-devel
    cd /usr/local/src
    wget -c https://openresty.org/download/openresty-1.15.8.1rc2.tar.gz
    tar -zxvf openresty-1.15.8.1rc2.tar.gz
    cd openresty-1.15.8.1rc2
    ./configure --prefix=/usr/local/openresty/ --with-http_stub_status_module --with-luajit --without-http_redis2_module --with-http_iconv_module --with-http_postgres_module --with-stream && gmake && gmake install
    export PATH=/usr/local/openresty/nginx/sbin:$PATH
    ```

3.  下载并安装skywalking-nginx-lua。

    1.  下载并解压skywalking-nginx-lua安装包。

        ```
        cd /usr/local/skywalking-nginx-lua
        wget https://mirrors.tuna.tsinghua.edu.cn/apache/skywalking/nginx-lua/0.5.0/skywalking-nginx-lua-0.5.0-src.tgz
        tar -xzvf skywalking-nginx-lua-0.5.0-src.tgz
        ```

    2.  修改nginx.conf文件中的lua\_package\_path和startBackendTimer。

        例如：

        -   lua\_package\_path改为`/usr/local/skywalking-nginx-lua/lib/?.lua;;"`。
        -   startBackendTimer改为`require("skywalking.client"):startBackendTimer("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_***")`。
    3.  启动skywalking-nginx-lua。

        ```
        nginx -c /usr/local/skywalking-nginx-lua/examples/nginx.conf
        ```


## 查看结果

稍等片刻后到[链路追踪Tracing Analysis控制台](https://tracing-sg.console.aliyun.com/)查看，如果有监控数据则表示追踪成功。如有关于Nginx监控的疑问，欢迎通过钉钉账号osfriend交流。

