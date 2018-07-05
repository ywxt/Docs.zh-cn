---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: Introducing ASP.NET 网页-通过使用窗体输入数据库的数据 |Microsoft Docs
author: tfitzmac
description: 本教程演示如何创建输入窗体，然后输入数据时收到的窗体中插入数据库表使用 ASP.NET Web Pages （...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: 41122b3bca5a3d3162a66be163642610b8349cc5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386402"
---
<a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a>Introducing ASP.NET 网页-通过使用窗体输入数据库数据
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本教程演示如何创建输入窗体，然后输入你从获取窗体到数据库表时使用 ASP.NET Web Pages (Razor) 的数据。 它假定你已完成通过时序[基础知识的 HTML 窗体在 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581)。
> 
> 你将学习：
> 
> - 有关如何处理输入窗体的详细信息。
> - 如何在数据库中添加数据 （插入）。
> - 如何确保用户具有在窗体 （如何验证用户输入） 中输入所需的值。
> - 如何显示验证错误。
> - 如何从当前页跳转到另一个页面。
>   
> 
> 功能/技术讨论：
> 
> - `Database.Execute` 方法。
> - SQL`Insert Into`语句
> - `Validation`帮助器。
> - `Response.Redirect` 方法。


## <a name="what-youll-build"></a>你将生成

通过编辑直接在 WebMatrix 中，使用数据库的数据库数据输入在本教程前面部分介绍了如何创建数据库，**数据库**工作区。 在大多数应用中，这不是一个实用方法可将数据放入数据库，不过。 因此在本教程中，您将创建一个基于 web 的界面，允许你或输入数据并将其保存到数据库的任何人。

你将创建可在其中输入新影片的页面。 该页将包含有您可以在其中输入电影标题、 genre 和年份字段 （文本框） 的输入窗体。 页面将类似于此页：

![在浏览器中添加电影页](entering-data/_static/image1.png)

文本框中将 HTML`<input>`元素看起来像此标记：

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a>创建基本的条目窗体

创建一个名为页*AddMovie.cshtml*。

替换为以下标记文件中。 覆盖所有内容;你稍后将在顶部添加代码块。

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

此示例显示创建窗体的典型 HTML。 它使用`<input>`元素的文本框和提交按钮。 文本框中的标题通过使用标准创建`<label>`元素。 `<fieldset>`和`<legend>`元素周围放置一个很好框窗体。

请注意，在此页上，`<form>`元素使用`post`的值作为`method`属性。 在上一教程中，创建使用窗体`get`方法。 因为窗体提交到服务器的值，尽管请求未进行任何更改，这是正确的。 它做不同的方式已提取数据。 但是，在此页您*将*进行更改，您要添加新的数据库记录。 因此，应使用此窗体`post`方法。 (有关详细信息之间的差异`GET`和`POST`操作，请参阅[GET、 POST 和 HTTP 谓词安全](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety)边栏上一教程中的。)

请注意，每个文本框中有`name`元素 (`title`， `genre`， `year`)。 正如您看到在上一教程，这些名称非常重要，因为您必须具有这些名称，以便稍后获取用户的输入。 可以使用任何名称。 会有所帮助使用有意义名称帮助你记住您正在使用哪些数据。

`value`属性的每个`<input>`元素包含的 Razor 代码 (例如， `Request.Form["title"]`)。 提交窗体后，可以保留 （如果有） 在文本框中输入的值在上一教程中学习的这一技巧的版本。

## <a name="getting-the-form-values"></a>获取窗体值

接下来，你添加代码，用于处理窗体。 在大纲中，将执行以下操作：

1. 检查是否正在发布页面 （已提交）。 要为你的代码仅时用户已单击按钮，不是在页面首次运行时运行。
2. 获取用户在文本框中输入的值。 在这种情况下，因为使用窗体`POST`谓词，则获取从窗体值`Request.Form`集合。
3. 将值插入新记录中作为*电影*数据库表。

在文件顶部，添加以下代码：

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

前几行创建变量 (`title`， `genre`，和`year`) 以从文本框中保存的值。 在行`if(IsPost)`可确保设置变量*仅*当用户单击**添加电影**按钮 — 也就是说，当窗体已发布。

