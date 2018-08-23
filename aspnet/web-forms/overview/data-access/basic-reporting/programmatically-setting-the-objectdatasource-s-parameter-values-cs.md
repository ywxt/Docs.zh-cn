---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs
title: 以编程方式设置 ObjectDataSource 的参数值 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将介绍方法添加到我们的 DAL 和 BLL 接受一个输入的参数并返回数据。 该示例将设置此参数...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 1c4588bb-255d-4088-b319-5208da756f4d
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs
msc.type: authoredcontent
ms.openlocfilehash: 78de288977f55ffe73c5b34329cd5b5c5c84334f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825476"
---
<a name="programmatically-setting-the-objectdatasources-parameter-values-c"></a>以编程方式设置 ObjectDataSource 的参数值 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_6_CS.exe)或[下载 PDF](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/datatutorial06cs1.pdf)

> 在本教程中我们将介绍方法添加到我们的 DAL 和 BLL 接受一个输入的参数并返回数据。 该示例将以编程方式设置此参数。


## <a name="introduction"></a>介绍

中可以看到[前一篇教程](declarative-parameters-cs.md)，有多种选项都是可用于以声明方式将参数值传递给 ObjectDataSource 的方法。 如果参数值为硬编码，来自 Web 控件在页上，或者由数据源是可读的任何其他源中`Parameter`对象，例如，值绑定到输入参数上，而无需编写一行代码。

但是，有时时参数值来自某些源由一个内置数据源已不计`Parameter`对象。 如果我们的站点支持的用户帐户我们可能想要设置参数基于当前登录的访问者的用户 id。 或者，我们可能需要先将其发送到 ObjectDataSource 的基础对象的方法自定义参数值。

每当 ObjectDataSource`Select`方法调用 ObjectDataSource 首先引发其[选择事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx)。 然后调用 ObjectDataSource 的基础对象的方法。 该操作完成 ObjectDataSource 的后[选定事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx)激发 （图 1 展示了这一序列的事件）。 传递到 ObjectDataSource 的基础对象的方法的参数值可设置或自定义的事件处理程序中`Selecting`事件。


[![ObjectDataSource 的选中和选择事件触发之前和之后及其基础对象的方法被调用](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image1.png)

**图 1**: ObjectDataSource`Selected`并`Selecting`调用事件触发之前和之后及其基础对象的方法 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image3.png))


在本教程中我们将介绍方法添加到我们的 DAL 和接受一个输入的参数的 BLL `Month`，类型的`int`，并返回`EmployeesDataTable`填入这些员工将其招聘周年中指定的对象`Month`. 我们的示例将设置此参数以编程方式基于当前月的上显示一系列"员工周年纪念日本月。"

让我们进入正题！

## <a name="step-1-adding-a-method-toemployeestableadapter"></a>步骤 1： 添加到方法`EmployeesTableAdapter`

对于我们的第一个示例中我们需要添加一种方法来检索这些员工其`HireDate`发生在指定月份中。 若要提供此功能根据我们需要首先创建中的方法的体系结构`EmployeesTableAdapter`，它映射到正确的 SQL 语句。 若要完成此操作，先打开 Northwind 类型化数据集。 右键单击`EmployeesTableAdapter`标签，然后选择添加查询。


