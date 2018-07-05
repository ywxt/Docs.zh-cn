---
uid: web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
title: 使用 Visual Studio 的 ASP.NET Web 部署： 设置文件夹权限 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 9715a121-fa55-4f1b-a5d2-fb3f6cd8be8f
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
msc.type: authoredcontent
ms.openlocfilehash: a0c4f9f7cf30c1fc6a06c2cf798dc7ed04585504
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37383644"
---
<a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a>使用 Visual Studio 的 ASP.NET Web 部署： 设置文件夹权限
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 或 Visual Studio 2010。 有关序列的信息，请参阅[系列中的第一个教程](introduction.md)。


## <a name="overview"></a>概述

在本教程中，设置文件夹的权限*Elmah*文件夹中已部署的 web 站点，以便应用程序可以在该文件夹中创建日志文件。

在 Visual Studio 中使用 Visual Studio 开发服务器 (Cassini) 或 IIS Express 测试 web 应用程序时，应用程序在你的身份下运行。 在开发计算机上最有可能是管理员并具有完整权限对任何文件夹中的任何文件执行任何操作。 但在 IIS 下运行应用程序，它将运行下定义为站点分配给应用程序池的标识。 这通常是具有有限的权限的系统定义的帐户。 默认情况下它具有读取和执行权限，对 web 应用程序的文件和文件夹，但它没有写访问权限。

如果你的应用程序创建或更新文件，这是一种常见需要在 web 应用程序中，这将成为一个问题。 在 Contoso 大学应用程序，Elmah 将创建 XML 文件中的*Elmah*文件夹，以便保存有关错误的详细信息。 即使不使用类似于 Elmah 的内容，你的站点可能会让用户将文件上传或执行其他任务将数据写入到你网站的文件夹中。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](troubleshooting.md)。

## <a name="test-error-logging-and-reporting"></a>测试错误日志记录和报告

若要查看如何应用程序不能正常工作在 IIS 中 （尽管它未在 Visual Studio 中测试时），可能会导致一个错误，通常会由 Elmah 记录，然后打开 Elmah 错误日志，以查看详细信息。 如果 Elmah 不能创建一个 XML 文件和存储的错误详细信息，您将看到一个空的错误报告。

打开浏览器并转到`http://localhost/ContosoUniversity`，然后请求无效的 URL，如*Studentsxxx.aspx*。 请参阅而不是系统生成的错误页面*GenericErrorPage.aspx*页，因为`customErrors`Web.config 文件中的设置为"RemoteOnly"并本地运行 IIS:

![HTTP 404 错误页面](setting-folder-permissions/_static/image1.png)

现在，运行*Elmah.axd*以查看错误报告。 使用管理员帐户凭据登录之后 (&quot;管理员&quot;并&quot;devpwd&quot;)，因为 Elmah 无法创建 XML 文件中的，您会看到一个空错误日志页面*Elmah*文件夹：

![错误日志为空](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a>Elmah 文件夹上设置的写入权限

可以手动设置文件夹权限，或使其自动部署过程的一部分。 使其自动需要复杂的 MSBuild 代码，以及由于仅需要执行此操作，第一次部署，以下的步骤如何手动执行该操作。 (有关如何使部署过程的此部分的信息，请参阅[设置文件夹权限 Web 发布](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)Sayed Hashimi 的博客上。)

1. 在中**文件资源管理器**，导航到*C:\inetpub\wwwroot\ContosoUniversity*。 右键单击*Elmah*文件夹，选择**属性**，然后选择**安全**选项卡。
2. 单击“编辑” 。
3. 在中**Elmah 的权限**对话框中，选择**DefaultAppPool**，然后选择**编写**中的复选框**允许**列。

    ![ELMAH 文件夹的权限](setting-folder-permissions/_static/image3.png)

    (如果看不到**DefaultAppPool**中**组或用户名**列表中，您大概是用一个指定在本教程中的其他某种方法在您的计算机上设置了 IIS 和 ASP.NET 4。 在这种情况下，找出哪些标识由分配给 Contoso 大学应用程序，并向该标识授予写入权限的应用程序池。 请参阅有关应用程序池标识链接在本教程末尾。）单击**确定**中这两个对话框。

## <a name="retest-error-logging-and-reporting"></a>重新测试错误日志记录和报告

通过再次导致错误 （请求错误 URL） 的相同方式来测试和运行**错误日志**页。 这一次在页面上会出现错误。

![ELMAH 错误日志页](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a>总结

您现在已经完成全部的 Contoso University 所需的任务在 IIS 中正常运行在本地计算机上。 在下一步的教程中，将在站点公开用于通过将其部署到 Azure。

## <a name="more-information"></a>详细信息

在此示例中，Elmah 为何无法保存日志文件的原因是相当明显。 可以在不那么明显; 问题原因的情况下使用 IIS 跟踪请参阅[故障排除失败的请求使用跟踪在 IIS 7 中](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)IIS.net 站点上。

有关如何向应用程序池标识授予权限的详细信息，请参阅[应用程序池标识](https://www.iis.net/learn/manage/configuring-security/application-pool-identities)并[在文件系统 Acl 通过 IIS 安全内容](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls)IIS.net 站点上。

> [!div class="step-by-step"]
> [上一页](deploying-to-iis.md)
> [下一页](deploying-to-production.md)
