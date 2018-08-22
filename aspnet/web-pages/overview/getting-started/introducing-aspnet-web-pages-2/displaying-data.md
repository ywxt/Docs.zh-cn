---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
title: Introducing ASP.NET 网页-显示数据 |Microsoft Docs
author: tfitzmac
description: 本教程演示了如何在 WebMatrix 中创建数据库以及如何使用 ASP.NET Web Pages (Razor) 时，在页面中显示数据库数据。 它假定 y...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: b3a006a0-3ea2-4d45-b833-e20e3a3c0a1a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
msc.type: authoredcontent
ms.openlocfilehash: 864b9f7826763e307368706116458678abf50d3b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826622"
---
<a name="introducing-aspnet-web-pages---displaying-data"></a>ASP.NET 网页简介-显示数据
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本教程演示了如何在 WebMatrix 中创建数据库以及如何使用 ASP.NET Web Pages (Razor) 时，在页面中显示数据库数据。 它假定你已完成通过时序[ASP.NET Web Pages 编程简介](../introducing-razor-syntax-c.md)。
> 
> 你将学习：
> 
> - 如何使用 WebMatrix 工具创建一个数据库和数据库表。
> - 如何使用 WebMatrix 工具将数据添加到数据库。
> - 如何在页面上显示数据库中的数据。
> - 如何运行 ASP.NET Web Pages 中的 SQL 命令。
> - 如何自定义`WebGrid`帮助器来更改数据显示并添加分页和排序。
>   
> 
> 功能/技术讨论：
> 
> - WebMatrix 数据库工具。
> - `WebGrid` 帮助器。


## <a name="what-youll-build"></a>你将生成

在上一教程中，已引入到 ASP.NET Web Pages (*.cshtml*文件)、 Razor 语法的基础知识以及帮助程序。 在本教程中，将开始创建你将在本系列的其余部分使用的实际 web 应用程序。 该应用是一个简单的影片应用程序，可用于查看、 添加、 更改和删除的有关信息。

完成本教程后，你将能够查看类似于此页的影片列表：

![包含参数的 WebGrid 显示设置为 CSS 类名称](displaying-data/_static/image1.png)

但若要开始，你必须创建一个数据库。

## <a name="a-very-brief-introduction-to-databases"></a>非常简单介绍了数据库

本教程将提供仅 briefest 引入到数据库。 如果你有数据库的经验，可以跳过此较短的节。

数据库包含一个或多个表包含的信息&mdash;例如，表为客户、 订单和供应商或面向学生、 教师、 类和成绩。 在结构上，数据库表就像电子表格。 想象一下典型的通讯簿。 通讯簿中的每个项 (即，每个用户) 包含一些相关的信息，例如名字、 姓氏、 地址、 电子邮件地址和电话号码。

![为简单网格的示例数据库表](displaying-data/_static/image2.png)

(行有时称为*记录*，和列有时称为*字段*。)

对于大多数数据库表，该表必须具有包含唯一值，如客户编号、 帐号，等的列。 此值称为表的*主键*，并使用它来标识表中的每个行。 在示例中，ID 列是在前面的示例所示的通讯簿的主键。

很多 web 应用程序中所做的工作包括： 读取数据库中的信息并显示在页面上。 通常还会从用户收集信息，并将其添加到数据库，或将修改在数据库中已存在的记录。 （我们将介绍所有这些操作在本教程系列的过程中。）

数据库工作可能会很大差别很复杂，可能需要专业的知识。 对于此教程的集，不过，您必须了解仅基本概念，其将所有解释意愿。

## <a name="creating-a-database"></a>创建数据库

WebMatrix 包含工具，可以轻松创建数据库和数据库中创建表。 (数据库的结构的数据库称为*架构*。)本教程系列中，你将创建在其中具有只有一个表的数据库&mdash;电影。

如果还没有，请打开 WebMatrix 并打开在上一教程中创建的 WebPagesMovies 站点。

在左窗格中，单击**数据库**工作区。

![WebMatrix 数据库工作区选项卡](displaying-data/_static/image3.png)

此功能区改为显示与数据库相关的任务。 在功能区中，单击**新的数据库**。

![在 WebMatrix 功能区中的新建数据库按钮](displaying-data/_static/image4.png)

WebMatrix 创建 SQL Server CE 数据库 ( *.sdf*文件) 作为你的站点具有相同名称&mdash; *WebPagesMovies.sdf*。 (不会执行此操作，但您可以重命名文件到您喜欢的任何内容，只要它具有 *.sdf*扩展。)

