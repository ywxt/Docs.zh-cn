---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-odata-53
title: 什么是 ASP.NET Web API OData 5.3 中的新增功能 |Microsoft 文档
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/16/2014
ms.topic: article
ms.assetid: e39eaa25-83ff-41dc-869d-3818d59a88ae
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/releases/whats-new-in-aspnet-web-api-odata-53
msc.type: authoredcontent
ms.openlocfilehash: e918f86ebd813f31ad0c21566e617482fc7dd963
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26508106"
---
<a name="whats-new-in-aspnet-web-api-odata-53"></a><span data-ttu-id="1876e-102">什么是 ASP.NET Web API OData 5.3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="1876e-102">What's New in ASP.NET Web API OData 5.3</span></span>
====================
<span data-ttu-id="1876e-103">通过[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1876e-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="1876e-104">本主题介绍什么是用于 ASP.NET Web API OData 5.3 的新功能。</span><span class="sxs-lookup"><span data-stu-id="1876e-104">This topic describes what's new for ASP.NET Web API OData 5.3.</span></span>

- [<span data-ttu-id="1876e-105">下载</span><span class="sxs-lookup"><span data-stu-id="1876e-105">Download</span></span>](#download)
- [<span data-ttu-id="1876e-106">文档</span><span class="sxs-lookup"><span data-stu-id="1876e-106">Documentation</span></span>](#documentation)
- [<span data-ttu-id="1876e-107">OData 核心库</span><span class="sxs-lookup"><span data-stu-id="1876e-107">OData Core Libraries</span></span>](#corelib)
- [<span data-ttu-id="1876e-108">新功能</span><span class="sxs-lookup"><span data-stu-id="1876e-108">New Features</span></span>](#newf)
- [<span data-ttu-id="1876e-109">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="1876e-109">Known Issues and Breaking Changes</span></span>](#known-issues)
- [<span data-ttu-id="1876e-110">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="1876e-110">Bug Fixes</span></span>](#bug-fixes)
- [<span data-ttu-id="1876e-111">ASP.NET Web API OData 5.3.1</span><span class="sxs-lookup"><span data-stu-id="1876e-111">ASP.NET Web API OData 5.3.1</span></span>](#OD)

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="1876e-112">下载</span><span class="sxs-lookup"><span data-stu-id="1876e-112">Download</span></span>

<span data-ttu-id="1876e-113">运行时功能将发布为 NuGet 库上的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="1876e-113">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="1876e-114">你可以安装或使用 NuGet 程序包管理器控制台更新到已发布的 NuGet 程序包：</span><span class="sxs-lookup"><span data-stu-id="1876e-114">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="1876e-115">文档</span><span class="sxs-lookup"><span data-stu-id="1876e-115">Documentation</span></span>

<span data-ttu-id="1876e-116">您可找到教程和有关在 ASP.NET Web API OData 的其他文档[ASP.NET 网站](../odata-support-in-aspnet-web-api/index.md)。</span><span class="sxs-lookup"><span data-stu-id="1876e-116">You can find tutorials and other documentation about ASP.NET Web API OData at the [ASP.NET web site](../odata-support-in-aspnet-web-api/index.md).</span></span>

<a id="corelib"></a>
## <a name="odata-core-libraries"></a><span data-ttu-id="1876e-117">OData 核心库</span><span class="sxs-lookup"><span data-stu-id="1876e-117">OData Core Libraries</span></span>

<span data-ttu-id="1876e-118">对于 OData v4，Web API 现在使用 ODataLib 版本 6.5.0</span><span class="sxs-lookup"><span data-stu-id="1876e-118">For OData v4, Web API now uses ODataLib version 6.5.0</span></span>

<a id="newf"></a>
## <a name="new-features-in-aspnet-web-api-odata-53"></a><span data-ttu-id="1876e-119">ASP.NET 中的新增功能的 Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="1876e-119">New Features in ASP.NET Web API OData 5.3</span></span>

### <a name="support-for-levels-in-expand"></a><span data-ttu-id="1876e-120">支持在 $ $levels 展开</span><span class="sxs-lookup"><span data-stu-id="1876e-120">Support for $levels in $expand</span></span>

<span data-ttu-id="1876e-121">你可以使用 $levels 中 $ 选项展开查询的查询。</span><span class="sxs-lookup"><span data-stu-id="1876e-121">You can use the $levels query option in $expand queries.</span></span> <span data-ttu-id="1876e-122">例如: </span><span class="sxs-lookup"><span data-stu-id="1876e-122">For example:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample2.cmd)]

<span data-ttu-id="1876e-123">此查询等效于：</span><span class="sxs-lookup"><span data-stu-id="1876e-123">This query is equivalent to:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample3.cmd)]

<a id="open-entity-types"></a>
### <a name="support-for-open-entity-types"></a><span data-ttu-id="1876e-124">打开实体类型的支持</span><span class="sxs-lookup"><span data-stu-id="1876e-124">Support for Open Entity Types</span></span>

<span data-ttu-id="1876e-125">*打开键入*是 stuctured 类型包含动态属性，除了在类型定义中声明的任何属性。</span><span class="sxs-lookup"><span data-stu-id="1876e-125">An *open type* is a stuctured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="1876e-126">开放类型允许你添加到数据模型的灵活性。</span><span class="sxs-lookup"><span data-stu-id="1876e-126">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="1876e-127">有关详细信息，请参阅 xxxx。</span><span class="sxs-lookup"><span data-stu-id="1876e-127">For more information, see xxxx.</span></span>

### <a name="support-for-dynamic-collection-properties-in-open-types"></a><span data-ttu-id="1876e-128">对动态集合属性中打开类型的支持</span><span class="sxs-lookup"><span data-stu-id="1876e-128">Support for dynamic collection properties in open types</span></span>

<span data-ttu-id="1876e-129">以前，动态属性必须是单个值。</span><span class="sxs-lookup"><span data-stu-id="1876e-129">Previously, a dynamic property had to be a single value.</span></span> <span data-ttu-id="1876e-130">在 5.3，动态属性可以具有集合值。</span><span class="sxs-lookup"><span data-stu-id="1876e-130">In 5.3, dynamic properties can have collection values.</span></span> <span data-ttu-id="1876e-131">例如，在下面的 JSON 负载，`Emails`属性是动态属性，并且是字符串类型的集合：</span><span class="sxs-lookup"><span data-stu-id="1876e-131">For example, in the following JSON payload, the `Emails` property is a dynamic property and is of collection of string type:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample4.cmd)]

### <a name="support-for-inheritance-for-complex-types"></a><span data-ttu-id="1876e-132">对于复杂类型的继承支持</span><span class="sxs-lookup"><span data-stu-id="1876e-132">Support for inheritance for complex types</span></span>

<span data-ttu-id="1876e-133">现在复杂类型可以继承自基类型。</span><span class="sxs-lookup"><span data-stu-id="1876e-133">Now complex types can inherit from a base type.</span></span> <span data-ttu-id="1876e-134">例如，OData 服务可以定义以下的复杂类型：</span><span class="sxs-lookup"><span data-stu-id="1876e-134">For example, an OData service could define the following complex types:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample5.cs)]

