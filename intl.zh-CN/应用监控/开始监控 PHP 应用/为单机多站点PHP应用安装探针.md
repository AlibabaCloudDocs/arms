---
keyword: [PHP, 应用监控, 单机多站点]
---

# 为单机多站点PHP应用安装探针

为PHP应用安装ARMS PHP探针后，ARMS即可开始监控PHP应用，您可以查看应用拓扑、调用链路、异常事务、慢事务和SQL分析等一系列监控数据。本文介绍如何为单机多站点PHP应用安装探针。

**说明：** 如果您需要试用新版PHP Agent，请立即开通[ARMS试用版](https://common-buy.aliyun.com/?&commodityCode=arms#/open)。新版PHP Agent的试用期结束时间请参见ARMS控制台公告。若您还有其他问题，可加入我们的钉钉答疑群：23328286。

## 安装探针

1.  安装探针，具体操作，请参见[为普通PHP应用安装探针](/intl.zh-CN/应用监控/开始监控 PHP 应用/为普通PHP应用安装探针.md)。

2.  修改Apache或Nginx的配置文件。

    -   如果是Apache单机多站点应用，则在每个VirtualHost中添加`php_value arms.app_name "<yourAppNewName>"`，其中`<yourAppNewName>`需替换为您的PHP应用的名称。例如：

        ```
        <VirtualHost *:80>
            ServerName www.example.com
            DocumentRoot /home/www/html
            php_value arms.app_name "example"
            <Directory "/home/www/html">
                  Options FollowSymLinks
                  AllowOverride All
                  Require all granted
            </Directory>
        </VirtualHost>
        <VirtualHost *:80>
            ServerName www.test.com
            DocumentRoot /home/www/test
            php_value arms.app_name "test"
            <Directory "/home/www/test">
                  Options FollowSymLinks
                  AllowOverride All
                  Require all denied
                  Require all granted
            </Directory>
        </VirtualHost>
        ```

    -   如果是Nginx单机多站点应用，则在每个Server的PHP-FPM配置文件中添加`fastcgi_param PHP_VALUE "arms.app_name=<yourAppNewName>"`，其中`<yourAppNewName>`需替换为您的PHP应用的名称。例如：

        ```
        server {
                listen       80;
                server_name  localhost;
                location / {
                            try_files $uri $uri/ /index.php?$query_string;
                    }
                error_page   500 502 503 504  /50x.html;
                location = /50x.html {
                    root   /usr/share/nginx/html;
                }
                location ~ \.php$ {
                    fastcgi_pass   localhost:9000;
                    fastcgi_index  index.php;
                    fastcgi_param  PHP_VALUE "arms.app_name=example"
                    fastcgi_param  SCRIPT_FILENAME  /var/www/html/$fastcgi_script_name;
                    include        fastcgi_params;
                }
            }
         server {
                listen       80;
                server_name  www.example.com;
                location / {
                            try_files $uri $uri/ /index.php?$query_string;
                    }
                error_page   500 502 503 504  /50x.html;
                location = /50x.html {
                    root   /usr/share/nginx/html;
                }
                location ~ \.php$ {
                    fastcgi_pass   localhost:9000;
                    fastcgi_index  index.php;
                    fastcgi_param  PHP_VALUE "arms.app_name=test"
                    fastcgi_param  SCRIPT_FILENAME  /var/www/test/$fastcgi_script_name;
                    include        fastcgi_params;
                }
            }
        ```

    等待1分钟左右，如果[ARMS控制台](https://arms-intl.console.aliyun.com/)的**应用监控** \> **应用列表**页面上出现了您的应用（应用名称为自定义的<yourAppName\>），则说明您已成功安装探针。


## 卸载探针

1.  删除[为普通PHP应用安装探针](/intl.zh-CN/应用监控/开始监控 PHP 应用/为普通PHP应用安装探针.md)文档的[步骤](/intl.zh-CN/应用监控/开始监控 PHP 应用/为普通PHP应用安装探针.md)添加的php.ini文件内容或arms.ini文件。

2.  删除本文档[步骤](#step_iti_ig7_2cd)在Apache或Nginx配置文件中添加的配置内容。

3.  重启服务。

    -   如果您使用的是Ngnix服务器，则重启PHP-FPM服务。
    -   如果您使用的是Apache服务器，则重启Apache2服务。
4.  执行以下命令停止并卸载Hercules服务。

    ```
    sudo ./hercules service stop
    sudo ./hercules service uninstall
    ```

5.  执行以下命令删除探针目录。

    ```
    sudo rm -rf /usr/local/arms/arms-php-agent
    ```

    您已完全卸载ARMS PHP探针。


**相关文档**  


[为普通PHP应用安装探针](/intl.zh-CN/应用监控/开始监控 PHP 应用/为普通PHP应用安装探针.md)

