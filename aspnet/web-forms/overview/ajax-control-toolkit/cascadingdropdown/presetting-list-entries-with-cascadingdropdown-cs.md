---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
title: 预设置列表条目使用 CascadingDropDown (C#) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中 anoth 值...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 04c79748-0f21-4a3b-aba5-e1ce3161c32e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 56093ad098d69039aafa9b4e6ba4e4c2ad91e49b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37361994"
---
<a name="presetting-list-entries-with-cascadingdropdown-c"></a><span data-ttu-id="a13f7-103">预设置列表条目使用 CascadingDropDown (C#)</span><span class="sxs-lookup"><span data-stu-id="a13f7-103">Presetting List Entries with CascadingDropDown (C#)</span></span>
====================
<span data-ttu-id="a13f7-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a13f7-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a13f7-105">[下载代码](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a13f7-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)</span></span>

> <span data-ttu-id="a13f7-106">AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。</span><span class="sxs-lookup"><span data-stu-id="a13f7-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="a13f7-107">借助极少量的代码就可以动态加载数据后，预先选择一个列表元素。</span><span class="sxs-lookup"><span data-stu-id="a13f7-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>


## <a name="overview"></a><span data-ttu-id="a13f7-108">概述</span><span class="sxs-lookup"><span data-stu-id="a13f7-108">Overview</span></span>

<span data-ttu-id="a13f7-109">AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。</span><span class="sxs-lookup"><span data-stu-id="a13f7-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="a13f7-110">（例如，一个列表提供了一系列我们状态，和与该状态中的主要城市然后填充下一个列表。）借助极少量的代码就可以动态加载数据后，预先选择一个列表元素。</span><span class="sxs-lookup"><span data-stu-id="a13f7-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="a13f7-111">步骤</span><span class="sxs-lookup"><span data-stu-id="a13f7-111">Steps</span></span>

<span data-ttu-id="a13f7-112">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="a13f7-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="a13f7-113">然后，DropDownList 控件是必需的：</span><span class="sxs-lookup"><span data-stu-id="a13f7-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="a13f7-114">对于此列表中，添加 CascadingDropDown 扩展程序以提供 web 服务 URL 和方法的信息：</span><span class="sxs-lookup"><span data-stu-id="a13f7-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="a13f7-115">然后 CascadingDropDown 扩展程序以异步方式调用 web 服务使用以下方法签名：</span><span class="sxs-lookup"><span data-stu-id="a13f7-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="a13f7-116">该方法返回类型 CascadingDropDown 值的数组。</span><span class="sxs-lookup"><span data-stu-id="a13f7-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="a13f7-117">类型的构造函数要求第一次列表项的标题和值 (HTML`value`属性)。</span><span class="sxs-lookup"><span data-stu-id="a13f7-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="a13f7-118">如果第三个参数设置为 true 时，列表中选择元素时自动在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="a13f7-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="a13f7-119">加载页面在浏览器中的将填充下拉列表中的与三个供应商，第二个被预先选定状态。</span><span class="sxs-lookup"><span data-stu-id="a13f7-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>


<span data-ttu-id="a13f7-120">[![填充和预先自动选择列表](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a13f7-120">[![The list is filled and preselected automatically](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="a13f7-121">填充和预先自动选择列表 ([单击此项可查看原尺寸图像](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a13f7-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a13f7-122">[上一页](using-cascadingdropdown-with-a-database-cs.md)
> [下一页](using-auto-postback-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="a13f7-122">[Previous](using-cascadingdropdown-with-a-database-cs.md)
[Next](using-auto-postback-with-cascadingdropdown-cs.md)</span></span>
