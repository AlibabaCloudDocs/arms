# ARMS应用监控与其他商用和开源监控成本对比

本文将在ARMS应用监控中使用资源包的成本分别与按量付费费用、某常见APM产品年付费用、自行搭建开源Skywalking监控方案的物理资源成本进行了对比，结果表明在ARMS应用监控中使用资源包能够显著降低成本。

|监控节点数|资源包年付费用|占按量付费费用比例 ¹|占某APM产品费用比例 ²|占开源自建成本比例 ³|
|-----|-------|-----------|-------------|-----------|
|100|66,838|13.6%|9%|92%|
|300|174,000|11.8%|8%|70%|
|500|238,710|9.7%|7%|59%|

1.  占按量付费费用比例=在ARMS应用监控中使用资源包时的年付费用/采用按量付费方式时的年付费用×100%
2.  占某APM产品费用比例=在ARMS应用监控中使用资源包时的年付费用 / 某常见APM产品的年付费用×100%
3.  占开源自建成本比例=在ARMS应用监控中使用资源包时的年付费用 / 自行搭建开源Skywalking监控方案的物理资源成本×100%

|监控节点数|Collector节点数|ZooKeeper节点数|集群配置|费用|
|-----|------------|------------|----|--|
|100|3|1|-   一个单可用区
-   3节点
-   8核CPU
-   32G内存
-   894GB SSD硬盘
-   Elasticsearch

|4×2426+63,065=72,769|
|300|8|1|-   一个双可用区
-   6节点
-   16核CPU
-   64G内存
-   1788GB SSD硬盘
-   Elasticsearch

|9×2426+225,632=247,466|
|500|12|3|-   一个双可用区
-   10节点
-   16核CPU
-   64G内存
-   1788GB SSD硬盘
-   Elasticsearch

|15×2426+370,712=407,102|

