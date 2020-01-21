# JSP和Servlet_02

# JSP

JavaWeb是JavaEE的一部分

JSP

- html+java代码

index.jsp

- 网站首页

jsp文件中书写java代码

```java
	<%
    //书写java代码
	%>
```

引入类

- `<%@page import="java.util.*">`

不同块之间的变量作用域是相同的

将代码使用`<%`以及`%>`分隔开并插入html语句可以减少使用语句`out.println`

- 隔开代码不影响逻辑

## 服务器端的数据传递

request.setAttribute("key",123);

request.getAttribute("key");

#### request生命周期

当访问request时，就自动创建一个request对象

访问页面时，不能通过request对象传递参数

## Session

会话

所有请求的集合

打开这个网站开始，就产生了session

直到关闭浏览器，或者长时间不和服务器交互，才关闭session

一个客户端只对应一个session

## Application

只存在服务器中

在tomcat中只有一个application对象

为所有的客户端服务

统计用户登陆的个数

## 定义表达式

用来定义变量的一片区域

`<%! int count = 0>`

用于定义jsp的成员变量，在刷新jsp页面时会保存该变量的值，而不是一般定义时的表达式直接初始化

### get方法和post方法

get

用于得到html页面和传递参数

传参时会将参数显示到url中

post

用于传递网页的参数跳转到页面

传参时不会将参数显示到url中

使用表单，设置method为post即可调用post方法

## API

`out.println("");`

- 添加jsp的内容

`<%-str %>`

- 将字符串输入到jsp页面中，同`out.println("")`

request.getParameter("username")

- 使用url得到对应的参数
- 不管是get还是post都能获取

`request.getRequestDispatcher("xx.jsp").forward(request,response)`

- 请求的转发
- 就是将参数发送给xx.jsp，并跳转到xx.jsp中
- 请求转发时，request是同一个

`new String(str.getBytes("iso-8859-1"),"utf-8")`

- 转换编码格式

# Servlet

相当于一个java类

servlet是可以被访问的，在网页中指定路径即可访问

用于书写逻辑，不方便用做展示

只需要在代码中添加servlet文件即可

JSP后期编译也会变成servlet

## Servlet访问路径配置

将tomcat例子里面的web.xml放到WEB-INF下面进行配置

配置文件格式如下

```xml
<servlet>
    	<servlet-name>LoginServlet</servlet-name><!--访问文件的名字,一般与servlet类名相同-->
    	<servlet-class>com.servlet.LoginServlet</servlet-class><!-- 文件的地址-->
</servlet>

<servlet-mapping>
		<servlet-name>LoginServlet</servlet-name><!--访问文件的名字，同servlet标签-->
		<url-pattern>/login_do</url-pattern><!--实际访问文件的路径-->
</servlet-mapping>
```

## 转发和重定向

#### 转发

request.getRequestDispatcher("login.jsp").forward(request,response);

访问的url不变

数据也会传递过去

返回的是原url改变后的html文本

#### 重定向

response.sendRedirect("login.jsp");

服务器告诉客户端访问新的页面

数据不会传递

## API

this.getServletContext()

- 得到JSP中的application对象

request.getSession()

- 得到当前会话