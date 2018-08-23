---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
title: Introducing ASP.NET 网页-编程基础知识 |Microsoft Docs
author: tfitzmac
description: 此教程提供了一些您简要介绍了使用 Razor 语法的 ASP.NET Web Pages 中程序到。 你将了解： 使用拉取请求的基本 Razor 语法...
ms.author: riande
ms.date: 06/17/2015
ms.assetid: 7526ed45-a97d-4e8a-8301-01324ef0eff9
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
msc.type: authoredcontent
ms.openlocfilehash: 120246fab3e71afeef2e2b7c4388f7c294e6b703
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834558"
---
<a name="introducing-aspnet-web-pages---programming-basics"></a>ASP.NET 网页简介-编程基础知识
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 此教程提供了一些您简要介绍了使用 Razor 语法的 ASP.NET Web Pages 中程序到。
> 
> 你将学习：
> 
> - 编程 ASP.NET Web Pages 中使用的基本"Razor"语法。
> - 一些基本 C# 中，这是你将使用的编程语言。
> - 网页的某些基本编程概念。
> - 如何安装包 （包含预生成的代码的组件） 以使用你的网站。
> - 如何使用*帮助程序*以执行常见编程任务。
>   
> 
> 功能/技术讨论：
> 
> - NuGet 和包管理器。
> - `Gravatar`帮助器。


本教程是主要向您介绍的编程语法，将使用为 ASP.NET Web Pages 中练习。 你将了解如何*Razor 语法*和 C# 中编写代码的编程语言。 前面的教程; 中有大致了解此语法在本教程中我们将介绍详细的语法。

我们保证，本教程涉及到您将看到在单个教程中，且它是唯一的教程，是编程最*仅*有关编程。 在此集中的其余教程，你实际上将创建一些有趣的操作的页面。

此外将了解*帮助程序*。 帮助器是一个组件 — 打包向上的一段代码，可添加到页面。 帮助器执行，否则可能是乏味或复杂手动进行的工作。

## <a name="creating-a-page-to-play-with-razor"></a>创建使用 Razor 页面

在本部分中您将扮演有点 Razor 以便您可以了解的基本语法。

启动 WebMatrix，如果它尚不存在正在运行。 你将使用上一教程中创建的网站 ([获取启动与网页](https://go.microsoft.com/fwlink/?LinkId=251578))。 若要重新打开它，请单击**我的网站**，然后选择**WebPageMovies**:

![显示打开站点选项并突出显示了我的网站的 WebMatrix 开始屏幕](intro-to-web-pages-programming/_static/image1.png)

选择**文件**工作区。

在功能区中，单击**新建**来创建一个页面。 选择**CSHTML**并命名新页面*TestRazor.cshtml*。

单击 **“确定”**。

将以下内容复制到文件中，完全替换什么已存在。

> [!NOTE]
> 复制时代码或标记示例中放入页中，缩进和对齐方式不可能与本教程中的相同。 缩进和对齐方式不会影响代码的运行方式，不过。


[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample1.cshtml)]

## <a name="examining-the-example-page"></a>检查示例页

您所看到的大多数都是普通的 HTML。 但是，在顶部没有此代码块：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample2.cshtml)]

请注意，此代码块有关以下操作：

- @ 字符告诉 ASP.NET，后面是 Razor 代码中，不是 HTML。 ASP.NET 将处理后的所有内容 @ 字符作为代码，直至它再次运行到一些 HTML。 (在这种情况下，这&lt;！DOCTYPE&gt;元素。
- 大括号 （{和}） 括起来的 Razor 代码块，如果代码具有多个行。 大括号告知 ASP.NET，该块中的代码开始和结束的位置。
- / / 字符标记注释 — 也就是说，不会执行的代码的一部分。
- 每个语句必须以分号 （;） 结束。 （不注释，但。）
- 可以存储中的值*变量*，创建 (*声明*) 与关键字 var。 在创建变量时，您为其提供一个名称，可以包含字母、 数字和下划线 (\_)。 变量名称不能以数字开头，并且不能使用编程关键字 （如 var) 的名称。
- 将字符字符串 （如"ASP.NET"和"网页"） 括在引号中。 （它们必须是两个双引号）。数字不是在引号中。
- 引号外的空白并不重要。 换行通常不重要;例外情况是，不能将引号中的字符串拆分到行。 缩进和对齐方式不重要。

