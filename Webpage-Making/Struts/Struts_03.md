# Struts_03

### 创建Action三种方法

都选择继承自ActionSupport

### struts.xml详解

```xml
<package name="MyPackage" namespace="/" extends="struts-default">
    <action name="LoginAction" class="com.web.UserAction" method="execute">
        <result name="success" type="redirect">/index.html</result>
        <result name="error">/login.jsp</result>
    </action>
</package>
```

package

- name:用来配置包名，是一个无关紧要的值
- namespace:相当于一个文件，用于指定访问的路径
- extends:默认值

action

- name：决定了action访问的资源名称，对应servlet：url-pattern
- class：action的完整类名，执行方法定位的类
- method：指定调用action中的哪个方法处理请求，执行的方法

#### 动态方法调用

将多个action变成一个标签

添加标签至package同级旁

```xml
<constant name="struts.devMode" value="true"></constant>
<constant name="struts.enable.DynamicMethodInvocation" value="true"></constant>
```

添加标签至action同级旁，并修改action标签

```xml
<global-allowed-methods>login,register,kill</global-allowed-methods>
<!-- 下一行是一键配置所有的 -->
<global-allowed-methods>regx:.*</global-allowed-methods>
<action name="LoginAction_*" class="com.sikiedu.web.UserAction" method="{1}">
    <!-- 重定向 -->
    <result name="success" type="redirect">/index.html</result>
    <!-- 默认为转发 -->
    <result name="error">/login.jsp</result>
</action>
```

这样当访问路径为/LoginAction_login时就会调用UserAction中的login方法

访问路径为/LoginAction_register时就会调用UserAction中的register方法

#### 转发、重定向到Action

```xml
<action name = "LoginActionDefault" class="com.sikiedu.web.DefaultAction" method="execute"></action>
		
<action name="LoginActionImpl_*" class = "com.sikiedu.web.ImplAction" method="{1}">
    <!-- 转发到LoginActionDefault,路径是不会变的 -->
    <result name="defaultAction" type="chain">LoginActionDefault</result>

    <!-- 重定向到Action(LoginAction_*) -->
    <result name="toLogin" type="redirectAction">
        <param name="actionName">LoginAction_login</param>
        <!-- 标记的action，其name属性必须是actionName -->
        <!-- 如果不带参数就直接写，不需要加标签-->
        <!-- 转发如果也想带参数就同理 -->
        <!-- 使用的是get方法，就是url后面加上?还有一堆参数 -->
		<!-- 通过ActionContext.getContext.put("username","123")传递参数 -->
        <param name="username">${username}</param>
        <param name="password">${password}</param>
    </result>
</action>
```

### 要点

一般的，重定向的明明要加to

