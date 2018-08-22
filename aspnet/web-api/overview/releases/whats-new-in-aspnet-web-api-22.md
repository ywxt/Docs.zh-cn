---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-22
title: 什么是 ASP.NET Web API 2.2 中的新增功能 |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 12/25/2014
ms.assetid: 99c59ae4-167e-4f66-a6cd-d3f1098c4e4a
msc.legacyurl: /web-api/overview/releases/whats-new-in-aspnet-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: ef08a3bb397ff54795ca6c70cdcc35206cf122f5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825074"
---
<a name="whats-new-in-aspnet-web-api-22"></a><span data-ttu-id="33b93-102">什么是 ASP.NET Web API 2.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="33b93-102">What's New in ASP.NET Web API 2.2</span></span>
====================
<span data-ttu-id="33b93-103">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="33b93-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="33b93-104">本主题介绍什么是 ASP.NET Web API 2.2 的新增功能。</span><span class="sxs-lookup"><span data-stu-id="33b93-104">This topic describes what's new for ASP.NET Web API 2.2.</span></span>

- [<span data-ttu-id="33b93-105">下载</span><span class="sxs-lookup"><span data-stu-id="33b93-105">Download</span></span>](#download)
- [<span data-ttu-id="33b93-106">文档</span><span class="sxs-lookup"><span data-stu-id="33b93-106">Documentation</span></span>](#documentation)
- [<span data-ttu-id="33b93-107">ASP.NET Web API 2.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="33b93-107">New Features in ASP.NET Web API 2.2</span></span>](#newf)

    - [<span data-ttu-id="33b93-108">OData v4</span><span class="sxs-lookup"><span data-stu-id="33b93-108">OData v4</span></span>](#OData)
    - [<span data-ttu-id="33b93-109">属性路由改进</span><span class="sxs-lookup"><span data-stu-id="33b93-109">Attribute Routing Improvements</span></span>](#ARI)
    - [<span data-ttu-id="33b93-110">Web API 客户端支持 Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="33b93-110">Web API Client support for Windows Phone 8.1</span></span>](#phone)
- [<span data-ttu-id="33b93-111">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="33b93-111">Known Issues and Breaking Changes</span></span>](#known-issues)
- [<span data-ttu-id="33b93-112">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="33b93-112">Bug Fixes</span></span>](#bug-fixes)
- [<span data-ttu-id="33b93-113">Microsoft.AspNet.OData 5.2.1 章</span><span class="sxs-lookup"><span data-stu-id="33b93-113">Microsoft.AspNet.OData 5.2.1</span></span>](#odata521)
- [<span data-ttu-id="33b93-114">Microsoft.AspNet.WebAPI 5.2.2</span><span class="sxs-lookup"><span data-stu-id="33b93-114">Microsoft.AspNet.WebAPI 5.2.2</span></span>](#522RC)
- [<span data-ttu-id="33b93-115">Microsoft.AspNet.WebAPI 5.2.3 Beta</span><span class="sxs-lookup"><span data-stu-id="33b93-115">Microsoft.AspNet.WebAPI 5.2.3 Beta</span></span>](#523)

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="33b93-116">下载</span><span class="sxs-lookup"><span data-stu-id="33b93-116">Download</span></span>

<span data-ttu-id="33b93-117">运行时功能将发布为 NuGet 库中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="33b93-117">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="33b93-118">所有运行时程序包遵循[语义化版本控制](http://semver.org/)规范。</span><span class="sxs-lookup"><span data-stu-id="33b93-118">All the runtime packages follow the [Semantic Versioning](http://semver.org/) specification.</span></span> <span data-ttu-id="33b93-119">最新的 ASP.NET Web API 2.2 包具有以下版本:"5.2.0"。</span><span class="sxs-lookup"><span data-stu-id="33b93-119">The latest ASP.NET Web API 2.2 package has the following version: "5.2.0".</span></span> <span data-ttu-id="33b93-120">可以安装或更新通过这些程序包[NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/)。</span><span class="sxs-lookup"><span data-stu-id="33b93-120">You can install or update these packages through [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/).</span></span> <span data-ttu-id="33b93-121">此版本还包括在 NuGet 上的相应本地化的包。</span><span class="sxs-lookup"><span data-stu-id="33b93-121">The release also includes corresponding localized packages on NuGet.</span></span>

<span data-ttu-id="33b93-122">可以安装或使用 NuGet 包管理器控制台更新为已发布的 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="33b93-122">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-22/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="33b93-123">文档</span><span class="sxs-lookup"><span data-stu-id="33b93-123">Documentation</span></span>

<span data-ttu-id="33b93-124">教程和有关 ASP.NET Web API 2.2 的其他信息是可通过 ASP.NET 网站 ([https://www.asp.net/web-api](../../index.md))。</span><span class="sxs-lookup"><span data-stu-id="33b93-124">Tutorials and other information about ASP.NET Web API 2.2 are available from the ASP.NET web site ([https://www.asp.net/web-api](../../index.md)).</span></span>

<a id="newf"></a>
## <a name="new-features-in-aspnet-web-api-22"></a><span data-ttu-id="33b93-125">ASP.NET Web API 2.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="33b93-125">New Features in ASP.NET Web API 2.2</span></span>

<a id="OData"></a>
### <a name="odata-v4"></a><span data-ttu-id="33b93-126">OData v4</span><span class="sxs-lookup"><span data-stu-id="33b93-126">OData v4</span></span>

<span data-ttu-id="33b93-127">此版本添加了对 OData v4 协议的支持。</span><span class="sxs-lookup"><span data-stu-id="33b93-127">This release adds support for the OData v4 protocol.</span></span> <span data-ttu-id="33b93-128">有关详细信息，请参阅[Web API OData v4 文档。](../odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="33b93-128">For more information, see the [Web API OData v4 documentation.](../odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint.md)</span></span>

<span data-ttu-id="33b93-129">下面是一些主要功能和更改的 OData v4:</span><span class="sxs-lookup"><span data-stu-id="33b93-129">Here are some of the key features and changes for OData v4:</span></span>

- [<span data-ttu-id="33b93-130">支持的 OData 模型中的别名属性</span><span class="sxs-lookup"><span data-stu-id="33b93-130">Support for aliasing properties in OData model</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataModelAliasingSample/)
- [<span data-ttu-id="33b93-131">支持 ComplexTypeAttribute、 AssociationAttribute、 TimesTampAttribute 和 ConcurrencyCheckAttribute ODataConventionModelBuilder 中</span><span class="sxs-lookup"><span data-stu-id="33b93-131">Support for ComplexTypeAttribute, AssociationAttribute, TimesTampAttribute and ConcurrencyCheckAttribute in ODataConventionModelBuilder</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEtagSample/)
- [<span data-ttu-id="33b93-132">提供功能来提供友好标题的操作</span><span class="sxs-lookup"><span data-stu-id="33b93-132">Provide ability to supply friendly Title for actions</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataActionsSample/)
- <span data-ttu-id="33b93-133">将与 ODL UriParser 集成</span><span class="sxs-lookup"><span data-stu-id="33b93-133">Integrate with ODL UriParser</span></span>
- <span data-ttu-id="33b93-134">为支持[enum](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEnumTypeSample/ODataEnumTypeSample/)，[包容](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)和[单一实例](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)</span><span class="sxs-lookup"><span data-stu-id="33b93-134">Support for [enum](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEnumTypeSample/ODataEnumTypeSample/), [containment](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/) and [singleton](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)</span></span>
- <span data-ttu-id="33b93-135">强制转换为基元类型的支持</span><span class="sxs-lookup"><span data-stu-id="33b93-135">Support cast for primitive types</span></span>
- [<span data-ttu-id="33b93-136">添加了的 OData 函数的支持</span><span class="sxs-lookup"><span data-stu-id="33b93-136">Added OData function support</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataFunctionSample/)
- [<span data-ttu-id="33b93-137">支持的函数调用的参数的别名</span><span class="sxs-lookup"><span data-stu-id="33b93-137">Support parameter aliases for function calls</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataFunctionSample/)
- [<span data-ttu-id="33b93-138">在模型中支持 camel 大小写的命名约定</span><span class="sxs-lookup"><span data-stu-id="33b93-138">Support camel case naming convention in model</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataCamelCaseSample/)
- <span data-ttu-id="33b93-139">在 $ $filter 中的 cast （） 的支持</span><span class="sxs-lookup"><span data-stu-id="33b93-139">Support for cast() in $filter</span></span>
- <span data-ttu-id="33b93-140">对打开的复杂类型的支持</span><span class="sxs-lookup"><span data-stu-id="33b93-140">Support for open complex type</span></span>
- <span data-ttu-id="33b93-141">已删除的 EntitySetController 和 AsyncEntitySetController</span><span class="sxs-lookup"><span data-stu-id="33b93-141">Removed EntitySetController and AsyncEntitySetController</span></span>
- [<span data-ttu-id="33b93-142">已更改为 $ref $link</span><span class="sxs-lookup"><span data-stu-id="33b93-142">Changed $link to $ref</span></span>](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataServiceSample/)
- [<span data-ttu-id="33b93-143">添加了的属性路由支持</span><span class="sxs-lookup"><span data-stu-id="33b93-143">Added Attribute routing support</span></span>](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataAttributeRoutingSample/)
- <span data-ttu-id="33b93-144">使用 OData 核心库 6.4.0</span><span class="sxs-lookup"><span data-stu-id="33b93-144">Uses OData Core Libraries 6.4.0</span></span>

<a id="ARI"></a>
### <a name="attribute-routing-improvements"></a><span data-ttu-id="33b93-145">属性路由改进</span><span class="sxs-lookup"><span data-stu-id="33b93-145">Attribute Routing Improvements</span></span>

<span data-ttu-id="33b93-146">属性路由现在提供了一个名为 IDirectRouteProvider，可完全控制如何发现和配置属性路由的扩展点。</span><span class="sxs-lookup"><span data-stu-id="33b93-146">Attribute Routing now provides an extensibility point called IDirectRouteProvider, which allows full control over how attribute routes are discovered and configured.</span></span> <span data-ttu-id="33b93-147">IDirectRouteProvider 负责提供的操作和控制器以及关联的路由信息来指定这些操作需要何种路由配置的情况完全列表。</span><span class="sxs-lookup"><span data-stu-id="33b93-147">An IDirectRouteProvider is responsible for providing a list of actions and controllers along with associated route information to specify exactly what routing configuration is desired for those actions.</span></span> <span data-ttu-id="33b93-148">调用 MapAttributes/MapHttpAttributeRoutes 时，可能会指定 IDirectRouteProvider 实现。</span><span class="sxs-lookup"><span data-stu-id="33b93-148">An IDirectRouteProvider implementation may be specified when calling MapAttributes/MapHttpAttributeRoutes.</span></span>

<span data-ttu-id="33b93-149">自定义 IDirectRouteProvider 将是最简单通过扩展我们的默认实现，DefaultDirectRouteProvider。</span><span class="sxs-lookup"><span data-stu-id="33b93-149">Customizing IDirectRouteProvider will be easiest by extending our default implementation, DefaultDirectRouteProvider.</span></span> <span data-ttu-id="33b93-150">此类提供了单独可重写虚拟方法，以更改用于发现属性、 创建路由项，以及发现路由前缀和区域前缀的逻辑。</span><span class="sxs-lookup"><span data-stu-id="33b93-150">This class provides separate overridable virtual methods to change the logic for discovering attributes, creating route entries, and discovering route prefix and area prefix.</span></span>

<span data-ttu-id="33b93-151">以下是有关使用此新的扩展点可以做些什么的一些示例：</span><span class="sxs-lookup"><span data-stu-id="33b93-151">Following are some examples on what you could do with this new extensibility point:</span></span>

1. <span data-ttu-id="33b93-152">支持路由属性的继承</span><span class="sxs-lookup"><span data-stu-id="33b93-152">Support inheritance of Route attributes</span></span>

    <span data-ttu-id="33b93-153">示例:</span><span class="sxs-lookup"><span data-stu-id="33b93-153">Example:</span></span>

    <span data-ttu-id="33b93-154">此处 like"/ api/值/10"的请求已成功将返回"成功： 10"</span><span class="sxs-lookup"><span data-stu-id="33b93-154">Here a request like "/api/values/10" would successfully return "Success:10"</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-web-api-22/samples/sample2.cs)]
2. <span data-ttu-id="33b93-155">按照您喜欢某些约定提供属性路由的默认路由名称。</span><span class="sxs-lookup"><span data-stu-id="33b93-155">Provide a default route name for your attribute routes by following some convention you like.</span></span> <span data-ttu-id="33b93-156">默认情况下，属性路由不会自动创建属性路由的名称。</span><span class="sxs-lookup"><span data-stu-id="33b93-156">By default, attribute routing doesn't automatically create names for attribute routes.</span></span>
3. <span data-ttu-id="33b93-157">修改属性路由的路由模板在一个中心位置，然后最终路由表中。</span><span class="sxs-lookup"><span data-stu-id="33b93-157">Modify attribute routes' route template at one central place before they end up in the route table.</span></span>

<a id="phone"></a>
### <a name="web-api-client-support-for-windows-phone-81"></a><span data-ttu-id="33b93-158">Windows Phone 8.1 的 web API 客户端支持</span><span class="sxs-lookup"><span data-stu-id="33b93-158">Web API Client Support for Windows Phone 8.1</span></span>

<span data-ttu-id="33b93-159">现在可以使用 Web API 客户端 NuGet 包以实现 Web API 客户端逻辑，面向 Windows Phone 8.1 时或从通用应用中。</span><span class="sxs-lookup"><span data-stu-id="33b93-159">You can now use the Web API Client NuGet package to implement your Web API client logic when targeting Windows Phone 8.1 or from within a Universal App.</span></span>

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="33b93-160">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="33b93-160">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="33b93-161">本部分介绍的已知的问题和 ASP.NET Web API 2.2 中的重大更改。</span><span class="sxs-lookup"><span data-stu-id="33b93-161">This section describes known issues and breaking changes in the ASP.NET Web API 2.2.</span></span>

### <a name="odata-v4"></a><span data-ttu-id="33b93-162">OData v4</span><span class="sxs-lookup"><span data-stu-id="33b93-162">OData v4</span></span>

#### <a name="model-builder"></a><span data-ttu-id="33b93-163">模型生成器</span><span class="sxs-lookup"><span data-stu-id="33b93-163">Model builder</span></span>

<span data-ttu-id="33b93-164">问题： 重载的函数可能不会公开为 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="33b93-164">Issue: Overloaded Functions could not be exposed as FunctionImport</span></span>

<span data-ttu-id="33b93-165">如果有两个重载的函数，也要 FunctionImport 然后请求中 System.InvalidOperationException ~/GetAllConventionCustomers(CustomerName={customerName}) 结果如下所示。</span><span class="sxs-lookup"><span data-stu-id="33b93-165">If there are 2 overloaded functions and they are also FunctionImport as shown below then requesting ~/GetAllConventionCustomers(CustomerName={customerName}) results in System.InvalidOperationException.</span></span>

[!code-xml[Main](whats-new-in-aspnet-web-api-22/samples/sample3.xml)]

<span data-ttu-id="33b93-166">解决方法： 此问题的解决方法是将这两个函数重载添加 FunctionImports 为。</span><span class="sxs-lookup"><span data-stu-id="33b93-166">Workaround: The workaround for this issue is to add both the function overloads as FunctionImports.</span></span>

#### <a name="odata-routing"></a><span data-ttu-id="33b93-167">OData 路由</span><span class="sxs-lookup"><span data-stu-id="33b93-167">OData Routing</span></span>

<span data-ttu-id="33b93-168">包含 URL 的字符串文本编码斜杠 (%2f) 和 backslash(%5C) OData 资源路径中使用它们时，会导致 404 错误。</span><span class="sxs-lookup"><span data-stu-id="33b93-168">String literals that include the URL encoded slash (%2F), and backslash(%5C) cause a 404 error when they are used in the OData resource paths.</span></span>

<span data-ttu-id="33b93-169">例如，字符串文本可以用作 OData 资源路径中的函数的参数或实体集的键值。</span><span class="sxs-lookup"><span data-stu-id="33b93-169">For example, string literals can be used in the OData resource paths as parameters of functions or key values of entity sets.</span></span>

<span data-ttu-id="33b93-170">/Employees/Total.GetCount(Name='Name%2F')</span><span class="sxs-lookup"><span data-stu-id="33b93-170">/Employees/Total.GetCount(Name='Name%2F')</span></span>

<span data-ttu-id="33b93-171">/Employees('Name%5C')</span><span class="sxs-lookup"><span data-stu-id="33b93-171">/Employees('Name%5C')</span></span>

<span data-ttu-id="33b93-172">当服务收到此类请求的主机将取消转义时那些转义序列，然后再将它们传递到 Web API 运行时。</span><span class="sxs-lookup"><span data-stu-id="33b93-172">When services receive such requests the hosts will un-escape those escape sequences before passing them to the Web API runtime.</span></span> <span data-ttu-id="33b93-173">这可防止攻击，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33b93-173">This protects against attacks like the following:</span></span>  
  
`http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:`

<span data-ttu-id="33b93-174">这会导致要返回 404 错误 （找不到） 的 Web API OData 堆栈。</span><span class="sxs-lookup"><span data-stu-id="33b93-174">This causes the Web API OData stack to return a 404 error (Not Found).</span></span> <span data-ttu-id="33b93-175">若要防止出现此错误，您的客户端应使用双转义序列的反斜杠 （%252f) 和反斜杠 （%255 C)。</span><span class="sxs-lookup"><span data-stu-id="33b93-175">To prevent this error, your client should use the double escape sequences for slash (%252F) and backslash (%255C).</span></span> <span data-ttu-id="33b93-176">这不会针对查询字符串，如 /Employees？ $filter = 名称 eq '名称 %2f</span><span class="sxs-lookup"><span data-stu-id="33b93-176">This does not happen for query strings such as /Employees?$filter=Name eq 'Name%2F'</span></span>

<span data-ttu-id="33b93-177">**请注意取消转义的斜杠 （'/') 和反斜杠 （"） 不能使用 OData 资源路径的字符串文字。应只作为路径分隔符出现斜杠和反斜杠不应出现在 OData 资源路径根本。（均可在 OData 查询字符串的某些部分中使用。）**</span><span class="sxs-lookup"><span data-stu-id="33b93-177">**Note un-escaped slashes ('/') and backslashes ('') are not legal in OData resource path string literals. Slashes should appear only as path separators and backslashes should not appear in the OData resource path at all. (Both are usable in some portions of an OData query string.)**</span></span>

<span data-ttu-id="33b93-178">解决方法： 您可以重写 DefaultODataPathHandler 进行实际解析它们之前转义的反斜杠和字符串文本中的反斜杠的分析方法。</span><span class="sxs-lookup"><span data-stu-id="33b93-178">Workaround: You could override the Parse method of DefaultODataPathHandler to escape the slash and backslash in string literals before actually parsing them.</span></span> <span data-ttu-id="33b93-179">您可以找到这种方法的示例。</span><span class="sxs-lookup"><span data-stu-id="33b93-179">You can find a sample of this approach here.</span></span>

### <a name="odata-v3"></a><span data-ttu-id="33b93-180">OData v3</span><span class="sxs-lookup"><span data-stu-id="33b93-180">OData v3</span></span>

#### <a name="queryable"></a><span data-ttu-id="33b93-181">[查询]</span><span class="sxs-lookup"><span data-stu-id="33b93-181">[Queryable]</span></span>

<span data-ttu-id="33b93-182">不推荐使用 [Queryable] 属性。</span><span class="sxs-lookup"><span data-stu-id="33b93-182">The [Queryable] attribute is deprecated.</span></span> <span data-ttu-id="33b93-183">新的 OData v3 应用程序应使用**System.Web.Http.OData.EnableQueryAttribute**。</span><span class="sxs-lookup"><span data-stu-id="33b93-183">New OData v3 applications should use **System.Web.Http.OData.EnableQueryAttribute**.</span></span>

<span data-ttu-id="33b93-184">**ODataHttpConfigurationExtensions.EnableQuerySupport**扩展方法现在将添加**EnableQueryAttribute**到全局筛选器集合。</span><span class="sxs-lookup"><span data-stu-id="33b93-184">The **ODataHttpConfigurationExtensions.EnableQuerySupport** extension method now adds an **EnableQueryAttribute** to the global filter collection.</span></span> <span data-ttu-id="33b93-185">如果有任何控制器 **[Queryable]** 属性，则调用`config.EnableQuerySupport()`将导致 **[Queryable]** 属性失败</span><span class="sxs-lookup"><span data-stu-id="33b93-185">If any controllers have the **[Queryable]** attribute, calling `config.EnableQuerySupport()` will cause the **[Queryable]** attribute to fail</span></span>

<span data-ttu-id="33b93-186">若要解决此问题的建议的方法是替换的所有实例**QueryableAttribute**与**System.Web.Http.OData.EnableQueryAttribute**。</span><span class="sxs-lookup"><span data-stu-id="33b93-186">The recommended way to resolve this issue is to replace all instances of **QueryableAttribute** with **System.Web.Http.OData.EnableQueryAttribute**.</span></span>

<span data-ttu-id="33b93-187">备用解决方法是在 Web API 配置中使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="33b93-187">An alternative workaround is to use the following code in your Web API configuration:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-22/samples/sample4.cs)]

### <a name="attribute-routing"></a><span data-ttu-id="33b93-188">属性路由</span><span class="sxs-lookup"><span data-stu-id="33b93-188">Attribute Routing</span></span>

<span data-ttu-id="33b93-189">问题： 修饰 FromUri 属性的复杂类型的模型绑定时的行为以不同的方式使用属性路由。</span><span class="sxs-lookup"><span data-stu-id="33b93-189">Issue: Model binding of complex type which is decorated with FromUri attribute behaves differently when using Attribute Routing.</span></span>

<span data-ttu-id="33b93-190">以下链接跟踪此问题，还有一种解决方法有关的详细信息。</span><span class="sxs-lookup"><span data-stu-id="33b93-190">Following link is tracking the issue and also has details about a workaround.</span></span>  
[http://aspnetwebstack.codeplex.com/workitem/1944](http://aspnetwebstack.codeplex.com/workitem/1944)

<span data-ttu-id="33b93-191">问题： 基架 MVC/Web API 到具有 5.2.0 项目包导致 5.1.2 打包以一种是在项目中尚不存在</span><span class="sxs-lookup"><span data-stu-id="33b93-191">Issue: Scaffolding MVC/Web API into a project with 5.2.0 packages results in 5.1.2 packages for ones that don't already exist in the project</span></span>

<span data-ttu-id="33b93-192">有关 ASP.NET MVC 5.2 更新 NuGet 包不会更新 Visual Studio 工具，如 ASP.NET 基架或 ASP.NET Web 应用程序项目模板。</span><span class="sxs-lookup"><span data-stu-id="33b93-192">Updating NuGet packages for ASP.NET MVC 5.2 does not update the Visual Studio tools such as ASP.NET scaffolding or the ASP.NET Web Application project template.</span></span> <span data-ttu-id="33b93-193">它们使用以前版本的 ASP.NET 运行时包 (例如 5.1.2 Update 2 中)。</span><span class="sxs-lookup"><span data-stu-id="33b93-193">They use the previous version of the ASP.NET runtime packages (e.g. 5.1.2 in Update 2).</span></span> <span data-ttu-id="33b93-194">因此，ASP.NET 基架将安装以前版本 (例如 5.1.2 Update 2 中) 的所需的包，如果它们尚不在你项目中可用。</span><span class="sxs-lookup"><span data-stu-id="33b93-194">As a result, the ASP.NET scaffolding will install the previous version (e.g. 5.1.2 in Update 2) of the required packages, if they are not already available in your projects.</span></span> <span data-ttu-id="33b93-195">但是，在 Visual Studio 2013 RTM 或 Update 1 中的 ASP.NET 基架不会覆盖在项目中最新的包。</span><span class="sxs-lookup"><span data-stu-id="33b93-195">However, the ASP.NET scaffolding in Visual Studio 2013 RTM or Update 1 does not overwrite the latest packages in your projects.</span></span> <span data-ttu-id="33b93-196">如果您使用 ASP.NET 基架 Web API 2.2 或 ASP.NET MVC 5.2 更新你的项目的包后，请确保了一致的 Web API 和 ASP.NET MVC 版本。</span><span class="sxs-lookup"><span data-stu-id="33b93-196">If you use ASP.NET scaffolding after updating the packages of your projects to Web API 2.2 or ASP.NET MVC 5.2, make sure the versions of Web API and ASP.NET MVC are consistent.</span></span>

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a><span data-ttu-id="33b93-197">Bug 修复和细微的功能更新</span><span class="sxs-lookup"><span data-stu-id="33b93-197">Bug Fixes and Minor Feature Updates</span></span>

<span data-ttu-id="33b93-198">此版本还包括几个 bug 修复和细微的功能更新。</span><span class="sxs-lookup"><span data-stu-id="33b93-198">This release also includes several bug fixes and minor feature updates.</span></span> <span data-ttu-id="33b93-199">您可以找到完整的列表：</span><span class="sxs-lookup"><span data-stu-id="33b93-199">You can find the complete list here:</span></span>

- [<span data-ttu-id="33b93-200">5.2 包</span><span class="sxs-lookup"><span data-stu-id="33b93-200">5.2 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.2%20RC|v5.2%20RTM&assignedTo=All&component=Web%20API|Web%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="odata521"></a>
## <a name="microsoftaspnetodata-521"></a><span data-ttu-id="33b93-201">Microsoft.AspNet.OData 5.2.1 章</span><span class="sxs-lookup"><span data-stu-id="33b93-201">Microsoft.AspNet.OData 5.2.1</span></span>

<span data-ttu-id="33b93-202">Microsoft.AspNet.OData 5.2.1 章包中包含 NuGet 依赖项更新，但任何 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="33b93-202">The Microsoft.AspNet.OData 5.2.1 package contains NuGet dependency updates but no bug fixes.</span></span> <span data-ttu-id="33b93-203">利用此更新，不再严格的依赖项上 Microsoft.OData.Core 6.4.0，但其中一个可以升级到 6.4.0 和 7.0.0 之间的任何版本。</span><span class="sxs-lookup"><span data-stu-id="33b93-203">With this update, there is no longer a strict dependency on Microsoft.OData.Core 6.4.0, but one can upgrade to any version between 6.4.0 and 7.0.0.</span></span>

<a id="522RC"></a>
## <a name="microsoftaspnetwebapi-522"></a><span data-ttu-id="33b93-204">Microsoft.AspNet.WebAPI 5.2.2</span><span class="sxs-lookup"><span data-stu-id="33b93-204">Microsoft.AspNet.WebAPI 5.2.2</span></span>

<span data-ttu-id="33b93-205">在此版本中我们所做的更改的依赖关系`Json.Net 6.0.4`。</span><span class="sxs-lookup"><span data-stu-id="33b93-205">In this release we have made a dependency change for `Json.Net 6.0.4`.</span></span> <span data-ttu-id="33b93-206">有关详细信息的此版本中新增`Json.NET`，请参阅[Json.NET 6.0 第 4 版-JSON 合并、 依赖关系注入](http://james.newtonking.com/archive/2014/08/04/json-net-6-0-release-4-json-merge-dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="33b93-206">For more information on what is new in this release of `Json.NET`, see [Json.NET 6.0 Release 4 - JSON Merge, Dependency Injection](http://james.newtonking.com/archive/2014/08/04/json-net-6-0-release-4-json-merge-dependency-injection).</span></span> <span data-ttu-id="33b93-207">此版本不包含任何其他新功能或 bug 修复，Web API 中。</span><span class="sxs-lookup"><span data-stu-id="33b93-207">This release doesn't have any other new features or bug fixes in Web API.</span></span> <span data-ttu-id="33b93-208">我们随后更新了我们拥有依赖于此新版本的 Web API 的所有依赖包。</span><span class="sxs-lookup"><span data-stu-id="33b93-208">We have subsequently updated all other dependent packages we own to depend on this new version of Web API.</span></span>

<a id="523"></a>
## <a name="microsoftaspnetwebapi-523-beta"></a><span data-ttu-id="33b93-209">Microsoft.AspNet.WebAPI 5.2.3 Beta</span><span class="sxs-lookup"><span data-stu-id="33b93-209">Microsoft.AspNet.WebAPI 5.2.3 Beta</span></span>

<span data-ttu-id="33b93-210">你可以阅读发行[此处](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)。</span><span class="sxs-lookup"><span data-stu-id="33b93-210">You can read about the release [here](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx).</span></span> <span data-ttu-id="33b93-211">此版本包含仅 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="33b93-211">This release contains only bug fixes.</span></span> <span data-ttu-id="33b93-212">可以使用[此查询](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=Web%20API&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed)若要查看此版本中修复的问题的列表。</span><span class="sxs-lookup"><span data-stu-id="33b93-212">You can use [this query](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=Web%20API&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) to see the list of issues fixed in this release.</span></span>