## <a name="creating-a-table"></a>创建表

在功能区中，单击**新表**。 WebMatrix 将在新选项卡中打开表设计器。（如果新的表选项不可用，请确保在左侧树视图中选择了新的数据库。）

![在 WebMatrix 功能区中的新建表按钮](displaying-data/_static/image5.png)

在顶部 （其中水印显示"输入表名称"） 文本框中，输入"电影"。

![在 WebMatrix 数据库设计器中输入表名称](displaying-data/_static/image6.png)

下表名称的窗格是你在其中定义单个列。 有关*电影*表在本教程中，你将创建只有几列： *ID*， *Title*，*流派*，和*年*.

在中**名称**框中，输入"ID"。 输入的值在此处激活新列的所有控件。

Tab 键切换至**数据类型**列表，然后选择**int**。此值指定 ID 列将包含整数 （数字） 数据。

> [!NOTE]
> 我们不会对它进行任何此处详细 （得多），但可以使用标准 Windows 键盘手势来在此网格中导航。 例如，您可以使用 tab 键字段之间，就可以开始键入以在列表中，选择一个项，依次类推。


过去的选项卡**默认值**框 （即，将其留空）。 Tab 键切换至**是 Primary Key**复选框，然后选择它。 此选项让数据库知道*ID*列将包含标识单个行的数据。 （即，每一行将具有唯一的值可用于查找行的 ID 列中。）

选择**是标识**选项。 此选项将指示数据库，它应自动生成每个新行的下一个序列号。 (**是标识**仅当你已选择选项的工作原理**是 Primary Key**选项。)

在下一步的网格行中，单击或按 Tab 两次以完成当前行。 任一手势将保存当前行，并启动下一个。 请注意，**默认值**列现在显示**Null**。 （null 是默认值的默认值众人皆知了。）

当您已完成定义新**ID**列中，在设计器看起来类似于此图中：

![WebMatrix 定义电影表的 ID 列后的数据库设计器](displaying-data/_static/image7.png)

若要创建下一专栏中，单击在框中，在**名称**列。 输入列"Title"，然后选择**nvarchar**有关**数据类型**值。 "Var"一部分**nvarchar**告诉数据库，此列的数据将一个字符串，其大小可能会记录到记录。 ("N"前缀表示"国家/地区，"指示字段可以保存任何字母表或书写的字符数据 — 即，该字段将持有 Unicode 数据。)

当你选择**nvarchar**，另一台计算机将显示可以为字段输入的最大长度。 输入 50，假定您将使用在本教程中没有电影标题将超过 50 个字符。

跳过**默认值**并清除**允许 null 值**选项。 您不希望数据库以允许任何电影以输入到数据库中不具有标题。

当您已完成并移动到下一行时，在设计器看起来像此图中：

![WebMatrix 定义电影表的标题列后的数据库设计器](displaying-data/_static/image8.png)

重复这些步骤创建列长度，除了名为"流派"，将其设置为只需 30。

创建名为"年份"。 另一个列 对于数据类型中，选择**nchar** (不**nvarchar**) 并将长度设置为 4。 为一年中，您将使用 4 位数字，如"1995"或"2010"，因此不需要的大小可变的列。

下面是已完成的设计如下所示：

![WebMatrix 数据库设计器后的所有字段都定义为电影表](displaying-data/_static/image9.png)

按 Ctrl + S 或单击**保存**中快速访问工具栏按钮。 通过关闭选项卡关闭数据库设计器。

## <a name="adding-some-example-data"></a>添加了一些示例数据

稍后在本系列教程中，你将创建可以在窗体中输入新影片的页面。 但是，现在，可以添加然后可以在页面显示一些示例数据。

在中**数据库**在 WebMatrix 中，请注意，没有一个树，它显示了您的工作区 *.sdf*前面创建的文件。 打开您的新节点 *.sdf*文件，然后打开**表**节点。

![与树到电影表打开 WebMatrix 数据库工作区](displaying-data/_static/image10.png)

右键单击**电影**节点，然后选择**数据**。 WebMatrix 将打开一个网格，您可以在其中输入数据*电影*表：

![在 WebMatrix 中 （空） 的数据库条目网格](displaying-data/_static/image11.png)

