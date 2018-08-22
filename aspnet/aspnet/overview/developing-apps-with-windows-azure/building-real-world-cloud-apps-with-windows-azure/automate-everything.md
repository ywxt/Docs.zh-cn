---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: 自动执行所有内容 （构建实际云应用与 Azure） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: 4acf7361bed7e135c73cd46c99d15e12757e4679
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825688"
---
<a name="automate-everything-building-real-world-cloud-apps-with-azure"></a>自动执行所有内容 （构建使用 Azure 的真实世界云应用程序）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 电子书的简介，请参阅[的第一章](introduction.md)。


我们将介绍的前三个模式实际上适用于任何软件开发项目中，但特别是用于云项目。 此模式是有关自动执行开发任务。 它是一个重要的主题，因为手动流程速度慢而且容易出错;尽可能多的设置的快速、 可靠且灵活的工作流可能有助于以自动执行。 它是唯一重要的云开发的因为可以轻松地自动执行各种难以或无法在本地环境中自动执行的许多任务。 例如，可以设置整个测试环境包括新的 web 服务器和后端 Vm，数据库、 blob 存储 （文件存储）、 队列等。

## <a name="devops-workflow"></a>DevOps 工作流

越来越多地了解术语"DevOps"。 带认识，您必须集成开发和操作任务，以便有效地开发软件开发术语。 你想要启用的工作流的类型为一个在其中你可以开发应用程序、 将其部署、 学习它的生产使用情况、 将其更改以响应您已了解，和快速可靠地重复周期。

一些成功的云开发团队部署一天内多次到实时环境。 用于部署一个较大的 Azure 团队更新每隔 2-3 月，但是现在它每隔 2-3 天和主要版本每隔 2-3 周发布次要更新。 在着手创建该频率可以真正帮助您及时响应客户反馈。

为此，必须启用开发和部署周期为可重复、 可靠且可预测，并且具有较低的周期时间。

![DevOps 工作流](automate-everything/_static/image1.png)

换而言之，如果有一项功能想法和客户使用它和提供反馈时之间的时间段必须尽可能短。 前三个模式-自动化全部操作，从源代码管理和持续集成和交付-就是指我们要使这种过程建议的最佳做法。

## <a name="azure-management-scripts"></a>Azure 管理脚本

在中[简介这本电子书](introduction.md)，看到了基于 web 的控制台中，Azure 管理门户。 在管理门户，可监视和管理所有已在 Azure 部署的资源。 它是轻松地创建和删除 web 应用和 Vm 等服务，配置这些服务，监视服务操作，等等。 它是一个很好的工具，但使用它是一个手动过程。 如果想要开发生产应用程序的任何大小，尤其是在团队环境中，我们建议你通过门户以了解并探索 Azure 中，UI，然后自动执行需要重复执行的进程。

