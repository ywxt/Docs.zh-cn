---
title: 标识模型自定义项
author: ajcvickers
description: 本文介绍如何为 ASP.NET 核心标识自定义的基础的实体框架核心数据模型。
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
# <a name="identity-model-customization"></a>标识模型自定义项

通过[Arthur Vickers](https://github.com/ajcvickers)

ASP.NET 核心标识提供一个框架，用于管理和 ASP.NET Core 应用程序中存储用户帐户。 标识添加到项目中，选中"单个用户帐户"时作为身份验证机制。 默认情况下，标识将使用的 Entity Framework (EF) 核心数据模型。 本文介绍如何自定义标识模型。

<a name="identity-migrations"></a>

## <a name="identity-and-ef-core-migrations"></a>标识和 EF 核心迁移

之前检查模型，它是有助于了解如何标识配合[EF 核心迁移](/ef/core/managing-schemas/migrations/)创建和更新数据库。 最高层的过程是：

1. 定义或更新[代码中的数据模型](/ef/core/modeling/)。
1. 添加迁移，以将此模型转换可以应用于数据库的更改。
1. 检查迁移能正确地表示您的意图。
1. 将应用迁移更新数据库要与模型同步。
1. 重复步骤 1-4 以进一步优化模型并使数据库保持同步。

迁移添加和使用应用：

* [程序包管理器控制台](/ef/core/miscellaneous/cli/powershell)(PMC) 如果你使用的 Visual Studio。
* [Dotnet 命令](/ef/core/miscellaneous/cli/dotnet)命令行上。
* 运行应用程序时，请选择错误页上的迁移链接。

ASP.NET 核心有可用于应用程序运行时应用迁移一个开发时间错误页处理程序。 对于生产应用程序，它通常会更适合从迁移中生成 SQL 脚本，将部署到数据库作为受控的应用程序和数据库部署的一部分。

创建新的应用程序使用标识时，已经完成上述步骤 1 和 2。 也就是说，初始数据模型已存在，并已添加到项目中的初始迁移。 仍然需要应用于数据库初始迁移。 通过运行更新数据库 (PMC)，dotnet ef 数据库更新 (.NET 核心 CLI) 命令，或通过在运行应用程序使用错误页，则可以完成的初始迁移。

需要对模型进行更改时重复前面的步骤。

<a name="identity-model"></a>

## <a name="the-identity-model"></a>标识模型

### <a name="entity-types"></a>实体类型

标识模型包含七个实体类型：

* `User` -表示的用户
* `Role` -表示的角色
* `UserClaim` -表示用户拥有的声明
* `UserToken` -表示用户的身份验证令牌
* `UserLogin` -将用户与一个登录名相关联
* `RoleClaim` -表示将授予角色中的所有用户的声明
* `UserRole` -加入将用户和角色相关联的实体

### <a name="entity-type-relationships"></a>实体类型关系

这些实体类型通过以下方式彼此相关：

* 每个`User`可以具有许多 `UserClaims`
* 每个`User`可以具有许多 `UserLogins`
* 每个`User`可以具有许多 `UserTokens`
* 每个`Role`可以具有许多关联 `RoleClaims`
* 每个`User`可以具有许多关联`Roles`，和每个`Role`可以与多个用户相关联
  * 这是一个多对多关系，这需要在数据库中的联接表。 联接表均由表示`UserRole`实体。

### <a name="default-model-configuration"></a>默认模型配置

标识定义的"上下文类"的继承了各种[DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext)配置和使用模型。 进行此配置使用[EF 核心代码 First Fluent API](/ef/core/modeling/)中[OnModelCreating](/dotnet/api/microsoft.entityframeworkcore.dbcontext.onmodelcreating#Microsoft_EntityFrameworkCore_DbContext_OnModelCreating_Microsoft_EntityFrameworkCore_ModelBuilder_)上下文类的方法。 默认配置是：

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

### <a name="model-generic-types"></a>模型的泛型类型

标识定义为每个上面列出的实体类型的默认 CLR 类型。 这些类型全都带有前缀"标识": `IdentityUser`， `IdentityRole`， `IdentityUserClaim`， `IdentityUserToken`， `IdentityUserLogin`， `IdentityRoleClaim`，和`IdentityUserRole`。

而不是直接使用这些类型，类型可以用作基类，这些类为应用程序自身的类型。 `DbContext`定义标识的类是泛型的这样的： 不同的 CLR 类型可以用于一个或多个模型中的实体类型。 以下泛型类型还允许用户主键的类型更改。

对于角色，支持使用标识时[IdentityDbContext](/dotnet/api/microsoft.aspnetcore.identity.entityframeworkcore.identitydbcontext)应使用类：

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

还有可能使用标识，而角色 （仅声明），在这种情况下`IdentityUserContext`应使用类：


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

## <a name="customizing-the-model"></a>自定义模型

自定义模型的起点是派生自的合适的上下文类型;请参阅前面的部分。 此上下文类型通常称为`ApplicationDbContext`和创建的 ASP.NET Core 模板。

使用上下文以两种方式配置的模型：
* 通过提供实体类型和密钥类型的泛型类型参数。
* 通过重写`OnModelCreating`修改这些类型的映射。

在重写`OnModelCreating`，`base.OnModelCreating`应首先调用，重写应调用配置下一步。 EF 核心通常具有配置的最后一个 wins 策略。 例如，如果`ToTable`实体类型是调用首先使用一个表名称和具有不同的表名称，然后再次更高版本，则第二次调用中的表名称是使用的一个。

### <a name="using-a-custom-user-type"></a>使用自定义的用户类型

若要使用自定义的用户类型，创建类型，并将其从继承`IdentityUser`。 通常将此类型`ApplicationUser`。 此类型通常将基类型中不具有附加属性，否则将有任何值中创建它。 例如：

```CSharp
public class ApplicationUser : IdentityUser
{
    public string CustomTag { get; set; }
}
```

接下来将此类型用作泛型自变量上下文：

```CSharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

更新`ConfigureServices`为使用新`ApplicationUser`类：

```CSharp
services.AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

无需重写`OnModelCreating`此处因为 EF 核心将映射`CustomTag`按照约定的属性。 但是，数据库将需要更新，以获取新`CustomTag`列。 若要执行此操作，添加迁移，和中所述，然后更新数据库[标识和 EF 核心迁移](#identity-migrations)。

### <a name="changing-the-key-type"></a>更改的键类型

创建数据库后更改的主键 (PK) 列类型会在很多数据库系统上出现问题。 更改在 PK 通常涉及除去并重新创建表。 因此，建议在消息以便创建数据库时创建的目标密钥类型，密钥类型指定的初始迁移。

如果已创建数据库，则`Drop-Database`(PMC) 或`dotnet ef database drop`(.NET 核心 CLI) 可用来将其删除。

一旦确认数据库不存在，删除与初始迁移`Remove-Migration`(PMC) 或`dotnet ef migrations remove`(.NET 核心 CLI)。

更新`ApplicationDbContext`以使用不同的基本类，指定的新键类型`TKey`。 例如，若要使用`Guid`密钥：

```CSharp
public class ApplicationDbContext : IdentityDbContext<IdentityUser<Guid>, IdentityRole<Guid>, Guid>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

请注意，泛型类`IdentityUser<TKey>`和`IdentityRole<TKey>`还必须指定要使用新的密钥类型。 `ConfigureServices` 必须更新为使用泛型的用户：

```CSharp
services.AddDefaultIdentity<IdentityUser<Guid>>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

如果自定义`ApplicationUser`是正在使用中，更新它以继承`IdentityUser<TKey>`。 例如：

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

### <a name="adding-navigation-properties"></a>添加导航属性

更改关系的模型配置可能会更加困难比进行其他更改。 必须格外小心，以替换现有的关系，而不是创建新的其他关系。 具体而言，已更改的关系必须指定相同的外键属性，作为现有的关系。 例如，之间的关系`Users`和`UserClaims`指定为默认为：

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

为此关系的外键指定为`UserClaim.UserId`属性。 `HasMany` 和`WithOne`调用不带参数来创建不使用导航属性关系。

添加到导航属性`ApplicationUser`这将允许关联`UserClaims`用户引用：

```CSharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
}
```

请注意，`TKey`为`IdentityUserClaim<TKey>`是指定的用户-在此情况下为主键类型`string`由于我们将使用默认值。 它是**不**的主键类型`UserClaim`实体类型。

现在，存在导航属性，则必须将它配置中`OnModelCreating`:

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

请注意关系是否已配置的完全一致之前，只能使用指定的调用中的导航属性`HasMany`。

在 EF 模型，不是数据库中仅存在导航属性。 因为尚未更改外的键关系，这种类型的模型更改不需要更新的数据库。 这可以通过添加后进行更改的迁移检查：`Up`和`Down`方法为空。

### <a name="adding-all-user-navigation-properties"></a>添加所有用户导航属性

使用上的一节中作为指南，此处是用户配置的所有关系的单向导航属性的示例：

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

### <a name="adding-user-and-role-navigation-properties"></a>添加用户和角色导航属性

使用上的一节中作为指南，此处是用户和角色配置的所有关系的导航属性的示例：

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

注意：

* 此示例还包括`UserRole`加入实体，需导航从用户角色的多对多关系。
* 请记得将更改类型的导航属性以反映该`ApplicationXxx`类型现在正在使用而不是`IdentityXxx`类型。
* 请记住使用`ApplicationXxx`中泛型`ApplicationContext`定义。

### <a name="adding-all-navigation-properties"></a>添加所有导航属性

使用上的一节中作为指南，此处是所有实体类型配置的所有关系的导航属性的示例：

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

### <a name="using-composite-keys"></a>使用复合键

前面几节所示更改标识模型中使用的键的类型。 更改要使用复合键的标识键模型是不受支持或建议。 使用具有标识的复合键会涉及更改标识管理器代码如何与模型，这是不受支持的自定义项和超出本文的讨论范围交互。

### <a name="changing-tablecolumn-names-and-facets"></a>更改表/列名称以及方面

若要更改的表和列的名称，调用`base.OnModelCreating`，然后添加配置，以重写任何默认值。 例如，若要更改的标识的所有表名称：

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

请注意，这些示例使用默认标识类型。 如果你正在使用的应用程序类型，如`ApplicationUser`然后配置该类型而不是默认类型。

下面是一个示例，更改某些列名称：

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

可以使用某些配置某些类型的数据库列_方面_如允许的最大字符串长度。 下面是示例模型中设置列的多个字符串属性的最大长度：

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

### <a name="mapping-to-a-different-schema"></a>将映射到不同的架构

架构可以具有的行为以不同的方式不同的数据库提供程序中，但对于 SQL Server 默认值是"dbo"架构中创建所有表。 可以更改此项以改为在不同的架构中创建表。 例如：

```CSharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.HasDefaultSchema("notdbo");
}
```

### <a name="lazy-loading"></a>延迟加载

在本部分中添加了对标识模型中的延迟加载代理支持。 Lazy 加载很有用，因为它允许使用未第一个，则确保加载这些导航属性。

实体类型可适用于采用多种方式的延迟加载中所述[EF 核心文档](/ef/core/querying/related-data#lazy-loading)。 为简单起见，我们将使用延迟加载代理，该软件需要：

* 安装[Microsoft.EntityFrameworkCore.Proxies](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Proxies/)包。
* 调用`.UseLazyLoadingProxies()`内`AddDbContext`。
* 具有公共虚拟导航属性的公共实体类型。

下面是一个示例调用`.UseLazyLoadingProxies()`:

```CSharp
services
    .AddDbContext<ApplicationDbContext>(
        b => b.UseSqlServer(connectionString)
            .UseLazyLoadingProxies())
    .AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

回头参考上面的示例获取将导航属性添加到实体类型。
