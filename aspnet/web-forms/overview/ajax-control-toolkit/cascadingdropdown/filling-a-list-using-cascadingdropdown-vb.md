---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: 填充使用 CascadingDropDown (VB) 的列表 |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展的 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中 anoth 值...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: e488a30443970d5e2ce825abd96d8e4a027585d1
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873048"
---
<a name="filling-a-list-using-cascadingdropdown-vb"></a><span data-ttu-id="77b62-103">填充使用 CascadingDropDown (VB) 的列表</span><span class="sxs-lookup"><span data-stu-id="77b62-103">Filling a List Using CascadingDropDown (VB)</span></span>
====================
<span data-ttu-id="77b62-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="77b62-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="77b62-105">[下载代码](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="77b62-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span></span>

> <span data-ttu-id="77b62-106">AJAX 控件工具包中的 CascadingDropDown 控件扩展的 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 值。</span><span class="sxs-lookup"><span data-stu-id="77b62-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="77b62-107">（例如，一个列表提供了一份我们状态，并且用处于该状态的主要城市然后填充下一个列表。）若要解决第一次质询是实际填充使用此控件的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="77b62-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>


## <a name="overview"></a><span data-ttu-id="77b62-108">概述</span><span class="sxs-lookup"><span data-stu-id="77b62-108">Overview</span></span>

<span data-ttu-id="77b62-109">AJAX 控件工具包中的 CascadingDropDown 控件扩展的 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 值。</span><span class="sxs-lookup"><span data-stu-id="77b62-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="77b62-110">（例如，一个列表提供了一份我们状态，并且用处于该状态的主要城市然后填充下一个列表。）若要解决第一次质询是实际填充使用此控件的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="77b62-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="77b62-111">步骤</span><span class="sxs-lookup"><span data-stu-id="77b62-111">Steps</span></span>

<span data-ttu-id="77b62-112">为了激活 ASP.NET AJAX 和控件工具包中的功能`ScriptManager`必须在页面上任意位置放置控件 (但内`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="77b62-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="77b62-113">然后，需要进行的 DropDownList 控制：</span><span class="sxs-lookup"><span data-stu-id="77b62-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="77b62-114">对于此列表中，添加 CascadingDropDown 扩展程序。</span><span class="sxs-lookup"><span data-stu-id="77b62-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="77b62-115">它将发送的异步请求到 web 服务，然后将返回要在列表中显示的项的列表。</span><span class="sxs-lookup"><span data-stu-id="77b62-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="77b62-116">为此，需要设置以下 CascadingDropDown 属性：</span><span class="sxs-lookup"><span data-stu-id="77b62-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="77b62-117">`ServicePath`: 提供的列表项 web 服务的 URL</span><span class="sxs-lookup"><span data-stu-id="77b62-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="77b62-118">`ServiceMethod`: Web 方法提供的列表项</span><span class="sxs-lookup"><span data-stu-id="77b62-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="77b62-119">`TargetControlID`: ID 的下拉列表</span><span class="sxs-lookup"><span data-stu-id="77b62-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="77b62-120">`Category`： 提交给 web 方法调用时的类别信息</span><span class="sxs-lookup"><span data-stu-id="77b62-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="77b62-121">`PromptText`： 当以异步方式从服务器加载列表数据时显示的文本</span><span class="sxs-lookup"><span data-stu-id="77b62-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="77b62-122">下面是有关标记`CascadingDropDown`元素。</span><span class="sxs-lookup"><span data-stu-id="77b62-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="77b62-123">C# 和 VB 的唯一区别是关联的 web 服务的名称：</span><span class="sxs-lookup"><span data-stu-id="77b62-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="77b62-124">JavaScript 代码来自`CascadingDropDown`扩展程序调用 web 服务方法具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="77b62-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="77b62-125">因此重要方面是该方法需要返回类型的数组`CascadingDropDownNameValue`（由 ASP.NET AJAX 控件工具包定义）。</span><span class="sxs-lookup"><span data-stu-id="77b62-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="77b62-126">在`CascadingDropDownNameValue`构造函数，第一个列表项的文本，然后其值都必须提供，就像`<option value="VALUE">NAME</option>`像在 HTML 中。</span><span class="sxs-lookup"><span data-stu-id="77b62-126">In the `CascadingDropDownNameValue` contructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="77b62-127">下面是一些示例数据：</span><span class="sxs-lookup"><span data-stu-id="77b62-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="77b62-128">加载浏览器中将触发三个供应商要填充的列表。</span><span class="sxs-lookup"><span data-stu-id="77b62-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>


<span data-ttu-id="77b62-129">[![列表已自动填充](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="77b62-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="77b62-130">列表已自动填充 ([单击以查看实际尺寸的图像](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="77b62-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="77b62-131">[上一页](using-auto-postback-with-cascadingdropdown-cs.md)
> [下一页](using-cascadingdropdown-with-a-database-vb.md)</span><span class="sxs-lookup"><span data-stu-id="77b62-131">[Previous](using-auto-postback-with-cascadingdropdown-cs.md)
[Next](using-cascadingdropdown-with-a-database-vb.md)</span></span>
