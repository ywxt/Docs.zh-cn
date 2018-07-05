---
title: ASP.NET Core 目录结构
author: guardrex
description: 了解已发布的 ASP.NET Core 应用的目录结构。
ms.author: riande
ms.custom: mvc
ms.date: 04/09/2018
uid: host-and-deploy/directory-structure
ms.openlocfilehash: 8e2693397f826d0e9a36ff52aa1d1d623b31043d
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2018
ms.locfileid: "36960822"
---
# <a name="aspnet-core-directory-structure"></a><span data-ttu-id="83ad9-103">ASP.NET Core 目录结构</span><span class="sxs-lookup"><span data-stu-id="83ad9-103">ASP.NET Core directory structure</span></span>

<span data-ttu-id="83ad9-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="83ad9-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="83ad9-105">在 ASP.NET Core 中，发布的应用程序目录 publish 由应用程序文件、配置文件、静态资产、程序包和运行时（适用于[独立部署](/dotnet/core/deploying/#self-contained-deployments-scd)）组成。</span><span class="sxs-lookup"><span data-stu-id="83ad9-105">In ASP.NET Core, the published application directory, *publish*, is comprised of application files, config files, static assets, packages, and the runtime (for [self-contained deployments](/dotnet/core/deploying/#self-contained-deployments-scd)).</span></span>


| <span data-ttu-id="83ad9-106">应用类型</span><span class="sxs-lookup"><span data-stu-id="83ad9-106">App Type</span></span> | <span data-ttu-id="83ad9-107">目录结构</span><span class="sxs-lookup"><span data-stu-id="83ad9-107">Directory Structure</span></span> |
| -------- | ------------------- |
| [<span data-ttu-id="83ad9-108">依赖框架的部署</span><span class="sxs-lookup"><span data-stu-id="83ad9-108">Framework-dependent Deployment</span></span>](/dotnet/core/deploying/#framework-dependent-deployments-fdd) | <ul><li><span data-ttu-id="83ad9-109">publish&dagger;</span><span class="sxs-lookup"><span data-stu-id="83ad9-109">publish&dagger;</span></span><ul><li><span data-ttu-id="83ad9-110">Logs&dagger;（除非需要接收 stdout 日志，否则为可选）</span><span class="sxs-lookup"><span data-stu-id="83ad9-110">Logs&dagger; (optional unless required to receive stdout logs)</span></span></li><li><span data-ttu-id="83ad9-111">Views&dagger;（MVC 应用；如果未预编译视图）</span><span class="sxs-lookup"><span data-stu-id="83ad9-111">Views&dagger; (MVC apps; if views aren't precompiled)</span></span></li><li><span data-ttu-id="83ad9-112">Pages&dagger;（MVC 或 Razor 页应用；如果未预编译页）</span><span class="sxs-lookup"><span data-stu-id="83ad9-112">Pages&dagger; (MVC or Razor Pages apps; if pages aren't precompiled)</span></span></li><li><span data-ttu-id="83ad9-113">wwwroot&dagger;</span><span class="sxs-lookup"><span data-stu-id="83ad9-113">wwwroot&dagger;</span></span></li><li><span data-ttu-id="83ad9-114">\*\.dll 文件</span><span class="sxs-lookup"><span data-stu-id="83ad9-114">\*\.dll files</span></span></li><li><span data-ttu-id="83ad9-115">\<assembly-name>.deps.json</span><span class="sxs-lookup"><span data-stu-id="83ad9-115">\<assembly-name>.deps.json</span></span></li><li><span data-ttu-id="83ad9-116">\<assembly-name>.dll</span><span class="sxs-lookup"><span data-stu-id="83ad9-116">\<assembly-name>.dll</span></span></li><li><span data-ttu-id="83ad9-117">\<assembly-name>.pdb</span><span class="sxs-lookup"><span data-stu-id="83ad9-117">\<assembly-name>.pdb</span></span></li><li><span data-ttu-id="83ad9-118">\<assembly-name>.PrecompiledViews.dll</span><span class="sxs-lookup"><span data-stu-id="83ad9-118">\<assembly-name>.PrecompiledViews.dll</span></span></li><li><span data-ttu-id="83ad9-119">\<assembly-name>.PrecompiledViews.pdb</span><span class="sxs-lookup"><span data-stu-id="83ad9-119">\<assembly-name>.PrecompiledViews.pdb</span></span></li><li><span data-ttu-id="83ad9-120">\<assembly-name>.runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="83ad9-120">\<assembly-name>.runtimeconfig.json</span></span></li><li><span data-ttu-id="83ad9-121">web.config（IIS 部署）</span><span class="sxs-lookup"><span data-stu-id="83ad9-121">web.config (IIS deployments)</span></span></li></ul></li></ul> |
| [<span data-ttu-id="83ad9-122">独立部署</span><span class="sxs-lookup"><span data-stu-id="83ad9-122">Self-contained Deployment</span></span>](/dotnet/core/deploying/#self-contained-deployments-scd) | <ul><li><span data-ttu-id="83ad9-123">publish&dagger;</span><span class="sxs-lookup"><span data-stu-id="83ad9-123">publish&dagger;</span></span><ul><li><span data-ttu-id="83ad9-124">Logs&dagger;（除非需要接收 stdout 日志，否则为可选）</span><span class="sxs-lookup"><span data-stu-id="83ad9-124">Logs&dagger; (optional unless required to receive stdout logs)</span></span></li><li><span data-ttu-id="83ad9-125">refs&dagger;</span><span class="sxs-lookup"><span data-stu-id="83ad9-125">refs&dagger;</span></span></li><li><span data-ttu-id="83ad9-126">Views&dagger;（MVC 应用；如果未预编译视图）</span><span class="sxs-lookup"><span data-stu-id="83ad9-126">Views&dagger; (MVC apps; if views aren't precompiled)</span></span></li><li><span data-ttu-id="83ad9-127">Pages&dagger;（MVC 或 Razor 页应用；如果未预编译页）</span><span class="sxs-lookup"><span data-stu-id="83ad9-127">Pages&dagger; (MVC or Razor Pages apps; if pages aren't precompiled)</span></span></li><li><span data-ttu-id="83ad9-128">wwwroot&dagger;</span><span class="sxs-lookup"><span data-stu-id="83ad9-128">wwwroot&dagger;</span></span></li><li><span data-ttu-id="83ad9-129">\*.dll 文件</span><span class="sxs-lookup"><span data-stu-id="83ad9-129">\*.dll files</span></span></li><li><span data-ttu-id="83ad9-130">\<assembly-name>.deps.json</span><span class="sxs-lookup"><span data-stu-id="83ad9-130">\<assembly-name>.deps.json</span></span></li><li><span data-ttu-id="83ad9-131">\<assembly-name>.exe</span><span class="sxs-lookup"><span data-stu-id="83ad9-131">\<assembly-name>.exe</span></span></li><li><span data-ttu-id="83ad9-132">\<assembly-name>.pdb</span><span class="sxs-lookup"><span data-stu-id="83ad9-132">\<assembly-name>.pdb</span></span></li><li><span data-ttu-id="83ad9-133">\<assembly-name>.PrecompiledViews.dll</span><span class="sxs-lookup"><span data-stu-id="83ad9-133">\<assembly-name>.PrecompiledViews.dll</span></span></li><li><span data-ttu-id="83ad9-134">\<assembly-name>.PrecompiledViews.pdb</span><span class="sxs-lookup"><span data-stu-id="83ad9-134">\<assembly-name>.PrecompiledViews.pdb</span></span></li><li><span data-ttu-id="83ad9-135">\<assembly-name>.runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="83ad9-135">\<assembly-name>.runtimeconfig.json</span></span></li><li><span data-ttu-id="83ad9-136">web.config（IIS 部署）</span><span class="sxs-lookup"><span data-stu-id="83ad9-136">web.config (IIS deployments)</span></span></li></ul></li></ul> |

<span data-ttu-id="83ad9-137">&dagger;指示目录</span><span class="sxs-lookup"><span data-stu-id="83ad9-137">&dagger;Indicates a directory</span></span>

<span data-ttu-id="83ad9-138">publish 目录代表部署的内容根路径，也称为应用程序基路径。</span><span class="sxs-lookup"><span data-stu-id="83ad9-138">The *publish* directory represents the *content root path*, also called the *application base path*, of the deployment.</span></span> <span data-ttu-id="83ad9-139">无论对服务器上已部署应用的 publish 目录如何命名，其位置都可作为托管应用的服务器物理路径。</span><span class="sxs-lookup"><span data-stu-id="83ad9-139">Whatever name is given to the *publish* directory of the deployed app on the server, its location serves as the server's physical path to the hosted app.</span></span>

<span data-ttu-id="83ad9-140">wwwroot 目录（如果存在）仅包含静态资产。</span><span class="sxs-lookup"><span data-stu-id="83ad9-140">The *wwwroot* directory, if present, only contains static assets.</span></span>

<span data-ttu-id="83ad9-141">可以使用以下两种方法之一为部署创建 stdout Logs 目录：</span><span class="sxs-lookup"><span data-stu-id="83ad9-141">The stdout *Logs* directory can be created for the deployment using one of the following two approaches:</span></span>

* <span data-ttu-id="83ad9-142">向项目添加以下 `<Target>` 元素：</span><span class="sxs-lookup"><span data-stu-id="83ad9-142">Add the following `<Target>` element to the project file:</span></span>

   ```xml
   <Target Name="CreateLogsFolder" AfterTargets="Publish">
     <MakeDir Directories="$(PublishDir)Logs" 
              Condition="!Exists('$(PublishDir)Logs')" />
     <WriteLinesToFile File="$(PublishDir)Logs\.log" 
                       Lines="Generated file" 
                       Overwrite="True" 
                       Condition="!Exists('$(PublishDir)Logs\.log')" />
   </Target>
   ```

   <span data-ttu-id="83ad9-143">`<MakeDir>` 元素在发布的输出中创建一个空的 Logs 文件夹。</span><span class="sxs-lookup"><span data-stu-id="83ad9-143">The `<MakeDir>` element creates an empty *Logs* folder in the published output.</span></span> <span data-ttu-id="83ad9-144">该元素使用 `PublishDir` 属性来确定创建文件夹的目标位置。</span><span class="sxs-lookup"><span data-stu-id="83ad9-144">The element uses the `PublishDir` property to determine the target location for creating the folder.</span></span> <span data-ttu-id="83ad9-145">几种部署方法（如 Web 部署）均在部署期间跳过空文件夹。</span><span class="sxs-lookup"><span data-stu-id="83ad9-145">Several deployment methods, such as Web Deploy, skip empty folders during deployment.</span></span> <span data-ttu-id="83ad9-146">`<WriteLinesToFile>` 元素在 Logs 文件夹中生成一个文件，该文件可确保将文件夹部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="83ad9-146">The `<WriteLinesToFile>` element generates a file in the *Logs* folder, which guarantees deployment of the folder to the server.</span></span> <span data-ttu-id="83ad9-147">注意，如果工作进程不具有对目标文件夹的写入权限，那么文件夹创建可能仍会失败。</span><span class="sxs-lookup"><span data-stu-id="83ad9-147">Note that folder creation may still fail if the worker process doesn't have write access to the target folder.</span></span>

* <span data-ttu-id="83ad9-148">在部署中的服务器上物理创建 Logs 目录。</span><span class="sxs-lookup"><span data-stu-id="83ad9-148">Physically create the *Logs* directory on the server in the deployment.</span></span>

<span data-ttu-id="83ad9-149">部署目录需要读取/执行权限。</span><span class="sxs-lookup"><span data-stu-id="83ad9-149">The deployment directory requires Read/Execute permissions.</span></span> <span data-ttu-id="83ad9-150">Logs 目录需要读/写权限。</span><span class="sxs-lookup"><span data-stu-id="83ad9-150">The *Logs* directory requires Read/Write permissions.</span></span> <span data-ttu-id="83ad9-151">将文件写入其他目录需要读/写权限。</span><span class="sxs-lookup"><span data-stu-id="83ad9-151">Additional directories where files are written require Read/Write permissions.</span></span>
