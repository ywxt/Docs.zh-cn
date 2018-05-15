---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
title: 引入的 ASP.NET Web Pages-编程基础知识 |Microsoft 文档
author: tfitzmac
description: 本教程提供你的概述如何给程序中的 ASP.NET Web Pages 使用 Razor 语法。 你将了解： 基本 Razor 语法用于 pr...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/17/2015
ms.topic: article
ms.assetid: 7526ed45-a97d-4e8a-8301-01324ef0eff9
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
msc.type: authoredcontent
ms.openlocfilehash: 60115dd06a27bf856427953de29e993194afb991
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
<a name="introducing-aspnet-web-pages---programming-basics"></a><span data-ttu-id="3eeba-104">引入了 ASP.NET Web 页-编程基础知识</span><span class="sxs-lookup"><span data-stu-id="3eeba-104">Introducing ASP.NET Web Pages - Programming Basics</span></span>
====================
<span data-ttu-id="3eeba-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3eeba-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3eeba-106">本教程提供你的概述如何给程序中的 ASP.NET Web Pages 使用 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="3eeba-106">This tutorial gives you an overview of how to program in ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="3eeba-107">你将学习：</span><span class="sxs-lookup"><span data-stu-id="3eeba-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="3eeba-108">将用于编程中的 ASP.NET Web Pages 基本"Razor"语法。</span><span class="sxs-lookup"><span data-stu-id="3eeba-108">The basic "Razor" syntax that you use for programming in ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="3eeba-109">一些基本 C# 中，这是你将使用的编程语言。</span><span class="sxs-lookup"><span data-stu-id="3eeba-109">Some basic C#, which is the programming language you'll use.</span></span>
> - <span data-ttu-id="3eeba-110">网页的某些基本的编程概念。</span><span class="sxs-lookup"><span data-stu-id="3eeba-110">Some fundamental programming concepts for Web Pages.</span></span>
> - <span data-ttu-id="3eeba-111">如何安装程序包 （包含预构建的代码的组件），以使用你的网站。</span><span class="sxs-lookup"><span data-stu-id="3eeba-111">How to install packages (components that contain prebuilt code) to use with your site.</span></span>
> - <span data-ttu-id="3eeba-112">如何使用*帮助器*以执行常见编程任务。</span><span class="sxs-lookup"><span data-stu-id="3eeba-112">How to use *helpers* to perform common programming tasks.</span></span>
>   
> 
> <span data-ttu-id="3eeba-113">功能/技术讨论：</span><span class="sxs-lookup"><span data-stu-id="3eeba-113">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="3eeba-114">NuGet 和程序包管理器中。</span><span class="sxs-lookup"><span data-stu-id="3eeba-114">NuGet and the package manager.</span></span>
> - <span data-ttu-id="3eeba-115">`Gravatar`帮助器。</span><span class="sxs-lookup"><span data-stu-id="3eeba-115">The `Gravatar` helper.</span></span>


<span data-ttu-id="3eeba-116">本教程是主要中引入的编程语法，你将使用 ASP.NET Web 页的一个过程。</span><span class="sxs-lookup"><span data-stu-id="3eeba-116">This tutorial is primarily an exercise in introducing you to the programming syntax that you'll use for ASP.NET Web Pages.</span></span> <span data-ttu-id="3eeba-117">你将了解*Razor 语法*和用 C# 编写的代码编程语言。</span><span class="sxs-lookup"><span data-stu-id="3eeba-117">You'll learn about *Razor syntax* and code that's written in the C# programming language.</span></span> <span data-ttu-id="3eeba-118">你在前面的教程中; 此语法 glimpse在本教程中我们将介绍更多的语法。</span><span class="sxs-lookup"><span data-stu-id="3eeba-118">You got a glimpse of this syntax in the previous tutorial; in this tutorial we'll explain the syntax more.</span></span>

<span data-ttu-id="3eeba-119">我们保证本教程，包括编程你会看到在单个教程中，以及它是否是唯一教程最*仅*有关编程。</span><span class="sxs-lookup"><span data-stu-id="3eeba-119">We promise that this tutorial involves the most programming that you'll see in a single tutorial, and that it's the only tutorial that is *only* about programming.</span></span> <span data-ttu-id="3eeba-120">在此组中的其余教程，你将实际创建有趣事情的页。</span><span class="sxs-lookup"><span data-stu-id="3eeba-120">In the remaining tutorials in this set, you'll actually create pages that do interesting things.</span></span>

<span data-ttu-id="3eeba-121">你还将了解有关*帮助器*。</span><span class="sxs-lookup"><span data-stu-id="3eeba-121">You'll also learn about *helpers*.</span></span> <span data-ttu-id="3eeba-122">一个帮助程序是一个组件-打包向上的一段代码-，可以添加到页。</span><span class="sxs-lookup"><span data-stu-id="3eeba-122">A helper is a component — a packaged-up piece of code — that you can add to a page.</span></span> <span data-ttu-id="3eeba-123">帮助器执行工作，否则可能会需要很长时间或太复杂，手动执行。</span><span class="sxs-lookup"><span data-stu-id="3eeba-123">The helper performs work for you that otherwise might be tedious or complex to do by hand.</span></span>

## <a name="creating-a-page-to-play-with-razor"></a><span data-ttu-id="3eeba-124">创建页以玩 Razor</span><span class="sxs-lookup"><span data-stu-id="3eeba-124">Creating a Page to Play with Razor</span></span>

<span data-ttu-id="3eeba-125">在本节中你将玩有点 Razor 以便您可以获取的意义上的基本语法。</span><span class="sxs-lookup"><span data-stu-id="3eeba-125">In this section you'll play a bit with Razor so you can get a sense of the basic syntax.</span></span>

