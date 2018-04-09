---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
title: 以编程方式设置对象数据源的参数值 (VB) |Microsoft 文档
author: rick-anderson
description: 在本教程中我们将查看将方法添加到我们的 DAL 和 BLL 接受一个输入的参数并返回数据。 该示例会将此参数设置...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 0ecb03b6-52a0-4731-8c7a-436391d36838
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
msc.type: authoredcontent
ms.openlocfilehash: ac53d651601829b6e7d2ce312a084618a8afbb61
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="programmatically-setting-the-objectdatasources-parameter-values-vb"></a><span data-ttu-id="28193-104">以编程方式设置对象数据源的参数值 (VB)</span><span class="sxs-lookup"><span data-stu-id="28193-104">Programmatically Setting the ObjectDataSource's Parameter Values (VB)</span></span>
====================
<span data-ttu-id="28193-105">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="28193-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="28193-106">[下载示例应用程序](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_6_VB.exe)或[下载 PDF](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/datatutorial06vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="28193-106">[Download Sample App](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_6_VB.exe) or [Download PDF](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/datatutorial06vb1.pdf)</span></span>

> <span data-ttu-id="28193-107">在本教程中我们将查看将方法添加到我们的 DAL 和 BLL 接受一个输入的参数并返回数据。</span><span class="sxs-lookup"><span data-stu-id="28193-107">In this tutorial we'll look at adding a method to our DAL and BLL that accepts a single input parameter and returns data.</span></span> <span data-ttu-id="28193-108">该示例将以编程方式设置此参数。</span><span class="sxs-lookup"><span data-stu-id="28193-108">The example will set this parameter programmatically.</span></span>


## <a name="introduction"></a><span data-ttu-id="28193-109">介绍</span><span class="sxs-lookup"><span data-stu-id="28193-109">Introduction</span></span>

<span data-ttu-id="28193-110">正如我们看到在[以前一教程](declarative-parameters-vb.md)，有多种选项都是可用于以声明方式将参数值传递给对象数据源的方法。</span><span class="sxs-lookup"><span data-stu-id="28193-110">As we saw in the [previous tutorial](declarative-parameters-vb.md), a number of options are available for declaratively passing parameter values to the ObjectDataSource's methods.</span></span> <span data-ttu-id="28193-111">如果参数值为硬编码，来自 Web 控件在页上，或在数据源是可读的任何其他源`Parameter`对象，例如，值将绑定到输入参数上，而无需编写一行代码。</span><span class="sxs-lookup"><span data-stu-id="28193-111">If the parameter value is hard-coded, comes from a Web control on the page, or is in any other source that is readable by a data source `Parameter` object, for example, that value can be bound to the input parameter without writing a line of code.</span></span>

<span data-ttu-id="28193-112">可能有些时候，但是，当参数值来源某些不已计由内置数据源之一`Parameter`对象。</span><span class="sxs-lookup"><span data-stu-id="28193-112">There may be times, however, when the parameter value comes from some source not already accounted for by one of the built-in data source `Parameter` objects.</span></span> <span data-ttu-id="28193-113">如果我们网站支持的用户帐户我们可能想要将基于当前登录的访问者的用户 id。 该参数设置</span><span class="sxs-lookup"><span data-stu-id="28193-113">If our site supported user accounts we might want to set the parameter based on the currently logged in visitor's User ID.</span></span> <span data-ttu-id="28193-114">或者，我们可能需要先将它传递发送到对象数据源的基础对象的方法自定义的参数值。</span><span class="sxs-lookup"><span data-stu-id="28193-114">Or we may need to customize the parameter value before sending it along to the ObjectDataSource's underlying object's method.</span></span>

