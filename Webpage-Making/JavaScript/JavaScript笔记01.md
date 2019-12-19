# JavaScript笔记01

## 标签

### script

`<script type="text/javascript"></script>`

里面写js代码

`<script type="text/javascript" src=""></script>`

网络外部引入

这个标签放在任何位置都可以

### onclick

`<font onclick="">你好</font>`

onclick里面写js代码，输入字符串时用单引号，不能使用双引号

触发事件才会调用

每一个标签都有onclick属性

## 语法

`alert(str)`

弹出一个弹出框

`typeof()`

显示类型

`console.log(str)`

输出语句

`function myname(参数){}`

定义函数

`document.write(str);`

将里面的对象输出到body中

## 字符串

### 属性

length

str[0]可以获取对应的字符，但是不会修改

### 方法

Javascript是不能改变字符串的，只能将变量赋值给新的字符串

所有的方法都是对原有的字符串没影响，返回修改后的字符串

`toUpperCase()`

`indexOf(str,int)`

取得字符串首字符的索引，没有就是-1

int代表从指定索引开始进行查找

`concat(str...)`

`slice(int,int)`

截取字符串，左闭右开，负数代表从后面开始数

`substring(int,int)`

同slice()，开始索引大于结束索引时直接调换参数位置，如果输入为负数就直接变为0

`substr(int,int)`

第一个指开始截取的索引，第二个指的是截取的长度

`split(str,int)`

分割,int代表取前n个截取的结果

`trim()`

`search(str)`

里面可以是字符串，也可以是正则表达式

`replace(str,str);`

第一个是要寻找的字符串，也可以是正则

第二个是要替换的字符串

`p1.test(str)`

代表检查str是否符合正则表达式

#### 正则表达式

描述一系列规则

##### 表示方式

i忽略大小写

g全局匹配

m表示多行查找

var p1 = /ab/i;

表示查找的是ab Ab aB AB

var index = str.search(p1)

默认搜索第一个子串

#### 语法

^	以...为开头

$	以...为结尾

[]	中括号内任意选择一个可以是1234，也可以是1-4，a-z

\d	代表数字

`*`	表示前面的字符可以有0个或者多个

`+`	前面的字符至少有1个

#### 例子

表示一个正整数

/^[1-9]\d*$/

## 要点

当内容包含双（单）引号时，注意单引号和双引号之间的切换。如果无法完成切换，使用转义字符

### 将两个变量转换成字符串

```javascript
var a = 3.5;
var b=2;
var res = ""+a+b;//3.52
```

### ==和===

==在比较时会进行强制转换

===就不会强制转换

### 匿名函数

使用方式一

将匿名函数赋值给一个变量，使用变量接收

```javascript
var a = function(){
    console.log("匿名函数");
}
a();
```

使用方式二

```javascript
function attack(attackmode){
    attackmode();
    console.log("掉血");
}
attack(function(){
   console.log("我使用刀进行攻击"); 
});
attack(function(){console.log("我是用枪进行攻击");});
//结果
//我使用刀进行攻击
//我是用枪进行攻击
```

## 对象

### 方法一

键值对

`user={name:"bian",age:80,sex:"男"}`就创建了user对象

### 方法二

```javascript
var user1 = new Object();
user1.name = "ab";
```

### 构造函数创建对象

```javascript
function user(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.show = function (){
        console.log(this.name + " " + this.age + " " + this.sex);
    }//给对象添加函数
}
user3 = new user("as",1,“女”);
```

对象的属性可以随时添加

使用匿名函数对对象添加函数

js中的对象实际上是键值对，使用`user3["name"]`也可以访问

遍历对象中属性

```javascript
for(key in user3){
	console.log(user3[key]);
}
```



