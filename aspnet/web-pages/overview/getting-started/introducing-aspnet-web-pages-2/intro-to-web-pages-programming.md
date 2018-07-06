---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
title: Introducing ASP.NET 网页-编程基础知识 |Microsoft Docs
author: tfitzmac
description: 此教程提供了一些您简要介绍了使用 Razor 语法的 ASP.NET Web Pages 中程序到。 你将了解： 使用拉取请求的基本 Razor 语法...
ms.author: aspnetcontent
ms.date: 06/17/2015
ms.assetid: 7526ed45-a97d-4e8a-8301-01324ef0eff9
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
msc.type: authoredcontent
ms.openlocfilehash: 56268943b09d366b15d3a11e641d6c6b6c95aa16
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37839744"
---
<a name="introducing-aspnet-web-pages---programming-basics"></a><span data-ttu-id="2801d-104">ASP.NET 网页简介-编程基础知识</span><span class="sxs-lookup"><span data-stu-id="2801d-104">Introducing ASP.NET Web Pages - Programming Basics</span></span>
====================
<span data-ttu-id="2801d-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="2801d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="2801d-106">此教程提供了一些您简要介绍了使用 Razor 语法的 ASP.NET Web Pages 中程序到。</span><span class="sxs-lookup"><span data-stu-id="2801d-106">This tutorial gives you an overview of how to program in ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="2801d-107">你将学习：</span><span class="sxs-lookup"><span data-stu-id="2801d-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="2801d-108">编程 ASP.NET Web Pages 中使用的基本"Razor"语法。</span><span class="sxs-lookup"><span data-stu-id="2801d-108">The basic "Razor" syntax that you use for programming in ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="2801d-109">一些基本 C# 中，这是你将使用的编程语言。</span><span class="sxs-lookup"><span data-stu-id="2801d-109">Some basic C#, which is the programming language you'll use.</span></span>
> - <span data-ttu-id="2801d-110">网页的某些基本编程概念。</span><span class="sxs-lookup"><span data-stu-id="2801d-110">Some fundamental programming concepts for Web Pages.</span></span>
> - <span data-ttu-id="2801d-111">如何安装包 （包含预生成的代码的组件） 以使用你的网站。</span><span class="sxs-lookup"><span data-stu-id="2801d-111">How to install packages (components that contain prebuilt code) to use with your site.</span></span>
> - <span data-ttu-id="2801d-112">如何使用*帮助程序*以执行常见编程任务。</span><span class="sxs-lookup"><span data-stu-id="2801d-112">How to use *helpers* to perform common programming tasks.</span></span>
>   
> 
> <span data-ttu-id="2801d-113">功能/技术讨论：</span><span class="sxs-lookup"><span data-stu-id="2801d-113">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="2801d-114">NuGet 和包管理器。</span><span class="sxs-lookup"><span data-stu-id="2801d-114">NuGet and the package manager.</span></span>
> - <span data-ttu-id="2801d-115">`Gravatar`帮助器。</span><span class="sxs-lookup"><span data-stu-id="2801d-115">The `Gravatar` helper.</span></span>


<span data-ttu-id="2801d-116">本教程是主要向您介绍的编程语法，将使用为 ASP.NET Web Pages 中练习。</span><span class="sxs-lookup"><span data-stu-id="2801d-116">This tutorial is primarily an exercise in introducing you to the programming syntax that you'll use for ASP.NET Web Pages.</span></span> <span data-ttu-id="2801d-117">你将了解如何*Razor 语法*和 C# 中编写代码的编程语言。</span><span class="sxs-lookup"><span data-stu-id="2801d-117">You'll learn about *Razor syntax* and code that's written in the C# programming language.</span></span> <span data-ttu-id="2801d-118">前面的教程; 中有大致了解此语法在本教程中我们将介绍详细的语法。</span><span class="sxs-lookup"><span data-stu-id="2801d-118">You got a glimpse of this syntax in the previous tutorial; in this tutorial we'll explain the syntax more.</span></span>

<span data-ttu-id="2801d-119">我们保证，本教程涉及到您将看到在单个教程中，且它是唯一的教程，是编程最*仅*有关编程。</span><span class="sxs-lookup"><span data-stu-id="2801d-119">We promise that this tutorial involves the most programming that you'll see in a single tutorial, and that it's the only tutorial that is *only* about programming.</span></span> <span data-ttu-id="2801d-120">在此集中的其余教程，你实际上将创建一些有趣的操作的页面。</span><span class="sxs-lookup"><span data-stu-id="2801d-120">In the remaining tutorials in this set, you'll actually create pages that do interesting things.</span></span>

<span data-ttu-id="2801d-121">此外将了解*帮助程序*。</span><span class="sxs-lookup"><span data-stu-id="2801d-121">You'll also learn about *helpers*.</span></span> <span data-ttu-id="2801d-122">帮助器是一个组件 — 打包向上的一段代码，可添加到页面。</span><span class="sxs-lookup"><span data-stu-id="2801d-122">A helper is a component — a packaged-up piece of code — that you can add to a page.</span></span> <span data-ttu-id="2801d-123">帮助器执行，否则可能是乏味或复杂手动进行的工作。</span><span class="sxs-lookup"><span data-stu-id="2801d-123">The helper performs work for you that otherwise might be tedious or complex to do by hand.</span></span>

## <a name="creating-a-page-to-play-with-razor"></a><span data-ttu-id="2801d-124">创建使用 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="2801d-124">Creating a Page to Play with Razor</span></span>

<span data-ttu-id="2801d-125">在本部分中您将扮演有点 Razor 以便您可以了解的基本语法。</span><span class="sxs-lookup"><span data-stu-id="2801d-125">In this section you'll play a bit with Razor so you can get a sense of the basic syntax.</span></span>

