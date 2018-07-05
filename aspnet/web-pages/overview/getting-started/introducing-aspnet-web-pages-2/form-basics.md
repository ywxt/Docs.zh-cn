---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: 介绍 ASP.NET 网页的 HTML 窗体基础知识 |Microsoft Docs
author: tfitzmac
description: 本教程演示如何创建输入窗体以及如何处理用户的输入时使用 ASP.NET Web Pages (Razor) 的基础知识。 和现在，您...
ms.author: aspnetcontent
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: 609c1c06ed8f29db82b5dd565a935440d4430819
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815390"
---
<a name="introducing-aspnet-web-pages---html-form-basics"></a>介绍 ASP.NET 网页的 HTML 窗体基础知识
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本教程演示如何创建输入窗体以及如何处理用户的输入时使用 ASP.NET Web Pages (Razor) 的基础知识。 和现在，您有一个数据库，将使用您的窗体技能以使用户可以在数据库中查找特定电影。 它假定你已完成通过时序[简介到显示数据使用 ASP.NET Web Pages](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)。
> 
> 你将学习：
> 
> - 如何通过使用标准 HTML 元素创建的窗体。
> - 如何读取用户的输入窗体中。
> - 如何创建 SQL 查询，有选择地获取数据使用的搜索词的用户提供。
> - 如何在页中"记住"用户输入的字段。
>   
> 
> 功能/技术讨论：
> 
> - `Request` 对象。
> - SQL`Where`子句。


## <a name="what-youll-build"></a>你将生成

在上一教程中，创建了一个数据库、 数据添加到它，然后使用`WebGrid`帮助器以显示数据。 在本教程中，将添加搜索框中，可以查找特定流派的电影或其标题包含您输入的任何单词。 （例如，你将能够找到所有电影流派"操作"或其标题包含"Harry"Adventure"。）

完成本教程后，将会得到类似此页：

![电影流派和标题搜索页](form-basics/_static/image1.png)

页的列表部分是与最后一个教程中的相同&mdash;网格。 区别是，网格将显示仅电影的搜索。

## <a name="about-html-forms"></a>有关 HTML 窗体

(如果您有体验与创建 HTML 窗体和之间的差异`GET`和`POST`，可以跳过此部分。)

窗体上有用户输入的元素&mdash;文本框、 按钮、 单选按钮、 复选框、 下拉列表和等等。 用户填写这些控件或进行选择，然后通过单击按钮提交窗体。

此示例中的窗体的基本 HTML 语法进行了说明：

[!code-html[Main](form-basics/samples/sample1.html)]

在页中运行此标记，将创建如图所示的简单窗体：

![作为在浏览器中呈现的基本 HTML 窗体](form-basics/_static/image2.png)

