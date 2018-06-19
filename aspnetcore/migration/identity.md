---
title: 将身份验证和标识迁移到 ASP.NET 核心
author: ardalis
description: 了解如何将身份验证和标识从 ASP.NET MVC 项目迁移到 ASP.NET 核心 MVC 项目。
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: migration/identity
ms.openlocfilehash: 2a80274e9056b41e370f199c7d41865db5fcedd7
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
ms.locfileid: "33851438"
---
# <a name="migrate-authentication-and-identity-to-aspnet-core"></a>将身份验证和标识迁移到 ASP.NET 核心

作者：[Steve Smith](https://ardalis.com/)

在以前的文章中，我们[配置从 ASP.NET MVC 项目迁移到 ASP.NET 核心 MVC](xref:migration/configuration)。 在本文中，我们将迁移的注册、 登录名和用户管理功能。

## <a name="configure-identity-and-membership"></a>配置的标识和成员身份

在 ASP.NET MVC 中，使用 ASP.NET Identity 中配置身份验证和标识功能*Startup.Auth.cs*和*IdentityConfig.cs*为位于*App_Start*文件夹。 在 ASP.NET 核心 MVC，这些功能在中配置*Startup.cs*。

安装`Microsoft.AspNetCore.Identity.EntityFrameworkCore`和`Microsoft.AspNetCore.Authentication.Cookies`NuGet 包。

然后，打开*Startup.cs*和更新`Startup.ConfigureServices`要使用实体框架和标识服务的方法：

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add EF services to the services container.
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

    services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

     services.AddMvc();
}
```

在这种情况下，有两种在上面的代码中，我们尚未尚未迁移从 ASP.NET MVC 项目中引用的类型：`ApplicationDbContext`和`ApplicationUser`。 创建一个新*模型*文件夹中 ASP.NET Core 项目，并将两个类添加到它对应于这些类型。 你将找到 ASP.NET MVC 的这些类中的版本 */Models/IdentityModels.cs*，但我们将使用每个已迁移的项目中的类的一个文件，因为它是更清晰。

*ApplicationUser.cs*:

```csharp
using Microsoft.AspNetCore.Identity.EntityFrameworkCore;

namespace NewMvcProject.Models
{
  public class ApplicationUser : IdentityUser
  {
  }
}
```

*ApplicationDbContext.cs*:

```csharp
using Microsoft.AspNetCore.Identity.EntityFramework;
using Microsoft.Data.Entity;

namespace NewMvcProject.Models
{
    public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }

        protected override void OnModelCreating(ModelBuilder builder)
        {
            base.OnModelCreating(builder);
            // Customize the ASP.NET Identity model and override the defaults if needed.
            // For example, you can rename the ASP.NET Identity table names and more.
            // Add your customizations after calling base.OnModelCreating(builder);
        }
    }
}
```

ASP.NET 核心 MVC 初学者 Web 项目不包括多的自定义的用户，或`ApplicationDbContext`。 当迁移实际应用程序时，你还需要迁移的所有自定义属性和方法的应用程序的用户和`DbContext`类，以及你的应用程序使用的任何其他模型类。 例如，如果你`DbContext`具有`DbSet<Album>`，你需要迁移`Album`类。

与就地情况下，这些文件*Startup.cs*文件可以进行编译，方法是更新其`using`语句：

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Identity;
using Microsoft.AspNetCore.Hosting;
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
```

我们的应用程序现在已准备好支持身份验证和标识服务。 它只需要具有向用户公开这些功能。

## <a name="migrate-registration-and-login-logic"></a>迁移注册和登录名逻辑

使用标识服务对应用程序配置和使用实体框架和 SQL Server 配置的数据访问，我们已准备好将支持注册和登录名添加到应用程序。 回想一下，[前面的迁移过程](xref:migration/mvc#migrate-the-layout-file)我们注释掉对的引用 *_LoginPartial*中 *_Layout.cshtml*。 现在，它是返回到该代码中，取消注释它，并在必要的控制器视图和视图，以支持登录功能将添加的时间。

取消注释`@Html.Partial`中一行 *_Layout.cshtml*:

```cshtml
      <li>@Html.ActionLink("Contact", "Contact", "Home")</li>
    </ul>
    @*@Html.Partial("_LoginPartial")*@
  </div>
</div>
```

现在，添加一个新的 Razor 视图调用 *_LoginPartial*到*视图/共享*文件夹：

更新 *_LoginPartial.cshtml*替换为以下代码 （替换其内容的所有）：

```cshtml
@inject SignInManager<ApplicationUser> SignInManager
@inject UserManager<ApplicationUser> UserManager

@if (SignInManager.IsSignedIn(User))
{
    <form asp-area="" asp-controller="Account" asp-action="Logout" method="post" id="logoutForm" class="navbar-right">
        <ul class="nav navbar-nav navbar-right">
            <li>
                <a asp-area="" asp-controller="Manage" asp-action="Index" title="Manage">Hello @UserManager.GetUserName(User)!</a>
            </li>
            <li>
                <button type="submit" class="btn btn-link navbar-btn navbar-link">Log out</button>
            </li>
        </ul>
    </form>
}
else
{
    <ul class="nav navbar-nav navbar-right">
        <li><a asp-area="" asp-controller="Account" asp-action="Register">Register</a></li>
        <li><a asp-area="" asp-controller="Account" asp-action="Login">Log in</a></li>
    </ul>
}
```

此时，你应能够刷新浏览器中的站点。

## <a name="summary"></a>总结

ASP.NET 核心引入 ASP.NET 标识功能更改。 在本文中，你看到了如何将 ASP.NET 标识的身份验证和用户管理功能迁移到 ASP.NET 核心。
