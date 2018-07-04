---
title: 将身份验证和标识迁移到 ASP.NET Core
author: ardalis
description: 了解如何将身份验证和标识从 ASP.NET MVC 项目迁移到 ASP.NET Core MVC 项目。
ms.author: riande
ms.date: 10/14/2016
uid: migration/identity
ms.openlocfilehash: e05d72ca78c7b8191a47f78cda31ee40e04d0706
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275692"
---
# <a name="migrate-authentication-and-identity-to-aspnet-core"></a><span data-ttu-id="d8bf4-103">将身份验证和标识迁移到 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d8bf4-103">Migrate Authentication and Identity to ASP.NET Core</span></span>

<span data-ttu-id="d8bf4-104">作者：[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="d8bf4-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="d8bf4-105">在以前的文章中，我们[配置从 ASP.NET MVC 项目迁移到 ASP.NET Core MVC](xref:migration/configuration)。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-105">In the previous article, we [migrated configuration from an ASP.NET MVC project to ASP.NET Core MVC](xref:migration/configuration).</span></span> <span data-ttu-id="d8bf4-106">在本文中，我们将迁移的注册、 登录名和用户管理功能。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-106">In this article, we migrate the registration, login, and user management features.</span></span>

## <a name="configure-identity-and-membership"></a><span data-ttu-id="d8bf4-107">配置的标识和成员身份</span><span class="sxs-lookup"><span data-stu-id="d8bf4-107">Configure Identity and Membership</span></span>

<span data-ttu-id="d8bf4-108">在 ASP.NET MVC 中，使用 ASP.NET Identity 中配置身份验证和标识功能*Startup.Auth.cs*和*IdentityConfig.cs*为位于*App_Start*文件夹。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-108">In ASP.NET MVC, authentication and identity features are configured using ASP.NET Identity in *Startup.Auth.cs* and *IdentityConfig.cs*, located in the *App_Start* folder.</span></span> <span data-ttu-id="d8bf4-109">在 ASP.NET Core MVC，这些功能在中配置*Startup.cs*。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-109">In ASP.NET Core MVC, these features are configured in *Startup.cs*.</span></span>

<span data-ttu-id="d8bf4-110">安装`Microsoft.AspNetCore.Identity.EntityFrameworkCore`和`Microsoft.AspNetCore.Authentication.Cookies`NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-110">Install the `Microsoft.AspNetCore.Identity.EntityFrameworkCore` and `Microsoft.AspNetCore.Authentication.Cookies` NuGet packages.</span></span>

<span data-ttu-id="d8bf4-111">然后，打开*Startup.cs*和更新`Startup.ConfigureServices`要使用实体框架和标识服务的方法：</span><span class="sxs-lookup"><span data-stu-id="d8bf4-111">Then, open *Startup.cs* and update the `Startup.ConfigureServices` method to use Entity Framework and Identity services:</span></span>

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

<span data-ttu-id="d8bf4-112">在这种情况下，有两种在上面的代码中，我们尚未尚未迁移从 ASP.NET MVC 项目中引用的类型：`ApplicationDbContext`和`ApplicationUser`。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-112">At this point, there are two types referenced in the above code that we haven't yet migrated from the ASP.NET MVC project: `ApplicationDbContext` and `ApplicationUser`.</span></span> <span data-ttu-id="d8bf4-113">创建一个新*模型*文件夹中 ASP.NET Core 项目，并将两个类添加到它对应于这些类型。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-113">Create a new *Models* folder in the ASP.NET Core project, and add two classes to it corresponding to these types.</span></span> <span data-ttu-id="d8bf4-114">你将找到 ASP.NET MVC 的这些类中的版本 */Models/IdentityModels.cs*，但我们将使用每个已迁移的项目中的类的一个文件，因为它是更清晰。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-114">You will find the ASP.NET MVC versions of these classes in */Models/IdentityModels.cs*, but we will use one file per class in the migrated project since that's more clear.</span></span>

<span data-ttu-id="d8bf4-115">*ApplicationUser.cs*:</span><span class="sxs-lookup"><span data-stu-id="d8bf4-115">*ApplicationUser.cs*:</span></span>

```csharp
using Microsoft.AspNetCore.Identity.EntityFrameworkCore;

namespace NewMvcProject.Models
{
  public class ApplicationUser : IdentityUser
  {
  }
}
```

<span data-ttu-id="d8bf4-116">*ApplicationDbContext.cs*:</span><span class="sxs-lookup"><span data-stu-id="d8bf4-116">*ApplicationDbContext.cs*:</span></span>

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

<span data-ttu-id="d8bf4-117">ASP.NET Core MVC 初学者 Web 项目不包括多的自定义的用户，或`ApplicationDbContext`。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-117">The ASP.NET Core MVC Starter Web project doesn't include much customization of users, or the `ApplicationDbContext`.</span></span> <span data-ttu-id="d8bf4-118">当迁移实际应用程序时，你还需要迁移的所有自定义属性和方法的应用程序的用户和`DbContext`类，以及你的应用程序使用的任何其他模型类。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-118">When migrating a real app, you also need to migrate all of the custom properties and methods of your app's user and `DbContext` classes, as well as any other Model classes your app utilizes.</span></span> <span data-ttu-id="d8bf4-119">例如，如果你`DbContext`具有`DbSet<Album>`，你需要迁移`Album`类。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-119">For example, if your `DbContext` has a `DbSet<Album>`, you need to migrate the `Album` class.</span></span>

<span data-ttu-id="d8bf4-120">与就地情况下，这些文件*Startup.cs*文件可以进行编译，方法是更新其`using`语句：</span><span class="sxs-lookup"><span data-stu-id="d8bf4-120">With these files in place, the *Startup.cs* file can be made to compile by updating its `using` statements:</span></span>

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Identity;
using Microsoft.AspNetCore.Hosting;
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
```

<span data-ttu-id="d8bf4-121">我们的应用程序现在已准备好支持身份验证和标识服务。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-121">Our app is now ready to support authentication and Identity services.</span></span> <span data-ttu-id="d8bf4-122">它只需要具有向用户公开这些功能。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-122">It just needs to have these features exposed to users.</span></span>

## <a name="migrate-registration-and-login-logic"></a><span data-ttu-id="d8bf4-123">迁移注册和登录名逻辑</span><span class="sxs-lookup"><span data-stu-id="d8bf4-123">Migrate registration and login logic</span></span>

<span data-ttu-id="d8bf4-124">使用标识服务对应用程序配置和使用实体框架和 SQL Server 配置的数据访问，我们已准备好将支持注册和登录名添加到应用程序。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-124">With Identity services configured for the app and data access configured using Entity Framework and SQL Server, we're ready to add support for registration and login to the app.</span></span> <span data-ttu-id="d8bf4-125">回想一下，[前面的迁移过程](xref:migration/mvc#migrate-the-layout-file)我们注释掉对的引用 *_LoginPartial*中 *_Layout.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-125">Recall that [earlier in the migration process](xref:migration/mvc#migrate-the-layout-file) we commented out a reference to *_LoginPartial* in *_Layout.cshtml*.</span></span> <span data-ttu-id="d8bf4-126">现在，它是返回到该代码中，取消注释它，并在必要的控制器视图和视图，以支持登录功能将添加的时间。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-126">Now it's time to return to that code, uncomment it, and add in the necessary controllers and views to support login functionality.</span></span>

<span data-ttu-id="d8bf4-127">取消注释`@Html.Partial`中一行 *_Layout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="d8bf4-127">Uncomment the `@Html.Partial` line in *_Layout.cshtml*:</span></span>

```cshtml
      <li>@Html.ActionLink("Contact", "Contact", "Home")</li>
    </ul>
    @*@Html.Partial("_LoginPartial")*@
  </div>
</div>
```

<span data-ttu-id="d8bf4-128">现在，添加一个新的 Razor 视图调用 *_LoginPartial*到*视图/共享*文件夹：</span><span class="sxs-lookup"><span data-stu-id="d8bf4-128">Now, add a new Razor view called *_LoginPartial* to the *Views/Shared* folder:</span></span>

<span data-ttu-id="d8bf4-129">更新 *_LoginPartial.cshtml*替换为以下代码 （替换其内容的所有）：</span><span class="sxs-lookup"><span data-stu-id="d8bf4-129">Update *_LoginPartial.cshtml* with the following code (replace all of its contents):</span></span>

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

<span data-ttu-id="d8bf4-130">此时，你应能够刷新浏览器中的站点。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-130">At this point, you should be able to refresh the site in your browser.</span></span>

## <a name="summary"></a><span data-ttu-id="d8bf4-131">总结</span><span class="sxs-lookup"><span data-stu-id="d8bf4-131">Summary</span></span>

<span data-ttu-id="d8bf4-132">ASP.NET Core引入 ASP.NET 标识功能更改。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-132">ASP.NET Core introduces changes to the ASP.NET Identity features.</span></span> <span data-ttu-id="d8bf4-133">在本文中，你看到了如何将 ASP.NET 标识的身份验证和用户管理功能迁移到 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="d8bf4-133">In this article, you have seen how to migrate the authentication and user management features of ASP.NET Identity to ASP.NET Core.</span></span>
