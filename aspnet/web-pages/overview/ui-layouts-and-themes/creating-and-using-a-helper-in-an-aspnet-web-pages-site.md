---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: 创建和使用一个帮助程序的 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本文介绍如何在 ASP.NET Web Pages (Razor) 的网站中创建一个帮助程序。 帮助器是包含代码和标记对性能的可重用组件...
ms.author: aspnetcontent
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: c2edc10e01f4d2358dd0b0bdf450348f01eb2bfa
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811894"
---
<a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="a7cdc-104">创建和使用 ASP.NET 网页 (Razor) 站点中的一个帮助程序</span><span class="sxs-lookup"><span data-stu-id="a7cdc-104">Creating and Using a Helper in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="a7cdc-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a7cdc-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a7cdc-106">本文介绍如何在 ASP.NET Web Pages (Razor) 的网站中创建一个帮助程序。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-106">This article describes how to create a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="a7cdc-107">一个*帮助器*是一个可重用的组件，包括代码和标记来执行可能繁琐或复杂的任务。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="a7cdc-108">**你将学习：**</span><span class="sxs-lookup"><span data-stu-id="a7cdc-108">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="a7cdc-109">如何创建和使用简单的帮助程序。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-109">How to create and use a simple helper.</span></span>
> 
> <span data-ttu-id="a7cdc-110">下面是在本文中引入的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="a7cdc-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="a7cdc-111">`@helper`语法。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-111">The `@helper` syntax.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a7cdc-112">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="a7cdc-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a7cdc-113">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="a7cdc-113">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="a7cdc-114">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-114">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="overview-of-helpers"></a><span data-ttu-id="a7cdc-115">帮助程序的概述</span><span class="sxs-lookup"><span data-stu-id="a7cdc-115">Overview of Helpers</span></span>

