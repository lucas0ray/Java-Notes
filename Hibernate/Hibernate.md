#Hibernate框架
##jar库：[https://mvnrepository.com/](https://mvnrepository.com/)
##1.添加hibernate依赖
	org.hibernate hibernate-core

	<dependency>
    	<groupId>org.hibernate</groupId>
    	<artifactId>hibernate-core</artifactId>
		<version>5.4.2.Final</version>
	</dependency>
##2.对数据库进行操作 添加mysql依赖
	mysql-connector-java

	<dependency>
  		<groupId>mysql</groupId>
  		<artifactId>mysql-connector-java</artifactId>
  		<version>8.0.16</version>
  	</dependency>
##3.J2SE-1.5问题
	```ruby
	<build>
	<finalName>WinXin</finalName>
	<plugins>  
        <plugin>    
        <groupId>org.apache.maven.plugins</groupId>    
        <artifactId>maven-compiler-plugin</artifactId>    
        <configuration>    
            <source>1.8</source>    
            <target>1.8</target>    
        </configuration>    
        </plugin>  
      </plugins>  
	</build>```
##4.创建数据库表-->>创建持久化po类对应数据库表
##5.在resources中创建类与表之间的映射文件
###类名.hbm.xml-->>声明dtd文件
**Libraries-->>
Maven Dependencies-->>
hibernate-core-x.x.x.Final.jar-->>
org.hibernate核心包-->>
hibernate-mapping-3.0.dtd
大概10-13行左右-->><!DDCTYPE开头dtd">结尾-->>为dtd文件声明**

	```ruby
	<!DOCTYPE hibernate-mapping PUBLIC 
    "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
    "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">```
	
###1.创建hibernate-mapping标签-->>创建class标签neme属性对应po类table属性为数据库表-->>内创建类映射主键为id标签 name属性为类里的id属性名，column属性为数据库表的主键字段名，主键映射需要在内指明主键生成策略generator标签 class属性暂时为native2.除去主键其他的属性声明为property 标签name属性与column属性对应

	```ruby
	<hibernate-mapping>
	<class name="po.Emp" table="emp">
		<id name="empno" column="empno">
			<generator class="native"></generator>
		</id>
		<property name="ename" column="ename"></property>
	</class>
	</hibernate-mapping>```

###1.在resources 创建链接数据库的配置信息hibernate.cfg.xml文件，核心包中的第一个 hibernate-conliguration-3.0.dtd文件大概10-13
	```
	<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
	```


9.	创建hibernate-configuration标签，内创建session-factory标签的session工厂，内创建property标签name属性配置数据库链接的属性username为用户名，password密码，url为jdbc:mysql://localhost:3306/数据库的名字，driver_class到mysql包中找driver类，com.mysql.jdbc.Driver，数据库的方言diolect用于生成sql语句在hibernate包里，MySQLDialect org.hibernate.dialect.MySQLDialect，想在控制台看到生成的sql语句配置show_sql为true
10.	hibernate只读一个配置文件 不会读映射文件，所以需要使用mapping标签 resource属性映射文件名
	```
	<hibernate-configuration>
	<session-factory>
		<property name="uername">root</property>
		<property name="password">root</property>
		<property name="url">jdbc:mysql://localhost:3306/数据库名称</property>
		<property name="driver_class">com.mysql.jdbc.Driver</property>
		<property name="dialect">org.hibernate.dialect.MySQLDialect</property>
		<property name="show_sql">true</property>
		<mapping resource="emp.hbm.xml"/>
	</session-factory>
	</hibernate-configuration>```