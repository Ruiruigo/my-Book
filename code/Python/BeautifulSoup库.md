# bs4.BeautifulSoup库

---

## 初始化

初始化一个BeautifulSoup对象

```python
BeautifulSoup(text, "html.parser")  # 'xml'
```

返回数据类型为：bs4.BeautifulSoup

返回数据类型可使用函数   ▼

| 函数       | 返回数据类型                | 解释                                           |
| ---------- | --------------------------- | ---------------------------------------------- |
| .标签      | bs4.element.Tag             | 标签，最基本的信息组织单元                     |
| tag.name   | str                         | 标签名.parent返回父级标签 .get(属性)返回属性值 |
| tag.attrs  | dict                        | 标签的属性，字典形式组织                       |
| tag.string | bs4.element.NavigableString | 标签内非属性字符串，标签内容                   |

### find_all()函数  搜索文档树

.find_all() 返回的是一个列表

函数方法   ▼

| 函数                                | 解释                                             |
| ----------------------------------- | ------------------------------------------------ |
| .find_all(['标签','标签'])          | 对标签名称的检索字符串,也可以穿入列表的形式      |
| .find_all(re.compile('正则表达式')) | 穿入正则表达式进行检索，会通过search()来匹配内容 |
| .find_all(函数)                     | 根据方法或是函数进行匹配                         |
| .find_all(属性='值')                | kwargs参数 属性匹配可使用正则                    |
| .find_all(attrs={'属性':'值'}       | 定义一个字典来搜索包含特殊属性的tag              |
| .find_all(text='内容')              | text参数接受字符串，正则表达式，列表，函数       |
| .find_all('标签',limit=值)          | limit参数来限制返回的数量                        |

.contents 获得子标签

.children 获得子标签 返回的是一个迭代对象，只能通过for循环来使用，不能直接通过索引来读取其中的内容

#### 其他搜索方式

| 函数                    | 解释                           |
| ----------------------- | ------------------------------ |
| find_parents()          | 返回所有祖先节点               |
| find_parent()           | 返回直接父节点                 |
| find_next_siblings()    | 返回后面所有的兄弟节点         |
| find_next_sibling()     | 返回后面的第一个兄弟节点       |
| ind_previous_siblings() | 返回前面所有的兄弟节点         |
| find_previous_sibling() | 返回前面第一个兄弟节点         |
| find_all_next()         | 返回节点后所有符合条件的节点   |
| find_next()             | 返回节点后第一个符合条件的节点 |
| find_all_previous()     | 返回节点前所有符合条件的节点   |
| find_previous()         | 返回节点前所有符合条件的节点   |

### select()函数 CSS选择器

.select()返回的是一个列表tag

函数方法   ▼

| 函数                       | 解释             |
| -------------------------- | ---------------- |
| .select('标签')            | 通过标签查找     |
| .select('类名')            | 通过类名查找     |
| .select('#id')             | 通过id查询       |
| .select('标签 标签')       | 组合查询         |
| .select('标签[属性参数]')  | 属性查找         |
| .select('父标签 > 子标签') | 直接子标签查找   |
| .select('.类 ～ .类')      | 兄弟节点标签查找 |

.select('标签')[0].get_text() >> 获取内容

