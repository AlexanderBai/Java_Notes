1. DBCP简介：

   DBCP(DateBase connnection pool)数据库连接池是apache上的一个Java连接池项目。DBCP通过连接池预先同数据库建立一些连接，放在在内存中（连接池）。当需要对数据库进行操作时，不需要进行连接，只需从连接池中拿取，用完后连接池回收连接，以达到重用连接，减少资源耗费。

2. DBCP依赖的包：

     commons-dbcp2-2.1.1.jar       commons-logging-1.2.jar       commons-pool2-2.4.2.jar

3. 创建config目录，用于存放DBCP的配置文件：dbcp.properties

![捕获2](C:\Users\bbg28\Documents\Java笔记\JavaEE\JavaWeb\捕获2.PNG)