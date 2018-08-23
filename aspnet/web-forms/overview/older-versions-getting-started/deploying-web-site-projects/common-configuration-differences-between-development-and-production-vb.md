---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
title: 开发和生产环境 (VB) 之间的常见配置差异 |Microsoft Docs
author: rick-anderson
description: 在之前的教程，我们通过将所有相关文件从开发环境复制到生产环境中部署了我们的网站。 但是，我...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 548e75f6-4d6c-4cb4-8da8-417915eb8393
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
msc.type: authoredcontent
ms.openlocfilehash: ec1d575fac4527db8f5bcab5f0d84e1f17eac46b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832485"
---
<a name="common-configuration-differences-between-development-and-production-vb"></a>开发和生产环境 (VB) 之间的常见配置差异
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial05_ConfigDifferences_vb.pdf)

> 在之前的教程，我们通过将所有相关文件从开发环境复制到生产环境中部署了我们的网站。 但是，不会配置差异，这使得每个环境有一个唯一的 Web.config 文件，需要在环境之间出现不常见。 本教程中检查典型配置差异，并维护单独的配置信息的策略。


## <a name="introduction"></a>介绍


最后两个教程介绍了如何部署简单的 web 应用程序。 [*使用 FTP 客户端部署站点*](deploying-your-site-using-an-ftp-client-vb.md)教程介绍了如何使用独立的 FTP 客户端将所需的文件复制到生产的开发环境。 前面的教程[*部署您站点使用的 Visual Studio*](deploying-your-site-using-visual-studio-vb.md)、 给出了部署使用 Visual Studio 复制网站工具和发布选项。 在这两篇教程在生产环境中的每个文件是文件的在开发环境上的副本。 但是，不常见的开发环境中这些不同于在生产环境中的配置文件。 Web 应用程序的配置存储在`Web.config`文件，并通常包括有关外部资源，例如数据库、 web 和电子邮件服务器的信息。 它还规定了某些情况下，例如的未经处理的异常发生时要采取的操作过程中的应用程序的行为。

在部署 web 应用程序非常重要，正确的配置信息最终会在生产环境中。 在大多数情况下`Web.config`开发环境中的文件不能复制到与生产环境-是。 相反，自定义的版本的`Web.config`需要上传到生产环境。 本教程简要介绍了一些较常见的配置差异;它还概述了一些技术来维护环境之间的不同的配置信息。

## <a name="typical-configuration-differences-between-the-development-and-production-environments"></a>开发和生产环境之间的典型配置差异

`Web.config`文件包含具有多种类型的 ASP.NET 应用程序的配置信息。 此配置信息的一些无论是相同的环境。 例如，身份验证设置和 URL 授权规则中描述`Web.config`文件的`<authentication>`和`<authorization>`元素通常是相同的而不考虑环境。 但其他配置信息-例如外部资源的信息通常根据环境不同。

