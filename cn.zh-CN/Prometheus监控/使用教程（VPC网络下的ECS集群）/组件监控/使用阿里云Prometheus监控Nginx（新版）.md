# 使用阿里云Prometheus监控Nginx（新版）

阿里云Prometheus监控提供一键安装配置Nginx类型的组件，并提供开箱即用的专属监控大盘。本文介绍新版Nginx类型的组件安装配置详情。

您已成功安装并运行Nginx服务。

-   Nginx状态监控模块ngx\_http\_stub\_status\_module是统计Nginx服务所接收和处理的请求数量的模块。
-   新版Nginx类型的组件安装的是ngx\_http\_stub\_status\_module模块。
-   新版Nginx类型的组件采集的Nginx指标如下表所示。

    |指标|描述|
    |--|--|
    |nginx\_connections\_accepted|接受的客户端连接总数|
    |nginx\_connections\_active|当前客户端连接数|
    |nginx\_connections\_handled|Handled状态的连接数|
    |nginx\_connections\_reading|读取客户端的连接数|
    |nginx\_connections\_waiting|等待中的客户端连接数|
    |nginx\_connections\_writing|回写客户端的连接数|
    |nginx\_http\_requests\_total|客户端请求总数|
    |nginx\_up|Nginx组件是否正常运行|
    |nginxexporter\_build\_info|Nginx组件的构建信息|


## 步骤一：安装ngx\_http\_stub\_status\_module模块

如果您的Nginx服务运行在云服务器ECS，则按照以下步骤安装Nginx类型的组件。

1.  检查状态监控模块ngx\_http\_stub\_status\_module是否已安装。

    ```
    nginx -V 2>&1 | grep -o with-http_stub_status_module
    ```

    -   出现以下提示则表示已安装ngx\_http\_stub\_status\_module模块。

        ![cw_prom_exporter_nginx_module](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7284298951/p128838.png)

    -   若未出现以上提示，则说明未安装ngx\_http\_stub\_status\_module模块，可执行以下命令安装此模块。

        ```
        wget http://nginx.org/download/nginx-1.13.12.tar.gz
        tar xfz nginx-1.13.12.tar.gz
        cd nginx-1.13.12/
        ./configure --with-http_stub_status_module
        make
        make install
        ```

2.  启用ngx\_http\_stub\_status\_module模块查询Nginx状态。

    ```
    location /nginx_status {
      stub_status on;
      allow 127.0.0.1;  #only allow requests from localhost
      deny all;   #deny all other hosts 
     }
    ```

    **说明：**

    -   Location地址请严格命名为`nginx_status`。
    -   `allow 127.0.0.1`和`deny all`表示仅允许本地访问。若需允许Nginx组件访问，则可将这两行代码注释，或者将`127.0.0.1`设置为Nginx组件的IP地址。
3.  重启Nginx。

    ```
    nginx -t
    nginx -s reload 
    ```

4.  验证ngx\_http\_stub\_status\_module模块是否已成功启动。

    ```
    curl http://127.0.0.1/nginx_status
    ```

    出现以下提示则表示ngx\_http\_stub\_status\_module模块已成功启动。

    ![cw_prom_exporter_nginx_module_success](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7284298951/p128860.png)


## 步骤二：安装新版Nginx类型的组件

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在页面左上角选择目标地域，然后单击Prometheus示例实例名称。

4.  在左侧导航栏单击**组件监控**。

5.  在组件监控页面，单击右上角的**添加组件监控**。

6.  在组件列表对话框右中单击Nginx\(V2\)组件图标。

7.  在Nginx\(V2\)组件配置对话框的**配置**页签输入各项参数。

    ![Nginx（v2）组件监控](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4686416261/p293833.png)

    |参数|描述|
    |--|--|
    |**组件名称**|组件的名称命名规范要求如下：    -   仅可包含小写字母、数字和短划线（-），且短划线不可出现在开头或结尾。
    -   名称具有唯一性。
**说明：** 默认名称由组件类型及数字后缀组成。 |
    |**Nginx（V2） 地址**|Nginx的连接地址。|
    |**Nginx（V2） 端口**|Nginx的端口号，例如：80。|

8.  在Nginx\(V2\)组件配置对话框的**指标**页签查看监控指标。

9.  配置完成后，单击**确定**。

10. 在组件监控页面，单击**大盘**列的大盘链接，查看Prometheus监控大盘。

    ![pg_prom_dashboard_Nginx](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7284298951/p97649.png)


## 相关操作

在组件监控页面，可对已添加的组件执行以下操作：

-   单击**操作**列的**删除**，可删除已添加的组件。
-   单击**操作**列的**日志**，可查看组件的运行日志。
-   单击**操作**列的**详情**，可查看组件的详情，包括组件的环境变量和描述信息。

