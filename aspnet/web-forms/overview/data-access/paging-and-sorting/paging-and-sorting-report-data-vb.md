---
uid: web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-vb
title: 分页和排序报表数据 (VB) |Microsoft Docs
author: rick-anderson
description: 分页和排序是两个非常常见的功能，在一个在线应用程序中显示数据时。 在本教程中我们将首先看一下添加排序和...
ms.author: aspnetcontent
ms.date: 08/15/2006
ms.assetid: b895e37e-0e69-45cc-a7e4-17ddd2e1b38d
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-vb
msc.type: authoredcontent
ms.openlocfilehash: e8e33bc11074815b5beacd92c49c95f8ea9da2c0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37808455"
---
<a name="paging-and-sorting-report-data-vb"></a><span data-ttu-id="7b1e6-104">分页和排序报表数据 (VB)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-104">Paging and Sorting Report Data (VB)</span></span>
====================
<span data-ttu-id="7b1e6-105">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="7b1e6-106">[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_VB.exe)或[下载 PDF](paging-and-sorting-report-data-vb/_static/datatutorial24vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-106">[Download Sample App](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_VB.exe) or [Download PDF](paging-and-sorting-report-data-vb/_static/datatutorial24vb1.pdf)</span></span>

> <span data-ttu-id="7b1e6-107">分页和排序是两个非常常见的功能，在一个在线应用程序中显示数据时。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-107">Paging and sorting are two very common features when displaying data in an online application.</span></span> <span data-ttu-id="7b1e6-108">在本教程中，我们将首先看一下添加排序和分页至我们的报表，然后，我们将生成后在将来的教程。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-108">In this tutorial we'll take a first look at adding sorting and paging to our reports, which we will then build upon in future tutorials.</span></span>


## <a name="introduction"></a><span data-ttu-id="7b1e6-109">介绍</span><span class="sxs-lookup"><span data-stu-id="7b1e6-109">Introduction</span></span>

<span data-ttu-id="7b1e6-110">分页和排序是两个非常常见的功能，在一个在线应用程序中显示数据时。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-110">Paging and sorting are two very common features when displaying data in an online application.</span></span> <span data-ttu-id="7b1e6-111">例如，搜索的一家网上书店在 ASP.NET 书籍时，可能有数百个此类书籍，但搜索结果中列出该报表列出每页的十个匹配项。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-111">For example, when searching for ASP.NET books at an online bookstore, there may be hundreds of such books, but the report listing the search results lists only ten matches per page.</span></span> <span data-ttu-id="7b1e6-112">此外，可以按标题、 价格、 页数、 作者姓名等对结果进行排序。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-112">Moreover, the results can be sorted by title, price, page count, author name, and so on.</span></span> <span data-ttu-id="7b1e6-113">而的过去 23 教程已介绍了如何生成各种报告，包括接口，它允许添加、 编辑和删除数据，我们不了解了如何对数据和唯一进行排序的已分页示例我们 ve 看到已与 DetailsView 和 FormView控件。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-113">While the past 23 tutorials have examined how to build a variety of reports, including interfaces that permit adding, editing, and deleting data, we ve not looked at how to sort data and the only paging examples we ve seen have been with the DetailsView and FormView controls.</span></span>

<span data-ttu-id="7b1e6-114">在本教程中我们将了解如何添加排序和分页至我们的报表，这可以通过只需检查几个复选框来完成。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-114">In this tutorial we'll see how to add sorting and paging to our reports, which can be accomplished by simply checking a few checkboxes.</span></span> <span data-ttu-id="7b1e6-115">遗憾的是，这个简单的实施有排序接口会使一些需要其缺点和分页例程并不设计用于高效地进行分页的大结果集。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-115">Unfortunately, this simplistic implementation has its drawbacks the sorting interface leaves a bit to be desired and the paging routines are not designed for efficiently paging through large result sets.</span></span> <span data-ttu-id="7b1e6-116">将来的教程将探讨如何克服这些限制--现成的分页和排序的解决方案。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-116">Future tutorials will explore how to overcome the limitations of the out-of-the-box paging and sorting solutions.</span></span>

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a><span data-ttu-id="7b1e6-117">步骤 1： 添加分页和排序教程网页</span><span class="sxs-lookup"><span data-stu-id="7b1e6-117">Step 1: Adding the Paging and Sorting Tutorial Web Pages</span></span>

<span data-ttu-id="7b1e6-118">在开始本教程之前，让我们来首先请花费片刻时间以添加我们需要为本教程和下一步的三个 ASP.NET 页面。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-118">Before we start this tutorial, let s first take a moment to add the ASP.NET pages we'll need for this tutorial and the next three.</span></span> <span data-ttu-id="7b1e6-119">首先，创建一个新的文件夹在项目中名为`PagingAndSorting`。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-119">Start by creating a new folder in the project named `PagingAndSorting`.</span></span> <span data-ttu-id="7b1e6-120">接下来，将以下五个 ASP.NET 页添加到此文件夹中，无需让他们配置为使用母版页`Site.master`:</span><span class="sxs-lookup"><span data-stu-id="7b1e6-120">Next, add the following five ASP.NET pages to this folder, having all of them configured to use the master page `Site.master`:</span></span>

- `Default.aspx`
- `SimplePagingSorting.aspx`
- `EfficientPaging.aspx`
- `SortParameter.aspx`
- `CustomSortingUI.aspx`


![创建 PagingAndSorting 文件夹并添加教程 ASP.NET 页面](paging-and-sorting-report-data-vb/_static/image1.png)

<span data-ttu-id="7b1e6-122">**图 1**： 创建 PagingAndSorting 文件夹并添加教程 ASP.NET 页面</span><span class="sxs-lookup"><span data-stu-id="7b1e6-122">**Figure 1**: Create a PagingAndSorting Folder and Add the Tutorial ASP.NET Pages</span></span>


<span data-ttu-id="7b1e6-123">接下来，打开`Default.aspx`页上，并将其拖`SectionLevelTutorialListing.ascx`从用户控制`UserControls`文件夹拖到设计图面。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-123">Next, open the `Default.aspx` page and drag the `SectionLevelTutorialListing.ascx` User Control from the `UserControls` folder onto the Design surface.</span></span> <span data-ttu-id="7b1e6-124">此用户控件，我们在中创建[母版页和站点导航](../introduction/master-pages-and-site-navigation-vb.md)教程中，枚举站点图，并在项目符号列表中的当前部分中显示这些教程。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-124">This User Control, which we created in the [Master Pages and Site Navigation](../introduction/master-pages-and-site-navigation-vb.md) tutorial, enumerates the site map and displays those tutorials in the current section in a bulleted list.</span></span>


![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](paging-and-sorting-report-data-vb/_static/image2.png)

<span data-ttu-id="7b1e6-126">**图 2**: SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx</span><span class="sxs-lookup"><span data-stu-id="7b1e6-126">**Figure 2**: Add the SectionLevelTutorialListing.ascx User Control to Default.aspx</span></span>


<span data-ttu-id="7b1e6-127">为了使显示分页和排序的教程中我们将创建的项目符号列表，我们需要将它们添加到的站点映射。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-127">In order to have the bulleted list display the paging and sorting tutorials we'll be creating, we need to add them to the site map.</span></span> <span data-ttu-id="7b1e6-128">打开`Web.sitemap`文件，并编辑、 插入、 和删除站点映射节点标记后添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-128">Open the `Web.sitemap` file and add the following markup after the Editing, Inserting, and Deleting site map node markup:</span></span>


[!code-xml[Main](paging-and-sorting-report-data-vb/samples/sample1.xml)]


![更新包括新的 ASP.NET 页面的站点图](paging-and-sorting-report-data-vb/_static/image3.png)

<span data-ttu-id="7b1e6-130">**图 3**： 更新包括新的 ASP.NET 页面的站点图</span><span class="sxs-lookup"><span data-stu-id="7b1e6-130">**Figure 3**: Update the Site Map to Include the New ASP.NET Pages</span></span>


## <a name="step-2-displaying-product-information-in-a-gridview"></a><span data-ttu-id="7b1e6-131">步骤 2： 在 GridView 中显示的产品信息</span><span class="sxs-lookup"><span data-stu-id="7b1e6-131">Step 2: Displaying Product Information in a GridView</span></span>

<span data-ttu-id="7b1e6-132">我们实际上实现分页和排序功能之前，让我们来首先创建标准非-srotable，列出了产品信息的非可分页 GridView。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-132">Before we actually implement paging and sorting capabilities, let s first create a standard non-srotable, non-pageable GridView that lists the product information.</span></span> <span data-ttu-id="7b1e6-133">这是一项任务我们已多次在此之前完成本教程系列因此以下步骤应该比较熟悉。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-133">This is a task we ve done many times before throughout this tutorial series so these steps should be familiar.</span></span> <span data-ttu-id="7b1e6-134">首先打开`SimplePagingSorting.aspx`页上，并将 GridView 控件从工具箱拖到设计器中，设置其`ID`属性设置为`Products`。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-134">Start by opening the `SimplePagingSorting.aspx` page and drag a GridView control from the Toolbox onto the Designer, setting its `ID` property to `Products`.</span></span> <span data-ttu-id="7b1e6-135">接下来，创建新对象数据源使用 ProductsBLL 类的`GetProducts()`方法以返回所有产品信息。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-135">Next, create a new ObjectDataSource that uses the ProductsBLL class s `GetProducts()` method to return all of the product information.</span></span>


![检索有关所有使用 GetProducts() 方法的产品信息](paging-and-sorting-report-data-vb/_static/image4.png)

<span data-ttu-id="7b1e6-137">**图 4**： 检索有关所有使用 GetProducts() 方法的产品信息</span><span class="sxs-lookup"><span data-stu-id="7b1e6-137">**Figure 4**: Retrieve Information About All of the Products Using the GetProducts() Method</span></span>


<span data-ttu-id="7b1e6-138">由于此报表不是只读的报告，在该处 s 需要映射的 ObjectDataSource s `Insert()`， `Update()`，或`Delete()`方法添加到相应`ProductsBLL`方法; 因此，（无） 从列表中选择下拉列表的 INSERT、 UPDATE和删除选项卡。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-138">Since this report is a read-only report, there s no need to map the ObjectDataSource s `Insert()`, `Update()`, or `Delete()` methods to corresponding `ProductsBLL` methods; therefore, choose (None) from the drop-down list for the UPDATE, INSERT, and DELETE tabs.</span></span>


![选择 （无） 选项的下拉列表中插入、 更新和删除选项卡](paging-and-sorting-report-data-vb/_static/image5.png)

<span data-ttu-id="7b1e6-140">**图 5**： 选择 （无） 选项的下拉列表中插入、 更新和删除选项卡</span><span class="sxs-lookup"><span data-stu-id="7b1e6-140">**Figure 5**: Choose the (None) Option in the Drop-Down List in the UPDATE, INSERT, and DELETE Tabs</span></span>


<span data-ttu-id="7b1e6-141">接下来，让 s 自定义 GridView 的字段，以便显示仅产品名称、 供应商、 类别、 价格和已停止使用的状态。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-141">Next, let s customize the GridView s fields so that only the products names, suppliers, categories, prices, and discontinued statuses are displayed.</span></span> <span data-ttu-id="7b1e6-142">此外，随意进行任何字段级格式设置发生更改，例如调整`HeaderText`属性或格式设置为货币的价格。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-142">Furthermore, feel free to make any field-level formatting changes, such as adjusting the `HeaderText` properties or formatting the price as a currency.</span></span> <span data-ttu-id="7b1e6-143">以后这些更改，您的 GridView s 声明性标记看起来应类似于下面：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-143">After these changes, your GridView s declarative markup should look similar to the following:</span></span>


[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample2.aspx)]

