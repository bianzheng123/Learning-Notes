# Hibernate_02

hibernate与c3p0进行对比

- 创建
  - hibernate
    - 创建hibernate.cfg.xml
    - 配置驱动，数据库url，用户名，密码
    - 数据库的方言
  - c3p0+dbutils
    - c3p0
      - 连接数据库
      - 配置驱动，数据库url，用户名，密码
    - dbutils
      - 操作数据库
- 添加实体
  - hibernate
    - 需要实体与表的映射文件xxx.hbm.xml
      - 需要配置属性与字段的对应，添加主键生成策略
  - c3p0+dbutils
    - 需要实体
- 操作数据库
  - hibernate
    - 通过session去操作数据库（开启事务）
      - 不用写sql语句（hibernate帮你写），一样代码解决
  - c3p0+dbutils
    - queryrunner操作数据库
      - 写sql语句
      - 相比于hibernate比较麻烦

