---
title: "分布式缓存标记帮助器 |Microsoft 文档"
author: pkellner
description: "演示如何使用缓存标记帮助器"
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper
ms.openlocfilehash: f5844dade218fdba1169a55fe3ce251a9cc03db2
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="distributed-cache-tag-helper"></a><span data-ttu-id="ec137-103">分布式的缓存标记帮助器</span><span class="sxs-lookup"><span data-stu-id="ec137-103">Distributed Cache Tag Helper</span></span>

<span data-ttu-id="ec137-104">作者：[Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="ec137-104">By [Peter Kellner](http://peterkellner.net)</span></span> 


<span data-ttu-id="ec137-105">分布式缓存标记帮助器提供的功能可以显著提高通过缓存到分布式的缓存源其内容的 ASP.NET Core 应用的性能。</span><span class="sxs-lookup"><span data-stu-id="ec137-105">The Distributed Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to a distributed cache source.</span></span>

<span data-ttu-id="ec137-106">分布式缓存标记帮助器继承自相同的基缓存标记帮助器类。</span><span class="sxs-lookup"><span data-stu-id="ec137-106">The Distributed Cache Tag Helper inherits from the same base class as the Cache Tag Helper.</span></span>  <span data-ttu-id="ec137-107">与缓存标记帮助器关联的所有属性也将都适用于分布式标记帮助器。</span><span class="sxs-lookup"><span data-stu-id="ec137-107">All attributes associated with the Cache Tag Helper will also work on the Distributed Tag Helper.</span></span>


<span data-ttu-id="ec137-108">分布式缓存标记帮助程序遵循**显式依赖关系原则**称为**构造函数注入**。</span><span class="sxs-lookup"><span data-stu-id="ec137-108">The Distributed Cache Tag Helper follows the **Explicit Dependencies Principle** known as **Constructor Injection**.</span></span>  <span data-ttu-id="ec137-109">具体而言，`IDistributedCache`接口容器传递到分布式缓存标记帮助器的构造函数。</span><span class="sxs-lookup"><span data-stu-id="ec137-109">Specifically, the `IDistributedCache` interface container is passed into the Distributed Cache Tag Helper's constructor.</span></span>  <span data-ttu-id="ec137-110">如果没有特定的具体实现`IDistributedCache`已在中创建`ConfigureServices`，通常会在 startup.cs，找到然后分布式缓存标记帮助程序将使用相同的内存中提供程序将缓存的数据存储为基本缓存标记帮助器。</span><span class="sxs-lookup"><span data-stu-id="ec137-110">If no specific concrete implementation of `IDistributedCache` has been created in `ConfigureServices`, usually found in startup.cs, then the Distributed Cache Tag Helper will use the same in-memory provider for storing cached data as the basic Cache Tag Helper.</span></span>

## <a name="distributed-cache-tag-helper-attributes"></a><span data-ttu-id="ec137-111">分布式缓存标记帮助器属性</span><span class="sxs-lookup"><span data-stu-id="ec137-111">Distributed Cache Tag Helper Attributes</span></span>

- - -

### <a name="enabled-expires-on-expires-after-expires-sliding-vary-by-header-vary-by-query-vary-by-route-vary-by-cookie-vary-by-user-vary-by-priority"></a><span data-ttu-id="ec137-112">启用过期上过期之后过期的滑动的标题会有所不同不同的查询不同的路由改变通过 cookie 改变按用户变化依据优先级</span><span class="sxs-lookup"><span data-stu-id="ec137-112">enabled expires-on expires-after expires-sliding vary-by-header vary-by-query vary-by-route vary-by-cookie vary-by-user vary-by priority</span></span>

<span data-ttu-id="ec137-113">有关定义，请参阅缓存标记帮助器。</span><span class="sxs-lookup"><span data-stu-id="ec137-113">See Cache Tag Helper for definitions.</span></span> <span data-ttu-id="ec137-114">分布式的缓存标记帮助器继承自与缓存标记帮助器类相同，因此所有这些特性是常见从缓存标记帮助器。</span><span class="sxs-lookup"><span data-stu-id="ec137-114">Distributed Cache Tag Helper inherits from the same class as Cache Tag Helper so all these attributes are common from Cache Tag Helper.</span></span>

- - -

### <a name="name-required"></a><span data-ttu-id="ec137-115">名称 （必需）</span><span class="sxs-lookup"><span data-stu-id="ec137-115">name (required)</span></span>

| <span data-ttu-id="ec137-116">特性类型</span><span class="sxs-lookup"><span data-stu-id="ec137-116">Attribute Type</span></span>    | <span data-ttu-id="ec137-117">示例值</span><span class="sxs-lookup"><span data-stu-id="ec137-117">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="ec137-118">字符串</span><span class="sxs-lookup"><span data-stu-id="ec137-118">string</span></span>    | <span data-ttu-id="ec137-119">"my-distributed-cache-unique-key-101"</span><span class="sxs-lookup"><span data-stu-id="ec137-119">"my-distributed-cache-unique-key-101"</span></span>     |

<span data-ttu-id="ec137-120">所需`name`属性用作每个实例的分布式缓存标记帮助器存储该缓存的键。</span><span class="sxs-lookup"><span data-stu-id="ec137-120">The required `name` attribute is used as a key to that cache stored for each instance of a Distributed Cache Tag Helper.</span></span>  <span data-ttu-id="ec137-121">与不同的是基本缓存标记帮助程序为基于 Razor 页名称和位置在 razor 页中的标记帮助程序的每个缓存标记帮助器实例分配一个密钥，分布式缓存标记帮助器仅基于的密钥属性`name`</span><span class="sxs-lookup"><span data-stu-id="ec137-121">Unlike the basic Cache Tag Helper that assigns a key to each Cache Tag Helper instance based on the Razor page name and location of the tag helper in the razor page, the Distributed Cache Tag Helper only bases it's key on the attribute `name`</span></span>

<span data-ttu-id="ec137-122">用法示例：</span><span class="sxs-lookup"><span data-stu-id="ec137-122">Usage Example:</span></span>

```cshtml
<distributed-cache name="my-distributed-cache-unique-key-101">
    Time Inside Cache Tag Helper: @DateTime.Now
</distributed-cache>
```

## <a name="distributed-cache-tag-helper-idistributedcache-implementations"></a><span data-ttu-id="ec137-123">分布式缓存标记帮助器 IDistributedCache 实现</span><span class="sxs-lookup"><span data-stu-id="ec137-123">Distributed Cache Tag Helper IDistributedCache Implementations</span></span>

<span data-ttu-id="ec137-124">有的两个实现`IDistributedCache`内置到 ASP.NET 核心。</span><span class="sxs-lookup"><span data-stu-id="ec137-124">There are two implementations of `IDistributedCache` built in to ASP.NET Core.</span></span>  <span data-ttu-id="ec137-125">一个基于**Sql Server**和其他基于**Redis**。</span><span class="sxs-lookup"><span data-stu-id="ec137-125">One is based on **Sql Server** and the other is based on **Redis**.</span></span> <span data-ttu-id="ec137-126">以下名为"使用分布式缓存"引用的资源处找不到这些实现的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ec137-126">Details of these implementations can be found at the resource referenced below named "Working with a distributed cache".</span></span> <span data-ttu-id="ec137-127">这两个实现涉及设置的实例`IDistributedCache`中 ASP.NET Core **startup.cs**。</span><span class="sxs-lookup"><span data-stu-id="ec137-127">Both implementations involve setting an instance of `IDistributedCache` in ASP.NET Core's **startup.cs**.</span></span>

<span data-ttu-id="ec137-128">没有专门与使用的任何特定实现标记特性`IDistributedCache`。</span><span class="sxs-lookup"><span data-stu-id="ec137-128">There are no tag attributes specifically associated with using any specific implementation of `IDistributedCache`.</span></span>



- - -



## <a name="additional-resources"></a><span data-ttu-id="ec137-129">其他资源</span><span class="sxs-lookup"><span data-stu-id="ec137-129">Additional resources</span></span>

* <xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper>
* <xref:fundamentals/dependency-injection#service-lifetimes-and-registration-options>
* <xref:performance/caching/distributed>
* <xref:performance/caching/memory>
* <xref:security/authentication/identity>
