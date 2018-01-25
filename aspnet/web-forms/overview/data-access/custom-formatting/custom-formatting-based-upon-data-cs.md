---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
title: "自定义格式设置取决于数据 (C#) |Microsoft 文档"
author: rick-anderson
description: "调整 GridView，说明如何或 FormView 取决于绑定到它的数据的格式可以采用多种方式来完成。 在本教程中我们将 l..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 871a4574-f89c-4214-b786-79253ed3653b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 606721b01fae34a7bce85d497a442cb110f1b51e
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="custom-formatting-based-upon-data-c"></a><span data-ttu-id="bc8cf-104">自定义格式设置取决于数据 (C#)</span><span class="sxs-lookup"><span data-stu-id="bc8cf-104">Custom Formatting Based Upon Data (C#)</span></span>
====================
<span data-ttu-id="bc8cf-105">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="bc8cf-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="bc8cf-106">[下载示例应用程序](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_11_CS.exe)或[下载 PDF](custom-formatting-based-upon-data-cs/_static/datatutorial11cs1.pdf)</span><span class="sxs-lookup"><span data-stu-id="bc8cf-106">[Download Sample App](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_11_CS.exe) or [Download PDF](custom-formatting-based-upon-data-cs/_static/datatutorial11cs1.pdf)</span></span>

> <span data-ttu-id="bc8cf-107">调整 GridView，说明如何或 FormView 取决于绑定到它的数据的格式可以采用多种方式来完成。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-107">Adjusting the format of the GridView, DetailsView, or FormView based upon the data bound to it can be accomplished in multiple ways.</span></span> <span data-ttu-id="bc8cf-108">在本教程中我们将查看如何完成数据绑定通过数据绑定和 RowDataBound 事件处理程序使用格式设置。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-108">In this tutorial we'll look at how to accomplish data bound formatting through the use of the DataBound and RowDataBound event handlers.</span></span>


## <a name="introduction"></a><span data-ttu-id="bc8cf-109">介绍</span><span class="sxs-lookup"><span data-stu-id="bc8cf-109">Introduction</span></span>

<span data-ttu-id="bc8cf-110">通过提供多种样式相关的属性，可以自定义 GridView、 说明如何和 FormView 控件的外观。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-110">The appearance of the GridView, DetailsView, and FormView controls can be customized through a myriad of style-related properties.</span></span> <span data-ttu-id="bc8cf-111">属性，例如`CssClass`， `Font`， `BorderWidth`， `BorderStyle`， `BorderColor`， `Width`，和`Height`，及其他规定呈现的控件的总体外观。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-111">Properties like `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`, `Width`, and `Height`, among others, dictate the general appearance of the rendered control.</span></span> <span data-ttu-id="bc8cf-112">属性包括`HeaderStyle`， `RowStyle`， `AlternatingRowStyle`，和其他允许这些相同的样式设置应用于特定部分。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-112">Properties including `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`, and others allow these same style settings to be applied to particular sections.</span></span> <span data-ttu-id="bc8cf-113">同样，可以在字段级别应用这些样式设置。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-113">Likewise, these style settings can be applied at the field level.</span></span>

<span data-ttu-id="bc8cf-114">在许多情况下通过，格式设置的要求取决于显示的数据的值。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-114">In many scenarios though, the formatting requirements depend upon the value of the displayed data.</span></span> <span data-ttu-id="bc8cf-115">例如，若要绘制的关注，以外常用产品，列出产品信息的报表可能将背景颜色设置为黄色为这些产品其`UnitsInStock`和`UnitsOnOrder`字段都等于 0。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-115">For example, to draw attention to out of stock products, a report listing product information might set the background color to yellow for those products whose `UnitsInStock` and `UnitsOnOrder` fields are both equal to 0.</span></span> <span data-ttu-id="bc8cf-116">要突出显示的开销更大的产品，我们可能想要显示的多个用粗体 $75.00 的成本计算这些产品价格。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-116">To highlight the more expensive products, we may want to display the prices of those products costing more than $75.00 in a bold font.</span></span>

<span data-ttu-id="bc8cf-117">调整 GridView，说明如何或 FormView 取决于绑定到它的数据的格式可以采用多种方式来完成。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-117">Adjusting the format of the GridView, DetailsView, or FormView based upon the data bound to it can be accomplished in multiple ways.</span></span> <span data-ttu-id="bc8cf-118">在本教程中我们将考察如何完成数据绑定的格式设置使用`DataBound`和`RowDataBound`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-118">In this tutorial we'll look at how to accomplish data bound formatting through the use of the `DataBound` and `RowDataBound` event handlers.</span></span> <span data-ttu-id="bc8cf-119">在下一步的教程，我们将探讨另一种方法。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-119">In the next tutorial we'll explore an alternative approach.</span></span>

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a><span data-ttu-id="bc8cf-120">使用说明如何控制`DataBound`事件处理程序</span><span class="sxs-lookup"><span data-stu-id="bc8cf-120">Using the DetailsView Control's`DataBound`Event Handler</span></span>

<span data-ttu-id="bc8cf-121">当数据绑定到说明如何从数据源控件或通过以编程方式将数据分配给控件的`DataSource`属性和调用其`DataBind()`方法，下面的步骤顺序发生：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-121">When data is bound to a DetailsView, either from a data source control or through programmatically assigning data to the control's `DataSource` property and calling its `DataBind()` method, the following sequence of steps occur:</span></span>

1. <span data-ttu-id="bc8cf-122">数据的 Web 控件`DataBinding`事件激发。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-122">The data Web control's `DataBinding` event fires.</span></span>
2. <span data-ttu-id="bc8cf-123">数据绑定到 Web 控件的数据。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-123">The data is bound to the data Web control.</span></span>
3. <span data-ttu-id="bc8cf-124">数据的 Web 控件`DataBound`事件激发。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-124">The data Web control's `DataBound` event fires.</span></span>

<span data-ttu-id="bc8cf-125">可通过一个事件处理程序的步骤 1 和 3 后立即插入自定义逻辑。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-125">Custom logic can be injected immediately after steps 1 and 3 through an event handler.</span></span> <span data-ttu-id="bc8cf-126">通过创建的事件处理程序`DataBound`我们就能以编程方式确定已被数据绑定到数据 Web 控件，并调整格式根据需要的事件。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-126">By creating an event handler for the `DataBound` event we can programmatically determine the data that has been bound to the data Web control and adjust the formatting as needed.</span></span> <span data-ttu-id="bc8cf-127">为了说明这一点让我们创建说明如何将列出有关产品的常规信息，但将显示`UnitPrice`中的值***加粗、 倾斜字体***如果它超过 $75.00。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-127">To illustrate this let's create a DetailsView that will list general information about a product, but will display the `UnitPrice` value in a ***bold, italic font*** if it exceeds $75.00.</span></span>

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a><span data-ttu-id="bc8cf-128">步骤 1： 在说明中显示的产品信息</span><span class="sxs-lookup"><span data-stu-id="bc8cf-128">Step 1: Displaying the Product Information in a DetailsView</span></span>

<span data-ttu-id="bc8cf-129">打开`CustomColors.aspx`页面`CustomFormatting`文件夹中，从工具箱中拖动到设计器中将说明如何控件、 设置其`ID`属性值设置为`ExpensiveProductsPriceInBoldItalic`，并将其绑定到一个新的 ObjectDataSource 控件调用`ProductsBLL`类的`GetProducts()`方法。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-129">Open the `CustomColors.aspx` page in the `CustomFormatting` folder, drag a DetailsView control from the Toolbox onto the Designer, set its `ID` property value to `ExpensiveProductsPriceInBoldItalic`, and bind it to a new ObjectDataSource control that invokes the `ProductsBLL` class's `GetProducts()` method.</span></span> <span data-ttu-id="bc8cf-130">实现此操作的详细的步骤为简洁起见我们检查它们在详细信息在前面的教程中由于此处省略。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-130">The detailed steps for accomplishing this are omitted here for brevity since we examined them in detail in previous tutorials.</span></span>

<span data-ttu-id="bc8cf-131">一旦你已绑定到说明的对象数据源，需要一段时间来修改的字段列表。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-131">Once you've bound the ObjectDataSource to the DetailsView, take a moment to modify the field list.</span></span> <span data-ttu-id="bc8cf-132">我已选择删除`ProductID`， `SupplierID`， `CategoryID`， `UnitsInStock`， `UnitsOnOrder`， `ReorderLevel`，和`Discontinued`BoundFields 和重命名并重新格式化剩余 BoundFields。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-132">I've opted to remove the `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`, and `Discontinued` BoundFields and renamed and reformatted the remaining BoundFields.</span></span> <span data-ttu-id="bc8cf-133">我也被清除`Width`和`Height`设置。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-133">I also cleared out the `Width` and `Height` settings.</span></span> <span data-ttu-id="bc8cf-134">由于说明如何显示单个记录，我们需要启用分页，以便允许最终用户若要查看所有产品。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-134">Since the DetailsView displays only a single record, we need to enable paging in order to allow the end user to view all of the products.</span></span> <span data-ttu-id="bc8cf-135">执行此操作通过检查中说明的智能标记的启用分页复选框。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-135">Do so by checking the Enable Paging checkbox in the DetailsView's smart tag.</span></span>


<span data-ttu-id="bc8cf-136">[![检查中说明的智能标记的启用分页复选框](custom-formatting-based-upon-data-cs/_static/image2.png)](custom-formatting-based-upon-data-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bc8cf-136">[![Check the Enable Paging Checkbox in the DetailsView's Smart Tag](custom-formatting-based-upon-data-cs/_static/image2.png)](custom-formatting-based-upon-data-cs/_static/image1.png)</span></span>

<span data-ttu-id="bc8cf-137">**图 1**： 检查启用分页中的复选框说明的智能标记 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="bc8cf-137">**Figure 1**: Check the Enable Paging Checkbox in the DetailsView's Smart Tag ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image3.png))</span></span>


<span data-ttu-id="bc8cf-138">这些更改后将来说明如何标记：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-138">After these changes, the DetailsView markup will be:</span></span>


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample1.aspx)]

