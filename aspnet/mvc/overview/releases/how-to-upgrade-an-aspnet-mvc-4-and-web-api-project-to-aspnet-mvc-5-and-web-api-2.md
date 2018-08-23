---
uid: mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2
title: 如何升级 ASP.NET MVC 4 和 Web API 项目到 ASP.NET MVC 5 和 Web API 2 |Microsoft Docs
author: Rick-Anderson
description: ASP.NET MVC 5 和 Web API 2 引入的新功能，包括属性路由、 身份验证筛选器和更多的主机。
ms.author: riande
ms.date: 10/17/2013
ms.assetid: db0d02d9-58e8-4a0b-8d7d-b8df8ea97b88
msc.legacyurl: /mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: e313fc2229026f1b11d2f6a046a8b550c08ba96b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834550"
---
<a name="how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2"></a><span data-ttu-id="7f06b-103">如何将 ASP.NET MVC 4 和 Web API 项目升级到 ASP.NET MVC 5 和 Web API 2</span><span class="sxs-lookup"><span data-stu-id="7f06b-103">How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2</span></span>
====================
<span data-ttu-id="7f06b-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="7f06b-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="7f06b-105">ASP.NET MVC 5 和 Web API 2 引入的新功能，包括属性路由、 身份验证筛选器和更多的主机。</span><span class="sxs-lookup"><span data-stu-id="7f06b-105">ASP.NET MVC 5 and Web API 2 bring a host of new features, including attribute routing, authentication filters, and much more.</span></span> <span data-ttu-id="7f06b-106">请参阅[ https://www.asp.net/vnext ](https://www.asp.net/core)的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="7f06b-106">See [https://www.asp.net/vnext](https://www.asp.net/core) for more details.</span></span>
> 
> <span data-ttu-id="7f06b-107">本演练将指导你执行升级到最新版本的应用程序所需的步骤。</span><span class="sxs-lookup"><span data-stu-id="7f06b-107">This walkthrough will guide you with the steps required to upgrade your application to the latest version.</span></span>  
> 
> > [!NOTE]
> > <span data-ttu-id="7f06b-108">请参阅[ASP.NET 和 Web Tools for Visual Studio 2013 发行说明](../../../visual-studio/overview/2013/release-notes.md)的重大更改从 MVC 4 和 Web API 到下一版本的信息。</span><span class="sxs-lookup"><span data-stu-id="7f06b-108">Please see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../visual-studio/overview/2013/release-notes.md) for information on breaking changes from MVC 4 and Web API to the next version.</span></span>
> 
>   
> 
> <span data-ttu-id="7f06b-109">通过 Youngjune 香港和 Rick Anderson 撰写本文时 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )</span><span class="sxs-lookup"><span data-stu-id="7f06b-109">This article was written by Youngjune Hong and Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )</span></span>


## <a name="upgrade-steps"></a><span data-ttu-id="7f06b-110">升级步骤</span><span class="sxs-lookup"><span data-stu-id="7f06b-110">Upgrade Steps</span></span>

1. <span data-ttu-id="7f06b-111">备份你的项目。</span><span class="sxs-lookup"><span data-stu-id="7f06b-111">Backup your project.</span></span> <span data-ttu-id="7f06b-112">本演练将要求您对项目文件、 包配置和 web.config 文件进行更改。</span><span class="sxs-lookup"><span data-stu-id="7f06b-112">This walkthrough will require you to make changes to your project file, package configuration, and web.config files.</span></span>
2. <span data-ttu-id="7f06b-113">对于 Web API 从升级到 Web API 2，在 global.asax 中，更改：</span><span class="sxs-lookup"><span data-stu-id="7f06b-113">For upgrading from Web API to Web API 2, in global.asax, change:</span></span>

    [!code-csharp[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample1.cs)]

   <span data-ttu-id="7f06b-114">更改为</span><span class="sxs-lookup"><span data-stu-id="7f06b-114">to</span></span>

    [!code-csharp[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample2.cs)]