<span data-ttu-id="1876e-135">下面是此示例 EDM:</span><span class="sxs-lookup"><span data-stu-id="1876e-135">Here is the EDM for this example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample6.xml?highlight=8,15)]

<span data-ttu-id="1876e-136">有关详细信息，请参阅[OData 复杂类型继承示例](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)。</span><span class="sxs-lookup"><span data-stu-id="1876e-136">For more information, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="1876e-137">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="1876e-137">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="1876e-138">本部分介绍已知的问题和 ASP.NET Web API OData 5.3 中的重大更改。</span><span class="sxs-lookup"><span data-stu-id="1876e-138">This section describes known issues and breaking changes in the ASP.NET Web API OData 5.3.</span></span>

### <a name="odata-v4"></a><span data-ttu-id="1876e-139">OData v4</span><span class="sxs-lookup"><span data-stu-id="1876e-139">OData v4</span></span>

#### <a name="query-options"></a><span data-ttu-id="1876e-140">查询选项</span><span class="sxs-lookup"><span data-stu-id="1876e-140">Query Options</span></span>

<span data-ttu-id="1876e-141">问题： 使用嵌套的 $展开与 $levels = max 导致不正确的扩展深度。</span><span class="sxs-lookup"><span data-stu-id="1876e-141">Issue: Using nested $expand with $levels=max results in an incorrect expansion depth.</span></span>

<span data-ttu-id="1876e-142">例如，给定以下请求：</span><span class="sxs-lookup"><span data-stu-id="1876e-142">For example, given the following request:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-odata-53/samples/sample7.cmd)]

<span data-ttu-id="1876e-143">如果`MaxExpansionDepth`为 5，此查询将导致 6 的扩展深度。</span><span class="sxs-lookup"><span data-stu-id="1876e-143">If `MaxExpansionDepth` is 5, this query would result in an expansion depth of 6.</span></span>

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a><span data-ttu-id="1876e-144">Bug 修复和细微的功能更新</span><span class="sxs-lookup"><span data-stu-id="1876e-144">Bug Fixes and Minor Feature Updates</span></span>

<span data-ttu-id="1876e-145">此版本还包括几个 bug 修复和细微的功能更新。</span><span class="sxs-lookup"><span data-stu-id="1876e-145">This release also includes several bug fixes and minor feature updates.</span></span> <span data-ttu-id="1876e-146">您可以找到完整的列表：</span><span class="sxs-lookup"><span data-stu-id="1876e-146">You can find the complete list here:</span></span>

- [<span data-ttu-id="1876e-147">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="1876e-147">Bug fixes</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.3%20Beta&assignedTo=All&component=Web%20API|Web%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="OD"></a>
## <a name="aspnet-web-api-odata-531"></a><span data-ttu-id="1876e-148">ASP.NET Web API OData 5.3.1</span><span class="sxs-lookup"><span data-stu-id="1876e-148">ASP.NET Web API OData 5.3.1</span></span>

<span data-ttu-id="1876e-149">在此版本中[bug 修复](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.3.1%20Beta&amp;assignedTo=All&amp;component=Web%20API%20OData&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=All)某些 AllowedFunctions 枚举。</span><span class="sxs-lookup"><span data-stu-id="1876e-149">In this release we made a [bug fix](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.3.1%20Beta&amp;assignedTo=All&amp;component=Web%20API%20OData&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=All) to some of the AllowedFunctions enums.</span></span> <span data-ttu-id="1876e-150">此版本没有任何其他 bug 修复或新的功能。</span><span class="sxs-lookup"><span data-stu-id="1876e-150">This release doesn't have any other bug fixes or new features.</span></span>
