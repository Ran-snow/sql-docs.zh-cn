---
title: Apache Spark 和 Apache Hadoop 配置属性
titleSuffix: SQL Server big data clusters
description: 有关 Apache Spark 和 Apache Hadoop (HDFS) 的配置属性的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ecb7fd295eded45995941c8a32e0519f10c8b78b
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196106"
---
# <a name="apache-spark--apache-hadoop-hdfs-configuration-properties"></a>Apache Spark 和 Apache Hadoop (HDFS) 配置属性

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

为了在大数据群集中配置 Apache Spark 和 Apache Hadoop，需要在部署时修改群集配置文件 (bdc.json)。

## <a name="supported-configurations"></a>支持的配置
大数据群集使用与各自的开源项目相同的默认配置值。
可以在关联的 Apache 文档网站上找到每个配置的所有可行配置和默认值：
- Apache Spark： https://spark.apache.org/docs/latest/configuration.html
- Apache Hadoop：
  - HDFS HDFS 站点： https://hadoop.apache.org/docs/r2.7.1/hadoop-project-dist/hadoop-hdfs/hdfs-default.xml
  - HDFS 核心站点： https://hadoop.apache.org/docs/r2.8.0/hadoop-project-dist/hadoop-common/core-default.xml  
  - Yarn： https://hadoop.apache.org/docs/r3.1.1/hadoop-yarn/hadoop-yarn-site/ResourceModel.html
- Hive： https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties#ConfigurationProperties-MetaStore
- Livy： https://github.com/cloudera/livy/blob/master/conf/livy.conf.template
- Apache Knox 网关： https://knox.apache.org/books/knox-0-14-0/user-guide.html#Gateway+Details

> [!NOTE]
> 可以更改某些配置设置的默认设置。 下面的 JSON 列出了这些设置及其默认值。 仍可以更改这些设置。 对于 JSON 中未列出的设置，请参考上面的链接。

> [!NOTE]
> 若要在存储池中包含 Spark，请在 `spec.resources.storage-0.spec.settings.spark` 的 `bdc.json` 配置文件中设置布尔值 `includeSpark`。 有关说明，请参阅[在大数据群集中配置 Apache Spark 和 Apache Hadoop](configure-spark-hdfs.md)。


###  <a name="big-data-clusters-specific-default-configurations"></a>大数据群集特定的默认配置
JSON 中列出的设置是 BDC 特定的默认设置。 如果需要，可以在部署时进行修改。 这里列出了这些设置，因为它们不同于各自的项目默认配置。

