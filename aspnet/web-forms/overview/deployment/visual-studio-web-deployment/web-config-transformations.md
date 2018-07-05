---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 使用 Visual Studio 的 ASP.NET Web 部署： Web.config 文件转换 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用...
ms.author: aspnetcontent
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: 0a52530396efa3612d19817eeaa0498cffdac38f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842434"
---
<a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>使用 Visual Studio 的 ASP.NET Web 部署： Web.config 文件转换
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 或 Visual Studio 2010。 有关序列的信息，请参阅[系列中的第一个教程](introduction.md)。


## <a name="overview"></a>概述

本教程演示如何自动执行更改的过程*Web.config*文件时将其部署到不同的目标环境。 大多数应用程序中具有设置*Web.config*部署应用程序必须是不同的文件。 自动执行进行这些更改的过程可以防止您无需手动执行它们，每次部署，这可能会比较繁琐且容易出错。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](troubleshooting.md)。

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>与 Web 部署参数的 Web.config 转换

有两种方法来自动执行更改的过程*Web.config*文件设置： [Web.config 转换](https://msdn.microsoft.com/library/dd465326.aspx)并[Web 部署参数](https://msdn.microsoft.com/library/ff398068.aspx)。 一个*Web.config*转换文件包含用于指定如何更改 XML 标记*Web.config*文件部署时。 您可以指定不同的更改的特定生成配置，并为特定发布配置文件。 默认生成配置是调试和发布，并且可以创建自定义生成配置。 发布配置文件通常对应于目标环境。 (有关详细信息发布配置文件中的，您将学习[作为测试环境部署到 IIS](deploying-to-iis.md)教程。)

Web 部署参数可用于指定必须在部署期间，包括设置中找到的配置设置的许多不同种类*Web.config*文件。 用于指定当*Web.config*文件发生更改，Web 部署参数是更复杂，进行设置，但不是知道要在部署前设置的值时十分有用。 例如，在企业环境中，您可以创建*部署包*并将其提供给 IT 部门中的用户安装在生产中，并该用户有能够输入连接字符串或不这样做的密码知道。

对于本教程系列介绍了方案，您事先知道所有内容都采取的措施*Web.config*文件，因此不需要使用 Web 部署参数。 将配置一些转换，具体取决于使用，将生成配置不同，一些，具体取决于使用的发布配置文件不同。

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>在 Azure 中的指定 Web.config 设置

如果*Web.config*你想要更改的文件设置位于`<connectionStrings>`或`<appSettings>`元素，并且您要部署到 Azure 应用服务中的 Web 应用，则可以自动执行过程中的更改的另一个选项部署。 可以输入你想要在 Azure 中才会生效的设置**配置**的 web 应用的管理门户页的选项卡 (向下滚动到**应用程序设置**和**连接字符串**部分)。 时部署项目时，Azure 会自动应用所做的更改。 有关详细信息，请参阅[Windows Azure 网站： 应用程序字符串和连接字符串的工作](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。

## <a name="default-transformation-files"></a>默认转换文件

在中**解决方案资源管理器**，展开*Web.config*以查看*Web.Debug.config*并*Web.Release.config*转换文件默认情况下，对两个默认的生成配置创建。

![Web.config_transform_files](web-config-transformations/_static/image1.png)

可以通过右键单击 Web.config 文件，然后选择创建转换文件的自定义生成配置**添加配置转换**从上下文菜单。 对于本教程无需执行此操作，并已禁用的菜单选项，因为尚未创建任何自定义生成配置。

稍后需要创建三个更多转换文件，每个测试，用于过渡和生产发布配置文件。 设置来处理在发布配置文件转换文件中因为它依赖于目标环境的一个典型示例是不同的测试与生产的 WCF 终结点。 你将创建发布配置文件转换文件中更高版本的教程后创建它们随附的发布配置文件。

## <a name="disable-debug-mode"></a>禁用调试模式

而不是目标环境将是依赖于生成配置设置的示例`debug`属性。 为发布版本中，您通常希望调试被禁用而不考虑哪些环境要部署到。 因此，默认情况下，Visual Studio 项目模板创建*Web.Release.config*转换文件中删除的代码`debug`属性从`compilation`元素。 下面是默认值*Web.Release.config*： 除了被注释掉了一些示例转换代码，它包括中的代码`compilation`移除的元素`debug`属性：

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

`xdt:Transform="RemoveAttributes(debug)"`属性指定您希望`debug`属性从删除`system.web/compilation`元素中已部署*Web.config*文件。 这会在每次部署发布版本。

## <a name="limit-error-log-access-to-administrators"></a>限制对管理员的错误日志访问

如果没有错误应用程序运行时，应用程序将显示一般错误页中代替系统生成的错误页上，并且它使用[Elmah NuGet 包](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)错误日志记录和报告。 `customErrors`应用程序中的元素*Web.config*文件指定的错误页：

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

若要查看错误页，暂时更改`mode`属性的`customErrors`"RemoteOnly"为"开"，并运行应用程序从 Visual Studio 中的元素。 导致错误的请求无效的 URL，如*Studentsxxx.aspx*。 而不是 IIS 生成"无法找到资源"错误页上，你看到*GenericErrorPage.aspx*页。

![错误页](web-config-transformations/_static/image2.png)

若要查看错误日志，替换 URL 中的所有内容后使用的端口号*elmah.axd* (例如， `http://localhost:51130/elmah.axd`) 并按 Enter:

![ELMAH 页](web-config-transformations/_static/image3.png)

不要忘记设置`customErrors`返回到"RemoteOnly"模式下完成后的元素。

在开发计算机上是可以方便地允许免费访问错误日志页中，但在生产环境时可能带来安全风险中。 对于生产站点中，您要添加授权规则，将错误日志的访问限制为管理员，并确保，限制适用于你想在测试和过渡还。 因此，这是另一项更改，你想要实现和每次部署发布版本中，因此它属于*Web.Release.config*文件。

打开*Web.Release.config* ，并添加新`location`立即关闭之前的元素`configuration`标签，如下所示。

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

`Transform`属性值为"插入"，则这`location`要作为同级添加到任何现有元素`location`中的元素*Web.config*文件。 (已包含一个`location`元素，它指定授权规则**更新信用额度**页。)

现在可以预览要确保您正确编码的转换。

在中**解决方案资源管理器**，右键单击*Web.Release.config*然后单击**预览版转换**。

![预览转换菜单](web-config-transformations/_static/image4.png)

演示如何开发一个页随即打开*Web.config*上的左窗格和内容文件在已部署*Web.config*文件将如下所示在右侧，突出显示了更改。

![调试转换的预览](web-config-transformations/_static/image5.png)

![位置转换的预览](web-config-transformations/_static/image6.png)

(在预览版中，您可能注意到不是自己编写一些附加更改转换为： 这些通常涉及到的空白区域，但不会影响功能删除。)

在部署后测试该站点时，还将测试以验证授权规则有效。

> [!NOTE] 
> 
> **安全说明**永远不会显示错误详细信息公开在生产应用程序中，或将该信息存储在公共位置。 攻击者可以使用错误的信息来发现站点中的漏洞。 如果在自己的应用程序中使用 ELMAH，配置 ELMAH，尽量降低安全风险。 在本教程中的 ELMAH 示例不应视为是建议的配置。 它是为了说明如何处理应用程序必须能够创建中的文件的文件夹选择了一个示例。 有关详细信息，请参阅[保护 ELMAH 终结点](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)。


## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>将处理中的设置发布配置文件转换文件

一种常见方案是让*Web.config*文件必须部署到每个环境中不同的设置。 例如，调用 WCF 服务的应用程序可能需要测试和生产环境中的不同终结点。 Contoso 大学应用程序还包括这种类型的设置。 此设置控制站点的页面上告诉您是在中，如开发、 测试或生产的环境的可见指示符。 设置值确定该应用程序是否将追加"（开发）"或"（测试）"中的主标题*Site.Master*母版页：

![环境指示器](web-config-transformations/_static/image7.png)

在过渡环境或生产环境中运行该应用程序时，将忽略环境指示器。

Contoso University web 页面读取中设置的值`appSettings`中*Web.config*以便确定哪种环境中运行应用程序的文件：

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

值应在测试环境中，将"Test"，"Prod"过渡和生产。

转换文件中的以下代码将实现此转换：

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

`xdt:Transform`属性的值"SetAttributes"指示此转换的目的是要更改属性值中的现有元素*Web.config*文件。 `xdt:Locator`属性的值"Match(key)"指示要修改的元素是一个其`key`属性匹配`key`此处指定的属性。 仅另一个属性的`add`元素是`value`，这也将更改的内容中已部署*Web.config*文件。 此处显示的原因的代码`value`的属性`Environment``appSettings`设置为"Test"中的元素*Web.config*部署的文件。

此转换属于你尚未创建的发布配置文件转换文件。 将创建并更新创建测试、 过渡和生产环境的发布配置文件时实施此更改的转换文件。 将在执行该操作[部署到 IIS](deploying-to-iis.md)并[部署到生产环境](deploying-to-production.md)教程。

> [!NOTE]
> 因为此设置位于`<appSettings>`元素中，您有另一种方法，用于指定转换时你正在部署到 Azure 应用服务另请参阅中的 Web 应用[在 Azure 中的指定 Web.config 设置](#watransforms)前面的本主题中。


## <a name="setting-connection-strings"></a>设置连接字符串

尽管默认转换文件中包含的示例，演示如何更新连接字符串，但在大多数情况下不需要设置连接字符串转换，因为你可以发布配置文件中指定连接字符串。 将在执行该操作[部署到 IIS](deploying-to-iis.md)并[部署到生产环境](deploying-to-production.md)教程。

## <a name="summary"></a>总结

您现在要做为您就可以*Web.config*转换之前创建发布配置文件，并已了解的一切将会在部署的 Web.config 文件预览。

![位置转换的预览](web-config-transformations/_static/image8.png)

在以下教程中，你将需要设置项目属性的部署设置任务的处理。

## <a name="more-information"></a>详细信息

本教程中所涉及的主题的详细信息，请参阅[使用 Web.config 转换，以在部署过程中更改目标 Web.config 文件或 app.config 文件中的设置](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms)中的 Web 部署内容映射Visual Studio 和 ASP.NET。

> [!div class="step-by-step"]
> [上一页](preparing-databases.md)
> [下一页](project-properties.md)
