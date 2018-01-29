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
ms.openlocfilehash: bfb00386af0e775b4c03a71567703ed87a785ce2
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
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
dotnet new --install Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0-rc1-final
```

## <a name="use-the-templates"></a>使用模板

- [使用 Angular 项目模板](xref:spa/angular)
- [使用 React 项目模板](xref:spa/react)
- [使用带 Redux 的 React 项目模板](xref:spa/react-with-redux)
