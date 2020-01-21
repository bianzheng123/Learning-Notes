# JSP和Servlet_03

注解和配置文件

注解在发布后不能随时修改

使用配置文件可以进行随时的修改

在工具类中使用单例模式

## MVC

model

放置数据

view

用户展示

使用servlet显示

controller

用于各种转发xxx_do

##### 流程

用户先访问controller

controller利用model层构造数据，并提供某些jsp

jsp返回给用户

## JavaEE分层

![img](./Snipaste_2020-01-19_16-23-02.png)

### web

jsp servlet

包含了controller、view

### service

调用dao层增删改查操作的

业务逻辑处理

### dao层

对数据库进行增删改查

只是单纯的增删改查操作

### 流程

controller向service层进行交互

service层访问dao层

dao层将修改的数据给service

service再给web层

传递的数据是model层

## 相对路径

使用request.getContextPath()获取当前目录下的绝对路径

客户端路径里面，不能使用相对路径

转发后使用相对路径则是相对于当前的路径，就会报错

客户端路径

- 需要在浏览器上解析
- 查看源代码后路径能显示
- 客户端路径统一使用绝对路径
- 客户端绝对路径是根目录

服务器端路径

- 在jsp中不会显示结果
- 例如`<jsp:include>`
- 绝对路径总是域名加项目名
- 不会发生客户端的问题

## 生命周期

init()

destroy()

构造方法()

service()

- 不管是触发doget还是dopost，都会调用该方法

构造方法和init()只会调用一次，就是第一次被访问的时候

## jar包引入

放到WEB-INF/lib下面

## 内置对象

### 域对象（从小到大）

page

转发则无效

代表当前页面，jsp中等同于this

request

只是在请求中有效

在转发中也有效

session

在整个会话周期有效

application

一整个应用有效

### 其他

pageContext

getOut()

getRequest()

getResponse()

getServletContext()//application

getSession()//httpSession

pageContext.setAttribute("user","fsd",PageContext.PAGE_SCOPE)//设置属性，并设置作用域

## API

jsp引入（用于设置相同内容的html网页）

`<jsp:include page="footer.jsp"></jsp:includde>`

## 要点

转发不会改变请求的方式

能重定向尽量重定向