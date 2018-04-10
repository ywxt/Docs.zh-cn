---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
title: 如何使用 ComboBox 控件？ (VB) | Microsoft Docs
author: microsoft
description: 组合框是一个文本框中的灵活性结合的用户可以从中选择的选项列表的 ASP.NET AJAX 控件。
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: e887e7b2-a6e7-4a28-a134-ba334494badb
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
msc.type: authoredcontent
ms.openlocfilehash: e42844e326cb190502a51c5a85195b4752d7e827
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="how-do-i-use-the-combobox-control-vb"></a><span data-ttu-id="db446-104">如何使用 ComboBox 控件？</span><span class="sxs-lookup"><span data-stu-id="db446-104">How do I use the ComboBox Control?</span></span> <span data-ttu-id="db446-105">(VB)</span><span class="sxs-lookup"><span data-stu-id="db446-105">(VB)</span></span>
====================
<span data-ttu-id="db446-106">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="db446-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="db446-107">组合框是一个文本框中的灵活性结合的用户可以从中选择的选项列表的 ASP.NET AJAX 控件。</span><span class="sxs-lookup"><span data-stu-id="db446-107">ComboBox is an ASP.NET AJAX control that combines the flexibility of a TextBox with a list of options from which users can choose.</span></span>


<span data-ttu-id="db446-108">本教程旨在说明 AJAX 控件工具包 ComboBox 控件。</span><span class="sxs-lookup"><span data-stu-id="db446-108">The goal of this tutorial is to explain the AJAX Control Toolkit ComboBox control.</span></span> <span data-ttu-id="db446-109">组合框的工作原理类似之间标准 ASP.NET DropDownList 控件和文本框控件的组合。</span><span class="sxs-lookup"><span data-stu-id="db446-109">The ComboBox works like a combination between a standard ASP.NET DropDownList control and a TextBox control.</span></span> <span data-ttu-id="db446-110">你可以从预先存在的项列表中选择或输入新的项目。</span><span class="sxs-lookup"><span data-stu-id="db446-110">You can either select from a pre-existing list of items or enter a new item.</span></span>

<span data-ttu-id="db446-111">组合框类似于记忆式键入功能控件扩展程序，但在不同的方案中使用的控件。</span><span class="sxs-lookup"><span data-stu-id="db446-111">The ComboBox is similar to the AutoComplete control extender, but the controls are used in different scenarios.</span></span> <span data-ttu-id="db446-112">记忆式键入功能扩展程序查询 web 服务以获取匹配项。</span><span class="sxs-lookup"><span data-stu-id="db446-112">The AutoComplete extender queries a web service to get matching entries.</span></span> <span data-ttu-id="db446-113">与此相反，组合框控件中，使用一组项的初始化。</span><span class="sxs-lookup"><span data-stu-id="db446-113">The ComboBox control, in contrast, is initialized with a set of items.</span></span> <span data-ttu-id="db446-114">使用自动完成扩展程序使意义时你正在使用大量数据 （数以百万计的汽车部件） 时使用组合框控件时有意义使用一小部分的数据 （数十个汽车部分）。</span><span class="sxs-lookup"><span data-stu-id="db446-114">Using the AutoComplete extender makes sense when you are working with a large set of data (millions of car parts) while using the ComboBox control makes sense when working with a small set of data (dozens of car parts).</span></span>

## <a name="selecting-from-a-static-list-of-items"></a><span data-ttu-id="db446-115">从静态的项列表中选择</span><span class="sxs-lookup"><span data-stu-id="db446-115">Selecting from a Static List of Items</span></span>

