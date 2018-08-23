---
uid: webhooks/diagnostics/debugging
title: 调试 ASP.NET Webhook |Microsoft Docs
author: rick-anderson
description: 如何调试 ASP.NET Webhook。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833265"
---
# <a name="aspnet-webhooks-debugging"></a>调试 ASP.NET Webhook  

## <a name="debugging-in-azure"></a>在 Azure 中进行调试

若要在 Azure 中运行时调试 Web 应用程序，请参阅本教程[使用 Visual Studio 的 Azure 应用服务中 web 应用进行故障排除](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)。

## <a name="debugging-with-source-and-symbols"></a>使用源和符号进行调试

除了调试您自己的代码，就可以直接在 Microsoft ASP.NET Webhook 和实际进行调试的所有.NET。 这样无论是否在本地或远程调试。 首先，配置 Visual Studio 以找到的源和符号： 转到**调试**，然后**选项和设置**。 设置选项如下：

![选项和设置](_static/SourceSymbols.png)

然后添加一个链接到[symbolsource.org](http://symbolsource.org)下载的源和符号。 转到**符号**上方的菜单选项卡，并作为符号位置添加以下：

```
http://srv.symbolsource.org/pdb/Public
```

此外，请确保缓存目录的短名称;否则无论文件名称这将导致要加载的符号，可能会太长。 示例路径为：

```
C:\SymCache
```

设置应类似于以下所示：

![选项符号文件位置示例](_static/SymSource.png)
