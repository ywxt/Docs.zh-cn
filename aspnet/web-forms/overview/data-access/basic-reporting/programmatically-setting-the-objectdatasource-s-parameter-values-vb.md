---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
title: 以编程方式设置 ObjectDataSource 的参数值 (VB) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将介绍方法添加到我们的 DAL 和 BLL 接受一个输入的参数并返回数据。 该示例将设置此参数...
ms.author: aspnetcontent
ms.date: 03/31/2010
ms.assetid: 0ecb03b6-52a0-4731-8c7a-436391d36838
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
msc.type: authoredcontent
ms.openlocfilehash: d779de4f5bd0d03f413237689e5a64330fcb491d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825777"
---
<a name="programmatically-setting-the-objectdatasources-parameter-values-vb"></a><span data-ttu-id="c84b0-104">以编程方式设置 ObjectDataSource 的参数值 (VB)</span><span class="sxs-lookup"><span data-stu-id="c84b0-104">Programmatically Setting the ObjectDataSource's Parameter Values (VB)</span></span>
====================
<span data-ttu-id="c84b0-105">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="c84b0-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="c84b0-106">[下载示例应用程序](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_6_VB.exe)或[下载 PDF](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/datatutorial06vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="c84b0-106">[Download Sample App](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_6_VB.exe) or [Download PDF](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/datatutorial06vb1.pdf)</span></span>

> <span data-ttu-id="c84b0-107">在本教程中我们将介绍方法添加到我们的 DAL 和 BLL 接受一个输入的参数并返回数据。</span><span class="sxs-lookup"><span data-stu-id="c84b0-107">In this tutorial we'll look at adding a method to our DAL and BLL that accepts a single input parameter and returns data.</span></span> <span data-ttu-id="c84b0-108">该示例将以编程方式设置此参数。</span><span class="sxs-lookup"><span data-stu-id="c84b0-108">The example will set this parameter programmatically.</span></span>


## <a name="introduction"></a><span data-ttu-id="c84b0-109">介绍</span><span class="sxs-lookup"><span data-stu-id="c84b0-109">Introduction</span></span>

<span data-ttu-id="c84b0-110">中可以看到[前一篇教程](declarative-parameters-vb.md)，有多种选项都是可用于以声明方式将参数值传递给 ObjectDataSource 的方法。</span><span class="sxs-lookup"><span data-stu-id="c84b0-110">As we saw in the [previous tutorial](declarative-parameters-vb.md), a number of options are available for declaratively passing parameter values to the ObjectDataSource's methods.</span></span> <span data-ttu-id="c84b0-111">如果参数值为硬编码，来自 Web 控件在页上，或者由数据源是可读的任何其他源中`Parameter`对象，例如，值绑定到输入参数上，而无需编写一行代码。</span><span class="sxs-lookup"><span data-stu-id="c84b0-111">If the parameter value is hard-coded, comes from a Web control on the page, or is in any other source that is readable by a data source `Parameter` object, for example, that value can be bound to the input parameter without writing a line of code.</span></span>

<span data-ttu-id="c84b0-112">但是，有时时参数值来自某些源由一个内置数据源已不计`Parameter`对象。</span><span class="sxs-lookup"><span data-stu-id="c84b0-112">There may be times, however, when the parameter value comes from some source not already accounted for by one of the built-in data source `Parameter` objects.</span></span> <span data-ttu-id="c84b0-113">如果我们的站点支持的用户帐户我们可能想要设置参数基于当前登录的访问者的用户 id。</span><span class="sxs-lookup"><span data-stu-id="c84b0-113">If our site supported user accounts we might want to set the parameter based on the currently logged in visitor's User ID.</span></span> <span data-ttu-id="c84b0-114">或者，我们可能需要先将其发送到 ObjectDataSource 的基础对象的方法自定义参数值。</span><span class="sxs-lookup"><span data-stu-id="c84b0-114">Or we may need to customize the parameter value before sending it along to the ObjectDataSource's underlying object's method.</span></span>