<span data-ttu-id="3eeba-126">如果它尚未运行，请启动 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="3eeba-126">Start WebMatrix if it's not already running.</span></span> <span data-ttu-id="3eeba-127">你将使用你在前面的教程中创建的网站 ([获取启动与网页](https://go.microsoft.com/fwlink/?LinkId=251578))。</span><span class="sxs-lookup"><span data-stu-id="3eeba-127">You'll use the website you created in the previous tutorial ([Getting Started With Web Pages](https://go.microsoft.com/fwlink/?LinkId=251578)).</span></span> <span data-ttu-id="3eeba-128">若要重新打开它，请单击**我的网站**选择**WebPageMovies**:</span><span class="sxs-lookup"><span data-stu-id="3eeba-128">To reopen it, click **My Sites** and choose **WebPageMovies**:</span></span>

![WebMatrix 开始屏幕显示打开的站点选项和我突出显示的网站](intro-to-web-pages-programming/_static/image1.png)

<span data-ttu-id="3eeba-130">选择**文件**工作区。</span><span class="sxs-lookup"><span data-stu-id="3eeba-130">Select the **Files** workspace.</span></span>

<span data-ttu-id="3eeba-131">在功能区中，单击**新建**来创建一个页面。</span><span class="sxs-lookup"><span data-stu-id="3eeba-131">In the ribbon, click **New** to create a page.</span></span> <span data-ttu-id="3eeba-132">选择**CSHTML**并命名新页*TestRazor.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="3eeba-132">Select **CSHTML** and name the new page *TestRazor.cshtml*.</span></span>

<span data-ttu-id="3eeba-133">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="3eeba-133">Click **OK**.</span></span>

<span data-ttu-id="3eeba-134">将以下内容复制到文件中，完全替换什么已存在。</span><span class="sxs-lookup"><span data-stu-id="3eeba-134">Copy the following into the file, completely replacing what's there already.</span></span>

> [!NOTE]
> <span data-ttu-id="3eeba-135">如果你放入页中，将示例中复制代码或标记，缩进和对齐方式可能不与本教程中的相同。</span><span class="sxs-lookup"><span data-stu-id="3eeba-135">When you copy code or markup from the examples into a page, the indentation and alignment might not be the same as in the tutorial.</span></span> <span data-ttu-id="3eeba-136">代码的运行方式，但并不影响缩进和对齐方式。</span><span class="sxs-lookup"><span data-stu-id="3eeba-136">Indentation and alignment don't affect how the code runs, though.</span></span>


[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample1.cshtml)]

## <a name="examining-the-example-page"></a><span data-ttu-id="3eeba-137">检查示例页面</span><span class="sxs-lookup"><span data-stu-id="3eeba-137">Examining the Example Page</span></span>

<span data-ttu-id="3eeba-138">你所看到的大多数是普通的 HTML。</span><span class="sxs-lookup"><span data-stu-id="3eeba-138">Most of what you see is ordinary HTML.</span></span> <span data-ttu-id="3eeba-139">但是，在顶部没有此代码块：</span><span class="sxs-lookup"><span data-stu-id="3eeba-139">However, at the top there's this code block:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample2.cshtml)]

<span data-ttu-id="3eeba-140">请注意有关此代码块的以下内容：</span><span class="sxs-lookup"><span data-stu-id="3eeba-140">Notice the following things about this code block:</span></span>

- <span data-ttu-id="3eeba-141">@ 字符是告诉 ASP.NET 的以下内容是 Razor 代码中，不 HTML。</span><span class="sxs-lookup"><span data-stu-id="3eeba-141">The @ character tells ASP.NET that what follows is Razor code, not HTML.</span></span> <span data-ttu-id="3eeba-142">ASP.NET 将处理后的所有内容 @ 字符如下代码，直至它再次运行到一些 HTML。</span><span class="sxs-lookup"><span data-stu-id="3eeba-142">ASP.NET will treat everything after the @ character as code until it runs into some HTML again.</span></span> <span data-ttu-id="3eeba-143">(在这种情况下的&lt;！DOCTYPE&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="3eeba-143">(In this case, that's the &lt;!DOCTYPE&gt; element.</span></span>
- <span data-ttu-id="3eeba-144">大括号 （{和}） 括起的 Razor 代码块，如果代码有多个行。</span><span class="sxs-lookup"><span data-stu-id="3eeba-144">The braces ( { and } ) enclose a block of Razor code if the code has more than one line.</span></span> <span data-ttu-id="3eeba-145">大括号告诉 ASP.NET，该块中的代码位置开始和结束。</span><span class="sxs-lookup"><span data-stu-id="3eeba-145">The braces tell ASP.NET where the code for that block starts and ends.</span></span>
- <span data-ttu-id="3eeba-146">/ / 字符标记注释-即，不会执行的代码的一部分。</span><span class="sxs-lookup"><span data-stu-id="3eeba-146">The // characters mark a comment — that is, a part of the code that won't execute.</span></span>
- <span data-ttu-id="3eeba-147">每个语句必须以分号 （;） 结尾。</span><span class="sxs-lookup"><span data-stu-id="3eeba-147">Each statement has to end with a semicolon (;).</span></span> <span data-ttu-id="3eeba-148">（不注释，但。）</span><span class="sxs-lookup"><span data-stu-id="3eeba-148">(Not comments, though.)</span></span>
- <span data-ttu-id="3eeba-149">你可以将值存储在*变量*，创建的 (*声明*) 与关键字差异</span><span class="sxs-lookup"><span data-stu-id="3eeba-149">You can store values in *variables*, which you create (*declare*) with the keyword var.</span></span> <span data-ttu-id="3eeba-150">在创建变量时，你赋予它一个名称，可以包含字母、 数字和下划线 (\_)。</span><span class="sxs-lookup"><span data-stu-id="3eeba-150">When you create a variable, you give it a name, which can include letters, numbers, and underscore (\_).</span></span> <span data-ttu-id="3eeba-151">变量名不能以数字开头，并且无法使用 （如 var) 编程关键字的名称。</span><span class="sxs-lookup"><span data-stu-id="3eeba-151">Variable names can't start with a number and can't use the name of a programming keyword (like var).</span></span>
- <span data-ttu-id="3eeba-152">将字符字符串 （例如"ASP.NET"和"网页"） 括在双引号中。</span><span class="sxs-lookup"><span data-stu-id="3eeba-152">You enclose character strings (like "ASP.NET" and "Web Pages") in quotation marks.</span></span> <span data-ttu-id="3eeba-153">（它们必须是两个双引号）。数字不是用引号引起来。</span><span class="sxs-lookup"><span data-stu-id="3eeba-153">(They must be double quotation marks.) Numbers are not in quotation marks.</span></span>
- <span data-ttu-id="3eeba-154">外部引号引起来的空白并不重要。</span><span class="sxs-lookup"><span data-stu-id="3eeba-154">Whitespace outside of quotation marks doesn't matter.</span></span> <span data-ttu-id="3eeba-155">分行符主要不重要;例外情况是，不能将用引号引起来的字符串拆分到行。</span><span class="sxs-lookup"><span data-stu-id="3eeba-155">Line breaks mostly don't matter; the exception is that you can't split a string in quotation marks across lines.</span></span> <span data-ttu-id="3eeba-156">缩进和对齐方式不重要。</span><span class="sxs-lookup"><span data-stu-id="3eeba-156">Indentation and alignment don't matter.</span></span>

<span data-ttu-id="3eeba-157">这一点不明显来自此示例是所有代码都是区分大小写。</span><span class="sxs-lookup"><span data-stu-id="3eeba-157">Something that's not obvious from this example is that all code is case sensitive.</span></span> <span data-ttu-id="3eeba-158">这意味着变量的参数是一个不同的变量比可能名参数的变量。</span><span class="sxs-lookup"><span data-stu-id="3eeba-158">This means that the variable TheSum is a different variable than variables that might be named theSum or thesum.</span></span> <span data-ttu-id="3eeba-159">同样，var 是一个关键字，但 Var 不是。</span><span class="sxs-lookup"><span data-stu-id="3eeba-159">Similarly, var is a keyword, but Var is not.</span></span>

### <a name="objects-and-properties-and-methods"></a><span data-ttu-id="3eeba-160">对象和属性和方法</span><span class="sxs-lookup"><span data-stu-id="3eeba-160">Objects and properties and methods</span></span>

<span data-ttu-id="3eeba-161">然后是 DateTime.Now 的表达式。</span><span class="sxs-lookup"><span data-stu-id="3eeba-161">Then there's the expression DateTime.Now.</span></span> <span data-ttu-id="3eeba-162">简单地说，DateTime 是*对象*。</span><span class="sxs-lookup"><span data-stu-id="3eeba-162">In simple terms, DateTime is an *object*.</span></span> <span data-ttu-id="3eeba-163">一个对象是，你可以使用编程 — 页、 文本框、 文件、 映像、 web 请求、 电子邮件、 客户记录，等等。对象具有一个或多个*属性*描述其特征。</span><span class="sxs-lookup"><span data-stu-id="3eeba-163">An object is a thing that you can program with—a page, a text box, a file, an image, a web request, an email message, a customer record, etc. Objects have one or more *properties* that describe their characteristics.</span></span> <span data-ttu-id="3eeba-164">文本框对象具有文本属性 （及其他）、 请求对象具有 Url 属性 （及其他）、 电子邮件，并且在 From 属性的收件人属性中，依次类推。</span><span class="sxs-lookup"><span data-stu-id="3eeba-164">A text box object has a Text property (among others), a request object has a Url property (and others), an email message has a From property and a To property, and so on.</span></span> <span data-ttu-id="3eeba-165">对象还具有*方法*是他们可以执行的"谓词"。</span><span class="sxs-lookup"><span data-stu-id="3eeba-165">Objects also have *methods* that are the "verbs" they can perform.</span></span> <span data-ttu-id="3eeba-166">你将对象大量使用。</span><span class="sxs-lookup"><span data-stu-id="3eeba-166">You'll be working with objects a lot.</span></span>

<span data-ttu-id="3eeba-167">如你所见示例中，日期时间将是可以程序日期和时间的对象。</span><span class="sxs-lookup"><span data-stu-id="3eeba-167">As you can see from the example, DateTime is an object that lets you program dates and times.</span></span> <span data-ttu-id="3eeba-168">它具有名为现在将返回当前日期和时间的属性。</span><span class="sxs-lookup"><span data-stu-id="3eeba-168">It has a property named Now that returns the current date and time.</span></span>

### <a name="using-code-to-render-markup-in-the-page"></a><span data-ttu-id="3eeba-169">使用代码来呈现页中标记</span><span class="sxs-lookup"><span data-stu-id="3eeba-169">Using code to render markup in the page</span></span>

<span data-ttu-id="3eeba-170">在页的正文中，注意以下事项：</span><span class="sxs-lookup"><span data-stu-id="3eeba-170">In the body of the page, notice the following:</span></span>

[!code-html[Main](intro-to-web-pages-programming/samples/sample3.html)]

<span data-ttu-id="3eeba-171">同样，@ 字符是告诉 ASP.NET 的以下该内容是代码，不 HTML。</span><span class="sxs-lookup"><span data-stu-id="3eeba-171">Again, the @ character tells ASP.NET that what follows is code, not HTML.</span></span> <span data-ttu-id="3eeba-172">在标记中你可以添加跟代码表达式，并且 ASP.NET 将在该点呈现该表达式的值。</span><span class="sxs-lookup"><span data-stu-id="3eeba-172">In the markup you can add @ followed by a code expression, and ASP.NET will render the value of that expression right at that point.</span></span> <span data-ttu-id="3eeba-173">在示例中，@a将呈现命名的变量的值是任何内容，@product呈现任何内容是在变量的命名产品中，依此类推。</span><span class="sxs-lookup"><span data-stu-id="3eeba-173">In the example, @a will render whatever the value is of the variable named a, @product renders whatever is in the variable named product, and so on.</span></span>

<span data-ttu-id="3eeba-174">你可以不局限于变量，但。</span><span class="sxs-lookup"><span data-stu-id="3eeba-174">You're not limited to variables, though.</span></span> <span data-ttu-id="3eeba-175">在某些情况下在这里，@ 字符之前表达式：</span><span class="sxs-lookup"><span data-stu-id="3eeba-175">In a few instances here, the @ character precedes an expression:</span></span>

- <span data-ttu-id="3eeba-176">@(\*b） 呈现变量中的所有内容的产品和 b。</span><span class="sxs-lookup"><span data-stu-id="3eeba-176">@(a\*b) renders the product of whatever is in the variables a and b.</span></span> <span data-ttu-id="3eeba-177">(\*运算符意味着乘法。)</span><span class="sxs-lookup"><span data-stu-id="3eeba-177">(The \* operator means multiplication.)</span></span>
- <span data-ttu-id="3eeba-178">@(技术 +""+ 产品) 将它们连接起来并之间添加空格之后呈现变量技术和产品中的值。</span><span class="sxs-lookup"><span data-stu-id="3eeba-178">@(technology + " " + product) renders the values in the variables technology and product after concatenating them and adding a space in between.</span></span> <span data-ttu-id="3eeba-179">为连接字符串的运算符 （+） 是与运算符相同的给出数字相加。</span><span class="sxs-lookup"><span data-stu-id="3eeba-179">The operator (+) for concatenating strings is the same as the operator for adding numbers.</span></span> <span data-ttu-id="3eeba-180">ASP.NET 通常可以判断计算机是否正在与数字或字符串并执行相应的操作使用 + 运算符。</span><span class="sxs-lookup"><span data-stu-id="3eeba-180">ASP.NET can usually tell whether you're working with numbers or with strings and does the right thing with the + operator.</span></span>
- <span data-ttu-id="3eeba-181">@Request.Url 呈现请求对象的 Url 属性。</span><span class="sxs-lookup"><span data-stu-id="3eeba-181">@Request.Url renders the Url property of the Request object.</span></span> <span data-ttu-id="3eeba-182">请求对象包含有关浏览器中，从当前请求的信息，这是当然的 Url 属性包含该当前请求的 URL。</span><span class="sxs-lookup"><span data-stu-id="3eeba-182">The Request object contains information about the current request from the browser, and of course the Url property contains the URL of that current request.</span></span>

<span data-ttu-id="3eeba-183">该示例还旨在演示你可以执行不同的方式工作。</span><span class="sxs-lookup"><span data-stu-id="3eeba-183">The example is also designed to show you that you can do work in different ways.</span></span> <span data-ttu-id="3eeba-184">你可以执行代码块顶部中的计算、 将结果放入变量中，和随后呈现标记中的变量。</span><span class="sxs-lookup"><span data-stu-id="3eeba-184">You can do calculations in the code block at the top, put the results into a variable, and then render the variable in markup.</span></span> <span data-ttu-id="3eeba-185">也可以执行在标记中的表达式权限中的计算。</span><span class="sxs-lookup"><span data-stu-id="3eeba-185">Or you can do calculations in an expression right in the markup.</span></span> <span data-ttu-id="3eeba-186">你使用的方法取决于你要执行的操作和，在某种程度上，在您自己的首选项。</span><span class="sxs-lookup"><span data-stu-id="3eeba-186">The approach you use depends on what you're doing and, to some extent, on your own preference.</span></span>

### <a name="seeing-the-code-in-action"></a><span data-ttu-id="3eeba-187">看到操作中的代码</span><span class="sxs-lookup"><span data-stu-id="3eeba-187">Seeing the code in action</span></span>

<span data-ttu-id="3eeba-188">右键单击该文件的名称，然后选择**在浏览器中启动**。</span><span class="sxs-lookup"><span data-stu-id="3eeba-188">Right-click the name of the file and then choose **Launch in browser**.</span></span> <span data-ttu-id="3eeba-189">你看到浏览器中使用的所有值和解决在页中的表达式中的页。</span><span class="sxs-lookup"><span data-stu-id="3eeba-189">You see the page in the browser with all the values and expressions resolved in the page.</span></span>

![浏览器中运行的 TestRazor 页](intro-to-web-pages-programming/_static/image2.png)

<span data-ttu-id="3eeba-191">查看浏览器中的源。</span><span class="sxs-lookup"><span data-stu-id="3eeba-191">Look at the source in the browser.</span></span>

![在浏览器中的测试 Razor 页面源文件](intro-to-web-pages-programming/_static/image3.png)

<span data-ttu-id="3eeba-193">正如预期从你在前面的教程中的体验，没有 Razor 代码是在页中。</span><span class="sxs-lookup"><span data-stu-id="3eeba-193">As you expect from your experience in the previous tutorial, none of the Razor code is in the page.</span></span> <span data-ttu-id="3eeba-194">你看到是实际显示的值。</span><span class="sxs-lookup"><span data-stu-id="3eeba-194">All you see are the actual display values.</span></span> <span data-ttu-id="3eeba-195">运行页面时，你实际上正在对内置 WebMatrix 的 web 服务器进行请求。</span><span class="sxs-lookup"><span data-stu-id="3eeba-195">When you run a page, you're actually making a request to the web server that's built into WebMatrix.</span></span> <span data-ttu-id="3eeba-196">当收到请求时，ASP.NET 解析所有的值和表达式，并将其值呈现到页。</span><span class="sxs-lookup"><span data-stu-id="3eeba-196">When the request is received, ASP.NET resolves all the values and expressions and renders their values into the page.</span></span> <span data-ttu-id="3eeba-197">它随后发送至浏览器的页面。</span><span class="sxs-lookup"><span data-stu-id="3eeba-197">It then sends the page to the browser.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="3eeba-198">**Razor 和 C#**</span><span class="sxs-lookup"><span data-stu-id="3eeba-198">**Razor and C#**</span></span>
> 
> <span data-ttu-id="3eeba-199">到目前为止我们讲到你正在使用 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="3eeba-199">Up to now we've said that you're working with Razor syntax.</span></span> <span data-ttu-id="3eeba-200">这是为 true，但它不是完成的情景。</span><span class="sxs-lookup"><span data-stu-id="3eeba-200">That's true, but it's not the complete story.</span></span> <span data-ttu-id="3eeba-201">要使用的实际编程语言称为*C#*。</span><span class="sxs-lookup"><span data-stu-id="3eeba-201">The actual programming language you're using is called *C#*.</span></span> <span data-ttu-id="3eeba-202">C# 通过十年前创建由 Microsoft 和已成为一种用于创建 Windows 应用程序的主编程语言。</span><span class="sxs-lookup"><span data-stu-id="3eeba-202">C# was created by Microsoft over a decade ago and has become one of the primary programming languages for creating Windows apps.</span></span> <span data-ttu-id="3eeba-203">你已了解有关如何命名变量以及如何创建语句的所有规则都都实际的 C# 语言的所有规则。</span><span class="sxs-lookup"><span data-stu-id="3eeba-203">All the rules you've seen about how to name a variable and how to create statements and so on are actually all rules of the C# language.</span></span>
> 
> <span data-ttu-id="3eeba-204">Razor 更具体地说就是指如何将此代码嵌入到页面的约定的少部分。</span><span class="sxs-lookup"><span data-stu-id="3eeba-204">Razor refers more specifically to the small set of conventions for how you embed this code into a page.</span></span> <span data-ttu-id="3eeba-205">例如，使用标记在页中的代码并使用的约定 @ {} 嵌入代码块是单页的 Razor 方面。</span><span class="sxs-lookup"><span data-stu-id="3eeba-205">For example, the convention of using @ to mark code in the page and using @{ } to embed a code block is the Razor aspect of a page.</span></span> <span data-ttu-id="3eeba-206">帮助器也被视为是 Razor 的一部分。</span><span class="sxs-lookup"><span data-stu-id="3eeba-206">Helpers are also considered to be part of Razor.</span></span> <span data-ttu-id="3eeba-207">在只需在 ASP.NET Web Pages 比多个位置使用 razor 语法。</span><span class="sxs-lookup"><span data-stu-id="3eeba-207">Razor syntax is used in more places than just in ASP.NET Web Pages.</span></span> <span data-ttu-id="3eeba-208">（例如，它用于 ASP.NET MVC 视图也。）</span><span class="sxs-lookup"><span data-stu-id="3eeba-208">(For example, it's used in ASP.NET MVC views as well.)</span></span>
> 
> <span data-ttu-id="3eeba-209">我们提到这是因为如果你寻找的编程 ASP.NET Web Pages 有关的信息时，你将找到大量对 Razor 的引用。</span><span class="sxs-lookup"><span data-stu-id="3eeba-209">We mention this because if you look for information about programming ASP.NET Web Pages, you'll find lots of references to Razor.</span></span> <span data-ttu-id="3eeba-210">但是，大量的这些引用不会应用到你要执行此操作并因此可能会造成混淆。</span><span class="sxs-lookup"><span data-stu-id="3eeba-210">However, a lot of those references don't apply to what you're doing and might therefore be confusing.</span></span> <span data-ttu-id="3eeba-211">和中的事实，许多编程问题实际上会成为有关使用 C# 或使用 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="3eeba-211">And in fact, many of your programming questions are really going to be about either working with C# or working with ASP.NET.</span></span> <span data-ttu-id="3eeba-212">因此如果你查看针对 Razor 有关的信息，您可能无法找到所需的答案。</span><span class="sxs-lookup"><span data-stu-id="3eeba-212">So if you look specifically for information about Razor, you might not find the answers you need.</span></span>


## <a name="adding-some-conditional-logic"></a><span data-ttu-id="3eeba-213">添加一些条件逻辑</span><span class="sxs-lookup"><span data-stu-id="3eeba-213">Adding Some Conditional Logic</span></span>

<span data-ttu-id="3eeba-214">有关在页中使用代码的强大功能之一是，您可以更改时会发生什么情况基于各种条件。</span><span class="sxs-lookup"><span data-stu-id="3eeba-214">One of the great features about using code in a page is that you can change what happens based on various conditions.</span></span> <span data-ttu-id="3eeba-215">在本教程的此部分中，你将要尝试一下更改页面中显示的内容的一些方法。</span><span class="sxs-lookup"><span data-stu-id="3eeba-215">In this part of the tutorial, you'll play around with some ways to change what's displayed in the page.</span></span>

<span data-ttu-id="3eeba-216">该示例将简单和专门设计，以便我们可以专注于条件逻辑的某种程度上。</span><span class="sxs-lookup"><span data-stu-id="3eeba-216">The example will be simple and somewhat contrived so that we can concentrate on the conditional logic.</span></span> <span data-ttu-id="3eeba-217">你将创建的页将执行此操作：</span><span class="sxs-lookup"><span data-stu-id="3eeba-217">The page you'll create will do this:</span></span>

- <span data-ttu-id="3eeba-218">根据是否第一次显示的页面或是否已单击按钮以提交页的页上显示不同的文本。</span><span class="sxs-lookup"><span data-stu-id="3eeba-218">Show different text on the page depending on whether it's the first time the page is displayed or whether you've clicked a button to submit the page.</span></span> <span data-ttu-id="3eeba-219">将第一个条件的测试。</span><span class="sxs-lookup"><span data-stu-id="3eeba-219">That will be the first conditional test.</span></span>
- <span data-ttu-id="3eeba-220">仅当某个值传递的 URL (http://...?show=true) 的查询字符串中显示消息。</span><span class="sxs-lookup"><span data-stu-id="3eeba-220">Display the message only if a certain value is passed in the query string of the URL (http://...?show=true).</span></span> <span data-ttu-id="3eeba-221">将第二个条件的测试。</span><span class="sxs-lookup"><span data-stu-id="3eeba-221">That will be the second conditional test.</span></span>

<span data-ttu-id="3eeba-222">在 WebMatrix 中，创建一个页面，并将其命名*TestRazorPart2.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="3eeba-222">In WebMatrix, create a page and name it *TestRazorPart2.cshtml*.</span></span> <span data-ttu-id="3eeba-223">(在功能区中，单击**新建**，选择**CSHTML**，作为文件名，然后单击**确定**。)</span><span class="sxs-lookup"><span data-stu-id="3eeba-223">(In the ribbon, click **New**, choose **CSHTML**, name the file, and then click **OK**.)</span></span>

<span data-ttu-id="3eeba-224">该页面的内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="3eeba-224">Replace the contents of that page with the following:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample4.cshtml)]

<span data-ttu-id="3eeba-225">在顶部的代码块初始化名为带有某些文本的消息的变量。</span><span class="sxs-lookup"><span data-stu-id="3eeba-225">The code block at the top initializes a variable named message with some text.</span></span> <span data-ttu-id="3eeba-226">在页的正文中，消息变量的内容显示在&lt;p&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="3eeba-226">In the body of the page, the contents of the message variable are displayed inside a &lt;p&gt; element.</span></span> <span data-ttu-id="3eeba-227">标记还包含&lt;输入&gt;元素以创建**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="3eeba-227">The markup also contains an &lt;input&gt; element to create a **Submit** button.</span></span>

<span data-ttu-id="3eeba-228">运行要查看其工作原理现在的页。</span><span class="sxs-lookup"><span data-stu-id="3eeba-228">Run the page to see how it works now.</span></span> <span data-ttu-id="3eeba-229">现在，它基本上是静态的页上，即使你单击**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="3eeba-229">For now, it's basically a static page, even if you click the **Submit** button.</span></span>

<span data-ttu-id="3eeba-230">返回到 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="3eeba-230">Go back to WebMatrix.</span></span> <span data-ttu-id="3eeba-231">在代码块中，添加以下突出显示的代码*后*初始化消息的行：</span><span class="sxs-lookup"><span data-stu-id="3eeba-231">Inside the code block, add the following highlighted code *after* the line that initializes message:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample5.cshtml?highlight=4-6)]

### <a name="the-if---block"></a><span data-ttu-id="3eeba-232">如果 {} 块</span><span class="sxs-lookup"><span data-stu-id="3eeba-232">The if { } block</span></span>

<span data-ttu-id="3eeba-233">你刚添加了 if 条件。</span><span class="sxs-lookup"><span data-stu-id="3eeba-233">What you just added was an if condition.</span></span> <span data-ttu-id="3eeba-234">在代码中，如果条件具有如下结构：</span><span class="sxs-lookup"><span data-stu-id="3eeba-234">In code, the if condition has a structure like this:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample6.cs)]

