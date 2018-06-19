---
uid: web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-vb
title: 分页和排序报告数据 (VB) |Microsoft 文档
author: rick-anderson
description: 分页和排序是两个非常常见功能，当在联机应用程序中显示数据。 在本教程中我们将首先查看一下添加排序和...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2006
ms.topic: article
ms.assetid: b895e37e-0e69-45cc-a7e4-17ddd2e1b38d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-vb
msc.type: authoredcontent
ms.openlocfilehash: c5e7e110d436caa7b7526eae105fde601367007a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30887234"
---
<a name="paging-and-sorting-report-data-vb"></a><span data-ttu-id="7fb5c-104">分页和排序报表数据 (VB)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-104">Paging and Sorting Report Data (VB)</span></span>
====================
<span data-ttu-id="7fb5c-105">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="7fb5c-106">[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_VB.exe)或[下载 PDF](paging-and-sorting-report-data-vb/_static/datatutorial24vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-106">[Download Sample App](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_VB.exe) or [Download PDF](paging-and-sorting-report-data-vb/_static/datatutorial24vb1.pdf)</span></span>

> <span data-ttu-id="7fb5c-107">分页和排序是两个非常常见功能，当在联机应用程序中显示数据。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-107">Paging and sorting are two very common features when displaying data in an online application.</span></span> <span data-ttu-id="7fb5c-108">在本教程中我们将花首先查看一下添加排序和分页至我们的报表，我们将然后相互依赖在将来的教程。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-108">In this tutorial we'll take a first look at adding sorting and paging to our reports, which we will then build upon in future tutorials.</span></span>


## <a name="introduction"></a><span data-ttu-id="7fb5c-109">介绍</span><span class="sxs-lookup"><span data-stu-id="7fb5c-109">Introduction</span></span>

<span data-ttu-id="7fb5c-110">分页和排序是两个非常常见功能，当在联机应用程序中显示数据。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-110">Paging and sorting are two very common features when displaying data in an online application.</span></span> <span data-ttu-id="7fb5c-111">例如，当搜索时在联机书店 ASP.NET 丛书，可能有数百个此类丛书，但此报表列出搜索结果将列出每页的仅十个匹配项。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-111">For example, when searching for ASP.NET books at an online bookstore, there may be hundreds of such books, but the report listing the search results lists only ten matches per page.</span></span> <span data-ttu-id="7fb5c-112">此外，可以按标题、 价格、 页计数、 作者姓名等排序结果。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-112">Moreover, the results can be sorted by title, price, page count, author name, and so on.</span></span> <span data-ttu-id="7fb5c-113">而的过去 23 教程已学习了如何生成各种报表，包括接口，它允许添加、 编辑和删除数据，我们看不到如何进行排序数据和唯一的已分页示例我们看到已被使用说明和 FormView控件。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-113">While the past 23 tutorials have examined how to build a variety of reports, including interfaces that permit adding, editing, and deleting data, we ve not looked at how to sort data and the only paging examples we ve seen have been with the DetailsView and FormView controls.</span></span>

<span data-ttu-id="7fb5c-114">在本教程中我们将了解如何添加排序和分页至我们的报表，这可以通过只需检查几个复选框完成。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-114">In this tutorial we'll see how to add sorting and paging to our reports, which can be accomplished by simply checking a few checkboxes.</span></span> <span data-ttu-id="7fb5c-115">遗憾的是，这个简单的实施有排序接口离开一个位需要改进其缺点和分页例程不用于有效地进行分页大型结果集。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-115">Unfortunately, this simplistic implementation has its drawbacks the sorting interface leaves a bit to be desired and the paging routines are not designed for efficiently paging through large result sets.</span></span> <span data-ttu-id="7fb5c-116">将来的教程将探索如何克服的-现成分页和排序解决方案的限制。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-116">Future tutorials will explore how to overcome the limitations of the out-of-the-box paging and sorting solutions.</span></span>

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a><span data-ttu-id="7fb5c-117">步骤 1： 添加分页和排序教程网页</span><span class="sxs-lookup"><span data-stu-id="7fb5c-117">Step 1: Adding the Paging and Sorting Tutorial Web Pages</span></span>

<span data-ttu-id="7fb5c-118">在开始本教程之前，让 s 先花点时间添加我们需要以及本教程的下一步的三个 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-118">Before we start this tutorial, let s first take a moment to add the ASP.NET pages we'll need for this tutorial and the next three.</span></span> <span data-ttu-id="7fb5c-119">首先创建一个新文件夹中名为的项目`PagingAndSorting`。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-119">Start by creating a new folder in the project named `PagingAndSorting`.</span></span> <span data-ttu-id="7fb5c-120">接下来，将以下五个 ASP.NET 页添加到此文件夹中，让所有的它们配置为使用母版页`Site.master`:</span><span class="sxs-lookup"><span data-stu-id="7fb5c-120">Next, add the following five ASP.NET pages to this folder, having all of them configured to use the master page `Site.master`:</span></span>

- `Default.aspx`
- `SimplePagingSorting.aspx`
- `EfficientPaging.aspx`
- `SortParameter.aspx`
- `CustomSortingUI.aspx`


![创建 PagingAndSorting 文件夹并添加教程 ASP.NET 页](paging-and-sorting-report-data-vb/_static/image1.png)

<span data-ttu-id="7fb5c-122">**图 1**： 创建 PagingAndSorting 文件夹并添加教程 ASP.NET 页</span><span class="sxs-lookup"><span data-stu-id="7fb5c-122">**Figure 1**: Create a PagingAndSorting Folder and Add the Tutorial ASP.NET Pages</span></span>


<span data-ttu-id="7fb5c-123">接下来，打开`Default.aspx`页上，并将其拖`SectionLevelTutorialListing.ascx`从用户控件`UserControls`到设计图面上的文件夹。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-123">Next, open the `Default.aspx` page and drag the `SectionLevelTutorialListing.ascx` User Control from the `UserControls` folder onto the Design surface.</span></span> <span data-ttu-id="7fb5c-124">用户控件中，我们在中创建的[母版页和网站的导航](../introduction/master-pages-and-site-navigation-vb.md)教程中，枚举站点图，并在项目符号列表中的当前节中显示这些教程。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-124">This User Control, which we created in the [Master Pages and Site Navigation](../introduction/master-pages-and-site-navigation-vb.md) tutorial, enumerates the site map and displays those tutorials in the current section in a bulleted list.</span></span>


![SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](paging-and-sorting-report-data-vb/_static/image2.png)

<span data-ttu-id="7fb5c-126">**图 2**: SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx</span><span class="sxs-lookup"><span data-stu-id="7fb5c-126">**Figure 2**: Add the SectionLevelTutorialListing.ascx User Control to Default.aspx</span></span>


<span data-ttu-id="7fb5c-127">为了具有显示分页和排序的教程中我们将创建的项目符号列表，我们需要将它们添加到站点映射。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-127">In order to have the bulleted list display the paging and sorting tutorials we'll be creating, we need to add them to the site map.</span></span> <span data-ttu-id="7fb5c-128">打开`Web.sitemap`文件，并在编辑、 插入、 和删除站点映射节点标记后添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-128">Open the `Web.sitemap` file and add the following markup after the Editing, Inserting, and Deleting site map node markup:</span></span>


[!code-xml[Main](paging-and-sorting-report-data-vb/samples/sample1.xml)]


![更新包括新的 ASP.NET 页的站点图](paging-and-sorting-report-data-vb/_static/image3.png)

<span data-ttu-id="7fb5c-130">**图 3**： 更新包括新的 ASP.NET 页的站点图</span><span class="sxs-lookup"><span data-stu-id="7fb5c-130">**Figure 3**: Update the Site Map to Include the New ASP.NET Pages</span></span>


## <a name="step-2-displaying-product-information-in-a-gridview"></a><span data-ttu-id="7fb5c-131">步骤 2： 在一个 GridView 中显示产品信息</span><span class="sxs-lookup"><span data-stu-id="7fb5c-131">Step 2: Displaying Product Information in a GridView</span></span>

<span data-ttu-id="7fb5c-132">我们实际上实现分页和排序功能之前，让我们来首先创建标准非-srotable，列出产品信息的不可分页 GridView。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-132">Before we actually implement paging and sorting capabilities, let s first create a standard non-srotable, non-pageable GridView that lists the product information.</span></span> <span data-ttu-id="7fb5c-133">这是一项任务我们已多次在此之前完成本教程系列中因此这些步骤应该会熟悉。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-133">This is a task we ve done many times before throughout this tutorial series so these steps should be familiar.</span></span> <span data-ttu-id="7fb5c-134">首先打开`SimplePagingSorting.aspx`页上，并将一个 GridView 控件从工具箱中拖动到设计器中，设置其`ID`属性`Products`。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-134">Start by opening the `SimplePagingSorting.aspx` page and drag a GridView control from the Toolbox onto the Designer, setting its `ID` property to `Products`.</span></span> <span data-ttu-id="7fb5c-135">接下来，创建新对象数据源使用的 ProductsBLL 类的`GetProducts()`方法以返回所有产品信息。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-135">Next, create a new ObjectDataSource that uses the ProductsBLL class s `GetProducts()` method to return all of the product information.</span></span>


![检索有关所有使用 GetProducts() 方法的产品信息](paging-and-sorting-report-data-vb/_static/image4.png)

<span data-ttu-id="7fb5c-137">**图 4**： 检索有关所有使用 GetProducts() 方法的产品信息</span><span class="sxs-lookup"><span data-stu-id="7fb5c-137">**Figure 4**: Retrieve Information About All of the Products Using the GetProducts() Method</span></span>


<span data-ttu-id="7fb5c-138">由于此报表不是只读的报表、 在该处 s 需要映射 ObjectDataSource s `Insert()`， `Update()`，或`Delete()`到对应的方法`ProductsBLL`方法; 因此，请 （无） 从下拉列表中选择更新，INSERT、和删除选项卡。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-138">Since this report is a read-only report, there s no need to map the ObjectDataSource s `Insert()`, `Update()`, or `Delete()` methods to corresponding `ProductsBLL` methods; therefore, choose (None) from the drop-down list for the UPDATE, INSERT, and DELETE tabs.</span></span>


![选择 （无） 选项的下拉列表中插入、 更新和删除选项卡](paging-and-sorting-report-data-vb/_static/image5.png)

<span data-ttu-id="7fb5c-140">**图 5**： 选择 （无） 选项的下拉列表中插入、 更新和删除选项卡</span><span class="sxs-lookup"><span data-stu-id="7fb5c-140">**Figure 5**: Choose the (None) Option in the Drop-Down List in the UPDATE, INSERT, and DELETE Tabs</span></span>


<span data-ttu-id="7fb5c-141">接下来，让 s 自定义的 GridView 的字段，以便显示仅产品名称、 供应商、 类别、 价格和停用的状态。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-141">Next, let s customize the GridView s fields so that only the products names, suppliers, categories, prices, and discontinued statuses are displayed.</span></span> <span data-ttu-id="7fb5c-142">此外，随意使任何字段级别格式设置发生更改，例如调整`HeaderText`属性或格式设置为货币的价格。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-142">Furthermore, feel free to make any field-level formatting changes, such as adjusting the `HeaderText` properties or formatting the price as a currency.</span></span> <span data-ttu-id="7fb5c-143">这些更改后 GridView s 声明性标记应看起来类似以下：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-143">After these changes, your GridView s declarative markup should look similar to the following:</span></span>


[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample2.aspx)]

