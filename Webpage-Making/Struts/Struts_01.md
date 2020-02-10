# Struts_01

#### 使用struts的action处理请求，代替原本的servlet

#### 配置struts

在WebContent/WEB-INF/web.xml中web-app标签里面加入如下标签即可

```xml
<filter>
  	<filter-name>struts</filter-name>
  	<filter-class>org.apache.struts2.dispatcher.filter.StrutsPrepareAndExecuteFilter</filter-class>
    <!-- 防止中文乱码问题 -->
    <init-param>
    	<param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
</filter>
  
<filter-mapping>
    <filter-name>struts</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

和使用xml配置servlet路径几乎一样

在src下面创建struts.xml,头部编写如下代码

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!DOCTYPE struts PUBLIC
	"-//Apache Software Foundation//DTD Struts Configuration 2.5//EN"
	"http://struts.apache.org/dtds/struts-2.5.dtd">
```

在com.web下创建UserAction类，编写代码如下

```java
package com.web;

import com.domain.User;
import com.opensymphony.xwork2.ActionSupport;
import com.opensymphony.xwork2.ModelDriven;
import com.service.UserService;

public class UserAction extends ActionSupport implements ModelDriven<User>{
//使用struts框架，一定要继承自ActionSupport类
	public User user = new User();
	
	@Override
	public String execute() throws Exception {
		UserService userService = new UserService();
		boolean success = userService.findUser(user);
		if(success) {
			return "success";
		}else {
			return "error";
		}
	}

	@Override
	public User getModel() {
		return user;
        //根据表单接收值，并通过框架调用set方法得到表单中的user对象
	}
}

```

在struts.xml下面加入以下标签

```xml
<struts>

	<!-- name：配置包名，一个包名可以有多个action -->
	<package name="MyPackage" namespace="/" extends="struts-default">
		<action name="LoginAction" class="com.web.UserAction" method="execute">
            <!-- 默认是转发，加上type属性就是重定向 -->
			<result name="success" type="redirect">/index.html</result>
			<result name="error">/login.jsp</result>
		</action>
	</package>
<!-- 
跳转页面时，url为${pageContext.request.contextPath }/LoginAction
系统会查找name为LoginAction的action标签，然后调用execute方法
如果execute返回的是success，就跳转到index.html
否则跳转到login.jsp
-->
</struts>
```

#### 解决中文乱码问题

添加log-4j-core这个jar包

web.xml中添加代码

src中添加log4j2.xml

