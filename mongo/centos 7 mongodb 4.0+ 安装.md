[TOC]

## 1、下载

```bash
# 下载
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-4.0.24.tgz    
# 新建目录
mkdir -p /usr/local/mongodb/ 
# 解压
tar -zxvf mongodb-linux-x86_64-4.0.24.tgz -C /usr/local/mongodb/                                   
```

## 2、配置

### 2.1  配置mongo.conf

```bash
vim /etc/mongo.conf
```

```ini
# mongo.conf文件内容
dbpath = /var/lib/mongo/
port = 27017
fork = true
#auth = true
logpath = /var/log/mongo/mongo.log
logappend = true
bind_ip = 0.0.0.0
```

### 2.2  创建dbpath和logpath

```bash
mkdir -p /var/lib/mongo/
mkdir -p /var/log/mongo/
```

### 2.3  配置环境

将下述内容写入到/etc/profile

```bash
vim /etc/profile
```

```bash
export PATH=/usr/local/mongodb/mongodb-linux-x86_64-4.0.24/bin:$PATH
```

```bash
source /etc/profile
```

### 2.4  启动命令配置start.sh

```bash
#!/bin/bash

mongod -f /etc/mongo.conf
```

### 2.5  停止命令配置stop.sh

```bash
#!/bin/bash

mongod -f /etc/mongo.conf --shutdown
```

```bash
chmod 777 start.sh 
chmod 777 stop.sh 
```

## 3  启动|停止

### 3.1  启动

```bash
./start.sh
tail -f /var/log/mongo/mongo.log
```

### 3.2  停止

```bash
./stop.sh
```

### 3.3 连接

#### 本机命令连接

```bash
[root]# mongo
MongoDB shell version v4.0.24
connecting to: mongodb://127.0.0.1:27017/?gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("689ba2b6-2165-4c1c-a12d-6635f13d36fb") }
MongoDB server version: 4.0.24
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
        http://docs.mongodb.org/
Questions? Try the support group
        http://groups.google.com/group/mongodb-user
Server has startup warnings: 
2021-06-02T04:12:17.903-0400 I CONTROL  [initandlisten] 
2021-06-02T04:12:17.903-0400 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
2021-06-02T04:12:17.903-0400 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
2021-06-02T04:12:17.903-0400 I CONTROL  [initandlisten] ** WARNING: You are running this process as the root user, which is not recommended.
2021-06-02T04:12:17.903-0400 I CONTROL  [initandlisten] 
2021-06-02T04:12:17.903-0400 I CONTROL  [initandlisten] 
2021-06-02T04:12:17.903-0400 I CONTROL  [initandlisten] ** WARNING: /sys/kernel/mm/transparent_hugepage/enabled is 'always'.
2021-06-02T04:12:17.903-0400 I CONTROL  [initandlisten] **        We suggest setting it to 'never'
2021-06-02T04:12:17.903-0400 I CONTROL  [initandlisten] 
2021-06-02T04:12:17.903-0400 I CONTROL  [initandlisten] ** WARNING: /sys/kernel/mm/transparent_hugepage/defrag is 'always'.
2021-06-02T04:12:17.903-0400 I CONTROL  [initandlisten] **        We suggest setting it to 'never'
2021-06-02T04:12:17.903-0400 I CONTROL  [initandlisten] 
> version()
4.0.24
> 
```

#### 客户端工具

也可以用mongodb客户端工具进行连接，常见的工具有：Dbeaver Enterprise、Navicat Premium、Studio 3T、Robo 3T （以前叫robomongo）。



