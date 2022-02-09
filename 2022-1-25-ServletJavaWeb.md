## 通过继承HttpServlet实现Servlet程序
***
一般在实际项目开发中，都是用继承HttpServlet类的方式实现Servlet程序。
- 编写一个类去继承HttpServlet
- 根据业务需要重写doGet和doPost方法
- 到web.xml中配置Servlet程序访问地址
  
  ## ServletConfig类
  ***
  ServletCOnfig类从类名上来看，就知道是Servlet程序的配置信息类。
  Servlet程序和ServletConfig对象都是由Tomcat负责创建，我们负责使用。
  Servlet程序默认是第一次访问的时候创建，ServletConfig是每个Servlet创建时，创建的一个对象。

  ## ServletContext 类
  ***
-  1）servletContext是一个接口他表示Servlet上下文对象。
- 2）一个Web工程只有一个ServletContext对象实例
- 3） ServletContext对象是一个域对象。

***
|   |存数据|取数据|删除数据|
|:---|:---:|----:|---:|
|Map|put()|get()|remove()|
|域对象|setAttribute()|getAttribute()|removeAttribute()
  ## ServletContext类的四个作用

***
- 获取web.xml配置的上下文参数context.param
-  获取当前工作路径，格式:/工程路径
-  获取工程部署后在服务器硬盘上的绝对路径
-   像Map一样存取数据
***
## HTTP协议
a)什么是HTTP协议
客户端给服务端发送数据叫请求，服务端给客户端传数据叫响应。
-  GET请求
   -  请求行
      - 请求方式 GET
      - 请求的资源路径
      - 请求的协议版本号
 - 请求头
   - key value不同请求有不同反应
   - GET /***/ http/1.1
   - Accept:告诉服务器，客户端可以接受的数据类型
   - Accept Language告诉服务器可以接受语言类型
   - User-Agent:浏览器信息
   - Accept-Encoding：告诉服务器，客户端可以接受的数据编码格式
   - Host:表示请求的服务器ip和端口号
   - ConnectionL告诉服务器如何处理链接 Keep-Alive开一段时间 close关
- POST请求
  - 请求行 post
  - 请求头
  - 请求体-发送给服务器的数据
  -Accept:表示客户端可以接受的数据类型
  Accept-Language:
  Refer
  User-Agent
  COntent-Type
- 常用的请求头
  - Accept
  - Accpt-Language
  
## GET请求有哪些
***
- form标签 method = get
- a标签
- 林肯标签引入csss
- img标签引入图片
- iframe引入html页面
- 在列兰奇地址栏中输入地址后回车
  
  ## POST请求有哪些
  ***
  - form标签 method = post
  
  ## 相应的HTTP协议格式
  - 响应行
    - 响应的协议和版本号
    - 响应状态码
    - 响应状态描述符
  - 响应头
    - key:value
      - Server服务器数据
      - Context-type:响应体数据类型
      - date:事件
  - 响应体
    - 回传给客户端数据
  - 常用响应码数据
    - 200 成功
    - 302重定向
    - 404不存在或地址错误
    - 500 服务器已经收到请求倒是服务器代码错误 
## MIME类型说明
***
- MIME是HTTP协议中数据类型
## HTTPServletRequest类
***
- HttpServletRequest类
  - HttpServletRequet类有什么作用
    - 每次只要有请求进入Tomcat服务器，Tomcat服务器就会把过来的HTTP协议解析防撞到Request对象中，然后传递到servlet方法(doGet和doPost)中给我们使用，我们可以通过HttpServletRequest对象，获取所有请求的信息。
      - getRequestURL
      - getRequest
## 请求的转发
***
<p>什么是请求的转发请求一个资源转换到另外一个资源叫做请求的转发

## Web中 /不同的意义
***
- 浏览器中解析得到的地址是:http://ip:port/
- 如果被服务器解析，得到的地址是：http://ip:port/工程项目名/

## HttpServletResponse
1)HttpServletResponse类的作用
httpServletRequest和HttpServletResponse类一样，每次请求进来，tomcat服务器就会创建一个response对象传递给Servlet程序去使用，HttpServletRequest请求过来的信息，都可以通过response进行设置。
- 两个输出流说明
  - 字节流 getOutPutStream()
  - 字符流 getWriter()常用于回传字符串。

## 请求重定向
***
- response1随着时间的推移和项目的不断更新，升级，Response1这个窗口慢慢被废弃了，由新的接口Response2所取代。
- response2 程序取代了Response1,功能更玩你删，安全性更高。

## JAVAEE三层架构
***
- http://ip:port/工程路径/资源路径 
- Web层
  - 获取请求参数
  - 调用Service层处理业务
  - 响应数据给客户端
- service业务层
  - 处理业务逻辑
  - 调入持久层保存数据库
- Dao持久层
  - 只负责数据库交互
  - CRUD操作
- 将结果展现在屏幕上
- 分层是为了解耦，解耦是为了方便之后的数据升级
- web层
  - com.$.web/servlet/controler
- service层
  - com.$.service service接口包

## book
***
- 创建数据库
- 编写数据库对应的JavaBean对象
- 编写工具类