---
title: ASP.NET Core 中的分布式缓存标记帮助程序
author: pkellner
description: 演示如何使用缓存标记帮助程序
ms.author: riande
ms.date: 02/14/2017
uid: mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper
ms.openlocfilehash: a35a5795c086273e773c613c483fc6343c694bf2
ms.sourcegitcommit: 927e510d68f269d8335b5a7c8592621219a90965
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2018
ms.locfileid: "39342167"
---
# <a name="distributed-cache-tag-helper-in-aspnet-core"></a><span data-ttu-id="fc39a-103">ASP.NET Core 中的分布式缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="fc39a-103">Distributed Cache Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="fc39a-104">作者：[Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="fc39a-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="fc39a-105">分布式缓存标记帮助程序将其内容缓存到分布式缓存源，从而大幅提高 ASP.NET Core 应用的性能。</span><span class="sxs-lookup"><span data-stu-id="fc39a-105">The Distributed Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to a distributed cache source.</span></span>

<span data-ttu-id="fc39a-106">分布式缓存标记帮助程序与缓存标记帮助程序继承自相同的基类。</span><span class="sxs-lookup"><span data-stu-id="fc39a-106">The Distributed Cache Tag Helper inherits from the same base class as the Cache Tag Helper.</span></span> <span data-ttu-id="fc39a-107">与缓存标记帮助程序相关的所有属性也将适用于分布式标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="fc39a-107">All attributes associated with the Cache Tag Helper will also work on the Distributed Tag Helper.</span></span>

<span data-ttu-id="fc39a-108">分布式缓存标记帮助程序遵循被称为“构造函数注入”的显式依赖关系原则。</span><span class="sxs-lookup"><span data-stu-id="fc39a-108">The Distributed Cache Tag Helper follows the **Explicit Dependencies Principle** known as **Constructor Injection**.</span></span> <span data-ttu-id="fc39a-109">具体而言，将 `IDistributedCache` 接口容器传递给分布式缓存标记帮助程序的构造函数。</span><span class="sxs-lookup"><span data-stu-id="fc39a-109">Specifically, the `IDistributedCache` interface container is passed into the Distributed Cache Tag Helper's constructor.</span></span> <span data-ttu-id="fc39a-110">如果未在 `ConfigureServices` 中创建 `IDistributedCache` 的特定具体实现（通常在 startup.cs 中找到），则分布式缓存标记帮助程序将使用与基本缓存标记帮助程序所用相同的内存中提供程序来存储缓存数据。</span><span class="sxs-lookup"><span data-stu-id="fc39a-110">If no specific concrete implementation of `IDistributedCache` has been created in `ConfigureServices`, usually found in startup.cs, then the Distributed Cache Tag Helper will use the same in-memory provider for storing cached data as the basic Cache Tag Helper.</span></span>

## <a name="distributed-cache-tag-helper-attributes"></a><span data-ttu-id="fc39a-111">分布式缓存标记帮助程序属性</span><span class="sxs-lookup"><span data-stu-id="fc39a-111">Distributed Cache Tag Helper Attributes</span></span>

- - -

### <a name="enabled-expires-on-expires-after-expires-sliding-vary-by-header-vary-by-query-vary-by-route-vary-by-cookie-vary-by-user-vary-by-priority"></a><span data-ttu-id="fc39a-112">enabled expires-on expires-after expires-sliding vary-by-header vary-by-query vary-by-route vary-by-cookie vary-by-user vary-by priority</span><span class="sxs-lookup"><span data-stu-id="fc39a-112">enabled expires-on expires-after expires-sliding vary-by-header vary-by-query vary-by-route vary-by-cookie vary-by-user vary-by priority</span></span>

<span data-ttu-id="fc39a-113">有关定义，请参阅缓存标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="fc39a-113">See Cache Tag Helper for definitions.</span></span> <span data-ttu-id="fc39a-114">分布式缓存标记帮助程序与缓存标记帮助程序继承自相同的类，因此其属性都是缓存标记帮助程序中的常见属性。</span><span class="sxs-lookup"><span data-stu-id="fc39a-114">Distributed Cache Tag Helper inherits from the same class as Cache Tag Helper so all these attributes are common from Cache Tag Helper.</span></span>

