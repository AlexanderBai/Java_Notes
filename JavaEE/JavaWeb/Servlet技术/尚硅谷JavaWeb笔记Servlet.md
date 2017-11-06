1. ### Java Web应用有一组Servlet、HTML页、类、以及其它可以被绑定的资源构成。它可以在实现Servlet规范的Servlet容器中运行。

   ​

2. ### Java Web应用中可有：

------Servlet

-------JSP

--------实用类

--------静态文档如HTML、图片等

--------描述Web应用的信息（web.xml)![捕获](C:\Users\bbg28\Documents\Java笔记\JavaEE\JavaWeb\捕获.PNG)

![捕获1](C:\Users\bbg28\Documents\Java笔记\JavaEE\JavaWeb\捕获1.PNG)

Java Servlet是和平台无关的服务器端组件，运行在Servlet容器中。Servlet容器负责Servlet和客户的通信以及调用Servlet的方法。Servlet和客户的通信采用“请求/响应”的模式。

### web.xml配置

     <servlet>
      	<!-- Servlet注册的名字 -->
        <servlet-name>MyServlet</servlet-name>
        <!-- Servlet的全类名 -->
        <servlet-class>com.bbg.servlet.MyServlet</servlet-class>
     </servlet>
      <servlet-mapping>
      	<!-- 需要和某个servlet节点的servlet子节点的文本节点一致 -->
        <servlet-name>MyServlet</servlet-name>
        <!-- 映射具体的访问路径：/代表当前Web应用的根目录 -->
        <url-pattern>/myservlet</url-pattern>
        <!-- 可以指定 Servlet 被创建的时机 -->
    	<load-on-startup>-1</load-on-startup>
      </servlet-mapping>
一个servlet可以有多个<servle-mappingt>对其映射

