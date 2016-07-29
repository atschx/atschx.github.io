---
author: Albert
date: 2014-08-16 09:57:52+00:00
layout: post
title: Java Web中WEB-INF目录的几点认识
categories: tech
---

## 项目开发现场的一段对话

甲：XX，我们项目运行起来为何不能直接访问我自己写的一个JSP文件？
乙：访问权限的问题，你把JSP文件移至WEB-INF下的views文件夹中，然后用个Controller映射访问。
甲：为什么要写Controller，直接JSP文件访问很正常啊
乙：针对mobile模块相关的访问开发阶段已去除了权限校验，你写个Controller映射下就可以直接访问。一般不允许客户端直接访问JSP文件（业内惯用做法：JSP文件放在WEB-INF下）。
Balabala…. 一番争论，未果，继续工作。

程序员的世界，你们不懂。

关于JSP文件直接放在web根目录下，还是放在WEB-INF下，各有各的利弊。对于本身就存在争议的问题，并没有什么标准答案，争吵都是无意义的口水战争。冷静下来思考各自的利弊，然后解决眼下的问题才是王道。

## Java™ Servlet Specification对WEB-INF的描述


A special directory exists within the application hierarchy named "WEB-INF". This directory contains all things related to the application that aren't in the document root of the application. **The WEB-INF node is not part of the public document tree of the application. **No file contained in the WEB-INF directory may be served directly to a client by the container. However, the contents of the WEB-INF directory are visible to servlet code using the **getResource **and **getResourceAsStream **method calls on the **ServletContext**, and may be exposed using the **RequestDispatchercalls**. Hence, _if the Application Developer needs access, from servlet code, to application specific configuration information that he does not wish to be exposed directly to the Web client, he may place it under this directory_. Since requests are matched to resource mappings in a case-sensitive manner, client requests for '/WEB-INF/foo', '/WEb-iNf/foo', for example, should not result in contents of the Web application located under/WEB-INF being returned, nor any form of directory listing thereof.


The contents of the WEB-INF directory are:

