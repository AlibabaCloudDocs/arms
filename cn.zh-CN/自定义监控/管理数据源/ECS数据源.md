# ECS数据源

ECS实例是重要的日志产生来源，也是ARMS支持的自定义监控数据源。您可以授权ARMS将您阿里云账号下的ECS实例信息同步至ARMS控制台，为这些实例安装Logtail日志采集Agent。您还可以为同步的ECS实例创建分组以便管理。

-   [提交工单申请开通自定义监控](https://selfservice.console.aliyun.com/ticket/createIndex)
-   [创建ECS实例](/cn.zh-CN/实例/实例概述.md)

## 同步ECS实例

**说明：** 执行同步ECS操作时，必须使用阿里云账号或具备完整权限（包括全部读权限和写权限）的RAM用户，不可使用不具备完整权限的RAM用户，例如仅具备只读权限的RAM用户。

将阿里云账号下的ECS实例信息同步至ARMS。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，选择**自定义监控数据源管理** \> **云服务器ECS**。

3.  如果此前未授权ARMS读取ECS数据，则按照ARMS的提示信息完成授权。

    1.  在**提示**对话框，单击**进入RAM进行授权**。

        ![Dialog Box Authorize ARMS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8444340161/p43560.png)

    2.  在**云资源访问授权**页面，选择权限，然后单击**同意授权**。

        ![Dialog Box Cloud Resource Authorization](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8444340161/p43561.png)

4.  在**实例列表**页面的顶部菜单栏，选择地域，然后在页面右上角，单击**同步ECS**。

5.  在**同步ECS**对话框，单击**确定同步**。

    **实例列表**页面显示您在该地域创建的ECS实例。

    ![ECS实例](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8444340161/p212745.png)


## 检查Logtail Agent状态

在为ECS实例安装Logtail Agent前，您需要检查ECS实例是否已安装Logtail Agent。

1.  在**实例列表**页面的**云服务器ECS**页签下，检查Agent状态。

    -   检查单个ECS实例的Agent状态：找到目标ECS实例，在其右侧**操作**列，单击**检查Agent**。
    -   检查多个ECS实例的Agent状态：选中所有目标ECS实例，在页面底部，单击**批量检测Agent**。
2.  在**提示**对话框，单击**确定**。


## 安装Logtail Agent

ARMS通过Logtail Agent收集ECS实例日志，您需要为目标ECS实例安装Logtail Agent。

1.  [连接ECS实例](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  下载Logtail Agent。

    ```
    wget <logtail.sh_path> -O logtail.sh
    ```

    请根据ECS实例的网络环境和日志服务所在地域替换<logtail.sh\_path\>。

    |网络类型|地域|下载地址|
    |----|--|----|
    |经典网络|华北2（北京）|http://logtail-release-cn-beijing.oss-cn-beijing-internal.aliyuncs.com/linux64/logtail.sh|
    |华北1（青岛）|http://logtail-release-cn-qingdao.oss-cn-qingdao-internal.aliyuncs.com/linux64/logtail.sh|
    |华东1（杭州）|http://logtail-release-cn-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/linux64/logtail.sh|
    |华东2（上海）|http://logtail-release-cn-shanghai.oss-cn-shanghai-internal.aliyuncs.com/linux64/logtail.sh|
    |华南1（深圳）|http://logtail-release-cn-shenzhen.oss-cn-shenzhen-internal.aliyuncs.com/linux64/logtail.sh|
    |VPC|华北2（北京）|http://logtail-release-bj.vpc100-oss-cn-beijing.aliyuncs.com/linux64/logtail.sh|
    |华东1（杭州）|http://logtail-release.vpc100-oss-cn-hangzhou.aliyuncs.com/linux64/logtail.sh|
    |华东2（上海）|http://logtail-release-sh.vpc100-oss-cn-shanghai.aliyuncs.com/linux64/logtail.sh|
    |华南1（深圳）|http://logtail-release-sz.vpc100-oss-cn-shenzhen.aliyuncs.com/linux64/logtail.sh|
    |公网（自建IDC或其他云主机）|华北2（北京）|http://logtail-release-cn-beijing.oss-cn-beijing.aliyuncs.com/linux64/logtail.sh|
    |华北1（青岛）|http://logtail-release-cn-qingdao.oss-cn-qingdao.aliyuncs.com/linux64/logtail.sh|
    |华东1（杭州）|http://logtail-release-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/linux64/logtail.sh|
    |华东2（上海）|http://logtail-release-cn-shanghai.oss-cn-shanghai.aliyuncs.com/linux64/logtail.sh|
    |华南1（深圳）|http://logtail-release-cn-shenzhen.oss-cn-shenzhen.aliyuncs.com/linux64/logtail.sh|

3.  执行授权操作。

    ```
    chmod 755 logtail.sh
    ```

4.  安装Agent。

    ```
    sudo ./logtail.sh install <region_id>
    ```

    请根据ECS实例的网络环境和日志服务所在地域替换<region\_id\>。

    |网络类型|地域|地域ID|
    |----|--|----|
    |经典网络|华北2（北京）|cn-beijing|
    |华北1（青岛）|cn-qingdao|
    |华东1（杭州）|cn-hangzhou|
    |华东2（上海）|cn-shanghai|
    |华南1（深圳）|cn-shenzhen|
    |VPC|华北2（北京）|cn\_beijing\_vpc|
    |华东1（杭州）|cn\_hangzhou\_vpc|
    |华东2（上海）|cn\_shanghai\_vpc|
    |华南1（深圳）|cn\_shenzhen\_vpc|
    |公网（自建IDC或其他云主机）|华北2（北京）|cn-beijing-internet|
    |华北1（青岛）|cn-qingdao-internet|
    |华东1（杭州）|cn-hangzhou-internet|
    |华东2（上海）|cn-shanghai-internet|
    |华南1（深圳）|cn-shenzhen-internet|

5.  创建配置文件。

    ```
    sudo touch /etc/ilogtail/users/1098370038733503
    ```

6.  [检查Logtail Agent状态](#section_e1j_tpi_0tn)。

    目标实例的**Agent状态**列显示**已安装**。


## 卸载Logtail Agent

如果您不再需要监控某个ECS实例，您可以卸载Logtail Agent。

1.  [连接ECS实例](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  卸载Logtail Agent。

    ```
    sudo sh logtail.sh uninstall
    ```

3.  删除配置文件。

    ```
    sudo rm -rf /etc/ilogtail/users/1098370038733503
    ```


## 创建ECS分组

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，选择**自定义监控数据源管理** \> **云服务器ECS**。

3.  在**实例列表**页面的顶部菜单栏，选择地域，然后单击**云服务器ECS分组**页签。

4.  在**云服务器ECS分组**页签右上角，单击**创建ECS分组**。

5.  在**新增ECS分组**对话框的**组名**文本框，输入分组名称，从**Region**列表，选择地域，添加需要加入当前分组的ECS实例，单击**确定**。

    **说明：** 只能将同一个地域下的ECS实例纳入同一个ECS分组。

    ![Create ECS Instances Group](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2214160161/p43700.png)


## 更多信息

同步ECS数据源后，您可以为该数据源创建监控任务。具体操作，请参见[配置数据源](/cn.zh-CN/自定义监控/创建监控任务/配置数据源.md)。

