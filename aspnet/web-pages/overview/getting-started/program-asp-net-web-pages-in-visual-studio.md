---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 编程 ASP.NET 网页 (Razor) 使用 Visual Studio |Microsoft Docs
author: tfitzmac
description: 本附录介绍了如何使用 Visual Studio 2010 或 Visual Web Developer 2010 速成版到程序 ASP.NET Web Pages with Razor syntax。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/13/2014
ms.topic: article
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: b7f9a6c2d55d31dc918d2b2e542e26639a54b39a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37380358"
---
<a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="48867-103">编程使用 Visual Studio 的 ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="48867-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>
====================
<span data-ttu-id="48867-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="48867-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="48867-105">本文介绍如何使用 Visual Studio 或 Visual Web Developer 速成版到程序 ASP.NET Web Pages (Razor) 网站。</span><span class="sxs-lookup"><span data-stu-id="48867-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
> 
> <span data-ttu-id="48867-106">学习内容</span><span class="sxs-lookup"><span data-stu-id="48867-106">What you'll learn</span></span>
> 
> - <span data-ttu-id="48867-107">需要安装 （如果有的话），以便在你的 Visual Studio 版本中使用 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="48867-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="48867-108">如何将支持适用于 ASP.NET 网页添加到 Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="48867-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="48867-109">如何使用 Visual Studio 中的功能以使用 ASP.NET Razor 页面，包括 IntelliSense 和调试程序。</span><span class="sxs-lookup"><span data-stu-id="48867-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="48867-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="48867-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="48867-111">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="48867-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="48867-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="48867-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="48867-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="48867-113">WebMatrix 3</span></span>
>   
> 
> <span data-ttu-id="48867-114">本教程也适用于 ASP.NET Web Pages 2、 Visual Studio 2012、 Visual Studio 2010 中，和 WebMatrix 2。</span><span class="sxs-lookup"><span data-stu-id="48867-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>


<span data-ttu-id="48867-115">您可以使用 Razor 语法使用 WebMatrix 或许多其他代码编辑器中编写的 ASP.NET Web pages。</span><span class="sxs-lookup"><span data-stu-id="48867-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="48867-116">此外可以使用 Microsoft Visual Studio 是一个全功能集成的开发环境 (IDE)，用于创建许多类型的应用程序 （而不仅仅是网站） 提供一组强大的工具。</span><span class="sxs-lookup"><span data-stu-id="48867-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="48867-117">若要使用 ASP.NET Razor 页面，您可以使用 Visual Studio 的完整版或免费[Visual Studio Express for Web](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-2013-express)版本。</span><span class="sxs-lookup"><span data-stu-id="48867-117">To work with ASP.NET Razor pages, you can either use one of the full editions of Visual Studio or the free [Visual Studio Express for Web](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-2013-express) edition.</span></span>

<span data-ttu-id="48867-118">Visual Studio 提供了使用 ASP.NET Razor web 页面进行编程的两个特别有用功能是：</span><span class="sxs-lookup"><span data-stu-id="48867-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="48867-119">*IntelliSense*。</span><span class="sxs-lookup"><span data-stu-id="48867-119">*IntelliSense*.</span></span> <span data-ttu-id="48867-120">Visual Studio 中内置的 IntelliSense 功能并更全面比在 WebMatrix 中的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="48867-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="48867-121">*调试器*。</span><span class="sxs-lookup"><span data-stu-id="48867-121">*Debugger*.</span></span> <span data-ttu-id="48867-122">调试程序，可通过停止程序，而是运行、 检查变量和单步执行代码逐行排查代码。</span><span class="sxs-lookup"><span data-stu-id="48867-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="48867-123">Visual Studio 中使用不同版本的 ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="48867-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="48867-124">Visual Studio 2012 和 Visual Studio 2013 包括支持适用于 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="48867-124">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="48867-125">（为了支持 ASP.NET Web Pages 需要安装包时安装 Visual Studio。）</span><span class="sxs-lookup"><span data-stu-id="48867-125">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="48867-126">Visual Studio 2010 不包括支持默认情况下为 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="48867-126">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="48867-127">若要使用 Visual Studio 2010 中使用 ASP.NET Web Pages，必须安装 ASP.NET MVC 包。</span><span class="sxs-lookup"><span data-stu-id="48867-127">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="48867-128">若要获取 ASP.NET Web Pages 2，你安装 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="48867-128">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="48867-129">下表总结了不同版本的 Visual Studio 中的支持为 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="48867-129">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="48867-130">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="48867-130">Visual Studio 2010</span></span> | <span data-ttu-id="48867-131">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="48867-131">Visual Studio 2012</span></span> | <span data-ttu-id="48867-132">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="48867-132">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="48867-133">**ASP.NET 网页 2**</span><span class="sxs-lookup"><span data-stu-id="48867-133">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="48867-134">安装 ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="48867-134">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="48867-135">（包含）</span><span class="sxs-lookup"><span data-stu-id="48867-135">(Included)</span></span> | <span data-ttu-id="48867-136">（包含）</span><span class="sxs-lookup"><span data-stu-id="48867-136">(Included)</span></span> |
| <span data-ttu-id="48867-137">**ASP.NET 网页 3**</span><span class="sxs-lookup"><span data-stu-id="48867-137">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="48867-138">更新到 ASP.NET Web Pages 3 通过 NuGet</span><span class="sxs-lookup"><span data-stu-id="48867-138">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="48867-139">（包含）</span><span class="sxs-lookup"><span data-stu-id="48867-139">(Included)</span></span> |

