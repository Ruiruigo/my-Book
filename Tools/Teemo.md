# Teemo 子域名信息收集及爆破

## 基本使用

运行环境：python 2.7.*

* 查看帮助

```shell
python teemo.py -h
```

* 枚举指定域名（会使用搜索引擎和第三方站点模块）

```shell
python teemo.py -d example.com
```

* 使用代理地址（默认会使用config.py中的设置）

```shell
python teemo.py -d example.com -x "http://127.0.0.1:9999"
```

* 启用枚举模式

```shell
python teemo.py -b -d example.com
```

* 将结果保存到指定文件(默认会根据config.py中的设置保存到以域名命名的文件中)

```shell
python teemo.py -d example.com -o result.txt
```

___项目地址：https://github.com/bit4woo/Teemo___