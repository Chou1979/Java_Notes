![[截屏2025-11-17 21.57.36.png]]

一、HDFS 存储集群启停

1. 执行启停脚本：
	一键启动 hdfs 集群
	Start-dfs. Sh
	
	一键关闭 hdfs 集群
	Stop-dfs. Sh

	如果遇到命令未找到的错误，表明环境变量未配置好，可以以绝对路径执行
	/export/server/hadoop/sbin/start-dfs. Sh
	/export/server/hadoop/sbin/stop-dfs. Sh

2.  启动完成后，可以在浏览器打开：
    http://node1:9870，即可查看到 hdfs 文件系统的管理网页。


二、YARN 资源调度集群启停

1. 启停脚本：

	一键启动 YARN 集群： $HADOOP_HOME/sbin/start-yarn. Sh
		会基于 yarn-site. Xml 中配置的 yarn. Resourcemanager. Hostname 决定在哪台机器上启动 resourcemanager；
		会基于 workers 文件配置的主机启动 NodeManager；
	一键停止 YARN 集群： $HADOOP_HOME/sbin/stop-yarn. Sh

	在当前机器，单独启动或停止进程：$HADOOP_HOME/bin/yarn --daemon    start|stop resourcemanager|nodemanager|proxyserver：Start 和 stop 决定启动和停止；
	可控制 resourcemanager、nodemanager、proxyserver 三种进程

	历史服务器启动和停止：$HADOOP_HOME/bin/mapred --daemon start|stop historyserver

2. 启动集群步骤：在 node 1 服务器，以 hadoop 用户执行
		1）首先执行：
		$HADOOP_HOME/sbin/start-yarn. Sh，一键启动所需的:
			ResourceManager
			NodeManager
			ProxyServer（代理服务器）
		2）其次执行：
		$HADOOP_HOME/bin/mapred --daemon start historyserver 
		启动: HistoryServer（历史服务器）

3. 启动完成后，可以在浏览器打开：
	http://node1:8088，可以看到YARN 的 WEB UI 页面并查看任务情况；


三、Hive 启动

	node 1 单机部署启动即可，会将任务分发到 hadoop 集群其它节点执行）：使用 hadoop 用户

	1.  启动元数据管理服务（必须启动，否则无法工作）
		前台启动：bin/hive --service metastore 
		后台启动：
		nohup bin/hive --service metastore >> logs/metastore. Log 2>&1 &

	2. HiveServer2服务：启动客户端，二选一（当前先选择 Hive Shell 方式）
		方式一：Hive Shell 方式（可以直接写 SQL）： bin/hive
		方式二：Hive ThriftServer 方式
		（不可直接写 SQL，需要外部客户端链接使用）： 
		执行以下脚本：
		前台启动：bin/hive --service hiveserver 2
		后台执行脚本：
		nohup bin/hive --service hiveserver2 >> logs/hiveserver2.log 2>&1 &

	3. 启动HiveServer2服务后，就可以用第三方客户端DBever来连接hive并操作sql
		如果已经建立HiveServer连接，即可在该连接下，新建sql脚本来执行sql语句；如果未建立连接，可以新增连接（localhost处填node1，username填hadoop，密码为空，填完测试一下连接）

	4. 也可以启动 Hive 内置的 beeline 客户端工具（命令行工具），来使用sql
		Beeline是JDBC的客户端，通过JDBC协议和Hiveserver2服务进行通信，协议的地址是：jdbc:hive2://node1:10000

[ hadoop@node1 ~]# /export/server/hive/bin/beeline 
执行结果：Beeline version 3.1.2 by Apache Hive
beeline> ! connect jdbc:hive2://node1:10000
执行结果：Connecting to jdbc:hive2://node1:10000
Enter username for jdbc:hive2://node1:10000: hadoop
Enter password for jdbc:hive2://node1:10000: 
执行结果：Connected to: Apache Hive (version 3.1.2)Driver: Hive JDBC (version 3.1.2)Transaction isolation: TRANSACTION_REPEATABLE_READ
启动成功，如下：
0: jdbc:hive2://node1:10000> 




