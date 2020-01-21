# JSP和Servlet_07

## 过滤器

### 用途

用于过滤敏感词汇

设置权限

进行统一的编码处理

### 访问方式

层层过滤

chain.doFilter()调用下一层过滤器

每当客户端发送一个request，就进行一层过滤，然后传到下一层

最后servlet进行处理，处理的结果继续经过该链逐层往上进行过滤

可以在response后面进行过滤，不过很少用

过滤的顺序和配置的顺序相关

### 相关操作

#### 路径配置

`@WebFilter()`里面写过滤的路径，也可以通过xml进行路径的配置

xml路径配置

```xml
<filter>
    <filter-name>TestFilter</filter-name>
    <filter-class>com.filter.Test1Filter</filter-class>//指定路径
    
    <init-param>
  <param-name>Encoding</param-name>
  <param-value>UTF-8</param-value>
  </init-param>//设置初始化参数
    
</filter>
<filter-mapping>
	<filter-name>Test1Filter</filter-name>
    <url-pattern>/*</url-pattern>//指定过滤器的作用范围
</filter-mapping>
```

#### 设置过滤请求的类型

在`<filter-mapping></filter-mapping>`下面添加标签

`<dispatcher></dispatcher>`

标签里面写类型，基本的如下

request

访问这个页面

include

当该页面被包含时调用该过滤器

dispatcher

当被转发到该页面时调用过滤器、

error

当错误发生，并调用该文件时调用过滤器

- 添加标签

  ```xml
  filter标签略
  <filter-mapping>
  	<filter-name>DispatcherFilter</filter-name>
      <url-pattern>/dispatcher1.jsp</url-pattern>
      <dispatcher>ERROR</dispatcher>
  </filter-mapping>
  
  <error-page>
  	<error-code>404</error-code>
      <location>/dispatcher1.jsp</location>
  </error-page>
  ```

  当输入一个不存在的网页时，自动跳转到dispatcher1.jsp，并提示为ERROR，就会调用DispatcherFilter这个过滤器

#### 要点

如果过滤所有的网址，就填写"/*"

在tomcat创建网站时会对filter执行构造方法，init

当打开一个网站时，就使用doFilter方法

关闭网站时会进行销毁

关键是doFilter方法

#### api

fConfig.getInitParameter("Encoding")

获取初始化的参数

初始化的参数在xml配置文件中声明