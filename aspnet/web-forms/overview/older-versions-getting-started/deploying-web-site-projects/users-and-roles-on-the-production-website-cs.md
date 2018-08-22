---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
title: 用户和角色生产网站中 (C#) |Microsoft Docs
author: rick-anderson
description: ASP.NET 网站管理工具 (WSAT) 提供了基于 web 的用户界面，用于配置成员身份和角色设置和用于创建、 编辑、...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: dbc54313-5d05-4285-98b3-726edea6d0c9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
msc.type: authoredcontent
ms.openlocfilehash: f08afe5f4ab379d1532f50267299892829c95dcc
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831075"
---
<a name="users-and-roles-on-the-production-website-c"></a>用户和角色生产网站中 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial16_CustomAWAT_cs.pdf)

> ASP.NET 网站管理工具 (WSAT) 提供基于 web 的用户界面，用于配置成员身份和角色设置和用于创建、 编辑和删除用户和角色。 遗憾的是，WSAT 只适用于从本地主机，这意味着你无法通过浏览器访问生产网站的管理工具。 好消息是有解决方法，使得可以管理用户和生产上的角色。 本教程介绍以下解决方法和其他人。


## <a name="introduction"></a>介绍

ASP.NET 2.0 引入了大量*应用程序服务*，这是一套可以添加到 web 应用程序的构建基块服务。 我们添加了成员身份和角色服务添加到书评网站重新[*配置网站，使用应用程序服务*教程](configuring-a-website-that-uses-application-services-cs.md)。 成员资格服务有助于创建和管理用户帐户;角色服务提供用于将用户分类为组的 API。 书评站点都有三个用户帐户-Scott，Jisun，Alice-和单个角色，管理员，与 Scott 和 Jisun 管理员角色中。

ASP。NET 的应用程序服务不受限于特定的实现。 相反，指示要使用特定的应用程序服务*提供程序*，并且该提供程序实现使用特定技术的服务。 我们配置书评 web 应用程序以使用`SqlMembershipProvider`和`SqlRoleProvider`的成员身份和角色服务提供程序。 这些两个提供程序在 SQL Server 数据库中存储用户帐户和角色信息，并为基于 Internet 的 web 应用程序托管在 web 托管公司最常使用的提供程序。

使用成员资格和角色服务的开发人员常见的难题管理用户和角色在生产环境。 您如何从生产网站中删除用户帐户、 添加新的角色，或将现有用户添加到现有的角色？ 本教程探讨了不同的技术来管理用户和生产网站上的角色。

## <a name="using-the-aspnet-web-site-administration-tool"></a>使用 ASP.NET 网站管理工具

