---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： Web.Config 文件转换的 3 部分，共 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: aspnetcontent
ms.date: 11/17/2011
ms.assetid: 2b0df3d9-450b-4ea6-b315-4c9650722cad
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
msc.type: authoredcontent
ms.openlocfilehash: a5afcf4d05d6fa51ad70f7e5bdfafd20002f188a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37841753"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-webconfig-file-transformations---3-of-12"></a>使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： Web.Config 文件转换的 3 部分，共 12
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。 如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。 该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 显示了 Visual Studio 2012 RC 版后引入的部署功能，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并显示了如何将部署到 Azure 应用服务 Web 应用的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。


## <a name="overview"></a>概述

本教程演示如何自动执行更改的过程*Web.config*文件时将其部署到不同的目标环境。 大多数应用程序中具有设置*Web.config*部署应用程序必须是不同的文件。 自动执行进行这些更改的过程可以防止您无需手动执行它们，每次部署，这可能会比较繁琐且容易出错。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config 转换与 Web 部署参数

有两种方法来自动执行更改的过程*Web.config*文件设置： [Web.config 转换](https://msdn.microsoft.com/library/dd465326.aspx)并[Web 部署参数](https://msdn.microsoft.com/library/ff398068.aspx)。 一个*Web.config*转换文件包含用于指定如何更改 XML 标记*Web.config*文件部署时。 您可以指定不同的更改的特定生成配置，并为特定发布配置文件。 默认生成配置是调试和发布，并且可以创建自定义生成配置。 发布配置文件通常对应于目标环境。 (有关详细信息发布配置文件中的，您将学习[作为测试环境部署到 IIS](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教程。)

Web 部署参数可用于指定必须在部署期间，包括设置中找到的配置设置的许多不同种类*Web.config*文件。 用于指定当*Web.config*文件发生更改，Web 部署参数是更复杂，进行设置，但不是知道要在部署前设置的值时十分有用。 例如，在企业环境中，您可以创建*部署包*并将其提供给 IT 部门中的用户安装在生产中，并该用户有能够输入连接字符串或不这样做的密码知道。

对于本教程介绍了方案，您知道的所有内容都要采取的措施*Web.config*文件，因此不需要使用 Web 部署参数。 将配置一些转换，具体取决于使用，将生成配置不同，一些，具体取决于使用的发布配置文件不同。

## <a name="creating-transformation-files-for-publish-profiles"></a>创建发布配置文件的转换文件

在中**解决方案资源管理器**，展开*Web.config*以查看*Web.Debug.config*并*Web.Release.config*转换文件默认情况下，对两个默认的生成配置创建。

![Web.config_transform_files](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image1.png)

可以通过右键单击 Web.config 文件，然后选择创建转换文件的自定义生成配置**添加配置转换**从上下文菜单中，但对于本教程无需执行此操作。

您需要两个更多的转换文件，用于配置部署目标，而不是生成配置相关的更改。 这种设置的典型示例是不同的测试与生产的 WCF 终结点。 在更高版本的教程中，您将创建发布配置文件，名为测试和生产环境中，因此您需要*Web.Test.config*文件和一个*Web.Production.config*文件。

必须手动创建发布配置文件相关联的转换文件。 在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目并选择**在 Windows 资源管理器中打开文件夹**。

![Open_folder_in_Windows_Explorer](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image2.png)

在中**Windows 资源管理器**，选择*Web.Release.config*文件，复制文件，然后再粘贴两份。 重命名这些副本*Web.Production.config*并*Web.Test.config*，然后关闭**Windows 资源管理器**。

在中**解决方案资源管理器**，单击**刷新**若要查看新的文件。

选择新文件中，右键单击，然后单击**在项目中的包括**的上下文菜单中。

![在项目中包括测试和生产配置文件](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image3.png)

若要阻止这些文件部署，选择在其**解决方案资源管理器**，然后在**属性**窗口中更改**生成操作**属性从**内容**到**无**。 （根据生成配置的转换文件会自动阻止部署。）

你现已准备好输入*Web.config*转换为*Web.config*转换文件。

## <a name="limiting-error-log-access-to-administrators"></a>限制对管理员的错误日志访问

如果没有错误应用程序运行时，应用程序将显示一般错误页中代替系统生成的错误页上，并且它使用[Elmah NuGet 包](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)错误日志记录和报告。 `customErrors`中的元素*Web.config*文件指定的错误页：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample1.xml)]

若要查看错误页，暂时更改`mode`属性的`customErrors`"RemoteOnly"为"开"，并运行应用程序从 Visual Studio 中的元素。 导致错误的请求无效的 URL，如*Studentsxxx.aspx*。 而不是 IIS 生成"找不到页面"错误页，您看到*GenericErrorPage.aspx*页。