<span data-ttu-id="2801d-126">启动 WebMatrix，如果它尚不存在正在运行。</span><span class="sxs-lookup"><span data-stu-id="2801d-126">Start WebMatrix if it's not already running.</span></span> <span data-ttu-id="2801d-127">你将使用上一教程中创建的网站 ([获取启动与网页](https://go.microsoft.com/fwlink/?LinkId=251578))。</span><span class="sxs-lookup"><span data-stu-id="2801d-127">You'll use the website you created in the previous tutorial ([Getting Started With Web Pages](https://go.microsoft.com/fwlink/?LinkId=251578)).</span></span> <span data-ttu-id="2801d-128">若要重新打开它，请单击**我的网站**，然后选择**WebPageMovies**:</span><span class="sxs-lookup"><span data-stu-id="2801d-128">To reopen it, click **My Sites** and choose **WebPageMovies**:</span></span>

![显示打开站点选项并突出显示了我的网站的 WebMatrix 开始屏幕](intro-to-web-pages-programming/_static/image1.png)

<span data-ttu-id="2801d-130">选择**文件**工作区。</span><span class="sxs-lookup"><span data-stu-id="2801d-130">Select the **Files** workspace.</span></span>

<span data-ttu-id="2801d-131">在功能区中，单击**新建**来创建一个页面。</span><span class="sxs-lookup"><span data-stu-id="2801d-131">In the ribbon, click **New** to create a page.</span></span> <span data-ttu-id="2801d-132">选择**CSHTML**并命名新页面*TestRazor.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="2801d-132">Select **CSHTML** and name the new page *TestRazor.cshtml*.</span></span>

<span data-ttu-id="2801d-133">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="2801d-133">Click **OK**.</span></span>

<span data-ttu-id="2801d-134">将以下内容复制到文件中，完全替换什么已存在。</span><span class="sxs-lookup"><span data-stu-id="2801d-134">Copy the following into the file, completely replacing what's there already.</span></span>

> [!NOTE]
> <span data-ttu-id="2801d-135">复制时代码或标记示例中放入页中，缩进和对齐方式不可能与本教程中的相同。</span><span class="sxs-lookup"><span data-stu-id="2801d-135">When you copy code or markup from the examples into a page, the indentation and alignment might not be the same as in the tutorial.</span></span> <span data-ttu-id="2801d-136">缩进和对齐方式不会影响代码的运行方式，不过。</span><span class="sxs-lookup"><span data-stu-id="2801d-136">Indentation and alignment don't affect how the code runs, though.</span></span>


[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample1.cshtml)]

## <a name="examining-the-example-page"></a><span data-ttu-id="2801d-137">检查示例页</span><span class="sxs-lookup"><span data-stu-id="2801d-137">Examining the Example Page</span></span>

<span data-ttu-id="2801d-138">您所看到的大多数都是普通的 HTML。</span><span class="sxs-lookup"><span data-stu-id="2801d-138">Most of what you see is ordinary HTML.</span></span> <span data-ttu-id="2801d-139">但是，在顶部没有此代码块：</span><span class="sxs-lookup"><span data-stu-id="2801d-139">However, at the top there's this code block:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample2.cshtml)]

<span data-ttu-id="2801d-140">请注意，此代码块有关以下操作：</span><span class="sxs-lookup"><span data-stu-id="2801d-140">Notice the following things about this code block:</span></span>

- <span data-ttu-id="2801d-141">@ 字符告诉 ASP.NET，后面是 Razor 代码中，不是 HTML。</span><span class="sxs-lookup"><span data-stu-id="2801d-141">The @ character tells ASP.NET that what follows is Razor code, not HTML.</span></span> <span data-ttu-id="2801d-142">ASP.NET 将处理后的所有内容 @ 字符作为代码，直至它再次运行到一些 HTML。</span><span class="sxs-lookup"><span data-stu-id="2801d-142">ASP.NET will treat everything after the @ character as code until it runs into some HTML again.</span></span> <span data-ttu-id="2801d-143">(在这种情况下，这&lt;！DOCTYPE&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="2801d-143">(In this case, that's the &lt;!DOCTYPE&gt; element.</span></span>
- <span data-ttu-id="2801d-144">大括号 （{和}） 括起来的 Razor 代码块，如果代码具有多个行。</span><span class="sxs-lookup"><span data-stu-id="2801d-144">The braces ( { and } ) enclose a block of Razor code if the code has more than one line.</span></span> <span data-ttu-id="2801d-145">大括号告知 ASP.NET，该块中的代码开始和结束的位置。</span><span class="sxs-lookup"><span data-stu-id="2801d-145">The braces tell ASP.NET where the code for that block starts and ends.</span></span>
- <span data-ttu-id="2801d-146">/ / 字符标记注释 — 也就是说，不会执行的代码的一部分。</span><span class="sxs-lookup"><span data-stu-id="2801d-146">The // characters mark a comment — that is, a part of the code that won't execute.</span></span>
- <span data-ttu-id="2801d-147">每个语句必须以分号 （;） 结束。</span><span class="sxs-lookup"><span data-stu-id="2801d-147">Each statement has to end with a semicolon (;).</span></span> <span data-ttu-id="2801d-148">（不注释，但。）</span><span class="sxs-lookup"><span data-stu-id="2801d-148">(Not comments, though.)</span></span>
- <span data-ttu-id="2801d-149">可以存储中的值*变量*，创建 (*声明*) 与关键字 var。</span><span class="sxs-lookup"><span data-stu-id="2801d-149">You can store values in *variables*, which you create (*declare*) with the keyword var.</span></span> <span data-ttu-id="2801d-150">在创建变量时，您为其提供一个名称，可以包含字母、 数字和下划线 (\_)。</span><span class="sxs-lookup"><span data-stu-id="2801d-150">When you create a variable, you give it a name, which can include letters, numbers, and underscore (\_).</span></span> <span data-ttu-id="2801d-151">变量名称不能以数字开头，并且不能使用编程关键字 （如 var) 的名称。</span><span class="sxs-lookup"><span data-stu-id="2801d-151">Variable names can't start with a number and can't use the name of a programming keyword (like var).</span></span>
- <span data-ttu-id="2801d-152">将字符字符串 （如"ASP.NET"和"网页"） 括在引号中。</span><span class="sxs-lookup"><span data-stu-id="2801d-152">You enclose character strings (like "ASP.NET" and "Web Pages") in quotation marks.</span></span> <span data-ttu-id="2801d-153">（它们必须是两个双引号）。数字不是在引号中。</span><span class="sxs-lookup"><span data-stu-id="2801d-153">(They must be double quotation marks.) Numbers are not in quotation marks.</span></span>
- <span data-ttu-id="2801d-154">引号外的空白并不重要。</span><span class="sxs-lookup"><span data-stu-id="2801d-154">Whitespace outside of quotation marks doesn't matter.</span></span> <span data-ttu-id="2801d-155">换行通常不重要;例外情况是，不能将引号中的字符串拆分到行。</span><span class="sxs-lookup"><span data-stu-id="2801d-155">Line breaks mostly don't matter; the exception is that you can't split a string in quotation marks across lines.</span></span> <span data-ttu-id="2801d-156">缩进和对齐方式不重要。</span><span class="sxs-lookup"><span data-stu-id="2801d-156">Indentation and alignment don't matter.</span></span>

<span data-ttu-id="2801d-157">这并不明显，此示例中是所有代码都是区分大小写。</span><span class="sxs-lookup"><span data-stu-id="2801d-157">Something that's not obvious from this example is that all code is case sensitive.</span></span> <span data-ttu-id="2801d-158">这意味着变量的参数是一个不同的变量比可能名为参数的变量。</span><span class="sxs-lookup"><span data-stu-id="2801d-158">This means that the variable TheSum is a different variable than variables that might be named theSum or thesum.</span></span> <span data-ttu-id="2801d-159">同样，var 关键字，但 Var 不是。</span><span class="sxs-lookup"><span data-stu-id="2801d-159">Similarly, var is a keyword, but Var is not.</span></span>

### <a name="objects-and-properties-and-methods"></a><span data-ttu-id="2801d-160">对象和属性和方法</span><span class="sxs-lookup"><span data-stu-id="2801d-160">Objects and properties and methods</span></span>

<span data-ttu-id="2801d-161">然后是 DateTime.Now 的表达式。</span><span class="sxs-lookup"><span data-stu-id="2801d-161">Then there's the expression DateTime.Now.</span></span> <span data-ttu-id="2801d-162">简单来说，是日期时间*对象*。</span><span class="sxs-lookup"><span data-stu-id="2801d-162">In simple terms, DateTime is an *object*.</span></span> <span data-ttu-id="2801d-163">一个对象是件事情可以与编程 — 页面、 文本框、 文件、 图像、 web 请求、 电子邮件、 客户记录，等等。对象具有一个或多个*属性*，用于描述它们的特征。</span><span class="sxs-lookup"><span data-stu-id="2801d-163">An object is a thing that you can program with—a page, a text box, a file, an image, a web request, an email message, a customer record, etc. Objects have one or more *properties* that describe their characteristics.</span></span> <span data-ttu-id="2801d-164">文本框对象具有文本属性 （及其他）、 请求对象具有 Url 属性 （和其他人）、 电子邮件具有 From 属性和 To 属性中，依次类推。</span><span class="sxs-lookup"><span data-stu-id="2801d-164">A text box object has a Text property (among others), a request object has a Url property (and others), an email message has a From property and a To property, and so on.</span></span> <span data-ttu-id="2801d-165">对象还具有*方法*是他们可以执行的"谓词"。</span><span class="sxs-lookup"><span data-stu-id="2801d-165">Objects also have *methods* that are the "verbs" they can perform.</span></span> <span data-ttu-id="2801d-166">您将使用对象大量。</span><span class="sxs-lookup"><span data-stu-id="2801d-166">You'll be working with objects a lot.</span></span>

<span data-ttu-id="2801d-167">如您所见示例中，日期时间将是可计划日期和时间的对象。</span><span class="sxs-lookup"><span data-stu-id="2801d-167">As you can see from the example, DateTime is an object that lets you program dates and times.</span></span> <span data-ttu-id="2801d-168">它具有一个名为现在，它返回当前日期和时间属性。</span><span class="sxs-lookup"><span data-stu-id="2801d-168">It has a property named Now that returns the current date and time.</span></span>

### <a name="using-code-to-render-markup-in-the-page"></a><span data-ttu-id="2801d-169">使用代码来呈现的页中的标记</span><span class="sxs-lookup"><span data-stu-id="2801d-169">Using code to render markup in the page</span></span>

<span data-ttu-id="2801d-170">在页的正文，请注意以下：</span><span class="sxs-lookup"><span data-stu-id="2801d-170">In the body of the page, notice the following:</span></span>

[!code-html[Main](intro-to-web-pages-programming/samples/sample3.html)]

<span data-ttu-id="2801d-171">同样，@ 字符告诉 ASP.NET，下面的内容是代码，不是 HTML。</span><span class="sxs-lookup"><span data-stu-id="2801d-171">Again, the @ character tells ASP.NET that what follows is code, not HTML.</span></span> <span data-ttu-id="2801d-172">在标记中您可以添加代码表达式后, 跟，ASP.NET 将呈现该表达式右侧的值在该点。</span><span class="sxs-lookup"><span data-stu-id="2801d-172">In the markup you can add @ followed by a code expression, and ASP.NET will render the value of that expression right at that point.</span></span> <span data-ttu-id="2801d-173">在示例中，@a将呈现的值是任何内容的名为的变量，@product呈现任何内容是中的变量的命名产品，依此类推。</span><span class="sxs-lookup"><span data-stu-id="2801d-173">In the example, @a will render whatever the value is of the variable named a, @product renders whatever is in the variable named product, and so on.</span></span>

<span data-ttu-id="2801d-174">您并不仅限于变量，但。</span><span class="sxs-lookup"><span data-stu-id="2801d-174">You're not limited to variables, though.</span></span> <span data-ttu-id="2801d-175">在某些情况下在这里，@ 字符之前表达式：</span><span class="sxs-lookup"><span data-stu-id="2801d-175">In a few instances here, the @ character precedes an expression:</span></span>

- <span data-ttu-id="2801d-176">@(\*b） 将呈现在变量中的所有内容的产品和 b。</span><span class="sxs-lookup"><span data-stu-id="2801d-176">@(a\*b) renders the product of whatever is in the variables a and b.</span></span> <span data-ttu-id="2801d-177">(\*运算符表示乘法。)</span><span class="sxs-lookup"><span data-stu-id="2801d-177">(The \* operator means multiplication.)</span></span>
- <span data-ttu-id="2801d-178">@(技术 +""+ 产品) 将它们连接起来并之间添加空格之后呈现变量技术和产品中的值。</span><span class="sxs-lookup"><span data-stu-id="2801d-178">@(technology + " " + product) renders the values in the variables technology and product after concatenating them and adding a space in between.</span></span> <span data-ttu-id="2801d-179">运算符 （+） 用于连接字符串是与运算符相同的数字添加。</span><span class="sxs-lookup"><span data-stu-id="2801d-179">The operator (+) for concatenating strings is the same as the operator for adding numbers.</span></span> <span data-ttu-id="2801d-180">ASP.NET，通常可以判断是否使用数字或字符串并采取适当的措施使用 + 运算符。</span><span class="sxs-lookup"><span data-stu-id="2801d-180">ASP.NET can usually tell whether you're working with numbers or with strings and does the right thing with the + operator.</span></span>
- <span data-ttu-id="2801d-181">@Request.Url 呈现请求对象的 Url 属性。</span><span class="sxs-lookup"><span data-stu-id="2801d-181">@Request.Url renders the Url property of the Request object.</span></span> <span data-ttu-id="2801d-182">请求对象包含有关浏览器中，从当前请求的信息，当然 Url 属性包含该当前请求的 URL。</span><span class="sxs-lookup"><span data-stu-id="2801d-182">The Request object contains information about the current request from the browser, and of course the Url property contains the URL of that current request.</span></span>

<span data-ttu-id="2801d-183">该示例还旨在演示您可以执行不同的方式工作。</span><span class="sxs-lookup"><span data-stu-id="2801d-183">The example is also designed to show you that you can do work in different ways.</span></span> <span data-ttu-id="2801d-184">可以执行在顶部的代码块中的计算，将结果放到变量中，并随后呈现标记中的变量。</span><span class="sxs-lookup"><span data-stu-id="2801d-184">You can do calculations in the code block at the top, put the results into a variable, and then render the variable in markup.</span></span> <span data-ttu-id="2801d-185">或者，可以执行中的标记中的表达式右侧的计算。</span><span class="sxs-lookup"><span data-stu-id="2801d-185">Or you can do calculations in an expression right in the markup.</span></span> <span data-ttu-id="2801d-186">则使用此方法取决于在您执行的操作，以及在某种程度上，在您自己的首选项。</span><span class="sxs-lookup"><span data-stu-id="2801d-186">The approach you use depends on what you're doing and, to some extent, on your own preference.</span></span>

### <a name="seeing-the-code-in-action"></a><span data-ttu-id="2801d-187">查看操作中的代码</span><span class="sxs-lookup"><span data-stu-id="2801d-187">Seeing the code in action</span></span>

<span data-ttu-id="2801d-188">右键单击该文件的名称，然后选择**浏览器中启动**。</span><span class="sxs-lookup"><span data-stu-id="2801d-188">Right-click the name of the file and then choose **Launch in browser**.</span></span> <span data-ttu-id="2801d-189">请参阅中的所有值和表达式在页中已解决了浏览器的页。</span><span class="sxs-lookup"><span data-stu-id="2801d-189">You see the page in the browser with all the values and expressions resolved in the page.</span></span>

![浏览器中运行的 TestRazor 页](intro-to-web-pages-programming/_static/image2.png)

<span data-ttu-id="2801d-191">查看浏览器中的源。</span><span class="sxs-lookup"><span data-stu-id="2801d-191">Look at the source in the browser.</span></span>

![在浏览器中测试 Razor 页面源文件](intro-to-web-pages-programming/_static/image3.png)

<span data-ttu-id="2801d-193">正如预期从你在上一教程中的体验的 Razor 代码都不是在页中。</span><span class="sxs-lookup"><span data-stu-id="2801d-193">As you expect from your experience in the previous tutorial, none of the Razor code is in the page.</span></span> <span data-ttu-id="2801d-194">您看到是实际显示的值。</span><span class="sxs-lookup"><span data-stu-id="2801d-194">All you see are the actual display values.</span></span> <span data-ttu-id="2801d-195">当运行页面时，实际上对内置到 WebMatrix 的 web 服务器进行请求。</span><span class="sxs-lookup"><span data-stu-id="2801d-195">When you run a page, you're actually making a request to the web server that's built into WebMatrix.</span></span> <span data-ttu-id="2801d-196">收到请求后，ASP.NET 解析所有值和表达式，并将它们的值呈现到页。</span><span class="sxs-lookup"><span data-stu-id="2801d-196">When the request is received, ASP.NET resolves all the values and expressions and renders their values into the page.</span></span> <span data-ttu-id="2801d-197">然后将页发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="2801d-197">It then sends the page to the browser.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="2801d-198">**Razor 和 C#**</span><span class="sxs-lookup"><span data-stu-id="2801d-198">**Razor and C#**</span></span>
> 
> <span data-ttu-id="2801d-199">到目前为止，我们已经说过您正在使用 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="2801d-199">Up to now we've said that you're working with Razor syntax.</span></span> <span data-ttu-id="2801d-200">如此，但并不完整的情景。</span><span class="sxs-lookup"><span data-stu-id="2801d-200">That's true, but it's not the complete story.</span></span> <span data-ttu-id="2801d-201">正在使用的实际编程语言称为*C#*。</span><span class="sxs-lookup"><span data-stu-id="2801d-201">The actual programming language you're using is called *C#*.</span></span> <span data-ttu-id="2801d-202">C# Microsoft 创建了前十多年并已成为一种用于创建 Windows 应用程序的主要编程语言。</span><span class="sxs-lookup"><span data-stu-id="2801d-202">C# was created by Microsoft over a decade ago and has become one of the primary programming languages for creating Windows apps.</span></span> <span data-ttu-id="2801d-203">您已了解有关如何命名变量以及如何创建语句的所有规则都都实际的 C# 语言的所有规则。</span><span class="sxs-lookup"><span data-stu-id="2801d-203">All the rules you've seen about how to name a variable and how to create statements and so on are actually all rules of the C# language.</span></span>
> 
> <span data-ttu-id="2801d-204">Razor 更具体地说是指获得少数几个有关如何将此代码嵌入到页面的约定。</span><span class="sxs-lookup"><span data-stu-id="2801d-204">Razor refers more specifically to the small set of conventions for how you embed this code into a page.</span></span> <span data-ttu-id="2801d-205">例如，使用来标记的页中的代码和使用的约定 @ {} 嵌入的代码块是一个页面的 Razor 方面。</span><span class="sxs-lookup"><span data-stu-id="2801d-205">For example, the convention of using @ to mark code in the page and using @{ } to embed a code block is the Razor aspect of a page.</span></span> <span data-ttu-id="2801d-206">帮助程序也被视为是 Razor 的一部分。</span><span class="sxs-lookup"><span data-stu-id="2801d-206">Helpers are also considered to be part of Razor.</span></span> <span data-ttu-id="2801d-207">在多个位置比只是 ASP.NET Web Pages 中使用 razor 语法。</span><span class="sxs-lookup"><span data-stu-id="2801d-207">Razor syntax is used in more places than just in ASP.NET Web Pages.</span></span> <span data-ttu-id="2801d-208">（例如，它用于 ASP.NET MVC 视图也。）</span><span class="sxs-lookup"><span data-stu-id="2801d-208">(For example, it's used in ASP.NET MVC views as well.)</span></span>
> 
> <span data-ttu-id="2801d-209">我们提起这个是因为如果您查看有关编程 ASP.NET Web Pages 的信息，您会发现大量对 Razor 的引用。</span><span class="sxs-lookup"><span data-stu-id="2801d-209">We mention this because if you look for information about programming ASP.NET Web Pages, you'll find lots of references to Razor.</span></span> <span data-ttu-id="2801d-210">但是，很多这些引用不会应用于您要这样做并因此可能会令人困惑。</span><span class="sxs-lookup"><span data-stu-id="2801d-210">However, a lot of those references don't apply to what you're doing and might therefore be confusing.</span></span> <span data-ttu-id="2801d-211">并且，事实上，许多编程问题实际上会采用有关使用 C# 或使用 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="2801d-211">And in fact, many of your programming questions are really going to be about either working with C# or working with ASP.NET.</span></span> <span data-ttu-id="2801d-212">因此如果您看专门为 Razor 有关的信息，您可能找不到所需的答案。</span><span class="sxs-lookup"><span data-stu-id="2801d-212">So if you look specifically for information about Razor, you might not find the answers you need.</span></span>


## <a name="adding-some-conditional-logic"></a><span data-ttu-id="2801d-213">添加一些条件逻辑</span><span class="sxs-lookup"><span data-stu-id="2801d-213">Adding Some Conditional Logic</span></span>

<span data-ttu-id="2801d-214">有关使用代码页中的强大功能之一是，您可以更改时会发生什么情况基于各种条件。</span><span class="sxs-lookup"><span data-stu-id="2801d-214">One of the great features about using code in a page is that you can change what happens based on various conditions.</span></span> <span data-ttu-id="2801d-215">在本教程的此部分中，您将调整相关更改的页中显示的内容的一些方法。</span><span class="sxs-lookup"><span data-stu-id="2801d-215">In this part of the tutorial, you'll play around with some ways to change what's displayed in the page.</span></span>

<span data-ttu-id="2801d-216">该示例将是简单和精心设计的以便我们可以专注于条件逻辑的某种程度上。</span><span class="sxs-lookup"><span data-stu-id="2801d-216">The example will be simple and somewhat contrived so that we can concentrate on the conditional logic.</span></span> <span data-ttu-id="2801d-217">你将创建的页将执行此操作：</span><span class="sxs-lookup"><span data-stu-id="2801d-217">The page you'll create will do this:</span></span>

- <span data-ttu-id="2801d-218">在页面上显示不同的文本，取决于它是否首次显示的页或是否已单击按钮以提交该页面。</span><span class="sxs-lookup"><span data-stu-id="2801d-218">Show different text on the page depending on whether it's the first time the page is displayed or whether you've clicked a button to submit the page.</span></span> <span data-ttu-id="2801d-219">将第一个条件测试。</span><span class="sxs-lookup"><span data-stu-id="2801d-219">That will be the first conditional test.</span></span>
- <span data-ttu-id="2801d-220">仅当某个值传递的 URL (http://...?show=true) 的查询字符串中显示该消息。</span><span class="sxs-lookup"><span data-stu-id="2801d-220">Display the message only if a certain value is passed in the query string of the URL (http://...?show=true).</span></span> <span data-ttu-id="2801d-221">将第二个条件测试。</span><span class="sxs-lookup"><span data-stu-id="2801d-221">That will be the second conditional test.</span></span>

<span data-ttu-id="2801d-222">在 WebMatrix 中，创建一个页面并将其命名*TestRazorPart2.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="2801d-222">In WebMatrix, create a page and name it *TestRazorPart2.cshtml*.</span></span> <span data-ttu-id="2801d-223">(在功能区中，单击**新建**，选择**CSHTML**，将文件命名，然后单击**确定**。)</span><span class="sxs-lookup"><span data-stu-id="2801d-223">(In the ribbon, click **New**, choose **CSHTML**, name the file, and then click **OK**.)</span></span>

<span data-ttu-id="2801d-224">该页的内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="2801d-224">Replace the contents of that page with the following:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample4.cshtml)]

<span data-ttu-id="2801d-225">在顶部的代码块初始化名为一些文本消息的变量。</span><span class="sxs-lookup"><span data-stu-id="2801d-225">The code block at the top initializes a variable named message with some text.</span></span> <span data-ttu-id="2801d-226">页的正文，消息变量的内容显示在内&lt;p&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="2801d-226">In the body of the page, the contents of the message variable are displayed inside a &lt;p&gt; element.</span></span> <span data-ttu-id="2801d-227">标记还包含&lt;输入&gt;元素来创建**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="2801d-227">The markup also contains an &lt;input&gt; element to create a **Submit** button.</span></span>

<span data-ttu-id="2801d-228">运行页后，可以如何立即查看其工作。</span><span class="sxs-lookup"><span data-stu-id="2801d-228">Run the page to see how it works now.</span></span> <span data-ttu-id="2801d-229">现在，它基本上是一个静态页面，即使您单击**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="2801d-229">For now, it's basically a static page, even if you click the **Submit** button.</span></span>

<span data-ttu-id="2801d-230">返回到 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="2801d-230">Go back to WebMatrix.</span></span> <span data-ttu-id="2801d-231">在代码块中，添加以下突出显示的代码*后*初始化消息的行：</span><span class="sxs-lookup"><span data-stu-id="2801d-231">Inside the code block, add the following highlighted code *after* the line that initializes message:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample5.cshtml?highlight=4-6)]

### <a name="the-if---block"></a><span data-ttu-id="2801d-232">If {} 块</span><span class="sxs-lookup"><span data-stu-id="2801d-232">The if { } block</span></span>

<span data-ttu-id="2801d-233">刚刚添加了 if 条件。</span><span class="sxs-lookup"><span data-stu-id="2801d-233">What you just added was an if condition.</span></span> <span data-ttu-id="2801d-234">在代码中，if 条件必须对于此类结构：</span><span class="sxs-lookup"><span data-stu-id="2801d-234">In code, the if condition has a structure like this:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample6.cs)]

