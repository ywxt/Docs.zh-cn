---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
title: 使用 DropDownList (VB) 进行筛选母版/详细信息 |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将了解如何使用 Dropdownlist 以显示用于显示 'master' 记录和 DataList 单个网页中显示母版/详细信息报表...
ms.author: aspnetcontent
ms.date: 07/18/2007
ms.assetid: ad0f1014-1eff-465f-bdc6-93058de00e44
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: e88a7459529e003b73ef5a42456de3501e3db461
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829316"
---
<a name="masterdetail-filtering-with-a-dropdownlist-vb"></a><span data-ttu-id="87b62-103">使用 DropDownList (VB) 进行筛选母版/详细信息</span><span class="sxs-lookup"><span data-stu-id="87b62-103">Master/Detail Filtering With a DropDownList (VB)</span></span>
====================
<span data-ttu-id="87b62-104">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="87b62-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="87b62-105">[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_VB.exe)或[下载 PDF](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/datatutorial33vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="87b62-105">[Download Sample App](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_VB.exe) or [Download PDF](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/datatutorial33vb1.pdf)</span></span>

> <span data-ttu-id="87b62-106">在本教程中我们将了解如何使用 Dropdownlist 以显示"主"的记录和显示的"详细信息"DataList 单个网页中显示母版/详细信息报表。</span><span class="sxs-lookup"><span data-stu-id="87b62-106">In this tutorial we see how to display master/detail reports in a single web page using DropDownLists to display the "master" records and a DataList to display the "details".</span></span>


## <a name="introduction"></a><span data-ttu-id="87b62-107">介绍</span><span class="sxs-lookup"><span data-stu-id="87b62-107">Introduction</span></span>

<span data-ttu-id="87b62-108">首次创建在早期版本中使用 GridView 的母版/详细信息报告[母版/详细信息筛选与 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md)教程中，首先会显示某些组的"主"的记录。</span><span class="sxs-lookup"><span data-stu-id="87b62-108">The master/detail report, which we first created using a GridView in the earlier [Master/Detail Filtering With a DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) tutorial, begins by showing some set of "master" records.</span></span> <span data-ttu-id="87b62-109">用户可以然后向下钻取到一个主机记录，从而查看该主记录的"详细信息。"</span><span class="sxs-lookup"><span data-stu-id="87b62-109">The user can then drill down into one of the master records, thereby viewing that master record's "details."</span></span> <span data-ttu-id="87b62-110">母版/详细信息报表是一个对多关系可视化和显示 （是有大量的列） 特别"宽型"的表中的详细的信息的理想之选。</span><span class="sxs-lookup"><span data-stu-id="87b62-110">Master/detail reports are an ideal choice for visualizing one-to-many relationships and for displaying detailed information from particularly "wide" tables (ones that have a lot of columns).</span></span> <span data-ttu-id="87b62-111">我们已经探讨了如何实现在前面的教程中使用 GridView 和 DetailsView 控件的母版/详细信息报表。</span><span class="sxs-lookup"><span data-stu-id="87b62-111">We've explored how to implement master/detail reports using the GridView and DetailsView controls in previous tutorials.</span></span> <span data-ttu-id="87b62-112">在本教程和两个，我们将重新检查这些概念，但侧重于使用 DataList 和 Repeater 控件，而是。</span><span class="sxs-lookup"><span data-stu-id="87b62-112">In this tutorial and the next two, we'll reexamine these concepts, but focus on using DataList and Repeater controls instead.</span></span>

<span data-ttu-id="87b62-113">在本教程中，我们将介绍使用 DropDownList 包含的"主"的记录，DataList 中显示的"详细信息"记录。</span><span class="sxs-lookup"><span data-stu-id="87b62-113">In this tutorial, we'll look at using a DropDownList to contain the "master" records, with the "details" records displayed in a DataList.</span></span>

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a><span data-ttu-id="87b62-114">步骤 1： 添加母版/详细信息教程 Web 页</span><span class="sxs-lookup"><span data-stu-id="87b62-114">Step 1: Adding the Master/Detail Tutorial Web Pages</span></span>

