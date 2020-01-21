# JSP和Servlet_01

## XML

标签大小写敏感

使用转义符表示特殊符号

- 在文本中加入等于号，尖括号等等

### 约束

使用框架进行配置，需要遵守约束

规定标记名称，子元素名称，要求标签必须有属性等等

### 约束文档

写配置文档时，就要使用约束文档，就是书写规则

DTD

#### 引入约束方式

新建一个dtd文件，写约束

引入dtd文件

```
	<!DOCTYPE note SYSTEM "note.dtd">
```

Schema

xmlns:w3=“http://www.w3school.com.cn”

- 对网址的命名空间起别名为w3

targetNamespace,xmlns指定命名空间

使用命名空间区分引入的不同元素

#### 引入约束方式

新建一个dtd文件，写约束

引入dtd文件

```
	<!DOCTYPE note SYSTEM "note.dtd">
```

## 解析XML

DOM方式

- 将xml文档加载到内存中，形成树形结构

dom4j

- 解析xml的开源插件

### 对象名称

```
Element
ele.getName()
ele.element("name")
//获取ele下面名字为name的子元素
ele.getText()
//获取ele里面的内容
ele.elementIterator(String name)
//返回名字为name的子元素迭代器
//如果没有参数就返回所有子元素
ele.attributeIterator()
//获取属性的迭代器

Attribute
attr.getName()
attr.getValue()
//也可以设置值
```



Element

getName()

Attribute

## 使用dom4j生成xml文档