<span data-ttu-id="bc8cf-139">需要一段时间来测试你的浏览器中的此页。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-139">Take a moment to test out this page in your browser.</span></span>


<span data-ttu-id="bc8cf-140">[![说明如何控制一次显示一个产品](custom-formatting-based-upon-data-cs/_static/image5.png)](custom-formatting-based-upon-data-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="bc8cf-140">[![The DetailsView Control Displays One Product at a Time](custom-formatting-based-upon-data-cs/_static/image5.png)](custom-formatting-based-upon-data-cs/_static/image4.png)</span></span>

<span data-ttu-id="bc8cf-141">**图 2**: 说明如何控制显示一个产品一次 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="bc8cf-141">**Figure 2**: The DetailsView Control Displays One Product at a Time ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image6.png))</span></span>


## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a><span data-ttu-id="bc8cf-142">步骤 2： 以编程方式确定数据绑定事件处理程序中的数据的值</span><span class="sxs-lookup"><span data-stu-id="bc8cf-142">Step 2: Programmatically Determining the Value of the Data in the DataBound Event Handler</span></span>

<span data-ttu-id="bc8cf-143">若要为这些产品用粗体、 斜体字体显示价格其`UnitPrice`值超过 $75.00，我们需要首先能够以编程方式确定`UnitPrice`值。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-143">In order to display the price in a bold, italic font for those products whose `UnitPrice` value exceeds $75.00, we need to first be able to programmatically determine the `UnitPrice` value.</span></span> <span data-ttu-id="bc8cf-144">对于说明，这可以完成`DataBound`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-144">For the DetailsView, this can be accomplished in the `DataBound` event handler.</span></span> <span data-ttu-id="bc8cf-145">若要创建事件处理程序说明如何在设计器中单击，然后导航到属性窗口。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-145">To create the event handler click on the DetailsView in the Designer then navigate to the Properties window.</span></span> <span data-ttu-id="bc8cf-146">按 F4 以显示它，如果不可见，或转到视图菜单并选择属性窗口菜单选项。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-146">Press F4 to bring it up, if it's not visible, or go to the View menu and select the Properties Window menu option.</span></span> <span data-ttu-id="bc8cf-147">从属性窗口中，单击闪电形图标，若要列出说明的事件。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-147">From the Properties window, click on the lightning bolt icon to list the DetailsView's events.</span></span> <span data-ttu-id="bc8cf-148">接下来，双击`DataBound`事件或输入你想要创建的事件处理程序的名称。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-148">Next, either double-click the `DataBound` event or type in the name of the event handler you want to create.</span></span>


![为数据绑定事件创建事件处理程序](custom-formatting-based-upon-data-cs/_static/image7.png)

<span data-ttu-id="bc8cf-150">**图 3**： 创建的事件处理程序`DataBound`事件</span><span class="sxs-lookup"><span data-stu-id="bc8cf-150">**Figure 3**: Create an Event Handler for the `DataBound` Event</span></span>


<span data-ttu-id="bc8cf-151">这样将自动创建事件处理程序，并将您带到的代码部分添加的位置。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-151">Doing so will automatically create the event handler and take you to the code portion where it has been added.</span></span> <span data-ttu-id="bc8cf-152">此时你将看到：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-152">At this point you will see:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample2.cs)]

