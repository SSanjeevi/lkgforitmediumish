---
layout: post
title:  "Unit Test Interview Notes"
author: sal
categories: [ Unit Test, Interview Notes ]
image: assets/images/17.jpg
---

**Unit Testing**

**Unit Test**

1. **namespace**  WebAPI.Tests
2. {
3.      **using**  Microsoft.VisualStudio.TestTools.UnitTesting;
4.      **using**  System.Net.Http;
5.      **using**  System.Web.Http;
6.      **using**  WebAPI.Controllers;
7.      **using**  WebAPI.Models;
8.     [TestClass]
9.     publicclassEmployeeUnitTest
10.     {
11.         [TestMethod]
12.         publicvoid EmployeeGetById()
13.         {
14.             // Set up Prerequisites
15.             var controller = new EmployeeController();
16.             controller.Request = new HttpRequestMessage();
17.             controller.Configuration = new HttpConfiguration();
18.             // Act on Test
19.             var response = controller.Get(1);
20.             // Assert the result
21.             Employee employee;
22.             Assert.IsTrue(response.TryGetContentValue \&lt; Employee \&gt; ( **out**  employee));
23.             Assert.AreEqual(&quot;Jignesh&quot;, employee.Name);
24.         }
25.     }
26. }

**OKNegotiatedContentResult\&lt;T\&gt; - for HttpAction result**

1. var response = controller.Get(1);
2.             var contentResult = response as OkNegotiatedContentResult\&lt;Department\&gt;;
3.             // Assert the result
4.             Assert.IsNotNull(contentResult);
5.             Assert.IsNotNull(contentResult.Content);
6.             Assert.AreEqual(1, contentResult.Content.DepartmentId);
7. Assert.AreEqual(&quot;DefaultApi&quot;, createdResult.RouteName);
8.     Assert.IsNotNull(createdResult.RouteValues[&quot;id&quot;]);

Assert.AreEqual(HttpStatusCode.Accepted, contentResult.StatusCode);

**NUnit testing: MOK framework**

usingMVC5\_Testing\_1.ModelAccess;

usingNUnit.Framework;

namespaceMVCModelTest

{

    [TestFixture]

    publicclassCheckDepartmentTest

    {

        [Test]

        publicvoidCheckDepartmentExist()

        {

            var obj = newDepartmentAccess();

            var Res = obj.CheckDeptExist(10);

            Assert.That(Res, Is.True);

        }

    }

}

[Test]

publicvoidCheckDepartmentExistWithMoq()

{

    //Create Fake Object

    var fakeObject = newMock\&lt;IDepartmentAccess\&gt;();

    //Set the Mock Configuration

    //The CheckDeptExist() method is call is set with the Integer parameter type

    //The Configuration also defines the Return type from the method

    fakeObject.Setup(x =\&gt; x.CheckDeptExist(It.IsAny\&lt;int\&gt;())).Returns(true);

    //Call the methid

    var Res = fakeObject.Object.CheckDeptExist(10);

    Assert.That(Res,Is.True);

}