<span data-ttu-id="2801d-235">要测试的条件是在括号中。</span><span class="sxs-lookup"><span data-stu-id="2801d-235">The condition to test is in parentheses.</span></span> <span data-ttu-id="2801d-236">它必须是一个值或返回 true 或 false 的表达式。</span><span class="sxs-lookup"><span data-stu-id="2801d-236">It has to be a value or an expression that returns true or false.</span></span> <span data-ttu-id="2801d-237">如果条件为 true，则 ASP.NET 运行的语句或大括号内的语句。</span><span class="sxs-lookup"><span data-stu-id="2801d-237">If the condition is true, ASP.NET runs the statement or statements that are inside the braces.</span></span> <span data-ttu-id="2801d-238">(这些都是*然后*的一部分*如果-那么*逻辑。)如果条件为 false，则跳过的代码块。</span><span class="sxs-lookup"><span data-stu-id="2801d-238">(Those are the *then* part of the *if-then* logic.) If the condition is false, the block of code is skipped.</span></span>

<span data-ttu-id="2801d-239">以下是一些示例可以在一个 if 测试的条件语句：</span><span class="sxs-lookup"><span data-stu-id="2801d-239">Here are a few examples of conditions you can test in an if statement:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample7.cs)]

<span data-ttu-id="2801d-240">可以使用测试变量值或表达式针对<em>逻辑运算符</em>或<em>比较运算符</em>： 等于 （= =），大于 (&gt;)，小于 (&lt;)，大于或等于 (&gt;=)，并且小于或等于 (&lt;=)。</span><span class="sxs-lookup"><span data-stu-id="2801d-240">You can test variables against values or against expressions by using a <em>logical operator</em> or <em>comparison operator</em>: equal to (==), greater than (&gt;), less than (&lt;), greater than or equal to (&gt;=), and less than or equal to (&lt;=).</span></span> <span data-ttu-id="2801d-241">！ = 运算符表示不等于-例如，如果 (！ = 0) 意味着<em>如果</em> <em>不等于 0</em>。</span><span class="sxs-lookup"><span data-stu-id="2801d-241">The != operator means not equal to — for example, if(a != 0) means <em>if</em> <em>a</em><em>is not equal to 0</em>.</span></span>