<span data-ttu-id="7b1e6-144">图 6 显示了我们到目前为止的浏览器查看时。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-144">Figure 6 shows our progress thus far when viewed through a browser.</span></span> <span data-ttu-id="7b1e6-145">请注意页面列出所有在一个屏幕中，显示每个产品的名称、 类别、 供应商、 价格、 产品和停用状态。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-145">Note that the page lists all of the products in one screen, showing each product s name, category, supplier, price, and discontinued status.</span></span>


<span data-ttu-id="7b1e6-146">[![列出了每个产品](paging-and-sorting-report-data-vb/_static/image7.png)](paging-and-sorting-report-data-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-146">[![Each of the Products are Listed](paging-and-sorting-report-data-vb/_static/image7.png)](paging-and-sorting-report-data-vb/_static/image6.png)</span></span>

<span data-ttu-id="7b1e6-147">**图 6**： 列出了每个产品 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="7b1e6-147">**Figure 6**: Each of the Products are Listed ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image8.png))</span></span>


## <a name="step-3-adding-paging-support"></a><span data-ttu-id="7b1e6-148">步骤 3： 添加分页支持</span><span class="sxs-lookup"><span data-stu-id="7b1e6-148">Step 3: Adding Paging Support</span></span>

<span data-ttu-id="7b1e6-149">列出*所有*的一个屏幕上的产品可能会导致用户仔细阅读数据的信息过载。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-149">Listing *all* of the products on one screen can lead to information overload for the user perusing the data.</span></span> <span data-ttu-id="7b1e6-150">若要帮助使结果更易于管理，我们可以分解成较小的数据页的数据，并允许用户一次遍历一页数据。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-150">To help make the results more manageable, we can break up the data into smaller pages of data and allow the user to step through the data one page at a time.</span></span> <span data-ttu-id="7b1e6-151">若要完成这只需检查从 GridView s 智能标记启用分页复选框 (这将设置 GridView s [ `AllowPaging`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx)到`true`)。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-151">To accomplish this simply check the Enable Paging checkbox from the GridView s smart tag (this sets the GridView s [`AllowPaging` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx) to `true`).</span></span>


<span data-ttu-id="7b1e6-152">[![检查启用分页复选框来添加分页支持](paging-and-sorting-report-data-vb/_static/image10.png)](paging-and-sorting-report-data-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-152">[![Check the Enable Paging Checkbox to Add Paging Support](paging-and-sorting-report-data-vb/_static/image10.png)](paging-and-sorting-report-data-vb/_static/image9.png)</span></span>

<span data-ttu-id="7b1e6-153">**图 7**： 选中启用分页复选框以添加分页支持 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image11.png))</span><span class="sxs-lookup"><span data-stu-id="7b1e6-153">**Figure 7**: Check the Enable Paging Checkbox to Add Paging Support ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image11.png))</span></span>


