# Description of alert rules

Prometheus Monitoring alert rules include Application Real-Time Monitoring Service \(ARMS\) alert rules, Kubernetes alert rules, MongoDB alert rules, MySQL alert rules, NGINX alert rules, and Redis alert rules.

## ARMS alert rules

|Name|Expression|Data collection time \(Unit: minutes\)|Trigger condition|
|----|----------|--------------------------------------|-----------------|
|PodCpu75|100 \* \(sum\(rate\(container\_cpu\_usage\_seconds\_total\[1m\]\)\) by \(pod\_name\) / sum\(label\_replace\(kube\_pod\_container\_resource\_limits\_cpu\_cores, "pod\_name", "$1", "pod", "\(.\*\)"\)\) by \(pod\_name\)\)\>75|7|The CPU utilization of a pod is greater than 75%.|
|PodMemory75|100 \* \(sum\(container\_memory\_working\_set\_bytes\) by \(pod\_name\) / sum\(label\_replace\(kube\_pod\_container\_resource\_limits\_memory\_bytes, "pod\_name", "$1", "pod", "\(.\*\)"\)\) by \(pod\_name\)\)\>75|5|The memory usage of a pod is greater than 75%.|
|pod\_status\_no\_running|sum \(kube\_pod\_status\_phase\{phase! ="Running"\}\) by \(pod,phase\)|5|A pod is not running.|
|PodMem4GbRestart|\(sum \(container\_memory\_working\_set\_bytes\{id! ="/"\}\)by \(pod\_name,container\_name\) /1024/1024/1024\)\>4|5|The memory of a pod is larger than 4 GB.|
|PodRestart|sum \(increase \(kube\_pod\_container\_status\_restarts\_total\{\}\[2m\]\)\) by \(namespace,pod\) \>0|5|A pod is restarted.|

## Kubernetes alert rules

