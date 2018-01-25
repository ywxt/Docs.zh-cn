---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb
title: "添加 GridView 列的复选框 (VB) |Microsoft 文档"
author: rick-anderson
description: "本教程讲述如何向 GridView 控件，以便用户提供选择 G.的多个行的一种直观方法中添加列的复选框..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/06/2007
ms.topic: article
ms.assetid: 39253d05-75c0-41c7-b9d4-a6c58ecf69ce
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: 4468f7e0c142fa432e58d4c686dd79d3b38612ad
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="adding-a-gridview-column-of-checkboxes-vb"></a><span data-ttu-id="822ed-103">添加 GridView 列的复选框 (VB)</span><span class="sxs-lookup"><span data-stu-id="822ed-103">Adding a GridView Column of Checkboxes (VB)</span></span>
====================
<span data-ttu-id="822ed-104">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="822ed-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="822ed-105">[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_VB.exe)或[下载 PDF](adding-a-gridview-column-of-checkboxes-vb/_static/datatutorial52vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="822ed-105">[Download Sample App](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_VB.exe) or [Download PDF](adding-a-gridview-column-of-checkboxes-vb/_static/datatutorial52vb1.pdf)</span></span>

> <span data-ttu-id="822ed-106">本教程讲述如何向 GridView 控件，以便用户提供选择多个行的 GridView 的一种直观方法中添加列的复选框。</span><span class="sxs-lookup"><span data-stu-id="822ed-106">This tutorial looks at how to add a column of check boxes to a GridView control to provide the user with an intuitive way of selecting multiple rows of the GridView.</span></span>


## <a name="introduction"></a><span data-ttu-id="822ed-107">介绍</span><span class="sxs-lookup"><span data-stu-id="822ed-107">Introduction</span></span>

<span data-ttu-id="822ed-108">在前面的教程中，我们将探讨如何将单选按钮的列添加到用于选择特定的记录 GridView。</span><span class="sxs-lookup"><span data-stu-id="822ed-108">In the preceding tutorial we examined how to add a column of radio buttons to the GridView for the purpose of selecting a particular record.</span></span> <span data-ttu-id="822ed-109">单选按钮的列是合适的用户界面，当用户从网格中进行选择最多一个项受到限制。</span><span class="sxs-lookup"><span data-stu-id="822ed-109">A column of radio buttons is a suitable user interface when the user is limited to choosing at most one item from the grid.</span></span> <span data-ttu-id="822ed-110">有时，但是，我们可能想要允许用户选取任意数目的网格中的项。</span><span class="sxs-lookup"><span data-stu-id="822ed-110">At times, however, we may want to allow the user to pick an arbitrary number of items from the grid.</span></span> <span data-ttu-id="822ed-111">基于 web 的电子邮件客户端，例如，通常显示的消息具有复选框的列的列表。</span><span class="sxs-lookup"><span data-stu-id="822ed-111">Web-based email clients, for example, typically display the list of messages with a column of checkboxes.</span></span> <span data-ttu-id="822ed-112">用户可以选择任意数目的消息，然后执行一些操作，如将电子邮件移动到另一个文件夹或删除它们。</span><span class="sxs-lookup"><span data-stu-id="822ed-112">The user can select an arbitrary number of messages and then perform some action, such as moving the emails to another folder or deleting them.</span></span>

<span data-ttu-id="822ed-113">在本教程中我们将了解如何添加复选框列以及如何确定哪些复选框已选中在回发时。</span><span class="sxs-lookup"><span data-stu-id="822ed-113">In this tutorial we will see how to add a column of checkboxes and how to determine what checkboxes were checked on postback.</span></span> <span data-ttu-id="822ed-114">具体而言，我们将生成的示例，类似于基于 web 的电子邮件客户端用户界面。</span><span class="sxs-lookup"><span data-stu-id="822ed-114">In particular, we'll build an example that closely mimics the web-based email client user interface.</span></span> <span data-ttu-id="822ed-115">我们的示例中将包括列出中的产品分页的 GridView`Products`数据库表具有一个复选框，在每个行 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="822ed-115">Our example will include a paged GridView listing the products in the `Products` database table with a checkbox in each row (see Figure 1).</span></span> <span data-ttu-id="822ed-116">删除所选产品按钮，单击时，将删除所选的这些产品。</span><span class="sxs-lookup"><span data-stu-id="822ed-116">A Delete Selected Products button, when clicked, will delete those products selected.</span></span>


