---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL 路由 |Microsoft 文档
author: Erikre
description: 本系列教程将教您生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: a195b36517bcae4bbeaf43fe7386e7787fd00212
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30886428"
---
<a name="url-routing"></a><span data-ttu-id="d2c23-103">URL 路由</span><span class="sxs-lookup"><span data-stu-id="d2c23-103">URL Routing</span></span>
====================
<span data-ttu-id="d2c23-104">通过[艾力克 Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="d2c23-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="d2c23-105">[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="d2c23-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="d2c23-106">本系列教程将教您构建使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的 ASP.NET Web 窗体应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="d2c23-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="d2c23-107">Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)是可以附带本系列教程。</span><span class="sxs-lookup"><span data-stu-id="d2c23-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="d2c23-108">在本教程中，你将要修改 Wingtip Toys 示例应用程序来支持 URL 路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-108">In this tutorial, you will modify the Wingtip Toys sample application to support URL routing.</span></span> <span data-ttu-id="d2c23-109">路由允许 web 应用程序使用友好、 更轻松地请记住，以及更好地支持按搜索引擎的 Url。</span><span class="sxs-lookup"><span data-stu-id="d2c23-109">Routing enables your web application to use URLs that are friendly, easier to remember, and better supported by search engines.</span></span> <span data-ttu-id="d2c23-110">本教程以前一教程"成员身份和管理"上构建，并为 Wingtip Toys 教程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="d2c23-110">This tutorial builds on the previous tutorial "Membership and Administration" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="d2c23-111">你将学习：</span><span class="sxs-lookup"><span data-stu-id="d2c23-111">What you'll learn:</span></span>

- <span data-ttu-id="d2c23-112">如何注册为 ASP.NET Web 窗体应用程序的路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-112">How to register routes for an ASP.NET Web Forms application.</span></span>
- <span data-ttu-id="d2c23-113">如何将路由添加到网页。</span><span class="sxs-lookup"><span data-stu-id="d2c23-113">How to add routes to a web page.</span></span>
- <span data-ttu-id="d2c23-114">如何从数据库以支持路由选择数据。</span><span class="sxs-lookup"><span data-stu-id="d2c23-114">How to select data from a database to support routes.</span></span>

## <a name="aspnet-routing-overview"></a><span data-ttu-id="d2c23-115">ASP.NET 路由概述</span><span class="sxs-lookup"><span data-stu-id="d2c23-115">ASP.NET Routing Overview</span></span>

<span data-ttu-id="d2c23-116">URL 路由允许你配置应用程序可以接受请求不映射到物理文件的 Url。</span><span class="sxs-lookup"><span data-stu-id="d2c23-116">URL routing allows you to configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="d2c23-117">请求 URL 是只需用户输入到其浏览器在网站上查找页的 URL。</span><span class="sxs-lookup"><span data-stu-id="d2c23-117">A request URL is simply the URL a user enters into their browser to find a page on your web site.</span></span> <span data-ttu-id="d2c23-118">使用路由来定义在语义上对用户有意义以及可帮助搜索引擎搜索引擎优化 (SEO) 使用的 Url。</span><span class="sxs-lookup"><span data-stu-id="d2c23-118">You use routing to define URLs that are semantically meaningful to users and that can help with search-engine optimization (SEO).</span></span>

<span data-ttu-id="d2c23-119">默认情况下，Web 窗体模板包括[ASP.NET 友好 Url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)。</span><span class="sxs-lookup"><span data-stu-id="d2c23-119">By default, the Web Forms template includes [ASP.NET Friendly URLs](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/).</span></span> <span data-ttu-id="d2c23-120">大部分基本的路由工作将由使用实现*友好 Url*。</span><span class="sxs-lookup"><span data-stu-id="d2c23-120">Much of the basic routing work will be implemented by using *Friendly URLs*.</span></span> <span data-ttu-id="d2c23-121">但是，在本教程中，你将添加自定义路由功能。</span><span class="sxs-lookup"><span data-stu-id="d2c23-121">However, in this tutorial you will add customized routing capabilities.</span></span>

<span data-ttu-id="d2c23-122">在自定义 URL 路由之前, Wingtip Toys 示例应用程序可以将链接到产品使用以下 URL:</span><span class="sxs-lookup"><span data-stu-id="d2c23-122">Before customizing URL routing, the Wingtip Toys sample application can link to a product using the following URL:</span></span>

`https://localhost:44300/ProductDetails.aspx?productID=2`

<span data-ttu-id="d2c23-123">通过自定义 URL 路由，Wingtip Toys 示例应用程序将链接到相同的产品使用易于阅读 URL:</span><span class="sxs-lookup"><span data-stu-id="d2c23-123">By customizing URL routing, the Wingtip Toys sample application will link to the same product using an easier to read URL:</span></span>

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a><span data-ttu-id="d2c23-124">路由</span><span class="sxs-lookup"><span data-stu-id="d2c23-124">Routes</span></span>

<span data-ttu-id="d2c23-125">路由是映射到处理程序的 URL 模式。</span><span class="sxs-lookup"><span data-stu-id="d2c23-125">A route is a URL pattern that is mapped to a handler.</span></span> <span data-ttu-id="d2c23-126">处理程序可以是物理文件，例如 Web 窗体应用程序中的.aspx 文件。</span><span class="sxs-lookup"><span data-stu-id="d2c23-126">The handler can be a physical file, such as an .aspx file in a Web Forms application.</span></span> <span data-ttu-id="d2c23-127">处理程序也可以处理请求的类。</span><span class="sxs-lookup"><span data-stu-id="d2c23-127">A handler can also be a class that processes the request.</span></span> <span data-ttu-id="d2c23-128">若要定义路由，请通过指定的 URL 模式、 处理程序中，和 （可选） 单击路由名称创建路由类的实例。</span><span class="sxs-lookup"><span data-stu-id="d2c23-128">To define a route, you create an instance of the Route class by specifying the URL pattern, the handler, and optionally a name for the route.</span></span>

<span data-ttu-id="d2c23-129">您通过添加到应用程序添加路由`Route`为对静态对象`Routes`属性`RouteTable`类。</span><span class="sxs-lookup"><span data-stu-id="d2c23-129">You add the route to the application by adding the `Route` object to the static `Routes` property of the `RouteTable` class.</span></span> <span data-ttu-id="d2c23-130">路由属性是`RouteCollection`对象，用于存储应用程序的所有路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-130">The Routes property is a `RouteCollection` object that stores all the routes for the application.</span></span>

### <a name="url-patterns"></a><span data-ttu-id="d2c23-131">URL 模式</span><span class="sxs-lookup"><span data-stu-id="d2c23-131">URL Patterns</span></span>

<span data-ttu-id="d2c23-132">URL 模式可以包含文本值和变量 （也称为 URL 参数） 的占位符。</span><span class="sxs-lookup"><span data-stu-id="d2c23-132">A URL pattern can contain literal values and variable placeholders (referred to as URL parameters).</span></span> <span data-ttu-id="d2c23-133">文本和占位符位于由斜杠分隔的 URL 段 (`/`) 字符。</span><span class="sxs-lookup"><span data-stu-id="d2c23-133">The literals and placeholders are located in segments of the URL which are delimited by the slash (`/`) character.</span></span>

<span data-ttu-id="d2c23-134">发出对 web 应用程序的请求后，URL 解析为段和占位符，并且变量的值提供给请求处理程序。</span><span class="sxs-lookup"><span data-stu-id="d2c23-134">When a request to your web application is made, the URL is parsed into segments and placeholders, and the variable values are provided to the request handler.</span></span> <span data-ttu-id="d2c23-135">此过程是相似的方式分析查询字符串中的数据并将其传递给请求处理程序。</span><span class="sxs-lookup"><span data-stu-id="d2c23-135">This process is similar to the way the data in a query string is parsed and passed to the request handler.</span></span> <span data-ttu-id="d2c23-136">在这两种情况下，变量信息是包含在 URL 中，并传递给中键 / 值对形式的处理程序。</span><span class="sxs-lookup"><span data-stu-id="d2c23-136">In both cases, variable information is included in the URL and passed to the handler in the form of key-value pairs.</span></span> <span data-ttu-id="d2c23-137">查询字符串键和值是在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="d2c23-137">For query strings, both the keys and the values are in the URL.</span></span> <span data-ttu-id="d2c23-138">对于路由，密钥是 URL 模式中定义的占位符名称和都位于 URL 中只使用的值。</span><span class="sxs-lookup"><span data-stu-id="d2c23-138">For routes, the keys are the placeholder names defined in the URL pattern, and only the values are in the URL.</span></span>

<span data-ttu-id="d2c23-139">你可以在 URL 模式中，来定义通过将它们括在大括号占位符 (`{`和`}`)。</span><span class="sxs-lookup"><span data-stu-id="d2c23-139">In a URL pattern, you define placeholders by enclosing them in braces ( `{` and `}` ).</span></span> <span data-ttu-id="d2c23-140">你可以定义多个占位符段中，但必须按某一文字值分隔占位符。</span><span class="sxs-lookup"><span data-stu-id="d2c23-140">You can define more than one placeholder in a segment, but the placeholders must be separated by a literal value.</span></span> <span data-ttu-id="d2c23-141">例如，`{language}-{country}/{action}`是有效的路由模式。</span><span class="sxs-lookup"><span data-stu-id="d2c23-141">For example, `{language}-{country}/{action}` is a valid route pattern.</span></span> <span data-ttu-id="d2c23-142">但是，`{language}{country}/{action}`不是有效的模式，因为没有文本值或占位符之间的分隔符。</span><span class="sxs-lookup"><span data-stu-id="d2c23-142">However, `{language}{country}/{action}` is not a valid pattern, because there is no literal value or delimiter between the placeholders.</span></span> <span data-ttu-id="d2c23-143">因此，路由无法确定分离值语言占位符的值为国家/地区占位符的位置。</span><span class="sxs-lookup"><span data-stu-id="d2c23-143">Therefore, routing cannot determine where to separate the value for the language placeholder from the value for the country placeholder.</span></span>

### <a name="mapping-and-registering-routes"></a><span data-ttu-id="d2c23-144">映射和注册路由</span><span class="sxs-lookup"><span data-stu-id="d2c23-144">Mapping and Registering Routes</span></span>

<span data-ttu-id="d2c23-145">可以包括 Wingtip Toys 示例应用程序页面的路由之前，你必须在应用程序启动时注册路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-145">Before you can include routes to pages of the Wingtip Toys sample application, you must register the routes when the application starts.</span></span> <span data-ttu-id="d2c23-146">若要注册路由，你将修改`Application_Start`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="d2c23-146">To register the routes, you will modify the `Application_Start` event handler.</span></span>

1. <span data-ttu-id="d2c23-147">在**解决方案资源管理器**的 Visual Studio 中，找到并打开*Global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="d2c23-147">In **Solution Explorer**of Visual Studio, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="d2c23-148">添加代码以到黄色突出显示*Global.asax.cs*文件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d2c23-148">Add the code highlighted in yellow to the *Global.asax.cs* file as follows:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

<span data-ttu-id="d2c23-149">当 Wingtip Toys 示例应用程序启动时，它将调用`Application_Start`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="d2c23-149">When the Wingtip Toys sample application starts, it calls the `Application_Start` event handler.</span></span> <span data-ttu-id="d2c23-150">此事件处理程序中，末尾`RegisterCustomRoutes`调用方法。</span><span class="sxs-lookup"><span data-stu-id="d2c23-150">At the end of this event handler, the `RegisterCustomRoutes` method is called.</span></span> <span data-ttu-id="d2c23-151">`RegisterCustomRoutes`方法将每个路由添加通过调用`MapPageRoute`方法`RouteCollection`对象。</span><span class="sxs-lookup"><span data-stu-id="d2c23-151">The `RegisterCustomRoutes` method adds each route by calling the `MapPageRoute` method of the `RouteCollection` object.</span></span> <span data-ttu-id="d2c23-152">使用路由名称，路由 URL 和物理 URL 来定义路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-152">Routes are defined using a route name, a route URL and a physical URL.</span></span>

<span data-ttu-id="d2c23-153">第一个参数 ("`ProductsByCategoryRoute`") 是路由名称。</span><span class="sxs-lookup"><span data-stu-id="d2c23-153">The first parameter ("`ProductsByCategoryRoute`") is the route name.</span></span> <span data-ttu-id="d2c23-154">它用于在需要时调用路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-154">It is used to call the route when it is needed.</span></span> <span data-ttu-id="d2c23-155">第二个参数 ("`Category/{categoryName}`") 定义可以是动态的 URL 基于代码友好替换。</span><span class="sxs-lookup"><span data-stu-id="d2c23-155">The second parameter ("`Category/{categoryName}`") defines the friendly replacement URL that can be dynamic based on code.</span></span> <span data-ttu-id="d2c23-156">将填充一个数据生成基于数据的链接时，你可以使用此路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-156">You use this route when you are populating a data control with links that are generated based on data.</span></span> <span data-ttu-id="d2c23-157">一个路由，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d2c23-157">A route is shown as follows:</span></span>

[!code-csharp[Main](url-routing/samples/sample2.cs)]

<span data-ttu-id="d2c23-158">路由的第二个参数包含指定的大括号的动态值 (`{ }`)。</span><span class="sxs-lookup"><span data-stu-id="d2c23-158">The second parameter of the route includes a dynamic value specified by braces (`{ }`).</span></span> <span data-ttu-id="d2c23-159">在这种情况下，`categoryName`是一个变量，用于确定正确的路由路径。</span><span class="sxs-lookup"><span data-stu-id="d2c23-159">In this case, the `categoryName` is a variable that will be used to determine the proper routing path.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="d2c23-160">**Optional**</span><span class="sxs-lookup"><span data-stu-id="d2c23-160">**Optional**</span></span>
> 
> <span data-ttu-id="d2c23-161">你可能会发现更轻松地管理你的代码通过移动`RegisterCustomRoutes`到单独的类的方法。</span><span class="sxs-lookup"><span data-stu-id="d2c23-161">You might find it easier to manage your code by moving the `RegisterCustomRoutes` method to a separate class.</span></span> <span data-ttu-id="d2c23-162">在*逻辑*文件夹中，创建一个单独`RouteActions`类。</span><span class="sxs-lookup"><span data-stu-id="d2c23-162">In the *Logic* folder, create a separate `RouteActions` class.</span></span> <span data-ttu-id="d2c23-163">移动上述`RegisterCustomRoutes`方法从*Global.asax.cs*到新的文件`RoutesActions`类。</span><span class="sxs-lookup"><span data-stu-id="d2c23-163">Move the above `RegisterCustomRoutes` method from the *Global.asax.cs* file into the new `RoutesActions` class.</span></span> <span data-ttu-id="d2c23-164">使用`RoleActions`类和`createAdmin`作为示例，了解如何调用的方法`RegisterCustomRoutes`方法从*Global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="d2c23-164">Use the `RoleActions` class and the `createAdmin` method as an example of how to call the `RegisterCustomRoutes` method from the *Global.asax.cs* file.</span></span>


<span data-ttu-id="d2c23-165">你可能还会发现`RegisterRoutes`方法调用使用`RouteConfig`的开始处对象`Application_Start`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="d2c23-165">You may also have noticed the `RegisterRoutes` method call using the `RouteConfig` object at the beginning of the `Application_Start` event handler.</span></span> <span data-ttu-id="d2c23-166">进行此调用以实现默认路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-166">This call is made to implement default routing.</span></span> <span data-ttu-id="d2c23-167">创建使用 Visual Studio 的 Web 窗体模板的应用程序时，它是作为默认代码。</span><span class="sxs-lookup"><span data-stu-id="d2c23-167">It was included as default code when you created the application using Visual Studio's Web Forms template.</span></span>

## <a name="retrieving-and-using-route-data"></a><span data-ttu-id="d2c23-168">检索和使用路线数据</span><span class="sxs-lookup"><span data-stu-id="d2c23-168">Retrieving and Using Route Data</span></span>

<span data-ttu-id="d2c23-169">如上所述，可以定义路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-169">As mentioned above, routes can be defined.</span></span> <span data-ttu-id="d2c23-170">添加到代码`Application_Start`中的事件处理程序*Global.asax.cs*文件加载的可定义的路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-170">The code that you added to the `Application_Start` event handler in the *Global.asax.cs* file loads the definable routes.</span></span>

### <a name="setting-routes"></a><span data-ttu-id="d2c23-171">设置路由</span><span class="sxs-lookup"><span data-stu-id="d2c23-171">Setting Routes</span></span>

<span data-ttu-id="d2c23-172">路由要求你添加附加代码。</span><span class="sxs-lookup"><span data-stu-id="d2c23-172">Routes require you to add additional code.</span></span> <span data-ttu-id="d2c23-173">在本教程中，你将使用模型绑定来检索`RouteValueDictionary`生成使用数据控件中的数据的路由时使用的对象。</span><span class="sxs-lookup"><span data-stu-id="d2c23-173">In this tutorial, you will use model binding to retrieve a `RouteValueDictionary` object that is used when generating the routes using data from a data control.</span></span> <span data-ttu-id="d2c23-174">`RouteValueDictionary`对象将包含属于产品的特定类别的产品名称的列表。</span><span class="sxs-lookup"><span data-stu-id="d2c23-174">The `RouteValueDictionary` object will contain a list of product names that belong to a specific category of products.</span></span> <span data-ttu-id="d2c23-175">对于基于的数据和路由每个产品创建链接。</span><span class="sxs-lookup"><span data-stu-id="d2c23-175">A link is created for each product based on the data and route.</span></span>

#### <a name="enable-routes-for-categories-and-products"></a><span data-ttu-id="d2c23-176">启用路由的类别和产品</span><span class="sxs-lookup"><span data-stu-id="d2c23-176">Enable Routes for Categories and Products</span></span>

<span data-ttu-id="d2c23-177">接下来，你将更新应用程序使用`ProductsByCategoryRoute`来确定正确的路由，以便将包含在每个产品类别链接。</span><span class="sxs-lookup"><span data-stu-id="d2c23-177">Next, you'll update the application to use the `ProductsByCategoryRoute` to determine the correct route to include for each product category link.</span></span> <span data-ttu-id="d2c23-178">你将更新*ProductList.aspx*页以包含每个产品的路由的链接。</span><span class="sxs-lookup"><span data-stu-id="d2c23-178">You'll also update the *ProductList.aspx* page to include a routed link for each product.</span></span> <span data-ttu-id="d2c23-179">链接将显示之前更改，但链接现在将使用 URL 路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-179">The links will be displayed as they were before the change, however the links will now use URL routing.</span></span>

1. <span data-ttu-id="d2c23-180">在**解决方案资源管理器**，打开*Site.Master*页上，如果尚未打开。</span><span class="sxs-lookup"><span data-stu-id="d2c23-180">In **Solution Explorer**, open the *Site.Master* page if it is not already open.</span></span>
2. <span data-ttu-id="d2c23-181">更新**ListView**控件名为"`categoryList`"使用以黄色突出显示的更改，因此标记会显示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d2c23-181">Update the **ListView** control named "`categoryList`" with the changes highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. <span data-ttu-id="d2c23-182">在**解决方案资源管理器**，打开*ProductList.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="d2c23-182">In **Solution Explorer**, open the *ProductList.aspx* page.</span></span>
4. <span data-ttu-id="d2c23-183">更新`ItemTemplate`元素*ProductList.aspx*因此标记，如下所示显示黄色突出显示的更新的页：</span><span class="sxs-lookup"><span data-stu-id="d2c23-183">Update the `ItemTemplate` element of the *ProductList.aspx* page with the updates highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. <span data-ttu-id="d2c23-184">打开的代码隐藏*ProductList.aspx.cs*并将以下命名空间添加为用黄色突出显示：</span><span class="sxs-lookup"><span data-stu-id="d2c23-184">Open the code-behind of *ProductList.aspx.cs* and add the following namespace as highlighted in yellow:</span></span>  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. <span data-ttu-id="d2c23-185">替换`GetProducts`方法的代码隐藏 (*ProductList.aspx.cs*) 替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="d2c23-185">Replace the `GetProducts` method of the code-behind (*ProductList.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a><span data-ttu-id="d2c23-186">将代码添加有关产品详细信息</span><span class="sxs-lookup"><span data-stu-id="d2c23-186">Add Code for Product Details</span></span>

<span data-ttu-id="d2c23-187">现在，更新代码隐藏 (*ProductDetails.aspx.cs*) 为*ProductDetails.aspx*页后，可以使用路由数据。</span><span class="sxs-lookup"><span data-stu-id="d2c23-187">Now, update the code-behind (*ProductDetails.aspx.cs*) for the *ProductDetails.aspx* page to use route data.</span></span> <span data-ttu-id="d2c23-188">请注意，新`GetProduct`方法还接受的用户在其标有书签的链接上的用例，使用较旧的不友好，非路由 URL 的查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="d2c23-188">Notice that the new `GetProduct` method also accepts a query string value for the case where the user has a link bookmarked that uses the older non-friendly, non-routed URL.</span></span>

1. <span data-ttu-id="d2c23-189">替换`GetProduct`方法的代码隐藏 (*ProductDetails.aspx.cs*) 替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="d2c23-189">Replace the `GetProduct` method of the code-behind (*ProductDetails.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a><span data-ttu-id="d2c23-190">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="d2c23-190">Running the Application</span></span>

<span data-ttu-id="d2c23-191">你可以运行应用程序现在以查看更新的路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-191">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="d2c23-192">按**F5**运行 Wingtip Toys 示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="d2c23-192">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="d2c23-193">浏览器将打开并显示*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="d2c23-193">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="d2c23-194">单击**产品**页顶部的链接。</span><span class="sxs-lookup"><span data-stu-id="d2c23-194">Click the **Products** link at the top of the page.</span></span>  
 <span data-ttu-id="d2c23-195">上显示的所有产品*ProductList.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="d2c23-195">All products are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="d2c23-196">浏览器的显示 （使用端口号） 的以下 URL:</span><span class="sxs-lookup"><span data-stu-id="d2c23-196">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/ProductList`
3. <span data-ttu-id="d2c23-197">接下来，单击**汽车**页面顶部附近的类别链接。</span><span class="sxs-lookup"><span data-stu-id="d2c23-197">Next, click the **Cars** category link near the top of the page.</span></span>  
 <span data-ttu-id="d2c23-198">上显示仅汽车*ProductList.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="d2c23-198">Only cars are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="d2c23-199">浏览器的显示 （使用端口号） 的以下 URL:</span><span class="sxs-lookup"><span data-stu-id="d2c23-199">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Category/Cars`
4. <span data-ttu-id="d2c23-200">单击列在页中包含名称的第一辆车的链接 ("**可转换汽车**") 以显示产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="d2c23-200">Click the link containing the name of the first car listed on the page ("**Convertible Car**") to display the product details.</span></span>  
 <span data-ttu-id="d2c23-201">浏览器的显示 （使用端口号） 的以下 URL:</span><span class="sxs-lookup"><span data-stu-id="d2c23-201">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Product/Convertible%20Car`
5. <span data-ttu-id="d2c23-202">接下来，输入到浏览器中的以下非路由 URL （使用端口号）：</span><span class="sxs-lookup"><span data-stu-id="d2c23-202">Next, enter the following non-routed URL (using your port number) into the browser:</span></span>  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 <span data-ttu-id="d2c23-203">该代码仍然会识别包含查询字符串，其中用户都具有标有书签的链接的情况的 URL。</span><span class="sxs-lookup"><span data-stu-id="d2c23-203">The code still recognizes a URL that includes a query string, for the case where a user has a link bookmarked.</span></span>

## <a name="summary"></a><span data-ttu-id="d2c23-204">总结</span><span class="sxs-lookup"><span data-stu-id="d2c23-204">Summary</span></span>

<span data-ttu-id="d2c23-205">在本教程中，你添加的类别和产品的路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-205">In this tutorial, you have added routes for categories and products.</span></span> <span data-ttu-id="d2c23-206">你已学习如何与使用模型绑定的数据控件集成路由。</span><span class="sxs-lookup"><span data-stu-id="d2c23-206">You have learned how routes can be integrated with data controls that use model binding.</span></span> <span data-ttu-id="d2c23-207">在下一步的教程中，你将实现全局错误处理。</span><span class="sxs-lookup"><span data-stu-id="d2c23-207">In the next tutorial, you will implement global error handling.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d2c23-208">其他资源</span><span class="sxs-lookup"><span data-stu-id="d2c23-208">Additional Resources</span></span>

[<span data-ttu-id="d2c23-209">ASP.NET 友好的 Url</span><span class="sxs-lookup"><span data-stu-id="d2c23-209">ASP.NET Friendly URLs</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[<span data-ttu-id="d2c23-210">将包含成员资格、 OAuth 和 SQL 数据库的安全的 ASP.NET Web 窗体应用程序部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d2c23-210">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="d2c23-211">Microsoft Azure 的免费试用版</span><span class="sxs-lookup"><span data-stu-id="d2c23-211">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> <span data-ttu-id="d2c23-212">[上一页](membership-and-administration.md)
> [下一页](aspnet-error-handling.md)</span><span class="sxs-lookup"><span data-stu-id="d2c23-212">[Previous](membership-and-administration.md)
[Next](aspnet-error-handling.md)</span></span>
