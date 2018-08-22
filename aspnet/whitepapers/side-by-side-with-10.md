---
uid: whitepapers/side-by-side-with-10
title: .NET framework 1.0 和 1.1 的 ASP.NET 并行执行 |Microsoft Docs
author: rick-anderson
description: 本白皮书介绍了如何允许帧任一版本上运行的 ASP.NET Web 应用程序在计算机上安装.NET 1.0 和.NET 1.1...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: b5457a62e127ba555674fbe3b9f75552cad041c7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824215"
---
<a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a>.NET framework 1.0 和 1.1 的 ASP.NET 并行执行
====================
> 本白皮书介绍了如何允许任一版本的 framework 上运行的 ASP.NET Web 应用程序在计算机上安装.NET 1.0 和.NET 1.1。
> 
> 适用于 ASP.NET 1.0 和 ASP.NET 1.1。


在 ASP.NET 中，应用程序被称为时它们安装在同一台计算机上，但使用不同版本的.NET Framework 并行运行。 以下主题介绍如何配置 ASP.NET 应用程序通过并行执行，并提供详细的步骤：

- [维护在安装过程中的 Web 应用程序映射到.NET Framework 1.0 版](#1)
- [将映射到特定版本的.NET Framework 的 Web 应用程序](#2)
- [查找使用网站上的.NET framework 版本](#3)

传统上，当更新的计算机上的组件或应用程序后，较旧版本删除并替换为较新版本。 如果新版本不是与以前的版本兼容的通常会中断其他应用程序使用的组件或应用程序。 .NET Framework 的并行执行，从而允许多个版本的程序集或在同一时间在同一台计算机上安装应用程序，用于提供支持。 可以同时安装多个版本，因为托管应用程序可以选择要使用而不会影响使用不同版本的应用程序的版本。

默认情况下，在.NET Framework 版本 1.1，安装过程中所有现有的 ASP.NET 应用程序会自动重新配置为使用.NET Framework 的最新版本。 如果不希望使 ASP.NET 应用程序默认为.NET Framework 1.1，请单击[此处](#1)若要了解如何防止这种在安装过程。

如果你更新到.NET Framework 1.1 的 Web 服务器，并想一个或多个 Web 应用程序运行.NET Framework 1.0，您需要更新 Internet 信息服务 (IIS) 脚本映射。 脚本映射是映射到.NET Framework 的版本特定的 Web 应用程序的.aspx 文件扩展名的机制。 单击[此处](#2)若要了解如何将映射到特定版本的.NET Framework 的 Web 应用程序。

可以使用 Internet 信息管理器或 ASP.NET IIS 注册工具 (Aspnet\_regiis.exe) 若要查找特定的 Web 应用程序运行的.NET Framework 版本。 单击[此处](#3)若要了解如何查找使用网站上的.NET framework 版本。

一个导入中不考虑迁移到.NET Framework 1.1 时是每个版本的.NET Framework 使用其自己的 Machine.config 文件。 因此，如果 Web 管理员已到 Machine.config 文件发生更改，这些更改必须迁移到.NET Framework 1.1 Machine.config 文件。

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a>维护.NET Framework 1.0 到在安装过程中的 Web 应用程序的映射

默认情况下，所有现有的 ASP.NET 应用程序会自动重新配置为使用.NET Framework 的较新版本的安装过程。 使用.NET Framework 的较新版本，应用程序可以充分利用的改进和新版本中包括的新功能。 同时，Web 管理员，他可能希望精确地控制哪些应用程序均已更新，可能会阻止自动重新映射的所有现有的 ASP.NET 应用程序在安装.NET Framework 的过程。

若要防止自动重新映射到较新版本的.NET Framework 的整个 ASP.NET 应用程序，Web 管理员可以使用 Dotnetfx.exe 安装程序使用 /noaspupgrade 命令行选项。

**若要防止总重新映射到较新版本的 ASP.NET 应用程序**

1. 转到**启动**。
2. 单击**运行**。
3. 键入“cmd”。
4. 单击 **“确定”**。  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. 从命令提示符处，键入要开始的.NET framework 安装的以下行： **Dotnetfx.exe 无"安装 /noaspupgrade？**。  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. 单击**是**中 Microsoft.NET Framework 1.1 安装程序。 这将启动.NET Framework 1.1 的安装过程。  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a>将映射到特定版本的.NET Framework 的 Web 应用程序

每个版本的.NET Framework 包括 ASP.NET IIS 注册工具的版本 (Aspnet\_regiis.exe)。 此工具使管理员可以指定特定版本的.NET Framework 下运行的 Web 应用程序。 这被称为映射到.NET framework 版本的 Web 应用程序。 管理员必须选择 Aspnet\_regiis.exe 将与 Web 应用程序相关联的.NET framework 的版本相对应。 例如，想要指定网站上使用.NET Framework 1.1 的管理员必须使用 Aspnet\_regiis.exe 随附.NET Framework 1.1。

Aspnet\_regiis.exe 对于 1.0 版位于：

- C:\WINDOWS\Microsoft.NET\Framework\**v1.0.3705**\aspnet\_regiis

Aspnet\_regiis.exe 版本 1，1 位于：

- C:\WINDOWS\Microsoft.NET\Framework\**v1.1.4322**\aspnet\_regiis

Aspnet\_regiis.exe 提供两个映射的 Web 应用程序的脚本选项：

- **-s**设置的脚本映射和及其子路径中的目录。
- **-sn**只能在路径中设置的脚本映射。

该路径定义 Web 应用程序 IIS 元数据路径，W3SVC/根的窗体中定义 / {WebSiteNumber} / {应用程序\_名称}。 例如，对于名为门户位于默认网站下的 Web 应用程序，元数据库路径是 W3SVC/1/根目录/门户。

![](side-by-side-with-10/_static/image4.gif)

请注意您可以使用一个称为配置数据库编辑器工具，若要获取的元数据库路径。 可以从 Microsoft 支持网站下载此工具[ https://support.microsoft.com/default.aspx?scid=kb; en-我们; 232068。](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)

- 运行 Aspnet\_regiis.exe-s W3SVC/1/根目录/门户更新门户 IIS 脚本映射和其 subapplication。  
  
    ![](side-by-side-with-10/_static/image5.gif)

- 运行 Aspnet\_regiis.exe-sn W3SVC/1/根目录/门户更新门户的 IIS 脚本映射，而不会影响在门户中的应用程序？ s 子目录。  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a>查找 Web 应用程序使用的.NET Framework 版本

管理员可以使用 Internet 服务管理器来查找 Web 站点运行的.NET framework 版本。 不同的操作系统版本以不同方式启动 Internet 服务管理器。 若要启动服务管理器，请执行下面列出的步骤。

**启动 Internet 服务管理器**

1. 转到**启动**。
2. 单击**运行**。
3. 类型**inetmgr**。  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. 从 Internet 服务管理器中，选择你想要知道的.NET Framework 版本的 Web 应用程序。  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. Web 应用程序中，右键单击，然后单击**属性。**  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. 从属性窗口中，选择**配置。**  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. 从应用程序映射表中，选择 **.aspx**，然后单击**编辑**。  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. 从**可执行文件**文本框中，查看通过滚动版本目录。 如果版本目录 v.1.1.4322，应用程序映射到.NET Framework 1.1。 相反，如果版本目录 v1.0.3705，应用程序映射到.NET Framework 1.0。  
  
    ![](side-by-side-with-10/_static/image12.gif)
