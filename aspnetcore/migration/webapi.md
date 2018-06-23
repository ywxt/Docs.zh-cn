---
title: 将从 ASP.NET Web API 迁移到 ASP.NET 核心
author: ardalis
description: 了解如何将 Web API 实现从 ASP.NET Web API 迁移到 ASP.NET 核心 MVC。
ms.author: riande
ms.date: 05/10/2018
uid: migration/webapi
ms.openlocfilehash: 4f4dc140bd60463037be0757176dcf7a619918bd
ms.sourcegitcommit: 79b756ea03eae77a716f500ef88253ee9b1464d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2018
ms.locfileid: "36327504"
---
# <a name="migrate-from-aspnet-web-api-to-aspnet-core"></a>将从 ASP.NET Web API 迁移到 ASP.NET 核心

作者：[Steve Smith](https://ardalis.com/) 和 [Scott Addie](https://scottaddie.com)

Web Api 是覆盖广泛的客户端，包括浏览器和移动设备的 HTTP 服务。 ASP.NET 核心 MVC 包括用于构建提供构建 web 应用程序的单个、 一致的方式的 Web Api 的支持。 在本文中，我们将演示将从 ASP.NET Web API 的 Web API 实现迁移到 ASP.NET 核心 MVC 所需的步骤。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/webapi/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="review-aspnet-web-api-project"></a>检查 ASP.NET Web API 项目

本文章将使用示例项目中， *ProductsApp*文章中创建[Getting Started with ASP.NET Web API 2](/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)作为其起点。 在该项目中，一个简单的 ASP.NET Web API 项目，如下所示配置。

在*Global.asax.cs*，调用了`WebApiConfig.Register`:

[!code-csharp[](../migration/webapi/sample/ProductsApp/Global.asax.cs?highlight=14)]

`WebApiConfig` 在中定义*App_Start*，并具有一个静态`Register`方法：

[!code-csharp[](../migration/webapi/sample/ProductsApp/App_Start/WebApiConfig.cs?highlight=15,16,17,18,19,20)]


此类配置[的属性路由](https://docs.microsoft.com/aspnet/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2)，不过它实际上并没有用于在项目中。 它还将配置路由表，它由 ASP.NET Web API。 在这种情况下，ASP.NET Web API 应 Url 以匹配格式 */api/ {controller} / {id}*，与 *{id}* 正在可选。

*ProductsApp*项目包括一个简单的控制器，它继承自`ApiController`和公开两个方法：

[!code-csharp[](../migration/webapi/sample/ProductsApp/Controllers/ProductsController.cs?highlight=19,24)]

最后，模型*产品*、 所用的*ProductsApp*，是一个简单的类：

[!code-csharp[](webapi/sample/ProductsApp/Models/Product.cs)]

现在，我们已从其开始一个简单的项目，我们可以演示如何将此 Web API 项目迁移到 ASP.NET 核心 MVC。

## <a name="create-the-destination-project"></a>创建目标项目

使用 Visual Studio，创建一个新的空解决方案，并将其命名*WebAPIMigration*。 添加现有*ProductsApp*到其中，项目，然后将新的 ASP.NET 核心 Web 应用程序项目添加到解决方案。 将新项目*ProductsCore*。

![新建项目对话框打开到 Web 模板](webapi/_static/add-web-project.png)

接下来，选择 Web API 项目模板。 我们会将迁移*ProductsApp*到此新项目的内容。

![使用 ASP.NET Core 模板列表中选择的 Web API 项目模板的新建 Web 应用程序对话框](webapi/_static/aspnet-5-webapi.png)

删除`Project_Readme.html`文件从新项目。 你的解决方案现在应如下所示：

![在显示文件和文件夹 ProductsApp 和 ProductsCore 项目的解决方案资源管理器中打开应用程序解决方案](webapi/_static/webapimigration-solution.png)

## <a name="migrate-configuration"></a>迁移配置

ASP.NET 核心不再使用*Global.asax*， *web.config*，或*App_Start*文件夹。 相反，所有启动任务都在都完成*Startup.cs*项目的根目录中 (请参阅[应用程序启动](../fundamentals/startup.md))。 在 ASP.NET 核心 MVC，基于属性的路由现在包含默认情况下时`UseMvc()`称为;，并且，这是建议的配置 Web API 的路由的方法 （Web API 初学者项目处理路由的方式）。

[!code-csharp[](../migration/webapi/sample/ProductsCore/Startup.cs?highlight=31)]

假设你想要使用你今后的项目中的属性路由，不需进行任何其他配置。 只需将应用的属性，根据需要向你的控制器和操作，在此示例中的做法一样`ValuesController`Web API 初学者项目中包含的类：

[!code-csharp[](../migration/webapi/sample/ProductsCore/Controllers/ValuesController.cs?highlight=9,13,20,27,33,39)]

请注意是否存在 *[控制器]* 第 8 行。 基于属性的路由现在支持某些令牌，如 *[控制器]* 和 *[操作]*。 这些标记分别被替换为在运行时的控制器或操作，名称，已向其应用该属性。 此选项可用于减少了大量神奇字符串在项目中，并确保路由将保留其相应的控制器和操作与同步时自动重命名重构应用。

若要迁移的产品的 API 控制器，我们必须首先将复制*ProductsController*到新项目。 然后只需包括在控制器上的 route 属性：

```csharp
[Route("api/[controller]")]
```

你还需要添加`[HttpGet]`属性设为两种方法，因为它们都应通过 HTTP Get 调用。 有关特性中包括的"id"参数的假定条件下`GetProduct()`:

```csharp
// /api/products
[HttpGet]
...

// /api/products/1
[HttpGet("{id}")]
```

此时，路由配置正确;但是，我们无法一尚未将其测试。 必须在之前进行其他更改*ProductsController*将进行编译。

## <a name="migrate-models-and-controllers"></a>迁移模型和控制器

此简单的 Web API 项目的迁移过程的最后一步是将复制到控制器，它们使用的所有模型。 在这种情况下，只需复制*Controllers/ProductsController.cs*从原始到新项目。 然后，将整个模型文件夹从原始项目复制到新的一个。 调整要与新的项目名称匹配的命名空间 (*ProductsCore*)。  此时，可以生成应用程序，并且你将找到大量的编译错误。 这些通常应属于以下类别：

* *ApiController*不存在

* *System.Web.Http*命名空间不存在

* *IHttpActionResult*不存在

幸运的是，这些是所有很容易更正：

* 更改*ApiController*到*控制器*(可能需要添加*使用 Microsoft.AspNetCore.Mvc*)

* 删除任何使用语句引用*System.Web.Http*

* 更改任何方法返回*IHttpActionResult*返回*IActionResult*

一旦后这些更改已生成且未使用 using 语句中删除，已迁移*ProductsController*类类似如下所示：

[!code-csharp[](../migration/webapi/sample/ProductsCore/Controllers/ProductsController.cs?highlight=1,2,6,8,9,27)]

你现在应能够运行已迁移的项目，浏览到 */api/产品*; 而且，你应看到 3 产品的完整列表。 浏览到 */api/products/1* ，你应看到第一个产品。

## <a name="microsoftaspnetcoremvcwebapicompatshim"></a>Microsoft.AspNetCore.Mvc.WebApiCompatShim

迁移 ASP.NET Web API 项目到 ASP.NET 核心时的有用工具是[Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim)库。 兼容性填充码扩展 ASP.NET 核心以允许不同的 Web API 2 约定，要使用的数目。 本文档中进行迁移，以前的示例是基本的兼容性填充程序不是所必需的。 对于大型项目，使用兼容性填充码可用于临时之间的隔阂 API ASP.NET Core 和 ASP.NET Web API 2。

Web API 兼容性填充码旨在作为临时的度量值用于促进将大型 Web API 项目迁移到 ASP.NET 核心。 随着时间推移，应更新项目以使用 ASP.NET Core 模式，而不是依靠兼容性填充码。 

Microsoft.AspNetCore.Mvc.WebApiCompatShim 中包含的兼容性功能包括：

* 将添加`ApiController`类型，以便控制器的基类型不需要更新。
* 使 Web API 样式模型绑定。 类似于 MVC 5，默认情况下，ASP.NET Core MVC 模型绑定功能。 兼容性填充码更改模型要更类似于 Web API 2 模型绑定约定绑定。 例如，复杂类型自动绑定从请求正文。
* 将扩展模型绑定，以便控制器操作可以采用参数类型`HttpRequestMessage`。
* 添加消息格式化程序允许操作来返回结果类型`HttpResponseMessage`。
* 添加 Web API 2 操作可能具有用于为响应提供服务的其他响应方法：
    * HttpResponseMessage 生成器：
        * `CreateResponse<T>`
        * `CreateErrorResponse`
    * 结果的操作方法：
        * `BadRequestErrorMessageResult`
        * `ExceptionResult`
        * `InternalServerErrorResult`
        * `InvalidModelStateResult`
        * `NegotiatedContentResult`
        * `ResponseMessageResult`
* 将的实例添加`IContentNegotiator`到应用程序的 DI 容器和使内容从协商相关类型[Microsoft.AspNet.WebApi.Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/)可用。 这包括类型，如`DefaultContentNegotiator`， `MediaTypeFormatter`，等等。

若要使用的兼容性填充码，你需要：

* 引用[Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) NuGet 包。
* 兼容性填充码的服务注册应用程序的 DI 容器通过调用`services.AddWebApiConventions()`中应用程序的`Startup.ConfigureServices`方法。
* 定义使用的 Web API 的特定路由`MapWebApiRoute`上`IRouteBuilder`中应用程序的`IApplicationBuilder.UseMvc`调用。

## <a name="summary"></a>总结

将一个简单的 ASP.NET Web API 项目迁移到 ASP.NET 核心 MVC 将非常简单，感谢到 ASP.NET 核心 MVC 中的 Web Api 的内置支持。 每个 ASP.NET Web API 项目将需要迁移的主要部分是路由、 控制器和模型，以及更新到控制器和操作由使用的类型。
