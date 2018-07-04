---
title: 杂项 ASP.NET Core 数据保护 Api
author: rick-anderson
description: 了解有关 ASP.NET Core 数据保护 ISecret 接口。
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/extensibility/misc-apis
ms.openlocfilehash: 114cdd6209970e46b827e403fbe79b95692d0242
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36279150"
---
# <a name="miscellaneous-aspnet-core-data-protection-apis"></a>杂项 ASP.NET Core 数据保护 Api

<a name="data-protection-extensibility-mics-apis"></a>

>[!WARNING]
> 实现的任意以下接口的类型应该是线程安全的多个调用方。

## <a name="isecret"></a>ISecret

`ISecret`接口表示一个机密的值，如加密的密钥材料。 它包含以下 API 图面：

* `Length`: `int`

* `Dispose()`: `void`

* `WriteSecretIntoBuffer(ArraySegment<byte> buffer)`: `void`

`WriteSecretIntoBuffer`方法填充原始机密值与提供的缓冲区。 此 API 将作为参数的缓冲区的原因而不返回`byte[]`直接是，这使调用方机会固定限制对托管的垃圾回收器的机密暴露该缓冲区对象。

`Secret`类型是的具体实现`ISecret`机密的值在进程中内存中的存储位置。 在 Windows 平台上的机密的值加密通过[CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx)。
