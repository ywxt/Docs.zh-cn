---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: 使用颜色选取器控件扩展程序 (VB) |Microsoft 文档
author: microsoft
description: 颜色选取器是客户端颜色选取功能提供 UI 弹出窗口控件中的 ASP.NET AJAX 扩展。 可以将它附加到任何 ASP.NET...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 3411119f85d7f5c26703b7df40cff24fdf30b81d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874510"
---
<a name="using-the-colorpicker-control-extender-vb"></a><span data-ttu-id="2647a-104">使用颜色选取器控件扩展程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="2647a-104">Using the ColorPicker Control Extender (VB)</span></span>
====================
<span data-ttu-id="2647a-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2647a-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="2647a-106">颜色选取器是客户端颜色选取功能提供 UI 弹出窗口控件中的 ASP.NET AJAX 扩展。</span><span class="sxs-lookup"><span data-stu-id="2647a-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="2647a-107">可以将它附加到任何 ASP.NET 文本框控件。</span><span class="sxs-lookup"><span data-stu-id="2647a-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="2647a-108">它。</span><span class="sxs-lookup"><span data-stu-id="2647a-108">It.</span></span>


<span data-ttu-id="2647a-109">本教程旨在说明如何使用 AJAX 控件工具包颜色选取器控件扩展程序。</span><span class="sxs-lookup"><span data-stu-id="2647a-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="2647a-110">颜色选取器控件扩展程序显示弹出对话框中，可用于选择一种颜色。</span><span class="sxs-lookup"><span data-stu-id="2647a-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="2647a-111">无论何时你想要提供一个直观的用户界面，供用户选择一个颜色时，颜色选取器非常有用。</span><span class="sxs-lookup"><span data-stu-id="2647a-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="2647a-112">扩展带颜色选取器控件扩展程序的 TextBox 控件</span><span class="sxs-lookup"><span data-stu-id="2647a-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="2647a-113">例如，假设你想要创建一个网站来使访问者可以创建自定义的业务卡。</span><span class="sxs-lookup"><span data-stu-id="2647a-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="2647a-114">访问者可以用于业务卡输入文本并选取的颜色。</span><span class="sxs-lookup"><span data-stu-id="2647a-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="2647a-115">列表 1 中的 ASP.NET 页面包含两个名为 txtCardText 和 txtCardColor 的文本框控件。</span><span class="sxs-lookup"><span data-stu-id="2647a-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="2647a-116">在提交表单时，将显示所选的值 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="2647a-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>


