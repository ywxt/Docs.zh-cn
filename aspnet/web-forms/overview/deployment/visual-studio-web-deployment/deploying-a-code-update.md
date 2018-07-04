---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 使用 Visual Studio 的 ASP.NET Web 部署： 部署代码更新 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3649f0250e830b76c42d832e51038c2c52ed4561
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368209"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a>使用 Visual Studio 的 ASP.NET Web 部署： 部署代码更新
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 或 Visual Studio 2010。 有关序列的信息，请参阅[系列中的第一个教程](introduction.md)。


## <a name="overview"></a>概述

在初始部署后持续维护和开发您的网站的工作，并在长时间之前你将想要将更新部署。 本教程将指导你完成更新部署到应用程序代码的过程。 实现和部署本教程中的更新不涉及数据库更改;您将看到有关部署下一教程中的数据库更改的差异。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](troubleshooting.md)。

## <a name="make-a-code-change"></a>进行代码更改

作为对应用程序更新的简单示例，你将添加到**讲师**页由所选讲师的课程列表。

如果在运行**讲师**页上，您会注意到，有**选择**链接在网格中，但他们不使以外的任何行背景变灰。

![选择讲师页](deploying-a-code-update/_static/image1.png)

现在，你将添加代码运行时**选择**链接单击，并显示由所选讲师的课程列表。

1. 在中*Instructors.aspx*，添加以下标记后立即**ErrorMessageLabel** `Label`控件：

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. 运行该页并选择讲师。 请参阅由讲师讲授的课程列表。

    ![使用教授的课程讲师页](deploying-a-code-update/_static/image2.png)
3. 关闭浏览器。

## <a name="deploy-the-code-update-to-the-test-environment"></a>将代码更新部署到测试环境

可以使用发布配置文件将部署到测试、 过渡和生产环境之前，需要更改数据库的发布选项。 不再需要运行成员资格数据库的授权和数据部署脚本。

1. 打开**发布 Web**右键单击 ContosoUniversity 项目并单击向导**发布**。
2. 单击**测试**分析中的**配置文件**下拉列表。
3. 单击**设置**选项卡。
4. 下**DefaultConnection**中**数据库**部分中，清除**更新数据库**复选框。
5. 单击**配置文件**选项卡，然后依次**过渡**分析中的**配置文件**下拉列表。
6. 当系统询问你是否想要保存所做的更改**测试**配置文件中，单击**是**。
7. 临时配置文件中进行相同的更改。
8. 重复该过程以在生产配置文件中进行相同的更改。
9. 关闭**发布 Web**向导。

部署到测试环境是现在只需运行一次单击即可重新发布。 若要使此过程更快，可以使用**Web 单键发布**工具栏。

1. 在中**视图**菜单中，选择**工具栏**，然后选择**Web 单键发布**。

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. 在中**解决方案资源管理器**，选择 ContosoUniversity 项目。
3. **Web 单键发布**工具栏上，选择**测试**发布配置文件，然后单击**发布 Web** （其箭头指向左侧和右侧的图标）。

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. Visual Studio 部署更新的应用程序，并在主页上会自动打开浏览器。
5. 运行讲师页并选择一名讲师，若要验证已成功部署更新。

通常会同样进行回归测试 （也就是说，测试以确保新的更改不会破坏任何现有功能的站点的其余部分）。 但对于本教程将跳过该步骤并继续将更新部署到过渡和生产。

时重新部署，Web 部署自动确定哪些文件已更改，并仅将更改为服务器的文件。 默认情况下，Web 部署使用上次更改日期的文件以确定哪些已更改。 某些源代码管理系统文件更改日期甚至时不要更改该文件的内容。 在这种情况下，你可能想要配置 Web 部署可以使用文件校验和来确定哪些文件已更改。 有关详细信息，请参阅[为何执行操作的所有文件重新部署虽然我没有改变它们？](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) ASP.NET 部署常见问题解答中。

## <a name="take-the-application-offline-during-deployment"></a>使应用程序脱机部署过程

