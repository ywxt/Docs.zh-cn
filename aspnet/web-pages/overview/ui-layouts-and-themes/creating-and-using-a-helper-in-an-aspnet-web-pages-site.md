---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: 创建和使用程序的帮助程序在 ASP.NET Web 页 (Razor) 站点 |Microsoft 文档
author: tfitzmac
description: 本文介绍如何在 ASP.NET Web 页 (Razor) 网站中创建一个帮助程序。 帮助器是包含代码和性能标记是可重用组件...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 5d0c1ae09d8fbc91ff76cd4045d439abafee7736
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26529996"
---
<a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="4b6dc-104">创建和使用 ASP.NET Web 页 (Razor) 站点中的一个帮助程序</span><span class="sxs-lookup"><span data-stu-id="4b6dc-104">Creating and Using a Helper in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="4b6dc-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4b6dc-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="4b6dc-106">本文介绍如何在 ASP.NET Web 页 (Razor) 网站中创建一个帮助程序。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-106">This article describes how to create a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="4b6dc-107">A*帮助器*包括代码和标记，以执行可能需要很长时间或复杂的任务是可重用组件。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="4b6dc-108">**你将学习：**</span><span class="sxs-lookup"><span data-stu-id="4b6dc-108">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="4b6dc-109">如何创建和使用简单的帮助器。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-109">How to create and use a simple helper.</span></span>
> 
> <span data-ttu-id="4b6dc-110">这些是文章中引入的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="4b6dc-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="4b6dc-111">`@helper`语法。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-111">The `@helper` syntax.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4b6dc-112">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="4b6dc-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="4b6dc-113">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="4b6dc-113">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="4b6dc-114">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-114">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="overview-of-helpers"></a><span data-ttu-id="4b6dc-115">帮助器概述</span><span class="sxs-lookup"><span data-stu-id="4b6dc-115">Overview of Helpers</span></span>

