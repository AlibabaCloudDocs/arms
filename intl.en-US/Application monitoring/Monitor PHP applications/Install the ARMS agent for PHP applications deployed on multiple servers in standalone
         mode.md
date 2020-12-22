---
keyword: [PHP, application monitoring, applications deployed on multiple servers in standalone mode]
---

# Install the ARMS agent for PHP applications deployed on multiple servers in standalone mode

After you install the Application Real-Time Monitoring Service \(ARMS\) agent for PHP applications, ARMS starts to monitor the PHP applications. You can view the monitoring data of application topology, API requests, abnormal transactions, slow transactions, and SQL analysis. This topic describes how to install the ARMS agent for PHP applications that are deployed on multiple servers in standalone mode.

**Note:** If you want to use the PHP Agent of the latest version, activate [ARMS trial](https://common-buy.aliyun.com/?&commodityCode=arms#/open) now. For the trial period of the new version of the PHP Agent, visit the ARMS console announcement. If you have other questions, you can join our DingTalk Q&A Group: 23328286.

## Install the ARMS agent

1.  Install the ARMS agent. For more information, see [Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for a PHP application.md).

2.  Edit the configuration file of Apache or NGINX.

    -   For PHP applications that are deployed on multiple Apache servers in standalone mode, add `php_value arms.app_name "<yourAppNewName>"` to each VirtualHost. Replace `<yourAppNewName>` with the name of your PHP application. Example:

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

    -   For PHP applications that are deployed on multiple NGINX servers in standalone mode, add `fastcgi_param PHP_VALUE "arms.app_name=<yourAppNewName>"` to the PHP-FPM configuration file of each server. Replace `<yourAppNewName>` with the name of your PHP application. Example:

        ```
        server {
                listen       80;
                server_name  localhost;
                location / {
                            try_files $uri $uri/ /index.php? $query_string;
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
                            try_files $uri $uri/ /index.php? $query_string;
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

    Wait for about 1 minute. In the [ARMS console](https://arms-intl.console.aliyun.com/), choose **Application Monitoring** \> **Applications** If your application \(with a custom name\) appears on the page, <yourAppName\> you have successfully installed the arms agent.


## Uninstall the ARMS agent

1.  Delete the content of the php.ini or arms.ini file. For more information, see [Step 7](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for a PHP application.md) in [Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for a PHP application.md).

2.  Delete the content that you added to the Apache or NGINX configuration file in [Step 2](#step_iti_ig7_2cd) of this topic.

3.  Restart the service.

    -   If you are using NGINX servers, restart the PHP-FPM service.
    -   If you are using Apache servers, restart the Apache2 service.
4.  Run the following commands to stop and uninstall the Hercules service:

    ```
    sudo ./hercules service stop
    sudo ./hercules service uninstall
    ```

5.  Run the following command to delete the directory of the ARMS agent:

    ```
    sudo rm -rf /usr/local/arms/arms-php-agent
    ```

    You have uninstalled the ARMS agent for PHP applications.


**Related topics**  


[Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for a PHP application.md)

