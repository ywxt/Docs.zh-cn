---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: 使用 ColorPicker 控件扩展程序 (VB) |Microsoft Docs
author: microsoft
description: 颜色选取器是客户端的颜色选择功能提供用户界面中的弹出控件的 ASP.NET AJAX 扩展程序。 可以将它附加到任何 ASP.NET...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 2fa3804411cb553de242a503f57e247efc990156
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824833"
---
<a name="using-the-colorpicker-control-extender-vb"></a><span data-ttu-id="b7c06-104">使用 ColorPicker 控件扩展程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="b7c06-104">Using the ColorPicker Control Extender (VB)</span></span>
====================
<span data-ttu-id="b7c06-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b7c06-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b7c06-106">颜色选取器是客户端的颜色选择功能提供用户界面中的弹出控件的 ASP.NET AJAX 扩展程序。</span><span class="sxs-lookup"><span data-stu-id="b7c06-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="b7c06-107">可以将它附加到任何 ASP.NET TextBox 控件。</span><span class="sxs-lookup"><span data-stu-id="b7c06-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="b7c06-108">它。</span><span class="sxs-lookup"><span data-stu-id="b7c06-108">It.</span></span>


<span data-ttu-id="b7c06-109">本教程的目的是说明如何使用 AJAX 控件工具包 ColorPicker 控件扩展程序。</span><span class="sxs-lookup"><span data-stu-id="b7c06-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="b7c06-110">ColorPicker 控件扩展程序显示弹出对话框中，可用于选择一种颜色。</span><span class="sxs-lookup"><span data-stu-id="b7c06-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="b7c06-111">只要您想要提供一个直观的用户界面，供用户选择一种颜色，颜色选取器非常有用。</span><span class="sxs-lookup"><span data-stu-id="b7c06-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="b7c06-112">扩展具有 ColorPicker 控件扩展程序的文本框控件</span><span class="sxs-lookup"><span data-stu-id="b7c06-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="b7c06-113">例如，假设你想要创建可使访问者可以创建自定义的业务卡的网站。</span><span class="sxs-lookup"><span data-stu-id="b7c06-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="b7c06-114">访问者可以为业务卡中输入的文本并选取的颜色。</span><span class="sxs-lookup"><span data-stu-id="b7c06-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="b7c06-115">列表 1 中的 ASP.NET 页包含两个名为 txtCardText 和 txtCardColor 的 TextBox 控件。</span><span class="sxs-lookup"><span data-stu-id="b7c06-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="b7c06-116">当用户提交窗体时，显示所选的值 （请参阅图 1）。</span><span class="sxs-lookup"><span data-stu-id="b7c06-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>


