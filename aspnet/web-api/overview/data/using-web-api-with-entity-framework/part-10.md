---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: 将应用发布到 Azure 的 Azure 应用服务 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: 66dde7b54ce084eed873afae56fd686d0dc8795f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37808222"
---
<a name="publish-the-app-to-azure-azure-app-service"></a>将应用发布到 Azure 的 Azure 应用服务
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](https://github.com/MikeWasson/BookService)

作为最后一个步骤中，您将发布到 Azure 应用程序。 在解决方案资源管理器，右键单击该项目并选择**发布**。

![](part-10/_static/image1.png)

单击**发布**调用**发布 Web**对话框。 如果您选中**在云中托管**时首次创建项目，然后连接并已配置设置。 在这种情况下，只需单击**设置**选项卡并选中&quot;执行 Code First 迁移&quot;。 (如果未选中**云中的主机**在开始时，然后按照中的步骤[下一节](#new-website)。)

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

若要将应用部署，请单击**发布**。 您可以查看中发布的进度**Web 发布活动**窗口。 (从**视图**菜单中，选择**其他 Windows**，然后选择**Web 发布活动**。)

![](part-10/_static/image4.png)

完成 Visual Studio 部署应用后，默认浏览器会自动打开指向已部署网站的 URL 和你创建的应用程序现在在云中运行。 浏览器地址栏中的 URL 显示正在从 Internet 加载该站点。

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a>部署到新网站

如果未选中**在云中托管**时首次创建项目时，您可以立即配置新的 web 应用。 在解决方案资源管理器，右键单击该项目并选择**发布**。 选择**配置文件**选项卡，单击**Microsoft Azure 网站**。 如果当前未登录到 Azure，系统会提示您登录。

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

在中**的现有网站**对话框中，单击**新建**。

![](part-10/_static/image9.png)

输入站点名称。 选择你的 Azure 订阅和区域。 下**数据库服务器**，选择**创建新的服务器**，或选择现有的服务器。 单击 **“创建”**。

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

单击**设置**选项卡并选中&quot;执行 Code First 迁移&quot;。 然后单击**发布**。

> [!div class="step-by-step"]
> [上一篇](part-9.md)