数据库连接字符串是不同的配置信息的一个典型示例根据环境。 当 web 应用程序的数据库服务器通信它必须首先建立连接，并通过实现[连接字符串](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)。 虽然可以直接在 web 页面或连接到数据库的代码中的数据库连接字符串进行硬编码，最好是将其置于`Web.config`的[`<connectionStrings>`元素](https://msdn.microsoft.com/library/bf7sd233.aspx)，以便连接字符串信息是一个单一的集中位置中。 通常不同的数据库使用在开发过程中不是在生产环境中使用因此，连接字符串信息必须是唯一的每个环境。

> [!NOTE]
> 将来的教程探索部署数据驱动的应用程序，此时我们将深入了解如何在配置文件中存储数据库连接字符串的详细信息。


开发和生产环境的预期的行为与显著不同。 在开发环境中的 web 应用程序正在创建、 测试和调试由一组少量开发人员。 在生产环境中的许多不同的并发用户正在访问同一应用程序。 ASP.NET 提供了一些功能，可帮助开发人员在测试和调试应用程序，但应为性能和安全原因，在生产环境中的禁用这些功能。 我们来看几个此类配置设置。

### <a name="configuration-settings-that-impact-performance"></a>影响性能的配置设置

ASP.NET 页面访问时第一次 （或第一次更改后），必须将其声明性标记转换为一个类，并且必须编译此类。 如果 web 应用程序使用自动编译页面的代码隐藏类需要进行编译，过。 你可以配置具有多种类型的编译选项通过`Web.config`文件的[`<compilation>`元素](https://msdn.microsoft.com/library/s10awwz0.aspx)。

调试属性是中的最重要属性之一`<compilation>`元素。 如果`debug`属性设置为"true"则编译的程序集将包含调试符号，调试 Visual Studio 中的应用程序时需要用到它。 但是，调试符号的程序集的大小增加，并运行代码时施加更多的内存要求。 此外，当`debug`属性设置为"true"返回任何内容`WebResource.axd`未缓存，这意味着，每次用户访问他们需要重新下载返回的静态内容的页面`WebResource.axd`。

> [!NOTE]
> `WebResource.axd` 内置 HTTP 处理程序中引入了 ASP.NET 2.0 服务器控件用于检索嵌入的资源，例如脚本文件、 图像、 CSS 文件和其他内容。 详细了解如何`WebResource.axd`的工作原理以及如何使用它来访问嵌入的资源从自定义服务器控件，请参阅[访问嵌入的资源通过 URL 使用`WebResource.axd` ](http://aspnet.4guysfromrolla.com/articles/080906-1.aspx)。


`<compilation>`元素的`debug`属性通常设置为"true"，在开发环境中。 实际上，此属性必须设置为"true"才能调试 web 应用程序;如果你尝试调试 ASP.NET 应用程序从 Visual Studio 和`debug`属性设置为"false"，Visual Studio 将显示一个消息，其中说明无法直到调试应用程序`debug`属性设置为"true"，并将产品/服务为你进行此更改。

您应该**永远不会**具有`debug`属性设置为"true"，在生产环境中由于其对性能的影响。 有关此主题的更深入讨论，请参阅[Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章[不运行生产 ASP.NET 应用程序与`debug="true"`已启用](https://weblogs.asp.net/scottgu/442448)。

### <a name="custom-errors-and-tracing"></a>自定义错误和跟踪

当 ASP.NET 应用程序中发生未经处理的异常时它冒泡到以下三种情况发生在哪个点运行：

- 显示通用运行时错误消息。 此页将通知用户存在运行时错误，但不提供任何错误的详细信息。
- 将显示异常详细信息消息，其中包括只需引发的异常的信息。
- 显示自定义错误页，即在 ASP.NET 页面创建用于显示所需的任何消息。

在遇到未经处理的异常时会发生什么情况取决于`Web.config`文件的[`<customErrors>`部分](https://msdn.microsoft.com/library/h0hfz6fc.aspx)。

开发和测试应用程序时最好先查看在浏览器中的任何异常的详细信息。 但是，在生产环境中的应用程序中显示异常详细信息是潜在的安全风险。 此外，它是 unflattering 并使你看起来不专业的网站。 理想情况下，发生未经处理的异常时在开发环境中的 web 应用程序将显示异常的详细信息而在生产环境中相同的应用程序将显示自定义错误页。

> [!NOTE]
> 默认值`<customErrors>`部分设置显示异常详细信息消息仅当页正在访问通过本地主机，并将否则显示通用运行时错误页。 这并不理想，但它确保要知道的默认行为不会显示对非本地的访客的异常详细信息。 将来的教程会说明`<customErrors>`中更多详细信息部分，并演示如何在自定义错误页面中所示在生产环境中发生的错误。


跟踪在开发期间非常有用的另一种 ASP.NET 功能。 跟踪，如果启用，记录有关每个传入请求的信息，并提供特殊网页`Trace.axd`，以查看最近的请求详细信息。 可以启用和配置跟踪通过[`<trace>`元素](https://msdn.microsoft.com/library/6915t83k.aspx)中`Web.config`。

如果启用跟踪，请确保它禁用在生产环境中。 由于跟踪信息包含 cookie、 会话数据和其他潜在的敏感信息，因此务必禁用在生产环境中的跟踪。 值得高兴的是，默认情况下禁用跟踪和`Trace.axd`才可通过本地主机访问文件。 如果更改这些默认设置在开发过程中请确保它们已返回在生产环境中。

## <a name="techniques-for-maintaining-separate-configuration-information"></a>维护单独的配置信息的方法

在开发和生产环境中拥有不同的配置设置会增加部署过程的复杂性。 在前面的两个教程部署过程涉及复制所有所需的文件从开发到生产环境，但该方法仅适用的配置信息是否在这两个环境中相同。 有各种技术用于部署具有不同的配置信息的应用程序。 让我们目录一些托管的 web 应用程序的这些选项。

### <a name="manually-deploying-the-production-environment-configuration-file"></a>手动部署生产环境配置文件

最简单的方法是保持两个版本的`Web.config`文件： 一个用于开发环境，一个用于生产环境。 站点部署到生产环境需要将所有文件复制到开发环境中的生产服务器*除*为`Web.config`文件。 相反，生产环境专属`Web.config`会将文件复制到生产环境。

此方法不是非常复杂，但很容易实现，因为不常更改的配置信息。 它最适合于应用程序与小型开发团队的单个 web 服务器上托管并不经常更改其配置信息。 手动部署采用独立 FTP 客户端的应用程序文件时，它是最 tenable。 使用 Visual Studio 的复制网站工具或发布选项时将需要首先换出特定于部署的`Web.config`与之前部署的特定于生产的一个文件，然后在部署完成后交换它们。

### <a name="change-the-configuration-during-the-build-or-deployment-process"></a>将在生成或部署过程期间配置更改

到目前为止讨论假设的即席生成和部署过程。 许多大型软件项目中有更为正式使用开放源代码，自行，或第三方工具的进程。 此类项目您可能可以自定义生成或部署过程，适当地修改的配置信息，然后将它推送到生产环境。 如果您构建 web 应用程序通过[MSBuild](http://en.wikipedia.org/wiki/MSBuild)， [NAnt](http://nant.sourceforge.net/)，或某些其他生成工具，可以很可能添加生成步骤来修改`Web.config`文件以包括特定于生产环境的设置。 或部署工作流无法以编程方式连接到源代码管理服务器并检索相应`Web.config`文件。

用于获取到生产环境的相应配置信息的实际方法广泛根据你的工具和工作流而异。 在这种情况下，我们不会深入了解本主题进一步。 如果使用常用的生成工具 MSBuild 或 NAnt 等部署文章和教程可以查找特定于这些工具通过 web 搜索。

### <a name="managing-configuration-differences-via-the-web-deployment-project-add-in"></a>通过 Web 部署的管理配置差异外接程序项目

在 2006 年 Microsoft Visual Studio 2005，发布了 Web 开发项目外接程序。 外接程序的 Visual Studio 2008 发布在 2008 年。 此外接程序，ASP.NET 开发人员可创建一个单独的 Web 部署项目，以及其 web 应用程序项目，生成时，显式编译 web 应用程序并将复制的文件将部署到本地的输出目录。 Web 应用程序项目在幕后使用 MSBuild。

默认情况下，在开发环境的`Web.config`文件复制到输出目录，但你可以设置要自定义的 Web 部署项目

按以下方式获取复制到此目录的配置信息：

- 通过`Web.config`文件部分替换，在其中指定要替换的部分和一个包含替换文本的 XML 文件。
- 通过提供外部配置源文件的路径。 选择此选项，则 Web 部署项目复制特定`Web.config`到输出目录的文件 (而不是`Web.config`开发环境中使用的文件)。
- 通过将自定义规则添加到使用 Web 部署项目的 MSBuild 文件。

若要部署 web 应用程序生成 Web 部署项目，然后将文件从项目的输出文件夹复制到生产环境。

若要了解有关使用 Web 部署项目的详细信息请查看[Web 部署项目本文](https://msdn.microsoft.com/magazine/cc163448.aspx)摘自的 2007 年 4 月发行[MSDN 杂志 》](https://msdn.microsoft.com/magazine/default.aspx)，或查阅在的更多参考资料部分中的链接本教程结束。

> [!NOTE]
> 不能使用 Visual Web Developer 使用 Web 部署项目，因为 Web 部署项目实现为 Visual Studio 外接程序和 Visual Studio 速成版 （包括 Visual Web Developer） 不支持外接程序。


## <a name="summary"></a>总结

外部资源和 web 应用程序开发中的行为通常不同于同一应用程序时在生产环境中。 例如，数据库连接字符串、 编译选项和未经处理的异常通常发生时的行为不同环境之间。 部署过程必须适应这些区别。 如我们在本教程中所述，最简单方法是手动将备用配置文件复制到生产环境。 可能会出现更简练的解决方案使用 Web 部署项目外接程序时或使用更正式的生成或部署进程可以容纳此类自定义项。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [所述的连接字符串](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)
- [数据库连接字符串 @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [不会运行 ASP.NET 生产应用程序与`debug="true"`启用](https://weblogs.asp.net/scottgu/Don_1920_t-run-production-ASP.NET-Applications-with-debug_3D001D20_true_1D20_-enabled)
- [适当地响应未经处理的异常-显示用户友好错误页](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [如何实现： 使用 Visual Studio 2008 Web 部署项目？](../../../videos/how-do-i/how-do-i-use-a-visual-studio-2008-web-deployment-project.md)
- [部署数据库时的密钥配置设置](http://aspnet.4guysfromrolla.com/articles/121008-1.aspx)
- [Visual Studio 2008 Web 部署项目下载](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) | [Visual Studio 2005 Web 部署项目下载](https://download.microsoft.com/download/9/4/9/9496adc4-574e-4043-bb70-bc841e27f13c/WebDeploymentSetup.msi)
- [VS 2008 Web 部署项目](https://weblogs.asp.net/scottgu/archive/2005/11/06/429723.aspx) | [VS 2008 Web 部署项目支持发布](https://weblogs.asp.net/scottgu/archive/2008/01/28/vs-2008-web-deployment-project-support-released.aspx)
- [Web 部署项目](https://msdn.microsoft.com/magazine/cc163448.aspx)

> [!div class="step-by-step"]
> [上一页](deploying-your-site-using-visual-studio-vb.md)
> [下一页](core-differences-between-iis-and-the-asp-net-development-server-vb.md)