<span data-ttu-id="b7c06-117">[![用于创建名片的简单窗体](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b7c06-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span></span>

<span data-ttu-id="b7c06-118">**图 01**： 用于创建名片的简单窗体 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="b7c06-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image2.png))</span></span>


<span data-ttu-id="b7c06-119">**代码清单 1-CreateCard.aspx**</span><span class="sxs-lookup"><span data-stu-id="b7c06-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

<span data-ttu-id="b7c06-120">在列表 1 中的工作原理，但窗体不提供出色的用户体验。</span><span class="sxs-lookup"><span data-stu-id="b7c06-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="b7c06-121">用户必须键入到文本框的一种颜色。</span><span class="sxs-lookup"><span data-stu-id="b7c06-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="b7c06-122">如果用户想要的专用的颜色-例如，只是正确的峰值绿色-则为用户阴影必须弄清楚的 HTML 颜色代码而无需任何帮助。</span><span class="sxs-lookup"><span data-stu-id="b7c06-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="b7c06-123">ColorPicker 控件扩展程序可用于创建更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="b7c06-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="b7c06-124">颜色选取器时将焦点移到 TextBox 控件显示颜色对话框 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="b7c06-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>


<span data-ttu-id="b7c06-125">[![ColorPicker 控件扩展程序](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="b7c06-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span></span>

<span data-ttu-id="b7c06-126">**图 02**: ColorPicker 控件扩展程序 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="b7c06-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image4.png))</span></span>


<span data-ttu-id="b7c06-127">需要完成 ColorPicker 控件扩展程序中使用的窗体列表 1 中的两个步骤：</span><span class="sxs-lookup"><span data-stu-id="b7c06-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="b7c06-128">向页面添加一个 ScriptManager 控件</span><span class="sxs-lookup"><span data-stu-id="b7c06-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="b7c06-129">ColorPicker 控件扩展程序添加到页面</span><span class="sxs-lookup"><span data-stu-id="b7c06-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="b7c06-130">可以使用颜色选取器之前，你必须将 ScriptManager 添加到您的页面。</span><span class="sxs-lookup"><span data-stu-id="b7c06-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="b7c06-131">添加 ScriptManager 的好时机是在打开服务器端下方&lt;窗体&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="b7c06-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="b7c06-132">您可以将 ScriptManager 到绘图页上从工具箱 （ScriptManager 位于 AJAX 扩展选项卡下）。</span><span class="sxs-lookup"><span data-stu-id="b7c06-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="b7c06-133">或者，可以在服务器端窗体标记下打开到源视图键入以下标记：</span><span class="sxs-lookup"><span data-stu-id="b7c06-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="b7c06-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span><span class="sxs-lookup"><span data-stu-id="b7c06-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="b7c06-135">ColorPicker 控件扩展程序添加到页面的最简单方法是在设计视图中。</span><span class="sxs-lookup"><span data-stu-id="b7c06-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="b7c06-136">如果将鼠标悬停 txtCardColor 文本框中，智能任务选项会显示，用于启用你添加扩展器 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="b7c06-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="b7c06-137">如果选择此选项，则将显示扩展器向导 （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="b7c06-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>


<span data-ttu-id="b7c06-138">[![添加扩展器](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="b7c06-138">[![Adding an extender](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span></span>

<span data-ttu-id="b7c06-139">**图 03**： 添加扩展器 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="b7c06-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image6.png))</span></span>


<span data-ttu-id="b7c06-140">[![选择扩展程序控件扩展程序向导](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="b7c06-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="b7c06-141">**图 04**： 选择使用扩展器向导扩展程序控件 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="b7c06-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image8.png))</span></span>


<span data-ttu-id="b7c06-142">可以选择要扩展 txtCardColor 文本框使用颜色选取器扩展器的颜色选取器扩展程序。</span><span class="sxs-lookup"><span data-stu-id="b7c06-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="b7c06-143">单击确定以关闭该对话框。</span><span class="sxs-lookup"><span data-stu-id="b7c06-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="b7c06-144">进行这些更改后，页面的源如下所示代码清单 2。</span><span class="sxs-lookup"><span data-stu-id="b7c06-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="b7c06-145">**代码清单 2-CreateCard.aspx （使用颜色选取器）**</span><span class="sxs-lookup"><span data-stu-id="b7c06-145">**Listing 2 - CreateCard.aspx (with ColorPicker)**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

<span data-ttu-id="b7c06-146">请注意到该页面现在包含出现正下方的 txtCardColor TextBox 控件的 ColorPickerExtender 控件。</span><span class="sxs-lookup"><span data-stu-id="b7c06-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="b7c06-147">ColorPickerExtender 控件扩展 txtCardColor 控件，以便显示颜色选取器对话框。</span><span class="sxs-lookup"><span data-stu-id="b7c06-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="b7c06-148">使用一个按钮以启动颜色选取器对话框</span><span class="sxs-lookup"><span data-stu-id="b7c06-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="b7c06-149">颜色选取器扩展器支持以下属性：</span><span class="sxs-lookup"><span data-stu-id="b7c06-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="b7c06-150">PopupButtonId-显示颜色选取器对话框的页上的按钮的 ID。</span><span class="sxs-lookup"><span data-stu-id="b7c06-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="b7c06-151">PopupPosition-的位置，相对于目标控件，颜色选取器对话框。</span><span class="sxs-lookup"><span data-stu-id="b7c06-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="b7c06-152">可能的值为 Absolute、 Center、 BottomLeft、 BottomRight、 左边框、 TopRight，向右、 和左侧 （默认值为 BottomLeft）。</span><span class="sxs-lookup"><span data-stu-id="b7c06-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="b7c06-153">SampleControlId-显示所选的颜色的控件的 ID。</span><span class="sxs-lookup"><span data-stu-id="b7c06-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="b7c06-154">SelectedColor-选定颜色选取器的初始颜色。</span><span class="sxs-lookup"><span data-stu-id="b7c06-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="b7c06-155">这些属性可用于自定义颜色选取器对话框的显示方式和所选的颜色的显示方式。</span><span class="sxs-lookup"><span data-stu-id="b7c06-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="b7c06-156">列表 3 中的页说明了如何使用多个这些属性。</span><span class="sxs-lookup"><span data-stu-id="b7c06-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="b7c06-157">**代码清单 3-CreateCardButton.aspx**</span><span class="sxs-lookup"><span data-stu-id="b7c06-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

<span data-ttu-id="b7c06-158">列表 3 中的页包括选取颜色按钮 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="b7c06-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="b7c06-159">单击此按钮时，颜色选取器对话框将出现在文本框上方。</span><span class="sxs-lookup"><span data-stu-id="b7c06-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="b7c06-160">如果从对话框中选择一种颜色的所选的颜色显示为 lblSample 标签控件的背景色。</span><span class="sxs-lookup"><span data-stu-id="b7c06-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="b7c06-161">ColorPicker PopupButtonID 属性用于将选择颜色按钮与颜色选取器扩展程序相关联。</span><span class="sxs-lookup"><span data-stu-id="b7c06-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="b7c06-162">提供 PopupButtonID 属性的值，颜色选取器对话框不会再出现在目标控件有焦点。</span><span class="sxs-lookup"><span data-stu-id="b7c06-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="b7c06-163">您必须单击按钮以显示对话框。</span><span class="sxs-lookup"><span data-stu-id="b7c06-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="b7c06-164">SampleControlID 属性用于将显示颜色选取器与所选的颜色的控件相关联。</span><span class="sxs-lookup"><span data-stu-id="b7c06-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="b7c06-165">颜色选取器将此控件的背景色更改为当前选定的颜色。</span><span class="sxs-lookup"><span data-stu-id="b7c06-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>


<span data-ttu-id="b7c06-166">[![显示具有一个按钮的颜色选取器对话框](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="b7c06-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span></span>

<span data-ttu-id="b7c06-167">**图 05**： 显示颜色选取器对话框使用一个按钮 ([单击以查看实际尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="b7c06-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image10.png))</span></span>


## <a name="summary"></a><span data-ttu-id="b7c06-168">总结</span><span class="sxs-lookup"><span data-stu-id="b7c06-168">Summary</span></span>

<span data-ttu-id="b7c06-169">在本教程中，您学习了如何使用 ColorPicker 控件扩展程序显示弹出颜色选取器对话框。</span><span class="sxs-lookup"><span data-stu-id="b7c06-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="b7c06-170">首先，我们探讨了如何显示对话框时焦点移动到 TextBox 控件。</span><span class="sxs-lookup"><span data-stu-id="b7c06-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="b7c06-171">接下来，您学习了如何创建显示颜色选取器对话框，单击该按钮的按钮。</span><span class="sxs-lookup"><span data-stu-id="b7c06-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b7c06-172">上一篇</span><span class="sxs-lookup"><span data-stu-id="b7c06-172">Previous</span></span>](using-the-colorpicker-control-extender-cs.md)
