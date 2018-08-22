---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: 单一登录 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: feace28c373a767453b1b984f6fdc5a3d97a9217
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831057"
---
<a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a>单一登录 （使用 Azure 构建实际云应用）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关电子书的信息，请参阅[的第一章](introduction.md)。


有很多安全问题，需考虑当正在开发云应用程序，但这一系列的情况下，我们将着眼于只是一个： 单一登录。 问题人们经常问这是:"我要主要构建应用我的公司; 员工如何托管这些应用在云中，同时让他们能够使用相同的安全模型，我的员工了解它们的运行应用时使用的本地环境中托管的防火墙内？" 我们启用此方案的方法之一是名为 Azure Active Directory (Azure AD)。 Azure AD，可使企业业务线 (LOB) 应用程序可通过 Internet，并且它使您能够将这些应用提供给业务合作伙伴。

## <a name="introduction-to-azure-ad"></a>Azure AD 简介

[Azure AD](https://docs.microsoft.com/azure/active-directory/)提供了[Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx)在云中。 主要功能包括：

- 它与在本地 Active Directory 集成。
- 这样，与您的应用程序的单一登录。
- 它支持开放标准，例如[SAML](http://en.wikipedia.org/wiki/SAML_2.0)， [Ws-fed](http://en.wikipedia.org/wiki/WS-Federation)，并[OAuth 2.0](http://oauth.net/2/)。
- 它支持企业[Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx)。

假设您有用于使员工能够登录到 Intranet 应用程序的本地 Windows Server Active Directory 环境：

![](single-sign-on/_static/image1.png)

什么 Azure AD，您可以执行是在云中创建一个目录。 它是一项免费功能且易于设置。

它可以是完全独立于你的本地 Active Directory;您可以将任何人都希望在它和 Internet 应用程序进行身份验证。

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

也可以将它集成与你的本地 AD。

![AD 和 WAAD 集成](single-sign-on/_static/image3.png)

现在可以进行本地身份验证的所有雇员可以还进行身份都验证通过 Internet-而无需打开防火墙或者部署你的数据中心中的任何新服务器。 您可以继续利用所有现有 Active Directory 环境的了解和使用其目前用于提供有关功能的内部应用单一登录。

后所做的 AD 和 Azure AD 之间的连接，您还可以启用你的 web 应用和移动设备进行身份验证你的员工在云中，你可以启用第三方应用，例如 Office 365、 SalesForce.com 或 Google 应用以接受你员工的凭据。 如果你使用 Office 365，你在设置了与 Azure AD 由于 Office 365 使用 Azure AD 进行身份验证和授权。

![第三方应用](single-sign-on/_static/image4.png)

此方法的优点是的每当你的组织添加或删除用户，或在用户更改密码，则使用你当前使用的本地环境中的同一个进程。 所有的你的本地 AD 的更改会自动传播到云环境。

如果你的公司使用或移动到 Office 365，值得高兴的，则必须自动设置因为 Office 365 使用 Azure AD 进行身份验证的 Azure AD。 因此，可以轻松地使用自己的应用程序中相同 Office 365 使用的身份验证。

## <a name="set-up-an-azure-ad-tenant"></a>设置 Azure AD 租户

Azure AD 目录称为一个 Azure AD[租户](https://technet.microsoft.com/library/jj573650.aspx)，而且设置租户非常简单。 我们将展示如何它通过 Azure 管理门户以阐明这些概念，但当然等其他门户函数还可以执行它通过使用脚本或管理 API。

在管理门户中单击 Active Directory 选项卡。

![在门户中的 WAAD](single-sign-on/_static/image5.png)

自动为你的 Azure 帐户，具有一个 Azure AD 租户，可以单击**添加**页后，可以创建其他目录底部的按钮。 建议一个用于测试环境，另一个用于生产，例如。 仔细考虑命名新目录。 如果你使用你的目录的名称以及如何将您再次为其中一个的用户，可能会造成混淆的名称。

![添加目录](single-sign-on/_static/image6.png)

该门户的完全支持创建、 删除和管理此环境中的用户。 例如，若要添加用户转到**用户**选项卡，单击**添加用户**按钮。

![添加用户按钮](single-sign-on/_static/image7.png)

![添加用户对话框](single-sign-on/_static/image8.png)

您可以创建仅在此目录中存在的新用户或可以为此目录中或注册的用户或另一个 Azure AD 目录中的用户注册 Microsoft 帐户，为此目录中的用户。 （在真实的目录，默认域为 ContosoTest.onmicrosoft.com。 您还可以使用您自己选择，如 contoso.com 的域。）

![用户类型](single-sign-on/_static/image9.png)

![添加用户对话框](single-sign-on/_static/image10.png)

可以将用户分配到角色。

![用户配置文件](single-sign-on/_static/image11.png)

并使用一个临时密码创建帐户。

![临时密码](single-sign-on/_static/image12.png)

这种方式创建的用户立即可以登录到 web 应用使用此云目录。

什么是适用于企业单一登录，不过，是**目录集成**选项卡：

![目录集成选项卡](single-sign-on/_static/image13.png)

如果启用目录集成，并[下载的工具，](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)，可以同步与现有的本地 Active Directory，你已在组织内部使用此云目录。 然后的所有用户存储在你的目录中将显示在此云目录。 你的云应用现在可以验证所有员工使用其现有的 Active Directory 凭据。 这是所有免费 – 同步工具和 Azure AD 本身和。

该工具是一个向导，是易于使用，因为这些屏幕截图中所示。 这些不是完整的说明，只是一个示例显示基本过程。 更多详细说明-将执行操作的 it 信息，请参阅中的链接[资源](#resources)本章末尾部分。

![WAAD 同步工具配置向导](single-sign-on/_static/image14.png)

单击**下一步**，然后输入你的 Azure Active Directory 凭据。

![WAAD 同步工具配置向导](single-sign-on/_static/image15.png)

单击**下一步**，然后输入你的本地 AD 凭据。

![WAAD 同步工具配置向导](single-sign-on/_static/image16.png)

单击**下一步**，，然后指明你想要在云中存储的 AD 密码哈希值。

![WAAD 同步工具配置向导](single-sign-on/_static/image17.png)

可以在云中存储密码哈希是单向哈希;实际的密码永远不会存储在 Azure AD 中。 如果又决定不将哈希值存储在云中，你必须使用[Active Directory 联合身份验证服务](https://technet.microsoft.com/library/hh831502.aspx)(ADFS)。 此外，还有[时要考虑其他因素选择是否使用 ADFS](https://technet.microsoft.com/library/jj573653.aspx)。 ADFS 选项需要几个其他配置步骤。

如果您选择将哈希值存储在云中，完成后，该工具启动时单击同步目录**下一步**。

![WAAD 同步工具配置向导](single-sign-on/_static/image18.png)

在几分钟内就大功告成了。

![WAAD 同步工具配置向导](single-sign-on/_static/image19.png)

只需运行此组织，在 Windows 2003 或更高版本中的一个域控制器上。 且无需重新启动。 当完成，你的所有用户都位于云中，可以执行从任何 web 或移动应用程序，使用 SAML、 OAuth 或 WS 联合身份验证的单一登录。

有时我们有人问这是有关如何安全 – 没有 Microsoft 用于它自己的敏感业务数据？ 和答案为的是我们执行操作。 例如，如果转到内部 Microsoft SharePoint 站点[ https://microsoft.sharepoint.com/ ](https://microsoft.sharepoint.com/)，会提示登录。

![Office 365 登录](single-sign-on/_static/image20.png)

Microsoft 已启用 ADFS，因此当您进入 Microsoft ID，您重定向到 ADFS 登录页。

![ADFS 登录](single-sign-on/_static/image21.png)

和后输入凭据存储在内部 Microsoft AD 帐户后，您可以访问到此内部应用程序。

![MS SharePoint 站点](single-sign-on/_static/image22.png)

主要是因为我们已经有 Azure AD 变得可用，但在云中的 Azure AD 目录正处于登录过程前设置 ADFS，我们将使用 AD 在登录服务器。 我们将我们的重要文档、 源代码管理、 性能管理文件、 销售报表和详细信息，在云中，并将此确切的同一个解决方案来保护它们。

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a>创建使用 Azure AD 进行单一登录的 ASP.NET 应用

Visual Studio 可以十分轻松地创建的应用程序使用 Azure AD 进行单一登录，您可以看到从几个屏幕截图。

创建一个新 ASP.NET 应用程序，MVC 或 Web 窗体时的默认身份验证方法是 ASP.NET 标识。 若要更改到 Azure AD，请单击**更改身份验证**按钮。

![更改身份验证](single-sign-on/_static/image23.png)

选择组织帐户，输入你的域名，并选择单一登录。

![配置身份验证对话框](single-sign-on/_static/image24.png)

您可以还授予应用程序读取或读/写权限的目录数据。 如果这样做，它可以使用[Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx)若要查找用户的电话号码，了解它们是否在办公室中，当最后一个记录，等等。

这就是您需要做的所有 Visual Studio 会要求输入凭据的 Azure AD 租户的管理员，然后配置你的项目和新的应用程序在 Azure AD 租户。

运行项目时，你将看到在登录页，并在 Azure AD 目录中可以使用的用户的凭据登录。

![组织帐户登录](single-sign-on/_static/image25.png)

![登录](single-sign-on/_static/image26.png)

当应用部署到 Azure 时，只需是选择**启用组织身份验证**复选框，然后再一次 Visual Studio 负责为您的所有配置。

![发布 Web](single-sign-on/_static/image27.png)

这些屏幕截图来自演示了如何生成使用 Azure AD 身份验证的应用程序的完整分步教程：[与 Azure Active Directory 开发 ASP.NET 应用程序](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)。

## <a name="summary"></a>总结

这一章中您可以看到，Azure Active Directory、 Visual Studio 和 ASP.NET，使其易于设置组织的用户的 Internet 应用程序中的单一登录。 你的用户可以使用他们用于登录在您的内部网络中使用 Active Directory 的相同凭据的 Internet 应用程序中登录。

[接下来的章节](data-storage-options.md)查看可用于云应用程序的数据存储选项。

<a id="resources"></a>
## <a name="resources"></a>资源

有关更多信息，请参见以下资源：

- [Azure Active Directory 文档](https://docs.microsoft.com/azure/active-directory/)。 Windowsazure.com 站点上的 Azure AD 文档的门户页。 有关分步教程，请参阅**开发**部分。
- [Azure 多重身份验证](https://docs.microsoft.com/azure/multi-factor-authentication/)。 有关在 Azure 中的多重身份验证的文档的门户页。
- [组织帐户身份验证选项](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)。 在 Visual Studio 2013 新项目对话框中的 Azure AD 身份验证选项的说明。
- [Microsoft 模式和实践-联合身份模式](https://msdn.microsoft.com/library/dn589790.aspx)。
- [如何： 安装 Azure Active Directory Sync 工具](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)。
- [Active Directory 联合身份验证服务 2.0 内容导航图](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)。 链接到有关 ADFS 2.0 的文档。
- [Windows Azure AD 应用程序中基于角色的和基于 ACL 的授权](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)。 示例应用程序。
- [Azure Active Directory 图形 API 博客](https://blogs.msdn.com/b/aadgraphteam/)。
- [访问控制在 BYOD 和混合标识基础结构中的目录集成](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)。 Tech Ed 2014 会话视频通过 Gayana Bagdasaryan。

> [!div class="step-by-step"]
> [上一页](web-development-best-practices.md)
> [下一页](data-storage-options.md)
