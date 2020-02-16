# Mybatis_02

## 字符串和占位符的区别

#{}占位符

- 尽量选用占位符解决问题

- 程序会自动添加单引号
- `王->'王'`

${}字符串拼接

- 仅仅是字符串拼接，不会做任何变化
- 里面的名字只能是value

### 字符串拼接转换成占位符

对于sql语句

`select * from user where u_username like '%王%'`

使用字符串拼接表示

`select * form user whre u_username like '%${value}%'`

占位符

`select * from user where u_username like "%"#{name}"%"`