|Name|Expression|Data collection time \(Unit: minutes\)|Trigger condition|
|----|----------|--------------------------------------|-----------------|
|KubeStateMetricsListErrors|\(sum\(rate\(kube\_state\_metrics\_list\_total\{job="kube-state-metrics",result="error"\}\[5m\]\)\) / sum\(rate\(kube\_state\_metrics\_list\_total\{job="kube-state-metrics"\}\[5m\]\)\)\) \> 0.01|15|An error occurs to a metric list.|
|KubeStateMetricsWatchErrors|\(sum\(rate\(kube\_state\_metrics\_watch\_total\{job="kube-state-metrics",result="error"\}\[5m\]\)\) / sum\(rate\(kube\_state\_metrics\_watch\_total\{job="kube-state-metrics"\}\[5m\]\)\)\) \> 0.01|15|An error occurs to Metric Watch.|
|NodeFilesystemAlmostOutOfSpace|\( node\_filesystem\_avail\_bytes\{job="node-exporter",fstype! =""\} / node\_filesystem\_size\_bytes\{job="node-exporter",fstype! =""\} \* 100 < 5 and node\_filesystem\_readonly\{job="node-exporter",fstype! =""\} == 0 \)|60|A node file system is running out of space.|
|NodeFilesystemSpaceFillingUp|\( node\_filesystem\_avail\_bytes\{job="node-exporter",fstype! =""\} / node\_filesystem\_size\_bytes\{job="node-exporter",fstype! =""\} \* 100 < 40 and predict\_linear\(node\_filesystem\_avail\_bytes\{job="node-exporter",fstype! =""\}\[6h\], 24\*60\*60\) < 0 and node\_filesystem\_readonly\{job="node-exporter",fstype! =""\} == 0 \)|60|A node file system is about to be fully occupied.|
|NodeFilesystemFilesFillingUp|\( node\_filesystem\_files\_free\{job="node-exporter",fstype! =""\} / node\_filesystem\_files\{job="node-exporter",fstype! =""\} \* 100 < 40 and predict\_linear\(node\_filesystem\_files\_free\{job="node-exporter",fstype! =""\}\[6h\], 24\*60\*60\) < 0 and node\_filesystem\_readonly\{job="node-exporter",fstype! =""\} == 0 \)|60|Files in a node file system are about to be fully occupied.|
|NodeFilesystemAlmostOutOfFiles|\( node\_filesystem\_files\_free\{job="node-exporter",fstype! =""\} / node\_filesystem\_files\{job="node-exporter",fstype! =""\} \* 100 < 3 and node\_filesystem\_readonly\{job="node-exporter",fstype! =""\} == 0 \)|60|Almost no files exist in a node file system.|
|NodeNetworkReceiveErrs|increase\(node\_network\_receive\_errs\_total\[2m\]\) \> 10|60|A network reception error occurs to a node.|
|NodeNetworkTransmitErrs|increase\(node\_network\_transmit\_errs\_total\[2m\]\) \> 10|60|A network transmission error occurs to a node.|
|NodeHighNumberConntrackEntriesUsed|\(node\_nf\_conntrack\_entries / node\_nf\_conntrack\_entries\_limit\) \> 0.75|None|A large number of conntrack entries are used.|
|NodeClockSkewDetected|\( node\_timex\_offset\_seconds \> 0.05 and deriv\(node\_timex\_offset\_seconds\[5m\]\) \>= 0 \) or \( node\_timex\_offset\_seconds < -0.05 and deriv\(node\_timex\_offset\_seconds\[5m\]\) <= 0 \)|10|Time deviation occurs.|
|NodeClockNotSynchronising|min\_over\_time\(node\_timex\_sync\_status\[5m\]\) == 0|10|Time inconsistency occurs.|
|KubePodCrashLooping|rate\(kube\_pod\_container\_status\_restarts\_total\{job="kube-state-metrics"\}\[15m\]\) \* 60 \* 5 \> 0|15|A loop crash occurs.|
|KubePodNotReady|sum by \(namespace, pod\) \(max by\(namespace, pod\) \(kube\_pod\_status\_phase\{job="kube-state-metrics", phase=~"Pending\|Unknown"\}\) \* on\(namespace, pod\) group\_left\(owner\_kind\) max by\(namespace, pod, owner\_kind\) \(kube\_pod\_owner\{owner\_kind! ="Job"\}\)\) \> 0|15|A pod is not ready.|
|KubeDeploymentGenerationMismatch|kube\_deployment\_status\_observed\_generation\{job="kube-state-metrics"\} ! = kube\_deployment\_metadata\_generation\{job="kube-state-metrics"\}|15|Deployment versions do not match.|
|KubeDeploymentReplicasMismatch|\( kube\_deployment\_spec\_replicas\{job="kube-state-metrics"\} ! = kube\_deployment\_status\_replicas\_available\{job="kube-state-metrics"\} \) and \( changes\(kube\_deployment\_status\_replicas\_updated\{job="kube-state-metrics"\}\[5m\]\) == 0 \)|15|Deployment replicas do not match.|
|KubeStatefulSetReplicasMismatch|\( kube\_statefulset\_status\_replicas\_ready\{job="kube-state-metrics"\} ! = kube\_statefulset\_status\_replicas\{job="kube-state-metrics"\} \) and \( changes\(kube\_statefulset\_status\_replicas\_updated\{job="kube-state-metrics"\}\[5m\]\) == 0 \)|15|State set replicas do not match.|
|KubeStatefulSetGenerationMismatch|kube\_statefulset\_status\_observed\_generation\{job="kube-state-metrics"\} ! = kube\_statefulset\_metadata\_generation\{job="kube-state-metrics"\}|15|State set versions do not match.|
|KubeStatefulSetUpdateNotRolledOut|max without \(revision\) \( kube\_statefulset\_status\_current\_revision\{job="kube-state-metrics"\} unless kube\_statefulset\_status\_update\_revision\{job="kube-state-metrics"\} \) \* \( kube\_statefulset\_replicas\{job="kube-state-metrics"\} ! = kube\_statefulset\_status\_replicas\_updated\{job="kube-state-metrics"\} \)|15|A state set update is not rolled out.|
|KubeDaemonSetRolloutStuck|kube\_daemonset\_status\_number\_ready\{job="kube-state-metrics"\} / kube\_daemonset\_status\_desired\_number\_scheduled\{job="kube-state-metrics"\} < 1.00|15|A DaemonSet rollout is stuck.|
|KubeContainerWaiting|sum by \(namespace, pod, container\) \(kube\_pod\_container\_status\_waiting\_reason\{job="kube-state-metrics"\}\) \> 0|60|A container is waiting.|
|KubeDaemonSetNotScheduled|kube\_daemonset\_status\_desired\_number\_scheduled\{job="kube-state-metrics"\} - kube\_daemonset\_status\_current\_number\_scheduled\{job="kube-state-metrics"\} \> 0|10|A DaemonSet is not scheduled.|
|KubeDaemonSetMisScheduled|kube\_daemonset\_status\_number\_misscheduled\{job="kube-state-metrics"\} \> 0|15|A DaemonSet is misscheduled.|
|KubeCronJobRunning|time\(\) - kube\_cronjob\_next\_schedule\_time\{job="kube-state-metrics"\} \> 3600|60|A cron job takes more than 1 hour to complete.|
|KubeJobCompletion|kube\_job\_spec\_completions\{job="kube-state-metrics"\} - kube\_job\_status\_succeeded\{job="kube-state-metrics"\} \> 0|60|A job is complete.|
|KubeJobFailed|kube\_job\_failed\{job="kube-state-metrics"\} \> 0|15|A job failed.|
|KubeHpaReplicasMismatch|\(kube\_hpa\_status\_desired\_replicas\{job="kube-state-metrics"\} ! = kube\_hpa\_status\_current\_replicas\{job="kube-state-metrics"\}\) and changes\(kube\_hpa\_status\_current\_replicas\[15m\]\) == 0|15|Host protected area \(HPA\) replicas do not match.|
|KubeHpaMaxedOut|kube\_hpa\_status\_current\_replicas\{job="kube-state-metrics"\} == kube\_hpa\_spec\_max\_replicas\{job="kube-state-metrics"\}|15|The maximum number of HPA replicas is reached.|
|KubeCPUOvercommit|sum\(namespace:kube\_pod\_container\_resource\_requests\_cpu\_cores:sum\{\}\) / sum\(kube\_node\_status\_allocatable\_cpu\_cores\) \> \(count\(kube\_node\_status\_allocatable\_cpu\_cores\)-1\) / count\(kube\_node\_status\_allocatable\_cpu\_cores\)|5|The CPU is overcommitted.|
|KubeMemoryOvercommit|sum\(namespace:kube\_pod\_container\_resource\_requests\_memory\_bytes:sum\{\}\) / sum\(kube\_node\_status\_allocatable\_memory\_bytes\) \> \(count\(kube\_node\_status\_allocatable\_memory\_bytes\)-1\) / count\(kube\_node\_status\_allocatable\_memory\_bytes\)|5|The storage is overcommitted.|
|KubeCPUQuotaOvercommit|sum\(kube\_resourcequota\{job="kube-state-metrics", type="hard", resource="cpu"\}\) / sum\(kube\_node\_status\_allocatable\_cpu\_cores\) \> 1.5|5|The CPU quota is overcommitted.|
|KubeMemoryQuotaOvercommit|sum\(kube\_resourcequota\{job="kube-state-metrics", type="hard", resource="memory"\}\) / sum\(kube\_node\_status\_allocatable\_memory\_bytes\{job="node-exporter"\}\) \> 1.5|5|The storage quota is overcommitted.|
|KubeQuotaExceeded|kube\_resourcequota\{job="kube-state-metrics", type="used"\} / ignoring\(instance, job, type\) \(kube\_resourcequota\{job="kube-state-metrics", type="hard"\} \> 0\) \> 0.90|15|The quota is exceeded.|
|CPUThrottlingHigh|sum\(increase\(container\_cpu\_cfs\_throttled\_periods\_total\{container! ="", \}\[5m\]\)\) by \(container, pod, namespace\) / sum\(increase\(container\_cpu\_cfs\_periods\_total\{\}\[5m\]\)\) by \(container, pod, namespace\) \> \( 25 / 100 \)|15|The CPU is overheated.|
|KubePersistentVolumeFillingUp|kubelet\_volume\_stats\_available\_bytes\{job="kubelet", metrics\_path="/metrics"\} / kubelet\_volume\_stats\_capacity\_bytes\{job="kubelet", metrics\_path="/metrics"\} < 0.03|1|The volume capacity is insufficient.|
|KubePersistentVolumeErrors|kube\_persistentvolume\_status\_phase\{phase=~"Failed\|Pending",job="kube-state-metrics"\} \> 0|5|An error occurs to the volume capacity.|
|KubeVersionMismatch|count\(count by \(gitVersion\) \(label\_replace\(kubernetes\_build\_info\{job! ~"kube-dns\|coredns"\},"gitVersion","$1","gitVersion","\(v\[0-9\]\*.\[ 0-9\]\*.\[ 0-9\]\*\). \*"\)\)\) \> 1|15|Versions do not match.|
|KubeClientErrors|\(sum\(rate\(rest\_client\_requests\_total\{code=~"5.."\}\[5m\]\)\) by \(instance, job\) / sum\(rate\(rest\_client\_requests\_total\[5m\]\)\) by \(instance, job\)\) \> 0.01|15|An error occurs to the client.|
|KubeAPIErrorBudgetBurn|sum\(apiserver\_request:burnrate1h\) \> \(14.40 \* 0.01000\) and sum\(apiserver\_request:burnrate5m\) \> \(14.40 \* 0.01000\)|2|Excessive API errors occur.|
|KubeAPILatencyHigh|\( cluster:apiserver\_request\_duration\_seconds:mean5m\{job="apiserver"\} \> on \(verb\) group\_left\(\) \( avg by \(verb\) \(cluster:apiserver\_request\_duration\_seconds:mean5m\{job="apiserver"\} \>= 0\) + 2\*stddev by \(verb\) \(cluster:apiserver\_request\_duration\_seconds:mean5m\{job="apiserver"\} \>= 0\) \) \) \> on \(verb\) group\_left\(\) 1.2 \* avg by \(verb\) \(cluster:apiserver\_request\_duration\_seconds:mean5m\{job="apiserver"\} \>= 0\) and on \(verb,resource\) cluster\_quantile:apiserver\_request\_duration\_seconds:histogram\_quantile\{job="apiserver",quantile="0.99"\} \> 1|5|The API latency is high.|
|KubeAPIErrorsHigh|sum\(rate\(apiserver\_request\_total\{job="apiserver",code=~"5.."\}\[5m\]\)\) by \(resource,subresource,verb\) / sum\(rate\(apiserver\_request\_total\{job="apiserver"\}\[5m\]\)\) by \(resource,subresource,verb\) \> 0.05|10|Excessive API errors occur.|
|KubeClientCertificateExpiration|apiserver\_client\_certificate\_expiration\_seconds\_count\{job="apiserver"\} \> 0 and on\(job\) histogram\_quantile\(0.01, sum by \(job, le\) \(rate\(apiserver\_client\_certificate\_expiration\_seconds\_bucket\{job="apiserver"\}\[5m\]\)\)\) < 604800|None|The client certificate expires.|
|AggregatedAPIErrors|sum by\(name, namespace\)\(increase\(aggregator\_unavailable\_apiservice\_count\[5m\]\)\) \> 2|None|An error occurs to the aggregated API.|
|AggregatedAPIDown|sum by\(name, namespace\)\(sum\_over\_time\(aggregator\_unavailable\_apiservice\[5m\]\)\) \> 0|5|The aggregated API is offline.|
|KubeAPIDown|absent\(up\{job="apiserver"\} == 1\)|15|An API operation is offline.|
|KubeNodeNotReady|kube\_node\_status\_condition\{job="kube-state-metrics",condition="Ready",status="true"\} == 0|15|A node is not ready.|
|KubeNodeUnreachable|kube\_node\_spec\_taint\{job="kube-state-metrics",key="node.kubernetes.io/unreachable",effect="NoSchedule"\} == 1|2|A node is unreachable.|
|KubeletTooManyPods|max\(max\(kubelet\_running\_pod\_count\{job="kubelet", metrics\_path="/metrics"\}\) by\(instance\) \* on\(instance\) group\_left\(node\) kubelet\_node\_name\{job="kubelet", metrics\_path="/metrics"\}\) by\(node\) / max\(kube\_node\_status\_capacity\_pods\{job="kube-state-metrics"\} ! = 1\) by\(node\) \> 0.95|15|Excessive pods exist.|
|KubeNodeReadinessFlapping|sum\(changes\(kube\_node\_status\_condition\{status="true",condition="Ready"\}\[15m\]\)\) by \(node\) \> 2|15|The readiness status changes frequently.|
|KubeletPlegDurationHigh|node\_quantile:kubelet\_pleg\_relist\_duration\_seconds:histogram\_quantile\{quantile="0.99"\} \>= 10|5|The pod lifecycle event generator \(PLEG\) lasts for an extended period of time.|
|KubeletPodStartUpLatencyHigh|histogram\_quantile\(0.99, sum\(rate\(kubelet\_pod\_worker\_duration\_seconds\_bucket\{job="kubelet", metrics\_path="/metrics"\}\[5m\]\)\) by \(instance, le\)\) \* on\(instance\) group\_left\(node\) kubelet\_node\_name\{job="kubelet", metrics\_path="/metrics"\} \> 60|15|The startup latency of a pod is high.|
|KubeletDown|absent\(up\{job="kubelet", metrics\_path="/metrics"\} == 1\)|15|The kubelet is offline.|
|KubeSchedulerDown|absent\(up\{job="kube-scheduler"\} == 1\)|15|The Kubernetes scheduler is offline.|
|KubeControllerManagerDown|absent\(up\{job="kube-controller-manager"\} == 1\)|15|The controller manager is offline.|
|TargetDown|100 \* \(count\(up == 0\) BY \(job, namespace, service\) / count\(up\) BY \(job, namespace, service\)\) \> 10|10|The target is offline.|
|NodeNetworkInterfaceFlapping|changes\(node\_network\_up\{job="node-exporter",device! ~"veth.+"\}\[2m\]\) \> 2|2|The network interface status changes frequently.|

