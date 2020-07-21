# Nmap

nmap [扫描类型] [选项] {目标规格}

## 端口状态

```
open 开放的
closed 关闭的
filtered 被过滤的）不确定开放还是关闭
unfiltered  未被过滤的
openfiltered  开放或者被过滤的
closedfiltered  关闭或者未被过滤的
```

## 参数

- **主机发现**

```shell
-sL：列表扫描 - 只需列出要扫描的目标
-sn：Ping 扫描 - 禁用端口扫描
-Pn：将所有主机视为在线 - 跳过主机发现
--traceroute：跟踪每个主机的跳转路径
```

- **扫描技术**

```shell
-sS / sT / sA / sW / sM：TCP SYN / Connect（）/ ACK / Window / Maimon 扫描
-sU：UDP 扫描
```

- **端口规格**

```shell
-p <端口范围>：仅扫描指定的端口
例如：-p22 -p1-65535; -p U：53,111,137，T：21-25,80,139,8080，S：9
--exclude-ports <port ranges>：从扫描中排除指定的端口
-F：快速模式 - 扫描比默认扫描少的端口
-r：连续扫描端口 - 不要随机化
--top-ports <number>：扫描<number>最常用的端口
--port-ratio <ratio>：扫描端口比<ratio>更常见
```

- **服务/版本检测**

```shell
-sV：探测打开端口以确定服务/版本信息
```

- **脚本扫描**

```shell
-sC：相当于--script = default
--script = <Lua scripts>：<Lua scripts>是一个逗号分隔的列表目录，脚本文件或脚本类
--script-args = <n1 = v1，[n2 = v2，...]>：为脚本提供参数
--script-trace：显示发送和接收的所有数据
--script-updatedb: 更新脚本数据库
--script-help = <Lua 脚本>：显示有关脚本的帮助。其中<scripts>部分可以逗号分隔的文件或脚本类别
```

- **操作系统检测**

```shell
-O：启用操作系统检测
--osscan-limit：将操作系统检测限制为有希望的目标
```

- **时间&输出**

```shell
-T <0-5>：设置时间模板（越高越好）
-oX <文件>：正常输出扫描，XML
-v：增加详细程度（使用-vv 或更多的效果）
-d：增加调试级别（使用-dd 或更多更大的效果）
--reason：显示端口处于特定状态的原因
--open：仅显示打开（或可能打开）的端口
--packet-trace：显示发送和接收的所有数据包
--webxml：来自 Nmap.Org 的引用样式表，用于更多的便携式 XML
```

## 脚本的应用

- **对目标机器进行扫描,同时对smb的用户进行枚举**

```shell
nmap  --script=smb-enum-users  <ip>
```

- **对目标机器所开启的smb共享进行枚举**

```shell
nmap  --script=smb-enum-shares <ip>
```

- **对目标机器的用户名和密码进行暴力猜测**

```shell
nmap  --script=smb-brute <ip>
```

- **对目标机器测试心脏滴血漏洞**

```shell
nmap -sV --script=ssl-heartbleed <ip>
```

## 常用组合

- **轻量级扫描**

```shell
nmap -sP 192.168.0.0/24   判断哪些主机存活
nmap -sT 192.168.0.3   开放了哪些端口
nmap -sS 192.168.0.127 开放了哪些端口（隐蔽扫描）
nmap -sU 192.168.0.127 开放了哪些端口（UDP）
nmap -sS -O  192.168.0.127 操作系统识别
nmap -sT -p 80 -oG – 192.168.1.* | grep open    列出开放了指定端口的主机列表
nmap -sV -p 80 thief.one  列出服务器类型(列出操作系统，开发端口，服务器类型,网站脚本类型等)
```

- **批量扫描**

```shell
nmap -sT -sV -O -P0 --open -n -oN result.txt -p80-89,8080-8099,8000-8009,7001-7009,9000-9099,21,443,873,2601,2604,3128,4440,6082,6379,8888,3389,9200,11211,27017,28017,389,8443,4848,8649,995,9440,9871,2222,2082,3311,18100,9956,1433,3306,1900,49705,50030,7778,5432,7080,5900,50070,5000,5560,10000 -iL ip.txt
```

- **批量扫描**

```shell
nmap -sT -sV -p80-89,8080-8099,8000-8009,7001-7009,9000-9099,21,443,873,2601,2604,3128,4440,6082,6379,8888,3389,9200,11211,27017,28017,389,8443,4848,8649,995,9440,9871,2222,2082,3311,18100,9956,1433,3306,1900,49705,50030,7778,5432,7080,5900,50070,5000,5560,10000 --open --max-hostgroup 10 --max-parallelism 10 --max-rtt-timeout 1000ms --host-timeout 800s --max-scan-delay 2000ms -iL ~/Desktop/ip.txt -oN ~/Desktop/result/result.txt
```

## Nmap api

**python-nmap**

安装：pip install python-nmap
作用：利用python调用nmap接口

```python
import nmap
nm = nmap.PortScanner()
nm.scan('127.0.0.1', '22-443')
nm.command_line()
```

