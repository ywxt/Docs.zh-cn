---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 编程 ASP.NET 网页 (Razor) 使用 Visual Studio |Microsoft 文档
author: tfitzmac
description: 本附录说明如何使用 Visual Studio 2010 或 Visual Web Developer 2010 Express 给程序的 ASP.NET Web Pages 使用 Razor 语法。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/13/2014
ms.topic: article
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: eb17c8cc1fab5b552c8495e74bb86ae9dbc5b972
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30896572"
---
<a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="96f82-103">使用 Visual Studio 编程 ASP.NET Web 页 (Razor)</span><span class="sxs-lookup"><span data-stu-id="96f82-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>
====================
<span data-ttu-id="96f82-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="96f82-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="96f82-105">此文章介绍了如何使用 Visual Studio 或 Visual Web Developer Express 给程序所需的 ASP.NET Web Pages (Razor) 网站。</span><span class="sxs-lookup"><span data-stu-id="96f82-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
> 
> <span data-ttu-id="96f82-106">学习内容</span><span class="sxs-lookup"><span data-stu-id="96f82-106">What you'll learn</span></span>
> 
> - <span data-ttu-id="96f82-107">需要安装 （如果有的话） 你的 Visual Studio 版本中的工作与 ASP.NET Web 页。</span><span class="sxs-lookup"><span data-stu-id="96f82-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="96f82-108">如何将支持为 ASP.NET 网页添加到 Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="96f82-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="96f82-109">如何使用 Visual Studio 中的功能用于 ASP.NET Razor 页，包括 IntelliSense 和调试程序。</span><span class="sxs-lookup"><span data-stu-id="96f82-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="96f82-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="96f82-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="96f82-111">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="96f82-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="96f82-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="96f82-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="96f82-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="96f82-113">WebMatrix 3</span></span>
>   
> 
> <span data-ttu-id="96f82-114">本教程还适用于 ASP.NET Web Pages 2、 Visual Studio 2012、 Visual Studio 2010 中，和 WebMatrix 2。</span><span class="sxs-lookup"><span data-stu-id="96f82-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>


<span data-ttu-id="96f82-115">使用 Razor 语法使用 WebMatrix 或许多其他代码编辑器，可以 ASP.NET Web 页进行编程。</span><span class="sxs-lookup"><span data-stu-id="96f82-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="96f82-116">你还可以使用 Microsoft Visual Studio 这是提供一套强大的工具创建的应用程序 （而不仅仅是网站） 的许多类型的全功能集成的开发环境 (IDE)。</span><span class="sxs-lookup"><span data-stu-id="96f82-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="96f82-117">若要使用 ASP.NET Razor 页，你可以使用 Visual Studio 的完整版本之一或者免费[Visual Studio Express for Web](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-2013-express)版本。</span><span class="sxs-lookup"><span data-stu-id="96f82-117">To work with ASP.NET Razor pages, you can either use one of the full editions of Visual Studio or the free [Visual Studio Express for Web](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-2013-express) edition.</span></span>

<span data-ttu-id="96f82-118">Visual Studio 提供了用于与 ASP.NET Razor 网页编程的两个特别有用功能是：</span><span class="sxs-lookup"><span data-stu-id="96f82-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="96f82-119">*IntelliSense*。</span><span class="sxs-lookup"><span data-stu-id="96f82-119">*IntelliSense*.</span></span> <span data-ttu-id="96f82-120">内置于 Visual Studio 中的 IntelliSense 功能是比在 WebMatrix 中的 IntelliSense 更全面。</span><span class="sxs-lookup"><span data-stu-id="96f82-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="96f82-121">*调试器*。</span><span class="sxs-lookup"><span data-stu-id="96f82-121">*Debugger*.</span></span> <span data-ttu-id="96f82-122">调试器可让您通过停止程序，它是运行、 检查变量和单步执行代码行的行时诊断你的代码。</span><span class="sxs-lookup"><span data-stu-id="96f82-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="96f82-123">Visual Studio 中使用不同版本的 ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="96f82-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="96f82-124">Visual Studio 2012 和 Visual Studio 2013 包括支持的 ASP.NET Web 页。</span><span class="sxs-lookup"><span data-stu-id="96f82-124">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="96f82-125">（为支持的 ASP.NET Web Pages 必需的包安装的安装 Visual Studio 时。）</span><span class="sxs-lookup"><span data-stu-id="96f82-125">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="96f82-126">Visual Studio 2010 不包括支持默认情况下为 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="96f82-126">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="96f82-127">若要使用 Visual Studio 2010 ASP.NET 网页，你必须安装 ASP.NET MVC 包。</span><span class="sxs-lookup"><span data-stu-id="96f82-127">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="96f82-128">若要获取 ASP.NET 网页 2，你需要安装 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="96f82-128">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="96f82-129">下表总结了不同版本的 Visual Studio 中的支持为 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="96f82-129">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="96f82-130">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="96f82-130">Visual Studio 2010</span></span> | <span data-ttu-id="96f82-131">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="96f82-131">Visual Studio 2012</span></span> | <span data-ttu-id="96f82-132">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="96f82-132">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="96f82-133">**ASP.NET Web Pages 2**</span><span class="sxs-lookup"><span data-stu-id="96f82-133">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="96f82-134">安装 ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="96f82-134">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="96f82-135">（包括）</span><span class="sxs-lookup"><span data-stu-id="96f82-135">(Included)</span></span> | <span data-ttu-id="96f82-136">（包括）</span><span class="sxs-lookup"><span data-stu-id="96f82-136">(Included)</span></span> |
| <span data-ttu-id="96f82-137">**ASP.NET Web Pages 3**</span><span class="sxs-lookup"><span data-stu-id="96f82-137">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="96f82-138">更新到 ASP.NET Web 页 3 通过 NuGet</span><span class="sxs-lookup"><span data-stu-id="96f82-138">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="96f82-139">（包括）</span><span class="sxs-lookup"><span data-stu-id="96f82-139">(Included)</span></span> |

