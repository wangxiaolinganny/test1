# MySQL数据库安装


安装mysql community server 5.1.60 windows版本（32或64位均支持)，安装过程中设置字符集为utf8，root账户密码为调试密码（该密码需向公司询问），安装目录可采用默认方式。 
- MySQL官方下载地址：[MySQL官方下载地址](http://downloads.mysql.com/archives/community/))

建议下载 mysql-essential-5.1.40-win32.exe 

安装采用默认选项，不断Next，注意在配置Instance时需要将端口加入到防火墙意外中，如下图：

![](http://ww1.sinaimg.cn/large/006R5gQQgy1fgjst6srz9j30e30aqdgm.jpg)

编码选择采用utf8，如下：

![](http://ww1.sinaimg.cn/large/006R5gQQgy1fgjst6rzixj30e00ammyo.jpg)

注意加入到环境变量：

![](http://ww1.sinaimg.cn/large/006R5gQQgy1fgjst6txd5j30e00amaba.jpg)

创建root用户和密码，注意密码必须为指定的通用数据库密码（密码向产品经理索取）

![](http://ww1.sinaimg.cn/large/006R5gQQgy1fgjst6ssc0j30e00amjsk.jpg)




# MySQL参数优化设置

MySQL安装完后，右键计算机-管理，选择服务与应用程序-服务，找到MySQL服务，右键停止服务。

打开MySQL安装目录，打开my配置文件。（NotePad++打开）

找到下列三个变量（找不到则添加），修改数值

```ini
innodb_file_per_table=1

tmp_table_size=128M  

max_heap_table_size=128M
```

找到下列三个变量，查看是否满足条件。

```ini
default-character-set=utf8

basedir="D:/Program Files/MySQL/MySQL Server 5.1/"

datadir="D:/ProgramData/MySQL/MySQL Server 5.1/Data/"

```

修改保存后，重新打开MySQL服务（右键计算机-管理，选择服务与应用程序-服务，找到MySQL服务，右键启动服务）。

