---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
title: 动态添加折叠窗格 (VB) |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 Accordion 控件提供多个窗格，并允许用户一次显示其中一个。 面板通常声明 w...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: fae968c9-1902-487d-b053-86a46dd52c3f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
msc.type: authoredcontent
ms.openlocfilehash: 68c60ba6d4be5eb6709f7558d6be4165f8232a4f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868719"
---
<a name="dynamically-adding-an-accordion-pane-vb"></a><span data-ttu-id="dfd13-104">动态添加折叠窗格 (VB)</span><span class="sxs-lookup"><span data-stu-id="dfd13-104">Dynamically Adding An Accordion Pane (VB)</span></span>
====================
<span data-ttu-id="dfd13-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="dfd13-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="dfd13-106">[下载代码](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="dfd13-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)</span></span>

> <span data-ttu-id="dfd13-107">AJAX 控件工具包中的 Accordion 控件提供多个窗格，并允许用户一次显示其中一个。</span><span class="sxs-lookup"><span data-stu-id="dfd13-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="dfd13-108">面板中通常声明页本身，但可以使用服务器端代码来实现相同的结果。</span><span class="sxs-lookup"><span data-stu-id="dfd13-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>


## <a name="overview"></a><span data-ttu-id="dfd13-109">概述</span><span class="sxs-lookup"><span data-stu-id="dfd13-109">Overview</span></span>

<span data-ttu-id="dfd13-110">AJAX 控件工具包中的 Accordion 控件提供多个窗格，并允许用户一次显示其中一个。</span><span class="sxs-lookup"><span data-stu-id="dfd13-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="dfd13-111">面板中通常声明页本身，但可以使用服务器端代码来实现相同的结果。</span><span class="sxs-lookup"><span data-stu-id="dfd13-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="dfd13-112">步骤</span><span class="sxs-lookup"><span data-stu-id="dfd13-112">Steps</span></span>

<span data-ttu-id="dfd13-113">Accordion 控件可公开到服务器端代码中的所有重要属性。</span><span class="sxs-lookup"><span data-stu-id="dfd13-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="dfd13-114">除了别的之外`Panes`属性授予对构成 Accordion 的窗格的集合的访问。</span><span class="sxs-lookup"><span data-stu-id="dfd13-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="dfd13-115">每个窗格中的类型没有`AccordionPane`。</span><span class="sxs-lookup"><span data-stu-id="dfd13-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="dfd13-116">因此，它是普通用于创建此类窗格：</span><span class="sxs-lookup"><span data-stu-id="dfd13-116">It is therefore trivial to create such a pane:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample1.vb)]

<span data-ttu-id="dfd13-117">`HeaderContainer`属性`AccordionPane`提供访问在窗格中; 的标头部分的 ASP.NET 控件`ContentContainer`属性`AccordionPane`执行相同的操作的窗格的内容部分。</span><span class="sxs-lookup"><span data-stu-id="dfd13-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="dfd13-118">这样，用于向窗格添加内容的 ASP.NET 代码：</span><span class="sxs-lookup"><span data-stu-id="dfd13-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample2.vb)]

<span data-ttu-id="dfd13-119">最后，必须将窗格添加到`Panes`Accordion 的集合：</span><span class="sxs-lookup"><span data-stu-id="dfd13-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample3.vb)]

<span data-ttu-id="dfd13-120">下面是将两个窗格添加到 Accordion 控件的完整服务器端代码：</span><span class="sxs-lookup"><span data-stu-id="dfd13-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample4.aspx)]

<span data-ttu-id="dfd13-121">唯一缺少元素是 Accordion 本身，这取决于是否存在的 ASP.NET`ScriptManager`控件：</span><span class="sxs-lookup"><span data-stu-id="dfd13-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample5.aspx)]

<span data-ttu-id="dfd13-122">若要完成该示例，两个 Accordion 控件中引用的 CSS 类提供浏览器样式的信息：</span><span class="sxs-lookup"><span data-stu-id="dfd13-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-vb/samples/sample6.css)]


<span data-ttu-id="dfd13-123">[![服务器端代码动态添加可折叠的面板中的数据](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="dfd13-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)</span></span>

<span data-ttu-id="dfd13-124">服务器端代码动态添加可折叠的面板中的数据 ([单击以查看实际尺寸的图像](dynamically-adding-an-accordion-pane-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="dfd13-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="dfd13-125">上一篇</span><span class="sxs-lookup"><span data-stu-id="dfd13-125">Previous</span></span>](databinding-to-an-accordion-vb.md)
