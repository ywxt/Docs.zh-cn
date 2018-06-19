---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: 使用 Razor 语法 (Visual Basic) 的 ASP.NET Web 编程简介 |Microsoft 文档
author: tfitzmac
description: 本附录可与 ASP.NET 网页编程的概述在 Visual Basic 中，使用 Razor 语法。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/07/2014
ms.topic: article
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: aad951a0e4344dbaafbdcc3b3980307a26fa75fc
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
ms.locfileid: "31483479"
---
<a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="834f7-103">使用 Razor 语法 (Visual Basic) 的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="834f7-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>
====================
<span data-ttu-id="834f7-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="834f7-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="834f7-105">本文概述你的编程与 ASP.NET Web Pages 使用 Razor 语法和 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="834f7-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="834f7-106">ASP.NET 是用于在 web 服务器上运行动态 web 页的 Microsoft 的技术。</span><span class="sxs-lookup"><span data-stu-id="834f7-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="834f7-107">**你将了解**:</span><span class="sxs-lookup"><span data-stu-id="834f7-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="834f7-108">编程提示的入门知识编程使用 Razor 语法的 ASP.NET Web Pages 顶部 8。</span><span class="sxs-lookup"><span data-stu-id="834f7-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="834f7-109">你将需要的基本编程概念。</span><span class="sxs-lookup"><span data-stu-id="834f7-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="834f7-110">哪些 ASP.NET 服务器代码和 Razor 语法与所有有关。</span><span class="sxs-lookup"><span data-stu-id="834f7-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="834f7-111">软件版本</span><span class="sxs-lookup"><span data-stu-id="834f7-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="834f7-112">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="834f7-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="834f7-113">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="834f7-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="834f7-114">使用 Razor 语法中使用的 ASP.NET Web Pages 的大多数示例使用 C#。</span><span class="sxs-lookup"><span data-stu-id="834f7-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="834f7-115">但 Razor 语法也支持 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="834f7-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="834f7-116">要编制 ASP.NET 网页在 Visual Basic 中，你创建一个包含网页 *.vbhtml*文件扩展名，然后添加 Visual Basic 代码。</span><span class="sxs-lookup"><span data-stu-id="834f7-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="834f7-117">本文提供使用 Visual Basic 语言和用于创建 ASP.NET 网页语法的概述。</span><span class="sxs-lookup"><span data-stu-id="834f7-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="834f7-118">Microsoft WebMatrix 的默认网站模板 (**面包店**，**照片库**，和**入门站点**等) 在 C# 和 Visual Basic 版本中可用。</span><span class="sxs-lookup"><span data-stu-id="834f7-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="834f7-119">你可以为 NuGet 包安装 Visual Basic 的模板。</span><span class="sxs-lookup"><span data-stu-id="834f7-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="834f7-120">名为的文件夹中的站点的根文件夹中安装的网站模板*Microsoft 模板*。</span><span class="sxs-lookup"><span data-stu-id="834f7-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>


## <a name="the-top-8-programming-tips"></a><span data-ttu-id="834f7-121">最重要的 8 编程提示</span><span class="sxs-lookup"><span data-stu-id="834f7-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="834f7-122">本部分列出绝对需要知道当你开始编写使用 Razor 语法的 ASP.NET 服务器代码的一些提示。</span><span class="sxs-lookup"><span data-stu-id="834f7-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="834f7-123">1.将代码添加到页使用 @ 字符</span><span class="sxs-lookup"><span data-stu-id="834f7-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="834f7-124">`@`字符开始内联表达式、 单语句块和多语句块：</span><span class="sxs-lookup"><span data-stu-id="834f7-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="834f7-125">在浏览器中所显示的结果：</span><span class="sxs-lookup"><span data-stu-id="834f7-125">The result displayed in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="834f7-127">**HTML 编码**</span><span class="sxs-lookup"><span data-stu-id="834f7-127">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="834f7-128">当你在页中使用显示内容`@`字符，如前面的示例中，ASP.NET 进行 HTML 编码输出。</span><span class="sxs-lookup"><span data-stu-id="834f7-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="834f7-129">这将替换保留的 HTML 字符 (如`<`和`>`和`&`) 与启用要显示为字符而不是被解释为 HTML 标记或实体的网页中的字符的代码。</span><span class="sxs-lookup"><span data-stu-id="834f7-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="834f7-130">HTML 编码，在服务器代码中的输出可能显示不正常，而无需无法公开安全风险的页。</span><span class="sxs-lookup"><span data-stu-id="834f7-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="834f7-131">如果你的目标是输出将标记呈现为标记的 HTML 标记 (例如`<p></p>`，段落或`<em></em>`强调文本)，请参阅明[组合文本、 标记和代码块中的代码](#BM_CombiningTextMarkupAndCode)本文后续部分中。</span><span class="sxs-lookup"><span data-stu-id="834f7-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="834f7-132">你可以阅读更多有关中的 HTML 编码[使用 ASP.NET Web Pages 站点中的 HTML 窗体](https://go.microsoft.com/fwlink/?LinkId=202892)。</span><span class="sxs-lookup"><span data-stu-id="834f7-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>


### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="834f7-133">2.你将包含代码的代码块...端代码</span><span class="sxs-lookup"><span data-stu-id="834f7-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="834f7-134">代码块包含一个或多个代码语句，并且包括与关键字`Code`和`End Code`。</span><span class="sxs-lookup"><span data-stu-id="834f7-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="834f7-135">将打开`Code`关键字后立即`@`字符&#8212;它们之间不能有空格。</span><span class="sxs-lookup"><span data-stu-id="834f7-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="834f7-136">在浏览器中所显示的结果：</span><span class="sxs-lookup"><span data-stu-id="834f7-136">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="834f7-138">3.在块中，你最终通过行中断每个代码语句</span><span class="sxs-lookup"><span data-stu-id="834f7-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="834f7-139">在 Visual Basic 代码块中，每个语句以换行符结尾。</span><span class="sxs-lookup"><span data-stu-id="834f7-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="834f7-140">（在本文的后面将看到一种方法，如果需要包装为多行长代码语句。）</span><span class="sxs-lookup"><span data-stu-id="834f7-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="834f7-141">4.使用变量来存储值</span><span class="sxs-lookup"><span data-stu-id="834f7-141">4. You use variables to store values</span></span>

<span data-ttu-id="834f7-142">你可以将值存储在*变量*，包括字符串、 数字和日期，等等。创建一个新的变量使用`Dim`关键字。</span><span class="sxs-lookup"><span data-stu-id="834f7-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="834f7-143">你可以直接在页中使用插入变量值`@`。</span><span class="sxs-lookup"><span data-stu-id="834f7-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="834f7-144">在浏览器中所显示的结果：</span><span class="sxs-lookup"><span data-stu-id="834f7-144">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="834f7-146">5.将文本字符串值括在双引号内</span><span class="sxs-lookup"><span data-stu-id="834f7-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="834f7-147">A*字符串*是作为文本处理的字符的序列。</span><span class="sxs-lookup"><span data-stu-id="834f7-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="834f7-148">若要指定一个字符串，则将它括在双引号中：</span><span class="sxs-lookup"><span data-stu-id="834f7-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="834f7-149">若要嵌入字符串值中的双引号括起来，插入两个双引号字符。</span><span class="sxs-lookup"><span data-stu-id="834f7-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="834f7-150">如果你想要一次出现在页面输出的双引号字符，则输入其作为`""`中带引号的字符串，并将其作为输入在您希望其出现两次，如果`""""`中带引号的字符串。</span><span class="sxs-lookup"><span data-stu-id="834f7-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="834f7-151">在浏览器中所显示的结果：</span><span class="sxs-lookup"><span data-stu-id="834f7-151">The result displayed in a browser:</span></span>

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="834f7-153">6.Visual Basic 代码不区分大小写</span><span class="sxs-lookup"><span data-stu-id="834f7-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="834f7-154">Visual Basic 语言不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="834f7-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="834f7-155">编程关键字 (如`Dim`， `If`，和`True`) 和变量名 (如`myString`，或`subTotal`) 可以在任何情况下编写。</span><span class="sxs-lookup"><span data-stu-id="834f7-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="834f7-156">下面的代码行将值分配给该变量`lastname`使用小写名称，然后输出到使用的是大写名称的页变量的值。</span><span class="sxs-lookup"><span data-stu-id="834f7-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="834f7-157">在浏览器中所显示的结果：</span><span class="sxs-lookup"><span data-stu-id="834f7-157">The result displayed in a browser:</span></span>

