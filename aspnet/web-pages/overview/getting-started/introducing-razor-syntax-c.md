---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: 使用 Razor 语法 (C#) 的 ASP.NET Web 编程简介 |Microsoft Docs
author: tfitzmac
description: 本章提供了您的编程概述与 ASP.NET Web Pages 使用 Razor 语法。 ASP.NET 是 Microsoft 的技术，用于运行动态 web pa...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: 347e5ddbc02866887d3f422ecc291e5e3dfacaaf
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832672"
---
<a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a>使用 Razor 语法 (C#) 的 ASP.NET Web 编程简介
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文提供了您的编程概述与 ASP.NET Web Pages 使用 Razor 语法。 ASP.NET 是 Microsoft 的技术，用于在 web 服务器上运行动态网页。 此文章重点介绍使用 C# 编程语言。
> 
> **你将了解**:
> 
> - 前 8 的编程的入门知识编程使用 Razor 语法的 ASP.NET Web Pages 的提示。
> - 你将需要的基本编程概念。
> - ASP.NET 服务器代码和 Razor 语法是所有有关。
>   
> 
> ## <a name="software-versions"></a>软件版本
> 
> 
> - ASP.NET 网页 (Razor) 3
>   
> 
> 本教程还适用于 ASP.NET Web Pages 2。


## <a name="the-top-8-programming-tips"></a>最重要的 8 编程提示

本部分列出了绝对需要知道当你开始使用 Razor 语法的 ASP.NET 服务器代码编写的一些提示。

> [!NOTE]
> Razor 语法基于 C# 编程语言，这也最常使用使用 ASP.NET Web Pages 的语言。 但是，Razor 语法还支持 Visual Basic 语言以及你看到你还可以执行在 Visual Basic 中的所有内容。 有关详细信息，请参阅附录[Visual Basic 语言和语法](https://go.microsoft.com/fwlink/?LinkId=202908)。


在本文的后面，可以找到有关这些编程技术的大多数的更多详细信息。

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1.将代码添加到页使用 @ 字符

`@`字符开始内联表达式、 单个语句块和多语句块：

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

这是这些语句在浏览器中运行页面时的如下：

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> **HTML 编码**
> 
> 在页面中使用显示内容时`@`字符 ASP.NET HTML 编码输出，如前面的示例中所示。 它取代了 HTML 的保留的字符 (如`<`并`>`和`&`) 启用字符作为字符而不是解释为 HTML 标记或实体的网页中显示的代码。 无需 HTML 编码，即可在服务器代码中的输出可能不会显示正确，并可能会暴露于安全风险的页面。
> 
> 如果你的目标是输出以标记形式呈现标记的 HTML 标记 (例如`<p></p>`段落或`<em></em>`来强调文本)，请参阅部分[组合文本、 标记和代码块中的代码](#BM_CombiningTextMarkupAndCode)这篇文章中更高版本。
> 
> 你可以阅读更多有关中的 HTML 编码[使用窗体](https://go.microsoft.com/fwlink/?LinkId=202892)。


### <a name="2-you-enclose-code-blocks-in-braces"></a>2.将代码块括在大括号中

一个*代码块*包括一个或多个代码语句并括在大括号。

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

在浏览器中显示的结果：

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a>3.在块中，您最终以分号结束每条代码语句

在代码块中，每个完整的代码语句必须以分号结尾。 内联表达式不以分号结束。

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a>4.使用变量来存储值

可以存储中的值*变量*，包括字符串、 数字和日期等。创建一个新的变量使用`var`关键字。 可以直接在页中使用插入变量值`@`。

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

在浏览器中显示的结果：

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5.将文本字符串值括在双引号内

一个*字符串*是被视为文本字符序列。 若要指定一个字符串，则将其括在双引号内：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

如果你想要显示的字符串包含反斜杠字符 ( `\` ) 或双引号 ( `"` )，使用*原义字符串文本*前面带`@`运算符。 (在 C# 中，\ 字符具有特殊含义，除非使用原义字符串文本。)

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

若要嵌入双引号引起来，使用逐字字符串文本，并重复引号引起来：

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

下面是在一个页面中使用这两个示例的结果：

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> 请注意，`@`标记在 C# 中的逐字字符串文本和标记 ASP.NET 页面中的代码使用字符。


### <a name="6-code-is-case-sensitive"></a>6.代码是区分大小写

在 C# 中，关键字 (如`var`， `true`，和`if`) 和变量名称区分大小写。 以下代码行创建两个不同的变量，`lastName`和 `LastName.`

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

如果声明一个变量，作为`var lastName = "Smith";`，如果试图引用该变量在页中作为`@LastName`，会发生错误，因为`LastName`将无法识别。

> [!NOTE]
> 在 Visual Basic 关键字和变量是*不*区分大小写。


### <a name="7-much-of-your-coding-involves-objects"></a>7.大部分代码涉及到对象

*对象*表示的接口可以带有程序&#8212;页、 文本框、 文件、 图像、 web 请求、 电子邮件、 客户记录 （数据库行），等等。对象具有描述它们的特征的属性，并且你可以读取或更改&#8212;文本框对象具有`Text`（及其他） 的属性，请求对象具有`Url`属性，电子邮件具有`From`属性，和客户对象都具有`FirstName`属性。 对象还具有方法&quot;谓词&quot;他们可以执行。 示例包括文件对象的`Save`方法中，映像对象的`Rotate`方法，并电子邮件对象的`Send`方法。

你经常要用`Request`对象，后者可提供信息，如值的文本框 （窗体字段） 在页面上，进行浏览器的哪种类型的请求的 URL 的页面、 用户标识，等等。下面的示例演示如何访问的属性`Request`对象以及如何调用`MapPath`方法的`Request`对象，这将使您在服务器上的页面的绝对路径：

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

在浏览器中显示的结果：

![Razor Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8.可以编写代码来做出决策

动态网页的一项主要功能是，您可以确定要执行的操作根据条件。 若要执行此操作的最常见方法是使用`if`语句 (和可选`else`语句)。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

该语句`if(IsPost)`是一种编写的速记方法`if(IsPost == true)`。 连同`if`语句，有多种方法可以测试条件，重复的代码块，并且依此类推，这是本文后面所述。

在浏览器中显示的结果 (单击后**提交**):

![Razor Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a>HTTP GET 和 POST 方法和 IsPost 属性
> 
> 用于网页 (HTTP) 的协议支持的方法 （谓词） 用来向服务器发出请求的数量很少。 两个最常见的是 GET、 用于读取某页和用于将网页提交的文章。 一般情况下，用户请求页面时，第一次请求页面时使用 GET。 如果用户在填写窗体，并单击提交按钮，浏览器向服务器发出的 POST 请求。
> 
> 在 web 编程中，它通常是有助于了解是否请求页面时正在作为 GET 或 POST，以便您知道如何处理页面。 ASP.NET Web Pages 中，可以使用`IsPost`属性以确定请求是否为 GET 或 POST。 如果请求为 POST，`IsPost`属性将返回 true，然后你可以执行诸如读取窗体上的文本框的值。 你将看到许多示例演示如何处理以不同的方式具体取决于值页面`IsPost`。


## <a name="a-simple-code-example"></a>简单的代码示例

此过程演示如何创建一个页面，说明了基本的编程技术。 在示例中，您可以创建允许用户输入两个数字，然后将它们添加并显示结果的页面。

1. 在编辑器中，创建一个新文件并将其命名*AddNumbers.cshtml*。
2. 将以下代码和标记复制到页中，替换已在页中的任何内容。  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    下面是您需要注意一些事项：

    - `@`字符在页中，启动第一个代码块，它位于之前`totalMessage`嵌入在页面底部附近的变量。
    - 在页面顶部块括在大括号中。
    - 在顶部块中，所有行以分号都结束。
    - 变量`total`， `num1`， `num2`，和`totalMessage`存储多个数字和字符串。
    - 分配给的文字字符串值`totalMessage`变量是在双引号。
    - 因为代码是区分大小写，当`totalMessage`变量使用页面底部附近，其名称必须完全匹配在顶部的变量。
    - 表达式`num1.AsInt() + num2.AsInt()`演示如何使用对象和方法。 `AsInt`上每个变量的方法将转换输入用户的数字 （整数），以便可以对其执行算术运算的字符串。
    - `<form>`标记包含`method="post"`属性。 此步骤指定当用户单击**添加**，页面将发送到服务器使用 HTTP POST 方法。 提交页面后，`if(IsPost)`测试的计算结果为 true，条件性代码运行时，显示数字相加的结果。
3. 保存页面，并在浏览器中运行它。 (请确保的页中选择**文件**工作区之前运行它。)输入两个整数，然后单击**添加**按钮。 

    ![Razor Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a>基本编程概念

本文为您提供了 ASP.NET web 编程的概述。 它并不详尽检查，只需快速介绍一下将最常使用的编程概念。 即便如此，它涵盖了你将需要开始使用 ASP.NET Web Pages 几乎所有内容。

但首先，一点的技术背景知识。

### <a name="the-razor-syntax-server-code-and-aspnet"></a>Razor 语法、 服务器代码和 ASP.NET

Razor 语法是一种简单的编程语法，用于在网页中嵌入基于服务器的代码。 在使用 Razor 语法的网页，有两种类型的内容： 客户端内容和服务器代码。 客户端内容是你习惯于在 web pages 中的内容： HTML 标记 （元素） 的样式信息，如 CSS，也许某些客户端脚本，如 JavaScript 和纯文本。

Razor 语法，可以将服务器代码添加到此客户端内容。 是否存在服务器代码页中，服务器运行该代码首先，它将页发送到浏览器之前。 通过在服务器上运行，代码可以执行任务，可以是更复杂，无法使用独立的如访问基于服务器的数据库的客户端内容执行操作。 最重要的是，服务器代码可以动态创建客户端内容&#8212;它可以生成 HTML 标记或其他动态内容并将其发送给浏览器以及页可能会包含任何静态 HTML。 从浏览器的角度来看，客户端在服务器代码生成的内容是与任何其他客户端内容没有什么不同。 如您所见，所需的服务器代码是非常简单。

包含 Razor 语法的 ASP.NET 网页具有特殊的文件扩展名 (*.cshtml*或 *.vbhtml*)。 服务器可以识别这些扩展，运行的代码，使用 Razor 语法标记，然后将页发送到浏览器。

### <a name="where-does-aspnet-fit-in"></a>ASP.NET 的适用？

Razor 语法基于名为 ASP.NET，又基于 Microsoft.NET Framework 的 microsoft 技术。 .Net Framework 是一个大的全面编程框架从 Microsoft 开发几乎任何类型的计算机应用程序。 ASP.NET 是专门设计用于创建 web 应用程序的.NET Framework 的一部分。 开发人员使用 ASP.NET 创建的最大和最高流量网站的许多世界中。 (只要您看到的文件扩展名 *.aspx*作为一个站点中的 URL 的一部分，您就会知道该站点使用 ASP.NET 进行编写。)

Razor 语法提供 ASP.NET，但使用的简化的语法来更轻松地了解你是否方面的专家，如果您是初学者，可将您提高工作效率的所有强大的功能。 尽管此语法易于使用，它与 ASP.NET 和.NET Framework 的系列关系意味着随着你的网站变得更复杂的还有可供你的更大框架的功能。

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> **类和实例**
> 
> ASP.NET 服务器代码使用对象，又基于类的概念。 此类是定义或模板的对象。 例如，应用程序可能包含`Customer`类，该类定义的属性和任何客户对象所需的方法。
> 
> 当应用程序需要使用实际的客户信息时，它创建的实例 (或*实例化*) 客户对象。 每个单独的客户是一个单独的实例`Customer`类。 每个实例支持的相同的属性和方法，但每个实例的属性值通常不同，因为每个客户对象都是唯一。 一个客户对象中`LastName`属性可能是"Smith"; 在另一个客户对象，`LastName`属性可能会"Jones"。
> 
> 同样，在站点中任何单个 web 页是`Page`对象，它的实例`Page`类。 页面上的按钮是`Button`对象，它的实例`Button`类中，依次类推。 每个实例都有其自己的特征，但它们都基于对象的类定义中指定的内容。


## <a name="basic-syntax"></a>基本语法

前面您了解了如何创建 ASP.NET Web Pages 页，以及如何可以将服务器代码添加到 HTML 标记的一个基本示例。 本文介绍使用 Razor 语法的 ASP.NET 服务器代码的基础知识&#8212;，它是编程语言规则。

如果你是经验丰富的编程 （尤其是如果你使用过 C、 c + +、 C#、 Visual Basic 或 JavaScript），您现在阅读的许多并不陌生。 您可能需要仅与如何将服务器代码添加到标记中了解了相关 *.cshtml*文件。

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a>组合文本、 标记和代码块中的代码

在服务器代码块内，通常要输出的文本或标记 （或两者） 到页面。 如果服务器代码块包含的文本的不是代码和，而是应呈现是，ASP.NET 将需要能够将该文本与代码区分开来。 有若干方法可实现此操作。

- 将文本括在类似的 HTML 元素`<p></p>`或`<em></em>`:   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    HTML 元素可以包括文本、 其他 HTML 元素和服务器代码表达式。 当 ASP.NET 发现 HTML 开始标记 (例如， `<p>`)，它将呈现所有内容包括元素和作为其内容是浏览器中，按照其设想解决服务器代码表达式。
- 使用`@:`运算符或`<text>`元素。 `@:`输出一行内容包含纯文本或 HTML 标记不匹配;`<text>`元素包含多行输出。 不想要作为输出的一部分呈现的 HTML 元素时，这些选项非常有用。  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    如果你想要输出多行文本或 HTML 标记不匹配，则可以在前面与每个行`@:`，或可以放置在行外侧`<text>`元素。 像`@:`运算符，`<text>`标记 ASP.NET 用于识别文本的内容和页面输出中永远不会呈现。

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    第一个示例重复前面的示例，但会使用一对`<text>`标记括起要呈现的文本。 在第二个示例中，`<text>`并`</text>`标记将三个行，都有一些非包含的文本和不匹配的 HTML 标记括起来 (`<br />`)，以及服务器代码和匹配的 HTML 标记。 同样，还可以位于单独使用每个行`@:`运算符; 任一种方法的工作原理。

    > [!NOTE]
    > 当输出文本，如本部分中所示&#8212;使用 HTML 元素，`@:`运算符，或`<text>`元素&#8212;ASP.NET 不会进行 HTML 编码输出。 (如前文所述，ASP.NET does 对服务器的代码表达式的前面使用的服务器代码块的输出进行编码`@`，本节中所述的特殊情况除外。)

### <a name="whitespace"></a>Whitespace

在语句中 （和字符串文字之外） 额外空间不会影响该语句：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

在语句中的一个分行符语句上的无效，且可换行以提高可读性的语句。 以下语句是相同的：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

但是，您将无法打包中间字符串文本行。 下面的示例不起作用：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

若要组合的长字符串，如上面的代码中的多个行包装，有两个选项。 可以使用串联运算符 (`+`)，您将会看到这篇文章中更高版本。 此外可以使用`@`创建原义字符串文本，如本文前面所看到的字符。 可以位于同一行中的原义字符串文本：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a>代码 （和标记） 的注释

注释使您可以保留为自己或他人的说明。 它们还允许您禁用 (*注释掉*) 代码或标记，您不想运行，但想要暂时在页中保留的部分。

没有其他注释语法 Razor 代码以及 HTML 标记。 与所有 Razor 代码一样，Razor 注释处理 （，然后删除） 页发送到浏览器之前在服务器上。 因此，Razor 注释语法允许您将编辑该文件，但用户看不到，即使在页源时，可以看到的注释的代码 （或甚至到标记）。

ASP.NET Razor 注释的开始与注释`@*`日期和结束其与`*@`。 注释可以为一行或多个行上：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

下面是一个代码块中的注释：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

下面的代码行使用同一个块的代码，注释掉，以便它不会运行：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

在代码块中，作为一种方式使用 Razor 注释语法，您可以使用注释使用的，如 C# 的编程语言的语法：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

在 C# 中的单行注释的前面有`//`字符和多行注释开头`/*`开头和结尾`*/`。 （使用 Razor 注释，如 C# 注释不会呈现到浏览器。）

标记中，您可能知道，可以创建 HTML 注释：

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

HTML 注释开头`<!--`字符和结尾`-->`。 您可以使用 HTML 注释来包围不仅文本，而且还可能想要保留的页中，但不想呈现任何 HTML 标记。 此 HTML 注释将隐藏标记和它们所包含的文本的整个内容：

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

与 Razor 注释，HTML 注释不同*是*呈现给页和用户可以通过查看页面源文件来查看它们。

Razor 在嵌套的块中的 C# 上存在限制。 有关详细信息请参阅[名为 C# 变量和嵌套的块生成中断代码](http://aspnetwebstack.codeplex.com/workitem/1914)

## <a name="variables"></a>变量

变量是命名的对象，用于存储数据。 您可以命名变量任何内容，但该名称必须以字母字符开头，不能包含空格或保留的字符。

### <a name="variables-and-data-types"></a>变量和数据类型

变量可以具有特定的数据类型，指示在变量中存储的数据的种类。 你可以存储字符串值的字符串变量 (如&quot;Hello world&quot;)，存储 （如 3 或 79） 的整数值的整数变量和存储中以不同的格式 （如 2012 年 4 月 12 日或 2009 年 3 月的日期值的日期变量). 还有许多可以使用其他数据类型。

但是，你通常无需指定类型的变量。 大多数情况下，ASP.NET 可找出基于变量中的数据的使用方式的类型。 （有时必须指定一个类型; 您将看到示例这为 true。）

声明变量使用`var`关键字 （如果不想指定类型） 或使用的类型名称：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

下面的示例演示在网页中的变量的一些典型用法：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

如果合并前面的示例页中，你会看到此浏览器中显示：

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>转换和测试数据类型

尽管 ASP.NET 通常可以自动确定数据类型，但有时不能进行。 因此，您可能需要通过执行显式转换来帮助解决问题的 ASP.NET。 即使您没有将类型转换，有时很有帮助进行测试以查看哪些类型的数据，可能正在处理。

最常见的情况是，您必须将字符串转换为另一种类型，如向整数或日期。 下面的示例演示一个典型的例子，必须将字符串转换为数字。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

通常，用户输入到你以字符串形式提供。 即使系统已提示用户输入一个数字，并且即使在提交用户输入以及代码中读取时所输入的一个数字，数据的格式字符串。 因此，必须将字符串转换为数字。 在示例中，如果你尝试值执行算术运算，而不转换它们，出现以下错误结果，因为 ASP.NET 不能添加两个字符串：

*不能隐式转换为 int 的 string 类型。*

若要将值转换为整数，则调用`AsInt`方法。 如果转换成功，您可以将数字。

下表列出了一些常见的转换和测试方法的变量。

:::row:::
    :::column:::
        <strong>方法</strong>
    :::column-end:::
    :::column:::
        <strong>说明</strong>
    :::column-end:::
    :::column:::
        <strong>示例</strong>
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        将转换为整数表示 （如"593") 的整数的字符串。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        将转换字符串，如&quot;，则返回 true&quot;或&quot;false&quot;为 Boolean 类型。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        将具有类似的十进制值的字符串转换&quot;1.3&quot;或&quot;7.439&quot;为浮点数。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        将具有类似的十进制值的字符串转换&quot;1.3&quot;或&quot;7.439&quot;为十进制数。 （在 ASP.NET 中，十进制数字是一个浮点数，更详细地说明。） :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        将对 ASP.NET 表示的日期和时间值的字符串转换`DateTime`类型。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        将任何其他数据类型转换为字符串。
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>运算符

运算符是命令的关键字或告诉 ASP.NET 什么样来执行在表达式中的字符。 C# 语言 （及对其基于 Razor 语法） 支持很多运算符，但只需识别几个开始。 下表总结了最常见的运算符。


:::row:::
    :::column:::
        <strong>Operator</strong>
    :::column-end:::
    :::column:::
        <strong>说明</strong>
    :::column-end:::
    :::column:::
        <strong>示例</strong>
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `+` `-` `*` `/`
    :::column-end:::
    :::column:::
        在数值表达式中使用的数学运算符。
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        赋值。 将一条语句右侧的值分配给左侧和右侧的对象。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
        相等。 返回`true`值是否相等。 (请注意之间的区别`=`运算符和`==`运算符。) :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
        不相等。 返回`true`如果值不相等。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        更少的相比，更高的比，小于-或者-等于，以及大于或等于。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
        串联用于联接的字符串。 ASP.NET 就会知道此运算符和加法运算符的表达式的数据类型之间的差异。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `+=` `-=`
    :::column-end:::
    :::column:::
        递增和递减运算符，从而添加，并且从变量 （分别） 减 1。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        圆点。 用于区分对象及其属性和方法。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        括号。 使用组表达式，并将参数传递给方法。
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
        方括号。 用于访问数组或集合中的值。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
        不。 反转`true`值设为`false`，反之亦然。 通常用作测试的速记方法`false`(即，对于不`true`)。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `&&` <code>&#124;&#124;</code>
    :::column-end:::
    :::column:::
        逻辑 AND 和 OR，用于链接在一起条件。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a>使用文件和代码中的文件夹路径

将在代码中经常处理的文件和文件夹的路径。 下面是用于网站的物理文件夹结构的示例，它可能会显示在开发计算机上：

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

下面是一些有关 Url 和路径的重要详细信息：

- 开始使用的域名的 URL (`http://www.example.com`) 或服务器名称 (`http://localhost`， `http://mycomputer`)。
- URL 对应于主机计算机上的物理路径。 例如，`http://myserver`可能对应于文件夹*C:\websites\mywebsite*在服务器上。
- 虚拟路径是简写形式来表示在代码中的路径，而无需指定完整路径。 它包括遵守域或服务器名称的 URL 的一部分。 当你使用的虚拟路径时，可以而无需更新的路径，你的代码移动到不同的域或服务器。

下面是一个示例，帮助您了解的差异：

| 完整的 URL | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| 服务器名称 | *mycompanyserver* |
| 虚拟路径 | */humanresources/CompanyPolicy.htm* |
| 物理路径 | *C:\mywebsites\humanresources\CompanyPolicy.htm* |

虚拟根目录为 /，就像在 c： 驱动器是 \。 （虚拟文件夹路径始终使用正斜杠。）文件夹的虚拟路径不需要作为物理文件夹; 具有相同的名称它可以是一个别名。 （在生产服务器上的虚拟路径很少与匹配确切的物理路径。）

代码中的文件和文件夹时，有时您需要引用的物理路径，有时也是虚拟路径，具体取决于您正在使用哪些对象。 ASP.NET 提供了这些工具用于在代码中的文件和文件夹路径：`Server.MapPath`方法，并`~`运算符和`Href`方法。

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a>转换虚拟与物理路径： Server.MapPath 方法

`Server.MapPath`方法将为虚拟路径 (如 */default.cshtml*) 为绝对物理路径 (如*C:\WebSites\MyWebSiteFolder\default.cshtml*)。 每当您需要完整的物理路径使用此方法。 典型示例是要读取或写入文本文件或 web 服务器上的图像文件时。

通常不知道你的站点托管站点服务器上的绝对物理路径，因此此方法可以将路径转换您知道的虚拟路径 — 到您的服务器上的相应路径。 将虚拟路径传递给文件或文件夹的方法，并返回的物理路径：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>引用虚拟根： ~ 运算符和 Href 方法

在中 *.cshtml*或 *.vbhtml*文件中，您可以引用虚拟根路径使用`~`运算符。 这是非常方便，因为您可以来回移动网页，在站点中，并且它们包含到其他页面的任何链接不会被破坏。 如果曾经将你的网站移动到另一个位置还有非常方便。 下面是一些可能的恶意活动：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

如果网站`http://myserver/myapp`，下面是如何 ASP.NET 会将这些路径运行页面时：

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

（您实际上不会看到这些路径作为该变量的值，但像这就是它们的是，ASP.NET 会将路径）。

可以使用`~`运算符 （如上所述） 的服务器代码中和在标记中，像这样：

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

在标记中，您使用`~`运算符来创建资源，如图像文件、 其他网页和 CSS 文件的路径。 页运行时，ASP.NET 页面 （代码和标记） 中查找并解决所有`~`引用到适当的路径。

## <a name="conditional-logic-and-loops"></a>条件逻辑和循环

ASP.NET 服务器代码可以执行基于条件的任务，并编写特定次数的重复语句的代码 （即，运行一个循环的代码）。

### <a name="testing-conditions"></a>测试条件

若要测试使用一个简单条件`if`语句，返回 true 或 false 基于你指定的测试：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

`if`关键字开始块。 实际的测试 （条件） 位于括号中，并返回 true 或 false。 运行测试为 true 的语句括在大括号中。 `if`语句中可以包含`else`指定如果条件为 false，则运行语句块：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

您可以添加多个条件使用`else if`块：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

在此示例中，如果第一个条件中 if 块不为 true，`else if`条件进行检查。 如果满足该条件，则在语句`else if`块执行。 如果没有条件为真中的语句`else`块执行。 可以添加任意数量的 else if 的阻止，并使用然后关闭`else`作为阻止&quot;其他所有内容&quot;条件。

若要测试大量的条件，请使用`switch`块：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

要测试的值位于括号中 (在示例中，`weekday`变量)。 每个单独测试使用`case`语句以冒号 （:） 结尾。 如果的值`case`语句进行匹配的测试值时，该事例块中的代码执行。 关闭与每个 case 语句`break`语句。 (如果你忘记了在每个包括中断`case`阻止，请从下一个代码`case`语句还将运行。)一个`switch`块通常具有`default`语句的最后一种情况作为&quot;其他所有内容&quot;如果不满足的其他情况下运行的选项。

在浏览器中显示的最后两个条件块的结果：

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a>循环的代码

通常需要反复运行相同的语句。 通过循环执行此操作。 例如，您通常运行同一个语句为每个项集合中的数据。 如果你确切地知道多少次循环，则可以使用`for`循环。 此种类型的循环非常适合计算或向下计数：

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

循环开头`for`关键字后, 跟三个语句在括号内，每个以分号结尾。

- 在括号内的第一个语句 (`var i=10;`) 创建一个计数器并将初始化为 10。 无需命名计数器`i`&#8212;可以使用任何变量。 当`for`循环运行时，会自动增加计数器的数值。
- 第二个语句 (`i < 21;`) 设置距离您要计数的条件。 在这种情况下，想要转到最多 20 个 （即，继续时该计数器是小于 21）。
- 第三个语句 (`i++` ) 使用递增运算符，只需指定计数器应具有 1 添加到其每次循环运行的时。

大括号内是循环的每次迭代就会运行的代码。 标记将创建一个新段落 (`<p>`元素) 每个时间，并将行添加到输出，显示的值`i`（计数器）。 在运行此页时，该示例将创建显示每个行，该值指示项编号中的文本的输出的 11 行。

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

如果您正在使用集合或数组，通常使用`foreach`循环。 集合是一组类似对象和`foreach`循环可让你执行在集合中每一项任务。 此类型的循环非常方便的集合，因为与不同`for`循环中，您无需使计数器递增或设置的限制。 相反，`foreach`循环代码只需继续遍历该集合直到完成。

例如，以下代码将返回中的项`Request.ServerVariables`集合，这是一个对象，包含有关你的 web 服务器的信息。 它使用`foreac`h 循环，以显示每个项的名称，通过创建一个新`<li>`HTML 项目符号列表中的元素。

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

`foreach`关键字后跟括号，声明表示集合中的单个项的变量 (在示例中， `var item`) 后, 跟`in`关键字后, 跟想要循环访问的集合。 正文中`foreach`循环中，您可以访问使用你之前声明的变量的当前项。

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

若要创建一个更通用的循环，请使用`while`语句：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

一个`while`循环开头`while`关键字后, 跟括号指定循环继续的时间长度 (这里，为只要`countNum`小于 50)，然后要重复的块。 循环通常递增 （将添加到） 或递减 （从减） 的变量或用于计数的对象。 在示例中，`+=`运算符将添加到 1`countNum`每次循环运行的时。 (若要递减的向下计数的循环中的变量，将使用递减运算符`-=`)。

## <a name="objects-and-collections"></a>对象和集合

在 ASP.NET 网站中几乎所有内容是一个对象，包括在 web 页面。 本部分介绍一些重要的对象，您将使用频繁地在代码中。

### <a name="page-objects"></a>页对象

在 ASP.NET 中的最基本对象是页。 可以访问的不符合要求的任何对象而直接的 page 对象的属性。 以下代码获取页的文件路径，使用`Request`页的对象：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

若要使其明确的引用的当前的页对象上属性和方法，你可以选择使用关键字`this`来表示在代码中的页对象。 下面是前面的代码示例中，使用`this`添加来表示页面：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

可以使用的属性`Page`对象以获得大量的信息，例如：

- `Request`。 如您所见，这是信息的一系列有关当前请求，包括哪种类型的浏览器发出了请求、 页面、 用户标识，等等的 URL。
- `Response`。 这是信息的有关在服务器代码完成运行时将发送到浏览器的响应 （页） 集合。 例如，此属性可用于将信息写入到响应。 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a>集合对象 （数组和字典）

一个*集合*是一组相同的类型，如集合的对象的`Customer`数据库中的对象。 ASP.NET 包含多个内置集合，例如`Request.Files`集合。

通常将使用集合中的数据。 两个常见集合类型是*数组*并*字典*。 如果你想要存储类似项的集合，但不想创建一个单独的变量来保存每个项，数组非常有用：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

对于数组，声明特定数据类型，如`string`， `int`，或`DateTime`。 若要指示该变量可以包含的数组，向声明添加方括号 (如`string[]`或`int[]`)。 您可以访问项在数组中使用它们的位置 （索引） 或通过使用`foreach`语句。 从零开始的数组索引为&#8212;，它是第一项是在位置 0，第二项是在位置 1，依此类推。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

可以通过获取确定数组中的项的数目及其`Length`属性。 若要获取特定项的数组 （若要搜索数组） 中的位置，请使用`Array.IndexOf`方法。 此外可以执行诸如反向数组的内容 (`Array.Reverse`方法) 或对内容进行排序 (`Array.Sort`方法)。

在浏览器中显示的字符串数组代码的输出：

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

字典是键/值对的集合，其中提供密钥 （或名称） 设置或检索相应的值：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

若要创建一个字典，请使用`new`关键字来指示您要创建新的字典对象。 可以将字典分配给变量使用`var`关键字。 指示使用尖括号字典中的项的数据类型 ( `< >` )。 在声明的末尾，必须添加一对圆括号，因为这是实际创建一个新的字典的方法。

若要将项添加到字典中，可以调用`Add`字典变量或方法 (`myScores`这种情况下)，然后指定一个键和值。 或者，可以使用方括号以指示该密钥，并执行简单的赋值，如以下示例所示：

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

若要从字典中获取一个值，请在方括号中指定密钥：

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a>调用带参数的方法

在阅读本文前面部分中，带有程序的对象可以具有方法。 例如，`Database`对象可能具有`Database.Connect`方法。 许多方法还具有一个或多个参数。 一个*参数*是向方法传递一个值以使该方法以完成其任务。 例如，查看有关声明`Request.MapPath`方法，它使用三个参数：

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

（已换行以使其更具可读性。 请记住，可以将分行符几乎任何位置除了内部字符串用引号括起来。)

此方法相对应的服务器上的物理路径返回到指定的虚拟路径。 该方法的三个参数是`virtualPath`， `baseVirtualDir`，和`allowCrossAppMapping`。 （请注意，在声明中，所列的参数将接受的数据的数据类型）。当调用此方法时，必须提供所有三个参数的值。

Razor 语法可以用于将参数传递给方法的两个选项：*位置参数*并*命名参数*。 若要调用使用位置参数的方法，请按严格顺序方法声明中指定的传递参数。 （您通常知道此顺序通过阅读文档的方法。）必须遵循的顺序，并且你不能跳过的任何参数&#8212;如果有必要，请传递了空字符串 (`""`) 或`null`不具有的值为位置参数。

下面的示例假定你有一个名为的文件夹*脚本*上你的网站。 该代码调用`Request.MapPath`方法，并传递正确的顺序中的三个参数的值。 然后，它显示生成映射的路径。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

当某个方法具有多个参数时，您可以保留你的代码更具可读性使用命名参数。 若要调用的方法使用命名的参数，您指定的参数名称后跟一个冒号 （:），然后选择值。 命名参数的优点是，可以将它们传递所需的任何顺序。 （一个缺点是方法调用不是精简。）

下面的示例调用按上面所述的相同方法，但使用命名参数提供的值：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

正如您所看到的会以不同的顺序传递参数。 但是，如果在运行上面的例子和此示例中，它们将返回相同的值。

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a>处理错误

### <a name="try-catch-statements"></a>Try Catch 语句

通常必须在代码中可能会失败的原因有您的控制范围内的语句。 例如：

- 如果你的代码尝试创建或访问的文件时，可能会出现各种类型的错误。 所需的文件可能不存在，则可能锁定，代码可能不具有的权限，等等。
- 同样，如果你的代码尝试更新数据库中的记录，可能出现权限问题、 与数据库的连接可能会断开，要保存的数据可能无效，依此类推。

在编程术语中，这些应用场景被称为*异常*。 如果你的代码遇到的异常，它将生成 （的引发操作） 的错误消息的在最令人讨厌的用户：

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

在其中您的代码可能会发生异常的情况下，为了避免这种类型的错误消息，可以使用`try/catch`语句。 在`try`语句中，您运行要检查的代码。 一个或多个`catch`语句，则可以寻找特定于可能发生的错误 （特定类型的异常）。 可以包括任意多个`catch`语句作为您需要查找你预期会发生的错误。

> [!NOTE]
> 我们建议您不要使用`Response.Redirect`中的方法`try/catch`语句，因为它可以在页面中导致异常。


下面的示例显示了创建第一个请求上的文本文件，然后显示一个按钮，使用户可以打开文件的页面。 该示例故意使用错误的文件名称，以便它将导致异常。 该代码包括`catch`两个可能的异常的语句： `FileNotFoundException`，就会出现此错误，文件名称是否和`DirectoryNotFoundException`，如果 ASP.NET 甚至找不到该文件夹将出现此情况。 （您可以取消注释该示例中的语句才能看到它时一切运行正常的运行。）

如果你的代码未处理异常，会看到一个错误页面，如前面的屏幕截图。 但是，`try/catch`部分可帮助防止用户看到这些类型的错误。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a>其他资源

**使用 Visual Basic 进行编程**


[附录： Visual Basic 语言和语法](https://go.microsoft.com/fwlink/?LinkId=202908)


**参考文档**


[ASP.NET 2.0](https://msdn.microsoft.com/library/ee532866.aspx)

[C# 语言](https://msdn.microsoft.com/library/kx37x362.aspx)
