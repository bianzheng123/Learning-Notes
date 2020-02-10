# Struts_06

## 创建拦截器的两种方法

### 第一种

推荐

继承自MethodFilterInterceptor

重写doIntercept()

```java
@Override
protected String doIntercept(ActionInvocation arg0) throws Exception {

    // 如果用户没有登录，就跳转到登录界面

    //放行
    return arg0.invoke();
}
```

### 第二种

实现Interceptor接口

在intercept()写过滤的代码

## 配置拦截器

在action同级目录下配置

**配置标签的顺序不能变**

```xml
<package name="PastePackage" namespace="/" extends="struts-default">
		<interceptors>
	    	<!-- 注册拦截器 -->
	        <interceptor name="myIntercept" class="com.web.intercept.MyIntercept"></interceptor>
	        <!-- 注册拦截器栈 -->
	        <interceptor-stack name="myStack">
	        	<!-- 引入自己创建的拦截器 -->
	        	<interceptor-ref name="myIntercept">
                	<param name="excludeMethods">login</param>
                    <!-- 配置不应该被拦截的方法 -->
                </interceptor-ref>
	        	<!-- 引入struts给你写好的拦截器 -->
	        	<interceptor-ref name="defaultStack"></interceptor-ref>
       		</interceptor-stack>
    	</interceptors>
    	
    	<!-- 指定包中的默认拦截器栈 -->
    	<default-interceptor-ref name="myStack"></default-interceptor-ref>
    	<!-- 如果不配置，就只使用默认的20个拦截器 -->
    	
    	<global-results>
    		<result name="toLogin" type="redirect">/login.jsp</result>
    	</global-results>
    	<!-- 全局结果集，返回字符串只要符合那个结果都会进入对应的jsp -->
    
		<global-allowed-methods>regex:.*</global-allowed-methods>
		<action name="PasteAction_*" class="com.web.PasteAction" method="{1}">
			<result name="index">/index.jsp</result>
		</action>
	</package>
```

在这个包下面的都会走配置的拦截器

拦截器只能控制访问action，不能控制访问jsp页面

#### 配置不应该拦截的方法

添加如下标签即可

```xml
<param name="excludeMethods">login</param>
```

