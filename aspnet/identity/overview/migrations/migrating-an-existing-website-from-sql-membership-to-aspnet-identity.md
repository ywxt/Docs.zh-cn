---
uid: identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
title: 从 SQL 成员身份的现有网站迁移到 ASP.NET 标识 |Microsoft Docs
author: Rick-Anderson
description: 本教程说明了步骤来迁移现有 web 应用程序具有用户和创建使用新的 ASP.NET 标识的 SQL 成员资格的角色数据...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/19/2014
ms.topic: article
ms.assetid: 220d3d75-16b2-4240-beae-a5b534f06419
ms.technology: ''
msc.legacyurl: /identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 7df2c9a6cccefd3c4f3022c14627394557543258
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389121"
---
<a name="migrating-an-existing-website-from-sql-membership-to-aspnet-identity"></a>从 SQL 成员身份的现有网站迁移到 ASP.NET 标识
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)， [Suhas Joshi](https://github.com/suhasj)

> 本教程说明了将迁移角色的数据创建新的 ASP.NET 标识系统中使用 SQL 成员资格用户与现有 web 应用程序的步骤。 这种方法涉及到一个 ASP.NET 标识和挂钩到它的新/老类中所需的更改现有数据库架构。 您采用此方法后将数据库迁移后，将轻松处理标识对将来的更新。


对于本教程，我们将使用 Visual Studio 2010 创建用户和角色的数据创建一个 web 应用程序模板 （Web 窗体）。 然后，我们将使用 SQL 脚本来将现有数据库迁移到所需的标识系统表。 接下来我们将安装所需的 NuGet 包并添加新帐户管理页用于成员资格管理标识系统。 为迁移的测试，创建使用 SQL 成员资格的用户应该能够以用户身份登录，新用户应能注册。 您可以找到完整示例[此处](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/SQLMembership-Identity-OWIN/)。 另请参阅[从 ASP.NET 成员身份迁移到 ASP.NET 标识](http://travis.io/blog/2015/03/24/migrate-from-aspnet-membership-to-aspnet-identity.html)。

## <a name="getting-started"></a>入门

### <a name="creating-an-application-with-sql-membership"></a>使用 SQL 成员资格创建应用程序

1. 我们需要以开头的现有应用程序使用 SQL 成员身份，并且有用户和角色的数据。 对于本文，让我们在 Visual Studio 2010 中创建 web 应用程序。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.jpg)
2. 使用 ASP.NET 配置工具中，创建 2 个用户： **oldAdminUser**和**oldUser。**

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.jpg)
3. 创建一个名为管理员角色并将 oldAdminUser 添加为该角色的用户。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.png)
4. 使用 Default.aspx 创建站点的管理部分。 若要启用只能访问管理员角色中的用户在 web.config 文件中设置授权标记。 可在此处找到详细信息 [https://www.asp.net/web-forms/tutorials/security/roles/role-based-authorization-cs](../../../web-forms/overview/older-versions-security/roles/role-based-authorization-cs.md)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.png)
5. 查看数据库在服务器资源管理器，若要了解 SQL 成员资格系统所创建的表。 用户登录数据存储在 aspnet\_用户和 aspnet\_表中的成员身份，而角色数据存储在 aspnet\_Roles 表。 有关哪些用户可以在哪些角色存储在 aspnet 信息\_UsersInRoles 表。 基本成员资格管理便已足够移植到 ASP.NET 标识系统上述表中的信息。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.png)

### <a name="migrating-to-visual-studio-2013"></a>迁移到 Visual Studio 2013

1. 安装 Visual Studio Express 2013 for Web 或与 Visual Studio 2013[最新的更新](https://www.microsoft.com/download/details.aspx?id=44921)。
2. 已安装版本的 Visual Studio 中打开的更高版本的项目。 如果在计算机上未安装 SQL Server Express，打开项目，因为连接字符串使用 SQL Express 时显示一条提示。 您可以选择要安装 SQL Express 或作为变通解决更改到 LocalDb 连接字符串。 本文中我们会将其更改为 LocalDb。
3. 打开 web.config 并更改中的连接字符串。到 (LocalDb)，为 v11.0 SQLExpess。 删除用户实例 = true 连接字符串。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.jpg)
4. 打开服务器资源管理器并验证可以观察表架构和数据。
5. ASP.NET 标识系统适用于版本 4.5 或更高版本的 framework。 重定目标到 4.5 或更高版本的应用程序。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image5.png)

    生成项目以验证有任何错误。

### <a name="installing-the-nuget-packages"></a>安装 Nuget 包

