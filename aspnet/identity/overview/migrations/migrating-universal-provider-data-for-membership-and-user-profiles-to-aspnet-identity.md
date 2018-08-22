---
uid: identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
title: 将通用提供程序的数据迁移的成员身份和用户配置文件到 ASP.NET 标识 (C#) |Microsoft Docs
author: rustd
description: 本教程中介绍的步骤所需迁移用户和角色的数据和创建使用现有应用的通用提供程序的用户配置文件数据...
ms.author: riande
ms.date: 12/13/2013
ms.assetid: 2e260430-d13c-4658-bd05-e256fc0d63b8
msc.legacyurl: /identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 6115b2a6caca05659f1c35ce97954807a6fb01ae
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825807"
---
<a name="migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity-c"></a>将通用提供程序的数据迁移的成员身份和用户配置文件到 ASP.NET 标识 (C#)
====================
通过[Pranav rastogi 撰写](https://github.com/rustd)， [Rick Anderson](https://github.com/Rick-Anderson)， [Robert McMurray](https://github.com/rmcmurray)， [Suhas Joshi](https://github.com/suhasj)

> 本教程介绍所需迁移用户和角色的数据和创建使用现有的应用程序到 ASP.NET 标识模型的通用提供程序的用户配置文件数据的步骤。 迁移用户配置文件数据可在具有 SQL 成员身份的应用程序，此处提及的方法。


使用 Visual Studio 2013 的发布，ASP.NET 团队引入了新的 ASP.NET 标识系统，并可以阅读更多有关该发行版[此处](../../index.md)。 后续文章将从 web 应用程序迁移[到新的标识系统的 SQL 成员资格](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)，本文将演示迁移现有应用程序的用户和角色管理的提供程序模型的步骤为新的身份标识模型。 本教程的焦点将主要在迁移用户配置文件数据，以无缝地将其挂接到新系统上。 迁移用户和角色的信息是类似的 SQL 成员身份。 可以使用 SQL 成员资格应用程序中使用迁移配置文件数据时遵循的方法。

例如，我们将开始使用 Visual Studio 2012 使用的提供程序模型创建的 web 应用。 我们将然后添加代码来配置文件管理、 注册用户、 添加的用户配置文件数据、 将数据库架构，迁移，然后将更改应用程序使用的标识系统的用户和角色管理。 为迁移的测试，创建使用通用提供程序的用户应该能够以用户身份登录，新用户应能注册。

> [!NOTE]
> 您可以找到完整的示例在[ https://github.com/suhasj/UniversalProviders-Identity-Migrations ](https://github.com/suhasj/UniversalProviders-Identity-Migrations)。


## <a name="profile-data-migration-summary"></a>配置文件数据迁移摘要

在开始之前与的迁移，让我们看一下在提供程序模型中存储配置文件数据的体验。 应用程序可以通过多种方式存储用户的配置文件数据，最常见在它们之间正在使用内置的配置文件提供程序和通用提供程序一起提供。 这些步骤将包括

1. 添加具有用来存储配置文件数据的属性的类。
2. 添加扩展 ProfileBase，并实现方法以获取用户的更高版本的配置文件数据的类。
3. 使用默认配置文件提供程序中的启用*web.config*文件，并定义用于访问配置文件信息的第 2 步中声明的类。

配置文件信息存储为序列化的 xml 和二进制数据在数据库中的配置文件表中。

迁移应用程序以使用新的 ASP.NET 标识系统之后, 是反序列化的配置文件信息并将其存储为用户类上的属性中。 然后可以将每个属性映射到用户表中的列上。 其优点在于属性都可以得到直接使用 user 类除了无需序列化/反序列化数据信息时对其进行访问的时间。

## <a name="getting-started"></a>入门

1. 在 Visual Studio 2012 中创建新的 ASP.NET 4.5 Web 窗体应用程序。 当前的示例使用 Web 窗体模板，但您也可以使用 MVC 应用程序。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.jpg)
2. 创建一个新文件夹模型来存储配置文件信息  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.png)
3. 作为示例，让我们在配置文件中存储的出生、 城市、 高度和权重的用户的日期。 身高和体重存储为一个名为 PersonalStats 的自定义类。 若要存储和检索配置文件，我们需要一个类以扩展 ProfileBase。 让我们创建一个新类 AppProfile 获取并存储配置文件信息。

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample1.cs)]
4. 启用配置文件中的*web.config*文件。 输入要用来存储/检索用户信息在步骤 #3 中创建的类名。

    [!code-xml[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample2.xml)]
5. 若要从用户获取配置文件数据并将其存储的帐户文件夹中添加 web 窗体页。 右键单击项目并选择添加新项。 添加新的 webforms 页与母版页 AddProfileData.aspx。 将以下内容复制的主要内容部分中：

    [!code-html[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample3.html)]

   在代码隐藏中添加以下代码：

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample4.cs)]

   添加命名空间下的 AppProfile 类定义以删除编译错误。
6. 运行应用并使用用户名创建一个新用户**olduser。** 导航到 AddProfileData 页，并添加用户的配置文件信息。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.png)

