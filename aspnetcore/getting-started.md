---
title: ASP.NET Core 入门
author: rick-anderson
description: 介绍如何使用 ASP.NET Core 创建并运行简单的 Hello World 应用的快速教程。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/10/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: getting-started
ms.openlocfilehash: e814277663ff5a964171a71ebb6e0f094e0ddc60
ms.sourcegitcommit: 3d071fabaf90e32906df97b08a8d00e602db25c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="get-started-with-aspnet-core"></a>ASP.NET Core 入门

::: moniker range=">= aspnetcore-2.0"

1. 安装 [!INCLUDE[](~/includes/net-core-sdk-download-link.md)]。

2. 创建新的 .NET Core 项目。

   在 macOS 和 Linux 上，打开终端窗口。 在 Windows 上，打开命令提示符。 输入以下命令：

    ```terminal
    dotnet new razor -o aspnetcoreapp
    ```

3. 使用以下命令运行应用：

    ```terminal
    cd aspnetcoreapp
    dotnet run
    ```

4. 浏览到 [http://localhost:5000](http://localhost:5000)。

5. 打开 Pages/About.cshtml 并将页面修改为显示消息“Hello, world! The time on the server is @DateTime.Now” ：

    [!code-cshtml[](getting-started/sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. 浏览到 [http://localhost:5000/About](http://localhost:5000/About) 并验证更改。

[!INCLUDE[next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. 从 [.NET Core 所有下载页面](https://www.microsoft.com/net/download/all)安装 SDK 1.0.4 的 .NET Core SDK 安装程序。

2. 为新 .NET Core 项目创建文件夹。

   在 macOS 和 Linux 上，打开终端窗口。 在 Windows 上，打开命令提示符。

   ```terminal
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. 如果已计算机上安装了 SDK 的更高版本，则创建一个 global.json 文件以选择 1.0.4 SDK。

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. 创建新的 .NET Core 项目。

   ```terminal
   dotnet new web
   ```

5. 还原程序包。

    ```terminal
    dotnet restore
    ```

6. 运行应用。

   ```terminal
   dotnet run
   ```

   如有需要，[dotnet run](/dotnet/core/tools/dotnet-run) 命令会首先生成应用。

7. 浏览到 `http://localhost:5000`。

[!INCLUDE[next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end