---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: ASP.NET 和 Visual Studio 2012 中的 Web 开发的新增功能 |Microsoft 文档
author: rick-anderson
description: Visual Studio 的新版本引入了一些增强功能集中于改进的体验和性能，使用 Web 技术时...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: f447dc0108dffb36ed6d627fb83b3117fd22c94c
ms.sourcegitcommit: 3a893ae05f010656d99d6ddf55e82f1b5b6933bc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/18/2018
ms.locfileid: "34306827"
---
<a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a><span data-ttu-id="87185-103">ASP.NET 和 Visual Studio 2012 中的 Web 开发的新增功能</span><span class="sxs-lookup"><span data-stu-id="87185-103">What's New in ASP.NET and Web Development in Visual Studio 2012</span></span>
====================
<span data-ttu-id="87185-104">通过[Web 营地团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="87185-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="87185-105">Visual Studio 的新版本引入了一些增强功能集中于改进的体验和性能，当使用 Web 技术。</span><span class="sxs-lookup"><span data-stu-id="87185-105">The new version of Visual Studio introduces a number of enhancements focused on improving the experience and performance when working with Web technologies.</span></span> <span data-ttu-id="87185-106">CSS、 JavaScript 和 HTML 的 visual Studio 编辑器已彻底改观，以包括许多最需代码指导，例如智能感知和自动缩进。</span><span class="sxs-lookup"><span data-stu-id="87185-106">Visual Studio Editors for CSS, JavaScript and HTML have been completely revamped to include many of the most in-demand code aids, such as IntelliSense and automatic indentation.</span></span> <span data-ttu-id="87185-107">至于性能方面，如内置功能，以便轻松地将减少页加载时间，则现已集成绑定和缩减。</span><span class="sxs-lookup"><span data-stu-id="87185-107">Regarding performance, bundling and minification are now integrated as built-in features to easily reduce page load time.</span></span>
> 
> <span data-ttu-id="87185-108">Visual Studio，可使用最新的网站技术。</span><span class="sxs-lookup"><span data-stu-id="87185-108">Visual Studio enables you to work with the latest website technologies.</span></span> <span data-ttu-id="87185-109">可以使用跨浏览器 CSS3 片段以确保你的站点工作不考虑客户端平台，同时还利用新的 HTML5 元素和功能。</span><span class="sxs-lookup"><span data-stu-id="87185-109">You can use cross-browser CSS3 Snippets to make sure your site works regardless of the client platform while also taking advantage of the new HTML5 elements and features.</span></span>
> 
> <span data-ttu-id="87185-110">编写和分析 JavaScript 代码应为此 Visual Studio 版本，更容易。</span><span class="sxs-lookup"><span data-stu-id="87185-110">Writing and profiling JavaScript code should be easier with this Visual Studio version.</span></span> <span data-ttu-id="87185-111">智能感知列表集成的 XML 文档和导航功能现可用于 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="87185-111">IntelliSense lists, integrated XML documentation and navigation features are now available for JavaScript code.</span></span> <span data-ttu-id="87185-112">你现在可以在您能够轻松利用的 JavaScript 目录。</span><span class="sxs-lookup"><span data-stu-id="87185-112">You now have the JavaScript catalog at your fingertips.</span></span> <span data-ttu-id="87185-113">此外，你可以检查 ECMAScript5 符合你的脚本，并在早期阶段检测语法错误。</span><span class="sxs-lookup"><span data-stu-id="87185-113">Additionally, you can check ECMAScript5 compliance with your scripts and detect syntax errors at an early stage.</span></span>
> 
> <span data-ttu-id="87185-114">上次值得一提的但此 Visual Studio 版本可实现内置绑定和缩减。</span><span class="sxs-lookup"><span data-stu-id="87185-114">Last but not least, this Visual Studio version implements built-in bundling and minification.</span></span> <span data-ttu-id="87185-115">你的脚本文件和样式表将打包和压缩，以便站点执行速度更快。</span><span class="sxs-lookup"><span data-stu-id="87185-115">Your script files and style sheets will be packed and compressed so that the site performs faster.</span></span>
> 
> <span data-ttu-id="87185-116">此实验室将引导你完成的增强功能和前面所述通过将细微的更改应用于源文件夹中提供的示例 Web 应用程序的新功能。</span><span class="sxs-lookup"><span data-stu-id="87185-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="87185-117">在 Web 营地培训工具包中，在包括所有的示例代码和代码段[ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="87185-117">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="87185-118">目标</span><span class="sxs-lookup"><span data-stu-id="87185-118">Objectives</span></span>

<span data-ttu-id="87185-119">在此动手实验中，你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="87185-119">In this hands on lab, you will learn how to:</span></span>

- <span data-ttu-id="87185-120">在 CSS 编辑器中使用的新功能和改进</span><span class="sxs-lookup"><span data-stu-id="87185-120">Use the new features and improvements in the CSS editor</span></span>
- <span data-ttu-id="87185-121">在 HTML 编辑器中使用的新功能和改进</span><span class="sxs-lookup"><span data-stu-id="87185-121">Use the new features and improvements in the HTML editor</span></span>
- <span data-ttu-id="87185-122">在 JavaScript 编辑器中使用的新功能和改进</span><span class="sxs-lookup"><span data-stu-id="87185-122">Use the new features and improvements in the JavaScript editor</span></span>
- <span data-ttu-id="87185-123">配置和使用绑定和缩减</span><span class="sxs-lookup"><span data-stu-id="87185-123">Configure and use bundling and minification</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="87185-124">系统必备</span><span class="sxs-lookup"><span data-stu-id="87185-124">Prerequisites</span></span>

- <span data-ttu-id="87185-125">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="87185-125">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="87185-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) （适用于安装程序脚本-已安装在 Windows 8 和 Windows Server 2008 R2）</span><span class="sxs-lookup"><span data-stu-id="87185-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (for setup scripts - already installed on Windows 8 and Windows Server 2008 R2)</span></span>
- <span data-ttu-id="87185-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) -或 HTML5 符合浏览器</span><span class="sxs-lookup"><span data-stu-id="87185-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) - or an HTML5 compliant browser</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="87185-128">练习</span><span class="sxs-lookup"><span data-stu-id="87185-128">Exercises</span></span>

<span data-ttu-id="87185-129">此动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="87185-129">This hands on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="87185-130">练习 1： 什么是 CSS 编辑器中的新增功能</span><span class="sxs-lookup"><span data-stu-id="87185-130">Exercise 1: What's New in the CSS Editor</span></span>](#Exercise1)
2. [<span data-ttu-id="87185-131">练习 2： 什么是新的 HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="87185-131">Exercise 2: What's New in the HTML Editor</span></span>](#Exercise2)
3. [<span data-ttu-id="87185-132">练习 3： 什么是 JavaScript 编辑器中的新增功能</span><span class="sxs-lookup"><span data-stu-id="87185-132">Exercise 3: What's New in the JavaScript Editor</span></span>](#Exercise3)
4. [<span data-ttu-id="87185-133">练习 4： 捆绑和缩减</span><span class="sxs-lookup"><span data-stu-id="87185-133">Exercise 4: Bundling and Minification</span></span>](#Exercise4)

<span data-ttu-id="87185-134">估计时间来完成该实验： **60 分钟**。</span><span class="sxs-lookup"><span data-stu-id="87185-134">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a><span data-ttu-id="87185-135">练习 1： 什么是 CSS 编辑器中的新增功能</span><span class="sxs-lookup"><span data-stu-id="87185-135">Exercise 1: What's New in the CSS Editor</span></span>

<span data-ttu-id="87185-136">Web 开发人员应熟悉许多与 CSS 编辑相关的困难。</span><span class="sxs-lookup"><span data-stu-id="87185-136">Web developers should be familiar with many of the difficulties related to CSS editing.</span></span> <span data-ttu-id="87185-137">CSS 样式的最大问题之一是跨浏览器兼容性。</span><span class="sxs-lookup"><span data-stu-id="87185-137">One of the biggest issues of CSS styling is cross-browser compatibility.</span></span> <span data-ttu-id="87185-138">经常会出现，将样式应用到你的站点之后, 它看起来不同，如果你发现你在其他浏览器或设备中打开它。</span><span class="sxs-lookup"><span data-stu-id="87185-138">It often happens that, after applying styles to your site, you notice that it looks different if you open it in another browser or device.</span></span> <span data-ttu-id="87185-139">因此，你可能在修复这些 visual 的问题，以实现，当你最后使其在浏览器，它会拆分中其他花费相当长的时间。</span><span class="sxs-lookup"><span data-stu-id="87185-139">Therefore, you may spend a considerable time on fixing those visual issues to realize that, when you finally make it work in one browser, it is broken in the others.</span></span>

<span data-ttu-id="87185-140">Visual Studio 现在包含功能，可帮助开发人员访问、 工作和有效地组织 CSS 样式表。</span><span class="sxs-lookup"><span data-stu-id="87185-140">Visual Studio now includes features that help developers access, work and organize CSS style sheets effectively.</span></span> <span data-ttu-id="87185-141">在本练习中，将满足的新功能为有效的组织和版本，以及跨浏览器兼容性 CSS3 代码段。</span><span class="sxs-lookup"><span data-stu-id="87185-141">Throughout this exercise, you will meet the new features for an effective organization and edition, as well as the CSS3 Code Snippets for cross-browser compatibility.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a><span data-ttu-id="87185-142">任务 1-新的编辑器功能</span><span class="sxs-lookup"><span data-stu-id="87185-142">Task 1 - New Editor Features</span></span>

<span data-ttu-id="87185-143">在此任务中，你将发现的新功能的 CSS 编辑器中。</span><span class="sxs-lookup"><span data-stu-id="87185-143">In this task, you will discover the new features of the CSS Editor.</span></span> <span data-ttu-id="87185-144">此新的编辑器将帮助你提高工作效率，通过利用新的智能缩进、 改进的代码注释和增强的智能感知列表。</span><span class="sxs-lookup"><span data-stu-id="87185-144">This new editor will help you increase your productivity by taking advantage of the new smart indentation, the improved code comments and the enhanced IntelliSense list.</span></span>

1. <span data-ttu-id="87185-145">启动**Visual Studio**并打开**WhatsNewASPNET.sln**解决方案位于**Source\WhatsNewASPNET**这个实验室的文件夹。</span><span class="sxs-lookup"><span data-stu-id="87185-145">Start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="87185-146">在解决方案资源管理器，打开**Site.css**文件位于**样式**文件夹。</span><span class="sxs-lookup"><span data-stu-id="87185-146">In Solution Explorer, open the **Site.css** file located under the **Styles** folder.</span></span> <span data-ttu-id="87185-147">请确保**文本编辑器**工具是在工具栏上可见。</span><span class="sxs-lookup"><span data-stu-id="87185-147">Make sure the **Text Editor** tools are visible on the toolbar.</span></span> <span data-ttu-id="87185-148">为此，请选择**视图** | **工具栏**菜单选项，并检查**文本编辑器**选项。</span><span class="sxs-lookup"><span data-stu-id="87185-148">To do that, select the **View** | **Toolbars** menu option, and check the **Text Editor** options.</span></span> <span data-ttu-id="87185-149">你将注意，此新版本，因为**注释**按钮 (![comment 按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png)) 和**取消注释**按钮 (![取消注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)) 也已启用了 CSS 编辑器。</span><span class="sxs-lookup"><span data-stu-id="87185-149">You will notice that, since this new version, the **Comment** button (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png) ) and the **Uncomment** button (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png) ) are also enabled for the CSS editor.</span></span>

    <span data-ttu-id="87185-150">![启用编辑器和 CSS 工具](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "启用编辑器和 CSS 工具")</span><span class="sxs-lookup"><span data-stu-id="87185-150">![Enabling Editor and CSS Tools](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "Enabling Editor and CSS Tools")</span></span>

    <span data-ttu-id="87185-151">*启用编辑器和 CSS 工具*</span><span class="sxs-lookup"><span data-stu-id="87185-151">*Enabling Editor and CSS Tools*</span></span>
3. <span data-ttu-id="87185-152">滚动代码并选择任意 CSS 类定义。</span><span class="sxs-lookup"><span data-stu-id="87185-152">Scroll the code and select any CSS class definition.</span></span> <span data-ttu-id="87185-153">单击**注释**(![comment 按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)) 按钮以注释所选的行。</span><span class="sxs-lookup"><span data-stu-id="87185-153">Click the **Comment** (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png) ) button to comment the selected lines.</span></span> <span data-ttu-id="87185-154">然后，单击**取消注释**(![取消注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png)) 按钮以还原所做的更改。</span><span class="sxs-lookup"><span data-stu-id="87185-154">Then, click the **Uncomment** (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png) ) button to undo the changes.</span></span>
4. <span data-ttu-id="87185-155">单击**折叠**(![折叠](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png)) 和**展开**(![展开](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png)) 按钮位于文本的左边距。</span><span class="sxs-lookup"><span data-stu-id="87185-155">Click the **Collapse** (![collapse](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) ) and **Expand** (![expand](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) ) buttons located on the left margin of the text.</span></span> <span data-ttu-id="87185-156">请注意，您现在可以隐藏不使用具有更简洁的视图的样式。</span><span class="sxs-lookup"><span data-stu-id="87185-156">Notice that you can now hide the styles you don't use to have a cleaner view.</span></span>

    <span data-ttu-id="87185-157">![折叠 CSS 类](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "折叠 CSS 类")</span><span class="sxs-lookup"><span data-stu-id="87185-157">![Collapsing CSS classes](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "Collapsing CSS classes")</span></span>

    <span data-ttu-id="87185-158">*折叠 CSS 类*</span><span class="sxs-lookup"><span data-stu-id="87185-158">*Collapsing CSS classes*</span></span>
5. <span data-ttu-id="87185-159">请确保启用了智能缩进功能。</span><span class="sxs-lookup"><span data-stu-id="87185-159">Make sure that the smart indentation feature is enabled.</span></span> <span data-ttu-id="87185-160">选择**工具** | **选项**菜单选项，然后选择**文本编辑器** | **CSS**  | **格式**屏幕的左窗格中的页。</span><span class="sxs-lookup"><span data-stu-id="87185-160">Select the **Tools** | **Options** menu option, and then select the **Text Editor** | **CSS** | **Formatting** page in the left pane of the screen.</span></span> <span data-ttu-id="87185-161">检查**分层缩进**选项。</span><span class="sxs-lookup"><span data-stu-id="87185-161">Check the **Hierarchical indentation** option.</span></span>

    <span data-ttu-id="87185-162">![启用分层缩进](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "启用分层缩进")</span><span class="sxs-lookup"><span data-stu-id="87185-162">![Enabling hierarchical indentation](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "Enabling hierarchical indentation")</span></span>

    <span data-ttu-id="87185-163">*启用分层缩进*</span><span class="sxs-lookup"><span data-stu-id="87185-163">*Enabling hierarchical indentation*</span></span>