<span data-ttu-id="bc8cf-153">可以通过访问数据绑定到说明如何`DataItem`属性。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-153">The data bound to the DetailsView can be accessed via the `DataItem` property.</span></span> <span data-ttu-id="bc8cf-154">回想一下，我们将我们控件绑定到强类型 DataTable，组成的强类型 DataRow 实例的集合。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-154">Recall that we are binding our controls to a strongly-typed DataTable, which is composed of a collection of strongly-typed DataRow instances.</span></span> <span data-ttu-id="bc8cf-155">DataTable 绑定到说明如何，数据表中的第一个 DataRow 会分配给说明的`DataItem`属性。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-155">When the DataTable is bound to the DetailsView, the first DataRow in the DataTable is assigned to the DetailsView's `DataItem` property.</span></span> <span data-ttu-id="bc8cf-156">具体而言，`DataItem`属性分配`DataRowView`对象。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-156">Specifically, the `DataItem` property is assigned a `DataRowView` object.</span></span> <span data-ttu-id="bc8cf-157">我们可以使用`DataRowView`的`Row`属性以获取访问权限的基础的 DataRow 对象，这是实际`ProductsRow`实例。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-157">We can use the `DataRowView`'s `Row` property to get access to the underlying DataRow object, which is actually a `ProductsRow` instance.</span></span> <span data-ttu-id="bc8cf-158">一旦我们有这`ProductsRow`我们可以通过简单地检查对象的属性值，让我们决策的实例。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-158">Once we have this `ProductsRow` instance we can make our decision by simply inspecting the object's property values.</span></span>

<span data-ttu-id="bc8cf-159">下面的代码演示如何确定是否`UnitPrice`绑定到说明控件的值是否大于 $75.00:</span><span class="sxs-lookup"><span data-stu-id="bc8cf-159">The following code illustrates how to determine whether the `UnitPrice` value bound to the DetailsView control is greater than $75.00:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="bc8cf-160">由于`UnitPrice`可以`NULL`值在数据库中，我们首先检查以确保我们正在不处理与`NULL`前访问值`ProductsRow`的`UnitPrice`属性。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-160">Since `UnitPrice` can have a `NULL` value in the database, we first check to make sure that we're not dealing with a `NULL` value before accessing the `ProductsRow`'s `UnitPrice` property.</span></span> <span data-ttu-id="bc8cf-161">此检查是重要因为如果我们尝试访问`UnitPrice`属性时它具有`NULL`值`ProductsRow`对象将引发[StrongTypingException 异常](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-161">This check is important because if we attempt to access the `UnitPrice` property when it has a `NULL` value the `ProductsRow` object will throw a [StrongTypingException exception](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx).</span></span>


## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a><span data-ttu-id="bc8cf-162">步骤 3： 格式设置说明中的单价值</span><span class="sxs-lookup"><span data-stu-id="bc8cf-162">Step 3: Formatting the UnitPrice Value in the DetailsView</span></span>

<span data-ttu-id="bc8cf-163">此时我们可以确定是否`UnitPrice`值绑定到说明具有值超过 $75.00，但我们尚未若要了解如何以编程方式调整说明的格式设置相应地。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-163">At this point we can determine whether the `UnitPrice` value bound to the DetailsView has a value that exceeds $75.00, but we've yet to see how to programmatically adjust the DetailsView's formatting accordingly.</span></span> <span data-ttu-id="bc8cf-164">若要修改的说明中的整个行格式设置，以编程方式访问行使用`DetailsViewID.Rows[index]`; 若要修改特定的单元格，访问，请使用`DetailsViewID.Rows[index].Cells[index]`。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-164">To modify the formatting of an entire row in the DetailsView, programmatically access the row using `DetailsViewID.Rows[index]`; to modify a particular cell, access use `DetailsViewID.Rows[index].Cells[index]`.</span></span> <span data-ttu-id="bc8cf-165">一旦我们有了对我们然后可以通过设置其样式相关的属性来调整其外观的单元格的行的引用。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-165">Once we have a reference to the row or cell we can then adjust its appearance by setting its style-related properties.</span></span>

<span data-ttu-id="bc8cf-166">以编程方式访问行需要知道的行的索引，从 0 开始的。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-166">Accessing a row programmatically requires that you know the row's index, which starts at 0.</span></span> <span data-ttu-id="bc8cf-167">`UnitPrice`行是说明如何，并向其提供的 4 索引并使其以编程方式访问中的第五个一行使用`ExpensiveProductsPriceInBoldItalic.Rows[4]`。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-167">The `UnitPrice` row is the fifth row in the DetailsView, giving it an index of 4 and making it programmatically accessible using `ExpensiveProductsPriceInBoldItalic.Rows[4]`.</span></span> <span data-ttu-id="bc8cf-168">此时，我们可以通过使用下面的代码显示在加粗、 倾斜字体中的整个行的内容：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-168">At this point we could have the entire row's content displayed in a bold, italic font by using the following code:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample4.cs)]

<span data-ttu-id="bc8cf-169">但是，这将使*同时*标签 （价格） 和加粗和倾斜的值。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-169">However, this will make *both* the label (Price) and the value bold and italic.</span></span> <span data-ttu-id="bc8cf-170">如果我们想要使只是价值加粗和倾斜我们需要将此应用到的第二个单元格的行，可以使用以下格式：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-170">If we want to make just the value bold and italic we need to apply this formatting to the second cell in the row, which can be accomplished using the following:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample5.cs)]

<span data-ttu-id="bc8cf-171">由于我们的教程到目前为止已使用样式表来维护与样式有关的信息呈现的标记之间完全分离，而不是设置的特定样式属性，如上所示让我们改为使用 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-171">Since our tutorials thus far have used stylesheets to maintain a clean separation between the rendered markup and style-related information, rather than setting the specific style properties as shown above let's instead use a CSS class.</span></span> <span data-ttu-id="bc8cf-172">打开`Styles.css`样式表并添加一个名为的新的 CSS 类`ExpensivePriceEmphasis`替换为以下定义：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-172">Open the `Styles.css` stylesheet and add a new CSS class named `ExpensivePriceEmphasis` with the following definition:</span></span>


[!code-css[Main](custom-formatting-based-upon-data-cs/samples/sample6.css)]

<span data-ttu-id="bc8cf-173">然后，在`DataBound`事件处理程序设置的单元格的`CssClass`属性`ExpensivePriceEmphasis`。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-173">Then, in the `DataBound` event handler, set the cell's `CssClass` property to `ExpensivePriceEmphasis`.</span></span> <span data-ttu-id="bc8cf-174">下面的代码演示`DataBound`其完整的事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-174">The following code shows the `DataBound` event handler in its entirety:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample7.cs)]

<span data-ttu-id="bc8cf-175">查看牛奶，成本小于 $75.00，价格将显示在普通字体 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-175">When viewing Chai, which costs less than $75.00, the price is displayed in a normal font (see Figure 4).</span></span> <span data-ttu-id="bc8cf-176">但是，当查看 Mishi Kobe Niku，具有指价格为 $97.00，价格会显示在加粗、 倾斜字体 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-176">However, when viewing Mishi Kobe Niku, which has a price of $97.00, the price is displayed in a bold, italic font (see Figure 5).</span></span>


<span data-ttu-id="bc8cf-177">[![价格低于 $75.00 将显示在普通字体](custom-formatting-based-upon-data-cs/_static/image9.png)](custom-formatting-based-upon-data-cs/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="bc8cf-177">[![Prices Less than $75.00 are Displayed in a Normal Font](custom-formatting-based-upon-data-cs/_static/image9.png)](custom-formatting-based-upon-data-cs/_static/image8.png)</span></span>

<span data-ttu-id="bc8cf-178">**图 4**： 价格低于 $75.00 将显示在普通字体 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="bc8cf-178">**Figure 4**: Prices Less than $75.00 are Displayed in a Normal Font ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image10.png))</span></span>


