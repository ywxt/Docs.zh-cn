---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
title: 基于数据 (VB) 自定义格式设置 |Microsoft Docs
author: rick-anderson
description: 可以通过多种方式来调整的 GridView、 detailsview 和 FormView 取决于绑定到它的数据格式。 在本教程中，我们将 l...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: df5a1525-386f-4632-972c-57b199870bc3
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 2ed55c181534e18bbbb4447ce9a4e5c19ff3717b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366195"
---
<a name="custom-formatting-based-upon-data-vb"></a><span data-ttu-id="7c1b9-104">自定义格式设置取决于数据 (VB)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-104">Custom Formatting Based Upon Data (VB)</span></span>
====================
<span data-ttu-id="7c1b9-105">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="7c1b9-106">[下载示例应用程序](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_11_VB.exe)或[下载 PDF](custom-formatting-based-upon-data-vb/_static/datatutorial11vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-106">[Download Sample App](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_11_VB.exe) or [Download PDF](custom-formatting-based-upon-data-vb/_static/datatutorial11vb1.pdf)</span></span>

> <span data-ttu-id="7c1b9-107">可以通过多种方式来调整的 GridView、 detailsview 和 FormView 取决于绑定到它的数据格式。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-107">Adjusting the format of the GridView, DetailsView, or FormView based upon the data bound to it can be accomplished in multiple ways.</span></span> <span data-ttu-id="7c1b9-108">在本教程中我们将介绍如何完成数据绑定通过使用 DataBound 和 RowDataBound 事件处理程序格式设置。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-108">In this tutorial we'll look at how to accomplish data bound formatting through the use of the DataBound and RowDataBound event handlers.</span></span>


## <a name="introduction"></a><span data-ttu-id="7c1b9-109">介绍</span><span class="sxs-lookup"><span data-stu-id="7c1b9-109">Introduction</span></span>

<span data-ttu-id="7c1b9-110">可以通过大量与样式有关的属性的自定义 GridView、 DetailsView 和 FormView 控件的外观。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-110">The appearance of the GridView, DetailsView, and FormView controls can be customized through a myriad of style-related properties.</span></span> <span data-ttu-id="7c1b9-111">属性，如`CssClass`， `Font`， `BorderWidth`， `BorderStyle`， `BorderColor`， `Width`，和`Height`，等等，指示呈现的控件的常规外观。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-111">Properties like `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`, `Width`, and `Height`, among others, dictate the general appearance of the rendered control.</span></span> <span data-ttu-id="7c1b9-112">属性包括`HeaderStyle`， `RowStyle`， `AlternatingRowStyle`，和其他允许这些相同的样式设置将应用于特定部分。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-112">Properties including `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`, and others allow these same style settings to be applied to particular sections.</span></span> <span data-ttu-id="7c1b9-113">同样，可以在字段级别应用这些样式设置。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-113">Likewise, these style settings can be applied at the field level.</span></span>

<span data-ttu-id="7c1b9-114">在许多情况下，格式设置要求取决于所显示的数据的值。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-114">In many scenarios though, the formatting requirements depend upon the value of the displayed data.</span></span> <span data-ttu-id="7c1b9-115">例如，若要绘制注意若要查看的常用产品，一个报告，列出产品信息可能背景颜色设置为对这些产品的黄色`UnitsInStock`和`UnitsOnOrder`字段都等于 0。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-115">For example, to draw attention to out of stock products, a report listing product information might set the background color to yellow for those products whose `UnitsInStock` and `UnitsOnOrder` fields are both equal to 0.</span></span> <span data-ttu-id="7c1b9-116">若要突出显示的成本更高的产品，我们可能想要显示多个为加粗字体中 75.00 美元的成本计算这些产品的价格。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-116">To highlight the more expensive products, we may want to display the prices of those products costing more than $75.00 in a bold font.</span></span>

<span data-ttu-id="7c1b9-117">可以通过多种方式来调整的 GridView、 detailsview 和 FormView 取决于绑定到它的数据格式。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-117">Adjusting the format of the GridView, DetailsView, or FormView based upon the data bound to it can be accomplished in multiple ways.</span></span> <span data-ttu-id="7c1b9-118">在本教程中我们将介绍如何完成数据绑定使用格式设置`DataBound`和`RowDataBound`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-118">In this tutorial we'll look at how to accomplish data bound formatting through the use of the `DataBound` and `RowDataBound` event handlers.</span></span> <span data-ttu-id="7c1b9-119">在下一教程中，我们将探讨一种替代方法。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-119">In the next tutorial we'll explore an alternative approach.</span></span>

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a><span data-ttu-id="7c1b9-120">使用 DetailsView 控件`DataBound`事件处理程序</span><span class="sxs-lookup"><span data-stu-id="7c1b9-120">Using the DetailsView Control's`DataBound`Event Handler</span></span>

<span data-ttu-id="7c1b9-121">当数据绑定到 DetailsView，从数据源控件或通过以编程方式将数据分配给控件的`DataSource`属性并调用其`DataBind()`方法时，执行以下步骤序列：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-121">When data is bound to a DetailsView, either from a data source control or through programmatically assigning data to the control's `DataSource` property and calling its `DataBind()` method, the following sequence of steps occur:</span></span>

1. <span data-ttu-id="7c1b9-122">数据 Web 控件的`DataBinding`事件触发。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-122">The data Web control's `DataBinding` event fires.</span></span>
2. <span data-ttu-id="7c1b9-123">数据绑定到数据 Web 控件。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-123">The data is bound to the data Web control.</span></span>
3. <span data-ttu-id="7c1b9-124">数据 Web 控件的`DataBound`事件触发。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-124">The data Web control's `DataBound` event fires.</span></span>

<span data-ttu-id="7c1b9-125">可以通过事件处理程序的步骤 1 和 3 后立即插入自定义逻辑。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-125">Custom logic can be injected immediately after steps 1 and 3 through an event handler.</span></span> <span data-ttu-id="7c1b9-126">通过创建的事件处理程序`DataBound`我们可以以编程方式确定已被数据绑定到数据 Web 控件并调整的格式设置的按需的事件。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-126">By creating an event handler for the `DataBound` event we can programmatically determine the data that has been bound to the data Web control and adjust the formatting as needed.</span></span> <span data-ttu-id="7c1b9-127">为了说明这一点让我们创建的将列出关于某种产品的常规信息，但会显示 DetailsView`UnitPrice`中的值***加粗、 倾斜字体***如果超过 $75.00。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-127">To illustrate this let's create a DetailsView that will list general information about a product, but will display the `UnitPrice` value in a ***bold, italic font*** if it exceeds $75.00.</span></span>

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a><span data-ttu-id="7c1b9-128">步骤 1： 在 DetailsView 中显示的产品信息</span><span class="sxs-lookup"><span data-stu-id="7c1b9-128">Step 1: Displaying the Product Information in a DetailsView</span></span>

<span data-ttu-id="7c1b9-129">打开`CustomColors.aspx`页中`CustomFormatting`文件夹中，将从工具箱拖到设计器的 DetailsView 控件，设置其`ID`属性值设置为`ExpensiveProductsPriceInBoldItalic`，并将其绑定到新的 ObjectDataSource 控件调用`ProductsBLL`类的`GetProducts()`方法。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-129">Open the `CustomColors.aspx` page in the `CustomFormatting` folder, drag a DetailsView control from the Toolbox onto the Designer, set its `ID` property value to `ExpensiveProductsPriceInBoldItalic`, and bind it to a new ObjectDataSource control that invokes the `ProductsBLL` class's `GetProducts()` method.</span></span> <span data-ttu-id="7c1b9-130">实现此目的的详细的步骤为简洁起见，我们探讨这些详细信息中在前面的教程中由于此处省略。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-130">The detailed steps for accomplishing this are omitted here for brevity since we examined them in detail in previous tutorials.</span></span>

<span data-ttu-id="7c1b9-131">一旦您已绑定到 DetailsView 的 ObjectDataSource，花点时间来修改字段列表。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-131">Once you've bound the ObjectDataSource to the DetailsView, take a moment to modify the field list.</span></span> <span data-ttu-id="7c1b9-132">我选择要删除`ProductID`， `SupplierID`， `CategoryID`， `UnitsInStock`， `UnitsOnOrder`， `ReorderLevel`，和`Discontinued`BoundFields 和重命名和重新格式化剩余 BoundFields。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-132">I've opted to remove the `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`, and `Discontinued` BoundFields and renamed and reformatted the remaining BoundFields.</span></span> <span data-ttu-id="7c1b9-133">我也被清除`Width`和`Height`设置。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-133">I also cleared out the `Width` and `Height` settings.</span></span> <span data-ttu-id="7c1b9-134">由于 DetailsView 显示单个记录，我们需要启用分页，才能允许最终用户可以查看所有产品。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-134">Since the DetailsView displays only a single record, we need to enable paging in order to allow the end user to view all of the products.</span></span> <span data-ttu-id="7c1b9-135">通过检查 DetailsView 的智能标记中的启用分页复选框来实现。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-135">Do so by checking the Enable Paging checkbox in the DetailsView's smart tag.</span></span>


<span data-ttu-id="7c1b9-136">[![图 1： 检查 DetailsView 的智能标记中的启用分页复选框](custom-formatting-based-upon-data-vb/_static/image2.png)](custom-formatting-based-upon-data-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-136">[![Figure 1: Check the Enable Paging Checkbox in the DetailsView's Smart Tag](custom-formatting-based-upon-data-vb/_static/image2.png)](custom-formatting-based-upon-data-vb/_static/image1.png)</span></span>

<span data-ttu-id="7c1b9-137">**图 1**： 图 1： 检查启用分页中的复选框 DetailsView 的智能标记 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7c1b9-137">**Figure 1**: Figure 1: Check the Enable Paging Checkbox in the DetailsView's Smart Tag ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image3.png))</span></span>


<span data-ttu-id="7c1b9-138">更改后，将为 DetailsView 标记：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-138">After these changes, the DetailsView markup will be:</span></span>


[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample1.aspx)]

<span data-ttu-id="7c1b9-139">请花费片刻时间来查看此页在浏览器中测试。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-139">Take a moment to test out this page in your browser.</span></span>


<span data-ttu-id="7c1b9-140">[![在 DetailsView 控件一次显示一种产品](custom-formatting-based-upon-data-vb/_static/image5.png)](custom-formatting-based-upon-data-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-140">[![The DetailsView Control Displays One Product at a Time](custom-formatting-based-upon-data-vb/_static/image5.png)](custom-formatting-based-upon-data-vb/_static/image4.png)</span></span>

<span data-ttu-id="7c1b9-141">**图 2**： 根据 DetailsView 控件显示一个产品一次 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="7c1b9-141">**Figure 2**: The DetailsView Control Displays One Product at a Time ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image6.png))</span></span>


## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a><span data-ttu-id="7c1b9-142">步骤 2： 以编程方式确定数据绑定事件处理程序中的数据的值</span><span class="sxs-lookup"><span data-stu-id="7c1b9-142">Step 2: Programmatically Determining the Value of the Data in the DataBound Event Handler</span></span>

<span data-ttu-id="7c1b9-143">若要对这些产品加粗、 倾斜字体显示价格其`UnitPrice`值超过 $75.00，我们需要首先能以编程方式确定`UnitPrice`值。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-143">In order to display the price in a bold, italic font for those products whose `UnitPrice` value exceeds $75.00, we need to first be able to programmatically determine the `UnitPrice` value.</span></span> <span data-ttu-id="7c1b9-144">对于 DetailsView，这可以完成`DataBound`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-144">For the DetailsView, this can be accomplished in the `DataBound` event handler.</span></span> <span data-ttu-id="7c1b9-145">若要创建事件处理程序在设计器中 DetailsView 单击，然后导航到属性窗口。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-145">To create the event handler click on the DetailsView in the Designer then navigate to the Properties window.</span></span> <span data-ttu-id="7c1b9-146">按 F4 以显示它，如果不可见，或转到视图菜单并选择属性窗口的菜单选项。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-146">Press F4 to bring it up, if it's not visible, or go to the View menu and select the Properties Window menu option.</span></span> <span data-ttu-id="7c1b9-147">在属性窗口中，单击闪电形图标以列出 DetailsView 的事件。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-147">From the Properties window, click on the lightning bolt icon to list the DetailsView's events.</span></span> <span data-ttu-id="7c1b9-148">接下来，双击`DataBound`事件或键入你想要创建的事件处理程序的名称。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-148">Next, either double-click the `DataBound` event or type in the name of the event handler you want to create.</span></span>


![为数据绑定事件创建事件处理程序](custom-formatting-based-upon-data-vb/_static/image7.png)

<span data-ttu-id="7c1b9-150">**图 3**： 创建的事件处理程序`DataBound`事件</span><span class="sxs-lookup"><span data-stu-id="7c1b9-150">**Figure 3**: Create an Event Handler for the `DataBound` Event</span></span>


> [!NOTE]
> <span data-ttu-id="7c1b9-151">从 ASP.NET 页面的代码部分中，还可以创建一个事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-151">You can also create an event handler from the ASP.NET page's code portion.</span></span> <span data-ttu-id="7c1b9-152">那里您会发现在页面顶部的两个下拉列表。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-152">There you'll find two drop-down lists at the top of the page.</span></span> <span data-ttu-id="7c1b9-153">从左侧的下拉列表中选择对象和你想要从右侧下拉列表和 Visual Studio 中创建的处理程序的事件将自动创建相应的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-153">Select the object from the left drop-down list and the event you want to create a handler for from the right drop-down list and Visual Studio will automatically create the appropriate event handler.</span></span>


<span data-ttu-id="7c1b9-154">执行此操作将自动创建事件处理程序，并将您带到的代码部分添加的位置。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-154">Doing so will automatically create the event handler and take you to the code portion where it has been added.</span></span> <span data-ttu-id="7c1b9-155">此时会看到：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-155">At this point you will see:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample2.vb)]