<span data-ttu-id="3eeba-235">要测试的条件位于括号中。</span><span class="sxs-lookup"><span data-stu-id="3eeba-235">The condition to test is in parentheses.</span></span> <span data-ttu-id="3eeba-236">它必须是一个值或一个表达式，返回 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="3eeba-236">It has to be a value or an expression that returns true or false.</span></span> <span data-ttu-id="3eeba-237">如果条件为 true，ASP.NET 将运行的语句或大括号内的语句。</span><span class="sxs-lookup"><span data-stu-id="3eeba-237">If the condition is true, ASP.NET runs the statement or statements that are inside the braces.</span></span> <span data-ttu-id="3eeba-238">(这种*然后*属于*如果那么*逻辑。)如果条件为 false，则跳过的代码块。</span><span class="sxs-lookup"><span data-stu-id="3eeba-238">(Those are the *then* part of the *if-then* logic.) If the condition is false, the block of code is skipped.</span></span>

<span data-ttu-id="3eeba-239">下面是可在 if 中测试的条件的几个示例语句：</span><span class="sxs-lookup"><span data-stu-id="3eeba-239">Here are a few examples of conditions you can test in an if statement:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample7.cs)]

<span data-ttu-id="3eeba-240">你可以通过使用测试变量对值或表达式<em>逻辑运算符</em>或<em>比较运算符</em>： 等于 （= =） 大于 (&gt;)，小于 (&lt;)，大于或等于 (&gt;=)，并且小于或等于 (&lt;=)。</span><span class="sxs-lookup"><span data-stu-id="3eeba-240">You can test variables against values or against expressions by using a <em>logical operator</em> or <em>comparison operator</em>: equal to (==), greater than (&gt;), less than (&lt;), greater than or equal to (&gt;=), and less than or equal to (&lt;=).</span></span> <span data-ttu-id="3eeba-241">！ = 运算符表示不等于-例如，如果 (！ = 0) 意味着<em>如果</em> <em>是否不等于 0</em>。</span><span class="sxs-lookup"><span data-stu-id="3eeba-241">The != operator means not equal to — for example, if(a != 0) means <em>if</em> <em>a</em><em>is not equal to 0</em>.</span></span>

