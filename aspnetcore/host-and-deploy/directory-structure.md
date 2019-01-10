---
title: ASP.NET Core 目录结构
author: guardrex
description: 了解已发布的 ASP.NET Core 应用的目录结构。
monikerRange: '>= aspnetcore-2.2'
ms.author: riande
ms.custom: mvc
ms.date: 12/11/2018
uid: host-and-deploy/directory-structure
ms.openlocfilehash: ee0bebb8b5c688f8471d6420d1641b87ac271f6c
ms.sourcegitcommit: b34b25da2ab68e6495b2460ff570468f16a9bf0d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2018
ms.locfileid: "53284560"
---
# <a name="aspnet-core-directory-structure"></a><span data-ttu-id="ca699-103">ASP.NET Core 目录结构</span><span class="sxs-lookup"><span data-stu-id="ca699-103">ASP.NET Core directory structure</span></span>

<span data-ttu-id="ca699-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="ca699-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="ca699-105">发布目录包含应用的可部署资产，由 [dotnet publish](/dotnet/core/tools/dotnet-publish) 命令生成。</span><span class="sxs-lookup"><span data-stu-id="ca699-105">The *publish* directory contains the app's deployable assets produced by the [dotnet publish](/dotnet/core/tools/dotnet-publish) command.</span></span> <span data-ttu-id="ca699-106">该目录包含：</span><span class="sxs-lookup"><span data-stu-id="ca699-106">The directory contains:</span></span>

