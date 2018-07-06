---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-vb
title: 核心 IIS 和 ASP.NET 开发服务器 (VB) 之间的差异 |Microsoft Docs
author: rick-anderson
description: 当测试 ASP.NET 应用程序的本地时，很可能使用 ASP.NET 开发 Web 服务器。 但是，生产网站是最有可能 pow...
ms.author: aspnetcontent
ms.date: 04/01/2009
ms.assetid: 090e9205-52f3-4d72-ae31-44775b8b8421
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-vb
msc.type: authoredcontent
ms.openlocfilehash: 586bc45a44e773c3097de0959411a2d27098459a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821085"
---
<a name="core-differences-between-iis-and-the-aspnet-development-server-vb"></a>IIS 和 ASP.NET 开发服务器 (VB) 之间的核心差异
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_06_VB.zip)或[下载 PDF](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial06_WebServerDiff_vb.pdf)

> 当测试 ASP.NET 应用程序的本地时，很可能使用 ASP.NET 开发 Web 服务器。 但是，生产网站是最有可能已通电的 IIS。 有一些区别这些 web 服务器如何处理请求，并且这些差异可以具有重要的结果。 本教程探讨的一些更无关的差异。


## <a name="introduction"></a>介绍

每当用户访问的 ASP.NET 应用程序时其浏览器发送请求到网站。 由 web 服务器软件与 ASP.NET 运行时生成并返回所请求的资源的内容协调选取该请求。 [**我**nternet**我**表示**S** ervices (IIS)](http://en.wikipedia.org/wiki/Internet_Information_Services)是一套服务提供的通用的基于 Internet 的功能Windows 服务器。 IIS 是 ASP.NET 应用程序在生产环境; 最常使用的 web 服务器它很可能是正在使用 web 宿主提供程序的 ASP.NET 应用程序提供服务的 web 服务器软件。 IIS 还可作为 web 服务器软件在开发环境中，尽管这需要安装 IIS 并将其正确配置。


ASP.NET 开发服务器是用于开发环境中; 一个替代 web 服务器选项它附带并集成到 Visual Studio。 除非 web 应用程序已配置为使用 IIS，ASP.NET Development Server 自动启动并用作 web 服务器访问网页从 Visual Studio 中的第一个时间。 我们回到在中创建的演示 web 应用程序[*确定哪些文件需要将部署到*](determining-what-files-need-to-be-deployed-vb.md)教程是未配置为使用 IIS 这两个文件基于系统的 web 应用程序。 因此，当访问 Visual Studio 中从这些网站之一使用 ASP.NET Development Server。

在理想情况下开发和生产环境将是相同的。 但是，如前面的教程中所述不常见的环境可以有不同的配置设置。 在环境中使用另一个 web 服务器软件添加部署应用程序时必须考虑的另一个变量。 本教程介绍了 IIS 和 ASP.NET 开发服务器之间的主要差异。 由于这些差异是的情形，在开发环境中良好运行的代码将引发异常或以不同的方式在生产环境中执行时的行为。

## <a name="security-context-differences"></a>安全上下文的差异

每当 web 服务器软件处理传入的请求时它将与特定的安全上下文关联该请求。 操作系统使用此安全上下文信息以确定哪些操作允许该请求。 例如，ASP.NET 页面可能包含某些消息记录到磁盘上的文件的代码。 为了使此 ASP.NET 页后，可以执行不会出错，安全上下文必须具有相应的文件系统级别的权限，即写入该文件上的权限。

ASP.NET Development Server 将传入请求与当前登录用户的安全上下文相关联。 如果登录到您的桌面以管理员身份，ASP.NET 开发服务器提供的 ASP.NET 页面将具有相同的访问权限，以管理员身份。 但是，由 IIS 处理 ASP.NET 请求是与特定的计算机帐户相关联。 默认情况下，网络服务计算机帐户使用由 IIS 版本 6 和 7，尽管 web 主机提供商可能已配置的唯一帐户，每个客户。 更重要的是，web 主机提供商可能提供到此计算机帐户的有限的权限。 最终结果是，您可能必须在开发环境中正确执行，但在生产环境中生成与授权相关的异常时托管的网页。

我的书评网站中的某人创建存储的最新的日期和时间的磁盘上的文件创建了一个页面在操作中展示此类错误查看*教您自己 ASP.NET 3.5 24 小时内*查看。 若要跟着介绍一起操作，打开`~/Tech/TYASP35.aspx`页上，添加以下代码`Page_Load`事件处理程序：

[!code-vb[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample1.vb)]

> [!NOTE]
> [ `File.WriteAllText`方法](https://msdn.microsoft.com/library/system.io.file.writealltext.aspx)创建一个新文件，如果它不存在，然后向其中写入指定的内容。 如果该文件已存在，则会覆盖现有内容。


接下来，请访问*教您自己 ASP.NET 3.5 24 小时内*使用 ASP.NET 开发服务器在开发环境中的通讯簿查看页。 假设你登录到您的计算机使用的帐户有足够的权限来创建和修改的文本文件中 web 应用程序的根目录书评出现与之前相同，但该页是每次访问日期和时间以及用户的 IP 地址存储在`LastTYASP35Access.txt`文件。 在浏览器指向此文件;应看到类似于图 1 中所示的消息。


[![文本文件包含的最后一个日期和时间访问过书籍评论&lt;](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image2.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image1.png)

**图 1**： 文本文件包含的最后一个日期和时间访问过书籍评论 ([单击以查看实际尺寸的图像](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image3.png))


部署到生产 web 应用程序，然后访问承载*教您自己 ASP.NET 3.5 24 小时内*书籍查看页。 此时你应为 normal 或图 2 所示的错误消息显示书籍查看页。 某些 web 宿主提供程序授予对匿名的 ASP.NET 计算机帐户，在其中用例页面无错误的写入权限。 如果，但是，web 主机提供商禁止匿名帐户的写访问权限，然后[`UnauthorizedAccessException`异常](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx)时，将引发`TYASP35.aspx`的页面尝试编写的当前日期和时间`LastTYASP35Access.txt`文件。


[![使用 IIS 的默认计算机帐户没有写入到文件系统权限](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image5.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image4.png)

**图 2**: 默认计算机帐户由 IIS 不会不有权写入到文件系统 ([单击以查看实际尺寸的图像](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image6.png))


好消息是大多数 web 主机提供商具有某种权限工具，可在你的网站中指定文件系统权限。 授予匿名 ASP.NET 帐户写入访问权限的根目录，然后重新审视书籍查看页。 （如果需要请联系您的 web 主机提供商寻求帮助如何授予到默认的 ASP.NET 帐户的写入权限。）此页应加载没有错误的时间和`LastTYASP35Access.txt`应已成功创建文件。

Take 掉下面是，由于 ASP.NET Development Server 比 IIS 不同的安全上下文下运行，所以有可能，ASP.NET 页的读取或写入到文件系统中，从读取或写入到 Windows 事件日志中，或读取或写入到 Windows 注册表将开发上按预期运行，但会生成生产上的异常。 在构建 web 应用程序将部署到共享 web 托管环境中，不读取或写入事件日志或 Windows 注册表。 此外请注意，读取或写入文件系统，因为可能需要授予读取和写入上相应的文件夹的权限在生产环境中任何 ASP.NET 页面。

## <a name="differences-on-serving-static-content"></a>提供静态内容上的差异

IIS 和 ASP.NET 开发服务器之间的另一个核心区别是它们如何处理对静态内容的请求。 进入 ASP.NET Development Server，无论是用于 ASP.NET 页、 图像或一个 JavaScript 文件，每个请求由 ASP.NET 运行时处理。 默认情况下，IIS 仅调用 ASP.NET 运行时对于 ASP.NET 资源，例如 ASP.NET 网页、 Web 服务等传入的请求时。 通过 IIS 而不涉及 ASP.NET 运行时检索的静态内容的图像、 CSS 文件、 JavaScript 文件、 PDF 文件、 ZIP 文件和类似的请求。 （它是可能会指示 IIS 以便与 ASP.NET 运行时一起使用时提供静态内容; 在本教程，了解详细信息请参阅的"执行基于窗体的身份验证和上使用 IIS 7 的静态文件的 URL 身份验证"部分。）

ASP.NET 运行时执行若干步骤来生成请求的内容，包括 （标识请求者） 的身份验证和授权 （如果请求者有权查看请求的内容确定）。 常用形式的身份验证是*基于窗体的身份验证*中的用户标识通过到文本框中输入其凭据 （通常的用户名和密码），在网页上。 在验证其凭据，网站将存储*身份验证票证*上用户的浏览器中，这与每个后续请求发送到网站和内容使用，用于对用户进行身份验证 cookie。 此外，就可以指定*URL 授权*规则，规定哪些用户可以或无法访问特定文件夹。 许多 ASP.NET 网站使用基于窗体的身份验证和授权 URL 来支持用户帐户并定义才可供身份验证的用户或属于某一特定角色的用户访问站点的部分。

> [!NOTE]
> 有关对 ASP 的全面检查。NET 的基于窗体的身份验证、 URL 授权和其他用户帐户相关的功能，请确保在签出我[网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。


请考虑可支持使用基于窗体的授权的用户帐户和具有的文件夹，使用 URL 授权配置为仅允许经过身份验证的用户的网站。 假设此文件夹包含 ASP.NET 页的 PDF 文件和其目的是，仅身份验证的用户可以查看这些 PDF 文件。

如果访问者尝试通过直接在其浏览器地址栏中输入 URL 来查看其中一个 PDF 文件，会发生什么情况？ 若要了解，让我们在书评站点中创建一个新的文件夹、 添加一些 PDF 文件，和将站点配置为使用 URL 授权，禁止匿名用户访问此文件夹。 如果下载演示应用程序，您将看到我创建一个名为文件夹`PrivateDocs`并添加从 PDF 我[网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)（如何配适 ！）。 `PrivateDocs`文件夹还包含`Web.config`指定 URL 授权规则以拒绝匿名用户的文件：

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample2.xml)]

最后，我配置了 web 应用程序使用基于窗体的身份验证通过更新 Web.config 文件的根目录中替换为：

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample3.xml)]

替换为：

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample4.xml)]

