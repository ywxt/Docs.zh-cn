---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
title: 使用 FormView 的模板 (VB) |Microsoft 文档
author: rick-anderson
description: 说明如何，与 FormView 不组成字段。 相反，使用模板呈现 FormView。 在本教程中，我们将检查使用 F....
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 67b25f4c-2823-42b6-b07d-1d650b3fd711
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
msc.type: authoredcontent
ms.openlocfilehash: 16293960f5d8758c93646844bd159547f5e0f38c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875144"
---
<a name="using-the-formviews-templates-vb"></a><span data-ttu-id="c7c88-105">使用 FormView 的模板 (VB)</span><span class="sxs-lookup"><span data-stu-id="c7c88-105">Using the FormView's Templates (VB)</span></span>
====================
<span data-ttu-id="c7c88-106">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="c7c88-106">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="c7c88-107">[下载示例应用程序](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_14_VB.exe)或[下载 PDF](using-the-formview-s-templates-vb/_static/datatutorial14vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="c7c88-107">[Download Sample App](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_14_VB.exe) or [Download PDF](using-the-formview-s-templates-vb/_static/datatutorial14vb1.pdf)</span></span>

> <span data-ttu-id="c7c88-108">说明如何，与 FormView 不组成字段。</span><span class="sxs-lookup"><span data-stu-id="c7c88-108">Unlike the DetailsView, the FormView is not composed of fields.</span></span> <span data-ttu-id="c7c88-109">相反，使用模板呈现 FormView。</span><span class="sxs-lookup"><span data-stu-id="c7c88-109">Instead, the FormView is rendered using templates.</span></span> <span data-ttu-id="c7c88-110">在本教程中我们将检查使用 FormView 控件呈现数据的不太严格显示。</span><span class="sxs-lookup"><span data-stu-id="c7c88-110">In this tutorial we'll examine using the FormView control to present a less rigid display of data.</span></span>


## <a name="introduction"></a><span data-ttu-id="c7c88-111">介绍</span><span class="sxs-lookup"><span data-stu-id="c7c88-111">Introduction</span></span>

<span data-ttu-id="c7c88-112">最后两个教程中我们已了解如何自定义使用 TemplateFields 的 GridView 和说明控件的输出。</span><span class="sxs-lookup"><span data-stu-id="c7c88-112">In the last two tutorials we saw how to customize the GridView and DetailsView controls' outputs using TemplateFields.</span></span> <span data-ttu-id="c7c88-113">TemplateFields 允许高度自定义的特定字段的内容，但最后的 GridView 和说明具有而是 boxy、 类似网格的外观。</span><span class="sxs-lookup"><span data-stu-id="c7c88-113">TemplateFields allow for the contents for a specific field to be highly customized, but in the end both the GridView and DetailsView have a rather boxy, grid-like appearance.</span></span> <span data-ttu-id="c7c88-114">很多情况下，此类的类似网格布局是理想的但有时需要更流畅、 不太严格的显示。</span><span class="sxs-lookup"><span data-stu-id="c7c88-114">For many scenarios such a grid-like layout is ideal, but at times a more fluid, less rigid display is needed.</span></span> <span data-ttu-id="c7c88-115">在显示一条记录，请使用 FormView 控件可能会出现此类的流畅的布局。</span><span class="sxs-lookup"><span data-stu-id="c7c88-115">When displaying a single record, such a fluid layout is possible using the FormView control.</span></span>

<span data-ttu-id="c7c88-116">说明如何，与 FormView 不组成字段。</span><span class="sxs-lookup"><span data-stu-id="c7c88-116">Unlike the DetailsView, the FormView is not composed of fields.</span></span> <span data-ttu-id="c7c88-117">无法将 BoundField 或 TemplateField 添加到 FormView。</span><span class="sxs-lookup"><span data-stu-id="c7c88-117">You can't add a BoundField or TemplateField to a FormView.</span></span> <span data-ttu-id="c7c88-118">相反，使用模板呈现 FormView。</span><span class="sxs-lookup"><span data-stu-id="c7c88-118">Instead, the FormView is rendered using templates.</span></span> <span data-ttu-id="c7c88-119">FormView 看作包含单个 TemplateField 说明如何控制。</span><span class="sxs-lookup"><span data-stu-id="c7c88-119">Think of the FormView as a DetailsView control that contains a single TemplateField.</span></span> <span data-ttu-id="c7c88-120">FormView 支持以下模板：</span><span class="sxs-lookup"><span data-stu-id="c7c88-120">The FormView supports the following templates:</span></span>

- <span data-ttu-id="c7c88-121">`ItemTemplate` 用于呈现特定的记录显示在 FormView</span><span class="sxs-lookup"><span data-stu-id="c7c88-121">`ItemTemplate` used to render the particular record displayed in the FormView</span></span>
- <span data-ttu-id="c7c88-122">`HeaderTemplate` 用于指定一个可选标头行</span><span class="sxs-lookup"><span data-stu-id="c7c88-122">`HeaderTemplate` used to specify an optional header row</span></span>
- <span data-ttu-id="c7c88-123">`FooterTemplate` 用于指定一个可选的页脚行</span><span class="sxs-lookup"><span data-stu-id="c7c88-123">`FooterTemplate` used to specify an optional footer row</span></span>
- <span data-ttu-id="c7c88-124">`EmptyDataTemplate` 当 FormView`DataSource`缺少任何记录，`EmptyDataTemplate`代替使用`ItemTemplate`来呈现控件的标记</span><span class="sxs-lookup"><span data-stu-id="c7c88-124">`EmptyDataTemplate` when the FormView's `DataSource` lacks any records, the `EmptyDataTemplate` is used in place of the `ItemTemplate` for rendering the control's markup</span></span>
- <span data-ttu-id="c7c88-125">`PagerTemplate` 可用于为已启用的分页的 FormViews 自定义分页接口</span><span class="sxs-lookup"><span data-stu-id="c7c88-125">`PagerTemplate` can be used to customize the paging interface for FormViews that have paging enabled</span></span>
- <span data-ttu-id="c7c88-126">`EditItemTemplate` / `InsertItemTemplate` 用于为支持此类功能的 FormViews 自定义的编辑界面或插入接口</span><span class="sxs-lookup"><span data-stu-id="c7c88-126">`EditItemTemplate` / `InsertItemTemplate` used to customize the editing interface or inserting interface for FormViews that support such functionality</span></span>

<span data-ttu-id="c7c88-127">在本教程中我们将检查使用 FormView 控件呈现以不太严格显示的产品。</span><span class="sxs-lookup"><span data-stu-id="c7c88-127">In this tutorial we'll examine using the FormView control to present a less rigid display of products.</span></span> <span data-ttu-id="c7c88-128">而不是使字段的名称、 类别、 供应商和等等，FormView 的`ItemTemplate`将显示使用的标头元素组合这些值和`<table>`（请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="c7c88-128">Rather than having fields for the name, category, supplier, and so on, the FormView's `ItemTemplate` will show these values using a combination of a header element and a `<table>` (see Figure 1).</span></span>


<span data-ttu-id="c7c88-129">[![FormView 中断的说明中所示类似网格布局](using-the-formview-s-templates-vb/_static/image2.png)](using-the-formview-s-templates-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c7c88-129">[![The FormView Breaks Out of the Grid-Like Layout Seen in the DetailsView](using-the-formview-s-templates-vb/_static/image2.png)](using-the-formview-s-templates-vb/_static/image1.png)</span></span>

<span data-ttu-id="c7c88-130">**图 1**: FormView 跳出 Grid-Like 布局看到说明如何在 ([单击以查看实际尺寸的图像](using-the-formview-s-templates-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c7c88-130">**Figure 1**: The FormView Breaks Out of the Grid-Like Layout Seen in the DetailsView ([Click to view full-size image](using-the-formview-s-templates-vb/_static/image3.png))</span></span>


## <a name="step-1-binding-the-data-to-the-formview"></a><span data-ttu-id="c7c88-131">步骤 1： 将数据绑定到 FormView</span><span class="sxs-lookup"><span data-stu-id="c7c88-131">Step 1: Binding the Data to the FormView</span></span>

<span data-ttu-id="c7c88-132">打开`FormView.aspx`页上，并将 FormView 拖到设计器工具箱。</span><span class="sxs-lookup"><span data-stu-id="c7c88-132">Open the `FormView.aspx` page and drag a FormView from the Toolbox onto the Designer.</span></span> <span data-ttu-id="c7c88-133">第一次添加 FormView 时它都显示为灰色的框中，指示我们的`ItemTemplate`需要。</span><span class="sxs-lookup"><span data-stu-id="c7c88-133">When first adding the FormView it appears as a gray box, instructing us that an `ItemTemplate` is needed.</span></span>


<span data-ttu-id="c7c88-134">[![要在设计器中呈现 FormView，直到提供 ItemTemplate](using-the-formview-s-templates-vb/_static/image5.png)](using-the-formview-s-templates-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c7c88-134">[![The FormView Cannot be Rendered in the Designer Until an ItemTemplate is Provided](using-the-formview-s-templates-vb/_static/image5.png)](using-the-formview-s-templates-vb/_static/image4.png)</span></span>

<span data-ttu-id="c7c88-135">**图 2**: FormView 无法在设计器直到呈现`ItemTemplate`提供 ([单击以查看实际尺寸的图像](using-the-formview-s-templates-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="c7c88-135">**Figure 2**: The FormView Cannot be Rendered in the Designer Until an `ItemTemplate` is Provided ([Click to view full-size image](using-the-formview-s-templates-vb/_static/image6.png))</span></span>


<span data-ttu-id="c7c88-136">`ItemTemplate`可以 （通过声明性语法） 手动创建，也可以自动创建通过将 FormView 绑定到数据源控件通过设计器。</span><span class="sxs-lookup"><span data-stu-id="c7c88-136">The `ItemTemplate` can be created by hand (through the declarative syntax) or can be auto-created by binding the FormView to a data source control through the Designer.</span></span> <span data-ttu-id="c7c88-137">此自动创建`ItemTemplate`包含，列表的名称的每个字段和标签控件的 HTML`Text`属性绑定到字段的值。</span><span class="sxs-lookup"><span data-stu-id="c7c88-137">This auto-created `ItemTemplate` contains HTML that lists the name of each field and a Label control whose `Text` property is bound to the field's value.</span></span> <span data-ttu-id="c7c88-138">此方法还自动-创建`InsertItemTemplate`和`EditItemTemplate`，这两种使用输入控件填充每个返回的数据源控件的数据字段。</span><span class="sxs-lookup"><span data-stu-id="c7c88-138">This approach also auto-creates an `InsertItemTemplate` and `EditItemTemplate`, both of which are populated with input controls for each of the data fields returned by the data source control.</span></span>

<span data-ttu-id="c7c88-139">如果你想要自动创建模板，从 FormView 的智能标记添加时，将调用新 ObjectDataSource 控件`ProductsBLL`类的`GetProducts()`方法。</span><span class="sxs-lookup"><span data-stu-id="c7c88-139">If you want to auto-create the template, from the FormView's smart tag add a new ObjectDataSource control that invokes the `ProductsBLL` class's `GetProducts()` method.</span></span> <span data-ttu-id="c7c88-140">这将创建与 FormView `ItemTemplate`， `InsertItemTemplate`，和`EditItemTemplate`。</span><span class="sxs-lookup"><span data-stu-id="c7c88-140">This will create a FormView with an `ItemTemplate`, `InsertItemTemplate`, and `EditItemTemplate`.</span></span> <span data-ttu-id="c7c88-141">从源视图中，删除`InsertItemTemplate`和`EditItemTemplate`编辑或尚未插入，因为我们不感兴趣创建 FormView 支持。</span><span class="sxs-lookup"><span data-stu-id="c7c88-141">From the Source view, remove the `InsertItemTemplate` and `EditItemTemplate` since we're not interested in creating a FormView that supports editing or inserting yet.</span></span> <span data-ttu-id="c7c88-142">下一步，清理中的标记`ItemTemplate`，因此，我们必须干净状态进行工作。</span><span class="sxs-lookup"><span data-stu-id="c7c88-142">Next, clear out the markup within the `ItemTemplate` so that we have a clean slate to work from.</span></span>

<span data-ttu-id="c7c88-143">如果中而不是所生成的生成`ItemTemplate`手动，你可以在其中添加和配置通过从工具箱中拖动到设计器拖动的对象数据源。</span><span class="sxs-lookup"><span data-stu-id="c7c88-143">If you'd rather build up the `ItemTemplate` manually, you can add and configure the ObjectDataSource by dragging it from the Toolbox onto the Designer.</span></span> <span data-ttu-id="c7c88-144">但是，不设置 FormView 的数据源从设计器。</span><span class="sxs-lookup"><span data-stu-id="c7c88-144">However, don't set the FormView's data source from the Designer.</span></span> <span data-ttu-id="c7c88-145">相反，请转到源视图，并手动设置 FormView`DataSourceID`属性`ID`ObjectDataSource 的值。</span><span class="sxs-lookup"><span data-stu-id="c7c88-145">Instead, go to the Source view and manually set the FormView's `DataSourceID` property to the `ID` value of the ObjectDataSource.</span></span> <span data-ttu-id="c7c88-146">接下来，手动添加`ItemTemplate`。</span><span class="sxs-lookup"><span data-stu-id="c7c88-146">Next, manually add the `ItemTemplate`.</span></span>

<span data-ttu-id="c7c88-147">无论使用哪种方法，您决定要执行，此时你 FormView 声明性标记应看到如下：</span><span class="sxs-lookup"><span data-stu-id="c7c88-147">Regardless of what approach you decided to take, at this point your FormView's declarative markup should look like:</span></span>


[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample1.aspx)]

<span data-ttu-id="c7c88-148">花一些时间来检查 FormView 的智能标记; 中的启用分页复选框这将添加`AllowPaging="True"`属性设为 FormView 的声明性语法。</span><span class="sxs-lookup"><span data-stu-id="c7c88-148">Take a moment to check the Enable Paging checkbox in the FormView's smart tag; this will add the `AllowPaging="True"` attribute to the FormView's declarative syntax.</span></span> <span data-ttu-id="c7c88-149">此外，还要设置`EnableViewState`属性设置为 False。</span><span class="sxs-lookup"><span data-stu-id="c7c88-149">Also, set the `EnableViewState` property to False.</span></span>

## <a name="step-2-defining-theitemtemplates-markup"></a><span data-ttu-id="c7c88-150">步骤 2： 定义`ItemTemplate`的标记</span><span class="sxs-lookup"><span data-stu-id="c7c88-150">Step 2: Defining the`ItemTemplate`'s Markup</span></span>

<span data-ttu-id="c7c88-151">与 FormView 绑定到 ObjectDataSource 控件以及配置以支持分页，我们已准备好指定的内容`ItemTemplate`。</span><span class="sxs-lookup"><span data-stu-id="c7c88-151">With the FormView bound to the ObjectDataSource control and configured to support paging we're ready to specify the content for the `ItemTemplate`.</span></span> <span data-ttu-id="c7c88-152">对于本教程，让我们具有该产品的名称显示在`<h3>`标题。</span><span class="sxs-lookup"><span data-stu-id="c7c88-152">For this tutorial, let's have the product's name displayed in an `<h3>` heading.</span></span> <span data-ttu-id="c7c88-153">接下来，让我们使用 HTML`<table>`在四个列表，其中第一个和第三个列则列出的属性名称，第二个和第四个列表及其值中显示剩余的产品属性。</span><span class="sxs-lookup"><span data-stu-id="c7c88-153">Following that, let's use an HTML `<table>` to display the remaining product properties in a four-column table where the first and third columns list the property names and the second and fourth list their values.</span></span>

<span data-ttu-id="c7c88-154">可以通过在设计器中的 FormView 的模板编辑界面中输入或通过声明性语法手动输入此标记。</span><span class="sxs-lookup"><span data-stu-id="c7c88-154">This markup can be entered in through the FormView's template editing interface in the Designer or entered manually through the declarative syntax.</span></span> <span data-ttu-id="c7c88-155">使用模板时通常找到它直接使用声明性语法，但可随意使用你最熟悉的无论技术更快。</span><span class="sxs-lookup"><span data-stu-id="c7c88-155">When working with templates I typically find it quicker to work directly with the declarative syntax, but feel free to use whatever technique you're most comfortable with.</span></span>

<span data-ttu-id="c7c88-156">以下标记显示 FormView 声明性标记后的`ItemTemplate`的结构已完成：</span><span class="sxs-lookup"><span data-stu-id="c7c88-156">The following markup shows the FormView declarative markup after the `ItemTemplate`'s structure has been completed:</span></span>


[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample2.aspx)]

<span data-ttu-id="c7c88-157">请注意，数据绑定语法中- `<%# Eval("ProductName") %>`，对于示例可以直接注入模板的输出。</span><span class="sxs-lookup"><span data-stu-id="c7c88-157">Notice that the databinding syntax - `<%# Eval("ProductName") %>`, for example can be injected directly into the template's output.</span></span> <span data-ttu-id="c7c88-158">也就是说，它需要将分配给的标签控件`Text`属性。</span><span class="sxs-lookup"><span data-stu-id="c7c88-158">That is, it need not be assigned to a Label control's `Text` property.</span></span> <span data-ttu-id="c7c88-159">例如，我们具有`ProductName`中显示值`<h3>`元素使用`<h3><%# Eval("ProductName") %></h3>`，这对于产品牛奶将呈现为`<h3>Chai</h3>`。</span><span class="sxs-lookup"><span data-stu-id="c7c88-159">For example, we have the `ProductName` value displayed in an `<h3>` element using `<h3><%# Eval("ProductName") %></h3>`, which for the product Chai will render as `<h3>Chai</h3>`.</span></span>

<span data-ttu-id="c7c88-160">`ProductPropertyLabel`和`ProductPropertyValue`CSS 类用于指定样式的产品属性名称和中的值`<table>`。</span><span class="sxs-lookup"><span data-stu-id="c7c88-160">The `ProductPropertyLabel` and `ProductPropertyValue` CSS classes are used for specifying the style of the product property names and values in the `<table>`.</span></span> <span data-ttu-id="c7c88-161">在中定义这些 CSS 类`Styles.css`和会导致属性名称是加粗和右对齐，并添加到属性值填充的权限。</span><span class="sxs-lookup"><span data-stu-id="c7c88-161">These CSS classes are defined in `Styles.css` and cause the property names to be bold and right-aligned and add a right padding to the property values.</span></span>

<span data-ttu-id="c7c88-162">因为不不存在任何 CheckBoxFields 附带 FormView，为了显示`Discontinued`值作为一个复选框中，我们必须添加自己的复选框控件。</span><span class="sxs-lookup"><span data-stu-id="c7c88-162">Since there are no CheckBoxFields available with the FormView, in order to show the `Discontinued` value as a checkbox we must add our own CheckBox control.</span></span> <span data-ttu-id="c7c88-163">`Enabled`属性设置为 False，使其成为只读的并复选框的`Checked`属性绑定到的值`Discontinued`数据字段。</span><span class="sxs-lookup"><span data-stu-id="c7c88-163">The `Enabled` property is set to False, making it read-only, and the CheckBox's `Checked` property is bound to the value of the `Discontinued` data field.</span></span>

<span data-ttu-id="c7c88-164">与`ItemTemplate`完成后，产品信息将显示在更流畅的方式。</span><span class="sxs-lookup"><span data-stu-id="c7c88-164">With the `ItemTemplate` complete, the product information is displayed in a much more fluid manner.</span></span> <span data-ttu-id="c7c88-165">说明如何将输出从最后一个教程 (图 3) 进行比较与 FormView 在本教程 (图 4) 中生成的输出。</span><span class="sxs-lookup"><span data-stu-id="c7c88-165">Compare the DetailsView output from the last tutorial (Figure 3) with the output generated by the FormView in this tutorial (Figure 4).</span></span>


<span data-ttu-id="c7c88-166">[![刚性说明如何输出](using-the-formview-s-templates-vb/_static/image8.png)](using-the-formview-s-templates-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c7c88-166">[![The Rigid DetailsView Output](using-the-formview-s-templates-vb/_static/image8.png)](using-the-formview-s-templates-vb/_static/image7.png)</span></span>

<span data-ttu-id="c7c88-167">**图 3**: 刚性说明如何输出 ([单击以查看实际尺寸的图像](using-the-formview-s-templates-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="c7c88-167">**Figure 3**: The Rigid DetailsView Output ([Click to view full-size image](using-the-formview-s-templates-vb/_static/image9.png))</span></span>


<span data-ttu-id="c7c88-168">[![流畅的 FormView 输出](using-the-formview-s-templates-vb/_static/image11.png)](using-the-formview-s-templates-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="c7c88-168">[![The Fluid FormView Output](using-the-formview-s-templates-vb/_static/image11.png)](using-the-formview-s-templates-vb/_static/image10.png)</span></span>

<span data-ttu-id="c7c88-169">**图 4**: 流体 FormView 输出 ([单击以查看实际尺寸的图像](using-the-formview-s-templates-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="c7c88-169">**Figure 4**: The Fluid FormView Output ([Click to view full-size image](using-the-formview-s-templates-vb/_static/image12.png))</span></span>


## <a name="summary"></a><span data-ttu-id="c7c88-170">总结</span><span class="sxs-lookup"><span data-stu-id="c7c88-170">Summary</span></span>

<span data-ttu-id="c7c88-171">虽然 GridView 和说明控件都有使用 TemplateFields 自定义其输出，同时仍以一种类似网格、 boxy 格式显示其数据。</span><span class="sxs-lookup"><span data-stu-id="c7c88-171">While the GridView and DetailsView controls can have their output customized using TemplateFields, both still present their data in a grid-like, boxy format.</span></span> <span data-ttu-id="c7c88-172">当需要显示单个记录这些时间使用不太严格的布局，FormView 是理想的选择。</span><span class="sxs-lookup"><span data-stu-id="c7c88-172">For those times when a single record needs to be shown using a less rigid layout, the FormView is an ideal choice.</span></span> <span data-ttu-id="c7c88-173">说明如何，如 FormView 呈现来自的单个记录其`DataSource`，但与说明如何将只需组成模板且不支持字段。</span><span class="sxs-lookup"><span data-stu-id="c7c88-173">Like the DetailsView, the FormView renders a single record from its `DataSource`, but unlike the DetailsView it is composed just of templates and does not support fields.</span></span>

<span data-ttu-id="c7c88-174">正如我们在本教程中看到的 FormView 时，可以更灵活的布局显示单个记录。</span><span class="sxs-lookup"><span data-stu-id="c7c88-174">As we saw in this tutorial, the FormView allows for a more flexible layout when displaying a single record.</span></span> <span data-ttu-id="c7c88-175">在将来我们将检查 DataList 和转发器控件，请提供相同级别的灵活性以作为 FormsView，但可以显示多个记录 （如 GridView) 的教程。</span><span class="sxs-lookup"><span data-stu-id="c7c88-175">In future tutorials we'll examine the DataList and Repeater controls, which provide the same level of flexibility as the FormsView, but are able to display multiple records (like the GridView).</span></span>

<span data-ttu-id="c7c88-176">尽情享受编程 ！</span><span class="sxs-lookup"><span data-stu-id="c7c88-176">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="c7c88-177">关于作者</span><span class="sxs-lookup"><span data-stu-id="c7c88-177">About the Author</span></span>

<span data-ttu-id="c7c88-178">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的七个 ASP/ASP.NET 书籍和的创始人[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年使用与 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="c7c88-178">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="c7c88-179">Scott 的作用是作为独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="c7c88-179">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="c7c88-180">最新书籍是[ *Sam 教授自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="c7c88-180">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="c7c88-181">他可以达到在[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)或通过他的博客，其中可以找到在[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="c7c88-181">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="c7c88-182">特别感谢</span><span class="sxs-lookup"><span data-stu-id="c7c88-182">Special Thanks To</span></span>

<span data-ttu-id="c7c88-183">本教程系列已由许多有用的审阅者评审。</span><span class="sxs-lookup"><span data-stu-id="c7c88-183">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="c7c88-184">本教程中的前导审阅者已 E.R.</span><span class="sxs-lookup"><span data-stu-id="c7c88-184">Lead reviewer for this tutorial was E.R.</span></span> <span data-ttu-id="c7c88-185">Gilmore。</span><span class="sxs-lookup"><span data-stu-id="c7c88-185">Gilmore.</span></span> <span data-ttu-id="c7c88-186">对感兴趣查看我即将到来的 MSDN 文章？</span><span class="sxs-lookup"><span data-stu-id="c7c88-186">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="c7c88-187">如果是这样，删除我一行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="c7c88-187">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c7c88-188">[上一页](using-templatefields-in-the-detailsview-control-vb.md)
> [下一页](displaying-summary-information-in-the-gridview-s-footer-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c7c88-188">[Previous](using-templatefields-in-the-detailsview-control-vb.md)
[Next](displaying-summary-information-in-the-gridview-s-footer-vb.md)</span></span>
