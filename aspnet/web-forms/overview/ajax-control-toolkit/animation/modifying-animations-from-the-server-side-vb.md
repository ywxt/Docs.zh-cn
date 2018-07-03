---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: 从服务器端 (VB) 修改动画 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 也可以将动画...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: d39a40f2776d5b87bf82d1a6c6282ce920f4a907
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37401949"
---
<a name="modifying-animations-from-the-server-side-vb"></a><span data-ttu-id="fcb24-104">从服务器端 (VB) 修改动画</span><span class="sxs-lookup"><span data-stu-id="fcb24-104">Modifying Animations From The Server Side (VB)</span></span>
====================
<span data-ttu-id="fcb24-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="fcb24-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fcb24-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="fcb24-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span></span>

> <span data-ttu-id="fcb24-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="fcb24-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="fcb24-108">也可能在服务器端发生更改动画</span><span class="sxs-lookup"><span data-stu-id="fcb24-108">The animations may also be changed on the server-side</span></span>


## <a name="overview"></a><span data-ttu-id="fcb24-109">概述</span><span class="sxs-lookup"><span data-stu-id="fcb24-109">Overview</span></span>

<span data-ttu-id="fcb24-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="fcb24-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="fcb24-111">也可能在服务器端发生更改动画</span><span class="sxs-lookup"><span data-stu-id="fcb24-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="fcb24-112">步骤</span><span class="sxs-lookup"><span data-stu-id="fcb24-112">Steps</span></span>

<span data-ttu-id="fcb24-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="fcb24-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

<span data-ttu-id="fcb24-114">动画将应用于文本的外观如下所示的面板：</span><span class="sxs-lookup"><span data-stu-id="fcb24-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

<span data-ttu-id="fcb24-115">在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：</span><span class="sxs-lookup"><span data-stu-id="fcb24-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

<span data-ttu-id="fcb24-116">代码的其余部分在服务器端上运行，并且不使用标记;相反，它使用代码来创建`AnimationExtender`控件：</span><span class="sxs-lookup"><span data-stu-id="fcb24-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

<span data-ttu-id="fcb24-117">但是，该控件工具包当前不提供创建单个动画 API 访问权限。</span><span class="sxs-lookup"><span data-stu-id="fcb24-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="fcb24-118">不过，它是可以将设置`AnimationExtender`的动画属性设置为一个字符串，包含以声明方式分配动画时使用的 XML 标记。</span><span class="sxs-lookup"><span data-stu-id="fcb24-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="fcb24-119">若要创建的 XML 不能包含`<Animations>`元素可以使用.NET Framework 的 XML 支持，或在以下代码，只需提供的字符串：</span><span class="sxs-lookup"><span data-stu-id="fcb24-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

<span data-ttu-id="fcb24-120">最后，添加`AnimationExtender`控制转移到当前页上，在`<form runat="server">`元素，并确保动画包含并运行：</span><span class="sxs-lookup"><span data-stu-id="fcb24-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]


<span data-ttu-id="fcb24-121">[![使用服务器端 C# /VB 代码创建动画](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fcb24-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span></span>

<span data-ttu-id="fcb24-122">使用服务器端 C# /VB 代码创建动画 ([单击此项可查看原尺寸图像](modifying-animations-from-the-server-side-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="fcb24-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fcb24-123">[上一页](triggering-an-animation-in-another-control-vb.md)
> [下一页](executing-animations-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="fcb24-123">[Previous](triggering-an-animation-in-another-control-vb.md)
[Next](executing-animations-using-client-side-code-vb.md)</span></span>
