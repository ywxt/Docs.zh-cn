---
title: 通过 ASP.NET Core 使用单页应用程序模板
author: SteveSandersonMS
description: 了解如何安装并开始使用 ASP.NET Core 单页应用程序 (SPA) 项目模板。
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/index
ms.openlocfilehash: eda4817de007f3c3184b2ba6ed6c97989ff17da5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="use-the-single-page-application-templates-with-aspnet-core"></a><span data-ttu-id="8d179-103">通过 ASP.NET Core 使用单页应用程序模板</span><span class="sxs-lookup"><span data-stu-id="8d179-103">Use the Single Page Application templates with ASP.NET Core</span></span>

> [!NOTE]
> <span data-ttu-id="8d179-104">已发布的 .NET Core 2.0.x SDK 包括 Angular、React 以及带 Redux 的 React 早期项目模板。</span><span class="sxs-lookup"><span data-stu-id="8d179-104">The released .NET Core 2.0.x SDK includes older project templates for Angular, React, and React with Redux.</span></span> <span data-ttu-id="8d179-105">本文档并不涉及这些早期项目模板。</span><span class="sxs-lookup"><span data-stu-id="8d179-105">This documentation isn't about those older project templates.</span></span> <span data-ttu-id="8d179-106">本文档适用于最新的 Angular、React 以及带 Redux 的 React 模板，这些模板可手动安装到 ASP.NET Core 2.0 中。</span><span class="sxs-lookup"><span data-stu-id="8d179-106">This documentation is for the latest Angular, React, and React with Redux templates, which can be installed manually into ASP.NET Core 2.0.</span></span> <span data-ttu-id="8d179-107">ASP.NET Core 2.1 中默认包含这些模板。</span><span class="sxs-lookup"><span data-stu-id="8d179-107">The templates are included by default with ASP.NET Core 2.1.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d179-108">系统必备</span><span class="sxs-lookup"><span data-stu-id="8d179-108">Prerequisites</span></span>

* [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]
* <span data-ttu-id="8d179-109">[Node.js](https://nodejs.org) 版本 6 或更高版本</span><span class="sxs-lookup"><span data-stu-id="8d179-109">[Node.js](https://nodejs.org), version 6 or later</span></span>

## <a name="installation"></a><span data-ttu-id="8d179-110">安装</span><span class="sxs-lookup"><span data-stu-id="8d179-110">Installation</span></span>

<span data-ttu-id="8d179-111">如果拥有 ASP.NET Core 2.0，请运行以下命令，安装 Angular、React 以及带 Redux 的 React 更新 ASP.NET Core 模板：</span><span class="sxs-lookup"><span data-stu-id="8d179-111">If you have ASP.NET Core 2.0, run the following command to install the updated ASP.NET Core templates for Angular, React, and React with Redux:</span></span>

```console
dotnet new --install Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0
```

## <a name="use-the-templates"></a><span data-ttu-id="8d179-112">使用模板</span><span class="sxs-lookup"><span data-stu-id="8d179-112">Use the templates</span></span>

- [<span data-ttu-id="8d179-113">使用 Angular 项目模板</span><span class="sxs-lookup"><span data-stu-id="8d179-113">Use the Angular project template</span></span>](xref:spa/angular)
- [<span data-ttu-id="8d179-114">使用 React 项目模板</span><span class="sxs-lookup"><span data-stu-id="8d179-114">Use the React project template</span></span>](xref:spa/react)
- [<span data-ttu-id="8d179-115">使用带 Redux 的 React 项目模板</span><span class="sxs-lookup"><span data-stu-id="8d179-115">Use the React with Redux project template</span></span>](xref:spa/react-with-redux)
