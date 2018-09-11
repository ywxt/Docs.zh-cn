---
title: 使用 ASP.NET Core 和 Azure DevOps |工具和下载
author: CamSoper
description: 提供有关为托管在 Azure 中的 ASP.NET Core 应用构建 DevOps 管道的端到端指导的指南。
ms.author: casoper
ms.date: 08/07/2018
uid: azure/devops/tools-and-downloads
ms.openlocfilehash: 5529068b83db475315784571fbf4151d7ecd0d5d
ms.sourcegitcommit: 57eccdea7d89a62989272f71aad655465f1c600a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2018
ms.locfileid: "44340155"
---
# <a name="tools-and-downloads"></a>工具和下载

Azure 具有用于预配和管理资源，如多个接口[Azure 门户](https://portal.azure.com)， [Azure CLI](https://docs.microsoft.com/cli/azure/)， [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)， [Azure 云Shell](https://shell.azure.com/bash)，和 Visual Studio。 本指南将最低要求方法，并使用 Azure Cloud Shell 中，只要有可能以减少所需的步骤。 但是，对于某些部分都必须使用 Azure 门户。

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

  确认 Visual Studio 具有以下[工作负荷](https://docs.microsoft.com/visualstudio/install/modify-visual-studio)安装：

  * ASP.NET 和 Web 开发
  * Azure 开发
  * .NET Core 跨平台开发