单击**标题**列并输入"时 Harry 满足 Sally"。 将移动到**流派**列 （您可以使用 Tab 键），然后输入"浪漫喜剧"。 将移动到**年**列并输入"1989":

![在 WebMatrix 中具有一条记录的数据库条目网格](displaying-data/_static/image12.png)

按 Enter，，WebMatrix 将保存新电影。 请注意， **ID**已填充列。

![在 WebMatrix 中使用一条记录和自动生成的 ID 的数据库条目网格](displaying-data/_static/image13.png)

输入另一个 movie （例如，"已与风暴"、"剧本"，"1939"）。 重新填充 ID 列：

![在 WebMatrix 中使用两条记录和自动生成 Id 的数据库条目网格](displaying-data/_static/image14.png)

输入 （例如，"Ghostbusters"、"喜剧"） 的第三个电影。 试验一下，将保留**年**列保留为空，然后按 Enter。 因为您未选中**允许 null 值**选项，数据库将显示错误：

![如果所需的列的值为空时，显示数据无效错误](displaying-data/_static/image15.png)

单击**确定**以返回并修复 （"Ghostbusters"的年份是 1984年） 的条目，然后按 Enter。

在将 8 之前或以便填写几个电影。 （输入 8 可以更轻松地使用分页更高版本。 但如果真是太多，输入现在几。）实际数据并不重要。

![在 WebMatrix 中使用任一记录的数据库条目网格](displaying-data/_static/image16.png)

如果输入未出现任何错误的所有电影，ID 值是连续的。 如果您尝试保存不完整的电影记录，可能不是顺序的 ID 号。 如果是这样，没关系。 数字没有任何固有含义，并仅是重要的一点是，它们是在唯一*电影*表。

关闭包含数据库设计器的选项卡。

现在就可以开始在网页上显示此数据。

## <a name="displaying-data-in-a-page-by-using-the-webgrid-helper"></a>使用 WebGrid 帮助器页中显示数据

若要在页面中显示数据，您将使用`WebGrid`帮助器。 此帮助器生成的网格或表 （行和列） 中显示。 正如您将看到，您将可以优化使用格式设置和其他功能的网格。

若要运行网格，您必须编写几行代码。 这几行可作为一种类型的几乎所有在本教程中执行数据访问模式。

> [!NOTE]
> 实际上有许多选项可用于页面; 上显示数据`WebGrid`帮助程序只是其中一个。 我们选择它对于本教程并显示数据的最简单方法是因为它是相当灵活。 在下一步的教程系列中，将看到如何使用更多的"手动"方法来处理页上，可以更直接控制如何显示数据中的数据。


在 WebMatrix 中左窗格中，单击**文件**工作区。

创建的新数据库处于*应用程序\_数据*文件夹。 如果文件夹尚不存在，WebMatrix 将创建它为新的数据库。 （该文件夹可能已存在于如果以前已安装了帮助程序。）

在树视图中，选择在网站的根目录。 必须选择网站; 的根否则，新的文件可能会添加到应用\_数据文件夹。

在功能区中，单击**新建**。 在中**选择文件类型**框中，选择**CSHTML**。

在中**名称**框中，命名新页面"Movies.cshtml":

![选择文件类型对话框中显示电影页](displaying-data/_static/image17.png)

单击**确定**按钮。 WebMatrix 使用在其中一些框架元素中打开一个新文件。 首先将编写一些代码来从数据库获取数据。 然后会将标记添加到页后，可以实际显示的数据。

### <a name="writing-the-data-query-code"></a>编写数据查询代码

在页上，顶部之间`@{`和`}`字符，输入以下代码。 （请确保开始标记和右大括号之间输入此代码。）

[!code-csharp[Main](displaying-data/samples/sample1.cs)]

第一行将打开之前创建的数据库即始终第一个步骤执行与数据库的内容之前。 您告诉`Database.Open`要打开的数据库的方法名称。 请注意，不包括 *.sdf*名称中。 `Open`方法假定它寻找 *.sdf*文件 (即*WebPagesMovies.sdf*)， *.sdf*文件位于*应用\_数据*文件夹。 (前面我们介绍的*应用程序\_数据*保留文件夹; 这种情况下是在其中 ASP.NET 会假设该名称的位置之一。)

打开数据库时，将对它的引用放入名为变量`db`。 （这可命名为任何内容。）`db`变量是如何您就会与数据库交互。