> [!NOTE]
> <span data-ttu-id="3eeba-242">请确保你注意到等于 （= =） 比较运算符不是 = 的相同。</span><span class="sxs-lookup"><span data-stu-id="3eeba-242">Make sure you notice that the comparison operator for equals to (==) is not the same as =.</span></span> <span data-ttu-id="3eeba-243">= 运算符仅用于将值分配 (var = 2)。</span><span class="sxs-lookup"><span data-stu-id="3eeba-243">The = operator is used only to assign values (var a=2).</span></span> <span data-ttu-id="3eeba-244">如果混合这些运算符，您可以将要获取错误或你将获得一些奇怪的结果。</span><span class="sxs-lookup"><span data-stu-id="3eeba-244">If you mix these operators up, you'll either get an error or you'll get some strange results.</span></span>


<span data-ttu-id="3eeba-245">若要测试是否内容为 true，完整的语法是 if(IsDone == true)。</span><span class="sxs-lookup"><span data-stu-id="3eeba-245">To test whether something is true, the complete syntax is if(IsDone == true).</span></span> <span data-ttu-id="3eeba-246">但你也可以使用快捷 if(IsDone)。</span><span class="sxs-lookup"><span data-stu-id="3eeba-246">But you can also use the shortcut if(IsDone).</span></span> <span data-ttu-id="3eeba-247">如果没有任何比较运算符，ASP.NET 将假定您要测试为 true。</span><span class="sxs-lookup"><span data-stu-id="3eeba-247">If there's no comparison operator, ASP.NET assumes that you're testing for true.</span></span>

<span data-ttu-id="3eeba-248">！</span><span class="sxs-lookup"><span data-stu-id="3eeba-248">The !</span></span> <span data-ttu-id="3eeba-249">运算符本身意味着逻辑非。</span><span class="sxs-lookup"><span data-stu-id="3eeba-249">operator by itself means a logical NOT.</span></span> <span data-ttu-id="3eeba-250">例如，条件 if （！IsPost) 意味着*若 IsPost 不为 true*。</span><span class="sxs-lookup"><span data-stu-id="3eeba-250">For example, the condition if(!IsPost) means *if IsPost is not true*.</span></span>

<span data-ttu-id="3eeba-251">你可以通过使用逻辑 AND 组合条件 (&amp; &amp;运算符) 或逻辑 OR (| | 运算符)。</span><span class="sxs-lookup"><span data-stu-id="3eeba-251">You can combine conditions by using a logical AND (&amp;&amp; operator) or logical OR (|| operator).</span></span> <span data-ttu-id="3eeba-252">例如，如果的最后一个条件在前面的示例表示*如果 FileProcessingIsDone 未设置为 true AND displayMessage 设置为 false*。</span><span class="sxs-lookup"><span data-stu-id="3eeba-252">For example, the last of the if conditions in the preceding examples means *if FileProcessingIsDone is not set to true AND displayMessage is set to false*.</span></span>

### <a name="the-else-block"></a><span data-ttu-id="3eeba-253">Else 块</span><span class="sxs-lookup"><span data-stu-id="3eeba-253">The else block</span></span>

<span data-ttu-id="3eeba-254">一个有关如果的最后一件事情块： 如果块可以跟到 else 块中。</span><span class="sxs-lookup"><span data-stu-id="3eeba-254">One final thing about if blocks: an if block can be followed by an else block.</span></span> <span data-ttu-id="3eeba-255">到 else 块中非常有用，您需要在条件为 false 时执行不同的代码。</span><span class="sxs-lookup"><span data-stu-id="3eeba-255">An else block is useful is you have to execute different code when the condition is false.</span></span> <span data-ttu-id="3eeba-256">下面是一个简单的示例：</span><span class="sxs-lookup"><span data-stu-id="3eeba-256">Here's a simple example:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample8.cs)]

<span data-ttu-id="3eeba-257">在更高版本，使用到 else 块中也是有用本系列教程中，你将看到一些示例。</span><span class="sxs-lookup"><span data-stu-id="3eeba-257">You'll see some examples in later tutorials in this series where using an else block is useful.</span></span>

### <a name="testing-whether-the-request-is-a-submit-post"></a><span data-ttu-id="3eeba-258">测试是否请求是提交 (post)</span><span class="sxs-lookup"><span data-stu-id="3eeba-258">Testing whether the request is a submit (post)</span></span>