3. <span data-ttu-id="7f06b-115">请确保你的项目使用的所有包都都与 MVC 5 和 Web API 2 兼容。</span><span class="sxs-lookup"><span data-stu-id="7f06b-115">Make sure all the packages that your projects use are compatible with MVC 5 and Web API 2.</span></span> <span data-ttu-id="7f06b-116">下表显示了 MVC 4 和 Web API 相关的包不是需要进行更改。</span><span class="sxs-lookup"><span data-stu-id="7f06b-116">The following table shows the MVC 4 and Web API related packages than need to be changed.</span></span> <span data-ttu-id="7f06b-117">如果必须依赖一个下面列出的包的包，请联系以获取与 MVC 5 和 Web API 2 兼容的较新版本的发布服务器。</span><span class="sxs-lookup"><span data-stu-id="7f06b-117">If you have a package that is dependent on one of the packages listed below, please contact the publishers to get the newer versions that are compatible with MVC 5 and Web API 2.</span></span> <span data-ttu-id="7f06b-118">如果你具有这些包的源代码，应该的 MVC 5 和 Web API 2 的新程序集时将它们重新编译。</span><span class="sxs-lookup"><span data-stu-id="7f06b-118">If you have the source code for those packages, you should recompile them with the new assemblies of MVC 5 and Web API 2.</span></span>   

    | <span data-ttu-id="7f06b-119">**包 Id**</span><span class="sxs-lookup"><span data-stu-id="7f06b-119">**Package Id**</span></span> | <span data-ttu-id="7f06b-120">**旧版本**</span><span class="sxs-lookup"><span data-stu-id="7f06b-120">**Old version**</span></span> | <span data-ttu-id="7f06b-121">**新版本**</span><span class="sxs-lookup"><span data-stu-id="7f06b-121">**New version**</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="7f06b-122">Microsoft.AspNet.Razor</span><span class="sxs-lookup"><span data-stu-id="7f06b-122">Microsoft.AspNet.Razor</span></span> | <span data-ttu-id="7f06b-123">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-123">2.0.x.x</span></span> | <span data-ttu-id="7f06b-124">3.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-124">3.0.0</span></span> |
    | <span data-ttu-id="7f06b-125">Microsoft.AspNet.WebPages</span><span class="sxs-lookup"><span data-stu-id="7f06b-125">Microsoft.AspNet.WebPages</span></span> | <span data-ttu-id="7f06b-126">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-126">2.0.x.x</span></span> | <span data-ttu-id="7f06b-127">3.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-127">3.0.0</span></span> |
    | <span data-ttu-id="7f06b-128">Microsoft.AspNet.WebPages.WebData</span><span class="sxs-lookup"><span data-stu-id="7f06b-128">Microsoft.AspNet.WebPages.WebData</span></span> | <span data-ttu-id="7f06b-129">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-129">2.0.x.x</span></span> | <span data-ttu-id="7f06b-130">3.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-130">3.0.0</span></span> |
    | <span data-ttu-id="7f06b-131">Microsoft.AspNet.WebPages.OAuth</span><span class="sxs-lookup"><span data-stu-id="7f06b-131">Microsoft.AspNet.WebPages.OAuth</span></span> | <span data-ttu-id="7f06b-132">2.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-132">2.0.x.x</span></span> | <span data-ttu-id="7f06b-133">3.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-133">3.0.0</span></span> |
    | <span data-ttu-id="7f06b-134">Microsoft.AspNet.Mvc</span><span class="sxs-lookup"><span data-stu-id="7f06b-134">Microsoft.AspNet.Mvc</span></span> | <span data-ttu-id="7f06b-135">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-135">4.0.x.x</span></span> | <span data-ttu-id="7f06b-136">5.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-136">5.0.0</span></span> |
    | <span data-ttu-id="7f06b-137">Microsoft.AspNet.Mvc.Facebook</span><span class="sxs-lookup"><span data-stu-id="7f06b-137">Microsoft.AspNet.Mvc.Facebook</span></span> | <span data-ttu-id="7f06b-138">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-138">4.0.x.x</span></span> | <span data-ttu-id="7f06b-139">5.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-139">5.0.0</span></span> |
    | <span data-ttu-id="7f06b-140">Microsoft.AspNet.WebApi.Core</span><span class="sxs-lookup"><span data-stu-id="7f06b-140">Microsoft.AspNet.WebApi.Core</span></span> | <span data-ttu-id="7f06b-141">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-141">4.0.x.x</span></span> | <span data-ttu-id="7f06b-142">5.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-142">5.0.0</span></span> |
    | <span data-ttu-id="7f06b-143">Microsoft.AspNet.WebApi.SelfHost</span><span class="sxs-lookup"><span data-stu-id="7f06b-143">Microsoft.AspNet.WebApi.SelfHost</span></span> | <span data-ttu-id="7f06b-144">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-144">4.0.x.x</span></span> | <span data-ttu-id="7f06b-145">5.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-145">5.0.0</span></span> |
    | <span data-ttu-id="7f06b-146">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="7f06b-146">Microsoft.AspNet.WebApi.Client</span></span> | <span data-ttu-id="7f06b-147">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-147">4.0.x.x</span></span> | <span data-ttu-id="7f06b-148">5.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-148">5.0.0</span></span> |
    | <span data-ttu-id="7f06b-149">Microsoft.AspNet.WebApi.OData</span><span class="sxs-lookup"><span data-stu-id="7f06b-149">Microsoft.AspNet.WebApi.OData</span></span> | <span data-ttu-id="7f06b-150">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-150">4.0.x.x</span></span> | <span data-ttu-id="7f06b-151">5.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-151">5.0.0</span></span> |
    | <span data-ttu-id="7f06b-152">Microsoft.AspNet.WebApi</span><span class="sxs-lookup"><span data-stu-id="7f06b-152">Microsoft.AspNet.WebApi</span></span> | <span data-ttu-id="7f06b-153">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-153">4.0.x.x</span></span> | <span data-ttu-id="7f06b-154">5.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-154">5.0.0</span></span> |
    | <span data-ttu-id="7f06b-155">Microsoft.AspNet.WebApi.WebHost</span><span class="sxs-lookup"><span data-stu-id="7f06b-155">Microsoft.AspNet.WebApi.WebHost</span></span> | <span data-ttu-id="7f06b-156">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-156">4.0.x.x</span></span> | <span data-ttu-id="7f06b-157">5.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-157">5.0.0</span></span> |
    | <span data-ttu-id="7f06b-158">Microsoft.AspNet.WebApi.Tracing</span><span class="sxs-lookup"><span data-stu-id="7f06b-158">Microsoft.AspNet.WebApi.Tracing</span></span> | <span data-ttu-id="7f06b-159">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-159">4.0.x.x</span></span> | <span data-ttu-id="7f06b-160">5.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-160">5.0.0</span></span> |
    | <span data-ttu-id="7f06b-161">Microsoft.AspNet.WebApi.HelpPage</span><span class="sxs-lookup"><span data-stu-id="7f06b-161">Microsoft.AspNet.WebApi.HelpPage</span></span> | <span data-ttu-id="7f06b-162">4.0.x.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-162">4.0.x.x</span></span> | <span data-ttu-id="7f06b-163">5.0.0</span><span class="sxs-lookup"><span data-stu-id="7f06b-163">5.0.0</span></span> |
    | <span data-ttu-id="7f06b-164">Microsoft.Net.Http</span><span class="sxs-lookup"><span data-stu-id="7f06b-164">Microsoft.Net.Http</span></span> | <span data-ttu-id="7f06b-165">2.0.x。</span><span class="sxs-lookup"><span data-stu-id="7f06b-165">2.0.x.</span></span> | <span data-ttu-id="7f06b-166">2.2.x。</span><span class="sxs-lookup"><span data-stu-id="7f06b-166">2.2.x.</span></span> |
    | <span data-ttu-id="7f06b-167">Microsoft.Data.OData</span><span class="sxs-lookup"><span data-stu-id="7f06b-167">Microsoft.Data.OData</span></span> | <span data-ttu-id="7f06b-168">5.2.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-168">5.2.x</span></span> | <span data-ttu-id="7f06b-169">5.6.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-169">5.6.x</span></span> |
    | <span data-ttu-id="7f06b-170">System.Spatial</span><span class="sxs-lookup"><span data-stu-id="7f06b-170">System.Spatial</span></span> | <span data-ttu-id="7f06b-171">5.2.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-171">5.2.x</span></span> | <span data-ttu-id="7f06b-172">5.6.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-172">5.6.x</span></span> |
    | <span data-ttu-id="7f06b-173">Microsoft.Data.Edm</span><span class="sxs-lookup"><span data-stu-id="7f06b-173">Microsoft.Data.Edm</span></span> | <span data-ttu-id="7f06b-174">5.2.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-174">5.2.x</span></span> | <span data-ttu-id="7f06b-175">5.6.x</span><span class="sxs-lookup"><span data-stu-id="7f06b-175">5.6.x</span></span> |
    | <span data-ttu-id="7f06b-176">Microsoft.AspNet.Mvc.FixedDisplayModes</span><span class="sxs-lookup"><span data-stu-id="7f06b-176">Microsoft.AspNet.Mvc.FixedDisplayModes</span></span> | <span data-ttu-id="7f06b-177">< o:p >< / o:p ></span><span class="sxs-lookup"><span data-stu-id="7f06b-177"><o:p> </o:p></span></span> | <span data-ttu-id="7f06b-178">已删除</span><span class="sxs-lookup"><span data-stu-id="7f06b-178">Removed</span></span> |
    | <span data-ttu-id="7f06b-179">Microsoft.AspNet.WebPages.Administration</span><span class="sxs-lookup"><span data-stu-id="7f06b-179">Microsoft.AspNet.WebPages.Administration</span></span> | <span data-ttu-id="7f06b-180">< o:p >< / o:p ></span><span class="sxs-lookup"><span data-stu-id="7f06b-180"><o:p> </o:p></span></span> | <span data-ttu-id="7f06b-181">已删除</span><span class="sxs-lookup"><span data-stu-id="7f06b-181">Removed</span></span> |
    | <span data-ttu-id="7f06b-182">Microsoft-Web-Helpers</span><span class="sxs-lookup"><span data-stu-id="7f06b-182">Microsoft-Web-Helpers</span></span> | <span data-ttu-id="7f06b-183">< o:p >< / o:p ></span><span class="sxs-lookup"><span data-stu-id="7f06b-183"><o:p> </o:p></span></span> | <span data-ttu-id="7f06b-184">Microsoft.AspNet.WebHelpers</span><span class="sxs-lookup"><span data-stu-id="7f06b-184">Microsoft.AspNet.WebHelpers</span></span> |

    > [!NOTE]
    > <span data-ttu-id="7f06b-185">Microsoft Web 帮助器已被 Microsoft.AspNet.WebHelpers 替换。</span><span class="sxs-lookup"><span data-stu-id="7f06b-185">Microsoft-Web-Helpers has been replaced with Microsoft.AspNet.WebHelpers.</span></span> <span data-ttu-id="7f06b-186">您应首先，请删除旧的包，然后安装较新的包。</span><span class="sxs-lookup"><span data-stu-id="7f06b-186">You should remove the old package first, and then install the newer package.</span></span>   
    >   
    > <span data-ttu-id="7f06b-187">没有跨版本兼容性，这些主要 ASP.NET 包。</span><span class="sxs-lookup"><span data-stu-id="7f06b-187">There is no cross version compatibility among major ASP.NET packages.</span></span> <span data-ttu-id="7f06b-188">例如，MVC 5 是与仅 Razor 3 和 Razor 2 不兼容。</span><span class="sxs-lookup"><span data-stu-id="7f06b-188">For example, MVC 5 is compatible with only Razor 3, and not Razor 2.</span></span>
