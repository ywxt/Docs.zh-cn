---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
title: 在 GridView 控件 (C#) 中使用 Templatefield |Microsoft Docs
author: rick-anderson
description: 若要提供的灵活性，GridView 提供 TemplateField，这使得使用模板。 模板可以包括静态 HTML Web 控件的组合和...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 11de31e8-a78a-4f96-bd75-66e994175902
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 4d1cad54d07ba3756d653685b3e04cb66e5ca98b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824836"
---
<a name="using-templatefields-in-the-gridview-control-c"></a>在 GridView 控件 (C#) 中使用 Templatefield
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_12_CS.exe)或[下载 PDF](using-templatefields-in-the-gridview-control-cs/_static/datatutorial12cs1.pdf)

> 若要提供的灵活性，GridView 提供 TemplateField，这使得使用模板。 模板可以包括组合的静态 HTML Web 控件和数据绑定语法。 在本教程中我们将介绍如何使用 templatefield 进一步自定义 GridView 控件更大程度。


## <a name="introduction"></a>介绍

GridView 组成的一组字段，指示哪些属性从`DataSource`都包括在呈现的输出以及数据的显示方式。 最简单的字段类型为 BoundField 后者将数据值显示为文本。 其他字段类型显示使用备用的 HTML 元素的数据。 CheckBoxField，例如，呈现为选中的状态取决于指定的数据字段; 的值的复选框ImageField 呈现其图像源基于指定的数据字段的图像。 使用 HyperLinkField 和 ButtonField 字段类型可以呈现超链接和按钮的状态取决于基础数据字段值。

尽管 CheckBoxField、 ImageField、 HyperLinkField 和 ButtonField 字段类型允许的数据的替代视图，它们仍是相对于格式设置却非常有限。 CheckBoxField 只能显示一个复选框，而 ImageField 只能显示一个映像。 如果需要显示一些文本，复选框，特定字段*和*映像，所有基于不同的数据字段值？ 或者，如果我们想要显示使用复选框、 图像、 超链接或按钮以外的 Web 控件的数据？ 此外，BoundField 限制到单个数据字段显示。 如果我们想要在单个的 GridView 列中显示两个或多个数据字段值？

为适应此程度的灵活性 GridView 提供 TemplateField，这使得使用*模板*。 模板可以包括组合的静态 HTML Web 控件和数据绑定语法。 此外，TemplateField 可以有各种模板，它们可用于自定义不同的情况下呈现。 例如，`ItemTemplate`默认情况下使用要呈现的单元格，对于每一行，但`EditItemTemplate`模板可用于自定义界面编辑数据时。

在本教程中我们将介绍如何使用 templatefield 进一步自定义 GridView 控件更大程度。 在中[前面的教程](custom-formatting-based-upon-data-cs.md)我们已了解如何自定义基于基础数据使用的格式设置`DataBound`和`RowDataBound`事件处理程序。 若要自定义基于基础数据的格式设置的另一种方法通过调用的格式设置方法在模板中。 我们将在本教程还介绍此技术。

本教程中我们将使用 Templatefield 以自定义的员工列表的外观。 具体而言，我们将列出所有员工，但会显示该雇员的一个列中，他们的雇佣日期在一个日历控件，并指示多少天它们已被采用了公司的状态列中的第一个和最后一个名称。


[![用于自定义显示三个 Templatefield](using-templatefields-in-the-gridview-control-cs/_static/image2.png)](using-templatefields-in-the-gridview-control-cs/_static/image1.png)

**图 1**： 用于自定义显示三个 Templatefield ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image3.png))


## <a name="step-1-binding-the-data-to-the-gridview"></a>步骤 1： 将数据绑定到 GridView

在报告中需要使用 Templatefield 外观进行自定义的方案，我发现最简单的方法首先创建第一次包含只 BoundFields 的 GridView 控件，然后添加新 Templatefield 或转换到现有 BoundFields根据需要 Templatefield。 因此，我们先来在设计器中翻页添加 GridView 并将其绑定到返回的员工列表中的 ObjectDataSource 的本教程。 这些步骤将为每个员工字段与 BoundFields 创建 GridView。

打开`GridViewTemplateField.aspx`页上，并将从工具箱拖到设计器的 GridView。 从 GridView 的智能标记选择添加新的 ObjectDataSource 控件，调用`EmployeesBLL`类的`GetEmployees()`方法。


[![添加新的 ObjectDataSource 控件，它调用 GetEmployees() 方法](using-templatefields-in-the-gridview-control-cs/_static/image5.png)](using-templatefields-in-the-gridview-control-cs/_static/image4.png)