正如您看到在前面的教程，获取文本框的值使用之类的表达式`Request.Form["name"]`，其中*名称*的名称`<input>`元素。

变量的名称 (`title`， `genre`，和`year`) 是任意的。 喜欢将分配给名称`<input>`元素，您可以您喜欢的任何调用它们。 (变量的名称并不必一致的名称属性`<input>`窗体上的元素。)但是，如使用`<input>`元素，它是一个好办法使用反映它们所包含的数据的变量名称。 当你编写代码时，采用一致的名称轻松记住您正在使用哪些数据。

## <a name="adding-data-to-the-database"></a>向数据库添加数据

你只需添加了，只需在代码中分组*内*右大括号 ( `}` ) 的`if`块 （而不仅仅是在代码块中） 中，添加以下代码：

[!code-csharp[Main](entering-data/samples/sample3.cs)]

此示例中是类似于前面的教程，提取和显示数据中使用的代码。 开头的行`db =`此时会打开数据库，如前面一样，和下一步的行定义 SQL 语句，再次为您之前看到的一样。 但是，这次它定义 SQL`Insert Into`语句。 下面的示例演示的常规语法`Insert Into`语句：

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

换而言之，你指定的表将插入，然后列出的列将插入，并列出要插入的值。 （如前面提到的 SQL 不区分大小写，但有些人首字母大写要更加轻松地阅读命令的关键字。）

在命令中将已列出中的插入的列 — `(Title, Genre, Year)`。 有趣的部分是如何从到文本框中获取值`VALUES`命令的一部分。 而不是实际值，请参阅`@0`， `@1`，和`@2`，这当然是占位符。 运行命令时 (在`db.Execute`行)，传递从文本框中获取的值。

**重要提示！** 请记住，您应包含输入的 SQL 语句中的用户的联机数据的唯一方法是使用占位符，如下所示 (`VALUES(@0, @1, @2)`)。 如果连接到 SQL 语句中的用户输入，则打开自己容易受到 SQL 注入攻击，如中所述[窗体基础知识在 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581) （上一个教程）。

仍内`if`块中，添加以下行后的`db.Execute`行：

[!code-css[Main](entering-data/samples/sample4.css)]

新电影已插入到数据库后，此行将跳转 （重定向） 到*电影*页，以便您可以看到刚才输入的电影。 `~`运算符表示"root 的网站。 (`~`运算符只能在 ASP.NET 页中，不在 HTML 中通常运行。)

完整的代码块如以下示例所示：

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a>测试插入命令 （到目前为止）

您还未完成，但现在是测试的好时机。

在 WebMatrix 中的文件树视图中，右键单击*AddMovie.cshtml*页，然后单击**浏览器中启动**。

![在浏览器中添加电影页](entering-data/_static/image2.png)

(如果您最终在浏览器中的其他页，请确保该 URL 是否`http://localhost:nnnnn/AddMovie`)，其中*nnnnn*是正在使用的端口号。)

遇到一个错误页面吗？ 如果是这样，请仔细阅读，并确保，代码看上去完全什么已在前面列出。

在表单中输入电影&mdash;例如，使用"公民 Kane"、"剧本"和"1941"。 （或任何内容。）然后单击**添加电影**。

如果一切顺利，将重定向到*电影*页。 请确保新电影已列出。

![显示新电影页面添加电影](entering-data/_static/image3.png)

## <a name="validating-user-input"></a>验证用户输入

返回到*AddMovie*页上，或再次运行。 输入另一个 movie，但这次，输入仅标题&mdash;例如，输入"上线 ' 中 Rain"。 然后单击**添加电影**。

将重定向到*电影*页。 您可以找到新电影，但不完整。

![电影页上显示缺少某些值的新电影](entering-data/_static/image4.png)

在创建时*电影*表中，你显式所说的任何字段可以为 null。 在此有新电影的输入窗体和要将字段留空。 这是一个错误。

在这种情况下，数据库没有实际引发 (或*引发*) 错误。 不能因此提供流派或两年中的代码*AddMovie*页被作为所谓处理这些值*空字符串*。 当 SQL`Insert Into`运行命令、 流派和年份字段中，没有有用的数据，但它们并不为 null。