4. <span data-ttu-id="7f06b-189">在 Visual Studio 2013 中打开你的项目。</span><span class="sxs-lookup"><span data-stu-id="7f06b-189">Open your project in Visual Studio 2013.</span></span>
5. <span data-ttu-id="7f06b-190">删除任何以下 ASP.NET NuGet 包安装。</span><span class="sxs-lookup"><span data-stu-id="7f06b-190">Remove any of the following ASP.NET NuGet packages that are installed.</span></span> <span data-ttu-id="7f06b-191">将删除这些使用包管理器控制台 (PMC)。</span><span class="sxs-lookup"><span data-stu-id="7f06b-191">You will remove these using the Package Manager Console (PMC).</span></span> <span data-ttu-id="7f06b-192">若要打开 PMC，请选择**工具**菜单，然后选择**库包管理器中，** 然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="7f06b-192">To open the PMC, select the **Tools** menu and then select **Library Package Manager,** then select **Package Manager Console**.</span></span> <span data-ttu-id="7f06b-193">你的项目可能不包括所有这些。</span><span class="sxs-lookup"><span data-stu-id="7f06b-193">Your project might not include all of these.</span></span>

    1. `Microsoft.AspNet.WebPages.Administration`  
   <span data-ttu-id="7f06b-194">从 MVC 3 升级到 MVC 4 时，通常被添加此包。</span><span class="sxs-lookup"><span data-stu-id="7f06b-194">This package is typically added when upgrading from MVC 3 to MVC 4.</span></span> <span data-ttu-id="7f06b-195">若要删除它，请在 PMC 中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="7f06b-195">To remove it, run the following command in the PMC:</span></span>  
        `Uninstall-Package -Id Microsoft.AspNet.WebPages.Administration`
    2. `Microsoft-Web-Helpers`   
   <span data-ttu-id="7f06b-196">此包有产品名称已更改为`Microsoft.AspNet.WebHelpers`。</span><span class="sxs-lookup"><span data-stu-id="7f06b-196">This package has been rebranded as `Microsoft.AspNet.WebHelpers`.</span></span> <span data-ttu-id="7f06b-197">若要删除它，请在 PMC 中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="7f06b-197">To remove it, run the following command in the PMC:</span></span>  
        `Uninstall-Package -Id Microsoft-Web-Helpers`
    3. `Microsoft.AspNet.Mvc.FixedDisplayMode`  
   <span data-ttu-id="7f06b-198">此包包含在 MVC 4 中的 MVC 5 中已修复 bug 的解决办法。</span><span class="sxs-lookup"><span data-stu-id="7f06b-198">This package contains a work around for a bug in MVC 4 that has been fixed in MVC 5.</span></span> <span data-ttu-id="7f06b-199">若要删除它，请在 PMC 中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="7f06b-199">To remove it, run the following command in the PMC:</span></span>  
        `Uninstall-Package -Id Microsoft.AspNet.Mvc.FixedDisplayModes`
