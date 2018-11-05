---
uid: identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
title: 自定义存储提供程序的 ASP.NET 标识概述 |Microsoft Docs
author: Rick-Anderson
description: ASP.NET 标识是一个可扩展的系统，这样就可以创建自己的存储提供程序并将其插入到你的应用程序而无需重新处理应用...
ms.author: riande
ms.date: 10/13/2014
ms.assetid: 681a9204-462e-4260-9a0b-19f0644d6ad7
msc.legacyurl: /identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: e7461098f93bf64d6ff0d0e4ecdb64338f96be8b
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021763"
---
<a name="overview-of-custom-storage-providers-for-aspnet-identity"></a>ASP.NET 标识的自定义存储提供程序的概述
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET 标识是一个可扩展的系统，这样就可以创建自己的存储提供程序并将其插入到你的应用程序而无需重新使用该应用程序。 本主题介绍如何创建 ASP.NET 标识的自定义的存储提供程序。 它介绍了用于创建自己的存储提供程序的重要概念，但并不实现自定义存储提供程序的分步演练。
> 
> 实现自定义存储提供程序的示例，请参阅[实现自定义 MySQL ASP.NET 标识存储提供程序](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)。
> 
> 本主题已更新为使用 ASP.NET 标识 2.0。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - Visual Studio 2013 Update 2
> - ASP.NET 标识 2


## <a name="introduction"></a>介绍

默认情况下，ASP.NET 标识系统将用户信息存储在 SQL Server 数据库中，并使用 Entity Framework Code First 创建数据库。 对于许多应用程序，此方法也适用。 但是，您可能更愿意使用另一种持久性机制，例如 Azure 表存储，或者你可能已具有与默认实现非常不同的结构与数据库表。 在任一情况下，可以为你的存储机制编写自定义提供程序和该提供程序插入应用程序。

默认情况下，许多 Visual Studio 2013 模板中包含 ASP.NET 标识。 您可以获得通过 ASP.NET 标识的更新[Microsoft AspNet 标识 EntityFramework NuGet 包](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)。

本主题包括以下部分：