<span data-ttu-id="7c1b9-156">可以通过访问数据绑定到 DetailsView`DataItem`属性。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-156">The data bound to the DetailsView can be accessed via the `DataItem` property.</span></span> <span data-ttu-id="7c1b9-157">回想一下，我们将我们控件绑定到的强类型化 DataRow 实例的集合组成的强类型化 DataTable。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-157">Recall that we are binding our controls to a strongly-typed DataTable, which is composed of a collection of strongly-typed DataRow instances.</span></span> <span data-ttu-id="7c1b9-158">在 DataTable 绑定到 DetailsView，DataTable 中的第一个 DataRow 分配给 DetailsView`DataItem`属性。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-158">When the DataTable is bound to the DetailsView, the first DataRow in the DataTable is assigned to the DetailsView's `DataItem` property.</span></span> <span data-ttu-id="7c1b9-159">具体而言，`DataItem`属性分配`DataRowView`对象。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-159">Specifically, the `DataItem` property is assigned a `DataRowView` object.</span></span> <span data-ttu-id="7c1b9-160">我们可以使用`DataRowView`的`Row`属性来访问基础 DataRow 对象，它是实际`ProductsRow`实例。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-160">We can use the `DataRowView`'s `Row` property to get access to the underlying DataRow object, which is actually a `ProductsRow` instance.</span></span> <span data-ttu-id="7c1b9-161">一旦我们有这`ProductsRow`我们可以通过简单地检查对象的属性值使我们决策的实例。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-161">Once we have this `ProductsRow` instance we can make our decision by simply inspecting the object's property values.</span></span>

<span data-ttu-id="7c1b9-162">下面的代码演示如何确定是否`UnitPrice`绑定到 DetailsView 控件的值是否大于 $75.00:</span><span class="sxs-lookup"><span data-stu-id="7c1b9-162">The following code illustrates how to determine whether the `UnitPrice` value bound to the DetailsView control is greater than $75.00:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample3.vb)]

> [!NOTE]
> <span data-ttu-id="7c1b9-163">由于`UnitPrice`可以有`NULL`数据库中的值，我们首先检查以确保，我们并没有解决`NULL`值，然后才能访问`ProductsRow`的`UnitPrice`属性。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-163">Since `UnitPrice` can have a `NULL` value in the database, we first check to make sure that we're not dealing with a `NULL` value before accessing the `ProductsRow`'s `UnitPrice` property.</span></span> <span data-ttu-id="7c1b9-164">此检查非常重要因为如果我们尝试访问`UnitPrice`属性时它具有`NULL`值`ProductsRow`对象将引发[StrongTypingException 异常](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-164">This check is important because if we attempt to access the `UnitPrice` property when it has a `NULL` value the `ProductsRow` object will throw a [StrongTypingException exception](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx).</span></span>


## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a><span data-ttu-id="7c1b9-165">步骤 3： 设置 DetailsView 中的单价值的格式</span><span class="sxs-lookup"><span data-stu-id="7c1b9-165">Step 3: Formatting the UnitPrice Value in the DetailsView</span></span>

<span data-ttu-id="7c1b9-166">现在我们可以确定是否`UnitPrice`值绑定到 DetailsView 具有某个值超过 $75.00，不过我们但若要了解如何以编程方式调整 DetailsView 的格式设置相应地。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-166">At this point we can determine whether the `UnitPrice` value bound to the DetailsView has a value that exceeds $75.00, but we've yet to see how to programmatically adjust the DetailsView's formatting accordingly.</span></span> <span data-ttu-id="7c1b9-167">若要修改在 DetailsView 中整个行的格式设置，以编程方式访问行使用`DetailsViewID.Rows(index)`; 若要修改特定单元格，访问，请使用`DetailsViewID.Rows(index).Cells(index)`。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-167">To modify the formatting of an entire row in the DetailsView, programmatically access the row using `DetailsViewID.Rows(index)`; to modify a particular cell, access use `DetailsViewID.Rows(index).Cells(index)`.</span></span> <span data-ttu-id="7c1b9-168">一旦我们有对我们然后可以通过设置其样式相关的属性来调整其外观的单元格的行的引用。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-168">Once we have a reference to the row or cell we can then adjust its appearance by setting its style-related properties.</span></span>

<span data-ttu-id="7c1b9-169">访问行以编程方式要求你知道的行的索引，从 0 开始。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-169">Accessing a row programmatically requires that you know the row's index, which starts at 0.</span></span> <span data-ttu-id="7c1b9-170">`UnitPrice`行是 DetailsView，向其提供的 4 索引并使其以编程方式访问中的第五个行使用`ExpensiveProductsPriceInBoldItalic.Rows(4)`。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-170">The `UnitPrice` row is the fifth row in the DetailsView, giving it an index of 4 and making it programmatically accessible using `ExpensiveProductsPriceInBoldItalic.Rows(4)`.</span></span> <span data-ttu-id="7c1b9-171">现在我们可以使用以下代码显示加粗、 倾斜字体中的整个行的内容：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-171">At this point we could have the entire row's content displayed in a bold, italic font by using the following code:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample4.vb)]

<span data-ttu-id="7c1b9-172">但是，这将使*同时*标签 （价格） 和粗体和斜体的值。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-172">However, this will make *both* the label (Price) and the value bold and italic.</span></span> <span data-ttu-id="7c1b9-173">如果我们想要使只是值粗体和斜体我们需要将此应用到的第二个单元格的行，可以使用以下格式：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-173">If we want to make just the value bold and italic we need to apply this formatting to the second cell in the row, which can be accomplished using the following:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample5.vb)]

<span data-ttu-id="7c1b9-174">由于我们的教程到目前为止已使用样式表来维护与样式有关的信息呈现的标记之间完全分离，而不是设置特定的样式属性，如上所示让我们改为使用 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-174">Since our tutorials thus far have used stylesheets to maintain a clean separation between the rendered markup and style-related information, rather than setting the specific style properties as shown above let's instead use a CSS class.</span></span> <span data-ttu-id="7c1b9-175">打开`Styles.css`样式表并添加一个名为的新 CSS 类`ExpensivePriceEmphasis`以下定义：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-175">Open the `Styles.css` stylesheet and add a new CSS class named `ExpensivePriceEmphasis` with the following definition:</span></span>


[!code-css[Main](custom-formatting-based-upon-data-vb/samples/sample6.css)]

<span data-ttu-id="7c1b9-176">然后，在`DataBound`事件处理程序设置的单元格`CssClass`属性设置为`ExpensivePriceEmphasis`。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-176">Then, in the `DataBound` event handler, set the cell's `CssClass` property to `ExpensivePriceEmphasis`.</span></span> <span data-ttu-id="7c1b9-177">下面的代码演示`DataBound`完整的事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-177">The following code shows the `DataBound` event handler in its entirety:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample7.vb)]

<span data-ttu-id="7c1b9-178">时查看 Chai，小于 75.00 美元的费用，价格显示为正常字体 （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-178">When viewing Chai, which costs less than $75.00, the price is displayed in a normal font (see Figure 4).</span></span> <span data-ttu-id="7c1b9-179">但是，当查看 Mishi Kobe Niku，具有 97.00 美元的价格，价格会显示在加粗、 倾斜字体 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-179">However, when viewing Mishi Kobe Niku, which has a price of $97.00, the price is displayed in a bold, italic font (see Figure 5).</span></span>


