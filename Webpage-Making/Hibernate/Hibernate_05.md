# Hibernate_05

## 一对多关系

对于model，外键直接添加对应的模型即可，而不是对应的id

对于User，是一对多

对于Paste，是多对一

Paste模型

```java
public class Paste {
	private String id;
	private String title;
	private String content;
	private Integer offer;
	private Integer ansnum;
	private Integer glanceover;
	private String createtime;
	
	private User user;
}
```

User模型

```java
public class User {
	
	private String id;
	private String username;
	private String password;
	private String name;
	private String email;
	private String telephone;
	
	private Set<Paste> pasteSet = new HashSet<Paste>();
}
```

配置表

Paste

```java
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-mapping PUBLIC 
    "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
    "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
    
<hibernate-mapping package="com.domain">
	<class name="Paste" table="paste">
		<id name="id">
			<generator class="uuid"></generator>
		</id>
		<property name="title" column="title"></property>
		<property name="content" column="content"></property>
		<property name="offer" column="offer"></property>
		<property name="ansnum" column="ansnum"></property>
		<property name="glanceover" column="glanceover"></property>
		<property name="createtime" column="createtime"></property>
		
		<!-- 配置外键,name指的是Paste中的名称,class指的是User这个类,column指的是数据库中对应的键值 -->
		<!-- name：引用属性名
				class:与他关系的对象的完整类名
				column:外键列名
				inverse:配置关系是否不维护
					true：不维护
					false：维护关系
                    用于性能优化
					无论怎么放弃维护，总有一方需要维护
					一般的开发中，一的一方放弃维护，多的一方不放弃维护
		 -->
		<many-to-one name="user" class="User" column="userid"></many-to-one>
	</class>
</hibernate-mapping>
```

User

```java
<!-- 指定会在哪个包中去找 -->
<hibernate-mapping package="com.domain">

	<class name="User" table="user">
	<!-- id元素 
			name:实体中的属性
			colum(可选):数据库的列名
			type(可选):填写列(属性)的类型,hibernate会自动检测实体的属性类型
						每个类型有三种填法:java类型|hibernate类型|数据库类型
			length(可选):配置数据库中列的长度
						默认值:使用数据库类型的最大长度
	 -->
		<id name="id" column="id">
			<!-- 主键生成策略(手动生成) 5种
				identity:主键自增
				sequence:oracle中主键生成策略
				native:identity+sequence (hibernate会根据连续的数据库自动选择(identity,sequence))
				uuid:产生随机字符串作为主键，主键必须为String
				
				assigned:我们要手动去指定
			
			-->
			<generator class="uuid"></generator>
		</id>
		
		<!-- 
			property:除了id之外的普通属性
			name:实体中的属性
			colum(可选):数据库列名
			length(可选):配置数据库中列的长度
						默认值:使用数据库类型的最大长度
			not-null(可选):配置该属性(列)是否不能为空，默认值:false
		 -->
		
		<property name="username" column="username"></property>
		<property name="password" column="password"></property>
		<property name="name" column="name"></property>
		<property name="email" column="email"></property>
		<property name="telephone" column="telephone"></property>
		
		<set name="pasteSet">
		<!-- 在数据库的paste表中找到userid的 -->
			<key column="userid"></key>
			<one-to-many class="Paste"/>
		</set>
	</class>
</hibernate-mapping>
```

## 多对多的关系

转换成两个一对多的关系

详情见代码，主要在于User，Paste，Answer的配置文件