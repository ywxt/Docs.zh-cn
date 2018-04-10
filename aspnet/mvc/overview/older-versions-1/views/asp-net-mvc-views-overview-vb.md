---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: ASP.NET MVC 视图概述 (VB) |Microsoft 文档
author: StephenWalther
description: 有何它区别从 HTML 页和 ASP.NET MVC 视图是什么？ 在本教程中，Stephen Walther 向您介绍视图，并演示如何 t...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2008
ms.topic: article
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: a64c70851d13b923964dfd1cf3bad55612ae0d0f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="aspnet-mvc-views-overview-vb"></a><span data-ttu-id="039b0-104">ASP.NET MVC 视图概述 (VB)</span><span class="sxs-lookup"><span data-stu-id="039b0-104">ASP.NET MVC Views Overview (VB)</span></span>
====================
<span data-ttu-id="039b0-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="039b0-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="039b0-106">有何它区别从 HTML 页和 ASP.NET MVC 视图是什么？</span><span class="sxs-lookup"><span data-stu-id="039b0-106">What is an ASP.NET MVC View and how does it differ from a HTML page?</span></span> <span data-ttu-id="039b0-107">在本教程中，Stephen Walther 视图向你介绍并演示了如何，你可以充分利用查看数据和 HTML 的视图中的帮助器。</span><span class="sxs-lookup"><span data-stu-id="039b0-107">In this tutorial, Stephen Walther introduces you to Views and demonstrates how you can take advantage of View Data and HTML Helpers within a View.</span></span>


<span data-ttu-id="039b0-108">本教程的目的是为你提供对 ASP.NET MVC 视图、 查看数据和 HTML 帮助器的简短介绍。</span><span class="sxs-lookup"><span data-stu-id="039b0-108">The purpose of this tutorial is to provide you with a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="039b0-109">本教程结束时，应了解如何创建新视图、 将数据从控制器传递了一个视图，和使用 HTML 帮助器以生成在视图中的内容。</span><span class="sxs-lookup"><span data-stu-id="039b0-109">By the end of this tutorial, you should understand how to create new views, pass data from a controller to a view, and use HTML Helpers to generate content in a view.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="039b0-110">了解视图</span><span class="sxs-lookup"><span data-stu-id="039b0-110">Understanding Views</span></span>

<span data-ttu-id="039b0-111">与 ASP.NET 或 Active Server Pages，不同的 ASP.NET MVC 不包括直接对应于页的任何内容。</span><span class="sxs-lookup"><span data-stu-id="039b0-111">Unlike ASP.NET or Active Server Pages, ASP.NET MVC does not include anything that directly corresponds to a page.</span></span> <span data-ttu-id="039b0-112">在 ASP.NET MVC 应用程序，没有一个页面对应于你的浏览器的地址栏中键入 URL 中的路径的磁盘上。</span><span class="sxs-lookup"><span data-stu-id="039b0-112">In an ASP.NET MVC application, there is not a page on disk that corresponds to the path in the URL that you type into the address bar of your browser.</span></span> <span data-ttu-id="039b0-113">在 ASP.NET MVC 应用程序页的最佳捷径是调用*视图*。</span><span class="sxs-lookup"><span data-stu-id="039b0-113">The closest thing to a page in an ASP.NET MVC application is something called a *view*.</span></span>

<span data-ttu-id="039b0-114">ASP.NET MVC 应用程序中传入的浏览器请求将映射到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="039b0-114">In an ASP.NET MVC application, incoming browser requests are mapped to controller actions.</span></span> <span data-ttu-id="039b0-115">控制器操作可能会返回一个视图。</span><span class="sxs-lookup"><span data-stu-id="039b0-115">A controller action might return a view.</span></span> <span data-ttu-id="039b0-116">但是，控制器操作可能会执行一些其他类型的操作时，例如将你重定向到另一个控制器操作。</span><span class="sxs-lookup"><span data-stu-id="039b0-116">However, a controller action might perform some other type of action such as redirecting you to another controller action.</span></span>