**图 2**： 添加新的 ObjectDataSource 控件的 Invoke`GetEmployees()`方法 ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image6.png))


绑定 GridView 以这种方式自动将 BoundField 为每个员工属性： `EmployeeID`， `LastName`， `FirstName`， `Title`， `HireDate`， `ReportsTo`，和`Country`。 为此报表让我们不会费神去的显示`EmployeeID`， `ReportsTo`，或`Country`属性。 若要删除这些 BoundFields 可以：

- 使用 GridView 的智能标记中的编辑列链接上字段对话框中，单击以显示此对话框。 接下来，选择左下角 BoundFields 列表，然后单击红色的 X 按钮以删除 BoundField。
- 源视图中手动编辑 GridView 的声明性语法，删除`<asp:BoundField>`BoundField 你想要删除的元素。

已删除后`EmployeeID`， `ReportsTo`，和`Country`BoundFields，GridView 的标记应如下所示：


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample1.aspx)]

请花费片刻时间浏览器中查看我们的进度。 此时应看到一条记录的表的每个雇员和四个列： 一个用于员工的姓氏、 一个用于其第一个名称，一个用于其标题，一个用于他们的雇佣日期。


[![LastName、 FirstName、 标题和的 HireDate 字段显示为每个员工](using-templatefields-in-the-gridview-control-cs/_static/image8.png)](using-templatefields-in-the-gridview-control-cs/_static/image7.png)

**图 3**: `LastName`， `FirstName`， `Title`，并`HireDate`将显示每个员工的字段 ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image9.png))


## <a name="step-2-displaying-the-first-and-last-names-in-a-single-column"></a>步骤 2： 在单个列中显示的第一个和最后一个名称

目前，每个雇员的名字和姓氏显示在一个单独的列。 可能会令人高兴而是将它们组合成单个列。 若要实现此目的，我们需要使用 templatefield 进一步。 我们可添加新 TemplateField、 向其添加所需的标记和数据绑定语法，然后删除`FirstName`并`LastName`BoundFields，或者我们可以将转换`FirstName`转换为 TemplateField BoundField 编辑包括 TemplateField`LastName`值，，然后删除`LastName`BoundField。

这两种方法 net 相同的结果，但我个人喜欢将 BoundFields 转换为 Templatefield 在可能的情况，因为转换会自动添加`ItemTemplate`和`EditItemTemplate`Web 控件和数据绑定语法来模拟外观和 BoundField 功能。 好处是，我们将需要执行较少使用 templatefield 进一步转换过程将具有执行一些操作，为我们。

若要将转换为 TemplateField 现有 BoundField，请单击 GridView 的智能标记，使字段对话框中的编辑列链接。 选择 BoundField 转换从左下角中的列表，然后单击右下角中的"转换此字段转换为 TemplateField"链接。


[![BoundField 转换为 TemplateField 从字段对话框](using-templatefields-in-the-gridview-control-cs/_static/image11.png)](using-templatefields-in-the-gridview-control-cs/_static/image10.png)

**图 4**： 将 TemplateField BoundField 到转换从字段对话框 ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image12.png))


继续操作并将转换`FirstName`转换为 TemplateField BoundField。 此更改后没有设计器中的任何角度区别。 这是因为 BoundField 转换为 TemplateField 创建 TemplateField 维护 BoundField 的外观。 即使没有可见差异此时在设计器中的那里，此转换过程已替换 BoundField 的声明性语法- `<asp:BoundField DataField="FirstName" HeaderText="FirstName" SortExpression="FirstName" />` -TemplateField 语法为：


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample2.aspx)]

TemplateField 正如您所看到的包括两个模板`ItemTemplate`具有一个标签其`Text`属性设置为的值`FirstName`数据字段和一个`EditItemTemplate`带有文本框控件`Text`属性也设置到`FirstName`数据字段。 数据绑定语法中- `<%# Bind("fieldName") %>` -指示数据字段*`fieldName`* 绑定到指定的 Web 控件属性。

若要添加`LastName`数据字段值为此我们需要添加另一个标签 Web 控件中的 TemplateField `ItemTemplate` ，并将绑定其`Text`属性设置为`LastName`。 此操作可以手动或通过设计器完成。 若要执行手动操作，只需添加相应的声明性语法对`ItemTemplate`:


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample3.aspx)]

若要将其添加通过设计器中，单击 GridView 的智能标记中的编辑模板链接。 这将显示 GridView 的模板编辑界面。 在此接口的智能标记是 GridView 中的模板的列表。 由于我们仅在这里有一个 TemplateField，下拉列表中列出的唯一模板是为这些模板`FirstName`TemplateField 连同`EmptyDataTemplate`和`PagerTemplate`。 `EmptyDataTemplate` ，如果指定，使用模板来呈现 GridView 的输出中是否存在任何结果的数据绑定到 GridView; `PagerTemplate`，如果指定，用于为支持分页的 GridView 呈现分页界面。


