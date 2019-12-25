# jQuery学习笔记01

# 添加onload方法

- 标签中添加`onload = ""`

- js代码中添加`window.onload = function();`

- js代码中添加`window.onload = init();`

- jQuery方式

  - `$(init);`//用来指定网页加载完成后需要完成的函数

  - ``` javascript
    	$(
        	function(){alert("xxx");}
      	);
    ```

# 获取HTML元素并进行简单操作

```javascript
    $(function(){
        $("#one")//返回一个jQuery对象,使用id获取对象
        $("#one").show();//display:block
        $("#one").text("jQuery")//innerHTML = jQuery
    });//在window.onload()中进行操作

```

```javascript
    //DOM方式
    var div = document.getElementById("one");
    div.style.display="block";//显示元素
    var div = document.getElementById("one");
    div.innerText="DOM";//获取代码
```

获取的DOM对象和jQuery对象是不能通用的

可以将jQuery对象转换成DOM对象

`$("#one").get(0).innerText="jQuery";`

# API

事件

```javascript
	$("closeBtn").click(function(){});
	$("closeBtn").mouseover(function(){});
	$("closeBtn").mousedown(function(){});
	$("closeBtn").mouseup(function(){});
```

show和hide

```javascript
    $("#one").show();//display:block
	$("#one").hide();//display:none
	$("#one").toggle();//隐藏的显示，显示的就隐藏
	//特效
    $("#one").show("slow");//"slow" "fast"
	$("#one").show(3000);//播放动画为3s
	$("#one").show(3000,function(){
        
    });//回调函数，在动画执行完之后调用
	//show,toggle同理
	//滑动的特效，参数同show,hide,toggle
	$("#one").slideDown();
	$("#one").slideUp();
	$("#one").slideToggle();
	//渐变的特效，参数同show,hide,toggle
	$("#one").fadeIn();
	$("#one").fadeOut();
	$("#one").fadeToggle();
	$("#one").fadeTo(“slow",0.5);//将透明度设置到合适的值,后面的0.5指的是最终透明度的值。0透明，1不透明
```

属性

```javascript
	$("tbody input[name='select']").prop("checked",this.checked);//指的是将满足条件的组件设置其checked属性为该对象的属性
	$("tbody input[name='select']").prop("checked");//指的是得到满足条件的组件其checked属性的值
```

其他

```javascript
	$("#one").text("jQuery")//innerHTML = jQuery
```

节点操作

```javascript
	//添加节点
	var option = document.createElement("option");
	$("#city").append(option);//添加DOM对象

	$("#city").append($("div"));//添加已有的jQuery节点
	$("#city").append("<strong>fsd</strong>");//添加文本节点
	//清除子结点
	$("#city").empty();//将该标签里面的内容清空
```



## 获取对象

$("#id")//返回单个jQuery对象

$(".two")//返回数组

$("div")//返回数组

$("*")//返回全部元素

## 过滤器

```javascript
	$("div:even")//取得所有的偶数标签
	$("div:odd")//取得所有的奇数标签
	//按照书写的先后顺序进行索引
	//父子关系不会影响索引的先后顺序
```

## 选择器

```javascript
	$("table td")//祖先选择器，这个选择后代
	$("#id td")
	$("div>span")//只选择孩子，就是只选择下一级的标签
	$("div[name='fsd']")//属性选择器
	$("div[href|='en']")//要么和给定的值相等，要么以-开头
	$("div[href!='en']")
```

## 属性





# 要点

将HTML，CSS，JS分离

隔行换色

jQuery的事件中this指的是DOM对象

## HTML表格

```html
    <thead></thead>
    <tbody></tbody>
    <tfoot></tfoot>
    这三个标签用来对表格的元素进行分类
```

## 常用插件

validation

pickadate

echarts

chosen

CKEditor