<span data-ttu-id="bc8cf-179">[![昂贵产品的价格显示粗体、 斜体字体](custom-formatting-based-upon-data-cs/_static/image12.png)](custom-formatting-based-upon-data-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="bc8cf-179">[![Expensive Products' Prices are Displayed in a Bold, Italic Font](custom-formatting-based-upon-data-cs/_static/image12.png)](custom-formatting-based-upon-data-cs/_static/image11.png)</span></span>

<span data-ttu-id="bc8cf-180">**图 5**： 昂贵产品的价格显示粗体、 斜体字体 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image13.png))</span><span class="sxs-lookup"><span data-stu-id="bc8cf-180">**Figure 5**: Expensive Products' Prices are Displayed in a Bold, Italic Font ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image13.png))</span></span>


## <a name="using-the-formview-controlsdataboundevent-handler"></a><span data-ttu-id="bc8cf-181">使用 FormView 控件的`DataBound`事件处理程序</span><span class="sxs-lookup"><span data-stu-id="bc8cf-181">Using the FormView Control's`DataBound`Event Handler</span></span>

<span data-ttu-id="bc8cf-182">确定基础数据绑定到 FormView 的步骤是相同的说明如何创建`DataBound`事件处理程序，强制转换`DataItem`到合适的对象类型的属性绑定到控件，并确定如何继续执行。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-182">The steps for determining the underlying data bound to a FormView are identical to those for a DetailsView create a `DataBound` event handler, cast the `DataItem` property to the appropriate object type bound to the control, and determine how to proceed.</span></span> <span data-ttu-id="bc8cf-183">FormView 和说明不同，但是，在如何更新自己的用户界面的外观。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-183">The FormView and DetailsView differ, however, in how their user interface's appearance is updated.</span></span>

<span data-ttu-id="bc8cf-184">FormView 不包含任何 BoundFields 并因此缺少`Rows`集合。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-184">The FormView does not contain any BoundFields and therefore lacks the `Rows` collection.</span></span> <span data-ttu-id="bc8cf-185">相反，FormView 组成模板，其中可以包含多种静态 HTML，Web 控件，以及数据绑定语法。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-185">Instead, a FormView is composed of templates, which can contain a mix of static HTML, Web controls, and databinding syntax.</span></span> <span data-ttu-id="bc8cf-186">调整 FormView 的样式通常涉及调整一个或多个 FormView 的模板中的 Web 控件的样式。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-186">Adjusting the style of a FormView typically involves adjusting the style of one or more of the Web controls within the FormView's templates.</span></span>

<span data-ttu-id="bc8cf-187">若要说明这一点，让我们为产品列表 FormView 中前面的示例中，但这次我们喜欢的使用显示只需的产品名称和单位使用以红色字体显示，如果它小于或等于 10 的库存量单位的库存量。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-187">To illustrate this, let's use a FormView to list products like in the previous example, but this time let's display just the product name and units in stock with the units in stock displayed in a red font if it is less than or equal to 10.</span></span>

## <a name="step-4-displaying-the-product-information-in-a-formview"></a><span data-ttu-id="bc8cf-188">步骤 4： 在 FormView 中显示的产品信息</span><span class="sxs-lookup"><span data-stu-id="bc8cf-188">Step 4: Displaying the Product Information in a FormView</span></span>

<span data-ttu-id="bc8cf-189">添加到 FormView`CustomColors.aspx`页下的说明和设置其`ID`属性`LowStockedProductsInRed`。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-189">Add a FormView to the `CustomColors.aspx` page beneath the DetailsView and set its `ID` property to `LowStockedProductsInRed`.</span></span> <span data-ttu-id="bc8cf-190">将 FormView 绑定到上一步中创建的 ObjectDataSource 控件。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-190">Bind the FormView to the ObjectDataSource control created from the previous step.</span></span> <span data-ttu-id="bc8cf-191">这将创建`ItemTemplate`， `EditItemTemplate`，和`InsertItemTemplate`FormView 有关。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-191">This will create an `ItemTemplate`, `EditItemTemplate`, and `InsertItemTemplate` for the FormView.</span></span> <span data-ttu-id="bc8cf-192">删除`EditItemTemplate`和`InsertItemTemplate`并简化`ItemTemplate`包括只需`ProductName`和`UnitsInStock`值，每个自己带有相应名称的标签控件。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-192">Remove the `EditItemTemplate` and `InsertItemTemplate` and simplify the `ItemTemplate` to include just the `ProductName` and `UnitsInStock` values, each in their own appropriately-named Label controls.</span></span> <span data-ttu-id="bc8cf-193">与从之前的示例说明如何，还检查 FormView 的智能标记中的启用分页复选框。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-193">As with the DetailsView from the earlier example, also check the Enable Paging checkbox in the FormView's smart tag.</span></span>

<span data-ttu-id="bc8cf-194">后这些编辑你 FormView 标记应看起来类似于以下：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-194">After these edits your FormView's markup should look similar to the following:</span></span>


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample8.aspx)]

<span data-ttu-id="bc8cf-195">请注意，`ItemTemplate`包含：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-195">Note that the `ItemTemplate` contains:</span></span>

- <span data-ttu-id="bc8cf-196">**静态 HTML**文本"产品:"和"库存量:"连同`<br />`和`<b>`元素。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-196">**Static HTML** the text "Product:" and "Units In Stock:" along with the `<br />` and `<b>` elements.</span></span>
- <span data-ttu-id="bc8cf-197">**Web 控件**两个标签控件，`ProductNameLabel`和`UnitsInStockLabel`。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-197">**Web controls** the two Label controls, `ProductNameLabel` and `UnitsInStockLabel`.</span></span>
- <span data-ttu-id="bc8cf-198">**数据绑定语法**`<%# Bind("ProductName") %>`和`<%# Bind("UnitsInStock") %>`语法，将从这些字段的值分配给的标签控件的`Text`属性。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-198">**Databinding syntax** the `<%# Bind("ProductName") %>` and `<%# Bind("UnitsInStock") %>` syntax, which assigns the values from these fields to the Label controls' `Text` properties.</span></span>

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a><span data-ttu-id="bc8cf-199">步骤 5： 以编程方式确定数据绑定事件处理程序中的数据的值</span><span class="sxs-lookup"><span data-stu-id="bc8cf-199">Step 5: Programmatically Determining the Value of the Data in the DataBound Event Handler</span></span>

