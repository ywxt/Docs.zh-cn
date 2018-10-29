---
title: 借助 Visual Studio for Mac 在 macOS 上的 ASP.NET Core 中开始使用 Razor 页面
author: rick-anderson
description: 了解如何借助 Visual Studio for Mac 在 ASP.NET Core 中开始使用 Razor 页面。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: tutorials/razor-pages-mac/razor-pages-start
ms.openlocfilehash: 8a4cc6c52684558ce9176f98205e439096e88cbf
ms.sourcegitcommit: 4d74644f11e0dac52b4510048490ae731c691496
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50089646"
---
# <a name="get-started-with-razor-pages-in-aspnet-core-on-macos-with-visual-studio-for-mac"></a>借助 Visual Studio for Mac 在 macOS 上的 ASP.NET Core 中开始使用 Razor 页面

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

本教程介绍构建 ASP.NET Core Razor Pages Web 应用的基础知识。 建议在学习本教程前先查看 [Razor 页面介绍](xref:razor-pages/index)。 Razor 页面是在 ASP.NET Core 中为 Web 应用程序生成 UI 时建议使用的方法。

## <a name="prerequisites"></a>系统必备

[!INCLUDE [](~/includes/net-core-prereqs-macos.md)]

## <a name="create-a-razor-web-app"></a>创建 Razor Web 应用

从终端运行以下命令：

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

::: moniker-end

上述命令使用 [.NET Core CLI](/dotnet/core/tools/dotnet) 创建并运行 Razor 页面项目。 打开浏览器，转到 http://localhost:5000 查看应用程序。

![主页或索引页](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE [razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a>打开项目

按 Ctrl+C 关闭应用程序。

在 Visual Studio 中，选择“文件”>“打开”，然后选择“RazorPagesMovie.csproj”文件。

### <a name="launch-the-app"></a>启动应用

在 Visual Studio 中，选择“运行”>“开始执行(不调试)”以启动应用。 Visual Studio 启动 [Kestrel](xref:fundamentals/servers/kestrel)，启动浏览器并导航到 `http://localhost:5000`。

在下一个教程中，我们将向项目添加模型。

> [!div class="step-by-step"]
> [下一篇：添加模型](xref:tutorials/razor-pages-mac/model)
