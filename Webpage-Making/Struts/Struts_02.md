# Struts_02

## struts和servlet对比

- 启动	
  - servlet
    - 无	
  - struts
    - 配置filter

- 创建
  - servlet
    - 继承HttpServlet,实现doget,dopost
    - 添加注解,或者配置web.xml	
  - struts
    - 继承ActionSupport,写一个带有String返回值且抛出一个异常的函数		
    - 根据返回值，判断跳转到哪个界面
    - 配置struts.xml

```xml
<package name="MyPackage" namespace="/" extends="struts-default">
    <action name="LoginAction" class="com.web.UserAction" method="execute">
        <result name="success" type="redirect">/index.html</result>
        <result name="error">/login.jsp</result>
    </action>
</package>
```

- 封装参数
  - servlet
    - 导入包BeanUtils,根据form表单中的name属性自动封装	
  - struts
    - 实现ModelDriven接口,实现getModel方法（先要把对象new出来）
    - 也是通过name属性进行封装

- 转发与重定向	
  - servlet		
    - 转发
      - `request.getRequestDispatcher`("/login.jsp").forward(request, response);
    - 重定向
      - `response.sendRedirect(request.getContextPath()+"/index.html");`
  - struts	
    - 使用配置文件中进行转发	
    - 转发（默认）		
      - `<result name="error">/login.jsp</result>`	
    - 重定向
      - `<result name="success" type="redirect">/index.html</result>`