<span data-ttu-id="87b62-115">在开始本教程之前，我们先来看一段时间来添加的文件夹和我们需要为本教程，并使用 DataList 和 Repeater 控件的母版/详细信息报表处理两个 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="87b62-115">Before we start this tutorial, let's first take a moment to add the folder and ASP.NET pages we'll need for this tutorial and the next two dealing with master/detail reports using the DataList and Repeater controls.</span></span> <span data-ttu-id="87b62-116">首先，创建一个新的文件夹在项目中名为`DataListRepeaterFiltering`。</span><span class="sxs-lookup"><span data-stu-id="87b62-116">Start by creating a new folder in the project named `DataListRepeaterFiltering`.</span></span> <span data-ttu-id="87b62-117">接下来，将以下五个 ASP.NET 页添加到此文件夹中，无需让他们配置为使用母版页`Site.master`:</span><span class="sxs-lookup"><span data-stu-id="87b62-117">Next, add the following five ASP.NET pages to this folder, having all of them configured to use the master page `Site.master`:</span></span>

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`


![创建 DataListRepeaterFiltering 文件夹并添加教程 ASP.NET 页面](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image1.png)

<span data-ttu-id="87b62-119">**图 1**： 创建`DataListRepeaterFiltering`文件夹并添加教程 ASP.NET 页面</span><span class="sxs-lookup"><span data-stu-id="87b62-119">**Figure 1**: Create a `DataListRepeaterFiltering` Folder and Add the Tutorial ASP.NET Pages</span></span>


<span data-ttu-id="87b62-120">接下来，打开`Default.aspx`页上，并将其拖`SectionLevelTutorialListing.ascx`从用户控制`UserControls`文件夹拖到设计图面。</span><span class="sxs-lookup"><span data-stu-id="87b62-120">Next, open the `Default.aspx` page and drag the `SectionLevelTutorialListing.ascx` User Control from the `UserControls` folder onto the Design surface.</span></span> <span data-ttu-id="87b62-121">此用户控件，我们在中创建[母版页和站点导航](../introduction/master-pages-and-site-navigation-vb.md)教程中，枚举站点图，并从项目符号列表中的当前部分显示这些教程。</span><span class="sxs-lookup"><span data-stu-id="87b62-121">This User Control, which we created in the [Master Pages and Site Navigation](../introduction/master-pages-and-site-navigation-vb.md) tutorial, enumerates the site map and displays the tutorials from the current section in a bulleted list.</span></span>


<span data-ttu-id="87b62-122">[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="87b62-122">[![Add the SectionLevelTutorialListing.ascx User Control to Default.aspx](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image2.png)</span></span>

<span data-ttu-id="87b62-123">**图 2**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="87b62-123">**Figure 2**: Add the `SectionLevelTutorialListing.ascx` User Control to `Default.aspx` ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image4.png))</span></span>


<span data-ttu-id="87b62-124">为了使项目符号列表显示母版/详细信息教程，我们将创建，我们需要将它们添加到站点地图。</span><span class="sxs-lookup"><span data-stu-id="87b62-124">In order to have the bulleted list display the master/detail tutorials we'll be creating, we need to add them to the site map.</span></span> <span data-ttu-id="87b62-125">打开`Web.sitemap`文件，并在"显示数据使用 DataList 和 Repeater"站点映射节点标记之后添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="87b62-125">Open the `Web.sitemap` file and add the following markup after the "Displaying Data with the DataList and Repeater" site map node markup:</span></span>

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample1.xml)]


![更新包括新的 ASP.NET 页面的站点图](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image5.png)

<span data-ttu-id="87b62-127">**图 3**： 更新包括新的 ASP.NET 页面的站点图</span><span class="sxs-lookup"><span data-stu-id="87b62-127">**Figure 3**: Update the Site Map to Include the New ASP.NET Pages</span></span>


## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a><span data-ttu-id="87b62-128">步骤 2： 在 DropDownList 中显示类别</span><span class="sxs-lookup"><span data-stu-id="87b62-128">Step 2: Displaying the Categories in a DropDownList</span></span>

<span data-ttu-id="87b62-129">我们的母版/详细信息报表将列出与所选的列表项的产品显示在下拉列表中，类别后面 DataList 中的页。</span><span class="sxs-lookup"><span data-stu-id="87b62-129">Our master/detail report will list the categories in a DropDownList, with the selected list item's products displayed further down in the page in a DataList.</span></span> <span data-ttu-id="87b62-130">然后，领先于我们的第一个任务是已在 DropDownList 中显示的类别。</span><span class="sxs-lookup"><span data-stu-id="87b62-130">The first task ahead of us, then, is to have the categories displayed in a DropDownList.</span></span> <span data-ttu-id="87b62-131">首先打开`FilterByDropDownList.aspx`页中`DataListRepeaterFiltering`文件夹，然后从工具箱拖动到页面的设计器将 DropDownList。</span><span class="sxs-lookup"><span data-stu-id="87b62-131">Start by opening the `FilterByDropDownList.aspx` page in the `DataListRepeaterFiltering` folder and drag a DropDownList from the Toolbox onto the page's designer.</span></span> <span data-ttu-id="87b62-132">接下来，设置 DropDownList`ID`属性设置为`Categories`。</span><span class="sxs-lookup"><span data-stu-id="87b62-132">Next, set the DropDownList's `ID` property to `Categories`.</span></span> <span data-ttu-id="87b62-133">单击选择数据源链接从 DropDownList 的智能标记并创建名为新 ObjectDataSource `CategoriesDataSource`。</span><span class="sxs-lookup"><span data-stu-id="87b62-133">Click on the Choose Data Source link from the DropDownList's smart tag and create a new ObjectDataSource named `CategoriesDataSource`.</span></span>


<span data-ttu-id="87b62-134">[![添加名为 CategoriesDataSource 新 ObjectDataSource](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="87b62-134">[![Add a New ObjectDataSource Named CategoriesDataSource](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image6.png)</span></span>

<span data-ttu-id="87b62-135">**图 4**： 添加新对象数据源名为`CategoriesDataSource`([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="87b62-135">**Figure 4**: Add a New ObjectDataSource Named `CategoriesDataSource` ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image8.png))</span></span>


<span data-ttu-id="87b62-136">配置新对象数据源，以便它将调用`CategoriesBLL`类的`GetCategories()`方法。</span><span class="sxs-lookup"><span data-stu-id="87b62-136">Configure the new ObjectDataSource such that it invokes the `CategoriesBLL` class's `GetCategories()` method.</span></span> <span data-ttu-id="87b62-137">配置的 ObjectDataSource 我们仍然需要指定应在 DropDownList 中显示哪些数据源字段和后一个应为每个列表项的值相关联。</span><span class="sxs-lookup"><span data-stu-id="87b62-137">After configuring the ObjectDataSource we still need to specify what data source field should be displayed in the DropDownList and which one should be associated as the value for each list item.</span></span> <span data-ttu-id="87b62-138">具有`CategoryName`字段与显示和`CategoryID`为每个列表项的值。</span><span class="sxs-lookup"><span data-stu-id="87b62-138">Have the `CategoryName` field as the display and `CategoryID` as the value for each list item.</span></span>


<span data-ttu-id="87b62-139">[![作为值的类别名称字段和使用 CategoryID 使 DropDownList 显示](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="87b62-139">[![Have the DropDownList Display the CategoryName Field and Use CategoryID as the Value](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image9.png)</span></span>

<span data-ttu-id="87b62-140">**图 5**： 使 DropDownList 显示`CategoryName`字段并使用`CategoryID`作为值 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image11.png))</span><span class="sxs-lookup"><span data-stu-id="87b62-140">**Figure 5**: Have the DropDownList Display the `CategoryName` Field and Use `CategoryID` as the Value ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image11.png))</span></span>


<span data-ttu-id="87b62-141">现在我们有从记录将填充 DropDownList 控件`Categories`表 （全部在大约六秒钟内完成）。</span><span class="sxs-lookup"><span data-stu-id="87b62-141">At this point we have a DropDownList control that's populated with the records from the `Categories` table (all accomplished in about six seconds).</span></span> <span data-ttu-id="87b62-142">图 6 显示了我们到目前为止的浏览器查看时。</span><span class="sxs-lookup"><span data-stu-id="87b62-142">Figure 6 shows our progress thus far when viewed through a browser.</span></span>


<span data-ttu-id="87b62-143">[![下拉列表列出了当前类别](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="87b62-143">[![A Drop-Down Lists the Current Categories](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image12.png)</span></span>

<span data-ttu-id="87b62-144">**图 6**: 下拉列表列出了当前类别 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="87b62-144">**Figure 6**: A Drop-Down Lists the Current Categories ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image14.png))</span></span>


## <a name="step-2-adding-the-products-datalist"></a><span data-ttu-id="87b62-145">步骤 2： 添加产品 DataList</span><span class="sxs-lookup"><span data-stu-id="87b62-145">Step 2: Adding the Products DataList</span></span>

<span data-ttu-id="87b62-146">我们的母版/详细信息报表的最后一步是列出与所选类别关联的产品。</span><span class="sxs-lookup"><span data-stu-id="87b62-146">The last step in our master/detail report is to list the products associated with the selected category.</span></span> <span data-ttu-id="87b62-147">若要实现此目的，向页面添加 DataList 并创建名为新 ObjectDataSource `ProductsByCategoryDataSource`。</span><span class="sxs-lookup"><span data-stu-id="87b62-147">To accomplish this, add a DataList to the page and create a new ObjectDataSource named `ProductsByCategoryDataSource`.</span></span> <span data-ttu-id="87b62-148">具有`ProductsByCategoryDataSource`控件检索其数据从`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。</span><span class="sxs-lookup"><span data-stu-id="87b62-148">Have the `ProductsByCategoryDataSource` control retrieve its data from the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method.</span></span> <span data-ttu-id="87b62-149">由于此母版/详细信息报表是只读的选择 (None) 选项中的 INSERT、 UPDATE 和 DELETE 的选项卡。</span><span class="sxs-lookup"><span data-stu-id="87b62-149">Since this master/detail report is read-only, choose the (None) option in the INSERT, UPDATE, and DELETE tabs.</span></span>