[![Error_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image5.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image4.png)

若要查看错误日志，替换 URL 中的所有内容后使用的端口号*elmah.axd* (例如屏幕截图中，在`http://localhost:51130/elmah.axd`) 并按 Enter:

[![Elmah_log_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image7.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image6.png)

不要忘记设置`customErrors`返回到"RemoteOnly"模式下完成后的元素。

在开发计算机上是可以方便地允许免费访问错误日志页中，但在生产环境时可能带来安全风险中。 对于生产站点中，可以添加只向管理员来配置中的转换限制错误日志访问的授权规则*Web.Production.config*文件。

打开*Web.Production.config* ，并添加新`location`紧跟左括号之后元素`configuration`标签，如下所示。 (请确保仅添加`location`元素，并不周围的标记的如下所示只是为了提供一些上下文。)

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample2.xml?highlight=2-9)]

`Transform`属性值为"插入"，则这`location`要作为同级添加到任何现有元素`location`中的元素*Web.config*文件。 (已包含一个`location`元素，它指定授权规则**更新信用额度**页。)在部署后测试生产站点时，将测试以验证此授权规则有效。

无需限制错误日志访问在测试环境中，因此无需添加到此代码*Web.Test.config*文件。

> [!NOTE] 
> 
> **安全说明**永远不会显示错误详细信息公开在生产应用程序中，或将该信息存储在公共位置。 攻击者可以使用错误的信息来发现站点中的漏洞。 如果在自己的应用程序中使用 ELMAH，务必调查中可以配置 ELMAH 以尽量降低安全风险的方式。 在本教程中的 ELMAH 示例不应视为是建议的配置。 它是为了说明如何处理应用程序必须能够创建中的文件的文件夹选择了一个示例。


## <a name="setting-an-environment-indicator"></a>设置环境指示器

一种常见方案是让*Web.config*文件必须部署到每个环境中不同的设置。 例如，调用 WCF 服务的应用程序可能需要测试和生产环境中的不同终结点。 Contoso 大学应用程序还包括这种类型的设置。 此设置控制站点的页面上告诉您是在中，如开发、 测试或生产的环境的可见指示符。 设置值确定该应用程序是否将追加"（开发）"或"（测试）"中的主标题*Site.Master*母版页：

[![Environment_indicator](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image9.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image8.png)

在生产中运行应用程序时，将忽略环境指示器。

Contoso University web 页面读取中设置的值`appSettings`中*Web.config*以便确定哪种环境中运行应用程序的文件：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample3.xml)]

值应为"Test"的测试环境和"Prod"在生产环境中。

打开*Web.Production.config*并添加`appSettings`元素的开始标记之前立即`location`前面添加的元素：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample4.xml)]

`xdt:Transform`属性的值"SetAttributes"指示此转换的目的是要更改属性值中的现有元素*Web.config*文件。 `xdt:Locator`属性的值"Match(key)"指示要修改的元素是一个其`key`属性匹配`key`此处指定的属性。 仅另一个属性的`add`元素是`value`，这也将更改的内容中已部署*Web.config*文件。 此代码会导致`value`的属性`Environment``appSettings`设置为"Prod"中的元素*Web.config*文件部署到生产环境。

接下来，将应用到相同的更改*Web.Test.config*文件中的，除集`value`到而不是"Prod""Test"。 完成后，`appSettings`主题中*Web.Test.config*看起来如下例所示：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample5.xml)]

## <a name="disabling-debug-mode"></a>禁用调试模式

为发布版本中，您不希望启用调试而不考虑哪些环境要部署到。 默认情况下*Web.Release.config*转换文件自动创建与删除的代码`debug`属性从`compilation`元素：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample6.xml)]

`Transform`属性的原因`debug`要省略属性从已部署*Web.config*文件时将部署发布版本。

此相同的转换是测试和生产环境中转换文件因为通过复制发布转换文件来创建它们。 此后不会那里重复，因此请打开每个文件，删除**编译**元素，并保存并关闭每个文件。

## <a name="setting-connection-strings"></a>设置连接字符串

在大多数情况下不需要设置连接字符串转换，因为你可以发布配置文件中指定连接字符串。 但有一点例外，在部署 SQL Server Compact 数据库时，并使用 Entity Framework Code First 迁移来更新目标服务器上的数据库。 对于此方案，您必须指定将可用于在服务器进行更新数据库架构的其他连接字符串。 若要设置此转换，将添加**&lt;connectionStrings&gt;** 紧跟左括号之后元素**&lt;configuration&gt;** 在这种标记*Web.Test.config*并*Web.Production.config*转换文件：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample7.xml)]

`Transform`属性指定此连接字符串将添加到*connectionStrings*元素中已部署*Web.config*文件。 (在发布过程创建此附加的连接字符串会自动为您如果不存在，但默认情况下**providerName**属性获取设置为`System.Data.SqlClient`，这不不适用于 SQL Server Compact 起作用。 通过手动添加的连接字符串，您将部署过程从使用错误的提供程序名称创建一个连接字符串元素。）

现在已指定的所有*Web.config* Contoso 大学应用程序来测试和生产部署所需的转换。 在以下教程中，你将需要设置项目属性的部署设置任务的处理。

## <a name="more-information"></a>详细信息

本教程中所涉及的主题的详细信息，请参阅中的 Web.config 转换方案[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521.aspx)。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
> [下一页](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
