# Mybatis_06

mybatis generator

生成sql的配置文件

generatorConfig.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
  PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
  "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>
	<!-- 配置数据库连接的包 -->
  <!-- <classPathEntry location="/Program Files/IBM/SQLLIB/java/db2java.zip" /> -->
  <context id="MyGererator" targetRuntime="MyBatis3">
  
  <!-- 这个标签可以去掉注释 -->
  <commentGenerator>
  <!-- 去掉注释 -->
  	<property name="suppressAllComments" value="true"/>
  <!-- 去掉时间戳 -->
  	<property name="suppressDate" value="true"/>
  </commentGenerator>
  
  
  <!-- 数据库连接信息 -->
    <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
        connectionURL="jdbc:mysql://localhost:3306/ssm_mybatis?serverTimezone=UTC"
        userId="root"
        password="123456">
        <!-- 防止数据库版本过高 -->
        <property name="nullCatalogMeansCurrent" value="true"/>
    </jdbcConnection>

	<!-- JAVA JDBC数据类型转换 -->
    <javaTypeResolver >
      <property name="forceBigDecimals" value="false" />
    </javaTypeResolver>

	<!--  javaModelGenerator javaBean配置
	targetPackage 输入包名 输出路径
	targetProject 输出项目位置 -->
    <javaModelGenerator targetPackage="com.bean" targetProject="src">
    <!-- enableSubPackages 是否开启子包名称 是否在包名后边加上scheme名称 -->
      <property name="enableSubPackages" value="false" />
      <!-- 在Set中加入.trim -->
      <property name="trimStrings" value="true" />
    </javaModelGenerator>

	<!-- mapper.xml -->
    <sqlMapGenerator targetPackage="com.mapper"  targetProject="src">
      <property name="enableSubPackages" value="false" />
    </sqlMapGenerator>

	<!-- java接口  -->
    <javaClientGenerator type="XMLMAPPER" targetPackage="com.mapper"  targetProject="src">
      <property name="enableSubPackages" value="true" />
    </javaClientGenerator>

	<!-- 数据表 要根据数据库中的表来生成  -->
	<table tableName="user"/>
	<table tableName="country"/>
	
    <!-- <table schema="DB2ADMIN" tableName="ALLTYPES" domainObjectName="Customer" >
      <property name="useActualColumnNames" value="true"/>
      <generatedKey column="ID" sqlStatement="DB2" identity="true" />
      <columnOverride column="DATE_FIELD" property="startDate" />
      <ignoreColumn column="FRED" />
      <columnOverride column="LONG_VARCHAR_FIELD" jdbcType="VARCHAR" />
    </table> -->
  </context>
</generatorConfiguration>
```

生成代码

```java
public static void main(String[] args) throws Exception {
		  List<String> warnings = new ArrayList<String>();
		   boolean overwrite = true;
		   File configFile = new File("src/generatorConfig.xml");
		   ConfigurationParser cp = new ConfigurationParser(warnings);
		   Configuration config = cp.parseConfiguration(configFile);
		   DefaultShellCallback callback = new DefaultShellCallback(overwrite);
		   MyBatisGenerator myBatisGenerator = new MyBatisGenerator(config, callback, warnings);
		   myBatisGenerator.generate(null);
	}
```