<span data-ttu-id="039b0-117">列表 1 包含名为 HomeController 的简单控制器。</span><span class="sxs-lookup"><span data-stu-id="039b0-117">Listing 1 contains a simple controller named the HomeController.</span></span> <span data-ttu-id="039b0-118">HomeController 公开名为 index （） 和 Details() 的两个控制器操作。</span><span class="sxs-lookup"><span data-stu-id="039b0-118">The HomeController exposes two controller actions named Index() and Details().</span></span>

<span data-ttu-id="039b0-119">**列表 1-HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="039b0-119">**Listing 1 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

<span data-ttu-id="039b0-120">你可以调用的第一个操作，index （） 操作中，通过在浏览器地址栏中键入以下 URL:</span><span class="sxs-lookup"><span data-stu-id="039b0-120">You can invoke the first action, the Index() action, by typing the following URL into your browser address bar:</span></span>

<span data-ttu-id="039b0-121">/ Home/Index</span><span class="sxs-lookup"><span data-stu-id="039b0-121">/Home/Index</span></span>

<span data-ttu-id="039b0-122">你可以调用第二个操作，Details() 操作中，通过将此地址键入你的浏览器：</span><span class="sxs-lookup"><span data-stu-id="039b0-122">You can invoke the second action, the Details() action, by typing this address into your browser:</span></span>

<span data-ttu-id="039b0-123">/ 主页/详细信息</span><span class="sxs-lookup"><span data-stu-id="039b0-123">/Home/Details</span></span>

<span data-ttu-id="039b0-124">Index （） 操作返回的视图。</span><span class="sxs-lookup"><span data-stu-id="039b0-124">The Index() action returns a view.</span></span> <span data-ttu-id="039b0-125">你创建的大多数操作将返回视图。</span><span class="sxs-lookup"><span data-stu-id="039b0-125">Most actions that you create will return views.</span></span> <span data-ttu-id="039b0-126">但是，操作可以返回其他类型的操作结果。</span><span class="sxs-lookup"><span data-stu-id="039b0-126">However, an action can return other types of action results.</span></span> <span data-ttu-id="039b0-127">例如，Details() 操作返回传入的请求重定向到 index （） 操作 RedirectToActionResult。</span><span class="sxs-lookup"><span data-stu-id="039b0-127">For example, the Details() action returns a RedirectToActionResult that redirects incoming request to the Index() action.</span></span>

<span data-ttu-id="039b0-128">Index （） 操作包含以下的单个代码行：</span><span class="sxs-lookup"><span data-stu-id="039b0-128">The Index() action contains the following single line of code:</span></span>

<span data-ttu-id="039b0-129">View()</span><span class="sxs-lookup"><span data-stu-id="039b0-129">View()</span></span>

<span data-ttu-id="039b0-130">以下代码行将返回必须位于你的 web 服务器上的以下路径的视图：</span><span class="sxs-lookup"><span data-stu-id="039b0-130">This line of code returns a view that must be located at the following path on your web server:</span></span>

<span data-ttu-id="039b0-131">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="039b0-131">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="039b0-132">该视图的路径可以推断出的控制器名称和控制器操作的名称。</span><span class="sxs-lookup"><span data-stu-id="039b0-132">The path to the view is inferred from the name of the controller and the name of the controller action.</span></span>

<span data-ttu-id="039b0-133">如果你愿意，你可以为显式有关视图。</span><span class="sxs-lookup"><span data-stu-id="039b0-133">If you prefer, you can be explicit about the view.</span></span> <span data-ttu-id="039b0-134">以下代码行返回名为 Fred 的视图：</span><span class="sxs-lookup"><span data-stu-id="039b0-134">The following line of code returns a view named Fred :</span></span>

<span data-ttu-id="039b0-135">视图 (Fred)</span><span class="sxs-lookup"><span data-stu-id="039b0-135">View( Fred )</span></span>

<span data-ttu-id="039b0-136">当执行此代码行时，视图将返回从以下路径：</span><span class="sxs-lookup"><span data-stu-id="039b0-136">When this line of code is executed, a view is returned from the following path:</span></span>