> [!NOTE]
> <span data-ttu-id="2801d-242">请确保您注意到等于 （= =） 比较运算符不是与 = 相同。</span><span class="sxs-lookup"><span data-stu-id="2801d-242">Make sure you notice that the comparison operator for equals to (==) is not the same as =.</span></span> <span data-ttu-id="2801d-243">= 运算符仅用于将值分配 (var = 2)。</span><span class="sxs-lookup"><span data-stu-id="2801d-243">The = operator is used only to assign values (var a=2).</span></span> <span data-ttu-id="2801d-244">如果混合使用这些运算符，也会发生错误，否则将显示一些奇怪的结果。</span><span class="sxs-lookup"><span data-stu-id="2801d-244">If you mix these operators up, you'll either get an error or you'll get some strange results.</span></span>


<span data-ttu-id="2801d-245">若要测试的内容是否为 true，完整的语法是 if(IsDone == true)。</span><span class="sxs-lookup"><span data-stu-id="2801d-245">To test whether something is true, the complete syntax is if(IsDone == true).</span></span> <span data-ttu-id="2801d-246">但也可以使用快捷方式 if(IsDone)。</span><span class="sxs-lookup"><span data-stu-id="2801d-246">But you can also use the shortcut if(IsDone).</span></span> <span data-ttu-id="2801d-247">如果没有任何比较运算符，ASP.NET 假定您要测试为 true。</span><span class="sxs-lookup"><span data-stu-id="2801d-247">If there's no comparison operator, ASP.NET assumes that you're testing for true.</span></span>

<span data-ttu-id="2801d-248">！</span><span class="sxs-lookup"><span data-stu-id="2801d-248">The !</span></span> <span data-ttu-id="2801d-249">运算符本身意味着逻辑非。</span><span class="sxs-lookup"><span data-stu-id="2801d-249">operator by itself means a logical NOT.</span></span> <span data-ttu-id="2801d-250">例如，条件 if （！IsPost) 意味着*如果 IsPost 条件不*。</span><span class="sxs-lookup"><span data-stu-id="2801d-250">For example, the condition if(!IsPost) means *if IsPost is not true*.</span></span>

<span data-ttu-id="2801d-251">您可以通过使用逻辑 AND 组合条件 (&amp; &amp;运算符) 或逻辑 OR (| | 运算符)。</span><span class="sxs-lookup"><span data-stu-id="2801d-251">You can combine conditions by using a logical AND (&amp;&amp; operator) or logical OR (|| operator).</span></span> <span data-ttu-id="2801d-252">例如，if 的最后一个条件在前面的示例平均值*如果 FileProcessingIsDone 未设置为 true AND displayMessage 设置为 false*。</span><span class="sxs-lookup"><span data-stu-id="2801d-252">For example, the last of the if conditions in the preceding examples means *if FileProcessingIsDone is not set to true AND displayMessage is set to false*.</span></span>

### <a name="the-else-block"></a><span data-ttu-id="2801d-253">Else 块</span><span class="sxs-lookup"><span data-stu-id="2801d-253">The else block</span></span>

<span data-ttu-id="2801d-254">一个最后一件事情一下，如果基块： 如果块可以跟到 else 块中。</span><span class="sxs-lookup"><span data-stu-id="2801d-254">One final thing about if blocks: an if block can be followed by an else block.</span></span> <span data-ttu-id="2801d-255">到 else 块中非常有用，您需要在条件为 false 时执行不同的代码。</span><span class="sxs-lookup"><span data-stu-id="2801d-255">An else block is useful is you have to execute different code when the condition is false.</span></span> <span data-ttu-id="2801d-256">下面是一个简单的示例：</span><span class="sxs-lookup"><span data-stu-id="2801d-256">Here's a simple example:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample8.cs)]

<span data-ttu-id="2801d-257">更高版本中，使用 else 块也是有用的本系列教程中，将看到一些示例。</span><span class="sxs-lookup"><span data-stu-id="2801d-257">You'll see some examples in later tutorials in this series where using an else block is useful.</span></span>

### <a name="testing-whether-the-request-is-a-submit-post"></a><span data-ttu-id="2801d-258">测试是否对请求进行提交 （文章）</span><span class="sxs-lookup"><span data-stu-id="2801d-258">Testing whether the request is a submit (post)</span></span>

