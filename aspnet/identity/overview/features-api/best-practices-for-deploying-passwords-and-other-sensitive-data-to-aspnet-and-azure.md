---
uid: identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
title: 密码和其他敏感数据部署到 ASP.NET 和 Azure 应用服务的最佳做法 |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何在代码可以安全地存储和访问安全信息。 最重要的一点是您应该永远不会存储密码或其他服务...
ms.author: aspnetcontent
ms.date: 05/21/2015
ms.assetid: 97902c66-cb61-4d11-be52-73f962f2db0a
msc.legacyurl: /identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
msc.type: authoredcontent
ms.openlocfilehash: 445e7c32baf4316273b0a5901a776684a6c5d73f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37832450"
---
<a name="best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure-app-service"></a>密码和其他敏感数据部署到 ASP.NET 和 Azure 应用服务的最佳实践
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> 本教程演示如何在代码可以安全地存储和访问安全信息。 最重要的一点是您应永远不会将密码或其他敏感数据存储在源代码中，并且不应在开发和测试模式下使用生产机密。
> 
> 示例代码是一个简单的 web 作业控制台应用和需要访问数据库连接字符串密码，Twilio，Google 和 SendGrid 安全密钥的 ASP.NET MVC 应用程序。
> 
> 在本地设置和 PHP 还将提到。


- [使用开发环境中的密码](#pwd)
- [处理在开发环境中的连接字符串](#con)
- [Web 作业的控制台应用](#wj)
- [将机密部署到 Azure](#da)
- [在本地和 PHP 的说明](#not)
- [其他资源](#addRes)

<a id="pwd"></a>
## <a name="working-with-passwords-in-the-development-environment"></a>使用开发环境中的密码

教程经常在源代码中，希望使用需要特别注意应永远不会将敏感数据存储在源代码中显示的敏感数据。 例如，我[ASP.NET MVC 5 应用程序使用 SMS 和电子邮件 2FA](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)教程演示中的以下*web.config*文件：

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample1.xml)]

*Web.config*文件是源代码，因此这些机密应永远不会存储在该文件中。 幸运的是，`<appSettings>`元素具有`file`可以指定外部文件包含敏感应用程序配置设置的属性。 只要外部文件未签入到源树，可以转到外部文件的所有机密。 例如，在下列标记中，该文件*AppSettingsSecrets.config*包含所有应用程序机密：

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample2.xml)]

外部文件中的标记 (*AppSettingsSecrets.config*在此示例中) 中, 找到相同的标记*web.config*文件：

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample3.xml)]

ASP.NET 运行时将外部文件中的标记的内容合并&lt;appSettings&gt;元素。 如果找不到指定的文件，运行时将忽略文件属性。

> [!WARNING]
> 安全性-不添加你*机密.config*文件添加到你的项目或将其签入源代码管理。 默认情况下，Visual Studio 将设置`Build Action`到`Content`，这意味着该文件部署。 有关详细信息请参阅[不为什么部署所有我的项目文件夹中的文件？](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment) 尽管可以使用任何适用于扩展*机密.config*文件，它是让它 *.config*，如配置文件不是由 IIS。 另请注意*AppSettingsSecrets.config*文件是从两个目录级别向上*web.config*文件，因此它完全不受解决方案目录。 将解决方案目录中，从文件移&quot;git 添加\*&quot;不会将其添加到你的存储库。


<a id="con"></a>
## <a name="working-with-connection-strings-in-the-development-environment"></a>处理在开发环境中的连接字符串

Visual Studio 将创建使用新 ASP.NET 项目[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)。 LocalDB 被创建专门针对开发环境。 它不需要密码，因此你无需执行任何操作来防止机密签入源代码。 一些开发团队使用需要密码的完整版本的 SQL Server （或其他 DBMS）。

可以使用`configSource`属性来替换整个`<connectionStrings>`标记。 与不同`<appSettings>``file`合并标记中，属性`configSource`特性将取代标记。 下面的标记演示`configSource`中的属性*web.config*文件：

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample4.xml?highlight=1)]

> [!NOTE]
> 如果使用`configSource`属性如上所示将您的连接字符串移动到外部文件，并让 Visual Studio 创建新的 web 站点，它将无法检测到您使用的是数据库，并不会获得配置数据库的选项时您 publish 到 Azure，从 Visual Studio。 如果使用的`configSource`属性，可以使用 PowerShell 创建和部署你的网站和数据库，也可以创建 web 站点和数据库在门户中发布之前。 [新建 AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)脚本将创建一个新的 web 站点和数据库。


