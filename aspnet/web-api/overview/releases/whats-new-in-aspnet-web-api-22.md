---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-22
title: 什么是 ASP.NET Web API 2.2 中的新增功能 |Microsoft 文档
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/25/2014
ms.topic: article
ms.assetid: 99c59ae4-167e-4f66-a6cd-d3f1098c4e4a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/releases/whats-new-in-aspnet-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 400329dd852ca3c527387ee45e3e902b725e771b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="whats-new-in-aspnet-web-api-22"></a><span data-ttu-id="e49df-102">什么是 ASP.NET Web API 2.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="e49df-102">What's New in ASP.NET Web API 2.2</span></span>
====================
<span data-ttu-id="e49df-103">通过[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e49df-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="e49df-104">本主题介绍什么是用于 ASP.NET Web API 2.2 的新功能。</span><span class="sxs-lookup"><span data-stu-id="e49df-104">This topic describes what's new for ASP.NET Web API 2.2.</span></span>

- [<span data-ttu-id="e49df-105">下载</span><span class="sxs-lookup"><span data-stu-id="e49df-105">Download</span></span>](#download)
- [<span data-ttu-id="e49df-106">文档</span><span class="sxs-lookup"><span data-stu-id="e49df-106">Documentation</span></span>](#documentation)
- [<span data-ttu-id="e49df-107">ASP.NET Web API 2.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="e49df-107">New Features in ASP.NET Web API 2.2</span></span>](#newf)

    - [<span data-ttu-id="e49df-108">OData v4</span><span class="sxs-lookup"><span data-stu-id="e49df-108">OData v4</span></span>](#OData)
    - [<span data-ttu-id="e49df-109">属性路由改进</span><span class="sxs-lookup"><span data-stu-id="e49df-109">Attribute Routing Improvements</span></span>](#ARI)
    - [<span data-ttu-id="e49df-110">Web API 客户端支持 Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="e49df-110">Web API Client support for Windows Phone 8.1</span></span>](#phone)
- [<span data-ttu-id="e49df-111">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="e49df-111">Known Issues and Breaking Changes</span></span>](#known-issues)
- [<span data-ttu-id="e49df-112">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="e49df-112">Bug Fixes</span></span>](#bug-fixes)
- [<span data-ttu-id="e49df-113">Microsoft.AspNet.OData 5.2.1 章</span><span class="sxs-lookup"><span data-stu-id="e49df-113">Microsoft.AspNet.OData 5.2.1</span></span>](#odata521)
- [<span data-ttu-id="e49df-114">Microsoft.AspNet.WebAPI 5.2.2</span><span class="sxs-lookup"><span data-stu-id="e49df-114">Microsoft.AspNet.WebAPI 5.2.2</span></span>](#522RC)
- [<span data-ttu-id="e49df-115">Microsoft.AspNet.WebAPI 5.2.3 Beta</span><span class="sxs-lookup"><span data-stu-id="e49df-115">Microsoft.AspNet.WebAPI 5.2.3 Beta</span></span>](#523)

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="e49df-116">下载</span><span class="sxs-lookup"><span data-stu-id="e49df-116">Download</span></span>

<span data-ttu-id="e49df-117">运行时功能将发布为 NuGet 库上的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e49df-117">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="e49df-118">所有运行时包按照[语义版本控制](http://semver.org/)规范。</span><span class="sxs-lookup"><span data-stu-id="e49df-118">All the runtime packages follow the [Semantic Versioning](http://semver.org/) specification.</span></span> <span data-ttu-id="e49df-119">最新的 ASP.NET Web API 2.2 包具有以下版本:"5.2.0"。</span><span class="sxs-lookup"><span data-stu-id="e49df-119">The latest ASP.NET Web API 2.2 package has the following version: "5.2.0".</span></span> <span data-ttu-id="e49df-120">你可以安装或更新这些包通过[NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/)。</span><span class="sxs-lookup"><span data-stu-id="e49df-120">You can install or update these packages through [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/).</span></span> <span data-ttu-id="e49df-121">版本还包括在 NuGet 上的相应本地化的包。</span><span class="sxs-lookup"><span data-stu-id="e49df-121">The release also includes corresponding localized packages on NuGet.</span></span>

<span data-ttu-id="e49df-122">你可以安装或使用 NuGet 程序包管理器控制台更新到已发布的 NuGet 程序包：</span><span class="sxs-lookup"><span data-stu-id="e49df-122">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-22/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="e49df-123">文档</span><span class="sxs-lookup"><span data-stu-id="e49df-123">Documentation</span></span>

<span data-ttu-id="e49df-124">教程和有关 ASP.NET Web API 2.2 的其他信息可以从 ASP.NET web 站点 ([https://www.asp.net/web-api](../../index.md))。</span><span class="sxs-lookup"><span data-stu-id="e49df-124">Tutorials and other information about ASP.NET Web API 2.2 are available from the ASP.NET web site ([https://www.asp.net/web-api](../../index.md)).</span></span>

<a id="newf"></a>
## <a name="new-features-in-aspnet-web-api-22"></a><span data-ttu-id="e49df-125">ASP.NET Web API 2.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="e49df-125">New Features in ASP.NET Web API 2.2</span></span>

<a id="OData"></a>
### <a name="odata-v4"></a><span data-ttu-id="e49df-126">OData v4</span><span class="sxs-lookup"><span data-stu-id="e49df-126">OData v4</span></span>

<span data-ttu-id="e49df-127">此版本添加了对 OData v4 协议的支持。</span><span class="sxs-lookup"><span data-stu-id="e49df-127">This release adds support for the OData v4 protocol.</span></span> <span data-ttu-id="e49df-128">有关详细信息，请参阅[Web API OData v4 文档。](../odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="e49df-128">For more information, see the [Web API OData v4 documentation.](../odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint.md)</span></span>

<span data-ttu-id="e49df-129">下面是一些主要功能和 OData v4 的更改：</span><span class="sxs-lookup"><span data-stu-id="e49df-129">Here are some of the key features and changes for OData v4:</span></span>

- [<span data-ttu-id="e49df-130">对 OData 模型中的别名属性的支持</span><span class="sxs-lookup"><span data-stu-id="e49df-130">Support for aliasing properties in OData model</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataModelAliasingSample/)
- [<span data-ttu-id="e49df-131">支持 ComplexTypeAttribute、 AssociationAttribute、 TimesTampAttribute 和 ConcurrencyCheckAttribute ODataConventionModelBuilder 中</span><span class="sxs-lookup"><span data-stu-id="e49df-131">Support for ComplexTypeAttribute, AssociationAttribute, TimesTampAttribute and ConcurrencyCheckAttribute in ODataConventionModelBuilder</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEtagSample/)
- [<span data-ttu-id="e49df-132">提供能够提供有关操作的友好标题</span><span class="sxs-lookup"><span data-stu-id="e49df-132">Provide ability to supply friendly Title for actions</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataActionsSample/)
- <span data-ttu-id="e49df-133">将与 ODL UriParser 集成</span><span class="sxs-lookup"><span data-stu-id="e49df-133">Integrate with ODL UriParser</span></span>
- <span data-ttu-id="e49df-134">支持[枚举](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEnumTypeSample/ODataEnumTypeSample/)，[包含](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)和[单一实例](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)</span><span class="sxs-lookup"><span data-stu-id="e49df-134">Support for [enum](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEnumTypeSample/ODataEnumTypeSample/), [containment](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/) and [singleton](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)</span></span>
- <span data-ttu-id="e49df-135">强制转换为基元类型的支持</span><span class="sxs-lookup"><span data-stu-id="e49df-135">Support cast for primitive types</span></span>
- [<span data-ttu-id="e49df-136">添加了 OData 函数的支持</span><span class="sxs-lookup"><span data-stu-id="e49df-136">Added OData function support</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataFunctionSample/)
- [<span data-ttu-id="e49df-137">支持的函数调用的参数的别名</span><span class="sxs-lookup"><span data-stu-id="e49df-137">Support parameter aliases for function calls</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataFunctionSample/)
- [<span data-ttu-id="e49df-138">在模型中支持 camel 大小写的命名约定</span><span class="sxs-lookup"><span data-stu-id="e49df-138">Support camel case naming convention in model</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataCamelCaseSample/)
- <span data-ttu-id="e49df-139">对在 $filter cast() 的支持</span><span class="sxs-lookup"><span data-stu-id="e49df-139">Support for cast() in $filter</span></span>
- <span data-ttu-id="e49df-140">打开的复杂类型的支持</span><span class="sxs-lookup"><span data-stu-id="e49df-140">Support for open complex type</span></span>
- <span data-ttu-id="e49df-141">删除的 EntitySetController 和 AsyncEntitySetController</span><span class="sxs-lookup"><span data-stu-id="e49df-141">Removed EntitySetController and AsyncEntitySetController</span></span>
- [<span data-ttu-id="e49df-142">更改到 $ref $link</span><span class="sxs-lookup"><span data-stu-id="e49df-142">Changed $link to $ref</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataServiceSample/)
- [<span data-ttu-id="e49df-143">添加的属性路由支持</span><span class="sxs-lookup"><span data-stu-id="e49df-143">Added Attribute routing support</span></span>](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataAttributeRoutingSample/)
- <span data-ttu-id="e49df-144">使用 OData 核心库 6.4.0</span><span class="sxs-lookup"><span data-stu-id="e49df-144">Uses OData Core Libraries 6.4.0</span></span>

<a id="ARI"></a>
### <a name="attribute-routing-improvements"></a><span data-ttu-id="e49df-145">属性路由改进</span><span class="sxs-lookup"><span data-stu-id="e49df-145">Attribute Routing Improvements</span></span>

<span data-ttu-id="e49df-146">现在的属性路由提供调用 IDirectRouteProvider，允许完全控制属性路由如何发现和配置一个扩展点。</span><span class="sxs-lookup"><span data-stu-id="e49df-146">Attribute Routing now provides an extensibility point called IDirectRouteProvider, which allows full control over how attribute routes are discovered and configured.</span></span> <span data-ttu-id="e49df-147">IDirectRouteProvider 负责提供的操作和以及关联的路由信息以指定哪些路由配置所需的这些操作完全的控制器的列表。</span><span class="sxs-lookup"><span data-stu-id="e49df-147">An IDirectRouteProvider is responsible for providing a list of actions and controllers along with associated route information to specify exactly what routing configuration is desired for those actions.</span></span> <span data-ttu-id="e49df-148">调用 MapAttributes/MapHttpAttributeRoutes 时，可能指定 IDirectRouteProvider 实现。</span><span class="sxs-lookup"><span data-stu-id="e49df-148">An IDirectRouteProvider implementation may be specified when calling MapAttributes/MapHttpAttributeRoutes.</span></span>

<span data-ttu-id="e49df-149">自定义 IDirectRouteProvider 是最简单的扩展了默认实现，DefaultDirectRouteProvider。</span><span class="sxs-lookup"><span data-stu-id="e49df-149">Customizing IDirectRouteProvider will be easiest by extending our default implementation, DefaultDirectRouteProvider.</span></span> <span data-ttu-id="e49df-150">此类提供单独可重写虚拟方法，若要更改用于发现属性、 创建的路由项和发现的路由前缀和区域前缀的逻辑。</span><span class="sxs-lookup"><span data-stu-id="e49df-150">This class provides separate overridable virtual methods to change the logic for discovering attributes, creating route entries, and discovering route prefix and area prefix.</span></span>

<span data-ttu-id="e49df-151">以下是一些示例上你可以使用此新的扩展点执行的操作：</span><span class="sxs-lookup"><span data-stu-id="e49df-151">Following are some examples on what you could do with this new extensibility point:</span></span>

1. <span data-ttu-id="e49df-152">支持路由属性的继承</span><span class="sxs-lookup"><span data-stu-id="e49df-152">Support inheritance of Route attributes</span></span>

    <span data-ttu-id="e49df-153">示例:</span><span class="sxs-lookup"><span data-stu-id="e49df-153">Example:</span></span>

    <span data-ttu-id="e49df-154">此处 like"/ 10/api/值"的请求已成功将返回"成功： 10"</span><span class="sxs-lookup"><span data-stu-id="e49df-154">Here a request like "/api/values/10" would successfully return "Success:10"</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-web-api-22/samples/sample2.cs)]
2. <span data-ttu-id="e49df-155">按照您喜欢的某些约定提供默认路由名称的属性路由。</span><span class="sxs-lookup"><span data-stu-id="e49df-155">Provide a default route name for your attribute routes by following some convention you like.</span></span> <span data-ttu-id="e49df-156">默认情况下，属性路由不会自动创建的属性路由的名称。</span><span class="sxs-lookup"><span data-stu-id="e49df-156">By default, attribute routing doesn't automatically create names for attribute routes.</span></span>
3. <span data-ttu-id="e49df-157">路由表中的它们结束之前，请修改在一个中心位置的属性路由的路由模板。</span><span class="sxs-lookup"><span data-stu-id="e49df-157">Modify attribute routes' route template at one central place before they end up in the route table.</span></span>

<a id="phone"></a>
### <a name="web-api-client-support-for-windows-phone-81"></a><span data-ttu-id="e49df-158">Web API Client Support for Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="e49df-158">Web API Client Support for Windows Phone 8.1</span></span>

<span data-ttu-id="e49df-159">现在可以使用 Web API 客户端 NuGet 包来实现你的 Web API 客户端逻辑，如果目标 Windows Phone 8.1 或通用应用程序中。</span><span class="sxs-lookup"><span data-stu-id="e49df-159">You can now use the Web API Client NuGet package to implement your Web API client logic when targeting Windows Phone 8.1 or from within a Universal App.</span></span>

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="e49df-160">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="e49df-160">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="e49df-161">本部分介绍已知的问题和 ASP.NET Web API 2.2 中的重大更改。</span><span class="sxs-lookup"><span data-stu-id="e49df-161">This section describes known issues and breaking changes in the ASP.NET Web API 2.2.</span></span>

### <a name="odata-v4"></a><span data-ttu-id="e49df-162">OData v4</span><span class="sxs-lookup"><span data-stu-id="e49df-162">OData v4</span></span>

#### <a name="model-builder"></a><span data-ttu-id="e49df-163">模型生成器</span><span class="sxs-lookup"><span data-stu-id="e49df-163">Model builder</span></span>

<span data-ttu-id="e49df-164">问题： 重载的函数可能不会公开为 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="e49df-164">Issue: Overloaded Functions could not be exposed as FunctionImport</span></span>

<span data-ttu-id="e49df-165">如果有两个重载的函数，并且它们还 FunctionImport 然后请求 ~/GetAllConventionCustomers(CustomerName={customerName}) 导致 System.InvalidOperationException 如下所示。</span><span class="sxs-lookup"><span data-stu-id="e49df-165">If there are 2 overloaded functions and they are also FunctionImport as shown below then requesting ~/GetAllConventionCustomers(CustomerName={customerName}) results in System.InvalidOperationException.</span></span>

[!code-xml[Main](whats-new-in-aspnet-web-api-22/samples/sample3.xml)]

<span data-ttu-id="e49df-166">解决方法： 此问题的解决方法是作为 FunctionImports 添加这两个函数重载。</span><span class="sxs-lookup"><span data-stu-id="e49df-166">Workaround: The workaround for this issue is to add both the function overloads as FunctionImports.</span></span>

#### <a name="odata-routing"></a><span data-ttu-id="e49df-167">OData 路由</span><span class="sxs-lookup"><span data-stu-id="e49df-167">OData Routing</span></span>

<span data-ttu-id="e49df-168">包括 URL 的字符串文本编码斜杠 (%2f) 和 backslash(%5C) 导致 404 错误时的 OData 资源路径中使用它们。</span><span class="sxs-lookup"><span data-stu-id="e49df-168">String literals that include the URL encoded slash (%2F), and backslash(%5C) cause a 404 error when they are used in the OData resource paths.</span></span>

<span data-ttu-id="e49df-169">例如，字符串文本可以用作 OData 资源路径中的函数的参数或实体集的密钥值。</span><span class="sxs-lookup"><span data-stu-id="e49df-169">For example, string literals can be used in the OData resource paths as parameters of functions or key values of entity sets.</span></span>

<span data-ttu-id="e49df-170">/Employees/Total.GetCount(Name='Name%2F')</span><span class="sxs-lookup"><span data-stu-id="e49df-170">/Employees/Total.GetCount(Name='Name%2F')</span></span>

<span data-ttu-id="e49df-171">/Employees('Name%5C')</span><span class="sxs-lookup"><span data-stu-id="e49df-171">/Employees('Name%5C')</span></span>

<span data-ttu-id="e49df-172">如果服务收到此类请求主机将取消转义那些转义序列，然后再将它们传递到 Web API 运行时。</span><span class="sxs-lookup"><span data-stu-id="e49df-172">When services receive such requests the hosts will un-escape those escape sequences before passing them to the Web API runtime.</span></span> <span data-ttu-id="e49df-173">这样可防止攻击，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e49df-173">This protects against attacks like the following:</span></span>  
  
 <span data-ttu-id="e49df-174">http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:</span><span class="sxs-lookup"><span data-stu-id="e49df-174">http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:</span></span>

<span data-ttu-id="e49df-175">这会导致 Web API OData 堆栈，以将返回 404 错误 （未找到）。</span><span class="sxs-lookup"><span data-stu-id="e49df-175">This causes the Web API OData stack to return a 404 error (Not Found).</span></span> <span data-ttu-id="e49df-176">若要防止出现此错误，你的客户端应使用斜杠 （%252f) 的双重转义序列和反斜杠 （%255 C)。</span><span class="sxs-lookup"><span data-stu-id="e49df-176">To prevent this error, your client should use the double escape sequences for slash (%252F) and backslash (%255C).</span></span> <span data-ttu-id="e49df-177">这不会发生的查询字符串，例如，/Employees？ $filter = Name eq '名称 %2f</span><span class="sxs-lookup"><span data-stu-id="e49df-177">This does not happen for query strings such as /Employees?$filter=Name eq 'Name%2F'</span></span>

<span data-ttu-id="e49df-178">**请注意取消转义的斜杠 （'/') 和反斜杠 （'） 不是合法中的 OData 资源路径字符串文字。斜杠应显示仅为路径分隔符和反斜杠应根本不显示在 OData 资源路径中。（都在 OData 查询字符串的某些部分中可用。）**</span><span class="sxs-lookup"><span data-stu-id="e49df-178">**Note un-escaped slashes ('/') and backslashes ('') are not legal in OData resource path string literals. Slashes should appear only as path separators and backslashes should not appear in the OData resource path at all. (Both are usable in some portions of an OData query string.)**</span></span>

<span data-ttu-id="e49df-179">解决方法： 你无法重写 DefaultODataPathHandler 进行实际分析它们之前转义的斜杠和字符串文本中的反斜杠的分析方法。</span><span class="sxs-lookup"><span data-stu-id="e49df-179">Workaround: You could override the Parse method of DefaultODataPathHandler to escape the slash and backslash in string literals before actually parsing them.</span></span> <span data-ttu-id="e49df-180">你可以找到这种方法的示例。</span><span class="sxs-lookup"><span data-stu-id="e49df-180">You can find a sample of this approach here.</span></span>

### <a name="odata-v3"></a><span data-ttu-id="e49df-181">OData v3</span><span class="sxs-lookup"><span data-stu-id="e49df-181">OData v3</span></span>

#### <a name="queryable"></a><span data-ttu-id="e49df-182">[查询]</span><span class="sxs-lookup"><span data-stu-id="e49df-182">[Queryable]</span></span>

<span data-ttu-id="e49df-183">[Queryable] 属性已弃用。</span><span class="sxs-lookup"><span data-stu-id="e49df-183">The [Queryable] attribute is deprecated.</span></span> <span data-ttu-id="e49df-184">新的 OData v3 应用程序应使用**System.Web.Http.OData.EnableQueryAttribute**。</span><span class="sxs-lookup"><span data-stu-id="e49df-184">New OData v3 applications should use **System.Web.Http.OData.EnableQueryAttribute**.</span></span>

<span data-ttu-id="e49df-185">**ODataHttpConfigurationExtensions.EnableQuerySupport**扩展方法现在将添加**EnableQueryAttribute**到全局筛选器集合。</span><span class="sxs-lookup"><span data-stu-id="e49df-185">The **ODataHttpConfigurationExtensions.EnableQuerySupport** extension method now adds an **EnableQueryAttribute** to the global filter collection.</span></span> <span data-ttu-id="e49df-186">如果任何控制器有 **[Queryable]** 属性，调用`config.EnableQuerySupport()`将导致 **[Queryable]** 属性失败</span><span class="sxs-lookup"><span data-stu-id="e49df-186">If any controllers have the **[Queryable]** attribute, calling `config.EnableQuerySupport()` will cause the **[Queryable]** attribute to fail</span></span>

<span data-ttu-id="e49df-187">若要解决此问题的建议的方法是替换的所有实例**QueryableAttribute**与**System.Web.Http.OData.EnableQueryAttribute**。</span><span class="sxs-lookup"><span data-stu-id="e49df-187">The recommended way to resolve this issue is to replace all instances of **QueryableAttribute** with **System.Web.Http.OData.EnableQueryAttribute**.</span></span>

<span data-ttu-id="e49df-188">备用解决方法是使用你的 Web API 配置中的以下代码：</span><span class="sxs-lookup"><span data-stu-id="e49df-188">An alternative workaround is to use the following code in your Web API configuration:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-22/samples/sample4.cs)]

### <a name="attribute-routing"></a><span data-ttu-id="e49df-189">属性路由</span><span class="sxs-lookup"><span data-stu-id="e49df-189">Attribute Routing</span></span>

<span data-ttu-id="e49df-190">问题： 模型绑定的复杂类型也使用 FromUri 特性修饰的行为有所不同时使用的属性路由。</span><span class="sxs-lookup"><span data-stu-id="e49df-190">Issue: Model binding of complex type which is decorated with FromUri attribute behaves differently when using Attribute Routing.</span></span>

<span data-ttu-id="e49df-191">以下链接在跟踪问题，并且也有一种解决方法有关的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e49df-191">Following link is tracking the issue and also has details about a workaround.</span></span>  
[<span data-ttu-id="e49df-192">http://aspnetwebstack.codeplex.com/workitem/1944</span><span class="sxs-lookup"><span data-stu-id="e49df-192">http://aspnetwebstack.codeplex.com/workitem/1944</span></span>](http://aspnetwebstack.codeplex.com/workitem/1944)

<span data-ttu-id="e49df-193">问题： 到 5.2.0 与项目的基架 MVC/Web API 包导致 5.1.2 打包以一种是在项目中尚不存在</span><span class="sxs-lookup"><span data-stu-id="e49df-193">Issue: Scaffolding MVC/Web API into a project with 5.2.0 packages results in 5.1.2 packages for ones that don't already exist in the project</span></span>

<span data-ttu-id="e49df-194">有关 ASP.NET MVC 5.2 更新 NuGet 程序包不会更新 Visual Studio 工具，例如 ASP.NET 基架或 ASP.NET Web 应用程序项目模板。</span><span class="sxs-lookup"><span data-stu-id="e49df-194">Updating NuGet packages for ASP.NET MVC 5.2 does not update the Visual Studio tools such as ASP.NET scaffolding or the ASP.NET Web Application project template.</span></span> <span data-ttu-id="e49df-195">它们使用以前版本的 ASP.NET 运行时包 (例如 5.1.2 Update 2 中)。</span><span class="sxs-lookup"><span data-stu-id="e49df-195">They use the previous version of the ASP.NET runtime packages (e.g. 5.1.2 in Update 2).</span></span> <span data-ttu-id="e49df-196">因此，ASP.NET 基架将安装所需的包的以前版本 (例如 5.1.2 Update 2 中)，如果它们尚不存在在你项目中可用。</span><span class="sxs-lookup"><span data-stu-id="e49df-196">As a result, the ASP.NET scaffolding will install the previous version (e.g. 5.1.2 in Update 2) of the required packages, if they are not already available in your projects.</span></span> <span data-ttu-id="e49df-197">但是，在 Visual Studio 2013 RTM 或 Update 1 中的 ASP.NET 基架不会覆盖你的项目中的最新包。</span><span class="sxs-lookup"><span data-stu-id="e49df-197">However, the ASP.NET scaffolding in Visual Studio 2013 RTM or Update 1 does not overwrite the latest packages in your projects.</span></span> <span data-ttu-id="e49df-198">如果您使用 ASP.NET Web API 2.2 或 ASP.NET MVC 5.2 到更新你的项目的包之后的基架，请确保 Web API 和 ASP.NET MVC 的版本都一致。</span><span class="sxs-lookup"><span data-stu-id="e49df-198">If you use ASP.NET scaffolding after updating the packages of your projects to Web API 2.2 or ASP.NET MVC 5.2, make sure the versions of Web API and ASP.NET MVC are consistent.</span></span>

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a><span data-ttu-id="e49df-199">Bug 修复和细微的功能更新</span><span class="sxs-lookup"><span data-stu-id="e49df-199">Bug Fixes and Minor Feature Updates</span></span>

<span data-ttu-id="e49df-200">此版本还包括几个 bug 修复和细微的功能更新。</span><span class="sxs-lookup"><span data-stu-id="e49df-200">This release also includes several bug fixes and minor feature updates.</span></span> <span data-ttu-id="e49df-201">您可以找到完整的列表：</span><span class="sxs-lookup"><span data-stu-id="e49df-201">You can find the complete list here:</span></span>

- [<span data-ttu-id="e49df-202">5.2 包</span><span class="sxs-lookup"><span data-stu-id="e49df-202">5.2 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.2%20RC|v5.2%20RTM&assignedTo=All&component=Web%20API|Web%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="odata521"></a>
## <a name="microsoftaspnetodata-521"></a><span data-ttu-id="e49df-203">Microsoft.AspNet.OData 5.2.1 章</span><span class="sxs-lookup"><span data-stu-id="e49df-203">Microsoft.AspNet.OData 5.2.1</span></span>

<span data-ttu-id="e49df-204">Microsoft.AspNet.OData 5.2.1 章程序包包含 NuGet 依赖项更新，但是没有 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="e49df-204">The Microsoft.AspNet.OData 5.2.1 package contains NuGet dependency updates but no bug fixes.</span></span> <span data-ttu-id="e49df-205">利用此更新，是不再严格的依赖项的 Microsoft.OData.Core 6.4.0，但是其中一个可以升级到 6.4.0 和 7.0.0 之间的任何版本。</span><span class="sxs-lookup"><span data-stu-id="e49df-205">With this update, there is no longer a strict dependency on Microsoft.OData.Core 6.4.0, but one can upgrade to any version between 6.4.0 and 7.0.0.</span></span>

<a id="522RC"></a>
## <a name="microsoftaspnetwebapi-522"></a><span data-ttu-id="e49df-206">Microsoft.AspNet.WebAPI 5.2.2</span><span class="sxs-lookup"><span data-stu-id="e49df-206">Microsoft.AspNet.WebAPI 5.2.2</span></span>

<span data-ttu-id="e49df-207">在此版本中，我们已创建依赖关系更改为`Json.Net 6.0.4`。</span><span class="sxs-lookup"><span data-stu-id="e49df-207">In this release we have made a dependency change for `Json.Net 6.0.4`.</span></span> <span data-ttu-id="e49df-208">有关详细信息中的此版本的新增`Json.NET`，请参阅[Json.NET 6.0 版本 4-JSON 合并，依赖关系注入](http://james.newtonking.com/archive/2014/08/04/json-net-6-0-release-4-json-merge-dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="e49df-208">For more information on what is new in this release of `Json.NET`, see [Json.NET 6.0 Release 4 - JSON Merge, Dependency Injection](http://james.newtonking.com/archive/2014/08/04/json-net-6-0-release-4-json-merge-dependency-injection).</span></span> <span data-ttu-id="e49df-209">此版本不具有任何其他新功能或 bug 修复的 Web API。</span><span class="sxs-lookup"><span data-stu-id="e49df-209">This release doesn't have any other new features or bug fixes in Web API.</span></span> <span data-ttu-id="e49df-210">随后，我们已更新我们拥有取决于此新版本的 Web API 的所有其他从属包。</span><span class="sxs-lookup"><span data-stu-id="e49df-210">We have subsequently updated all other dependent packages we own to depend on this new version of Web API.</span></span>

<a id="523"></a>
## <a name="microsoftaspnetwebapi-523-beta"></a><span data-ttu-id="e49df-211">Microsoft.AspNet.WebAPI 5.2.3 Beta</span><span class="sxs-lookup"><span data-stu-id="e49df-211">Microsoft.AspNet.WebAPI 5.2.3 Beta</span></span>

<span data-ttu-id="e49df-212">你可以阅读有关版本[此处](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e49df-212">You can read about the release [here](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx).</span></span> <span data-ttu-id="e49df-213">此版本包含仅 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="e49df-213">This release contains only bug fixes.</span></span> <span data-ttu-id="e49df-214">你可以使用[此查询](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=Web%20API&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed)若要查看此版本中修复的问题的列表。</span><span class="sxs-lookup"><span data-stu-id="e49df-214">You can use [this query](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=Web%20API&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) to see the list of issues fixed in this release.</span></span>
