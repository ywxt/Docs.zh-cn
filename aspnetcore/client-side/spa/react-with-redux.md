---
title: 通过 ASP.NET Core 使用带 Redux 的 React 项目模板
author: SteveSandersonMS
description: 了解如何开始使用适用于带 Redux 的 React 和 create-react-app 的 ASP.NET Core 单页应用程序 (SPA) 项目模板。
monikerRange: '>= aspnetcore-2.0'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
uid: spa/react-with-redux
ms.openlocfilehash: dab3d20865250aae548bff4614e631dd7c73b46f
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36291480"
---
# <a name="use-the-react-with-redux-project-template-with-aspnet-core"></a>通过 ASP.NET Core 使用带 Redux 的 React 项目模板

::: moniker range="= aspnetcore-2.0"

> [!NOTE]
> 本文档不涉及 ASP.NET Core 2.0 中包含的带 Redux 的 React项目模板。 本文介绍你可以手动更新的新版带 Redux 的 React 模板。 该模板默认包含在 ASP.NET Core 2.1 中。

::: moniker-end

更新的带 Redux 的 React 项目模板为使用 React、Redux 和 [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) 约定实现丰富的客户端用户界面 (UI) 的 ASP.NET Core 应用程序提供了便捷起点。

除了项目创建命令外，关于带 Redux 的 React 模板的所有信息都与 React 模板相同。 要创建此项目类型，请运行 `dotnet new reactredux` 而不是 `dotnet new react`。 有关这两个基于 React 的模板的通用功能的详细信息，请参阅 [React 模板文档](xref:spa/react)。