<span data-ttu-id="7b1e6-154">启用分页限制每个页面所显示的记录数和添加*分页界面*到 GridView。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-154">Enabling paging limits the number of records shown per page and adds a *paging interface* to the GridView.</span></span> <span data-ttu-id="7b1e6-155">图 7 中所示的默认分页界面是页码，这样就允许用户从一页数据快速导航到另一系列。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-155">The default paging interface, shown in Figure 7, is a series of page numbers, allowing the user to quickly navigate from one page of data to another.</span></span> <span data-ttu-id="7b1e6-156">此分页接口应该很熟悉，因为我们已在过去的教程中将分页支持添加到 DetailsView 和 FormView 控件时看到它。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-156">This paging interface should look familiar, as we ve seen it when adding paging support to the DetailsView and FormView controls in past tutorials.</span></span>

<span data-ttu-id="7b1e6-157">在 DetailsView 和 FormView 控件仅显示每页的单个记录。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-157">Both the DetailsView and FormView controls only show a single record per page.</span></span> <span data-ttu-id="7b1e6-158">GridView 中，但是，会查询其[`PageSize`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx)以确定每页显示的记录数 （此属性默认为值为 10）。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-158">The GridView, however, consults its [`PageSize` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx) to determine how many records to show per page (this property defaults to a value of 10).</span></span>

<span data-ttu-id="7b1e6-159">可以使用以下属性自定义此 GridView、 DetailsView 和 FormView 的分页接口：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-159">This GridView, DetailsView, and FormView s paging interface can be customized using the following properties:</span></span>

- <span data-ttu-id="7b1e6-160">`PagerStyle` 指示分页界面的样式信息可以指定设置，例如`BackColor`， `ForeColor`， `CssClass`， `HorizontalAlign`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-160">`PagerStyle` indicates the style information for the paging interface; can specify settings like `BackColor`, `ForeColor`, `CssClass`, `HorizontalAlign`, and so on.</span></span>
- <span data-ttu-id="7b1e6-161">`PagerSettings` 包含一系列的属性，可以自定义分页界面中; 的功能`PageButtonCount`指示数字页号 （默认值为 10） 在分页界面中显示的最大数目; [ `Mode`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx)指示分页界面如何进行操作并可以将设置为：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-161">`PagerSettings` contains a bevy of properties that can customize the functionality of the paging interface; `PageButtonCount` indicates the maximum number of numeric page numbers displayed in the paging interface (the default is 10); the [`Mode` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx) indicates how the paging interface operates and can be set to:</span></span> 

    - <span data-ttu-id="7b1e6-162">`NextPrevious` 显示允许用户若要逐步向前或向后一页一次下一步和上一步按钮</span><span class="sxs-lookup"><span data-stu-id="7b1e6-162">`NextPrevious` shows a Next and Previous buttons, allowing the user to step forwards or backwards one page at a time</span></span>
    - <span data-ttu-id="7b1e6-163">`NextPreviousFirstLast` 除了下一步和上一步按钮，第一个和最后一个按钮，还提供了，这样就允许用户快速移动到第一个或最后一个数据页</span><span class="sxs-lookup"><span data-stu-id="7b1e6-163">`NextPreviousFirstLast` in addition to Next and Previous buttons, First and Last buttons are also included, allowing the user to quickly move to the first or last page of data</span></span>
    - <span data-ttu-id="7b1e6-164">`Numeric` 显示页码，这样就允许用户立即跳转到任何页面的系列</span><span class="sxs-lookup"><span data-stu-id="7b1e6-164">`Numeric` shows a series of page numbers, allowing the user to immediately jump to any page</span></span>
    - <span data-ttu-id="7b1e6-165">`NumericFirstLast` 除了页码，包括第一个和最后一个按钮，允许用户以快速移动到的数据; 第一个或最后一页第一个/最后一个按钮才会显示是否所有的数字页号不适合</span><span class="sxs-lookup"><span data-stu-id="7b1e6-165">`NumericFirstLast` in addition to the page numbers, includes First and Last buttons, allowing the user to quickly move to the first or last page of data; the First/Last buttons are only shown if all of the numeric page numbers cannot fit</span></span>

<span data-ttu-id="7b1e6-166">此外，GridView、 DetailsView 和所有产品/服务的 FormView`PageIndex`和`PageCount`属性，分别指示当前正在查看的页和数据的总页数。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-166">Moreover, the GridView, DetailsView, and FormView all offer the `PageIndex` and `PageCount` properties, which indicate the current page being viewed and the total number of pages of data, respectively.</span></span> <span data-ttu-id="7b1e6-167">`PageIndex`属性编制了索引 0，这意味着，查看数据的第一页时开始`PageIndex`将等于 0。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-167">The `PageIndex` property is indexed starting at 0, meaning that when viewing the first page of data `PageIndex` will equal 0.</span></span> <span data-ttu-id="7b1e6-168">`PageCount`计数 1，这意味着，但是，启动`PageIndex`仅限于值介于 0 和`PageCount - 1`。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-168">`PageCount`, on the other hand, starts counting at 1, meaning that `PageIndex` is limited to the values between 0 and `PageCount - 1`.</span></span>

<span data-ttu-id="7b1e6-169">允许 s 请花费片刻时间来提高我们 GridView 的分页接口的默认外观。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-169">Let s take a moment to improve the default appearance of our GridView s paging interface.</span></span> <span data-ttu-id="7b1e6-170">具体而言，让 s 具有浅灰色背景与右对齐的分页界面。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-170">Specifically, let s have the paging interface right-aligned with a light gray background.</span></span> <span data-ttu-id="7b1e6-171">而不是设置这些属性直接通过 GridView s`PagerStyle`属性，让 s 创建中的 CSS 类`Styles.css`名为`PagerRowStyle`，然后将分配`PagerStyle`s`CssClass`通过我们的主题的属性。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-171">Rather than setting these properties directly through the GridView s `PagerStyle` property, let s create a CSS class in `Styles.css` named `PagerRowStyle` and then assign the `PagerStyle` s `CssClass` property through our Theme.</span></span> <span data-ttu-id="7b1e6-172">首先打开`Styles.css`并添加以下 CSS 类定义：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-172">Start by opening `Styles.css` and adding the following CSS class definition:</span></span>


[!code-css[Main](paging-and-sorting-report-data-vb/samples/sample3.css)]

<span data-ttu-id="7b1e6-173">接下来，打开`GridView.skin`文件中`DataWebControls`文件夹内的`App_Themes`文件夹。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-173">Next, open the `GridView.skin` file in the `DataWebControls` folder within the `App_Themes` folder.</span></span> <span data-ttu-id="7b1e6-174">如中所述*母版页和站点导航*教程，外观文件可用于指定 Web 控件的默认属性值。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-174">As we discussed in the *Master Pages and Site Navigation* tutorial, Skin files can be used to specify the default property values for a Web control.</span></span> <span data-ttu-id="7b1e6-175">因此，增加现有设置，以包含设置`PagerStyle`s`CssClass`属性设置为`PagerRowStyle`。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-175">Therefore, augment the existing settings to include setting the `PagerStyle` s `CssClass` property to `PagerRowStyle`.</span></span> <span data-ttu-id="7b1e6-176">此外，let s 配置要显示最多五个数字页按钮使用的分页界面`NumericFirstLast`分页界面。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-176">Also, let s configure the paging interface to show at most five numeric page buttons using the `NumericFirstLast` paging interface.</span></span>