<span data-ttu-id="db446-116">允许 s 开头使用组合框控件的一个简单的示例。</span><span class="sxs-lookup"><span data-stu-id="db446-116">Let�s start with a simple sample of using the ComboBox control.</span></span> <span data-ttu-id="db446-117">假设你想要在下拉列表中显示的项的静态列表。</span><span class="sxs-lookup"><span data-stu-id="db446-117">Imagine that you want to display a static list of items in a dropdown list.</span></span> <span data-ttu-id="db446-118">但是，你想要使保持打开状态的列表并不完整的可能性。</span><span class="sxs-lookup"><span data-stu-id="db446-118">However, you want to leave open the possibility that the list is not complete.</span></span> <span data-ttu-id="db446-119">你想要允许用户输入到列表的自定义值。</span><span class="sxs-lookup"><span data-stu-id="db446-119">You want to allow a user to enter a custom value into the list.</span></span>

<span data-ttu-id="db446-120">我们将创建新的 ASP.NET Web 窗体页并在页中使用 ComboBox 控件。</span><span class="sxs-lookup"><span data-stu-id="db446-120">We�ll create a new ASP.NET Web Forms page and use the ComboBox control in the page.</span></span> <span data-ttu-id="db446-121">将新的 ASP.NET 页添加到你的项目，并切换到设计视图。</span><span class="sxs-lookup"><span data-stu-id="db446-121">Add the new ASP.NET page to your project and switch to Design view.</span></span>

<span data-ttu-id="db446-122">如果你想要在页中使用的组合框控件必须将 ScriptManager 控件添加到页。</span><span class="sxs-lookup"><span data-stu-id="db446-122">If you want to use the ComboBox control in the page then you must add a ScriptManager control to the page.</span></span> <span data-ttu-id="db446-123">从 AJAX Extensions 选项卡将 ScriptManager 控件拖动到设计器图面。</span><span class="sxs-lookup"><span data-stu-id="db446-123">Drag the ScriptManager control from beneath the AJAX Extensions tab onto the Designer surface.</span></span> <span data-ttu-id="db446-124">应在页; 的顶部添加 ScriptManager 控件将其添加下面打开服务器端的立即&lt;窗体&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="db446-124">You should add the ScriptManager control at the top of the page; you can add it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="db446-125">接下来，将 ComboBox 控件拖到该页面。</span><span class="sxs-lookup"><span data-stu-id="db446-125">Next, drag the ComboBox control onto the page.</span></span> <span data-ttu-id="db446-126">与其他 AJAX 控件工具包控件和控件扩展程序 （请参见图 1） 工具箱中，可以找到 ComboBox 控件。</span><span class="sxs-lookup"><span data-stu-id="db446-126">You can find the ComboBox control in the Toolbox with the other AJAX Control Toolkit controls and control extenders (see figure1).</span></span>


