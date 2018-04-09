---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: 修改动画从服务器端 (VB) |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。 动画也可能会...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: 2b9ce85fc5040b2318233b3c553c2cf53dd03555
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="modifying-animations-from-the-server-side-vb"></a><span data-ttu-id="902c2-104">修改动画从服务器端 (VB)</span><span class="sxs-lookup"><span data-stu-id="902c2-104">Modifying Animations From The Server Side (VB)</span></span>
====================
<span data-ttu-id="902c2-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="902c2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="902c2-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="902c2-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span></span>

> <span data-ttu-id="902c2-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="902c2-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="902c2-108">也可能在服务器端发生更改动画</span><span class="sxs-lookup"><span data-stu-id="902c2-108">The animations may also be changed on the server-side</span></span>


## <a name="overview"></a><span data-ttu-id="902c2-109">概述</span><span class="sxs-lookup"><span data-stu-id="902c2-109">Overview</span></span>

<span data-ttu-id="902c2-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="902c2-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="902c2-111">也可能在服务器端发生更改动画</span><span class="sxs-lookup"><span data-stu-id="902c2-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="902c2-112">步骤</span><span class="sxs-lookup"><span data-stu-id="902c2-112">Steps</span></span>

<span data-ttu-id="902c2-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载后，使其可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="902c2-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

<span data-ttu-id="902c2-114">动画将应用于如下所示的文本的一个面板中：</span><span class="sxs-lookup"><span data-stu-id="902c2-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

<span data-ttu-id="902c2-115">在关联 CSS 类中的面板，定义一种很好的背景色，并且还设置面板的宽度固定:</span><span class="sxs-lookup"><span data-stu-id="902c2-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

<span data-ttu-id="902c2-116">其余代码在服务器端上运行，并且不使用标记;相反，它使用代码来创建`AnimationExtender`控件：</span><span class="sxs-lookup"><span data-stu-id="902c2-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

<span data-ttu-id="902c2-117">但是，该控件工具包当前不提供的 API 访问权限，以创建单独的动画。</span><span class="sxs-lookup"><span data-stu-id="902c2-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="902c2-118">不过，它是可以设置`AnimationExtender`的动画属性设置为一个字符串包含以声明方式分配动画时使用的 XML 标记。</span><span class="sxs-lookup"><span data-stu-id="902c2-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="902c2-119">若要创建的 XML 不能包含`<Animations>`可以使用.NET Framework 的 XML 元素支持，或按照以下代码，只需提供的字符串：</span><span class="sxs-lookup"><span data-stu-id="902c2-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

<span data-ttu-id="902c2-120">最后，添加`AnimationExtender`内控制转移到当前页上，`<form runat="server">`元素，并确保动画附带，运行：</span><span class="sxs-lookup"><span data-stu-id="902c2-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]


<span data-ttu-id="902c2-121">[![使用服务器端 C# /VB 代码创建动画](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="902c2-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span></span>

<span data-ttu-id="902c2-122">使用服务器端 C# /VB 代码创建动画 ([单击以查看实际尺寸的图像](modifying-animations-from-the-server-side-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="902c2-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="902c2-123">[上一页](triggering-an-animation-in-another-control-vb.md)
> [下一页](executing-animations-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="902c2-123">[Previous](triggering-an-animation-in-another-control-vb.md)
[Next](executing-animations-using-client-side-code-vb.md)</span></span>