显然，您不想让用户输入到数据库中每半空电影信息。 解决方案是验证用户的输入。 最初，验证将只需确保用户具有的所有字段中都输入的值 （也就是说，该其中任何一个包含空字符串）。

> [!TIP]
> 
> **Null 和空字符串**
> 
> 在编程中，是区分不同的"空值。"概念 一般情况下，当值*null*如果它永远不会设置或已以任何方式初始化。 与此相反，需要字符数据 （字符串） 的变量可以设置为*空字符串*。 在这种情况下，值不是 null。它只是已显式设置为其长度为零的字符的字符串。 这两个语句显示的差异：
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> 它具有更复杂一些，但重要的一点是`null`表示一种不确定状态。
> 
> 现在，然后务必了解完全值为 null 时，只是空字符串时。 中的代码*AddMovie*页中，您通过使用获取的值的文本框`Request.Form["title"]`，依此类推。 当页面第一次运行 （在您单击的按钮） 之前，值`Request.Form["title"]`为 null。 当您提交窗体，但是`Request.Form["title"]`获取的值`title`文本框。 它不是显而易见的但一个空文本框不为 null;它只是在其中具有空字符串。 因此在代码运行以响应该按钮时单击，`Request.Form["title"]`中有一个空字符串。
> 
> 为什么这一区别很重要？ 在创建时*电影*表中，你显式所说的任何字段可以为 null。 在此有新电影的输入窗体，但要将字段留空。 合理地预期要抱怨尝试保存新影片，但没有流派或年份的值时的数据库。 但关键在于&mdash;即使将这些文本框留空，值不为 null; 它们是空字符串。 因此，您可以将新电影保存到具有这些列空数据库&mdash;但不是为 null ！ &mdash; 值。 因此，您必须确保用户不提交空字符串，可以通过验证用户的输入来执行此操作。


### <a name="the-validation-helper"></a>验证帮助程序

ASP.NET Web 页面包括一个帮助程序&mdash;`Validation`帮助器&mdash;可用于确保用户输入符合你要求的数据。 `Validation`帮助器是一个内置到 ASP.NET Web Pages 中，因此无需将其作为安装包使用 NuGet，在前面的教程安装 Gravatar 帮助程序的方式的帮助器。

若要验证用户的输入，将执行以下操作：

- 使用代码来指定你希望要求页面上的文本框中的值。
- 代码中插入一个测试，以便仅当所有内容正确验证，电影信息添加到数据库。
- 将代码添加到标记以显示错误消息。

在中的代码块*AddMovie*页上，向右向上变量声明前，顶部添加以下代码：

[!code-csharp[Main](entering-data/samples/sample7.cs)]

在调用`Validation.RequireField`一次针对每个字段 (`<input>`元素) 想要要求一个条目。 此外可以添加的自定义错误消息的每个调用，如所示。 （我们不同的消息只是为了说明，可以将您喜欢的任何那里）。

如果没有问题，你想要防止新电影信息插入到数据库。 在中`if(IsPost)`块中，使用`&&`（逻辑与） 添加另一个条件，它测试`Validation.IsValid()`。 完成后，整个`if(IsPost)`块代码所示：

[!code-csharp[Main](entering-data/samples/sample8.cs)]

如果没有任何使用注册的字段的验证错误`Validation`帮助器，`Validation.IsValid`方法返回 false。 而这种情况下，在该块中的代码都不会运行，因此任何无效的电影条目将不插入到数据库。 当然您在不重定向到*电影*页。

完整的代码块，包括验证代码，现在看起来如下例所示：

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a>显示验证错误

最后一步是要显示任何错误消息。 可以显示各个消息的每个验证错误时，也可以显示和 / 或摘要。 对于本教程，您将执行这两，以便您可以看到其工作原理。

每旁边`<input>`要验证的元素，请调用`Html.ValidationMessage`方法并将其传递的名称`<input>`你在验证的元素。 您将放`Html.ValidationMessage`方法右想要显示的错误消息。 当该页运行时，则`Html.ValidationMessage`方法还呈现`<span>`会验证错误的元素。 (如果没有错误，`<span>`元素呈现，但其中没有任何文本。)