这并不明显，此示例中是所有代码都是区分大小写。 这意味着变量的参数是一个不同的变量比可能名为参数的变量。 同样，var 关键字，但 Var 不是。

### <a name="objects-and-properties-and-methods"></a>对象和属性和方法

然后是 DateTime.Now 的表达式。 简单来说，是日期时间*对象*。 一个对象是件事情可以与编程 — 页面、 文本框、 文件、 图像、 web 请求、 电子邮件、 客户记录，等等。对象具有一个或多个*属性*，用于描述它们的特征。 文本框对象具有文本属性 （及其他）、 请求对象具有 Url 属性 （和其他人）、 电子邮件具有 From 属性和 To 属性中，依次类推。 对象还具有*方法*是他们可以执行的"谓词"。 您将使用对象大量。

如您所见示例中，日期时间将是可计划日期和时间的对象。 它具有一个名为现在，它返回当前日期和时间属性。

### <a name="using-code-to-render-markup-in-the-page"></a>使用代码来呈现的页中的标记

在页的正文，请注意以下：

[!code-html[Main](intro-to-web-pages-programming/samples/sample3.html)]

同样，@ 字符告诉 ASP.NET，下面的内容是代码，不是 HTML。 在标记中您可以添加代码表达式后, 跟，ASP.NET 将呈现该表达式右侧的值在该点。 在示例中，@a将呈现的值是任何内容的名为的变量，@product呈现任何内容是中的变量的命名产品，依此类推。

您并不仅限于变量，但。 在某些情况下在这里，@ 字符之前表达式：

- @(\*b） 将呈现在变量中的所有内容的产品和 b。 (\*运算符表示乘法。)
- @(技术 +""+ 产品) 将它们连接起来并之间添加空格之后呈现变量技术和产品中的值。 运算符 （+） 用于连接字符串是与运算符相同的数字添加。 ASP.NET，通常可以判断是否使用数字或字符串并采取适当的措施使用 + 运算符。
- @Request.Url 呈现请求对象的 Url 属性。 请求对象包含有关浏览器中，从当前请求的信息，当然 Url 属性包含该当前请求的 URL。

该示例还旨在演示您可以执行不同的方式工作。 可以执行在顶部的代码块中的计算，将结果放到变量中，并随后呈现标记中的变量。 或者，可以执行中的标记中的表达式右侧的计算。 则使用此方法取决于在您执行的操作，以及在某种程度上，在您自己的首选项。

### <a name="seeing-the-code-in-action"></a>查看操作中的代码

右键单击该文件的名称，然后选择**浏览器中启动**。 请参阅中的所有值和表达式在页中已解决了浏览器的页。

![浏览器中运行的 TestRazor 页](intro-to-web-pages-programming/_static/image2.png)

查看浏览器中的源。

![在浏览器中测试 Razor 页面源文件](intro-to-web-pages-programming/_static/image3.png)

正如预期从你在上一教程中的体验的 Razor 代码都不是在页中。 您看到是实际显示的值。 当运行页面时，实际上对内置到 WebMatrix 的 web 服务器进行请求。 收到请求后，ASP.NET 解析所有值和表达式，并将它们的值呈现到页。 然后将页发送到浏览器。

> [!TIP] 
> 
> **Razor 和 C#**
> 
> 到目前为止，我们已经说过您正在使用 Razor 语法。 如此，但并不完整的情景。 正在使用的实际编程语言称为*C#*。 C# Microsoft 创建了前十多年并已成为一种用于创建 Windows 应用程序的主要编程语言。 您已了解有关如何命名变量以及如何创建语句的所有规则都都实际的 C# 语言的所有规则。
> 
> Razor 更具体地说是指获得少数几个有关如何将此代码嵌入到页面的约定。 例如，使用来标记的页中的代码和使用的约定 @ {} 嵌入的代码块是一个页面的 Razor 方面。 帮助程序也被视为是 Razor 的一部分。 在多个位置比只是 ASP.NET Web Pages 中使用 razor 语法。 （例如，它用于 ASP.NET MVC 视图也。）
> 
> 我们提起这个是因为如果您查看有关编程 ASP.NET Web Pages 的信息，您会发现大量对 Razor 的引用。 但是，很多这些引用不会应用于您要这样做并因此可能会令人困惑。 并且，事实上，许多编程问题实际上会采用有关使用 C# 或使用 ASP.NET。 因此如果您看专门为 Razor 有关的信息，您可能找不到所需的答案。


## <a name="adding-some-conditional-logic"></a>添加一些条件逻辑

有关使用代码页中的强大功能之一是，您可以更改时会发生什么情况基于各种条件。 在本教程的此部分中，您将调整相关更改的页中显示的内容的一些方法。

该示例将是简单和精心设计的以便我们可以专注于条件逻辑的某种程度上。 你将创建的页将执行此操作：

- 在页面上显示不同的文本，取决于它是否首次显示的页或是否已单击按钮以提交该页面。 将第一个条件测试。
- 仅当某个值传递的 URL (http://...?show=true) 的查询字符串中显示该消息。 将第二个条件测试。

在 WebMatrix 中，创建一个页面并将其命名*TestRazorPart2.cshtml*。 (在功能区中，单击**新建**，选择**CSHTML**，将文件命名，然后单击**确定**。)

该页的内容替换为以下：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample4.cshtml)]