<span data-ttu-id="2801d-259">还有更多，但让我们回到示例中，它具有条件 if(IsPost) {...}。</span><span class="sxs-lookup"><span data-stu-id="2801d-259">There's more, but let's get back to the example, which has the condition if(IsPost){ ... }.</span></span> <span data-ttu-id="2801d-260">IsPost 是实际的当前页的属性。</span><span class="sxs-lookup"><span data-stu-id="2801d-260">IsPost is actually a property of the current page.</span></span> <span data-ttu-id="2801d-261">第一次请求页面时，IsPost 返回 false。</span><span class="sxs-lookup"><span data-stu-id="2801d-261">The first time the page is requested, IsPost returns false.</span></span> <span data-ttu-id="2801d-262">但是，如果单击一个按钮或以其他方式提交页面，其发布，即-IsPost，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="2801d-262">However, if you click a button or otherwise submit the page — that is, you post it — IsPost returns true.</span></span> <span data-ttu-id="2801d-263">因此 IsPost 可以确定您是否正在处理的窗体提交。</span><span class="sxs-lookup"><span data-stu-id="2801d-263">So IsPost lets you determine whether you're dealing with a form submission.</span></span> <span data-ttu-id="2801d-264">（根据 HTTP 谓词 GET 操作，该请求是否 IsPost 返回 false。</span><span class="sxs-lookup"><span data-stu-id="2801d-264">(In terms of HTTP verbs, if the request is a GET operation, IsPost returns false.</span></span> <span data-ttu-id="2801d-265">如果请求的 POST 操作，IsPost 返回 true。）在下一个教程将使用输入窗体，此测试变得特别有用。</span><span class="sxs-lookup"><span data-stu-id="2801d-265">If the request is a POST operation, IsPost returns true.) In a later tutorial you'll work with input forms, where this test becomes particularly useful.</span></span>

<span data-ttu-id="2801d-266">运行页。</span><span class="sxs-lookup"><span data-stu-id="2801d-266">Run the page.</span></span> <span data-ttu-id="2801d-267">由于这是首次接到请求页上，你将看到"这是你已请求页面第一次"。</span><span class="sxs-lookup"><span data-stu-id="2801d-267">Because this is the first time you're requested the page, you see "This is the first time you've requested the page".</span></span> <span data-ttu-id="2801d-268">该字符串是初始化到的消息变量的值。</span><span class="sxs-lookup"><span data-stu-id="2801d-268">That string is the value that you initialized the message variable to.</span></span> <span data-ttu-id="2801d-269">一项 if(IsPost) 测试，但，返回目前，false，所以 if 代码块不会运行。</span><span class="sxs-lookup"><span data-stu-id="2801d-269">There's an if(IsPost) test, but that returns false at the moment, so the code inside the if block doesn't run.</span></span>

<span data-ttu-id="2801d-270">单击**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="2801d-270">Click the **Submit** button.</span></span> <span data-ttu-id="2801d-271">再次请求页面时。</span><span class="sxs-lookup"><span data-stu-id="2801d-271">The page is requested again.</span></span> <span data-ttu-id="2801d-272">作为之前，消息变量将设置为"是第一次..."。</span><span class="sxs-lookup"><span data-stu-id="2801d-272">As before, the message variable is set to "This is the first time ...".</span></span> <span data-ttu-id="2801d-273">但这次测试 if(IsPost) 返回 true，所以 if 代码块将运行。</span><span class="sxs-lookup"><span data-stu-id="2801d-273">But this time, the test if(IsPost) returns true, so the code inside the if block runs.</span></span> <span data-ttu-id="2801d-274">代码更改为不同的值，这是要呈现的标记中的消息变量的值。</span><span class="sxs-lookup"><span data-stu-id="2801d-274">The code changes the value of the message variable to a different value, which is what's rendered in the markup.</span></span>

<span data-ttu-id="2801d-275">现在，添加 if 标记中的条件。</span><span class="sxs-lookup"><span data-stu-id="2801d-275">Now add an if condition in the markup.</span></span> <span data-ttu-id="2801d-276">下面&lt;p&gt;元素，其中包含**提交**按钮，添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="2801d-276">Below the &lt;p&gt; element that contains the **Submit** button, add the following markup:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample9.cshtml)]

<span data-ttu-id="2801d-277">要添加标记内的代码，因此必须首先@。</span><span class="sxs-lookup"><span data-stu-id="2801d-277">You're adding code inside the markup, so you have to start with @.</span></span> <span data-ttu-id="2801d-278">If 则类似于先前添加代码块中的测试。</span><span class="sxs-lookup"><span data-stu-id="2801d-278">Then there's an if test similar to the one you added earlier up in the code block.</span></span> <span data-ttu-id="2801d-279">在大括号，但是，在添加普通 HTML —，至少它很普通，直至到达@DateTime.Now。</span><span class="sxs-lookup"><span data-stu-id="2801d-279">Inside the braces, though, you're adding ordinary HTML — at least, it's ordinary until it gets to @DateTime.Now.</span></span> <span data-ttu-id="2801d-280">这是另一小段 Razor 代码，因此再次需要它的前面添加 @。</span><span class="sxs-lookup"><span data-stu-id="2801d-280">This is another little bit of Razor code, so again you have to add @ in front of it.</span></span>

<span data-ttu-id="2801d-281">这里的一点是，如果在这种情况的代码块顶部和标记中，可以添加。</span><span class="sxs-lookup"><span data-stu-id="2801d-281">The point here is that you can add if conditions in both the code block at the top and in the markup.</span></span> <span data-ttu-id="2801d-282">如果使用 if 条件中的页上，在块内的行正文可以是标记或代码。</span><span class="sxs-lookup"><span data-stu-id="2801d-282">If you use an if condition in the body of the page, the lines inside the block can be markup or code.</span></span> <span data-ttu-id="2801d-283">在这种情况下，只要您混合使用标记和代码，则为 true，因为您必须使用以使它清楚地 ASP.NET 代码所在。</span><span class="sxs-lookup"><span data-stu-id="2801d-283">In that case, and as is true anytime you mix markup and code, you have to use @ to make it clear to ASP.NET where the code is.</span></span>

<span data-ttu-id="2801d-284">运行页面，然后单击**提交**。</span><span class="sxs-lookup"><span data-stu-id="2801d-284">Run the page and click **Submit**.</span></span> <span data-ttu-id="2801d-285">这一次您不仅能看到不同的消息时，提交 （"现在您提交了..."），但看到列出的日期和时间的新消息。</span><span class="sxs-lookup"><span data-stu-id="2801d-285">This time you not only see a different message when you submit ("Now you've submitted ..."), but you see a new message that lists the date and time.</span></span>

![与时间戳后显示在浏览器中运行测试 Razor 2 页上提交](intro-to-web-pages-programming/_static/image4.png)

### <a name="testing-the-value-of-a-query-string"></a><span data-ttu-id="2801d-287">测试查询字符串的值</span><span class="sxs-lookup"><span data-stu-id="2801d-287">Testing the value of a query string</span></span>

<span data-ttu-id="2801d-288">一个测试。</span><span class="sxs-lookup"><span data-stu-id="2801d-288">One more test.</span></span> <span data-ttu-id="2801d-289">此时，你将添加 if 块以便测试某个值名为可能的查询字符串中传递的显示。</span><span class="sxs-lookup"><span data-stu-id="2801d-289">This time, you'll add an if block that tests a value named show that might be passed in the query string.</span></span> <span data-ttu-id="2801d-290">(如下所示： `http://localhost:43097/TestRazorPart2.cshtml?show=true`)，以便该消息，已显示，将更改的页 （"这是首次..."，等等） 如果显示的值为 true，则仅显示。</span><span class="sxs-lookup"><span data-stu-id="2801d-290">(Like this: `http://localhost:43097/TestRazorPart2.cshtml?show=true`) You'll change the page so that the message you've been displaying ("This is the first time ...", etc.) is only displayed if the value of show is true.</span></span>

<span data-ttu-id="2801d-291">在底部 （但内部） 的代码块顶部的页上，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="2801d-291">At the bottom (but inside) the code block at the top of the page, add the following:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample10.cs)]