更改页面中的标记，以便它包含`Html.ValidationMessage`方法的三个`<input>`元素在页面上，如下例所示：

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

若要查看摘要的工作原理，还添加以下标记和代码之后`<h1>Add a Movie</h1>`页面上的元素：

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

默认情况下`Html.ValidationSummary`方法以列表形式显示所有验证消息 (`<ul>`内元素`<div>`元素)。 与使用`Html.ValidationMessage`方法，始终呈现验证摘要的标记; 如果没有任何错误，没有列表项呈现。

摘要可以是一种方法来显示验证消息，而不是通过使用`Html.ValidationMessage`方法来显示每个特定于字段的错误。 或者，可以使用摘要和详细信息。 也可以使用`Html.ValidationSummary`方法以显示一般错误，然后使用单个`Html.ValidationMessage`调用以显示详细信息。

完成页现在看起来如下例所示：

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

介绍完毕。 现在可以通过添加电影，但是省去一个或多个字段来测试页。 执行操作时，您将看到显示了以下错误：

![添加电影页面，其中显示验证错误消息](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a>设置验证错误消息的样式

您可以看到的错误消息，但它们不真正与众不同很好。 没有错误消息，但设置样式的简单方法。

通过显示的单个错误消息的样式`Html.ValidationMessage`，创建一个名为的 CSS 样式类`field-validation-error`。 若要定义验证摘要的外观，请创建一个名为的 CSS 样式类`validation-summary-errors`。

若要查看此技术的工作原理，请添加`<style>`元素内的`<head>`页部分。 然后定义名为的样式类`field-validation-error`和`validation-summary-errors`包含以下规则：

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

通常情况下您可能会将放到单独的样式信息 *.css*文件，但为简单起见，可以将其放在页面现在。 (稍后在本教程系列中将移动到一个单独的 CSS 规则 *.css*文件。)

如果没有验证错误时，`Html.ValidationMessage`方法还呈现`<span>`元素包含`class="field-validation-error"`。 通过添加该类的样式定义，可以配置消息如下所示。 如果有错误，`ValidationSummary`方法将同样动态呈现属性`class="validation-summary-errors"`。

再次运行该页并有意遗漏了几个字段。 错误现更明显。 （事实上，它们过度，但这是只是为了说明可以执行的操作。）

![添加电影页面，其中显示已设置样式的验证错误](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a>将链接添加到电影页面

最后一步是使其可以方便地到达*AddMovie*页上从原始的电影列表。

打开*电影*页。 关闭之后`</div>`标记后面`WebGrid`帮助器，添加以下标记：

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

正如您看到之前，ASP.NET 将解释`~`运算符用作在网站的根目录。 无需使用`~`运算符; 您可以使用标记`<a href="./AddMovie">Add a movie</a>`或通过其他方式来定义 HTML 能够理解的路径。 但`~`运算符是一个好常规方法时创建链接，了解 Razor 页面，因为它使站点更灵活，如果当前页移动到子文件夹时，该链接将仍请转到*AddMovie*页。 (请记住，`~`运算符仅适用于 *.cshtml*页。 ASP.NET 理解它，但它不是标准 HTML）。

完成后，运行*电影*页。 它将类似此页：

![电影页面，其中包含指向添加电影页](entering-data/_static/image7.png)

单击**添加电影**链接，以确保它进入*AddMovie*页。

## <a name="coming-up-next"></a>即将推出下一步

在下一步的教程中，您将了解如何让用户编辑已在数据库中的数据。

## <a name="complete-listing-for-addmovie-page"></a>AddMovie 页的完整列表

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a>其他资源

- [使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkID=202890)
- [INTO 语句中插入的 SQL](http://www.w3schools.com/sql/sql_insert.asp) W3Schools 站点上
- [验证用户输入在 ASP.NET Web Pages 站点](https://go.microsoft.com/fwlink/?LinkId=253002)。 详细了解如何使用`Validation`帮助器。

> [!div class="step-by-step"]
> [上一页](form-basics.md)
> [下一页](updating-data.md)
