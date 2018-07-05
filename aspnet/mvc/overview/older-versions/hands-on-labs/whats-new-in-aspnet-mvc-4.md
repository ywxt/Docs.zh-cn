---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: 什么是 ASP.NET MVC 4 中的新增功能 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 是一个框架，用于构建可缩放的基于标准的 web 应用程序使用成熟设计模式和 ASP.NET 的强大功能和...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 8862c4da0d881a6f1084317e08697354c0ae6d48
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374099"
---
# <a name="whats-new-in-aspnet-mvc-4"></a><span data-ttu-id="27d1d-103">什么是 ASP.NET MVC 4 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="27d1d-103">What's New in ASP.NET MVC 4</span></span>

<span data-ttu-id="27d1d-104">通过[Web 训练营团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="27d1d-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="27d1d-105">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="27d1d-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="27d1d-106">ASP.NET MVC 4 是一个框架，用于构建可缩放的基于标准的 web 应用程序使用成熟设计模式和 ASP.NET 和.NET framework 的强大功能。</span><span class="sxs-lookup"><span data-stu-id="27d1d-106">ASP.NET MVC 4 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of the ASP.NET and the .NET framework.</span></span> <span data-ttu-id="27d1d-107">此新，第四个版本的 framework 侧重于提高移动 web 应用程序开发更容易。</span><span class="sxs-lookup"><span data-stu-id="27d1d-107">This new, fourth version of the framework focuses on making mobile web application development easier.</span></span>

<span data-ttu-id="27d1d-108">开始时，创建新的 ASP.NET MVC 4 项目时现在可用于构建一款独立应用专用于移动设备的移动应用程序项目模板。</span><span class="sxs-lookup"><span data-stu-id="27d1d-108">To begin with, when you create a new ASP.NET MVC 4 project there is now a mobile application project template you can use to build a standalone app specifically for mobile devices.</span></span> <span data-ttu-id="27d1d-109">此外，ASP.NET MVC 4 与通过 jQuery.Mobile.MVC NuGet 程序包的 jQuery Mobile 集成。</span><span class="sxs-lookup"><span data-stu-id="27d1d-109">Additionally, ASP.NET MVC 4 integrates with jQuery Mobile through a jQuery.Mobile.MVC NuGet package.</span></span> <span data-ttu-id="27d1d-110">jQuery Mobile 是用于开发 web 应用与所有主流移动设备平台，包括 Windows Phone、 iPhone、 Android 等兼容的基于 HTML5 的框架。</span><span class="sxs-lookup"><span data-stu-id="27d1d-110">jQuery Mobile is an HTML5-based framework for developing web apps that are compatible with all popular mobile device platforms, including Windows Phone, iPhone, Android and so on.</span></span> <span data-ttu-id="27d1d-111">但是，如果你需要专用化，ASP.NET MVC 4 还可以提供适用于不同设备的不同视图，并提供特定于设备的优化。</span><span class="sxs-lookup"><span data-stu-id="27d1d-111">However, if you need specialization, ASP.NET MVC 4 also enables you to serve different views for different devices and provide device-specific optimizations.</span></span>

<span data-ttu-id="27d1d-112">在此动手实验中，将开始使用 ASP.NET MVC 4 &quot;Internet 应用程序&quot;项目模板创建照片库应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-112">In this hands-on lab, you will start with the ASP.NET MVC 4 &quot;Internet Application&quot; project template to create a Photo Gallery application.</span></span> <span data-ttu-id="27d1d-113">您将逐渐增强使用的 jQuery Mobile 和 ASP.NET MVC 4 的新功能，使其与不同的移动设备和桌面 web 浏览器兼容的应用。</span><span class="sxs-lookup"><span data-stu-id="27d1d-113">You will progressively enhance the app using jQuery Mobile and ASP.NET MVC 4's new features to make it compatible with different mobile devices and desktop web browsers.</span></span> <span data-ttu-id="27d1d-114">你还将了解对代码生成和如何 ASP.NET MVC 4 可以更轻松地编写异步操作方法，通过支持任务的新代码方案&lt;ActionResult&gt;返回类型。</span><span class="sxs-lookup"><span data-stu-id="27d1d-114">You will also learn about new code recipes for code generation and how ASP.NET MVC 4 makes it easier for you to write asynchronous action methods by supporting Task&lt;ActionResult&gt; return types.</span></span>

> [!NOTE]
> <span data-ttu-id="27d1d-115">在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-115">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="27d1d-116">特定于此实验室项目位于[What's New in ASP.NET 4.5 中的 Web 窗体](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-116">The project specific to this lab is available at [What's New in Web Forms in ASP.NET 4.5](https://github.com/Microsoft-Web/HOL-ASPNETWebForms).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="27d1d-117">目标</span><span class="sxs-lookup"><span data-stu-id="27d1d-117">Objectives</span></span>

<span data-ttu-id="27d1d-118">在本动手实验，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="27d1d-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="27d1d-119">充分利用 ASP.NET MVC 项目模板包括新的移动应用程序项目模板的增强功能</span><span class="sxs-lookup"><span data-stu-id="27d1d-119">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="27d1d-120">使用 HTML5 视区属性和 CSS 媒体查询来改善在移动设备上显示</span><span class="sxs-lookup"><span data-stu-id="27d1d-120">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="27d1d-121">使用 jQuery Mobile 的渐进式增强功能和用于构建触控优化的 web UI</span><span class="sxs-lookup"><span data-stu-id="27d1d-121">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="27d1d-122">创建移动特定视图</span><span class="sxs-lookup"><span data-stu-id="27d1d-122">Create mobile-specific views</span></span>
- <span data-ttu-id="27d1d-123">使用视图切换器组件来移动和桌面应用程序中的视图之间切换</span><span class="sxs-lookup"><span data-stu-id="27d1d-123">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="27d1d-124">创建使用任务支持异步控制器</span><span class="sxs-lookup"><span data-stu-id="27d1d-124">Create asynchronous controllers using task support</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="27d1d-125">系统必备</span><span class="sxs-lookup"><span data-stu-id="27d1d-125">Prerequisites</span></span>

<span data-ttu-id="27d1d-126">必须具有要完成本实验的以下项：</span><span class="sxs-lookup"><span data-stu-id="27d1d-126">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="27d1d-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 B](#AppendixB)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>
- <span data-ttu-id="27d1d-128">[ASP.NET MVC 4](../../../mvc4.md) （包含在 Microsoft Visual Studio 2012 安装）</span><span class="sxs-lookup"><span data-stu-id="27d1d-128">[ASP.NET MVC 4](../../../mvc4.md) (included in the Microsoft Visual Studio 2012 installation)</span></span>
- <span data-ttu-id="27d1d-129">Windows Phone 仿真程序 (包含在[Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span><span class="sxs-lookup"><span data-stu-id="27d1d-129">Windows Phone Emulator (included in the [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span></span>
- <span data-ttu-id="27d1d-130">可选- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/)与**Electric Plum iPhone 模拟器**扩展 （仅适用于用来与 iPhone 模拟器中浏览 web 应用程序的练习 3)</span><span class="sxs-lookup"><span data-stu-id="27d1d-130">Optional - [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) with **Electric Plum iPhone Simulator** extension (only for Exercise 3 used to browse the web application with an iPhone simulator)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="27d1d-131">安装</span><span class="sxs-lookup"><span data-stu-id="27d1d-131">Setup</span></span>

<span data-ttu-id="27d1d-132">在整个实验文档中，将指示您插入代码块。</span><span class="sxs-lookup"><span data-stu-id="27d1d-132">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="27d1d-133">为方便起见，该代码的大部分以 Visual Studio 代码段，可用于从 Visual Studio 内无需手动添加形式提供。</span><span class="sxs-lookup"><span data-stu-id="27d1d-133">For your convenience, most of that code is provided as Visual Studio Code Snippets, which you can use from within Visual Studio to avoid having to add it manually.</span></span>

<span data-ttu-id="27d1d-134">若要安装的代码片段：</span><span class="sxs-lookup"><span data-stu-id="27d1d-134">To install the code snippets:</span></span>

1. <span data-ttu-id="27d1d-135">打开 Windows 资源管理器窗口并浏览到本实验**Source\Setup**文件夹。</span><span class="sxs-lookup"><span data-stu-id="27d1d-135">Open a Windows Explorer window and browse to the lab's **Source\Setup** folder.</span></span>
2. <span data-ttu-id="27d1d-136">双击**Setup.cmd**此文件夹来安装 Visual Studio 代码段中的文件。</span><span class="sxs-lookup"><span data-stu-id="27d1d-136">Double-click the **Setup.cmd** file in this folder to install the Visual Studio code snippets.</span></span>

<span data-ttu-id="27d1d-137">如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 a： 使用代码片段](#AppendixA)&quot;。</span><span class="sxs-lookup"><span data-stu-id="27d1d-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="27d1d-138">练习</span><span class="sxs-lookup"><span data-stu-id="27d1d-138">Exercises</span></span>

<span data-ttu-id="27d1d-139">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="27d1d-139">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="27d1d-140">新的 ASP.NET MVC 4 项目模板</span><span class="sxs-lookup"><span data-stu-id="27d1d-140">New ASP.NET MVC 4 Project Templates</span></span>](#Exercise1)
2. [<span data-ttu-id="27d1d-141">创建照片库 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="27d1d-141">Creating the Photo Gallery Web Application</span></span>](#Exercise2)
3. [<span data-ttu-id="27d1d-142">添加对移动设备的支持</span><span class="sxs-lookup"><span data-stu-id="27d1d-142">Adding Support for Mobile Devices</span></span>](#Exercise3)
4. [<span data-ttu-id="27d1d-143">使用异步控制器</span><span class="sxs-lookup"><span data-stu-id="27d1d-143">Using Asynchronous Controllers</span></span>](#Exercise4)

> [!NOTE]
> <span data-ttu-id="27d1d-144">每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="27d1d-144">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="27d1d-145">如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="27d1d-145">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="27d1d-146">估计的时间才能完成此实验： **60 分钟**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-146">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a><span data-ttu-id="27d1d-147">练习 1： 新的 ASP.NET MVC 4 项目模板</span><span class="sxs-lookup"><span data-stu-id="27d1d-147">Exercise 1: New ASP.NET MVC 4 Project Templates</span></span>

<span data-ttu-id="27d1d-148">在此练习中，您将了解在 ASP.NET MVC 4 项目模板中的增强功能。</span><span class="sxs-lookup"><span data-stu-id="27d1d-148">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 Project templates.</span></span> <span data-ttu-id="27d1d-149">除了 Internet 应用程序模板，在 MVC 3 中已存在此版本现在包括用于移动应用程序单独的模板。</span><span class="sxs-lookup"><span data-stu-id="27d1d-149">In addition to the Internet Application template, already present in MVC 3, this version now includes a separate template for Mobile applications.</span></span> <span data-ttu-id="27d1d-150">首先，您将查看每个模板的某些相关功能。</span><span class="sxs-lookup"><span data-stu-id="27d1d-150">First, you will look at some relevant features of each of the templates.</span></span> <span data-ttu-id="27d1d-151">然后，将适用于通过使用适当的方法呈现页面在不同平台上正常运行。</span><span class="sxs-lookup"><span data-stu-id="27d1d-151">Then, you will work on rendering your page properly on the different platforms by using the right approach.</span></span>

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a><span data-ttu-id="27d1d-152">任务 1-浏览 Internet 应用程序模板</span><span class="sxs-lookup"><span data-stu-id="27d1d-152">Task 1 - Exploring the Internet Application Template</span></span>

1. <span data-ttu-id="27d1d-153">打开**Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-153">Open **Visual Studio**.</span></span>
2. <span data-ttu-id="27d1d-154">选择**文件 |新 |项目**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="27d1d-154">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="27d1d-155">在中**新的项目**对话框中，选择**Visual C# |Web**在左窗格中的模板树，并选择**ASP.NET MVC 4 Web 应用程序。**</span><span class="sxs-lookup"><span data-stu-id="27d1d-155">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="27d1d-156">将项目命名**PhotoGallery**，选择一个位置 （或保留默认值），单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-156">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27d1d-157">稍后将自定义现在要创建的图片库 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="27d1d-157">You will later customize the PhotoGallery ASP.NET MVC 4 solution you are now creating.</span></span>

    <span data-ttu-id="27d1d-158">![创建新的项目](whats-new-in-aspnet-mvc-4/_static/image1.png "创建新的项目")</span><span class="sxs-lookup"><span data-stu-id="27d1d-158">![Creating a new project](whats-new-in-aspnet-mvc-4/_static/image1.png "Creating a new project")</span></span>

    <span data-ttu-id="27d1d-159">*创建新的项目*</span><span class="sxs-lookup"><span data-stu-id="27d1d-159">*Creating a new project*</span></span>
3. <span data-ttu-id="27d1d-160">在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**项目模板，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-160">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="27d1d-161">请确保已选择 Razor 作为视图引擎。</span><span class="sxs-lookup"><span data-stu-id="27d1d-161">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="27d1d-162">![创建新 ASP.NET MVC 4 Internet 应用程序](whats-new-in-aspnet-mvc-4/_static/image2.png "新建 ASP.NET MVC 4 Internet 应用程序")</span><span class="sxs-lookup"><span data-stu-id="27d1d-162">![Creating a new ASP.NET MVC 4 Internet Application](whats-new-in-aspnet-mvc-4/_static/image2.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="27d1d-163">*创建新 ASP.NET MVC 4 Internet 应用程序*</span><span class="sxs-lookup"><span data-stu-id="27d1d-163">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="27d1d-164">在 ASP.NET MVC 3 中引入了 razor 语法。</span><span class="sxs-lookup"><span data-stu-id="27d1d-164">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="27d1d-165">其目标是字符和击键所需的文件中启用快速、 流畅编码工作流的数量降至最低。</span><span class="sxs-lookup"><span data-stu-id="27d1d-165">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="27d1d-166">Razor 利用现有 C# / VB （或其他） 语言技能，并提供可以实现令人惊叹的 HTML 构造工作流的模板标记语法。</span><span class="sxs-lookup"><span data-stu-id="27d1d-166">Razor leverages existing C# / VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="27d1d-167">按**F5**以运行该解决方案和查看已续订的模板。</span><span class="sxs-lookup"><span data-stu-id="27d1d-167">Press **F5** to run the solution and see the renewed templates.</span></span> <span data-ttu-id="27d1d-168">您可以签出了以下功能：</span><span class="sxs-lookup"><span data-stu-id="27d1d-168">You can check out the following features:</span></span>

    <span data-ttu-id="27d1d-169">**现代样式模板**</span><span class="sxs-lookup"><span data-stu-id="27d1d-169">**Modern-style templates**</span></span>

    <span data-ttu-id="27d1d-170">模板已被续订，提供更多的新式样式。</span><span class="sxs-lookup"><span data-stu-id="27d1d-170">The templates have been renewed, providing more modern-looking styles.</span></span>

    <span data-ttu-id="27d1d-171">![ASP.NET MVC 4 restyled 模板](whats-new-in-aspnet-mvc-4/_static/image3.png "restyled 模板的 MVC 4")</span><span class="sxs-lookup"><span data-stu-id="27d1d-171">![ASP.NET MVC 4 restyled templates](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 restyled templates")</span></span>

    <span data-ttu-id="27d1d-172">*ASP.NET MVC 4 restyled 模板*</span><span class="sxs-lookup"><span data-stu-id="27d1d-172">*ASP.NET MVC 4 restyled templates*</span></span>

    <span data-ttu-id="27d1d-173">![新联系人页](whats-new-in-aspnet-mvc-4/_static/image4.png "新联系人页")</span><span class="sxs-lookup"><span data-stu-id="27d1d-173">![New Contact page](whats-new-in-aspnet-mvc-4/_static/image4.png "New Contact page")</span></span>

    <span data-ttu-id="27d1d-174">*新联系人页*</span><span class="sxs-lookup"><span data-stu-id="27d1d-174">*New Contact page*</span></span>

    <span data-ttu-id="27d1d-175">**自适应呈现**</span><span class="sxs-lookup"><span data-stu-id="27d1d-175">**Adaptive Rendering**</span></span>

    <span data-ttu-id="27d1d-176">签出调整浏览器窗口，请注意，页面布局如何动态调整为新的窗口大小。</span><span class="sxs-lookup"><span data-stu-id="27d1d-176">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="27d1d-177">这些模板使用自适应呈现技术在没有任何自定义项的桌面和移动平台中正确呈现。</span><span class="sxs-lookup"><span data-stu-id="27d1d-177">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

    <span data-ttu-id="27d1d-178">![在不同的浏览器大小中的 ASP.NET MVC 4 项目模板](whats-new-in-aspnet-mvc-4/_static/image5.png "中不同的浏览器大小的 ASP.NET MVC 4 项目模板")</span><span class="sxs-lookup"><span data-stu-id="27d1d-178">![ASP.NET MVC 4 project template in different browser sizes](whats-new-in-aspnet-mvc-4/_static/image5.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

    <span data-ttu-id="27d1d-179">*在不同的浏览器大小中的 ASP.NET MVC 4 项目模板*</span><span class="sxs-lookup"><span data-stu-id="27d1d-179">*ASP.NET MVC 4 project template in different browser sizes*</span></span>

    <span data-ttu-id="27d1d-180">**使用 JavaScript 更丰富的 UI**</span><span class="sxs-lookup"><span data-stu-id="27d1d-180">**Richer UI with JavaScript**</span></span>

    <span data-ttu-id="27d1d-181">默认项目模板的另一个增强功能是使用 JavaScript 来提供更具交互性的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="27d1d-181">Another enhancement to default project templates is the use of JavaScript to provide a more interactive JavaScript.</span></span> <span data-ttu-id="27d1d-182">在模板中使用的登录和注册链接将如何使用 jQuery 验证来验证从客户端的输入的字段。</span><span class="sxs-lookup"><span data-stu-id="27d1d-182">The Login and Register links used in the template exemplify how to use the jQuery Validations to validate the input fields from client-side.</span></span>

    ![jQuery 验证](whats-new-in-aspnet-mvc-4/_static/image6.png)

    <span data-ttu-id="27d1d-184">*jQuery 验证*</span><span class="sxs-lookup"><span data-stu-id="27d1d-184">*jQuery Validation*</span></span>

    > [!NOTE]
    > <span data-ttu-id="27d1d-185">请注意，这两个日志中的第一节中的部分，您可以记录中使用该站点中的注册帐户和可以使用另一个身份验证服务，如 google （默认情况下禁用） 的 altenativelly 登录的第二个部分。</span><span class="sxs-lookup"><span data-stu-id="27d1d-185">Notice the two log in sections, in the first section you can log in using a registerd account from the site and in the second section you can altenativelly log in using another authentication service like google (disabled by default).</span></span>
5. <span data-ttu-id="27d1d-186">关闭浏览器以停止调试器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="27d1d-186">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="27d1d-187">打开文件**AuthConfig.cs**位于**应用\_启动**文件夹。</span><span class="sxs-lookup"><span data-stu-id="27d1d-187">Open the file **AuthConfig.cs** located under the **App\_Start** folder.</span></span>
7. <span data-ttu-id="27d1d-188">从注册 Google 客户端的最后一行中删除注释*OAuth*身份验证。</span><span class="sxs-lookup"><span data-stu-id="27d1d-188">Remove the comment from the last line to register Google client for *OAuth* authentication.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > <span data-ttu-id="27d1d-189">请注意，可以轻松启用使用如 Facebook、 Twitter、 Microsoft 等任何 OpenID 或 OAuth 服务进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="27d1d-189">Notice you can easily enable authentication using any OpenID or OAuth service like Facebook, Twitter, Microsoft, etc.</span></span>
8. <span data-ttu-id="27d1d-190">按**F5**运行解决方案并导航到登录页。</span><span class="sxs-lookup"><span data-stu-id="27d1d-190">Press **F5** to run the solution and navigate to the login page.</span></span>
9. <span data-ttu-id="27d1d-191">选择**Google**服务进行登录。</span><span class="sxs-lookup"><span data-stu-id="27d1d-191">Select **Google** service to log in.</span></span>

    ![在服务中选择日志](whats-new-in-aspnet-mvc-4/_static/image7.png)

    <span data-ttu-id="27d1d-193">*在服务中选择日志*</span><span class="sxs-lookup"><span data-stu-id="27d1d-193">*Selecting the log in service*</span></span>
10. <span data-ttu-id="27d1d-194">使用你的 Google 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="27d1d-194">Log in using your Google account.</span></span>
11. <span data-ttu-id="27d1d-195">允许 Google 帐户中检索信息的站点 (localhost)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-195">Allow the site (localhost) to retrieve information from Google account.</span></span>
12. <span data-ttu-id="27d1d-196">最后，您将必须在要将 Google 帐户相关联的站点中注册。</span><span class="sxs-lookup"><span data-stu-id="27d1d-196">Finally, you will have to register in the site to associate the Google account.</span></span>

   ![将你的 Google 帐户相关联](whats-new-in-aspnet-mvc-4/_static/image8.png)

   <span data-ttu-id="27d1d-198">*将你的 Google 帐户相关联*</span><span class="sxs-lookup"><span data-stu-id="27d1d-198">*Associating your Google account*</span></span>
13. <span data-ttu-id="27d1d-199">关闭浏览器以停止调试器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="27d1d-199">Close the browser to stop the debugger and return to Visual Studio.</span></span>
14. <span data-ttu-id="27d1d-200">立即浏览要查看由 ASP.NET MVC 4 项目模板中引入了一些其他新功能的解决方案。</span><span class="sxs-lookup"><span data-stu-id="27d1d-200">Now explore the solution to check out some other new features introduced by ASP.NET MVC 4 in the project template.</span></span>

   <span data-ttu-id="27d1d-201">![ASP.NET MVC 4 Internet 应用程序项目模板](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 Internet 应用程序项目模板")</span><span class="sxs-lookup"><span data-stu-id="27d1d-201">![The ASP.NET MVC 4 Internet Application Project Template](whats-new-in-aspnet-mvc-4/_static/image9.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

   <span data-ttu-id="27d1d-202">*ASP.NET MVC 4 Internet 应用程序项目模板*</span><span class="sxs-lookup"><span data-stu-id="27d1d-202">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

   - <span data-ttu-id="27d1d-203">**HTML 5 标记**</span><span class="sxs-lookup"><span data-stu-id="27d1d-203">**HTML 5 Markup**</span></span>

       <span data-ttu-id="27d1d-204">浏览模板视图若要了解新的主题标记。</span><span class="sxs-lookup"><span data-stu-id="27d1d-204">Browse template views to find out the new theme markup.</span></span>

       <span data-ttu-id="27d1d-205">![使用 Razor 和 HTML5 标记 About.cshtml 新模板.](whats-new-in-aspnet-mvc-4/_static/image10.png "使用 Razor 和 HTML5 标记 About.cshtml 的新模板。")</span><span class="sxs-lookup"><span data-stu-id="27d1d-205">![New template, using Razor and HTML5 markup About.cshtml.](whats-new-in-aspnet-mvc-4/_static/image10.png "New template, using Razor and HTML5 markup About.cshtml.")</span></span>

       <span data-ttu-id="27d1d-206">*新模板，使用 Razor 和 HTML5 标记 (About.cshtml)。*</span><span class="sxs-lookup"><span data-stu-id="27d1d-206">*New template, using Razor and HTML5 markup (About.cshtml).*</span></span>
   - <span data-ttu-id="27d1d-207">**更新的 JavaScript 库**</span><span class="sxs-lookup"><span data-stu-id="27d1d-207">**Updated JavaScript libraries**</span></span>

       <span data-ttu-id="27d1d-208">ASP.NET MVC 4 默认模板现在包括 KnockoutJS、 允许您创建丰富的 JavaScript MVVM 框架和高响应 web 应用程序使用 JavaScript 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="27d1d-208">The ASP.NET MVC 4 default template now includes KnockoutJS, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="27d1d-209">如在 MVC3，jQuery 和 jQuery UI 库都还包含在 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="27d1d-209">Like in MVC3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

     > [!NOTE]
     > <span data-ttu-id="27d1d-210">可以获取有关此链接中的 KnockOutJS 库的详细信息： [ [ http://learn.knockoutjs.com/ ](http://learn.knockoutjs.com/) ](http://learn.knockoutjs.com/)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-210">You can get more information about KnockOutJS library in this link: [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/).</span></span> <span data-ttu-id="27d1d-211">此外，了解有关 jQuery 和 jQuery UI 中[ [ http://docs.jquery.com/ ](http://docs.jquery.com/) ](http://docs.jquery.com/)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-211">Additionally, you can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a><span data-ttu-id="27d1d-212">任务 2-探索移动应用程序模板</span><span class="sxs-lookup"><span data-stu-id="27d1d-212">Task 2 - Exploring the Mobile Application Template</span></span>

<span data-ttu-id="27d1d-213">ASP.NET MVC 4 便于网站适用于移动设备和平板电脑浏览器的开发。</span><span class="sxs-lookup"><span data-stu-id="27d1d-213">ASP.NET MVC 4 facilitates the development of websites for mobile and tablet browsers.</span></span> <span data-ttu-id="27d1d-214">此模板具有相同的应用程序结构为 Internet 应用程序模板 （请注意控制器代码，并几乎完全相同），但其样式进行了修改以便在基于触控的移动设备中正确呈现。</span><span class="sxs-lookup"><span data-stu-id="27d1d-214">This template has the same application structure as the Internet Application template (notice that the controller code is practically identical), but its style was modified to render properly in touch-based mobile devices.</span></span>

1. <span data-ttu-id="27d1d-215">选择**文件 |新 |项目**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="27d1d-215">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="27d1d-216">在中**新的项目**对话框中，选择**Visual C# |Web**在左窗格中的模板树，并选择**ASP.NET MVC 4 Web 应用程序。**</span><span class="sxs-lookup"><span data-stu-id="27d1d-216">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="27d1d-217">将项目命名**PhotoGallery.Mobile**，选择一个位置 （或保留默认值），选择&quot;将添加到解决方案&quot;然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-217">Name the project **PhotoGallery.Mobile**, select a location (or leave the default), select &quot;Add to solution&quot; and click **OK**.</span></span>
2. <span data-ttu-id="27d1d-218">在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Mobile 应用程序**项目模板，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-218">In the **New ASP.NET MVC 4 Project** dialog, select the **Mobile Application** project template and click **OK**.</span></span> <span data-ttu-id="27d1d-219">请确保已选择 Razor 作为视图引擎。</span><span class="sxs-lookup"><span data-stu-id="27d1d-219">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="27d1d-220">![创建新 ASP.NET MVC 4 移动应用程序](whats-new-in-aspnet-mvc-4/_static/image11.png "新建 ASP.NET MVC 4 移动应用程序")</span><span class="sxs-lookup"><span data-stu-id="27d1d-220">![Creating a new ASP.NET MVC 4 Mobile Application](whats-new-in-aspnet-mvc-4/_static/image11.png "Creating a new ASP.NET MVC 4 Mobile Application")</span></span>

    <span data-ttu-id="27d1d-221">*创建新 ASP.NET MVC 4 移动应用程序*</span><span class="sxs-lookup"><span data-stu-id="27d1d-221">*Creating a new ASP.NET MVC 4 Mobile Application*</span></span>
3. <span data-ttu-id="27d1d-222">现在，你就能够了解解决方案，并查看一些引入移动的 ASP.NET MVC 4 解决方案模板的新功能：</span><span class="sxs-lookup"><span data-stu-id="27d1d-222">Now you are able to explore the solution and check out some of the new features introduced by the ASP.NET MVC 4 solution template for mobile:</span></span>

    - <span data-ttu-id="27d1d-223">**jQuery 移动库**</span><span class="sxs-lookup"><span data-stu-id="27d1d-223">**jQuery Mobile Library**</span></span>

        <span data-ttu-id="27d1d-224">移动应用程序项目模板包括 jQuery 移动库，它是移动浏览器兼容性的开源库。</span><span class="sxs-lookup"><span data-stu-id="27d1d-224">The Mobile Application project template includes the jQuery Mobile library, which is an open source library for mobile browser compatibility.</span></span> <span data-ttu-id="27d1d-225">jQuery Mobile 对支持 CSS 和 JavaScript 的移动浏览器应用渐进增强。</span><span class="sxs-lookup"><span data-stu-id="27d1d-225">jQuery Mobile applies progressive enhancement to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="27d1d-226">渐进式增强功能，所有浏览器显示网页的基本内容，同时仅使功能最强大的浏览器显示的丰富内容。</span><span class="sxs-lookup"><span data-stu-id="27d1d-226">Progressive enhancement enables all browsers to display the basic content of a web page, while it only enables the most powerful browsers to display the rich content.</span></span> <span data-ttu-id="27d1d-227">JavaScript 和 CSS 文件，包括 jQuery 移动样式在帮助移动浏览器以适应屏幕中的内容，而无需在页标记中进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="27d1d-227">The JavaScript and CSS files, included in the jQuery Mobile style, help mobile browsers to fit the content in the screen without making any change in the page markup.</span></span>

        ![jQuery-mobile-library-included-in-the-template](whats-new-in-aspnet-mvc-4/_static/image12.png)

        <span data-ttu-id="27d1d-229">*模板中包括 jQuery 移动库*</span><span class="sxs-lookup"><span data-stu-id="27d1d-229">*jQuery mobile library included in the template*</span></span>
    - <span data-ttu-id="27d1d-230">**基于 HTML5 标记**</span><span class="sxs-lookup"><span data-stu-id="27d1d-230">**HTML5 based markup**</span></span>

        ![Mobile-application-template-using-HTML5-markup](whats-new-in-aspnet-mvc-4/_static/image13.png)

        <span data-ttu-id="27d1d-232">*使用 HTML5 标记、 （Login.cshtml 和 index.cshtml） 的移动应用程序模板*</span><span class="sxs-lookup"><span data-stu-id="27d1d-232">*Mobile application template using HTML5 markup, (Login.cshtml and index.cshtml)*</span></span>
4. <span data-ttu-id="27d1d-233">按**F5**运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="27d1d-233">Press **F5** to run the solution.</span></span>
5. <span data-ttu-id="27d1d-234">打开**Windows Phone 7 仿真程序**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-234">Open the **Windows Phone 7 Emulator**.</span></span>
6. <span data-ttu-id="27d1d-235">在电话开始屏幕中，打开 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="27d1d-235">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="27d1d-236">签出的桌面应用程序的起始位置的 URL 并通过手机浏览到该 URL (例如`http://localhost:[PortNumber]/`)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-236">Check out the URL where the desktop application started and browse to that URL from the phone (e.g. `http://localhost:[PortNumber]/`).</span></span>
7. <span data-ttu-id="27d1d-237">现在，你就能够输入的登录页或查看有关页面。</span><span class="sxs-lookup"><span data-stu-id="27d1d-237">Now you are able to enter the login page or check out the about page.</span></span> <span data-ttu-id="27d1d-238">请注意到该网站的样式基于新美俏移动设备的应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-238">Notice that the style of the website is based on the new Metro app for mobile.</span></span> <span data-ttu-id="27d1d-239">ASP.NET MVC 4 项目模板正确显示移动设备，从而确保页面的所有元素都都可见且已启用。</span><span class="sxs-lookup"><span data-stu-id="27d1d-239">The ASP.NET MVC 4 project template is correctly displayed on mobile devices, making sure all the elements of the page are visible and enabled.</span></span> <span data-ttu-id="27d1d-240">请注意，在标头中的链接不够大，无法单击或点击。</span><span class="sxs-lookup"><span data-stu-id="27d1d-240">Notice that the links on the header are big enough to be clicked or tapped.</span></span>

    <span data-ttu-id="27d1d-241">![项目在移动设备中的模板页](whats-new-in-aspnet-mvc-4/_static/image14.png "项目在移动设备中的模板页")</span><span class="sxs-lookup"><span data-stu-id="27d1d-241">![Project template pages in a mobile device](whats-new-in-aspnet-mvc-4/_static/image14.png "Project template pages in a mobile device")</span></span>

    <span data-ttu-id="27d1d-242">*在移动设备中的项目模板页*</span><span class="sxs-lookup"><span data-stu-id="27d1d-242">*Project template pages in a mobile device*</span></span>
8. <span data-ttu-id="27d1d-243">新模板还使用了**视区 meta 标记**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-243">The new template also uses the **Viewport meta tag**.</span></span> <span data-ttu-id="27d1d-244">大多数移动浏览器定义虚拟浏览器窗口的宽度或&quot;视区&quot;，这比移动设备的实际宽度。</span><span class="sxs-lookup"><span data-stu-id="27d1d-244">Most mobile browsers define a width for a virtual browser window or &quot;viewport&quot;, which is larger than the actual width of the mobile device.</span></span> <span data-ttu-id="27d1d-245">这使得移动浏览器以显示整个 web 页内的虚拟显示器。</span><span class="sxs-lookup"><span data-stu-id="27d1d-245">This enables mobile browsers to display the entire web page inside the virtual display.</span></span> <span data-ttu-id="27d1d-246">**视区 meta 标记**使 web 开发人员的移动设备上设置的宽度、 高度和小数位数为浏览器区域 **。**</span><span class="sxs-lookup"><span data-stu-id="27d1d-246">The **Viewport meta tag** allows web developers to set the width, height and scale of the browser area on mobile devices **.**</span></span> <span data-ttu-id="27d1d-247">移动应用程序的 ASP.NET MVC 4 模板将视区设置为设备宽 (&quot;宽度 = 设备宽度&quot;) 中的布局模板 (*views/shared\_Layout.cshtml*)，以便所有页面将具有其视区设置为设备屏幕宽度。</span><span class="sxs-lookup"><span data-stu-id="27d1d-247">The ASP.NET MVC 4 template for Mobile Applications sets the viewport to the device width (&quot;width=device-width&quot;) in the layout template (*Views\Shared\_Layout.cshtml*), so that all the pages will have their viewport set to the device screen width.</span></span> <span data-ttu-id="27d1d-248">请注意，视区 meta 标记不会更改默认浏览器视图。</span><span class="sxs-lookup"><span data-stu-id="27d1d-248">Notice that the Viewport meta tag will not change the default browser view.</span></span>
9. <span data-ttu-id="27d1d-249">打开 **\_Layout.cshtml**，它位于**视图 |共享**文件夹，并注释视区 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="27d1d-249">Open **\_Layout.cshtml**, located in the **Views | Shared** folder, and comment the Viewport meta tag.</span></span> <span data-ttu-id="27d1d-250">运行应用程序，如果不是已打开，并查看差异。</span><span class="sxs-lookup"><span data-stu-id="27d1d-250">Run the application, if not already opened, and check out the differences.</span></span>


[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

<span data-ttu-id="27d1d-251">![注释视区 meta 标记后的站点](whats-new-in-aspnet-mvc-4/_static/image15.png "注释视区 meta 标记后的站点")</span><span class="sxs-lookup"><span data-stu-id="27d1d-251">![The site after commenting the viewport meta tag](whats-new-in-aspnet-mvc-4/_static/image15.png "The site after commenting the viewport meta tag")</span></span>

<span data-ttu-id="27d1d-252">*注释视区 meta 标记后站点*</span><span class="sxs-lookup"><span data-stu-id="27d1d-252">*The site after commenting the viewport meta tag*</span></span>
10. <span data-ttu-id="27d1d-253">在 Visual Studio 中，按**SHIFT** + **F5**以停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-253">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
11. <span data-ttu-id="27d1d-254">取消注释视区 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="27d1d-254">Uncomment the viewport meta tag.</span></span>


[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a><span data-ttu-id="27d1d-255">任务 3-使用自适应呈现</span><span class="sxs-lookup"><span data-stu-id="27d1d-255">Task 3 - Using Adaptive Rendering</span></span>

<span data-ttu-id="27d1d-256">在本任务中，您将学习另一种方法，而无需进行任何自定义同时呈现在移动设备和 Web 浏览器上正常网页。</span><span class="sxs-lookup"><span data-stu-id="27d1d-256">In this task, you will learn another method to render a Web page correctly on mobile devices and Web browsers at the same time without any customization.</span></span> <span data-ttu-id="27d1d-257">你已具有类似用途使用视区 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="27d1d-257">You have already used Viewport meta tag with a similar purpose.</span></span> <span data-ttu-id="27d1d-258">现在就可以满足另一个功能强大的方法：*自适应呈现*。</span><span class="sxs-lookup"><span data-stu-id="27d1d-258">Now you will meet another powerful method: *adaptive rendering*.</span></span>

<span data-ttu-id="27d1d-259">自适应呈现是使用一种技术**CSS3 媒体查询**自定义应用于页面的样式。</span><span class="sxs-lookup"><span data-stu-id="27d1d-259">Adaptive rendering is a technique that uses **CSS3 media queries** to customize the style applied to a page.</span></span> <span data-ttu-id="27d1d-260">媒体查询定义分组的特定条件下的 CSS 样式的样式表内的条件。</span><span class="sxs-lookup"><span data-stu-id="27d1d-260">Media queries define conditions inside a style sheet, grouping CSS styles under a certain condition.</span></span> <span data-ttu-id="27d1d-261">仅当条件为 true，则会将样式应用于已声明的对象。</span><span class="sxs-lookup"><span data-stu-id="27d1d-261">Only when the condition is true, the style is applied to the declared objects.</span></span>

<span data-ttu-id="27d1d-262">提供的自适应呈现技术的灵活性使不同的设备上显示该站点进行任何自定义。</span><span class="sxs-lookup"><span data-stu-id="27d1d-262">The flexibility provided by the adaptive rendering technique enables any customization for displaying the site on different devices.</span></span> <span data-ttu-id="27d1d-263">您可以定义任意多个样式所需的单一样式表上而无需编写逻辑代码选择样式。</span><span class="sxs-lookup"><span data-stu-id="27d1d-263">You can define as many styles as you want on a single style sheet without writing logic code to choose the style.</span></span> <span data-ttu-id="27d1d-264">因此，因为它可以减少重复的代码和用于呈现目的的逻辑的数量是调整页样式的一种非常巧妙方法。</span><span class="sxs-lookup"><span data-stu-id="27d1d-264">Therefore, it is a very neat way of adapting page styles, as it reduces the amount of duplicated code and logic for rendering purposes.</span></span> <span data-ttu-id="27d1d-265">但是，带宽消耗会增加，如 CSS 文件的大小会变得略微。</span><span class="sxs-lookup"><span data-stu-id="27d1d-265">On the other hand, bandwidth consumption would increase, as the size of your CSS files could grow marginally.</span></span>

<span data-ttu-id="27d1d-266">通过使用自适应呈现技术，站点将**正确显示，而不考虑浏览器。**</span><span class="sxs-lookup"><span data-stu-id="27d1d-266">By using the adaptive rendering technique, your site will be **displayed properly, regardless of the browser.**</span></span> <span data-ttu-id="27d1d-267">但是，应该考虑是否加载了额外的带宽是一个问题。</span><span class="sxs-lookup"><span data-stu-id="27d1d-267">However, you should consider if the bandwidth extra load is a concern.</span></span>

> [!NOTE]
> <span data-ttu-id="27d1d-268">媒体查询的基本格式： @media \[作用域： 所有 | 手持 | 打印 | 投影 | 屏幕\]([属性： 值]，然后...[属性： 值]）</span><span class="sxs-lookup"><span data-stu-id="27d1d-268">The basic format of a media query is: @media \[Scope: all | handheld | print | projection | screen\] ([property:value] and ... [property:value])</span></span>


<span data-ttu-id="27d1d-269">媒体查询的示例： &gt;  <strong>@media所有和 (最大宽度： 1000 像素) 和 (最小宽度： 700px) {}:</strong>有关 700px 和 1000 像素之间的所有解决方法。</span><span class="sxs-lookup"><span data-stu-id="27d1d-269">Examples of media queries: &gt;<strong>@media all and (max-width: 1000px) and (min-width: 700px) {}:</strong> For all the resolutions between 700px and 1000px.</span></span>

> <span data-ttu-id="27d1d-270"><strong>@media 屏幕和 (最小宽度： 400px) 和 (最大宽度： 700px) {...}:</strong>仅对于屏幕。</span><span class="sxs-lookup"><span data-stu-id="27d1d-270"><strong>@media screen and (min-width: 400px) and (max-width: 700px) { ... }:</strong> Only for screens.</span></span> <span data-ttu-id="27d1d-271">解决方法必须介于 400 和 700px 之间。</span><span class="sxs-lookup"><span data-stu-id="27d1d-271">The resolution must be between 400 and 700px.</span></span>
> 
> <span data-ttu-id="27d1d-272"><strong>@media 手持和 (最小宽度： 20em)，屏幕和 (最小宽度： 20em) {...}:</strong>手持设备 （移动设备和设备） 和屏幕。</span><span class="sxs-lookup"><span data-stu-id="27d1d-272"><strong>@media handheld and (min-width: 20em), screen and (min-width: 20em) { ... }:</strong> For handhelds(mobile and devices) and screens.</span></span> <span data-ttu-id="27d1d-273">最小宽度必须大于 20em。</span><span class="sxs-lookup"><span data-stu-id="27d1d-273">The minimum width must be greater than 20em.</span></span>
> 
> <span data-ttu-id="27d1d-274">有关更多相关信息[W3C 站点](http://www.w3.org/TR/css3-mediaqueries/)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-274">You can find more information about this on the [W3C site](http://www.w3.org/TR/css3-mediaqueries/).</span></span>


<span data-ttu-id="27d1d-275">您现在将探索自适应呈现的工作原理、 提高其可读性的 ASP.NET MVC 4 默认网站模板。</span><span class="sxs-lookup"><span data-stu-id="27d1d-275">You will now explore how the adaptive rendering works, improving the readability of the ASP.NET MVC 4 default website template.</span></span>

1. <span data-ttu-id="27d1d-276">打开**PhotoGallery.sln**解决方案已在任务 1 中创建并选择**PhotoGallery**项目。</span><span class="sxs-lookup"><span data-stu-id="27d1d-276">Open the **PhotoGallery.sln** solution you have created at Task 1 and select the **PhotoGallery** project.</span></span> <span data-ttu-id="27d1d-277">按**F5**运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="27d1d-277">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="27d1d-278">调整浏览器的宽度，设置 windows 到一半或小于其原始大小的四分之一。</span><span class="sxs-lookup"><span data-stu-id="27d1d-278">Resize the browser's width, setting the windows to half or to less than a quarter of its original size.</span></span> <span data-ttu-id="27d1d-279">请注意，在标头中的项会出现什么情况： 一些元素不会显示在标头的可见区域。</span><span class="sxs-lookup"><span data-stu-id="27d1d-279">Notice what happens with the items in the header: Some elements will not appear in the visible area of the header.</span></span>
3. <span data-ttu-id="27d1d-280">打开<strong>Site.css</strong>文件从 Visual Studio 解决方案资源管理器，位于<strong>内容</strong>项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="27d1d-280">Open <strong>Site.css</strong> file from the Visual Studio Solution explorer, located in <strong>Content</strong> project folder.</span></span> <span data-ttu-id="27d1d-281">按<strong>CTRL + F</strong>若要打开 Visual Studio 集成的搜索，并写入<strong>@media</strong>查找<strong>CSS 媒体查询</strong>。</span><span class="sxs-lookup"><span data-stu-id="27d1d-281">Press <strong>CTRL + F</strong> to open Visual Studio integrated search, and write <strong>@media</strong> to locate the <strong>CSS media query</strong>.</span></span>

    <span data-ttu-id="27d1d-282">此模板中定义的媒体查询条件的工作以这种方式： 当浏览器的窗口大小低于**850 px**，应用的 CSS 规则是在此媒体块内定义的。</span><span class="sxs-lookup"><span data-stu-id="27d1d-282">The media query condition defined in this template works in this way: When the browser's window size is below **850 px**, the CSS rules applied are the ones defined inside this media block.</span></span>

    <span data-ttu-id="27d1d-283">![定位到该媒体查询](whats-new-in-aspnet-mvc-4/_static/image16.png "定位到该媒体查询")</span><span class="sxs-lookup"><span data-stu-id="27d1d-283">![Locating the media query](whats-new-in-aspnet-mvc-4/_static/image16.png "Locating the media query")</span></span>

    <span data-ttu-id="27d1d-284">*定位到该媒体查询*</span><span class="sxs-lookup"><span data-stu-id="27d1d-284">*Locating the media query*</span></span>
4. <span data-ttu-id="27d1d-285">850 中设置的最大宽度属性值替换为与 px **10px**，以便禁用自适应呈现，然后按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="27d1d-285">Replace the max-width attribute value set in 850 px with **10px**, in order to disable the adaptive rendering, and press **CTRL + S** to save the changes.</span></span> <span data-ttu-id="27d1d-286">返回到浏览器并按**CTRL + F5**若要刷新所做的更改与页面。</span><span class="sxs-lookup"><span data-stu-id="27d1d-286">Return to the browser and press **CTRL + F5** to refresh the page with the changes you have made.</span></span> <span data-ttu-id="27d1d-287">调整窗口的宽度时，请注意这两个页中的差异。</span><span class="sxs-lookup"><span data-stu-id="27d1d-287">Notice the differences in both pages when adjusting the width of the window.</span></span>

    <span data-ttu-id="27d1d-288">![在左侧，应用页@media省略样式，请在右侧，样式](whats-new-in-aspnet-mvc-4/_static/image17.png "左侧，在应用页@media省略样式，请在右侧，样式")</span><span class="sxs-lookup"><span data-stu-id="27d1d-288">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image17.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="27d1d-289"><em>在左侧，应用页@media省略样式，请在右侧，样式</em></span><span class="sxs-lookup"><span data-stu-id="27d1d-289"><em>In the left, the page is applying the @media style, in the right, the style is omitted</em></span></span>

    <span data-ttu-id="27d1d-290">现在，我们来看下在移动设备上会发生什么情况：</span><span class="sxs-lookup"><span data-stu-id="27d1d-290">Now, let's check out what happens on mobile devices:</span></span>

    <span data-ttu-id="27d1d-291">![在左侧，应用页@media省略样式，请在右侧，样式](whats-new-in-aspnet-mvc-4/_static/image18.png "左侧，在应用页@media省略样式，请在右侧，样式")</span><span class="sxs-lookup"><span data-stu-id="27d1d-291">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image18.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="27d1d-292"><em>在左侧，应用页@media省略样式，请在右侧，样式</em></span><span class="sxs-lookup"><span data-stu-id="27d1d-292"><em>In the left, the page is applying the @media style, in the right, the style is omitted</em></span></span>

    <span data-ttu-id="27d1d-293">尽管您会注意到，在 Web 浏览器中呈现页时不更改非常重要，使用移动设备时的差异变得更明显。</span><span class="sxs-lookup"><span data-stu-id="27d1d-293">Although you will notice that the changes when the page is rendered in a Web browser are not very significant, when using a mobile device the differences become more obvious.</span></span> <span data-ttu-id="27d1d-294">在左侧和右侧的图像，我们可以看到的自定义样式提高了可读性。</span><span class="sxs-lookup"><span data-stu-id="27d1d-294">On the left side of the image, we can see that the custom style improved the readability.</span></span>

    <span data-ttu-id="27d1d-295">可以在很多情况，从而更便于将条件设置到网站上的样式和解决常见的一种巧妙方法样式问题应用中使用自适应呈现。</span><span class="sxs-lookup"><span data-stu-id="27d1d-295">Adaptive rendering can be used in many more scenarios, making it easier to apply conditional styling to a Web site and solving common style issues with a neat approach.</span></span>

    <span data-ttu-id="27d1d-296">视区 meta 标记和 CSS 媒体查询不是特定于 ASP.NET MVC 4 中，因此您可以在任何 web 应用程序中充分利用这些功能。</span><span class="sxs-lookup"><span data-stu-id="27d1d-296">The Viewport meta tag and CSS media queries are not specific to ASP.NET MVC 4, so you can take advantage of these features in any web application.</span></span>
5. <span data-ttu-id="27d1d-297">在 Visual Studio 中，按**SHIFT** + **F5**以停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-297">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a><span data-ttu-id="27d1d-298">练习 2： 创建照片库 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="27d1d-298">Exercise 2: Creating the Photo Gallery Web Application</span></span>

<span data-ttu-id="27d1d-299">在此练习中，您将适用于显示照片的照片库应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-299">In this exercise, you will work on a Photo Gallery application to display photos.</span></span> <span data-ttu-id="27d1d-300">ASP.NET MVC 4 项目模板，将开始，然后您将添加一项功能以从服务中检索照片并将其显示在主页页面中。</span><span class="sxs-lookup"><span data-stu-id="27d1d-300">You will start with the ASP.NET MVC 4 project template, and then you will add a feature to retrieve photos from a service and display them in the home page.</span></span>

<span data-ttu-id="27d1d-301">在以下练习中，你将更新此解决方案以增强移动设备显示的方式。</span><span class="sxs-lookup"><span data-stu-id="27d1d-301">In the following exercise, you will update this solution to enhance the way it is displayed on mobile devices.</span></span>

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a><span data-ttu-id="27d1d-302">任务 1-创建 Mock 照片服务</span><span class="sxs-lookup"><span data-stu-id="27d1d-302">Task 1 - Creating a Mock Photo Service</span></span>

<span data-ttu-id="27d1d-303">在本任务中，您将创建要检索的内容将显示在库中的照片服务的模拟。</span><span class="sxs-lookup"><span data-stu-id="27d1d-303">In this task, you will create a mock of the photo service to retrieve the content that will be displayed in the gallery.</span></span> <span data-ttu-id="27d1d-304">若要执行此操作，将添加将只返回每张照片的数据的 JSON 文件的新控制器。</span><span class="sxs-lookup"><span data-stu-id="27d1d-304">To do this, you will add a new controller that will simply return a JSON file with the data of each photo.</span></span>

1. <span data-ttu-id="27d1d-305">打开**Visual Studio**如果尚未打开。</span><span class="sxs-lookup"><span data-stu-id="27d1d-305">Open **Visual Studio** if not already opened.</span></span>
2. <span data-ttu-id="27d1d-306">选择**文件 |新 |项目**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="27d1d-306">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="27d1d-307">在中**新的项目**对话框中，选择**Visual C# |Web**在左窗格中的模板树，并选择**ASP.NET MVC 4 Web 应用程序。**</span><span class="sxs-lookup"><span data-stu-id="27d1d-307">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="27d1d-308">将项目命名**PhotoGallery**，选择一个位置 （或保留默认值），单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-308">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span> <span data-ttu-id="27d1d-309">或者，从现有的 ASP.NET MVC 4 继续工作**Internet 应用程序**从解决方案**练习 1**并跳过下一步。</span><span class="sxs-lookup"><span data-stu-id="27d1d-309">Alternatively, you can continue working from your existing ASP.NET MVC 4 **Internet Application** solution from **Exercise 1** and skip the next step.</span></span>
3. <span data-ttu-id="27d1d-310">在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**项目模板，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-310">In the **New ASP.NET MVC 4 Project** dialog box, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="27d1d-311">请确保具有 Razor 视图引擎为所选。</span><span class="sxs-lookup"><span data-stu-id="27d1d-311">Make sure you have Razor selected as the View Engine.</span></span>
4. <span data-ttu-id="27d1d-312">在中**解决方案资源管理器**，右键单击**应用\_数据**文件夹的项目，然后选择**添加 |现有项**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-312">In the **Solution Explorer**, right-click the **App\_Data** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="27d1d-313">浏览到**Source\Assets\App\_数据**本实验的文件夹，并添加**Photos.json**文件。</span><span class="sxs-lookup"><span data-stu-id="27d1d-313">Browse to the **Source\Assets\App\_Data** folder of this lab and add the **Photos.json** file.</span></span>
5. <span data-ttu-id="27d1d-314">创建新的控制器名称**PhotoController**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-314">Create a new controller with the name **PhotoController**.</span></span> <span data-ttu-id="27d1d-315">若要执行此操作，右键单击**控制器**文件夹中，转到**添加**，然后选择**控制器。**</span><span class="sxs-lookup"><span data-stu-id="27d1d-315">To do this, right-click on the **Controllers** folder, go to **Add** and select **Controller.**</span></span> <span data-ttu-id="27d1d-316">完成该控制器的名称，将保留**空 MVC 控制器**模板，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-316">Complete the controller name, leave the **Empty MVC controller** template and click **Add**.</span></span>

    <span data-ttu-id="27d1d-317">![添加 PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "添加 PhotoController")</span><span class="sxs-lookup"><span data-stu-id="27d1d-317">![Adding the PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "Adding the PhotoController")</span></span>

    <span data-ttu-id="27d1d-318">*添加 PhotoController*</span><span class="sxs-lookup"><span data-stu-id="27d1d-318">*Adding the PhotoController*</span></span>
6. <span data-ttu-id="27d1d-319">替换**索引**方法替换以下**库**操作，并返回内容时从您最近添加到项目的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="27d1d-319">Replace the **Index** method with the following **Gallery** action, and return the content from the JSON file you have recently added to the project.</span></span>

    <span data-ttu-id="27d1d-320">(代码段- *ASP.NET MVC 4 实验-Ex02-库操作*)</span><span class="sxs-lookup"><span data-stu-id="27d1d-320">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Gallery Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. <span data-ttu-id="27d1d-321">按**F5**运行该解决方案，然后浏览到以下 URL 以测试模拟的照片服务： `http://localhost:[port]/photo/gallery` （已启动应用程序的当前端口上的 [端口] 值取决于）。</span><span class="sxs-lookup"><span data-stu-id="27d1d-321">Press **F5** to run the solution, and then browse to the following URL in order to test the mocked photo service: `http://localhost:[port]/photo/gallery` (the [port] value depends on the current port where the application was launched).</span></span> <span data-ttu-id="27d1d-322">对此 URL 的请求应检索的内容**Photos.json**文件。</span><span class="sxs-lookup"><span data-stu-id="27d1d-322">The request to this URL should retrieve the content of the **Photos.json** file.</span></span>

    <span data-ttu-id="27d1d-323">![测试模拟的照片服务](whats-new-in-aspnet-mvc-4/_static/image20.png "测试模拟的照片服务")</span><span class="sxs-lookup"><span data-stu-id="27d1d-323">![Testing the mocked photo service](whats-new-in-aspnet-mvc-4/_static/image20.png "Testing the mocked photo service")</span></span>

    <span data-ttu-id="27d1d-324">*测试模拟的照片服务*</span><span class="sxs-lookup"><span data-stu-id="27d1d-324">*Testing the mocked photo service*</span></span>

<span data-ttu-id="27d1d-325">在实际实现可以使用[ASP.NET Web API](../../../../web-api/index.md)实现照片库服务。</span><span class="sxs-lookup"><span data-stu-id="27d1d-325">In a real implementation you could use [ASP.NET Web API](../../../../web-api/index.md) to implement the Photo Gallery service.</span></span> <span data-ttu-id="27d1d-326">ASP.NET Web API 是一种框架，可以轻松地构建 HTTP 服务访问范围广泛的客户端，包括浏览器和移动设备。</span><span class="sxs-lookup"><span data-stu-id="27d1d-326">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="27d1d-327">ASP.NET Web API 是用于在 .NET Framework 上生成 RESTful 应用程序的理想平台。</span><span class="sxs-lookup"><span data-stu-id="27d1d-327">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a><span data-ttu-id="27d1d-328">任务 2-显示照片库</span><span class="sxs-lookup"><span data-stu-id="27d1d-328">Task 2 - Displaying the Photo Gallery</span></span>

<span data-ttu-id="27d1d-329">在本任务中，你将更新主页上要显示在照片库，请使用此练习中的第一个任务中创建的模拟的服务。</span><span class="sxs-lookup"><span data-stu-id="27d1d-329">In this task, you will update the Home page to show the photo gallery by using the mocked service you created in the first task of this exercise.</span></span> <span data-ttu-id="27d1d-330">将添加模型文件并更新库视图。</span><span class="sxs-lookup"><span data-stu-id="27d1d-330">You will add model files and update the gallery views.</span></span>

1. <span data-ttu-id="27d1d-331">在 Visual Studio 中，按**SHIFT** + **F5**以停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-331">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="27d1d-332">创建**照片**类**模型**文件夹。</span><span class="sxs-lookup"><span data-stu-id="27d1d-332">Create the **Photo** class in the **Models** folder.</span></span> <span data-ttu-id="27d1d-333">若要执行此操作，右键单击**模型**文件夹，选择**添加**然后单击**类**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-333">To do this, right-click on the **Models** folder, select **Add** and click **Class**.</span></span> <span data-ttu-id="27d1d-334">然后，将名称设置为**Photo.cs**然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-334">Then, set the name to **Photo.cs** and click **Add**.</span></span>
3. <span data-ttu-id="27d1d-335">添加到以下成员**照片**类。</span><span class="sxs-lookup"><span data-stu-id="27d1d-335">Add the following members to the **Photo** class.</span></span>

    <span data-ttu-id="27d1d-336">(代码段- *ASP.NET MVC 4 实验-Ex02-照片模型*)</span><span class="sxs-lookup"><span data-stu-id="27d1d-336">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo model*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. <span data-ttu-id="27d1d-337">从“控制器”文件夹打开 HomeController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="27d1d-337">Open the **HomeController.cs** file from the **Controllers** folder.</span></span>
5. <span data-ttu-id="27d1d-338">添加下面的 using 语句。</span><span class="sxs-lookup"><span data-stu-id="27d1d-338">Add the following using statements.</span></span>

    <span data-ttu-id="27d1d-339">(代码段- *ASP.NET MVC 4 实验-Ex02-HomeController Using*)</span><span class="sxs-lookup"><span data-stu-id="27d1d-339">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - HomeController Usings*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. <span data-ttu-id="27d1d-340">更新**索引**操作以使用**HttpClient**检索库数据，然后使用**JavaScriptSerializer**要反其序列化到视图模型。</span><span class="sxs-lookup"><span data-stu-id="27d1d-340">Update the **Index** action to use **HttpClient** to retrieve the gallery data, and then use the **JavaScriptSerializer** to deserialize it to the view model.</span></span>

    <span data-ttu-id="27d1d-341">(代码段- *ASP.NET MVC 4 实验-Ex02-索引操作*)</span><span class="sxs-lookup"><span data-stu-id="27d1d-341">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Index Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. <span data-ttu-id="27d1d-342">打开**Index.cshtml**下的文件**views/home**文件夹并将替换为以下代码的所有内容。</span><span class="sxs-lookup"><span data-stu-id="27d1d-342">Open the **Index.cshtml** file located under the **Views\Home** folder and replace all the content with the following code.</span></span>

    <span data-ttu-id="27d1d-343">此代码循环访问从服务检索的所有照片，并将它们显示为未排序列表。</span><span class="sxs-lookup"><span data-stu-id="27d1d-343">This code loops through all the photos retrieved from the service and displays them into an unordered list.</span></span>

    <span data-ttu-id="27d1d-344">(代码段- *ASP.NET MVC 4 实验-Ex02-照片列表*)</span><span class="sxs-lookup"><span data-stu-id="27d1d-344">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo List*)</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. <span data-ttu-id="27d1d-345">在中**解决方案资源管理器**，右键单击**内容**文件夹的项目，然后选择**添加 |现有项**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-345">In the **Solution Explorer**, right-click the **Content** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="27d1d-346">浏览到**Source\Assets\Content**本实验的文件夹，并添加**Site.css**文件。</span><span class="sxs-lookup"><span data-stu-id="27d1d-346">Browse to the **Source\Assets\Content** folder of this lab and add the **Site.css** file.</span></span> <span data-ttu-id="27d1d-347">必须确认其替换。</span><span class="sxs-lookup"><span data-stu-id="27d1d-347">You will have to confirm its replacement.</span></span> <span data-ttu-id="27d1d-348">如果有**Site.css**文件打开时，必须确认还重新加载该文件。</span><span class="sxs-lookup"><span data-stu-id="27d1d-348">If you have the **Site.css** file open, you will have to confirm to reload the file also.</span></span>
9. <span data-ttu-id="27d1d-349">打开文件资源管理器，并复制整个**照片**文件夹位于下**Source\Assets**此体验的解决方案资源管理器中的项目的根文件夹的文件夹。</span><span class="sxs-lookup"><span data-stu-id="27d1d-349">Open File Explorer and copy the entire **Photos** folder located under the **Source\Assets** folder of this lab to the root folder of your project in Solution Explorer.</span></span>
10. <span data-ttu-id="27d1d-350">运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-350">Run the application.</span></span> <span data-ttu-id="27d1d-351">现在应看到在库中显示照片的主页。</span><span class="sxs-lookup"><span data-stu-id="27d1d-351">You should now see the home page displaying the photos in the gallery.</span></span>

    <span data-ttu-id="27d1d-352">![照片库](whats-new-in-aspnet-mvc-4/_static/image21.png "照片库")</span><span class="sxs-lookup"><span data-stu-id="27d1d-352">![Photo Gallery](whats-new-in-aspnet-mvc-4/_static/image21.png "Photo Gallery")</span></span>

    <span data-ttu-id="27d1d-353">*照片库*</span><span class="sxs-lookup"><span data-stu-id="27d1d-353">*Photo Gallery*</span></span>
11. <span data-ttu-id="27d1d-354">在 Visual Studio 中，按**SHIFT** + **F5**以停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-354">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a><span data-ttu-id="27d1d-355">练习 3： 添加对移动设备的支持</span><span class="sxs-lookup"><span data-stu-id="27d1d-355">Exercise 3: Adding support for mobile devices</span></span>

<span data-ttu-id="27d1d-356">一个 ASP.NET MVC 4 中的关键更新是适用于移动开发的支持。</span><span class="sxs-lookup"><span data-stu-id="27d1d-356">One of the key updates in ASP.NET MVC 4 is the support for mobile development.</span></span> <span data-ttu-id="27d1d-357">在此练习中，您将通过扩展已在上一练习中创建的图片库解决方案浏览 ASP.NET MVC 4 移动应用程序的新功能。</span><span class="sxs-lookup"><span data-stu-id="27d1d-357">In this exercise, you will explore ASP.NET MVC 4 new features for mobile applications by extending the PhotoGallery solution you have created in the previous exercise.</span></span>

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a><span data-ttu-id="27d1d-358">任务 1-ASP.NET MVC 4 应用程序的安装 jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="27d1d-358">Task 1 - Installing jQuery Mobile in an ASP.NET MVC 4 Application</span></span>

1. <span data-ttu-id="27d1d-359">打开**开始**解决方案位于**源/Ex3-MobileSupport/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="27d1d-359">Open the **Begin** solution located at **Source/Ex3-MobileSupport/Begin/** folder.</span></span> <span data-ttu-id="27d1d-360">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="27d1d-360">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="27d1d-361">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="27d1d-361">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="27d1d-362">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-362">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="27d1d-363">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="27d1d-363">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="27d1d-364">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-364">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="27d1d-365">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="27d1d-365">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="27d1d-366">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="27d1d-366">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="27d1d-367">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="27d1d-367">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="27d1d-368">打开**程序包管理器控制台**通过单击**工具** &gt; **库程序包管理器** &gt; **包管理器控制台**菜单选项。</span><span class="sxs-lookup"><span data-stu-id="27d1d-368">Open the **Package Manager Console** by clicking the **Tools** &gt; **Library Package Manager** &gt; **Package Manager Console** menu option.</span></span>

    <span data-ttu-id="27d1d-369">![打开 NuGet Package Manager Console](whats-new-in-aspnet-mvc-4/_static/image22.png "打开 NuGet 包管理器控制台")</span><span class="sxs-lookup"><span data-stu-id="27d1d-369">![Opening the NuGet Package Manager Console](whats-new-in-aspnet-mvc-4/_static/image22.png "Opening the NuGet Package Manager Console")</span></span>

    <span data-ttu-id="27d1d-370">*打开 NuGet 包管理器控制台*</span><span class="sxs-lookup"><span data-stu-id="27d1d-370">*Opening the NuGet Package Manager Console*</span></span>
3. <span data-ttu-id="27d1d-371">在包管理器控制台中运行以下命令以安装**jQuery.Mobile.MVC**包。</span><span class="sxs-lookup"><span data-stu-id="27d1d-371">In the Package Manager Console run the following command to install the **jQuery.Mobile.MVC** package.</span></span>

    <span data-ttu-id="27d1d-372">jQuery Mobile 是一个开源库，用于构建触控优化的 web UI。</span><span class="sxs-lookup"><span data-stu-id="27d1d-372">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="27d1d-373">JQuery.Mobile.MVC NuGet 程序包包括帮助程序以使用 jQuery Mobile 与 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-373">The jQuery.Mobile.MVC NuGet package includes helpers to use jQuery Mobile with an ASP.NET MVC 4 application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27d1d-374">通过运行以下命令，你将下载 jQuery.Mobile.MVC 库从 Nuget。</span><span class="sxs-lookup"><span data-stu-id="27d1d-374">By running the following command, you will be downloading the jQuery.Mobile.MVC library from Nuget.</span></span>

    <span data-ttu-id="27d1d-375">PM</span><span class="sxs-lookup"><span data-stu-id="27d1d-375">PM</span></span>

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    <span data-ttu-id="27d1d-376">此命令将安装 jQuery Mobile 和一些帮助器文件，其中包括：</span><span class="sxs-lookup"><span data-stu-id="27d1d-376">This command installs jQuery Mobile and some helper files, including the following:</span></span>

    - <span data-ttu-id="27d1d-377">**Views/Shared/\_Layout.Mobile.cshtml**： 是针对较小屏幕而优化的 jQuery Mobile 基于布局。</span><span class="sxs-lookup"><span data-stu-id="27d1d-377">**Views/Shared/\_Layout.Mobile.cshtml**: is a jQuery Mobile-based layout optimized for a smaller screen.</span></span> <span data-ttu-id="27d1d-378">当网站收到请求时从移动浏览器时，它将替换原始布局 (\_Layout.cshtml) 替换为。</span><span class="sxs-lookup"><span data-stu-id="27d1d-378">When the website receives a request from a mobile browser, it will replace the original layout (\_Layout.cshtml) with this one.</span></span>
    - <span data-ttu-id="27d1d-379">视图切换器组件： 组成**Views/Shared/\_ViewSwitcher.cshtml**分部视图和**ViewSwitcherController.cs**控制器。</span><span class="sxs-lookup"><span data-stu-id="27d1d-379">A view-switcher component: consists of the **Views/Shared/\_ViewSwitcher.cshtml** partial view and the **ViewSwitcherController.cs** controller.</span></span> <span data-ttu-id="27d1d-380">此组件将在移动浏览器以使用户能够切换到桌面版本的页面上显示的链接。</span><span class="sxs-lookup"><span data-stu-id="27d1d-380">This component will show a link on mobile browsers to enable users to switch to the desktop version of the page.</span></span>  
        <span data-ttu-id="27d1d-381">![照片库项目与移动设备的支持](whats-new-in-aspnet-mvc-4/_static/image23.png "照片库项目与移动设备的支持")</span><span class="sxs-lookup"><span data-stu-id="27d1d-381">![Photo Gallery project with mobile support](whats-new-in-aspnet-mvc-4/_static/image23.png "Photo Gallery project with mobile support")</span></span>

        <span data-ttu-id="27d1d-382">*照片库项目与移动设备的支持*</span><span class="sxs-lookup"><span data-stu-id="27d1d-382">*Photo Gallery project with mobile support*</span></span>
4. <span data-ttu-id="27d1d-383">注册的移动捆绑包。</span><span class="sxs-lookup"><span data-stu-id="27d1d-383">Register the Mobile bundles.</span></span> <span data-ttu-id="27d1d-384">若要执行此操作，打开**Global.asax.cs**文件，并添加以下行。</span><span class="sxs-lookup"><span data-stu-id="27d1d-384">To do this, open the **Global.asax.cs** file and add the following line.</span></span>

    <span data-ttu-id="27d1d-385">(代码段- *ASP.NET MVC 4 实验室-Ex03-注册的移动捆绑*)</span><span class="sxs-lookup"><span data-stu-id="27d1d-385">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - Register Mobile Bundles*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. <span data-ttu-id="27d1d-386">运行使用桌面 web 浏览器的应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-386">Run the application using a desktop web browser.</span></span>
6. <span data-ttu-id="27d1d-387">打开**Windows Phone 7 仿真器**位于**开始菜单 |所有程序 |Windows Phone SDK 7.1 |Windows Phone 仿真程序。**</span><span class="sxs-lookup"><span data-stu-id="27d1d-387">Open the **Windows Phone 7 Emulator,** located in **Start Menu | All Programs | Windows Phone SDK 7.1 | Windows Phone Emulator.**</span></span>
7. <span data-ttu-id="27d1d-388">在电话开始屏幕中，打开 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="27d1d-388">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="27d1d-389">请查看应用程序的起始位置的 URL 并浏览到该 URL 与手机浏览器 (例如`http://localhost:[PortNumber]/`)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-389">Check out the URL where the application started and browse to that URL with the phone browser (e.g. `http://localhost:[PortNumber]/`).</span></span>

    <span data-ttu-id="27d1d-390">您将注意到如 jQuery.Mobile.MVC 具有显示针对移动设备优化的视图在项目中创建新的资产，看起来你的应用程序在 Windows Phone 模拟器中，不同。</span><span class="sxs-lookup"><span data-stu-id="27d1d-390">You will notice that your application will look different in the Windows Phone emulator, as the jQuery.Mobile.MVC has created new assets in your project that show views optimized for mobile devices.</span></span>

    <span data-ttu-id="27d1d-391">请注意，显示将切换到桌面视图的链接，手机顶部的消息。</span><span class="sxs-lookup"><span data-stu-id="27d1d-391">Notice the message at the top of the phone, showing the link that switches to the Desktop view.</span></span> <span data-ttu-id="27d1d-392">此外，  **\_Layout.Mobile.cshtml**已创建的已安装的包的布局应用程序中包含不同的布局。</span><span class="sxs-lookup"><span data-stu-id="27d1d-392">Additionally, the **\_Layout.Mobile.cshtml** layout that was created by the package you have installed is including a different layout in the application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27d1d-393">到目前为止，没有链接以返回到移动视图。</span><span class="sxs-lookup"><span data-stu-id="27d1d-393">So far, there is no link to get back to mobile view.</span></span> <span data-ttu-id="27d1d-394">它将包含在更高版本。</span><span class="sxs-lookup"><span data-stu-id="27d1d-394">It will be included in later versions.</span></span>

    <span data-ttu-id="27d1d-395">![照片库主页上的移动视图](whats-new-in-aspnet-mvc-4/_static/image24.png "照片库主页上的移动视图")</span><span class="sxs-lookup"><span data-stu-id="27d1d-395">![Mobile view of the Photo Gallery Home page](whats-new-in-aspnet-mvc-4/_static/image24.png "Mobile view of the Photo Gallery Home page")</span></span>

    <span data-ttu-id="27d1d-396">*照片库主页上的移动视图*</span><span class="sxs-lookup"><span data-stu-id="27d1d-396">*Mobile view of the Photo Gallery Home page*</span></span>
8. <span data-ttu-id="27d1d-397">在 Visual Studio 中，按**SHIFT** + **F5**以停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-397">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a><span data-ttu-id="27d1d-398">任务 2-创建移动视图</span><span class="sxs-lookup"><span data-stu-id="27d1d-398">Task 2 - Creating Mobile Views</span></span>

<span data-ttu-id="27d1d-399">在此任务中，将改写，以便进行更好地 appareance 在移动设备中的内容创建索引视图的移动版本。</span><span class="sxs-lookup"><span data-stu-id="27d1d-399">In this task, you will create a mobile version of the index view with content adapted for better appareance in mobile devices.</span></span>

1. <span data-ttu-id="27d1d-400">复制**Views\Home\Index.cshtml**查看并将其创建副本、 重命名的新文件粘贴**Index.Mobile.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-400">Copy the **Views\Home\Index.cshtml** view and paste it to create a copy, rename the new file to **Index.Mobile.cshtml**.</span></span>
2. <span data-ttu-id="27d1d-401">打开新创建**Index.Mobile.cshtml**查看和替换现有&lt;ul&gt;标记，此代码。</span><span class="sxs-lookup"><span data-stu-id="27d1d-401">Open the new created **Index.Mobile.cshtml** view and replace the existing &lt;ul&gt; tag with this code.</span></span> <span data-ttu-id="27d1d-402">通过执行此操作，你将更新&lt;ul&gt; jQuery 移动数据批注，以使用从 jQuery 移动主题的标记。</span><span class="sxs-lookup"><span data-stu-id="27d1d-402">By doing this, you will be updating the &lt;ul&gt; tag with jQuery Mobile data annotations to use the mobile themes from jQuery.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > <span data-ttu-id="27d1d-403">请注意：</span><span class="sxs-lookup"><span data-stu-id="27d1d-403">Notice that:</span></span>
    > 
    > - <span data-ttu-id="27d1d-404">**数据角色**属性设置为**listview**将呈现使用 listview 样式的列表。</span><span class="sxs-lookup"><span data-stu-id="27d1d-404">The **data-role** attribute set to **listview** will render the list using the listview styles.</span></span>
    > 
    > - <span data-ttu-id="27d1d-405">**数据嵌入**属性设置为 true 会显示带圆角的边框和边距的列表。</span><span class="sxs-lookup"><span data-stu-id="27d1d-405">The **data-inset** attribute set to true will show the list with rounded border and margin.</span></span>
    > 
    > - <span data-ttu-id="27d1d-406">**数据筛选器**属性设置为**true**将生成一个搜索框。</span><span class="sxs-lookup"><span data-stu-id="27d1d-406">The **data-filter** attribute set to **true** will generate a search box.</span></span>
    > 
    > <span data-ttu-id="27d1d-407">您可以了解有关项目文档中的 jQuery 移动约定的详细信息： [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span><span class="sxs-lookup"><span data-stu-id="27d1d-407">You can learn more about jQuery Mobile conventions in the project documentation: [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span></span>
3. <span data-ttu-id="27d1d-408">按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="27d1d-408">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="27d1d-409">切换到**Windows Phone 仿真程序**和刷新站点。</span><span class="sxs-lookup"><span data-stu-id="27d1d-409">Switch to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="27d1d-410">请注意，新的外观和感觉的库列表中，以及新的搜索框右上角。</span><span class="sxs-lookup"><span data-stu-id="27d1d-410">Notice the new look and feel of the gallery list, as well as the new search box located on the top.</span></span> <span data-ttu-id="27d1d-411">然后，在搜索框中键入一个词 (例如， **Tulips**) 才能启动照片库中搜索。</span><span class="sxs-lookup"><span data-stu-id="27d1d-411">Then, type a word in the search box (for instance, **Tulips**) to start a search in the photo gallery.</span></span>

    <span data-ttu-id="27d1d-412">![库使用筛选使用 listview 样式](whats-new-in-aspnet-mvc-4/_static/image25.png "库使用筛选使用 listview 样式")</span><span class="sxs-lookup"><span data-stu-id="27d1d-412">![Gallery using listview style with filtering](whats-new-in-aspnet-mvc-4/_static/image25.png "Gallery using listview style with filtering")</span></span>

    <span data-ttu-id="27d1d-413">*使用筛选使用 listview 样式的库*</span><span class="sxs-lookup"><span data-stu-id="27d1d-413">*Gallery using listview style with filtering*</span></span>

    <span data-ttu-id="27d1d-414">总之，具有使用该视图可持续方案创建索引视图中处理的副本&quot;移动&quot;后缀。</span><span class="sxs-lookup"><span data-stu-id="27d1d-414">To summarize, you have used the View Mobilizer recipe to create a copy of the Index view with the &quot;mobile&quot; suffix.</span></span> <span data-ttu-id="27d1d-415">此后缀指示到 ASP.NET MVC 4 移动设备生成的每个请求将使用此副本的索引。</span><span class="sxs-lookup"><span data-stu-id="27d1d-415">This suffix indicates to ASP.NET MVC 4 that every request generated from a mobile device will use this copy of the index.</span></span> <span data-ttu-id="27d1d-416">此外，您已更新索引视图，以增强站点外观和感觉在移动设备中使用 jQuery Mobile 的移动的版本。</span><span class="sxs-lookup"><span data-stu-id="27d1d-416">Additionally, you have updated the mobile version of the Index view to use jQuery Mobile for enhancing the site look and feel in mobile devices.</span></span>
5. <span data-ttu-id="27d1d-417">返回到 Visual Studio 并打开**Site.Mobile.css**位于**内容**文件夹。</span><span class="sxs-lookup"><span data-stu-id="27d1d-417">Go back to Visual Studio and open **Site.Mobile.css** located under the **Content** folder.</span></span>
6. <span data-ttu-id="27d1d-418">修复照片标题，以使其显示在右侧的图像的位置。</span><span class="sxs-lookup"><span data-stu-id="27d1d-418">Fix the positioning of the photo title to make it show at the right side of the image.</span></span> <span data-ttu-id="27d1d-419">若要执行此操作，以下代码添加到**Site.Mobile.css**文件。</span><span class="sxs-lookup"><span data-stu-id="27d1d-419">To do this, add the following code to the **Site.Mobile.css** file.</span></span>

    <span data-ttu-id="27d1d-420">CSS</span><span class="sxs-lookup"><span data-stu-id="27d1d-420">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. <span data-ttu-id="27d1d-421">按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="27d1d-421">Press **CTRL + S** to save the changes.</span></span>
8. <span data-ttu-id="27d1d-422">切换回**Windows Phone 仿真程序**和刷新站点。</span><span class="sxs-lookup"><span data-stu-id="27d1d-422">Switch back to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="27d1d-423">请注意，现在可恰当地定位照片标题。</span><span class="sxs-lookup"><span data-stu-id="27d1d-423">Notice the photo title is properly positioned now.</span></span>

    <span data-ttu-id="27d1d-424">![标题位于图像的右侧](whats-new-in-aspnet-mvc-4/_static/image26.png "定位在图像的右侧上的标题")</span><span class="sxs-lookup"><span data-stu-id="27d1d-424">![Title positioned on the right side of the image](whats-new-in-aspnet-mvc-4/_static/image26.png "Title positioned on the right side of the image")</span></span>

    <span data-ttu-id="27d1d-425">*定位在图像的右侧上的标题*</span><span class="sxs-lookup"><span data-stu-id="27d1d-425">*Title positioned on the right side of the image*</span></span>

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a><span data-ttu-id="27d1d-426">任务 3-jQuery Mobile 主题</span><span class="sxs-lookup"><span data-stu-id="27d1d-426">Task 3 - jQuery Mobile Themes</span></span>

<span data-ttu-id="27d1d-427">每个布局和小组件中的 jQuery Mobile 被针对新的面向对象的 CSS 框架，利用它可以将完整统一的可视化设计主题应用到站点和应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-427">Every layout and widget in jQuery Mobile is designed around a new object-oriented CSS framework that makes it possible to apply a complete unified visual design theme to sites and applications.</span></span>

<span data-ttu-id="27d1d-428">jQuery Mobile 的默认主题包括 5 个样本指定字母 (a、 b、 c、 d、 e） 的快速参考。</span><span class="sxs-lookup"><span data-stu-id="27d1d-428">jQuery Mobile's default Theme includes 5 swatches that are given letters (a, b, c, d, e) for quick reference.</span></span>

<span data-ttu-id="27d1d-429">在本任务中，你将更新要使用不同的主题，而不是默认的移动布局。</span><span class="sxs-lookup"><span data-stu-id="27d1d-429">In this task, you will update the mobile layout to use a different theme than the default.</span></span>

1. <span data-ttu-id="27d1d-430">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="27d1d-430">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="27d1d-431">打开 **\_Layout.Mobile.cshtml**文件位于**views/shared**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-431">Open the **\_Layout.Mobile.cshtml** file located in **Views\Shared**.</span></span>
3. <span data-ttu-id="27d1d-432">数据角色设置为使用找到的 div 元素&quot;页上&quot;，并更新**数据主题**到&quot; **e**&quot;。</span><span class="sxs-lookup"><span data-stu-id="27d1d-432">Find the div element with the data-role set to &quot;page&quot; and update the **data-theme** to &quot;**e**&quot;.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. <span data-ttu-id="27d1d-433">按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="27d1d-433">Press **CTRL + S** to save the changes.</span></span>
5. <span data-ttu-id="27d1d-434">刷新中的站点**Windows Phone 仿真程序**并留意新的颜色方案。</span><span class="sxs-lookup"><span data-stu-id="27d1d-434">Refresh the site in the **Windows Phone Emulator** and notice the new colors scheme.</span></span>

    <span data-ttu-id="27d1d-435">![使用不同的配色方案的移动布局](whats-new-in-aspnet-mvc-4/_static/image27.png "具有不同的配色方案的移动布局")</span><span class="sxs-lookup"><span data-stu-id="27d1d-435">![Mobile layout with a different color scheme](whats-new-in-aspnet-mvc-4/_static/image27.png "Mobile layout with a different color scheme")</span></span>

    <span data-ttu-id="27d1d-436">*使用不同的配色方案的移动布局*</span><span class="sxs-lookup"><span data-stu-id="27d1d-436">*Mobile layout with a different color scheme*</span></span>

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a><span data-ttu-id="27d1d-437">任务 4-使用视图切换器组件和重写功能的浏览器</span><span class="sxs-lookup"><span data-stu-id="27d1d-437">Task 4 - Using the View-Switcher Component and the Browser Overriding Features</span></span>

<span data-ttu-id="27d1d-438">移动优化 web pages 的约定将添加其文本是如桌面视图或完整的站点模式，使用户切换到桌面版本的页面的链接。</span><span class="sxs-lookup"><span data-stu-id="27d1d-438">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="27d1d-439">JQuery.Mobile.MVC 包包括了示例**视图切换器**组件中使用此目的 **\_Layout.Mobile.cshtml**视图。</span><span class="sxs-lookup"><span data-stu-id="27d1d-439">The jQuery.Mobile.MVC package includes a sample **view-switcher** component for this purpose used in the **\_Layout.Mobile.cshtml** view.</span></span>

<span data-ttu-id="27d1d-440">![若要切换到桌面视图链接](whats-new-in-aspnet-mvc-4/_static/image28.png "链接以切换到桌面视图")</span><span class="sxs-lookup"><span data-stu-id="27d1d-440">![Link to switch to Desktop View](whats-new-in-aspnet-mvc-4/_static/image28.png "Link to switch to Desktop View")</span></span>

<span data-ttu-id="27d1d-441">*链接以切换到桌面视图*</span><span class="sxs-lookup"><span data-stu-id="27d1d-441">*Link to switch to Desktop View*</span></span>

<span data-ttu-id="27d1d-442">视图切换器使用名为的新功能**浏览器重写**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-442">The view switcher uses a new feature called **Browser Overriding**.</span></span> <span data-ttu-id="27d1d-443">此功能允许将请求视为其视为来自其他浏览器 （用户代理） 比它们实际来自你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-443">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they are actually coming from.</span></span>

<span data-ttu-id="27d1d-444">在此任务中，您将了解通过 jQuery.Mobile.MVC 和新浏览器中重写功能在 ASP.NET MVC 4 中添加的视图切换器的示例实现。</span><span class="sxs-lookup"><span data-stu-id="27d1d-444">In this task, you will explore the sample implementation of a view-switcher added by jQuery.Mobile.MVC and the new browser overriding features in ASP.NET MVC 4.</span></span>

1. <span data-ttu-id="27d1d-445">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="27d1d-445">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="27d1d-446">打开 **\_Layout.Mobile.cshtml**视图位于下**views/shared**文件夹，注意为分部视图所引用的视图切换器组件。</span><span class="sxs-lookup"><span data-stu-id="27d1d-446">Open the **\_Layout.Mobile.cshtml** view located under the **Views\Shared** folder and notice the view-switcher component being referenced as a partial view.</span></span>

    <span data-ttu-id="27d1d-447">![使用视图切换器组件的移动布局](whats-new-in-aspnet-mvc-4/_static/image29.png "使用视图切换器组件的移动布局")</span><span class="sxs-lookup"><span data-stu-id="27d1d-447">![Mobile layout using View-Switcher component](whats-new-in-aspnet-mvc-4/_static/image29.png "Mobile layout using View-Switcher component")</span></span>

    <span data-ttu-id="27d1d-448">*使用视图切换器组件的移动布局*</span><span class="sxs-lookup"><span data-stu-id="27d1d-448">*Mobile layout using View-Switcher component*</span></span>
3. <span data-ttu-id="27d1d-449">打开 **\_ViewSwitcher.cshtml**分部视图。</span><span class="sxs-lookup"><span data-stu-id="27d1d-449">Open the **\_ViewSwitcher.cshtml** partial view.</span></span>

    <span data-ttu-id="27d1d-450">分部视图使用的新方法**ViewContext.HttpContext.GetOverriddenBrowser()** 来确定 web 请求的来源并显示相应的链接以切换到桌面或移动视图。</span><span class="sxs-lookup"><span data-stu-id="27d1d-450">The partial view uses the new method **ViewContext.HttpContext.GetOverriddenBrowser()** to determine the origin of the web request and show the corresponding link to switch either to the Desktop or Mobile views.</span></span>

    <span data-ttu-id="27d1d-451">**GetOverridenBrowser**方法将返回**HttpBrowserCapabilitiesBase**对应于当前设置为请求的用户代理的实例 （实际或重写）。</span><span class="sxs-lookup"><span data-stu-id="27d1d-451">The **GetOverridenBrowser** method returns an **HttpBrowserCapabilitiesBase** instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="27d1d-452">可以使用此值来获取属性，如**IsMobileDevice**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-452">You can use this value to get properties such as **IsMobileDevice**.</span></span>

    <span data-ttu-id="27d1d-453">![ViewSwitcher 分部视图](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 分部视图")</span><span class="sxs-lookup"><span data-stu-id="27d1d-453">![ViewSwitcher partial view](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher partial view")</span></span>

    <span data-ttu-id="27d1d-454">*ViewSwitcher 分部视图*</span><span class="sxs-lookup"><span data-stu-id="27d1d-454">*ViewSwitcher partial view*</span></span>
4. <span data-ttu-id="27d1d-455">打开**ViewSwitcherController.cs**类位于**控制器**文件夹。</span><span class="sxs-lookup"><span data-stu-id="27d1d-455">Open the **ViewSwitcherController.cs** class located in the **Controllers** folder.</span></span> <span data-ttu-id="27d1d-456">签出该 SwitchView 操作由 ViewSwitcher 组件中的链接，请注意，新的 HttpContext 方法。</span><span class="sxs-lookup"><span data-stu-id="27d1d-456">Check out that SwitchView action is called by the link in the ViewSwitcher component, and notice the new HttpContext methods.</span></span>

    - <span data-ttu-id="27d1d-457">**HttpContext.ClearOverridenBrowser()** 方法移除当前请求的任何重写的用户代理。</span><span class="sxs-lookup"><span data-stu-id="27d1d-457">The **HttpContext.ClearOverridenBrowser()** method removes any overridden user agent for the current request.</span></span>
    - <span data-ttu-id="27d1d-458">**HttpContext.SetOverridenBrowser()** 方法重写请求的实际用户代理值使用指定的用户代理。</span><span class="sxs-lookup"><span data-stu-id="27d1d-458">The **HttpContext.SetOverridenBrowser()** method overrides the request's actual user agent value using the specified user agent.</span></span>  
        <span data-ttu-id="27d1d-459">![ViewSwitcher 控制器](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher 控制器")</span><span class="sxs-lookup"><span data-stu-id="27d1d-459">![ViewSwitcher Controller](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher Controller")</span></span>  
<span data-ttu-id="27d1d-460">*ViewSwitcher 控制器*</span><span class="sxs-lookup"><span data-stu-id="27d1d-460">*ViewSwitcher Controller*</span></span>

        <span data-ttu-id="27d1d-461">浏览器重写是一项核心功能的 ASP.NET MVC 4 中，即使不安装 jQuery.Mobile.MVC 包，这是也可用。</span><span class="sxs-lookup"><span data-stu-id="27d1d-461">Browser Overriding is a core feature of ASP.NET MVC 4, which is also available even if you do not install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="27d1d-462">但是，此功能会影响视图、 布局和分部视图，并且它不影响任何依赖于 Request.Browser 对象的功能。</span><span class="sxs-lookup"><span data-stu-id="27d1d-462">However, this feature affects only view, layout, and partial-view, and it does not affect any of the features that depend on the Request.Browser object.</span></span>

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a><span data-ttu-id="27d1d-463">任务 5-在桌面视图中添加视图切换器</span><span class="sxs-lookup"><span data-stu-id="27d1d-463">Task 5 - Adding the View-Switcher in the Desktop View</span></span>

<span data-ttu-id="27d1d-464">在此任务中，你将更新以包括视图切换器的桌面布局。</span><span class="sxs-lookup"><span data-stu-id="27d1d-464">In this task, you will update the desktop layout to include the view-switcher.</span></span> <span data-ttu-id="27d1d-465">这将允许移动用户返回到移动视图，浏览桌面视图时。</span><span class="sxs-lookup"><span data-stu-id="27d1d-465">This will allow mobile users to go back to the mobile view when browsing the desktop view.</span></span>

1. <span data-ttu-id="27d1d-466">刷新中的站点**Windows Phone 仿真程序**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-466">Refresh the site in the **Windows Phone Emulator**.</span></span>
2. <span data-ttu-id="27d1d-467">单击**桌面视图**库顶部的链接。</span><span class="sxs-lookup"><span data-stu-id="27d1d-467">Click on the **Desktop view** link at the top of the gallery.</span></span> <span data-ttu-id="27d1d-468">请注意在桌面视图以便返回到移动视图中没有任何视图切换器。</span><span class="sxs-lookup"><span data-stu-id="27d1d-468">Notice there is no view-switcher in the desktop view to allow you return to the mobile view.</span></span>
3. <span data-ttu-id="27d1d-469">返回到 Visual Studio 并打开 **\_Layout.cshtml**视图。</span><span class="sxs-lookup"><span data-stu-id="27d1d-469">Go back to Visual Studio and open the **\_Layout.cshtml** view.</span></span>
4. <span data-ttu-id="27d1d-470">找到登录节，插入的调用来呈现 **\_ViewSwitcher**下面的分部视图 **\_LogOnPartial**分部视图。</span><span class="sxs-lookup"><span data-stu-id="27d1d-470">Find the login section and insert a call to render the **\_ViewSwitcher** partial view below the **\_LogOnPartial** partial view.</span></span> <span data-ttu-id="27d1d-471">然后，按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="27d1d-471">Then, press **CTRL + S** to save the changes.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. <span data-ttu-id="27d1d-472">按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="27d1d-472">Press **CTRL + S** to save the changes.</span></span>
6. <span data-ttu-id="27d1d-473">Windows Phone 仿真程序中刷新页面，然后双击要放大的屏幕。</span><span class="sxs-lookup"><span data-stu-id="27d1d-473">Refresh the page in the Windows Phone Emulator and double-click the screen to zoom in.</span></span> <span data-ttu-id="27d1d-474">请注意，现在显示主页页面**移动视图**从移动视图切换到桌面视图的链接。</span><span class="sxs-lookup"><span data-stu-id="27d1d-474">Notice that the home page now shows the **Mobile view** link that switches from mobile to desktop view.</span></span>

    <span data-ttu-id="27d1d-475">![查看切换器在桌面视图中呈现](whats-new-in-aspnet-mvc-4/_static/image32.png "桌面视图中呈现的视图切换器")</span><span class="sxs-lookup"><span data-stu-id="27d1d-475">![View Switcher rendered in desktop view](whats-new-in-aspnet-mvc-4/_static/image32.png "View Switcher rendered in desktop view")</span></span>

    <span data-ttu-id="27d1d-476">*在桌面视图中呈现的视图切换器*</span><span class="sxs-lookup"><span data-stu-id="27d1d-476">*View Switcher rendered in desktop view*</span></span>
7. <span data-ttu-id="27d1d-477">再次切换到移动视图，然后浏览到<strong>有关</strong>页 (http://localhost[端口] / Home/有关)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-477">Switch to the Mobile view again and browse to <strong>About</strong> page (http://localhost[port]/Home/About).</span></span> <span data-ttu-id="27d1d-478">请注意，即使尚未创建 About.Mobile.cshtml 视图，关于页面将显示使用移动布局 (\_Layout.Mobile.cshtml)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-478">Notice that, even if you haven't created an About.Mobile.cshtml view, the About page is displayed using the mobile layout (\_Layout.Mobile.cshtml).</span></span>

    <span data-ttu-id="27d1d-479">![有关页面](whats-new-in-aspnet-mvc-4/_static/image33.png "有关页面")</span><span class="sxs-lookup"><span data-stu-id="27d1d-479">![About page](whats-new-in-aspnet-mvc-4/_static/image33.png "About page")</span></span>

    <span data-ttu-id="27d1d-480">*有关页*</span><span class="sxs-lookup"><span data-stu-id="27d1d-480">*About page*</span></span>
8. <span data-ttu-id="27d1d-481">最后，桌面 Web 浏览器中打开的网站。</span><span class="sxs-lookup"><span data-stu-id="27d1d-481">Finally, open the site in a desktop Web browser.</span></span> <span data-ttu-id="27d1d-482">请注意，没有任何以前的更新具有影响桌面视图。</span><span class="sxs-lookup"><span data-stu-id="27d1d-482">Notice that none of the previous updates has affected the desktop view.</span></span>

    <span data-ttu-id="27d1d-483">![图片库桌面视图](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery 桌面视图")</span><span class="sxs-lookup"><span data-stu-id="27d1d-483">![PhotoGallery desktop view](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery desktop view")</span></span>

    <span data-ttu-id="27d1d-484">*图片库桌面视图*</span><span class="sxs-lookup"><span data-stu-id="27d1d-484">*PhotoGallery desktop view*</span></span>

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a><span data-ttu-id="27d1d-485">任务 6-创建新的显示模式</span><span class="sxs-lookup"><span data-stu-id="27d1d-485">Task 6 - Creating New Display Modes</span></span>

<span data-ttu-id="27d1d-486">新的显示模式功能，支持应用程序选择具体取决于生成请求的浏览器的视图。</span><span class="sxs-lookup"><span data-stu-id="27d1d-486">The new display modes feature lets an application select views depending on the browser that is generating the request.</span></span> <span data-ttu-id="27d1d-487">例如，如果桌面浏览器主页发送请求，应用程序将返回**Views\Home\Index.cshtml**模板。</span><span class="sxs-lookup"><span data-stu-id="27d1d-487">For example, if a desktop browser requests the Home page, the application will return the **Views\Home\Index.cshtml** template.</span></span> <span data-ttu-id="27d1d-488">然后，如果在移动浏览器主页发送请求，应用程序将返回**Views\Home\Index.mobile.cshtml**模板。</span><span class="sxs-lookup"><span data-stu-id="27d1d-488">Then, if a mobile browser requests the Home page, the application will return the **Views\Home\Index.mobile.cshtml** template.</span></span>

<span data-ttu-id="27d1d-489">在此任务中，您将创建适用于 iPhone 设备的自定义的布局和必须模拟从 iPhone 设备的请求。</span><span class="sxs-lookup"><span data-stu-id="27d1d-489">In this task, you will create a customized layout for iPhone devices, and you will have to simulate requests from iPhone devices.</span></span> <span data-ttu-id="27d1d-490">若要执行此操作，可以使用任一 iPhone 仿真器/模拟器 (例如[电力移动模拟器](http://www.electricplum.com/)) 或修改用户代理的外接程序的浏览器。</span><span class="sxs-lookup"><span data-stu-id="27d1d-490">To do this, you can use either an iPhone emulator/simulator (like [Electric Mobile Simulator](http://www.electricplum.com/)) or a browser with add-ons that modify the user agent.</span></span> <span data-ttu-id="27d1d-491">有关如何在 Safari 浏览器中设置的用户代理字符串以模拟 iPhone 的说明，请参阅[如何让 Safari 模拟 IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)中 David Alison 的博文。</span><span class="sxs-lookup"><span data-stu-id="27d1d-491">For instructions on how to set the user agent string in an Safari browser to emulate an iPhone, see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) in David Alison's blog.</span></span>

<span data-ttu-id="27d1d-492">**请注意，此任务是可选的可以在整个实验室继续而不执行它。**</span><span class="sxs-lookup"><span data-stu-id="27d1d-492">**Notice that this task is optional and you can continue throughout the lab without executing it.**</span></span>

1. <span data-ttu-id="27d1d-493">在 Visual Studio 中，按**SHIFT** + **F5**以停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-493">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="27d1d-494">打开**Global.asax.cs**并添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="27d1d-494">Open **Global.asax.cs** and add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. <span data-ttu-id="27d1d-495">将以下突出显示的代码添加到应用程序\_Start 方法。</span><span class="sxs-lookup"><span data-stu-id="27d1d-495">Add the following highlighted code into the Application\_Start method.</span></span>

    <span data-ttu-id="27d1d-496">(代码段- *ASP.NET MVC 4 实验室-Ex03-iPhone DisplayMode*)</span><span class="sxs-lookup"><span data-stu-id="27d1d-496">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - iPhone DisplayMode*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

<span data-ttu-id="27d1d-497">已注册的新**名为为 DefaultDisplayMode &quot;iPhone&quot;** 中静态, **DisplayModeProvider.Instance.Modes**静态列表中，将针对匹配每个传入请求。</span><span class="sxs-lookup"><span data-stu-id="27d1d-497">You have registered a new **DefaultDisplayMode named &quot;iPhone&quot;**, within the static **DisplayModeProvider.Instance.Modes** static list, that will be matched against each incoming request.</span></span> <span data-ttu-id="27d1d-498">如果传入请求包含字符串&quot;iPhone&quot;，ASP.NET MVC 将查找其名称包含的视图&quot;iPhone&quot;后缀。</span><span class="sxs-lookup"><span data-stu-id="27d1d-498">If the incoming request contains the string &quot;iPhone&quot;, ASP.NET MVC will find the views whose name contain the &quot;iPhone&quot; suffix.</span></span> <span data-ttu-id="27d1d-499">0 的参数指示如何特定是新的模式;例如，此视图是比常规更具体&quot;.mobile&quot;匹配请求从移动设备的规则。</span><span class="sxs-lookup"><span data-stu-id="27d1d-499">The 0 parameter indicates how specific is the new mode; for instance, this view is more specific than the general &quot;.mobile&quot; rule that matches requests from mobile devices.</span></span>

<span data-ttu-id="27d1d-500">此代码运行，iPhone 浏览器将生成请求后，将使用你的应用程序**views/shared\\_Layout.iPhone.cshtml**将在下一步骤中创建的布局。</span><span class="sxs-lookup"><span data-stu-id="27d1d-500">After this code runs, when an iPhone browser generates a request, your application will use the **Views\Shared\\_Layout.iPhone.cshtml** layout you will create in the next steps.</span></span>

> [!NOTE]
> <span data-ttu-id="27d1d-501">测试请求的 iPhone 简化出于演示目的，并且可能无法按预期的每个 iPhone 用户代理字符串 （对应于示例测试是区分大小写） 的这种方式。</span><span class="sxs-lookup"><span data-stu-id="27d1d-501">This way of testing the request for iPhone has been simplified for demo purposes and might not work as expected for every iPhone user agent string (for example test is case sensitive).</span></span>

4. <span data-ttu-id="27d1d-502">创建一份 **\_Layout.Mobile.cshtml**中的文件**views/shared**文件夹并将复制到重命名&quot;  **\_Layout.iPhone.csthml**&quot;.</span><span class="sxs-lookup"><span data-stu-id="27d1d-502">Create a copy of the **\_Layout.Mobile.cshtml** file in the **Views\Shared** folder and rename the copy to &quot;**\_Layout.iPhone.csthml**&quot;.</span></span>
5. <span data-ttu-id="27d1d-503">打开 **\_Layout.iPhone.csthml**在上一步中创建。</span><span class="sxs-lookup"><span data-stu-id="27d1d-503">Open **\_Layout.iPhone.csthml** you created in the previous step.</span></span>
6. <span data-ttu-id="27d1d-504">数据角色属性设置为使用找到的 div 元素**页上**并将更改**数据主题**归于&quot; &quot;。</span><span class="sxs-lookup"><span data-stu-id="27d1d-504">Find the div element with the data-role attribute set to **page** and change the **data-theme** attribute to &quot;**a**&quot;.</span></span>


[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

<span data-ttu-id="27d1d-505">现在在 ASP.NET MVC 4 应用程序中有 3 个布局：</span><span class="sxs-lookup"><span data-stu-id="27d1d-505">Now you have 3 layouts in your ASP.NET MVC 4 application:</span></span>

1. <span data-ttu-id="27d1d-506">**\_Layout.cshtml**： 对于桌面浏览器所使用的默认布局。</span><span class="sxs-lookup"><span data-stu-id="27d1d-506">**\_Layout.cshtml**: default layout used for desktop browsers.</span></span>
2. <span data-ttu-id="27d1d-507">**\_Layout.mobile.cshtml**： 为移动设备所使用的默认布局。</span><span class="sxs-lookup"><span data-stu-id="27d1d-507">**\_Layout.mobile.cshtml**: default layout used for mobile devices.</span></span>
3. <span data-ttu-id="27d1d-508">**\_Layout.iPhone.cshtml**： 适用于 iPhone 设备，使用不同的配色方案来区分从特定布局\_Layout.mobile.cshtml。</span><span class="sxs-lookup"><span data-stu-id="27d1d-508">**\_Layout.iPhone.cshtml**: specific layout for iPhone devices, using a different color scheme to differentiate from \_Layout.mobile.cshtml.</span></span>
7. <span data-ttu-id="27d1d-509">按**F5**运行该应用程序和浏览中的站点**Windows Phone 仿真程序**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-509">Press **F5** to run the application and browse the site in the **Windows Phone Emulator**.</span></span>
8. <span data-ttu-id="27d1d-510">打开**iPhone 模拟器**(请参阅[附录 C](#AppendixC)有关如何安装和配置 iPhone 模拟器的说明)，并浏览到该网站太。</span><span class="sxs-lookup"><span data-stu-id="27d1d-510">Open an **iPhone simulator** (see [Appendix C](#AppendixC) for instructions on how to install and configure an iPhone simulator), and browse to the site too.</span></span> <span data-ttu-id="27d1d-511">请注意，每个电话使用特定的模板。</span><span class="sxs-lookup"><span data-stu-id="27d1d-511">Notice that each phone is using the specific template.</span></span>

    ![Using-different-views-for-each-mobile-device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    <span data-ttu-id="27d1d-513">*对于每个移动设备使用不同的视图*</span><span class="sxs-lookup"><span data-stu-id="27d1d-513">*Using different views for each mobile device*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a><span data-ttu-id="27d1d-514">练习 4： 使用异步控制器</span><span class="sxs-lookup"><span data-stu-id="27d1d-514">Exercise 4: Using Asynchronous Controllers</span></span>

<span data-ttu-id="27d1d-515">Microsoft.NET Framework 4.5 引入了 C# 和 Visual Basic 中为.NET 编程中的异步功能提供新的基础的新语言功能。</span><span class="sxs-lookup"><span data-stu-id="27d1d-515">Microsoft .NET Framework 4.5 introduces new language features in C# and Visual Basic to provide a new foundation for asynchrony in .NET programming.</span></span> <span data-ttu-id="27d1d-516">此新基础使异步编程，类似于-和大约为-同步编程一样简单。</span><span class="sxs-lookup"><span data-stu-id="27d1d-516">This new foundation makes asynchronous programming similar to - and about as straightforward as - synchronous programming.</span></span> <span data-ttu-id="27d1d-517">你现可使用在 ASP.NET MVC 4 中编写异步操作方法**AsyncController**类。</span><span class="sxs-lookup"><span data-stu-id="27d1d-517">You are now able to write asynchronous action methods in ASP.NET MVC 4 by using the **AsyncController** class.</span></span> <span data-ttu-id="27d1d-518">用于长时间运行的异步操作方法、 非 CPU 绑定的请求。</span><span class="sxs-lookup"><span data-stu-id="27d1d-518">You can use asynchronous action methods for long-running, non-CPU bound requests.</span></span> <span data-ttu-id="27d1d-519">这样可避免阻止 Web 服务器在处理请求时执行工作。</span><span class="sxs-lookup"><span data-stu-id="27d1d-519">This avoids blocking the Web server from performing work while the request is being processed.</span></span> <span data-ttu-id="27d1d-520">AsyncController 类通常用于长时间运行的 Web 服务调用。</span><span class="sxs-lookup"><span data-stu-id="27d1d-520">The AsyncController class is typically used for long-running Web service calls.</span></span>

<span data-ttu-id="27d1d-521">本练习中介绍了 ASP.NET MVC 4 中的异步操作的基础知识。</span><span class="sxs-lookup"><span data-stu-id="27d1d-521">This exercise explains the basics of asynchronous operation in ASP.NET MVC 4.</span></span> <span data-ttu-id="27d1d-522">如果您希望更深入的了解，可以查看以下文章： [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="27d1d-522">If you want a deeper dive, you can check out the following article: [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span></span>

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a><span data-ttu-id="27d1d-523">任务 1-实现异步控制器</span><span class="sxs-lookup"><span data-stu-id="27d1d-523">Task 1 - Implementing an Asynchronous Controller</span></span>

1. <span data-ttu-id="27d1d-524">打开**开始**解决方案位于**源/Ex4-Async/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="27d1d-524">Open the **Begin** solution located at **Source/Ex4-Async/Begin/** folder.</span></span> <span data-ttu-id="27d1d-525">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="27d1d-525">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="27d1d-526">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="27d1d-526">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="27d1d-527">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-527">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="27d1d-528">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="27d1d-528">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="27d1d-529">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-529">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="27d1d-530">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="27d1d-530">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="27d1d-531">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="27d1d-531">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="27d1d-532">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="27d1d-532">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="27d1d-533">打开**HomeController.cs**类派生**控制器**文件夹。</span><span class="sxs-lookup"><span data-stu-id="27d1d-533">Open the **HomeController.cs** class from the **Controllers** folder.</span></span>
3. <span data-ttu-id="27d1d-534">添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="27d1d-534">Add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. <span data-ttu-id="27d1d-535">更新**HomeController**类继承自**AsyncController**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-535">Update the **HomeController** class to inherit from **AsyncController**.</span></span> <span data-ttu-id="27d1d-536">派生自 AsyncController 控制器使 ASP.NET 能够处理异步请求，并且它们仍可以服务同步操作方法。</span><span class="sxs-lookup"><span data-stu-id="27d1d-536">Controllers that derive from AsyncController enable ASP.NET to process asynchronous requests, and they can still service synchronous action methods.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. <span data-ttu-id="27d1d-537">添加**异步**关键字**索引**方法，并使其返回类型**任务&lt;ActionResult&gt;**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-537">Add the **async** keyword to the **Index** method and make it return the type **Task&lt;ActionResult&gt;**.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > <span data-ttu-id="27d1d-538">**异步**关键字是一个.NET Framework 4.5 提供了新的关键字; 它会告知编译器，此方法包含异步代码。</span><span class="sxs-lookup"><span data-stu-id="27d1d-538">The **async** keyword is one of the new keywords the .NET Framework 4.5 provides; it tells the compiler that this method contains asynchronous code.</span></span> <span data-ttu-id="27d1d-539">一个**任务**对象都表示可能在将来某个时刻完成的异步操作。</span><span class="sxs-lookup"><span data-stu-id="27d1d-539">A **Task** object represents an asynchronous operation that may complete at some point in the future.</span></span>
6. <span data-ttu-id="27d1d-540">替换为**客户端。GetAsync()** 调用与使用完整的异步版本，如下所示的 await 关键字。</span><span class="sxs-lookup"><span data-stu-id="27d1d-540">Replace the **client.GetAsync()** call with the full async version using await keyword as shown below.</span></span>

    <span data-ttu-id="27d1d-541">(代码段- *ASP.NET MVC 4 实验室-Ex04-GetAsync*)</span><span class="sxs-lookup"><span data-stu-id="27d1d-541">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - GetAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="27d1d-542">在上一版本中，使用**结果**属性从**任务**对象来阻止线程，直到结果为返回 （同步版本）。</span><span class="sxs-lookup"><span data-stu-id="27d1d-542">In the previous version, you were using the **Result** property from the **Task** object to block the thread until the result is returned (sync version).</span></span>
    > 
    > <span data-ttu-id="27d1d-543">添加**await**关键字告知编译器以异步方式等待方法调用返回的任务。</span><span class="sxs-lookup"><span data-stu-id="27d1d-543">Adding the **await** keyword tells the compiler to asynchronously wait for the task returned from the method call.</span></span> <span data-ttu-id="27d1d-544">这意味着仅等待的方法完成后将为以回调形式执行代码的其余部分。</span><span class="sxs-lookup"><span data-stu-id="27d1d-544">This means that the rest of the code will be executed as a callback only after the awaited method completes.</span></span> <span data-ttu-id="27d1d-545">需要注意的另一件事情是您不需要更改的 try-catch 块，以实现此目的： 中背景或前景中发生的异常都仍被捕获，而无需使用处理程序框架提供的任何额外工作。</span><span class="sxs-lookup"><span data-stu-id="27d1d-545">Another thing to notice is that you do not need to change your try-catch block in order to make this work: the exceptions that happen in background or in foreground will still be caught without any extra work using a handler provided by the framework.</span></span>
7. <span data-ttu-id="27d1d-546">更改代码以继续进行异步实现通过将行替换为对新代码，如下所示</span><span class="sxs-lookup"><span data-stu-id="27d1d-546">Change the code to continue with the asynchronous implementation by replacing the lines with the new code as shown below</span></span>

    <span data-ttu-id="27d1d-547">(代码段- *ASP.NET MVC 4 实验室-Ex04-ReadAsStringAsync*)</span><span class="sxs-lookup"><span data-stu-id="27d1d-547">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - ReadAsStringAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. <span data-ttu-id="27d1d-548">运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-548">Run the application.</span></span> <span data-ttu-id="27d1d-549">你会注意到没有较大的变化，但你的代码不会阻止来自线程池使服务器资源的更好地使用并提高性能的线程。</span><span class="sxs-lookup"><span data-stu-id="27d1d-549">You will notice no major changes, but your code will not block a thread from the thread pool making a better usage of the server resources and improving performance.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27d1d-550">您可以了解有关在实验室中的新异步编程功能的详细信息&quot;**中使用 C# 和 Visual Basic.NET 4.5 的异步编程**&quot;包含在 Visual Studio 培训工具包。</span><span class="sxs-lookup"><span data-stu-id="27d1d-550">You can learn more about the new asynchronous programming features in the lab &quot;**Asynchronous Programming in .NET 4.5 with C# and Visual Basic**&quot; included in the Visual Studio Training Kit.</span></span>

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a><span data-ttu-id="27d1d-551">任务 2-取消标记的处理超时</span><span class="sxs-lookup"><span data-stu-id="27d1d-551">Task 2 - Handling Time-Outs with Cancellation Tokens</span></span>

<span data-ttu-id="27d1d-552">异步操作方法的返回任务实例还可以支持超时。</span><span class="sxs-lookup"><span data-stu-id="27d1d-552">Asynchronous action methods that return Task instances can also support time-outs.</span></span> <span data-ttu-id="27d1d-553">在本任务中，将更新索引方法代码以处理超时方案使用取消标记。</span><span class="sxs-lookup"><span data-stu-id="27d1d-553">In this task, you will update the Index method code to handle a time-out scenario using a cancellation token.</span></span>

1. <span data-ttu-id="27d1d-554">返回到 Visual Studio 并按**SHIFT + F5**以停止调试。</span><span class="sxs-lookup"><span data-stu-id="27d1d-554">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>
2. <span data-ttu-id="27d1d-555">添加以下 using 语句**HomeController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="27d1d-555">Add the following using statement to the **HomeController.cs** file.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. <span data-ttu-id="27d1d-556">更新索引操作，以便接收**CancellationToken**参数。</span><span class="sxs-lookup"><span data-stu-id="27d1d-556">Update the Index action to receive a **CancellationToken** argument.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. <span data-ttu-id="27d1d-557">更新**GetAsync**调用即可传递的取消标记。</span><span class="sxs-lookup"><span data-stu-id="27d1d-557">Update the **GetAsync** call to pass the cancellation token.</span></span>

    <span data-ttu-id="27d1d-558">(代码段- *CancellationToken 与 ASP.NET MVC 4 实验室-Ex04-SendAsync*)</span><span class="sxs-lookup"><span data-stu-id="27d1d-558">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - SendAsync with CancellationToken*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. <span data-ttu-id="27d1d-559">修饰*索引*方法替换**AsyncTimeout**属性设置为 500 毫秒和一个**HandleError**属性配置为处理**TaskCanceledException**通过重定向到**TimedOut**视图。</span><span class="sxs-lookup"><span data-stu-id="27d1d-559">Decorate the *Index* method with an **AsyncTimeout** attribute set to 500 milliseconds and a **HandleError** attribute configured to handle **TaskCanceledException** by redirecting to a **TimedOut** view.</span></span>

    <span data-ttu-id="27d1d-560">(代码段- *ASP.NET MVC 4 实验室-Ex04-属性*)</span><span class="sxs-lookup"><span data-stu-id="27d1d-560">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - Attributes*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. <span data-ttu-id="27d1d-561">打开**PhotoController**类和更新**库**方法来延迟执行 1000年毫秒 （1 秒），以模拟长时间运行的任务。</span><span class="sxs-lookup"><span data-stu-id="27d1d-561">Open the **PhotoController** class and update the **Gallery** method to delay the execution 1000 miliseconds (1 second) to simulate a long running task.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. <span data-ttu-id="27d1d-562">打开**Web.config**文件并添加以下元素，从而启用自定义错误。</span><span class="sxs-lookup"><span data-stu-id="27d1d-562">Open the **Web.config** file and enable custom errors by adding the following element.</span></span>

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. <span data-ttu-id="27d1d-563">创建新视图中的**views/shared**名为**TimedOut** ，并使用默认布局。</span><span class="sxs-lookup"><span data-stu-id="27d1d-563">Create a new view in **Views\Shared** named **TimedOut** and use the default layout.</span></span> <span data-ttu-id="27d1d-564">在解决方案资源管理器，右键单击**views/shared**文件夹，然后选择**添加 |视图**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-564">In the Solution Explorer, right-click the **Views\Shared** folder and select **Add | View**.</span></span>

    <span data-ttu-id="27d1d-565">![对于每个移动设备使用不同的视图](whats-new-in-aspnet-mvc-4/_static/image36.png "对于每个移动设备使用不同的视图")</span><span class="sxs-lookup"><span data-stu-id="27d1d-565">![Using different views for each mobile device](whats-new-in-aspnet-mvc-4/_static/image36.png "Using different views for each mobile device")</span></span>

    <span data-ttu-id="27d1d-566">*对于每个移动设备使用不同的视图*</span><span class="sxs-lookup"><span data-stu-id="27d1d-566">*Using different views for each mobile device*</span></span>
9. <span data-ttu-id="27d1d-567">更新**TimedOut**查看内容，如下所示。</span><span class="sxs-lookup"><span data-stu-id="27d1d-567">Update the **TimedOut** view content as shown below.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. <span data-ttu-id="27d1d-568">运行应用程序并导航到的根 URL。</span><span class="sxs-lookup"><span data-stu-id="27d1d-568">Run the application and navigate to the root URL.</span></span> <span data-ttu-id="27d1d-569">随着您添加**Thread.Sleep**的 1000年毫秒，则会出现超时错误，由生成**AsyncTimeout**属性，来发现**HandleError**属性。</span><span class="sxs-lookup"><span data-stu-id="27d1d-569">As you have added a **Thread.Sleep** of 1000 milliseconds, you will get a time-out error, generated by the **AsyncTimeout** attribute and catch by the **HandleError** attribute.</span></span>

    <span data-ttu-id="27d1d-570">![处理超时异常](whats-new-in-aspnet-mvc-4/_static/image37.png "超时异常处理")</span><span class="sxs-lookup"><span data-stu-id="27d1d-570">![Time-out exception handled](whats-new-in-aspnet-mvc-4/_static/image37.png "Time-out exception handled")</span></span>

    <span data-ttu-id="27d1d-571">*超时异常处理*</span><span class="sxs-lookup"><span data-stu-id="27d1d-571">*Time-out exception handled*</span></span>

> [!NOTE]
> <span data-ttu-id="27d1d-572">此外，可以部署此应用程序到 Windows Azure Web Sites 以下[附录 d： 发布 ASP.NET MVC 4 应用程序使用 Web 部署](#AppendixD)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-572">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixD).</span></span>


<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="27d1d-573">总结</span><span class="sxs-lookup"><span data-stu-id="27d1d-573">Summary</span></span>

<span data-ttu-id="27d1d-574">在此动手实验，我们已观察到的一些新功能驻留在 ASP.NET MVC 4 中。</span><span class="sxs-lookup"><span data-stu-id="27d1d-574">In this hands-on-lab, you've observed some of the new features resident in ASP.NET MVC 4.</span></span> <span data-ttu-id="27d1d-575">讨论了以下概念：</span><span class="sxs-lookup"><span data-stu-id="27d1d-575">The following concepts have been discussed:</span></span>

- <span data-ttu-id="27d1d-576">充分利用 ASP.NET MVC 项目模板包括新的移动应用程序项目模板的增强功能</span><span class="sxs-lookup"><span data-stu-id="27d1d-576">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="27d1d-577">使用 HTML5 视区属性和 CSS 媒体查询来改善在移动设备上显示</span><span class="sxs-lookup"><span data-stu-id="27d1d-577">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="27d1d-578">使用 jQuery Mobile 的渐进式增强功能和用于构建触控优化的 web UI</span><span class="sxs-lookup"><span data-stu-id="27d1d-578">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="27d1d-579">创建移动特定视图</span><span class="sxs-lookup"><span data-stu-id="27d1d-579">Create mobile-specific views</span></span>
- <span data-ttu-id="27d1d-580">使用视图切换器组件来移动和桌面应用程序中的视图之间切换</span><span class="sxs-lookup"><span data-stu-id="27d1d-580">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="27d1d-581">创建使用任务支持异步控制器</span><span class="sxs-lookup"><span data-stu-id="27d1d-581">Create asynchronous controllers using task support</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="27d1d-582">附录 a： 使用代码片段</span><span class="sxs-lookup"><span data-stu-id="27d1d-582">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="27d1d-583">使用代码段，可以轻松获得相关所需的所有代码。</span><span class="sxs-lookup"><span data-stu-id="27d1d-583">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="27d1d-584">实验室文档将告诉您完全何时可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="27d1d-584">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="27d1d-585">![使用 Visual Studio 代码段代码插入到你的项目](whats-new-in-aspnet-mvc-4/_static/image38.png "使用 Visual Studio 代码段代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="27d1d-585">![Using Visual Studio code snippets to insert code into your project](whats-new-in-aspnet-mvc-4/_static/image38.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="27d1d-586">*使用 Visual Studio 代码段代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="27d1d-586">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="27d1d-587">***若要添加代码段使用键盘 (仅限 C#)***</span><span class="sxs-lookup"><span data-stu-id="27d1d-587">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="27d1d-588">将光标置于要插入的代码。</span><span class="sxs-lookup"><span data-stu-id="27d1d-588">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="27d1d-589">开始键入代码片段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="27d1d-589">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="27d1d-590">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="27d1d-590">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="27d1d-591">选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。</span><span class="sxs-lookup"><span data-stu-id="27d1d-591">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="27d1d-592">按 Tab 键两次，以在光标位置插入代码段。</span><span class="sxs-lookup"><span data-stu-id="27d1d-592">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="27d1d-593">![开始键入代码段名称](whats-new-in-aspnet-mvc-4/_static/image39.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="27d1d-593">![Start typing the snippet name](whats-new-in-aspnet-mvc-4/_static/image39.png "Start typing the snippet name")</span></span>

<span data-ttu-id="27d1d-594">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="27d1d-594">*Start typing the snippet name*</span></span>

<span data-ttu-id="27d1d-595">![按 tab 键以选择突出显示代码段](whats-new-in-aspnet-mvc-4/_static/image40.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="27d1d-595">![Press Tab to select the highlighted snippet](whats-new-in-aspnet-mvc-4/_static/image40.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="27d1d-596">*按 tab 键以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="27d1d-596">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="27d1d-597">![再次按 Tab 和代码段将 expand](whats-new-in-aspnet-mvc-4/_static/image41.png "再次按 Tab 和代码段将扩展")</span><span class="sxs-lookup"><span data-stu-id="27d1d-597">![Press Tab again and the snippet will expand](whats-new-in-aspnet-mvc-4/_static/image41.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="27d1d-598">*再次按 Tab 和代码段将扩展*</span><span class="sxs-lookup"><span data-stu-id="27d1d-598">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="27d1d-599">***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）***</span><span class="sxs-lookup"><span data-stu-id="27d1d-599">***To add a code snippet using the mouse (C#, Visual Basic and XML)***</span></span>

1. <span data-ttu-id="27d1d-600">右键单击你想要插入的代码片段。</span><span class="sxs-lookup"><span data-stu-id="27d1d-600">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="27d1d-601">选择**插入代码段**跟**我的代码片段**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-601">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="27d1d-602">通过单击选择列表中中的相关代码片段。</span><span class="sxs-lookup"><span data-stu-id="27d1d-602">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="27d1d-603">![右键单击你想要插入代码段和选择插入代码段](whats-new-in-aspnet-mvc-4/_static/image42.png "右键单击你想要插入代码段和选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="27d1d-603">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-aspnet-mvc-4/_static/image42.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="27d1d-604">*右键单击你想要插入代码段和选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="27d1d-604">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="27d1d-605">![通过单击选择列表中中的相关代码片段](whats-new-in-aspnet-mvc-4/_static/image43.png "通过单击选择列表中中的相关代码片段")</span><span class="sxs-lookup"><span data-stu-id="27d1d-605">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-aspnet-mvc-4/_static/image43.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="27d1d-606">*通过单击选择列表中中的相关代码片段*</span><span class="sxs-lookup"><span data-stu-id="27d1d-606">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="27d1d-607">附录 b： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="27d1d-607">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="27d1d-608">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="27d1d-608">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="27d1d-609">以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="27d1d-609">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="27d1d-610">转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-610">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="27d1d-611">或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="27d1d-611">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="27d1d-612">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-612">Click on **Install Now**.</span></span> <span data-ttu-id="27d1d-613">如果还没有**Web 平台安装程序**将重定向以下载并安装。</span><span class="sxs-lookup"><span data-stu-id="27d1d-613">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="27d1d-614">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-614">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="27d1d-615">![安装 Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="27d1d-615">![Install Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="27d1d-616">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="27d1d-616">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="27d1d-617">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="27d1d-617">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](whats-new-in-aspnet-mvc-4/_static/image45.png)

    <span data-ttu-id="27d1d-619">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="27d1d-619">*Accepting the license terms*</span></span>
5. <span data-ttu-id="27d1d-620">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="27d1d-620">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](whats-new-in-aspnet-mvc-4/_static/image46.png)

    <span data-ttu-id="27d1d-622">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="27d1d-622">*Installation progress*</span></span>
6. <span data-ttu-id="27d1d-623">安装完成后，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-623">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](whats-new-in-aspnet-mvc-4/_static/image47.png)

    <span data-ttu-id="27d1d-625">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="27d1d-625">*Installation completed*</span></span>
7. <span data-ttu-id="27d1d-626">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-626">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="27d1d-627">若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="27d1d-627">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](whats-new-in-aspnet-mvc-4/_static/image48.png)

    <span data-ttu-id="27d1d-629">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="27d1d-629">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a><span data-ttu-id="27d1d-630">附录 c： 安装 WebMatrix 2 和 iPhone 模拟器</span><span class="sxs-lookup"><span data-stu-id="27d1d-630">Appendix C: Installing WebMatrix 2 and iPhone Simulator</span></span>

<span data-ttu-id="27d1d-631">若要模拟的 iPhone 设备中运行你的站点可以使用 WebMatrix 扩展&quot;适用于 iPhone 的电力移动模拟器&quot;。</span><span class="sxs-lookup"><span data-stu-id="27d1d-631">To run your site in a simulated iPhone device you can use the WebMatrix extension &quot;Electric Mobile Simulator for the iPhone&quot;.</span></span> <span data-ttu-id="27d1d-632">此外，您可以配置相同的扩展名从 Visual Studio 2012 运行模拟器。</span><span class="sxs-lookup"><span data-stu-id="27d1d-632">Also, you can configure the same extension to run the simulator from Visual Studio 2012.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a><span data-ttu-id="27d1d-633">任务 1-安装 WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="27d1d-633">Task 1 - Installing WebMatrix 2</span></span>

1. <span data-ttu-id="27d1d-634">转到[ [ https://go.microsoft.com/?linkid=9809776 ](https://go.microsoft.com/?linkid=9809776) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-634">Go to [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="27d1d-635">或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>WebMatrix 2</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="27d1d-635">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>WebMatrix 2</em>&quot;.</span></span>
2. <span data-ttu-id="27d1d-636">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-636">Click on **Install Now**.</span></span> <span data-ttu-id="27d1d-637">如果还没有**Web 平台安装程序**将重定向以下载并安装。</span><span class="sxs-lookup"><span data-stu-id="27d1d-637">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="27d1d-638">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-638">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="27d1d-639">![安装 WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "安装 WebMatrix 2")</span><span class="sxs-lookup"><span data-stu-id="27d1d-639">![Install WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "Install WebMatrix 2")</span></span>

    <span data-ttu-id="27d1d-640">*安装 WebMatrix 2*</span><span class="sxs-lookup"><span data-stu-id="27d1d-640">*Install WebMatrix 2*</span></span>
4. <span data-ttu-id="27d1d-641">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="27d1d-641">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    <span data-ttu-id="27d1d-642">![接受许可条款](whats-new-in-aspnet-mvc-4/_static/image50.png "接受许可条款")</span><span class="sxs-lookup"><span data-stu-id="27d1d-642">![Accepting the license terms](whats-new-in-aspnet-mvc-4/_static/image50.png "Accepting the license terms")</span></span>

    <span data-ttu-id="27d1d-643">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="27d1d-643">*Accepting the license terms*</span></span>
5. <span data-ttu-id="27d1d-644">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="27d1d-644">Wait until the downloading and installation process completes.</span></span>

    <span data-ttu-id="27d1d-645">![安装进度](whats-new-in-aspnet-mvc-4/_static/image51.png "安装进度")</span><span class="sxs-lookup"><span data-stu-id="27d1d-645">![Installation progress](whats-new-in-aspnet-mvc-4/_static/image51.png "Installation progress")</span></span>

    <span data-ttu-id="27d1d-646">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="27d1d-646">*Installation progress*</span></span>
6. <span data-ttu-id="27d1d-647">安装完成后，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-647">When the installation completes, click **Finish**.</span></span>

    <span data-ttu-id="27d1d-648">![安装已完成](whats-new-in-aspnet-mvc-4/_static/image52.png "安装已完成")</span><span class="sxs-lookup"><span data-stu-id="27d1d-648">![Installation completed](whats-new-in-aspnet-mvc-4/_static/image52.png "Installation completed")</span></span>

    <span data-ttu-id="27d1d-649">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="27d1d-649">*Installation completed*</span></span>
7. <span data-ttu-id="27d1d-650">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-650">Click **Exit** to close Web Platform Installer.</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a><span data-ttu-id="27d1d-651">任务 2-安装在 iPhone 模拟器扩展</span><span class="sxs-lookup"><span data-stu-id="27d1d-651">Task 2 - Installing the iPhone Simulator Extension</span></span>

1. <span data-ttu-id="27d1d-652">运行**WebMatrix**和打开任何现有的网站或创建一个新。</span><span class="sxs-lookup"><span data-stu-id="27d1d-652">Run **WebMatrix** and open any existing Web site or create a new one.</span></span>
2. <span data-ttu-id="27d1d-653">单击**运行**按钮从**主页**功能区，然后选择**添加新**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-653">Click the **Run** button from the **Home** ribbon and select **Add new**.</span></span>

    <span data-ttu-id="27d1d-654">![添加新的 WebMatrix 扩展](whats-new-in-aspnet-mvc-4/_static/image53.png "添加新的 WebMatrix 扩展插件")</span><span class="sxs-lookup"><span data-stu-id="27d1d-654">![Adding new WebMatrix extension](whats-new-in-aspnet-mvc-4/_static/image53.png "Adding new WebMatrix extension")</span></span>

    <span data-ttu-id="27d1d-655">*添加新的 WebMatrix 扩展插件*</span><span class="sxs-lookup"><span data-stu-id="27d1d-655">*Adding new WebMatrix extension*</span></span>
3. <span data-ttu-id="27d1d-656">选择**iPhone 模拟器**然后单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-656">Select **iPhone Simulator** and click **Install**.</span></span>

    <span data-ttu-id="27d1d-657">![浏览 WebMatrix 扩展](whats-new-in-aspnet-mvc-4/_static/image54.png "浏览 WebMatrix 扩展")</span><span class="sxs-lookup"><span data-stu-id="27d1d-657">![Browsing WebMatrix extensions](whats-new-in-aspnet-mvc-4/_static/image54.png "Browsing WebMatrix extensions")</span></span>

    <span data-ttu-id="27d1d-658">*浏览 WebMatrix 扩展*</span><span class="sxs-lookup"><span data-stu-id="27d1d-658">*Browsing WebMatrix extensions*</span></span>
4. <span data-ttu-id="27d1d-659">在包的详细信息，请单击**安装**继续扩展安装。</span><span class="sxs-lookup"><span data-stu-id="27d1d-659">In the package details, click **Install** to continue with the extension installation.</span></span>

    <span data-ttu-id="27d1d-660">![iPhone 模拟器扩展](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone 模拟器扩展")</span><span class="sxs-lookup"><span data-stu-id="27d1d-660">![iPhone Simulator extension](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone Simulator extension")</span></span>

    <span data-ttu-id="27d1d-661">*iPhone 模拟器扩展*</span><span class="sxs-lookup"><span data-stu-id="27d1d-661">*iPhone Simulator extension*</span></span>
5. <span data-ttu-id="27d1d-662">阅读并接受最终用户许可协议的扩展。</span><span class="sxs-lookup"><span data-stu-id="27d1d-662">Read and accept the extension EULA.</span></span>

    <span data-ttu-id="27d1d-663">![WebMatrix 扩展 EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 扩展最终用户许可协议")</span><span class="sxs-lookup"><span data-stu-id="27d1d-663">![WebMatrix extension EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix extension EULA")</span></span>

    <span data-ttu-id="27d1d-664">*WebMatrix 扩展最终用户许可协议*</span><span class="sxs-lookup"><span data-stu-id="27d1d-664">*WebMatrix extension EULA*</span></span>
6. <span data-ttu-id="27d1d-665">现在，可以从 WebMatrix 中运行你的网站使用 iPhone 模拟器选项。</span><span class="sxs-lookup"><span data-stu-id="27d1d-665">Now, you can run your Web site from WebMatrix using the iPhone Simulator option.</span></span>

    <span data-ttu-id="27d1d-666">![运行使用 iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "运行使用 iPhone")</span><span class="sxs-lookup"><span data-stu-id="27d1d-666">![Run using iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "Run using iPhone")</span></span>

    <span data-ttu-id="27d1d-667">*使用 iPhone 运行*</span><span class="sxs-lookup"><span data-stu-id="27d1d-667">*Run using iPhone*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a><span data-ttu-id="27d1d-668">任务 3-配置 Visual Studio 2012 运行 iPhone 模拟器</span><span class="sxs-lookup"><span data-stu-id="27d1d-668">Task 3 - Configuring Visual Studio 2012 to run iPhone Simulator</span></span>

1. <span data-ttu-id="27d1d-669">打开**Visual Studio 2012**和打开的任何网站或创建新的项目。</span><span class="sxs-lookup"><span data-stu-id="27d1d-669">Open **Visual Studio 2012** and open any Web site or create a new project.</span></span>
2. <span data-ttu-id="27d1d-670">单击从运行按钮的向下箭头，然后选择**浏览与**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-670">Click the down arrow from the Run button and select **Browse with**.</span></span>

    <span data-ttu-id="27d1d-671">![使用浏览](whats-new-in-aspnet-mvc-4/_static/image58.png "浏览与")</span><span class="sxs-lookup"><span data-stu-id="27d1d-671">![Browse with](whats-new-in-aspnet-mvc-4/_static/image58.png "Browse with")</span></span>

    <span data-ttu-id="27d1d-672">*浏览与*</span><span class="sxs-lookup"><span data-stu-id="27d1d-672">*Browse with*</span></span>
3. <span data-ttu-id="27d1d-673">在中&quot;浏览方式&quot;对话框中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-673">In the &quot;Browse With&quot; dialog, click **Add**.</span></span>
4. <span data-ttu-id="27d1d-674">在中&quot;添加程序&quot;对话框中，使用以下值：</span><span class="sxs-lookup"><span data-stu-id="27d1d-674">In the &quot;Add Program&quot; dialog, use the following values:</span></span>

   - <span data-ttu-id="27d1d-675"><strong>程序</strong>: C:\Users\*{CurrentUser}<em>\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe * （相应地更新路径）</em></span><span class="sxs-lookup"><span data-stu-id="27d1d-675"><strong>Program</strong>: C:\Users\*{CurrentUser}<em>\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(update the path accordingly)</em></span></span>
   - <span data-ttu-id="27d1d-676">**自变量**: &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="27d1d-676">**Arguments**: &quot;1&quot;</span></span>
   - <span data-ttu-id="27d1d-677">**友好名称**: iPhone 模拟器</span><span class="sxs-lookup"><span data-stu-id="27d1d-677">**Friendly name**: iPhone Simulator</span></span>

     <span data-ttu-id="27d1d-678">![添加程序](whats-new-in-aspnet-mvc-4/_static/image59.png "添加程序")</span><span class="sxs-lookup"><span data-stu-id="27d1d-678">![Add program](whats-new-in-aspnet-mvc-4/_static/image59.png "Add program")</span></span>

     <span data-ttu-id="27d1d-679">*添加程序使用浏览*</span><span class="sxs-lookup"><span data-stu-id="27d1d-679">*Add program to browse with*</span></span>
5. <span data-ttu-id="27d1d-680">单击**确定**并关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="27d1d-680">Click **OK** and close the dialogs.</span></span>
6. <span data-ttu-id="27d1d-681">现在，已能够从 Visual Studio 2012 在 iPhone 模拟器中运行 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="27d1d-681">Now you are able to run your Web applications in the iPhone simulator from Visual Studio 2012.</span></span>

    <span data-ttu-id="27d1d-682">![浏览包含 iPhone 模拟器](whats-new-in-aspnet-mvc-4/_static/image60.png "浏览包含 iPhone 模拟器")</span><span class="sxs-lookup"><span data-stu-id="27d1d-682">![Browse with iPhone Simulator](whats-new-in-aspnet-mvc-4/_static/image60.png "Browse with iPhone Simulator")</span></span>

    <span data-ttu-id="27d1d-683">*使用 iPhone 模拟器中浏览*</span><span class="sxs-lookup"><span data-stu-id="27d1d-683">*Browse with iPhone Simulator*</span></span>

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="27d1d-684">附录 d： 发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="27d1d-684">Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="27d1d-685">本附录将演示如何从 Windows Azure 管理门户创建新的网站和发布应用程序获取按照本实验中，利用 Windows Azure 提供的 Web 部署发布功能。</span><span class="sxs-lookup"><span data-stu-id="27d1d-685">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="27d1d-686">任务 1-创建新的 Web 站点从 Windows Azure 门户</span><span class="sxs-lookup"><span data-stu-id="27d1d-686">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="27d1d-687">转到[Windows Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="27d1d-687">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27d1d-688">使用 Windows Azure 可以免费托管 10 个 ASP.NET 网站，然后随着流量增长情况。</span><span class="sxs-lookup"><span data-stu-id="27d1d-688">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="27d1d-689">你可以注册[此处](http://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-689">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="27d1d-690">![登录到 Windows Azure 门户](whats-new-in-aspnet-mvc-4/_static/image61.png "登录到 Windows Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="27d1d-690">![Log on to Windows Azure portal](whats-new-in-aspnet-mvc-4/_static/image61.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="27d1d-691">*登录到 Windows Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="27d1d-691">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="27d1d-692">单击**新建**命令栏上。</span><span class="sxs-lookup"><span data-stu-id="27d1d-692">Click **New** on the command bar.</span></span>

    <span data-ttu-id="27d1d-693">![创建新的 Web 站点](whats-new-in-aspnet-mvc-4/_static/image62.png "创建新的 Web 站点")</span><span class="sxs-lookup"><span data-stu-id="27d1d-693">![Creating a new Web Site](whats-new-in-aspnet-mvc-4/_static/image62.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="27d1d-694">*创建新的 Web 站点*</span><span class="sxs-lookup"><span data-stu-id="27d1d-694">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="27d1d-695">单击**计算** | **网站**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-695">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="27d1d-696">然后选择**快速创建**选项。</span><span class="sxs-lookup"><span data-stu-id="27d1d-696">Then select **Quick Create** option.</span></span> <span data-ttu-id="27d1d-697">为新网站提供可用的 URL，然后单击**创建网站**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-697">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27d1d-698">Windows Azure 网站是可以控制和管理在云中运行的 web 应用程序主机。</span><span class="sxs-lookup"><span data-stu-id="27d1d-698">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="27d1d-699">快速创建选项，可将已完成的 web 应用程序到 Windows Azure 网站从门户外部的部署。</span><span class="sxs-lookup"><span data-stu-id="27d1d-699">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="27d1d-700">它不包括用于设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="27d1d-700">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="27d1d-701">![创建新的网站使用快速创建](whats-new-in-aspnet-mvc-4/_static/image63.png "创建新的网站使用快速创建")</span><span class="sxs-lookup"><span data-stu-id="27d1d-701">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-mvc-4/_static/image63.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="27d1d-702">*创建新的网站使用快速创建*</span><span class="sxs-lookup"><span data-stu-id="27d1d-702">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="27d1d-703">等到新**网站**创建。</span><span class="sxs-lookup"><span data-stu-id="27d1d-703">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="27d1d-704">创建网站后，单击下面的链接**URL**列。</span><span class="sxs-lookup"><span data-stu-id="27d1d-704">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="27d1d-705">检查新的 Web 站点正常工作。</span><span class="sxs-lookup"><span data-stu-id="27d1d-705">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="27d1d-706">![浏览到新的 web 站点](whats-new-in-aspnet-mvc-4/_static/image64.png "浏览到新的 web 站点")</span><span class="sxs-lookup"><span data-stu-id="27d1d-706">![Browsing to the new web site](whats-new-in-aspnet-mvc-4/_static/image64.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="27d1d-707">*浏览到新的 web 站点*</span><span class="sxs-lookup"><span data-stu-id="27d1d-707">*Browsing to the new web site*</span></span>

    <span data-ttu-id="27d1d-708">![正在运行的网站](whats-new-in-aspnet-mvc-4/_static/image65.png "正在运行的网站")</span><span class="sxs-lookup"><span data-stu-id="27d1d-708">![Web site running](whats-new-in-aspnet-mvc-4/_static/image65.png "Web site running")</span></span>

    <span data-ttu-id="27d1d-709">*正在运行的网站*</span><span class="sxs-lookup"><span data-stu-id="27d1d-709">*Web site running*</span></span>
6. <span data-ttu-id="27d1d-710">返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。</span><span class="sxs-lookup"><span data-stu-id="27d1d-710">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="27d1d-711">![打开网站管理页](whats-new-in-aspnet-mvc-4/_static/image66.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="27d1d-711">![Opening the web site management pages](whats-new-in-aspnet-mvc-4/_static/image66.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="27d1d-712">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="27d1d-712">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="27d1d-713">在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。</span><span class="sxs-lookup"><span data-stu-id="27d1d-713">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27d1d-714">*发布配置文件*包含所有发布到每个启用的发布方法的 Windows Azure 网站的 web 应用程序所需的信息。</span><span class="sxs-lookup"><span data-stu-id="27d1d-714">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="27d1d-715">发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="27d1d-715">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="27d1d-716">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="27d1d-716">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="27d1d-717">![正在下载网站发布配置文件](whats-new-in-aspnet-mvc-4/_static/image67.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="27d1d-717">![Downloading the web site publish profile](whats-new-in-aspnet-mvc-4/_static/image67.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="27d1d-718">*正在下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="27d1d-718">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="27d1d-719">下载发布配置文件到已知位置。</span><span class="sxs-lookup"><span data-stu-id="27d1d-719">Download the publish profile file to a known location.</span></span> <span data-ttu-id="27d1d-720">进一步在此练习中将了解如何使用此文件从 Visual Studio 的 web 应用程序到 Windows Azure 网站发布。</span><span class="sxs-lookup"><span data-stu-id="27d1d-720">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="27d1d-721">![保存发布配置文件](whats-new-in-aspnet-mvc-4/_static/image68.png "保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="27d1d-721">![Saving the publish profile file](whats-new-in-aspnet-mvc-4/_static/image68.png "Saving the publish profile")</span></span>

    <span data-ttu-id="27d1d-722">*保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="27d1d-722">*Saving the publish profile file*</span></span>

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="27d1d-723">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="27d1d-723">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="27d1d-724">如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="27d1d-724">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="27d1d-725">如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="27d1d-725">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="27d1d-726">用于存储应用程序数据库，将需要 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="27d1d-726">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="27d1d-727">可以从在 Windows Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-727">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="27d1d-728">如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。</span><span class="sxs-lookup"><span data-stu-id="27d1d-728">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="27d1d-729">请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="27d1d-729">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="27d1d-730">不创建数据库，因为它将在后面的阶段中创建。</span><span class="sxs-lookup"><span data-stu-id="27d1d-730">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="27d1d-731">![SQL 数据库服务器仪表板](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database 服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="27d1d-731">![SQL Database Server Dashboard](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="27d1d-732">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="27d1d-732">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="27d1d-733">在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-733">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="27d1d-734">若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框中，然后单击![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png)按钮。</span><span class="sxs-lookup"><span data-stu-id="27d1d-734">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) button.</span></span>

    ![添加客户端 IP 地址](whats-new-in-aspnet-mvc-4/_static/image71.png)

    <span data-ttu-id="27d1d-736">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="27d1d-736">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="27d1d-737">一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。</span><span class="sxs-lookup"><span data-stu-id="27d1d-737">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认更改](whats-new-in-aspnet-mvc-4/_static/image72.png)

    <span data-ttu-id="27d1d-739">*确认更改*</span><span class="sxs-lookup"><span data-stu-id="27d1d-739">*Confirm Changes*</span></span>

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="27d1d-740">任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布</span><span class="sxs-lookup"><span data-stu-id="27d1d-740">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="27d1d-741">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="27d1d-741">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="27d1d-742">在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-742">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="27d1d-743">![发布应用程序](whats-new-in-aspnet-mvc-4/_static/image73.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="27d1d-743">![Publishing the Application](whats-new-in-aspnet-mvc-4/_static/image73.png "Publishing the Application")</span></span>

    <span data-ttu-id="27d1d-744">*发布此网站*</span><span class="sxs-lookup"><span data-stu-id="27d1d-744">*Publishing the web site*</span></span>
2. <span data-ttu-id="27d1d-745">导入发布配置文件保存在第一个任务。</span><span class="sxs-lookup"><span data-stu-id="27d1d-745">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="27d1d-746">![导入发布配置文件](whats-new-in-aspnet-mvc-4/_static/image74.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="27d1d-746">![Importing the publish profile](whats-new-in-aspnet-mvc-4/_static/image74.png "Importing the publish profile")</span></span>

    <span data-ttu-id="27d1d-747">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="27d1d-747">*Importing publish profile*</span></span>
3. <span data-ttu-id="27d1d-748">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-748">Click **Validate Connection**.</span></span> <span data-ttu-id="27d1d-749">验证完成后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-749">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27d1d-750">请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。</span><span class="sxs-lookup"><span data-stu-id="27d1d-750">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="27d1d-751">![验证连接](whats-new-in-aspnet-mvc-4/_static/image75.png "验证连接")</span><span class="sxs-lookup"><span data-stu-id="27d1d-751">![Validating connection](whats-new-in-aspnet-mvc-4/_static/image75.png "Validating connection")</span></span>

    <span data-ttu-id="27d1d-752">*验证连接*</span><span class="sxs-lookup"><span data-stu-id="27d1d-752">*Validating connection*</span></span>
4. <span data-ttu-id="27d1d-753">在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="27d1d-753">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="27d1d-754">![Web 部署配置](whats-new-in-aspnet-mvc-4/_static/image76.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="27d1d-754">![Web deploy configuration](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy configuration")</span></span>

    <span data-ttu-id="27d1d-755">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="27d1d-755">*Web deploy configuration*</span></span>
5. <span data-ttu-id="27d1d-756">配置数据库连接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="27d1d-756">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="27d1d-757">在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。</span><span class="sxs-lookup"><span data-stu-id="27d1d-757">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="27d1d-758">在中**用户名**键入服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="27d1d-758">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="27d1d-759">在中**密码**键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="27d1d-759">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="27d1d-760">键入新的数据库名称，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="27d1d-760">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="27d1d-761">![配置目标连接字符串](whats-new-in-aspnet-mvc-4/_static/image77.png "配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="27d1d-761">![Configuring destination connection string](whats-new-in-aspnet-mvc-4/_static/image77.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="27d1d-762">*配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="27d1d-762">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="27d1d-763">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="27d1d-763">Then click **OK**.</span></span> <span data-ttu-id="27d1d-764">当系统提示你创建数据库时，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-764">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="27d1d-765">![创建数据库](whats-new-in-aspnet-mvc-4/_static/image78.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="27d1d-765">![Creating the database](whats-new-in-aspnet-mvc-4/_static/image78.png "Creating the database string")</span></span>

    <span data-ttu-id="27d1d-766">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="27d1d-766">*Creating the database*</span></span>
7. <span data-ttu-id="27d1d-767">将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。</span><span class="sxs-lookup"><span data-stu-id="27d1d-767">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="27d1d-768">然后，单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-768">Then click **Next**.</span></span>

    <span data-ttu-id="27d1d-769">![连接字符串指向 SQL 数据库](whats-new-in-aspnet-mvc-4/_static/image79.png "指向 SQL 数据库连接字符串")</span><span class="sxs-lookup"><span data-stu-id="27d1d-769">![Connection string pointing to SQL Database](whats-new-in-aspnet-mvc-4/_static/image79.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="27d1d-770">*连接字符串指向 SQL 数据库*</span><span class="sxs-lookup"><span data-stu-id="27d1d-770">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="27d1d-771">在中**预览版**页上，单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="27d1d-771">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="27d1d-772">![Web 应用程序发布](whats-new-in-aspnet-mvc-4/_static/image80.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="27d1d-772">![Publishing the web application](whats-new-in-aspnet-mvc-4/_static/image80.png "Publishing the web application")</span></span>

    <span data-ttu-id="27d1d-773">*Web 应用程序发布*</span><span class="sxs-lookup"><span data-stu-id="27d1d-773">*Publishing the web application*</span></span>
9. <span data-ttu-id="27d1d-774">在发布过程完成后，在默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="27d1d-774">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="27d1d-775">![应用程序发布到 Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "应用程序发布到 Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="27d1d-775">![Application published to Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="27d1d-776">*应用程序发布到 Windows Azure*</span><span class="sxs-lookup"><span data-stu-id="27d1d-776">*Application published to Windows Azure*</span></span>
