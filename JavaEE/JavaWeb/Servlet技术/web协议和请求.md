# 								HTTP简介

##### HTTP协议：web浏览器和web服务器之间的一问一答的交互过程所遵循的原则。用于定义web浏览器和web服务器之间交换数据的过程以及数据本身的格式。

HTTP请求消息的结构：

一个请求行、若干消息头、以及实体内容。消息和实体内容要用空行隔开

### 请求方式

###### get请求：

1. 直接输入URL地址或点击网页上的一个链接时；

2. 网页中的<form>表单的method属性设置为get

3. 使用get请求给web服务器传递参数；如http://www.atguigu.com/counter.jsp?name=lc&password=123

4. 数据量一般限制在1KB一下

   ###### post请求：

   1. form表单的method置为post；
   2. 表单字段元素及其数据作为HTTP消息的实体内容是时。