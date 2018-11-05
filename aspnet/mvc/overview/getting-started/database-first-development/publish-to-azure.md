---
uid: mvc/overview/getting-started/database-first-development/publish-to-azure
title: 将 MVC 数据库第一个站点发布到 Azure |Microsoft Docs
author: Rick-Anderson
description: 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 此教程系列...
ms.author: riande
ms.date: 12/22/2014
ms.assetid: 7131f1c1-cef3-4396-ab44-ed4519676546
msc.legacyurl: /mvc/overview/getting-started/database-first-development/publish-to-azure
msc.type: authoredcontent
ms.openlocfilehash: 1d2c26c211c5c8d97076327d01fe59d5ba4dc9ac
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021623"
---
<a name="publish-mvc-database-first-site-to-azure"></a>将 MVC 数据库第一个站点发布到 Azure
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。 生成的代码对应于数据库表中的列。
> 
> 本系列的此部分重点介绍将 web 应用和数据库发布到 Azure。 可以阅读本主题，了解如何发布 web 应用和数据库，但实际执行的步骤必须在本教程开始启动。 请参阅[入门](setting-up-database.md)。


## <a name="deploy-your-web-app-on-azure"></a>在 Azure 上的将 web 应用部署

需要一个 Azure 帐户才能完成本教程中：

- 你可以[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)-获取信用额度可用于试用付费版 Azure 服务，甚至在用之后最多可以保留帐户并使用免费的 Azure 服务。
- 你可以[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)-MSDN 订阅提供信用额度可以用于付费版 Azure 服务的每个月。

若要将 web 应用发布，右键单击该项目并选择**发布**。

![发布站点](publish-to-azure/_static/image1.png)

选择 Microsoft Azure 网站。

![选择 Azure](publish-to-azure/_static/image2.png)

如果未登录到 Azure，提供你的 Azure 帐户凭据。 然后，选择新建以创建新的 web 应用。

![新的站点](publish-to-azure/_static/image3.png)

创建 web 应用的唯一名称。 如果看到一个绿色的复选标记，右侧的名称字段，将知道名称是唯一的。 选择你的 web 应用的区域。 选择**创建新的服务器**数据库，并为此新的数据库服务器提供的用户名和密码。 完成后，单击**创建**。

![创建站点](publish-to-azure/_static/image4.png)

连接值现在一切就绪。 您可以将这些值保持不变。

![connection](publish-to-azure/_static/image5.png)

单击 **“下一步”**。

对于设置，请注意，两个数据库连接指定-ApplicationDBContext 和 ContosoUniversityDataEntities。 ApplicationDBContext 是用户帐户表的连接。 这些值仅显示数据库的连接字符串。 它并不意味着当你发布你的站点时，将发布这些数据库。 完成 web 应用发布后，您将发布您的数据库项目。

![](publish-to-azure/_static/image6.png)

数据库连接旁边的省略号 （...） 显示连接字符串的详细信息。 单击 ContosoUniversityDataEntities 旁边的省略号。

![](publish-to-azure/_static/image7.png)

记下数据库服务器和数据库的名称。 随机生成的服务器名称。 数据库名称是简单的你的站点名称 **\_db**追加。 当你发布你的数据库时，将更高版本需要两个名称。

单击**确定**以关闭数据库连接字符串窗口。

在发布 Web 窗口中，单击**下一步**以查看预览。

![](publish-to-azure/_static/image8.png)

您可以单击开始预览以查看要发布的文件的列表。 由于这是首次发布此站点，该列表将为项目中的每个相关文件。

单击“发布” 。

输出窗格将显示你发布的结果。

![](publish-to-azure/_static/image9.png)

在发布后的站点是 immedialely web 浏览器中启动。 已部署你的站点，并且可以注册到站点; 一个新用户但是，在 ContosoUniversityData 项目中的表具有尚未发布。 如果学生链接的列表中单击你将收到错误。

## <a name="publish-database-to-sql-azure"></a>将数据库发布到 SQL Azure

在发布之前您的数据库，您必须确保在本地计算机可以连接到数据库服务器。 数据库服务器的防火墙将限制哪些计算机可以连接到数据库。 您需要将您的计算机的 IP 地址添加到防火墙允许的 IP 地址。