<span data-ttu-id="bc8cf-200">与完整的 FormView 的标记下, 一步是以编程方式确定如果`UnitsInStock`值是否小于或等于 10。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-200">With the FormView's markup complete, the next step is to programmatically determine if the `UnitsInStock` value is less than or equal to 10.</span></span> <span data-ttu-id="bc8cf-201">可以做到这一点与 FormView 完全相同的方式按照原样使用说明。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-201">This is accomplished in the exact same manner with the FormView as it was with the DetailsView.</span></span> <span data-ttu-id="bc8cf-202">首先为 FormView 创建事件处理程序`DataBound`事件。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-202">Start by creating an event handler for the FormView's `DataBound` event.</span></span>


![创建数据绑定事件处理程序](custom-formatting-based-upon-data-cs/_static/image14.png)

<span data-ttu-id="bc8cf-204">**图 6**： 创建`DataBound`事件处理程序</span><span class="sxs-lookup"><span data-stu-id="bc8cf-204">**Figure 6**: Create the `DataBound` Event Handler</span></span>


<span data-ttu-id="bc8cf-205">在事件处理程序强制转换 FormView`DataItem`属性`ProductsRow`实例，并确定是否`UnitsInPrice`值是，我们需要用红色字体显示。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-205">In the event handler cast the FormView's `DataItem` property to a `ProductsRow` instance and determine whether the `UnitsInPrice` value is such that we need to display it in a red font.</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample9.cs)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a><span data-ttu-id="bc8cf-206">步骤 6： 格式设置在 FormView ItemTemplate UnitsInStockLabel 标签控件</span><span class="sxs-lookup"><span data-stu-id="bc8cf-206">Step 6: Formatting the UnitsInStockLabel Label Control in the FormView's ItemTemplate</span></span>

<span data-ttu-id="bc8cf-207">最后一步是要设置格式显示`UnitsInStock`值以红色字体，如果值为 10 或更少。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-207">The final step is to format the displayed `UnitsInStock` value in a red font if the value is 10 or less.</span></span> <span data-ttu-id="bc8cf-208">若要完成此我们需要以编程方式访问`UnitsInStockLabel`中控制`ItemTemplate`并设置其样式属性，以便其文本显示为红色。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-208">To accomplish this we need to programmatically access the `UnitsInStockLabel` control in the `ItemTemplate` and set its style properties so that its text is displayed in red.</span></span> <span data-ttu-id="bc8cf-209">若要访问 Web 控件模板中的，使用`FindControl("controlID")`方法如下：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-209">To access a Web control in a template, use the `FindControl("controlID")` method like this:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample10.cs)]

<span data-ttu-id="bc8cf-210">对于我们的示例中我们想要访问一个标签来控制其`ID`值是`UnitsInStockLabel`，因此我们将使用：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-210">For our example we want to access a Label control whose `ID` value is `UnitsInStockLabel`, so we'd use:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample11.cs)]

<span data-ttu-id="bc8cf-211">一旦我们有了对 Web 控件的编程引用，我们可以根据需要修改其与样式有关的属性。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-211">Once we have a programmatic reference to the Web control, we can modify its style-related properties as needed.</span></span> <span data-ttu-id="bc8cf-212">如前面的示例中，我已创建中的 CSS 类`Styles.css`名为`LowUnitsInStockEmphasis`。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-212">As with the earlier example, I've created a CSS class in `Styles.css` named `LowUnitsInStockEmphasis`.</span></span> <span data-ttu-id="bc8cf-213">若要将此样式应用到标签 Web 控件，将设置其`CssClass`属性相应地。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-213">To apply this style to the Label Web control, set its `CssClass` property accordingly.</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="bc8cf-214">格式设置以编程方式访问 Web 控件使用的模板的语法`FindControl("controlID")`，然后设置其样式相关的属性还可使用时[TemplateFields](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx)中的说明或 GridView控件。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-214">The syntax for formatting a template programmatically accessing the Web control using `FindControl("controlID")` and then setting its style-related properties can also be used when using [TemplateFields](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) in the DetailsView or GridView controls.</span></span> <span data-ttu-id="bc8cf-215">在我们的下一步教程，我们将检查 TemplateFields。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-215">We'll examine TemplateFields in our next tutorial.</span></span>


<span data-ttu-id="bc8cf-216">图 7 显示 FormView 查看产品时其`UnitsInStock`图 8 中的产品获得它的值小于 10 时，值是大于 10。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-216">Figures 7 shows the FormView when viewing a product whose `UnitsInStock` value is greater than 10, while the product in Figure 8 has its value less than 10.</span></span>


<span data-ttu-id="bc8cf-217">[![对于产品与足够大 Units In Stock，无自定义格式设置将应用](custom-formatting-based-upon-data-cs/_static/image16.png)](custom-formatting-based-upon-data-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="bc8cf-217">[![For Products With a Sufficiently Large Units In Stock, No Custom Formatting is Applied](custom-formatting-based-upon-data-cs/_static/image16.png)](custom-formatting-based-upon-data-cs/_static/image15.png)</span></span>

<span data-ttu-id="bc8cf-218">**图 7**： 应用的产品与足够大 Units In Stock、 无自定义格式设置 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image17.png))</span><span class="sxs-lookup"><span data-stu-id="bc8cf-218">**Figure 7**: For Products With a Sufficiently Large Units In Stock, No Custom Formatting is Applied ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image17.png))</span></span>


<span data-ttu-id="bc8cf-219">[![在库存数量的单位以红色显示的那些产品包含值 10 或更少的](custom-formatting-based-upon-data-cs/_static/image19.png)](custom-formatting-based-upon-data-cs/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="bc8cf-219">[![The Units in Stock Number is Shown in Red for Those Products With Values of 10 or Less](custom-formatting-based-upon-data-cs/_static/image19.png)](custom-formatting-based-upon-data-cs/_static/image18.png)</span></span>

<span data-ttu-id="bc8cf-220">**图 8**： 内库存数量的设备以红色显示的那些产品使用的值小于或等于 10 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="bc8cf-220">**Figure 8**: The Units in Stock Number is Shown in Red for Those Products With Values of 10 or Less ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image20.png))</span></span>


## <a name="formatting-with-the-gridviewsrowdataboundevent"></a><span data-ttu-id="bc8cf-221">使用 GridView 的格式设置`RowDataBound`事件</span><span class="sxs-lookup"><span data-stu-id="bc8cf-221">Formatting with the GridView's`RowDataBound`Event</span></span>

<span data-ttu-id="bc8cf-222">前面我们检查的步骤说明如何顺序并 FormView 在数据绑定期间控制通过的进度。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-222">Earlier we examined the sequence of steps the DetailsView and FormView controls progress through during databinding.</span></span> <span data-ttu-id="bc8cf-223">让我们看通过这些步骤再一次作为刷新程序。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-223">Let's look over these steps once again as a refresher.</span></span>

1. <span data-ttu-id="bc8cf-224">数据的 Web 控件`DataBinding`事件激发。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-224">The data Web control's `DataBinding` event fires.</span></span>
2. <span data-ttu-id="bc8cf-225">数据绑定到 Web 控件的数据。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-225">The data is bound to the data Web control.</span></span>
3. <span data-ttu-id="bc8cf-226">数据的 Web 控件`DataBound`事件激发。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-226">The data Web control's `DataBound` event fires.</span></span>

