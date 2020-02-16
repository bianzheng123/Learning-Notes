# Mybatis_05

## 动态sql

用于整合sql语句

#### if标签

```sql
select * 
		from user
		where
		<if test="u_sex != null and u_sex != ''">
			u_sex=#{u_sex}
		</if>
		<if test="u_username != null and u_username != ''">
			and u_username like "%"#{u_username}"%"
		</if>
		<if test="u_cid != null">
			and u_cid=#{u_cid}
		</if>
```

#### where标签

防止出现多加或者少加了and关键字的情况

```xml
select *
		from user
		<where>
		<!-- where标签可以去掉开头的and -->
			<if test="u_sex != null and u_sex != ''">
				and u_sex=#{u_sex}
			</if>
			<if test="u_username != null and u_username != ''">
				and u_username like "%"#{u_username}"%"
			</if>
			<if test="u_cid != null">
				and u_cid=#{u_cid}
			</if>
		</where>
```

#### trim标签

定制where标签的规则

prefix:前置标签替换

suffix：将属性替换到标签的结尾处

#### set标签

解决更新数据表时字符串拼接逗号","的问题

#### foreach标签

用于进行遍历

```xml
<!-- 	//使用多个id获取用户列表
	public List<User> selectUserListByList(); -->
	<select id="selectUserListByList" resultType="User">
		select *
		from user
		where u_id
		in
		<!-- (1,2,3) -->
        <!-- 使用包装类的list作为输入参数时，需要写属性的字段名，否则就写数据结构名(list,array等) -->
		<foreach collection="list" item="id" open="(" close=")" separator=",">
			#{id}
		</foreach>
		
	</select>
```

#### sql标签

用于简写不同的包名

可以提取重复sql语句片段