<span data-ttu-id="28193-115">每当 ObjectDataSource`Select`调用方法 ObjectDataSource 首先引发其[选择事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="28193-115">Whenever the ObjectDataSource's `Select` method is invoked the ObjectDataSource first raises its [Selecting event](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx).</span></span> <span data-ttu-id="28193-116">然后调用对象数据源的基础对象的方法。</span><span class="sxs-lookup"><span data-stu-id="28193-116">The ObjectDataSource's underlying object's method is then invoked.</span></span> <span data-ttu-id="28193-117">一旦完成 ObjectDataSource[所选事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx)激发 （图 1 展示了这一序列的事件）。</span><span class="sxs-lookup"><span data-stu-id="28193-117">Once that completes the ObjectDataSource's [Selected event](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx) fires (Figure 1 illustrates this sequence of events).</span></span> <span data-ttu-id="28193-118">传递给对象数据源的基础对象的方法的参数值可设置或自定义的事件处理程序中`Selecting`事件。</span><span class="sxs-lookup"><span data-stu-id="28193-118">The parameter values passed into the ObjectDataSource's underlying object's method can be set or customized in an event handler for the `Selecting` event.</span></span>


<span data-ttu-id="28193-119">[![调用 ObjectDataSource 选中和选择事件激发之前和之后及其基础对象的方法](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="28193-119">[![The ObjectDataSource's Selected and Selecting Events Fire Before and After Its Underlying Object's Method is Invoked](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image1.png)</span></span>

<span data-ttu-id="28193-120">**图 1**: ObjectDataSource`Selected`和`Selecting`均会调用事件的激发之前和之后及其基础对象的方法 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="28193-120">**Figure 1**: The ObjectDataSource's `Selected` and `Selecting` Events Fire Before and After Its Underlying Object's Method is Invoked ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image3.png))</span></span>


<span data-ttu-id="28193-121">在本教程中我们将考察方法添加到我们的 DAL 和接受一个输入的参数的 BLL `Month`，类型的`Integer`并返回`EmployeesDataTable`填入这些其招聘周年中指定这些员工的对象`Month`.</span><span class="sxs-lookup"><span data-stu-id="28193-121">In this tutorial we'll look at adding a method to our DAL and BLL that accepts a single input parameter `Month`, of type `Integer` and returns an `EmployeesDataTable` object populated with those employees that have their hiring anniversary in the specified `Month`.</span></span> <span data-ttu-id="28193-122">我们的示例将设置此参数以编程方式根据当前月份，显示"员工周年纪念日的本月。"列表</span><span class="sxs-lookup"><span data-stu-id="28193-122">Our example will set this parameter programmatically based on the current month, showing a list of "Employee Anniversaries This Month."</span></span>

<span data-ttu-id="28193-123">让我们进入正题！</span><span class="sxs-lookup"><span data-stu-id="28193-123">Let's get started!</span></span>

## <a name="step-1-adding-a-method-toemployeestableadapter"></a><span data-ttu-id="28193-124">步骤 1： 添加到方法`EmployeesTableAdapter`</span><span class="sxs-lookup"><span data-stu-id="28193-124">Step 1: Adding a Method to`EmployeesTableAdapter`</span></span>

<span data-ttu-id="28193-125">对于我们我们需要添加一种方式来检索这些员工的第一个示例其`HireDate`在指定的月份中发生。</span><span class="sxs-lookup"><span data-stu-id="28193-125">For our first example we need to add a means to retrieve those employees whose `HireDate` occurred in a specified month.</span></span> <span data-ttu-id="28193-126">若要提供此功能根据我们体系结构，我们需要先创建中的方法`EmployeesTableAdapter`映射到正确的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="28193-126">To provide this functionality in accordance with our architecture we need to first create a method in `EmployeesTableAdapter` that maps to the proper SQL statement.</span></span> <span data-ttu-id="28193-127">若要完成此操作，首先打开 Northwind 类型化数据集。</span><span class="sxs-lookup"><span data-stu-id="28193-127">To accomplish this, start by opening the Northwind Typed DataSet.</span></span> <span data-ttu-id="28193-128">右键单击`EmployeesTableAdapter`标签，然后选择添加查询。</span><span class="sxs-lookup"><span data-stu-id="28193-128">Right-click on the `EmployeesTableAdapter` label and choose Add Query.</span></span>


<span data-ttu-id="28193-129">[![将新查询添加到 EmployeesTableAdapter](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="28193-129">[![Add a New Query to the EmployeesTableAdapter](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image4.png)</span></span>

<span data-ttu-id="28193-130">**图 2**： 添加到一个新查询`EmployeesTableAdapter`([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="28193-130">**Figure 2**: Add a New Query to the `EmployeesTableAdapter` ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image6.png))</span></span>


<span data-ttu-id="28193-131">选择添加返回行的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="28193-131">Choose to add a SQL statement that returns rows.</span></span> <span data-ttu-id="28193-132">在访问指定`SELECT`语句屏幕默认`SELECT`语句`EmployeesTableAdapter`已将加载。</span><span class="sxs-lookup"><span data-stu-id="28193-132">When you reach the Specify a `SELECT` Statement screen the default `SELECT` statement for the `EmployeesTableAdapter` will already be loaded.</span></span> <span data-ttu-id="28193-133">在中只需添加`WHERE`子句： `WHERE DATEPART(m, HireDate) = @Month`。</span><span class="sxs-lookup"><span data-stu-id="28193-133">Simply add in the `WHERE` clause: `WHERE DATEPART(m, HireDate) = @Month`.</span></span> <span data-ttu-id="28193-134">[DATEPART](https://msdn.microsoft.com/library/ms174420.aspx)是 T-SQL 的函数，返回的特定日期部分`datetime`类型; 在这种情况下，我们将使用`DATEPART`返回的月份`HireDate`列。</span><span class="sxs-lookup"><span data-stu-id="28193-134">[DATEPART](https://msdn.microsoft.com/library/ms174420.aspx) is a T-SQL function that returns a particular date portion of a `datetime` type; in this case we're using `DATEPART` to return the month of the `HireDate` column.</span></span>


<span data-ttu-id="28193-135">[![返回仅的那些行其中 hiredate 列是否小于或等于@HiredBeforeDate参数](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="28193-135">[![Return Only Those Rows Where the HireDate Column is Less Than or Equal to the @HiredBeforeDate Parameter](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image7.png)</span></span>

<span data-ttu-id="28193-136">**图 3**： 返回仅的那些行其中`HireDate`列是否小于或等于`@HiredBeforeDate`参数 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="28193-136">**Figure 3**: Return Only Those Rows Where the `HireDate` Column is Less Than or Equal to the `@HiredBeforeDate` Parameter ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image9.png))</span></span>


<span data-ttu-id="28193-137">最后，更改`FillBy`和`GetDataBy`方法名称为`FillByHiredDateMonth`和`GetEmployeesByHiredDateMonth`分别。</span><span class="sxs-lookup"><span data-stu-id="28193-137">Finally, change the `FillBy` and `GetDataBy` method names to `FillByHiredDateMonth` and `GetEmployeesByHiredDateMonth`, respectively.</span></span>


<span data-ttu-id="28193-138">[![选择比 FillBy 和 GetDataBy 更合适的方法名称](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="28193-138">[![Choose More Appropriate Method Names Than FillBy and GetDataBy](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image10.png)</span></span>

<span data-ttu-id="28193-139">**图 4**： 选择更适当方法名称比`FillBy`和`GetDataBy`([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="28193-139">**Figure 4**: Choose More Appropriate Method Names Than `FillBy` and `GetDataBy` ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image12.png))</span></span>


<span data-ttu-id="28193-140">单击完成以完成向导并返回到数据集的设计图面。</span><span class="sxs-lookup"><span data-stu-id="28193-140">Click Finish to complete the wizard and return to the DataSet's design surface.</span></span> <span data-ttu-id="28193-141">`EmployeesTableAdapter`现在应包含一组新的用于访问指定的月份内雇用的员工的方法。</span><span class="sxs-lookup"><span data-stu-id="28193-141">The `EmployeesTableAdapter` should now include a new set of methods for accessing employees hired in a specified month.</span></span>


<span data-ttu-id="28193-142">[![新的方法显示在数据集的设计图面](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="28193-142">[![The New Methods Appear in the DataSet's Design Surface](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image13.png)</span></span>

<span data-ttu-id="28193-143">**图 5**: 新方法显示在数据集的设计图面 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="28193-143">**Figure 5**: The New Methods Appear in the DataSet's Design Surface ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image15.png))</span></span>


## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a><span data-ttu-id="28193-144">步骤 2： 添加`GetEmployeesByHiredDateMonth(month)`业务逻辑层的方法</span><span class="sxs-lookup"><span data-stu-id="28193-144">Step 2: Adding the`GetEmployeesByHiredDateMonth(month)`Method to the Business Logic Layer</span></span>

<span data-ttu-id="28193-145">由于我们应用程序体系结构用于单独的层的业务逻辑和数据访问逻辑，我们需要将方法添加到指定日期前的租期下 DAL 的调用以检索员工我们 BLL。</span><span class="sxs-lookup"><span data-stu-id="28193-145">Since our application architecture uses a separate layer for the business logic and data access logic, we need to add a method to our BLL that calls down to the DAL to retrieve employees hired before a specified date.</span></span> <span data-ttu-id="28193-146">打开`EmployeesBLL.vb`文件并添加以下方法：</span><span class="sxs-lookup"><span data-stu-id="28193-146">Open the `EmployeesBLL.vb` file and add the following method:</span></span>


[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample1.vb)]

<span data-ttu-id="28193-147">与我们在此类中的其他方法一样`GetEmployeesByHiredDateMonth(month)`只需调入 DAL 并返回结果。</span><span class="sxs-lookup"><span data-stu-id="28193-147">As with our other methods in this class, `GetEmployeesByHiredDateMonth(month)` simply calls down into the DAL and returns the results.</span></span>

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a><span data-ttu-id="28193-148">步骤 3： 显示其招聘周年日是这个月的员工</span><span class="sxs-lookup"><span data-stu-id="28193-148">Step 3: Displaying Employees Whose Hiring Anniversary Is This Month</span></span>

<span data-ttu-id="28193-149">此示例中我们最后一个步骤是显示其招聘周年日是本月这些员工。</span><span class="sxs-lookup"><span data-stu-id="28193-149">Our final step for this example is to display those employees whose hiring anniversary is this month.</span></span> <span data-ttu-id="28193-150">首先，通过添加到 GridView`ProgrammaticParams.aspx`页面`BasicReporting`文件夹并将新对象数据源添加为其数据源。</span><span class="sxs-lookup"><span data-stu-id="28193-150">Start by adding a GridView to the `ProgrammaticParams.aspx` page in the `BasicReporting` folder and add a new ObjectDataSource as its data source.</span></span> <span data-ttu-id="28193-151">配置对象数据源以使用`EmployeesBLL`类，该类具有`SelectMethod`设置为`GetEmployeesByHiredDateMonth(month)`。</span><span class="sxs-lookup"><span data-stu-id="28193-151">Configure the ObjectDataSource to use the `EmployeesBLL` class with the `SelectMethod` set to `GetEmployeesByHiredDateMonth(month)`.</span></span>


<span data-ttu-id="28193-152">[![使用 EmployeesBLL 类](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="28193-152">[![Use the EmployeesBLL Class](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image16.png)</span></span>

<span data-ttu-id="28193-153">**图 6**： 使用`EmployeesBLL`类 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="28193-153">**Figure 6**: Use the `EmployeesBLL` Class ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image18.png))</span></span>


<span data-ttu-id="28193-154">[![选择从 GetEmployeesByHiredDateMonth(month) 方法](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="28193-154">[![Select From the GetEmployeesByHiredDateMonth(month) method](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image19.png)</span></span>

<span data-ttu-id="28193-155">**图 7**: Select From`GetEmployeesByHiredDateMonth(month)`方法 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="28193-155">**Figure 7**: Select From the `GetEmployeesByHiredDateMonth(month)` method ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image21.png))</span></span>


<span data-ttu-id="28193-156">最后一个屏幕可让我们提供`month`参数值的源。</span><span class="sxs-lookup"><span data-stu-id="28193-156">The final screen asks us to provide the `month` parameter value's source.</span></span> <span data-ttu-id="28193-157">由于我们将以编程方式设置此值，保留参数源设置默认值为 None 选项，然后单击完成。</span><span class="sxs-lookup"><span data-stu-id="28193-157">Since we'll set this value programmatically, leave the Parameter source set to the default None option and click Finish.</span></span>


<span data-ttu-id="28193-158">[![将参数源设置保留为无](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="28193-158">[![Leave the Parameter Source Set to None](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image22.png)</span></span>

<span data-ttu-id="28193-159">**图 8**： 将保留为无设置参数源 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="28193-159">**Figure 8**: Leave the Parameter Source Set to None ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image24.png))</span></span>


<span data-ttu-id="28193-160">这将创建`Parameter`中对象数据源的对象`SelectParameters`不具有指定的值的集合。</span><span class="sxs-lookup"><span data-stu-id="28193-160">This will create a `Parameter` object in the ObjectDataSource's `SelectParameters` collection that does not have a value specified.</span></span>


[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample2.aspx)]

<span data-ttu-id="28193-161">若要以编程方式设置此值，我们需要创建对象数据源的事件处理程序`Selecting`事件。</span><span class="sxs-lookup"><span data-stu-id="28193-161">To set this value programmatically, we need to create an event handler for the ObjectDataSource's `Selecting` event.</span></span> <span data-ttu-id="28193-162">若要完成此操作，请转到设计视图，并双击 ObjectDataSource。</span><span class="sxs-lookup"><span data-stu-id="28193-162">To accomplish this, go to the Design view and double-click the ObjectDataSource.</span></span> <span data-ttu-id="28193-163">或者，选中 ObjectDataSource、 转到属性窗口中，然后单击闪电形图标。</span><span class="sxs-lookup"><span data-stu-id="28193-163">Alternatively, select the ObjectDataSource, go to the Properties window, and click the lightning bolt icon.</span></span> <span data-ttu-id="28193-164">接下来，请双击在文本框中旁边`Selecting`事件或输入你想要使用的事件处理程序的名称。</span><span class="sxs-lookup"><span data-stu-id="28193-164">Next, either double-click in the textbox next to the `Selecting` event or type in the name of the event handler you want to use.</span></span> <span data-ttu-id="28193-165">如第三个选项，你可以通过选择 ObjectDataSource 创建事件处理程序并将其`Selecting`顶部的页的代码隐藏类的两个下拉列表中的事件。</span><span class="sxs-lookup"><span data-stu-id="28193-165">As a third option, you can create the event handler by selecting the ObjectDataSource and its `Selecting` event from the two drop-down lists at the top of the page's code-behind class.</span></span>


![单击属性窗口列出 Web 控件的事件中的闪电形图标](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image25.png)

<span data-ttu-id="28193-167">**图 9**： 单击属性窗口列出 Web 控件的事件中的闪电形图标</span><span class="sxs-lookup"><span data-stu-id="28193-167">**Figure 9**: Click on the Lightning Bolt Icon in the Properties Window to List a Web Control's Events</span></span>


<span data-ttu-id="28193-168">所有三种方法添加的新的事件处理程序 ObjectDataSource`Selecting`到页面的代码隐藏类的事件。</span><span class="sxs-lookup"><span data-stu-id="28193-168">All three approaches add a new event handler for the ObjectDataSource's `Selecting` event to the page's code-behind class.</span></span> <span data-ttu-id="28193-169">在此事件处理程序中，我们可以读取和写入使用的参数值`e.InputParameters(parameterName)`，其中*`parameterName`*是值`Name`属性中`<asp:Parameter>`标记 (`InputParameters`集合也可以是按序号对它们，在索引`e.InputParameters(index)`)。</span><span class="sxs-lookup"><span data-stu-id="28193-169">In this event handler we can read and write to the parameter values using `e.InputParameters(parameterName)`, where *`parameterName`* is the value of the `Name` attribute in the `<asp:Parameter>` tag (the `InputParameters` collection can also be indexed ordinally, as in `e.InputParameters(index)`).</span></span> <span data-ttu-id="28193-170">若要设置`month`到当前月份，参数添加到以下`Selecting`事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="28193-170">To set the `month` parameter to the current month, add the following to the `Selecting` event handler:</span></span>


[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample3.vb)]

<span data-ttu-id="28193-171">在访问此页通过浏览器时，我们可以看到该只有一个员工受雇本月 （年 3 月） 刘娜王五，1994年起已在公司人员。</span><span class="sxs-lookup"><span data-stu-id="28193-171">When visiting this page through a browser we can see that only one employee was hired this month (March) Laura Callahan, who's been with the company since 1994.</span></span>


<span data-ttu-id="28193-172">[![其纪念日显示本月这些员工](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image26.png)</span><span class="sxs-lookup"><span data-stu-id="28193-172">[![Those Employees Whose Anniversaries This Month Are Shown](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image26.png)</span></span>

<span data-ttu-id="28193-173">**图 10**： 那些员工其纪念日此月显示 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image28.png))</span><span class="sxs-lookup"><span data-stu-id="28193-173">**Figure 10**: Those Employees Whose Anniversaries This Month Are Shown ([Click to view full-size image](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image28.png))</span></span>


## <a name="summary"></a><span data-ttu-id="28193-174">总结</span><span class="sxs-lookup"><span data-stu-id="28193-174">Summary</span></span>

<span data-ttu-id="28193-175">尽管对象数据源的参数值通常可设置以声明方式，而无需代码行，很容易以编程方式设置参数值。</span><span class="sxs-lookup"><span data-stu-id="28193-175">While the ObjectDataSource's parameters' values can typically be set declaratively, without requiring a line of code, it's easy to set the parameter values programmatically.</span></span> <span data-ttu-id="28193-176">我们需要做的就是创建为对象数据源的事件处理程序`Selecting`触发的事件，基础对象的方法未调用，且手动设置通过一个或多个参数的值之前`InputParameters`集合。</span><span class="sxs-lookup"><span data-stu-id="28193-176">All we need to do is create an event handler for the ObjectDataSource's `Selecting` event, which fires before the underlying object's method is invoked, and manually set the values for one or more parameters via the `InputParameters` collection.</span></span>

<span data-ttu-id="28193-177">本教程到结束基本报告部分。</span><span class="sxs-lookup"><span data-stu-id="28193-177">This tutorial concludes the Basic Reporting section.</span></span> <span data-ttu-id="28193-178">[下一教程](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md)启动关闭筛选和主-详细信息方案部分，我们将在其中查看允许访问者来筛选数据的技术，并从主报表深化到详细信息报告。</span><span class="sxs-lookup"><span data-stu-id="28193-178">The [next tutorial](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) kicks off the Filtering and Master-Details Scenarios section, in which we'll look at techniques for allowing the visitor to filter data and drill down from a master report into a details report.</span></span>

<span data-ttu-id="28193-179">尽情享受编程 ！</span><span class="sxs-lookup"><span data-stu-id="28193-179">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="28193-180">关于作者</span><span class="sxs-lookup"><span data-stu-id="28193-180">About the Author</span></span>

<span data-ttu-id="28193-181">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的七个 ASP/ASP.NET 书籍和的创始人[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年使用与 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="28193-181">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="28193-182">Scott 的作用是作为独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="28193-182">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="28193-183">最新书籍是[ *Sam 教授自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="28193-183">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="28193-184">他可以达到在[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)或通过他的博客，其中可以找到在[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="28193-184">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="28193-185">特别感谢</span><span class="sxs-lookup"><span data-stu-id="28193-185">Special Thanks To</span></span>

<span data-ttu-id="28193-186">本教程系列已由许多有用的审阅者评审。</span><span class="sxs-lookup"><span data-stu-id="28193-186">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="28193-187">本教程中的前导审阅者已希尔顿 Giesenow。</span><span class="sxs-lookup"><span data-stu-id="28193-187">Lead reviewer for this tutorial was Hilton Giesenow.</span></span> <span data-ttu-id="28193-188">对感兴趣查看我即将到来的 MSDN 文章？</span><span class="sxs-lookup"><span data-stu-id="28193-188">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="28193-189">如果是这样，删除我一行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="28193-189">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="28193-190">上一篇</span><span class="sxs-lookup"><span data-stu-id="28193-190">Previous</span></span>](declarative-parameters-vb.md)
