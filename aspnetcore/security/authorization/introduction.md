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
# <a name="introduction"></a>介绍

<a name="security-authorization-introduction"></a>

授权是指确定进程用户是能够执行。 例如，管理用户可以创建文档库、 将文档添加、 编辑文档，以及删除它们。 使用库的非管理用户仅有权读取文档。

授权是正交和独立于身份验证，这是有助于确定用户是谁的过程。 身份验证可能会创建一个或多个标识为当前用户。

## <a name="authorization-types"></a>授权类型

ASP.NET 核心授权提供一个简单的声明性[角色](roles.md)和[基于的丰富策略](policies.md)模型。 要求，以表示授权，并且处理程序评估针对需求的用户的声明。 命令性检查可以基于简单的策略或策略的评估用户标识和该用户尝试访问资源的属性。

## <a name="namespaces"></a>命名空间

授权组件，包括`AuthorizeAttribute`和`AllowAnonymousAttribute`中找不到属性`Microsoft.AspNetCore.Authorization`命名空间。