```json
{
  "hdfs": {
    "hdfs-site.dfs.replication": "2",
    "hdfs-site.dfs.ls.limit": "500",
    "hdfs-site.dfs.namenode.provided.enabled": "true",
    "hdfs-site.dfs.datanode.provided.enabled": "true",
    "hdfs-site.dfs.datanode.provided.volume.lazy.load": "true",
    "hdfs-site.dfs.provided.aliasmap.inmemory.enabled": "true",
    "hdfs-site.dfs.provided.aliasmap.class": "org.apache.hadoop.hdfs.server.common.blockaliasmap.impl.InMemoryLevelDBAliasMapClient",
    "hdfs-site.dfs.namenode.provided.aliasmap.class": "org.apache.hadoop.hdfs.server.common.blockaliasmap.impl.NamenodeInMemoryAliasMapClient",
    "hdfs-site.dfs.provided.aliasmap.load.retries": "10",
    "hdfs-site.dfs.provided.aliasmap.inmemory.batch-size": "1000",
    "hdfs-site.dfs.datanode.provided.volume.readthrough": "true",
    "hdfs-site.dfs.provided.overreplication.factor": "1",
    "hdfs-site.dfs.provided.cache.capacity.fraction": "0.01",
    "hdfs-site.dfs.provided.cache.capacity.mount": "true",

    "hdfs-env.HDFS_NAMENODE_OPTS": "-Dhadoop.security.logger=INFO,RFAS -Xmx2g",
    "hdfs-env.HDFS_DATANODE_OPTS": "-Dhadoop.security.logger=ERROR,RFAS -Xmx2g",
    "hdfs-env.HDFS_ZKFC_OPTS": "-Xmx1g",
    "hdfs-env.HDFS_JOURNALNODE_OPTS": "-Xmx2g",
    "hdfs-env.HDFS_AUDIT_LOGGER": "INFO,RFAAUDIT",

    "core-site.hadoop.security.group.mapping.ldap.search.group.hierarchy.levels": "10",
    "core-site.fs.permissions.umask-mode": "077",
    "core-site.hadoop.security.kms.client.failover.max.retries": "20",

    "kms-site.hadoop.security.kms.encrypted.key.cache.size": "500",

    "zoo-cfg.tickTime": "2000",
    "zoo-cfg.initLimit": "10",
    "zoo-cfg.syncLimit": "5",
    "zoo-cfg.maxClientCnxns": "60",
    "zoo-cfg.minSessionTimeout": "4000",
    "zoo-cfg.maxSessionTimeout": "40000",
    "zoo-cfg.autopurge.snapRetainCount": "3",
    "zoo-cfg.autopurge.purgeInterval": "0",

    "zookeeper-java-env.JVMFLAGS": "-Xmx1G -Xms1G",
    
    "zookeeper-log4j-properties.zookeeper.console.threshold": "INFO"
  },
  "spark": {
    "capacity-scheduler.yarn.scheduler.capacity.maximum-applications": "10000",
    "capacity-scheduler.yarn.scheduler.capacity.resource-calculator": "org.apache.hadoop.yarn.util.resource.DominantResourceCalculator",
    "capacity-scheduler.yarn.scheduler.capacity.root.queues": "default",
    "capacity-scheduler.yarn.scheduler.capacity.root.default.capacity": "100",
    "capacity-scheduler.yarn.scheduler.capacity.root.default.user-limit-factor": "1",
    "capacity-scheduler.yarn.scheduler.capacity.root.default.maximum-capacity": "100",
    "capacity-scheduler.yarn.scheduler.capacity.root.default.state": "RUNNING",
    "capacity-scheduler.yarn.scheduler.capacity.root.default.maximum-application-lifetime": "-1",
    "capacity-scheduler.yarn.scheduler.capacity.root.default.default-application-lifetime": "-1",
    "capacity-scheduler.yarn.scheduler.capacity.node-locality-delay": "40",
    "capacity-scheduler.yarn.scheduler.capacity.rack-locality-additional-delay": "-1",

    "yarn-env.YARN_RESOURCEMANAGER_HEAPSIZE": "2048",
    "yarn-env.YARN_NODEMANAGER_HEAPSIZE": "2048",

    "mapred-env.HADOOP_JOB_HISTORYSERVER_HEAPSIZE": "2048",

    "hive-env.HADOOP_HEAPSIZE": "2048",

    "livy-conf.livy.server.session.timeout-check": "true",
    "livy-conf.livy.server.session.timeout-check.skip-busy": "true",
    "livy-conf.livy.server.session.timeout": "2h",
    "livy-conf.livy.server.yarn.poll-interval": "500ms",
    "livy-conf.livy.rsc.jars": "local:/opt/livy/rsc-jars/livy-api.jar,local:/opt/livy/rsc-jars/livy-rsc.jar,local:/opt/livy/rsc-jars/netty-all.jar",
    "livy-conf.livy.repl.jars": "local:/opt/livy/repl_2.11-jars/livy-core.jar,local:/opt/livy/repl_2.11-jars/livy-repl.jar,local:/opt/livy/repl_2.11-jars/commons-codec.jar",
    "livy-conf.livy.rsc.sparkr.package": "hdfs:///system/livy/sparkr.zip",

    "livy-env.LIVY_SERVER_JAVA_OPTS": "-Xmx2g",

    "spark-defaults-conf.spark.r.backendConnectionTimeout": "86400",
    "spark-defaults-conf.spark.pyspark.python": "python3",
    "spark-defaults-conf.spark.yarn.jars": "local:/opt/spark/jars/*",

    "spark-history-server-conf.spark.history.fs.cleaner.maxAge": "7d",
    "spark-history-server-conf.spark.history.fs.cleaner.interval": "12h",

    "spark-env.SPARK_DAEMON_MEMORY": "2g",
    "spark-env.PYSPARK_ARCHIVES_PATH": "local:/opt/spark/python/lib/pyspark.zip,local:/opt/spark/python/lib/py4j-0.10.7-src.zip",

    "yarn-site.yarn.log-aggregation.retain-seconds": "604800",
    "yarn-site.yarn.nodemanager.log-aggregation.compression-type": "gz",
    "yarn-site.yarn.nodemanager.log-aggregation.roll-monitoring-interval-seconds": "3600",
    "yarn-site.yarn.scheduler.minimum-allocation-mb": "512",
    "yarn-site.yarn.scheduler.minimum-allocation-vcores": "1",
    "yarn-site.yarn.nm.liveness-monitor.expiry-interval-ms": "180000",
    "yarn-site.yarn.nodemanager.container-executor.class": "org.apache.hadoop.yarn.server.nodemanager.LinuxContainerExecutor"
  },
  "gateway": {
    "gateway-site.gateway.httpclient.socketTimeout": "90s",
    "gateway-site.sun.security.krb5.debug": "false",
    "knox-env.KNOX_GATEWAY_MEM_OPTS": "-Xmx2g"
  }
}
```

