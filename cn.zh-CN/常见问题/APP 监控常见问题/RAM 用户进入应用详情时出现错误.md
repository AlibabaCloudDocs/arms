# RAM 用户进入应用详情时出现错误 {#concept_2118453 .concept}

本文介绍了当 RAM 用户进入应用详情，出现如下错误“对不起，你没有权限执行操作”时的解决办法。

请参见

## 背景信息 {#section_1w1_wka_c5d .section}

用户创建的 APP 资源，都是该用户自己拥有的资源。默认情况下，用户对自己的资源拥有完整的操作权限。但在访问控制 RAM 的场景下，RAM 用户刚创建时没有权限去操作阿里云账号的资源，需要通过 RAM 授权的方式，给予 RAM 用户操作阿里云账号资源的权限。

## 操作步骤 {#section_nxs_q3f_0bm .section}

1.  登录 [RAM 控制台](https://ram.console.aliyun.com)。
2.  在左侧菜单栏中选择**权限管理** \> **权限策略管理**。
3.  在权限策略管理页面，单击左侧的**新建权限策略**。
4.  在新建自定义权限策略页面，填写策略名称和备注，配置模式选择**脚本配置**，输入策略内容后，单击**确定**。
    -   策略内容：只读权限

        ``` {#codeblock_7kz_0z8_ywl}
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": "emasha:View*",
                    "Resource": "*"
                }
            ],
            "Version": "1"
        }
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1681336/156810297359948_zh-CN.png)

    -   策略内容：管理权限

        ``` {#codeblock_y2h_a34_m7z}
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": "emasha:*",
                    "Resource": "*"
                }
            ],
            "Version": "1"
        }
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1681336/156810297459950_zh-CN.png)

5.  在左侧菜单栏中选择**人员管理** \> **用户**，跳转至用户页面。在页面左侧**用户登录名称**输入框中输入需要添加权限的用户名称，单击搜索图标搜索到用户后，在页面右侧的**操作**列单击**添加权限**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1681336/156810297459951_zh-CN.png)

6.  在**添加权限**弹出窗口中，在**选择权限**列表中选择**自定义权限策略**，并且在**权限策略**输入框中输入刚才添加的权限策略名称，单击搜索图标。从左侧**权限策略名称**列表选中搜索到的权限策略后，显示在右侧的**已选择**列表中，单击**确定**成功添加权限策略。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1681336/156810297459952_zh-CN.png)