<span data-ttu-id="3eeba-259">还有更多，但我们回过头的示例中，它具有条件 if(IsPost) {...}。</span><span class="sxs-lookup"><span data-stu-id="3eeba-259">There's more, but let's get back to the example, which has the condition if(IsPost){ ... }.</span></span> <span data-ttu-id="3eeba-260">IsPost 是实际当前页的属性。</span><span class="sxs-lookup"><span data-stu-id="3eeba-260">IsPost is actually a property of the current page.</span></span> <span data-ttu-id="3eeba-261">第一次请求页时，IsPost 返回 false。</span><span class="sxs-lookup"><span data-stu-id="3eeba-261">The first time the page is requested, IsPost returns false.</span></span> <span data-ttu-id="3eeba-262">但是，如果你单击一个按钮，或以其他方式提交页 — 你发布的即-IsPost，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="3eeba-262">However, if you click a button or otherwise submit the page — that is, you post it — IsPost returns true.</span></span> <span data-ttu-id="3eeba-263">因此 IsPost 使你能够确定是否正在处理与表单提交。</span><span class="sxs-lookup"><span data-stu-id="3eeba-263">So IsPost lets you determine whether you're dealing with a form submission.</span></span> <span data-ttu-id="3eeba-264">（根据 HTTP 谓词 GET 操作时，该请求是否 IsPost 返回 false。</span><span class="sxs-lookup"><span data-stu-id="3eeba-264">(In terms of HTTP verbs, if the request is a GET operation, IsPost returns false.</span></span> <span data-ttu-id="3eeba-265">如果请求是 POST 操作，IsPost 返回 true。）在后面的教程中，您将可以使用输入的表单，此测试变得特别有用。</span><span class="sxs-lookup"><span data-stu-id="3eeba-265">If the request is a POST operation, IsPost returns true.) In a later tutorial you'll work with input forms, where this test becomes particularly useful.</span></span>

<span data-ttu-id="3eeba-266">运行页面。</span><span class="sxs-lookup"><span data-stu-id="3eeba-266">Run the page.</span></span> <span data-ttu-id="3eeba-267">因为这是首次在请求页中，你将看到"这是在首次已请求页"。</span><span class="sxs-lookup"><span data-stu-id="3eeba-267">Because this is the first time you're requested the page, you see "This is the first time you've requested the page".</span></span> <span data-ttu-id="3eeba-268">该字符串将是初始化消息变量的值。</span><span class="sxs-lookup"><span data-stu-id="3eeba-268">That string is the value that you initialized the message variable to.</span></span> <span data-ttu-id="3eeba-269">没有一 if(IsPost) 项测试，但，返回 false 时间，因此块置于 if 的代码不运行。</span><span class="sxs-lookup"><span data-stu-id="3eeba-269">There's an if(IsPost) test, but that returns false at the moment, so the code inside the if block doesn't run.</span></span>

<span data-ttu-id="3eeba-270">单击**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="3eeba-270">Click the **Submit** button.</span></span> <span data-ttu-id="3eeba-271">再次请求该页。</span><span class="sxs-lookup"><span data-stu-id="3eeba-271">The page is requested again.</span></span> <span data-ttu-id="3eeba-272">为之前，消息变量设置为"这是首次..."。</span><span class="sxs-lookup"><span data-stu-id="3eeba-272">As before, the message variable is set to "This is the first time ...".</span></span> <span data-ttu-id="3eeba-273">但这一次，测试 if(IsPost)，则返回 true，因此如果内的代码块将运行。</span><span class="sxs-lookup"><span data-stu-id="3eeba-273">But this time, the test if(IsPost) returns true, so the code inside the if block runs.</span></span> <span data-ttu-id="3eeba-274">代码更改为不同的值，这是在标记中呈现的内容的消息变量的值。</span><span class="sxs-lookup"><span data-stu-id="3eeba-274">The code changes the value of the message variable to a different value, which is what's rendered in the markup.</span></span>

<span data-ttu-id="3eeba-275">现在添加 if 标记中的条件。</span><span class="sxs-lookup"><span data-stu-id="3eeba-275">Now add an if condition in the markup.</span></span> <span data-ttu-id="3eeba-276">下面&lt;p&gt;包含的元素**提交**按钮，添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="3eeba-276">Below the &lt;p&gt; element that contains the **Submit** button, add the following markup:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample9.cshtml)]

<span data-ttu-id="3eeba-277">你要添加标记内的代码，因此你必须首先@。</span><span class="sxs-lookup"><span data-stu-id="3eeba-277">You're adding code inside the markup, so you have to start with @.</span></span> <span data-ttu-id="3eeba-278">If 则类似于你前面添加的代码块中的测试。</span><span class="sxs-lookup"><span data-stu-id="3eeba-278">Then there's an if test similar to the one you added earlier up in the code block.</span></span> <span data-ttu-id="3eeba-279">在大括号，不过，你要添加普通 HTML-至少，它是普通，直到到达@DateTime.Now。</span><span class="sxs-lookup"><span data-stu-id="3eeba-279">Inside the braces, though, you're adding ordinary HTML — at least, it's ordinary until it gets to @DateTime.Now.</span></span> <span data-ttu-id="3eeba-280">这是另一小段 Razor 代码，因此再次你需要添加前面遮挡它。</span><span class="sxs-lookup"><span data-stu-id="3eeba-280">This is another little bit of Razor code, so again you have to add @ in front of it.</span></span>

<span data-ttu-id="3eeba-281">这里的要点是，如果你可以添加在条件块的代码在顶部和标记中。</span><span class="sxs-lookup"><span data-stu-id="3eeba-281">The point here is that you can add if conditions in both the code block at the top and in the markup.</span></span> <span data-ttu-id="3eeba-282">如果使用 if 页上，在该块内的行的正文中的条件可以是标记或代码。</span><span class="sxs-lookup"><span data-stu-id="3eeba-282">If you use an if condition in the body of the page, the lines inside the block can be markup or code.</span></span> <span data-ttu-id="3eeba-283">在这种情况下，并且因为每当混合使用标记和代码，则为 true，你必须使用 @ 以使它清楚地了解 ASP.NET 代码。</span><span class="sxs-lookup"><span data-stu-id="3eeba-283">In that case, and as is true anytime you mix markup and code, you have to use @ to make it clear to ASP.NET where the code is.</span></span>

<span data-ttu-id="3eeba-284">运行页面并单击**提交**。</span><span class="sxs-lookup"><span data-stu-id="3eeba-284">Run the page and click **Submit**.</span></span> <span data-ttu-id="3eeba-285">这次你不仅看到不同的消息时提交 （"现在你已提交..."），但看到列出的日期和时间的新消息。</span><span class="sxs-lookup"><span data-stu-id="3eeba-285">This time you not only see a different message when you submit ("Now you've submitted ..."), but you see a new message that lists the date and time.</span></span>

![提交后显示的时间戳与浏览器中运行的测试 Razor 2 页](intro-to-web-pages-programming/_static/image4.png)

### <a name="testing-the-value-of-a-query-string"></a><span data-ttu-id="3eeba-287">测试查询字符串的值</span><span class="sxs-lookup"><span data-stu-id="3eeba-287">Testing the value of a query string</span></span>

<span data-ttu-id="3eeba-288">一个多个测试。</span><span class="sxs-lookup"><span data-stu-id="3eeba-288">One more test.</span></span> <span data-ttu-id="3eeba-289">此时，你将添加 if 测试某个值的块名为可能传递给查询字符串中的显示。</span><span class="sxs-lookup"><span data-stu-id="3eeba-289">This time, you'll add an if block that tests a value named show that might be passed in the query string.</span></span> <span data-ttu-id="3eeba-290">(如下所示： `http://localhost:43097/TestRazorPart2.cshtml?show=true`)，以便消息你已显示，将更改的页 （"这是首次..."，等等） 如果显示的值为 true，则仅显示。</span><span class="sxs-lookup"><span data-stu-id="3eeba-290">(Like this: `http://localhost:43097/TestRazorPart2.cshtml?show=true`) You'll change the page so that the message you've been displaying ("This is the first time ...", etc.) is only displayed if the value of show is true.</span></span>

<span data-ttu-id="3eeba-291">在底部 （但内部） 在代码块中的页上，顶部添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="3eeba-291">At the bottom (but inside) the code block at the top of the page, add the following:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample10.cs)]