第二行实际上会提取数据库数据，通过使用`Query`方法。 请注意，此代码的工作方式：`db`变量具有对打开的数据库的引用并调用`Query`方法使用`db`变量 (`db.Query`)。

在查询本身是一个 SQL`Select`语句。 （有关 sql 的一些背景信息，请参阅说明更高版本）。在语句中，`Movies`标识查询的表。 `*`字符指定查询应返回表中的所有列。 （你可能还列出列单独，用逗号隔开。）

的查询，如果有的话，返回结果并将在`selectedData`变量。 同样，该变量可命名为任何内容。

最后，第三行告知了 ASP.NET 你想要使用的实例`WebGrid`帮助器。 创建 (*实例化*) 使用的帮助程序对象`new`关键字并将其传递通过查询结果`selectedData`变量。 新`WebGrid`对象，以及数据库查询的结果可按`grid`变量。 在一段时间来实际在页中显示数据中，你将需要该结果。

在此阶段，打开该数据库，您已经看到了数据，并已准备好`WebGrid`使用该数据的帮助程序。 下一步是在页面中创建标记。

> [!TIP] 
> 
> **结构化的查询语言 (SQL)**
> 
> SQL 是一种语言，用在大多数关系数据库的管理数据库中的数据。 该指南包含的命令，用于检索数据并更新它，并能够让你创建、 修改和管理数据库表中的数据。 SQL 是不同于编程语言 （如 C# 中)。 Sql，您告诉数据库所需的并且数据库的作业，以了解如何获取数据或执行任务。 下面是一些 SQL 命令的示例，以及他们执行的操作：
> 
> `Select * From Movies`
> 
> `SELECT ID, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> 第一个`Select`语句获取的所有列 (通过指定`*`) 从*电影*表。
> 
> 第二个`Select`语句从记录中提取的 ID、 名称和价格的列*产品*其价格列的值是 10 个以上的表。 该命令的名称列的值的按字母顺序返回结果。 如果没有记录符合价格条件，该命令将返回一个空集。
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ('Croissant', 'A flaky delight', 1.99)`
> 
> 此命令将插入新记录划分*产品*表中，将名称列"新月形面包"、"A 不可靠兴致勃勃"到说明列和价格设置为 1.99。
> 
> 请注意，在指定的非数字值时，值括在单引号 （不双引号括起，与 C#）。 使用这些引号周围文本或日期值，但不是围绕数字。
> 
> `DELETE FROM Product WHERE ExpirationDate < '01/01/2008'`
> 
> 此命令删除中的记录*产品*其到期日期列是早于 2008 年 1 月 1 日的表。 (该命令假定*产品*表当然有这样的列。)此处采用 MM/DD/YYYY 格式输入日期，但它应在你的区域设置使用的格式输入。
> 
> `Insert`和`Delete`命令不返回结果集。 相反，它们返回一个数字，告知你多少条记录受影响的命令。
> 
> 对于某些操作 （如插入和删除记录），请求操作的进程必须在数据库中具有适当的权限。 这就是为什么用于生产数据库通常必须将连接到数据库时提供用户名和密码。
> 
> 有许多 SQL 命令，但它们都遵循类似的命令所示的模式。 SQL 命令可用于创建数据库表、 计算的表中的记录数、 计算价格，和执行很多更多操作。


### <a name="adding-markup-to-display-the-data"></a>添加标记以显示数据

内部`<head>`元素中，集的内容的`<title>`"Movies"的元素：

[!code-html[Main](displaying-data/samples/sample2.html?highlight=3)]

内部`<body>`元素的页上，添加以下：

[!code-html[Main](displaying-data/samples/sample3.html)]

介绍完毕。 `grid`变量是在创建时创建的值`WebGrid`前面代码中的对象。

在 WebMatrix 树视图中，右键单击页并选择**浏览器中启动**。 你将看到类似于此页的内容：

![电影表中的默认 WebGrid 帮助器输出](displaying-data/_static/image18.png)

单击列标题链接以按该列排序。 可以通过单击标题排序是一项功能内置于**WebGrid**帮助器。

`GetHtml`方法，如其名称所示，将生成标记，显示的数据。 默认情况下`GetHtml`方法将生成一个 HTML`<table>`元素。 （如果你想，您可以验证呈现通过查看页面在浏览器中的源。）

## <a name="modifying-the-look-of-the-grid"></a>修改查找范围的网格