使用 ASP.NET 开发服务器，请访问网站和直接 URL 输入到浏览器地址栏中的 PDF 文件之一。 如果您下载与本教程中的 URL 应如下所示关联的网站： `http://localhost:portNumber/PrivateDocs/aspnet_tutorial01_Basics_vb.pdf`

在地址栏中输入此 URL 会导致浏览器将请求发送到 ASP.NET 开发服务器的文件。 ASP.NET Development Server 移交给 ASP.NET 运行时进行处理的请求。 因为我们尚未登录，并且`Web.config`中`PrivateDocs`文件夹配置为拒绝匿名访问，ASP.NET 运行时自动重我们定向到登录页上， `Login.aspx` （参见图 3）。 当将用户重定向到登录页，ASP.NET 包括`ReturnUrl`查询字符串参数，用于指示页面用户正在尝试查看。 在用户成功登录后可以返回到此页。


[![未经授权的用户会自动重定向到登录页](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image8.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image7.png)

**图 3**： 未经授权的用户会自动重定向到登录页 ([单击以查看实际尺寸的图像](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image9.png))


现在让我们了解此生产上的行为方式。 部署应用程序和直接 URL 输入到一个在 Pdf`PrivateDocs`在生产环境中的文件夹。 这会提示你的浏览器发送请求的 IIS 的文件。 因为请求静态文件时，IIS 检索并返回该文件而无需调用 ASP.NET 运行时。 因此，执行; 没有 URL 授权检查据推测专用 PDF 内容都可以了解到的文件的直接 URL 的任何人访问。


[![匿名用户可以通过直接 URL 输入到文件下载私有 PDF 文件](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image11.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image10.png)

**图 4**： 匿名用户可以下载专用 PDF 文件的输入直接 URL 到文件 ([单击以查看实际尺寸的图像](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image12.png))


### <a name="performing-forms-based-authentication-and-url-authentication-on-static-files-with-iis-7"></a>对静态文件与 IIS 7 执行基于窗体的身份验证和 URL 身份验证

有几个可以用来防止未经授权的用户的静态内容的方法。 IIS 7 引入*集成的管道*，其中结婚 IIS 的工作流与 ASP.NET 运行时的工作流。 简单地说，您可以指示要调用 ASP.NET 运行时的身份验证和授权模块 （包括静态内容，如 PDF 文件） 的所有传入请求的 IIS。 与 web 主机提供商联系以了解如何配置网站以使用集成的管道。

集成的管道配置 IIS 以使用后添加以下标记到`Web.config`的根目录中的文件：

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample5.xml)]

