# 一、Filter简介

​	web开发人员通过Filter技术对web服务器管理的所有web资源（jsp、Servlet、静态图片或静态HTML文件等)进行拦截，从而实现一些特殊的功能(如实现URL级别的权限访问控制、过滤敏感词、压缩响应信息等)。

doFilter的源代码：

	public abstract interface Filter{     
	    public abstract void init(FilterConfig paramFilterConfig) throws ServletException;  
	    public abstract void doFilter(ServletRequest paramServletRequest, ServletResponse 				paramServletResponse, FilterChain   paramFilterChain) throws IOException, ServletException;  
	    public abstract void destroy();  
	}	
# 二、Filter的工作原理

​	编写好Filter后，并配置对哪个web资源进行拦截后，web服务器每次在调用web资源的service方法之前，都会调用Filter的doFilter方法，因此，在该方法内编写代码可达到如下目的：

1、调用目标资源之前，让一段代码执行；

2、是否调用木匾资源(既是否让用户访问web资源)；

3、调用目标资源后让一段代码执行；

​	web服务器在调用doFilter时，会传递一个FilterChain对象，FilterChain对象是Filter接口中重用的一个对象,也提供了一个doFilter方法，开发人员可以根据需求决定否调用该方法。调用该方法，则web服务器是就会调用web资源的service方法，既web资源可被访问，否则不能。

# 三、Filter开发流程

#### 1、Filter开发步骤

a、用java类实现Filter接口，并实现doFilter方法

b、在web.xml中使用<filter>和<filter-mapping>元素对编写的filter进行注册，并设置它所能拦截的资源。

#### 2、Filter链

在一个web应用中，可以编写多个Filter，组合起来称为一个Filter链。web服务器根据Filter在web.xml文件中的注册顺序决定先调用哪个Filter；web服务器会创建一个代表Filter链的FilterChain对象传递给doFilter方法，若开发人员调用了FilterChain的doFilter方法，则web服务器会检查FilterChain中是否还有rFilte。

# 四、Spring在框架下，过滤器的配置

# 五、Filter的生命周期

1. 创建：Filter的创建和销毁都是由web服务器负责。启动web应用程序时，web服务器创建Filter的对象，并调用其init方法，完成对象打的初始化功能。Filter对象只会被创建一次，init方法也只会被调用一次。通过init方法的参数可以获得Filter配置信息的FilterConfig对象。
2. 销毁：web容器调用destroy方法，且只被调用一次，释放Filter所使用的资源。
3. FilterConfig接口：在web.xml中可以用<init-param>配置一些初始化参数，当web容器调用init方法时，会把封装了Filter初始化参数的FilterConfig对象传递进来。开发人员可以通过FilterConfig对象的方法，就可获得：

	//得到Filter的名称
	String getFilterNamte()
	//返回部署在描述文件中指定名称的初始化参数的值。如果不存在，返回null
	String getInitParameters(String name) 
	//返回过滤器的所有初始化参数的名字的枚举集合
	Enumeration getInitParameterNames() 
	//返回Servlet上下文对象的引用
	public ServletContext ()
	






# 六、在部署时一些参数的含义

# 六、在部署时一些参数的含义

# 

