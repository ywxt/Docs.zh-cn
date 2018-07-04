---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: 使用 Razor 语法 (Visual Basic 中) 的 ASP.NET Web 编程简介 |Microsoft Docs
author: tfitzmac
description: 本附录提供使用 ASP.NET Web pages 编程概述在 Visual Basic 中使用 Razor 语法。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/07/2014
ms.topic: article
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: d4be7e2ed1b847d8b4167872728815330dbfe432
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378736"
---
<a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="64754-103">使用 Razor 语法 (Visual Basic 中) 的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="64754-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>
====================
<span data-ttu-id="64754-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="64754-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="64754-105">本文提供了您的编程概述与 ASP.NET Web Pages 使用 Razor 语法和 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="64754-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="64754-106">ASP.NET 是 Microsoft 的技术，用于在 web 服务器上运行动态网页。</span><span class="sxs-lookup"><span data-stu-id="64754-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="64754-107">**你将了解**:</span><span class="sxs-lookup"><span data-stu-id="64754-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="64754-108">前 8 的编程的入门知识编程使用 Razor 语法的 ASP.NET Web Pages 的提示。</span><span class="sxs-lookup"><span data-stu-id="64754-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="64754-109">你将需要的基本编程概念。</span><span class="sxs-lookup"><span data-stu-id="64754-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="64754-110">ASP.NET 服务器代码和 Razor 语法是所有有关。</span><span class="sxs-lookup"><span data-stu-id="64754-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="64754-111">软件版本</span><span class="sxs-lookup"><span data-stu-id="64754-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="64754-112">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="64754-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="64754-113">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="64754-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="64754-114">使用 ASP.NET Web Pages with Razor syntax 的大多数示例使用 C#。</span><span class="sxs-lookup"><span data-stu-id="64754-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="64754-115">但 Razor 语法还支持 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="64754-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="64754-116">进行编程 ASP.NET 网页在 Visual Basic 中，创建与网页 *.vbhtml*文件扩展名，以及如何将 Visual Basic 代码。</span><span class="sxs-lookup"><span data-stu-id="64754-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="64754-117">本文提供使用 Visual Basic 语言和用于创建 ASP.NET 网页语法的概述。</span><span class="sxs-lookup"><span data-stu-id="64754-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="64754-118">Microsoft WebMatrix 的默认网站模板 (**面包店**，**照片库**，并**入门网站**等) 在 C# 和 Visual Basic 版本中可用。</span><span class="sxs-lookup"><span data-stu-id="64754-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="64754-119">可以安装 Visual Basic 的模板作为 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="64754-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="64754-120">名为的文件夹中的站点的根文件夹中安装网站模板*Microsoft 模板*。</span><span class="sxs-lookup"><span data-stu-id="64754-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>


## <a name="the-top-8-programming-tips"></a><span data-ttu-id="64754-121">最重要的 8 编程提示</span><span class="sxs-lookup"><span data-stu-id="64754-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="64754-122">本部分列出了绝对需要知道当你开始使用 Razor 语法的 ASP.NET 服务器代码编写的一些提示。</span><span class="sxs-lookup"><span data-stu-id="64754-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="64754-123">1.将代码添加到页使用 @ 字符</span><span class="sxs-lookup"><span data-stu-id="64754-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="64754-124">`@`字符开始内联表达式、 单语句块和多语句块：</span><span class="sxs-lookup"><span data-stu-id="64754-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="64754-125">在浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="64754-125">The result displayed in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="64754-127">**HTML 编码**</span><span class="sxs-lookup"><span data-stu-id="64754-127">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="64754-128">在页面中使用显示内容时`@`字符 ASP.NET HTML 编码输出，如前面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="64754-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="64754-129">它取代了 HTML 的保留的字符 (如`<`并`>`和`&`) 启用字符作为字符而不是解释为 HTML 标记或实体的网页中显示的代码。</span><span class="sxs-lookup"><span data-stu-id="64754-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="64754-130">无需 HTML 编码，即可在服务器代码中的输出可能不会显示正确，并可能会暴露于安全风险的页面。</span><span class="sxs-lookup"><span data-stu-id="64754-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="64754-131">如果你的目标是输出以标记形式呈现标记的 HTML 标记 (例如`<p></p>`段落或`<em></em>`来强调文本)，请参阅部分[组合文本、 标记和代码块中的代码](#BM_CombiningTextMarkupAndCode)这篇文章中更高版本。</span><span class="sxs-lookup"><span data-stu-id="64754-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="64754-132">你可以阅读更多有关中的 HTML 编码[使用 ASP.NET Web Pages 站点中的 HTML 窗体](https://go.microsoft.com/fwlink/?LinkId=202892)。</span><span class="sxs-lookup"><span data-stu-id="64754-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>


### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="64754-133">2.将代码的代码块...结束代码</span><span class="sxs-lookup"><span data-stu-id="64754-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="64754-134">代码块包含一个或多个代码语句，并且通过关键字括`Code`和`End Code`。</span><span class="sxs-lookup"><span data-stu-id="64754-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="64754-135">将左括号`Code`关键字后立即`@`字符&#8212;它们之间不能有空格。</span><span class="sxs-lookup"><span data-stu-id="64754-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="64754-136">在浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="64754-136">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="64754-138">3.在块中，您最终每个代码语句提供一个分行符</span><span class="sxs-lookup"><span data-stu-id="64754-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="64754-139">在 Visual Basic 代码块中，每个语句以换行符结尾。</span><span class="sxs-lookup"><span data-stu-id="64754-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="64754-140">（本文稍后将看到根据需要换行到多个行的冗长的代码语句的方法。）</span><span class="sxs-lookup"><span data-stu-id="64754-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="64754-141">4.使用变量来存储值</span><span class="sxs-lookup"><span data-stu-id="64754-141">4. You use variables to store values</span></span>

<span data-ttu-id="64754-142">可以存储中的值*变量*，包括字符串、 数字和日期等。创建一个新的变量使用`Dim`关键字。</span><span class="sxs-lookup"><span data-stu-id="64754-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="64754-143">可以直接在页中使用插入变量值`@`。</span><span class="sxs-lookup"><span data-stu-id="64754-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="64754-144">在浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="64754-144">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="64754-146">5.将文本字符串值括在双引号内</span><span class="sxs-lookup"><span data-stu-id="64754-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="64754-147">一个*字符串*是被视为文本字符序列。</span><span class="sxs-lookup"><span data-stu-id="64754-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="64754-148">若要指定一个字符串，则将其括在双引号内：</span><span class="sxs-lookup"><span data-stu-id="64754-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="64754-149">若要嵌入双引号引起来的字符串值中，插入两个双引号字符。</span><span class="sxs-lookup"><span data-stu-id="64754-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="64754-150">如果你想要出现一次页面输出中的双引号字符，作为其输入`""`中带引号的字符串，并将其作为输入在您希望其出现两次，如果`""""`中带引号的字符串。</span><span class="sxs-lookup"><span data-stu-id="64754-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="64754-151">在浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="64754-151">The result displayed in a browser:</span></span>

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="64754-153">6.Visual Basic 代码不区分大小写</span><span class="sxs-lookup"><span data-stu-id="64754-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="64754-154">Visual Basic 语言不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="64754-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="64754-155">编程关键字 (如`Dim`， `If`，并`True`) 和变量名称 (如`myString`，或`subTotal`) 可以在任何情况下编写。</span><span class="sxs-lookup"><span data-stu-id="64754-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="64754-156">以下代码行向变量分配值`lastname`使用小写名称，然后再将变量值输出到页面使用的是大写的名称。</span><span class="sxs-lookup"><span data-stu-id="64754-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="64754-157">在浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="64754-157">The result displayed in a browser:</span></span>