<span data-ttu-id="96f82-140">若要使用 Visual Studio 2010，请参阅[安装支持 ASP.NET Web 页的 Visual Studio 2010 中](#vs2010support)。</span><span class="sxs-lookup"><span data-stu-id="96f82-140">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="96f82-141">启动 Visual Studio 中的，从 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="96f82-141">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="96f82-142">如果你已在 WebMatrix 中启动项目，并想要切换到 Visual Studio，WebMatrix 将提供用于轻松地在 Visual Studio 中打开项目的按钮。</span><span class="sxs-lookup"><span data-stu-id="96f82-142">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="96f82-143">你必须安装 Visual Studio 此按钮在计算机上启用。</span><span class="sxs-lookup"><span data-stu-id="96f82-143">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="96f82-144">下图显示在 WebMatrix 中的按钮。</span><span class="sxs-lookup"><span data-stu-id="96f82-144">The following image shows the button in WebMatrix.</span></span>

![启动 Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="96f82-146">单击按钮时，在 Visual Studio 中打开该项目。</span><span class="sxs-lookup"><span data-stu-id="96f82-146">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="96f82-147">你可以来回切换 WebMatrix 和 Visual Studio 之间没有任何问题。</span><span class="sxs-lookup"><span data-stu-id="96f82-147">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="96f82-148">如果任何文件中另一个环境中已更改并且需要重新加载以获取最新的更改，你将收到通知。</span><span class="sxs-lookup"><span data-stu-id="96f82-148">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="96f82-149">在 Visual Studio 中创建 ASP.NET Razor 站点</span><span class="sxs-lookup"><span data-stu-id="96f82-149">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="96f82-150">在 Visual Studio 中创建 ASP.NET Razor 网站：</span><span class="sxs-lookup"><span data-stu-id="96f82-150">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="96f82-151">Visual Studio 或 Visual Web Developer 启动。</span><span class="sxs-lookup"><span data-stu-id="96f82-151">Start Visual Studio or Visual Web Developer.</span></span>
2. <span data-ttu-id="96f82-152">在**文件**菜单上，单击**新网站**。</span><span class="sxs-lookup"><span data-stu-id="96f82-152">In the **File** menu, click **New Web Site**.</span></span>

    ![创建新网站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="96f82-154">在**新网站**对话框框中，选择要使用 （Visual C# 或 Visual Basic） 的语言。</span><span class="sxs-lookup"><span data-stu-id="96f82-154">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="96f82-155">选择**ASP.NET 网站 (Razor)** 模板。</span><span class="sxs-lookup"><span data-stu-id="96f82-155">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![razor 站点](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="96f82-157">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="96f82-157">Click **OK**.</span></span>

<span data-ttu-id="96f82-158">新的项目中存在，且使用某些默认的 web 页面以帮助你开始填充。</span><span class="sxs-lookup"><span data-stu-id="96f82-158">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="96f82-159">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="96f82-159">Using IntelliSense</span></span>

<span data-ttu-id="96f82-160">现在，你已创建站点，你可以看到在 Visual Studio 中的 IntelliSense 工作原理。</span><span class="sxs-lookup"><span data-stu-id="96f82-160">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="96f82-161">在你刚创建的网站，打开*Default.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="96f82-161">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="96f82-162">后`<h3>`标记在页中，键入`@ServerInfo.`（包括该点）。</span><span class="sxs-lookup"><span data-stu-id="96f82-162">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="96f82-163">请注意如何 IntelliSense 显示的可用方法`ServerInfo`下拉列表中的帮助器。</span><span class="sxs-lookup"><span data-stu-id="96f82-163">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span> 

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="96f82-165">选择`GetHtml`方法从列表，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="96f82-165">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="96f82-166">IntelliSense 会自动填写方法中。</span><span class="sxs-lookup"><span data-stu-id="96f82-166">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="96f82-167">(如使用 C# 中的任何方法，你必须添加`()`在方法之后的字符。)</span><span class="sxs-lookup"><span data-stu-id="96f82-167">(As with any method in C#, you must add `()` characters after the method.)</span></span>  
   <span data-ttu-id="96f82-168">已完成的代码`GetHtml`方法类似于下面的示例：</span><span class="sxs-lookup"><span data-stu-id="96f82-168">The completed code for the `GetHtml` method looks like the following example:</span></span>  

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="96f82-169">按 Ctrl + F5 运行页面。</span><span class="sxs-lookup"><span data-stu-id="96f82-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="96f82-170">这是什么时显示在浏览器中网页的外观：</span><span class="sxs-lookup"><span data-stu-id="96f82-170">This is what the page looks like when displayed in a browser:</span></span> 

    ![在浏览器中的默认页](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="96f82-172">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="96f82-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="96f82-173">使用调试器</span><span class="sxs-lookup"><span data-stu-id="96f82-173">Using the Debugger</span></span>

1. <span data-ttu-id="96f82-174">在顶部*Default.cshtml*页上，开头的行之后`Page.Title`，添加以下代码行：</span><span class="sxs-lookup"><span data-stu-id="96f82-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span> 

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="96f82-175">在左侧的代码编辑器的灰色边缘，单击此新行的旁边为了添加*断点*。</span><span class="sxs-lookup"><span data-stu-id="96f82-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="96f82-176">断点是一种标记，告知调试器停止在该点运行程序，以便你可以查看发生了什么情况。</span><span class="sxs-lookup"><span data-stu-id="96f82-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![设置断点](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="96f82-178">删除对的调用`ServerInfo.GetHtml`方法，并添加对的调用`@myTime`变量在其位置。</span><span class="sxs-lookup"><span data-stu-id="96f82-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="96f82-179">此调用将显示由新的代码行的当前时间值。</span><span class="sxs-lookup"><span data-stu-id="96f82-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="96f82-180">按 F5 以在调试器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="96f82-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="96f82-181">页会在你设置的断点处停止。</span><span class="sxs-lookup"><span data-stu-id="96f82-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="96f82-182">下图显示了页面外观在编辑器中使用断点 （用黄色）。</span><span class="sxs-lookup"><span data-stu-id="96f82-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span> 

    ![调试断点](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="96f82-184">在调试工具栏中，单击**单步执行**按钮 （或按 F11） 以运行下一个代码行。</span><span class="sxs-lookup"><span data-stu-id="96f82-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="96f82-185">单击此按钮时，每次你向前执行移动到下一行代码。</span><span class="sxs-lookup"><span data-stu-id="96f82-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![单步执行按钮](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="96f82-187">检查的值`myTime`变量在其上停留鼠标指针或通过检查中显示的值**局部变量**和**调用堆栈**windows。</span><span class="sxs-lookup"><span data-stu-id="96f82-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="96f82-188">Visual Studio 显示变量的值。</span><span class="sxs-lookup"><span data-stu-id="96f82-188">Visual Studio display the value of the variable.</span></span>

    ![显示时间值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="96f82-190">当完成时检查变量和逐句通过代码时，按 F5 以继续运行而不停止在每个行的页。</span><span class="sxs-lookup"><span data-stu-id="96f82-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="96f82-191">在单步执行所有代码完后，浏览器将显示页。</span><span class="sxs-lookup"><span data-stu-id="96f82-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="96f82-192">若要了解有关调试器以及如何调试 Visual Studio 中的代码的详细信息，请参阅[演练： 在 Visual Web Developer 调试 Web 页](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="96f82-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="96f82-193">在使用 Visual Studio 的 ASP.NET MVC 项目中使用 Razor</span><span class="sxs-lookup"><span data-stu-id="96f82-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="96f82-194">ASP.NET MVC 项目中还进行了广泛使用 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="96f82-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="96f82-195">MVC 是构建动态网站功能强大、 基于模式的方法。</span><span class="sxs-lookup"><span data-stu-id="96f82-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="96f82-196">如果你的 ASP.NET Web Pages 站点变得难以维护，你可能想要考虑将其转换为 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="96f82-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="96f82-197">有关创建 MVC 应用程序的示例，请参阅[Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="96f82-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="96f82-198">在 Visual Studio 2010 安装 ASP.NET 网页的支持</span><span class="sxs-lookup"><span data-stu-id="96f82-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="96f82-199">本部分演示如何安装 Visual Web Developer Express 2010 以及 ASP.NET 网页 Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="96f82-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="96f82-200">如果你尚未安装 Web 平台安装程序，请从以下 URL 下载它：</span><span class="sxs-lookup"><span data-stu-id="96f82-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="96f82-201">运行 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="96f82-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="96f82-202">单击**产品**选项卡。</span><span class="sxs-lookup"><span data-stu-id="96f82-202">Click the **Products** tab.</span></span>

    ![WebPI 产品选项卡](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="96f82-204">搜索**ASP.NET MVC 4** （适用于 ASP.NET Web Pages 2)，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="96f82-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="96f82-205">这些产品包括 Visual Studio 工具生成 ASP.NET Razor 网站。</span><span class="sxs-lookup"><span data-stu-id="96f82-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi 安装选项](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="96f82-207">单击**安装**以完成安装。</span><span class="sxs-lookup"><span data-stu-id="96f82-207">Click **Install** to complete the installation.</span></span>
