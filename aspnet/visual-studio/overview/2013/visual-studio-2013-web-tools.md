---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 动手实验： Visual Studio 2013 Web 工具 |Microsoft Docs
author: rick-anderson
description: Visual Studio 是一个极好开发环境。基于 NET 的 Windows 和 web 项目。 它包括一个强大的文本编辑器，可轻松用于...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
ms.technology: ''
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 8f0f19a184d50cdc6e8e5a2da0e55a0e8ca44dc5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399395"
---
<a name="hands-on-lab-visual-studio-2013-web-tools"></a><span data-ttu-id="3358e-104">动手实验： Visual Studio 2013 Web 工具</span><span class="sxs-lookup"><span data-stu-id="3358e-104">Hands On Lab: Visual Studio 2013 Web Tools</span></span>
====================
<span data-ttu-id="3358e-105">通过[Web 训练营团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="3358e-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="3358e-106">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="3358e-106">Download Web Camps Training Kit</span></span>](http://aka.ms/webcamps-training-kit)

> <span data-ttu-id="3358e-107">Visual Studio 是一个极好开发环境。基于 NET 的 Windows 和 web 项目。</span><span class="sxs-lookup"><span data-stu-id="3358e-107">Visual Studio is an excellent development environment for .NET-based Windows and web projects.</span></span> <span data-ttu-id="3358e-108">它包括一个强大的文本编辑器，可以轻松地用来编辑不含项目的独立文件。</span><span class="sxs-lookup"><span data-stu-id="3358e-108">It includes a powerful text editor that can easily be used to edit standalone files without a project.</span></span>
> 
> <span data-ttu-id="3358e-109">在编辑每个文件时，visual Studio 维护全面分析树。</span><span class="sxs-lookup"><span data-stu-id="3358e-109">Visual Studio maintains a full-featured parse tree as you edit each file.</span></span> <span data-ttu-id="3358e-110">这样，Visual Studio 以进行更快、 更舒适的开发体验的同时提供无与伦比的自动完成功能和基于文档的操作。</span><span class="sxs-lookup"><span data-stu-id="3358e-110">This allows Visual Studio to provide unparalleled auto-completion and document-based actions while making the development experience much faster and more pleasant.</span></span> <span data-ttu-id="3358e-111">这些功能会特别大 HTML 和 CSS 文档中。</span><span class="sxs-lookup"><span data-stu-id="3358e-111">These features are especially powerful in HTML and CSS documents.</span></span>
> 
> <span data-ttu-id="3358e-112">所有这种能力也是可用于扩展，使其易于扩展，具有强大的新功能以满足你需求的编辑器。</span><span class="sxs-lookup"><span data-stu-id="3358e-112">All of this power is also available for extensions, making it simple to extend the editors with powerful new features to suit your needs.</span></span> <span data-ttu-id="3358e-113">Web Essentials 是一系列 （主要） 与 web 相关增强功能 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3358e-113">Web Essentials is a collection of (mostly) web-related enhancements to Visual Studio.</span></span> <span data-ttu-id="3358e-114">它还包括了许多新的 IntelliSense 完成 （尤其是对于 CSS)、 新的浏览器链接功能、 自动 JSHint 的 JavaScript 文件、 HTML 和 CSS 和对新式 web 开发至关重要的许多其他功能的新的警告。</span><span class="sxs-lookup"><span data-stu-id="3358e-114">It includes lots of new IntelliSense completions (especially for CSS), new Browser Link features, automatic JSHint for JavaScript files, new warnings for HTML and CSS, and many other features that are essential to modern web development.</span></span>
> 
> <span data-ttu-id="3358e-115">在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)。</span><span class="sxs-lookup"><span data-stu-id="3358e-115">All sample code and snippets are included in the Web Camps Training Kit, available at [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).</span></span>


<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="3358e-116">概述</span><span class="sxs-lookup"><span data-stu-id="3358e-116">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="3358e-117">目标</span><span class="sxs-lookup"><span data-stu-id="3358e-117">Objectives</span></span>

<span data-ttu-id="3358e-118">在本动手实验，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="3358e-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="3358e-119">使用新的 HTML 编辑器功能，这些功能包含在 Web Essentials 等丰富的 HTML5 代码代码段和处理编码</span><span class="sxs-lookup"><span data-stu-id="3358e-119">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="3358e-120">使用颜色选取器和浏览器矩阵工具提示等 Web Essentials 中包括的新 CSS 编辑器功能</span><span class="sxs-lookup"><span data-stu-id="3358e-120">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="3358e-121">使用 Web Essentials 等中提取到文件和智能感知中包括的所有 HTML 元素的新 JavaScript 编辑器功能</span><span class="sxs-lookup"><span data-stu-id="3358e-121">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="3358e-122">你的浏览器和 Visual Studio 中使用浏览器链接之间交换数据</span><span class="sxs-lookup"><span data-stu-id="3358e-122">Exchange data between your browser and Visual Studio using Browser Link</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="3358e-123">系统必备</span><span class="sxs-lookup"><span data-stu-id="3358e-123">Prerequisites</span></span>