在顶部的代码块初始化名为一些文本消息的变量。 页的正文，消息变量的内容显示在内&lt;p&gt;元素。 标记还包含&lt;输入&gt;元素来创建**提交**按钮。

运行页后，可以如何立即查看其工作。 现在，它基本上是一个静态页面，即使您单击**提交**按钮。

返回到 WebMatrix。 在代码块中，添加以下突出显示的代码*后*初始化消息的行：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample5.cshtml?highlight=4-6)]

### <a name="the-if---block"></a>If {} 块

刚刚添加了 if 条件。 在代码中，if 条件必须对于此类结构：

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample6.cs)]

要测试的条件是在括号中。 它必须是一个值或返回 true 或 false 的表达式。 如果条件为 true，则 ASP.NET 运行的语句或大括号内的语句。 (这些都是*然后*的一部分*如果-那么*逻辑。)如果条件为 false，则跳过的代码块。

以下是一些示例可以在一个 if 测试的条件语句：

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample7.cs)]

可以使用测试变量值或表达式针对<em>逻辑运算符</em>或<em>比较运算符</em>： 等于 （= =），大于 (&gt;)，小于 (&lt;)，大于或等于 (&gt;=)，并且小于或等于 (&lt;=)。 ！ = 运算符表示不等于-例如，如果 (！ = 0) 意味着<em>如果</em> <em>不等于 0</em>。

> [!NOTE]
> 请确保您注意到等于 （= =） 比较运算符不是与 = 相同。 = 运算符仅用于将值分配 (var = 2)。 如果混合使用这些运算符，也会发生错误，否则将显示一些奇怪的结果。


若要测试的内容是否为 true，完整的语法是 if(IsDone == true)。 但也可以使用快捷方式 if(IsDone)。 如果没有任何比较运算符，ASP.NET 假定您要测试为 true。

！ 运算符本身意味着逻辑非。 例如，条件 if （！IsPost) 意味着*如果 IsPost 条件不*。

您可以通过使用逻辑 AND 组合条件 (&amp; &amp;运算符) 或逻辑 OR (| | 运算符)。 例如，if 的最后一个条件在前面的示例平均值*如果 FileProcessingIsDone 未设置为 true AND displayMessage 设置为 false*。

### <a name="the-else-block"></a>Else 块

一个最后一件事情一下，如果基块： 如果块可以跟到 else 块中。 到 else 块中非常有用，您需要在条件为 false 时执行不同的代码。 下面是一个简单的示例：

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample8.cs)]

更高版本中，使用 else 块也是有用的本系列教程中，将看到一些示例。

### <a name="testing-whether-the-request-is-a-submit-post"></a>测试是否对请求进行提交 （文章）

还有更多，但让我们回到示例中，它具有条件 if(IsPost) {...}。 IsPost 是实际的当前页的属性。 第一次请求页面时，IsPost 返回 false。 但是，如果单击一个按钮或以其他方式提交页面，其发布，即-IsPost，则返回 true。 因此 IsPost 可以确定您是否正在处理的窗体提交。 （根据 HTTP 谓词 GET 操作，该请求是否 IsPost 返回 false。 如果请求的 POST 操作，IsPost 返回 true。）在下一个教程将使用输入窗体，此测试变得特别有用。