6. <span data-ttu-id="87185-164">找到的主类定义 (.main) 并追加到的 div 元素的样式。</span><span class="sxs-lookup"><span data-stu-id="87185-164">Locate the main class definition (.main) and append a style to the div elements.</span></span> <span data-ttu-id="87185-165">你将注意到代码将自动，对齐帮助用户查找父级类一目了然。</span><span class="sxs-lookup"><span data-stu-id="87185-165">You will notice that the code aligns automatically, helping users to find the parent classes at a glance.</span></span>

    <span data-ttu-id="87185-166">CSS</span><span class="sxs-lookup"><span data-stu-id="87185-166">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    <span data-ttu-id="87185-167">![在 CSS 层次结构的对齐方式](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS 中的层次结构对齐方式")</span><span class="sxs-lookup"><span data-stu-id="87185-167">![Hierarchical alignment in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "Hierarchical alignment in CSS")</span></span>

    <span data-ttu-id="87185-168">*在 CSS 层次结构的对齐方式*</span><span class="sxs-lookup"><span data-stu-id="87185-168">*Hierarchical alignment in CSS*</span></span>
7. <span data-ttu-id="87185-169">内部 **.main div**类，在末尾找到光标**边框： 0px;** 按**Enter**以显示 IntelliSense 列表。</span><span class="sxs-lookup"><span data-stu-id="87185-169">Inside **.main div** class, locate the cursor at the end of **border: 0px;** and press **Enter** to display the IntelliSense list.</span></span> <span data-ttu-id="87185-170">开始键入**顶部**，并注意你进行键入筛选列表的方式。</span><span class="sxs-lookup"><span data-stu-id="87185-170">Start typing **top** and notice how the list is filtered as you type.</span></span> <span data-ttu-id="87185-171">该列表将显示包含的元素**顶部**在 word 的任何部分 (在以前版本的 Visual Studio 中，对列表进行筛选的项，*开始*一词的)。</span><span class="sxs-lookup"><span data-stu-id="87185-171">The list will display the elements that contain **top** at any part of the word (In prior versions of Visual Studio, the list is filtered by the items that *begin* with the term).</span></span>

    <span data-ttu-id="87185-172">![在 CSS 中的 IntelliSense 增强功能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS 中的 IntelliSense 增强功能")</span><span class="sxs-lookup"><span data-stu-id="87185-172">![IntelliSense enhancements in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "IntelliSense enhancements in CSS")</span></span>

    <span data-ttu-id="87185-173">*在 CSS 中的 IntelliSense 增强功能*</span><span class="sxs-lookup"><span data-stu-id="87185-173">*IntelliSense enhancements in CSS*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a><span data-ttu-id="87185-174">任务 2-颜色选取器</span><span class="sxs-lookup"><span data-stu-id="87185-174">Task 2 - The Color Picker</span></span>

<span data-ttu-id="87185-175">在此任务中，你会发现新的 CSS 颜色选取器集成到 Visual Studio IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="87185-175">In this task, you will discover the new CSS Color Picker integrated into Visual Studio IntelliSense.</span></span>

1. <span data-ttu-id="87185-176">在**Site.css，** 找到标头类定义 (.header) 并将光标放在旁边**背景色**特性，之间&quot;:&quot;和&quot; #&quot;上的代码行的字符 **。**</span><span class="sxs-lookup"><span data-stu-id="87185-176">In **Site.css,** locate the header class definition (.header) and place the cursor next to **background-color** attribute, between the &quot;:&quot; and &quot;#&quot; characters on that line of code **.**</span></span>

    <span data-ttu-id="87185-177">![定位光标](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "定位光标")</span><span class="sxs-lookup"><span data-stu-id="87185-177">![Locating the cursor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "Locating the cursor")</span></span>

    <span data-ttu-id="87185-178">*定位游标*</span><span class="sxs-lookup"><span data-stu-id="87185-178">*Locating the cursor*</span></span>
2. <span data-ttu-id="87185-179">删除**冒号**（:） 并将其再次以显示颜色选取器写入。</span><span class="sxs-lookup"><span data-stu-id="87185-179">Delete the **colon** (:) and write it again to display the color picker.</span></span> <span data-ttu-id="87185-180">请注意，你将看到的第一个颜色是你的站点的最常见颜色。</span><span class="sxs-lookup"><span data-stu-id="87185-180">Notice that the first colors you will see are the most frequent colors of your site.</span></span> <span data-ttu-id="87185-181">如果你单击白色的颜色，其 HTML 颜色代码 (#fff) 会替换样式表中的当前颜色代码。</span><span class="sxs-lookup"><span data-stu-id="87185-181">If you click the white color, its HTML color code (#fff) will replace the current color code in the stylesheet.</span></span>

    <span data-ttu-id="87185-182">![颜色选取器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "颜色选取器")</span><span class="sxs-lookup"><span data-stu-id="87185-182">![Color picker](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Color picker")</span></span>

    <span data-ttu-id="87185-183">*颜色选取器*</span><span class="sxs-lookup"><span data-stu-id="87185-183">*Color picker*</span></span>
3. <span data-ttu-id="87185-184">按**展开**(![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png) ) 以显示的颜色渐变，然后拖动要选择不同的颜色的渐变光标颜色选取器上的按钮。</span><span class="sxs-lookup"><span data-stu-id="87185-184">Press the **Expand** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png) ) button on the color picker to display the color gradient, and then drag the gradient cursor to select a different color.</span></span> <span data-ttu-id="87185-185">之后，单击**取色器**按钮，然后从屏幕中选择任意颜色。</span><span class="sxs-lookup"><span data-stu-id="87185-185">After that, click the **Eyedropper** button and select any color from the screen.</span></span> <span data-ttu-id="87185-186">请注意，背景颜色值动态更改移动光标时。</span><span class="sxs-lookup"><span data-stu-id="87185-186">Notice that background color value changes dynamically while you move the cursor.</span></span>

    <span data-ttu-id="87185-187">![颜色选取器渐变](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "颜色选取器渐变")</span><span class="sxs-lookup"><span data-stu-id="87185-187">![Color picker gradient](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "Color picker gradient")</span></span>

    <span data-ttu-id="87185-188">*颜色选取器渐变*</span><span class="sxs-lookup"><span data-stu-id="87185-188">*Color picker gradient*</span></span>
4. <span data-ttu-id="87185-189">在**不透明度**滑块，将选择器移到的栏，以减少不透明度的中心。</span><span class="sxs-lookup"><span data-stu-id="87185-189">In the **Opacity** slider, move the selector to the center of the bar to reduce the opacity.</span></span> <span data-ttu-id="87185-190">请注意，背景颜色值现在变为其刻度 RGBA。</span><span class="sxs-lookup"><span data-stu-id="87185-190">Notice that background-color value now changes its scale to RGBA.</span></span>

    <span data-ttu-id="87185-191">![颜色选取器不透明度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "颜色选取器不透明度")</span><span class="sxs-lookup"><span data-stu-id="87185-191">![Color picker Opacity](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "Color picker Opacity")</span></span>

    <span data-ttu-id="87185-192">*颜色选取器不透明度*</span><span class="sxs-lookup"><span data-stu-id="87185-192">*Color picker Opacity*</span></span>

    > [!NOTE]
    > <span data-ttu-id="87185-193">CSS3 中的 RGBA （红色、 绿色，蓝色、 Alpha） 颜色定义可以定义单个项的颜色不透明度值。</span><span class="sxs-lookup"><span data-stu-id="87185-193">The RGBA (Red, Green, Blue, Alpha) color definition in CSS3 enables you to define the color opacity value for a single item.</span></span> <span data-ttu-id="87185-194">与不同**不透明度-** 类似的 CSS 属性**-** RGBA 颜色也是最新的浏览器与兼容。</span><span class="sxs-lookup"><span data-stu-id="87185-194">Unlike **opacity -** a similar CSS attribute **-** RGBA colors are also compatible with the latest browsers.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a><span data-ttu-id="87185-195">任务 3-CSS 兼容的代码段</span><span class="sxs-lookup"><span data-stu-id="87185-195">Task 3 - CSS Compatible Code Snippets</span></span>

<span data-ttu-id="87185-196">在此任务中，你将了解如何使用跨浏览器兼容 CSS3 代码段以实现你的网站中的某些功能。</span><span class="sxs-lookup"><span data-stu-id="87185-196">In this task, you will learn how to use cross-browser compatible CSS3 snippets in order to implement some features in your website.</span></span>

1. <span data-ttu-id="87185-197">在**Site.css**文件中，找到**标头**CSS 类定义 (.header)，将以下光标 **/\*边框 radius\* /** 占位符，以添加新的代码段。</span><span class="sxs-lookup"><span data-stu-id="87185-197">In the **Site.css** file, locate the **header** CSS class definition (.header) and place the cursor below the **/\*border radius\*/** placeholder to add a new snippet.</span></span> <span data-ttu-id="87185-198">按**Enter**以显示类型以及智能感知列表**radius**以筛选列表。</span><span class="sxs-lookup"><span data-stu-id="87185-198">Press **Enter** to display the IntelliSense list and type **radius** to filter the list.</span></span> <span data-ttu-id="87185-199">选择**边框 radius**从该列表与双击，选项，然后按**选项卡**键以插入代码段。</span><span class="sxs-lookup"><span data-stu-id="87185-199">Select the **border-radius** option from the list with a double click, and then press the **TAB** key to insert the snippet.</span></span> <span data-ttu-id="87185-200">然后，键入像素为单位，然后按 radius 大小**Enter**。</span><span class="sxs-lookup"><span data-stu-id="87185-200">Then, type a radius size in pixels and press **Enter**.</span></span> <span data-ttu-id="87185-201">例如，键入**15px**。</span><span class="sxs-lookup"><span data-stu-id="87185-201">For instance, type **15px**.</span></span>

    <span data-ttu-id="87185-202">添加的代码段 CSS3 属性将呈现在大多数的 HTML5 法规遵从性浏览器，包括 Mozilla 和基于 WebKit 浏览器中的圆角的边框。</span><span class="sxs-lookup"><span data-stu-id="87185-202">The CSS3 attributes added by the snippet will render rounded borders in most HTML5 compliance browsers, including Mozilla and WebKit-based browsers.</span></span>

    <span data-ttu-id="87185-203">![使用边框 radius 段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "使用边框 radius 段")</span><span class="sxs-lookup"><span data-stu-id="87185-203">![Using a border-radius snippet](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "Using a border-radius snippet")</span></span>

    <span data-ttu-id="87185-204">*使用边框 radius 段*</span><span class="sxs-lookup"><span data-stu-id="87185-204">*Using a border-radius snippet*</span></span>
2. <span data-ttu-id="87185-205">将相同的应用**边框**页样式 (.page) 中的代码段。</span><span class="sxs-lookup"><span data-stu-id="87185-205">Apply the same **border** snippets in the page style (.page).</span></span>

    <span data-ttu-id="87185-206">CSS</span><span class="sxs-lookup"><span data-stu-id="87185-206">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. <span data-ttu-id="87185-207">按**F5**运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="87185-207">Press **F5** to run the solution.</span></span> <span data-ttu-id="87185-208">请注意，每个页面现在已舍入边框。</span><span class="sxs-lookup"><span data-stu-id="87185-208">Notice that each page now has rounded borders.</span></span>

    <span data-ttu-id="87185-209">![圆角](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "圆角")</span><span class="sxs-lookup"><span data-stu-id="87185-209">![Rounded corners](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "Rounded corners")</span></span>

    <span data-ttu-id="87185-210">*圆的角*</span><span class="sxs-lookup"><span data-stu-id="87185-210">*Rounded corners*</span></span>
4. <span data-ttu-id="87185-211">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="87185-211">Close the browser and return to Visual Studio.</span></span>
5. <span data-ttu-id="87185-212">打开**Custom.css**文件位于**样式**文件夹并将光标置于**div.images ul li img**类定义。</span><span class="sxs-lookup"><span data-stu-id="87185-212">Open the **Custom.css** file located under the **Styles** folder and place the cursor inside **div.images ul li img** class definition.</span></span>
6. <span data-ttu-id="87185-213">按 enter 以显示 IntelliSense 列表中，类型**框阴影**按**选项卡**键两次以插入的类定义中的默认卷影代码段。</span><span class="sxs-lookup"><span data-stu-id="87185-213">Press enter to display the IntelliSense list, type **box-shadow** and press the **TAB** key twice to insert the default shadow code snippet inside the class definition.</span></span> <span data-ttu-id="87185-214">将卷影值设置为**10px 10px 5px #888**。</span><span class="sxs-lookup"><span data-stu-id="87185-214">Set the shadow values to **10px 10px 5px #888**.</span></span> <span data-ttu-id="87185-215">然后，键入**边框 radius**和插入代码段。</span><span class="sxs-lookup"><span data-stu-id="87185-215">Then, type **border-radius** and insert the code snippet.</span></span> <span data-ttu-id="87185-216">类型**15px**设置 radius 大小和按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="87185-216">Type **15px** to set radius size and press **ENTER**.</span></span>

    <span data-ttu-id="87185-217">![圆角与卷影](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "圆角与卷影")</span><span class="sxs-lookup"><span data-stu-id="87185-217">![Rounded corners with shadow](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "Rounded corners with shadow")</span></span>

    <span data-ttu-id="87185-218">*使用卷影圆的角*</span><span class="sxs-lookup"><span data-stu-id="87185-218">*Rounded corners with shadow*</span></span>

    > [!NOTE]
    > <span data-ttu-id="87185-219">此时，则使用相应的前缀 （moz、 易于使用的功能、 o） 以支持 Mozilla 和 Webkit (Chrome、 Safari，Konkeror) 浏览器中插入卷影属性。</span><span class="sxs-lookup"><span data-stu-id="87185-219">At this moment, the shadow attribute is inserted with the corresponding prefix (moz, webkit, o) to support Mozilla and Webkit (Chrome, Safari, Konkeror) browsers.</span></span>
7. <span data-ttu-id="87185-220">创建一个新类**div.images ul li img:hover**下面**div.images ul li img**类定义，并将光标置于括号 **。**</span><span class="sxs-lookup"><span data-stu-id="87185-220">Create a new class **div.images ul li img:hover** below the **div.images ul li img** class definition and place the cursor inside the brackets **.**</span></span>

    <span data-ttu-id="87185-221">CSS</span><span class="sxs-lookup"><span data-stu-id="87185-221">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. <span data-ttu-id="87185-222">类型**转换**按**选项卡**两次以插入转换代码段的密钥。</span><span class="sxs-lookup"><span data-stu-id="87185-222">Type **transform** and press the **TAB** key twice in order to insert the transform snippet.</span></span> <span data-ttu-id="87185-223">然后，输入**rotate(-15deg)** 图像光标悬停上时更改旋转角度值。</span><span class="sxs-lookup"><span data-stu-id="87185-223">Then, enter **rotate(-15deg)** to change the rotation angle value when images are hovered.</span></span>

    <span data-ttu-id="87185-224">CSS</span><span class="sxs-lookup"><span data-stu-id="87185-224">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. <span data-ttu-id="87185-225">按**F5**若要运行解决方案并浏览到 CSS3 页。</span><span class="sxs-lookup"><span data-stu-id="87185-225">Press **F5** to run the solution and browse to the CSS3 page.</span></span> <span data-ttu-id="87185-226">请注意，映像有了圆形角并框阴影。</span><span class="sxs-lookup"><span data-stu-id="87185-226">Notice that the images have rounded corners and box shadows.</span></span> <span data-ttu-id="87185-227">鼠标悬停的图像，并观察它们旋转。</span><span class="sxs-lookup"><span data-stu-id="87185-227">Hover the mouse over the images and watch them rotate.</span></span>

    <span data-ttu-id="87185-228">![转换旋转图像的代码段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "转换段旋转图像")</span><span class="sxs-lookup"><span data-stu-id="87185-228">![Transform snippet rotating an image](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "Transform snippet rotating an image")</span></span>

    <span data-ttu-id="87185-229">*转换旋转图像的代码段*</span><span class="sxs-lookup"><span data-stu-id="87185-229">*Transform snippet rotating an image*</span></span>

    > [!NOTE]
    > <span data-ttu-id="87185-230">如果你使用 Internet Explorer 10，并且无法看到阴影，请确保文档模式设置为 IE10 标准。</span><span class="sxs-lookup"><span data-stu-id="87185-230">If you are using Internet Explorer 10 and cannot see the shadows, make sure the document mode is set to IE10 standards.</span></span> <span data-ttu-id="87185-231">按**F12**若要打开 Internet Explorer 开发人员工具，然后单击**文档模式**更改为 IE10 标准。</span><span class="sxs-lookup"><span data-stu-id="87185-231">Press **F12** to open Internet Explorer developer tools and click **Document Mode** to change to IE10 standards.</span></span>

    ![有关-我们](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a><span data-ttu-id="87185-233">练习 2： 什么是新的 HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="87185-233">Exercise 2: What's New in the HTML Editor</span></span>

<span data-ttu-id="87185-234">Visual Studio 提供改进的 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="87185-234">Visual Studio has an improved HTML editor.</span></span> <span data-ttu-id="87185-235">某些包含在此版本中的增强功能是在 HTML 文档、 HTML5 代码段、 HTML 开始和结束标记匹配，和 HTML 验证智能缩进。</span><span class="sxs-lookup"><span data-stu-id="87185-235">Some of the enhancements included in this version are smart indentation in HTML documents, HTML5 snippets, HTML start and end tag matching, and HTML validation.</span></span> <span data-ttu-id="87185-236">在本练习中，你将看到在网站标记中工作时，这些更改如何改进你流畅性。</span><span class="sxs-lookup"><span data-stu-id="87185-236">Throughout this exercise, you will see how these changes improve your fluency when working in the website markup.</span></span>

<span data-ttu-id="87185-237">CSS 编辑器中，如 HTML 编辑器也已得到改进。</span><span class="sxs-lookup"><span data-stu-id="87185-237">Like the CSS editor, the HTML editor was also improved.</span></span> <span data-ttu-id="87185-238">这些改进大部分都是使 Web 开发人员更轻松的小的。</span><span class="sxs-lookup"><span data-stu-id="87185-238">Most of these improvements are small ones that make the Web developer's life easier.</span></span> <span data-ttu-id="87185-239">针对 HTML5，智能缩进匹配开始和结束标记时编辑和验证目标 HTML 文档 DOCTYPE 其中有些改善像多个代码段。</span><span class="sxs-lookup"><span data-stu-id="87185-239">Things like more code snippets for HTML5, smart indentation, matching start and end tags when editing and validation targeting the HTML document DOCTYPE are some of these improvements.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a><span data-ttu-id="87185-240">任务 1-改进的 DOCTYPE 验证</span><span class="sxs-lookup"><span data-stu-id="87185-240">Task 1 - Improved DOCTYPE Validation</span></span>

<span data-ttu-id="87185-241">HTML 编辑器现在具有能够检查你的页面，DOCTYPE，即使定义可能在母版页中。</span><span class="sxs-lookup"><span data-stu-id="87185-241">The HTML editor now has the ability to check the DOCTYPE of your page, even though the definition might be in the master page.</span></span> <span data-ttu-id="87185-242">具体取决于你的页面的 DOCTYPE，HTML 编辑器将验证与正确的规则集，并将筛选考虑 DOCTYPE 元素的智能感知列表。</span><span class="sxs-lookup"><span data-stu-id="87185-242">Depending on the DOCTYPE of your page, the HTML editor will validate with the correct set of rules and will filter the IntelliSense list considering the DOCTYPE elements.</span></span>

<span data-ttu-id="87185-243">在此任务中，你将更改页面的 DOCTYPE，若要了解如何 HTML 编辑器行为相应地改变。</span><span class="sxs-lookup"><span data-stu-id="87185-243">In this task, you will change the DOCTYPE of a page to see how the HTML editor behavior changes accordingly.</span></span>

1. <span data-ttu-id="87185-244">如果尚未打开，启动**Visual Studio**并打开**WhatsNewASPNET.sln**解决方案位于**Source\WhatsNewASPNET**这个实验室的文件夹。</span><span class="sxs-lookup"><span data-stu-id="87185-244">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="87185-245">打开**Site.Master**页。</span><span class="sxs-lookup"><span data-stu-id="87185-245">Open the **Site.Master** page.</span></span>
3. <span data-ttu-id="87185-246">验证工具栏，请注意目标架构。</span><span class="sxs-lookup"><span data-stu-id="87185-246">Notice the Target Schema for Validation Toolbar.</span></span> <span data-ttu-id="87185-247">HTML 编辑器的行为 （验证、 IntelliSense 等） 将正确更改以适应所选 Doctype。</span><span class="sxs-lookup"><span data-stu-id="87185-247">The way the HTML editor behaves (Validation, IntelliSense, etc.) will properly change to fit the Doctype selected.</span></span>

    <span data-ttu-id="87185-248">![在 HTML 源编辑工具栏中使用 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "使用 Doctype HTML 源编辑工具栏中")</span><span class="sxs-lookup"><span data-stu-id="87185-248">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="87185-249">*使用 Doctype HTML 源编辑工具栏中*</span><span class="sxs-lookup"><span data-stu-id="87185-249">*Use Doctype in HTML Source Editing toolbar*</span></span>
4. <span data-ttu-id="87185-250">将目标架构更改为 HTML 4.01。</span><span class="sxs-lookup"><span data-stu-id="87185-250">Change the Target Schema to HTML 4.01.</span></span>

    <span data-ttu-id="87185-251">![在 HTML 源编辑工具栏中更改 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "更改 Doctype HTML 源编辑工具栏中")</span><span class="sxs-lookup"><span data-stu-id="87185-251">![Changing Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "Changing Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="87185-252">*在 HTML 源编辑工具栏中更改 Doctype*</span><span class="sxs-lookup"><span data-stu-id="87185-252">*Changing Doctype in HTML Source Editing toolbar*</span></span>
5. <span data-ttu-id="87185-253">将在光标**正文**元素，并开始键入 HTML5 元素的名称 (例如，**视频**)。</span><span class="sxs-lookup"><span data-stu-id="87185-253">Place the cursor under the **body** element, and start typing the name of an HTML5 element (for example, **video**).</span></span> <span data-ttu-id="87185-254">请注意，元素不存在的智能感知列表中。</span><span class="sxs-lookup"><span data-stu-id="87185-254">Notice that the element is not available in the IntelliSense list.</span></span>

    <span data-ttu-id="87185-255">![未列出的 HTML5 元素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "未列出的 HTML5 元素")</span><span class="sxs-lookup"><span data-stu-id="87185-255">![HTML5 elements not listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "HTML5 elements not listed")</span></span>

    <span data-ttu-id="87185-256">*未列出的 HTML5 元素*</span><span class="sxs-lookup"><span data-stu-id="87185-256">*HTML5 elements not listed*</span></span>
6. <span data-ttu-id="87185-257">撤消对目标架构的更改的验证工具栏上，选择 DOCTYPE: XHTML5 从下拉列表。</span><span class="sxs-lookup"><span data-stu-id="87185-257">Undo the changes to the Target Schema for Validation Toolbar, picking DOCTYPE: XHTML5 from the dropdown list.</span></span>

    <span data-ttu-id="87185-258">![在 HTML 源编辑工具栏中使用 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "使用 Doctype HTML 源编辑工具栏中")</span><span class="sxs-lookup"><span data-stu-id="87185-258">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="87185-259">*重置 Doctype HTML 源编辑工具栏中*</span><span class="sxs-lookup"><span data-stu-id="87185-259">*Reset Doctype in HTML Source Editing toolbar*</span></span>
7. <span data-ttu-id="87185-260">将在光标**正文**元素并开始再次键入 HTML5 元素 (例如，如**视频**)。</span><span class="sxs-lookup"><span data-stu-id="87185-260">Place the cursor under the **body** element and start typing an HTML5 element again (For example, like **video**).</span></span> <span data-ttu-id="87185-261">请注意 HTML5 元素现可用于智能感知列表。</span><span class="sxs-lookup"><span data-stu-id="87185-261">Notice that the HTML5 elements are now available in the IntelliSense list.</span></span>

    <span data-ttu-id="87185-262">![HTML5 元素会列出](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "正在列出的 HTML5 元素")</span><span class="sxs-lookup"><span data-stu-id="87185-262">![HTML5 elements being listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "HTML5 elements being listed")</span></span>

    <span data-ttu-id="87185-263">*正在列出的 HTML5 元素*</span><span class="sxs-lookup"><span data-stu-id="87185-263">*HTML5 elements being listed*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a><span data-ttu-id="87185-264">任务 2-开始/结束标记自动更新</span><span class="sxs-lookup"><span data-stu-id="87185-264">Task 2 - Start/End Tags Automatic Update</span></span>

<span data-ttu-id="87185-265">Visual Studio 现在更新打开或关闭正在编辑相互匹配的元素的标记的 HTML。</span><span class="sxs-lookup"><span data-stu-id="87185-265">Visual Studio now updates the HTML opening or closing tags of the element that you are editing to match each other.</span></span> <span data-ttu-id="87185-266">在编辑 HTML 标记时，此新功能将提高工作效率。</span><span class="sxs-lookup"><span data-stu-id="87185-266">This new feature will improve your productivity when editing HTML tags.</span></span>

1. <span data-ttu-id="87185-267">上**Default.aspx**页上，添加**H3**具有标题 （例如，Visual Studio 2012 岩石 ！） 的元素。</span><span class="sxs-lookup"><span data-stu-id="87185-267">On the **Default.aspx** page, add an **H3** element with a title (for example, Visual Studio 2012 Rocks!).</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. <span data-ttu-id="87185-268">更改**H3**标记和类型**H2**或**h 1。**</span><span class="sxs-lookup"><span data-stu-id="87185-268">Change the **H3** tag and type **H2** or **H1.**</span></span>

    <span data-ttu-id="87185-269">请注意，自动更新的结束标记。</span><span class="sxs-lookup"><span data-stu-id="87185-269">Notice that the end tag automatically updates.</span></span> <span data-ttu-id="87185-270">你还可以修改以查看，开始标记会相应地更新过的结束标记。</span><span class="sxs-lookup"><span data-stu-id="87185-270">You can also modify the end tag to see that the start tag updates accordingly too.</span></span>

    <span data-ttu-id="87185-271">![结束标记的自动更新](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "的结束标记的自动更新")</span><span class="sxs-lookup"><span data-stu-id="87185-271">![Automatic update of the end tag](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "Automatic update of the end tag")</span></span>

    <span data-ttu-id="87185-272">*结束标记的自动更新*</span><span class="sxs-lookup"><span data-stu-id="87185-272">*Automatic update of the end tag*</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a><span data-ttu-id="87185-273">任务 3-新的 HTML5 代码段</span><span class="sxs-lookup"><span data-stu-id="87185-273">Task 3 - New HTML5 Code Snippets</span></span>

<span data-ttu-id="87185-274">Visual Studio 现在包含几个 HTML5 代码段。</span><span class="sxs-lookup"><span data-stu-id="87185-274">Visual Studio now includes several HTML5 code snippets.</span></span> <span data-ttu-id="87185-275">在此任务中，你将使用这些代码段的一些。</span><span class="sxs-lookup"><span data-stu-id="87185-275">In this task, you will use some of these snippets.</span></span>

1. <span data-ttu-id="87185-276">添加一个名为的新文件夹**音频**到网站文件夹的根目录。</span><span class="sxs-lookup"><span data-stu-id="87185-276">Add a new folder named **audio** to the root of the web site folder.</span></span> <span data-ttu-id="87185-277">打开 Windows 资源管理器并将复制到任何音频文件**音频**文件夹**WhatsNewASPNET.sln**解决方案。</span><span class="sxs-lookup"><span data-stu-id="87185-277">Open Windows Explorer and copy any audio file into the **audio** folder of the **WhatsNewASPNET.sln** solution.</span></span>
2. <span data-ttu-id="87185-278">在**Default.aspx**页上，找到下 Web11 岩石光标!!</span><span class="sxs-lookup"><span data-stu-id="87185-278">In the **Default.aspx** page, locate the cursor under the Web11 Rocks!!</span></span> <span data-ttu-id="87185-279">标头。</span><span class="sxs-lookup"><span data-stu-id="87185-279">Header.</span></span> <span data-ttu-id="87185-280">类型**音频**，然后按 TAB 键。</span><span class="sxs-lookup"><span data-stu-id="87185-280">Type **audio** and press the TAB key.</span></span>

    <span data-ttu-id="87185-281">新的 HTML 编辑器包括 HTML5 内容的代码段。</span><span class="sxs-lookup"><span data-stu-id="87185-281">The new HTML editor includes code snippets for HTML5 content.</span></span> <span data-ttu-id="87185-282">请记住使用正确的 DOCTYPE 定义来启用 HTML5 代码段。</span><span class="sxs-lookup"><span data-stu-id="87185-282">Remember to use the proper DOCTYPE definition to enable the HTML5 snippets.</span></span>

    <span data-ttu-id="87185-283">![插入 HTML5 代码代码段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "插入 HTML5 代码代码段")</span><span class="sxs-lookup"><span data-stu-id="87185-283">![Inserting HTML5 Code Snippets](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "Inserting HTML5 Code Snippets")</span></span>

    <span data-ttu-id="87185-284">*插入 HTML5 代码代码段*</span><span class="sxs-lookup"><span data-stu-id="87185-284">*Inserting HTML5 Code Snippets*</span></span>
3. <span data-ttu-id="87185-285">更新音频源以指向现有的音频文件。</span><span class="sxs-lookup"><span data-stu-id="87185-285">Update the audio source to point to an existing audio file.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > <span data-ttu-id="87185-286">你将需要向解决方案中添加的音频文件。</span><span class="sxs-lookup"><span data-stu-id="87185-286">You will need to add the audio file to the solution.</span></span>
4. <span data-ttu-id="87185-287">按**F5**来运行该站点和播放音频。</span><span class="sxs-lookup"><span data-stu-id="87185-287">Press **F5** to run the site and play the audio.</span></span>

    <span data-ttu-id="87185-288">![运行音频控件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "运行音频控件")</span><span class="sxs-lookup"><span data-stu-id="87185-288">![Running the audio control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "Running the audio control")</span></span>

    <span data-ttu-id="87185-289">*运行音频控件*</span><span class="sxs-lookup"><span data-stu-id="87185-289">*Running the audio control*</span></span>

    > [!NOTE]
    > <span data-ttu-id="87185-290">你还可以尝试多个代码段包含在 Visual Studio 中，例如视频、 图，等等。</span><span class="sxs-lookup"><span data-stu-id="87185-290">You can also try more snippets included in Visual Studio, such as video, figure, etc.</span></span>
5. <span data-ttu-id="87185-291">现在，尝试将控件插入页的某些部分。</span><span class="sxs-lookup"><span data-stu-id="87185-291">Now, try to insert a control in some part of the page.</span></span> <span data-ttu-id="87185-292">例如，尝试插入**GridView**控件，但而不是键入 **&lt;gri 可持续发展，** 开始键入 **&lt;GV**。</span><span class="sxs-lookup"><span data-stu-id="87185-292">For example, try to insert a **GridView** control, but instead of typing **&lt;Gri,** start typing **&lt;GV**.</span></span> <span data-ttu-id="87185-293">请注意，IntelliSense 列表显示**asp: GridView**控件。</span><span class="sxs-lookup"><span data-stu-id="87185-293">Notice that the IntelliSense list shows the **asp:GridView** control.</span></span>

    <span data-ttu-id="87185-294">IntelliSense 的 HTML 编辑器现在提供标题大小写搜索，以及部分匹配 （检索包含术语的所有元素）。</span><span class="sxs-lookup"><span data-stu-id="87185-294">IntelliSense in the HTML Editor now provides title-casing search, as well as partial matching (retrieving all elements that contains the term).</span></span>

    <span data-ttu-id="87185-295">![插入与智能感知列表 GridView](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "插入与智能感知列表 GridView")</span><span class="sxs-lookup"><span data-stu-id="87185-295">![Inserting a GridView with IntelliSense lists](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "Inserting a GridView with IntelliSense lists")</span></span>

    <span data-ttu-id="87185-296">*插入与智能感知列表 GridView*</span><span class="sxs-lookup"><span data-stu-id="87185-296">*Inserting a GridView with IntelliSense lists*</span></span>

    <span data-ttu-id="87185-297">如果你键入**&lt;网格**会获得词，匹配的所有项而 Visual Studio 将建议**gridview**控件：</span><span class="sxs-lookup"><span data-stu-id="87185-297">If you type **&lt;grid** you will get all the items that match the term, but Visual Studio will suggest the **gridview** control:</span></span>

    <span data-ttu-id="87185-298">![插入与智能感知列表和部分匹配 GridView](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "插入与智能感知列表和部分匹配 GridView")</span><span class="sxs-lookup"><span data-stu-id="87185-298">![Inserting a GridView with IntelliSense lists and partial matching](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "Inserting a GridView with IntelliSense lists and partial matching")</span></span>

    <span data-ttu-id="87185-299">*插入与智能感知列表和部分匹配 GridView*</span><span class="sxs-lookup"><span data-stu-id="87185-299">*Inserting a GridView with IntelliSense lists and partial matching*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a><span data-ttu-id="87185-300">任务 4-HTML 编辑器智能标记</span><span class="sxs-lookup"><span data-stu-id="87185-300">Task 4 - HTML Editor Smart Tags</span></span>

<span data-ttu-id="87185-301">在 HTML 编辑器中的另一改进是智能标记功能。</span><span class="sxs-lookup"><span data-stu-id="87185-301">Another improvement in the HTML Editor is the Smart Tags feature.</span></span> <span data-ttu-id="87185-302">智能标记使易于基于每个控件执行常见或重复的开发任务。</span><span class="sxs-lookup"><span data-stu-id="87185-302">Smart tags make it easy to perform common or repetitive development tasks on a per-control basis.</span></span> <span data-ttu-id="87185-303">此功能已可用在 HTML 设计器中，但不是在 HTML 编辑器中。</span><span class="sxs-lookup"><span data-stu-id="87185-303">This feature was already available in the HTML Designer, but not in the HTML Editor.</span></span>

1. <span data-ttu-id="87185-304">打开**Site.Master**并找到**asp： 菜单**元素。</span><span class="sxs-lookup"><span data-stu-id="87185-304">Open **Site.Master** and locate the **asp:Menu** element.</span></span> <span data-ttu-id="87185-305">将光标置于开始标记和元素的底部显示的小标志符号单击它以打开智能任务菜单的通知。</span><span class="sxs-lookup"><span data-stu-id="87185-305">Place the cursor on the start tag and notice that the small glyph displayed at the bottom of the element - click it to open the smart tasks menu.</span></span> <span data-ttu-id="87185-306">请注意，可以快速访问与菜单控件相关的一些任务。</span><span class="sxs-lookup"><span data-stu-id="87185-306">Notice that you have quick access to some tasks related to the Menu control.</span></span>

    <span data-ttu-id="87185-307">![智能菜单控件任务的](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "智能菜单控件有关的任务")</span><span class="sxs-lookup"><span data-stu-id="87185-307">![Smart tasks for the Menu control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Smart tasks for the Menu control")</span></span>

    <span data-ttu-id="87185-308">*菜单控件的智能任务*</span><span class="sxs-lookup"><span data-stu-id="87185-308">*Smart tasks for the Menu control*</span></span>

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a><span data-ttu-id="87185-309">任务 5-智能缩进</span><span class="sxs-lookup"><span data-stu-id="87185-309">Task 5 - Smart Indentation</span></span>

<span data-ttu-id="87185-310">HTML 中的最佳做法之一缩进的嵌套的元素，以使代码更具可读性。</span><span class="sxs-lookup"><span data-stu-id="87185-310">One of the best practices in HTML is indenting the nested elements to keep the code readable.</span></span> <span data-ttu-id="87185-311">在 Visual Studio 2012 中，你将注意到您在编写代码时，编辑器可以自动将元素。</span><span class="sxs-lookup"><span data-stu-id="87185-311">In Visual Studio 2012, you will notice that the editor automatically indents the elements while you are writing the code.</span></span>

> [!NOTE]
> <span data-ttu-id="87185-312">在以前版本的 Visual Studio 中，提供智能缩进的 XML 编辑器中，但不是在 HTML 编辑器中。</span><span class="sxs-lookup"><span data-stu-id="87185-312">In previous version of Visual Studio, smart indentation was available in the XML editor but not in the HTML editor.</span></span>


1. <span data-ttu-id="87185-313">请确保在 HTML 编辑器中的缩进配置设置为智能缩进。</span><span class="sxs-lookup"><span data-stu-id="87185-313">Make sure that the Indenting configuration on the HTML Editor is set to Smart Indentation.</span></span> <span data-ttu-id="87185-314">为此，请选择**工具 |选项**菜单选项，然后选择**文本编辑器 |HTML |选项卡**屏幕的左窗格中的页。</span><span class="sxs-lookup"><span data-stu-id="87185-314">To do that, select the **Tools | Options** menu option and then select the **Text Editor | HTML | Tabs** page in the left pane of the screen.</span></span> <span data-ttu-id="87185-315">选择智能缩进选项。</span><span class="sxs-lookup"><span data-stu-id="87185-315">Select the Smart indentation option.</span></span>

    <span data-ttu-id="87185-316">![HTML 编辑器设置](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML 编辑器设置")</span><span class="sxs-lookup"><span data-stu-id="87185-316">![HTML Editor settings](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML Editor settings")</span></span>

    <span data-ttu-id="87185-317">*HTML 编辑器设置*</span><span class="sxs-lookup"><span data-stu-id="87185-317">*HTML Editor settings*</span></span>
2. <span data-ttu-id="87185-318">上**Default.aspx**页上，删除音频元素下的所有内容。</span><span class="sxs-lookup"><span data-stu-id="87185-318">On the **Default.aspx** page, remove all the content under the audio element.</span></span>
3. <span data-ttu-id="87185-319">将光标放在打开末尾**音频**元素然后点击**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="87185-319">Place the cursor at the end of the opening **audio** element and hit **ENTER**.</span></span>

    <span data-ttu-id="87185-320">请注意，新光标的位置有一个其他的缩进级别。</span><span class="sxs-lookup"><span data-stu-id="87185-320">Notice that the new position of cursor has an additional indentation level.</span></span>

    <span data-ttu-id="87185-321">![智能缩进的 HTML 编辑器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "智能缩进的 HTML 编辑器")</span><span class="sxs-lookup"><span data-stu-id="87185-321">![Smart indentation in the HTML Editor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "Smart indentation in the HTML Editor")</span></span>

    <span data-ttu-id="87185-322">*智能缩进的 HTML 编辑器*</span><span class="sxs-lookup"><span data-stu-id="87185-322">*Smart indentation in the HTML Editor*</span></span>
4. <span data-ttu-id="87185-323">还原已删除，或关闭的内容与音频标记**Default.aspx**而不保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="87185-323">Restore the audio tag with the content you have removed, or close **Default.aspx** without saving the changes.</span></span>

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a><span data-ttu-id="87185-324">任务 6-提取到用户控件</span><span class="sxs-lookup"><span data-stu-id="87185-324">Task 6 - Extract to User Control</span></span>

<span data-ttu-id="87185-325">包括在 Visual Studio 中，如提取部分、 指向函数的重构工具是代码的帮助改善和重构现有代码的强大功能。</span><span class="sxs-lookup"><span data-stu-id="87185-325">The Refactoring tools included in Visual Studio, such as extracting a portion of code to a function, are great features that facilitate the improvement and the refactoring the existing code.</span></span> <span data-ttu-id="87185-326">ASP.NET 页面对应的将提取到用户控件的 HTML 代码。</span><span class="sxs-lookup"><span data-stu-id="87185-326">The counterpart for ASP.NET pages would be the extraction of HTML code to a User Control.</span></span> <span data-ttu-id="87185-327">不要手动将涉及几个步骤，如创建新的用户控件、 将代码部分移到用户控件、 注册用户控件标记前缀和，最后，实例化的页上该用户控件。</span><span class="sxs-lookup"><span data-stu-id="87185-327">Doing it manually would involve several steps, like creating a new User Control, moving the code section to the User Control, registering a tag prefix for the User Control, and, finally, instantiating the User Control on the pages.</span></span> <span data-ttu-id="87185-328">现在，新*提取到用户控件*工具会自动为你执行所有这些步骤。</span><span class="sxs-lookup"><span data-stu-id="87185-328">Now, the new *Extract to User Control* tool automatically performs all those steps for you.</span></span>

<span data-ttu-id="87185-329">在此任务中，你将使用新提取到用户控制上下文操作从所选的代码生成一个新的用户控件。</span><span class="sxs-lookup"><span data-stu-id="87185-329">In this task, you will use the new Extract to User Control contextual operation to generate a new user control from the selected code.</span></span>

1. <span data-ttu-id="87185-330">上**Default.aspx**页上，选择**H2**和**音频**元素。</span><span class="sxs-lookup"><span data-stu-id="87185-330">On the **Default.aspx** page, select the **H2** and **audio** elements.</span></span>
2. <span data-ttu-id="87185-331">右键单击并选择**提取到用户控件**。</span><span class="sxs-lookup"><span data-stu-id="87185-331">Right click and select **Extract to User Control**.</span></span>

    <span data-ttu-id="87185-332">![提取到用户控件菜单选项](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "提取到用户控件菜单选项")</span><span class="sxs-lookup"><span data-stu-id="87185-332">![Extract to User Control menu option](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "Extract to User Control menu option")</span></span>

    <span data-ttu-id="87185-333">*提取到用户控件菜单选项*</span><span class="sxs-lookup"><span data-stu-id="87185-333">*Extract to User Control menu option*</span></span>
3. <span data-ttu-id="87185-334">键入新的用户控件的名称。</span><span class="sxs-lookup"><span data-stu-id="87185-334">Type a name for the new user control.</span></span> <span data-ttu-id="87185-335">例如， **Jukebox.ascx**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="87185-335">For instance, **Jukebox.ascx**, and then click **OK**.</span></span>

    <span data-ttu-id="87185-336">![保存提取的用户控件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "保存提取的用户控件")</span><span class="sxs-lookup"><span data-stu-id="87185-336">![Saving the extracted user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "Saving the extracted user control")</span></span>

    <span data-ttu-id="87185-337">*保存提取的用户控件*</span><span class="sxs-lookup"><span data-stu-id="87185-337">*Saving the extracted user control*</span></span>
4. <span data-ttu-id="87185-338">请注意，所选的代码提取到用户控件并与新的用户控件的实例替换为所选代码的原始位置。</span><span class="sxs-lookup"><span data-stu-id="87185-338">Notice that the selected code was extracted to a user control and the original location of the selected code was replaced with an instance of the new user control.</span></span>

    <span data-ttu-id="87185-339">![页自动更新，以使用新的用户控件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "页将自动更新，以使用新的用户控件")</span><span class="sxs-lookup"><span data-stu-id="87185-339">![Page automatically updated to use the new user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "Page automatically updated to use the new user control")</span></span>

    <span data-ttu-id="87185-340">*页自动更新，以使用新的用户控件*</span><span class="sxs-lookup"><span data-stu-id="87185-340">*Page automatically updated to use the new user control*</span></span>
5. <span data-ttu-id="87185-341">按**F5**运行页面，并验证该控件是否有效。</span><span class="sxs-lookup"><span data-stu-id="87185-341">Press **F5** to run the page and verify that the control works.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a><span data-ttu-id="87185-342">练习 3： 什么是 JavaScript 编辑器中的新增功能</span><span class="sxs-lookup"><span data-stu-id="87185-342">Exercise 3: What's New in the JavaScript Editor</span></span>

<span data-ttu-id="87185-343">编写或编辑 JavaScript 代码不是一个简单的任务，特别是在你的应用程序启动增大，并且你发现自己长文件处理和数百个函数。</span><span class="sxs-lookup"><span data-stu-id="87185-343">Writing or editing JavaScript code is not an easy task, especially when your application starts to grow in size and you find yourself dealing with long files and hundreds of functions.</span></span> <span data-ttu-id="87185-344">脚本开发人员通常需要执行一些额外的工作以维护代码可读性并在文件之间导航。</span><span class="sxs-lookup"><span data-stu-id="87185-344">Script developers usually have to do some extra work to maintain code legibility and navigate across files.</span></span> <span data-ttu-id="87185-345">如 jQuery JavaScript 库为包含，脚本导航变得艰巨本身由于代码长度。</span><span class="sxs-lookup"><span data-stu-id="87185-345">With the inclusion of JavaScript libraries like jQuery, script navigation has become a challenge itself because of the code length.</span></span>

<span data-ttu-id="87185-346">Visual Studio 已续订承诺来使代码模式，可访问和组织的 JavaScript 编辑器。</span><span class="sxs-lookup"><span data-stu-id="87185-346">Visual Studio has renewed the JavaScript editor with the promise to make the code mode accessible and organized.</span></span> <span data-ttu-id="87185-347">已经存在于 C# 或 VB 编辑器中的许多 Visual Studio 功能现在已实现在 JavaScript 编辑器中： 转到定义、 自动缩进、 文档和当你正在编写时进行验证。</span><span class="sxs-lookup"><span data-stu-id="87185-347">Many Visual Studio features that already existed in C# or VB editors are now implemented in the JavaScript editor: Go To Definition, automatic indentation, documentation and validation when you are writing.</span></span> <span data-ttu-id="87185-348">与续订的 IntelliSense 列表将在您能够轻松利用具有 JavaScript 函数目录。</span><span class="sxs-lookup"><span data-stu-id="87185-348">With the renewed IntelliSense list you will have the JavaScript function catalog at your fingertips.</span></span>

<span data-ttu-id="87185-349">在本练习中，你将学习的一些新功能和改进的 JavaScript 编辑器。</span><span class="sxs-lookup"><span data-stu-id="87185-349">In this exercise, you will learn some of the new features and improvements of JavaScript editor.</span></span> <span data-ttu-id="87185-350">将浏览示例文件，并且发现每个将使在 JavaScript 编程更高效 Visual Studio 2012 中的新特征。</span><span class="sxs-lookup"><span data-stu-id="87185-350">You will browse sample files and discover each of the new characteristics that will make your JavaScript programming more efficient within Visual Studio 2012.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a><span data-ttu-id="87185-351">任务 1-JavaScript 编辑器新功能</span><span class="sxs-lookup"><span data-stu-id="87185-351">Task 1 - JavaScript Editor New Features</span></span>

<span data-ttu-id="87185-352">此任务将向你介绍某些新的 JavaScript 编辑器功能，其中重点介绍组织你的代码并将更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="87185-352">This task will introduce you to some of the new JavaScript editor features, which focus on organizing your code and bringing a better user experience.</span></span>

1. <span data-ttu-id="87185-353">如果尚未打开，启动**Visual Studio**并打开**WhatsNewASPNET.sln**解决方案位于**Source\WhatsNewASPNET**这个实验室的文件夹。</span><span class="sxs-lookup"><span data-stu-id="87185-353">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="87185-354">按**F5**运行该应用程序，然后单击导航栏中的 JavaScript 链接。</span><span class="sxs-lookup"><span data-stu-id="87185-354">Press **F5** to run the application, then click the JavaScript link in the navigation bar.</span></span> <span data-ttu-id="87185-355">刷新页面几次并检查如何此计数器递增。</span><span class="sxs-lookup"><span data-stu-id="87185-355">Refresh the page several times and check how the counter increments.</span></span>

    <span data-ttu-id="87185-356">![Page 计数器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Page 计数器")</span><span class="sxs-lookup"><span data-stu-id="87185-356">![Page counter](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Page counter")</span></span>

    <span data-ttu-id="87185-357">*Page 计数器*</span><span class="sxs-lookup"><span data-stu-id="87185-357">*Page counter*</span></span>
3. <span data-ttu-id="87185-358">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="87185-358">Close the browser and go back to Visual Studio.</span></span>
4. <span data-ttu-id="87185-359">打开**JavaScript.aspx**页然后找到**&lt;脚本&gt;** 块 （如下所示）。</span><span class="sxs-lookup"><span data-stu-id="87185-359">Open the **JavaScript.aspx** page and locate the **&lt;script&gt;** block (shown below).</span></span>

    <span data-ttu-id="87185-360">下面的代码使用 HTML5 本地存储来存储*pageLoadCount*变量，用于存储的当前用户访问页的次数。</span><span class="sxs-lookup"><span data-stu-id="87185-360">The following code uses HTML5 local storage to store a *pageLoadCount* variable that stores the number of times the page has been visited by the current user.</span></span> <span data-ttu-id="87185-361">本地存储是引入 HTML5 标准的客户端键值对的数据库。</span><span class="sxs-lookup"><span data-stu-id="87185-361">Local Storage is a client-side key-value database introduced with the HTML5 standard.</span></span> <span data-ttu-id="87185-362">在用户的浏览器内的本地计算机上保存的数据。</span><span class="sxs-lookup"><span data-stu-id="87185-362">The data is saved on the local machine, inside the user's browser.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="87185-363">确保 DOCTYPE 设置为 XHTML5 然后再继续进行下一步的步骤。</span><span class="sxs-lookup"><span data-stu-id="87185-363">Ensure the DOCTYPE is set to XHTML5 before proceeding with the next steps.</span></span>
5. <span data-ttu-id="87185-364">编辑代码，并请注意，适用于 JavaScript IntelliSense 包含 HTML5 功能，如本地存储区和其内部的方法。</span><span class="sxs-lookup"><span data-stu-id="87185-364">Edit the code and notice that IntelliSense for JavaScript includes HTML5 features, like local storage, and their inner methods.</span></span>

    <span data-ttu-id="87185-365">![在 JavaScript 中的 HTML5 JavaScript 功能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "JavaScript 中的 HTML5 JavaScript 功能")</span><span class="sxs-lookup"><span data-stu-id="87185-365">![HTML5 JavaScript features in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "HTML5 JavaScript features in JavaScript")</span></span>

    <span data-ttu-id="87185-366">*在 JavaScript 中的 HTML5 JavaScript 功能*</span><span class="sxs-lookup"><span data-stu-id="87185-366">*HTML5 JavaScript features in JavaScript*</span></span>
6. <span data-ttu-id="87185-367">单击任何左大括号 (**{**) 从脚本代码，并注意括号突出显示。</span><span class="sxs-lookup"><span data-stu-id="87185-367">Click any opening bracket (**{**) from the scripting code and notice that the brackets are highlighted.</span></span>

    <span data-ttu-id="87185-368">![括号突出显示](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "括号突出显示")</span><span class="sxs-lookup"><span data-stu-id="87185-368">![Brackets are highlighted](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "Brackets are highlighted")</span></span>

    <span data-ttu-id="87185-369">*括号突出显示*</span><span class="sxs-lookup"><span data-stu-id="87185-369">*Brackets are highlighted*</span></span>
7. <span data-ttu-id="87185-370">取消注释函数**testAutoAlign()** (选择三个行，然后你可以使用**CTRL** + **K**;**CTRL** + **U**) 并找到光标置于函数代码。</span><span class="sxs-lookup"><span data-stu-id="87185-370">Uncomment the function **testAutoAlign()** (select the three lines and you can use **CTRL** + **K**; **CTRL** + **U**) and locate the cursor inside the function code.</span></span> <span data-ttu-id="87185-371">按 enter 要追加第二行。</span><span class="sxs-lookup"><span data-stu-id="87185-371">Press enter to append a second line.</span></span> <span data-ttu-id="87185-372">请注意，代码现在是**对齐**和**自动缩进**。</span><span class="sxs-lookup"><span data-stu-id="87185-372">Notice that the code is now **aligned** and **auto-indented**.</span></span>

    <span data-ttu-id="87185-373">![JavaScript 代码是对齐的自动](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript 代码是自动的对齐")</span><span class="sxs-lookup"><span data-stu-id="87185-373">![JavaScript code is auto aligned](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript code is auto aligned")</span></span>

    <span data-ttu-id="87185-374">*JavaScript 代码是自动的对齐*</span><span class="sxs-lookup"><span data-stu-id="87185-374">*JavaScript code is auto aligned*</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a><span data-ttu-id="87185-375">任务 2-验证 JavaScript</span><span class="sxs-lookup"><span data-stu-id="87185-375">Task 2 - Validating JavaScript</span></span>

<span data-ttu-id="87185-376">在此任务中，你会发现 ECMAScript5 标准的新 JavaScript 验证。</span><span class="sxs-lookup"><span data-stu-id="87185-376">In this task, you will discover the new JavaScript validation for the ECMAScript5 standard.</span></span> <span data-ttu-id="87185-377">此功能将帮助你编写兼容的 JavaScript 代码，在站点部署之前阻止脚本问题时。</span><span class="sxs-lookup"><span data-stu-id="87185-377">This feature will help you to write compliant JavaScript code, while preventing scripting issues before site deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="87185-378">Visual Studio 2010 实现 ECMAStript3 法规遵从性，而 Visual Studio 2012 提供 ECMAScript5 法规遵从性。</span><span class="sxs-lookup"><span data-stu-id="87185-378">Visual Studio 2010 implemented ECMAStript3 compliance, while Visual Studio 2012 provides ECMAScript5 compliance.</span></span>


1. <span data-ttu-id="87185-379">打开**ECMA5script5.js**位于**Scripts\custom**项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="87185-379">Open **ECMA5script5.js** located under the **Scripts\custom** project folder.</span></span> <span data-ttu-id="87185-380">现在，你将测试 ECMAScript5 标准的验证。</span><span class="sxs-lookup"><span data-stu-id="87185-380">You will now test validation for ECMAScript5 standard.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    <span data-ttu-id="87185-381">你可以查看&quot;**使用严格**&quot;方向在第一行中的文件，这样 ECMAScript5**严格模式下**。</span><span class="sxs-lookup"><span data-stu-id="87185-381">You can check out the &quot; **use strict** &quot; direction in the first line of the file, which enables ECMAScript5 **strict mode**.</span></span> <span data-ttu-id="87185-382">此模式包含在阐明多义性从过去版本，并在对象属性上添加一些新功能，例如 getter 和 setter、 JSON 和更完整的反射的库支持的语言的子集。</span><span class="sxs-lookup"><span data-stu-id="87185-382">This mode consists in a subset of the language that clarifies ambiguities from the past edition, and adds some new features, such as getters and setters, library support for JSON, and more complete reflection on object properties.</span></span>
2. <span data-ttu-id="87185-383">打开**错误列表**如果尚未打开 (**视图**菜单 |**错误列表**)。</span><span class="sxs-lookup"><span data-stu-id="87185-383">Open the **Error List** if not already opened (**View** menu | **Error List**).</span></span> <span data-ttu-id="87185-384">请注意**函数**声明是否有下划线。</span><span class="sxs-lookup"><span data-stu-id="87185-384">Notice the **function** declaration is underlined.</span></span> <span data-ttu-id="87185-385">这是因为 ECMA5 标准函数不能嵌套在语言结构。</span><span class="sxs-lookup"><span data-stu-id="87185-385">This is because in ECMA5 standard functions cannot be nested inside language structures.</span></span> <span data-ttu-id="87185-386">在错误列表下面你将看到警告详细信息。</span><span class="sxs-lookup"><span data-stu-id="87185-386">In the error list below you will see the warning details.</span></span>

    <span data-ttu-id="87185-387">![JavaScript 验证错误消息](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript 验证错误消息")</span><span class="sxs-lookup"><span data-stu-id="87185-387">![JavaScript validation error message](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript validation error message")</span></span>

    <span data-ttu-id="87185-388">*JavaScript 验证错误消息*</span><span class="sxs-lookup"><span data-stu-id="87185-388">*JavaScript validation error message*</span></span>
3. <span data-ttu-id="87185-389">注释掉**&quot;使用严格&quot;** 方向和请注意，错误消失，但警告保持。</span><span class="sxs-lookup"><span data-stu-id="87185-389">Comment out the **&quot;use strict&quot;** direction and notice that errors disappear, but the warnings remain.</span></span>
4. <span data-ttu-id="87185-390">在该文件的最后一行，编写任何字符串如下所示**&quot;测试&quot;** （包括引号引起来，以指示它是以字符串形式）。</span><span class="sxs-lookup"><span data-stu-id="87185-390">In the last line of the file, write any string like **&quot;test&quot;** (include the quotation marks to indicate it is as string).</span></span> <span data-ttu-id="87185-391">编写一段时间的字符串可以显示智能感知列表中，并选择旁边**trim**选项。</span><span class="sxs-lookup"><span data-stu-id="87185-391">Write a period next to the string to display the IntelliSense list, and select the **trim** option.</span></span>

    <span data-ttu-id="87185-392">在 ECMAScript5 标准中，字符串值和变量也有定义，如 trim、 大写、 搜索和替换的字符串方法。</span><span class="sxs-lookup"><span data-stu-id="87185-392">In ECMAScript5 standard, string values and variables also have string methods defined, like trim, uppercase, search and replace.</span></span>

    <span data-ttu-id="87185-393">![在 JavaScript 中的智能感知列表](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "在 JavaScript 中的 IntelliSense 列表")</span><span class="sxs-lookup"><span data-stu-id="87185-393">![IntelliSense list in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "IntelliSense list in JavaScript")</span></span>

    <span data-ttu-id="87185-394">*在 JavaScript 中的 IntelliSense 列表*</span><span class="sxs-lookup"><span data-stu-id="87185-394">*IntelliSense list in JavaScript*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a><span data-ttu-id="87185-395">任务 3-JavaScript XML 文档</span><span class="sxs-lookup"><span data-stu-id="87185-395">Task 3 - XML Documentation for JavaScript</span></span>

<span data-ttu-id="87185-396">在此任务中，您将了解有关在 JavaScript 中的 XML 文档的 Visual Studio 功能。</span><span class="sxs-lookup"><span data-stu-id="87185-396">In this task, you will explore Visual Studio features for XML documentation in JavaScript.</span></span> <span data-ttu-id="87185-397">你将看到 JavaScript IntelliSense 列表现在显示每个函数的 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="87185-397">You will see the JavaScript IntelliSense list now shows the XML documentation of each function.</span></span> <span data-ttu-id="87185-398">此外，你会发现在 JavaScript 中的导航功能。</span><span class="sxs-lookup"><span data-stu-id="87185-398">Additionally, you will discover the navigation feature in JavaScript.</span></span>

1. <span data-ttu-id="87185-399">打开**XMLDoc.js**文件位于**自定义脚本/** 项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="87185-399">Open **XMLDoc.js** file located in **Scripts/custom** project folder.</span></span> <span data-ttu-id="87185-400">此文件包含有关每个 JavaScript 函数的 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="87185-400">This file contains XML documentation on each of the JavaScript functions.</span></span>

    <span data-ttu-id="87185-401">![JavaScript XML 文档集成到 IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "JavaScript XML 文档集成到 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="87185-401">![JavaScript XML documentation integrated to IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "JavaScript XML documentation integrated to IntelliSense")</span></span>

    <span data-ttu-id="87185-402">*集成到 IntelliSense 的 JavaScript XML 文档*</span><span class="sxs-lookup"><span data-stu-id="87185-402">*JavaScript XML documentation integrated to IntelliSense*</span></span>
2. <span data-ttu-id="87185-403">下面**添加**函数中**XMLDoc.js**文件，创建一个名为的新函数**测试**。</span><span class="sxs-lookup"><span data-stu-id="87185-403">Below **add** function in **XMLDoc.js** file, create a new function named **test**.</span></span>
3. <span data-ttu-id="87185-404">在**测试**函数中，调用**乘**接收两个参数的函数。</span><span class="sxs-lookup"><span data-stu-id="87185-404">In the **test** function, call the **multiply** function that receives two parameters.</span></span> <span data-ttu-id="87185-405">请注意显示的工具提示框**乘**函数文档。</span><span class="sxs-lookup"><span data-stu-id="87185-405">Notice the tooltip box is showing the **multiply** function documentation.</span></span>

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    <span data-ttu-id="87185-406">![对于 JavaScript 函数为 XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "对于 JavaScript 函数为 XML 文档")</span><span class="sxs-lookup"><span data-stu-id="87185-406">![XML documentation for JavaScript functions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "XML documentation for JavaScript functions")</span></span>

    <span data-ttu-id="87185-407">*对于 JavaScript 函数为 XML 文档*</span><span class="sxs-lookup"><span data-stu-id="87185-407">*XML documentation for JavaScript functions*</span></span>
4. <span data-ttu-id="87185-408">完成的函数调用语句和类型*点*打开的智能感知列表上返回的值。</span><span class="sxs-lookup"><span data-stu-id="87185-408">Complete the function call statement and type a *dot* to open the IntelliSense list on the returned value.</span></span> <span data-ttu-id="87185-409">请注意，检测 Visual Studio**返回**在文档中，以便将该值视为一个数字的值。</span><span class="sxs-lookup"><span data-stu-id="87185-409">Notice that Visual Studio is detecting the **return** value in the documentation, treating the value as a number.</span></span>

    <span data-ttu-id="87185-410">![返回类型的 XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "返回类型的 XML 文档")</span><span class="sxs-lookup"><span data-stu-id="87185-410">![XML documentation for return types](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "XML documentation for return types")</span></span>

    <span data-ttu-id="87185-411">*返回类型的 XML 文档*</span><span class="sxs-lookup"><span data-stu-id="87185-411">*XML documentation for return types*</span></span>
5. <span data-ttu-id="87185-412">现在，插入要添加函数的调用。</span><span class="sxs-lookup"><span data-stu-id="87185-412">Now, insert a call to add function.</span></span> <span data-ttu-id="87185-413">请注意 JavaScript 编辑器现在支持函数重载。</span><span class="sxs-lookup"><span data-stu-id="87185-413">Notice that the JavaScript editor now supports function overloads.</span></span> <span data-ttu-id="87185-414">当你编写的函数名称时，你将能够选择任何可用的文档中指定的重载。</span><span class="sxs-lookup"><span data-stu-id="87185-414">When you write a function name, you will be able to select any of the available overloads specified in the documentation.</span></span>

    <span data-ttu-id="87185-415">![重载的 XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "重载的 XML 文档")</span><span class="sxs-lookup"><span data-stu-id="87185-415">![XML documentation for overloads](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "XML documentation for overloads")</span></span>

    <span data-ttu-id="87185-416">*重载的 XML 文档*</span><span class="sxs-lookup"><span data-stu-id="87185-416">*XML documentation for overloads*</span></span>
6. <span data-ttu-id="87185-417">打开**GotoDefinition.js**文件并找到 **$().html()** 函数调用。</span><span class="sxs-lookup"><span data-stu-id="87185-417">Open **GotoDefinition.js** file and locate the **$().html()** function call.</span></span> <span data-ttu-id="87185-418">在上找到光标**html**。</span><span class="sxs-lookup"><span data-stu-id="87185-418">Locate the cursor on **html**.</span></span>
7. <span data-ttu-id="87185-419">按**F12**和导航到的定义。</span><span class="sxs-lookup"><span data-stu-id="87185-419">Press **F12** and navigate to the definition.</span></span> <span data-ttu-id="87185-420">请注意，现在可以访问，并浏览你的 JavaScript 代码，而无需使用**查找**工具。</span><span class="sxs-lookup"><span data-stu-id="87185-420">Notice you can now access and browse your JavaScript code without using the **Find** tool.</span></span>
8. <span data-ttu-id="87185-421">在底部的代码文件的签名块之前的 jQuery 指令上查找光标。</span><span class="sxs-lookup"><span data-stu-id="87185-421">Locate the cursor on the jQuery instruction prior to the signature block at the bottom of the code file.</span></span> <span data-ttu-id="87185-422">按**F12**。</span><span class="sxs-lookup"><span data-stu-id="87185-422">Press **F12**.</span></span> <span data-ttu-id="87185-423">你将导航到 jQuery 库文件。</span><span class="sxs-lookup"><span data-stu-id="87185-423">You will navigate to the jQuery library file.</span></span> <span data-ttu-id="87185-424">请注意你还可以使用 jQuery 文件中导航**F12**。</span><span class="sxs-lookup"><span data-stu-id="87185-424">Notice you can also navigate across the jQuery files using **F12**.</span></span>

    <span data-ttu-id="87185-425">![导航到 jQuery 定义](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "导航到 jQuery 定义")</span><span class="sxs-lookup"><span data-stu-id="87185-425">![Navigating to jQuery definitions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "Navigating to jQuery definitions")</span></span>

    <span data-ttu-id="87185-426">*导航到 jQuery 定义*</span><span class="sxs-lookup"><span data-stu-id="87185-426">*Navigating to jQuery definitions*</span></span>

> [!NOTE]
> <span data-ttu-id="87185-427">请确保 GotoDefinition.js 保存文件之前具有没有语法错误。</span><span class="sxs-lookup"><span data-stu-id="87185-427">Make sure that GotoDefinition.js has no syntax errors before saving the file.</span></span>


<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a><span data-ttu-id="87185-428">练习 4： 捆绑和缩减</span><span class="sxs-lookup"><span data-stu-id="87185-428">Exercise 4: Bundling and Minification</span></span>

<span data-ttu-id="87185-429">您的网站多少次包括多个 JavaScript 或 CSS 文件？</span><span class="sxs-lookup"><span data-stu-id="87185-429">How many times do your websites include more than one JavaScript or CSS file?</span></span> <span data-ttu-id="87185-430">这是非常常见的方案，其中绑定和缩减可以帮助减少文件大小，而且使执行速度更快的站点。</span><span class="sxs-lookup"><span data-stu-id="87185-430">This is a very common scenario where bundling and minification can help to reduce the file size and make the site perform faster.</span></span> <span data-ttu-id="87185-431">ASP.NET 4.5 中的新捆绑功能插入单个元素，包一套 JS 或 CSS 文件，以及通过贴图层 （即删除不是必需的空白区域，删除注释，减少标识符） 的内容来减小其大小。</span><span class="sxs-lookup"><span data-stu-id="87185-431">The new bundling feature in ASP.NET 4.5 packs a set of JS or CSS files into a single element, and reduces its size by minifying the content ( i.e. removing not required blank spaces, removing comments, reducing identifiers ).</span></span>

<span data-ttu-id="87185-432">绑定和缩减 ASP.NET 4.5 中的执行在运行时，以便在过程可以标识用户代理 （例如 IE、 Mozilla，等等），并因此，通过针对用户的浏览器 （例如，删除内容的 Mozilla 特定来提高压缩当请求来自 IE）。</span><span class="sxs-lookup"><span data-stu-id="87185-432">Bundling and minification in ASP.NET 4.5 is performed at runtime, so that the process can identify the user agent (for example IE, Mozilla, etc), and thus, improve the compression by targeting the user browser (for instance, removing stuff that is Mozilla specific when the request comes from IE).</span></span>

<span data-ttu-id="87185-433">在此练习中，你将了解如何启用和使用 ASP.NET 4.5 中的不同类型的绑定和缩减。</span><span class="sxs-lookup"><span data-stu-id="87185-433">In this exercise, you will learn how to enable and use the different types of bundling and minification in ASP.NET 4.5.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a><span data-ttu-id="87185-434">任务 1-安装捆绑和缩减包从 NuGet</span><span class="sxs-lookup"><span data-stu-id="87185-434">Task 1 - Installing the Bundling and Minification Package from NuGet</span></span>

1. <span data-ttu-id="87185-435">如果尚未打开，启动**Visual Studio**并打开**WhatsNewASPNET.sln**解决方案位于**Source\WhatsNewASPNET**这个实验室的文件夹。</span><span class="sxs-lookup"><span data-stu-id="87185-435">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="87185-436">打开 NuGet 包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="87185-436">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="87185-437">若要执行此操作，请使用菜单**视图** | **其他窗口** | **程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="87185-437">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>

    <span data-ttu-id="87185-438">![打开程序包管理器 file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "打开包管理器控制台")</span><span class="sxs-lookup"><span data-stu-id="87185-438">![Opening the package manager file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "Opening the package manager console")</span></span>

    <span data-ttu-id="87185-439">*打开包管理器控制台*</span><span class="sxs-lookup"><span data-stu-id="87185-439">*Opening the package manager console*</span></span>
3. <span data-ttu-id="87185-440">在**程序包管理器控制台中，** 类型**安装包 Microsoft.Web.Optimization**按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="87185-440">In the **Package Manager Console,** type **Install-Package Microsoft.Web.Optimization** and press **ENTER**.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a><span data-ttu-id="87185-441">任务 2-默认捆绑包</span><span class="sxs-lookup"><span data-stu-id="87185-441">Task 2 - Default Bundles</span></span>

<span data-ttu-id="87185-442">使用绑定和缩减的最简单方法是启用的默认捆绑包。</span><span class="sxs-lookup"><span data-stu-id="87185-442">The simplest way to use bundling and minification is to enable the default bundles.</span></span> <span data-ttu-id="87185-443">此方法使用约定来让你引用 JS 和 CSS 文件的文件夹中的捆绑和缩减版本。</span><span class="sxs-lookup"><span data-stu-id="87185-443">This method uses conventions to let you reference the bundled and minified version for the JS and CSS files in a folder.</span></span>

<span data-ttu-id="87185-444">在此任务中，你将了解如何启用和引用捆绑和缩减型 JS 和 CSS 文件，查看生成的输出。</span><span class="sxs-lookup"><span data-stu-id="87185-444">In this task, you will learn how to enable and reference the bundled and minified JS and CSS files and view the resulting output.</span></span>

1. <span data-ttu-id="87185-445">如果尚未打开，启动**Visual Studio**并打开**WhatsNewASPNET.sln**解决方案位于**Source\WhatsNewASPNET**这个实验室的文件夹。</span><span class="sxs-lookup"><span data-stu-id="87185-445">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="87185-446">在**解决方案资源管理器**，展开**样式**， **Scripts\custom**和**Scripts\bundle**文件夹。</span><span class="sxs-lookup"><span data-stu-id="87185-446">In the **Solution Explorer**, expand the **Styles**, **Scripts\custom** and **Scripts\bundle** folders.</span></span>

    <span data-ttu-id="87185-447">请注意应用程序正在使用多个 CSS 和 JS 文件。</span><span class="sxs-lookup"><span data-stu-id="87185-447">Notice that the application is using more than one CSS and JS file.</span></span>

    <span data-ttu-id="87185-448">![应用程序中的多个样式表和 JavaScript 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "应用程序中的多个样式表和 JavaScript 文件")</span><span class="sxs-lookup"><span data-stu-id="87185-448">![Multiple Stylesheets and JavaScript files in the application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "Multiple Stylesheets and JavaScript files in the application")</span></span>

    <span data-ttu-id="87185-449">*应用程序中的多个样式表和 JavaScript 文件*</span><span class="sxs-lookup"><span data-stu-id="87185-449">*Multiple Stylesheets and JavaScript files in the application*</span></span>
3. <span data-ttu-id="87185-450">打开**Global.asax.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="87185-450">Open the **Global.asax.cs** file.</span></span>

    <span data-ttu-id="87185-451">请注意，新**Microsoft.Web.Optimization**命名空间被注释掉该文件的开头。</span><span class="sxs-lookup"><span data-stu-id="87185-451">Notice that the new **Microsoft.Web.Optimization** namespace is commented out at the beginning of the file.</span></span> <span data-ttu-id="87185-452">取消注释使用指令以包含绑定和缩减功能。</span><span class="sxs-lookup"><span data-stu-id="87185-452">Uncomment the using directive to include the bundling and minification features.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. <span data-ttu-id="87185-453">找到**应用程序\_启动**方法。</span><span class="sxs-lookup"><span data-stu-id="87185-453">Locate the **Application\_Start** method.</span></span>

    <span data-ttu-id="87185-454">在此方法中，取消注释 EnableDefaultBundles 调用，如下面的代码段中所示。</span><span class="sxs-lookup"><span data-stu-id="87185-454">In this method, uncomment the EnableDefaultBundles call as shown in the snippet below.</span></span> <span data-ttu-id="87185-455">这使我们能够通过使用该文件夹的路径引用的文件夹中的 CSS 文件捆绑的集合加上&quot;CSS&quot;或&quot;JS&quot;后缀。</span><span class="sxs-lookup"><span data-stu-id="87185-455">This enables us to reference a bundled collection of CSS files in a folder by using the path to that folder, plus the &quot;CSS&quot; or the &quot;JS&quot; suffix.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. <span data-ttu-id="87185-456">打开**Optimization.aspx**文件并找到的内容控件**HeadContent**。</span><span class="sxs-lookup"><span data-stu-id="87185-456">Open the **Optimization.aspx** file and locate the content control for **HeadContent**.</span></span>

    <span data-ttu-id="87185-457">请注意 CSS 文件和 JS 文件有一个引用的标记。</span><span class="sxs-lookup"><span data-stu-id="87185-457">Notice the CSS files and the JS files have a single referenced tag.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > <span data-ttu-id="87185-458">此代码是出于演示目的。</span><span class="sxs-lookup"><span data-stu-id="87185-458">This code is for demo purposes.</span></span> <span data-ttu-id="87185-459">理想情况下，将引用 Site.Master 文件中的捆绑包。</span><span class="sxs-lookup"><span data-stu-id="87185-459">Ideally, you will reference the bundles in the Site.Master file.</span></span> <span data-ttu-id="87185-460">在此示例代码中，你会发现，某些捆绑文件也被引用 Site.Master 文件，使此最后一个引用冗余。</span><span class="sxs-lookup"><span data-stu-id="87185-460">In this sample code, you will find that some of the bundled files are also being referenced by the Site.Master file, making this last reference redundant.</span></span>
6. <span data-ttu-id="87185-461">请注意，使用链接中的捆绑约定**href**属性从样式和 Scripts\custom 获取所有 CSS 或 JS 文件文件夹分别。</span><span class="sxs-lookup"><span data-stu-id="87185-461">Notice that the links are using the bundling conventions in the **href** attribute to get all the CSS or JS files from the Styles and Scripts\custom folder respectively.</span></span>

    <span data-ttu-id="87185-462">你可以使用路径**脚本/自定义/JS**如下所示捆绑和 minify 内的所有 JS 文件**自定义脚本/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="87185-462">You can use the path **Scripts/custom/JS** as shown below to bundle and minify all the JS files inside a **Scripts/custom** folder.</span></span> <span data-ttu-id="87185-463">这是默认捆绑包的默认行为。</span><span class="sxs-lookup"><span data-stu-id="87185-463">This is the default behavior with the default bundles.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. <span data-ttu-id="87185-464">打开**Styles\Site.css**文件。</span><span class="sxs-lookup"><span data-stu-id="87185-464">Open the **Styles\Site.css** file.</span></span>

    <span data-ttu-id="87185-465">请注意，原始的 CSS 文件包含缩进的代码、 空格和扩大文件的注释。</span><span class="sxs-lookup"><span data-stu-id="87185-465">Notice that the original CSS file contains indented code, blank spaces and comments that enlarge the file.</span></span> <span data-ttu-id="87185-466">（还 JavaScript 文件包含空格和注释）。</span><span class="sxs-lookup"><span data-stu-id="87185-466">(Also the JavaScript file contains blank spaces and comments).</span></span>

    <span data-ttu-id="87185-467">![在脚本文件夹中的其中一个原始 CSS 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "其中一个原始 CSS 文件的脚本文件夹中")</span><span class="sxs-lookup"><span data-stu-id="87185-467">![One of the original CSS files in the Scripts folder](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "One of the original CSS files in the Scripts folder")</span></span>

    <span data-ttu-id="87185-468">*在脚本文件夹中的原始 CSS 文件之一*</span><span class="sxs-lookup"><span data-stu-id="87185-468">*One of the original CSS files in the Scripts folder*</span></span>
8. <span data-ttu-id="87185-469">按**F5**运行该应用程序并导航到**优化**页。</span><span class="sxs-lookup"><span data-stu-id="87185-469">Press **F5** to run the application and navigate to the **Optimization** page.</span></span>
9. <span data-ttu-id="87185-470">单击**CSS 捆绑包**链接以下载并打开文件。</span><span class="sxs-lookup"><span data-stu-id="87185-470">Click on the **CSS Bundle** link to download and open the file.</span></span>

    <span data-ttu-id="87185-471">签出缩减捆绑文件。</span><span class="sxs-lookup"><span data-stu-id="87185-471">Check out the minified bundled file.</span></span> <span data-ttu-id="87185-472">你将注意到，已删除所有空格、 注释和缩进字符，生成较小的文件。</span><span class="sxs-lookup"><span data-stu-id="87185-472">You will notice that all the blank spaces, comments and indentation characters have been removed, generating a smaller file.</span></span>

    <span data-ttu-id="87185-473">![捆绑 CSS 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "捆绑 CSS 文件")</span><span class="sxs-lookup"><span data-stu-id="87185-473">![Bundled CSS files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Bundled CSS files")</span></span>

    <span data-ttu-id="87185-474">*捆绑的 CSS 文件*</span><span class="sxs-lookup"><span data-stu-id="87185-474">*Bundled CSS files*</span></span>
10. <span data-ttu-id="87185-475">现在，请单击**JS 捆绑**链接以打开捆绑在一起的 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="87185-475">Now click the **JS Bundle** link to open the JavaScript bundled file.</span></span> <span data-ttu-id="87185-476">你可以放心地忽略警告的资源管理器。</span><span class="sxs-lookup"><span data-stu-id="87185-476">You can safely disregard the explorer warning.</span></span> <span data-ttu-id="87185-477">请注意下的 JavaScript 文件**自定义**文件夹也将捆绑的和缩减。</span><span class="sxs-lookup"><span data-stu-id="87185-477">Notice the JavaScript files under the **custom** folder are also bundled and minified.</span></span>

    <span data-ttu-id="87185-478">![捆绑 JavaScript 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "捆绑 JavaScript 文件")</span><span class="sxs-lookup"><span data-stu-id="87185-478">![Bundled JavaScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Bundled JavaScript files")</span></span>

    <span data-ttu-id="87185-479">*捆绑的 JavaScript 文件*</span><span class="sxs-lookup"><span data-stu-id="87185-479">*Bundled JavaScript files*</span></span>

    <span data-ttu-id="87185-480">ASP.NET 的早期版本中，启用压缩，从而提供 CSS 或 JS 文件时非常复杂。</span><span class="sxs-lookup"><span data-stu-id="87185-480">Enabling compression for CSS or JS files was much more complicated in previous ASP.NET version.</span></span> <span data-ttu-id="87185-481">现在，正如你所看到的你只需添加中的一行*Global.asax*文件来启用绑定，，然后从你的站点引用捆绑的文件。</span><span class="sxs-lookup"><span data-stu-id="87185-481">Now, as you have seen, you just need to add one line in the *Global.asax* file to enable bundling, and then reference the bundled files from your site.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a><span data-ttu-id="87185-482">任务 3-静态捆绑包</span><span class="sxs-lookup"><span data-stu-id="87185-482">Task 3 - Static Bundles</span></span>

<span data-ttu-id="87185-483">静态捆绑方法允许你自定义捆绑、 引用和缩减方法将使用的文件组。</span><span class="sxs-lookup"><span data-stu-id="87185-483">The static bundle approach allows you to customize the set of files to bundle, the reference and the minification method that will be used.</span></span>

<span data-ttu-id="87185-484">在此任务中，你将配置静态的捆绑包来定义一组特定的捆绑和 minify 的文件。</span><span class="sxs-lookup"><span data-stu-id="87185-484">In this task, you will configure a static bundle to define a specific set of files to bundle and minify.</span></span>

1. <span data-ttu-id="87185-485">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="87185-485">Close the browser.</span></span>
2. <span data-ttu-id="87185-486">打开**Global.asax.cs**文件并找到**应用程序\_启动**方法。</span><span class="sxs-lookup"><span data-stu-id="87185-486">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
3. <span data-ttu-id="87185-487">取消注释下面的代码中所示的静态捆绑代码。</span><span class="sxs-lookup"><span data-stu-id="87185-487">Uncomment the static bundle code as shown in the code below.</span></span>

    <span data-ttu-id="87185-488">定义将使用引用的静态捆绑&quot; **~/StaticBundle** &quot;虚拟路径和使用**JsMinify**与所有指定的文件的缩减为**AddFile**方法。</span><span class="sxs-lookup"><span data-stu-id="87185-488">You are defining a static bundle that will be referenced with the &quot;**~/StaticBundle**&quot; virtual path and use **JsMinify** for minification of all the specified files with the **AddFile** method.</span></span> <span data-ttu-id="87185-489">最后，要添加到此静态捆绑**BundleTable**和启用它。</span><span class="sxs-lookup"><span data-stu-id="87185-489">Finally, you are adding the static bundle to the **BundleTable** and enabling it.</span></span>

    <span data-ttu-id="87185-490">请注意，文件不位于同一位置;这是通过默认绑定的另一个优点。</span><span class="sxs-lookup"><span data-stu-id="87185-490">Notice that the files are not located in the same place; this is another advantage over the default bundling.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. <span data-ttu-id="87185-491">打开**Optimization.aspx**文件。</span><span class="sxs-lookup"><span data-stu-id="87185-491">Open the **Optimization.aspx** file.</span></span>

    <span data-ttu-id="87185-492">请注意，链接到**静态 JS 捆绑**正在使用时的 Global.asax.cs 文件中配置静态捆绑已声明的路径： **/StaticBundle**。</span><span class="sxs-lookup"><span data-stu-id="87185-492">Notice that the link to **Static JS Bundle** is using the path you have declared when you configured the static bundle in the Global.asax.cs file: **/StaticBundle**.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. <span data-ttu-id="87185-493">按**F5**以运行该应用程序，然后导航到**优化**页。</span><span class="sxs-lookup"><span data-stu-id="87185-493">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
6. <span data-ttu-id="87185-494">单击**静态 JS 捆绑**链接以打开该文件。</span><span class="sxs-lookup"><span data-stu-id="87185-494">Click on the **Static JS Bundle** link to open the file.</span></span>

    <span data-ttu-id="87185-495">请注意缩减捆绑 JavaScript 文件是在路径下的静态捆绑文件中配置的所有 JavaScript 文件的输出&quot;/StaticBundle&quot;。</span><span class="sxs-lookup"><span data-stu-id="87185-495">Notice that the minified bundled JavaScript file is the output for all the JavaScript files configured in the static bundle file under the path &quot;/StaticBundle&quot;.</span></span>

    <span data-ttu-id="87185-496">![静态 JavaScript 文件捆绑](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "静态 JavaScript 文件捆绑")</span><span class="sxs-lookup"><span data-stu-id="87185-496">![Static JavaScript files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "Static JavaScript files bundle")</span></span>

    <span data-ttu-id="87185-497">*静态 JavaScript 文件捆绑在一起*</span><span class="sxs-lookup"><span data-stu-id="87185-497">*Static JavaScript files bundle*</span></span>
7. <span data-ttu-id="87185-498">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="87185-498">Close the browser and return to Visual Studio.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a><span data-ttu-id="87185-499">任务 4-动态文件夹捆绑包</span><span class="sxs-lookup"><span data-stu-id="87185-499">Task 4 - Dynamic Folder Bundles</span></span>

<span data-ttu-id="87185-500">在此任务中，你将了解如何配置动态文件夹捆绑包。</span><span class="sxs-lookup"><span data-stu-id="87185-500">In this task, you will learn how to configure dynamic folder bundles.</span></span> <span data-ttu-id="87185-501">可以包含静态 JavaScript，以及其他文件编译到 JavaScript 的语言中，因此，需要进行一些处理绑定执行前可以为动态绑定的权限。</span><span class="sxs-lookup"><span data-stu-id="87185-501">The power of dynamic bundling is that you can include static JavaScript, as well as other files in languages that compiles into JavaScript, and thus, require some processing before the bundling is executed.</span></span>

<span data-ttu-id="87185-502">在此示例中，您将学习如何使用**DynamicFolderBundle**类来创建一个动态绑定的 CofeeScript 中编写的文件。</span><span class="sxs-lookup"><span data-stu-id="87185-502">In this example, you will learn how to use the **DynamicFolderBundle** class to create a dynamic bundle for files written in CofeeScript.</span></span> <span data-ttu-id="87185-503">CofeeScript 是一种编程语言，编译到 JavaScript 并为编写 JavaScript 代码，从而加强 JavaScript 的简洁起见和可读性提供更简单的语法。</span><span class="sxs-lookup"><span data-stu-id="87185-503">CofeeScript is a programming language that compiles into JavaScript and provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability.</span></span>

1. <span data-ttu-id="87185-504">打开**Global.asax.cs**文件并找到**应用程序\_启动**方法。</span><span class="sxs-lookup"><span data-stu-id="87185-504">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
2. <span data-ttu-id="87185-505">取消注释下面的代码中所示的动态捆绑代码。</span><span class="sxs-lookup"><span data-stu-id="87185-505">Uncomment the dynamic bundle code as shown in the code below.</span></span>

    <span data-ttu-id="87185-506">定义将使用的动态文件夹捆绑**CoffeeMinify**将仅应用到的文件的自定义缩减处理器&quot; **.coffee** &quot;扩展 (CoffeeScript 文件）。</span><span class="sxs-lookup"><span data-stu-id="87185-506">You are defining a dynamic folder bundle that will use the **CoffeeMinify** custom minification processor that will only apply to the files with the &quot;**.coffee**&quot; extension (CoffeeScript files).</span></span> <span data-ttu-id="87185-507">请注意，你可以使用的搜索模式以选择要在文件夹中，如捆绑的文件\*.coffee。</span><span class="sxs-lookup"><span data-stu-id="87185-507">Notice that you can use a search pattern to select the files to bundle within a folder, like '\*.coffee'.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. <span data-ttu-id="87185-508">打开 NuGet 包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="87185-508">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="87185-509">若要执行此操作，请使用菜单**视图** | **其他窗口** | **程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="87185-509">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>
4. <span data-ttu-id="87185-510">在**程序包管理器控制台中，** 类型**安装包 CoffeeSharp**按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="87185-510">In the **Package Manager Console,** type **Install-Package CoffeeSharp** and press **ENTER**.</span></span>
5. <span data-ttu-id="87185-511">单击**显示所有文件**按钮**解决方案资源管理器**窗口</span><span class="sxs-lookup"><span data-stu-id="87185-511">Click the **Show All Files** button in the **Solution Explorer** window</span></span>

    <span data-ttu-id="87185-512">![显示的所有文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "都显示的所有文件")</span><span class="sxs-lookup"><span data-stu-id="87185-512">![Showing all files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "Showing all files")</span></span>

    <span data-ttu-id="87185-513">*显示的所有文件*</span><span class="sxs-lookup"><span data-stu-id="87185-513">*Showing all files*</span></span>
6. <span data-ttu-id="87185-514">右键单击**CoffeeMinify.cs**文件中**解决方案资源管理器**和选择**包括在项目中**</span><span class="sxs-lookup"><span data-stu-id="87185-514">Right click the **CoffeeMinify.cs** file in the **Solution Explorer** and select **Include in Project**</span></span>

    <span data-ttu-id="87185-515">![在项目中包含 CoffeeMinify.cs 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "在项目中包含 CoffeeMinify.cs 文件")</span><span class="sxs-lookup"><span data-stu-id="87185-515">![Include the CoffeeMinify.cs file in the project](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "Include the CoffeeMinify.cs file in the project")</span></span>

    <span data-ttu-id="87185-516">*在项目中包含 CoffeeMinify.cs 文件*</span><span class="sxs-lookup"><span data-stu-id="87185-516">*Include the CoffeeMinify.cs file in the project*</span></span>
7. <span data-ttu-id="87185-517">打开**CoffeeMinify.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="87185-517">Open the **CoffeeMinify.cs** file.</span></span>

    <span data-ttu-id="87185-518">此类继承自 JsMinify 以 minify JavaScript 输出的 CoffeeScript 代码编译引起的。</span><span class="sxs-lookup"><span data-stu-id="87185-518">This class inherits from JsMinify to minify the JavaScript output resulting from the CoffeeScript code compilation.</span></span> <span data-ttu-id="87185-519">它调用 CoffeeScript 编译器首先，生成的 JavaScript 代码，然后将它发送到 JsMinify.Process 方法以 minify 生成的代码。</span><span class="sxs-lookup"><span data-stu-id="87185-519">It calls the CoffeeScript compiler to generate the JavaScript code first, and then it sends it to the JsMinify.Process method to minify the resulting code.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. <span data-ttu-id="87185-520">打开**Script1.coffee**和**Script2.coffee**文件从**脚本/捆绑**文件夹。</span><span class="sxs-lookup"><span data-stu-id="87185-520">Open the **Script1.coffee** and **Script2.coffee** files from the **Scripts/bundle** folder.</span></span>

    <span data-ttu-id="87185-521">这些文件将包括 CoffeScript 代码执行与 CoffeeMinify 类绑定时编译。</span><span class="sxs-lookup"><span data-stu-id="87185-521">These files will include the CoffeScript code to be compiled while performing the bundling with the CoffeeMinify class.</span></span>

    <span data-ttu-id="87185-522">为了简单起见，提供的 CoffeeScript 文件仅包含 CoffeeScript 示例代码。</span><span class="sxs-lookup"><span data-stu-id="87185-522">For simplicity purposes, the CoffeeScript files provided are only including CoffeeScript sample code.</span></span> <span data-ttu-id="87185-523">注释排除的 JsMinify 过程。</span><span class="sxs-lookup"><span data-stu-id="87185-523">The comments are excluded by the JsMinify process.</span></span>

    <span data-ttu-id="87185-524">![CoffeeScript 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript 文件")</span><span class="sxs-lookup"><span data-stu-id="87185-524">![CoffeeScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript files")</span></span>

    <span data-ttu-id="87185-525">*CoffeeScript 文件*</span><span class="sxs-lookup"><span data-stu-id="87185-525">*CoffeeScript files*</span></span>

    > [!NOTE]
    > <span data-ttu-id="87185-526">[CofeeScript](https://github.com/jashkenas/coffeescript/)提供更简单的语法来编写 JavaScript 代码、 增强了 JavaScript 的简洁起见和可读性，以及添加其他功能，如数组理解和模式匹配。</span><span class="sxs-lookup"><span data-stu-id="87185-526">[CofeeScript](https://github.com/jashkenas/coffeescript/) provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability, as well as adding other features like array comprehension and pattern matching.</span></span>
9. <span data-ttu-id="87185-527">打开**Optimization.aspx**文件并找到的捆绑包链接。</span><span class="sxs-lookup"><span data-stu-id="87185-527">Open the **Optimization.aspx** file and locate the bundle links.</span></span>

    <span data-ttu-id="87185-528">请注意，链接到**动态 JS 捆绑**正在引用**脚本/捆绑**文件夹使用 **/咖啡**动态文件夹捆绑包配置的后缀。</span><span class="sxs-lookup"><span data-stu-id="87185-528">Notice that the link to **Dynamic JS Bundle** is referencing the **Scripts/bundle** folder by using the **/Coffee** suffix you configured for the dynamic folder bundle.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. <span data-ttu-id="87185-529">按**F5**以运行该应用程序，然后导航到**优化**页。</span><span class="sxs-lookup"><span data-stu-id="87185-529">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
11. <span data-ttu-id="87185-530">单击**动态 JS 捆绑**链接以打开生成的文件。</span><span class="sxs-lookup"><span data-stu-id="87185-530">Click on the **Dynamic JS Bundle** link to open the generated file.</span></span>

    <span data-ttu-id="87185-531">请注意，此包中包含的内容仅包含 **.coffee**文件。</span><span class="sxs-lookup"><span data-stu-id="87185-531">Notice that the content that was included in this bundle only contains **.coffee** files.</span></span> <span data-ttu-id="87185-532">你还可以看到 CoffeeScript 代码已编译为 JavaScript 和注释掉的行已删除。</span><span class="sxs-lookup"><span data-stu-id="87185-532">You can also see that the CoffeeScript code was compiled to JavaScript and the commented-out lines has been removed.</span></span>

    <span data-ttu-id="87185-533">![动态 JS 文件捆绑](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "动态 JS 文件捆绑")</span><span class="sxs-lookup"><span data-stu-id="87185-533">![Dynamic JS files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "Dynamic JS files bundle")</span></span>

    <span data-ttu-id="87185-534">*动态 JS 文件捆绑在一起*</span><span class="sxs-lookup"><span data-stu-id="87185-534">*Dynamic JS files bundle*</span></span>

> [!NOTE]
> <span data-ttu-id="87185-535">此外，你可以部署此应用程序对 Windows Azure 网站以下[附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web Deploy](#AppendixB)。</span><span class="sxs-lookup"><span data-stu-id="87185-535">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="87185-536">总结</span><span class="sxs-lookup"><span data-stu-id="87185-536">Summary</span></span>

<span data-ttu-id="87185-537">此实验室可帮助你了解 ASP.NET 中的新增功能和 Visual Studio 2012 中的 Web 开发是什么以及如何利用 Visual Studio 2012 中的许多增强功能。</span><span class="sxs-lookup"><span data-stu-id="87185-537">This lab helps you to understand what New in ASP.NET and Web Development in Visual Studio 2012 is and how to take advantage of the variety of enhancements in Visual Studio 2012.</span></span>

<span data-ttu-id="87185-538">通过完成本动手实验，您已了解到如何在 Visual Studio 2012 编辑器中使用的新功能和改进，CSS、 JavaScript 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="87185-538">By completing this Hands-On Lab, you have learnt how to use the new features and improvements in Visual Studio 2012 Editors for CSS, JavaScript and HTML.</span></span> <span data-ttu-id="87185-539">此外，您已了解到 Visual Studio 2012 内置绑定和缩减的实现。</span><span class="sxs-lookup"><span data-stu-id="87185-539">In addition, you have learnt how Visual Studio 2012 implements built-in bundling and minification.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="87185-540">附录 a： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="87185-540">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="87185-541">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;版本使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="87185-541">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="87185-542">以下说明将指导你完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="87185-542">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="87185-543">转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="87185-543">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="87185-544">或者，如果你已安装 Web 平台安装程序，你可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 的 Windows Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="87185-544">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="87185-545">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="87185-545">Click on **Install Now**.</span></span> <span data-ttu-id="87185-546">如果你没有**Web 平台安装程序**将重定向以下载并请先安装它。</span><span class="sxs-lookup"><span data-stu-id="87185-546">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="87185-547">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="87185-547">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="87185-548">![安装 Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="87185-548">![Install Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="87185-549">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="87185-549">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="87185-550">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="87185-550">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    <span data-ttu-id="87185-552">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="87185-552">*Accepting the license terms*</span></span>
5. <span data-ttu-id="87185-553">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="87185-553">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    <span data-ttu-id="87185-555">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="87185-555">*Installation progress*</span></span>
6. <span data-ttu-id="87185-556">当安装完成后时，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="87185-556">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    <span data-ttu-id="87185-558">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="87185-558">*Installation completed*</span></span>
7. <span data-ttu-id="87185-559">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="87185-559">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="87185-560">若要打开 Visual Studio Express for Web，请转到**启动**屏幕并开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="87185-560">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web 磁贴的 VS Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    <span data-ttu-id="87185-562">*Web 磁贴的 VS Express*</span><span class="sxs-lookup"><span data-stu-id="87185-562">*VS Express for Web tile*</span></span>

* * *

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="87185-563">附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="87185-563">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="87185-564">本附录将演示如何从 Windows Azure 管理门户创建新的网站和发布应用程序获取按照本实验中，利用 Windows Azure 提供的 Web 部署发布功能。</span><span class="sxs-lookup"><span data-stu-id="87185-564">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="87185-565">任务 1-创建新的 Web 站点从 Windows Azure 门户</span><span class="sxs-lookup"><span data-stu-id="87185-565">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="87185-566">转到[Windows Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="87185-566">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="87185-567">使用 Windows Azure 可以免费承载 10 个 ASP.NET 网站，然后随着流量增长而扩展。</span><span class="sxs-lookup"><span data-stu-id="87185-567">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="87185-568">你可以注册[此处](http://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="87185-568">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="87185-569">![登录到 Windows Azure 门户](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "登录到 Windows Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="87185-569">![Log on to Windows Azure portal](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="87185-570">*登录到 Windows Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="87185-570">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="87185-571">单击**新建**命令栏上。</span><span class="sxs-lookup"><span data-stu-id="87185-571">Click **New** on the command bar.</span></span>

    <span data-ttu-id="87185-572">![创建新网站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "创建新网站")</span><span class="sxs-lookup"><span data-stu-id="87185-572">![Creating a new Web Site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="87185-573">*创建新网站*</span><span class="sxs-lookup"><span data-stu-id="87185-573">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="87185-574">单击**计算** | **网站**。</span><span class="sxs-lookup"><span data-stu-id="87185-574">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="87185-575">然后选择**快速创建**选项。</span><span class="sxs-lookup"><span data-stu-id="87185-575">Then select **Quick Create** option.</span></span> <span data-ttu-id="87185-576">为新网站提供可用的 URL，然后单击**创建网站**。</span><span class="sxs-lookup"><span data-stu-id="87185-576">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="87185-577">Windows Azure 网站是在云中，你可以控制和管理运行的 web 应用程序的宿主。</span><span class="sxs-lookup"><span data-stu-id="87185-577">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="87185-578">快速创建选项，可将已完成的 web 应用程序到 Windows Azure 网站从在门户外部部署。</span><span class="sxs-lookup"><span data-stu-id="87185-578">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="87185-579">它不包括用于设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="87185-579">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="87185-580">![创建新的网站使用快速创建](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "创建新的网站使用快速创建")</span><span class="sxs-lookup"><span data-stu-id="87185-580">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="87185-581">*创建新的网站使用快速创建*</span><span class="sxs-lookup"><span data-stu-id="87185-581">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="87185-582">等到新**网站**创建。</span><span class="sxs-lookup"><span data-stu-id="87185-582">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="87185-583">创建网站后单击下的链接**URL**列。</span><span class="sxs-lookup"><span data-stu-id="87185-583">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="87185-584">检查新的 Web 站点工作。</span><span class="sxs-lookup"><span data-stu-id="87185-584">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="87185-585">![浏览到新的 web 站点](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "浏览到新的 web 站点")</span><span class="sxs-lookup"><span data-stu-id="87185-585">![Browsing to the new web site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="87185-586">*浏览到新的 web 站点*</span><span class="sxs-lookup"><span data-stu-id="87185-586">*Browsing to the new web site*</span></span>

    <span data-ttu-id="87185-587">![运行网站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "运行的网站")</span><span class="sxs-lookup"><span data-stu-id="87185-587">![Web site running](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "Web site running")</span></span>

    <span data-ttu-id="87185-588">*运行的网站*</span><span class="sxs-lookup"><span data-stu-id="87185-588">*Web site running*</span></span>
6. <span data-ttu-id="87185-589">返回到门户并单击在网站的名称**名称**列以显示的管理页。</span><span class="sxs-lookup"><span data-stu-id="87185-589">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="87185-590">![打开网站管理页](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="87185-590">![Opening the web site management pages](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="87185-591">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="87185-591">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="87185-592">在**仪表板**页上，在**速览**部分中，单击**下载发布配置文件**链接。</span><span class="sxs-lookup"><span data-stu-id="87185-592">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="87185-593">*发布配置文件*包含所有 web 应用程序发布到 Windows Azure 网站中的每个启用的发布方法所需的信息。</span><span class="sxs-lookup"><span data-stu-id="87185-593">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="87185-594">发布配置文件包含的 Url、 用户凭据和连接到并针对每个发布方法启用的终结点进行身份验证所需的数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="87185-594">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="87185-595">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件以自动执行的这些程序，以便配置web 应用程序发布到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="87185-595">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="87185-596">![下载网站发布配置文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="87185-596">![Downloading the web site publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="87185-597">*下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="87185-597">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="87185-598">到一个已知位置下载发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="87185-598">Download the publish profile file to a known location.</span></span> <span data-ttu-id="87185-599">进一步在本练习中您将了解如何使用此文件来发布 Visual Studio 中的 web 应用程序到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="87185-599">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="87185-600">![保存发布配置文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="87185-600">![Saving the publish profile file](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "Saving the publish profile")</span></span>

    <span data-ttu-id="87185-601">*保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="87185-601">*Saving the publish profile file*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="87185-602">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="87185-602">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="87185-603">如果你的应用程序将使用 SQL Server 数据库将需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="87185-603">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="87185-604">如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="87185-604">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="87185-605">需要将用于存储应用程序数据库的 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="87185-605">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="87185-606">你可以从你的订阅在 Windows Azure 管理门户中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**。</span><span class="sxs-lookup"><span data-stu-id="87185-606">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="87185-607">如果你没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。</span><span class="sxs-lookup"><span data-stu-id="87185-607">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="87185-608">请记下的**服务器名称和 URL、 管理员登录名和密码**，如你将在接下来的任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="87185-608">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="87185-609">不创建数据库，它将在后面的阶段中创建。</span><span class="sxs-lookup"><span data-stu-id="87185-609">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="87185-610">![SQL 数据库服务器仪表板](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database 服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="87185-610">![SQL Database Server Dashboard](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="87185-611">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="87185-611">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="87185-612">在下一个任务将测试从 Visual Studio 中，数据库连接，因此你需要在的服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。</span><span class="sxs-lookup"><span data-stu-id="87185-612">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="87185-613">若要做到这一点，请单击**配置**，选择的 IP 地址从**当前客户端 IP 地址**并将其粘贴在**起始 IP 地址**和**结束 IP 地址**文本框。</span><span class="sxs-lookup"><span data-stu-id="87185-613">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes.</span></span> <span data-ttu-id="87185-614">输入规则的名称，然后单击![add-client-ip-address-ok-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png)按钮。</span><span class="sxs-lookup"><span data-stu-id="87185-614">Enter a name for the rule and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) button.</span></span>

    ![添加客户端 IP 地址](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    <span data-ttu-id="87185-616">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="87185-616">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="87185-617">一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。</span><span class="sxs-lookup"><span data-stu-id="87185-617">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认做的更改](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    <span data-ttu-id="87185-619">*确认做的更改*</span><span class="sxs-lookup"><span data-stu-id="87185-619">*Confirm Changes*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="87185-620">任务 3-发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="87185-620">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="87185-621">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="87185-621">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="87185-622">在**解决方案资源管理器**，右键单击网站项目，然后选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="87185-622">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="87185-623">![发布应用程序](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="87185-623">![Publishing the Application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "Publishing the Application")</span></span>

    <span data-ttu-id="87185-624">*发布此网站*</span><span class="sxs-lookup"><span data-stu-id="87185-624">*Publishing the web site*</span></span>
2. <span data-ttu-id="87185-625">导入发布配置文件保存在第一个任务。</span><span class="sxs-lookup"><span data-stu-id="87185-625">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="87185-626">![导入发布配置文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="87185-626">![Importing the publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "Importing the publish profile")</span></span>

    <span data-ttu-id="87185-627">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="87185-627">*Importing publish profile*</span></span>
3. <span data-ttu-id="87185-628">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="87185-628">Click **Validate Connection**.</span></span> <span data-ttu-id="87185-629">验证完成后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="87185-629">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="87185-630">请参阅验证连接按钮旁边将显示绿色的复选标记后，验证已完成。</span><span class="sxs-lookup"><span data-stu-id="87185-630">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="87185-631">![正在验证连接](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "验证连接")</span><span class="sxs-lookup"><span data-stu-id="87185-631">![Validating connection](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "Validating connection")</span></span>

    <span data-ttu-id="87185-632">*正在验证连接*</span><span class="sxs-lookup"><span data-stu-id="87185-632">*Validating connection*</span></span>
4. <span data-ttu-id="87185-633">在**设置**页上，在**数据库**部分中，单击你的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="87185-633">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="87185-634">![Web 部署配置](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="87185-634">![Web deploy configuration](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web deploy configuration")</span></span>

    <span data-ttu-id="87185-635">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="87185-635">*Web deploy configuration*</span></span>
5. <span data-ttu-id="87185-636">配置数据库连接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="87185-636">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="87185-637">在**服务器名称**类型 SQL 数据库服务器 URL 使用*tcp:* 前缀。</span><span class="sxs-lookup"><span data-stu-id="87185-637">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="87185-638">在**用户名**键入您的服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="87185-638">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="87185-639">在**密码**键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="87185-639">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="87185-640">键入新的数据库名称，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="87185-640">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="87185-641">![配置目标连接字符串](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="87185-641">![Configuring destination connection string](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="87185-642">*配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="87185-642">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="87185-643">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="87185-643">Then click **OK**.</span></span> <span data-ttu-id="87185-644">当系统提示创建数据库单击**是**。</span><span class="sxs-lookup"><span data-stu-id="87185-644">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="87185-645">![创建数据库](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="87185-645">![Creating the database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "Creating the database string")</span></span>

    <span data-ttu-id="87185-646">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="87185-646">*Creating the database*</span></span>
7. <span data-ttu-id="87185-647">在默认连接文本框中显示了将用于连接到 Windows Azure 中的 SQL 数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="87185-647">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="87185-648">然后，单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="87185-648">Then click **Next**.</span></span>

    <span data-ttu-id="87185-649">![连接字符串指向 SQL 数据库](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "指向 SQL 数据库的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="87185-649">![Connection string pointing to SQL Database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="87185-650">*连接字符串指向 SQL 数据库*</span><span class="sxs-lookup"><span data-stu-id="87185-650">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="87185-651">在**预览**页上，单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="87185-651">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="87185-652">![Web 应用程序发布](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="87185-652">![Publishing the web application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Publishing the web application")</span></span>

    <span data-ttu-id="87185-653">*发布 web 应用程序*</span><span class="sxs-lookup"><span data-stu-id="87185-653">*Publishing the web application*</span></span>
9. <span data-ttu-id="87185-654">完成发布过程后，默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="87185-654">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="87185-655">![应用程序发布到 Windows Azure](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "应用程序发布到 Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="87185-655">![Application published to Windows Azure](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="87185-656">*应用程序发布到 Windows Azure*</span><span class="sxs-lookup"><span data-stu-id="87185-656">*Application published to Windows Azure*</span></span>
