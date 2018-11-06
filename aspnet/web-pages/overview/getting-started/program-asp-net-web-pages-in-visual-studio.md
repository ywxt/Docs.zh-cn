---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 编程 ASP.NET 网页 (Razor) 使用 Visual Studio |Microsoft Docs
author: Rick-Anderson
description: 本附录介绍了如何使用 Visual Studio 2010 或 Visual Web Developer 2010 速成版到程序 ASP.NET Web Pages with Razor syntax。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 5b8df17ec1021d133579e23cb4f5b0d0f67d4c7c
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51020450"
---
<a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="62b83-103">编程使用 Visual Studio 的 ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="62b83-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>
====================
<span data-ttu-id="62b83-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="62b83-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="62b83-105">本文介绍如何使用 Visual Studio 或 Visual Web Developer 速成版到程序 ASP.NET Web Pages (Razor) 网站。</span><span class="sxs-lookup"><span data-stu-id="62b83-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="62b83-106">学习内容</span><span class="sxs-lookup"><span data-stu-id="62b83-106">What you'll learn</span></span>
>
> - <span data-ttu-id="62b83-107">需要安装 （如果有的话），以便在你的 Visual Studio 版本中使用 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="62b83-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="62b83-108">如何将支持适用于 ASP.NET 网页添加到 Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="62b83-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="62b83-109">如何使用 Visual Studio 中的功能以使用 ASP.NET Razor 页面，包括 IntelliSense 和调试程序。</span><span class="sxs-lookup"><span data-stu-id="62b83-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="62b83-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="62b83-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="62b83-111">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="62b83-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="62b83-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="62b83-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="62b83-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="62b83-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="62b83-114">本教程也适用于 ASP.NET Web Pages 2、 Visual Studio 2012、 Visual Studio 2010 中，和 WebMatrix 2。</span><span class="sxs-lookup"><span data-stu-id="62b83-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>


<span data-ttu-id="62b83-115">您可以使用 Razor 语法使用 WebMatrix 或许多其他代码编辑器中编写的 ASP.NET Web pages。</span><span class="sxs-lookup"><span data-stu-id="62b83-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="62b83-116">此外可以使用 Microsoft Visual Studio 是一个全功能集成的开发环境 (IDE)，用于创建许多类型的应用程序 （而不仅仅是网站） 提供一组强大的工具。</span><span class="sxs-lookup"><span data-stu-id="62b83-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="62b83-117">若要使用 ASP.NET Razor 页面，可以使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="62b83-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="62b83-118">Visual Studio 提供了使用 ASP.NET Razor web 页面进行编程的两个特别有用功能是：</span><span class="sxs-lookup"><span data-stu-id="62b83-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="62b83-119">*IntelliSense*。</span><span class="sxs-lookup"><span data-stu-id="62b83-119">*IntelliSense*.</span></span> <span data-ttu-id="62b83-120">Visual Studio 中内置的 IntelliSense 功能并更全面比在 WebMatrix 中的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="62b83-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="62b83-121">*调试器*。</span><span class="sxs-lookup"><span data-stu-id="62b83-121">*Debugger*.</span></span> <span data-ttu-id="62b83-122">调试程序，可通过停止程序，而是运行、 检查变量和单步执行代码逐行排查代码。</span><span class="sxs-lookup"><span data-stu-id="62b83-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="62b83-123">Visual Studio 中使用不同版本的 ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="62b83-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="62b83-124">若要开发 Visual Studio 2017 中的 ASP.NET web 应用程序，安装**ASP.NET 和 web 开发**工作负荷。</span><span class="sxs-lookup"><span data-stu-id="62b83-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="62b83-125">Visual Studio 2012 和 Visual Studio 2013 包括支持适用于 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="62b83-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="62b83-126">（为了支持 ASP.NET Web Pages 需要安装包时安装 Visual Studio。）</span><span class="sxs-lookup"><span data-stu-id="62b83-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="62b83-127">Visual Studio 2010 不包括支持默认情况下为 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="62b83-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="62b83-128">若要使用 Visual Studio 2010 中使用 ASP.NET Web Pages，必须安装 ASP.NET MVC 包。</span><span class="sxs-lookup"><span data-stu-id="62b83-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="62b83-129">若要获取 ASP.NET Web Pages 2，你安装 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="62b83-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="62b83-130">下表总结了不同版本的 Visual Studio 中的支持为 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="62b83-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="62b83-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="62b83-131">Visual Studio 2010</span></span> | <span data-ttu-id="62b83-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="62b83-132">Visual Studio 2012</span></span> | <span data-ttu-id="62b83-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="62b83-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62b83-134">**ASP.NET 网页 2**</span><span class="sxs-lookup"><span data-stu-id="62b83-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="62b83-135">安装 ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="62b83-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="62b83-136">（包含）</span><span class="sxs-lookup"><span data-stu-id="62b83-136">(Included)</span></span> | <span data-ttu-id="62b83-137">（包含）</span><span class="sxs-lookup"><span data-stu-id="62b83-137">(Included)</span></span> |
| <span data-ttu-id="62b83-138">**ASP.NET 网页 3**</span><span class="sxs-lookup"><span data-stu-id="62b83-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="62b83-139">更新到 ASP.NET Web Pages 3 通过 NuGet</span><span class="sxs-lookup"><span data-stu-id="62b83-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="62b83-140">（包含）</span><span class="sxs-lookup"><span data-stu-id="62b83-140">(Included)</span></span> |

