---
title: ASP.NET Core 上的标识简介
author: rick-anderson
description: 将标识与 ASP.NET Core 应用配合使用。 包括设置密码要求（RequireDigit、RequiredLength、RequiredUniqueChars 等）。
ms.author: riande
ms.date: 01/24/2018
uid: security/authentication/identity
ms.openlocfilehash: c231a7619a4433ce004342ce68564e4c3892e702
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829297"
---
# <a name="introduction-to-identity-on-aspnet-core"></a><span data-ttu-id="a2bed-104">ASP.NET Core 上的标识简介</span><span class="sxs-lookup"><span data-stu-id="a2bed-104">Introduction to Identity on ASP.NET Core</span></span>

<span data-ttu-id="a2bed-105">通过[Pranav rastogi 撰写](https://github.com/rustd)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)，Jon Galloway [Erik Reitan](https://github.com/Erikre)，和[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="a2bed-105">By [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), Jon Galloway, [Erik Reitan](https://github.com/Erikre), and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="a2bed-106">ASP.NET Core 标识是一种用于向应用程序添加登录功能的成员身份系统。</span><span class="sxs-lookup"><span data-stu-id="a2bed-106">ASP.NET Core Identity is a membership system which allows you to add login functionality to your application.</span></span> <span data-ttu-id="a2bed-107">用户可以创建一个帐户，然后使用用户名和密码登录，也可以使用 Facebook、Google、Microsoft 帐户、Twitter 等外部登录提供程序。</span><span class="sxs-lookup"><span data-stu-id="a2bed-107">Users can create an account and login with a user name and password or they can use an external login provider such as Facebook, Google, Microsoft Account, Twitter or others.</span></span>

<span data-ttu-id="a2bed-108">可以将 ASP.NET Core 标识配置为使用 SQL Server 数据库来存储用户名、密码和配置文件数据。</span><span class="sxs-lookup"><span data-stu-id="a2bed-108">You can configure ASP.NET Core Identity to use a SQL Server database to store user names, passwords, and profile data.</span></span> <span data-ttu-id="a2bed-109">也可以使用你自己的持久存储，例如 Azure 表存储。</span><span class="sxs-lookup"><span data-stu-id="a2bed-109">Alternatively, you can use your own persistent store, for example, an Azure Table Storage.</span></span> <span data-ttu-id="a2bed-110">本文档包含的说明适用于 Visual Studio 和 CLI。</span><span class="sxs-lookup"><span data-stu-id="a2bed-110">This document contains instructions for Visual Studio and for using the CLI.</span></span>

[<span data-ttu-id="a2bed-111">查看或下载示例代码。</span><span class="sxs-lookup"><span data-stu-id="a2bed-111">View or download the sample code.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/identity/sample/src/ASPNETCore-IdentityDemoComplete/) [<span data-ttu-id="a2bed-112">（如何下载）</span><span class="sxs-lookup"><span data-stu-id="a2bed-112">(How to download)</span></span>](xref:tutorials/index#how-to-download-a-sample)

## <a name="overview-of-identity"></a><span data-ttu-id="a2bed-113">标识概述</span><span class="sxs-lookup"><span data-stu-id="a2bed-113">Overview of Identity</span></span>

<span data-ttu-id="a2bed-114">本主题介绍如何使用 ASP.NET Core 标识来添加用于注册、登录和注销用户的功能。</span><span class="sxs-lookup"><span data-stu-id="a2bed-114">In this topic, you'll learn how to use ASP.NET Core Identity to add functionality to register, log in, and log out a user.</span></span> <span data-ttu-id="a2bed-115">若要详细了解如何使用 ASP.NET Core 标识来创建应用，请参阅本文末尾的“后续步骤”部分。</span><span class="sxs-lookup"><span data-stu-id="a2bed-115">For more detailed instructions about creating apps using ASP.NET Core Identity, see the Next Steps section at the end of this article.</span></span>

1. <span data-ttu-id="a2bed-116">使用单个用户帐户创建一个 ASP.NET Core Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="a2bed-116">Create an ASP.NET Core Web Application project with Individual User Accounts.</span></span>

   # <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="a2bed-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a2bed-117">Visual Studio</span></span>](#tab/visual-studio)

   <span data-ttu-id="a2bed-118">在 Visual Studio 中，选择**文件** > **新建** > **项目**。</span><span class="sxs-lookup"><span data-stu-id="a2bed-118">In Visual Studio, select **File** > **New** > **Project**.</span></span> <span data-ttu-id="a2bed-119">选择**ASP.NET Core Web 应用程序**单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="a2bed-119">Select **ASP.NET Core Web Application** and click **OK**.</span></span>

   ![“新建项目”对话框](identity/_static/01-new-project.png)

   <span data-ttu-id="a2bed-121">选择 ASP.NET Core **Web 应用程序 （模型-视图-控制器）** asp.NET Core 2.x，然后选择**更改身份验证**。</span><span class="sxs-lookup"><span data-stu-id="a2bed-121">Select an ASP.NET Core **Web Application (Model-View-Controller)** for ASP.NET Core 2.x, then select **Change Authentication**.</span></span>

   ![“新建项目”对话框](identity/_static/02-new-project.png)

   <span data-ttu-id="a2bed-123">出现一个对话框，产品/服务身份验证选项。</span><span class="sxs-lookup"><span data-stu-id="a2bed-123">A dialog appears offering authentication choices.</span></span> <span data-ttu-id="a2bed-124">选择**单个用户帐户**然后单击**确定**以返回到上一个对话框。</span><span class="sxs-lookup"><span data-stu-id="a2bed-124">Select **Individual User Accounts** and click **OK** to return to the previous dialog.</span></span>

   ![“新建项目”对话框](identity/_static/03-new-project-auth.png)

   <span data-ttu-id="a2bed-126">选择**单个用户帐户**指示 Visual Studio 创建模型、 Viewmodel、 视图、 控制器和其他资产所需的身份验证作为项目模板的一部分。</span><span class="sxs-lookup"><span data-stu-id="a2bed-126">Selecting **Individual User Accounts** directs Visual Studio to create Models, ViewModels, Views, Controllers, and other assets required for authentication as part of the project template.</span></span>

   # <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="a2bed-127">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="a2bed-127">.NET Core CLI</span></span>](#tab/netcore-cli)

   <span data-ttu-id="a2bed-128">如果使用.NET Core CLI，创建新的项目使用`dotnet new mvc --auth Individual`。</span><span class="sxs-lookup"><span data-stu-id="a2bed-128">If using the .NET Core CLI, create the new project using `dotnet new mvc --auth Individual`.</span></span> <span data-ttu-id="a2bed-129">此命令创建具有相同标识模板代码 Visual Studio 将创建一个新的项目。</span><span class="sxs-lookup"><span data-stu-id="a2bed-129">This command creates a new project with the same Identity template code Visual Studio creates.</span></span>

   <span data-ttu-id="a2bed-130">创建的项目包含`Microsoft.AspNetCore.Identity.EntityFrameworkCore`包，仍然存在的标识数据和 SQL Server 使用的架构[Entity Framework Core](https://docs.microsoft.com/ef/)。</span><span class="sxs-lookup"><span data-stu-id="a2bed-130">The created project contains the `Microsoft.AspNetCore.Identity.EntityFrameworkCore` package, which persists the Identity data and schema to SQL Server using [Entity Framework Core](https://docs.microsoft.com/ef/).</span></span>

   ---

2. <span data-ttu-id="a2bed-131">配置标识服务，并添加中间件中的`Startup`。</span><span class="sxs-lookup"><span data-stu-id="a2bed-131">Configure Identity services and add middleware in `Startup`.</span></span>

   <span data-ttu-id="a2bed-132">标识服务添加到中的应用程序`ConfigureServices`中的方法`Startup`类：</span><span class="sxs-lookup"><span data-stu-id="a2bed-132">The Identity services are added to the application in the `ConfigureServices` method in the `Startup` class:</span></span>

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="a2bed-133">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="a2bed-133">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]

   <span data-ttu-id="a2bed-134">这些服务都提供给应用程序通过[依赖关系注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="a2bed-134">These services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="a2bed-135">通过调用情况下，启用应用程序的身份标识`UseAuthentication`在`Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="a2bed-135">Identity is enabled for the application by calling `UseAuthentication` in the `Configure` method.</span></span> <span data-ttu-id="a2bed-136">`UseAuthentication` 添加了身份验证[中间件](xref:fundamentals/middleware/index)到请求管道。</span><span class="sxs-lookup"><span data-stu-id="a2bed-136">`UseAuthentication` adds authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configure&highlight=17)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="a2bed-137">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="a2bed-137">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,13-33)]

   <span data-ttu-id="a2bed-138">这些服务都提供给应用程序通过[依赖关系注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="a2bed-138">These services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="a2bed-139">通过调用情况下，启用应用程序的身份标识`UseIdentity`在`Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="a2bed-139">Identity is enabled for the application by calling `UseIdentity` in the `Configure` method.</span></span> <span data-ttu-id="a2bed-140">`UseIdentity` 添加了基于 cookie 的身份验证[中间件](xref:fundamentals/middleware/index)到请求管道。</span><span class="sxs-lookup"><span data-stu-id="a2bed-140">`UseIdentity` adds cookie-based authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configure&highlight=21)]

   ---

   <span data-ttu-id="a2bed-141">有关应用程序启动过程的详细信息，请参阅[应用程序启动](xref:fundamentals/startup)。</span><span class="sxs-lookup"><span data-stu-id="a2bed-141">For more information about the application start up process, see [Application Startup](xref:fundamentals/startup).</span></span>

3. <span data-ttu-id="a2bed-142">创建一个用户。</span><span class="sxs-lookup"><span data-stu-id="a2bed-142">Create a user.</span></span>

   <span data-ttu-id="a2bed-143">启动应用程序，然后单击**注册**链接。</span><span class="sxs-lookup"><span data-stu-id="a2bed-143">Launch the application and then click on the **Register** link.</span></span>

   <span data-ttu-id="a2bed-144">如果这是首次在执行此操作，您可能需要运行迁移。</span><span class="sxs-lookup"><span data-stu-id="a2bed-144">If this is the first time you're performing this action, you may be required to run migrations.</span></span> <span data-ttu-id="a2bed-145">应用程序会提示您**应用迁移**。</span><span class="sxs-lookup"><span data-stu-id="a2bed-145">The application prompts you to **Apply Migrations**.</span></span> <span data-ttu-id="a2bed-146">如果需要请刷新页面。</span><span class="sxs-lookup"><span data-stu-id="a2bed-146">Refresh the page if needed.</span></span>

   ![将应用迁移网页](identity/_static/apply-migrations.png)

   <span data-ttu-id="a2bed-148">也可使用内存中数据库来测试如何在没有持久数据库的情况下将 ASP.NET Core 标识与应用配合使用。</span><span class="sxs-lookup"><span data-stu-id="a2bed-148">Alternately, you can test using ASP.NET Core Identity with your app without a persistent database by using an in-memory database.</span></span> <span data-ttu-id="a2bed-149">若要使用内存中数据库，请将 `Microsoft.EntityFrameworkCore.InMemory` 包添加到应用，然后在 `ConfigureServices` 中修改应用对 `AddDbContext` 的调用，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a2bed-149">To use an in-memory database, add the `Microsoft.EntityFrameworkCore.InMemory` package to your app and modify your app's call to `AddDbContext` in `ConfigureServices` as follows:</span></span>

   ```csharp
   services.AddDbContext<ApplicationDbContext>(options =>
       options.UseInMemoryDatabase(Guid.NewGuid().ToString()));
   ```

   <span data-ttu-id="a2bed-150">当用户单击**注册**链接，链接`Register`上调用操作`AccountController`。</span><span class="sxs-lookup"><span data-stu-id="a2bed-150">When the user clicks the **Register** link, the `Register` action is invoked on `AccountController`.</span></span> <span data-ttu-id="a2bed-151">`Register`操作将创建用户，通过调用`CreateAsync`上`_userManager`对象 (提供给`AccountController`通过依赖关系注入):</span><span class="sxs-lookup"><span data-stu-id="a2bed-151">The `Register` action creates the user by calling `CreateAsync` on the `_userManager` object (provided to `AccountController` by dependency injection):</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_register&highlight=11)]

   <span data-ttu-id="a2bed-152">如果已成功创建用户，用户记录通过调用`_signInManager.SignInAsync`。</span><span class="sxs-lookup"><span data-stu-id="a2bed-152">If the user was created successfully, the user is logged in by the call to `_signInManager.SignInAsync`.</span></span>

   <span data-ttu-id="a2bed-153">**注意：** 请参阅[帐户确认](xref:security/authentication/accconfirm#prevent-login-at-registration)有关步骤，以防止在登记时立即登录。</span><span class="sxs-lookup"><span data-stu-id="a2bed-153">**Note:** See [account confirmation](xref:security/authentication/accconfirm#prevent-login-at-registration) for steps to prevent immediate login at registration.</span></span>

4. <span data-ttu-id="a2bed-154">登录。</span><span class="sxs-lookup"><span data-stu-id="a2bed-154">Log in.</span></span>

   <span data-ttu-id="a2bed-155">用户可以通过单击登录**登录**链接顶部的站点，或可能的登录页导航它们，如果用户尝试访问需要授权的站点的一部分。</span><span class="sxs-lookup"><span data-stu-id="a2bed-155">Users can sign in by clicking the **Log in** link at the top of the site, or they may be navigated to the Login page if they attempt to access a part of the site that requires authorization.</span></span> <span data-ttu-id="a2bed-156">当用户提交窗体上的登录页中， `AccountController` `Login`调用操作。</span><span class="sxs-lookup"><span data-stu-id="a2bed-156">When the user submits the form on the Login page, the `AccountController` `Login` action is called.</span></span>

   <span data-ttu-id="a2bed-157">`Login`操作调用`PasswordSignInAsync`上`_signInManager`对象 (提供给`AccountController`通过依赖关系注入)。</span><span class="sxs-lookup"><span data-stu-id="a2bed-157">The `Login` action calls `PasswordSignInAsync` on the `_signInManager` object (provided to `AccountController` by dependency injection).</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_login&highlight=13-14)]

   <span data-ttu-id="a2bed-158">基`Controller`类公开`User`，可以从控制器方法访问的属性。</span><span class="sxs-lookup"><span data-stu-id="a2bed-158">The base `Controller` class exposes a `User` property that you can access from controller methods.</span></span> <span data-ttu-id="a2bed-159">例如，可以枚举`User.Claims`和做出授权决定。</span><span class="sxs-lookup"><span data-stu-id="a2bed-159">For instance, you can enumerate `User.Claims` and make authorization decisions.</span></span> <span data-ttu-id="a2bed-160">有关详细信息，请参阅[授权](xref:security/authorization/index)。</span><span class="sxs-lookup"><span data-stu-id="a2bed-160">For more information, see [Authorization](xref:security/authorization/index).</span></span>

