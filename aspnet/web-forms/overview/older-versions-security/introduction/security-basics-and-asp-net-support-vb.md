---
uid: web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-vb
title: 安全基础知识和 ASP.NET 支持 (VB) |Microsoft Docs
author: rick-anderson
description: 这是一系列教程，其中会介绍技术进行身份验证通过 web 窗体的访问者授权访问简介中的第一个教程...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/13/2008
ms.topic: article
ms.assetid: ab68a92b-fc81-40a4-a7dc-406625d2c5d4
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-vb
msc.type: authoredcontent
ms.openlocfilehash: 2213f2ac323e59fa67e51d6c9dcc8c2efdd2619e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398506"
---
<a name="security-basics-and-aspnet-support-vb"></a>安全基础知识和 ASP.NET 支持 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial01_Basics_vb.pdf)

> 这是一系列教程，其中会介绍用于通过 web 窗体的访问者进行身份验证、 授予对特定页面和功能，访问权限和管理 ASP.NET 应用程序中的用户帐户的技术中的第一个教程。


## <a name="introduction"></a>介绍

什么是一件事论坛、 电子商务网站、 在线电子邮件网站、 门户网站和所有具有共同的社交网络站点？ 它们都提供*用户帐户*。 提供用户帐户的站点必须提供多个服务。 新的访问者能够创建帐户所需的最低，且返回访问者必须能够以用户身份登录。 此类 web 应用程序可以做出决策基于已登录的用户： 某些页面或操作可能被限制为只记录在用户或特定的子集用户;其他页可能会向登录的用户特定信息，或可能显示更多或更少信息，具体取决于哪些用户查看页面。

这是一系列教程，其中会介绍用于通过 web 窗体的访问者进行身份验证、 授予对特定页面和功能，访问权限和管理 ASP.NET 应用程序中的用户帐户的技术中的第一个教程。 在过去的这些教程中我们将说明如何：

- 标识和用户登录到网站
- 使用 ASP。NET 的成员资格框架来管理用户帐户
- 创建、 更新和删除用户帐户
- 限制对网页、 目录或基于登录用户的特定功能的访问
- 使用 ASP。若要将用户帐户与角色相关联的 NET 的角色框架
- 管理用户角色
- 限制对网页、 目录或特定功能，根据登录的用户的角色的访问
- 自定义和扩展 ASP。NET 的安全 Web 控件

这些教程旨在是简洁并提供引导你完成该过程以可视方式很大的屏幕截图的分步说明。 每个教程是在 C# 和 Visual Basic 版本中可用，包括使用的完整代码下载。 （第一个教程重点介绍从高层次的角度来看的安全概念和因此不包含任何关联的代码。）

在本教程中我们将讨论重要的安全概念和哪些功能是 ASP.NET 帮助实现窗体身份验证、 授权、 用户帐户和角色提供。 让我们进入正题！

> [!NOTE]
> 安全是跨物理、 技术，任何应用程序的一个重要方面和策略决策和需要高度的规划和领域知识。 本系列教程不用于开发安全的 web 应用程序应作为指南。 相反，它重点介绍专门窗体身份验证、 授权、 用户帐户和角色。 本系列教程将介绍解决这些问题绕转某些安全概念，而其他人会保留未探索。


## <a name="authentication-authorization-user-accounts-and-roles"></a>身份验证、 授权、 用户帐户和角色

身份验证、 授权、 用户帐户和角色是四个术语，将使用经常在整个教程系列中，因此我想要快速花定义 web 安全的上下文中的这些术语。 在客户端-服务器模型，如 Internet，有很多情况下需要用来标识发出请求的客户端服务器。 *身份验证*是认定客户端的标识的过程。 客户端已成功识别说可*进行身份验证*。 无法识别客户端则称*未经身份验证*或*匿名*。