<span data-ttu-id="3eeba-292">完整的代码块现在看起来像下面的示例。</span><span class="sxs-lookup"><span data-stu-id="3eeba-292">The complete code block now look like the following example.</span></span> <span data-ttu-id="3eeba-293">（请记住，当你将代码复制到你的页面，缩进显示可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="3eeba-293">(Remember that when you copy the code into your page, the indentation might look different.</span></span> <span data-ttu-id="3eeba-294">但是，不会影响代码的运行方式。）</span><span class="sxs-lookup"><span data-stu-id="3eeba-294">But that doesn't affect how the code runs.)</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample11.cshtml)]

<span data-ttu-id="3eeba-295">新代码块中的初始化一个名为分隔开为 false 的多个变量。</span><span class="sxs-lookup"><span data-stu-id="3eeba-295">The new code in the block initializes a variable named showMessage to false.</span></span> <span data-ttu-id="3eeba-296">它，则执行 if 测试查找查询字符串中的值。</span><span class="sxs-lookup"><span data-stu-id="3eeba-296">It then does an if test to look for a value in the query string.</span></span> <span data-ttu-id="3eeba-297">当您第一次请求的页面时，它具有与此类似的 URL:</span><span class="sxs-lookup"><span data-stu-id="3eeba-297">When you first request the page, it has a URL like this one:</span></span>

`http://localhost:43097/TestRazorPart2.cshtml`

<span data-ttu-id="3eeba-298">代码将确定 URL 是否包含名为查询字符串，如 URL 的此版本中显示的变量：</span><span class="sxs-lookup"><span data-stu-id="3eeba-298">The code determines whether the URL contains a variable named show in the query string, like this version of the URL:</span></span>

<span data-ttu-id="3eeba-299">`http://localhost:43097/TestRazorPart2.cshtml`？ 显示 = true</span><span class="sxs-lookup"><span data-stu-id="3eeba-299">`http://localhost:43097/TestRazorPart2.cshtml`?show=true</span></span>

<span data-ttu-id="3eeba-300">测试本身来看待请求对象的查询字符串属性。</span><span class="sxs-lookup"><span data-stu-id="3eeba-300">The test itself looks at the QueryString property of the Request object.</span></span> <span data-ttu-id="3eeba-301">如果查询字符串包含项命名的显示，并且该项设置为 true，如果块运行，并将分隔开多个变量设置为 true。</span><span class="sxs-lookup"><span data-stu-id="3eeba-301">If the query string contains an item named show, and if that item is set to true, the if block runs and sets the showMessage variable to true.</span></span>

<span data-ttu-id="3eeba-302">没有了技巧，可以在这里，你可以看到。</span><span class="sxs-lookup"><span data-stu-id="3eeba-302">There's a trick here, as you can see.</span></span> <span data-ttu-id="3eeba-303">规定的名称，查询字符串是一个字符串。</span><span class="sxs-lookup"><span data-stu-id="3eeba-303">Like the name says, the query string is a string.</span></span> <span data-ttu-id="3eeba-304">但是，你可以仅测试为 true 和 false 如果您要测试的值是一个布尔 (true/false) 值。</span><span class="sxs-lookup"><span data-stu-id="3eeba-304">However, you can only test for true and false if the value you're testing is a Boolean (true/false) value.</span></span> <span data-ttu-id="3eeba-305">你可以测试查询字符串中的显示变量的值之前，必须将其转换为一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="3eeba-305">Before you can test the value of the show variable in the query string, you have to convert it to a Boolean value.</span></span> <span data-ttu-id="3eeba-306">这就是 AsBool 方法作用 — 它采用字符串作为输入，并将其转换为布尔值。</span><span class="sxs-lookup"><span data-stu-id="3eeba-306">That's what the AsBool method does — it takes a string as input and converts it to a Boolean value.</span></span> <span data-ttu-id="3eeba-307">很明显，如果字符串为"true"，AsBool 方法会将该值转换为 true。</span><span class="sxs-lookup"><span data-stu-id="3eeba-307">Clearly, if the string is "true", the AsBool method converts that value to true.</span></span> <span data-ttu-id="3eeba-308">如果任何其他内容字符串的值，则 AsBool 返回 false。</span><span class="sxs-lookup"><span data-stu-id="3eeba-308">If the value of the string is anything else, AsBool returns false.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="3eeba-309">**数据类型和 as （） 方法**</span><span class="sxs-lookup"><span data-stu-id="3eeba-309">**Data Types and As() Methods**</span></span>
> 
> <span data-ttu-id="3eeba-310">我们仅讲到目前为止，当创建变量时，你会使用关键字差异</span><span class="sxs-lookup"><span data-stu-id="3eeba-310">We've only said so far that when you create a variable, you use the keyword var.</span></span> <span data-ttu-id="3eeba-311">这不是整篇文章，不过。</span><span class="sxs-lookup"><span data-stu-id="3eeba-311">That's not the entire story, though.</span></span> <span data-ttu-id="3eeba-312">为了操作值-若要添加数字，或连接字符串，或比较日期，或测试 true/false-C# 必须使用适当的值的内部表示形式。</span><span class="sxs-lookup"><span data-stu-id="3eeba-312">In order to manipulate values — to add numbers, or concatenate strings, or compare dates, or test for true/false — C# has to work with an appropriate internal representation of the value.</span></span> <span data-ttu-id="3eeba-313">C# 可以*通常*找出该表示形式中应该是什么 (即，什么*类型*数据) 基于您所做的值。</span><span class="sxs-lookup"><span data-stu-id="3eeba-313">C# can *usually* figure out what that representation should be (that is, what *type* the data is) based on what you're doing with the values.</span></span> <span data-ttu-id="3eeba-314">现在，然后，不过，它无法做到这一点。</span><span class="sxs-lookup"><span data-stu-id="3eeba-314">Now and then, though, it can't do that.</span></span> <span data-ttu-id="3eeba-315">如果没有，你需要通过显式，该值指示如何 C# 应表示的数据帮助解决问题。</span><span class="sxs-lookup"><span data-stu-id="3eeba-315">If not, you have to help out by explicitly indicating how C# should represent the data.</span></span> <span data-ttu-id="3eeba-316">AsBool 方法执行的 — 它告诉 C#"true"或"false"的字符串值应视为一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="3eeba-316">The AsBool method does that — it tells C# that a string value of "true" or "false" should be treated as a Boolean value.</span></span> <span data-ttu-id="3eeba-317">存在类似的方法无法表示为其他类型，如 AsInt (treat 整数形式)、 AsDateTime （视为日期/时间）、 AsFloat （视为浮点数） 和等等的字符串。</span><span class="sxs-lookup"><span data-stu-id="3eeba-317">Similar methods exist to represent strings as other types as well, like AsInt (treat as an integer), AsDateTime (treat as a date/time), AsFloat (treat as a floating-point number), and so on.</span></span> <span data-ttu-id="3eeba-318">当你使用这些项目称为 （） 方法，如果 C# 不能表示的字符串值的要求时，你将看到一个错误。</span><span class="sxs-lookup"><span data-stu-id="3eeba-318">When you use these As( ) methods, if C# can't represent the string value as requested, you'll see an error.</span></span>


<span data-ttu-id="3eeba-319">在页面的标记中，删除或注释掉此元素 （此处显示注释掉）：</span><span class="sxs-lookup"><span data-stu-id="3eeba-319">In the markup of the page, remove or comment out this element (here it's shown commented out):</span></span>

[!code-html[Main](intro-to-web-pages-programming/samples/sample12.html)]

<span data-ttu-id="3eeba-320">右删除或注释掉该文本的位置添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="3eeba-320">Right where you removed or commented out that text, add the following:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample13.cshtml)]

<span data-ttu-id="3eeba-321">如果测试表明，是否分隔开多个变量为 true，呈现&lt;p&gt;具有消息变量的值的元素。</span><span class="sxs-lookup"><span data-stu-id="3eeba-321">The if test says that if the showMessage variable is true, render a &lt;p&gt; element with the value of the message variable.</span></span>

### <a name="summary-of-your-conditional-logic"></a><span data-ttu-id="3eeba-322">条件逻辑的摘要</span><span class="sxs-lookup"><span data-stu-id="3eeba-322">Summary of your conditional logic</span></span>

<span data-ttu-id="3eeba-323">如果你不能完全确定只需完成的新增功能，这里只是摘要。</span><span class="sxs-lookup"><span data-stu-id="3eeba-323">In case you're not entirely sure of what you've just done, here's a summary.</span></span>

- <span data-ttu-id="3eeba-324">消息变量初始化为默认字符串 （"这是首次..."）。</span><span class="sxs-lookup"><span data-stu-id="3eeba-324">The message variable is initialized to a default string ("This is the first time ...").</span></span>
- <span data-ttu-id="3eeba-325">如果页面请求是提交 (post) 的结果，消息的值更改为"现在你已提交..."</span><span class="sxs-lookup"><span data-stu-id="3eeba-325">If the page request is the result of a submit (post), the value of message is changed to "Now you've submitted ..."</span></span>
- <span data-ttu-id="3eeba-326">分隔开多个变量初始化为 false。</span><span class="sxs-lookup"><span data-stu-id="3eeba-326">The showMessage variable is initialized to false.</span></span>
- <span data-ttu-id="3eeba-327">如果查询字符串包含？ 显示 = 分隔开多个变量设置为 true，则为 true。</span><span class="sxs-lookup"><span data-stu-id="3eeba-327">If the query string contains ?show=true, the showMessage variable is set to true.</span></span>
- <span data-ttu-id="3eeba-328">在标记中，如果分隔开多个为 true， &lt;p&gt;元素呈现显示消息的值。</span><span class="sxs-lookup"><span data-stu-id="3eeba-328">In the markup, if showMessage is true, a &lt;p&gt; element is rendered that shows the value of message.</span></span> <span data-ttu-id="3eeba-329">（如果分隔开多个为 false，执行任何操作将呈现在该点标记中。）</span><span class="sxs-lookup"><span data-stu-id="3eeba-329">(If showMessage is false, nothing is rendered at that point in the markup.)</span></span>
- <span data-ttu-id="3eeba-330">在标记中，如果请求是 post， &lt;p&gt;元素呈现，显示的日期和时间。</span><span class="sxs-lookup"><span data-stu-id="3eeba-330">In the markup, if the request is a post, a &lt;p&gt; element is rendered that displays the date and time.</span></span>

<span data-ttu-id="3eeba-331">运行页面。</span><span class="sxs-lookup"><span data-stu-id="3eeba-331">Run the page.</span></span> <span data-ttu-id="3eeba-332">没有任何消息，因为分隔开多个为 false，因此在标记中 if(showMessage) 测试返回 false。</span><span class="sxs-lookup"><span data-stu-id="3eeba-332">There's no message, because showMessage is false, so in the markup the if(showMessage) test returns false.</span></span>

<span data-ttu-id="3eeba-333">单击“提交”。</span><span class="sxs-lookup"><span data-stu-id="3eeba-333">Click **Submit**.</span></span> <span data-ttu-id="3eeba-334">你看到该日期和时间，但仍任何消息。</span><span class="sxs-lookup"><span data-stu-id="3eeba-334">You see the date and time, but still no message.</span></span>

<span data-ttu-id="3eeba-335">在浏览器中，转到 URL 框中，并将以下代码添加到 URL 的末尾:？ 显示为 true，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="3eeba-335">In your browser, go to the URL box and add the following to the end of the URL: ?show=true and then press Enter.</span></span>

![在浏览器显示查询字符串中的测试 Razor 2 页](intro-to-web-pages-programming/_static/image5.png)

<span data-ttu-id="3eeba-337">将再次显示的页。</span><span class="sxs-lookup"><span data-stu-id="3eeba-337">The page is displayed again.</span></span> <span data-ttu-id="3eeba-338">（由于更改 URL，这是新请求，不提交。）单击**提交**试。</span><span class="sxs-lookup"><span data-stu-id="3eeba-338">(Because you changed the URL, this is a new request, not a submit.) Click **Submit** again.</span></span> <span data-ttu-id="3eeba-339">原样的日期和时间，将再次显示消息。</span><span class="sxs-lookup"><span data-stu-id="3eeba-339">The message is displayed again, as is the date and time.</span></span>

![查询字符串时，将提交后的测试 Razor 2 页](intro-to-web-pages-programming/_static/image6.png)

