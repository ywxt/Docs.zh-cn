---
title: ASP.NET 成员资格身份验证从迁移到 ASP.NET Core 2.0 标识
author: isaac2004
description: 了解如何迁移现有的 ASP.NET 应用程序使用成员资格到 ASP.NET Core 2.0 标识的身份验证。
ms.author: scaddie
ms.custom: mvc
ms.date: 04/24/2018
uid: migration/proper-to-2x/membership-to-core-identity
ms.openlocfilehash: 82158ec500151a0bb61fb1da55a53684367d9a4e
ms.sourcegitcommit: 2e054638b69f2b14f6d67d9fa3664999172ee1b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "41825029"
---
# <a name="migrate-from-aspnet-membership-authentication-to-aspnet-core-20-identity"></a><span data-ttu-id="2f566-103">ASP.NET 成员资格身份验证从迁移到 ASP.NET Core 2.0 标识</span><span class="sxs-lookup"><span data-stu-id="2f566-103">Migrate from ASP.NET Membership authentication to ASP.NET Core 2.0 Identity</span></span>

<span data-ttu-id="2f566-104">作者：[Isaac Levin](https://isaaclevin.com)</span><span class="sxs-lookup"><span data-stu-id="2f566-104">By [Isaac Levin](https://isaaclevin.com)</span></span>

<span data-ttu-id="2f566-105">本文演示如何迁移使用成员资格到 ASP.NET Core 2.0 标识的身份验证的 ASP.NET 应用程序的数据库架构。</span><span class="sxs-lookup"><span data-stu-id="2f566-105">This article demonstrates migrating the database schema for ASP.NET apps using Membership authentication to ASP.NET Core 2.0 Identity.</span></span>

> [!NOTE]
> <span data-ttu-id="2f566-106">本文档提供将基于 ASP.NET 成员资格的应用程序的数据库架构迁移到用于 ASP.NET Core 标识的数据库架构所需的步骤。</span><span class="sxs-lookup"><span data-stu-id="2f566-106">This document provides the steps needed to migrate the database schema for ASP.NET Membership-based apps to the database schema used for ASP.NET Core Identity.</span></span> <span data-ttu-id="2f566-107">有关从基于 ASP.NET 成员资格的身份验证迁移到 ASP.NET 标识的详细信息，请参阅[将现有应用程序从 SQL 成员身份迁移到 ASP.NET 标识](/aspnet/identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity)。</span><span class="sxs-lookup"><span data-stu-id="2f566-107">For more information about migrating from ASP.NET Membership-based authentication to ASP.NET Identity, see [Migrate an existing app from SQL Membership to ASP.NET Identity](/aspnet/identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity).</span></span> <span data-ttu-id="2f566-108">有关 ASP.NET Core 标识的详细信息，请参阅[ASP.NET Core 上的标识简介](xref:security/authentication/identity)。</span><span class="sxs-lookup"><span data-stu-id="2f566-108">For more information about ASP.NET Core Identity, see [Introduction to Identity on ASP.NET Core](xref:security/authentication/identity).</span></span>

## <a name="review-of-membership-schema"></a><span data-ttu-id="2f566-109">查看的成员身份架构</span><span class="sxs-lookup"><span data-stu-id="2f566-109">Review of Membership schema</span></span>

<span data-ttu-id="2f566-110">在 ASP.NET 2.0 之前开发人员被负责创建自己的应用的整个身份验证和授权过程。</span><span class="sxs-lookup"><span data-stu-id="2f566-110">Prior to ASP.NET 2.0, developers were tasked with creating the entire authentication and authorization process for their apps.</span></span> <span data-ttu-id="2f566-111">使用 ASP.NET 2.0 成员身份引入时，提供处理 ASP.NET 应用程序中的安全性的样本解决方案。</span><span class="sxs-lookup"><span data-stu-id="2f566-111">With ASP.NET 2.0, Membership was introduced, providing a boilerplate solution to handling security within ASP.NET apps.</span></span> <span data-ttu-id="2f566-112">开发人员现在可以启动到与 SQL Server 数据库架构[aspnet_regsql.exe](https://msdn.microsoft.com/library/ms229862.aspx)命令。</span><span class="sxs-lookup"><span data-stu-id="2f566-112">Developers were now able to bootstrap a schema into a SQL Server database with the [aspnet_regsql.exe](https://msdn.microsoft.com/library/ms229862.aspx) command.</span></span> <span data-ttu-id="2f566-113">运行此命令后，已在数据库中创建以下表。</span><span class="sxs-lookup"><span data-stu-id="2f566-113">After running this command, the following tables were created in the database.</span></span>

  ![成员资格表](identity/_static/membership-tables.png)

<span data-ttu-id="2f566-115">若要将现有应用迁移到 ASP.NET Core 2.0 标识，这些表中的数据需要迁移到使用新的标识架构的表。</span><span class="sxs-lookup"><span data-stu-id="2f566-115">To migrate existing apps to ASP.NET Core 2.0 Identity, the data in these tables needs to be migrated to the tables used by the new Identity schema.</span></span>

## <a name="aspnet-core-identity-20-schema"></a><span data-ttu-id="2f566-116">ASP.NET Core 标识 2.0 架构</span><span class="sxs-lookup"><span data-stu-id="2f566-116">ASP.NET Core Identity 2.0 schema</span></span>

<span data-ttu-id="2f566-117">ASP.NET Core 2.0 遵循[标识](/aspnet/identity/index)ASP.NET 4.5 中引入的原则。</span><span class="sxs-lookup"><span data-stu-id="2f566-117">ASP.NET Core 2.0 follows the [Identity](/aspnet/identity/index) principle introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="2f566-118">尽管共享的原则，框架之间的实现是不同的甚至 ASP.NET Core 的版本之间 (请参阅[将身份验证和标识迁移到 ASP.NET Core 2.0](xref:migration/1x-to-2x/index))。</span><span class="sxs-lookup"><span data-stu-id="2f566-118">Though the principle is shared, the implementation between the frameworks is different, even between versions of ASP.NET Core (see [Migrate authentication and Identity to ASP.NET Core 2.0](xref:migration/1x-to-2x/index)).</span></span>

<span data-ttu-id="2f566-119">ASP.NET Core 2.0 标识查看架构的最快方法是创建新的 ASP.NET Core 2.0 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2f566-119">The fastest way to view the schema for ASP.NET Core 2.0 Identity is to create a new ASP.NET Core 2.0 app.</span></span> <span data-ttu-id="2f566-120">请按照 Visual Studio 2017 中的执行以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="2f566-120">Follow these steps in Visual Studio 2017:</span></span>

* <span data-ttu-id="2f566-121">选择“文件” > “新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="2f566-121">Select **File** > **New** > **Project**.</span></span>
* <span data-ttu-id="2f566-122">创建一个新**ASP.NET Core Web 应用程序**并将项目命名*CoreIdentitySample*。</span><span class="sxs-lookup"><span data-stu-id="2f566-122">Create a new **ASP.NET Core Web Application** and name the project *CoreIdentitySample*.</span></span>
* <span data-ttu-id="2f566-123">选择**ASP.NET Core 2.0**在下拉列表中，然后选择**Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="2f566-123">Select **ASP.NET Core 2.0** in the dropdown and then select **Web Application**.</span></span> <span data-ttu-id="2f566-124">此模板会生成[Razor 页面](xref:razor-pages/index)应用。</span><span class="sxs-lookup"><span data-stu-id="2f566-124">This template produces a [Razor Pages](xref:razor-pages/index) app.</span></span> <span data-ttu-id="2f566-125">然后再单击**确定**，单击**更改身份验证**。</span><span class="sxs-lookup"><span data-stu-id="2f566-125">Before clicking **OK**, click **Change Authentication**.</span></span>
* <span data-ttu-id="2f566-126">选择**单个用户帐户**标识模板。</span><span class="sxs-lookup"><span data-stu-id="2f566-126">Choose **Individual User Accounts** for the Identity templates.</span></span> <span data-ttu-id="2f566-127">最后，单击**确定**，然后**确定**。</span><span class="sxs-lookup"><span data-stu-id="2f566-127">Finally, click **OK**, then **OK**.</span></span> <span data-ttu-id="2f566-128">Visual Studio 创建项目时使用 ASP.NET Core 标识模板。</span><span class="sxs-lookup"><span data-stu-id="2f566-128">Visual Studio creates a project using the ASP.NET Core Identity template.</span></span>

<span data-ttu-id="2f566-129">ASP.NET Core 2.0 标识使用[实体框架核心](/ef/core)与存储的身份验证数据的数据库进行交互。</span><span class="sxs-lookup"><span data-stu-id="2f566-129">ASP.NET Core 2.0 Identity uses [Entity Framework Core](/ef/core) to interact with the database storing the authentication data.</span></span> <span data-ttu-id="2f566-130">为了使新创建的应用程序能够，那里需要使用数据库来存储此数据。</span><span class="sxs-lookup"><span data-stu-id="2f566-130">In order for the newly created app to work, there needs to be a database to store this data.</span></span> <span data-ttu-id="2f566-131">创建新的应用程序之后, 检查的数据库环境中的架构的最快方法是创建使用 Entity Framework 迁移的数据库。</span><span class="sxs-lookup"><span data-stu-id="2f566-131">After creating a new app, the fastest way to inspect the schema in a database environment is to create the database using Entity Framework migrations.</span></span> <span data-ttu-id="2f566-132">此过程创建数据库、 在本地或其他位置，模拟该架构。</span><span class="sxs-lookup"><span data-stu-id="2f566-132">This process creates a database, either locally or elsewhere, which mimics that schema.</span></span> <span data-ttu-id="2f566-133">查看上述文档，有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="2f566-133">Review the preceding documentation for more information.</span></span>

<span data-ttu-id="2f566-134">若要使用 ASP.NET Core 标识架构中创建数据库，运行`Update-Database`命令在 Visual Studio 的**程序包管理器控制台**(PMC) 窗口&mdash;位于**工具** > **NuGet 包管理器** > **程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="2f566-134">To create a database with the ASP.NET Core Identity schema, run the `Update-Database` command in Visual Studio's **Package Manager Console** (PMC) window&mdash;it's located at **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="2f566-135">PMC 支持正在运行的 Entity Framework 命令。</span><span class="sxs-lookup"><span data-stu-id="2f566-135">PMC supports running Entity Framework commands.</span></span>

<span data-ttu-id="2f566-136">Entity Framework 命令中指定的数据库使用连接字符串*appsettings.json*。</span><span class="sxs-lookup"><span data-stu-id="2f566-136">Entity Framework commands use the connection string for the database specified in *appsettings.json*.</span></span> <span data-ttu-id="2f566-137">下面的连接字符串上的目标数据库*localhost*名为*asp net core 标识*。</span><span class="sxs-lookup"><span data-stu-id="2f566-137">The following connection string targets a database on *localhost* named *asp-net-core-identity*.</span></span> <span data-ttu-id="2f566-138">在此设置中，实体框架配置为使用`DefaultConnection`连接字符串。</span><span class="sxs-lookup"><span data-stu-id="2f566-138">In this setting, Entity Framework is configured to use the `DefaultConnection` connection string.</span></span>

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=aspnet-core-identity;Trusted_Connection=True;MultipleActiveResultSets=true"
  }
}
```

<span data-ttu-id="2f566-139">此命令可生成与架构指定的数据库和任何所需的应用程序初始化的数据。</span><span class="sxs-lookup"><span data-stu-id="2f566-139">This command builds the database specified with the schema and any data needed for app initialization.</span></span> <span data-ttu-id="2f566-140">下图描绘了使用上述步骤创建的表结构。</span><span class="sxs-lookup"><span data-stu-id="2f566-140">The following image depicts the table structure that's created with the preceding steps.</span></span>

   ![标识表](identity/_static/identity-tables.png)

## <a name="migrate-the-schema"></a><span data-ttu-id="2f566-142">迁移架构</span><span class="sxs-lookup"><span data-stu-id="2f566-142">Migrate the schema</span></span>

<span data-ttu-id="2f566-143">有细微的差别的表结构和成员身份和 ASP.NET Core 标识字段。</span><span class="sxs-lookup"><span data-stu-id="2f566-143">There are subtle differences in the table structures and fields for both Membership and ASP.NET Core Identity.</span></span> <span data-ttu-id="2f566-144">模式已显著更改身份验证/授权与 ASP.NET 和 ASP.NET Core 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2f566-144">The pattern has changed substantially for authentication/authorization with ASP.NET and ASP.NET Core apps.</span></span> <span data-ttu-id="2f566-145">仍用于标识的关键对象是*用户*并*角色*。</span><span class="sxs-lookup"><span data-stu-id="2f566-145">The key objects that are still used with Identity are *Users* and *Roles*.</span></span> <span data-ttu-id="2f566-146">以下是有关映射表*用户*，*角色*，并*UserRoles*。</span><span class="sxs-lookup"><span data-stu-id="2f566-146">Here are mapping tables for *Users*, *Roles*, and *UserRoles*.</span></span>

### <a name="users"></a><span data-ttu-id="2f566-147">用户</span><span class="sxs-lookup"><span data-stu-id="2f566-147">Users</span></span>

| <span data-ttu-id="2f566-148">*Identity(AspNetUsers)*</span><span class="sxs-lookup"><span data-stu-id="2f566-148">*Identity(AspNetUsers)*</span></span> |   | <span data-ttu-id="2f566-149">*Membership(aspnet_Users/aspnet_Membership)*</span><span class="sxs-lookup"><span data-stu-id="2f566-149">*Membership(aspnet_Users/aspnet_Membership)*</span></span> ||
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="2f566-150">**字段名称**</span><span class="sxs-lookup"><span data-stu-id="2f566-150">**Field Name**</span></span> | <span data-ttu-id="2f566-151">**Type**</span><span class="sxs-lookup"><span data-stu-id="2f566-151">**Type**</span></span>  |   <span data-ttu-id="2f566-152">**字段名称**</span><span class="sxs-lookup"><span data-stu-id="2f566-152">**Field Name**</span></span> | <span data-ttu-id="2f566-153">**Type**</span><span class="sxs-lookup"><span data-stu-id="2f566-153">**Type**</span></span>  |
|`Id` | <span data-ttu-id="2f566-154">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-154">string</span></span> | `aspnet_Users.UserId` | <span data-ttu-id="2f566-155">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-155">string</span></span>
|`UserName` | <span data-ttu-id="2f566-156">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-156">string</span></span> | `aspnet_Users.UserName` | <span data-ttu-id="2f566-157">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-157">string</span></span>
|`Email` | <span data-ttu-id="2f566-158">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-158">string</span></span> | `aspnet_Membership.Email` | <span data-ttu-id="2f566-159">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-159">string</span></span>
|`NormalizedUserName` | <span data-ttu-id="2f566-160">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-160">string</span></span> | `aspnet_Users.LoweredUserName` | <span data-ttu-id="2f566-161">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-161">string</span></span>
|`NormalizedEmail` | <span data-ttu-id="2f566-162">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-162">string</span></span> | `aspnet_Membership.LoweredEmail` | <span data-ttu-id="2f566-163">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-163">string</span></span>
|`PhoneNumber` | <span data-ttu-id="2f566-164">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-164">string</span></span> | `aspnet_Users.MobileAlias` | <span data-ttu-id="2f566-165">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-165">string</span></span>
|`LockoutEnabled` | <span data-ttu-id="2f566-166">位</span><span class="sxs-lookup"><span data-stu-id="2f566-166">bit</span></span> | `aspnet_Membership.IsLockedOut` | <span data-ttu-id="2f566-167">位</span><span class="sxs-lookup"><span data-stu-id="2f566-167">bit</span></span>

> [!NOTE]
> <span data-ttu-id="2f566-168">并非所有字段映射类似都于从成员资格到 ASP.NET Core 标识的一对一关系。</span><span class="sxs-lookup"><span data-stu-id="2f566-168">Not all the field mappings resemble one-to-one relationships from Membership to ASP.NET Core Identity.</span></span> <span data-ttu-id="2f566-169">前面的表使用默认成员资格用户架构，并将其映射到 ASP.NET Core 标识架构。</span><span class="sxs-lookup"><span data-stu-id="2f566-169">The preceding table takes the default Membership User schema and maps it to the ASP.NET Core Identity schema.</span></span> <span data-ttu-id="2f566-170">用于成员资格的任何其他自定义字段需要手动映射。</span><span class="sxs-lookup"><span data-stu-id="2f566-170">Any other custom fields that were used for Membership need to be mapped manually.</span></span> <span data-ttu-id="2f566-171">在此映射中，则没有密码的映射因为两者之间不迁移密码条件和密码 salt。</span><span class="sxs-lookup"><span data-stu-id="2f566-171">In this mapping, there's no map for passwords, as both password criteria and password salts don't migrate between the two.</span></span> <span data-ttu-id="2f566-172">**建议可保留为 null 的密码，并要求用户重置其密码。**</span><span class="sxs-lookup"><span data-stu-id="2f566-172">**It's recommended to leave the password as null and to ask users to reset their passwords.**</span></span> <span data-ttu-id="2f566-173">在 ASP.NET Core 标识`LockoutEnd`应设置为在将来的某个日期中，如果用户被锁定。迁移脚本所示。</span><span class="sxs-lookup"><span data-stu-id="2f566-173">In ASP.NET Core Identity, `LockoutEnd` should be set to some date in the future if the user is locked out. This is shown in the migration script.</span></span>

### <a name="roles"></a><span data-ttu-id="2f566-174">角色</span><span class="sxs-lookup"><span data-stu-id="2f566-174">Roles</span></span>

| <span data-ttu-id="2f566-175">*Identity(AspNetRoles)*</span><span class="sxs-lookup"><span data-stu-id="2f566-175">*Identity(AspNetRoles)*</span></span> |   | <span data-ttu-id="2f566-176">*Membership(aspnet_Roles)*</span><span class="sxs-lookup"><span data-stu-id="2f566-176">*Membership(aspnet_Roles)*</span></span> ||
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="2f566-177">**字段名称**</span><span class="sxs-lookup"><span data-stu-id="2f566-177">**Field Name**</span></span> | <span data-ttu-id="2f566-178">**Type**</span><span class="sxs-lookup"><span data-stu-id="2f566-178">**Type**</span></span>  |   <span data-ttu-id="2f566-179">**字段名称**</span><span class="sxs-lookup"><span data-stu-id="2f566-179">**Field Name**</span></span> | <span data-ttu-id="2f566-180">**Type**</span><span class="sxs-lookup"><span data-stu-id="2f566-180">**Type**</span></span>  |
|`Id` | <span data-ttu-id="2f566-181">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-181">string</span></span> | `RoleId` | <span data-ttu-id="2f566-182">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-182">string</span></span>
|`Name` | <span data-ttu-id="2f566-183">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-183">string</span></span> | `RoleName` | <span data-ttu-id="2f566-184">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-184">string</span></span>
|`NormalizedName` | <span data-ttu-id="2f566-185">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-185">string</span></span> | `LoweredRoleName` | <span data-ttu-id="2f566-186">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-186">string</span></span>

### <a name="user-roles"></a><span data-ttu-id="2f566-187">用户角色</span><span class="sxs-lookup"><span data-stu-id="2f566-187">User Roles</span></span>

| <span data-ttu-id="2f566-188">*Identity(AspNetUserRoles)*</span><span class="sxs-lookup"><span data-stu-id="2f566-188">*Identity(AspNetUserRoles)*</span></span> |   | <span data-ttu-id="2f566-189">*Membership(aspnet_UsersInRoles)*</span><span class="sxs-lookup"><span data-stu-id="2f566-189">*Membership(aspnet_UsersInRoles)*</span></span> ||
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="2f566-190">**字段名称**</span><span class="sxs-lookup"><span data-stu-id="2f566-190">**Field Name**</span></span> | <span data-ttu-id="2f566-191">**Type**</span><span class="sxs-lookup"><span data-stu-id="2f566-191">**Type**</span></span>  |   <span data-ttu-id="2f566-192">**字段名称**</span><span class="sxs-lookup"><span data-stu-id="2f566-192">**Field Name**</span></span> | <span data-ttu-id="2f566-193">**Type**</span><span class="sxs-lookup"><span data-stu-id="2f566-193">**Type**</span></span>  |
|`RoleId` | <span data-ttu-id="2f566-194">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-194">string</span></span> | `RoleId` | <span data-ttu-id="2f566-195">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-195">string</span></span>
|`UserId` | <span data-ttu-id="2f566-196">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-196">string</span></span> | `UserId` | <span data-ttu-id="2f566-197">字符串</span><span class="sxs-lookup"><span data-stu-id="2f566-197">string</span></span>

<span data-ttu-id="2f566-198">创建的迁移脚本时，引用前面的映射表*用户*并*角色*。</span><span class="sxs-lookup"><span data-stu-id="2f566-198">Reference the preceding mapping tables when creating a migration script for *Users* and *Roles*.</span></span> <span data-ttu-id="2f566-199">下面的示例假定数据库服务器上有两个数据库。</span><span class="sxs-lookup"><span data-stu-id="2f566-199">The following example assumes you have two databases on a database server.</span></span> <span data-ttu-id="2f566-200">一个数据库包含的现有 ASP.NET 成员身份架构和数据。</span><span class="sxs-lookup"><span data-stu-id="2f566-200">One database contains the existing ASP.NET Membership schema and data.</span></span> <span data-ttu-id="2f566-201">使用前面所述的步骤创建另一个数据库。</span><span class="sxs-lookup"><span data-stu-id="2f566-201">The other database was created using steps described earlier.</span></span> <span data-ttu-id="2f566-202">注释是以内联形式包含有关更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="2f566-202">Comments are included inline for more details.</span></span>

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
       --Security Stamp is a token used to verify the state of an account and is subject to change at any time. It should be initialized as a new ID.
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

<span data-ttu-id="2f566-203">完成后此脚本，使用成员资格用户填充前面创建的 ASP.NET Core 标识应用程序。</span><span class="sxs-lookup"><span data-stu-id="2f566-203">After completion of this script, the ASP.NET Core Identity app created earlier is populated with Membership users.</span></span> <span data-ttu-id="2f566-204">用户需要在登录之前更改其密码。</span><span class="sxs-lookup"><span data-stu-id="2f566-204">Users need to change their passwords before logging in.</span></span>

> [!NOTE]
> <span data-ttu-id="2f566-205">如果成员资格系统必须具有不匹配其电子邮件地址的用户名的用户，不需要对创建早期为解决此问题的应用更改。</span><span class="sxs-lookup"><span data-stu-id="2f566-205">If the Membership system had users with user names that didn't match their email address, changes are required to the app created earlier to accommodate this.</span></span> <span data-ttu-id="2f566-206">默认模板需要`UserName`和`Email`相同。</span><span class="sxs-lookup"><span data-stu-id="2f566-206">The default template expects `UserName` and `Email` to be the same.</span></span> <span data-ttu-id="2f566-207">它们是不同的情况下，登录过程需要进行修改以使用`UserName`而不是`Email`。</span><span class="sxs-lookup"><span data-stu-id="2f566-207">For situations in which they're different, the login process needs to be modified to use `UserName` instead of `Email`.</span></span>

<span data-ttu-id="2f566-208">在中`PageModel`的登录页上，位于*Pages\Account\Login.cshtml.cs*，删除`[EmailAddress]`属性从*电子邮件*属性。</span><span class="sxs-lookup"><span data-stu-id="2f566-208">In the `PageModel` of the Login Page, located at *Pages\Account\Login.cshtml.cs*, remove the `[EmailAddress]` attribute from the *Email* property.</span></span> <span data-ttu-id="2f566-209">其重命名为*用户名*。</span><span class="sxs-lookup"><span data-stu-id="2f566-209">Rename it to *UserName*.</span></span> <span data-ttu-id="2f566-210">这需要更改无论在何处`EmailAddress`所述，在*视图*并*PageModel*。</span><span class="sxs-lookup"><span data-stu-id="2f566-210">This requires a change wherever `EmailAddress` is mentioned, in the *View* and *PageModel*.</span></span> <span data-ttu-id="2f566-211">结果看起来如下所示：</span><span class="sxs-lookup"><span data-stu-id="2f566-211">The result looks like the following:</span></span>

 ![固定的登录名](identity/_static/fixed-login.png)

## <a name="next-steps"></a><span data-ttu-id="2f566-213">后续步骤</span><span class="sxs-lookup"><span data-stu-id="2f566-213">Next steps</span></span>

<span data-ttu-id="2f566-214">在本教程中，您学习了如何移植到 ASP.NET Core 2.0 标识从 SQL 成员资格用户。</span><span class="sxs-lookup"><span data-stu-id="2f566-214">In this tutorial, you learned how to port users from SQL membership to ASP.NET Core 2.0 Identity.</span></span> <span data-ttu-id="2f566-215">有关 ASP.NET Core 标识的详细信息，请参阅[标识简介](xref:security/authentication/identity)。</span><span class="sxs-lookup"><span data-stu-id="2f566-215">For more information regarding ASP.NET Core Identity, see [Introduction to Identity](xref:security/authentication/identity).</span></span>