<span data-ttu-id="7fb5c-144">通过浏览器查看时为止图 6 显示我们的进度。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-144">Figure 6 shows our progress thus far when viewed through a browser.</span></span> <span data-ttu-id="7fb5c-145">请注意页列出所有在一个屏幕中，显示每个产品的名称、 类别、 供应商、 价格、 产品和停用状态。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-145">Note that the page lists all of the products in one screen, showing each product s name, category, supplier, price, and discontinued status.</span></span>


<span data-ttu-id="7fb5c-146">[![每个产品列出](paging-and-sorting-report-data-vb/_static/image7.png)](paging-and-sorting-report-data-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-146">[![Each of the Products are Listed](paging-and-sorting-report-data-vb/_static/image7.png)](paging-and-sorting-report-data-vb/_static/image6.png)</span></span>

<span data-ttu-id="7fb5c-147">**图 6**： 每个产品列出 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="7fb5c-147">**Figure 6**: Each of the Products are Listed ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image8.png))</span></span>


## <a name="step-3-adding-paging-support"></a><span data-ttu-id="7fb5c-148">步骤 3： 添加分页支持</span><span class="sxs-lookup"><span data-stu-id="7fb5c-148">Step 3: Adding Paging Support</span></span>

<span data-ttu-id="7fb5c-149">列出*所有*在一个屏幕上的产品可能会导致用户浏览数据的信息重载。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-149">Listing *all* of the products on one screen can lead to information overload for the user perusing the data.</span></span> <span data-ttu-id="7fb5c-150">为了帮助使结果更易于管理，我们可以中断将数据分成较小的数据页，并允许用户一次单步执行一页数据。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-150">To help make the results more manageable, we can break up the data into smaller pages of data and allow the user to step through the data one page at a time.</span></span> <span data-ttu-id="7fb5c-151">若要完成这只需选中从 GridView s 智能标记启用分页复选框 (这将设置 GridView s [ `AllowPaging`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx)到`true`)。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-151">To accomplish this simply check the Enable Paging checkbox from the GridView s smart tag (this sets the GridView s [`AllowPaging` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx) to `true`).</span></span>


<span data-ttu-id="7fb5c-152">[![选中启用分页复选框可添加分页支持](paging-and-sorting-report-data-vb/_static/image10.png)](paging-and-sorting-report-data-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-152">[![Check the Enable Paging Checkbox to Add Paging Support](paging-and-sorting-report-data-vb/_static/image10.png)](paging-and-sorting-report-data-vb/_static/image9.png)</span></span>

<span data-ttu-id="7fb5c-153">**图 7**： 检查启用分页所对应复选框添加分页支持 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image11.png))</span><span class="sxs-lookup"><span data-stu-id="7fb5c-153">**Figure 7**: Check the Enable Paging Checkbox to Add Paging Support ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image11.png))</span></span>


