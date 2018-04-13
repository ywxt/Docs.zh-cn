---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: 什么是 ASP.NET MVC 4 中的新增功能 |Microsoft 文档
author: rick-anderson
description: ASP.NET MVC 4 是用于构建可缩放的、 基于标准的 web 应用程序使用成熟设计模式和 ASP.NET 的强大功能的框架和...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 977a6b5a84825ebd087752dcc2ebc0c5410e1657
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
---
# <a name="whats-new-in-aspnet-mvc-4"></a><span data-ttu-id="54379-103">什么是 ASP.NET MVC 4 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="54379-103">What's New in ASP.NET MVC 4</span></span>

<span data-ttu-id="54379-104">通过[Web 营地团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="54379-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="54379-105">下载 Web 营地培训工具包</span><span class="sxs-lookup"><span data-stu-id="54379-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="54379-106">ASP.NET MVC 4 是一个框架，用于构建可缩放的、 基于标准的 web 应用程序使用成熟设计模式以及 ASP.NET 和.NET framework 的能力。</span><span class="sxs-lookup"><span data-stu-id="54379-106">ASP.NET MVC 4 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of the ASP.NET and the .NET framework.</span></span> <span data-ttu-id="54379-107">此新，第四个版本的 framework 侧重于使移动 web 应用程序开发更容易。</span><span class="sxs-lookup"><span data-stu-id="54379-107">This new, fourth version of the framework focuses on making mobile web application development easier.</span></span>

<span data-ttu-id="54379-108">开始时，当你创建新的 ASP.NET MVC 4 项目现在有了你可以使用生成独立应用程序专用于移动设备的移动应用程序项目模板。</span><span class="sxs-lookup"><span data-stu-id="54379-108">To begin with, when you create a new ASP.NET MVC 4 project there is now a mobile application project template you can use to build a standalone app specifically for mobile devices.</span></span> <span data-ttu-id="54379-109">此外，与 jQuery Mobile jQuery.Mobile.MVC NuGet 程序包通过集成 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="54379-109">Additionally, ASP.NET MVC 4 integrates with jQuery Mobile through a jQuery.Mobile.MVC NuGet package.</span></span> <span data-ttu-id="54379-110">jQuery Mobile 是基于 HTML5 的开发与所有主流移动设备平台，包括 Windows Phone，iPhone、 Android 等兼容的 web 应用程序框架。</span><span class="sxs-lookup"><span data-stu-id="54379-110">jQuery Mobile is an HTML5-based framework for developing web apps that are compatible with all popular mobile device platforms, including Windows Phone, iPhone, Android and so on.</span></span> <span data-ttu-id="54379-111">但是，如果你需要专用化，ASP.NET MVC 4 还使您能够服务适用于不同设备的不同视图，并提供特定于设备的优化。</span><span class="sxs-lookup"><span data-stu-id="54379-111">However, if you need specialization, ASP.NET MVC 4 also enables you to serve different views for different devices and provide device-specific optimizations.</span></span>

<span data-ttu-id="54379-112">在此动手实验中，你将使用 ASP.NET MVC 4 中启动&quot;Internet 应用程序&quot;项目模板创建照片库应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-112">In this hands-on lab, you will start with the ASP.NET MVC 4 &quot;Internet Application&quot; project template to create a Photo Gallery application.</span></span> <span data-ttu-id="54379-113">你将逐渐增强使用 jQuery Mobile 和 ASP.NET MVC 4 的新功能以使其与不同的移动设备和桌面 web 浏览器兼容的应用。</span><span class="sxs-lookup"><span data-stu-id="54379-113">You will progressively enhance the app using jQuery Mobile and ASP.NET MVC 4's new features to make it compatible with different mobile devices and desktop web browsers.</span></span> <span data-ttu-id="54379-114">您还将了解代码生成和如何 ASP.NET MVC 4 使你更轻松地编写异步操作方法通过支持任务的新代码食谱&lt;ActionResult&gt;返回类型。</span><span class="sxs-lookup"><span data-stu-id="54379-114">You will also learn about new code recipes for code generation and how ASP.NET MVC 4 makes it easier for you to write asynchronous action methods by supporting Task&lt;ActionResult&gt; return types.</span></span>

> [!NOTE]
> <span data-ttu-id="54379-115">在 Web 营地培训工具包中，在包括所有的示例代码和代码段[Microsoft 的 Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。</span><span class="sxs-lookup"><span data-stu-id="54379-115">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="54379-116">特定于此实验室项目位于[在 ASP.NET 4.5 Web 窗体中的新增](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)。</span><span class="sxs-lookup"><span data-stu-id="54379-116">The project specific to this lab is available at [What's New in Web Forms in ASP.NET 4.5](https://github.com/Microsoft-Web/HOL-ASPNETWebForms).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="54379-117">目标</span><span class="sxs-lookup"><span data-stu-id="54379-117">Objectives</span></span>

<span data-ttu-id="54379-118">在此动手实验中，你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="54379-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="54379-119">充分利用 ASP.NET MVC 项目模板-包括新的移动应用程序项目模板的增强功能</span><span class="sxs-lookup"><span data-stu-id="54379-119">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="54379-120">使用 HTML5 视区属性和 CSS 媒体查询来改善在移动设备上的显示</span><span class="sxs-lookup"><span data-stu-id="54379-120">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="54379-121">使用 jQuery Mobile，来渐进式增强功能并构建触控优化 web UI</span><span class="sxs-lookup"><span data-stu-id="54379-121">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="54379-122">创建移动特定的视图</span><span class="sxs-lookup"><span data-stu-id="54379-122">Create mobile-specific views</span></span>
- <span data-ttu-id="54379-123">视图切换器组件用于应用程序中的移动和桌面视图之间切换</span><span class="sxs-lookup"><span data-stu-id="54379-123">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="54379-124">创建使用任务支持异步控制器</span><span class="sxs-lookup"><span data-stu-id="54379-124">Create asynchronous controllers using task support</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="54379-125">系统必备</span><span class="sxs-lookup"><span data-stu-id="54379-125">Prerequisites</span></span>

<span data-ttu-id="54379-126">你必须具有要完成本实验的以下项：</span><span class="sxs-lookup"><span data-stu-id="54379-126">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="54379-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 B](#AppendixB)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="54379-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>
- <span data-ttu-id="54379-128">[ASP.NET MVC 4](../../../mvc4.md) （Microsoft Visual Studio 2012 安装中包括）</span><span class="sxs-lookup"><span data-stu-id="54379-128">[ASP.NET MVC 4](../../../mvc4.md) (included in the Microsoft Visual Studio 2012 installation)</span></span>
- <span data-ttu-id="54379-129">Windows Phone 仿真程序 (包括在[Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span><span class="sxs-lookup"><span data-stu-id="54379-129">Windows Phone Emulator (included in the [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span></span>
- <span data-ttu-id="54379-130">可选- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/)与**Electric Plum iPhone 模拟器**（仅适用于用来与 iPhone 模拟器中浏览 web 应用程序的练习 3) 的扩展</span><span class="sxs-lookup"><span data-stu-id="54379-130">Optional - [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) with **Electric Plum iPhone Simulator** extension (only for Exercise 3 used to browse the web application with an iPhone simulator)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="54379-131">安装</span><span class="sxs-lookup"><span data-stu-id="54379-131">Setup</span></span>

<span data-ttu-id="54379-132">在整个实验文档中，你将指示要插入代码块。</span><span class="sxs-lookup"><span data-stu-id="54379-132">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="54379-133">为方便起见，该代码的大部分提供作为 Visual Studio 代码段，你可以使用从 Visual Studio 中为了避免必须手动添加它。</span><span class="sxs-lookup"><span data-stu-id="54379-133">For your convenience, most of that code is provided as Visual Studio Code Snippets, which you can use from within Visual Studio to avoid having to add it manually.</span></span>

<span data-ttu-id="54379-134">若要安装的代码段：</span><span class="sxs-lookup"><span data-stu-id="54379-134">To install the code snippets:</span></span>

1. <span data-ttu-id="54379-135">打开 Windows 资源管理器窗口并浏览到本实验的**Source\Setup**文件夹。</span><span class="sxs-lookup"><span data-stu-id="54379-135">Open a Windows Explorer window and browse to the lab's **Source\Setup** folder.</span></span>
2. <span data-ttu-id="54379-136">双击**Setup.cmd**文件置于此文件夹以安装的 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="54379-136">Double-click the **Setup.cmd** file in this folder to install the Visual Studio code snippets.</span></span>

<span data-ttu-id="54379-137">如果你不熟悉 Visual Studio 代码段，并想要了解如何使用它们，你可以从该文档引用的附录&quot;[附录 a： 使用代码段](#AppendixA)&quot;。</span><span class="sxs-lookup"><span data-stu-id="54379-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="54379-138">练习</span><span class="sxs-lookup"><span data-stu-id="54379-138">Exercises</span></span>

<span data-ttu-id="54379-139">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="54379-139">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="54379-140">新的 ASP.NET MVC 4 项目模板</span><span class="sxs-lookup"><span data-stu-id="54379-140">New ASP.NET MVC 4 Project Templates</span></span>](#Exercise1)
2. [<span data-ttu-id="54379-141">创建照片库 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="54379-141">Creating the Photo Gallery Web Application</span></span>](#Exercise2)
3. [<span data-ttu-id="54379-142">添加对移动设备的支持</span><span class="sxs-lookup"><span data-stu-id="54379-142">Adding Support for Mobile Devices</span></span>](#Exercise3)
4. [<span data-ttu-id="54379-143">使用异步控制器</span><span class="sxs-lookup"><span data-stu-id="54379-143">Using Asynchronous Controllers</span></span>](#Exercise4)

> [!NOTE]
> <span data-ttu-id="54379-144">每个练习均附带由**结束**包含生成您应该完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="54379-144">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="54379-145">如果你需要通过在练习工作的更多帮助，可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="54379-145">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="54379-146">估计时间来完成该实验： **60 分钟**。</span><span class="sxs-lookup"><span data-stu-id="54379-146">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a><span data-ttu-id="54379-147">练习 1： 新的 ASP.NET MVC 4 项目模板</span><span class="sxs-lookup"><span data-stu-id="54379-147">Exercise 1: New ASP.NET MVC 4 Project Templates</span></span>

<span data-ttu-id="54379-148">在此练习中，您将了解在 ASP.NET MVC 4 项目模板中的增强功能。</span><span class="sxs-lookup"><span data-stu-id="54379-148">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 Project templates.</span></span> <span data-ttu-id="54379-149">除了 Internet 应用程序模板中，在 MVC 3 中，已存在此版本现在包括用于移动应用程序的单独的模板。</span><span class="sxs-lookup"><span data-stu-id="54379-149">In addition to the Internet Application template, already present in MVC 3, this version now includes a separate template for Mobile applications.</span></span> <span data-ttu-id="54379-150">首先，你将查看每个模板的某些相关功能。</span><span class="sxs-lookup"><span data-stu-id="54379-150">First, you will look at some relevant features of each of the templates.</span></span> <span data-ttu-id="54379-151">然后，将处理呈现你的页正确在不同的平台上使用适当的方法。</span><span class="sxs-lookup"><span data-stu-id="54379-151">Then, you will work on rendering your page properly on the different platforms by using the right approach.</span></span>

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a><span data-ttu-id="54379-152">任务 1-浏览 Internet 应用程序模板</span><span class="sxs-lookup"><span data-stu-id="54379-152">Task 1 - Exploring the Internet Application Template</span></span>

1. <span data-ttu-id="54379-153">打开**Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="54379-153">Open **Visual Studio**.</span></span>
2. <span data-ttu-id="54379-154">选择**文件 |新 |项目**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="54379-154">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="54379-155">在**新项目**对话框中，选择**Visual C# |Web**左窗格中的模板树，并选择**ASP.NET MVC 4 Web 应用程序。**</span><span class="sxs-lookup"><span data-stu-id="54379-155">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="54379-156">将项目**PhotoGallery**、 选择一个位置 （或保留默认值），然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="54379-156">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="54379-157">稍后将自定义图片库 ASP.NET MVC 4 解决方案现在要创建。</span><span class="sxs-lookup"><span data-stu-id="54379-157">You will later customize the PhotoGallery ASP.NET MVC 4 solution you are now creating.</span></span>

    <span data-ttu-id="54379-158">![创建新的项目](whats-new-in-aspnet-mvc-4/_static/image1.png "创建新项目")</span><span class="sxs-lookup"><span data-stu-id="54379-158">![Creating a new project](whats-new-in-aspnet-mvc-4/_static/image1.png "Creating a new project")</span></span>

    <span data-ttu-id="54379-159">*创建新项目*</span><span class="sxs-lookup"><span data-stu-id="54379-159">*Creating a new project*</span></span>
3. <span data-ttu-id="54379-160">在**新建 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**项目模板，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="54379-160">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="54379-161">请确保您已选择 Razor 作为视图引擎。</span><span class="sxs-lookup"><span data-stu-id="54379-161">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="54379-162">![新建 ASP.NET MVC 4 Internet 应用程序](whats-new-in-aspnet-mvc-4/_static/image2.png "新建 ASP.NET MVC 4 Internet 应用程序")</span><span class="sxs-lookup"><span data-stu-id="54379-162">![Creating a new ASP.NET MVC 4 Internet Application](whats-new-in-aspnet-mvc-4/_static/image2.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="54379-163">*新建 ASP.NET MVC 4 Internet 应用程序*</span><span class="sxs-lookup"><span data-stu-id="54379-163">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="54379-164">ASP.NET MVC 3 中引入了 razor 语法。</span><span class="sxs-lookup"><span data-stu-id="54379-164">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="54379-165">其目标是字符和在文件中，需要启用快速和流体编码工作流的击键的数量降至最低。</span><span class="sxs-lookup"><span data-stu-id="54379-165">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="54379-166">Razor 利用现有的 C# / VB （或其他） 语言技能和提供使出色的 HTML 构造流的模板标记语法。</span><span class="sxs-lookup"><span data-stu-id="54379-166">Razor leverages existing C# / VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="54379-167">按**F5**以运行该解决方案并查看续订的模板。</span><span class="sxs-lookup"><span data-stu-id="54379-167">Press **F5** to run the solution and see the renewed templates.</span></span> <span data-ttu-id="54379-168">你可以查看以下功能：</span><span class="sxs-lookup"><span data-stu-id="54379-168">You can check out the following features:</span></span>

    <span data-ttu-id="54379-169">**现代样式模板**</span><span class="sxs-lookup"><span data-stu-id="54379-169">**Modern-style templates**</span></span>

    <span data-ttu-id="54379-170">已续订的模板，提供更多的外观现代的样式。</span><span class="sxs-lookup"><span data-stu-id="54379-170">The templates have been renewed, providing more modern-looking styles.</span></span>

    <span data-ttu-id="54379-171">![ASP.NET MVC 4 其样式模板](whats-new-in-aspnet-mvc-4/_static/image3.png "其样式模板的 MVC 4")</span><span class="sxs-lookup"><span data-stu-id="54379-171">![ASP.NET MVC 4 restyled templates](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 restyled templates")</span></span>

    <span data-ttu-id="54379-172">*ASP.NET MVC 4 其样式模板*</span><span class="sxs-lookup"><span data-stu-id="54379-172">*ASP.NET MVC 4 restyled templates*</span></span>

    <span data-ttu-id="54379-173">![新联系人页](whats-new-in-aspnet-mvc-4/_static/image4.png "新联系人页")</span><span class="sxs-lookup"><span data-stu-id="54379-173">![New Contact page](whats-new-in-aspnet-mvc-4/_static/image4.png "New Contact page")</span></span>

    <span data-ttu-id="54379-174">*新联系人页*</span><span class="sxs-lookup"><span data-stu-id="54379-174">*New Contact page*</span></span>

    <span data-ttu-id="54379-175">**自适应呈现**</span><span class="sxs-lookup"><span data-stu-id="54379-175">**Adaptive Rendering**</span></span>

    <span data-ttu-id="54379-176">签出调整浏览器窗口的大小，请注意如何页面布局可以动态地适应新的窗口大小。</span><span class="sxs-lookup"><span data-stu-id="54379-176">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="54379-177">这些模板使用的自适应呈现技术在没有任何自定义项的桌面和移动平台中正确呈现。</span><span class="sxs-lookup"><span data-stu-id="54379-177">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

    <span data-ttu-id="54379-178">![在不同的浏览器大小中的 ASP.NET MVC 4 项目模板](whats-new-in-aspnet-mvc-4/_static/image5.png "中不同的浏览器大小的 ASP.NET MVC 4 项目模板")</span><span class="sxs-lookup"><span data-stu-id="54379-178">![ASP.NET MVC 4 project template in different browser sizes](whats-new-in-aspnet-mvc-4/_static/image5.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

    <span data-ttu-id="54379-179">*在不同的浏览器大小中的 ASP.NET MVC 4 项目模板*</span><span class="sxs-lookup"><span data-stu-id="54379-179">*ASP.NET MVC 4 project template in different browser sizes*</span></span>

    <span data-ttu-id="54379-180">**更丰富的 UI，使用 JavaScript**</span><span class="sxs-lookup"><span data-stu-id="54379-180">**Richer UI with JavaScript**</span></span>

    <span data-ttu-id="54379-181">还有一项增强默认的项目模板是使用 JavaScript 来提供更交互式 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="54379-181">Another enhancement to default project templates is the use of JavaScript to provide a more interactive JavaScript.</span></span> <span data-ttu-id="54379-182">在模板中使用的登录和注册链接演示如何使用 jQuery 验证来验证从客户端的输入的字段。</span><span class="sxs-lookup"><span data-stu-id="54379-182">The Login and Register links used in the template exemplify how to use the jQuery Validations to validate the input fields from client-side.</span></span>

    ![jQuery 验证](whats-new-in-aspnet-mvc-4/_static/image6.png)

    <span data-ttu-id="54379-184">*jQuery 验证*</span><span class="sxs-lookup"><span data-stu-id="54379-184">*jQuery Validation*</span></span>

    > [!NOTE]
    > <span data-ttu-id="54379-185">请注意这两个日志中的第一节中的部分，你可以登录和你可以使用另一个身份验证服务，如 google （默认情况下禁用） 的 altenativelly 登录的第二部分中使用已注册帐户从站点。</span><span class="sxs-lookup"><span data-stu-id="54379-185">Notice the two log in sections, in the first section you can log in using a registerd account from the site and in the second section you can altenativelly log in using another authentication service like google (disabled by default).</span></span>
5. <span data-ttu-id="54379-186">关闭浏览器以停止调试器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="54379-186">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="54379-187">打开文件**AuthConfig.cs**位于**应用\_启动**文件夹。</span><span class="sxs-lookup"><span data-stu-id="54379-187">Open the file **AuthConfig.cs** located under the **App\_Start** folder.</span></span>
7. <span data-ttu-id="54379-188">从注册的 Google 客户端的最后一行中删除注释*OAuth*身份验证。</span><span class="sxs-lookup"><span data-stu-id="54379-188">Remove the comment from the last line to register Google client for *OAuth* authentication.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

> [!NOTE]
> Notice you can easily enable authentication using any OpenID or OAuth service like Facebook, Twitter, Microsoft, etc.
~~~
8. <span data-ttu-id="54379-189">按**F5**若要运行解决方案，并导航到登录页。</span><span class="sxs-lookup"><span data-stu-id="54379-189">Press **F5** to run the solution and navigate to the login page.</span></span>
9. <span data-ttu-id="54379-190">选择**Google**服务进行登录。</span><span class="sxs-lookup"><span data-stu-id="54379-190">Select **Google** service to log in.</span></span>

    ![在服务中选择日志](whats-new-in-aspnet-mvc-4/_static/image7.png)

    <span data-ttu-id="54379-192">*在服务中选择日志*</span><span class="sxs-lookup"><span data-stu-id="54379-192">*Selecting the log in service*</span></span>
10. <span data-ttu-id="54379-193">使用你的 Google 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="54379-193">Log in using your Google account.</span></span>
11. <span data-ttu-id="54379-194">允许 Google 帐户中检索信息的站点 (localhost)。</span><span class="sxs-lookup"><span data-stu-id="54379-194">Allow the site (localhost) to retrieve information from Google account.</span></span>
12. <span data-ttu-id="54379-195">最后，你将需要在要将 Google 帐户相关联的站点中注册。</span><span class="sxs-lookup"><span data-stu-id="54379-195">Finally, you will have to register in the site to associate the Google account.</span></span>

   ![将你的 Google 帐户相关联](whats-new-in-aspnet-mvc-4/_static/image8.png)

   <span data-ttu-id="54379-197">*将你的 Google 帐户相关联*</span><span class="sxs-lookup"><span data-stu-id="54379-197">*Associating your Google account*</span></span>
13. <span data-ttu-id="54379-198">关闭浏览器以停止调试器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="54379-198">Close the browser to stop the debugger and return to Visual Studio.</span></span>
14. <span data-ttu-id="54379-199">现在浏览要签出项目模板中由 ASP.NET MVC 4 引入了一些其他新功能的解决方案。</span><span class="sxs-lookup"><span data-stu-id="54379-199">Now explore the solution to check out some other new features introduced by ASP.NET MVC 4 in the project template.</span></span>

   <span data-ttu-id="54379-200">![ASP.NET MVC 4 Internet 应用程序项目模板](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 Internet 应用程序项目模板")</span><span class="sxs-lookup"><span data-stu-id="54379-200">![The ASP.NET MVC 4 Internet Application Project Template](whats-new-in-aspnet-mvc-4/_static/image9.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

   <span data-ttu-id="54379-201">*ASP.NET MVC 4 Internet 应用程序项目模板*</span><span class="sxs-lookup"><span data-stu-id="54379-201">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

   - <span data-ttu-id="54379-202">**HTML 5 标记**</span><span class="sxs-lookup"><span data-stu-id="54379-202">**HTML 5 Markup**</span></span>

       <span data-ttu-id="54379-203">浏览模板视图若要了解新的主题标记。</span><span class="sxs-lookup"><span data-stu-id="54379-203">Browse template views to find out the new theme markup.</span></span>

       <span data-ttu-id="54379-204">![使用 Razor 和 HTML5 标记 About.cshtml 新模板。](whats-new-in-aspnet-mvc-4/_static/image10.png "使用 Razor 和 HTML5 标记 About.cshtml 的新模板。")</span><span class="sxs-lookup"><span data-stu-id="54379-204">![New template, using Razor and HTML5 markup About.cshtml.](whats-new-in-aspnet-mvc-4/_static/image10.png "New template, using Razor and HTML5 markup About.cshtml.")</span></span>

       <span data-ttu-id="54379-205">*使用 Razor 和 HTML5 标记 (About.cshtml) 新模板。*</span><span class="sxs-lookup"><span data-stu-id="54379-205">*New template, using Razor and HTML5 markup (About.cshtml).*</span></span>
   - <span data-ttu-id="54379-206">**更新的 JavaScript 库**</span><span class="sxs-lookup"><span data-stu-id="54379-206">**Updated JavaScript libraries**</span></span>

       <span data-ttu-id="54379-207">ASP.NET MVC 4 默认模板现在包括 KnockoutJS、 JavaScript MVVM 框架，它允许你创建丰富和响应度高的 web 应用程序使用 JavaScript 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="54379-207">The ASP.NET MVC 4 default template now includes KnockoutJS, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="54379-208">如在 MVC3，jQuery 和 jQuery UI 库也包括在 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="54379-208">Like in MVC3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

     > [!NOTE]
     > <span data-ttu-id="54379-209">你可以获取有关此链接中的 KnockOutJS 库的详细信息： [ [ http://learn.knockoutjs.com/ ](http://learn.knockoutjs.com/) ](http://learn.knockoutjs.com/)。</span><span class="sxs-lookup"><span data-stu-id="54379-209">You can get more information about KnockOutJS library in this link: [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/).</span></span> <span data-ttu-id="54379-210">此外，你可以了解有关 jQuery 和 jQuery UI 中[ [ http://docs.jquery.com/ ](http://docs.jquery.com/) ](http://docs.jquery.com/)。</span><span class="sxs-lookup"><span data-stu-id="54379-210">Additionally, you can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a><span data-ttu-id="54379-211">任务 2-浏览移动应用程序模板</span><span class="sxs-lookup"><span data-stu-id="54379-211">Task 2 - Exploring the Mobile Application Template</span></span>

<span data-ttu-id="54379-212">ASP.NET MVC 4 便于移动的网站和平板电脑浏览器的开发。</span><span class="sxs-lookup"><span data-stu-id="54379-212">ASP.NET MVC 4 facilitates the development of websites for mobile and tablet browsers.</span></span> <span data-ttu-id="54379-213">此模板具有相同的应用程序结构与 Internet 应用程序模板 （注意控制器代码，并几乎完全相同），但其样式进行了修改以基于 touch 的移动设备中正确呈现。</span><span class="sxs-lookup"><span data-stu-id="54379-213">This template has the same application structure as the Internet Application template (notice that the controller code is practically identical), but its style was modified to render properly in touch-based mobile devices.</span></span>

1. <span data-ttu-id="54379-214">选择**文件 |新 |项目**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="54379-214">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="54379-215">在**新项目**对话框中，选择**Visual C# |Web**左窗格中的模板树，并选择**ASP.NET MVC 4 Web 应用程序。**</span><span class="sxs-lookup"><span data-stu-id="54379-215">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="54379-216">将项目**PhotoGallery.Mobile**、 选择一个位置 （或保留默认值），选择&quot;将添加到解决方案&quot;单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="54379-216">Name the project **PhotoGallery.Mobile**, select a location (or leave the default), select &quot;Add to solution&quot; and click **OK**.</span></span>
2. <span data-ttu-id="54379-217">在**新建 ASP.NET MVC 4 项目**对话框中，选择**移动应用程序**项目模板，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="54379-217">In the **New ASP.NET MVC 4 Project** dialog, select the **Mobile Application** project template and click **OK**.</span></span> <span data-ttu-id="54379-218">请确保您已选择 Razor 作为视图引擎。</span><span class="sxs-lookup"><span data-stu-id="54379-218">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="54379-219">![新建 ASP.NET MVC 4 移动应用程序](whats-new-in-aspnet-mvc-4/_static/image11.png "新建 ASP.NET MVC 4 移动应用程序")</span><span class="sxs-lookup"><span data-stu-id="54379-219">![Creating a new ASP.NET MVC 4 Mobile Application](whats-new-in-aspnet-mvc-4/_static/image11.png "Creating a new ASP.NET MVC 4 Mobile Application")</span></span>

    <span data-ttu-id="54379-220">*新建 ASP.NET MVC 4 移动应用程序*</span><span class="sxs-lookup"><span data-stu-id="54379-220">*Creating a new ASP.NET MVC 4 Mobile Application*</span></span>
3. <span data-ttu-id="54379-221">现在，你将能够浏览解决方案和签出引入的一些新功能由移动的 ASP.NET MVC 4 解决方案模板：</span><span class="sxs-lookup"><span data-stu-id="54379-221">Now you are able to explore the solution and check out some of the new features introduced by the ASP.NET MVC 4 solution template for mobile:</span></span>

    - <span data-ttu-id="54379-222">**jQuery Mobile 库**</span><span class="sxs-lookup"><span data-stu-id="54379-222">**jQuery Mobile Library**</span></span>

        <span data-ttu-id="54379-223">移动应用程序项目模板包括 jQuery Mobile 库，这是移动浏览器兼容性的开放源代码库。</span><span class="sxs-lookup"><span data-stu-id="54379-223">The Mobile Application project template includes the jQuery Mobile library, which is an open source library for mobile browser compatibility.</span></span> <span data-ttu-id="54379-224">jQuery Mobile 适用于移动浏览器支持 CSS 和 JavaScript 渐进增强。</span><span class="sxs-lookup"><span data-stu-id="54379-224">jQuery Mobile applies progressive enhancement to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="54379-225">渐进增强允许所有浏览器显示网页的基本内容，虽然它仅可用于最强大的浏览器来显示丰富内容。</span><span class="sxs-lookup"><span data-stu-id="54379-225">Progressive enhancement enables all browsers to display the basic content of a web page, while it only enables the most powerful browsers to display the rich content.</span></span> <span data-ttu-id="54379-226">JavaScript 和 CSS 文件，包含在 jQuery 移动样式，帮助移动浏览器为适合在屏幕中的内容，而无需进行任何更改的页标记中。</span><span class="sxs-lookup"><span data-stu-id="54379-226">The JavaScript and CSS files, included in the jQuery Mobile style, help mobile browsers to fit the content in the screen without making any change in the page markup.</span></span>

        ![jQuery-mobile-library-included-in-the-template](whats-new-in-aspnet-mvc-4/_static/image12.png)

        <span data-ttu-id="54379-228">*模板中包含的 jQuery mobile 库*</span><span class="sxs-lookup"><span data-stu-id="54379-228">*jQuery mobile library included in the template*</span></span>
    - <span data-ttu-id="54379-229">**基于 HTML5 标记**</span><span class="sxs-lookup"><span data-stu-id="54379-229">**HTML5 based markup**</span></span>

        ![Mobile-application-template-using-HTML5-markup](whats-new-in-aspnet-mvc-4/_static/image13.png)

        <span data-ttu-id="54379-231">*使用 HTML5 标记、 （Login.cshtml 和 index.cshtml） 的移动应用程序模板*</span><span class="sxs-lookup"><span data-stu-id="54379-231">*Mobile application template using HTML5 markup, (Login.cshtml and index.cshtml)*</span></span>
4. <span data-ttu-id="54379-232">按**F5**运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="54379-232">Press **F5** to run the solution.</span></span>
5. <span data-ttu-id="54379-233">打开**Windows Phone 7 仿真程序**。</span><span class="sxs-lookup"><span data-stu-id="54379-233">Open the **Windows Phone 7 Emulator**.</span></span>
6. <span data-ttu-id="54379-234">在 phone 开始屏幕中，打开 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="54379-234">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="54379-235">签出桌面应用程序的起始位置的 URL 并通过手机浏览到该 URL (例如`http://localhost:[PortNumber]/`)。</span><span class="sxs-lookup"><span data-stu-id="54379-235">Check out the URL where the desktop application started and browse to that URL from the phone (e.g. `http://localhost:[PortNumber]/`).</span></span>
7. <span data-ttu-id="54379-236">现在你已能够输入登录页或了解有关页面。</span><span class="sxs-lookup"><span data-stu-id="54379-236">Now you are able to enter the login page or check out the about page.</span></span> <span data-ttu-id="54379-237">请注意到该网站的样式基于新美俏移动设备的应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-237">Notice that the style of the website is based on the new Metro app for mobile.</span></span> <span data-ttu-id="54379-238">ASP.NET MVC 4 项目模板正确显示在移动设备，并确保页面的所有元素都可见且已启用。</span><span class="sxs-lookup"><span data-stu-id="54379-238">The ASP.NET MVC 4 project template is correctly displayed on mobile devices, making sure all the elements of the page are visible and enabled.</span></span> <span data-ttu-id="54379-239">请注意，在标头的链接不够大，无法单击或点击。</span><span class="sxs-lookup"><span data-stu-id="54379-239">Notice that the links on the header are big enough to be clicked or tapped.</span></span>

    <span data-ttu-id="54379-240">![项目模板在移动设备中的页](whats-new-in-aspnet-mvc-4/_static/image14.png "项目在移动设备中的模板页")</span><span class="sxs-lookup"><span data-stu-id="54379-240">![Project template pages in a mobile device](whats-new-in-aspnet-mvc-4/_static/image14.png "Project template pages in a mobile device")</span></span>

    <span data-ttu-id="54379-241">*在移动设备中的项目模板页*</span><span class="sxs-lookup"><span data-stu-id="54379-241">*Project template pages in a mobile device*</span></span>
8. <span data-ttu-id="54379-242">新模板还使用**视区元标记**。</span><span class="sxs-lookup"><span data-stu-id="54379-242">The new template also uses the **Viewport meta tag**.</span></span> <span data-ttu-id="54379-243">大多数移动浏览器定义一个虚拟的浏览器窗口的宽度或&quot;视区&quot;，该值大于移动设备的实际宽度。</span><span class="sxs-lookup"><span data-stu-id="54379-243">Most mobile browsers define a width for a virtual browser window or &quot;viewport&quot;, which is larger than the actual width of the mobile device.</span></span> <span data-ttu-id="54379-244">这使得移动浏览器以显示内部虚拟显示整个 web 页。</span><span class="sxs-lookup"><span data-stu-id="54379-244">This enables mobile browsers to display the entire web page inside the virtual display.</span></span> <span data-ttu-id="54379-245">**视区元标记**允许 web 开发人员可以在移动设备上设置的宽度、 高度和浏览器区域的小数位数**。**</span><span class="sxs-lookup"><span data-stu-id="54379-245">The **Viewport meta tag** allows web developers to set the width, height and scale of the browser area on mobile devices **.**</span></span> <span data-ttu-id="54379-246">移动应用程序的 ASP.NET MVC 4 模板将视区设置为设备宽度 (&quot;宽度 = 设备宽度&quot;) 中的布局模板 (*views/shared\_Layout.cshtml*)，以便所有页将具有设置为设备屏幕宽度其视区。</span><span class="sxs-lookup"><span data-stu-id="54379-246">The ASP.NET MVC 4 template for Mobile Applications sets the viewport to the device width (&quot;width=device-width&quot;) in the layout template (*Views\Shared\_Layout.cshtml*), so that all the pages will have their viewport set to the device screen width.</span></span> <span data-ttu-id="54379-247">请注意视区元标记不会更改默认浏览器视图。</span><span class="sxs-lookup"><span data-stu-id="54379-247">Notice that the Viewport meta tag will not change the default browser view.</span></span>
9. <span data-ttu-id="54379-248">打开 **\_Layout.cshtml**为位于**视图 |共享**文件夹，并注释视区 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="54379-248">Open **\_Layout.cshtml**, located in the **Views | Shared** folder, and comment the Viewport meta tag.</span></span> <span data-ttu-id="54379-249">运行该应用程序，如果不是已打开，并且签出差异。</span><span class="sxs-lookup"><span data-stu-id="54379-249">Run the application, if not already opened, and check out the differences.</span></span>


~~~
[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

![The site after commenting the viewport meta tag](whats-new-in-aspnet-mvc-4/_static/image15.png "The site after commenting the viewport meta tag")

*The site after commenting the viewport meta tag*
~~~
10. <span data-ttu-id="54379-250">在 Visual Studio 中，按**SHIFT** + **F5**来停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-250">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
11. <span data-ttu-id="54379-251">请取消注释视区 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="54379-251">Uncomment the viewport meta tag.</span></span>


~~~
[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]
~~~

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a><span data-ttu-id="54379-252">任务 3-使用自适应呈现</span><span class="sxs-lookup"><span data-stu-id="54379-252">Task 3 - Using Adaptive Rendering</span></span>

<span data-ttu-id="54379-253">在此任务中，你将学习另一种方法在没有任何自定义项的同一时间呈现在移动设备和 Web 浏览器上正常的网页。</span><span class="sxs-lookup"><span data-stu-id="54379-253">In this task, you will learn another method to render a Web page correctly on mobile devices and Web browsers at the same time without any customization.</span></span> <span data-ttu-id="54379-254">你已具有类似用途使用视区 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="54379-254">You have already used Viewport meta tag with a similar purpose.</span></span> <span data-ttu-id="54379-255">现在就可以满足另一种功能强大的方法：*自适应呈现*。</span><span class="sxs-lookup"><span data-stu-id="54379-255">Now you will meet another powerful method: *adaptive rendering*.</span></span>

<span data-ttu-id="54379-256">自适应呈现是使用一种技术**CSS3 媒体查询**以自定义应用于页面的样式。</span><span class="sxs-lookup"><span data-stu-id="54379-256">Adaptive rendering is a technique that uses **CSS3 media queries** to customize the style applied to a page.</span></span> <span data-ttu-id="54379-257">媒体查询定义分组特定条件下的 CSS 样式的样式表内的条件。</span><span class="sxs-lookup"><span data-stu-id="54379-257">Media queries define conditions inside a style sheet, grouping CSS styles under a certain condition.</span></span> <span data-ttu-id="54379-258">仅当条件为 true，则会将样式应用到已声明的对象。</span><span class="sxs-lookup"><span data-stu-id="54379-258">Only when the condition is true, the style is applied to the declared objects.</span></span>

<span data-ttu-id="54379-259">提供的自适应呈现技术的灵活性允许用于在不同设备上显示站点的任何自定义。</span><span class="sxs-lookup"><span data-stu-id="54379-259">The flexibility provided by the adaptive rendering technique enables any customization for displaying the site on different devices.</span></span> <span data-ttu-id="54379-260">你可以定义要在单个样式表而无需编写逻辑代码选择样式的所有样式。</span><span class="sxs-lookup"><span data-stu-id="54379-260">You can define as many styles as you want on a single style sheet without writing logic code to choose the style.</span></span> <span data-ttu-id="54379-261">因此，它是调整页样式的一种非常巧妙方法，因为这可以减少量重复的代码和呈现目的的逻辑。</span><span class="sxs-lookup"><span data-stu-id="54379-261">Therefore, it is a very neat way of adapting page styles, as it reduces the amount of duplicated code and logic for rendering purposes.</span></span> <span data-ttu-id="54379-262">另一方面，带宽消耗会增加，如 CSS 文件的大小会变得非常稍。</span><span class="sxs-lookup"><span data-stu-id="54379-262">On the other hand, bandwidth consumption would increase, as the size of your CSS files could grow marginally.</span></span>

<span data-ttu-id="54379-263">通过使用自适应呈现技术，你的站点将**正确显示，而不考虑浏览器。**</span><span class="sxs-lookup"><span data-stu-id="54379-263">By using the adaptive rendering technique, your site will be **displayed properly, regardless of the browser.**</span></span> <span data-ttu-id="54379-264">但是，你应考虑是否加载了额外的带宽是个问题。</span><span class="sxs-lookup"><span data-stu-id="54379-264">However, you should consider if the bandwidth extra load is a concern.</span></span>

> [!NOTE]
> <span data-ttu-id="54379-265">媒体查询的基本格式： @media \[作用域： 所有 | 手持 | 打印 | 投影 | 屏幕\]([属性： 值] 和...[属性： 值]）</span><span class="sxs-lookup"><span data-stu-id="54379-265">The basic format of a media query is: @media \[Scope: all | handheld | print | projection | screen\] ([property:value] and ... [property:value])</span></span>


<span data-ttu-id="54379-266">媒体查询的示例： &gt;  <strong>@media所有和 (最大宽度： 1000px) 和 (最小宽度： 700px) {}:</strong>针对 700px 和 1000px 之间的所有分辨率。</span><span class="sxs-lookup"><span data-stu-id="54379-266">Examples of media queries: &gt;<strong>@media all and (max-width: 1000px) and (min-width: 700px) {}:</strong> For all the resolutions between 700px and 1000px.</span></span>

> <span data-ttu-id="54379-267"><strong>@media 屏幕和 (最小宽度： 400px) 和 (最大宽度： 700px) {...}:</strong>仅对屏幕。</span><span class="sxs-lookup"><span data-stu-id="54379-267"><strong>@media screen and (min-width: 400px) and (max-width: 700px) { ... }:</strong> Only for screens.</span></span> <span data-ttu-id="54379-268">分辨率必须为介于 400 和 700px。</span><span class="sxs-lookup"><span data-stu-id="54379-268">The resolution must be between 400 and 700px.</span></span>
> 
> <span data-ttu-id="54379-269"><strong>@media 手持和 (最小宽度： 20em)，屏幕和 (最小宽度： 20em) {...}:</strong>手持设备 （移动设备和设备） 和屏幕。</span><span class="sxs-lookup"><span data-stu-id="54379-269"><strong>@media handheld and (min-width: 20em), screen and (min-width: 20em) { ... }:</strong> For handhelds(mobile and devices) and screens.</span></span> <span data-ttu-id="54379-270">最小宽度必须大于 20em。</span><span class="sxs-lookup"><span data-stu-id="54379-270">The minimum width must be greater than 20em.</span></span>
> 
> <span data-ttu-id="54379-271">你可以在上找到有关此的详细信息[W3C 站点](http://www.w3.org/TR/css3-mediaqueries/)。</span><span class="sxs-lookup"><span data-stu-id="54379-271">You can find more information about this on the [W3C site](http://www.w3.org/TR/css3-mediaqueries/).</span></span>


<span data-ttu-id="54379-272">您现在将了解自适应呈现的工作原理、 提高其可读性的 ASP.NET MVC 4 默认网站模板。</span><span class="sxs-lookup"><span data-stu-id="54379-272">You will now explore how the adaptive rendering works, improving the readability of the ASP.NET MVC 4 default website template.</span></span>

1. <span data-ttu-id="54379-273">打开**PhotoGallery.sln**解决方案具有在任务 1 中创建和选择**PhotoGallery**项目。</span><span class="sxs-lookup"><span data-stu-id="54379-273">Open the **PhotoGallery.sln** solution you have created at Task 1 and select the **PhotoGallery** project.</span></span> <span data-ttu-id="54379-274">按**F5**运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="54379-274">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="54379-275">调整浏览器的宽度，设置 windows 到一半或小于其原始大小的四分之一。</span><span class="sxs-lookup"><span data-stu-id="54379-275">Resize the browser's width, setting the windows to half or to less than a quarter of its original size.</span></span> <span data-ttu-id="54379-276">请注意与标头中的项会发生什么情况： 某些元素不会出现在标头的可见区域。</span><span class="sxs-lookup"><span data-stu-id="54379-276">Notice what happens with the items in the header: Some elements will not appear in the visible area of the header.</span></span>
3. <span data-ttu-id="54379-277">打开<strong>Site.css</strong>文件从 Visual Studio 解决方案资源管理器，位于<strong>内容</strong>项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="54379-277">Open <strong>Site.css</strong> file from the Visual Studio Solution explorer, located in <strong>Content</strong> project folder.</span></span> <span data-ttu-id="54379-278">按<strong>CTRL + F</strong>若要打开 Visual Studio 集成的搜索，并写入<strong>@media</strong>查找<strong>CSS 媒体查询</strong>。</span><span class="sxs-lookup"><span data-stu-id="54379-278">Press <strong>CTRL + F</strong> to open Visual Studio integrated search, and write <strong>@media</strong> to locate the <strong>CSS media query</strong>.</span></span>

    <span data-ttu-id="54379-279">此模板中定义的媒体查询条件的工作原理以这种方式： 当浏览器的窗口大小低于**850 px**，应用的 CSS 规则是在此媒体块内定义的。</span><span class="sxs-lookup"><span data-stu-id="54379-279">The media query condition defined in this template works in this way: When the browser's window size is below **850 px**, the CSS rules applied are the ones defined inside this media block.</span></span>

    <span data-ttu-id="54379-280">![定位到该媒体查询](whats-new-in-aspnet-mvc-4/_static/image16.png "定位到该媒体查询")</span><span class="sxs-lookup"><span data-stu-id="54379-280">![Locating the media query](whats-new-in-aspnet-mvc-4/_static/image16.png "Locating the media query")</span></span>

    <span data-ttu-id="54379-281">*定位到该媒体查询*</span><span class="sxs-lookup"><span data-stu-id="54379-281">*Locating the media query*</span></span>
4. <span data-ttu-id="54379-282">替换 850 中设置的最大宽度特性值与 px **10px**，禁用自适应呈现，以便按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="54379-282">Replace the max-width attribute value set in 850 px with **10px**, in order to disable the adaptive rendering, and press **CTRL + S** to save the changes.</span></span> <span data-ttu-id="54379-283">返回到浏览器和按**CTRL + F5**若要刷新的页中所做的更改。</span><span class="sxs-lookup"><span data-stu-id="54379-283">Return to the browser and press **CTRL + F5** to refresh the page with the changes you have made.</span></span> <span data-ttu-id="54379-284">在调整窗口的宽度，请注意这两个页中的差异。</span><span class="sxs-lookup"><span data-stu-id="54379-284">Notice the differences in both pages when adjusting the width of the window.</span></span>

    <span data-ttu-id="54379-285">![在左侧，应用页@media省略样式，请在右侧，样式](whats-new-in-aspnet-mvc-4/_static/image17.png "左侧，在应用页面@media省略样式，请在右侧，样式")</span><span class="sxs-lookup"><span data-stu-id="54379-285">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image17.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="54379-286"><em>在左侧，应用页@media省略样式，请在右侧，样式</em></span><span class="sxs-lookup"><span data-stu-id="54379-286"><em>In the left, the page is applying the @media style, in the right, the style is omitted</em></span></span>

    <span data-ttu-id="54379-287">现在，让我们了解移动设备上会发生什么情况：</span><span class="sxs-lookup"><span data-stu-id="54379-287">Now, let's check out what happens on mobile devices:</span></span>

    <span data-ttu-id="54379-288">![在左侧，应用页@media省略样式，请在右侧，样式](whats-new-in-aspnet-mvc-4/_static/image18.png "左侧，在应用页面@media省略样式，请在右侧，样式")</span><span class="sxs-lookup"><span data-stu-id="54379-288">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image18.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="54379-289"><em>在左侧，应用页@media省略样式，请在右侧，样式</em></span><span class="sxs-lookup"><span data-stu-id="54379-289"><em>In the left, the page is applying the @media style, in the right, the style is omitted</em></span></span>

    <span data-ttu-id="54379-290">尽管你会注意到，在 Web 浏览器中呈现页时的更改不非常重要，使用移动设备时的差异变得更加明显。</span><span class="sxs-lookup"><span data-stu-id="54379-290">Although you will notice that the changes when the page is rendered in a Web browser are not very significant, when using a mobile device the differences become more obvious.</span></span> <span data-ttu-id="54379-291">左侧的映像，我们可以看到的自定义样式改进可读性。</span><span class="sxs-lookup"><span data-stu-id="54379-291">On the left side of the image, we can see that the custom style improved the readability.</span></span>

    <span data-ttu-id="54379-292">可以在很多情况，从而更便于应用条件到网站样式和解决常见的样式问题，通过一种巧妙方法中使用自适应呈现。</span><span class="sxs-lookup"><span data-stu-id="54379-292">Adaptive rendering can be used in many more scenarios, making it easier to apply conditional styling to a Web site and solving common style issues with a neat approach.</span></span>

    <span data-ttu-id="54379-293">使你可以利用这些功能在任何 web 应用程序，并不特定于 ASP.NET MVC 4，视区元标记和 CSS 媒体查询。</span><span class="sxs-lookup"><span data-stu-id="54379-293">The Viewport meta tag and CSS media queries are not specific to ASP.NET MVC 4, so you can take advantage of these features in any web application.</span></span>
5. <span data-ttu-id="54379-294">在 Visual Studio 中，按**SHIFT** + **F5**来停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-294">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a><span data-ttu-id="54379-295">练习 2： 创建照片库 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="54379-295">Exercise 2: Creating the Photo Gallery Web Application</span></span>

<span data-ttu-id="54379-296">在本练习中，你将处理要显示照片的照片库应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-296">In this exercise, you will work on a Photo Gallery application to display photos.</span></span> <span data-ttu-id="54379-297">将开始使用 ASP.NET MVC 4 项目模板，，然后你将添加用于从服务中检索照片并将其显示在主页中的功能。</span><span class="sxs-lookup"><span data-stu-id="54379-297">You will start with the ASP.NET MVC 4 project template, and then you will add a feature to retrieve photos from a service and display them in the home page.</span></span>

<span data-ttu-id="54379-298">在以下练习中，你将更新此解决方案，以增强移动设备显示的方式。</span><span class="sxs-lookup"><span data-stu-id="54379-298">In the following exercise, you will update this solution to enhance the way it is displayed on mobile devices.</span></span>

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a><span data-ttu-id="54379-299">任务 1-创建 Mock 照片服务</span><span class="sxs-lookup"><span data-stu-id="54379-299">Task 1 - Creating a Mock Photo Service</span></span>

<span data-ttu-id="54379-300">在此任务中，你将创建照片要检索服务将在库中显示的内容的模型。</span><span class="sxs-lookup"><span data-stu-id="54379-300">In this task, you will create a mock of the photo service to retrieve the content that will be displayed in the gallery.</span></span> <span data-ttu-id="54379-301">若要执行此操作，将添加新的控制器，只需将返回一个 JSON 文件含有每张照片的数据。</span><span class="sxs-lookup"><span data-stu-id="54379-301">To do this, you will add a new controller that will simply return a JSON file with the data of each photo.</span></span>

1. <span data-ttu-id="54379-302">打开**Visual Studio**如果尚未打开。</span><span class="sxs-lookup"><span data-stu-id="54379-302">Open **Visual Studio** if not already opened.</span></span>
2. <span data-ttu-id="54379-303">选择**文件 |新 |项目**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="54379-303">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="54379-304">在**新项目**对话框中，选择**Visual C# |Web**左窗格中的模板树，并选择**ASP.NET MVC 4 Web 应用程序。**</span><span class="sxs-lookup"><span data-stu-id="54379-304">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="54379-305">将项目**PhotoGallery**、 选择一个位置 （或保留默认值），然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="54379-305">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span> <span data-ttu-id="54379-306">或者，您可以从现有的 ASP.NET MVC 4 继续工作**Internet 应用程序**解决方案从**练习 1**和跳过下一步。</span><span class="sxs-lookup"><span data-stu-id="54379-306">Alternatively, you can continue working from your existing ASP.NET MVC 4 **Internet Application** solution from **Exercise 1** and skip the next step.</span></span>
3. <span data-ttu-id="54379-307">在**新建 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**项目模板，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="54379-307">In the **New ASP.NET MVC 4 Project** dialog box, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="54379-308">请确保你具有 Razor 作为视图引擎选择。</span><span class="sxs-lookup"><span data-stu-id="54379-308">Make sure you have Razor selected as the View Engine.</span></span>
4. <span data-ttu-id="54379-309">在**解决方案资源管理器**，右键单击**应用\_数据**文件夹的项目，然后选择**添加 |现有项**。</span><span class="sxs-lookup"><span data-stu-id="54379-309">In the **Solution Explorer**, right-click the **App\_Data** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="54379-310">浏览到**Source\Assets\App\_数据**这个实验室的文件夹并添加**Photos.json**文件。</span><span class="sxs-lookup"><span data-stu-id="54379-310">Browse to the **Source\Assets\App\_Data** folder of this lab and add the **Photos.json** file.</span></span>
5. <span data-ttu-id="54379-311">使用名称创建新的控制器**PhotoController**。</span><span class="sxs-lookup"><span data-stu-id="54379-311">Create a new controller with the name **PhotoController**.</span></span> <span data-ttu-id="54379-312">若要执行此操作，右键单击**控制器**文件夹中，转到**添加**和选择**控制器。**</span><span class="sxs-lookup"><span data-stu-id="54379-312">To do this, right-click on the **Controllers** folder, go to **Add** and select **Controller.**</span></span> <span data-ttu-id="54379-313">完成该控制器的名称，保留**空 MVC 控制器**模板，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="54379-313">Complete the controller name, leave the **Empty MVC controller** template and click **Add**.</span></span>

    <span data-ttu-id="54379-314">![添加 PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "添加 PhotoController")</span><span class="sxs-lookup"><span data-stu-id="54379-314">![Adding the PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "Adding the PhotoController")</span></span>

    <span data-ttu-id="54379-315">*添加 PhotoController*</span><span class="sxs-lookup"><span data-stu-id="54379-315">*Adding the PhotoController*</span></span>
6. <span data-ttu-id="54379-316">替换**索引**方法替换为以下**库**操作，并从你最近添加到项目的 JSON 文件的返回内容。</span><span class="sxs-lookup"><span data-stu-id="54379-316">Replace the **Index** method with the following **Gallery** action, and return the content from the JSON file you have recently added to the project.</span></span>

    <span data-ttu-id="54379-317">(代码段- *ASP.NET MVC 4 实验-Ex02-库操作*)</span><span class="sxs-lookup"><span data-stu-id="54379-317">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Gallery Action*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
~~~
7. <span data-ttu-id="54379-318">按**F5**运行该解决方案，然后浏览到以下 URL 若要测试的模拟的照片服务： `http://localhost:[port]/photo/gallery` （[端口] 值依赖于已启动应用程序的当前端口）。</span><span class="sxs-lookup"><span data-stu-id="54379-318">Press **F5** to run the solution, and then browse to the following URL in order to test the mocked photo service: `http://localhost:[port]/photo/gallery` (the [port] value depends on the current port where the application was launched).</span></span> <span data-ttu-id="54379-319">对此 URL 的请求应检索其内容的**Photos.json**文件。</span><span class="sxs-lookup"><span data-stu-id="54379-319">The request to this URL should retrieve the content of the **Photos.json** file.</span></span>

    <span data-ttu-id="54379-320">![测试的模拟的照片服务](whats-new-in-aspnet-mvc-4/_static/image20.png "测试的模拟的照片服务")</span><span class="sxs-lookup"><span data-stu-id="54379-320">![Testing the mocked photo service](whats-new-in-aspnet-mvc-4/_static/image20.png "Testing the mocked photo service")</span></span>

    <span data-ttu-id="54379-321">*测试的模拟的照片服务*</span><span class="sxs-lookup"><span data-stu-id="54379-321">*Testing the mocked photo service*</span></span>

<span data-ttu-id="54379-322">你可以使用在实际实现[ASP.NET Web API](../../../../web-api/index.md)若要实现照片库服务。</span><span class="sxs-lookup"><span data-stu-id="54379-322">In a real implementation you could use [ASP.NET Web API](../../../../web-api/index.md) to implement the Photo Gallery service.</span></span> <span data-ttu-id="54379-323">ASP.NET Web API 是一个框架，可以轻松地生成覆盖广泛的客户端，包括浏览器和移动设备的 HTTP 服务。</span><span class="sxs-lookup"><span data-stu-id="54379-323">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="54379-324">ASP.NET Web API 是用于在 .NET Framework 上生成 RESTful 应用程序的理想平台。</span><span class="sxs-lookup"><span data-stu-id="54379-324">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a><span data-ttu-id="54379-325">任务 2-显示照片库</span><span class="sxs-lookup"><span data-stu-id="54379-325">Task 2 - Displaying the Photo Gallery</span></span>

<span data-ttu-id="54379-326">在此任务中，你将更新主页页后，可以通过使用在本练习中的第一个任务中创建模拟的服务显示照片库。</span><span class="sxs-lookup"><span data-stu-id="54379-326">In this task, you will update the Home page to show the photo gallery by using the mocked service you created in the first task of this exercise.</span></span> <span data-ttu-id="54379-327">你将添加模型文件和更新库视图。</span><span class="sxs-lookup"><span data-stu-id="54379-327">You will add model files and update the gallery views.</span></span>

1. <span data-ttu-id="54379-328">在 Visual Studio 中，按**SHIFT** + **F5**来停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-328">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="54379-329">创建**照片**类**模型**文件夹。</span><span class="sxs-lookup"><span data-stu-id="54379-329">Create the **Photo** class in the **Models** folder.</span></span> <span data-ttu-id="54379-330">若要执行此操作，右键单击**模型**文件夹，选择**添加**单击**类**。</span><span class="sxs-lookup"><span data-stu-id="54379-330">To do this, right-click on the **Models** folder, select **Add** and click **Class**.</span></span> <span data-ttu-id="54379-331">然后，将名称设置为**Photo.cs**单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="54379-331">Then, set the name to **Photo.cs** and click **Add**.</span></span>
3. <span data-ttu-id="54379-332">添加到以下成员**照片**类。</span><span class="sxs-lookup"><span data-stu-id="54379-332">Add the following members to the **Photo** class.</span></span>

    <span data-ttu-id="54379-333">(代码段- *ASP.NET MVC 4 实验-Ex02-照片模型*)</span><span class="sxs-lookup"><span data-stu-id="54379-333">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo model*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
~~~
4. <span data-ttu-id="54379-334">从“控制器”文件夹打开 HomeController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="54379-334">Open the **HomeController.cs** file from the **Controllers** folder.</span></span>
5. <span data-ttu-id="54379-335">添加下面的 using 语句。</span><span class="sxs-lookup"><span data-stu-id="54379-335">Add the following using statements.</span></span>

    <span data-ttu-id="54379-336">(代码段- *ASP.NET MVC 4 实验-Ex02-HomeController Using*)</span><span class="sxs-lookup"><span data-stu-id="54379-336">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - HomeController Usings*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
~~~
6. <span data-ttu-id="54379-337">更新**索引**操作使用**HttpClient**检索库数据，然后使用**JavaScriptSerializer**反其序列化到视图模型。</span><span class="sxs-lookup"><span data-stu-id="54379-337">Update the **Index** action to use **HttpClient** to retrieve the gallery data, and then use the **JavaScriptSerializer** to deserialize it to the view model.</span></span>

    <span data-ttu-id="54379-338">(代码段- *ASP.NET MVC 4 实验-Ex02-索引操作*)</span><span class="sxs-lookup"><span data-stu-id="54379-338">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Index Action*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
~~~
7. <span data-ttu-id="54379-339">打开**Index.cshtml**文件位于**views/home**文件夹，然后替换替换为以下代码的所有内容。</span><span class="sxs-lookup"><span data-stu-id="54379-339">Open the **Index.cshtml** file located under the **Views\Home** folder and replace all the content with the following code.</span></span>

    <span data-ttu-id="54379-340">此代码循环访问所有从服务检索的照片，并显示它们转换为无序的列表。</span><span class="sxs-lookup"><span data-stu-id="54379-340">This code loops through all the photos retrieved from the service and displays them into an unordered list.</span></span>

    <span data-ttu-id="54379-341">(代码段- *ASP.NET MVC 4 实验-Ex02-照片列表*)</span><span class="sxs-lookup"><span data-stu-id="54379-341">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo List*)</span></span>


~~~
[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
~~~
8. <span data-ttu-id="54379-342">在**解决方案资源管理器**，右键单击**内容**文件夹的项目，然后选择**添加 |现有项**。</span><span class="sxs-lookup"><span data-stu-id="54379-342">In the **Solution Explorer**, right-click the **Content** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="54379-343">浏览到**Source\Assets\Content**这个实验室的文件夹并添加**Site.css**文件。</span><span class="sxs-lookup"><span data-stu-id="54379-343">Browse to the **Source\Assets\Content** folder of this lab and add the **Site.css** file.</span></span> <span data-ttu-id="54379-344">你将需要确认其替换。</span><span class="sxs-lookup"><span data-stu-id="54379-344">You will have to confirm its replacement.</span></span> <span data-ttu-id="54379-345">如果你有**Site.css**文件打开时，你将需要确认还重新加载该文件。</span><span class="sxs-lookup"><span data-stu-id="54379-345">If you have the **Site.css** file open, you will have to confirm to reload the file also.</span></span>
9. <span data-ttu-id="54379-346">打开文件资源管理器并将复制整个**照片**文件夹位于下**Source\Assets**的解决方案资源管理器中的项目的根文件夹到本实验的文件夹。</span><span class="sxs-lookup"><span data-stu-id="54379-346">Open File Explorer and copy the entire **Photos** folder located under the **Source\Assets** folder of this lab to the root folder of your project in Solution Explorer.</span></span>
10. <span data-ttu-id="54379-347">运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-347">Run the application.</span></span> <span data-ttu-id="54379-348">你现在应看到在库中显示照片的主页。</span><span class="sxs-lookup"><span data-stu-id="54379-348">You should now see the home page displaying the photos in the gallery.</span></span>

    <span data-ttu-id="54379-349">![照片库](whats-new-in-aspnet-mvc-4/_static/image21.png "照片库")</span><span class="sxs-lookup"><span data-stu-id="54379-349">![Photo Gallery](whats-new-in-aspnet-mvc-4/_static/image21.png "Photo Gallery")</span></span>

    <span data-ttu-id="54379-350">*照片库*</span><span class="sxs-lookup"><span data-stu-id="54379-350">*Photo Gallery*</span></span>
11. <span data-ttu-id="54379-351">在 Visual Studio 中，按**SHIFT** + **F5**来停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-351">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a><span data-ttu-id="54379-352">练习 3： 添加对移动设备的支持</span><span class="sxs-lookup"><span data-stu-id="54379-352">Exercise 3: Adding support for mobile devices</span></span>

<span data-ttu-id="54379-353">ASP.NET MVC 4 中的密钥更新之一是对移动开发的支持。</span><span class="sxs-lookup"><span data-stu-id="54379-353">One of the key updates in ASP.NET MVC 4 is the support for mobile development.</span></span> <span data-ttu-id="54379-354">在此练习中，您将了解通过扩展 PhotoGallery 解决方案具有在上一练习中创建的 ASP.NET MVC 4 移动应用程序的新功能。</span><span class="sxs-lookup"><span data-stu-id="54379-354">In this exercise, you will explore ASP.NET MVC 4 new features for mobile applications by extending the PhotoGallery solution you have created in the previous exercise.</span></span>

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a><span data-ttu-id="54379-355">任务 1-ASP.NET MVC 4 应用程序中的安装 jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="54379-355">Task 1 - Installing jQuery Mobile in an ASP.NET MVC 4 Application</span></span>

1. <span data-ttu-id="54379-356">打开**开始**解决方案位于**源/Ex3-MobileSupport/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="54379-356">Open the **Begin** solution located at **Source/Ex3-MobileSupport/Begin/** folder.</span></span> <span data-ttu-id="54379-357">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="54379-357">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="54379-358">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="54379-358">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="54379-359">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="54379-359">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="54379-360">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="54379-360">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="54379-361">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="54379-361">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="54379-362">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="54379-362">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="54379-363">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="54379-363">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="54379-364">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="54379-364">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="54379-365">打开**程序包管理器控制台**通过单击**工具** &gt; **库程序包管理器** &gt; **程序包管理器控制台**菜单选项。</span><span class="sxs-lookup"><span data-stu-id="54379-365">Open the **Package Manager Console** by clicking the **Tools** &gt; **Library Package Manager** &gt; **Package Manager Console** menu option.</span></span>

    <span data-ttu-id="54379-366">![打开 NuGet 包管理器控制台](whats-new-in-aspnet-mvc-4/_static/image22.png "打开 NuGet 包管理器控制台")</span><span class="sxs-lookup"><span data-stu-id="54379-366">![Opening the NuGet Package Manager Console](whats-new-in-aspnet-mvc-4/_static/image22.png "Opening the NuGet Package Manager Console")</span></span>

    <span data-ttu-id="54379-367">*打开 NuGet 包管理器控制台*</span><span class="sxs-lookup"><span data-stu-id="54379-367">*Opening the NuGet Package Manager Console*</span></span>
3. <span data-ttu-id="54379-368">在程序包管理器控制台中运行以下命令以安装**jQuery.Mobile.MVC**包。</span><span class="sxs-lookup"><span data-stu-id="54379-368">In the Package Manager Console run the following command to install the **jQuery.Mobile.MVC** package.</span></span>

    <span data-ttu-id="54379-369">jQuery Mobile 是用于构建触控优化 web UI 一个开放源代码库。</span><span class="sxs-lookup"><span data-stu-id="54379-369">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="54379-370">JQuery.Mobile.MVC NuGet 程序包包括帮助器 jQuery Mobile 用于 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-370">The jQuery.Mobile.MVC NuGet package includes helpers to use jQuery Mobile with an ASP.NET MVC 4 application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="54379-371">通过运行以下命令，你将下载 jQuery.Mobile.MVC 库从 Nuget。</span><span class="sxs-lookup"><span data-stu-id="54379-371">By running the following command, you will be downloading the jQuery.Mobile.MVC library from Nuget.</span></span>

    <span data-ttu-id="54379-372">PM</span><span class="sxs-lookup"><span data-stu-id="54379-372">PM</span></span>

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    <span data-ttu-id="54379-373">此命令将安装 jQuery Mobile 和一些帮助程序文件，其中包括：</span><span class="sxs-lookup"><span data-stu-id="54379-373">This command installs jQuery Mobile and some helper files, including the following:</span></span>

    - <span data-ttu-id="54379-374">**视图/共享/\_Layout.Mobile.cshtml**： 是针对较小屏幕进行了优化的 jQuery 基于移动的布局。</span><span class="sxs-lookup"><span data-stu-id="54379-374">**Views/Shared/\_Layout.Mobile.cshtml**: is a jQuery Mobile-based layout optimized for a smaller screen.</span></span> <span data-ttu-id="54379-375">当网站收到请求时从移动浏览器时，它将替换原始布局 (\_Layout.cshtml) 替换为此。</span><span class="sxs-lookup"><span data-stu-id="54379-375">When the website receives a request from a mobile browser, it will replace the original layout (\_Layout.cshtml) with this one.</span></span>
    - <span data-ttu-id="54379-376">视图切换器组件： 组成**视图/共享/\_ViewSwitcher.cshtml**分部视图和**ViewSwitcherController.cs**控制器。</span><span class="sxs-lookup"><span data-stu-id="54379-376">A view-switcher component: consists of the **Views/Shared/\_ViewSwitcher.cshtml** partial view and the **ViewSwitcherController.cs** controller.</span></span> <span data-ttu-id="54379-377">此组件将在移动浏览器以使用户能够切换到桌面版本的页面上显示的链接。</span><span class="sxs-lookup"><span data-stu-id="54379-377">This component will show a link on mobile browsers to enable users to switch to the desktop version of the page.</span></span>  
        <span data-ttu-id="54379-378">![移动支持照片库项目](whats-new-in-aspnet-mvc-4/_static/image23.png "移动支持照片库项目")</span><span class="sxs-lookup"><span data-stu-id="54379-378">![Photo Gallery project with mobile support](whats-new-in-aspnet-mvc-4/_static/image23.png "Photo Gallery project with mobile support")</span></span>

        <span data-ttu-id="54379-379">*移动支持照片库项目*</span><span class="sxs-lookup"><span data-stu-id="54379-379">*Photo Gallery project with mobile support*</span></span>
4. <span data-ttu-id="54379-380">注册移动捆绑包。</span><span class="sxs-lookup"><span data-stu-id="54379-380">Register the Mobile bundles.</span></span> <span data-ttu-id="54379-381">若要执行此操作，打开**Global.asax.cs**文件并添加以下行。</span><span class="sxs-lookup"><span data-stu-id="54379-381">To do this, open the **Global.asax.cs** file and add the following line.</span></span>

    <span data-ttu-id="54379-382">(代码段- *ASP.NET MVC 4 实验室-Ex03-注册移动捆绑*)</span><span class="sxs-lookup"><span data-stu-id="54379-382">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - Register Mobile Bundles*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
~~~
5. <span data-ttu-id="54379-383">运行使用桌面 web 浏览器的应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-383">Run the application using a desktop web browser.</span></span>
6. <span data-ttu-id="54379-384">打开**Windows Phone 7 仿真程序中，**位于**开始菜单 |所有程序 |Windows Phone SDK 7.1 |Windows Phone 仿真程序。**</span><span class="sxs-lookup"><span data-stu-id="54379-384">Open the **Windows Phone 7 Emulator,** located in **Start Menu | All Programs | Windows Phone SDK 7.1 | Windows Phone Emulator.**</span></span>
7. <span data-ttu-id="54379-385">在 phone 开始屏幕中，打开 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="54379-385">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="54379-386">签出启动该应用程序的 URL 并浏览到 phone 浏览器使用该 URL (例如`http://localhost:[PortNumber]/`)。</span><span class="sxs-lookup"><span data-stu-id="54379-386">Check out the URL where the application started and browse to that URL with the phone browser (e.g. `http://localhost:[PortNumber]/`).</span></span>

    <span data-ttu-id="54379-387">你将注意到： 你的应用程序将看起来不同在 Windows Phone 模拟器中，如 jQuery.Mobile.MVC 具有显示针对移动设备进行了优化的视图在项目中创建新的资产。</span><span class="sxs-lookup"><span data-stu-id="54379-387">You will notice that your application will look different in the Windows Phone emulator, as the jQuery.Mobile.MVC has created new assets in your project that show views optimized for mobile devices.</span></span>

    <span data-ttu-id="54379-388">注意在手机上，显示的链接，切换到桌面视图顶部的消息。</span><span class="sxs-lookup"><span data-stu-id="54379-388">Notice the message at the top of the phone, showing the link that switches to the Desktop view.</span></span> <span data-ttu-id="54379-389">此外，  **\_Layout.Mobile.cshtml**由已安装的包的布局应用程序中包括一个不同的布局。</span><span class="sxs-lookup"><span data-stu-id="54379-389">Additionally, the **\_Layout.Mobile.cshtml** layout that was created by the package you have installed is including a different layout in the application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="54379-390">到目前为止，没有要返回到移动视图的链接。</span><span class="sxs-lookup"><span data-stu-id="54379-390">So far, there is no link to get back to mobile view.</span></span> <span data-ttu-id="54379-391">它将包括在更高版本。</span><span class="sxs-lookup"><span data-stu-id="54379-391">It will be included in later versions.</span></span>

    <span data-ttu-id="54379-392">![照片库主页上的移动视图](whats-new-in-aspnet-mvc-4/_static/image24.png "移动视图的照片库主页")</span><span class="sxs-lookup"><span data-stu-id="54379-392">![Mobile view of the Photo Gallery Home page](whats-new-in-aspnet-mvc-4/_static/image24.png "Mobile view of the Photo Gallery Home page")</span></span>

    <span data-ttu-id="54379-393">*移动视图的照片库主页*</span><span class="sxs-lookup"><span data-stu-id="54379-393">*Mobile view of the Photo Gallery Home page*</span></span>
8. <span data-ttu-id="54379-394">在 Visual Studio 中，按**SHIFT** + **F5**来停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-394">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a><span data-ttu-id="54379-395">任务 2-创建移动视图</span><span class="sxs-lookup"><span data-stu-id="54379-395">Task 2 - Creating Mobile Views</span></span>

<span data-ttu-id="54379-396">在此任务中，将使用适用于移动设备中的更好 appareance 的内容创建索引视图的移动版本。</span><span class="sxs-lookup"><span data-stu-id="54379-396">In this task, you will create a mobile version of the index view with content adapted for better appareance in mobile devices.</span></span>

1. <span data-ttu-id="54379-397">复制**Views\Home\Index.cshtml**查看并将其创建的副本，请重命名新文件与粘贴**Index.Mobile.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="54379-397">Copy the **Views\Home\Index.cshtml** view and paste it to create a copy, rename the new file to **Index.Mobile.cshtml**.</span></span>
2. <span data-ttu-id="54379-398">打开新创建**Index.Mobile.cshtml**查看和将现有&lt;ul&gt;标记替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="54379-398">Open the new created **Index.Mobile.cshtml** view and replace the existing &lt;ul&gt; tag with this code.</span></span> <span data-ttu-id="54379-399">通过执行此操作，你将更新&lt;ul&gt;标记中使用 jQuery 移动数据注释，用于从 jQuery 移动的主题。</span><span class="sxs-lookup"><span data-stu-id="54379-399">By doing this, you will be updating the &lt;ul&gt; tag with jQuery Mobile data annotations to use the mobile themes from jQuery.</span></span>


~~~
[!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

> [!NOTE] 
> 
> Notice that:
> 
> - The **data-role** attribute set to **listview** will render the list using the listview styles.
> 
> - The **data-inset** attribute set to true will show the list with rounded border and margin.
> 
> - The **data-filter** attribute set to **true** will generate a search box.
> 
> You can learn more about jQuery Mobile conventions in the project documentation: [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)
~~~
3. <span data-ttu-id="54379-400">按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="54379-400">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="54379-401">切换到**Windows Phone 仿真程序**和刷新站点。</span><span class="sxs-lookup"><span data-stu-id="54379-401">Switch to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="54379-402">请注意新的外观和感觉的库列表中，以及新的搜索框位于顶部。</span><span class="sxs-lookup"><span data-stu-id="54379-402">Notice the new look and feel of the gallery list, as well as the new search box located on the top.</span></span> <span data-ttu-id="54379-403">然后，在搜索框中键入一个词 (例如，**郁金香**) 照片库中开始搜索。</span><span class="sxs-lookup"><span data-stu-id="54379-403">Then, type a word in the search box (for instance, **Tulips**) to start a search in the photo gallery.</span></span>

    <span data-ttu-id="54379-404">![使用 listview 样式筛选的库](whats-new-in-aspnet-mvc-4/_static/image25.png "库使用 listview 样式筛选")</span><span class="sxs-lookup"><span data-stu-id="54379-404">![Gallery using listview style with filtering](whats-new-in-aspnet-mvc-4/_static/image25.png "Gallery using listview style with filtering")</span></span>

    <span data-ttu-id="54379-405">*使用 listview 样式筛选的库*</span><span class="sxs-lookup"><span data-stu-id="54379-405">*Gallery using listview style with filtering*</span></span>

    <span data-ttu-id="54379-406">总之，你使用的视图可持续配方创建索引视图中处理的副本&quot;移动&quot;后缀。</span><span class="sxs-lookup"><span data-stu-id="54379-406">To summarize, you have used the View Mobilizer recipe to create a copy of the Index view with the &quot;mobile&quot; suffix.</span></span> <span data-ttu-id="54379-407">此后缀指示 ASP.NET MVC 4，从移动设备生成的每个请求将使用此副本的索引。</span><span class="sxs-lookup"><span data-stu-id="54379-407">This suffix indicates to ASP.NET MVC 4 that every request generated from a mobile device will use this copy of the index.</span></span> <span data-ttu-id="54379-408">此外，您已更新要使用 jQuery Mobile 增强站点外观和感觉，移动设备中的索引视图的移动版本。</span><span class="sxs-lookup"><span data-stu-id="54379-408">Additionally, you have updated the mobile version of the Index view to use jQuery Mobile for enhancing the site look and feel in mobile devices.</span></span>
5. <span data-ttu-id="54379-409">返回到 Visual Studio 和打开**Site.Mobile.css**位于**内容**文件夹。</span><span class="sxs-lookup"><span data-stu-id="54379-409">Go back to Visual Studio and open **Site.Mobile.css** located under the **Content** folder.</span></span>
6. <span data-ttu-id="54379-410">修复该照片标题，以使其显示在右侧的映像的位置。</span><span class="sxs-lookup"><span data-stu-id="54379-410">Fix the positioning of the photo title to make it show at the right side of the image.</span></span> <span data-ttu-id="54379-411">若要执行此操作，将添加到下面的代码**Site.Mobile.css**文件。</span><span class="sxs-lookup"><span data-stu-id="54379-411">To do this, add the following code to the **Site.Mobile.css** file.</span></span>

    <span data-ttu-id="54379-412">CSS</span><span class="sxs-lookup"><span data-stu-id="54379-412">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. <span data-ttu-id="54379-413">按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="54379-413">Press **CTRL + S** to save the changes.</span></span>
8. <span data-ttu-id="54379-414">切换回**Windows Phone 仿真程序**和刷新站点。</span><span class="sxs-lookup"><span data-stu-id="54379-414">Switch back to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="54379-415">请注意照片标题正确现在定位。</span><span class="sxs-lookup"><span data-stu-id="54379-415">Notice the photo title is properly positioned now.</span></span>

    <span data-ttu-id="54379-416">![定位图像右侧标题](whats-new-in-aspnet-mvc-4/_static/image26.png "定位图像右侧的标题")</span><span class="sxs-lookup"><span data-stu-id="54379-416">![Title positioned on the right side of the image](whats-new-in-aspnet-mvc-4/_static/image26.png "Title positioned on the right side of the image")</span></span>

    <span data-ttu-id="54379-417">*定位图像右侧的标题*</span><span class="sxs-lookup"><span data-stu-id="54379-417">*Title positioned on the right side of the image*</span></span>

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a><span data-ttu-id="54379-418">任务 3-jQuery Mobile 主题</span><span class="sxs-lookup"><span data-stu-id="54379-418">Task 3 - jQuery Mobile Themes</span></span>

<span data-ttu-id="54379-419">每个布局和小组件中 jQuery Mobile 在于，围绕设计就将完成统一的可视化设计主题应用于站点和应用程序新的面向对象的 CSS 框架。</span><span class="sxs-lookup"><span data-stu-id="54379-419">Every layout and widget in jQuery Mobile is designed around a new object-oriented CSS framework that makes it possible to apply a complete unified visual design theme to sites and applications.</span></span>

<span data-ttu-id="54379-420">jQuery Mobile 默认情况下主题包括 5 样本是否指定字母 (a、 b、 c、 d、 e） 供快速引用。</span><span class="sxs-lookup"><span data-stu-id="54379-420">jQuery Mobile's default Theme includes 5 swatches that are given letters (a, b, c, d, e) for quick reference.</span></span>

<span data-ttu-id="54379-421">在此任务中，你将更新要使用不同的主题，而不是默认的移动布局。</span><span class="sxs-lookup"><span data-stu-id="54379-421">In this task, you will update the mobile layout to use a different theme than the default.</span></span>

1. <span data-ttu-id="54379-422">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="54379-422">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="54379-423">打开 **\_Layout.Mobile.cshtml**文件位于**views/shared**。</span><span class="sxs-lookup"><span data-stu-id="54379-423">Open the **\_Layout.Mobile.cshtml** file located in **Views\Shared**.</span></span>
3. <span data-ttu-id="54379-424">使用数据的角色设置为找到的 div 元素&quot;页&quot;和更新**数据主题**到&quot; **e**&quot;。</span><span class="sxs-lookup"><span data-stu-id="54379-424">Find the div element with the data-role set to &quot;page&quot; and update the **data-theme** to &quot;**e**&quot;.</span></span>


~~~
[!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
~~~
4. <span data-ttu-id="54379-425">按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="54379-425">Press **CTRL + S** to save the changes.</span></span>
5. <span data-ttu-id="54379-426">刷新中的站点**Windows Phone 仿真程序**并留意新的颜色方案。</span><span class="sxs-lookup"><span data-stu-id="54379-426">Refresh the site in the **Windows Phone Emulator** and notice the new colors scheme.</span></span>

    <span data-ttu-id="54379-427">![具有不同的配色方案的移动布局](whats-new-in-aspnet-mvc-4/_static/image27.png "具有不同的配色方案的移动布局")</span><span class="sxs-lookup"><span data-stu-id="54379-427">![Mobile layout with a different color scheme](whats-new-in-aspnet-mvc-4/_static/image27.png "Mobile layout with a different color scheme")</span></span>

    <span data-ttu-id="54379-428">*具有不同的配色方案的移动布局*</span><span class="sxs-lookup"><span data-stu-id="54379-428">*Mobile layout with a different color scheme*</span></span>

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a><span data-ttu-id="54379-429">任务 4-使用视图切换器组件和重写功能的浏览器</span><span class="sxs-lookup"><span data-stu-id="54379-429">Task 4 - Using the View-Switcher Component and the Browser Overriding Features</span></span>

<span data-ttu-id="54379-430">移动优化网页中的约定是将添加其文本是如桌面视图或完整的站点模式，从而让用户切换到该页面的桌面版本的链接。</span><span class="sxs-lookup"><span data-stu-id="54379-430">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="54379-431">JQuery.Mobile.MVC 包包括一个示例，**视图切换器**组件为用于此目的 **\_Layout.Mobile.cshtml**视图。</span><span class="sxs-lookup"><span data-stu-id="54379-431">The jQuery.Mobile.MVC package includes a sample **view-switcher** component for this purpose used in the **\_Layout.Mobile.cshtml** view.</span></span>

<span data-ttu-id="54379-432">![链接以切换到桌面视图](whats-new-in-aspnet-mvc-4/_static/image28.png "链接以切换到桌面视图")</span><span class="sxs-lookup"><span data-stu-id="54379-432">![Link to switch to Desktop View](whats-new-in-aspnet-mvc-4/_static/image28.png "Link to switch to Desktop View")</span></span>

<span data-ttu-id="54379-433">*用于切换到桌面视图的链接*</span><span class="sxs-lookup"><span data-stu-id="54379-433">*Link to switch to Desktop View*</span></span>

<span data-ttu-id="54379-434">视图切换器使用称为的新增功能**浏览器重写**。</span><span class="sxs-lookup"><span data-stu-id="54379-434">The view switcher uses a new feature called **Browser Overriding**.</span></span> <span data-ttu-id="54379-435">此功能允许你的应用程序处理请求，就像它们来自于它们实际来自其他浏览器 （用户代理）。</span><span class="sxs-lookup"><span data-stu-id="54379-435">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they are actually coming from.</span></span>

<span data-ttu-id="54379-436">在此任务中，您将了解视图切换器添加 jQuery.Mobile.MVC 和重写 ASP.NET MVC 4 中的功能的新浏览器的示例实现。</span><span class="sxs-lookup"><span data-stu-id="54379-436">In this task, you will explore the sample implementation of a view-switcher added by jQuery.Mobile.MVC and the new browser overriding features in ASP.NET MVC 4.</span></span>

1. <span data-ttu-id="54379-437">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="54379-437">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="54379-438">打开 **\_Layout.Mobile.cshtml**视图位于**views/shared**文件夹，请注意为分部视图所引用的视图切换器组件。</span><span class="sxs-lookup"><span data-stu-id="54379-438">Open the **\_Layout.Mobile.cshtml** view located under the **Views\Shared** folder and notice the view-switcher component being referenced as a partial view.</span></span>

    <span data-ttu-id="54379-439">![使用视图切换器组件的移动布局](whats-new-in-aspnet-mvc-4/_static/image29.png "使用视图切换器组件的移动布局")</span><span class="sxs-lookup"><span data-stu-id="54379-439">![Mobile layout using View-Switcher component](whats-new-in-aspnet-mvc-4/_static/image29.png "Mobile layout using View-Switcher component")</span></span>

    <span data-ttu-id="54379-440">*使用视图切换器组件的移动布局*</span><span class="sxs-lookup"><span data-stu-id="54379-440">*Mobile layout using View-Switcher component*</span></span>
3. <span data-ttu-id="54379-441">打开 **\_ViewSwitcher.cshtml**分部视图。</span><span class="sxs-lookup"><span data-stu-id="54379-441">Open the **\_ViewSwitcher.cshtml** partial view.</span></span>

    <span data-ttu-id="54379-442">分部视图使用的新方法**ViewContext.HttpContext.GetOverriddenBrowser()**确定 web 请求的源，并显示相应的链接可切换到桌面或移动视图。</span><span class="sxs-lookup"><span data-stu-id="54379-442">The partial view uses the new method **ViewContext.HttpContext.GetOverriddenBrowser()** to determine the origin of the web request and show the corresponding link to switch either to the Desktop or Mobile views.</span></span>

    <span data-ttu-id="54379-443">**GetOverridenBrowser**方法返回**HttpBrowserCapabilitiesBase**对应于当前为请求设置的用户代理的实例 （实际或重写）。</span><span class="sxs-lookup"><span data-stu-id="54379-443">The **GetOverridenBrowser** method returns an **HttpBrowserCapabilitiesBase** instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="54379-444">你可以使用此值以获取属性，如**IsMobileDevice**。</span><span class="sxs-lookup"><span data-stu-id="54379-444">You can use this value to get properties such as **IsMobileDevice**.</span></span>

    <span data-ttu-id="54379-445">![ViewSwitcher 分部视图](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 分部视图")</span><span class="sxs-lookup"><span data-stu-id="54379-445">![ViewSwitcher partial view](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher partial view")</span></span>

    <span data-ttu-id="54379-446">*ViewSwitcher 分部视图*</span><span class="sxs-lookup"><span data-stu-id="54379-446">*ViewSwitcher partial view*</span></span>
4. <span data-ttu-id="54379-447">打开**ViewSwitcherController.cs**类位于**控制器**文件夹。</span><span class="sxs-lookup"><span data-stu-id="54379-447">Open the **ViewSwitcherController.cs** class located in the **Controllers** folder.</span></span> <span data-ttu-id="54379-448">签出该 SwitchView 操作由 ViewSwitcher 组件中的链接，并注意新的 HttpContext 方法。</span><span class="sxs-lookup"><span data-stu-id="54379-448">Check out that SwitchView action is called by the link in the ViewSwitcher component, and notice the new HttpContext methods.</span></span>

    - <span data-ttu-id="54379-449">**HttpContext.ClearOverridenBrowser()**方法移除当前请求的任何重写的用户代理。</span><span class="sxs-lookup"><span data-stu-id="54379-449">The **HttpContext.ClearOverridenBrowser()** method removes any overridden user agent for the current request.</span></span>
    - <span data-ttu-id="54379-450">**HttpContext.SetOverridenBrowser()**方法重写请求的实际用户代理值使用指定的用户代理。</span><span class="sxs-lookup"><span data-stu-id="54379-450">The **HttpContext.SetOverridenBrowser()** method overrides the request's actual user agent value using the specified user agent.</span></span>  
        <span data-ttu-id="54379-451">![ViewSwitcher 控制器](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher 控制器")</span><span class="sxs-lookup"><span data-stu-id="54379-451">![ViewSwitcher Controller](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher Controller")</span></span>  
<span data-ttu-id="54379-452">*ViewSwitcher 控制器*</span><span class="sxs-lookup"><span data-stu-id="54379-452">*ViewSwitcher Controller*</span></span>

        <span data-ttu-id="54379-453">浏览器重写是一项核心功能的 ASP.NET MVC 4 中，即使你不安装 jQuery.Mobile.MVC 包，这是也可用。</span><span class="sxs-lookup"><span data-stu-id="54379-453">Browser Overriding is a core feature of ASP.NET MVC 4, which is also available even if you do not install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="54379-454">但是，此功能会影响仅视图、 布局和分部视图，并且它不影响任何依赖于 Request.Browser 对象的功能。</span><span class="sxs-lookup"><span data-stu-id="54379-454">However, this feature affects only view, layout, and partial-view, and it does not affect any of the features that depend on the Request.Browser object.</span></span>

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a><span data-ttu-id="54379-455">任务 5-在桌面视图中添加视图切换器</span><span class="sxs-lookup"><span data-stu-id="54379-455">Task 5 - Adding the View-Switcher in the Desktop View</span></span>

<span data-ttu-id="54379-456">在此任务中，你将更新桌面的布局，以包括视图切换器。</span><span class="sxs-lookup"><span data-stu-id="54379-456">In this task, you will update the desktop layout to include the view-switcher.</span></span> <span data-ttu-id="54379-457">这将允许移动用户在浏览桌面视图时返回到移动视图。</span><span class="sxs-lookup"><span data-stu-id="54379-457">This will allow mobile users to go back to the mobile view when browsing the desktop view.</span></span>

1. <span data-ttu-id="54379-458">刷新中的站点**Windows Phone 仿真程序**。</span><span class="sxs-lookup"><span data-stu-id="54379-458">Refresh the site in the **Windows Phone Emulator**.</span></span>
2. <span data-ttu-id="54379-459">单击**桌面视图**顶部的库的链接。</span><span class="sxs-lookup"><span data-stu-id="54379-459">Click on the **Desktop view** link at the top of the gallery.</span></span> <span data-ttu-id="54379-460">请注意在桌面的视图，从而使你返回到移动视图中没有任何视图切换器。</span><span class="sxs-lookup"><span data-stu-id="54379-460">Notice there is no view-switcher in the desktop view to allow you return to the mobile view.</span></span>
3. <span data-ttu-id="54379-461">返回到 Visual Studio 和打开 **\_Layout.cshtml**视图。</span><span class="sxs-lookup"><span data-stu-id="54379-461">Go back to Visual Studio and open the **\_Layout.cshtml** view.</span></span>
4. <span data-ttu-id="54379-462">查找登录部分和插入的调用来呈现 **\_ViewSwitcher**下面的部分视图 **\_LogOnPartial**分部视图。</span><span class="sxs-lookup"><span data-stu-id="54379-462">Find the login section and insert a call to render the **\_ViewSwitcher** partial view below the **\_LogOnPartial** partial view.</span></span> <span data-ttu-id="54379-463">然后，按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="54379-463">Then, press **CTRL + S** to save the changes.</span></span>


~~~
[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
~~~
5. <span data-ttu-id="54379-464">按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="54379-464">Press **CTRL + S** to save the changes.</span></span>
6. <span data-ttu-id="54379-465">刷新 Windows Phone 仿真程序中的页，然后双击以放大屏幕。</span><span class="sxs-lookup"><span data-stu-id="54379-465">Refresh the page in the Windows Phone Emulator and double-click the screen to zoom in.</span></span> <span data-ttu-id="54379-466">请注意，主页页面现在显示**移动视图**从移动切换到桌面视图的链接。</span><span class="sxs-lookup"><span data-stu-id="54379-466">Notice that the home page now shows the **Mobile view** link that switches from mobile to desktop view.</span></span>

    <span data-ttu-id="54379-467">![查看在桌面视图中呈现的切换器](whats-new-in-aspnet-mvc-4/_static/image32.png "在桌面视图中呈现的视图切换器")</span><span class="sxs-lookup"><span data-stu-id="54379-467">![View Switcher rendered in desktop view](whats-new-in-aspnet-mvc-4/_static/image32.png "View Switcher rendered in desktop view")</span></span>

    <span data-ttu-id="54379-468">*在桌面视图中呈现的视图切换器*</span><span class="sxs-lookup"><span data-stu-id="54379-468">*View Switcher rendered in desktop view*</span></span>
7. <span data-ttu-id="54379-469">重新切换到移动视图，并浏览到<strong>有关</strong>页 (http://localhost[端口] / Home/有关)。</span><span class="sxs-lookup"><span data-stu-id="54379-469">Switch to the Mobile view again and browse to <strong>About</strong> page (http://localhost[port]/Home/About).</span></span> <span data-ttu-id="54379-470">请注意，即使你尚未创建 About.Mobile.cshtml 视图，关于页面显示使用移动布局 (\_Layout.Mobile.cshtml)。</span><span class="sxs-lookup"><span data-stu-id="54379-470">Notice that, even if you haven't created an About.Mobile.cshtml view, the About page is displayed using the mobile layout (\_Layout.Mobile.cshtml).</span></span>

    <span data-ttu-id="54379-471">![有关页面](whats-new-in-aspnet-mvc-4/_static/image33.png "有关页面")</span><span class="sxs-lookup"><span data-stu-id="54379-471">![About page](whats-new-in-aspnet-mvc-4/_static/image33.png "About page")</span></span>

    <span data-ttu-id="54379-472">*有关页面*</span><span class="sxs-lookup"><span data-stu-id="54379-472">*About page*</span></span>
8. <span data-ttu-id="54379-473">最后，在桌面的 Web 浏览器中打开网站。</span><span class="sxs-lookup"><span data-stu-id="54379-473">Finally, open the site in a desktop Web browser.</span></span> <span data-ttu-id="54379-474">请注意的任何以前的更新影响桌面视图。</span><span class="sxs-lookup"><span data-stu-id="54379-474">Notice that none of the previous updates has affected the desktop view.</span></span>

    <span data-ttu-id="54379-475">![图片库桌面视图](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery 桌面视图")</span><span class="sxs-lookup"><span data-stu-id="54379-475">![PhotoGallery desktop view](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery desktop view")</span></span>

    <span data-ttu-id="54379-476">*图片库桌面视图*</span><span class="sxs-lookup"><span data-stu-id="54379-476">*PhotoGallery desktop view*</span></span>

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a><span data-ttu-id="54379-477">任务 6-创建新的显示模式</span><span class="sxs-lookup"><span data-stu-id="54379-477">Task 6 - Creating New Display Modes</span></span>

<span data-ttu-id="54379-478">使用新的显示模式功能，应用程序选择具体取决于正在生成请求的浏览器的视图。</span><span class="sxs-lookup"><span data-stu-id="54379-478">The new display modes feature lets an application select views depending on the browser that is generating the request.</span></span> <span data-ttu-id="54379-479">例如，如果桌面浏览器请求主页上，该应用程序将返回**Views\Home\Index.cshtml**模板。</span><span class="sxs-lookup"><span data-stu-id="54379-479">For example, if a desktop browser requests the Home page, the application will return the **Views\Home\Index.cshtml** template.</span></span> <span data-ttu-id="54379-480">然后，如果移动浏览器请求主页上，该应用程序将返回**Views\Home\Index.mobile.cshtml**模板。</span><span class="sxs-lookup"><span data-stu-id="54379-480">Then, if a mobile browser requests the Home page, the application will return the **Views\Home\Index.mobile.cshtml** template.</span></span>

<span data-ttu-id="54379-481">在此任务中，你将创建的自定义的布局的 iPhone 设备，并必须以模拟 iPhone 设备发出的请求。</span><span class="sxs-lookup"><span data-stu-id="54379-481">In this task, you will create a customized layout for iPhone devices, and you will have to simulate requests from iPhone devices.</span></span> <span data-ttu-id="54379-482">若要执行此操作，可以使用任一一个 iPhone 仿真程序/仿真程序 (如[Electric 移动模拟器](http://www.electricplum.com/)) 或外接程序中修改用户代理使用的浏览器。</span><span class="sxs-lookup"><span data-stu-id="54379-482">To do this, you can use either an iPhone emulator/simulator (like [Electric Mobile Simulator](http://www.electricplum.com/)) or a browser with add-ons that modify the user agent.</span></span> <span data-ttu-id="54379-483">有关如何在 Safari 浏览器中设置的用户代理字符串以模拟 iPhone 的说明，请参阅[如何让 Safari 模拟很 IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) David Alison 的博文中。</span><span class="sxs-lookup"><span data-stu-id="54379-483">For instructions on how to set the user agent string in an Safari browser to emulate an iPhone, see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) in David Alison's blog.</span></span>

<span data-ttu-id="54379-484">**请注意，此任务是可选的可以在实验室整个继续而不执行它。**</span><span class="sxs-lookup"><span data-stu-id="54379-484">**Notice that this task is optional and you can continue throughout the lab without executing it.**</span></span>

1. <span data-ttu-id="54379-485">在 Visual Studio 中，按**SHIFT** + **F5**来停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-485">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="54379-486">打开**Global.asax.cs**并添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="54379-486">Open **Global.asax.cs** and add the following using statement.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
~~~
3. <span data-ttu-id="54379-487">将以下突出显示的代码添加到应用程序\_Start 方法。</span><span class="sxs-lookup"><span data-stu-id="54379-487">Add the following highlighted code into the Application\_Start method.</span></span>

    <span data-ttu-id="54379-488">(代码段- *ASP.NET MVC 4 实验室-Ex03-iPhone DisplayMode*)</span><span class="sxs-lookup"><span data-stu-id="54379-488">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - iPhone DisplayMode*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

You have registered a new **DefaultDisplayMode named &quot;iPhone&quot;**, within the static **DisplayModeProvider.Instance.Modes** static list, that will be matched against each incoming request. If the incoming request contains the string &quot;iPhone&quot;, ASP.NET MVC will find the views whose name contain the &quot;iPhone&quot; suffix. The 0 parameter indicates how specific is the new mode; for instance, this view is more specific than the general &quot;.mobile&quot; rule that matches requests from mobile devices.

After this code runs, when an iPhone browser generates a request, your application will use the **Views\Shared\\_Layout.iPhone.cshtml** layout you will create in the next steps.

> [!NOTE]
> This way of testing the request for iPhone has been simplified for demo purposes and might not work as expected for every iPhone user agent string (for example test is case sensitive).
~~~
4. <span data-ttu-id="54379-489">创建一份 **\_Layout.Mobile.cshtml**文件中**views/shared**文件夹并将复制到重命名&quot;  **\_Layout.iPhone.csthml**&quot;.</span><span class="sxs-lookup"><span data-stu-id="54379-489">Create a copy of the **\_Layout.Mobile.cshtml** file in the **Views\Shared** folder and rename the copy to &quot;**\_Layout.iPhone.csthml**&quot;.</span></span>
5. <span data-ttu-id="54379-490">打开 **\_Layout.iPhone.csthml**你在上一步中创建。</span><span class="sxs-lookup"><span data-stu-id="54379-490">Open **\_Layout.iPhone.csthml** you created in the previous step.</span></span>
6. <span data-ttu-id="54379-491">将数据角色属性设置为使用找到的 div 元素**页**和更改**数据主题**属性设为&quot; &quot;。</span><span class="sxs-lookup"><span data-stu-id="54379-491">Find the div element with the data-role attribute set to **page** and change the **data-theme** attribute to &quot;**a**&quot;.</span></span>


~~~
[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

Now you have 3 layouts in your ASP.NET MVC 4 application:

1. **\_Layout.cshtml**: default layout used for desktop browsers.
2. **\_Layout.mobile.cshtml**: default layout used for mobile devices.
3. **\_Layout.iPhone.cshtml**: specific layout for iPhone devices, using a different color scheme to differentiate from \_Layout.mobile.cshtml.
~~~
7. <span data-ttu-id="54379-492">按**F5**运行该应用程序和浏览中的站点**Windows Phone 仿真程序**。</span><span class="sxs-lookup"><span data-stu-id="54379-492">Press **F5** to run the application and browse the site in the **Windows Phone Emulator**.</span></span>
8. <span data-ttu-id="54379-493">打开**iPhone 模拟器**(请参阅[附录 C](#AppendixC)有关如何安装和配置 iPhone 模拟器的说明)，和太浏览到该网站。</span><span class="sxs-lookup"><span data-stu-id="54379-493">Open an **iPhone simulator** (see [Appendix C](#AppendixC) for instructions on how to install and configure an iPhone simulator), and browse to the site too.</span></span> <span data-ttu-id="54379-494">请注意，每个 phone 使用特定的模板。</span><span class="sxs-lookup"><span data-stu-id="54379-494">Notice that each phone is using the specific template.</span></span>

    ![Using-different-views-for-each-mobile-device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    <span data-ttu-id="54379-496">*对于每个移动设备使用不同的视图*</span><span class="sxs-lookup"><span data-stu-id="54379-496">*Using different views for each mobile device*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a><span data-ttu-id="54379-497">练习 4： 使用异步控制器</span><span class="sxs-lookup"><span data-stu-id="54379-497">Exercise 4: Using Asynchronous Controllers</span></span>

<span data-ttu-id="54379-498">Microsoft.NET Framework 4.5 引入了以 C# 和 Visual Basic 中的.NET 编程异步提供新的基础的新语言功能。</span><span class="sxs-lookup"><span data-stu-id="54379-498">Microsoft .NET Framework 4.5 introduces new language features in C# and Visual Basic to provide a new foundation for asynchrony in .NET programming.</span></span> <span data-ttu-id="54379-499">此新 foundation 能使异步编程，类似于-也大约像简单-同步编程。</span><span class="sxs-lookup"><span data-stu-id="54379-499">This new foundation makes asynchronous programming similar to - and about as straightforward as - synchronous programming.</span></span> <span data-ttu-id="54379-500">你现可通过使用 ASP.NET MVC 4 中编写的异步操作方法**AsyncController**类。</span><span class="sxs-lookup"><span data-stu-id="54379-500">You are now able to write asynchronous action methods in ASP.NET MVC 4 by using the **AsyncController** class.</span></span> <span data-ttu-id="54379-501">可以使用的长时间运行的异步操作方法，非 CPU 绑定的请求。</span><span class="sxs-lookup"><span data-stu-id="54379-501">You can use asynchronous action methods for long-running, non-CPU bound requests.</span></span> <span data-ttu-id="54379-502">这样可避免阻止 Web 服务器在处理请求时执行工作。</span><span class="sxs-lookup"><span data-stu-id="54379-502">This avoids blocking the Web server from performing work while the request is being processed.</span></span> <span data-ttu-id="54379-503">AsyncController 类通常用于长时间运行的 Web 服务调用。</span><span class="sxs-lookup"><span data-stu-id="54379-503">The AsyncController class is typically used for long-running Web service calls.</span></span>

<span data-ttu-id="54379-504">本练习中说明 ASP.NET MVC 4 中的异步操作的基础的知识。</span><span class="sxs-lookup"><span data-stu-id="54379-504">This exercise explains the basics of asynchronous operation in ASP.NET MVC 4.</span></span> <span data-ttu-id="54379-505">如果你希望更深入的了解，你可以查看以下文章： [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="54379-505">If you want a deeper dive, you can check out the following article: [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span></span>

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a><span data-ttu-id="54379-506">任务 1-实现异步控制器</span><span class="sxs-lookup"><span data-stu-id="54379-506">Task 1 - Implementing an Asynchronous Controller</span></span>

1. <span data-ttu-id="54379-507">打开**开始**解决方案位于**源/Ex4-Async/开始/**文件夹。</span><span class="sxs-lookup"><span data-stu-id="54379-507">Open the **Begin** solution located at **Source/Ex4-Async/Begin/** folder.</span></span> <span data-ttu-id="54379-508">否则，可能会继续使用**结束**解决方案获取通过完成上一练习。</span><span class="sxs-lookup"><span data-stu-id="54379-508">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="54379-509">如果你打开提供**开始**解决方案，你将需要下载一些缺少的 NuGet 程序包才能继续。</span><span class="sxs-lookup"><span data-stu-id="54379-509">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="54379-510">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="54379-510">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="54379-511">在**管理 NuGet 包**对话框中，单击**还原**以便下载缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="54379-511">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="54379-512">最后，通过单击生成解决方案**生成** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="54379-512">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="54379-513">使用 NuGet 的优点之一是，你无需提供你的项目中的所有库减小项目大小。</span><span class="sxs-lookup"><span data-stu-id="54379-513">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="54379-514">使用 NuGet 增强工具，请通过指定的包版本在 Packages.config 文件中，你将能够下载首次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="54379-514">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="54379-515">这是你将需要从本实验打开现有的解决方案后运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="54379-515">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="54379-516">打开**HomeController.cs**类**控制器**文件夹。</span><span class="sxs-lookup"><span data-stu-id="54379-516">Open the **HomeController.cs** class from the **Controllers** folder.</span></span>
3. <span data-ttu-id="54379-517">添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="54379-517">Add the following using statement.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
~~~
4. <span data-ttu-id="54379-518">更新**HomeController**类继承自**AsyncController**。</span><span class="sxs-lookup"><span data-stu-id="54379-518">Update the **HomeController** class to inherit from **AsyncController**.</span></span> <span data-ttu-id="54379-519">从 AsyncController 派生的控制器使 ASP.NET 能够处理异步请求和它们仍可以服务的同步操作方法。</span><span class="sxs-lookup"><span data-stu-id="54379-519">Controllers that derive from AsyncController enable ASP.NET to process asynchronous requests, and they can still service synchronous action methods.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
~~~
5. <span data-ttu-id="54379-520">添加**异步**关键字**索引**方法并使其返回类型**任务&lt;ActionResult&gt;**。</span><span class="sxs-lookup"><span data-stu-id="54379-520">Add the **async** keyword to the **Index** method and make it return the type **Task&lt;ActionResult&gt;**.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

> [!NOTE]
> The **async** keyword is one of the new keywords the .NET Framework 4.5 provides; it tells the compiler that this method contains asynchronous code. A **Task** object represents an asynchronous operation that may complete at some point in the future.
~~~
6. <span data-ttu-id="54379-521">替换**客户端。GetAsync()**调用具有完整的异步版本使用 await 关键字，如下所示。</span><span class="sxs-lookup"><span data-stu-id="54379-521">Replace the **client.GetAsync()** call with the full async version using await keyword as shown below.</span></span>

    <span data-ttu-id="54379-522">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - GetAsync*)</span><span class="sxs-lookup"><span data-stu-id="54379-522">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - GetAsync*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

> [!NOTE]
> In the previous version, you were using the **Result** property from the **Task** object to block the thread until the result is returned (sync version).
> 
> Adding the **await** keyword tells the compiler to asynchronously wait for the task returned from the method call. This means that the rest of the code will be executed as a callback only after the awaited method completes. Another thing to notice is that you do not need to change your try-catch block in order to make this work: the exceptions that happen in background or in foreground will still be caught without any extra work using a handler provided by the framework.
~~~
7. <span data-ttu-id="54379-523">更改代码以继续进行的异步实现通过将替换为新的代码行，如下所示</span><span class="sxs-lookup"><span data-stu-id="54379-523">Change the code to continue with the asynchronous implementation by replacing the lines with the new code as shown below</span></span>

    <span data-ttu-id="54379-524">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - ReadAsStringAsync*)</span><span class="sxs-lookup"><span data-stu-id="54379-524">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - ReadAsStringAsync*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
~~~
8. <span data-ttu-id="54379-525">运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-525">Run the application.</span></span> <span data-ttu-id="54379-526">你将注意到没有较大的变化，但你的代码不会阻止线程池中进行的服务器资源的更好的利用率并提高性能的线程。</span><span class="sxs-lookup"><span data-stu-id="54379-526">You will notice no major changes, but your code will not block a thread from the thread pool making a better usage of the server resources and improving performance.</span></span>

    > [!NOTE]
    > <span data-ttu-id="54379-527">你可以了解有关在实验室中新的异步编程功能&quot;**使用 C# 和 Visual Basic.NET 4.5 中的异步编程**&quot;包含在 Visual Studio 培训工具包。</span><span class="sxs-lookup"><span data-stu-id="54379-527">You can learn more about the new asynchronous programming features in the lab &quot;**Asynchronous Programming in .NET 4.5 with C# and Visual Basic**&quot; included in the Visual Studio Training Kit.</span></span>

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a><span data-ttu-id="54379-528">任务 2-处理的取消标记的超时时间</span><span class="sxs-lookup"><span data-stu-id="54379-528">Task 2 - Handling Time-Outs with Cancellation Tokens</span></span>

<span data-ttu-id="54379-529">返回 Task 实例的异步操作方法还可以支持超时。</span><span class="sxs-lookup"><span data-stu-id="54379-529">Asynchronous action methods that return Task instances can also support time-outs.</span></span> <span data-ttu-id="54379-530">在此任务中，你将更新索引方法代码，来处理超时方案中使用取消标记。</span><span class="sxs-lookup"><span data-stu-id="54379-530">In this task, you will update the Index method code to handle a time-out scenario using a cancellation token.</span></span>

1. <span data-ttu-id="54379-531">返回到 Visual Studio，然后按**SHIFT + F5**来停止调试。</span><span class="sxs-lookup"><span data-stu-id="54379-531">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>
2. <span data-ttu-id="54379-532">添加以下 using 语句到**HomeController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="54379-532">Add the following using statement to the **HomeController.cs** file.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
~~~
3. <span data-ttu-id="54379-533">更新索引操作，即可接收**CancellationToken**自变量。</span><span class="sxs-lookup"><span data-stu-id="54379-533">Update the Index action to receive a **CancellationToken** argument.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
~~~
4. <span data-ttu-id="54379-534">更新**GetAsync**调用即可传递的取消标记。</span><span class="sxs-lookup"><span data-stu-id="54379-534">Update the **GetAsync** call to pass the cancellation token.</span></span>

    <span data-ttu-id="54379-535">(代码段- *CancellationToken 与 ASP.NET MVC 4 实验室-Ex04-SendAsync*)</span><span class="sxs-lookup"><span data-stu-id="54379-535">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - SendAsync with CancellationToken*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
~~~
5. <span data-ttu-id="54379-536">修饰*索引*方法替换**AsyncTimeout**属性设置为 500 毫秒和**HandleError**属性配置为以处理**TaskCanceledException**通过重定向到**TimedOut**视图。</span><span class="sxs-lookup"><span data-stu-id="54379-536">Decorate the *Index* method with an **AsyncTimeout** attribute set to 500 milliseconds and a **HandleError** attribute configured to handle **TaskCanceledException** by redirecting to a **TimedOut** view.</span></span>

    <span data-ttu-id="54379-537">(代码段- *ASP.NET MVC 4 实验室-Ex04-特性*)</span><span class="sxs-lookup"><span data-stu-id="54379-537">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - Attributes*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
~~~
6. <span data-ttu-id="54379-538">打开**PhotoController**类和更新**库**方法延迟执行 1000年毫秒 （1 秒），以模拟长时间运行的任务。</span><span class="sxs-lookup"><span data-stu-id="54379-538">Open the **PhotoController** class and update the **Gallery** method to delay the execution 1000 miliseconds (1 second) to simulate a long running task.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
~~~
7. <span data-ttu-id="54379-539">打开**Web.config**文件，并通过添加下面的元素启用自定义错误。</span><span class="sxs-lookup"><span data-stu-id="54379-539">Open the **Web.config** file and enable custom errors by adding the following element.</span></span>


~~~
[!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
~~~
8. <span data-ttu-id="54379-540">创建新视图在**views/shared**名为**TimedOut**并使用默认的布局。</span><span class="sxs-lookup"><span data-stu-id="54379-540">Create a new view in **Views\Shared** named **TimedOut** and use the default layout.</span></span> <span data-ttu-id="54379-541">在解决方案资源管理器，右键单击**views/shared**文件夹，然后选择**添加 |视图**。</span><span class="sxs-lookup"><span data-stu-id="54379-541">In the Solution Explorer, right-click the **Views\Shared** folder and select **Add | View**.</span></span>

    <span data-ttu-id="54379-542">![对于每个移动设备使用不同的视图](whats-new-in-aspnet-mvc-4/_static/image36.png "为每个移动设备使用不同的视图")</span><span class="sxs-lookup"><span data-stu-id="54379-542">![Using different views for each mobile device](whats-new-in-aspnet-mvc-4/_static/image36.png "Using different views for each mobile device")</span></span>

    <span data-ttu-id="54379-543">*对于每个移动设备使用不同的视图*</span><span class="sxs-lookup"><span data-stu-id="54379-543">*Using different views for each mobile device*</span></span>
9. <span data-ttu-id="54379-544">更新**TimedOut**查看内容，如下所示。</span><span class="sxs-lookup"><span data-stu-id="54379-544">Update the **TimedOut** view content as shown below.</span></span>


~~~
[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
~~~
10. <span data-ttu-id="54379-545">运行应用程序并导航到根 URL。</span><span class="sxs-lookup"><span data-stu-id="54379-545">Run the application and navigate to the root URL.</span></span> <span data-ttu-id="54379-546">如已添加**Thread.Sleep**为 1000年毫秒，则会超时错误，生成的**AsyncTimeout**属性，并通过捕获**HandleError**属性。</span><span class="sxs-lookup"><span data-stu-id="54379-546">As you have added a **Thread.Sleep** of 1000 milliseconds, you will get a time-out error, generated by the **AsyncTimeout** attribute and catch by the **HandleError** attribute.</span></span>

    <span data-ttu-id="54379-547">![处理的超时异常](whats-new-in-aspnet-mvc-4/_static/image37.png "超时异常处理")</span><span class="sxs-lookup"><span data-stu-id="54379-547">![Time-out exception handled](whats-new-in-aspnet-mvc-4/_static/image37.png "Time-out exception handled")</span></span>

    <span data-ttu-id="54379-548">*超时异常处理*</span><span class="sxs-lookup"><span data-stu-id="54379-548">*Time-out exception handled*</span></span>

> [!NOTE]
> <span data-ttu-id="54379-549">此外，你可以部署此应用程序对 Windows Azure 网站以下[附录 d： 发布 ASP.NET MVC 4 应用程序使用 Web Deploy](#AppendixD)。</span><span class="sxs-lookup"><span data-stu-id="54379-549">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixD).</span></span>


<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="54379-550">总结</span><span class="sxs-lookup"><span data-stu-id="54379-550">Summary</span></span>

<span data-ttu-id="54379-551">在此动手实验，您已观察到的一些新功能驻留在 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="54379-551">In this hands-on-lab, you've observed some of the new features resident in ASP.NET MVC 4.</span></span> <span data-ttu-id="54379-552">讨论了以下概念：</span><span class="sxs-lookup"><span data-stu-id="54379-552">The following concepts have been discussed:</span></span>

- <span data-ttu-id="54379-553">充分利用 ASP.NET MVC 项目模板-包括新的移动应用程序项目模板的增强功能</span><span class="sxs-lookup"><span data-stu-id="54379-553">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="54379-554">使用 HTML5 视区属性和 CSS 媒体查询来改善在移动设备上的显示</span><span class="sxs-lookup"><span data-stu-id="54379-554">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="54379-555">使用 jQuery Mobile，来渐进式增强功能并构建触控优化 web UI</span><span class="sxs-lookup"><span data-stu-id="54379-555">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="54379-556">创建移动特定的视图</span><span class="sxs-lookup"><span data-stu-id="54379-556">Create mobile-specific views</span></span>
- <span data-ttu-id="54379-557">视图切换器组件用于应用程序中的移动和桌面视图之间切换</span><span class="sxs-lookup"><span data-stu-id="54379-557">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="54379-558">创建使用任务支持异步控制器</span><span class="sxs-lookup"><span data-stu-id="54379-558">Create asynchronous controllers using task support</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="54379-559">附录 a： 使用代码片段</span><span class="sxs-lookup"><span data-stu-id="54379-559">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="54379-560">和代码片段，必须将你能够轻松获得所需的所有代码所示。</span><span class="sxs-lookup"><span data-stu-id="54379-560">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="54379-561">实验室文档将告诉您完全时你可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="54379-561">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="54379-562">![使用 Visual Studio 代码段将代码插入到你的项目](whats-new-in-aspnet-mvc-4/_static/image38.png "使用 Visual Studio 代码片段，可将代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="54379-562">![Using Visual Studio code snippets to insert code into your project](whats-new-in-aspnet-mvc-4/_static/image38.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="54379-563">*使用 Visual Studio 代码段将代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="54379-563">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="54379-564">***若要添加代码片段使用键盘 (仅限 C#)***</span><span class="sxs-lookup"><span data-stu-id="54379-564">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="54379-565">将光标置于想要插入代码。</span><span class="sxs-lookup"><span data-stu-id="54379-565">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="54379-566">开始键入代码段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="54379-566">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="54379-567">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="54379-567">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="54379-568">选择正确的代码段 （或继续键入直到选中整个代码段的名称）。</span><span class="sxs-lookup"><span data-stu-id="54379-568">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="54379-569">按 Tab 键两次以光标位置处插入代码段。</span><span class="sxs-lookup"><span data-stu-id="54379-569">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="54379-570">![开始键入代码段名称](whats-new-in-aspnet-mvc-4/_static/image39.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="54379-570">![Start typing the snippet name](whats-new-in-aspnet-mvc-4/_static/image39.png "Start typing the snippet name")</span></span>

<span data-ttu-id="54379-571">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="54379-571">*Start typing the snippet name*</span></span>

<span data-ttu-id="54379-572">![按 Tab 以选择突出显示代码段](whats-new-in-aspnet-mvc-4/_static/image40.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="54379-572">![Press Tab to select the highlighted snippet](whats-new-in-aspnet-mvc-4/_static/image40.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="54379-573">*按 Tab 以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="54379-573">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="54379-574">![再次按 Tab 和代码段将会扩展](whats-new-in-aspnet-mvc-4/_static/image41.png "再次按 Tab 和代码段将会扩展")</span><span class="sxs-lookup"><span data-stu-id="54379-574">![Press Tab again and the snippet will expand](whats-new-in-aspnet-mvc-4/_static/image41.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="54379-575">*再次按 Tab 和代码段将会扩展*</span><span class="sxs-lookup"><span data-stu-id="54379-575">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="54379-576">***若要添加代码片段使用鼠标 （C#、 Visual Basic 和 XML）***</span><span class="sxs-lookup"><span data-stu-id="54379-576">***To add a code snippet using the mouse (C#, Visual Basic and XML)***</span></span>

1. <span data-ttu-id="54379-577">右键单击你想要插入代码段。</span><span class="sxs-lookup"><span data-stu-id="54379-577">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="54379-578">选择**插入代码段**跟**我的代码段**。</span><span class="sxs-lookup"><span data-stu-id="54379-578">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="54379-579">选择相关的代码段从列表中，通过单击它。</span><span class="sxs-lookup"><span data-stu-id="54379-579">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="54379-580">![右键单击你想要插入代码段，并选择插入代码段](whats-new-in-aspnet-mvc-4/_static/image42.png "右键单击你想要插入代码段，并选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="54379-580">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-aspnet-mvc-4/_static/image42.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="54379-581">*右键单击你想要插入代码段，并选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="54379-581">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="54379-582">![通过单击它选取列表中中的相关代码片段](whats-new-in-aspnet-mvc-4/_static/image43.png "选取相关的代码段从列表中，通过单击它")</span><span class="sxs-lookup"><span data-stu-id="54379-582">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-aspnet-mvc-4/_static/image43.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="54379-583">*通过单击它选取从列表中，相关代码段*</span><span class="sxs-lookup"><span data-stu-id="54379-583">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="54379-584">附录 b： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="54379-584">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="54379-585">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;版本使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="54379-585">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="54379-586">以下说明将指导你完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="54379-586">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="54379-587">转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="54379-587">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="54379-588">或者，如果你已安装 Web 平台安装程序，你可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 的 Windows Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="54379-588">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="54379-589">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="54379-589">Click on **Install Now**.</span></span> <span data-ttu-id="54379-590">如果你没有**Web 平台安装程序**将重定向以下载并请先安装它。</span><span class="sxs-lookup"><span data-stu-id="54379-590">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="54379-591">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="54379-591">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="54379-592">![安装 Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="54379-592">![Install Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="54379-593">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="54379-593">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="54379-594">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="54379-594">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](whats-new-in-aspnet-mvc-4/_static/image45.png)

    <span data-ttu-id="54379-596">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="54379-596">*Accepting the license terms*</span></span>
5. <span data-ttu-id="54379-597">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="54379-597">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](whats-new-in-aspnet-mvc-4/_static/image46.png)

    <span data-ttu-id="54379-599">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="54379-599">*Installation progress*</span></span>
6. <span data-ttu-id="54379-600">当安装完成后时，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="54379-600">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](whats-new-in-aspnet-mvc-4/_static/image47.png)

    <span data-ttu-id="54379-602">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="54379-602">*Installation completed*</span></span>
7. <span data-ttu-id="54379-603">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="54379-603">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="54379-604">若要打开 Visual Studio Express for Web，请转到**启动**屏幕并开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="54379-604">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web 磁贴的 VS Express](whats-new-in-aspnet-mvc-4/_static/image48.png)

    <span data-ttu-id="54379-606">*Web 磁贴的 VS Express*</span><span class="sxs-lookup"><span data-stu-id="54379-606">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a><span data-ttu-id="54379-607">附录 c： 安装 WebMatrix 2 和 iPhone 模拟器</span><span class="sxs-lookup"><span data-stu-id="54379-607">Appendix C: Installing WebMatrix 2 and iPhone Simulator</span></span>

<span data-ttu-id="54379-608">若要模拟的 iPhone 设备中运行你的站点可以使用 WebMatrix 扩展&quot;适用于 iPhone 的电力移动模拟器&quot;。</span><span class="sxs-lookup"><span data-stu-id="54379-608">To run your site in a simulated iPhone device you can use the WebMatrix extension &quot;Electric Mobile Simulator for the iPhone&quot;.</span></span> <span data-ttu-id="54379-609">此外，你可以配置要从 Visual Studio 2012 中运行模拟器的相同扩展。</span><span class="sxs-lookup"><span data-stu-id="54379-609">Also, you can configure the same extension to run the simulator from Visual Studio 2012.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a><span data-ttu-id="54379-610">任务 1-安装 WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="54379-610">Task 1 - Installing WebMatrix 2</span></span>

1. <span data-ttu-id="54379-611">转到[ [ https://go.microsoft.com/?linkid=9809776 ](https://go.microsoft.com/?linkid=9809776) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="54379-611">Go to [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="54379-612">或者，如果你已安装 Web 平台安装程序，你可以打开它，并搜索产品&quot; <em>WebMatrix 2</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="54379-612">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>WebMatrix 2</em>&quot;.</span></span>
2. <span data-ttu-id="54379-613">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="54379-613">Click on **Install Now**.</span></span> <span data-ttu-id="54379-614">如果你没有**Web 平台安装程序**将重定向以下载并请先安装它。</span><span class="sxs-lookup"><span data-stu-id="54379-614">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="54379-615">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="54379-615">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="54379-616">![安装 WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "安装 WebMatrix 2")</span><span class="sxs-lookup"><span data-stu-id="54379-616">![Install WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "Install WebMatrix 2")</span></span>

    <span data-ttu-id="54379-617">*安装 WebMatrix 2*</span><span class="sxs-lookup"><span data-stu-id="54379-617">*Install WebMatrix 2*</span></span>
4. <span data-ttu-id="54379-618">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="54379-618">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    <span data-ttu-id="54379-619">![接受许可条款](whats-new-in-aspnet-mvc-4/_static/image50.png "接受许可条款")</span><span class="sxs-lookup"><span data-stu-id="54379-619">![Accepting the license terms](whats-new-in-aspnet-mvc-4/_static/image50.png "Accepting the license terms")</span></span>

    <span data-ttu-id="54379-620">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="54379-620">*Accepting the license terms*</span></span>
5. <span data-ttu-id="54379-621">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="54379-621">Wait until the downloading and installation process completes.</span></span>

    <span data-ttu-id="54379-622">![安装进度](whats-new-in-aspnet-mvc-4/_static/image51.png "安装进度")</span><span class="sxs-lookup"><span data-stu-id="54379-622">![Installation progress](whats-new-in-aspnet-mvc-4/_static/image51.png "Installation progress")</span></span>

    <span data-ttu-id="54379-623">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="54379-623">*Installation progress*</span></span>
6. <span data-ttu-id="54379-624">当安装完成后时，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="54379-624">When the installation completes, click **Finish**.</span></span>

    <span data-ttu-id="54379-625">![安装已完成](whats-new-in-aspnet-mvc-4/_static/image52.png "安装已完成")</span><span class="sxs-lookup"><span data-stu-id="54379-625">![Installation completed](whats-new-in-aspnet-mvc-4/_static/image52.png "Installation completed")</span></span>

    <span data-ttu-id="54379-626">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="54379-626">*Installation completed*</span></span>
7. <span data-ttu-id="54379-627">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="54379-627">Click **Exit** to close Web Platform Installer.</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a><span data-ttu-id="54379-628">任务 2-安装 iPhone 模拟器扩展</span><span class="sxs-lookup"><span data-stu-id="54379-628">Task 2 - Installing the iPhone Simulator Extension</span></span>

1. <span data-ttu-id="54379-629">运行**WebMatrix**和打开任何现有的网站或创建一个新。</span><span class="sxs-lookup"><span data-stu-id="54379-629">Run **WebMatrix** and open any existing Web site or create a new one.</span></span>
2. <span data-ttu-id="54379-630">单击**运行**按钮从**主页**功能区，然后选择**添加新**。</span><span class="sxs-lookup"><span data-stu-id="54379-630">Click the **Run** button from the **Home** ribbon and select **Add new**.</span></span>

    <span data-ttu-id="54379-631">![添加新的 WebMatrix 扩展](whats-new-in-aspnet-mvc-4/_static/image53.png "添加新的 WebMatrix 扩展")</span><span class="sxs-lookup"><span data-stu-id="54379-631">![Adding new WebMatrix extension](whats-new-in-aspnet-mvc-4/_static/image53.png "Adding new WebMatrix extension")</span></span>

    <span data-ttu-id="54379-632">*添加新的 WebMatrix 扩展*</span><span class="sxs-lookup"><span data-stu-id="54379-632">*Adding new WebMatrix extension*</span></span>
3. <span data-ttu-id="54379-633">选择**iPhone 模拟器**单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="54379-633">Select **iPhone Simulator** and click **Install**.</span></span>

    <span data-ttu-id="54379-634">![浏览 WebMatrix 扩展](whats-new-in-aspnet-mvc-4/_static/image54.png "浏览 WebMatrix 扩展")</span><span class="sxs-lookup"><span data-stu-id="54379-634">![Browsing WebMatrix extensions](whats-new-in-aspnet-mvc-4/_static/image54.png "Browsing WebMatrix extensions")</span></span>

    <span data-ttu-id="54379-635">*浏览 WebMatrix 扩展*</span><span class="sxs-lookup"><span data-stu-id="54379-635">*Browsing WebMatrix extensions*</span></span>
4. <span data-ttu-id="54379-636">在包的详细信息，单击**安装**继续扩展安装。</span><span class="sxs-lookup"><span data-stu-id="54379-636">In the package details, click **Install** to continue with the extension installation.</span></span>

    <span data-ttu-id="54379-637">![iPhone 模拟器扩展](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone 模拟器扩展")</span><span class="sxs-lookup"><span data-stu-id="54379-637">![iPhone Simulator extension](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone Simulator extension")</span></span>

    <span data-ttu-id="54379-638">*iPhone 模拟器扩展*</span><span class="sxs-lookup"><span data-stu-id="54379-638">*iPhone Simulator extension*</span></span>
5. <span data-ttu-id="54379-639">阅读并接受最终用户许可协议的扩展。</span><span class="sxs-lookup"><span data-stu-id="54379-639">Read and accept the extension EULA.</span></span>

    <span data-ttu-id="54379-640">![WebMatrix 扩展 EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 扩展 EULA")</span><span class="sxs-lookup"><span data-stu-id="54379-640">![WebMatrix extension EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix extension EULA")</span></span>

    <span data-ttu-id="54379-641">*WebMatrix 扩展 EULA*</span><span class="sxs-lookup"><span data-stu-id="54379-641">*WebMatrix extension EULA*</span></span>
6. <span data-ttu-id="54379-642">现在，可以从 WebMatrix 中运行您的网站使用 iPhone 模拟器选项。</span><span class="sxs-lookup"><span data-stu-id="54379-642">Now, you can run your Web site from WebMatrix using the iPhone Simulator option.</span></span>

    <span data-ttu-id="54379-643">![使用 iPhone 运行](whats-new-in-aspnet-mvc-4/_static/image57.png "使用 iPhone 运行")</span><span class="sxs-lookup"><span data-stu-id="54379-643">![Run using iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "Run using iPhone")</span></span>

    <span data-ttu-id="54379-644">*使用 iPhone 运行*</span><span class="sxs-lookup"><span data-stu-id="54379-644">*Run using iPhone*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a><span data-ttu-id="54379-645">任务 3-配置 Visual Studio 2012 运行 iPhone 模拟器</span><span class="sxs-lookup"><span data-stu-id="54379-645">Task 3 - Configuring Visual Studio 2012 to run iPhone Simulator</span></span>

1. <span data-ttu-id="54379-646">打开**Visual Studio 2012**和打开的任何网站或创建新项目。</span><span class="sxs-lookup"><span data-stu-id="54379-646">Open **Visual Studio 2012** and open any Web site or create a new project.</span></span>
2. <span data-ttu-id="54379-647">单击运行按钮从的向下箭头，然后选择**浏览与**。</span><span class="sxs-lookup"><span data-stu-id="54379-647">Click the down arrow from the Run button and select **Browse with**.</span></span>

    <span data-ttu-id="54379-648">![浏览与](whats-new-in-aspnet-mvc-4/_static/image58.png "浏览与")</span><span class="sxs-lookup"><span data-stu-id="54379-648">![Browse with](whats-new-in-aspnet-mvc-4/_static/image58.png "Browse with")</span></span>

    <span data-ttu-id="54379-649">*浏览与*</span><span class="sxs-lookup"><span data-stu-id="54379-649">*Browse with*</span></span>
3. <span data-ttu-id="54379-650">在&quot;浏览&quot;对话框中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="54379-650">In the &quot;Browse With&quot; dialog, click **Add**.</span></span>
4. <span data-ttu-id="54379-651">在&quot;添加程序&quot;对话框中，使用以下值：</span><span class="sxs-lookup"><span data-stu-id="54379-651">In the &quot;Add Program&quot; dialog, use the following values:</span></span>

   - <span data-ttu-id="54379-652"><strong>程序</strong>: C:\Users\*{CurrentUser}<em>\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe * （相应地更新的路径）</em></span><span class="sxs-lookup"><span data-stu-id="54379-652"><strong>Program</strong>: C:\Users\*{CurrentUser}<em>\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(update the path accordingly)</em></span></span>
   - <span data-ttu-id="54379-653">**自变量**: &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="54379-653">**Arguments**: &quot;1&quot;</span></span>
   - <span data-ttu-id="54379-654">**友好名称**: iPhone 模拟器</span><span class="sxs-lookup"><span data-stu-id="54379-654">**Friendly name**: iPhone Simulator</span></span>

     <span data-ttu-id="54379-655">![添加程序](whats-new-in-aspnet-mvc-4/_static/image59.png "添加程序")</span><span class="sxs-lookup"><span data-stu-id="54379-655">![Add program](whats-new-in-aspnet-mvc-4/_static/image59.png "Add program")</span></span>

     <span data-ttu-id="54379-656">*添加程序与浏览*</span><span class="sxs-lookup"><span data-stu-id="54379-656">*Add program to browse with*</span></span>
5. <span data-ttu-id="54379-657">单击**确定**并关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="54379-657">Click **OK** and close the dialogs.</span></span>
6. <span data-ttu-id="54379-658">现在，你就能够从 Visual Studio 2012 在 iPhone 模拟器中运行 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="54379-658">Now you are able to run your Web applications in the iPhone simulator from Visual Studio 2012.</span></span>

    <span data-ttu-id="54379-659">![浏览方式 iPhone 模拟器](whats-new-in-aspnet-mvc-4/_static/image60.png "浏览方式 iPhone 模拟器")</span><span class="sxs-lookup"><span data-stu-id="54379-659">![Browse with iPhone Simulator](whats-new-in-aspnet-mvc-4/_static/image60.png "Browse with iPhone Simulator")</span></span>

    <span data-ttu-id="54379-660">*浏览方式 iPhone 模拟器*</span><span class="sxs-lookup"><span data-stu-id="54379-660">*Browse with iPhone Simulator*</span></span>

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="54379-661">附录 d： 发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="54379-661">Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="54379-662">本附录将演示如何从 Windows Azure 管理门户创建新的网站和发布应用程序获取按照本实验中，利用 Windows Azure 提供的 Web 部署发布功能。</span><span class="sxs-lookup"><span data-stu-id="54379-662">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="54379-663">任务 1-创建新的 Web 站点从 Windows Azure 门户</span><span class="sxs-lookup"><span data-stu-id="54379-663">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="54379-664">转到[Windows Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="54379-664">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="54379-665">使用 Windows Azure 可以免费承载 10 个 ASP.NET 网站，然后随着流量增长而扩展。</span><span class="sxs-lookup"><span data-stu-id="54379-665">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="54379-666">你可以注册[此处](http://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="54379-666">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="54379-667">![登录到 Windows Azure 门户](whats-new-in-aspnet-mvc-4/_static/image61.png "登录到 Windows Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="54379-667">![Log on to Windows Azure portal](whats-new-in-aspnet-mvc-4/_static/image61.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="54379-668">*登录到 Windows Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="54379-668">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="54379-669">单击**新建**命令栏上。</span><span class="sxs-lookup"><span data-stu-id="54379-669">Click **New** on the command bar.</span></span>

    <span data-ttu-id="54379-670">![创建新网站](whats-new-in-aspnet-mvc-4/_static/image62.png "创建新网站")</span><span class="sxs-lookup"><span data-stu-id="54379-670">![Creating a new Web Site](whats-new-in-aspnet-mvc-4/_static/image62.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="54379-671">*创建新网站*</span><span class="sxs-lookup"><span data-stu-id="54379-671">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="54379-672">单击**计算** | **网站**。</span><span class="sxs-lookup"><span data-stu-id="54379-672">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="54379-673">然后选择**快速创建**选项。</span><span class="sxs-lookup"><span data-stu-id="54379-673">Then select **Quick Create** option.</span></span> <span data-ttu-id="54379-674">为新网站提供可用的 URL，然后单击**创建网站**。</span><span class="sxs-lookup"><span data-stu-id="54379-674">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="54379-675">Windows Azure 网站是在云中，你可以控制和管理运行的 web 应用程序的宿主。</span><span class="sxs-lookup"><span data-stu-id="54379-675">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="54379-676">快速创建选项，可将已完成的 web 应用程序到 Windows Azure 网站从在门户外部部署。</span><span class="sxs-lookup"><span data-stu-id="54379-676">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="54379-677">它不包括用于设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="54379-677">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="54379-678">![创建新的网站使用快速创建](whats-new-in-aspnet-mvc-4/_static/image63.png "创建新的网站使用快速创建")</span><span class="sxs-lookup"><span data-stu-id="54379-678">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-mvc-4/_static/image63.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="54379-679">*创建新的网站使用快速创建*</span><span class="sxs-lookup"><span data-stu-id="54379-679">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="54379-680">等到新**网站**创建。</span><span class="sxs-lookup"><span data-stu-id="54379-680">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="54379-681">创建网站后单击下的链接**URL**列。</span><span class="sxs-lookup"><span data-stu-id="54379-681">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="54379-682">检查新的 Web 站点工作。</span><span class="sxs-lookup"><span data-stu-id="54379-682">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="54379-683">![浏览到新的 web 站点](whats-new-in-aspnet-mvc-4/_static/image64.png "浏览到新的 web 站点")</span><span class="sxs-lookup"><span data-stu-id="54379-683">![Browsing to the new web site](whats-new-in-aspnet-mvc-4/_static/image64.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="54379-684">*浏览到新的 web 站点*</span><span class="sxs-lookup"><span data-stu-id="54379-684">*Browsing to the new web site*</span></span>

    <span data-ttu-id="54379-685">![运行网站](whats-new-in-aspnet-mvc-4/_static/image65.png "运行的网站")</span><span class="sxs-lookup"><span data-stu-id="54379-685">![Web site running](whats-new-in-aspnet-mvc-4/_static/image65.png "Web site running")</span></span>

    <span data-ttu-id="54379-686">*运行的网站*</span><span class="sxs-lookup"><span data-stu-id="54379-686">*Web site running*</span></span>
6. <span data-ttu-id="54379-687">返回到门户并单击在网站的名称**名称**列以显示的管理页。</span><span class="sxs-lookup"><span data-stu-id="54379-687">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="54379-688">![打开网站管理页](whats-new-in-aspnet-mvc-4/_static/image66.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="54379-688">![Opening the web site management pages](whats-new-in-aspnet-mvc-4/_static/image66.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="54379-689">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="54379-689">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="54379-690">在**仪表板**页上，在**速览**部分中，单击**下载发布配置文件**链接。</span><span class="sxs-lookup"><span data-stu-id="54379-690">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="54379-691">*发布配置文件*包含所有 web 应用程序发布到 Windows Azure 网站中的每个启用的发布方法所需的信息。</span><span class="sxs-lookup"><span data-stu-id="54379-691">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="54379-692">发布配置文件包含的 Url、 用户凭据和连接到并针对每个发布方法启用的终结点进行身份验证所需的数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="54379-692">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="54379-693">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件以自动执行的这些程序，以便配置web 应用程序发布到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="54379-693">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="54379-694">![下载网站发布配置文件](whats-new-in-aspnet-mvc-4/_static/image67.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="54379-694">![Downloading the web site publish profile](whats-new-in-aspnet-mvc-4/_static/image67.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="54379-695">*下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="54379-695">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="54379-696">到一个已知位置下载发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="54379-696">Download the publish profile file to a known location.</span></span> <span data-ttu-id="54379-697">进一步在本练习中您将了解如何使用此文件来发布 Visual Studio 中的 web 应用程序到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="54379-697">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="54379-698">![保存发布配置文件](whats-new-in-aspnet-mvc-4/_static/image68.png "保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="54379-698">![Saving the publish profile file](whats-new-in-aspnet-mvc-4/_static/image68.png "Saving the publish profile")</span></span>

    <span data-ttu-id="54379-699">*保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="54379-699">*Saving the publish profile file*</span></span>

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="54379-700">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="54379-700">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="54379-701">如果你的应用程序将使用 SQL Server 数据库将需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="54379-701">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="54379-702">如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="54379-702">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="54379-703">需要将用于存储应用程序数据库的 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="54379-703">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="54379-704">你可以从你的订阅在 Windows Azure 管理门户中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**。</span><span class="sxs-lookup"><span data-stu-id="54379-704">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="54379-705">如果你没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。</span><span class="sxs-lookup"><span data-stu-id="54379-705">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="54379-706">请记下的**服务器名称和 URL、 管理员登录名和密码**，如你将在接下来的任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="54379-706">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="54379-707">不创建数据库，它将在后面的阶段中创建。</span><span class="sxs-lookup"><span data-stu-id="54379-707">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="54379-708">![SQL 数据库服务器仪表板](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database 服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="54379-708">![SQL Database Server Dashboard](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="54379-709">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="54379-709">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="54379-710">在下一个任务将测试从 Visual Studio 中，数据库连接，因此你需要在的服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。</span><span class="sxs-lookup"><span data-stu-id="54379-710">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="54379-711">若要做到这一点，请单击**配置**，选择的 IP 地址从**当前客户端 IP 地址**并将其粘贴在**起始 IP 地址**和**结束 IP 地址**文本框和单击![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png)按钮。</span><span class="sxs-lookup"><span data-stu-id="54379-711">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) button.</span></span>

    ![添加客户端 IP 地址](whats-new-in-aspnet-mvc-4/_static/image71.png)

    <span data-ttu-id="54379-713">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="54379-713">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="54379-714">一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。</span><span class="sxs-lookup"><span data-stu-id="54379-714">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认做的更改](whats-new-in-aspnet-mvc-4/_static/image72.png)

    <span data-ttu-id="54379-716">*确认做的更改*</span><span class="sxs-lookup"><span data-stu-id="54379-716">*Confirm Changes*</span></span>

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="54379-717">任务 3-发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="54379-717">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="54379-718">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="54379-718">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="54379-719">在**解决方案资源管理器**，右键单击网站项目，然后选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="54379-719">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="54379-720">![发布应用程序](whats-new-in-aspnet-mvc-4/_static/image73.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="54379-720">![Publishing the Application](whats-new-in-aspnet-mvc-4/_static/image73.png "Publishing the Application")</span></span>

    <span data-ttu-id="54379-721">*发布此网站*</span><span class="sxs-lookup"><span data-stu-id="54379-721">*Publishing the web site*</span></span>
2. <span data-ttu-id="54379-722">导入发布配置文件保存在第一个任务。</span><span class="sxs-lookup"><span data-stu-id="54379-722">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="54379-723">![导入发布配置文件](whats-new-in-aspnet-mvc-4/_static/image74.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="54379-723">![Importing the publish profile](whats-new-in-aspnet-mvc-4/_static/image74.png "Importing the publish profile")</span></span>

    <span data-ttu-id="54379-724">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="54379-724">*Importing publish profile*</span></span>
3. <span data-ttu-id="54379-725">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="54379-725">Click **Validate Connection**.</span></span> <span data-ttu-id="54379-726">验证完成后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="54379-726">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="54379-727">请参阅验证连接按钮旁边将显示绿色的复选标记后，验证已完成。</span><span class="sxs-lookup"><span data-stu-id="54379-727">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="54379-728">![正在验证连接](whats-new-in-aspnet-mvc-4/_static/image75.png "验证连接")</span><span class="sxs-lookup"><span data-stu-id="54379-728">![Validating connection](whats-new-in-aspnet-mvc-4/_static/image75.png "Validating connection")</span></span>

    <span data-ttu-id="54379-729">*正在验证连接*</span><span class="sxs-lookup"><span data-stu-id="54379-729">*Validating connection*</span></span>
4. <span data-ttu-id="54379-730">在**设置**页上，在**数据库**部分中，单击你的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="54379-730">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="54379-731">![Web 部署配置](whats-new-in-aspnet-mvc-4/_static/image76.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="54379-731">![Web deploy configuration](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy configuration")</span></span>

    <span data-ttu-id="54379-732">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="54379-732">*Web deploy configuration*</span></span>
5. <span data-ttu-id="54379-733">配置数据库连接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="54379-733">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="54379-734">在**服务器名称**类型 SQL 数据库服务器 URL 使用*tcp:*前缀。</span><span class="sxs-lookup"><span data-stu-id="54379-734">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="54379-735">在**用户名**键入您的服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="54379-735">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="54379-736">在**密码**键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="54379-736">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="54379-737">键入新的数据库名称，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="54379-737">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="54379-738">![配置目标连接字符串](whats-new-in-aspnet-mvc-4/_static/image77.png "配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="54379-738">![Configuring destination connection string](whats-new-in-aspnet-mvc-4/_static/image77.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="54379-739">*配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="54379-739">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="54379-740">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="54379-740">Then click **OK**.</span></span> <span data-ttu-id="54379-741">当系统提示创建数据库单击**是**。</span><span class="sxs-lookup"><span data-stu-id="54379-741">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="54379-742">![创建数据库](whats-new-in-aspnet-mvc-4/_static/image78.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="54379-742">![Creating the database](whats-new-in-aspnet-mvc-4/_static/image78.png "Creating the database string")</span></span>

    <span data-ttu-id="54379-743">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="54379-743">*Creating the database*</span></span>
7. <span data-ttu-id="54379-744">在默认连接文本框中显示了将用于连接到 Windows Azure 中的 SQL 数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="54379-744">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="54379-745">然后，单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="54379-745">Then click **Next**.</span></span>

    <span data-ttu-id="54379-746">![连接字符串指向 SQL 数据库](whats-new-in-aspnet-mvc-4/_static/image79.png "指向 SQL 数据库的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="54379-746">![Connection string pointing to SQL Database](whats-new-in-aspnet-mvc-4/_static/image79.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="54379-747">*连接字符串指向 SQL 数据库*</span><span class="sxs-lookup"><span data-stu-id="54379-747">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="54379-748">在**预览**页上，单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="54379-748">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="54379-749">![Web 应用程序发布](whats-new-in-aspnet-mvc-4/_static/image80.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="54379-749">![Publishing the web application](whats-new-in-aspnet-mvc-4/_static/image80.png "Publishing the web application")</span></span>

    <span data-ttu-id="54379-750">*发布 web 应用程序*</span><span class="sxs-lookup"><span data-stu-id="54379-750">*Publishing the web application*</span></span>
9. <span data-ttu-id="54379-751">完成发布过程后，默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="54379-751">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="54379-752">![应用程序发布到 Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "应用程序发布到 Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="54379-752">![Application published to Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="54379-753">*应用程序发布到 Windows Azure*</span><span class="sxs-lookup"><span data-stu-id="54379-753">*Application published to Windows Azure*</span></span>
