---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: 使用 AJAX 控件工具包控件和控件扩展 (C#) |Microsoft 文档
author: microsoft
description: 了解如何将 AJAX 控件工具包控件和扩展程序添加到 ASP.NET 页。
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 3d7cea2452db01ca116849ffb17631db3b935668
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a><span data-ttu-id="9d667-103">使用 AJAX 控件工具包控件和控件扩展 (C#)</span><span class="sxs-lookup"><span data-stu-id="9d667-103">Using AJAX Control Toolkit Controls and Control Extenders (C#)</span></span>
====================
<span data-ttu-id="9d667-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9d667-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="9d667-105">了解如何将 AJAX 控件工具包控件和扩展程序添加到 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="9d667-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>


<span data-ttu-id="9d667-106">AJAX 控件工具包中包含控件和控件扩展程序的集。</span><span class="sxs-lookup"><span data-stu-id="9d667-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="9d667-107">在此简易教程，您将学习如何将控件和控件扩展程序添加到 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="9d667-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9d667-108">有关安装 AJAX 控件工具包和将 AJAX 控件工具包添加到 Visual Studio/Visual Web Developer 工具箱中，说明，请参阅本教程[入门 AJAX 控件工具包](get-started-with-the-ajax-control-toolkit-cs.md)。</span><span class="sxs-lookup"><span data-stu-id="9d667-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).</span></span>


## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="9d667-109">使用 AJAX 控件工具包控件</span><span class="sxs-lookup"><span data-stu-id="9d667-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="9d667-110">AJAX 控件工具包控件的工作方式就像普通的 ASP.NET 控件一样。</span><span class="sxs-lookup"><span data-stu-id="9d667-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="9d667-111">你可以将控件从工具箱中拖动到 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="9d667-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="9d667-112">可以将控件添加到设计视图或源视图中的页面。</span><span class="sxs-lookup"><span data-stu-id="9d667-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="9d667-113">使用 AJAX 控件工具包中的控件时一个特殊的要求。</span><span class="sxs-lookup"><span data-stu-id="9d667-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="9d667-114">页面必须包含 ScriptManager 控件。</span><span class="sxs-lookup"><span data-stu-id="9d667-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="9d667-115">ScriptManager 控件负责包括所有必要 AJAX 控件工具包控件所需的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="9d667-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="9d667-116">例如，AJAX 控件工具包选项卡包括名为编辑器控件的控件。</span><span class="sxs-lookup"><span data-stu-id="9d667-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="9d667-117">此控件显示的丰富的 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="9d667-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="9d667-118">请按照下列步骤编辑器控件添加到页面：</span><span class="sxs-lookup"><span data-stu-id="9d667-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="9d667-119">创建一个名为 ShowEditor.aspx 的新 ASP.NET 页</span><span class="sxs-lookup"><span data-stu-id="9d667-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="9d667-120">在工具箱中选择 AJAX Extensions 选项卡下 ScriptManager 控件并将控件拖到该页面。</span><span class="sxs-lookup"><span data-stu-id="9d667-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="9d667-121">在工具箱中选择 AJAX 控件工具包选项卡下的编辑器控件并将控件拖动到该页面上 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="9d667-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="9d667-122">设计器应该如图 2 所示。</span><span class="sxs-lookup"><span data-stu-id="9d667-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="9d667-123">通过选择菜单选项来运行网站**调试、 启动调试**或按 F5 键。</span><span class="sxs-lookup"><span data-stu-id="9d667-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="9d667-124">你应看到图 3 中的页。</span><span class="sxs-lookup"><span data-stu-id="9d667-124">You should see the page in Figure 3.</span></span>


<span data-ttu-id="9d667-125">[![选择的 HTML 编辑器控件](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9d667-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span></span>

<span data-ttu-id="9d667-126">**图 01**： 选择的 HTML 编辑器控件 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="9d667-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span></span>


<span data-ttu-id="9d667-127">[![与 ScriptManager 和编辑控件的 visual Studio 设计器](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="9d667-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span></span>

<span data-ttu-id="9d667-128">**图 02**： 与 ScriptManager 和编辑控件的 Visual Studio 设计器 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="9d667-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span></span>


<span data-ttu-id="9d667-129">[![DisplayEditor.aspx 页](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="9d667-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span></span>

<span data-ttu-id="9d667-130">**图 03**: DisplayEditor.aspx 页 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="9d667-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span></span>


## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="9d667-131">使用 AJAX 控件工具包控件扩展程序</span><span class="sxs-lookup"><span data-stu-id="9d667-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="9d667-132">AJAX 控件工具包还包含的控件扩展程序。</span><span class="sxs-lookup"><span data-stu-id="9d667-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="9d667-133">顾名思义，一个控件扩展程序添加扩展现有控件的功能。</span><span class="sxs-lookup"><span data-stu-id="9d667-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="9d667-134">例如，ConfirmButton 控件扩展程序扩展标准的 ASP.NET 按钮控件。</span><span class="sxs-lookup"><span data-stu-id="9d667-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="9d667-135">扩展程序更改按钮控件的行为，以便当你单击它时，按钮将显示确认对话框。</span><span class="sxs-lookup"><span data-stu-id="9d667-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="9d667-136">控件扩展，就像的 AJAX 控件工具包控件，需要 ScriptManager 控件。</span><span class="sxs-lookup"><span data-stu-id="9d667-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="9d667-137">在开始使用的页中的控件扩展程序之前，你必须将 ScriptManager 控件添加到页。</span><span class="sxs-lookup"><span data-stu-id="9d667-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="9d667-138">请按照下列步骤，使用 ConfirmButton 控件扩展程序操作：</span><span class="sxs-lookup"><span data-stu-id="9d667-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="9d667-139">创建一个名为 ShowConfirmButton.aspx 的新 ASP.NET 页</span><span class="sxs-lookup"><span data-stu-id="9d667-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="9d667-140">将 ScriptManager 控件添加到页面中，通过将控件拖动到该页面上，从 AJAX Extensions 选项卡。</span><span class="sxs-lookup"><span data-stu-id="9d667-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="9d667-141">将一个标准按钮控件添加到页面中，通过在工具箱中拖动到设计器图面上拖动标准选项卡下的按钮。</span><span class="sxs-lookup"><span data-stu-id="9d667-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="9d667-142">单击**添加扩展程序**任务选项 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="9d667-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="9d667-143">在选择扩展程序对话框中，选择 ConfirmButtonExtender （请参见图 5），然后单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="9d667-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="9d667-144">在设计器中选择按钮控件和展开 Extender，Button1\_ConfirmButtonExtender 节点在属性窗口中的 （请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="9d667-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="9d667-145">将值分配*真正？*到 ConfirmText 属性。</span><span class="sxs-lookup"><span data-stu-id="9d667-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="9d667-146">通过选择菜单选项运行页面**调试、 启动调试**或按 F5 键。</span><span class="sxs-lookup"><span data-stu-id="9d667-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>


<span data-ttu-id="9d667-147">[![添加扩展程序任务选项](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="9d667-147">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span></span>

<span data-ttu-id="9d667-148">**图 04**: 添加的扩展程序任务选项 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="9d667-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span></span>


<span data-ttu-id="9d667-149">[![选择 ConfirmButton 控件扩展程序](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="9d667-149">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span></span>

<span data-ttu-id="9d667-150">**图 05**： 选择 ConfirmButton 控件扩展程序 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="9d667-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span></span>


<span data-ttu-id="9d667-151">[![设置 ConfirmButton 属性](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="9d667-151">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span></span>

<span data-ttu-id="9d667-152">**图 06**： 设置 ConfirmButton 属性 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="9d667-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span></span>


<span data-ttu-id="9d667-153">当该页打开时，你会看到一个按钮。</span><span class="sxs-lookup"><span data-stu-id="9d667-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="9d667-154">单击按钮时，获取确认对话框中图 7。</span><span class="sxs-lookup"><span data-stu-id="9d667-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>


<span data-ttu-id="9d667-155">[![显示确认对话框](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="9d667-155">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span></span>

<span data-ttu-id="9d667-156">**图 07**： 显示确认对话框中 ([单击以查看实际尺寸的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="9d667-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span></span>


<span data-ttu-id="9d667-157">请注意，你通常不要拖动一个控件扩展程序添加到页面。</span><span class="sxs-lookup"><span data-stu-id="9d667-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="9d667-158">相反，你使用**添加扩展程序**任务将扩展程序添加到你已添加到页上的控件的选项。</span><span class="sxs-lookup"><span data-stu-id="9d667-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="9d667-159">此外，请注意，你设置控件扩展程序属性通过打开要扩展控件的属性表。</span><span class="sxs-lookup"><span data-stu-id="9d667-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="9d667-160">可以由多个控件扩展扩展单个 ASP.NET 控件。</span><span class="sxs-lookup"><span data-stu-id="9d667-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="9d667-161">要扩展控件的属性表将列出所有与该控件关联的控件扩展程序。</span><span class="sxs-lookup"><span data-stu-id="9d667-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9d667-162">[上一页](get-started-with-the-ajax-control-toolkit-cs.md)
> [下一页](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span><span class="sxs-lookup"><span data-stu-id="9d667-162">[Previous](get-started-with-the-ajax-control-toolkit-cs.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span></span>