<span data-ttu-id="7fb5c-154">启用分页限制每页显示的记录数，并且将添加*分页接口*到 GridView。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-154">Enabling paging limits the number of records shown per page and adds a *paging interface* to the GridView.</span></span> <span data-ttu-id="7fb5c-155">图 7 所示的默认分页界面是页码，允许用户从一页数据快速导航到另一系列。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-155">The default paging interface, shown in Figure 7, is a series of page numbers, allowing the user to quickly navigate from one page of data to another.</span></span> <span data-ttu-id="7fb5c-156">此分页接口应看起来很熟悉，正如我们已在过去教程说明如何和 FormView 控件添加分页支持时看到它。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-156">This paging interface should look familiar, as we ve seen it when adding paging support to the DetailsView and FormView controls in past tutorials.</span></span>

<span data-ttu-id="7fb5c-157">说明和 FormView 控件只显示每页的单个记录。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-157">Both the DetailsView and FormView controls only show a single record per page.</span></span> <span data-ttu-id="7fb5c-158">GridView，但是，向其[`PageSize`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx)以确定每页显示的记录数量 （此属性默认值为 10）。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-158">The GridView, however, consults its [`PageSize` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx) to determine how many records to show per page (this property defaults to a value of 10).</span></span>

<span data-ttu-id="7fb5c-159">可以使用以下属性自定义此 GridView、 说明如何和 FormView 的分页接口：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-159">This GridView, DetailsView, and FormView s paging interface can be customized using the following properties:</span></span>

- <span data-ttu-id="7fb5c-160">`PagerStyle` 指示的分页接口; 的样式信息可以指定设置，例如`BackColor`， `ForeColor`， `CssClass`， `HorizontalAlign`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-160">`PagerStyle` indicates the style information for the paging interface; can specify settings like `BackColor`, `ForeColor`, `CssClass`, `HorizontalAlign`, and so on.</span></span>
- <span data-ttu-id="7fb5c-161">`PagerSettings` 包含可以自定义分页接口中; 的功能的属性 bevy`PageButtonCount`指示数值页码 （默认值为 10） 的分页界面中显示的最大数目; [ `Mode`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx)指示如何分页界面运行，并可以将设置为：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-161">`PagerSettings` contains a bevy of properties that can customize the functionality of the paging interface; `PageButtonCount` indicates the maximum number of numeric page numbers displayed in the paging interface (the default is 10); the [`Mode` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx) indicates how the paging interface operates and can be set to:</span></span> 

    - <span data-ttu-id="7fb5c-162">`NextPrevious` 显示允许用户在单步向前或向后一页时间下一步和上一步按钮</span><span class="sxs-lookup"><span data-stu-id="7fb5c-162">`NextPrevious` shows a Next and Previous buttons, allowing the user to step forwards or backwards one page at a time</span></span>
    - <span data-ttu-id="7fb5c-163">`NextPreviousFirstLast` 下一步和上一步按钮，除了第一个和最后一个按钮，还提供，允许用户以快速移动到第一个或最后一个数据页</span><span class="sxs-lookup"><span data-stu-id="7fb5c-163">`NextPreviousFirstLast` in addition to Next and Previous buttons, First and Last buttons are also included, allowing the user to quickly move to the first or last page of data</span></span>
    - <span data-ttu-id="7fb5c-164">`Numeric` 显示页码，使用户可立即跳转到任何页的系列</span><span class="sxs-lookup"><span data-stu-id="7fb5c-164">`Numeric` shows a series of page numbers, allowing the user to immediately jump to any page</span></span>
    - <span data-ttu-id="7fb5c-165">`NumericFirstLast` 除了页码，包括第一个和最后一个按钮，从而允许用户以快速移动到第一个或最后一页的数据;第一个/最后一个按钮才会显示是否所有数值的页码无法容纳</span><span class="sxs-lookup"><span data-stu-id="7fb5c-165">`NumericFirstLast` in addition to the page numbers, includes First and Last buttons, allowing the user to quickly move to the first or last page of data; the First/Last buttons are only shown if all of the numeric page numbers cannot fit</span></span>

<span data-ttu-id="7fb5c-166">此外，GridView、 说明如何和所有提供的 FormView`PageIndex`和`PageCount`属性，分别指示当前正在查看的页和数据，页的总数。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-166">Moreover, the GridView, DetailsView, and FormView all offer the `PageIndex` and `PageCount` properties, which indicate the current page being viewed and the total number of pages of data, respectively.</span></span> <span data-ttu-id="7fb5c-167">`PageIndex`属性编制了索引从 0，表示该参数时查看数据的第一页开始`PageIndex`将等于 0。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-167">The `PageIndex` property is indexed starting at 0, meaning that when viewing the first page of data `PageIndex` will equal 0.</span></span> <span data-ttu-id="7fb5c-168">`PageCount`另一方面，启动计数 1，这意味着，`PageIndex`限制为的值介于 0 和`PageCount - 1`。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-168">`PageCount`, on the other hand, starts counting at 1, meaning that `PageIndex` is limited to the values between 0 and `PageCount - 1`.</span></span>

<span data-ttu-id="7fb5c-169">允许花一些时间来提高我们 GridView 的分页接口的默认外观的 s。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-169">Let s take a moment to improve the default appearance of our GridView s paging interface.</span></span> <span data-ttu-id="7fb5c-170">具体来说，让 s 具有分页接口与浅灰色背景右对齐。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-170">Specifically, let s have the paging interface right-aligned with a light gray background.</span></span> <span data-ttu-id="7fb5c-171">而不是设置这些属性直接通过 GridView s`PagerStyle`属性，可让 s 创建中的 CSS 类`Styles.css`名为`PagerRowStyle`然后分配`PagerStyle`s`CssClass`通过我们的主题的属性。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-171">Rather than setting these properties directly through the GridView s `PagerStyle` property, let s create a CSS class in `Styles.css` named `PagerRowStyle` and then assign the `PagerStyle` s `CssClass` property through our Theme.</span></span> <span data-ttu-id="7fb5c-172">首先打开`Styles.css`并添加以下 CSS 类定义：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-172">Start by opening `Styles.css` and adding the following CSS class definition:</span></span>


[!code-css[Main](paging-and-sorting-report-data-vb/samples/sample3.css)]

<span data-ttu-id="7fb5c-173">接下来，打开`GridView.skin`文件中`DataWebControls`文件夹内的`App_Themes`文件夹。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-173">Next, open the `GridView.skin` file in the `DataWebControls` folder within the `App_Themes` folder.</span></span> <span data-ttu-id="7fb5c-174">如我们所述*母版页和网站的导航*教程，外观文件可以用于指定的 Web 控件的默认属性值。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-174">As we discussed in the *Master Pages and Site Navigation* tutorial, Skin files can be used to specify the default property values for a Web control.</span></span> <span data-ttu-id="7fb5c-175">因此，增加现有的设置，以包含设置`PagerStyle`s`CssClass`属性`PagerRowStyle`。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-175">Therefore, augment the existing settings to include setting the `PagerStyle` s `CssClass` property to `PagerRowStyle`.</span></span> <span data-ttu-id="7fb5c-176">此外，让 s 配置要显示最多五个数字寻呼按钮使用的分页界面`NumericFirstLast`分页接口。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-176">Also, let s configure the paging interface to show at most five numeric page buttons using the `NumericFirstLast` paging interface.</span></span>