<span data-ttu-id="7c1b9-180">[![价格小于 $75.00 将显示在普通字体](custom-formatting-based-upon-data-vb/_static/image9.png)](custom-formatting-based-upon-data-vb/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-180">[![Prices Less than $75.00 are Displayed in a Normal Font](custom-formatting-based-upon-data-vb/_static/image9.png)](custom-formatting-based-upon-data-vb/_static/image8.png)</span></span>

<span data-ttu-id="7c1b9-181">**图 4**： 价格小于 $75.00 将显示在普通字体 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="7c1b9-181">**Figure 4**: Prices Less than $75.00 are Displayed in a Normal Font ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image10.png))</span></span>


<span data-ttu-id="7c1b9-182">[![粗体、 斜体字体显示昂贵产品的价格](custom-formatting-based-upon-data-vb/_static/image12.png)](custom-formatting-based-upon-data-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-182">[![Expensive Products' Prices are Displayed in a Bold, Italic Font](custom-formatting-based-upon-data-vb/_static/image12.png)](custom-formatting-based-upon-data-vb/_static/image11.png)</span></span>

<span data-ttu-id="7c1b9-183">**图 5**： 中加粗、 倾斜字体显示昂贵产品的价格 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-vb/_static/image13.png))</span><span class="sxs-lookup"><span data-stu-id="7c1b9-183">**Figure 5**: Expensive Products' Prices are Displayed in a Bold, Italic Font ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image13.png))</span></span>


## <a name="using-the-formview-controlsdataboundevent-handler"></a><span data-ttu-id="7c1b9-184">使用 FormView 控件`DataBound`事件处理程序</span><span class="sxs-lookup"><span data-stu-id="7c1b9-184">Using the FormView Control's`DataBound`Event Handler</span></span>

<span data-ttu-id="7c1b9-185">确定基础数据绑定到 FormView 的步骤是相同的 DetailsView 创建`DataBound`事件处理程序，强制转换`DataItem`为适当的对象类型的属性绑定到控件，并确定如何继续执行。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-185">The steps for determining the underlying data bound to a FormView are identical to those for a DetailsView create a `DataBound` event handler, cast the `DataItem` property to the appropriate object type bound to the control, and determine how to proceed.</span></span> <span data-ttu-id="7c1b9-186">FormView 和 DetailsView 有所不同，但是，在如何更新用户界面的外观。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-186">The FormView and DetailsView differ, however, in how their user interface's appearance is updated.</span></span>

<span data-ttu-id="7c1b9-187">FormView 不包含任何 BoundFields 并因此缺少`Rows`集合。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-187">The FormView does not contain any BoundFields and therefore lacks the `Rows` collection.</span></span> <span data-ttu-id="7c1b9-188">相反，FormView 组成的模板，可以包含多种静态 HTML，Web 控件和数据绑定语法。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-188">Instead, a FormView is composed of templates, which can contain a mix of static HTML, Web controls, and databinding syntax.</span></span> <span data-ttu-id="7c1b9-189">调整的 FormView 样式通常涉及调整一个或多个 FormView 的模板中的 Web 控件的样式。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-189">Adjusting the style of a FormView typically involves adjusting the style of one or more of the Web controls within the FormView's templates.</span></span>

<span data-ttu-id="7c1b9-190">若要说明这一点，让我们使用 FormView 到产品列表中上一示例中，但这次让我们喜欢显示只是产品名称和单位以红色字体显示，如果它小于或等于 10 的库存数量的库存数量。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-190">To illustrate this, let's use a FormView to list products like in the previous example, but this time let's display just the product name and units in stock with the units in stock displayed in a red font if it is less than or equal to 10.</span></span>

## <a name="step-4-displaying-the-product-information-in-a-formview"></a><span data-ttu-id="7c1b9-191">步骤 4： 在 FormView 中显示的产品信息</span><span class="sxs-lookup"><span data-stu-id="7c1b9-191">Step 4: Displaying the Product Information in a FormView</span></span>

<span data-ttu-id="7c1b9-192">添加到 FormView`CustomColors.aspx`页下的 DetailsView 并设置其`ID`属性设置为`LowStockedProductsInRed`。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-192">Add a FormView to the `CustomColors.aspx` page beneath the DetailsView and set its `ID` property to `LowStockedProductsInRed`.</span></span> <span data-ttu-id="7c1b9-193">将 FormView 绑定到上一步中创建的 ObjectDataSource 控件。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-193">Bind the FormView to the ObjectDataSource control created from the previous step.</span></span> <span data-ttu-id="7c1b9-194">这将创建`ItemTemplate`， `EditItemTemplate`，和`InsertItemTemplate`FormView 的。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-194">This will create an `ItemTemplate`, `EditItemTemplate`, and `InsertItemTemplate` for the FormView.</span></span> <span data-ttu-id="7c1b9-195">删除`EditItemTemplate`和`InsertItemTemplate`并简化`ItemTemplate`包括只需`ProductName`和`UnitsInStock`值，每个在其自己适当地命名为标签控件中。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-195">Remove the `EditItemTemplate` and `InsertItemTemplate` and simplify the `ItemTemplate` to include just the `ProductName` and `UnitsInStock` values, each in their own appropriately-named Label controls.</span></span> <span data-ttu-id="7c1b9-196">与前面的示例从 DetailsView，还检查 FormView 的智能标记中的启用分页复选框。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-196">As with the DetailsView from the earlier example, also check the Enable Paging checkbox in the FormView's smart tag.</span></span>

<span data-ttu-id="7c1b9-197">以后这些编辑 FormView 的标记看起来应类似于下面：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-197">After these edits your FormView's markup should look similar to the following:</span></span>


[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample8.aspx)]

<span data-ttu-id="7c1b9-198">请注意，`ItemTemplate`包含：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-198">Note that the `ItemTemplate` contains:</span></span>

- <span data-ttu-id="7c1b9-199">**静态 HTML**文本"产品:"和"库存数量:"连同`<br />`和`<b>`元素。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-199">**Static HTML** the text "Product:" and "Units In Stock:" along with the `<br />` and `<b>` elements.</span></span>
- <span data-ttu-id="7c1b9-200">**Web 控件**两个标签控件，`ProductNameLabel`和`UnitsInStockLabel`。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-200">**Web controls** the two Label controls, `ProductNameLabel` and `UnitsInStockLabel`.</span></span>
- <span data-ttu-id="7c1b9-201">**数据绑定语法**`<%# Bind("ProductName") %>`并`<%# Bind("UnitsInStock") %>`语法，将从这些字段的值分配给标签控件的`Text`属性。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-201">**Databinding syntax** the `<%# Bind("ProductName") %>` and `<%# Bind("UnitsInStock") %>` syntax, which assigns the values from these fields to the Label controls' `Text` properties.</span></span>

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a><span data-ttu-id="7c1b9-202">步骤 5： 以编程方式确定数据绑定事件处理程序中的数据的值</span><span class="sxs-lookup"><span data-stu-id="7c1b9-202">Step 5: Programmatically Determining the Value of the Data in the DataBound Event Handler</span></span>

