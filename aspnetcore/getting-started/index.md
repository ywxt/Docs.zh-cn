---
title: ASP.NET Core 入门
author: rick-anderson
description: 介绍如何使用 ASP.NET Core 创建并运行简单的 Hello World 应用的快速教程。
ms.author: riande
ms.custom: mvc
ms.date: 05/31/2018
uid: getting-started
ms.openlocfilehash: 7ab9f303d74786c4ac76f002d0f2c66371e78cb8
ms.sourcegitcommit: b4c7b1a4c48dec0865f27874275c73da1f75e918
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2018
ms.locfileid: "39228577"
---
# <a name="get-started-with-aspnet-core"></a>ASP.NET Core 入门

::: moniker range=">= aspnetcore-2.1"

1. 安装 [!INCLUDE [](~/includes/2.1-SDK.md)]。

2. 创建 ASP.NET Core 项目。 打开命令行界面，输入以下命令：

    ```console
    dotnet new webapp -o aspnetcoreapp
    ```

    [!INCLUDE [](~/includes/webapp-alias-notice.md)]

3. 信任 HTTPS 开发证书：

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

    ```console
    dotnet dev-certs https --trust
    ```

   以上命令会显示以下对话：

   ![安全警告对话](_static/cert.png)

   如果你同意信任开发证书，请选择“是”。

# <a name="macostabmacos"></a>[macOS](#tab/macos)

    ```console
    dotnet dev-certs https --trust
    ```

   以上命令会显示以下消息：

   *请求信任 HTTPS 开发证书。如果尚未信任该证书，将运行以下命令：*`'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'`*此命令可能提醒你输入密码，已在系统密钥链上安装该证书。  密码：*

   如果你同意信任开发证书，请输入密码。

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

   <a name="see-the-documentation-for-your-linux-distribution-on-how-to-trust-the-https-development-certificate"></a>查看你的 Linux 分发对应的文档，了解如何信任 HTTPS 开发证书
---

4. 运行应用：

    ```console
    cd aspnetcoreapp
    dotnet run
    ```

5. 浏览到 [http://localhost:5001](http://localhost:5001)。  单击“接受”，接受隐私和 cookie 政策。 此应用不保留个人信息。

6. 打开 Pages/About.cshtml，使用以下突出显示标记修改该页面：

    [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9)]

7. 浏览到 [http://localhost:5001/About](http://localhost:5001/About) 并验证是否显示更改。

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

1. 安装 [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]。

2. 创建新的 ASP.NET Core 项目。

   打开命令行界面。 输入以下命令：

    ```console
    dotnet new razor -o aspnetcoreapp
    ```

3. 使用以下命令运行应用：

    ```console
    cd aspnetcoreapp
    dotnet run
    ```

4. 浏览到 [http://localhost:5000](http://localhost:5000)。

5. 打开 Pages/About.cshtml 并将页面修改为显示消息“Hello, world! The time on the server is @DateTime.Now” ：

    [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. 浏览到 [http://localhost:5000/About](http://localhost:5000/About) 并验证更改。

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. 从 [.NET Core 所有下载页面](https://www.microsoft.com/net/download/all)安装 SDK 1.0.4 的 .NET Core SDK 安装程序。

2. 为新 ASP.NET Core 项目创建文件夹。

   打开命令行界面。 输入以下命令：

   ```console
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. 如果已计算机上安装了 SDK 的更高版本，则创建一个 global.json 文件以选择 1.0.4 SDK。

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. 创建新的 ASP.NET Core 项目。

   ```console
   dotnet new web
   ```

5. 还原程序包。

    ```console
    dotnet restore
    ```

6. 运行应用。

   ```console
   dotnet run
   ```

   如有需要，[dotnet run](/dotnet/core/tools/dotnet-run) 命令会首先生成应用。

7. 浏览到 `http://localhost:5000`。

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end
