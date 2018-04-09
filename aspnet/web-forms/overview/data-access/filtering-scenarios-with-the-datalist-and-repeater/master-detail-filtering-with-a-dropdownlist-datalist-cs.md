---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-cs
title: 使用 DropDownList (C#) 进行筛选主/详细信息 |Microsoft 文档
author: rick-anderson
description: 在本教程中，我们将了解如何使用 DropDownLists 显示用于显示 'master' 记录和 DataList 单个 web 页中显示主/详细信息报表...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/18/2007
ms.topic: article
ms.assetid: 07fa47ae-e491-4a2f-b265-d342b9ddef46
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: c84902ccf028c976246380abfaebb6a76c573603
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="masterdetail-filtering-with-a-dropdownlist-c"></a><span data-ttu-id="8cde8-103">主/从使用 DropDownList (C#) 进行筛选</span><span class="sxs-lookup"><span data-stu-id="8cde8-103">Master/Detail Filtering With a DropDownList (C#)</span></span>
====================
<span data-ttu-id="8cde8-104">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="8cde8-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="8cde8-105">[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_CS.exe)或[下载 PDF](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/datatutorial33cs1.pdf)</span><span class="sxs-lookup"><span data-stu-id="8cde8-105">[Download Sample App](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_CS.exe) or [Download PDF](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/datatutorial33cs1.pdf)</span></span>

> <span data-ttu-id="8cde8-106">在本教程中，我们将了解如何使用 DropDownLists 以显示"主"的记录和显示的"详细信息"DataList 单个 web 页中显示主/详细信息报表。</span><span class="sxs-lookup"><span data-stu-id="8cde8-106">In this tutorial we see how to display master/detail reports in a single web page using DropDownLists to display the "master" records and a DataList to display the "details".</span></span>


## <a name="introduction"></a><span data-ttu-id="8cde8-107">介绍</span><span class="sxs-lookup"><span data-stu-id="8cde8-107">Introduction</span></span>

<span data-ttu-id="8cde8-108">主/详细信息报表，我们首先创建在早期版本中使用一个 GridView[主/详细信息筛选与 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)教程中，首先显示的"主"的记录集。</span><span class="sxs-lookup"><span data-stu-id="8cde8-108">The master/detail report, which we first created using a GridView in the earlier [Master/Detail Filtering With a DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) tutorial, begins by showing some set of "master" records.</span></span> <span data-ttu-id="8cde8-109">用户可以然后向下钻取一个主机记录，从而查看该主记录的"详细信息。"</span><span class="sxs-lookup"><span data-stu-id="8cde8-109">The user can then drill down into one of the master records, thereby viewing that master record's "details."</span></span> <span data-ttu-id="8cde8-110">主/详细信息报表是可视化一个对多关系以及如何显示特别"宽"的表 （一种是有大量的列） 中的详细的信息的理想选择。</span><span class="sxs-lookup"><span data-stu-id="8cde8-110">Master/detail reports are an ideal choice for visualizing one-to-many relationships and for displaying detailed information from particularly "wide" tables (ones that have a lot of columns).</span></span> <span data-ttu-id="8cde8-111">我们已介绍了如何实现使用在前面的教程中的 GridView 和说明控件的主/详细信息报表。</span><span class="sxs-lookup"><span data-stu-id="8cde8-111">We've explored how to implement master/detail reports using the GridView and DetailsView controls in previous tutorials.</span></span> <span data-ttu-id="8cde8-112">在本教程和后面的两个，我们将重新检查这些概念，但重点在于使用 DataList 和转发器而是控制。</span><span class="sxs-lookup"><span data-stu-id="8cde8-112">In this tutorial and the next two, we'll reexamine these concepts, but focus on using DataList and Repeater controls instead.</span></span>

<span data-ttu-id="8cde8-113">在本教程中，我们将查看使用说明包含的"主"的记录，DataList 中显示的"详细信息"的记录。</span><span class="sxs-lookup"><span data-stu-id="8cde8-113">In this tutorial, we'll look at using a DropDownList to contain the "master" records, with the "details" records displayed in a DataList.</span></span>

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a><span data-ttu-id="8cde8-114">步骤 1： 添加主/从教程 Web 页</span><span class="sxs-lookup"><span data-stu-id="8cde8-114">Step 1: Adding the Master/Detail Tutorial Web Pages</span></span>

<span data-ttu-id="8cde8-115">让我们开始本教程之前，首先我们一段时间来添加的文件夹和我们需要以及本教程后面的两个处理使用 DataList 和转发器控件的主/详细信息报表的 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="8cde8-115">Before we start this tutorial, let's first take a moment to add the folder and ASP.NET pages we'll need for this tutorial and the next two dealing with master/detail reports using the DataList and Repeater controls.</span></span> <span data-ttu-id="8cde8-116">首先创建一个新文件夹中名为的项目`DataListRepeaterFiltering`。</span><span class="sxs-lookup"><span data-stu-id="8cde8-116">Start by creating a new folder in the project named `DataListRepeaterFiltering`.</span></span> <span data-ttu-id="8cde8-117">接下来，将以下五个 ASP.NET 页添加到此文件夹中，让所有的它们配置为使用母版页`Site.master`:</span><span class="sxs-lookup"><span data-stu-id="8cde8-117">Next, add the following five ASP.NET pages to this folder, having all of them configured to use the master page `Site.master`:</span></span>

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`


![创建 DataListRepeaterFiltering 文件夹并添加教程 ASP.NET 页](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image1.png)

<span data-ttu-id="8cde8-119">**图 1**： 创建`DataListRepeaterFiltering`文件夹并添加教程 ASP.NET 页</span><span class="sxs-lookup"><span data-stu-id="8cde8-119">**Figure 1**: Create a `DataListRepeaterFiltering` Folder and Add the Tutorial ASP.NET Pages</span></span>


<span data-ttu-id="8cde8-120">接下来，打开`Default.aspx`页上，并将其拖`SectionLevelTutorialListing.ascx`从用户控件`UserControls`到设计图面上的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8cde8-120">Next, open the `Default.aspx` page and drag the `SectionLevelTutorialListing.ascx` User Control from the `UserControls` folder onto the Design surface.</span></span> <span data-ttu-id="8cde8-121">用户控件中，我们在中创建的[母版页和网站的导航](../introduction/master-pages-and-site-navigation-cs.md)教程中，枚举站点图，并会显示项目符号列表中的当前节中的教程。</span><span class="sxs-lookup"><span data-stu-id="8cde8-121">This User Control, which we created in the [Master Pages and Site Navigation](../introduction/master-pages-and-site-navigation-cs.md) tutorial, enumerates the site map and displays the tutorials from the current section in a bulleted list.</span></span>


<span data-ttu-id="8cde8-122">[![SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="8cde8-122">[![Add the SectionLevelTutorialListing.ascx User Control to Default.aspx](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image2.png)</span></span>

<span data-ttu-id="8cde8-123">**图 2**： 添加`SectionLevelTutorialListing.ascx`用户控件`Default.aspx`([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="8cde8-123">**Figure 2**: Add the `SectionLevelTutorialListing.ascx` User Control to `Default.aspx` ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image4.png))</span></span>


<span data-ttu-id="8cde8-124">为了使项目符号列表显示的主/从教程，我们将创建，我们需要将它们添加到站点图。</span><span class="sxs-lookup"><span data-stu-id="8cde8-124">In order to have the bulleted list display the master/detail tutorials we'll be creating, we need to add them to the site map.</span></span> <span data-ttu-id="8cde8-125">打开`Web.sitemap`文件，并在"显示数据与 DataList 和转发器"站点映射节点标记后添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="8cde8-125">Open the `Web.sitemap` file and add the following markup after the "Displaying Data with the DataList and Repeater" site map node markup:</span></span>

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample1.xml)]


![更新包括新的 ASP.NET 页的站点图](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image5.png)

<span data-ttu-id="8cde8-127">**图 3**： 更新包括新的 ASP.NET 页的站点图</span><span class="sxs-lookup"><span data-stu-id="8cde8-127">**Figure 3**: Update the Site Map to Include the New ASP.NET Pages</span></span>


## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a><span data-ttu-id="8cde8-128">步骤 2： 在 DropDownList 中显示的类别</span><span class="sxs-lookup"><span data-stu-id="8cde8-128">Step 2: Displaying the Categories in a DropDownList</span></span>

<span data-ttu-id="8cde8-129">主/从报表将与显示的选定的列表项的产品列出的 DropDownList 中的类别在 DataList 的页中进一步向下。</span><span class="sxs-lookup"><span data-stu-id="8cde8-129">Our master/detail report will list the categories in a DropDownList, with the selected list item's products displayed further down in the page in a DataList.</span></span> <span data-ttu-id="8cde8-130">然后，早 us，第一个任务是具有 DropDownList 中显示的类别。</span><span class="sxs-lookup"><span data-stu-id="8cde8-130">The first task ahead of us, then, is to have the categories displayed in a DropDownList.</span></span> <span data-ttu-id="8cde8-131">首先打开`FilterByDropDownList.aspx`页面`DataListRepeaterFiltering`文件夹，然后拖动 DropDownList 从工具箱拖到页面的设计器。</span><span class="sxs-lookup"><span data-stu-id="8cde8-131">Start by opening the `FilterByDropDownList.aspx` page in the `DataListRepeaterFiltering` folder and drag a DropDownList from the Toolbox onto the page's designer.</span></span> <span data-ttu-id="8cde8-132">接下来，设置的 DropDownList`ID`属性`Categories`。</span><span class="sxs-lookup"><span data-stu-id="8cde8-132">Next, set the DropDownList's `ID` property to `Categories`.</span></span> <span data-ttu-id="8cde8-133">单击下拉列表的智能标记中的选择数据源链接并创建名为新 ObjectDataSource `CategoriesDataSource`。</span><span class="sxs-lookup"><span data-stu-id="8cde8-133">Click on the Choose Data Source link from the DropDownList's smart tag and create a new ObjectDataSource named `CategoriesDataSource`.</span></span>


<span data-ttu-id="8cde8-134">[![添加名为 CategoriesDataSource 新对象数据源](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="8cde8-134">[![Add a New ObjectDataSource Named CategoriesDataSource](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image6.png)</span></span>

<span data-ttu-id="8cde8-135">**图 4**： 添加新对象数据源名为`CategoriesDataSource`([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="8cde8-135">**Figure 4**: Add a New ObjectDataSource Named `CategoriesDataSource` ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image8.png))</span></span>


<span data-ttu-id="8cde8-136">配置新对象数据源，以便它将调用`CategoriesBLL`类的`GetCategories()`方法。</span><span class="sxs-lookup"><span data-stu-id="8cde8-136">Configure the new ObjectDataSource such that it invokes the `CategoriesBLL` class's `GetCategories()` method.</span></span> <span data-ttu-id="8cde8-137">配置对象数据源，我们仍需要来指定哪些数据源字段应显示在下拉列表和后一个应为每个列表项的值关联。</span><span class="sxs-lookup"><span data-stu-id="8cde8-137">After configuring the ObjectDataSource we still need to specify what data source field should be displayed in the DropDownList and which one should be associated as the value for each list item.</span></span> <span data-ttu-id="8cde8-138">具有`CategoryName`字段作为显示和`CategoryID`作为每个列表项的值。</span><span class="sxs-lookup"><span data-stu-id="8cde8-138">Have the `CategoryName` field as the display and `CategoryID` as the value for each list item.</span></span>


<span data-ttu-id="8cde8-139">[![具有 DropDownList 显示 CategoryName 字段和使用 CategoryID 值](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="8cde8-139">[![Have the DropDownList Display the CategoryName Field and Use CategoryID as the Value](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image9.png)</span></span>

<span data-ttu-id="8cde8-140">**图 5**： 具有 DropDownList 显示`CategoryName`字段并使用`CategoryID`作为值 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image11.png))</span><span class="sxs-lookup"><span data-stu-id="8cde8-140">**Figure 5**: Have the DropDownList Display the `CategoryName` Field and Use `CategoryID` as the Value ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image11.png))</span></span>


<span data-ttu-id="8cde8-141">此时我们具有从记录将填充一个 DropDownList 控件`Categories`表 （所有在大约六个秒钟内完成）。</span><span class="sxs-lookup"><span data-stu-id="8cde8-141">At this point we have a DropDownList control that's populated with the records from the `Categories` table (all accomplished in about six seconds).</span></span> <span data-ttu-id="8cde8-142">通过浏览器查看时为止图 6 显示我们的进度。</span><span class="sxs-lookup"><span data-stu-id="8cde8-142">Figure 6 shows our progress thus far when viewed through a browser.</span></span>


<span data-ttu-id="8cde8-143">[![下拉列表将列出当前类别](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="8cde8-143">[![A Drop-Down Lists the Current Categories](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image12.png)</span></span>

<span data-ttu-id="8cde8-144">**图 6**: 下拉列表将列出当前类别 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="8cde8-144">**Figure 6**: A Drop-Down Lists the Current Categories ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image14.png))</span></span>


## <a name="step-2-adding-the-products-datalist"></a><span data-ttu-id="8cde8-145">步骤 2： 添加产品 DataList</span><span class="sxs-lookup"><span data-stu-id="8cde8-145">Step 2: Adding the Products DataList</span></span>

<span data-ttu-id="8cde8-146">主/详细信息报表的最后一步是列出与所选类别关联的产品。</span><span class="sxs-lookup"><span data-stu-id="8cde8-146">The last step in our master/detail report is to list the products associated with the selected category.</span></span> <span data-ttu-id="8cde8-147">若要完成此操作，向页面添加 DataList 并创建名为新 ObjectDataSource `ProductsByCategoryDataSource`。</span><span class="sxs-lookup"><span data-stu-id="8cde8-147">To accomplish this, add a DataList to the page and create a new ObjectDataSource named `ProductsByCategoryDataSource`.</span></span> <span data-ttu-id="8cde8-148">具有`ProductsByCategoryDataSource`控件检索从其数据`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。</span><span class="sxs-lookup"><span data-stu-id="8cde8-148">Have the `ProductsByCategoryDataSource` control retrieve its data from the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method.</span></span> <span data-ttu-id="8cde8-149">由于此主/详细信息报表是只读的则选择 (None) 选项在插入、 更新和删除选项卡中。</span><span class="sxs-lookup"><span data-stu-id="8cde8-149">Since this master/detail report is read-only, choose the (None) option in the INSERT, UPDATE, and DELETE tabs.</span></span>


<span data-ttu-id="8cde8-150">[![选择 GetProductsByCategoryID(categoryID) 方法](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="8cde8-150">[![Select the GetProductsByCategoryID(categoryID) Method](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image15.png)</span></span>

<span data-ttu-id="8cde8-151">**图 7**： 选择`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image17.png))</span><span class="sxs-lookup"><span data-stu-id="8cde8-151">**Figure 7**: Select the `GetProductsByCategoryID(categoryID)` Method ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image17.png))</span></span>


<span data-ttu-id="8cde8-152">单击下一步后, ObjectDataSource 向导将提示我们提供的值的源`GetProductsByCategoryID(categoryID)`方法的*`categoryID`*参数。</span><span class="sxs-lookup"><span data-stu-id="8cde8-152">After clicking Next, the ObjectDataSource wizard prompts us for the source of the value for the `GetProductsByCategoryID(categoryID)` method's *`categoryID`* parameter.</span></span> <span data-ttu-id="8cde8-153">若要使用的所选值`categories`DropDownList 项设置为控件和到 ControlID 参数源`Categories`。</span><span class="sxs-lookup"><span data-stu-id="8cde8-153">To use the value of the selected `categories` DropDownList item set the Parameter source to Control and the ControlID to `Categories`.</span></span>


<span data-ttu-id="8cde8-154">[![CategoryID 参数值设置为类别下拉列表](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="8cde8-154">[![Set the categoryID Parameter to the Value of the Categories DropDownList](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image18.png)</span></span>

<span data-ttu-id="8cde8-155">**图 8**： 设置*`categoryID`*参数的值`Categories`DropDownList ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="8cde8-155">**Figure 8**: Set the *`categoryID`* Parameter to the Value of the `Categories` DropDownList ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image20.png))</span></span>


<span data-ttu-id="8cde8-156">Visual Studio 将自动生成完成之后配置数据源向导，`ItemTemplate`的显示名称和值的每个数据字段 DataList。</span><span class="sxs-lookup"><span data-stu-id="8cde8-156">Upon completing the Configure Data Source wizard, Visual Studio will automatically generate an `ItemTemplate` for the DataList that displays the name and value of each data field.</span></span> <span data-ttu-id="8cde8-157">让我们增强 DataList 若要改用`ItemTemplate`显示只需产品的名称、 类别、 供应商，每个单元，并连同价格数量`SeparatorTemplate`，插入`<hr>`每个项之间的元素。</span><span class="sxs-lookup"><span data-stu-id="8cde8-157">Let's enhance the DataList to instead use an `ItemTemplate` that displays just the product's name, category, supplier, quantity per unit, and price along with a `SeparatorTemplate` that injects an `<hr>` element between each item.</span></span> <span data-ttu-id="8cde8-158">我要使用`ItemTemplate`部分中的示例从[带有 DataList 和转发器控件中显示数据](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs.md)教程中，但随意使用查找最引人注目的任何模板标记。</span><span class="sxs-lookup"><span data-stu-id="8cde8-158">I'm going to use the `ItemTemplate` from an example in the [Displaying Data with the DataList and Repeater Controls](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs.md) tutorial, but feel free to use whatever template markup you find most visually appealing.</span></span>

<span data-ttu-id="8cde8-159">进行这些更改后，你 DataList 和其 ObjectDataSource 标记应类似于以下：</span><span class="sxs-lookup"><span data-stu-id="8cde8-159">After making these changes, your DataList and its ObjectDataSource's markup should look similar to the following:</span></span>

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample2.aspx)]

<span data-ttu-id="8cde8-160">需要一段时间来签出我们的浏览器中的进度。</span><span class="sxs-lookup"><span data-stu-id="8cde8-160">Take a moment to check out our progress in a browser.</span></span> <span data-ttu-id="8cde8-161">第一次访问该页面，属于所选的类别 （饮料） 这些产品将显示 （如图 9 中所示），但更改 DropDownList 不更新的数据。</span><span class="sxs-lookup"><span data-stu-id="8cde8-161">When first visiting the page, those products belonging to the selected category (Beverages) are displayed (as shown in Figure 9), but changing the DropDownList doesn't update the data.</span></span> <span data-ttu-id="8cde8-162">这是因为 DataList 更新必须进行回发。</span><span class="sxs-lookup"><span data-stu-id="8cde8-162">This is because a postback must occur for the DataList to update.</span></span> <span data-ttu-id="8cde8-163">若要完成此我们可以设置的 DropDownList`AutoPostBack`属性`true`或向页面添加按钮 Web 控件。</span><span class="sxs-lookup"><span data-stu-id="8cde8-163">To accomplish this we can either set the DropDownList's `AutoPostBack` property to `true` or add a Button Web control to the page.</span></span> <span data-ttu-id="8cde8-164">对于本教程，我已选择要设置的 DropDownList`AutoPostBack`属性`true`。</span><span class="sxs-lookup"><span data-stu-id="8cde8-164">For this tutorial, I've opted to set the DropDownList's `AutoPostBack` property to `true`.</span></span>

<span data-ttu-id="8cde8-165">图 9 和 10 说明了操作中的主/从报表。</span><span class="sxs-lookup"><span data-stu-id="8cde8-165">Figures 9 and 10 illustrate the master/detail report in action.</span></span>


<span data-ttu-id="8cde8-166">[![第一次访问该页面，将显示饮料产品](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="8cde8-166">[![When First Visiting the Page, the Beverage Products are Displayed](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image21.png)</span></span>

<span data-ttu-id="8cde8-167">**图 9**： 第一次访问该页面，将显示饮料产品 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image23.png))</span><span class="sxs-lookup"><span data-stu-id="8cde8-167">**Figure 9**: When First Visiting the Page, the Beverage Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image23.png))</span></span>


<span data-ttu-id="8cde8-168">[![自动选择新的产品 （生成） 将导致回发时，更新 DataList](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="8cde8-168">[![Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the DataList](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image24.png)</span></span>

<span data-ttu-id="8cde8-169">**图 10**： 自动选择新的产品 （生成） 将导致回发时，更新 DataList ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="8cde8-169">**Figure 10**: Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the DataList ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image26.png))</span></span>


## <a name="adding-a----choose-a-category----list-item"></a><span data-ttu-id="8cde8-170">添加"-选择一个类别-"列表项</span><span class="sxs-lookup"><span data-stu-id="8cde8-170">Adding a "-- Choose a Category --" List Item</span></span>

<span data-ttu-id="8cde8-171">在第一次访问时`FilterByDropDownList.aspx`页上的 DropDownList 的第一个列表项 （饮料） 选择默认情况下，在 DataList 显示饮料产品的类别。</span><span class="sxs-lookup"><span data-stu-id="8cde8-171">When first visiting the `FilterByDropDownList.aspx` page the categories DropDownList's first list item (Beverages) is selected by default, showing the beverage products in the DataList.</span></span> <span data-ttu-id="8cde8-172">在*主/详细信息筛选与 DropDownList*教程，我们将"-选择一个类别-"选项添加到下拉列表，已选择默认情况下，如果选中，显示*所有*的在数据库中的产品。</span><span class="sxs-lookup"><span data-stu-id="8cde8-172">In the *Master/Detail Filtering With a DropDownList* tutorial we added a "-- Choose a Category --" option to the DropDownList that was selected by default and, when selected, displayed *all* of the products in the database.</span></span> <span data-ttu-id="8cde8-173">这种方法时可管理列出一个 GridView 中的产品时为每个产品行占用了少量的屏幕的实际空间。</span><span class="sxs-lookup"><span data-stu-id="8cde8-173">Such an approach was manageable when listing the products in a GridView, as each product row took up a small amount of screen real estate.</span></span> <span data-ttu-id="8cde8-174">与 DataList，但是，每个产品的信息将占用更大块的屏幕。</span><span class="sxs-lookup"><span data-stu-id="8cde8-174">With the DataList, however, each product's information consumes a much larger chunk of the screen.</span></span> <span data-ttu-id="8cde8-175">我们仍将添加"-选择一个类别-"选项和让它在默认情况下，选择但而不是让它显示所有产品当选中时，让我们将其配置，使之显示要安装的产品。</span><span class="sxs-lookup"><span data-stu-id="8cde8-175">Let's still add a "-- Choose a Category --" option and have it selected by default, but instead of having it show all products when selected, let's configure it so that it shows no products.</span></span>

<span data-ttu-id="8cde8-176">若要将新的列表项添加到下拉列表中，转到属性窗口，然后单击中的省略号`Items`属性。</span><span class="sxs-lookup"><span data-stu-id="8cde8-176">To add a new list item to the DropDownList, go to the Properties window and click on the ellipses in the `Items` property.</span></span> <span data-ttu-id="8cde8-177">添加新列表项与`Text`"-选择一个类别-"和`Value` `0`。</span><span class="sxs-lookup"><span data-stu-id="8cde8-177">Add a new list item with the `Text` "-- Choose a Category --" and the `Value` `0`.</span></span>


![添加](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image27.png)

<span data-ttu-id="8cde8-179">**图 11**： 添加"-选择一个类别-"列表项</span><span class="sxs-lookup"><span data-stu-id="8cde8-179">**Figure 11**: Add a "-- Choose a Category --" List Item</span></span>


<span data-ttu-id="8cde8-180">或者，你可以通过将以下标记添加到下拉列表添加列表项：</span><span class="sxs-lookup"><span data-stu-id="8cde8-180">Alternatively, you can add the list item by adding the following markup to the DropDownList:</span></span>

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample3.aspx)]

<span data-ttu-id="8cde8-181">此外，我们需要将设置的 DropDownList 控件的`AppendDataBoundItems`到`true`因为如果设置为`false`（默认值），当从 ObjectDataSource 类别绑定的 DropDownList 到时它们将会覆盖任何手动添加的列表项。</span><span class="sxs-lookup"><span data-stu-id="8cde8-181">Additionally, we need to set the DropDownList control's `AppendDataBoundItems` to `true` because if it's set to `false` (the default), when the categories are bound to the DropDownList from the ObjectDataSource they'll overwrite any manually-added list items.</span></span>


![AppendDataBoundItems 属性设置为 True](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image28.png)

<span data-ttu-id="8cde8-183">**图 12**： 设置`AppendDataBoundItems`属性为 True</span><span class="sxs-lookup"><span data-stu-id="8cde8-183">**Figure 12**: Set the `AppendDataBoundItems` Property to True</span></span>


<span data-ttu-id="8cde8-184">我们选择值的原因`0`对于"-选择一个类别-"列表项都是因为值为系统中不有任何类别`0`，选择"-选择一个类别-"列表项目时将因此返回任何产品记录。</span><span class="sxs-lookup"><span data-stu-id="8cde8-184">The reason we chose the value `0` for the "-- Choose a Category --" list item is because there are no categories in the system with a value of `0`, hence no product records will be returned when the "-- Choose a Category --" list item is selected.</span></span> <span data-ttu-id="8cde8-185">若要确认这一点，请一段时间来访问通过浏览器页面。</span><span class="sxs-lookup"><span data-stu-id="8cde8-185">To confirm this, take a moment to visit the page through a browser.</span></span> <span data-ttu-id="8cde8-186">如图 13 所示，当最初查看页面选定了"-选择一个类别-"列表项，并显示安装的产品。</span><span class="sxs-lookup"><span data-stu-id="8cde8-186">As Figure 13 shows, when initially viewing the page the "-- Choose a Category --" list item is selected and no products are displayed.</span></span>


<span data-ttu-id="8cde8-187">[![当](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="8cde8-187">[![When the](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image29.png)</span></span>

<span data-ttu-id="8cde8-188">**图 13**： 选择"-选择一个类别-"列表项目时，将显示否产品 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image31.png))</span><span class="sxs-lookup"><span data-stu-id="8cde8-188">**Figure 13**: When the "-- Choose a Category --" List Item is Selected, No Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image31.png))</span></span>


<span data-ttu-id="8cde8-189">如果您而是将显示*所有*产品选中"-选择一个类别-"选项后，使用值`-1`相反。</span><span class="sxs-lookup"><span data-stu-id="8cde8-189">If you'd rather display *all* of the products when the "-- Choose a Category --" option is selected, use a value of `-1` instead.</span></span> <span data-ttu-id="8cde8-190">敏锐读取器将能在该重新中回调*主/详细信息筛选与 DropDownList*教程我们更新了`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法，以便如果*`categoryID`*值`-1`在未返回记录的所有产品中传递。</span><span class="sxs-lookup"><span data-stu-id="8cde8-190">The astute reader will recall that back in the *Master/Detail Filtering With a DropDownList* tutorial we updated the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method so that if a *`categoryID`* value of `-1` was passed in, all product records were returned.</span></span>

## <a name="summary"></a><span data-ttu-id="8cde8-191">总结</span><span class="sxs-lookup"><span data-stu-id="8cde8-191">Summary</span></span>

<span data-ttu-id="8cde8-192">显示按层次结构相关的数据时，它通常有助于呈现使用主/详细信息报表，用户可以从中启动浏览的层次结构中按自上而下的数据以及向下钻取详细信息数据。</span><span class="sxs-lookup"><span data-stu-id="8cde8-192">When displaying hierarchically-related data, it often helps to present the data using master/detail reports, from which the user can start perusing the data from the top of the hierarchy and drill down into details.</span></span> <span data-ttu-id="8cde8-193">在本教程中，我们探讨生成一个简单的主/详细信息报告，显示所选的类别的产品。</span><span class="sxs-lookup"><span data-stu-id="8cde8-193">In this tutorial we examined building a simple master/detail report showing a selected category's products.</span></span> <span data-ttu-id="8cde8-194">这通过 DropDownList 用于类别列表，属于所选类别的产品 DataList 完成。</span><span class="sxs-lookup"><span data-stu-id="8cde8-194">This was accomplished by using a DropDownList for the list of categories and a DataList for the products belonging to the selected category.</span></span>

<span data-ttu-id="8cde8-195">在下一教程中我们将查看跨两个页分隔 master 和详细信息记录。</span><span class="sxs-lookup"><span data-stu-id="8cde8-195">In the next tutorial we'll look at separating the master and details records across two pages.</span></span> <span data-ttu-id="8cde8-196">在第一页中，"主"的记录的列表将显示，包含要查看的详细信息的链接。</span><span class="sxs-lookup"><span data-stu-id="8cde8-196">In the first page, a list of "master" records will be displayed, with a link to view the details.</span></span> <span data-ttu-id="8cde8-197">单击链接将 whisk 用户第二个页上，将显示为所选的主记录的详细信息。</span><span class="sxs-lookup"><span data-stu-id="8cde8-197">Clicking on the link will whisk the user to the second page, which will display the details for the selected master record.</span></span>

<span data-ttu-id="8cde8-198">尽情享受编程 ！</span><span class="sxs-lookup"><span data-stu-id="8cde8-198">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="8cde8-199">关于作者</span><span class="sxs-lookup"><span data-stu-id="8cde8-199">About the Author</span></span>

<span data-ttu-id="8cde8-200">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的七个 ASP/ASP.NET 书籍和的创始人[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年使用与 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="8cde8-200">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="8cde8-201">Scott 的作用是作为独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="8cde8-201">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="8cde8-202">最新书籍是[ *Sam 教授自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="8cde8-202">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="8cde8-203">他可以达到在[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)或通过他的博客，其中可以找到在[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="8cde8-203">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="8cde8-204">特别感谢...</span><span class="sxs-lookup"><span data-stu-id="8cde8-204">Special Thanks To…</span></span>

<span data-ttu-id="8cde8-205">本教程系列已由许多有用的审阅者评审。</span><span class="sxs-lookup"><span data-stu-id="8cde8-205">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="8cde8-206">本教程中的前导审阅者已徐 Schmidt。</span><span class="sxs-lookup"><span data-stu-id="8cde8-206">Lead reviewer for this tutorial was Randy Schmidt.</span></span> <span data-ttu-id="8cde8-207">对感兴趣查看我即将到来的 MSDN 文章？</span><span class="sxs-lookup"><span data-stu-id="8cde8-207">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="8cde8-208">如果是这样，删除我一行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="8cde8-208">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8cde8-209">下一篇</span><span class="sxs-lookup"><span data-stu-id="8cde8-209">Next</span></span>](master-detail-filtering-acess-two-pages-datalist-cs.md)
