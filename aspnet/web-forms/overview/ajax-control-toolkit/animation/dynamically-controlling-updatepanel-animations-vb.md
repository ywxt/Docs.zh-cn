---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: 动态控制 UpdatePanel 动画 (VB) |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。 内容...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: ff2853b4457a83a7367b4d1072d21929c40a3ed2
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871540"
---
<a name="dynamically-controlling-updatepanel-animations-vb"></a><span data-ttu-id="bcbd0-104">动态控制 UpdatePanel 动画 (VB)</span><span class="sxs-lookup"><span data-stu-id="bcbd0-104">Dynamically Controlling UpdatePanel Animations (VB)</span></span>
====================
<span data-ttu-id="bcbd0-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="bcbd0-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="bcbd0-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="bcbd0-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span></span>

> <span data-ttu-id="bcbd0-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="bcbd0-108">UpdatePanel 的内容，对于一个特殊的扩展程序添加存在很大程度依赖于动画 framework: UpdatePanelAnimation。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="bcbd0-109">它还可以与 UpdatePanel 触发器协作运行。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-109">It can also work together with UpdatePanel triggers.</span></span>


## <a name="overview"></a><span data-ttu-id="bcbd0-110">概述</span><span class="sxs-lookup"><span data-stu-id="bcbd0-110">Overview</span></span>

<span data-ttu-id="bcbd0-111">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="bcbd0-112">内容`UpdatePanel`，特殊的扩展程序存在很大程度依赖于动画 framework: `UpdatePanelAnimation`。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="bcbd0-113">它还可以一起使用`UpdatePanel`触发器。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="bcbd0-114">步骤</span><span class="sxs-lookup"><span data-stu-id="bcbd0-114">Steps</span></span>

<span data-ttu-id="bcbd0-115">第一步是像往常一样包括`ScriptManager`在页中，以便加载 ASP.NET AJAX 库，并可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="bcbd0-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

<span data-ttu-id="bcbd0-116">在此方案中动画将应用于当前时间的显示。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="bcbd0-117">此信息可写入标签使用`Page_Load()`方法，或 （为简单起见） 使用下面的内联代码：</span><span class="sxs-lookup"><span data-stu-id="bcbd0-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

<span data-ttu-id="bcbd0-118">此外，创建一个按钮以触发更新时间：</span><span class="sxs-lookup"><span data-stu-id="bcbd0-118">Also, a button to trigger updating the time is created:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

<span data-ttu-id="bcbd0-119">然后将此代码放入`<ContentTemplate>`部分`UpdatePanel`元素。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="bcbd0-120">面板的`UpdateMode`属性必须设置为`"Conditional"`，因为仅触发器可能会更新面板中的内容。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="bcbd0-121">在`<Triggers>`部分`UpdatePanel`，创建并绑定到一个异步回发的触发器`Click`该按钮的事件。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="bcbd0-122">因此，如果用户单击按钮，`UpdatePanel`进行刷新。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="bcbd0-123">下面是有关标记`UpdatePanel`控件：</span><span class="sxs-lookup"><span data-stu-id="bcbd0-123">Here is the markup for the `UpdatePanel` control:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

<span data-ttu-id="bcbd0-124">最后，`UpdatePanelAnimationExtender`必须配置： 设置`TargetControlID`属性面板的 ID 和定义中扩展器动画。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="bcbd0-125">在使淡出意义上，创建好 visual 主要侧重于更新的时间。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="bcbd0-126">扩展程序标记可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="bcbd0-126">Your extender markup may then look like this:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

<span data-ttu-id="bcbd0-127">在浏览器中运行该文件。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-127">Run the file in the browser.</span></span> <span data-ttu-id="bcbd0-128">只要你单击按钮时，当前时间是显示在面板中，始终为 1 秒的持续时间内淡入。</span><span class="sxs-lookup"><span data-stu-id="bcbd0-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>


<span data-ttu-id="bcbd0-129">[![当前时间淡入淡出](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bcbd0-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span></span>

<span data-ttu-id="bcbd0-130">当前时间淡入 ([单击以查看实际尺寸的图像](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="bcbd0-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="bcbd0-131">上一篇</span><span class="sxs-lookup"><span data-stu-id="bcbd0-131">Previous</span></span>](animating-an-updatepanel-control-vb.md)
