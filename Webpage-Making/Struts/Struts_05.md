# Struts_05

## ognl

ognl = jstl + el

在jsp中添加引用

```jsp
<%@taglib uri="/struts-tags" prefix="s" %>
```

循环

```xml
<s:iterator value="pasteList" var="paste">
    <div> <s:property value="ansnum"/> </div>
    <!-- 获取值paste.ansnum -->
</s:iterator>
```

条件

```xml
<s:if test="ansnum%2==0">张大值</s:if>
<s:else>bian</s:else>
<!-- 
	如果paste.ansnum%2==0就输出张大值，否则输出bian
	struts通过if，else，elseif标签进行条件判断 
-->
```

输出对象

```xml
<s:property value="#user.username"/>
<!-- 输出对象就要加上井号 -->
```

#代表ActionContext.getContext()

### ValueStack

##### 流程

创建Action时，先创建actionContext，再创建valueStack，再将action放到valueStack中

ognl直接访问valueStack

对于不同域相同名称的变量，先取得作用域最小的那个

action与jsp数据交互的媒介

### Action

请求到来时

1. 进入前端控制器的东西
2. 进入拦截器
3. 进入valueStack
   - stack
   - actionContext
   - ognl引擎
4. 在拦截器中创建action
5. 将拦截器压入valueStack的栈里面
   - action也会被压入栈中，拦截器的栈和action的栈不是同一个栈

6. 执行拦截器和action
   - 拦截器相当于filter，顺序进入拦截器，然后执行action，再逆序进入拦截器（压栈时为了逆序顺一遍拦截器）

7. 创建result结果集

8. 转换到jsp界面
   - 用ognl引擎，将表达式转换成对应的字符串

### Result

负责输出的处理

转发与重定向是一种特殊的输出方式

转发和重定向书写带参数的格式都一样