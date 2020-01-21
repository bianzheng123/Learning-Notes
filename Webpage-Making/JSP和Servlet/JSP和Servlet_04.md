# JSP和Servlet_04

## el表达式

让jsp变得更加简单

#### 从域对象取得数据

```el
存储数据的代码
request.setAttribute("number",2000);
session.setAttribute("user","www.sikiedu.com");
application.setAttribute("count","fsdfdsfds");

取得数据的代码(在html中写即可)
${requestScope.number}
${sessionScope.user}
${applicationScope.count}
如果没有指定域，就可能产生歧义
如果没有找到对应的值，就输出空字符串
```

#### 得到数据的某个属性

```el
从类中取得数据
<%
User u = new User("fsd","fds",90,"男",false);
request.setAttribute("user",u);
%>
获取属性
${requestScope.user.username}

从map中取得数据
<%
Map<String,String> map = new HashMap<>();
map.put("name","李四");
map.put("age","12");
request.setAttribute("map",map);
%>
获取属性
${requestScope.map.name}
${requestScope.map.age}

从list集合中取得数据，list放置的是对象
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
获取属性
${list[2].username}
${list[4].username}
```

#### 判断对错，简单运算

```el
${90+90}
${90>80}
${empty list}//判断是否为空
${empty list2}
```

#### 其他

```el
${pageContext.request.contextPath}//获取当前文件路径
等同于request.getContextPath()
```

el只能取数据