<span data-ttu-id="7c1b9-203">使用 FormView 的标记完成下, 一步是以编程方式确定如果`UnitsInStock`值是否小于或等于 10。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-203">With the FormView's markup complete, the next step is to programmatically determine if the `UnitsInStock` value is less than or equal to 10.</span></span> <span data-ttu-id="7c1b9-204">完成此操作完全相同的方式与 FormView 中使用 DetailsView 一样。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-204">This is accomplished in the exact same manner with the FormView as it was with the DetailsView.</span></span> <span data-ttu-id="7c1b9-205">首先，创建一个事件处理程序的 FormView 的`DataBound`事件。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-205">Start by creating an event handler for the FormView's `DataBound` event.</span></span>


![创建数据绑定事件处理程序](custom-formatting-based-upon-data-vb/_static/image14.png)

<span data-ttu-id="7c1b9-207">**图 6**： 创建`DataBound`事件处理程序</span><span class="sxs-lookup"><span data-stu-id="7c1b9-207">**Figure 6**: Create the `DataBound` Event Handler</span></span>


<span data-ttu-id="7c1b9-208">在事件处理程序转换 FormView`DataItem`属性设置为`ProductsRow`实例，并确定是否`UnitsInPrice`值是这样，我们需要以红色字体显示。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-208">In the event handler cast the FormView's `DataItem` property to a `ProductsRow` instance and determine whether the `UnitsInPrice` value is such that we need to display it in a red font.</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample9.vb)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a><span data-ttu-id="7c1b9-209">步骤 6： 格式设置在 FormView ItemTemplate UnitsInStockLabel 标签控件</span><span class="sxs-lookup"><span data-stu-id="7c1b9-209">Step 6: Formatting the UnitsInStockLabel Label Control in the FormView's ItemTemplate</span></span>

<span data-ttu-id="7c1b9-210">最后一步是设置的格式显示`UnitsInStock`以红色字体值，如果值为 10 或更少。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-210">The final step is to format the displayed `UnitsInStock` value in a red font if the value is 10 or less.</span></span> <span data-ttu-id="7c1b9-211">若要完成此我们需要以编程方式访问`UnitsInStockLabel`控件中`ItemTemplate`并设置其样式属性，以便显示其文本为红色。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-211">To accomplish this we need to programmatically access the `UnitsInStockLabel` control in the `ItemTemplate` and set its style properties so that its text is displayed in red.</span></span> <span data-ttu-id="7c1b9-212">若要访问的 Web 控件模板中，使用`FindControl("controlID")`方法如下：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-212">To access a Web control in a template, use the `FindControl("controlID")` method like this:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample10.vb)]

<span data-ttu-id="7c1b9-213">对于我们的示例中我们想要访问标签控件`ID`值是`UnitsInStockLabel`，因此，我们将使用：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-213">For our example we want to access a Label control whose `ID` value is `UnitsInStockLabel`, so we'd use:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample11.vb)]

<span data-ttu-id="7c1b9-214">对 Web 控件的编程引用后，我们可以根据需要修改其与样式有关的属性。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-214">Once we have a programmatic reference to the Web control, we can modify its style-related properties as needed.</span></span> <span data-ttu-id="7c1b9-215">如前面的示例中，我创建了中的 CSS 类`Styles.css`名为`LowUnitsInStockEmphasis`。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-215">As with the earlier example, I've created a CSS class in `Styles.css` named `LowUnitsInStockEmphasis`.</span></span> <span data-ttu-id="7c1b9-216">若要将此样式应用于标签 Web 控件，设置其`CssClass`属性相应地。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-216">To apply this style to the Label Web control, set its `CssClass` property accordingly.</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample12.vb)]

> [!NOTE]
> <span data-ttu-id="7c1b9-217">格式设置以编程方式访问使用在 Web 控件模板的语法`FindControl("controlID")`，然后设置其样式相关的属性还可用使用时[Templatefield](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) DetailsView 或 GridView 中控件。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-217">The syntax for formatting a template programmatically accessing the Web control using `FindControl("controlID")` and then setting its style-related properties can also be used when using [TemplateFields](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) in the DetailsView or GridView controls.</span></span> <span data-ttu-id="7c1b9-218">我们将在下一教程中我们介绍 Templatefield。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-218">We'll examine TemplateFields in our next tutorial.</span></span>


<span data-ttu-id="7c1b9-219">图 7 显示了 FormView 查看产品时其`UnitsInStock`值大于 10，而图 8 中的产品具有其值小于 10。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-219">Figures 7 shows the FormView when viewing a product whose `UnitsInStock` value is greater than 10, while the product in Figure 8 has its value less than 10.</span></span>


<span data-ttu-id="7c1b9-220">[![对于产品具有足够大 Units In Stock，无自定义格式设置将应用](custom-formatting-based-upon-data-vb/_static/image16.png)](custom-formatting-based-upon-data-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-220">[![For Products With a Sufficiently Large Units In Stock, No Custom Formatting is Applied](custom-formatting-based-upon-data-vb/_static/image16.png)](custom-formatting-based-upon-data-vb/_static/image15.png)</span></span>

<span data-ttu-id="7c1b9-221">**图 7**： 应用的产品具有足够大 Units In Stock、 无自定义格式设置 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-vb/_static/image17.png))</span><span class="sxs-lookup"><span data-stu-id="7c1b9-221">**Figure 7**: For Products With a Sufficiently Large Units In Stock, No Custom Formatting is Applied ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image17.png))</span></span>


<span data-ttu-id="7c1b9-222">[![在库存数量的单位以红色显示的那些产品使用的值小于或等于 10](custom-formatting-based-upon-data-vb/_static/image19.png)](custom-formatting-based-upon-data-vb/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-222">[![The Units in Stock Number is Shown in Red for Those Products With Values of 10 or Less](custom-formatting-based-upon-data-vb/_static/image19.png)](custom-formatting-based-upon-data-vb/_static/image18.png)</span></span>

<span data-ttu-id="7c1b9-223">**图 8**： 内库存数量的设备以红色显示的那些产品使用的值小于或等于 10 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="7c1b9-223">**Figure 8**: The Units in Stock Number is Shown in Red for Those Products With Values of 10 or Less ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image20.png))</span></span>


## <a name="formatting-with-the-gridviewsrowdataboundevent"></a><span data-ttu-id="7c1b9-224">使用 GridView 的格式设置`RowDataBound`事件</span><span class="sxs-lookup"><span data-stu-id="7c1b9-224">Formatting with the GridView's`RowDataBound`Event</span></span>

<span data-ttu-id="7c1b9-225">前面部分中，我们探讨的一系列步骤 DetailsView 和 FormView 控件在数据绑定期间通过进度。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-225">Earlier we examined the sequence of steps the DetailsView and FormView controls progress through during databinding.</span></span> <span data-ttu-id="7c1b9-226">让我们看这些步骤再一次作为刷新程序。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-226">Let's look over these steps once again as a refresher.</span></span>

