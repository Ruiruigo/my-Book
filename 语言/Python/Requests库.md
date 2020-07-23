# Requests库

---

## requests

发送一个发送请求可携带参数,json,cookies,files,timeout代理及请求头内容(字典形式)

```python
requests.get(url,data=,json=,cookies=,proxies=,headers=,files=,timeout=,verify=False)
requests.post(url,data=,json=,cookies=,proxies=,headers=,timeout=)
```

返回数据类型为：<class 'requests.models.Response'>

返回数据类型可使用函数   ▼

| 函数         | 解释                             |
| ------------ | -------------------------------- |
| .test        | 获取str类型（Unicode编码）的响应 |
| .content     | 获取bytes类型的响应(二进制)      |
| .status_code | 获取响应状态码                   |
| .encoding    | 获取编码                         |
| .headers     | 获取响应头                       |
| .request     | 获取相应对应的请求               |

## 获取cookie信息

获取cookies保存为字典形式

```python
requests.utils.dict_from_cookiejar(requests.cookies,session.cookies)
```

返回数据类型为：<class 'requests.cookies.RequestsCookieJar’>

## 构造session回话对象

先使用session发送请求登陆网站，session会自动封装cookie在session之中

```python
.post(url,data=,json=,cookies=,proxies=,headers=,files=,timeout=)
```

在使用携带已经封装好cookie的session请求登陆过后的网站，session能够自动的携带cookie进行请求

```python
.get(url,data=,json=,cookies=,proxies=,headers=,files=,timeout=)
```

返回数据类型为：<class 'requests.sessions.Session’>

## 获取响应头

```
.headers  #返回字典的形式
====
r = requests.get('https://www.baidu.com')
print(r.headers['Server'])
print(r.headers.get('Server'))  #两种方式
```