> [!WARNING]
> 安全性-与不同*AppSettingsSecrets.config*文件中，外部连接字符串文件必须在相同的目录作为根*web.config*文件，因此您必须采取预防措施以确保你不将其签入源代码存储库。


> [!NOTE]
> **机密文件上的安全警告：** 最佳做法是使用测试和开发中的生产机密。 使用生产环境中测试或开发的密码泄漏这些机密。


<a id="wj"></a>
## <a name="webjobs-console-apps"></a>Web 作业的控制台应用

*App.config*文件使用的控制台应用程序不支持相对路径，但它支持绝对路径。 可以使用绝对路径移出您的项目目录的机密。 以下标记显示了中的机密*C:\secrets\AppSettingsSecrets.config*文件和中的非敏感数据*app.config*文件。

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample5.xml?highlight=2)]

<a id="da"></a>
## <a name="deploying-secrets-to-azure"></a>将机密部署到 Azure

将 web 应用部署到 Azure 中，当*AppSettingsSecrets.config*文件不会将部署 （这是所需）。 可以转到[Azure 管理门户](https://azure.microsoft.com/services/management-portal/)和手动设置这些设置，若要执行此操作：

1. 转到[ https://portal.azure.com ](https://portal.azure.com)，并使用你的 Azure 凭据登录。
2. 单击**浏览&gt;Web 应用**，然后单击你的 web 应用的名称。
3. 单击**的所有设置&gt;应用程序设置**。

**应用设置**并**连接字符串**值会重写中的相同设置*web.config*文件。 在本示例中，我们未部署这些设置到 Azure，但如果这些密钥处于*web.config*文件中，在门户上显示的设置将优先。

最佳做法是按照[DevOps 工作流](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md)并用[Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) (或另一个框架[Chef](http://www.opscode.com/chef/)或[Puppet](http://puppetlabs.com/puppet/what-is-puppet)) 到自动执行在 Azure 中设置这些值。 使用以下 PowerShell 脚本[Export-clixml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk)导出到磁盘加密的机密：

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample6.ps1)]

在上述脚本中，Name 是名称的机密密钥，如&quot;FB\_AppSecret&quot;或"twittersecret"。 您可以查看你的浏览器中的脚本创建的".credential"文件。 下面的代码段将测试每个凭据文件，并设置命名的 web 应用的机密：

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample7.ps1)]

> [!WARNING]
> 安全性-不包含密码或其他机密在 PowerShell 脚本中，执行这样的失败操作使用的 PowerShell 脚本以将敏感数据部署的目的。 [Get-credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet 提供了一种安全机制来获取密码。 使用 UI 提示可以防止泄露密码。


### <a name="deploying-db-connection-strings"></a>部署数据库连接字符串

DB 连接字符串为应用设置的相似方式进行处理。 如果部署 web 应用从 Visual Studio 时，将为你配置的连接字符串。 可以在门户中对此进行验证。 设置连接字符串的建议的方法是使用 PowerShell。 有关 PowerShell 脚本的示例创建网站和数据库，并设置连接字符串在网站中，下载[新建 AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)从[Azure 脚本库](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)。

<a id="not"></a>
## <a name="notes-for-php"></a>用于 PHP 的说明

由于两个键 / 值对**应用设置**并**连接字符串**存储在 Azure 应用服务上的环境变量使用任何 web 应用程序框架 （如 PHP) 可以轻松的开发人员检索这些值。 请参阅 Stefan Schackow [Windows Azure 网站： 应用程序字符串和连接字符串的工作](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)博客文章，其中显示了 PHP 代码段以读取应用程序设置和连接字符串。

## <a name="notes-for-on-premises-servers"></a>在本地服务器的说明

如果您要部署到的本地 web 服务器，可帮助通过安全的机密[加密配置文件的配置节](https://msdn.microsoft.com/library/ff647398.aspx)。 或者，可以使用相同的方法，建议为 Azure 网站： 在配置文件中保留开发设置和使用生产设置环境变量值。 在这种情况下，但是，你已将会自动在 Azure 网站中的功能的应用程序代码： 从环境变量中检索设置并使用这些值来替代配置文件设置，或使用配置文件设置时找不到环境变量。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他资源

有关 PowerShell 的示例脚本可创建 web 应用 + 数据库中，设置连接字符串 + 应用程序设置、 下载[新建 AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)从[Azure 脚本库](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)。 

请参阅 Stefan Schackow [Windows Azure 网站： 如何应用程序字符串和连接字符串的工作](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)


特别感谢 Barry Dorrans ( [ @blowdart ](https://twitter.com/blowdart) ) 和 Carlos Farre 对进行了审阅。