可以使用url的通配符（*.扩展名）或（/*）

<url-pattern>*.html<url-pattern>*

或<url-pattern>/*<url-pattern>

而<url-pattern>/*.HTML<url-pattern>不合法



###  Servlet容器：运行Servlet、JSP、Filter、Listener、Tag等的软件。

1. 可以来创建Servlet，并调用Servlet的相关生命周期方法。

2. JSP、Filter、Listener、Tag....

   ​

### Servlet生命周期的方法：以下方法都是Servlet容器负责调用

1. 构造器： 只被调用一次，只有第一次请求Servlet时，创建Servlet的实列，调用构造器，这说明Servlet的单实列！
2. init方法：只被调用一次，在创建实列后立即被调用，用于初始化当前的Servlet。
3. service方法：被多次调用，每次请求都会调用service方法，实际用于响应请求
4. destroy方法：只被调用一次，在当前servlet所在的web应用被卸载前调用。用于释放当前servlet所占用的资源。



### load-on-startup参数：

1. 配置在servlet节点中

     <servlet>
      	<!-- Servlet注册的名字 -->
        <servlet-name>MyServlet</servlet-name>
        <!-- Servlet的全类名 -->
        <servlet-class>com.bbg.servlet.MyServlet</servlet-class>
        <!-- 可以指定 Servlet 被创建的时机 -->
        <load-on-startup>-1</load-on-startup>
     </servlet>
      <servlet-mapping>
      	<!-- 需要和某个servlet节点的servlet子节点的文本节点一致 -->
        <servlet-name>MyServlet</servlet-name>
        <!-- 映射具体的访问路径：/代表当前Web应用的根目录 -->
        <url-pattern>/myservlet</url-pattern>
      </servlet-mapping>	
     2.load-on-startup：可以指定servlet被创建的时机。若为负数，则在第一次请求时被创建，若为0或正数，则在当前web应用被Servlet容器加载时创建实列，且数字越小越早创建。






### 设置初始化参数

    <servlet>
      	<!-- Servlet注册的名字 -->
        <servlet-name>MyServlet</servlet-name>
        <!-- Servlet的全类名 -->
        <servlet-class>com.bbg.servlet.MyServlet</servlet-class>
        <!-- 配置servlet的初始化参数.且节点必须在 load-on-startup 节点的前面-->
        <init-param>
            <!-- 参数名 -->
            <param-name>user</param-name>
            <!-- 参数值 -->
            <param-value>root</param-value>    	
        </init-param>
        <init-param>
            <param-name>password</param-name>
            <param-value>bbg</param-value>
        </init-param>
        <load-on-startup>-1</load-on-startup>
      </servlet>


### 获取初始化参数：



		String user=config.getInitParameter("user");	
		System.out.println("user:"+user);
		Enumeration<String> names=config.getInitParameterNames();
		while(names.hasMoreElements()){
			String name=names.nextElement();
			String value=config.getInitParameter(name);
			System.out.println("name:"+name+"  value:"+value);
		}


### 获取Servlet的名称

		String name1=config.getServletName();
		System.out.println(name1);
### Servlet Context

1. #### 可以由Servlet Config获取：

   #### ServletConfig封装了servlet的配置信息，并且可以获得servletContext的对象

2. #### 该对象代表当前web应用：

   可以认为ServletContext是当前web应用中的一个大管家，可从中获取到当前web应用的各个方面的信息。

   ##### （1）、获取web应用初始化的参数

   设置初始化参数：可以为所有的Servlet所获取，而Servlet的初始化参数只用那个Servlet可以获取

   <context-param>
     	<param-name>driver</param-name>
     	<param-value>com.mysql.jdbc.Driver</param-value>
     </context-param>

   方法： 

   getInitParameter

   getInitParameterNames

   ##### （2）、 获取当前web应用的某一个文件的决定路径，而不是部署前的路径

   getRealPath(String path);

   ##### （3）、获取当前web应用的名称：

   getContextPath()

   ##### （4）、获取当前web应用的某一个文件对应的输入流 ：

   getREsourceAsStream(String Path):Path的 / 为当前web应用的根目录。

   java.io.InputStream is2=servletcontext.getResourceAsStream("/WEB-INF/class/jdbc.proties");
   ​			

   ================================================================================================================================================================================

   ## 														应答请求

   1. #### 如何在Servlet中获取请求参数

   servlet的service（）方法用于应答请求：每次请求都会调用一次service（）方法。

   protected void service(HttpServletRequest request, HttpServletResponse response) 

   throws ServletException, IOException


   ######     HttpServletRequest ：封装了请求信息，可以从中获取任何的请求信息

   ######     HttpServletResponse：封装了响应信息，想给用户什么信息，具体可以使用该接口的方法实现

   这两个接口的实现都是服务器给予的，在服务器调用service方法时传入。

   2.  #### 获取请求参数

       > String getParameter(String name):根据请求参数的名字，返回参数值。若请求参数有多个值（列如checkbox），该方法只能获取到第一个提交值。
       >
       > ​
       >
       > String[]  getParameterValue(Sting name):根据请求参数的名字，返回请求参数对应的字符串数组。
       >
       > ​
       >
       > Map getParameterMap():返回参数名对应的Enumeration对象，类似于Servlet Context（或Servlet fig）的getInitParameterNames()方法。
       >
       > ​
       >
       > Enumeration getPasrameterNames():返回请求参数的键值对，key:参数名，value：参数值，String数组类型
       >
       > ​

       ###### 	（1）、获取请求的URL:

       String requestURl=request.getRequestURI();
       System.out.println(requestURl);

       ###### 	(2)、获取请求方式：

       String method=request.getMethod();
       System.out.println(method);
       ###### 	(3)、获取请求的参数字符串：

       	String queryString=request.getQueryString();
       	System.out.println(queryString);

> 若是get请求，获取请求参数对应的那个字符串，即 ？后的那个字符串。
>
> 若是post请求，获取为null。

###### 		(4)、获取请求的Servlet的映射路径：

		String servletPath=request.getServletPath();
		System.out.println(servletPath);

###### 		(5)、和attribute相关的几个方法：



#### 3.HttpServletRequest：

HttpServletRequest是Servlet Request的子接口，针对HTTP请求所定义，里面包含了大量获取HTTPi请求的方法。

> 1. getWriter():返回Print Writer对象，调用peint()方法，将print()中的参数直接打印到客户的浏览器上
> 2. 设置响应的文档类型：response.setContentType("application/msword");
> 3. void sendRedirection(String location):请求重定向。（此方法是HttpServletResponse中定义的。



----------------------------------------------------------------------------------------------------------------------------------------------------------------

## 						知识巩固

在 web.xml 文件中设置两个 WEB 应用的初始化参数, user, password.
定义一个 login.html, 里边定义两个请求字段: user, password. 发送请求到 loginServlet
再创建一个 LoginServlet, 在其中获取请求的 user, password. 比对其和 web.xml 文件中定义的请求参数是否一致
若一致, 响应 Hello:xxx, 若不一致, 响应 Sorry: xxx  xxx 为 user.

## 				GenericServlet：

1、GenericServlet是一个接口，是Servlet和ServletConfig接口的实现类。但是是一个抽象类，因为其中的service方法为抽象方法。

2、如果新建的servlet程序直接继承GenericServlet会使开发简洁。

3、具体实现：

①.在Genericservlet中声明了一个ServletConfig类型的成员变量，在init(ServletConfig)方法中对其进行了初始化

②.利用servletConfig成员变量的方法实现了ServletConfig接口的方法。

③.还定义了一个init()方法，在init(ServletConfig)方法中对其进行调用，子类可以直接覆盖init()在其中实现对Servlet的初始化。

④.不介意直接覆盖init(ServletConfig),因为如果忘记编写super(ServletConfig)，而还是用了ServletConfig接口的方法，则会出现空指针异常。

⑤.新建的init(){}并非Servlet的生命周期的方法，而init(ServletConfig)是生命周期相关的方法。

 * ​
     package com.atguigu.javaweb;
     ​	
     	import java.io.IOException;

     	import java.util.Enumeration;

     	import javax.servlet.Servlet;

     	import javax.servlet.ServletConfig;

     	import javax.servlet.ServletContext;

     	import javax.servlet.ServletException;

     	import javax.servlet.ServletRequest;

     	import javax.servlet.ServletResponse;

     	/**

     	- 自定义的Servlet接口的实现类：
     	- 让开发的任何Servlet都继承该类，以简化开发
     	  */
     	  public abstract  class MyGenericServlet implements Servlet, ServletConfig {
     	  /以下方法为Servlet接口的方法/
     	  @Override
     	  public void destroy() {}
     	  @Override
     	  public ServletConfig getServletConfig() {
     	
     	return servletConfig;
     	}
     	- @Override
     	  public String getServletInfo() {
     	      return null;
     	  }
     	  private ServletConfig servletConfig;
     	  @Override
     	  public void init(ServletConfig arg0) throws ServletException {
     	      this.servletConfig=arg0;
     	      init();
     	  }
     	  public void init() throws ServletException{}
     	  @Override
     	  public abstract void service(ServletRequest arg0, ServletResponse arg1) 
     	      	throws ServletException, IOException ;
     	  
     	  /以下方法为Servlet Config接口的方法/
     	  @Override
     	  public String getInitParameter(String arg0) {
     	      return servletConfig.getInitParameter(arg0);
     	  }
     	  @Override
     	  public Enumeration<String> getInitParameterNames() {
     	      return servletConfig.getInitParameterNames();
     	  }
     	  @Override
     	  public ServletContext getServletContext() {
     	      return servletConfig.getServletContext();
     	  }
     	  @Override
     	  public String getServletName() {
     	      return servletConfig.getServletName();
     	  }
     	
     	}
     	@Override
     	
     	public String getServletInfo() {
     	
     	return null;
     	- }
     	  private ServletConfig servletConfig;
     	  @Override
     	  public void init(ServletConfig arg0) throws ServletException {
     	      this.servletConfig=arg0;
     	      init();
     	  }
     	  public void init() throws ServletException{}
     	  @Override
     	  public abstract void service(ServletRequest arg0, ServletResponse arg1) 
     	      	throws ServletException, IOException ;
     	  
     	  /以下方法为Servlet Config接口的方法/
     	  @Override
     	  public String getInitParameter(String arg0) {
     	      return servletConfig.getInitParameter(arg0);
     	  }
     	  @Override
     	  public Enumeration<String> getInitParameterNames() {
     	      return servletConfig.getInitParameterNames();
     	  }
     	  @Override
     	  public ServletContext getServletContext() {
     	      return servletConfig.getServletContext();
     	  }
     	  @Override
     	  public String getServletName() {
     	      return servletConfig.getServletName();
     	  }
     	
     	}