<span data-ttu-id="62b83-141">若要使用 Visual Studio 2010，请参阅[安装支持的 ASP.NET Web Pages Visual Studio 2010 中](#vs2010support)。</span><span class="sxs-lookup"><span data-stu-id="62b83-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="62b83-142">启动 Visual Studio 中的从 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="62b83-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="62b83-143">如果你在 WebMatrix 中启动项目，并想要切换到 Visual Studio，WebMatrix 提供了用于轻松地在 Visual Studio 中打开项目的按钮。</span><span class="sxs-lookup"><span data-stu-id="62b83-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="62b83-144">必须具有 Visual Studio 安装在计算机中的此按钮才可用。</span><span class="sxs-lookup"><span data-stu-id="62b83-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="62b83-145">下图显示在 WebMatrix 中的按钮。</span><span class="sxs-lookup"><span data-stu-id="62b83-145">The following image shows the button in WebMatrix.</span></span>

![启动 Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="62b83-147">当单击按钮时，在 Visual Studio 中打开该项目。</span><span class="sxs-lookup"><span data-stu-id="62b83-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="62b83-148">您可以来回切换 WebMatrix 和 Visual Studio 之间没有任何问题。</span><span class="sxs-lookup"><span data-stu-id="62b83-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="62b83-149">如果任何文件在其他环境中已更改并且需要重新加载以获取最新更改，你将收到通知。</span><span class="sxs-lookup"><span data-stu-id="62b83-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="62b83-150">在 Visual Studio 中创建 ASP.NET Razor 站点</span><span class="sxs-lookup"><span data-stu-id="62b83-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="62b83-151">在 Visual Studio 中创建 ASP.NET Razor 网站：</span><span class="sxs-lookup"><span data-stu-id="62b83-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="62b83-152">打开 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="62b83-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="62b83-153">在中**文件**菜单上，单击**新的 Web 站点**。</span><span class="sxs-lookup"><span data-stu-id="62b83-153">In the **File** menu, click **New Web Site**.</span></span>

    ![创建新网站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="62b83-155">在中**新的 Web 站点**对话框框中，选择要使用 （Visual C# 或 Visual Basic） 的语言。</span><span class="sxs-lookup"><span data-stu-id="62b83-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="62b83-156">选择**ASP.NET Web 站点 (Razor)** 模板。</span><span class="sxs-lookup"><span data-stu-id="62b83-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![razor 站点](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="62b83-158">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="62b83-158">Click **OK**.</span></span>

<span data-ttu-id="62b83-159">新的项目存在，并填入一些默认 web 页，以帮助您入门。</span><span class="sxs-lookup"><span data-stu-id="62b83-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="62b83-160">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="62b83-160">Using IntelliSense</span></span>

<span data-ttu-id="62b83-161">现在，已创建一个站点，您可以看到在 Visual Studio 中的 IntelliSense 工作原理。</span><span class="sxs-lookup"><span data-stu-id="62b83-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="62b83-162">在刚刚创建的网站，打开*Default.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="62b83-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="62b83-163">之后`<h3>`标记在页中，键入`@ServerInfo.`（包含句点）。</span><span class="sxs-lookup"><span data-stu-id="62b83-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="62b83-164">请注意 IntelliSense 如何在显示的可用方法`ServerInfo`下拉列表中的帮助程序。</span><span class="sxs-lookup"><span data-stu-id="62b83-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="62b83-166">选择`GetHtml`方法从列表中，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="62b83-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="62b83-167">IntelliSense 会自动填充该方法。</span><span class="sxs-lookup"><span data-stu-id="62b83-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="62b83-168">(如 C# 中的任何方法，则你必须添加`()`方法之后的字符。)已完成的代码`GetHtml`方法看起来如下例所示：</span><span class="sxs-lookup"><span data-stu-id="62b83-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="62b83-169">按 Ctrl + F5 以运行该页。</span><span class="sxs-lookup"><span data-stu-id="62b83-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="62b83-170">这是页面看起来像时显示在浏览器中：</span><span class="sxs-lookup"><span data-stu-id="62b83-170">This is what the page looks like when displayed in a browser:</span></span>

    ![在浏览器中的默认页](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="62b83-172">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="62b83-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="62b83-173">使用调试器</span><span class="sxs-lookup"><span data-stu-id="62b83-173">Using the Debugger</span></span>

1. <span data-ttu-id="62b83-174">在顶部*Default.cshtml*页上，开头的行后`Page.Title`，添加以下代码行：</span><span class="sxs-lookup"><span data-stu-id="62b83-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="62b83-175">在左侧的代码编辑器的灰色边距中，单击此新行的旁边以添加*断点*。</span><span class="sxs-lookup"><span data-stu-id="62b83-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="62b83-176">断点是一个标记，通知调试器停止在该点运行该程序，以便您可以看到发生了什么情况。</span><span class="sxs-lookup"><span data-stu-id="62b83-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![设置断点](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="62b83-178">删除对调用`ServerInfo.GetHtml`方法，并添加对调用`@myTime`变量在其原位置。</span><span class="sxs-lookup"><span data-stu-id="62b83-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="62b83-179">此调用显示新的代码行返回的当前时间值。</span><span class="sxs-lookup"><span data-stu-id="62b83-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="62b83-180">按 F5 以在调试器中运行该页。</span><span class="sxs-lookup"><span data-stu-id="62b83-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="62b83-181">页面设置的断点处停止。</span><span class="sxs-lookup"><span data-stu-id="62b83-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="62b83-182">下图显示了页面外观在编辑器中使用断点 （用黄色）。</span><span class="sxs-lookup"><span data-stu-id="62b83-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![调试断点](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="62b83-184">在调试工具栏中，单击**单步执行**按钮 （或按 F11） 以运行下的一行代码。</span><span class="sxs-lookup"><span data-stu-id="62b83-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="62b83-185">每次单击此按钮，则在前进执行到下一行代码。</span><span class="sxs-lookup"><span data-stu-id="62b83-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![单步执行按钮](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="62b83-187">检查的值`myTime`变量在其上停留鼠标指针或通过检查中显示的值**局部变量**并**调用堆栈**windows。</span><span class="sxs-lookup"><span data-stu-id="62b83-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="62b83-188">Visual Studio 显示变量的值。</span><span class="sxs-lookup"><span data-stu-id="62b83-188">Visual Studio display the value of the variable.</span></span>

    ![显示时间值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="62b83-190">完成检查变量和单步执行代码时，按 F5 继续运行而无需停止在每个行的页。</span><span class="sxs-lookup"><span data-stu-id="62b83-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="62b83-191">已完成逐步调试所有代码，浏览器显示的页面。</span><span class="sxs-lookup"><span data-stu-id="62b83-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="62b83-192">若要了解有关调试器以及如何在 Visual Studio 中调试代码的详细信息，请参阅[演练： 在 Visual Web Developer 中调试 Web Pages](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="62b83-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="62b83-193">在使用 Visual Studio 的 ASP.NET MVC 项目中使用 Razor</span><span class="sxs-lookup"><span data-stu-id="62b83-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="62b83-194">Razor 语法还在 ASP.NET MVC 项目中广泛使用。</span><span class="sxs-lookup"><span data-stu-id="62b83-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="62b83-195">MVC 是功能强大、 基于模式的方式来构建动态网站。</span><span class="sxs-lookup"><span data-stu-id="62b83-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="62b83-196">如果你的 ASP.NET Web Pages 站点变得难以维护，您可能需要考虑将其转换为 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="62b83-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="62b83-197">创建 MVC 应用程序的示例，请参阅[Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="62b83-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="62b83-198">在 Visual Studio 2010 中安装 ASP.NET Web pages 支持</span><span class="sxs-lookup"><span data-stu-id="62b83-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="62b83-199">本部分演示如何安装 Visual Web Developer 学习版 2010年和 ASP.NET Web Pages Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="62b83-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="62b83-200">如果还没有 Web 平台安装程序，请从以下 URL 下载：</span><span class="sxs-lookup"><span data-stu-id="62b83-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="62b83-201">运行 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="62b83-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="62b83-202">单击**产品**选项卡。</span><span class="sxs-lookup"><span data-stu-id="62b83-202">Click the **Products** tab.</span></span>

    ![WebPI 产品选项卡](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="62b83-204">搜索**ASP.NET MVC 4** （适用于 ASP.NET Web Pages 2)，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="62b83-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="62b83-205">这些产品包括 Visual Studio 工具，用于构建 ASP.NET Razor 网站。</span><span class="sxs-lookup"><span data-stu-id="62b83-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi 安装选项](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="62b83-207">单击**安装**以完成安装。</span><span class="sxs-lookup"><span data-stu-id="62b83-207">Click **Install** to complete the installation.</span></span>
