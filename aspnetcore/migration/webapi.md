---
title: 将从 ASP.NET Web API 迁移到 ASP.NET Core
author: ardalis
description: 了解如何将 Web API 实现从 ASP.NET Web API 迁移到 ASP.NET Core MVC。
ms.author: riande
ms.date: 05/10/2018
uid: migration/webapi
ms.openlocfilehash: 8dd969c8644525606227989ca87e41fbfae5aed1
ms.sourcegitcommit: ea7ec8d47f94cfb8e008d771f647f86bbb4baa44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2018
ms.locfileid: "37894187"
---
# <a name="migrate-from-aspnet-web-api-to-aspnet-core"></a>将从 ASP.NET Web API 迁移到 ASP.NET Core

作者：[Steve Smith](https://ardalis.com/) 和 [Scott Addie](https://scottaddie.com)

Web Api 是 HTTP 服务的访问范围广泛的客户端，包括浏览器和移动设备。 ASP.NET Core MVC 包括用于构建提供构建 web 应用程序的单个、 一致的方式的 Web Api 的支持。 在本文中，我们将演示将从 ASP.NET Web API 的 Web API 实现迁移到 ASP.NET Core MVC 所需的步骤。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/webapi/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="review-aspnet-web-api-project"></a>检查 ASP.NET Web API 项目

本文使用示例项目*ProductsApp*一文中创建[Getting Started with ASP.NET Web API 2](/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)作为其起点。 该项目中，一个简单的 ASP.NET Web API 项目配置，如下所示。

在中*Global.asax.cs*，调用`WebApiConfig.Register`:

[!code-csharp[](../migration/webapi/sample/ProductsApp/Global.asax.cs?highlight=14)]

`WebApiConfig` 在中定义*App_Start*，并具有一个静态`Register`方法：

[!code-csharp[](../migration/webapi/sample/ProductsApp/App_Start/WebApiConfig.cs?highlight=15,16,17,18,19,20)]

此类配置[的属性路由](/aspnet/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2)，但它实际上未使用项目中。 它还可以配置 ASP.NET Web API 使用的路由表。 在这种情况下，ASP.NET Web API 将预期 Url 与格式匹配 */api/ {controller} / {id}*，使用 *{id}* 可选的。

*ProductsApp*项目包括一个简单的控制器，继承自`ApiController`和公开两个方法：

[!code-csharp[](../migration/webapi/sample/ProductsApp/Controllers/ProductsController.cs?highlight=19,24)]

最后，模型*产品*，则由*ProductsApp*，是一个简单的类：

[!code-csharp[](webapi/sample/ProductsApp/Models/Product.cs)]

现在，我们已从其开始一个简单的项目，我们可以演示如何将此 Web API 项目迁移到 ASP.NET Core MVC。

## <a name="create-the-destination-project"></a>创建目标项目

使用 Visual Studio，创建一个新的空解决方案，并将其命名*WebAPIMigration*。 添加现有*ProductsApp*到其中，项目，然后将新的 ASP.NET Core Web 应用程序项目添加到解决方案。 将新项目命名*ProductsCore*。

![新建项目对话框打开到 Web 模板](webapi/_static/add-web-project.png)

接下来，选择 Web API 项目模板。 我们将迁移*ProductsApp*到此新项目的内容。

![使用 ASP.NET Core 模板列表中选择的 Web API 项目模板的新建 Web 应用程序对话框](webapi/_static/aspnet-5-webapi.png)

删除`Project_Readme.html`文件从新项目。 你的解决方案现在应如下所示：

![在显示文件和文件夹在 ProductsApp 和 ProductsCore 项目的解决方案资源管理器中打开应用程序解决方案](webapi/_static/webapimigration-solution.png)

## <a name="migrate-configuration"></a>迁移配置

ASP.NET Core 不再使用*Global.asax*， *web.config*，或*App_Start*文件夹。 相反，完成所有启动任务*Startup.cs*项目的根目录中 (请参阅[应用程序启动](../fundamentals/startup.md))。 在 ASP.NET Core MVC，基于属性的路由现在包含默认情况下时`UseMvc()`称为;，并且，这是建议的配置 Web API 的路由的方法 （Web API 初学者项目处理路由的方式）。

[!code-csharp[](../migration/webapi/sample/ProductsCore/Startup.cs?highlight=31)]

假设你想要使用属性路由今后在项目中，不需进行任何其他配置。 只需将属性根据需要向控制器和操作，就像在该示例应用`ValuesController`Web API 入门项目中包含的类：

[!code-csharp[](../migration/webapi/sample/ProductsCore/Controllers/ValuesController.cs?highlight=9,13,20,27,33,39)]

请注意是否存在 *[controller]* 第 8 行。 基于属性的路由现在支持某些令牌，如 *[controller]* 并 *[操作]*。 这些标记分别被替换为在运行时的控制器或操作的名称，已向其应用了该属性。 此选项可用于减少的魔幻字符串在项目中，并确保路由将保持同步，包括其相应的控制器和操作应用自动重命名重构时。

若要迁移产品 API 控制器，我们首先必须复制*ProductsController*到新的项目。 然后只需包含在控制器上的路由属性：

```csharp
[Route("api/[controller]")]
```

此外需要添加`[HttpGet]`属性的两个方法，因为它们都应通过 HTTP Get 调用。 在属性中包含"id"参数的假定条件下`GetProduct()`:

```csharp
// /api/products
[HttpGet]
...

// /api/products/1
[HttpGet("{id}")]
```

在此情况下，路由配置正确;但是，我们不能尚未测试它。 必须进行其他更改之前*ProductsController*将进行编译。

## <a name="migrate-models-and-controllers"></a>迁移模型和控制器

此简单的 Web API 项目的迁移过程的最后一步是将复制的控制器和它们所使用的任何模型。 在这种情况下，只需将复制*Controllers/ProductsController.cs*从原始到新项目。 然后，将整个模型文件夹从原始项目复制到新建一个。 调整要与新的项目名称匹配的命名空间 (*ProductsCore*)。  此时，可以生成应用程序，并会发现多个编译错误。 这些通常应属于以下类别：

* *ApiController*不存在

* *System.Web.Http*命名空间不存在

* *IHttpActionResult*不存在

幸运的是，这些是所有非常容易解决：

* 更改*ApiController*到*控制器*(可能需要添加*使用 Microsoft.AspNetCore.Mvc*)

* 删除任何使用语句引用*System.Web.Http*

* 更改任何方法返回*IHttpActionResult*返回*IActionResult*

这些更改后和未使用 using 语句中删除，已迁移*ProductsController*类如下所示：

[!code-csharp[](../migration/webapi/sample/ProductsCore/Controllers/ProductsController.cs?highlight=1,2,6,8,9,27)]

现在应能够运行已迁移的项目，并浏览到 */api/产品*; 然后，应看到三个产品的完整列表。 浏览到 */api/products/1* ，应会看到的第一个产品。

## <a name="aspnet-4x-web-api-2-compatibility-shim"></a>ASP.NET 4.x Web API 2 的兼容性填充程序

迁移 ASP.NET Web API 项目到 ASP.NET Core 时的有用工具是[Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim)库。 兼容性填充码扩展 ASP.NET Core 以允许不同的 Web API 2 约定，要使用的数目。 移植之前在本文档中的示例是基本兼容性填充程序不是必需的。 对于大型项目，使用兼容性填充码可用于临时之间的隔阂 API ASP.NET Core 和 ASP.NET Web API 2。

Web API 兼容性填充码旨在作为临时的度量值用于促进将大型 Web API 项目迁移到 ASP.NET Core。 随着时间推移，应更新项目以使用 ASP.NET Core 模式，而不是依靠兼容性填充码。

中包含的兼容性功能`Microsoft.AspNetCore.Mvc.WebApiCompatShim`包括：

* 添加`ApiController`类型，以便控制器的基类型不需要更新。
* 启用 Web API 样式模型绑定。 类似于 MVC 5，默认情况下，ASP.NET Core MVC 模型绑定功能。 兼容性填充程序更改模型绑定是更类似于 Web API 2 模型绑定约定。 例如，复杂类型自动绑定从请求正文。
* 扩展模型绑定，以便控制器操作可以采取的类型参数`HttpRequestMessage`。
* 添加消息格式化程序，允许的操作以返回类型的结果`HttpResponseMessage`。
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
* 添加的一个实例`IContentNegotiator`到应用的 DI 容器和使内容协商相关类型从[Microsoft.AspNet.WebApi.Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/)可用。 这包括类型，如`DefaultContentNegotiator`， `MediaTypeFormatter`，等等。

若要使用兼容性修补程序，需要：

* 安装[Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) NuGet 包。
* 兼容性修补程序的服务注册应用程序的 DI 容器通过调用`services.AddMvc().AddWebApiConventions()`在应用的`Startup.ConfigureServices`方法。
* 定义使用特定于 Web API 的路由`MapWebApiRoute`上`IRouteBuilder`在应用的`IApplicationBuilder.UseMvc`调用。

## <a name="summary"></a>总结

将一个简单的 ASP.NET Web API 项目迁移到 ASP.NET Core MVC 将非常简单，感谢到 ASP.NET Core MVC 中的 Web Api 的内置支持。 每个 ASP.NET Web API 项目将需要迁移的主要部分是路由、 控制器和模型，以及对使用控制器和操作的类型的更新。
