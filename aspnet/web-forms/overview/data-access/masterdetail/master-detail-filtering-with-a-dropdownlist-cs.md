---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
title: 使用 DropDownList (C#) 进行筛选主/详细信息 |Microsoft 文档
author: rick-anderson
description: 在本教程中我们将了解如何在 DropDownList 控件和一个 GridView 中的选定的列表项的详细信息中显示的主记录。
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 53e659cc-eefb-40c1-a1dc-559481c99443
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 42a6a76b0b05045bed1ada227b7c32a51600b760
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30880627"
---
<a name="masterdetail-filtering-with-a-dropdownlist-c"></a><span data-ttu-id="cb132-103">主/从使用 DropDownList (C#) 进行筛选</span><span class="sxs-lookup"><span data-stu-id="cb132-103">Master/Detail Filtering With a DropDownList (C#)</span></span>
====================
<span data-ttu-id="cb132-104">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="cb132-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="cb132-105">[下载示例应用程序](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_7_CS.exe)或[下载 PDF](master-detail-filtering-with-a-dropdownlist-cs/_static/datatutorial07cs1.pdf)</span><span class="sxs-lookup"><span data-stu-id="cb132-105">[Download Sample App](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_7_CS.exe) or [Download PDF](master-detail-filtering-with-a-dropdownlist-cs/_static/datatutorial07cs1.pdf)</span></span>

> <span data-ttu-id="cb132-106">在本教程中我们将了解如何在 DropDownList 控件和一个 GridView 中的选定的列表项的详细信息中显示的主记录。</span><span class="sxs-lookup"><span data-stu-id="cb132-106">In this tutorial we'll see how to display the master records in a DropDownList control and the details of the selected list item in a GridView.</span></span>


## <a name="introduction"></a><span data-ttu-id="cb132-107">介绍</span><span class="sxs-lookup"><span data-stu-id="cb132-107">Introduction</span></span>

<span data-ttu-id="cb132-108">常用的报表类型是*主/详细信息报表*中，报表从此处开始通过显示的"主"的记录集。</span><span class="sxs-lookup"><span data-stu-id="cb132-108">A common type of report is the *master/detail report*, in which the report begins by showing some set of "master" records.</span></span> <span data-ttu-id="cb132-109">用户可以然后向下钻取一个主机记录，从而查看该主记录的"详细信息。"</span><span class="sxs-lookup"><span data-stu-id="cb132-109">The user can then drill down into one of the master records, thereby viewing that master record's "details."</span></span> <span data-ttu-id="cb132-110">主/详细信息报告是用于可视化一个对多关系，如报表的理想选择显示的所有类别，然后允许用户选择一种特定类别，然后显示其关联的产品。</span><span class="sxs-lookup"><span data-stu-id="cb132-110">Master/detail reports are an ideal choice for visualizing one-to-many relationships, such as a report showing all of the categories and then allowing a user to select a particular category and display its associated products.</span></span> <span data-ttu-id="cb132-111">此外，主/详细信息报表可用于显示特别"宽"表 （一种是有大量的列） 中的详细的信息。</span><span class="sxs-lookup"><span data-stu-id="cb132-111">Additionally, master/detail reports are useful for displaying detailed information from particularly "wide" tables (ones that have a lot of columns).</span></span> <span data-ttu-id="cb132-112">例如，主/详细信息报表的"主"级别可能会在数据库中，显示只包括产品名称和单位价格的产品和向下钻取到特定的产品将显示额外的产品字段 (分类、 供应商、 每个单元，数量和等等）。</span><span class="sxs-lookup"><span data-stu-id="cb132-112">For example, the "master" level of a master/detail report might show just the product name and unit price of the products in the database, and drilling down into a particular product would show the additional product fields (category, supplier, quantity per unit, and so on).</span></span>

<span data-ttu-id="cb132-113">有多种方法可以与其实现主/详细信息报表。</span><span class="sxs-lookup"><span data-stu-id="cb132-113">There are many ways with which a master/detail report can be implemented.</span></span> <span data-ttu-id="cb132-114">通过这和接下来三个教程中，我们将查看在不同的主/详细信息报表。</span><span class="sxs-lookup"><span data-stu-id="cb132-114">Over this and the next three tutorials we'll look at a variety of master/detail reports.</span></span> <span data-ttu-id="cb132-115">在本教程中，我们将了解如何显示中的主记录[DropDownList 控件](https://msdn.microsoft.com/library/dtx91y0z.aspx)和 GridView 中的选定的列表项的详细信息。</span><span class="sxs-lookup"><span data-stu-id="cb132-115">In this tutorial we'll see how to display the master records in a [DropDownList control](https://msdn.microsoft.com/library/dtx91y0z.aspx) and the details of the selected list item in a GridView.</span></span> <span data-ttu-id="cb132-116">具体而言，本教程的主/从报表将列出类别和产品信息。</span><span class="sxs-lookup"><span data-stu-id="cb132-116">In particular, this tutorial's master/detail report will list category and product information.</span></span>

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a><span data-ttu-id="cb132-117">步骤 1： 在 DropDownList 中显示的类别</span><span class="sxs-lookup"><span data-stu-id="cb132-117">Step 1: Displaying the Categories in a DropDownList</span></span>

<span data-ttu-id="cb132-118">主/从报表将与显示的选定的列表项的产品列出的 DropDownList 中的类别在 GridView 的页中进一步向下。</span><span class="sxs-lookup"><span data-stu-id="cb132-118">Our master/detail report will list the categories in a DropDownList, with the selected list item's products displayed further down in the page in a GridView.</span></span> <span data-ttu-id="cb132-119">然后，早 us，第一个任务是具有 DropDownList 中显示的类别。</span><span class="sxs-lookup"><span data-stu-id="cb132-119">The first task ahead of us, then, is to have the categories displayed in a DropDownList.</span></span> <span data-ttu-id="cb132-120">打开`FilterByDropDownList.aspx`页面`Filtering`文件夹中，将在 DropDownList 上从工具箱中拖动到页面的设计器，并设置其`ID`属性`Categories`。</span><span class="sxs-lookup"><span data-stu-id="cb132-120">Open the `FilterByDropDownList.aspx` page in the `Filtering` folder, drag on a DropDownList from the Toolbox onto the page's designer, and set its `ID` property to `Categories`.</span></span> <span data-ttu-id="cb132-121">接下来，单击下拉列表的智能标记中的选择数据源链接。</span><span class="sxs-lookup"><span data-stu-id="cb132-121">Next, click on the Choose Data Source link from the DropDownList's smart tag.</span></span> <span data-ttu-id="cb132-122">这将显示数据源配置向导。</span><span class="sxs-lookup"><span data-stu-id="cb132-122">This will display the Data Source Configuration wizard.</span></span>


<span data-ttu-id="cb132-123">[![指定的 DropDownList 数据源](master-detail-filtering-with-a-dropdownlist-cs/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-123">[![Specify the DropDownList's Data Source](master-detail-filtering-with-a-dropdownlist-cs/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="cb132-124">**图 1**： 指定下拉列表的数据源 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-124">**Figure 1**: Specify the DropDownList's Data Source ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image3.png))</span></span>


<span data-ttu-id="cb132-125">选择要添加名为新 ObjectDataSource `CategoriesDataSource` ，它调用`CategoriesBLL`类的`GetCategories()`方法。</span><span class="sxs-lookup"><span data-stu-id="cb132-125">Choose to add a new ObjectDataSource named `CategoriesDataSource` that invokes the `CategoriesBLL` class's `GetCategories()` method.</span></span>


<span data-ttu-id="cb132-126">[![添加名为 CategoriesDataSource 新对象数据源](master-detail-filtering-with-a-dropdownlist-cs/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-126">[![Add a New ObjectDataSource Named CategoriesDataSource](master-detail-filtering-with-a-dropdownlist-cs/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image4.png)</span></span>

<span data-ttu-id="cb132-127">**图 2**： 添加新对象数据源名为`CategoriesDataSource`([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-127">**Figure 2**: Add a New ObjectDataSource Named `CategoriesDataSource` ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image6.png))</span></span>


<span data-ttu-id="cb132-128">[![选择使用 CategoriesBLL 类](master-detail-filtering-with-a-dropdownlist-cs/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-128">[![Choose to Use the CategoriesBLL Class](master-detail-filtering-with-a-dropdownlist-cs/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image7.png)</span></span>

<span data-ttu-id="cb132-129">**图 3**： 选择使用`CategoriesBLL`类 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-129">**Figure 3**: Choose to Use the `CategoriesBLL` Class ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image9.png))</span></span>


<span data-ttu-id="cb132-130">[![配置对象数据源以使用 GetCategories() 方法](master-detail-filtering-with-a-dropdownlist-cs/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-130">[![Configure the ObjectDataSource to Use the GetCategories() Method](master-detail-filtering-with-a-dropdownlist-cs/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image10.png)</span></span>

<span data-ttu-id="cb132-131">**图 4**： 配置使用 ObjectDataSource`GetCategories()`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-131">**Figure 4**: Configure the ObjectDataSource to Use the `GetCategories()` Method ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image12.png))</span></span>


<span data-ttu-id="cb132-132">配置对象数据源，我们仍需要来指定哪些数据源字段应显示在 DropDownList 和后一个应关联为列表项的值。</span><span class="sxs-lookup"><span data-stu-id="cb132-132">After configuring the ObjectDataSource we still need to specify what data source field should be displayed in DropDownList and which one should be associated as the value for the list item.</span></span> <span data-ttu-id="cb132-133">具有`CategoryName`字段作为显示和`CategoryID`作为每个列表项的值。</span><span class="sxs-lookup"><span data-stu-id="cb132-133">Have the `CategoryName` field as the display and `CategoryID` as the value for each list item.</span></span>


<span data-ttu-id="cb132-134">[![具有 DropDownList 显示 CategoryName 字段和使用 CategoryID 值](master-detail-filtering-with-a-dropdownlist-cs/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-134">[![Have the DropDownList Display the CategoryName Field and Use CategoryID as the Value](master-detail-filtering-with-a-dropdownlist-cs/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image13.png)</span></span>

<span data-ttu-id="cb132-135">**图 5**： 具有 DropDownList 显示`CategoryName`字段并使用`CategoryID`作为值 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-135">**Figure 5**: Have the DropDownList Display the `CategoryName` Field and Use `CategoryID` as the Value ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image15.png))</span></span>


<span data-ttu-id="cb132-136">此时我们具有从记录将填充一个 DropDownList 控件`Categories`表 （所有在大约六个秒钟内完成）。</span><span class="sxs-lookup"><span data-stu-id="cb132-136">At this point we have a DropDownList control that's populated with the records from the `Categories` table (all accomplished in about six seconds).</span></span> <span data-ttu-id="cb132-137">通过浏览器查看时为止图 6 显示我们的进度。</span><span class="sxs-lookup"><span data-stu-id="cb132-137">Figure 6 shows our progress thus far when viewed through a browser.</span></span>


<span data-ttu-id="cb132-138">[![下拉列表将列出当前类别](master-detail-filtering-with-a-dropdownlist-cs/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-138">[![A Drop-Down Lists the Current Categories](master-detail-filtering-with-a-dropdownlist-cs/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image16.png)</span></span>

<span data-ttu-id="cb132-139">**图 6**: 下拉列表将列出当前类别 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-139">**Figure 6**: A Drop-Down Lists the Current Categories ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image18.png))</span></span>


## <a name="step-2-adding-the-products-gridview"></a><span data-ttu-id="cb132-140">步骤 2： 添加产品 GridView</span><span class="sxs-lookup"><span data-stu-id="cb132-140">Step 2: Adding the Products GridView</span></span>

<span data-ttu-id="cb132-141">主/详细信息报表中的最后一个步骤是列出与所选类别关联的产品。</span><span class="sxs-lookup"><span data-stu-id="cb132-141">That last step in our master/detail report is to list the products associated with the selected category.</span></span> <span data-ttu-id="cb132-142">若要完成此操作，向页面添加一个 GridView，并创建名为新 ObjectDataSource `productsDataSource`。</span><span class="sxs-lookup"><span data-stu-id="cb132-142">To accomplish this, add a GridView to the page and create a new ObjectDataSource named `productsDataSource`.</span></span> <span data-ttu-id="cb132-143">具有`productsDataSource`控件精选从其数据`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。</span><span class="sxs-lookup"><span data-stu-id="cb132-143">Have the `productsDataSource` control cull its data from the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method.</span></span>


<span data-ttu-id="cb132-144">[![选择 GetProductsByCategoryID(categoryID) 方法](master-detail-filtering-with-a-dropdownlist-cs/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-144">[![Select the GetProductsByCategoryID(categoryID) Method](master-detail-filtering-with-a-dropdownlist-cs/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image19.png)</span></span>

<span data-ttu-id="cb132-145">**图 7**： 选择`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-145">**Figure 7**: Select the `GetProductsByCategoryID(categoryID)` Method ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image21.png))</span></span>


<span data-ttu-id="cb132-146">在选择此方法之后, ObjectDataSource 向导提示我们值的方法的*`categoryID`* 参数。</span><span class="sxs-lookup"><span data-stu-id="cb132-146">After choosing this method, the ObjectDataSource wizard prompts us for the value for the method's *`categoryID`* parameter.</span></span> <span data-ttu-id="cb132-147">若要使用的所选值`categories`DropDownList 项设置为控件和到 ControlID 参数源`Categories`。</span><span class="sxs-lookup"><span data-stu-id="cb132-147">To use the value of the selected `categories` DropDownList item set the Parameter source to Control and the ControlID to `Categories`.</span></span>


<span data-ttu-id="cb132-148">[![CategoryID 参数值设置为类别下拉列表](master-detail-filtering-with-a-dropdownlist-cs/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-148">[![Set the categoryID Parameter to the Value of the Categories DropDownList](master-detail-filtering-with-a-dropdownlist-cs/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image22.png)</span></span>

<span data-ttu-id="cb132-149">**图 8**： 设置*`categoryID`* 参数的值`Categories`DropDownList ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-149">**Figure 8**: Set the *`categoryID`* Parameter to the Value of the `Categories` DropDownList ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image24.png))</span></span>


<span data-ttu-id="cb132-150">需要一段时间来签出我们的浏览器中的进度。</span><span class="sxs-lookup"><span data-stu-id="cb132-150">Take a moment to check out our progress in a browser.</span></span> <span data-ttu-id="cb132-151">当第一次访问该页面，这些产品属于所选类别 （如图 9 中所示），则会显示 （饮料），但更改 DropDownList 不更新的数据。</span><span class="sxs-lookup"><span data-stu-id="cb132-151">When first visiting the page, those products belong to the selected category (Beverages) are displayed (as shown in Figure 9), but changing the DropDownList doesn't update the data.</span></span> <span data-ttu-id="cb132-152">这是因为 GridView 更新必须进行回发。</span><span class="sxs-lookup"><span data-stu-id="cb132-152">This is because a postback must occur for the GridView to update.</span></span> <span data-ttu-id="cb132-153">为了实现此目的进行 （都不需要编写任何代码） 的两个选项：</span><span class="sxs-lookup"><span data-stu-id="cb132-153">To accomplish this we have two options (neither of which requires writing any code):</span></span>

- <span data-ttu-id="cb132-154">**设置的类别的 DropDownList 的**[有些属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**为 True。**</span><span class="sxs-lookup"><span data-stu-id="cb132-154">**Set the categories DropDownList's**[AutoPostBack property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**to True.**</span></span> <span data-ttu-id="cb132-155">（你可以完成此操作通过检查 DropDownList 的智能标记中的启用有些选项。）这将触发回发，每当 DropDownList 的选定项更改的用户。</span><span class="sxs-lookup"><span data-stu-id="cb132-155">(You can accomplish this by checking the Enable AutoPostBack option in the DropDownList's smart tag.) This will trigger a postback whenever the DropDownList's selected item is changed by the user.</span></span> <span data-ttu-id="cb132-156">因此，当用户从下拉列表中选择新类别回发将随之发生，并且将使用新选择的类别的产品更新 GridView。</span><span class="sxs-lookup"><span data-stu-id="cb132-156">Therefore, when the user selects a new category from the DropDownList a postback will ensue and the GridView will be updated with the products for the newly selected category.</span></span> <span data-ttu-id="cb132-157">（这是我已在本教程中使用的方法）。</span><span class="sxs-lookup"><span data-stu-id="cb132-157">(This is the approach I've used in this tutorial.)</span></span>
- <span data-ttu-id="cb132-158">**添加的 DropDownList 旁边的按钮 Web 控件。**</span><span class="sxs-lookup"><span data-stu-id="cb132-158">**Add a Button Web control next to the DropDownList.**</span></span> <span data-ttu-id="cb132-159">设置其`Text`到刷新的属性或其他类似的。</span><span class="sxs-lookup"><span data-stu-id="cb132-159">Set its `Text` property to Refresh or something similar.</span></span> <span data-ttu-id="cb132-160">使用此方法时，用户将需要选择新类别，然后单击按钮。</span><span class="sxs-lookup"><span data-stu-id="cb132-160">With this approach, the user will need to select a new category and then click the Button.</span></span> <span data-ttu-id="cb132-161">单击的按钮，将导致回发，并更新 GridView 列出所选类别的这些产品。</span><span class="sxs-lookup"><span data-stu-id="cb132-161">Clicking the Button will cause a postback and update the GridView to list those products of the selected category.</span></span>

<span data-ttu-id="cb132-162">图 9 和 10 说明了操作中的主/从报表。</span><span class="sxs-lookup"><span data-stu-id="cb132-162">Figures 9 and 10 illustrate the master/detail report in action.</span></span>


<span data-ttu-id="cb132-163">[![第一次访问该页面，将显示饮料产品](master-detail-filtering-with-a-dropdownlist-cs/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-163">[![When First Visiting the Page, the Beverage Products are Displayed](master-detail-filtering-with-a-dropdownlist-cs/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image25.png)</span></span>

<span data-ttu-id="cb132-164">**图 9**： 第一次访问该页面，将显示饮料产品 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-164">**Figure 9**: When First Visiting the Page, the Beverage Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image27.png))</span></span>


<span data-ttu-id="cb132-165">[![自动选择新的产品 （生成） 将导致回发时，更新 GridView](master-detail-filtering-with-a-dropdownlist-cs/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-165">[![Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the GridView](master-detail-filtering-with-a-dropdownlist-cs/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image28.png)</span></span>

<span data-ttu-id="cb132-166">**图 10**： 自动选择新的产品 （生成） 将导致回发时，更新 GridView ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image30.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-166">**Figure 10**: Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the GridView ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image30.png))</span></span>


## <a name="adding-a----choose-a-category----list-item"></a><span data-ttu-id="cb132-167">添加"-选择一个类别-"列表项</span><span class="sxs-lookup"><span data-stu-id="cb132-167">Adding a "-- Choose a Category --" List Item</span></span>

<span data-ttu-id="cb132-168">在第一次访问时`FilterByDropDownList.aspx`页上的 DropDownList 的第一个列表项 （饮料） 选择默认情况下，在 GridView 显示饮料产品的类别。</span><span class="sxs-lookup"><span data-stu-id="cb132-168">When first visiting the `FilterByDropDownList.aspx` page the categories DropDownList's first list item (Beverages) is selected by default, showing the beverage products in the GridView.</span></span> <span data-ttu-id="cb132-169">而不是显示第一个类别的产品，我们可能想要改为让 DropDownList 项选择该列表将显示为类似，"-选择一个类别-"。</span><span class="sxs-lookup"><span data-stu-id="cb132-169">Rather than showing the first category's products, we may want to instead have a DropDownList item selected that says something like, "-- Choose a Category --".</span></span>

<span data-ttu-id="cb132-170">若要将新的列表项添加到下拉列表中，转到属性窗口，然后单击中的省略号`Items`属性。</span><span class="sxs-lookup"><span data-stu-id="cb132-170">To add a new list item to the DropDownList, go to the Properties window and click on the ellipses in the `Items` property.</span></span> <span data-ttu-id="cb132-171">添加新列表项与`Text`"-选择一个类别-"和`Value` `-1`。</span><span class="sxs-lookup"><span data-stu-id="cb132-171">Add a new list item with the `Text` "-- Choose a Category --" and the `Value` `-1`.</span></span>


<span data-ttu-id="cb132-172">[![添加 a — 选择列表项的类别-](master-detail-filtering-with-a-dropdownlist-cs/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-172">[![Add a -- Choose a Category -- List Item](master-detail-filtering-with-a-dropdownlist-cs/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image31.png)</span></span>

<span data-ttu-id="cb132-173">**图 11**： 添加-选择列表项的类别-([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image33.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-173">**Figure 11**: Add a -- Choose a Category -- List Item ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image33.png))</span></span>


<span data-ttu-id="cb132-174">或者，你可以通过将以下标记添加到下拉列表添加列表项：</span><span class="sxs-lookup"><span data-stu-id="cb132-174">Alternatively, you can add the list item by adding the following markup to the DropDownList:</span></span>

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample1.aspx)]

<span data-ttu-id="cb132-175">此外，我们需要将设置的 DropDownList 控件的`AppendDataBoundItems`设为 True，因为当类别所绑定到的下拉列表从 ObjectDataSource 时它们将覆盖任何手动添加列表项，如果`AppendDataBoundItems`不 True。</span><span class="sxs-lookup"><span data-stu-id="cb132-175">Additionally, we need to set the DropDownList control's `AppendDataBoundItems` to True because when the categories are bound to the DropDownList from the ObjectDataSource they'll overwrite any manually-added list items if `AppendDataBoundItems` isn't True.</span></span>


![AppendDataBoundItems 属性设置为 True](master-detail-filtering-with-a-dropdownlist-cs/_static/image34.png)

<span data-ttu-id="cb132-177">**图 12**： 设置`AppendDataBoundItems`属性为 True</span><span class="sxs-lookup"><span data-stu-id="cb132-177">**Figure 12**: Set the `AppendDataBoundItems` Property to True</span></span>


<span data-ttu-id="cb132-178">之后这些更改，当第一次访问的页面的"-选择一个类别-"选项，并且不显示任何产品时。</span><span class="sxs-lookup"><span data-stu-id="cb132-178">After these changes, when first visiting the page the "-- Choose a Category --" option is selected and no products are displayed.</span></span>


<span data-ttu-id="cb132-179">[![在初始页面加载显示要安装的产品](master-detail-filtering-with-a-dropdownlist-cs/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-179">[![On the Initial Page Load No Products are Displayed](master-detail-filtering-with-a-dropdownlist-cs/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image35.png)</span></span>

<span data-ttu-id="cb132-180">**图 13**： 显示在初始页负载否产品 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image37.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-180">**Figure 13**: On the Initial Page Load No Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image37.png))</span></span>


<span data-ttu-id="cb132-181">因为"-选择一个类别-"列表项被选中时显示任何产品的原因是因为其值是`-1`和与数据库中有任何产品`CategoryID`的`-1`。</span><span class="sxs-lookup"><span data-stu-id="cb132-181">The reason no products are displayed when because the "-- Choose a Category --" list item is selected is because its value is `-1` and there are no products in the database with a `CategoryID` of `-1`.</span></span> <span data-ttu-id="cb132-182">如果这是你想要然后完此时的行为 ！</span><span class="sxs-lookup"><span data-stu-id="cb132-182">If this is the behavior you want then you're done at this point!</span></span> <span data-ttu-id="cb132-183">如果，但是，你想要显示*所有*类别中的选中"-选择一个类别-"列表项时，返回到`ProductsBLL`类和自定义`GetProductsByCategoryID(categoryID)`方法，以便它时，将调用`GetProducts()`方法如果传入中*`categoryID`* 参数小于零：</span><span class="sxs-lookup"><span data-stu-id="cb132-183">If, however, you want to display *all* of the categories when the "-- Choose a Category --" list item is selected, return to the `ProductsBLL` class and customize the `GetProductsByCategoryID(categoryID)` method so that it invokes the `GetProducts()` method if the passed in *`categoryID`* parameter is less than zero:</span></span>

[!code-csharp[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample2.cs)]

<span data-ttu-id="cb132-184">此处使用的方法是通过类似于我们用来显示所有供应商的方法返回[声明性参数](../basic-reporting/declarative-parameters-cs.md)教程，虽然此示例中，我们将使用值为`-1`以指示应为所有记录相对于检索`null`。</span><span class="sxs-lookup"><span data-stu-id="cb132-184">The technique used here is similar to the approach we used to display all suppliers back in the [Declarative Parameters](../basic-reporting/declarative-parameters-cs.md) tutorial, although for this example we're using a value of `-1` to indicate that all records should be retrieved as opposed to `null`.</span></span> <span data-ttu-id="cb132-185">这是因为*`categoryID`* 参数`GetProductsByCategoryID(categoryID)`方法要求为整数值通过在中，而声明性的参数教程中我们已传递的字符串输入参数中。</span><span class="sxs-lookup"><span data-stu-id="cb132-185">This is because the *`categoryID`* parameter of the `GetProductsByCategoryID(categoryID)` method expects as integer value passed in, whereas in the Declarative Parameters tutorial we were passing in a string input parameter.</span></span>

<span data-ttu-id="cb132-186">图 14 显示的屏幕截图`FilterByDropDownList.aspx`如果选择"-选择一个类别-"选项。</span><span class="sxs-lookup"><span data-stu-id="cb132-186">Figure 14 shows a screen shot of `FilterByDropDownList.aspx` when the "-- Choose a Category --" option is selected.</span></span> <span data-ttu-id="cb132-187">在这里，默认情况下，将显示所有产品，用户可以通过选择特定类别，缩小显示。</span><span class="sxs-lookup"><span data-stu-id="cb132-187">Here, all of the products are displayed by default, and the user can narrow the display by choosing a specific category.</span></span>


<span data-ttu-id="cb132-188">[![所有产品都现在列出默认情况下](master-detail-filtering-with-a-dropdownlist-cs/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image38.png)</span><span class="sxs-lookup"><span data-stu-id="cb132-188">[![All of the Products are Now Listed By Default](master-detail-filtering-with-a-dropdownlist-cs/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image38.png)</span></span>

<span data-ttu-id="cb132-189">**图 14**： 所有产品都现在列出默认情况下 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image40.png))</span><span class="sxs-lookup"><span data-stu-id="cb132-189">**Figure 14**: All of the Products are Now Listed By Default ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image40.png))</span></span>


## <a name="summary"></a><span data-ttu-id="cb132-190">总结</span><span class="sxs-lookup"><span data-stu-id="cb132-190">Summary</span></span>

<span data-ttu-id="cb132-191">显示按层次结构相关的数据时，它通常有助于呈现使用主/详细信息报表，用户可以从中启动浏览的层次结构中按自上而下的数据以及向下钻取详细信息数据。</span><span class="sxs-lookup"><span data-stu-id="cb132-191">When displaying hierarchically-related data, it often helps to present the data using master/detail reports, from which the user can start perusing the data from the top of the hierarchy and drill down into details.</span></span> <span data-ttu-id="cb132-192">在本教程中，我们探讨生成一个简单的主/详细信息报告，显示所选的类别的产品。</span><span class="sxs-lookup"><span data-stu-id="cb132-192">In this tutorial we examined building a simple master/detail report showing a selected category's products.</span></span> <span data-ttu-id="cb132-193">这是使用完成的 DropDownList 的类别和一个 GridView 属于所选类别的产品的列表。</span><span class="sxs-lookup"><span data-stu-id="cb132-193">This was accomplished by using a DropDownList for the list of categories and a GridView for the products belonging to the selected category.</span></span>

<span data-ttu-id="cb132-194">在[下一教程](master-detail-filtering-with-two-dropdownlists-cs.md)我们将进一步的 DropDownList 接口一个步骤，使用两个 DropDownLists。</span><span class="sxs-lookup"><span data-stu-id="cb132-194">In the [next tutorial](master-detail-filtering-with-two-dropdownlists-cs.md) we'll take the DropDownList interface one step further, using two DropDownLists.</span></span>

<span data-ttu-id="cb132-195">尽情享受编程 ！</span><span class="sxs-lookup"><span data-stu-id="cb132-195">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="cb132-196">关于作者</span><span class="sxs-lookup"><span data-stu-id="cb132-196">About the Author</span></span>

<span data-ttu-id="cb132-197">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的七个 ASP/ASP.NET 书籍和的创始人[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年使用与 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="cb132-197">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="cb132-198">Scott 的作用是作为独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="cb132-198">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="cb132-199">最新书籍是[ *Sam 教授自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="cb132-199">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="cb132-200">他可以达到在[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)或通过他的博客，其中可以找到在[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="cb132-200">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="cb132-201">下一篇</span><span class="sxs-lookup"><span data-stu-id="cb132-201">Next</span></span>](master-detail-filtering-with-two-dropdownlists-cs.md)