<span data-ttu-id="2801d-292">完整的代码块现在看起来像下面的示例。</span><span class="sxs-lookup"><span data-stu-id="2801d-292">The complete code block now look like the following example.</span></span> <span data-ttu-id="2801d-293">（请记住，当将代码复制到您的页面后，缩进看起来会有所不同。</span><span class="sxs-lookup"><span data-stu-id="2801d-293">(Remember that when you copy the code into your page, the indentation might look different.</span></span> <span data-ttu-id="2801d-294">但是，不会影响代码的运行方式。）</span><span class="sxs-lookup"><span data-stu-id="2801d-294">But that doesn't affect how the code runs.)</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample11.cshtml)]

<span data-ttu-id="2801d-295">新代码块中的初始化一个变量，名为 showMessage 为 false。</span><span class="sxs-lookup"><span data-stu-id="2801d-295">The new code in the block initializes a variable named showMessage to false.</span></span> <span data-ttu-id="2801d-296">它就会执行 if 测试，以查找的查询字符串中的值。</span><span class="sxs-lookup"><span data-stu-id="2801d-296">It then does an if test to look for a value in the query string.</span></span> <span data-ttu-id="2801d-297">在第一次请求页面时，它具有如下 URL:</span><span class="sxs-lookup"><span data-stu-id="2801d-297">When you first request the page, it has a URL like this one:</span></span>

`http://localhost:43097/TestRazorPart2.cshtml`

<span data-ttu-id="2801d-298">该代码将确定 URL 是否包含名为查询字符串，如 URL 的此版本中显示的变量：</span><span class="sxs-lookup"><span data-stu-id="2801d-298">The code determines whether the URL contains a variable named show in the query string, like this version of the URL:</span></span>

<span data-ttu-id="2801d-299">`http://localhost:43097/TestRazorPart2.cshtml`？ 显示 = true</span><span class="sxs-lookup"><span data-stu-id="2801d-299">`http://localhost:43097/TestRazorPart2.cshtml`?show=true</span></span>

<span data-ttu-id="2801d-300">测试本身来看待请求对象的查询字符串属性。</span><span class="sxs-lookup"><span data-stu-id="2801d-300">The test itself looks at the QueryString property of the Request object.</span></span> <span data-ttu-id="2801d-301">如果查询字符串包含名为的显示，并且该项设置为 true，if 块运行和 showMessage 变量设置为 true。</span><span class="sxs-lookup"><span data-stu-id="2801d-301">If the query string contains an item named show, and if that item is set to true, the if block runs and sets the showMessage variable to true.</span></span>

<span data-ttu-id="2801d-302">还有奥妙在这里，您可以看到。</span><span class="sxs-lookup"><span data-stu-id="2801d-302">There's a trick here, as you can see.</span></span> <span data-ttu-id="2801d-303">正如其名称所指，查询字符串是一个字符串。</span><span class="sxs-lookup"><span data-stu-id="2801d-303">Like the name says, the query string is a string.</span></span> <span data-ttu-id="2801d-304">但是，你可以仅测试 true 和 false 如果您要测试的值为布尔值 (true/false)。</span><span class="sxs-lookup"><span data-stu-id="2801d-304">However, you can only test for true and false if the value you're testing is a Boolean (true/false) value.</span></span> <span data-ttu-id="2801d-305">查询字符串中测试显示变量的值之前，必须将其转换为布尔值。</span><span class="sxs-lookup"><span data-stu-id="2801d-305">Before you can test the value of the show variable in the query string, you have to convert it to a Boolean value.</span></span> <span data-ttu-id="2801d-306">这就是 AsBool 方法作用 — 采用字符串作为输入并将其转换为布尔值。</span><span class="sxs-lookup"><span data-stu-id="2801d-306">That's what the AsBool method does — it takes a string as input and converts it to a Boolean value.</span></span> <span data-ttu-id="2801d-307">很明显，如果字符串为"true"，AsBool 方法将该值转换为 true。</span><span class="sxs-lookup"><span data-stu-id="2801d-307">Clearly, if the string is "true", the AsBool method converts that value to true.</span></span> <span data-ttu-id="2801d-308">如果字符串的值为其他类型，AsBool 返回 false。</span><span class="sxs-lookup"><span data-stu-id="2801d-308">If the value of the string is anything else, AsBool returns false.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="2801d-309">**数据类型和 as （） 方法**</span><span class="sxs-lookup"><span data-stu-id="2801d-309">**Data Types and As() Methods**</span></span>
> 
> <span data-ttu-id="2801d-310">我们已只是说到目前为止创建变量时，使用关键字 var。</span><span class="sxs-lookup"><span data-stu-id="2801d-310">We've only said so far that when you create a variable, you use the keyword var.</span></span> <span data-ttu-id="2801d-311">这不是整篇文章，不过。</span><span class="sxs-lookup"><span data-stu-id="2801d-311">That's not the entire story, though.</span></span> <span data-ttu-id="2801d-312">为了操作值 — 若要添加数字，或连接字符串，或比较日期，或测试为 true/false-C# 必须使用适当的值的内部表示形式。</span><span class="sxs-lookup"><span data-stu-id="2801d-312">In order to manipulate values — to add numbers, or concatenate strings, or compare dates, or test for true/false — C# has to work with an appropriate internal representation of the value.</span></span> <span data-ttu-id="2801d-313">C# 可以*通常*找出该表示形式应为 (即，什么*类型*数据) 基于您所做的值。</span><span class="sxs-lookup"><span data-stu-id="2801d-313">C# can *usually* figure out what that representation should be (that is, what *type* the data is) based on what you're doing with the values.</span></span> <span data-ttu-id="2801d-314">现在，然后，不过，它无法做到这一点。</span><span class="sxs-lookup"><span data-stu-id="2801d-314">Now and then, though, it can't do that.</span></span> <span data-ttu-id="2801d-315">如果没有，您必须通过显式，该值指示如何 C# 应表示的数据帮助解决问题。</span><span class="sxs-lookup"><span data-stu-id="2801d-315">If not, you have to help out by explicitly indicating how C# should represent the data.</span></span> <span data-ttu-id="2801d-316">AsBool 方法执行的 — 它告诉 C# 字符串值"true"或"false"应视为一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="2801d-316">The AsBool method does that — it tells C# that a string value of "true" or "false" should be treated as a Boolean value.</span></span> <span data-ttu-id="2801d-317">存在类似的方法来表示字符串作为其他类型，如 AsInt （视为一个整数）、 AsDateTime （视为日期/时间）、 AsFloat （视为浮点数），等等。</span><span class="sxs-lookup"><span data-stu-id="2801d-317">Similar methods exist to represent strings as other types as well, like AsInt (treat as an integer), AsDateTime (treat as a date/time), AsFloat (treat as a floating-point number), and so on.</span></span> <span data-ttu-id="2801d-318">当您使用它们作为 （） 方法，如果 C# 不能表示的字符串值的请求时，您将看到一个错误。</span><span class="sxs-lookup"><span data-stu-id="2801d-318">When you use these As( ) methods, if C# can't represent the string value as requested, you'll see an error.</span></span>


<span data-ttu-id="2801d-319">在页面的标记中，删除或注释掉此元素 （此处它显示注释掉）：</span><span class="sxs-lookup"><span data-stu-id="2801d-319">In the markup of the page, remove or comment out this element (here it's shown commented out):</span></span>

[!code-html[Main](intro-to-web-pages-programming/samples/sample12.html)]

<span data-ttu-id="2801d-320">你删除或注释掉该文本，添加以下权限：</span><span class="sxs-lookup"><span data-stu-id="2801d-320">Right where you removed or commented out that text, add the following:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample13.cshtml)]

<span data-ttu-id="2801d-321">如果测试显示为分隔开多个变量为 true，是否呈现的&lt;p&gt;具有消息变量的值的元素。</span><span class="sxs-lookup"><span data-stu-id="2801d-321">The if test says that if the showMessage variable is true, render a &lt;p&gt; element with the value of the message variable.</span></span>

### <a name="summary-of-your-conditional-logic"></a><span data-ttu-id="2801d-322">条件逻辑的摘要</span><span class="sxs-lookup"><span data-stu-id="2801d-322">Summary of your conditional logic</span></span>

<span data-ttu-id="2801d-323">如果您不完全确定的只是完成的内容，下面是摘要。</span><span class="sxs-lookup"><span data-stu-id="2801d-323">In case you're not entirely sure of what you've just done, here's a summary.</span></span>

- <span data-ttu-id="2801d-324">消息变量初始化为默认字符串 （"这是首次..."）。</span><span class="sxs-lookup"><span data-stu-id="2801d-324">The message variable is initialized to a default string ("This is the first time ...").</span></span>
- <span data-ttu-id="2801d-325">如果页请求的提交 (post) 结果，消息的值更改为"现在您提交了..."</span><span class="sxs-lookup"><span data-stu-id="2801d-325">If the page request is the result of a submit (post), the value of message is changed to "Now you've submitted ..."</span></span>
- <span data-ttu-id="2801d-326">分隔开多个变量初始化为 false。</span><span class="sxs-lookup"><span data-stu-id="2801d-326">The showMessage variable is initialized to false.</span></span>
- <span data-ttu-id="2801d-327">如果查询字符串包含？ 显示 = showMessage 变量设置为 true，则为 true。</span><span class="sxs-lookup"><span data-stu-id="2801d-327">If the query string contains ?show=true, the showMessage variable is set to true.</span></span>
- <span data-ttu-id="2801d-328">在标记中，如果为 true，showMessage &lt;p&gt;元素呈现，显示消息的值。</span><span class="sxs-lookup"><span data-stu-id="2801d-328">In the markup, if showMessage is true, a &lt;p&gt; element is rendered that shows the value of message.</span></span> <span data-ttu-id="2801d-329">（如果 showMessage 为 false，执行任何操作将呈现在该点的标记中。）</span><span class="sxs-lookup"><span data-stu-id="2801d-329">(If showMessage is false, nothing is rendered at that point in the markup.)</span></span>
- <span data-ttu-id="2801d-330">在标记中，如果请求是 post &lt;p&gt;元素呈现，显示的日期和时间。</span><span class="sxs-lookup"><span data-stu-id="2801d-330">In the markup, if the request is a post, a &lt;p&gt; element is rendered that displays the date and time.</span></span>

<span data-ttu-id="2801d-331">运行页。</span><span class="sxs-lookup"><span data-stu-id="2801d-331">Run the page.</span></span> <span data-ttu-id="2801d-332">没有任何消息，因为 showMessage 为 false，因此在标记中 if(showMessage) 测试返回 false。</span><span class="sxs-lookup"><span data-stu-id="2801d-332">There's no message, because showMessage is false, so in the markup the if(showMessage) test returns false.</span></span>

<span data-ttu-id="2801d-333">单击“提交”。</span><span class="sxs-lookup"><span data-stu-id="2801d-333">Click **Submit**.</span></span> <span data-ttu-id="2801d-334">请参阅日期和时间，但仍没有消息。</span><span class="sxs-lookup"><span data-stu-id="2801d-334">You see the date and time, but still no message.</span></span>

<span data-ttu-id="2801d-335">在浏览器中，转到 URL 框中，并将以下代码添加到 URL 的末尾:？ 显示为 true，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="2801d-335">In your browser, go to the URL box and add the following to the end of the URL: ?show=true and then press Enter.</span></span>

![在浏览器中显示查询字符串 test Razor 2 页](intro-to-web-pages-programming/_static/image5.png)

<span data-ttu-id="2801d-337">将再次显示的页。</span><span class="sxs-lookup"><span data-stu-id="2801d-337">The page is displayed again.</span></span> <span data-ttu-id="2801d-338">（因为更改 URL，这是新的请求，不提交。）单击**提交**试。</span><span class="sxs-lookup"><span data-stu-id="2801d-338">(Because you changed the URL, this is a new request, not a submit.) Click **Submit** again.</span></span> <span data-ttu-id="2801d-339">同样，显示消息原样的日期和时间。</span><span class="sxs-lookup"><span data-stu-id="2801d-339">The message is displayed again, as is the date and time.</span></span>