[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample4.aspx)]

## <a name="the-paging-user-experience"></a><span data-ttu-id="7b1e6-177">分页的用户体验</span><span class="sxs-lookup"><span data-stu-id="7b1e6-177">The Paging User Experience</span></span>

<span data-ttu-id="7b1e6-178">图 8 显示了 web 页上选中的 GridView s 启用分页复选框后，通过浏览器访问时，`PagerStyle`并`PagerSettings`通过进行了配置`GridView.skin`文件。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-178">Figure 8 shows the web page when visited through a browser after the GridView s Enable Paging checkbox has been checked and the `PagerStyle` and `PagerSettings` configurations have been made through the `GridView.skin` file.</span></span> <span data-ttu-id="7b1e6-179">请注意如何唯一十个记录将显示，并且分页界面指示我们正在查看数据的第一页。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-179">Note how only ten records are shown, and the paging interface indicates that we are viewing the first page of data.</span></span>


<span data-ttu-id="7b1e6-180">[![使用启用了分页，每次显示仅记录的子集](paging-and-sorting-report-data-vb/_static/image13.png)](paging-and-sorting-report-data-vb/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-180">[![With Paging Enabled, Only a Subset of the Records are Displayed at a Time](paging-and-sorting-report-data-vb/_static/image13.png)](paging-and-sorting-report-data-vb/_static/image12.png)</span></span>

<span data-ttu-id="7b1e6-181">**图 8**： 一次使用已启用分页，显示记录的一个子集 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="7b1e6-181">**Figure 8**: With Paging Enabled, Only a Subset of the Records are Displayed at a Time ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image14.png))</span></span>


<span data-ttu-id="7b1e6-182">当用户单击其中一个分页界面中的页码时，回发时，才会和页面重新加载请求的页面 + s 记录显示。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-182">When the user clicks on one of the page numbers in the paging interface, a postback ensues and the page reloads showing that requested page s records.</span></span> <span data-ttu-id="7b1e6-183">图 9 显示的结果，如果选择查看数据的最后一页。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-183">Figure 9 shows the results after opting to view the final page of data.</span></span> <span data-ttu-id="7b1e6-184">请注意，最后一页仅包含一条记录;这是因为总数，从而导致与单独记录每个页面以及一页的 10 条记录的 8 个页面中有 81 记录。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-184">Notice that the final page only has one record; this is because there are 81 records in total, resulting in eight pages of 10 records per page plus one page with a lone record.</span></span>


<span data-ttu-id="7b1e6-185">[![单击页码导致回发，并显示相应记录的子集](paging-and-sorting-report-data-vb/_static/image16.png)](paging-and-sorting-report-data-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-185">[![Clicking On a Page Number Causes a Postback and Shows the Appropriate Subset of Records](paging-and-sorting-report-data-vb/_static/image16.png)](paging-and-sorting-report-data-vb/_static/image15.png)</span></span>

<span data-ttu-id="7b1e6-186">**图 9**： 单击页码导致回发并显示相应记录子集 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image17.png))</span><span class="sxs-lookup"><span data-stu-id="7b1e6-186">**Figure 9**: Clicking On a Page Number Causes a Postback and Shows the Appropriate Subset of Records ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image17.png))</span></span>


## <a name="paging-s-server-side-workflow"></a><span data-ttu-id="7b1e6-187">分页的服务器端工作流</span><span class="sxs-lookup"><span data-stu-id="7b1e6-187">Paging s Server-Side Workflow</span></span>

<span data-ttu-id="7b1e6-188">当最终用户单击分页界面中的按钮上时，回发时，才会和在以下服务器端工作流开始：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-188">When the end user clicks on a button in the paging interface, a postback ensues and the following server-side workflow begins:</span></span>

1. <span data-ttu-id="7b1e6-189">GridView s （或 DetailsView 或 FormView）`PageIndexChanging`触发事件</span><span class="sxs-lookup"><span data-stu-id="7b1e6-189">The GridView s (or DetailsView or FormView) `PageIndexChanging` event fires</span></span>
2. <span data-ttu-id="7b1e6-190">重新请求 ObjectDataSource*所有*BLL; 中的数据的 GridView s`PageIndex`和`PageSize`属性值用于确定需要在 GridView 中显示的 BLL 从返回的记录</span><span class="sxs-lookup"><span data-stu-id="7b1e6-190">The ObjectDataSource re-requests *all* of the data from the BLL; the GridView s `PageIndex` and `PageSize` property values are used to determine what records returned from the BLL need to be displayed in the GridView</span></span>
3. <span data-ttu-id="7b1e6-191">GridView 的`PageIndexChanged`触发事件</span><span class="sxs-lookup"><span data-stu-id="7b1e6-191">The GridView s `PageIndexChanged` event fires</span></span>

<span data-ttu-id="7b1e6-192">步骤 2 中，在 ObjectDataSource 重新请求所有其数据源中的数据。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-192">In Step 2, the ObjectDataSource re-requests all of the data from its data source.</span></span> <span data-ttu-id="7b1e6-193">这种样式的分页通常称为*默认分页*，因为它的分页行为使用默认情况下设置时`AllowPaging`属性设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-193">This style of paging is commonly referred to as *default paging*, as it s the paging behavior used by default when setting the `AllowPaging` property to `true`.</span></span> <span data-ttu-id="7b1e6-194">默认值天真分页数据 Web 控件检索的数据，每个页面的所有记录，即使仅记录的子集实际呈现到的 HTML 发送到浏览器的 s。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-194">With default paging the data Web control naively retrieves all records for each page of data, even though only a subset of records are actually rendered into the HTML that s sent to the browser.</span></span> <span data-ttu-id="7b1e6-195">除非数据库数据缓存的 BLL 或对象数据源，则默认分页，为足够大的结果集或 web 应用程序与多个并发用户处于无法工作。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-195">Unless the database data is cached by the BLL or ObjectDataSource, default paging is unworkable for sufficiently large result sets or for web applications with many concurrent users.</span></span>

<span data-ttu-id="7b1e6-196">在下一教程中，我们将介绍如何实现*自定义分页*。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-196">In the next tutorial we'll examine how to implement *custom paging*.</span></span> <span data-ttu-id="7b1e6-197">使用自定义分页，您可以专门指示 ObjectDataSource 来仅检索精确的所需的请求的数据页的记录集。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-197">With custom paging you can specifically instruct the ObjectDataSource to only retrieve the precise set of records needed for the requested page of data.</span></span> <span data-ttu-id="7b1e6-198">可以想象，自定义分页极大地提高了效率较大的结果集进行分页。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-198">As you can imagine, custom paging greatly improves the efficiency of paging through large result sets.</span></span>