6. <span data-ttu-id="7f06b-200">升级所有使用 PMC 的 ASP.NET NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="7f06b-200">Upgrade all the ASP.NET NuGet packages using the PMC.</span></span> <span data-ttu-id="7f06b-201">在 PMC 中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="7f06b-201">In the PMC, run the following command:</span></span>  
    `Update-Package`  
   <span data-ttu-id="7f06b-202">`Update-Package`命令没有任何参数将更新每个包。</span><span class="sxs-lookup"><span data-stu-id="7f06b-202">The `Update-Package` command without any parameters will update every package.</span></span> <span data-ttu-id="7f06b-203">使用 ID 参数，可以单独更新包。</span><span class="sxs-lookup"><span data-stu-id="7f06b-203">You can update packages individually by using the ID argument.</span></span> <span data-ttu-id="7f06b-204">有关更新命令的详细信息，请运行`get-help update-package`。</span><span class="sxs-lookup"><span data-stu-id="7f06b-204">For more information about the update command, run     `get-help update-package` .</span></span>

## <a name="update-the-application-webconfig-file"></a><span data-ttu-id="7f06b-205">更新应用程序*web.config*文件</span><span class="sxs-lookup"><span data-stu-id="7f06b-205">Update the Application *web.config* File</span></span>

<span data-ttu-id="7f06b-206">请务必在应用中进行这些更改*web.config*文件，不可*web.config*文件中*视图*文件夹。</span><span class="sxs-lookup"><span data-stu-id="7f06b-206">Be sure to make these changes in the app *web.config* file, not the *web.config* file in the *Views* folder.</span></span>