* <span data-ttu-id="ca699-107">应用程序文件</span><span class="sxs-lookup"><span data-stu-id="ca699-107">Application files</span></span>
* <span data-ttu-id="ca699-108">配置文件</span><span class="sxs-lookup"><span data-stu-id="ca699-108">Configuration files</span></span>
* <span data-ttu-id="ca699-109">静态资产</span><span class="sxs-lookup"><span data-stu-id="ca699-109">Static assets</span></span>
* <span data-ttu-id="ca699-110">包</span><span class="sxs-lookup"><span data-stu-id="ca699-110">Packages</span></span>
* <span data-ttu-id="ca699-111">运行时（仅限[独立部署](/dotnet/core/deploying/#self-contained-deployments-scd)）</span><span class="sxs-lookup"><span data-stu-id="ca699-111">A runtime ([self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd) only)</span></span>

| <span data-ttu-id="ca699-112">应用类型</span><span class="sxs-lookup"><span data-stu-id="ca699-112">App Type</span></span> | <span data-ttu-id="ca699-113">目录结构</span><span class="sxs-lookup"><span data-stu-id="ca699-113">Directory Structure</span></span> |
| -------- | ------------------- |
| [<span data-ttu-id="ca699-114">依赖框架的部署</span><span class="sxs-lookup"><span data-stu-id="ca699-114">Framework-dependent Deployment</span></span>](/dotnet/core/deploying/#framework-dependent-deployments-fdd) | <ul><li><span data-ttu-id="ca699-115">publish&dagger;</span><span class="sxs-lookup"><span data-stu-id="ca699-115">publish&dagger;</span></span><ul><li><span data-ttu-id="ca699-116">Logs&dagger;（除非需要接收 stdout 日志，否则为可选）</span><span class="sxs-lookup"><span data-stu-id="ca699-116">Logs&dagger; (optional unless required to receive stdout logs)</span></span></li><li><span data-ttu-id="ca699-117">Views&dagger;（MVC 应用；如果未预编译视图）</span><span class="sxs-lookup"><span data-stu-id="ca699-117">Views&dagger; (MVC apps; if views aren't precompiled)</span></span></li><li><span data-ttu-id="ca699-118">Pages&dagger;（MVC 或 Razor 页应用；如果未预编译页）</span><span class="sxs-lookup"><span data-stu-id="ca699-118">Pages&dagger; (MVC or Razor Pages apps; if pages aren't precompiled)</span></span></li><li><span data-ttu-id="ca699-119">wwwroot&dagger;</span><span class="sxs-lookup"><span data-stu-id="ca699-119">wwwroot&dagger;</span></span></li><li><span data-ttu-id="ca699-120">\*\.dll 文件</span><span class="sxs-lookup"><span data-stu-id="ca699-120">\*\.dll files</span></span></li><li><span data-ttu-id="ca699-121">{ASSEMBLY NAME}.deps.json</span><span class="sxs-lookup"><span data-stu-id="ca699-121">{ASSEMBLY NAME}.deps.json</span></span></li><li><span data-ttu-id="ca699-122">{ASSEMBLY NAME}.dll</span><span class="sxs-lookup"><span data-stu-id="ca699-122">{ASSEMBLY NAME}.dll</span></span></li><li><span data-ttu-id="ca699-123">{ASSEMBLY NAME}.pdb</span><span class="sxs-lookup"><span data-stu-id="ca699-123">{ASSEMBLY NAME}.pdb</span></span></li><li><span data-ttu-id="ca699-124">{ASSEMBLY NAME}.Views.dll</span><span class="sxs-lookup"><span data-stu-id="ca699-124">{ASSEMBLY NAME}.Views.dll</span></span></li><li><span data-ttu-id="ca699-125">{ASSEMBLY NAME}.Views.pdb</span><span class="sxs-lookup"><span data-stu-id="ca699-125">{ASSEMBLY NAME}.Views.pdb</span></span></li><li><span data-ttu-id="ca699-126">{ASSEMBLY NAME}.runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="ca699-126">{ASSEMBLY NAME}.runtimeconfig.json</span></span></li><li><span data-ttu-id="ca699-127">web.config（IIS 部署）</span><span class="sxs-lookup"><span data-stu-id="ca699-127">web.config (IIS deployments)</span></span></li></ul></li></ul> |
| [<span data-ttu-id="ca699-128">独立部署</span><span class="sxs-lookup"><span data-stu-id="ca699-128">Self-contained Deployment</span></span>](/dotnet/core/deploying/#self-contained-deployments-scd) | <ul><li><span data-ttu-id="ca699-129">publish&dagger;</span><span class="sxs-lookup"><span data-stu-id="ca699-129">publish&dagger;</span></span><ul><li><span data-ttu-id="ca699-130">Logs&dagger;（除非需要接收 stdout 日志，否则为可选）</span><span class="sxs-lookup"><span data-stu-id="ca699-130">Logs&dagger; (optional unless required to receive stdout logs)</span></span></li><li><span data-ttu-id="ca699-131">Views&dagger;（MVC 应用；如果未预编译视图）</span><span class="sxs-lookup"><span data-stu-id="ca699-131">Views&dagger; (MVC apps; if views aren't precompiled)</span></span></li><li><span data-ttu-id="ca699-132">Pages&dagger;（MVC 或 Razor 页应用；如果未预编译页）</span><span class="sxs-lookup"><span data-stu-id="ca699-132">Pages&dagger; (MVC or Razor Pages apps; if pages aren't precompiled)</span></span></li><li><span data-ttu-id="ca699-133">wwwroot&dagger;</span><span class="sxs-lookup"><span data-stu-id="ca699-133">wwwroot&dagger;</span></span></li><li><span data-ttu-id="ca699-134">\*.dll 文件</span><span class="sxs-lookup"><span data-stu-id="ca699-134">\*.dll files</span></span></li><li><span data-ttu-id="ca699-135">{ASSEMBLY NAME}.deps.json</span><span class="sxs-lookup"><span data-stu-id="ca699-135">{ASSEMBLY NAME}.deps.json</span></span></li><li><span data-ttu-id="ca699-136">{ASSEMBLY NAME}.dll</span><span class="sxs-lookup"><span data-stu-id="ca699-136">{ASSEMBLY NAME}.dll</span></span></li><li><span data-ttu-id="ca699-137">{ASSEMBLY NAME}.exe</span><span class="sxs-lookup"><span data-stu-id="ca699-137">{ASSEMBLY NAME}.exe</span></span></li><li><span data-ttu-id="ca699-138">{ASSEMBLY NAME}.pdb</span><span class="sxs-lookup"><span data-stu-id="ca699-138">{ASSEMBLY NAME}.pdb</span></span></li><li><span data-ttu-id="ca699-139">{ASSEMBLY NAME}.Views.dll</span><span class="sxs-lookup"><span data-stu-id="ca699-139">{ASSEMBLY NAME}.Views.dll</span></span></li><li><span data-ttu-id="ca699-140">{ASSEMBLY NAME}.Views.pdb</span><span class="sxs-lookup"><span data-stu-id="ca699-140">{ASSEMBLY NAME}.Views.pdb</span></span></li><li><span data-ttu-id="ca699-141">{ASSEMBLY NAME}.runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="ca699-141">{ASSEMBLY NAME}.runtimeconfig.json</span></span></li><li><span data-ttu-id="ca699-142">web.config（IIS 部署）</span><span class="sxs-lookup"><span data-stu-id="ca699-142">web.config (IIS deployments)</span></span></li></ul></li></ul> |

<span data-ttu-id="ca699-143">&dagger;指示目录</span><span class="sxs-lookup"><span data-stu-id="ca699-143">&dagger;Indicates a directory</span></span>

<span data-ttu-id="ca699-144">publish 目录代表部署的内容根路径，也称为应用程序基路径。</span><span class="sxs-lookup"><span data-stu-id="ca699-144">The *publish* directory represents the *content root path*, also called the *application base path*, of the deployment.</span></span> <span data-ttu-id="ca699-145">无论对服务器上已部署应用的 publish 目录如何命名，其位置都可作为托管应用的服务器物理路径。</span><span class="sxs-lookup"><span data-stu-id="ca699-145">Whatever name is given to the *publish* directory of the deployed app on the server, its location serves as the server's physical path to the hosted app.</span></span>

<span data-ttu-id="ca699-146">wwwroot 目录（如果存在）仅包含静态资产。</span><span class="sxs-lookup"><span data-stu-id="ca699-146">The *wwwroot* directory, if present, only contains static assets.</span></span>

<span data-ttu-id="ca699-147">可以使用以下两种方法之一为部署创建 stdout Logs 目录：</span><span class="sxs-lookup"><span data-stu-id="ca699-147">The stdout *Logs* directory can be created for the deployment using one of the following two approaches:</span></span>

* <span data-ttu-id="ca699-148">向项目添加以下 `<Target>` 元素：</span><span class="sxs-lookup"><span data-stu-id="ca699-148">Add the following `<Target>` element to the project file:</span></span>

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

   <span data-ttu-id="ca699-149">`<MakeDir>` 元素在发布的输出中创建一个空的 Logs 文件夹。</span><span class="sxs-lookup"><span data-stu-id="ca699-149">The `<MakeDir>` element creates an empty *Logs* folder in the published output.</span></span> <span data-ttu-id="ca699-150">该元素使用 `PublishDir` 属性来确定创建文件夹的目标位置。</span><span class="sxs-lookup"><span data-stu-id="ca699-150">The element uses the `PublishDir` property to determine the target location for creating the folder.</span></span> <span data-ttu-id="ca699-151">几种部署方法（如 Web 部署）均在部署期间跳过空文件夹。</span><span class="sxs-lookup"><span data-stu-id="ca699-151">Several deployment methods, such as Web Deploy, skip empty folders during deployment.</span></span> <span data-ttu-id="ca699-152">`<WriteLinesToFile>` 元素在 Logs 文件夹中生成一个文件，该文件可确保将文件夹部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="ca699-152">The `<WriteLinesToFile>` element generates a file in the *Logs* folder, which guarantees deployment of the folder to the server.</span></span> <span data-ttu-id="ca699-153">如果工作进程不具有对目标文件夹的写入权限，则使用此方法的文件夹创建操作将失败。</span><span class="sxs-lookup"><span data-stu-id="ca699-153">Folder creation using this approach fails if the worker process doesn't have write access to the target folder.</span></span>

* <span data-ttu-id="ca699-154">在部署中的服务器上物理创建 Logs 目录。</span><span class="sxs-lookup"><span data-stu-id="ca699-154">Physically create the *Logs* directory on the server in the deployment.</span></span>

<span data-ttu-id="ca699-155">部署目录需要读取/执行权限。</span><span class="sxs-lookup"><span data-stu-id="ca699-155">The deployment directory requires Read/Execute permissions.</span></span> <span data-ttu-id="ca699-156">Logs 目录需要读/写权限。</span><span class="sxs-lookup"><span data-stu-id="ca699-156">The *Logs* directory requires Read/Write permissions.</span></span> <span data-ttu-id="ca699-157">将文件写入其他目录需要读/写权限。</span><span class="sxs-lookup"><span data-stu-id="ca699-157">Additional directories where files are written require Read/Write permissions.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ca699-158">其他资源</span><span class="sxs-lookup"><span data-stu-id="ca699-158">Additional resources</span></span>

* [<span data-ttu-id="ca699-159">dotnet publish</span><span class="sxs-lookup"><span data-stu-id="ca699-159">dotnet publish</span></span>](/dotnet/core/tools/dotnet-publish)
* [<span data-ttu-id="ca699-160">.NET Core 应用程序部署</span><span class="sxs-lookup"><span data-stu-id="ca699-160">.NET Core application deployment</span></span>](/dotnet/core/deploying/)
* [<span data-ttu-id="ca699-161">目标框架</span><span class="sxs-lookup"><span data-stu-id="ca699-161">Target frameworks</span></span>](/dotnet/standard/frameworks)
* [<span data-ttu-id="ca699-162">.NET Core RID 目录</span><span class="sxs-lookup"><span data-stu-id="ca699-162">.NET Core RID Catalog</span></span>](/dotnet/core/rid-catalog)