[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample4.aspx)]

## <a name="the-paging-user-experience"></a><span data-ttu-id="7fb5c-177">分页用户体验</span><span class="sxs-lookup"><span data-stu-id="7fb5c-177">The Paging User Experience</span></span>

<span data-ttu-id="7fb5c-178">图 8 显示网页时在选中的 GridView s 启用分页复选框后，通过浏览器访问和`PagerStyle`和`PagerSettings`配置已通过`GridView.skin`文件。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-178">Figure 8 shows the web page when visited through a browser after the GridView s Enable Paging checkbox has been checked and the `PagerStyle` and `PagerSettings` configurations have been made through the `GridView.skin` file.</span></span> <span data-ttu-id="7fb5c-179">显示注意仅十个记录，并且分页接口指示我们正在查看数据的第一页。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-179">Note how only ten records are shown, and the paging interface indicates that we are viewing the first page of data.</span></span>


<span data-ttu-id="7fb5c-180">[![与分页启用，仅记录的子集显示一次](paging-and-sorting-report-data-vb/_static/image13.png)](paging-and-sorting-report-data-vb/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-180">[![With Paging Enabled, Only a Subset of the Records are Displayed at a Time](paging-and-sorting-report-data-vb/_static/image13.png)](paging-and-sorting-report-data-vb/_static/image12.png)</span></span>

<span data-ttu-id="7fb5c-181">**图 8**： 与分页已启用，仅记录的子集显示一次 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="7fb5c-181">**Figure 8**: With Paging Enabled, Only a Subset of the Records are Displayed at a Time ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image14.png))</span></span>


<span data-ttu-id="7fb5c-182">当用户单击分页接口中的页码之一上时，回发时，才会和页重新加载请求的页面的记录的显示。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-182">When the user clicks on one of the page numbers in the paging interface, a postback ensues and the page reloads showing that requested page s records.</span></span> <span data-ttu-id="7fb5c-183">选择要查看的数据的最后一页后，图 9 显示的结果。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-183">Figure 9 shows the results after opting to view the final page of data.</span></span> <span data-ttu-id="7fb5c-184">请注意最后一页上，仅有一条记录;这是因为，从而导致与唯一记录每个页面以及一页的 10 条记录的八个页总共有 81 记录。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-184">Notice that the final page only has one record; this is because there are 81 records in total, resulting in eight pages of 10 records per page plus one page with a lone record.</span></span>


<span data-ttu-id="7fb5c-185">[![单击页号导致回发，并演示记录的相应的子集](paging-and-sorting-report-data-vb/_static/image16.png)](paging-and-sorting-report-data-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-185">[![Clicking On a Page Number Causes a Postback and Shows the Appropriate Subset of Records](paging-and-sorting-report-data-vb/_static/image16.png)](paging-and-sorting-report-data-vb/_static/image15.png)</span></span>

<span data-ttu-id="7fb5c-186">**图 9**： 对页号单击导致回发并显示相应记录子集 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image17.png))</span><span class="sxs-lookup"><span data-stu-id="7fb5c-186">**Figure 9**: Clicking On a Page Number Causes a Postback and Shows the Appropriate Subset of Records ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image17.png))</span></span>


## <a name="paging-s-server-side-workflow"></a><span data-ttu-id="7fb5c-187">分页的服务器端工作流</span><span class="sxs-lookup"><span data-stu-id="7fb5c-187">Paging s Server-Side Workflow</span></span>

<span data-ttu-id="7fb5c-188">当最终用户单击分页接口中的按钮上时，回发时，才会和以下服务器端工作流一开始：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-188">When the end user clicks on a button in the paging interface, a postback ensues and the following server-side workflow begins:</span></span>

1. <span data-ttu-id="7fb5c-189">GridView s （或说明或 FormView）`PageIndexChanging`事件激发</span><span class="sxs-lookup"><span data-stu-id="7fb5c-189">The GridView s (or DetailsView or FormView) `PageIndexChanging` event fires</span></span>
2. <span data-ttu-id="7fb5c-190">ObjectDataSource 重新请求*所有*BLL; 中的数据的 GridView s`PageIndex`和`PageSize`属性值用于确定记录从 BLL 返回需要显示在 GridView</span><span class="sxs-lookup"><span data-stu-id="7fb5c-190">The ObjectDataSource re-requests *all* of the data from the BLL; the GridView s `PageIndex` and `PageSize` property values are used to determine what records returned from the BLL need to be displayed in the GridView</span></span>
3. <span data-ttu-id="7fb5c-191">GridView 的`PageIndexChanged`事件激发</span><span class="sxs-lookup"><span data-stu-id="7fb5c-191">The GridView s `PageIndexChanged` event fires</span></span>

<span data-ttu-id="7fb5c-192">在步骤 2 中，ObjectDataSource 重新请求所有来自其数据源的数据。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-192">In Step 2, the ObjectDataSource re-requests all of the data from its data source.</span></span> <span data-ttu-id="7fb5c-193">这种样式的分页通常称为*默认分页*，因为它分页行为，使用默认设置时`AllowPaging`属性`true`。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-193">This style of paging is commonly referred to as *default paging*, as it s the paging behavior used by default when setting the `AllowPaging` property to `true`.</span></span> <span data-ttu-id="7fb5c-194">使用默认 naively 分页 Web 控件的数据检索的数据，每一页的所有记录，即使仅记录的子集实际呈现到 HTML 发送到浏览器 s。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-194">With default paging the data Web control naively retrieves all records for each page of data, even though only a subset of records are actually rendered into the HTML that s sent to the browser.</span></span> <span data-ttu-id="7fb5c-195">数据库数据由 BLL 或 ObjectDataSource 缓存，则默认分页是不适用于为足够大的结果集或包含许多并发用户的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-195">Unless the database data is cached by the BLL or ObjectDataSource, default paging is unworkable for sufficiently large result sets or for web applications with many concurrent users.</span></span>

<span data-ttu-id="7fb5c-196">在下一教程中，我们将查看如何实现*自定义分页*。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-196">In the next tutorial we'll examine how to implement *custom paging*.</span></span> <span data-ttu-id="7fb5c-197">使用自定义分页专门可以指示 ObjectDataSource 以仅检索精确的所需的请求的数据页的记录集。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-197">With custom paging you can specifically instruct the ObjectDataSource to only retrieve the precise set of records needed for the requested page of data.</span></span> <span data-ttu-id="7fb5c-198">如你所想象的自定义分页大幅提高大型结果集进行分页的效率。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-198">As you can imagine, custom paging greatly improves the efficiency of paging through large result sets.</span></span>

> [!NOTE]
> <span data-ttu-id="7fb5c-199">默认分页，尽管不是适合时访问足够大的结果集或站点分页与许多并发用户发现自定义分页需要更多的更改和工作量才能实施，且不是像 （就是默认选中复选框一样简单分页）。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-199">While default paging is not suitable when paging through sufficiently large result sets or for sites with many simultaneous users, realize that custom paging requires more changes and effort to implement and is not as simple as checking a checkbox (as is default paging).</span></span> <span data-ttu-id="7fb5c-200">因此，默认分页可能会小、 低流量网站或相对较小的结果进行分页的设置时，作为它的理想选择 s 更轻松、 更加快速地实现。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-200">Therefore, default paging may be the ideal choice for small, low-traffic websites or when paging through relatively small result sets, as it s much easier and quicker to implement.</span></span>