运行页。 由于这是首次接到请求页上，你将看到"这是你已请求页面第一次"。 该字符串是初始化到的消息变量的值。 一项 if(IsPost) 测试，但，返回目前，false，所以 if 代码块不会运行。

单击**提交**按钮。 再次请求页面时。 作为之前，消息变量将设置为"是第一次..."。 但这次测试 if(IsPost) 返回 true，所以 if 代码块将运行。 代码更改为不同的值，这是要呈现的标记中的消息变量的值。

现在，添加 if 标记中的条件。 下面&lt;p&gt;元素，其中包含**提交**按钮，添加以下标记：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample9.cshtml)]

要添加标记内的代码，因此必须首先@。 If 则类似于先前添加代码块中的测试。 在大括号，但是，在添加普通 HTML —，至少它很普通，直至到达@DateTime.Now。 这是另一小段 Razor 代码，因此再次需要它的前面添加 @。

这里的一点是，如果在这种情况的代码块顶部和标记中，可以添加。 如果使用 if 条件中的页上，在块内的行正文可以是标记或代码。 在这种情况下，只要您混合使用标记和代码，则为 true，因为您必须使用以使它清楚地 ASP.NET 代码所在。

运行页面，然后单击**提交**。 这一次您不仅能看到不同的消息时，提交 （"现在您提交了..."），但看到列出的日期和时间的新消息。

![与时间戳后显示在浏览器中运行测试 Razor 2 页上提交](intro-to-web-pages-programming/_static/image4.png)

### <a name="testing-the-value-of-a-query-string"></a>测试查询字符串的值

一个测试。 此时，你将添加 if 块以便测试某个值名为可能的查询字符串中传递的显示。 (如下所示： `http://localhost:43097/TestRazorPart2.cshtml?show=true`)，以便该消息，已显示，将更改的页 （"这是首次..."，等等） 如果显示的值为 true，则仅显示。

在底部 （但内部） 的代码块顶部的页上，添加以下代码：

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample10.cs)]

完整的代码块现在看起来像下面的示例。 （请记住，当将代码复制到您的页面后，缩进看起来会有所不同。 但是，不会影响代码的运行方式。）

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample11.cshtml)]

新代码块中的初始化一个变量，名为 showMessage 为 false。 它就会执行 if 测试，以查找的查询字符串中的值。 在第一次请求页面时，它具有如下 URL:

`http://localhost:43097/TestRazorPart2.cshtml`

该代码将确定 URL 是否包含名为查询字符串，如 URL 的此版本中显示的变量：

`http://localhost:43097/TestRazorPart2.cshtml`？ 显示 = true

测试本身来看待请求对象的查询字符串属性。 如果查询字符串包含名为的显示，并且该项设置为 true，if 块运行和 showMessage 变量设置为 true。

还有奥妙在这里，您可以看到。 正如其名称所指，查询字符串是一个字符串。 但是，你可以仅测试 true 和 false 如果您要测试的值为布尔值 (true/false)。 查询字符串中测试显示变量的值之前，必须将其转换为布尔值。 这就是 AsBool 方法作用 — 采用字符串作为输入并将其转换为布尔值。 很明显，如果字符串为"true"，AsBool 方法将该值转换为 true。 如果字符串的值为其他类型，AsBool 返回 false。

> [!TIP] 
> 
> **数据类型和 as （） 方法**
> 
> 我们已只是说到目前为止创建变量时，使用关键字 var。 这不是整篇文章，不过。 为了操作值 — 若要添加数字，或连接字符串，或比较日期，或测试为 true/false-C# 必须使用适当的值的内部表示形式。 C# 可以*通常*找出该表示形式应为 (即，什么*类型*数据) 基于您所做的值。 现在，然后，不过，它无法做到这一点。 如果没有，您必须通过显式，该值指示如何 C# 应表示的数据帮助解决问题。 AsBool 方法执行的 — 它告诉 C# 字符串值"true"或"false"应视为一个布尔值。 存在类似的方法来表示字符串作为其他类型，如 AsInt （视为一个整数）、 AsDateTime （视为日期/时间）、 AsFloat （视为浮点数），等等。 当您使用它们作为 （） 方法，如果 C# 不能表示的字符串值的请求时，您将看到一个错误。


在页面的标记中，删除或注释掉此元素 （此处它显示注释掉）：

[!code-html[Main](intro-to-web-pages-programming/samples/sample12.html)]