```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" id="WebApp_ID" version="3.1">
  <display-name>Day_30</display-name>
  
  <!-- 配置当前web应用的初始化参数 -->
  <context-param>
  	<param-name>user</param-name>
  	<param-value>atguigu</param-value>
  </context-param>
  
  <context-param>
  	<param-name>password</param-name>
  	<param-value>1234567</param-value>
  </context-param>
  
  <!-- 配置Servlet -->
  <servlet>
  	<servlet-name>loginServlet</servlet-name>
  	<servlet-class>com.atguigu.javaweb.LoginServlet</servlet-class>
  </servlet>
  <servlet-mapping>
  	<servlet-name>loginServlet</servlet-name>
  	<url-pattern>/LoginServlet</url-pattern>
  </servlet-mapping>

</web-app>
```

	<!DOCTYPE html>

	<html>

	<head>

	<meta charset="UTF-8">

	<title>Insert title here</title>

	</head>

	<body>

	<form action="LoginServlet" method="post">
		user: <input type="text" name="username"/>
		password: <input type="password" name="password"/>
		
		<input type="submit" value="submit"/>
		
	</form>
	</body>
	
	</html>


	package com.atguigu.javaweb;

	import java.io.IOException;
	import java.io.PrintWriter;
	
	import javax.servlet.GenericServlet;
	import javax.servlet.Servlet;
	import javax.servlet.ServletConfig;
	import javax.servlet.ServletContext;
	import javax.servlet.ServletException;
	import javax.servlet.ServletRequest;
	import javax.servlet.ServletResponse;


	public class LoginServlet extends GenericServlet {

	@Override
	public void init() throws ServletException {
		System.out.println("初始化。。。。"+getServletName());
	}
	
	@Override
	public void service(ServletRequest req, ServletResponse resp)
			throws ServletException, IOException {
		//1、获取请求参数：username、password
		String username=req.getParameter("username");
		String password=req.getParameter("password");
		
		//2、获取当前web应用的初始化参数：user，password
		//需要使用ServletContext对象
		String initUsername=getServletContext().getInitParameter("user");
		String initPassword=getServletContext().getInitParameter("password");
		
		PrintWriter out=resp.getWriter();
	
		//3、比对参数与上下文参数是否一致
		//4、向客户端浏览器打印信息
		if(initUsername.equals(username) && initPassword.equals(password)) {
			out.println("hello:"+username);
		}
		else {
			out.print("sorry:"+username);
		}
		}
	}
----------------------------------------------------------------------------------------------------------------------------------------------------------------

#### 							HttpServlet

1、HttpServlet是一个Servlet，继承自GenericServlet，针对于HTTP协议定制。

2、在service()方法中直接把Servlet Request和ServletResponse转为HTTP Servlet Request和HTTP Servlet Response，并调用重载的service(HttpServletRequest request,HttpServletResponse response) 

3、在service(HttpServletRequest request,HttpServletResponse httpresponse)获取了请求方式：request.getMethod()，根据请求方式创建对应的处理方式







































































