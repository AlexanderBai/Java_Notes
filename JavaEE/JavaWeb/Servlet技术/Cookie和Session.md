## 一、Session:

​	Session是在服务器端保存的一个数据结构，用来跟踪用户的状态，这个数据可以保存在集群、数据库、文件中，Session的运行依赖于Seseion id，而session id。是存在于cookie中的，如果浏览器禁用了cookie，同时session也失效（但也可以通过其他方式实现，比如在url中传递session_id）；

## 二、Cookie:

​	Cookie是客户端保存用户信息的一种机制，用来记录用户的一些信息，也是实现Session的一种方式

## 三、Cookie、Session、ServletContentext的区别和用法  

1、Cookie和Session都是通过request得到的，ServletCOntext通过this得到。

Cookie通过getValue取值，Session和ServletContext通过getAttribute取值。

Cookie通过setMaxAge来清空，Session通过setMaxActiveInterval来清空

2、Cookie的创建：Cookie通过new，add，setMaxAge的方式设定值，Session和ServletContext通过setAttribute方式设定值。

## 四、Token

### 1、什么是Token

​	Token是服务器端生成的一串字符串，以作为客户端进行请求的一个令牌，当客服端第一次请求资源时，服务器端生成一个Token，并返回给客服端，当客户端再次请求时，不需要用Cookie携带用户名和密码，只需带上Token即可。从而达到减轻服务器的压力（和避免频繁查询数据库的目的。

### 2、Token的原理

![img](file:///C:/Users/bbg28/Documents/Java%E7%AC%94%E8%AE%B0/JavaEE/JavaWeb/20160723154518396.png?lastModify=1508164216)

1. 将载荷和Header用Base64进行加密，生成payload密文和Header密文，(payload和Header都是JSON文件)；
2. 把生成payload密文和Header密文用点号连接，用服务器端密钥进行HS256加密，生成签名；
3. 将前面两个密文后面用点号连接签名最终形成Token返回给客户端。

Token可非为三部分：载荷(paylod)密文、Heade密文r、签名密文



### 3、Token的实现

![20160723193343759](C:\Users\bbg28\Documents\Java笔记\JavaEE\JavaWeb\20160723193343759.png)

1. 用户登录校验，若正确，则返回Token给客户端；
2. 客户端收到Token后保存在客户端；
3. 客户端再次访问API时带都上Token到服务器端；
4. 服务器端用Filter过滤器进行校验，若正确，返回请求数据，否则返回错误码。

### 4、Token的应用

1. 用设备号/设备Mac地址作为Token（推荐）；
2. 用Session值作为Token。



