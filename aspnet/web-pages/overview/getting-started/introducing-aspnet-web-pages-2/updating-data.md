---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: Introducing ASP.NET 网页-更新数据库的数据 |Microsoft Docs
author: tfitzmac
description: 本教程演示如何使用 ASP.NET Web Pages (Razor) 时，更新 （更改） 的现有数据库条目。 它假定你已完成一系列第...
ms.author: aspnetcontent
ms.date: 01/02/2018
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: 948f5b5933669a43bf37dc0317ad644660dc67e9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842897"
---
<a name="introducing-aspnet-web-pages---updating-database-data"></a>ASP.NET 网页简介-更新数据库数据
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本教程演示如何使用 ASP.NET Web Pages (Razor) 时，更新 （更改） 的现有数据库条目。 它假定你已完成通过时序[输入数据通过使用窗体使用 ASP.NET Web Pages](entering-data.md)。
> 
> 你将学习：
> 
> - 如何选择中的单个记录`WebGrid`帮助器。
> - 如何从数据库中读取一条记录。
> - 如何预加载窗体中的数据库记录的值。
> - 如何更新数据库中的现有记录。
> - 如何在页面中存储信息，而不会显示它。
> - 如何使用隐藏的字段来存储信息。
>   
> 
> 功能/技术讨论：
> 
> - `WebGrid`帮助器。
> - SQL`Update`命令。
> - `Database.Execute` 方法。
> - 隐藏字段 (`<input type="hidden">`)。


## <a name="what-youll-build"></a>你将生成

在前面的教程，您学习了如何将一条记录添加到数据库。 在这里，您将了解如何以显示用于编辑的记录。 在中*电影*页上，你将更新`WebGrid`帮助程序，以便它显示**编辑**每部电影旁边的链接：

![WebGrid 显示包括每部电影的编辑链接](updating-data/_static/image1.png)

当您单击**编辑**链接，它将您带入不同的页的电影信息已在窗体：

![编辑电影页面，其中显示要编辑的电影](updating-data/_static/image2.png)

您可以更改的任何值。 当提交所做的更改时，页面中的代码将更新数据库，并将影片列表返回。

此过程的一部分方法几乎完全相同*AddMovie.cshtml*因此本教程的大部分将熟悉在上一教程中，创建的页。

有几种方法可以实现编辑单个电影的方法。 选择显示的方法是因为它是易于实现且易于理解。

## <a name="adding-an-edit-link-to-the-movie-listing"></a>添加到电影列表的编辑链接

若要开始，你将更新*电影*页上，以便每个电影列表也包含**编辑**链接。

打开*Movies.cshtml*文件。

在页面的正文中，更改`WebGrid`通过添加列的标记。 下面是修改后的标记：

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

新列是这样一个：

[!code-html[Main](updating-data/samples/sample2.html)]

本专栏的重点是说明链接 (`<a>`元素) 的文本显示的是"编辑"。 我们所期望是创建页运行时，如以下所示的链接使用`id`每部电影的不同值：

[!code-css[Main](updating-data/samples/sample3.css)]

此链接将调用一个名为页*EditMovie*，以及它将传递查询字符串`?id=7`到该页。

新列的语法可能看起来有点复杂，但这只是因为汇集多个元素。 每个元素非常简单。 如果您专注于只需`<a>`元素，请参阅此标记：

[!code-html[Main](updating-data/samples/sample4.html)]

有关网格的工作方式的一些背景信息： 网格显示行，分别针对每个数据库记录，并显示数据库记录中的每个字段的列。 构造每个网格行时，虽然`item`对象包含该行的数据库记录 （项）。 此安排使代码来访问数据，为该行中一种方法。 这就是，请参阅此处： 表达式`item.ID`获取当前的数据库项的 ID 值。 您可以通过使用得到的任何数据库值 （标题、 genre 或年） 相同的方式`item.Title`， `item.Genre`，或`item.Year`。

表达式`"~/EditMovie?id=@item.ID`结合了硬编码一部分的目标 URL (`~/EditMovie?id=`) 与此动态派生的 id。 (您看到的那样`~`运算符在上一教程; 它是一个表示当前网站根目录的 ASP.NET 运算符。)

结果是标记的，这一部分的列中只是标记的生成类似于以下标记的内容在运行时：

