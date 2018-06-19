---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
title: 在 GridView 的页脚 (C#) 中显示的摘要信息 |Microsoft 文档
author: rick-anderson
description: 摘要信息通常显示在摘要行中的报表的底部。 GridView 控件可以包含为其单元中，我们可以 pr 的页脚行...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: d50edc31-9286-4c6a-8635-be09e72752a4
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bb00a41bee86090f71d6315d73037cd41b2c621
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30877419"
---
<a name="displaying-summary-information-in-the-gridviews-footer-c"></a><span data-ttu-id="14939-104">在 GridView 的页脚 (C#) 中显示的摘要信息</span><span class="sxs-lookup"><span data-stu-id="14939-104">Displaying Summary Information in the GridView's Footer (C#)</span></span>
====================
<span data-ttu-id="14939-105">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="14939-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="14939-106">[下载示例应用程序](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_15_CS.exe)或[下载 PDF](displaying-summary-information-in-the-gridview-s-footer-cs/_static/datatutorial15cs1.pdf)</span><span class="sxs-lookup"><span data-stu-id="14939-106">[Download Sample App](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_15_CS.exe) or [Download PDF](displaying-summary-information-in-the-gridview-s-footer-cs/_static/datatutorial15cs1.pdf)</span></span>

> <span data-ttu-id="14939-107">摘要信息通常显示在摘要行中的报表的底部。</span><span class="sxs-lookup"><span data-stu-id="14939-107">Summary information is often displayed at the bottom of the report in a summary row.</span></span> <span data-ttu-id="14939-108">GridView 控件可以包含为其单元格我们可以以编程方式插入聚合数据的页脚行。</span><span class="sxs-lookup"><span data-stu-id="14939-108">The GridView control can include a footer row into whose cells we can programmatically inject aggregate data.</span></span> <span data-ttu-id="14939-109">在本教程中我们将了解如何在页脚此行中显示聚合数据。</span><span class="sxs-lookup"><span data-stu-id="14939-109">In this tutorial we'll see how to display aggregate data in this footer row.</span></span>


## <a name="introduction"></a><span data-ttu-id="14939-110">介绍</span><span class="sxs-lookup"><span data-stu-id="14939-110">Introduction</span></span>

<span data-ttu-id="14939-111">除了上顺序和重新排序级别中看到每个产品的价格、 库存量，单位，用户可能还会对感兴趣聚合的信息，例如平均价格，库存，量的总数，依此类推。</span><span class="sxs-lookup"><span data-stu-id="14939-111">In addition to seeing each of the products' prices, units in stock, units on order, and reorder levels, a user might also be interested in aggregate information, such as the average price, the total number of units in stock, and so on.</span></span> <span data-ttu-id="14939-112">此类的摘要信息通常显示在摘要行中的报表的底部。</span><span class="sxs-lookup"><span data-stu-id="14939-112">Such summary information is often displayed at the bottom of the report in a summary row.</span></span> <span data-ttu-id="14939-113">GridView 控件可以包含为其单元格我们可以以编程方式插入聚合数据的页脚行。</span><span class="sxs-lookup"><span data-stu-id="14939-113">The GridView control can include a footer row into whose cells we can programmatically inject aggregate data.</span></span>

<span data-ttu-id="14939-114">此任务将向我们提供三个难题：</span><span class="sxs-lookup"><span data-stu-id="14939-114">This task presents us with three challenges:</span></span>

1. <span data-ttu-id="14939-115">配置 GridView 若要显示其页脚行</span><span class="sxs-lookup"><span data-stu-id="14939-115">Configuring the GridView to display its footer row</span></span>
2. <span data-ttu-id="14939-116">确定摘要数据;即如何我们计算平均价格或库存量的单元总数？</span><span class="sxs-lookup"><span data-stu-id="14939-116">Determining the summary data; that is, how do we compute the average price or the total of the units in stock?</span></span>
3. <span data-ttu-id="14939-117">将摘要数据注入到相应的单元格中的页脚行</span><span class="sxs-lookup"><span data-stu-id="14939-117">Injecting the summary data into the appropriate cells of the footer row</span></span>

<span data-ttu-id="14939-118">在本教程中我们将了解如何克服这些难题。</span><span class="sxs-lookup"><span data-stu-id="14939-118">In this tutorial we'll see how to overcome these challenges.</span></span> <span data-ttu-id="14939-119">具体而言，我们将创建的页面与一个 GridView 中显示的所选的类别的产品列出下拉列表中的类别。</span><span class="sxs-lookup"><span data-stu-id="14939-119">Specifically, we'll create a page that lists the categories in a drop-down list with the selected category's products displayed in a GridView.</span></span> <span data-ttu-id="14939-120">GridView 将包括显示了平均价格和总单位数，库存量和在该类别中的产品的订单的页脚行。</span><span class="sxs-lookup"><span data-stu-id="14939-120">The GridView will include a footer row that shows the average price and total number of units in stock and on order for products in that category.</span></span>


<span data-ttu-id="14939-121">[![摘要信息显示在 GridView 的页脚行中](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="14939-121">[![Summary Information is Displayed in the GridView's Footer Row](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image1.png)</span></span>

<span data-ttu-id="14939-122">**图 1**： 摘要信息显示在 GridView 的页脚行中 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="14939-122">**Figure 1**: Summary Information is Displayed in the GridView's Footer Row ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image3.png))</span></span>


<span data-ttu-id="14939-123">本教程中的，产品主/从接口，其类别均基于在早期版本中介绍的概念[主/详细信息筛选与 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)教程。</span><span class="sxs-lookup"><span data-stu-id="14939-123">This tutorial, with its category to products master/detail interface, builds upon the concepts covered in the earlier [Master/Detail Filtering With a DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) tutorial.</span></span> <span data-ttu-id="14939-124">如果你尚未过完成前面的教程，请这样做之前上继续进行此。</span><span class="sxs-lookup"><span data-stu-id="14939-124">If you've not yet worked through the earlier tutorial, please do so before continuing on with this one.</span></span>

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a><span data-ttu-id="14939-125">步骤 1： 添加的类别的 DropDownList 和产品 GridView</span><span class="sxs-lookup"><span data-stu-id="14939-125">Step 1: Adding the Categories DropDownList and Products GridView</span></span>

<span data-ttu-id="14939-126">在以前有关自行处理将摘要信息添加到 GridView 的页脚，让我们首先只需生成主/详细信息报表。</span><span class="sxs-lookup"><span data-stu-id="14939-126">Before concerning ourselves with adding summary information to the GridView's footer, let's first simply build the master/detail report.</span></span> <span data-ttu-id="14939-127">我们已完成此第一步，我们将查看如何包含摘要数据。</span><span class="sxs-lookup"><span data-stu-id="14939-127">Once we've completed this first step, we'll look at how to include summary data.</span></span>

<span data-ttu-id="14939-128">首先打开`SummaryDataInFooter.aspx`页面`CustomFormatting`文件夹。</span><span class="sxs-lookup"><span data-stu-id="14939-128">Start by opening the `SummaryDataInFooter.aspx` page in the `CustomFormatting` folder.</span></span> <span data-ttu-id="14939-129">添加的 DropDownList 控件并设置其`ID`到`Categories`。</span><span class="sxs-lookup"><span data-stu-id="14939-129">Add a DropDownList control and set its `ID` to `Categories`.</span></span> <span data-ttu-id="14939-130">接下来，单击从下拉列表的智能标记的选择数据源链接，然后选择要添加名为新 ObjectDataSource `CategoriesDataSource` ，它调用`CategoriesBLL`类的`GetCategories()`方法。</span><span class="sxs-lookup"><span data-stu-id="14939-130">Next, click on the Choose Data Source link from the DropDownList's smart tag and opt to add a new ObjectDataSource named `CategoriesDataSource` that invokes the `CategoriesBLL` class's `GetCategories()` method.</span></span>


<span data-ttu-id="14939-131">[![添加名为 CategoriesDataSource 新对象数据源](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="14939-131">[![Add a New ObjectDataSource Named CategoriesDataSource](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image4.png)</span></span>

<span data-ttu-id="14939-132">**图 2**： 添加新对象数据源名为`CategoriesDataSource`([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="14939-132">**Figure 2**: Add a New ObjectDataSource Named `CategoriesDataSource` ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image6.png))</span></span>


<span data-ttu-id="14939-133">[![已调用 CategoriesBLL 类 GetCategories() 方法 ObjectDataSource](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="14939-133">[![Have the ObjectDataSource Invoke the CategoriesBLL Class's GetCategories() Method](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image7.png)</span></span>

<span data-ttu-id="14939-134">**图 3**： 具有 ObjectDataSource 调用`CategoriesBLL`类的`GetCategories()`方法 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="14939-134">**Figure 3**: Have the ObjectDataSource Invoke the `CategoriesBLL` Class's `GetCategories()` Method ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image9.png))</span></span>


<span data-ttu-id="14939-135">配置对象数据源之后, 该向导将返回我们应显示的向导我们需要指定哪些数据字段值的下拉列表的数据源配置和哪一个应对应于的下拉列表的值`ListItem` s。</span><span class="sxs-lookup"><span data-stu-id="14939-135">After configuring the ObjectDataSource, the wizard returns us to the DropDownList's Data Source Configuration wizard from which we need to specify what data field value should be displayed and which one should correspond to the value of the DropDownList's `ListItem` s.</span></span> <span data-ttu-id="14939-136">具有`CategoryName`显示的字段并使用`CategoryID`作为值。</span><span class="sxs-lookup"><span data-stu-id="14939-136">Have the `CategoryName` field displayed and use the `CategoryID` as the value.</span></span>


<span data-ttu-id="14939-137">[![作为文本和值 ListItems，分别使用类别名称和类别 id 字段](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="14939-137">[![Use the CategoryName and CategoryID Fields as the Text and Value for the ListItems, Respectively](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image10.png)</span></span>

<span data-ttu-id="14939-138">**图 4**： 使用`CategoryName`和`CategoryID`字段为`Text`和`Value`为`ListItem`s，分别 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="14939-138">**Figure 4**: Use the `CategoryName` and `CategoryID` Fields as the `Text` and `Value` for the `ListItem` s, Respectively ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image12.png))</span></span>


<span data-ttu-id="14939-139">我们现在有 DropDownList (`Categories`)，它列出系统中的类别。</span><span class="sxs-lookup"><span data-stu-id="14939-139">At this point we have a DropDownList (`Categories`) that lists the categories in the system.</span></span> <span data-ttu-id="14939-140">现在，我们需要添加一个 GridView，列出属于所选类别这些产品。</span><span class="sxs-lookup"><span data-stu-id="14939-140">We now need to add a GridView that lists those products that belong to the selected category.</span></span> <span data-ttu-id="14939-141">我们执行，但是之前, 需要一段时间来检查 DropDownList 的智能标记中的启用有些复选框。</span><span class="sxs-lookup"><span data-stu-id="14939-141">Before we do, though, take a moment to check the Enable AutoPostBack checkbox in the DropDownList's smart tag.</span></span> <span data-ttu-id="14939-142">中所述*主/详细信息筛选与 DropDownList*教程，通过设置的 DropDownList`AutoPostBack`属性`true`将回发每次更改时的 DropDownList 值页。</span><span class="sxs-lookup"><span data-stu-id="14939-142">As discussed in the *Master/Detail Filtering With a DropDownList* tutorial, by setting the DropDownList's `AutoPostBack` property to `true` the page will be posted back each time the DropDownList value is changed.</span></span> <span data-ttu-id="14939-143">这将导致 GridView 进行刷新，显示为新选择的类别这些产品。</span><span class="sxs-lookup"><span data-stu-id="14939-143">This will cause the GridView to be refreshed, showing those products for the newly selected category.</span></span> <span data-ttu-id="14939-144">如果`AutoPostBack`属性设置为`false`（默认值）、 更改类别不会导致回发并因此不会更新列出的产品。</span><span class="sxs-lookup"><span data-stu-id="14939-144">If the `AutoPostBack` property is set to `false` (the default), changing the category won't cause a postback and therefore won't update the listed products.</span></span>


<span data-ttu-id="14939-145">[![检查 DropDownList 的智能标记中的启用有些复选框](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="14939-145">[![Check the Enable AutoPostBack Checkbox in the DropDownList's Smart Tag](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image13.png)</span></span>

<span data-ttu-id="14939-146">**图 5**： 检查启用有些中的复选框的 DropDownList 智能标记 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="14939-146">**Figure 5**: Check the Enable AutoPostBack Checkbox in the DropDownList's Smart Tag ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image15.png))</span></span>


<span data-ttu-id="14939-147">将 GridView 控件添加到页面中，为了显示所选类别的产品。</span><span class="sxs-lookup"><span data-stu-id="14939-147">Add a GridView control to the page in order to display the products for the selected category.</span></span> <span data-ttu-id="14939-148">设置 GridView`ID`到`ProductsInCategory`并将其绑定到名为新 ObjectDataSource `ProductsInCategoryDataSource`。</span><span class="sxs-lookup"><span data-stu-id="14939-148">Set the GridView's `ID` to `ProductsInCategory` and bind it to a new ObjectDataSource named `ProductsInCategoryDataSource`.</span></span>


<span data-ttu-id="14939-149">[![添加名为 ProductsInCategoryDataSource 新对象数据源](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="14939-149">[![Add a New ObjectDataSource Named ProductsInCategoryDataSource](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image16.png)</span></span>

<span data-ttu-id="14939-150">**图 6**： 添加新对象数据源名为`ProductsInCategoryDataSource`([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="14939-150">**Figure 6**: Add a New ObjectDataSource Named `ProductsInCategoryDataSource` ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image18.png))</span></span>


<span data-ttu-id="14939-151">配置对象数据源，以便它将调用`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。</span><span class="sxs-lookup"><span data-stu-id="14939-151">Configure the ObjectDataSource so that it invokes the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method.</span></span>


<span data-ttu-id="14939-152">[![已调用 GetProductsByCategoryID(categoryID) 方法 ObjectDataSource](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="14939-152">[![Have the ObjectDataSource Invoke the GetProductsByCategoryID(categoryID) Method](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image19.png)</span></span>

<span data-ttu-id="14939-153">**图 7**： 具有 ObjectDataSource 调用`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="14939-153">**Figure 7**: Have the ObjectDataSource Invoke the `GetProductsByCategoryID(categoryID)` Method ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image21.png))</span></span>


<span data-ttu-id="14939-154">由于`GetProductsByCategoryID(categoryID)`方法采用一个输入参数，在向导的最后一步中，我们可以指定参数值的源。</span><span class="sxs-lookup"><span data-stu-id="14939-154">Since the `GetProductsByCategoryID(categoryID)` method takes in an input parameter, in the final step of the wizard we can specify the source of the parameter value.</span></span> <span data-ttu-id="14939-155">为了显示从所选类别这些产品，则用参数从拉取`Categories`DropDownList。</span><span class="sxs-lookup"><span data-stu-id="14939-155">In order to display those products from the selected category, have the parameter pulled from the `Categories` DropDownList.</span></span>


<span data-ttu-id="14939-156">[![从选择的类别 DropDownList 获取 categoryID 参数值](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="14939-156">[![Get the categoryID Parameter Value from the Selected Categories DropDownList](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image22.png)</span></span>

<span data-ttu-id="14939-157">**图 8**： 获取*`categoryID`* 从所选类别下拉列表的参数值 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="14939-157">**Figure 8**: Get the *`categoryID`* Parameter Value from the Selected Categories DropDownList ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image24.png))</span></span>


<span data-ttu-id="14939-158">完成向导后 GridView 都将有 BoundField 的每个产品的属性。</span><span class="sxs-lookup"><span data-stu-id="14939-158">After completing the wizard the GridView will have a BoundField for each of the product properties.</span></span> <span data-ttu-id="14939-159">让我们来清理这些 BoundFields 以便仅`ProductName`， `UnitPrice`， `UnitsInStock`，和`UnitsOnOrder`BoundFields 会显示。</span><span class="sxs-lookup"><span data-stu-id="14939-159">Let's clean up these BoundFields so that only the `ProductName`, `UnitPrice`, `UnitsInStock`, and `UnitsOnOrder` BoundFields are displayed.</span></span> <span data-ttu-id="14939-160">请尝试将任何字段级别设置添加到剩余 BoundFields (如格式`UnitPrice`作为一种货币)。</span><span class="sxs-lookup"><span data-stu-id="14939-160">Feel free to add any field-level settings to the remaining BoundFields (such as formatting the `UnitPrice` as a currency).</span></span> <span data-ttu-id="14939-161">进行这些更改后，GridView 的声明性标记应类似于以下：</span><span class="sxs-lookup"><span data-stu-id="14939-161">After making these changes, the GridView's declarative markup should look similar to the following:</span></span>


[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample1.aspx)]

<span data-ttu-id="14939-162">此时我们具有完全正常运行的主/详细信息报表的订购件属于所选类别这些产品显示名称、 单价、 库存，量和单位。</span><span class="sxs-lookup"><span data-stu-id="14939-162">At this point we have a fully functioning master/detail report that shows the name, unit price, units in stock, and units on order for those products that belong to the selected category.</span></span>


<span data-ttu-id="14939-163">[![从选择的类别 DropDownList 获取 categoryID 参数值](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="14939-163">[![Get the categoryID Parameter Value from the Selected Categories DropDownList](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image25.png)</span></span>

<span data-ttu-id="14939-164">**图 9**： 获取*`categoryID`* 从所选类别下拉列表的参数值 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="14939-164">**Figure 9**: Get the *`categoryID`* Parameter Value from the Selected Categories DropDownList ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image27.png))</span></span>


## <a name="step-2-displaying-a-footer-in-the-gridview"></a><span data-ttu-id="14939-165">步骤 2： 在 GridView 中显示页脚</span><span class="sxs-lookup"><span data-stu-id="14939-165">Step 2: Displaying a Footer in the GridView</span></span>

<span data-ttu-id="14939-166">GridView 控件可以显示页眉和页脚行。</span><span class="sxs-lookup"><span data-stu-id="14939-166">The GridView control can display both a header and footer row.</span></span> <span data-ttu-id="14939-167">这些行显示的值决定`ShowHeader`和`ShowFooter`属性，分别与`ShowHeader`默认为`true`和`ShowFooter`到`false`。</span><span class="sxs-lookup"><span data-stu-id="14939-167">These rows are displayed depending on the values of the `ShowHeader` and `ShowFooter` properties, respectively, with `ShowHeader` defaulting to `true` and `ShowFooter` to `false`.</span></span> <span data-ttu-id="14939-168">若要只需包含在 GridView 的页脚设置其`ShowFooter`属性`true`。</span><span class="sxs-lookup"><span data-stu-id="14939-168">To include a footer in the GridView simply set its `ShowFooter` property to `true`.</span></span>


<span data-ttu-id="14939-169">[![GridView ShowFooter 属性设置为 true](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="14939-169">[![Set the GridView's ShowFooter Property to true](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image28.png)</span></span>

<span data-ttu-id="14939-170">**图 10**： 设置 GridView`ShowFooter`属性`true`([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image30.png))</span><span class="sxs-lookup"><span data-stu-id="14939-170">**Figure 10**: Set the GridView's `ShowFooter` Property to `true` ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image30.png))</span></span>


<span data-ttu-id="14939-171">页脚行具有 GridView; 中定义的字段的每个单元格但是，这些单元格是默认情况下为空。</span><span class="sxs-lookup"><span data-stu-id="14939-171">The footer row has a cell for each of the fields defined in the GridView; however, these cells are empty by default.</span></span> <span data-ttu-id="14939-172">需要一段时间来在浏览器中查看我们的进度。</span><span class="sxs-lookup"><span data-stu-id="14939-172">Take a moment to view our progress in a browser.</span></span> <span data-ttu-id="14939-173">与`ShowFooter`属性现在设置为`true`，GridView 包括空的页脚行。</span><span class="sxs-lookup"><span data-stu-id="14939-173">With the `ShowFooter` property now set to `true`, the GridView includes an empty footer row.</span></span>


<span data-ttu-id="14939-174">[![GridView 现在包括页脚行](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="14939-174">[![The GridView Now Includes a Footer Row](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image31.png)</span></span>

<span data-ttu-id="14939-175">**图 11**: GridView 现在包括尾行 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image33.png))</span><span class="sxs-lookup"><span data-stu-id="14939-175">**Figure 11**: The GridView Now Includes a Footer Row ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image33.png))</span></span>


<span data-ttu-id="14939-176">图 11 中的页脚行不会突出显示，因为它具有白色背景。</span><span class="sxs-lookup"><span data-stu-id="14939-176">The footer row in Figure 11 doesn't stand out, as it has a white background.</span></span> <span data-ttu-id="14939-177">让我们创建`FooterStyle`CSS 类`Styles.css`，指定深红色背景，然后配置`GridView.skin`中的外观文件`DataWebControls`主题向 GridView 的分配此 CSS 类`FooterStyle`的`CssClass`属性。</span><span class="sxs-lookup"><span data-stu-id="14939-177">Let's create a `FooterStyle` CSS class in `Styles.css` that specifies a dark red background and then configure the `GridView.skin` Skin file in the `DataWebControls` Theme to assign this CSS class to the GridView's `FooterStyle`'s `CssClass` property.</span></span> <span data-ttu-id="14939-178">如果你需要提升外观和主题，回头参考[将数据显示与 ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)教程。</span><span class="sxs-lookup"><span data-stu-id="14939-178">If you need to brush up on Skins and Themes, refer back to the [Displaying Data With the ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) tutorial.</span></span>

<span data-ttu-id="14939-179">首先，通过添加以下 CSS 类`Styles.css`:</span><span class="sxs-lookup"><span data-stu-id="14939-179">Start by adding the following CSS class to `Styles.css`:</span></span>


[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample2.css)]

<span data-ttu-id="14939-180">`FooterStyle` CSS 类中是类似的样式应用到`HeaderStyle`类，尽管`HeaderStyle`的背景色是很微妙更深的地方，其文本将以粗体显示。</span><span class="sxs-lookup"><span data-stu-id="14939-180">The `FooterStyle` CSS class is similar in style to the `HeaderStyle` class, although the `HeaderStyle`'s background color is subtlety darker and its text is displayed in a bold font.</span></span> <span data-ttu-id="14939-181">此外，页脚中的文本为右对齐; 而居中标头的文本。</span><span class="sxs-lookup"><span data-stu-id="14939-181">Furthermore, the text in the footer is right-aligned whereas the header's text is centered.</span></span>

<span data-ttu-id="14939-182">接下来，若要将此 CSS 类与每个 GridView 页脚相关联，请打开`GridView.skin`文件中`DataWebControls`主题和集`FooterStyle`的`CssClass`属性。</span><span class="sxs-lookup"><span data-stu-id="14939-182">Next, to associate this CSS class with every GridView's footer, open the `GridView.skin` file in the `DataWebControls` Theme and set the `FooterStyle`'s `CssClass` property.</span></span> <span data-ttu-id="14939-183">在此添加后文件的标记应如下所示：</span><span class="sxs-lookup"><span data-stu-id="14939-183">After this addition the file's markup should look like:</span></span>


[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample3.aspx)]

<span data-ttu-id="14939-184">在下面所示的屏幕快照，此更改作出页脚清晰地突显出来的详细信息。</span><span class="sxs-lookup"><span data-stu-id="14939-184">As the screen shot below shows, this change makes the footer stand out more clearly.</span></span>


<span data-ttu-id="14939-185">[![GridView 的页脚行现在具有红色背景色](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image34.png)</span><span class="sxs-lookup"><span data-stu-id="14939-185">[![The GridView's Footer Row Now Has a Reddish Background Color](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image34.png)</span></span>

<span data-ttu-id="14939-186">**图 12**: GridView 页脚行现在具有红色背景色 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image36.png))</span><span class="sxs-lookup"><span data-stu-id="14939-186">**Figure 12**: The GridView's Footer Row Now Has a Reddish Background Color ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image36.png))</span></span>


## <a name="step-3-computing-the-summary-data"></a><span data-ttu-id="14939-187">步骤 3： 计算摘要数据</span><span class="sxs-lookup"><span data-stu-id="14939-187">Step 3: Computing the Summary Data</span></span>

<span data-ttu-id="14939-188">使用显示的 GridView 的页脚，面向我们的下一个挑战是如何计算摘要数据。</span><span class="sxs-lookup"><span data-stu-id="14939-188">With the GridView's footer displayed, the next challenge facing us is how to compute the summary data.</span></span> <span data-ttu-id="14939-189">有两种方法来计算此聚合的信息：</span><span class="sxs-lookup"><span data-stu-id="14939-189">There are two ways to compute this aggregate information:</span></span>

1. <span data-ttu-id="14939-190">通过 SQL 查询我们无法向数据库来计算特定类别的摘要数据发出的其他查询。</span><span class="sxs-lookup"><span data-stu-id="14939-190">Through a SQL query we could issue an additional query to the database to compute the summary data for a particular category.</span></span> <span data-ttu-id="14939-191">SQL 包括大量的聚合函数以及`GROUP BY`子句以指定应通过该汇总数据的数据。</span><span class="sxs-lookup"><span data-stu-id="14939-191">SQL includes a number of aggregate functions along with a `GROUP BY` clause to specify the data over which the data should be summarized.</span></span> <span data-ttu-id="14939-192">以下 SQL 查询将恢复所需的信息：</span><span class="sxs-lookup"><span data-stu-id="14939-192">The following SQL query would bring back the needed information:</span></span>  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample4.sql)]

    <span data-ttu-id="14939-193">当然，您不希望发出直接从此查询`SummaryDataInFooter.aspx`页上，但会通过创建中的方法`ProductsTableAdapter`和`ProductsBLL`。</span><span class="sxs-lookup"><span data-stu-id="14939-193">Of course you wouldn't want to issue this query directly from the `SummaryDataInFooter.aspx` page, but rather by creating a method in the `ProductsTableAdapter` and the `ProductsBLL`.</span></span>
2. <span data-ttu-id="14939-194">计算此信息，因为它将被添加到 GridView 中, 所述[自定义格式设置基于时数据](custom-formatting-based-upon-data-cs.md)教程，GridView`RowDataBound`事件处理程序引发一次每个行添加到 GridView 后其已数据绑定。</span><span class="sxs-lookup"><span data-stu-id="14939-194">Compute this information as it's being added to the GridView as discussed in [Custom Formatting Based Upon Data](custom-formatting-based-upon-data-cs.md) tutorial, the GridView's `RowDataBound` event handler fires once for each row being added to the GridView after its been databound.</span></span> <span data-ttu-id="14939-195">通过创建此事件的事件处理程序，我们可以将是正在运行的总我们期待的值的聚合。</span><span class="sxs-lookup"><span data-stu-id="14939-195">By creating an event handler for this event we can keep a running total of the values we want to aggregate.</span></span> <span data-ttu-id="14939-196">上次数据行已绑定到 GridView 我们具有总计和所需计算平均值的信息。</span><span class="sxs-lookup"><span data-stu-id="14939-196">After the last data row has been bound to the GridView we have the totals and the information needed to compute the average.</span></span>

<span data-ttu-id="14939-197">我通常采用第二种方法，它将行程保存到数据库和数据访问层和业务逻辑层中实现的摘要的功能所需的工作量，但是这两种方法便已足够。</span><span class="sxs-lookup"><span data-stu-id="14939-197">I typically employ the second approach as it saves a trip to the database and the effort needed to implement the summary functionality in the Data Access Layer and Business Logic Layer, but either approach would suffice.</span></span> <span data-ttu-id="14939-198">对于本教程让我们使用第二个选项，并跟踪正在运行的总使用`RowDataBound`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="14939-198">For this tutorial let's use the second option and keep track of the running total using the `RowDataBound` event handler.</span></span>

<span data-ttu-id="14939-199">创建`RowDataBound`事件处理程序，方法是通过在设计器中选择 GridView，单击闪电形图标从属性窗口中，双击 GridView`RowDataBound`事件。</span><span class="sxs-lookup"><span data-stu-id="14939-199">Create a `RowDataBound` event handler for the GridView by selecting the GridView in the Designer, clicking the lightning bolt icon from the Properties window, and double-clicking the `RowDataBound` event.</span></span> <span data-ttu-id="14939-200">这将创建名为一个新的事件处理程序`ProductsInCategory_RowDataBound`中`SummaryDataInFooter.aspx`页的代码隐藏类。</span><span class="sxs-lookup"><span data-stu-id="14939-200">This will create a new event handler named `ProductsInCategory_RowDataBound` in the `SummaryDataInFooter.aspx` page's code-behind class.</span></span>


[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample5.cs)]

<span data-ttu-id="14939-201">为了维护运行总和我们需要定义事件处理程序的范围之外的变量。</span><span class="sxs-lookup"><span data-stu-id="14939-201">In order to maintain a running total we need to define variables outside of the scope of the event handler.</span></span> <span data-ttu-id="14939-202">创建以下四个页面级别变量：</span><span class="sxs-lookup"><span data-stu-id="14939-202">Create the following four page-level variables:</span></span>

- <span data-ttu-id="14939-203">`_totalUnitPrice`的类型 `decimal`</span><span class="sxs-lookup"><span data-stu-id="14939-203">`_totalUnitPrice`, of type `decimal`</span></span>
- <span data-ttu-id="14939-204">`_totalNonNullUnitPriceCount`的类型 `int`</span><span class="sxs-lookup"><span data-stu-id="14939-204">`_totalNonNullUnitPriceCount`, of type `int`</span></span>
- <span data-ttu-id="14939-205">`_totalUnitsInStock`的类型 `int`</span><span class="sxs-lookup"><span data-stu-id="14939-205">`_totalUnitsInStock`, of type `int`</span></span>
- <span data-ttu-id="14939-206">`_totalUnitsOnOrder`的类型 `int`</span><span class="sxs-lookup"><span data-stu-id="14939-206">`_totalUnitsOnOrder`, of type `int`</span></span>

<span data-ttu-id="14939-207">接下来，编写代码以递增这三个变量，每个数据行中遇到`RowDataBound`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="14939-207">Next, write the code to increment these three variables for each data row encountered in the `RowDataBound` event handler.</span></span>


[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample6.cs)]

<span data-ttu-id="14939-208">`RowDataBound`通过确保我们正在处理 DataRow 启动事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="14939-208">The `RowDataBound` event handler starts by ensuring that we're dealing with a DataRow.</span></span> <span data-ttu-id="14939-209">一旦已建立的`Northwind.ProductsRow`只绑定到的实例`GridViewRow`对象在`e.Row`变量中存储`product`。</span><span class="sxs-lookup"><span data-stu-id="14939-209">Once that's been established, the `Northwind.ProductsRow` instance that was just bound to the `GridViewRow` object in `e.Row` is stored in the variable `product`.</span></span> <span data-ttu-id="14939-210">下一步，它运行的总变量就会递增当前产品的对应值 1 (前提是它们不包含数据库`NULL`值)。</span><span class="sxs-lookup"><span data-stu-id="14939-210">Next, running total variables are incremented by the current product's corresponding values (assuming that they don't contain a database `NULL` value).</span></span> <span data-ttu-id="14939-211">我们跟踪的两个运行`UnitPrice`总计和数非`NULL``UnitPrice`记录因为平均价格为这两个数字的商。</span><span class="sxs-lookup"><span data-stu-id="14939-211">We keep track of both the running `UnitPrice` total and the number of non-`NULL` `UnitPrice` records because the average price is the quotient of these two numbers.</span></span>

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a><span data-ttu-id="14939-212">步骤 4： 在页脚中显示的摘要数据</span><span class="sxs-lookup"><span data-stu-id="14939-212">Step 4: Displaying the Summary Data in the Footer</span></span>

<span data-ttu-id="14939-213">服务器总计在一起的摘要数据，最后一步是将其显示在 GridView 的页脚行。</span><span class="sxs-lookup"><span data-stu-id="14939-213">With the summary data totaled, the last step is to display it in the GridView's footer row.</span></span> <span data-ttu-id="14939-214">此任务中，也可以以编程方式通过`RowDataBound`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="14939-214">This task, too, can be accomplished programmatically through the `RowDataBound` event handler.</span></span> <span data-ttu-id="14939-215">回想一下，`RowDataBound`个事件处理程序都会激发*每个*绑定到 GridView，包括页脚行的行。</span><span class="sxs-lookup"><span data-stu-id="14939-215">Recall that the `RowDataBound` event handler fires for *every* row that's bound to the GridView, including the footer row.</span></span> <span data-ttu-id="14939-216">因此，我们可以增加我们的事件处理程序，以显示页脚行中使用下面的代码中的数据：</span><span class="sxs-lookup"><span data-stu-id="14939-216">Therefore, we can augment our event handler to display the data in the footer row using the following code:</span></span>


[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample7.cs)]

<span data-ttu-id="14939-217">由于页脚行添加到 GridView 后已添加的所有数据行，我们可以确信，按时间我们已准备好运行的总计算将已完成的脚注中显示的摘要数据。</span><span class="sxs-lookup"><span data-stu-id="14939-217">Since the footer row is added to the GridView after all of the data rows have been added, we can be confident that by the time we're ready to display the summary data in the footer the running total calculations will have completed.</span></span> <span data-ttu-id="14939-218">最后一步中，然后，是在表尾的单元格设置这些值。</span><span class="sxs-lookup"><span data-stu-id="14939-218">The last step, then, is to set these values in the footer's cells.</span></span>

<span data-ttu-id="14939-219">若要在特定的页脚单元格中显示文本，请使用`e.Row.Cells[index].Text = value`，其中`Cells`索引从 0 处开始。</span><span class="sxs-lookup"><span data-stu-id="14939-219">To display text in a particular footer cell, use `e.Row.Cells[index].Text = value`, where the `Cells` indexing starts at 0.</span></span> <span data-ttu-id="14939-220">下面的代码计算平均价格 （除以产品数的总价格），以及总单位数，库存顺序的 GridView 相应页脚单元格上单元中显示内容。</span><span class="sxs-lookup"><span data-stu-id="14939-220">The following code computes the average price (the total price divided by the number of products) and displays it along with the total number of units in stock and units on order in the appropriate footer cells of the GridView.</span></span>


[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample8.cs)]

<span data-ttu-id="14939-221">图 13 显示报表后已添加此代码。</span><span class="sxs-lookup"><span data-stu-id="14939-221">Figure 13 shows the report after this code has been added.</span></span> <span data-ttu-id="14939-222">请注意如何`ToString("c")`格式为一种货币将平均价格摘要信息。</span><span class="sxs-lookup"><span data-stu-id="14939-222">Note how the `ToString("c")` causes the average price summary information to be formatted like a currency.</span></span>


<span data-ttu-id="14939-223">[![GridView 的页脚行现在具有红色背景色](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image37.png)</span><span class="sxs-lookup"><span data-stu-id="14939-223">[![The GridView's Footer Row Now Has a Reddish Background Color](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image37.png)</span></span>

<span data-ttu-id="14939-224">**图 13**: GridView 页脚行现在具有红色背景色 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image39.png))</span><span class="sxs-lookup"><span data-stu-id="14939-224">**Figure 13**: The GridView's Footer Row Now Has a Reddish Background Color ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image39.png))</span></span>


## <a name="summary"></a><span data-ttu-id="14939-225">总结</span><span class="sxs-lookup"><span data-stu-id="14939-225">Summary</span></span>

<span data-ttu-id="14939-226">显示摘要数据是常见的报表要求，并 GridView 控件可以轻松地在其页脚行中包括此类信息。</span><span class="sxs-lookup"><span data-stu-id="14939-226">Displaying summary data is a common report requirement, and the GridView control makes it easy to include such information in its footer row.</span></span> <span data-ttu-id="14939-227">显示页脚行时 GridView`ShowFooter`属性设置为`true`中以编程方式通过设置其单元格可以包含文本和`RowDataBound`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="14939-227">The footer row is displayed when the GridView's `ShowFooter` property is set to `true` and can have the text in its cells set programmatically through the `RowDataBound` event handler.</span></span> <span data-ttu-id="14939-228">计算摘要数据或者可以通过重新查询数据库或通过使用代码在 ASP.NET 页的代码隐藏类以编程方式计算摘要数据。</span><span class="sxs-lookup"><span data-stu-id="14939-228">Computing the summary data can either be done by re-querying the database or by using code in the ASP.NET page's code-behind class to programmatically compute the summary data.</span></span>

<span data-ttu-id="14939-229">本教程到结束 GridView、 说明如何和 FormView 控件使用的自定义格式设置我们的检查。</span><span class="sxs-lookup"><span data-stu-id="14939-229">This tutorial concludes our examination of custom formatting with the GridView, DetailsView, and FormView controls.</span></span> <span data-ttu-id="14939-230">我们的下一步教程中启动时，我们浏览的插入、 更新和删除使用这些相同的控件的数据。</span><span class="sxs-lookup"><span data-stu-id="14939-230">Our next tutorial kicks off our exploration of inserting, updating, and deleting data using these same controls.</span></span>

<span data-ttu-id="14939-231">尽情享受编程 ！</span><span class="sxs-lookup"><span data-stu-id="14939-231">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="14939-232">关于作者</span><span class="sxs-lookup"><span data-stu-id="14939-232">About the Author</span></span>

<span data-ttu-id="14939-233">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的七个 ASP/ASP.NET 书籍和的创始人[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年使用与 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="14939-233">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="14939-234">Scott 的作用是作为独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="14939-234">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="14939-235">最新书籍是[ *Sam 教授自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="14939-235">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="14939-236">他可以达到在[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)或通过他的博客，其中可以找到在[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="14939-236">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="14939-237">[上一页](using-the-formview-s-templates-cs.md)
> [下一页](custom-formatting-based-upon-data-vb.md)</span><span class="sxs-lookup"><span data-stu-id="14939-237">[Previous](using-the-formview-s-templates-cs.md)
[Next](custom-formatting-based-upon-data-vb.md)</span></span>
