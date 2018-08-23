---
uid: whitepapers/aspnet-and-iis6
title: 通过 IIS 6.0 运行 ASP.NET 1.1 |Microsoft Docs
author: rick-anderson
description: Windows Server 2003 包括 IIS 6.0 和 ASP.NET 1.1，默认情况下禁用这些组件。 本白皮书介绍了如何启用 IIS 6.0...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 38cd0abc1e9133b9b86cff6dd2759ce98ac5a115
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832241"
---
<a name="running-aspnet-11-with-iis-60"></a>通过 IIS 6.0 运行 ASP.NET 1.1
====================
> Windows Server 2003 包括 IIS 6.0 和 ASP.NET 1.1，默认情况下禁用这些组件。 本白皮书介绍如何启用 IIS 6.0 和 ASP.NET 1.1 中，并推荐几项配置设置以从 IIS 和 ASP.NET 中获得最佳性能。
> 
> 适用于 ASP.NET 1.1 和 IIS 6.0。


ASP.NET 1.1 附带有 Windows Server 2003，还包括最新版本的 Internet 信息服务器 (IIS) 6.0 版。 IIS 6.0 和 ASP.NET 1.1 旨在无缝集成，且 ASP.NET 现在默认为新的 IIS 6.0 工作进程模型。

## <a name="aspnet-11-is-not-installed-by-default"></a>默认情况下未安装 ASP.NET 1.1

与以前版本的 Microsoft 的服务器操作系统，不同的是 Internet 信息服务器 (IIS) 未启用默认设置。也不是 ASP.NET 1.1。 有两个选项用于启用 IIS:

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a>启用 IIS，选项 #1-配置服务器向导

Windows Server 2003 提供了新配置服务器向导来帮助你正确配置你的服务器中所需的模式。

若要启动向导-请注意，若要运行的向导必须以管理员身份的身份登录，请转到： 启动 |程序 |管理工具并选择配置您的服务器。

选择后，你应看到在配置服务器向导打开的屏幕：

![](aspnet-and-iis6/_static/image1.jpg)

单击下一步&gt;:

![](aspnet-and-iis6/_static/image2.jpg)

单击下一步&gt;

![](aspnet-and-iis6/_static/image3.jpg)

在此屏幕上，你将需要选择应用程序服务器 （IIS、 ASP.NET） 作为配置的选项。

单击下一步&gt;。

![](aspnet-and-iis6/_static/image4.jpg)

选择后将服务器配置为应用程序服务器，此屏幕将显示提示应安装哪些其他功能。 默认情况下选择任何选项。 若要自动启用 ASP.NET，您需要选择启用 ASP。NET。

单击下一步&gt;。

![](aspnet-and-iis6/_static/image5.jpg)

此屏幕显示选项，可安装。

单击下一步&gt;。

![](aspnet-and-iis6/_static/image6.jpg)

所选的选项在安装时，你将看到此屏幕。 它是正常的其他对话框框显示为正在安装服务。 您可能此外会提示输入 Windows 2003 Server 安装光盘的位置。

单击下一步&gt;时完成。

![](aspnet-and-iis6/_static/image7.jpg)

单击完成-Windows Server 2003 现在已配置为支持 IIS 6.0 和 ASP.NET 1.1。

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a>启用 IIS，选项 #2-手动配置 IIS 和 ASP.NET

如果不希望使用配置服务器向导可以根据需要安装 IIS 6.0 和 ASP.NET 1.1 使用添加或删除程序从控制面板。

首次打开控制面板：

![](aspnet-and-iis6/_static/image8.jpg)

接下来，单击添加/删除 Windows 组件以打开 Windows 组件向导:

![](aspnet-and-iis6/_static/image9.jpg)

突出显示并检查应用程序服务器，然后单击详细信息？ 按钮：

![](aspnet-and-iis6/_static/image10.jpg)

若要安装 ASP.NET，检查 ASP。NET。

单击确定以返回到 Windows 组件向导。 单击下一步&gt;从 Windows 组件向导以开始安装：

![](aspnet-and-iis6/_static/image11.jpg)

它是正常的其他对话框框显示为正在安装服务。 您可能此外会提示输入 Windows 2003 Server 安装光盘的位置。

安装完成后您将看到 Windows 组件向导的最后一个屏幕：

![](aspnet-and-iis6/_static/image12.jpg)

IIS 6.0 和 ASP.NET 1.1 现在都已配置并且可用。

## <a name="recommended-settings"></a>建议的设置

使用 IIS 6.0 运行 ASP.NET 1.1 时有多个要从 ASP.NET 获取最佳性能，建议的配置设置：

- 配置工作线程进程内存限制
- 配置工作进程回收

### <a name="configuring-worker-process-memory-limits"></a>配置工作线程进程内存限制

默认情况下 IIS 6.0 不允许 IIS 使用的内存量设置限制。 ASP。NET 的缓存功能依赖于内存的限制，以便从内存中缓存可以主动删除未使用的项。

