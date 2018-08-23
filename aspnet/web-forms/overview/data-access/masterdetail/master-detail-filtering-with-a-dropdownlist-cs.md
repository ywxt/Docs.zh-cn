---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
title: 使用 DropDownList (C#) 进行筛选母版/详细信息 |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将了解如何在 DropDownList 控件和 GridView 中的所选的列表项的详细信息中显示的主记录。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 53e659cc-eefb-40c1-a1dc-559481c99443
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
msc.type: authoredcontent
ms.openlocfilehash: a2d7a27a8bf9da365e4f48d7ca2d9d902ec4a5ba
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831087"
---
<a name="masterdetail-filtering-with-a-dropdownlist-c"></a><span data-ttu-id="4f802-103">使用 DropDownList (C#) 进行筛选母版/详细信息</span><span class="sxs-lookup"><span data-stu-id="4f802-103">Master/Detail Filtering With a DropDownList (C#)</span></span>
====================
<span data-ttu-id="4f802-104">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="4f802-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="4f802-105">[下载示例应用程序](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_7_CS.exe)或[下载 PDF](master-detail-filtering-with-a-dropdownlist-cs/_static/datatutorial07cs1.pdf)</span><span class="sxs-lookup"><span data-stu-id="4f802-105">[Download Sample App](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_7_CS.exe) or [Download PDF](master-detail-filtering-with-a-dropdownlist-cs/_static/datatutorial07cs1.pdf)</span></span>

> <span data-ttu-id="4f802-106">在本教程中我们将了解如何在 DropDownList 控件和 GridView 中的所选的列表项的详细信息中显示的主记录。</span><span class="sxs-lookup"><span data-stu-id="4f802-106">In this tutorial we'll see how to display the master records in a DropDownList control and the details of the selected list item in a GridView.</span></span>


## <a name="introduction"></a><span data-ttu-id="4f802-107">介绍</span><span class="sxs-lookup"><span data-stu-id="4f802-107">Introduction</span></span>

<span data-ttu-id="4f802-108">报表的通用类型是*母版/详细信息报表*中的报表开始通过显示某些组的"主"的记录。</span><span class="sxs-lookup"><span data-stu-id="4f802-108">A common type of report is the *master/detail report*, in which the report begins by showing some set of "master" records.</span></span> <span data-ttu-id="4f802-109">用户可以然后向下钻取到一个主机记录，从而查看该主记录的"详细信息。"</span><span class="sxs-lookup"><span data-stu-id="4f802-109">The user can then drill down into one of the master records, thereby viewing that master record's "details."</span></span> <span data-ttu-id="4f802-110">母版/详细信息报告是用于可视化一对多关系，如报表的理想之选显示所有类别，并允许用户选择特定的类别并显示其相关联的产品。</span><span class="sxs-lookup"><span data-stu-id="4f802-110">Master/detail reports are an ideal choice for visualizing one-to-many relationships, such as a report showing all of the categories and then allowing a user to select a particular category and display its associated products.</span></span> <span data-ttu-id="4f802-111">此外，母版/详细信息报表可用于显示来自特别"宽型"表 （是有大量的列） 的详细的信息。</span><span class="sxs-lookup"><span data-stu-id="4f802-111">Additionally, master/detail reports are useful for displaying detailed information from particularly "wide" tables (ones that have a lot of columns).</span></span> <span data-ttu-id="4f802-112">例如，母版/详细信息报表的"主"级别可能会显示在数据库中，只是产品名称和单位产品的价格并向下钻取特定产品会显示其他产品字段 (类别、 供应商、 每个单元，数量和等）。</span><span class="sxs-lookup"><span data-stu-id="4f802-112">For example, the "master" level of a master/detail report might show just the product name and unit price of the products in the database, and drilling down into a particular product would show the additional product fields (category, supplier, quantity per unit, and so on).</span></span>

<span data-ttu-id="4f802-113">有许多方法可以用于实现母版/详细信息报表。</span><span class="sxs-lookup"><span data-stu-id="4f802-113">There are many ways with which a master/detail report can be implemented.</span></span> <span data-ttu-id="4f802-114">通过这和接下来三个教程中，我们将介绍在不同的母版/详细信息报表。</span><span class="sxs-lookup"><span data-stu-id="4f802-114">Over this and the next three tutorials we'll look at a variety of master/detail reports.</span></span> <span data-ttu-id="4f802-115">在本教程中，我们将了解如何显示中的主记录[DropDownList 控件](https://msdn.microsoft.com/library/dtx91y0z.aspx)和 GridView 中的所选的列表项的详细信息。</span><span class="sxs-lookup"><span data-stu-id="4f802-115">In this tutorial we'll see how to display the master records in a [DropDownList control](https://msdn.microsoft.com/library/dtx91y0z.aspx) and the details of the selected list item in a GridView.</span></span> <span data-ttu-id="4f802-116">具体而言，本教程中的母版/详细信息报告将列出类别和产品信息。</span><span class="sxs-lookup"><span data-stu-id="4f802-116">In particular, this tutorial's master/detail report will list category and product information.</span></span>

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a><span data-ttu-id="4f802-117">步骤 1： 在 DropDownList 中显示类别</span><span class="sxs-lookup"><span data-stu-id="4f802-117">Step 1: Displaying the Categories in a DropDownList</span></span>

<span data-ttu-id="4f802-118">我们的母版/详细信息报表将列出与所选的列表项的产品显示在下拉列表中，类别在 GridView 的页中进一步向下。</span><span class="sxs-lookup"><span data-stu-id="4f802-118">Our master/detail report will list the categories in a DropDownList, with the selected list item's products displayed further down in the page in a GridView.</span></span> <span data-ttu-id="4f802-119">然后，领先于我们的第一个任务是已在 DropDownList 中显示的类别。</span><span class="sxs-lookup"><span data-stu-id="4f802-119">The first task ahead of us, then, is to have the categories displayed in a DropDownList.</span></span> <span data-ttu-id="4f802-120">打开`FilterByDropDownList.aspx`页中`Filtering`文件夹中，从工具箱拖到页面的设计器中，将在 DropDownList 上并设置其`ID`属性设置为`Categories`。</span><span class="sxs-lookup"><span data-stu-id="4f802-120">Open the `FilterByDropDownList.aspx` page in the `Filtering` folder, drag on a DropDownList from the Toolbox onto the page's designer, and set its `ID` property to `Categories`.</span></span> <span data-ttu-id="4f802-121">接下来，单击选择数据源链接从 DropDownList 的智能标记。</span><span class="sxs-lookup"><span data-stu-id="4f802-121">Next, click on the Choose Data Source link from the DropDownList's smart tag.</span></span> <span data-ttu-id="4f802-122">这将显示数据源配置向导。</span><span class="sxs-lookup"><span data-stu-id="4f802-122">This will display the Data Source Configuration wizard.</span></span>


<span data-ttu-id="4f802-123">[![指定 DropDownList 的数据源](master-detail-filtering-with-a-dropdownlist-cs/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-123">[![Specify the DropDownList's Data Source](master-detail-filtering-with-a-dropdownlist-cs/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="4f802-124">**图 1**： 指定 DropDownList 的数据源 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-124">**Figure 1**: Specify the DropDownList's Data Source ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image3.png))</span></span>


<span data-ttu-id="4f802-125">选择将添加名为新 ObjectDataSource `CategoriesDataSource` ，它调用`CategoriesBLL`类的`GetCategories()`方法。</span><span class="sxs-lookup"><span data-stu-id="4f802-125">Choose to add a new ObjectDataSource named `CategoriesDataSource` that invokes the `CategoriesBLL` class's `GetCategories()` method.</span></span>


<span data-ttu-id="4f802-126">[![添加名为 CategoriesDataSource 新 ObjectDataSource](master-detail-filtering-with-a-dropdownlist-cs/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-126">[![Add a New ObjectDataSource Named CategoriesDataSource](master-detail-filtering-with-a-dropdownlist-cs/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image4.png)</span></span>

<span data-ttu-id="4f802-127">**图 2**： 添加新对象数据源名为`CategoriesDataSource`([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-127">**Figure 2**: Add a New ObjectDataSource Named `CategoriesDataSource` ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image6.png))</span></span>


<span data-ttu-id="4f802-128">[![选择使用 CategoriesBLL 类](master-detail-filtering-with-a-dropdownlist-cs/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-128">[![Choose to Use the CategoriesBLL Class](master-detail-filtering-with-a-dropdownlist-cs/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image7.png)</span></span>

<span data-ttu-id="4f802-129">**图 3**： 选择使用`CategoriesBLL`类 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-129">**Figure 3**: Choose to Use the `CategoriesBLL` Class ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image9.png))</span></span>


<span data-ttu-id="4f802-130">[![配置对象数据源使用 GetCategories() 方法](master-detail-filtering-with-a-dropdownlist-cs/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-130">[![Configure the ObjectDataSource to Use the GetCategories() Method](master-detail-filtering-with-a-dropdownlist-cs/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image10.png)</span></span>

<span data-ttu-id="4f802-131">**图 4**： 配置为使用 ObjectDataSource`GetCategories()`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-131">**Figure 4**: Configure the ObjectDataSource to Use the `GetCategories()` Method ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image12.png))</span></span>


<span data-ttu-id="4f802-132">配置的 ObjectDataSource 我们仍然需要指定应在 DropDownList 中显示哪些数据源字段和后一个应为列表项的值相关联。</span><span class="sxs-lookup"><span data-stu-id="4f802-132">After configuring the ObjectDataSource we still need to specify what data source field should be displayed in DropDownList and which one should be associated as the value for the list item.</span></span> <span data-ttu-id="4f802-133">具有`CategoryName`字段与显示和`CategoryID`为每个列表项的值。</span><span class="sxs-lookup"><span data-stu-id="4f802-133">Have the `CategoryName` field as the display and `CategoryID` as the value for each list item.</span></span>


<span data-ttu-id="4f802-134">[![作为值的类别名称字段和使用 CategoryID 使 DropDownList 显示](master-detail-filtering-with-a-dropdownlist-cs/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-134">[![Have the DropDownList Display the CategoryName Field and Use CategoryID as the Value](master-detail-filtering-with-a-dropdownlist-cs/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image13.png)</span></span>

<span data-ttu-id="4f802-135">**图 5**： 使 DropDownList 显示`CategoryName`字段并使用`CategoryID`作为值 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-135">**Figure 5**: Have the DropDownList Display the `CategoryName` Field and Use `CategoryID` as the Value ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image15.png))</span></span>


<span data-ttu-id="4f802-136">现在我们有从记录将填充 DropDownList 控件`Categories`表 （全部在大约六秒钟内完成）。</span><span class="sxs-lookup"><span data-stu-id="4f802-136">At this point we have a DropDownList control that's populated with the records from the `Categories` table (all accomplished in about six seconds).</span></span> <span data-ttu-id="4f802-137">图 6 显示了我们到目前为止的浏览器查看时。</span><span class="sxs-lookup"><span data-stu-id="4f802-137">Figure 6 shows our progress thus far when viewed through a browser.</span></span>


<span data-ttu-id="4f802-138">[![下拉列表列出了当前类别](master-detail-filtering-with-a-dropdownlist-cs/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-138">[![A Drop-Down Lists the Current Categories](master-detail-filtering-with-a-dropdownlist-cs/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image16.png)</span></span>

<span data-ttu-id="4f802-139">**图 6**: 下拉列表列出了当前类别 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-139">**Figure 6**: A Drop-Down Lists the Current Categories ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image18.png))</span></span>


## <a name="step-2-adding-the-products-gridview"></a><span data-ttu-id="4f802-140">步骤 2： 添加产品 GridView</span><span class="sxs-lookup"><span data-stu-id="4f802-140">Step 2: Adding the Products GridView</span></span>

<span data-ttu-id="4f802-141">我们的母版/详细信息报表的最后一步是列出与所选类别关联的产品。</span><span class="sxs-lookup"><span data-stu-id="4f802-141">That last step in our master/detail report is to list the products associated with the selected category.</span></span> <span data-ttu-id="4f802-142">若要完成此操作，向页添加 GridView 并创建名为新 ObjectDataSource `productsDataSource`。</span><span class="sxs-lookup"><span data-stu-id="4f802-142">To accomplish this, add a GridView to the page and create a new ObjectDataSource named `productsDataSource`.</span></span> <span data-ttu-id="4f802-143">具有`productsDataSource`控件中搜集从其数据`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。</span><span class="sxs-lookup"><span data-stu-id="4f802-143">Have the `productsDataSource` control cull its data from the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method.</span></span>


<span data-ttu-id="4f802-144">[![选择 GetProductsByCategoryID(categoryID) 方法](master-detail-filtering-with-a-dropdownlist-cs/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-144">[![Select the GetProductsByCategoryID(categoryID) Method](master-detail-filtering-with-a-dropdownlist-cs/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image19.png)</span></span>

<span data-ttu-id="4f802-145">**图 7**： 选择`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-145">**Figure 7**: Select the `GetProductsByCategoryID(categoryID)` Method ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image21.png))</span></span>


<span data-ttu-id="4f802-146">选择此方法之后, 该 ObjectDataSource 向导会提示我们的方法的值*`categoryID`* 参数。</span><span class="sxs-lookup"><span data-stu-id="4f802-146">After choosing this method, the ObjectDataSource wizard prompts us for the value for the method's *`categoryID`* parameter.</span></span> <span data-ttu-id="4f802-147">若要使用的所选的值`categories`DropDownList 项设置参数源为控件和到 ControlID `Categories`。</span><span class="sxs-lookup"><span data-stu-id="4f802-147">To use the value of the selected `categories` DropDownList item set the Parameter source to Control and the ControlID to `Categories`.</span></span>


<span data-ttu-id="4f802-148">[![将类别 id 参数设置为 Categories DropDownList 的值](master-detail-filtering-with-a-dropdownlist-cs/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-148">[![Set the categoryID Parameter to the Value of the Categories DropDownList](master-detail-filtering-with-a-dropdownlist-cs/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image22.png)</span></span>

<span data-ttu-id="4f802-149">**图 8**： 设置*`categoryID`* 的值的参数`Categories`DropDownList ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-149">**Figure 8**: Set the *`categoryID`* Parameter to the Value of the `Categories` DropDownList ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image24.png))</span></span>


<span data-ttu-id="4f802-150">请花费片刻时间来了解我们在浏览器中的进度。</span><span class="sxs-lookup"><span data-stu-id="4f802-150">Take a moment to check out our progress in a browser.</span></span> <span data-ttu-id="4f802-151">当首次访问的页面，这些产品属于所选类别 （饮料） 会显示 （如图 9 中所示），但更改 DropDownList 不会更新数据。</span><span class="sxs-lookup"><span data-stu-id="4f802-151">When first visiting the page, those products belong to the selected category (Beverages) are displayed (as shown in Figure 9), but changing the DropDownList doesn't update the data.</span></span> <span data-ttu-id="4f802-152">这是因为必须 GridView 来更新在回发。</span><span class="sxs-lookup"><span data-stu-id="4f802-152">This is because a postback must occur for the GridView to update.</span></span> <span data-ttu-id="4f802-153">若要实现此目的我们具有两个选项 （这两者都不需要编写任何代码）：</span><span class="sxs-lookup"><span data-stu-id="4f802-153">To accomplish this we have two options (neither of which requires writing any code):</span></span>

- <span data-ttu-id="4f802-154">**设置类别 DropDownList 的**[AutoPostBack 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**为 True。**</span><span class="sxs-lookup"><span data-stu-id="4f802-154">**Set the categories DropDownList's**[AutoPostBack property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**to True.**</span></span> <span data-ttu-id="4f802-155">（您可以实现此目的通过检查 DropDownList 的智能标记中的启用自动回发选项。）这会触发回发，只要 DropDownList 的选中用户更改项。</span><span class="sxs-lookup"><span data-stu-id="4f802-155">(You can accomplish this by checking the Enable AutoPostBack option in the DropDownList's smart tag.) This will trigger a postback whenever the DropDownList's selected item is changed by the user.</span></span> <span data-ttu-id="4f802-156">因此，当用户从下拉列表中选择新类别时回发将会随之发生，并将使用新选择的类别的产品更新 GridView。</span><span class="sxs-lookup"><span data-stu-id="4f802-156">Therefore, when the user selects a new category from the DropDownList a postback will ensue and the GridView will be updated with the products for the newly selected category.</span></span> <span data-ttu-id="4f802-157">（这是我在本教程中使用的方法）。</span><span class="sxs-lookup"><span data-stu-id="4f802-157">(This is the approach I've used in this tutorial.)</span></span>
- <span data-ttu-id="4f802-158">**添加一个按钮 Web 控件旁边 DropDownList。**</span><span class="sxs-lookup"><span data-stu-id="4f802-158">**Add a Button Web control next to the DropDownList.**</span></span> <span data-ttu-id="4f802-159">设置其`Text`刷新属性或类似的内容。</span><span class="sxs-lookup"><span data-stu-id="4f802-159">Set its `Text` property to Refresh or something similar.</span></span> <span data-ttu-id="4f802-160">使用此方法时，用户将需要选择新类别，然后单击该按钮。</span><span class="sxs-lookup"><span data-stu-id="4f802-160">With this approach, the user will need to select a new category and then click the Button.</span></span> <span data-ttu-id="4f802-161">单击按钮将会导致回发，并更新 GridView，其中列出所选类别的产品。</span><span class="sxs-lookup"><span data-stu-id="4f802-161">Clicking the Button will cause a postback and update the GridView to list those products of the selected category.</span></span>

<span data-ttu-id="4f802-162">图 9 和 10 说明了操作中的母版/详细信息报表。</span><span class="sxs-lookup"><span data-stu-id="4f802-162">Figures 9 and 10 illustrate the master/detail report in action.</span></span>


<span data-ttu-id="4f802-163">[![当首次访问的页面，显示饮料产品](master-detail-filtering-with-a-dropdownlist-cs/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-163">[![When First Visiting the Page, the Beverage Products are Displayed](master-detail-filtering-with-a-dropdownlist-cs/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image25.png)</span></span>

<span data-ttu-id="4f802-164">**图 9**： 当首次访问的页面，显示饮料产品 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-164">**Figure 9**: When First Visiting the Page, the Beverage Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image27.png))</span></span>


<span data-ttu-id="4f802-165">[![选择一种新产品 （生成） 将自动导致回发，更新 GridView](master-detail-filtering-with-a-dropdownlist-cs/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-165">[![Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the GridView](master-detail-filtering-with-a-dropdownlist-cs/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image28.png)</span></span>

<span data-ttu-id="4f802-166">**图 10**： 选择一种新产品 （生成） 将自动导致回发，更新 GridView ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image30.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-166">**Figure 10**: Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the GridView ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image30.png))</span></span>


## <a name="adding-a----choose-a-category----list-item"></a><span data-ttu-id="4f802-167">添加"--选择一个类别-"列表项</span><span class="sxs-lookup"><span data-stu-id="4f802-167">Adding a "-- Choose a Category --" List Item</span></span>

<span data-ttu-id="4f802-168">首次访问时`FilterByDropDownList.aspx`页 DropDownList 的第一个列表项 （饮料） 选择默认情况下，在 GridView 中显示的饮料产品的类别。</span><span class="sxs-lookup"><span data-stu-id="4f802-168">When first visiting the `FilterByDropDownList.aspx` page the categories DropDownList's first list item (Beverages) is selected by default, showing the beverage products in the GridView.</span></span> <span data-ttu-id="4f802-169">而不是显示第一个类别的产品，我们可能想要改为具有 DropDownList 项选择的显示类似于"--选择一个类别-"的内容。</span><span class="sxs-lookup"><span data-stu-id="4f802-169">Rather than showing the first category's products, we may want to instead have a DropDownList item selected that says something like, "-- Choose a Category --".</span></span>

<span data-ttu-id="4f802-170">若要向 DropDownList 添加新列表项，请转到属性窗口，然后单击中的椭圆`Items`属性。</span><span class="sxs-lookup"><span data-stu-id="4f802-170">To add a new list item to the DropDownList, go to the Properties window and click on the ellipses in the `Items` property.</span></span> <span data-ttu-id="4f802-171">添加的新列表项`Text`"--选择一个类别-"和`Value` `-1`。</span><span class="sxs-lookup"><span data-stu-id="4f802-171">Add a new list item with the `Text` "-- Choose a Category --" and the `Value` `-1`.</span></span>


<span data-ttu-id="4f802-172">[![添加--选择列表项的 Category-](master-detail-filtering-with-a-dropdownlist-cs/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-172">[![Add a -- Choose a Category -- List Item](master-detail-filtering-with-a-dropdownlist-cs/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image31.png)</span></span>

<span data-ttu-id="4f802-173">**图 11**： 添加--列表项中选择一个类别-([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image33.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-173">**Figure 11**: Add a -- Choose a Category -- List Item ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image33.png))</span></span>


<span data-ttu-id="4f802-174">或者，可以通过将以下标记添加到下拉列表添加列表项：</span><span class="sxs-lookup"><span data-stu-id="4f802-174">Alternatively, you can add the list item by adding the following markup to the DropDownList:</span></span>

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample1.aspx)]

<span data-ttu-id="4f802-175">此外，我们需要设置 DropDownList 控件`AppendDataBoundItems`设为 True，因为从 ObjectDataSource 类别绑定到 DropDownList 时它们将覆盖任何手动添加列表项，如果`AppendDataBoundItems`不是 True。</span><span class="sxs-lookup"><span data-stu-id="4f802-175">Additionally, we need to set the DropDownList control's `AppendDataBoundItems` to True because when the categories are bound to the DropDownList from the ObjectDataSource they'll overwrite any manually-added list items if `AppendDataBoundItems` isn't True.</span></span>


![AppendDataBoundItems 属性设置为 True](master-detail-filtering-with-a-dropdownlist-cs/_static/image34.png)

<span data-ttu-id="4f802-177">**图 12**： 设置`AppendDataBoundItems`属性设为 True</span><span class="sxs-lookup"><span data-stu-id="4f802-177">**Figure 12**: Set the `AppendDataBoundItems` Property to True</span></span>


<span data-ttu-id="4f802-178">之后这些更改，首次访问的页面选择"--选择一个类别-"选项并不显示任何产品时。</span><span class="sxs-lookup"><span data-stu-id="4f802-178">After these changes, when first visiting the page the "-- Choose a Category --" option is selected and no products are displayed.</span></span>


<span data-ttu-id="4f802-179">[![无产品都会显示在加载初始页](master-detail-filtering-with-a-dropdownlist-cs/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-179">[![On the Initial Page Load No Products are Displayed](master-detail-filtering-with-a-dropdownlist-cs/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image35.png)</span></span>

<span data-ttu-id="4f802-180">**图 13**： 显示在初始页面负载否产品 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image37.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-180">**Figure 13**: On the Initial Page Load No Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image37.png))</span></span>


<span data-ttu-id="4f802-181">因为选择了"--选择一个类别-"列表项时显示任何产品的原因是它的值是`-1`并且与数据库中有任何产品`CategoryID`的`-1`。</span><span class="sxs-lookup"><span data-stu-id="4f802-181">The reason no products are displayed when because the "-- Choose a Category --" list item is selected is because its value is `-1` and there are no products in the database with a `CategoryID` of `-1`.</span></span> <span data-ttu-id="4f802-182">如果这是你想在此时完成，然后的行为 ！</span><span class="sxs-lookup"><span data-stu-id="4f802-182">If this is the behavior you want then you're done at this point!</span></span> <span data-ttu-id="4f802-183">如果你想要显示的但是*所有*个类别时选择"--选择一个类别-"列表项时，返回到`ProductsBLL`类和自定义`GetProductsByCategoryID(categoryID)`方法，使其调用`GetProducts()`方法如果传递中*`categoryID`* 参数小于零：</span><span class="sxs-lookup"><span data-stu-id="4f802-183">If, however, you want to display *all* of the categories when the "-- Choose a Category --" list item is selected, return to the `ProductsBLL` class and customize the `GetProductsByCategoryID(categoryID)` method so that it invokes the `GetProducts()` method if the passed in *`categoryID`* parameter is less than zero:</span></span>

[!code-csharp[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample2.cs)]

<span data-ttu-id="4f802-184">此处使用的方法是类似于我们用来显示所有供应商的方法返回[声明性参数](../basic-reporting/declarative-parameters-cs.md)教程中，尽管我们对于此示例使用的值为`-1`指示应在所有记录而不是检索`null`。</span><span class="sxs-lookup"><span data-stu-id="4f802-184">The technique used here is similar to the approach we used to display all suppliers back in the [Declarative Parameters](../basic-reporting/declarative-parameters-cs.md) tutorial, although for this example we're using a value of `-1` to indicate that all records should be retrieved as opposed to `null`.</span></span> <span data-ttu-id="4f802-185">这是因为*`categoryID`* 参数的`GetProductsByCategoryID(categoryID)`方法需要作为整数值传递，而声明性参数教程中我们已传入的字符串输入参数。</span><span class="sxs-lookup"><span data-stu-id="4f802-185">This is because the *`categoryID`* parameter of the `GetProductsByCategoryID(categoryID)` method expects as integer value passed in, whereas in the Declarative Parameters tutorial we were passing in a string input parameter.</span></span>

<span data-ttu-id="4f802-186">图 14 显示了的屏幕截图`FilterByDropDownList.aspx`如果选择"--选择一个类别-"选项。</span><span class="sxs-lookup"><span data-stu-id="4f802-186">Figure 14 shows a screen shot of `FilterByDropDownList.aspx` when the "-- Choose a Category --" option is selected.</span></span> <span data-ttu-id="4f802-187">在这里，默认情况下显示的所有产品，用户可以通过选择特定类别，缩小显示。</span><span class="sxs-lookup"><span data-stu-id="4f802-187">Here, all of the products are displayed by default, and the user can narrow the display by choosing a specific category.</span></span>


<span data-ttu-id="4f802-188">[![所有产品都现在列出默认情况下](master-detail-filtering-with-a-dropdownlist-cs/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image38.png)</span><span class="sxs-lookup"><span data-stu-id="4f802-188">[![All of the Products are Now Listed By Default](master-detail-filtering-with-a-dropdownlist-cs/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image38.png)</span></span>

<span data-ttu-id="4f802-189">**图 14**： 所有产品都现在列出默认情况下 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-cs/_static/image40.png))</span><span class="sxs-lookup"><span data-stu-id="4f802-189">**Figure 14**: All of the Products are Now Listed By Default ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-cs/_static/image40.png))</span></span>


## <a name="summary"></a><span data-ttu-id="4f802-190">总结</span><span class="sxs-lookup"><span data-stu-id="4f802-190">Summary</span></span>

<span data-ttu-id="4f802-191">显示按层次结构相关数据时，它通常用于呈现使用主/详细信息报表，用户可以从中启动仔细阅读的层次结构顶部的数据和向下钻取到详细信息数据。</span><span class="sxs-lookup"><span data-stu-id="4f802-191">When displaying hierarchically-related data, it often helps to present the data using master/detail reports, from which the user can start perusing the data from the top of the hierarchy and drill down into details.</span></span> <span data-ttu-id="4f802-192">在本教程中，我们探讨构建一个简单的母版/详细信息报告，显示所选的类别的产品。</span><span class="sxs-lookup"><span data-stu-id="4f802-192">In this tutorial we examined building a simple master/detail report showing a selected category's products.</span></span> <span data-ttu-id="4f802-193">这被通过使用 DropDownList 的类别和 GridView 属于所选类别的产品列表。</span><span class="sxs-lookup"><span data-stu-id="4f802-193">This was accomplished by using a DropDownList for the list of categories and a GridView for the products belonging to the selected category.</span></span>

<span data-ttu-id="4f802-194">在中[下一教程](master-detail-filtering-with-two-dropdownlists-cs.md)我们将进一步 DropDownList 接口的一个步骤，使用两个 Dropdownlist。</span><span class="sxs-lookup"><span data-stu-id="4f802-194">In the [next tutorial](master-detail-filtering-with-two-dropdownlists-cs.md) we'll take the DropDownList interface one step further, using two DropDownLists.</span></span>

<span data-ttu-id="4f802-195">快乐编程 ！</span><span class="sxs-lookup"><span data-stu-id="4f802-195">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="4f802-196">关于作者</span><span class="sxs-lookup"><span data-stu-id="4f802-196">About the Author</span></span>

<span data-ttu-id="4f802-197">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="4f802-197">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="4f802-198">Scott 是独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="4f802-198">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="4f802-199">他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="4f802-199">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="4f802-200">他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="4f802-200">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="4f802-201">或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="4f802-201">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4f802-202">下一篇</span><span class="sxs-lookup"><span data-stu-id="4f802-202">Next</span></span>](master-detail-filtering-with-two-dropdownlists-cs.md)