![查询字符串时，将提交后的测试 Razor 2 页](intro-to-web-pages-programming/_static/image6.png)

<span data-ttu-id="2801d-341">在 URL 中，更改？ 显示 = true 以？ 显示 = false，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="2801d-341">In the URL, change ?show=true to ?show=false and press Enter.</span></span> <span data-ttu-id="2801d-342">重新提交该页面。</span><span class="sxs-lookup"><span data-stu-id="2801d-342">Submit the page again.</span></span> <span data-ttu-id="2801d-343">该页是返回到你的启动方式 — 任何消息。</span><span class="sxs-lookup"><span data-stu-id="2801d-343">The page is back to how you started — no message.</span></span>

<span data-ttu-id="2801d-344">如前文所述，此示例中的逻辑是一个小精心设计的。</span><span class="sxs-lookup"><span data-stu-id="2801d-344">As noted earlier, the logic of this example is a little contrived.</span></span> <span data-ttu-id="2801d-345">但是，如果要在很多页面，转，将此处需要一个或多个您所见的窗体。</span><span class="sxs-lookup"><span data-stu-id="2801d-345">However, if is going to come up in many of your pages, and it will take one or more of the forms you've seen here.</span></span>

## <a name="installing-a-helper-displaying-a-gravatar-image"></a><span data-ttu-id="2801d-346">安装帮助程序 （显示 Gravatar 图像）</span><span class="sxs-lookup"><span data-stu-id="2801d-346">Installing a Helper (Displaying a Gravatar Image)</span></span>

<span data-ttu-id="2801d-347">人们通常希望为在网页上某些任务需要大量的代码，或需要额外知识。</span><span class="sxs-lookup"><span data-stu-id="2801d-347">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="2801d-348">示例： 显示的图的数据;将 Facebook"Like"按钮放置在页;从你的网站; 发送电子邮件裁剪或调整图像; 的大小为您的网站使用 PayPal。</span><span class="sxs-lookup"><span data-stu-id="2801d-348">Examples: displaying a chart for data; putting a Facebook "Like" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="2801d-349">若要能够轻松执行此类目的，ASP.NET Web Pages 使您可以使用*帮助程序*。</span><span class="sxs-lookup"><span data-stu-id="2801d-349">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="2801d-350">帮助器是的组件，为站点安装，以及允许您通过使用几行的 Razor 代码中执行的典型任务。</span><span class="sxs-lookup"><span data-stu-id="2801d-350">Helpers are components that you install for a site and that let you perform typical tasks by using just a few lines of Razor code.</span></span>

<span data-ttu-id="2801d-351">ASP.NET Web Pages 具有内置的几个帮助程序。</span><span class="sxs-lookup"><span data-stu-id="2801d-351">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="2801d-352">但是，使用 NuGet 包管理器提供的包 （加载项） 中提供了许多帮助程序。</span><span class="sxs-lookup"><span data-stu-id="2801d-352">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="2801d-353">NuGet，可以选择要安装的程序包，然后它就会完成安装的所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="2801d-353">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

<span data-ttu-id="2801d-354">在本教程的此部分中，你将安装一个帮助程序，使您可以显示 Gravatar （"全局识别虚拟形象"） 映像。</span><span class="sxs-lookup"><span data-stu-id="2801d-354">In this part of the tutorial, you'll install a helper that lets you display a Gravatar ("globally recognized avatar") image.</span></span> <span data-ttu-id="2801d-355">你将了解以下两种情况。</span><span class="sxs-lookup"><span data-stu-id="2801d-355">You'll learn two things.</span></span> <span data-ttu-id="2801d-356">一个是如何查找和安装帮助程序。</span><span class="sxs-lookup"><span data-stu-id="2801d-356">One is how to find and install a helper.</span></span> <span data-ttu-id="2801d-357">您还将学习如何帮助程序轻松地执行某些您需要使用大量必须自己编写的代码可完成的操作。</span><span class="sxs-lookup"><span data-stu-id="2801d-357">You'll also learn how a helper makes it easy to do something you'd otherwise need to do by using a lot of code you'd have to write yourself.</span></span>