> [!NOTE]
> <span data-ttu-id="7b1e6-199">虽然许多用户同时使用分页通过足够大的结果集或的站点时，默认的分页不适合，意识到，自定义分页需要更多的更改和精力来实现，并且不是像选中一个复选框 （如是默认设置一样简单分页）。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-199">While default paging is not suitable when paging through sufficiently large result sets or for sites with many simultaneous users, realize that custom paging requires more changes and effort to implement and is not as simple as checking a checkbox (as is default paging).</span></span> <span data-ttu-id="7b1e6-200">因此，默认的分页可能是小型、 低流量的网站或相对较小的结果进行分页的设置时，因为它的最佳选择 s 更轻松、 更快速地实现。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-200">Therefore, default paging may be the ideal choice for small, low-traffic websites or when paging through relatively small result sets, as it s much easier and quicker to implement.</span></span>


<span data-ttu-id="7b1e6-201">例如，如果我们知道我们将在我们的数据库中永远不会有超过 100 个产品，通过它实现所需的工作量可能偏移享受的自定义分页的最小的性能提升。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-201">For example, if we know that we'll never have more than 100 products in our database, the minimal performance gain enjoyed by custom paging is likely offset by the effort required to implement it.</span></span> <span data-ttu-id="7b1e6-202">如果，但是，我们可能会一天有数千甚至上万个产品*不*实现自定义分页会极大地妨碍我们的应用程序的可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-202">If, however, we may one day have thousands or tens of thousands of products, *not* implementing custom paging would greatly hamper the scalability of our application.</span></span>

## <a name="step-4-customizing-the-paging-experience"></a><span data-ttu-id="7b1e6-203">步骤 4： 自定义分页体验</span><span class="sxs-lookup"><span data-stu-id="7b1e6-203">Step 4: Customizing the Paging Experience</span></span>

<span data-ttu-id="7b1e6-204">数据 Web 控件提供多个可用于增强用户的分页体验的属性。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-204">The data Web controls provide a number of properties that can be used to enhance the user s paging experience.</span></span> <span data-ttu-id="7b1e6-205">`PageCount`属性，例如，指示有多少总页数是，虽然`PageIndex`属性指示当前正在访问的页，可以设置将用户快速移动到特定的页。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-205">The `PageCount` property, for example, indicates how many total pages there are, while the `PageIndex` property indicates the current page being visited and can be set to quickly move a user to a specific page.</span></span> <span data-ttu-id="7b1e6-206">为了说明如何使用这些属性来改进用户的分页体验，让我们来添加一个标签 Web 控制对我们将通知用户哪些页面的页面它们重新当前访问，以及将 DropDownList 控件，其可快速跳转到任何给定页面.</span><span class="sxs-lookup"><span data-stu-id="7b1e6-206">To illustrate how to use these properties to improve upon the user s paging experience, let s add a Label Web control to our page that informs the user what page they re currently visiting, along with a DropDownList control that allows them to quickly jump to any given page.</span></span>

<span data-ttu-id="7b1e6-207">首先，将标签 Web 控件添加到您的页面，设置其`ID`属性设置为`PagingInformation`，并将清除其`Text`属性。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-207">First, add a Label Web control to your page, set its `ID` property to `PagingInformation`, and clear out its `Text` property.</span></span> <span data-ttu-id="7b1e6-208">接下来，创建事件处理程序的 GridView s`DataBound`事件，并添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-208">Next, create an event handler for the GridView s `DataBound` event and add the following code:</span></span>


[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample5.vb)]

<span data-ttu-id="7b1e6-209">此事件处理程序将分配`PagingInformation`标签 s`Text`属性设置为消息通知用户页面当前访问`Products.PageIndex + 1`出多少总页数`Products.PageCount`(我们将添加到 1`Products.PageIndex`属性因为`PageIndex`编制索引的索引从 0 开始)。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-209">This event handler assigns the `PagingInformation` Label s `Text` property to a message informing the user the page they are currently visiting `Products.PageIndex + 1` out of how many total pages `Products.PageCount` (we add 1 to the `Products.PageIndex` property because `PageIndex` is indexed starting at 0).</span></span> <span data-ttu-id="7b1e6-210">我选择将此标签 s`Text`中的属性`DataBound`事件处理程序，而不是`PageIndexChanged`事件处理程序由于`DataBound`事件将激发每次数据绑定到 GridView 而`PageIndexChanged`事件处理程序页索引更改时激发。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-210">I chose the assign this Label s `Text` property in the `DataBound` event handler as opposed to the `PageIndexChanged` event handler because the `DataBound` event fires every time data is bound to the GridView whereas the `PageIndexChanged` event handler only fires when the page index is changed.</span></span> <span data-ttu-id="7b1e6-211">当 GridView 最初是绑定到的第一页上的数据访问时，`PageIndexChanging`事件不是 t 火灾 (而`DataBound`事件的作用)。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-211">When the GridView is initially data bound on the first page visit, the `PageIndexChanging` event doesn t fire (whereas the `DataBound` event does).</span></span>

<span data-ttu-id="7b1e6-212">添加此元素后，用户现已显示一条消息指出正在访问哪些页面和有多少总页的数据。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-212">With this addition, the user is now shown a message indicating what page they are visiting and how many total pages of data there are.</span></span>


<span data-ttu-id="7b1e6-213">[![显示当前页码和总页数](paging-and-sorting-report-data-vb/_static/image19.png)](paging-and-sorting-report-data-vb/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-213">[![The Current Page Number and Total Number of Pages are Displayed](paging-and-sorting-report-data-vb/_static/image19.png)](paging-and-sorting-report-data-vb/_static/image18.png)</span></span>

<span data-ttu-id="7b1e6-214">**图 10**： 显示当前页码和总页数 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="7b1e6-214">**Figure 10**: The Current Page Number and Total Number of Pages are Displayed ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image20.png))</span></span>


<span data-ttu-id="7b1e6-215">除了标签控件，让我们来还添加 DropDownList 控件，其中列出与当前正在查看的页面选择了 GridView 中的页码。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-215">In addition to the Label control, let s also add a DropDownList control that lists the page numbers in the GridView with the currently viewed page selected.</span></span> <span data-ttu-id="7b1e6-216">这里的思路是，用户可快速跳转从当前页到另一个只需从下拉列表中选择新的页索引。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-216">The idea here is that the user can quickly jump from the current page to another by simply selecting the new page index from the DropDownList.</span></span> <span data-ttu-id="7b1e6-217">首先将 DropDownList 添加到设计器中，设置其`ID`属性设置为`PageList`，从其智能标记启用自动回发选项。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-217">Start by adding a DropDownList to the Designer, setting its `ID` property to `PageList` and checking the Enable AutoPostBack option from its smart tag.</span></span>

<span data-ttu-id="7b1e6-218">接下来，返回到`DataBound`事件处理程序并添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-218">Next, return to the `DataBound` event handler and add the following code:</span></span>


[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample6.vb)]

<span data-ttu-id="7b1e6-219">此代码首先清除中项的布局`PageList`DropDownList。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-219">This code begins by clearing out the items in the `PageList` DropDownList.</span></span> <span data-ttu-id="7b1e6-220">这可能是多余的因为一个对 t 期望的页数，若要更改，但其他用户可能会同时使用系统、 添加或删除的记录`Products`表。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-220">This may seem superfluous, since one wouldn t expect the number of pages to change, but other users may be using the system simultaneously, adding or removing records from the `Products` table.</span></span> <span data-ttu-id="7b1e6-221">此类插入或删除无法更改数据的页数。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-221">Such insertions or deletions could alter the number of pages of data.</span></span>

