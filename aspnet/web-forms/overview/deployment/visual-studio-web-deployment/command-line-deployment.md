---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 使用 Visual Studio 的 ASP.NET Web 部署： 命令行部署 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 9b2832dd23f68f9283983b52a85e8a9d5f85fd2f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831848"
---
<a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a>使用 Visual Studio 的 ASP.NET Web 部署： 命令行部署
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 或 Visual Studio 2010。 有关序列的信息，请参阅[系列中的第一个教程](introduction.md)。


## <a name="overview"></a>概述

本教程演示如何调用 Visual Studio web 发布管道从命令行。 这可用于方案，即向[自动执行部署过程](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)而不手动完成 Visual Studio 中，通常通过使用[源代码版本控制系统](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)。

## <a name="make-a-change-to-deploy"></a>若要部署更改

当前关于页面显示的模板代码。

![有关使用模板代码页](command-line-deployment/_static/image1.png)

您将替换为用于显示摘要学生注册代码。

打开*About.aspx*页上，删除所有标记内`MainContent``Content`元素，并插入其原位置中的以下标记：

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

运行该项目并选择**有关**页。

![“关于”页面](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a>通过使用命令行部署到测试

您不会部署另一个数据库更改，因此禁用 dbDacFx 数据库部署为 aspnet ContosoUniversity 数据库。 打开**发布 Web**向导，以及在这三个发布配置文件，清除**更新数据库**上的复选框**设置**选项卡。

在 Windows 8 启动页上，搜索**VS2012 的开发人员命令提示**。

右键单击图标**VS2012 的开发人员命令提示**然后单击**以管理员身份运行**。

输入以下命令在命令提示符下，解决方案文件的路径替换为您的解决方案文件的路径：

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

MSBuild 生成解决方案，并将其部署到测试环境。

![命令行输出](command-line-deployment/_static/image3.png)

打开浏览器并转到`http://localhost/ContosoUniversity`，然后单击**有关**页以验证部署是否成功。

如果在测试中尚未创建任何学生，则会看到下的一个空白页面**学生正文统计信息**标题。 转到**学生**页上，单击**添加学生**，并添加一些学生，并返回到**有关**页以查看学生统计信息。

![有关在测试环境中的页面](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a>密钥的命令行选项

您输入的命令传递到 MSBuild 解决方案文件路径和两个属性：

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a>部署与部署的各个项目的解决方案

指定解决方案文件中要生成该解决方案将导致所有项目。 如果解决方案中有多个 web 项目，以下 MSBuild 行为适用：

- 在命令行指定的属性将传递给每个项目。 因此，每个 web 项目必须具有与你指定的名称的发布配置文件。 如果指定`/p:PublishProfile=Test`，每个 web 项目必须具有名为的发布配置文件*测试*。
- 甚至不会生成另一个时，您可能已成功发布一个项目。 有关详细信息，请参阅 stackoverflow 线程[MSBuild 失败，出现两个包](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)。

如果指定单个项目而不是一种解决方案，您必须添加一个参数，指定 Visual Studio 的版本。 如果你正在使用 Visual Studio 2012 命令行应类似于下面的示例：

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

Visual Studio 2010 版本的版本号是 10.0。 有关详细信息，请参阅[Visual Studio 项目兼容性和 VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) Sayed Hashimi 的博客上。

### <a name="specifying-the-publish-profile"></a>指定发布配置文件

按名称或完整路径，可以指定发布配置文件 *.pubxml*文件，在下面的示例所示：

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a>Web 发布所支持的命令行发布方法

三个发布方法支持用于命令行发布：

- `MSDeploy` -使用 Web 部署发布。
- `Package` -通过创建 Web 部署包发布。 您必须单独安装包，从创建它的 MSBuild 命令。
- `FileSystem` -通过将文件复制到指定的文件夹来发布。

### <a name="specifying-the-build-configuration-and-platform"></a>指定生成配置和平台

在 Visual Studio 或命令行上，必须设置生成配置和平台。 发布配置文件还包括命名的属性`LastUsedBuildConfiguration`和`LastUsedPlatform`，但不能设置这些属性以确定如何生成该项目。 有关详细信息，请参阅[MSBuild： 如何设置配置属性](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)Sayed Hashimi 的博客上。

## <a name="deploy-to-staging"></a>部署到过渡环境

若要部署到 Azure，必须将密码添加到命令行中。 如果您在 Visual Studio 中发布配置文件中保存了密码，它存储在加密表单中您 *.pubxml 用户*文件。 当进行命令行部署，因此您必须在密码命令行参数中传递时，MSBuild 不访问该文件。

1. 复制从所需的密码 *.publishsettings*前面为过渡网站下载的文件。 密码为的值`userPWD`属性用于 Web 部署`publishProfile`元素。

    ![Web 部署密码](command-line-deployment/_static/image5.png)
2. 在 Windows 8 启动页上，搜索**VS2012 的开发人员命令提示**，并单击图标以打开命令提示符。 （您无需打开它以管理员身份这一次因为你不部署到 IIS 在本地计算机上。）
3. 输入以下命令在命令提示符下，解决方案文件的路径替换为您的解决方案文件并将密码与你的密码的路径：

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    请注意，此命令行包含一个额外的参数： `/p:AllowUntrustedCertificate=true`。 本教程是在编写，`AllowUntrustedCertificate`时从命令行发布到 Azure，必须设置属性。 当发布此 bug 的修复程序后时，你不需要该参数。
4. 打开浏览器并转到将过渡站点的 URL，然后单击**有关**页以验证部署是否成功。

    如上文针对测试环境中，您可能需要创建一些学生上查看统计信息**有关**页。

## <a name="deploy-to-production"></a>部署到生产环境

部署到生产环境的过程是类似于过渡的过程。

1. 复制从所需的密码 *.publishsettings*前面为生产 web 站点下载的文件。
2. 打开**VS2012 的开发人员命令提示**。
3. 输入以下命令在命令提示符下，解决方案文件的路径替换为您的解决方案文件并将密码与你的密码的路径：

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    对于实际的生产站点，如果还没有数据库更改，通常复制*应用程序\_offline.htm*到部署之前站点文件，并成功部署后将其删除。
4. 打开浏览器并转到将过渡站点的 URL，然后单击**有关**页以验证部署是否成功。

## <a name="summary"></a>总结

现已通过使用命令行部署应用程序更新。

![有关在测试环境中的页面](command-line-deployment/_static/image6.png)

在下一步的教程中，你将看到举例说明如何扩展 web 发布管道。 该示例将演示如何部署项目中不包含的文件。

> [!div class="step-by-step"]
> [上一页](deploying-a-database-update.md)
> [下一页](deploying-extra-files.md)