<span data-ttu-id="48867-140">若要使用 Visual Studio 2010，请参阅[安装支持的 ASP.NET Web Pages Visual Studio 2010 中](#vs2010support)。</span><span class="sxs-lookup"><span data-stu-id="48867-140">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="48867-141">启动 Visual Studio 中的从 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="48867-141">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="48867-142">如果你在 WebMatrix 中启动项目，并想要切换到 Visual Studio，WebMatrix 提供了用于轻松地在 Visual Studio 中打开项目的按钮。</span><span class="sxs-lookup"><span data-stu-id="48867-142">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="48867-143">必须具有 Visual Studio 安装在计算机中的此按钮才可用。</span><span class="sxs-lookup"><span data-stu-id="48867-143">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="48867-144">下图显示在 WebMatrix 中的按钮。</span><span class="sxs-lookup"><span data-stu-id="48867-144">The following image shows the button in WebMatrix.</span></span>

![启动 Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="48867-146">当单击按钮时，在 Visual Studio 中打开该项目。</span><span class="sxs-lookup"><span data-stu-id="48867-146">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="48867-147">您可以来回切换 WebMatrix 和 Visual Studio 之间没有任何问题。</span><span class="sxs-lookup"><span data-stu-id="48867-147">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="48867-148">如果任何文件在其他环境中已更改并且需要重新加载以获取最新更改，你将收到通知。</span><span class="sxs-lookup"><span data-stu-id="48867-148">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="48867-149">在 Visual Studio 中创建 ASP.NET Razor 站点</span><span class="sxs-lookup"><span data-stu-id="48867-149">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="48867-150">在 Visual Studio 中创建 ASP.NET Razor 网站：</span><span class="sxs-lookup"><span data-stu-id="48867-150">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="48867-151">启动 Visual Studio 或 Visual Web Developer。</span><span class="sxs-lookup"><span data-stu-id="48867-151">Start Visual Studio or Visual Web Developer.</span></span>
2. <span data-ttu-id="48867-152">在中**文件**菜单上，单击**新的 Web 站点**。</span><span class="sxs-lookup"><span data-stu-id="48867-152">In the **File** menu, click **New Web Site**.</span></span>

    ![创建新网站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="48867-154">在中**新的 Web 站点**对话框框中，选择要使用 （Visual C# 或 Visual Basic） 的语言。</span><span class="sxs-lookup"><span data-stu-id="48867-154">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="48867-155">选择**ASP.NET Web 站点 (Razor)** 模板。</span><span class="sxs-lookup"><span data-stu-id="48867-155">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![razor 站点](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="48867-157">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="48867-157">Click **OK**.</span></span>

<span data-ttu-id="48867-158">新的项目存在，并填入一些默认 web 页，以帮助您入门。</span><span class="sxs-lookup"><span data-stu-id="48867-158">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="48867-159">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="48867-159">Using IntelliSense</span></span>

<span data-ttu-id="48867-160">现在，已创建一个站点，您可以看到在 Visual Studio 中的 IntelliSense 工作原理。</span><span class="sxs-lookup"><span data-stu-id="48867-160">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="48867-161">在刚刚创建的网站，打开*Default.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="48867-161">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="48867-162">之后`<h3>`标记在页中，键入`@ServerInfo.`（包含句点）。</span><span class="sxs-lookup"><span data-stu-id="48867-162">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="48867-163">请注意 IntelliSense 如何在显示的可用方法`ServerInfo`下拉列表中的帮助程序。</span><span class="sxs-lookup"><span data-stu-id="48867-163">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span> 

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="48867-165">选择`GetHtml`方法从列表中，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="48867-165">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="48867-166">IntelliSense 会自动填充该方法。</span><span class="sxs-lookup"><span data-stu-id="48867-166">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="48867-167">(如 C# 中的任何方法，则你必须添加`()`方法之后的字符。)</span><span class="sxs-lookup"><span data-stu-id="48867-167">(As with any method in C#, you must add `()` characters after the method.)</span></span>  
   <span data-ttu-id="48867-168">已完成的代码`GetHtml`方法看起来如下例所示：</span><span class="sxs-lookup"><span data-stu-id="48867-168">The completed code for the `GetHtml` method looks like the following example:</span></span>  

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="48867-169">按 Ctrl + F5 以运行该页。</span><span class="sxs-lookup"><span data-stu-id="48867-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="48867-170">这是页面看起来像时显示在浏览器中：</span><span class="sxs-lookup"><span data-stu-id="48867-170">This is what the page looks like when displayed in a browser:</span></span> 

    ![在浏览器中的默认页](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="48867-172">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="48867-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="48867-173">使用调试器</span><span class="sxs-lookup"><span data-stu-id="48867-173">Using the Debugger</span></span>

1. <span data-ttu-id="48867-174">在顶部*Default.cshtml*页上，开头的行后`Page.Title`，添加以下代码行：</span><span class="sxs-lookup"><span data-stu-id="48867-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span> 

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="48867-175">在左侧的代码编辑器的灰色边距中，单击此新行的旁边以添加*断点*。</span><span class="sxs-lookup"><span data-stu-id="48867-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="48867-176">断点是一个标记，通知调试器停止在该点运行该程序，以便您可以看到发生了什么情况。</span><span class="sxs-lookup"><span data-stu-id="48867-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![设置断点](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="48867-178">删除对调用`ServerInfo.GetHtml`方法，并添加对调用`@myTime`变量在其原位置。</span><span class="sxs-lookup"><span data-stu-id="48867-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="48867-179">此调用显示新的代码行返回的当前时间值。</span><span class="sxs-lookup"><span data-stu-id="48867-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="48867-180">按 F5 以在调试器中运行该页。</span><span class="sxs-lookup"><span data-stu-id="48867-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="48867-181">页面设置的断点处停止。</span><span class="sxs-lookup"><span data-stu-id="48867-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="48867-182">下图显示了页面外观在编辑器中使用断点 （用黄色）。</span><span class="sxs-lookup"><span data-stu-id="48867-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span> 

    ![调试断点](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="48867-184">在调试工具栏中，单击**单步执行**按钮 （或按 F11） 以运行下的一行代码。</span><span class="sxs-lookup"><span data-stu-id="48867-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="48867-185">每次单击此按钮，则在前进执行到下一行代码。</span><span class="sxs-lookup"><span data-stu-id="48867-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![单步执行按钮](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="48867-187">检查的值`myTime`变量在其上停留鼠标指针或通过检查中显示的值**局部变量**并**调用堆栈**windows。</span><span class="sxs-lookup"><span data-stu-id="48867-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="48867-188">Visual Studio 显示变量的值。</span><span class="sxs-lookup"><span data-stu-id="48867-188">Visual Studio display the value of the variable.</span></span>

    ![显示时间值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="48867-190">完成检查变量和单步执行代码时，按 F5 继续运行而无需停止在每个行的页。</span><span class="sxs-lookup"><span data-stu-id="48867-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="48867-191">已完成逐步调试所有代码，浏览器显示的页面。</span><span class="sxs-lookup"><span data-stu-id="48867-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="48867-192">若要了解有关调试器以及如何在 Visual Studio 中调试代码的详细信息，请参阅[演练： 在 Visual Web Developer 中调试 Web Pages](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="48867-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="48867-193">在使用 Visual Studio 的 ASP.NET MVC 项目中使用 Razor</span><span class="sxs-lookup"><span data-stu-id="48867-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="48867-194">Razor 语法还在 ASP.NET MVC 项目中广泛使用。</span><span class="sxs-lookup"><span data-stu-id="48867-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="48867-195">MVC 是功能强大、 基于模式的方式来构建动态网站。</span><span class="sxs-lookup"><span data-stu-id="48867-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="48867-196">如果你的 ASP.NET Web Pages 站点变得难以维护，您可能需要考虑将其转换为 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="48867-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="48867-197">创建 MVC 应用程序的示例，请参阅[Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="48867-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="48867-198">在 Visual Studio 2010 中安装 ASP.NET Web pages 支持</span><span class="sxs-lookup"><span data-stu-id="48867-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="48867-199">本部分演示如何安装 Visual Web Developer 学习版 2010年和 ASP.NET Web Pages Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="48867-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="48867-200">如果还没有 Web 平台安装程序，请从以下 URL 下载：</span><span class="sxs-lookup"><span data-stu-id="48867-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="48867-201">运行 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="48867-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="48867-202">单击**产品**选项卡。</span><span class="sxs-lookup"><span data-stu-id="48867-202">Click the **Products** tab.</span></span>

    ![WebPI 产品选项卡](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="48867-204">搜索**ASP.NET MVC 4** （适用于 ASP.NET Web Pages 2)，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="48867-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="48867-205">这些产品包括 Visual Studio 工具，用于构建 ASP.NET Razor 网站。</span><span class="sxs-lookup"><span data-stu-id="48867-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi 安装选项](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="48867-207">单击**安装**以完成安装。</span><span class="sxs-lookup"><span data-stu-id="48867-207">Click **Install** to complete the installation.</span></span>