<span data-ttu-id="7f06b-207">找到`<runtime>/<assemblyBinding>`部分，并进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="7f06b-207">Locate the `<runtime>/<assemblyBinding>` section, and make the following changes:</span></span>

1. <span data-ttu-id="7f06b-208">在名称属性"System.Web.Mvc"具有的元素，更改版本号从"4.0.0.0"到"5.0.0.0"。</span><span class="sxs-lookup"><span data-stu-id="7f06b-208">In the elements with the name attribute "System.Web.Mvc", change the version number from "4.0.0.0" to "5.0.0.0".</span></span> <span data-ttu-id="7f06b-209">（该元素中的两个更改。）</span><span class="sxs-lookup"><span data-stu-id="7f06b-209">(Two changes in that element.)</span></span>
2. <span data-ttu-id="7f06b-210">在名称属性的元素&quot;System.Web.Helpers"和&quot;System.Web.WebPages&quot;更改版本号从"2.0.0.0"到"3.0.0.0"。</span><span class="sxs-lookup"><span data-stu-id="7f06b-210">In elements with the name attribute &quot;System.Web.Helpers" and &quot;System.Web.WebPages&quot; change the version number from "2.0.0.0" to "3.0.0.0".</span></span> <span data-ttu-id="7f06b-211">四个更改，将出现两个在每个元素。</span><span class="sxs-lookup"><span data-stu-id="7f06b-211">Four changes will occur, two in each of the elements.</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample3.xml?highlight=6,10,14)]
3. <span data-ttu-id="7f06b-212">找到`<appSettings>`部分，并更新到 3.0.0.0 从 2.0.0.0.0 webpages:version，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7f06b-212">Locate the `<appSettings>` section and update the webpages:version from 2.0.0.0.0 to 3.0.0.0 as shown below:</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample4.xml?highlight=2)]
4. <span data-ttu-id="7f06b-213">删除而不是完整的任何信任级别。</span><span class="sxs-lookup"><span data-stu-id="7f06b-213">Remove any trust levels other than Full.</span></span> <span data-ttu-id="7f06b-214">例如：</span><span class="sxs-lookup"><span data-stu-id="7f06b-214">For example:</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample5.xml?highlight=2)]