<span data-ttu-id="bc8cf-227">这三个简单步骤的说明和 FormView 足以，因为它们将显示单个记录。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-227">These three simple steps are sufficient for the DetailsView and FormView because they display only a single record.</span></span> <span data-ttu-id="bc8cf-228">Gridview，它会显示*所有*记录绑定到它 （而不仅仅是第一个），步骤 2 非常有些复杂。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-228">For the GridView, which displays *all* records bound to it (not just the first), step 2 is a bit more involved.</span></span>

<span data-ttu-id="bc8cf-229">在步骤的 2 GridView 枚举数据源，并为每个记录，创建`GridViewRow`实例并将当前记录绑定到它。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-229">In step 2 the GridView enumerates the data source and, for each record, creates a `GridViewRow` instance and binds the current record to it.</span></span> <span data-ttu-id="bc8cf-230">每个`GridViewRow`添加到 GridView，会引发两个事件：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-230">For each `GridViewRow` added to the GridView, two events are raised:</span></span>

- <span data-ttu-id="bc8cf-231">**`RowCreated`**之后，将引发`GridViewRow`已创建</span><span class="sxs-lookup"><span data-stu-id="bc8cf-231">**`RowCreated`** fires after the `GridViewRow` has been created</span></span>
- <span data-ttu-id="bc8cf-232">**`RowDataBound`**当前记录已绑定到之后激发`GridViewRow`。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-232">**`RowDataBound`** fires after the current record has been bound to the `GridViewRow`.</span></span>

<span data-ttu-id="bc8cf-233">为 GridView，然后，数据绑定是更准确地由以下序列描述的步骤：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-233">For the GridView, then, data binding is more accurately described by the following sequence of steps:</span></span>

1. <span data-ttu-id="bc8cf-234">GridView`DataBinding`事件激发。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-234">The GridView's `DataBinding` event fires.</span></span>
2. <span data-ttu-id="bc8cf-235">将数据绑定到 GridView。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-235">The data is bound to the GridView.</span></span>   
  
 <span data-ttu-id="bc8cf-236">为数据源中的每个记录</span><span class="sxs-lookup"><span data-stu-id="bc8cf-236">For each record in the data source</span></span> 

    1. <span data-ttu-id="bc8cf-237">创建`GridViewRow`对象</span><span class="sxs-lookup"><span data-stu-id="bc8cf-237">Create a `GridViewRow` object</span></span>
    2. <span data-ttu-id="bc8cf-238">激发`RowCreated`事件</span><span class="sxs-lookup"><span data-stu-id="bc8cf-238">Fire the `RowCreated` event</span></span>
    3. <span data-ttu-id="bc8cf-239">将绑定到记录`GridViewRow`</span><span class="sxs-lookup"><span data-stu-id="bc8cf-239">Bind the record to the `GridViewRow`</span></span>
    4. <span data-ttu-id="bc8cf-240">激发`RowDataBound`事件</span><span class="sxs-lookup"><span data-stu-id="bc8cf-240">Fire the `RowDataBound` event</span></span>
    5. <span data-ttu-id="bc8cf-241">添加`GridViewRow`到`Rows`集合</span><span class="sxs-lookup"><span data-stu-id="bc8cf-241">Add the `GridViewRow` to the `Rows` collection</span></span>
3. <span data-ttu-id="bc8cf-242">GridView`DataBound`事件激发。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-242">The GridView's `DataBound` event fires.</span></span>

<span data-ttu-id="bc8cf-243">若要自定义的 GridView 的单个记录的格式，然后，我们需要创建的事件处理程序`RowDataBound`事件。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-243">To customize the format of the GridView's individual records, then, we need to create an event handler for the `RowDataBound` event.</span></span> <span data-ttu-id="bc8cf-244">若要说明这一点，让我们将添加到 GridView`CustomColors.aspx`页，其中列出名称、 类别和突出显示其价格是小于用黄色背景色 $10.00 这些产品的每个产品的价格。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-244">To illustrate this, let's add a GridView to the `CustomColors.aspx` page that lists the name, category, and price for each product, highlighting those products whose price is less than $10.00 with a yellow background color.</span></span>

## <a name="step-7-displaying-product-information-in-a-gridview"></a><span data-ttu-id="bc8cf-245">步骤 7： 在一个 GridView 中显示产品信息</span><span class="sxs-lookup"><span data-stu-id="bc8cf-245">Step 7: Displaying Product Information in a GridView</span></span>

<span data-ttu-id="bc8cf-246">添加上一示例中的下 FormView GridView，并设置其`ID`属性`HighlightCheapProducts`。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-246">Add a GridView beneath the FormView from the previous example and set its `ID` property to `HighlightCheapProducts`.</span></span> <span data-ttu-id="bc8cf-247">由于我们已有返回页的所有产品 ObjectDataSource，绑定到的 GridView。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-247">Since we already have an ObjectDataSource that returns all products on the page, bind the GridView to that.</span></span> <span data-ttu-id="bc8cf-248">最后，编辑 GridView BoundFields 包括只需产品的名称、 类别和价格。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-248">Finally, edit the GridView's BoundFields to include just the products' names, categories, and prices.</span></span> <span data-ttu-id="bc8cf-249">在这些编辑后 GridView 标记应如下所示：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-249">After these edits the GridView's markup should look like:</span></span>


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample13.aspx)]

<span data-ttu-id="bc8cf-250">图 9 显示我们到目前为止，通过浏览器查看时的进度。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-250">Figure 9 shows our progress to this point when viewed through a browser.</span></span>


<span data-ttu-id="bc8cf-251">[![GridView 列出名称、 类别和每个产品的价格](custom-formatting-based-upon-data-cs/_static/image22.png)](custom-formatting-based-upon-data-cs/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="bc8cf-251">[![The GridView Lists the Name, Category, and Price For Each Product](custom-formatting-based-upon-data-cs/_static/image22.png)](custom-formatting-based-upon-data-cs/_static/image21.png)</span></span>

<span data-ttu-id="bc8cf-252">**图 9**: GridView 列出名称、 类别和每个产品的价格 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image23.png))</span><span class="sxs-lookup"><span data-stu-id="bc8cf-252">**Figure 9**: The GridView Lists the Name, Category, and Price For Each Product ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image23.png))</span></span>


## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a><span data-ttu-id="bc8cf-253">步骤 8： 以编程方式确定 RowDataBound 事件处理程序中的数据的值</span><span class="sxs-lookup"><span data-stu-id="bc8cf-253">Step 8: Programmatically Determining the Value of the Data in the RowDataBound Event Handler</span></span>

