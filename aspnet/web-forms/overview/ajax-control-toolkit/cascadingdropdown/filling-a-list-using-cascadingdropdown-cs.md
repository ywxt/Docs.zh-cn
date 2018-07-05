---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: 使用 CascadingDropDown (C#) 填充列表 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中 anoth 值...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 12a4271b2697df8e24fca5f7ff30797b1e4e077a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385416"
---
<a name="filling-a-list-using-cascadingdropdown-c"></a><span data-ttu-id="02699-103">使用 CascadingDropDown (C#) 填充列表</span><span class="sxs-lookup"><span data-stu-id="02699-103">Filling a List Using CascadingDropDown (C#)</span></span>
====================
<span data-ttu-id="02699-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="02699-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="02699-105">[下载代码](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="02699-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span></span>

> <span data-ttu-id="02699-106">AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。</span><span class="sxs-lookup"><span data-stu-id="02699-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="02699-107">（例如，一个列表提供了一系列我们状态，和与该状态中的主要城市然后填充下一个列表。）若要解决的第一个挑战是实际填充下拉列表中使用此控件。</span><span class="sxs-lookup"><span data-stu-id="02699-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>


## <a name="overview"></a><span data-ttu-id="02699-108">概述</span><span class="sxs-lookup"><span data-stu-id="02699-108">Overview</span></span>

<span data-ttu-id="02699-109">AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。</span><span class="sxs-lookup"><span data-stu-id="02699-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="02699-110">（例如，一个列表提供了一系列我们状态，和与该状态中的主要城市然后填充下一个列表。）若要解决的第一个挑战是实际填充下拉列表中使用此控件。</span><span class="sxs-lookup"><span data-stu-id="02699-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="02699-111">步骤</span><span class="sxs-lookup"><span data-stu-id="02699-111">Steps</span></span>

<span data-ttu-id="02699-112">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="02699-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="02699-113">然后，DropDownList 控件是必需的：</span><span class="sxs-lookup"><span data-stu-id="02699-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="02699-114">对于此列表中，添加一个 CascadingDropDown 扩展程序。</span><span class="sxs-lookup"><span data-stu-id="02699-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="02699-115">它将发送的异步请求到 web 服务，这将返回的条目显示在列表中的列表。</span><span class="sxs-lookup"><span data-stu-id="02699-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="02699-116">为实现此目的，需要设置以下 CascadingDropDown 属性：</span><span class="sxs-lookup"><span data-stu-id="02699-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="02699-117">`ServicePath`: Web 服务提供的列表项的 URL</span><span class="sxs-lookup"><span data-stu-id="02699-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="02699-118">`ServiceMethod`: Web 方法提供的列表项</span><span class="sxs-lookup"><span data-stu-id="02699-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="02699-119">`TargetControlID`: 下拉列表的 ID</span><span class="sxs-lookup"><span data-stu-id="02699-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="02699-120">`Category`： 提交到 web 方法调用时类别信息</span><span class="sxs-lookup"><span data-stu-id="02699-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="02699-121">`PromptText`： 以异步方式从服务器加载列表数据时显示的文本</span><span class="sxs-lookup"><span data-stu-id="02699-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="02699-122">下面是针对标记`CascadingDropDown`元素。</span><span class="sxs-lookup"><span data-stu-id="02699-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="02699-123">C# 和 VB 的唯一区别是关联的 web 服务的名称：</span><span class="sxs-lookup"><span data-stu-id="02699-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="02699-124">来自的 JavaScript 代码`CascadingDropDown`扩展程序调用 web 服务方法具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="02699-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="02699-125">因此重要的方面是该方法需要返回类型的数组`CascadingDropDownNameValue`（由 ASP.NET AJAX 控件工具包定义）。</span><span class="sxs-lookup"><span data-stu-id="02699-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="02699-126">在中`CascadingDropDownNameValue`构造函数，首先必须提供的列表项的文本，然后其值，就像`<option value="VALUE">NAME</option>`像在 HTML 中。</span><span class="sxs-lookup"><span data-stu-id="02699-126">In the `CascadingDropDownNameValue` contructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="02699-127">下面是一些示例数据：</span><span class="sxs-lookup"><span data-stu-id="02699-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="02699-128">正在加载页在浏览器中的将触发要填充与三个供应商的列表。</span><span class="sxs-lookup"><span data-stu-id="02699-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>


<span data-ttu-id="02699-129">[![列表已自动填充](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="02699-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="02699-130">自动填充列表 ([单击此项可查看原尺寸图像](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="02699-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="02699-131">下一篇</span><span class="sxs-lookup"><span data-stu-id="02699-131">Next</span></span>](using-cascadingdropdown-with-a-database-cs.md)
