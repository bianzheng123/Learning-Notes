# Spring_01

导入spring

配置web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  <display-name>SpringProject</display-name>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>
  
  <!-- 让spring随着web项目的启动而去启动 -->
  <listener>
  	<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>
  <!-- 配置spring配置文件的位置 -->
  <context-param>
  	<param-name>contextConfigLocation</param-name>
  	<param-value>classpath:applicationContext.xml</param-value>
  </context-param>
  
  <filter>
  	<filter-name>struts</filter-name>
  	<filter-class>org.apache.struts2.dispatcher.filter.StrutsPrepareAndExecuteFilter</filter-class>
  </filter>
  
  <filter-mapping>
  	<filter-name>struts</filter-name>
  	<url-pattern>/*</url-pattern>
  </filter-mapping>
  
</web-app>
```

配置struts.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE struts PUBLIC
	"-//Apache Software Foundation//DTD Struts Configuration 2.5//EN"
	"http://struts.apache.org/dtds/struts-2.5.dtd">
	
<struts>
	<constant name="struts.devMode" value="true"></constant>
	<constant name="struts.enable.DynamicMethodInvocation" value="true"></constant>

    <!-- 加上这行 -->
	<!-- 告诉struts，你不用创建Action，spring帮你创建Action -->
	<constant name="struts.objectFactory" value="spring"></constant>

	<package name="spring" namespace="/" extends="struts-default">
		<global-allowed-methods>regex:.*</global-allowed-methods>
		<action name="UserAction_*" class="com.web.UserAction" method="{1}">
			<result name="login">/login.jsp</result>
			<result name="toIndex" type="redirect">/index.html</result>
		</action>
	</package>
	
</struts>

```

配置applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:tx="http://www.springframework.org/schema/tx"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
	http://www.springframework.org/schema/beans/spring-beans.xsd
	http://www.springframework.org/schema/context
	http://www.springframework.org/schema/context/spring-context.xsd
	http://www.springframework.org/schema/aop
	http://www.springframework.org/schema/aop/spring-aop.xsd
	http://www.springframework.org/schema/tx
	http://www.springframework.org/schema/tx/spring-tx.xsd">

	<!-- 配置Action -->
	<bean name="userAction" class="com.web.UserAction" scope="prototype">
		<!-- name对应UserAction中的userService变量，名称要一致 -->
		<!-- ref对应配置的Service层中的userService，使用了依赖注入 -->
		<property name="userService" ref="userService"></property>
	</bean>
	
	<!-- 配置Service -->
	<bean name="userService" class="com.service.UserService">
		<property name="userDao" ref="userDao"></property>
	</bean>
	
	<!-- 配置Dao -->
	<bean name="userDao" class="com.dao.UserDao">
	
	</bean>

</beans>
```

将UserService和UserAction中的userDao,userService提取出来成域变量

UserService和UserAction中生成userDao,userService的set方法