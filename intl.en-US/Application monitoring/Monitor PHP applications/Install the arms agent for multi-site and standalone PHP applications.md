---
keyword: [PHP, Application monitoring, Single-host multi-site]
---

# Install the arms agent for multi-site and standalone PHP applications

After installing the application real-time Monitoring Service \(ARMS\) PHP agent, you can monitor PHP applications. For example, you can view the monitoring data of application topology, traces, abnormal transactions, and slow transactions, and conduct SQL analysis. This topic describes how to install the arms agent for single-server, multi-site PHP applications.

## Install the arms agent for multi-site and standalone PHP applications

1.  Make sure that the arms agent has been installed for a common application. For more information, see [Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for common PHP applications.md).

2.  Modify the Apache or Nginx configuration file.

    -   For an Apache single-site multi-site application, add `php_value arms.app_name "<yourAppNewName>"` configuration, where `<yourAppNewName>` replace it with the name of your PHP application. For example, in the following code:

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
                  # Require all denied
                  Require all granted
            </Directory>
        </VirtualHost>
        ```

    -   For a single-site application of Nginx, add `fastcgi_param PHP_VALUE "arms.app_name=<yourAppNewName>"` configuration, where `<yourAppNewName>` replace it with the name of your PHP application. For example, in the following code:

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
                    fastcgi_param PHP_VALUE "arms.app_name=example"
                    fastcgi_param SCRIPT_FILENAME /var/www/html/$fastcgi_script_name;
                    include        fastcgi_params;
                }
            }
         server {
                listen       80;
                server_name www.example.com
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
                    fastcgi_param PHP_VALUE "arms.app_name=test"
                    fastcgi_param SCRIPT_FILENAME /var/www/test/$fastcgi_script_name;
                    include        fastcgi_params;
                }
            }
        ```


## Uninstall the ARMS agent

1.  Delete [Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for common PHP applications.md)document's [step](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for common PHP applications.md)[7](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for common PHP applications.md) the added php.ini file content or arms.ini file.

2.  Delete the [step](#step_iti_ig7_2cd)[2](#step_iti_ig7_2cd) the configuration content to be added in the Apache or Nginx configuration file.

3.  Restart the service.

    -   If you are using an Ngnix server, restart the PHP-FPM.
    -   If you are using the Apache server, restart Apache2 service.
4.  Run the following commands to stop and uninstall the Hercules service:

    ```
    sudo ./hercules service stop
    sudo ./hercules service uninstall
    ```

5.  Run the following command to delete the arms Agent Directory:

    ```
    sudo rm -rf /usr/local/arms/arms-php-agent
    ```

    You have completely uninstalled ARMS PHP agent.


**Related topics**  


[Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for common PHP applications.md)

