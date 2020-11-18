---
title: SkyWalking8.2 + Mysql 8.0 安装教程
date: 2020-11-13 16:12:00
updated: 2020-11-13 16:12:00
type:
comments:
description: SkyWalking
keywords: SkyWalking
top_img: https://cdn.jsdelivr.net/gh/jerryc127/CDN@latest/Photo/index.jpg
cover: http://qiniu.lancaiwu.com/SkyWalking-12364.jpg
tag: SkyWalking
categories: Java
---
### 下载Msqyl 8.0  
下载地址 https://cdn.mysql.com//Downloads/MySQLInstaller/mysql-installer-community-8.0.22.0.msi

### SkyWalking 8.2 
下载地址 https://ftp.fau.de/apache/skywalking/8.2.0/apache-skywalking-apm-8.2.0.tar.gz

### 下载 Mysql8.0驱动 
* 下载地址 https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.21/mysql-connector-java-8.0.21.jar
* 将下载好的Mysql 8.0驱动移动到 **oap-libs**文件夹中

### 修改SkyWalking配置文件：
* **config/application.yml**文件
  修改**storage.selector** 修改为 **mysql**,默认的是 **h2** ,你也可以自己选择合适的存储介质
  修改为**mysql**存储后，也要修改对应的**mysql**配置，修改**store**下的**mysql**节点信息，其中连接url要增加时区**serverTimezone=Asia/Shanghai**,不然会报时区错误。
* 拷贝一份**agent文件夹**到与项目jar一起的地方，修改**agent/config/agent.config**文件。
  1、修改**agent.service_name**为实际名
  2、修改**agent.instance_name**名，每个实例都应该是唯一的。
  3、修改**collector.backend_service**修改为实际的backend所在的主机ip和端口

### 启动SkyWalking
* Windows: 点击bin文件夹下的**startup.bat**
* Linux： 运行bin文件夹下的**startup.sh**

### 在需要监控的jar包启动脚本添加如下命令
``` 
-javaagent:/xxx/agent/skywalking-agent.jar
```