[![将一个新查询添加到 EmployeesTableAdapter](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image4.png)

**图 2**： 添加到一个新查询`EmployeesTableAdapter`([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image6.png))


选择要添加将返回行的 SQL 语句。 在访问指定`SELECT`语句屏幕上的默认值`SELECT`语句`EmployeesTableAdapter`将加载。 只需在中添加`WHERE`子句： `WHERE DATEPART(m, HireDate) = @Month`。 [DATEPART](https://msdn.microsoft.com/library/ms174420.aspx)是返回特定日期的一部分的 T-SQL 函数`datetime`类型; 我们使用这种情况下`DATEPART`返回的月份`HireDate`列。


[![返回仅这些行位置的 HireDate 列是否小于或等于@HiredBeforeDate参数](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image7.png)

**图 3**： 返回仅这些行位置`HireDate`列是否小于或等于`@HiredBeforeDate`参数 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image9.png))


最后，更改`FillBy`并`GetDataBy`方法的名称到`FillByHiredDateMonth`和`GetEmployeesByHiredDateMonth`分别。


[![选择比 FillBy 和 GetDataBy 更合适的方法名称](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image10.png)

**图 4**： 选择更适当方法的名称比`FillBy`并`GetDataBy`([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image12.png))


单击完成以完成向导并返回到数据集的设计图面上。 `EmployeesTableAdapter`现在应包含一组新的用于访问在指定月份中雇用的员工的方法。


[![在数据集的设计图面上显示的新方法](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image13.png)

**图 5**: 新方法出现在数据集的设计图面上 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image15.png))


## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a>步骤 2： 添加`GetEmployeesByHiredDateMonth(month)`业务逻辑层方法

由于我们应用程序体系结构用于单独层业务逻辑和数据访问逻辑，我们需要将方法添加到 DAL 的调用来检索雇员雇佣在指定日期前我们 BLL。 打开`EmployeesBLL.cs`文件，并添加以下方法：


[!code-csharp[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample1.cs)]

与我们在此类中的其他方法一样`GetEmployeesByHiredDateMonth(month)`只需调用 DAL 并返回结果。

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a>步骤 3： 显示其招聘周年日是这个月的员工

此示例中我们最后一步是要显示其招聘周年日是这个月的员工。 首先，通过添加到 GridView`ProgrammaticParams.aspx`页中`BasicReporting`文件夹并将新对象数据源添加为其数据源。 配置要使用 ObjectDataSource`EmployeesBLL`类的`SelectMethod`设置为`GetEmployeesByHiredDateMonth(month)`。


[![使用 EmployeesBLL 类](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image16.png)

**图 6**： 使用`EmployeesBLL`类 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image18.png))


[![选择从 GetEmployeesByHiredDateMonth(month) 方法](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image19.png)

**图 7**: Select From`GetEmployeesByHiredDateMonth(month)`方法 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image21.png))


最后一个屏幕询问我们提供`month`参数值的源。 由于我们将以编程方式设置此值，将保留参数源设置为默认值 None 选项，然后单击完成。


[![将参数源设置为 None](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image22.png)

**图 8**： 将保留为无设置参数源 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image24.png))


这将创建`Parameter`对象中的 ObjectDataSource`SelectParameters`不具有指定的值的集合。


[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample2.aspx)]

若要以编程方式设置此值，我们需要为 ObjectDataSource 的创建事件处理程序`Selecting`事件。 若要实现此目的，请转到设计视图，并双击 ObjectDataSource。 或者，选择 ObjectDataSource 中，转到属性窗口中，并单击闪电形图标。 接下来，可以双击在文本框旁边`Selecting`事件或键入你想要使用的事件处理程序的名称。


![单击属性窗口列出 Web 控件的事件中的闪电形图标](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image25.png)

**图 9**： 单击属性窗口列出 Web 控件的事件中的闪电形图标


这两种方法将新的事件处理程序添加了 ObjectDataSource 的`Selecting`到页面的代码隐藏类的事件。 此事件处理程序中我们可以读取和写入到使用的参数值`e.InputParameters[parameterName]`，其中*`parameterName`* 的值`Name`属性中`<asp:Parameter>`标记 (`InputParameters`也可以是集合索引作为中序号， `e.InputParameters[index]`)。 若要设置`month`当前月份，参数添加到以下`Selecting`事件处理程序：


[!code-csharp[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample3.cs)]

访问此页上的通过浏览器时，我们可以看到该只有一个雇员雇佣的这个月 （年 3 月） Laura Callahan，已在公司自 1994 年。


[![这个月显示其周年纪念日这些员工](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image26.png)

**图 10**： 这些员工其周年纪念日此月显示 ([单击以查看实际尺寸的图像](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image28.png))


## <a name="summary"></a>总结

虽然 ObjectDataSource 的参数值通常可以设置以声明方式，而无需一行代码，很容易地以编程方式设置参数值。 我们需要做的就是为 ObjectDataSource 的创建事件处理程序`Selecting`触发的事件，基础对象的方法是调用，并手动设置为通过一个或多个参数的值之前`InputParameters`集合。

基本报告部分到本教程结束。 [下一教程](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)开始为期筛选和母版-详细信息方案部分，我们将介绍的技术允许筛选数据的访问者并从主报表深化到详细信息报表。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Hilton Giesenow。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](declarative-parameters-cs.md)
> [下一页](displaying-data-with-the-objectdatasource-vb.md)
