---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
title: 修改动画从服务器端 (C#) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 也可以将动画...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: b0abec39-a1c9-422d-ba9a-ef16f6185af8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
msc.type: authoredcontent
ms.openlocfilehash: 8954f025873ea553fde26c6e2330ce6e5be2b539
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804049"
---
<a name="modifying-animations-from-the-server-side-c"></a><span data-ttu-id="f5e80-104">修改动画从服务器端 (C#)</span><span class="sxs-lookup"><span data-stu-id="f5e80-104">Modifying Animations From The Server Side (C#)</span></span>
====================
<span data-ttu-id="f5e80-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f5e80-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f5e80-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f5e80-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)</span></span>

> <span data-ttu-id="f5e80-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="f5e80-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="f5e80-108">也可能在服务器端发生更改动画</span><span class="sxs-lookup"><span data-stu-id="f5e80-108">The animations may also be changed on the server-side</span></span>


## <a name="overview"></a><span data-ttu-id="f5e80-109">概述</span><span class="sxs-lookup"><span data-stu-id="f5e80-109">Overview</span></span>

<span data-ttu-id="f5e80-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="f5e80-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="f5e80-111">也可能在服务器端发生更改动画</span><span class="sxs-lookup"><span data-stu-id="f5e80-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="f5e80-112">步骤</span><span class="sxs-lookup"><span data-stu-id="f5e80-112">Steps</span></span>

<span data-ttu-id="f5e80-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="f5e80-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample1.aspx)]

<span data-ttu-id="f5e80-114">动画将应用于文本的外观如下所示的面板：</span><span class="sxs-lookup"><span data-stu-id="f5e80-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample2.aspx)]

<span data-ttu-id="f5e80-115">在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：</span><span class="sxs-lookup"><span data-stu-id="f5e80-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample3.css)]

<span data-ttu-id="f5e80-116">代码的其余部分在服务器端上运行，并且不使用标记;相反，它使用代码来创建`AnimationExtender`控件：</span><span class="sxs-lookup"><span data-stu-id="f5e80-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample4.aspx)]

<span data-ttu-id="f5e80-117">但是，该控件工具包当前不提供创建单个动画 API 访问权限。</span><span class="sxs-lookup"><span data-stu-id="f5e80-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="f5e80-118">不过，它是可以将设置`AnimationExtender`的动画属性设置为一个字符串，包含以声明方式分配动画时使用的 XML 标记。</span><span class="sxs-lookup"><span data-stu-id="f5e80-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="f5e80-119">若要创建的 XML 不能包含`<Animations>`元素可以使用.NET Framework 的 XML 支持，或在以下代码，只需提供的字符串：</span><span class="sxs-lookup"><span data-stu-id="f5e80-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample5.css)]

<span data-ttu-id="f5e80-120">最后，添加`AnimationExtender`控制转移到当前页上，在`<form runat="server">`元素，并确保动画包含并运行：</span><span class="sxs-lookup"><span data-stu-id="f5e80-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-html[Main](modifying-animations-from-the-server-side-cs/samples/sample6.html)]


<span data-ttu-id="f5e80-121">[![使用服务器端 C# /VB 代码创建动画](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f5e80-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)</span></span>

<span data-ttu-id="f5e80-122">使用服务器端 C# /VB 代码创建动画 ([单击此项可查看原尺寸图像](modifying-animations-from-the-server-side-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f5e80-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f5e80-123">[上一页](triggering-an-animation-in-another-control-cs.md)
> [下一页](executing-animations-using-client-side-code-cs.md)</span><span class="sxs-lookup"><span data-stu-id="f5e80-123">[Previous](triggering-an-animation-in-another-control-cs.md)
[Next](executing-animations-using-client-side-code-cs.md)</span></span>
