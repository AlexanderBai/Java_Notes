# 									jsp

JSP源代码可以分为两部分：模板数据与元素

- 模板数据：即JSP中的代码，模板数据输出到客户端浏览器时都不会发生变化，也不会控制程序的流程
- 元素：即JSP中的Java部分，包括脚本（Scriptlet,也就是JSP中的Java代码）、JSP指令（Directive)、JSP标签（Tag）等。元素决定了程序的流程。

![2获](C:\Users\bbg28\Documents\Java笔记\JavaEE\Javaweb整合开发－王者归来笔记\2获.PNG)

## 							jsp指令

![捕获1](C:\Users\bbg28\Documents\Java笔记\JavaEE\Javaweb整合开发－王者归来笔记\捕获1.PNG)

### 							page指令：

![捕获](C:\Users\bbg28\Documents\Java笔记\JavaEE\Javaweb整合开发－王者归来笔记\捕获.PNG)



![捕获4](C:\Users\bbg28\Documents\Java笔记\JavaEE\Javaweb整合开发－王者归来笔记\捕获4.PNG)

![捕获5](C:\Users\bbg28\Documents\Java笔记\JavaEE\Javaweb整合开发－王者归来笔记\捕获5.PNG)

![捕获2](C:\Users\bbg28\Documents\Java笔记\JavaEE\Javaweb整合开发－王者归来笔记\捕获2.PNG)

System.out.println("这是打印到控制台");

out.println("这是输出到页面");

<%! %>中可以声明全局变量或方法

<% %>中可以声明局部变量或方法

<% =表达式 %>//注意：表达式不以分号结束

## 						 jsp生命周期

![捕获3](C:\Users\bbg28\Documents\Java笔记\JavaEE\Javaweb整合开发－王者归来笔记\捕获3.PNG)

当用户第一次请求jsp页面时，jsp引擎把该jsp文件转换成一个Servlet，并创建这个servlet的实列，所以调用其构造方法，生成字节码，再调用jspInit()方法，最后执行jspService()方法。

```
<link rel="stylesheet" type="text/css" href="css/style.css">
```

linkl连接，HTML里引用外部样式表。

type类型，声明这是css的文本格式。text/css

rel，stylesheet~声明这是样式表

href链接，这是css文档下名叫style后缀为css的文档













<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<meta http-equiv="pragma" content="no-cache">
<meta http-equiv="cache-control" content="no-cache">
<meta http-equiv="exprires" content="0">
<meta http-equiv="keywords" content="keyeord1,keyword2,keyword3">
<meta http-equiv="description" content="This is my page">

<meta>是HTML中一个可选的标记项，提供关于HTML文档的元数据

meta 元素被用于规定页面的描述、关键词、文档的作者、最后修改时间以及其他元数据。

语法： <meta name="name" content="string">

1. name:项常用的选项有keyword（关键词）、decription(描述或说明)、author（制作者）等
2. http-equiv项：可用于替代name项，常用的选项有creation-date(创作日期)、refresh（刷新与自动跳转）等
3. conten(内容)项：根据name项或HTTP-equiv项的定义来决定此项填写什么样的字符串。

<meta name="n"