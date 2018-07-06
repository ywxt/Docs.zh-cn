---
uid: web-pages/readme/overview
title: WebMatrix 自述文件 |Microsoft Docs
author: rick-anderson
description: WebMatrix 和 ASP.NET 网页 (Razor) 1.0 版自述文件
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/06/2011
ms.topic: article
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: 924bf04772a1d73c7fdfb1168090daef388438ab
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398795"
---
<a name="webmatrix-readme"></a>WebMatrix 自述文件
====================
2011 年 1 月 13日

## <a name="contents"></a>内容

> [!NOTE]
> 本自述文件适用于 WebMatrix 1.0 版。


- [概述](#Overview)
- [安装](#Installation_Notes)
- [如何发布应用程序](#InstructionsForPublishingApplications)
- [更改和问题](#ChangesAndIssues)

    - [WebMatrix 1.0 安装](#Known_Issues_Installation)
    - [ASP.NET 网页](#Known_Issues_ASPNET)
    - [WebMatrix](#Known_Issues_WebMatrix)
    - [IIS Express](#Known_Issues_IISExpress)
    - [SQL Server Compact](#Known_Issues_SQLServerCompact)
    - [安装应用程序](#Known_Issues_Installing_Applications)
    - [发布应用程序](#Known_Issues_Publishing_Applications)
- [有关详细信息](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>概述

> Microsoft WebMatrix 1.0 是在几分钟内将安装免费的 web 开发堆栈。 它与数据库和编程框架用于创建单一的集成体验集成的 web 服务器。 你可以使用 WebMatrix 简化编码、 测试和发布自己的 ASP.NET 或 PHP 网站的方式或使用 WebMatrix 来启动新的网站使用 DotNetNuke、 Umbraco、 WordPress 或 Joomla 等受欢迎的开源应用。 WebMatrix 使用同一个功能强大的 web 服务器、 数据库引擎和框架环境，将在 internet 上，这使从开发过渡到生产顺畅、 无缝运行你的网站。


<a id="Installation_Notes"></a>

## <a name="installation"></a>安装

> 若要安装 WebMatrix 1.0，必须先安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。 安装 Web 平台安装程序后，可用于安装 WebMatrix。
> 
> 如果在安装过程中遇到问题，请参阅[问题的 Microsoft Web 平台安装程序疑难解答](https://go.microsoft.com/fwlink/?LinkId=196212)。


<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a>如何发布应用程序

> 请参阅[发布应用程序的分步说明](https://go.microsoft.com/fwlink/?LinkID=196149)


<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a>更改和问题

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a>WebMatrix 1.0 安装问题

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a>问题： WebMatrix 1.0 是仅在支持 Microsoft.NET Framework 4 的平台上可用

> .NET Framework 版本 4 是必需的 WebMatrix。 在某些情况下，WebMatrix 1.0 安装程序会让您尝试安装不受支持的配置集的一部分的平台上。 具体而言，Windows Vista SP1 更新不会让您开始安装 WebMatrix，但.NET Framework 4 组件将失败并且阻止您的安装。
> 
> **解决方法**  
> 安装在受支持的平台，其中包括：
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista SP1 或更高版本
> - Windows XP SP3
> - Windows Server 2003 SP2


#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>问题： 无法安装 WebMatrix 1.0，如果没有 Microsoft Visual Studio 2008 SP1 的情况下安装 Microsoft Visual Studio 2008

> **解决方法**  
> 安装[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en)从 Microsoft 下载中心获得。


#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>问题： SQL Server Compact 4.0 某些程序集未安装在 GAC 中

> 在 64 位计算机上安装 SQL Server Compact 4.0 和计算机具有仅.NET Framework 3.5 SP1 客户端安装了配置文件时，SQL Server Compact 4.0 的托管程序集不会放在全局程序集缓存 (GAC) 中。 未安装在 GAC 中的托管程序集是：
> 
> - *System.Data.SqlServerCe.dll* （ADO.NET 提供程序）
> - *System.Data.SqlServerCe.Entity.dll* （ADO.NET 实体框架）
> 
> **解决方法**  
> 卸载 SQL Server Compact 4.0。 下载并安装.NET Framework 3.5 SP1 的完整版本，从以下位置：  
>   
> [Microsoft.NET Framework 3.5 Service pack 1 （完整程序包）](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> 然后重新安装 SQL Server Compact 4.0。


#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>问题： 无法卸载 SQL Server Compact 使用命令行

> 卸载 SQL Server Compact 使用命令行选项不适用于此版本。
> 
> **解决方法**  
> 使用*程序和功能*Windows 控制面板卸载 Microsoft SQL Server Compact 4.0 中。


<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>ASP.NET 网页

文档的本节介绍新功能、 更改和 1.0 版本的 ASP.NET Web Pages 使用 Razor 语法的已知的问题。

- [新增功能](#NewFeatures)
- [更改](#Changes)
- [问题](#Issues)

#### <a id="NewFeatures"></a>  新增功能

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a>配置设置添加禁用包管理器的新增内容：

> 一个新`asp:AdminManagerEnabled`密钥是可用于`<appSettings>`中的元素*web.config*文件，这样就可以完全禁用包管理器。 此元素的默认值为 true，也就是说，如果它不包含在*web.config*是否启用了文件，包管理器。 若要禁用包管理器，将以下元素添加到*web.config*在网站的根目录中的文件：
> 
> [!code-xml[Main](overview/samples/sample1.xml)]


#### <a id="Changes"></a>  更改

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a>重命名为"asp: AdminFolderVirtualPath"的更改:"webPages:AdminFolderVirtualPath"密钥

> `webPages:AdminFolderVirtualPath`可以添加到的密钥*web.config*文件，以指定包管理器的位置已重命名为使用`asp:`命名空间而不是`webPages`命名空间。 如果已使用此元素，必须在配置文件中时将其重命名。


#### <a id="Issues"></a>  已知的问题

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a>问题： 不能再被识别的成员身份用户的密码

> 用于创建和存储成员资格 （登录名） 密码的算法已更改为更安全。 因此，将不识别存储成员 （用户） 的 ASP.NET Razor 的 Beta 版本中创建的密码。 
> 
> **解决方法**站点尚未放到生产环境，如果从成员资格数据库中删除用户记录。 如果数据库是实时功能，以编程方式重新生成成员资格数据库中的现有密码。


#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>问题： 意外的行为时使用自定义用户表的成员身份

> 若要初始化 ASP.NET Razor 网站成员资格提供程序，请调用`WebSecurity.InitializeDatabaseConnection`方法。 (在 WebMatrix 中，入门网站模板包括对在此方法的调用 *\_AppStart.cshtml*文件。)如果`autoCreateTables`此方法的参数设置为 true (默认情况下它设置为 true 入门网站模板中)，并且如果一个无法识别的表名称传递给方法 （第二个参数），该方法不会引发错误。 相反，它会自动创建的表。
> 
> 如果你想要使用自定义用户表的成员身份，但将传递到的错误的表名称，这可能是问题`WebSecurity.InitializeDatabaseConnection`方法。 如果运行该站点的服务器位于代理服务器后面，可能需要配置中的代理信息Web.config以便能够读取来自你的站点之外的信息的文件。 例如，如果您使用帮助器，帮助者与 reCAPTCHA 服务通信，但可能无法通过代理服务器。
> 
> **解决方法**  
> 同样，使用 ASP.NET Web Pages 中，如包管理器，使用源的馈送可能需要代理服务器配置。


#### <a name="issue-error-message-the-admin-module-requires-access-to-appdata"></a>问题： 错误消息"管理员模块需要访问 ~/App\_数据"

> 在某些情况下，尝试创建用户，或以其他方式处理 ASP.NET 成员资格系统可能会导致页后，可以显示错误*管理员模块需要访问 ~/App\_数据*。 发生这种情况是如果 IIS 或 IIS Express 下运行的帐户不具有创建和写入权限*应用程序\_数据*网站根下的文件夹。 
> 
> **解决方法**手动创建*应用程序\_数据*的网站的文件夹。 请确保应用程序 (通常为 NETWORK SERVICE) 下运行的 Windows 帐户具有读/写权限的应用程序的根文件夹和子文件夹，例如应用\_数据。 如果您以前安装的 Beta 1 版本的 ASP.NET Web Pages 使用 Razor 语法，然后再安装 Beta 3 版本，所有适当的程序集安装在 gac 中除[Microsoft.Web.Infrastructure.dll](https://support.microsoft.com/kb/2002980)。


#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>如果使用外部服务或使用包源中的问题，将以下元素放入应用程序的根Web.config文件：

> 有关配置代理服务器的详细信息，请参阅代理元素 （网络设置） MSDN 网站上。
> 
> **问题:"无法加载 Microsoft.Web.Infrastructure.dll"错误 如果您以前安装的 Beta 1 版本的 ASP.NET Web Pages 使用 Razor 语法，然后再安装 Beta 3 版本，所有适当的程序集安装在 gac 中除[Microsoft.Web.Infrastructure.dll](https://support.microsoft.com/kb/2002980)。


#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a>问题： 包含包管理器资源或程序包管理器密码的文件是可用在 IIS 6.0 及更早版本

> 如果部署使用 RC2 版本构建的 ASP.NET Web Pages (Razor) 应用程序和应用程序包含*password.txt*或*packagesources.txt*文件下 */App\_数据/admin*，IIS 6.0 将提供文件如果请求，可能要公开为包管理器实例的密码。 
> 
> **解决方法**重命名*password.txt*或*packagesources.txt*文件为*password.config*或*packagesources.config*.默认情况下，IIS 6.0 不会处理的文件 *.config*扩展。 (在 IIS 7 中中, 没有文件*应用程序\_数据*文件夹提供服务，因此不需要重命名文件。)


#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a>问题： 卸载安装使用 Beta 3 版本的包不会完全删除包组件

> 如果安装了 Beta 3 版本中使用的包管理器的包，然后尝试使用当前版本中卸载它未完全卸载包。 使用程序包管理器**卸载**按钮删除某些组件，但会导致包的库的代码并不会更新*package.config*文件。
> 
> **解决方法**   
> 执行以下步骤：  
> 1. 删除*应用程序\_Data\packages*文件夹。 这将删除所有包。   
> 2. 删除*packages.config*在网站的根目录中的文件。


#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a>问题： 在 Visual Studio 中，调用的基于 web 的程序包管理器使应用程序脱机

> 如果你在 Visual Studio (而不是 WebMatrix) 中工作，并使用*\_管理员*功能，用于启动程序包管理器，Visual Studio 使应用程序脱机，并将发布*应用\_offline.htm*到网站根目录中，这样会中断你能够使用包管理器。
> 
> [!NOTE]
> 尽管使用基于 web 的程序包管理器界面时，通常希望看到此行为，但如果添加、 删除或修改任何文件中的，相同的行为会发生*应用程序\_数据*文件夹。
> 
> **解决方法**   
> 若要使用 Visual Studio 中的包，而不是基于 web 的程序包管理器使用的 NuGet 扩展。 有关信息，请参阅[NuGet 文档](https://docs.microsoft.com/nuget/)。 如果你正在使用中的其他文件*应用程序\_数据*文件夹，请考虑使文件保持在其他位置来避免此问题。 如果不可行，请删除*应用程序\_offline.htm*手动文件，或者等待，直到站点自动 （默认情况下，在 30 秒后） 重新联机。


#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>如果卸载.NET Framework 版本 4，然后重新安装它，则禁用使用 Razor 语法的 ASP.NET Web Pages。

> 与页.cshtml扩展不能正确运行。
> 
> **ASP.NET 网页机根目录中注册程序集**Web.config**文件，并删除.NET Framework 中删除该文件。


#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>如果你可以控制在服务器计算机，在服务器计算机上安装的更新中所述更新可启用某些 IIS 7.0 或 IIS 7.5 处理程序来处理请求的 Url 不以句点结尾。

> 如果运行该站点的服务器位于代理服务器后面，可能需要配置中的代理信息*web.config*以便能够读取来自你的站点之外的信息的文件。 例如，如果您使用`ReCaptcha`帮助器，帮助者与 reCAPTCHA 服务通信，但可能无法通过代理服务器。 同样，使用 ASP.NET Web Pages 中，如包管理器，使用源的馈送可能需要代理服务器配置。
> 
> 如果使用外部服务或使用包源中的问题，将以下元素放入应用程序的根*web.config*文件：
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> 有关配置代理服务器的详细信息，请参阅[&lt;代理&gt;元素 （网络设置）](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN 网站上。


#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>问题： 卸载.NET Framework 版本 4 禁用使用 Razor 语法的 ASP.NET Web Pages

> 如果卸载.NET Framework 版本 4，然后重新安装它，则禁用使用 Razor 语法的 ASP.NET Web Pages。 与页 *.cshtml*扩展不能正确运行。 ASP.NET 网页机根目录中注册程序集*web.config*文件，并删除.NET Framework 中删除该文件。 重新安装.NET Framework 安装的配置文件的新版本，但不会将引用添加 ASP.NET Web Pages 的程序集。
> 
> **解决方法**后重新安装.NET Framework，请重新安装 ASP.NET Web Pages 使用 Razor 语法。 这将添加到下面的元素*web.config*机根目录，这通常是在以下位置中的文件：  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]


#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>问题： 无扩展名的 Url 不到在 IIS 7 或 IIS 7.5 上的.cshtml/.vbhtml 文件

> 在 IIS 7 或 IIS 7.5 上，使用类似于以下 URL 的请求不能将查找具有的页 *.cshtml*或 *.vbhtml*扩展：  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> 由于 URL 重写未启用默认情况下为 IIS 7 或 IIS 7.5，则会产生问题。 很可能方案是使用本地 IIS Express，测试时未看到该问题，但在你的网站部署到托管网站时遇到。
> 
> **解决方法**
> 
> - 如果你可以控制在服务器计算机，在服务器计算机上安装的更新中所述[更新可启用某些 IIS 7.0 或 IIS 7.5 处理程序来处理请求的 Url 不以句点结尾](https://support.microsoft.com/kb/980368)。
> - 如果您没有对服务器计算机的控制 （例如，要部署到托管的网站），将以下代码添加到该网站*web.config*文件： 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]


#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>问题： 应用程序部署到不具有 SQL Server Compact 安装的计算机

> SQL Server Compact 未安装在计算机上可以运行包含 SQL Server Compact 数据库的应用程序。 Microsoft WebMatrix 1.0 中自动将这些二进制文件复制，并执行适当*web.config*文件转换。
> 
> **解决方法**如果你需要将这些文件复制并使*web.config*文件更改手动，执行以下操作：
> 
> 1. 将复制到的数据库引擎程序集*Bin*目标计算机上的应用程序文件夹 （和子文件夹）：  
> 
>    - 复制*C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*   
>        **to** *\Bin*
>    - 复制<em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\</em><strong><em>到</em></strong>\Bin\x86*
>    - 复制<em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\</em>* <strong>到</strong><em>\Bin\amd64</em>
> 
> 2. 在该网站的根文件夹中创建或打开*web.config*文件。 (此文件类型是在 WebMatrix 1.0 中，单击**所有**中**选择文件类型**对话框。)
> 3. 将以下元素添加为的子`<configuration>`元素 (而不是在`<system.web>`元素):
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]


#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>问题:"数据库"和"WebGrid"帮助程序不能不能在 Visual Basic 中的中等信任

> 如果使用的 Visual Basic (创建 *.vbhtml*文件)，则`Database`和`WebGrid`如果应用程序设置为使用中等信任级别，帮助程序将无法工作。
> 
> **解决方法**  
> 如果使用 Visual Studio 2010，您可以通过安装 Service Pack 1 版本来解决此问题。 可用的 SP1 版本的最终版本之前，您可以下载从 SP1 的 Beta 版[Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) Microsoft 下载中心页。   
>   
> 如果这不可行，或如果不使用 Visual Studio 2010，则可以暂时设置要使用完全信任的应用程序。


#### <a name="issue-applicationpart-resources-are-externally-accessible"></a>问题:"ApplicationPart"资源是从外部访问

> 如果程序集包含派生的对象`ApplicationPart`类，程序集的资源公开的`ResourceRouteHandler`类。 以下列 URL 为例：  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> 此请求下载中的资源字符串的所有*System.Web.WebPages.Administration.dll*程序集。 下载的所有嵌入资源 （甚至不应为静态内容提供的那些）。 如果嵌入的资源包含敏感信息，这可以表示存在安全风险。 
> 
> **解决方法**   
> 如果您创建**ApplicationPart**对象，请确保与相关联的嵌入的资源**ApplicationPart**对象的程序集不包含敏感信息。


<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a>WebMatrix

> [!NOTE]
> WebMatrix 安装问题的信息，请参阅[WebMatrix 安装问题](#Known_Issues_Installation)本文档前面。


文档本部分介绍 WebMatrix 开发环境的已知的问题。

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a>问题： 用户名或密码的 web.config 文件中的数据库连接字符串中的更改不会反映在数据库工作区

> **解决方法**  
> 
> 1. 在中*web.config*文件中，将连接字符串中的数据库名称 （例如，向其添加"1"）。
> 2. 保存*web.config*文件。
> 3. 单击**数据库**和刷新。
> 4. 更改连接字符串中的数据库名称*web.config*文件返回到原始数据库名称。
> 5. 保存*web.config*文件。
> 6. 单击**数据库**和刷新。


#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a>问题： 无法删除由 WebMatrix 所创建文件夹

> 如果使用提升的权限运行 WebMatrix (也就是说，您如何使用 WebMatrix**以管理员身份运行**Windows 中的选项)，不能使用 Windows 资源管理器删除创建的 WebMatrix 的文件夹。
> 
> **解决方法**  
> 运行 Windows 资源管理器使用提升的权限。 请执行这些步骤：  
> 
> 1. 在 Windows 中，单击**启动**。
> 2. 输入"Windows 资源管理器"，然后右键单击的项**Windows 资源管理器**。
> 3. 单击**以管理员身份运行**。 然后，可以删除的文件夹。


#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a>问题： WebMatrix 1.0 是无法执行某些任务需要提升

> WebMatrix 1.0 是无法执行某些任务需要提升，例如，在以下情况下安装其他组件：
> 
> - 在 Windows Vista 或 Windows 7 中，使用不具有管理权限的帐户登录并禁用用户帐户控制 (UAC)。
> - 使用 Microsoft Windows XP 或 Microsoft Windows Server 2003。
> 
> **解决方法**  
> 在 WebMatrix 1.0 中的大多数任务不需要管理权限。 对于那些确实可以执行的操作以管理员身份，或请执行以下步骤：
> 
> - 在 Windows Vista 或 Windows 7，启用 UAC。
> - 在 Windows XP 中，将用户添加到管理员安全组。


#### <a name="issue-site-from-web-gallery-is-disabled"></a>问题:"从 Web 库的站点"已禁用

> **站点从 Web 库**如果未安装 Web 平台安装程序 3.0 选项被禁用。
> 
> **解决方法**  
> 安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。


#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>问题： Google Chrome 不能作为运行选项

> 在浏览器的列表中不显示 Google Chrome**运行**上**主页**选项卡。
> 
> **解决方法**  
> 某些版本的 Google Chrome 并不能注册正确地与 Windows 中的默认程序功能。 解决此问题，启动 Google Chrome 中，单击*自定义和控制 Google Chrome*菜单上，单击*选项*，然后单击*使 Google Chrome 我的默认浏览器*。


#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>问题:"外键"对话框中不允许输入主键

> **外键**对话框不允许您输入从主键表的主键名称。
> 
> **解决方法**  
> 这是有意为之。 不需要输入主键表的主键的名称。


#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a>问题： IntelliSense 不能在 WebMatrix 中的 Razor 语法、 C# 或 Visual Basic

> 在 WebMatrix 中的 HTML 和 CSS 支持 IntelliSense。 但是，不用于其他语言。 
> 
> **解决方法**   
> 无。


#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a>问题： 适用于 HTML 和 CSS IntelliSense 建议不是上下文相关的元素

> 在 WebMatrix 中的标记的 IntelliSense 支持使用 HTML [XHTML 1.0 Transitional 架构](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional)并使用 CSS [CSS 2.1 架构](http://www.w3.org/TR/CSS2/)。 IntelliSense 根据这些特定的架构，因为某些标记、 属性可能不适合当前页或样式定义的建议。 为 HTML，它可能还会导致意外建议可能会被解释为格式不正确 （例如，当未关闭标记） 的 XHTML 内容中。 此问题可能是更明显，如果插入点位于不完整的标记;在这种情况下，IntelliSense 可能建议新开始标记或提供其他不正确的建议。 
> 
> **解决方法**   
> 对于 HTML，请确保在格式正确的、 完整的 HTML 页。 对于 CSS，没有任何解决方法。


#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a>问题： 您键入的同时意味着没有调用 IntelliSense

> 有时，IntelliSense 可能不会调用为 HTML 或 CSS 正在输入后在编辑器中。 具体而言，这可能会发生时插入点，则直接旁边的另一个元素或在文件末尾。 
> 
> **解决方法**   
> 请确保没有插入点周围的空格并且插入点不是在文件末尾。 此外可以通过按 Ctrl + 空格键手动调用 IntelliSense。


#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a>问题： 没有用户界面是可用于禁用 IntelliSense

> WebMatrix 1.0 允许任何用户界面或手势禁用 IntelliSense。 
> 
> **解决方法**   
> 启动 WebMatrix 使用以下命令，其中包括禁用 IntelliSense 的交换机：  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`


<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a>IIS Express

IIS Express 具有其自己的自述文件，可在以下 URL:

[https://go.microsoft.com/fwlink/?LinkID=207675&ampclcid = 0x409](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a>SQL Server Compact

SQL Server Compact 具有其自己的自述文件，可在以下 URL:

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

有关涉及 WebMatrix 的组成部分，以安装 SQL Server Compact 的问题的信息，请参阅[WebMatrix 安装问题](#Known_Issues_Installation)本文档前面。

### <a id="Known_Issues_Installing_Applications"></a>  安装应用程序

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>问题： 安装应用程序可能需要长时间如果用户的 My Documents 文件夹重定向到网络共享

> **解决方法**  
> 无。 应用程序可能需要一段时间才能安装，但将正确安装。


### <a id="Known_Issues_Publishing_Applications"></a>  发布应用程序

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a>发布 SQL Compact 数据库时的问题:"要求不能获取权限"的错误

> WebMatrix 不完全支持为 SQL Server Compact 的支持的二进制文件部署到正在运行.NET Framework 版本 3.5 使用中等信任配置的服务器。
> 
> **解决方法**  
> 首选的解决方法是在服务器上安装.NET Framework 4。 或者，请执行以下操作：
> 
> 1. 添加到以下元素`SecurityClasses`主题中*Web\_MediumTrust.config*文件：
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. 创建一个新权限集*Web\_MediumTrust.config*文件所需的以下权限：
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. 应用将权限设置为 SQL Server Compact 通过将以下元素放入*Web\_MediumTrust.config*文件：
> 
>     [!code-html[Main](overview/samples/sample8.html)]


#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a>问题： 库和 PhpBB web 应用程序发布后显示"服务不可用"错误

> 在某些情况下，发布应用程序会导致"服务不可用"错误。
> 
> **解决方法**  
> 在 WebMatrix 中，添加一个反斜杠 (\)到中的服务器名称的末尾**发布设置**窗口，然后将发布一次应用程序。


#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a>问题： Moodle 网站布局和链接已断开发布后

> 发布的 Moodle 应用程序后，应用程序不会无法正常工作。
> 
> **解决方法**  
> 在 WebMatrix 中，将反斜杠 （/） 添加到末尾**站点名称**字段中**发布设置**窗口，然后将发布一次应用程序。


#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a>问题： 发布 nopCommerce 失败，出现数据库错误

> 发布 nopCommerce 失败并报告数据库错误，如"插入 nop\_日志表失败。"
> 
> **解决方法**  
> 
> 1. 在 WebMatrix 中，单击**运行**以启动本地 nopCommerce。
> 2. 登录到管理页。
> 3. 单击**系统**菜单。
> 4. 单击**日志**选项。
> 5. 单击**清除日志**按钮。
> 6. 重新发布 nopCommerce。


#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a>问题： 下载已发布的站点时 Silverstripe CMS 显示"HTTP 500 PHP FCGI 错误"

> **解决方法**  
> 单击后**下载已发布的站点**，跳过`silverstripe-cache/manifest_main`中**发布预览**。 此文件用于缓存和特定于每台计算机。


#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a>问题： Subtext 显示"服务器错误 '/' 应用程序中"时下载已发布的站点

> **解决方法**  
> 打开站点的*web.config*文件，并替换 SQL Server 管理员凭据 （"sa"凭据） 的用户 ID 和数据库连接字符串中的密码。
> 
> 或者，请执行以下步骤，以便您登录时所用的用户帐户中为提供`db_owner`权限：
> 
> 1. 安装 SQL Server Management Studio 中使用 Web 平台安装程序。
> 2. 连接到本地 SQL Server Express 实例 (默认情况下， `.\SQLEXPRESS`)。
> 3. 单击**数据库** &gt; *[localSubtextDatabase]* &gt; **安全** &gt; **用户**&gt; *[localSubtextUser*] (默认值是`subtextuser`]，右键单击，然后单击**属性**。
> 4. 选择**db\_所有者**角色成员身份部分中。


#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>问题： 站点可能无法在发布如果将"目标 URL"字段不 http:// 或 https:// 开头的前缀后

> 在中**发布设置**对话框中，如果目标 URL 不以开头`http://`或`https://`，部署后，该站点可能无法工作。
> 
> **解决方法**  
> 请确保在发布的站点中的目标 URL 前**发布设置**对话框的开头`http://`或`https://`。


#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>问题： 发布的 MySQL 数据库失败，出现错误"无法将数据库发布。 这可以是远程数据库不能运行脚本。"

> 多种原因可能出现此错误。 可以看到此错误的原因之一是，如果数据库脚本中包含单引号字符 （'），并且目标 MySQL 数据库的默认字符集为 utf-8。
> 
> **解决方法**  
> 设置为远程的 MySQL 数据库设置为 utf-8 的默认字符。


#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a>问题： 某些链接后不可见 DotNetNuke 中发布或从其下载站点

> 如果您发布或下载的 DotNetNuke 站点，您可能需要清除缓存，以获取新的链接可显示在网站上。
> 
> **解决方法**
> 
> 1. 以"Host"身份登录。
> 2. 转到主机菜单并选择**主机设置**。
> 3. 向下的滚动并下**高级设置**，展开**性能设置**。
> 4. 单击**清除缓存**页的链接。
> 5. 转到页面底部并重新启动该应用程序。


#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a>问题： 某些中的链接 AtomSite 是中断后下载已发布的站点

> **解决方法**  
> 在*service.config*文件中， *users.config*文件，以及所有 *.xml*文件，将为 URL 字符串 (例如， `http://myhost.com/atomsite`) 与本地 (例如， `http://localhost:1239`).


#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a>问题： WordPress 等基于 MySQL 的应用程序无法将发布和报告数据库错误

> 默认情况下，WebMatrix 使用 utf-8 字符集安装 MySQL。 如果在你自己，计算机上安装 MySQL 和设置的字符不是 utf-8 （例如，它是 Latin1），发布过程的数据库可能会失败。
> 
> **解决方法**
> 
> 1. 更改 MySQL 为 utf-8 字符集。 (有关详细信息，请参阅[服务器字符集和排序规则](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html)MySQL 网站上。)
> 2. 重新安装该应用程序。
> 3. 重新发布应用程序。


#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a>问题:"下载发布的站点"失败的应用程序的基于浏览器的设置

> 某些应用程序 (例如，订购 Kentico CMS) 要求你在浏览器中启动它们才能执行安装后设置，如创建数据库。 如果发布这样的应用程序，而无需完成基于浏览器的设置，请尝试从远程服务器下载同一站点将失败。
> 
> **解决方法**  
> 将站点发布之前完成基于浏览器的设置。


#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a>问题:"下载发布的站点"失败，出现数据库错误 DotNetNuke 和 Kooboo CMS

> 如果你尝试从服务器下载应用程序和数据库连接字符串中具有管理员凭据**发布设置**对话框中，可能会看到发布日志中的以下错误：
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> **解决方法**  
> 如果可行，重新发布该网站 （或将其发布） 的数据库使用非管理员凭据。


<a id="More_Info"></a>

## <a name="for-more-information"></a>更多信息

有关 WebMatrix 1.0 的详细信息，请参阅以下网站：

- [IIS.net](http://iis.net/)
- [ASP.NET 2.0](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

© 2011 Microsoft Corporation. 保留所有权利。 [使用条款](https://msdn.microsoft.cos/cc300389.aspx)。
