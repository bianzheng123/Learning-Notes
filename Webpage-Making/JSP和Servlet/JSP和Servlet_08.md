# JSP和Servlet_08

# 监听器

监听request（HttpServletRequest），session（HttpSession），application（ServletContext）状态的改变

当这三个东西被销毁时，监听器也同时被销毁

也需要配置文件，添加注解

可以创建多个sessionlistener

### 配置文件

```xml
<listener>
	<listener-class>com.listener.SessionListener</listener-class>
</listener>
```

### 设置session生命周期

```xml
<session-config>
	<session-timeout>1</session-timeout>
    如果1分钟之内没有响应，那么session就销毁
</session-config>
```

对changes to attribute调用不同类型的属性监听器

### 属性监听器

对于application、session、request都适用

attributeAdded

attributeRemoved

attributeReplaced

通过getName(),getValue()得到变化的属性名，属性值

### session绑定监听器

往session添加/移除特定的数据类型才会触发监听

对于model层的某个数据结构添加HttpSessionBindingListener接口，并重写对应的方法即可