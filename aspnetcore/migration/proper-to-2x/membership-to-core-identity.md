---
title: ASP.NET 成员资格身份验证从迁移到 ASP.NET 核心 2.0 标识
author: isaac2004
description: 了解如何迁移现有的 ASP.NET 应用程序使用成员资格到 ASP.NET 核心 2.0 标识的身份验证。
ms.author: scaddie
ms.custom: mvc
ms.date: 04/24/2018
uid: migration/proper-to-2x/membership-to-core-identity
ms.openlocfilehash: 3ec22713997a74b587ef5d18e71a28668a5481e2
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36274100"
---
# <a name="migrate-from-aspnet-membership-authentication-to-aspnet-core-20-identity"></a>ASP.NET 成员资格身份验证从迁移到 ASP.NET 核心 2.0 标识

作者：[Isaac Levin](https://isaaclevin.com)

本文演示如何迁移使用成员资格到 ASP.NET 核心 2.0 标识的身份验证的 ASP.NET 应用程序的数据库架构。

> [!NOTE]
> 本文档提供将基于 ASP.NET 成员资格的应用程序的数据库架构迁移到用于 ASP.NET 核心标识的数据库架构所需的步骤。 有关从基于 ASP.NET 成员身份的身份验证迁移到 ASP.NET Identity 的详细信息，请参阅[将从 SQL 成员资格的现有应用程序迁移到 ASP.NET 标识](/aspnet/identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity)。 有关 ASP.NET 核心标识的详细信息，请参阅[ASP.NET Core 上的标识简介](xref:security/authentication/identity)。

## <a name="review-of-membership-schema"></a>成员资格架构评审

在 ASP.NET 2.0 中之前, 开发人员已执行的任务创建为其应用程序的整个身份验证和授权过程。 ASP.NET 2.0 中，成员身份已引入，提供处理的 ASP.NET 应用程序内的安全的样本解决方案。 开发人员现在已能够启动到使用 SQL Server 数据库的架构[aspnet_regsql.exe](https://msdn.microsoft.com/library/ms229862.aspx)命令。 运行此命令后下, 表在数据库中创建。

  ![成员资格表](identity/_static/membership-tables.png)

若要将现有应用迁移到 ASP.NET 核心 2.0 标识，这些表中的数据需要迁移到使用新的标识架构的表。

## <a name="aspnet-core-identity-20-schema"></a>ASP.NET 核心标识 2.0 架构

ASP.NET 核心 2.0 遵循[标识](/aspnet/identity/index)ASP.NET 4.5 中引入的原则。 尽管共享的原则，框架之间的实现是不同的甚至 ASP.NET 核心的版本之间 (请参阅[将身份验证和标识迁移到 ASP.NET 核心 2.0](xref:migration/1x-to-2x/index))。

ASP.NET 核心 2.0 标识查看架构的最快方法是创建新的 ASP.NET 核心 2.0 应用程序。 请按照下列步骤在 Visual Studio 2017:

* 选择“文件” > “新建” > “项目”。
* 创建一个新**ASP.NET 核心 Web 应用程序**，并将项目*CoreIdentitySample*。
* 在下拉列表中选择“ASP.NET Core 2.0”，然后选择“Web 应用程序”。 此模板生成[Razor 页](xref:razor-pages/index)应用。 然后单击**确定**，单击**更改身份验证**。
* 选择**单个用户帐户**标识模板。 最后，单击**确定**，然后**确定**。 Visual Studio 创建项目时使用 ASP.NET 核心标识模板。

ASP.NET 核心 2.0 标识使用[实体框架核心](/ef/core)与存储的身份验证数据的数据库进行交互。 为了使新创建应用程序处理，需要使用数据库来存储此数据。 在创建新的应用程序后, 检查数据库环境中的架构的最快方法是创建使用实体框架迁移的数据库。 此过程创建数据库，或者本地或其他位置，其中模仿该架构。 查看前面的文档以了解更多信息。

若要使用 ASP.NET 核心标识架构中创建数据库，运行`Update-Database`命令在 Visual Studio 的**程序包管理器控制台**(PMC) 窗口&mdash;位于**工具** > **NuGet 包管理器** > **程序包管理器控制台**。 PMC 支持实体框架中运行命令。

实体框架命令使用连接字符串中指定的数据库为*appsettings.json*。 以下连接字符串上的目标数据库*localhost*名为*asp net 核心标识*。 在此设置中，实体框架配置为使用`DefaultConnection`连接字符串。

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=aspnet-core-identity;Trusted_Connection=True;MultipleActiveResultSets=true"
  }
}
```

此命令将生成指定的架构的数据库和所需的应用程序初始化任何数据。 下图描绘了使用前面的步骤创建的表结构。

   ![标识表](identity/_static/identity-tables.png)

## <a name="migrate-the-schema"></a>迁移架构

有细微的差别的表结构和成员身份和 ASP.NET 核心标识字段。 模式已显著更改身份验证/授权与 ASP.NET 和 ASP.NET Core 应用程序。 仍用于标识的键对象具有*用户*和*角色*。 以下是有关映射表*用户*，*角色*，和*UserRoles*。

### <a name="users"></a>用户

| *Identity(AspNetUsers)* |   | *Membership(aspnet_Users/aspnet_Membership)* ||
| --- | --- | --- | --- | --- | --- |
| **字段名称** | **Type**  |   **字段名称** | **Type**  |
|`Id` | 字符串 | `aspnet_Users.UserId` | 字符串
|`UserName` | 字符串 | `aspnet_Users.UserName` | 字符串
|`Email` | 字符串 | `aspnet_Membership.Email` | 字符串
|`NormalizedUserName` | 字符串 | `aspnet_Users.LoweredUserName` | 字符串
|`NormalizedEmail` | 字符串 | `aspnet_Membership.LoweredEmail` | 字符串
|`PhoneNumber` | 字符串 | `aspnet_Users.MobileAlias` | 字符串
|`LockoutEnabled` | 位 | `aspnet_Membership.IsLockedOut` | 位

> [!NOTE]
> 并非所有字段映射类似都于从成员资格到 ASP.NET 核心标识的一对一关系。 前面的表使用默认成员资格用户架构，并将其映射到 ASP.NET 核心标识架构。 已用于成员资格的任何其他自定义字段都需要手动映射。 在此映射中，密码，没有映射因为密码条件和密码 salt 会迁移两个之间。 **建议可保留为 null 的密码并要求用户重置其密码。** 在 ASP.NET 核心标识`LockoutEnd`应设置为在将来的某个日期中，如果用户被锁定。迁移脚本所示。

### <a name="roles"></a>角色

| *Identity(AspNetRoles)* |   | *Membership(aspnet_Roles)* ||
| --- | --- | --- | --- | --- | --- |
| **字段名称** | **Type**  |   **字段名称** | **Type**  |
|`Id` | 字符串 | `RoleId` | 字符串
|`Name` | 字符串 | `RoleName` | 字符串
|`NormalizedName` | 字符串 | `LoweredRoleName` | 字符串

### <a name="user-roles"></a>用户角色

| *Identity(AspNetUserRoles)* |   | *Membership(aspnet_UsersInRoles)* ||
| --- | --- | --- | --- | --- | --- |
| **字段名称** | **Type**  |   **字段名称** | **Type**  |
|`RoleId` | 字符串 | `RoleId` | 字符串
|`UserId` | 字符串 | `UserId` | 字符串

创建用于的迁移脚本时引用前面的映射表*用户*和*角色*。 下面的示例假定数据库服务器上有两个数据库。 一个数据库包含的现有的 ASP.NET 成员资格架构和数据。 使用前面所述的步骤创建另一个数据库。 注释是以内联形式包含有关详细信息。

```sql
-- THIS SCRIPT NEEDS TO RUN FROM THE CONTEXT OF THE MEMBERSHIP DB
BEGIN TRANSACTION MigrateUsersAndRoles
use aspnetdb

