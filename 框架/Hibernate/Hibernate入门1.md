## 1、使用jdbc进行数据库操作的缺点

----------需要编写大量的SQL语句

----------需要设置大量的参数值

-----------需要将ResultSet记录转换成POJO对象

-----------数据库变更某些特殊功能需要改变SQL，简称移植性差。列如分页查询、主键生成方法，数据库函数等

## 2、Hibernate设计思想、

##### 优点：

hibernate采用ORM思想对JDBC进行封装，解决jdbcde不足

--------------自动生成SQl语句

--------------自动设置参数值

---------------自动将ResultSet记录映射成POJO

---------------采用一致的方法对数据库操作。列如分页查询和主键生成控制。移植性比较好。

	save(admin);//insert语句
	update(admin);//update语句
	Admin admin=(Admin)load();//findByld语句
##### ORM：

Object Relation Mapping，对象关系映射。解决java对象和关系数据库之间的映射关系。

​	hibernate框架是ORM的一种实现，解决了对象和数据库映射问题。在数据库添加或更新时，可以将一个对象自动写入或更新数据表；查询时，可以将记录自动封装成对象返回。这些操作在中间执行时涉及的一些细节开发者不要参与和关注。

## 3、Hibernate框架体系结构

#### a、hibernate.cfg.xml(1个)：

是hibernate框架的配置文件。可以配置数据库连接参数、hibernate框架参数等。

#### b、POJO()实体类(n个)：

指与数据库对应的实体类，用于封装数据库记录的对象类型。

#### c、hbm.xml映射描述文件(n个)：

指定了实体类与数据表的对应关系，类中属性和数据表字段之间对应关系。

#### d、hibernate顶层的API(jar包)：

主要是对hbm.xml解析，根据写出的内容，动态生成SQL语句，自动将属性和字段映射。

## 4、Hibernate框架常用API

##### a、Configuration：

负责加载hibernate.cfg.xml主配置信息，同时也可以加载hbm.xml信息。

##### b、SessionFaction

负责加载创建Session对象，对jdbc的connection对象的封装。

##### c、Session

负责执行增删改操作，提供了save，update、delete等方法。

##### d、Transaction

负责事务控制

##### e、Query

负责执行特殊查询。

## 5、Hibernate基本应用

1. ##### 引入hibernate开发包、数据库驱动包

2. ##### 引入hibernate主配置文件hibernate.cfg.xml

3. ##### 添加实体类Cost

4. ##### 描述Cost.hbm.xml映射描述

5. ##### 根据Hibernate提供的常用API执行增删改查操作