<span data-ttu-id="db446-127">[![用于创建名片简单窗体](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="db446-127">[![Simple form for creating a business card](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="db446-128">**图 01**： 从工具箱中选择的组合框控件 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="db446-128">**Figure 01**: Selecting the ComboBox control from the toolbox ([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image2.png))</span></span>


<span data-ttu-id="db446-129">我们将使用 ComboBox 控件以显示静态列表的选择。</span><span class="sxs-lookup"><span data-stu-id="db446-129">We�ll use the ComboBox control to display a static list of choices.</span></span> <span data-ttu-id="db446-130">用户可以从三个选项的列表中选择特定级别的其食品 spiciness： 轻微、 中型和作用 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="db446-130">The user can select a particular level of spiciness for their food from a list of three choices: Mild, Medium, and Hot (see Figure 2).</span></span>


<span data-ttu-id="db446-131">[![从静态的项列表中选择](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="db446-131">[![Selecting from a static list of items](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)</span></span>

<span data-ttu-id="db446-132">**图 02**： 从静态的项列表中选择 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="db446-132">**Figure 02**: Selecting from a static list of items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image4.png))</span></span>


<span data-ttu-id="db446-133">有两种方法，可以将这些选项添加到 ComboBox 控件。</span><span class="sxs-lookup"><span data-stu-id="db446-133">There are two ways that you can add these choices to the ComboBox control.</span></span> <span data-ttu-id="db446-134">首先，选择任务编辑选项选项，当鼠标悬停在设计视图中的控件和打开项编辑器 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="db446-134">First, you select the Edit Options task option when hovering your mouse over the control in Design view and open the Item Editor (see Figure 3).</span></span>


<span data-ttu-id="db446-135">[![编辑组合框项](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="db446-135">[![Editing ComboBox items](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)</span></span>

<span data-ttu-id="db446-136">**图 03**： 编辑组合框项 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="db446-136">**Figure 03**: Editing ComboBox items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image6.png))</span></span>


<span data-ttu-id="db446-137">第二个选项是添加到开始和结束之间的项列表&lt;asp: ComboBox&gt;源视图中的标记。</span><span class="sxs-lookup"><span data-stu-id="db446-137">The second option is to add the list of items in between the opening and closing &lt;asp:ComboBox&gt; tags in Source view.</span></span> <span data-ttu-id="db446-138">列表 1 中的页面包含更新组合框具有的项的列表。</span><span class="sxs-lookup"><span data-stu-id="db446-138">The page in Listing 1 contains the updated ComboBox that has the list of items.</span></span>

<span data-ttu-id="db446-139">**Listing 1 - Static.aspx**</span><span class="sxs-lookup"><span data-stu-id="db446-139">**Listing 1 - Static.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample1.aspx)]

<span data-ttu-id="db446-140">列出 1 中打开页面时，你可以从组合框中选择预先存在的选项之一。</span><span class="sxs-lookup"><span data-stu-id="db446-140">When you open the page in Listing 1, you can select one of the pre-existing options from the ComboBox.</span></span> <span data-ttu-id="db446-141">换而言之，组合框的工作方式与 DropDownList 控件。</span><span class="sxs-lookup"><span data-stu-id="db446-141">In other words, the ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="db446-142">但是，还必须输入 （例如，超级辣味） 现有列表中不是一个新选择的选项。</span><span class="sxs-lookup"><span data-stu-id="db446-142">However, you also have the option of entering a new choice (for example, Super Spicy) that is not in the existing list.</span></span> <span data-ttu-id="db446-143">因此，组合框还工作原理类似文本框控件。</span><span class="sxs-lookup"><span data-stu-id="db446-143">So, the ComboBox also works like a TextBox control.</span></span>

<span data-ttu-id="db446-144">无论是否选择预先存在的项，或输入自定义项，在提交窗体中，你的选择会显示标签控件中时。</span><span class="sxs-lookup"><span data-stu-id="db446-144">Regardless of whether you pick a pre-existing item or you enter a custom item, when you submit the form, your choice appears in the label control.</span></span> <span data-ttu-id="db446-145">当你将提交窗体上，btnSubmit\_单击处理程序执行，并更新标签 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="db446-145">When you submit the form, the btnSubmit\_Click handler executes and updates the label (see Figure 4).</span></span>


<span data-ttu-id="db446-146">[![显示选定的项](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="db446-146">[![Displaying the selected item](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)</span></span>

<span data-ttu-id="db446-147">**图 04**： 显示所选的项 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="db446-147">**Figure 04**: Displaying the selected item([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image8.png))</span></span>


<span data-ttu-id="db446-148">组合框用于检索选定的项，在提交窗体之后、 支持与 DropDownList 控件相同的属性：</span><span class="sxs-lookup"><span data-stu-id="db446-148">The ComboBox supports the same properties as the DropDownList control for retrieving the selected item after a form is submitted:</span></span>

- <span data-ttu-id="db446-149">SelectedItem.Text-显示选定项的文本属性的值。</span><span class="sxs-lookup"><span data-stu-id="db446-149">SelectedItem.Text - Displays the value of the Text property of the selected item.</span></span>
- <span data-ttu-id="db446-150">SelectedItem.Value-显示选定项的 Value 属性的值或显示到组合框中键入的文本。</span><span class="sxs-lookup"><span data-stu-id="db446-150">SelectedItem.Value - Displays the value of the Value property of the selected item or displays the text typed into the ComboBox.</span></span>
- <span data-ttu-id="db446-151">SelectedValue-与 SelectedItem.Value 相同，只不过此属性使您能够指定默认值 （初始） 选定的项。</span><span class="sxs-lookup"><span data-stu-id="db446-151">SelectedValue - Same as SelectedItem.Value except that this property enables you to specify the default (initial) selected item.</span></span>

<span data-ttu-id="db446-152">如果你键入自定义然后自定义选项在组合框选择分配给 SelectedItem.Text 和 SelectedItem.Value 属性。</span><span class="sxs-lookup"><span data-stu-id="db446-152">If you type a custom choice into the ComboBox then the custom choice is assigned to both the SelectedItem.Text and SelectedItem.Value properties.</span></span>

## <a name="selecting-the-list-of-items-from-the-database"></a><span data-ttu-id="db446-153">从数据库中选择的项的列表</span><span class="sxs-lookup"><span data-stu-id="db446-153">Selecting the List of Items from the Database</span></span>

<span data-ttu-id="db446-154">你可以从数据库中检索的组合框显示的项的列表。</span><span class="sxs-lookup"><span data-stu-id="db446-154">You can retrieve the list of items that the ComboBox displays from a database.</span></span> <span data-ttu-id="db446-155">例如，你可以将组合框绑定到 SqlDataSource 控件、 ObjectDataSource 控件、 LinqDataSource 或 EntityDataSource。</span><span class="sxs-lookup"><span data-stu-id="db446-155">For example, you can bind the ComboBox to a SqlDataSource control, an ObjectDataSource control, a LinqDataSource, or an EntityDataSource.</span></span>

<span data-ttu-id="db446-156">假设你想要在组合框中显示影片列表。</span><span class="sxs-lookup"><span data-stu-id="db446-156">Imagine that you want to display a list of movies in a ComboBox.</span></span> <span data-ttu-id="db446-157">你想要从电影数据库表中检索的影片列表。</span><span class="sxs-lookup"><span data-stu-id="db446-157">You want to retrieve the list of movies from the Movies database table.</span></span> <span data-ttu-id="db446-158">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="db446-158">Follow these steps:</span></span>

1. <span data-ttu-id="db446-159">创建一个名为 Movies.aspx 页</span><span class="sxs-lookup"><span data-stu-id="db446-159">Create a page named Movies.aspx</span></span>
2. <span data-ttu-id="db446-160">将 ScriptManager 控件添加到页面中，通过从 AJAX Extensions 选项卡下 ScriptManager 拖动工具箱拖到页中。</span><span class="sxs-lookup"><span data-stu-id="db446-160">Add a ScriptManager control to the page by dragging the ScriptManager from under the AJAX Extensions tab in the Toolbox onto the page.</span></span>
3. <span data-ttu-id="db446-161">将 ComboBox 控件添加到页面中，通过拖动到该页面上的组合框。</span><span class="sxs-lookup"><span data-stu-id="db446-161">Add a ComboBox control to the page by dragging the ComboBox onto the page.</span></span>
4. <span data-ttu-id="db446-162">在设计视图中，请将鼠标悬停 ComboBox 控件并选择**选择数据源**任务选项 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="db446-162">In Design view, hover your mouse over the ComboBox control and select the **Choose Data Source** task option (see Figure 5).</span></span> <span data-ttu-id="db446-163">数据源配置向导将启动。</span><span class="sxs-lookup"><span data-stu-id="db446-163">The Data Source Configuration Wizard is launched.</span></span>
5. <span data-ttu-id="db446-164">在**选择数据源**步骤中，选择&lt;新数据源&gt;选项。</span><span class="sxs-lookup"><span data-stu-id="db446-164">In the **Choose a Data Source** step, select the &lt;New data source�&gt; option.</span></span>
6. <span data-ttu-id="db446-165">在**选择数据源类型**步骤中，选择数据库。</span><span class="sxs-lookup"><span data-stu-id="db446-165">In the **Choose a Data Source Type** step, select Database.</span></span>
7. <span data-ttu-id="db446-166">在**选择你的数据连接**步骤中，选择你的数据库 (例如，MoviesDB.mdf)。</span><span class="sxs-lookup"><span data-stu-id="db446-166">In the **Choose Your Data Connection** step, select your database (for example, MoviesDB.mdf).</span></span>
8. <span data-ttu-id="db446-167">在**将连接字符串保存到应用程序配置文件**步骤中，选择此选项以保存你的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="db446-167">In the **Save the Connection String to the Application Configuration File** step, select the option to save your connection string.</span></span>
9. <span data-ttu-id="db446-168">在**配置 Select 语句**步骤，选择电影数据库表并选择所有列。</span><span class="sxs-lookup"><span data-stu-id="db446-168">In the **Configure the Select Statement** step, select the Movies database table and select all of the columns.</span></span>
10. <span data-ttu-id="db446-169">在**测试查询**步骤中，单击完成按钮。</span><span class="sxs-lookup"><span data-stu-id="db446-169">In the **Test Query** step, click the Finish button.</span></span>
11. <span data-ttu-id="db446-170">返回**选择数据源**步骤中，选择要显示的字段的标题列和数据的 Id 列字段 （请参见图）。</span><span class="sxs-lookup"><span data-stu-id="db446-170">Back in the **Choose Data Source** step, select the Title column for the field to display and the Id column for the data field (see Figure).</span></span>
12. <span data-ttu-id="db446-171">单击确定按钮以关闭向导。</span><span class="sxs-lookup"><span data-stu-id="db446-171">Click the OK button to close the wizard.</span></span>


<span data-ttu-id="db446-172">[![选择数据源](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="db446-172">[![Choosing a data source](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)</span></span>

<span data-ttu-id="db446-173">**图 05**： 选择数据源 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="db446-173">**Figure 05**: Choosing a data source([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image10.png))</span></span>


<span data-ttu-id="db446-174">[![选择数据的文本和值字段](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="db446-174">[![Choosing the data text and value fields](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)</span></span>

<span data-ttu-id="db446-175">**图 06**： 选择数据的文本和值字段 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="db446-175">**Figure 06**: Choosing the data text and value fields([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image12.png))</span></span>


<span data-ttu-id="db446-176">完成上述步骤后，组合框绑定到影片数据库表中表示电影 SqlDataSource 控件。</span><span class="sxs-lookup"><span data-stu-id="db446-176">After you complete the steps above, the ComboBox is bound to a SqlDataSource control that represents the movies from the Movies database table.</span></span> <span data-ttu-id="db446-177">页的源如下所示列出 2 （我清理格式设置得有点）。</span><span class="sxs-lookup"><span data-stu-id="db446-177">The source for the page looks like Listing 2 (I cleaned up the formatting a little bit).</span></span>

<span data-ttu-id="db446-178">**列出 2-Movies.aspx**</span><span class="sxs-lookup"><span data-stu-id="db446-178">**Listing 2 - Movies.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample2.aspx)]

<span data-ttu-id="db446-179">请注意，ComboBox 控件 SqlDataSource 控件所指向的 DataSourceID 属性。</span><span class="sxs-lookup"><span data-stu-id="db446-179">Notice that the ComboBox control has a DataSourceID property that points to the SqlDataSource control.</span></span> <span data-ttu-id="db446-180">当您在浏览器中打开页时，显示从数据库的影片列表 （请参阅图 7）。</span><span class="sxs-lookup"><span data-stu-id="db446-180">When you open the page in a browser, the list of movies from the database is displayed (see Figure 7).</span></span> <span data-ttu-id="db446-181">你可以任一选取一部电影，从列表或通过键入电影到组合框中输入新的影片。</span><span class="sxs-lookup"><span data-stu-id="db446-181">You can either a pick a movie from the list or enter a new movie by typing the movie into the ComboBox.</span></span>


<span data-ttu-id="db446-182">[![显示影片列表](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="db446-182">[![Displaying a list of movies](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)</span></span>

<span data-ttu-id="db446-183">**图 07**： 显示影片列表 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="db446-183">**Figure 07**: Displaying a list of movies([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image14.png))</span></span>


## <a name="setting-the-dropdownstyle"></a><span data-ttu-id="db446-184">设置 DropDownStyle</span><span class="sxs-lookup"><span data-stu-id="db446-184">Setting the DropDownStyle</span></span>

<span data-ttu-id="db446-185">组合框 DropDownStyle 属性可用于更改组合框的行为。</span><span class="sxs-lookup"><span data-stu-id="db446-185">You can use the ComboBox DropDownStyle property to change the behavior of the ComboBox.</span></span> <span data-ttu-id="db446-186">此属性接受那里可能的值：</span><span class="sxs-lookup"><span data-stu-id="db446-186">This property accepts there possible values:</span></span>

- <span data-ttu-id="db446-187">下拉列表中的 （默认值） 的组合框显示一个下拉列表列出当您单击的箭头，您可以输入自定义值。</span><span class="sxs-lookup"><span data-stu-id="db446-187">DropDown - (default value) The ComboBox displays a dropdown list when you click the arrow and you can enter a custom value.</span></span>
- <span data-ttu-id="db446-188">简单的组合框会自动显示一个下拉列表，你可以输入自定义值。</span><span class="sxs-lookup"><span data-stu-id="db446-188">Simple - The ComboBox displays a dropdown list automatically and you can enter a custom value.</span></span>
- <span data-ttu-id="db446-189">DropDownList-ComboBox 作用一样的 DropDownList 控件。</span><span class="sxs-lookup"><span data-stu-id="db446-189">DropDownList - The ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="db446-190">不同的下拉列表中之间和简单时显示的项的列表。</span><span class="sxs-lookup"><span data-stu-id="db446-190">The different between DropDown and Simple is when the list of items is displayed.</span></span> <span data-ttu-id="db446-191">对于简单，立即时将焦点移到组合框显示的列表。</span><span class="sxs-lookup"><span data-stu-id="db446-191">In the case of Simple, the list is displayed immediately when you move focus to the ComboBox.</span></span> <span data-ttu-id="db446-192">如果下拉列表中，必须单击该箭头可查看的项的列表。</span><span class="sxs-lookup"><span data-stu-id="db446-192">In the case of DropDown, you must click the arrow to see the list of items.</span></span>

<span data-ttu-id="db446-193">DropDownList 值将导致 ComboBox 控件，就像标准的 DropDownList 控件一样工作。</span><span class="sxs-lookup"><span data-stu-id="db446-193">The DropDownList value causes the ComboBox control to work just like a standard DropDownList control.</span></span> <span data-ttu-id="db446-194">但是，是一个重要的区别。</span><span class="sxs-lookup"><span data-stu-id="db446-194">However, there is an important difference here.</span></span> <span data-ttu-id="db446-195">控件将显示于前面遮挡它施加任何控制，因此，较旧版本的 Internet Explorer 将显示具有无限 z 索引的 DropDownList 控件。</span><span class="sxs-lookup"><span data-stu-id="db446-195">Older versions of Internet Explorer display a DropDownList control with an infinite z-index so the control will appear in front of any control placed in front of it.</span></span> <span data-ttu-id="db446-196">由于组合框上呈现 HTML &lt;div&gt;而不是 HTML 标记&lt;选择&gt;标记，组合框正确遵循 z 顺序。</span><span class="sxs-lookup"><span data-stu-id="db446-196">Because the ComboBox renders an HTML &lt;div&gt; tag instead of an HTML &lt;select&gt; tag, the ComboBox correctly respects z-ordering.</span></span>

## <a name="setting-the-autocompletemode"></a><span data-ttu-id="db446-197">设置 AutoCompleteMode</span><span class="sxs-lookup"><span data-stu-id="db446-197">Setting the AutoCompleteMode</span></span>

<span data-ttu-id="db446-198">组合框 AutoCompleteMode 属性用于指定当有人到组合框中键入文本时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="db446-198">You use the ComboBox AutoCompleteMode property to specify what happens when someone types text into the ComboBox.</span></span> <span data-ttu-id="db446-199">此属性接受以下可能值：</span><span class="sxs-lookup"><span data-stu-id="db446-199">This property accepts the following possible values:</span></span>

- <span data-ttu-id="db446-200">None-（默认值） 的组合框不提供任何自动完成行为。</span><span class="sxs-lookup"><span data-stu-id="db446-200">None - (default value) The ComboBox does not provide any auto-complete behavior.</span></span>
- <span data-ttu-id="db446-201">建议的组合框显示的列表，并会突出显示列表中的匹配项 （请参阅图 8）。</span><span class="sxs-lookup"><span data-stu-id="db446-201">Suggest - The ComboBox displays the list and it highlights the matching item in the list (see Figure 8).</span></span>
- <span data-ttu-id="db446-202">追加-组合框不会显示列表和追加的列表拖到键入的内容 （请参阅图 9） 的匹配项。</span><span class="sxs-lookup"><span data-stu-id="db446-202">Append - The ComboBox does not display the list and it appends the matching item from the list onto what you have typed (see Figure 9).</span></span>
- <span data-ttu-id="db446-203">SuggestAppend-ComboBox 同时显示的列表，并追加的列表拖到键入的内容 （请参阅图 10） 的匹配项。</span><span class="sxs-lookup"><span data-stu-id="db446-203">SuggestAppend - The ComboBox both displays the list and appends the matching item from the list onto what you have typed (see Figure 10).</span></span>


<span data-ttu-id="db446-204">[![组合框使建议](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="db446-204">[![The ComboBox makes a suggestion](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)</span></span>

<span data-ttu-id="db446-205">**图 08**: ComboBox 使建议 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="db446-205">**Figure 08**: The ComboBox makes a suggestion([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image16.png))</span></span>


<span data-ttu-id="db446-206">[![组合框将匹配的文本追加](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="db446-206">[![ComboBox appends matching text](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)</span></span>

<span data-ttu-id="db446-207">**图 09**: ComboBox 将匹配的文本追加 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="db446-207">**Figure 09**: ComboBox appends matching text([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image18.png))</span></span>


<span data-ttu-id="db446-208">[![组合框提供的建议，并追加](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="db446-208">[![The ComboBox suggests and appends](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)</span></span>

<span data-ttu-id="db446-209">**图 10**: 组合框提供的建议，并追加 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="db446-209">**Figure 10**: The ComboBox suggests and appends([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image20.png))</span></span>


## <a name="summary"></a><span data-ttu-id="db446-210">总结</span><span class="sxs-lookup"><span data-stu-id="db446-210">Summary</span></span>

<span data-ttu-id="db446-211">在本教程中，您学习了如何使用 ComboBox 控件来显示一组固定的项。</span><span class="sxs-lookup"><span data-stu-id="db446-211">In this tutorial, you learned how to use the ComboBox control to display a fixed set of items.</span></span> <span data-ttu-id="db446-212">我们将这两种到的项设置静态和到数据库表该组合框控件绑定。</span><span class="sxs-lookup"><span data-stu-id="db446-212">We bound the ComboBox control both to a static set of items and to a database table.</span></span> <span data-ttu-id="db446-213">最后，您学习了如何通过设置其 DropDownStyle 和 AutoCompleteMode 属性修改组合框的行为。</span><span class="sxs-lookup"><span data-stu-id="db446-213">Finally, you learned how to modify the behavior of the ComboBox by setting its DropDownStyle and AutoCompleteMode properties.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="db446-214">上一篇</span><span class="sxs-lookup"><span data-stu-id="db446-214">Previous</span></span>](how-do-i-use-the-combobox-control-cs.md)