•The /WEB-INF/web.xml deployment descriptor.
•The /WEB-INF/classes/directory for servlet and utility classes. The classes in this directory must be available to the application class loader.
•The /WEB-INF/lib/*.jar area for Java archive files. These files contain servlets, beans, and other utility classes useful to the Web application. The Web application class loader must be able to load classes from any of these archive files.

The Web application class loader must load classes from the WEB-INF/ classes directory first, and then from library JARs in the WEB-INF/lib directory. Also, any requests from the client to access the resources in WEB-INF/directory must be returned with a SC_NOT_FOUND(404) response.

更多内容请参阅：[JSR-315](https://www.jcp.org/en/jsr/detail?id=315)


## 让我们回忆下Java Web开发的演变

Model 1 和 Model 2 ，此部分内容原始出处：

[http://download.oracle.com/otn_hosted_doc/jdeveloper/1012/developing_mvc_applications/adf_aboutmvc2.html](http://download.oracle.com/otn_hosted_doc/jdeveloper/1012/developing_mvc_applications/adf_aboutmvc2.html)

Early web application design regarded the JSP page as the focal point for the entire application. Termed Model 1 architecture, the JSP page not only contains the display elements to output HTML, but is also responsible for extracting HTTP request parameters, call the business logic (implemented in JavaBeans, if not directly in the JSP), and handle the HTTP session. Although Model 1 is suitable for simple applications, this architecture usually leads to a significant amount of scriptlets (Java code embedded within HTML code in the JSP page), especially if there is a significant amount of request processing to be performed.

The following diagram illustrates the JSP Model 1 architecture.

![](http://www.jfxgraph.com/wp-content/uploads/2014/08/081614_1656_JavaWebWEBI1.gif)


As a response to the Model 1 architecture, Apache Software Organization developed the Jakarta Project's Struts framework. Struts is an open source framework for building web applications that integrate with standard technologies, such as Java Servlets, JavaBeans, and JSP. Struts offers many benefits to the web application developer, including Model 2 implementation of Model-View-Controller (MVC) design patterns in JSP web applications. The MVC Model 2 paradigm applied to web applications lets you separate display code (for example, HTML and tag libraries) from flow control logic (Struts action classes).

The following figure illustrates the Model 2 web application architecture, where Servlets control the flow of the web application and delegate the business logic to external components, usually JavaBeans or EJBs, while JSP pages generate the HTML for web browsers:

![](http://www.jfxgraph.com/wp-content/uploads/2014/08/081614_1656_JavaWebWEBI2.gif)

由此让我回忆起，当年model1模式下开发时，JSP页面（java混搭html元素外挂JS+CSS）混乱的时代。那个时候的jsp基本上都放在web根目录下，why ? 更多的解释就是为了跳转方便，表单的action直接就是XXX.jsp。那个时候感觉JSP和ASP相比没有什么多大的差别，ASP页面中嵌入VBScript 和 JSP中嵌入Java代码的感觉真TMD类似（感觉Sun公司模仿微软ASP技术推出的JSP）。然则技术是不断进步的，当SUN公司推出的Servlet技术之后，彻底扭转了web开发的这一局面。Model 2 模式引用而生，WEB开发框架雨后春笋般出现，Struts、Spring MVC、Web4J等等。JSP页面不断减负：标签化、模板化。

说到这里，就引出了Java Web开发中关于页面跳转的两种方式：forward和redirect。

此处留个链接：[Forward versus redirect](http://www.javapractices.com/topic/TopicAction.do?Id=181)

Model 2 阶段更多使用的是forward的模式，客户端发送request之后，web框架根据前端的request**解析**出其mapping的Action或Controller然后调用Service处理相应的业务，使用forward方式到相应页面response给客户端（forward模式可共享request scope 中的处理结果，进一步大家也可以思考下OpenSessionInView的东西）。

注：在Struts中基于Filter完成解析，Spring MVC中基于Servlet完成解析。从机制上来讲，Spring此部分的设计优于Struts，也是这几年来Spring MVC 越来越火的原因。


## 既然这样…那么…

不喜欢吊胃口的感觉，所以我的惯用做法是：

将JSP放在WEB-INF的目录下的一个文件夹下然后按模块的层次结构进行组织文件目录结构，静态文件直接甩在根目录下的static文件夹下，按类别区分。

![](http://www.jfxgraph.com/wp-content/uploads/2014/08/081614_1656_JavaWebWEBI3.png)

那是不是都要这样子呢，那倒未必，就像PHP现在还是Model 1 开发的感觉，但它依然很火。Ruby 亦是如此，何必较真。

就像大家说window有很多弊病，但还是使用它。windows is very popular, just like php.

## 相关参考，业内观点

Spring MVC 将JSP放在WEB-INF目录作为一种最佳实践

The InternalResourceBundleViewResolver can be configured for using JSPs as described above. **As a best practice**, we strongly encourage placing your JSP files in a directory under the 'WEB-INF' directory, so there can be no direct access by clients.

**stackoverflow** 中也出现过类似的问答

[what-is-web-inf-used-for-in-a-java-web-application](http://stackoverflow.com/questions/19786142/what-is-web-inf-used-for-in-a-java-web-application)


[why-put-jsp-in-web-inf](http://stackoverflow.com/questions/6825907/why-put-jsp-in-web-inf)


## 写在后面的感悟

长期以来在软件开发团队，总有一群技术人喜欢较真，他们可爱又可恨。可爱之处不想过多阐述，可恨之处：

>>半权威伪装——具体表现过度的使用"一定"、"肯定"等定语，强烈的个人挑衅色彩，令听者不悦

>>过多的争吵——不可否认有一定的性格因素，好的论证才是你NB的砝码，才能建立正确的共识，结束争吵

>>分散的精力——很多程序员工作效率特低，时间管理意识淡薄，晓不晓得加班很大程度上都是自己的错

项目成员之间的沟通应摒弃个人色彩，客观的提供解决问题的方案，技术观点需要有力的论证。"拿来主义"仅是一颗夺命救心丸，经常自己独立思考和理解问题的本质方可强身健体。

技术是死的，人是活的。思考的深度不同，层次就不同，境界自然就不一样。做技术务必时刻保持"大智若愚，虚怀若谷"的心态。

最后，希望所有的奋战在开发工作岗位上的技术人在项目泥潭或产品困境中愈挫愈勇，你不是一个人在战斗，珍惜你身边的每一个人！
