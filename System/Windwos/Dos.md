# Windows Dos常用命令

## 用户操作

* net user 用户名 密码 /add (建立用户) 
* net localgroup administrators 用户名 /add (将用户加到管理员，使其拥有管理权限)
* net user guest /active:Yes (激活guest用户) 
* net user guest 12345 (修改guest密码为12345) 
* net user (查看账号属性) 
* whoami 当前用户

## 服务

- net use \\ip\ipc$ "" /user (建立空IPC链接)
- net use \\ip\ipc$ "密码" /user:"用户名" (建立IPC非空链接，非空链接就是需要帐户和密码) 
- net use \\ip\ipc$ /del (删除IPC空链接) 
- net start (查看开启了哪些服务)
- net start 服务名 (开启服务) 
- net time \\目标IP (查看对方时间) 
- net view (查看本地局域网开启了哪些共享) 
- net share (查看本地开启的哪些共享) 
- net share C$/del (删除C：共享) 
- netstat -ano (查看计算机开放了哪些端口以及链接情况和PID) 
- nbtstat -A ip (对方136到139一个端口开放了就可以查出对方用户名)

## 操作

- Copy xx.exe \\ip\admin$\System32 (将当前xx.exe复制到对方Admin$共享的System32目录内)
- net stop sharedaccess(关闭系统自带的防火墙)
- net send IP 消息(利用messenger服务向目标IP发送消息)
- tasklist(查看进程)
- taskkill(结束进程)
- 开启3389远程终端 reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t reg_dword /d 0 /f
- 开启C盘默认共享 net share c$=c:
- 开启计划任务服务（at命令需要这一服务）net start schedule

## 杂项

```
Cd             切换目录
Dir            列出所有文件信息
Del            删除文件
Md             创建目录 
Rd             删除目录
Copy           复制
Xcopy          复制文件和文件夹
Cls            清屏
Attrib         修改文件、文件夹属性
Date、Time     显示日期、时间
Path           系统路径
Set            显示、设置系统信息
Ren(Rename)    重命名
Subst     		 虚拟磁盘
Ver            显示操作系统版本
Help           帮助
Systeminfo     查看系统软硬件信息
/?             显示某条命令的帮助
```

