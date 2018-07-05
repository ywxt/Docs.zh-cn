---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs
title: 配置网站使用应用程序服务 (C#) |Microsoft Docs
author: rick-anderson
description: ASP.NET 2.0 版引入了一系列的应用程序服务，这是.NET Framework 的一部分，作为构建基块的一套服务 yo...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/23/2009
ms.topic: article
ms.assetid: 1e33d1c6-3f9f-4c26-81e2-2a8f8907bb05
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs
msc.type: authoredcontent
ms.openlocfilehash: 27c91868d46b6040a25b8cb83480bf83081fc98c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399089"
---
<a name="configuring-a-website-that-uses-application-services-c"></a>配置网站使用应用程序服务 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_09_CS.zip)或[下载 PDF](http://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial09_AppServicesConfig_cs.pdf)

> ASP.NET 2.0 版引入了一系列的应用程序服务，这是.NET Framework 的一部分，作为一套可用于将丰富的功能添加到 web 应用程序的构建基块服务。 本教程探讨了如何在要使用应用程序服务的生产环境中配置一个网站，并解决了管理用户帐户和角色在生产环境的常见问题。


## <a name="introduction"></a>介绍

ASP.NET 2.0 版引入了一系列*应用程序服务*，这是.NET Framework 的一部分，作为构建基块的一套服务可用于对 web 应用程序添加丰富的功能。 应用程序服务包括：

- **成员资格**-用于创建和管理用户帐户的 API。
- **角色**-用于将用户分类为组的 API。
- **配置文件**-用于存储自定义的特定于用户的内容的 API。
- **站点地图**-用于在层次结构，则可以通过导航控件，如菜单和痕迹导航栏显示的窗体中定义站点 s 逻辑结构的 API。
- **个性化**-用于维护自定义项首选项，通常与一起使用的 API [ *web 部件*](https://msdn.microsoft.com/library/e0s9t4ck.aspx)。
- **运行状况监视**-用于监视性能、 安全性、 错误和运行的 web 应用程序其他系统运行状况指标的 API。
  

应用程序服务 Api 不受限于特定的实现。 相反，指示要使用特定的应用程序服务*提供程序*，并且该提供程序实现使用特定技术的服务。 在 web 托管公司托管的基于 Internet 的 web 应用程序最常使用的提供商将使用 SQL Server 数据库实现这些提供程序。 例如，`SqlMembershipProvider`是将用户帐户信息存储在 Microsoft SQL Server 数据库中的成员身份 API 的提供程序。

部署应用程序时使用的应用程序服务和 SQL Server 提供程序添加一些挑战。 对于初学者而言，必须正确地开发和生产数据库上创建应用程序服务数据库对象并将其正确地初始化。 也有不需要进行重要的配置设置。

> [!NOTE]
> Api 设计使用的应用程序服务[*提供程序模型*](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)，允许 API s 的实现详细信息，以在运行时提供的设计模式。 .NET Framework 提供了很多的应用程序服务提供程序可以使用，如`SqlMembershipProvider`和`SqlRoleProvider`、 哪些是提供程序的成员身份和角色 Api，使用 SQL Server 数据库实现。 此外可以创建插件和自定义提供程序。 事实上，书评 web 应用程序已包含站点映射 API 的自定义提供程序 (`ReviewSiteMapProvider`)，该构造中的数据从站点地图`Genres`和`Books`数据库中的表。


本教程开始，看我如何扩展书评 web 应用程序以使用成员资格和角色 Api。 它然后演示如何部署应用程序服务使用 SQL Server 数据库实现，并通过解决常见的问题管理用户帐户和角色在生产环境以结束的 web 应用程序。

## <a name="updates-to-the-book-reviews-application"></a>通讯簿评审应用程序的更新

过去的几通讯簿评审 web 应用程序已更新从静态网站，以动态、 数据驱动的 web 应用程序的教程使用一组管理页用于管理流派和评审完成。 但是，本部分中管理当前不受保护-任何用户都知道 （或猜测） 管理页面的 URL 可以 waltz 中和创建、 编辑或删除我们的网站上的评论。 若要保护的网站的某些部分的常用方法是实现用户帐户，然后使用 URL 授权规则来限制对特定用户或角色的访问。 可供下载与本教程中的书评 web 应用程序支持用户帐户和角色。 它具有单个角色定义名为管理员和只有此角色中的用户可以访问的管理页面。

> [!NOTE]
> 我 ve 书评 web 应用程序中创建三个用户帐户： Scott、 Jisun 和 Alice。 所有三个用户具有相同的密码：**密码 ！** Scott 和 Jisun 是管理员角色中，Alice 不是。 仍可供匿名用户访问站点 s 非管理页面。 也就是说，不需要登录以访问站点，除非你想要管理它，这种情况下您必须登录为管理员角色中的用户。


书评应用程序的母版页进行已更新，包括已经过身份验证和匿名用户的不同的用户界面。 如果匿名用户访问该网站她会看到右上角的登录链接。 身份验证的用户将看到此消息，"欢迎回来，*用户名*！" 并将其注销的链接。此处 s 还登录页 (`~/Login.aspx`)，其中包含提供用户界面和逻辑，用于对访问者进行身份验证的登录名 Web 控件。 只有管理员才能创建新帐户。 (用于创建和管理中的用户帐户的页面`~/Admin`文件夹。)

### <a name="configuring-the-membership-and-roles-apis"></a>配置成员资格和角色 Api

书评 web 应用程序使用的成员身份和角色 Api 以支持用户帐户并向角色 （即管理员角色） 对这些用户进行分组。 `SqlMembershipProvider`和`SqlRoleProvider`使用提供程序类是因为我们想要在 SQL Server 数据库中存储帐户和角色的信息。

> [!NOTE]
> 本教程不是要在 web 应用程序配置为支持的成员身份和角色 Api 进行详尽。 有关这些 Api，需要配置网站以使用它们所采取的步骤的全面信息，请阅读我[*网站安全教程*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。


若要使用 SQL Server 数据库使用的应用程序服务必须首先添加使用这些提供程序到数据库用户帐户所需的数据库对象和存储角色信息。 这些必要的数据库对象包括各种表、 视图和存储的过程。 除非另有指定，`SqlMembershipProvider`并`SqlRoleProvider`提供程序类使用名为的 SQL Server Express Edition 数据库`ASPNETDB`位于应用程序的`App_Data`文件夹; 如果此类数据库不存在，它将自动创建通过在运行时这些提供程序的必要的数据库对象。

可能实现，且通常的理想之选，创建应用程序服务网站 s 特定于应用程序数据的存储位置在同一数据库中的数据库对象。 .NET Framework 附带了一个名为工具`aspnet_regsql.exe`用于指定数据库上安装的数据库对象。 我已提前，并使用此工具将添加到这些对象`Reviews.mdf`数据库中`App_Data`文件夹 （开发数据库）。 我们将了解如何在本教程后面使用此工具，当我们将这些对象添加到生产数据库。

如果应用程序服务数据库的数据库对象而不添加`ASPNETDB`将需要自定义`SqlMembershipProvider`和`SqlRoleProvider`提供程序类配置，以便他们使用相应的数据库。 若要自定义成员资格提供程序添加[ *&lt;成员身份&gt;元素*](https://msdn.microsoft.com/library/1b9hw62f.aspx)内`<system.web>`中`Web.config`; 使用[ *&lt;roleManager&gt;元素*](https://msdn.microsoft.com/library/ms164660.aspx)配置角色提供程序。 以下代码片段取自书评应用程序的`Web.config`和显示了成员资格和角色 Api 的配置设置。 请注意，同时注册新的提供程序-`ReviewMembership`并`ReviewRole`-使用`SqlMembershipProvider`和`SqlRoleProvider`提供程序，分别。

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample1.xml)]

`Web.config`文件的`<authentication>`元素同时已配置为支持基于窗体的身份验证。
  

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample2.xml)]