使用`WebGrid`帮助器就像很容易，但生成的显示是普通。 `WebGrid`帮助者各种类型的选项可让你控制数据的显示方式。 有太多，以浏览本教程中，但此部分可让你了解这些选项的一些。 本系列教程的后续教程中我们将介绍几个其他选项。

### <a name="specifying-individual-columns-to-display"></a>指定显示的单个列

若要开始，可以指定你想要显示的那些列。 默认情况下，如您所见，该网格将显示所有四个中的列*电影*表。

在中*Movies.cshtml*文件，将为`@grid.GetHtml()`刚添加以下标记：

[!code-css[Main](displaying-data/samples/sample4.css)]

若要指示帮助者要显示的列，则包含`columns`参数`GetHtml`方法并传入列的集合。 在集合中，您可以指定要包含每个列。 指定单独的列以显示通过包括`grid.Column`对象，并传入所需的数据列的名称。 (这些列必须包含在 SQL 查询结果-`WebGrid`帮助器无法显示未由查询返回的列。)

启动*Movies.cshtml*试，并在此时获得类似于以下显示在浏览器中的页面 （请注意，显示没有 ID 列）：

![WebGrid 显示仅所选的列](displaying-data/_static/image19.png)

### <a name="changing-the-look-of-the-grid"></a>更改查找范围的网格

有很多更多选项用于显示的列，其中一些将在此集中的后续教程中探讨了。 现在，本节将向您介绍可以在其中设置样式为整个网格的方式。

内部`<head>`页上，只需在关闭前一节`</head>`标记中，添加以下`<style>`元素：

[!code-css[Main](displaying-data/samples/sample5.css)]

此 CSS 标记定义了名为的类`grid`， `head`，依次类推。 您还可以将这些样式定义在单独 *.css*文件，并链接到的页。 （事实上，您将实现更高版本在本教程系列中。）但为了方便起见就本教程来说，它们在显示的数据的同一页面内。

现在可以获取`WebGrid`帮助者使用这些样式类。 帮助程序具有多个属性 (例如， `tableStyle`) 实现此目的 — 将 CSS 样式类名称分配给它们，并且该类的名称呈现为呈现的帮助程序的标记的一部分。

更改`grid.GetHtml`标记使它现在如下所示代码所示：

[!code-css[Main](displaying-data/samples/sample6.css)]

已添加的新是`tableStyle`， `headerStyle`，并`alternatingRowStyle`参数`GetHtml`方法。 这些参数已设置为刚才添加的 CSS 样式的名称。

运行此页面，和此时会显示一个网格，看起来比太普通之前：

![包含参数的 WebGrid 显示设置为 CSS 类名称](displaying-data/_static/image20.png)

若要查看什么`GetHtml`生成的方法，您可以查看页面在浏览器中的源。 我们将不会详细说明，但重要的一点是，通过指定参数，例如`tableStyle`，导致网格生成 HTML 标记，如下所示：

`<table class="grid">`

`<table>`标记有`class`引用了一个先前添加的 CSS 规则的属性添加到它。 此代码演示了基本模式&mdash;不同的参数`GetHtml`方法让您引用 CSS 类以及标记，然后生成该方法。 使用 CSS 类做什么是取决于您。

## <a name="adding-paging"></a>添加分页

作为本教程的最后一个任务，你将向网格添加分页。 现在，它是任何一次显示所有电影的问题。 但如果添加数百个电影，页面显示将会很长。

在页代码中，创建的行更改`WebGrid`对象为以下代码：

[!code-csharp[Main](displaying-data/samples/sample7.cs)]

与之前的唯一区别是你添加的`rowsPerPage`参数设置为 3。

运行页。 该网格显示时间，加上导航链接，使您的数据库中电影翻页 3 行：

![使用分页 WebGrid 显示](displaying-data/_static/image21.png)

## <a name="coming-up-next"></a>即将推出下一步

在下一步的教程中，您将了解如何使用 Razor 和 C# 代码来获取窗体中的用户输入。 以便您可以找到按标题或流派的电影，您将添加到电影页面搜索框。

## <a name="complete-listing-for-movies-page"></a>电影页的完整列表

[!code-cshtml[Main](displaying-data/samples/sample8.cshtml)]

## <a name="additional-resources"></a>其他资源

- [使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkID=202890)

> [!div class="step-by-step"]
> [上一页](intro-to-web-pages-programming.md)
> [下一页](form-basics.md)
