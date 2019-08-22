# Object Oriented JavaScript

## 相关操作

定义类

`class c{`

​	`constructor(){this.size='160oz';}`

​	`checkSize(){console.log('My size is: ',this.size);}`

`}`

使用new关键字创建变量 

## 概念

var是函数内有效，let是在花括号内有效

函数内部的返回值可以是函数，如果想要使用变量接收该函数返回值并调用该函数，则在变量后面加上括号即可

closure：一个可以访问父函数作用域的函数，即使该父作用域已经被关闭

如果自身的作用域没找到，就去父作用域找 

使用closure的外部函数传递参数来利用closure这个性质