<span data-ttu-id="7fb5c-201">例如，如果我们知道我们将在我们的数据库中永远不会有 100 个以上的产品，通过实现它所需的工作量可能偏移享受自定义分页的最小的性能提升。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-201">For example, if we know that we'll never have more than 100 products in our database, the minimal performance gain enjoyed by custom paging is likely offset by the effort required to implement it.</span></span> <span data-ttu-id="7fb5c-202">如果，但是，我们可能一天有数千或成千上万的产品，*不*实现自定义分页将极大地影响我们的应用程序的可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-202">If, however, we may one day have thousands or tens of thousands of products, *not* implementing custom paging would greatly hamper the scalability of our application.</span></span>

## <a name="step-4-customizing-the-paging-experience"></a><span data-ttu-id="7fb5c-203">步骤 4： 自定义分页体验</span><span class="sxs-lookup"><span data-stu-id="7fb5c-203">Step 4: Customizing the Paging Experience</span></span>

<span data-ttu-id="7fb5c-204">数据 Web 控件提供多个可用于增强用户的分页体验的属性。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-204">The data Web controls provide a number of properties that can be used to enhance the user s paging experience.</span></span> <span data-ttu-id="7fb5c-205">`PageCount`属性，例如，指示有多少总页数，虽然`PageIndex`属性指示要访问当前页，可以对其进行设置，以快速移动到特定页的用户。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-205">The `PageCount` property, for example, indicates how many total pages there are, while the `PageIndex` property indicates the current page being visited and can be set to quickly move a user to a specific page.</span></span> <span data-ttu-id="7fb5c-206">说明如何使用这些属性来改进了用户的分页体验，让我们来添加标签 Web 控制转移到我们向用户通知页面的页面它们重新当前访问，以及使他们能够快速跳转至任何给定页的 DropDownList 控件.</span><span class="sxs-lookup"><span data-stu-id="7fb5c-206">To illustrate how to use these properties to improve upon the user s paging experience, let s add a Label Web control to our page that informs the user what page they re currently visiting, along with a DropDownList control that allows them to quickly jump to any given page.</span></span>

<span data-ttu-id="7fb5c-207">首先，将标签 Web 控件添加到你的页面，设置其`ID`属性`PagingInformation`，并将清空其`Text`属性。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-207">First, add a Label Web control to your page, set its `ID` property to `PagingInformation`, and clear out its `Text` property.</span></span> <span data-ttu-id="7fb5c-208">接下来，创建的事件处理程序 GridView 的`DataBound`事件并添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-208">Next, create an event handler for the GridView s `DataBound` event and add the following code:</span></span>


[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample5.vb)]

<span data-ttu-id="7fb5c-209">此事件处理程序分配`PagingInformation`标签 s`Text`条消息，告知用户页当前访问属性`Products.PageIndex + 1`外多少总页数`Products.PageCount`(我们将添加到 1`Products.PageIndex`属性因为`PageIndex`编制了索引从 0 开始)。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-209">This event handler assigns the `PagingInformation` Label s `Text` property to a message informing the user the page they are currently visiting `Products.PageIndex + 1` out of how many total pages `Products.PageCount` (we add 1 to the `Products.PageIndex` property because `PageIndex` is indexed starting at 0).</span></span> <span data-ttu-id="7fb5c-210">分配选择此标签 s`Text`中的属性`DataBound`事件处理程序，而不是`PageIndexChanged`事件处理程序因为`DataBound`事件将激发每次数据绑定到 GridView，而对于`PageIndexChanged`事件处理程序更改页索引时激发。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-210">I chose the assign this Label s `Text` property in the `DataBound` event handler as opposed to the `PageIndexChanged` event handler because the `DataBound` event fires every time data is bound to the GridView whereas the `PageIndexChanged` event handler only fires when the page index is changed.</span></span> <span data-ttu-id="7fb5c-211">当 GridView 最初被数据绑定的第一页访问`PageIndexChanging`事件不 t 激发 (而`DataBound`事件)。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-211">When the GridView is initially data bound on the first page visit, the `PageIndexChanging` event doesn t fire (whereas the `DataBound` event does).</span></span>

<span data-ttu-id="7fb5c-212">添加此元素后，用户现在显示一条消息指出他们访问的页面，并且存在数据的多少总页数。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-212">With this addition, the user is now shown a message indicating what page they are visiting and how many total pages of data there are.</span></span>


<span data-ttu-id="7fb5c-213">[![显示的当前页码和总页数](paging-and-sorting-report-data-vb/_static/image19.png)](paging-and-sorting-report-data-vb/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-213">[![The Current Page Number and Total Number of Pages are Displayed](paging-and-sorting-report-data-vb/_static/image19.png)](paging-and-sorting-report-data-vb/_static/image18.png)</span></span>

<span data-ttu-id="7fb5c-214">**图 10**： 显示当前页码和总页数 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="7fb5c-214">**Figure 10**: The Current Page Number and Total Number of Pages are Displayed ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image20.png))</span></span>


<span data-ttu-id="7fb5c-215">除了标签控件，让我们来还添加 DropDownList 控件，其中列出与当前正在查看的页面选择了 GridView 中的页码。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-215">In addition to the Label control, let s also add a DropDownList control that lists the page numbers in the GridView with the currently viewed page selected.</span></span> <span data-ttu-id="7fb5c-216">其目的是，用户可以快速跳转从当前页到另一个只需从下拉列表中选择新的页索引。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-216">The idea here is that the user can quickly jump from the current page to another by simply selecting the new page index from the DropDownList.</span></span> <span data-ttu-id="7fb5c-217">通过将 DropDownList 添加到设计器中，设置启动其`ID`属性`PageList`并检查其智能标记的启用有些选项。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-217">Start by adding a DropDownList to the Designer, setting its `ID` property to `PageList` and checking the Enable AutoPostBack option from its smart tag.</span></span>

<span data-ttu-id="7fb5c-218">接下来，返回到`DataBound`事件处理程序并添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-218">Next, return to the `DataBound` event handler and add the following code:</span></span>


[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample6.vb)]

<span data-ttu-id="7fb5c-219">此代码先清除中的项`PageList`DropDownList。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-219">This code begins by clearing out the items in the `PageList` DropDownList.</span></span> <span data-ttu-id="7fb5c-220">这看起来似乎多余的因为一个对 t 预期的页数，若要更改，但其他用户可能同时使用系统、 添加或删除记录从`Products`表。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-220">This may seem superfluous, since one wouldn t expect the number of pages to change, but other users may be using the system simultaneously, adding or removing records from the `Products` table.</span></span> <span data-ttu-id="7fb5c-221">此类插入或删除无法更改的数据页数。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-221">Such insertions or deletions could alter the number of pages of data.</span></span>

