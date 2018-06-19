---
uid: webhooks/receiving/dependencies
title: ASP.NET Webhook 接收方依赖项 |Microsoft 文档
author: rick-anderson
description: 接收方依赖项，在 ASP.NET Webhook 的依赖关系注入。
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.technology: ''
ms.prod: .net-framework
ms.openlocfilehash: f9726c746c8934594e26f2871f9b867c192374bb
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26529906"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="780c3-103">ASP.NET Webhook 接收方依赖项</span><span class="sxs-lookup"><span data-stu-id="780c3-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="780c3-104">Microsoft ASP.NET Webhook 设计为具有记住的依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="780c3-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="780c3-105">可以使用备用实现使用依赖关系注入引擎替换系统中的大多数依赖项。</span><span class="sxs-lookup"><span data-stu-id="780c3-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="780c3-106">请参阅[DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs)的接收方依赖项的列表。</span><span class="sxs-lookup"><span data-stu-id="780c3-106">Please see [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="780c3-107">如果已不注册的任何依赖项，则使用默认实现。</span><span class="sxs-lookup"><span data-stu-id="780c3-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="780c3-108">请参阅[ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs)有关的默认实现的列表。</span><span class="sxs-lookup"><span data-stu-id="780c3-108">Please see [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
