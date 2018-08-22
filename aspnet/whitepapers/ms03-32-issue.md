---
uid: whitepapers/ms03-32-issue
title: 应用 IE 安全更新后的服务器应用程序不可用错误修复 |Microsoft Docs
author: rick-anderson
description: 本白皮书介绍了影响 Wi 上运行的 ASP.NET 1.0 应用程序的 Internet explorer 与 MS03 32 安全更新解决了问题的修补程序...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 1365eebb-bdf7-4a05-8d18-7f200531be55
msc.legacyurl: /whitepapers/ms03-32-issue
msc.type: content
ms.openlocfilehash: ce2d705a93577b0c6d28f86069873c6ecd891db6
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826621"
---
<a name="fix-for-server-application-unavailable-error-after-applying-security-update-for-ie"></a>应用 IE 安全更新后的服务器应用程序不可用错误修复
====================
> 本白皮书介绍会影响 ASP.NET 1.0 应用程序在 Windows XP Professional 上运行的 Internet explorer 与 MS03 32 安全更新解决了问题的修补程序。
> 
> 适用于 ASP.NET 1.0 和 Windows XP Professional。


Microsoft 使用 Internet Explorer 的安全修补程序 MS03 32 安全更新和 Windows XP 上运行的 ASP.NET 1.0 标识问题。 手动或通过从 Windows 更新站点获取最新的关键更新，可以安装此修补程序。

此问题的症状是，在 Windows XP 计算机上安装此修补程序之后, 对本地 IIS 5.1 web 服务器上运行的 ASP.NET 应用程序的所有请求都导致错误消息，指出"服务器应用程序不可用"。 对远程 web 服务器的请求不会受到影响。

此问题只会影响在 Windows XP 上运行 ASP.NET 1.0 安装。 它不会影响运行 Windows 2000 或 Windows Server 2003 的计算机。 它也不会影响 ASP.NET 1.1 安装运行 Windows XP 的计算机。

请注意，此问题**不是**与 ASP.NET 是安全性错误。 它**却不**打开或允许 ASP.NET 应用程序或服务器遭受恶意攻击。 相反，它是纯粹的功能错误引起的修补程序本身。

我们正在努力针对此问题的永久解决方案。 在此期间，你可以执行以下批处理文件作为此问题的解决方法。 批处理文件执行以下任务：

1. 停止 IIS 和 ASP.NET 状态服务
2. 删除并重新创建具有已知的临时密码的 ASPNET 帐户
3. 使用 Windows`runas`命令以启动创建 ASPNET 用户配置文件的可执行文件
4. 重新注册 ASP.NET。 这将创建新的随机密码的帐户并应用它的默认 ASP.NET 访问控制设置
5. 重新启动 IIS 服务

批处理文件包含硬编码的临时密码"<strong>1pass@word</strong>"您将提示你输入的 runas 命令运行此批处理文件。 Runas 命令完成后，ASPNET 帐户密码的强随机值重新创建。 请注意，如果硬编码密码不符合您的环境中的密码复杂性要求，可能会失败的批处理文件。 如果是这种情况，可以将其更改为另一个适用于你的环境的值。

*> [!IMPORTANT]* 如果已添加自定义访问控制设置或数据库帐户为 ASPNET 帐户的权限，他们将需要此批处理文件完成后重新创建。 这是因为时重新创建该帐户，它将获取新的安全标识符 (SID)。

*> [!IMPORTANT]* 如果运行的 ASP.NET 工作进程的非 ASPNET 帐户的自定义帐户，则应不运行此批处理文件。 相反，应以交互方式登录，或与该帐户将创建该帐户的用户配置文件中使用 runas 命令。

下面的自解压缩存档中包含的批处理文件。 若要使用它：

1. 您必须为帐户运行，使用管理员权限
2. [下载并打开自解压可执行文件](ms03-32-issue/_static/fixup1.exe)
3. 将内容提取到 c:\
4. 从开始菜单中，选择运行...并输入 `cmd.exe`
5. 在打开命令窗口中，键入`c:\fixup.cmd`。
6. 出现提示时，输入<strong>1pass@word</strong>作为密码。
7. 如果你有以前自定义访问控制设置或数据库帐户为 ASPNET 帐户的权限，你需要立即重新应用这些设置。

这导致不便的许多道歉。 当提供时，我们将发布的其他信息。

下表详细介绍了平台和版本受此问题。

| .NET Framework | 平台 | 受影响 |
| --- | --- | --- |
| 版本 1.0 | Windows 2000 Professional | 否 |
| 版本 1.0 | Windows 2000 Server | 否 |
| 版本 1.0 | Windows XP Professional | 是 |
| 版本 1.0 | Windows Server 2003 | 否 |
| 版本 1.0 | 使用 Cassini 的 Windows XP Home | 否 |
| 版本 1.1 | Windows 2000 Professional | 否 |
| 版本 1.1 | Windows 2000 Server | 否 |
| 版本 1.1 | Windows XP Professional | 否 |
| 版本 1.1 | Windows Server 2003 | 否 |
| 版本 1.1 | 使用 Cassini 的 Windows XP Home | 否 |

谢谢你，   
 ASP.NET 团队