<span data-ttu-id="7b1e6-222">接下来，我们需要再次创建页号并具有一个映射到当前的 GridView`PageIndex`默认选中状态。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-222">Next, we need to create the page numbers again and have the one that maps to the current GridView `PageIndex` selected by default.</span></span> <span data-ttu-id="7b1e6-223">我们实现此目的使用从 0 到循环`PageCount - 1`，添加一个新`ListItem`中每个迭代和设置其`Selected`属性设置为 true，如果当前迭代索引等于 GridView 的`PageIndex`属性。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-223">We accomplish this with a loop from 0 to `PageCount - 1`, adding a new `ListItem` in each iteration and setting its `Selected` property to true if the current iteration index equals the GridView s `PageIndex` property.</span></span>

<span data-ttu-id="7b1e6-224">最后，我们需要创建的事件处理程序的 DropDownList s`SelectedIndexChanged`触发的事件，每当用户选择从列表中的另一个项。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-224">Finally, we need to create an event handler for the DropDownList s `SelectedIndexChanged` event, which fires each time the user pick a different item from the list.</span></span> <span data-ttu-id="7b1e6-225">若要创建此事件处理程序，只需双击在设计器，DropDownList，然后添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-225">To create this event handler, simply double-click the DropDownList in the Designer, then add the following code:</span></span>


[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample7.vb)]

<span data-ttu-id="7b1e6-226">如图 11 所示，只更改 GridView 的`PageIndex`属性会导致数据重新绑定到 GridView。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-226">As Figure 11 shows, merely changing the GridView s `PageIndex` property causes the data to be rebound to the GridView.</span></span> <span data-ttu-id="7b1e6-227">在 GridView`DataBound`事件处理程序，相应的 DropDownList`ListItem`处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-227">In the GridView s `DataBound` event handler, the appropriate DropDownList `ListItem` is selected.</span></span>


<span data-ttu-id="7b1e6-228">[![用户将自动转到第六个页时选择页面 6 下拉列表项](paging-and-sorting-report-data-vb/_static/image22.png)](paging-and-sorting-report-data-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-228">[![The User is Automatically Taken to the Sixth Page When Selecting the Page 6 Drop-Down List Item](paging-and-sorting-report-data-vb/_static/image22.png)](paging-and-sorting-report-data-vb/_static/image21.png)</span></span>

<span data-ttu-id="7b1e6-229">**图 11**: 用户将自动转到第六个页时选择页面 6 下拉列表项 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image23.png))</span><span class="sxs-lookup"><span data-stu-id="7b1e6-229">**Figure 11**: The User is Automatically Taken to the Sixth Page When Selecting the Page 6 Drop-Down List Item ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image23.png))</span></span>


## <a name="step-5-adding-bi-directional-sorting-support"></a><span data-ttu-id="7b1e6-230">步骤 5： 添加排序的双向支持</span><span class="sxs-lookup"><span data-stu-id="7b1e6-230">Step 5: Adding Bi-Directional Sorting Support</span></span>

<span data-ttu-id="7b1e6-231">添加双向语言排序支持非常简单，只添加分页支持只需选中 GridView s 智能标记中的启用排序选项 (用于设置 GridView s [ `AllowSorting`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx)到`true`)。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-231">Adding bi-directional sorting support is as simple as adding paging support simply check the Enable Sorting option from the GridView s smart tag (which sets the GridView s [`AllowSorting` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx) to `true`).</span></span> <span data-ttu-id="7b1e6-232">这会使每个的 GridView 的字段标头作为 Linkbutton，单击时，会导致回发并返回按所单击的列以升序排序的数据。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-232">This renders each of the headers of the GridView s fields as LinkButtons that, when clicked, cause a postback and return the data sorted by the clicked column in ascending order.</span></span> <span data-ttu-id="7b1e6-233">再次单击 LinkButton 的同一个标头重新对数据进行排序降序排序。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-233">Clicking the same header LinkButton again re-sorts the data in descending order.</span></span>

> [!NOTE]
> <span data-ttu-id="7b1e6-234">如果使用自定义的数据访问层而不是类型化数据集，您可能没有启用排序的选项中的 GridView s 智能标记。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-234">If you are using a custom Data Access Layer rather than a Typed DataSet, you may not have an Enable Sorting option in the GridView s smart tag.</span></span> <span data-ttu-id="7b1e6-235">仅绑定到数据源以本机方式支持排序的 Gridview 有可用此复选框。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-235">Only GridViews bound to data sources that natively support sorting have this checkbox available.</span></span> <span data-ttu-id="7b1e6-236">类型化数据集提供了开箱排序支持，因为 ADO.NET DataTable 提供`Sort`方法，调用时，对使用指定的条件的 Datarow 的 DataTable s 进行排序。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-236">The Typed DataSet provides out-of-the-box sorting support since the ADO.NET DataTable provides a `Sort` method that, when invoked, sorts the DataTable s DataRows using the criteria specified.</span></span>


<span data-ttu-id="7b1e6-237">如果将 DAL 不返回由 DAL 的本机支持排序将需要配置 ObjectDataSource 要传递给业务逻辑层，以对数据进行排序或具有数据的排序信息排序的对象。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-237">If your DAL does not return objects that natively support sorting you will need to configure the ObjectDataSource to pass sorting information to the Business Logic Layer, which can either sort the data or have the data sorted by the DAL.</span></span> <span data-ttu-id="7b1e6-238">我们将探讨如何对数据的业务逻辑和数据访问层在将来的教程中进行排序。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-238">We'll explore how to sort data at the Business Logic and Data Access Layers in a future tutorial.</span></span>

<span data-ttu-id="7b1e6-239">排序 Linkbutton 呈现为 HTML 超链接，其当前的颜色 （蓝色表示未访问的链接和已访问链接深红色） 冲突与标题行的背景色。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-239">The sorting LinkButtons are rendered as HTML hyperlinks, whose current colors (blue for an unvisited link and a dark red for a visited link) clash with the background color of the header row.</span></span> <span data-ttu-id="7b1e6-240">相反，let s 具有所有标头行链接中显示为空白，而不管是否它们 ve 已或未访问过。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-240">Instead, let s have all header row links displayed in white, regardless of whether they ve been visited or not.</span></span> <span data-ttu-id="7b1e6-241">这可以通过添加以下`Styles.css`类：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-241">This can be accomplished by adding the following to the `Styles.css` class:</span></span>


[!code-css[Main](paging-and-sorting-report-data-vb/samples/sample8.css)]

<span data-ttu-id="7b1e6-242">此语法指示要显示的元素，使用 HeaderStyle 类中的这些超链接时使用白色文本。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-242">This syntax indicates to use white text when displaying those hyperlinks within an element that uses the HeaderStyle class.</span></span>

<span data-ttu-id="7b1e6-243">之后此 CSS 元素后，访问通过浏览器页面时在屏幕上将看到类似于图 12。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-243">After this CSS addition, when visiting the page through a browser your screen should look similar to Figure 12.</span></span> <span data-ttu-id="7b1e6-244">具体而言，图 12 显示结果后单击价格字段 s 标头链接。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-244">In particular, Figure 12 shows the results after the Price field s header link has been clicked.</span></span>


