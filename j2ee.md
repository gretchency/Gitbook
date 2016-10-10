# J2EE


### JSP 与 Servlet 的关系



Tomcat 等 Web 容器最终会把 JSP转化为 Servlet

Jsp更擅长表现于页面显示, Servlet更擅长于逻辑控制

Servlet是利用 System.out.println()来输出 html 代码，由于包括大量的HTML标签、大量的静态文本及格式等，导致Servlet的开发效率低下

JSP通过在标准的HTML页面中嵌入Java代码，其静态的部分无须Java程序控制，Java 代码只控制那些动态生成的信息
最终 JSP 被容器解释为 Servlet，其中Html 代码也是用System.out.println()等拼接输出的

JSP 第一次访问的时候，要转化为 java 文件，然后编译为 class 文件，所以第一次访问 JSP 速度会比较慢，后面会快很多
Servlet 生命周期

主要是java.servlet.Servlet接口中的init() 、service() 、和destroy() 3个方法。


### Servlet 生命周期



初始化阶段，web容器通过调用init()方法来初始化Servlet实例，在Servlet的整个生命周期类，init()方法只被调用一次

客户请求到来时，容器会开始一个新线程，并调用servlet的 service()方法，service() 方法根据请求的http方法来调用 doget() 或dopost()

终止阶段调用destroy()方法，销毁一些资源


### GET 请求 vs POST 请求



GET用于信息获取，是安全的和幂等的，GET一般是对后台数据库的信息进行查询

POST表示可能修改变服务器上的资源的请求，一般是对后台数据库进行增、删、改的操作

GET请求的参数会跟在URL后进行传递，请求的数据会附在URL之后，以?分割URL和传输数据，参数之间以&相连，一般浏览器对 URL 的长度会有限制

POST请求，提交的数据则放置在是HTTP包的包体中，用类似Key-Value的格式发送一些数据，相对来说，GET请求会把请求的参数暴露在 URL 中，安全性比POST差一些


### HTTP 请求的基本格式



<request line> 请求行
<headers> 请求头（参数头）
<blank line> 空白行
[<request-body>] 请求实体（GET没有， POST有）