<span data-ttu-id="039b0-137">\Views\Home\Fred.aspx</span><span class="sxs-lookup"><span data-stu-id="039b0-137">\Views\Home\Fred.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="039b0-138">如果你打算创建 ASP.NET MVC 应用程序的单元测试然后它是一个好办法应明确视图名称。</span><span class="sxs-lookup"><span data-stu-id="039b0-138">If you plan to create unit tests for your ASP.NET MVC application then it is a good idea to be explicit about view names.</span></span> <span data-ttu-id="039b0-139">这样一来，你可以创建单元测试验证预期的视图已由控制器操作。</span><span class="sxs-lookup"><span data-stu-id="039b0-139">That way, you can create a unit test to verify that the expected view was returned by a controller action.</span></span>


## <a name="adding-content-to-a-view"></a><span data-ttu-id="039b0-140">将内容添加到视图</span><span class="sxs-lookup"><span data-stu-id="039b0-140">Adding Content to a View</span></span>

<span data-ttu-id="039b0-141">视图是一种标准 (X) 可以包含脚本的 HTML 文档。</span><span class="sxs-lookup"><span data-stu-id="039b0-141">A view is a standard (X)HTML document that can contain scripts.</span></span> <span data-ttu-id="039b0-142">您可以使用脚本将动态内容添加到视图。</span><span class="sxs-lookup"><span data-stu-id="039b0-142">You use scripts to add dynamic content to a view.</span></span>

<span data-ttu-id="039b0-143">例如，清单 2 中的视图显示当前日期和时间。</span><span class="sxs-lookup"><span data-stu-id="039b0-143">For example, the view in Listing 2 displays the current date and time.</span></span>

<span data-ttu-id="039b0-144">**列出 2-\Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="039b0-144">**Listing 2 - \Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

<span data-ttu-id="039b0-145">请注意，列出 2 中的 HTML 页面的正文包含以下脚本：</span><span class="sxs-lookup"><span data-stu-id="039b0-145">Notice that the body of the HTML page in Listing 2 contains the following script:</span></span>

<span data-ttu-id="039b0-146">&lt;% Response.Write(DateTime.Now)%&gt;</span><span class="sxs-lookup"><span data-stu-id="039b0-146">&lt;% Response.Write(DateTime.Now)%&gt;</span></span>

<span data-ttu-id="039b0-147">使用脚本分隔符&lt;%和 %&gt;来标记的开头和末尾脚本。</span><span class="sxs-lookup"><span data-stu-id="039b0-147">You use the script delimiters &lt;% and %&gt; to mark the beginning and end of a script.</span></span> <span data-ttu-id="039b0-148">在 Visual basic 中编写此脚本。</span><span class="sxs-lookup"><span data-stu-id="039b0-148">This script is written in Visual basic.</span></span> <span data-ttu-id="039b0-149">它通过调用 Response.Write() 方法，以呈现到浏览器的内容显示了当前日期和时间。</span><span class="sxs-lookup"><span data-stu-id="039b0-149">It displays the current date and time by calling the Response.Write() method to render content to the browser.</span></span> <span data-ttu-id="039b0-150">脚本分隔符&lt;%和 %&gt;可以用于执行一个或多个语句。</span><span class="sxs-lookup"><span data-stu-id="039b0-150">The script delimiters &lt;% and %&gt; can be used to execute one or more statements.</span></span>

<span data-ttu-id="039b0-151">由于如此频繁调用 Response.Write()，Microsoft 为你提供一种快捷方式为调用 Response.Write() 方法。</span><span class="sxs-lookup"><span data-stu-id="039b0-151">Since you call Response.Write() so often, Microsoft provides you with a shortcut for calling the Response.Write() method.</span></span> <span data-ttu-id="039b0-152">列出 3 中的视图使用分隔符&lt;%= 和 %&gt;作为调用 Response.Write() 的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="039b0-152">The view in Listing 3 uses the delimiters &lt;%= and %&gt; as a shortcut for calling Response.Write().</span></span>

<span data-ttu-id="039b0-153">**列出 3-Views\Home\Index2.aspx**</span><span class="sxs-lookup"><span data-stu-id="039b0-153">**Listing 3 - Views\Home\Index2.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

