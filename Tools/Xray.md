# Xray Poc漏洞扫描器

## 快速使用

### 扫描一个站点

```shell
./xray webscan --basic-crawler http://127.0.0.1/
```

### 指定扫描输出

不指定输出时，默认输出到控制台的标准输出中，可以做管道处理，也可以选择输出为文件，如：

```shell
./xray webscan --url http://127.0.0.1/ --json-output report.json
```

不同参数对应不同的输出方式：

```shell
无参数：输出到控制台的标准输出 
--`text-output`：输出到文本文件中 
--`json-output`：输出到 JSON 文件中 
--`html-output`：输出到 HTML 文件中
```

## 高级姿势

### 指定扫描插件

使用 `--plugins` 参数可以选择仅启用部分扫描插件，多个插件之间可使用逗号分隔，如：

```shell
./xray webscan --plugins cmd_injection --url http://127.0.0.1/
```

目前提供的插件列表如下：

```shell
SQL 注入检测 (key: sqldet)：支持报错注入、布尔注入和时间盲注等
XSS 检测（key: xss）：支持扫描反射型、存储型 XSS
命令/代码注入检测 (key: cmd_injection)：支持 shell 命令注入、PHP 代码执行、模板注入等
目录枚举 (key: dirscan)：检测备份文件、临时文件、debug 页面、配置文件等10余类敏感路径和文件
路径穿越检测 (key: path_traversal)：支持常见平台和编码
XML 实体注入检测 (key: xxe)：支持有回显和反连平台检测
POC 管理 (key: phantasm)：默认内置部分常用的 POC，用户可以根据需要自行构建 POC 并运行。可参考：POC 编写文档（https://chaitin.github.io/xray/#/guide/poc）
文件上传检测 (key: upload)：支持检测常见的后端服务器语言的上传漏洞
弱口令检测 (key: brute_force)：支持检测 HTTP 基础认证和简易表单弱口令，内置常见用户名和密码字典
JSONP 检测 (key: jsonp)：检测包含敏感信息可以被跨域读取的 jsonp 接口
SSRF 检测 (key: ssrf)：ssrf 检测模块，支持常见的绕过技术和反连平台检测
基线检查 (key: baseline)：检测低 SSL 版本、缺失的或错误添加的 http 头等
任意跳转检测 (key: redirect)：支持 HTML meta 跳转、30x 跳转等
CRLF 注入 (key: crlf_injection)：检测 HTTP 头注入，支持 query、body 等位置的参数
```

___项目地址：https://github.com/chaitin/xray___