`<form>`元素包含要提交的 HTML 元素。 (若要使易犯错误是将元素添加到页面，但然后忘了将它们放`<form>`元素。 在这种情况下，执行任何操作提交。）`method`属性告知浏览器如何提交用户输入。 将其设置为`post`如果要执行的更新服务器上或`get`如果只从服务器提取数据。

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **GET、 POST 和 HTTP 谓词安全**
> 
> HTTP，浏览器和服务器交换信息，而使用的协议是在其基本操作非常简单。 浏览器中使用只有几个谓词向服务器发出请求。 在编写 web 的代码，是有助于您了解这些谓词和如何在浏览器和服务器使用它们。 无疑最常使用的谓词是：
> 
> - `GET`。 浏览器使用此谓词以从服务器提取的内容。 例如，当浏览器中键入 URL，浏览器执行`GET`操作来请求所需的页面。 如果页中包含图形，浏览器执行其他`GET`操作来获取映像。 如果`GET`操作必须将信息发送到服务器，作为查询字符串中的 URL 的一部分传递的信息。
> - `POST`。 浏览器发送`POST`请求，以便将数据要添加或更改服务器上提交。 例如，`POST`谓词用于在数据库中创建记录或更改现有的。 大多数情况下，如果窗体中填写，单击提交按钮，浏览器执行`POST`操作。 在`POST`操作中，传递给服务器的数据是在页的正文中。
> 
> 这些动词之间的重要区别在于`GET`操作不应在服务器上进行任何更改，或将其放在更抽象的方式，`GET`操作不会导致在服务器上的状态的更改。 你可以执行`GET`无数次，您喜欢，也不会更改这些资源的同一资源上的操作。 (A`GET`为"安全，"或使用技术术语，常说操作是*幂等*。)与之相反，当然，`POST`请求更改了某些内容在服务器上每次执行该操作。
> 
> 两个示例将帮助说明这一区别。 执行搜索时使用必应或 Google 等引擎包含一个文本框中，窗体中填充，然后单击搜索按钮。 浏览器执行`GET`操作，与作为 URL 的一部分传递在框中输入的值。 使用`GET`操作此类型的窗体是没问题，因为搜索操作不会更改服务器上的任何资源，只需提取信息。
> 
> 现在，考虑排序某些在线内容的过程。 您填写订单详细信息，然后单击提交按钮。 此操作将为`POST`请求，因为该操作将导致在服务器上，如新的订单记录、 你的帐户信息中的更改和可能是许多其他更改的更改。 与不同`GET`操作，不能重复你`POST`请求 — 如果您这样做，重新提交请求，每次会生成服务器上的新订单。 （在这种情况下，网站通常会警告你不要超过一次单击提交按钮或将禁用提交按钮，以便不会意外地重新提交该窗体。）
> 
> 在本教程的过程中将使用这两`GET`操作和一个`POST`操作以处理 HTML 窗体。 我们将介绍在每个事例的原因你使用的谓词是一个合适。
> 
> (若要了解有关 HTTP 谓词的详细信息，请参阅[方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)W3C 网站上的文章。)


大多数用户输入的元素以 HTML 为`<input>`元素。 它们看起来像`<input type="type" name="name">,`其中*类型*指示所需的用户输入控件的类型。 这些元素是常见的：

- 文本框中： `<input type="text">`
- 复选框： `<input type="check">`
- 单选按钮： `<input type="radio">`
- 按钮： `<input type="button">`
- 提交按钮： `<input type="submit">`

此外可以使用`<textarea>`元素以创建多行文本框和`<select>`元素来创建一个下拉列表或可滚动的列表。 (有关更多关于 HTML 窗体中的元素，请参阅[HTML 窗体和输入](http://www.w3schools.com/html/html_forms.asp)W3Schools 站点上。)

`name`属性是非常重要，因为该名称是如何将获取更高版本，该元素的值如稍后您将看到。

有趣的是你做些什么，页面开发人员，用户的输入。 没有与这些元素相关联的任何内置行为。 相反，您必须获取用户输入或选择的值并使用它们执行某些操作。 这就是将在本教程中了解的内容。

> [!TIP] 
> 
> **HTML5 和输入窗体**
> 
> 您可能知道，HTML 处于过渡状态，最新版本 (HTML5) 包括对更直观的方式将用户输入信息的支持。 例如，html5，您 （页面开发人员） 可以告诉页面所需用户输入日期。 然后可以自动显示在浏览器，日历，而不是要求用户手动输入日期。 但是，HTML5 新，尚不支持在所有浏览器中。
> 
> ASP.NET Web Pages 支持 HTML5 输入的范围内用户的浏览器 does。 新特性的了解`<input>`元素中 HTML5，请参阅[HTML&lt;输入&gt;键入属性](http://www.w3schools.com/html/html_form_input_types.asp)W3Schools 站点上。


## <a name="creating-the-form"></a>创建窗体

在 WebMatrix 中，在**文件**工作区中，打开*Movies.cshtml*页。

关闭之后`</h1>`标记并打开之前`<div>`标记的`grid.GetHtml`调用中，添加以下标记：

[!code-html[Main](form-basics/samples/sample2.html)]

此标记创建具有一个名为文本框的窗体`searchGenre`和一个提交按钮。 文本框并将其提交按钮括在`<form>`元素的`method`属性设置为`get`。 (请记住，如果不将文本框中，提交按钮内的`<form>`元素中，单击此按钮时，将提交执行任何操作。)您使用`GET`谓词此处因为您将创建一个窗体的不进行任何更改在服务器上 — 它只需在搜索结果。 (在前面的教程，您使用`post`方法，它是如何提交对服务器的更改。 您会看到，在下一教程中再次。）

运行页。 尽管尚未定义窗体的任何行为，但您可以看到如下所示：

![使用搜索框中的流派的电影页面](form-basics/_static/image3.png)

输入一个值，在文本框中，如"喜剧。" 然后单击**搜索流派**。

请注意页面的 URL。 因为您设置`<form>`元素的`method`属性为`get`，您输入的值现在是类似如下的 URL 中的查询字符串的一部分：

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>读取窗体值

该页面已包含一些代码，获取数据库数据，并在网格中显示结果。 现在您必须添加一些代码来读取文本框中的值，因此你可以运行包含搜索词的 SQL 查询。

因为窗体的方法设置为`get`，可以读取已通过使用如下所示的代码输入到文本框中的值：

`var searchTerm = Request.QueryString["searchGenre"];`

`Request.QueryString`对象 (`QueryString`的属性`Request`对象) 包含的已提交的一部分的元素值`GET`操作。 `Request.QueryString`属性包含*集合*（列表） 的形式提交的值。 若要获取任何单个值，指定所需的元素的名称。 这就是为什么您必须拥有`name`特性，可以在`<input>`元素 (`searchTerm`) 创建文本框。 (有关详细信息`Request`对象，请参阅[侧栏](#BKMK_TheRequestObject)更高版本。)

它非常简单，可以读取的文本框中的值。 但是，如果用户未输入任何内容，在文本框中，但单击**搜索**不管怎样，可以忽略该单击，因为没有要搜索内容。

以下代码是一个示例，演示如何实现这些条件。 （无需尚未添加此代码; 稍后将执行该操作。）

[!code-csharp[Main](form-basics/samples/sample3.cs)]

测试以这种方式分解：

- 获取的值`Request.QueryString["searchGenre"]`，即输入到的值`<input>`名为元素`searchGenre`。
- 了解它是否为空使用`IsEmpty`方法。 此方法是确定是否某些内容 （例如，窗体元素） 包含值的标准方法。 但实际上，处理仅当它具有*不*为空，因此...
- 添加`!`前的运算符`IsEmpty`测试。 (`!`运算符表示逻辑非)。

用通俗易懂，整个`if`条件转换为以下：*如果窗体的 searchGenre 元素不为空，然后...*

此块创造了用于创建使用搜索词的查询。 下一节中，将执行该操作。

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **请求对象**
> 
> `Request`对象包含请求或提交页面时浏览器发送到你的应用程序的所有信息。 此对象中包含用户提供，例如文本框值或要上载的文件的任何信息。 它还包括各种类型的其他信息，例如 cookie、 URL 查询字符串 （如果有） 中的值的页的正在运行的浏览器的用户正在使用，在浏览器中设置的语言的列表类型的文件路径以及更多。
> 
> `Request`对象是*集合*（列表） 的值。 通过指定其名称获取单个值超出集合：
> 
> `var someValue = Request["name"];`
> 
> `Request`对象实际上公开多个子集。 例如：
> 
> - `Request.Form` 直观显示值中的元素内提交`<form>`元素，该请求是否`POST`请求。
> - `Request.QueryString` 在为您提供的值只是 URL 的查询字符串。 (如 URL 中`http://mysite/myapp/page?searchGenre=action&page=2`，则`?searchGenre=action&page=2`URL 的部分是查询字符串。)
> - `Request.Cookies` 集合使您可以访问到浏览器发送的 cookie。
> 
> 若要获取一个值，您知道该值是在提交窗体中，可以使用`Request["name"]`。 或者，可以使用更具体的版本`Request.Form["name"]`(对于`POST`请求) 或`Request.QueryString["name"]`(对于`GET`请求)。 当然*名称*是要获取的项的名称。
> 
> 你想要获取的项的名称必须是要将的集合中唯一的。 这就是为什么`Request`对象提供子集喜欢`Request.Form`和`Request.QueryString`。 假设您的页面包含名为的窗体元素`userName`并*还*包含名为 cookie `userName`。 如果收到`Request["userName"]`，它是不明确所需的窗体值或 cookie。 但是，如果您收到`Request.Form["userName"]`或`Request.Cookie["userName"]`，您要对其显式要获取的值。
> 
> 很好的做法是特定的使用的子集`Request`感兴趣，如`Request.Form`或`Request.QueryString`。 对于要在本教程中创建的简单页面，它可能不会真正带来任何差异。 但是，当您创建更复杂的页，使用显式版本`Request.Form`或`Request.QueryString`可以帮助您避免出现问题时的页面包含一个窗体 （或多个窗体），可能出现的 cookie、 查询字符串值等。


## <a name="creating-a-query-by-using-a-search-term"></a>使用搜索词创建查询

既然您知道如何获取用户输入的搜索词，可以创建使用它的查询。 请记住，为获取在数据库之外的所有电影项目，你使用类似于此语句的 SQL 查询：

`SELECT * FROM Movies`

若要获取仅某些电影，您必须使用包含的查询`Where`子句。 此子句允许您设置由查询返回行的条件。 以下是一个示例：

`SELECT * FROM Movies WHERE Genre = 'Action'`

基本格式`WHERE column = value`。 除了只是可以使用不同的运算符`=`，例如`>`（大于）、 `<` （小于）， `<>` （不等于）、 `<=` （小于或等于）、 等等，具体取决于要查找的内容。

如果您想知道，SQL 语句不是区分大小写&mdash;`SELECT`等同于`Select`(或甚至`select`)。 但是，人们通常将首字母大写关键字在 SQL 语句中，如`SELECT`和`WHERE`，以使其更易于读取。

### <a name="passing-the-search-term-as-a-parameter"></a>作为参数传递的搜索词

搜索特定流派非常简单 (`WHERE Genre = 'Action'`)，但你想要搜索的用户输入的任何类型。 若要执行此操作，创建时为包含值的占位符，若要搜索的 SQL 查询。 它将类似此命令：

`SELECT * FROM Movies WHERE Genre = @0`

占位符是`@`字符后跟零。 您可能已经猜到，查询可以包含多个占位符，并将命名为`@0`， `@1`， `@2`，等等。

若要设置的查询和实际上将其传递值，您可以使用如下所示的代码：

[!code-sql[Main](form-basics/samples/sample4.sql)]

此代码是类似于前面已的操作以在网格中显示数据。 唯一的区别是：

- 查询包含一个占位符 (`WHERE Genre = @0"`)。
- 该查询将放入一个变量 (`selectCommand`); 之前，请直接传递查询`db.Query`方法。
- 当您调用`db.Query`方法，则传递查询和要使用的占位符的值。 (如果查询具有多个占位符，会将其传递所有作为单独值的方法。)

如果整理所有这些元素，将得到以下代码：

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **重要提示！** 使用占位符 (如`@0`) 将值传递给 SQL 命令是*极其重要*的安全。 可以看到它，带有占位符变量数据的方法是应构造 SQL 命令的唯一方法。
> 
> 永远不会通过将组合在一起 （连接） 的文字文本和从用户获取的值来构造 SQL 语句。 连接到 SQL 语句中的用户输入将打开到站点*SQL 注入攻击*，恶意用户提交 hack 数据库页的值。 (您可以阅读更多文章中[SQL 注入](https://msdn.microsoft.com/library/ms161953.aspx)MSDN 网站。)


## <a name="updating-the-movies-page-with-search-code"></a>使用搜索代码更新电影页面

现在可以更新中的代码*Movies.cshtml*文件。 若要开始，请将在页面顶部的代码块中的代码替换此代码：

[!code-csharp[Main](form-basics/samples/sample6.cs)]

此处的差别是您已放置到查询`selectCommand`变量，将传递给`db.Query`更高版本。 将放到一个变量中的 SQL 语句，可以更改语句，它将执行哪些操作来执行搜索。

您也删除了以下两行，您将放回中更高版本：

[!code-csharp[Main](form-basics/samples/sample7.cs)]

不想尚未运行查询 (也就是说，调用`db.Query`) 并且不想要初始化`WebGrid`帮助程序，但任何一个。 已经想到的 SQL 语句必须运行后，将执行这些操作。

此重写块后可以添加用于处理搜索新的逻辑。 已完成的代码将如下所示。 使其匹配此示例，请更新您的页面中的代码：

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

页面现在工作方式如下。 每次运行页面时，代码将打开的数据库和`selectCommand`变量设置为获取中的所有记录的 SQL 语句`Movies`表。 此代码还初始化`searchTerm`变量。

但是，如果当前请求中包含的值`searchGenre`元素，该代码设置`selectCommand`到另一个查询，即为包括`Where`子句来搜索的一种流派。 它还将设置`searchTerm`到任何传递的搜索框中 （这可能是执行任何操作）。

而不考虑哪些 SQL 语句位于`selectCommand`，然后，代码调用`db.Query`若要运行查询，并向其传递任何位于`searchTerm`。 如果中没有任何内容`searchTerm`，它并不重要，因为在这种情况下没有参数传递到值`selectCommand`是否仍要。

最后，代码将初始化`WebGrid`帮助器通过使用查询结果中的，像以前一样。

可以看到，通过将置于 SQL 语句和搜索词到变量中，你已向代码添加大的灵活性。 正如您将看到更高版本在本教程中，您可以使用此基本框架，并继续添加用于不同类型的搜索逻辑。

## <a name="testing-the-search-by-genre-feature"></a>测试按流派搜索功能

在 WebMatrix 中，运行*Movies.cshtml*页。 请参阅流派文本框中的页。

输入已输入一个你测试的记录，然后单击一种流派**搜索**。 此时会显示仅匹配该类型的电影的列表：

![列出搜索流派 Comedies 后的电影页](form-basics/_static/image4.png)

输入不同的流派，然后再次进行搜索。 请尝试使用所有小写字母或全部大写的字母，以便您可以看到，搜索不区分大小写输入类型。

## <a name="remembering-what-the-user-entered"></a>"记住"用户输入的内容

您可能已经注意到，之后您输入一种流派，并单击**搜索流派**，看到了该类型的列表。 但是，在搜索文本框中为空&mdash;换而言之，它没有记住以前输入的内容。

请务必了解为什么会发生此行为。 当您提交一个页面时，在浏览器到 web 服务器发送请求。 当 ASP.NET 获取请求时，它创建页面的一个全新的实例，在中，运行代码，然后将重新呈现到浏览器页面。 实际上，不过，页面并不知道，刚刚使用与自身的以前的版本。 所有它知道它有都有一些的请求中它的窗体数据。

每次请求页面&mdash;是第一次，还是通过提交它&mdash;可将一个新页面。 Web 服务器具有的最后一个请求的任何内存。 不能用 ASP.NET 中，也不能用浏览器。 页的这些单独的实例之间的唯一连接是它们之间传输任何数据。 如果提交的页面，例如，新的页实例可以获取由早期实例发送的窗体数据。 （若要在页面之间传递数据的另一种方法是使用 cookie。）

正式地说这种情况下是说，web 页中找到*无状态*。 Web 服务器和页面本身和页面中的元素不维护有关页面的以前的状态的任何信息。 Web 被设计这种方式，因为维护各个请求的状态会快速耗尽资源的 web 服务器，通常可能处理数千个，甚至几十万个情况下，每秒的请求。

因此这就是为什么文本框为空。 提交页面后，ASP.NET 创建的页的新实例，并运行通过代码和标记。 执行任何操作中没有告诉 ASP.NET 将值放到文本框中的代码。 因此 ASP.NET 不执行任何操作，并在文本框中呈现而无需在其中一个值。

没有实际的简单办法解决这个问题。 在文本框中输入的流派*是*在代码中使用&mdash;处于`Request.QueryString["searchGenre"]`。

更新文本框中的标记，以便`value`属性获取其值从`searchTerm`，如下例所示：

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

在此页中，你也可以还设置`value`属性为`searchTerm`输入变量，因为该变量还包含流派。 不过，使用`Request`对象，以设置`value`特性，如此处显示的标准方法来完成此任务。 (即使想要执行此操作假定&mdash;在某些情况下，你可能想要呈现的页面*而无需*中字段的值。 这完全取决于这怎么回事与你的应用。）

> [!NOTE]
> 您不能"记住"用于密码的文本框中的值。 它会让人以填充密码字段中使用代码安全漏洞。


再次运行此页，输入一种流派，然后单击**搜索流派**。 这一次不只执行你看到的搜索结果，但会记住文本框中，输入上一次：

![页面显示，在文本框中具有记住以前的条目](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>搜索标题中的任何字词

你现在可以搜索任何类型，但可能还想要搜索的标题。 很难获取标题完全正确，因此，您可以搜索单词出现在标题内的任意位置搜索时。 若要在 SQL 中执行的操作，应使用`LIKE`运算符和语法如下所示：

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

此命令将获取其标题包含"adventure"的所有电影。 当你使用`LIKE`运算符，包括通配符字符`%`作为搜索词的一部分。 搜索`LIKE 'adventure%'`意味着"开头 'adventure'"。 （从技术上讲，这意味着"字符串 'adventure' 跟任何内容。）同样，搜索词`LIKE '%adventure'`表示"任何内容后面是字符串 'adventure'"，这是另一种方法可以说"与 adventure 结束"。

搜索词`LIKE '%adventure%'`因此意味着"使用"adventure' 标题中的任意位置。" （从技术上讲，"中的任何内容的标题后, 跟 'adventure'，跟任何内容。"）

内部`<form>`元素中，添加以下标记下右`</div>`流派搜索的标记 (只需在关闭前`</form>`元素):

[!code-html[Main](form-basics/samples/sample10.html)]

代码来处理此搜索是类似于流派搜索代码，只不过你必须以组合`LIKE`搜索。 在代码块中的页的顶部，添加以下`if`之后阻止`if`流派搜索的块：

[!code-csharp[Main](form-basics/samples/sample11.cs)]

此代码使用更早版本，看到的相同逻辑，只搜索使用`LIKE`运算符，代码会使"`%`"之前和之后的搜索词。

请注意如何很容易就可以将另一个搜索添加到页。 您所要做的一切是：

- 创建`if`进行测试，查看相关的搜索框中是否具有值的块。
- 设置`selectCommand`变量到新的 SQL 语句。
- 设置`searchTerm`变量指向要传递给查询的值。

下面是完整的代码块，其中包含标题搜索的新逻辑：

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

下面是此代码的作用的摘要：

- 变量`searchTerm`和`selectCommand`顶部初始化。 用户执行的页中根据相应的 SQL 命令和想要将这些变量设置为相应的搜索词 （如果有）。 默认搜索是从数据库中获取所有电影的简单情况。
- 中的测试`searchGenre`并`searchTitle`，该代码设置`searchTerm`你想要搜索的值。 这些代码块还设置`selectCommand`对该搜索的相应 SQL 命令。
- `db.Query`方法使用任何 SQL 命令在只有一次调用`selectedCommand`并且任何值在`searchTerm`。 如果没有搜索词 （没有流派和没有标题 word） 的值`searchTerm`为空字符串。 但是，，并不重要，因为在这种情况下，查询不需要参数。

## <a name="testing-the-title-search-feature"></a>测试标题搜索功能

现在，你可以测试已完成的搜索页。 运行*Movies.cshtml*。

输入一种流派，然后单击**搜索流派**。 网格显示电影的流派，如之前。

输入标题 word，然后单击**搜索标题**。 网格将显示在标题中包含该单词的电影。

![中搜索标题后列出的电影页](form-basics/_static/image6.png)

将两个文本框留空，然后单击任一按钮。 网格显示所有电影。

## <a name="combining-the-queries"></a>合并查询

您可能注意到可以执行的搜索，是互斥的。 您不能一次搜索的标题和流派即使这两个搜索框中都有值。 例如，不能搜索其标题包含"Adventure"的所有操作电影。 （如果流派和标题的输入值，现在，编码页面，如标题搜索获取优先顺序。）若要创建组合条件的搜索，您将必须创建具有如下所示的语法的 SQL 查询：

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

和必须通过使用类似于以下语句来运行查询 （大体而言）：

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

如您所见，创建逻辑，以允许许多排列的搜索条件可以获取有点复杂。 因此，我们将就此打住。

## <a name="coming-up-next"></a>即将推出下一步

在下一步的教程中，你将创建使用窗体以使用户可以向数据库添加电影的页。

## <a name="complete-listing-for-movie-page-updated-with-search"></a>电影页面 （使用搜索更新） 的完整列表

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>其他资源

- [使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkID=202890)
- [SQL WHERE 子句](http://www.w3schools.com/sql/sql_where.asp)W3Schools 站点上
- [方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)W3C 网站上的文章

> [!div class="step-by-step"]
> [上一页](displaying-data.md)
> [下一页](entering-data.md)