[!code-xml[Main](updating-data/samples/sample5.xml)]

当然，实际值的`id`将不同的每一行。

## <a name="creating-a-custom-display-for-a-grid-column"></a>创建自定义显示的网格列

现在回网格列。 三个列最初必须显示网格的唯一数据值 （标题、 genre 和年份）。 通过将数据库列的名称传递指定此显示&mdash;例如， `grid.Column("Title")`。

这一新**编辑**链接列是不同。 指定列名称，而不传递`format`参数。 此参数允许你定义标记的`WebGrid`帮助器将呈现连同`item`列数据显示为粗体或绿色或在任何格式，您需要的值。 例如，如果您希望该标题以粗体显示，您可以创建如下例所示的列：

[!code-html[Main](updating-data/samples/sample6.html)]

(的各种`@`中看到的字符`format`属性标记的标记和代码值之间的转换。)

一旦您知道的关于`format`属性，它是更轻松地了解如何新**编辑**链接列结合在一起：

[!code-html[Main](updating-data/samples/sample7.html)]

列组成*仅*的呈现链接的标记，以及某些信息 (ID)，从提取的行的数据库记录。

> [!TIP]
> 
> **命名的参数和一个方法的位置参数**
> 
> 很多时候时调用的一个方法并传递给它的参数后，你只是已加入由逗号分隔的参数值。 以下为若干示例：
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> 当第一次看到此代码中，但每种情况下，您要将参数传递给以特定顺序的方法时，我们没有提过问题&mdash;即，在该方法中定义参数的顺序。 有关`db.Execute`和`Validation.RequireFields`，如果您混您传递的值的顺序，则会得到一条错误消息页运行时或至少一些奇怪的结果。 很明显，您必须知道传递中的参数顺序。 （在 WebMatrix 中，IntelliSense 可帮助您了解出名称、 类型和参数的顺序图。）
> 
> 作为按顺序将值传递的替代方法，你可以使用*命名参数*。 (按顺序传递参数即为使用*位置参数*。)对于命名参数，则可以传递它的值时显式包括到参数的名称。 已命名的参数已多次在使用这些教程。 例如：
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> 和
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> 命名的参数可以方便地几个情况下的尤其是当某方法采用多个参数。 一个是当你想要传递只能将一个或两个参数，但你想要传递的值不是在参数列表中的第一个位置。 当你想要通过将参数传递给您最有利的顺序，使代码更具可读性时，另一种情况。
> 
> 显然，若要使用命名的参数，您需要知道的参数的名称。 WebMatrix IntelliSense 可以*显示*您的名称，但它不能当前它们为你填充。


## <a name="creating-the-edit-page"></a>创建编辑页

现在，你可以创建*EditMovie*页。 当用户单击**编辑**链接，它们就会在此页上。

创建一个名为页*EditMovie.cshtml*和替换为以下标记文件中：

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

这种标记和代码是类似于中有*AddMovie*页。 没有提交按钮的文本略有不同。 如同*AddMovie*页上，没有`Html.ValidationSummary`如果有的话，将显示验证错误的调用。 这次我们要离开掉调用`Validation.Message`，因为在验证摘要中将显示错误。 上一教程中所述，您可以在各种组合中使用验证摘要和单独的错误消息。

再次请注意，`method`的属性`<form>`元素设置为`post`。 如同*AddMovie.cshtml*页上，此页进行更改到数据库。 因此，此窗体中应执行`POST`操作。 (有关详细信息之间的差异`GET`和`POST`操作，请参阅[GET、 POST 和 HTTP 谓词安全](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety)HTML 窗体上本教程中的边栏。)

正如在前面的教程，你看到`value`Razor 代码与预加载其设置属性的文本框。 这一次，不过，你使用的变量，诸如`title`并`genre`而不是该任务`Request.Form["title"]`:

`<input type="text" name="title" value="@title" />`

为之前，此标记将预加载的电影值的文本框值。 为什么很方便地使用变量这一次而不是使用的稍后将看到`Request`对象。

此外，还有`<input type="hidden">`此页上的元素。 此元素而不使其可见的页上存储的电影 ID。 ID 最初传递到页上，通过使用查询字符串值 (`?id=7`或类似的 URL 中)。 通过将 ID 值放入隐藏的字段，您可以确保便可提交窗体时，即使不再有权访问调用页时使用了原始 URL。

