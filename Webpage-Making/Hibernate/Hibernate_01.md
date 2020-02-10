# Hibernate_01

## 配置hibernate

导包

配置文件

src下面新建hibernate.cfg.xml文件，配置如下

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
	<!-- 负责初始化hibernate -->
	<session-factory>
		<!-- 连接数据库驱动 -->
		<property name="hibernate.connection.driver_class">com.mysql.cj.jdbc.Driver</property>
		<!-- 数据库地址 -->
		<property name="hibernate.connection.url">
			<![CDATA[jdbc:mysql://localhost:3306/hibernatelearn?useUnicode=true&characterEncoding=UTF8&serverTimezone=UTC&useSSL=true]]>
		</property>
		<!-- 数据库用户名 -->
		<property name="hibernate.connection.username">root</property>
		<!-- 数据库密码 -->
		<property name="hibernate.connection.password">123456</property>
		
		<!-- 配置数据库的方言 -->
		<property name="hibernate.dialect">org.hibernate.dialect.MySQL5InnoDBDialect</property>
		
		<!-- 将hibernate生成的sql语句打印到控制台 -->
		<property name="hibernate.show_sql">true</property>
		<!-- 格式化hibernate生成的sql语句 -->
		<property name="hibernate.format_sql">true</property>
		
		<!-- hibernate自动创建表
			create:			自动创建表，每次框架运行都会创建一张新的表，原来的数据会丢失（开发）
			create-drop:	自动建表，每次框架运行结束都会将所有表删除（开发环境中测试使用）
			update(推荐):	自动生成表，如果表已经存在，则更新数据，如果表不存在，就会创建一张新的表
		 -->
		<property name="hibernate.hbm2ddl.auto">update</property>
		
		<!-- 与User配置文件相关联 -->
		<!-- 写多少配多少 -->
		<mapping resource="com/domain/User.hbm.xml"/>
	</session-factory>
		
</hibernate-configuration>
```

## 配置管理特定表的文件

domain包下面有一个User的model，所以在domain包下面新建User.hbm.xml，配置如下

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-mapping PUBLIC 
    "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
    "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
    
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
	</class>
</hibernate-mapping>
```

## 编写dao层

```java
package com.dao;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

import com.domain.User;

public class UserDao {
	//增
	public void addUser(User user) {
		
		//使用hibernate
		//得到配置信息
		Configuration config = new Configuration().configure();
		//创建sessionFactory对象
		SessionFactory sessionFactory = config.buildSessionFactory();
		//获取session
		Session session = sessionFactory.openSession();
		
		//打开事务
		Transaction transaction = session.beginTransaction();
		//存储user对象
		session.save(user);
		
		//提交事务
		transaction.commit();
		//关闭资源
		session.close();
	}
	
    //删
	public void deleteUser() {
		Configuration config = new Configuration().configure();
		SessionFactory sessionFactory = config.buildSessionFactory();
		Session session = sessionFactory.openSession();
		Transaction transaction = session.beginTransaction();
		//得到id为eb667fc1-ae83-4af6-91ca-0d41265a56fb的对象
		User user = session.get(User.class, "eb667fc1-ae83-4af6-91ca-0d41265a56fb");
		session.delete(user);
		transaction.commit();
		session.close();
	}
	
    //改
	public void changeUser() {
		//读取hibernate.cfg.xml
		Configuration config = new Configuration().configure();
		//获取sessionFactory工厂
		SessionFactory factory = config.buildSessionFactory();
		//获取session
		Session session = factory.openSession();
		//开启事务
		Transaction transaction = session.beginTransaction();
		//获得id为eb667fc1-ae83-4af6-91ca-0d41265a56fb的对象
		User user = session.get(User.class, "eb667fc1-ae83-4af6-91ca-0d41265a56fb");
		//将该对象改名为trigger
		user.setUsername("trigger");
		//更新数据库
		session.update(user);
		//提交事务
		transaction.commit();
		//关闭session
		session.close();
	}
	
    //查
	public void findUser() {
		Configuration config = new Configuration().configure();
		SessionFactory factory = config.buildSessionFactory();
		Session session = factory.openSession();
		Transaction transaction = session.beginTransaction();
		session.get(User.class, "eb667fc1-ae83-4af6-91ca-0d41265a56fb");
		transaction.commit();
		session.close();
	}
}

```

