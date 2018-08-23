---
uid: whitepapers/denied-access-to-iis-directories
title: ASP.NET 拒绝对 IIS 目录的访问 |Microsoft Docs
author: rick-anderson
description: 本白皮书介绍了对 ASP.NET 应用程序请求将返回错误，"拒绝访问 DirectoryName 目录如果您必须做什么。 失败为 s...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: c3a14f51df7aaf5c5935cf60ee4e687c10048e91
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833133"
---
<a name="aspnet-denied-access-to-iis-directories"></a>ASP.NET 拒绝对 IIS 目录的访问
====================
> 本白皮书介绍了对 ASP.NET 应用程序的请求将返回错误，如果您必须做什么"拒绝访问权限*DirectoryName*目录。 无法开始监视目录更改。"
> 
> 适用于 ASP.NET 1.0 和 ASP.NET 1.1。


ASP.NET V1 RTM 现在运行在使用无特权 windows 帐户的注册为本地计算机上的"ASPNET"帐户。

在某些情况下系统锁定状态，此帐户可能会默认情况下不具有读取安全访问的网站内容目录、 应用程序根目录以外的目录或网站根目录。 在这种情况下从给定的 web 应用程序请求页时将收到以下错误：

![](denied-access-to-iis-directories/_static/image1.jpg)

若要解决此问题将需要更改上的相应目录的安全权限。

具体而言，ASP.NET 需要读取、 执行和列出网站根目录的 ASPNET 帐户的访问权限 (例如： c:\inetpub\wwwroot 或可能在 IIS 中配置任何其他站点目录)，内容目录和应用程序根目录下若要监视的配置文件更改。 应用程序根对应于与 IIS 管理工具 (inetmgr) 中的应用程序虚拟目录关联的文件夹路径。

例如，考虑以下应用程序层次结构的 wwwroot 文件夹下。

`C:\inetpub\wwwroot\myapp\default.aspx`

此示例中，为 ASPNET 帐户需上面定义 myapp 和的 wwwroot 目录中的内容的读取的权限。 在根文件夹的单个继承的 ACL 还可以选择可为两个目录如果它们嵌套。

若要添加到目录的权限，请执行以下步骤：

- 使用 Windows 资源管理器，导航到的目录
- 右键单击目录文件夹，然后选择"属性"
- 导航到属性对话框上的"安全性"选项卡
- 单击"添加"按钮并输入计算机名称后跟 ASPNET 帐户名称。 例如，在计算机上名为"webdev"，将输入 webdev\ASPNET 并点击"确定"。
- 请确保 ASPNET 帐户具有"读取&amp;Execute"，"列出文件夹内容"，并选中"读取"复选框。
- 点击确定以关闭该对话框并保存所做的更改。

![](denied-access-to-iis-directories/_static/image2.jpg)

如果需要，可以通过 Windows 使用脚本或附带的"cacls.exe"工具自动这些更改。 ASPNET 帐户的详细信息，请参阅[篇常见问题解答文档](https://go.microsoft.com/fwlink/?LinkId=5828)。

如果给定的 web 应用程序依赖于具有写入或修改特定文件夹或文件的权限，这可以授予通过遵循相同的过程，并检查"写入"和/或"修改"复选框。

将允许每个人或用户组读取访问权限 （这是默认配置） 这些目录的计算机上遇到任何问题，则不需要上述步骤。
