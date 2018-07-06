---
title: 标识模型自定义项
author: ajcvickers
description: 本文介绍如何为 ASP.NET Core 标识自定义的基础的实体框架核心数据模型。
monikerRange: '>= aspnetcore-2.1'
ms.author: avickers
ms.date: 04/12/2018
uid: security/authentication/customize_identity_model
ms.openlocfilehash: 41ea125414c5997ee36f4e312beba4ff318a4a8d
ms.sourcegitcommit: 931b6a2d7eb28a0f1295e8a95690b8c4c5f58477
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37077670"
---
# <a name="identity-model-customization"></a><span data-ttu-id="73f42-103">标识模型自定义项</span><span class="sxs-lookup"><span data-stu-id="73f42-103">Identity model customization</span></span>

<span data-ttu-id="73f42-104">通过[Arthur Vickers](https://github.com/ajcvickers)</span><span class="sxs-lookup"><span data-stu-id="73f42-104">By [Arthur Vickers](https://github.com/ajcvickers)</span></span>

<span data-ttu-id="73f42-105">ASP.NET Core 标识提供一个框架，用于管理和 ASP.NET Core 应用程序中存储用户帐户。</span><span class="sxs-lookup"><span data-stu-id="73f42-105">ASP.NET Core Identity provides a framework for managing and storing user accounts in ASP.NET Core applications.</span></span> <span data-ttu-id="73f42-106">标识添加到项目中，选中"单个用户帐户"时作为身份验证机制。</span><span class="sxs-lookup"><span data-stu-id="73f42-106">Identity is added to your project when "Individual User Accounts" is selected as the authentication mechanism.</span></span> <span data-ttu-id="73f42-107">默认情况下，标识将使用的 Entity Framework (EF) 核心数据模型。</span><span class="sxs-lookup"><span data-stu-id="73f42-107">By default, Identity makes use of an Entity Framework (EF) Core data model.</span></span> <span data-ttu-id="73f42-108">本文介绍如何自定义标识模型。</span><span class="sxs-lookup"><span data-stu-id="73f42-108">This article describes how to customize the Identity model.</span></span>

<a name="identity-migrations"></a>

## <a name="identity-and-ef-core-migrations"></a><span data-ttu-id="73f42-109">标识和 EF Core 迁移</span><span class="sxs-lookup"><span data-stu-id="73f42-109">Identity and EF Core Migrations</span></span>

<span data-ttu-id="73f42-110">之前检查模型，它是有助于了解如何标识配合[EF Core 迁移](/ef/core/managing-schemas/migrations/)创建和更新数据库。</span><span class="sxs-lookup"><span data-stu-id="73f42-110">Before examining the model, it's useful to understand how Identity works with [EF Core Migrations](/ef/core/managing-schemas/migrations/) to create and update a database.</span></span> <span data-ttu-id="73f42-111">最高层的过程是：</span><span class="sxs-lookup"><span data-stu-id="73f42-111">At the top level, the process is:</span></span>

1. <span data-ttu-id="73f42-112">定义或更新[代码中的数据模型](/ef/core/modeling/)。</span><span class="sxs-lookup"><span data-stu-id="73f42-112">Define or update a [data model in code](/ef/core/modeling/).</span></span>
1. <span data-ttu-id="73f42-113">添加迁移，以将此模型转换可以应用于数据库的更改。</span><span class="sxs-lookup"><span data-stu-id="73f42-113">Add a migration to translate this model into changes that can be applied to the database.</span></span>
1. <span data-ttu-id="73f42-114">检查迁移能正确地表示您的意图。</span><span class="sxs-lookup"><span data-stu-id="73f42-114">Check that the migration correctly represents your intentions.</span></span>
1. <span data-ttu-id="73f42-115">将应用迁移更新数据库要与模型同步。</span><span class="sxs-lookup"><span data-stu-id="73f42-115">Apply the migration to update the database to be in sync with the model.</span></span>
1. <span data-ttu-id="73f42-116">重复步骤 1-4 以进一步优化模型并使数据库保持同步。</span><span class="sxs-lookup"><span data-stu-id="73f42-116">Repeat steps 1-4 to further refine the model and keep the database in sync.</span></span>

<span data-ttu-id="73f42-117">迁移添加和使用应用：</span><span class="sxs-lookup"><span data-stu-id="73f42-117">Migrations are added and applied using:</span></span>

* <span data-ttu-id="73f42-118">[程序包管理器控制台](/ef/core/miscellaneous/cli/powershell)(PMC) 如果你使用的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="73f42-118">The [Package Manager Console](/ef/core/miscellaneous/cli/powershell) (PMC) if you are using Visual Studio.</span></span>
* <span data-ttu-id="73f42-119">[Dotnet 命令](/ef/core/miscellaneous/cli/dotnet)命令行上。</span><span class="sxs-lookup"><span data-stu-id="73f42-119">The [dotnet commands](/ef/core/miscellaneous/cli/dotnet) on the command line.</span></span>
* <span data-ttu-id="73f42-120">运行应用程序时，请选择错误页上的迁移链接。</span><span class="sxs-lookup"><span data-stu-id="73f42-120">Selecting the migrations link on the error page when the application is run.</span></span>

<span data-ttu-id="73f42-121">ASP.NET Core 有可用于应用程序运行时应用迁移一个开发时间错误页处理程序。</span><span class="sxs-lookup"><span data-stu-id="73f42-121">ASP.NET Core has a development-time error page handler that can be used to apply migrations when the application is run.</span></span> <span data-ttu-id="73f42-122">对于生产应用程序，它通常会更适合从迁移中生成 SQL 脚本，将部署到数据库作为受控的应用程序和数据库部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="73f42-122">For production applications, it is often more appropriate to generate SQL scripts from the migrations and deploy these to the database as part of a controlled application and database deployment.</span></span>

<span data-ttu-id="73f42-123">创建新的应用程序使用标识时，已经完成上述步骤 1 和 2。</span><span class="sxs-lookup"><span data-stu-id="73f42-123">When a new application using Identity is created, steps 1 and 2 above have already been completed.</span></span> <span data-ttu-id="73f42-124">也就是说，初始数据模型已存在，并已添加到项目中的初始迁移。</span><span class="sxs-lookup"><span data-stu-id="73f42-124">That is, the initial data model already exists, and the initial migration has been added to the project.</span></span> <span data-ttu-id="73f42-125">仍然需要应用于数据库初始迁移。</span><span class="sxs-lookup"><span data-stu-id="73f42-125">The initial migration still needs to be applied to the database.</span></span> <span data-ttu-id="73f42-126">通过运行更新数据库 (PMC)，dotnet ef 数据库更新 (.NET Core CLI) 命令，或通过在运行应用程序使用错误页，则可以完成的初始迁移。</span><span class="sxs-lookup"><span data-stu-id="73f42-126">The initial migration can be done by running the Update-Database (PMC), the dotnet ef database update (.NET Core CLI) command, or by using the error page when the application is run.</span></span>

<span data-ttu-id="73f42-127">需要对模型进行更改时重复前面的步骤。</span><span class="sxs-lookup"><span data-stu-id="73f42-127">The preceding steps need to be repeated as changes are made to the model.</span></span>

<a name="identity-model"></a>

## <a name="the-identity-model"></a><span data-ttu-id="73f42-128">标识模型</span><span class="sxs-lookup"><span data-stu-id="73f42-128">The Identity model</span></span>

### <a name="entity-types"></a><span data-ttu-id="73f42-129">实体类型</span><span class="sxs-lookup"><span data-stu-id="73f42-129">Entity types</span></span>

<span data-ttu-id="73f42-130">标识模型包含七个实体类型：</span><span class="sxs-lookup"><span data-stu-id="73f42-130">The Identity model consists of seven entity types:</span></span>

* <span data-ttu-id="73f42-131">`User` -表示的用户</span><span class="sxs-lookup"><span data-stu-id="73f42-131">`User` - represents the user</span></span>
* <span data-ttu-id="73f42-132">`Role` -表示的角色</span><span class="sxs-lookup"><span data-stu-id="73f42-132">`Role` - represents a role</span></span>
* <span data-ttu-id="73f42-133">`UserClaim` -表示用户拥有的声明</span><span class="sxs-lookup"><span data-stu-id="73f42-133">`UserClaim` - represents a claim that a user possess</span></span>
* <span data-ttu-id="73f42-134">`UserToken` -表示用户的身份验证令牌</span><span class="sxs-lookup"><span data-stu-id="73f42-134">`UserToken` - represents an authentication token for a user</span></span>
* <span data-ttu-id="73f42-135">`UserLogin` -将用户与一个登录名相关联</span><span class="sxs-lookup"><span data-stu-id="73f42-135">`UserLogin` - associates a user with a login</span></span>
* <span data-ttu-id="73f42-136">`RoleClaim` -表示将授予角色中的所有用户的声明</span><span class="sxs-lookup"><span data-stu-id="73f42-136">`RoleClaim` - represents a claim that is granted to all users within a role</span></span>
* <span data-ttu-id="73f42-137">`UserRole` -加入将用户和角色相关联的实体</span><span class="sxs-lookup"><span data-stu-id="73f42-137">`UserRole` - join entity that associates users and roles</span></span>

### <a name="entity-type-relationships"></a><span data-ttu-id="73f42-138">实体类型关系</span><span class="sxs-lookup"><span data-stu-id="73f42-138">Entity type relationships</span></span>

<span data-ttu-id="73f42-139">这些实体类型通过以下方式彼此相关：</span><span class="sxs-lookup"><span data-stu-id="73f42-139">These entity types are related to each other in the following ways:</span></span>

* <span data-ttu-id="73f42-140">每个`User`可以具有许多 `UserClaims`</span><span class="sxs-lookup"><span data-stu-id="73f42-140">Each `User` can have many `UserClaims`</span></span>
* <span data-ttu-id="73f42-141">每个`User`可以具有许多 `UserLogins`</span><span class="sxs-lookup"><span data-stu-id="73f42-141">Each `User` can have many `UserLogins`</span></span>
* <span data-ttu-id="73f42-142">每个`User`可以具有许多 `UserTokens`</span><span class="sxs-lookup"><span data-stu-id="73f42-142">Each `User` can have many `UserTokens`</span></span>
* <span data-ttu-id="73f42-143">每个`Role`可以具有许多关联 `RoleClaims`</span><span class="sxs-lookup"><span data-stu-id="73f42-143">Each `Role` can have many associated `RoleClaims`</span></span>
* <span data-ttu-id="73f42-144">每个`User`可以具有许多关联`Roles`，和每个`Role`可以与多个用户相关联</span><span class="sxs-lookup"><span data-stu-id="73f42-144">Each `User` can have many associated `Roles`, and each `Role` can be associated with many Users</span></span>
  * <span data-ttu-id="73f42-145">这是一个多对多关系，这需要在数据库中的联接表。</span><span class="sxs-lookup"><span data-stu-id="73f42-145">This is a many-to-many relationship, which requires a join table in the database.</span></span> <span data-ttu-id="73f42-146">联接表均由表示`UserRole`实体。</span><span class="sxs-lookup"><span data-stu-id="73f42-146">The join table is represented by the `UserRole` entity.</span></span>

### <a name="default-model-configuration"></a><span data-ttu-id="73f42-147">默认模型配置</span><span class="sxs-lookup"><span data-stu-id="73f42-147">Default model configuration</span></span>

<span data-ttu-id="73f42-148">标识定义的"上下文类"的继承了各种[DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext)配置和使用模型。</span><span class="sxs-lookup"><span data-stu-id="73f42-148">Identity defines a variety of "context classes" which inherit from [DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext) to configure and use the model.</span></span> <span data-ttu-id="73f42-149">进行此配置使用[EF Core 代码 First Fluent API](/ef/core/modeling/)中[OnModelCreating](/dotnet/api/microsoft.entityframeworkcore.dbcontext.onmodelcreating#Microsoft_EntityFrameworkCore_DbContext_OnModelCreating_Microsoft_EntityFrameworkCore_ModelBuilder_)上下文类的方法。</span><span class="sxs-lookup"><span data-stu-id="73f42-149">This configuration is done using the [EF Core Code First Fluent API](/ef/core/modeling/) in the [OnModelCreating](/dotnet/api/microsoft.entityframeworkcore.dbcontext.onmodelcreating#Microsoft_EntityFrameworkCore_DbContext_OnModelCreating_Microsoft_EntityFrameworkCore_ModelBuilder_) method of the context class.</span></span> <span data-ttu-id="73f42-150">默认配置是：</span><span class="sxs-lookup"><span data-stu-id="73f42-150">The default configuration is:</span></span>

```CSharp
builder.Entity<TUser>(b =>
{
    // Primary key
    b.HasKey(u => u.Id);

    // Indexes for "normalized" username and email, to allow efficient lookups
    b.HasIndex(u => u.NormalizedUserName).HasName("UserNameIndex").IsUnique();
    b.HasIndex(u => u.NormalizedEmail).HasName("EmailIndex");

    // Maps to the AspNetUsers table
    b.ToTable("AspNetUsers");

    // A concurrency token for use with the optimistic concurrency checking
    b.Property(u => u.ConcurrencyStamp).IsConcurrencyToken();

    // Limit the size of columns to use efficient database types
    b.Property(u => u.UserName).HasMaxLength(256);
    b.Property(u => u.NormalizedUserName).HasMaxLength(256);
    b.Property(u => u.Email).HasMaxLength(256);
    b.Property(u => u.NormalizedEmail).HasMaxLength(256);

    // The relationships between User and other entity types
    // Note that these relationships are configured with no navigation properties

    // Each User can have many UserClaims
    b.HasMany<TUserClaim>().WithOne().HasForeignKey(uc => uc.UserId).IsRequired();

    // Each User can have many UserLogins
    b.HasMany<TUserLogin>().WithOne().HasForeignKey(ul => ul.UserId).IsRequired();

    // Each User can have many UserTokens
    b.HasMany<TUserToken>().WithOne().HasForeignKey(ut => ut.UserId).IsRequired();

    // Each User can have many entries in the UserRole join table
    b.HasMany<TUserRole>().WithOne().HasForeignKey(ur => ur.UserId).IsRequired();
});

builder.Entity<TUserClaim>(b =>
{
    // Primary key
    b.HasKey(uc => uc.Id);

    // Maps to the AspNetUserClaims table
    b.ToTable("AspNetUserClaims");
});

builder.Entity<TUserLogin>(b =>
{
    // Composite primary key consisting of the LoginProvider and the key to use
    // with that provider
    b.HasKey(l => new { l.LoginProvider, l.ProviderKey });

    // Limit the size of the composite key columns due to common database restrictions
    b.Property(l => l.LoginProvider).HasMaxLength(128);
    b.Property(l => l.ProviderKey).HasMaxLength(128);

    // Maps to the AspNetUserLogins table
    b.ToTable("AspNetUserLogins");
});

builder.Entity<TUserToken>(b =>
{
    // Composite primary key consisting of the UserId, LoginProvider and Name
    b.HasKey(t => new { t.UserId, t.LoginProvider, t.Name });

    // Limit the size of the composite key columns due to common database restrictions
    b.Property(t => t.LoginProvider).HasMaxLength(maxKeyLength);
    b.Property(t => t.Name).HasMaxLength(maxKeyLength);

    // Maps to the AspNetUserTokens table
    b.ToTable("AspNetUserTokens");
});

builder.Entity<TRole>(b =>
{
    // Primary key
    b.HasKey(r => r.Id);

    // Index for "normalized" role name to allow efficient lookups
    b.HasIndex(r => r.NormalizedName).HasName("RoleNameIndex").IsUnique();

    // Maps to the AspNetRoles table
    b.ToTable("AspNetRoles");

    // A concurrency token for use with the optimistic concurrency checking
    b.Property(r => r.ConcurrencyStamp).IsConcurrencyToken();

    // Limit the size of columns to use efficient database types
    b.Property(u => u.Name).HasMaxLength(256);
    b.Property(u => u.NormalizedName).HasMaxLength(256);

    // The relationships between Role and other entity types
    // Note that these relationships are configured with no navigation properties

    // Each Role can have many entries in the UserRole join table
    b.HasMany<TUserRole>().WithOne().HasForeignKey(ur => ur.RoleId).IsRequired();

    // Each Role can have many associated RoleClaims
    b.HasMany<TRoleClaim>().WithOne().HasForeignKey(rc => rc.RoleId).IsRequired();
});

builder.Entity<TRoleClaim>(b =>
{
    // Primary key
    b.HasKey(rc => rc.Id);

    // Maps to the AspNetRoleClaims table
    b.ToTable("AspNetRoleClaims");
});

builder.Entity<TUserRole>(b =>
{
    // Primary key
    b.HasKey(r => new { r.UserId, r.RoleId });

    // Maps to the AspNetUserRoles table
    b.ToTable("AspNetUserRoles");
});
```

### <a name="model-generic-types"></a><span data-ttu-id="73f42-151">模型的泛型类型</span><span class="sxs-lookup"><span data-stu-id="73f42-151">Model generic types</span></span>

<span data-ttu-id="73f42-152">标识定义为每个上面列出的实体类型的默认 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="73f42-152">Identity defines default CLR types for each of the entity types listed above.</span></span> <span data-ttu-id="73f42-153">这些类型全都带有前缀"标识": `IdentityUser`， `IdentityRole`， `IdentityUserClaim`， `IdentityUserToken`， `IdentityUserLogin`， `IdentityRoleClaim`，和`IdentityUserRole`。</span><span class="sxs-lookup"><span data-stu-id="73f42-153">These types are all prefixed with "Identity": `IdentityUser`, `IdentityRole`, `IdentityUserClaim`, `IdentityUserToken`, `IdentityUserLogin`, `IdentityRoleClaim`, and `IdentityUserRole`.</span></span>

<span data-ttu-id="73f42-154">而不是直接使用这些类型，类型可以用作基类，这些类为应用程序自身的类型。</span><span class="sxs-lookup"><span data-stu-id="73f42-154">Rather than using these types directly, the types can be used as base classes for the application's own types.</span></span> <span data-ttu-id="73f42-155">`DbContext`定义标识的类是泛型的这样的： 不同的 CLR 类型可以用于一个或多个模型中的实体类型。</span><span class="sxs-lookup"><span data-stu-id="73f42-155">The `DbContext` classes defined by Identity are generic such that different CLR types can be used for one or more of the entity types in the model.</span></span> <span data-ttu-id="73f42-156">以下泛型类型还允许用户主键的类型更改。</span><span class="sxs-lookup"><span data-stu-id="73f42-156">These generic types also allow for the type of the User primary key to be changed.</span></span>

<span data-ttu-id="73f42-157">对于角色，支持使用标识时[IdentityDbContext](/dotnet/api/microsoft.aspnetcore.identity.entityframeworkcore.identitydbcontext)应使用类：</span><span class="sxs-lookup"><span data-stu-id="73f42-157">When using Identity with support for roles, an [IdentityDbContext](/dotnet/api/microsoft.aspnetcore.identity.entityframeworkcore.identitydbcontext) class should be used:</span></span>

```CSharp
// Uses all the built-in Identity types
// Uses `string` as the key type
public class IdentityDbContext
    : IdentityDbContext<IdentityUser, IdentityRole, string>
{
}

// Uses the built-in Identity types except with a custom User type
// Uses `string` as the key type
public class IdentityDbContext<TUser>
    : IdentityDbContext<TUser, IdentityRole, string>
        where TUser : IdentityUser
{
}

// Uses the built-in Identity types except with custom User and Role types
// The key type is defined by TKey
public class IdentityDbContext<TUser, TRole, TKey>
    : IdentityDbContext<TUser, TRole, TKey, IdentityUserClaim<TKey>, IdentityUserRole<TKey>, IdentityUserLogin<TKey>, IdentityRoleClaim<TKey>, IdentityUserToken<TKey>>
        where TUser : IdentityUser<TKey>
        where TRole : IdentityRole<TKey>
        where TKey : IEquatable<TKey>
{
}

// No built-in Identity types are used; all are specified by generic arguments
// The key type is defined by TKey
public abstract class IdentityDbContext<TUser, TRole, TKey, TUserClaim, TUserRole, TUserLogin, TRoleClaim, TUserToken>
    : IdentityUserContext<TUser, TKey, TUserClaim, TUserLogin, TUserToken>
         where TUser : IdentityUser<TKey>
         where TRole : IdentityRole<TKey>
         where TKey : IEquatable<TKey>
         where TUserClaim : IdentityUserClaim<TKey>
         where TUserRole : IdentityUserRole<TKey>
         where TUserLogin : IdentityUserLogin<TKey>
         where TRoleClaim : IdentityRoleClaim<TKey>
         where TUserToken : IdentityUserToken<TKey>

```

<span data-ttu-id="73f42-158">还有可能使用标识，而角色 （仅声明），在这种情况下`IdentityUserContext`应使用类：</span><span class="sxs-lookup"><span data-stu-id="73f42-158">It is also possible to use Identity without roles (only claims), in which case an `IdentityUserContext` class should be used:</span></span>


```CSharp
// Uses the built-in non-role Identity types except with a custom User type
// Uses `string` as the key type
public class IdentityUserContext<TUser>
    : IdentityUserContext<TUser, string>
        where TUser : IdentityUser
{
}

// Uses the built-in non-role Identity types except with a custom User type
// The key type is defined by TKey
public class IdentityUserContext<TUser, TKey>
    : IdentityUserContext<TUser, TKey, IdentityUserClaim<TKey>, IdentityUserLogin<TKey>, IdentityUserToken<TKey>>
        where TUser : IdentityUser<TKey>
        where TKey : IEquatable<TKey>
{
}

// No built-in Identity types are used; all are specified by generic arguments, with no roles
// The key type is defined by TKey
public abstract class IdentityUserContext<TUser, TKey, TUserClaim, TUserLogin, TUserToken>
    : DbContext
        where TUser : IdentityUser<TKey>
        where TKey : IEquatable<TKey>
        where TUserClaim : IdentityUserClaim<TKey>
        where TUserLogin : IdentityUserLogin<TKey>
        where TUserToken : IdentityUserToken<TKey>
{
}
```

## <a name="customizing-the-model"></a><span data-ttu-id="73f42-159">自定义模型</span><span class="sxs-lookup"><span data-stu-id="73f42-159">Customizing the model</span></span>

<span data-ttu-id="73f42-160">自定义模型的起点是派生自的合适的上下文类型;请参阅前面的部分。</span><span class="sxs-lookup"><span data-stu-id="73f42-160">The starting point for customizing the model is to derive from the appropriate context type; see the preceding section.</span></span> <span data-ttu-id="73f42-161">此上下文类型通常称为`ApplicationDbContext`和创建的 ASP.NET Core 模板。</span><span class="sxs-lookup"><span data-stu-id="73f42-161">This context type is customarily called `ApplicationDbContext` and is created by the ASP.NET Core templates.</span></span>

<span data-ttu-id="73f42-162">使用上下文以两种方式配置的模型：</span><span class="sxs-lookup"><span data-stu-id="73f42-162">The context is used to configure the model in two ways:</span></span>
* <span data-ttu-id="73f42-163">通过提供实体类型和密钥类型的泛型类型参数。</span><span class="sxs-lookup"><span data-stu-id="73f42-163">By supplying entity and key types for the generic type parameters.</span></span>
* <span data-ttu-id="73f42-164">通过重写`OnModelCreating`修改这些类型的映射。</span><span class="sxs-lookup"><span data-stu-id="73f42-164">By overriding `OnModelCreating` to modify the mapping of these types.</span></span>

<span data-ttu-id="73f42-165">在重写`OnModelCreating`，`base.OnModelCreating`应首先调用，重写应调用配置下一步。</span><span class="sxs-lookup"><span data-stu-id="73f42-165">When overriding `OnModelCreating`, `base.OnModelCreating` should be called first, the overriding configuration should be called next.</span></span> <span data-ttu-id="73f42-166">EF Core 通常具有配置的最后一个 wins 策略。</span><span class="sxs-lookup"><span data-stu-id="73f42-166">EF Core generally has a last-one-wins policy for configuration.</span></span> <span data-ttu-id="73f42-167">例如，如果`ToTable`实体类型是调用首先使用一个表名称和具有不同的表名称，然后再次更高版本，则第二次调用中的表名称是使用的一个。</span><span class="sxs-lookup"><span data-stu-id="73f42-167">For example, if the `ToTable` for an entity type is called first with one table name and then again later with a different table name, then the table name in the second call is the one that is used.</span></span>

### <a name="using-a-custom-user-type"></a><span data-ttu-id="73f42-168">使用自定义的用户类型</span><span class="sxs-lookup"><span data-stu-id="73f42-168">Using a custom User type</span></span>

<span data-ttu-id="73f42-169">若要使用自定义的用户类型，创建类型，并将其从继承`IdentityUser`。</span><span class="sxs-lookup"><span data-stu-id="73f42-169">To use a custom User type, create the type and have it inherit from `IdentityUser`.</span></span> <span data-ttu-id="73f42-170">通常将此类型`ApplicationUser`。</span><span class="sxs-lookup"><span data-stu-id="73f42-170">It is customary to name this type `ApplicationUser`.</span></span> <span data-ttu-id="73f42-171">此类型通常将基类型中不具有附加属性，否则将有任何值中创建它。</span><span class="sxs-lookup"><span data-stu-id="73f42-171">This type will typically have additional properties not in the base type, otherwise there would be no value in creating it.</span></span> <span data-ttu-id="73f42-172">例如：</span><span class="sxs-lookup"><span data-stu-id="73f42-172">For example:</span></span>

```CSharp
public class ApplicationUser : IdentityUser
{
    public string CustomTag { get; set; }
}
```

<span data-ttu-id="73f42-173">接下来将此类型用作泛型自变量上下文：</span><span class="sxs-lookup"><span data-stu-id="73f42-173">Next use this type as a generic argument for the context:</span></span>

```CSharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

<span data-ttu-id="73f42-174">更新`ConfigureServices`为使用新`ApplicationUser`类：</span><span class="sxs-lookup"><span data-stu-id="73f42-174">Update `ConfigureServices` to use the new `ApplicationUser` class:</span></span>

```CSharp
services.AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

<span data-ttu-id="73f42-175">无需重写`OnModelCreating`此处因为 EF Core 将映射`CustomTag`按照约定的属性。</span><span class="sxs-lookup"><span data-stu-id="73f42-175">There is no need to override `OnModelCreating` here because EF Core will map the `CustomTag` property by convention.</span></span> <span data-ttu-id="73f42-176">但是，数据库将需要更新，以获取新`CustomTag`列。</span><span class="sxs-lookup"><span data-stu-id="73f42-176">However, the database will need to be updated to get a new `CustomTag` column.</span></span> <span data-ttu-id="73f42-177">若要执行此操作，添加迁移，和中所述，然后更新数据库[标识和 EF Core 迁移](#identity-migrations)。</span><span class="sxs-lookup"><span data-stu-id="73f42-177">To do this, add a migration, and then update the database as described in  [Identity and EF Core Migrations](#identity-migrations).</span></span>

### <a name="changing-the-key-type"></a><span data-ttu-id="73f42-178">更改的键类型</span><span class="sxs-lookup"><span data-stu-id="73f42-178">Changing the key type</span></span>

<span data-ttu-id="73f42-179">创建数据库后更改的主键 (PK) 列类型会在很多数据库系统上出现问题。</span><span class="sxs-lookup"><span data-stu-id="73f42-179">Changing the type of a primary key (PK) column after the database has been created is problematic on many database systems.</span></span> <span data-ttu-id="73f42-180">更改在 PK 通常涉及除去并重新创建表。</span><span class="sxs-lookup"><span data-stu-id="73f42-180">Changing the PK typically involves dropping and re-creating the table.</span></span> <span data-ttu-id="73f42-181">因此，建议在消息以便创建数据库时创建的目标密钥类型，密钥类型指定的初始迁移。</span><span class="sxs-lookup"><span data-stu-id="73f42-181">Therefore, it is recommended that key types be specified in the initial migration such that the target key types are created when the database is created.</span></span>

<span data-ttu-id="73f42-182">如果已创建数据库，则`Drop-Database`(PMC) 或`dotnet ef database drop`(.NET Core CLI) 可用来将其删除。</span><span class="sxs-lookup"><span data-stu-id="73f42-182">If the database has been created, then `Drop-Database` (PMC) or `dotnet ef database drop` (.NET Core CLI) can be used to delete it.</span></span>

<span data-ttu-id="73f42-183">一旦确认数据库不存在，删除与初始迁移`Remove-Migration`(PMC) 或`dotnet ef migrations remove`(.NET Core CLI)。</span><span class="sxs-lookup"><span data-stu-id="73f42-183">Once it is confirmed that the database doesn't exist,  remove the initial migration with `Remove-Migration` (PMC) or `dotnet ef migrations remove` (.NET Core CLI).</span></span>

<span data-ttu-id="73f42-184">更新`ApplicationDbContext`以使用不同的基本类，指定的新键类型`TKey`。</span><span class="sxs-lookup"><span data-stu-id="73f42-184">Update the `ApplicationDbContext` to use a different base class, specifying the new key type for `TKey`.</span></span> <span data-ttu-id="73f42-185">例如，若要使用`Guid`密钥：</span><span class="sxs-lookup"><span data-stu-id="73f42-185">For example, to use a `Guid` key:</span></span>

```CSharp
public class ApplicationDbContext : IdentityDbContext<IdentityUser<Guid>, IdentityRole<Guid>, Guid>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

<span data-ttu-id="73f42-186">请注意，泛型类`IdentityUser<TKey>`和`IdentityRole<TKey>`还必须指定要使用新的密钥类型。</span><span class="sxs-lookup"><span data-stu-id="73f42-186">Notice that the generic classes `IdentityUser<TKey>` and `IdentityRole<TKey>` must also be specified to use the new key type.</span></span> <span data-ttu-id="73f42-187">`ConfigureServices` 必须更新为使用泛型的用户：</span><span class="sxs-lookup"><span data-stu-id="73f42-187">`ConfigureServices` must be updated to use the generic user:</span></span>

```CSharp
services.AddDefaultIdentity<IdentityUser<Guid>>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

<span data-ttu-id="73f42-188">如果自定义`ApplicationUser`是正在使用中，更新它以继承`IdentityUser<TKey>`。</span><span class="sxs-lookup"><span data-stu-id="73f42-188">If a custom `ApplicationUser` is being used, update it to inherit from `IdentityUser<TKey>`.</span></span> <span data-ttu-id="73f42-189">例如：</span><span class="sxs-lookup"><span data-stu-id="73f42-189">For example:</span></span>

```CSharp
public class ApplicationUser : IdentityUser<Guid>
{
    public string CustomTag { get; set; }
}

public class ApplicationDbContext : IdentityDbContext<ApplicationUser, IdentityRole<Guid>, Guid>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

```CSharp
services.AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

### <a name="adding-navigation-properties"></a><span data-ttu-id="73f42-190">添加导航属性</span><span class="sxs-lookup"><span data-stu-id="73f42-190">Adding navigation properties</span></span>

<span data-ttu-id="73f42-191">更改关系的模型配置可能会更加困难比进行其他更改。</span><span class="sxs-lookup"><span data-stu-id="73f42-191">Changing the model configuration for relationships can be a more difficult than making other changes.</span></span> <span data-ttu-id="73f42-192">必须格外小心，以替换现有的关系，而不是创建新的其他关系。</span><span class="sxs-lookup"><span data-stu-id="73f42-192">Care must be taken to replace the existing relationships rather than create a new additional relationships.</span></span> <span data-ttu-id="73f42-193">具体而言，已更改的关系必须指定相同的外键属性，作为现有的关系。</span><span class="sxs-lookup"><span data-stu-id="73f42-193">In particular, the changed relationship must specify the same foreign key property as the existing relationship.</span></span> <span data-ttu-id="73f42-194">例如，之间的关系`Users`和`UserClaims`指定为默认为：</span><span class="sxs-lookup"><span data-stu-id="73f42-194">For example, the relationship between `Users` and `UserClaims` is by default specified as:</span></span>

```CSharp
builder.Entity<TUser>(b =>
{
    // Each User can have many UserClaims
    b.HasMany<TUserClaim>()
     .WithOne()
     .HasForeignKey(uc => uc.UserId)
     .IsRequired();
});
```

<span data-ttu-id="73f42-195">为此关系的外键指定为`UserClaim.UserId`属性。</span><span class="sxs-lookup"><span data-stu-id="73f42-195">The foreign key for this relationship is specified as the `UserClaim.UserId` property.</span></span> <span data-ttu-id="73f42-196">`HasMany` 和`WithOne`调用不带参数来创建不使用导航属性关系。</span><span class="sxs-lookup"><span data-stu-id="73f42-196">`HasMany` and `WithOne` are called without arguments to create the relationship without navigation properties.</span></span>

<span data-ttu-id="73f42-197">添加到导航属性`ApplicationUser`这将允许关联`UserClaims`用户引用：</span><span class="sxs-lookup"><span data-stu-id="73f42-197">Add a navigation property to `ApplicationUser` that will allow associated `UserClaims` to be referenced from the user:</span></span>

```CSharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
}
```

<span data-ttu-id="73f42-198">请注意，`TKey`为`IdentityUserClaim<TKey>`是指定的用户-在此情况下为主键类型`string`由于我们将使用默认值。</span><span class="sxs-lookup"><span data-stu-id="73f42-198">Note that the `TKey` for `IdentityUserClaim<TKey>` is type specified for the primary key of users--in this case `string` since we're using the defaults.</span></span> <span data-ttu-id="73f42-199">它是**不**的主键类型`UserClaim`实体类型。</span><span class="sxs-lookup"><span data-stu-id="73f42-199">It is **not** the primary key type for the `UserClaim` entity type.</span></span>

<span data-ttu-id="73f42-200">现在，存在导航属性，则必须将它配置中`OnModelCreating`:</span><span class="sxs-lookup"><span data-stu-id="73f42-200">Now that the navigation property exists it must be configured in `OnModelCreating`:</span></span>

```CSharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();
        });
    }
}
```

<span data-ttu-id="73f42-201">请注意关系是否已配置的完全一致之前，只能使用指定的调用中的导航属性`HasMany`。</span><span class="sxs-lookup"><span data-stu-id="73f42-201">Notice that relationship is configured exactly as it was before, only with a navigation property specified in the call to `HasMany`.</span></span>

<span data-ttu-id="73f42-202">在 EF 模型，不是数据库中仅存在导航属性。</span><span class="sxs-lookup"><span data-stu-id="73f42-202">The navigation properties only exist in the EF model, not the database.</span></span> <span data-ttu-id="73f42-203">因为尚未更改外的键关系，这种类型的模型更改不需要更新的数据库。</span><span class="sxs-lookup"><span data-stu-id="73f42-203">Because the foreign key for the relationship has not changed, this kind of model change does not require the database to be updated.</span></span> <span data-ttu-id="73f42-204">这可以通过添加后进行更改的迁移检查：`Up`和`Down`方法为空。</span><span class="sxs-lookup"><span data-stu-id="73f42-204">This can be checked by adding a migration after making the change: the `Up` and `Down` methods are empty.</span></span>

### <a name="adding-all-user-navigation-properties"></a><span data-ttu-id="73f42-205">添加所有用户导航属性</span><span class="sxs-lookup"><span data-stu-id="73f42-205">Adding all User navigation properties</span></span>

<span data-ttu-id="73f42-206">使用上的一节中作为指南，此处是用户配置的所有关系的单向导航属性的示例：</span><span class="sxs-lookup"><span data-stu-id="73f42-206">Using the section above as guidance, here is an example that configures unidirectional navigation properties for all relationships on User:</span></span>

```CSharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
    public virtual ICollection<IdentityUserLogin<string>> Logins { get; set; }
    public virtual ICollection<IdentityUserToken<string>> Tokens { get; set; }
    public virtual ICollection<IdentityUserRole<string>> UserRoles { get; set; }
}
```

```CSharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne()
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne()
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne()
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });
    }
}
```

### <a name="adding-user-and-role-navigation-properties"></a><span data-ttu-id="73f42-207">添加用户和角色导航属性</span><span class="sxs-lookup"><span data-stu-id="73f42-207">Adding User and Role navigation properties</span></span>

<span data-ttu-id="73f42-208">使用上的一节中作为指南，此处是用户和角色配置的所有关系的导航属性的示例：</span><span class="sxs-lookup"><span data-stu-id="73f42-208">Using the section above as guidance, here is an example that configures navigation properties for all relationships on User and Role:</span></span>

```CSharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
    public virtual ICollection<IdentityUserLogin<string>> Logins { get; set; }
    public virtual ICollection<IdentityUserToken<string>> Tokens { get; set; }
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationRole : IdentityRole
{
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationUserRole : IdentityUserRole<string>
{
    public virtual ApplicationUser User { get; set; }
    public virtual ApplicationRole Role { get; set; }
}
```

```CSharp
public class ApplicationDbContext
    : IdentityDbContext<
        ApplicationUser, ApplicationRole, string,
        IdentityUserClaim<string>, ApplicationUserRole, IdentityUserLogin<string>,
        IdentityRoleClaim<string>, IdentityUserToken<string>>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne()
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne()
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.User)
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });

        modelBuilder.Entity<ApplicationRole>(b =>
        {
            // Each Role can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.Role)
                .HasForeignKey(ur => ur.RoleId)
                .IsRequired();
        });

    }
}
```

<span data-ttu-id="73f42-209">注意：</span><span class="sxs-lookup"><span data-stu-id="73f42-209">Notes:</span></span>

* <span data-ttu-id="73f42-210">此示例还包括`UserRole`加入实体，需导航从用户角色的多对多关系。</span><span class="sxs-lookup"><span data-stu-id="73f42-210">This example also includes the `UserRole` join entity, which is needed to navigate the many-to-many relationship from Users to Roles.</span></span>
* <span data-ttu-id="73f42-211">请记得将更改类型的导航属性以反映该`ApplicationXxx`类型现在正在使用而不是`IdentityXxx`类型。</span><span class="sxs-lookup"><span data-stu-id="73f42-211">Remember to change the types of the navigation properties to reflect that `ApplicationXxx` types are now being used instead of `IdentityXxx` types.</span></span>
* <span data-ttu-id="73f42-212">请记住使用`ApplicationXxx`中泛型`ApplicationContext`定义。</span><span class="sxs-lookup"><span data-stu-id="73f42-212">Remember to use the `ApplicationXxx` in the generic `ApplicationContext` definition.</span></span>

### <a name="adding-all-navigation-properties"></a><span data-ttu-id="73f42-213">添加所有导航属性</span><span class="sxs-lookup"><span data-stu-id="73f42-213">Adding all navigation properties</span></span>

<span data-ttu-id="73f42-214">使用上的一节中作为指南，此处是所有实体类型配置的所有关系的导航属性的示例：</span><span class="sxs-lookup"><span data-stu-id="73f42-214">Using the section above as guidance, here is an example that configures navigation properties for all relationships on all entity types:</span></span>

```CSharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<ApplicationUserClaim> Claims { get; set; }
    public virtual ICollection<ApplicationUserLogin> Logins { get; set; }
    public virtual ICollection<ApplicationUserToken> Tokens { get; set; }
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationRole : IdentityRole
{
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
    public virtual ICollection<ApplicationRoleClaim> RoleClaims { get; set; }
}

public class ApplicationUserRole : IdentityUserRole<string>
{
    public virtual ApplicationUser User { get; set; }
    public virtual ApplicationRole Role { get; set; }
}

public class ApplicationUserClaim : IdentityUserClaim<string>
{
    public virtual ApplicationUser User { get; set; }
}

public class ApplicationUserLogin : IdentityUserLogin<string>
{
    public virtual ApplicationUser User { get; set; }
}

public class ApplicationRoleClaim : IdentityRoleClaim<string>
{
    public virtual ApplicationRole Role { get; set; }
}

public class ApplicationUserToken : IdentityUserToken<string>
{
    public virtual ApplicationUser User { get; set; }
}
```

```CSharp
public class ApplicationDbContext
    : IdentityDbContext<
        ApplicationUser, ApplicationRole, string,
        ApplicationUserClaim, ApplicationUserRole, ApplicationUserLogin,
        ApplicationRoleClaim, ApplicationUserToken>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne(e => e.User)
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne(e => e.User)
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne(e => e.User)
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.User)
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });

        modelBuilder.Entity<ApplicationRole>(b =>
        {
            // Each Role can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.Role)
                .HasForeignKey(ur => ur.RoleId)
                .IsRequired();

            // Each Role can have many associated RoleClaims
            b.HasMany(e => e.RoleClaims)
                .WithOne(e => e.Role)
                .HasForeignKey(rc => rc.RoleId)
                .IsRequired();
        });

    }
}
```

### <a name="using-composite-keys"></a><span data-ttu-id="73f42-215">使用复合键</span><span class="sxs-lookup"><span data-stu-id="73f42-215">Using composite keys</span></span>

<span data-ttu-id="73f42-216">前面几节所示更改标识模型中使用的键的类型。</span><span class="sxs-lookup"><span data-stu-id="73f42-216">The preceding sections demonstrated changing the type of key used in the Identity model.</span></span> <span data-ttu-id="73f42-217">更改要使用复合键的标识键模型是不受支持或建议。</span><span class="sxs-lookup"><span data-stu-id="73f42-217">Changing the Identity key model to use composite keys is not supported or recommended.</span></span> <span data-ttu-id="73f42-218">使用具有标识的复合键会涉及更改标识管理器代码如何与模型，这是不受支持的自定义项和超出本文的讨论范围交互。</span><span class="sxs-lookup"><span data-stu-id="73f42-218">Using a composite key with Identity would involve changing how the Identity manager code interacts with the model, which is an unsupported customization and beyond the scope of this document.</span></span>

### <a name="changing-tablecolumn-names-and-facets"></a><span data-ttu-id="73f42-219">更改表/列名称以及方面</span><span class="sxs-lookup"><span data-stu-id="73f42-219">Changing table/column names and facets</span></span>

<span data-ttu-id="73f42-220">若要更改的表和列的名称，调用`base.OnModelCreating`，然后添加配置，以重写任何默认值。</span><span class="sxs-lookup"><span data-stu-id="73f42-220">To change the names of tables and columns, call `base.OnModelCreating`, and then add configuration to override any of the defaults.</span></span> <span data-ttu-id="73f42-221">例如，若要更改的标识的所有表名称：</span><span class="sxs-lookup"><span data-stu-id="73f42-221">For example, to change the name of all the identity tables:</span></span>

```CSharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.ToTable("MyUsers");
    });

    modelBuilder.Entity<IdentityUserClaim<string>>(b =>
    {
        b.ToTable("MyUserClaims");
    });

    modelBuilder.Entity<IdentityUserLogin<string>>(b =>
    {
        b.ToTable("MyUserLogins");
    });

    modelBuilder.Entity<IdentityUserToken<string>>(b =>
    {
        b.ToTable("MyUserTokens");
    });

    modelBuilder.Entity<IdentityRole>(b =>
    {
        b.ToTable("MyRoles");
    });

    modelBuilder.Entity<IdentityRoleClaim<string>>(b =>
    {
        b.ToTable("MyRoleClaims");
    });

    modelBuilder.Entity<IdentityUserRole<string>>(b =>
    {
        b.ToTable("MyUserRoles");
    });
}
```

<span data-ttu-id="73f42-222">请注意，这些示例使用默认标识类型。</span><span class="sxs-lookup"><span data-stu-id="73f42-222">Note that these examples use the default Identity types.</span></span> <span data-ttu-id="73f42-223">如果你正在使用的应用程序类型，如`ApplicationUser`然后配置该类型而不是默认类型。</span><span class="sxs-lookup"><span data-stu-id="73f42-223">If you are using an application type, such as `ApplicationUser` then configure that type instead of the default type.</span></span>

<span data-ttu-id="73f42-224">下面是一个示例，更改某些列名称：</span><span class="sxs-lookup"><span data-stu-id="73f42-224">Here is an example that changes some column names:</span></span>

```CSharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.Property(e => e.Email).HasColumnName("EMail");
    });

    modelBuilder.Entity<IdentityUserClaim<string>>(b =>
    {
        b.Property(e => e.ClaimType).HasColumnName("CType");
        b.Property(e => e.ClaimValue).HasColumnName("CValue");
    });
}
```

<span data-ttu-id="73f42-225">可以使用某些配置某些类型的数据库列_方面_如允许的最大字符串长度。</span><span class="sxs-lookup"><span data-stu-id="73f42-225">Some types of database columns can be configured with certain _facets_ such as the maximum string length allowed.</span></span> <span data-ttu-id="73f42-226">下面是示例模型中设置列的多个字符串属性的最大长度：</span><span class="sxs-lookup"><span data-stu-id="73f42-226">Here is an example that sets column max lengths for several string properties in the model:</span></span>

```CSharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.Property(u => u.UserName).HasMaxLength(128);
        b.Property(u => u.NormalizedUserName).HasMaxLength(128);
        b.Property(u => u.Email).HasMaxLength(128);
        b.Property(u => u.NormalizedEmail).HasMaxLength(128);
    });

    modelBuilder.Entity<IdentityUserToken<string>>(b =>
    {
        b.Property(t => t.LoginProvider).HasMaxLength(128);
        b.Property(t => t.Name).HasMaxLength(128);
    });
}
```

### <a name="mapping-to-a-different-schema"></a><span data-ttu-id="73f42-227">将映射到不同的架构</span><span class="sxs-lookup"><span data-stu-id="73f42-227">Mapping to a different schema</span></span>

<span data-ttu-id="73f42-228">架构可以具有的行为以不同的方式不同的数据库提供程序中，但对于 SQL Server 默认值是"dbo"架构中创建所有表。</span><span class="sxs-lookup"><span data-stu-id="73f42-228">Schemas can behave differently in different database providers, but for SQL Server, the default is to create all tables in the "dbo" schema.</span></span> <span data-ttu-id="73f42-229">可以更改此项以改为在不同的架构中创建表。</span><span class="sxs-lookup"><span data-stu-id="73f42-229">This can be changed to instead create the tables in a different schema.</span></span> <span data-ttu-id="73f42-230">例如：</span><span class="sxs-lookup"><span data-stu-id="73f42-230">For example:</span></span>

```CSharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.HasDefaultSchema("notdbo");
}
```

### <a name="lazy-loading"></a><span data-ttu-id="73f42-231">延迟加载</span><span class="sxs-lookup"><span data-stu-id="73f42-231">Lazy loading</span></span>

<span data-ttu-id="73f42-232">在本部分中添加了对标识模型中的延迟加载代理支持。</span><span class="sxs-lookup"><span data-stu-id="73f42-232">In this section support for lazy-loading proxies in the Identity model is added.</span></span> <span data-ttu-id="73f42-233">Lazy 加载很有用，因为它允许使用未第一个，则确保加载这些导航属性。</span><span class="sxs-lookup"><span data-stu-id="73f42-233">Lazy-loading is useful since it allows navigation properties to be used without first ensuring they are loaded.</span></span>

<span data-ttu-id="73f42-234">实体类型可适用于采用多种方式的延迟加载中所述[EF Core 文档](/ef/core/querying/related-data#lazy-loading)。</span><span class="sxs-lookup"><span data-stu-id="73f42-234">Entity types can be made suitable for lazy-loading in several ways, as described in the [EF Core documentation](/ef/core/querying/related-data#lazy-loading).</span></span> <span data-ttu-id="73f42-235">为简单起见，我们将使用延迟加载代理，该软件需要：</span><span class="sxs-lookup"><span data-stu-id="73f42-235">For simplicity, we will use lazy-loading proxies, which requires:</span></span>

* <span data-ttu-id="73f42-236">安装[Microsoft.EntityFrameworkCore.Proxies](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Proxies/)包。</span><span class="sxs-lookup"><span data-stu-id="73f42-236">Installation of the [Microsoft.EntityFrameworkCore.Proxies](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Proxies/) package.</span></span>
* <span data-ttu-id="73f42-237">调用`.UseLazyLoadingProxies()`内`AddDbContext`。</span><span class="sxs-lookup"><span data-stu-id="73f42-237">A call to `.UseLazyLoadingProxies()` inside `AddDbContext`.</span></span>
* <span data-ttu-id="73f42-238">具有公共虚拟导航属性的公共实体类型。</span><span class="sxs-lookup"><span data-stu-id="73f42-238">Public entity types with public virtual navigation properties.</span></span>

<span data-ttu-id="73f42-239">下面是一个示例调用`.UseLazyLoadingProxies()`:</span><span class="sxs-lookup"><span data-stu-id="73f42-239">Here is an example of calling `.UseLazyLoadingProxies()`:</span></span>

```CSharp
services
    .AddDbContext<ApplicationDbContext>(
        b => b.UseSqlServer(connectionString)
            .UseLazyLoadingProxies())
    .AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

<span data-ttu-id="73f42-240">回头参考上面的示例获取将导航属性添加到实体类型。</span><span class="sxs-lookup"><span data-stu-id="73f42-240">Refer back to the examples above for adding navigation properties to the entity types.</span></span>
