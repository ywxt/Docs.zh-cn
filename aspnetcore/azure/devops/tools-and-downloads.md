---
title: 工具和下载-使用 ASP.NET Core 和 Azure 进行开发运营
author: CamSoper
description: 工具和下载所需的 ASP.NET Core 和 Azure 中的 DevOps。
ms.author: casoper
ms.custom: mvc, seodec18
ms.date: 10/24/2018
uid: azure/devops/tools-and-downloads
ms.openlocfilehash: a12bced8826a3399d5cf347be72baf77cc39d8b6
ms.sourcegitcommit: 49faca2644590fc081d86db46ea5e29edfc28b7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2018
ms.locfileid: "53121409"
---
# <a name="tools-and-downloads"></a>工具和下载

Azure 具有用于预配和管理资源，如多个接口[Azure 门户](https://portal.azure.com)， [Azure CLI](/cli/azure/)， [Azure PowerShell](/powershell/azure/overview)， [Azure 云Shell](https://shell.azure.com/bash)，和 Visual Studio。 本指南将最低要求方法，并使用 Azure Cloud Shell 中，只要有可能以减少所需的步骤。 但是，对于某些部分都必须使用 Azure 门户。

## <a name="prerequisites"></a>系统必备

以下订阅是必需的：

* Azure&mdash;如果还没有帐户，[获取免费试用版](https://azure.microsoft.com/free/)。
* Azure DevOps 服务&mdash;第 4 章中创建你的 Azure DevOps 订阅和组织。
* GitHub&mdash;如果还没有帐户，[免费注册](https://github.com/join)。

以下工具是必需的：

* [Git](https://git-scm.com/downloads) &mdash;本指南中建议的 Git 基本的了解。 审阅[Git 文档](https://git-scm.com/doc)，具体而言[的 git remote](https://git-scm.com/docs/git-remote)并[git 推送](https://git-scm.com/docs/git-push)。
* [.NET core SDK](https://www.microsoft.com/net/download/) &mdash; 2.1.300 版本或更高版本需要生成并运行示例应用程序。 如果使用安装了 Visual Studio **.NET Core 跨平台开发**已安装工作负荷中，.NET Core SDK。

    验证您的.NET Core SDK 安装。 打开命令外壳中，并运行以下命令：

    ```console
    dotnet --version
    ```

## <a name="recommended-tools-windows-only"></a>建议的工具 (仅 Windows)

* [Visual Studio](https://www.visualstudio.com/)的可靠的 Azure 工具提供了 GUI 的大部分在本指南中所述的功能。 任何版本的 Visual Studio 将起作用，包括免费的 Visual Studio Community Edition。 教程旨在演示开发、 部署和 DevOps 与和不使用 Visual Studio。

  确认 Visual Studio 具有以下[工作负荷](/visualstudio/install/modify-visual-studio)安装：

  * ASP.NET 和 Web 开发
  * Azure 开发
  * .NET Core 跨平台开发
