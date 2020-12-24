# JS错误诊断

ARMS前端监控的JS错误诊断功能可展示JS错误的基本信息和分布情况，以及回溯用户行为，帮助您快速定位错误位置。

## 功能入口

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。
2.  在左侧导航栏单击**前端监控**，在**前端监控**页面上单击应用名称。
3.  在左侧导航栏选择**应用** \> **JS错误诊断**。

## 查看错误总览

**错误总览**区域可展示选定时间段内的JS错误基本统计信息和趋势，包括以下指标：

-   **错误数**：选定时间段内的JS错误总数。
-   **JS错误率**：选定时间段内发生过错误的PV占总PV的比例。
-   **影响用户数**：JS错误影响到的用户数量和比例。

![应用层面的错误总览](../images/p187064.png "应用层面的错误总览")

在**错误总览**区域可执行以下操作：

-   将鼠标悬浮于曲线上，曲线拐点所对应时间点的错误数、错误率、影响用户数将显示在浮层中。
-   将鼠标悬浮于曲线拐点上，当鼠标显示为手形指针时单击拐点，可打开该时间点的**异常洞察**对话框。更多信息，请参见[查看异常洞察](#section_bji_tuz_4y3)。
-   在曲线图区域内按住鼠标左键并拖动鼠标来框选其中一段，即可放大查看该段曲线。单击右上角的**重置缩放**即可还原视图。

**说明：** 在JS错误诊断页面上，默认情况下**错误总览**区域显示的是应用层面的总览信息。在**页面错误率排行**或**页面错误率Top 5**页签单击**分析**后，展示的是对应页面的总览信息。

![页面层面的错误总览](../images/p187065.png "页面层面的错误总览")

## 查看异常洞察

**异常洞察**对话框可显示具体时间点的JS错误情况，包括以下指标：

-   **错误数**：对应时间点的JS错误总数。
-   **JS错误率**：对应时间点发生过错误的PV占总PV的比例。
-   **影响用户数**：JS错误影响到的用户数量和比例。
-   **高频错误Top 5**：对应时间点出现次数最多的前5种JS错误，包括ARMS捕捉到的JS错误内容、错误出现次数和影响用户数。
-   **页面错误率Top 5**：对应时间点JS错误率最高的前5个页面，包括出现过JS错误的页面名称、页面的JS错误率和页面访问量。

![JS错误异常洞察](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8188037061/p187070.png)

在**异常洞察**对话框可执行以下操作：

-   单击**高频错误Top 5**页签，然后单击**操作**列中的**诊断**，进入错误详情页面。
-   单击**页面错误率Top 5**页签，然后单击**操作**列中的**分析**，进入该页面的页面分析页面。

## 查看页面错误率排行

**页面错误率排行**页签可按JS错误率从高到低的顺序展示选定时间段内出现JS错误的页面，包括以下指标：

-   **页面**：出现过JS错误的页面。
-   **错误率**：选定时间段内在该页面发生过错误的PV占总PV的比例。
-   **访问量**：页面的访问量。

单击**操作**列中的**分析**，可查看该页面的错误总览视图。

## 查看高频错误

**高频错误**页签可按出现次数从多到少的顺序展示选定时间段内的JS错误，包括以下指标：

-   **错误信息**：ARMS捕捉到的JS错误内容。
-   **页面**：JS错误出现的页面。
-   **错误数**：JS错误出现的次数。
-   **影响用户数**：JS错误影响到的用户数量和比例。

单击**操作**列中的**诊断**，进入**错误详情**页签。

**说明：** 在JS错误诊断页面上，默认情况下**高频错误**页签显示的是应用层面的JS错误。在**页面错误率排行**或**页面错误率Top 5**页签单击**分析**后，**高频错误**页签展示的是对应页面上的JS错误。

## 查看错误详情

**错误详情**页签可展示以下信息：

-   **概要信息**
    -   **名称**
    -   **类型**
    -   **时间**（JS错误的发现时间）
    -   **设备**
    -   **操作系统**
    -   **浏览器**
    -   **IP**
    -   **地区**
    -   **行**
    -   **列**
    -   **URL**
    -   **文件**（出现JS错误的文件路径）
-   **堆栈信息**：与JS错误出现位置有关的信息。
-   **用户行为回溯**：回溯的用户行为信息，用于还原报错现场。

![JS错误详情页面](../images/p203704.png "JS错误详情页面")

在**错误详情**页签上可执行以下操作：

-   如需确定JS错误的准确出错位置，请在**堆栈信息**区域单击一条堆栈信息左侧的三角形图标展开该行，单击**选择Source Map**，然后在Source Map文件对话框中选择现有的Source Map文件或上传新的Source Map文件，最后单击**确定**。

    ![Select Source Map](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/db_source_map_select.png)

    ARMS将利用Source Map文件还原准确的JS错误位置。

    ![Stack Mapped](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/sc_bm_js_error_diag_details_stack_mapped.png)

-   如需查看用户行为轨迹，请查看[回溯用户行为](#sc_behavior)区域。
-   如需查看该错误的分布情况，请单击**错误分布**页签。


## 回溯用户行为

**错误详情**页签上的**用户行为回溯**区域展示用户的行为轨迹，辅助还原报错现场。

![Section Behavior](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0140458061/p60498.png)

## 查看错误分布

JS错误诊断页面的**错误分布**页签可展示具体JS错误的分布情况，统计维度包括：

-   **时间**：最近24小时和最近30天。
-   **浏览器**。
-   **操作系统**。
-   **设备**。
-   **地理**：在中国维度下按省、直辖市、自治区统计，在世界维度下按国家/地区统计。

![JS错误分布页面](../images/p203745.png "JS错误分布页面")

在**错误分布**页签上可执行以下操作：

-   在**时间分布**区域，将鼠标悬浮于曲线上，曲线拐点所对应时间点的错误数将显示在浮层中。

-   在**地理分布**区域的**中国**或**世界**页签上，单击右侧表格中的**错误数**列标题，可切换表格的排序顺序（从正序切换为倒序，或从倒序切换为正序）。

    ![JS错误分布-地理](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0140458061/p203750.png)


## 常见问题

-   如何开启或关闭用户行为回溯功能？

    该功能默认开启。如需关闭，请在config配置中添加SDK配置项behavior: false。SDK配置项的详细信息参见[SDK参考](/cn.zh-CN/前端监控/SDK参考.md)。

-   开启用户行为回溯后，调试过程中通过console.log打印出的信息会定位到ARMS的SDK代码bl.js中，而不是原代码中的位置，如何解决？

    ![Issue Before](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0140458061/p60499.png)

    造成这种现象的原因是ARMS通过重写console对象的log等方法来监控浏览器控制台打印的内容。解决方法为：

    -   方法一（推荐）：设置Chrome浏览器的黑盒（Blackboxing）。

        1.  打开Chrome浏览器，按Ctrl + Shift + I打开开发者工具面板，在设置菜单中单击**Settings**。

            ![Chrome Developer Mode Settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1140458061/p60501.png)

        2.  在**Settings**面板左侧单击**Blackboxing**，单击**Add pattern**，在**Pattern**文本框中输入/bl.\*\\.js$，并单击**Add**。

            ![Tab Blackboxing](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1140458061/p60502.png)

    -   方法二：使用SDK配置项behavior: false关闭用户行为回溯。

        ```
        <script>
            ! (function ( c , b, d, a ) {
                c [a] || ( c[a] = {});
                c [a].config = {
                    pid: "xxxxx",
                    imgUrl: "https://arms-retcode.aliyuncs.com/r.png?",
                    sendResource: true,
                    enableLinkTrace: true,
                    behavior: false
                };
                with(b) with(body) with(insertBefore(createElement("script"), firstChild)) setAttribute("crossorigin", "", src = d)
            })(window, document, "https://retcode.alicdn.com/retcode/bl.js", "__bl");
        </script>
        ```

    按照上述方法处理后，console.log打印出的信息即可定位到原代码中的位置。

    ![Issue After](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1140458061/p60500.png)


**相关文档**  


[SDK参考](/cn.zh-CN/前端监控/SDK参考.md)