以下部分列出了不支持的配置。

## <a name="unsupported-spark-configurations"></a>不支持的 `spark` 配置

以下 `spark` 配置不受支持，并且无法在大数据群集的上下文中进行更改。

| 类别  | 子类别               | 文件                       | 不支持的配置                                              |
|-----------|----------------------------|----------------------------|-------------------------------------------------------------------------|
|           | yarn-site                  | yarn-site.xml              | yarn.log-aggregation-enable                                             |
|           |                            |                            | yarn.log.server.url                                                     |
|           |                            |                            | yarn.nodemanager.pmem-check-enabled                                     |
|           |                            |                            | yarn.nodemanager.vmem-check-enabled                                     |
|           |                            |                            | yarn.nodemanager.aux-services                                           |
|           |                            |                            | yarn.resourcemanager.address                                            |
|           |                            |                            | yarn.nodemanager.address                                                |
|           |                            |                            | yarn.client.failover-no-ha-proxy-provider                               |
|           |                            |                            | yarn.client.failover-proxy-provider                                     |
|           |                            |                            | yarn.http.policy                                                        |
|           |                            |                            | yarn.nodemanager.linux-container-executor.secure-mode.use-pool-user     |
|           |                            |                            | yarn.nodemanager.linux-container-executor.secure-mode.pool-user-prefix  |
|           |                            |                            | yarn.nodemanager.linux-container-executor.nonsecure-mode.local-user     |
|           |                            |                            | yarn.acl.enable                                                         |
|           |                            |                            | yarn.admin.acl                                                          |
|           |                            |                            | yarn.resourcemanager.hostname                                           |
|           |                            |                            | yarn.resourcemanager.principal                                          |
|           |                            |                            | yarn.resourcemanager.keytab                                             |
|           |                            |                            | yarn.resourcemanager.webapp.spnego-keytab-file                          |
|           |                            |                            | yarn.resourcemanager.webapp.spnego-principal                            |
|           |                            |                            | yarn.nodemanager.principal                                              |
|           |                            |                            | yarn.nodemanager.keytab                                                 |
|           |                            |                            | yarn.nodemanager.webapp.spnego-keytab-file                              |
|           |                            |                            | yarn.nodemanager.webapp.spnego-principal                                |
|           |                            |                            | yarn.resourcemanager.ha.enabled                                         |
|           |                            |                            | yarn.resourcemanager.cluster-id                                         |
|           |                            |                            | yarn.resourcemanager.zk-address                                         |
|           |                            |                            | yarn.resourcemanager.ha.rm-ids                                          |
|           |                            |                            | yarn.resourcemanager.hostname.*                                         |
|           | capacity-scheduler         | capacity-scheduler.xml     | yarn.scheduler.capacity.root.acl_submit_applications                    |
|           |                            |                            | yarn.scheduler.capacity.root.acl_administer_queue                       |
|           |                            |                            | yarn.scheduler.capacity.root.default.acl_application_max_priority       |
|           | yarn-env                   | yarn-env.sh                |                                                                         |
|           | spark-defaults-conf        | spark-defaults.conf        | spark.yarn.archive                                                      |
|           |                            |                            | spark.yarn.historyServer.address                                        |
|           |                            |                            | spark.eventLog.enabled                                                  |
|           |                            |                            | spark.eventLog.dir                                                      |
|           |                            |                            | spark.sql.warehouse.dir                                                 |
|           |                            |                            | spark.sql.hive.metastore.version                                        |
|           |                            |                            | spark.sql.hive.metastore.jars                                           |
|           |                            |                            | spark.extraListeners                                                    |
|           |                            |                            | spark.metrics.conf                                                      |
|           |                            |                            | spark.ssl.enabled                                                       |
|           |                            |                            | spark.authenticate                                                      |
|           |                            |                            | spark.network.crypto.enabled                                            |
|           |                            |                            | spark.ssl.keyStore                                                      |
|           |                            |                            | spark.ssl.keyStorePassword  
|           |                            |                            | spark.ui.enabled                                                        |
|           | spark-env                  | spark-env.sh               | SPARK_NO_DAEMONIZE                                                      |
|           |                            |                            | SPARK_DIST_CLASSPATH                                                    |
|           | spark-history-server-conf  | spark-history-server.conf  | spark.history.fs.logDirectory                                           |
|           |                            |                            | spark.ui.proxyBase                                                      |
|           |                            |                            | spark.history.fs.cleaner.enabled                                        |
|           |                            |                            | spark.ssl.enabled                                                       |
|           |                            |                            | spark.authenticate                                                      |
|           |                            |                            | spark.network.crypto.enabled                                            |
|           |                            |                            | spark.ssl.keyStore                                                      |
|           |                            |                            | spark.ssl.keyStorePassword                                              |
|           |                            |                            | spark.history.kerberos.enabled                                          |
|           |                            |                            | spark.history.kerberos.principal                                        |
|           |                            |                            | spark.history.kerberos.keytab                                           |
|           |                            |                            | spark.ui.filters                                                        |
|           |                            |                            | spark.acls.enable                                                       |
|           |                            |                            | spark.history.ui.acls.enable                                            |
|           |                            |                            | spark.history.ui.admin.acls                                             |
|           |                            |                            | spark.history.ui.admin.acls.groups                                      |
|           | livy-conf                  | livy.conf                  | livy.keystore                                                           |
|           |                            |                            | livy.keystore.password                                                  |
|           |                            |                            | livy.spark.master                                                       |
|           |                            |                            | livy.spark.deploy-mode                                                  |
|           |                            |                            | livy.rsc.jars                                                           |
|           |                            |                            | livy.repl.jars                                                          |
|           |                            |                            | livy.rsc.pyspark.archives                                               |
|           |                            |                            | livy.rsc.sparkr.package                                                 |
|           |                            |                            | livy.repl.enable-hive-context                                           |
|           |                            |                            | livy.superusers                                                         |
|           |                            |                            | livy.server.auth.type                                                   |
|           |                            |                            | livy.server.launch.kerberos.keytab                                      |
|           |                            |                            | livy.server.launch.kerberos.principal                                   |
|           |                            |                            | livy.server.auth.kerberos.principal                                     |
|           |                            |                            | livy.server.auth.kerberos.keytab                                        |
|           |                            |                            | livy.impersonation.enabled                                              |
|           |                            |                            | livy.server.access-control.enabled                                      |
|           |                            |                            | livy.server.access-control.*                                            |
|           | livy-env                   | livy-env.sh                |                                                                         |
|           | hive-site                  | hive-site.xml              | javax.jdo.option.ConnectionURL                                          |
|           |                            |                            | javax.jdo.option.ConnectionDriverName                                   |
|           |                            |                            | javax.jdo.option.ConnectionUserName                                     |
|           |                            |                            | javax.jdo.option.ConnectionPassword                                     |
|           |                            |                            | hive.metastore.uris                                                     |
|           |                            |                            | hive.metastore.pre.event.listeners                                      |
|           |                            |                            | hive.security.authorization.enabled                                     |
|           |                            |                            | hive.security.metastore.authenticator.manager                           |
|           |                            |                            | hive.security.metastore.authorization.manager                           |
|           |                            |                            | hive.metastore.use.SSL                                                  |
|           |                            |                            | hive.metastore.keystore.path                                            |
|           |                            |                            | hive.metastore.keystore.password                                        |
|           |                            |                            | hive.metastore.truststore.path                                          |
|           |                            |                            | hive.metastore.truststore.password                                      |
|           |                            |                            | hive.metastore.kerberos.keytab.file                                     |
|           |                            |                            | hive.metastore.kerberos.principal                                       |
|           |                            |                            | hive.metastore.sasl.enabled                                             |
|           |                            |                            | hive.metastore.execute.setugi                                           |
|           |                            |                            | hive.cluster.delegation.token.store.class                               |
|           | hive-env                   | hive-env.sh                