[![可以通过在设计器编辑 GridView 的模板](using-templatefields-in-the-gridview-control-cs/_static/image14.png)](using-templatefields-in-the-gridview-control-cs/_static/image13.png)

**图 5**： 的 GridView 模板可以是编辑通过设计器 ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image15.png))


此外显示`LastName`中`FirstName`TemplateField 拖动标签控件从工具箱拖到`FirstName`TemplateField 的`ItemTemplate`GridView 中的模板编辑界面。


[![将标签 Web 控件添加到名字 TemplateField ItemTemplate](using-templatefields-in-the-gridview-control-cs/_static/image17.png)](using-templatefields-in-the-gridview-control-cs/_static/image16.png)

**图 6**： 添加标签 Web 控件与`FirstName`TemplateField 的 ItemTemplate ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image18.png))


在这点标签 Web 控件添加到 TemplateField 有其`Text`属性设置为"标签"。 我们需要更改，以便此属性绑定到的值`LastName`改为数据字段。 若要完成此标签控件的智能标记，请单击并选择编辑数据绑定选项。


[![从标签的智能标记中选择编辑数据绑定选项](using-templatefields-in-the-gridview-control-cs/_static/image20.png)](using-templatefields-in-the-gridview-control-cs/_static/image19.png)

**图 7**： 从标签的智能标记中选择编辑数据绑定选项 ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image21.png))


此时会弹出数据绑定对话框。 在这里可以选择要参与数据绑定，从左侧列表中，选择要将数据绑定到从下拉列表右侧的字段的属性。 选择`Text`从左侧的属性和`LastName`字段从右侧，然后单击确定。


[![将 Text 属性绑定到 LastName 数据字段](using-templatefields-in-the-gridview-control-cs/_static/image23.png)](using-templatefields-in-the-gridview-control-cs/_static/image22.png)

**图 8**： 将绑定`Text`属性设置为`LastName`数据字段 ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image24.png))


> [!NOTE]
> 数据绑定对话框中，可指示是否执行双向数据绑定。 如果您不勾选此项，数据绑定语法`<%# Eval("LastName")%>`而不是将使用`<%# Bind("LastName")%>`。 本教程这两种方法是没问题。 双向数据绑定变得重要时插入和编辑数据。 只是显示数据，但是，这两种方法将同等有效。 在将来的教程中，我们将讨论详细信息中的双向数据绑定。


请花费片刻时间来查看此页上的通过浏览器。 如您所见，GridView 仍包含四个列;但是，`FirstName`列现在会列出*同时*`FirstName`和`LastName`数据字段值。


[![单个列中所示的 FirstName 和 LastName 值](using-templatefields-in-the-gridview-control-cs/_static/image26.png)](using-templatefields-in-the-gridview-control-cs/_static/image25.png)

**图 9**： 既`FirstName`并`LastName`单个列中显示值 ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image27.png))


若要完成此第一个步骤，删除`LastName`BoundField 和重命名`FirstName`TemplateField 的`HeaderText`属性设置为"Name"。 这些更改后 GridView 的声明性标记应如下所示：


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample4.aspx)]


[![每个员工的第一个和最后一个名称显示在一个列](using-templatefields-in-the-gridview-control-cs/_static/image29.png)](using-templatefields-in-the-gridview-control-cs/_static/image28.png)

**图 10**： 在一个列中显示每个员工的第一个和最后一个名称 ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image30.png))


## <a name="step-3-using-the-calendar-control-to-display-thehireddatefield"></a>步骤 3： 使用日历控件显示`HiredDate`字段

在 GridView 中以文本显示数据字段值是使用 BoundField 一样简单。 对于某些方案中，但是，数据最适合使用表示特定的 Web 控件而不是只包含文本。 可以使用 Templatefield 此类自定义显示的数据。 例如，而不是以文本形式显示雇员的雇佣日期，我们可以显示日历 (使用[日历控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar(VS.80).aspx)) 使用他们的雇佣日期突出显示。

若要完成此操作，首先将转换`HiredDate`转换为 TemplateField BoundField。 只需转到 GridView 的智能标记，并单击编辑列链接，打开字段对话框。 选择`HiredDate`BoundField，然后单击"转换此字段转换为 TemplateField。"


[![HiredDate BoundField 转换为 TemplateField](using-templatefields-in-the-gridview-control-cs/_static/image32.png)](using-templatefields-in-the-gridview-control-cs/_static/image31.png)

