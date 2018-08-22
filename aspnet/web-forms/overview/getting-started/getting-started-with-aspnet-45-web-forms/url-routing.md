---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL 路由 |Microsoft Docs
author: Erikre
description: 本教程系列将指导您学习生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: d9f0779d560d6ec7796a16dc2996b959dd171c80
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824634"
---
<a name="url-routing"></a>URL 路由
====================
通过[Erik Reitan](https://github.com/Erikre)

[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 此教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。 Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)可随附于本系列教程。


在本教程中，您将修改 Wingtip Toys 示例应用程序，支持 URL 路由。 路由，使用 Url 友好、 更轻松地请记住，且被搜索引擎更好地支持将 web 应用程序。 本教程上一教程为基础"成员身份和管理"，并为 Wingtip Toys 教程系列的一部分。

## <a name="what-youll-learn"></a>你将学习：

- 如何注册 ASP.NET Web 窗体应用程序的路由。
- 如何将路由添加到 web 页。
- 如何从支持的路由的数据库选择数据。

## <a name="aspnet-routing-overview"></a>ASP.NET 路由概述

URL 路由可配置为接受的应用程序请求不会映射到物理文件的 Url。 请求 URL 是只需用户输入到浏览器在网站上查找页的 URL。 使用路由来定义的语义上对用户有意义以及可帮助使用搜索引擎搜索引擎优化 (SEO) 的 Url。

默认情况下，Web 窗体模板包括[ASP.NET 友好 Url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)。 将通过使用实现大部分基本路由工作*友好的 Url*。 但是，在本教程将添加自定义的路由功能。

在自定义 URL 的路由之前, Wingtip Toys 示例应用程序可以链接到产品使用以下 URL:

`https://localhost:44300/ProductDetails.aspx?productID=2`

通过自定义 URL 的路由，Wingtip Toys 示例应用程序将链接到相同的产品使用易于阅读 URL:

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a>路由

路由是映射到处理程序的 URL 模式。 该处理程序可以是物理文件，例如 Web 窗体应用程序中的.aspx 文件。 一个处理程序还可以处理请求的类。 若要定义的路由，请通过指定的 URL 模式、 处理程序和 （可选） 单击路由名称创建路由类的实例。

您通过添加到应用程序添加路由`Route`对象对静态`Routes`属性的`RouteTable`类。 路由属性是`RouteCollection`对象，用于存储应用程序的所有路由。

### <a name="url-patterns"></a>URL 模式

URL 模式可以包含文字值和变量 （称为 URL 参数） 的占位符。 文本和占位符中由斜杠分隔的 URL 段的位置 (`/`) 字符。

发出对 web 应用程序的请求后，URL 解析为段和占位符，并且变量值提供给请求处理程序。 此过程是类似于分析查询字符串中的数据并将其传递给请求处理程序的方式。 在这两种情况下，变量信息是包含在 URL 中且传递到中的键 / 值对形式的处理程序。 查询字符串键和值是在 URL 中。 对于路由，密钥是 URL 模式中定义的占位符名称和 URL 中的仅值。

通过将它们括在大括号在 URL 模式中，定义占位符 (`{`和`}`)。 您可以定义多个占位符在段中，但占位符必须分隔文本值。 例如，`{language}-{country}/{action}`是有效的路由模式。 但是，`{language}{country}/{action}`不是有效的模式，因为没有文本值或占位符之间的分隔符。 因此，路由不能确定位置的值分隔开的语言占位符的值的国家/地区占位符。

### <a name="mapping-and-registering-routes"></a>映射和注册的路由

可以包括到 Wingtip Toys 示例应用程序的页面的路由之前，必须在应用程序启动时注册路由。 若要注册的路由，您将修改`Application_Start`事件处理程序。

1. 在中**解决方案资源管理器**的 Visual Studio 中，找到并打开*Global.asax.cs*文件。
2. 添加到的黄色突出显示的代码*Global.asax.cs*文件，如下所示：   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

当 Wingtip Toys 示例应用程序启动时，它将调用`Application_Start`事件处理程序。 此事件处理程序末尾`RegisterCustomRoutes`调用方法。 `RegisterCustomRoutes`方法将每个路由添加通过调用`MapPageRoute`方法的`RouteCollection`对象。 使用路由名称、 路由 URL 和物理 URL 定义路由。

第一个参数 ("`ProductsByCategoryRoute`") 是路由名称。 它用于在需要时调用的路由。 第二个参数 ("`Category/{categoryName}`") 定义可以是动态的 URL 基于代码友好替换。 将填充与生成基于数据的链接的数据控件时使用此路由。 路由所示，如下所示：

[!code-csharp[Main](url-routing/samples/sample2.cs)]

路由的第二个参数包含由大括号指定一个动态值 (`{ }`)。 在这种情况下，`categoryName`是一个变量，用于确定适当的路由路径。

> [!NOTE] 
> 
> **Optional**
> 
> 你可能会发现可以更轻松地管理您的代码通过移动`RegisterCustomRoutes`到一个单独的类的方法。 在中*逻辑*文件夹中，创建一个单独`RouteActions`类。 移动上述`RegisterCustomRoutes`方法从*Global.asax.cs*到新文件`RoutesActions`类。 使用`RoleActions`类和`createAdmin`为了举例说明如何调用的方法`RegisterCustomRoutes`方法从*Global.asax.cs*文件。


您可能还会发现`RegisterRoutes`方法调用使用`RouteConfig`对象的开始处`Application_Start`事件处理程序。 进行此调用以实现默认路由。 创建使用 Visual Studio 的 Web 窗体模板的应用程序时，它是作为默认代码。

## <a name="retrieving-and-using-route-data"></a>检索和使用路由数据

如上所述，可以定义路由。 添加到代码`Application_Start`中的事件处理程序*Global.asax.cs*文件加载的可定义的路由。

### <a name="setting-routes"></a>设置路由

路由要求添加额外的代码。 在本教程中，您将使用模型绑定来检索`RouteValueDictionary`生成使用数据控件中的数据的路由时使用的对象。 `RouteValueDictionary`对象将包含属于产品的特定类别的产品名称的列表。 根据数据和路由每个产品创建的链接。

#### <a name="enable-routes-for-categories-and-products"></a>启用路由的类别和产品

接下来，将更新应用程序以使用`ProductsByCategoryRoute`确定正确的路由，以便将包含在每个产品类别链接。 此外会更新*ProductList.aspx*页以包含每个产品的路由的链接。 链接将显示前更改，但链接现在将使用 URL 路由。

1. 在中**解决方案资源管理器**，打开*Site.Master*页上，如果已打开。
2. 更新**ListView**控件命名为"`categoryList`"以黄色突出显示的更改，因此标记将出现，如下所示：   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. 在中**解决方案资源管理器**，打开*ProductList.aspx*页。
4. 更新`ItemTemplate`的元素*ProductList.aspx*使标记，如下所示显示以黄色突出显示的更新的页：   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. 打开的代码隐藏*ProductList.aspx.cs*并将以下命名空间添加以黄色突出显示为：  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. 替换`GetProducts`方法的代码隐藏 (*ProductList.aspx.cs*) 使用以下代码：   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a>将代码添加有关产品的详细信息

现在，更新代码隐藏 (*ProductDetails.aspx.cs*) 用于*ProductDetails.aspx*页后，可以使用路由数据。 请注意，新`GetProduct`方法还接受的用户具有设置为书签的链接的情况下，使用较旧的非兼容的、 非路由 URL 的查询字符串值。

1. 替换`GetProduct`方法的代码隐藏 (*ProductDetails.aspx.cs*) 使用以下代码：   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a>运行应用程序

可以运行应用程序现在以查看更新的路由。

1. 按**F5**运行 Wingtip Toys 示例应用程序。  
 在浏览器将打开并显示*Default.aspx*页。
2. 单击**产品**在页面顶部的链接。  
 上显示所有产品*ProductList.aspx*页。 （使用端口号） 的以下 URL 显示为浏览器：  
    `https://localhost:44300/ProductList`
3. 接下来，单击**汽车**页面顶部附近的类别链接。  
 上显示仅汽车*ProductList.aspx*页。 （使用端口号） 的以下 URL 显示为浏览器：  
    `https://localhost:44300/Category/Cars`
4. 单击页面列出包含名称的第一辆车的链接 ("**可转换为汽车**") 以显示产品详细信息。  
 （使用端口号） 的以下 URL 显示为浏览器：  
    `https://localhost:44300/Product/Convertible%20Car`
5. 接下来，输入到浏览器中的以下非路由 URL （使用端口号）：  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 该代码仍会识别包含查询字符串时，用户在其中具有设置为书签的链接的情况下的 URL。

## <a name="summary"></a>总结

在本教程中，您添加了类别和产品的路由。 介绍了如何使用模型绑定的数据控件与集成的路由。 在下一步的教程中，您将实现全局错误处理。

## <a name="additional-resources"></a>其他资源

[ASP.NET 友好 Url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[包含成员资格、 OAuth 和 SQL 数据库的安全的 ASP.NET Web 窗体应用部署到 Azure 应用服务](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure-免费试用版](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [上一页](membership-and-administration.md)
> [下一页](aspnet-error-handling.md)
