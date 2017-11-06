#### 一、直接请求转发（Forward）

客户端和浏览器只发出一次请求，Servlet、HTML、JSP或其他信息资源，有第二个信息资源响应该请求，在请求对象request中，保存的对象对于每个信息资源是共享的。一般用于MVC设计模式中的控制层，由控制器来控制请求应该转发给那个信息资源。

```
......
    //Servlet里处理get请求的方法
 public void doGet(HttpServletRequest request , HttpServletResponse response){
     //获取请求转发器对象，该转发器的指向通过getRequestDisPatcher()的参数设置
   RequestDispatcher requestDispatcher =request.getRequestDispatcher("资源的URL");
    //调用forward()方法，转发请求      
   requestDispatcher.forward(request,response);    
}
......
```





#### 二、间接请求转发（Redirect）（也叫重定向）

实现两次HTTP请求，服务器在响应客户端请求后，让客户端再向另一个URL发出请求。

一般用于避免非正常访问，列如在没有登录的情况下访问后台资源，Servelet可以将HTTP请求重定向到登录界面。在servlet中通过调用response对象的SendRedirect()方法，

```
......
//Servlet中处理get请求的方法
public void doGet(HttpServletRequest request,HttpServletResponse response){
//请求重定向到另外的资源
    response.sendRedirect("资源的URL");
}
........
```