- - -

### <a name="name-required"></a><span data-ttu-id="fc39a-115">name（必需）</span><span class="sxs-lookup"><span data-stu-id="fc39a-115">name (required)</span></span>

| <span data-ttu-id="fc39a-116">属性类型</span><span class="sxs-lookup"><span data-stu-id="fc39a-116">Attribute Type</span></span>    | <span data-ttu-id="fc39a-117">示例值</span><span class="sxs-lookup"><span data-stu-id="fc39a-117">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="fc39a-118">字符串</span><span class="sxs-lookup"><span data-stu-id="fc39a-118">string</span></span>    | <span data-ttu-id="fc39a-119">"my-distributed-cache-unique-key-101"</span><span class="sxs-lookup"><span data-stu-id="fc39a-119">"my-distributed-cache-unique-key-101"</span></span>     |

<span data-ttu-id="fc39a-120">必需的 `name` 属性用作为分布式缓存标记帮助程序的每个实例存储的缓存的键。</span><span class="sxs-lookup"><span data-stu-id="fc39a-120">The required `name` attribute is used as a key to that cache stored for each instance of a Distributed Cache Tag Helper.</span></span> <span data-ttu-id="fc39a-121">分布式缓存标记帮助程序与基础缓存标记帮助程序不同：后者基于 Razor 页面名称和 Razor 页面中标记帮助程序的位置，向每个缓存标记帮助程序实例分配一个键；前者的键仅基于属性 `name`</span><span class="sxs-lookup"><span data-stu-id="fc39a-121">Unlike the basic Cache Tag Helper that assigns a key to each Cache Tag Helper instance based on the Razor page name and location of the Tag Helper in the razor page, the Distributed Cache Tag Helper only bases its key on the attribute `name`</span></span>

<span data-ttu-id="fc39a-122">用法示例：</span><span class="sxs-lookup"><span data-stu-id="fc39a-122">Usage Example:</span></span>

```cshtml
<distributed-cache name="my-distributed-cache-unique-key-101">
    Time Inside Cache Tag Helper: @DateTime.Now
</distributed-cache>
```

## <a name="distributed-cache-tag-helper-idistributedcache-implementations"></a><span data-ttu-id="fc39a-123">分布式缓存标记帮助程序 IDistributedCache 实现</span><span class="sxs-lookup"><span data-stu-id="fc39a-123">Distributed Cache Tag Helper IDistributedCache implementations</span></span>

<span data-ttu-id="fc39a-124">ASP.NET Core 中内置了 `IDistributedCache` 的两个实现。</span><span class="sxs-lookup"><span data-stu-id="fc39a-124">There are two implementations of `IDistributedCache` built in to ASP.NET Core.</span></span> <span data-ttu-id="fc39a-125">一个基于 SQL Server，另一个基于 Redis。</span><span class="sxs-lookup"><span data-stu-id="fc39a-125">One is based on SQL Server and the other is based on Redis.</span></span> <span data-ttu-id="fc39a-126">有关这些实现的详细信息，请参阅 <xref:performance/caching/distributed>。</span><span class="sxs-lookup"><span data-stu-id="fc39a-126">Details of these implementations can be found at <xref:performance/caching/distributed>.</span></span> <span data-ttu-id="fc39a-127">这两个实现都涉及在 ASP.NET Core 的 startup.cs 中设置 `IDistributedCache` 的实例。</span><span class="sxs-lookup"><span data-stu-id="fc39a-127">Both implementations involve setting an instance of `IDistributedCache` in ASP.NET Core's *Startup.cs*.</span></span>

<span data-ttu-id="fc39a-128">没有专门与使用 `IDistributedCache` 的任何特定实现相关的标记属性。</span><span class="sxs-lookup"><span data-stu-id="fc39a-128">There are no tag attributes specifically associated with using any specific implementation of `IDistributedCache`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fc39a-129">其他资源</span><span class="sxs-lookup"><span data-stu-id="fc39a-129">Additional resources</span></span>

* <xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper>
* <xref:fundamentals/dependency-injection>
* <xref:performance/caching/distributed>
* <xref:performance/caching/memory>
* <xref:security/authentication/identity>
