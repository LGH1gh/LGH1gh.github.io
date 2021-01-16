---
title: Hadoop安装与配置
date: 2021-01-16 22:20:44
categories: [BIG_DATA, DATA_PROCESSING]
tags: [hadoop, install, deploy]
---

### 环境

| 项目         | 版本                                       |
| ------------ | ------------------------------------------ |
| 操作系统     | macOS Big Sur Version 11.1                 |
| 集成开发环境 | IntelliJ IDEA 2020.3.1 (Community Edition) |
| Hadoop       | Hadoop 3.3.0                               |

## Hadoop安装与配置

### 安装Hadoop

```bash
brew install hadoop
```

### 配置Hadoop

**进入配置文件目录**

```bash
cd /usr/local/Cellar/hadoop/3.3.0/libexec/etc/hadoop
```

**修改配置文件**

   1. 修改`core-site.xml`

      ```xml
      <property>
      	<name>hadoop.tmp.dir</name>
      	<value>/Users/wangzeyuan/SourceCode/Dataset/tmp</value>
      	<description>A base for other temporary directories.</description>
      </property>
      <property>
      	<name>fs.default.name</name>
      	<value>hdfs://localhost:8088</value>
      </property>
      ```

   2. 修改`mapred-site.xml`

      ```xml
      <property>
      	<name>mapred.job.tracker</name>
      	<value>localhost:8089</value>
      </property>
      ```

   3. 修改`hdfs-site.xml `

      ```xml
      <property>
      	<name>dfs.replication</name>
      	<value>1</value>
      </property>
      <property>
      	<name>dfs.http.address</name>
      	<value>localhost:9870</value>
      </property>
      ```

### 启动Hadoop

```bash
# 进入系统命令文件
cd /usr/local/Cellar/hadoop/3.3.0/bin
# 格式化NameNode
./hdfs namenode --format

# 进入用户命令文件
cd /usr/local/Cellar/hadoop/3.3.0/sbin
# 启动Hadoop
./start-all.sh
```

### 访问Hadoop WebUI

访问网页：http://localhost:9870/

![Hadoop WebUI](/images/hadoop-webui.png)

## Idea配置

### 新建Java项目

![Idea New Project](/images/idea-new-project.png)

### 添加本地Hadoop依赖

找到hadoop中share文件夹下的包含jar文件的文件夹，将其放入build.gradle，并重新加载grade

```
dependencies {
    compile fileTree(dir:'/usr/local/Cellar/hadoop/3.3.0/libexec/share/hadoop/common',include:['*.jar'])
    compile fileTree(dir:'/usr/local/Cellar/hadoop/3.3.0/libexec/share/hadoop/client',include:['*.jar'])
    compile fileTree(dir:'/usr/local/Cellar/hadoop/3.3.0/libexec/share/hadoop/hdfs',include:['*.jar'])
    compile fileTree(dir:'/usr/local/Cellar/hadoop/3.3.0/libexec/share/hadoop/mapreduce',include:['*.jar'])
    compile fileTree(dir:'/usr/local/Cellar/hadoop/3.3.0/libexec/share/hadoop/tools',include:['*.jar'])
    compile fileTree(dir:'/usr/local/Cellar/hadoop/3.3.0/libexec/share/hadoop/yarn',include:['*.jar'])
    compile fileTree(dir:'/usr/local/Cellar/hadoop/3.3.0/libexec/share/hadoop/common/lib',include:['*.jar'])
}
```

![Idea Dependency](/images/idea-dependency-step1.png)