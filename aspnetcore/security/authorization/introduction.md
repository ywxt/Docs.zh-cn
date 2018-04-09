---
title: 在 ASP.NET Core 中授权简介
author: rick-anderson
description: 了解授权以及授权 ASP.NET Core 应用中的工作方式的基础知识。
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/introduction
ms.openlocfilehash: 7ba1966dcaf1ce0510f489cfe0ff11501faffa56
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="introduction-to-authorization-in-aspnet-core"></a><span data-ttu-id="5180a-103">在 ASP.NET Core 中授权简介</span><span class="sxs-lookup"><span data-stu-id="5180a-103">Introduction to authorization in ASP.NET Core</span></span>

<a name="security-authorization-introduction"></a>

<span data-ttu-id="5180a-104">授权是指确定进程用户是能够执行。</span><span class="sxs-lookup"><span data-stu-id="5180a-104">Authorization refers to the process that determines what a user is able to do.</span></span> <span data-ttu-id="5180a-105">例如，管理用户可以创建文档库、 将文档添加、 编辑文档，以及删除它们。</span><span class="sxs-lookup"><span data-stu-id="5180a-105">For example, an administrative user is allowed to create a document library, add documents, edit documents, and delete them.</span></span> <span data-ttu-id="5180a-106">使用库的非管理用户仅有权读取文档。</span><span class="sxs-lookup"><span data-stu-id="5180a-106">A non-administrative user working with the library is only authorized to read the documents.</span></span>

<span data-ttu-id="5180a-107">授权是正交和独立于身份验证，这是有助于确定用户是谁的过程。</span><span class="sxs-lookup"><span data-stu-id="5180a-107">Authorization is orthogonal and independent from authentication, which is the process of ascertaining who a user is.</span></span> <span data-ttu-id="5180a-108">身份验证可能会创建一个或多个标识为当前用户。</span><span class="sxs-lookup"><span data-stu-id="5180a-108">Authentication may create one or more identities for the current user.</span></span>

## <a name="authorization-types"></a><span data-ttu-id="5180a-109">授权类型</span><span class="sxs-lookup"><span data-stu-id="5180a-109">Authorization types</span></span>

<span data-ttu-id="5180a-110">ASP.NET 核心授权提供一个简单、 声明性[角色](xref:security/authorization/roles)以及丰富[基于策略的](xref:security/authorization/policies)模型。</span><span class="sxs-lookup"><span data-stu-id="5180a-110">ASP.NET Core authorization provides a simple, declarative [role](xref:security/authorization/roles) and a rich [policy-based](xref:security/authorization/policies) model.</span></span> <span data-ttu-id="5180a-111">要求，以表示授权，并且处理程序评估针对需求的用户的声明。</span><span class="sxs-lookup"><span data-stu-id="5180a-111">Authorization is expressed in requirements, and handlers evaluate a user's claims against requirements.</span></span> <span data-ttu-id="5180a-112">命令性检查可以基于简单的策略或策略的评估用户标识和该用户尝试访问资源的属性。</span><span class="sxs-lookup"><span data-stu-id="5180a-112">Imperative checks can be based on simple policies or policies which evaluate both the user identity and properties of the resource that the user is attempting to access.</span></span>

## <a name="namespaces"></a><span data-ttu-id="5180a-113">命名空间</span><span class="sxs-lookup"><span data-stu-id="5180a-113">Namespaces</span></span>

<span data-ttu-id="5180a-114">授权组件，包括`AuthorizeAttribute`和`AllowAnonymousAttribute`中找不到属性，`Microsoft.AspNetCore.Authorization`命名空间。</span><span class="sxs-lookup"><span data-stu-id="5180a-114">Authorization components, including the `AuthorizeAttribute` and `AllowAnonymousAttribute` attributes, are found in the `Microsoft.AspNetCore.Authorization` namespace.</span></span>

<span data-ttu-id="5180a-115">请查阅上的文档[简单授权](xref:security/authorization/simple)。</span><span class="sxs-lookup"><span data-stu-id="5180a-115">Consult the documentation on [simple authorization](xref:security/authorization/simple).</span></span>