<span data-ttu-id="a7cdc-116">如果需要在站点中的不同页上执行相同的任务，可以使用一个帮助程序。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-116">If you need to perform the same tasks on different pages in your site, you can use a helper.</span></span> <span data-ttu-id="a7cdc-117">ASP.NET 网页包括大量的帮助程序，并且有许多数据越多，您可以下载并安装。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-117">ASP.NET Web Pages includes a number of helpers, and there are many more that you can download and install.</span></span> <span data-ttu-id="a7cdc-118">(一组内置帮助程序 ASP.NET Web Pages 中所示[ASP.NET API 快速参考](https://go.microsoft.com/fwlink/?LinkId=202907)。)如果现有的帮助程序都不能满足您的需要，可以创建自己的帮助器。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-118">(A list of the built-in helpers in ASP.NET Web Pages is listed in the [ASP.NET API Quick Reference](https://go.microsoft.com/fwlink/?LinkId=202907).) If none of the existing helpers meet your needs, you can create your own helper.</span></span>

<span data-ttu-id="a7cdc-119">一个帮助程序允许您使用的多个页面的一个常见的代码块。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-119">A helper lets you use a common block of code across multiple pages.</span></span> <span data-ttu-id="a7cdc-120">假设在您的页面通常要创建的注意项目的设置除了普通段落。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-120">Suppose that in your page you often want to create a note item that's set apart from normal paragraphs.</span></span> <span data-ttu-id="a7cdc-121">注意为创建的可能是`<div>`元素，具有的样式设置为具有边框的框。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-121">Perhaps the note is created as a `<div>` element that's styled as a box with a border.</span></span> <span data-ttu-id="a7cdc-122">而不是每次想要显示注释，此相同的标记添加到页面，可打包为一个帮助程序标记。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-122">Rather than add this same markup to a page every time you want to display a note, you can package the markup as a helper.</span></span> <span data-ttu-id="a7cdc-123">然后，您可以插入便笺的一行代码需要的任意位置。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-123">You can then insert the note with a single line of code anywhere you need it.</span></span>

<span data-ttu-id="a7cdc-124">使用此类的一个帮助程序使每个页面中的代码，更简单、 更容易阅读。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-124">Using a helper like this makes the code in each of your pages simpler and easier to read.</span></span> <span data-ttu-id="a7cdc-125">它还使得它更易于维护你的站点，因为如果需要更改外观的说明，你可以在一个位置的标记。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-125">It also makes it easier to maintain your site, because if you need to change how the notes look, you can change the markup in one place.</span></span>

## <a name="creating-a-helper"></a><span data-ttu-id="a7cdc-126">创建一个帮助程序</span><span class="sxs-lookup"><span data-stu-id="a7cdc-126">Creating a Helper</span></span>

<span data-ttu-id="a7cdc-127">此过程演示如何创建帮助程序将创建便笺，按前面所述。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-127">This procedure shows you how to create the helper that creates the note, as just described.</span></span> <span data-ttu-id="a7cdc-128">这是一个简单的示例，但自定义帮助程序可以包含任何标记和所需的 ASP.NET 代码。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-128">This is a simple example, but the custom helper can include any markup and ASP.NET code that you need.</span></span>

1. <span data-ttu-id="a7cdc-129">在该网站的根文件夹中，创建名为的文件夹*应用程序\_代码*。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-129">In the root folder of the website, create a folder named *App\_Code*.</span></span> <span data-ttu-id="a7cdc-130">这是在 ASP.NET 中的保留的文件夹名称可以放置的组件，如帮助程序的代码。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-130">This is a reserved folder name in ASP.NET where you can put code for components like helpers.</span></span>
2. <span data-ttu-id="a7cdc-131">在中*应用程序\_代码*文件夹中创建一个新 *.cshtml*文件并将其命名*MyHelpers.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-131">In the *App\_Code* folder create a new *.cshtml* file and name it *MyHelpers.cshtml*.</span></span>
3. <span data-ttu-id="a7cdc-132">使用以下内容替换现有内容：</span><span class="sxs-lookup"><span data-stu-id="a7cdc-132">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="a7cdc-133">该代码使用`@helper`语法来声明一个新的帮助程序，名为`MakeNote`。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-133">The code uses the `@helper` syntax to declare a new helper named `MakeNote`.</span></span> <span data-ttu-id="a7cdc-134">此特定的帮助器，可以传递参数名为`content`，可以包含的文本和标记组合。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-134">This particular helper lets you pass a parameter named `content` that can contain a combination of text and markup.</span></span> <span data-ttu-id="a7cdc-135">帮助器将字符串插入到注意正文使用`@content`变量。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-135">The helper inserts the string into the note body using the `@content` variable.</span></span>

    <span data-ttu-id="a7cdc-136">请注意，该文件命名*MyHelpers.cshtml*，但帮助者名为`MakeNote`。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-136">Notice that the file is named *MyHelpers.cshtml*, but the helper is named `MakeNote`.</span></span> <span data-ttu-id="a7cdc-137">可以将多个自定义帮助程序放入单个文件。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-137">You can put multiple custom helpers into a single file.</span></span>
4. <span data-ttu-id="a7cdc-138">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-138">Save and close the file.</span></span>

## <a name="using-the-helper-in-a-page"></a><span data-ttu-id="a7cdc-139">在页面中使用该帮助器</span><span class="sxs-lookup"><span data-stu-id="a7cdc-139">Using the Helper in a Page</span></span>

1. <span data-ttu-id="a7cdc-140">在根文件夹中，创建新的空白文件称为*TestHelper.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-140">In the root folder, create a new blank file called *TestHelper.cshtml*.</span></span>
2. <span data-ttu-id="a7cdc-141">向文件中添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="a7cdc-141">Add the following code to the file:</span></span>

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    <span data-ttu-id="a7cdc-142">若要调用帮助器创建，使用`@`跟的文件名，该帮助器位置后，一个点，然后帮助程序名称。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-142">To call the helper you created, use `@` followed by the file name where the helper is, a dot, and then the helper name.</span></span> <span data-ttu-id="a7cdc-143">(如果在具有多个文件夹*应用程序\_代码*文件夹中，可以使用语法`@FolderName.FileName.HelperName`调用帮助者内任何嵌套的文件夹级别)。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-143">(If you had multiple folders in the *App\_Code* folder, you could use the syntax `@FolderName.FileName.HelperName` to call your helper within any nested folder level).</span></span> <span data-ttu-id="a7cdc-144">在括号中的引号中添加的文本是说明的帮助程序将显示在网页中的一部分的文本。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-144">The text that you add in quotation marks within the parentheses is the text that the helper will display as part of the note in the web page.</span></span>
3. <span data-ttu-id="a7cdc-145">保存页面，并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-145">Save the page and run it in a browser.</span></span> <span data-ttu-id="a7cdc-146">帮助程序生成的注意项直接调用帮助程序的位置： 两个段落间。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-146">The helper generates the note item right where you called the helper: between the two paragraphs.</span></span>

    ![在浏览器以及如何帮助程序生成标记放入指定的文本周围的框中显示的页面的屏幕截图。](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.jpg)

## <a name="additional-resources"></a><span data-ttu-id="a7cdc-148">其他资源</span><span class="sxs-lookup"><span data-stu-id="a7cdc-148">Additional Resources</span></span>


<span data-ttu-id="a7cdc-149">[为 Razor 帮助器的水平菜单](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-149">[Horizontal menu as a Razor helper](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341).</span></span> <span data-ttu-id="a7cdc-150">由 Mike 教皇此博客文章显示了如何创建使用标记、 CSS 和代码的帮助程序作为一个水平菜单。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-150">This blog entry by Mike Pope shows how to create a horizontal menu as a helper using markup, CSS, and code.</span></span>

<span data-ttu-id="a7cdc-151">[利用 ASP.NET Web 中的 HTML5 页帮助程序适用于 WebMatrix 和 ASP.NET MVC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-151">[Leveraging HTML5 in ASP.NET Web Pages Helpers for WebMatrix and ASP.NET MVC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx).</span></span> <span data-ttu-id="a7cdc-152">由 Sam Abraham 此博客文章显示了一个帮助程序，将呈现一个 HTML5`Canvas`元素。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-152">This blog entry by Sam Abraham shows a helper that renders an HTML5 `Canvas` element.</span></span>

<span data-ttu-id="a7cdc-153">[之间的差异@Helpers并@Functions在 WebMatrix 中](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-153">[The Difference Between @Helpers and @Functions in WebMatrix](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span></span> <span data-ttu-id="a7cdc-154">由 Mike Brind 此博客条目描述`@helper`语法和`@function`语法以及何时使用每个。</span><span class="sxs-lookup"><span data-stu-id="a7cdc-154">This blog entry by Mike Brind describes `@helper` syntax and `@function` syntax and when to use each.</span></span>
