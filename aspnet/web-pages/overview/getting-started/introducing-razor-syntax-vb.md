---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: 使用 Razor 语法 (Visual Basic 中) 的 ASP.NET Web 编程简介 |Microsoft Docs
author: tfitzmac
description: 本附录提供使用 ASP.NET Web pages 编程概述在 Visual Basic 中使用 Razor 语法。
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: cbec035533c37723afcd5bf4aa0c6e1c83dbae23
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831065"
---
<a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a>使用 Razor 语法 (Visual Basic 中) 的 ASP.NET Web 编程简介
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文提供了您的编程概述与 ASP.NET Web Pages 使用 Razor 语法和 Visual Basic。 ASP.NET 是 Microsoft 的技术，用于在 web 服务器上运行动态网页。
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


使用 ASP.NET Web Pages with Razor syntax 的大多数示例使用 C#。 但 Razor 语法还支持 Visual Basic。 进行编程 ASP.NET 网页在 Visual Basic 中，创建与网页 *.vbhtml*文件扩展名，以及如何将 Visual Basic 代码。 本文提供使用 Visual Basic 语言和用于创建 ASP.NET 网页语法的概述。

> [!NOTE]
> Microsoft WebMatrix 的默认网站模板 (**面包店**，**照片库**，并**入门网站**等) 在 C# 和 Visual Basic 版本中可用。 可以安装 Visual Basic 的模板作为 NuGet 包。 名为的文件夹中的站点的根文件夹中安装网站模板*Microsoft 模板*。


## <a name="the-top-8-programming-tips"></a>最重要的 8 编程提示

本部分列出了绝对需要知道当你开始使用 Razor 语法的 ASP.NET 服务器代码编写的一些提示。

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1.将代码添加到页使用 @ 字符

`@`字符开始内联表达式、 单语句块和多语句块：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