1. 在解决方案资源管理器中右键单击该项目&gt;**管理 NuGet 包**。 在搜索框中，输入"Asp.net 标识"。 在结果列表中选择的包，然后单击安装。 通过单击"我接受"按钮接受许可协议。 请注意，此包将安装依赖项包： EntityFramework 和 Microsoft ASP.NET 标识 Core。 同样安装以下包 （如果不想要启用 OAuth 登录，请跳过最后 4 个 OWIN 包）：

   - Microsoft.AspNet.Identity.Owin
   - Microsoft.Owin.Host.SystemWeb
   - Microsoft.Owin.Security.Facebook
   - Microsoft.Owin.Security.Google
   - Microsoft.Owin.Security.MicrosoftAccount
   - Microsoft.Owin.Security.Twitter

     ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image6.png)

### <a name="migrate-database-to-the-new-identity-system"></a>将数据库迁移到新的标识系统

下一步是将现有数据库迁移到 ASP.NET 标识系统所需的架构。 若要实现此我们运行 SQL 脚本拥有一组命令以创建新表并将现有的用户信息迁移到新表。 可以找到脚本文件[此处](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/SQLMembership-Identity-OWIN/Migrations.sql)。

此脚本文件是特定于此示例。 如果创建的表的架构使用 SQL 成员资格自定义或修改的脚本需要相应地更改。

### <a name="how-to-generate-the-sql-script-for-schema-migration"></a>如何生成架构迁移的 SQL 脚本

若要运行的现有用户数据使用现成的 ASP.NET 标识类，我们需要将数据库架构迁移到所需的 ASP.NET 标识。 我们可以通过添加新表并将现有的信息复制到这些表来执行此操作。 默认情况下 ASP.NET 标识使用 EntityFramework 标识模型类映射回数据库来存储/检索的信息。 这些模型类实现核心标识接口定义用户和角色对象。 表和数据库中的列基于这些模型的类。 EntityFramework 模型中的类标识 v2.1.0 和它们的属性是定义如下

| **IdentityUser** | **Type** | **IdentityRole** | **IdentityUserRole** | **IdentityUserLogin** | **IdentityUserClaim** |
| --- | --- | --- | --- | --- | --- |
| Id | 字符串 | Id | RoleId | ProviderKey | Id |
| 用户名 | 字符串 | name | 用户 Id | 用户 Id | ClaimType |
| PasswordHash | 字符串 |  |  | LoginProvider | ClaimValue |
| SecurityStamp | 字符串 |  |  |  | 用户\_Id |
| 电子邮件 | 字符串 |  |  |  |  |
| EmailConfirmed | bool |  |  |  |  |
| 电话号码 | 字符串 |  |  |  |  |
| PhoneNumberConfirmed | bool |  |  |  |  |
| LockoutEnabled | bool |  |  |  |  |
| LockoutEndDate | DateTime |  |  |  |  |
| AccessFailedCount | int |  |  |  |  |

我们需要为每个这些模型的表具有与属性相对应的列。 在中定义的类与表之间的映射`OnModelCreating`方法的`IdentityDBContext`。 这称为配置的 fluent API 方法，可找到更多信息[此处](https://msdn.microsoft.com/data/jj591617.aspx)。 类的配置是如下所示

| **类** | **Table** | **主键** | **外键** |
| --- | --- | --- | --- |
| IdentityUser | AspnetUsers | Id |  |
| IdentityRole | AspnetRoles | Id |  |
| IdentityUserRole | AspnetUserRole | 用户 Id + RoleId | 用户\_Id-&gt;AspnetUsers RoleId-&gt;AspnetRoles |
| IdentityUserLogin | AspnetUserLogins | ProviderKey + UserId + LoginProvider | 用户 Id-&gt;AspnetUsers |
| IdentityUserClaim | AspnetUserClaims | Id | 用户\_Id-&gt;AspnetUsers |

使用此信息，我们可以创建 SQL 语句来创建新表。 我们可以单独编写每个语句，或生成整个脚本根据需要使用我们然后可以编辑的 EntityFramework PowerShell 命令。 为此，VS 开放**程序包管理器控制台**从**视图**或**工具**菜单

- 运行命令"Enable-migrations"以启用 EntityFramework 迁移。
- 运行命令"添加迁移初始"，这将创建在 C# 中创建数据库的初始设置代码 / vb。
- 最后一步是运行"更新数据库-脚本"生成 SQL 脚本的命令基于模型的类。

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

此数据库生成脚本可用作其中我们会进行其他更改，以添加新列并将数据复制开始。 这样做的优点是，我们生成`_MigrationHistory`EntityFramework 用于模型的类标识发布的未来版本的更改时，修改数据库架构的表。 

SQL 成员资格用户信息有其他属性标识用户模型类即电子邮件中的属性、 密码尝试次数、 上次登录日期、 最后一个锁定日期等。这是有用的信息，我们想让它转入标识系统。 这可以通过将其他属性添加到用户模型并将其映射回数据库中表的列。 我们可以执行此操作，请添加该子类`IdentityUser`模型。 我们可以将属性添加到此自定义类和编辑 SQL 脚本，以创建表时添加相应的列。 此类的代码是一文中作了进一步介绍。 用于创建的 SQL 脚本`AspnetUsers`表后会添加新属性

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample1.sql)]

