---
title: 使用 ASP.NET Core 响应与回顾的项目模板
author: SteveSandersonMS
description: 了解如何开始使用 ASP.NET 核心单页面应用程序 (SPA) 项目模板用于使用 Redux 和创建响应应用程序的响应。
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/react-with-redux
ms.openlocfilehash: 9abfbfe5be69d3145de453d9d9e56ea35eec64ed
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="use-the-react-with-redux-project-template-with-aspnet-core"></a><span data-ttu-id="023e8-103">使用 ASP.NET Core 响应与回顾的项目模板</span><span class="sxs-lookup"><span data-stu-id="023e8-103">Use the React-with-Redux project template with ASP.NET Core</span></span>

> [!NOTE]
> <span data-ttu-id="023e8-104">本文档不有关响应与回顾的项目模板包括在 ASP.NET 核心 2.0。</span><span class="sxs-lookup"><span data-stu-id="023e8-104">This documentation isn't about the React-with-Redux project template included in ASP.NET Core 2.0.</span></span> <span data-ttu-id="023e8-105">它是有关与其则可手动更新较新的响应与回顾模板。</span><span class="sxs-lookup"><span data-stu-id="023e8-105">It's about the newer React-with-Redux template to which you can update manually.</span></span> <span data-ttu-id="023e8-106">默认情况下，该模板包含在 ASP.NET 核心 2.1。</span><span class="sxs-lookup"><span data-stu-id="023e8-106">The template is included in ASP.NET Core 2.1 by default.</span></span>

<span data-ttu-id="023e8-107">已更新的响应与 Redux 项目模板提供了方便的起始点，为使用 ASP.NET Core 应用做出响应，Redux，和[创建响应应用](https://github.com/facebookincubator/create-react-app)(CRA) 约定，可以实现的丰富的客户端用户界面 (UI)。</span><span class="sxs-lookup"><span data-stu-id="023e8-107">The updated React-with-Redux project template provides a convenient starting point for ASP.NET Core apps using React, Redux, and [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) conventions to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="023e8-108">除了项目创建命令的响应与回顾模板有关的所有信息都是响应模板相同。</span><span class="sxs-lookup"><span data-stu-id="023e8-108">With the exception of the project creation command, all information about the React-with-Redux template is the same as the React template.</span></span> <span data-ttu-id="023e8-109">若要创建此项目类型，请运行`dotnet new reactredux`而不是`dotnet new react`。</span><span class="sxs-lookup"><span data-stu-id="023e8-109">To create this project type, run `dotnet new reactredux` instead of `dotnet new react`.</span></span> <span data-ttu-id="023e8-110">有关响应基于这两个模板共同的功能的详细信息，请参阅[做出响应模板文档](xref:spa/react)。</span><span class="sxs-lookup"><span data-stu-id="023e8-110">For more information about the functionality common to both React-based templates, see [React template documentation](xref:spa/react).</span></span>
