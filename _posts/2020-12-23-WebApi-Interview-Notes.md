---
layout: post
title:  "ASP.NET WebApi Interview Notes"
author: "Sanjeevi Subramani"
categories: [ ASP.NET WebApi, Interview Notes ]
image: assets/images/16.jpg
---

# **Web api**

    - http protocol
  - controller – action – routing
  - (GET/POST/PUT/PATCH/DELETE)

Eg:

[HttpPost]

publicvoid SaveNewValue([FromBody]stringvalue)

{

}

Codes are grouped into five categories based upon the first number.

| **S. No.** | **HTTP Status Code** | **Description** |
| --- | --- | --- |
| 1. | 1XX | Informational |
| 2. | 2XX | Success |
| 3. | 3XX | Redirection |
| 4. | 4XX | Client-Side Error |
| 5. | 5XX | Server-Side Error |

Table: HTTP Status Code with Description

Some of the commonly seen HTTP Status Codes are: 200 (Request is Ok), 201 (Created), 202 (Accepted), 204 (No Content), 301 (Moved Permanently), 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 500 (Internal Server Error), 502 (Bad Gateway), 503 (Service Unavailable) etc.

    1. Difference between Web API and MVC controller

| Web API Controller | MVC Controller |
| --- | --- |
| Derives from System.Web.Http.ApiController class | Derives from System.Web.Mvc.Controller class. |
| --- | --- |
| Method name must start with Http verbs otherwise apply http verbs attribute. | Must apply appropriate Http verbs attribute. |
| Specialized in returning data. | Specialized in rendering view. |
| Return data automatically formatted based on Accept-Type header attribute. Default to json or xml. | Returns ActionResult or any derived type. |
| Requires .NET 4.0 or above | Requires .NET 3.5 or above |

    1. ASP.NET Web API vs WCF

| Web API | WCF |
| --- | --- |
| Open source and ships with .NET framework. | Ships with .NET framework |
| --- | --- |
| Supports only HTTP protocol. | Supports HTTP, TCP, UDP and custom transport protocol. |
| Maps http verbs to methods | Uses attributes based programming model. |
| Uses routing and controller concept similar to ASP.NET MVC. | Uses Service, Operation and Data contracts. |
| Does not support Reliable Messaging and transaction. | Supports Reliable Messaging and Transactions. |
| Web API can be configured using HttpConfiguration class but not in web.config. | Uses web.config and attributes to configure a service. |
| Ideal for building RESTful services. | Supports RESTful services but with limitations. |

1. **OData**

1. The Open Data Protocol (OData) is a data access protocol for the web. OData provides a uniform way to query and manipulate data sets through CRUD operations (create, read, update, and delete).

1. OData defines parameters that can be used to modify an OData query. The client sends these parameters in the query string of the request URI. For example, to sort the results, a client uses the $orderby parameter:

1. http://localhost/Products?$orderby=Name

1. The OData specification calls these parameters query options. You can enable OData query options for any Web API controller in your project — the controller does not need to be an OData endpoint. This gives you a convenient way to add features such as filtering and sorting to any Web API application.

- Web API 5.2
- OData v4
- Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/))
- Entity Framework 6
- .NET 4.7.2

##

  1.
## Configure the OData endpoint

Open the file App\_Start/WebApiConfig.cs. Add the following  **using**  statements:

C#Copy

using ProductService.Models;

using Microsoft.AspNet.OData.Builder;

using Microsoft.AspNet.OData.Extensions;

Then add the following code to the  **Register**  method:

C#Copy

publicstaticclassWebApiConfig

{

publicstaticvoidRegister(HttpConfiguration config)

{

// New code:

ODataModelBuilder builder = new ODataConventionModelBuilder();

builder.EntitySet\&lt;Product\&gt;(&quot;Products&quot;);

config.MapODataServiceRoute(

routeName: &quot;ODataRoute&quot;,

routePrefix: null,

model: builder.GetEdmModel());

}

}

**Inherits odatacontroller:**

publicclassProductsController : ODataController

publicasync Task\&lt;IHttpActionResult\&gt; Patch([FromODataUri] int key, Delta\&lt;Product\&gt; product)