在浏览器中显示的结果：

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> **HTML 编码**
> 
> 在页面中使用显示内容时`@`字符 ASP.NET HTML 编码输出，如前面的示例中所示。 它取代了 HTML 的保留的字符 (如`<`并`>`和`&`) 启用字符作为字符而不是解释为 HTML 标记或实体的网页中显示的代码。 无需 HTML 编码，即可在服务器代码中的输出可能不会显示正确，并可能会暴露于安全风险的页面。
> 
> 如果你的目标是输出以标记形式呈现标记的 HTML 标记 (例如`<p></p>`段落或`<em></em>`来强调文本)，请参阅部分[组合文本、 标记和代码块中的代码](#BM_CombiningTextMarkupAndCode)这篇文章中更高版本。
> 
> 你可以阅读更多有关中的 HTML 编码[使用 ASP.NET Web Pages 站点中的 HTML 窗体](https://go.microsoft.com/fwlink/?LinkId=202892)。


### <a name="2-you-enclose-code-blocks-with-codeend-code"></a>2.将代码的代码块...结束代码

代码块包含一个或多个代码语句，并且通过关键字括`Code`和`End Code`。 将左括号`Code`关键字后立即`@`字符&#8212;它们之间不能有空格。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

在浏览器中显示的结果：

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a>3.在块中，您最终每个代码语句提供一个分行符

在 Visual Basic 代码块中，每个语句以换行符结尾。 （本文稍后将看到根据需要换行到多个行的冗长的代码语句的方法。）

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a>4.使用变量来存储值

可以存储中的值*变量*，包括字符串、 数字和日期等。创建一个新的变量使用`Dim`关键字。 可以直接在页中使用插入变量值`@`。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

在浏览器中显示的结果：

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5.将文本字符串值括在双引号内

一个*字符串*是被视为文本字符序列。 若要指定一个字符串，则将其括在双引号内：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

若要嵌入双引号引起来的字符串值中，插入两个双引号字符。 如果你想要出现一次页面输出中的双引号字符，作为其输入`""`中带引号的字符串，并将其作为输入在您希望其出现两次，如果`""""`中带引号的字符串。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

在浏览器中显示的结果：

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a>6.Visual Basic 代码不区分大小写

Visual Basic 语言不区分大小写。 编程关键字 (如`Dim`， `If`，并`True`) 和变量名称 (如`myString`，或`subTotal`) 可以在任何情况下编写。

以下代码行向变量分配值`lastname`使用小写名称，然后再将变量值输出到页面使用的是大写的名称。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

在浏览器中显示的结果：

![vb 语法 5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a>7.大部分代码涉及到使用对象

对象表示的接口可以与编程&#8212;页、 文本框、 文件、 图像、 web 请求、 电子邮件、 客户记录 （数据库行），等等。对象具有描述其特征的属性&#8212;文本框对象具有`Text`属性，请求对象具有`Url`属性，电子邮件具有`From`属性，且客户对象都具有`FirstName`属性。 对象还具有方法&quot;谓词&quot;他们可以执行。 示例包括文件对象的`Save`方法中，映像对象的`Rotate`方法，并电子邮件对象的`Send`方法。

你经常要用`Request`对象，它为您提供了信息，如值的窗体字段 （文本框等），在页上进行浏览器的哪种类型的请求的 URL 的页面、 用户标识，等等。此示例演示如何访问的属性`Request`对象以及如何调用`MapPath`方法的`Request`对象，这将使您在服务器上的页面的绝对路径：

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

在浏览器中显示的结果：

![Razor Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8.可以编写代码来做出决策

动态网页的一项主要功能是，您可以确定要执行的操作根据条件。 若要执行此操作的最常见方法是使用`If`语句 (和可选`Else`语句)。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

该语句`If IsPost`是一种编写的速记方法`If IsPost = True`。 连同`If`语句，有多种方法可以测试条件，重复的代码块，并且依此类推，这是本文后面所述。

在浏览器中显示的结果 (单击后**提交**):

![Razor Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> **HTTP GET 和 POST 方法和 IsPost 属性**
> 
> 用于网页 (HTTP) 的协议支持的方法非常有限的数量 (&quot;谓词&quot;)，用于向服务器发出请求。 两个最常见的是 GET、 用于读取某页和用于将网页提交的文章。 一般情况下，用户请求页面时，第一次请求页面时使用 GET。 如果用户在填写窗体，并单击**提交**，浏览器向服务器发出的 POST 请求。
> 
> 在 web 编程中，它通常是有助于了解是否请求页面时正在作为 GET 或 POST，以便您知道如何处理页面。 ASP.NET Web Pages 中，可以使用`IsPost`属性以确定请求是否为 GET 或 POST。 如果请求为 POST，`IsPost`属性将返回 true，然后你可以执行诸如读取窗体上的文本框的值。 你将看到许多示例演示如何处理以不同的方式具体取决于值页面`IsPost`。


## <a name="a-simple-code-example"></a>简单的代码示例

此过程演示如何创建一个页面，说明了基本的编程技术。 在示例中，您可以创建允许用户输入两个数字，然后将它们添加并显示结果的页面。

1. 在编辑器中，创建一个新文件并将其命名*AddNumbers.vbhtml*。
2. 将以下代码和标记复制到页中，替换已在页中的任何内容。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    下面是您需要注意一些事项：

    - `@`字符在页中，启动第一个代码块，它位于之前`totalMessage`变量嵌入靠近底部。
    - 在页面顶部块括在`Code...End Code`。
    - 变量`total`， `num1`， `num2`，和`totalMessage`存储多个数字和字符串。
    - 分配给的文字字符串值`totalMessage`变量是在双引号。
    - 因为 Visual Basic 代码时不区分大小写`totalMessage`变量使用页面底部附近，其名称只需要匹配在页面顶部的变量声明的拼写是否正确。 大小写并不重要。
    - 表达式`num1.AsInt()`  +  `num2.AsInt()`演示如何使用对象和方法。 `AsInt`上每个变量的方法将转换到整数 （整数），可以添加由用户输入的字符串。
    - `<form>`标记包含`method="post"`属性。 此步骤指定当用户单击**添加**，页面将发送到服务器使用 HTTP POST 方法。 提交页面时，代码`If IsPost`计算结果为 true，条件性代码运行时，显示数字相加的结果。
3. 保存页面，并在浏览器中运行它。 (请确保的页中选择**文件**工作区之前运行它。)输入两个整数，然后单击**添加**按钮。

    ![Razor Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a>Visual Basic 语言和语法

前面您了解了如何创建 ASP.NET web 页面中，以及如何可以将服务器代码添加到 HTML 标记的基本示例。 本文介绍使用 Visual Basic 来编写使用 Razor 语法的 ASP.NET 服务器代码的基础知识&#8212;，它是编程语言规则。

如果你是经验丰富的编程 （尤其是如果你使用过 C、 c + +、 C#、 Visual Basic 或 JavaScript），您现在阅读的许多并不陌生。 您可能需要仅与如何 WebMatrix 代码添加到标记中了解了相关 *.vbhtml*文件。

### <a id="BM_CombiningTextMarkupAndCode"></a>  组合文本、 标记和代码块中的代码

在服务器代码块中，您通常需要输出文本和到页面的标记。 如果服务器代码块包含的文本的不是代码和，而是应呈现是，ASP.NET 将需要能够将该文本与代码区分开来。 有若干方法可实现此操作。

- 将文本括在类似的 HTML 块元素`<p></p>`或`<em></em>`:

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    HTML 元素可以包括文本、 其他 HTML 元素和服务器代码表达式。 当 ASP.NET 发现 HTML 开始标记 (例如， `<p>`)，它会呈现所有内容的元素，并且作为其内容的浏览器 （和解析服务器代码表达式）。

- 使用`@:`运算符或`<text>`元素。 `@:`输出一行内容包含纯文本或 HTML 标记不匹配;`<text>`元素包含多行输出。 不想要作为输出的一部分呈现的 HTML 元素时，这些选项非常有用。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    下面的示例重复前面的示例，但使用一对`<text>`标记括起要呈现的文本。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    在以下示例中，`<text>`并`</text>`标记将三个行，都有一些非包含的文本和不匹配的 HTML 标记括起来 (`<br />`)，以及服务器代码和匹配的 HTML 标记。 同样，还可以位于单独使用每个行`@:`运算符; 任一种方法的工作原理。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > 当输出文本，如本部分中所示&#8212;使用 HTML 元素，`@:`运算符，或`<text>`元素&#8212;ASP.NET 不会进行 HTML 编码输出。 (如前文所述，ASP.NET does 对服务器的代码表达式的前面使用的服务器代码块的输出进行编码`@`，本节中所述的特殊情况除外。)

### <a name="whitespace"></a>Whitespace

在语句中 （和字符串文字之外） 额外空间不会影响该语句：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a>将长语句分成多个行

您可以使用下划线字符长代码语句拆分为多个行`_`(在 Visual Basic 中的这种行为称为*继续符*) 之后的每一行代码。 若要中断语句到下一行上的，在行尾添加一个空格，然后继续符。 在下一行上继续该语句。 可以包装到尽可能多的行以提高可读性所需的语句。 以下语句是相同的：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

但是，您将无法打包中间字符串文本行。 下面的示例不起作用：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

若要组合的长字符串，如上面的代码中的多个行包装，您需要使用*串联运算符*(`&`)，您将会看到这篇文章中更高版本。

### <a name="code-comments"></a>代码注释

注释使您可以保留为自己或他人的说明。 Razor 语法的注释都带有前缀`@*`开头和结尾`*@`。

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

在代码块中，您可以使用 Razor 语法注释，也可以使用普通的 Visual Basic 注释字符，这是一个单引号 (`'`) 作为每个行的前缀。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a>变量

变量是命名的对象，用于存储数据。 您可以命名变量任何内容，但该名称必须以字母字符开头，不能包含空格或保留的字符。 在 Visual Basic 中，正如您看到的更早版本，并不重要的变量名称中的字母大小写。

### <a name="variables-and-data-types"></a>变量和数据类型

变量可以具有特定的数据类型，指示在变量中存储的数据的种类。 你可以存储字符串值的字符串变量 (如&quot;Hello world&quot;)，存储 （如 3 或 79） 的整数值的整数变量和存储中以不同的格式 （如 2012 年 4 月 12 日或 2009 年 3 月的日期值的日期变量). 还有许多可以使用其他数据类型。

但是，您无需指定类型的变量。 在大多数情况下 ASP.NET 可找出基于变量中的数据的使用方式的类型。 （有时必须指定一个类型; 您将看到示例这为 true。）

若要声明变量时不指定类型的情况下，使用`Dim`加变量名称 (例如， `Dim myVar`)。 若要声明变量的类型时，使用`Dim`加变量名称后, 跟`As`，然后是类型名称 (例如， `Dim myVar As String`)。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

下面的示例演示在网页中使用变量的某些内联表达式。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

在浏览器中显示的结果：

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>转换和测试数据类型

尽管 ASP.NET 通常可以自动确定数据类型，但有时不能进行。 因此，您可能需要通过执行显式转换来帮助解决问题的 ASP.NET。 即使您没有将类型转换，有时很有帮助进行测试以查看哪些类型的数据，可能正在处理。

最常见的情况是，您必须将字符串转换为另一种类型，如向整数或日期。 下面的示例演示一个典型的例子，必须将字符串转换为数字。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

通常，用户输入到你以字符串形式提供。 即使系统已提示用户输入一个数字，并且即使在提交用户输入以及代码中读取时所输入的一个数字，数据的格式字符串。 因此，必须将字符串转换为数字。 在示例中，如果你尝试值执行算术运算，而不转换它们，出现以下错误结果，因为 ASP.NET 不能添加两个字符串：

`Cannot implicitly convert type 'string' to 'int'.`

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
        将表示为整数的字符串转换 (如&quot;593&quot;) 为整数。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::


## <a name="operators"></a>运算符

运算符是命令的关键字或告诉 ASP.NET 什么样来执行在表达式中的字符。 Visual Basic 支持许多运算符，但只需识别了一些以开始开发 ASP.NET 网页。 下表总结了最常见的运算符。


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
        `+ - * /`
    :::column-end:::
    :::column:::
        在数值表达式中使用的数学运算符。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        赋值和相等。 根据上下文，将一条语句右侧的值分配给左侧和右侧，对象或检查值相等。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        不相等。 返回`True`如果值不相等。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        小于、 大于、 小于或等于，以及大于或等于。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        串联用于联接的字符串。
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        递增和递减运算符，从而添加，并且从变量 （分别） 减 1。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        括号。 为组表达式，用于将参数传递给方法，并访问数组和集合的成员。
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        不。 反转 true 值为 false，反之亦然。 通常用作测试的速记方法`False`(即，对于不`True`)。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        逻辑 AND 和 OR，用于链接在一起条件。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

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

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>引用虚拟根： ~ 运算符和 Href 方法

在中 *.cshtml*或 *.vbhtml*文件中，您可以引用虚拟根路径使用`~`运算符。 这是非常方便，因为您可以来回移动网页，在站点中，并且它们包含到其他页面的任何链接不会被破坏。 如果曾经将你的网站移动到另一个位置还有非常方便。 下面是一些可能的恶意活动：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

如果网站`http://myserver/myapp`，下面是如何 ASP.NET 会将这些路径运行页面时：

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

（您实际上不会看到这些路径作为该变量的值，但像这就是它们的是，ASP.NET 会将路径）。

可以使用`~`运算符 （如上所述） 的服务器代码中和在标记中，像这样：

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

在标记中，您使用`~`运算符来创建资源，如图像文件、 其他网页和 CSS 文件的路径。 页运行时，ASP.NET 页面 （代码和标记） 中查找并解决所有`~`引用到适当的路径。

## <a name="conditional-logic-and-loops"></a>条件逻辑和循环

ASP.NET 服务器代码可以执行任务根据条件和编写代码重复特定次数，即代码的语句运行一个循环）。

### <a name="testing-conditions"></a>测试条件

若要测试使用一个简单条件`If...Then`语句，它将返回`True`或`False`基于你指定的测试：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

`If`关键字开始块。 实际的测试 （条件） 遵循`If`关键字并返回 true 或 false。 `If`语句结尾`Then`。 将运行测试为 true 的语句被括`If`和`End If`。 `If`语句中可以包含`Else`指定如果条件为 false，则运行语句块：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

如果`If`语句将启动一个代码块，无需使用普通`Code...End Code`语句以包括的块。 可以仅添加`@`到块，并且它将起作用。 此方法适用于`If`以及其他 Visual Basic 编程关键字跟代码块，其中包括`For`， `For Each`， `Do While`，等等。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

您可以添加多个条件使用一个或多个`ElseIf`基块：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

在此示例中，如果第一个条件中`If`块不为 true，`ElseIf`条件进行检查。 如果满足该条件，则在语句`ElseIf`块执行。 如果没有条件为真中的语句`Else`块执行。 可以添加任意数量的`ElseIf`阻止，并使用然后关闭`Else`作为阻止&quot;其他所有内容&quot;条件。

若要测试大量的条件，请使用`Select Case`块：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

要测试的值是在括号内 （在示例中，在工作日变量）。 每个单独测试使用`Case`列出了值的语句。 如果的值`Case`语句与测试值中的代码匹配`Case`执行块。

在浏览器中显示的最后两个条件块的结果：

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a>循环的代码

通常需要反复运行相同的语句。 通过循环执行此操作。 例如，您通常运行同一个语句为每个项集合中的数据。 如果你确切地知道多少次循环，则可以使用`For`循环。 此种类型的循环非常适合计算或向下计数：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

循环开头`For`关键字后, 跟三个元素：

- 后立即`For`语句中，您将计数器变量声明 (无需使用`Dim`)，然后指明范围，如`i = 10 to 20`。 这意味着变量`i`将从开始计数 10 并继续，直到它达到 20 （含）。
- 之间`For`和`Next`语句是在块的内容。 这可以包含一个或多个代码执行的语句每次循环。
- `Next i`语句结束循环。 其递增的计数器，并启动循环的下一个迭代。

之间的代码行`For`和`Next`行包含每个迭代的循环运行的代码。 标记将创建一个新段落 (`<p>`元素) 每个时间，并将行添加到输出，显示的值 i （计数器）。 在运行此页时，该示例将创建显示每个行，该值指示项编号中的文本的输出的 11 行。

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

如果您正在使用集合或数组，通常使用`For Each`循环。 集合是一组类似对象和`For Each`循环可让你执行在集合中每一项任务。 此类型的循环非常方便的集合，因为与不同`For`循环中，您无需使计数器递增或设置的限制。 相反，`For Each`循环代码只需继续遍历该集合直到完成。

此示例将返回中的项`Request.ServerVariables`集合 （其中包含有关你的 web 服务器的信息）。 它使用`For Each`循环，以显示每个项的名称，通过创建一个新`<li>`HTML 项目符号列表中的元素。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

`For Each`关键字后跟表示集合中的单个项的变量 (在示例中， `myItem`) 后, 跟`In`关键字后, 跟想要循环访问的集合。 正文中`For Each`循环中，您可以访问使用你之前声明的变量的当前项。

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

若要创建一个更通用的循环，请使用`Do While`语句：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

此循环开头`Do While`关键字后, 跟的条件后, 跟要重复的块。 循环通常递增 （将添加到） 或递减 （从减） 的变量或用于计数的对象。 在示例中，`+=`运算符将添加 1 到变量的值每次循环运行的时。 (若要递减的向下计数的循环中的变量，将使用递减运算符`-=`。)

## <a name="objects-and-collections"></a>对象和集合

在 ASP.NET 网站中几乎所有内容是一个对象，包括在 web 页面。 本部分介绍一些重要的对象，您将使用频繁地在代码中。

### <a name="page-objects"></a>页对象

在 ASP.NET 中的最基本对象是页。 可以访问的不符合要求的任何对象而直接的 page 对象的属性。 以下代码获取页的文件路径，使用`Request`页的对象：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

可以使用的属性`Page`对象以获得大量的信息，例如：

- `Request`。 如您所见，这是信息的一系列有关当前请求，包括哪种类型的浏览器发出了请求、 页面、 用户标识，等等的 URL。
- `Response`。 这是信息的有关在服务器代码完成运行时将发送到浏览器的响应 （页） 集合。 例如，此属性可用于将信息写入到响应。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a>集合对象 （数组和字典）

集合是一组相同的类型，如集合对象`Customer`数据库中的对象。 ASP.NET 包含多个内置集合，例如`Request.Files`集合。

通常将使用集合中的数据。 两个常见集合类型是*数组*并*字典*。 如果你想要存储类似项的集合，但不想创建一个单独的变量来保存每个项，数组非常有用：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

对于数组，声明特定数据类型，如`String`， `Integer`，或`DateTime`。 若要指示该变量可以包含的数组，将括号添加到声明中的变量名称 (如`Dim myVar() As String`)。 您可以访问项在数组中使用它们的位置 （索引） 或通过使用`For Each`语句。 从零开始的数组索引为&#8212;，它是第一项是在位置 0，第二项是在位置 1，依此类推。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

可以通过获取确定数组中的项的数目及其`Length`属性。 若要获取特定项的数组中的位置 (即，搜索数组)，使用`Array.IndexOf`方法。 此外可以执行诸如反向数组的内容 (`Array.Reverse`方法) 或对内容进行排序 (`Array.Sort`方法)。

在浏览器中显示的字符串数组代码的输出：

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

字典是键/值对的集合，其中提供密钥 （或名称） 设置或检索相应的值：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

若要创建一个字典，请使用`New`关键字来指示要创建一个新`Dictionary`对象。 可以将字典分配给变量使用`Dim`关键字。 指示使用括号的字典中的项的数据类型 ( `( )` )。 在声明的末尾，必须添加另一对括号，因为这是实际创建一个新的字典的方法。

若要将项添加到字典中，可以调用`Add`字典变量或方法 (`myScores`这种情况下)，然后指定一个键和值。 或者，可以使用括号以指示该密钥，并执行简单的赋值，如以下示例所示：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

若要从字典中获取一个值，请在括号中指定密钥：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a>调用带参数的方法

正如您看到本文前面部分，带有程序的对象具有方法。 例如，`Database`对象可能具有`Database.Connect`方法。 许多方法还具有一个或多个参数。 一个*参数*是向方法传递一个值以使该方法以完成其任务。 例如，查看有关声明`Request.MapPath`方法，它使用三个参数：

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

此方法相对应的服务器上的物理路径返回到指定的虚拟路径。 该方法的三个参数是`virtualPath`， `baseVirtualDir`，和`allowCrossAppMapping`。 （请注意，在声明中，所列的参数将接受的数据的数据类型）。当调用此方法时，必须提供所有三个参数的值。

当你使用 Visual Basic 使用 Razor 语法时，具有用于将参数传递给方法的两个选项：*位置参数*或*命名参数*。 若要调用使用位置参数的方法，请按严格顺序方法声明中指定的传递参数。 （您通常知道此顺序通过阅读文档的方法。）必须遵循的顺序，并且你不能跳过的任何参数&#8212;如果有必要，请传递了空字符串 (`""`) 或不具有的值的位置参数为 null。

下面的示例假定你有一个名为的文件夹*脚本*上你的网站。 该代码调用`Request.MapPath`方法，并传递正确的顺序中的三个参数的值。 然后，它显示生成映射的路径。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

当有多个参数的方法时，您可以保留你的代码更简洁且更具可读性使用命名参数。 若要调用的方法使用命名的参数，指定参数名称后跟`:=`，然后提供值。 命名参数的一个优点是，可以将其添加所需的任何顺序。 （一个缺点是方法调用不是精简。）

下面的示例调用按上面所述的相同方法，但使用命名参数提供的值：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

正如您所看到的会以不同的顺序传递参数。 但是，如果在运行上面的例子和此示例中，它们将返回相同的值。

## <a name="handling-errors"></a>处理错误

### <a name="try-catch-statements"></a>Try Catch 语句

通常必须在代码中可能会失败的原因有您的控制范围内的语句。 例如：

- 如果你的代码尝试打开、 创建、 读取或写入文件时，可能会出现各种类型的错误。 所需的文件可能不存在，则可能锁定，代码可能不具有的权限，等等。
- 同样，如果你的代码尝试更新数据库中的记录，可能出现权限问题、 与数据库的连接可能会断开，要保存的数据可能无效，依此类推。

在编程术语中，这些应用场景被称为*异常*。 如果你的代码遇到的异常，它将生成 （的引发操作） 错误消息，而该充其量，令人讨厌的用户。

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

在其中您的代码可能会发生异常的情况下，为了避免这种类型的错误消息，可以使用`Try/Catch`语句。 在`Try`语句中，您运行要检查的代码。 一个或多个`Catch`语句，则可以寻找特定于可能发生的错误 （特定类型的异常）。 可以包括任意多个`Catch`语句作为您需要查找的预期的错误。

> [!NOTE]
> 我们建议您不要使用`Response.Redirect`中的方法`Try/Catch`语句，因为它可以在页面中导致异常。


下面的示例显示了创建第一个请求上的文本文件，然后显示一个按钮，使用户可以打开文件的页面。 该示例故意使用错误的文件名称，以便它将导致异常。 该代码包括`Catch`两个可能的异常的语句： `FileNotFoundException`，就会出现此错误，文件名称是否和`DirectoryNotFoundException`，如果 ASP.NET 甚至找不到该文件夹将出现此情况。 （您可以取消注释该示例中的语句才能看到它时一切运行正常的运行。）

如果你的代码未处理异常，会看到一个错误页面，如前面的屏幕截图。 但是，`Try/Catch`部分可帮助防止用户看到这些类型的错误。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a>其他资源

### <a name="reference-documentation"></a>参考文档

- [ASP.NET 2.0](https://msdn.microsoft.com/library/ee532866.aspx)
- [Visual Basic 语言](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
