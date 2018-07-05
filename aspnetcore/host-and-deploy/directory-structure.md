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
# <a name="aspnet-core-directory-structure"></a>ASP.NET Core 目录结构

作者：[Luke Latham](https://github.com/guardrex)

在 ASP.NET Core 中，发布的应用程序目录 publish 由应用程序文件、配置文件、静态资产、程序包和运行时（适用于[独立部署](/dotnet/core/deploying/#self-contained-deployments-scd)）组成。


| 应用类型 | 目录结构 |
| -------- | ------------------- |
| [依赖框架的部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd) | <ul><li>publish&dagger;<ul><li>Logs&dagger;（除非需要接收 stdout 日志，否则为可选）</li><li>Views&dagger;（MVC 应用；如果未预编译视图）</li><li>Pages&dagger;（MVC 或 Razor 页应用；如果未预编译页）</li><li>wwwroot&dagger;</li><li>*\.dll 文件</li><li>\<assembly-name>.deps.json</li><li>\<assembly-name>.dll</li><li>\<assembly-name>.pdb</li><li>\<assembly-name>.PrecompiledViews.dll</li><li>\<assembly-name>.PrecompiledViews.pdb</li><li>\<assembly-name>.runtimeconfig.json</li><li>web.config（IIS 部署）</li></ul></li></ul> |
| [独立部署](/dotnet/core/deploying/#self-contained-deployments-scd) | <ul><li>publish&dagger;<ul><li>Logs&dagger;（除非需要接收 stdout 日志，否则为可选）</li><li>refs&dagger;</li><li>Views&dagger;（MVC 应用；如果未预编译视图）</li><li>Pages&dagger;（MVC 或 Razor 页应用；如果未预编译页）</li><li>wwwroot&dagger;</li><li>\*.dll 文件</li><li>\<assembly-name>.deps.json</li><li>\<assembly-name>.exe</li><li>\<assembly-name>.pdb</li><li>\<assembly-name>.PrecompiledViews.dll</li><li>\<assembly-name>.PrecompiledViews.pdb</li><li>\<assembly-name>.runtimeconfig.json</li><li>web.config（IIS 部署）</li></ul></li></ul> |

&dagger;指示目录

publish 目录代表部署的内容根路径，也称为应用程序基路径。 无论对服务器上已部署应用的 publish 目录如何命名，其位置都可作为托管应用的服务器物理路径。

wwwroot 目录（如果存在）仅包含静态资产。

可以使用以下两种方法之一为部署创建 stdout Logs 目录：

* 向项目添加以下 `<Target>` 元素：

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

   `<MakeDir>` 元素在发布的输出中创建一个空的 Logs 文件夹。 该元素使用 `PublishDir` 属性来确定创建文件夹的目标位置。 几种部署方法（如 Web 部署）均在部署期间跳过空文件夹。 `<WriteLinesToFile>` 元素在 Logs 文件夹中生成一个文件，该文件可确保将文件夹部署到服务器。 注意，如果工作进程不具有对目标文件夹的写入权限，那么文件夹创建可能仍会失败。

* 在部署中的服务器上物理创建 Logs 目录。

部署目录需要读取/执行权限。 Logs 目录需要读/写权限。 将文件写入其他目录需要读/写权限。
