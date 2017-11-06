# 			Struts2

## 一、什么是Struts2

​	在MVC模式进行web开发时，Servlet在控制层起到控制页面跳转的作用，其实Struts2就是封装了的Servlet，既提供了Servlet实现的接口，而不需要自己去实现Servlet。

## 二、Struts的作用

简化了jsp跳转的复杂操作，提供了易于编写的标签，可以快速开发view层代码。



## 三、实现原理

1、jsp和Servlet搭配时

①、jsp触发action

②、Servlet接受action，交给后台class处理

③、后台class跳转到其他的jsp，实现数据展现

③、后台class跳转到其他jsp，实现数据展现

2、有了Struts2后

①、jsp触发action

2、Struts2拦截请求，调用后台action

3、action返回结果，由不同的jsp展现数据



## 四、Struts的应用