**图 11**： 将转换`HiredDate`BoundField 到 TemplateField ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image33.png))


步骤 2 中可以看到，这会 BoundField 将替换为包含 TemplateField`ItemTemplate`和`EditItemTemplate`标签和文本框使用其`Text`属性绑定到`HiredDate`值使用数据绑定语法`<%# Bind("HiredDate")%>`.

将文本替换为一个日历控件，请通过删除标签和添加一个日历控件编辑的模板。 从设计器中，从 GridView 的智能标记选择编辑模板，并选择`HireDate`TemplateField 的`ItemTemplate`从下拉列表。 接下来，删除标签控件，并将一个日历控件从工具箱拖到模板的编辑界面。


[![添加到一个日历控件的 HireDate TemplateField 的 ItemTemplate](using-templatefields-in-the-gridview-control-cs/_static/image35.png)](using-templatefields-in-the-gridview-control-cs/_static/image34.png)

**图 12**： 添加到一个日历控件`HireDate`TemplateField 的`ItemTemplate`([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image36.png))


此时 GridView 中的每一行将包含一个日历控件在其`HiredDate`TemplateField。 但是，该员工的实际`HiredDate`未日历控件，从而导致每个默认为显示当前月份和日期的日历控件中任意位置设置值。 若要解决此问题，我们需要分配每个雇员`HiredDate`对日历控件[SelectedDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selecteddate(VS.80).aspx)并[VisibleDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.visibledate(VS.80).aspx)属性。

从日历控件的智能标记，选择编辑 DataBindings。 接下来，将两者绑定`SelectedDate`并`VisibleDate`属性设置为`HiredDate`数据字段。


[![将的 SelectedDate 和 VisibleDate 属性绑定到 HiredDate 数据字段](using-templatefields-in-the-gridview-control-cs/_static/image38.png)](using-templatefields-in-the-gridview-control-cs/_static/image37.png)

**图 13**： 将绑定`SelectedDate`并`VisibleDate`属性设置为`HiredDate`数据字段 ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image39.png))


> [!NOTE]
> 日历控件的所选的日期不一定需要可见。 例如，日历可能有 8 月 1 日<sup>st</sup>、 1999 作为所选的日期，但会显示当前月份和年份。 日历控件的指定所选的日期和可视日期`SelectedDate`和`VisibleDate`属性。 由于我们希望这两个选择的员工`HiredDate`，并确保它显示我们需要将这两个到这些属性绑定`HireDate`数据字段。


在浏览器中查看网页时, 日历现在显示员工的雇用日期的月份，并选择该特定日期。


[![日历控件中显示该雇员的 HiredDate](using-templatefields-in-the-gridview-control-cs/_static/image41.png)](using-templatefields-in-the-gridview-control-cs/_static/image40.png)

**图 14**: 员工`HiredDate`日历控件中所示 ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image42.png))


> [!NOTE]
> 与我们到目前为止看到的所有示例，本教程中我们*不*设置`EnableViewState`属性设置为`false`为此 GridView。 此决策的原因是因为单击的日期的日历控件导致回发，只需单击迄今为止设置日历的所选的日期。 如果禁用了 GridView 的视图状态，但是，每次回发 GridView 的数据会重新绑定到其基础数据源，这会导致要设置的日历的所选的日期*回*到员工的`HireDate`、 覆盖用户选择日期。


本教程中这是毫无意义了讨论，因为用户不能更新员工的`HireDate`。 它可能是最佳配置，以便其日期不可选择的日历控件。 无论如何，本教程演示，在某些情况下启用视图状态必须是为了提供特定功能。

## <a name="step-4-showing-the-number-of-days-the-employee-has-worked-for-the-company"></a>步骤 4： 显示该雇员的天数已在公司工作的

到目前为止我们看到 Templatefield 的两个应用的程序：

- 将两个或多个数据字段值组合到一列和
- 表示数据字段值而不文本中使用的 Web 控件

使用第三个 Templatefield 中显示有关 GridView 的元数据基础数据。 除了显示员工的雇佣日期，例如，我们可能还想要有一列显示多少就已经在该作业的总天数。

尚未 Templatefield 的另一种用法中，会出现方案时的基础数据需要不是在数据库中存储的格式，以不同的方式显示网页报表中。 想象一下`Employees`表有`Gender`存储字符字段`M`或`F`以指示该员工的性别。 在网页中显示此信息时，我们可能需要将显示为"Male"或"Female"，而不是只需"M"或"F"显示性别。

