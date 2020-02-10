# Hibernate_04

## HQL

**完全的面向对象**

HQL不能出现表中的任何内容

#### 基本查询

```java
public void search() {
    Session session = HibernateUtils.getSession();
    Transaction beginTransaction = session.beginTransaction();

    //////////////////////////////////
    //操作
    String hql = "from com.domain.User";
    //将user表对应的内容放到User类中
    Query query = session.createQuery(hql);
    List<User> list = query.list();//返回多条数据
    //		User user = (User) query.uniqueResult();//查询唯一数据

    System.out.println(list);
    /////////////////////////////////////

    beginTransaction.commit();
    session.close();
}
```

#### 条件查询

```java
//select * from user where id=1
String hql = "from com.domain.User where id=?0";
//问号要紧跟数字，代表索引
Query query = session.createQuery(hql);
query.setParameter(0,"1");
User user = (User)query.uniqueResult();
System.out.println(user.getUsername());
```

```java
//select * from user where id=1
String hql = "from com.domain.User where id=:id";
//冒号后面跟上要表示字符的索引
Query query = session.createQuery(hql);
query.setParameter("id","1");
User user = (User)query.uniqueResult();
System.out.println(user.getUsername());
```

#### 分页查询

```java
//select * from user limit 0,1
String hql = "from com.domain.User";
Query query = session.createQuery(hql);
query.setFirstResult(2);
//代表查询的是第几页
query.setMaxResults(1);
//代表每一页的查询个数
List<User> list = query.list();
System.out.println(list);
```

## Criteria

头部和尾部与HQL相似，这里不写了

#### 基本查询

```java
CriteriaBuilder criteriaBuilder = session.getCriteriaBuilder();
//createQuery-->查询条件(首先要知道查询什么类型数据)
CriteriaQuery<User> createQuery = criteriaBuilder.createQuery(User.class);
Root<User> from = createQuery.from(User.class);
createQuery.select(from);
//得到所有user表中的数据
List<User> resultList = session.createQuery(createQuery).getResultList();
System.out.println(resultList);
```

#### 条件查询

```java
CriteriaBuilder criteriaBuilder = session.getCriteriaBuilder();
//createQuery-->查询条件(首先要知道查询什么类型数据)
CriteriaQuery<User> criteria = criteriaBuilder.createQuery(User.class);
Root<User> root = criteria.from(User.class);
criteria.select(root).where(root.get("id").in("1"));
//select * from user where id in (1)
List<User> resultList = session.createQuery(criteria).getResultList();
System.out.println(resultList);
```

#### 聚集函数

```java
//select count(*) from user
CriteriaBuilder criteriaBuilder = session.getCriteriaBuilder();
//createQuery-->查询条件(首先要知道查询什么类型数据)(数Integer Long)
CriteriaQuery<Long> criteria = criteriaBuilder.createQuery(Long.class);
Root<User> root = criteria.from(User.class);
criteria.select(criteriaBuilder.count(root));
//执行查询
Long count  = session.createQuery(criteria).uniqueResult();
System.out.println(count);
```

```java
//select count(*) from user where username like '%i%'
CriteriaBuilder criteriaBuilder = session.getCriteriaBuilder();
CriteriaQuery<Long> criteria = criteriaBuilder.createQuery(Long.class);
Root<User> root = criteria.from(User.class);
criteria.select(criteriaBuilder.count(root)).where(criteriaBuilder.like(root.get("username"), "%i%"));
Long count = session.createQuery(criteria).uniqueResult();
System.out.println(count);
```

## SQL

#### 基本查询

```java
public void fun() {
    Session session = HibernateUtils.getSession();
    Transaction beginTransaction = session.beginTransaction();

    String sql = "select * from user";
    //创建sql查询对象
    NativeQuery query = session.createSQLQuery(sql);
    //封装数据
    query.addEntity(User.class);
    //接收list
    List<User> list = query.list();
    //接受单一返回值
    //query.uniqueResult();
    System.out.println(list);

    beginTransaction.commit();
    session.close();
}
```

##### 条件查询

```java
public void fun2() {
    Session session = HibernateUtils.getSession();
    Transaction beginTransaction = session.beginTransaction();

    String sql = "select * from user where id=?";
    //创建sql查询对象
    NativeQuery query = session.createSQLQuery(sql);
    //给?赋值
    query.setParameter(1, "1");
    //封装数据
    query.addEntity(User.class);
    //接收list
    //	    List<User> list = query.list();
    //接受单一返回值
    User user = (User)query.uniqueResult();
    System.out.println(user);

    beginTransaction.commit();
    session.close();
}
```