<span data-ttu-id="039b0-154">可以使用任何.NET 语言生成动态内容视图中。</span><span class="sxs-lookup"><span data-stu-id="039b0-154">You can use any .NET language to generate dynamic content in a view.</span></span> <span data-ttu-id="039b0-155">通常情况下，你将使用 Visual Basic.NET 或 C# 编写你的控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="039b0-155">Normally, you�ll use either Visual Basic .NET or C# to write your controllers and views.</span></span>

## <a name="using-html-helpers-to-generate-view-content"></a><span data-ttu-id="039b0-156">使用 HTML 帮助器生成查看内容</span><span class="sxs-lookup"><span data-stu-id="039b0-156">Using HTML Helpers to Generate View Content</span></span>

<span data-ttu-id="039b0-157">若要更加轻松地将内容添加到视图，你可以利用称为*的 HTML 帮助器*。</span><span class="sxs-lookup"><span data-stu-id="039b0-157">To make it easier to add content to a view, you can take advantage of something called an *HTML Helper*.</span></span> <span data-ttu-id="039b0-158">HTML 帮助器，通常情况下，是生成的字符串的方法。</span><span class="sxs-lookup"><span data-stu-id="039b0-158">An HTML Helper, typically, is a method that generates a string.</span></span> <span data-ttu-id="039b0-159">HTML 帮助器可用于生成如文本框、 链接、 下拉列表和列表框的标准 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="039b0-159">You can use HTML Helpers to generate standard HTML elements such as textboxes, links, dropdown lists, and list boxes.</span></span>

<span data-ttu-id="039b0-160">例如，三个 HTML 帮助器-列出 4 利用中的视图的 BeginForm()、 TextBox() 和 Password() 帮助器-生成登录名窗体 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="039b0-160">For example, the view in Listing 4 takes advantage of three HTML Helpers -- the BeginForm(), the TextBox() and Password() helpers -- to generate a Login form (see Figure 1).</span></span>

<span data-ttu-id="039b0-161">**列出 4--\Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="039b0-161">**Listing 4 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]