<span data-ttu-id="7b1e6-245">[![结果已按升序排序单价](paging-and-sorting-report-data-vb/_static/image25.png)](paging-and-sorting-report-data-vb/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-245">[![The Results Have Been Sorted by the UnitPrice in Ascending Order](paging-and-sorting-report-data-vb/_static/image25.png)](paging-and-sorting-report-data-vb/_static/image24.png)</span></span>

<span data-ttu-id="7b1e6-246">**图 12**: 结果具有已按升序顺序单价 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="7b1e6-246">**Figure 12**: The Results Have Been Sorted by the UnitPrice in Ascending Order ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image26.png))</span></span>


## <a name="examining-the-sorting-workflow"></a><span data-ttu-id="7b1e6-247">检查排序的工作流</span><span class="sxs-lookup"><span data-stu-id="7b1e6-247">Examining the Sorting Workflow</span></span>

<span data-ttu-id="7b1e6-248">所有 GridView 都字段 BoundField、 CheckBoxField、 TemplateField，并等具有`SortExpression`属性，指示应使用对数据进行排序时单击该字段 s 排序标头链接的表达式。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-248">All GridView fields the BoundField, CheckBoxField, TemplateField, and so on have a `SortExpression` property that indicates the expression that should be used to sort the data when that field s sorting header link is clicked.</span></span> <span data-ttu-id="7b1e6-249">这个 GridView 也有`SortExpression`属性。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-249">The GridView also has a `SortExpression` property.</span></span> <span data-ttu-id="7b1e6-250">GridView 时单击 LinkButton 排序的标头，将该字段 s 分配`SortExpression`值设为其`SortExpression`属性。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-250">When a sorting header LinkButton is clicked, the GridView assigns that field s `SortExpression` value to its `SortExpression` property.</span></span> <span data-ttu-id="7b1e6-251">接下来，并将数据重新检索 ObjectDataSource 中根据 GridView s 排序`SortExpression`属性。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-251">Next, the data is re-retrieved from the ObjectDataSource and sorted according to the GridView s `SortExpression` property.</span></span> <span data-ttu-id="7b1e6-252">以下列表详细说明了怎样时最终用户对 GridView 中的数据进行排序步骤的顺序：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-252">The following list details the sequence of steps that transpires when an end user sorts the data in a GridView:</span></span>

1. <span data-ttu-id="7b1e6-253">GridView s [Sorting 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx)激发</span><span class="sxs-lookup"><span data-stu-id="7b1e6-253">The GridView s [Sorting event](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx) fires</span></span>
2. <span data-ttu-id="7b1e6-254">GridView s [ `SortExpression`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx)设置为`SortExpression`字段的单击 LinkButton 了其排序的标头</span><span class="sxs-lookup"><span data-stu-id="7b1e6-254">The GridView s [`SortExpression` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) is set to the `SortExpression` of the field whose sorting header LinkButton was clicked</span></span>
3. <span data-ttu-id="7b1e6-255">ObjectDataSource 重新检索所有 BLL 中的数据，然后对使用 GridView s 的数据进行排序 `SortExpression`</span><span class="sxs-lookup"><span data-stu-id="7b1e6-255">The ObjectDataSource re-retrieves all of the data from the BLL and then sorts the data using the GridView s `SortExpression`</span></span>
4. <span data-ttu-id="7b1e6-256">GridView 的`PageIndex`属性重置为 0，这意味着，对用户进行排序时返回到数据 （假设实现分页支持） 的第一页</span><span class="sxs-lookup"><span data-stu-id="7b1e6-256">The GridView s `PageIndex` property is reset to 0, meaning that when sorting the user is returned to the first page of data (assuming paging support has been implemented)</span></span>
5. <span data-ttu-id="7b1e6-257">GridView s [ `Sorted`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx)激发</span><span class="sxs-lookup"><span data-stu-id="7b1e6-257">The GridView s [`Sorted` event](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx) fires</span></span>

<span data-ttu-id="7b1e6-258">像默认分页，请使用默认排序选项重新检索*所有*的 BLL 中的记录。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-258">Like with default paging, the default sorting option re-retrieves *all* of the records from the BLL.</span></span> <span data-ttu-id="7b1e6-259">使用排序没有分页或在使用使用进行排序时的默认分页，那里 s 没有办法避开此性能下降 （除了缓存数据库数据）。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-259">When using sorting without paging or when using sorting with default paging, there s no way to circumvent this performance hit (short of caching the database data).</span></span> <span data-ttu-id="7b1e6-260">但是，正如我们在将来的教程中，将看到它可以有效地对数据进行排序时使用自定义分页。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-260">However, as we'll see in a future tutorial, it s possible to efficiently sort data when using custom paging.</span></span>

<span data-ttu-id="7b1e6-261">每个 GridView 字段绑定到 GridView s 智能标记中的下拉列表通过 GridView ObjectDataSource 时, 自动有其`SortExpression`属性分配给中的数据字段的名称`ProductsRow`类。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-261">When binding an ObjectDataSource to the GridView through the drop-down list in the GridView s smart tag, each GridView field automatically has its `SortExpression` property assigned to the name of the data field in the `ProductsRow` class.</span></span> <span data-ttu-id="7b1e6-262">例如， `ProductName` BoundField s`SortExpression`设置为`ProductName`，如下面的声明性标记中所示：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-262">For example, the `ProductName` BoundField s `SortExpression` is set to `ProductName`, as shown in the following declarative markup:</span></span>


[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample9.aspx)]

<span data-ttu-id="7b1e6-263">可以配置一个字段，以便它 s 不可排序通过清除其`SortExpression`属性 （将其分配给一个空字符串）。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-263">A field can be configured so that it s not sortable by clearing out its `SortExpression` property (assigning it to an empty string).</span></span> <span data-ttu-id="7b1e6-264">为了说明这一点，想象一下，我们并没有 t 想要让客户对我们的产品价格进行排序。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-264">To illustrate this, imagine that we didn t want to let our customers sort our products by price.</span></span> <span data-ttu-id="7b1e6-265">`UnitPrice` BoundField 的`SortExpression`从声明性标记或通过字段对话框中 （这是通过单击 GridView s 智能标记中的编辑列链接的访问），可以删除属性。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-265">The `UnitPrice` BoundField s `SortExpression` property can be removed either from the declarative markup or through the Fields dialog box (which is accessible by clicking on the Edit Columns link in the GridView s smart tag).</span></span>


![结果已按升序排序单价](paging-and-sorting-report-data-vb/_static/image27.png)

<span data-ttu-id="7b1e6-267">**图 13**： 结果已按升序排序单价</span><span class="sxs-lookup"><span data-stu-id="7b1e6-267">**Figure 13**: The Results Have Been Sorted by the UnitPrice in Ascending Order</span></span>


<span data-ttu-id="7b1e6-268">一次`SortExpression`属性已被移除。 `UnitPrice` BoundField 标头将呈现为文本而不是作为链接，从而防止用户对数据进行排序的价格。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-268">Once the `SortExpression` property has been removed for the `UnitPrice` BoundField, the header is rendered as text rather than as a link, thereby preventing users from sorting the data by price.</span></span>