ASP.NET 包括[网站管理工具](https://msdn.microsoft.com/library/yy40ytx0.aspx)(WSAT)，可轻松创建和管理用户帐户和角色并指定基于用户和角色的授权规则。 若要使用 WSAT，单击解决方案资源管理器中的 ASP.NET 配置图标或转到网站或项目菜单并选择 ASP.NET 配置选项。 这两种方法启动 web 浏览器并指向 WSAT 类似的地址处： `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`

WSAT 分为三个部分：

- **安全**-管理用户、 角色和授权规则。
- **应用程序配置**-管理&lt;appSettings&gt;和 SMTP 从此处的设置。 您可以还使应用程序脱机和管理调试和跟踪从此处，设置，以及指定默认自定义错误页。
- **ProviderConfiguration** -配置应用程序服务使用的提供程序。

安全性部分 (所示**图 1**) 包括链接创建新用户、 管理用户、 创建和管理角色，以及创建和管理访问规则。 从此处可以向系统添加新的角色、 删除现有用户，或添加或删除角色，从特定用户帐户。

[![](users-and-roles-on-the-production-website-cs/_static/image2.png)](users-and-roles-on-the-production-website-cs/_static/image1.png)

**图 1**: WSAT 安全部分包含用于管理用户和角色选项  
([单击此项可查看原尺寸图像](users-and-roles-on-the-production-website-cs/_static/image3.png))

遗憾的是，WSAT 才可访问本地。 您不能访问 WSAT 上远程生产网站;如果您访问`www.yoursite.com/asp.netwebadminfiles/default.aspx`获取 404 找不到响应。 提供支持 WSAT 使用的代码`Membership`和`Roles`类在.NET Framework，才能创建、 编辑和删除用户和角色。 这些类查阅 web 应用程序的配置信息来确定哪种访问接口使用;回到[*配置网站，使用应用程序服务*教程](configuring-a-website-that-uses-application-services-cs.md)我们设置书评网站以使用`SqlMembershipProvider`和`SqlRoleProvider`提供程序。 这需要执行添加`<membership>`并`<roleManager>`到部分`Web.config`。

[!code-xml[Main](users-and-roles-on-the-production-website-cs/samples/sample1.xml)]

请注意，`<membership>`并`<roleManager>`部分引用`SqlMembershipProvider`并`SqlRoleProvider`中的提供程序其`type`属性，分别。 这些提供程序在指定的 SQL Server 数据库中存储的用户和角色信息。 通过指定由这些提供程序使用的数据库`connectionStringName`属性， `ReviewsConnectionString`，其定义中`~/ConfigSections/databaseConnectionStrings.config`文件。 请记住，`databaseConnectionStrings.config`开发环境中的文件包含到开发数据库的连接字符串，而`databaseConnectionStrings.config`生产上的文件包含对生产数据库的连接字符串。

简单地说，必须通过开发环境中，本地访问 WSAT 和它适用于中指定的数据库中的用户和角色信息`databaseConnectionStrings.config`文件。 因此，如果我们更改中的连接字符串信息`databaseConnectionStrings.config`文件在开发环境中我们可以使用 WSAT 本地管理用户和生产环境中的角色。

若要演示此功能，请打开`databaseConnectionStrings.config`文件在 Visual Studio 中，在开发环境和开发数据库连接字符串替换为生产数据库连接字符串。 然后启动 WSAT，转到安全选项卡，并添加新用户密码"password ！"创建名为 Sam （小于引号）。 **图 2**显示 WSAT 屏幕时创建此帐户。

[![](users-and-roles-on-the-production-website-cs/_static/image5.png)](users-and-roles-on-the-production-website-cs/_static/image4.png)

**图 2**： 创建一个名为 Sam 在生产环境中的新用户  
([单击此项可查看原尺寸图像](users-and-roles-on-the-production-website-cs/_static/image6.png))

因为我们更改中的连接字符串`databaseConnectionStrings.config`为指向生产数据库服务器，Sam 已添加为生产环境中的用户。 若要验证这一点，更改中的连接字符串`databaseConnectionStrings.config`返回到开发数据库文件，然后访问`Login.aspx`开发环境中的页。 尝试登录为 Sam (请参阅**图 3**)。

[![](users-and-roles-on-the-production-website-cs/_static/image8.png)](users-and-roles-on-the-production-website-cs/_static/image7.png)

**图 3**： 不能以在开发环境中的 Sam 身份登录  
([单击此项可查看原尺寸图像](users-and-roles-on-the-production-website-cs/_static/image9.png))

您不能作为 Sam 在开发环境中由于登录本地数据库中不存在的用户帐户信息。 相反，是已添加到生产数据库。 若要验证这一点，查看的内容`aspnet_Users`开发和生产数据库中的表。 在开发环境中应为 Scott，Jisun 和 Alice 的用户只有三个记录。 但是，`aspnet_Users`生产数据库中的表具有四个记录： Scott、 Jisun、 Alice 和 Sam。 因此，Sam 可以登录通过网站在生产中，但不能通过在开发环境。

[![](users-and-roles-on-the-production-website-cs/_static/image11.png)](users-and-roles-on-the-production-website-cs/_static/image10.png)

**图 4**: Sam 可以在生产网站上登录  
([单击此项可查看原尺寸图像](users-and-roles-on-the-production-website-cs/_static/image12.png))

> [!NOTE]
> 不要忘记更改中的连接字符串`databaseConnectionStrings.config`完成后，返回到开发数据库文件的连接字符串使用的 WSAT 否则为测试开发站点时将使用与生产数据环境。 另请注意，虽然我们刚刚讨论的技术使我们能够使用 WSAT 来远程管理用户和角色，对任何其他 WSAT 配置选项 （访问规则、 SMTP 设置、 调试和跟踪设置和等等） 的更改修改`Web.config`文件。 因此，任何对设置所做的更改适用于开发环境而不适用于生产环境。


## <a name="creating-custom-user-and-role-management-web-pages"></a>创建自定义用户和角色管理网页

WSAT 提供带框系统，用于管理用户和角色，但仅在本地启动，需要对连接字符串信息进行更改，以便管理用户和生产上的角色。 大多数支持用户帐户的网站还包含多个用户和角色管理网页，使管理员能够管理从站点中的页的用户和角色。 此类基于 web 的管理页使其更轻松地管理用户和角色，并对站点而言至关重要的可能有很多管理员或是否有权访问或使用 Visual Studio 启动 WSAT 的技术背景的管理员。

ASP.NET 包括大量内置登录相关 Web 控件，使实现许多这些管理网页拖放一样简单。 例如，可以创建用于管理员通过将 CreateUserWizard 控件拖到绘图页上，并设置几个属性创建新的用户帐户的页面。 事实上，在中所示 WSAT 中创建用户的页面**图 2**使用相同的 CreateUserWizard 控件可添加到您的页面。 此外，成员身份和角色服务的功能可通过以编程方式`Membership`和`Roles`.NET Framework 中的类。 与这些类可以编写代码以创建、 编辑和删除用户和角色，也可以添加或删除用户到角色，以确定用户位于什么角色，并执行其他用户和角色相关的任务。

在中[*配置网站，使用应用程序服务*教程](configuring-a-website-that-uses-application-services-cs.md)添加到一个页面，我`Admin`文件夹名为`CreateAccount.aspx`。 此页面允许管理员将新的用户帐户添加到站点，并以指定新创建的用户是否是管理员角色中 (请参阅**图 5**)。

[![](users-and-roles-on-the-production-website-cs/_static/image14.png)](users-and-roles-on-the-production-website-cs/_static/image13.png)

**图 5**： 管理员可以创建新的用户帐户  
([单击此项可查看原尺寸图像](users-and-roles-on-the-production-website-cs/_static/image15.png))

有关更详细地查看构建用户和角色的管理页面，以及使用的分步说明`Membership`并`Roles`类和登录相关的 ASP.NET Web 控件，请务必阅读我[网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。 那里您可以找到指南如何生成用于创建新帐户、 创建和管理角色，网页将用户分配到角色，以及其他常见管理任务。

若要实现 WSAT 类似的功能，生产网站上可以始终生成实现 WSAT 的功能的网页的序列。 若要帮助入门，请查看位于文件夹中的 WSAT 源代码`%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`。 另一种方法是使用 Dan Clem WSAT 替代方法，他将分享他的文章，其中[滚动你自己网站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)。 Dan 指导读者全面了解构建自定义 WSAT 类似的工具的过程、 包含 （在 C# 中)，下载其应用程序的源代码，并提供用于将其自定义 WSAT 添加到托管网站的分步说明。

## <a name="summary"></a>总结

可以在迁移后的成员身份和角色应用程序服务中使用 ASP.NET 网站管理工具 (WSAT)，来管理你的网站的用户和角色信息。 遗憾的是，WSAT 仅本地访问，不能从你的生产网站访问。 但是，通过更改连接字符串在开发环境，以点到生产数据库可以使用 WSAT 来管理用户和生产网站上的角色。

虽然 WSAT 方法提供了一种快速而简单的方法来管理用户和角色，它要求启动的连接字符串信息从 Visual Studio，以及发生临时更改 WSAT。 WSAT 提供了一种快速的方式来管理用户和角色在生产环境中，但很麻烦，不会不适用于网站与多个管理员或不具有或不熟悉 Visual Studio 和 WSAT 的管理员。 出于这些原因，支持用户帐户的大多数网站包含一组管理的 web 页面。 这样一组网页就不必进行 WSAT 且使用各种管理用户从任何计算机。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [正在检查 ASP。NET 的成员资格、 角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [滚动你自己的网站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [网站管理工具概述](https://msdn.microsoft.com/library/yy40ytx0.aspx)
- [网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [上一页](precompiling-your-website-cs.md)
> [下一页](asp-net-hosting-options-vb.md)
