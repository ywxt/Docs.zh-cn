---
uid: web-pages/overview/releases/running-v1-and-v2-sites-side-by-side
title: 运行不同版本的 ASP.NET Web Pages (Razor) 同时 |Microsoft Docs
author: Rick-Anderson
description: 此文章介绍了如何在同一个计算机或服务器上运行 ASP.NET Web Pages (Razor) 网站，网站配置为使用不同版本时...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: a861409b-4ae6-4868-9e09-87edfac3535f
msc.legacyurl: /web-pages/overview/releases/running-v1-and-v2-sites-side-by-side
msc.type: authoredcontent
ms.openlocfilehash: e587398b430795c12a1dcee394852b4e2b8a0e44
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021166"
---
<a name="running-different-versions-of-aspnet-web-pages-razor-side-by-side"></a><span data-ttu-id="b6ff7-103">并行运行不同版本的 ASP.NET 网页 (Razor)</span><span class="sxs-lookup"><span data-stu-id="b6ff7-103">Running Different Versions of ASP.NET Web Pages (Razor) Side by Side</span></span>
====================
<span data-ttu-id="b6ff7-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b6ff7-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b6ff7-105">本文介绍如何在网站配置为使用不同版本的 ASP.NET Web Pages 时相同的计算机或服务器上运行 ASP.NET Web Pages (Razor) 网站。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-105">This article explains how to run ASP.NET Web Pages (Razor) websites on the same computer or server when the websites are configured to use different versions of ASP.NET Web Pages.</span></span>
> 
> <span data-ttu-id="b6ff7-106">你将学习：</span><span class="sxs-lookup"><span data-stu-id="b6ff7-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="b6ff7-107">什么的默认行为是在 ASP.NET 中，有时生成与 ASP.NET Web Pages 站点。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-107">What the default behavior is in ASP.NET when you have sites built with ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="b6ff7-108">如何配置新站点以使用较旧版本的 ASP.NET Web Pages 运行。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-108">How to configure a new site to run with an older version of ASP.NET Web Pages.</span></span>
>   
> 
> <span data-ttu-id="b6ff7-109">这是引入一文中的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="b6ff7-109">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="b6ff7-110">`webPages:Version`配置设置。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-110">The `webPages:Version` configuration setting.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="b6ff7-111">软件版本</span><span class="sxs-lookup"><span data-stu-id="b6ff7-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="b6ff7-112">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="b6ff7-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="b6ff7-113">本教程还适用于 ASP.NET Web Pages 2 和 ASP.NET Web Pages 1.0。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-113">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0.</span></span>


<span data-ttu-id="b6ff7-114">ASP.NET Web Pages 支持能够运行网站并排显示。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-114">ASP.NET Web Pages supports the ability to run websites side by side.</span></span> <span data-ttu-id="b6ff7-115">这样可以继续运行较旧的 ASP.NET Web Pages 应用程序，构建新的 ASP.NET Web Pages 应用程序，并在同一台计算机上运行所有这些。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-115">This lets you continue to run your older ASP.NET Web Pages applications, build new ASP.NET Web Pages applications, and run all of them on the same computer.</span></span>

<span data-ttu-id="b6ff7-116">下面是要使用 WebMatrix 安装 Web 页时，应注意一些事项：</span><span class="sxs-lookup"><span data-stu-id="b6ff7-116">Here are some things to remember when you install the Web Pages with WebMatrix:</span></span>

- <span data-ttu-id="b6ff7-117">默认情况下，现有的 Web Pages 应用程序将在计算机上运行的最新版本。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-117">By default, existing Web Pages applications will run as the latest version on your computer.</span></span> <span data-ttu-id="b6ff7-118">（程序集在全局程序集缓存 (GAC) 中安装和自动使用。）</span><span class="sxs-lookup"><span data-stu-id="b6ff7-118">(The assemblies are installed in the global assembly cache (GAC) and are used automatically.)</span></span>
- <span data-ttu-id="b6ff7-119">如果你想要运行使用不同版本的 ASP.NET Web Pages 站点，可以配置要执行此操作的站点。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-119">If you want to run a site using a different version of ASP.NET Web Pages, you can configure the site to do that.</span></span> <span data-ttu-id="b6ff7-120">如果您的网站还没有*web.config*文件位于站点的根目录中，创建一个新，并将以下 XML 复制到其中，覆盖现有内容。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-120">If your site doesn't already have a *web.config* file in the root of the site, create a new one and copy the following XML into it, overwriting the existing content.</span></span> <span data-ttu-id="b6ff7-121">如果站点中已包含*web.config*文件中，添加`<appSettings>`元素到如下`<configuration>`部分。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-121">If the site already contains a *web.config* file, add an `<appSettings>` element like the following one to the `<configuration>` section.</span></span>

    [!code-xml[Main](running-v1-and-v2-sites-side-by-side/samples/sample1.xml)]
  <span data-ttu-id="b6ff7-122">-如果未指定的版本中*web.config*文件中，将站点部署为最新版本。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-122">\`- If you do not specify a version in the *web.config* file, a site is deployed as the latest version.</span></span> <span data-ttu-id="b6ff7-123">(程序集复制到*bin*已部署站点中的文件夹。)</span><span class="sxs-lookup"><span data-stu-id="b6ff7-123">(The assemblies are copied to the *bin* folder in the deployed site.)</span></span>
- <span data-ttu-id="b6ff7-124">创建使用 Web Matrix 中的站点模板的新应用程序在站点中包括网页版程序集*bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-124">New applications that you create using the site templates in Web Matrix include the Web Pages version assemblies in the site's *bin* folder.</span></span>

<span data-ttu-id="b6ff7-125">一般情况下，您可以始终控制 Web 页以使用你的网站，通过使用 NuGet 将相应的程序集安装到站点的哪些版本*bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-125">In general, you can always control which version of Web Pages to use with your site by using NuGet to install the appropriate assemblies into the site's *bin* folder.</span></span> <span data-ttu-id="b6ff7-126">若要查找程序包，请访问[NuGet.org](http://NuGet.org)。</span><span class="sxs-lookup"><span data-stu-id="b6ff7-126">To find packages, visit [NuGet.org](http://NuGet.org).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b6ff7-127">其他资源</span><span class="sxs-lookup"><span data-stu-id="b6ff7-127">Additional Resources</span></span>

[<span data-ttu-id="b6ff7-128">ASP.NET Web Pages 2 中的常用功能</span><span class="sxs-lookup"><span data-stu-id="b6ff7-128">The Top Features in ASP.NET Web Pages 2</span></span>](top-features-in-web-pages-2.md)