1. <span data-ttu-id="7c1b9-227">数据 Web 控件的`DataBinding`事件触发。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-227">The data Web control's `DataBinding` event fires.</span></span>
2. <span data-ttu-id="7c1b9-228">数据绑定到数据 Web 控件。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-228">The data is bound to the data Web control.</span></span>
3. <span data-ttu-id="7c1b9-229">数据 Web 控件的`DataBound`事件触发。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-229">The data Web control's `DataBound` event fires.</span></span>

<span data-ttu-id="7c1b9-230">这三个简单步骤便足以针对 DetailsView 和 FormView，因为它们显示单个记录。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-230">These three simple steps are sufficient for the DetailsView and FormView because they display only a single record.</span></span> <span data-ttu-id="7c1b9-231">对于 GridView，其中显示*所有*记录绑定到它 （而不仅仅是第一个），第 2 步是稍微要复杂。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-231">For the GridView, which displays *all* records bound to it (not just the first), step 2 is a bit more involved.</span></span>

<span data-ttu-id="7c1b9-232">步骤的 2 GridView 枚举数据源，并为每个记录创建`GridViewRow`实例并对其绑定的当前记录。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-232">In step 2 the GridView enumerates the data source and, for each record, creates a `GridViewRow` instance and binds the current record to it.</span></span> <span data-ttu-id="7c1b9-233">每个`GridViewRow`添加到 GridView，会引发两个事件：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-233">For each `GridViewRow` added to the GridView, two events are raised:</span></span>

- <span data-ttu-id="7c1b9-234">**`RowCreated`** 之后才激发`GridViewRow`已创建</span><span class="sxs-lookup"><span data-stu-id="7c1b9-234">**`RowCreated`** fires after the `GridViewRow` has been created</span></span>
- <span data-ttu-id="7c1b9-235">**`RowDataBound`** 已绑定到当前记录之后激发`GridViewRow`。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-235">**`RowDataBound`** fires after the current record has been bound to the `GridViewRow`.</span></span>

<span data-ttu-id="7c1b9-236">对于 GridView 中，然后，数据绑定更准确地描述了通过以下步骤序列：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-236">For the GridView, then, data binding is more accurately described by the following sequence of steps:</span></span>

1. <span data-ttu-id="7c1b9-237">GridView 的`DataBinding`事件触发。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-237">The GridView's `DataBinding` event fires.</span></span>
2. <span data-ttu-id="7c1b9-238">将数据绑定到 GridView。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-238">The data is bound to the GridView.</span></span>   
  
   <span data-ttu-id="7c1b9-239">为数据源中的每个记录</span><span class="sxs-lookup"><span data-stu-id="7c1b9-239">For each record in the data source</span></span> 

    1. <span data-ttu-id="7c1b9-240">创建`GridViewRow`对象</span><span class="sxs-lookup"><span data-stu-id="7c1b9-240">Create a `GridViewRow` object</span></span>
    2. <span data-ttu-id="7c1b9-241">激发`RowCreated`事件</span><span class="sxs-lookup"><span data-stu-id="7c1b9-241">Fire the `RowCreated` event</span></span>
    3. <span data-ttu-id="7c1b9-242">将绑定到的记录 `GridViewRow`</span><span class="sxs-lookup"><span data-stu-id="7c1b9-242">Bind the record to the `GridViewRow`</span></span>
    4. <span data-ttu-id="7c1b9-243">激发`RowDataBound`事件</span><span class="sxs-lookup"><span data-stu-id="7c1b9-243">Fire the `RowDataBound` event</span></span>
    5. <span data-ttu-id="7c1b9-244">添加`GridViewRow`到`Rows`集合</span><span class="sxs-lookup"><span data-stu-id="7c1b9-244">Add the `GridViewRow` to the `Rows` collection</span></span>
3. <span data-ttu-id="7c1b9-245">GridView 的`DataBound`事件触发。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-245">The GridView's `DataBound` event fires.</span></span>

<span data-ttu-id="7c1b9-246">若要自定义 GridView 的单个记录的格式，然后，我们需要创建的事件处理程序`RowDataBound`事件。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-246">To customize the format of the GridView's individual records, then, we need to create an event handler for the `RowDataBound` event.</span></span> <span data-ttu-id="7c1b9-247">若要说明这一点，让我们将添加到 GridView`CustomColors.aspx`页面列出了名称、 类别和每个产品，突出显示的价格是不超过 10.00 美元的部分用黄色背景颜色的那些产品价格。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-247">To illustrate this, let's add a GridView to the `CustomColors.aspx` page that lists the name, category, and price for each product, highlighting those products whose price is less than $10.00 with a yellow background color.</span></span>

## <a name="step-7-displaying-product-information-in-a-gridview"></a><span data-ttu-id="7c1b9-248">步骤 7： 在 GridView 中显示的产品信息</span><span class="sxs-lookup"><span data-stu-id="7c1b9-248">Step 7: Displaying Product Information in a GridView</span></span>

<span data-ttu-id="7c1b9-249">上一示例中添加下 FormView GridView，并设置其`ID`属性设置为`HighlightCheapProducts`。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-249">Add a GridView beneath the FormView from the previous example and set its `ID` property to `HighlightCheapProducts`.</span></span> <span data-ttu-id="7c1b9-250">因为我们已经有 ObjectDataSource，返回所有产品页上，将 GridView 绑定到的。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-250">Since we already have an ObjectDataSource that returns all products on the page, bind the GridView to that.</span></span> <span data-ttu-id="7c1b9-251">最后，编辑 GridView 的 BoundFields 包括只需产品的名称、 类别和价格。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-251">Finally, edit the GridView's BoundFields to include just the products' names, categories, and prices.</span></span> <span data-ttu-id="7c1b9-252">在这些编辑后 GridView 的标记应如下所示：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-252">After these edits the GridView's markup should look like:</span></span>


[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample13.aspx)]

<span data-ttu-id="7c1b9-253">图 9 显示了我们到目前为止的浏览器查看时的进度。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-253">Figure 9 shows our progress to this point when viewed through a browser.</span></span>


<span data-ttu-id="7c1b9-254">[![GridView 列出名称、 类别和每个产品的价格](custom-formatting-based-upon-data-vb/_static/image22.png)](custom-formatting-based-upon-data-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-254">[![The GridView Lists the Name, Category, and Price For Each Product](custom-formatting-based-upon-data-vb/_static/image22.png)](custom-formatting-based-upon-data-vb/_static/image21.png)</span></span>

<span data-ttu-id="7c1b9-255">**图 9**: GridView 列出名称、 类别和每个产品的价格 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-vb/_static/image23.png))</span><span class="sxs-lookup"><span data-stu-id="7c1b9-255">**Figure 9**: The GridView Lists the Name, Category, and Price For Each Product ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image23.png))</span></span>


## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a><span data-ttu-id="7c1b9-256">步骤 8： 以编程方式确定 RowDataBound 事件处理程序中的数据的值</span><span class="sxs-lookup"><span data-stu-id="7c1b9-256">Step 8: Programmatically Determining the Value of the Data in the RowDataBound Event Handler</span></span>

