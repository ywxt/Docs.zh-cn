---
title: 在 ASP.NET Core 中授权简介
author: rick-anderson
description: 了解授权以及授权 ASP.NET Core 应用中的工作方式的基础知识。
ms.author: riande
ms.date: 10/14/2016
uid: security/authorization/introduction
ms.openlocfilehash: 5465eb7875ebecd77b628376ef886db0ddd05025
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276862"
---
# <a name="introduction-to-authorization-in-aspnet-core"></a>在 ASP.NET Core 中授权简介

<a name="security-authorization-introduction"></a>

授权是指确定进程用户是能够执行。 例如，管理用户可以创建文档库、 将文档添加、 编辑文档，以及删除它们。 使用库的非管理用户仅有权读取文档。

授权是正交和独立于身份验证。 但是，授权要求的身份验证机制。 身份验证是有助于确定用户是谁的过程。 身份验证可能会创建一个或多个标识为当前用户。

## <a name="authorization-types"></a>授权类型

ASP.NET 核心授权提供一个简单、 声明性[角色](xref:security/authorization/roles)以及丰富[基于策略的](xref:security/authorization/policies)模型。 要求，以表示授权，并且处理程序评估针对需求的用户的声明。 命令性检查可以基于简单的策略或策略的评估用户标识和该用户尝试访问资源的属性。

## <a name="namespaces"></a>命名空间

授权组件，包括`AuthorizeAttribute`和`AllowAnonymousAttribute`中找不到属性，`Microsoft.AspNetCore.Authorization`命名空间。

请查阅上的文档[简单授权](xref:security/authorization/simple)。