- [了解体系结构](#architecture)
- [了解存储的数据](#data)
- [创建数据访问层](#dal)
- [自定义用户类](#user)
- [自定义用户存储](#userstore)
- [自定义角色类](#role)
- [自定义角色存储](#rolestore)
- [重新配置应用程序以使用新的存储提供程序](#reconfigure)
- [自定义存储提供程序的其他实现](#other)

<a id="architecture"></a>
## <a name="understand-the-architecture"></a>了解体系结构

ASP.NET 标识包含的类称为管理器和存储。 管理器是用于执行操作，如 ASP.NET 标识系统中创建用户，应用程序开发人员的高级类。 存储区是指定如何保持实体，例如用户和角色，较低级别类。 存储紧密结合的永久保存机制，但管理器相互脱耦存储这意味着您可以替换持久性机制，而不会中断整个应用程序。

下图显示了如何将 web 应用程序交互与管理器，并存储与数据访问层进行交互。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image1.png)

若要创建 ASP.NET 标识的自定义的存储提供程序，必须使用此数据访问层中创建数据源、 数据访问层和交互的存储类。 你可以继续使用相同的管理器 Api 来执行数据操作的用户，但现在，数据保存到不同的存储系统。

不需要自定义管理器类，因为创建 UserManager 或 RoleManager 的新实例时提供的用户类的类型并将存储类的实例作为参数传递。 这种方法可以插入到现有结构的自定义的类。 您将了解如何使用您的部分中的自定义的存储类实例化 UserManager 和 RoleManager[重新配置应用程序以使用新的存储提供程序](#reconfigure)。

<a id="data"></a>
## <a name="understand-the-data-that-is-stored"></a>了解存储的数据

若要实现自定义存储提供程序，必须了解与 ASP.NET 标识一起使用的数据类型，并决定哪些功能是与应用程序相关。

| 数据 | 描述 |
| --- | --- |
| 用户 | 你的网站的已注册的用户。 包括用户 Id 和用户名称。 如果使用特定于你的站点的凭据登录的用户可能会包括经过哈希处理的密码 （而非从 Facebook 等外部站点使用的凭据），并指示是否有更改的内容中的用户凭据的安全戳。 可能还包含电子邮件地址、 电话号码，当前的数目是否启用双因素身份验证，失败登录名和帐户已被锁定。 |
| 用户声明 | 语句 （或声明），它表示用户的标识的用户有关的一组。 可以启用的用户的标识不是可以通过角色实现更大的表达式。 |
| 用户登录名 | 有关外部身份验证提供程序 （如 Facebook) 的信息日志记录使用户登录时使用。 |
| 角色 | 你的站点的授权组。 包含角色 Id 和角色名称 （如"管理员"或"Employee"）。 |

<a id="dal"></a>
## <a name="create-the-data-access-layer"></a>创建数据访问层

本主题假定你熟悉要使用的持久性机制以及如何创建实体，可用于该机制。 本主题不提供有关如何创建存储库或数据访问类; 的详细信息相反，它提供了有关设计决策地使用 ASP.NET 标识时所需一些建议。

有很多自由设计自定义的存储库时的存储提供程序。 只需创建要在应用程序中使用的功能的存储库。 例如，如果不在应用程序中使用角色，你不必创建存储的角色或用户角色。 你的技术和现有的基础结构可能需要与 ASP.NET Identity 的默认实现很大差异的结构。 数据访问层，在提供的逻辑以使用你的存储库的结构。

有关 MySQL 的实现，以 ASP.NET 标识 2.0 的数据存储库，请参阅[MySQLIdentity.sql](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)。

数据访问层中提供的逻辑将 ASP.NET 标识中的数据保存到数据源。 自定义的存储提供程序的数据访问层可能包括以下类用于存储用户和角色信息。

| 类 | 描述 | 示例 |
| --- | --- | --- |
| 上下文 | 若要连接到持久性机制并执行查询的信息进行封装。 此类是您的数据访问层的中心。 其他数据类将需要此类来执行其操作的实例。 此外将初始化您的存储类使用此类的实例。 | [MySQLDatabase](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) |
| 用户存储 | 存储和检索用户信息 （如用户名称和密码哈希）。 | [数据库 (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserTable.cs) |
| 角色存储 | 存储和检索角色信息 （例如角色名称）。 | [RoleTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleTable.cs) |
| UserClaims 存储 | 存储和检索用户声明信息 （如的声明类型和值）。 | [UserClaimsTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) |
| UserLogins 存储 | 存储和检索用户登录信息 （例如外部身份验证提供程序）。 | [UserLoginsTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) |
| UserRole 存储 | 存储和检索用户分配到哪些角色。 | [UserRoleTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) |

同样，您只需实现您打算在应用程序中使用的类。

在数据访问类中，提供的代码以执行特定的永久性机制的数据操作。 例如，在 MySQL 实现中，数据库类包含用于将一条新记录插入到用户数据库表的方法。 命名的变量`_database`是 MySQLDatabase 类的实例。

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample1.cs)]

在创建后的数据访问类，必须创建在数据访问层中调用特定方法的存储类。

<a id="user"></a>
## <a name="customize-the-user-class"></a>自定义用户类

在实现自己的存储提供程序时，您必须创建一个用户类等效于[IdentityUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser(v=vs.108).aspx)类[Microsoft.ASP.NET.Identity.EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx)命名空间：

下图显示了必须创建的 IdentityUser 类和要在此类中实现的接口。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image2.png)

[IUser&lt;TKey&gt; ](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx)接口定义 UserManager 尝试执行请求的操作时要调用的属性。 此接口包含两个属性的 Id 和用户名。 [IUser&lt;TKey&gt; ](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx)接口，可指定的键的用户通过泛型类型**TKey**参数。 Id 属性的类型匹配 TKey 参数的值。

标识框架还提供了[IUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.iuser(v=vs.108).aspx)接口 （如果不使用泛型参数） 时，你想要对密钥使用一个字符串值。

IdentityUser 类实现 IUser，并包含任何其他属性或构造函数为您的网站上的用户。 下面的示例演示一个键使用整数的 IdentityUser 类。 Id 字段设置为**int**以匹配的泛型参数的值。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample2.cs)]

 有关完整实现，请参阅[IdentityUser (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityUser.cs)。 

<a id="userstore"></a>
## <a name="customize-the-user-store"></a>自定义用户存储

您还创建一个 UserStore 类，提供用户的所有数据操作的方法。 此类是等效于[UserStore&lt;TUser&gt; ](https://msdn.microsoft.com/library/dn315446(v=vs.108).aspx)类[Microsoft.ASP.NET.Identity.EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx)命名空间。 在 UserStore 类中，您实现[IUserStore&lt;TUser、 TKey&gt; ](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx)和任何可选接口。 您选择实现的可选接口基于您希望在应用程序中提供的功能。

下图显示了必须创建到 UserStore 类和相关的接口。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image3.png)

在 Visual Studio 中的默认项目模板包含假设已在用户存储中实现许多可选接口的代码。 如果与自定义的用户存储区一起使用的默认模板，在必须在用户存储区实现可选接口，或更改了模板代码，不能再调用中尚未实现的接口的方法。

 下面的示例演示一个简单的用户存储类。 **TUser**泛型参数将你的用户类的通常是您定义的 IdentityUser 类的类型。 **TKey**泛型参数将用户密钥的类型。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample3.cs)]

 在此示例中，构造函数采用参数名为*数据库*ExampleDatabase 是仅举例说明了如何在您的数据访问类中传递的类型。 例如，在 MySQL 实现中，此构造函数采用类型 MySQLDatabase 的参数。 

在 UserStore 类中，您可以使用您创建的用于执行操作的数据访问类。 例如，在 MySQL 实现中，到 UserStore 类具有使用数据库的实例来插入新记录的 CreateAsync 方法。 **插入**方法**数据库**对象是在上一部分中所示的相同方法。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample4.cs)]

### <a name="interfaces-to-implement-when-customizing-user-store"></a>要实现自定义用户存储区时接口

下图显示每个接口中定义的功能的更多详细信息。 所有可选接口继承自 IUserStore。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image4.png)