<span data-ttu-id="7c1b9-257">当`ProductsDataTable`绑定到 GridView 其`ProductsRow`已枚举，并为每个实例`ProductsRow``GridViewRow`创建。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-257">When the `ProductsDataTable` is bound to the GridView its `ProductsRow` instances are enumerated and for each `ProductsRow` a `GridViewRow` is created.</span></span> <span data-ttu-id="7c1b9-258">`GridViewRow`的`DataItem`属性分配给特定`ProductRow`，在其后 GridView 的`RowDataBound`引发事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-258">The `GridViewRow`'s `DataItem` property is assigned to the particular `ProductRow`, after which the GridView's `RowDataBound` event handler is raised.</span></span> <span data-ttu-id="7c1b9-259">若要确定`UnitPrice`每个产品的值绑定到 GridView，然后，我们需要为 GridView 的创建事件处理程序`RowDataBound`事件。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-259">To determine the `UnitPrice` value for each product bound to the GridView, then, we need to create an event handler for the GridView's `RowDataBound` event.</span></span> <span data-ttu-id="7c1b9-260">在此事件处理程序可以检查`UnitPrice`值为当前`GridViewRow`，并为该行格式设置决定。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-260">In this event handler we can inspect the `UnitPrice` value for the current `GridViewRow` and make a formatting decision for that row.</span></span>

<span data-ttu-id="7c1b9-261">可以使用 FormView 和 DetailsView 中使用相同的一系列步骤作为创建此事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-261">This event handler can be created using the same series of steps as with the FormView and DetailsView.</span></span>


![GridView 的 RowDataBound 事件创建事件处理程序](custom-formatting-based-upon-data-vb/_static/image24.png)

<span data-ttu-id="7c1b9-263">**图 10**： 创建 GridView 的事件处理程序`RowDataBound`事件</span><span class="sxs-lookup"><span data-stu-id="7c1b9-263">**Figure 10**: Create an Event Handler for the GridView's `RowDataBound` Event</span></span>


<span data-ttu-id="7c1b9-264">以这种方式创建的事件处理程序将导致自动添加到 ASP.NET 页面的代码部分的以下代码：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-264">Creating the event hander in this manner will cause the following code to be automatically added to the ASP.NET page's code portion:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample14.vb)]

<span data-ttu-id="7c1b9-265">当`RowDataBound`事件触发时，事件处理程序作为其第二个参数传递类型的对象`GridViewRowEventArgs`，其中有一个名为`Row`。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-265">When the `RowDataBound` event fires, the event handler is passed as its second parameter an object of type `GridViewRowEventArgs`, which has a property named `Row`.</span></span> <span data-ttu-id="7c1b9-266">此属性返回的引用`GridViewRow`那只是数据绑定。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-266">This property returns a reference to the `GridViewRow` that was just data bound.</span></span> <span data-ttu-id="7c1b9-267">访问`ProductsRow`实例绑定到`GridViewRow`我们使用`DataItem`属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-267">To access the `ProductsRow` instance bound to the `GridViewRow` we use the `DataItem` property like so:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample15.vb)]

<span data-ttu-id="7c1b9-268">使用时`RowDataBound`务必要记住 GridView 组成不同类型的行，为激发此事件的事件处理程序*所有*行类型。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-268">When working with the `RowDataBound` event handler it is important to keep in mind that the GridView is composed of different types of rows and that this event is fired for *all* row types.</span></span> <span data-ttu-id="7c1b9-269">一个`GridViewRow`的类型可以由其`RowType`属性，并且可以具有的可能值之一：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-269">A `GridViewRow`'s type can be determined by its `RowType` property, and can have one of the possible values:</span></span>

- <span data-ttu-id="7c1b9-270">`DataRow` 从 GridView 绑定到一个记录的行 `DataSource`</span><span class="sxs-lookup"><span data-stu-id="7c1b9-270">`DataRow` a row that is bound to a record from the GridView's `DataSource`</span></span>
- <span data-ttu-id="7c1b9-271">`EmptyDataRow` 如果显示的行 GridView 的`DataSource`为空</span><span class="sxs-lookup"><span data-stu-id="7c1b9-271">`EmptyDataRow` the row displayed if the GridView's `DataSource` is empty</span></span>
- <span data-ttu-id="7c1b9-272">`Footer` 脚注行;显示的如果 GridView 的`ShowFooter`属性设置为 `True`</span><span class="sxs-lookup"><span data-stu-id="7c1b9-272">`Footer` the footer row; shown if the GridView's `ShowFooter` property is set to `True`</span></span>
- <span data-ttu-id="7c1b9-273">`Header` 标头行中;显示是否 GridView 的 ShowHeader 属性设置为`True`（默认值）</span><span class="sxs-lookup"><span data-stu-id="7c1b9-273">`Header` the header row; shown if the GridView's ShowHeader property is set to `True` (the default)</span></span>
- <span data-ttu-id="7c1b9-274">`Pager` 对于 GridView 的实现分页，显示分页界面的行</span><span class="sxs-lookup"><span data-stu-id="7c1b9-274">`Pager` for GridView's that implement paging, the row that displays the paging interface</span></span>
- <span data-ttu-id="7c1b9-275">`Separator` 未使用 GridView，但由`RowType`DataList 和 Repeater 的属性控制，两个数据 Web 控件，我们将讨论在将来教程</span><span class="sxs-lookup"><span data-stu-id="7c1b9-275">`Separator` not used for the GridView, but used by the `RowType` properties for the DataList and Repeater controls, two data Web controls we'll discuss in future tutorials</span></span>

<span data-ttu-id="7c1b9-276">由于`EmptyDataRow`， `Header`， `Footer`，和`Pager`行不与关联`DataSource`记录，它们将始终具有值的`Nothing`有关其`DataItem`属性。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-276">Since the `EmptyDataRow`, `Header`, `Footer`, and `Pager` rows aren't associated with a `DataSource` record, they will always have a value of `Nothing` for their `DataItem` property.</span></span> <span data-ttu-id="7c1b9-277">出于此原因，然后再尝试使用当前`GridViewRow`的`DataItem`属性，我们首先必须确保我们正在处理与`DataRow`。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-277">For this reason, before attempting to work with the current `GridViewRow`'s `DataItem` property, we first must make sure that we're dealing with a `DataRow`.</span></span> <span data-ttu-id="7c1b9-278">这可以通过检查来实现`GridViewRow`的`RowType`属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-278">This can be accomplished by checking the `GridViewRow`'s `RowType` property like so:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample16.vb)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a><span data-ttu-id="7c1b9-279">步骤 9： 突出显示行黄色时单价值是小于 10.00 美元</span><span class="sxs-lookup"><span data-stu-id="7c1b9-279">Step 9: Highlighting the Row Yellow When the UnitPrice Value is Less than $10.00</span></span>

