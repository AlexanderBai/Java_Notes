# 一、JSTL

​	(JSP Standard Tag Library):JSP标准标签库，常用来实现页面逻辑判断和迭代使用

1、核心标签

2、格式化标签

3、SQL标签

4、XML标签

5、JSTL函数

	<%@ taglib prefix="c"  uri="http://java.sun.com/jsp/jstl/core" %>  引入标签库
	
	<c:out> 	用于在JSP中显示数据，就像<%= ... >
	<c:set> 	用于保存数据，就像session.setAttribute()
	<c:remove> 	用于删除数据,就像session.removeAttrbute()
	<c:catch> 	用来处理产生错误的异常状况，并且将错误信息储存起来,类似于java中的try
	<c:if> 	与我们在一般程序中用的if一样
	
	
	<c:choose> 	本身只当做<c:when>和<c:otherwise>的父标签，类似于java中的switch
	<c:when> 	<c:choose>的子标签，用来判断条件是否成立，类似于java中的case
	<c:otherwise> 	<c:choose>的子标签，接在<c:when>标签后，当<c:when>标签判断为false时被执行
	
	
	<c:import> 	检索一个绝对或相对 URL，然后将其内容暴露给页面
	<c:forEach> 	基础迭代标签，接受多种集合类型，类似于java中的for循环
	<c:forTokens> 	根据指定的分隔符来分隔内容并迭代输出，类似于java中的foreach循环
	<c:param> 	用来给包含或重定向的页面传递参数
	<c:redirect> 	重定向至一个新的URL.
	<c:url> 	使用可选的查询参数来创造一个URL
	
	<%@ taglib prefix="fmt" 
	           uri="http://java.sun.com/jsp/jstl/fmt" %>
	<fmt:formatDate><!--这货非常常用-->
	
	<%@ taglib prefix="fn" 
	           uri="http://java.sun.com/jsp/jstl/functions" %>
# 二、EL

​	(Expression Language):表达式语言，常用来显示数据

以$开头，内容都在{}中

```
语法：${expression}

常用的 ${sessionScope.username}
	  ${pageContext.request.contextPath}  直接用点访问属性的。。
```

# 三、使用

当JSP页面不想使用大量的java代码处理逻辑的时候，可以用JSTL和EL