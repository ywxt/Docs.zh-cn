---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: 源控件 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: aspnetcontent
ms.date: 06/23/2015
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: 045dc654057802be4ad96f5ecc3ed6c3d7a1ccb1
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823308"
---
<a name="source-control-building-real-world-cloud-apps-with-azure"></a>源代码管理 （使用 Azure 构建实际云应用）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关电子书的信息，请参阅[的第一章](introduction.md)。


源代码管理的所有云开发项目，而不仅仅是团队环境至关重要。 您不会将编辑源代码或甚至无需撤消的功能和自动备份和源代码管理的 Word 文档为您提供这些函数在项目级别，它们可以在其中保存时出现问题的更多时间。 使用云的源代码管理服务，不再需要担心复杂的设置，并可以使用最多 5 个用户免费的 Visual Studio Online 源代码管理。

这一章中的第一部分介绍了三个关键的最佳实践要时刻牢记：

- [自动化脚本视为源代码](#scripts)和版本以及应用程序代码对其。
- [中的机密永远不会检查](#secrets)（例如凭据的敏感数据） 到源代码存储库。
- [设置源分支](#devops)启用 DevOps 工作流。

本章的其余部分提供了 Visual Studio、 Azure 和 Visual Studio Online 中的这些模式的一些示例实现：

- [将脚本添加到 Visual Studio 中的源控件](#vsscripts)
- [在 Azure 中存储敏感数据](#appsettings)
- [在 Visual Studio 和 Visual Studio Online 中使用 Git](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a>自动化脚本视为源代码

当您在处理云项目时要频繁地更改内容，并且你想要能够快速响应客户报告的问题的能力。 快速响应，需使用自动化脚本中所述[使一切自动化](automate-everything.md)一章。 所有脚本用来创建你的环境，将部署到其规模，等等，需要与应用程序源代码保持同步。

若要使脚本与代码保持同步，请将其存储在源代码管理系统。 然后如果需要回滚更改或快速修复生产代码不同于开发代码，您无需浪费时间尝试跟踪哪些设置已更改或哪些团队成员具有所需的版本的副本。 也可以确保所需的脚本将与基本代码，你需要它们，您就可以保证所有团队成员都正在使用相同脚本保持同步。 然后你是否需要自动测试和部署到生产或新功能开发了修补，您必须为需要更新的代码正确的脚本。

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a>不签入机密

源代码存储库都太多的人，它为相应安全的位置的敏感数据，如密码通常可以访问。 如果脚本依赖于如密码的机密，参数化这些设置，以便它们不会保存在源代码中，并存储在其他地方的机密。

例如，Azure 可让您下载文件，其中包含发布设置以自动创建发布配置文件。 这些文件包括用户名和密码有权管理 Azure 服务。 如果您使用此方法来创建发布配置文件，并签入到源代码管理这些文件时，如果有权访问你的存储库的任何人都可以看到这些用户名和密码。 您可以安全地将密码存储在发布配置文件本身由于对其进行加密，它位于 *.pubxml 用户*默认情况下不包含在源代码管理中的文件。

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a>结构源分支，以便于 DevOps 工作流

如何在存储库中实现分支会影响开发新的功能和在生产环境中解决问题的能力。 此处是中等的大量大小的团队使用的模式：

![源分支结构](source-control/_static/image1.png)

主分支与在生产环境中的代码始终匹配。 在开发生命周期中，下方 master 分支对应于不同的阶段。 Development 分支是你在其中实施新功能。 对于小团队可能只有 master 和开发，但我们通常建议的人员具有开发和主机之间过渡分支。 对于最终集成测试更新移到生产环境之前，可以使用过渡环境。

对于较大的团队可能有不同的分支的每个新功能;对于较小的团队可能必须所有人签入到 development 分支。

如果必须为每个功能，分支功能启用时一个准备好你合并其源代码更改向上到开发分支和其他功能分支到向下。 此合并过程的源代码会非常耗时，并且若要避免该工作的同时仍将功能分开，一些团队实现名为一种替代方法*[功能切换](http://en.wikipedia.org/wiki/Feature_toggle)* （也称为*功能标志*)。 这意味着所有的所有功能的代码都在同一个分支，但启用或禁用每个功能在代码中使用的开关。 例如，假设一个功能是修复其应用程序任务，新的字段，并功能 B 添加缓存功能。 这两项功能的代码可以是开发分支中，但应用程序将仅显示新字段时变量设置为 true，并且它将仅使用缓存时不同的变量设置为 true。 如果功能 A 还未准备好进行升级，但功能 B 是准备就绪，可以升级到生产环境使用功能 A 开关设置为 off 的代码的所有和功能 B 切换。 然后，可以完成功能 A，并将其提升更高版本，所有与任何源的代码合并。

指示使用分支或切换功能，如下一个分支结构，可采用敏捷且可重复的方式流动开发到生产环境中的代码。

此结构还可以快速响应客户反馈。 如果您需要进行快速修复到生产环境，您还可以执行的有效地采用灵活的方式。 可以创建从 master 或暂存，一个分支和何时可以将其合并到主分支合并向上和向下为开发和功能分支。

![修补程序分支](source-control/_static/image2.png)

没有此类具有其单独的生产和开发分支的分支结构，生产问题可能使您无需提升新功能代码，以及您生产的修复程序的位置中。 新的功能代码可能不是经过充分测试和准备好进行生产，您可能需要做大量工作正在放弃未准备好的更改。 或者，可能需要延迟以测试更改，并使其准备好部署您的修复程序。

接下来你将看到如何在 Visual Studio、 Azure 和 Visual Studio Online 中实现以下三种模式的示例。 这些是示例而不是详细的分步说明-将执行操作的 it 说明;提供所有必需的上下文的详细说明，请参阅[资源](#resources)本章末尾部分。

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a>将脚本添加到 Visual Studio 中的源控件

通过包括在 Visual Studio 解决方案文件夹中 （假设你的项目在源代码管理中），可以将脚本添加到 Visual Studio 中的源控件。 下面是一种方法执行此操作。

在你的解决方案文件夹中创建的脚本的文件夹 (具有的相同文件夹你 *.sln*文件)。

![自动化文件夹](source-control/_static/image3.png)

将脚本文件复制到的文件夹。

![自动化文件夹内容](source-control/_static/image4.png)

在 Visual Studio 中，将添加到项目的解决方案文件夹。

![新解决方案文件夹菜单选项](source-control/_static/image5.png)

并将脚本文件添加到解决方案文件夹。

![添加现有项菜单选项](source-control/_static/image6.png)

![“添加现有项”对话框](source-control/_static/image7.png)

你的项目中现在包含脚本文件和源控件正在跟踪其版本更改随相应的源代码更改。

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a>在 Azure 中存储敏感数据

如果在 Azure 网站中运行你的应用程序，避免将凭据存储在源代码管理中的一种方法是将其存储在 Azure 中。

例如，修复其应用程序将存储在其 Web.config 文件两个连接字符串会在生产环境和密钥，你的 Azure 存储帐户可以访问的密码。

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

如果实际的生产中的这些设置的值将放在*Web.config*文件，或如果将其放在*Web.Release.config*文件来配置一个 Web.config 转换，以便将它们插入在部署期间，将源存储库中存储它们。 如果数据库连接字符串输入到生产环境发布配置文件，密码将在你 *.pubxml*文件。 (你无法排除 *.pubxml*文件从源代码管理，但这样会失去共享所有其他部署设置的权益。)

Azure 为你提供的备用**appSettings**和连接字符串的部分*Web.config*文件。 下面是相关部分**配置**Azure 管理门户中的 web 站点的选项卡：

![appSettings 和门户中的 connectionstrings 节](source-control/_static/image8.png)

在一个项目部署到此网站和应用程序运行时，已在 Azure 中存储任何值将覆盖 Web.config 文件中的任何有效值。

通过使用管理门户或脚本，可以在 Azure 中设置这些值。 在中看到的环境创建自动化脚本[使一切自动化](automate-everything.md)章创建 Azure SQL 数据库、 获取的存储和 SQL 数据库连接字符串，并将这些机密存储在您的网站的设置。

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

请注意，以便不获取实际值保存到源存储库参数化脚本。

当您在开发环境中本地运行时，应用读取您本地的 Web.config 文件和你的连接字符串指向 LocalDB SQL Server 数据库中*应用程序\_数据*web 项目的文件夹。 在 Azure 中运行应用并应用将尝试从 Web.config 文件中读取这些值，它将获取并使用时，对于网站，不是在 Web.config 文件中存储的值。

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-visual-studio-online"></a>在 Visual Studio 和 Visual Studio Online 中使用 Git

可以使用任何源代码管理环境实现前面提供的 DevOps 分支结构。 为分布式团队[分布式版本控制系统](http://en.wikipedia.org/wiki/Distributed_revision_control)(DVCS) 可以达到最佳效果; 对于其他团队[集中式系统](http://en.wikipedia.org/wiki/Revision_control)可能更好地工作。

[Git](http://git-scm.com/)是 DVCS 变得非常受欢迎。 当您使用 Git 进行源代码管理时，你在本地计算机上具有其历史记录的所有存储库的完整副本。 很多人喜欢，因为更容易以继续工作时不连接到网络，可以继续执行提交和回滚、 创建和切换分支，等等。 即使您正在连接到网络，它是更轻松、 更快创建分支和切换分支时所有内容都是本地。 此外可以执行本地提交和回滚操作不会影响对其他开发人员。 你可以执行批处理提交之前将它们发送到服务器。

[Microsoft Visual Studio Online](https://www.visualstudio.com/)(VSO) 以前称为 Team Foundation Service 提供了这两个 Git 和[Team Foundation 版本控制](https://msdn.microsoft.com/library/ms181237(v=vs.120).aspx)(TFVC; 集中式源代码管理)。 此处在 Microsoft Azure 的组中有些团队使用集中式的源控件，分布式的一些使用和一些使用混合 （对于某些项目集中式和分布式其他项目）。 VSO 服务是免费的最多 5 个用户。 你可以注册一个免费计划[此处](https://go.microsoft.com/fwlink/?LinkId=307137)。

Visual Studio 2013 包括内置一流[Git 支持](https://msdn.microsoft.com/library/hh850437.aspx); 下面是一个快速的工作原理的演示。

在 Visual Studio 2013 中打开项目，右键单击该解决方案中的**解决方案资源管理器**，然后选择**将解决方案添加到源代码管理**。

![将解决方案添加到源代码管理](source-control/_static/image9.png)

Visual Studio 会询问你是否想要使用 TFVC （集中式的版本控制） 或 Git。

![选择源代码管理](source-control/_static/image10.png)

当您选择 Git，然后单击**确定**，Visual Studio 在你的解决方案文件夹中创建新的本地 Git 存储库。 新的存储库有任何文件尚未;必须将它们添加到存储库中，通过执行操作的 Git 提交。 右键单击该解决方案中的**解决方案资源管理器**，然后单击**提交**。

![提交](source-control/_static/image11.png)

Visual Studio 自动暂存所有提交的项目文件，并列出它们**团队资源管理器**中**包含的更改**窗格。 (如果有一些不想包括到提交中，您可以选择它们，右键单击，然后单击**排除**。)

![Team Explorer](source-control/_static/image12.png)

输入提交注释，然后单击**提交**，和 Visual Studio 执行提交，并显示提交 id。

![团队资源管理器更改](source-control/_static/image13.png)

现在如果您更改一些代码，以便不同于什么是存储库中，可以轻松地查看的差异。 右键单击你已更改的文件选择**Unmodified 与比较**，并获取比较显示它显示在未提交的更改。

![与未修改进行比较](source-control/_static/image14.png)

![显示更改的差异](source-control/_static/image15.png)

你可以轻松看到哪些更改需要做找出和签入。

假设您需要进行分支 – 你可以也可以这样做，Visual Studio 中。 在中**团队资源管理器**，单击**新分支**。

![团队资源管理器中新的分支](source-control/_static/image16.png)

输入分支名称，单击**创建分支**，并且选中**签出分支**，Visual Studio 会自动签出新分支。

![团队资源管理器中新的分支](source-control/_static/image17.png)

现在可以对文件进行更改并签入到此分支。 您可以轻松地切换分支和 Visual Studio 之间自动同步到者为准分支文件已经签出。在此示例中 web 页标题中 *\_Layout.cshtml*已更改为"热修复补丁程序 1"中 HotFix1 分支。

![Hotfix1 分支](source-control/_static/image18.png)

如果切换回主分支的内容 *\_Layout.cshtml*文件自动还原到所在的主分支中。

![主分支](source-control/_static/image19.png)

此方式可以快速创建分支和分支之间来回切换的一个简单示例。 此功能使使用分支结构的高度灵活的工作流和自动化脚本中提供[使一切自动化](automate-everything.md)一章。 例如，可以是开发分支中工作，创建热修复补丁程序从 master 分支，切换到新分支，在那里进行更改和提交，然后切换回开发分支并继续之前进行的操作。

你已了解了如何使用 Visual Studio 中的本地 Git 存储库。 在团队环境中你通常还将更改推送到的公共储存库。 Visual Studio 工具还可使其指向远程 Git 存储库。 可以使用 GitHub.com 实现此目的，也可以使用[Visual Studio Online 中的 Git](https://msdn.microsoft.com/library/hh850437.aspx)与所有其他 Visual Studio Online 功能，例如工作项和 bug 跟踪集成在一起。

这不是您可以实现敏捷的分支策略，当然的唯一方法。 您可以使用集中式的源控件存储库相同的敏捷工作流。

## <a name="summary"></a>总结

度量值基于多快的速度可以进行更改，并获取实时安全且可预测方式在源代码管理系统成功。 如果你发现自己被困难所吓倒，因为您只需一天或两个手动测试对其进行更改，您可能会问自己您需要做 process-wise 或 test-wise，以便可以使所做的更改，以分钟为单位，或在最差不再比一小时。 执行该操作的一种策略是实现持续集成和持续交付，我们将在中介绍[接下来的章节](continuous-integration-and-continuous-delivery.md)。

<a id="resources"></a>
## <a name="resources"></a>资源

[Visual Studio Online](https://www.visualstudio.com/)门户提供了文档和支持服务，并且你可以注册一个帐户。 如果您有 Visual Studio 2012，并且想要使用 Git，请参阅[Visual Studio Tools for Git](https://visualstudiogallery.msdn.microsoft.com/abafc7d6-dcaa-40f4-8a5e-d6724bdb980c)。

有关 TFVC （集中式的版本控制） 和 Git （分布式的版本控制） 的详细信息，请参阅以下资源：

- [应使用哪个版本控制系统： TFVC 或 Git？](https://msdn.microsoft.com/library/vstudio/ms181368.aspx#tfvc_or_git_summary) MSDN 文档，包括汇总 TFVC 和 Git 之间的差异的表。
- [嗯，我喜欢 Team Foundation Server 和我喜欢 Git，但这是更好？](https://blogs.msdn.com/b/visualstudiouk/archive/2013/08/05/well-i-like-team-foundation-server-and-i-like-git-but-which-is-better.aspx) Git 和 TFVC 的比较。

有关分支策略的详细信息，请参阅以下资源：

- [构建发布管道与 Team Foundation Server 2012](https://msdn.microsoft.com/library/dn449957.aspx)。 Microsoft 模式和实践文档。 请参阅有关的分支策略讨论第 6 章。 提倡者功能通过功能分支切换，如果使用功能分支，提倡保持其生存期较短 （小时或天至多）。
- [版本控制指南](https://aka.ms/vsarsolutions)。 通过 ALM Rangers 指南分支策略。 在下载选项卡上，请参阅分支 Strategies.pdf。
- [使用功能切换进行软件开发](https://msdn.microsoft.com/magazine/dn683796.aspx)。 MSDN 杂志 》 一文。
- [功能切换](http://martinfowler.com/bliki/FeatureToggle.html)。 功能简介切换/Martin Fowler 的博客上的功能标志。
- [功能切换与功能分支](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx)。 有关功能切换，由 Dylan Smith 的另一博客文章。

有关如何处理不应保留在源代码管理存储库中的敏感信息的详细信息，请参阅以下资源：

- [有关密码和其他敏感数据部署到 ASP.NET 和 Azure 应用服务最佳实践](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。
- [Azure 网站： 如何应用程序字符串和连接字符串的工作](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)。 介绍了重写的 Azure 功能`appSettings`并`connectionStrings`中的数据*Web.config*文件。
- [自定义配置和应用程序设置在 Azure 网站-和 Stefan schackow 一起](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/)。

有关保留源代码管理中的敏感信息的其他方法的信息，请参阅[ASP.NET MVC： 外出时的源代码管理中保留专用设置](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)。

> [!div class="step-by-step"]
> [上一页](automate-everything.md)
> [下一页](continuous-integration-and-continuous-delivery.md)
