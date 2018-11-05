---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET 网页 (Razor) 故障排除指南 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍使用 ASP.NET Web Pages (Razor) 和一些建议的解决方案时可能遇到的问题。 软件版本 ASP.NET Web 页的链接...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: ec8cdda5c5b298736a650f82cd6b52d73b6dfe3d
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021191"
---
<a name="aspnet-web-pages-razor-troubleshooting-guide"></a>ASP.NET 网页 (Razor) 疑难解答指南
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍使用 ASP.NET Web Pages (Razor) 和一些建议的解决方案时可能遇到的问题。
> 
> ## <a name="software-versions"></a>软件版本
> 
> 
> - ASP.NET 网页 (Razor) 3
>   
> 
> 本教程还适用于 ASP.NET Web Pages 2 和 ASP.NET Web Pages 1.0。


本主题包含以下各节：

- [与正在运行的页面的问题](#Issues_Running_.cshtml_Pages)
- [Razor 代码的问题](#IssuesWithRazorCode)
- [安全和成员身份的问题](#membership)
- [发送电子邮件的问题](#email)
- [其他资源](#AdditionalResources)

常规问题，请参阅[ASP.NET Web Pages (Razor) 常见问题解答](https://go.microsoft.com/fwlink/?LinkId=253000)。

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a>与正在运行的页面的问题

各种问题可能会阻止 *.cshtml*并 *.vbhtml*中正常运行的页面。 本部分列出了常见的错误消息和可能的原因。

### <a name="http-error-403---forbidden-access-is-denied"></a>HTTP 错误 403-禁止访问： 访问被拒绝

*你没有权限查看此目录或页面使用所提供的凭据。*

如果服务器未运行.NET Framework 的正确版本，可以发生此错误。 请确保运行服务器 （本地或远程） 计算机至少具有安装.NET Framework 4。 此外请确保应用程序本身配置为运行正确版本。

如果本地在 WebMatrix 中工作时看到此问题，请单击**站点**工作区中，然后在树视图中单击**设置**。 在中**选择.NET Framework 版本**列表中，选择 **.NET 4 （集成）**。 如果已设置此版本，请尝试以管理员身份运行 WebMatrix。

请确保你的网站的根目录具有至少一个 *.cshtml*中该文件。

如果远程服务器上的 web 服务器时看到此错误，请与服务器管理员联系。 请确保服务器具有.NET Framework 4 或更高版本安装。 此外请确保在配置为使用该版本的.net Framework 的应用程序池中运行该应用程序。

如果必须对服务器的控制，请确保它正在运行的.NET framework 的正确版本。 您还可以尝试通过运行修复安装`aspnet_regiis -iru`命令。 （例如，如果在安装.NET Framework 之后安装 IIS，IIS 将不正确配置为运行 ASP.NET 页。）有关详细信息，请参阅[ASP.NET IIS 注册工具 (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)。

### <a name="http-error-40314---forbidden"></a>HTTP 错误 403.14-禁止访问

*Web 服务器配置为不列出此目录的内容。*

如果请求受保护的资源，则可能出现此错误 (如*Web.config*文件) 或受保护的文件夹中 (如*应用\_数据*或*应用\_代码*)。

### <a name="http-error-40417---not-found"></a>HTTP 错误 404.17-找不到

*请求的内容显示为脚本，并且不会提供静态文件处理程序。*

如果服务器未正确配置为使用.NET Framework 4 或更高版本，因此无法识别中的代码，可能出现此错误`@{ }`块。 请参阅前面的说明*HTTP 错误 403-禁止访问： 访问被拒绝*。

### <a name="http-error-4047---not-found"></a>HTTP 错误 404.7-找不到

*请求筛选模块配置为拒绝文件扩展名*

如果发生此错误，可以 *.cshtml*或 *.vbhtml*扩展已显式阻止在服务器上。 此问题的症状是该 Url 工作时不包括的扩展，但包含的 Url *.cshtml*或 *.vbhtml*不起作用。 可能的解决方案是重新启用的站点中的扩展*Web.config*文件。 下面的示例演示如何能够 *.cshtml*扩展。

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a>HTTP 错误 404.8-找不到

*配置请求筛选模块拒绝包含 hiddenSegment 部分在 URL 中的路径。*

如果请求受保护的资源，则可能出现此错误 (如*Web.config*文件) 或受保护的文件夹中 (如*应用\_数据*或*应用\_代码*)。

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a>这种类型的页未处理 （服务器错误 '/' 应用程序中）

请参阅 HTTP 错误 404.17 前面的说明。

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a>Razor 代码的问题

### <a name="the-name-class-does-not-exist-in-the-current-context"></a>名称*类*当前上下文中不存在

通常情况下，请参阅此错误的原因在于`class`未安装一个帮助器，但该帮助器的引用。 例如，如果你尝试使用一个帮助器，但尚未从 NuGet 安装包，您将看到此错误。 使用 WebMatrix 中的库查找和安装的帮助程序。

如果已安装该帮助器，但页面仍不能识别它，请尝试添加添加`using`语句的代码。 在`using`语句，包括帮助程序的命名空间的引用。 例如，ASP.NET Web 帮助器包中的基本帮助器位于`System.Web.Helpers`命名空间。 在想要使用该帮助器页的顶部，添加下面一行：

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a>安全和成员身份的问题

如果使用内置的安全 （成员资格） 系统中 ASP.NET Web Pages (Razor)，可能会遇到以下问题。

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a>若要调用此方法，"Membership.Provider"属性必须是"采用 ExtendedMembershipProvider"的实例

此错误可能指示没有`AspNetSqlMembershipProvider`配置类。 （一种症状是站点本地可正常使用，但会引发此错误时将其发布到宿主提供程序的服务器。）此问题的一个解决方法是通过将以下内容添加到站点的来显式启用简单成员资格*Web.config*文件：

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a>发送电子邮件的问题

发送电子邮件的问题可能很难调试。 最初的问题可能无法连接到 SMTP 服务器。 如果连接成功，ASP.NET 会将消息传送到 SMTP 服务器中。 但是，可能会有问题，并显示消息本身，以防止将其发送 SMTP 服务器。

如果你的应用程序未成功发送电子邮件，请尝试以下操作：

- SMTP 服务器名称通常是类似于`smtp.provider.com`或`smtp.provider.net`。 但是，如果将站点发布到宿主提供程序，将 SMTP 服务器名此时可能`localhost`。 因为已发布和提供程序的服务器上运行你的站点之后，SMTP 服务器可能会在本地从你的应用程序的角度来看，将出现这种情况。 此服务器名称中的更改可能意味着您必须在发布过程中更改 SMTP 服务器名称。
- 端口号通常为 25。 但是，某些提供程序需要使用端口 587 或某些其他端口。 咨询哪个端口号，他们期望您要使用的 SMTP 服务器的所有者。
- 请确保使用正确的凭据。 如果你已将站点发布到宿主提供程序，使用提供程序专门指示用于电子邮件的凭据。 这些凭据可能不同于你使用发布的凭据。
- 有时您根本不需要凭据。 如果要使用您个人的 ISP 来发送电子邮件，电子邮件提供商可能已经知道你的凭据。 发布后，你可能需要使用比测试本地计算机上的其他凭据。
- 如果你的电子邮件提供商使用加密，请设置`WebMail.EnableSsl`到`true`。

如果发送电子邮件时出错，可能会看到如下所示的标准 ASP.NET 错误消息：

![ASP.NET 错误消息时使用电子邮件问题](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

此外可以调试使用发送电子邮件问题`try-catch`块，如以下示例所示。 当你使用`try-catch`块中，ASP.NET 不会显示其标准错误消息。 相反，您可以捕获中的错误`catch`的块部分。

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

替换为相应值`your-SMTP-server-name`，依次类推。 某些错误消息可能会看到这种方式包括：

- *无法发送邮件。*

    或

    *连接尝试失败，因为被连接的方未正确响应时间或建立的连接失败，因为连接的主机未能响应一段时间后*

    此错误通常意味着应用程序无法连接到 SMTP 服务器。 请检查服务器名和端口号。
- <em>邮箱不可用。服务器响应为： 5.1.0 &lt; someuser@invaliddomain &gt;发件人已拒绝： 无效的发件人域</em>

    此消息可能指示`From`地址不正确或缺少。
- *指定的字符串不是窗体所需的电子邮件地址。*

    此错误可能指示的值`To`或`From`属性不会识别为电子邮件地址。 (ASP.NET 不能检查电子邮件地址是否有效，只有它的格式正确，如*name@domain.com*。)

> [!NOTE]
> 删除显示的错误的标记 (`@errorMessage`) 页面发布到实时站点之前。 它不是一个好办法，请参阅从服务器获取的错误消息的用户。


<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>其他资源

[ASP.NET 网页 (Razor) 常见问题解答](https://go.microsoft.com/fwlink/?LinkId=253000)

[WebMatrix 和 ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) ASP.NET 网站上的论坛