<span data-ttu-id="7fb5c-222">接下来，我们需要再次创建页码，并且有一个映射到当前的 GridView`PageIndex`默认选择。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-222">Next, we need to create the page numbers again and have the one that maps to the current GridView `PageIndex` selected by default.</span></span> <span data-ttu-id="7fb5c-223">我们实现此目的从 0 到存在循环的`PageCount - 1`，添加一个新`ListItem`在每个迭代和设置其`Selected`属性设置为 true，如果当前迭代索引等于 GridView 的`PageIndex`属性。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-223">We accomplish this with a loop from 0 to `PageCount - 1`, adding a new `ListItem` in each iteration and setting its `Selected` property to true if the current iteration index equals the GridView s `PageIndex` property.</span></span>

<span data-ttu-id="7fb5c-224">最后，我们需要创建的事件处理程序的 DropDownList s`SelectedIndexChanged`触发的每当用户选择不同的项从列表中的事件。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-224">Finally, we need to create an event handler for the DropDownList s `SelectedIndexChanged` event, which fires each time the user pick a different item from the list.</span></span> <span data-ttu-id="7fb5c-225">若要创建此事件处理程序，只需双击设计器中，在下拉列表，然后添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-225">To create this event handler, simply double-click the DropDownList in the Designer, then add the following code:</span></span>


[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample7.vb)]

<span data-ttu-id="7fb5c-226">如图 11 所示，只更改 GridView 的`PageIndex`属性将导致数据重新绑定到 GridView。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-226">As Figure 11 shows, merely changing the GridView s `PageIndex` property causes the data to be rebound to the GridView.</span></span> <span data-ttu-id="7fb5c-227">在 GridView`DataBound`事件处理程序，相应的 DropDownList`ListItem`选择。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-227">In the GridView s `DataBound` event handler, the appropriate DropDownList `ListItem` is selected.</span></span>


<span data-ttu-id="7fb5c-228">[![用户将自动转到第六个页时选择页 6 下拉列表项](paging-and-sorting-report-data-vb/_static/image22.png)](paging-and-sorting-report-data-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-228">[![The User is Automatically Taken to the Sixth Page When Selecting the Page 6 Drop-Down List Item](paging-and-sorting-report-data-vb/_static/image22.png)](paging-and-sorting-report-data-vb/_static/image21.png)</span></span>

<span data-ttu-id="7fb5c-229">**图 11**： 的用户将自动转到第六个页时选择页 6 下拉列表项 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image23.png))</span><span class="sxs-lookup"><span data-stu-id="7fb5c-229">**Figure 11**: The User is Automatically Taken to the Sixth Page When Selecting the Page 6 Drop-Down List Item ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image23.png))</span></span>


## <a name="step-5-adding-bi-directional-sorting-support"></a><span data-ttu-id="7fb5c-230">步骤 5： 添加双向语言排序支持</span><span class="sxs-lookup"><span data-stu-id="7fb5c-230">Step 5: Adding Bi-Directional Sorting Support</span></span>

<span data-ttu-id="7fb5c-231">添加双向语言排序支持非常简单，只添加分页支持只需选中 GridView s 智能标记的启用排序选项 (这会设置 GridView s [ `AllowSorting`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx)到`true`)。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-231">Adding bi-directional sorting support is as simple as adding paging support simply check the Enable Sorting option from the GridView s smart tag (which sets the GridView s [`AllowSorting` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx) to `true`).</span></span> <span data-ttu-id="7fb5c-232">此呈现每个标头的 GridView 的字段作为 LinkButtons，单击时，导致回发，并返回按所单击的列以升序排序的数据。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-232">This renders each of the headers of the GridView s fields as LinkButtons that, when clicked, cause a postback and return the data sorted by the clicked column in ascending order.</span></span> <span data-ttu-id="7fb5c-233">再次单击同一标题 LinkButton 重新对数据进行排序以降序顺序。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-233">Clicking the same header LinkButton again re-sorts the data in descending order.</span></span>

> [!NOTE]
> <span data-ttu-id="7fb5c-234">如果你使用自定义的数据访问层，而不是类型化数据集，你可能没有启用排序选项 GridView s 智能标记中。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-234">If you are using a custom Data Access Layer rather than a Typed DataSet, you may not have an Enable Sorting option in the GridView s smart tag.</span></span> <span data-ttu-id="7fb5c-235">仅 GridViews 绑定到数据源以本机方式支持排序具有可用此复选框。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-235">Only GridViews bound to data sources that natively support sorting have this checkbox available.</span></span> <span data-ttu-id="7fb5c-236">类型化数据集提供现成可用排序支持由于 ADO.NET DataTable 提供`Sort`方法，调用时，对 DataTable s 使用指定的条件的数据行进行排序。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-236">The Typed DataSet provides out-of-the-box sorting support since the ADO.NET DataTable provides a `Sort` method that, when invoked, sorts the DataTable s DataRows using the criteria specified.</span></span>


<span data-ttu-id="7fb5c-237">如果你 DAL 不返回由 DAL 的本机支持排序将需要配置对象数据源将排序的信息传递给业务逻辑层，以对数据进行排序或具有的数据排序的对象。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-237">If your DAL does not return objects that natively support sorting you will need to configure the ObjectDataSource to pass sorting information to the Business Logic Layer, which can either sort the data or have the data sorted by the DAL.</span></span> <span data-ttu-id="7fb5c-238">我们将探讨如何进行排序在将来的教程中的数据在业务逻辑和数据访问层。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-238">We'll explore how to sort data at the Business Logic and Data Access Layers in a future tutorial.</span></span>

<span data-ttu-id="7fb5c-239">排序 LinkButtons 呈现为 HTML 超链接，其当前的颜色 （蓝色未访问的链接并访问过的链接深红色表示） 与标头行的背景色冲突。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-239">The sorting LinkButtons are rendered as HTML hyperlinks, whose current colors (blue for an unvisited link and a dark red for a visited link) clash with the background color of the header row.</span></span> <span data-ttu-id="7fb5c-240">相反，让 s 必须中显示为空白，而不管是否的所有标头行链接它们已被访问或不。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-240">Instead, let s have all header row links displayed in white, regardless of whether they ve been visited or not.</span></span> <span data-ttu-id="7fb5c-241">这可以通过添加以下实现`Styles.css`类：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-241">This can be accomplished by adding the following to the `Styles.css` class:</span></span>


[!code-css[Main](paging-and-sorting-report-data-vb/samples/sample8.css)]

<span data-ttu-id="7fb5c-242">此语法指示要显示这些元素使用的 HeaderStyle 类中的超链接时使用白色文本。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-242">This syntax indicates to use white text when displaying those hyperlinks within an element that uses the HeaderStyle class.</span></span>

<span data-ttu-id="7fb5c-243">此 CSS 添加后, 访问通过浏览器的页面屏幕看起来应类似于图 12。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-243">After this CSS addition, when visiting the page through a browser your screen should look similar to Figure 12.</span></span> <span data-ttu-id="7fb5c-244">具体而言，图 12 显示的结果后单击价格字段 s 标头链接。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-244">In particular, Figure 12 shows the results after the Price field s header link has been clicked.</span></span>