## <a name="update-the-webconfig-files-under-the-views-folder"></a><span data-ttu-id="7f06b-215">更新*web.config*视图文件夹下的文件</span><span class="sxs-lookup"><span data-stu-id="7f06b-215">Update the *web.config* files under the Views folder</span></span>

<span data-ttu-id="7f06b-216">如果你的应用程序使用的区域，将需要更新每个*web.config*中的文件*视图*每个区域文件夹的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="7f06b-216">If your application is using areas, you will also need to update each *web.config* file in the *Views* sub-folder of each Area folder.</span></span>

1. <span data-ttu-id="7f06b-217">更新到版本"5.0.0.0"从版本"4.0.0.0"包含"System.Web.Mvc"的所有元素。</span><span class="sxs-lookup"><span data-stu-id="7f06b-217">Update all elements that contain "System.Web.Mvc" from version "4.0.0.0" to version "5.0.0.0".</span></span>  

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample6.xml?highlight=2)]

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample7.xml?highlight=4-6,8)]
2. <span data-ttu-id="7f06b-218">更新到版本"3.0.0.0"从版本"2.0.0.0"包含"System.Web.WebPages.Razor"的所有元素。</span><span class="sxs-lookup"><span data-stu-id="7f06b-218">Update all elements that contain "System.Web.WebPages.Razor" from version "2.0.0.0" to version"3.0.0.0".</span></span> <span data-ttu-id="7f06b-219">如果本部分包含"System.Web.WebPages"，更新到版本"3.0.0.0"从版本"2.0.0.0"这些元素</span><span class="sxs-lookup"><span data-stu-id="7f06b-219">If this section contains "System.Web.WebPages", update those elements from version "2.0.0.0" to version"3.0.0.0"</span></span>  

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample8.xml?highlight=3-5)]
3. <span data-ttu-id="7f06b-220">如果你删除`Microsoft-Web-Helpers`NuGet 包在上一步骤中，安装`Microsoft.AspNet.WebHelpers`PMC 中的以下命令：</span><span class="sxs-lookup"><span data-stu-id="7f06b-220">If you removed the `Microsoft-Web-Helpers` NuGet package in a previous step, install `Microsoft.AspNet.WebHelpers` with the following command in the PMC:</span></span>  
    `Install-Package -Id Microsoft.AspNet.WebHelpers`
