# Mybatis_03

### Dao层开发

使用接口，实现类，一个写sql的xml文件

### Mapper动态代理

使用接口，配置文件，实现类使用mybatis自动生成

### 主配置文件简写

UserMapper.java

```java
package com.mapper;

import java.util.List;
import com.bean.User;

public interface UserMapper {

	//mapper动态代理开发四大原则 + 一个注意
	//1、接口方法名需要与mapper.xml的要调用的sql语句的id一致
	//2、接口的形参类型需要与mapper.xml parameterType一致
	//3、接口的返回值需要与mapper.xml resultType一致
	//4、mapper.xml 中的namespace要与接口的全包名一致
	//5、注意mapper动态代理开发中，根据返回值类型来自动选择
	
	//通过id查询用户
	public User selectUserById(Integer id);
	
	//通过用户名模糊查询 获取用户列表
	public List<User> selectUserByName(String name);	
}
```

UserMapper.xml，需要和UserMapper.java名字一致且在同一个包下

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.mapper.UserMapper">
	<select id="selectUserById" parameterType="Integer" resultType="User">
		select * from user where u_id=#{id}
	</select>
	
	<!-- ${}代表字符串拼接 -->
	<select id="selectUserByName" parameterType="String" resultType="com.bean.User">
		<!-- select * from user where u_username like '%${value}%' -->
		select * from user where u_username like "%"#{name}"%"
	</select>
	
	<!-- 添加用户 -->
	<insert id="insertUser" parameterType="com.bean.User">
		insert into user values(null,#{u_username},#{u_password},#{u_sex},#{u_createTime},#{u_cid})
	</insert>
	
	<!-- 修改用户 -->
	<update id="updateUser" parameterType="com.bean.User">
		update user set u_username=#{u_username} where u_id=#{u_id}
	</update>
	
	<!-- 根据id删除用户 -->
	<delete id="deleteUserById" parameterType="Integer">
		delete from user where u_id=#{id}
	</delete>
</mapper>
```

db.properties

```
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql:///ssm_mybatis?serverTimezone=UTC
jdbc.username=root
jdbc.password=123456
```

sqlMapConfig.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
  
<configuration>
	<!-- 读取配置文件
		将配置的属性与当前文件进行隔离
	 -->
	<properties resource="db.properties"/>

	<!-- 用于简写UserMapper的resultType和parameterType的名称
		推荐使用package包的形式来配置别名
		包的形式会扫描主包以及子包下的所有文件
		以对象类名为别名，大小写不限，推荐使用小写
	 -->
	<typeAliases>
		<package name="com.bean"/>
		<!-- <typeAlias type="com.bean.User" alias="user"/> -->
	</typeAliases>

	<!-- 继承spring后不需要配置 -->
  <environments default="development">
    <environment id="development">
    <!-- 使用jdbc事务 -->
      <transactionManager type="JDBC"/>
      <!-- 使用连接池连接数据库 -->
      <dataSource type="POOLED">
        <property name="driver" value="${jdbc.driver}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
      </dataSource>
    </environment>
  </environments>
  
  <mappers>
    <!-- <mapper resource="mapper/UserMapper.xml"/> --> 
    <!-- <mapper class="com.mapper.UserMapper"/> --> 
    <!-- 配置映射器的位置,接口的文件要和xml文件名字一致，且在同一个包下 -->
    <package name="com.mapper"/>
  </mappers>
</configuration>
```

