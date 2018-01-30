---
title: "授权简介"
author: rick-anderson
description: "本文档提供授权的基本说明，并说明授权如何与 ASP.NET Core 相关。"
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/introduction
ms.openlocfilehash: a6bd81a4e5796c1d0a0033c2b8d5a6ba9282564c
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="introduction"></a><span data-ttu-id="19cd6-103">介绍</span><span class="sxs-lookup"><span data-stu-id="19cd6-103">Introduction</span></span>

<a name="security-authorization-introduction"></a>

<span data-ttu-id="19cd6-104">授权是指确定进程用户是能够执行。</span><span class="sxs-lookup"><span data-stu-id="19cd6-104">Authorization refers to the process that determines what a user is able to do.</span></span> <span data-ttu-id="19cd6-105">例如，管理用户可以创建文档库、 将文档添加、 编辑文档，以及删除它们。</span><span class="sxs-lookup"><span data-stu-id="19cd6-105">For example, an administrative user is allowed to create a document library, add documents, edit documents, and delete them.</span></span> <span data-ttu-id="19cd6-106">使用库的非管理用户仅有权读取文档。</span><span class="sxs-lookup"><span data-stu-id="19cd6-106">A non-administrative user working with the library is only authorized to read the documents.</span></span>

<span data-ttu-id="19cd6-107">授权是正交和独立于身份验证，这是有助于确定用户是谁的过程。</span><span class="sxs-lookup"><span data-stu-id="19cd6-107">Authorization is orthogonal and independent from authentication, which is the process of ascertaining who a user is.</span></span> <span data-ttu-id="19cd6-108">身份验证可能会创建一个或多个标识为当前用户。</span><span class="sxs-lookup"><span data-stu-id="19cd6-108">Authentication may create one or more identities for the current user.</span></span>

## <a name="authorization-types"></a><span data-ttu-id="19cd6-109">授权类型</span><span class="sxs-lookup"><span data-stu-id="19cd6-109">Authorization Types</span></span>

<span data-ttu-id="19cd6-110">ASP.NET 核心授权提供一个简单的声明性[角色](roles.md)和[基于的丰富策略](policies.md)模型。</span><span class="sxs-lookup"><span data-stu-id="19cd6-110">ASP.NET Core authorization provides a simple declarative [role](roles.md) and a [rich policy based](policies.md) model.</span></span> <span data-ttu-id="19cd6-111">要求，以表示授权，并且处理程序评估针对需求的用户的声明。</span><span class="sxs-lookup"><span data-stu-id="19cd6-111">Authorization is expressed in requirements, and handlers evaluate a user's claims against requirements.</span></span> <span data-ttu-id="19cd6-112">命令性检查可以基于简单的策略或策略的评估用户标识和该用户尝试访问资源的属性。</span><span class="sxs-lookup"><span data-stu-id="19cd6-112">Imperative checks can be based on simple policies or policies which evaluate both the user identity and properties of the resource that the user is attempting to access.</span></span>

## <a name="namespaces"></a><span data-ttu-id="19cd6-113">命名空间</span><span class="sxs-lookup"><span data-stu-id="19cd6-113">Namespaces</span></span>

<span data-ttu-id="19cd6-114">授权组件，包括`AuthorizeAttribute`和`AllowAnonymousAttribute`中找不到属性`Microsoft.AspNetCore.Authorization`命名空间。</span><span class="sxs-lookup"><span data-stu-id="19cd6-114">Authorization components, including the `AuthorizeAttribute` and `AllowAnonymousAttribute` attributes are found in the `Microsoft.AspNetCore.Authorization` namespace.</span></span>
