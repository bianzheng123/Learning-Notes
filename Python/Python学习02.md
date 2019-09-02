# Python学习02

## 函数

创建函数

```def Function():```

属性```Function.__doc__```指的是查看文档

- 使用```''```写函数的文档
- 使用```#```写默认的注释

关键字索引

- 定义函数为

  ```SaySome(name,words)```:

  则调用函数可以为:

  ```SaySome(words="fsd",name="aaa")```

  则words就是"fsd"，而name为"aaa"

也可以在定义函数的时候带上默认值

可变参数（加上星号）

- eg:```def test(*params):```，则这个params就是一个列表
- 可变参数一定要是在最后一个，或者不可变参数要使用默认值

函数都有返回值，而且可以返回多个值

- ```return[1,2]```
- 也可以是```return 1,2```实际上是返回元组

屏蔽机制：在函数内部，不能修改函数外部的值

使用关键字```global```声明变量是否为全局变量

- eg：```global count```则count为全局变量
- 就是说，在函数里面修改count的值会影响到函数外部

### 内嵌函数

内部函数作用域在整个外部函数之内

#### 闭包

`def Funx(x):`

​	`def Funy(y):`

​		`return x * y`

​	`return Funy`

闭包的使用

`i = Funx(8)`

`i(5) #结果是40`

`Funx(8)(5) #结果也是40`

需要注意的是，Funx（）中返回值Funy不能加括号

`nonlocal`声明这个不是局部变量，用于嵌套函数的内部变量声明

由于元组是存在堆里面，所以将变量放在元组里面，就可以在内部函数对该元组进行访问

### lambda表达式

用于匿名函数

`g = lambda x,y : x + y`

上述表达式等同于

`def g(x,y):`

​	`return x + y`

则g就是一个函数

lambda使得代码变得简洁

用于调用次数非常少的函数

lambda例子

- `filter()`过滤器，用于过滤不需要的值

  第一个参数是函数，使用lambda就可以简洁的写出过滤的方法

- `map()`映射函数，同`filter()`

## 字典和集合

字典

代表的是一种映射

`dict1 = {'a':'a1','b':'b1'}`

dict1['a']的值为'a1'

key也可以是数字

使用dict创建字典：

- `dict3 = dict(('f',70),('i',30))`
- `dict4 = dict(fi=70,i="fsdfa"))`注意key不能加引号

使用dict['fi'] = ...

`keys()`，`values()`，`items()`

- 用于for循环

集合

没有映射

唯一

无序

使用`set()`变成一个集合，转换成集合时自动将元素变为唯一的

不可变集合使用`frozenset()`

## 对象

#### 类声明对象

`class Turtle:`

​	`#属性`

​	`color = 'green'`

​	`weight=10`

​	`#方法`

​	`def climb(self):`

​		`print('1234')`

​	`def __init__(self,name):`

​		`self.name = name;`

self相当于this指针，后面在方法中列举参数即可

`__init__`代表构造函数

#### 继承

`class MyList(list): #代表继承自list`

​	`pass#代表不做任何修改`

`list2 = MyList()`

`list2.append(2)`

则list2的值为[2]

#### 共有，私有

在函数或者变量前面加上两个下划线（_）即可将共有变量变成私有变量

但是这个是伪私有，其实换了一个名称仍然能够在外部访问到该变量