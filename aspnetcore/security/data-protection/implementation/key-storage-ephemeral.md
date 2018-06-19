---
title: ASP.NET 核心中的临时数据保护提供程序
author: rick-anderson
description: 了解 ASP.NET 核心暂时数据保护提供程序的实现详细信息。
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/implementation/key-storage-ephemeral
ms.openlocfilehash: 9cdd3949826091807f3139f51aa0c05ddaac696a
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
ms.locfileid: "30076129"
---
# <a name="ephemeral-data-protection-providers-in-aspnet-core"></a>ASP.NET 核心中的临时数据保护提供程序

<a name="data-protection-implementation-key-storage-ephemeral"></a>

有的方案： 应用程序需要的 throwaway `IDataProtectionProvider`。 例如，开发人员可能只需在一次性的控制台应用程序中，进行试验或应用程序本身是暂时性 （已编写脚本或单元测试项目）。 若要支持这些方案[Microsoft.AspNetCore.DataProtection](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection/)包包括一种类型`EphemeralDataProtectionProvider`。 此类型提供的基本实现`IDataProtectionProvider`其密钥的存储库保留仅在内存中和不写出到任何后备存储。

每个实例`EphemeralDataProtectionProvider`使用其自身唯一的主密钥。 因此，如果`IDataProtector`处`EphemeralDataProtectionProvider`生成受保护的负载，该负载仅受等效`IDataProtector`(给定相同[目的](xref:security/data-protection/consumer-apis/purpose-strings#data-protection-consumer-apis-purposes)链) 位于同一个取得 root 权限`EphemeralDataProtectionProvider`实例。

下面的示例演示如何实例化`EphemeralDataProtectionProvider`并使用它来保护和取消保护数据。

```csharp
using System;
using Microsoft.AspNetCore.DataProtection;

public class Program
{
    public static void Main(string[] args)
    {
        const string purpose = "Ephemeral.App.v1";

        // create an ephemeral provider and demonstrate that it can round-trip a payload
        var provider = new EphemeralDataProtectionProvider();
        var protector = provider.CreateProtector(purpose);
        Console.Write("Enter input: ");
        string input = Console.ReadLine();

        // protect the payload
        string protectedPayload = protector.Protect(input);
        Console.WriteLine($"Protect returned: {protectedPayload}");

        // unprotect the payload
        string unprotectedPayload = protector.Unprotect(protectedPayload);
        Console.WriteLine($"Unprotect returned: {unprotectedPayload}");

        // if I create a new ephemeral provider, it won't be able to unprotect existing
        // payloads, even if I specify the same purpose
        provider = new EphemeralDataProtectionProvider();
        protector = provider.CreateProtector(purpose);
        unprotectedPayload = protector.Unprotect(protectedPayload); // THROWS
    }
}

/*
* SAMPLE OUTPUT
*
* Enter input: Hello!
* Protect returned: CfDJ8AAAAAAAAAAAAAAAAAAAAA...uGoxWLjGKtm1SkNACQ
* Unprotect returned: Hello!
* << throws CryptographicException >>
*/
```