<span data-ttu-id="2647a-117">[![用于创建名片简单窗体](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2647a-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span></span>

<span data-ttu-id="2647a-118">**图 01**： 用于创建名片简单窗体 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="2647a-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image2.png))</span></span>


<span data-ttu-id="2647a-119">**Listing 1 - CreateCard.aspx**</span><span class="sxs-lookup"><span data-stu-id="2647a-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

<span data-ttu-id="2647a-120">窗体中列出 1 工作原理，但它不提供出色的用户体验。</span><span class="sxs-lookup"><span data-stu-id="2647a-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="2647a-121">用户必须在文本框中键入一种颜色。</span><span class="sxs-lookup"><span data-stu-id="2647a-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="2647a-122">如果用户想专用的颜色-例如，只需右明暗度的 pea 绿色-然后用户必须找出 HTML 颜色代码而无需任何帮助。</span><span class="sxs-lookup"><span data-stu-id="2647a-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="2647a-123">颜色选取器控件扩展程序可用于创建更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="2647a-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="2647a-124">颜色选取器显示颜色对话框时将焦点移到 TextBox 控件 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="2647a-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>


<span data-ttu-id="2647a-125">[![颜色选取器控件扩展](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2647a-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span></span>

<span data-ttu-id="2647a-126">**图 02**: 颜色选取器控件扩展程序 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="2647a-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image4.png))</span></span>


<span data-ttu-id="2647a-127">你需要完成两个步骤将颜色选取器控件扩展程序的窗体中列出 1 用于：</span><span class="sxs-lookup"><span data-stu-id="2647a-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="2647a-128">ScriptManager 控件添加到页面</span><span class="sxs-lookup"><span data-stu-id="2647a-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="2647a-129">颜色选取器控件扩展程序添加到页面</span><span class="sxs-lookup"><span data-stu-id="2647a-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="2647a-130">你可以使用颜色选取器之前，你必须将 ScriptManager 添加到你的页面。</span><span class="sxs-lookup"><span data-stu-id="2647a-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="2647a-131">添加 ScriptManager 的好时机是正下方打开服务器端&lt;窗体&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="2647a-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="2647a-132">你可以从 （ScriptManager 位于 AJAX Extensions 选项卡） 工具箱拖到页面上 ScriptManager。</span><span class="sxs-lookup"><span data-stu-id="2647a-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="2647a-133">或者，你可以开始服务器端窗体标记下，到源视图中键入以下标记：</span><span class="sxs-lookup"><span data-stu-id="2647a-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="2647a-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span><span class="sxs-lookup"><span data-stu-id="2647a-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="2647a-135">颜色选取器控件扩展程序添加到页面的最简单方法是在设计视图中。</span><span class="sxs-lookup"><span data-stu-id="2647a-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="2647a-136">如果鼠标悬停 txtCardColor 文本框中，智能任务选项将显示使用，你可以添加扩展程序 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="2647a-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="2647a-137">如果您选择此选项，则将显示扩展程序向导 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="2647a-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>


<span data-ttu-id="2647a-138">[![添加扩展程序](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="2647a-138">[![Adding an extender](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span></span>

<span data-ttu-id="2647a-139">**图 03**： 添加扩展程序 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="2647a-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image6.png))</span></span>


<span data-ttu-id="2647a-140">[![选择一个控件扩展程序添加的扩展程序向导](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="2647a-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="2647a-141">**图 04**： 选择一个控件扩展程序添加的扩展程序向导 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="2647a-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image8.png))</span></span>


<span data-ttu-id="2647a-142">你可以选择要扩展 txtCardColor 文本框中使用的颜色选取器扩展程序的颜色选取器扩展程序。</span><span class="sxs-lookup"><span data-stu-id="2647a-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="2647a-143">单击确定以关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="2647a-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="2647a-144">进行这些更改后，页上的源如下所示列出 2。</span><span class="sxs-lookup"><span data-stu-id="2647a-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="2647a-145">**列出 2-CreateCard.aspx （与颜色选取器）**</span><span class="sxs-lookup"><span data-stu-id="2647a-145">**Listing 2 - CreateCard.aspx (with ColorPicker)**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

<span data-ttu-id="2647a-146">请注意，页现在包含出现正下方的 txtCardColor TextBox 控件 ColorPickerExtender 控件。</span><span class="sxs-lookup"><span data-stu-id="2647a-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="2647a-147">ColorPickerExtender 控件扩展 txtCardColor 控件，使其显示颜色选取器对话框。</span><span class="sxs-lookup"><span data-stu-id="2647a-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="2647a-148">一个按钮用于启动颜色选取器对话框</span><span class="sxs-lookup"><span data-stu-id="2647a-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="2647a-149">颜色选取器扩展程序支持以下属性：</span><span class="sxs-lookup"><span data-stu-id="2647a-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="2647a-150">PopupButtonId-显示颜色选取器对话框页上的按钮的 ID。</span><span class="sxs-lookup"><span data-stu-id="2647a-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="2647a-151">PopupPosition-的位置，相对于目标控件，颜色选取器对话框。</span><span class="sxs-lookup"><span data-stu-id="2647a-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="2647a-152">可能的值是绝对、 Center、 BottomLeft、 BottomRight、、 左边框、 右上边框、 右、 和 （默认值为 BottomLeft） 的左侧。</span><span class="sxs-lookup"><span data-stu-id="2647a-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="2647a-153">SampleControlId-显示所选的颜色的控件的 ID。</span><span class="sxs-lookup"><span data-stu-id="2647a-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="2647a-154">SelectedColor-选定颜色选取器的初始颜色。</span><span class="sxs-lookup"><span data-stu-id="2647a-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="2647a-155">这些属性可用于自定义颜色选取器对话框的显示方式以及所选的颜色的显示方式。</span><span class="sxs-lookup"><span data-stu-id="2647a-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="2647a-156">中列出的 3 页说明了如何使用几个这些属性。</span><span class="sxs-lookup"><span data-stu-id="2647a-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="2647a-157">**Listing 3 - CreateCardButton.aspx**</span><span class="sxs-lookup"><span data-stu-id="2647a-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

<span data-ttu-id="2647a-158">中列出的 3 页包括取色按钮 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="2647a-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="2647a-159">单击此按钮时，颜色选取器对话框将出现上方文本框。</span><span class="sxs-lookup"><span data-stu-id="2647a-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="2647a-160">如果从对话框中选择一种颜色所选的颜色显示为 lblSample 标签控件的背景色。</span><span class="sxs-lookup"><span data-stu-id="2647a-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="2647a-161">颜色选取器 PopupButtonID 属性用于将选择颜色按钮的颜色选取器扩展程序与相关联。</span><span class="sxs-lookup"><span data-stu-id="2647a-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="2647a-162">你提供 PopupButtonID 属性的值，颜色选取器对话框不会再出现目标控件有焦点。</span><span class="sxs-lookup"><span data-stu-id="2647a-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="2647a-163">你必须单击按钮以显示对话框。</span><span class="sxs-lookup"><span data-stu-id="2647a-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="2647a-164">SampleControlID 属性用于将显示颜色选取器与所选的颜色的控件相关联。</span><span class="sxs-lookup"><span data-stu-id="2647a-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="2647a-165">颜色选取器更改为当前所选颜色的此控件的背景色。</span><span class="sxs-lookup"><span data-stu-id="2647a-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>


<span data-ttu-id="2647a-166">[![显示具有一个按钮的颜色选取器对话框](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="2647a-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span></span>

<span data-ttu-id="2647a-167">**图 05**： 显示具有一个按钮的颜色选取器对话框 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="2647a-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image10.png))</span></span>


## <a name="summary"></a><span data-ttu-id="2647a-168">总结</span><span class="sxs-lookup"><span data-stu-id="2647a-168">Summary</span></span>

<span data-ttu-id="2647a-169">在本教程中，您学习了如何使用颜色选取器控件扩展程序显示弹出窗口颜色选取器对话框。</span><span class="sxs-lookup"><span data-stu-id="2647a-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="2647a-170">首先，我们探讨了如何才能显示对话框时焦点移动到文本框控件。</span><span class="sxs-lookup"><span data-stu-id="2647a-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="2647a-171">接下来，您学习了如何创建显示颜色选取器对话框，单击该按钮的按钮。</span><span class="sxs-lookup"><span data-stu-id="2647a-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2647a-172">上一篇</span><span class="sxs-lookup"><span data-stu-id="2647a-172">Previous</span></span>](using-the-colorpicker-control-extender-cs.md)
