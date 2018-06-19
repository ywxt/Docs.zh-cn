---
title: ASP.NET Core 中的环境标记帮助程序
author: pkellner
description: 定义的 ASP.NET Core 环境标记帮助程序（包括所有属性）
manager: wpickett
ms.author: riande
ms.date: 07/14/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/environment-tag-helper
ms.openlocfilehash: 7a99ee0e59c7f49a3208d2c86c11cabce4294889
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
ms.locfileid: "28901179"
---
# <a name="environment-tag-helper-in-aspnet-core"></a><span data-ttu-id="e9b21-103">ASP.NET Core 中的环境标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="e9b21-103">Environment Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="e9b21-104">作者：[Peter Kellner](http://peterkellner.net) 和 [Hisham Bin Ateya](https://twitter.com/hishambinateya)</span><span class="sxs-lookup"><span data-stu-id="e9b21-104">By [Peter Kellner](http://peterkellner.net) and [Hisham Bin Ateya](https://twitter.com/hishambinateya)</span></span>

<span data-ttu-id="e9b21-105">环境标记帮助程序根据当前宿主环境，有条件地呈现其包含的内容。</span><span class="sxs-lookup"><span data-stu-id="e9b21-105">The Environment Tag Helper conditionally renders its enclosed content based on the current hosting environment.</span></span> <span data-ttu-id="e9b21-106">其单一属性 `names` 是一个以逗号分隔的环境名称列表，如果其中的任何名称与当前环境匹配，就会触发已包含内容的呈现。</span><span class="sxs-lookup"><span data-stu-id="e9b21-106">Its single attribute `names` is a comma separated list of environment names, that if any match to the current environment, will trigger the enclosed content to be rendered.</span></span>

## <a name="environment-tag-helper-attributes"></a><span data-ttu-id="e9b21-107">环境标记帮助程序属性</span><span class="sxs-lookup"><span data-stu-id="e9b21-107">Environment Tag Helper Attributes</span></span>

### <a name="names"></a><span data-ttu-id="e9b21-108">名称</span><span class="sxs-lookup"><span data-stu-id="e9b21-108">names</span></span>

<span data-ttu-id="e9b21-109">采用单个宿主环境名称或以逗号分隔的宿主环境名称列表，用于触发已包含内容的呈现。</span><span class="sxs-lookup"><span data-stu-id="e9b21-109">Accepts a single hosting environment name or a comma-separated list of hosting environment names that trigger the rendering of the enclosed content.</span></span>

<span data-ttu-id="e9b21-110">这些值与从 ASP.NET Core 静态属性 `HostingEnvironment.EnvironmentName` 返回的当前值进行比较。</span><span class="sxs-lookup"><span data-stu-id="e9b21-110">These value(s) are compared to the current value returned from the ASP.NET Core static property `HostingEnvironment.EnvironmentName`.</span></span>  <span data-ttu-id="e9b21-111">此值为以下值之一：**Staging**、**Development** 或 **Production**。</span><span class="sxs-lookup"><span data-stu-id="e9b21-111">This value is one of the following: **Staging**; **Development** or **Production**.</span></span> <span data-ttu-id="e9b21-112">比较不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="e9b21-112">The comparison ignores case.</span></span>

<span data-ttu-id="e9b21-113">有效的 `environment` 标记帮助程序示例为：</span><span class="sxs-lookup"><span data-stu-id="e9b21-113">An example of a valid `environment` tag helper is:</span></span>

```cshtml
<environment names="Staging,Production">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

## <a name="include-and-exclude-attributes"></a><span data-ttu-id="e9b21-114">include 和 exclude 属性</span><span class="sxs-lookup"><span data-stu-id="e9b21-114">include and exclude attributes</span></span>

<span data-ttu-id="e9b21-115">ASP.NET Core 2.x 添加了 `include` & `exclude` 属性。</span><span class="sxs-lookup"><span data-stu-id="e9b21-115">ASP.NET Core 2.x adds the `include` & `exclude` attributes.</span></span> <span data-ttu-id="e9b21-116">这些属性基于已包括或已排除的宿主环境名称，控制已包含内容的呈现。</span><span class="sxs-lookup"><span data-stu-id="e9b21-116">These attributes control rendering the enclosed content based on the included or excluded hosting environment names.</span></span>

### <a name="include-aspnet-core-20-and-later"></a><span data-ttu-id="e9b21-117">include ASP.NET Core 2.0 及更高版本</span><span class="sxs-lookup"><span data-stu-id="e9b21-117">include ASP.NET Core 2.0 and later</span></span>

<span data-ttu-id="e9b21-118">`include` 属性的行为与 ASP.NET Core 1.0 中 `names` 属性的行为类似。</span><span class="sxs-lookup"><span data-stu-id="e9b21-118">The `include` property has a similar behavior of the `names` attribute in ASP.NET Core 1.0.</span></span>

```cshtml
<environment include="Staging,Production">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

### <a name="exclude-aspnet-core-20-and-later"></a><span data-ttu-id="e9b21-119">exclude ASP.NET Core 2.0 及更高版本</span><span class="sxs-lookup"><span data-stu-id="e9b21-119">exclude ASP.NET Core 2.0 and later</span></span>

<span data-ttu-id="e9b21-120">相反，`exclude` 属性允许 `EnvironmentTagHelper` 为指定名称以外的所有宿主环境名称呈现已包含内容。</span><span class="sxs-lookup"><span data-stu-id="e9b21-120">In contrast, the `exclude` property lets the `EnvironmentTagHelper` render the enclosed content for all hosting environment names except the one(s) that you specified.</span></span>

```cshtml
<environment exclude="Development">
  <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

## <a name="additional-resources"></a><span data-ttu-id="e9b21-121">其他资源</span><span class="sxs-lookup"><span data-stu-id="e9b21-121">Additional resources</span></span>

* <xref:fundamentals/environments>
* <xref:fundamentals/dependency-injection#service-lifetimes-and-registration-options>