这两个方案可以通过创建处理*格式设置方法*ASP.NET 页面的代码隐藏类中 (或在单独的类库，作为实现`static`方法) 调用从模板。 此类的格式设置方法调用从使用相同的数据绑定语法前面介绍的模板。 格式设置方法可以采用任意数量的参数，但必须返回一个字符串。 此返回的字符串是注入到模板的 HTML。

为了说明这一概念，让我们提供了本教程中要显示列，其中列出了某位员工已在作业总天数。 此格式设置方法将采用`Northwind.EmployeesRow`对象，并且返回的员工已使用字符串形式的天数。 此方法可以添加到 ASP.NET 页面的代码隐藏类，但*必须*标记为`protected`或`public`以便可从该模板。


[!code-csharp[Main](using-templatefields-in-the-gridview-control-cs/samples/sample5.cs)]

由于`HiredDate`字段可以包含`NULL`数据库的值我们必须首先确保该值不是`NULL`然后继续进行计算。 如果`HiredDate`值是`NULL`，我们只需返回字符串"Unknown"; 如果不是`NULL`，我们计算当前时间之间的差异和`HiredDate`值并返回的天数。

若要利用此方法需要调用中使用数据绑定语法 GridView TemplateField 从。 首先通过单击 GridView 的智能标记中的编辑列链接并添加新 templatefield 进一步将新 TemplateField 添加到 GridView。


[![将新 TemplateField 添加到 GridView](using-templatefields-in-the-gridview-control-cs/_static/image44.png)](using-templatefields-in-the-gridview-control-cs/_static/image43.png)

**图 15**： 将新 TemplateField 添加到 GridView ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image45.png))


设置此新 TemplateField`HeaderText`属性设置为"作业的天上"并将其`ItemStyle`的`HorizontalAlign`属性设置为`Center`。 若要调用`DisplayDaysOnJob`方法从该模板后，将添加`ItemTemplate`，并使用以下数据绑定语法：


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample6.aspx)]

`Container.DataItem` 返回`DataRowView`对象对应于`DataSource`记录绑定到`GridViewRow`。 其`Row`属性返回强类型`Northwind.EmployeesRow`，它会传递给`DisplayDaysOnJob`方法。 此数据绑定语法可以出现在直接`ItemTemplate`（如下面的声明性语法中所示） 或可分配给`Text`标签 Web 控件的属性。

> [!NOTE]
> 或者，而不是传入`EmployeesRow`实例中，我们可能只需传递`HireDate`值使用`<%# DisplayDaysOnJob(Eval("HireDate")) %>`。 但是，`Eval`方法将返回`object`，因此我们将需要更改我们`DisplayDaysOnJob`方法签名，以接受类型的输入的参数`object`，改为。 我们不能隐式强制转换`Eval("HireDate")`调用`DateTime`因为`HireDate`中的列`Employees`表可以包含`NULL`值。 因此，我们将需要接受`object`作为输入参数`DisplayDaysOnJob`方法中，如果它有一个数据库检查`NULL`值 (可以使用完成其`Convert.IsDBNull(objectToCheck)`)，并相应地继续。


由于这些微妙之处，我选择将在整个`EmployeesRow`实例。 在下一教程，我们将了解使用的多个调整示例`Eval("columnName")`将输入的参数传递到格式设置方法的语法。

以下显示了声明性语法我们 GridView 在后已添加 TemplateField 并`DisplayDaysOnJob`方法从调用`ItemTemplate`:


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample7.aspx)]

图 16 显示了已完成本教程中，通过浏览器查看时。


[![显示员工已在该作业的日期数](using-templatefields-in-the-gridview-control-cs/_static/image47.png)](using-templatefields-in-the-gridview-control-cs/_static/image46.png)

**图 16**: 天数显示员工已在作业上 ([单击以查看实际尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image48.png))


## <a name="summary"></a>总结

在 GridView 控件中的 TemplateField 允许更高程度的灵活性比其他字段控件显示数据。 Templatefield 非常适合的情况下其中：

- 多个数据字段需要一个 GridView 列中显示
- 最好使用 Web 控件，而不是纯文本格式表示数据
- 输出取决于基础数据，例如显示元数据或重新格式化数据

除了自定义数据的显示，Templatefield 还可用于自定义的用户界面，用于编辑和插入数据，正如我们将在将来看到教程。

接下来两个教程继续了解模板，看在 DetailsView 中使用 Templatefield 从开始。 接下来，我们将会打开到 FormView，使用模板而非字段来提供更大的灵活性的布局和数据的结构。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Dan Jagers。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](custom-formatting-based-upon-data-cs.md)
> [下一页](using-templatefields-in-the-detailsview-control-cs.md)