<span data-ttu-id="7c1b9-280">最后一步是以编程方式突出显示整个`GridViewRow`如果`UnitPrice`值的行是不超过 10.00 美元的部分。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-280">The last step is to programmatically highlight the entire `GridViewRow` if the `UnitPrice` value for that row is less than $10.00.</span></span> <span data-ttu-id="7c1b9-281">访问一个 GridView 行或单元格的语法是与 DetailsView 相同`GridViewID.Rows(index)`若要访问整个行，`GridViewID.Rows(index).Cells(index)`访问特定单元格。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-281">The syntax for accessing a GridView's rows or cells is the same as with the DetailsView `GridViewID.Rows(index)` to access the entire row, `GridViewID.Rows(index).Cells(index)` to access a particular cell.</span></span> <span data-ttu-id="7c1b9-282">但是，当`RowDataBound`事件处理程序会触发数据绑定`GridViewRow`尚未添加到 GridView 的`Rows`集合。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-282">However, when the `RowDataBound` event handler fires the data bound `GridViewRow` has yet to be added to the GridView's `Rows` collection.</span></span> <span data-ttu-id="7c1b9-283">因此，您不能访问当前`GridViewRow`实例与`RowDataBound`事件处理程序使用的行集合。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-283">Therefore you cannot access the current `GridViewRow` instance from the `RowDataBound` event handler using the Rows collection.</span></span>

<span data-ttu-id="7c1b9-284">而不是`GridViewID.Rows(index)`，我们可以引用当前`GridViewRow`实例中`RowDataBound`事件处理程序使用`e.Row`。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-284">Instead of `GridViewID.Rows(index)`, we can reference the current `GridViewRow` instance in the `RowDataBound` event handler using `e.Row`.</span></span> <span data-ttu-id="7c1b9-285">也就是说，为了突出显示当前`GridViewRow`实例与`RowDataBound`事件处理程序，我们将使用：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-285">That is, in order to highlight the current `GridViewRow` instance from the `RowDataBound` event handler we would use:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample17.vb)]

<span data-ttu-id="7c1b9-286">而不是设置`GridViewRow`的`BackColor`属性直接，让我们坚持使用 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-286">Rather than set the `GridViewRow`'s `BackColor` property directly, let's stick with using CSS classes.</span></span> <span data-ttu-id="7c1b9-287">我创建了一个名为的 CSS 类`AffordablePriceEmphasis`，将背景色设置为黄色。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-287">I've created a CSS class named `AffordablePriceEmphasis` that sets the background color to yellow.</span></span> <span data-ttu-id="7c1b9-288">已完成`RowDataBound`事件处理程序遵循：</span><span class="sxs-lookup"><span data-stu-id="7c1b9-288">The completed `RowDataBound` event handler follows:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample18.vb)]


<span data-ttu-id="7c1b9-289">[![最经济的产品是黄色突出显示](custom-formatting-based-upon-data-vb/_static/image26.png)](custom-formatting-based-upon-data-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-289">[![The Most Affordable Products are Highlighted Yellow](custom-formatting-based-upon-data-vb/_static/image26.png)](custom-formatting-based-upon-data-vb/_static/image25.png)</span></span>

<span data-ttu-id="7c1b9-290">**图 11**： 最经济的产品是黄色突出显示 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-vb/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="7c1b9-290">**Figure 11**: The Most Affordable Products are Highlighted Yellow ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image27.png))</span></span>


## <a name="summary"></a><span data-ttu-id="7c1b9-291">总结</span><span class="sxs-lookup"><span data-stu-id="7c1b9-291">Summary</span></span>

<span data-ttu-id="7c1b9-292">在本教程中我们已了解如何设置 GridView、 DetailsView 和 FormView 基于绑定到控件的数据的格式。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-292">In this tutorial we saw how to format the GridView, DetailsView, and FormView based on the data bound to the control.</span></span> <span data-ttu-id="7c1b9-293">若要完成此我们创建的事件处理程序`DataBound`或`RowDataBound`事件，如果需要格式设置的更改，以及检查基础数据是其中。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-293">To accomplish this we created an event handler for the `DataBound` or `RowDataBound` events, where the underlying data was examined along with a formatting change, if needed.</span></span> <span data-ttu-id="7c1b9-294">若要访问绑定到 detailsview FormView 的数据，我们使用`DataItem`中的属性`DataBound`事件处理程序; 对于 GridView 中后，每个`GridViewRow`实例的`DataItem`属性包含的数据绑定到该行，可在`RowDataBound`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-294">To access the data bound to a DetailsView or FormView, we use the `DataItem` property in the `DataBound` event handler; for a GridView, each `GridViewRow` instance's `DataItem` property contains the data bound to that row, which is available in the `RowDataBound` event handler.</span></span>

<span data-ttu-id="7c1b9-295">以编程方式调整数据 Web 控件的格式设置的语法取决于 Web 控件和要设置格式的数据的显示方式。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-295">The syntax for programmatically adjusting the data Web control's formatting depends upon the Web control and how the data to be formatted is displayed.</span></span> <span data-ttu-id="7c1b9-296">在 DetailsView 和 GridView 控件、 行和单元格可以访问的序号索引。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-296">For DetailsView and GridView controls, the rows and cells can be accessed by an ordinal index.</span></span> <span data-ttu-id="7c1b9-297">有关使用模板，FormView`FindControl("controlID")`方法通常用于查找从 Web 控件模板中的。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-297">For the FormView, which uses templates, the `FindControl("controlID")` method is commonly used to locate a Web control from within the template.</span></span>

<span data-ttu-id="7c1b9-298">在下一教程中我们将介绍如何使用 GridView 和 DetailsView 中使用模板。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-298">In the next tutorial we'll look at how to use templates with the GridView and DetailsView.</span></span> <span data-ttu-id="7c1b9-299">此外，我们将看到另一种方法用于自定义基于基础数据的格式设置。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-299">Additionally, we'll see another technique for customizing the formatting based on the underlying data.</span></span>

<span data-ttu-id="7c1b9-300">快乐编程 ！</span><span class="sxs-lookup"><span data-stu-id="7c1b9-300">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="7c1b9-301">关于作者</span><span class="sxs-lookup"><span data-stu-id="7c1b9-301">About the Author</span></span>

<span data-ttu-id="7c1b9-302">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-302">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="7c1b9-303">Scott 是独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-303">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="7c1b9-304">他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-304">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="7c1b9-305">他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-305">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="7c1b9-306">或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-306">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="7c1b9-307">特别感谢</span><span class="sxs-lookup"><span data-stu-id="7c1b9-307">Special Thanks To</span></span>

<span data-ttu-id="7c1b9-308">很多有用的审阅者已评审本系列教程。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-308">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="7c1b9-309">本教程中的潜在顾客审阅者已 E.R.</span><span class="sxs-lookup"><span data-stu-id="7c1b9-309">Lead reviewers for this tutorial were E.R.</span></span> <span data-ttu-id="7c1b9-310">Gilmore，Dennis Patterson 和 Dan Jagers。</span><span class="sxs-lookup"><span data-stu-id="7c1b9-310">Gilmore, Dennis Patterson, and Dan Jagers.</span></span> <span data-ttu-id="7c1b9-311">是否有兴趣查看我即将推出的 MSDN 文章？</span><span class="sxs-lookup"><span data-stu-id="7c1b9-311">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="7c1b9-312">如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-312">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7c1b9-313">[上一页](displaying-summary-information-in-the-gridview-s-footer-cs.md)
> [下一页](using-templatefields-in-the-gridview-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7c1b9-313">[Previous](displaying-summary-information-in-the-gridview-s-footer-cs.md)
[Next](using-templatefields-in-the-gridview-control-vb.md)</span></span>