- **IUserStore**  
  [IUserStore&lt;TUser、 TKey&gt; ](https://msdn.microsoft.com/library/dn613278(v=vs.108).aspx)接口是在用户存储中必须实现的唯一接口。 它定义用于创建、 更新、 删除和检索用户的方法。
- **IUserClaimStore**  
  [IUserClaimStore&lt;TUser、 TKey&gt; ](https://msdn.microsoft.com/library/dn613265(v=vs.108).aspx)接口定义的方法必须在你的用户存储区，若要启用用户声明实现。 它包含方法或添加、 删除和检索用户声明。
- **IUserLoginStore**  
  [IUserLoginStore&lt;TUser、 TKey&gt; ](https://msdn.microsoft.com/library/dn613272(v=vs.108).aspx)定义的方法必须在您的用户存储区以启用外部身份验证提供程序中实现。 它包含用于添加、 删除和检索用户登录名和用于检索用户的登录信息基于方法的方法。
- **IUserRoleStore**  
  [IUserRoleStore&lt;TKey，TUser&gt; ](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx)接口定义的方法必须在用户存储将用户映射到角色中实现。 它包含方法以添加、 删除和检索用户的角色和一个方法以检查是否将用户分配到角色。
- **IUserPasswordStore**  
  [IUserPasswordStore&lt;TUser、 TKey&gt; ](https://msdn.microsoft.com/library/dn613273(v=vs.108).aspx)接口定义必须在用户存储来持久保存中实现的方法进行密码哈希处理。 它包含用于获取和设置哈希的密码和用于指示用户是否已设置密码的方法的方法。
- **IUserSecurityStampStore**  
  [IUserSecurityStampStore&lt;TUser、 TKey&gt; ](https://msdn.microsoft.com/library/dn613277(v=vs.108).aspx)接口定义用户存储要用于安全戳，该值指示是否已更改用户的帐户信息中必须实现的方法. 用户更改密码，或添加或删除登录名时，将更新此 stamp。 它包含方法用于获取和设置的安全戳。
- **IUserTwoFactorStore**  
  [IUserTwoFactorStore&lt;TUser、 TKey&gt; ](https://msdn.microsoft.com/library/dn613279(v=vs.108).aspx)接口定义必须实现到实现双因素身份验证的方法。 它包含用于获取和设置是否为用户启用双因素身份验证方法。
- **IUserPhoneNumberStore**  
  [IUserPhoneNumberStore&lt;TUser、 TKey&gt; ](https://msdn.microsoft.com/library/dn613275(v=vs.108).aspx)接口定义必须实现以存储用户电话号码的方法。 它包含用于获取和设置的电话号码和电话号码是否已确认的方法。
- **IUserEmailStore**  
  [IUserEmailStore&lt;TUser、 TKey&gt; ](https://msdn.microsoft.com/library/dn613143(v=vs.108).aspx)接口定义必须实现以存储用户的电子邮件地址的方法。 它包含用于获取和设置的电子邮件地址和电子邮件是否已确认的方法。
- **IUserLockoutStore**  
  [IUserLockoutStore&lt;TUser、 TKey&gt; ](https://msdn.microsoft.com/library/dn613271(v=vs.108).aspx)接口定义为存储帐户的锁定信息而必须实现的方法。 它包含用于获取当前的失败的访问尝试次数、 获取和设置是否可以锁定该帐户，获取和设置锁定结束日期，数量递增失败的尝试，和重置失败尝试次数的方法。
- **IQueryableUserStore**  
  [IQueryableUserStore&lt;TUser、 TKey&gt; ](https://msdn.microsoft.com/library/dn613267(v=vs.108).aspx)接口定义必须实现以提供可查询的用户存储区的成员。 它包含一个属性，保存可查询的用户。

  在应用程序; 实现所需的接口例如，IUserClaimStore、 IUserLoginStore、 IUserRoleStore、 IUserPasswordStore 和 IUserSecurityStampStore 接口，如下所示。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample5.cs)]

有关完整实现 （包括所有接口），请参阅[UserStore (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserStore.cs)。

### <a name="identityuserclaim-identityuserlogin-and-identityuserrole"></a>IdentityUserClaim、 IdentityUserLogin 和 IdentityUserRole

Microsoft.AspNet.Identity.EntityFramework 命名空间包含的实现[IdentityUserClaim](https://msdn.microsoft.com/library/dn613250(v=vs.108).aspx)， [IdentityUserLogin](https://msdn.microsoft.com/library/dn613251(v=vs.108).aspx)，并[IdentityUserRole](https://msdn.microsoft.com/library/dn613252(v=vs.108).aspx)类。 如果使用这些功能，您可能想要创建这些类的版本并定义你的应用程序的属性。 但是，有时它是更高效，若要执行基本操作 （如添加或删除用户的声明） 时不将这些实体加载到内存。 相反后, 端存储类可以执行这些操作直接在数据源上。 例如，UserStore.GetClaimsAsync() 方法可以调用 userClaimTable.FindByUserId(user.Id) 方法来执行查询，在直接表并返回声明的列表。

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample6.cs)]

<a id="role"></a>
## <a name="customize-the-role-class"></a>自定义角色类

在实现自己的存储提供程序时，您必须创建一个角色类等效于[IdentityRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityrole(v=vs.108).aspx)类[Microsoft.ASP.NET.Identity.EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx)命名空间：

下图显示了必须创建 IdentityRole 类和要在此类中实现的接口。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image5.png)

[IRole&lt;TKey&gt; ](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx)接口定义 RoleManager 尝试执行请求的操作时要调用的属性。 此接口包含两个属性的 Id 和名称。 [IRole&lt;TKey&gt; ](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx)接口，可指定的密钥的通过泛型类型**TKey**参数。 Id 属性的类型匹配 TKey 参数的值。

标识框架还提供了[IRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.irole(v=vs.108).aspx)接口 （如果不使用泛型参数） 时，你想要对密钥使用一个字符串值。

下面的示例演示一个使用整数键的 IdentityRole 类。 Id 字段设置为 int，以匹配的泛型参数的值。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample7.cs)]

 有关完整实现，请参阅[IdentityRole (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityRole.cs)。 

<a id="rolestore"></a>
## <a name="customize-the-role-store"></a>自定义角色存储

您还创建一个 RoleStore 类，提供对角色的所有数据操作的方法。 此类是等效于[RoleStore&lt;TRole&gt; ](https://msdn.microsoft.com/library/dn468181(v=vs.108).aspx) Microsoft.ASP.NET.Identity.EntityFramework 命名空间中的类。 在您 RoleStore 的类，你将实现[IRoleStore&lt;TRole、 TKey&gt; ](https://msdn.microsoft.com/library/dn613266(v=vs.108).aspx)和 （可选） [IQueryableRoleStore&lt;TRole、 TKey&gt; ](https://msdn.microsoft.com/library/dn613262(v=vs.108).aspx)接口。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image6.png)

下面的示例显示了角色存储类。 TRole 泛型参数将你的角色类的通常是您定义的 IdentityRole 类的类型。 TKey 泛型参数将角色参数的类型。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample8.cs)]

- **IRoleStore&lt;TRole&gt;**  
  [IRoleStore](https://msdn.microsoft.com/library/dn468195.aspx)接口定义角色存储类中实现的方法。 它包含用于创建、 更新、 删除和检索角色的方法。
- **RoleStore&lt;TRole&gt;**  
  若要自定义 RoleStore，请创建实现 IRoleStore 接口的类。 只需实现此类，如果想要使用你的系统上的角色。 采用一个名为参数的构造函数*数据库*ExampleDatabase 是仅举例说明了如何在您的数据访问类中传递的类型。 例如，在 MySQL 实现中，此构造函数采用类型 MySQLDatabase 的参数。  
  
  有关完整实现，请参阅[RoleStore (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleStore.cs) 。

<a id="reconfigure"></a>
## <a name="reconfigure-application-to-use-new-storage-provider"></a>重新配置应用程序以使用新的存储提供程序

您已实现新的存储提供程序。 现在，你必须配置应用程序以使用此存储提供程序。 如果你的项目中包括默认存储提供程序，必须删除默认的提供程序并将其替换为您的提供程序。

### <a name="replace-default-storage-provider-in-mvc-project"></a>替换为在 MVC 项目中的默认存储提供程序

1. 在中**管理 NuGet 包**窗口中，卸载**Microsoft ASP.NET 标识 EntityFramework**包。 可以通过 Identity.EntityFramework 搜索已安装包中找到此包。  
    ![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image7.png) 系统将要求是否还想要卸载实体框架。 如果不在你的应用程序的其他部分需要它，则可以卸载它。
2. 在模型文件夹中 IdentityModels.cs 文件中，删除或注释掉**ApplicationUser**并**ApplicationDbContext**类。 在 MVC 应用程序，可以删除整个 IdentityModels.cs 文件。 在 Web 窗体应用程序中，删除两个类，但请确保保留也位于 IdentityModels.cs 文件的帮助器类。
3. 如果您的存储提供程序驻留在一个单独的项目，在 web 应用程序中添加对它的引用。
4. 替换为对所有引用`using Microsoft.AspNet.Identity.EntityFramework;`使用 using 语句的命名空间的存储提供程序。
5. 在中**Startup.Auth.cs**类中，更改**ConfigureAuth**方法以使用适当的上下文的单个实例。 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample9.cs?highlight=3)]
6. 在应用程序\_启动文件夹中，打开**IdentityConfig.cs**。 在 ApplicationUserManager 类中，更改**创建**方法以返回使用自定义的用户存储区的用户管理器。 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample10.cs?highlight=3)]
7. 替换为对所有引用**ApplicationUser**与**IdentityUser**。
8. 默认项目中未在 IUser 接口; 中定义用户类包含一些成员例如，电子邮件、 PasswordHash 和 GenerateUserIdentityAsync。 如果您的用户类不具有这些成员，您必须实现它们，或更改使用这些成员的代码。
9. 如果已创建 RoleManager 任何实例，更改代码，从而使用新 RoleStore 类。  

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample11.cs)]
10. 默认项目专为具有键的字符串值的用户类。 如果您的用户类具有不同的类型 （如整数） 的密钥，则必须更改项目以使用你的类型。 请参阅[更改为在 ASP.NET 标识中的用户的主键](change-primary-key-for-users-in-aspnet-identity.md)。
11. 如果需要将连接字符串添加到 Web.config 文件中。

<a id="other"></a>
## <a name="other-resources"></a>其他资源

- 博客：[实现 ASP.NET 标识](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- 教程和 GIT 的代码： [Simple.Data Asp.Net 标识提供程序](http://designcoderelease.blogspot.co.uk/2015/03/simpledata-aspnet-identity-provider.html)
- 教程：[设置了基本的标识帐户，并指向外部 DB](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)。 通过[ @xivSolutions ](https://twitter.com/xivSolutions)。
- 教程[： 实现自定义 MySQL ASP.NET 标识存储提供程序](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- [CodeFluent 实体](http://blog.codefluententities.com/2014/04/30/asp-net-identity-v2-and-codefluent-entities/)通过[SoftFluent](http://www.softfluent.com/)
- [Azure 表存储](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/)由 James randall 简要介绍。
- Azure 表存储： [AspNet.Identity.TableStorage](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage)通过[ @stuartleeks ](https://twitter.com/stuartleeks)。
- [CouchDB / 通过 Daniel Wertheim Cloudant。](https://github.com/danielwertheim/mycouch.aspnet.identity)
- 弹性搜索[h： 弹性标识](https://github.com/bmbsqd/elastic-identity)通过 Bombsquad AB.
- [MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/)由 Jonathan Sheely Jonathan Sheely。
- [NHibernate.AspNet.Identity](https://github.com/milesibastos/NHibernate.AspNet.Identity) Antônio Milesi Bastos 通过。
- [RavenDB](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0)由[ @tourismgeek ](https://twitter.com/tourismgeek)。
- [RavenDB.AspNet.Identity](https://github.com/ILMServices/RavenDB.AspNet.Identity)由[ILMServices](http://www.ilmservice.com/)。
- Redis: [Redis.AspNet.Identity](https://github.com/aminjam/Redis.AspNet.Identity)
- 针对"数据库优先"的用户存储区的 T4 模板以生成 EF 代码： [AspNet.Identity.EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)