<span data-ttu-id="7fb5c-245">[![具有已按升序排序单价排序结果](paging-and-sorting-report-data-vb/_static/image25.png)](paging-and-sorting-report-data-vb/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-245">[![The Results Have Been Sorted by the UnitPrice in Ascending Order](paging-and-sorting-report-data-vb/_static/image25.png)](paging-and-sorting-report-data-vb/_static/image24.png)</span></span>

<span data-ttu-id="7fb5c-246">**图 12**: 结果排过序升序顺序 UnitPrice ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="7fb5c-246">**Figure 12**: The Results Have Been Sorted by the UnitPrice in Ascending Order ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image26.png))</span></span>


## <a name="examining-the-sorting-workflow"></a><span data-ttu-id="7fb5c-247">检查排序工作流</span><span class="sxs-lookup"><span data-stu-id="7fb5c-247">Examining the Sorting Workflow</span></span>

<span data-ttu-id="7fb5c-248">所有 GridView 都字段 BoundField、 CheckBoxField、 TemplateField，和等等具有`SortExpression`属性，指示应使用对数据进行排序时单击该字段 s 排序标头链接的表达式。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-248">All GridView fields the BoundField, CheckBoxField, TemplateField, and so on have a `SortExpression` property that indicates the expression that should be used to sort the data when that field s sorting header link is clicked.</span></span> <span data-ttu-id="7fb5c-249">GridView 还有`SortExpression`属性。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-249">The GridView also has a `SortExpression` property.</span></span> <span data-ttu-id="7fb5c-250">GridView 时单击 LinkButton 排序标头，指定该字段 s`SortExpression`值赋给其`SortExpression`属性。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-250">When a sorting header LinkButton is clicked, the GridView assigns that field s `SortExpression` value to its `SortExpression` property.</span></span> <span data-ttu-id="7fb5c-251">接下来，并将数据从 ObjectDataSource 重新检索根据 GridView s 排序`SortExpression`属性。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-251">Next, the data is re-retrieved from the ObjectDataSource and sorted according to the GridView s `SortExpression` property.</span></span> <span data-ttu-id="7fb5c-252">下表详细描述调查时最终用户对数据进行 GridView 的步骤顺序：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-252">The following list details the sequence of steps that transpires when an end user sorts the data in a GridView:</span></span>

1. <span data-ttu-id="7fb5c-253">GridView s [Sorting 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx)激发</span><span class="sxs-lookup"><span data-stu-id="7fb5c-253">The GridView s [Sorting event](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx) fires</span></span>
2. <span data-ttu-id="7fb5c-254">GridView s [ `SortExpression`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx)设置为`SortExpression`的字段 LinkButton 被单击其排序标头</span><span class="sxs-lookup"><span data-stu-id="7fb5c-254">The GridView s [`SortExpression` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) is set to the `SortExpression` of the field whose sorting header LinkButton was clicked</span></span>
3. <span data-ttu-id="7fb5c-255">ObjectDataSource 重新检索所有 BLL 中的数据，然后对使用 GridView s 的数据进行排序 `SortExpression`</span><span class="sxs-lookup"><span data-stu-id="7fb5c-255">The ObjectDataSource re-retrieves all of the data from the BLL and then sorts the data using the GridView s `SortExpression`</span></span>
4. <span data-ttu-id="7fb5c-256">GridView 的`PageIndex`属性重置为 0，这意味着，排序用户时返回到 （假设已实现分页支持） 的数据的第一页</span><span class="sxs-lookup"><span data-stu-id="7fb5c-256">The GridView s `PageIndex` property is reset to 0, meaning that when sorting the user is returned to the first page of data (assuming paging support has been implemented)</span></span>
5. <span data-ttu-id="7fb5c-257">GridView s [ `Sorted`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx)激发</span><span class="sxs-lookup"><span data-stu-id="7fb5c-257">The GridView s [`Sorted` event](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx) fires</span></span>

<span data-ttu-id="7fb5c-258">像默认分页，请使用默认排序选项重新检索*所有*从 BLL 的记录。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-258">Like with default paging, the default sorting option re-retrieves *all* of the records from the BLL.</span></span> <span data-ttu-id="7fb5c-259">使用不分页的情况下排序时，或者使用使用进行排序时默认分页，那里 s 没有办法避开此性能下降 （缺少缓存的数据库数据）。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-259">When using sorting without paging or when using sorting with default paging, there s no way to circumvent this performance hit (short of caching the database data).</span></span> <span data-ttu-id="7fb5c-260">但是，正如在将来的教程，我们看到它可以有效地对数据进行排序时使用自定义分页的 s。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-260">However, as we'll see in a future tutorial, it s possible to efficiently sort data when using custom paging.</span></span>

<span data-ttu-id="7fb5c-261">当对象数据源绑定到 GridView 通过 GridView s 智能标记中的下拉列表时，每个 GridView 字段会自动拥有其`SortExpression`属性分配给中的数据字段的名称`ProductsRow`类。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-261">When binding an ObjectDataSource to the GridView through the drop-down list in the GridView s smart tag, each GridView field automatically has its `SortExpression` property assigned to the name of the data field in the `ProductsRow` class.</span></span> <span data-ttu-id="7fb5c-262">例如， `ProductName` BoundField s`SortExpression`设置为`ProductName`，以下声明标记中所示：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-262">For example, the `ProductName` BoundField s `SortExpression` is set to `ProductName`, as shown in the following declarative markup:</span></span>


[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample9.aspx)]

<span data-ttu-id="7fb5c-263">可以配置一个字段，以便它可通过清除不排序 s 其`SortExpression`（将其分配为空字符串） 的属性。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-263">A field can be configured so that it s not sortable by clearing out its `SortExpression` property (assigning it to an empty string).</span></span> <span data-ttu-id="7fb5c-264">为了说明这一点，我们假设，我们没有 t 想要让我们按价格排序我们的产品的客户。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-264">To illustrate this, imagine that we didn t want to let our customers sort our products by price.</span></span> <span data-ttu-id="7fb5c-265">`UnitPrice` BoundField 的`SortExpression`通过声明性的标记或通过字段对话框 （这是通过单击 GridView s 智能标记中的编辑列链接的访问） 可以删除此属性。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-265">The `UnitPrice` BoundField s `SortExpression` property can be removed either from the declarative markup or through the Fields dialog box (which is accessible by clicking on the Edit Columns link in the GridView s smart tag).</span></span>


![具有已按升序排序单价排序结果](paging-and-sorting-report-data-vb/_static/image27.png)

<span data-ttu-id="7fb5c-267">**图 13**： 结果已按升序排序单价进行了排序</span><span class="sxs-lookup"><span data-stu-id="7fb5c-267">**Figure 13**: The Results Have Been Sorted by the UnitPrice in Ascending Order</span></span>


<span data-ttu-id="7fb5c-268">一次`SortExpression`属性已被撤除`UnitPrice`BoundField 页眉呈现为文本而不是一个链接，从而阻止用户对数据进行排序的价格。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-268">Once the `SortExpression` property has been removed for the `UnitPrice` BoundField, the header is rendered as text rather than as a link, thereby preventing users from sorting the data by price.</span></span>