接下来我们需要将现有的信息从 SQL 成员资格数据库复制到新添加的表，用于标识。 这可以通过 SQL 将数据直接从一个表复制到另一个。 若要将数据添加到表中的行，我们使用`INSERT INTO [Table]`构造。 若要从另一个表，我们可以使用复制`INSERT INTO`语句以及`SELECT`语句。 若要获取我们需要进行查询的所有用户信息*aspnet\_用户*并*aspnet\_成员身份*表和复制数据的*AspNetUsers*表。 我们使用`INSERT INTO`并`SELECT`连同`JOIN`和`LEFT OUTER JOIN`语句。 有关查询和表之间复制数据的详细信息，请参阅[这](https://technet.microsoft.com/library/ms190750%28v=sql.105%29.aspx)链接。 此外 AspnetUserLogins 和 AspnetUserClaims 表是空的开始时由于没有在默认情况下映射到此 SQL 成员资格信息。 复制的唯一信息是用户和角色。 对于在前述步骤中创建的项目，将为要将信息复制到用户表的 SQL 查询

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample2.sql)]

在上述 SQL 语句中，从每个用户的信息*aspnet\_用户*并*aspnet\_成员身份*表复制到的列*AspnetUsers*表。 当我们复制的密码时，此处这样做的唯一修改。 由于 SQL 成员资格中的密码的加密算法使用 PasswordSalt 和 PasswordFormat，我们将复制的太以及经过哈希处理密码，以便可以使用用于解密密码的标识。 这当挂接自定义密码哈希计算器文章中进一步说明。 

此脚本文件是特定于此示例。 对于具有其他表的应用程序，开发人员可以按照类似的方法上用户 model 类添加其他属性，并将它们映射到在 AspnetUsers 表中的列。 若要运行脚本，

1. 打开服务器资源管理器。 展开要显示表的 ApplicationServices 连接。 右键单击表节点并选择新建查询选项

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image7.png)
2. 在查询窗口中，复制并粘贴 Migrations.sql 文件中的整个 SQL 脚本。 通过点击执行箭头按钮来运行脚本文件。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.jpg)

    刷新服务器资源管理器窗口。 在数据库中创建五个新表。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image8.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image9.png)

    下面是 SQL 成员资格表中的信息映射到新的标识系统的方式。

    aspnet\_角色-&gt; AspNetRoles

    asp\_netUsers 和 asp\_netMembership-&gt; AspNetUsers

    aspnet\_UserInRoles-&gt; AspNetUserRoles

    上面的节中所述，AspNetUserClaims 和 AspNetUserLogins 表是空的。 AspNetUser 表中的鉴别器字段应与下一步定义模型类名称匹配。 PasswordHash 列也处于窗体加密的密码 | 密码 salt | 密码格式。 这使您可以使用特殊 SQL 成员资格加密逻辑，以便可以重复使用旧密码。 是本文后面所述。

### <a name="creating-models-and-membership-pages"></a>创建模型和成员资格页

前面曾提到，标识功能将使用实体框架与用于默认情况下存储帐户信息的数据库。 若要使用表中的现有数据，我们需要创建模型类映射回表并将它们连接起来，标识系统中。 作为标识协定的一部分，在 model 类应实现 Identity.Core dll 中定义的接口，或可以扩展现有 Microsoft.AspNet.Identity.EntityFramework 中提供这些接口的实现。

在本示例中，AspNetRoles、 AspNetUserClaims、 AspNetLogins 和 AspNetUserRole 表具有类似于标识系统的现有实现的列。 因此我们可以重复使用现有的类将映射到这些表。 AspNetUser 表有一些额外的列将用它们来存储 SQL 成员资格表中的其他信息。 这可以通过创建模型类，可以扩展 IdentityUser 的现有实现并添加其他属性映射。

