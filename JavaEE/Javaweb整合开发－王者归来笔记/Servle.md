# 				Servlet

### Servlet是什么？

​	Servlet是运行在服务器上的小程序。一个Servlet就是一个Java类，并且通过“请求-响应”编程模型来访问的这个驻留在服务器内存里的Servlet程序

### 编写Servlet

1. 继承HttpServlet
2. 重写doGet()或doPost()
3. 在web.xml中注册Servlet（有的ida会自动配置）







JavaWeb项目中web.xml有关servlet的基本配置

```
<servlet>
    <servlet-name>servlet的名称（自己起的，不要重复）</servlet-name>
    <servlet-class>Servlet的类的路径</servlet-class>
</Servlet>
 <Servlet-mapping>
    <param-name>Servlet的名称（与上面的一样）</param-name>
    <uri-pattern>/uri名字（自己起的，不要重复，注意“/”不能丢）
<Servlet-mapping>
```













