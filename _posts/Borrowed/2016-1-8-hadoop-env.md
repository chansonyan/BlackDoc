---
layout: post
title: Hadoop OS X 伪分布式环境配置
categories: hadoop
tags: hadoop
---

###  Hadoop OS X 伪分布式环境配置

---

####OS

OS X EI Capitan 10.11.2

####JAVA enviorment

    java version "1.8.0_60"
    Java(TM) SE Runtime Environment (build 1.8.0_60-b27)
    Java HotSpot(TM) 64-Bit Server VM (build 25.60-b23, mixed mode)

---

####开启SSH：

开启测试方法： `ssh localhost`

碰到的问题：

1. 权限不足  `system preference --> sharing`
2. 每次要求输入密码
    - `ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa` 生成一对私钥和公钥
    - `cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys` 将公钥追加到授权的key中去

---

####安装hadoop，并运行

下载hadoop，解压。版本：0.20.0


需配置的文件：

- __hadoop-env.sh__        配置相关依赖的环境变量
- __core-site.xml__        配置hdfs地址和端口号
- __mapred-site.xml__      配置 jobTracker的地址和端口号
- __hdfs-site.xml__        hdfs其他配置，伪分布式系统中默认备份方式要改为1，否则会报问题。

具体修改：

__hadoop-env.sh__

    export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_60.jdk/Contents/Home
    export HADOOP_HEAPSIZE=2000
    export HADOOP_OPTS=-server
    export HADOOP_INSTALL=/Users/zozhou/hadoop/hadoop-0.20.2
    export PATH=$PATH:$HADOOP_INSTALL/bin

__core-site.xml__

    <?xml version="1.0"?>
    <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>

    <!-- Put site-specific property overrides in this file. -->

    <configuration>
        <property>
            <name>fs.default.name</name>
            <value>hdfs://localhost:9000</value>
        </property>
    </configuration>

__mapped-site.xml__

    <?xml version="1.0"?>
    <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
    
    <!-- Put site-specific property overrides in this file. -->
    
    <configuration>
        <property>
            <name>mapred.job.tracker</name>
            <value>localhost:9001</value>
        </property>
    </configuration>

__hdfs-site.xml__

    <?xml version="1.0"?>
    <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
    
    <!-- Put site-specific property overrides in this file. -->
    
    <configuration>
        <property>
            <name>dfs.replication</name>
            <value>1</value>
        </property>
    </configuration>

---

配置完成后，需要__格式化namenode__

`hadoop NameNode -format`  (可能需要先将hadoop所在路径加入环境变量)

---
然后就可以通过运行bin目录下的各个脚本来使用hadoop了

如： start-all.sh, start-hdfs.sh 等

如果启动正常的话

可在`http://localhost:50030` 和 `http://localhost:50070` 分别看到map-reduce和hdfs的相关信息

---




