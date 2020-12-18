# 管理 ECS 数据源

ECS 实例是重要的日志产生来源，也是 ARMS 支持的自定义监控数据源。您可以授权 ARMS 将您阿里云账号下的 ECS 实例信息同步至 ARMS 控制台，为这些实例安装 Logtail 日志采集 Agent。您也可以为这些 ECS 实例分组以便管理。

执行同步 ECS 操作时必须使用阿里云账号或具备完整权限（包括全部读权限和写权限）的 RAM 用户，不可使用不具备完整权限的 RAM 用户，例如仅具备只读权限的 RAM 用户。

## 同步 ECS 实例

为了进行后续的管理，首先需要将您阿里云账号下的 ECS 实例信息同步至 ARMS 控制台。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏中选择**自定义监控数据源管理** \> **云服务器 ECS** 。

3.  在实例列表页面顶部选择目标地域，单击右上角的**同步ECS**。

    **说明：** 同步操作仅针对当前所选地域。

    ![ECS Datasource Regions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3880758751/p43559.png)

4.  如果您此前没有授权，则在提示框中单击**进入RAM进行授权**。

    ![Dialog Box Authorize ARMS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3880758751/p43560.png)

5.  在**云资源访问授权**页面选择所需权限，并单击**同意授权**。

    ![Dialog Box Cloud Resource Authorization](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3880758751/p43561.png)

    **说明：** 如果您使用的是不具备完整权限的 RAM 子账号，则无法授权。请使用阿里云主账号或具备完整权限的 RAM 用户授权。


## 检查 Logtail Agent 状态

ARMS 系统通过 Logtail Agent 日志收集客户端来收集 ECS 实例上的日志，故需为每台 ECS 实例安装 Logtail Agent。

安装前需要检查 Logtail Agent 状态，可以对单个 ECS 实例执行检查，也可以对选中的多个 ECS 实例执行批量检查。

-   对单个 ECS 实例执行检查：在云服务器ECS页签上，在目标 ECS 实例右侧**操作**列中单击**检查Agent**。
-   对多个 ECS 实例执行检查：在云服务器ECS上，勾选所有目标 ECS 实例，并单击页面底部的**批量检测Agent**

## 安装 Logtail Agent

若检查发现未安装 Logtail Agent，请按照以下步骤安装：

1.  下载 Agent。请根据 ECS 实例的网络环境和日志服务所在地域替换 <logtail.sh\_path\>。

    ```
    wget <logtail.sh_path> -O logtail.sh
    ```

    |网络类型|地域|下载地址|
    |----|--|----|
    |经典网络|华北 2（北京）|http://logtail-release-cn-beijing.oss-cn-beijing-internal.aliyuncs.com/linux64/logtail.sh|
    |华北 1（青岛）|http://logtail-release-cn-qingdao.oss-cn-qingdao-internal.aliyuncs.com/linux64/logtail.sh|
    |华东 1（杭州）|http://logtail-release-cn-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/linux64/logtail.sh|
    |华东 2（上海）|http://logtail-release-cn-shanghai.oss-cn-shanghai-internal.aliyuncs.com/linux64/logtail.sh|
    |华南 1（深圳）|http://logtail-release-cn-shenzhen.oss-cn-shenzhen-internal.aliyuncs.com/linux64/logtail.sh|
    |VPC|华北 2（北京）|http://logtail-release-bj.vpc100-oss-cn-beijing.aliyuncs.com/linux64/logtail.sh|
    |华东 1（杭州）|http://logtail-release.vpc100-oss-cn-hangzhou.aliyuncs.com/linux64/logtail.sh|
    |华东 2（上海）|http://logtail-release-sh.vpc100-oss-cn-shanghai.aliyuncs.com/linux64/logtail.sh|
    |华南 1（深圳）|http://logtail-release-sz.vpc100-oss-cn-shenzhen.aliyuncs.com/linux64/logtail.sh|
    |公网（自建 IDC 或其他云主机）|华北 2（北京）|http://logtail-release-cn-beijing.oss-cn-beijing.aliyuncs.com/linux64/logtail.sh|
    |华北 1（青岛）|http://logtail-release-cn-qingdao.oss-cn-qingdao.aliyuncs.com/linux64/logtail.sh|
    |华东 1（杭州）|http://logtail-release-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/linux64/logtail.sh|
    |华东 2（上海）|http://logtail-release-cn-shanghai.oss-cn-shanghai.aliyuncs.com/linux64/logtail.sh|
    |华南 1（深圳）|http://logtail-release-cn-shenzhen.oss-cn-shenzhen.aliyuncs.com/linux64/logtail.sh|