登录到 Azure 帐户通过 Azure 门户。

选择新数据库，并选择**管理**。

![管理](publish-to-azure/_static/image10.png)

必须配置你的数据库服务器以允许从您的计算机的连接。 选择管理，系统会要求将当前的 IP 地址添加到数据库服务器允许的方式。 选择是。

![添加 ip 地址](publish-to-azure/_static/image11.png)

没有机会在上一步中添加的 IP 地址不是您需要为连接配置的唯一 IP 地址。 您可以尝试登录到数据库以查看是否连接已正确设置。 提供的用户和前面创建的密码。

![登录](publish-to-azure/_static/image12.png)

如果你收到一条错误消息，您需要添加另一个 IP 地址。 单击以查看有关错误的更多详细信息的错误消息。 在详细信息，您将看到您需要添加的 IP 地址。 记下此 IP 地址。

![不允许](publish-to-azure/_static/image13.png)

关闭此登录窗口中，并返回到 Azure 门户。

导航到你的数据库的仪表板。 单击**允许的 IP 地址管理**。

![管理 ip 地址](publish-to-azure/_static/image14.png)

现在必须从错误消息添加 IP 地址。 更改允许的 IP 地址以包括错误消息中的一个范围，或者将该 IP 地址添加为一个单独的条目。

![添加新地址](publish-to-azure/_static/image15.png)

将更改保存到允许的 IP 地址。

单击管理，并尝试再次登录到数据库。 您可能需要等待几分钟才能正确地为防火墙配置允许的 IP 地址。 如果可以成功登录数据库中，你已完成与数据库的连接设置。

因为您稍后将检查数据库部署的结果，可以将此管理窗口打开。

返回到您的数据库项目。 右键单击项目并选择**发布**。

![发布数据库](publish-to-azure/_static/image16.png)

在发布数据库窗口中，选择**编辑**。

![编辑](publish-to-azure/_static/image17.png)

为服务器提供数据库服务器和身份验证凭据的名称。 提供凭据后，选择从可用数据库列表创建的数据库。 默认情况下，Visual Studio 将数据库字段的名称设置为你的项目可能不是你创建的数据库相同的名称。

![](publish-to-azure/_static/image18.png)

单击“确定”。

您可能会想要保存此配置文件，以便可以发布在将来的更新而无需重新输入的所有连接信息。 选择“创建配置文件”。

![保存配置文件](publish-to-azure/_static/image19.png)

它将创建一个文件中名为的项目**ContosoUniversityData.publish.xml**。 下次你想要将数据库发布到 Azure，只需加载该配置文件。

现在，单击**发布**在 Azure 上创建数据库。

![publish](publish-to-azure/_static/image20.png)

后运行一段时间，显示发布结果。

![results](publish-to-azure/_static/image21.png)

现在，你可以返回到管理门户为你的数据库。 刷新设计视图中，并请注意，已部署包含预填充的数据的 3 个表。

![新表](publish-to-azure/_static/image22.png)

现在已准备好部署到 Azure web 应用进行测试。 导航到在 Azure 上的 web 应用 (如 http://contosositeexample.azurewebsites.net/)。 单击链接获取学生列表，您应看到面向学生的索引视图。

![查看](publish-to-azure/_static/image23.png)

有时候，数据库和连接需要一些时间来正确配置。 如果收到错误，等待几分钟并再试一次。

## <a name="conclusion"></a>结束语

本系列提供一个简单的示例说明如何从现有数据库，使用户能够编辑、 更新、 创建和删除数据生成代码。 它使用 ASP.NET MVC 5，实体框架和 ASP.NET 基架创建项目。

Code First 开发的介绍性示例，请参阅[Getting Started with ASP.NET MVC 5](../introduction/getting-started.md)。

有关更高级的示例，请参阅[为 ASP.NET MVC 4 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 请注意，使用第一个数据库中的数据使用 DbContext API 是用于在第一个代码中使用数据的 API 相同。 即使你想要使用第一个数据库，您可以了解如何处理更复杂的方案，如读取和更新相关的数据，处理并发冲突，请从代码第一个教程，等等。 如何创建数据库、 上下文类和实体类中是唯一的区别。

> [!div class="step-by-step"]
> [上一篇](enhancing-data-validation.md)