要部署的更改现在是单个页面的简单更改。 但有时您部署较大的更改，或部署代码和数据库更改，以及站点可能会出现错误的行为之前部署完成后，用户请求页面时。 若要防止用户访问站点，在进行部署时，可以使用*应用程序\_offline.htm*文件。 当将名为的文件*应用程序\_offline.htm*在你的应用程序的根文件夹中，IIS 会自动显示该文件而不是运行你的应用程序。 因此为了防止访问在部署期间，您将放*应用程序\_offline.htm*根文件夹中运行部署过程中，，然后删除*应用\_offline.htm*后成功部署。

你可以配置 Web 部署以将默认值自动*应用程序\_offline.htm*启动部署时在服务器上的文件并将在它完成后将其删除。 若要执行所有您只需是下面的 XML 元素添加到发布配置文件 (.pubxml) 文件：

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

对于本教程中，您将看到如何创建和使用自定义*应用程序\_offline.htm*文件。

使用*应用程序\_offline.htm*暂存网站中不是必需的因为你没有访问暂存站点的用户。 但最好使用暂存所有内容测试你计划在生产环境中部署的方式。

### <a name="create-appofflinehtm"></a>创建应用\_offline.htm

1. 在中**解决方案资源管理器**，右键单击该解决方案，然后单击**添加**，然后单击**新项**。
2. 创建**HTML 页面**名为*应用\_offline.htm* (在删除最后一个"l" *.html*扩展 Visual Studio 将创建默认情况下)。
3. 模板标记替换为以下标记：

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. 保存并关闭文件。

### <a name="copy-appofflinehtm-to-the-root-folder-of-the-web-site"></a>复制应用\_offline.htm web 站点的根文件夹

