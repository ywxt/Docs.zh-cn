---
title: ASP.NET Core 目录结构
author: guardrex
description: 了解已发布的 ASP.NET Core 应用的目录结构。
ms.author: riande
ms.custom: mvc
ms.date: 04/09/2018
uid: host-and-deploy/directory-structure
ms.openlocfilehash: 06d3f097cd93ceb2a23b9f6516a9b7a1f3ca3089
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36273668"
---
# <a name="aspnet-core-directory-structure"></a><span data-ttu-id="73169-103">ASP.NET Core 目录结构</span><span class="sxs-lookup"><span data-stu-id="73169-103">ASP.NET Core directory structure</span></span>

<span data-ttu-id="73169-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="73169-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="73169-105">在 ASP.NET Core 中，发布的应用程序目录 publish 由应用程序文件、配置文件、静态资产、程序包和运行时（适用于[独立部署](/dotnet/core/deploying/#self-contained-deployments-scd)）组成。</span><span class="sxs-lookup"><span data-stu-id="73169-105">In ASP.NET Core, the published application directory, *publish*, is comprised of application files, config files, static assets, packages, and the runtime (for [self-contained deployments](/dotnet/core/deploying/#self-contained-deployments-scd)).</span></span>


| <span data-ttu-id="73169-106">应用类型</span><span class="sxs-lookup"><span data-stu-id="73169-106">App Type</span></span> | <span data-ttu-id="73169-107">目录结构</span><span class="sxs-lookup"><span data-stu-id="73169-107">Directory Structure</span></span> |
| -------- | ------------------- |
| [<span data-ttu-id="73169-108">依赖框架的部署</span><span class="sxs-lookup"><span data-stu-id="73169-108">Framework-dependent Deployment</span></span>](/dotnet/core/deploying/#framework-dependent-deployments-fdd) | <ul><li><span data-ttu-id="73169-109">publish&dagger;</span><span class="sxs-lookup"><span data-stu-id="73169-109">publish&dagger;</span></span><ul><li><span data-ttu-id="73169-110">logs&dagger;（除非需要接收 stdout 日志，否则为可选）</span><span class="sxs-lookup"><span data-stu-id="73169-110">logs&dagger; (optional unless required to receive stdout logs)</span></span></li><li><span data-ttu-id="73169-111">Views&dagger;（MVC 应用；如果未预编译视图）</span><span class="sxs-lookup"><span data-stu-id="73169-111">Views&dagger; (MVC apps; if views aren't precompiled)</span></span></li><li><span data-ttu-id="73169-112">Pages&dagger;（MVC 或 Razor 页应用；如果未预编译页）</span><span class="sxs-lookup"><span data-stu-id="73169-112">Pages&dagger; (MVC or Razor Pages apps; if pages aren't precompiled)</span></span></li><li><span data-ttu-id="73169-113">wwwroot&dagger;</span><span class="sxs-lookup"><span data-stu-id="73169-113">wwwroot&dagger;</span></span></li><li><span data-ttu-id="73169-114">\*\.dll 文件</span><span class="sxs-lookup"><span data-stu-id="73169-114">\*\.dll files</span></span></li><li><span data-ttu-id="73169-115">\<assembly-name>.deps.json</span><span class="sxs-lookup"><span data-stu-id="73169-115">\<assembly-name>.deps.json</span></span></li><li><span data-ttu-id="73169-116">\<assembly-name>.dll</span><span class="sxs-lookup"><span data-stu-id="73169-116">\<assembly-name>.dll</span></span></li><li><span data-ttu-id="73169-117">\<assembly-name>.pdb</span><span class="sxs-lookup"><span data-stu-id="73169-117">\<assembly-name>.pdb</span></span></li><li><span data-ttu-id="73169-118">\<assembly-name>.PrecompiledViews.dll</span><span class="sxs-lookup"><span data-stu-id="73169-118">\<assembly-name>.PrecompiledViews.dll</span></span></li><li><span data-ttu-id="73169-119">\<assembly-name>.PrecompiledViews.pdb</span><span class="sxs-lookup"><span data-stu-id="73169-119">\<assembly-name>.PrecompiledViews.pdb</span></span></li><li><span data-ttu-id="73169-120">\<assembly-name>.runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="73169-120">\<assembly-name>.runtimeconfig.json</span></span></li><li><span data-ttu-id="73169-121">web.config（IIS 部署）</span><span class="sxs-lookup"><span data-stu-id="73169-121">web.config (IIS deployments)</span></span></li></ul></li></ul> |
| [<span data-ttu-id="73169-122">独立部署</span><span class="sxs-lookup"><span data-stu-id="73169-122">Self-contained Deployment</span></span>](/dotnet/core/deploying/#self-contained-deployments-scd) | <ul><li><span data-ttu-id="73169-123">publish&dagger;</span><span class="sxs-lookup"><span data-stu-id="73169-123">publish&dagger;</span></span><ul><li><span data-ttu-id="73169-124">logs&dagger;（除非需要接收 stdout 日志，否则为可选）</span><span class="sxs-lookup"><span data-stu-id="73169-124">logs&dagger; (optional unless required to receive stdout logs)</span></span></li><li><span data-ttu-id="73169-125">refs&dagger;</span><span class="sxs-lookup"><span data-stu-id="73169-125">refs&dagger;</span></span></li><li><span data-ttu-id="73169-126">Views&dagger;（MVC 应用；如果未预编译视图）</span><span class="sxs-lookup"><span data-stu-id="73169-126">Views&dagger; (MVC apps; if views aren't precompiled)</span></span></li><li><span data-ttu-id="73169-127">Pages&dagger;（MVC 或 Razor 页应用；如果未预编译页）</span><span class="sxs-lookup"><span data-stu-id="73169-127">Pages&dagger; (MVC or Razor Pages apps; if pages aren't precompiled)</span></span></li><li><span data-ttu-id="73169-128">wwwroot&dagger;</span><span class="sxs-lookup"><span data-stu-id="73169-128">wwwroot&dagger;</span></span></li><li><span data-ttu-id="73169-129">\*.dll 文件</span><span class="sxs-lookup"><span data-stu-id="73169-129">\*.dll files</span></span></li><li><span data-ttu-id="73169-130">\<assembly-name>.deps.json</span><span class="sxs-lookup"><span data-stu-id="73169-130">\<assembly-name>.deps.json</span></span></li><li><span data-ttu-id="73169-131">\<assembly-name>.exe</span><span class="sxs-lookup"><span data-stu-id="73169-131">\<assembly-name>.exe</span></span></li><li><span data-ttu-id="73169-132">\<assembly-name>.pdb</span><span class="sxs-lookup"><span data-stu-id="73169-132">\<assembly-name>.pdb</span></span></li><li><span data-ttu-id="73169-133">\<assembly-name>.PrecompiledViews.dll</span><span class="sxs-lookup"><span data-stu-id="73169-133">\<assembly-name>.PrecompiledViews.dll</span></span></li><li><span data-ttu-id="73169-134">\<assembly-name>.PrecompiledViews.pdb</span><span class="sxs-lookup"><span data-stu-id="73169-134">\<assembly-name>.PrecompiledViews.pdb</span></span></li><li><span data-ttu-id="73169-135">\<assembly-name>.runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="73169-135">\<assembly-name>.runtimeconfig.json</span></span></li><li><span data-ttu-id="73169-136">web.config（IIS 部署）</span><span class="sxs-lookup"><span data-stu-id="73169-136">web.config (IIS deployments)</span></span></li></ul></li></ul> |

<span data-ttu-id="73169-137">&dagger;指示目录</span><span class="sxs-lookup"><span data-stu-id="73169-137">&dagger;Indicates a directory</span></span>

<span data-ttu-id="73169-138">publish 目录代表部署的内容根路径，也称为应用程序基路径。</span><span class="sxs-lookup"><span data-stu-id="73169-138">The *publish* directory represents the *content root path*, also called the *application base path*, of the deployment.</span></span> <span data-ttu-id="73169-139">无论对服务器上已部署应用的 publish 目录如何命名，其位置都可作为托管应用的服务器物理路径。</span><span class="sxs-lookup"><span data-stu-id="73169-139">Whatever name is given to the *publish* directory of the deployed app on the server, its location serves as the server's physical path to the hosted app.</span></span>

<span data-ttu-id="73169-140">wwwroot 目录（如果存在）仅包含静态资产。</span><span class="sxs-lookup"><span data-stu-id="73169-140">The *wwwroot* directory, if present, only contains static assets.</span></span>

<span data-ttu-id="73169-141">可以使用以下两种方法之一为部署创建 stdout logs 目录：</span><span class="sxs-lookup"><span data-stu-id="73169-141">The stdout *logs* directory can be created for the deployment using one of the following two approaches:</span></span>

* <span data-ttu-id="73169-142">向项目添加以下 `<Target>` 元素：</span><span class="sxs-lookup"><span data-stu-id="73169-142">Add the following `<Target>` element to the project file:</span></span>

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

   <span data-ttu-id="73169-143">`<MakeDir>` 元素在发布的输出中创建一个空的 Logs 文件夹。</span><span class="sxs-lookup"><span data-stu-id="73169-143">The `<MakeDir>` element creates an empty *Logs* folder in the published output.</span></span> <span data-ttu-id="73169-144">该元素使用 `PublishDir` 属性来确定创建文件夹的目标位置。</span><span class="sxs-lookup"><span data-stu-id="73169-144">The element uses the `PublishDir` property to determine the target location for creating the folder.</span></span> <span data-ttu-id="73169-145">几种部署方法（如 Web 部署）均在部署期间跳过空文件夹。</span><span class="sxs-lookup"><span data-stu-id="73169-145">Several deployment methods, such as Web Deploy, skip empty folders during deployment.</span></span> <span data-ttu-id="73169-146">`<WriteLinesToFile>` 元素在 Logs 文件夹中生成一个文件，该文件可确保将文件夹部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="73169-146">The `<WriteLinesToFile>` element generates a file in the *Logs* folder, which guarantees deployment of the folder to the server.</span></span> <span data-ttu-id="73169-147">注意，如果工作进程不具有对目标文件夹的写入权限，那么文件夹创建可能仍会失败。</span><span class="sxs-lookup"><span data-stu-id="73169-147">Note that folder creation may still fail if the worker process doesn't have write access to the target folder.</span></span>

* <span data-ttu-id="73169-148">在部署中的服务器上物理创建 Logs 目录。</span><span class="sxs-lookup"><span data-stu-id="73169-148">Physically create the *Logs* directory on the server in the deployment.</span></span>

<span data-ttu-id="73169-149">部署目录需要读取/执行权限。</span><span class="sxs-lookup"><span data-stu-id="73169-149">The deployment directory requires Read/Execute permissions.</span></span> <span data-ttu-id="73169-150">Logs 目录需要读/写权限。</span><span class="sxs-lookup"><span data-stu-id="73169-150">The *Logs* directory requires Read/Write permissions.</span></span> <span data-ttu-id="73169-151">将文件写入其他目录需要读/写权限。</span><span class="sxs-lookup"><span data-stu-id="73169-151">Additional directories where files are written require Read/Write permissions.</span></span>