你删除或注释掉该文本，添加以下权限：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample13.cshtml)]

如果测试显示为分隔开多个变量为 true，是否呈现的&lt;p&gt;具有消息变量的值的元素。

### <a name="summary-of-your-conditional-logic"></a>条件逻辑的摘要

如果您不完全确定的只是完成的内容，下面是摘要。

- 消息变量初始化为默认字符串 （"这是首次..."）。
- 如果页请求的提交 (post) 结果，消息的值更改为"现在您提交了..."
- 分隔开多个变量初始化为 false。
- 如果查询字符串包含？ 显示 = showMessage 变量设置为 true，则为 true。
- 在标记中，如果为 true，showMessage &lt;p&gt;元素呈现，显示消息的值。 （如果 showMessage 为 false，执行任何操作将呈现在该点的标记中。）
- 在标记中，如果请求是 post &lt;p&gt;元素呈现，显示的日期和时间。

运行页。 没有任何消息，因为 showMessage 为 false，因此在标记中 if(showMessage) 测试返回 false。

单击“提交”。 请参阅日期和时间，但仍没有消息。

在浏览器中，转到 URL 框中，并将以下代码添加到 URL 的末尾:？ 显示为 true，然后按 Enter。

![在浏览器中显示查询字符串 test Razor 2 页](intro-to-web-pages-programming/_static/image5.png)

将再次显示的页。 （因为更改 URL，这是新的请求，不提交。）单击**提交**试。 同样，显示消息原样的日期和时间。

![查询字符串时，将提交后的测试 Razor 2 页](intro-to-web-pages-programming/_static/image6.png)

在 URL 中，更改？ 显示 = true 以？ 显示 = false，然后按 Enter。 重新提交该页面。 该页是返回到你的启动方式 — 任何消息。

如前文所述，此示例中的逻辑是一个小精心设计的。 但是，如果要在很多页面，转，将此处需要一个或多个您所见的窗体。

## <a name="installing-a-helper-displaying-a-gravatar-image"></a>安装帮助程序 （显示 Gravatar 图像）

人们通常希望为在网页上某些任务需要大量的代码，或需要额外知识。 示例： 显示的图的数据;将 Facebook"Like"按钮放置在页;从你的网站; 发送电子邮件裁剪或调整图像; 的大小为您的网站使用 PayPal。 若要能够轻松执行此类目的，ASP.NET Web Pages 使您可以使用*帮助程序*。 帮助器是的组件，为站点安装，以及允许您通过使用几行的 Razor 代码中执行的典型任务。

ASP.NET Web Pages 具有内置的几个帮助程序。 但是，使用 NuGet 包管理器提供的包 （加载项） 中提供了许多帮助程序。 NuGet，可以选择要安装的程序包，然后它就会完成安装的所有详细信息。

在本教程的此部分中，你将安装一个帮助程序，使您可以显示 Gravatar （"全局识别虚拟形象"） 映像。 你将了解以下两种情况。 一个是如何查找和安装帮助程序。 您还将学习如何帮助程序轻松地执行某些您需要使用大量必须自己编写的代码可完成的操作。