<span data-ttu-id="822ed-117">[![每个产品行包含一个复选框](adding-a-gridview-column-of-checkboxes-vb/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="822ed-117">[![Each Product Row Includes a Checkbox](adding-a-gridview-column-of-checkboxes-vb/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image1.png)</span></span>

<span data-ttu-id="822ed-118">**图 1**： 每个产品行包含一个复选框 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="822ed-118">**Figure 1**: Each Product Row Includes a Checkbox ([Click to view full-size image](adding-a-gridview-column-of-checkboxes-vb/_static/image2.png))</span></span>


## <a name="step-1-adding-a-paged-gridview-that-lists-product-information"></a><span data-ttu-id="822ed-119">步骤 1： 添加一个分页的 GridView，列出产品信息</span><span class="sxs-lookup"><span data-stu-id="822ed-119">Step 1: Adding a Paged GridView that Lists Product Information</span></span>

<span data-ttu-id="822ed-120">我们担心添加复选框列之前，让 s 第一个专注于列出一个 GridView，支持分页中的产品。</span><span class="sxs-lookup"><span data-stu-id="822ed-120">Before we worry about adding a column of checkboxes, let s first focus on listing the products in a GridView that supports paging.</span></span> <span data-ttu-id="822ed-121">首先打开`CheckBoxField.aspx`页面`EnhancedGridView`文件夹，然后拖动一个 GridView 从工具箱中拖动到设计器中，设置其`ID`到`Products`。</span><span class="sxs-lookup"><span data-stu-id="822ed-121">Start by opening the `CheckBoxField.aspx` page in the `EnhancedGridView` folder and drag a GridView from the Toolbox onto the Designer, setting its `ID` to `Products`.</span></span> <span data-ttu-id="822ed-122">接下来，选择要绑定到名为新对象数据源的 GridView `ProductsDataSource`。</span><span class="sxs-lookup"><span data-stu-id="822ed-122">Next, choose to bind the GridView to a new ObjectDataSource named `ProductsDataSource`.</span></span> <span data-ttu-id="822ed-123">配置对象数据源以使用`ProductsBLL`类，调用`GetProducts()`方法以返回数据。</span><span class="sxs-lookup"><span data-stu-id="822ed-123">Configure the ObjectDataSource to use the `ProductsBLL` class, calling the `GetProducts()` method to return the data.</span></span> <span data-ttu-id="822ed-124">由于此 GridView 将为只读的在更新中，INSERT、 设置的下拉列表，并删除选项卡添加到 （无）。</span><span class="sxs-lookup"><span data-stu-id="822ed-124">Since this GridView will be read-only, set the drop-down lists in the UPDATE, INSERT, and DELETE tabs to (None) .</span></span>


<span data-ttu-id="822ed-125">[![创建名为 ProductsDataSource 新对象数据源](adding-a-gridview-column-of-checkboxes-vb/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="822ed-125">[![Create a New ObjectDataSource Named ProductsDataSource](adding-a-gridview-column-of-checkboxes-vb/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image3.png)</span></span>

<span data-ttu-id="822ed-126">**图 2**： 创建新对象数据源命名`ProductsDataSource`([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="822ed-126">**Figure 2**: Create a New ObjectDataSource Named `ProductsDataSource` ([Click to view full-size image](adding-a-gridview-column-of-checkboxes-vb/_static/image4.png))</span></span>


<span data-ttu-id="822ed-127">[![配置对象数据源检索数据使用 GetProducts() 方法](adding-a-gridview-column-of-checkboxes-vb/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="822ed-127">[![Configure the ObjectDataSource to Retrieve Data Using the GetProducts() Method](adding-a-gridview-column-of-checkboxes-vb/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image5.png)</span></span>

<span data-ttu-id="822ed-128">**图 3**： 配置检索数据使用 ObjectDataSource`GetProducts()`方法 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="822ed-128">**Figure 3**: Configure the ObjectDataSource to Retrieve Data Using the `GetProducts()` Method ([Click to view full-size image](adding-a-gridview-column-of-checkboxes-vb/_static/image6.png))</span></span>


<span data-ttu-id="822ed-129">[![在更新中，INSERT、 设置的下拉列表和删除选项卡到 （无）](adding-a-gridview-column-of-checkboxes-vb/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="822ed-129">[![Set the Drop-Down Lists in the UPDATE, INSERT, and DELETE Tabs to (None)](adding-a-gridview-column-of-checkboxes-vb/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image7.png)</span></span>

<span data-ttu-id="822ed-130">**图 4**： 设置的下拉列表中更新、 插入和删除选项卡为 （无） ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="822ed-130">**Figure 4**: Set the Drop-Down Lists in the UPDATE, INSERT, and DELETE Tabs to (None) ([Click to view full-size image](adding-a-gridview-column-of-checkboxes-vb/_static/image8.png))</span></span>


<span data-ttu-id="822ed-131">完成配置数据源向导后，Visual Studio 将自动创建 BoundColumns 和 CheckBoxColumn 与产品相关的数据字段。</span><span class="sxs-lookup"><span data-stu-id="822ed-131">After completing the Configure Data Source wizard, Visual Studio will automatically create BoundColumns and a CheckBoxColumn for the product-related data fields.</span></span> <span data-ttu-id="822ed-132">如我们未在前面的教程，请删除以外的所有`ProductName`， `CategoryName`，和`UnitPrice`BoundFields，并更改`HeaderText`到产品、 类别和价格的属性。</span><span class="sxs-lookup"><span data-stu-id="822ed-132">Like we did in the previous tutorial, remove all but the `ProductName`, `CategoryName`, and `UnitPrice` BoundFields, and change the `HeaderText` properties to Product, Category, and Price.</span></span> <span data-ttu-id="822ed-133">配置`UnitPrice`BoundField，以便其值设置为货币的格式。</span><span class="sxs-lookup"><span data-stu-id="822ed-133">Configure the `UnitPrice` BoundField so that its value is formatted as a currency.</span></span> <span data-ttu-id="822ed-134">此外配置 GridView 支持分页，通过检查从智能标记启用分页复选框。</span><span class="sxs-lookup"><span data-stu-id="822ed-134">Also configure the GridView to support paging by checking the Enable Paging checkbox from the smart tag.</span></span>

<span data-ttu-id="822ed-135">允许 s 还添加删除所选的产品的用户界面。</span><span class="sxs-lookup"><span data-stu-id="822ed-135">Let s also add the user interface for deleting the selected products.</span></span> <span data-ttu-id="822ed-136">添加按钮 Web 控件下 GridView，设置其`ID`到`DeleteSelectedProducts`及其`Text`删除所选产品的属性。</span><span class="sxs-lookup"><span data-stu-id="822ed-136">Add a Button Web control beneath the GridView, setting its `ID` to `DeleteSelectedProducts` and its `Text` property to Delete Selected Products.</span></span> <span data-ttu-id="822ed-137">而不是真正从数据库中删除产品，此示例中我们将只显示一条消息将被删除的产品。</span><span class="sxs-lookup"><span data-stu-id="822ed-137">Rather than actually deleting products from the database, for this example we'll just display a message stating the products that would have been deleted.</span></span> <span data-ttu-id="822ed-138">若要适应这种情况，请添加标签 Web 控件在按钮下方。</span><span class="sxs-lookup"><span data-stu-id="822ed-138">To accommodate this, add a Label Web control beneath the Button.</span></span> <span data-ttu-id="822ed-139">将其 ID 设置为`DeleteResults`，清除出其`Text`属性，并设置其`Visible`和`EnableViewState`属性设置为`False`。</span><span class="sxs-lookup"><span data-stu-id="822ed-139">Set its ID to `DeleteResults`, clear out its `Text` property, and set its `Visible` and `EnableViewState` properties to `False`.</span></span>

<span data-ttu-id="822ed-140">进行这些更改后，应类似于以下的 GridView、 ObjectDataSource、 按钮和标签 s 声明性标记：</span><span class="sxs-lookup"><span data-stu-id="822ed-140">After making these changes, the GridView, ObjectDataSource, Button, and Label s declarative markup should similar to the following:</span></span>


[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample1.aspx)]

<span data-ttu-id="822ed-141">花些时间查看浏览器中的页 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="822ed-141">Take a moment to view the page in a browser (see Figure 5).</span></span> <span data-ttu-id="822ed-142">此时应看到名称、 类别和的前 10 个产品的价格。</span><span class="sxs-lookup"><span data-stu-id="822ed-142">At this point you should see the name, category, and price of the first ten products.</span></span>


<span data-ttu-id="822ed-143">[![列出名称、 类别和第十个产品价格](adding-a-gridview-column-of-checkboxes-vb/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="822ed-143">[![The Name, Category, and Price of the First Ten Products are Listed](adding-a-gridview-column-of-checkboxes-vb/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image9.png)</span></span>

<span data-ttu-id="822ed-144">**图 5**： 列出名称、 类别和第十个产品的价格 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="822ed-144">**Figure 5**: The Name, Category, and Price of the First Ten Products are Listed ([Click to view full-size image](adding-a-gridview-column-of-checkboxes-vb/_static/image10.png))</span></span>


## <a name="step-2-adding-a-column-of-checkboxes"></a><span data-ttu-id="822ed-145">步骤 2： 添加列的复选框</span><span class="sxs-lookup"><span data-stu-id="822ed-145">Step 2: Adding a Column of Checkboxes</span></span>

<span data-ttu-id="822ed-146">由于 ASP.NET 2.0 包括 CheckBoxField，有人可能认为，它无法用于向一个 GridView 中添加列的复选框。</span><span class="sxs-lookup"><span data-stu-id="822ed-146">Since ASP.NET 2.0 includes a CheckBoxField, one might think that it could be used to add a column of checkboxes to a GridView.</span></span> <span data-ttu-id="822ed-147">遗憾的是，程序不是这种情况，CheckBoxField 用于处理与布尔数据字段。</span><span class="sxs-lookup"><span data-stu-id="822ed-147">Unfortunately, that is not the case, as the CheckBoxField is designed to work with a Boolean data field.</span></span> <span data-ttu-id="822ed-148">也就是说，为了使用 CheckBoxField 我们必须指定其值参考来确定是否呈现的复选框已选中的基础数据字段。</span><span class="sxs-lookup"><span data-stu-id="822ed-148">That is, in order to use the CheckBoxField we must specify the underlying data field whose value is consulted to determine whether the rendered checkbox is checked.</span></span> <span data-ttu-id="822ed-149">我们无法使用 CheckBoxField 只包含未选中的复选框的列。</span><span class="sxs-lookup"><span data-stu-id="822ed-149">We cannot use the CheckBoxField to just include a column of unchecked checkboxes.</span></span>

<span data-ttu-id="822ed-150">相反，我们必须添加为 TemplateField 并添加复选框 Web 控件与其`ItemTemplate`。</span><span class="sxs-lookup"><span data-stu-id="822ed-150">Instead, we must add a TemplateField and add a CheckBox Web control to its `ItemTemplate`.</span></span> <span data-ttu-id="822ed-151">请继续并添加到 TemplateField `Products` GridView 并使其第一个 （最左侧） 字段。</span><span class="sxs-lookup"><span data-stu-id="822ed-151">Go ahead and add a TemplateField to the `Products` GridView and make it the first (far-left) field.</span></span> <span data-ttu-id="822ed-152">从 GridView s 智能标记中，单击编辑模板链接，然后将复选框 Web 控件拖到工具箱从`ItemTemplate`。</span><span class="sxs-lookup"><span data-stu-id="822ed-152">From the GridView s smart tag, click on the Edit Templates link and then drag a CheckBox Web control from the Toolbox into the `ItemTemplate`.</span></span> <span data-ttu-id="822ed-153">设置此复选框 s`ID`属性`ProductSelector`。</span><span class="sxs-lookup"><span data-stu-id="822ed-153">Set this CheckBox s `ID` property to `ProductSelector`.</span></span>


<span data-ttu-id="822ed-154">[![添加一个名为到 TemplateField 的 ItemTemplate ProductSelector 的复选框 Web 控件](adding-a-gridview-column-of-checkboxes-vb/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="822ed-154">[![Add a CheckBox Web Control Named ProductSelector to the TemplateField s ItemTemplate](adding-a-gridview-column-of-checkboxes-vb/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image11.png)</span></span>

<span data-ttu-id="822ed-155">**图 6**： 添加复选框 Web 控件命名为`ProductSelector`到 TemplateField s `ItemTemplate` ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="822ed-155">**Figure 6**: Add a CheckBox Web Control Named `ProductSelector` to the TemplateField s `ItemTemplate` ([Click to view full-size image](adding-a-gridview-column-of-checkboxes-vb/_static/image12.png))</span></span>


<span data-ttu-id="822ed-156">与添加 TemplateField 和复选框 Web 控件，每个行现在包括一个复选框。</span><span class="sxs-lookup"><span data-stu-id="822ed-156">With the TemplateField and CheckBox Web control added, each row now includes a checkbox.</span></span> <span data-ttu-id="822ed-157">图 7 显示此页上，在添加的 TemplateField 和复选框后，通过浏览器，查看时。</span><span class="sxs-lookup"><span data-stu-id="822ed-157">Figure 7 shows this page, when viewed through a browser, after the TemplateField and CheckBox have been added.</span></span>


<span data-ttu-id="822ed-158">[![每个产品行现在包含一个复选框](adding-a-gridview-column-of-checkboxes-vb/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="822ed-158">[![Each Product Row Now Includes a Checkbox](adding-a-gridview-column-of-checkboxes-vb/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image13.png)</span></span>

<span data-ttu-id="822ed-159">**图 7**： 每个产品行现在包含一个复选框 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="822ed-159">**Figure 7**: Each Product Row Now Includes a Checkbox ([Click to view full-size image](adding-a-gridview-column-of-checkboxes-vb/_static/image14.png))</span></span>


## <a name="step-3-determining-what-checkboxes-were-checked-on-postback"></a><span data-ttu-id="822ed-160">步骤 3： 确定哪些复选框在回发时签入</span><span class="sxs-lookup"><span data-stu-id="822ed-160">Step 3: Determining What Checkboxes Were Checked On Postback</span></span>

<span data-ttu-id="822ed-161">此时我们具有的复选框，但无法确定哪些复选框已选中在回发时的列。</span><span class="sxs-lookup"><span data-stu-id="822ed-161">At this point we have a column of checkboxes but no way to determine what checkboxes were checked on postback.</span></span> <span data-ttu-id="822ed-162">单击删除所选产品按钮后，不过，我们需要知道哪些复选框已选中状态，以便删除这些产品。</span><span class="sxs-lookup"><span data-stu-id="822ed-162">When the Delete Selected Products button is clicked, though, we need to know what checkboxes were checked in order to delete those products.</span></span>

<span data-ttu-id="822ed-163">GridView s [ `Rows`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx)提供对 GridView 中的数据行的访问。</span><span class="sxs-lookup"><span data-stu-id="822ed-163">The GridView s [`Rows` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx) provides access to the data rows in the GridView.</span></span> <span data-ttu-id="822ed-164">我们可以循环访问这些行，以编程方式访问复选框控件中，并请查阅其`Checked`属性来确定是否已选中的复选框。</span><span class="sxs-lookup"><span data-stu-id="822ed-164">We can iterate through these rows, programmatically access the CheckBox control, and then consult its `Checked` property to determine whether the CheckBox has been selected.</span></span>

<span data-ttu-id="822ed-165">创建的事件处理程序`DeleteSelectedProducts`按钮 Web 控件的`Click`事件并添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="822ed-165">Create an event handler for the `DeleteSelectedProducts` Button Web control s `Click` event and add the following code:</span></span>


[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample2.vb)]

<span data-ttu-id="822ed-166">`Rows`属性返回的集合`GridViewRow`实例该构成 GridView 的数据行。</span><span class="sxs-lookup"><span data-stu-id="822ed-166">The `Rows` property returns a collection of `GridViewRow` instances that makeup the GridView s data rows.</span></span> <span data-ttu-id="822ed-167">`For Each`此处循环枚举此集合。</span><span class="sxs-lookup"><span data-stu-id="822ed-167">The `For Each` loop here enumerates this collection.</span></span> <span data-ttu-id="822ed-168">每个`GridViewRow`对象，以编程方式使用访问行 s 复选框`row.FindControl("controlID")`。</span><span class="sxs-lookup"><span data-stu-id="822ed-168">For each `GridViewRow` object, the row s CheckBox is programmatically accessed using `row.FindControl("controlID")`.</span></span> <span data-ttu-id="822ed-169">如果选中该复选框，则行 s 相应`ProductID`从检索值`DataKeys`集合。</span><span class="sxs-lookup"><span data-stu-id="822ed-169">If the CheckBox is checked, the row s corresponding `ProductID` value is retrieved from the `DataKeys` collection.</span></span> <span data-ttu-id="822ed-170">在此练习中，我们只需显示一条信息性消息中的`DeleteResults`标签，尽管工作应用程序中我们 d 改为使调用`ProductsBLL`类的`DeleteProduct(productID)`方法。</span><span class="sxs-lookup"><span data-stu-id="822ed-170">In this exercise, we simply display an informative message in the `DeleteResults` Label, although in a working application we d instead make a call to the `ProductsBLL` class s `DeleteProduct(productID)` method.</span></span>

<span data-ttu-id="822ed-171">此事件处理程序添加后，单击删除所选产品按钮现在将显示`ProductID`的所选产品的 s。</span><span class="sxs-lookup"><span data-stu-id="822ed-171">With the addition of this event handler, clicking the Delete Selected Products button now displays the `ProductID` s of the selected products.</span></span>


<span data-ttu-id="822ed-172">[![单击删除所选产品按钮时列出所选产品 Productid](adding-a-gridview-column-of-checkboxes-vb/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="822ed-172">[![When the Delete Selected Products Button is Clicked the Selected Products ProductIDs are Listed](adding-a-gridview-column-of-checkboxes-vb/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image15.png)</span></span>

<span data-ttu-id="822ed-173">**图 8**： 时删除所选产品单击按钮选择产品`ProductID`列出 s ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="822ed-173">**Figure 8**: When the Delete Selected Products Button is Clicked the Selected Products `ProductID` s are Listed ([Click to view full-size image](adding-a-gridview-column-of-checkboxes-vb/_static/image16.png))</span></span>


## <a name="step-4-adding-check-all-and-uncheck-all-buttons"></a><span data-ttu-id="822ed-174">步骤 4： 添加选中所有并取消选中所有按钮</span><span class="sxs-lookup"><span data-stu-id="822ed-174">Step 4: Adding Check All and Uncheck All Buttons</span></span>

<span data-ttu-id="822ed-175">如果用户想要删除当前页面上的所有产品，它们必须检查每十个复选框。</span><span class="sxs-lookup"><span data-stu-id="822ed-175">If a user wants to delete all products on the current page, they must check each of the ten checkboxes.</span></span> <span data-ttu-id="822ed-176">我们可以帮助加快此过程通过添加检查所有按钮，单击时，在网格中选择所有复选框。</span><span class="sxs-lookup"><span data-stu-id="822ed-176">We can help expedite this process by adding a Check All button that, when clicked, selects all of the checkboxes in the grid.</span></span> <span data-ttu-id="822ed-177">取消选中所有按钮将都会同样有用。</span><span class="sxs-lookup"><span data-stu-id="822ed-177">An Uncheck All button would be equally helpful.</span></span>

<span data-ttu-id="822ed-178">将两个按钮 Web 控件添加到页上，将它们放置上方 GridView。</span><span class="sxs-lookup"><span data-stu-id="822ed-178">Add two Button Web controls to the page, placing them above the GridView.</span></span> <span data-ttu-id="822ed-179">设置第一个 s`ID`到`CheckAll`及其`Text`检查所有属性; 设置第二个 s`ID`到`UncheckAll`并将其`Text`取消选中所有属性。</span><span class="sxs-lookup"><span data-stu-id="822ed-179">Set the first one s `ID` to `CheckAll` and its `Text` property to Check All ; set the second one s `ID` to `UncheckAll` and its `Text` property to Uncheck All .</span></span>


[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample3.aspx)]

<span data-ttu-id="822ed-180">接下来，创建名为的代码隐藏类中的一种方法`ToggleCheckState(checkState)`，调用时，枚举`Products`GridView s`Rows`集合和设置每个复选框 s`Checked`属性与传递的值中*复选*参数。</span><span class="sxs-lookup"><span data-stu-id="822ed-180">Next, create a method in the code-behind class named `ToggleCheckState(checkState)` that, when invoked, enumerates the `Products` GridView s `Rows` collection and sets each CheckBox s `Checked` property to the value of the passed in *checkState* parameter.</span></span>


[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample4.vb)]

<span data-ttu-id="822ed-181">接下来，创建`Click`事件处理程序`CheckAll`和`UncheckAll`按钮。</span><span class="sxs-lookup"><span data-stu-id="822ed-181">Next, create `Click` event handlers for the `CheckAll` and `UncheckAll` buttons.</span></span> <span data-ttu-id="822ed-182">在`CheckAll`s 事件处理程序，只需调用`ToggleCheckState(True)`; 在`UncheckAll`，调用`ToggleCheckState(False)`。</span><span class="sxs-lookup"><span data-stu-id="822ed-182">In `CheckAll` s event handler, simply call `ToggleCheckState(True)`; in `UncheckAll`, call `ToggleCheckState(False)`.</span></span>


[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample5.vb)]

<span data-ttu-id="822ed-183">使用此代码中，单击全部检查按钮导致回发，并且检查所有 GridView 中的复选框。</span><span class="sxs-lookup"><span data-stu-id="822ed-183">With this code, clicking the Check All button causes a postback and checks all of the checkboxes in the GridView.</span></span> <span data-ttu-id="822ed-184">同样，单击取消选中所有，就会取消选择所有复选框。</span><span class="sxs-lookup"><span data-stu-id="822ed-184">Likewise, clicking Uncheck All unselects all checkboxes.</span></span> <span data-ttu-id="822ed-185">在选中全部检查按钮后，图 9 显示的屏幕。</span><span class="sxs-lookup"><span data-stu-id="822ed-185">Figure 9 shows the screen after the Check All button has been checked.</span></span>


<span data-ttu-id="822ed-186">[![单击全部按钮的检查选择所有复选框](adding-a-gridview-column-of-checkboxes-vb/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="822ed-186">[![Clicking the Check All Button Selects All Checkboxes](adding-a-gridview-column-of-checkboxes-vb/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image17.png)</span></span>

<span data-ttu-id="822ed-187">**图 9**： 单击检查所有按钮选择所有复选框 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="822ed-187">**Figure 9**: Clicking the Check All Button Selects All Checkboxes ([Click to view full-size image](adding-a-gridview-column-of-checkboxes-vb/_static/image18.png))</span></span>


> [!NOTE]
> <span data-ttu-id="822ed-188">当显示的列的复选框，选择或取消选择所有复选框的一种方法是通过一个标题行中的复选框。</span><span class="sxs-lookup"><span data-stu-id="822ed-188">When displaying a column of checkboxes, one approach for selecting or unselecting all of the checkboxes is through a checkbox in the header row.</span></span> <span data-ttu-id="822ed-189">此外，当前选中所有/取消选中所有实现都需要回发。</span><span class="sxs-lookup"><span data-stu-id="822ed-189">Moreover, the current Check All / Uncheck All implementation requires a postback.</span></span> <span data-ttu-id="822ed-190">复选框可以选中或取消选中后，但是，完全通过客户端脚本，从而提供 snappier 的用户体验。</span><span class="sxs-lookup"><span data-stu-id="822ed-190">The checkboxes can be checked or unchecked, however, entirely through client-side script, thereby providing a snappier user experience.</span></span> <span data-ttu-id="822ed-191">若要了解详细信息，以及使用客户端技术的讨论中使用的所有检查和取消选中所有的标头行复选框签出[检查 GridView 使用客户端脚本和选中所有复选框中的所有复选框](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx)。</span><span class="sxs-lookup"><span data-stu-id="822ed-191">To explore using a header row checkbox for Check All and Uncheck All in detail, along with a discussion on using client-side techniques, check out [Checking All CheckBoxes in a GridView Using Client-Side Script and a Check All CheckBox](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx).</span></span>


## <a name="summary"></a><span data-ttu-id="822ed-192">摘要</span><span class="sxs-lookup"><span data-stu-id="822ed-192">Summary</span></span>

<span data-ttu-id="822ed-193">在需要使用户可以从在继续之前 GridView 选择任意数目的行的情况下，添加复选框列是一个选项。</span><span class="sxs-lookup"><span data-stu-id="822ed-193">In cases where you need to let users choose an arbitrary number of rows from a GridView before proceeding, adding a column of checkboxes is one option.</span></span> <span data-ttu-id="822ed-194">正如我们在本教程中看到的包括在 GridView 的复选框的列时，需要添加与复选框 Web 控件 TemplateField。</span><span class="sxs-lookup"><span data-stu-id="822ed-194">As we saw in this tutorial, including a column of checkboxes in the GridView entails adding a TemplateField with a CheckBox Web control.</span></span> <span data-ttu-id="822ed-195">通过使用 Web 控件 （而不是像前面的教程，请将标记注入直接到该模板后，） ASP.NET 自动会记住复选框已和未签跨回发。</span><span class="sxs-lookup"><span data-stu-id="822ed-195">By using a Web control (versus injecting markup directly into the template, as we did in the previous tutorial) ASP.NET automatically remembers what CheckBoxes were and were not checked across postback.</span></span> <span data-ttu-id="822ed-196">我们可以以编程方式访问中的复选框代码来确定是否检查一个给定的复选框，或更改的选中的状态。</span><span class="sxs-lookup"><span data-stu-id="822ed-196">We can also programmatically access the CheckBoxes in code to determine whether a given CheckBox is checked, or to chnage the checked state.</span></span>

<span data-ttu-id="822ed-197">本教程和最后一个认为将行选择器列添加到 GridView。</span><span class="sxs-lookup"><span data-stu-id="822ed-197">This tutorial and the last one looked at adding a row selector column to the GridView.</span></span> <span data-ttu-id="822ed-198">在我们的下一步教程中，我们将查看如何操作，请通过执行少量工作，我们可以插入将功能添加到 GridView。</span><span class="sxs-lookup"><span data-stu-id="822ed-198">In our next tutorial we'll examine how, with a bit of work, we can add inserting capabilities to the GridView.</span></span>

<span data-ttu-id="822ed-199">尽情享受编程 ！</span><span class="sxs-lookup"><span data-stu-id="822ed-199">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="822ed-200">关于作者</span><span class="sxs-lookup"><span data-stu-id="822ed-200">About the Author</span></span>

<span data-ttu-id="822ed-201">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的七个 ASP/ASP.NET 书籍和的创始人[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年使用与 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="822ed-201">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="822ed-202">Scott 的作用是作为独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="822ed-202">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="822ed-203">最新书籍是[ *Sam 教授自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="822ed-203">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="822ed-204">他可以达到在[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)或通过他的博客，其中可以找到在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="822ed-204">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="822ed-205">[上一页](adding-a-gridview-column-of-radio-buttons-vb.md)
[下一页](inserting-a-new-record-from-the-gridview-s-footer-vb.md)</span><span class="sxs-lookup"><span data-stu-id="822ed-205">[Previous](adding-a-gridview-column-of-radio-buttons-vb.md)
[Next](inserting-a-new-record-from-the-gridview-s-footer-vb.md)</span></span>