<span data-ttu-id="039b0-162">[![新项目对话框](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="039b0-162">[![The New Project dialog box](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="039b0-163">**图 01**： 一个标准的登录窗体 ([单击以查看实际尺寸的图像](asp-net-mvc-views-overview-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="039b0-163">**Figure 01**: A standard Login form ([Click to view full-size image](asp-net-mvc-views-overview-vb/_static/image2.png))</span></span>


<span data-ttu-id="039b0-164">在视图的 Html 属性上调用所有 HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="039b0-164">All of the HTML Helpers methods are called on the Html property of the view.</span></span> <span data-ttu-id="039b0-165">例如，通过调用 Html.TextBox() 方法呈现文本框。</span><span class="sxs-lookup"><span data-stu-id="039b0-165">For example, you render a TextBox by calling the Html.TextBox() method.</span></span>

<span data-ttu-id="039b0-166">请注意，使用脚本分隔符&lt;%= 和 %&gt;时调用的 Html.TextBox() 和 Html.Password() 帮助器。</span><span class="sxs-lookup"><span data-stu-id="039b0-166">Notice that you use the script delimiters &lt;%= and %&gt; when calling both the Html.TextBox() and Html.Password() helpers.</span></span> <span data-ttu-id="039b0-167">这些帮助器只返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="039b0-167">These helpers simply return a string.</span></span> <span data-ttu-id="039b0-168">你需要调用 Response.Write() 以呈现到浏览器的字符串。</span><span class="sxs-lookup"><span data-stu-id="039b0-168">You need to call Response.Write() in order to render the string to the browser.</span></span>

<span data-ttu-id="039b0-169">使用 HTML 帮助器方法是可选的。</span><span class="sxs-lookup"><span data-stu-id="039b0-169">Using HTML Helper methods is optional.</span></span> <span data-ttu-id="039b0-170">它们使你更轻松通过减少的 HTML 和你需要编写的脚本。</span><span class="sxs-lookup"><span data-stu-id="039b0-170">They make your life easier by reducing the amount of HTML and script that you need to write.</span></span> <span data-ttu-id="039b0-171">列出 5 中的视图将列出 4 中的视图与完全相同的方式呈现而无需使用 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="039b0-171">The view in Listing 5 renders the exact same form as the view in Listing 4 without using HTML Helpers.</span></span>

<span data-ttu-id="039b0-172">**Listing 5 -- \Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="039b0-172">**Listing 5 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

<span data-ttu-id="039b0-173">此外可以创建你自己的 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="039b0-173">You also have the option of creating your own HTML Helpers.</span></span> <span data-ttu-id="039b0-174">例如，你可以创建一个 HTML 表中自动显示一组数据库记录的 GridView() 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="039b0-174">For example, you can create a GridView() helper method that displays a set of database records in an HTML table automatically.</span></span> <span data-ttu-id="039b0-175">我们在本教程中浏览本主题**创建自定义 HTML 帮助器**。</span><span class="sxs-lookup"><span data-stu-id="039b0-175">We explore this topic in the tutorial **Creating Custom HTML Helpers**.</span></span>

## <a name="using-view-data-to-pass-data-to-a-view"></a><span data-ttu-id="039b0-176">使用视图数据来将数据传递到视图</span><span class="sxs-lookup"><span data-stu-id="039b0-176">Using View Data to Pass Data to a View</span></span>

<span data-ttu-id="039b0-177">使用视图数据将从控制器的数据传递到视图。</span><span class="sxs-lookup"><span data-stu-id="039b0-177">You use view data to pass data from a controller to a view.</span></span> <span data-ttu-id="039b0-178">将像通过邮件发送的包的视图数据。</span><span class="sxs-lookup"><span data-stu-id="039b0-178">Think of view data like a package that you send through the mail.</span></span> <span data-ttu-id="039b0-179">必须使用此包发送从控制器中传递给视图的所有数据。</span><span class="sxs-lookup"><span data-stu-id="039b0-179">All data passed from a controller to a view must be sent using this package.</span></span> <span data-ttu-id="039b0-180">例如，列出 6 中的控制器中添加消息来查看数据。</span><span class="sxs-lookup"><span data-stu-id="039b0-180">For example, the controller in Listing 6 adds a message to view data.</span></span>

<span data-ttu-id="039b0-181">**列出 6-ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="039b0-181">**Listing 6 - ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

<span data-ttu-id="039b0-182">控制器 ViewData 属性表示名称和值对的集合。</span><span class="sxs-lookup"><span data-stu-id="039b0-182">The controller ViewData property represents a collection of name and value pairs.</span></span> <span data-ttu-id="039b0-183">在列出 6 中，index （） 方法将项添加到名为 Hello World 的值的消息视图数据收集 ！。</span><span class="sxs-lookup"><span data-stu-id="039b0-183">In Listing 6, the Index() method adds an item to the view data collection named message with the value Hello World!.</span></span> <span data-ttu-id="039b0-184">当视图返回由 index （） 方法时，查看数据被自动传递到视图中。</span><span class="sxs-lookup"><span data-stu-id="039b0-184">When the view is returned by the Index() method, the view data is passed to the view automatically.</span></span>

<span data-ttu-id="039b0-185">列出 7 中的视图从查看数据中检索消息，并呈现到浏览器的消息。</span><span class="sxs-lookup"><span data-stu-id="039b0-185">The view in Listing 7 retrieves the message from the view data and renders the message to the browser.</span></span>

<span data-ttu-id="039b0-186">**Listing 7 -- \Views\Product\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="039b0-186">**Listing 7 -- \Views\Product\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

<span data-ttu-id="039b0-187">请注意视图充分利用的 Html.Encode() HTML 帮助器方法，在呈现消息时。</span><span class="sxs-lookup"><span data-stu-id="039b0-187">Notice that the view takes advantage of the Html.Encode() HTML Helper method when rendering the message.</span></span> <span data-ttu-id="039b0-188">Html.Encode() HTML 帮助器特殊字符进行编码如&lt;和&gt;转换是安全网页中显示的字符。</span><span class="sxs-lookup"><span data-stu-id="039b0-188">The Html.Encode() HTML Helper encodes special characters such as &lt; and &gt; into characters that are safe to display in a web page.</span></span> <span data-ttu-id="039b0-189">每当你呈现用户提交到网站的内容，应该对要防止 JavaScript 注入式攻击的内容进行编码。</span><span class="sxs-lookup"><span data-stu-id="039b0-189">Whenever you render content that a user submits to a website, you should encode the content to prevent JavaScript injection attacks.</span></span>

<span data-ttu-id="039b0-190">(因为我们在创建的消息自行 ProductController，我们不真正需要对消息进行编码。</span><span class="sxs-lookup"><span data-stu-id="039b0-190">(Because we created the message ourselves in the ProductController, we don�t really need to encode the message.</span></span> <span data-ttu-id="039b0-191">但是，它是一个好习惯时从查看数据的视图中显示内容检索始终调用 Html.Encode() 方法。）</span><span class="sxs-lookup"><span data-stu-id="039b0-191">However, it is a good habit to always call the Html.Encode() method when displaying content retrieved from view data within a view.)</span></span>

<span data-ttu-id="039b0-192">在列出 7 中，我们利用要从控制器的一个简单的字符串消息传递到视图的视图数据。</span><span class="sxs-lookup"><span data-stu-id="039b0-192">In Listing 7, we took advantage of view data to pass a simple string message from a controller to a view.</span></span> <span data-ttu-id="039b0-193">此外可以使用视图数据将其他类型的数据，如数据库记录，从到视图控制器的集合。</span><span class="sxs-lookup"><span data-stu-id="039b0-193">You also can use view data to pass other types of data, such as a collection of database records, from a controller to a view.</span></span> <span data-ttu-id="039b0-194">例如，如果你想要的产品数据库表的内容显示在视图中，然后将数据库的集合视图中记录的数据。</span><span class="sxs-lookup"><span data-stu-id="039b0-194">For example, if you want to display the contents of the Products database table in a view, then you would pass the collection of database records in view data.</span></span>

<span data-ttu-id="039b0-195">此外可以将从控制器的强类型化的视图数据传递到视图。</span><span class="sxs-lookup"><span data-stu-id="039b0-195">You also have the option of passing strongly typed view data from a controller to a view.</span></span> <span data-ttu-id="039b0-196">我们在本教程中浏览本主题**了解强类型化视图数据和视图**。</span><span class="sxs-lookup"><span data-stu-id="039b0-196">We explore this topic in the tutorial **Understanding Strongly Typed View Data and Views**.</span></span>

## <a name="summary"></a><span data-ttu-id="039b0-197">总结</span><span class="sxs-lookup"><span data-stu-id="039b0-197">Summary</span></span>

<span data-ttu-id="039b0-198">本教程提供对 ASP.NET MVC 视图、 查看数据和 HTML 帮助器的简短介绍。</span><span class="sxs-lookup"><span data-stu-id="039b0-198">This tutorial provided a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="039b0-199">在第一个部分中，您学习了如何将新视图添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="039b0-199">In the first section, you learned how to add new views to your project.</span></span> <span data-ttu-id="039b0-200">你已了解，你必须添加视图到正确的文件夹以从特定控制器调用它。</span><span class="sxs-lookup"><span data-stu-id="039b0-200">You learned that you must add a view to the right folder in order to call it from a particular controller.</span></span> <span data-ttu-id="039b0-201">接下来，我们讨论 HTML 帮助的主题。</span><span class="sxs-lookup"><span data-stu-id="039b0-201">Next, we discussed the topic of HTML Helpers.</span></span> <span data-ttu-id="039b0-202">你已了解如何 HTML 帮助器使您能够轻松地生成标准 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="039b0-202">You learned how HTML Helpers enable you to easily generate standard HTML content.</span></span> <span data-ttu-id="039b0-203">最后，您学习了如何充分利用查看数据以将数据从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="039b0-203">Finally, you learned how to take advantage of view data to pass data from a controller to a view.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="039b0-204">[上一页](passing-data-to-view-master-pages-cs.md)
> [下一页](creating-custom-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="039b0-204">[Previous](passing-data-to-view-master-pages-cs.md)
[Next](creating-custom-html-helpers-vb.md)</span></span>