4. <span data-ttu-id="7f06b-221">如果您的应用程序使用[User.IsInRole()](https://msdn.microsoft.com/en-us/library/system.web.security.roleprincipal.isinrole(v=vs.110).aspx)方法中，添加以下*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="7f06b-221">If your app uses the [User.IsInRole()](https://msdn.microsoft.com/en-us/library/system.web.security.roleprincipal.isinrole(v=vs.110).aspx) method, add the following to the *Web.config* file.</span></span>

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample9.xml)]

## <a name="final-steps"></a><span data-ttu-id="7f06b-222">最后的步骤</span><span class="sxs-lookup"><span data-stu-id="7f06b-222">Final Steps</span></span>

<span data-ttu-id="7f06b-223">生成和测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="7f06b-223">Build and test the application.</span></span>

<span data-ttu-id="7f06b-224">从项目文件中删除的 MVC 4 项目类型 GUID。</span><span class="sxs-lookup"><span data-stu-id="7f06b-224">Remove the MVC 4 project type GUID from the project files.</span></span>

1. <span data-ttu-id="7f06b-225">在解决方案资源管理器，右键单击项目名称，然后选择**卸载项目**。</span><span class="sxs-lookup"><span data-stu-id="7f06b-225">In Solution Explorer, right-click the project name and then select **Unload Project**.</span></span>
2. <span data-ttu-id="7f06b-226">右键单击该项目并选择编辑项目名.csproj。</span><span class="sxs-lookup"><span data-stu-id="7f06b-226">Right-click the project and select Edit ProjectName.csproj.</span></span>
3. <span data-ttu-id="7f06b-227">找到`ProjectTypeGuids`元素，然后删除 MVC 4 项目 GUID、 `{E3E379DF-F4C6-4180-9B81-6769533ABE47}`。</span><span class="sxs-lookup"><span data-stu-id="7f06b-227">Locate the `ProjectTypeGuids` element and then remove the MVC 4 project GUID, `{E3E379DF-F4C6-4180-9B81-6769533ABE47}`.</span></span>
4. <span data-ttu-id="7f06b-228">保存并关闭打开的项目文件。</span><span class="sxs-lookup"><span data-stu-id="7f06b-228">Save and close the open project file.</span></span>
5. <span data-ttu-id="7f06b-229">右键单击项目并选择**重新加载项目**。</span><span class="sxs-lookup"><span data-stu-id="7f06b-229">Right-click the project and select **Reload Project**.</span></span>