也可以通过调用 REST 管理 API 几乎是可以在管理门户中或从 Visual Studio 手动执行的一切。 你可以编写脚本使用[Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)，或者可以使用的开放源代码框架，如[Chef](http://www.opscode.com/chef/)或[Puppet](http://puppetlabs.com/puppet/what-is-puppet)。 您还可以在 Mac 或 Linux 环境中使用 Bash 命令行工具。 Azure 具有脚本 Api 编写所有这些不同的环境，并且它具有[.NET 管理 API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)以防你想要编写代码而不是脚本。

我们已修复其应用创建自动执行以下过程创建测试环境，并将项目部署到该环境中，一些 Windows PowerShell 脚本和我们将回顾一些这些脚本的内容。

## <a name="environment-creation-script"></a>环境创建脚本

我们将介绍的第一个脚本名为*新建 AzureWebsiteEnv.ps1*。 它将创建 Azure 环境，您可以修复它将应用部署到用于测试。 此脚本执行的主要任务如下所示：

- 创建 web 应用。
- 创建存储帐户。 （所需 blob 和队列，您将看到在后面的章节。）
- 创建 SQL 数据库服务器和两个数据库： 应用程序数据库和成员资格数据库。
- 设置存储在 Azure 应用程序将用于访问存储帐户和数据库。
- 创建将用于自动执行部署的设置文件。

### <a name="run-the-script"></a>运行脚本


> [!NOTE]
> 一章的此部分显示了脚本和输入才能运行这些命令的示例。 此演示，并不提供所有需要知道，才能运行脚本。 说明-将执行操作的 it 的分步说明，请参阅[附录： 修复它示例应用程序](the-fix-it-sample-application.md#deploybase)。


若要运行 PowerShell 脚本，用于管理 Azure 服务，必须安装 Azure PowerShell 控制台并将其配置为使用你的 Azure 订阅。 您正在设置后，你可以使用类似此命令的命令运行的 Fix It 环境创建脚本：

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

`Name`参数指定要在创建数据库和存储帐户时使用的名称和`SqlDatabasePassword`参数指定将为 SQL 数据库创建的管理员帐户的密码。 有您可以使用，我们将在更高版本的其他参数。

![PowerShell 窗口](automate-everything/_static/image2.png)

在脚本完成之后您可以在管理门户中看到已创建的内容。 您会发现两个数据库：

![数据库](automate-everything/_static/image3.png)

存储帐户：

![存储帐户](automate-everything/_static/image4.png)

和 web 应用：

![网站](automate-everything/_static/image5.png)

上**配置**选项卡上的 web 应用，可以看到它具有存储帐户设置和 SQL 数据库连接字符串设置为修复其应用。

![appSettings 和 connectionStrings](automate-everything/_static/image6.png)

*自动化*文件夹现在还包含 *&lt;websitename&gt;.pubxml*文件。 此文件存储 MSBuild 将使用应用程序部署到刚创建的 Azure 环境的设置。 例如：

[!code-xml[Main](automate-everything/samples/sample1.xml)]

如您所见，创建一个完整的测试环境中，脚本，并且在大约 90 秒内完成整个过程。

如果你的团队的其他人想要创建的测试环境，它们可直接运行该脚本。 不仅速度快，而且还他们可以确信它们使用等同于正在使用的环境。 您不是完全按照确信，如果每个人都已进行设置手动使用管理门户 UI。

### <a name="a-look-at-the-scripts"></a>查看脚本

有实际完成这项工作的三个脚本。 调用一个从命令行并自动使用另外两个执行的一些任务：

- *新 AzureWebSiteEnv.ps1*是主要的脚本。

    - *新 AzureStorage.ps1*创建存储帐户。
    - *新 AzureSql.ps1*创建数据库。

### <a name="parameters-in-the-main-script"></a>主脚本中的参数

主脚本*新建 AzureWebSiteEnv.ps1*，定义了多个参数：

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

两个参数是必需的：

- 该脚本创建的 web 应用的名称。 (这也用于 URL: `<name>.azurewebsites.net`。)
- 该脚本创建的数据库服务器的新管理用户的密码。

可选参数，你可以指定的数据中心位置 （默认为"West US"）、 数据库服务器管理员名称 （默认为"数据库用户"） 和数据库服务器的防火墙规则。

### <a name="create-the-web-app"></a>创建 web 应用

该脚本会执行的第一件事是通过调用创建 web 应用`New-AzureWebsite`cmdlet，在将其传递给 web 应用名称和位置参数值：

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a>创建存储帐户

然后运行主脚本<em>新建 AzureStorage.ps1</em>编写脚本，请指定"<em>&lt;websitename&gt;</em>存储"的存储帐户名称和相同的数据中心位置为web 应用中。

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

*新 AzureStorage.ps1*调用`New-AzureStorageAccount`cmdlet 来创建存储帐户，和它返回帐户名称和访问密钥值。 若要访问的 blob 和队列的存储帐户中，应用程序将需要这些值。

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

您可能并不总是希望创建新的存储帐户;通过添加参数，可以选择将定向为使用现有的存储帐户，可增强该脚本。

### <a name="create-the-databases"></a>创建数据库

然后运行主脚本的数据库创建脚本，*新建 AzureSql.ps1*、 后设置为默认数据库和防火墙规则名称：

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

数据库创建脚本检索适用于开发人员计算机的 IP 地址，并设置防火墙规则，因此开发人员计算机可以连接到和管理服务器。 数据库创建脚本然后经历几个步骤来设置数据库：

- 通过创建服务器`New-AzureSqlDatabaseServer`cmdlet。

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- 创建防火墙规则以启用开发计算机来管理服务器并启用 web 应用可以连接到它。 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- 创建的服务器名称和凭据，使用包含的数据库上下文`New-AzureSqlDatabaseServerContext`cmdlet。

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    `New-PSCredentialFromPlainText` 是调用的脚本中的函数`ConvertTo-SecureString`cmdlet 可加密密码并返回`PSCredential`对象，相同的类型的`Get-Credential`cmdlet 将返回。
- 使用创建应用程序数据库和成员资格数据库`New-AzureSqlDatabase`cmdlet。

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- 为每个数据库调用本地定义的函数 tocreates 连接字符串。 应用程序将使用这些连接字符串访问数据库。 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    Get SQLAzureDatabaseConnectionString 是基于为其提供的参数值创建的连接字符串在脚本中定义的函数。

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- 返回包含的数据库服务器名称和连接字符串的哈希表。

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

Fix It 应用程序使用单独的成员身份和应用程序数据库。 还有可能要将成员资格和应用程序数据放在一个数据库中。

### <a name="store-app-settings-and-connection-strings"></a>应用商店应用程序设置和连接字符串

Azure 有一项功能，使你能够存储设置和自动重写时返回的内容到应用程序尝试读取的连接字符串`appSettings`或`connectionStrings`Web.config 文件中的集合。 这是应用的替代方法[Web.config 转换](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)部署时。 有关详细信息，请参阅[在 Azure 中存储敏感数据](source-control.md#appsettings)此电子书中更高版本。

环境创建脚本将存储在 Azure 的所有`appSettings`和`connectionStrings`应用程序需要在 Azure 中运行时访问的存储帐户和数据库的值。

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

[New Relic](http://newrelic.com/)是我们将演示中的遥测数据框架[监视和遥测](monitoring-and-telemetry.md)一章。 环境创建脚本也会重启 web 应用，确保它选取的 New Relic 设置。

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a>为部署做好准备

在该过程结束时，环境创建脚本调用两个函数来创建部署脚本将使用的文件。

这些函数之一可创建发布配置文件 *(&lt;websitename&gt;.pubxml*文件)。 该代码调用 Azure REST API 以获取发布设置，和它将保存中的信息 *.publishsettings*文件。 然后，它从该文件的模板文件和使用信息 (*pubxml.template*) 来创建 *.pubxml*包含发布配置文件的文件。 此两步过程模拟你在 Visual Studio 中所执行的操作： 下载 *.publishsettings*文件并导入，若要创建的发布配置文件。

其他函数使用另一个模板文件 (网站 environment.template) 来创建*网站 environment.xml*文件，其中包含部署脚本将使用与设置 *.pubxml*文件。

### <a name="troubleshooting-and-error-handling"></a>故障排除和错误处理

脚本就像程序： 它们可能会失败，并且当他们做你想要知道为相关的失败，原因是什么。 出于此原因，环境创建脚本更改的值`VerbosePreference`变量从`SilentlyContinue`到`Continue`，以便显示所有详细消息。 它也会更改的值`ErrorActionPreference`变量从`Continue`到`Stop`，以便该脚本停止甚至当遇到非终止性错误：

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

它执行任何工作之前，该脚本将存储的开始时间，以便在完成时，它可以计算经过的时间：

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

完成其工作后，脚本将显示运行时间：

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

并为每个密钥操作脚本写入详细消息，例如：

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a>部署脚本

什么*新建 AzureWebsiteEnv.ps1*脚本来创建的环境，将执行*发布 AzureWebsite.ps1*脚本执行的应用程序部署。

部署脚本获取从 web 应用的名称*网站 environment.xml*创建环境创建脚本文件。

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

获取部署用户密码从 *.publishsettings*文件：

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

它将执行[MSBuild](http://msbuildbook.com/)生成并部署项目的命令：

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

如果已指定`Launch`在命令行参数，它调用`Show-AzureWebsite`cmdlet 打开默认浏览器访问网站的 URL。

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

可以使用类似此命令的命令来运行部署脚本：

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

完成后，浏览器打开与在云中运行的站点和`<websitename>.azurewebsites.net`URL。

![修复此错误应用部署到 Windows Azure](automate-everything/_static/image7.png)

## <a name="summary"></a>总结

使用这些脚本可以确信在使用相同的选项的顺序将始终执行相同的步骤。 这有助于确保团队每个开发人员不会漏掉了一些活动或搞得一团糟的内容或部署不会实际工作方式相同，在其他团队成员的环境中或在生产环境中他自己计算机上自定义内容。

类似的方式，您可以自动执行大多数 Azure 的管理功能均可在管理门户中，通过使用 REST API、 Windows PowerShell 脚本、.NET 语言 API 或一个 Bash 实用程序，可以运行在 Linux 或 mac。

在中[接下来的章节](source-control.md)我们将查看源代码，并解释其在源代码存储库中包含您的脚本。

## <a name="resources"></a>资源

- [安装和配置适用于 Azure 的 Windows PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。 说明如何安装 Azure PowerShell cmdlet 以及如何安装证书，你需要在您的计算机以便管理你的 Azure 帐户。 这是一个很好，因为它还具有用于 PowerShell 自身的资源的链接开始。
- [Azure 脚本中心](https://docs.microsoft.com/azure/automation/automation-runbook-gallery)。 适用于开发管理 Azure 服务，其中包含指向入门教程中，cmdlet 参考文档和源代码代码和示例脚本的脚本资源的 WindowsAzure.com 门户
- [周末脚本专家： 开始使用 Azure 和 PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)。 在专用于 Windows PowerShell 博客中，此文章提供了使用 PowerShell for Azure 的管理功能的出色介绍。
- [安装和配置 Azure 跨平台命令行接口](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)。 关于 Azure 的脚本框架，适用于 Mac 和 Linux 以及 Windows 系统的入门教程。
- [下载 Azure Sdk 和工具主题的命令行工具部分](https://azure.microsoft.com/downloads/)。 有关文档和命令行工具与适用于 Azure 相关的下载门户页面。
- [使用 Azure 管理库和.NET 使一切自动化](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)。 Scott Hanselman 介绍了 Azure 的.NET 管理 API。
- [使用 Windows PowerShell 脚本发布到开发和测试环境](https://msdn.microsoft.com/library/azure/dn642480.aspx)。 说明如何使用的 MSDN 文档发布 Visual Studio 会自动生成用于 web 项目的脚本。
- [PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597)。 在 Visual Studio 中添加了对 Windows PowerShell 的语言支持的 visual Studio 扩展。

> [!div class="step-by-step"]
> [上一页](introduction.md)
> [下一页](source-control.md)