-- INSERT USERS
INSERT INTO coreidentity.dbo.aspnetusers
            (id,
             username,
             normalizedusername,
             passwordhash,
             securitystamp,
             emailconfirmed,
             phonenumber,
             phonenumberconfirmed,
             twofactorenabled,
             lockoutend,
             lockoutenabled,
             accessfailedcount,
             email,
             normalizedemail)
SELECT aspnet_users.userid,
       aspnet_users.username,
       aspnet_users.loweredusername,
       --Creates an empty password since passwords don't map between the two schemas
       '',
       --Security Stamp is a token used to verify the state of an account and is subject to change at any time. It should be intialized as a new ID.
       NewID(),
       --EmailConfirmed is set when a new user is created and confirmed via email. Users must have this set during migration to ensure they're able to reset passwords.
       1,
       aspnet_users.mobilealias,
       CASE
         WHEN aspnet_Users.MobileAlias is null THEN 0
         ELSE 1
       END,
       --2-factor Auth likely wasn't setup in Membership for users, so setting as false.
       0,
       CASE
         --Setting lockout date to time in the future (1000 years)
         WHEN aspnet_membership.islockedout = 1 THEN Dateadd(year, 1000,
                                                     Sysutcdatetime())
         ELSE NULL
       END,
       aspnet_membership.islockedout,
       --AccessFailedAccount is used to track failed logins. This is stored in membership in multiple columns. Setting to 0 arbitrarily.
       0,
       aspnet_membership.email,
       aspnet_membership.loweredemail
FROM   aspnet_users
       LEFT OUTER JOIN aspnet_membership
                    ON aspnet_membership.applicationid =
                       aspnet_users.applicationid
                       AND aspnet_users.userid = aspnet_membership.userid
       LEFT OUTER JOIN coreidentity.dbo.aspnetusers
                    ON aspnet_membership.userid = aspnetusers.id
WHERE  aspnetusers.id IS NULL

-- INSERT ROLES
INSERT INTO coreIdentity.dbo.aspnetroles(id,name)
SELECT roleId,rolename
FROM aspnet_roles;

-- INSERT USER ROLES
INSERT INTO coreidentity.dbo.aspnetuserroles(userid,roleid)
SELECT userid,roleid
FROM aspnet_usersinroles;

IF @@ERROR <> 0
  BEGIN
    ROLLBACK TRANSACTION MigrateUsersAndRoles
    RETURN
  END

COMMIT TRANSACTION MigrateUsersAndRoles
```

完成后此脚本，使用成员资格用户填充前面创建的 ASP.NET 核心标识应用程序。 用户需要在中的日志记录之前更改其密码。

> [!NOTE]
> 如果成员资格系统具有与不匹配其电子邮件地址的用户名的用户，不需要向应用程序创建早期以适应此更改。 默认模板需要`UserName`和`Email`相同。 对于它们是不同的情况下，登录过程需要进行修改以使用`UserName`而不是`Email`。

在`PageModel`的登录页上，位于*Pages\Account\Login.cshtml.cs*，删除`[EmailAddress]`属性从*电子邮件*属性。 将其命名为*用户名*。 这需要更改任何地方`EmailAddress`提到，在*视图*和*PageModel*。 结果如下所示：

 ![固定的登录名](identity/_static/fixed-login.png)

## <a name="next-steps"></a>后续步骤

在本教程中，您学习了如何移植到 ASP.NET 核心 2.0 标识从 SQL 成员资格用户。 有关 ASP.NET 核心标识的详细信息，请参阅[标识简介](xref:security/authentication/identity)。