<span data-ttu-id="7b1e6-269">[![通过删除 SortExpression 属性，用户不再可以进行排序的产品价格](paging-and-sorting-report-data-vb/_static/image29.png)](paging-and-sorting-report-data-vb/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-269">[![By Removing the SortExpression Property, Users Can No Longer Sort the Products By Price](paging-and-sorting-report-data-vb/_static/image29.png)](paging-and-sorting-report-data-vb/_static/image28.png)</span></span>

<span data-ttu-id="7b1e6-270">**图 14**： 通过删除 SortExpression 属性，用户可以不再对产品的价格 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image30.png))</span><span class="sxs-lookup"><span data-stu-id="7b1e6-270">**Figure 14**: By Removing the SortExpression Property, Users Can No Longer Sort the Products By Price ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image30.png))</span></span>


## <a name="programmatically-sorting-the-gridview"></a><span data-ttu-id="7b1e6-271">以编程方式排序 GridView</span><span class="sxs-lookup"><span data-stu-id="7b1e6-271">Programmatically Sorting the GridView</span></span>

<span data-ttu-id="7b1e6-272">您还可以进行排序的 GridView 内容以编程方式使用 GridView s [ `Sort`方法](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-272">You can also sort the contents of the GridView programmatically by using the GridView s [`Sort` method](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx).</span></span> <span data-ttu-id="7b1e6-273">只需传入`SortExpression`值作为排序依据连同[ `SortDirection` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) (`Ascending`或`Descending`)，GridView 的数据都将重新排序。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-273">Simply pass in the `SortExpression` value to sort by along with the [`SortDirection`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) (`Ascending` or `Descending`), and the GridView s data will be re-sorted.</span></span>

<span data-ttu-id="7b1e6-274">假设原因我们关闭排序通过`UnitPrice`是的因为我们担心我们的客户会只是购买仅价格最低的产品。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-274">Imagine that the reason we turned off sorting by the `UnitPrice` was because we were worried that our customers would simply buy only the lowest-priced products.</span></span> <span data-ttu-id="7b1e6-275">但是，我们想要鼓励他们购买的成本最高的产品，因此我们 d 喜欢它们能够进行排序的产品的价格，但只能从成本最高价格到最少。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-275">However, we want to encourage them to buy the most expensive products, so we d like them to be able to sort the products by price, but only from the most expensive price to the least.</span></span>

<span data-ttu-id="7b1e6-276">若要完成这将按钮 Web 控件添加到页上，设置其`ID`属性设置为`SortPriceDescending`，并将其`Text`价格按排序的属性。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-276">To accomplish this add a Button Web control to the page, set its `ID` property to `SortPriceDescending`, and its `Text` property to Sort by Price.</span></span> <span data-ttu-id="7b1e6-277">接下来，为 s 按钮创建一个事件处理程序`Click`通过双击设计器中的按钮控件的事件。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-277">Next, create an event handler for the Button s `Click` event by double-clicking the Button control in the Designer.</span></span> <span data-ttu-id="7b1e6-278">将以下代码添加到此事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-278">Add the following code to this event handler:</span></span>


[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample10.vb)]

<span data-ttu-id="7b1e6-279">单击此按钮使用户返回到第一页与按定价从最代价高昂的开销最少 （请参阅图 15） 排序的产品。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-279">Clicking this Button returns the user to the first page with the products sorted by price, from most expensive to least expensive (see Figure 15).</span></span>


<span data-ttu-id="7b1e6-280">[![单击按钮进行排序的产品从成本最高到最低](paging-and-sorting-report-data-vb/_static/image32.png)](paging-and-sorting-report-data-vb/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-280">[![Clicking the Button Orders the Products From the Most Expensive to the Least](paging-and-sorting-report-data-vb/_static/image32.png)](paging-and-sorting-report-data-vb/_static/image31.png)</span></span>

<span data-ttu-id="7b1e6-281">**图 15**： 单击的按钮进行排序的产品从最高到最少 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image33.png))</span><span class="sxs-lookup"><span data-stu-id="7b1e6-281">**Figure 15**: Clicking the Button Orders the Products From the Most Expensive to the Least ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image33.png))</span></span>


## <a name="summary"></a><span data-ttu-id="7b1e6-282">总结</span><span class="sxs-lookup"><span data-stu-id="7b1e6-282">Summary</span></span>

<span data-ttu-id="7b1e6-283">在本教程中我们已了解如何实现默认分页和排序功能，这两个已像选中一个复选框一样简单 ！</span><span class="sxs-lookup"><span data-stu-id="7b1e6-283">In this tutorial we saw how to implement default paging and sorting capabilities, both of which were as easy as checking a checkbox!</span></span> <span data-ttu-id="7b1e6-284">当用户进行排序或数据进行分页时，则展开类似的工作流：</span><span class="sxs-lookup"><span data-stu-id="7b1e6-284">When a user sorts or pages through data, a similar workflow unfolds:</span></span>

1. <span data-ttu-id="7b1e6-285">回发时，才会</span><span class="sxs-lookup"><span data-stu-id="7b1e6-285">A postback ensues</span></span>
2. <span data-ttu-id="7b1e6-286">数据 Web 控件 s 预级别触发事件 (`PageIndexChanging`或`Sorting`)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-286">The data Web control s pre-level event fires (`PageIndexChanging` or `Sorting`)</span></span>
3. <span data-ttu-id="7b1e6-287">所有数据将重新检索对象数据源</span><span class="sxs-lookup"><span data-stu-id="7b1e6-287">All of the data is re-retrieved by the ObjectDataSource</span></span>
4. <span data-ttu-id="7b1e6-288">数据 Web 控件 s 后级别触发事件 (`PageIndexChanged`或`Sorted`)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-288">The data Web control s post-level event fires (`PageIndexChanged` or `Sorted`)</span></span>

<span data-ttu-id="7b1e6-289">尽管实现基本的分页和排序非常简单，以利用更有效的自定义分页或进一步增强分页或排序接口必须施加更多的工作。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-289">While implementing basic paging and sorting is a breeze, more effort must be exerted to utilize the more efficient custom paging or to further enhance the paging or sorting interface.</span></span> <span data-ttu-id="7b1e6-290">将来的教程将探讨这些主题。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-290">Future tutorials will explore these topics.</span></span>

<span data-ttu-id="7b1e6-291">快乐编程 ！</span><span class="sxs-lookup"><span data-stu-id="7b1e6-291">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="7b1e6-292">关于作者</span><span class="sxs-lookup"><span data-stu-id="7b1e6-292">About the Author</span></span>

<span data-ttu-id="7b1e6-293">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-293">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="7b1e6-294">Scott 是独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-294">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="7b1e6-295">他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-295">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="7b1e6-296">他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-296">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="7b1e6-297">或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="7b1e6-297">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7b1e6-298">[上一页](creating-a-customized-sorting-user-interface-cs.md)
> [下一页](efficiently-paging-through-large-amounts-of-data-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7b1e6-298">[Previous](creating-a-customized-sorting-user-interface-cs.md)
[Next](efficiently-paging-through-large-amounts-of-data-vb.md)</span></span>