此标记指示 IIS 7 以使用基于 ASP.NET 的身份验证和授权模块。 重新部署你的应用程序，然后重新访问的 PDF 文件。 当 IIS 将处理该请求这次它使 ASP.NET 运行时的身份验证和授权逻辑能够检查请求。 因为只有经过身份验证的用户有权查看中的内容`PrivateDocs`文件夹中，匿名访问者将自动重定向到登录页 （回头参考图 3 中）。

> [!NOTE]
> 如果您的 web 主机提供商仍在使用 IIS 6，则无法使用集成的管道功能。 一种解决办法是将私有文档放入禁止 HTTP 访问的文件夹 (如`App_Data`)，然后创建页后，可以服务于这些文档。 此页可能会调用`GetPDF.aspx`，并传递 PDF 通过查询字符串参数的名称。 `GetPDF.aspx`页会首先验证用户有权查看该文件并且，如果是这样，将使用[ `Response.WriteFile(filePath)` ](https://msdn.microsoft.com/library/system.web.httpresponse.writefile.aspx)方法以返回到请求的客户端发送请求的 PDF 文件的内容。 如果不希望启用集成的管道，此方法将也适用于 IIS 7。


## <a name="summary"></a>总结

使用 Microsoft 的 IIS web 服务器软件被托管在生产环境中的 web 应用程序。 在开发环境中，但是，应用程序可能位于使用 IIS 或 ASP.NET 开发服务器。 理想情况下，相同的 web 服务器软件应在这两个环境中由于使用不同的软件的组合中添加另一个变量。 但是，易于使用的 ASP.NET Development Server 使其成为一个理想选择开发环境中。 值得高兴的是，只有几个基本差异 IIS 和 ASP.NET 开发服务器之间，如果已经知道这些差异的您可以采取措施来帮助确保应用程序工作原理和功能相同的方式而不考虑环境。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [使用 IIS 7.0 ASP.NET 集成](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)
- [与所有类型的内容在 IIS 7 上使用 ASP.NET 论坛身份验证](https://blogs.iis.net/bills/archive/2007/05/19/using-asp-net-forms-authentication-with-all-types-of-content-with-iis7-video.aspx)（视频）
- [Visual Web Developer 中的 web 服务器](https://msdn.microsoft.com/library/58wxa9w5.aspx)

> [!div class="step-by-step"]
> [上一页](common-configuration-differences-between-development-and-production-vb.md)
> [下一页](deploying-a-database-vb.md)