<span data-ttu-id="bc8cf-254">当`ProductsDataTable`绑定到 GridView 其`ProductsRow`实例已枚举并为每个`ProductsRow``GridViewRow`创建。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-254">When the `ProductsDataTable` is bound to the GridView its `ProductsRow` instances are enumerated and for each `ProductsRow` a `GridViewRow` is created.</span></span> <span data-ttu-id="bc8cf-255">`GridViewRow`的`DataItem`属性分配给特定`ProductRow`，此后 GridView`RowDataBound`事件处理程序引发。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-255">The `GridViewRow`'s `DataItem` property is assigned to the particular `ProductRow`, after which the GridView's `RowDataBound` event handler is raised.</span></span> <span data-ttu-id="bc8cf-256">若要确定`UnitPrice`为每个产品的值绑定到 GridView，然后，我们需要创建一个事件处理程序为 GridView`RowDataBound`事件。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-256">To determine the `UnitPrice` value for each product bound to the GridView, then, we need to create an event handler for the GridView's `RowDataBound` event.</span></span> <span data-ttu-id="bc8cf-257">此事件处理程序中，我们可以检查`UnitPrice`当前值`GridViewRow`并且格式设置为该行决定。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-257">In this event handler we can inspect the `UnitPrice` value for the current `GridViewRow` and make a formatting decision for that row.</span></span>

<span data-ttu-id="bc8cf-258">可以使用相同的一系列步骤作为不带 FormView 和说明如何创建此事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-258">This event handler can be created using the same series of steps as with the FormView and DetailsView.</span></span>


![GridView RowDataBound 事件创建事件处理程序](custom-formatting-based-upon-data-cs/_static/image24.png)

<span data-ttu-id="bc8cf-260">**图 10**： 为 GridView 创建事件处理程序`RowDataBound`事件</span><span class="sxs-lookup"><span data-stu-id="bc8cf-260">**Figure 10**: Create an Event Handler for the GridView's `RowDataBound` Event</span></span>


<span data-ttu-id="bc8cf-261">在这种方式中创建的事件处理程序将导致下面的代码要自动添加到 ASP.NET 页的代码部分：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-261">Creating the event hander in this manner will cause the following code to be automatically added to the ASP.NET page's code portion:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample14.cs)]

<span data-ttu-id="bc8cf-262">当`RowDataBound`事件激发事件处理程序作为其第二个参数传递类型的对象`GridViewRowEventArgs`，其中有一个名为`Row`。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-262">When the `RowDataBound` event fires, the event handler is passed as its second parameter an object of type `GridViewRowEventArgs`, which has a property named `Row`.</span></span> <span data-ttu-id="bc8cf-263">此属性返回的引用`GridViewRow`已只是数据绑定。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-263">This property returns a reference to the `GridViewRow` that was just data bound.</span></span> <span data-ttu-id="bc8cf-264">访问`ProductsRow`实例绑定到`GridViewRow`我们使用`DataItem`属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-264">To access the `ProductsRow` instance bound to the `GridViewRow` we use the `DataItem` property like so:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample15.cs)]

<span data-ttu-id="bc8cf-265">使用时`RowDataBound`务必要记住 GridView 组成的行的不同类型，此事件针对激发的事件处理程序*所有*行类型。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-265">When working with the `RowDataBound` event handler it is important to keep in mind that the GridView is composed of different types of rows and that this event is fired for *all* row types.</span></span> <span data-ttu-id="bc8cf-266">A`GridViewRow`的类型可以由其`RowType`属性，并且可以具有可能的值之一：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-266">A `GridViewRow`'s type can be determined by its `RowType` property, and can have one of the possible values:</span></span>

- <span data-ttu-id="bc8cf-267">`DataRow`从 GridView 的绑定到一个记录行`DataSource`</span><span class="sxs-lookup"><span data-stu-id="bc8cf-267">`DataRow` a row that is bound to a record from the GridView's `DataSource`</span></span>
- <span data-ttu-id="bc8cf-268">`EmptyDataRow`如果显示的行 GridView`DataSource`为空</span><span class="sxs-lookup"><span data-stu-id="bc8cf-268">`EmptyDataRow` the row displayed if the GridView's `DataSource` is empty</span></span>
- <span data-ttu-id="bc8cf-269">`Footer`页脚行中;显示的如果 GridView`ShowFooter`属性设置为`true`</span><span class="sxs-lookup"><span data-stu-id="bc8cf-269">`Footer` the footer row; shown if the GridView's `ShowFooter` property is set to `true`</span></span>
- <span data-ttu-id="bc8cf-270">`Header`标头行中;显示是否 GridView ShowHeader 属性设置为`true`（默认值）</span><span class="sxs-lookup"><span data-stu-id="bc8cf-270">`Header` the header row; shown if the GridView's ShowHeader property is set to `true` (the default)</span></span>
- <span data-ttu-id="bc8cf-271">`Pager`GridView 的中，来实现分页，将显示分页接口的行</span><span class="sxs-lookup"><span data-stu-id="bc8cf-271">`Pager` for GridView's that implement paging, the row that displays the paging interface</span></span>
- <span data-ttu-id="bc8cf-272">`Separator`不用于 GridView，但使用`RowType`DataList 和转发器的属性控制，两个数据，我们将讨论在将来教程的 Web 控件</span><span class="sxs-lookup"><span data-stu-id="bc8cf-272">`Separator` not used for the GridView, but used by the `RowType` properties for the DataList and Repeater controls, two data Web controls we'll discuss in future tutorials</span></span>

<span data-ttu-id="bc8cf-273">由于`EmptyDataRow`， `Header`， `Footer`，和`Pager`行不与关联`DataSource`记录，它们将始终具有`null`值，则为其`DataItem`属性。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-273">Since the `EmptyDataRow`, `Header`, `Footer`, and `Pager` rows aren't associated with a `DataSource` record, they will always have a `null` value for their `DataItem` property.</span></span> <span data-ttu-id="bc8cf-274">出于此原因，然后再尝试处理当前`GridViewRow`的`DataItem`属性，我们首先必须确保我们正在处理与`DataRow`。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-274">For this reason, before attempting to work with the current `GridViewRow`'s `DataItem` property, we first must make sure that we're dealing with a `DataRow`.</span></span> <span data-ttu-id="bc8cf-275">这可以通过检查来实现`GridViewRow`的`RowType`属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-275">This can be accomplished by checking the `GridViewRow`'s `RowType` property like so:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample16.cs)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a><span data-ttu-id="bc8cf-276">步骤 9： 突出显示行黄色时 UnitPrice 值是小于 $10.00</span><span class="sxs-lookup"><span data-stu-id="bc8cf-276">Step 9: Highlighting the Row Yellow When the UnitPrice Value is Less than $10.00</span></span>

<span data-ttu-id="bc8cf-277">最后一步是以编程方式突出显示整个`GridViewRow`如果`UnitPrice`值该行是小于 $10.00。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-277">The last step is to programmatically highlight the entire `GridViewRow` if the `UnitPrice` value for that row is less than $10.00.</span></span> <span data-ttu-id="bc8cf-278">访问一个 GridView 行或单元格的语法是说明如何与相同`GridViewID.Rows[index]`访问整行，`GridViewID.Rows[index].Cells[index]`访问特定的单元格。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-278">The syntax for accessing a GridView's rows or cells is the same as with the DetailsView `GridViewID.Rows[index]` to access the entire row, `GridViewID.Rows[index].Cells[index]` to access a particular cell.</span></span> <span data-ttu-id="bc8cf-279">但是，当`RowDataBound`事件处理程序，将引发绑定数据`GridViewRow`中尚未添加到的 GridView`Rows`集合。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-279">However, when the `RowDataBound` event handler fires the data bound `GridViewRow` has yet to be added to the GridView's `Rows` collection.</span></span> <span data-ttu-id="bc8cf-280">因此无法访问当前`GridViewRow`实例从`RowDataBound`事件处理程序使用的行集合。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-280">Therefore you cannot access the current `GridViewRow` instance from the `RowDataBound` event handler using the Rows collection.</span></span>