<span data-ttu-id="3358e-124">完成本动手实验需要以下：</span><span class="sxs-lookup"><span data-stu-id="3358e-124">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="3358e-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/)或更高版本</span><span class="sxs-lookup"><span data-stu-id="3358e-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="3358e-126">Web Essentials 2013</span><span class="sxs-lookup"><span data-stu-id="3358e-126">Web Essentials 2013</span></span>](http://vswebessentials.com/)
- [<span data-ttu-id="3358e-127">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="3358e-127">Google Chrome</span></span>](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="3358e-128">安装</span><span class="sxs-lookup"><span data-stu-id="3358e-128">Setup</span></span>

<span data-ttu-id="3358e-129">若要运行本动手实验中练习，需要先设置你的环境。</span><span class="sxs-lookup"><span data-stu-id="3358e-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="3358e-130">打开 Windows 资源管理器窗口并浏览到本实验**源**文件夹。</span><span class="sxs-lookup"><span data-stu-id="3358e-130">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="3358e-131">右键单击**Setup.cmd** ，然后选择**以管理员身份运行**以启动将配置你的环境并安装本实验的 Visual Studio 代码段的安装过程。</span><span class="sxs-lookup"><span data-stu-id="3358e-131">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="3358e-132">如果显示用户帐户控制对话框中，确认要继续执行的操作。</span><span class="sxs-lookup"><span data-stu-id="3358e-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="3358e-133">请确保您运行安装程序之前已为此实验室的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="3358e-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="3358e-134">使用代码片段</span><span class="sxs-lookup"><span data-stu-id="3358e-134">Using the Code Snippets</span></span>

<span data-ttu-id="3358e-135">在整个实验文档中，将指示您插入代码块。</span><span class="sxs-lookup"><span data-stu-id="3358e-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="3358e-136">为方便起见，此代码的大部分以 Visual Studio 代码段，可以在 Visual Studio 2013，为了避免必须手动添加访问从形式提供。</span><span class="sxs-lookup"><span data-stu-id="3358e-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="3358e-137">每个练习均附带位于中的开始解决方案**开始**本练习，您可以按照独立于其他每个练习的文件夹。</span><span class="sxs-lookup"><span data-stu-id="3358e-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="3358e-138">请注意在练习期间添加的代码片段缺少这些开始解决方案中，并且可能无法工作，直到完成该练习。</span><span class="sxs-lookup"><span data-stu-id="3358e-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="3358e-139">在练习的源代码，您将发现**最终**包含具有无法完成相应练习中的步骤得到的代码的 Visual Studio 解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="3358e-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="3358e-140">如果您在演练本动手实验需要更多帮助，可以使用这些解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="3358e-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


* * *

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="3358e-141">练习</span><span class="sxs-lookup"><span data-stu-id="3358e-141">Exercises</span></span>

<span data-ttu-id="3358e-142">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="3358e-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="3358e-143">使用浏览器链接和 Web Essentials</span><span class="sxs-lookup"><span data-stu-id="3358e-143">Working with Browser Link and Web Essentials</span></span>](#Exercise1)
2. [<span data-ttu-id="3358e-144">利用代码段和 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="3358e-144">Taking Advantage of Code Snippets and IntelliSense</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="3358e-145">在首次启动 Visual Studio，您必须选择一个预定义的设置集合。</span><span class="sxs-lookup"><span data-stu-id="3358e-145">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="3358e-146">每个预定义的集合旨在符合特定的开发风格，并确定窗口布局、 编辑器行为、 IntelliSense 代码段和对话框选项。</span><span class="sxs-lookup"><span data-stu-id="3358e-146">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="3358e-147">此实验中的过程描述了完成给定的任务在 Visual Studio 中使用时所需的操作**常规开发设置**集合。</span><span class="sxs-lookup"><span data-stu-id="3358e-147">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="3358e-148">如果您为您的开发环境选择不同的设置集合，可能会中应考虑到的步骤有所不同。</span><span class="sxs-lookup"><span data-stu-id="3358e-148">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a><span data-ttu-id="3358e-149">练习 1： 使用浏览器链接和 Web Essentials</span><span class="sxs-lookup"><span data-stu-id="3358e-149">Exercise 1: Working with Browser Link and Web Essentials</span></span>

<span data-ttu-id="3358e-150">**Web Essentials**是一个 Visual Studio 扩展，将添加各种新式 web 开发，主要侧重于使 web 开发体验更快、 更舒适的有用功能。</span><span class="sxs-lookup"><span data-stu-id="3358e-150">**Web Essentials** is a Visual Studio extension that adds a variety of useful features for modern web development, mostly focused on making the web development experience much faster and more pleasant.</span></span> <span data-ttu-id="3358e-151">可以从 Visual Studio 中的扩展库安装 Web Essentials。</span><span class="sxs-lookup"><span data-stu-id="3358e-151">You can install Web Essentials from the Extension Gallery in Visual Studio.</span></span>

<span data-ttu-id="3358e-152">**浏览器链接**是提供你的 web 应用程序和 Visual Studio 之间交换数据的 Visual Studio IDE 和任何打开的浏览器之间通道的 Visual Studio 2013 中包含的新功能。</span><span class="sxs-lookup"><span data-stu-id="3358e-152">**Browser Link** is a new feature included in Visual Studio 2013 that provides a channel between the Visual Studio IDE and any open browser to exchange data between your web application and Visual Studio.</span></span> <span data-ttu-id="3358e-153">Web Essentials 扩展浏览器链接了用来操作 DOM 对象模型和您直接从浏览器的 web 页面的 CSS 样式的工具。</span><span class="sxs-lookup"><span data-stu-id="3358e-153">Web Essentials extends Browser Link with tools to manipulate the DOM object model and the CSS styles of your web pages directly from the browser.</span></span>

<span data-ttu-id="3358e-154">在此练习中，您将了解一些支持的功能**Web Essentials**并**浏览器链接**来增强简单的测验页。</span><span class="sxs-lookup"><span data-stu-id="3358e-154">In this exercise, you will explore some of the features supported by **Web Essentials** and **Browser Link** to enhance a simple quiz page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a><span data-ttu-id="3358e-155">任务 1-在多个浏览器中运行项目</span><span class="sxs-lookup"><span data-stu-id="3358e-155">Task 1 - Running the Project in Multiple Browsers</span></span>

<span data-ttu-id="3358e-156">在本任务中，将配置 web 应用程序以在多个浏览器在运行一次，这对于跨浏览器测试很有用。</span><span class="sxs-lookup"><span data-stu-id="3358e-156">In this task, you will configure your web application to run in multiple browsers at once, which is useful for cross-browser testing.</span></span>

1. <span data-ttu-id="3358e-157">打开**Microsoft Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="3358e-157">Open **Microsoft Visual Studio**.</span></span>
2. <span data-ttu-id="3358e-158">在中**文件**菜单中，选择**打开 |项目/解决方案...** 并浏览到**Ex1 WorkingwithBrowserLinkandWebEssentials\Begin**中**源**实验室 (C:\WebCampsTK\HOL\VSWebTooling\Source) 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="3358e-158">In the **File** menu, select **Open | Project/Solution...** and browse to **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** in the **Source** folder of the lab (C:\WebCampsTK\HOL\VSWebTooling\Source).</span></span> <span data-ttu-id="3358e-159">选择**Begin.sln**然后单击**打开**。</span><span class="sxs-lookup"><span data-stu-id="3358e-159">Select **Begin.sln** and click **Open**.</span></span>
3. <span data-ttu-id="3358e-160">在 Visual Studio 工具栏中，展开浏览器菜单并选择**浏览方式...**.</span><span class="sxs-lookup"><span data-stu-id="3358e-160">In the Visual Studio toolbar, expand the browser menu and select **Browse With...**.</span></span>

    <span data-ttu-id="3358e-161">![浏览与菜单选项](visual-studio-2013-web-tools/_static/image1.png "浏览与...在浏览器菜单")</span><span class="sxs-lookup"><span data-stu-id="3358e-161">![Browse With menu option](visual-studio-2013-web-tools/_static/image1.png "Browse with... in browser menu")</span></span>

    <span data-ttu-id="3358e-162">*浏览与菜单选项*</span><span class="sxs-lookup"><span data-stu-id="3358e-162">*Browse With menu option*</span></span>
4. <span data-ttu-id="3358e-163">中**浏览方式**对话框中，选择这两种**Google Chrome**并**Internet Explorer**通过按住**CTRL**键，然后单击**设置为默认值**。</span><span class="sxs-lookup"><span data-stu-id="3358e-163">In the **Browse With** dialog box, select both **Google Chrome** and **Internet Explorer** by holding down the **CTRL** key and click **Set as Default**.</span></span>

    <span data-ttu-id="3358e-164">![浏览方式对话框](visual-studio-2013-web-tools/_static/image2.png "浏览方式对话框")</span><span class="sxs-lookup"><span data-stu-id="3358e-164">![Browse with dialog box](visual-studio-2013-web-tools/_static/image2.png "Browse with dialog box")</span></span>

    <span data-ttu-id="3358e-165">*选择多个默认浏览器*</span><span class="sxs-lookup"><span data-stu-id="3358e-165">*Selecting multiple default browsers*</span></span>
5. <span data-ttu-id="3358e-166">Google Chrome 和 Internet Explorer 现在应显示为默认浏览器。</span><span class="sxs-lookup"><span data-stu-id="3358e-166">Both Google Chrome and Internet Explorer should now appear as the default browsers.</span></span> <span data-ttu-id="3358e-167">单击**取消**以关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="3358e-167">Click **Cancel** to close the dialog box.</span></span>

    <span data-ttu-id="3358e-168">![Google Chrome 和 Internet Explorer 设置为默认浏览器](visual-studio-2013-web-tools/_static/image3.png "Google Chrome 和 Internet Explorer 的默认浏览器")</span><span class="sxs-lookup"><span data-stu-id="3358e-168">![Google Chrome and Internet Explorer as default browsers](visual-studio-2013-web-tools/_static/image3.png "Google Chrome and Internet Explorer default browsers")</span></span>

    <span data-ttu-id="3358e-169">*Google Chrome 和 Internet Explorer 设置为默认浏览器*</span><span class="sxs-lookup"><span data-stu-id="3358e-169">*Google Chrome and Internet Explorer as default browsers*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3358e-170">配置默认浏览器之后,**多个浏览器**浏览器菜单中选择选项。</span><span class="sxs-lookup"><span data-stu-id="3358e-170">After configuring the default browsers, the **Multiple Browsers** option is selected in the browser menu.</span></span>
    > 
    > <span data-ttu-id="3358e-171">![多个浏览器](visual-studio-2013-web-tools/_static/image4.png "多个浏览器")</span><span class="sxs-lookup"><span data-stu-id="3358e-171">![Multiple browsers](visual-studio-2013-web-tools/_static/image4.png "Multiple browsers")</span></span>
6. <span data-ttu-id="3358e-172">按**CTRL** + **F5**不进行调试直接运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="3358e-172">Press **CTRL** + **F5** to run the application without debugging.</span></span>
7. <span data-ttu-id="3358e-173">这两个浏览器窗口打开时，请将其中一个上下放以便同时查看两个浏览器上的更新。</span><span class="sxs-lookup"><span data-stu-id="3358e-173">When both browser windows open, place one of them above the other in order to see the updates on both browsers simultaneously.</span></span> <span data-ttu-id="3358e-174">浏览器应显示具有浅蓝色矩形的 web 页。</span><span class="sxs-lookup"><span data-stu-id="3358e-174">The browsers should display a web page with a light-blue rectangle.</span></span>

    <span data-ttu-id="3358e-175">![放置一个浏览器上下](visual-studio-2013-web-tools/_static/image5.png "放置上面另一个浏览器")</span><span class="sxs-lookup"><span data-stu-id="3358e-175">![Placing one browser above the other](visual-studio-2013-web-tools/_static/image5.png "Placing one browser above the other")</span></span>

    <span data-ttu-id="3358e-176">*将上面另一个浏览器*</span><span class="sxs-lookup"><span data-stu-id="3358e-176">*Placing one browser above the other*</span></span>
8. <span data-ttu-id="3358e-177">不要关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="3358e-177">Do not close the browsers.</span></span> <span data-ttu-id="3358e-178">将在下一个任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="3358e-178">You will use them in the next task.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a><span data-ttu-id="3358e-179">任务 2-使用 Zen 编码来创建 HTML 元素</span><span class="sxs-lookup"><span data-stu-id="3358e-179">Task 2 - Using Zen Coding to Create HTML Elements</span></span>

<span data-ttu-id="3358e-180">**处理编码**是一种编辑器，适用于高速 HTML、 XML、 XSL （或任何其他结构化的代码格式） 插件编写代码和编辑。</span><span class="sxs-lookup"><span data-stu-id="3358e-180">**Zen Coding** is an editor plugin for high-speed HTML, XML, XSL (or any other structured code format) coding and editing.</span></span> <span data-ttu-id="3358e-181">此插件的核心是一个功能强大的缩写引擎可用于扩展到 HTML 代码-类似于 CSS 选择器的表达式。</span><span class="sxs-lookup"><span data-stu-id="3358e-181">The core of this plugin is a powerful abbreviation engine which allows you to expand expressions -similar to CSS selectors- into HTML code.</span></span> <span data-ttu-id="3358e-182">处理编码是一种编写 HTML 使用 CSS 样式选择器语法的快速方法。</span><span class="sxs-lookup"><span data-stu-id="3358e-182">Zen Coding is a fast way to write HTML using a CSS style selector syntax.</span></span>

<span data-ttu-id="3358e-183">在此练习中，将使用提供的 Web Essentials Zen 编码功能来生成表示问题的选项的 HTML 按钮。</span><span class="sxs-lookup"><span data-stu-id="3358e-183">In this exercise, you will use the Zen Coding feature provided by Web Essentials to generate the HTML buttons that represent the options of the question.</span></span>

1. <span data-ttu-id="3358e-184">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3358e-184">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="3358e-185">打开**Index.cshtml**文件位于**视图** | **主页**文件夹。</span><span class="sxs-lookup"><span data-stu-id="3358e-185">Open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="3358e-186">替换**&lt;！-TODO： 添加选项-&gt;** 注释以下代码，然后按**选项卡**。</span><span class="sxs-lookup"><span data-stu-id="3358e-186">Replace the **&lt;!-- TODO: add options here--&gt;** comment with the following code, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. <span data-ttu-id="3358e-187">代码应扩展到 HTML。</span><span class="sxs-lookup"><span data-stu-id="3358e-187">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="3358e-188">![扩展的 HTML](visual-studio-2013-web-tools/_static/image6.png "扩展 HTML")</span><span class="sxs-lookup"><span data-stu-id="3358e-188">![Expanded HTML](visual-studio-2013-web-tools/_static/image6.png "Expanded HTML")</span></span>

    <span data-ttu-id="3358e-189">*扩展的 HTML*</span><span class="sxs-lookup"><span data-stu-id="3358e-189">*Expanded HTML*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3358e-190">若要了解有关处理编码语法的详细信息，请参阅以下[一文](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="3358e-190">To learn more about Zen Coding syntax, see the following [article](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).</span></span>
5. <span data-ttu-id="3358e-191">单击**刷新链接的浏览器**按钮更新两个浏览器。</span><span class="sxs-lookup"><span data-stu-id="3358e-191">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="3358e-192">![刷新链接的浏览器](visual-studio-2013-web-tools/_static/image7.png "刷新链接的浏览器")</span><span class="sxs-lookup"><span data-stu-id="3358e-192">![Refresh linked browsers](visual-studio-2013-web-tools/_static/image7.png "Refresh linked browsers")</span></span>

    <span data-ttu-id="3358e-193">*刷新链接的浏览器*</span><span class="sxs-lookup"><span data-stu-id="3358e-193">*Refresh linked browsers*</span></span>

    <span data-ttu-id="3358e-194">![Internet Explorer-带四个按钮更新页](visual-studio-2013-web-tools/_static/image8.png "带四个按钮的 Internet 资源管理器-页面更新")</span><span class="sxs-lookup"><span data-stu-id="3358e-194">![Internet Explorer - Page updated with four buttons](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer - Page updated with four buttons")</span></span>

    <span data-ttu-id="3358e-195">*带四个按钮的 Internet 资源管理器-页面更新*</span><span class="sxs-lookup"><span data-stu-id="3358e-195">*Internet Explorer - Page updated with four buttons*</span></span>

    <span data-ttu-id="3358e-196">![Google Chrome-带四个按钮更新页](visual-studio-2013-web-tools/_static/image9.png "带四个按钮的 Google Chrome-页面更新")</span><span class="sxs-lookup"><span data-stu-id="3358e-196">![Google Chrome - Page updated with four buttons](visual-studio-2013-web-tools/_static/image9.png "Google Chrome - Page updated with four buttons")</span></span>

    <span data-ttu-id="3358e-197">*带四个按钮的 Google Chrome-页面更新*</span><span class="sxs-lookup"><span data-stu-id="3358e-197">*Google Chrome - Page updated with four buttons*</span></span>
6. <span data-ttu-id="3358e-198">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3358e-198">Switch back to Visual Studio.</span></span>
7. <span data-ttu-id="3358e-199">这些按钮添加到页上，但仍需要添加模板问题。</span><span class="sxs-lookup"><span data-stu-id="3358e-199">You have added the buttons to the page, but you still need to add a template question.</span></span> <span data-ttu-id="3358e-200">若要执行此操作，将使用一项新功能中调用的 Web Essentials**乱数假文生成器**。</span><span class="sxs-lookup"><span data-stu-id="3358e-200">To do so, you will use a new feature in Web Essentials called **Lorem Ipsum generator**.</span></span> <span data-ttu-id="3358e-201">找到**div**具有元素**类**特性**front**。</span><span class="sxs-lookup"><span data-stu-id="3358e-201">Locate the **div** element with the **class** attribute **front**.</span></span>
8. <span data-ttu-id="3358e-202">添加以下代码作为第一个子元素**div**，然后按**选项卡**。</span><span class="sxs-lookup"><span data-stu-id="3358e-202">Add the following code as the first child element of the **div**, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. <span data-ttu-id="3358e-203">代码应扩展到 HTML。</span><span class="sxs-lookup"><span data-stu-id="3358e-203">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="3358e-204">![乱数假文自动生成](visual-studio-2013-web-tools/_static/image10.png "乱数假文自动生成")</span><span class="sxs-lookup"><span data-stu-id="3358e-204">![Lorem Ipsum autogenerated](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum autogenerated")</span></span>

    <span data-ttu-id="3358e-205">*乱数假文自动生成*</span><span class="sxs-lookup"><span data-stu-id="3358e-205">*Lorem Ipsum autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3358e-206">作为处理编码的一部分，现在可以直接在 HTML 编辑器中生成乱数假文代码。</span><span class="sxs-lookup"><span data-stu-id="3358e-206">As part of Zen Coding, you can now generate Lorem Ipsum code directly in the HTML editor.</span></span> <span data-ttu-id="3358e-207">只需键入**lorem**并点击**选项卡**和 30 字乱数假文将插入文本。</span><span class="sxs-lookup"><span data-stu-id="3358e-207">Simply type **lorem** and hit **TAB** and a 30 word Lorem Ipsum text will be inserted.</span></span> <span data-ttu-id="3358e-208">例如，</span><span class="sxs-lookup"><span data-stu-id="3358e-208">E.g.</span></span> <span data-ttu-id="3358e-209">*lorem10*插入 10 位乱数假文的单词。</span><span class="sxs-lookup"><span data-stu-id="3358e-209">*lorem10* inserts 10 Lorem Ipsum words.</span></span>
10. <span data-ttu-id="3358e-210">将顶部的问题添加徽标，使用另一项新功能中调用的 Web Essentials **Lorem 像素生成器**。</span><span class="sxs-lookup"><span data-stu-id="3358e-210">You will add a logo at the top of the question by using another new feature in Web Essentials called **Lorem Pixel generator**.</span></span> <span data-ttu-id="3358e-211">添加以下代码作为第一个子元素**div**具有元素**容器**作为**类**值，然后按**选项卡**。</span><span class="sxs-lookup"><span data-stu-id="3358e-211">Add the following code as the first child element of the **div** element with **container** as **class** value, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. <span data-ttu-id="3358e-212">该代码应该扩展以 html 格式。</span><span class="sxs-lookup"><span data-stu-id="3358e-212">The code should expand to HTML.</span></span>

    <span data-ttu-id="3358e-213">![Lorem 像素自动生成](visual-studio-2013-web-tools/_static/image11.png "Lorem 像素自动生成")</span><span class="sxs-lookup"><span data-stu-id="3358e-213">![Lorem Pixel autogenerated](visual-studio-2013-web-tools/_static/image11.png "Lorem Pixel autogenerated")</span></span>

    <span data-ttu-id="3358e-214">*Lorem 像素自动生成*</span><span class="sxs-lookup"><span data-stu-id="3358e-214">*Lorem Pixel autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3358e-215">作为处理编码的一部分，还可以直接在 HTML 编辑器中生成 Lorem 像素的代码。</span><span class="sxs-lookup"><span data-stu-id="3358e-215">As part of Zen Coding, you can also generate Lorem Pixel code directly in the HTML editor.</span></span> <span data-ttu-id="3358e-216">只需键入**pix 200x200 动物**并点击**选项卡**和一个**i m g**将插入动物的大小为 200x200 映像的标记。</span><span class="sxs-lookup"><span data-stu-id="3358e-216">Simply type **pix-200x200-animals** and hit **TAB** and an **img** tag with a 200x200 image of an animal will be inserted.</span></span> <span data-ttu-id="3358e-217">有关详细信息，请参阅[Lorem 像素](http://www.lorempixel.com)。</span><span class="sxs-lookup"><span data-stu-id="3358e-217">For more information, refer to [Lorem Pixel](http://www.lorempixel.com).</span></span>
12. <span data-ttu-id="3358e-218">单击**刷新链接的浏览器**按钮更新两个浏览器。</span><span class="sxs-lookup"><span data-stu-id="3358e-218">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="3358e-219">![Internet Explorer-自动生成的图像和文本](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-自动生成的图像和文本")</span><span class="sxs-lookup"><span data-stu-id="3358e-219">![Internet Explorer - Autogenerated image and text](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer - Autogenerated image and text")</span></span>

    <span data-ttu-id="3358e-220">*Internet Explorer – 自动生成的图像和文本*</span><span class="sxs-lookup"><span data-stu-id="3358e-220">*Internet Explorer - Autogenerated image and text*</span></span>

    <span data-ttu-id="3358e-221">![Google Chrome-自动生成的图像和文本](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-自动生成的图像和文本")</span><span class="sxs-lookup"><span data-stu-id="3358e-221">![Google Chrome - Autogenerated image and text](visual-studio-2013-web-tools/_static/image13.png "Google Chrome - Autogenerated image and text")</span></span>

    <span data-ttu-id="3358e-222">*Google Chrome-自动生成的图像和文本*</span><span class="sxs-lookup"><span data-stu-id="3358e-222">*Google Chrome - Autogenerated image and text*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3358e-223">添加代码段时，将随机选择映像，因为可能不同的浏览器中显示的图像。</span><span class="sxs-lookup"><span data-stu-id="3358e-223">Because the image is selected randomly when adding the code snippet, the image shown in the browsers may differ.</span></span>
13. <span data-ttu-id="3358e-224">不要关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="3358e-224">Do not close the browsers.</span></span> <span data-ttu-id="3358e-225">将在下一个任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="3358e-225">You will use them in the next task.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a><span data-ttu-id="3358e-226">任务 3-更新样式属性</span><span class="sxs-lookup"><span data-stu-id="3358e-226">Task 3 - Updating a Style Property</span></span>

<span data-ttu-id="3358e-227">在本任务中，您将使用浏览器链接**检查模式**功能检测生成特定的 DOM 元素的确切位置，然后更新使用颜色选取器通过 Web 提供该元素的颜色属性Essentials。</span><span class="sxs-lookup"><span data-stu-id="3358e-227">In this task, you will use the Browser Link's **Inspect Mode** feature to detect the exact location where the specific DOM element is generated and then update the color property of that element using a color picker provided by Web Essentials.</span></span>

1. <span data-ttu-id="3358e-228">在 Internet Explorer 浏览器中，按**CTRL** + **ALT** + **我**若要启用检查模式。</span><span class="sxs-lookup"><span data-stu-id="3358e-228">In the Internet Explorer browser, press **CTRL** + **ALT** + **I** to enable Inspect Mode.</span></span>
2. <span data-ttu-id="3358e-229">将指针移动浅蓝色边框，然后单击。</span><span class="sxs-lookup"><span data-stu-id="3358e-229">Move the pointer over the light blue border and click.</span></span>

    <span data-ttu-id="3358e-230">![将指针移动到浅蓝色边框上方](visual-studio-2013-web-tools/_static/image14.png "浅蓝色边框上移动指针")</span><span class="sxs-lookup"><span data-stu-id="3358e-230">![Moving the pointer over the light blue border](visual-studio-2013-web-tools/_static/image14.png "Moving the pointer over the light blue border")</span></span>

    <span data-ttu-id="3358e-231">*浅蓝色边框上移动指针*</span><span class="sxs-lookup"><span data-stu-id="3358e-231">*Moving the pointer over the light blue border*</span></span>
3. <span data-ttu-id="3358e-232">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3358e-232">Switch back to Visual Studio.</span></span> <span data-ttu-id="3358e-233">请注意如何在 Visual Studio HTML 编辑器中还选择在浏览器中选择 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="3358e-233">Notice how the HTML element that you selected in the browser is also selected in the Visual Studio HTML editor.</span></span>

    <span data-ttu-id="3358e-234">![在 Visual Studio HTML 编辑器中选择 HTML 元素](visual-studio-2013-web-tools/_static/image15.png "Visual Studio HTML 编辑器中选择 HTML 元素")</span><span class="sxs-lookup"><span data-stu-id="3358e-234">![HTML element selected in the Visual Studio HTML editor](visual-studio-2013-web-tools/_static/image15.png "HTML element selected in the Visual Studio HTML editor")</span></span>

    <span data-ttu-id="3358e-235">*在 Visual Studio HTML 编辑器中选择 HTML 元素*</span><span class="sxs-lookup"><span data-stu-id="3358e-235">*HTML element selected in the Visual Studio HTML editor*</span></span>
4. <span data-ttu-id="3358e-236">现在，你将更新**front**以更改所选元素的样式的 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="3358e-236">You will now update the **front** CSS class in order to change the styling of the selected element.</span></span> <span data-ttu-id="3358e-237">若要执行此操作，按**CTRL** + **，** 以打开**导航到**搜索框中。</span><span class="sxs-lookup"><span data-stu-id="3358e-237">To do so, press **CTRL** + **,** to open the **Navigate To** search box.</span></span> <span data-ttu-id="3358e-238">类型**site.css**然后按**ENTER**以打开该文件。</span><span class="sxs-lookup"><span data-stu-id="3358e-238">Type **site.css** and press **ENTER** to open the file.</span></span>

    <span data-ttu-id="3358e-239">![打开文件 Site.css](visual-studio-2013-web-tools/_static/image16.png "打开 Site.css 文件")</span><span class="sxs-lookup"><span data-stu-id="3358e-239">![Opening file Site.css](visual-studio-2013-web-tools/_static/image16.png "Opening file Site.css")</span></span>

    <span data-ttu-id="3358e-240">*打开文件 Site.css*</span><span class="sxs-lookup"><span data-stu-id="3358e-240">*Opening file Site.css*</span></span>
5. <span data-ttu-id="3358e-241">按**CTRL** + **F**输 **.flip 容器.front**若要查找的 CSS 选择器。</span><span class="sxs-lookup"><span data-stu-id="3358e-241">Press **CTRL** + **F** and type **.flip-containter .front** to find the CSS selector.</span></span>
6. <span data-ttu-id="3358e-242">单击以打开颜色选取器的类的边框属性中的浅蓝色正方形。</span><span class="sxs-lookup"><span data-stu-id="3358e-242">Click the light blue square in the border property of the class to open the Color Picker.</span></span>

    <span data-ttu-id="3358e-243">![打开颜色选取器](visual-studio-2013-web-tools/_static/image17.png "打开颜色选取器")</span><span class="sxs-lookup"><span data-stu-id="3358e-243">![Opening the Color Picker](visual-studio-2013-web-tools/_static/image17.png "Opening the Color Picker")</span></span>

    <span data-ttu-id="3358e-244">*打开颜色选取器*</span><span class="sxs-lookup"><span data-stu-id="3358e-244">*Opening the Color Picker*</span></span>
7. <span data-ttu-id="3358e-245">通过单击 v 形图标按钮展开颜色选取器并选择一种新颜色。</span><span class="sxs-lookup"><span data-stu-id="3358e-245">Expand the Color Picker by clicking the chevron button and select a new color.</span></span>

    <span data-ttu-id="3358e-246">![展开颜色选取器](visual-studio-2013-web-tools/_static/image18.png "展开颜色选取器")</span><span class="sxs-lookup"><span data-stu-id="3358e-246">![Expanding the Color Picker](visual-studio-2013-web-tools/_static/image18.png "Expanding the Color Picker")</span></span>

    <span data-ttu-id="3358e-247">*展开颜色选取器*</span><span class="sxs-lookup"><span data-stu-id="3358e-247">*Expanding the Color Picker*</span></span>
8. <span data-ttu-id="3358e-248">按**CTRL** + **ALT** + **ENTER**刷新链接的浏览器。</span><span class="sxs-lookup"><span data-stu-id="3358e-248">Press **CTRL** + **ALT** + **ENTER** to refresh linked browsers.</span></span>
9. <span data-ttu-id="3358e-249">切换到 Internet 资源管理器，并请注意如何变化边框的颜色。</span><span class="sxs-lookup"><span data-stu-id="3358e-249">Switch to Internet Explorer and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="3358e-250">![Internet Explorer 的更新的边框颜色](visual-studio-2013-web-tools/_static/image19.png "Internet 资源管理器-更新的边框颜色")</span><span class="sxs-lookup"><span data-stu-id="3358e-250">![Internet Explorer - Border color updated](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer - Border color updated")</span></span>

    <span data-ttu-id="3358e-251">*Internet Explorer 的更新的边框颜色*</span><span class="sxs-lookup"><span data-stu-id="3358e-251">*Internet Explorer - Border color updated*</span></span>
10. <span data-ttu-id="3358e-252">切换到 Google Chrome，请注意如何变化边框的颜色。</span><span class="sxs-lookup"><span data-stu-id="3358e-252">Switch to Google Chrome and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="3358e-253">![Google Chrome-更新的边框颜色](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-更新的边框颜色")</span><span class="sxs-lookup"><span data-stu-id="3358e-253">![Google Chrome - Border color updated](visual-studio-2013-web-tools/_static/image20.png "Google Chrome - Border color updated")</span></span>

    <span data-ttu-id="3358e-254">*Google Chrome-更新的边框颜色*</span><span class="sxs-lookup"><span data-stu-id="3358e-254">*Google Chrome - Border color updated*</span></span>
11. <span data-ttu-id="3358e-255">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3358e-255">Switch back to Visual Studio.</span></span>
12. <span data-ttu-id="3358e-256">转到末尾**Site.css**文件，然后按**CTRL** + **F**查找 **.btn**选择器。</span><span class="sxs-lookup"><span data-stu-id="3358e-256">Go to the end of the **Site.css** file and press **CTRL** + **F** to locate the **.btn** selector.</span></span>
13. <span data-ttu-id="3358e-257">请注意， **-webkit 边框半径**属性是否带下划线显示为绿色。</span><span class="sxs-lookup"><span data-stu-id="3358e-257">Notice that the **-webkit-border-radius** property is underlined in green.</span></span>

    <span data-ttu-id="3358e-258">![-webkit 边框半径 btn 选择器的属性](visual-studio-2013-web-tools/_static/image21.png "btn 选择器-webkit 边框半径属性")</span><span class="sxs-lookup"><span data-stu-id="3358e-258">![-webkit-border-radius property of the btn selector](visual-studio-2013-web-tools/_static/image21.png "-webkit-border-radius property of the btn selector")</span></span>

    <span data-ttu-id="3358e-259">*-webkit 边框半径属性的 btn 选择器*</span><span class="sxs-lookup"><span data-stu-id="3358e-259">*-webkit-border-radius property of the btn selector*</span></span>
14. <span data-ttu-id="3358e-260">将在光标 **-webkit 边框半径**属性。</span><span class="sxs-lookup"><span data-stu-id="3358e-260">Place the caret in the **-webkit-border-radius** property.</span></span> <span data-ttu-id="3358e-261">属性的第一个单词的第一个字母下应显示一条蓝线。</span><span class="sxs-lookup"><span data-stu-id="3358e-261">A blue line should appear under the first letter of the first word of the property.</span></span> <span data-ttu-id="3358e-262">这是**智能标记**。</span><span class="sxs-lookup"><span data-stu-id="3358e-262">This is the **smart tag**.</span></span>
15. <span data-ttu-id="3358e-263">按**CTRL** + **。**</span><span class="sxs-lookup"><span data-stu-id="3358e-263">Press **CTRL** + **.**</span></span> <span data-ttu-id="3358e-264">若要打开建议菜单上，然后单击**缺少标准属性 （边框半径） 添加**。</span><span class="sxs-lookup"><span data-stu-id="3358e-264">to open the suggestions menu and click **Add missing standard property (border-radius)**.</span></span>

    <span data-ttu-id="3358e-265">![添加缺少的标准属性建议](visual-studio-2013-web-tools/_static/image22.png "添加缺少的标准属性建议")</span><span class="sxs-lookup"><span data-stu-id="3358e-265">![Add missing standard property suggestion](visual-studio-2013-web-tools/_static/image22.png "Add missing standard property suggestion")</span></span>

    <span data-ttu-id="3358e-266">*添加缺失的标准属性建议*</span><span class="sxs-lookup"><span data-stu-id="3358e-266">*Add missing standard property suggestion*</span></span>
16. <span data-ttu-id="3358e-267">**边框半径**属性将自动添加到 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="3358e-267">The **border-radius** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="3358e-268">![添加的标准属性缺失](visual-studio-2013-web-tools/_static/image23.png "缺少添加的标准属性")</span><span class="sxs-lookup"><span data-stu-id="3358e-268">![Missing standard property added](visual-studio-2013-web-tools/_static/image23.png "Missing standard property added")</span></span>

    <span data-ttu-id="3358e-269">*缺少添加的标准属性*</span><span class="sxs-lookup"><span data-stu-id="3358e-269">*Missing standard property added*</span></span>
17. <span data-ttu-id="3358e-270">将指针移**边框半径**属性来显示**浏览器矩阵工具提示**。</span><span class="sxs-lookup"><span data-stu-id="3358e-270">Move the pointer over the **border-radius** property to display the **Browser matrix tooltip**.</span></span> <span data-ttu-id="3358e-271">**浏览器矩阵工具提示**在每个浏览器中显示该属性的可用性。</span><span class="sxs-lookup"><span data-stu-id="3358e-271">The **Browser matrix tooltip** shows the availability of the property in each browser.</span></span>

    <span data-ttu-id="3358e-272">![浏览器矩阵工具提示](visual-studio-2013-web-tools/_static/image24.png "浏览器矩阵工具提示")</span><span class="sxs-lookup"><span data-stu-id="3358e-272">![Browser matrix tooltip](visual-studio-2013-web-tools/_static/image24.png "Browser matrix tooltip")</span></span>

    <span data-ttu-id="3358e-273">*浏览器矩阵工具提示*</span><span class="sxs-lookup"><span data-stu-id="3358e-273">*Browser matrix tooltip*</span></span>
18. <span data-ttu-id="3358e-274">请注意，值**边框半径**属性是否仍带有下划线。</span><span class="sxs-lookup"><span data-stu-id="3358e-274">Notice that the value of the **border-radius** property is still underlined.</span></span> <span data-ttu-id="3358e-275">将指针移值以查看警告消息。</span><span class="sxs-lookup"><span data-stu-id="3358e-275">Move the pointer over the value to see the warning message.</span></span>

    <span data-ttu-id="3358e-276">![边框半径属性值警告](visual-studio-2013-web-tools/_static/image25.png "边框半径属性值警告")</span><span class="sxs-lookup"><span data-stu-id="3358e-276">![Border-radius property value warning](visual-studio-2013-web-tools/_static/image25.png "Border-radius property value warning")</span></span>

    <span data-ttu-id="3358e-277">*边框半径属性值警告*</span><span class="sxs-lookup"><span data-stu-id="3358e-277">*Border-radius property value warning*</span></span>
19. <span data-ttu-id="3358e-278">删除的单元**边框半径**作为工具提示所建议的属性值。</span><span class="sxs-lookup"><span data-stu-id="3358e-278">Remove the unit of the **border-radius** property value as suggested by the tooltip.</span></span>
20. <span data-ttu-id="3358e-279">作为**边框半径**是用于定义如何圆角的边框边角是，您可以删除的标准属性 **-webkit 边框半径**属性和值从 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="3358e-279">As **border-radius** is the standard property for defining how rounded border corners are, you can remove the **-webkit-border-radius** property and value from the CSS rule.</span></span>
21. <span data-ttu-id="3358e-280">将在光标**自动换行**属性，请注意，下面也会出现智能标记。</span><span class="sxs-lookup"><span data-stu-id="3358e-280">Place the caret in the **word-wrap** property and notice that the smart tag also appears below.</span></span>
22. <span data-ttu-id="3358e-281">打开菜单，然后单击**添加缺少的供应商具体内容**。</span><span class="sxs-lookup"><span data-stu-id="3358e-281">Open the menu and click **Add missing vendor specifics**.</span></span>

    <span data-ttu-id="3358e-282">![添加缺少的供应商细节建议](visual-studio-2013-web-tools/_static/image26.png "添加缺少的供应商细节建议")</span><span class="sxs-lookup"><span data-stu-id="3358e-282">![Add missing vendor specifics suggestion](visual-studio-2013-web-tools/_static/image26.png "Add missing vendor specifics suggestion")</span></span>

    <span data-ttu-id="3358e-283">*添加缺少的供应商细节建议*</span><span class="sxs-lookup"><span data-stu-id="3358e-283">*Add missing vendor specifics suggestion*</span></span>
23. <span data-ttu-id="3358e-284">**Ms 自动换行**属性将自动添加到 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="3358e-284">The **-ms-word-wrap** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="3358e-285">![供应商特定属性添加](visual-studio-2013-web-tools/_static/image27.png "添加供应商特定属性")</span><span class="sxs-lookup"><span data-stu-id="3358e-285">![Vendor specific property added](visual-studio-2013-web-tools/_static/image27.png "Vendor specific property added")</span></span>

    <span data-ttu-id="3358e-286">*添加的供应商特定属性*</span><span class="sxs-lookup"><span data-stu-id="3358e-286">*Vendor specific property added*</span></span>

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a><span data-ttu-id="3358e-287">任务 4-更新浏览器中的 HTML 代码</span><span class="sxs-lookup"><span data-stu-id="3358e-287">Task 4 - Updating the HTML Code from the Browser</span></span>

<span data-ttu-id="3358e-288">在本任务中，您将使用浏览器链接**设计模式下**编辑浏览器中的 DOM 对象并将所做的更改传输到 Visual Studio 中的 HTML 源代码文件的功能。</span><span class="sxs-lookup"><span data-stu-id="3358e-288">In this task, you will use the Browser Link's **Design Mode** feature to edit the DOM object from the browser and transfer the changes to the HTML source file in Visual Studio.</span></span>

1. <span data-ttu-id="3358e-289">在 Google Chrome 中，按**CTRL** + **ALT** + **D**若要启用设计模式。</span><span class="sxs-lookup"><span data-stu-id="3358e-289">In Google Chrome, press **CTRL** + **ALT** + **D** to enable Design Mode.</span></span>
2. <span data-ttu-id="3358e-290">将指针移**Lorem Ipsum dolor sit amet**标记，单击。</span><span class="sxs-lookup"><span data-stu-id="3358e-290">Move the pointer over the **Lorem Ipsum dolor sit amet** label and click.</span></span>

    <span data-ttu-id="3358e-291">![编辑问题](visual-studio-2013-web-tools/_static/image28.png "编辑问题")</span><span class="sxs-lookup"><span data-stu-id="3358e-291">![Editing the question](visual-studio-2013-web-tools/_static/image28.png "Editing the question")</span></span>

    <span data-ttu-id="3358e-292">*编辑问题*</span><span class="sxs-lookup"><span data-stu-id="3358e-292">*Editing the question*</span></span>
3. <span data-ttu-id="3358e-293">应显示光标。</span><span class="sxs-lookup"><span data-stu-id="3358e-293">A cursor should appear.</span></span> <span data-ttu-id="3358e-294">将原始文本替换为*什么它看起来像时我编写一个较长的问题？*，然后按**ESC**退出设计模式。</span><span class="sxs-lookup"><span data-stu-id="3358e-294">Replace the original text with *What does it look like when I write a longer question?*, and then press **ESC** to exit Design Mode.</span></span>

    <span data-ttu-id="3358e-295">![编辑的问题](visual-studio-2013-web-tools/_static/image29.png "编辑的问题")</span><span class="sxs-lookup"><span data-stu-id="3358e-295">![Question edited](visual-studio-2013-web-tools/_static/image29.png "Question edited")</span></span>

    <span data-ttu-id="3358e-296">*编辑的问题*</span><span class="sxs-lookup"><span data-stu-id="3358e-296">*Question edited*</span></span>
4. <span data-ttu-id="3358e-297">切换回 Visual Studio 并打开**Index.cshtml**，如果尚未打开。</span><span class="sxs-lookup"><span data-stu-id="3358e-297">Switch back to Visual Studio and open **Index.cshtml**, if not already opened.</span></span> <span data-ttu-id="3358e-298">请注意的内部文本**&lt;p&gt;** 更新元素。</span><span class="sxs-lookup"><span data-stu-id="3358e-298">Notice that the inner text of the **&lt;p&gt;** element has been updated.</span></span>

    <span data-ttu-id="3358e-299">![在 HTML 页面中的最新问题](visual-studio-2013-web-tools/_static/image30.png "HTML 页中的更新问题")</span><span class="sxs-lookup"><span data-stu-id="3358e-299">![Updated question in the HTML page](visual-studio-2013-web-tools/_static/image30.png "Updated question in the HTML page")</span></span>

    <span data-ttu-id="3358e-300">*在 HTML 页面中的更新的问题*</span><span class="sxs-lookup"><span data-stu-id="3358e-300">*Updated question in the HTML page*</span></span>

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a><span data-ttu-id="3358e-301">任务 5-查看 SEO 相关警告</span><span class="sxs-lookup"><span data-stu-id="3358e-301">Task 5 - Reviewing SEO Related Warnings</span></span>

<span data-ttu-id="3358e-302">**搜索引擎优化**(SEO) 是网站排名更高版本上的搜索引擎结果列表中的过程。</span><span class="sxs-lookup"><span data-stu-id="3358e-302">**Search Engine Optimization** (SEO) is the process of making a website rank higher on a search engine's list of results.</span></span> <span data-ttu-id="3358e-303">更高版本站点进行排名和更连贯地列出，该站点将从该搜索引擎获取更多访问者。</span><span class="sxs-lookup"><span data-stu-id="3358e-303">The higher the site ranks and the more consistently it is listed, the more visitors the site will get from that search engine.</span></span> <span data-ttu-id="3358e-304">Web Essentials 合并检查 HTML 的分析工具，报告问题，找到并提供了帮助来解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="3358e-304">Web Essentials incorporates an analytical tool that examines HTML, reports the issues found and provides assistance to fix them.</span></span>

1. <span data-ttu-id="3358e-305">转到**视图**菜单，然后单击**错误列表**以打开**错误列表**窗口。</span><span class="sxs-lookup"><span data-stu-id="3358e-305">Go to the **View** menu and click **Error List** to open the **Error List** window.</span></span>

    <span data-ttu-id="3358e-306">![错误列表视图中菜单](visual-studio-2013-web-tools/_static/image31.png "视图菜单中的错误列表")</span><span class="sxs-lookup"><span data-stu-id="3358e-306">![Error List in View menu](visual-studio-2013-web-tools/_static/image31.png "Error List in View menu")</span></span>

    <span data-ttu-id="3358e-307">*错误列表视图中菜单*</span><span class="sxs-lookup"><span data-stu-id="3358e-307">*Error List in View menu*</span></span>
2. <span data-ttu-id="3358e-308">请注意，没有通知的 SEO 警告**&lt;meta&gt;** 标记为缺少页说明。</span><span class="sxs-lookup"><span data-stu-id="3358e-308">Notice that there is an SEO warning notifying that a **&lt;meta&gt;** tag for the page description is missing.</span></span> <span data-ttu-id="3358e-309">双击 SEO 警告条目，以修复此错误。</span><span class="sxs-lookup"><span data-stu-id="3358e-309">Double-click the SEO warning entry to fix it.</span></span>

    <span data-ttu-id="3358e-310">![错误列表窗口](visual-studio-2013-web-tools/_static/image32.png "错误列表窗口")</span><span class="sxs-lookup"><span data-stu-id="3358e-310">![Error List window](visual-studio-2013-web-tools/_static/image32.png "Error List window")</span></span>

    <span data-ttu-id="3358e-311">*错误列表窗口*</span><span class="sxs-lookup"><span data-stu-id="3358e-311">*Error List window*</span></span>
3. <span data-ttu-id="3358e-312">在中**Web Essentials**对话框中，单击**是**插入说明&lt;元&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="3358e-312">In the **Web Essentials** dialog box, click **Yes** to insert a description &lt;meta&gt; tag.</span></span>

    <span data-ttu-id="3358e-313">![Web Essentials 对话框](visual-studio-2013-web-tools/_static/image33.png "Web Essentials 对话框")</span><span class="sxs-lookup"><span data-stu-id="3358e-313">![Web Essentials dialog box](visual-studio-2013-web-tools/_static/image33.png "Web Essentials dialog box")</span></span>

    <span data-ttu-id="3358e-314">*Web Essentials 对话框*</span><span class="sxs-lookup"><span data-stu-id="3358e-314">*Web Essentials dialog box*</span></span>
4. <span data-ttu-id="3358e-315">编辑器 **\_Layout.cshtml**此时将打开并**&lt;元&gt;** 标记自动添加到**头**部分HTML 文件。</span><span class="sxs-lookup"><span data-stu-id="3358e-315">The editor for **\_Layout.cshtml** opens and the **&lt;meta&gt;** tag is automatically added to the **head** section of the HTML file.</span></span>

    <span data-ttu-id="3358e-316">![自动添加 _Layout 页中的 Meta 标记](visual-studio-2013-web-tools/_static/image34.png "Meta 标记自动添加在 _Layout 页")</span><span class="sxs-lookup"><span data-stu-id="3358e-316">![Meta tag automatically added in _Layout page](visual-studio-2013-web-tools/_static/image34.png "Meta tag automatically added in _Layout page")</span></span>

    <span data-ttu-id="3358e-317">*Meta 标记自动添加到\_布局页*</span><span class="sxs-lookup"><span data-stu-id="3358e-317">*Meta tag automatically added to \_Layout page*</span></span>
5. <span data-ttu-id="3358e-318">更改的值**内容**归于*GeekQuiz*并保存该文件。</span><span class="sxs-lookup"><span data-stu-id="3358e-318">Change the value of the **content** attribute to *GeekQuiz* and save the file.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a><span data-ttu-id="3358e-319">练习 2： 利用代码段和 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="3358e-319">Exercise 2: Taking Advantage of Code Snippets and IntelliSense</span></span>

<span data-ttu-id="3358e-320">使用 Web Essentials HTML 编辑器已扩展具有额外功能。</span><span class="sxs-lookup"><span data-stu-id="3358e-320">With Web Essentials, the HTML editor has been extended with extra functionality.</span></span> <span data-ttu-id="3358e-321">在此练习中，你将看到一些新功能，开发 web 应用程序时很有用。</span><span class="sxs-lookup"><span data-stu-id="3358e-321">In this exercise, you will see some new features that are helpful when developing web applications.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a><span data-ttu-id="3358e-322">任务 1-在 HTML 文档中使用 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="3358e-322">Task 1 - Using IntelliSense in HTML Documents</span></span>

<span data-ttu-id="3358e-323">您将看到在本任务中的第一个新功能称为**动态 IntelliSense**。</span><span class="sxs-lookup"><span data-stu-id="3358e-323">The first new feature you will see in this task is called **Dynamic IntelliSense**.</span></span> <span data-ttu-id="3358e-324">动态 IntelliSense 读取其他标记和属性，以推断可能将使用的 id。</span><span class="sxs-lookup"><span data-stu-id="3358e-324">Dynamic IntelliSense reads other tags and attributes to infer the possible ids you will use.</span></span>

<span data-ttu-id="3358e-325">在本任务中，将创建新的 HTML 窗体元素包含一个标签和输入的字段。</span><span class="sxs-lookup"><span data-stu-id="3358e-325">In this task, you will create a new HTML form element which contains a label and an input field.</span></span> <span data-ttu-id="3358e-326">然后，您将添加**为**属性为要将其绑定到的输入的标签，你将看到 IntelliSense 建议基于作用域中的输入的 id。</span><span class="sxs-lookup"><span data-stu-id="3358e-326">Then you will add a **for** attribute to the label to bind it to the input, and you will see IntelliSense suggestions based on the ids of the inputs in scope.</span></span>

1. <span data-ttu-id="3358e-327">打开**Visual Studio Express 2013 for Web**并**Begin.sln**解决方案位于**源/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/开始**文件夹。</span><span class="sxs-lookup"><span data-stu-id="3358e-327">Open **Visual Studio Express 2013 for Web** and the **Begin.sln** solution located in the **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin** folder.</span></span> <span data-ttu-id="3358e-328">或者，继续使用该解决方案并获得前一练习中。</span><span class="sxs-lookup"><span data-stu-id="3358e-328">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="3358e-329">在中**解决方案资源管理器**，打开**Index.cshtml**文件位于**视图** | **主页**文件夹。</span><span class="sxs-lookup"><span data-stu-id="3358e-329">In **Solution Explorer**, open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="3358e-330">添加以下形式内的**&lt;部分&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="3358e-330">Add the following form inside the **&lt;section&gt;** element.</span></span>

    <span data-ttu-id="3358e-331">(代码段- *VisualStudio2013WebTooling* - *Ex2* - *窗体*)</span><span class="sxs-lookup"><span data-stu-id="3358e-331">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *Form*)</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. <span data-ttu-id="3358e-332">输入的标记前面应带有标签的字段的一些说明。</span><span class="sxs-lookup"><span data-stu-id="3358e-332">The input tag should be preceded by a label with some description of the field.</span></span> <span data-ttu-id="3358e-333">添加以下标签之前输入的标记。</span><span class="sxs-lookup"><span data-stu-id="3358e-333">Add the following label before the input tag.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. <span data-ttu-id="3358e-334">**有关**的属性**&lt;标签&gt;** 指定标签的窗体元素绑定到。</span><span class="sxs-lookup"><span data-stu-id="3358e-334">The **for** attribute of a **&lt;label&gt;** specifies which form element a label is bound to.</span></span> <span data-ttu-id="3358e-335">该属性的值应设置为相关的元素的 id。</span><span class="sxs-lookup"><span data-stu-id="3358e-335">The attribute's value should be equal to the id of the related element.</span></span> <span data-ttu-id="3358e-336">添加**有关**归于**&lt;标签&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="3358e-336">Add the **for** attribute to the **&lt;label&gt;** element.</span></span> <span data-ttu-id="3358e-337">下图中所示&quot;名称&quot;值会弹出在 IntelliSense 中，基于相同的作用域内的元素的 id (封闭**&lt;窗体&gt;**)。</span><span class="sxs-lookup"><span data-stu-id="3358e-337">As shown in the following figure, the &quot;name&quot; value pops up in the IntelliSense box, based on the id of the elements within the same scope (the enclosing **&lt;form&gt;**).</span></span>

    <span data-ttu-id="3358e-338">![在 IntelliSense 中显示 id](visual-studio-2013-web-tools/_static/image35.png "id 显示在 IntelliSense 中")</span><span class="sxs-lookup"><span data-stu-id="3358e-338">![Showing the id in IntelliSense](visual-studio-2013-web-tools/_static/image35.png "Showing the id in IntelliSense")</span></span>

    <span data-ttu-id="3358e-339">*显示在 IntelliSense 中的 id*</span><span class="sxs-lookup"><span data-stu-id="3358e-339">*Showing the id in IntelliSense*</span></span>
6. <span data-ttu-id="3358e-340">删除最近添加**&lt;窗体&gt;** 元素和其内容。</span><span class="sxs-lookup"><span data-stu-id="3358e-340">Delete the recently added **&lt;form&gt;** element and its content.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a><span data-ttu-id="3358e-341">任务 2-使用 HTML 代码段</span><span class="sxs-lookup"><span data-stu-id="3358e-341">Task 2 - Using HTML Code Snippets</span></span>

<span data-ttu-id="3358e-342">HTML5 引入了 25 个以上的新语义标记。</span><span class="sxs-lookup"><span data-stu-id="3358e-342">HTML5 introduced more than 25 new semantic tags.</span></span> <span data-ttu-id="3358e-343">Visual Studio 已具有对这些标记的 IntelliSense 支持，但 Visual Studio 2013 可以更快、 更轻松地通过添加新的代码片段编写标记。</span><span class="sxs-lookup"><span data-stu-id="3358e-343">Visual Studio already had IntelliSense support for these tags, but Visual Studio 2013 makes it faster and easier to write markup by adding new code snippets.</span></span> <span data-ttu-id="3358e-344">尽管这些标记不是复杂的但这会产生一些小的微妙之处，例如添加为正确的编解码器回退*音频*标记。</span><span class="sxs-lookup"><span data-stu-id="3358e-344">Though these tags are not complicated, they come with a few small subtleties, such as adding the correct codec fallbacks for the *audio* tag.</span></span> <span data-ttu-id="3358e-345">在此任务中，您将看到的音频的标记的 HTML 代码段。</span><span class="sxs-lookup"><span data-stu-id="3358e-345">In this task, you will see the HTML code snippets for the audio tag.</span></span>

1. <span data-ttu-id="3358e-346">在中**Index.cshtml**文件中，键入 **&lt;aud**内**&lt;部分&gt;** 元素在下图中所示。</span><span class="sxs-lookup"><span data-stu-id="3358e-346">In the **Index.cshtml** file, type **&lt;aud** inside the **&lt;section&gt;** element as shown in the following figure.</span></span>

    <span data-ttu-id="3358e-347">![插入音频元素](visual-studio-2013-web-tools/_static/image36.png "插入音频元素")</span><span class="sxs-lookup"><span data-stu-id="3358e-347">![Inserting an audio element](visual-studio-2013-web-tools/_static/image36.png "Inserting an audio element")</span></span>

    <span data-ttu-id="3358e-348">*插入音频元素*</span><span class="sxs-lookup"><span data-stu-id="3358e-348">*Inserting an audio element*</span></span>
2. <span data-ttu-id="3358e-349">按**选项卡**两次请注意如何在页上添加以下代码，并将光标置于**src**的第一个源的属性。</span><span class="sxs-lookup"><span data-stu-id="3358e-349">Press **TAB** twice and notice how the following code is added on the page and the cursor is placed on the **src** attribute of the first source.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > <span data-ttu-id="3358e-350">通过按**选项卡**键两次，插入代码段。</span><span class="sxs-lookup"><span data-stu-id="3358e-350">By pressing the **TAB** key twice, the code snippet is inserted.</span></span> <span data-ttu-id="3358e-351">音频的代码段显示了标准使用情况*音频*具有改进的支持的两个源代码文件的标记。</span><span class="sxs-lookup"><span data-stu-id="3358e-351">The audio snippet shows the standard usage of the *audio* tag, with two source files for improved support.</span></span>
3. <span data-ttu-id="3358e-352">删除第二行，然后使用以下链接 WebCampsTV Katana 显示更新的第一行源： [ http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3 ](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)。</span><span class="sxs-lookup"><span data-stu-id="3358e-352">Delete the second line and update the source of the first line with the following link to the WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3).</span></span> <span data-ttu-id="3358e-353">生成的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="3358e-353">The resulting code is shown below.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="3358e-354">源文件*KatanaProject.mp3*用作示例。</span><span class="sxs-lookup"><span data-stu-id="3358e-354">The source file *KatanaProject.mp3* is used as an example.</span></span> <span data-ttu-id="3358e-355">如果您愿意，可以使用另一个源。</span><span class="sxs-lookup"><span data-stu-id="3358e-355">You can use another source if you prefer.</span></span>
4. <span data-ttu-id="3358e-356">按**CTRL** + **S**保存该文件。</span><span class="sxs-lookup"><span data-stu-id="3358e-356">Press **CTRL** + **S** to save the file.</span></span>
5. <span data-ttu-id="3358e-357">按**CTRL** + **F5**启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="3358e-357">Press **CTRL** + **F5** to start the application.</span></span>
6. <span data-ttu-id="3358e-358">请注意音频播放机已添加到应用程序。</span><span class="sxs-lookup"><span data-stu-id="3358e-358">Notice that an audio player was added to the application.</span></span>

    <span data-ttu-id="3358e-359">![在 Internet Explorer 中的音频播放器](visual-studio-2013-web-tools/_static/image37.png "在 Internet Explorer 中的音频播放机")</span><span class="sxs-lookup"><span data-stu-id="3358e-359">![Audio player in Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "Audio player in Internet Explorer")</span></span>

    <span data-ttu-id="3358e-360">*在 Internet Explorer 中的音频播放器*</span><span class="sxs-lookup"><span data-stu-id="3358e-360">*Audio player in Internet Explorer*</span></span>

    <span data-ttu-id="3358e-361">![在 Google Chrome 中的音频播放器](visual-studio-2013-web-tools/_static/image38.png "音频播放机在 Google Chrome")</span><span class="sxs-lookup"><span data-stu-id="3358e-361">![Audio player in Google Chrome](visual-studio-2013-web-tools/_static/image38.png "Audio player in Google Chrome")</span></span>

    <span data-ttu-id="3358e-362">*在 Google Chrome 中的音频播放器*</span><span class="sxs-lookup"><span data-stu-id="3358e-362">*Audio player in Google Chrome*</span></span>
7. <span data-ttu-id="3358e-363">不要关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="3358e-363">Do not close the browsers.</span></span> <span data-ttu-id="3358e-364">将在下一个任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="3358e-364">You will use them in the next task.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a><span data-ttu-id="3358e-365">任务 3-使用 JavaScript 文档中的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="3358e-365">Task 3 - Using IntelliSense in JavaScript Documents</span></span>

<span data-ttu-id="3358e-366">Web Essentials 2013，样式表和 HTML 页面生成 Id 和类名称的列表。</span><span class="sxs-lookup"><span data-stu-id="3358e-366">With Web Essentials 2013, style sheets and HTML pages produce a list of IDs and class names.</span></span> <span data-ttu-id="3358e-367">在本任务中，您将学习如何这些列表，从而改进 Web Essentials 2013 中的 JavaScript IntelliSense 支持。</span><span class="sxs-lookup"><span data-stu-id="3358e-367">In this task, you will learn how those lists improve JavaScript IntelliSense support in Web Essentials 2013.</span></span>

1. <span data-ttu-id="3358e-368">在中**Index.cshtml**文件中，添加以下代码以定义**脚本**标记的 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="3358e-368">In the **Index.cshtml** file, add the following code to define a **script** tag for JavaScript code.</span></span>

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. <span data-ttu-id="3358e-369">添加以下代码**脚本**标记定义准备就绪的回调函数。</span><span class="sxs-lookup"><span data-stu-id="3358e-369">Add the following code inside the **script** tag to define the ready callback function.</span></span>

    <span data-ttu-id="3358e-370">(代码段- *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)</span><span class="sxs-lookup"><span data-stu-id="3358e-370">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. <span data-ttu-id="3358e-371">将在光标**脚本**标记，然后按**CTRL** + **。**</span><span class="sxs-lookup"><span data-stu-id="3358e-371">Place the caret in the **script** tag and press **CTRL** + **.**</span></span> <span data-ttu-id="3358e-372">若要打开建议菜单。</span><span class="sxs-lookup"><span data-stu-id="3358e-372">to open the suggestion menu.</span></span>
4. <span data-ttu-id="3358e-373">单击**提取到文件**。</span><span class="sxs-lookup"><span data-stu-id="3358e-373">Click **Extract To File**.</span></span>

    <span data-ttu-id="3358e-374">![JavaScript 将解压缩到文件的建议](visual-studio-2013-web-tools/_static/image39.png "JavaScript 提取到文件的建议")</span><span class="sxs-lookup"><span data-stu-id="3358e-374">![JavaScript extract to file suggestion](visual-studio-2013-web-tools/_static/image39.png "JavaScript extract to file suggestion")</span></span>

    <span data-ttu-id="3358e-375">*JavaScript 将解压缩到文件的建议*</span><span class="sxs-lookup"><span data-stu-id="3358e-375">*JavaScript extract to file suggestion*</span></span>
5. <span data-ttu-id="3358e-376">在中**另存为**窗口中，选择**脚本**文件夹中，将文件命名**init.js**然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="3358e-376">In the **Save As** window, select the **Scripts** folder, name the file **init.js** and click **Save**.</span></span>

    <span data-ttu-id="3358e-377">![另存为窗口](visual-studio-2013-web-tools/_static/image40.png "另存为窗口")</span><span class="sxs-lookup"><span data-stu-id="3358e-377">![Save As window](visual-studio-2013-web-tools/_static/image40.png "Save As window")</span></span>

    <span data-ttu-id="3358e-378">*另存为窗口*</span><span class="sxs-lookup"><span data-stu-id="3358e-378">*Save As window*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3358e-379">**Init.js**创建文件和脚本的内容移动到文件。</span><span class="sxs-lookup"><span data-stu-id="3358e-379">The **init.js** file is created and the content of the script is moved to the file.</span></span>
    > 
    > <span data-ttu-id="3358e-380">![使用包含的内容创建 Init.js 文件](visual-studio-2013-web-tools/_static/image41.png "Init.js 文件包含的内容创建")</span><span class="sxs-lookup"><span data-stu-id="3358e-380">![Init.js file created with the content included](visual-studio-2013-web-tools/_static/image41.png "Init.js file created with the content included")</span></span>
    > 
    > <span data-ttu-id="3358e-381">*使用包含的内容创建 Init.js 文件*</span><span class="sxs-lookup"><span data-stu-id="3358e-381">*Init.js file created with the content included*</span></span>
6. <span data-ttu-id="3358e-382">打开**Index.cshtml**文件，然后检查脚本标记被替换的引用**init.js**文件。</span><span class="sxs-lookup"><span data-stu-id="3358e-382">Open the **Index.cshtml** file and check that the script tag was replaced with a reference to the **init.js** file.</span></span>

    <span data-ttu-id="3358e-383">![Init.js html 引用](visual-studio-2013-web-tools/_static/image42.png "Init.js html 引用")</span><span class="sxs-lookup"><span data-stu-id="3358e-383">![Init.js html reference](visual-studio-2013-web-tools/_static/image42.png "Init.js html reference")</span></span>

    <span data-ttu-id="3358e-384">*Init.js html 引用*</span><span class="sxs-lookup"><span data-stu-id="3358e-384">*Init.js html reference*</span></span>
7. <span data-ttu-id="3358e-385">转到**解决方案资源管理器**您会发现**init.js**文件已自动包含在解决方案中。</span><span class="sxs-lookup"><span data-stu-id="3358e-385">Go to the **Solution Explorer** and notice that the **init.js** file was included automatically in the solution.</span></span>

    <span data-ttu-id="3358e-386">![Init.js 文件包含在解决方案中](visual-studio-2013-web-tools/_static/image43.png "Init.js 文件包含在解决方案中")</span><span class="sxs-lookup"><span data-stu-id="3358e-386">![Init.js file included in solution](visual-studio-2013-web-tools/_static/image43.png "Init.js file included in solution")</span></span>

    <span data-ttu-id="3358e-387">*Init.js 文件包含在解决方案中*</span><span class="sxs-lookup"><span data-stu-id="3358e-387">*Init.js file included in solution*</span></span>
8. <span data-ttu-id="3358e-388">切换回**init.js**文件以更新**准备**函数回调。</span><span class="sxs-lookup"><span data-stu-id="3358e-388">Switch back to the **init.js** file to update the **ready** function callback.</span></span>
9. <span data-ttu-id="3358e-389">在传递给函数回调定义*准备*，添加以下代码可以通过特定的类属性中获取所有元素。</span><span class="sxs-lookup"><span data-stu-id="3358e-389">Inside the function callback definition that is passed to *ready*, add the following code to get all the elements by a specific class attribute.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. <span data-ttu-id="3358e-390">按**CTRL** + **空间**内部引号之间**getElementsByClassName**函数调用。</span><span class="sxs-lookup"><span data-stu-id="3358e-390">Press **CTRL** + **Space** between the quotes inside the **getElementsByClassName** function call.</span></span>

    <span data-ttu-id="3358e-391">![GetElementsByClassName 函数显示 IntelliSense](visual-studio-2013-web-tools/_static/image44.png "getElementsByClassName 函数显示 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="3358e-391">![Showing IntelliSense for the getElementsByClassName function](visual-studio-2013-web-tools/_static/image44.png "Showing IntelliSense for the getElementsByClassName function")</span></span>

    <span data-ttu-id="3358e-392">*显示 IntelliSense getElementsByClassName 函数*</span><span class="sxs-lookup"><span data-stu-id="3358e-392">*Showing IntelliSense for the getElementsByClassName function*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3358e-393">请注意，IntelliSense 会显示项目样式表中定义的类。</span><span class="sxs-lookup"><span data-stu-id="3358e-393">Notice that IntelliSense shows the classes defined in the project style sheets.</span></span>
11. <span data-ttu-id="3358e-394">已使用以下代码创建的行替换为。</span><span class="sxs-lookup"><span data-stu-id="3358e-394">Replace the line that you have created with the following code.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. <span data-ttu-id="3358e-395">之后将光标置于**au**在引号内**getElementsByTagName**函数，并按**CTRL** + **空间**.</span><span class="sxs-lookup"><span data-stu-id="3358e-395">Position the cursor after **au** inside the quotes in the **getElementsByTagName** function and press **CTRL** + **Space**.</span></span>

    <span data-ttu-id="3358e-396">![GetElementByTagName 方法显示 IntelliSense](visual-studio-2013-web-tools/_static/image45.png "getElementByTagName 方法显示 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="3358e-396">![Showing IntelliSense for the getElementByTagName method](visual-studio-2013-web-tools/_static/image45.png "Showing IntelliSense for the getElementByTagName method")</span></span>

    <span data-ttu-id="3358e-397">*GetElementsByTagName 方法显示 IntelliSense*</span><span class="sxs-lookup"><span data-stu-id="3358e-397">*Showing IntelliSense for the getElementsByTagName method*</span></span>
13. <span data-ttu-id="3358e-398">选择**&quot;音频&quot;** 列表然后按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="3358e-398">Select **&quot;audio&quot;** from the list and press **ENTER**.</span></span> <span data-ttu-id="3358e-399">结果如下图所示。</span><span class="sxs-lookup"><span data-stu-id="3358e-399">The result is shown in the following figure.</span></span>

    <span data-ttu-id="3358e-400">![检索音频元素](visual-studio-2013-web-tools/_static/image46.png "检索音频元素")</span><span class="sxs-lookup"><span data-stu-id="3358e-400">![Retrieving Audio Elements](visual-studio-2013-web-tools/_static/image46.png "Retrieving Audio Elements")</span></span>

    <span data-ttu-id="3358e-401">*检索音频元素*</span><span class="sxs-lookup"><span data-stu-id="3358e-401">*Retrieving Audio Elements*</span></span>
14. <span data-ttu-id="3358e-402">在中**解决方案资源管理器**，右键单击**init.js**文件中**脚本**文件夹，然后选择**缩小 JavaScript 文件**从**Web Essentials**菜单。</span><span class="sxs-lookup"><span data-stu-id="3358e-402">In **Solution Explorer**, right-click the **init.js** file in the **Scripts** folder and select **Minify JavaScript file(s)** from the **Web Essentials** menu.</span></span>

    <span data-ttu-id="3358e-403">![缩小 JavaScript 文件](visual-studio-2013-web-tools/_static/image47.png "缩小 JavaScript 文件")</span><span class="sxs-lookup"><span data-stu-id="3358e-403">![Minify JavaScript file(s)](visual-studio-2013-web-tools/_static/image47.png "Minify JavaScript files")</span></span>

    <span data-ttu-id="3358e-404">*缩小 JavaScript 文件*</span><span class="sxs-lookup"><span data-stu-id="3358e-404">*Minify JavaScript file(s)*</span></span>
15. <span data-ttu-id="3358e-405">当系统提示你单击源文件更改时启用自动缩减**是**。</span><span class="sxs-lookup"><span data-stu-id="3358e-405">When prompted to enable automatic minification when the source file changes click **Yes**.</span></span>

    <span data-ttu-id="3358e-406">![启用自动缩小警告](visual-studio-2013-web-tools/_static/image48.png "启用自动缩小警告")</span><span class="sxs-lookup"><span data-stu-id="3358e-406">![Enabling automatic minification warning](visual-studio-2013-web-tools/_static/image48.png "Enabling automatic minification warning")</span></span>

    <span data-ttu-id="3358e-407">*启用自动缩小警告*</span><span class="sxs-lookup"><span data-stu-id="3358e-407">*Enabling automatic minification warning*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3358e-408">**Init.min.js**将创建并添加作为的依赖项**init.js**文件。</span><span class="sxs-lookup"><span data-stu-id="3358e-408">The **init.min.js** is created and is added as a dependency of the **init.js** file.</span></span>
    > 
    > <span data-ttu-id="3358e-409">![创建 Init.min.js 文件](visual-studio-2013-web-tools/_static/image49.png "Init.min.js 文件创建")</span><span class="sxs-lookup"><span data-stu-id="3358e-409">![Init.min.js file created](visual-studio-2013-web-tools/_static/image49.png "Init.min.js file created")</span></span>
    > 
    > <span data-ttu-id="3358e-410">*创建 Init.min.js 文件*</span><span class="sxs-lookup"><span data-stu-id="3358e-410">*Init.min.js file created*</span></span>
16. <span data-ttu-id="3358e-411">打开**init.min.js**文件，请注意，缩小该文件。</span><span class="sxs-lookup"><span data-stu-id="3358e-411">Open the **init.min.js** file and notice that the file is minified.</span></span>

    <span data-ttu-id="3358e-412">![Init.min.js 文件内容](visual-studio-2013-web-tools/_static/image50.png "Init.min.js 文件内容")</span><span class="sxs-lookup"><span data-stu-id="3358e-412">![Init.min.js file content](visual-studio-2013-web-tools/_static/image50.png "Init.min.js file content")</span></span>

    <span data-ttu-id="3358e-413">*Init.min.js 文件内容*</span><span class="sxs-lookup"><span data-stu-id="3358e-413">*Init.min.js file content*</span></span>
17. <span data-ttu-id="3358e-414">在中**init.js**文件中，添加以下代码**getElementsByTagName**函数调用播放音频的所有元素。</span><span class="sxs-lookup"><span data-stu-id="3358e-414">In the **init.js** file, add the following code below the **getElementsByTagName** function call to play all the audio elements.</span></span>

    <span data-ttu-id="3358e-415">(代码段- *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*)</span><span class="sxs-lookup"><span data-stu-id="3358e-415">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*)</span></span>

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. <span data-ttu-id="3358e-416">单击**CTRL** + **S**保存该文件。</span><span class="sxs-lookup"><span data-stu-id="3358e-416">Click **CTRL** + **S** to save the file.</span></span> <span data-ttu-id="3358e-417">由于缩小的文件已打开，您将看到对话框，指出，源编辑器外修改该文件。</span><span class="sxs-lookup"><span data-stu-id="3358e-417">Since the minified file is already opened, you will see a dialog box saying that the file was modified outside of the source editor.</span></span> <span data-ttu-id="3358e-418">单击 **“是”**。</span><span class="sxs-lookup"><span data-stu-id="3358e-418">Click **Yes**.</span></span>

    <span data-ttu-id="3358e-419">![Microsoft Visual Studio 警告](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 警告")</span><span class="sxs-lookup"><span data-stu-id="3358e-419">![Microsoft Visual Studio warning](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="3358e-420">*Microsoft Visual Studio 警告*</span><span class="sxs-lookup"><span data-stu-id="3358e-420">*Microsoft Visual Studio warning*</span></span>
19. <span data-ttu-id="3358e-421">切换回**init.min.js**文件以验证该文件已更新使用新的代码。</span><span class="sxs-lookup"><span data-stu-id="3358e-421">Switch back to the **init.min.js** file to verify that the file was updated with the new code.</span></span>

    <span data-ttu-id="3358e-422">![Init.min.js 文件已更新](visual-studio-2013-web-tools/_static/image52.png "Init.min.js 文件已更新")</span><span class="sxs-lookup"><span data-stu-id="3358e-422">![Init.min.js file updated](visual-studio-2013-web-tools/_static/image52.png "Init.min.js file updated")</span></span>

    <span data-ttu-id="3358e-423">*Init.min.js 文件已更新*</span><span class="sxs-lookup"><span data-stu-id="3358e-423">*Init.min.js file updated*</span></span>
20. <span data-ttu-id="3358e-424">单击**浏览器链接刷新**按钮。</span><span class="sxs-lookup"><span data-stu-id="3358e-424">Click the **Browser Link Refresh** button.</span></span>
21. <span data-ttu-id="3358e-425">后两个浏览器会刷新在上一任务中看到的音频播放机将开始自动播放。</span><span class="sxs-lookup"><span data-stu-id="3358e-425">Once both browsers are refreshed the audio players you saw in the previous task will start playing automatically.</span></span>

    <span data-ttu-id="3358e-426">![视图中包含的音频播放器](visual-studio-2013-web-tools/_static/image53.png "视图中包含的音频播放机")</span><span class="sxs-lookup"><span data-stu-id="3358e-426">![Audio player included in view](visual-studio-2013-web-tools/_static/image53.png "Audio player included in view")</span></span>

    <span data-ttu-id="3358e-427">*视图中包含的音频播放器*</span><span class="sxs-lookup"><span data-stu-id="3358e-427">*Audio player included in view*</span></span>

* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="3358e-428">总结</span><span class="sxs-lookup"><span data-stu-id="3358e-428">Summary</span></span>

<span data-ttu-id="3358e-429">通过完成本动手实验介绍了如何：</span><span class="sxs-lookup"><span data-stu-id="3358e-429">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="3358e-430">使用新的 HTML 编辑器功能，这些功能包含在 Web Essentials 等丰富的 HTML5 代码代码段和处理编码</span><span class="sxs-lookup"><span data-stu-id="3358e-430">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="3358e-431">使用颜色选取器和浏览器矩阵工具提示等 Web Essentials 中包括的新 CSS 编辑器功能</span><span class="sxs-lookup"><span data-stu-id="3358e-431">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="3358e-432">使用 Web Essentials 等中提取到文件和智能感知中包括的所有 HTML 元素的新 JavaScript 编辑器功能</span><span class="sxs-lookup"><span data-stu-id="3358e-432">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="3358e-433">你的浏览器和 Visual Studio 中使用浏览器链接之间交换数据</span><span class="sxs-lookup"><span data-stu-id="3358e-433">Exchange data between your browser and Visual Studio using Browser Link</span></span>
