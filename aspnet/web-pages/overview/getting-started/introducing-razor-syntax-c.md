---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: 使用 Razor 语法 (C#) 的 ASP.NET Web 编程简介 |Microsoft 文档
author: tfitzmac
description: 本章概述你的编程与 ASP.NET Web Pages 使用 Razor 语法。 ASP.NET 是 Microsoft 的技术，用于运行动态 web pa...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/07/2014
ms.topic: article
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: 48f49f40a6fc0c6a0c664873879f9f61080132ea
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
<a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a><span data-ttu-id="016e3-104">使用 Razor 语法 (C#) 的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="016e3-104">Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)</span></span>
====================
<span data-ttu-id="016e3-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="016e3-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="016e3-106">本文概述你的编程与 ASP.NET Web Pages 使用 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="016e3-106">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax.</span></span> <span data-ttu-id="016e3-107">ASP.NET 是用于在 web 服务器上运行动态 web 页的 Microsoft 的技术。</span><span class="sxs-lookup"><span data-stu-id="016e3-107">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span> <span data-ttu-id="016e3-108">此文章重点使用 C# 编程语言。</span><span class="sxs-lookup"><span data-stu-id="016e3-108">This articles focuses on using the C# programming language.</span></span>
> 
> <span data-ttu-id="016e3-109">**你将了解**:</span><span class="sxs-lookup"><span data-stu-id="016e3-109">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="016e3-110">编程提示的入门知识编程使用 Razor 语法的 ASP.NET Web Pages 顶部 8。</span><span class="sxs-lookup"><span data-stu-id="016e3-110">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="016e3-111">你将需要的基本编程概念。</span><span class="sxs-lookup"><span data-stu-id="016e3-111">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="016e3-112">哪些 ASP.NET 服务器代码和 Razor 语法与所有有关。</span><span class="sxs-lookup"><span data-stu-id="016e3-112">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="016e3-113">软件版本</span><span class="sxs-lookup"><span data-stu-id="016e3-113">Software versions</span></span>
> 
> 
> - <span data-ttu-id="016e3-114">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="016e3-114">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="016e3-115">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="016e3-115">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="the-top-8-programming-tips"></a><span data-ttu-id="016e3-116">最重要的 8 编程提示</span><span class="sxs-lookup"><span data-stu-id="016e3-116">The Top 8 Programming Tips</span></span>

<span data-ttu-id="016e3-117">本部分列出绝对需要知道当你开始编写使用 Razor 语法的 ASP.NET 服务器代码的一些提示。</span><span class="sxs-lookup"><span data-stu-id="016e3-117">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="016e3-118">Razor 语法基于 C# 编程语言中，这也最常使用的 ASP.NET Web Pages 使用的语言。</span><span class="sxs-lookup"><span data-stu-id="016e3-118">The Razor syntax is based on the C# programming language, and that's the language that's used most often with ASP.NET Web Pages.</span></span> <span data-ttu-id="016e3-119">但是，Razor 语法还支持 Visual Basic 语言中，以及你看到你还可以执行在 Visual Basic 中的所有内容。</span><span class="sxs-lookup"><span data-stu-id="016e3-119">However, the Razor syntax also supports the Visual Basic language, and everything you see you can also do in Visual Basic.</span></span> <span data-ttu-id="016e3-120">有关详细信息，请参阅附录[Visual Basic 语言和语法](https://go.microsoft.com/fwlink/?LinkId=202908)。</span><span class="sxs-lookup"><span data-stu-id="016e3-120">For details, see the appendix [Visual Basic Language and Syntax](https://go.microsoft.com/fwlink/?LinkId=202908).</span></span>


<span data-ttu-id="016e3-121">在本文的后面，你可以找到有关这些编程技术的大多数的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="016e3-121">You can find more details about most of these programming techniques later in the article.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="016e3-122">1.将代码添加到页使用 @ 字符</span><span class="sxs-lookup"><span data-stu-id="016e3-122">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="016e3-123">`@`字符开始内联表达式、 单个语句块和多语句块：</span><span class="sxs-lookup"><span data-stu-id="016e3-123">The `@` character starts inline expressions, single statement blocks, and multi-statement blocks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

<span data-ttu-id="016e3-124">这是这些语句在页的浏览器中运行时的外观：</span><span class="sxs-lookup"><span data-stu-id="016e3-124">This is what these statements look like when the page runs in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="016e3-126">**HTML 编码**</span><span class="sxs-lookup"><span data-stu-id="016e3-126">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="016e3-127">当你在页中使用显示内容`@`字符，如前面的示例中，ASP.NET 进行 HTML 编码输出。</span><span class="sxs-lookup"><span data-stu-id="016e3-127">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="016e3-128">这将替换保留的 HTML 字符 (如`<`和`>`和`&`) 与启用要显示为字符而不是被解释为 HTML 标记或实体的网页中的字符的代码。</span><span class="sxs-lookup"><span data-stu-id="016e3-128">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="016e3-129">HTML 编码，在服务器代码中的输出可能显示不正常，而无需无法公开安全风险的页。</span><span class="sxs-lookup"><span data-stu-id="016e3-129">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="016e3-130">如果你的目标是输出将标记呈现为标记的 HTML 标记 (例如`<p></p>`，段落或`<em></em>`强调文本)，请参阅明[组合文本、 标记和代码块中的代码](#BM_CombiningTextMarkupAndCode)本文后续部分中。</span><span class="sxs-lookup"><span data-stu-id="016e3-130">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="016e3-131">你可以阅读更多有关中的 HTML 编码[使用窗体](https://go.microsoft.com/fwlink/?LinkId=202892)。</span><span class="sxs-lookup"><span data-stu-id="016e3-131">You can read more about HTML encoding in [Working with Forms](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>


### <a name="2-you-enclose-code-blocks-in-braces"></a><span data-ttu-id="016e3-132">2.将代码块括在大括号中</span><span class="sxs-lookup"><span data-stu-id="016e3-132">2. You enclose code blocks in braces</span></span>

<span data-ttu-id="016e3-133">A*代码块*包括一个或多个代码语句并括在大括号。</span><span class="sxs-lookup"><span data-stu-id="016e3-133">A *code block* includes one or more code statements and is enclosed in braces.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

<span data-ttu-id="016e3-134">在浏览器中所显示的结果：</span><span class="sxs-lookup"><span data-stu-id="016e3-134">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a><span data-ttu-id="016e3-136">3.在块中，你最终用分号每个代码语句</span><span class="sxs-lookup"><span data-stu-id="016e3-136">3. Inside a block, you end each code statement with a semicolon</span></span>

<span data-ttu-id="016e3-137">在代码块中，每个完整的代码语句必须以分号结尾。</span><span class="sxs-lookup"><span data-stu-id="016e3-137">Inside a code block, each complete code statement must end with a semicolon.</span></span> <span data-ttu-id="016e3-138">内联表达式不以分号结尾。</span><span class="sxs-lookup"><span data-stu-id="016e3-138">Inline expressions don't end with a semicolon.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="016e3-139">4.使用变量来存储值</span><span class="sxs-lookup"><span data-stu-id="016e3-139">4. You use variables to store values</span></span>

<span data-ttu-id="016e3-140">你可以将值存储在*变量*，包括字符串、 数字和日期，等等。创建一个新的变量使用`var`关键字。</span><span class="sxs-lookup"><span data-stu-id="016e3-140">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `var` keyword.</span></span> <span data-ttu-id="016e3-141">你可以直接在页中使用插入变量值`@`。</span><span class="sxs-lookup"><span data-stu-id="016e3-141">You can insert variable values directly in a page using `@`.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

<span data-ttu-id="016e3-142">在浏览器中所显示的结果：</span><span class="sxs-lookup"><span data-stu-id="016e3-142">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="016e3-144">5.将文本字符串值括在双引号内</span><span class="sxs-lookup"><span data-stu-id="016e3-144">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="016e3-145">A*字符串*是作为文本处理的字符的序列。</span><span class="sxs-lookup"><span data-stu-id="016e3-145">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="016e3-146">若要指定一个字符串，则将它括在双引号中：</span><span class="sxs-lookup"><span data-stu-id="016e3-146">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

<span data-ttu-id="016e3-147">如果你想要显示的字符串包含反斜杠字符 ( `\` ) 或双击引号引起来 ( `"` )，使用*原义字符串*且具有前缀与`@`运算符。</span><span class="sxs-lookup"><span data-stu-id="016e3-147">If the string that you want to display contains a backslash character ( `\` ) or double quotation marks ( `"` ), use a *verbatim string literal* that's prefixed with the `@` operator.</span></span> <span data-ttu-id="016e3-148">(在 C# 中，\ 字符具有特殊含义，除非你使用原义字符串。)</span><span class="sxs-lookup"><span data-stu-id="016e3-148">(In C#, the \ character has special meaning unless you use a verbatim string literal.)</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

<span data-ttu-id="016e3-149">若要嵌入双引号括起来，使用原义字符串且不重复引号引起来：</span><span class="sxs-lookup"><span data-stu-id="016e3-149">To embed double quotation marks, use a verbatim string literal and repeat the quotation marks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

<span data-ttu-id="016e3-150">下面是在页中使用的两个这些示例的结果：</span><span class="sxs-lookup"><span data-stu-id="016e3-150">Here's the result of using both of these examples in a page:</span></span>

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> <span data-ttu-id="016e3-152">请注意，`@`标记在 C# 中逐字字符串文本和标记 ASP.NET 页中的代码使用字符。</span><span class="sxs-lookup"><span data-stu-id="016e3-152">Notice that the `@` character is used both to mark verbatim string literals in C# and to mark code in ASP.NET pages.</span></span>


### <a name="6-code-is-case-sensitive"></a><span data-ttu-id="016e3-153">6.代码是区分大小写</span><span class="sxs-lookup"><span data-stu-id="016e3-153">6. Code is case sensitive</span></span>

<span data-ttu-id="016e3-154">在 C# 中，关键字 (如`var`， `true`，和`if`) 且变量名称区分大小写。</span><span class="sxs-lookup"><span data-stu-id="016e3-154">In C#, keywords (like `var`, `true`, and `if`) and variable names are case sensitive.</span></span> <span data-ttu-id="016e3-155">代码的以下行创建两个不同的变量，`lastName`和 `LastName.`</span><span class="sxs-lookup"><span data-stu-id="016e3-155">The following lines of code create two different variables, `lastName` and `LastName.`</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

<span data-ttu-id="016e3-156">如果你声明一个变量，作为`var lastName = "Smith";`和如果你尝试引用该变量作为在页中的`@LastName`，产生错误，因为`LastName`将不会识别。</span><span class="sxs-lookup"><span data-stu-id="016e3-156">If you declare a variable as `var lastName = "Smith";` and if you try to reference that variable in your page as `@LastName`, an error results because `LastName` won't be recognized.</span></span>

> [!NOTE]
> <span data-ttu-id="016e3-157">在 Visual Basic 中，关键字和变量是*不*区分大小写。</span><span class="sxs-lookup"><span data-stu-id="016e3-157">In Visual Basic, keywords and variables are *not* case sensitive.</span></span>


### <a name="7-much-of-your-coding-involves-objects"></a><span data-ttu-id="016e3-158">7.大部分代码涉及对象</span><span class="sxs-lookup"><span data-stu-id="016e3-158">7. Much of your coding involves objects</span></span>

<span data-ttu-id="016e3-159">*对象*表示，你可以使用编程件事情&#8212;页、 文本框、 文件、 映像、 web 请求、 电子邮件、 客户记录 （数据库行），等等。对象具有描述其特征的属性并确保你可以读取或更改&#8212;文本框对象具有`Text`（及其他） 的属性，请求对象具有`Url`属性，电子邮件具有`From`属性，和客户对象都具有`FirstName`属性。</span><span class="sxs-lookup"><span data-stu-id="016e3-159">An *object* represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics and that you can read or change &#8212; a text box object has a `Text` property (among others), a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="016e3-160">对象还具有方法&quot;谓词&quot;他们可以执行。</span><span class="sxs-lookup"><span data-stu-id="016e3-160">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="016e3-161">示例包括文件对象的`Save`方法中，映像对象的`Rotate`方法和电子邮件对象的`Send`方法。</span><span class="sxs-lookup"><span data-stu-id="016e3-161">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="016e3-162">通常将使用`Request`对象，它会为你提供的文本框 （窗体字段） 的信息，如值在页上，浏览器的类型进行请求的 URL 的页面、 用户标识，等等。下面的示例演示如何访问属性的`Request`对象以及如何调用`MapPath`方法`Request`对象，这将使您在服务器上的页的绝对路径：</span><span class="sxs-lookup"><span data-stu-id="016e3-162">You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page, what type of browser made the request, the URL of the page, the user identity, etc. The following example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

<span data-ttu-id="016e3-163">在浏览器中所显示的结果：</span><span class="sxs-lookup"><span data-stu-id="016e3-163">The result displayed in a browser:</span></span>

![Razor Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="016e3-165">8.你可以编写做出决策的代码</span><span class="sxs-lookup"><span data-stu-id="016e3-165">8. You can write code that makes decisions</span></span>

<span data-ttu-id="016e3-166">动态网页的一项重要功能是你可以确定要执行的操作根据条件。</span><span class="sxs-lookup"><span data-stu-id="016e3-166">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="016e3-167">若要执行此操作的最常见方法是使用`if`语句 (和可选`else`语句)。</span><span class="sxs-lookup"><span data-stu-id="016e3-167">The most common way to do this is with the `if` statement (and optional `else` statement).</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

<span data-ttu-id="016e3-168">语句`if(IsPost)`是写入的速记方式`if(IsPost == true)`。</span><span class="sxs-lookup"><span data-stu-id="016e3-168">The statement `if(IsPost)` is a shorthand way of writing `if(IsPost == true)`.</span></span> <span data-ttu-id="016e3-169">连同`if`语句，有各种方法来测试条件，重复代码块，并依此类推，它们进行了描述这篇文章中更高版本。</span><span class="sxs-lookup"><span data-stu-id="016e3-169">Along with `if` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="016e3-170">在浏览器中所显示的结果 (单击后**提交**):</span><span class="sxs-lookup"><span data-stu-id="016e3-170">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a><span data-ttu-id="016e3-172">HTTP GET 和 POST 方法以及 IsPost 属性</span><span class="sxs-lookup"><span data-stu-id="016e3-172">HTTP GET and POST Methods and the IsPost Property</span></span>
> 
> <span data-ttu-id="016e3-173">用于网页 (HTTP) 的协议支持非常有限的数量的用于向服务器发出请求的方法 （谓词）。</span><span class="sxs-lookup"><span data-stu-id="016e3-173">The protocol used for web pages (HTTP) supports a very limited number of methods (verbs) that are used to make requests to the server.</span></span> <span data-ttu-id="016e3-174">两个最常见的是 GET，用于读取某页以及开机自检，用于提交的页面。</span><span class="sxs-lookup"><span data-stu-id="016e3-174">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="016e3-175">一般情况下，用户请求页面时，第一次请求页时使用 GET。</span><span class="sxs-lookup"><span data-stu-id="016e3-175">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="016e3-176">如果用户在填写窗体，然后单击提交按钮，浏览器向服务器发出的 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="016e3-176">If the user fills in a form and then clicks a submit button, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="016e3-177">在 web 编程中，它通常是有助于你了解是否请求该页为 GET 或 POST，以便你知道如何处理该页。</span><span class="sxs-lookup"><span data-stu-id="016e3-177">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="016e3-178">在 ASP.NET Web 页中，你可以使用`IsPost`属性以查看是否 GET 或 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="016e3-178">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="016e3-179">如果请求是 POST，`IsPost`属性将返回 true，并且可执行诸如读取窗体上的文本框的值。</span><span class="sxs-lookup"><span data-stu-id="016e3-179">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="016e3-180">你将看到许多示例演示如何处理以不同的方式根据的值页`IsPost`。</span><span class="sxs-lookup"><span data-stu-id="016e3-180">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>


## <a name="a-simple-code-example"></a><span data-ttu-id="016e3-181">一个简单代码示例</span><span class="sxs-lookup"><span data-stu-id="016e3-181">A Simple Code Example</span></span>

<span data-ttu-id="016e3-182">此过程演示如何创建阐释基本的编程技术的页。</span><span class="sxs-lookup"><span data-stu-id="016e3-182">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="016e3-183">在示例中，你将创建一个允许用户输入两个数字，然后再将它们添加显示结果页面。</span><span class="sxs-lookup"><span data-stu-id="016e3-183">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="016e3-184">在编辑器中创建一个新文件并将其命名*AddNumbers.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="016e3-184">In your editor, create a new file and name it *AddNumbers.cshtml*.</span></span>
2. <span data-ttu-id="016e3-185">将下面的代码和标记复制到页中，替换已在页中的任何内容。</span><span class="sxs-lookup"><span data-stu-id="016e3-185">Copy the following code and markup into the page, replacing anything already in the page.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    <span data-ttu-id="016e3-186">下面是为你要注意一些事项：</span><span class="sxs-lookup"><span data-stu-id="016e3-186">Here are some things for you to note:</span></span>

    - <span data-ttu-id="016e3-187">`@`字符在页中，启动代码的第一个块，它位于之前`totalMessage`嵌入在页面底部附近的变量。</span><span class="sxs-lookup"><span data-stu-id="016e3-187">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable that's embedded near the bottom of the page.</span></span>
    - <span data-ttu-id="016e3-188">在页面顶部块括在大括号中。</span><span class="sxs-lookup"><span data-stu-id="016e3-188">The block at the top of the page is enclosed in braces.</span></span>
    - <span data-ttu-id="016e3-189">在顶部块中，所有行以分号都结尾。</span><span class="sxs-lookup"><span data-stu-id="016e3-189">In the block at the top, all lines end with a semicolon.</span></span>
    - <span data-ttu-id="016e3-190">变量`total`， `num1`， `num2`，和`totalMessage`存储多个数字和字符串。</span><span class="sxs-lookup"><span data-stu-id="016e3-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="016e3-191">分配给的文字字符串值`totalMessage`变量是在双引号内。</span><span class="sxs-lookup"><span data-stu-id="016e3-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="016e3-192">由于代码时区分大小写，因此`totalMessage`变量使用页面底部附近，其名称必须与在顶部变量完全匹配。</span><span class="sxs-lookup"><span data-stu-id="016e3-192">Because the code is case-sensitive, when the `totalMessage` variable is used near the bottom of the page, its name must match the variable at the top exactly.</span></span>
    - <span data-ttu-id="016e3-193">表达式`num1.AsInt() + num2.AsInt()`演示如何使用对象和方法。</span><span class="sxs-lookup"><span data-stu-id="016e3-193">The expression `num1.AsInt() + num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="016e3-194">`AsInt`上每个变量的方法将转换到号 （整数） 输入的用户，因此，你可以在其上执行算术的字符串。</span><span class="sxs-lookup"><span data-stu-id="016e3-194">The `AsInt` method on each variable converts the string entered by a user to a number (an integer) so that you can perform arithmetic on it.</span></span>
    - <span data-ttu-id="016e3-195">`<form>`标记包含`method="post"`属性。</span><span class="sxs-lookup"><span data-stu-id="016e3-195">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="016e3-196">此步骤指定当用户单击**添加**，页面将发送到服务器使用 HTTP POST 方法。</span><span class="sxs-lookup"><span data-stu-id="016e3-196">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="016e3-197">当提交页时，`if(IsPost)`测试的计算结果为 true，而条件性代码运行时，显示的添加数字结果。</span><span class="sxs-lookup"><span data-stu-id="016e3-197">When the page is submitted, the `if(IsPost)` test evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="016e3-198">保存页并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="016e3-198">Save the page and run it in a browser.</span></span> <span data-ttu-id="016e3-199">(请确保页中选择**文件**工作区之前运行它。)输入两个整数，然后单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="016e3-199">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span> 

    ![Razor Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a><span data-ttu-id="016e3-201">基本编程概念</span><span class="sxs-lookup"><span data-stu-id="016e3-201">Basic Programming Concepts</span></span>

<span data-ttu-id="016e3-202">本文为你提供了 ASP.NET web 编程的概述。</span><span class="sxs-lookup"><span data-stu-id="016e3-202">This article provides you with an overview of ASP.NET web programming.</span></span> <span data-ttu-id="016e3-203">并不详尽检查，只需通过将最常使用的编程概念的快速教程。</span><span class="sxs-lookup"><span data-stu-id="016e3-203">It isn't an exhaustive examination, just a quick tour through the programming concepts you'll use most often.</span></span> <span data-ttu-id="016e3-204">即便如此，它涵盖几乎所有操作都将需要若要开始使用 ASP.NET Web 页。</span><span class="sxs-lookup"><span data-stu-id="016e3-204">Even so, it covers almost everything you'll need to get started with ASP.NET Web Pages.</span></span>

<span data-ttu-id="016e3-205">但首先，很少的技术背景。</span><span class="sxs-lookup"><span data-stu-id="016e3-205">But first, a little technical background.</span></span>

### <a name="the-razor-syntax-server-code-and-aspnet"></a><span data-ttu-id="016e3-206">Razor 语法、 服务器代码和 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="016e3-206">The Razor Syntax, Server Code, and ASP.NET</span></span>

<span data-ttu-id="016e3-207">Razor 语法是一种简单的编程语法，为基于服务器的代码嵌入在网页中。</span><span class="sxs-lookup"><span data-stu-id="016e3-207">Razor syntax is a simple programming syntax for embedding server-based code in a web page.</span></span> <span data-ttu-id="016e3-208">在使用 Razor 语法的网页，有两种类型的内容： 客户端内容和服务器代码。</span><span class="sxs-lookup"><span data-stu-id="016e3-208">In a web page that uses the Razor syntax, there are two kinds of content: client content and server code.</span></span> <span data-ttu-id="016e3-209">客户端的内容是用于在网页中的内容： HTML 标记 （元素） 的样式如 CSS 的信息可能某些客户端脚本，如 JavaScript 和纯文本。</span><span class="sxs-lookup"><span data-stu-id="016e3-209">Client content is the stuff you're used to in web pages: HTML markup (elements), style information such as CSS, maybe some client script such as JavaScript, and plain text.</span></span>

<span data-ttu-id="016e3-210">Razor 语法允许您添加到此客户端内容的服务器代码。</span><span class="sxs-lookup"><span data-stu-id="016e3-210">Razor syntax lets you add server code to this client content.</span></span> <span data-ttu-id="016e3-211">如果存在服务器代码页中，服务器运行该代码第一次，再将页发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="016e3-211">If there's server code in the page, the server runs that code first, before it sends the page to the browser.</span></span> <span data-ttu-id="016e3-212">通过在服务器上运行，代码可以执行任务，可以是更加复杂，无法使用客户端内容单独出现时，例如类似于访问基于服务器的数据库执行操作。</span><span class="sxs-lookup"><span data-stu-id="016e3-212">By running on the server, the code can perform tasks that can be a lot more complex to do using client content alone, like accessing server-based databases.</span></span> <span data-ttu-id="016e3-213">服务器代码最重要的是，动态创建客户端内容&#8212;它可以生成 HTML 标记或在运行过程中的其他内容中并发送到以及页可能会包含任何静态 HTML 浏览器。</span><span class="sxs-lookup"><span data-stu-id="016e3-213">Most importantly, server code can dynamically create client content &#8212; it can generate HTML markup or other content on the fly and then send it to the browser along with any static HTML that the page might contain.</span></span> <span data-ttu-id="016e3-214">从浏览器的角度来看，由服务器代码生成的客户端内容是比任何其他内容，客户端没有什么不同。</span><span class="sxs-lookup"><span data-stu-id="016e3-214">From the browser's perspective, client content that's generated by your server code is no different than any other client content.</span></span> <span data-ttu-id="016e3-215">如你已经了解，具有所需的服务器代码是非常简单。</span><span class="sxs-lookup"><span data-stu-id="016e3-215">As you've already seen, the server code that's required is quite simple.</span></span>

<span data-ttu-id="016e3-216">包含 Razor 语法的 ASP.NET web pages 具有特殊的文件扩展名 (*.cshtml*或 *.vbhtml*)。</span><span class="sxs-lookup"><span data-stu-id="016e3-216">ASP.NET web pages that include the Razor syntax have a special file extension (*.cshtml* or *.vbhtml*).</span></span> <span data-ttu-id="016e3-217">服务器可识别这些扩展，运行的代码，使用 Razor 语法标记，然后将页发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="016e3-217">The server recognizes these extensions, runs the code that's marked with Razor syntax, and then sends the page to the browser.</span></span>

### <a name="where-does-aspnet-fit-in"></a><span data-ttu-id="016e3-218">ASP.NET 放置何处？</span><span class="sxs-lookup"><span data-stu-id="016e3-218">Where does ASP.NET fit in?</span></span>

<span data-ttu-id="016e3-219">Razor 语法取决于从调用 ASP.NET，又基于 Microsoft.NET Framework 的 Microsoft 技术。</span><span class="sxs-lookup"><span data-stu-id="016e3-219">Razor syntax is based on a technology from Microsoft called ASP.NET, which in turn is based on the Microsoft .NET Framework.</span></span> <span data-ttu-id="016e3-220">.Net Framework 开发几乎任何类型的计算机应用程序是一个大型的全面编程框架，从 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="016e3-220">The.NET Framework is a big, comprehensive programming framework from Microsoft for developing virtually any type of computer application.</span></span> <span data-ttu-id="016e3-221">ASP.NET 是专门设计用于创建 web 应用程序的.NET framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="016e3-221">ASP.NET is the part of the .NET Framework that's specifically designed for creating web applications.</span></span> <span data-ttu-id="016e3-222">开发人员使用 ASP.NET 创建的最大值和最高流量网站许多世界。</span><span class="sxs-lookup"><span data-stu-id="016e3-222">Developers have used ASP.NET to create many of the largest and highest-traffic websites in the world.</span></span> <span data-ttu-id="016e3-223">(你看到的文件扩展名的任何时间 *.aspx*作为站点中的 URL 的一部分，你将知道站点编写使用 ASP.NET。)</span><span class="sxs-lookup"><span data-stu-id="016e3-223">(Any time you see the file-name extension *.aspx* as part of the URL in a site, you'll know that the site was written using ASP.NET.)</span></span>

<span data-ttu-id="016e3-224">Razor 语法使您能够 ASP.NET，但使用可以更轻松地了解当你方面的专家，如果您是初学者，可将你提高工作效率的简化的语法的所有功能。</span><span class="sxs-lookup"><span data-stu-id="016e3-224">The Razor syntax gives you all the power of ASP.NET, but using a simplified syntax that's easier to learn if you're a beginner and that makes you more productive if you're an expert.</span></span> <span data-ttu-id="016e3-225">即使此语法是易于使用，它与 ASP.NET 和.NET Framework 的系列关系意味着，在您的网站变得越来越复杂，你会有更大的框架可供你的 power。</span><span class="sxs-lookup"><span data-stu-id="016e3-225">Even though this syntax is simple to use, its family relationship to ASP.NET and the .NET Framework means that as your websites become more sophisticated, you have the power of the larger frameworks available to you.</span></span>

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> <span data-ttu-id="016e3-227">**类和实例**</span><span class="sxs-lookup"><span data-stu-id="016e3-227">**Classes and Instances**</span></span>
> 
> <span data-ttu-id="016e3-228">ASP.NET 服务器代码使用反过来生成类的理论基础的对象。</span><span class="sxs-lookup"><span data-stu-id="016e3-228">ASP.NET server code uses objects, which are in turn built on the idea of classes.</span></span> <span data-ttu-id="016e3-229">此类是定义或模板对象。</span><span class="sxs-lookup"><span data-stu-id="016e3-229">The class is the definition or template for an object.</span></span> <span data-ttu-id="016e3-230">例如，应用程序可能包含`Customer`定义的属性和任何客户对象所需的方法的类。</span><span class="sxs-lookup"><span data-stu-id="016e3-230">For example, an application might contain a `Customer` class that defines the properties and methods that any customer object needs.</span></span>
> 
> <span data-ttu-id="016e3-231">当应用程序需要处理的实际客户信息时，它创建的实例 (或*实例化*) 的客户对象。</span><span class="sxs-lookup"><span data-stu-id="016e3-231">When the application needs to work with actual customer information, it creates an instance of (or *instantiates*) a customer object.</span></span> <span data-ttu-id="016e3-232">每个单独的客户是一个单独的实例`Customer`类。</span><span class="sxs-lookup"><span data-stu-id="016e3-232">Each individual customer is a separate instance of the `Customer` class.</span></span> <span data-ttu-id="016e3-233">每个实例支持的相同的属性和方法，但每个实例的属性值通常不同，因为每个客户对象是唯一的。</span><span class="sxs-lookup"><span data-stu-id="016e3-233">Every instance supports the same properties and methods, but the property values for each instance are typically different, because each customer object is unique.</span></span> <span data-ttu-id="016e3-234">一个客户对象中`LastName`属性可能是"Smith"; 在另一个客户对象，`LastName`属性可能是"Jones"。</span><span class="sxs-lookup"><span data-stu-id="016e3-234">In one customer object, the `LastName` property might be "Smith"; in another customer object, the `LastName` property might be "Jones."</span></span>
> 
> <span data-ttu-id="016e3-235">同样，在你的站点中任何单个 web 页是`Page`是的一个实例的对象`Page`类。</span><span class="sxs-lookup"><span data-stu-id="016e3-235">Similarly, any individual web page in your site is a `Page` object that's an instance of the `Page` class.</span></span> <span data-ttu-id="016e3-236">页上的按钮是`Button`是的一个实例的对象`Button`类中，依次类推。</span><span class="sxs-lookup"><span data-stu-id="016e3-236">A button on the page is a `Button` object that is an instance of the `Button` class, and so on.</span></span> <span data-ttu-id="016e3-237">每个实例都具有其自己的特征，但它们都基于对象的类定义中指定的内容。</span><span class="sxs-lookup"><span data-stu-id="016e3-237">Each instance has its own characteristics, but they all are based on what's specified in the object's class definition.</span></span>


## <a name="basic-syntax"></a><span data-ttu-id="016e3-238">基本语法</span><span class="sxs-lookup"><span data-stu-id="016e3-238">Basic Syntax</span></span>

<span data-ttu-id="016e3-239">前面你已了解如何创建一个 ASP.NET Web Pages 页面上，以及如何将服务器代码添加到 HTML 标记的一个基本示例。</span><span class="sxs-lookup"><span data-stu-id="016e3-239">Earlier you saw a basic example of how to create an ASP.NET Web Pages page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="016e3-240">此处将介绍编写使用 Razor 语法的 ASP.NET 服务器代码的基础知识&#8212;，即使用编程语言规则。</span><span class="sxs-lookup"><span data-stu-id="016e3-240">Here you'll learn the basics of writing ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="016e3-241">如果你有使用编程 （尤其是如果您使用过 C、 c + +、 C#、 Visual Basic 或 JavaScript） 的经验，此处读取大部分将熟悉。</span><span class="sxs-lookup"><span data-stu-id="016e3-241">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="016e3-242">你可能需要先熟悉一下仅如何服务器代码添加到标记中 *.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="016e3-242">You'll probably need to familiarize yourself only with how server code is added to markup in *.cshtml* files.</span></span>

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a><span data-ttu-id="016e3-243">组合文本、 标记和代码块中的代码</span><span class="sxs-lookup"><span data-stu-id="016e3-243">Combining Text, Markup, and Code in Code Blocks</span></span>

<span data-ttu-id="016e3-244">在服务器代码块内，你通常想输出文本或标记 （或两者） 页。</span><span class="sxs-lookup"><span data-stu-id="016e3-244">In server code blocks, you often want to output text or markup (or both) to the page.</span></span> <span data-ttu-id="016e3-245">如果服务器代码块包含的文本，不是代码和，而是应呈现原样，ASP.NET 将需要能够将该文本与代码区分开来。</span><span class="sxs-lookup"><span data-stu-id="016e3-245">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="016e3-246">有若干方法可实现此操作。</span><span class="sxs-lookup"><span data-stu-id="016e3-246">There are several ways to do this.</span></span>

- <span data-ttu-id="016e3-247">将文本括在 HTML 元素类似`<p></p>`或`<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="016e3-247">Enclose the text in an HTML element like `<p></p>` or `<em></em>`:</span></span>   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    <span data-ttu-id="016e3-248">文本、 其他 HTML 元素和服务器代码表达式，可以包括 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="016e3-248">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="016e3-249">当 ASP.NET 发现开始 HTML 标记 (例如， `<p>`)、 呈现包括元素的所有内容和浏览器中，解决服务器代码表达式，因为它将是作为其内容。</span><span class="sxs-lookup"><span data-stu-id="016e3-249">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything including the element and its content as is to the browser, resolving server-code expressions as it goes.</span></span>
- <span data-ttu-id="016e3-250">使用`@:`运算符或`<text>`元素。</span><span class="sxs-lookup"><span data-stu-id="016e3-250">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="016e3-251">`@:`输出单个行的内容包含纯文本或不匹配的 HTML 标记;`<text>`元素包含多行输出。</span><span class="sxs-lookup"><span data-stu-id="016e3-251">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="016e3-252">当你不想要呈现的 HTML 元素作为输出的一部分，这些选项非常有用。</span><span class="sxs-lookup"><span data-stu-id="016e3-252">These options are useful when you don't want to render an HTML element as part of the output.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    <span data-ttu-id="016e3-253">如果你想要输出的文本或不匹配的 HTML 标记的多个行，你可以在前面的每一行`@:`，或可以放置在行外侧`<text>`元素。</span><span class="sxs-lookup"><span data-stu-id="016e3-253">If you want to output multiple lines of text or unmatched HTML tags, you can precede each line with `@:`, or you can enclose the line in a `<text>` element.</span></span> <span data-ttu-id="016e3-254">如`@:`运算符，`<text>`标记 ASP.NET 用于识别文本内容，并且永远不会呈现在页输出中。</span><span class="sxs-lookup"><span data-stu-id="016e3-254">Like the `@:` operator,`<text>` tags are used by ASP.NET to identify text content and are never rendered in the page output.</span></span>

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    <span data-ttu-id="016e3-255">第一个示例重复前面的示例，但使用一对`<text>`标记括起要呈现的文本。</span><span class="sxs-lookup"><span data-stu-id="016e3-255">The first example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span> <span data-ttu-id="016e3-256">在第二个示例中，`<text>`和`</text>`标记括起三行，它们都有一些非包含的文本和不匹配的 HTML 标记的行 (`<br />`)，以及服务器代码和匹配的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="016e3-256">In the second example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="016e3-257">另外无法再次，先完成每个行分别`@:`运算符; 它们的方式都有效。</span><span class="sxs-lookup"><span data-stu-id="016e3-257">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    > [!NOTE]
    > <span data-ttu-id="016e3-258">此部分中所述，输出文本的时&#8212;使用 HTML 元素，`@:`运算符，或`<text>`元素&#8212;ASP.NET 不会进行 HTML 编码输出。</span><span class="sxs-lookup"><span data-stu-id="016e3-258">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="016e3-259">(如前所述，ASP.NET 未编码的服务器的代码表达式和服务器代码块前面带有输出`@`，除非在本节中所述的特殊情况。)</span><span class="sxs-lookup"><span data-stu-id="016e3-259">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="016e3-260">Whitespace</span><span class="sxs-lookup"><span data-stu-id="016e3-260">Whitespace</span></span>

<span data-ttu-id="016e3-261">在语句中 （和外部字符串文本） 的额外空间不会影响该语句：</span><span class="sxs-lookup"><span data-stu-id="016e3-261">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

<span data-ttu-id="016e3-262">在语句中的换行符的语句上无效，并可以将包装语句的可读性。</span><span class="sxs-lookup"><span data-stu-id="016e3-262">A line break in a statement has no effect on the statement, and you can wrap statements for readability.</span></span> <span data-ttu-id="016e3-263">以下语句是相同的：</span><span class="sxs-lookup"><span data-stu-id="016e3-263">The following statements are the same:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

<span data-ttu-id="016e3-264">但是，不能环绕文本字符串中间的行。</span><span class="sxs-lookup"><span data-stu-id="016e3-264">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="016e3-265">下面的示例不起作用：</span><span class="sxs-lookup"><span data-stu-id="016e3-265">The following example doesn't work:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

<span data-ttu-id="016e3-266">若要合并的长字符串换行到多个行与上面的代码一样，有两个选项。</span><span class="sxs-lookup"><span data-stu-id="016e3-266">To combine a long string that wraps to multiple lines like the above code, there are two options.</span></span> <span data-ttu-id="016e3-267">可以使用串联运算符 (`+`)，您可以看到这篇文章中更高版本。</span><span class="sxs-lookup"><span data-stu-id="016e3-267">You can use the concatenation operator (`+`), which you'll see later in this article.</span></span> <span data-ttu-id="016e3-268">你还可以使用`@`创建原义字符串文本，如本文前面看到的字符。</span><span class="sxs-lookup"><span data-stu-id="016e3-268">You can also use the `@` character to create a verbatim string literal, as you saw earlier in this article.</span></span> <span data-ttu-id="016e3-269">你可以位于同一行中逐字字符串文本：</span><span class="sxs-lookup"><span data-stu-id="016e3-269">You can break verbatim string literals across lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a><span data-ttu-id="016e3-270">代码 （和标记） 注释</span><span class="sxs-lookup"><span data-stu-id="016e3-270">Code (and Markup) Comments</span></span>

<span data-ttu-id="016e3-271">注释可以为自己或他人留言。</span><span class="sxs-lookup"><span data-stu-id="016e3-271">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="016e3-272">它们还使您可以禁用 (*注释掉*) 部分的代码或不想运行但想要保留暂时在页中的标记。</span><span class="sxs-lookup"><span data-stu-id="016e3-272">They also allow you to disable (*comment out*) a section of code or markup that you don't want to run but want to keep in your page for the time being.</span></span>

<span data-ttu-id="016e3-273">没有不同注释语法 Razor 代码以及的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="016e3-273">There's different commenting syntax for Razor code and for HTML markup.</span></span> <span data-ttu-id="016e3-274">与所有 Razor 代码中，Razor 注释处理 （，然后删除） 页发送到浏览器之前在服务器上。</span><span class="sxs-lookup"><span data-stu-id="016e3-274">As with all Razor code, Razor comments are processed (and then removed) on the server before the page is sent to the browser.</span></span> <span data-ttu-id="016e3-275">因此，Razor 注释语法可以放置时编辑文件，但用户看不到，即使在页面源文件中，可以看到的注释到代码 （或甚至向的标记）。</span><span class="sxs-lookup"><span data-stu-id="016e3-275">Therefore, the Razor commenting syntax lets you put comments into the code (or even into the markup) that you can see when you edit the file, but that users don't see, even in the page source.</span></span>

<span data-ttu-id="016e3-276">对于 ASP.NET Razor 注释你开始在批注`@*`，并与的结尾`*@`。</span><span class="sxs-lookup"><span data-stu-id="016e3-276">For ASP.NET Razor comments, you start the comment with `@*` and end it with `*@`.</span></span> <span data-ttu-id="016e3-277">注释可以是多了一行或多个行：</span><span class="sxs-lookup"><span data-stu-id="016e3-277">The comment can be on one line or multiple lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

<span data-ttu-id="016e3-278">下面是在代码块的注释：</span><span class="sxs-lookup"><span data-stu-id="016e3-278">Here is a comment within a code block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

<span data-ttu-id="016e3-279">下面的代码行的相同块的代码，注释掉，以便它不会运行：</span><span class="sxs-lookup"><span data-stu-id="016e3-279">Here is the same block of code, with the line of code commented out so that it won't run:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

<span data-ttu-id="016e3-280">在代码块中，除了使用 Razor 注释语法，你可以使用你使用的如 C# 的编程语言的注释语法：</span><span class="sxs-lookup"><span data-stu-id="016e3-280">Inside a code block, as an alternative to using Razor comment syntax, you can use the commenting syntax of the programming language you're using, such as C#:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

<span data-ttu-id="016e3-281">C# 中的单行注释前面带有`//`字符和多行注释开头`/*`和以结尾`*/`。</span><span class="sxs-lookup"><span data-stu-id="016e3-281">In C#, single-line comments are preceded by the `//` characters, and multi-line comments begin with `/*` and end with `*/`.</span></span> <span data-ttu-id="016e3-282">（与 Razor 注释，C# 注释不会呈现到浏览器。）</span><span class="sxs-lookup"><span data-stu-id="016e3-282">(As with Razor comments, C# comments are not rendered to the browser.)</span></span>

<span data-ttu-id="016e3-283">对于标记，你可能知道，你可以创建的 HTML 注释：</span><span class="sxs-lookup"><span data-stu-id="016e3-283">For markup, as you probably know, you can create an HTML comment:</span></span>

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

<span data-ttu-id="016e3-284">HTML 注释开头`<!--`字符和以结尾`-->`。</span><span class="sxs-lookup"><span data-stu-id="016e3-284">HTML comments start with `<!--` characters and end with `-->`.</span></span> <span data-ttu-id="016e3-285">可以使用 HTML 注释来包围不仅文本，而且还可能想要保留在页中但不想要呈现任何 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="016e3-285">You can use HTML comments to surround not only text, but also any HTML markup that you may want to keep in the page but don't want to render.</span></span> <span data-ttu-id="016e3-286">此 HTML 注释将隐藏，标记，并且它们包含的文本的整个内容：</span><span class="sxs-lookup"><span data-stu-id="016e3-286">This HTML comment will hide the entire content of the tags and the text they contain:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

<span data-ttu-id="016e3-287">与不同的是 Razor 注释，HTML 注释*是*呈现到页和用户可以通过查看页面源文件来查看它们。</span><span class="sxs-lookup"><span data-stu-id="016e3-287">Unlike Razor comments, HTML comments *are* rendered to the page and the user can see them by viewing the page source.</span></span>

<span data-ttu-id="016e3-288">有关 C# 的嵌套块，razor 具有限制。</span><span class="sxs-lookup"><span data-stu-id="016e3-288">Razor has limitations on nested blocks of C#.</span></span> <span data-ttu-id="016e3-289">有关详细信息请参阅[名为 C# 变量和嵌套块生成中断代码](http://aspnetwebstack.codeplex.com/workitem/1914)</span><span class="sxs-lookup"><span data-stu-id="016e3-289">For more information see [Named C# Variables and Nested Blocks Generate Broken Code](http://aspnetwebstack.codeplex.com/workitem/1914)</span></span>

## <a name="variables"></a><span data-ttu-id="016e3-290">变量</span><span class="sxs-lookup"><span data-stu-id="016e3-290">Variables</span></span>

<span data-ttu-id="016e3-291">变量是用于存储数据的已命名的对象。</span><span class="sxs-lookup"><span data-stu-id="016e3-291">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="016e3-292">您可以命名变量的任何内容，但名称必须以字母字符开头，不能包含空格或保留的字符。</span><span class="sxs-lookup"><span data-stu-id="016e3-292">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="016e3-293">变量和数据类型</span><span class="sxs-lookup"><span data-stu-id="016e3-293">Variables and Data Types</span></span>

<span data-ttu-id="016e3-294">变量可以具有特定的数据类型，这表示什么类型的数据存储在变量中。</span><span class="sxs-lookup"><span data-stu-id="016e3-294">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="016e3-295">你可以存储字符串值的字符串变量 (如&quot;Hello world&quot;)，整数变量，其中存储整数值 （如 3 或 79） 和各种 （例如，2012 年 4 月 12 日或 2009 年 3 月的格式存储日期值的日期变量).</span><span class="sxs-lookup"><span data-stu-id="016e3-295">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="016e3-296">还有许多其他可以使用的数据类型。</span><span class="sxs-lookup"><span data-stu-id="016e3-296">And there are many other data types you can use.</span></span>

<span data-ttu-id="016e3-297">但是，你通常不必指定类型的变量。</span><span class="sxs-lookup"><span data-stu-id="016e3-297">However, you generally don't have to specify a type for a variable.</span></span> <span data-ttu-id="016e3-298">大多数情况下，ASP.NET 可以找出基于了如何使用变量中的数据的类型。</span><span class="sxs-lookup"><span data-stu-id="016e3-298">Most of the time, ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="016e3-299">（有时必须指定一个类型; 你将看到示例其中是如此。）</span><span class="sxs-lookup"><span data-stu-id="016e3-299">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="016e3-300">声明变量的使用`var`关键字 （如果你不想指定类型） 或通过使用类型的名称：</span><span class="sxs-lookup"><span data-stu-id="016e3-300">You declare a variable using the `var` keyword (if you don't want to specify a type) or by using the name of the type:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

<span data-ttu-id="016e3-301">下面的示例演示在网页中的变量的一些典型用法：</span><span class="sxs-lookup"><span data-stu-id="016e3-301">The following example shows some typical uses of variables in a web page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

<span data-ttu-id="016e3-302">如果合并前面的示例在页中，你将看到此浏览器中显示：</span><span class="sxs-lookup"><span data-stu-id="016e3-302">If you combine the previous examples in a page, you see this displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="016e3-304">转换和测试数据类型</span><span class="sxs-lookup"><span data-stu-id="016e3-304">Converting and Testing Data Types</span></span>

<span data-ttu-id="016e3-305">尽管 ASP.NET 通常可以自动确定数据类型，有时它不能。</span><span class="sxs-lookup"><span data-stu-id="016e3-305">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="016e3-306">因此，你可能需要帮助解决 ASP.NET，通过执行显式转换。</span><span class="sxs-lookup"><span data-stu-id="016e3-306">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="016e3-307">即使你无需转换类型，有时会有帮助进行测试以查看哪种类型的数据你可能正在处理。</span><span class="sxs-lookup"><span data-stu-id="016e3-307">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="016e3-308">最常见的情况是，你必须将字符串转换为另一个类型，如整数或日期。</span><span class="sxs-lookup"><span data-stu-id="016e3-308">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="016e3-309">下面的示例演示一种典型情况其中必须将字符串转换为数字。</span><span class="sxs-lookup"><span data-stu-id="016e3-309">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

<span data-ttu-id="016e3-310">一般来说，用户输入发送给您作为字符串。</span><span class="sxs-lookup"><span data-stu-id="016e3-310">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="016e3-311">即使已提示用户输入一个数字，并且即使在提交用户输入而读取在代码中所输入的一个数字，数据是字符串格式。</span><span class="sxs-lookup"><span data-stu-id="016e3-311">Even if you've prompted users to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="016e3-312">因此，你必须将字符串转换为数字。</span><span class="sxs-lookup"><span data-stu-id="016e3-312">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="016e3-313">在示例中，如果你尝试对值执行算术运算，而不转换它们，以下的错误结果，因为 ASP.NET 不能添加两个字符串：</span><span class="sxs-lookup"><span data-stu-id="016e3-313">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

<span data-ttu-id="016e3-314">*不能隐式转换为 int 的 string 类型。*</span><span class="sxs-lookup"><span data-stu-id="016e3-314">*Cannot implicitly convert type 'string' to 'int'.*</span></span>

<span data-ttu-id="016e3-315">若要将值转换为整数，则调用`AsInt`方法。</span><span class="sxs-lookup"><span data-stu-id="016e3-315">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="016e3-316">如果转换成功，你可以然后添加数字。</span><span class="sxs-lookup"><span data-stu-id="016e3-316">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="016e3-317">下表列出了一些常见的转换和测试方法的变量。</span><span class="sxs-lookup"><span data-stu-id="016e3-317">The following table lists some common conversion and test methods for variables.</span></span>

<span data-ttu-id="016e3-318">::: 行:::::: 列:::<strong>方法</strong>::: 列端:::::: 列:::<strong>说明</strong>::: 列端:::::: 列:::<strong>示例</strong>::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-318">:::row::: :::column::: <strong>Method</strong> :::column-end::: :::column::: <strong>Description</strong> :::column-end::: :::column::: <strong>Example</strong> :::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-319">::: 行:::::: 列::: `AsInt(), IsInt()` ::: 列端:::::: 列::: 将转换为整数表示整数数量 （如"593") 的字符串。</span><span class="sxs-lookup"><span data-stu-id="016e3-319">:::row::: :::column::: `AsInt(), IsInt()` :::column-end::: :::column::: Converts a string that represents a whole number (like "593") to an integer.</span></span>
<span data-ttu-id="016e3-320">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-320">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]</span></span>
    <span data-ttu-id="016e3-321">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-321">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-322">::: 行:::::: 列::: `AsBool(), IsBool()` ::: 列端:::::: 列::: 将转换字符串如下所示&quot;true&quot;或&quot;false&quot;到类型为 Boolean 类型。</span><span class="sxs-lookup"><span data-stu-id="016e3-322">:::row::: :::column::: `AsBool(), IsBool()` :::column-end::: :::column::: Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
<span data-ttu-id="016e3-323">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-323">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]</span></span>
    <span data-ttu-id="016e3-324">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-324">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-325">::: 行:::::: 列::: `AsFloat(), IsFloat()` ::: 列端:::::: 列::: 将具有类似的十进制值的字符串转换&quot;1.3&quot;或&quot;7.439&quot;为浮点数。</span><span class="sxs-lookup"><span data-stu-id="016e3-325">:::row::: :::column::: `AsFloat(), IsFloat()` :::column-end::: :::column::: Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
<span data-ttu-id="016e3-326">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-326">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]</span></span>
    <span data-ttu-id="016e3-327">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-327">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-328">::: 行:::::: 列::: `AsDecimal(), IsDecimal()` ::: 列端:::::: 列::: 将具有类似的十进制值的字符串转换&quot;1.3&quot;或&quot;7.439&quot;为十进制数。</span><span class="sxs-lookup"><span data-stu-id="016e3-328">:::row::: :::column::: `AsDecimal(), IsDecimal()` :::column-end::: :::column::: Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="016e3-329">（在 ASP.NET 中，十进制数是比浮点数更精确。）::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-329">(In ASP.NET, a decimal number is more precise than a floating-point number.) :::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]</span></span>
    <span data-ttu-id="016e3-330">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-330">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-331">::: 行:::::: 列::: `AsDateTime(), IsDateTime()` ::: 列端:::::: 列::: 将对 ASP.NET 表示的日期和时间值的字符串转换`DateTime`类型。</span><span class="sxs-lookup"><span data-stu-id="016e3-331">:::row::: :::column::: `AsDateTime(), IsDateTime()` :::column-end::: :::column::: Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
<span data-ttu-id="016e3-332">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-332">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]</span></span>
    <span data-ttu-id="016e3-333">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-333">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-334">::: 行:::::: 列::: `ToString()` ::: 列端:::::: 列::: 将任何其他数据类型转换为字符串。</span><span class="sxs-lookup"><span data-stu-id="016e3-334">:::row::: :::column::: `ToString()` :::column-end::: :::column::: Converts any other data type to a string.</span></span>
<span data-ttu-id="016e3-335">::: 列端:::::: 列::: [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]</span><span class="sxs-lookup"><span data-stu-id="016e3-335">:::column-end::: :::column::: [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]</span></span>
    <span data-ttu-id="016e3-336">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-336">:::column-end::: :::row-end:::</span></span>

## <a name="operators"></a><span data-ttu-id="016e3-337">运算符</span><span class="sxs-lookup"><span data-stu-id="016e3-337">Operators</span></span>

<span data-ttu-id="016e3-338">运算符是命令的关键字或哪种类型的表达式中执行将告诉 ASP.NET 的字符。</span><span class="sxs-lookup"><span data-stu-id="016e3-338">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="016e3-339">C# 语言 （和基于它的 Razor 语法） 支持很多运算符，但你只需以识别一些吧。</span><span class="sxs-lookup"><span data-stu-id="016e3-339">The C# language (and the Razor syntax that's based on it) supports many operators, but you only need to recognize a few to get started.</span></span> <span data-ttu-id="016e3-340">下表总结了最常用的运算符。</span><span class="sxs-lookup"><span data-stu-id="016e3-340">The following table summarizes the most common operators.</span></span>


<span data-ttu-id="016e3-341">::: 行:::::: 列:::<strong>运算符</strong>::: 列端:::::: 列:::<strong>说明</strong>::: 列端:::::: 列:::<strong>示例</strong>::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-341">:::row::: :::column::: <strong>Operator</strong> :::column-end::: :::column::: <strong>Description</strong> :::column-end::: :::column::: <strong>Examples</strong> :::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-342">::: 行:::::: 列::: `+` `-` `*` `/` ::: 列端:::::: 列::: 数学运算符在数值表达式中使用。</span><span class="sxs-lookup"><span data-stu-id="016e3-342">:::row::: :::column::: `+` `-` `*` `/` :::column-end::: :::column::: Math operators used in numerical expressions.</span></span>
<span data-ttu-id="016e3-343">::: 列端:::::: 列::: [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]</span><span class="sxs-lookup"><span data-stu-id="016e3-343">:::column-end::: :::column::: [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]</span></span>
    <span data-ttu-id="016e3-344">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-344">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-345">::: 行:::::: 列::: `=` ::: 列端:::::: 列::: 分配。</span><span class="sxs-lookup"><span data-stu-id="016e3-345">:::row::: :::column::: `=` :::column-end::: :::column::: Assignment.</span></span> <span data-ttu-id="016e3-346">将一条语句右侧的值分配给左侧的对象。</span><span class="sxs-lookup"><span data-stu-id="016e3-346">Assigns the value on the right side of a statement to the object on the left side.</span></span>
<span data-ttu-id="016e3-347">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-347">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]</span></span>
    <span data-ttu-id="016e3-348">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-348">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-349">::: 行:::::: 列::: `==` ::: 列端:::::: 列::: 是否相等。</span><span class="sxs-lookup"><span data-stu-id="016e3-349">:::row::: :::column::: `==` :::column-end::: :::column::: Equality.</span></span> <span data-ttu-id="016e3-350">返回`true`如果这些值是否相等。</span><span class="sxs-lookup"><span data-stu-id="016e3-350">Returns `true` if the values are equal.</span></span> <span data-ttu-id="016e3-351">(请注意之间的区别`=`运算符和`==`运算符。)::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-351">(Notice the distinction between the `=` operator and the `==` operator.) :::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]</span></span>
    <span data-ttu-id="016e3-352">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-352">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-353">::: 行:::::: 列::: `!=` ::: 列端:::::: 列::: 是否不相等。</span><span class="sxs-lookup"><span data-stu-id="016e3-353">:::row::: :::column::: `!=` :::column-end::: :::column::: Inequality.</span></span> <span data-ttu-id="016e3-354">返回`true`如果值不相等。</span><span class="sxs-lookup"><span data-stu-id="016e3-354">Returns `true` if the values are not equal.</span></span>
<span data-ttu-id="016e3-355">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-355">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]</span></span>
    <span data-ttu-id="016e3-356">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-356">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-357">::: 行:::::: 列::: `< > <= >=` ::: 列端:::::: 列::: 较少-号、 大于-比小于-或-等于和大于或等于。</span><span class="sxs-lookup"><span data-stu-id="016e3-357">:::row::: :::column::: `< > <= >=` :::column-end::: :::column::: Less-than, greater-than, less-than-or-equal, and greater-than-or-equal.</span></span>
<span data-ttu-id="016e3-358">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-358">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]</span></span>
    <span data-ttu-id="016e3-359">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-359">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-360">::: 行:::::: 列::: `+` ::: 列端:::::: 列::: 串联，用来联接字符串。</span><span class="sxs-lookup"><span data-stu-id="016e3-360">:::row::: :::column::: `+` :::column-end::: :::column::: Concatenation, which is used to join strings.</span></span> <span data-ttu-id="016e3-361">ASP.NET 就会知道此运算符和加法运算符基于表达式的数据类型之间的差异。</span><span class="sxs-lookup"><span data-stu-id="016e3-361">ASP.NET knows the difference between this operator and the addition operator based on the data type of the expression.</span></span>
<span data-ttu-id="016e3-362">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-362">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]</span></span>
    <span data-ttu-id="016e3-363">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-363">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-364">::: 行:::::: 列::: `+=` `-=` ::: 列端:::::: 列::: 递增和递减运算符，从而添加，并且从变量 （分别） 减去 1。</span><span class="sxs-lookup"><span data-stu-id="016e3-364">:::row::: :::column::: `+=` `-=` :::column-end::: :::column::: The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
<span data-ttu-id="016e3-365">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-365">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]</span></span>
    <span data-ttu-id="016e3-366">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-366">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-367">::: 行:::::: 列::: `.` ::: 列端:::::: 列::: 点。</span><span class="sxs-lookup"><span data-stu-id="016e3-367">:::row::: :::column::: `.` :::column-end::: :::column::: Dot.</span></span> <span data-ttu-id="016e3-368">用于区分对象及其属性和方法。</span><span class="sxs-lookup"><span data-stu-id="016e3-368">Used to distinguish objects and their properties and methods.</span></span>
<span data-ttu-id="016e3-369">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-369">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]</span></span>
    <span data-ttu-id="016e3-370">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-370">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-371">::: 行:::::: 列::: `()` ::: 列端:::::: 列::: 括号。</span><span class="sxs-lookup"><span data-stu-id="016e3-371">:::row::: :::column::: `()` :::column-end::: :::column::: Parentheses.</span></span> <span data-ttu-id="016e3-372">用于到组表达式并将参数传递给方法。</span><span class="sxs-lookup"><span data-stu-id="016e3-372">Used to group expressions and to pass parameters to methods.</span></span>
<span data-ttu-id="016e3-373">::: 列端:::::: 列::: [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]</span><span class="sxs-lookup"><span data-stu-id="016e3-373">:::column-end::: :::column::: [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]</span></span>
    <span data-ttu-id="016e3-374">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-374">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-375">::: 行:::::: 列::: `[]` ::: 列端:::::: 列::: 方括号。</span><span class="sxs-lookup"><span data-stu-id="016e3-375">:::row::: :::column::: `[]` :::column-end::: :::column::: Brackets.</span></span> <span data-ttu-id="016e3-376">用于访问数组或集合中的值。</span><span class="sxs-lookup"><span data-stu-id="016e3-376">Used for accessing values in arrays or collections.</span></span>
<span data-ttu-id="016e3-377">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-377">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]</span></span>
    <span data-ttu-id="016e3-378">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-378">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-379">::: 行:::::: 列::: `!` ::: 列端:::::: 列::: 不。</span><span class="sxs-lookup"><span data-stu-id="016e3-379">:::row::: :::column::: `!` :::column-end::: :::column::: Not.</span></span> <span data-ttu-id="016e3-380">反转`true`值赋给`false`，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="016e3-380">Reverses a `true` value to `false` and vice versa.</span></span> <span data-ttu-id="016e3-381">通常用作要测试的速记方法`false`(即，为不`true`)。</span><span class="sxs-lookup"><span data-stu-id="016e3-381">Typically used as a shorthand way to test for `false` (that is, for not `true`).</span></span>
<span data-ttu-id="016e3-382">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-382">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]</span></span>
    <span data-ttu-id="016e3-383">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-383">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="016e3-384">::: 行:::::: 列::: `&&` <code>&#124;&#124;</code> ::: 列端:::::: 列::: 逻辑和也用于链接条件组合在一起。</span><span class="sxs-lookup"><span data-stu-id="016e3-384">:::row::: :::column::: `&&` <code>&#124;&#124;</code> :::column-end::: :::column::: Logical AND and OR, which are used to link conditions together.</span></span>
<span data-ttu-id="016e3-385">::: 列端:::::: 列::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]</span><span class="sxs-lookup"><span data-stu-id="016e3-385">:::column-end::: :::column::: [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]</span></span>
    <span data-ttu-id="016e3-386">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="016e3-386">:::column-end::: :::row-end:::</span></span>

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="016e3-387">使用文件和代码中的文件夹路径</span><span class="sxs-lookup"><span data-stu-id="016e3-387">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="016e3-388">将在代码中经常处理的文件和文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="016e3-388">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="016e3-389">可能显示的开发计算机上，下面是一个网站的物理文件夹结构的示例：</span><span class="sxs-lookup"><span data-stu-id="016e3-389">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="016e3-390">下面是一些有关 Url 和路径的基本详细信息：</span><span class="sxs-lookup"><span data-stu-id="016e3-390">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="016e3-391">URL 开头的域名 (`http://www.example.com`) 或服务器名称 (`http://localhost`， `http://mycomputer`)。</span><span class="sxs-lookup"><span data-stu-id="016e3-391">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="016e3-392">URL 对应于主机计算机上的物理路径。</span><span class="sxs-lookup"><span data-stu-id="016e3-392">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="016e3-393">例如，`http://myserver`可能对应于文件夹*C:\websites\mywebsite*服务器上。</span><span class="sxs-lookup"><span data-stu-id="016e3-393">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="016e3-394">虚拟路径是简写形式来表示在代码中的路径，而无需指定完整路径。</span><span class="sxs-lookup"><span data-stu-id="016e3-394">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="016e3-395">它包含后面的域或服务器名称的 URL 的部分。</span><span class="sxs-lookup"><span data-stu-id="016e3-395">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="016e3-396">当你使用虚拟路径时，可以无需更新的路径，将代码移动到不同的域或服务器。</span><span class="sxs-lookup"><span data-stu-id="016e3-396">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="016e3-397">此处是一个示例来帮助你了解的差异：</span><span class="sxs-lookup"><span data-stu-id="016e3-397">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="016e3-398">完整的 URL</span><span class="sxs-lookup"><span data-stu-id="016e3-398">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="016e3-399">服务器名称</span><span class="sxs-lookup"><span data-stu-id="016e3-399">Server name</span></span> | <span data-ttu-id="016e3-400">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="016e3-400">*mycompanyserver*</span></span> |
| <span data-ttu-id="016e3-401">虚拟路径</span><span class="sxs-lookup"><span data-stu-id="016e3-401">Virtual path</span></span> | <span data-ttu-id="016e3-402">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="016e3-402">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="016e3-403">物理路径</span><span class="sxs-lookup"><span data-stu-id="016e3-403">Physical path</span></span> | <span data-ttu-id="016e3-404">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="016e3-404">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="016e3-405">虚拟根目录为 /，驱动器是一样的 c： 根目录 \。</span><span class="sxs-lookup"><span data-stu-id="016e3-405">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="016e3-406">（虚拟文件夹路径始终使用正斜杠。）文件夹的虚拟路径不需要作为物理文件夹; 具有相同的名称它可以是一个别名。</span><span class="sxs-lookup"><span data-stu-id="016e3-406">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="016e3-407">（生产服务器上的虚拟路径很少的匹配确切的物理路径。）</span><span class="sxs-lookup"><span data-stu-id="016e3-407">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="016e3-408">当代码中的文件和文件夹时，有时你需要引用的物理路径和有时虚拟路径，具体取决于你正在使用哪些对象。</span><span class="sxs-lookup"><span data-stu-id="016e3-408">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="016e3-409">ASP.NET 为你提供这些工具用于处理在代码中的文件和文件夹路径：`Server.MapPath`方法，与`~`运算符和`Href`方法。</span><span class="sxs-lookup"><span data-stu-id="016e3-409">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="016e3-410">转换虚拟与物理路径： Server.MapPath 方法</span><span class="sxs-lookup"><span data-stu-id="016e3-410">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="016e3-411">`Server.MapPath`方法将转换的虚拟路径 (如 */default.cshtml*) 为绝对物理路径 (如*C:\WebSites\MyWebSiteFolder\default.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="016e3-411">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="016e3-412">需要完整的物理路径时使用此方法。</span><span class="sxs-lookup"><span data-stu-id="016e3-412">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="016e3-413">一个典型示例是要读取或写入文本文件或 web 服务器上的图像文件时。</span><span class="sxs-lookup"><span data-stu-id="016e3-413">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="016e3-414">你通常不知道你的站点托管站点的服务器上的绝对物理路径，因此此方法可以将路径转换你知道-的虚拟路径-到你的服务器上的相应路径。</span><span class="sxs-lookup"><span data-stu-id="016e3-414">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="016e3-415">将虚拟路径传递给文件或文件夹的方法，并返回物理路径：</span><span class="sxs-lookup"><span data-stu-id="016e3-415">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="016e3-416">引用的虚拟根： ~ 运算符和 Href 方法</span><span class="sxs-lookup"><span data-stu-id="016e3-416">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="016e3-417">在 *.cshtml*或 *.vbhtml*文件，你可以引用虚拟根路径使用`~`运算符。</span><span class="sxs-lookup"><span data-stu-id="016e3-417">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="016e3-418">这是非常方便，因为您可以来回移动网页，在站点中，并且它们包含至其他页面的任何链接不会被破坏。</span><span class="sxs-lookup"><span data-stu-id="016e3-418">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="016e3-419">也很方便以防曾经将你的网站移动到其他位置。</span><span class="sxs-lookup"><span data-stu-id="016e3-419">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="016e3-420">下面是一些可能的恶意活动：</span><span class="sxs-lookup"><span data-stu-id="016e3-420">Here are some examples:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

<span data-ttu-id="016e3-421">如果网站`http://myserver/myapp`，下面是运行页面时 ASP.NET 将这些路径的方式：</span><span class="sxs-lookup"><span data-stu-id="016e3-421">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="016e3-422">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="016e3-422">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="016e3-423">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="016e3-423">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="016e3-424">（你实际上不会看到这些路径的值的变量，但 ASP.NET 将则将路径视为即它们是一样。）</span><span class="sxs-lookup"><span data-stu-id="016e3-424">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="016e3-425">你可以使用`~`运算符在 （如上所述） 的服务器代码和在标记中，如下：</span><span class="sxs-lookup"><span data-stu-id="016e3-425">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

<span data-ttu-id="016e3-426">在标记中，你使用`~`运算符来创建资源，如图像文件、 其他网页和 CSS 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="016e3-426">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="016e3-427">ASP.NET 页运行时，（代码和标记） 页中查找和解析所有`~`与相应路径的引用。</span><span class="sxs-lookup"><span data-stu-id="016e3-427">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="016e3-428">条件逻辑，并循环</span><span class="sxs-lookup"><span data-stu-id="016e3-428">Conditional Logic and Loops</span></span>

<span data-ttu-id="016e3-429">ASP.NET 服务器代码允许你执行基于条件的任务，编写特定次数的重复语句的代码 （即运行一个循环中的代码）。</span><span class="sxs-lookup"><span data-stu-id="016e3-429">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times (that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="016e3-430">测试条件</span><span class="sxs-lookup"><span data-stu-id="016e3-430">Testing Conditions</span></span>

<span data-ttu-id="016e3-431">你使用对简单条件进行测试`if`语句，返回 true 或 false 基于你指定的测试：</span><span class="sxs-lookup"><span data-stu-id="016e3-431">To test a simple condition you use the `if` statement, which returns true or false based on a test you specify:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

<span data-ttu-id="016e3-432">`if`关键字开始块。</span><span class="sxs-lookup"><span data-stu-id="016e3-432">The `if` keyword starts a block.</span></span> <span data-ttu-id="016e3-433">实际的测试 （条件） 位于括号中，并返回 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="016e3-433">The actual test (condition) is in parentheses and returns true or false.</span></span> <span data-ttu-id="016e3-434">运行测试为 true 的语句括在大括号中。</span><span class="sxs-lookup"><span data-stu-id="016e3-434">The statements that run if the test is true are enclosed in braces.</span></span> <span data-ttu-id="016e3-435">`if`语句可以包含`else`指定语句在条件为 false 时要运行的块：</span><span class="sxs-lookup"><span data-stu-id="016e3-435">An `if` statement can include an `else` block that specifies statements to run if the condition is false:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

<span data-ttu-id="016e3-436">你可以添加多个条件使用`else if`块：</span><span class="sxs-lookup"><span data-stu-id="016e3-436">You can add multiple conditions using an `else if` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

<span data-ttu-id="016e3-437">在此示例中，如果第一个条件在 if 块不为 true，`else if`才会检查条件。</span><span class="sxs-lookup"><span data-stu-id="016e3-437">In this example, if the first condition in the if block is not true, the `else if` condition is checked.</span></span> <span data-ttu-id="016e3-438">如果满足该条件，则中的语句`else if`块执行。</span><span class="sxs-lookup"><span data-stu-id="016e3-438">If that condition is met, the statements in the `else if` block are executed.</span></span> <span data-ttu-id="016e3-439">如果不符合任何条件中的语句`else`块执行。</span><span class="sxs-lookup"><span data-stu-id="016e3-439">If none of the conditions are met, the statements in the `else` block are executed.</span></span> <span data-ttu-id="016e3-440">你可以添加任意数量的 else if 块，并与然后关闭`else`作为阻止&quot;其他一切&quot;条件。</span><span class="sxs-lookup"><span data-stu-id="016e3-440">You can add any number of else if blocks, and then close with an `else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="016e3-441">若要测试大量的条件，使用`switch`块：</span><span class="sxs-lookup"><span data-stu-id="016e3-441">To test a large number of conditions, use a `switch` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

<span data-ttu-id="016e3-442">要测试的值位于括号中 (在示例中，`weekday`变量)。</span><span class="sxs-lookup"><span data-stu-id="016e3-442">The value to test is in parentheses (in the example, the `weekday` variable).</span></span> <span data-ttu-id="016e3-443">每个单独测试使用`case`结尾冒号 （:） 语句。</span><span class="sxs-lookup"><span data-stu-id="016e3-443">Each individual test uses a `case` statement that ends with a colon (:).</span></span> <span data-ttu-id="016e3-444">如果值`case`语句与匹配的测试的值，在执行中该事例的块的代码。</span><span class="sxs-lookup"><span data-stu-id="016e3-444">If the value of a `case` statement matches the test value, the code in that case block is executed.</span></span> <span data-ttu-id="016e3-445">关闭与每个 case 语句`break`语句。</span><span class="sxs-lookup"><span data-stu-id="016e3-445">You close each case statement with a `break` statement.</span></span> <span data-ttu-id="016e3-446">(如果你忘记了要包括在每个中断`case`阻止，请从下一个代码`case`语句还将运行。)A`switch`块通常有`default`语句的最后一种情况作为&quot;其他一切&quot;运行任何其他情况下是否的选项。</span><span class="sxs-lookup"><span data-stu-id="016e3-446">(If you forget to include break in each `case` block, the code from the next `case` statement will run also.) A `switch` block often has a `default` statement as the last case for an &quot;everything else&quot; option that runs if none of the other cases are true.</span></span>

<span data-ttu-id="016e3-447">在浏览器中显示的最后两个条件块的结果：</span><span class="sxs-lookup"><span data-stu-id="016e3-447">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="016e3-449">循环的代码</span><span class="sxs-lookup"><span data-stu-id="016e3-449">Looping Code</span></span>

<span data-ttu-id="016e3-450">你经常需要重复运行相同的语句。</span><span class="sxs-lookup"><span data-stu-id="016e3-450">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="016e3-451">通过循环执行此操作。</span><span class="sxs-lookup"><span data-stu-id="016e3-451">You do this by looping.</span></span> <span data-ttu-id="016e3-452">例如，你通常运行的相同语句的每个项集合中的数据。</span><span class="sxs-lookup"><span data-stu-id="016e3-452">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="016e3-453">如果你知道完全多少次想要循环，则可以使用`for`循环。</span><span class="sxs-lookup"><span data-stu-id="016e3-453">If you know exactly how many times you want to loop, you can use a `for` loop.</span></span> <span data-ttu-id="016e3-454">这种类型是循环的的向上计数或倒计时特别有用：</span><span class="sxs-lookup"><span data-stu-id="016e3-454">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

<span data-ttu-id="016e3-455">循环开头`for`每个以分号结尾的关键字后, 跟置于括号内，三个语句。</span><span class="sxs-lookup"><span data-stu-id="016e3-455">The loop begins with the `for` keyword, followed by three statements in parentheses, each terminated with a semicolon.</span></span>

- <span data-ttu-id="016e3-456">在括号内的第一个语句 (`var i=10;`) 创建一个计数器并将初始化为 10。</span><span class="sxs-lookup"><span data-stu-id="016e3-456">Inside the parentheses, the first statement (`var i=10;`) creates a counter and initializes it to 10.</span></span> <span data-ttu-id="016e3-457">你不需要命名该计数器`i`&#8212;你可以使用任何变量。</span><span class="sxs-lookup"><span data-stu-id="016e3-457">You don't have to name the counter `i` &#8212; you can use any variable.</span></span> <span data-ttu-id="016e3-458">当`for`循环运行时，此计数器时自动递增。</span><span class="sxs-lookup"><span data-stu-id="016e3-458">When the `for` loop runs, the counter is automatically incremented.</span></span>
- <span data-ttu-id="016e3-459">第二个语句 (`i < 21;`) 设置为你想要计数的距离的条件。</span><span class="sxs-lookup"><span data-stu-id="016e3-459">The second statement (`i < 21;`) sets the condition for how far you want to count.</span></span> <span data-ttu-id="016e3-460">在这种情况下，您希望其转到最多 20 个 （即，继续阅读计数器时小于 21）。</span><span class="sxs-lookup"><span data-stu-id="016e3-460">In this case, you want it to go to a maximum of 20 (that is, keep going while the counter is less than 21).</span></span>
- <span data-ttu-id="016e3-461">第三个语句 (`i++` ) 使用一个递增运算符，它只需指定计数器应具有 1 添加到其每次循环运行的时。</span><span class="sxs-lookup"><span data-stu-id="016e3-461">The third statement (`i++` ) uses an increment operator, which simply specifies that the counter should have 1 added to it each time the loop runs.</span></span>

<span data-ttu-id="016e3-462">在括号内是循环的将每个迭代中运行的代码。</span><span class="sxs-lookup"><span data-stu-id="016e3-462">Inside the braces is the code that will run for each iteration of the loop.</span></span> <span data-ttu-id="016e3-463">标记将创建一个新段落 (`<p>`元素) 每个时间，并将行添加到输出中，显示的值`i`（计数器）。</span><span class="sxs-lookup"><span data-stu-id="016e3-463">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of `i` (the counter).</span></span> <span data-ttu-id="016e3-464">运行此页时，该示例将创建 11 行显示输出，与每个行，该值指示项数中的文本。</span><span class="sxs-lookup"><span data-stu-id="016e3-464">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

<span data-ttu-id="016e3-466">如果你正在使用集合或数组，则通常会使用`foreach`循环。</span><span class="sxs-lookup"><span data-stu-id="016e3-466">If you're working with a collection or array, you often use a `foreach` loop.</span></span> <span data-ttu-id="016e3-467">集合是一组类似对象和`foreach`循环的允许您执行的任务集合中的每个项。</span><span class="sxs-lookup"><span data-stu-id="016e3-467">A collection is a group of similar objects, and the `foreach` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="016e3-468">这种类型的循环是方便对于集合，因为与不同`for`循环中，你无需递增计数器或设置一个限制。</span><span class="sxs-lookup"><span data-stu-id="016e3-468">This type of loop is convenient for collections, because unlike a `for` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="016e3-469">相反，`foreach`循环代码只需继续访问该集合之前完成。</span><span class="sxs-lookup"><span data-stu-id="016e3-469">Instead, the `foreach` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="016e3-470">例如，以下代码将返回中的项`Request.ServerVariables`集合，这是一个对象，包含有关你的 web 服务器的信息。</span><span class="sxs-lookup"><span data-stu-id="016e3-470">For example, the following code returns the items in the `Request.ServerVariables` collection, which is an object that contains information about your web server.</span></span> <span data-ttu-id="016e3-471">它使用`foreac`h 循环，以显示每个项的名称，通过创建新`<li>`HTML 项目符号列表中的元素。</span><span class="sxs-lookup"><span data-stu-id="016e3-471">It uses a `foreac` h loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

<span data-ttu-id="016e3-472">`foreach`关键字后跟圆括号其中声明表示单个项集合中的变量 (在示例中， `var item`) 后, 跟`in`关键字后, 跟你想要循环访问的集合。</span><span class="sxs-lookup"><span data-stu-id="016e3-472">The `foreach` keyword is followed by parentheses where you declare a variable that represents a single item in the collection (in the example, `var item`), followed by the `in` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="016e3-473">正文中`foreach`循环中，你可以访问使用你之前声明的变量的当前项。</span><span class="sxs-lookup"><span data-stu-id="016e3-473">In the body of the `foreach` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

<span data-ttu-id="016e3-475">若要创建更通用的循环，使用`while`语句：</span><span class="sxs-lookup"><span data-stu-id="016e3-475">To create a more general-purpose loop, use the `while` statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

<span data-ttu-id="016e3-476">A`while`循环开头`while`关键字后, 跟括号你在其中指定循环继续的多长时间 (在此处，供，只要`countNum`小于 50)，然后用于重复的块。</span><span class="sxs-lookup"><span data-stu-id="016e3-476">A `while` loop begins with the `while` keyword, followed by parentheses where you specify how long the loop continues (here, for as long as `countNum` is less than 50), then the block to repeat.</span></span> <span data-ttu-id="016e3-477">循环通常递增 （添加） 或递减 （从减） 变量或用于计数的对象。</span><span class="sxs-lookup"><span data-stu-id="016e3-477">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="016e3-478">在示例中，`+=`运算符将添加到 1`countNum`每次循环运行的时。</span><span class="sxs-lookup"><span data-stu-id="016e3-478">In the example, the `+=` operator adds 1 to `countNum` each time the loop runs.</span></span> <span data-ttu-id="016e3-479">(要递减进行倒计时的循环中的变量，你可以使用递减运算符`-=`)。</span><span class="sxs-lookup"><span data-stu-id="016e3-479">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`).</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="016e3-480">对象和集合</span><span class="sxs-lookup"><span data-stu-id="016e3-480">Objects and Collections</span></span>

<span data-ttu-id="016e3-481">在 ASP.NET 网站中几乎所有操作是一个对象，包括 web 页本身。</span><span class="sxs-lookup"><span data-stu-id="016e3-481">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="016e3-482">本部分讨论一些重要的对象，你将经常你在代码中使用。</span><span class="sxs-lookup"><span data-stu-id="016e3-482">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="016e3-483">Page 对象</span><span class="sxs-lookup"><span data-stu-id="016e3-483">Page Objects</span></span>

<span data-ttu-id="016e3-484">在 ASP.NET 中的最基本对象是的页。</span><span class="sxs-lookup"><span data-stu-id="016e3-484">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="016e3-485">你可以访问的直接不带任何合格的对象的页对象的属性。</span><span class="sxs-lookup"><span data-stu-id="016e3-485">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="016e3-486">以下代码将获取该页面的文件路径，使用`Request`页的对象：</span><span class="sxs-lookup"><span data-stu-id="016e3-486">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

<span data-ttu-id="016e3-487">为了更加明确要引用属性和当前的页对象上的方法，你可以选择使用关键字`this`来表示你的代码中的页对象。</span><span class="sxs-lookup"><span data-stu-id="016e3-487">To make it clear that you're referencing properties and methods on the current page object, you can optionally use the keyword `this` to represent the page object in your code.</span></span> <span data-ttu-id="016e3-488">下面是与前面的代码示例，`this`添加以表示页：</span><span class="sxs-lookup"><span data-stu-id="016e3-488">Here is the previous code example, with `this` added to represent the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

<span data-ttu-id="016e3-489">你可以使用属性的`Page`对象以获取大量的信息，如：</span><span class="sxs-lookup"><span data-stu-id="016e3-489">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="016e3-490">`Request`。</span><span class="sxs-lookup"><span data-stu-id="016e3-490">`Request`.</span></span> <span data-ttu-id="016e3-491">如你已经了解，这是信息的有关当前请求，包括哪种类型的浏览器发出了请求、 页面、 用户标识，等等的 URL 的集合。</span><span class="sxs-lookup"><span data-stu-id="016e3-491">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="016e3-492">`Response`。</span><span class="sxs-lookup"><span data-stu-id="016e3-492">`Response`.</span></span> <span data-ttu-id="016e3-493">这是信息的有关将发送到浏览器中，当服务器代码程序完成运行响应 （页） 的集合。</span><span class="sxs-lookup"><span data-stu-id="016e3-493">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="016e3-494">例如，此属性可用于将信息写入到响应中。</span><span class="sxs-lookup"><span data-stu-id="016e3-494">For example, you can use this property to write information into the response.</span></span> 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="016e3-495">（数组和字典） 的集合对象</span><span class="sxs-lookup"><span data-stu-id="016e3-495">Collection Objects (Arrays and Dictionaries)</span></span>

<span data-ttu-id="016e3-496">A*集合*是一组相同的类型，例如的集合对象`Customer`数据库中的对象。</span><span class="sxs-lookup"><span data-stu-id="016e3-496">A *collection* is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="016e3-497">ASP.NET 包含多个内置集合，如`Request.Files`集合。</span><span class="sxs-lookup"><span data-stu-id="016e3-497">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="016e3-498">通常，你将使用集合中的数据。</span><span class="sxs-lookup"><span data-stu-id="016e3-498">You'll often work with data in collections.</span></span> <span data-ttu-id="016e3-499">两个常见集合类型是*数组*和*字典*。</span><span class="sxs-lookup"><span data-stu-id="016e3-499">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="016e3-500">如果你想要存储的相似的项目集合，但不想创建一个单独的变量以保存每个项，则数组非常有用：</span><span class="sxs-lookup"><span data-stu-id="016e3-500">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

<span data-ttu-id="016e3-501">数组，可声明特定的数据类型，如`string`， `int`，或`DateTime`。</span><span class="sxs-lookup"><span data-stu-id="016e3-501">With arrays, you declare a specific data type, such as `string`, `int`, or `DateTime`.</span></span> <span data-ttu-id="016e3-502">要指明变量可以包含一个数组，可将括号添加到声明 (如`string[]`或`int[]`)。</span><span class="sxs-lookup"><span data-stu-id="016e3-502">To indicate that the variable can contain an array, you add brackets to the declaration (such as `string[]` or `int[]`).</span></span> <span data-ttu-id="016e3-503">你可以访问项数组使用它们的位置 （索引） 中或通过使用`foreach`语句。</span><span class="sxs-lookup"><span data-stu-id="016e3-503">You can access items in an array using their position (index) or by using the `foreach` statement.</span></span> <span data-ttu-id="016e3-504">数组索引是从零开始&#8212;，即第一项是在位置 0，第二项是在位置 1，依此类推。</span><span class="sxs-lookup"><span data-stu-id="016e3-504">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

<span data-ttu-id="016e3-505">你可以通过获取确定数组中的项的数目及其`Length`属性。</span><span class="sxs-lookup"><span data-stu-id="016e3-505">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="016e3-506">若要获取特定项 （要搜索数组） 的数组中的位置，请使用`Array.IndexOf`方法。</span><span class="sxs-lookup"><span data-stu-id="016e3-506">To get the position of a specific item in the array (to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="016e3-507">你还可以执行诸如反向数组的内容 (`Array.Reverse`方法) 或对内容进行排序 (`Array.Sort`方法)。</span><span class="sxs-lookup"><span data-stu-id="016e3-507">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="016e3-508">在浏览器中显示的字符串数组代码的输出：</span><span class="sxs-lookup"><span data-stu-id="016e3-508">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

<span data-ttu-id="016e3-510">字典是键/值对的集合，其中提供的密钥 （或名称） 来设置或检索相应的值：</span><span class="sxs-lookup"><span data-stu-id="016e3-510">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

<span data-ttu-id="016e3-511">若要创建一个字典，请使用`new`关键字以指示你要创建新的字典对象。</span><span class="sxs-lookup"><span data-stu-id="016e3-511">To create a dictionary, you use the `new` keyword to indicate that you're creating a new dictionary object.</span></span> <span data-ttu-id="016e3-512">你可以将字典分配给变量的使用`var`关键字。</span><span class="sxs-lookup"><span data-stu-id="016e3-512">You can assign a dictionary to a variable using the `var` keyword.</span></span> <span data-ttu-id="016e3-513">指示在使用命令的尖括号字典中的项的数据类型 ( `< >` )。</span><span class="sxs-lookup"><span data-stu-id="016e3-513">You indicate the data types of the items in the dictionary using angle brackets ( `< >` ).</span></span> <span data-ttu-id="016e3-514">在声明结束时，你必须添加一对括号，因为这是实际创建一个新的字典的方法。</span><span class="sxs-lookup"><span data-stu-id="016e3-514">At the end of the declaration, you must add a pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="016e3-515">若要将项添加到字典中，你可以调用`Add`字典变量或方法 (`myScores`在这种情况下)，然后指定一个键和值。</span><span class="sxs-lookup"><span data-stu-id="016e3-515">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="016e3-516">或者，可以使用方括号来指示键并执行简单的赋值，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="016e3-516">Alternatively, you can use square brackets to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

<span data-ttu-id="016e3-517">若要从字典中获取一个值，请在括号中指定的密钥：</span><span class="sxs-lookup"><span data-stu-id="016e3-517">To get a value from the dictionary, you specify the key in brackets:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="016e3-518">调用带参数的方法</span><span class="sxs-lookup"><span data-stu-id="016e3-518">Calling Methods with Parameters</span></span>

<span data-ttu-id="016e3-519">阅读本文前面时，与程序的对象可以具有方法。</span><span class="sxs-lookup"><span data-stu-id="016e3-519">As you read earlier in this article, the objects that you program with can have methods.</span></span> <span data-ttu-id="016e3-520">例如，`Database`对象可能具有`Database.Connect`方法。</span><span class="sxs-lookup"><span data-stu-id="016e3-520">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="016e3-521">许多方法还具有一个或多个参数。</span><span class="sxs-lookup"><span data-stu-id="016e3-521">Many methods also have one or more parameters.</span></span> <span data-ttu-id="016e3-522">A*参数*是向某个方法传递的值以使该方法以完成其任务。</span><span class="sxs-lookup"><span data-stu-id="016e3-522">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="016e3-523">例如，查看有关声明`Request.MapPath`方法，采用三个参数：</span><span class="sxs-lookup"><span data-stu-id="016e3-523">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

<span data-ttu-id="016e3-524">（已换行以使其更具可读性。</span><span class="sxs-lookup"><span data-stu-id="016e3-524">(The line has been wrapped to make it more readable.</span></span> <span data-ttu-id="016e3-525">请记住，你可以插入的换行符几乎任何位置使用但内部字符串用引号引起来。)</span><span class="sxs-lookup"><span data-stu-id="016e3-525">Remember that you can put line breaks almost any place except inside strings that are enclosed in quotation marks.)</span></span>

<span data-ttu-id="016e3-526">此方法对应的服务器上的物理路径返回到指定的虚拟路径。</span><span class="sxs-lookup"><span data-stu-id="016e3-526">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="016e3-527">该方法的三个参数`virtualPath`， `baseVirtualDir`，和`allowCrossAppMapping`。</span><span class="sxs-lookup"><span data-stu-id="016e3-527">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="016e3-528">（请注意，在声明中，列出了参数将接受的数据的数据类型）。在调用此方法时，你必须提供所有三个参数的值。</span><span class="sxs-lookup"><span data-stu-id="016e3-528">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="016e3-529">Razor 语法为你提供了用于将参数传递给方法的两个选项：*位置参数*和*命名参数*。</span><span class="sxs-lookup"><span data-stu-id="016e3-529">The Razor syntax gives you two options for passing parameters to a method: *positional parameters* and *named parameters*.</span></span> <span data-ttu-id="016e3-530">若要调用的使用位置参数的方法，请在方法声明中指定严格顺序传递参数。</span><span class="sxs-lookup"><span data-stu-id="016e3-530">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="016e3-531">（你将通常知道此顺序通过阅读的方法的文档。）你必须遵循的顺序，并且你不能跳过任何参数&#8212;如果有必要，你将传递一个空字符串 (`""`) 或`null`为不具有的值的位置参数。</span><span class="sxs-lookup"><span data-stu-id="016e3-531">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or `null` for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="016e3-532">下面的示例假定你有一个名为的文件夹*脚本*在网站上。</span><span class="sxs-lookup"><span data-stu-id="016e3-532">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="016e3-533">该代码调用`Request.MapPath`方法并传递正确的顺序中的三个参数的值。</span><span class="sxs-lookup"><span data-stu-id="016e3-533">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="016e3-534">然后，它将显示生成的映射的路径。</span><span class="sxs-lookup"><span data-stu-id="016e3-534">It then displays the resulting mapped path.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

<span data-ttu-id="016e3-535">当一个方法具有多个参数时，您可以保留你的代码更具可读性使用命名参数。</span><span class="sxs-lookup"><span data-stu-id="016e3-535">When a method has many parameters, you can keep your code more readable by using named parameters.</span></span> <span data-ttu-id="016e3-536">若要调用的方法使用命名的参数，你指定的参数名称后跟一个冒号 （:），然后选择值。</span><span class="sxs-lookup"><span data-stu-id="016e3-536">To call a method using named parameters, you specify the parameter name followed by a colon (:), and then the value.</span></span> <span data-ttu-id="016e3-537">命名参数的优点是，你可以将它们传递你希望任何顺序。</span><span class="sxs-lookup"><span data-stu-id="016e3-537">The advantage of named parameters is that you can pass them in any order you want.</span></span> <span data-ttu-id="016e3-538">（一个缺点是方法调用不是为 compact。）</span><span class="sxs-lookup"><span data-stu-id="016e3-538">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="016e3-539">下面的示例调用按上面所述的相同方法，但使用命名参数提供的值：</span><span class="sxs-lookup"><span data-stu-id="016e3-539">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

<span data-ttu-id="016e3-540">如你所见，参数进行传递以不同的顺序。</span><span class="sxs-lookup"><span data-stu-id="016e3-540">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="016e3-541">但是，如果你运行前面的示例和此示例，它们将返回相同的值。</span><span class="sxs-lookup"><span data-stu-id="016e3-541">However, if you run the previous example and this example, they'll return the same value.</span></span>

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a><span data-ttu-id="016e3-542">处理错误</span><span class="sxs-lookup"><span data-stu-id="016e3-542">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="016e3-543">Try Catch 语句</span><span class="sxs-lookup"><span data-stu-id="016e3-543">Try-Catch Statements</span></span>

<span data-ttu-id="016e3-544">通常将在代码中可能会失败的原因，在你的控制范围具有语句。</span><span class="sxs-lookup"><span data-stu-id="016e3-544">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="016e3-545">例如：</span><span class="sxs-lookup"><span data-stu-id="016e3-545">For example:</span></span>

- <span data-ttu-id="016e3-546">如果你的代码尝试创建或访问文件，可能会出现各种类型的错误。</span><span class="sxs-lookup"><span data-stu-id="016e3-546">If your code tries to create or access a file, all sorts of errors might occur.</span></span> <span data-ttu-id="016e3-547">所需的文件可能不存在，则可能锁定，代码可能不具有权限，依次类推。</span><span class="sxs-lookup"><span data-stu-id="016e3-547">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="016e3-548">同样，如果你的代码尝试更新数据库中的记录，可以有权限问题、 与数据库的连接可能会丢弃，要保存的数据可能无效，依次类推。</span><span class="sxs-lookup"><span data-stu-id="016e3-548">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="016e3-549">编程术语中，这些情况下调用*异常*。</span><span class="sxs-lookup"><span data-stu-id="016e3-549">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="016e3-550">如果你的代码遇到的异常，它会生成 （引发） 一条错误消息的在最好的情况，令人讨厌的用户：</span><span class="sxs-lookup"><span data-stu-id="016e3-550">If your code encounters an exception, it generates (throws) an error message that's, at best, annoying to users:</span></span>

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

<span data-ttu-id="016e3-552">在情况下，你的代码可能会遇到的异常，并且为了避免这种类型的错误消息，你可以使用`try/catch`语句。</span><span class="sxs-lookup"><span data-stu-id="016e3-552">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `try/catch` statements.</span></span> <span data-ttu-id="016e3-553">在`try`语句，你将运行要检查的代码。</span><span class="sxs-lookup"><span data-stu-id="016e3-553">In the `try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="016e3-554">在一个或多个`catch`语句，则你可以查看为特定可能发生的错误 （特定类型的异常）。</span><span class="sxs-lookup"><span data-stu-id="016e3-554">In one or more `catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="016e3-555">可以包括任意多个`catch`语句作为你需要查找以及预期的错误。</span><span class="sxs-lookup"><span data-stu-id="016e3-555">You can include as many `catch` statements as you need to look for errors that you are anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="016e3-556">我们建议你避免使用`Response.Redirect`中的方法`try/catch`语句，因为它可以在页中导致异常。</span><span class="sxs-lookup"><span data-stu-id="016e3-556">We recommend that you avoid using the `Response.Redirect` method in `try/catch` statements, because it can cause an exception in your page.</span></span>


<span data-ttu-id="016e3-557">下面的示例演示创建第一个请求上的文本文件，然后显示一个按钮，使用户能够打开文件的页。</span><span class="sxs-lookup"><span data-stu-id="016e3-557">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="016e3-558">该示例有意使用错误的文件名称，以便它会导致异常。</span><span class="sxs-lookup"><span data-stu-id="016e3-558">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="016e3-559">代码包含`catch`两个可能的异常的语句： `FileNotFoundException`，就会出现此错误，文件名称是否和`DirectoryNotFoundException`，如果 ASP.NET 甚至找不到文件夹时会出现此情况。</span><span class="sxs-lookup"><span data-stu-id="016e3-559">The code includes `catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="016e3-560">（你可以取消注释在示例中的语句才能看到它时一切运行正常的运行。）</span><span class="sxs-lookup"><span data-stu-id="016e3-560">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="016e3-561">如果你的代码未处理异常，你会看到一个错误页面，如前面的屏幕快照。</span><span class="sxs-lookup"><span data-stu-id="016e3-561">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="016e3-562">但是，`try/catch`部分可帮助防止用户看到这些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="016e3-562">However, the `try/catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="016e3-563">其他资源</span><span class="sxs-lookup"><span data-stu-id="016e3-563">Additional Resources</span></span>

<span data-ttu-id="016e3-564">**使用 Visual Basic 编程**</span><span class="sxs-lookup"><span data-stu-id="016e3-564">**Programming with Visual Basic**</span></span>


[<span data-ttu-id="016e3-565">附录： Visual Basic 语言和语法</span><span class="sxs-lookup"><span data-stu-id="016e3-565">Appendix: Visual Basic Language and Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkId=202908)


<span data-ttu-id="016e3-566">**参考文档**</span><span class="sxs-lookup"><span data-stu-id="016e3-566">**Reference Documentation**</span></span>


[<span data-ttu-id="016e3-567">ASP.NET 2.0</span><span class="sxs-lookup"><span data-stu-id="016e3-567">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)

[<span data-ttu-id="016e3-568">C# 语言</span><span class="sxs-lookup"><span data-stu-id="016e3-568">C# Language</span></span>](https://msdn.microsoft.com/library/kx37x362.aspx)