<span data-ttu-id="bc8cf-281">而不是`GridViewID.Rows[index]`，我们可以引用当前`GridViewRow`实例中`RowDataBound`事件处理程序使用`e.Row`。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-281">Instead of `GridViewID.Rows[index]`, we can reference the current `GridViewRow` instance in the `RowDataBound` event handler using `e.Row`.</span></span> <span data-ttu-id="bc8cf-282">即，按顺序，以突出显示当前`GridViewRow`实例从`RowDataBound`我们将使用的事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-282">That is, in order to highlight the current `GridViewRow` instance from the `RowDataBound` event handler we would use:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample17.cs)]

<span data-ttu-id="bc8cf-283">而不是设置`GridViewRow`的`BackColor`属性直接，让我们只讨论与使用 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-283">Rather than set the `GridViewRow`'s `BackColor` property directly, let's stick with using CSS classes.</span></span> <span data-ttu-id="bc8cf-284">我已创建一个名为的 CSS 类`AffordablePriceEmphasis`，将背景色设置为黄色。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-284">I've created a CSS class named `AffordablePriceEmphasis` that sets the background color to yellow.</span></span> <span data-ttu-id="bc8cf-285">已完成`RowDataBound`事件处理程序遵循：</span><span class="sxs-lookup"><span data-stu-id="bc8cf-285">The completed `RowDataBound` event handler follows:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample18.cs)]


<span data-ttu-id="bc8cf-286">[![最经济的产品是黄色突出显示](custom-formatting-based-upon-data-cs/_static/image26.png)](custom-formatting-based-upon-data-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="bc8cf-286">[![The Most Affordable Products are Highlighted Yellow](custom-formatting-based-upon-data-cs/_static/image26.png)](custom-formatting-based-upon-data-cs/_static/image25.png)</span></span>

<span data-ttu-id="bc8cf-287">**图 11**： 最经济的产品是突出显示黄色 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="bc8cf-287">**Figure 11**: The Most Affordable Products are Highlighted Yellow ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image27.png))</span></span>


## <a name="summary"></a><span data-ttu-id="bc8cf-288">摘要</span><span class="sxs-lookup"><span data-stu-id="bc8cf-288">Summary</span></span>

<span data-ttu-id="bc8cf-289">在本教程中我们已了解如何设置 GridView，说明如何和 FormView 在基于绑定到控件的数据的格式。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-289">In this tutorial we saw how to format the GridView, DetailsView, and FormView based on the data bound to the control.</span></span> <span data-ttu-id="bc8cf-290">若要完成此我们创建的事件处理程序`DataBound`或`RowDataBound`事件，如果需要格式设置的更改，以及检查基础数据已其中。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-290">To accomplish this we created an event handler for the `DataBound` or `RowDataBound` events, where the underlying data was examined along with a formatting change, if needed.</span></span> <span data-ttu-id="bc8cf-291">若要访问的数据绑定到一个说明如何或 FormView，我们使用`DataItem`中的属性`DataBound`事件处理程序; 对于一个 GridView，每个`GridViewRow`实例的`DataItem`属性包含绑定到该行，即在中可用的数据`RowDataBound`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-291">To access the data bound to a DetailsView or FormView, we use the `DataItem` property in the `DataBound` event handler; for a GridView, each `GridViewRow` instance's `DataItem` property contains the data bound to that row, which is available in the `RowDataBound` event handler.</span></span>

<span data-ttu-id="bc8cf-292">以编程方式调整数据 Web 控件的格式设置的语法取决于 Web 控件和要设置格式的数据的显示方式。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-292">The syntax for programmatically adjusting the data Web control's formatting depends upon the Web control and how the data to be formatted is displayed.</span></span> <span data-ttu-id="bc8cf-293">说明如何和 GridView 控件、 行和单元格可以访问由的序号索引。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-293">For DetailsView and GridView controls, the rows and cells can be accessed by an ordinal index.</span></span> <span data-ttu-id="bc8cf-294">有关说明，使用模板，`FindControl("controlID")`方法通常用于查找 Web 控件从模板中的。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-294">For the FormView, which uses templates, the `FindControl("controlID")` method is commonly used to locate a Web control from within the template.</span></span>

<span data-ttu-id="bc8cf-295">在下一教程中我们将查看如何使用 GridView 和说明如何使用模板。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-295">In the next tutorial we'll look at how to use templates with the GridView and DetailsView.</span></span> <span data-ttu-id="bc8cf-296">此外，我们将看到另一种自定义基于基础数据的格式设置的方法。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-296">Additionally, we'll see another technique for customizing the formatting based on the underlying data.</span></span>

<span data-ttu-id="bc8cf-297">尽情享受编程 ！</span><span class="sxs-lookup"><span data-stu-id="bc8cf-297">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="bc8cf-298">关于作者</span><span class="sxs-lookup"><span data-stu-id="bc8cf-298">About the Author</span></span>

<span data-ttu-id="bc8cf-299">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的七个 ASP/ASP.NET 书籍和的创始人[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年使用与 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-299">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="bc8cf-300">Scott 的作用是作为独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-300">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="bc8cf-301">最新书籍是[ *Sam 教授自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-301">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="bc8cf-302">他可以达到在[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)或通过他的博客，其中可以找到在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-302">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="bc8cf-303">特别感谢</span><span class="sxs-lookup"><span data-stu-id="bc8cf-303">Special Thanks To</span></span>

<span data-ttu-id="bc8cf-304">本教程系列已由许多有用的审阅者评审。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-304">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="bc8cf-305">本教程中的前导审阅者已 E.R.</span><span class="sxs-lookup"><span data-stu-id="bc8cf-305">Lead reviewers for this tutorial were E.R.</span></span> <span data-ttu-id="bc8cf-306">Gilmore，Dennis Patterson 和 Dan Jagers。</span><span class="sxs-lookup"><span data-stu-id="bc8cf-306">Gilmore, Dennis Patterson, and Dan Jagers.</span></span> <span data-ttu-id="bc8cf-307">对感兴趣查看我即将到来的 MSDN 文章？</span><span class="sxs-lookup"><span data-stu-id="bc8cf-307">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="bc8cf-308">如果是这样，删除我一行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="bc8cf-308">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="bc8cf-309">下一篇</span><span class="sxs-lookup"><span data-stu-id="bc8cf-309">Next</span></span>](using-templatefields-in-the-gridview-control-cs.md)
