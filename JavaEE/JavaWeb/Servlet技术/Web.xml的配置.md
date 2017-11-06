#### web.xml文件是用来配置：欢迎页、Servlet、filter等的。当web工程没用到这些时可以不要web./xnl文件来配置web工程。



#### 1.每个web.xml的文件的根元素<web-app>中，都必须表明这个web.xml使用的是哪个模式文件。如：

<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.5" 
​	 xmlns="<http://java.sun.com/xml/ns/javaee>"
​	 xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>"
​	 xsi:schemaLocation="<http://java.sun.com/xml/ns/javaee>
​	 <http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd>"
</web-app>



#### 2.web.xml常用标签就功能：

###### 》》1、指定欢迎页面：

 	 <welcome-file-list>
   		 <welcome-file>index.jsp</welcome-file>
   		 <welcome-file>index1.jsp</welcome-file>
 	 </welcome-file-list>

​	指定了两个欢迎页面，在第一个不存在的情况下，显示第二个。

###### 》》2、为Servlet命名：

​	<servlet>
  	 	 <servlet-name>servlet1</servlet-name>
   		 <servlet-class>net.test.TestServlet</servlet-class>
​	</servlet>

###### 》》3、为Servlet定制URL：

​	<servlet-mapping>
  		  <servlet-name>servlet1</servlet-name>
   		 <url-pattern>*.do</url-pattern>
​	</servlet-mapping>

###### 》》4、定制初始化参数：

​	可以定制Servlet、JSP、Context的初始化参数，然后在Servlet、JSP、Context中获取这些参数值。如：

​	<servlet>
 	   <servlet-name>servlet1</servlet-name>
 	   <servlet-class>net.test.TestServlet</servlet-class>
 	  <init-parm>
​       	 	<param-name>userName<param-name>
​         	<param-value>Tommy<param-value>
 	 </init-param>
  	  <init-param>
​        	  <param-name>E-mail</param-name>
​         	 <param-value>Tommy@163.com</param-value>
  		  </init-param>
​	</servlet>

经过配置，在Servlet中能够调用getServletConfig().getInitParam("param1")获得参数名对应的值。