你可以验证的数据存储为序列化的 xml 中使用服务器资源管理器窗口的配置文件表。 在 Visual Studio 中，从视图菜单中，选择服务器资源管理器。 应为数据库中定义的数据连接*web.config*文件。 单击数据连接显示不同的子类别。 展开表以显示在不同的表在数据库中，然后右键单击配置文件，并选择显示表数据以查看配置文件表中存储的配置文件数据。

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.png)

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image4.png)

## <a name="migrating-database-schema"></a>迁移数据库架构

若要使现有数据库使用的标识系统，我们需要更新标识数据库来支持我们添加到原始数据库的字段中的架构。 这可以使用 SQL 脚本来创建新表并将复制的现有信息。 在服务器资源管理器窗口中，展开 DefaultConnection 以显示表。 右键单击表并选择新建查询

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image5.png)

将从 SQL 脚本粘贴[ https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt ](https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt)并运行它。 如果刷新 DefaultConnection 时，我们可以看到添加的新表。 您可以检查以查看已迁移的信息的表中的数据。

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image6.png)

## <a name="migrating-the-application-to-use-aspnet-identity"></a>迁移应用程序以使用 ASP.NET 标识

1. 安装 Nuget 包所需的 ASP.NET 标识：

    - Microsoft.AspNet.Identity.EntityFramework
    - Microsoft.AspNet.Identity.Owin
    - Microsoft.Owin.Host.SystemWeb
    - Microsoft.Owin.Security.Facebook
    - Microsoft.Owin.Security.Google
    - Microsoft.Owin.Security.MicrosoftAccount
    - Microsoft.Owin.Security.Twitter

   管理 Nuget 包的详细信息可在[此处](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)
2. 若要使用表中的现有数据，我们需要创建模型类映射回表并将它们连接起来，标识系统中。 作为标识协定的一部分，在 model 类应实现 Identity.Core dll 中定义的接口，或可以扩展现有 Microsoft.AspNet.Identity.EntityFramework 中提供这些接口的实现。 我们将角色、 用户登录名和用户声明使用现有的类。 我们需要我们的示例使用自定义用户。 右键单击项目并创建新文件夹 IdentityModels。 添加新的用户类，如下所示：

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample5.cs)]

   请注意，ProfileInfo 现在是用户类的属性。 因此我们可以使用用户类来直接使用配置文件数据。

复制中的文件**IdentityModels**并**IdentityAccount**中下载源的文件夹 ( [ https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations ](https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations) )。 这些具有剩余模型类和所需的用户和角色管理使用 ASP.NET 标识 Api 的新页。 使用的方法类似于 SQL 成员资格，可以找到详细的说明[此处](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)。

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

## <a name="copying-profile-data-to-the-new-tables"></a>配置文件将数据复制到新表

前面曾提到，我们需要反序列化配置文件表中的 xml 数据并将其存储在 AspNetUsers 表中的列。 因此，剩下的就是填充这些列使用必要的数据在上一步骤中的用户表中创建新列。 若要执行此操作，我们将使用一次运行以填充新创建的用户表中列的控制台应用程序。

1. 在现有解决方案中创建新的控制台应用程序。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.jpg)
2. 安装 Entity Framework 包的最新版本。
3. 添加对该控制台应用程序的引用上面创建的 web 应用程序。 为此，右击项目，然后添加引用，然后解决方案，然后单击项目，并单击确定。
4. 复制下面的 Program.cs 类中的代码。 此逻辑读取的每个用户配置文件数据、 将其作为 ProfileInfo 对象序列化并将其存储回数据库。

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample6.cs)]

   所使用的模型的一些文件夹中定义 IdentityModels 的 web 应用程序项目，因此你必须将包含相应的命名空间。
5. 上面的代码适用于应用程序中的数据库文件\_前面步骤中创建的 web 应用程序项目的数据文件夹。 若要引用的请使用 web 应用程序的 web.config 中的连接字符串更新控制台应用程序的 app.config 文件中的连接字符串。 此外提供 AttachDbFilename 属性中的完整物理路径。
6. 打开命令提示符并导航到更高版本的控制台应用程序的 bin 文件夹。 运行可执行文件并查看日志输出，如在下图中所示。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.jpg)
7. 在服务器资源管理器中打开 AspNetUsers 表，并验证保存属性的新列中的数据。 它们应更新相应的属性值。

## <a name="verify-functionality"></a>验证功能

使用新添加的成员资格页使用 ASP.NET 标识登录的用户从旧数据库实现。 用户应该能够在使用相同的凭据进行登录。 请尝试其他功能类似于添加 OAuth，创建新用户，更改密码，添加角色，将用户添加到角色，等等。

应检索和存储在用户表中的旧用户和新用户的配置文件数据。 应不再引用旧表。

## <a name="conclusion"></a>结束语

本文所述的 web 应用程序迁移到 ASP.NET 标识的成员身份使用提供程序模型的过程。 此外文章所述的用户要挂钩到标识系统的迁移配置文件数据。 请留下注释下面的问题和迁移您的应用程序时遇到的问题。

*感谢 Rick Anderson 和 Robert McMurray 有关本文的审阅。*