<span data-ttu-id="87b62-150">[![选择 GetProductsByCategoryID(categoryID) 方法](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="87b62-150">[![Select the GetProductsByCategoryID(categoryID) Method](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image15.png)</span></span>

<span data-ttu-id="87b62-151">**图 7**： 选择`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image17.png))</span><span class="sxs-lookup"><span data-stu-id="87b62-151">**Figure 7**: Select the `GetProductsByCategoryID(categoryID)` Method ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image17.png))</span></span>


<span data-ttu-id="87b62-152">单击下一步后, ObjectDataSource 向导提示我们输入的值的源`GetProductsByCategoryID(categoryID)`方法的*`categoryID`* 参数。</span><span class="sxs-lookup"><span data-stu-id="87b62-152">After clicking Next, the ObjectDataSource wizard prompts us for the source of the value for the `GetProductsByCategoryID(categoryID)` method's *`categoryID`* parameter.</span></span> <span data-ttu-id="87b62-153">若要使用的所选的值`categories`DropDownList 项设置参数源为控件和到 ControlID `Categories`。</span><span class="sxs-lookup"><span data-stu-id="87b62-153">To use the value of the selected `categories` DropDownList item set the Parameter source to Control and the ControlID to `Categories`.</span></span>


<span data-ttu-id="87b62-154">[![将类别 id 参数设置为 Categories DropDownList 的值](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="87b62-154">[![Set the categoryID Parameter to the Value of the Categories DropDownList](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image18.png)</span></span>

<span data-ttu-id="87b62-155">**图 8**： 设置*`categoryID`* 的值的参数`Categories`DropDownList ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="87b62-155">**Figure 8**: Set the *`categoryID`* Parameter to the Value of the `Categories` DropDownList ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image20.png))</span></span>


<span data-ttu-id="87b62-156">Visual Studio 将自动生成完成之后配置数据源向导，`ItemTemplate`的显示名称和值的每个数据字段的 DataList。</span><span class="sxs-lookup"><span data-stu-id="87b62-156">Upon completing the Configure Data Source wizard, Visual Studio will automatically generate an `ItemTemplate` for the DataList that displays the name and value of each data field.</span></span> <span data-ttu-id="87b62-157">让我们来改进要改为使用 DataList `ItemTemplate` ，它显示只需产品的名称、 类别、 供应商，每个单元和价格和数量`SeparatorTemplate`的注入`<hr>`每个项之间的元素。</span><span class="sxs-lookup"><span data-stu-id="87b62-157">Let's enhance the DataList to instead use an `ItemTemplate` that displays just the product's name, category, supplier, quantity per unit, and price along with a `SeparatorTemplate` that injects an `<hr>` element between each item.</span></span> <span data-ttu-id="87b62-158">我将使用`ItemTemplate`从示例，请参见[使用 DataList 和 Repeater 控件显示数据](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb.md)教程中，但可随时使用查找最引人注目的任何模板标记。</span><span class="sxs-lookup"><span data-stu-id="87b62-158">I'm going to use the `ItemTemplate` from an example in the [Displaying Data with the DataList and Repeater Controls](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb.md) tutorial, but feel free to use whatever template markup you find most visually appealing.</span></span>

<span data-ttu-id="87b62-159">进行这些更改后，你 DataList 和其 ObjectDataSource 的标记应类似于下面：</span><span class="sxs-lookup"><span data-stu-id="87b62-159">After making these changes, your DataList and its ObjectDataSource's markup should look similar to the following:</span></span>

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample2.aspx)]

<span data-ttu-id="87b62-160">请花费片刻时间来了解我们在浏览器中的进度。</span><span class="sxs-lookup"><span data-stu-id="87b62-160">Take a moment to check out our progress in a browser.</span></span> <span data-ttu-id="87b62-161">当首次访问的页面，属于所选的类别 （饮料） 这些产品会显示 （如图 9 中所示），但更改 DropDownList 不会更新数据。</span><span class="sxs-lookup"><span data-stu-id="87b62-161">When first visiting the page, those products belonging to the selected category (Beverages) are displayed (as shown in Figure 9), but changing the DropDownList doesn't update the data.</span></span> <span data-ttu-id="87b62-162">这是因为必须 DataList 更新在回发。</span><span class="sxs-lookup"><span data-stu-id="87b62-162">This is because a postback must occur for the DataList to update.</span></span> <span data-ttu-id="87b62-163">若要完成此我们可以设置 DropDownList`AutoPostBack`属性设置为`true`或向页面添加一个按钮 Web 控件。</span><span class="sxs-lookup"><span data-stu-id="87b62-163">To accomplish this we can either set the DropDownList's `AutoPostBack` property to `true` or add a Button Web control to the page.</span></span> <span data-ttu-id="87b62-164">对于本教程中，我选择要设置 DropDownList`AutoPostBack`属性设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="87b62-164">For this tutorial, I've opted to set the DropDownList's `AutoPostBack` property to `true`.</span></span>

<span data-ttu-id="87b62-165">图 9 和 10 说明了操作中的母版/详细信息报表。</span><span class="sxs-lookup"><span data-stu-id="87b62-165">Figures 9 and 10 illustrate the master/detail report in action.</span></span>


<span data-ttu-id="87b62-166">[![当首次访问的页面，显示饮料产品](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="87b62-166">[![When First Visiting the Page, the Beverage Products are Displayed](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image21.png)</span></span>

<span data-ttu-id="87b62-167">**图 9**： 当首次访问的页面，显示饮料产品 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image23.png))</span><span class="sxs-lookup"><span data-stu-id="87b62-167">**Figure 9**: When First Visiting the Page, the Beverage Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image23.png))</span></span>


<span data-ttu-id="87b62-168">[![选择一种新产品 （生成） 将自动导致回发，更新 DataList](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="87b62-168">[![Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the DataList](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image24.png)</span></span>

<span data-ttu-id="87b62-169">**图 10**： 选择一种新产品 （生成） 将自动导致回发，更新 DataList ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="87b62-169">**Figure 10**: Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the DataList ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image26.png))</span></span>


## <a name="adding-a----choose-a-category----list-item"></a><span data-ttu-id="87b62-170">添加"--选择一个类别-"列表项</span><span class="sxs-lookup"><span data-stu-id="87b62-170">Adding a "-- Choose a Category --" List Item</span></span>

<span data-ttu-id="87b62-171">首次访问时`FilterByDropDownList.aspx`页 DropDownList 的第一个列表项 （饮料） 选择默认情况下，显示 DataList 中的饮料产品的类别。</span><span class="sxs-lookup"><span data-stu-id="87b62-171">When first visiting the `FilterByDropDownList.aspx` page the categories DropDownList's first list item (Beverages) is selected by default, showing the beverage products in the DataList.</span></span> <span data-ttu-id="87b62-172">在中*母版/详细信息筛选与 DropDownList*教程中我们向 DropDownList，已选择默认情况下，选中后，显示添加"--选择一个类别-"选项*所有*的在数据库中的产品。</span><span class="sxs-lookup"><span data-stu-id="87b62-172">In the *Master/Detail Filtering With a DropDownList* tutorial we added a "-- Choose a Category --" option to the DropDownList that was selected by default and, when selected, displayed *all* of the products in the database.</span></span> <span data-ttu-id="87b62-173">这种方法是可管理时列出的产品在 GridView 中后，因为每个产品行占据了少量的屏幕空间。</span><span class="sxs-lookup"><span data-stu-id="87b62-173">Such an approach was manageable when listing the products in a GridView, as each product row took up a small amount of screen real estate.</span></span> <span data-ttu-id="87b62-174">使用 DataList，但是，每个产品的信息使用较大块的屏幕。</span><span class="sxs-lookup"><span data-stu-id="87b62-174">With the DataList, however, each product's information consumes a much larger chunk of the screen.</span></span> <span data-ttu-id="87b62-175">我们仍将添加"--选择一个类别-"选项和让它默认情况下，选择但而不是让它显示的所有产品时选择，让我们将其配置，使之显示任何产品。</span><span class="sxs-lookup"><span data-stu-id="87b62-175">Let's still add a "-- Choose a Category --" option and have it selected by default, but instead of having it show all products when selected, let's configure it so that it shows no products.</span></span>

<span data-ttu-id="87b62-176">若要向 DropDownList 添加新列表项，请转到属性窗口，然后单击中的椭圆`Items`属性。</span><span class="sxs-lookup"><span data-stu-id="87b62-176">To add a new list item to the DropDownList, go to the Properties window and click on the ellipses in the `Items` property.</span></span> <span data-ttu-id="87b62-177">添加的新列表项`Text`"--选择一个类别-"和`Value` `0`。</span><span class="sxs-lookup"><span data-stu-id="87b62-177">Add a new list item with the `Text` "-- Choose a Category --" and the `Value` `0`.</span></span>


![添加](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image27.png)

<span data-ttu-id="87b62-179">**图 11**： 添加"--选择一个类别-"列表项</span><span class="sxs-lookup"><span data-stu-id="87b62-179">**Figure 11**: Add a "-- Choose a Category --" List Item</span></span>


<span data-ttu-id="87b62-180">或者，可以通过将以下标记添加到下拉列表添加列表项：</span><span class="sxs-lookup"><span data-stu-id="87b62-180">Alternatively, you can add the list item by adding the following markup to the DropDownList:</span></span>

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample3.aspx)]

<span data-ttu-id="87b62-181">此外，我们需要设置 DropDownList 控件`AppendDataBoundItems`到`true`由于如果设置为`false`（默认值），将类别从 ObjectDataSource 绑定到 DropDownList 时这些更改会覆盖任何手动添加列表项。</span><span class="sxs-lookup"><span data-stu-id="87b62-181">Additionally, we need to set the DropDownList control's `AppendDataBoundItems` to `true` because if it's set to `false` (the default), when the categories are bound to the DropDownList from the ObjectDataSource they'll overwrite any manually-added list items.</span></span>


![AppendDataBoundItems 属性设置为 True](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image28.png)

<span data-ttu-id="87b62-183">**图 12**： 设置`AppendDataBoundItems`属性设为 True</span><span class="sxs-lookup"><span data-stu-id="87b62-183">**Figure 12**: Set the `AppendDataBoundItems` Property to True</span></span>


<span data-ttu-id="87b62-184">因此我们选择了值`0`对于"--选择一个类别-"列表项都是因为值为系统中不有任何类别`0`，因此任何产品记录时，将返回选定了"--选择一个类别-"的列表项。</span><span class="sxs-lookup"><span data-stu-id="87b62-184">The reason we chose the value `0` for the "-- Choose a Category --" list item is because there are no categories in the system with a value of `0`, hence no product records will be returned when the "-- Choose a Category --" list item is selected.</span></span> <span data-ttu-id="87b62-185">若要确认这一点，请花费片刻时间访问通过浏览器页面。</span><span class="sxs-lookup"><span data-stu-id="87b62-185">To confirm this, take a moment to visit the page through a browser.</span></span> <span data-ttu-id="87b62-186">如图 13 所示，当最初查看页上选定了"--选择一个类别-"的列表项并不显示任何产品。</span><span class="sxs-lookup"><span data-stu-id="87b62-186">As Figure 13 shows, when initially viewing the page the "-- Choose a Category --" list item is selected and no products are displayed.</span></span>


<span data-ttu-id="87b62-187">[![时](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="87b62-187">[![When the](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image29.png)</span></span>

<span data-ttu-id="87b62-188">**图 13**： 否产品时选择"--选择一个类别-"列表项时，会显示 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image31.png))</span><span class="sxs-lookup"><span data-stu-id="87b62-188">**Figure 13**: When the "-- Choose a Category --" List Item is Selected, No Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image31.png))</span></span>


<span data-ttu-id="87b62-189">如果您而是会显示*所有*的产品时选择"--选择一个类别-"选项，则使用值为`-1`相反。</span><span class="sxs-lookup"><span data-stu-id="87b62-189">If you'd rather display *all* of the products when the "-- Choose a Category --" option is selected, use a value of `-1` instead.</span></span> <span data-ttu-id="87b62-190">敏锐的读者都记得中的该重新*母版/详细信息筛选与 DropDownList*教程中，我们更新`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法，以便如果*`categoryID`* 值`-1`返回记录的所有产品中传递。</span><span class="sxs-lookup"><span data-stu-id="87b62-190">The astute reader will recall that back in the *Master/Detail Filtering With a DropDownList* tutorial we updated the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method so that if a *`categoryID`* value of `-1` was passed in, all product records were returned.</span></span>

## <a name="summary"></a><span data-ttu-id="87b62-191">总结</span><span class="sxs-lookup"><span data-stu-id="87b62-191">Summary</span></span>

<span data-ttu-id="87b62-192">显示按层次结构相关数据时，它通常用于呈现使用主/详细信息报表，用户可以从中启动仔细阅读的层次结构顶部的数据和向下钻取到详细信息数据。</span><span class="sxs-lookup"><span data-stu-id="87b62-192">When displaying hierarchically-related data, it often helps to present the data using master/detail reports, from which the user can start perusing the data from the top of the hierarchy and drill down into details.</span></span> <span data-ttu-id="87b62-193">在本教程中，我们探讨构建一个简单的母版/详细信息报告，显示所选的类别的产品。</span><span class="sxs-lookup"><span data-stu-id="87b62-193">In this tutorial we examined building a simple master/detail report showing a selected category's products.</span></span> <span data-ttu-id="87b62-194">这被通过使用 DropDownList 的类别和 DataList 属于所选类别的产品列表。</span><span class="sxs-lookup"><span data-stu-id="87b62-194">This was accomplished by using a DropDownList for the list of categories and a DataList for the products belonging to the selected category.</span></span>

<span data-ttu-id="87b62-195">在下一教程中我们将介绍分隔跨两个页面的母版和详细信息记录。</span><span class="sxs-lookup"><span data-stu-id="87b62-195">In the next tutorial we'll look at separating the master and details records across two pages.</span></span> <span data-ttu-id="87b62-196">在第一页中，"主"记录的列表将显示，包含用于查看详细信息的链接。</span><span class="sxs-lookup"><span data-stu-id="87b62-196">In the first page, a list of "master" records will be displayed, with a link to view the details.</span></span> <span data-ttu-id="87b62-197">单击链接将 whisk 到第二页上，将显示为所选的主记录的详细信息的用户。</span><span class="sxs-lookup"><span data-stu-id="87b62-197">Clicking on the link will whisk the user to the second page, which will display the details for the selected master record.</span></span>

<span data-ttu-id="87b62-198">快乐编程 ！</span><span class="sxs-lookup"><span data-stu-id="87b62-198">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="87b62-199">关于作者</span><span class="sxs-lookup"><span data-stu-id="87b62-199">About the Author</span></span>

<span data-ttu-id="87b62-200">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="87b62-200">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="87b62-201">Scott 是独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="87b62-201">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="87b62-202">他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="87b62-202">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="87b62-203">他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="87b62-203">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="87b62-204">或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="87b62-204">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="87b62-205">特别感谢...</span><span class="sxs-lookup"><span data-stu-id="87b62-205">Special Thanks To…</span></span>

<span data-ttu-id="87b62-206">很多有用的审阅者已评审本系列教程。</span><span class="sxs-lookup"><span data-stu-id="87b62-206">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="87b62-207">本教程中的潜在顾客审阅者已 Randy Schmidt。</span><span class="sxs-lookup"><span data-stu-id="87b62-207">Lead reviewer for this tutorial was Randy Schmidt.</span></span> <span data-ttu-id="87b62-208">是否有兴趣查看我即将推出的 MSDN 文章？</span><span class="sxs-lookup"><span data-stu-id="87b62-208">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="87b62-209">如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="87b62-209">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="87b62-210">[上一页](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
> [下一页](master-detail-filtering-acess-two-pages-datalist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="87b62-210">[Previous](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
[Next](master-detail-filtering-acess-two-pages-datalist-vb.md)</span></span>