1. 在项目中的可用来创建 Models 文件夹，并添加用户的类。 类的名称应与 AspnetUsers 表中的鉴别器列中添加的数据。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image10.png)

    用户类应扩展中找到的 IdentityUser 类*Microsoft.AspNet.Identity.EntityFramework* dll。 声明映射回 AspNetUser 列在类中的属性。 属性 ID、 用户名、 PasswordHash 和 SecurityStamp IdentityUser 中定义，并省略了这些。 下面是具有所有属性的用户类的代码

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample3.cs)]
2. 实体框架 DbContext 类，才能保留在模型中返回到表的数据，并从要填充模型的表中检索数据。 *Microsoft.AspNet.Identity.EntityFramework* dll 定义与标识表检索和存储的信息进行交互的 IdentityDbContext 类。 IdentityDbContext&lt;tuser&gt;采用 TUser 类可以是任何类来扩展 IdentityUser 类。

    创建一个新类扩展传递在步骤 1 中创建的用户类中的模型文件夹下的 IdentityDbContext 的 ApplicationDBContext

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample4.cs)]
3. 完成新的标识系统中的用户管理使用 UserManager&lt;tuser&gt;类中定义*Microsoft.AspNet.Identity.EntityFramework* dll。 我们需要创建自定义类来扩展 UserManager，传递在步骤 1 中创建的用户类中。

    在模型文件夹中创建一个新类扩展了 UserManager UserManager&lt;用户&gt;

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample5.cs)]
4. 应用程序的用户的密码进行加密和存储在数据库中。 SQL 成员资格中使用的加密算法与新的标识系统中的一个不同。 若要重复使用旧密码，我们需要旧用户登录时使用的标识中的新用户的加密算法使用 SQL 成员资格算法时有选择地解密密码。

    UserManager 类有一个属性存储的实现 IPasswordHasher 接口的类实例的 PasswordHasher。 这用来在用户身份验证的事务期间加密/解密密码。 在步骤 3 中定义的 UserManager 类，创建一个新类 SQLPasswordHasher 和复制下面的代码。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample6.cs)]

    通过导入 System.Text 和 System.Security.Cryptography 命名空间解决编译错误。

    EncodePassword 方法对默认 SQL 成员资格加密实现根据密码进行加密。 这是来自 System.Web dll。 如果旧的应用使用自定义实现则它应反映此处。 我们需要定义其他两种方法*HashPassword*并*VerifyHashedPassword*使用*EncodePassword*给定的密码哈希或验证纯文本方法与一个现有数据库中的密码。

    SQL 成员资格系统使用 PasswordHash 和 PasswordSalt PasswordFormat 注册或更改其密码时，用户输入的密码进行哈希。 在迁移期间所有三个字段存储分隔 AspNetUser 表中的 PasswordHash 列在 | 字符。 当用户登录，密码包含这些字段时，我们使用 SQL 成员资格加密来检查密码;否则我们使用标识系统的默认加密来验证该密码。 这种方式旧用户不必迁移应用程序后更改其密码。
5. UserManager 类的构造函数声明并将此作为 SQLPasswordHasher 传递给构造函数中的属性。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample7.cs)]

### <a name="create-new-account-management-pages"></a>创建新的帐户管理页

迁移的下一步是添加将允许用户注册和登录的帐户管理页。 从 SQL 成员资格的旧帐户页面使用新的标识系统不支持的控件。 若要添加新用户管理页面，请按照此链接处的教程[ https://www.asp.net/identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project ](../getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md)从步骤添加 Web 窗体用于注册到你的应用程序的用户由于我们已创建项目并添加 NuGet包。

我们需要进行一些更改以使用我们在这里的项目的示例。

- Register.aspx.cs 和 Login.aspx.cs 代码隐藏类使用`UserManager`从标识包创建的用户。 对于此示例使用 UserManager Models 文件夹中添加前面所述的步骤。
- 使用而不是 IdentityUser Register.aspx.cs 和 Login.aspx.cs 代码隐藏类中创建的用户类。 这在我们的自定义用户类挂接到标识系统。
- 要创建数据库的部件，可以跳过。
- 开发人员需要设置新用户 ApplicationId，以匹配当前应用程序 id。 这可以通过查询此应用程序 ApplicationId 之前 Register.aspx.cs 类中创建一个用户对象并将其设置前创建用户。 

    示例:

    定义一个方法中 Register.aspx.cs 页后，可以查询 aspnet\_应用程序表，并根据应用程序名称获取应用程序 Id

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample8.cs)]

    现在获取或设置此用户对象上

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample9.cs)]

使用旧的用户名和密码登录现有用户。 使用注册页来创建新用户。 此外验证用户在角色中，与预期一致。

移植到标识系统可帮助用户可以将开放式身份验证 (OAuth) 添加到应用程序。 该示例，请参阅[此处](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/SQLMembership-Identity-OWIN/)具有启用了 OAuth。

## <a name="next-steps"></a>后续步骤

在本教程中我们介绍了如何移植到 ASP.NET 标识用户从 SQL 成员资格，但我们没有端口配置文件数据。 在下一教程中，我们将了解到移植到新的标识系统的配置文件数据从 SQL 成员资格。

可以将保留在本文底部的反馈。

*感谢 Tom Dykstra 和 Rick Anderson 对本文的审阅。*