<span data-ttu-id="4b6dc-116">如果你需要在你的站点中的不同页上执行相同的任务，你可以使用程序的帮助。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-116">If you need to perform the same tasks on different pages in your site, you can use a helper.</span></span> <span data-ttu-id="4b6dc-117">ASP.NET Web Pages 包括大量的帮助器，并且有很多数据越多，你可以下载并安装。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-117">ASP.NET Web Pages includes a number of helpers, and there are many more that you can download and install.</span></span> <span data-ttu-id="4b6dc-118">(中列出的内置的帮助器中的 ASP.NET Web Pages 列表[ASP.NET API 快速参考](https://go.microsoft.com/fwlink/?LinkId=202907)。)如果没有任何现有的帮助器满足你的需求，你可以创建你自己的帮助器。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-118">(A list of the built-in helpers in ASP.NET Web Pages is listed in the [ASP.NET API Quick Reference](https://go.microsoft.com/fwlink/?LinkId=202907).) If none of the existing helpers meet your needs, you can create your own helper.</span></span>

<span data-ttu-id="4b6dc-119">一个帮助程序允许你跨多个页面使用常见的代码块。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-119">A helper lets you use a common block of code across multiple pages.</span></span> <span data-ttu-id="4b6dc-120">假设在页中你通常想要创建注意项的设置除了普通段落。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-120">Suppose that in your page you often want to create a note item that's set apart from normal paragraphs.</span></span> <span data-ttu-id="4b6dc-121">为可能创建了注意`<div>`元素，具有格式为包装盒边框。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-121">Perhaps the note is created as a `<div>` element that's styled as a box with a border.</span></span> <span data-ttu-id="4b6dc-122">而不是每次你想显示注释，请将此相同标记添加到页中，你可以标记打包为一个帮助程序。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-122">Rather than add this same markup to a page every time you want to display a note, you can package the markup as a helper.</span></span> <span data-ttu-id="4b6dc-123">然后，您可以插入一行代码具有注释需要的任何位置。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-123">You can then insert the note with a single line of code anywhere you need it.</span></span>

<span data-ttu-id="4b6dc-124">使用如下的帮助使每个页面中的代码，更简单且更易读。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-124">Using a helper like this makes the code in each of your pages simpler and easier to read.</span></span> <span data-ttu-id="4b6dc-125">它还使它成为易于维护你的站点，因为如果你需要更改说明的外观，你可以更改在一个位置的标记。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-125">It also makes it easier to maintain your site, because if you need to change how the notes look, you can change the markup in one place.</span></span>

## <a name="creating-a-helper"></a><span data-ttu-id="4b6dc-126">创建一个帮助程序</span><span class="sxs-lookup"><span data-stu-id="4b6dc-126">Creating a Helper</span></span>

<span data-ttu-id="4b6dc-127">此过程演示如何创建创建的说明，如上所述的帮助程序。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-127">This procedure shows you how to create the helper that creates the note, as just described.</span></span> <span data-ttu-id="4b6dc-128">这是一个简单的示例，但任何标记和你需要的 ASP.NET 代码，可以包括自定义帮助器。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-128">This is a simple example, but the custom helper can include any markup and ASP.NET code that you need.</span></span>

1. <span data-ttu-id="4b6dc-129">在网站的根文件夹中，创建名为的文件夹*应用\_代码*。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-129">In the root folder of the website, create a folder named *App\_Code*.</span></span> <span data-ttu-id="4b6dc-130">这是在 ASP.NET 中的保留的文件夹名称的组件，如帮助器代码的放置位置。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-130">This is a reserved folder name in ASP.NET where you can put code for components like helpers.</span></span>
2. <span data-ttu-id="4b6dc-131">在*应用\_代码*文件夹创建一个新 *.cshtml*文件并将其命名*MyHelpers.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-131">In the *App\_Code* folder create a new *.cshtml* file and name it *MyHelpers.cshtml*.</span></span>
3. <span data-ttu-id="4b6dc-132">将现有内容替换为以下：</span><span class="sxs-lookup"><span data-stu-id="4b6dc-132">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="4b6dc-133">该代码使用`@helper`语法来声明名为的新帮助`MakeNote`。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-133">The code uses the `@helper` syntax to declare a new helper named `MakeNote`.</span></span> <span data-ttu-id="4b6dc-134">此特定的帮助器，可以将传递一个名为参数`content`可以包含文本和标记的组合。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-134">This particular helper lets you pass a parameter named `content` that can contain a combination of text and markup.</span></span> <span data-ttu-id="4b6dc-135">帮助器将字符串插入到注意正文使用`@content`变量。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-135">The helper inserts the string into the note body using the `@content` variable.</span></span>

    <span data-ttu-id="4b6dc-136">请注意该文件名为*MyHelpers.cshtml*，但在名为帮助器`MakeNote`。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-136">Notice that the file is named *MyHelpers.cshtml*, but the helper is named `MakeNote`.</span></span> <span data-ttu-id="4b6dc-137">可以将多个自定义帮助器放入单个文件。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-137">You can put multiple custom helpers into a single file.</span></span>
4. <span data-ttu-id="4b6dc-138">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-138">Save and close the file.</span></span>

## <a name="using-the-helper-in-a-page"></a><span data-ttu-id="4b6dc-139">在页中使用的帮助器</span><span class="sxs-lookup"><span data-stu-id="4b6dc-139">Using the Helper in a Page</span></span>

1. <span data-ttu-id="4b6dc-140">在根文件夹中，创建新的空白文件调用*TestHelper.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-140">In the root folder, create a new blank file called *TestHelper.cshtml*.</span></span>
2. <span data-ttu-id="4b6dc-141">向文件中添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="4b6dc-141">Add the following code to the file:</span></span>

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    <span data-ttu-id="4b6dc-142">若要调用你创建的帮助程序，使用`@`跟帮助器的工作所在，一个点的文件名称，然后选择帮助程序名称。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-142">To call the helper you created, use `@` followed by the file name where the helper is, a dot, and then the helper name.</span></span> <span data-ttu-id="4b6dc-143">(如果在具有多个文件夹*应用\_代码*文件夹中，你可以使用语法`@FolderName.FileName.HelperName`调用中任何帮助程序嵌套文件夹级别)。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-143">(If you had multiple folders in the *App\_Code* folder, you could use the syntax `@FolderName.FileName.HelperName` to call your helper within any nested folder level).</span></span> <span data-ttu-id="4b6dc-144">添加用引号引起来，在括号内的文本是说明的帮助器将显示为网页中的一部分的文本。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-144">The text that you add in quotation marks within the parentheses is the text that the helper will display as part of the note in the web page.</span></span>
3. <span data-ttu-id="4b6dc-145">保存页并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-145">Save the page and run it in a browser.</span></span> <span data-ttu-id="4b6dc-146">帮助器生成的注意项右中调用帮助器： 两个段落之间。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-146">The helper generates the note item right where you called the helper: between the two paragraphs.</span></span>

    ![显示在浏览器和帮助器如何生成将指定的文本围框内的标记中的页的屏幕截图。](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.jpg)

## <a name="additional-resources"></a><span data-ttu-id="4b6dc-148">其他资源</span><span class="sxs-lookup"><span data-stu-id="4b6dc-148">Additional Resources</span></span>


<span data-ttu-id="4b6dc-149">[作为 Razor 助手水平菜单](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-149">[Horizontal menu as a Razor helper](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341).</span></span> <span data-ttu-id="4b6dc-150">由 Mike Pope 此博客文章说明如何创建水平菜单方式使用标记、 CSS 和代码的帮助。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-150">This blog entry by Mike Pope shows how to create a horizontal menu as a helper using markup, CSS, and code.</span></span>

<span data-ttu-id="4b6dc-151">[利用在 ASP.NET 网页中的 HTML5 WebMatrix 和 ASP.NET MVC3 页帮助器](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-151">[Leveraging HTML5 in ASP.NET Web Pages Helpers for WebMatrix and ASP.NET MVC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx).</span></span> <span data-ttu-id="4b6dc-152">通过 Sam 当年此博客文章说明的帮助程序呈现 HTML5`Canvas`元素。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-152">This blog entry by Sam Abraham shows a helper that renders an HTML5 `Canvas` element.</span></span>

<span data-ttu-id="4b6dc-153">[之间的差异@Helpers和@Functions在 WebMatrix 中](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-153">[The Difference Between @Helpers and @Functions in WebMatrix](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span></span> <span data-ttu-id="4b6dc-154">由 Mike Brind 此博客条目描述`@helper`语法和`@function`语法以及何时使用每个。</span><span class="sxs-lookup"><span data-stu-id="4b6dc-154">This blog entry by Mike Brind describes `@helper` syntax and `@function` syntax and when to use each.</span></span>
