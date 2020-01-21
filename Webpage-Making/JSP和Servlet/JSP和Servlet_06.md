# JSP和Servlet_06

json

数组，对象

对象：键值对

数组：`[]`

方法

```java
String str = JSON.toJSONString(goods);
Goods goods = JSON.parseObject(str,Goods.class);
```

## Ajax

使用js原生代码发起ajax：XMLHttpRequest

发起请求

在不进行页面跳转或者页面刷新时发起请求

在js中写

#### GET方法

```javascript
setInterval("callAjax()", 2000);

function callAjax(){
	alert("ajax");
	$.ajax({
		url:encodeURI("${pageContext.request.contextPath}/ajaxrequest?data=我是数据"),//url里面填的是目标jsp或者servlet，如果URI里面有中文就要进行编码
		type:"get",
		success:function(msg){//接收结果后得到的函数，msg是返回的参数
			
		}
	})
}

```

#### POST方法

```javascript
function verifyUsername(){
		
		$.ajax({
url:encodeURI("${pageContext.request.contextPath}/verifyusername"),
			type:"post",
			data:{
	username:$("input[name='username']").val()
			},
			dataType:"json",
			cache:false,
			success:function(msg){
				if(msg.isSuccess){
					$("#msg").html("<font color='green'>用户名可以用！</font>");
				}else{
					$("#msg").html("<font color='red'>用户名重复！</font>");
				}
			}
		})
	}
```



#### 客户端向服务端发送数据

对于get方法，在url后面加上?并跟上键值对即可

### 服务端api

#### 服务端向客户端发送数据

response.getWriter().append("str");

设置返回的参数msg

response.setContentType("");

设置返回报文的字符