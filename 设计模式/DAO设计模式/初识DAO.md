####     1、  DAO(Date Access Object,数据访问对象)：

​			主要用于进行数据操作，在程序的标准开发框架中属于数据层的操作。

#### 	2、数据开发结构：

![img](http://img.blog.csdn.net/20141207130012401?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdGh5c3Rhcg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

资源层是数据库的操作层，可以存储各种数据，依赖于SQL语句，数据层通过一个专门的数据库组件来完成对数据库的操作。

业务层是整个项目的核心。



#### 3、DAO组成

1. DatabaseConnection：专门负责数据库打开与关闭操作的类；

2. VO：主要由属性，setter，getter方法组成，VO类中的属性与表中的字段相对应，每一个VO类的对象都表示数据库中的每一条记录；

3. DAO：主要定义操作的接口，定义一系列数据库的原子性操作，列如增删改查等；

4. Impl：DAO接口的真实实现类，完成具体的数据库操作，但不负责数据库的打开与关闭；

5. Proxy：代理实现类，主要完成数据库的打开和关闭并且调用真实实现类对象的操作；

6. Factory：工厂类，通过工厂类取得一个DAO的实列对象。

   ​		

   #### 4、在使用DAO时对包有严格的命名

7. 数据库连接：xxx.dbc.DataConnection

8. DAO接口：xxx.dao.IXxxDAO

9. DAO接口真实实现类：xxx.dao.impl.XxxDAOImpl

10. DAO接口代理类：xxx.dao.proxy.XxxDAOProxy

11. VO类：xxx.vo.Xxx,VO命名要与表中的命名一致

12. 工厂类：xxx.factory.DAOFactory.

    ​

    #### 5、DAO与DBUtils区别

    DBUtils是工具类，理论上应该所有的方法都是static的；

    DAO是访问数据库的一种模式，是数据处理接口，提交数据到数据库时，需要使用一些工具类，比如DBUtils主要用于数据库连接、关闭数据库连接(getConnection,close)

