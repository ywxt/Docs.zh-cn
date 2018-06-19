---
title: ASP.NET Core 内置标记帮助程序
author: pkellner
description: 了解 ASP.NET Core 内置标记帮助程序如何提高生产力。
manager: wpickett
ms.author: riande
ms.date: 09/13/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/Index
ms.openlocfilehash: f539f96a87b125c0f55855f780bbff005db8c0d9
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
ms.locfileid: "29903203"
---
# <a name="aspnet-core-built-in-tag-helpers"></a><span data-ttu-id="2f775-103">ASP.NET Core 内置标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="2f775-103">ASP.NET Core built-in Tag Helpers</span></span>

<span data-ttu-id="2f775-104">作者：[Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="2f775-104">By [Peter Kellner](http://peterkellner.net)</span></span>

<span data-ttu-id="2f775-105">ASP.NET Core 包括了许多内置标记帮助程序以用于提高生产力。</span><span class="sxs-lookup"><span data-stu-id="2f775-105">ASP.NET Core includes many built-in Tag Helpers to boost your productivity.</span></span> <span data-ttu-id="2f775-106">本部分对内置标记帮助程序进行了概述。</span><span class="sxs-lookup"><span data-stu-id="2f775-106">This section provides an overview of the built-in Tag Helpers.</span></span>

> [!NOTE]
> <span data-ttu-id="2f775-107">有些内置标记帮助程序未在此处讨论，因为它们由 [Razor](xref:mvc/views/razor) 视图引擎在内部使用。</span><span class="sxs-lookup"><span data-stu-id="2f775-107">There are built-in Tag Helpers which aren't discussed, since they're used internally by the [Razor](xref:mvc/views/razor) view engine.</span></span> <span data-ttu-id="2f775-108">这包括针对扩展到网站根路径的 ~ 字符所适用的标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="2f775-108">This includes a Tag Helper for the ~ character, which expands to the root path of the website.</span></span>

## <a name="built-in-aspnet-core-tag-helpers"></a><span data-ttu-id="2f775-109">内置 ASP.NET Core 标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="2f775-109">Built-in ASP.NET Core Tag Helpers</span></span>

<span data-ttu-id="2f775-110">**[定位点标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-110">**[Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span></span>

<span data-ttu-id="2f775-111">**[缓存标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-111">**[Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span></span>

<span data-ttu-id="2f775-112">**[分布式缓存帮助程序](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-112">**[Distributed Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span></span>

<span data-ttu-id="2f775-113">**[环境标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-113">**[Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span></span>

[comment]: **[FormActionTagHelper](xref:mvc/views/tag-helpers/builtin-th/form-action-tag-helper)**

<span data-ttu-id="2f775-114">**[表单标记帮助程序](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-114">**[Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span></span>

<span data-ttu-id="2f775-115">**[图像标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-115">**[Image Tag Helper](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span></span>

<span data-ttu-id="2f775-116">**[输入标记帮助程序](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-116">**[Input Tag Helper](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span></span>

<span data-ttu-id="2f775-117">**[标签标记帮助程序](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-117">**[Label Tag Helper](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span></span>

[comment]: **[LinkTagHelper](xref:mvc/views/tag-helpers/builtin-th/link-tag-helper)**

[comment]: **[OptionTagHelper](xref:mvc/views/tag-helpers/builtin-th/option-tag-helper)**

[comment]: **[ScriptTagHelper](xref:mvc/views/tag-helpers/builtin-th/script-tag-helper)**

<span data-ttu-id="2f775-118">**[部分标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-118">**[Partial Tag Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span></span>

<span data-ttu-id="2f775-119">**[选择标记帮助程序](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-119">**[Select Tag Helper](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span></span>

<span data-ttu-id="2f775-120">**[文本区标记帮助程序](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-120">**[Textarea Tag Helper](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span></span>

<span data-ttu-id="2f775-121">**[验证消息标记帮助程序](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-121">**[Validation Message Tag Helper](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span></span>

<span data-ttu-id="2f775-122">**[验证摘要标记帮助程序](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="2f775-122">**[Validation Summary Tag Helper](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f775-123">其他资源</span><span class="sxs-lookup"><span data-stu-id="2f775-123">Additional resources</span></span>

* [<span data-ttu-id="2f775-124">客户端开发</span><span class="sxs-lookup"><span data-stu-id="2f775-124">Client-side development</span></span>](xref:client-side/index)
* [<span data-ttu-id="2f775-125">标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="2f775-125">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
