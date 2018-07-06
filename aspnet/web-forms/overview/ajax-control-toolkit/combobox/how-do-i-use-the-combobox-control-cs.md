---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: 如何使用组合框控件？ (C#) |Microsoft Docs
author: microsoft
description: 组合框是 ASP.NET AJAX 控件，将文本框的灵活性与用户可以从中选择的选项的列表相结合。
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 2589fe79b56d3794b46b3da84c96f6e0283c61a7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37373362"
---
<a name="how-do-i-use-the-combobox-control-c"></a>如何使用组合框控件？ (C#)
====================
by [Microsoft](https://github.com/microsoft)

> 组合框是 ASP.NET AJAX 控件，将文本框的灵活性与用户可以从中选择的选项的列表相结合。


本教程的目的是说明 AJAX 控件工具包组合框控件。 组合框类似于标准的 ASP.NET DropDownList 控件和文本框控件之间的组合。 您可以从预先存在的项列表中选择或输入新的项目。

组合框类似于自动完成控件扩展程序，但在不同方案中使用的控件。 AutoComplete 扩展器查询 web 服务以获取匹配项。 与此相反，组合框控件中，使用一组项的初始化。 使用记忆式键入功能扩展器使您正在使用大量的数据 （数以百万计的汽车部件） 时使用组合框控件时有意义使用少量的数据时 （数十个汽车部件）。

## <a name="selecting-from-a-static-list-of-items"></a>从项的静态列表中选择

让我们来开始使用组合框控件的简单示例。 想象你想要在下拉列表中显示的项的静态列表。 但是，你想要保持打开状态的列表不完整的可能性。 你想要允许用户输入到列表的自定义值。

我们将创建新的 ASP.NET Web 窗体页面和页面中使用组合框控件。 向项目添加新的 ASP.NET 页面和切换到设计视图。

如果你想要在页面中使用组合框控件必须将 ScriptManager 控件添加到页面。 从地板下面传来 AJAX 扩展选项卡将 ScriptManager 控件拖动到设计器图面。 应在页顶部添加 ScriptManager 控件将其添加下面打开服务器端的立即&lt;窗体&gt;标记。

接下来，将组合框控件拖到绘图页上。 在工具箱中与其他 AJAX 控件工具包控件和控件扩展程序 （请参阅图 1），可以查找组合框控件。


[![用于创建名片的简单窗体](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**图 01**： 从工具箱中选择组合框控件 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-cs/_static/image2.png))


我们将使用组合框控件以显示选择的静态列表。 用户可以从三个选项的列表中选择其食物的 spiciness 一个特殊级别： 暴力、 中和热 （请参见图 2）。


[![从项的静态列表中选择](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**图 02**： 从项的静态列表中选择 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-cs/_static/image4.png))


有两种方法可以将这些选项添加到组合框控件。 首先，将鼠标悬停在设计视图中的控件时选择任务编辑选项选项并打开项编辑器中 （请参见图 3）。


[![编辑组合框项](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**图 03**： 编辑组合框项 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-cs/_static/image6.png))


第二个选项是添加列表项之间的开始和结束&lt;asp： 组合框&gt;源视图中的标记。 在列表 1 中的页面包含更新组合框具有项的列表。

**代码清单 1-Static.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

当在列表 1 中打开页时，您可以选择预先存在的选项之一组合框中的。 换而言之，组合框的工作方式相似 DropDownList 控件。

但是，你还具有输入 （例如，超级辣味） 现有列表中不是一个新选择的选项。 因此，组合框还工作原理类似 TextBox 控件。

无论是否选择预先存在的项，或输入自定义项，在提交窗体中，所选标签控件中显示时。 当您提交窗体 btnSubmit\_单击处理程序执行并更新标签 （请参阅图 4）。


[![显示选定的项](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**图 04**： 显示选定的项 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-cs/_static/image8.png))


组合框用于提交窗体后检索所选的项支持与 DropDownList 控件相同的属性：

- SelectedItem.Text-显示所选的项的 Text 属性的值。
- SelectedItem.Value-显示所选的项的 Value 属性的值或显示组合框中键入的文本。
- SelectedValue 的不同之处在于此属性可以指定默认值 （初始） 选定的项与 SelectedItem.Value 相同。

如果您键入到组合框选择然后自定义的自定义选择分配给 SelectedItem.Text 和 SelectedItem.Value 属性。

## <a name="selecting-the-list-of-items-from-the-database"></a>从数据库中选择项的列表

您可以从数据库中检索项的组合框显示的列表。 例如，可以将组合框绑定到 SqlDataSource 控件、 ObjectDataSource 控件、 LinqDataSource 或 EntityDataSource。

想象你想要在组合框中显示的影片列表。 你想要从电影数据库表中检索的影片列表。 请执行这些步骤：

1. 创建一个名为 Movies.aspx 页
2. 通过在工具箱中拖到页面上将从 AJAX 扩展选项卡下的 ScriptManager 将 ScriptManager 控件添加到页面。
3. 将组合框控件添加到页面中，通过将组合框拖到绘图页上。
4. 在设计视图中，请将鼠标悬停在组合框控件，然后选择**选择数据源**任务选项 （请参见图 5）。 启动数据源配置向导。
5. 在中**选择数据源**步骤中，选择&lt;新数据源&gt;选项。
6. 在中**选择数据源类型**步骤中，选择数据库。
7. 在中**选择数据连接**步骤中，选择你的数据库 (例如，MoviesDB.mdf)。
8. 在中**将连接字符串保存到应用程序配置文件**步骤中，选择选项以保存你的连接字符串。
9. 在中**配置 Select 语句**步骤中，选择的电影数据库表，然后选择的所有列。
10. 在中**测试查询**步骤中，单击完成按钮。
11. 回到**选择数据源**步骤中，选择要显示的字段的标题列和 Id 列的数据字段 （见图）。
12. 单击确定按钮以关闭向导。


[![选择数据源](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**图 05**： 选择数据源 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-cs/_static/image10.png))


[![选择数据的文本和值字段](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**图 06**： 选择数据的文本和值字段 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-cs/_static/image12.png))


完成上述步骤后，组合框绑定到表示电影的电影数据库表从 SqlDataSource 控件。 页面的源如下所示 （我清除格式设置有点） 的代码清单 2。

**代码清单 2-Movies.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

请注意，ComboBox 控件包含指向 SqlDataSource 控件的 DataSourceID 属性。 当在浏览器中打开页时，请显示电影从数据库列表 （请参阅图 7）。 可以是提取电影从列表中或通过在组合框中键入电影输入新电影。


[![显示电影列表](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**图 07**： 显示电影列表 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-cs/_static/image14.png))


## <a name="setting-the-dropdownstyle"></a>设置 DropDownStyle

组合框 DropDownStyle 属性可用于更改将组合框的行为。 此属性接受那里可能的值：

- 下拉列表中的 （默认值） 的组合框显示一个下拉列表列出当您单击的箭头，您可以输入自定义值。
- 简单的组合框会自动显示一个下拉列表，并且您可以输入自定义值。
- DropDownList 的组合框的工作方式相似 DropDownList 控件。

不同的下拉列表中之间和简单时显示的项的列表。 在简单的情况下立即时将焦点移到组合框显示的列表。 在下拉列表中，必须单击该箭头可查看的项的列表。

DropDownList 值会导致要使用标准的 DropDownList 控件一样的组合框控件。 但是，是一项重大的差异。 较旧版本的 Internet Explorer 显示具有无限的 z 索引的 DropDownList 控件，因此控件将显示它的前面放置任何控件的前面。 由于组合框呈现 HTML &lt;div&gt;而不是对应的 HTML 标记&lt;选择&gt;标记，组合框正确遵循 z 顺序。

## <a name="setting-the-autocompletemode"></a>设置 AutoCompleteMode

组合框 AutoCompleteMode 属性用于指定当有人到组合框中键入文本时，会发生什么情况。 此属性接受以下可能值：

- 无-（默认值） 组合框不提供任何自动完成行为。
- 建议的组合框显示的列表，并突出显示列表中的匹配项 （请参阅图 8）。
- 追加-组合框不会显示列表并将追加到键入内容 （请参阅图 9） 上的列表中的匹配项。
- SuggestAppend 的组合框同时显示的列表，并追加到键入内容 （请参阅图 10） 上的列表中的匹配项。


[![组合框使建议](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**图 08**: 组合框使建议 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-cs/_static/image16.png))


[![组合框将匹配的文本追加](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**图 09**： 组合框将匹配的文本追加 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-cs/_static/image18.png))


[![组合框会建议，并追加](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**图 10**: 组合框会建议，并追加 ([单击以查看实际尺寸的图像](how-do-i-use-the-combobox-control-cs/_static/image20.png))


## <a name="summary"></a>总结

在本教程中，您学习了如何使用组合框控件来显示一组固定的项。 我们绑定组合框控件，同时为静态设置的项和数据库表。 最后，您学习了如何通过设置其 DropDownStyle 和 AutoCompleteMode 属性来修改将组合框的行为。

> [!div class="step-by-step"]
> [下一篇](how-do-i-use-the-combobox-control-vb.md)
