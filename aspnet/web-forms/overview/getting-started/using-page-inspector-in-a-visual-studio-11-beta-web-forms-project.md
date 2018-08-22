---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: Visual Studio 2012 中 ASP.NET Web 窗体使用 Page Inspector |Microsoft Docs
author: rick-anderson
description: 适用于 Visual Studio 2012 的 Page Inspector 是一个 web 开发工具，使用集成浏览器。 集成的浏览器和 Page Inspector 中选择任何元素...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: d2c377f8466f8f324b75ce60860aa00c11bc0ffe
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826017"
---
<a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a><span data-ttu-id="edf0d-104">适用于 ASP.NET Web 窗体中的 Visual Studio 2012 中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="edf0d-104">Using Page Inspector for Visual Studio 2012 in ASP.NET Web Forms</span></span>
====================
<span data-ttu-id="edf0d-105">由 Tim Ammann</span><span class="sxs-lookup"><span data-stu-id="edf0d-105">by Tim Ammann</span></span>

> <span data-ttu-id="edf0d-106">适用于 Visual Studio 2012 的 Page Inspector 是一个 web 开发工具，使用集成浏览器。</span><span class="sxs-lookup"><span data-stu-id="edf0d-106">Page Inspector for Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="edf0d-107">在集成浏览器中选择任何元素和 Page Inspector 立即突出显示元素的源和 CSS。</span><span class="sxs-lookup"><span data-stu-id="edf0d-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="edf0d-108">可以在应用程序中浏览任何页面、 快速查找呈现的标记的源和使用 Visual Studio 环境中的浏览器工具。</span><span class="sxs-lookup"><span data-stu-id="edf0d-108">You can browse any page in your application, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> <span data-ttu-id="edf0d-109">此教程 shwos 如何启用检查模式下，然后快速查找和编辑 CSS 规则和你的 web 项目中的文本。</span><span class="sxs-lookup"><span data-stu-id="edf0d-109">This tutorial shwos how to enable Inspection Mode and then quickly locate and edit CSS rules and text within your web project.</span></span> <span data-ttu-id="edf0d-110">本教程使用 Web 窗体应用程序项目中，但您也可以使用 Page Inspector 对于网站项目并[MVC](https://go.microsoft.com/?linkid=9802002)应用程序。</span><span class="sxs-lookup"><span data-stu-id="edf0d-110">The tutorial uses a Web Forms Application Project, but you can also use Page Inspector for Web Site projects and [MVC](https://go.microsoft.com/?linkid=9802002) applications.</span></span>
> 
> <span data-ttu-id="edf0d-111">本教程包含以下部分：</span><span class="sxs-lookup"><span data-stu-id="edf0d-111">The tutorial has the following sections:</span></span>
> 
> [<span data-ttu-id="edf0d-112">先决条件</span><span class="sxs-lookup"><span data-stu-id="edf0d-112">Prerequisites</span></span>](#_1_prerequisites)
> 
> [<span data-ttu-id="edf0d-113">创建 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="edf0d-113">Create a Web Application</span></span>](#_2_creating_a)
> 
> [<span data-ttu-id="edf0d-114">使用 Page Inspector 查看应用程序</span><span class="sxs-lookup"><span data-stu-id="edf0d-114">Use Page Inspector to View the Application</span></span>](#_3_using_page)
> 
> [<span data-ttu-id="edf0d-115">启用检查模式</span><span class="sxs-lookup"><span data-stu-id="edf0d-115">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> 
> [<span data-ttu-id="edf0d-116">使用 Page Inspector 对标记进行的更改</span><span class="sxs-lookup"><span data-stu-id="edf0d-116">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> 
> [<span data-ttu-id="edf0d-117">检查模式下和 HTML 窗口</span><span class="sxs-lookup"><span data-stu-id="edf0d-117">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> 
> [<span data-ttu-id="edf0d-118">在样式窗口中预览 CSS 更改</span><span class="sxs-lookup"><span data-stu-id="edf0d-118">Preview CSS Changes in the Styles Window</span></span>](#_7_previewing_css)
> 
> [<span data-ttu-id="edf0d-119">CSS 自动同步</span><span class="sxs-lookup"><span data-stu-id="edf0d-119">CSS Auto Sync</span></span>](#css_auto_sync)
> 
> [<span data-ttu-id="edf0d-120">使用 CSS 颜色选取器</span><span class="sxs-lookup"><span data-stu-id="edf0d-120">Using the CSS Color Picker</span></span>](#css_color_picker)


<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="edf0d-121">系统必备</span><span class="sxs-lookup"><span data-stu-id="edf0d-121">Prerequisites</span></span>

- <span data-ttu-id="edf0d-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11)或[Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="edf0d-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="edf0d-123">若要获取 Page Inspector 的最新版本，请使用[Web 平台安装程序](https://go.microsoft.com/fwlink/?LinkId=255386)要安装 Azure SDK for.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="edf0d-123">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Azure SDK for .NET 2.0.</span></span>


<span data-ttu-id="edf0d-124">Page Inspector 与 Microsoft Web 开发人员工具捆绑在一起。</span><span class="sxs-lookup"><span data-stu-id="edf0d-124">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="edf0d-125">最新版本是 1.3。</span><span class="sxs-lookup"><span data-stu-id="edf0d-125">The latest version is 1.3.</span></span> <span data-ttu-id="edf0d-126">若要检查的版本，运行 Visual Studio 并选择**关于 Microsoft Visual Studio**从**帮助**菜单。</span><span class="sxs-lookup"><span data-stu-id="edf0d-126">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="edf0d-127">创建 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="edf0d-127">Create a Web Application</span></span>

<span data-ttu-id="edf0d-128">首先，将创建的 web 应用程序将使用与 Page Inspector。</span><span class="sxs-lookup"><span data-stu-id="edf0d-128">First, you will create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="edf0d-129">在 Visual Studio 中，选择**文件** &gt; **新项目**。</span><span class="sxs-lookup"><span data-stu-id="edf0d-129">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="edf0d-130">在左侧，展开**Visual C#**，选择**Web**，然后选择**ASP.NET Web 窗体应用程序**。</span><span class="sxs-lookup"><span data-stu-id="edf0d-130">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET Web Forms Application**.</span></span>

![新 Web 窗体应用程序](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

<span data-ttu-id="edf0d-132">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="edf0d-132">Click **OK**.</span></span>

<span data-ttu-id="edf0d-133">应用程序中打开**源**视图。</span><span class="sxs-lookup"><span data-stu-id="edf0d-133">The application opens in **Source** view.</span></span>

![在源视图中的新 Web 窗体应用程序](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

<span data-ttu-id="edf0d-135">现在，已有要使用的应用程序，可以使用 Page Inspector 检查并对其进行修改。</span><span class="sxs-lookup"><span data-stu-id="edf0d-135">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a><span data-ttu-id="edf0d-136">使用 Page Inspector 查看应用程序</span><span class="sxs-lookup"><span data-stu-id="edf0d-136">Use Page Inspector to View the Application</span></span>

<span data-ttu-id="edf0d-137">接下来，您将查看使用 Page Inspector 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="edf0d-137">Next, you will view the application with Page Inspector.</span></span> <span data-ttu-id="edf0d-138">在中**解决方案资源管理器**，右键单击该项目，然后选择**在 Page Inspector 中的查看**。</span><span class="sxs-lookup"><span data-stu-id="edf0d-138">In **Solution Explorer**, right click the project, and then choose **View in Page Inspector**.</span></span>

![在 Page Inspector 中的视图](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

<span data-ttu-id="edf0d-140">默认情况下，Page Inspector 首次启动时它停靠在一个狭窄窗口作为 Visual Studio 环境的左侧。</span><span class="sxs-lookup"><span data-stu-id="edf0d-140">By default, when Page Inspector launches for the first time, it is docked as a narrow window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="edf0d-141">将其停靠在左侧和右侧，并将其设置为宽度都能轻松地为你，或将它工具领域中的一个停靠在顶部、 底部或右侧：</span><span class="sxs-lookup"><span data-stu-id="edf0d-141">Leave it docked on the left side and set it to a width that is comfortable for you, or dock it in one of the tool areas on the top, bottom, or right:</span></span>

![Page Inspector 停靠位置](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

<span data-ttu-id="edf0d-143">如果您取消停靠该页面检查器窗口，您可以将其放置外部 Visual Studio 中，或即使在第二个监视器上如果有。</span><span class="sxs-lookup"><span data-stu-id="edf0d-143">If you undock the Page Inspector window, you can place it outside Visual Studio, or even on a second monitor if you have one.</span></span> <span data-ttu-id="edf0d-144">但是，按 ALT + TAB Page Inspector 和 Visual Studio 之间的顺序未停靠的页面检查器窗口时，请转到**工具** &gt; **选项** &gt; **环境** &gt; **选项卡和 Windows**，然后在**选项卡也**，则清除该复选框调用**浮动工具窗口始终掌握的主窗口**:</span><span class="sxs-lookup"><span data-stu-id="edf0d-144">However, in order to ALT+TAB between Page Inspector and Visual Studio when the Page Inspector window is undocked, go to **Tools** &gt; **Options** &gt; **Environment** &gt; **Tabs and Windows**, and under **Tab Well**, clear the check box called **Floating tool windows always stay on top of the main window**:</span></span>

![清除 ALT + TAB Visual Studio 和停靠的页面检查器窗口之间的浮动工具 windows 复选框](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

<span data-ttu-id="edf0d-146">页面检查器窗口的顶部窗格会显示在浏览器窗口中当前页。</span><span class="sxs-lookup"><span data-stu-id="edf0d-146">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="edf0d-147">底部窗格显示在左侧的 HTML 标记中的页，并允许您在右侧的某些选项卡检查页的不同方面。</span><span class="sxs-lookup"><span data-stu-id="edf0d-147">The bottom pane shows the page in HTML markup on the left, and some tabs on the right that let you inspect different aspects of the page.</span></span> <span data-ttu-id="edf0d-148">在底部窗格是类似于[F12 开发人员工具](https://msdn.microsoft.com/ie/aa740478)Internet 资源管理器中。</span><span class="sxs-lookup"><span data-stu-id="edf0d-148">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span> <span data-ttu-id="edf0d-149">（但是，与不同的开发人员工具，您可以使用 Page Inspector 直接在 Visual Studio。）</span><span class="sxs-lookup"><span data-stu-id="edf0d-149">(However, unlike the developer tools, you can use Page Inspector right within Visual Studio.)</span></span>

![Page Inspector](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

<span data-ttu-id="edf0d-151">在本教程中，您将使用 Page Inspector 浏览器窗格中，并**HTML**并**样式**选项卡，有助于快速导航并对应用程序进行更改。</span><span class="sxs-lookup"><span data-stu-id="edf0d-151">In this tutorial, you will use the Page Inspector browser pane, and the **HTML** and **Styles** tabs to help you rapidly navigate and make changes to the application.</span></span>

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a><span data-ttu-id="edf0d-152">启用检查模式</span><span class="sxs-lookup"><span data-stu-id="edf0d-152">Enable Inspection Mode</span></span>

<span data-ttu-id="edf0d-153">接下来，你将看到 Page Inspector 的检查模式下的工作原理。</span><span class="sxs-lookup"><span data-stu-id="edf0d-153">Next, you will see how Page Inspector's Inspection Mode works.</span></span> <span data-ttu-id="edf0d-154">在页面检查器窗口中，单击**检查**按钮。</span><span class="sxs-lookup"><span data-stu-id="edf0d-154">In the Page Inspector window, click the **Inspect** button.</span></span>

![检查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

<span data-ttu-id="edf0d-156">若要查看操作中的检查模式下，将鼠标移动 Page Inspector 浏览器窗口中页面的不同部分。</span><span class="sxs-lookup"><span data-stu-id="edf0d-156">To see inspection mode in action, move your mouse over different parts of the page within the Page Inspector browser window.</span></span> <span data-ttu-id="edf0d-157">执行操作时，鼠标指针更改为较大的加号，并突出显示下面的元素：</span><span class="sxs-lookup"><span data-stu-id="edf0d-157">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![悬停在 div.content 包装器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

<span data-ttu-id="edf0d-159">移动鼠标指针时，请注意，</span><span class="sxs-lookup"><span data-stu-id="edf0d-159">As you move the mouse pointer, note that</span></span>

- <span data-ttu-id="edf0d-160">中的内容**源**查看发生变化，显示对应于页面上所选元素的标记。</span><span class="sxs-lookup"><span data-stu-id="edf0d-160">The content in **Source** view changes to show the markup corresponding to the selected element on the page.</span></span> <span data-ttu-id="edf0d-161">突出显示相关的标记。</span><span class="sxs-lookup"><span data-stu-id="edf0d-161">The relevant markup is highlighted.</span></span> <span data-ttu-id="edf0d-162">如果源是在另一个文件，该文件在源视图中打开与突出显示的相关标记。</span><span class="sxs-lookup"><span data-stu-id="edf0d-162">If the source is in another file, that file is opened in Source view with the relevant markup highlighted.</span></span>

- <span data-ttu-id="edf0d-163">在显示的标记**HTML**在 Page Inspector 中的选项卡也会更改以与页面上所选元素相对应。</span><span class="sxs-lookup"><span data-stu-id="edf0d-163">The markup displayed in the **HTML** tab in Page Inspector also changes to correspond to the selected element on the page.</span></span> <span data-ttu-id="edf0d-164">在中**HTML**选项卡上，概述了相关的标记。</span><span class="sxs-lookup"><span data-stu-id="edf0d-164">In the **HTML** tab, the relevant markup is outlined.</span></span>

- <span data-ttu-id="edf0d-165">**样式**选项卡显示与当前所选内容相关的 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="edf0d-165">The **Styles** tab shows the CSS rules relevant to the current selection.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="edf0d-166">使用 Page Inspector 对标记进行的更改</span><span class="sxs-lookup"><span data-stu-id="edf0d-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="edf0d-167">现在，将看到如何使用 Page Inspector 来查找和标记或其位置可能不是显而易见的文本进行更改。</span><span class="sxs-lookup"><span data-stu-id="edf0d-167">Now you will see how you can use Page Inspector to find and make changes to markup or text whose location might not be immediately obvious.</span></span>

<span data-ttu-id="edf0d-168">Page Inspector 置于检查模式下，然后滚动到主页页面的底部。</span><span class="sxs-lookup"><span data-stu-id="edf0d-168">Put Page Inspector in Inspection Mode and then scroll to the bottom of the home page.</span></span>

<span data-ttu-id="edf0d-169">一旦您输入的页脚区域，Page Inspector 将打开*Site.Master*中的布局文件**源**视图右侧的另一个临时选项卡中选项卡，并突出显示主节点的部分页上，您已选择。</span><span class="sxs-lookup"><span data-stu-id="edf0d-169">As soon as you enter the footer area, Page Inspector opens the *Site.Master* layout file in **Source** view in a temporary tab to the right of the other tabs and highlights the section of the master page that you have selected.</span></span> <span data-ttu-id="edf0d-170">此时会显示 Page Inspector 如何查找并可能实际上来自于不同的文件比最初打开的页面上显示的内容。</span><span class="sxs-lookup"><span data-stu-id="edf0d-170">This shows you how Page Inspector can find and display content on a page that might actually come from a different file than the one you originally opened.</span></span>

![在检查模式下的页脚重点推荐](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

<span data-ttu-id="edf0d-172">在 Page Inspector 浏览器窗口中，将移动鼠标指针在行的版权<a id="a"></a>注意到。</span><span class="sxs-lookup"><span data-stu-id="edf0d-172">In the Page Inspector browser window, move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span>

<span data-ttu-id="edf0d-173">在中*Site.Master*突出显示页面上，相应的行。</span><span class="sxs-lookup"><span data-stu-id="edf0d-173">In the *Site.Master* page, the corresponding line is highlighted.</span></span>

![页脚版权行突出显示](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

<span data-ttu-id="edf0d-175">将一些文本添加到中的行末尾*Site.Master*文件。</span><span class="sxs-lookup"><span data-stu-id="edf0d-175">Add some text to the end of the line in the *Site.Master* file.</span></span>

<span data-ttu-id="edf0d-176">&lt;p&gt;&amp;复制;&lt;%: DateTime.Now.Year %&gt; -我的 ASP.NET 应用程序 Rocks ！&lt;/ p&gt;</span><span class="sxs-lookup"><span data-stu-id="edf0d-176">&lt;p&gt;&amp;copy; &lt;%: DateTime.Now.Year %&gt; - My ASP.NET Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="edf0d-177">现在，按 Ctrl + Alt + Enter 或单击更新条以查看 Page Inspector 浏览器窗口中的结果。</span><span class="sxs-lookup"><span data-stu-id="edf0d-177">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![我的 ASP.NET 应用程序 Rocks ！](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

<span data-ttu-id="edf0d-179">您可能会想到上是页脚*Default.aspx*页上，但它原来在母版布局页中，并为你的 Page Inspector 找到它。</span><span class="sxs-lookup"><span data-stu-id="edf0d-179">You might have thought that the footer was on the *Default.aspx* page, but it turned out to be in the master layout page, and Page Inspector found it for you.</span></span>

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="edf0d-180">检查模式下和 HTML 窗口</span><span class="sxs-lookup"><span data-stu-id="edf0d-180">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="edf0d-181">接下来，您必须快速看一下 HTML 窗口以及它如何为您映射元素。</span><span class="sxs-lookup"><span data-stu-id="edf0d-181">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="edf0d-182">Page Inspector 置于检查模式。</span><span class="sxs-lookup"><span data-stu-id="edf0d-182">Put Page Inspector in Inspection Mode.</span></span>

![检查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

<span data-ttu-id="edf0d-184">单击显示"your logo here"的页的上半部分。</span><span class="sxs-lookup"><span data-stu-id="edf0d-184">Click the top part of the page that says "your logo here".</span></span> <span data-ttu-id="edf0d-185">正在检查中更多详细信息，因此您将鼠标指针移动无法再更改浏览器窗口中的显示的特定元素。</span><span class="sxs-lookup"><span data-stu-id="edf0d-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="edf0d-186">现在，转到鼠标指针**HTML**窗口。</span><span class="sxs-lookup"><span data-stu-id="edf0d-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="edf0d-187">移动鼠标指针时，Page Inspector 概述了中的元素**HTML**窗口，并突出显示浏览器窗口中的相应元素。</span><span class="sxs-lookup"><span data-stu-id="edf0d-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML 窗口](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

<span data-ttu-id="edf0d-189">如前面一样，Page Inspector 将打开*Site.Master*临时选项卡中为你的文件。单击 Site.Master 选项卡，并以突出显示相应的标记&lt;标头&gt;部分：</span><span class="sxs-lookup"><span data-stu-id="edf0d-189">As before, Page Inspector opens the *Site.Master* file for you in a temporary tab. Click the Site.Master tab, and the corresponding markup is highlighted in the &lt;header&gt; section:</span></span>

![突出显示的标记](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="edf0d-191">在样式窗口中预览 CSS 更改</span><span class="sxs-lookup"><span data-stu-id="edf0d-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="edf0d-192">接下来，你将看到如何使用 Page Inspector**样式**窗口来预览对 CSS 的更改。</span><span class="sxs-lookup"><span data-stu-id="edf0d-192">Next, you will see how you can use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="edf0d-193">单击**检查**将 Page Inspector 置于检查模式下的按钮。</span><span class="sxs-lookup"><span data-stu-id="edf0d-193">Click the **Inspect** button to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="edf0d-194">在 Page Inspector 浏览器窗口中，将鼠标指针移动到"主页"部分**div.content 包装**显示标签。</span><span class="sxs-lookup"><span data-stu-id="edf0d-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![悬停在元素上](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

<span data-ttu-id="edf0d-196">单击后，div.content 包装器部分中，然后移动鼠标指针指向**样式**窗口。</span><span class="sxs-lookup"><span data-stu-id="edf0d-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="edf0d-197">下.featured.content 包装器类选择器中，清除并选择背景色属性旁的复选框。</span><span class="sxs-lookup"><span data-stu-id="edf0d-197">Under the .featured .content-wrapper class selector, clear and select the checkbox for the background-color property.</span></span>

![清除背景色](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

<span data-ttu-id="edf0d-199">请注意如何更改预览可立即在 Page Inspector 浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="edf0d-199">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="edf0d-200">再次选中的复选框，然后双击属性值并将其更改为`red`。</span><span class="sxs-lookup"><span data-stu-id="edf0d-200">Select the checkbox again, then double-click the property value and change it to `red`.</span></span> <span data-ttu-id="edf0d-201">更改立即显示：</span><span class="sxs-lookup"><span data-stu-id="edf0d-201">The change shows immediately:</span></span>

![红色背景色](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

<span data-ttu-id="edf0d-203">**样式**窗口进行，可以轻松地测试并预览 CSS 更改之前将更改提交到样式表本身。</span><span class="sxs-lookup"><span data-stu-id="edf0d-203">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="edf0d-204">CSS 自动同步</span><span class="sxs-lookup"><span data-stu-id="edf0d-204">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="edf0d-205">此功能需要 Page Inspector 的 1.3 版。</span><span class="sxs-lookup"><span data-stu-id="edf0d-205">This feature requires version 1.3 of Page Inspector.</span></span>


<span data-ttu-id="edf0d-206">CSS 自动同步功能，可直接编辑 CSS 文件并查看立即在 Page Inspector 浏览器中的更改。</span><span class="sxs-lookup"><span data-stu-id="edf0d-206">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="edf0d-207">单击**检查**将 Page Inspector 置于检查模式。</span><span class="sxs-lookup"><span data-stu-id="edf0d-207">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="edf0d-208">在 Page Inspector 浏览器中，将移动鼠标指针的"主页"部分直到**div.content 包装**显示标签。</span><span class="sxs-lookup"><span data-stu-id="edf0d-208">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="edf0d-209">单击一次以选择此元素。</span><span class="sxs-lookup"><span data-stu-id="edf0d-209">Click once to select this element.</span></span>

<span data-ttu-id="edf0d-210">**样式**窗口将显示所有此元素的 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="edf0d-210">The **Syles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="edf0d-211">向下滚动到查找.featured.content 包装器类选择器。</span><span class="sxs-lookup"><span data-stu-id="edf0d-211">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="edf0d-212">单击"包装器.featured.content"。</span><span class="sxs-lookup"><span data-stu-id="edf0d-212">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="edf0d-213">Page Inspector 将打开定义此样式 (Site.css) 并突出显示相应的 CSS 样式的 CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="edf0d-213">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![CSS 文件](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

<span data-ttu-id="edf0d-215">现在，更改的值为`background-color`为"red"。</span><span class="sxs-lookup"><span data-stu-id="edf0d-215">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="edf0d-216">Page Inspector 浏览器中立即显示更改。</span><span class="sxs-lookup"><span data-stu-id="edf0d-216">The change appears immediately in the Page Inspector browser.</span></span>

![Page Inspector 浏览器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a><span data-ttu-id="edf0d-218">使用 CSS 颜色选取器</span><span class="sxs-lookup"><span data-stu-id="edf0d-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="edf0d-219">接下来，您将了解如何使用 Page Inspector 可以快速找到并更改默认应用程序中突出显示的文本的 CSS。</span><span class="sxs-lookup"><span data-stu-id="edf0d-219">Next, you'll learn how to use Page Inspector to quickly find and change the CSS for highlighted text in the default application.</span></span> <span data-ttu-id="edf0d-220">在此示例中，您已决定你不喜欢蓝色突出显示并想要将其更改为另一种颜色。</span><span class="sxs-lookup"><span data-stu-id="edf0d-220">In this example, you've decided that you don't like the blue highlighting and want to change it to another color.</span></span>

<span data-ttu-id="edf0d-221">单击**检查**按钮。</span><span class="sxs-lookup"><span data-stu-id="edf0d-221">Click the **Inspect** button.</span></span>

![检查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

<span data-ttu-id="edf0d-223">在 Page Inspector 浏览器窗口中，将鼠标指针移动突出显示"视频、 教程和示例"，以便 CSS"标记"标签文本显示。</span><span class="sxs-lookup"><span data-stu-id="edf0d-223">In the Page Inspector browser window, move the mouse pointer over the highlighted "videos, tutorials, and samples" text so that the CSS "mark" label appears.</span></span>

![悬停在标记元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

<span data-ttu-id="edf0d-225">单击以选中它的文本。</span><span class="sxs-lookup"><span data-stu-id="edf0d-225">Click the text to select it.</span></span> <span data-ttu-id="edf0d-226">相应的 CSS 标记选择器将显示在底部**样式**窗口。</span><span class="sxs-lookup"><span data-stu-id="edf0d-226">The corresponding CSS mark selector appears at the bottom of the **Styles** window.</span></span>

![在样式窗口中的标记选择器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

<span data-ttu-id="edf0d-228">单击标记选择器。</span><span class="sxs-lookup"><span data-stu-id="edf0d-228">Click the mark selector.</span></span> <span data-ttu-id="edf0d-229">这将打开*Site.css* web 应用程序文件。</span><span class="sxs-lookup"><span data-stu-id="edf0d-229">This opens the *Site.css* file for the web application.</span></span> <span data-ttu-id="edf0d-230">单击 Site.css 选项卡，并突出显示相应的 CSS 选择器：</span><span class="sxs-lookup"><span data-stu-id="edf0d-230">Click the Site.css tab, and the corresponding CSS for the selector is highlighted:</span></span>

![样式表中的标记选择器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

<span data-ttu-id="edf0d-232">选择并删除在行的背景色属性。</span><span class="sxs-lookup"><span data-stu-id="edf0d-232">Select and remove the line with the background-color property.</span></span>

<span data-ttu-id="edf0d-233">现在将使用新的 Visual Studio 2012 CSS 颜色选取器选择的新颜色**标记**背景颜色属性。</span><span class="sxs-lookup"><span data-stu-id="edf0d-233">You will now use the new Visual Studio 2012 CSS color picker to choose a new color for the **mark** background-color property.</span></span>

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a><span data-ttu-id="edf0d-234">使用 Visual Studio 2012 CSS 颜色选取器</span><span class="sxs-lookup"><span data-stu-id="edf0d-234">Using the Visual Studio 2012 CSS Color Picker</span></span>

<span data-ttu-id="edf0d-235">在 Visual Studio 2012 CSS 编辑器具有颜色选取器，轻松地选择和插入颜色。</span><span class="sxs-lookup"><span data-stu-id="edf0d-235">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="edf0d-236">它具有一个简单的颜色条和的"pop 停机"选取器，可提供更精细的控制。</span><span class="sxs-lookup"><span data-stu-id="edf0d-236">It has a simple color bar and a "pop-down" picker that offers finer control.</span></span>

<span data-ttu-id="edf0d-237">颜色选取器包括一个标准颜色的调色板，支持标准颜色名称、 哈希代码、 RGB、 RGBA、 HSL 和 HSLA 颜色和维护已在文档中最近使用的颜色的列表。</span><span class="sxs-lookup"><span data-stu-id="edf0d-237">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="edf0d-238">上的背景色属性所在的行中，键入"bc"并一次按向下箭头。</span><span class="sxs-lookup"><span data-stu-id="edf0d-238">On the line where the background-color property was, type "bc" and press the down arrow once.</span></span>

<span data-ttu-id="edf0d-239">连字符分隔的属性，如"背景色"中键入每个单词的第一个字符时，IntelliSense 将筛选要显示匹配的属性列表：</span><span class="sxs-lookup"><span data-stu-id="edf0d-239">When you type the first character of each word in a hyphen-separated property like "background-color", IntelliSense filters the list for you to show only the properties that match:</span></span>

![Intellisense 筛选值](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

<span data-ttu-id="edf0d-241">现在，键入一个冒号。</span><span class="sxs-lookup"><span data-stu-id="edf0d-241">Now type a colon.</span></span> <span data-ttu-id="edf0d-242">执行操作时，将插入完整的背景色属性名称。</span><span class="sxs-lookup"><span data-stu-id="edf0d-242">When you do, the full background-color property name is inserted.</span></span> <span data-ttu-id="edf0d-243">类型**#** 或**rgb (**，并显示颜色选取器条：</span><span class="sxs-lookup"><span data-stu-id="edf0d-243">Type **#** or **rgb(**, and the color picker bar appears:</span></span>

![CSS 颜色选取器栏](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

<span data-ttu-id="edf0d-245">若要查看颜色选取器栏的工作原理，请单击它将鼠标指针的颜色或按向下箭头键，然后使用左侧和右侧的箭头键遍历颜色。</span><span class="sxs-lookup"><span data-stu-id="edf0d-245">To see how the color picker bar works, click its colors with the mouse pointer, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="edf0d-246">当您访问一种颜色时，预览的背景色属性的相应值：</span><span class="sxs-lookup"><span data-stu-id="edf0d-246">When you visit a color, the corresponding value for the background-color property is previewed:</span></span>

![预览的背景色属性值](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

<span data-ttu-id="edf0d-248">此时，可以按 enter 键以选择值，然后完成 CSS 输入分号 （;）。</span><span class="sxs-lookup"><span data-stu-id="edf0d-248">At this point, you could press Enter to select the value and then a semicolon (;) to complete the CSS entry.</span></span> <span data-ttu-id="edf0d-249">现在，转到下一节，以便可以查看颜色选取器 pop 列表的工作原理。</span><span class="sxs-lookup"><span data-stu-id="edf0d-249">For now, go on to the next section so that you can see how the color picker pop-down works.</span></span>

#### <a name="using-the-color-picker-pop-down"></a><span data-ttu-id="edf0d-250">使用颜色选取器 Pop 列表</span><span class="sxs-lookup"><span data-stu-id="edf0d-250">Using the Color Picker Pop-Down</span></span>

<span data-ttu-id="edf0d-251">当在颜色栏不具有所需的确切颜色时，可以使用颜色选取器 pop 列表。</span><span class="sxs-lookup"><span data-stu-id="edf0d-251">When the color bar doesn't have the exact color that you're looking for, you can use the color picker pop-down.</span></span>

<span data-ttu-id="edf0d-252">若要打开它，请单击颜色栏右侧的双 v 形图标或按键盘上一次或两次的向下箭头。</span><span class="sxs-lookup"><span data-stu-id="edf0d-252">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS 颜色选取器 Pop 列表](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

<span data-ttu-id="edf0d-254">单击从右侧的垂直条的颜色。</span><span class="sxs-lookup"><span data-stu-id="edf0d-254">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="edf0d-255">这将在主窗口中显示该颜色渐变。</span><span class="sxs-lookup"><span data-stu-id="edf0d-255">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="edf0d-256">通过按 Enter，直接从垂直条中选择一种颜色，或单击以选择具有更高的精度在主窗口中的任意点。</span><span class="sxs-lookup"><span data-stu-id="edf0d-256">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="edf0d-257">你想要使用的计算机屏幕上是否存在一种颜色 （不一定要在 Visual Studio 用户界面内），你可以通过使用取色器工具右下角中捕获它的值。</span><span class="sxs-lookup"><span data-stu-id="edf0d-257">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="edf0d-258">此外可以通过移动颜色选取器底部的滑块来更改一种颜色的不透明度。</span><span class="sxs-lookup"><span data-stu-id="edf0d-258">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="edf0d-259">这样做的更改颜色为 RGBA 值的值，因为 RGBA 格式可以表示不透明度。</span><span class="sxs-lookup"><span data-stu-id="edf0d-259">Doing so changes color values to RGBA values because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="edf0d-260">选择一种颜色后，按 Enter，，然后键入分号完成中的背景色条目*Site.css*文件。</span><span class="sxs-lookup"><span data-stu-id="edf0d-260">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="edf0d-261">页面检查器更新条</span><span class="sxs-lookup"><span data-stu-id="edf0d-261">The Page Inspector Update Bar</span></span>

<span data-ttu-id="edf0d-262">Page Inspector 立即检测到更改*Site.css*文件 （或应用程序中的任何文件），并显示更新条中的警报。</span><span class="sxs-lookup"><span data-stu-id="edf0d-262">Page Inspector immediately detects the change to the *Site.css* file (or to any file in the application) and displays an alert in an update bar.</span></span>

![更新条](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

<span data-ttu-id="edf0d-264">若要保存所有文件并刷新 Page Inspector 浏览器，请按 Ctrl + Alt + Enter 或单击更新条。</span><span class="sxs-lookup"><span data-stu-id="edf0d-264">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="edf0d-265">中的突出显示颜色更改显示在浏览器中：</span><span class="sxs-lookup"><span data-stu-id="edf0d-265">The change in the highlight color appears in the browser:</span></span>

![突出显示颜色更改](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a><span data-ttu-id="edf0d-267">请注意，您可以方便地刷新 Page Inspector 浏览器直接从 Visual Studio 环境中。</span><span class="sxs-lookup"><span data-stu-id="edf0d-267">Notice that you conveniently refreshed the Page Inspector browser right from within the Visual Studio environment.</span></span> <span data-ttu-id="edf0d-268">而不外部浏览器中使用 Page Inspector 允许您在开发 web 应用程序时不会在编辑器中。</span><span class="sxs-lookup"><span data-stu-id="edf0d-268">Using Page Inspector instead of an external browser lets you stay in the editor when you develop your web applications.</span></span>

## <a name="see-also"></a><span data-ttu-id="edf0d-269">请参阅</span><span class="sxs-lookup"><span data-stu-id="edf0d-269">See Also</span></span>

<span data-ttu-id="edf0d-270">[引入了 Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) （第 9 频道视频）</span><span class="sxs-lookup"><span data-stu-id="edf0d-270">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 video)</span></span>

<span data-ttu-id="edf0d-271">[Page Inspector 错误信息](https://go.microsoft.com/?linkid=9813062)(MSDN)</span><span class="sxs-lookup"><span data-stu-id="edf0d-271">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
