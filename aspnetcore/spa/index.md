---
title: "使用单页应用模板"
author: SteveSandersonMS
description: "了解如何安装并开始使用 ASP.NET Core 单页应用 (SPA) 候选发布项目模板。"
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 12/06/2017
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/index
ms.openlocfilehash: 2017c2ada835eb7206dcfd195f6e2c032909f9ef
ms.sourcegitcommit: b83a5f731a9c02bdb1cc1e3f9a8bf273eb5b33e0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="use-the-single-page-application-templates-release-candidate"></a>使用单页应用模板（候选发布）

> [!NOTE]
> 已发布的 .NET Core 2.0.x SDK 包括 Angular、React 以及带 Redux 的 React 项目模板。 **本文档并不涉及已发布的项目模板。** 本文档介绍的是下一版 Angular、React 以及带 Redux 的 React 模板（有望在 2018 年年初发布）。

## <a name="prerequisites"></a>系统必备

* [.NET Core SDK](https://www.microsoft.com/net/download) 版本 2.0.0 或更高版本
* [Node.js](https://nodejs.org) 版本 6 或更高版本

## <a name="installation"></a>安装

运行以下命令，安装 Angular、React 以及带 Redux 的 React ASP.NET Core 模板（候选发布）：

```console
dotnet new --install Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0-rc2-final
```

## <a name="use-the-templates"></a>使用模板

- [使用 Angular 项目模板](xref:spa/angular)
- [使用 React 项目模板](xref:spa/react)
- [使用带 Redux 的 React 项目模板](xref:spa/react-with-redux)