可以使用任何 FTP 工具将文件复制到该网站。 [FileZilla](http://filezilla-project.org/)是 FTP 工具和屏幕截图中所示。

若要使用 FTP 工具，需要以下三项： FTP URL、 用户名和密码。

URL 显示在网站的仪表板页上，在 Azure 管理门户中，并可以中找到用户名和密码 FTP *.publishsettings*前面下载的文件。 以下步骤演示如何获取这些值。

1. 在 Azure 管理门户中，单击**网站**选项卡，然后单击过渡 web 站点。
2. 上**仪表板**页上，向下滚动到的 FTP 主机名中查找**速览**部分。

    ![FTP 主机名](deploying-a-code-update/_static/image5.png)
3. 打开暂存 *.publishsettings*在记事本或其他文本编辑器中的文件。
4. 查找`publishProfile`FTP 配置文件的元素。
5. 复制`userName`和`userPWD`值。

    ![FTP 凭据](deploying-a-code-update/_static/image6.png)
6. 打开你的 FTP 工具和登录到 FTP URL。
7. 复制*应用程序\_offline.htm*到解决方案文件夹从 */site/wwwroot*过渡站点中的文件夹。

    ![复制 app_offline](deploying-a-code-update/_static/image7.png)
8. 浏览到将过渡站点的 URL。 可以看到*应用程序\_offline.htm*页现在显示而不是您的主页。

    ![在浏览器窗口 app_offline.htm](deploying-a-code-update/_static/image8.png)

现在你现可部署到过渡环境。

## <a name="deploy-the-code-update-to-staging-and-production"></a>将代码更新部署到过渡和生产

1. 在中**Web 单键发布**工具栏上，选择**过渡**发布配置文件，然后单击**发布 Web**。

    Visual Studio 部署更新的应用程序和网站的主页上浏览器中打开。 *应用程序\_offline.htm*显示文件。 您可以对其进行测试以验证是否成功的部署之前，必须删除*应用程序\_offline.htm*文件。
2. 返回到您的 FTP 工具，并删除**应用程序\_offline.htm**从过渡站点。
3. 在浏览器中的临时站点，打开讲师页并选择讲师来验证已成功部署更新。
4. 相同的步骤用于生产之前用于过渡。

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a>查看更改和部署特定的文件

Visual Studio 2012 还提供了部署单独的文件的能力。 所选文件可以查看本地版本和已部署的版本之间的差异、 将文件部署到目标环境中，或从目标环境将文件复制到本地项目。 在本教程的本部分中，您将看到如何使用这些功能。

### <a name="make-a-change-to-deploy"></a>若要部署更改

1. 打开*Content/Site.css*，并查找的块`body`标记。
2. 更改的值`background-color`从`#fff`到`darkblue`。

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a>在发布预览窗口中查看更改

当你使用**发布 Web**向导以发布该项目，您可以看到更改要发布的中双击该文件**预览**窗口。

1. 右键单击 ContosoUniversity 项目，然后单击**发布**。
2. 从**配置文件**下拉列表中，选择**测试**发布配置文件。
3. 单击**预览版**，然后单击**开始预览**。
4. 在中**预览版**窗格中，双击**Site.css**。

    ![双击 Site.css](deploying-a-code-update/_static/image9.png)

    **预览更改**对话框显示的更改将在其中部署预览。

    ![对 Site.css 预览更改](deploying-a-code-update/_static/image10.png)

    如果您双击*Web.config*文件中，**预览更改**对话框显示了生成的效果配置转换和发布配置文件转换。 此时你尚未这样做会导致的任何内容*Web.config*若要更改，因此您会不看到任何更改在服务器上的文件。 但是，**预览更改**窗口错误地显示了两项更改。 看起来，将删除两个 XML 元素。 当您选择，发布过程会添加这些元素**执行 Code First 迁移应用程序启动**Code First 的上下文类。 发布过程添加这些元素，因此看起来，尽管它们不会删除要被删除之前进行比较。 将在将来的版本中更正此错误。
5. 单击 **“关闭”**。
6. 单击“发布” 。
7. 当浏览器打开到测试站点的主页上时，按 CTRL + F5 来硬刷新才能看到 CSS 更改的效果。

    ![CSS 更改的效果](deploying-a-code-update/_static/image11.png)
8. 关闭浏览器。

### <a name="publish-specific-files-from-solution-explorer"></a>发布解决方案资源管理器中的特定文件

假设不喜欢蓝色背景，并想要恢复为原始的颜色。 在本部分中，您将恢复原始设置通过直接从特定文件发布**解决方案资源管理器**。

1. 打开*Content/Site.css*和还原`background-color`设置为`#fff`。
2. 在中**解决方案资源管理器**，右键单击*Content/Site.css*文件。

    上下文菜单显示了三个发布选项。

    ![发布解决方案资源管理器选项](deploying-a-code-update/_static/image12.png)
3. 单击**预览更改为 Site.css**。

    窗口将打开以显示目标环境中的本地文件和它的版本之间的差异。

    ![Diff-Content/Site.css](deploying-a-code-update/_static/image13.png)
4. 在中**解决方案资源管理器**，右键单击**Site.css**再次单击**发布 Site.css**。

    **Web 发布活动**窗口将显示已发布文件。

    ![Web 发布活动窗口](deploying-a-code-update/_static/image14.png)
5. 浏览器中打开`http://localhost/contosouniversity`URL，然后按 CTRL + F5 来导致一种较难刷新才能查看更改的 CSS 的效果。

    ![使用普通 CSS 的主页](deploying-a-code-update/_static/image15.png)
6. 关闭浏览器。

## <a name="summary"></a>总结

现在，已了解多种方式来部署应用程序更新不涉及数据库更改，并已了解如何预览更改后，若要验证，将更新的内容是你期望的内容。 讲师页现在具有**讲授课程**部分。

![使用教授的课程讲师页](deploying-a-code-update/_static/image16.png)

下一步的教程演示如何部署数据库更改： 将将 birthdate 字段添加到数据库和讲师页。

> [!div class="step-by-step"]
> [上一页](deploying-to-production.md)
> [下一页](deploying-a-database-update.md)
