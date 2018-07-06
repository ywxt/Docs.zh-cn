---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb
title: 执行批量更新 (VB) |Microsoft Docs
author: rick-anderson
description: 了解如何创建完全编辑 DataList 的所有项处于编辑模式和其值可以通过单击全部更新按钮保存...
ms.author: aspnetcontent
ms.date: 10/30/2006
ms.assetid: 8dac22a7-91de-4e3b-888f-a4c438b03851
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb
msc.type: authoredcontent
ms.openlocfilehash: 6d6575e5f13441c38c5d7c74c8b5136a5206ffa9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803890"
---
<a name="performing-batch-updates-vb"></a><span data-ttu-id="15a5b-103">执行批量更新 (VB)</span><span class="sxs-lookup"><span data-stu-id="15a5b-103">Performing Batch Updates (VB)</span></span>
====================
<span data-ttu-id="15a5b-104">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="15a5b-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="15a5b-105">[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_VB.exe)或[下载 PDF](performing-batch-updates-vb/_static/datatutorial37vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="15a5b-105">[Download Sample App](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_VB.exe) or [Download PDF](performing-batch-updates-vb/_static/datatutorial37vb1.pdf)</span></span>

> <span data-ttu-id="15a5b-106">了解如何创建完全编辑 DataList 的所有项处于编辑模式，可以通过单击页上的"全部更新"按钮保存其值。</span><span class="sxs-lookup"><span data-stu-id="15a5b-106">Learn how to create a fully-editable DataList where all of its items are in edit mode and whose values can be saved by clicking an "Update All" button on the page.</span></span>


## <a name="introduction"></a><span data-ttu-id="15a5b-107">介绍</span><span class="sxs-lookup"><span data-stu-id="15a5b-107">Introduction</span></span>

<span data-ttu-id="15a5b-108">在中[前面的教程](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)介绍了如何创建项目级 DataList。</span><span class="sxs-lookup"><span data-stu-id="15a5b-108">In the [preceding tutorial](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md) we examined how to create an item-level DataList.</span></span> <span data-ttu-id="15a5b-109">像标准的可编辑 GridView DataList 中的每个项包含编辑按钮，当单击时，会使项可编辑。</span><span class="sxs-lookup"><span data-stu-id="15a5b-109">Like the standard editable GridView, each item in the DataList included an Edit button that, when clicked, would make the item editable.</span></span> <span data-ttu-id="15a5b-110">虽然这项级别编辑适用于仅偶尔更新的数据，某些用例场景要求用户编辑多个记录。</span><span class="sxs-lookup"><span data-stu-id="15a5b-110">While this item-level editing works well for data that is only updated occasionally, certain use case scenarios require the user to edit many records.</span></span> <span data-ttu-id="15a5b-111">如果用户需要编辑数十个记录，并强制，单击编辑，使他们的更改，然后单击为每个更新，则单击量可能妨碍她的工作效率。</span><span class="sxs-lookup"><span data-stu-id="15a5b-111">If a user needs to edit dozens of records and is forced to click Edit, make their changes, and click Update for each one, the amount of clicking can hamper her productivity.</span></span> <span data-ttu-id="15a5b-112">在这种情况下，更好的选择是要提供完全可编辑的 DataList，其中*所有*已在编辑模式，其值可以通过单击页上的全部更新按钮进行编辑的项 （请参阅图 1）。</span><span class="sxs-lookup"><span data-stu-id="15a5b-112">In such situations, a better option is to provide a fully-editable DataList, one where *all* of its items are in edit mode and whose values can be edited by clicking an Update All button on the page (see Figure 1).</span></span>