建议配置内存回收 IIS 6.0 的功能。 若要配置此打开的 Internet 信息服务管理器 (启动 |程序 |管理工具 |Internet 信息服务）。 一旦打开，请展开应用程序池文件夹：

为每个应用程序池：

![](aspnet-and-iis6/_static/image13.jpg)

1. 右键单击应用程序池例如DefaultAppPool，并选择属性:

![](aspnet-and-iis6/_static/image14.jpg)

2. 接下来，启用内存回收单击任何一个最大值 （以兆字节为单位） 使用的内存:。 值不应为多个服务器上的 （不是虚拟的） 的物理内存量、 准确的估算是 60%的物理内存，即为具有 512 MB 的物理内存选择 310 的服务器。 此外建议使用 2 GB 的地址空间时，最大值将不超过 800 mb 的空间。 如果服务器的内存地址空间为 3 GB，工作进程的最大内存限制最高可为 1，800 mb 的空间：

![](aspnet-and-iis6/_static/image15.jpg)

单击应用和确定退出属性对话框。 重复此步骤的所有可用的应用程序池。

### <a name="configuring-worker-recycling"></a>配置辅助角色回收

默认情况下 IIS 6.0 配置为每 29 小时回收其工作进程。 这是有点主动运行 ASP.NET 的应用程序，建议，禁用自动工作进程回收。

若要禁用自动工作进程回收，请先打开 Internet 信息服务管理器 (启动 |程序 |管理工具 |Internet 信息服务）。 一旦打开，请展开应用程序池文件夹：

![](aspnet-and-iis6/_static/image16.jpg)

为每个应用程序池：

1. 右键单击应用程序池例如DefaultAppPool，并选择属性:

![](aspnet-and-iis6/_static/image17.jpg)

2. 取消选中回收工作进程 （分钟）::

![](aspnet-and-iis6/_static/image18.jpg)

单击应用和确定退出属性对话框。 重复此步骤的所有可用的应用程序池。

## <a name="granting-write-access-to-the-file-system"></a>授予对文件系统的写访问权限

如果你的应用程序需要写到文件系统的访问权限，并且使用 NTFS，需要修改访问控制列表 (ACL) 上的文件夹或文件授予对 ASP.NET 访问权限。

例如，若要授予 ASP.NET 到 c:\inetpub\wwwroot 的写访问权限首次打开资源管理器并导航到的目录：

![](aspnet-and-iis6/_static/image19.jpg)

接下来，右键单击该目录，例如 wwwroot 并选择属性。 属性对话框打开后，选择安全选项卡：

![](aspnet-and-iis6/_static/image20.jpg)

C:\inetpub\wwwroot\ 目录是一个特殊目录中的特殊 IIS 6.0 组 IIS\_WPG 已授予读取&amp;执行、 列出文件夹内容、 和读取权限。 但是，若要授予写入权限，需要单击允许复选框以进行写入：

![](aspnet-and-iis6/_static/image21.jpg)

IIS 6.0 现在对此文件夹具有写权限。 若要授予写权限，对其他文件夹，请按照以下步骤-请注意，可能需要添加 IIS\_WPG 组如果尚不存在。

> [!CAUTION]
> 授予对 IIS 的写入权限\_WPG 将允许任何 ASP.NET 应用程序写入到该目录。

## <a name="supporting-integrated-authentication-with-sql-server"></a>支持与 SQL Server 的集成身份验证

集成身份验证允许 SQL Server 利用 Windows NT 身份验证来验证 SQL Server 登录帐户。 这允许用户绕过标准的 SQL Server 登录过程。 使用此方法时，网络用户可以访问 SQL Server 数据库，无需提供单独的登录标识或密码，因为 SQL Server 获取从 Windows NT 网络安全过程的用户和密码信息。

选择集成身份验证的 ASP.NET 应用程序是一个不错的选择，因为你的应用程序在连接字符串中曾经不存储任何凭据。 而是用来连接到 SQL 连接字符串将如下所示：

`"server=localhost; database=Northwind;Trusted_Connection=true"`

此连接字符串告知 SQL Server 以使用应用程序尝试访问 SQL Server 的 Windows 凭据。 在 ASP.NET/IIS 6 的情况下这会在 IIS 中的帐户\_WPG 组。

若要启用 SQL Server 和 ASP.NET 之间的集成身份验证，你将需要首先确保 SQL Server 配置为集成身份验证或混合模式身份验证-请与您的 DBA 可以确定这一点。 如果这两种模式之一是 SQL Server，可以使用集成身份验证。

打开 SQL Server 企业管理器 (启动 |程序 |Microsoft SQL Server |企业管理器），选择相应的服务器，并展开安全性文件夹：

![](aspnet-and-iis6/_static/image22.jpg)

如果 BUILTINT\IIS\_WPG 未列出组，右键单击登录名并选择新建登录名:

![](aspnet-and-iis6/_static/image23.jpg)

在名称: 文本框中输入 [服务器/Domain Name] \IIS\_WPG' 或单击省略号按钮以打开 Windows NT 用户/组选取器：

![](aspnet-and-iis6/_static/image24.jpg)

选择当前计算机的 IIS\_WPG 组，然后单击添加和确定以关闭选择器。

然后需要也设置为默认数据库并有权访问数据库。 若要设置的默认数据库选择从下拉列表中，如下面的 Northwind 处于选中状态：

![](aspnet-and-iis6/_static/image25.jpg)

接下来，单击数据库访问权限选项卡：

![](aspnet-and-iis6/_static/image26.jpg)

单击你想要允许访问每个数据库的允许复选框。 您还需要选择数据库角色检查 db\_所有者将确保你的登录名具有所有必需的权限来管理并使用所选的数据库。

单击确定退出属性对话框。 ASP.NET 应用程序现在已配置为支持集成的 SQL Server 身份验证。

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a>不在 IIS 6.0 本机模式下运行 ASP.NET 1.0

IIS 6.0 上的 ASP.NET 1.0 仅支持在 IIS 5 兼容性模式下。

若要配置 ASP.NET 1.0 在 IIS 5.0 兼容性模式下运行，请打开 Internet 服务管理器和右键单击网站并选择属性:

![](aspnet-and-iis6/_static/image27.jpg)

切换到服务选项卡并检查？在 IIS 5.0 隔离模式运行 WWW 服务？:

![](aspnet-and-iis6/_static/image28.jpg)
