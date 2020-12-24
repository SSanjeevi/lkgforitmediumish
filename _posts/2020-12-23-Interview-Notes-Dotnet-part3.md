---
layout: post
title:  "Dotnet part 3 Interview Notes"
author: sal
categories: [ Dotnet, Interview Notes ]
image: assets/images/2.jpg
rating: 3
---
**What is a Garbage Collector?**

**Ans:**  Garbage collection is a feature of .Net to free the unused code objects in the memory.

**The memory heap is divided into three generations. Generation 0, Generation 1 and Generation 2.**

**Generation 0**  – This is used to store short-lived objects. Garbage Collection happens frequently in this Generation.

**Generation 1**  – This is for medium-lived objects. Usually, the objects that get moved from generation 0 are stored in this.

**Generation 2**  – This is for long-lived objects.

Collecting a Generation refers to collecting the objects in that generation and all its younger generations. Garbage collection of Generation 2 means full garbage collection, it collects all the objects in Generation 2 as well as Generation 1 and Generation 0.

During the Garbage collection process, as the first phase, list of live objects are identified. In the second phase, references are updated for those objects which will be compacted. And in the last phase, the space occupied by dead objects are reclaimed. The remaining objects are moved to an older segment.

**What is BCL?**

The Base Class Library is a Common Language Infrastructure. BCL encapsulates a large number of common functionalities which are available to all the .NET Languages. BCL makes the developers life much simpler while implementing various  functionalities like I/O operations, Data access operations, graphical user interfaces and interfaces to various hardware devices by encapsulating them into various namespaces and classes. It also encapsulates the services which are required by the latest real world applications. .NET Framework applications, components and the controls are built on BCL.

**Explain Different Types of Constructors in C#?**

There are four different types of constructors you can write in a class -

1. Default Constructor

2. Parameterized Constructor

3. Copy Constructor

4. Static Constructor

**What are functional and non-functional requirements?**

Functional requirements defines the behavior of a system whereas non-functional requirements specify how the system should behave; in other words they specify the quality requirements and judge the behavior of a system.

E.g.

Functional - Display a chart which shows the maximum number of products sold in a region.

Non-functional – The data presented in the chart must be updated every 5 minutes.

**What is a stack? What is a heap? Give the differences between the two?**

Stack is a place in the memory where value types are stored. Heap is a place in the memory where the reference types are stored.

**What is instrumentation?**

It is the ability to monitor an application so that information about the application&#39;s progress, performance and status can be captured and reported.

**What is object role modeling (ORM) ?**

It is a logical model for designing and querying database models. There are various ORM tools in the market like CaseTalk, Microsoft Visio for Enterprise Architects, Infagon etc.

**What is a COM Callable Wrapper (CCW)?**

CCW is a wrapper created by the common language runtime(CLR) that enables COM components to access .NET objects.

**What is a Runtime Callable Wrapper (RCW)?**

RCW is a wrapper created by the common language runtime(CLR) to enable .NET components to call COM components.

**What is a digital signature?**

A digital signature is an electronic signature used to verify/gurantee the identity of the individual who is sending the message.

**What is Application Domain and how does it work?**

Windows Operating Systems load a set of resources like .EXE, DLLs and allocate the memory for those resources in an area called as Process. Windows OS creates a separate and isolated area for each running application. Making separate isolation area for each application, makes the process more secure and stable. In case, one process fails, it does not affect the other process.

.NET applications, however, are not hosted like traditional applications by Windows Operating System. Under .NET, .EXEs are hosted under a process by logical partitioning which is known as &quot;Application Domain&quot;. Now you can host multiple application domains under one single process.

**What is MIME?**

The definition of MIME or Multipurpose Internet Mail Extensions as stated in MSDN is &quot;MIME is a standard that can be used to include content of various types in a single message. MIME extends the Simple Mail Transfer Protocol (SMTP) format of mail messages to include multiple content, both textual and non-textual. Parts of the message may be images, audio, or text in different character sets.

What are Cookies in ASP.NET?

Answer: Cookies are a State Management Technique that can store the values of control after a post-back. Cookies can store user-specific Information on the client&#39;s machine like when the user last visited your site. Cookies are also known by many names, such as HTTP Cookies, Browser Cookies, Web Cookies, Session Cookies and so on. Basically cookies are a small text file sent by the web server and saved by the Web Browser on the client&#39;s machine.

List of properties containing the HttpCookies Class:

1. **Domain:**  Using these properties we can set the domain of the cookie.
2. **Expires:**  This property sets the Expiration time of the cookies.
3. **HasKeys: ** If the cookies have a subkey then it returns True.
4. **Name: ** Contains the name of the Key.
5. **Path: ** Contains the Virtual Path to be submitted with the Cookies.
6. **Secured:**  If the cookies are to be passed in a secure connection then it only returns True.
7. **Value: ** Contains the value of the cookies.

**Limitation of the Cookies**

1. The size of cookies is limited to 4096 bytes.
2. A total of 20 cookies can be used in a single website.

## What is Ajax in ASP.NET?

Answer. Ajax stands for Asynchronous JavaScript and XML; in other words Ajax is the combination of various technologies such as a JavaScript, CSS, XHTML, DOM, etc.

AJAX allows web pages to be updated asynchronously by exchanging small amounts of data with the server behind the scenes. This means that it is possible to update parts of a web page, without reloading the entire page.

Web applications running within Microsoft&#39;s Internet Information Services (IIS) utilize what is known as IIS worker processes. These worker processes run as w3wp.exe, and there can be multiple per computer. It is possible to run IIS on a Windows desktop or Windows server, although it is usually only seen on Microsoft Windows Servers configured as web servers.

### **What is w3wp.exe / IIS Worker Process?**

Web applications on Windows Servers are configured via command line or Internet Information Systems (IIS) Manager. Within IIS you can set up websites and which application pools they are assigned. Multiple websites can be assigned to a single IIS application pool.

IIS application pools also provide a bunch of [advanced settings](https://msdn.microsoft.com/en-us/library/aa720391(v=vs.71).aspx). These impact the behavior of w3wp and your IIS worker process. Including things like what Windows user account it runs as, auto restarting of the process, auto shutdown, and more. It is also possible for one IIS application pool to create multiple IIS worker processes in what is called a [web garden](https://social.technet.microsoft.com/wiki/contents/articles/33647.web-gardening-in-iis-7-configure-step-by-step.aspx).

There is one key thing you need to know about IIS application pools that are a little confusing. Within the IIS management console, you can stop and start application pools. But, just because an IIS application pool is started, **there may not be an IIS worker process (w3wp) running**. IIS will not  **start the worker process until the first web request is received**.