### <a name="limiting-access-to-the-administration-pages"></a>限制对管理页的访问

ASP.NET 可以轻松授予或拒绝访问特定文件或文件夹由用户或角色通过其*URL 授权*功能。 (我们简要讨论了中的 URL 授权*核心 IIS 之间的差异和 ASP.NET Development Server*教程介绍了 IIS 和 ASP.NET Development Server 将以不同的方式为静态的 URL 授权规则的应用与动态内容。）因为我们想要禁止访问`~/Admin`除管理员角色的用户文件夹中，我们需要将 URL 授权规则添加到此文件夹。 具体而言，URL 授权规则需要允许管理员角色中的用户并拒绝所有其他用户。 这可以通过添加`Web.config`文件为`~/Admin`文件夹包含以下内容：

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample3.xml)]

有关 ASP.NET 的 URL 授权功能以及如何使用它为用户和角色的授权规则明确说明的详细信息请阅读[*基于用户的授权*](../../older-versions-security/membership/user-based-authorization-cs.md)和[*基于角色的授权*](../../older-versions-security/roles/role-based-authorization-cs.md)教程从我[*网站安全教程*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。

## <a name="deploying-a-web-application-that-uses-application-services"></a>部署 Web 应用程序使用应用程序服务

在部署时使用应用程序服务和应用程序服务信息存储在数据库中的提供程序的网站，它是命令性，在生产数据库中创建所需的应用程序服务的数据库对象。 最初生产数据库不包含这些对象，因此首次部署应用程序时 （或第一次后添加的应用程序服务部署时），必须采取额外步骤来获取这些必备项的数据库对象上生产数据库。

部署使用应用程序服务，如果你想要复制到生产环境在开发环境中创建的用户帐户的网站时，可能会发生另一项挑战。 根据成员资格和角色的配置，就可以，即使在成功复制到生产数据库在开发环境中创建的用户帐户，这些用户将无法登录到在生产环境中的 web 应用程序。 我们将看一下此问题的原因，并讨论如何避免这种情况发生。

ASP.NET 附带有效果很好[*网站管理工具 (WSAT)* ](https://msdn.microsoft.com/library/yy40ytx0.aspx) ，可以从 Visual Studio 启动，并允许用户通过基于 web 的管理帐户、 角色和授权规则接口。 遗憾的是，WSAT 仅适用于本地网站，这意味着它不能用于远程管理用户帐户、 角色和 web 应用程序在生产环境中的授权规则。 我们将介绍不同的方式来实现从你的生产网站 WSAT 类似的行为。

### <a name="adding-the-database-objects-using-aspnetregsqlexe"></a>添加数据库对象使用 aspnet\_regsql.exe

*部署数据库*教程介绍了如何将表和数据开发数据库复制到生产数据库，以及这些技术确实可以用来复制到的应用程序服务数据库对象生产数据库。 另一个选项是`aspnet_regsql.exe`工具，它将添加或从数据库中删除应用程序服务数据库对象。

> [!NOTE]
> `aspnet_regsql.exe`工具指定数据库上创建数据库对象。 但不会对生产数据库从开发数据库迁移这些数据库对象中的数据。 如果你是想将开发数据库中的用户帐户和角色信息复制到生产数据库使用中介绍的技术*部署数据库*教程。


让我们来看看如何将数据库对象添加到生产数据库使用`aspnet_regsql.exe`工具。 首先，打开 Windows 资源管理器并导航到 %WINDIR%\ 您的计算机上的.NET Framework 2.0 版目录Microsoft.NET\Framework\v2.0.50727。 会显示`aspnet_regsql.exe`工具。 可以使用此工具从命令行中，但它还包括图形用户界面;双击`aspnet_regsql.exe`文件以启动其图形组件。

该工具首先会显示初始屏幕，说明其用途。 单击旁边转到"选择安装程序选项"屏幕中，图 1 所示。 从此处可以选择要添加的应用程序服务数据库对象或从数据库中删除它们。 因为我们想要将这些对象添加到生产数据库，选择"配置应用程序服务的 SQL Server"选项，并单击下一步。


[![选择 SQL Server 配置为应用程序服务](configuring-a-website-that-uses-application-services-cs/_static/image2.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image1.jpg)

**图 1**： 配置 SQL server 选择的应用程序服务 ([单击以查看实际尺寸的图像](configuring-a-website-that-uses-application-services-cs/_static/image3.jpg))


在"选择服务器和数据库"屏幕提示输入信息以连接到数据库。 输入数据库服务器、 安全凭据，并为您提供您的 web 托管公司的数据库名称，然后单击下一步。

> [!NOTE]
> 输入您的数据库服务器和凭据后可能会遇到错误，展开数据库下拉列表时。 `aspnet_regsql.exe`工具查询`sysdatabases`系统表检索的数据库服务器，但一些 web 托管公司锁定其数据库服务器，以便此信息不是公用的列表。 如果收到此错误可以直接在下拉列表中键入数据库名称。


[![提供你的数据库的连接信息的工具](configuring-a-website-that-uses-application-services-cs/_static/image5.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image4.jpg)

**图 2**： 提供的工具与您的数据库 s 连接信息 ([单击以查看实际尺寸的图像](configuring-a-website-that-uses-application-services-cs/_static/image6.jpg))


随后出现的屏幕总结了要执行的位置，即操作将应用程序服务数据库对象添加到指定的数据库。 单击旁边完成此操作。 几分钟后的最后一个屏幕将显示，注意数据库对象已添加了 （参见图 3）。


[![成功 ！应用程序服务数据库对象已添加到生产数据库](configuring-a-website-that-uses-application-services-cs/_static/image8.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image7.jpg)

**图 3**： 成功 ！ 应用程序服务数据库对象已添加到生产数据库 ([单击此项可查看原尺寸图像](configuring-a-website-that-uses-application-services-cs/_static/image9.jpg))


若要验证应用程序服务数据库对象已成功添加到生产数据库，请打开 SQL Server Management Studio 并连接到您的生产数据库。 如图 4 所示，你应看到应用程序服务数据库表在数据库中， `aspnet_Applications`， `aspnet_Membership`， `aspnet_Users`，依次类推。


[![确认数据库对象已添加到生产数据库](configuring-a-website-that-uses-application-services-cs/_static/image11.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image10.jpg)

**图 4**： 确认数据库对象已添加到生产数据库 ([单击以查看实际尺寸的图像](configuring-a-website-that-uses-application-services-cs/_static/image12.jpg))


您只需要使用`aspnet_regsql.exe`工具时部署 web 应用程序第一次或首次使用应用程序服务启动后。 一旦这些数据库对象是在生产数据库上他们赢得 t 需要重新添加或修改。

### <a name="copying-user-accounts-from-development-to-production"></a>复制从开发到生产环境的用户帐户

使用时`SqlMembershipProvider`并`SqlRoleProvider`提供程序类，以将应用程序服务信息存储在 SQL Server 数据库中，用户帐户和角色信息存储在数据库表，其中包括各种`aspnet_Users`， `aspnet_Membership`，`aspnet_Roles`，和`aspnet_UsersInRoles`，等等。 如果在开发过程中创建用户帐户在开发环境中，可以通过将相应的记录复制适用数据库表中复制这些用户帐户在生产环境中。 如果使用数据库发布向导来部署您可能还选择要复制的记录，这将导致在开发也是在生产环境中创建的用户帐户的应用程序服务数据库对象。 但是，具体取决于您的配置设置，您可能会发现其帐户已在开发过程中创建并复制到生产这些用户将无法从生产网站登录。 代表什么意思？

`SqlMembershipProvider`和`SqlRoleProvider`设计提供程序类，以便单一数据库可用作用户存储多个应用程序，其中每个应用程序可以从理论上讲，具有重叠的用户名的用户和角色具有相同名称。 若要允许这种灵活性，数据库将保留一系列中的应用程序`aspnet_Applications`表和每个用户都使用其中一个应用程序相关联。 具体而言，`aspnet_Users`表中有`ApplicationId`列中的记录到每个用户关联在一起`aspnet_Applications`表。

除了`ApplicationId`列中，`aspnet_Applications`该表还包括`ApplicationName`列中，它提供应用程序的更多的用户友好名称。 当网站试图使用用户帐户，如验证从登录页上，用户的凭据必须告知`SqlMembershipProvider`类要使用的应用程序。 它通常会通过提供应用程序名称，这并此值来自中的提供程序的配置`Web.config`-具体通过`applicationName`属性。

但会发生什么情况`applicationName`属性中未指定`Web.config`？ 这种情况下成员资格系统使用的应用程序根路径为`applicationName`值。 如果`applicationName`属性中未显式设置`Web.config`，然后，则可能会开发环境和生产环境使用不同的应用程序的根，因此将无法与不同的应用程序相关联应用程序服务中的名称。 如果出现这种不匹配，则在开发环境中创建这些用户将具有`ApplicationId`与不匹配的值`ApplicationId`生产环境的值。 最终结果是赢得 t 这些用户能够登录。

> [!NOTE]
> 如果您发现自己处于这种情况下-使用用户帐户复制到生产环境且不匹配`ApplicationId`值-可以编写查询以更新这些不正确`ApplicationId`值到`ApplicationId`用于生产。 更新后，请在开发环境中创建的帐户的用户现在将能够登录到生产上的 web 应用程序。


好消息是可用于确保两个环境使用相同的简单步骤`ApplicationId`-显式设置`applicationName`属性中`Web.config`所有应用程序服务提供程序。 我显式设置`applicationName`属性为"BookReviews"中`<membership>`并`<roleManager>`元素中此代码片段作为`Web.config`显示。

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample4.xml)]

有关设置的详细讨论`applicationName`属性和的基本原理，请参阅[ *Scott Guthrie* ](https://weblogs.asp.net/scottgu/) s 博客文章[*始终设置应用程序名称配置 ASP.NET 成员资格和其他提供程序时的属性*](https://weblogs.asp.net/scottgu/443634)。

### <a name="managing-user-accounts-in-the-production-environment"></a>管理生产环境中的用户帐户

ASP.NET 网站管理工具 (WSAT) 轻松创建和管理用户帐户、 定义和应用角色和拼写出基于用户和角色的授权规则。 通过转到解决方案资源管理器并单击 ASP.NET 配置图标，或通过转到网站或项目菜单并选择 ASP.NET 配置菜单项，可以启动从 Visual Studio WSAT。 遗憾的是，WSAT 可以仅适用于本地网站。 因此，不能从工作站使用 WSAT 管理生产环境中的网站。

好消息是功能的公开的所有提供的 WSAT 是功能的以编程方式通过成员资格和角色 Api;此外，许多 WSAT 屏幕使用标准 ASP.NET 登录相关控件。 简单地说，您可以将 ASP.NET 页面添加到你提供了必需的管理功能的网站。

回想一下前面的教程中，更新书评 web 应用程序以包括`~/Admin`文件夹，以及此文件夹具有已配置为仅允许用户管理员角色中。 我添加一个页面名为该文件夹`CreateAccount.aspx`从该管理员可以创建新的用户帐户。 此页使用 CreateUserWizard 控件来显示用于创建新的用户帐户的用户界面和后端逻辑。 新增更多，我自定义控件以包含一个复选框，提示是否还应添加到管理员角色的新用户 （请参见图 5）。 使用很少的工作可以构建自定义的一组页面实现的用户和角色管理相关任务 WSAT 否则会提供。

> [!NOTE]
> 有关与登录相关的 ASP.NET Web 控件一起使用的成员身份和角色 Api 的详细信息请阅读我[*网站安全教程*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。 有关自定义 CreateUserWizard 控件的详细信息，请参阅[*创建用户帐户*](../../older-versions-security/membership/creating-user-accounts-cs.md)并[*存储的其他用户信息*](../../older-versions-security/membership/storing-additional-user-information-cs.md)教程中或查看[ *Erich Peterson* ](http://www.erichpeterson.com/) s 文章[*自定义 CreateUserWizard 控件*](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx).


[![管理员可以创建新的用户帐户](configuring-a-website-that-uses-application-services-cs/_static/image14.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image13.jpg)

**图 5**： 管理员可以创建新的用户帐户 ([单击以查看实际尺寸的图像](configuring-a-website-that-uses-application-services-cs/_static/image15.jpg))


如果您需要的全部功能的 WSAT 签出[*滚动你自己网站管理工具*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)，在作者 Dan Clem 逐步构建自定义 WSAT 类似的工具的过程。 Dan 共享应用程序的源代码 （在 C# 中)，并提供有关将其添加到托管网站的分步说明。

## <a name="summary"></a>总结

部署使用的应用程序服务数据库实现的 web 应用程序时必须首先确保的生产数据库都有必要的数据库对象。 可以使用中讨论的技术添加这些对象*部署的数据库*教程; 或者，可以使用`aspnet_regsql.exe`工具，如我们在本教程中看到。 以同步 （这是重要信息： 如果你想要在生产中无效的用户和开发环境中创建的角色） 的开发和生产环境和技术中使用的应用程序名称为中心，我们介绍其他挑战管理用户和生产环境中的角色。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [*ASP.NET SQL Server 注册工具 (aspnet_regsql.exe)*](https://msdn.microsoft.com/library/ms229862.aspx)
- [*为 SQL Server 中创建应用程序服务数据库*](https://msdn.microsoft.com/library/x28wfk74.aspx)
- [*SQL Server 中创建成员身份架构*](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md)
- [*检查 ASP.NET s 成员资格、 角色和配置文件*](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [*滚动你自己的网站管理工具*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [*网站安全教程*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)
- [*网站管理工具概述*](https://msdn.microsoft.com/library/yy40ytx0.aspx)

> [!div class="step-by-step"]
> [上一页](configuring-the-production-web-application-to-use-the-production-database-cs.md)
> [下一页](strategies-for-database-development-and-deployment-cs.md)