![vb 语法 5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="64754-159">7.大部分代码涉及到使用对象</span><span class="sxs-lookup"><span data-stu-id="64754-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="64754-160">对象表示的接口可以与编程&#8212;页、 文本框、 文件、 图像、 web 请求、 电子邮件、 客户记录 （数据库行），等等。对象具有描述其特征的属性&#8212;文本框对象具有`Text`属性，请求对象具有`Url`属性，电子邮件具有`From`属性，且客户对象都具有`FirstName`属性。</span><span class="sxs-lookup"><span data-stu-id="64754-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="64754-161">对象还具有方法&quot;谓词&quot;他们可以执行。</span><span class="sxs-lookup"><span data-stu-id="64754-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="64754-162">示例包括文件对象的`Save`方法中，映像对象的`Rotate`方法，并电子邮件对象的`Send`方法。</span><span class="sxs-lookup"><span data-stu-id="64754-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="64754-163">你经常要用`Request`对象，它为您提供了信息，如值的窗体字段 （文本框等），在页上进行浏览器的哪种类型的请求的 URL 的页面、 用户标识，等等。此示例演示如何访问的属性`Request`对象以及如何调用`MapPath`方法的`Request`对象，这将使您在服务器上的页面的绝对路径：</span><span class="sxs-lookup"><span data-stu-id="64754-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="64754-164">在浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="64754-164">The result displayed in a browser:</span></span>

![Razor Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="64754-166">8.可以编写代码来做出决策</span><span class="sxs-lookup"><span data-stu-id="64754-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="64754-167">动态网页的一项主要功能是，您可以确定要执行的操作根据条件。</span><span class="sxs-lookup"><span data-stu-id="64754-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="64754-168">若要执行此操作的最常见方法是使用`If`语句 (和可选`Else`语句)。</span><span class="sxs-lookup"><span data-stu-id="64754-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="64754-169">该语句`If IsPost`是一种编写的速记方法`If IsPost = True`。</span><span class="sxs-lookup"><span data-stu-id="64754-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="64754-170">连同`If`语句，有多种方法可以测试条件，重复的代码块，并且依此类推，这是本文后面所述。</span><span class="sxs-lookup"><span data-stu-id="64754-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="64754-171">在浏览器中显示的结果 (单击后**提交**):</span><span class="sxs-lookup"><span data-stu-id="64754-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> <span data-ttu-id="64754-173">**HTTP GET 和 POST 方法和 IsPost 属性**</span><span class="sxs-lookup"><span data-stu-id="64754-173">**HTTP GET and POST Methods and the IsPost Property**</span></span>
> 
> <span data-ttu-id="64754-174">用于网页 (HTTP) 的协议支持的方法非常有限的数量 (&quot;谓词&quot;)，用于向服务器发出请求。</span><span class="sxs-lookup"><span data-stu-id="64754-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="64754-175">两个最常见的是 GET、 用于读取某页和用于将网页提交的文章。</span><span class="sxs-lookup"><span data-stu-id="64754-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="64754-176">一般情况下，用户请求页面时，第一次请求页面时使用 GET。</span><span class="sxs-lookup"><span data-stu-id="64754-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="64754-177">如果用户在填写窗体，并单击**提交**，浏览器向服务器发出的 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="64754-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="64754-178">在 web 编程中，它通常是有助于了解是否请求页面时正在作为 GET 或 POST，以便您知道如何处理页面。</span><span class="sxs-lookup"><span data-stu-id="64754-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="64754-179">ASP.NET Web Pages 中，可以使用`IsPost`属性以确定请求是否为 GET 或 POST。</span><span class="sxs-lookup"><span data-stu-id="64754-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="64754-180">如果请求为 POST，`IsPost`属性将返回 true，然后你可以执行诸如读取窗体上的文本框的值。</span><span class="sxs-lookup"><span data-stu-id="64754-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="64754-181">你将看到许多示例演示如何处理以不同的方式具体取决于值页面`IsPost`。</span><span class="sxs-lookup"><span data-stu-id="64754-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>


## <a name="a-simple-code-example"></a><span data-ttu-id="64754-182">简单的代码示例</span><span class="sxs-lookup"><span data-stu-id="64754-182">A Simple Code Example</span></span>

<span data-ttu-id="64754-183">此过程演示如何创建一个页面，说明了基本的编程技术。</span><span class="sxs-lookup"><span data-stu-id="64754-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="64754-184">在示例中，您可以创建允许用户输入两个数字，然后将它们添加并显示结果的页面。</span><span class="sxs-lookup"><span data-stu-id="64754-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="64754-185">在编辑器中，创建一个新文件并将其命名*AddNumbers.vbhtml*。</span><span class="sxs-lookup"><span data-stu-id="64754-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="64754-186">将以下代码和标记复制到页中，替换已在页中的任何内容。</span><span class="sxs-lookup"><span data-stu-id="64754-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="64754-187">下面是您需要注意一些事项：</span><span class="sxs-lookup"><span data-stu-id="64754-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="64754-188">`@`字符在页中，启动第一个代码块，它位于之前`totalMessage`变量嵌入靠近底部。</span><span class="sxs-lookup"><span data-stu-id="64754-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="64754-189">在页面顶部块括在`Code...End Code`。</span><span class="sxs-lookup"><span data-stu-id="64754-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="64754-190">变量`total`， `num1`， `num2`，和`totalMessage`存储多个数字和字符串。</span><span class="sxs-lookup"><span data-stu-id="64754-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="64754-191">分配给的文字字符串值`totalMessage`变量是在双引号。</span><span class="sxs-lookup"><span data-stu-id="64754-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="64754-192">因为 Visual Basic 代码时不区分大小写`totalMessage`变量使用页面底部附近，其名称只需要匹配在页面顶部的变量声明的拼写是否正确。</span><span class="sxs-lookup"><span data-stu-id="64754-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="64754-193">大小写并不重要。</span><span class="sxs-lookup"><span data-stu-id="64754-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="64754-194">表达式`num1.AsInt()`  +  `num2.AsInt()`演示如何使用对象和方法。</span><span class="sxs-lookup"><span data-stu-id="64754-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="64754-195">`AsInt`上每个变量的方法将转换到整数 （整数），可以添加由用户输入的字符串。</span><span class="sxs-lookup"><span data-stu-id="64754-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="64754-196">`<form>`标记包含`method="post"`属性。</span><span class="sxs-lookup"><span data-stu-id="64754-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="64754-197">此步骤指定当用户单击**添加**，页面将发送到服务器使用 HTTP POST 方法。</span><span class="sxs-lookup"><span data-stu-id="64754-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="64754-198">提交页面时，代码`If IsPost`计算结果为 true，条件性代码运行时，显示数字相加的结果。</span><span class="sxs-lookup"><span data-stu-id="64754-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="64754-199">保存页面，并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="64754-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="64754-200">(请确保的页中选择**文件**工作区之前运行它。)输入两个整数，然后单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="64754-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="64754-202">Visual Basic 语言和语法</span><span class="sxs-lookup"><span data-stu-id="64754-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="64754-203">前面您了解了如何创建 ASP.NET web 页面中，以及如何可以将服务器代码添加到 HTML 标记的基本示例。</span><span class="sxs-lookup"><span data-stu-id="64754-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="64754-204">本文介绍使用 Visual Basic 来编写使用 Razor 语法的 ASP.NET 服务器代码的基础知识&#8212;，它是编程语言规则。</span><span class="sxs-lookup"><span data-stu-id="64754-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="64754-205">如果你是经验丰富的编程 （尤其是如果你使用过 C、 c + +、 C#、 Visual Basic 或 JavaScript），您现在阅读的许多并不陌生。</span><span class="sxs-lookup"><span data-stu-id="64754-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="64754-206">您可能需要仅与如何 WebMatrix 代码添加到标记中了解了相关 *.vbhtml*文件。</span><span class="sxs-lookup"><span data-stu-id="64754-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a>  <span data-ttu-id="64754-207">组合文本、 标记和代码块中的代码</span><span class="sxs-lookup"><span data-stu-id="64754-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="64754-208">在服务器代码块中，您通常需要输出文本和到页面的标记。</span><span class="sxs-lookup"><span data-stu-id="64754-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="64754-209">如果服务器代码块包含的文本的不是代码和，而是应呈现是，ASP.NET 将需要能够将该文本与代码区分开来。</span><span class="sxs-lookup"><span data-stu-id="64754-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="64754-210">有若干方法可实现此操作。</span><span class="sxs-lookup"><span data-stu-id="64754-210">There are several ways to do this.</span></span>

- <span data-ttu-id="64754-211">将文本括在类似的 HTML 块元素`<p></p>`或`<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="64754-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="64754-212">HTML 元素可以包括文本、 其他 HTML 元素和服务器代码表达式。</span><span class="sxs-lookup"><span data-stu-id="64754-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="64754-213">当 ASP.NET 发现 HTML 开始标记 (例如， `<p>`)，它会呈现所有内容的元素，并且作为其内容的浏览器 （和解析服务器代码表达式）。</span><span class="sxs-lookup"><span data-stu-id="64754-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="64754-214">使用`@:`运算符或`<text>`元素。</span><span class="sxs-lookup"><span data-stu-id="64754-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="64754-215">`@:`输出一行内容包含纯文本或 HTML 标记不匹配;`<text>`元素包含多行输出。</span><span class="sxs-lookup"><span data-stu-id="64754-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="64754-216">不想要作为输出的一部分呈现的 HTML 元素时，这些选项非常有用。</span><span class="sxs-lookup"><span data-stu-id="64754-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="64754-217">下面的示例重复前面的示例，但使用一对`<text>`标记括起要呈现的文本。</span><span class="sxs-lookup"><span data-stu-id="64754-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="64754-218">在以下示例中，`<text>`并`</text>`标记将三个行，都有一些非包含的文本和不匹配的 HTML 标记括起来 (`<br />`)，以及服务器代码和匹配的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="64754-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="64754-219">同样，还可以位于单独使用每个行`@:`运算符; 任一种方法的工作原理。</span><span class="sxs-lookup"><span data-stu-id="64754-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="64754-220">当输出文本，如本部分中所示&#8212;使用 HTML 元素，`@:`运算符，或`<text>`元素&#8212;ASP.NET 不会进行 HTML 编码输出。</span><span class="sxs-lookup"><span data-stu-id="64754-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="64754-221">(如前文所述，ASP.NET does 对服务器的代码表达式的前面使用的服务器代码块的输出进行编码`@`，本节中所述的特殊情况除外。)</span><span class="sxs-lookup"><span data-stu-id="64754-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="64754-222">Whitespace</span><span class="sxs-lookup"><span data-stu-id="64754-222">Whitespace</span></span>

<span data-ttu-id="64754-223">在语句中 （和字符串文字之外） 额外空间不会影响该语句：</span><span class="sxs-lookup"><span data-stu-id="64754-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="64754-224">将长语句分成多个行</span><span class="sxs-lookup"><span data-stu-id="64754-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="64754-225">您可以使用下划线字符长代码语句拆分为多个行`_`(在 Visual Basic 中的这种行为称为*继续符*) 之后的每一行代码。</span><span class="sxs-lookup"><span data-stu-id="64754-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="64754-226">若要中断语句到下一行上的，在行尾添加一个空格，然后继续符。</span><span class="sxs-lookup"><span data-stu-id="64754-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="64754-227">在下一行上继续该语句。</span><span class="sxs-lookup"><span data-stu-id="64754-227">Continue the statement on the next line.</span></span> <span data-ttu-id="64754-228">可以包装到尽可能多的行以提高可读性所需的语句。</span><span class="sxs-lookup"><span data-stu-id="64754-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="64754-229">以下语句是相同的：</span><span class="sxs-lookup"><span data-stu-id="64754-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="64754-230">但是，您将无法打包中间字符串文本行。</span><span class="sxs-lookup"><span data-stu-id="64754-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="64754-231">下面的示例不起作用：</span><span class="sxs-lookup"><span data-stu-id="64754-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="64754-232">若要组合的长字符串，如上面的代码中的多个行包装，您需要使用*串联运算符*(`&`)，您将会看到这篇文章中更高版本。</span><span class="sxs-lookup"><span data-stu-id="64754-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="64754-233">代码注释</span><span class="sxs-lookup"><span data-stu-id="64754-233">Code comments</span></span>

<span data-ttu-id="64754-234">注释使您可以保留为自己或他人的说明。</span><span class="sxs-lookup"><span data-stu-id="64754-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="64754-235">Razor 语法的注释都带有前缀`@*`开头和结尾`*@`。</span><span class="sxs-lookup"><span data-stu-id="64754-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="64754-236">在代码块中，您可以使用 Razor 语法注释，也可以使用普通的 Visual Basic 注释字符，这是一个单引号 (`'`) 作为每个行的前缀。</span><span class="sxs-lookup"><span data-stu-id="64754-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="64754-237">变量</span><span class="sxs-lookup"><span data-stu-id="64754-237">Variables</span></span>

<span data-ttu-id="64754-238">变量是命名的对象，用于存储数据。</span><span class="sxs-lookup"><span data-stu-id="64754-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="64754-239">您可以命名变量任何内容，但该名称必须以字母字符开头，不能包含空格或保留的字符。</span><span class="sxs-lookup"><span data-stu-id="64754-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="64754-240">在 Visual Basic 中，正如您看到的更早版本，并不重要的变量名称中的字母大小写。</span><span class="sxs-lookup"><span data-stu-id="64754-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="64754-241">变量和数据类型</span><span class="sxs-lookup"><span data-stu-id="64754-241">Variables and data types</span></span>

<span data-ttu-id="64754-242">变量可以具有特定的数据类型，指示在变量中存储的数据的种类。</span><span class="sxs-lookup"><span data-stu-id="64754-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="64754-243">你可以存储字符串值的字符串变量 (如&quot;Hello world&quot;)，存储 （如 3 或 79） 的整数值的整数变量和存储中以不同的格式 （如 2012 年 4 月 12 日或 2009 年 3 月的日期值的日期变量).</span><span class="sxs-lookup"><span data-stu-id="64754-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="64754-244">还有许多可以使用其他数据类型。</span><span class="sxs-lookup"><span data-stu-id="64754-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="64754-245">但是，您无需指定类型的变量。</span><span class="sxs-lookup"><span data-stu-id="64754-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="64754-246">在大多数情况下 ASP.NET 可找出基于变量中的数据的使用方式的类型。</span><span class="sxs-lookup"><span data-stu-id="64754-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="64754-247">（有时必须指定一个类型; 您将看到示例这为 true。）</span><span class="sxs-lookup"><span data-stu-id="64754-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="64754-248">若要声明变量时不指定类型的情况下，使用`Dim`加变量名称 (例如， `Dim myVar`)。</span><span class="sxs-lookup"><span data-stu-id="64754-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="64754-249">若要声明变量的类型时，使用`Dim`加变量名称后, 跟`As`，然后是类型名称 (例如， `Dim myVar As String`)。</span><span class="sxs-lookup"><span data-stu-id="64754-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="64754-250">下面的示例演示在网页中使用变量的某些内联表达式。</span><span class="sxs-lookup"><span data-stu-id="64754-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="64754-251">在浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="64754-251">The result displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="64754-253">转换和测试数据类型</span><span class="sxs-lookup"><span data-stu-id="64754-253">Converting and testing data types</span></span>

<span data-ttu-id="64754-254">尽管 ASP.NET 通常可以自动确定数据类型，但有时不能进行。</span><span class="sxs-lookup"><span data-stu-id="64754-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="64754-255">因此，您可能需要通过执行显式转换来帮助解决问题的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="64754-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="64754-256">即使您没有将类型转换，有时很有帮助进行测试以查看哪些类型的数据，可能正在处理。</span><span class="sxs-lookup"><span data-stu-id="64754-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="64754-257">最常见的情况是，您必须将字符串转换为另一种类型，如向整数或日期。</span><span class="sxs-lookup"><span data-stu-id="64754-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="64754-258">下面的示例演示一个典型的例子，必须将字符串转换为数字。</span><span class="sxs-lookup"><span data-stu-id="64754-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="64754-259">通常，用户输入到你以字符串形式提供。</span><span class="sxs-lookup"><span data-stu-id="64754-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="64754-260">即使系统已提示用户输入一个数字，并且即使在提交用户输入以及代码中读取时所输入的一个数字，数据的格式字符串。</span><span class="sxs-lookup"><span data-stu-id="64754-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="64754-261">因此，必须将字符串转换为数字。</span><span class="sxs-lookup"><span data-stu-id="64754-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="64754-262">在示例中，如果你尝试值执行算术运算，而不转换它们，出现以下错误结果，因为 ASP.NET 不能添加两个字符串：</span><span class="sxs-lookup"><span data-stu-id="64754-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="64754-263">若要将值转换为整数，则调用`AsInt`方法。</span><span class="sxs-lookup"><span data-stu-id="64754-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="64754-264">如果转换成功，您可以将数字。</span><span class="sxs-lookup"><span data-stu-id="64754-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="64754-265">下表列出了一些常见的转换和测试方法的变量。</span><span class="sxs-lookup"><span data-stu-id="64754-265">The following table lists some common conversion and test methods for variables.</span></span>


<span data-ttu-id="64754-266">::: 行:::::: 列:::<strong>方法</strong>::: 列线终止:::::: 列:::<strong>说明</strong>::: 列线终止:::::: 列:::<strong>示例</strong>::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-266">:::row::: :::column::: <strong>Method</strong> :::column-end::: :::column::: <strong>Description</strong> :::column-end::: :::column::: <strong>Example</strong> :::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-267">::: 行:::::: 列::: `AsInt(), IsInt()` ::: 列线终止:::::: 列::: 将表示为整数的字符串转换 (如&quot;593&quot;) 为整数。</span><span class="sxs-lookup"><span data-stu-id="64754-267">:::row::: :::column::: `AsInt(), IsInt()` :::column-end::: :::column::: Converts a string that represents a whole number (like &quot;593&quot;) to an integer.</span></span>
<span data-ttu-id="64754-268">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-268">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]</span></span>
    <span data-ttu-id="64754-269">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-269">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-270">::: 行:::::: 列::: `AsBool(), IsBool()` ::: 列线终止:::::: 列::: 转换字符串，如&quot;true&quot;或&quot;false&quot;为 Boolean 类型。</span><span class="sxs-lookup"><span data-stu-id="64754-270">:::row::: :::column::: `AsBool(), IsBool()` :::column-end::: :::column::: Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
<span data-ttu-id="64754-271">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-271">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]</span></span>
    <span data-ttu-id="64754-272">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-272">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-273">::: 行:::::: 列::: `AsFloat(), IsFloat()` ::: 列线终止:::::: 列::: 将具有类似的十进制值的字符串转换&quot;1.3&quot;或&quot;7.439&quot;为浮点数。</span><span class="sxs-lookup"><span data-stu-id="64754-273">:::row::: :::column::: `AsFloat(), IsFloat()` :::column-end::: :::column::: Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
<span data-ttu-id="64754-274">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-274">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]</span></span>
    <span data-ttu-id="64754-275">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-275">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-276">::: 行:::::: 列::: `AsDecimal(), IsDecimal()` ::: 列线终止:::::: 列::: 将具有类似的十进制值的字符串转换&quot;1.3&quot;或&quot;7.439&quot;为十进制数。</span><span class="sxs-lookup"><span data-stu-id="64754-276">:::row::: :::column::: `AsDecimal(), IsDecimal()` :::column-end::: :::column::: Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="64754-277">（在 ASP.NET 中，十进制数字是一个浮点数，更详细地说明。）::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-277">(In ASP.NET, a decimal number is more precise than a floating-point number.) :::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]</span></span>
    <span data-ttu-id="64754-278">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-278">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-279">::: 行:::::: 列::: `AsDateTime(), IsDateTime()` ::: 列线终止:::::: 列::: 将对 ASP.NET 表示的日期和时间值的字符串转换`DateTime`类型。</span><span class="sxs-lookup"><span data-stu-id="64754-279">:::row::: :::column::: `AsDateTime(), IsDateTime()` :::column-end::: :::column::: Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
<span data-ttu-id="64754-280">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-280">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]</span></span>
    <span data-ttu-id="64754-281">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-281">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-282">::: 行:::::: 列::: `ToString()` ::: 列线终止:::::: 列::: 任何其他数据类型转换的字符串。</span><span class="sxs-lookup"><span data-stu-id="64754-282">:::row::: :::column::: `ToString()` :::column-end::: :::column::: Converts any other data type to a string.</span></span>
<span data-ttu-id="64754-283">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-283">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]</span></span>
    <span data-ttu-id="64754-284">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-284">:::column-end::: :::row-end:::</span></span>


## <a name="operators"></a><span data-ttu-id="64754-285">运算符</span><span class="sxs-lookup"><span data-stu-id="64754-285">Operators</span></span>

<span data-ttu-id="64754-286">运算符是命令的关键字或告诉 ASP.NET 什么样来执行在表达式中的字符。</span><span class="sxs-lookup"><span data-stu-id="64754-286">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="64754-287">Visual Basic 支持许多运算符，但只需识别了一些以开始开发 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="64754-287">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="64754-288">下表总结了最常见的运算符。</span><span class="sxs-lookup"><span data-stu-id="64754-288">The following table summarizes the most common operators.</span></span>


<span data-ttu-id="64754-289">::: 行:::::: 列:::<strong>运算符</strong>::: 列线终止:::::: 列:::<strong>说明</strong>::: 列线终止:::::: 列:::<strong>示例</strong>::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-289">:::row::: :::column::: <strong>Operator</strong> :::column-end::: :::column::: <strong>Description</strong> :::column-end::: :::column::: <strong>Examples</strong> :::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-290">::: 行:::::: 列::: `+ - * /` ::: 列线终止:::::: 列::: 数值表达式中使用的数学运算符。</span><span class="sxs-lookup"><span data-stu-id="64754-290">:::row::: :::column::: `+ - * /` :::column-end::: :::column::: Math operators used in numerical expressions.</span></span>
<span data-ttu-id="64754-291">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-291">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]</span></span>
    <span data-ttu-id="64754-292">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-292">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-293">::: 行:::::: 列::: `=` ::: 列线终止:::::: 列::: 赋值和相等性。</span><span class="sxs-lookup"><span data-stu-id="64754-293">:::row::: :::column::: `=` :::column-end::: :::column::: Assignment and equality.</span></span> <span data-ttu-id="64754-294">根据上下文，将一条语句右侧的值分配给左侧和右侧，对象或检查值相等。</span><span class="sxs-lookup"><span data-stu-id="64754-294">Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.</span></span>
<span data-ttu-id="64754-295">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-295">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]</span></span>
    <span data-ttu-id="64754-296">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-296">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-297">::: 行:::::: 列::: `<>` ::: 列线终止:::::: 列::: 是否不相等。</span><span class="sxs-lookup"><span data-stu-id="64754-297">:::row::: :::column::: `<>` :::column-end::: :::column::: Inequality.</span></span> <span data-ttu-id="64754-298">返回`True`如果值不相等。</span><span class="sxs-lookup"><span data-stu-id="64754-298">Returns `True` if the values are not equal.</span></span>
<span data-ttu-id="64754-299">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-299">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]</span></span>
    <span data-ttu-id="64754-300">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-300">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-301">::: 行:::::: 列::: `< > <= >=` ::: 列线终止:::::: 列::: 小于、 大于、 小于或等于，以及大于或等于。</span><span class="sxs-lookup"><span data-stu-id="64754-301">:::row::: :::column::: `< > <= >=` :::column-end::: :::column::: Less than, greater than, less than or equal, and greater than or equal.</span></span>
<span data-ttu-id="64754-302">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-302">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]</span></span>
    <span data-ttu-id="64754-303">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-303">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-304">::: 行:::::: 列::: `&` ::: 列线终止:::::: 列::: 用于联接的字符串的串联。</span><span class="sxs-lookup"><span data-stu-id="64754-304">:::row::: :::column::: `&` :::column-end::: :::column::: Concatenation, which is used to join strings.</span></span>
<span data-ttu-id="64754-305">::: 列线终止:::::: 列::: [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]</span><span class="sxs-lookup"><span data-stu-id="64754-305">:::column-end::: :::column::: [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]</span></span>
    <span data-ttu-id="64754-306">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-306">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-307">::: 行:::::: 列::: `+= -=` ::: 列线终止:::::: 列::: 递增和递减运算符，从而添加，并且从变量 （分别） 减 1。</span><span class="sxs-lookup"><span data-stu-id="64754-307">:::row::: :::column::: `+= -=` :::column-end::: :::column::: The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
<span data-ttu-id="64754-308">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-308">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]</span></span>
    <span data-ttu-id="64754-309">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-309">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-310">::: 行:::::: 列::: `.` ::: 列线终止:::::: 列::: 圆点。</span><span class="sxs-lookup"><span data-stu-id="64754-310">:::row::: :::column::: `.` :::column-end::: :::column::: Dot.</span></span> <span data-ttu-id="64754-311">用于区分对象及其属性和方法。</span><span class="sxs-lookup"><span data-stu-id="64754-311">Used to distinguish objects and their properties and methods.</span></span>
<span data-ttu-id="64754-312">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-312">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]</span></span>
    <span data-ttu-id="64754-313">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-313">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-314">::: 行:::::: 列::: `()` ::: 列线终止:::::: 列::: 括号。</span><span class="sxs-lookup"><span data-stu-id="64754-314">:::row::: :::column::: `()` :::column-end::: :::column::: Parentheses.</span></span> <span data-ttu-id="64754-315">为组表达式，用于将参数传递给方法，并访问数组和集合的成员。</span><span class="sxs-lookup"><span data-stu-id="64754-315">Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.</span></span>
<span data-ttu-id="64754-316">::: 列线终止:::::: 列::: [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]</span><span class="sxs-lookup"><span data-stu-id="64754-316">:::column-end::: :::column::: [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]</span></span>
    <span data-ttu-id="64754-317">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-317">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-318">::: 行:::::: 列::: `Not` ::: 列线终止:::::: 列::: 不。</span><span class="sxs-lookup"><span data-stu-id="64754-318">:::row::: :::column::: `Not` :::column-end::: :::column::: Not.</span></span> <span data-ttu-id="64754-319">反转 true 值为 false，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="64754-319">Reverses a true value to false and vice versa.</span></span> <span data-ttu-id="64754-320">通常用作测试的速记方法`False`(即，对于不`True`)。</span><span class="sxs-lookup"><span data-stu-id="64754-320">Typically used as a shorthand way to test for `False` (that is, for not `True`).</span></span>
<span data-ttu-id="64754-321">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-321">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]</span></span>
    <span data-ttu-id="64754-322">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-322">:::column-end::: :::row-end:::</span></span>
* * *
<span data-ttu-id="64754-323">::: 行:::::: 列::: `AndAlso OrElse` ::: 列线终止:::::: 列::: 逻辑与和一起用于链接条件。</span><span class="sxs-lookup"><span data-stu-id="64754-323">:::row::: :::column::: `AndAlso OrElse` :::column-end::: :::column::: Logical AND and OR, which are used to link conditions together.</span></span>
<span data-ttu-id="64754-324">::: 列线终止:::::: 列::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]</span><span class="sxs-lookup"><span data-stu-id="64754-324">:::column-end::: :::column::: [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]</span></span>
    <span data-ttu-id="64754-325">::: 列线终止:::::: 行线终止:::</span><span class="sxs-lookup"><span data-stu-id="64754-325">:::column-end::: :::row-end:::</span></span>

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="64754-326">使用文件和代码中的文件夹路径</span><span class="sxs-lookup"><span data-stu-id="64754-326">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="64754-327">将在代码中经常处理的文件和文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="64754-327">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="64754-328">下面是用于网站的物理文件夹结构的示例，它可能会显示在开发计算机上：</span><span class="sxs-lookup"><span data-stu-id="64754-328">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="64754-329">下面是一些有关 Url 和路径的重要详细信息：</span><span class="sxs-lookup"><span data-stu-id="64754-329">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="64754-330">开始使用的域名的 URL (`http://www.example.com`) 或服务器名称 (`http://localhost`， `http://mycomputer`)。</span><span class="sxs-lookup"><span data-stu-id="64754-330">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="64754-331">URL 对应于主机计算机上的物理路径。</span><span class="sxs-lookup"><span data-stu-id="64754-331">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="64754-332">例如，`http://myserver`可能对应于文件夹*C:\websites\mywebsite*在服务器上。</span><span class="sxs-lookup"><span data-stu-id="64754-332">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="64754-333">虚拟路径是简写形式来表示在代码中的路径，而无需指定完整路径。</span><span class="sxs-lookup"><span data-stu-id="64754-333">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="64754-334">它包括遵守域或服务器名称的 URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="64754-334">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="64754-335">当你使用的虚拟路径时，可以而无需更新的路径，你的代码移动到不同的域或服务器。</span><span class="sxs-lookup"><span data-stu-id="64754-335">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="64754-336">下面是一个示例，帮助您了解的差异：</span><span class="sxs-lookup"><span data-stu-id="64754-336">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="64754-337">完整的 URL</span><span class="sxs-lookup"><span data-stu-id="64754-337">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="64754-338">服务器名称</span><span class="sxs-lookup"><span data-stu-id="64754-338">Server name</span></span> | <span data-ttu-id="64754-339">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="64754-339">*mycompanyserver*</span></span> |
| <span data-ttu-id="64754-340">虚拟路径</span><span class="sxs-lookup"><span data-stu-id="64754-340">Virtual path</span></span> | <span data-ttu-id="64754-341">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="64754-341">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="64754-342">物理路径</span><span class="sxs-lookup"><span data-stu-id="64754-342">Physical path</span></span> | <span data-ttu-id="64754-343">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="64754-343">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="64754-344">虚拟根目录为 /，就像在 c： 驱动器是 \。</span><span class="sxs-lookup"><span data-stu-id="64754-344">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="64754-345">（虚拟文件夹路径始终使用正斜杠。）文件夹的虚拟路径不需要作为物理文件夹; 具有相同的名称它可以是一个别名。</span><span class="sxs-lookup"><span data-stu-id="64754-345">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="64754-346">（在生产服务器上的虚拟路径很少与匹配确切的物理路径。）</span><span class="sxs-lookup"><span data-stu-id="64754-346">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="64754-347">代码中的文件和文件夹时，有时您需要引用的物理路径，有时也是虚拟路径，具体取决于您正在使用哪些对象。</span><span class="sxs-lookup"><span data-stu-id="64754-347">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="64754-348">ASP.NET 提供了这些工具用于在代码中的文件和文件夹路径：`Server.MapPath`方法，并`~`运算符和`Href`方法。</span><span class="sxs-lookup"><span data-stu-id="64754-348">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="64754-349">转换虚拟与物理路径： Server.MapPath 方法</span><span class="sxs-lookup"><span data-stu-id="64754-349">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="64754-350">`Server.MapPath`方法将为虚拟路径 (如 */default.cshtml*) 为绝对物理路径 (如*C:\WebSites\MyWebSiteFolder\default.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="64754-350">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="64754-351">每当您需要完整的物理路径使用此方法。</span><span class="sxs-lookup"><span data-stu-id="64754-351">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="64754-352">典型示例是要读取或写入文本文件或 web 服务器上的图像文件时。</span><span class="sxs-lookup"><span data-stu-id="64754-352">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="64754-353">通常不知道你的站点托管站点服务器上的绝对物理路径，因此此方法可以将路径转换您知道的虚拟路径 — 到您的服务器上的相应路径。</span><span class="sxs-lookup"><span data-stu-id="64754-353">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="64754-354">将虚拟路径传递给文件或文件夹的方法，并返回的物理路径：</span><span class="sxs-lookup"><span data-stu-id="64754-354">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="64754-355">引用虚拟根： ~ 运算符和 Href 方法</span><span class="sxs-lookup"><span data-stu-id="64754-355">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="64754-356">在中 *.cshtml*或 *.vbhtml*文件中，您可以引用虚拟根路径使用`~`运算符。</span><span class="sxs-lookup"><span data-stu-id="64754-356">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="64754-357">这是非常方便，因为您可以来回移动网页，在站点中，并且它们包含到其他页面的任何链接不会被破坏。</span><span class="sxs-lookup"><span data-stu-id="64754-357">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="64754-358">如果曾经将你的网站移动到另一个位置还有非常方便。</span><span class="sxs-lookup"><span data-stu-id="64754-358">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="64754-359">下面是一些可能的恶意活动：</span><span class="sxs-lookup"><span data-stu-id="64754-359">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="64754-360">如果网站`http://myserver/myapp`，下面是如何 ASP.NET 会将这些路径运行页面时：</span><span class="sxs-lookup"><span data-stu-id="64754-360">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="64754-361">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="64754-361">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="64754-362">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="64754-362">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="64754-363">（您实际上不会看到这些路径作为该变量的值，但像这就是它们的是，ASP.NET 会将路径）。</span><span class="sxs-lookup"><span data-stu-id="64754-363">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="64754-364">可以使用`~`运算符 （如上所述） 的服务器代码中和在标记中，像这样：</span><span class="sxs-lookup"><span data-stu-id="64754-364">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="64754-365">在标记中，您使用`~`运算符来创建资源，如图像文件、 其他网页和 CSS 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="64754-365">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="64754-366">页运行时，ASP.NET 页面 （代码和标记） 中查找并解决所有`~`引用到适当的路径。</span><span class="sxs-lookup"><span data-stu-id="64754-366">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="64754-367">条件逻辑和循环</span><span class="sxs-lookup"><span data-stu-id="64754-367">Conditional Logic and Loops</span></span>

<span data-ttu-id="64754-368">ASP.NET 服务器代码可以执行任务根据条件和编写代码重复特定次数，即代码的语句运行一个循环）。</span><span class="sxs-lookup"><span data-stu-id="64754-368">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="64754-369">测试条件</span><span class="sxs-lookup"><span data-stu-id="64754-369">Testing conditions</span></span>

<span data-ttu-id="64754-370">若要测试使用一个简单条件`If...Then`语句，它将返回`True`或`False`基于你指定的测试：</span><span class="sxs-lookup"><span data-stu-id="64754-370">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="64754-371">`If`关键字开始块。</span><span class="sxs-lookup"><span data-stu-id="64754-371">The `If` keyword starts a block.</span></span> <span data-ttu-id="64754-372">实际的测试 （条件） 遵循`If`关键字并返回 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="64754-372">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="64754-373">`If`语句结尾`Then`。</span><span class="sxs-lookup"><span data-stu-id="64754-373">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="64754-374">将运行测试为 true 的语句被括`If`和`End If`。</span><span class="sxs-lookup"><span data-stu-id="64754-374">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="64754-375">`If`语句中可以包含`Else`指定如果条件为 false，则运行语句块：</span><span class="sxs-lookup"><span data-stu-id="64754-375">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="64754-376">如果`If`语句将启动一个代码块，无需使用普通`Code...End Code`语句以包括的块。</span><span class="sxs-lookup"><span data-stu-id="64754-376">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="64754-377">可以仅添加`@`到块，并且它将起作用。</span><span class="sxs-lookup"><span data-stu-id="64754-377">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="64754-378">此方法适用于`If`以及其他 Visual Basic 编程关键字跟代码块，其中包括`For`， `For Each`， `Do While`，等等。</span><span class="sxs-lookup"><span data-stu-id="64754-378">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="64754-379">您可以添加多个条件使用一个或多个`ElseIf`基块：</span><span class="sxs-lookup"><span data-stu-id="64754-379">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="64754-380">在此示例中，如果第一个条件中`If`块不为 true，`ElseIf`条件进行检查。</span><span class="sxs-lookup"><span data-stu-id="64754-380">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="64754-381">如果满足该条件，则在语句`ElseIf`块执行。</span><span class="sxs-lookup"><span data-stu-id="64754-381">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="64754-382">如果没有条件为真中的语句`Else`块执行。</span><span class="sxs-lookup"><span data-stu-id="64754-382">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="64754-383">可以添加任意数量的`ElseIf`阻止，并使用然后关闭`Else`作为阻止&quot;其他所有内容&quot;条件。</span><span class="sxs-lookup"><span data-stu-id="64754-383">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="64754-384">若要测试大量的条件，请使用`Select Case`块：</span><span class="sxs-lookup"><span data-stu-id="64754-384">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="64754-385">要测试的值是在括号内 （在示例中，在工作日变量）。</span><span class="sxs-lookup"><span data-stu-id="64754-385">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="64754-386">每个单独测试使用`Case`列出了值的语句。</span><span class="sxs-lookup"><span data-stu-id="64754-386">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="64754-387">如果的值`Case`语句与测试值中的代码匹配`Case`执行块。</span><span class="sxs-lookup"><span data-stu-id="64754-387">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="64754-388">在浏览器中显示的最后两个条件块的结果：</span><span class="sxs-lookup"><span data-stu-id="64754-388">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="64754-390">循环的代码</span><span class="sxs-lookup"><span data-stu-id="64754-390">Looping code</span></span>

<span data-ttu-id="64754-391">通常需要反复运行相同的语句。</span><span class="sxs-lookup"><span data-stu-id="64754-391">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="64754-392">通过循环执行此操作。</span><span class="sxs-lookup"><span data-stu-id="64754-392">You do this by looping.</span></span> <span data-ttu-id="64754-393">例如，您通常运行同一个语句为每个项集合中的数据。</span><span class="sxs-lookup"><span data-stu-id="64754-393">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="64754-394">如果你确切地知道多少次循环，则可以使用`For`循环。</span><span class="sxs-lookup"><span data-stu-id="64754-394">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="64754-395">此种类型的循环非常适合计算或向下计数：</span><span class="sxs-lookup"><span data-stu-id="64754-395">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="64754-396">循环开头`For`关键字后, 跟三个元素：</span><span class="sxs-lookup"><span data-stu-id="64754-396">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="64754-397">后立即`For`语句中，您将计数器变量声明 (无需使用`Dim`)，然后指明范围，如`i = 10 to 20`。</span><span class="sxs-lookup"><span data-stu-id="64754-397">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="64754-398">这意味着变量`i`将从开始计数 10 并继续，直到它达到 20 （含）。</span><span class="sxs-lookup"><span data-stu-id="64754-398">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="64754-399">之间`For`和`Next`语句是在块的内容。</span><span class="sxs-lookup"><span data-stu-id="64754-399">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="64754-400">这可以包含一个或多个代码执行的语句每次循环。</span><span class="sxs-lookup"><span data-stu-id="64754-400">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="64754-401">`Next i`语句结束循环。</span><span class="sxs-lookup"><span data-stu-id="64754-401">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="64754-402">其递增的计数器，并启动循环的下一个迭代。</span><span class="sxs-lookup"><span data-stu-id="64754-402">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="64754-403">之间的代码行`For`和`Next`行包含每个迭代的循环运行的代码。</span><span class="sxs-lookup"><span data-stu-id="64754-403">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="64754-404">标记将创建一个新段落 (`<p>`元素) 每个时间，并将行添加到输出，显示的值 i （计数器）。</span><span class="sxs-lookup"><span data-stu-id="64754-404">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="64754-405">在运行此页时，该示例将创建显示每个行，该值指示项编号中的文本的输出的 11 行。</span><span class="sxs-lookup"><span data-stu-id="64754-405">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="64754-407">如果您正在使用集合或数组，通常使用`For Each`循环。</span><span class="sxs-lookup"><span data-stu-id="64754-407">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="64754-408">集合是一组类似对象和`For Each`循环可让你执行在集合中每一项任务。</span><span class="sxs-lookup"><span data-stu-id="64754-408">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="64754-409">此类型的循环非常方便的集合，因为与不同`For`循环中，您无需使计数器递增或设置的限制。</span><span class="sxs-lookup"><span data-stu-id="64754-409">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="64754-410">相反，`For Each`循环代码只需继续遍历该集合直到完成。</span><span class="sxs-lookup"><span data-stu-id="64754-410">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="64754-411">此示例将返回中的项`Request.ServerVariables`集合 （其中包含有关你的 web 服务器的信息）。</span><span class="sxs-lookup"><span data-stu-id="64754-411">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="64754-412">它使用`For Each`循环，以显示每个项的名称，通过创建一个新`<li>`HTML 项目符号列表中的元素。</span><span class="sxs-lookup"><span data-stu-id="64754-412">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="64754-413">`For Each`关键字后跟表示集合中的单个项的变量 (在示例中， `myItem`) 后, 跟`In`关键字后, 跟想要循环访问的集合。</span><span class="sxs-lookup"><span data-stu-id="64754-413">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="64754-414">正文中`For Each`循环中，您可以访问使用你之前声明的变量的当前项。</span><span class="sxs-lookup"><span data-stu-id="64754-414">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="64754-416">若要创建一个更通用的循环，请使用`Do While`语句：</span><span class="sxs-lookup"><span data-stu-id="64754-416">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="64754-417">此循环开头`Do While`关键字后, 跟的条件后, 跟要重复的块。</span><span class="sxs-lookup"><span data-stu-id="64754-417">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="64754-418">循环通常递增 （将添加到） 或递减 （从减） 的变量或用于计数的对象。</span><span class="sxs-lookup"><span data-stu-id="64754-418">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="64754-419">在示例中，`+=`运算符将添加 1 到变量的值每次循环运行的时。</span><span class="sxs-lookup"><span data-stu-id="64754-419">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="64754-420">(若要递减的向下计数的循环中的变量，将使用递减运算符`-=`。)</span><span class="sxs-lookup"><span data-stu-id="64754-420">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="64754-421">对象和集合</span><span class="sxs-lookup"><span data-stu-id="64754-421">Objects and Collections</span></span>

<span data-ttu-id="64754-422">在 ASP.NET 网站中几乎所有内容是一个对象，包括在 web 页面。</span><span class="sxs-lookup"><span data-stu-id="64754-422">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="64754-423">本部分介绍一些重要的对象，您将使用频繁地在代码中。</span><span class="sxs-lookup"><span data-stu-id="64754-423">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="64754-424">页对象</span><span class="sxs-lookup"><span data-stu-id="64754-424">Page objects</span></span>

<span data-ttu-id="64754-425">在 ASP.NET 中的最基本对象是页。</span><span class="sxs-lookup"><span data-stu-id="64754-425">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="64754-426">可以访问的不符合要求的任何对象而直接的 page 对象的属性。</span><span class="sxs-lookup"><span data-stu-id="64754-426">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="64754-427">以下代码获取页的文件路径，使用`Request`页的对象：</span><span class="sxs-lookup"><span data-stu-id="64754-427">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="64754-428">可以使用的属性`Page`对象以获得大量的信息，例如：</span><span class="sxs-lookup"><span data-stu-id="64754-428">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="64754-429">`Request`。</span><span class="sxs-lookup"><span data-stu-id="64754-429">`Request`.</span></span> <span data-ttu-id="64754-430">如您所见，这是信息的一系列有关当前请求，包括哪种类型的浏览器发出了请求、 页面、 用户标识，等等的 URL。</span><span class="sxs-lookup"><span data-stu-id="64754-430">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="64754-431">`Response`。</span><span class="sxs-lookup"><span data-stu-id="64754-431">`Response`.</span></span> <span data-ttu-id="64754-432">这是信息的有关在服务器代码完成运行时将发送到浏览器的响应 （页） 集合。</span><span class="sxs-lookup"><span data-stu-id="64754-432">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="64754-433">例如，此属性可用于将信息写入到响应。</span><span class="sxs-lookup"><span data-stu-id="64754-433">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="64754-434">集合对象 （数组和字典）</span><span class="sxs-lookup"><span data-stu-id="64754-434">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="64754-435">集合是一组相同的类型，如集合对象`Customer`数据库中的对象。</span><span class="sxs-lookup"><span data-stu-id="64754-435">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="64754-436">ASP.NET 包含多个内置集合，例如`Request.Files`集合。</span><span class="sxs-lookup"><span data-stu-id="64754-436">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="64754-437">通常将使用集合中的数据。</span><span class="sxs-lookup"><span data-stu-id="64754-437">You'll often work with data in collections.</span></span> <span data-ttu-id="64754-438">两个常见集合类型是*数组*并*字典*。</span><span class="sxs-lookup"><span data-stu-id="64754-438">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="64754-439">如果你想要存储类似项的集合，但不想创建一个单独的变量来保存每个项，数组非常有用：</span><span class="sxs-lookup"><span data-stu-id="64754-439">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="64754-440">对于数组，声明特定数据类型，如`String`， `Integer`，或`DateTime`。</span><span class="sxs-lookup"><span data-stu-id="64754-440">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="64754-441">若要指示该变量可以包含的数组，将括号添加到声明中的变量名称 (如`Dim myVar() As String`)。</span><span class="sxs-lookup"><span data-stu-id="64754-441">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="64754-442">您可以访问项在数组中使用它们的位置 （索引） 或通过使用`For Each`语句。</span><span class="sxs-lookup"><span data-stu-id="64754-442">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="64754-443">从零开始的数组索引为&#8212;，它是第一项是在位置 0，第二项是在位置 1，依此类推。</span><span class="sxs-lookup"><span data-stu-id="64754-443">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="64754-444">可以通过获取确定数组中的项的数目及其`Length`属性。</span><span class="sxs-lookup"><span data-stu-id="64754-444">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="64754-445">若要获取特定项的数组中的位置 (即，搜索数组)，使用`Array.IndexOf`方法。</span><span class="sxs-lookup"><span data-stu-id="64754-445">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="64754-446">此外可以执行诸如反向数组的内容 (`Array.Reverse`方法) 或对内容进行排序 (`Array.Sort`方法)。</span><span class="sxs-lookup"><span data-stu-id="64754-446">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="64754-447">在浏览器中显示的字符串数组代码的输出：</span><span class="sxs-lookup"><span data-stu-id="64754-447">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="64754-449">字典是键/值对的集合，其中提供密钥 （或名称） 设置或检索相应的值：</span><span class="sxs-lookup"><span data-stu-id="64754-449">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="64754-450">若要创建一个字典，请使用`New`关键字来指示要创建一个新`Dictionary`对象。</span><span class="sxs-lookup"><span data-stu-id="64754-450">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="64754-451">可以将字典分配给变量使用`Dim`关键字。</span><span class="sxs-lookup"><span data-stu-id="64754-451">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="64754-452">指示使用括号的字典中的项的数据类型 ( `( )` )。</span><span class="sxs-lookup"><span data-stu-id="64754-452">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="64754-453">在声明的末尾，必须添加另一对括号，因为这是实际创建一个新的字典的方法。</span><span class="sxs-lookup"><span data-stu-id="64754-453">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="64754-454">若要将项添加到字典中，可以调用`Add`字典变量或方法 (`myScores`这种情况下)，然后指定一个键和值。</span><span class="sxs-lookup"><span data-stu-id="64754-454">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="64754-455">或者，可以使用括号以指示该密钥，并执行简单的赋值，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="64754-455">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="64754-456">若要从字典中获取一个值，请在括号中指定密钥：</span><span class="sxs-lookup"><span data-stu-id="64754-456">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="64754-457">调用带参数的方法</span><span class="sxs-lookup"><span data-stu-id="64754-457">Calling Methods with Parameters</span></span>

<span data-ttu-id="64754-458">正如您看到本文前面部分，带有程序的对象具有方法。</span><span class="sxs-lookup"><span data-stu-id="64754-458">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="64754-459">例如，`Database`对象可能具有`Database.Connect`方法。</span><span class="sxs-lookup"><span data-stu-id="64754-459">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="64754-460">许多方法还具有一个或多个参数。</span><span class="sxs-lookup"><span data-stu-id="64754-460">Many methods also have one or more parameters.</span></span> <span data-ttu-id="64754-461">一个*参数*是向方法传递一个值以使该方法以完成其任务。</span><span class="sxs-lookup"><span data-stu-id="64754-461">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="64754-462">例如，查看有关声明`Request.MapPath`方法，它使用三个参数：</span><span class="sxs-lookup"><span data-stu-id="64754-462">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="64754-463">此方法相对应的服务器上的物理路径返回到指定的虚拟路径。</span><span class="sxs-lookup"><span data-stu-id="64754-463">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="64754-464">该方法的三个参数是`virtualPath`， `baseVirtualDir`，和`allowCrossAppMapping`。</span><span class="sxs-lookup"><span data-stu-id="64754-464">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="64754-465">（请注意，在声明中，所列的参数将接受的数据的数据类型）。当调用此方法时，必须提供所有三个参数的值。</span><span class="sxs-lookup"><span data-stu-id="64754-465">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="64754-466">当你使用 Visual Basic 使用 Razor 语法时，具有用于将参数传递给方法的两个选项：*位置参数*或*命名参数*。</span><span class="sxs-lookup"><span data-stu-id="64754-466">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="64754-467">若要调用使用位置参数的方法，请按严格顺序方法声明中指定的传递参数。</span><span class="sxs-lookup"><span data-stu-id="64754-467">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="64754-468">（您通常知道此顺序通过阅读文档的方法。）必须遵循的顺序，并且你不能跳过的任何参数&#8212;如果有必要，请传递了空字符串 (`""`) 或不具有的值的位置参数为 null。</span><span class="sxs-lookup"><span data-stu-id="64754-468">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="64754-469">下面的示例假定你有一个名为的文件夹*脚本*上你的网站。</span><span class="sxs-lookup"><span data-stu-id="64754-469">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="64754-470">该代码调用`Request.MapPath`方法，并传递正确的顺序中的三个参数的值。</span><span class="sxs-lookup"><span data-stu-id="64754-470">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="64754-471">然后，它显示生成映射的路径。</span><span class="sxs-lookup"><span data-stu-id="64754-471">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="64754-472">当有多个参数的方法时，您可以保留你的代码更简洁且更具可读性使用命名参数。</span><span class="sxs-lookup"><span data-stu-id="64754-472">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="64754-473">若要调用的方法使用命名的参数，指定参数名称后跟`:=`，然后提供值。</span><span class="sxs-lookup"><span data-stu-id="64754-473">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="64754-474">命名参数的一个优点是，可以将其添加所需的任何顺序。</span><span class="sxs-lookup"><span data-stu-id="64754-474">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="64754-475">（一个缺点是方法调用不是精简。）</span><span class="sxs-lookup"><span data-stu-id="64754-475">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="64754-476">下面的示例调用按上面所述的相同方法，但使用命名参数提供的值：</span><span class="sxs-lookup"><span data-stu-id="64754-476">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="64754-477">正如您所看到的会以不同的顺序传递参数。</span><span class="sxs-lookup"><span data-stu-id="64754-477">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="64754-478">但是，如果在运行上面的例子和此示例中，它们将返回相同的值。</span><span class="sxs-lookup"><span data-stu-id="64754-478">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="64754-479">处理错误</span><span class="sxs-lookup"><span data-stu-id="64754-479">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="64754-480">Try Catch 语句</span><span class="sxs-lookup"><span data-stu-id="64754-480">Try-Catch statements</span></span>

<span data-ttu-id="64754-481">通常必须在代码中可能会失败的原因有您的控制范围内的语句。</span><span class="sxs-lookup"><span data-stu-id="64754-481">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="64754-482">例如：</span><span class="sxs-lookup"><span data-stu-id="64754-482">For example:</span></span>

- <span data-ttu-id="64754-483">如果你的代码尝试打开、 创建、 读取或写入文件时，可能会出现各种类型的错误。</span><span class="sxs-lookup"><span data-stu-id="64754-483">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="64754-484">所需的文件可能不存在，则可能锁定，代码可能不具有的权限，等等。</span><span class="sxs-lookup"><span data-stu-id="64754-484">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="64754-485">同样，如果你的代码尝试更新数据库中的记录，可能出现权限问题、 与数据库的连接可能会断开，要保存的数据可能无效，依此类推。</span><span class="sxs-lookup"><span data-stu-id="64754-485">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="64754-486">在编程术语中，这些应用场景被称为*异常*。</span><span class="sxs-lookup"><span data-stu-id="64754-486">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="64754-487">如果你的代码遇到的异常，它将生成 （的引发操作） 错误消息，而该充其量，令人讨厌的用户。</span><span class="sxs-lookup"><span data-stu-id="64754-487">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="64754-489">在其中您的代码可能会发生异常的情况下，为了避免这种类型的错误消息，可以使用`Try/Catch`语句。</span><span class="sxs-lookup"><span data-stu-id="64754-489">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="64754-490">在`Try`语句中，您运行要检查的代码。</span><span class="sxs-lookup"><span data-stu-id="64754-490">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="64754-491">一个或多个`Catch`语句，则可以寻找特定于可能发生的错误 （特定类型的异常）。</span><span class="sxs-lookup"><span data-stu-id="64754-491">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="64754-492">可以包括任意多个`Catch`语句作为您需要查找的预期的错误。</span><span class="sxs-lookup"><span data-stu-id="64754-492">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="64754-493">我们建议您不要使用`Response.Redirect`中的方法`Try/Catch`语句，因为它可以在页面中导致异常。</span><span class="sxs-lookup"><span data-stu-id="64754-493">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>


<span data-ttu-id="64754-494">下面的示例显示了创建第一个请求上的文本文件，然后显示一个按钮，使用户可以打开文件的页面。</span><span class="sxs-lookup"><span data-stu-id="64754-494">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="64754-495">该示例故意使用错误的文件名称，以便它将导致异常。</span><span class="sxs-lookup"><span data-stu-id="64754-495">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="64754-496">该代码包括`Catch`两个可能的异常的语句： `FileNotFoundException`，就会出现此错误，文件名称是否和`DirectoryNotFoundException`，如果 ASP.NET 甚至找不到该文件夹将出现此情况。</span><span class="sxs-lookup"><span data-stu-id="64754-496">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="64754-497">（您可以取消注释该示例中的语句才能看到它时一切运行正常的运行。）</span><span class="sxs-lookup"><span data-stu-id="64754-497">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="64754-498">如果你的代码未处理异常，会看到一个错误页面，如前面的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="64754-498">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="64754-499">但是，`Try/Catch`部分可帮助防止用户看到这些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="64754-499">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="64754-500">其他资源</span><span class="sxs-lookup"><span data-stu-id="64754-500">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="64754-501">参考文档</span><span class="sxs-lookup"><span data-stu-id="64754-501">Reference Documentation</span></span>

- [<span data-ttu-id="64754-502">ASP.NET 2.0</span><span class="sxs-lookup"><span data-stu-id="64754-502">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="64754-503">Visual Basic 语言</span><span class="sxs-lookup"><span data-stu-id="64754-503">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
