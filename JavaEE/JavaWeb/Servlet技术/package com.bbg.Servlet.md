

​     







     package com.bbg.Servlet;
       import java.io.IOException;
        
       		import java.io.InputStream;
        
            import java.util.Enumeration;
        
            import java.util.Properties;
        
            import javax.servlet.ServletConfig;
        
            import javax.servlet.ServletContext;
        
            import javax.servlet.ServletException;
        
            import javax.servlet.ServletRequest;
        
            import javax.servlet.ServletResponse;
        
            import javax.servlet.annotation.WebServlet;
        
            import javax.servlet.http.HttpServlet;
        
            import javax.servlet.http.HttpServletRequest;
        
            import javax.servlet.http.HttpServletResponse;
        
            @WebServlet("/MyServlet")
        
            public class MyServlet extends HttpServlet {
        
    private static final long serialVersionUID = 1L;
    public MyServlet() {
    	super();
    	System.out.println("MyServlet's constructor");
    }
    @Override
    public void service(ServletRequest arg0, ServletResponse arg1) throws ServletException, IOException {
    	super.service(arg0, arg1);
    }
    
    @Override
    public void destroy() {
    	super.destroy();
    }
    
    @Override
    public ServletConfig getServletConfig() {
    	return super.getServletConfig();
    }
    
    @Override
    public String getServletInfo() {
    	return super.getServletInfo();
    }
    
    @Override
    public void init(ServletConfig config) throws ServletException {
    	super.init(config);
    	System.out.println("init");
    	
    	//获取值
    	String user=config.getInitParameter("user");
    	System.out.println("user:"+user);
    	
    	//以枚举方式获取值
    	Enumeration<String> names=config.getInitParameterNames();
    	while(names.hasMoreElements()) {
    		String name=names.nextElement();
    		String value=config.getInitParameter(name);
    		System.out.println("name:"+name+"  value:"+value);
    	}
    	
    	//获取Servlet的名称
    	String servletName=config.getServletName();
    	System.out.println("servletName:"+servletName);
    	
    	//获取Servlet Context的对象
    	ServletContext servletContext=config.getServletContext();
    	String driver=config.getInitParameter("driver");
    	System.out.println("driver:"+driver);
    	
    	Enumeration<String> names2=servletContext.getInitParameterNames();
    	while(names2.hasMoreElements()) {
    		String name=names2.nextElement();
    		System.out.println("-->"+name);
    	}
    	
    	//获取当前目录下的文件的路径
    	String realPath=servletContext.getRealPath("/note.text");
    	System.out.println("the realPath of note.text is "+realPath);
    	
    	String contextPath=servletContext.getRealPath(realPath);
    	System.out.println("the realPath of servletContext is "+contextPath);
    	
    	Properties pros=new Properties();
    	try {
    		ClassLoader classLoader=getClass().getClassLoader();
    		InputStream is=classLoader.getResourceAsStream("/jdbc.properties");
    		System.out.println("1:"+is);
    		pros.load(is);//以指定的值搜索属性
    	} catch (IOException e) {
    		e.printStackTrace();
    	}
    	
    	try {
    		InputStream is2 = servletContext.getResourceAsStream("/WEB-INF/classes/jdbc.properties");
    		System.out.println("2. " + is2);
    		pros.load(is2);
    		System.out.println(pros.getProperty("name"));  
    	} catch (Exception e) {
    		e.printStackTrace();
    	}
    	
    	String picPath = servletContext.getRealPath("/WEB-INF/lib");
    	System.out.println(picPath);
    }
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    	response.getWriter().append("Served at: ").append(request.getContextPath());
    }
    
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    	doGet(request, response);
    }
    }









	<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
	
	<html>
	
	<head>
	
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
	
	<title>Insert title here</title>
	
	</head>
	
	<body>
	
	<form action="MyloginServlet" method="post">
		user: <input type="text" name="user"/>
		password: <input type="password" name="password"/>
		
		<br><br>
		
		interesting:
		<input type="checkbox" name="interesting" value="reading"/>reading
		<input type="checkbox" name="interesting" value="game"/>game
		<input type="checkbox" name="interesting" value="party"/>party
		<input type="checkbox" name="interesting" value="shoping"/>shoping
		<input type="checkbox" name="interesting" value="sport"/>sport
		<input type="checkbox" name="interesting" value="tv"/>tv
		
		<input type="submit" value="Submit"/>
	</form>
	</body>
	
	</html>




	package com.bbg.Servlet;

	import java.io.IOException;

	import java.util.Arrays;

	import java.util.Enumeration;

	import java.util.Map;

	import javax.servlet.ServletConfig;

	import javax.servlet.ServletException;

	import javax.servlet.annotation.WebServlet;

	import javax.servlet.http.HttpServlet;

	import javax.servlet.http.HttpServletRequest;

	import javax.servlet.http.HttpServletResponse;

	@WebServlet("/MyLoginServlet")

	public class MyLoginServlet extends HttpServlet {

	private static final long serialVersionUID = 1L;
	MyLoginServlet(){
		System.out.println("MyServlet's Constou");
	}
	
	@Override
	public void init(ServletConfig config) throws ServletException {
	}
	
	@Override
	public ServletConfig getServletConfig() {
		return null;
	}
	
	@Override
	public String getServletInfo() {
		return null; 
	}
	
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) 
			throws ServletException, IOException {
	
		System.out.println("请求来了。。。。");
		System.out.println(request);
		
		String user=request.getParameter("user");
		String password=request.getParameter("password");
		System.out.println(user+":"+password);
		
		String interesting=request.getParameter("interesting");
		System.out.println(interesting);
		
		String[] interestings=request.getParameterValues("interesting");
		for(String interest:interestings) {
			System.out.println("--->"+ interest);
		}
		
		Enumeration<String> names=request.getParameterNames();
		while(names.hasMoreElements()) {
			 String name=names.nextElement();
			 String val=request.getParameter(name);
			 
			 System.out.println(">>"+name+":"+val);
		}
		
		Map<String,String[]> map=request.getParameterMap();
		for(Map.Entry<String,String[]> entry: map.entrySet()){
			System.out.println("**"+entry.getKey()+":"+Arrays.asList(entry));
		}
		
		String requestURl=request.getRequestURI();
		System.out.println(requestURl);
		
		String method=request.getMethod();
		System.out.println(method);
		
		String queryString=request.getQueryString();
		System.out.println(queryString);
		
		String servletPath=request.getServletPath();
		System.out.println(servletPath);
		}
		@Override
	public void destroy() {
		super.destroy();
		System.out.println("destroy");
	}






