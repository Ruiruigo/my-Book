# JSFinder

JSFinder是一款用作快速在网站的js文件中提取URL，子域名的工具。 环境 Python3

## 用法

- **简单爬取**

```shell
python JSFinder.py -u http://www.mi.com
```

这个命令会爬取 http://www.mi.com 这单个页面的所有的js链接，并在其中发现url和子域名

- **深度爬取**

```shell
python JSFinder.py -u http://www.mi.com -d
```

深入一层页面爬取JS，时间会消耗的更长。

建议使用-ou 和 -os来指定保存URL和子域名的文件名。 例如：

```shell
python JSFinder.py -u http://www.mi.com -d -ou mi_url.txt -os mi_subdomain.txt
```

- **批量指定URL/指定JS**

指定URL：

```shell
python JSFinder.py -f text.txt
```

指定JS：

```shell
python JSFinder.py -f text.txt -j
```

可以用brupsuite爬取网站后提取出URL或者JS链接，保存到txt文件中，一行一个。

指定URL或JS就不需要加深度爬取，单个页面即可。

- **其他**

-c 指定cookie来爬取页面 例：

```shell
python JSFinder.py -u http://www.mi.com -c "session=xxx"
```

-ou 指定文件名保存URL链接 例：

```shell
python JSFinder.py -u http://www.mi.com -ou mi_url.txt
```

-os 指定文件名保存子域名 例：

```shell
python JSFinder.py -u http://www.mi.com -os mi_subdomain.txt
```

- **注意**

url 不用加引号

url 需要http:// 或 https://

指定JS文件爬取时，返回的URL为相对URL

指定URL文件爬取时，返回的相对URL都会以指定的第一个链接的域名作为其域名来转化为绝对URL。

实测简单爬取：

```shell
python3 JSFinder.py -u https://www.jd.com/
```

实测深度爬取：

```shell
python3 JSFinder.py -u https://www.jd.com/ -d -ou jd_url.txt -os jd_domain.txt
```

1