与不同*AddMovie*页上的代码*EditMovie*页有两个不同的功能。 第一个函数是，在第一次显示的页时 (并*仅*然后)，代码从查询字符串获取电影 ID。 然后，此代码使用 ID 来读取相应电影移出数据库，并显示 （预先加载） 它在文本框中。

第二个函数是，当用户单击**提交更改**按钮，代码都需要读取的值的文本框和对其进行验证。 代码还必须使用新值更新数据库项。 此技术是类似于添加一条记录中所示*AddMovie*。

## <a name="adding-code-to-read-a-single-movie"></a>添加代码来读取单个电影

若要执行的第一个函数，将此代码添加到页的顶部：

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

此代码的大部分是在启动块内`if(!IsPost)`。 `!`运算符表示"not，"因此，该表达式表示*如果此请求不是 post 提交*，这是说的间接方法*此请求是否已运行此页的第一个时间*。 如前文所述，应运行此代码*仅*首次运行时页面。 如果未将中的代码`if(!IsPost)`，它会运行每次页面调用时，是否第一次或响应按钮单击。

请注意，该代码包含`else`阻止这一次。 正如我们所说时我们引入了`if`块，有时你想要运行替代代码，如果您要测试的条件不是这样。 这是此处的示例。 如果满足条件 （即，如果传递到页的 ID 为确定），您可以从数据库读取行。 但是，如果条件未通过，`else`块运行和代码设置一条错误消息。

## <a name="validating-a-value-passed-to-the-page"></a>验证传递到页的值

该代码使用`Request.QueryString["id"]`获取传递到页面的 ID。 代码可确保实际 id 传递的值 如果不传递的任何值，该代码设置验证错误。

此代码显示了不同的方式来验证信息。 在上一教程中，您使用过`Validation`帮助器。 注册字段，若要验证，并且 ASP.NET 自动未验证，并通过使用显示的错误`Html.ValidationMessage`和`Html.ValidationSummary`。 在这种情况下，但是，你在实际上不验证用户输入。 相反，你在验证从其他位置传递到页一个值。 `Validation`帮助程序不会为您做的。

因此，您自行检查值，通过测试其与`if(!Request.QueryString["ID"].IsEmpty()`)。 如果没有问题，可以通过使用显示错误`Html.ValidationSummary`，就像处理一样`Validation`帮助器。 若要执行此操作，请调用`Validation.AddFormError`并将其传递要显示的消息。 `Validation.AddFormError` 为使您可以定义自定义消息，同时结合使用您已经熟悉了验证系统的内置方法。 （稍后在本教程中我们将介绍有关如何进行此验证过程更加强大。）

确保没有将电影的 ID 之后, 代码读取数据库，查找仅为单个数据库项。 (您可能已经注意到常规模式，用于数据库操作： 打开数据库，定义 SQL 语句，然后运行该语句。)这一次，SQL`Select`语句中包含`WHERE ID = @0`。 ID 是唯一的因为只有一条记录可能会返回。

通过执行查询`db.QuerySingle`(不`db.Query`，如用于电影列表)，然后代码将放入结果`row`变量。 名称`row`是任意的; 您喜欢的任何命名变量。 在顶部进行初始化的变量将然后填入电影详细信息，以便可以在文本框中显示这些值。

## <a name="testing-the-edit-page-so-far"></a>测试编辑页 （到目前为止）

如果你想要测试您的页面，运行*电影*现在页，然后单击**编辑**任何电影旁边的链接。 你将看到*EditMovie*为所选的电影的详细信息页填充：

![编辑电影页面，其中显示要编辑的电影](updating-data/_static/image3.png)

请注意，页面的 URL 包含类似于`?id=10`（或其他一些号码）。 到目前为止您已测试**编辑**中的链接*电影*页上工作，您的页面从查询字符串读取 ID 和查询数据库以获取单个电影记录是否正常工作。

可以更改电影信息，但当您单击时没有任何反应**提交更改**。

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a>添加代码以使用用户的更改更新电影