## <a name="unsupported-hdfs-configurations"></a>不支持的 `hdfs` 配置

以下 `hdfs` 配置不受支持，并且无法在大数据群集的上下文中进行更改。

| 类别  | 子类别               | 文件                       | 不支持的配置                                              |
|-----------|----------------------------|----------------------------|-------------------------------------------------------------------------|
|          | core-site                   | core-site.xml                 | fs.defaultFS                                          |
|          |                             |                               | ha.zookeeper.quorum                                   |
|          |                             |                               | hadoop.tmp.dir                                        |
|          |                             |                               | hadoop.rpc.protection                                 |
|          |                             |                               | hadoop.security.auth_to_local                         |
|          |                             |                               | hadoop.security.authentication                        |
|          |                             |                               | hadoop.security.authorization                         |
|          |                             |                               | hadoop.http.authentication.simple.anonymous.allowed   |
|          |                             |                               | hadoop.http.authentication.type                       |
|          |                             |                               | hadoop.http.authentication.kerberos.principal         |
|          |                             |                               | hadoop.http.authentication.kerberos.keytab            |
|          |                             |                               | hadoop.http.filter.initializers                       |
|          |                             |                               | hadoop.security.group.mapping.*                       |                               |
|          |                             |                               | hadoop.security.key.provider.path                     |                               |
|          | mapred-env                  | mapred-env.sh                 |                                                       |
|          | hdfs-site                   | hdfs-site.xml                 | dfs.namenode.name.dir                                 |
|          |                             |                               | dfs.datanode.data.dir                                 |
|          |                             |                               | dfs.namenode.acls.enabled                             |
|          |                             |                               | dfs.namenode.datanode.registration.ip-hostname-check  |
|          |                             |                               | dfs.client.retry.policy.enabled                       |
|          |                             |                               | dfs.permissions.enabled                               |
|          |                             |                               | dfs.nameservices                                      |
|          |                             |                               | dfs.ha.namenodes.nmnode-0                             |
|          |                             |                               | dfs.namenode.rpc-address.nmnode-0.*                   |
|          |                             |                               | dfs.namenode.shared.edits.dir                         |
|          |                             |                               | dfs.ha.automatic-failover.enabled                     |
|          |                             |                               | dfs.ha.fencing.methods                                |
|          |                             |                               | dfs.journalnode.edits.dir                             |
|          |                             |                               | dfs.client.failover.proxy.provider.nmnode-0           |
|          |                             |                               | dfs.namenode.http-address                             |
|          |                             |                               | dfs.namenode.httpS-address                            |
|          |                             |                               | dfs.http.policy                                       |
|          |                             |                               | dfs.encrypt.data.transfer                             |
|          |                             |                               | dfs.block.access.token.enable                         |
|          |                             |                               | dfs.data.transfer.protection                          |
|          |                             |                               | dfs.encrypt.data.transfer.cipher.suites               |
|          |                             |                               | dfs.https.port                                        |
|          |                             |                               | dfs.namenode.keytab.file                              |
|          |                             |                               | dfs.namenode.kerberos.principal                       |
|          |                             |                               | dfs.namenode.kerberos.internal.spnego.principal       |
|          |                             |                               | dfs.datanode.data.dir.perm                            |
|          |                             |                               | dfs.datanode.address                                  |
|          |                             |                               | dfs.datanode.http.address                             |
|          |                             |                               | dfs.datanode.ipc.address                              |
|          |                             |                               | dfs.datanode.https.address                            |
|          |                             |                               | dfs.datanode.keytab.file                              |
|          |                             |                               | dfs.datanode.kerberos.principal                       |
|          |                             |                               | dfs.journalnode.keytab.file                           |
|          |                             |                               | dfs.journalnode.kerberos.principal                    |
|          |                             |                               | dfs.journalnode.kerberos.internal.spnego.principal    |
|          |                             |                               | dfs.web.authentication.kerberos.keytab                |
|          |                             |                               | dfs.web.authentication.kerberos.principal             |
|          |                             |                               | dfs.webhdfs.enabled                                   |
|          |                             |                               | dfs.permissions.superusergroup                        |
|          | hdfs-env                    | hdfs-env.sh                   | HADOOP_HEAPSIZE_MAX                                   |
|          | zoo-cfg                     | zoo.cfg                       | secureClientPort                                      |
|          |                             |                               | clientPort                                            |
|          |                             |                               | dataDir                                               |
|          |                             |                               | dataLogDir                                            |
|          |                             |                               | 4lw.commands.whitelist                                |
|          | zookeeper-java-env          | java.env                      | ZK_LOG_DIR                                            |
|          |                             |                               | SERVER_JVMFLAGS                                       |
|          | zookeeper-log4j-properties  | log4j.properties (zookeeper)  | log4j.rootLogger                                      |
|          |                             |                               | log4j.appender.CONSOLE.*                              |

## <a name="unsupported-gateway-configurations"></a>不支持的 `gateway` 配置

以下 `gateway` 配置不受支持，并且无法在大数据群集的上下文中进行更改。

| 类别  | 子类别               | 文件                       | 不支持的配置                                              |
|-----------|----------------------------|----------------------------|-------------------------------------------------------------------------|
|          | gateway-site                | gateway-site.xml              | gateway.port                                          |
|          |                             |                               | gateway.path                                          |
|          |                             |                               | gateway.gateway.conf.dir                              |
|          |                             |                               | gateway.hadoop.kerberos.secured                       |
|          |                             |                               | java.security.krb5.conf                               |
|          |                             |                               | java.security.auth.login.config                       |
|          |                             |                               | gateway.websocket.feature.enabled                     |
|          |                             |                               | gateway.scope.cookies.feature.enabled                 |
|          |                             |                               | ssl.exclude.protocols                                 |
|          |                             |                               | ssl.include.ciphers                                   |

## <a name="next-steps"></a>后续步骤

[在大数据群集中配置 Apache Spark 和 Apache Hadoop](configure-spark-hdfs.md)
