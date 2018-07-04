---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: 在 Visual Studio 2012 中使用 Page Inspector |Microsoft Docs
author: rick-anderson
description: 在本动手实验中，你会发现新的工具来查找和修复 Visual Studio-Page Inspector 中的 web 页的问题。 Page Inspector 是一个新工具： b...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 236b739abb8c9073535361040dd7d921da9dba6e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365719"
---
<a name="using-page-inspector-in-visual-studio-2012"></a><span data-ttu-id="86803-104">在 Visual Studio 2012 中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="86803-104">Using Page Inspector in Visual Studio 2012</span></span>
====================
<span data-ttu-id="86803-105">通过[Web 训练营团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="86803-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="86803-106">在本动手实验中，你会发现新的工具来查找和修复 Visual Studio-Page Inspector 中的 web 页的问题。</span><span class="sxs-lookup"><span data-stu-id="86803-106">In this Hands-on Lab, you will discover a new tool to find and fix web page issues in Visual Studio - the Page Inspector.</span></span>
> 
> <span data-ttu-id="86803-107">Page Inspector 是一个新工具，Visual studio 将浏览器诊断工具，并提供在浏览器、 ASP.NET 和源代码之间的集成的体验。</span><span class="sxs-lookup"><span data-stu-id="86803-107">Page Inspector is a new tool that brings browser diagnostics tools to Visual Studio and provides an integrated experience among the browser, ASP.NET, and source code.</span></span> <span data-ttu-id="86803-108">它呈现网页 （HTML、 Web 窗体、 ASP.NET MVC 或网页） 直接在 Visual Studio IDE 中，并允许您检查源代码和生成的输出。</span><span class="sxs-lookup"><span data-stu-id="86803-108">It renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) directly within the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="86803-109">Page Inspector，可轻松地分解网站、 快速生成从零开始的页面，并快速诊断问题。</span><span class="sxs-lookup"><span data-stu-id="86803-109">Page Inspector enables you to easily decompose a website, rapidly build pages from the ground up, and quickly diagnose issues.</span></span>
> 
> <span data-ttu-id="86803-110">现在我们有许多及时地，如 ASP.NET MVC 和 WebForms 创建灵活且可缩放的网站的 Web 框架。</span><span class="sxs-lookup"><span data-stu-id="86803-110">Nowadays we have a number of Web frameworks that create flexible and scalable websites in a timely manner, such as ASP.NET MVC and WebForms.</span></span> <span data-ttu-id="86803-111">但是，它获取更难发现的页上的问题，因为 IDE 不支持在基于模板的页面和动态内容中的设计器视图。</span><span class="sxs-lookup"><span data-stu-id="86803-111">On the other hand, it gets harder to find issues on the pages because the IDE does not support the designer view in template-based pages and dynamic content.</span></span> <span data-ttu-id="86803-112">因此，这些网站必须打开在浏览器中查看它们如何向用户显示。</span><span class="sxs-lookup"><span data-stu-id="86803-112">Therefore, these websites have to be opened in a browser to see how they appear to a user.</span></span>
> 
> <span data-ttu-id="86803-113">Web 开发人员使用外部工具发现定期运行在浏览器中的问题。</span><span class="sxs-lookup"><span data-stu-id="86803-113">Web developers use external tools to find issues that regularly run in the browser.</span></span> <span data-ttu-id="86803-114">然后，它们返回到 IDE，并着手修复。</span><span class="sxs-lookup"><span data-stu-id="86803-114">Then, they return to the IDE and start fixing.</span></span> <span data-ttu-id="86803-115">这来回 IDE、 浏览器和分析工具之间的活动可能效率很低，并且有时需要全新部署和清除每个希望以重现某个问题的时间的缓存。</span><span class="sxs-lookup"><span data-stu-id="86803-115">This back and forth activity among the IDE, the browser and the profiling tools can be inefficient, and sometimes requires a fresh deployment and cache cleaning each time you want to reproduce an issue.</span></span>
> 
> <span data-ttu-id="86803-116">Page Inspector 通过组合在一起的使用组合的功能集这两个优势来桥接客户端 （浏览器工具） 和服务器 （ASP.NET 和源代码代码） 之间的 Web 开发中存在间隔。</span><span class="sxs-lookup"><span data-stu-id="86803-116">Page Inspector bridges a gap in Web development between the client (browser tools) and the server (ASP.NET and source code) by bringing together the best of both worlds using a combined set of features.</span></span>
> 
> <span data-ttu-id="86803-117">使用 Page Inspector，您可以看到源文件 （包括服务器端代码） 中的哪些元素具有生成在浏览器中呈现的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="86803-117">Using Page Inspector, you can see which elements in the source files (including server-side code) have produced the HTML markup to be rendered in the browser.</span></span> <span data-ttu-id="86803-118">Page Inspector 还允许您修改 CSS 属性和 DOM 元素特性，若要查看立即反映在浏览器中的更改。</span><span class="sxs-lookup"><span data-stu-id="86803-118">Page Inspector also lets you modify CSS properties and DOM element attributes to see the changes reflected immediately in the browser.</span></span>
> 
> <span data-ttu-id="86803-119">本动手实验将向您介绍 Page Inspector 功能并向您展示如何使用它们来修复 Web 应用程序中的问题。</span><span class="sxs-lookup"><span data-stu-id="86803-119">This hands-on lab will walk you through the Page Inspector features and show you how you can use them to fix issues in Web applications.</span></span> <span data-ttu-id="86803-120">**此实验室中包含两个练习使用类似的流，但面向不同的技术。如果你是 ASP.NET MVC 开发人员，完成练习如果您是两个 WebForms 开发人员按照练习**。</span><span class="sxs-lookup"><span data-stu-id="86803-120">**This lab contains two exercises using similar flows but targeting different technologies. If you are an ASP.NET MVC Developer, follow exercise one; if you are a WebForms developer follow exercise two**.</span></span>
> 
> <span data-ttu-id="86803-121">此实验室将引导你通过前面所述通过将细微的更改应用于源文件夹中提供的示例 Web 应用的新功能和增强功能。</span><span class="sxs-lookup"><span data-stu-id="86803-121">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="86803-122">在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="86803-122">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="86803-123">目标</span><span class="sxs-lookup"><span data-stu-id="86803-123">Objectives</span></span>

<span data-ttu-id="86803-124">在本动手实验，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="86803-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="86803-125">分解使用 Page Inspector 的 Web 站点</span><span class="sxs-lookup"><span data-stu-id="86803-125">Decompose a Web Site using Page Inspector</span></span>
- <span data-ttu-id="86803-126">检查并预览使用 Page Inspector 的 CSS 样式更改</span><span class="sxs-lookup"><span data-stu-id="86803-126">Inspect and preview CSS styles changes with Page Inspector</span></span>
- <span data-ttu-id="86803-127">检测和修复使用 Page Inspector 在网页中的问题</span><span class="sxs-lookup"><span data-stu-id="86803-127">Detect and fix issues in your web pages using Page Inspector</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="86803-128">系统必备</span><span class="sxs-lookup"><span data-stu-id="86803-128">Prerequisites</span></span>

<span data-ttu-id="86803-129">必须具有要完成本实验的以下项：</span><span class="sxs-lookup"><span data-stu-id="86803-129">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="86803-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="86803-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="86803-131">Internet Explorer 9 或更高版本</span><span class="sxs-lookup"><span data-stu-id="86803-131">Internet Explorer 9 or higher</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="86803-132">练习</span><span class="sxs-lookup"><span data-stu-id="86803-132">Exercises</span></span>

