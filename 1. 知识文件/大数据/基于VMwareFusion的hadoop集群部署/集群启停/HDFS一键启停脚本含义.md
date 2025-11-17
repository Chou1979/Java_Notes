
Hadoop HDFS 组件内置了 HDFS 集群的一键启停脚本。
$HADOOP_HOME/sbin/start-dfs. Sh，一键启动 HDFS 集群
执行原理：
	1.  在执行此脚本的机器上，启动 SecondaryNameNode；
	2. 读取 core-site. Xml 内容（fs. DefaultFS 项），确认 NameNode 所在机器，启动 NameNode；
	3. 读取 workers 内容，确认 DataNode 所在机器，启动全部 DataNode；


$HADOOP_HOME/sbin/stop-dfs. Sh，一键关闭 HDFS 集群
执行原理：
1. 在执行此脚本的机器上，关闭 SecondaryNameNode；
2. 读取 core-site. Xml 内容（fs. DefaultFS 项），确认 NameNode 所在机器，关闭 NameNode；
3. 读取 workers 内容，确认 DataNode 所在机器，关闭全部 NameNode；