## MongoDB alert rules

|Name|Expression|Data collection time \(Unit: minutes\)|Trigger condition|
|----|----------|--------------------------------------|-----------------|
|MongodbReplicationLag|avg\(mongodb\_replset\_member\_optime\_date\{state="PRIMARY"\}\) - avg\(mongodb\_replset\_member\_optime\_date\{state="SECONDARY"\}\) \> 10|5|The replication lantency is long.|
|MongodbReplicationHeadroom|\(avg\(mongodb\_replset\_oplog\_tail\_timestamp - mongodb\_replset\_oplog\_head\_timestamp\) - \(avg\(mongodb\_replset\_member\_optime\_date\{state="PRIMARY"\}\) - avg\(mongodb\_replset\_member\_optime\_date\{state="SECONDARY"\}\)\)\) <= 0|5|The replication margin is insufficient.|
|MongodbReplicationStatus3|mongodb\_replset\_member\_state == 3|5|The replication status is 3.|
|MongodbReplicationStatus6|mongodb\_replset\_member\_state == 6|5|The replication status is 6.|
|MongodbReplicationStatus8|mongodb\_replset\_member\_state == 8|5|The replication status is 8.|
|MongodbReplicationStatus10|mongodb\_replset\_member\_state == 10|5|The replication status is 10.|
|MongodbNumberCursorsOpen|mongodb\_metrics\_cursor\_open\{state="total\_open"\} \> 10000|5|Excessive cursors exist.|
|MongodbCursorsTimeouts|sum \(increase increase\(mongodb\_metrics\_cursor\_timed\_out\_total\[10m\]\) \> 100|5|The cursor times out.|
|MongodbTooManyConnections|mongodb\_connections\{state="current"\} \> 500|5|Excessive connections exist.|
|MongodbVirtualMemoryUsage|\(sum\(mongodb\_memory\{type="virtual"\}\) BY \(ip\) / sum\(mongodb\_memory\{type="mapped"\}\) BY \(ip\)\) \> 3|5|The virtual memory usage is high.|

## MySQL alert rules

|Name|Expression|Data collection time \(Unit: minutes\)|Trigger condition|
|----|----------|--------------------------------------|-----------------|
|MySQL is down|mysql\_up == 0|1|MySQL is offline.|
|open files high|mysql\_global\_status\_innodb\_num\_open\_files \> \(mysql\_global\_variables\_open\_files\_limit\) \* 0.75|1|Excessive files are opened.|
|Read buffer size is bigger than max. allowed packet size|mysql\_global\_variables\_read\_buffer\_size \> mysql\_global\_variables\_slave\_max\_allowed\_packet|1|The size of the read buffer exceeds the maximum allowed packet size.|
|Sort buffer possibly missconfigured|mysql\_global\_variables\_innodb\_sort\_buffer\_size <256\*1024 or mysql\_global\_variables\_read\_buffer\_size \> 4\*1024\*1024|1|A configuration error may exist in the sort buffer.|
|Thread stack size is too small|mysql\_global\_variables\_thread\_stack <196608|1|The thread stack size is small.|
|Used more than 80% of max connections limited|mysql\_global\_status\_max\_used\_connections \> mysql\_global\_variables\_max\_connections \* 0.8|1|The maximum connection rate of 80% is reached.|
|InnoDB Force Recovery is enabled|mysql\_global\_variables\_innodb\_force\_recovery ! = 0|1|Force recovery is enabled.|
|InnoDB Log File size is too small|mysql\_global\_variables\_innodb\_log\_file\_size < 16777216|1|The log file size is small.|
|InnoDB Flush Log at Transaction Commit|mysql\_global\_variables\_innodb\_flush\_log\_at\_trx\_commit ! = 1|1|Logs are refreshed when transactions are committed.|
|Table definition cache too small|mysql\_global\_status\_open\_table\_definitions \> mysql\_global\_variables\_table\_definition\_cache|1|The number of cached table definitions is small.|
|Table open cache too small|mysql\_global\_status\_open\_tables \>mysql\_global\_variables\_table\_open\_cache \* 99/100|1|The number of cached open tables is small.|
|Thread stack size is possibly too small|mysql\_global\_variables\_thread\_stack < 262144|1|The thread stack size may be small.|
|InnoDB Buffer Pool Instances is too small|mysql\_global\_variables\_innodb\_buffer\_pool\_instances == 1|1|The number of instances in the buffer pool is small.|
|InnoDB Plugin is enabled|mysql\_global\_variables\_ignore\_builtin\_innodb == 1|1|The plug-in is enabled.|
|Binary Log is disabled|mysql\_global\_variables\_log\_bin ! = 1|1|Binary logs are disabled.|
|Binlog Cache size too small|mysql\_global\_variables\_binlog\_cache\_size < 1048576|1|The cache size is small.|
|Binlog Statement Cache size too small|mysql\_global\_variables\_binlog\_stmt\_cache\_size <1048576 and mysql\_global\_variables\_binlog\_stmt\_cache\_size \> 0|1|The statement cache size is small.|
|Binlog Transaction Cache size too small|mysql\_global\_variables\_binlog\_cache\_size <1048576|1|The transaction cache size is small.|
|Sync Binlog is enabled|mysql\_global\_variables\_sync\_binlog == 1|1|Binary logs are enabled.|
|IO thread stopped|mysql\_slave\_status\_slave\_io\_running ! = 1|1|I/O threads are stopped.|
|SQL thread stopped|mysql\_slave\_status\_slave\_sql\_running == 0|1|SQL threads are stopped.|
|Mysql\_Too\_Many\_Connections|rate\(mysql\_global\_status\_threads\_connected\[5m\]\)\>200|5|Excessive connections exist.|
|Mysql\_Too\_Many\_slow\_queries|rate\(mysql\_global\_status\_slow\_queries\[5m\]\)\>3|5|Excessive slow queries exist.|
|Slave lagging behind Master|rate\(mysql\_slave\_status\_seconds\_behind\_master\[1m\]\) \>30|1|The primary node outperforms the secondary nodes.|
|Slave is NOT read only\(Please ignore this warning indicator.\)|mysql\_global\_variables\_read\_only ! = 0|1|Permissions on the secondary nodes are not read-only permissions.|

## NGINX alert rules

|Name|Expression|Data collection time \(Unit: minutes\)|Trigger condition|
|----|----------|--------------------------------------|-----------------|
|NginxHighHttp4xxErrorRate|sum\(rate\(nginx\_http\_requests\_total\{status=~"^4.."\}\[1m\]\)\) / sum\(rate\(nginx\_http\_requests\_total\[1m\]\)\) \* 100 \> 5|5|The rate of HTTP 4xx errors is high.|
|NginxHighHttp5xxErrorRate|sum\(rate\(nginx\_http\_requests\_total\{status=~"^5.."\}\[1m\]\)\) / sum\(rate\(nginx\_http\_requests\_total\[1m\]\)\) \* 100 \> 5|5|The rate of HTTP 5xx errors is high.|
|NginxLatencyHigh|histogram\_quantile\(0.99, sum\(rate\(nginx\_http\_request\_duration\_seconds\_bucket\[30m\]\)\) by \(host, node\)\) \> 10|5|The latency is high.|

## Redis alert rules

|Name|Expression|Data collection time \(Unit: minutes\)|Trigger condition|
|----|----------|--------------------------------------|-----------------|
|RedisDown|redis\_up == 0|5|Redis is offline.|
|RedisMissingMaster|count\(redis\_instance\_info\{role="master"\}\) == 0|5|The primary node is missing.|
|RedisTooManyMasters|count\(redis\_instance\_info\{role="master"\}\) \> 1|5|Excessive primary nodes exist.|
|RedisDisconnectedSlaves|count without \(instance, job\) \(redis\_connected\_slaves\) - sum without \(instance, job\) \(redis\_connected\_slaves\) - 1 \> 1|5|Secondary nodes are disconnected.|
|RedisReplicationBroken|delta\(redis\_connected\_slaves\[1m\]\) < 0|5|The replication is interrupted.|
|RedisClusterFlapping|changes\(redis\_connected\_slaves\[5m\]\) \> 2|5|Changes are detected in the connection to replica nodes.|
|RedisMissingBackup|time\(\) - redis\_rdb\_last\_save\_timestamp\_seconds \> 60 \* 60 \* 24|5|The backup is interrupted.|
|RedisOutOfMemory|redis\_memory\_used\_bytes / redis\_total\_system\_memory\_bytes \* 100 \> 90|5|The memory is insufficient.|
|RedisTooManyConnections|redis\_connected\_clients \> 100|5|Excessive connections exist.|
|RedisNotEnoughConnections|redis\_connected\_clients < 5|5|Connections are insufficient.|
|RedisRejectedConnections|increase\(redis\_rejected\_connections\_total\[1m\]\) \> 0|5|The connection is rejected.|

