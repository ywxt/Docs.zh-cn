---
title: ASP.NET Core 入门
author: rick-anderson
description: 介绍如何使用 ASP.NET Core 创建并运行简单的 Hello World 应用的快速教程。
ms.author: riande
ms.custom: mvc
ms.date: 12/01/2018
uid: getting-started
ms.openlocfilehash: 29a328b610b0a6e1616cd6ebc70a8fa3e515eb92
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861701"
---
# <a name="tutorial-get-started-with-aspnet-core"></a>教程：ASP.NET Core 入门

本教程演示如何使用 .NET Core 命令行接口创建 ASP.NET Core Web 应用。

你将了解如何：

> [!div class="checklist"]
> * 创建 Web 应用项目。
> * 启用本地 HTTPS。
> * 运行应用。
> * 编辑 Razor 页面。

最后，在本地计算机上运行工作 Web 应用。

![Web 应用主页](_static/home-page.png)

## <a name="prerequisites"></a>系统必备

安装 [!INCLUDE [](~/includes/2.1-SDK.md)]。

## <a name="create-a-web-app-project"></a>创建 Web 应用项目

打开命令行界面，然后输入以下命令：

```console
dotnet new webapp -o aspnetcoreapp
```

## <a name="enable-local-https"></a>启用本地 HTTPS

信任 HTTPS 开发证书：

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

*请求信任 HTTPS 开发证书。如果证书尚不受信任，我们将运行以下命令：* `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'`。  
*此命令可能会提示你输入密码以在系统密钥链上安装证书。

密码：*

如果你同意信任开发证书，请输入密码。

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

查看你的 Linux 分发对应的文档，了解如何信任 HTTPS 开发证书。

---

## <a name="run-the-app"></a>运行应用

运行以下命令：

```console
cd aspnetcoreapp
dotnet run
```

浏览到 [https://localhost:5001](https://localhost:5001)。 单击“接受”，接受隐私和 cookie 政策。 此应用不保留个人信息。

## <a name="edit-a-razor-page"></a>编辑 Razor 页面

打开 Pages/About.cshtml，使用以下突出显示标记修改该页面：

[!code-cshtml[](sample/getting-started/about.cshtml?highlight=9)]

浏览到 [https://localhost:5001/About](https://localhost:5001/About) 并验证是否显示更改。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 创建 Web 应用项目。
> * 启用本地 HTTPS。
> * 运行该项目。
> * 进行更改。

若要了解有关 ASP.NET Core 的详细信息，请参阅简介：

> [!div class="nextstepaction"]
> <xref:index>

> [!NOTE]
> 我们要测试所建议的新 ASP.NET Core 目录结构是否可用。 如果有几分钟时间尝试了解当前或所建议目录中的七个不同主题，请[单击此处参与调查](https://dpk4xbh5.optimalworkshop.com/treejack/aa11wn82)。