<span data-ttu-id="86803-133">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="86803-133">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="86803-134">练习 1： 在 ASP.NET MVC 项目中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="86803-134">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>](#Exercise1)
2. [<span data-ttu-id="86803-135">练习 2： 在 WebForms 项目中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="86803-135">Exercise 2: Using Page Inspector in WebForms Projects</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="86803-136">每个练习均附带位于该练习，可用于完成独立于其他每个练习的 Begin 文件夹中的起始解决方案。</span><span class="sxs-lookup"><span data-stu-id="86803-136">Each exercise is accompanied by a starting solution, located in the Begin folder of the exercise, that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="86803-137">在练习的源代码，还会发现一个 End 文件夹，其中包含具有无法完成相应练习中的步骤得到的代码的 Visual Studio 解决方案。</span><span class="sxs-lookup"><span data-stu-id="86803-137">Inside the source code for an exercise, you will also find an End folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="86803-138">如果您在演练本动手实验需要更多帮助，可以使用这些解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="86803-138">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


<span data-ttu-id="86803-139">估计的时间才能完成此实验： **30 分钟**。</span><span class="sxs-lookup"><span data-stu-id="86803-139">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a><span data-ttu-id="86803-140">练习 1： 在 ASP.NET MVC 项目中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="86803-140">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>

<span data-ttu-id="86803-141">在此练习中，您将学习如何预览和调试**ASP.NET MVC 4**解决方案： 使用**Page Inspector**。</span><span class="sxs-lookup"><span data-stu-id="86803-141">In this exercise, you will learn how to preview and debug an **ASP.NET MVC 4** solution using **Page Inspector**.</span></span> <span data-ttu-id="86803-142">首先，您将执行简要了解该工具来了解促进 Web 调试进程的功能。</span><span class="sxs-lookup"><span data-stu-id="86803-142">First, you will perform a brief lap around the tool to learn the features that facilitate the Web debugging process.</span></span> <span data-ttu-id="86803-143">然后，您可以在包含样式设置问题的网页中。</span><span class="sxs-lookup"><span data-stu-id="86803-143">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="86803-144">您将学习如何使用 Page Inspector 找到生成问题的源代码和修复此错误。</span><span class="sxs-lookup"><span data-stu-id="86803-144">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="86803-145">任务 1-浏览页面检查器</span><span class="sxs-lookup"><span data-stu-id="86803-145">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="86803-146">在本任务中，您将学习如何在显示照片库的 ASP.NET MVC 4 项目的上下文中使用 Page Inspector。</span><span class="sxs-lookup"><span data-stu-id="86803-146">In this task, you will learn how to use the Page Inspector in the context of an ASP.NET MVC 4 project that shows a photo gallery.</span></span>

1. <span data-ttu-id="86803-147">打开**开始**解决方案位于**源/Ex1-MVC4/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="86803-147">Open the **Begin** solution located at **Source/Ex1-MVC4/Begin/** folder.</span></span>

   1. <span data-ttu-id="86803-148">需要先下载某些缺少的 NuGet 包然后再继续。</span><span class="sxs-lookup"><span data-stu-id="86803-148">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="86803-149">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="86803-149">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="86803-150">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="86803-150">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="86803-151">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="86803-151">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="86803-152">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="86803-152">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="86803-153">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="86803-153">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="86803-154">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="86803-154">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="86803-155">在解决方案资源管理器，找到**Index.cshtml**下查看 **/views/home**项目文件夹，右键单击它并选择**在 Page Inspector 中的查看**。</span><span class="sxs-lookup"><span data-stu-id="86803-155">In the Solution Explorer, locate **Index.cshtml** view under the **/Views/Home** project folder, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="86803-156">![选择一个文件，若要预览在 Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image1.png "选择要预览在 Page Inspector 中的文件")</span><span class="sxs-lookup"><span data-stu-id="86803-156">![Selecting a file to preview in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image1.png "Selecting a file to preview in Page Inspector")</span></span>

    <span data-ttu-id="86803-157">*选择要预览在 Page Inspector 中的文件*</span><span class="sxs-lookup"><span data-stu-id="86803-157">*Selecting a file to preview in Page Inspector*</span></span>
3. <span data-ttu-id="86803-158">Page Inspector 窗口将显示 */Home/Index* URL 映射到所选的视图的源。</span><span class="sxs-lookup"><span data-stu-id="86803-158">The Page Inspector window will show the */Home/Index* URL mapped to the source View you selected.</span></span>

    ![ThefirstcontactwithPageInspector](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    <span data-ttu-id="86803-160">*使用 Page Inspector 第一次联系*</span><span class="sxs-lookup"><span data-stu-id="86803-160">*The first contact with Page Inspector*</span></span>

    <span data-ttu-id="86803-161">Page Inspector 工具已集成在 Visual Studio 环境中。</span><span class="sxs-lookup"><span data-stu-id="86803-161">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="86803-162">该检查器包含嵌入式浏览器，以及功能强大的 HTML 探查器。</span><span class="sxs-lookup"><span data-stu-id="86803-162">The inspector contains an embedded browser, together with a powerful HTML profiler.</span></span> <span data-ttu-id="86803-163">请注意，不需要运行解决方案，以查看您的页面的外观。</span><span class="sxs-lookup"><span data-stu-id="86803-163">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86803-164">当 Page Inspector 浏览器宽度小于所打开的页的宽度时，您不会正确地看到页面。</span><span class="sxs-lookup"><span data-stu-id="86803-164">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="86803-165">如果发生这种情况，调整页面检查器的宽度。</span><span class="sxs-lookup"><span data-stu-id="86803-165">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="86803-166">单击**文件**在 Page Inspector 中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="86803-166">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="86803-167">您将看到正在撰写的索引页的所有源文件。</span><span class="sxs-lookup"><span data-stu-id="86803-167">You will see all the source files that are composing the Index page.</span></span> <span data-ttu-id="86803-168">此功能有助于识别一眼的所有元素，尤其是当你正在使用分部视图和模板。</span><span class="sxs-lookup"><span data-stu-id="86803-168">This feature helps to identify all the elements at a glance, especially when you are working with partial views and templates.</span></span> <span data-ttu-id="86803-169">请注意，您还可以打开每个文件，是否单击的链接。</span><span class="sxs-lookup"><span data-stu-id="86803-169">Notice that you can also open each of the files if you click the links.</span></span>

    ![The-Files-tab](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    <span data-ttu-id="86803-171">*文件选项卡*</span><span class="sxs-lookup"><span data-stu-id="86803-171">*The Files tab*</span></span>
5. <span data-ttu-id="86803-172">单击**切换检查模式下**按钮，位于左侧的选项卡。</span><span class="sxs-lookup"><span data-stu-id="86803-172">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="86803-173">此工具会让您选择的页的任何元素，并查看其 HTML 和 Razor 代码。</span><span class="sxs-lookup"><span data-stu-id="86803-173">This tool will let you select any element of the page and see its HTML and Razor code.</span></span>

    ![Toggle-Inspection-Mode-button](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    <span data-ttu-id="86803-175">*切换检查模式按钮*</span><span class="sxs-lookup"><span data-stu-id="86803-175">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="86803-176">在 Page Inspector 浏览器中，将鼠标指针移动页面元素。</span><span class="sxs-lookup"><span data-stu-id="86803-176">In the Page Inspector browser, move the mouse pointer over the page elements.</span></span> <span data-ttu-id="86803-177">将鼠标指针移过所呈现页中的任何部分，而显示的元素类型和 Visual Studio 编辑器中突出显示相应的源标记或代码。</span><span class="sxs-lookup"><span data-stu-id="86803-177">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    ![Inspectionmodeinaction](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    <span data-ttu-id="86803-179">*在操作中检查模式*</span><span class="sxs-lookup"><span data-stu-id="86803-179">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="86803-180">不最大化页面检查器窗口或你将无法再看到显示的源代码的预览选项卡。</span><span class="sxs-lookup"><span data-stu-id="86803-180">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="86803-181">如果它最大化时单击 Page Inspector 中的元素，将显示所选内容的源代码，但它会隐藏页面检查器窗口。</span><span class="sxs-lookup"><span data-stu-id="86803-181">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="86803-182">如果您注意到**Index.cshtml**文件中，你会注意到，突出显示的源代码的生成所选的元素的部分。</span><span class="sxs-lookup"><span data-stu-id="86803-182">If you pay attention to the **Index.cshtml** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="86803-183">此功能便于编辑长源代码文件，提供指导支持和快速的方法来访问代码。</span><span class="sxs-lookup"><span data-stu-id="86803-183">This feature facilitates the editing of long source files, providing a direct and fast way to access the code.</span></span>

    ![Inspectingelements](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    <span data-ttu-id="86803-185">*检查元素*</span><span class="sxs-lookup"><span data-stu-id="86803-185">*Inspecting elements*</span></span>
7. <span data-ttu-id="86803-186">单击**切换检查模式下**按钮 (![选择 HTML 选项卡以显示在 Page Inspector 浏览器中呈现的 HTML 代码。](using-page-inspector-in-visual-studio-2012/_static/image7.png "选择 HTML 选项卡以显示在 Page Inspector 浏览器中呈现的 HTML 代码。")</span><span class="sxs-lookup"><span data-stu-id="86803-186">Click the **Toggle Inspection Mode** button (![Select the HTML tab to display the HTML code rendered in the Page Inspector browser.](using-page-inspector-in-visual-studio-2012/_static/image7.png "Select the HTML tab to display the HTML code rendered in the Page Inspector browser.")</span></span> <span data-ttu-id="86803-187">) 若要禁用光标。</span><span class="sxs-lookup"><span data-stu-id="86803-187">) to disable the cursor.</span></span>
8. <span data-ttu-id="86803-188">选择**HTML**选项卡以显示在 Page Inspector 浏览器中呈现的 HTML 代码。</span><span class="sxs-lookup"><span data-stu-id="86803-188">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="86803-189">在 HTML 标记中，找到与 Koala 链接的列表项并选择它。</span><span class="sxs-lookup"><span data-stu-id="86803-189">In the HTML markup, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="86803-190">请注意，当您选择的代码，相应的输出自动突出显示在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="86803-190">Notice that when you select the code, the corresponding output is automatically highlighted in the browser.</span></span> <span data-ttu-id="86803-191">此功能可用于查看 HTML 块的页上的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="86803-191">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="86803-192">![在页中的选择 HTML 元素](using-page-inspector-in-visual-studio-2012/_static/image8.png "页中的选择 HTML 元素")</span><span class="sxs-lookup"><span data-stu-id="86803-192">![Selecting HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image8.png "Selecting HTML element in the page")</span></span>

    <span data-ttu-id="86803-193">*在页面中选择 HTML 元素*</span><span class="sxs-lookup"><span data-stu-id="86803-193">*Selecting HTML element in the page*</span></span>
10. <span data-ttu-id="86803-194">单击**切换检查模式下**按钮以启用*检查模式下*单击导航栏。</span><span class="sxs-lookup"><span data-stu-id="86803-194">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="86803-195">右侧的 HTML 代码，在样式窗格中，将看到列表，与应用于所选元素的 CSS 样式。</span><span class="sxs-lookup"><span data-stu-id="86803-195">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86803-196">因为标头是站点布局的一部分，Page Inspector 将打开\_Layout.cshtml 文件并突出显示的代码段会受到影响。</span><span class="sxs-lookup"><span data-stu-id="86803-196">Since the header is a part of the site layout, Page Inspector will also open \_Layout.cshtml file and highlight the segment of code affected.</span></span>

    ![Discoveringstyles](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    <span data-ttu-id="86803-198">*发现所选元素的样式和源文件*</span><span class="sxs-lookup"><span data-stu-id="86803-198">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="86803-199">启用切换检查指针，移动鼠标指针下面特色的蓝色条形，再单击一半的圆圈。</span><span class="sxs-lookup"><span data-stu-id="86803-199">With the toggle inspection pointer enabled, move the mouse pointer below the blue featured bar and click the half circle.</span></span>

    <span data-ttu-id="86803-200">![选择元素](using-page-inspector-in-visual-studio-2012/_static/image10.png "选择元素")</span><span class="sxs-lookup"><span data-stu-id="86803-200">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image10.png "Selecting an element")</span></span>

    <span data-ttu-id="86803-201">*选择元素*</span><span class="sxs-lookup"><span data-stu-id="86803-201">*Selecting an element*</span></span>
12. <span data-ttu-id="86803-202">在样式窗格中，找到**背景图像**项下 **.main 内容**组。</span><span class="sxs-lookup"><span data-stu-id="86803-202">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="86803-203">**取消选中****背景图像**，看看效果。</span><span class="sxs-lookup"><span data-stu-id="86803-203">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="86803-204">您将注意到浏览器将立即反映所做的更改，并且该圆形处于隐藏状态。</span><span class="sxs-lookup"><span data-stu-id="86803-204">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86803-205">在页面检查器样式的选项卡上应用的更改不会影响原始样式表。</span><span class="sxs-lookup"><span data-stu-id="86803-205">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="86803-206">您可以取消选中样式或更改无数次，但它们会在还原刷新页面后，其值。</span><span class="sxs-lookup"><span data-stu-id="86803-206">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="86803-207">![启用和禁用 CSS 样式](using-page-inspector-in-visual-studio-2012/_static/image11.png "启用和禁用 CSS 样式")</span><span class="sxs-lookup"><span data-stu-id="86803-207">![Enabling and disabling CSS styles](using-page-inspector-in-visual-studio-2012/_static/image11.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="86803-208">*启用和禁用 CSS 样式*</span><span class="sxs-lookup"><span data-stu-id="86803-208">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="86803-209">现在，单击**徽标此处**上使用检查模式下的标头的文本。</span><span class="sxs-lookup"><span data-stu-id="86803-209">Now, click the '**your logo here**' text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="86803-210">在中**样式**选项卡上，找到**字体大小**CSS 属性下 **.site 标题**组。</span><span class="sxs-lookup"><span data-stu-id="86803-210">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="86803-211">双击属性值，然后将 2.3 em 值替换为**3 个 em**，然后按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="86803-211">Double-click the attribute value and replace the 2.3 em value with **3 em**, and then press **ENTER**.</span></span> <span data-ttu-id="86803-212">请注意，标题看上去更大。</span><span class="sxs-lookup"><span data-stu-id="86803-212">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="86803-213">![更改在 Page Inspector 中的 CSS 值](using-page-inspector-in-visual-studio-2012/_static/image12.png "在 Page Inspector 中的更改的 CSS 值")</span><span class="sxs-lookup"><span data-stu-id="86803-213">![Changing CSS values in the Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image12.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="86803-214">*更改在 Page Inspector 中的 CSS 值*</span><span class="sxs-lookup"><span data-stu-id="86803-214">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="86803-215">单击**跟踪样式**选项卡上，Page Inspector 的右窗格中。</span><span class="sxs-lookup"><span data-stu-id="86803-215">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="86803-216">这是一种方法来查看应用于所选内容，按属性名称排序的所有样式。</span><span class="sxs-lookup"><span data-stu-id="86803-216">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    ![CSSstylestracing](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    <span data-ttu-id="86803-218">*所选元素的 CSS 样式跟踪*</span><span class="sxs-lookup"><span data-stu-id="86803-218">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="86803-219">Page Inspector 的另一个功能是布局窗格。</span><span class="sxs-lookup"><span data-stu-id="86803-219">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="86803-220">使用检查模式下，选择导航栏，然后单击**布局**右窗格上的选项卡。</span><span class="sxs-lookup"><span data-stu-id="86803-220">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="86803-221">你将看到所选元素的确切大小以及其偏移量、 边距、 填充和边框的大小。</span><span class="sxs-lookup"><span data-stu-id="86803-221">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="86803-222">请注意，您还可以修改此视图中的值。</span><span class="sxs-lookup"><span data-stu-id="86803-222">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="86803-223">![在 Page Inspector 中的元素布局](using-page-inspector-in-visual-studio-2012/_static/image14.png "在 Page Inspector 中的元素布局")</span><span class="sxs-lookup"><span data-stu-id="86803-223">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image14.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="86803-224">*在 Page Inspector 中的元素布局*</span><span class="sxs-lookup"><span data-stu-id="86803-224">*Element layout in Page Inspector*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="86803-225">任务 2-查找并修复在照片库中的样式问题</span><span class="sxs-lookup"><span data-stu-id="86803-225">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="86803-226">如何诊断与以前版本的 Visual Studio 的网页问题？</span><span class="sxs-lookup"><span data-stu-id="86803-226">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="86803-227">您将可能非常熟悉 web 调试工具，Visual Studio IDE，如 Internet Explorer 开发人员工具或 Firebug 之外运行。</span><span class="sxs-lookup"><span data-stu-id="86803-227">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="86803-228">浏览器只了解 HTML、 脚本和样式，而基础框架生成将呈现的 HTML。</span><span class="sxs-lookup"><span data-stu-id="86803-228">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="86803-229">为此，通常需要部署的整个站点，以查看网页的显示效果。</span><span class="sxs-lookup"><span data-stu-id="86803-229">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="86803-230">当你想要检测和修复问题，在您的网站时，可能必须遵循以下步骤：</span><span class="sxs-lookup"><span data-stu-id="86803-230">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="86803-231">从 Visual Studio 中，运行该解决方案或部署 web 服务器上的页。</span><span class="sxs-lookup"><span data-stu-id="86803-231">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="86803-232">在浏览器中打开开发人员工具使用，或只需打开源代码和样式并会尝试匹配该问题。</span><span class="sxs-lookup"><span data-stu-id="86803-232">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="86803-233">若要查找所涉及的文件，你会使用&quot;搜索&quot;或&quot;文件中的搜索&quot;样式类同名的功能。</span><span class="sxs-lookup"><span data-stu-id="86803-233">To find the files involved, you would have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="86803-234">一旦检测到错误，停止 Web 浏览器和服务器。</span><span class="sxs-lookup"><span data-stu-id="86803-234">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="86803-235">清除浏览器缓存。</span><span class="sxs-lookup"><span data-stu-id="86803-235">Clear the browser cache.</span></span>
5. <span data-ttu-id="86803-236">返回到 Visual Studio 来应用修补程序。</span><span class="sxs-lookup"><span data-stu-id="86803-236">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="86803-237">重复测试的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="86803-237">Repeat all the steps to test.</span></span>

<span data-ttu-id="86803-238">因为 ASP.NET MVC 4 中没有任何真正所见即所得，大部分样式问题上检测到后面的阶段，在运行或 web 应用程序部署后。</span><span class="sxs-lookup"><span data-stu-id="86803-238">As there is no real WYSIWYG in ASP.NET MVC 4, most of the style issues are detected on a later stage, after running or deploying the web application.</span></span> <span data-ttu-id="86803-239">现在，使用 Page Inspector，可以预览任何页，而无需运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="86803-239">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="86803-240">在此任务中，将使用 Page inspector 和修复照片库应用程序的一些问题。</span><span class="sxs-lookup"><span data-stu-id="86803-240">In this task, you will use the Page inspector and fix some issues the Photo Gallery application.</span></span>

1. <span data-ttu-id="86803-241">使用 Page Inspector，找到**注册**并**登录**标头的左侧的链接。</span><span class="sxs-lookup"><span data-stu-id="86803-241">Using Page Inspector, locate the **Register** and the **Log in** links at the left side of the header.</span></span>

    <span data-ttu-id="86803-242">请注意，链接不会显示在预期位置在右侧，它们会显示类似项目符号列表。</span><span class="sxs-lookup"><span data-stu-id="86803-242">Notice that the links are not displayed at the expected place on the right, and they are shown like a bulleted list.</span></span> <span data-ttu-id="86803-243">现在将对齐到右侧的链接，并可以相应地重新应用。</span><span class="sxs-lookup"><span data-stu-id="86803-243">You will now align the links to the right and restyle them accordingly.</span></span>

    <span data-ttu-id="86803-244">![在链接中查找的注册和日志](using-page-inspector-in-visual-studio-2012/_static/image15.png "在链接中查找的注册和日志")</span><span class="sxs-lookup"><span data-stu-id="86803-244">![Locating the Register and Log in links](using-page-inspector-in-visual-studio-2012/_static/image15.png "Locating the Register and Log in links")</span></span>

    <span data-ttu-id="86803-245">*在链接中查找的注册和日志*</span><span class="sxs-lookup"><span data-stu-id="86803-245">*Locating the Register and Log in links*</span></span>
2. <span data-ttu-id="86803-246">选择切换检查模式下，单击要关闭，但不是在注册链接以打开其代码。</span><span class="sxs-lookup"><span data-stu-id="86803-246">With Toggle Inspection Mode selected, click close to, but not on, the Register link to open its code.</span></span>

    <span data-ttu-id="86803-247">请注意，链接的源代码位于 **\_LoginPartial.cshtml**文件，不 Index.cshtml 和\_Layout.cshtml，是您可以在第一个位置中查找的位置。</span><span class="sxs-lookup"><span data-stu-id="86803-247">Notice that the source code of the links is located in the **\_LoginPartial.cshtml** file, not the Index.cshtml nor the \_Layout.cshtml, which are the places you might look in first place.</span></span> <span data-ttu-id="86803-248">你具有已直接放在正确的源文件。</span><span class="sxs-lookup"><span data-stu-id="86803-248">You have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="86803-249">在中**样式**选项卡上，找到并单击**<section> #login</section>** 项，它是下面的链接的 HTML 容器。</span><span class="sxs-lookup"><span data-stu-id="86803-249">In the **Styles** tab, locate and click the **<section> #login</section>** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="86803-250">请注意， **#login**样式会自动位于**Site.css**单击后。</span><span class="sxs-lookup"><span data-stu-id="86803-250">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="86803-251">此外，代码现在已突出显示。</span><span class="sxs-lookup"><span data-stu-id="86803-251">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="86803-252">![选择的 CSS 样式](using-page-inspector-in-visual-studio-2012/_static/image16.png "选择 CSS 样式")</span><span class="sxs-lookup"><span data-stu-id="86803-252">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image16.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="86803-253">*选择的 CSS 样式*</span><span class="sxs-lookup"><span data-stu-id="86803-253">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="86803-254">取消注释**文本对齐**属性中突出显示的代码通过删除开始和结束字符并保存**Site.css**文件。</span><span class="sxs-lookup"><span data-stu-id="86803-254">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="86803-255">Page Inspector 可以识别的所有不同文件构成当前页上，以及它可以检测这些文件的任何更改时。</span><span class="sxs-lookup"><span data-stu-id="86803-255">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="86803-256">它向你发出警报时在浏览器中的当前页面不是与源文件同步。</span><span class="sxs-lookup"><span data-stu-id="86803-256">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="86803-257">在 Page Inspector 浏览器中，单击位于地址栏以重新加载页面下方的栏。</span><span class="sxs-lookup"><span data-stu-id="86803-257">In the Page Inspector browser, click the bar located below the address bar to reload the page.</span></span>

    ![重新加载页面](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    <span data-ttu-id="86803-259">*重新加载页面*</span><span class="sxs-lookup"><span data-stu-id="86803-259">*Reloading the page*</span></span>

    <span data-ttu-id="86803-260">链接现在位于右侧，但它们看起来仍像项目符号列表。</span><span class="sxs-lookup"><span data-stu-id="86803-260">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="86803-261">现在，将删除的项目符号和水平对齐的链接。</span><span class="sxs-lookup"><span data-stu-id="86803-261">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![更新后的页面](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    <span data-ttu-id="86803-263">*更新后的页面*</span><span class="sxs-lookup"><span data-stu-id="86803-263">*Updated page*</span></span>
6. <span data-ttu-id="86803-264">使用检查模式下，选择任一**&lt;li&gt;** 包含的项&quot;注册&quot;并&quot;以用户身份登录&quot;链接。</span><span class="sxs-lookup"><span data-stu-id="86803-264">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="86803-265">然后，单击**&lt;部分&gt;#login**访问项**Styles.css**代码。</span><span class="sxs-lookup"><span data-stu-id="86803-265">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="86803-266">![查找样式](using-page-inspector-in-visual-studio-2012/_static/image19.png "查找样式")</span><span class="sxs-lookup"><span data-stu-id="86803-266">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image19.png "Finding the style")</span></span>

    <span data-ttu-id="86803-267">*查找样式*</span><span class="sxs-lookup"><span data-stu-id="86803-267">*Finding the style*</span></span>
7. <span data-ttu-id="86803-268">在中**Style.css**，取消注释的代码 **#login li**项。</span><span class="sxs-lookup"><span data-stu-id="86803-268">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="86803-269">要添加的样式将隐藏项目符号和水平显示的项目。</span><span class="sxs-lookup"><span data-stu-id="86803-269">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="86803-270">![重新设计的登录链接](using-page-inspector-in-visual-studio-2012/_static/image20.png "重新设计的登录链接")</span><span class="sxs-lookup"><span data-stu-id="86803-270">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image20.png "Restyling the login links")</span></span>

    <span data-ttu-id="86803-271">*重新设计的登录链接*</span><span class="sxs-lookup"><span data-stu-id="86803-271">*Restyling the login links*</span></span>
8. <span data-ttu-id="86803-272">保存**Style.css**文件，并在位于以下地址来重新加载页面的栏上单击一次。</span><span class="sxs-lookup"><span data-stu-id="86803-272">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="86803-273">请注意，链接正确显示。</span><span class="sxs-lookup"><span data-stu-id="86803-273">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="86803-274">![链接到的右侧对齐](using-page-inspector-in-visual-studio-2012/_static/image21.png "链接到的右侧对齐")</span><span class="sxs-lookup"><span data-stu-id="86803-274">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image21.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="86803-275">*链接到的右侧对齐*</span><span class="sxs-lookup"><span data-stu-id="86803-275">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="86803-276">最后，您将更改标头标题。</span><span class="sxs-lookup"><span data-stu-id="86803-276">Finally, you will change the header title.</span></span> <span data-ttu-id="86803-277">使用检查模式下单击**徽标此处**文本并生成它的源代码获取。</span><span class="sxs-lookup"><span data-stu-id="86803-277">Use the inspection mode to click **your logo here** text and get to the source code that generates it.</span></span>
10. <span data-ttu-id="86803-278">现在你已在 **\_Layout.cshtml**，将为**此处显示的徽标**文本**照片库**。</span><span class="sxs-lookup"><span data-stu-id="86803-278">Now you are in **\_Layout.cshtml**, replace '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="86803-279">保存并更新 Page Inspector 浏览器。</span><span class="sxs-lookup"><span data-stu-id="86803-279">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="86803-280">![分配新的标题](using-page-inspector-in-visual-studio-2012/_static/image22.png "分配新的标题")</span><span class="sxs-lookup"><span data-stu-id="86803-280">![Assigning a new title](using-page-inspector-in-visual-studio-2012/_static/image22.png "Assigning a new title")</span></span>

    <span data-ttu-id="86803-281">*分配新的标题*</span><span class="sxs-lookup"><span data-stu-id="86803-281">*Assigning a new title*</span></span>

    ![PhotoGallerypage](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    <span data-ttu-id="86803-283">*更新照片库页*</span><span class="sxs-lookup"><span data-stu-id="86803-283">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="86803-284">最后，选择**PhotoGallery**项目，然后按**F5**运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="86803-284">Finally, selet the **PhotoGallery** project and press **F5** to run the app.</span></span> <span data-ttu-id="86803-285">请查看所做的更改按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="86803-285">Check out all the changes work as expected.</span></span>

* * *

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a><span data-ttu-id="86803-286">练习 2： 在 WebForms 项目中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="86803-286">Exercise 2: Using Page Inspector in WebForms Projects</span></span>

<span data-ttu-id="86803-287">在此练习中，您将学习如何预览和调试使用 Page Inspector 的 WebForms 解决方案。</span><span class="sxs-lookup"><span data-stu-id="86803-287">In this exercise, you will learn how to preview and debug a WebForms solution using Page Inspector.</span></span> <span data-ttu-id="86803-288">首先会执行简要了解该工具来了解促进 Web 调试进程的 Page Inspector 功能。</span><span class="sxs-lookup"><span data-stu-id="86803-288">You will first perform a brief lap around the tool to learn the Page Inspector features that facilitate the Web debugging process.</span></span> <span data-ttu-id="86803-289">然后，您可以在包含样式设置问题的网页中。</span><span class="sxs-lookup"><span data-stu-id="86803-289">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="86803-290">您将学习如何使用 Page Inspector 找到生成问题的源代码和修复此错误。</span><span class="sxs-lookup"><span data-stu-id="86803-290">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="86803-291">任务 1-浏览页面检查器</span><span class="sxs-lookup"><span data-stu-id="86803-291">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="86803-292">在本任务中，您将学习如何在显示照片库 WebForms 项目的上下文中使用 Page Inspector 功能。</span><span class="sxs-lookup"><span data-stu-id="86803-292">In this task, you will learn how to use the Page Inspector features in the context of a WebForms project that shows a photo gallery.</span></span>

1. <span data-ttu-id="86803-293">打开**开始**解决方案位于**源/Ex2-WebForms/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="86803-293">Open the **Begin** solution located at **Source/Ex2-WebForms/Begin/** folder.</span></span>

   1. <span data-ttu-id="86803-294">需要先下载某些缺少的 NuGet 包然后再继续。</span><span class="sxs-lookup"><span data-stu-id="86803-294">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="86803-295">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="86803-295">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="86803-296">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="86803-296">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="86803-297">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="86803-297">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="86803-298">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="86803-298">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="86803-299">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="86803-299">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="86803-300">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="86803-300">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="86803-301">在解决方案资源管理器，找到**Default.aspx**页上，右键单击它并选择**在 Page Inspector 中的查看**。</span><span class="sxs-lookup"><span data-stu-id="86803-301">In the Solution Explorer, locate **Default.aspx** page, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="86803-302">![使用 Page Inspector 打开 Default.aspx](using-page-inspector-in-visual-studio-2012/_static/image24.png "打开 Default.aspx 使用 Page Inspector")</span><span class="sxs-lookup"><span data-stu-id="86803-302">![Opening Default.aspx with Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image24.png "Opening Default.aspx with Page Inspector")</span></span>

    <span data-ttu-id="86803-303">*打开 Default.aspx 使用 Page Inspector*</span><span class="sxs-lookup"><span data-stu-id="86803-303">*Opening Default.aspx with Page Inspector*</span></span>
3. <span data-ttu-id="86803-304">Page Inspector 窗口将显示 Default.aspx。</span><span class="sxs-lookup"><span data-stu-id="86803-304">The Page Inspector window will show Default.aspx.</span></span>

    <span data-ttu-id="86803-305">![在 Page Inspector 中查看 Default.aspx](using-page-inspector-in-visual-studio-2012/_static/image25.png "在 Page Inspector 中查看 Default.aspx")</span><span class="sxs-lookup"><span data-stu-id="86803-305">![Viewing Default.aspx in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image25.png "Viewing Default.aspx in Page Inspector")</span></span>

    <span data-ttu-id="86803-306">*在 Page Inspector 中查看 Default.aspx*</span><span class="sxs-lookup"><span data-stu-id="86803-306">*Viewing Default.aspx in Page Inspector*</span></span>

    <span data-ttu-id="86803-307">Page Inspector 工具已集成在 Visual Studio 环境中。</span><span class="sxs-lookup"><span data-stu-id="86803-307">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="86803-308">该检查器包含嵌入式浏览器，以及功能强大的 HTML 探查器将显示所选的代码。</span><span class="sxs-lookup"><span data-stu-id="86803-308">The inspector contains an embedded browser, together with a powerful HTML profiler that will show the selected code.</span></span> <span data-ttu-id="86803-309">请注意，不需要运行解决方案，以查看您的页面的外观。</span><span class="sxs-lookup"><span data-stu-id="86803-309">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86803-310">当 Page Inspector 浏览器宽度小于所打开的页的宽度时，您不会正确地看到页面。</span><span class="sxs-lookup"><span data-stu-id="86803-310">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="86803-311">如果发生这种情况，调整页面检查器的宽度。</span><span class="sxs-lookup"><span data-stu-id="86803-311">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="86803-312">单击**文件**在 Page Inspector 中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="86803-312">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="86803-313">您将看到正在撰写呈现的默认页面的所有源文件。</span><span class="sxs-lookup"><span data-stu-id="86803-313">You will see all the source files that are composing the rendered Default page.</span></span> <span data-ttu-id="86803-314">这是一个有用的功能，尤其在使用用户控件和母版页时标识一眼的所有元素。</span><span class="sxs-lookup"><span data-stu-id="86803-314">This is a useful feature to identify all the elements at a glance, especially when you are working with User Controls and Master Pages.</span></span> <span data-ttu-id="86803-315">请注意，还可以导航到每个文件。</span><span class="sxs-lookup"><span data-stu-id="86803-315">Notice that you can also navigate to each of the files.</span></span>

    <span data-ttu-id="86803-316">![文件选项卡](using-page-inspector-in-visual-studio-2012/_static/image26.png "文件选项卡")</span><span class="sxs-lookup"><span data-stu-id="86803-316">![The Files tab](using-page-inspector-in-visual-studio-2012/_static/image26.png "The Files tab")</span></span>

    <span data-ttu-id="86803-317">*文件选项卡*</span><span class="sxs-lookup"><span data-stu-id="86803-317">*The Files tab*</span></span>
5. <span data-ttu-id="86803-318">单击**切换检查模式下**按钮，位于左侧的选项卡。</span><span class="sxs-lookup"><span data-stu-id="86803-318">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="86803-319">此工具会让您选择的页的任何元素，并查看其 HTML 代码和.aspx 源。</span><span class="sxs-lookup"><span data-stu-id="86803-319">This tool will let you select any element of the page and see its HTML code and .aspx source.</span></span>

    <span data-ttu-id="86803-320">![切换检查模式按钮](using-page-inspector-in-visual-studio-2012/_static/image27.png "切换检查模式按钮")</span><span class="sxs-lookup"><span data-stu-id="86803-320">![Toggle Inspection Mode button](using-page-inspector-in-visual-studio-2012/_static/image27.png "Toggle Inspection Mode button")</span></span>

    <span data-ttu-id="86803-321">*切换检查模式按钮*</span><span class="sxs-lookup"><span data-stu-id="86803-321">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="86803-322">在 Page Inspector 浏览器中，将鼠标移动页面元素。</span><span class="sxs-lookup"><span data-stu-id="86803-322">In the Page Inspector browser, move the mouse over the page elements.</span></span> <span data-ttu-id="86803-323">将鼠标指针移过所呈现页中的任何部分，而显示的元素类型和 Visual Studio 编辑器中突出显示相应的源标记或代码。</span><span class="sxs-lookup"><span data-stu-id="86803-323">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    <span data-ttu-id="86803-324">![在操作中的检查模式下](using-page-inspector-in-visual-studio-2012/_static/image28.png "操作在检查模式")</span><span class="sxs-lookup"><span data-stu-id="86803-324">![Inspection mode in action](using-page-inspector-in-visual-studio-2012/_static/image28.png "Inspection mode in action")</span></span>

    <span data-ttu-id="86803-325">*在操作中检查模式*</span><span class="sxs-lookup"><span data-stu-id="86803-325">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="86803-326">不最大化页面检查器窗口或你将无法再看到显示的源代码的预览选项卡。</span><span class="sxs-lookup"><span data-stu-id="86803-326">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="86803-327">如果它最大化时单击 Page Inspector 中的元素，将显示所选内容的源代码，但它会隐藏页面检查器窗口。</span><span class="sxs-lookup"><span data-stu-id="86803-327">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="86803-328">如果您注意到**Default.aspx**文件中，你会注意到，突出显示的源代码的生成所选的元素的部分。</span><span class="sxs-lookup"><span data-stu-id="86803-328">If you pay attention to **Default.aspx** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="86803-329">此功能便于长的源文件，提供指导支持和快速的方法来访问代码的版本。</span><span class="sxs-lookup"><span data-stu-id="86803-329">This feature facilitates the edition of long source files, providing a direct and fast way to access the code.</span></span>

    <span data-ttu-id="86803-330">![检查元素](using-page-inspector-in-visual-studio-2012/_static/image29.png "检查元素")</span><span class="sxs-lookup"><span data-stu-id="86803-330">![Inspecting elements](using-page-inspector-in-visual-studio-2012/_static/image29.png "Inspecting elements")</span></span>

    <span data-ttu-id="86803-331">*检查元素*</span><span class="sxs-lookup"><span data-stu-id="86803-331">*Inspecting elements*</span></span>
7. <span data-ttu-id="86803-332">单击**切换检查模式下**按钮 (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser。](using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser。")</span><span class="sxs-lookup"><span data-stu-id="86803-332">Click the **Toggle Inspection Mode** button (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.](using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.")</span></span> <span data-ttu-id="86803-333">) 中的 Page Inspector 选项卡，若要禁用光标。</span><span class="sxs-lookup"><span data-stu-id="86803-333">), located in Page Inspector tabs, to disable the cursor.</span></span>
8. <span data-ttu-id="86803-334">选择**HTML**选项卡以显示在 Page Inspector 浏览器中呈现的 HTML 代码。</span><span class="sxs-lookup"><span data-stu-id="86803-334">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="86803-335">在 HTML 代码中，找到与 Koala 链接的列表项并选择它。</span><span class="sxs-lookup"><span data-stu-id="86803-335">In the HTML code, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="86803-336">请注意，当您选择的代码，相应的输出是自动突出显示浏览器。</span><span class="sxs-lookup"><span data-stu-id="86803-336">Notice that when you select the code, the corresponding output is automatically highlighted browser.</span></span> <span data-ttu-id="86803-337">此功能可用于查看 HTML 块的页上的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="86803-337">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="86803-338">![在页中选择 HTML 元素](using-page-inspector-in-visual-studio-2012/_static/image31.png "的页中选择 HTML 元素")</span><span class="sxs-lookup"><span data-stu-id="86803-338">![Selecting an HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image31.png "Selecting an HTML element in the page")</span></span>

    <span data-ttu-id="86803-339">*在页中选择 HTML 元素*</span><span class="sxs-lookup"><span data-stu-id="86803-339">*Selecting an HTML element in the page*</span></span>
10. <span data-ttu-id="86803-340">单击**切换检查模式下**按钮以启用*检查模式下*单击导航栏。</span><span class="sxs-lookup"><span data-stu-id="86803-340">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="86803-341">右侧的 HTML 代码，在样式窗格中，将看到列表，与应用于所选元素的 CSS 样式。</span><span class="sxs-lookup"><span data-stu-id="86803-341">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86803-342">因为标头是站点布局的一部分，Page Inspector 还将打开 Site.Master 文件并突出显示的受影响的代码段。</span><span class="sxs-lookup"><span data-stu-id="86803-342">since the header is a part of the site layout, Page Inspector will also open Site.Master file and highlight the segment of code affected.</span></span>

    <span data-ttu-id="86803-343">![DiscoveringstylesWebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "发现样式和所选元素的源文件")</span><span class="sxs-lookup"><span data-stu-id="86803-343">![DiscoveringstylesWebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "Discovering styles and source files of a selected element")</span></span>

    <span data-ttu-id="86803-344">*发现所选元素的样式和源文件*</span><span class="sxs-lookup"><span data-stu-id="86803-344">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="86803-345">启用切换检查指针，将鼠标指针菜单栏下方移动，再单击空白一半的圆圈。</span><span class="sxs-lookup"><span data-stu-id="86803-345">With the toggle inspection pointer enabled, move the mouse pointer below the menu bar and click the blank half circle.</span></span>

    <span data-ttu-id="86803-346">![选择元素](using-page-inspector-in-visual-studio-2012/_static/image33.png "选择元素")</span><span class="sxs-lookup"><span data-stu-id="86803-346">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image33.png "Selecting an element")</span></span>

    <span data-ttu-id="86803-347">*选择元素*</span><span class="sxs-lookup"><span data-stu-id="86803-347">*Selecting an element*</span></span>
12. <span data-ttu-id="86803-348">在样式窗格中，找到**背景图像**项下 **.main 内容**组。</span><span class="sxs-lookup"><span data-stu-id="86803-348">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="86803-349">**取消选中****背景图像**，看看效果。</span><span class="sxs-lookup"><span data-stu-id="86803-349">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="86803-350">您将注意到浏览器将立即反映所做的更改，并且该圆形处于隐藏状态。</span><span class="sxs-lookup"><span data-stu-id="86803-350">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86803-351">在页面检查器样式的选项卡上应用的更改不会影响原始样式表。</span><span class="sxs-lookup"><span data-stu-id="86803-351">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="86803-352">您可以取消选中样式或更改无数次，但它们会在还原刷新页面后，其值。</span><span class="sxs-lookup"><span data-stu-id="86803-352">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="86803-353">![启用和禁用 CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "启用和禁用 CSS 样式")</span><span class="sxs-lookup"><span data-stu-id="86803-353">![Enabling and disabling CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="86803-354">*启用和禁用 CSS 样式*</span><span class="sxs-lookup"><span data-stu-id="86803-354">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="86803-355">现在，单击**你****此处显示的徽标**上使用检查模式下的标头的文本。</span><span class="sxs-lookup"><span data-stu-id="86803-355">Now, click the '**your** **logo here'** text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="86803-356">在中**样式**选项卡上，找到**字体大小**CSS 属性下 **.site 标题**组。</span><span class="sxs-lookup"><span data-stu-id="86803-356">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="86803-357">双击该属性一次以编辑其值。</span><span class="sxs-lookup"><span data-stu-id="86803-357">Double-click the attribute once to edit its value.</span></span> <span data-ttu-id="86803-358">值替换为 2.3em **3em**，然后按 ENTER。</span><span class="sxs-lookup"><span data-stu-id="86803-358">Replace the 2.3em value with **3em**, and then press ENTER.</span></span> <span data-ttu-id="86803-359">请注意，标题看上去更大。</span><span class="sxs-lookup"><span data-stu-id="86803-359">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="86803-360">![更改页面 Inspector2 中的 CSS 值](using-page-inspector-in-visual-studio-2012/_static/image35.png "在 Page Inspector 中的更改的 CSS 值")</span><span class="sxs-lookup"><span data-stu-id="86803-360">![Changing CSS values in the Page Inspector2](using-page-inspector-in-visual-studio-2012/_static/image35.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="86803-361">*更改在 Page Inspector 中的 CSS 值*</span><span class="sxs-lookup"><span data-stu-id="86803-361">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="86803-362">单击**跟踪样式**选项卡上，Page Inspector 的右窗格中。</span><span class="sxs-lookup"><span data-stu-id="86803-362">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="86803-363">这是一种方法来查看应用于所选内容，按属性名称排序的所有样式。</span><span class="sxs-lookup"><span data-stu-id="86803-363">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    <span data-ttu-id="86803-364">![所选元素的 CSS 样式跟踪](using-page-inspector-in-visual-studio-2012/_static/image36.png "所选元素的 CSS 样式跟踪")</span><span class="sxs-lookup"><span data-stu-id="86803-364">![CSS styles tracing of the selected element](using-page-inspector-in-visual-studio-2012/_static/image36.png "CSS styles tracing of the selected element")</span></span>

    <span data-ttu-id="86803-365">*所选元素的 CSS 样式跟踪*</span><span class="sxs-lookup"><span data-stu-id="86803-365">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="86803-366">Page Inspector 的另一个功能是布局窗格。</span><span class="sxs-lookup"><span data-stu-id="86803-366">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="86803-367">使用检查模式下，选择导航栏，然后单击**布局**右窗格上的选项卡。</span><span class="sxs-lookup"><span data-stu-id="86803-367">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="86803-368">你将看到所选元素的确切大小以及其偏移量、 边距、 填充和边框的大小。</span><span class="sxs-lookup"><span data-stu-id="86803-368">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="86803-369">请注意，您还可以修改此视图中的值。</span><span class="sxs-lookup"><span data-stu-id="86803-369">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="86803-370">![在 Page Inspector 中的元素布局](using-page-inspector-in-visual-studio-2012/_static/image37.png "在 Page Inspector 中的元素布局")</span><span class="sxs-lookup"><span data-stu-id="86803-370">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image37.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="86803-371">*在 Page Inspector 中的元素布局*</span><span class="sxs-lookup"><span data-stu-id="86803-371">*Element layout in Page Inspector*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="86803-372">任务 2-查找并修复在照片库中的样式问题</span><span class="sxs-lookup"><span data-stu-id="86803-372">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="86803-373">如何诊断与以前版本的 Visual Studio 的网页问题？</span><span class="sxs-lookup"><span data-stu-id="86803-373">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="86803-374">您将可能非常熟悉 web 调试工具，Visual Studio IDE，如 Internet Explorer 开发人员工具或 Firebug 之外运行。</span><span class="sxs-lookup"><span data-stu-id="86803-374">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="86803-375">浏览器只了解 HTML、 脚本和样式，而基础框架生成将呈现的 HTML。</span><span class="sxs-lookup"><span data-stu-id="86803-375">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="86803-376">为此，通常需要部署的整个站点，以查看网页的显示效果。</span><span class="sxs-lookup"><span data-stu-id="86803-376">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="86803-377">当你想要检测和修复问题，在您的网站时，可能必须遵循以下步骤：</span><span class="sxs-lookup"><span data-stu-id="86803-377">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="86803-378">从 Visual Studio 中，运行该解决方案或部署 web 服务器上的页。</span><span class="sxs-lookup"><span data-stu-id="86803-378">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="86803-379">在浏览器中打开开发人员工具使用，或只需打开源代码和样式并会尝试匹配该问题。</span><span class="sxs-lookup"><span data-stu-id="86803-379">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="86803-380">若要查找所涉及的文件，你会使用&quot;搜索&quot;或&quot;文件中的搜索&quot;样式类同名的功能。</span><span class="sxs-lookup"><span data-stu-id="86803-380">To find the files involved, you'd have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="86803-381">一旦检测到错误，停止 Web 浏览器和服务器。</span><span class="sxs-lookup"><span data-stu-id="86803-381">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="86803-382">清除浏览器缓存。</span><span class="sxs-lookup"><span data-stu-id="86803-382">Clear the browser cache.</span></span>
5. <span data-ttu-id="86803-383">返回到 Visual Studio 来应用修补程序。</span><span class="sxs-lookup"><span data-stu-id="86803-383">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="86803-384">重复测试的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="86803-384">Repeat all the steps to test.</span></span>

<span data-ttu-id="86803-385">因为没有不真正所见即所得 ASP.NET WebForms 中，某些样式问题上检测到后面的阶段，在运行或部署后。</span><span class="sxs-lookup"><span data-stu-id="86803-385">As there is no real WYSIWYG in ASP.NET WebForms, some style issues are detected on a later stage, after running or deploying.</span></span> <span data-ttu-id="86803-386">现在，使用 Page Inspector，可以预览任何页，而无需运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="86803-386">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="86803-387">在此任务中，将使用 Page inspector，修复照片库应用程序的一些问题。</span><span class="sxs-lookup"><span data-stu-id="86803-387">In this task, you will use the Page inspector for fixing some issues of the Photo Gallery application.</span></span> <span data-ttu-id="86803-388">在以下步骤中，将检测并快速修复标头中的一些简单样式问题。</span><span class="sxs-lookup"><span data-stu-id="86803-388">In the following steps, you will detect and quickly fix some simple styling issue in the header.</span></span>

1. <span data-ttu-id="86803-389">使用页检查，找到**注册**并**Log In**处的标头的左侧链接。</span><span class="sxs-lookup"><span data-stu-id="86803-389">Using Page Inspection, locate the **Register** and the **Log In** links at the left side of the header.</span></span>

    <span data-ttu-id="86803-390">请注意，该链接不显示在右侧的预期位置。</span><span class="sxs-lookup"><span data-stu-id="86803-390">Notice that the link is not displayed at the expected place on the right.</span></span> <span data-ttu-id="86803-391">现在将对齐到右侧的链接，并可以相应地重新应用。</span><span class="sxs-lookup"><span data-stu-id="86803-391">You will now align the link to the right and restyle it accordingly.</span></span>

    <span data-ttu-id="86803-392">![登录链接位于左侧](using-page-inspector-in-visual-studio-2012/_static/image38.png "定位在左侧的链接以用户身份登录")</span><span class="sxs-lookup"><span data-stu-id="86803-392">![Log in link positioned on the left](using-page-inspector-in-visual-studio-2012/_static/image38.png "Log in link positioned on the left")</span></span>

    <span data-ttu-id="86803-393">*在左侧定位的登录链接*</span><span class="sxs-lookup"><span data-stu-id="86803-393">*Log In link positioned on the left*</span></span>
2. <span data-ttu-id="86803-394">使用所选的切换检查模式下，选择日志中的链接以打开其代码。</span><span class="sxs-lookup"><span data-stu-id="86803-394">With Toggle Inspection Mode selected, select the Log In link to open its code.</span></span>

    <span data-ttu-id="86803-395">请注意，链接源代码位于**Site.Master**文件中，未在 Default.aspx 页，这是一个您可能会看到在第一个位置; 你具有已直接放在正确的源文件。</span><span class="sxs-lookup"><span data-stu-id="86803-395">Notice that the link source code is located in the **Site.Master** file, not in the Default.aspx page which is the place you might look in first place; you have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="86803-396">在中**样式**选项卡上，找到并单击**&lt;部分&gt;#login**项，它是下面的链接的 HTML 容器。</span><span class="sxs-lookup"><span data-stu-id="86803-396">In the **Styles** tab, locate and click the **&lt;section&gt; #login** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="86803-397">请注意， **#login**样式会自动位于**Site.css**单击后。</span><span class="sxs-lookup"><span data-stu-id="86803-397">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="86803-398">此外，代码现在已突出显示。</span><span class="sxs-lookup"><span data-stu-id="86803-398">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="86803-399">![选择的 CSS 样式](using-page-inspector-in-visual-studio-2012/_static/image39.png "选择 CSS 样式")</span><span class="sxs-lookup"><span data-stu-id="86803-399">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image39.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="86803-400">*选择的 CSS 样式*</span><span class="sxs-lookup"><span data-stu-id="86803-400">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="86803-401">取消注释**文本对齐**属性中突出显示的代码通过删除开始和结束字符并保存**Site.css**文件。</span><span class="sxs-lookup"><span data-stu-id="86803-401">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="86803-402">Page Inspector 可以识别的所有不同文件构成当前页上，以及它可以检测这些文件的任何更改时。</span><span class="sxs-lookup"><span data-stu-id="86803-402">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="86803-403">它向你发出警报时在浏览器中的当前页面不是与源文件同步。</span><span class="sxs-lookup"><span data-stu-id="86803-403">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="86803-404">在 Page Inspector 浏览器中，单击位于地址栏以保存所做的更改并重新加载页面下方的栏。</span><span class="sxs-lookup"><span data-stu-id="86803-404">In the Page Inspector browser, click the bar located below the address bar to save the changes and reload the page.</span></span>

    ![Reloadingthepage](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    <span data-ttu-id="86803-406">*重新加载页面*</span><span class="sxs-lookup"><span data-stu-id="86803-406">*Reloading the page*</span></span>

    <span data-ttu-id="86803-407">链接现在位于右侧，但它们看起来仍像项目符号列表。</span><span class="sxs-lookup"><span data-stu-id="86803-407">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="86803-408">现在，将删除的项目符号和水平对齐的链接。</span><span class="sxs-lookup"><span data-stu-id="86803-408">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![更新后的页面](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    <span data-ttu-id="86803-410">*更新后的页面*</span><span class="sxs-lookup"><span data-stu-id="86803-410">*Updated page*</span></span>
6. <span data-ttu-id="86803-411">使用检查模式下，选择任一**&lt;li&gt;** 包含的项&quot;注册&quot;并&quot;以用户身份登录&quot;链接。</span><span class="sxs-lookup"><span data-stu-id="86803-411">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="86803-412">然后，单击**&lt;部分&gt;#login**访问项**Styles.css**代码。</span><span class="sxs-lookup"><span data-stu-id="86803-412">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="86803-413">![查找样式](using-page-inspector-in-visual-studio-2012/_static/image42.png "查找样式")</span><span class="sxs-lookup"><span data-stu-id="86803-413">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image42.png "Finding the style")</span></span>

    <span data-ttu-id="86803-414">*查找样式*</span><span class="sxs-lookup"><span data-stu-id="86803-414">*Finding the style*</span></span>
7. <span data-ttu-id="86803-415">在中**Style.css**，取消注释的代码 **#login li**项。</span><span class="sxs-lookup"><span data-stu-id="86803-415">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="86803-416">要添加的样式将隐藏项目符号和水平显示的项目。</span><span class="sxs-lookup"><span data-stu-id="86803-416">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="86803-417">![重新设计的登录链接](using-page-inspector-in-visual-studio-2012/_static/image43.png "重新设计的登录链接")</span><span class="sxs-lookup"><span data-stu-id="86803-417">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image43.png "Restyling the login links")</span></span>

    <span data-ttu-id="86803-418">*重新设计的登录链接*</span><span class="sxs-lookup"><span data-stu-id="86803-418">*Restyling the login links*</span></span>
8. <span data-ttu-id="86803-419">保存**Style.css**文件，并在位于以下地址来重新加载页面的栏上单击一次。</span><span class="sxs-lookup"><span data-stu-id="86803-419">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="86803-420">请注意，链接正确显示。</span><span class="sxs-lookup"><span data-stu-id="86803-420">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="86803-421">![链接到的右侧对齐](using-page-inspector-in-visual-studio-2012/_static/image44.png "链接到的右侧对齐")</span><span class="sxs-lookup"><span data-stu-id="86803-421">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image44.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="86803-422">*链接到的右侧对齐*</span><span class="sxs-lookup"><span data-stu-id="86803-422">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="86803-423">最后，您将更改标头标题。</span><span class="sxs-lookup"><span data-stu-id="86803-423">Finally, you will change the header title.</span></span> <span data-ttu-id="86803-424">而不是搜索**此处显示的徽标**文本中所有文件，使用检查模式下单击文本并生成它的源代码。</span><span class="sxs-lookup"><span data-stu-id="86803-424">Instead of searching for the '**your logo here'** text in all the files, use the inspection mode to click the text and get to source code that generates it.</span></span>

    <span data-ttu-id="86803-425">![查找站点标题](using-page-inspector-in-visual-studio-2012/_static/image45.png "查找网站标题")</span><span class="sxs-lookup"><span data-stu-id="86803-425">![Finding the site title](using-page-inspector-in-visual-studio-2012/_static/image45.png "Finding the site title")</span></span>

    <span data-ttu-id="86803-426">*查找网站标题*</span><span class="sxs-lookup"><span data-stu-id="86803-426">*Finding the site title*</span></span>
10. <span data-ttu-id="86803-427">现在你已在**Site.Master**，将为**此处显示的徽标**文本**照片库**。</span><span class="sxs-lookup"><span data-stu-id="86803-427">Now you are in **Site.Master**, replace the '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="86803-428">保存并更新 Page Inspector 浏览器。</span><span class="sxs-lookup"><span data-stu-id="86803-428">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="86803-429">![照片库页更新](using-page-inspector-in-visual-studio-2012/_static/image46.png "更新照片库页")</span><span class="sxs-lookup"><span data-stu-id="86803-429">![Photo Gallery page updated](using-page-inspector-in-visual-studio-2012/_static/image46.png "Photo Gallery page updated")</span></span>

    <span data-ttu-id="86803-430">*更新照片库页*</span><span class="sxs-lookup"><span data-stu-id="86803-430">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="86803-431">最后，按**F5**运行应用的签出所有所做的更改按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="86803-431">Finally press **F5** to run the app the check out all the changes work as expected.</span></span>

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="86803-432">总结</span><span class="sxs-lookup"><span data-stu-id="86803-432">Summary</span></span>

<span data-ttu-id="86803-433">通过完成本动手实验，你已了解到如何使用 Page Inspector 无需重新生成并运行网站的浏览器中预览 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="86803-433">By completing this Hands-On Lab, you have learnt how to use Page Inspector to preview your Web application without having to rebuild and run the Web site in a browser.</span></span> <span data-ttu-id="86803-434">此外，你已了解到如何快速查找并修复 bug，通过直接从呈现的输出访问源代码。</span><span class="sxs-lookup"><span data-stu-id="86803-434">In addition, you have learnt how to quickly find and fix bugs by accessing directly from the rendered output to the source code.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="86803-435">附录 a： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="86803-435">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="86803-436">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="86803-436">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="86803-437">以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="86803-437">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="86803-438">转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="86803-438">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="86803-439">或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="86803-439">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="86803-440">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="86803-440">Click on **Install Now**.</span></span> <span data-ttu-id="86803-441">如果还没有**Web 平台安装程序**将重定向以下载并安装。</span><span class="sxs-lookup"><span data-stu-id="86803-441">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="86803-442">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="86803-442">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="86803-443">![安装 Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="86803-443">![Install Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="86803-444">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="86803-444">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="86803-445">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="86803-445">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    <span data-ttu-id="86803-447">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="86803-447">*Accepting the license terms*</span></span>
5. <span data-ttu-id="86803-448">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="86803-448">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    <span data-ttu-id="86803-450">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="86803-450">*Installation progress*</span></span>
6. <span data-ttu-id="86803-451">安装完成后，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="86803-451">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    <span data-ttu-id="86803-453">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="86803-453">*Installation completed*</span></span>
7. <span data-ttu-id="86803-454">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="86803-454">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="86803-455">若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="86803-455">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    <span data-ttu-id="86803-457">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="86803-457">*VS Express for Web tile*</span></span>
