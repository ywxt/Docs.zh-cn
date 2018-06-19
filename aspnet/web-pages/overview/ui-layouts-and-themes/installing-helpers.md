---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: 在 ASP.NET Web 安装程序的帮助页 (Razor) 站点 |Microsoft 文档
author: tfitzmac
description: 本文介绍如何在 ASP.NET Web 页 (Razor) 网站上安装程序的帮助。 一个帮助程序是一个可重用组件，包括代码和标记每个...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2014
ms.topic: article
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 766fbb87ae8bcb8917eb8fa7f552c00792242cf6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30896767"
---
<a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="7bd83-104">在一个 ASP.NET Web 页 (Razor) 站点中安装程序的帮助程序</span><span class="sxs-lookup"><span data-stu-id="7bd83-104">Installing a Helper in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="7bd83-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7bd83-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="7bd83-106">本文介绍如何在 ASP.NET Web 页 (Razor) 网站上安装程序的帮助。</span><span class="sxs-lookup"><span data-stu-id="7bd83-106">This article describes how to install a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="7bd83-107">A*帮助器*包括代码和标记，以执行可能需要很长时间或复杂的任务是可重用组件。</span><span class="sxs-lookup"><span data-stu-id="7bd83-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="7bd83-108">你将学习：</span><span class="sxs-lookup"><span data-stu-id="7bd83-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="7bd83-109">如何使用 WebMatrix 3 创建的网站中安装程序的帮助。</span><span class="sxs-lookup"><span data-stu-id="7bd83-109">How to install a helper in a website created using WebMatrix 3.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7bd83-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="7bd83-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="7bd83-111">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="7bd83-111">WebMatrix 3</span></span>


## <a name="overview-of-helpers"></a><span data-ttu-id="7bd83-112">帮助器概述</span><span class="sxs-lookup"><span data-stu-id="7bd83-112">Overview of Helpers</span></span>

<span data-ttu-id="7bd83-113">用户通常想要在网页上执行某些任务需要大量的代码，或者需要额外的知识。</span><span class="sxs-lookup"><span data-stu-id="7bd83-113">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="7bd83-114">示例包括显示的图表数据;在页面上; 将 Twitter"跟踪"按钮从您的网站; 发送电子邮件裁剪或调整图像; 的大小为您的网站使用 PayPal。</span><span class="sxs-lookup"><span data-stu-id="7bd83-114">Examples include displaying a chart for data; putting a Twitter "Follow" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="7bd83-115">为了更加轻松地完成这些类型的操作，ASP.NET 网页，你可以使用*帮助器*。</span><span class="sxs-lookup"><span data-stu-id="7bd83-115">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="7bd83-116">帮助器组件，你为站点和安装，可让你通过使用刚刚一行或两个 Razor 代码执行典型的任务。</span><span class="sxs-lookup"><span data-stu-id="7bd83-116">Helpers are components that you install for a site and that let you perform typical tasks by using just a line or two of Razor code.</span></span>

<span data-ttu-id="7bd83-117">ASP.NET Web 页具有内置的几个帮助器。</span><span class="sxs-lookup"><span data-stu-id="7bd83-117">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="7bd83-118">但是，使用 NuGet 包管理器提供的包 （外接程序） 中提供了许多的帮助器。</span><span class="sxs-lookup"><span data-stu-id="7bd83-118">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="7bd83-119">NuGet 允许你选择要安装的程序包，然后它就会完成安装的所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="7bd83-119">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

## <a name="installing-a-helper-in-webmatrix-3"></a><span data-ttu-id="7bd83-120">在 WebMatrix 3 中安装程序的帮助程序</span><span class="sxs-lookup"><span data-stu-id="7bd83-120">Installing a Helper in WebMatrix 3</span></span>

1. <span data-ttu-id="7bd83-121">在 WebMatrix 3 中，单击**NuGet**按钮。</span><span class="sxs-lookup"><span data-stu-id="7bd83-121">In WebMatrix 3, click the **NuGet** button.</span></span>

    ![在 WebMatrix 的 NuGet 库对话框](installing-helpers/_static/image1.png)
2. <span data-ttu-id="7bd83-123">这将启动 NuGet 包管理器，并显示可用的包。</span><span class="sxs-lookup"><span data-stu-id="7bd83-123">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="7bd83-124">在搜索框中，输入你想要安装的帮助程序关键字。</span><span class="sxs-lookup"><span data-stu-id="7bd83-124">In the search box, enter a keyword for the helper you want to install.</span></span>

    ![在 WebMatrix 的 NuGet 库对话框](installing-helpers/_static/image2.png)
3. <span data-ttu-id="7bd83-126">选择包，然后单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="7bd83-126">Select the package and then click **Install**.</span></span> <span data-ttu-id="7bd83-127">单击**是**当系统询问你是否想要安装包，并指示你接受条款。</span><span class="sxs-lookup"><span data-stu-id="7bd83-127">Click **Yes** when asked if you want to install the package and indicate that you accept the terms.</span></span>

     <span data-ttu-id="7bd83-128">如果这是已安装程序的帮助程序第一次，NuGet 将在你的网站代码的组成帮助器中创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="7bd83-128">If this is the first time you've installed a helper, NuGet creates folders in your website for the code that makes up the helper.</span></span>
4. <span data-ttu-id="7bd83-129">若要卸载程序的帮助，请单击**库**菜单上，单击**已安装**选项卡，然后选择你想要卸载的程序包。</span><span class="sxs-lookup"><span data-stu-id="7bd83-129">To uninstall a helper, click the **Gallery** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="installing-the-twitter-helper"></a><span data-ttu-id="7bd83-130">安装的 Twitter 帮助程序</span><span class="sxs-lookup"><span data-stu-id="7bd83-130">Installing the Twitter helper</span></span>

<span data-ttu-id="7bd83-131">Twitter API 的最新版本不兼容与通过 NuGet 安装 Twitter 帮助器。</span><span class="sxs-lookup"><span data-stu-id="7bd83-131">The latest version of the Twitter API is not compatible with the Twitter helper you install through NuGet.</span></span> <span data-ttu-id="7bd83-132">相反，请参阅[Twitter 使用 WebMatrix 的帮助器](twitter-helper.md)有关如何设置项目中的 Twitter 帮助程序信息的主题。</span><span class="sxs-lookup"><span data-stu-id="7bd83-132">Instead, see the [Twitter Helper with WebMatrix](twitter-helper.md) topic for information about how to set up the Twitter helper in your project.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="7bd83-133">其他资源</span><span class="sxs-lookup"><span data-stu-id="7bd83-133">Additional Resources</span></span>


[<span data-ttu-id="7bd83-134">简介 ASP.NET Web Pages 2-编程基础知识</span><span class="sxs-lookup"><span data-stu-id="7bd83-134">Introducing ASP.NET Web Pages 2 - Programming Basics</span></span>](../getting-started/introducing-razor-syntax-c.md)

[<span data-ttu-id="7bd83-135">使用 WebMatrix 的 twitter 帮助器</span><span class="sxs-lookup"><span data-stu-id="7bd83-135">Twitter Helper with WebMatrix</span></span>](twitter-helper.md)
