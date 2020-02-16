# Mybatis_04

输出映射

resultType,resultMap

两者必须选择其中一个

resultMap可以自定义字段的映射

resultType就不行

对于多表查询，映射需要一一列出

### 两个表的联合查询

一一列出需要映射的值

```xml
<!-- 查询所有用户的包装类 -->
	<resultMap type="UserVo" id="uservolist">
        <!-- 使用id代表每个表的主键，result代表每个表的属性值 -->
		<id property="u_id" column="u_id"/>
		<result property="u_username" column="u_username"/>
		<result property="u_sex" column="u_sex"/>
		<association property="country" javaType="Country">
			<id property="id" column="c_id"/>
			<result property="c_countryname" column="c_countryname"/>
		</association>
	</resultMap>
	<select id="selectAllUserVo" resultMap="uservolist">
		select u.`u_id`,u.`u_username`,u.`u_sex`,c.`c_id`,c.`c_countryname` from user u left join country c on u.`u_cid`=c.`c_id`
	</select>
```

一对多关系查询

使用list表示即可

```xml
<!-- 
	//查询所有的countryVo
	List<CountryVo> selectAllCountryVo();
	 -->
	 <resultMap type="CountryVo" id="countryVo">
	 	<id property="id" column="c_id"/>
	 	<result property="c_countryname" column="c_countryname"/>
	 	<result property="c_capital" column="c_capital"/>
	 	<!-- 一对多关系 -->
	 	<collection property="userList" ofType="User">
	 		<id property="u_id" column="u_id"/>
	 		<result property="u_username" column="u_username"/>
	 	</collection>
	 </resultMap>
	<select id="selectAllCountryVo" resultMap="countryVo">
		select 
		c.`c_id`,
		c.`c_countryname`,
		c.`c_capital`,
		u.`u_id`,
		u.`u_username` 
		from country c 
		left join 
		user u on 
		u.`u_cid`=c.`c_id`
	</select>
```