<span data-ttu-id="3eeba-341">在 URL 更改？ 显示为真 =？ 显示 = false 然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="3eeba-341">In the URL, change ?show=true to ?show=false and press Enter.</span></span> <span data-ttu-id="3eeba-342">重新提交页。</span><span class="sxs-lookup"><span data-stu-id="3eeba-342">Submit the page again.</span></span> <span data-ttu-id="3eeba-343">该页是返回到你的启动方式如何-任何消息。</span><span class="sxs-lookup"><span data-stu-id="3eeba-343">The page is back to how you started — no message.</span></span>

<span data-ttu-id="3eeba-344">如前文所述，在此示例中的逻辑是一个小虚构浓。</span><span class="sxs-lookup"><span data-stu-id="3eeba-344">As noted earlier, the logic of this example is a little contrived.</span></span> <span data-ttu-id="3eeba-345">但是，如果要在很多的页，提出，需要一个或多个窗体，你已了解此处。</span><span class="sxs-lookup"><span data-stu-id="3eeba-345">However, if is going to come up in many of your pages, and it will take one or more of the forms you've seen here.</span></span>

## <a name="installing-a-helper-displaying-a-gravatar-image"></a><span data-ttu-id="3eeba-346">安装程序 （显示 Gravatar 图像） 的帮助程序</span><span class="sxs-lookup"><span data-stu-id="3eeba-346">Installing a Helper (Displaying a Gravatar Image)</span></span>

<span data-ttu-id="3eeba-347">用户通常想要在网页上执行某些任务需要大量的代码，或者需要额外的知识。</span><span class="sxs-lookup"><span data-stu-id="3eeba-347">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="3eeba-348">示例： 显示的图表数据;将 Facebook"Like"按钮放置在页;从您的网站; 发送电子邮件裁剪或调整图像; 的大小为您的网站使用 PayPal。</span><span class="sxs-lookup"><span data-stu-id="3eeba-348">Examples: displaying a chart for data; putting a Facebook "Like" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="3eeba-349">为了更加轻松地完成这些类型的操作，ASP.NET 网页，你可以使用*帮助器*。</span><span class="sxs-lookup"><span data-stu-id="3eeba-349">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="3eeba-350">帮助器是为站点安装，并能够让你通过使用 Razor 代码只需几行执行典型的任务的组件。</span><span class="sxs-lookup"><span data-stu-id="3eeba-350">Helpers are components that you install for a site and that let you perform typical tasks by using just a few lines of Razor code.</span></span>

<span data-ttu-id="3eeba-351">ASP.NET Web 页具有内置的几个帮助器。</span><span class="sxs-lookup"><span data-stu-id="3eeba-351">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="3eeba-352">但是，使用 NuGet 包管理器提供的包 （外接程序） 中提供了许多的帮助器。</span><span class="sxs-lookup"><span data-stu-id="3eeba-352">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="3eeba-353">NuGet 允许你选择要安装的程序包，然后它就会完成安装的所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="3eeba-353">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

<span data-ttu-id="3eeba-354">在本教程的此部分中，你将安装的帮助程序便可以显示 Gravatar （"全局识别虚拟形象"） 映像。</span><span class="sxs-lookup"><span data-stu-id="3eeba-354">In this part of the tutorial, you'll install a helper that lets you display a Gravatar ("globally recognized avatar") image.</span></span> <span data-ttu-id="3eeba-355">你将学习以下两项操作。</span><span class="sxs-lookup"><span data-stu-id="3eeba-355">You'll learn two things.</span></span> <span data-ttu-id="3eeba-356">一个是如何查找和安装程序的帮助。</span><span class="sxs-lookup"><span data-stu-id="3eeba-356">One is how to find and install a helper.</span></span> <span data-ttu-id="3eeba-357">你还将了解如何帮助程序可以轻松地执行某些否则需要使用大量您将不得不自己编写的代码执行操作。</span><span class="sxs-lookup"><span data-stu-id="3eeba-357">You'll also learn how a helper makes it easy to do something you'd otherwise need to do by using a lot of code you'd have to write yourself.</span></span>

