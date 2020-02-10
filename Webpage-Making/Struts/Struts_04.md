# Struts_04

### 接收参数

#### 方法一

模型驱动

**推荐**

实现`ModelDriven<T>`接口

创建一个User的成员变量

重写getModel方法，返回一个user

```java
public class UserAction extends ActionSupport implements ModelDriven<User>{

	public User user = new User();
	
	@Override
	public String execute() throws Exception {
        //处理响应
        System.out.println(user.toString());
		return "success";
	}

	@Override
	public User getModel() {
		// TODO Auto-generated method stub
		return user;
	}
}
```

新建了一个user，就相当于将user对象压入栈顶，指针查找的时候就很快

#### 方法二

属性驱动

在Action类中创建表单中对应名称的变量

写对应的get，set方法

```java
public class UserAction extends ActionSupport{

	private String username;
    private String password;
	
	@Override
	public String execute() throws Exception {
        //处理响应
        System.out.println(username + ":" + password);
		return "success";
	}
	//实现username,password的get，set函数
}
```

#### 方法三

对象驱动

jsp的表单中name改成user.password,user.username

在User类中实现username,password的getset方法

在Action类中实现user的getset方法

```java
public class UserAction extends ActionSupport{

	public User user;
	
	@Override
	public String execute() throws Exception {
        //处理响应
        System.out.println(user.toString());
		return "success";
	}
    //user的getset函数
}
```

### 传递参数

传递到jsp

### ActionContext

和request是两个域

功能增强版的request

ActionContext是一个map，装了想获得的所有对象

生命周期是一次请求，但只是声明一个新的引用

request,response,servletContext,session,application,attr,param,valueStack

```java
ActionContext.getContext.put("username","123");
//访问request域

Map<String,Object> session = ActionContext.getContext.getSession();
//访问session域

Map<String,Object> application = ActionContext.getContext.getApplication();
//访问application域
//如果向添加参数，直接调用put方法即可
```