5. <span data-ttu-id="a2bed-161">注销。</span><span class="sxs-lookup"><span data-stu-id="a2bed-161">Log out.</span></span>

   <span data-ttu-id="a2bed-162">单击**注销**链接调用`LogOut`操作。</span><span class="sxs-lookup"><span data-stu-id="a2bed-162">Clicking the **Log out** link calls the `LogOut` action.</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_logout&highlight=7)]

   <span data-ttu-id="a2bed-163">前面的代码调用上面`_signInManager.SignOutAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="a2bed-163">The preceding code above calls the `_signInManager.SignOutAsync` method.</span></span> <span data-ttu-id="a2bed-164">`SignOutAsync`方法将清除用户的声明存储在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="a2bed-164">The `SignOutAsync` method clears the user's claims stored in a cookie.</span></span>

<a name="pw"></a>
6. <span data-ttu-id="a2bed-165">配置。</span><span class="sxs-lookup"><span data-stu-id="a2bed-165">Configuration.</span></span>

   <span data-ttu-id="a2bed-166">标识具有一些可以在应用程序的 startup 类中重写的默认行为。</span><span class="sxs-lookup"><span data-stu-id="a2bed-166">Identity has some default behaviors that can be overridden in the app's startup class.</span></span> <span data-ttu-id="a2bed-167">`IdentityOptions` 无需使用的默认行为时，配置。</span><span class="sxs-lookup"><span data-stu-id="a2bed-167">`IdentityOptions` don't need to be configured when using the default behaviors.</span></span> <span data-ttu-id="a2bed-168">下面的代码设置多个密码强度选项：</span><span class="sxs-lookup"><span data-stu-id="a2bed-168">The following code sets several password strength options:</span></span>

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="a2bed-169">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="a2bed-169">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="a2bed-170">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="a2bed-170">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=13-33)]

   ---

   <span data-ttu-id="a2bed-171">有关如何配置标识的详细信息，请参阅[配置标识](xref:security/authentication/identity-configuration)。</span><span class="sxs-lookup"><span data-stu-id="a2bed-171">For more information about how to configure Identity, see [Configure Identity](xref:security/authentication/identity-configuration).</span></span>

   <span data-ttu-id="a2bed-172">您还可以配置的数据类型的主键，请参阅[配置标识为主键数据类型](xref:security/authentication/identity-primary-key-configuration)。</span><span class="sxs-lookup"><span data-stu-id="a2bed-172">You also can configure the data type of the primary key, see [Configure Identity primary keys data type](xref:security/authentication/identity-primary-key-configuration).</span></span>

7. <span data-ttu-id="a2bed-173">查看数据库。</span><span class="sxs-lookup"><span data-stu-id="a2bed-173">View the database.</span></span>

   <span data-ttu-id="a2bed-174">如果您的应用程序使用 SQL Server 数据库 （默认和 Visual Studio 用户的 Windows 上），则可以查看数据库中创建的应用。</span><span class="sxs-lookup"><span data-stu-id="a2bed-174">If your app is using a SQL Server database (the default on Windows and for Visual Studio users), you can view the database the app created.</span></span> <span data-ttu-id="a2bed-175">可以使用**SQL Server Management Studio**。</span><span class="sxs-lookup"><span data-stu-id="a2bed-175">You can use **SQL Server Management Studio**.</span></span> <span data-ttu-id="a2bed-176">或者，从 Visual Studio 中，选择**视图** > **SQL Server 对象资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="a2bed-176">Alternatively, from Visual Studio, select **View** > **SQL Server Object Explorer**.</span></span> <span data-ttu-id="a2bed-177">连接到 **(localdb) \MSSQLLocalDB**。</span><span class="sxs-lookup"><span data-stu-id="a2bed-177">Connect to **(localdb)\MSSQLLocalDB**.</span></span> <span data-ttu-id="a2bed-178">其名称与数据库`aspnet-<name of your project>-<guid>`显示。</span><span class="sxs-lookup"><span data-stu-id="a2bed-178">The database with a name matching `aspnet-<name of your project>-<guid>` is displayed.</span></span>

   ![在 AspNetUsers 表中数据库的上下文菜单](identity/_static/04-db.png)

   <span data-ttu-id="a2bed-180">展开数据库并将其**表**，然后右键单击**dbo。AspNetUsers**表，然后选择**查看数据**。</span><span class="sxs-lookup"><span data-stu-id="a2bed-180">Expand the database and its **Tables**, then right-click the **dbo.AspNetUsers** table and select **View Data**.</span></span>

8. <span data-ttu-id="a2bed-181">验证标识起作用。</span><span class="sxs-lookup"><span data-stu-id="a2bed-181">Verify Identity works</span></span>

    <span data-ttu-id="a2bed-182">默认值*ASP.NET Core Web 应用程序*项目模板，用户可以访问应用程序中的任何操作，而无到登录名。</span><span class="sxs-lookup"><span data-stu-id="a2bed-182">The default *ASP.NET Core Web Application* project template allows users to access any action in the application without having to login.</span></span> <span data-ttu-id="a2bed-183">若要验证 ASP.NET 标识是否正常工作，添加`[Authorize]`归于`About`操作的`Home`控制器。</span><span class="sxs-lookup"><span data-stu-id="a2bed-183">To verify that ASP.NET Identity works, add an`[Authorize]` attribute to the `About` action of the `Home` Controller.</span></span>

    ```csharp
    [Authorize]
    public IActionResult About()
    {
        ViewData["Message"] = "Your application description page.";
        return View();
    }
    ```

    # <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="a2bed-184">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a2bed-184">Visual Studio</span></span>](#tab/visual-studio)

    <span data-ttu-id="a2bed-185">项目使用运行**Ctrl** + **F5** ，并导航到**有关**页。</span><span class="sxs-lookup"><span data-stu-id="a2bed-185">Run the project using **Ctrl** + **F5** and navigate to the **About** page.</span></span> <span data-ttu-id="a2bed-186">仅经过身份验证的用户可以访问**有关**现在，网页，使 ASP.NET 将你重定向到登录页登录或注册。</span><span class="sxs-lookup"><span data-stu-id="a2bed-186">Only authenticated users may access the **About** page now, so ASP.NET redirects you to the login page to login or register.</span></span>

    # <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="a2bed-187">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="a2bed-187">.NET Core CLI</span></span>](#tab/netcore-cli)

    <span data-ttu-id="a2bed-188">打开命令窗口并导航到项目的根目录包含`.csproj`文件。</span><span class="sxs-lookup"><span data-stu-id="a2bed-188">Open a command window and navigate to the project's root directory containing the `.csproj` file.</span></span> <span data-ttu-id="a2bed-189">运行[dotnet 运行](/dotnet/core/tools/dotnet-run)命令以运行该应用程序：</span><span class="sxs-lookup"><span data-stu-id="a2bed-189">Run the [dotnet run](/dotnet/core/tools/dotnet-run) command to run the app:</span></span>

    ```csharp
    dotnet run 
    ```

    <span data-ttu-id="a2bed-190">浏览从输出中指定的 URL [dotnet 运行](/dotnet/core/tools/dotnet-run)命令。</span><span class="sxs-lookup"><span data-stu-id="a2bed-190">Browse the URL specified in the output from the [dotnet run](/dotnet/core/tools/dotnet-run) command.</span></span> <span data-ttu-id="a2bed-191">该 URL 应指向`localhost`与生成的端口号。</span><span class="sxs-lookup"><span data-stu-id="a2bed-191">The URL should point to `localhost` with a generated port number.</span></span> <span data-ttu-id="a2bed-192">导航到**有关**页。</span><span class="sxs-lookup"><span data-stu-id="a2bed-192">Navigate to the **About** page.</span></span> <span data-ttu-id="a2bed-193">仅经过身份验证的用户可以访问**有关**现在，网页，使 ASP.NET 将你重定向到登录页登录或注册。</span><span class="sxs-lookup"><span data-stu-id="a2bed-193">Only authenticated users may access the **About** page now, so ASP.NET redirects you to the login page to login or register.</span></span>

    ---

## <a name="identity-components"></a><span data-ttu-id="a2bed-194">标识组件</span><span class="sxs-lookup"><span data-stu-id="a2bed-194">Identity Components</span></span>

<span data-ttu-id="a2bed-195">标识系统的主引用程序集是 `Microsoft.AspNetCore.Identity`。</span><span class="sxs-lookup"><span data-stu-id="a2bed-195">The primary reference assembly for the Identity system is `Microsoft.AspNetCore.Identity`.</span></span> <span data-ttu-id="a2bed-196">此包包含 ASP.NET Core 标识的核心接口集，是 `Microsoft.AspNetCore.Identity.EntityFrameworkCore` 提供的。</span><span class="sxs-lookup"><span data-stu-id="a2bed-196">This package contains the core set of interfaces for ASP.NET Core Identity, and is included by `Microsoft.AspNetCore.Identity.EntityFrameworkCore`.</span></span>

<span data-ttu-id="a2bed-197">这些依赖关系需要 ASP.NET Core 应用程序中使用的标识系统：</span><span class="sxs-lookup"><span data-stu-id="a2bed-197">These dependencies are needed to use the Identity system in ASP.NET Core applications:</span></span>

* <span data-ttu-id="a2bed-198">`Microsoft.AspNetCore.Identity.EntityFrameworkCore` - 包含将标识与 Entity Framework Core 配合使用所需的类型。</span><span class="sxs-lookup"><span data-stu-id="a2bed-198">`Microsoft.AspNetCore.Identity.EntityFrameworkCore` - Contains the required types to use Identity with Entity Framework Core.</span></span>

* <span data-ttu-id="a2bed-199">`Microsoft.EntityFrameworkCore.SqlServer` -Entity Framework Core 是 Microsoft 的建议的数据访问技术的 SQL Server 等关系数据库。</span><span class="sxs-lookup"><span data-stu-id="a2bed-199">`Microsoft.EntityFrameworkCore.SqlServer` - Entity Framework Core is Microsoft's recommended data access technology for relational databases like SQL Server.</span></span> <span data-ttu-id="a2bed-200">对于测试，可以使用`Microsoft.EntityFrameworkCore.InMemory`。</span><span class="sxs-lookup"><span data-stu-id="a2bed-200">For testing, you can use `Microsoft.EntityFrameworkCore.InMemory`.</span></span>

* <span data-ttu-id="a2bed-201">`Microsoft.AspNetCore.Authentication.Cookies` -允许应用程序使用基于 cookie 的身份验证的中间件。</span><span class="sxs-lookup"><span data-stu-id="a2bed-201">`Microsoft.AspNetCore.Authentication.Cookies` - Middleware that enables an app to use cookie-based authentication.</span></span>

## <a name="migrating-to-aspnet-core-identity"></a><span data-ttu-id="a2bed-202">迁移到 ASP.NET Core 标识</span><span class="sxs-lookup"><span data-stu-id="a2bed-202">Migrating to ASP.NET Core Identity</span></span>

<span data-ttu-id="a2bed-203">有关其他信息和指南迁移现有的标识存储，请参阅[迁移身份验证和标识](xref:migration/identity)。</span><span class="sxs-lookup"><span data-stu-id="a2bed-203">For additional information and guidance on migrating your existing Identity store see [Migrate Authentication and Identity](xref:migration/identity).</span></span>

## <a name="setting-password-strength"></a><span data-ttu-id="a2bed-204">设置密码强度</span><span class="sxs-lookup"><span data-stu-id="a2bed-204">Setting password strength</span></span>

<span data-ttu-id="a2bed-205">请参阅[配置](#pw)有关设置的最小密码要求的示例。</span><span class="sxs-lookup"><span data-stu-id="a2bed-205">See [Configuration](#pw) for a sample that sets the minimum password requirements.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2bed-206">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a2bed-206">Next Steps</span></span>

* [<span data-ttu-id="a2bed-207">迁移身份验证和标识</span><span class="sxs-lookup"><span data-stu-id="a2bed-207">Migrate Authentication and Identity</span></span>](xref:migration/identity)
* [<span data-ttu-id="a2bed-208">帐户确认和密码恢复</span><span class="sxs-lookup"><span data-stu-id="a2bed-208">Account Confirmation and Password Recovery</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="a2bed-209">使用 SMS 设置双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="a2bed-209">Two-factor authentication with SMS</span></span>](xref:security/authentication/2fa)
* [<span data-ttu-id="a2bed-210">Facebook、 Google 和外部提供程序身份验证</span><span class="sxs-lookup"><span data-stu-id="a2bed-210">Facebook, Google, and external provider authentication</span></span>](xref:security/authentication/social/index)
