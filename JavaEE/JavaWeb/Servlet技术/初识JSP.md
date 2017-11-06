# 						JSP																		

### JSP指令

##### ｐａｇ指令：

用于定义整个ｊｓｐ页面的相关属性

	<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>

主要的属性有：language、extends，import、ｐａｇｅＥｎｃｏｄｉｎｇ、ｃｏｎｔｅｎＴｙｐｅ、session、buffer、autoFlush等。

##### ｉｎｃｌｕｄｅ指令：

用于文件包含，仅支持静态包含

	<%@include file="log.jsp"%>


##### ｔａｇｌｉｂ指令：

用于加载用户自定义标签

### JSP脚本

＜％　％＞　嵌入Java代码

＜％！　％＞　自定义全局变量或方法

＜％＝　％＞ＪＳＰ表达式

### JSP动作标签

###### ＜ｊｓｐ：ｉｎｃｌｕｄｅ＞　调用文件

＜ｊｓｐ：ｉｎｃｌｕｄｅ　ｐａｇｅ＝＂ｕｒｌ＂／＞

###### ＜ｊｓｐ：ｆｏｒｗａｒｄ＞请求转发标签

＜ｊｓｐ：ｆｏｒｗａｒｄ　ｐａｇｅ＝＂ＨｅｌｌｏＷｏｒｄ．ｊｓｐ”／＞

###### ＜ｊｓｐ：ｐａｒａｍ＞　可作为另一标签的子标签



### JSP对象

###### out

###### request

###### response

###### session

###### application

###### page

###### exception

###### pageContext

###### configjsp





