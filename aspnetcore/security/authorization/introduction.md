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
ms.openlocfilehash: f969cb26d1fcddeac967b1e3d13e3c06ebc7631f
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
ms.locfileid: "31483077"
---
# <a name="introduction-to-authorization-in-aspnet-core"></a><span data-ttu-id="5955f-103">在 ASP.NET Core 中授权简介</span><span class="sxs-lookup"><span data-stu-id="5955f-103">Introduction to authorization in ASP.NET Core</span></span>

<a name="security-authorization-introduction"></a>

<span data-ttu-id="5955f-104">授权是指确定进程用户是能够执行。</span><span class="sxs-lookup"><span data-stu-id="5955f-104">Authorization refers to the process that determines what a user is able to do.</span></span> <span data-ttu-id="5955f-105">例如，管理用户可以创建文档库、 将文档添加、 编辑文档，以及删除它们。</span><span class="sxs-lookup"><span data-stu-id="5955f-105">For example, an administrative user is allowed to create a document library, add documents, edit documents, and delete them.</span></span> <span data-ttu-id="5955f-106">使用库的非管理用户仅有权读取文档。</span><span class="sxs-lookup"><span data-stu-id="5955f-106">A non-administrative user working with the library is only authorized to read the documents.</span></span>

<span data-ttu-id="5955f-107">授权是正交和独立于身份验证。</span><span class="sxs-lookup"><span data-stu-id="5955f-107">Authorization is orthogonal and independent from authentication.</span></span> <span data-ttu-id="5955f-108">但是，授权要求的身份验证机制。</span><span class="sxs-lookup"><span data-stu-id="5955f-108">However, authorization requires an authentication mechanism.</span></span> <span data-ttu-id="5955f-109">身份验证是有助于确定用户是谁的过程。</span><span class="sxs-lookup"><span data-stu-id="5955f-109">Authentication is the process of ascertaining who a user is.</span></span> <span data-ttu-id="5955f-110">身份验证可能会创建一个或多个标识为当前用户。</span><span class="sxs-lookup"><span data-stu-id="5955f-110">Authentication may create one or more identities for the current user.</span></span>

## <a name="authorization-types"></a><span data-ttu-id="5955f-111">授权类型</span><span class="sxs-lookup"><span data-stu-id="5955f-111">Authorization types</span></span>

<span data-ttu-id="5955f-112">ASP.NET 核心授权提供一个简单、 声明性[角色](xref:security/authorization/roles)以及丰富[基于策略的](xref:security/authorization/policies)模型。</span><span class="sxs-lookup"><span data-stu-id="5955f-112">ASP.NET Core authorization provides a simple, declarative [role](xref:security/authorization/roles) and a rich [policy-based](xref:security/authorization/policies) model.</span></span> <span data-ttu-id="5955f-113">要求，以表示授权，并且处理程序评估针对需求的用户的声明。</span><span class="sxs-lookup"><span data-stu-id="5955f-113">Authorization is expressed in requirements, and handlers evaluate a user's claims against requirements.</span></span> <span data-ttu-id="5955f-114">命令性检查可以基于简单的策略或策略的评估用户标识和该用户尝试访问资源的属性。</span><span class="sxs-lookup"><span data-stu-id="5955f-114">Imperative checks can be based on simple policies or policies which evaluate both the user identity and properties of the resource that the user is attempting to access.</span></span>

## <a name="namespaces"></a><span data-ttu-id="5955f-115">命名空间</span><span class="sxs-lookup"><span data-stu-id="5955f-115">Namespaces</span></span>

<span data-ttu-id="5955f-116">授权组件，包括`AuthorizeAttribute`和`AllowAnonymousAttribute`中找不到属性，`Microsoft.AspNetCore.Authorization`命名空间。</span><span class="sxs-lookup"><span data-stu-id="5955f-116">Authorization components, including the `AuthorizeAttribute` and `AllowAnonymousAttribute` attributes, are found in the `Microsoft.AspNetCore.Authorization` namespace.</span></span>

<span data-ttu-id="5955f-117">请查阅上的文档[简单授权](xref:security/authorization/simple)。</span><span class="sxs-lookup"><span data-stu-id="5955f-117">Consult the documentation on [simple authorization](xref:security/authorization/simple).</span></span>