<span data-ttu-id="2801d-358">您可以注册在 Gravatar 网站在自己 Gravatar [ http://www.gravatar.com/ ](http://www.gravatar.com/)，但并不必要创建 Gravatar 帐户以执行教程的此部分。</span><span class="sxs-lookup"><span data-stu-id="2801d-358">You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/), but it is not essential to create a Gravatar account to perform this part of the tutorial.</span></span>

<span data-ttu-id="2801d-359">在 WebMatrix 中，单击**NuGet**按钮。</span><span class="sxs-lookup"><span data-stu-id="2801d-359">In WebMatrix, click the **NuGet** button.</span></span>

![在 WebMatrix 中的 NuGet 库对话框](intro-to-web-pages-programming/_static/image7.png)

<span data-ttu-id="2801d-361">这会启动 NuGet 包管理器，并显示可用的包。</span><span class="sxs-lookup"><span data-stu-id="2801d-361">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="2801d-362">(并非所有包都是帮助程序; 一些将功能添加到 WebMatrix 中本身，一些是其他模板，依次类推。)可能会收到有关版本不兼容的错误消息。</span><span class="sxs-lookup"><span data-stu-id="2801d-362">(Not all of the packages are helpers; some add functionality to WebMatrix itself, some are additional templates, and so on.) You may get an error message about version incompatibility.</span></span> <span data-ttu-id="2801d-363">可以通过单击忽略此错误消息**确定**和继续执行本教程。</span><span class="sxs-lookup"><span data-stu-id="2801d-363">You can ignore this error message by clicking **OK** and proceeding with this tutorial.</span></span>

![在 WebMatrix 中的 NuGet 库对话框](intro-to-web-pages-programming/_static/image8.png)

<span data-ttu-id="2801d-365">在搜索框中，输入"asp.net 帮助器"。</span><span class="sxs-lookup"><span data-stu-id="2801d-365">In the search box, enter "asp.net helpers".</span></span> <span data-ttu-id="2801d-366">NuGet 显示与搜索词匹配的程序包。</span><span class="sxs-lookup"><span data-stu-id="2801d-366">NuGet shows the packages that match the search terms.</span></span>

![在 WebMatrix 中显示包的 NuGet 库](intro-to-web-pages-programming/_static/image9.png)

<span data-ttu-id="2801d-368">ASP.NET Web Helpers Library 包含代码，以简化许多常见任务，包括使用 Gravatar 图像。</span><span class="sxs-lookup"><span data-stu-id="2801d-368">The ASP.NET Web Helpers Library contains code to simplify many common tasks, including the use of Gravatar images.</span></span> <span data-ttu-id="2801d-369">选择**ASP.NET Web Helpers Library**包，然后单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="2801d-369">Select the **ASP.NET Web Helpers Library** package and then click **Install** to launch the installer.</span></span> <span data-ttu-id="2801d-370">选择**是**当系统询问你是否想要安装包，并接受条款以完成安装。</span><span class="sxs-lookup"><span data-stu-id="2801d-370">Select **Yes** when asked if you want to install the package, and accept the terms to complete the installation.</span></span>

<span data-ttu-id="2801d-371">介绍完毕。</span><span class="sxs-lookup"><span data-stu-id="2801d-371">That's it.</span></span> <span data-ttu-id="2801d-372">NuGet 会下载并安装所有内容，包括可能需要的任何其他组件 (*依赖项*)。</span><span class="sxs-lookup"><span data-stu-id="2801d-372">NuGet downloads and installs everything, including any additional components that might be required (*dependencies*).</span></span>

<span data-ttu-id="2801d-373">如果出于某种原因您必须卸载程序的帮助程序，过程也是非常相似。</span><span class="sxs-lookup"><span data-stu-id="2801d-373">If for some reason you have to uninstall a helper, the process is very similar.</span></span> <span data-ttu-id="2801d-374">单击**NuGet**按钮，再单击**已安装**选项卡，然后选择你想要卸载的程序包。</span><span class="sxs-lookup"><span data-stu-id="2801d-374">Click the **NuGet** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="using-a-helper-in-a-page"></a><span data-ttu-id="2801d-375">在页面中使用一个帮助程序</span><span class="sxs-lookup"><span data-stu-id="2801d-375">Using a Helper in a Page</span></span>

<span data-ttu-id="2801d-376">现在，您将使用刚安装的帮助器。</span><span class="sxs-lookup"><span data-stu-id="2801d-376">Now you'll use the helper that you just installed.</span></span> <span data-ttu-id="2801d-377">向页面添加一个帮助程序的过程是类似的大多数帮助程序。</span><span class="sxs-lookup"><span data-stu-id="2801d-377">The process for adding a helper to a page is similar for most helpers.</span></span>

<span data-ttu-id="2801d-378">在 WebMatrix 中，创建一个页面并将其命名*GravatarTest.cshml*。</span><span class="sxs-lookup"><span data-stu-id="2801d-378">In WebMatrix, create a page and name it *GravatarTest.cshml*.</span></span> <span data-ttu-id="2801d-379">（要创建一个特殊网页来测试帮助器，但可以在你的站点中的任意页面中使用帮助器。）</span><span class="sxs-lookup"><span data-stu-id="2801d-379">(You're creating a special page to test the helper, but you can use helpers in any page in your site.)</span></span>

<span data-ttu-id="2801d-380">内部&lt;正文&gt;元素中，添加&lt;div&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="2801d-380">Inside the &lt;body&gt; element, add a &lt;div&gt; element.</span></span> <span data-ttu-id="2801d-381">内部&lt;div&gt;元素中，键入：</span><span class="sxs-lookup"><span data-stu-id="2801d-381">Inside the &lt;div&gt; element, type this:</span></span>

<span data-ttu-id="2801d-382">@Gravatar。</span><span class="sxs-lookup"><span data-stu-id="2801d-382">@Gravatar.</span></span>

<span data-ttu-id="2801d-383">@ 字符是你已使用标记 Razor 代码中的相同字符。</span><span class="sxs-lookup"><span data-stu-id="2801d-383">The @ character is the same character you've been using to mark Razor code.</span></span> <span data-ttu-id="2801d-384">**Gravatar**是您正在使用的帮助程序对象。</span><span class="sxs-lookup"><span data-stu-id="2801d-384">**Gravatar** is the helper object that you're working with.</span></span>

<span data-ttu-id="2801d-385">只要键入句点 （.），WebMatrix 将显示一系列*方法*Gravatar 帮助程序提供 （函数）：</span><span class="sxs-lookup"><span data-stu-id="2801d-385">As soon as you type the period (.), WebMatrix displays a list of *methods* (functions) that the Gravatar helper makes available:</span></span>

![Gravatar 帮助程序 IntelliSense 下拉列表](intro-to-web-pages-programming/_static/image10.png)

<span data-ttu-id="2801d-387">此功能被称为*IntelliSense*。</span><span class="sxs-lookup"><span data-stu-id="2801d-387">This feature is known as *IntelliSense*.</span></span> <span data-ttu-id="2801d-388">它通过提供上下文相应选项来帮助你的代码。</span><span class="sxs-lookup"><span data-stu-id="2801d-388">It helps you code by providing context-appropriate choices.</span></span> <span data-ttu-id="2801d-389">IntelliSense 适用于 HTML、 CSS、 ASP.NET 代码、 JavaScript 和在 WebMatrix 中支持其他语言。</span><span class="sxs-lookup"><span data-stu-id="2801d-389">IntelliSense works with HTML, CSS, ASP.NET code, JavaScript, and other languages that are supported in WebMatrix.</span></span> <span data-ttu-id="2801d-390">它是另一项功能，简化了开发在 WebMatrix 中的网页。</span><span class="sxs-lookup"><span data-stu-id="2801d-390">It's another feature that makes it easier to develop web pages in WebMatrix.</span></span>

<span data-ttu-id="2801d-391">按 G 上于键盘，并且您看到 IntelliSense 查找 GetHtml 方法。</span><span class="sxs-lookup"><span data-stu-id="2801d-391">Press G on the keyboard, and you see that IntelliSense finds the GetHtml method.</span></span> <span data-ttu-id="2801d-392">按 Tab 键。IntelliSense 为您插入所选的方法 (GetHtml)。</span><span class="sxs-lookup"><span data-stu-id="2801d-392">Press Tab. IntelliSense inserts the selected method (GetHtml) for you.</span></span> <span data-ttu-id="2801d-393">键入左括号，并请注意，会自动添加右括号。</span><span class="sxs-lookup"><span data-stu-id="2801d-393">Type an open parenthesis, and notice that the closing parenthesis is automatically added.</span></span> <span data-ttu-id="2801d-394">在引号内的两个括号之间键入您的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="2801d-394">Type your email address in quotation marks between the two parenthesis.</span></span> <span data-ttu-id="2801d-395">如果你有 Gravatar 帐户，将返回个人资料图片。</span><span class="sxs-lookup"><span data-stu-id="2801d-395">If you have a Gravatar account, your profile picture will be returned.</span></span> <span data-ttu-id="2801d-396">如果没有 Gravatar 帐户，则返回默认图像。</span><span class="sxs-lookup"><span data-stu-id="2801d-396">If you do not have a Gravatar account, a default image is returned.</span></span> <span data-ttu-id="2801d-397">完成后，在行如下所示：</span><span class="sxs-lookup"><span data-stu-id="2801d-397">When you're done, the line looks like this:</span></span>

[!code-css[Main](intro-to-web-pages-programming/samples/sample14.css)]

<span data-ttu-id="2801d-398">现在在浏览器中查看的页面。</span><span class="sxs-lookup"><span data-stu-id="2801d-398">Now view the page in a browser.</span></span> <span data-ttu-id="2801d-399">您的图片或默认图像将显示，具体取决于是否具有 Gravatar 帐户。</span><span class="sxs-lookup"><span data-stu-id="2801d-399">Either your picture or the default image is displayed, depending on whether you have a Gravatar account.</span></span>

![Gravatar](intro-to-web-pages-programming/_static/image11.png) ![默认映像](intro-to-web-pages-programming/_static/image12.png)

<span data-ttu-id="2801d-402">若要了解的内容的帮助程序为你做，在浏览器中查看页面的源代码。</span><span class="sxs-lookup"><span data-stu-id="2801d-402">To get an idea of what the helper is doing for you, view the source of the page in the browser.</span></span> <span data-ttu-id="2801d-403">随 HTML，您的页面中，您将看到将标识符包含一个 image 元素。</span><span class="sxs-lookup"><span data-stu-id="2801d-403">Along with the HTML that you had in your page, you see an image element that includes an identifier.</span></span> <span data-ttu-id="2801d-404">这是帮助器呈现到页中有位置的位置的代码@Gravatar.GetHtml。</span><span class="sxs-lookup"><span data-stu-id="2801d-404">This is code that the helper rendered into the page at the place where you had @Gravatar.GetHtml.</span></span> <span data-ttu-id="2801d-405">帮助者花费了提供和生成的代码与直接 Gravatar 以便获取正确的映像提供帐户的信息。</span><span class="sxs-lookup"><span data-stu-id="2801d-405">The helper took the information you provided and generated the code that talks directly to Gravatar in order to get back the correct image for supplied account.</span></span>

<span data-ttu-id="2801d-406">GetHtml 方法还可以通过提供其他参数自定义映像。</span><span class="sxs-lookup"><span data-stu-id="2801d-406">The GetHtml method also enables you to customize the image by providing other parameters.</span></span> <span data-ttu-id="2801d-407">下面的代码演示如何请求映像具有宽度和高度为 40 像素，并使用名为指定的默认映像**wavatar**如果指定的帐户不存在。</span><span class="sxs-lookup"><span data-stu-id="2801d-407">The following code shows how to request an image has a width and height of 40 pixels, and uses a specified default image named **wavatar** if the specified account does not exist.</span></span>

[!code-javascript[Main](intro-to-web-pages-programming/samples/sample15.js)]

<span data-ttu-id="2801d-408">此代码生成类似于以下的结果 （将随机有所不同的默认映像） 的内容。</span><span class="sxs-lookup"><span data-stu-id="2801d-408">This code produces something like the following result (the default image will randomly vary).</span></span>

![](intro-to-web-pages-programming/_static/image13.png)

## <a name="coming-up-next"></a><span data-ttu-id="2801d-409">即将推出下一步</span><span class="sxs-lookup"><span data-stu-id="2801d-409">Coming Up Next</span></span>

<span data-ttu-id="2801d-410">若要使此教程短，我们可以专注于仅的一些基本知识。</span><span class="sxs-lookup"><span data-stu-id="2801d-410">To keep this tutorial short, we had to focus on only a few basics.</span></span> <span data-ttu-id="2801d-411">当然，这里有*很多*Razor 和 C# 的信息。</span><span class="sxs-lookup"><span data-stu-id="2801d-411">Naturally, there's a *lot* more to Razor and C#.</span></span> <span data-ttu-id="2801d-412">你将了解详细信息作为您经历这些教程。</span><span class="sxs-lookup"><span data-stu-id="2801d-412">You'll learn more as you go through these tutorials.</span></span> <span data-ttu-id="2801d-413">如果有兴趣学习有关 Razor 和 C# 的编程方面的详细信息稍后再试，则可以读取的更全面的介绍： [ASP.NET Web 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkID=202890)。</span><span class="sxs-lookup"><span data-stu-id="2801d-413">If you're interested in learning more about the programming aspects of Razor and C# right now, you can read a more thorough introduction here: [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=202890).</span></span>

<span data-ttu-id="2801d-414">下一教程将介绍使用数据库。</span><span class="sxs-lookup"><span data-stu-id="2801d-414">The next tutorial introduces you to working with a database.</span></span> <span data-ttu-id="2801d-415">在该教程中，将开始创建允许你列出你最喜爱的电影的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="2801d-415">In that tutorial, you'll begin creating the sample application that lets you list your favorite movies.</span></span>

## <a name="complete-listing-for-testrazor-page"></a><span data-ttu-id="2801d-416">TestRazor 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="2801d-416">Complete Listing for TestRazor Page</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample16.cshtml)]

## <a name="complete-listing-for-testrazorpart2-page"></a><span data-ttu-id="2801d-417">TestRazorPart2 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="2801d-417">Complete Listing for TestRazorPart2 Page</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample17.cshtml)]

## <a name="complete-listing-for-gravatartest-page"></a><span data-ttu-id="2801d-418">GravatarTest 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="2801d-418">Complete Listing for GravatarTest Page</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample18.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="2801d-419">其他资源</span><span class="sxs-lookup"><span data-stu-id="2801d-419">Additional Resources</span></span>

- [<span data-ttu-id="2801d-420">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="2801d-420">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- [<span data-ttu-id="2801d-421">Twitter 帮助程序</span><span class="sxs-lookup"><span data-stu-id="2801d-421">Twitter helper</span></span>](../../ui-layouts-and-themes/twitter-helper.md)

> [!div class="step-by-step"]
> <span data-ttu-id="2801d-422">[上一页](getting-started.md)
> [下一页](displaying-data.md)</span><span class="sxs-lookup"><span data-stu-id="2801d-422">[Previous](getting-started.md)
[Next](displaying-data.md)</span></span>