<span data-ttu-id="3eeba-358">你可以注册在 Gravatar 网站在自己 Gravatar [ http://www.gravatar.com/ ](http://www.gravatar.com/)，但它不是创建 Gravatar 帐户执行本教程的此部分非常重要。</span><span class="sxs-lookup"><span data-stu-id="3eeba-358">You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/), but it is not essential to create a Gravatar account to perform this part of the tutorial.</span></span>

<span data-ttu-id="3eeba-359">在 WebMatrix 中，单击**NuGet**按钮。</span><span class="sxs-lookup"><span data-stu-id="3eeba-359">In WebMatrix, click the **NuGet** button.</span></span>

![在 WebMatrix 的 NuGet 库对话框](intro-to-web-pages-programming/_static/image7.png)

<span data-ttu-id="3eeba-361">这将启动 NuGet 包管理器，并显示可用的包。</span><span class="sxs-lookup"><span data-stu-id="3eeba-361">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="3eeba-362">(不是所有包都帮助器; 一些将功能添加到 WebMatrix 中本身，一些是其他模板，依次类推。)你可能会收到有关版本不兼容的错误消息。</span><span class="sxs-lookup"><span data-stu-id="3eeba-362">(Not all of the packages are helpers; some add functionality to WebMatrix itself, some are additional templates, and so on.) You may get an error message about version incompatibility.</span></span> <span data-ttu-id="3eeba-363">你可以忽略此错误消息，通过单击**确定**和继续执行本教程。</span><span class="sxs-lookup"><span data-stu-id="3eeba-363">You can ignore this error message by clicking **OK** and proceeding with this tutorial.</span></span>

![在 WebMatrix 的 NuGet 库对话框](intro-to-web-pages-programming/_static/image8.png)

<span data-ttu-id="3eeba-365">在搜索框中，输入"asp.net 帮助器"。</span><span class="sxs-lookup"><span data-stu-id="3eeba-365">In the search box, enter "asp.net helpers".</span></span> <span data-ttu-id="3eeba-366">NuGet 显示与搜索词匹配的程序包。</span><span class="sxs-lookup"><span data-stu-id="3eeba-366">NuGet shows the packages that match the search terms.</span></span>

![在 WebMatrix 中显示包的 NuGet 库](intro-to-web-pages-programming/_static/image9.png)

<span data-ttu-id="3eeba-368">ASP.NET Web 帮助程序库包含代码以简化许多常见任务，包括使用 Gravatar 图像。</span><span class="sxs-lookup"><span data-stu-id="3eeba-368">The ASP.NET Web Helpers Library contains code to simplify many common tasks, including the use of Gravatar images.</span></span> <span data-ttu-id="3eeba-369">选择**ASP.NET Web 帮助程序库**包，然后单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="3eeba-369">Select the **ASP.NET Web Helpers Library** package and then click **Install** to launch the installer.</span></span> <span data-ttu-id="3eeba-370">选择**是**当系统询问你是否想要安装包，并接受条款以完成安装。</span><span class="sxs-lookup"><span data-stu-id="3eeba-370">Select **Yes** when asked if you want to install the package, and accept the terms to complete the installation.</span></span>

<span data-ttu-id="3eeba-371">介绍完毕。</span><span class="sxs-lookup"><span data-stu-id="3eeba-371">That's it.</span></span> <span data-ttu-id="3eeba-372">NuGet 下载并安装所有内容，包括可能需要的任何其他组件 (*依赖关系*)。</span><span class="sxs-lookup"><span data-stu-id="3eeba-372">NuGet downloads and installs everything, including any additional components that might be required (*dependencies*).</span></span>

<span data-ttu-id="3eeba-373">如果出于某种原因你必须卸载程序的帮助程序，此过程是非常类似。</span><span class="sxs-lookup"><span data-stu-id="3eeba-373">If for some reason you have to uninstall a helper, the process is very similar.</span></span> <span data-ttu-id="3eeba-374">单击**NuGet**菜单上，单击**已安装**选项卡，然后选择你想要卸载的程序包。</span><span class="sxs-lookup"><span data-stu-id="3eeba-374">Click the **NuGet** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="using-a-helper-in-a-page"></a><span data-ttu-id="3eeba-375">在页中使用程序的帮助程序</span><span class="sxs-lookup"><span data-stu-id="3eeba-375">Using a Helper in a Page</span></span>

<span data-ttu-id="3eeba-376">现在，你将使用你刚安装的帮助程序。</span><span class="sxs-lookup"><span data-stu-id="3eeba-376">Now you'll use the helper that you just installed.</span></span> <span data-ttu-id="3eeba-377">将程序的帮助程序添加到页过程是类似的大多数帮助器。</span><span class="sxs-lookup"><span data-stu-id="3eeba-377">The process for adding a helper to a page is similar for most helpers.</span></span>

<span data-ttu-id="3eeba-378">在 WebMatrix 中，创建一个页面，并将其命名*GravatarTest.cshml*。</span><span class="sxs-lookup"><span data-stu-id="3eeba-378">In WebMatrix, create a page and name it *GravatarTest.cshml*.</span></span> <span data-ttu-id="3eeba-379">（你要创建特殊页后，可以测试帮助器，但你可以使用在你的站点中的任意页中的帮助器。）</span><span class="sxs-lookup"><span data-stu-id="3eeba-379">(You're creating a special page to test the helper, but you can use helpers in any page in your site.)</span></span>

<span data-ttu-id="3eeba-380">内部&lt;正文&gt;元素中，添加&lt;div&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="3eeba-380">Inside the &lt;body&gt; element, add a &lt;div&gt; element.</span></span> <span data-ttu-id="3eeba-381">内部&lt;div&gt;元素中，键入：</span><span class="sxs-lookup"><span data-stu-id="3eeba-381">Inside the &lt;div&gt; element, type this:</span></span>

<span data-ttu-id="3eeba-382">@Gravatar。</span><span class="sxs-lookup"><span data-stu-id="3eeba-382">@Gravatar.</span></span>

<span data-ttu-id="3eeba-383">@ 字符是你所用来标记 Razor 代码的相同字符。</span><span class="sxs-lookup"><span data-stu-id="3eeba-383">The @ character is the same character you've been using to mark Razor code.</span></span> <span data-ttu-id="3eeba-384">**Gravatar**即你正在使用的帮助程序对象。</span><span class="sxs-lookup"><span data-stu-id="3eeba-384">**Gravatar** is the helper object that you're working with.</span></span>

<span data-ttu-id="3eeba-385">WebMatrix 只要键入句点 （.），显示的列表*方法*（函数） 的 Gravatar 帮助程序使可：</span><span class="sxs-lookup"><span data-stu-id="3eeba-385">As soon as you type the period (.), WebMatrix displays a list of *methods* (functions) that the Gravatar helper makes available:</span></span>

![Gravatar 帮助器 IntelliSense 下拉列表](intro-to-web-pages-programming/_static/image10.png)

<span data-ttu-id="3eeba-387">此功能被称为*IntelliSense*。</span><span class="sxs-lookup"><span data-stu-id="3eeba-387">This feature is known as *IntelliSense*.</span></span> <span data-ttu-id="3eeba-388">它通过提供上下文相对应的选项帮助你进行编码。</span><span class="sxs-lookup"><span data-stu-id="3eeba-388">It helps you code by providing context-appropriate choices.</span></span> <span data-ttu-id="3eeba-389">IntelliSense 适用于 HTML、 CSS、 ASP.NET 代码、 JavaScript 和其他语言，支持在 WebMatrix 中。</span><span class="sxs-lookup"><span data-stu-id="3eeba-389">IntelliSense works with HTML, CSS, ASP.NET code, JavaScript, and other languages that are supported in WebMatrix.</span></span> <span data-ttu-id="3eeba-390">它是另一个功能，它可以更轻松地开发在 WebMatrix 中的网页。</span><span class="sxs-lookup"><span data-stu-id="3eeba-390">It's another feature that makes it easier to develop web pages in WebMatrix.</span></span>

<span data-ttu-id="3eeba-391">按 G 上键盘，请参阅 IntelliSense 查找 GetHtml 方法。</span><span class="sxs-lookup"><span data-stu-id="3eeba-391">Press G on the keyboard, and you see that IntelliSense finds the GetHtml method.</span></span> <span data-ttu-id="3eeba-392">按 Tab。IntelliSense 为您插入所选的方法 (GetHtml)。</span><span class="sxs-lookup"><span data-stu-id="3eeba-392">Press Tab. IntelliSense inserts the selected method (GetHtml) for you.</span></span> <span data-ttu-id="3eeba-393">键入左括号，请注意，自动添加右括号。</span><span class="sxs-lookup"><span data-stu-id="3eeba-393">Type an open parenthesis, and notice that the closing parenthesis is automatically added.</span></span> <span data-ttu-id="3eeba-394">用引号括起来的两个括号之间键入你的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="3eeba-394">Type your email address in quotation marks between the two parenthesis.</span></span> <span data-ttu-id="3eeba-395">如果你有 Gravatar 帐户，将返回你的个人资料图片。</span><span class="sxs-lookup"><span data-stu-id="3eeba-395">If you have a Gravatar account, your profile picture will be returned.</span></span> <span data-ttu-id="3eeba-396">如果你没有 Gravatar 帐户，则返回默认图像。</span><span class="sxs-lookup"><span data-stu-id="3eeba-396">If you do not have a Gravatar account, a default image is returned.</span></span> <span data-ttu-id="3eeba-397">完成后，行如下所示：</span><span class="sxs-lookup"><span data-stu-id="3eeba-397">When you're done, the line looks like this:</span></span>

[!code-css[Main](intro-to-web-pages-programming/samples/sample14.css)]

<span data-ttu-id="3eeba-398">现在在浏览器中查看的页面。</span><span class="sxs-lookup"><span data-stu-id="3eeba-398">Now view the page in a browser.</span></span> <span data-ttu-id="3eeba-399">你的图片或默认图像将显示，具体取决于是否有 Gravatar 帐户。</span><span class="sxs-lookup"><span data-stu-id="3eeba-399">Either your picture or the default image is displayed, depending on whether you have a Gravatar account.</span></span>

![Gravatar](intro-to-web-pages-programming/_static/image11.png) ![默认映像](intro-to-web-pages-programming/_static/image12.png)

<span data-ttu-id="3eeba-402">若要了解的内容的帮助器为你做，在浏览器中查看的页面的源。</span><span class="sxs-lookup"><span data-stu-id="3eeba-402">To get an idea of what the helper is doing for you, view the source of the page in the browser.</span></span> <span data-ttu-id="3eeba-403">必须在页中的 HTML，以及你将看到包含的标识符的图像元素。</span><span class="sxs-lookup"><span data-stu-id="3eeba-403">Along with the HTML that you had in your page, you see an image element that includes an identifier.</span></span> <span data-ttu-id="3eeba-404">这是帮助器呈现到页，其中 d 的位置的代码@Gravatar.GetHtml。</span><span class="sxs-lookup"><span data-stu-id="3eeba-404">This is code that the helper rendered into the page at the place where you had @Gravatar.GetHtml.</span></span> <span data-ttu-id="3eeba-405">帮助器所花费的提供和生成交谈直接 Gravatar 若要提供帐户的取回了正确的图像的代码的信息。</span><span class="sxs-lookup"><span data-stu-id="3eeba-405">The helper took the information you provided and generated the code that talks directly to Gravatar in order to get back the correct image for supplied account.</span></span>

<span data-ttu-id="3eeba-406">GetHtml 方法还可通过提供其他参数自定义映像。</span><span class="sxs-lookup"><span data-stu-id="3eeba-406">The GetHtml method also enables you to customize the image by providing other parameters.</span></span> <span data-ttu-id="3eeba-407">下面的代码演示如何请求映像具有宽度和高度 40 个像素，并使用名为指定的默认映像**wavatar**如果指定的帐户不存在。</span><span class="sxs-lookup"><span data-stu-id="3eeba-407">The following code shows how to request an image has a width and height of 40 pixels, and uses a specified default image named **wavatar** if the specified account does not exist.</span></span>

[!code-javascript[Main](intro-to-web-pages-programming/samples/sample15.js)]

<span data-ttu-id="3eeba-408">此代码生成以下 （默认映像随机有所不同） 的结果类似。</span><span class="sxs-lookup"><span data-stu-id="3eeba-408">This code produces something like the following result (the default image will randomly vary).</span></span>

![](intro-to-web-pages-programming/_static/image13.png)

## <a name="coming-up-next"></a><span data-ttu-id="3eeba-409">接下来</span><span class="sxs-lookup"><span data-stu-id="3eeba-409">Coming Up Next</span></span>

<span data-ttu-id="3eeba-410">若要使此教程短，我们不得不专注于仅几个基础知识。</span><span class="sxs-lookup"><span data-stu-id="3eeba-410">To keep this tutorial short, we had to focus on only a few basics.</span></span> <span data-ttu-id="3eeba-411">当然，没有*很多*更多的 Razor 和 C#。</span><span class="sxs-lookup"><span data-stu-id="3eeba-411">Naturally, there's a *lot* more to Razor and C#.</span></span> <span data-ttu-id="3eeba-412">你将了解更多其他你经历这些教程。</span><span class="sxs-lookup"><span data-stu-id="3eeba-412">You'll learn more as you go through these tutorials.</span></span> <span data-ttu-id="3eeba-413">如果你感兴趣稍后再试学习有关 Razor 和 C# 的编程方面的详细信息，你可以阅读的更全面的介绍： [ASP.NET Web 编程使用 Razor 语法的简介](https://go.microsoft.com/fwlink/?LinkID=202890)。</span><span class="sxs-lookup"><span data-stu-id="3eeba-413">If you're interested in learning more about the programming aspects of Razor and C# right now, you can read a more thorough introduction here: [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=202890).</span></span>

<span data-ttu-id="3eeba-414">下一步教程将介绍如何使用的数据库。</span><span class="sxs-lookup"><span data-stu-id="3eeba-414">The next tutorial introduces you to working with a database.</span></span> <span data-ttu-id="3eeba-415">在该教程中，你将开始创建的示例应用程序允许你列出您最喜爱的电影。</span><span class="sxs-lookup"><span data-stu-id="3eeba-415">In that tutorial, you'll begin creating the sample application that lets you list your favorite movies.</span></span>

## <a name="complete-listing-for-testrazor-page"></a><span data-ttu-id="3eeba-416">TestRazor 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="3eeba-416">Complete Listing for TestRazor Page</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample16.cshtml)]

## <a name="complete-listing-for-testrazorpart2-page"></a><span data-ttu-id="3eeba-417">TestRazorPart2 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="3eeba-417">Complete Listing for TestRazorPart2 Page</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample17.cshtml)]

## <a name="complete-listing-for-gravatartest-page"></a><span data-ttu-id="3eeba-418">GravatarTest 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="3eeba-418">Complete Listing for GravatarTest Page</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample18.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="3eeba-419">其他资源</span><span class="sxs-lookup"><span data-stu-id="3eeba-419">Additional Resources</span></span>

- [<span data-ttu-id="3eeba-420">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="3eeba-420">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- [<span data-ttu-id="3eeba-421">Twitter 帮助器</span><span class="sxs-lookup"><span data-stu-id="3eeba-421">Twitter helper</span></span>](../../ui-layouts-and-themes/twitter-helper.md)

> [!div class="step-by-step"]
> <span data-ttu-id="3eeba-422">[上一页](getting-started.md)
> [下一页](displaying-data.md)</span><span class="sxs-lookup"><span data-stu-id="3eeba-422">[Previous](getting-started.md)
[Next](displaying-data.md)</span></span>