<span data-ttu-id="c84b0-115">每当 ObjectDataSource`Select`方法调用 ObjectDataSource 首先引发其[选择事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c84b0-115">Whenever the ObjectDataSource's `Select` method is invoked the ObjectDataSource first raises its [Selecting event](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx).</span></span> <span data-ttu-id="c84b0-116">然后调用 ObjectDataSource 的基础对象的方法。</span><span class="sxs-lookup"><span data-stu-id="c84b0-116">The ObjectDataSource's underlying object's method is then invoked.</span></span> <span data-ttu-id="c84b0-117">该操作完成 ObjectDataSource 的后[选定事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx)激发 （图 1 展示了这一序列的事件）。</span><span class="sxs-lookup"><span data-stu-id="c84b0-117">Once that completes the ObjectDataSource's [Selected event](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx) fires (Figure 1 illustrates this sequence of events).</span></span> <span data-ttu-id="c84b0-118">传递到 ObjectDataSource 的基础对象的方法的参数值可设置或自定义的事件处理程序中`Selecting`事件。</span><span class="sxs-lookup"><span data-stu-id="c84b0-118">The parameter values passed into the ObjectDataSource's underlying object's method can be set or customized in an event handler for the `Selecting` event.</span></span>


<span data-ttu-id="c84b0-119">[![ObjectDataSource 的选中和选择事件触发之前和之后及其基础对象的方法被调用](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c84b0-119">[![The ObjectDataSource's Selected and Selecting Events Fire Before and After Its Underlying Object's Method is Invoked](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image1.png)</span></span>

<span data-ttu-id="c84b0-120">**图 1**: ObjectDataSource`Selected`并`Selecting`调用事件触发之前和之后及其基础对象的方法 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c84b0-120">**Figure 1**: The ObjectDataSource's `Selected` and `Selecting` Events Fire Before and After Its Underlying Object's Method is Invoked ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image3.png))</span></span>


<span data-ttu-id="c84b0-121">在本教程中我们将介绍方法添加到我们的 DAL 和接受一个输入的参数的 BLL `Month`，类型的`Integer`，并返回`EmployeesDataTable`填入这些员工将其招聘周年中指定的对象`Month`.</span><span class="sxs-lookup"><span data-stu-id="c84b0-121">In this tutorial we'll look at adding a method to our DAL and BLL that accepts a single input parameter `Month`, of type `Integer` and returns an `EmployeesDataTable` object populated with those employees that have their hiring anniversary in the specified `Month`.</span></span> <span data-ttu-id="c84b0-122">我们的示例将设置此参数以编程方式基于当前月的上显示一系列"员工周年纪念日本月。"</span><span class="sxs-lookup"><span data-stu-id="c84b0-122">Our example will set this parameter programmatically based on the current month, showing a list of "Employee Anniversaries This Month."</span></span>

<span data-ttu-id="c84b0-123">让我们进入正题！</span><span class="sxs-lookup"><span data-stu-id="c84b0-123">Let's get started!</span></span>

## <a name="step-1-adding-a-method-toemployeestableadapter"></a><span data-ttu-id="c84b0-124">步骤 1： 添加到方法`EmployeesTableAdapter`</span><span class="sxs-lookup"><span data-stu-id="c84b0-124">Step 1: Adding a Method to`EmployeesTableAdapter`</span></span>

<span data-ttu-id="c84b0-125">对于我们的第一个示例中我们需要添加一种方法来检索这些员工其`HireDate`发生在指定月份中。</span><span class="sxs-lookup"><span data-stu-id="c84b0-125">For our first example we need to add a means to retrieve those employees whose `HireDate` occurred in a specified month.</span></span> <span data-ttu-id="c84b0-126">若要提供此功能根据我们需要首先创建中的方法的体系结构`EmployeesTableAdapter`，它映射到正确的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="c84b0-126">To provide this functionality in accordance with our architecture we need to first create a method in `EmployeesTableAdapter` that maps to the proper SQL statement.</span></span> <span data-ttu-id="c84b0-127">若要完成此操作，先打开 Northwind 类型化数据集。</span><span class="sxs-lookup"><span data-stu-id="c84b0-127">To accomplish this, start by opening the Northwind Typed DataSet.</span></span> <span data-ttu-id="c84b0-128">右键单击`EmployeesTableAdapter`标签，然后选择添加查询。</span><span class="sxs-lookup"><span data-stu-id="c84b0-128">Right-click on the `EmployeesTableAdapter` label and choose Add Query.</span></span>


<span data-ttu-id="c84b0-129">[![将一个新查询添加到 EmployeesTableAdapter](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c84b0-129">[![Add a New Query to the EmployeesTableAdapter](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image4.png)</span></span>

<span data-ttu-id="c84b0-130">**图 2**： 添加到一个新查询`EmployeesTableAdapter`([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="c84b0-130">**Figure 2**: Add a New Query to the `EmployeesTableAdapter` ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image6.png))</span></span>


<span data-ttu-id="c84b0-131">选择要添加将返回行的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="c84b0-131">Choose to add a SQL statement that returns rows.</span></span> <span data-ttu-id="c84b0-132">在访问指定`SELECT`语句屏幕上的默认值`SELECT`语句`EmployeesTableAdapter`将加载。</span><span class="sxs-lookup"><span data-stu-id="c84b0-132">When you reach the Specify a `SELECT` Statement screen the default `SELECT` statement for the `EmployeesTableAdapter` will already be loaded.</span></span> <span data-ttu-id="c84b0-133">只需在中添加`WHERE`子句： `WHERE DATEPART(m, HireDate) = @Month`。</span><span class="sxs-lookup"><span data-stu-id="c84b0-133">Simply add in the `WHERE` clause: `WHERE DATEPART(m, HireDate) = @Month`.</span></span> <span data-ttu-id="c84b0-134">[DATEPART](https://msdn.microsoft.com/library/ms174420.aspx)是返回特定日期的一部分的 T-SQL 函数`datetime`类型; 我们使用这种情况下`DATEPART`返回的月份`HireDate`列。</span><span class="sxs-lookup"><span data-stu-id="c84b0-134">[DATEPART](https://msdn.microsoft.com/library/ms174420.aspx) is a T-SQL function that returns a particular date portion of a `datetime` type; in this case we're using `DATEPART` to return the month of the `HireDate` column.</span></span>


<span data-ttu-id="c84b0-135">[![返回仅这些行位置的 HireDate 列是否小于或等于@HiredBeforeDate参数](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c84b0-135">[![Return Only Those Rows Where the HireDate Column is Less Than or Equal to the @HiredBeforeDate Parameter](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image7.png)</span></span>

<span data-ttu-id="c84b0-136">**图 3**： 返回仅这些行位置`HireDate`列是否小于或等于`@HiredBeforeDate`参数 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="c84b0-136">**Figure 3**: Return Only Those Rows Where the `HireDate` Column is Less Than or Equal to the `@HiredBeforeDate` Parameter ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image9.png))</span></span>


<span data-ttu-id="c84b0-137">最后，更改`FillBy`并`GetDataBy`方法的名称到`FillByHiredDateMonth`和`GetEmployeesByHiredDateMonth`分别。</span><span class="sxs-lookup"><span data-stu-id="c84b0-137">Finally, change the `FillBy` and `GetDataBy` method names to `FillByHiredDateMonth` and `GetEmployeesByHiredDateMonth`, respectively.</span></span>


<span data-ttu-id="c84b0-138">[![选择比 FillBy 和 GetDataBy 更合适的方法名称](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="c84b0-138">[![Choose More Appropriate Method Names Than FillBy and GetDataBy](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image10.png)</span></span>

<span data-ttu-id="c84b0-139">**图 4**： 选择更适当方法的名称比`FillBy`并`GetDataBy`([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="c84b0-139">**Figure 4**: Choose More Appropriate Method Names Than `FillBy` and `GetDataBy` ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image12.png))</span></span>


<span data-ttu-id="c84b0-140">单击完成以完成向导并返回到数据集的设计图面上。</span><span class="sxs-lookup"><span data-stu-id="c84b0-140">Click Finish to complete the wizard and return to the DataSet's design surface.</span></span> <span data-ttu-id="c84b0-141">`EmployeesTableAdapter`现在应包含一组新的用于访问在指定月份中雇用的员工的方法。</span><span class="sxs-lookup"><span data-stu-id="c84b0-141">The `EmployeesTableAdapter` should now include a new set of methods for accessing employees hired in a specified month.</span></span>


<span data-ttu-id="c84b0-142">[![在数据集的设计图面上显示的新方法](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="c84b0-142">[![The New Methods Appear in the DataSet's Design Surface](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image13.png)</span></span>

<span data-ttu-id="c84b0-143">**图 5**: 新方法出现在数据集的设计图面上 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="c84b0-143">**Figure 5**: The New Methods Appear in the DataSet's Design Surface ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image15.png))</span></span>


## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a><span data-ttu-id="c84b0-144">步骤 2： 添加`GetEmployeesByHiredDateMonth(month)`业务逻辑层方法</span><span class="sxs-lookup"><span data-stu-id="c84b0-144">Step 2: Adding the`GetEmployeesByHiredDateMonth(month)`Method to the Business Logic Layer</span></span>

<span data-ttu-id="c84b0-145">由于我们应用程序体系结构用于单独层业务逻辑和数据访问逻辑，我们需要将方法添加到 DAL 的调用来检索雇员雇佣在指定日期前我们 BLL。</span><span class="sxs-lookup"><span data-stu-id="c84b0-145">Since our application architecture uses a separate layer for the business logic and data access logic, we need to add a method to our BLL that calls down to the DAL to retrieve employees hired before a specified date.</span></span> <span data-ttu-id="c84b0-146">打开`EmployeesBLL.vb`文件，并添加以下方法：</span><span class="sxs-lookup"><span data-stu-id="c84b0-146">Open the `EmployeesBLL.vb` file and add the following method:</span></span>


[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample1.vb)]

<span data-ttu-id="c84b0-147">与我们在此类中的其他方法一样`GetEmployeesByHiredDateMonth(month)`只需调用 DAL 并返回结果。</span><span class="sxs-lookup"><span data-stu-id="c84b0-147">As with our other methods in this class, `GetEmployeesByHiredDateMonth(month)` simply calls down into the DAL and returns the results.</span></span>

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a><span data-ttu-id="c84b0-148">步骤 3： 显示其招聘周年日是这个月的员工</span><span class="sxs-lookup"><span data-stu-id="c84b0-148">Step 3: Displaying Employees Whose Hiring Anniversary Is This Month</span></span>

<span data-ttu-id="c84b0-149">此示例中我们最后一步是要显示其招聘周年日是这个月的员工。</span><span class="sxs-lookup"><span data-stu-id="c84b0-149">Our final step for this example is to display those employees whose hiring anniversary is this month.</span></span> <span data-ttu-id="c84b0-150">首先，通过添加到 GridView`ProgrammaticParams.aspx`页中`BasicReporting`文件夹并将新对象数据源添加为其数据源。</span><span class="sxs-lookup"><span data-stu-id="c84b0-150">Start by adding a GridView to the `ProgrammaticParams.aspx` page in the `BasicReporting` folder and add a new ObjectDataSource as its data source.</span></span> <span data-ttu-id="c84b0-151">配置要使用 ObjectDataSource`EmployeesBLL`类的`SelectMethod`设置为`GetEmployeesByHiredDateMonth(month)`。</span><span class="sxs-lookup"><span data-stu-id="c84b0-151">Configure the ObjectDataSource to use the `EmployeesBLL` class with the `SelectMethod` set to `GetEmployeesByHiredDateMonth(month)`.</span></span>


<span data-ttu-id="c84b0-152">[![使用 EmployeesBLL 类](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="c84b0-152">[![Use the EmployeesBLL Class](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image16.png)</span></span>

<span data-ttu-id="c84b0-153">**图 6**： 使用`EmployeesBLL`类 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="c84b0-153">**Figure 6**: Use the `EmployeesBLL` Class ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image18.png))</span></span>


<span data-ttu-id="c84b0-154">[![选择从 GetEmployeesByHiredDateMonth(month) 方法](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="c84b0-154">[![Select From the GetEmployeesByHiredDateMonth(month) method](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image19.png)</span></span>

<span data-ttu-id="c84b0-155">**图 7**: Select From`GetEmployeesByHiredDateMonth(month)`方法 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="c84b0-155">**Figure 7**: Select From the `GetEmployeesByHiredDateMonth(month)` method ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image21.png))</span></span>


<span data-ttu-id="c84b0-156">最后一个屏幕询问我们提供`month`参数值的源。</span><span class="sxs-lookup"><span data-stu-id="c84b0-156">The final screen asks us to provide the `month` parameter value's source.</span></span> <span data-ttu-id="c84b0-157">由于我们将以编程方式设置此值，将保留参数源设置为默认值 None 选项，然后单击完成。</span><span class="sxs-lookup"><span data-stu-id="c84b0-157">Since we'll set this value programmatically, leave the Parameter source set to the default None option and click Finish.</span></span>


<span data-ttu-id="c84b0-158">[![将参数源设置为 None](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="c84b0-158">[![Leave the Parameter Source Set to None](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image22.png)</span></span>

<span data-ttu-id="c84b0-159">**图 8**： 将保留为无设置参数源 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="c84b0-159">**Figure 8**: Leave the Parameter Source Set to None ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image24.png))</span></span>


<span data-ttu-id="c84b0-160">这将创建`Parameter`对象中的 ObjectDataSource`SelectParameters`不具有指定的值的集合。</span><span class="sxs-lookup"><span data-stu-id="c84b0-160">This will create a `Parameter` object in the ObjectDataSource's `SelectParameters` collection that does not have a value specified.</span></span>


[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample2.aspx)]

<span data-ttu-id="c84b0-161">若要以编程方式设置此值，我们需要为 ObjectDataSource 的创建事件处理程序`Selecting`事件。</span><span class="sxs-lookup"><span data-stu-id="c84b0-161">To set this value programmatically, we need to create an event handler for the ObjectDataSource's `Selecting` event.</span></span> <span data-ttu-id="c84b0-162">若要实现此目的，请转到设计视图，并双击 ObjectDataSource。</span><span class="sxs-lookup"><span data-stu-id="c84b0-162">To accomplish this, go to the Design view and double-click the ObjectDataSource.</span></span> <span data-ttu-id="c84b0-163">或者，选择 ObjectDataSource 中，转到属性窗口中，并单击闪电形图标。</span><span class="sxs-lookup"><span data-stu-id="c84b0-163">Alternatively, select the ObjectDataSource, go to the Properties window, and click the lightning bolt icon.</span></span> <span data-ttu-id="c84b0-164">接下来，可以双击在文本框旁边`Selecting`事件或键入你想要使用的事件处理程序的名称。</span><span class="sxs-lookup"><span data-stu-id="c84b0-164">Next, either double-click in the textbox next to the `Selecting` event or type in the name of the event handler you want to use.</span></span> <span data-ttu-id="c84b0-165">如第三个选项，可以通过选择 ObjectDataSource 创建事件处理程序并将其`Selecting`页面的代码隐藏类顶部的两个下拉列表中的事件。</span><span class="sxs-lookup"><span data-stu-id="c84b0-165">As a third option, you can create the event handler by selecting the ObjectDataSource and its `Selecting` event from the two drop-down lists at the top of the page's code-behind class.</span></span>


![单击属性窗口列出 Web 控件的事件中的闪电形图标](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image25.png)

<span data-ttu-id="c84b0-167">**图 9**： 单击属性窗口列出 Web 控件的事件中的闪电形图标</span><span class="sxs-lookup"><span data-stu-id="c84b0-167">**Figure 9**: Click on the Lightning Bolt Icon in the Properties Window to List a Web Control's Events</span></span>


<span data-ttu-id="c84b0-168">所有这三种方法将新的事件处理程序添加了 ObjectDataSource 的`Selecting`到页面的代码隐藏类的事件。</span><span class="sxs-lookup"><span data-stu-id="c84b0-168">All three approaches add a new event handler for the ObjectDataSource's `Selecting` event to the page's code-behind class.</span></span> <span data-ttu-id="c84b0-169">此事件处理程序中我们可以读取和写入到使用的参数值`e.InputParameters(parameterName)`，其中*`parameterName`* 的值`Name`属性中`<asp:Parameter>`标记 (`InputParameters`也可以是集合索引作为中序号， `e.InputParameters(index)`)。</span><span class="sxs-lookup"><span data-stu-id="c84b0-169">In this event handler we can read and write to the parameter values using `e.InputParameters(parameterName)`, where *`parameterName`* is the value of the `Name` attribute in the `<asp:Parameter>` tag (the `InputParameters` collection can also be indexed ordinally, as in `e.InputParameters(index)`).</span></span> <span data-ttu-id="c84b0-170">若要设置`month`当前月份，参数添加到以下`Selecting`事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="c84b0-170">To set the `month` parameter to the current month, add the following to the `Selecting` event handler:</span></span>


[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample3.vb)]

<span data-ttu-id="c84b0-171">访问此页上的通过浏览器时，我们可以看到该只有一个雇员雇佣的这个月 （年 3 月） Laura Callahan，已在公司自 1994 年。</span><span class="sxs-lookup"><span data-stu-id="c84b0-171">When visiting this page through a browser we can see that only one employee was hired this month (March) Laura Callahan, who's been with the company since 1994.</span></span>


<span data-ttu-id="c84b0-172">[![这个月显示其周年纪念日这些员工](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image26.png)</span><span class="sxs-lookup"><span data-stu-id="c84b0-172">[![Those Employees Whose Anniversaries This Month Are Shown](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image26.png)</span></span>

<span data-ttu-id="c84b0-173">**图 10**： 这些员工其周年纪念日此月显示 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image28.png))</span><span class="sxs-lookup"><span data-stu-id="c84b0-173">**Figure 10**: Those Employees Whose Anniversaries This Month Are Shown ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image28.png))</span></span>


## <a name="summary"></a><span data-ttu-id="c84b0-174">总结</span><span class="sxs-lookup"><span data-stu-id="c84b0-174">Summary</span></span>

<span data-ttu-id="c84b0-175">虽然 ObjectDataSource 的参数值通常可以设置以声明方式，而无需一行代码，很容易地以编程方式设置参数值。</span><span class="sxs-lookup"><span data-stu-id="c84b0-175">While the ObjectDataSource's parameters' values can typically be set declaratively, without requiring a line of code, it's easy to set the parameter values programmatically.</span></span> <span data-ttu-id="c84b0-176">我们需要做的就是为 ObjectDataSource 的创建事件处理程序`Selecting`触发的事件，基础对象的方法是调用，并手动设置为通过一个或多个参数的值之前`InputParameters`集合。</span><span class="sxs-lookup"><span data-stu-id="c84b0-176">All we need to do is create an event handler for the ObjectDataSource's `Selecting` event, which fires before the underlying object's method is invoked, and manually set the values for one or more parameters via the `InputParameters` collection.</span></span>

<span data-ttu-id="c84b0-177">基本报告部分到本教程结束。</span><span class="sxs-lookup"><span data-stu-id="c84b0-177">This tutorial concludes the Basic Reporting section.</span></span> <span data-ttu-id="c84b0-178">[下一教程](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md)开始为期筛选和母版-详细信息方案部分，我们将介绍的技术允许筛选数据的访问者并从主报表深化到详细信息报表。</span><span class="sxs-lookup"><span data-stu-id="c84b0-178">The [next tutorial](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) kicks off the Filtering and Master-Details Scenarios section, in which we'll look at techniques for allowing the visitor to filter data and drill down from a master report into a details report.</span></span>

<span data-ttu-id="c84b0-179">快乐编程 ！</span><span class="sxs-lookup"><span data-stu-id="c84b0-179">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="c84b0-180">关于作者</span><span class="sxs-lookup"><span data-stu-id="c84b0-180">About the Author</span></span>

<span data-ttu-id="c84b0-181">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="c84b0-181">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="c84b0-182">Scott 是独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="c84b0-182">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="c84b0-183">他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="c84b0-183">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="c84b0-184">他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="c84b0-184">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="c84b0-185">或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="c84b0-185">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="c84b0-186">特别感谢</span><span class="sxs-lookup"><span data-stu-id="c84b0-186">Special Thanks To</span></span>

<span data-ttu-id="c84b0-187">很多有用的审阅者已评审本系列教程。</span><span class="sxs-lookup"><span data-stu-id="c84b0-187">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="c84b0-188">本教程中的潜在顾客审阅者是 Hilton Giesenow。</span><span class="sxs-lookup"><span data-stu-id="c84b0-188">Lead reviewer for this tutorial was Hilton Giesenow.</span></span> <span data-ttu-id="c84b0-189">是否有兴趣查看我即将推出的 MSDN 文章？</span><span class="sxs-lookup"><span data-stu-id="c84b0-189">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="c84b0-190">如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="c84b0-190">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c84b0-191">上一篇</span><span class="sxs-lookup"><span data-stu-id="c84b0-191">Previous</span></span>](declarative-parameters-vb.md)