2.  执行授权操作。

    ```
    chmod 755 logtail.sh
    ```

3.  安装 Agent。请根据 ECS 实例的网络环境和日志服务所在地域替换 <region\_id\>。

    ```
    sudo ./logtail.sh install <region_id>
    ```

    |网络类型|地域|地域 ID|
    |----|--|-----|
    |经典网络|华北 2（北京）|cn-beijing|
    |华北 1（青岛）|cn-qingdao|
    |华东 1（杭州）|cn-hangzhou|
    |华东 2（上海）|cn-shanghai|
    |华南 1（深圳）|cn-shenzhen|
    |VPC|华北 2（北京）|cn\_beijing\_vpc|
    |华东 1（杭州）|cn\_hangzhou\_vpc|
    |华东 2（上海）|cn\_shanghai\_vpc|
    |华南 1（深圳）|cn\_shenzhen\_vpc|
    |公网（自建 IDC 或其他云主机）|华北 2（北京）|cn-beijing-internet|
    |华北 1（青岛）|cn-qingdao-internet|
    |华东 1（杭州）|cn-hangzhou-internet|
    |华东 2（上海）|cn-shanghai-internet|
    |华南 1（深圳）|cn-shenzhen-internet|

4.  创建配置文件。

    ```
    sudo touch /etc/ilogtail/users/1098370038733503
    ```


执行完上述步骤后，按照[检查 Logtail Agent 状态](#section_e1j_tpi_0tn)的说明操作。若 Agent 状态变为**已安装**则表示安装成功。

## 卸载 Logtail Agent

按照[1](#step_mo3_6ld_bqv)的说明下载 Logtail Agent，并在 Shell 环境下以管理员身份运行以下命令：

```
sudo sh logtail.sh uninstall
sudo rm -rf /etc/ilogtail/users/1098370038733503 
```

## 创建 ECS 分组

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在控制台左侧导航栏中选择**自定义监控数据源管理** \> **云服务器 ECS**，并单击**云服务器ECS分组**页签。

3.  在**云服务器ECS分组**页签单击右上角的**创建ECS分组**。

4.  在新增ECS分组对话框中，输入组名、选择地域（Region）、添加需要加入当前分组的 ECS 实例，单击**确定**。

    **说明：** 只能将同一个地域下的 ECS 实例纳入同一个 ECS 分组。

    ![Create ECS Instances Group](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3880758751/p43700.png)


## 查看 ECS 分组内的实例详情

在**云服务器ECS分组**页签，单击 ECS 分组的展开按钮，即可查看该分组内的 ECS 实例详细信息，如图所示。

![ECS分组详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3880758751/p43701.png)

您也可以在此页面将特定 ECS 实例从分组中移除。

## 编辑 ECS 分组

单击 ECS 分组的铅笔按钮，即可修改该 ECS 分组的信息。例如，您可以修改 ECS 分组名称，添加 ECS 实例到分组，或者将某个 ECS 实例从分组中移除。

![编辑ECS分组](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4880758751/p43704.png)

## 删除 ECS 分组

单击 ECS 分组的删除按钮，即可删除当前分组。

## 更多信息

