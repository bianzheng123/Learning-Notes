# JSP和Servlet_05

## jstl

能进行循环的遍历

引入jstl

```html
<%@ taglib uri="" prefix="c"%>
使用前缀表示使用的是哪一个类下面的标签
不同的标签名字可能会重复，所以要引入相当于命名空间的东西
uri引入一个提示的网址即可
```

## 标签

添加、设置、删除标签

```xml
设置值
<c:set var="username" value="bian" scope="request"></c:set>
等价于<% request.setAttribute("username", "bian"); %>
    
取值
    相当于将文本输出
<c:out value="${username}"></c:out>
    
从某个域里面移除值
<c:remove var="username"></c:remove>
```

条件标签

单纯的if

```xml
<c:set var="age" value="19" scope="request"></c:set>

<c:if test="${age>=18}">
    <font color="green“>你是成年人</font>
</c:if>
如果test里面为true，就输出里面的话
```

if-else

```xml
<c:set var="age" value="19" scope="request"></c:set>

<c:choose>
    <c:when test="${age>18}">
        <font color="green">你是成年人</font>
    </c:when>
    <c:otherwise>
        <font color="red">未成年</font>
    </c:otherwise>
</c:choose>
```

循环标签

```xml
<c:forEach var="i" begin="1" end="10">
    ${i}<br/>
</c:forEach>
打印输出1到10
```

```xml
<%
List<User> list = new ArrayList<>();
list.add(new User("中国","123",90,"男",false));
list.add(new User("中45国","123",90,"男",false));
list.add(new User("中7国","123",90,"男",false));
list.add(new User("中2国","123",90,"男",false));
list.add(new User("中12国","123",90,"男",false));
list.add(new User("中56国","123",90,"男",false));
list.add(new User("中98国","123",90,"男",false));
list.add(new User("中17国","123",90,"男",false));
request.setAttribute("list",list);
%>

<c:forEach items="${list}" var="u">
    ${u.username}:${u.password}:${u.age}<br/>
</c:forEach>
```

