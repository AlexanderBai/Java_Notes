在hibernate.cfg.xml出现如下错误

Attribute "resoure" must be declared for element type "mapping".

![捕获](C:\Users\bbg28\Documents\Java笔记\Error\框架\捕获.PNG)

这是因为自己复制了hibernate.cfg.xml头部文件

不应该用hibernate-cofiguration,应修改为mapping的头文件

![捕获1](C:\Users\bbg28\Documents\Java笔记\Error\框架\捕获1.PNG)