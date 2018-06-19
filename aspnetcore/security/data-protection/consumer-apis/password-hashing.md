---
title: 在 ASP.NET 核心中的哈希密码
author: rick-anderson
description: 了解如何使用 ASP.NET 核心数据保护 Api 的密码执行哈希。
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/consumer-apis/password-hashing
ms.openlocfilehash: f44e66789bf348ef6d99f6d862fb34c2d943a0b2
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32740096"
---
# <a name="hash-passwords-in-aspnet-core"></a>在 ASP.NET 核心中的哈希密码

基本数据保护代码包括包*Microsoft.AspNetCore.Cryptography.KeyDerivation*其中包含加密密钥派生函数。 此包是一个独立组件，并不依赖于数据保护系统的其余部分。 可以完全单独使用它。 源共存于基本为方便起见数据保护代码。

包当前提供一种方法`KeyDerivation.Pbkdf2`这样，哈希密码使用[PBKDF2 算法](https://tools.ietf.org/html/rfc2898#section-5.2)。 此 API 已非常类似于.NET Framework 的现有[Rfc2898DeriveBytes 类型](/dotnet/api/system.security.cryptography.rfc2898derivebytes)，但有三个重要区别：

1. `KeyDerivation.Pbkdf2`方法支持使用多个 PRFs (当前`HMACSHA1`， `HMACSHA256`，和`HMACSHA512`)，而`Rfc2898DeriveBytes`类型仅支持`HMACSHA1`。

2. `KeyDerivation.Pbkdf2`方法检测到当前操作系统，然后尝试选择最优化的实现的例程，提供更好的性能，在某些情况下，选择。 (在 Windows 8 中，它提供约 10 倍的吞吐量`Rfc2898DeriveBytes`。)

3. `KeyDerivation.Pbkdf2`方法要求调用方指定的所有参数 (salt，PRF 和迭代计数)。 `Rfc2898DeriveBytes`类型提供的这些默认值。

[!code-csharp[](password-hashing/samples/passwordhasher.cs)]

ASP.NET 核心标识，请参阅源代码`PasswordHasher`现实世界的类型用例。
