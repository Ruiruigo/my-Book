# re 模块

---

- **findall函数**

```python
ret = re.findall('\d+','age=19,出生年=2000，出生月=10', re.S)
#返回所有满足匹配条件的结果，都是放在列表中的，\d+在正则表达式的用法为匹配数字 
#re.S将这个字符串作为一个整体，在整体中进行匹配
print(ret)
结果：['19', '2000', '10']
```

- **search函数**

  只匹配从左到右的第一个，得到的不是直接的结果，而是一个变量。可返回True

```python
ret = re.search('\d+','age=19,出生年=2000，出生月=10')
print(ret)
#结果：是内存地址,这是一个正则匹配的结果，<re.Match object; span=(4, 6), match='19'>
print(ret.group())  # 通过ret.group()获取真正的结果
#结果：<re.Match object; span=(4, 6), match='19'>
#19
```

- **match函数**

```python
ret = re.match('\d+$','age=19,出生年=2000，出生月=10')
print(ret)
#结果：None
#从头开始匹配,相当于search中的正则表达式加上一个^
```

- **spilt函数**

```python
s = ('age=19,出生年=2000，出生月=10')
print(',切割:',s.split(','))  #按，来切割
s1 = ('age=19,出生年=2000，出生月=10')
ret = re.split('\d+',s)     #按数字来切割
print(ret )
#结果：,切割: ['age=19', '出生年=2000，出生月=10']
# ['age=', ',出生年=', '，出生月=', '']
```

- **sub函数**

```python
s = ('age=19,出生年=2000，出生月=10')
ret = re.sub('\d+','*',s)   #把所有的数字替换成*
# 替换的次数自己可以定义例如替换一次ret = re.sub('\d+','*',s,1)
print(ret)
#结果：age=*,出生年=*，出生月=*
```

- **subn函数**

```python
s = ('age=19,出生年=2000，出生月=10')
ret = re.subn('\d+','*',s)
print(ret)
#结果：('age=*,出生年=*，出生月=*', 3)
```

- **compile函数**

```python
ret = re.compile('\d+')     #已经完成编译了
print(ret)
# 结果：re.compile('\\d+')
s = ('age=19,出生年=2000，出生月=10')
res = ret.findall(s)
print(res)
# 结果：['19', '2000', '10']
```

- **finditer函数**

```python
s = ('age=19,出生年=2000，出生月=10')
ret = re.finditer('\d+',s)
print(ret)
#<callable_iterator object at 0x000001DBEE68A2E8>
# 结果：返回一个迭代器,所有的结果都在这个迭代器中,需要通过循环+group的形式取值 能够节省内存
for el in ret:
　　print(el.group())
#结果：19
# 2000
# 10
```