您可以注册在 Gravatar 网站在自己 Gravatar [ http://www.gravatar.com/ ](http://www.gravatar.com/)，但并不必要创建 Gravatar 帐户以执行教程的此部分。

在 WebMatrix 中，单击**NuGet**按钮。

![在 WebMatrix 中的 NuGet 库对话框](intro-to-web-pages-programming/_static/image7.png)

这会启动 NuGet 包管理器，并显示可用的包。 (并非所有包都是帮助程序; 一些将功能添加到 WebMatrix 中本身，一些是其他模板，依次类推。)可能会收到有关版本不兼容的错误消息。 可以通过单击忽略此错误消息**确定**和继续执行本教程。

![在 WebMatrix 中的 NuGet 库对话框](intro-to-web-pages-programming/_static/image8.png)

在搜索框中，输入"asp.net 帮助器"。 NuGet 显示与搜索词匹配的程序包。

![在 WebMatrix 中显示包的 NuGet 库](intro-to-web-pages-programming/_static/image9.png)

ASP.NET Web Helpers Library 包含代码，以简化许多常见任务，包括使用 Gravatar 图像。 选择**ASP.NET Web Helpers Library**包，然后单击**安装**以启动安装程序。 选择**是**当系统询问你是否想要安装包，并接受条款以完成安装。

介绍完毕。 NuGet 会下载并安装所有内容，包括可能需要的任何其他组件 (*依赖项*)。

如果出于某种原因您必须卸载程序的帮助程序，过程也是非常相似。 单击**NuGet**按钮，再单击**已安装**选项卡，然后选择你想要卸载的程序包。

## <a name="using-a-helper-in-a-page"></a>在页面中使用一个帮助程序

现在，您将使用刚安装的帮助器。 向页面添加一个帮助程序的过程是类似的大多数帮助程序。

在 WebMatrix 中，创建一个页面并将其命名*GravatarTest.cshml*。 （要创建一个特殊网页来测试帮助器，但可以在你的站点中的任意页面中使用帮助器。）

内部&lt;正文&gt;元素中，添加&lt;div&gt;元素。 内部&lt;div&gt;元素中，键入：

@Gravatar。

@ 字符是你已使用标记 Razor 代码中的相同字符。 **Gravatar**是您正在使用的帮助程序对象。

只要键入句点 （.），WebMatrix 将显示一系列*方法*Gravatar 帮助程序提供 （函数）：

![Gravatar 帮助程序 IntelliSense 下拉列表](intro-to-web-pages-programming/_static/image10.png)

此功能被称为*IntelliSense*。 它通过提供上下文相应选项来帮助你的代码。 IntelliSense 适用于 HTML、 CSS、 ASP.NET 代码、 JavaScript 和在 WebMatrix 中支持其他语言。 它是另一项功能，简化了开发在 WebMatrix 中的网页。

按 G 上于键盘，并且您看到 IntelliSense 查找 GetHtml 方法。 按 Tab 键。IntelliSense 为您插入所选的方法 (GetHtml)。 键入左括号，并请注意，会自动添加右括号。 在引号内的两个括号之间键入您的电子邮件地址。 如果你有 Gravatar 帐户，将返回个人资料图片。 如果没有 Gravatar 帐户，则返回默认图像。 完成后，在行如下所示：

[!code-css[Main](intro-to-web-pages-programming/samples/sample14.css)]

现在在浏览器中查看的页面。 您的图片或默认图像将显示，具体取决于是否具有 Gravatar 帐户。

![Gravatar](intro-to-web-pages-programming/_static/image11.png) ![默认映像](intro-to-web-pages-programming/_static/image12.png)

若要了解的内容的帮助程序为你做，在浏览器中查看页面的源代码。 随 HTML，您的页面中，您将看到将标识符包含一个 image 元素。 这是帮助器呈现到页中有位置的位置的代码@Gravatar.GetHtml。 帮助者花费了提供和生成的代码与直接 Gravatar 以便获取正确的映像提供帐户的信息。

GetHtml 方法还可以通过提供其他参数自定义映像。 下面的代码演示如何请求映像具有宽度和高度为 40 像素，并使用名为指定的默认映像**wavatar**如果指定的帐户不存在。

[!code-javascript[Main](intro-to-web-pages-programming/samples/sample15.js)]

此代码生成类似于以下的结果 （将随机有所不同的默认映像） 的内容。

![](intro-to-web-pages-programming/_static/image13.png)

## <a name="coming-up-next"></a>即将推出下一步

若要使此教程短，我们可以专注于仅的一些基本知识。 当然，这里有*很多*Razor 和 C# 的信息。 你将了解详细信息作为您经历这些教程。 如果有兴趣学习有关 Razor 和 C# 的编程方面的详细信息稍后再试，则可以读取的更全面的介绍： [ASP.NET Web 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkID=202890)。

下一教程将介绍使用数据库。 在该教程中，将开始创建允许你列出你最喜爱的电影的示例应用程序。

## <a name="complete-listing-for-testrazor-page"></a>TestRazor 页的完整列表

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample16.cshtml)]

## <a name="complete-listing-for-testrazorpart2-page"></a>TestRazorPart2 页的完整列表

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample17.cshtml)]

## <a name="complete-listing-for-gravatartest-page"></a>GravatarTest 页的完整列表

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample18.cshtml)]

## <a name="additional-resources"></a>其他资源

- [使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkID=202890)
- [Twitter 帮助程序](../../ui-layouts-and-themes/twitter-helper.md)

> [!div class="step-by-step"]
> [上一页](getting-started.md)
> [下一页](displaying-data.md)
