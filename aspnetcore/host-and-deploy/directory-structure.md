---
title: ASP.NET 核心目录结构
author: guardrex
description: 了解有关已发布 ASP.NET Core 应用的目录结构。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 04/09/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/directory-structure
ms.openlocfilehash: ac9b777bcc7f4a8634161fc1347a4d0fdc3b4784
ms.sourcegitcommit: 7c8fd9b7445cd77eb7f7d774bfd120c26f3b5d84
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="aspnet-core-directory-structure"></a>ASP.NET 核心目录结构

作者：[Luke Latham](https://github.com/guardrex)

在 ASP.NET 核，发布的应用程序目录中，*发布*，组成应用程序文件、 配置文件、 静态资产、 包和运行时 (有关[自包含的部署](/dotnet/core/deploying/#self-contained-deployments-scd))。


| 应用类型 | 目录结构 |
| -------- | ------------------- |
| [依赖于框架的部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd) | <ul><li>发布&dagger;<ul><li>日志&dagger;（除非需要接收 stdout 日志可选）</li><li>视图&dagger;（MVC 应用程序; 如果不预编译视图）</li><li>页&dagger;（MVC 或 Razor 页应用; 如果不预编译页）</li><li>wwwroot&dagger;</li><li>*\.dll 文件</li><li>\<程序集名称 >。 deps.json</li><li>\<程序集名称 >.dll</li><li>\<程序集名称 >.pdb</li><li>\<程序集名称 >。PrecompiledViews.dll</li><li>\<程序集名称 >。PrecompiledViews.pdb</li><li>\<程序集名称 >。 runtimeconfig.json</li><li>web.config （IIS 部署）</li></ul></li></ul> |
| [自包含的部署](/dotnet/core/deploying/#self-contained-deployments-scd) | <ul><li>发布&dagger;<ul><li>日志&dagger;（除非需要接收 stdout 日志可选）</li><li>refs&dagger;</li><li>视图&dagger;（MVC 应用程序; 如果不预编译视图）</li><li>页&dagger;（MVC 或 Razor 页应用; 如果不预编译页）</li><li>wwwroot&dagger;</li><li>\*.dll 文件</li><li>\<程序集名称 >。 deps.json</li><li>\<程序集名称 >.exe</li><li>\<程序集名称 >.pdb</li><li>\<程序集名称 >。PrecompiledViews.dll</li><li>\<程序集名称 >。PrecompiledViews.pdb</li><li>\<程序集名称 >。 runtimeconfig.json</li><li>web.config （IIS 部署）</li></ul></li></ul> |

&dagger;指示目录

*发布*目录表示*内容的根路径*，也称为*应用程序基路径*，部署。 任何名称提供给*发布*目录中的服务器上部署的应用程序，其位置用作托管的应用程序服务器的物理路径。

*Wwwroot*目录中，如果存在，仅包含静态资产。

Stdout*日志*可以使用以下两种方法之一部署创建目录：

* 添加以下`<Target>`项目文件的元素：

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

   `<MakeDir>`元素创建一个空*日志*中已发布的输出文件夹。 元素使用`PublishDir`属性来确定用于创建文件夹的目标位置。 多种部署方法，例如 Web 部署，在部署过程中跳过空文件夹。 `<WriteLinesToFile>`元素生成的文件中*日志*文件夹中，这可确保部署到服务器的文件夹。 请注意，如果工作进程不具有写访问权限的目标文件夹的文件夹创建可能仍会失败。

* 以物理方式创建*日志*目录部署中的服务器。

部署目录中需要读取/Execute 权限。 *日志*目录需要读/写权限。 其中写入文件的其他目录需要读/写权限。
