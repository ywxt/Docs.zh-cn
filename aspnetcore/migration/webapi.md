---
title: 将从 ASP.NET Web API 迁移到 ASP.NET Core
author: ardalis
description: 了解如何将 Web API 实现从 ASP.NET Web API 迁移到 ASP.NET Core MVC。
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
# <a name="migrate-from-aspnet-web-api-to-aspnet-core"></a><span data-ttu-id="a16f8-103">将从 ASP.NET Web API 迁移到 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a16f8-103">Migrate from ASP.NET Web API to ASP.NET Core</span></span>

<span data-ttu-id="a16f8-104">作者：[Steve Smith](https://ardalis.com/) 和 [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="a16f8-104">By [Steve Smith](https://ardalis.com/) and [Scott Addie](https://scottaddie.com)</span></span>

<span data-ttu-id="a16f8-105">Web Api 是覆盖广泛的客户端，包括浏览器和移动设备的 HTTP 服务。</span><span class="sxs-lookup"><span data-stu-id="a16f8-105">Web APIs are HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="a16f8-106">ASP.NET Core MVC 包括用于构建提供构建 web 应用程序的单个、 一致的方式的 Web Api 的支持。</span><span class="sxs-lookup"><span data-stu-id="a16f8-106">ASP.NET Core MVC includes support for building Web APIs providing a single, consistent way of building web applications.</span></span> <span data-ttu-id="a16f8-107">在本文中，我们将演示将从 ASP.NET Web API 的 Web API 实现迁移到 ASP.NET Core MVC 所需的步骤。</span><span class="sxs-lookup"><span data-stu-id="a16f8-107">In this article, we demonstrate the steps required to migrate a Web API implementation from ASP.NET Web API to ASP.NET Core MVC.</span></span>

<span data-ttu-id="a16f8-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/webapi/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="a16f8-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/webapi/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="review-aspnet-web-api-project"></a><span data-ttu-id="a16f8-109">检查 ASP.NET Web API 项目</span><span class="sxs-lookup"><span data-stu-id="a16f8-109">Review ASP.NET Web API Project</span></span>

<span data-ttu-id="a16f8-110">本文章将使用示例项目中， *ProductsApp*文章中创建[Getting Started with ASP.NET Web API 2](/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)作为其起点。</span><span class="sxs-lookup"><span data-stu-id="a16f8-110">This article uses the sample project, *ProductsApp*, created in the article [Getting Started with ASP.NET Web API 2](/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) as its starting point.</span></span> <span data-ttu-id="a16f8-111">在该项目中，一个简单的 ASP.NET Web API 项目，如下所示配置。</span><span class="sxs-lookup"><span data-stu-id="a16f8-111">In that project, a simple ASP.NET Web API  project is configured as follows.</span></span>

<span data-ttu-id="a16f8-112">在*Global.asax.cs*，调用了`WebApiConfig.Register`:</span><span class="sxs-lookup"><span data-stu-id="a16f8-112">In *Global.asax.cs*, a call is made to `WebApiConfig.Register`:</span></span>

[!code-csharp[](../migration/webapi/sample/ProductsApp/Global.asax.cs?highlight=14)]

<span data-ttu-id="a16f8-113">`WebApiConfig` 在中定义*App_Start*，并具有一个静态`Register`方法：</span><span class="sxs-lookup"><span data-stu-id="a16f8-113">`WebApiConfig` is defined in *App_Start*, and has just one static `Register` method:</span></span>

[!code-csharp[](../migration/webapi/sample/ProductsApp/App_Start/WebApiConfig.cs?highlight=15,16,17,18,19,20)]


<span data-ttu-id="a16f8-114">此类配置[的属性路由](https://docs.microsoft.com/aspnet/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2)，不过它实际上并没有用于在项目中。</span><span class="sxs-lookup"><span data-stu-id="a16f8-114">This class configures [attribute routing](https://docs.microsoft.com/aspnet/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2), although it's not actually being used in the project.</span></span> <span data-ttu-id="a16f8-115">它还将配置路由表，它由 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="a16f8-115">It also configures the routing table, which is used by ASP.NET Web API.</span></span> <span data-ttu-id="a16f8-116">在这种情况下，ASP.NET Web API 应 Url 以匹配格式 */api/ {controller} / {id}*，与 *{id}* 正在可选。</span><span class="sxs-lookup"><span data-stu-id="a16f8-116">In this case, ASP.NET Web API will expect URLs to match the format */api/{controller}/{id}*, with *{id}* being optional.</span></span>

<span data-ttu-id="a16f8-117">*ProductsApp*项目包括一个简单的控制器，它继承自`ApiController`和公开两个方法：</span><span class="sxs-lookup"><span data-stu-id="a16f8-117">The *ProductsApp* project includes just one simple controller, which inherits from `ApiController` and exposes two methods:</span></span>

[!code-csharp[](../migration/webapi/sample/ProductsApp/Controllers/ProductsController.cs?highlight=19,24)]

<span data-ttu-id="a16f8-118">最后，模型*产品*、 所用的*ProductsApp*，是一个简单的类：</span><span class="sxs-lookup"><span data-stu-id="a16f8-118">Finally, the model, *Product*, used by the *ProductsApp*, is a simple class:</span></span>

[!code-csharp[](webapi/sample/ProductsApp/Models/Product.cs)]

<span data-ttu-id="a16f8-119">现在，我们已从其开始一个简单的项目，我们可以演示如何将此 Web API 项目迁移到 ASP.NET Core MVC。</span><span class="sxs-lookup"><span data-stu-id="a16f8-119">Now that we have a simple project from which to start, we can demonstrate how to migrate this Web API project to ASP.NET Core MVC.</span></span>

## <a name="create-the-destination-project"></a><span data-ttu-id="a16f8-120">创建目标项目</span><span class="sxs-lookup"><span data-stu-id="a16f8-120">Create the Destination Project</span></span>

<span data-ttu-id="a16f8-121">使用 Visual Studio，创建一个新的空解决方案，并将其命名*WebAPIMigration*。</span><span class="sxs-lookup"><span data-stu-id="a16f8-121">Using Visual Studio, create a new, empty solution, and name it *WebAPIMigration*.</span></span> <span data-ttu-id="a16f8-122">添加现有*ProductsApp*到其中，项目，然后将新的 ASP.NET Core Web 应用程序项目添加到解决方案。</span><span class="sxs-lookup"><span data-stu-id="a16f8-122">Add the existing *ProductsApp* project to it, then, add a new ASP.NET Core Web Application Project to the solution.</span></span> <span data-ttu-id="a16f8-123">将新项目*ProductsCore*。</span><span class="sxs-lookup"><span data-stu-id="a16f8-123">Name the new project *ProductsCore*.</span></span>

![新建项目对话框打开到 Web 模板](webapi/_static/add-web-project.png)

<span data-ttu-id="a16f8-125">接下来，选择 Web API 项目模板。</span><span class="sxs-lookup"><span data-stu-id="a16f8-125">Next, choose the Web API project template.</span></span> <span data-ttu-id="a16f8-126">我们会将迁移*ProductsApp*到此新项目的内容。</span><span class="sxs-lookup"><span data-stu-id="a16f8-126">We will migrate the *ProductsApp* contents to this new project.</span></span>

![使用 ASP.NET Core 模板列表中选择的 Web API 项目模板的新建 Web 应用程序对话框](webapi/_static/aspnet-5-webapi.png)

<span data-ttu-id="a16f8-128">删除`Project_Readme.html`文件从新项目。</span><span class="sxs-lookup"><span data-stu-id="a16f8-128">Delete the `Project_Readme.html` file from the new project.</span></span> <span data-ttu-id="a16f8-129">你的解决方案现在应如下所示：</span><span class="sxs-lookup"><span data-stu-id="a16f8-129">Your solution should now look like this:</span></span>

![在显示文件和文件夹 ProductsApp 和 ProductsCore 项目的解决方案资源管理器中打开应用程序解决方案](webapi/_static/webapimigration-solution.png)

## <a name="migrate-configuration"></a><span data-ttu-id="a16f8-131">迁移配置</span><span class="sxs-lookup"><span data-stu-id="a16f8-131">Migrate Configuration</span></span>

<span data-ttu-id="a16f8-132">ASP.NET Core不再使用*Global.asax*， *web.config*，或*App_Start*文件夹。</span><span class="sxs-lookup"><span data-stu-id="a16f8-132">ASP.NET Core no longer uses *Global.asax*, *web.config*, or *App_Start* folders.</span></span> <span data-ttu-id="a16f8-133">相反，所有启动任务都在都完成*Startup.cs*项目的根目录中 (请参阅[应用程序启动](../fundamentals/startup.md))。</span><span class="sxs-lookup"><span data-stu-id="a16f8-133">Instead, all startup tasks are done in *Startup.cs* in the root of the project (see [Application Startup](../fundamentals/startup.md)).</span></span> <span data-ttu-id="a16f8-134">在 ASP.NET Core MVC，基于属性的路由现在包含默认情况下时`UseMvc()`称为;，并且，这是建议的配置 Web API 的路由的方法 （Web API 初学者项目处理路由的方式）。</span><span class="sxs-lookup"><span data-stu-id="a16f8-134">In ASP.NET Core MVC, attribute-based routing is now included by default when `UseMvc()` is called; and, this is the recommended approach for configuring Web API routes (and is how the Web API starter project handles routing).</span></span>

[!code-csharp[](../migration/webapi/sample/ProductsCore/Startup.cs?highlight=31)]

<span data-ttu-id="a16f8-135">假设你想要使用你今后的项目中的属性路由，不需进行任何其他配置。</span><span class="sxs-lookup"><span data-stu-id="a16f8-135">Assuming you want to use attribute routing in your project going forward, no additional configuration is needed.</span></span> <span data-ttu-id="a16f8-136">只需将应用的属性，根据需要向你的控制器和操作，在此示例中的做法一样`ValuesController`Web API 初学者项目中包含的类：</span><span class="sxs-lookup"><span data-stu-id="a16f8-136">Simply apply the attributes as needed to your controllers and actions, as is done in the sample `ValuesController` class that's included in the Web API starter project:</span></span>

[!code-csharp[](../migration/webapi/sample/ProductsCore/Controllers/ValuesController.cs?highlight=9,13,20,27,33,39)]

<span data-ttu-id="a16f8-137">请注意是否存在 *[控制器]* 第 8 行。</span><span class="sxs-lookup"><span data-stu-id="a16f8-137">Note the presence of *[controller]* on line 8.</span></span> <span data-ttu-id="a16f8-138">基于属性的路由现在支持某些令牌，如 *[控制器]* 和 *[操作]*。</span><span class="sxs-lookup"><span data-stu-id="a16f8-138">Attribute-based routing now supports certain tokens, such as *[controller]* and *[action]*.</span></span> <span data-ttu-id="a16f8-139">这些标记分别被替换为在运行时的控制器或操作，名称，已向其应用该属性。</span><span class="sxs-lookup"><span data-stu-id="a16f8-139">These tokens are replaced at runtime with the name of the controller or action, respectively, to which the attribute has been applied.</span></span> <span data-ttu-id="a16f8-140">此选项可用于减少了大量神奇字符串在项目中，并确保路由将保留其相应的控制器和操作与同步时自动重命名重构应用。</span><span class="sxs-lookup"><span data-stu-id="a16f8-140">This serves to reduce the number of magic strings in the project, and it ensures the routes will be kept synchronized with their corresponding controllers and actions when automatic rename refactorings are applied.</span></span>

<span data-ttu-id="a16f8-141">若要迁移的产品的 API 控制器，我们必须首先将复制*ProductsController*到新项目。</span><span class="sxs-lookup"><span data-stu-id="a16f8-141">To migrate the Products API controller, we must first copy *ProductsController* to the new project.</span></span> <span data-ttu-id="a16f8-142">然后只需包括在控制器上的 route 属性：</span><span class="sxs-lookup"><span data-stu-id="a16f8-142">Then simply include the route attribute on the controller:</span></span>

```csharp
[Route("api/[controller]")]
```

<span data-ttu-id="a16f8-143">你还需要添加`[HttpGet]`属性设为两种方法，因为它们都应通过 HTTP Get 调用。</span><span class="sxs-lookup"><span data-stu-id="a16f8-143">You also need to add the `[HttpGet]` attribute to the two methods, since they both should be called via HTTP Get.</span></span> <span data-ttu-id="a16f8-144">有关特性中包括的"id"参数的假定条件下`GetProduct()`:</span><span class="sxs-lookup"><span data-stu-id="a16f8-144">Include the expectation of an "id" parameter in the attribute for `GetProduct()`:</span></span>

```csharp
// /api/products
[HttpGet]
...

// /api/products/1
[HttpGet("{id}")]
```

<span data-ttu-id="a16f8-145">此时，路由配置正确;但是，我们无法一尚未将其测试。</span><span class="sxs-lookup"><span data-stu-id="a16f8-145">At this point, routing is configured correctly; however, we can't yet test it.</span></span> <span data-ttu-id="a16f8-146">必须在之前进行其他更改*ProductsController*将进行编译。</span><span class="sxs-lookup"><span data-stu-id="a16f8-146">Additional changes must be made before *ProductsController* will compile.</span></span>

## <a name="migrate-models-and-controllers"></a><span data-ttu-id="a16f8-147">迁移模型和控制器</span><span class="sxs-lookup"><span data-stu-id="a16f8-147">Migrate Models and Controllers</span></span>

<span data-ttu-id="a16f8-148">此简单的 Web API 项目的迁移过程的最后一步是将复制到控制器，它们使用的所有模型。</span><span class="sxs-lookup"><span data-stu-id="a16f8-148">The last step in the migration process for this simple Web API project is to copy over the Controllers and any Models they use.</span></span> <span data-ttu-id="a16f8-149">在这种情况下，只需复制*Controllers/ProductsController.cs*从原始到新项目。</span><span class="sxs-lookup"><span data-stu-id="a16f8-149">In this case, simply copy *Controllers/ProductsController.cs* from the original project to the new one.</span></span> <span data-ttu-id="a16f8-150">然后，将整个模型文件夹从原始项目复制到新的一个。</span><span class="sxs-lookup"><span data-stu-id="a16f8-150">Then, copy the entire Models folder from the original project to the new one.</span></span> <span data-ttu-id="a16f8-151">调整要与新的项目名称匹配的命名空间 (*ProductsCore*)。</span><span class="sxs-lookup"><span data-stu-id="a16f8-151">Adjust the namespaces to match the new project name (*ProductsCore*).</span></span>  <span data-ttu-id="a16f8-152">此时，可以生成应用程序，并且你将找到大量的编译错误。</span><span class="sxs-lookup"><span data-stu-id="a16f8-152">At this point, you can build the application, and you will find a number of compilation errors.</span></span> <span data-ttu-id="a16f8-153">这些通常应属于以下类别：</span><span class="sxs-lookup"><span data-stu-id="a16f8-153">These should generally fall into the following categories:</span></span>

* <span data-ttu-id="a16f8-154">*ApiController*不存在</span><span class="sxs-lookup"><span data-stu-id="a16f8-154">*ApiController* does not exist</span></span>

* <span data-ttu-id="a16f8-155">*System.Web.Http*命名空间不存在</span><span class="sxs-lookup"><span data-stu-id="a16f8-155">*System.Web.Http* namespace does not exist</span></span>

* <span data-ttu-id="a16f8-156">*IHttpActionResult*不存在</span><span class="sxs-lookup"><span data-stu-id="a16f8-156">*IHttpActionResult* does not exist</span></span>

<span data-ttu-id="a16f8-157">幸运的是，这些是所有很容易更正：</span><span class="sxs-lookup"><span data-stu-id="a16f8-157">Fortunately, these are all very easy to correct:</span></span>

* <span data-ttu-id="a16f8-158">更改*ApiController*到*控制器*(可能需要添加*使用 Microsoft.AspNetCore.Mvc*)</span><span class="sxs-lookup"><span data-stu-id="a16f8-158">Change *ApiController* to *Controller* (you may need to add *using Microsoft.AspNetCore.Mvc*)</span></span>

* <span data-ttu-id="a16f8-159">删除任何使用语句引用*System.Web.Http*</span><span class="sxs-lookup"><span data-stu-id="a16f8-159">Delete any using statement referring to *System.Web.Http*</span></span>

* <span data-ttu-id="a16f8-160">更改任何方法返回*IHttpActionResult*返回*IActionResult*</span><span class="sxs-lookup"><span data-stu-id="a16f8-160">Change any method returning *IHttpActionResult* to return a *IActionResult*</span></span>

<span data-ttu-id="a16f8-161">一旦后这些更改已生成且未使用 using 语句中删除，已迁移*ProductsController*类类似如下所示：</span><span class="sxs-lookup"><span data-stu-id="a16f8-161">Once these changes have been made and unused using statements removed, the migrated *ProductsController* class looks like this:</span></span>

[!code-csharp[](../migration/webapi/sample/ProductsCore/Controllers/ProductsController.cs?highlight=1,2,6,8,9,27)]

<span data-ttu-id="a16f8-162">你现在应能够运行已迁移的项目，浏览到 */api/产品*; 而且，你应看到 3 产品的完整列表。</span><span class="sxs-lookup"><span data-stu-id="a16f8-162">You should now be able to run the migrated project and browse to */api/products*; and, you should see the full list of 3 products.</span></span> <span data-ttu-id="a16f8-163">浏览到 */api/products/1* ，你应看到第一个产品。</span><span class="sxs-lookup"><span data-stu-id="a16f8-163">Browse to */api/products/1* and you should see the first product.</span></span>

## <a name="microsoftaspnetcoremvcwebapicompatshim"></a><span data-ttu-id="a16f8-164">Microsoft.AspNetCore.Mvc.WebApiCompatShim</span><span class="sxs-lookup"><span data-stu-id="a16f8-164">Microsoft.AspNetCore.Mvc.WebApiCompatShim</span></span>

<span data-ttu-id="a16f8-165">迁移 ASP.NET Web API 项目到 ASP.NET Core时的有用工具是[Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim)库。</span><span class="sxs-lookup"><span data-stu-id="a16f8-165">A useful tool when migrating ASP.NET Web API projects to ASP.NET Core is the [Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) library.</span></span> <span data-ttu-id="a16f8-166">兼容性填充码扩展 ASP.NET Core以允许不同的 Web API 2 约定，要使用的数目。</span><span class="sxs-lookup"><span data-stu-id="a16f8-166">The compatibility shim extends ASP.NET Core to allow a number of different Web API 2 conventions to be used.</span></span> <span data-ttu-id="a16f8-167">本文档中进行迁移，以前的示例是基本的兼容性填充程序不是所必需的。</span><span class="sxs-lookup"><span data-stu-id="a16f8-167">The sample ported previously in this document is basic enough that the compatibility shim was not necessary.</span></span> <span data-ttu-id="a16f8-168">对于大型项目，使用兼容性填充码可用于临时之间的隔阂 API ASP.NET Core 和 ASP.NET Web API 2。</span><span class="sxs-lookup"><span data-stu-id="a16f8-168">For larger projects, using the compatibility shim can be useful for temporarily bridging the API gap between ASP.NET Core and ASP.NET Web API 2.</span></span>

<span data-ttu-id="a16f8-169">Web API 兼容性填充码旨在作为临时的度量值用于促进将大型 Web API 项目迁移到 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="a16f8-169">The Web API compatibility shim is meant to be used as a temporary measure to facilitate migrating large Web API projects to ASP.NET Core.</span></span> <span data-ttu-id="a16f8-170">随着时间推移，应更新项目以使用 ASP.NET Core 模式，而不是依靠兼容性填充码。</span><span class="sxs-lookup"><span data-stu-id="a16f8-170">Over time, projects should be updated to use ASP.NET Core patterns instead of relying on the compatibility shim.</span></span> 

<span data-ttu-id="a16f8-171">Microsoft.AspNetCore.Mvc.WebApiCompatShim 中包含的兼容性功能包括：</span><span class="sxs-lookup"><span data-stu-id="a16f8-171">Compatibility features included in Microsoft.AspNetCore.Mvc.WebApiCompatShim include:</span></span>

* <span data-ttu-id="a16f8-172">将添加`ApiController`类型，以便控制器的基类型不需要更新。</span><span class="sxs-lookup"><span data-stu-id="a16f8-172">Adds an `ApiController` type so that controllers' base types don't need to be updated.</span></span>
* <span data-ttu-id="a16f8-173">使 Web API 样式模型绑定。</span><span class="sxs-lookup"><span data-stu-id="a16f8-173">Enables Web API-style model binding.</span></span> <span data-ttu-id="a16f8-174">类似于 MVC 5，默认情况下，ASP.NET Core MVC 模型绑定功能。</span><span class="sxs-lookup"><span data-stu-id="a16f8-174">ASP.NET Core MVC model binding functions similarly to MVC 5, by default.</span></span> <span data-ttu-id="a16f8-175">兼容性填充码更改模型要更类似于 Web API 2 模型绑定约定绑定。</span><span class="sxs-lookup"><span data-stu-id="a16f8-175">The compatibility shim changes model binding to be more similar to Web API 2 model binding conventions.</span></span> <span data-ttu-id="a16f8-176">例如，复杂类型自动绑定从请求正文。</span><span class="sxs-lookup"><span data-stu-id="a16f8-176">For example, complex types are automatically bound from the request body.</span></span>
* <span data-ttu-id="a16f8-177">将扩展模型绑定，以便控制器操作可以采用参数类型`HttpRequestMessage`。</span><span class="sxs-lookup"><span data-stu-id="a16f8-177">Extends model binding so that controller actions can take parameters of type `HttpRequestMessage`.</span></span>
* <span data-ttu-id="a16f8-178">添加消息格式化程序允许操作来返回结果类型`HttpResponseMessage`。</span><span class="sxs-lookup"><span data-stu-id="a16f8-178">Adds message formatters allowing actions to return results of type `HttpResponseMessage`.</span></span>
* <span data-ttu-id="a16f8-179">添加 Web API 2 操作可能具有用于为响应提供服务的其他响应方法：</span><span class="sxs-lookup"><span data-stu-id="a16f8-179">Adds additional response methods that Web API 2 actions may have used to serve responses:</span></span>
    * <span data-ttu-id="a16f8-180">HttpResponseMessage 生成器：</span><span class="sxs-lookup"><span data-stu-id="a16f8-180">HttpResponseMessage generators:</span></span>
        * `CreateResponse<T>`
        * `CreateErrorResponse`
    * <span data-ttu-id="a16f8-181">结果的操作方法：</span><span class="sxs-lookup"><span data-stu-id="a16f8-181">Action result methods:</span></span>
        * `BadRequestErrorMessageResult`
        * `ExceptionResult`
        * `InternalServerErrorResult`
        * `InvalidModelStateResult`
        * `NegotiatedContentResult`
        * `ResponseMessageResult`
* <span data-ttu-id="a16f8-182">将的实例添加`IContentNegotiator`到应用程序的 DI 容器和使内容从协商相关类型[Microsoft.AspNet.WebApi.Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/)可用。</span><span class="sxs-lookup"><span data-stu-id="a16f8-182">Adds an instance of `IContentNegotiator` to the app's DI container and makes content negotiation-related types from [Microsoft.AspNet.WebApi.Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) available.</span></span> <span data-ttu-id="a16f8-183">这包括类型，如`DefaultContentNegotiator`， `MediaTypeFormatter`，等等。</span><span class="sxs-lookup"><span data-stu-id="a16f8-183">This includes types like `DefaultContentNegotiator`, `MediaTypeFormatter`, etc.</span></span>

<span data-ttu-id="a16f8-184">若要使用的兼容性填充码，你需要：</span><span class="sxs-lookup"><span data-stu-id="a16f8-184">To use the compatibility shim, you need to:</span></span>

* <span data-ttu-id="a16f8-185">引用[Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="a16f8-185">Reference the [Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) NuGet package.</span></span>
* <span data-ttu-id="a16f8-186">兼容性填充码的服务注册应用程序的 DI 容器通过调用`services.AddWebApiConventions()`中应用程序的`Startup.ConfigureServices`方法。</span><span class="sxs-lookup"><span data-stu-id="a16f8-186">Register the compatibility shim's services with the app's DI container by calling `services.AddWebApiConventions()` in the application's `Startup.ConfigureServices` method.</span></span>
* <span data-ttu-id="a16f8-187">定义使用的 Web API 的特定路由`MapWebApiRoute`上`IRouteBuilder`中应用程序的`IApplicationBuilder.UseMvc`调用。</span><span class="sxs-lookup"><span data-stu-id="a16f8-187">Define Web API-specific routes using `MapWebApiRoute` on the `IRouteBuilder` in the application's `IApplicationBuilder.UseMvc` call.</span></span>

## <a name="summary"></a><span data-ttu-id="a16f8-188">总结</span><span class="sxs-lookup"><span data-stu-id="a16f8-188">Summary</span></span>

<span data-ttu-id="a16f8-189">将一个简单的 ASP.NET Web API 项目迁移到 ASP.NET Core MVC 将非常简单，感谢到 ASP.NET Core MVC 中的 Web Api 的内置支持。</span><span class="sxs-lookup"><span data-stu-id="a16f8-189">Migrating a simple ASP.NET Web API project to ASP.NET Core MVC is fairly straightforward, thanks to the built-in support for Web APIs in ASP.NET Core MVC.</span></span> <span data-ttu-id="a16f8-190">每个 ASP.NET Web API 项目将需要迁移的主要部分是路由、 控制器和模型，以及更新到控制器和操作由使用的类型。</span><span class="sxs-lookup"><span data-stu-id="a16f8-190">The main pieces every ASP.NET Web API project will need to migrate are routes, controllers, and models, along with updates to the types used by  controllers and actions.</span></span>