<span data-ttu-id="7fb5c-269">[![通过删除 SortExpression 属性，用户可以不再对价格按产品](paging-and-sorting-report-data-vb/_static/image29.png)](paging-and-sorting-report-data-vb/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-269">[![By Removing the SortExpression Property, Users Can No Longer Sort the Products By Price](paging-and-sorting-report-data-vb/_static/image29.png)](paging-and-sorting-report-data-vb/_static/image28.png)</span></span>

<span data-ttu-id="7fb5c-270">**图 14**： 通过删除 SortExpression 属性，用户可以不再对产品的价格 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image30.png))</span><span class="sxs-lookup"><span data-stu-id="7fb5c-270">**Figure 14**: By Removing the SortExpression Property, Users Can No Longer Sort the Products By Price ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image30.png))</span></span>


## <a name="programmatically-sorting-the-gridview"></a><span data-ttu-id="7fb5c-271">以编程方式排序 GridView</span><span class="sxs-lookup"><span data-stu-id="7fb5c-271">Programmatically Sorting the GridView</span></span>

<span data-ttu-id="7fb5c-272">你也可以进行排序的 GridView 内容以编程方式使用 GridView s [ `Sort`方法](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-272">You can also sort the contents of the GridView programmatically by using the GridView s [`Sort` method](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx).</span></span> <span data-ttu-id="7fb5c-273">只需传入`SortExpression`值作为排序依据以及[ `SortDirection` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) (`Ascending`或`Descending`)，并且 GridView 的数据将会重新排序。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-273">Simply pass in the `SortExpression` value to sort by along with the [`SortDirection`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) (`Ascending` or `Descending`), and the GridView s data will be re-sorted.</span></span>

<span data-ttu-id="7fb5c-274">假设，原因我们关闭排序`UnitPrice`是的因为我们只需担心我们的客户只需将购买仅价格最低的产品。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-274">Imagine that the reason we turned off sorting by the `UnitPrice` was because we were worried that our customers would simply buy only the lowest-priced products.</span></span> <span data-ttu-id="7fb5c-275">但是，我们想要鼓励他们购买的成本最高的产品，因此我们 d 诸如它们才能进行排序的价格，但只能从最高价到最少的产品。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-275">However, we want to encourage them to buy the most expensive products, so we d like them to be able to sort the products by price, but only from the most expensive price to the least.</span></span>

<span data-ttu-id="7fb5c-276">若要完成这将 Button Web 控件添加到页中，设置其`ID`属性`SortPriceDescending`，并将其`Text`价格按排序的属性。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-276">To accomplish this add a Button Web control to the page, set its `ID` property to `SortPriceDescending`, and its `Text` property to Sort by Price.</span></span> <span data-ttu-id="7fb5c-277">接下来，为 s 按钮创建一个事件处理程序`Click`通过双击该按钮控件设计器中的事件。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-277">Next, create an event handler for the Button s `Click` event by double-clicking the Button control in the Designer.</span></span> <span data-ttu-id="7fb5c-278">将以下代码添加到此事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-278">Add the following code to this event handler:</span></span>


[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample10.vb)]

<span data-ttu-id="7fb5c-279">单击此按钮使用户返回到的第一页与按定价从成本最高到最便宜 （请参阅图 15） 产品。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-279">Clicking this Button returns the user to the first page with the products sorted by price, from most expensive to least expensive (see Figure 15).</span></span>


<span data-ttu-id="7fb5c-280">[![单击按钮订单中成本最高的产品到最少](paging-and-sorting-report-data-vb/_static/image32.png)](paging-and-sorting-report-data-vb/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-280">[![Clicking the Button Orders the Products From the Most Expensive to the Least](paging-and-sorting-report-data-vb/_static/image32.png)](paging-and-sorting-report-data-vb/_static/image31.png)</span></span>

<span data-ttu-id="7fb5c-281">**图 15**： 单击按钮订单产品从成本最高到最少 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-vb/_static/image33.png))</span><span class="sxs-lookup"><span data-stu-id="7fb5c-281">**Figure 15**: Clicking the Button Orders the Products From the Most Expensive to the Least ([Click to view full-size image](paging-and-sorting-report-data-vb/_static/image33.png))</span></span>


## <a name="summary"></a><span data-ttu-id="7fb5c-282">总结</span><span class="sxs-lookup"><span data-stu-id="7fb5c-282">Summary</span></span>

<span data-ttu-id="7fb5c-283">在本教程中我们已了解如何实现分页和排序功能的默认值，这两种都是简单地检查一个复选框的 ！</span><span class="sxs-lookup"><span data-stu-id="7fb5c-283">In this tutorial we saw how to implement default paging and sorting capabilities, both of which were as easy as checking a checkbox!</span></span> <span data-ttu-id="7fb5c-284">当用户对进行排序或数据进行分页时，则展开类似的工作流：</span><span class="sxs-lookup"><span data-stu-id="7fb5c-284">When a user sorts or pages through data, a similar workflow unfolds:</span></span>

1. <span data-ttu-id="7fb5c-285">回发时，才会</span><span class="sxs-lookup"><span data-stu-id="7fb5c-285">A postback ensues</span></span>
2. <span data-ttu-id="7fb5c-286">Web 控件 s 的数据预先级别事件将触发 (`PageIndexChanging`或`Sorting`)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-286">The data Web control s pre-level event fires (`PageIndexChanging` or `Sorting`)</span></span>
3. <span data-ttu-id="7fb5c-287">所有数据将重新检索的对象数据源</span><span class="sxs-lookup"><span data-stu-id="7fb5c-287">All of the data is re-retrieved by the ObjectDataSource</span></span>
4. <span data-ttu-id="7fb5c-288">Web 控件 s 的数据后级别事件将触发 (`PageIndexChanged`或`Sorted`)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-288">The data Web control s post-level event fires (`PageIndexChanged` or `Sorted`)</span></span>

<span data-ttu-id="7fb5c-289">尽管实现基本的分页和排序是轻松，以利用更高效的自定义分页或来进一步增强分页或排序接口必须造成更多的工作。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-289">While implementing basic paging and sorting is a breeze, more effort must be exerted to utilize the more efficient custom paging or to further enhance the paging or sorting interface.</span></span> <span data-ttu-id="7fb5c-290">将来的教程将探索这些主题。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-290">Future tutorials will explore these topics.</span></span>

<span data-ttu-id="7fb5c-291">尽情享受编程 ！</span><span class="sxs-lookup"><span data-stu-id="7fb5c-291">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="7fb5c-292">关于作者</span><span class="sxs-lookup"><span data-stu-id="7fb5c-292">About the Author</span></span>

<span data-ttu-id="7fb5c-293">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的七个 ASP/ASP.NET 书籍和的创始人[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年使用与 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-293">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="7fb5c-294">Scott 的作用是作为独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-294">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="7fb5c-295">最新书籍是[ *Sam 教授自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-295">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="7fb5c-296">他可以达到在[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)或通过他的博客，其中可以找到在[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-296">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7fb5c-297">[上一页](creating-a-customized-sorting-user-interface-cs.md)
> [下一页](efficiently-paging-through-large-amounts-of-data-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-297">[Previous](creating-a-customized-sorting-user-interface-cs.md)
[Next](efficiently-paging-through-large-amounts-of-data-vb.md)</span></span>