![vb 语法 5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="834f7-159">7.大部分代码涉及对象的使用</span><span class="sxs-lookup"><span data-stu-id="834f7-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="834f7-160">对象表示，你可以使用编程件事情&#8212;页、 文本框、 文件、 映像、 web 请求、 电子邮件、 客户记录 （数据库行），等等。对象具有属性，用于描述其特征&#8212;文本框对象具有`Text`属性，请求对象具有`Url`属性，电子邮件具有`From`属性和客户对象都有`FirstName`属性。</span><span class="sxs-lookup"><span data-stu-id="834f7-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="834f7-161">对象还具有方法&quot;谓词&quot;他们可以执行。</span><span class="sxs-lookup"><span data-stu-id="834f7-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="834f7-162">示例包括文件对象的`Save`方法中，映像对象的`Rotate`方法和电子邮件对象的`Send`方法。</span><span class="sxs-lookup"><span data-stu-id="834f7-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="834f7-163">通常将使用`Request`对象，这为你提供信息，如值形式的字段 （文本框中，等等），在页面上哪种类型的浏览器发出了请求、 页面、 用户标识，等等的 URL。此示例演示如何访问属性`Request`对象以及如何调用`MapPath`方法`Request`对象，这将使您在服务器上的页的绝对路径：</span><span class="sxs-lookup"><span data-stu-id="834f7-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="834f7-164">在浏览器中所显示的结果：</span><span class="sxs-lookup"><span data-stu-id="834f7-164">The result displayed in a browser:</span></span>

![Razor Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="834f7-166">8.你可以编写做出决策的代码</span><span class="sxs-lookup"><span data-stu-id="834f7-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="834f7-167">动态网页的一项重要功能是你可以确定要执行的操作根据条件。</span><span class="sxs-lookup"><span data-stu-id="834f7-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="834f7-168">若要执行此操作的最常见方法是使用`If`语句 (和可选`Else`语句)。</span><span class="sxs-lookup"><span data-stu-id="834f7-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="834f7-169">语句`If IsPost`是写入的速记方式`If IsPost = True`。</span><span class="sxs-lookup"><span data-stu-id="834f7-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="834f7-170">连同`If`语句，有各种方法来测试条件，重复代码块，并依此类推，它们进行了描述这篇文章中更高版本。</span><span class="sxs-lookup"><span data-stu-id="834f7-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="834f7-171">在浏览器中所显示的结果 (单击后**提交**):</span><span class="sxs-lookup"><span data-stu-id="834f7-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> <span data-ttu-id="834f7-173">**HTTP GET 和 POST 方法以及 IsPost 属性**</span><span class="sxs-lookup"><span data-stu-id="834f7-173">**HTTP GET and POST Methods and the IsPost Property**</span></span>
> 
> <span data-ttu-id="834f7-174">用于网页 (HTTP) 的协议支持非常有限的数量的方法 (&quot;谓词&quot;)，用于向服务器发出请求。</span><span class="sxs-lookup"><span data-stu-id="834f7-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="834f7-175">两个最常见的是 GET，用于读取某页以及开机自检，用于提交的页面。</span><span class="sxs-lookup"><span data-stu-id="834f7-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="834f7-176">一般情况下，用户请求页面时，第一次请求页时使用 GET。</span><span class="sxs-lookup"><span data-stu-id="834f7-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="834f7-177">如果用户在填写窗体，然后单击**提交**，浏览器向服务器发出的 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="834f7-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="834f7-178">在 web 编程中，它通常是有助于你了解是否请求该页为 GET 或 POST，以便你知道如何处理该页。</span><span class="sxs-lookup"><span data-stu-id="834f7-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="834f7-179">在 ASP.NET Web 页中，你可以使用`IsPost`属性以查看是否 GET 或 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="834f7-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="834f7-180">如果请求是 POST，`IsPost`属性将返回 true，并且可执行诸如读取窗体上的文本框的值。</span><span class="sxs-lookup"><span data-stu-id="834f7-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="834f7-181">你将看到许多示例演示如何处理以不同的方式根据的值页`IsPost`。</span><span class="sxs-lookup"><span data-stu-id="834f7-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>


## <a name="a-simple-code-example"></a><span data-ttu-id="834f7-182">一个简单代码示例</span><span class="sxs-lookup"><span data-stu-id="834f7-182">A Simple Code Example</span></span>

<span data-ttu-id="834f7-183">此过程演示如何创建阐释基本的编程技术的页。</span><span class="sxs-lookup"><span data-stu-id="834f7-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="834f7-184">在示例中，你将创建一个允许用户输入两个数字，然后再将它们添加显示结果页面。</span><span class="sxs-lookup"><span data-stu-id="834f7-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="834f7-185">在编辑器中创建一个新文件并将其命名*AddNumbers.vbhtml*。</span><span class="sxs-lookup"><span data-stu-id="834f7-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="834f7-186">将下面的代码和标记复制到页中，替换已在页中的任何内容。</span><span class="sxs-lookup"><span data-stu-id="834f7-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="834f7-187">下面是为你要注意一些事项：</span><span class="sxs-lookup"><span data-stu-id="834f7-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="834f7-188">`@`字符在页中，启动代码的第一个块，它位于之前`totalMessage`变量嵌入底部附近。</span><span class="sxs-lookup"><span data-stu-id="834f7-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="834f7-189">在页面顶部块括在`Code...End Code`。</span><span class="sxs-lookup"><span data-stu-id="834f7-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="834f7-190">变量`total`， `num1`， `num2`，和`totalMessage`存储多个数字和字符串。</span><span class="sxs-lookup"><span data-stu-id="834f7-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="834f7-191">分配给的文字字符串值`totalMessage`变量是在双引号内。</span><span class="sxs-lookup"><span data-stu-id="834f7-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="834f7-192">因为 Visual Basic 代码时不区分大小写，`totalMessage`变量使用页面底部附近，其名称只需要匹配在页面顶部的变量声明的拼写是否正确。</span><span class="sxs-lookup"><span data-stu-id="834f7-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="834f7-193">大小写并不重要。</span><span class="sxs-lookup"><span data-stu-id="834f7-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="834f7-194">表达式`num1.AsInt()`  +  `num2.AsInt()`演示如何使用对象和方法。</span><span class="sxs-lookup"><span data-stu-id="834f7-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="834f7-195">`AsInt`上每个变量的方法将转换为整数 （整数） 可添加到由用户输入的字符串。</span><span class="sxs-lookup"><span data-stu-id="834f7-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="834f7-196">`<form>`标记包含`method="post"`属性。</span><span class="sxs-lookup"><span data-stu-id="834f7-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="834f7-197">此步骤指定当用户单击**添加**，页面将发送到服务器使用 HTTP POST 方法。</span><span class="sxs-lookup"><span data-stu-id="834f7-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="834f7-198">当提交页面，则代码`If IsPost`计算结果为 true，条件的代码运行时，显示的添加数字结果。</span><span class="sxs-lookup"><span data-stu-id="834f7-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="834f7-199">保存页并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="834f7-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="834f7-200">(请确保页中选择**文件**工作区之前运行它。)输入两个整数，然后单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="834f7-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="834f7-202">Visual Basic 语言和语法</span><span class="sxs-lookup"><span data-stu-id="834f7-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="834f7-203">前面你已了解如何创建 ASP.NET web 页中，以及如何将服务器代码添加到 HTML 标记的一个基本示例。</span><span class="sxs-lookup"><span data-stu-id="834f7-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="834f7-204">此处将介绍使用 Visual Basic 编写使用 Razor 语法的 ASP.NET 服务器代码的基础知识&#8212;，即使用编程语言规则。</span><span class="sxs-lookup"><span data-stu-id="834f7-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="834f7-205">如果你有使用编程 （尤其是如果您使用过 C、 c + +、 C#、 Visual Basic 或 JavaScript） 的经验，此处读取大部分将熟悉。</span><span class="sxs-lookup"><span data-stu-id="834f7-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="834f7-206">你可能需要先熟悉一下仅如何 WebMatrix 代码添加到标记中 *.vbhtml*文件。</span><span class="sxs-lookup"><span data-stu-id="834f7-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a>  <span data-ttu-id="834f7-207">组合文本、 标记和代码块中的代码</span><span class="sxs-lookup"><span data-stu-id="834f7-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="834f7-208">在服务器代码块内，你将通常想输出文本和到页面的标记。</span><span class="sxs-lookup"><span data-stu-id="834f7-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="834f7-209">如果服务器代码块包含的文本，不是代码和，而是应呈现原样，ASP.NET 将需要能够将该文本与代码区分开来。</span><span class="sxs-lookup"><span data-stu-id="834f7-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="834f7-210">有若干方法可实现此操作。</span><span class="sxs-lookup"><span data-stu-id="834f7-210">There are several ways to do this.</span></span>

- <span data-ttu-id="834f7-211">将文本括在 HTML 块元素类似`<p></p>`或`<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="834f7-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="834f7-212">文本、 其他 HTML 元素和服务器代码表达式，可以包括 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="834f7-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="834f7-213">当 ASP.NET 发现开始 HTML 标记 (例如， `<p>`)，它会呈现的所有内容的元素，作为其内容是在浏览器 （和解析的服务器代码表达式）。</span><span class="sxs-lookup"><span data-stu-id="834f7-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="834f7-214">使用`@:`运算符或`<text>`元素。</span><span class="sxs-lookup"><span data-stu-id="834f7-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="834f7-215">`@:`输出单个行的内容包含纯文本或不匹配的 HTML 标记;`<text>`元素包含多行输出。</span><span class="sxs-lookup"><span data-stu-id="834f7-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="834f7-216">当你不想要呈现的 HTML 元素作为输出的一部分，这些选项非常有用。</span><span class="sxs-lookup"><span data-stu-id="834f7-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="834f7-217">下面的示例重复前面的示例，但使用一对`<text>`标记括起要呈现的文本。</span><span class="sxs-lookup"><span data-stu-id="834f7-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="834f7-218">在下面的示例中，`<text>`和`</text>`标记括起三行，它们都有一些非包含的文本和不匹配的 HTML 标记的行 (`<br />`)，以及服务器代码和匹配的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="834f7-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="834f7-219">另外无法再次，先完成每个行分别`@:`运算符; 它们的方式都有效。</span><span class="sxs-lookup"><span data-stu-id="834f7-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="834f7-220">此部分中所述，输出文本的时&#8212;使用 HTML 元素，`@:`运算符，或`<text>`元素&#8212;ASP.NET 不会进行 HTML 编码输出。</span><span class="sxs-lookup"><span data-stu-id="834f7-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="834f7-221">(如前所述，ASP.NET 未编码的服务器的代码表达式和服务器代码块前面带有输出`@`，除非在本节中所述的特殊情况。)</span><span class="sxs-lookup"><span data-stu-id="834f7-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="834f7-222">Whitespace</span><span class="sxs-lookup"><span data-stu-id="834f7-222">Whitespace</span></span>

<span data-ttu-id="834f7-223">在语句中 （和外部字符串文本） 的额外空间不会影响该语句：</span><span class="sxs-lookup"><span data-stu-id="834f7-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="834f7-224">长语句拆分为多行</span><span class="sxs-lookup"><span data-stu-id="834f7-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="834f7-225">你可以通过使用下划线字符长码语句拆分为多个行`_`(在 Visual Basic 中的这种行为称为*继续符*) 之后的每一行代码。</span><span class="sxs-lookup"><span data-stu-id="834f7-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="834f7-226">若要中断的语句到下一行，行末尾添加一个空格，然后继续符。</span><span class="sxs-lookup"><span data-stu-id="834f7-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="834f7-227">在下一行继续该语句。</span><span class="sxs-lookup"><span data-stu-id="834f7-227">Continue the statement on the next line.</span></span> <span data-ttu-id="834f7-228">你可以包装到以提高可读性所需的尽可能多行语句。</span><span class="sxs-lookup"><span data-stu-id="834f7-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="834f7-229">以下语句是相同的：</span><span class="sxs-lookup"><span data-stu-id="834f7-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="834f7-230">但是，不能环绕文本字符串中间的行。</span><span class="sxs-lookup"><span data-stu-id="834f7-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="834f7-231">下面的示例不起作用：</span><span class="sxs-lookup"><span data-stu-id="834f7-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="834f7-232">若要合并的长字符串换行到多个行与上面的代码一样，你将需要使用*串联运算符*(`&`)，您可以看到这篇文章中更高版本。</span><span class="sxs-lookup"><span data-stu-id="834f7-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="834f7-233">代码注释</span><span class="sxs-lookup"><span data-stu-id="834f7-233">Code comments</span></span>

<span data-ttu-id="834f7-234">注释可以为自己或他人留言。</span><span class="sxs-lookup"><span data-stu-id="834f7-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="834f7-235">带有前缀 razor 语法注释`@*`和以结尾`*@`。</span><span class="sxs-lookup"><span data-stu-id="834f7-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="834f7-236">在代码块内，你可以使用 Razor 语法注释，或者可以使用普通的 Visual Basic 注释字符，这是单引号 (`'`) 每一行的前缀。</span><span class="sxs-lookup"><span data-stu-id="834f7-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="834f7-237">变量</span><span class="sxs-lookup"><span data-stu-id="834f7-237">Variables</span></span>

<span data-ttu-id="834f7-238">变量是用于存储数据的已命名的对象。</span><span class="sxs-lookup"><span data-stu-id="834f7-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="834f7-239">您可以命名变量的任何内容，但名称必须以字母字符开头，不能包含空格或保留的字符。</span><span class="sxs-lookup"><span data-stu-id="834f7-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="834f7-240">在 Visual Basic 中，正如你看到的更早版本，并不重要的变量名称中的字母大小写。</span><span class="sxs-lookup"><span data-stu-id="834f7-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="834f7-241">变量和数据类型</span><span class="sxs-lookup"><span data-stu-id="834f7-241">Variables and data types</span></span>

<span data-ttu-id="834f7-242">变量可以具有特定的数据类型，这表示什么类型的数据存储在变量中。</span><span class="sxs-lookup"><span data-stu-id="834f7-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="834f7-243">你可以存储字符串值的字符串变量 (如&quot;Hello world&quot;)，整数变量，其中存储整数值 （如 3 或 79） 和各种 （例如，2012 年 4 月 12 日或 2009 年 3 月的格式存储日期值的日期变量).</span><span class="sxs-lookup"><span data-stu-id="834f7-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="834f7-244">还有许多其他可以使用的数据类型。</span><span class="sxs-lookup"><span data-stu-id="834f7-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="834f7-245">但是，你不必指定类型的变量。</span><span class="sxs-lookup"><span data-stu-id="834f7-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="834f7-246">在大多数情况下 ASP.NET 可以找出基于了如何使用变量中的数据的类型。</span><span class="sxs-lookup"><span data-stu-id="834f7-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="834f7-247">（有时必须指定一个类型; 你将看到示例其中是如此。）</span><span class="sxs-lookup"><span data-stu-id="834f7-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="834f7-248">若要声明变量时不指定类型的情况下，使用`Dim`加变量的名称 (例如， `Dim myVar`)。</span><span class="sxs-lookup"><span data-stu-id="834f7-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="834f7-249">若要使用的类型声明变量时，使用`Dim`加变量的名称后, 跟`As`，然后是类型名称 (例如， `Dim myVar As String`)。</span><span class="sxs-lookup"><span data-stu-id="834f7-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="834f7-250">下面的示例演示某些内联表达式，在网页中使用变量。</span><span class="sxs-lookup"><span data-stu-id="834f7-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="834f7-251">在浏览器中所显示的结果：</span><span class="sxs-lookup"><span data-stu-id="834f7-251">The result displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="834f7-253">转换和测试数据类型</span><span class="sxs-lookup"><span data-stu-id="834f7-253">Converting and testing data types</span></span>

<span data-ttu-id="834f7-254">尽管 ASP.NET 通常可以自动确定数据类型，有时它不能。</span><span class="sxs-lookup"><span data-stu-id="834f7-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="834f7-255">因此，你可能需要帮助解决 ASP.NET，通过执行显式转换。</span><span class="sxs-lookup"><span data-stu-id="834f7-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="834f7-256">即使你无需转换类型，有时会有帮助进行测试以查看哪种类型的数据你可能正在处理。</span><span class="sxs-lookup"><span data-stu-id="834f7-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="834f7-257">最常见的情况是，你必须将字符串转换为另一个类型，如整数或日期。</span><span class="sxs-lookup"><span data-stu-id="834f7-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="834f7-258">下面的示例演示一种典型情况其中必须将字符串转换为数字。</span><span class="sxs-lookup"><span data-stu-id="834f7-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="834f7-259">一般来说，用户输入发送给您作为字符串。</span><span class="sxs-lookup"><span data-stu-id="834f7-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="834f7-260">即使已提示用户输入一个数字，并且即使在提交用户输入而读取在代码中所输入的一个数字，数据是字符串格式。</span><span class="sxs-lookup"><span data-stu-id="834f7-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="834f7-261">因此，你必须将字符串转换为数字。</span><span class="sxs-lookup"><span data-stu-id="834f7-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="834f7-262">在示例中，如果你尝试对值执行算术运算，而不转换它们，以下的错误结果，因为 ASP.NET 不能添加两个字符串：</span><span class="sxs-lookup"><span data-stu-id="834f7-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="834f7-263">若要将值转换为整数，则调用`AsInt`方法。</span><span class="sxs-lookup"><span data-stu-id="834f7-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="834f7-264">如果转换成功，你可以然后添加数字。</span><span class="sxs-lookup"><span data-stu-id="834f7-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="834f7-265">下表列出了一些常见的转换和测试方法的变量。</span><span class="sxs-lookup"><span data-stu-id="834f7-265">The following table lists some common conversion and test methods for variables.</span></span>


<span data-ttu-id="834f7-266">::: 行:::::: 列:::<strong>方法</strong>::: 列端:::::: 列:::<strong>说明</strong>::: 列端:::::: 列:::<strong>示例</strong>::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-266">:::row::: :::column::: <strong>Method</strong> :::column-end::: :::column::: <strong>Description</strong> :::column-end::: :::column::: <strong>Example</strong> :::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-267">::: 行:::::: 列::: `AsInt(), IsInt()` ::: 列端:::::: 列::: 将表示为整数的字符串转换 (如&quot;593&quot;) 为整数。</span><span class="sxs-lookup"><span data-stu-id="834f7-267">:::row::: :::column::: `AsInt(), IsInt()` :::column-end::: :::column::: Converts a string that represents a whole number (like &quot;593&quot;) to an integer.</span></span>
<span data-ttu-id="834f7-268">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-268">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]</span></span>
    <span data-ttu-id="834f7-269">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-269">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-270">::: 行:::::: 列::: `AsBool(), IsBool()` ::: 列端:::::: 列::: 将转换字符串如下所示&quot;true&quot;或&quot;false&quot;到类型为 Boolean 类型。</span><span class="sxs-lookup"><span data-stu-id="834f7-270">:::row::: :::column::: `AsBool(), IsBool()` :::column-end::: :::column::: Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
<span data-ttu-id="834f7-271">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-271">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]</span></span>
    <span data-ttu-id="834f7-272">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-272">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-273">::: 行:::::: 列::: `AsFloat(), IsFloat()` ::: 列端:::::: 列::: 将具有类似的十进制值的字符串转换&quot;1.3&quot;或&quot;7.439&quot;为浮点数。</span><span class="sxs-lookup"><span data-stu-id="834f7-273">:::row::: :::column::: `AsFloat(), IsFloat()` :::column-end::: :::column::: Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
<span data-ttu-id="834f7-274">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-274">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]</span></span>
    <span data-ttu-id="834f7-275">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-275">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-276">::: 行:::::: 列::: `AsDecimal(), IsDecimal()` ::: 列端:::::: 列::: 将具有类似的十进制值的字符串转换&quot;1.3&quot;或&quot;7.439&quot;为十进制数。</span><span class="sxs-lookup"><span data-stu-id="834f7-276">:::row::: :::column::: `AsDecimal(), IsDecimal()` :::column-end::: :::column::: Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="834f7-277">（在 ASP.NET 中，十进制数是比浮点数更精确。）::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-277">(In ASP.NET, a decimal number is more precise than a floating-point number.) :::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]</span></span>
    <span data-ttu-id="834f7-278">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-278">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-279">::: 行:::::: 列::: `AsDateTime(), IsDateTime()` ::: 列端:::::: 列::: 将对 ASP.NET 表示的日期和时间值的字符串转换`DateTime`类型。</span><span class="sxs-lookup"><span data-stu-id="834f7-279">:::row::: :::column::: `AsDateTime(), IsDateTime()` :::column-end::: :::column::: Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
<span data-ttu-id="834f7-280">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-280">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]</span></span>
    <span data-ttu-id="834f7-281">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-281">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-282">::: 行:::::: 列::: `ToString()` ::: 列端:::::: 列::: 将任何其他数据类型转换为字符串。</span><span class="sxs-lookup"><span data-stu-id="834f7-282">:::row::: :::column::: `ToString()` :::column-end::: :::column::: Converts any other data type to a string.</span></span>
<span data-ttu-id="834f7-283">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-283">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]</span></span>
    <span data-ttu-id="834f7-284">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-284">:::column-end::: :::row-end:::</span></span>


## <a name="operators"></a><span data-ttu-id="834f7-285">运算符</span><span class="sxs-lookup"><span data-stu-id="834f7-285">Operators</span></span>

<span data-ttu-id="834f7-286">运算符是命令的关键字或哪种类型的表达式中执行将告诉 ASP.NET 的字符。</span><span class="sxs-lookup"><span data-stu-id="834f7-286">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="834f7-287">Visual Basic 支持许多运算符，但你只需以识别一些若要开始开发 ASP.NET web 页。</span><span class="sxs-lookup"><span data-stu-id="834f7-287">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="834f7-288">下表总结了最常用的运算符。</span><span class="sxs-lookup"><span data-stu-id="834f7-288">The following table summarizes the most common operators.</span></span>


<span data-ttu-id="834f7-289">::: 行:::::: 列:::<strong>运算符</strong>::: 列端:::::: 列:::<strong>说明</strong>::: 列端:::::: 列:::<strong>示例</strong>::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-289">:::row::: :::column::: <strong>Operator</strong> :::column-end::: :::column::: <strong>Description</strong> :::column-end::: :::column::: <strong>Examples</strong> :::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-290">::: 行:::::: 列::: `+ - * /` ::: 列端:::::: 列::: 数学运算符在数值表达式中使用。</span><span class="sxs-lookup"><span data-stu-id="834f7-290">:::row::: :::column::: `+ - * /` :::column-end::: :::column::: Math operators used in numerical expressions.</span></span>
<span data-ttu-id="834f7-291">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-291">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]</span></span>
    <span data-ttu-id="834f7-292">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-292">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-293">::: 行:::::: 列::: `=` ::: 列端:::::: 列::: 分配和相等性。</span><span class="sxs-lookup"><span data-stu-id="834f7-293">:::row::: :::column::: `=` :::column-end::: :::column::: Assignment and equality.</span></span> <span data-ttu-id="834f7-294">根据上下文，或者将语句右侧的值分配给左侧，对象，或检查值相等。</span><span class="sxs-lookup"><span data-stu-id="834f7-294">Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.</span></span>
<span data-ttu-id="834f7-295">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-295">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]</span></span>
    <span data-ttu-id="834f7-296">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-296">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-297">::: 行:::::: 列::: `<>` ::: 列端:::::: 列::: 是否不相等。</span><span class="sxs-lookup"><span data-stu-id="834f7-297">:::row::: :::column::: `<>` :::column-end::: :::column::: Inequality.</span></span> <span data-ttu-id="834f7-298">返回`True`如果值不相等。</span><span class="sxs-lookup"><span data-stu-id="834f7-298">Returns `True` if the values are not equal.</span></span>
<span data-ttu-id="834f7-299">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-299">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]</span></span>
    <span data-ttu-id="834f7-300">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-300">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-301">::: 行:::::: 列::: `< > <= >=` ::: 列端:::::: 列::: 小于、 大于、 小于或等于、 和大于或等于。</span><span class="sxs-lookup"><span data-stu-id="834f7-301">:::row::: :::column::: `< > <= >=` :::column-end::: :::column::: Less than, greater than, less than or equal, and greater than or equal.</span></span>
<span data-ttu-id="834f7-302">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-302">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]</span></span>
    <span data-ttu-id="834f7-303">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-303">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-304">::: 行:::::: 列::: `&` ::: 列端:::::: 列::: 串联，用来联接字符串。</span><span class="sxs-lookup"><span data-stu-id="834f7-304">:::row::: :::column::: `&` :::column-end::: :::column::: Concatenation, which is used to join strings.</span></span>
<span data-ttu-id="834f7-305">::: 列端:::::: 列::: [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]</span><span class="sxs-lookup"><span data-stu-id="834f7-305">:::column-end::: :::column::: [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]</span></span>
    <span data-ttu-id="834f7-306">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-306">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-307">::: 行:::::: 列::: `+= -=` ::: 列端:::::: 列::: 递增和递减运算符，从而添加，并且从变量 （分别） 减去 1。</span><span class="sxs-lookup"><span data-stu-id="834f7-307">:::row::: :::column::: `+= -=` :::column-end::: :::column::: The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
<span data-ttu-id="834f7-308">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-308">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]</span></span>
    <span data-ttu-id="834f7-309">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-309">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-310">::: 行:::::: 列::: `.` ::: 列端:::::: 列::: 点。</span><span class="sxs-lookup"><span data-stu-id="834f7-310">:::row::: :::column::: `.` :::column-end::: :::column::: Dot.</span></span> <span data-ttu-id="834f7-311">用于区分对象及其属性和方法。</span><span class="sxs-lookup"><span data-stu-id="834f7-311">Used to distinguish objects and their properties and methods.</span></span>
<span data-ttu-id="834f7-312">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-312">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]</span></span>
    <span data-ttu-id="834f7-313">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-313">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-314">::: 行:::::: 列::: `()` ::: 列端:::::: 列::: 括号。</span><span class="sxs-lookup"><span data-stu-id="834f7-314">:::row::: :::column::: `()` :::column-end::: :::column::: Parentheses.</span></span> <span data-ttu-id="834f7-315">为组表达式，用于将参数传递到方法，并访问数组和集合的成员。</span><span class="sxs-lookup"><span data-stu-id="834f7-315">Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.</span></span>
<span data-ttu-id="834f7-316">::: 列端:::::: 列::: [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]</span><span class="sxs-lookup"><span data-stu-id="834f7-316">:::column-end::: :::column::: [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]</span></span>
    <span data-ttu-id="834f7-317">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-317">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-318">::: 行:::::: 列::: `Not` ::: 列端:::::: 列::: 不。</span><span class="sxs-lookup"><span data-stu-id="834f7-318">:::row::: :::column::: `Not` :::column-end::: :::column::: Not.</span></span> <span data-ttu-id="834f7-319">反转 true 值为 false，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="834f7-319">Reverses a true value to false and vice versa.</span></span> <span data-ttu-id="834f7-320">通常用作要测试的速记方法`False`(即，为不`True`)。</span><span class="sxs-lookup"><span data-stu-id="834f7-320">Typically used as a shorthand way to test for `False` (that is, for not `True`).</span></span>
<span data-ttu-id="834f7-321">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-321">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]</span></span>
    <span data-ttu-id="834f7-322">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-322">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="834f7-323">::: 行:::::: 列::: `AndAlso OrElse` ::: 列端:::::: 列::: 逻辑和也用于链接条件组合在一起。</span><span class="sxs-lookup"><span data-stu-id="834f7-323">:::row::: :::column::: `AndAlso OrElse` :::column-end::: :::column::: Logical AND and OR, which are used to link conditions together.</span></span>
<span data-ttu-id="834f7-324">::: 列端:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]</span><span class="sxs-lookup"><span data-stu-id="834f7-324">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]</span></span>
    <span data-ttu-id="834f7-325">::: 列端:::::: 行尾:::</span><span class="sxs-lookup"><span data-stu-id="834f7-325">:::column-end::: :::row-end:::</span></span>

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="834f7-326">使用文件和代码中的文件夹路径</span><span class="sxs-lookup"><span data-stu-id="834f7-326">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="834f7-327">将在代码中经常处理的文件和文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="834f7-327">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="834f7-328">可能显示的开发计算机上，下面是一个网站的物理文件夹结构的示例：</span><span class="sxs-lookup"><span data-stu-id="834f7-328">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="834f7-329">下面是一些有关 Url 和路径的基本详细信息：</span><span class="sxs-lookup"><span data-stu-id="834f7-329">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="834f7-330">URL 开头的域名 (`http://www.example.com`) 或服务器名称 (`http://localhost`， `http://mycomputer`)。</span><span class="sxs-lookup"><span data-stu-id="834f7-330">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="834f7-331">URL 对应于主机计算机上的物理路径。</span><span class="sxs-lookup"><span data-stu-id="834f7-331">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="834f7-332">例如，`http://myserver`可能对应于文件夹*C:\websites\mywebsite*服务器上。</span><span class="sxs-lookup"><span data-stu-id="834f7-332">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="834f7-333">虚拟路径是简写形式来表示在代码中的路径，而无需指定完整路径。</span><span class="sxs-lookup"><span data-stu-id="834f7-333">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="834f7-334">它包含后面的域或服务器名称的 URL 的部分。</span><span class="sxs-lookup"><span data-stu-id="834f7-334">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="834f7-335">当你使用虚拟路径时，可以无需更新的路径，将代码移动到不同的域或服务器。</span><span class="sxs-lookup"><span data-stu-id="834f7-335">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="834f7-336">此处是一个示例来帮助你了解的差异：</span><span class="sxs-lookup"><span data-stu-id="834f7-336">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="834f7-337">完整的 URL</span><span class="sxs-lookup"><span data-stu-id="834f7-337">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="834f7-338">服务器名称</span><span class="sxs-lookup"><span data-stu-id="834f7-338">Server name</span></span> | <span data-ttu-id="834f7-339">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="834f7-339">*mycompanyserver*</span></span> |
| <span data-ttu-id="834f7-340">虚拟路径</span><span class="sxs-lookup"><span data-stu-id="834f7-340">Virtual path</span></span> | <span data-ttu-id="834f7-341">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="834f7-341">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="834f7-342">物理路径</span><span class="sxs-lookup"><span data-stu-id="834f7-342">Physical path</span></span> | <span data-ttu-id="834f7-343">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="834f7-343">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="834f7-344">虚拟根目录为 /，驱动器是一样的 c： 根目录 \。</span><span class="sxs-lookup"><span data-stu-id="834f7-344">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="834f7-345">（虚拟文件夹路径始终使用正斜杠。）文件夹的虚拟路径不需要作为物理文件夹; 具有相同的名称它可以是一个别名。</span><span class="sxs-lookup"><span data-stu-id="834f7-345">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="834f7-346">（生产服务器上的虚拟路径很少的匹配确切的物理路径。）</span><span class="sxs-lookup"><span data-stu-id="834f7-346">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="834f7-347">当代码中的文件和文件夹时，有时你需要引用的物理路径和有时虚拟路径，具体取决于你正在使用哪些对象。</span><span class="sxs-lookup"><span data-stu-id="834f7-347">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="834f7-348">ASP.NET 为你提供这些工具用于处理在代码中的文件和文件夹路径：`Server.MapPath`方法，与`~`运算符和`Href`方法。</span><span class="sxs-lookup"><span data-stu-id="834f7-348">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="834f7-349">转换虚拟与物理路径： Server.MapPath 方法</span><span class="sxs-lookup"><span data-stu-id="834f7-349">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="834f7-350">`Server.MapPath`方法将转换的虚拟路径 (如 */default.cshtml*) 为绝对物理路径 (如*C:\WebSites\MyWebSiteFolder\default.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="834f7-350">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="834f7-351">需要完整的物理路径时使用此方法。</span><span class="sxs-lookup"><span data-stu-id="834f7-351">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="834f7-352">一个典型示例是要读取或写入文本文件或 web 服务器上的图像文件时。</span><span class="sxs-lookup"><span data-stu-id="834f7-352">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="834f7-353">你通常不知道你的站点托管站点的服务器上的绝对物理路径，因此此方法可以将路径转换你知道-的虚拟路径-到你的服务器上的相应路径。</span><span class="sxs-lookup"><span data-stu-id="834f7-353">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="834f7-354">将虚拟路径传递给文件或文件夹的方法，并返回物理路径：</span><span class="sxs-lookup"><span data-stu-id="834f7-354">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="834f7-355">引用的虚拟根： ~ 运算符和 Href 方法</span><span class="sxs-lookup"><span data-stu-id="834f7-355">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="834f7-356">在 *.cshtml*或 *.vbhtml*文件，你可以引用虚拟根路径使用`~`运算符。</span><span class="sxs-lookup"><span data-stu-id="834f7-356">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="834f7-357">这是非常方便，因为您可以来回移动网页，在站点中，并且它们包含至其他页面的任何链接不会被破坏。</span><span class="sxs-lookup"><span data-stu-id="834f7-357">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="834f7-358">也很方便以防曾经将你的网站移动到其他位置。</span><span class="sxs-lookup"><span data-stu-id="834f7-358">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="834f7-359">下面是一些可能的恶意活动：</span><span class="sxs-lookup"><span data-stu-id="834f7-359">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="834f7-360">如果网站`http://myserver/myapp`，下面是运行页面时 ASP.NET 将这些路径的方式：</span><span class="sxs-lookup"><span data-stu-id="834f7-360">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="834f7-361">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="834f7-361">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="834f7-362">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="834f7-362">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="834f7-363">（你实际上不会看到这些路径的值的变量，但 ASP.NET 将则将路径视为即它们是一样。）</span><span class="sxs-lookup"><span data-stu-id="834f7-363">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="834f7-364">你可以使用`~`运算符在 （如上所述） 的服务器代码和在标记中，如下：</span><span class="sxs-lookup"><span data-stu-id="834f7-364">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="834f7-365">在标记中，你使用`~`运算符来创建资源，如图像文件、 其他网页和 CSS 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="834f7-365">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="834f7-366">ASP.NET 页运行时，（代码和标记） 页中查找和解析所有`~`与相应路径的引用。</span><span class="sxs-lookup"><span data-stu-id="834f7-366">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="834f7-367">条件逻辑，并循环</span><span class="sxs-lookup"><span data-stu-id="834f7-367">Conditional Logic and Loops</span></span>

<span data-ttu-id="834f7-368">ASP.NET 服务器代码允许你执行基于条件和重复特定次数，即代码的语句运行循环的编写代码的任务）。</span><span class="sxs-lookup"><span data-stu-id="834f7-368">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="834f7-369">测试条件</span><span class="sxs-lookup"><span data-stu-id="834f7-369">Testing conditions</span></span>

<span data-ttu-id="834f7-370">你使用对简单条件进行测试`If...Then`语句，它返回`True`或`False`基于你指定的测试：</span><span class="sxs-lookup"><span data-stu-id="834f7-370">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="834f7-371">`If`关键字开始块。</span><span class="sxs-lookup"><span data-stu-id="834f7-371">The `If` keyword starts a block.</span></span> <span data-ttu-id="834f7-372">实际的测试 （条件） 遵循`If`关键字，并返回 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="834f7-372">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="834f7-373">`If`语句结尾`Then`。</span><span class="sxs-lookup"><span data-stu-id="834f7-373">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="834f7-374">如果测试为 true，将运行的语句括通过`If`和`End If`。</span><span class="sxs-lookup"><span data-stu-id="834f7-374">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="834f7-375">`If`语句可以包含`Else`指定语句在条件为 false 时要运行的块：</span><span class="sxs-lookup"><span data-stu-id="834f7-375">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="834f7-376">如果`If`语句启动代码块时，无需使用普通`Code...End Code`语句以包括的块。</span><span class="sxs-lookup"><span data-stu-id="834f7-376">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="834f7-377">可以仅添加`@`到块，以及它将工作。</span><span class="sxs-lookup"><span data-stu-id="834f7-377">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="834f7-378">此方法适用于`If`以及编程关键字跟代码块，包括其他 Visual Basic `For`， `For Each`， `Do While`，等等。</span><span class="sxs-lookup"><span data-stu-id="834f7-378">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="834f7-379">你可以添加多个条件使用一个或多个`ElseIf`块：</span><span class="sxs-lookup"><span data-stu-id="834f7-379">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="834f7-380">在此示例中，如果第一个条件中`If`块不为 true，`ElseIf`才会检查条件。</span><span class="sxs-lookup"><span data-stu-id="834f7-380">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="834f7-381">如果满足该条件，则中的语句`ElseIf`块执行。</span><span class="sxs-lookup"><span data-stu-id="834f7-381">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="834f7-382">如果不符合任何条件中的语句`Else`块执行。</span><span class="sxs-lookup"><span data-stu-id="834f7-382">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="834f7-383">你可以添加任意数量的`ElseIf`块，并与然后关闭`Else`作为阻止&quot;其他一切&quot;条件。</span><span class="sxs-lookup"><span data-stu-id="834f7-383">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="834f7-384">若要测试大量的条件，使用`Select Case`块：</span><span class="sxs-lookup"><span data-stu-id="834f7-384">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="834f7-385">要测试的值位于 （在示例中，工作日变量） 的括号中。</span><span class="sxs-lookup"><span data-stu-id="834f7-385">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="834f7-386">每个单独测试使用`Case`列出一个值的语句。</span><span class="sxs-lookup"><span data-stu-id="834f7-386">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="834f7-387">如果值`Case`语句与匹配的测试的值的代码`Case`执行块。</span><span class="sxs-lookup"><span data-stu-id="834f7-387">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="834f7-388">在浏览器中显示的最后两个条件块的结果：</span><span class="sxs-lookup"><span data-stu-id="834f7-388">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="834f7-390">循环的代码</span><span class="sxs-lookup"><span data-stu-id="834f7-390">Looping code</span></span>

<span data-ttu-id="834f7-391">你经常需要重复运行相同的语句。</span><span class="sxs-lookup"><span data-stu-id="834f7-391">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="834f7-392">通过循环执行此操作。</span><span class="sxs-lookup"><span data-stu-id="834f7-392">You do this by looping.</span></span> <span data-ttu-id="834f7-393">例如，你通常运行的相同语句的每个项集合中的数据。</span><span class="sxs-lookup"><span data-stu-id="834f7-393">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="834f7-394">如果你知道完全多少次想要循环，则可以使用`For`循环。</span><span class="sxs-lookup"><span data-stu-id="834f7-394">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="834f7-395">这种类型是循环的的向上计数或倒计时特别有用：</span><span class="sxs-lookup"><span data-stu-id="834f7-395">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="834f7-396">循环开头`For`关键字后, 跟三个元素：</span><span class="sxs-lookup"><span data-stu-id="834f7-396">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="834f7-397">后立即`For`语句，您将计数器变量声明 (无需使用`Dim`) 然后中表示范围， `i = 10 to 20`。</span><span class="sxs-lookup"><span data-stu-id="834f7-397">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="834f7-398">这意味着变量`i`将开始计数 10 并继续，直到它达到 20 （含）。</span><span class="sxs-lookup"><span data-stu-id="834f7-398">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="834f7-399">之间`For`和`Next`语句为块的内容。</span><span class="sxs-lookup"><span data-stu-id="834f7-399">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="834f7-400">这可以包含一个或多个代码语句，执行与每个循环。</span><span class="sxs-lookup"><span data-stu-id="834f7-400">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="834f7-401">`Next i`语句结束循环。</span><span class="sxs-lookup"><span data-stu-id="834f7-401">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="834f7-402">它会递增的计数器，并启动循环的下一个迭代。</span><span class="sxs-lookup"><span data-stu-id="834f7-402">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="834f7-403">之间的代码行`For`和`Next`行包含每个迭代的循环中运行的代码。</span><span class="sxs-lookup"><span data-stu-id="834f7-403">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="834f7-404">标记将创建一个新段落 (`<p>`元素) 每个时间，并将行添加到输出中，显示的值 i （计数器）。</span><span class="sxs-lookup"><span data-stu-id="834f7-404">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="834f7-405">运行此页时，该示例将创建 11 行显示输出，与每个行，该值指示项数中的文本。</span><span class="sxs-lookup"><span data-stu-id="834f7-405">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="834f7-407">如果你正在使用集合或数组，则通常会使用`For Each`循环。</span><span class="sxs-lookup"><span data-stu-id="834f7-407">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="834f7-408">集合是一组类似对象和`For Each`循环的允许您执行的任务集合中的每个项。</span><span class="sxs-lookup"><span data-stu-id="834f7-408">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="834f7-409">这种类型的循环是方便对于集合，因为与不同`For`循环中，你无需递增计数器或设置一个限制。</span><span class="sxs-lookup"><span data-stu-id="834f7-409">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="834f7-410">相反，`For Each`循环代码只需继续访问该集合之前完成。</span><span class="sxs-lookup"><span data-stu-id="834f7-410">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="834f7-411">此示例将返回中的项`Request.ServerVariables`集合 （其中包含有关你的 web 服务器的信息）。</span><span class="sxs-lookup"><span data-stu-id="834f7-411">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="834f7-412">它使用`For Each`循环来显示每个项的名称，通过创建新`<li>`HTML 项目符号列表中的元素。</span><span class="sxs-lookup"><span data-stu-id="834f7-412">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="834f7-413">`For Each`关键字后跟表示单个项集合中的变量 (在示例中， `myItem`) 后, 跟`In`关键字后, 跟你想要循环访问的集合。</span><span class="sxs-lookup"><span data-stu-id="834f7-413">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="834f7-414">正文中`For Each`循环中，你可以访问使用你之前声明的变量的当前项。</span><span class="sxs-lookup"><span data-stu-id="834f7-414">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="834f7-416">若要创建更通用的循环，使用`Do While`语句：</span><span class="sxs-lookup"><span data-stu-id="834f7-416">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="834f7-417">此循环开头`Do While`关键字后, 跟一个条件后, 跟用于重复的块。</span><span class="sxs-lookup"><span data-stu-id="834f7-417">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="834f7-418">循环通常递增 （添加） 或递减 （从减） 变量或用于计数的对象。</span><span class="sxs-lookup"><span data-stu-id="834f7-418">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="834f7-419">在示例中，`+=`已将 1 运算符添加到变量的值每次循环运行的时。</span><span class="sxs-lookup"><span data-stu-id="834f7-419">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="834f7-420">(要递减进行倒计时的循环中的变量，你可以使用递减运算符`-=`。)</span><span class="sxs-lookup"><span data-stu-id="834f7-420">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="834f7-421">对象和集合</span><span class="sxs-lookup"><span data-stu-id="834f7-421">Objects and Collections</span></span>

<span data-ttu-id="834f7-422">在 ASP.NET 网站中几乎所有操作是一个对象，包括 web 页本身。</span><span class="sxs-lookup"><span data-stu-id="834f7-422">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="834f7-423">本部分讨论一些重要的对象，你将经常你在代码中使用。</span><span class="sxs-lookup"><span data-stu-id="834f7-423">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="834f7-424">Page 对象</span><span class="sxs-lookup"><span data-stu-id="834f7-424">Page objects</span></span>

<span data-ttu-id="834f7-425">在 ASP.NET 中的最基本对象是的页。</span><span class="sxs-lookup"><span data-stu-id="834f7-425">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="834f7-426">你可以访问的直接不带任何合格的对象的页对象的属性。</span><span class="sxs-lookup"><span data-stu-id="834f7-426">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="834f7-427">以下代码将获取该页面的文件路径，使用`Request`页的对象：</span><span class="sxs-lookup"><span data-stu-id="834f7-427">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="834f7-428">你可以使用属性的`Page`对象以获取大量的信息，如：</span><span class="sxs-lookup"><span data-stu-id="834f7-428">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="834f7-429">`Request`。</span><span class="sxs-lookup"><span data-stu-id="834f7-429">`Request`.</span></span> <span data-ttu-id="834f7-430">如你已经了解，这是信息的有关当前请求，包括哪种类型的浏览器发出了请求、 页面、 用户标识，等等的 URL 的集合。</span><span class="sxs-lookup"><span data-stu-id="834f7-430">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="834f7-431">`Response`。</span><span class="sxs-lookup"><span data-stu-id="834f7-431">`Response`.</span></span> <span data-ttu-id="834f7-432">这是信息的有关将发送到浏览器中，当服务器代码程序完成运行响应 （页） 的集合。</span><span class="sxs-lookup"><span data-stu-id="834f7-432">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="834f7-433">例如，此属性可用于将信息写入到响应中。</span><span class="sxs-lookup"><span data-stu-id="834f7-433">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="834f7-434">（数组和字典） 的集合对象</span><span class="sxs-lookup"><span data-stu-id="834f7-434">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="834f7-435">集合是一组相同的类型，例如的集合对象`Customer`数据库中的对象。</span><span class="sxs-lookup"><span data-stu-id="834f7-435">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="834f7-436">ASP.NET 包含多个内置集合，如`Request.Files`集合。</span><span class="sxs-lookup"><span data-stu-id="834f7-436">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="834f7-437">通常，你将使用集合中的数据。</span><span class="sxs-lookup"><span data-stu-id="834f7-437">You'll often work with data in collections.</span></span> <span data-ttu-id="834f7-438">两个常见集合类型是*数组*和*字典*。</span><span class="sxs-lookup"><span data-stu-id="834f7-438">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="834f7-439">如果你想要存储的相似的项目集合，但不想创建一个单独的变量以保存每个项，则数组非常有用：</span><span class="sxs-lookup"><span data-stu-id="834f7-439">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="834f7-440">数组，可声明特定的数据类型，如`String`， `Integer`，或`DateTime`。</span><span class="sxs-lookup"><span data-stu-id="834f7-440">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="834f7-441">要指明变量可以包含一个数组，可将括号添加到声明中的变量名称 (如`Dim myVar() As String`)。</span><span class="sxs-lookup"><span data-stu-id="834f7-441">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="834f7-442">你可以访问项数组使用它们的位置 （索引） 中或通过使用`For Each`语句。</span><span class="sxs-lookup"><span data-stu-id="834f7-442">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="834f7-443">数组索引是从零开始&#8212;，即第一项是在位置 0，第二项是在位置 1，依此类推。</span><span class="sxs-lookup"><span data-stu-id="834f7-443">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="834f7-444">你可以通过获取确定数组中的项的数目及其`Length`属性。</span><span class="sxs-lookup"><span data-stu-id="834f7-444">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="834f7-445">若要获取数组中特定项的位置 (即，搜索数组)，使用`Array.IndexOf`方法。</span><span class="sxs-lookup"><span data-stu-id="834f7-445">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="834f7-446">你还可以执行诸如反向数组的内容 (`Array.Reverse`方法) 或对内容进行排序 (`Array.Sort`方法)。</span><span class="sxs-lookup"><span data-stu-id="834f7-446">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="834f7-447">在浏览器中显示的字符串数组代码的输出：</span><span class="sxs-lookup"><span data-stu-id="834f7-447">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="834f7-449">字典是键/值对的集合，其中提供的密钥 （或名称） 来设置或检索相应的值：</span><span class="sxs-lookup"><span data-stu-id="834f7-449">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="834f7-450">若要创建一个字典，请使用`New`关键字以指示你要创建一个新`Dictionary`对象。</span><span class="sxs-lookup"><span data-stu-id="834f7-450">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="834f7-451">你可以将字典分配给变量的使用`Dim`关键字。</span><span class="sxs-lookup"><span data-stu-id="834f7-451">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="834f7-452">指示在使用括号字典中的项的数据类型 ( `( )` )。</span><span class="sxs-lookup"><span data-stu-id="834f7-452">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="834f7-453">在声明的末尾，你必须添加另一对括号，因为这是实际创建一个新的字典的方法。</span><span class="sxs-lookup"><span data-stu-id="834f7-453">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="834f7-454">若要将项添加到字典中，你可以调用`Add`字典变量或方法 (`myScores`在这种情况下)，然后指定一个键和值。</span><span class="sxs-lookup"><span data-stu-id="834f7-454">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="834f7-455">或者，可以使用括号以指示键和执行简单的赋值，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="834f7-455">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="834f7-456">若要从字典中获取一个值，请在括号中指定的密钥：</span><span class="sxs-lookup"><span data-stu-id="834f7-456">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="834f7-457">调用带参数的方法</span><span class="sxs-lookup"><span data-stu-id="834f7-457">Calling Methods with Parameters</span></span>

<span data-ttu-id="834f7-458">正如你看到这篇文章中的更早版本，与程序的对象具有方法。</span><span class="sxs-lookup"><span data-stu-id="834f7-458">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="834f7-459">例如，`Database`对象可能具有`Database.Connect`方法。</span><span class="sxs-lookup"><span data-stu-id="834f7-459">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="834f7-460">许多方法还具有一个或多个参数。</span><span class="sxs-lookup"><span data-stu-id="834f7-460">Many methods also have one or more parameters.</span></span> <span data-ttu-id="834f7-461">A*参数*是向某个方法传递的值以使该方法以完成其任务。</span><span class="sxs-lookup"><span data-stu-id="834f7-461">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="834f7-462">例如，查看有关声明`Request.MapPath`方法，采用三个参数：</span><span class="sxs-lookup"><span data-stu-id="834f7-462">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="834f7-463">此方法对应的服务器上的物理路径返回到指定的虚拟路径。</span><span class="sxs-lookup"><span data-stu-id="834f7-463">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="834f7-464">该方法的三个参数`virtualPath`， `baseVirtualDir`，和`allowCrossAppMapping`。</span><span class="sxs-lookup"><span data-stu-id="834f7-464">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="834f7-465">（请注意，在声明中，列出了参数将接受的数据的数据类型）。在调用此方法时，你必须提供所有三个参数的值。</span><span class="sxs-lookup"><span data-stu-id="834f7-465">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="834f7-466">在使用 Razor 语法，你使用 Visual Basic，你可以用于将参数传递给方法的两个选项：*位置参数*或*命名参数*。</span><span class="sxs-lookup"><span data-stu-id="834f7-466">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="834f7-467">若要调用的使用位置参数的方法，请在方法声明中指定严格顺序传递参数。</span><span class="sxs-lookup"><span data-stu-id="834f7-467">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="834f7-468">（你将通常知道此顺序通过阅读的方法的文档。）你必须遵循的顺序，并且你不能跳过任何参数&#8212;如果有必要，你将传递一个空字符串 (`""`) 则不具有的值的位置参数为 null。</span><span class="sxs-lookup"><span data-stu-id="834f7-468">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="834f7-469">下面的示例假定你有一个名为的文件夹*脚本*在网站上。</span><span class="sxs-lookup"><span data-stu-id="834f7-469">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="834f7-470">该代码调用`Request.MapPath`方法并传递正确的顺序中的三个参数的值。</span><span class="sxs-lookup"><span data-stu-id="834f7-470">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="834f7-471">然后，它将显示生成的映射的路径。</span><span class="sxs-lookup"><span data-stu-id="834f7-471">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="834f7-472">当存在多个参数的方法时，你可以将代码更简洁且更具可读性使用命名参数。</span><span class="sxs-lookup"><span data-stu-id="834f7-472">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="834f7-473">若要调用的方法使用命名的参数，指定参数名称后跟`:=`然后提供值。</span><span class="sxs-lookup"><span data-stu-id="834f7-473">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="834f7-474">命名参数的一个优点是，你可以按任何所需的顺序添加它们。</span><span class="sxs-lookup"><span data-stu-id="834f7-474">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="834f7-475">（一个缺点是方法调用不是为 compact。）</span><span class="sxs-lookup"><span data-stu-id="834f7-475">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="834f7-476">下面的示例调用按上面所述的相同方法，但使用命名参数提供的值：</span><span class="sxs-lookup"><span data-stu-id="834f7-476">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="834f7-477">如你所见，参数进行传递以不同的顺序。</span><span class="sxs-lookup"><span data-stu-id="834f7-477">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="834f7-478">但是，如果你运行前面的示例和此示例，它们将返回相同的值。</span><span class="sxs-lookup"><span data-stu-id="834f7-478">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="834f7-479">处理错误</span><span class="sxs-lookup"><span data-stu-id="834f7-479">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="834f7-480">Try Catch 语句</span><span class="sxs-lookup"><span data-stu-id="834f7-480">Try-Catch statements</span></span>

<span data-ttu-id="834f7-481">通常将在代码中可能会失败的原因，在你的控制范围具有语句。</span><span class="sxs-lookup"><span data-stu-id="834f7-481">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="834f7-482">例如：</span><span class="sxs-lookup"><span data-stu-id="834f7-482">For example:</span></span>

- <span data-ttu-id="834f7-483">如果你的代码尝试打开、 创建、 读取或写入文件时，可能会出现各种类型的错误。</span><span class="sxs-lookup"><span data-stu-id="834f7-483">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="834f7-484">所需的文件可能不存在，则可能锁定，代码可能不具有权限，依次类推。</span><span class="sxs-lookup"><span data-stu-id="834f7-484">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="834f7-485">同样，如果你的代码尝试更新数据库中的记录，可以有权限问题、 与数据库的连接可能会丢弃，要保存的数据可能无效，依次类推。</span><span class="sxs-lookup"><span data-stu-id="834f7-485">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="834f7-486">编程术语中，这些情况下调用*异常*。</span><span class="sxs-lookup"><span data-stu-id="834f7-486">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="834f7-487">如果你的代码遇到的异常，它会生成 （引发） 错误消息，它是，在最好的情况，令人讨厌的用户。</span><span class="sxs-lookup"><span data-stu-id="834f7-487">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="834f7-489">在情况下，你的代码可能会遇到的异常，并且为了避免这种类型的错误消息，你可以使用`Try/Catch`语句。</span><span class="sxs-lookup"><span data-stu-id="834f7-489">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="834f7-490">在`Try`语句，你将运行要检查的代码。</span><span class="sxs-lookup"><span data-stu-id="834f7-490">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="834f7-491">在一个或多个`Catch`语句，则你可以查看为特定可能发生的错误 （特定类型的异常）。</span><span class="sxs-lookup"><span data-stu-id="834f7-491">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="834f7-492">可以包括任意多个`Catch`语句作为你需要查找你要预测，将出现的错误。</span><span class="sxs-lookup"><span data-stu-id="834f7-492">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="834f7-493">我们建议你避免使用`Response.Redirect`中的方法`Try/Catch`语句，因为它可以在页中导致异常。</span><span class="sxs-lookup"><span data-stu-id="834f7-493">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>


<span data-ttu-id="834f7-494">下面的示例演示创建第一个请求上的文本文件，然后显示一个按钮，使用户能够打开文件的页。</span><span class="sxs-lookup"><span data-stu-id="834f7-494">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="834f7-495">该示例有意使用错误的文件名称，以便它会导致异常。</span><span class="sxs-lookup"><span data-stu-id="834f7-495">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="834f7-496">代码包含`Catch`两个可能的异常的语句： `FileNotFoundException`，就会出现此错误，文件名称是否和`DirectoryNotFoundException`，如果 ASP.NET 甚至找不到文件夹时会出现此情况。</span><span class="sxs-lookup"><span data-stu-id="834f7-496">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="834f7-497">（你可以取消注释在示例中的语句才能看到它时一切运行正常的运行。）</span><span class="sxs-lookup"><span data-stu-id="834f7-497">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="834f7-498">如果你的代码未处理异常，你会看到一个错误页面，如前面的屏幕快照。</span><span class="sxs-lookup"><span data-stu-id="834f7-498">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="834f7-499">但是，`Try/Catch`部分可帮助防止用户看到这些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="834f7-499">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="834f7-500">其他资源</span><span class="sxs-lookup"><span data-stu-id="834f7-500">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="834f7-501">参考文档</span><span class="sxs-lookup"><span data-stu-id="834f7-501">Reference Documentation</span></span>

- [<span data-ttu-id="834f7-502">ASP.NET 2.0</span><span class="sxs-lookup"><span data-stu-id="834f7-502">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="834f7-503">Visual Basic 语言</span><span class="sxs-lookup"><span data-stu-id="834f7-503">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