<span data-ttu-id="15a5b-113">[![可以修改完全可编辑的 DataList 中的每个项](performing-batch-updates-vb/_static/image2.png)](performing-batch-updates-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="15a5b-113">[![Each Item in a Fully Editable DataList can be Modified](performing-batch-updates-vb/_static/image2.png)](performing-batch-updates-vb/_static/image1.png)</span></span>

<span data-ttu-id="15a5b-114">**图 1**： 可以修改完全可编辑的 DataList 中的每个项 ([单击以查看实际尺寸的图像](performing-batch-updates-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="15a5b-114">**Figure 1**: Each Item in a Fully Editable DataList can be Modified ([Click to view full-size image](performing-batch-updates-vb/_static/image3.png))</span></span>


<span data-ttu-id="15a5b-115">在本教程中我们将介绍如何使用户能够更新供应商的地址信息完全可编辑的 DataList。</span><span class="sxs-lookup"><span data-stu-id="15a5b-115">In this tutorial we'll examine how to enable users to update suppliers address information using a fully editable DataList.</span></span>

## <a name="step-1-create-the-editable-user-interface-in-the-datalist-s-itemtemplate"></a><span data-ttu-id="15a5b-116">步骤 1： 创建可编辑的用户界面中 DataList 的 ItemTemplate</span><span class="sxs-lookup"><span data-stu-id="15a5b-116">Step 1: Create the Editable User Interface in the DataList s ItemTemplate</span></span>

<span data-ttu-id="15a5b-117">在前面的教程，其中我们创建标准的项级别的可编辑 DataList，我们使用两个模板：</span><span class="sxs-lookup"><span data-stu-id="15a5b-117">In the preceding tutorial, where we creating a standard, item-level editable DataList, we used two templates:</span></span>

- <span data-ttu-id="15a5b-118">`ItemTemplate` 包含只读的用户界面 （标签 Web 控件用于显示每个产品名称和价格）。</span><span class="sxs-lookup"><span data-stu-id="15a5b-118">`ItemTemplate` contained the read-only user interface (the Label Web controls for displaying each product s name and price).</span></span>
- <span data-ttu-id="15a5b-119">`EditItemTemplate` 包含编辑模式用户界面 （两个 TextBox Web 控件）。</span><span class="sxs-lookup"><span data-stu-id="15a5b-119">`EditItemTemplate` contained the edit mode user interface (the two TextBox Web controls).</span></span>

<span data-ttu-id="15a5b-120">DataList s`EditItemIndex`属性决定了什么`DataListItem`（如果有） 使用呈现`EditItemTemplate`。</span><span class="sxs-lookup"><span data-stu-id="15a5b-120">The DataList s `EditItemIndex` property dictates what `DataListItem` (if any) is rendered using the `EditItemTemplate`.</span></span> <span data-ttu-id="15a5b-121">具体而言，`DataListItem`其`ItemIndex`值与匹配 DataList s`EditItemIndex`使用呈现属性`EditItemTemplate`。</span><span class="sxs-lookup"><span data-stu-id="15a5b-121">In particular, the `DataListItem` whose `ItemIndex` value matches the DataList s `EditItemIndex` property is rendered using the `EditItemTemplate`.</span></span> <span data-ttu-id="15a5b-122">此模型适用于创建完全可编辑 DataList 时，可以在时间，但现在相隔编辑只有一项。</span><span class="sxs-lookup"><span data-stu-id="15a5b-122">This model works well when only one item can be edited at a time, but falls apart when creating a fully-editable DataList.</span></span>

<span data-ttu-id="15a5b-123">对于完全可编辑的 DataList，我们希望*所有*的`DataListItem`s 使用的可编辑界面来呈现。</span><span class="sxs-lookup"><span data-stu-id="15a5b-123">For a fully editable DataList, we want *all* of the `DataListItem` s to render using the editable interface.</span></span> <span data-ttu-id="15a5b-124">若要实现此目的的最简单方法是定义中的可编辑界面`ItemTemplate`。</span><span class="sxs-lookup"><span data-stu-id="15a5b-124">The simplest way to accomplish this is to define the editable interface in the `ItemTemplate`.</span></span> <span data-ttu-id="15a5b-125">用于修改供应商地址信息，可编辑接口包含地址、 城市和国家/地区值为文本，然后选择文本框的供应商名称。</span><span class="sxs-lookup"><span data-stu-id="15a5b-125">For modifying the suppliers address information, the editable interface contains the supplier name as text and then TextBoxes for the address, city, and country values.</span></span>

<span data-ttu-id="15a5b-126">首先打开`BatchUpdate.aspx`页上，添加 DataList 控件，并设置其`ID`属性设置为`Suppliers`。</span><span class="sxs-lookup"><span data-stu-id="15a5b-126">Start by opening the `BatchUpdate.aspx` page, add a DataList control, and set its `ID` property to `Suppliers`.</span></span> <span data-ttu-id="15a5b-127">通过 DataList s 智能标记中，选择要添加一个名为的新 ObjectDataSource 控件`SuppliersDataSource`。</span><span class="sxs-lookup"><span data-stu-id="15a5b-127">From the DataList s smart tag, opt to add a new ObjectDataSource control named `SuppliersDataSource`.</span></span>


<span data-ttu-id="15a5b-128">[![创建名为 SuppliersDataSource 新 ObjectDataSource](performing-batch-updates-vb/_static/image5.png)](performing-batch-updates-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="15a5b-128">[![Create a New ObjectDataSource Named SuppliersDataSource](performing-batch-updates-vb/_static/image5.png)](performing-batch-updates-vb/_static/image4.png)</span></span>

<span data-ttu-id="15a5b-129">**图 2**： 创建新对象数据源命名`SuppliersDataSource`([单击以查看实际尺寸的图像](performing-batch-updates-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="15a5b-129">**Figure 2**: Create a New ObjectDataSource Named `SuppliersDataSource` ([Click to view full-size image](performing-batch-updates-vb/_static/image6.png))</span></span>


<span data-ttu-id="15a5b-130">配置对象数据源检索数据使用`SuppliersBLL`类的`GetSuppliers()`方法 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="15a5b-130">Configure the ObjectDataSource to retrieve data using the `SuppliersBLL` class s `GetSuppliers()` method (see Figure 3).</span></span> <span data-ttu-id="15a5b-131">与前面的教程中，而不更新通过 ObjectDataSource 的供应商信息，我们将直接与业务逻辑层进行合作。</span><span class="sxs-lookup"><span data-stu-id="15a5b-131">As with the preceding tutorial, rather than updating the supplier information through the ObjectDataSource, we'll work directly with the Business Logic Layer.</span></span> <span data-ttu-id="15a5b-132">因此，在更新选项卡中设置为 （无） 下拉列表 （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="15a5b-132">Therefore, set the drop-down list to (None) in the UPDATE tab (see Figure 4).</span></span>


<span data-ttu-id="15a5b-133">[![检索使用 GetSuppliers() 方法供应商信息](performing-batch-updates-vb/_static/image8.png)](performing-batch-updates-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="15a5b-133">[![Retrieve Supplier Information Using the GetSuppliers() Method](performing-batch-updates-vb/_static/image8.png)](performing-batch-updates-vb/_static/image7.png)</span></span>

<span data-ttu-id="15a5b-134">**图 3**： 检索供应商信息使用`GetSuppliers()`方法 ([单击以查看实际尺寸的图像](performing-batch-updates-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="15a5b-134">**Figure 3**: Retrieve Supplier Information Using the `GetSuppliers()` Method ([Click to view full-size image](performing-batch-updates-vb/_static/image9.png))</span></span>


<span data-ttu-id="15a5b-135">[![在更新选项卡中设置为 （无） 下拉列表](performing-batch-updates-vb/_static/image11.png)](performing-batch-updates-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="15a5b-135">[![Set the Drop-Down List to (None) in the UPDATE Tab](performing-batch-updates-vb/_static/image11.png)](performing-batch-updates-vb/_static/image10.png)</span></span>

<span data-ttu-id="15a5b-136">**图 4**： 在更新选项卡中设置为 （无） 下拉列表 ([单击以查看实际尺寸的图像](performing-batch-updates-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="15a5b-136">**Figure 4**: Set the Drop-Down List to (None) in the UPDATE Tab ([Click to view full-size image](performing-batch-updates-vb/_static/image12.png))</span></span>


<span data-ttu-id="15a5b-137">完成向导后，Visual Studio 会自动生成 DataList 的`ItemTemplate`显示标签 Web 控件中的数据源返回的每个数据字段。</span><span class="sxs-lookup"><span data-stu-id="15a5b-137">After completing the wizard, Visual Studio automatically generates the DataList s `ItemTemplate` to display each data field returned by the data source in a Label Web control.</span></span> <span data-ttu-id="15a5b-138">我们需要修改此模板，可改为提供的编辑界面。</span><span class="sxs-lookup"><span data-stu-id="15a5b-138">We need to modify this template so that it provides the editing interface instead.</span></span> <span data-ttu-id="15a5b-139">`ItemTemplate`可以通过使用 DataList s 智能标记中的编辑模板选项的设计器或直接通过声明性语法的自定义。</span><span class="sxs-lookup"><span data-stu-id="15a5b-139">The `ItemTemplate` can be customized through the Designer using the Edit Templates option from the DataList s smart tag or directly through the declarative syntax.</span></span>

<span data-ttu-id="15a5b-140">请花费片刻时间来创建用于编辑界面显示供应商的名为文本，但包括供应商的地址、 城市和国家/地区值的文本框。</span><span class="sxs-lookup"><span data-stu-id="15a5b-140">Take a moment to create an editing interface that displays the supplier s name as text, but includes TextBoxes for the supplier s address, city, and country values.</span></span> <span data-ttu-id="15a5b-141">进行这些更改后，在页 s 声明性语法应看起来类似于下面：</span><span class="sxs-lookup"><span data-stu-id="15a5b-141">After making these changes, your page s declarative syntax should look similar to the following:</span></span>


[!code-aspx[Main](performing-batch-updates-vb/samples/sample1.aspx)]

> [!NOTE]
> <span data-ttu-id="15a5b-142">与前面的教程中，在本教程中 DataList 必须具有启用了其视图状态。</span><span class="sxs-lookup"><span data-stu-id="15a5b-142">As with the preceding tutorial, the DataList in this tutorial must have its view state enabled.</span></span>


<span data-ttu-id="15a5b-143">中`ItemTemplate`我使用两个新的 CSS 类，m`SupplierPropertyLabel`并`SupplierPropertyValue`，其中已添加到`Styles.css`类，并配置为使用相同的样式设置`ProductPropertyLabel`和`ProductPropertyValue`CSS 类。</span><span class="sxs-lookup"><span data-stu-id="15a5b-143">In the `ItemTemplate` I m using two new CSS classes, `SupplierPropertyLabel` and `SupplierPropertyValue`, which have been added to the `Styles.css` class and configured to use the same style settings as the `ProductPropertyLabel` and `ProductPropertyValue` CSS classes.</span></span>


[!code-css[Main](performing-batch-updates-vb/samples/sample2.css)]

<span data-ttu-id="15a5b-144">进行这些更改后，请访问此页上的通过浏览器。</span><span class="sxs-lookup"><span data-stu-id="15a5b-144">After making these changes, visit this page through a browser.</span></span> <span data-ttu-id="15a5b-145">如图 5 所示，每个 DataList 项供应商名称显示为文本，并使用文本框来显示地址、 城市和国家/地区。</span><span class="sxs-lookup"><span data-stu-id="15a5b-145">As Figure 5 shows, each DataList item displays the supplier name as text and uses TextBoxes to display the address, city, and country.</span></span>


<span data-ttu-id="15a5b-146">[![DataList 中的每个供应商是可编辑](performing-batch-updates-vb/_static/image14.png)](performing-batch-updates-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="15a5b-146">[![Each Supplier in the DataList is Editable](performing-batch-updates-vb/_static/image14.png)](performing-batch-updates-vb/_static/image13.png)</span></span>

<span data-ttu-id="15a5b-147">**图 5**: DataList 中的每个供应商是可编辑 ([单击以查看实际尺寸的图像](performing-batch-updates-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="15a5b-147">**Figure 5**: Each Supplier in the DataList is Editable ([Click to view full-size image](performing-batch-updates-vb/_static/image15.png))</span></span>


## <a name="step-2-adding-an-update-all-button"></a><span data-ttu-id="15a5b-148">步骤 2： 添加更新所有按钮</span><span class="sxs-lookup"><span data-stu-id="15a5b-148">Step 2: Adding an Update All Button</span></span>

<span data-ttu-id="15a5b-149">图 5 中的每个供应商有其地址、 城市和国家/地区字段显示在文本框中，当前没有任何更新按钮可用。</span><span class="sxs-lookup"><span data-stu-id="15a5b-149">While each supplier in Figure 5 has its address, city, and country fields displayed in a TextBox, there currently is no Update button available.</span></span> <span data-ttu-id="15a5b-150">而不是让每个项的更新按钮，使用完全可编辑 DataLists 没有通常一次更新所有按钮的页上，单击时，更新*所有*DataList 中的记录。</span><span class="sxs-lookup"><span data-stu-id="15a5b-150">Rather than having an Update button per item, with fully editable DataLists there is typically a single Update All button on the page that, when clicked, updates *all* of the records in the DataList.</span></span> <span data-ttu-id="15a5b-151">对于本教程，让我们来添加两个更新所有按钮-一个在页面顶部，一个在底部 （尽管单击任一按钮将具有相同的效果）。</span><span class="sxs-lookup"><span data-stu-id="15a5b-151">For this tutorial, let s add two Update All buttons - one at the top of the page and one at the bottom (although clicking either button will have the same effect).</span></span>

<span data-ttu-id="15a5b-152">首先添加一个按钮 Web 控件上面的 DataList 并设置其`ID`属性设置为`UpdateAll1`。</span><span class="sxs-lookup"><span data-stu-id="15a5b-152">Start by adding a Button Web control above the DataList and set its `ID` property to `UpdateAll1`.</span></span> <span data-ttu-id="15a5b-153">接下来，添加第二个按钮 Web 控件下方 DataList，设置其`ID`到`UpdateAll2`。</span><span class="sxs-lookup"><span data-stu-id="15a5b-153">Next, add the second Button Web control beneath the DataList, setting its `ID` to `UpdateAll2`.</span></span> <span data-ttu-id="15a5b-154">设置`Text`到更新所有的两个按钮的属性。</span><span class="sxs-lookup"><span data-stu-id="15a5b-154">Set the `Text` properties for the two Buttons to Update All.</span></span> <span data-ttu-id="15a5b-155">最后，为这两个按钮创建事件处理程序`Click`事件。</span><span class="sxs-lookup"><span data-stu-id="15a5b-155">Lastly, create event handlers for both Buttons `Click` events.</span></span> <span data-ttu-id="15a5b-156">而不会复制每个事件处理程序中的更新逻辑，let s 重构到第三种方法，该逻辑`UpdateAllSupplierAddresses`，具有事件处理程序只需调用此第三个方法。</span><span class="sxs-lookup"><span data-stu-id="15a5b-156">Rather than duplicating the update logic in each of the event handlers, let s refactor that logic to a third method, `UpdateAllSupplierAddresses`, having the event handlers simply invoking this third method.</span></span>


[!code-vb[Main](performing-batch-updates-vb/samples/sample3.vb)]

<span data-ttu-id="15a5b-157">图 6 添加更新所有按钮后显示的页。</span><span class="sxs-lookup"><span data-stu-id="15a5b-157">Figure 6 shows the page after the Update All buttons have been added.</span></span>


<span data-ttu-id="15a5b-158">[![两个更新所有按钮已都添加到页面](performing-batch-updates-vb/_static/image17.png)](performing-batch-updates-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="15a5b-158">[![Two Update All Buttons have been Added to the Page](performing-batch-updates-vb/_static/image17.png)](performing-batch-updates-vb/_static/image16.png)</span></span>

<span data-ttu-id="15a5b-159">**图 6**： 两个更新所有按钮已都添加到页面 ([单击以查看实际尺寸的图像](performing-batch-updates-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="15a5b-159">**Figure 6**: Two Update All Buttons have been Added to the Page ([Click to view full-size image](performing-batch-updates-vb/_static/image18.png))</span></span>


## <a name="step-3-updating-all-of-the-suppliers-address-information"></a><span data-ttu-id="15a5b-160">步骤 3： 更新所有供应商地址信息</span><span class="sxs-lookup"><span data-stu-id="15a5b-160">Step 3: Updating All of the Suppliers Address Information</span></span>

<span data-ttu-id="15a5b-161">与所有显示的编辑界面的 DataList 的项和添加的所有更新的按钮，所有这些仍编写代码来执行批处理更新。</span><span class="sxs-lookup"><span data-stu-id="15a5b-161">With all of the DataList s items displaying the editing interface and with the addition of the Update All buttons, all that remains is writing the code to perform the batch update.</span></span> <span data-ttu-id="15a5b-162">具体而言，我们需要循环访问的 DataList 的项和调用`SuppliersBLL`类的`UpdateSupplierAddress`为每个方法。</span><span class="sxs-lookup"><span data-stu-id="15a5b-162">Specifically, we need to loop through the DataList s items and call the `SuppliersBLL` class s `UpdateSupplierAddress` method for each one.</span></span>

<span data-ttu-id="15a5b-163">集合`DataListItem`实例可以通过 DataList s 访问 DataList 该构成[`Items`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.items.aspx)。</span><span class="sxs-lookup"><span data-stu-id="15a5b-163">The collection of `DataListItem` instances that makeup the DataList can be accessed via the DataList s [`Items` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.items.aspx).</span></span> <span data-ttu-id="15a5b-164">对引用`DataListItem`，我们可以获取相应`SupplierID`从`DataKeys`集合和以编程方式引用文本框 Web 控件内`ItemTemplate`如以下代码所示：</span><span class="sxs-lookup"><span data-stu-id="15a5b-164">With a reference to a `DataListItem`, we can grab the corresponding `SupplierID` from the `DataKeys` collection and programmatically reference the TextBox Web controls within the `ItemTemplate` as the following code illustrates:</span></span>


[!code-vb[Main](performing-batch-updates-vb/samples/sample4.vb)]

<span data-ttu-id="15a5b-165">当用户单击全部更新按钮，之一`UpdateAllSupplierAddresses`方法循环访问每个`DataListItem`中`Suppliers`DataList 和调用`SuppliersBLL`类的`UpdateSupplierAddress`方法，传入相应的值。</span><span class="sxs-lookup"><span data-stu-id="15a5b-165">When the user clicks one of the Update All buttons, the `UpdateAllSupplierAddresses` method iterates through each `DataListItem` in the `Suppliers` DataList and calls the `SuppliersBLL` class s `UpdateSupplierAddress` method, passing in the corresponding values.</span></span> <span data-ttu-id="15a5b-166">地址、 城市或国家/地区传递的非输入值是值为`Nothing`到`UpdateSupplierAddress`（而不是空字符串），这会导致数据库`NULL`基础记录 s 字段。</span><span class="sxs-lookup"><span data-stu-id="15a5b-166">A non-entered value for address, city, or country passes is a value of `Nothing` to `UpdateSupplierAddress` (rather than a blank string), which results in a database `NULL` for the underlying record s fields.</span></span>

> [!NOTE]
> <span data-ttu-id="15a5b-167">是增强，您可能想要将状态标签 Web 控件添加到提供一些确认消息，执行批处理更新后的页面。</span><span class="sxs-lookup"><span data-stu-id="15a5b-167">As an enhancement, you may want to add a status Label Web control to the page that provides some confirmation message after the batch update is performed.</span></span>


## <a name="updating-only-those-addresses-that-have-been-modified"></a><span data-ttu-id="15a5b-168">更新已修改这些地址</span><span class="sxs-lookup"><span data-stu-id="15a5b-168">Updating Only Those Addresses That Have Been Modified</span></span>

<span data-ttu-id="15a5b-169">用于此教程的调用的批处理更新算法`UpdateSupplierAddress`方法*每个*DataList，无论是否已更改其地址信息中的供应商。</span><span class="sxs-lookup"><span data-stu-id="15a5b-169">The batch update algorithm used for this tutorial calls the `UpdateSupplierAddress` method for *every* supplier in the DataList, regardless of whether their address information has been changed.</span></span> <span data-ttu-id="15a5b-170">而此类 blind 更新计划运行 t 通常性能问题，它们可能会导致多余记录如果您重新审核更改为数据库表。</span><span class="sxs-lookup"><span data-stu-id="15a5b-170">While such blind updates aren t usually a performance issue, they can lead to superfluous records if you re auditing changes to the database table.</span></span> <span data-ttu-id="15a5b-171">例如，如果你使用触发器来记录所有`UPDATE`到`Suppliers`到审核表，每次用户单击全部更新按钮将在系统中，而不管用户是否进行任何为每个供应商创建一个新的审核记录的表更改。</span><span class="sxs-lookup"><span data-stu-id="15a5b-171">For example, if you use triggers to record all `UPDATE` s to the `Suppliers` table to an auditing table, every time a user clicks the Update All button a new audit record will be created for each supplier in the system, regardless of whether the user made any changes.</span></span>

<span data-ttu-id="15a5b-172">ADO.NET DataTable 和 DataAdapter 类旨在支持批量更新，其中仅修改、 删除和新记录结果中的任何数据库通信。</span><span class="sxs-lookup"><span data-stu-id="15a5b-172">The ADO.NET DataTable and DataAdapter classes are designed to support batch updates where only modified, deleted, and new records results in any database communication.</span></span> <span data-ttu-id="15a5b-173">DataTable 中的每一行都具有[`RowState`属性](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx)，该值指示行是否已添加到 DataTable，从它，修改、 删除或保持不变。</span><span class="sxs-lookup"><span data-stu-id="15a5b-173">Each row in the DataTable has a [`RowState` property](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx) that indicates whether the row has been added to the DataTable, deleted from it, modified, or remains unchanged.</span></span> <span data-ttu-id="15a5b-174">当最初填充数据表时，所有标记的行不变。</span><span class="sxs-lookup"><span data-stu-id="15a5b-174">When a DataTable is initially populated, all rows are marked unchanged.</span></span> <span data-ttu-id="15a5b-175">更改任何行的列的值标记为已修改。</span><span class="sxs-lookup"><span data-stu-id="15a5b-175">Changing the value of any of the row s columns marks the row as modified.</span></span>

<span data-ttu-id="15a5b-176">在中`SuppliersBLL`我们通过一个供应商记录到中的第一个读取更新指定供应商的地址信息的类`SuppliersDataTable`，然后设置`Address`， `City`，和`Country`列的值使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="15a5b-176">In the `SuppliersBLL` class we update the specified supplier s address information by first reading in the single supplier record into a `SuppliersDataTable` and then set the `Address`, `City`, and `Country` column values using the following code:</span></span>


[!code-vb[Main](performing-batch-updates-vb/samples/sample5.vb)]

<span data-ttu-id="15a5b-177">传入的地址、 城市和国家/地区值，此代码段将分配`SuppliersRow`在`SuppliersDataTable`而不考虑值没有变化。</span><span class="sxs-lookup"><span data-stu-id="15a5b-177">This code naively assigns the passed-in address, city, and country values to the `SuppliersRow` in the `SuppliersDataTable` regardless of whether or not the values have changed.</span></span> <span data-ttu-id="15a5b-178">这些修改会导致`SuppliersRow`s`RowState`属性被标记为已修改。</span><span class="sxs-lookup"><span data-stu-id="15a5b-178">These modifications cause the `SuppliersRow` s `RowState` property to be marked as modified.</span></span> <span data-ttu-id="15a5b-179">当数据访问层 s`Update`方法调用时，它发现`SupplierRow`已被修改，因此发送`UPDATE`命令到数据库。</span><span class="sxs-lookup"><span data-stu-id="15a5b-179">When the Data Access Layer s `Update` method is called, it sees that the `SupplierRow` has been modified and therefore sends an `UPDATE` command to the database.</span></span>

<span data-ttu-id="15a5b-180">假设，我们将代码添加到此方法以仅分配传入的地址、 城市和国家/地区值，如果它们与不同`SuppliersRow`s 现有值。</span><span class="sxs-lookup"><span data-stu-id="15a5b-180">Imagine, however, that we added code to this method to only assign the passed-in address, city, and country values if they differ from the `SuppliersRow` s existing values.</span></span> <span data-ttu-id="15a5b-181">其中的地址、 城市和国家/地区将与现有的数据相同的情况下，在进行任何更改并`SupplierRow`s`RowState`将保留标记为不变。</span><span class="sxs-lookup"><span data-stu-id="15a5b-181">In the case where the address, city, and country are the same as the existing data, no changes will be made and the `SupplierRow` s `RowState` will be left marked as unchanged.</span></span> <span data-ttu-id="15a5b-182">最终结果是，当 DAL s`Update`调用方法，将对任何数据库调用，因为`SuppliersRow`尚未修改。</span><span class="sxs-lookup"><span data-stu-id="15a5b-182">The net result is that when the DAL s `Update` method is called, no database call will be made because the `SuppliersRow` has not been modified.</span></span>

<span data-ttu-id="15a5b-183">若要执行此更改，将为传入的地址、 城市和国家/地区值使用以下代码会盲目地将分配的语句：</span><span class="sxs-lookup"><span data-stu-id="15a5b-183">To enact this change, replace the statements that blindly assign the passed-in address, city, and country values with the following code:</span></span>


[!code-vb[Main](performing-batch-updates-vb/samples/sample6.vb)]

<span data-ttu-id="15a5b-184">与此添加代码，DAL s`Update`方法发送`UPDATE`到只有那些其与地址相关的值已更改的记录的数据库的语句。</span><span class="sxs-lookup"><span data-stu-id="15a5b-184">With this added code, the DAL s `Update` method sends an `UPDATE` statement to the database for only those records whose address-related values have changed.</span></span>

<span data-ttu-id="15a5b-185">或者，我们无法跟踪是否有传入的地址字段和数据库数据之间的差异和，如果没有任何表，只需跳过对 DAL 的调用`Update`方法。</span><span class="sxs-lookup"><span data-stu-id="15a5b-185">Alternatively, we could keep track of whether there are any differences between the passed-in address fields and the database data and, if there are none, simply bypass the call to the DAL s `Update` method.</span></span> <span data-ttu-id="15a5b-186">如果您重新使用 DB 定向方法，因为 DB 直接方法并不是 t 传递，此方法适用`SuppliersRow`实例，它的`RowState`可以进行检查，以确定是否实际需要的数据库调用。</span><span class="sxs-lookup"><span data-stu-id="15a5b-186">This approach works well if you re using the DB direct method, since the DB direct method isn t passed a `SuppliersRow` instance whose `RowState` can be checked to determine whether a database call is actually needed.</span></span>

> [!NOTE]
> <span data-ttu-id="15a5b-187">每次`UpdateSupplierAddress`调用方法、 调用数据库以检索有关已更新记录的信息。</span><span class="sxs-lookup"><span data-stu-id="15a5b-187">Each time the `UpdateSupplierAddress` method is invoked, a call is made to the database to retrieve information about the updated record.</span></span> <span data-ttu-id="15a5b-188">然后，如果数据中有任何更改，另一个到数据库进行调用以更新表行。</span><span class="sxs-lookup"><span data-stu-id="15a5b-188">Then, if there are any changes in data, another call to the database is made to update the table row.</span></span> <span data-ttu-id="15a5b-189">可以通过创建优化此工作流`UpdateSupplierAddress`方法重载，接受`EmployeesDataTable`具有实例*所有*中的更改的`BatchUpdate.aspx`页。</span><span class="sxs-lookup"><span data-stu-id="15a5b-189">This workflow could be optimized by creating an `UpdateSupplierAddress` method overload that accepts an `EmployeesDataTable` instance that has *all* of the changes from the `BatchUpdate.aspx` page.</span></span> <span data-ttu-id="15a5b-190">然后，它可以进行一次调用到数据库，若要获取所有从记录`Suppliers`表。</span><span class="sxs-lookup"><span data-stu-id="15a5b-190">Then, it could make one call to the database to get all of the records from the `Suppliers` table.</span></span> <span data-ttu-id="15a5b-191">然后可以枚举两个结果集，无法更新只有那些已发生更改的记录。</span><span class="sxs-lookup"><span data-stu-id="15a5b-191">The two resultsets could then be enumerated and only those records where changes have occurred could be updated.</span></span>


## <a name="summary"></a><span data-ttu-id="15a5b-192">总结</span><span class="sxs-lookup"><span data-stu-id="15a5b-192">Summary</span></span>

<span data-ttu-id="15a5b-193">在本教程中我们已了解如何创建完全可编辑的 DataList，从而使用户可快速修改多个供应商的地址信息。</span><span class="sxs-lookup"><span data-stu-id="15a5b-193">In this tutorial we saw how to create a fully editable DataList, allowing a user to quickly modify the address information for multiple suppliers.</span></span> <span data-ttu-id="15a5b-194">我们通过 DataList s 中定义的供应商的地址、 城市和国家/地区值的文本框中 Web 控件的编辑界面启动`ItemTemplate`。</span><span class="sxs-lookup"><span data-stu-id="15a5b-194">We started by defining the editing interface a TextBox Web control for the supplier s address, city, and country values in the DataList s `ItemTemplate`.</span></span> <span data-ttu-id="15a5b-195">接下来，我们添加了更新所有按钮的上方和下方 DataList。</span><span class="sxs-lookup"><span data-stu-id="15a5b-195">Next, we added Update All buttons above and below the DataList.</span></span> <span data-ttu-id="15a5b-196">用户已进行他的更改并单击全部更新按钮，之一后`DataListItem`s 枚举和调用`SuppliersBLL`类的`UpdateSupplierAddress`方法由。</span><span class="sxs-lookup"><span data-stu-id="15a5b-196">After a user has made his changes and clicked one of the Update All buttons, the `DataListItem` s are enumerated and a call to the `SuppliersBLL` class s `UpdateSupplierAddress` method is made.</span></span>

<span data-ttu-id="15a5b-197">快乐编程 ！</span><span class="sxs-lookup"><span data-stu-id="15a5b-197">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="15a5b-198">关于作者</span><span class="sxs-lookup"><span data-stu-id="15a5b-198">About the Author</span></span>

<span data-ttu-id="15a5b-199">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="15a5b-199">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="15a5b-200">Scott 是独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="15a5b-200">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="15a5b-201">他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="15a5b-201">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="15a5b-202">他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="15a5b-202">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="15a5b-203">或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="15a5b-203">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="15a5b-204">特别感谢</span><span class="sxs-lookup"><span data-stu-id="15a5b-204">Special Thanks To</span></span>

<span data-ttu-id="15a5b-205">很多有用的审阅者已评审本系列教程。</span><span class="sxs-lookup"><span data-stu-id="15a5b-205">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="15a5b-206">本教程中的潜在顾客审阅者已 Zack Jones 和 Ken Pespisa。</span><span class="sxs-lookup"><span data-stu-id="15a5b-206">Lead reviewers for this tutorial were Zack Jones and Ken Pespisa.</span></span> <span data-ttu-id="15a5b-207">是否有兴趣查看我即将推出的 MSDN 文章？</span><span class="sxs-lookup"><span data-stu-id="15a5b-207">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="15a5b-208">如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="15a5b-208">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="15a5b-209">[上一页](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
> [下一页](handling-bll-and-dal-level-exceptions-vb.md)</span><span class="sxs-lookup"><span data-stu-id="15a5b-209">[Previous](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
[Next](handling-bll-and-dal-level-exceptions-vb.md)</span></span>