{

OData supports two different semantics for updating an entity, PATCH and PUT.

- PATCH performs a partial update. The client specifies just the properties to update.
- PUT replaces the entire entity.

  1. **Query Options**

The following are the OData query options that ASP.NET WebAPI supports:

- $orderby: Sorts the fetched record in particular order like ascending or descending.

[_?$orderby=ProductName desc_](http://localhost:50875/v1/Products/Product/allproducts?%24orderby=ProductName%20desc)

_$orderby=ProductName asc_

- $select: Selects the columns or properties in the result set. Specifies which all attributes or properties to include in the fetched result.
- $skip: Used to skip the number of records or results. For example, I want to skip first 100 records from the database while fetching complete table data, then I can make use of $skip.

[_$top=5&amp;$skip=3_](http://localhost:50875/v1/Products/Product/allproducts?%24top=5&amp;%24skip=3)

[_$orderby=ProductName asc &amp;$skip=6_](http://localhost:50875/v1/Products/Product/allproducts?%24orderby=ProductName%20asc%20&amp;%24skip=6)

- $top: Fetches only top n records. For e.g. I want to fetch top 10 records from the database, then my particular service should be OData enabled to support $top query option. -  &quot;? **$top=2&quot;**

_$orderby=ProductId asc&amp;$top=5_

- $expand: Expands the related domain entities of the fetched entities.
- $filter: Filters the result set based on certain conditions, it is like where clause of LINQ. For e.g. I want to fetch the records of 50 students who have scored more than 90% marks, and then I can make use of this query option.

**$filter=ProductName eq &#39;computer&#39;**

[_$filter=ProductId lt 3_](http://localhost:50875/v1/Products/Product/allproducts?%24filter=ProductId%20lt%203)

[_$filter=ProductId ge 3 and ProductId le 5_](http://localhost:50875/v1/Products/Product/allproducts?%24filter=ProductId%20ge%203%20and%20ProductId%20le%205)

[_$filter=substringof(&#39;IPhone&#39;,ProductName)_](http://localhost:50875/v1/Products/Product/allproducts?%24filter=substringof(%27IPhone%27,ProductName))

- $inlinecount: This query option is mostly used for pagination at client side. It tells the count of total entities fetched from the server to the client.

[Queryable]

[GET(&quot;allproducts&quot;)]

[GET(&quot;all&quot;)]

public HttpResponseMessage Get()

{

var products = \_productServices.GetAllProducts().AsQueryable();

var productEntities = products as List\&lt;ProductEntity\&gt; ?? products.ToList();

if (productEntities.Any())

returnRequest.CreateResponse(HttpStatusCode.OK, productEntities.AsQueryable());

throw new ApiDataException(1000, &quot;Products not found&quot;, HttpStatusCode.NotFound);

}

  1.
# Standard filter operators

The Web API supports the standard OData filter operators listed in the following table.

| **Operator** | **Description** | **Example** |
| --- | --- | --- |
| **Comparison Operators** |
| --- |
| **Eq** | Equal | $filter=revenue eq 100000 |
| **Ne** | Not Equal | $filter=revenue ne 100000 |
| **Gt** | Greater than | $filter=revenue gt 100000 |
| **Ge** | Greater than or equal | $filter=revenue ge 100000 |
| **Lt** | Less than | $filter=revenue lt 100000 |
| **Le** | Less than or equal | $filter=revenue le 100000 |
| **Logical Operators** |
| **And** | Logical and | $filter=revenue lt 100000 and revenue gt 2000 |
| **Or** | Logical or | $filter=contains(name,&#39;(sample)&#39;) or contains(name,&#39;test&#39;) |
| **Not** | Logical negation | $filter=not contains(name,&#39;sample&#39;) |
| **Grouping Operators** |
| **( )** | Precedence grouping | (contains(name,&#39;sample&#39;) or contains(name,&#39;test&#39;)) and revenue gt 5000 |

  1.
# Standard query functions

The web API supports these standard OData string query functions.

| **Function** | **Example** |
| --- | --- |
| **contains** | $filter=contains(name,&#39;(sample)&#39;) |
| --- | --- |
| **endswith** | $filter=endswith(name,&#39;Inc.&#39;) |
| **startswith** | $filter=startswith(name,&#39;a&#39;) |

Paging:

[Queryable(PageSize = 10)]

  1. Query Constraints:

[Queryable(AllowedQueryOptions =AllowedQueryOptions.Filter | AllowedQueryOptions.OrderBy)]

[GET(&quot;allproducts&quot;)]

[GET(&quot;all&quot;)]

public HttpResponseMessage Get()