在中*EditMovie.cshtml*文件中，若要实现第二个函数 （保存更改），添加以下代码置于右大括号的`@`块。 (如果不确定如何将代码放在则可以查看[完整代码列表的编辑电影页面](#Complete_Page_Listing_for_EditMovie)，在本教程的最后阶段显示。)

[!code-csharp[Main](updating-data/samples/sample12.cs)]

同样，此标记和代码是类似于中的代码*AddMovie*。 代码位于`if(IsPost)`阻止，因为仅当用户单击时，在运行此代码**提交更改**按钮&mdash;，即当 （和仅当） 发送窗体。 在这种情况下，不使用像测试`if(IsPost && Validation.IsValid())`— 也就是说，在不合并这两个测试通过使用 and。 在此页上，您首先确定是否提交窗体 (`if(IsPost)`)，然后仅注册用于验证的字段。 然后可以测试验证结果 (`if(Validation.IsValid()`)。 流的方向是中略有不同*AddMovie.cshtml*页上，但效果是相同。

使用获取的值的文本框`Request.Form["title"]`和其他类似的代码`<input>`元素。 请注意，这一次，此代码可获取电影 ID 移出隐藏字段 (`<input type="hidden">`)。 当页面运行了第一次时，代码必须从查询字符串的 ID。 从隐藏的字段，以确保在从那时起，查询字符串以某种方式更改的情况下您将获得的最初所显示的电影 ID 获取的值。

真正重要区别*AddMovie*代码和此代码是在此代码中使用 SQL`Update`语句而不是`Insert Into`语句。 下面的示例显示了 SQL 的语法`Update`语句：

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

可以按任意顺序指定的任何列，则不一定必须更新期间的每个列`Update`操作。 (不能更新与 ID 本身，因为这实际上将保存该记录为一个新的记录，并为不允许的`Update`操作。)

> [!NOTE] 
> 
> **重要**`Where`子句具有 ID 是非常重要，因为这是数据库如何知道哪个数据库记录你想要更新。 如果您离开`Where`子句中，数据库将更新*每个*记录在数据库中。 在大多数情况下，会是一场灾难。


在代码中，要更新的值传递到 SQL 语句使用占位符。 若要重复我们曾经说过： 出于安全原因*仅*占位符用于将值传递给 SQL 语句。

该代码使用后`db.Execute`运行`Update`语句，它将重定向回列表页，其中可以看到所做的更改。

> [!TIP] 
> 
> **不同的 SQL 语句，不同的方法**
> 
> 您可能已经注意到使用略有不同的方法来运行不同的 SQL 语句。 若要运行`Select`查询，它可能返回多个记录，则使用`Query`方法。 若要运行`Select`您知道的查询将返回一个数据库项，则使用`QuerySingle`方法。 若要运行的命令进行更改，但不返回数据库项，请使用`Execute`方法。
> 
> 您必须具有不同的方法，因为每个返回不同的结果，正如您已看到之间的差异`Query`和`QuerySingle`。 (`Execute`方法实际上返回一个值还&mdash;即的数据库行受影响的命令数&mdash;但您忽略了，到目前为止。)
> 
> 当然，`Query`方法可能返回只有一个数据库行。 但是，ASP.NET 始终处理的结果`Query`作为集合的方法。 即使该方法返回一个行，您必须从集合中提取这一行。 因此，在情况下，你*知道*您就会得到只包含一行，它就会更方便地使用`QuerySingle`。
> 
> 有几个其他执行特定类型的数据库操作的方法。 您可以查找数据库中的方法的列表[ASP.NET Web Pages API 快速参考](../../api-reference/asp-net-web-pages-api-reference.md#Data)。


## <a name="making-validation-for-the-id-more-robust"></a>使稳健，验证 ID 详细信息

第一次运行页面时，你获取电影 ID 从查询字符串，以便您可以从数据库中获取该电影。 您已确保实际时出现的值去寻找机会，未使用此代码：

[!code-csharp[Main](updating-data/samples/sample13.cs)]

此代码用于可以确保，如果用户到达*EditMovies*页，但没有首先选择电影*电影*页上，页面将显示一条用户友好错误消息。 （否则，用户会看到一个错误，将可能只需将它们混淆。）

但是，此验证不太可靠。 页面也可能使用这些错误的调用：

- ID 不是一个数字。 例如，页面可能调用使用的 URL，例如`http://localhost:nnnnn/EditMovie?id=abc`。
- ID 是一个数字，但它引用了不存在的电影 (例如， `http://localhost:nnnnn/EditMovie?id=100934`)。

如果您想要查看从这些 Url，运行产生的错误*电影*页。 选择要编辑的电影，然后更改的 URL *EditMovie* ID 或不存在电影 ID 到包含字母的 URL 页上。

因此，您该怎么办？ 第一个解决方法是确保该不只一个 ID 传递到页上，但 ID 是一个整数。 更改的代码`!IsPost`测试看起来如下例所示：

[!code-csharp[Main](updating-data/samples/sample14.cs)]

已添加到第二个条件`IsEmpty`测试与链接`&&`（逻辑与）：

[!code-csharp[Main](updating-data/samples/sample15.cs)]

可能会从记得[ASP.NET Web Pages 编程介绍](../introducing-razor-syntax-c.md)等方法的教程`AsBool``AsInt`将字符字符串转换为其他数据类型。 `IsInt`方法 (和其他人，喜欢`IsBool`和`IsDateTime`) 类似。 但是，它们仅用于测试是否您*可以*转换的字符串，而不实际执行转换。 因此，在这里基本上就*如果查询字符串值可以转换为整数...*.

其他潜在问题正在寻求不存在的电影。 若要获取电影的代码如下所示代码所示：

[!code-csharp[Main](updating-data/samples/sample16.cs)]

如果传递`movieId`值设为`QuerySingle`不对应于任何实际电影的方法，未返回任何内容且后面的语句 (例如， `title=row.Title`) 导致的错误。

同样是容易解决此问题。 如果`db.QuerySingle`方法会返回任何结果，`row`变量将为 null。 这样您就可以检查是否`row`变量为 null，然后再尝试从其获取值。 下面的代码添加`if`获取的值的语句周围的块`row`对象：

[!code-csharp[Main](updating-data/samples/sample17.cs)]

使用这两个其他验证测试，页面变得更高防护。 完整代码`!IsPost`分支现在看起来如下例所示：

[!code-csharp[Main](updating-data/samples/sample18.cs)]

我们注意一次此任务是有关充分利用`else`块。 如果测试未通过，`else`块设置错误消息。

## <a name="adding-a-link-to-return-to-the-movies-page"></a>添加用于返回到电影页面的链接

最后一个也是很有帮助的详细信息将添加一个链接回*电影*页。 在普通的事件流中，用户将开始处*电影*页上，单击**编辑**链接。 将用户带到*EditMovie*页上，它们可以在其中编辑电影并单击按钮。 代码已处理更改后，它将重定向回到*电影*页。

但是：

- 用户可能会决定不需进行任何更改。
- 用户可能没有先单击此页收到**编辑**中的链接*电影*页。

无论哪种方式，你想要使其能够方便地返回到主列表。 很容易解决此问题&mdash;恰好在关闭后添加以下标记`</form>`标记的标记中：

[!code-html[Main](updating-data/samples/sample19.html)]

此标记使用的相同语法`<a>`您所见到其他位置的元素。 URL 中包括`~`来表示"root 的网站。

## <a name="testing-the-movie-update-process"></a>测试电影更新过程

现在，可以测试。 运行*电影*页，然后单击**编辑**旁边电影。 当*EditMovie*页出现后，更改到电影，然后单击**提交更改**。 电影列表出现时，请确保显示所做的更改。

若要确保验证正常工作，请单击**编辑**为另一个的电影。 转到*EditMovie*页上，清除**流派**字段 (或**年**字段，或两者) 并尝试提交所做的更改。 如您所料，将看到一个错误：

![编辑电影页面，其中显示验证错误](updating-data/_static/image4.png)

单击**返回到的电影列表**链接以放弃所做的更改并返回到*电影*页。

## <a name="coming-up-next"></a>即将推出下一步

在下一步的教程中，您将了解如何删除电影记录。

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a>电影页面 （使用编辑链接更新） 的完整列表

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a>完成编辑电影页的页列表

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a>其他资源

- [使用 Razor 语法的 ASP.NET Web 编程简介](../../getting-started/introducing-razor-syntax-c.md)
- [SQL UPDATE 语句](http://www.w3schools.com/sql/sql_update.asp)W3Schools 站点上

> [!div class="step-by-step"]
> [上一页](entering-data.md)
> [下一页](deleting-data.md)