安全的身份验证系统涉及在至少一个以下三个方面：[你知道的东西，你拥有的东西，或你](http://www.cs.cornell.edu/Courses/cs513/2005fa/NNLauthPeople.html)。 大多数 web 应用程序依靠的是一些客户端知道，如密码或 PIN。 用来标识用户的用户名和密码，例如-的信息被称为*凭据*。 本系列教程侧重*窗体身份验证*，这是其中的用户登录到站点通过提供其凭据以网页形式的身份验证模型。 我们有所有遇到这种身份验证之前。 请转到任何电子商务网站。 你现可查看系统会要求通过文本框在网页上输入用户名和密码进行登录。

除了标识客户端，可能需要限制哪些资源或功能可以根据发出请求的客户端访问服务器。 *授权*是确定特定用户是否有权访问特定资源或功能的过程。

一个*用户帐户*是有关某个特定用户保存信息的存储。 用户帐户必须至少包括唯一标识用户，如用户的登录名和密码的信息。 此基本信息，以及用户帐户可能包括诸如： 用户的电子邮件地址;日期和时间创建帐户;日期和时间及其持续记录第一个和最后一个名称;电话号码;和邮寄地址。 当使用窗体身份验证，用户帐户信息通常存储在 Microsoft SQL Server 等关系数据库。

支持用户帐户的 web 应用程序 （可选） 可以分组到用户*角色*。 角色是仅应用于用户，并提供用于定义授权规则和页面级别的功能的抽象的标签。 例如，网站可能包括使用禁止管理员才能访问一组特定的 web 页面以外的任何人的授权规则的管理员角色。 此外，多个 （包括非管理员） 的所有用户都都可以访问的页面可能显示额外的数据或提供额外的功能中的管理员角色的用户访问时。 使用角色，我们可以在角色的角色为基础，而不是由用户定义这些授权规则。

## <a name="authenticating-users-in-an-aspnet-application"></a>在 ASP.NET 应用程序中的用户进行身份验证

当用户输入到其浏览器地址窗口或单击的链接的 URL 时，该浏览器建立[超文本传输协议 (HTTP)](http://en.wikipedia.org/wiki/HTTP)请求到指定的内容的 web 服务器，它是 ASP.NET 页上，一个映像，JavaScript文件或任何其他类型的内容。 返回请求的内容，任务是 web 服务器。 在执行此操作，它必须确定执行大量请求，包括谁做了请求和是否标识有权检索请求的内容有关的操作。

默认情况下，浏览器发送的 HTTP 请求的缺乏任何类型的标识信息。 但是，如果浏览器包括身份验证信息的 web 服务器开始身份验证工作流，它会尝试标识客户端发出请求。 身份验证工作流的步骤取决于 web 应用程序正在使用的身份验证的类型。 ASP.NET 支持三种类型的身份验证： Windows、 Passport 和窗体。 本系列教程侧重于窗体身份验证，但让我们花点时间进行比较和对比 Windows 身份验证用户的存储和工作流。

### <a name="authentication-via-windows-authentication"></a>通过 Windows 身份验证的身份验证

Windows 身份验证工作流使用以下身份验证方法之一：

- 基本身份验证
- 摘要式身份验证
- Windows 集成身份验证

所有这三种技术的工作方式大致相同： 时未经授权匿名请求到达时，web 服务器会返回 HTTP 响应，指示该授权才能继续。 在浏览器然后显示一个模式对话框，提示用户输入其用户名和密码 （请参见图 1）。 然后，此信息将发送回 web 服务器通过 HTTP 标头。


![模式对话框提示用户提供其凭据](security-basics-and-asp-net-support-vb/_static/image1.png)

**图 1**： 模式对话框提示用户提供其凭据


提供的凭据是根据 web 服务器的 Windows 用户存储验证。 这意味着，在 web 应用程序中每个经过身份验证的用户的 Windows 帐户必须在组织中。 这是在 intranet 方案中的日益普及。 事实上，当 intranet 设置中使用 Windows 集成身份验证，在浏览器自动为 web 服务器提供用于登录到网络，从而取消显示在图 1 中所示的对话框上的凭据。 适用于 intranet 应用程序 Windows 身份验证时，它通常不可行的 Internet 应用程序是因为您不想要创建您的站点上注册的每个用户的 Windows 帐户。

### <a name="authentication-via-forms-authentication"></a>通过窗体身份验证的身份验证

窗体身份验证，但是，非常适合于 Internet 的 web 应用程序。 回想一下，窗体身份验证标识的用户的提示他们输入其凭据通过 web 窗体。 因此，当用户尝试访问未经授权的资源，它们会自动重定向到可在其中输入其凭据的登录页。 针对自定义用户存储区-通常为数据库然后验证已提交的凭据。

验证已提交的凭据后,*窗体身份验证票证*为用户创建。 此票证指出用户已经过身份验证，并包括标识信息，如用户名。 窗体身份验证票证 （通常情况下） 存储为客户端计算机上的 cookie。 因此，以后访问该网站包含窗体身份验证票证在 HTTP 请求中，从而使 web 应用程序具有登录后将用户标识。

图 2 说明了窗体身份验证工作流的高级的出发点。 请注意如何在 ASP.NET 中的身份验证和授权部分充当两个单独的实体。 窗体身份验证系统标识用户 （或报告它们是匿名）。 授权系统是什么确定用户是否有权访问所请求的资源。 如果 （因为它们位于图 2 时尝试以匿名方式访问 ProtectedPage.aspx） 未授权用户，授权系统将报告用户已被拒绝，这将导致窗体身份验证系统会自动将用户重定向到登录页。

用户已成功登录后，后续 HTTP 请求包括窗体身份验证票证。 窗体身份验证系统只是标识用户-它是确定用户是否可以访问所请求的资源的授权系统。


![窗体身份验证工作流](security-basics-and-asp-net-support-vb/_static/image2.png)

**图 2**： 窗体身份验证工作流


我们将深入探讨在接下来两个教程中，窗体变得更详细的身份验证[概述的窗体身份验证](an-overview-of-forms-authentication-vb.md)并[窗体身份验证配置和高级主题](forms-authentication-configuration-and-advanced-topics-vb.md)。 ASP 的详细信息。NET 的身份验证选项，请参阅[ASP.NET 身份验证](https://msdn.microsoft.com/library/eeyk640h.aspx)。

## <a name="limiting-access-to-web-pages-directories-and-page-functionality"></a>限制对网页、 目录和页的功能的访问

ASP.NET 包括两种方法来确定特定用户是否有权访问特定文件或目录：

- **文件授权**-由于 ASP.NET 页和 web 服务实施为可通过访问控制列表 (Acl) 指定驻留在 web 服务器的文件系统上，访问这些文件的文件。 使用 Windows 身份验证最常使用文件授权，因为使用 Acl 是适用于 Windows 帐户的权限。 时使用的窗体身份验证，所有操作系统和文件系统级别请求都执行通过相同的 Windows 帐户，而不考虑用户访问网站。
- **URL 授权**-使用 URL 授权时，页面开发人员所指定的 Web.config 中的授权规则。这些授权规则指定哪些用户或角色允许访问还是被拒绝访问特定页面或应用程序中的目录。

文件授权和 URL 授权特定目录中定义用于访问特定的 ASP.NET 页面或所有 ASP.NET 页面的授权规则。 使用这些技术，我们可以指示 ASP.NET 可以拒绝对特定用户的特定页的请求或允许访问一组用户，拒绝其他所有人的访问。 在所有用户都可以访问页上，但页面的功能取决于用户方案呢？ 例如，支持用户帐户的许多站点具有显示不同的内容或与匿名用户身份验证的用户的数据的页。 匿名用户可能会看到用于登录到站点的链接，而身份验证的用户将看到的消息，欢迎回来，如*用户名*以及将其注销的链接。另一个示例： 查看拍卖站点处的项时，请参阅具体取决于你是 bidder 还是 auctioning 项的一个不同的信息。

以声明方式或以编程方式，可以实现此类页面级别调整。 若要显示不同的内容为匿名身份验证的用户，只需将比[LoginView 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx)拖动到页面并其 AnonymousTemplate 和 LoggedInTemplate 模板中输入合适的内容。 或者，您可以以编程方式确定是否当前的请求进行身份验证、 用户是，谁以及哪些角色所属 （如果有）。 可以使用此信息以然后显示或隐藏网格或面板中的页上的列。

本系列包括三个专注于授权的教程。 ***基于用户的授权***探讨如何限制到一个页面或页面的目录中的特定用户帐户; 的访问***基于角色授权***探讨级别; 最后，提供在角色的授权规则***显示内容根据当前记录中的用户***教程将探讨如何修改特定页面的内容和功能根据用户访问的页面。 ASP 的详细信息。NET 的授权选项，请参阅[ASP.NET 授权](https://msdn.microsoft.com/library/wce3kxhd.aspx)。

## <a name="user-accounts-and-roles"></a>用户帐户和角色

ASP。NET 的窗体身份验证提供的基础结构，用户能够登录到站点，并将跨页面访问记住它们已经过身份验证的状态。 和 URL 授权提供了一个框架，用于限制对特定文件或文件夹中的 ASP.NET 应用程序的访问。 任一功能，但是，提供了一种方法用于存储用户帐户信息或管理角色。

ASP.NET 2.0 中，开发人员之前负责创建其自己的用户和角色存储。 它们也是在设计用户界面并将类似的登录页和页后，可以创建新帐户，以及其他与帐户相关的页写基本用户的代码挂钩。 而无需在 ASP.NET 中，每个开发人员实现的用户帐户有问题，例如，在他自己的设计决策到达任何内置用户帐户框架如何存储密码或其他敏感信息？和哪些指导原则应该我会施加有关密码长度和强度？

现在，在 ASP.NET 应用程序中实现的用户帐户是要简单得归功于*成员资格框架*和内置登录 Web 控件。 成员资格框架是中的类的少量[System.Web.Security 命名空间](https://msdn.microsoft.com/library/system.web.security.aspx)用于执行基本的用户帐户相关的任务提供功能。 成员资格框架中的关键类是[成员资格类](https://msdn.microsoft.com/library/system.web.security.membership.aspx)，其中包含类似的方法：

- CreateUser
- DeleteUser
- GetAllUsers
- GetUser
- UpdateUser
- 验证用户

使用成员资格框架[提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)，这清楚地划分成员资格框架 API 从它的实现。 这使开发人员能够使用公共 API，但使他们能够使用满足其应用程序的自定义需求的实现。 简单地说，成员资格类定义的基本功能的框架 （方法、 属性和事件），但不会实际提供任何实现细节。 相反，成员资格类的方法调用执行实际工作的配置提供程序。 例如，调用成员资格类的 CreateUser 方法时，成员资格类并不知道用户存储的详细信息。 它不知道是否用户需要维护的数据库中或 XML 文件或某些其他存储。 成员资格类将检查 web 应用程序的配置，以确定要委托的调用，哪些提供程序，该提供程序类负责在适当的用户存储区中实际创建新的用户帐户。 图 3 说明了这种交互。

Microsoft.NET Framework 中提供两个成员资格提供程序类：

- [ActiveDirectoryMembershipProvider](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) -在 Active Directory 和 Active Directory 应用程序模式 (ADAM) 服务器中实现成员资格 API。
- [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) -SQL Server 数据库中实现成员资格 API。

本系列教程重点介绍专门 SqlMembershipProvider。


[![提供程序模型使不同的实现是无缝地插入到框架](security-basics-and-asp-net-support-vb/_static/image4.png)](security-basics-and-asp-net-support-vb/_static/image3.png)

**图 03**: 提供程序模型使不同的实现是无缝地插入到框架 ([单击以查看实际尺寸的图像](security-basics-and-asp-net-support-vb/_static/image5.png))


提供程序模型的好处是可以由 Microsoft、 第三方供应商或单独的开发人员开发并无缝地插入到成员资格框架替代实现。 例如，Microsoft 已发布[针对 Microsoft Access 数据库的成员资格提供程序](https://download.microsoft.com/download/5/5/b/55bc291f-4316-4fd7-9269-dbf9edbaada8/sampleaccessproviders.vsi)。 有关成员资格提供程序的详细信息，请参阅[提供程序工具包](https://msdn.microsoft.com/asp.net/aa336558.aspx)，其中包括的成员资格提供程序、 示例自定义提供程序、 100 多个页上提供程序模型中，文档的演练和针对内置成员资格提供程序 （即，ActiveDirectoryMembershipProvider 和 SqlMembershipProvider） 完成的源代码。

ASP.NET 2.0 还引入了角色框架。 成员资格框架，如角色框架构建提供程序模型之上。 通过公开其 API[角色类](https://msdn.microsoft.com/library/system.web.security.roles.aspx)和.NET Framework 附带有三个提供程序类：

- [AuthorizationStoreRoleProvider](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx) -管理授权管理器策略存储区，如 Active Directory 或 ADAM 中的角色信息。
- [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) -SQL Server 数据库中实现角色。
- [WindowsTokenRoleProvider](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx) -将角色信息的访问者的 Windows 组相关联。 此方法通常与 Windows 身份验证一起使用。

本系列教程重点介绍专门 SqlRoleProvider。

由于提供程序模型包括单个前置 API （成员资格和角色类），则可以生成围绕该 API 的功能而无需担心如何实现详细信息-这些步骤将由选定的页的提供程序开发人员。 此统一的 API 允许 Microsoft 和第三方供应商构建 Web 控件的成员身份和角色框架与连接的。 ASP.NET 附带的许多[登录 Web 控件](https://msdn.microsoft.com/library/ms178329.aspx)实现常用用户帐户的用户界面。 例如， [Login 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)提示用户输入其凭据验证，并将然后将其在记录通过窗体身份验证。 [LoginView 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx)提供了用于显示不同的标记，向匿名用户与身份验证的用户或根据用户的角色的不同标记的模板。 并[CreateUserWizard 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.aspx)渐进式用户界面提供用于创建新的用户帐户。

幕后的各种登录控件与成员资格和角色框架进行交互。 大多数登录控件可以实现无需编写一行代码。 我们将在将来的教程，其中包括扩展和自定义它们的功能的技术说明中更详细地介绍这些控件。

## <a name="summary"></a>总结

支持用户帐户的所有 web 应用程序都需要类似的功能，例如： 用户登录并在状态页的访问; 跨记住其日志的能力某一网页寻求新的访问者来创建帐户;并向页面开发人员能够指定哪些资源、 数据和功能可向哪些用户或角色。 进行身份验证和授权用户和管理用户帐户和角色的任务是非常容易实现，得益于窗体身份验证、 URL 授权和成员身份和角色框架的 ASP.NET 应用程序中。

在过去的下一步的多个教程我们将通过构建使用 web 应用程序的基础知识，以分步方式检查这些方面。 接下来的两本教程中我们将探讨在详细信息窗体身份验证。 我们将看到窗体身份验证工作流在操作中，剖析窗体身份验证票证，讨论的安全问题，并请参阅如何配置窗体身份验证系统-所有生成的 web 应用程序时允许访问者来登录和注销。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 2.0 成员身份、 角色、 窗体身份验证和安全资源](https://weblogs.asp.net/scottgu/ASP.NET-2.0-Membership_2C00_-Roles_2C00_-Forms-Authentication_2C00_-and-Security-Resources-)
- [ASP.NET 2.0 安全指导原则](https://msdn.microsoft.com/library/ms998258.aspx)
- [ASP.NET 身份验证](https://msdn.microsoft.com/library/eeyk640h.aspx)
- [ASP.NET 授权](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [ASP.NET 登录控件概述](https://msdn.microsoft.com/library/ms178329.aspx)
- [检查 ASP.NET 2.0 的成员资格、 角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [实现： 如何保护我的网站使用成员资格和角色？](https://asp.net/learn/videos/video-45.aspx) （视频）
- [成员资格简介](https://msdn.microsoft.com/library/yh26yfzy.aspx)
- [MSDN 安全性开发中心](https://msdn.microsoft.com/security/default.aspx)
- [专业 ASP.NET 2.0 安全、 成员资格和角色管理](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html)(ISBN: 978-0-7645-9698-8)
- [提供程序工具包](https://msdn.microsoft.com/asp.net/aa336558.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是许多有用的审阅者已评审本系列本教程。 本教程中的潜在顾客审阅者包括 Alicja Maziarz、 John Suru 和 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](forms-authentication-configuration-and-advanced-topics-cs.md)
> [下一页](an-overview-of-forms-authentication-vb.md)
