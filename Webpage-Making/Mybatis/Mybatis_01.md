# Mybatis_01

和hibernate相比，mybatis可以将多个sql语句整合在一个文件中

操作步骤

配置连接池(sqlMapConfig.xml)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
  
<configuration>
<!-- 继承spring后不需要配置 -->
  <environments default="development">
    <environment id="development">
    <!-- 使用jdbc事务 -->
      <transactionManager type="JDBC"/>
      <!-- 使用连接池连接数据库 -->
      <dataSource type="POOLED">
        <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql:///ssm_mybatis?serverTimezone=UTC"/>
        <property name="username" value="root"/>
        <property name="password" value="123456"/>
      </dataSource>
    </environment>
  </environments>
  
  <mappers>
    <mapper resource="mapper/UserMapper.xml"/>
  </mappers>
</configuration>
```

创建user这个模型

配置UserMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="UserMapper">
	<select id="selectUserById" parameterType="Integer" resultType="com.bean.User">
        <!-- #{}代表占位符，通过代码填写需要的参数 -->
		select * from user where u_id=#{id}
	</select>
	
	<!-- ${}代表字符串拼接 -->
	<select id="selectUserByName" parameterType="String" resultType="com.bean.User">
        <!-- ${}用于字符串的拼接 -->
		select * from user where u_username like '%${value}%'
	</select>
    
    <!-- 添加用户 -->
	<insert id="insertUser" parameterType="com.bean.User">
        <!-- 当传递的参数是对象时，命名的属性名一定要和对象的变量名一致 -->
		insert into user values(null,#{u_username},#{u_password},#{u_sex},#{u_createTime},#{u_cid})
	</insert>
</mapper>
```

编写测试代码

```xml
	@Test
	//通过id查询用户
	public void Test1() throws IOException {
            String resource = "sqlMapConfig.xml";
            //读取配置文件
            InputStream in = Resources.getResourceAsStream(resource);
            //需要sqlSessionFactoryBuilder
            SqlSessionFactoryBuilder ssfb = new SqlSessionFactoryBuilder();
            //创建sqlSessionfactory
            SqlSessionFactory ssf = ssfb.build(in);
            //生产一个sqlSession
            SqlSession session = ssf.openSession();
            //操作数据库
            //参数一 ：要操作的sql语句  	参数二：sql语句的参数
            User user = session.selectOne("UserMapper.selectUserById",1);
            System.out.println(user);
        }
	
	@Test
	//通过用户名模糊查找匹配的用户列表
	public void Test2() throws IOException {
		String resource = "sqlMapConfig.xml";
		//读取配置文件
		InputStream in = Resources.getResourceAsStream(resource);
		//需要sqlSessionFactoryBuilder
		SqlSessionFactoryBuilder ssfb = new SqlSessionFactoryBuilder();
		//创建sqlSessionfactory
		SqlSessionFactory ssf = ssfb.build(in);
		//生产一个sqlSession
		SqlSession session = ssf.openSession();
		//操作数据库
		//参数一 ：要操作的sql语句  	参数二：sql语句的参数
		List<User> list = session.selectList("UserMapper.selectUserByName","王");
		for (User u : list) {
			System.out.println(u);
		}
	}
            
    @Test
	//添加用户
	public void Test3() throws IOException {
		String resource = "sqlMapConfig.xml";
		//读取配置文件
		InputStream in = Resources.getResourceAsStream(resource);
		//需要sqlSessionFactoryBuilder
		SqlSessionFactoryBuilder ssfb = new SqlSessionFactoryBuilder();
		//创建sqlSessionfactory
		SqlSessionFactory ssf = ssfb.build(in);
		//生产一个sqlSession
		SqlSession session = ssf.openSession();
		//操作数据库
		//参数一 ：要操作的sql语句  	参数二：sql语句的参数
		User user = new User();
		user.setU_username("卞证");
		user.setU_password("123456");
		user.setU_sex("1");
		user.setU_createTime(new Date());
		user.setU_cid(1);
		
		session.insert("UserMapper.insertUser",user);
		session.commit();
	}
```

