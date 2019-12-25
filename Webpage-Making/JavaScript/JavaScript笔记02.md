# JavaScript笔记02

得到某个对象的引用

var username = document.getElementById("username");

## 标签属性

innerText

用来修改，获取标签里面的内容

## input标签

onblur=“”

失去焦点时调用

## 字符串比较

使用==，!=即可

# 获取html元素

document.getElementById()

> document.getElementsByTagName("div");
>
> div.getElementsByTagName("span");
>
> 代表从div这个变量的子元素中找对应的标签，返回的都是数组

> document.getElementsByClassName("xxx");
>
> div.getElementsByClassName("");
>
> 将搜索范围限定在其子标签内

> document.getElementByName("xxx");
>
> 通过标签的name属性获取，多个标签可以有同一个name值

# 对元素的操作

## 设置内容

p.innerText

只是单纯的添加文本

p.innerHTML

在该范围内添加文本，可以添加别的html标签

## 设置属性

myfont.setAttribute("color","green")

参数：属性名，属性值

var size = myfont.getAttribute("size");

获取属性，返回值都是字符串类型

## 设置CSS样式

myfont.setAttribute("style","font-family:幼圆");

就是设置style属性

## 修改属性

mya.href=""

myimg.src=""

mycheckbox.checked=true;

mydiv.style

修改CSS样式

mydiv.style.fontSize="20px";

修改该标签CSS的一些属性

自动设置

# DOM事件

例如onclick就是DOM事件

这些事件适用于大多数标签

在标签中添加对应的属性即可

onclick

onsumit

提交表单时触发

onblur

失去焦点时触发

## 添加事件

### 通过onclick属性添加事件

### 通过代码动态添加事件

#### 方法一

`var myspan = document.getElementById("myspan");`

`myspan.onclick = function(){}`

#### 方法二

`myspan.addEventListener("click",function(){});`

## 常用事件

onload

当整个元素以及子标签被加载出来后就执行该事件

> onunload
>
> onbeforeunload

onchange

文本的值发生改变，并切换焦点时调用该函数

onmouseover

鼠标滑到标签后就执行

onmouseout

鼠标划出标签后执行

onmousedown

鼠标按下

onmouseup

鼠标抬起

# 节点操作

## 添加节点

使用innerHTML创建

- myp.innerHTML添加子标签

使用document.createElement()创建

```javascript
var newSpan = document.createElement("span")
var mydiv = document.getElementById("xxx");
mydiv.appendChild(newSpan);
```

## 给某个标签添加文本

- ```javascript
  var textNode = document.createTextNode("xxx");
  newSpan.appendChild(textnode)
  ```

- ```javascript
  newSpan.innerText="xxx";
  ```

## 删除节点

获取他们的引用，直接删除即可

`mydiv.removeChild(myp);`

# 轮播图要点

window.setTimeout(function,time)

过了time时间后调用function

window.setInterval(function,time)

每隔time的时间就调用函数function

# 数组

```javascript
var arr1 = new Array(10);//可以默认长度，也可以不默认长度
arr[0] = 100;
arr[1] = 30;
arr1.length
```

长度是按照最大索引+1

### 声明数组

```javascript
var arr1 = new Array();
var arr2 = new Array(10);
var arr3 = new Array(90,"xx",80,20);
```

# Window对象

指的是浏览器窗口

定义变量时会自动地将变量放在window这个域里面

document位于window里面

```javascript
window.alert(str);
window.setInterval(str,2000);
window.setTimeout(str,2000);
window.confirm("你好吗");//点击确定返回true，否则返回false
window.prompt("请输入性别");//需要输入一个文本域，返回值为输入的值
var w = window.open("http://www.baidu.com","new_window","width=500,height=500");//用来打开新的网址
w.resizeTo(300,300);//设置打开网页的长和宽
w.moveTo(200,500);//指的是打开网页时的相对位置(相对于左上角)
w.focus();//让该网页处于焦点
w.close();//关闭某个窗口
```

```javascript
screen.availWidth
screen.availHeight//可用宽度和可用高度，也就是分辨率
location.hostname//获得其主机域名
location.port
location.pathname
location.protocol
location.assign("www.baidu.com");//相当于跳转到超链接
```

```javascript
window.history//获取该网页的浏览记录
history.forward();
history.back();//后退和前进
history.go(-1);//代表前进/后退几步
```



# 注意要点

html代码是由上到下执行

对于立马执行的JavaScript代码，如果放在tag前面，则找不到对应的组件，因为还没有解释到对应的标签

对于一些所有标签加载完成后再需要进行操作的代码

- 在body标签中添加onload属性，里面写需要加载的函数