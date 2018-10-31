---
title: ASP.NET Core 上的标识简介
author: rick-anderson
description: 将标识与 ASP.NET Core 应用配合使用。 了解如何设置密码要求 （RequireDigit、 RequiredLength、 RequiredUniqueChars，和的详细信息）。
ms.author: riande
ms.date: 08/08/2018
uid: security/authentication/identity
ms.openlocfilehash: 4e162edc8fb63457c8690692685f344dccdfc659
ms.sourcegitcommit: 4a6bbe84db24c2f3dd2de065de418fde952c8d40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2018
ms.locfileid: "50252924"
---
# <a name="introduction-to-identity-on-aspnet-core"></a><span data-ttu-id="51f4e-104">ASP.NET Core 上的标识简介</span><span class="sxs-lookup"><span data-stu-id="51f4e-104">Introduction to Identity on ASP.NET Core</span></span>

<span data-ttu-id="51f4e-105">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="51f4e-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="51f4e-106">ASP.NET Core 标识是一个成员身份系统，将登录功能添加到 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="51f4e-106">ASP.NET Core Identity is a membership system that adds login functionality to ASP.NET Core apps.</span></span> <span data-ttu-id="51f4e-107">用户可以标识中存储的登录信息创建一个帐户，或它们可以使用外部登录提供程序。</span><span class="sxs-lookup"><span data-stu-id="51f4e-107">Users can create an account with the login information stored in Identity or they can use an external login provider.</span></span> <span data-ttu-id="51f4e-108">受支持的外部登录提供程序包括[Facebook、 Google、 Microsoft 帐户和 Twitter](xref:security/authentication/social/index)。</span><span class="sxs-lookup"><span data-stu-id="51f4e-108">Supported external login providers include [Facebook, Google, Microsoft Account, and Twitter](xref:security/authentication/social/index).</span></span>

<span data-ttu-id="51f4e-109">可以使用 SQL Server 数据库来存储用户名、 密码和配置文件数据配置标识。</span><span class="sxs-lookup"><span data-stu-id="51f4e-109">Identity can be configured using a SQL Server database to store user names, passwords, and profile data.</span></span> <span data-ttu-id="51f4e-110">或者，另一个的持久存储区可用，例如，Azure 表存储。</span><span class="sxs-lookup"><span data-stu-id="51f4e-110">Alternatively, another persistent store can be used, for example, Azure Table Storage.</span></span>

<span data-ttu-id="51f4e-111">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/identity/sample/src/ASPNETCore-IdentityDemoComplete/)([如何下载)](xref:index#how-to-download-a-sample))。</span><span class="sxs-lookup"><span data-stu-id="51f4e-111">[View or download the sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/identity/sample/src/ASPNETCore-IdentityDemoComplete/) ([how to download)](xref:index#how-to-download-a-sample)).</span></span>

<span data-ttu-id="51f4e-112">在本主题中，将了解如何使用标识来注册、 登录和注销用户。</span><span class="sxs-lookup"><span data-stu-id="51f4e-112">In this topic, you learn how to use Identity to register, log in, and log out a user.</span></span> <span data-ttu-id="51f4e-113">有关创建使用标识的应用程序的更多详细说明，请参阅本文末尾的后续步骤部分。</span><span class="sxs-lookup"><span data-stu-id="51f4e-113">For more detailed instructions about creating apps that use Identity, see the Next Steps section at the end of this article.</span></span>

::: moniker range=">= aspnetcore-2.1"

<a name="adi"></a>
## <a name="adddefaultidentity-and-addidentity"></a><span data-ttu-id="51f4e-114">AddDefaultIdentity 和 AddIdentity</span><span class="sxs-lookup"><span data-stu-id="51f4e-114">AddDefaultIdentity and AddIdentity</span></span>

<span data-ttu-id="51f4e-115">[AddDefaultIdentity](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionuiextensions.adddefaultidentity?view=aspnetcore-2.1#Microsoft_Extensions_DependencyInjection_IdentityServiceCollectionUIExtensions_AddDefaultIdentity__1_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Identity_IdentityOptions__) ASP 中引入了。Core 2.1。</span><span class="sxs-lookup"><span data-stu-id="51f4e-115">[AddDefaultIdentity](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionuiextensions.adddefaultidentity?view=aspnetcore-2.1#Microsoft_Extensions_DependencyInjection_IdentityServiceCollectionUIExtensions_AddDefaultIdentity__1_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Identity_IdentityOptions__) was introduced in ASP.Core 2.1.</span></span> <span data-ttu-id="51f4e-116">调用`AddDefaultIdentity`类似于调用以下：</span><span class="sxs-lookup"><span data-stu-id="51f4e-116">Calling `AddDefaultIdentity` is similar to calling the following:</span></span>

* [<span data-ttu-id="51f4e-117">AddIdentity</span><span class="sxs-lookup"><span data-stu-id="51f4e-117">AddIdentity</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.addidentity?view=aspnetcore-2.1#Microsoft_Extensions_DependencyInjection_IdentityServiceCollectionExtensions_AddIdentity__2_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Identity_IdentityOptions__)
* [<span data-ttu-id="51f4e-118">AddDefaultUI</span><span class="sxs-lookup"><span data-stu-id="51f4e-118">AddDefaultUI</span></span>](/dotnet/api/microsoft.aspnetcore.identity.identitybuilderuiextensions.adddefaultui?view=aspnetcore-2.1#Microsoft_AspNetCore_Identity_IdentityBuilderUIExtensions_AddDefaultUI_Microsoft_AspNetCore_Identity_IdentityBuilder_)
* [<span data-ttu-id="51f4e-119">AddDefaultTokenProviders</span><span class="sxs-lookup"><span data-stu-id="51f4e-119">AddDefaultTokenProviders</span></span>](/dotnet/api/microsoft.aspnetcore.identity.identitybuilderextensions.adddefaulttokenproviders?view=aspnetcore-2.1#Microsoft_AspNetCore_Identity_IdentityBuilderExtensions_AddDefaultTokenProviders_Microsoft_AspNetCore_Identity_IdentityBuilder_)

<span data-ttu-id="51f4e-120">请参阅[AddDefaultIdentity 源](https://github.com/aspnet/Identity/blob/2634637fd535b229762b5e4a49cdd128f4d8f12e/src/UI/IdentityServiceCollectionUIExtensions.cs#L47-L64)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="51f4e-120">See [AddDefaultIdentity source](https://github.com/aspnet/Identity/blob/2634637fd535b229762b5e4a49cdd128f4d8f12e/src/UI/IdentityServiceCollectionUIExtensions.cs#L47-L64) for more information.</span></span>

::: moniker-end

## <a name="create-a-web-app-with-authentication"></a><span data-ttu-id="51f4e-121">使用身份验证创建的 Web 应用</span><span class="sxs-lookup"><span data-stu-id="51f4e-121">Create a Web app with authentication</span></span>

<span data-ttu-id="51f4e-122">使用单个用户帐户创建一个 ASP.NET Core Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="51f4e-122">Create an ASP.NET Core Web Application project with Individual User Accounts.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="51f4e-123">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51f4e-123">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="51f4e-124">选择“文件” > “新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="51f4e-124">Select **File** > **New** > **Project**.</span></span>
* <span data-ttu-id="51f4e-125">选择“ASP.NET Core Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="51f4e-125">Select **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="51f4e-126">将项目命名**WebApp1**具有项目下载相同的命名空间。</span><span class="sxs-lookup"><span data-stu-id="51f4e-126">Name the project **WebApp1** to have the same namespace as the project download.</span></span> <span data-ttu-id="51f4e-127">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="51f4e-127">Click **OK**.</span></span>
* <span data-ttu-id="51f4e-128">选择 ASP.NET Core **Web 应用程序**ASP.NET Core 2.1，然后选择**更改身份验证**。</span><span class="sxs-lookup"><span data-stu-id="51f4e-128">Select an ASP.NET Core **Web Application** for ASP.NET Core 2.1, then select **Change Authentication**.</span></span>
* <span data-ttu-id="51f4e-129">选择**单个用户帐户**然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="51f4e-129">Select **Individual User Accounts** and click **OK**.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="51f4e-130">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="51f4e-130">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet new webapp --auth Individual -o WebApp1
```

---

<span data-ttu-id="51f4e-131">生成的项目提供了[ASP.NET Core 标识](xref:security/authentication/identity)作为[Razor 类库](xref:razor-pages/ui-class)。</span><span class="sxs-lookup"><span data-stu-id="51f4e-131">The generated project provides [ASP.NET Core Identity](xref:security/authentication/identity) as a [Razor Class Library](xref:razor-pages/ui-class).</span></span>

### <a name="test-register-and-login"></a><span data-ttu-id="51f4e-132">测试注册和登录名</span><span class="sxs-lookup"><span data-stu-id="51f4e-132">Test Register and Login</span></span>

<span data-ttu-id="51f4e-133">运行应用并注册用户。</span><span class="sxs-lookup"><span data-stu-id="51f4e-133">Run the app and register a user.</span></span> <span data-ttu-id="51f4e-134">具体取决于你的屏幕大小，可能需要选择导航切换按钮以查看**注册**并**登录名**链接。</span><span class="sxs-lookup"><span data-stu-id="51f4e-134">Depending on your screen size, you might need to select the navigation toggle button to see the **Register** and **Login** links.</span></span>

![切换导航栏按钮](identity/_static/navToggle.png)

[!INCLUDE[](~/includes/view-identity-db.md)]

<a name="pw"></a>
### <a name="configure-identity-services"></a><span data-ttu-id="51f4e-136">配置标识服务</span><span class="sxs-lookup"><span data-stu-id="51f4e-136">Configure Identity services</span></span>

<span data-ttu-id="51f4e-137">在添加服务`ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="51f4e-137">Services are added in `ConfigureServices`.</span></span> <span data-ttu-id="51f4e-138">典型模式是调用所有 `Add{Service}` 方法，然后调用所有 `services.Configure{Service}` 方法。</span><span class="sxs-lookup"><span data-stu-id="51f4e-138">The typical pattern is to call all the `Add{Service}` methods, and then call all the `services.Configure{Service}` methods.</span></span> <span data-ttu-id="51f4e-139">下面的代码不包括生成的模板`CookiePolicyOptions`:</span><span class="sxs-lookup"><span data-stu-id="51f4e-139">The following code doesn't include the template generated `CookiePolicyOptions`:</span></span>

::: moniker range=">= aspnetcore-2.1"

   [!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/Startup.cs?name=snippet_configureservices)]

<span data-ttu-id="51f4e-140">上述代码使用默认的选项值配置标识。</span><span class="sxs-lookup"><span data-stu-id="51f4e-140">The preceding code configures Identity with default option values.</span></span> <span data-ttu-id="51f4e-141">服务可用于通过应用[依赖关系注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="51f4e-141">Services are made available to the app through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="51f4e-142">标识启用通过调用[UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_)。</span><span class="sxs-lookup"><span data-stu-id="51f4e-142">Identity is enabled by calling [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_).</span></span> <span data-ttu-id="51f4e-143">`UseAuthentication` 添加了身份验证[中间件](xref:fundamentals/middleware/index)到请求管道。</span><span class="sxs-lookup"><span data-stu-id="51f4e-143">`UseAuthentication` adds authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/Startup.cs?name=snippet_configure&highlight=18)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]

   <span data-ttu-id="51f4e-144">服务都提供给应用程序通过[依赖关系注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="51f4e-144">Services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="51f4e-145">通过调用情况下，启用应用程序的身份标识`UseAuthentication`在`Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="51f4e-145">Identity is enabled for the application by calling `UseAuthentication` in the `Configure` method.</span></span> <span data-ttu-id="51f4e-146">`UseAuthentication` 添加了身份验证[中间件](xref:fundamentals/middleware/index)到请求管道。</span><span class="sxs-lookup"><span data-stu-id="51f4e-146">`UseAuthentication` adds authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configure&highlight=17)]

::: moniker-end

::: moniker range="= aspnetcore-1.1"

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,13-33)]

   <span data-ttu-id="51f4e-147">这些服务都提供给应用程序通过[依赖关系注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="51f4e-147">These services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="51f4e-148">通过调用情况下，启用应用程序的身份标识`UseIdentity`在`Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="51f4e-148">Identity is enabled for the application by calling `UseIdentity` in the `Configure` method.</span></span> <span data-ttu-id="51f4e-149">`UseIdentity` 添加了基于 cookie 的身份验证[中间件](xref:fundamentals/middleware/index)到请求管道。</span><span class="sxs-lookup"><span data-stu-id="51f4e-149">`UseIdentity` adds cookie-based authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configure&highlight=21)]

::: moniker-end

<span data-ttu-id="51f4e-150">有关详细信息，请参阅[IdentityOptions 类](/dotnet/api/microsoft.aspnetcore.identity.identityoptions)并[应用程序启动](xref:fundamentals/startup)。</span><span class="sxs-lookup"><span data-stu-id="51f4e-150">For more information, see the [IdentityOptions Class](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) and [Application Startup](xref:fundamentals/startup).</span></span>

## <a name="scaffold-register-login-and-logout"></a><span data-ttu-id="51f4e-151">基架注册、 登录和注销</span><span class="sxs-lookup"><span data-stu-id="51f4e-151">Scaffold Register, Login, and LogOut</span></span>

<span data-ttu-id="51f4e-152">请按照[创建标识为具有授权的 Razor 项目基架](xref:security/authentication/scaffold-identity#scaffold-identity-into-a-razor-project-with-authorization)说明。</span><span class="sxs-lookup"><span data-stu-id="51f4e-152">Follow the [Scaffold identity into a Razor project with authorization](xref:security/authentication/scaffold-identity#scaffold-identity-into-a-razor-project-with-authorization) instructions.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="51f4e-153">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51f4e-153">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="51f4e-154">添加注册、 登录和注销文件。</span><span class="sxs-lookup"><span data-stu-id="51f4e-154">Add the Register, Login, and LogOut files.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="51f4e-155">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="51f4e-155">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="51f4e-156">如果使用名称创建项目**WebApp1**，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="51f4e-156">If you created the project with name **WebApp1**, run the following commands.</span></span> <span data-ttu-id="51f4e-157">否则，请使用正确的命名空间为`ApplicationDbContext`:</span><span class="sxs-lookup"><span data-stu-id="51f4e-157">Otherwise, use the correct namespace for the `ApplicationDbContext`:</span></span>

```cli
dotnet aspnet-codegenerator identity -dc WebApp1.Data.ApplicationDbContext --files "Account.Register;Account.Login;Account.Logout"
```

<span data-ttu-id="51f4e-158">PowerShell 使用分号作为命令分隔符。</span><span class="sxs-lookup"><span data-stu-id="51f4e-158">PowerShell uses semicolon as a command separator.</span></span> <span data-ttu-id="51f4e-159">使用 PowerShell 时，转义分号的文件列表中，或将文件列表放在双引号内，如前面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="51f4e-159">When using PowerShell, escape the semicolons in the file list or put the file list in double quotes, as the preceding example shows.</span></span>

---

### <a name="examine-register"></a><span data-ttu-id="51f4e-160">检查注册</span><span class="sxs-lookup"><span data-stu-id="51f4e-160">Examine Register</span></span>

::: moniker range=">= aspnetcore-2.1"

   <span data-ttu-id="51f4e-161">当用户单击**注册**链接，`RegisterModel.OnPostAsync`调用操作。</span><span class="sxs-lookup"><span data-stu-id="51f4e-161">When a user clicks the **Register** link, the `RegisterModel.OnPostAsync` action is invoked.</span></span> <span data-ttu-id="51f4e-162">通过创建用户[CreateAsync](/dotnet/api/microsoft.aspnetcore.identity.usermanager-1.createasync#Microsoft_AspNetCore_Identity_UserManager_1_CreateAsync__0_System_String_)上`_userManager`对象。</span><span class="sxs-lookup"><span data-stu-id="51f4e-162">The user is created by [CreateAsync](/dotnet/api/microsoft.aspnetcore.identity.usermanager-1.createasync#Microsoft_AspNetCore_Identity_UserManager_1_CreateAsync__0_System_String_) on the `_userManager` object.</span></span> <span data-ttu-id="51f4e-163">`_userManager` 提供依赖关系注入）：</span><span class="sxs-lookup"><span data-stu-id="51f4e-163">`_userManager` is provided by dependency injection):</span></span>

   [!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/Register.cshtml.cs?name=snippet&highlight=7,22)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

   <span data-ttu-id="51f4e-164">当用户单击**注册**链接，链接`Register`上调用操作`AccountController`。</span><span class="sxs-lookup"><span data-stu-id="51f4e-164">When a user clicks the **Register** link, the `Register` action is invoked on `AccountController`.</span></span> <span data-ttu-id="51f4e-165">`Register`操作将创建用户，通过调用`CreateAsync`上`_userManager`对象 (提供给`AccountController`通过依赖关系注入):</span><span class="sxs-lookup"><span data-stu-id="51f4e-165">The `Register` action creates the user by calling `CreateAsync` on the `_userManager` object (provided to `AccountController` by dependency injection):</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_register&highlight=11)]

::: moniker-end

   <span data-ttu-id="51f4e-166">如果已成功创建用户，用户记录通过调用`_signInManager.SignInAsync`。</span><span class="sxs-lookup"><span data-stu-id="51f4e-166">If the user was created successfully, the user is logged in by the call to `_signInManager.SignInAsync`.</span></span>

   <span data-ttu-id="51f4e-167">**注意：** 请参阅[帐户确认](xref:security/authentication/accconfirm#prevent-login-at-registration)有关步骤，以防止在登记时立即登录。</span><span class="sxs-lookup"><span data-stu-id="51f4e-167">**Note:** See [account confirmation](xref:security/authentication/accconfirm#prevent-login-at-registration) for steps to prevent immediate login at registration.</span></span>

### <a name="log-in"></a><span data-ttu-id="51f4e-168">登录</span><span class="sxs-lookup"><span data-stu-id="51f4e-168">Log in</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="51f4e-169">显示登录窗体时：</span><span class="sxs-lookup"><span data-stu-id="51f4e-169">The Login form is displayed when:</span></span>

* <span data-ttu-id="51f4e-170">**登录**选择链接。</span><span class="sxs-lookup"><span data-stu-id="51f4e-170">The **Log in** link is selected.</span></span>
* <span data-ttu-id="51f4e-171">用户尝试访问受限的页面，他们不向被授权访问**或**时在还没有已完成身份验证系统。</span><span class="sxs-lookup"><span data-stu-id="51f4e-171">A user attempts to access a restricted page that they aren't authorized to access **or** when they haven't been authenticated by the system.</span></span>

<span data-ttu-id="51f4e-172">登录页上的表单提交时，`OnPostAsync`调用操作。</span><span class="sxs-lookup"><span data-stu-id="51f4e-172">When the form on the Login page is submitted, the `OnPostAsync` action is called.</span></span> <span data-ttu-id="51f4e-173">`PasswordSignInAsync` 对调用`_signInManager`对象 （由依赖关系注入提供）。</span><span class="sxs-lookup"><span data-stu-id="51f4e-173">`PasswordSignInAsync` is called on the `_signInManager` object (provided by dependency injection).</span></span>

   [!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/Login.cshtml.cs?name=snippet&highlight=10-11)]

   <span data-ttu-id="51f4e-174">基`Controller`类公开`User`，可以从控制器方法访问的属性。</span><span class="sxs-lookup"><span data-stu-id="51f4e-174">The base `Controller` class exposes a `User` property that you can access from controller methods.</span></span> <span data-ttu-id="51f4e-175">例如，可以枚举`User.Claims`和做出授权决定。</span><span class="sxs-lookup"><span data-stu-id="51f4e-175">For instance, you can enumerate `User.Claims` and make authorization decisions.</span></span> <span data-ttu-id="51f4e-176">有关详细信息，请参阅 <xref:security/authorization/introduction> 。</span><span class="sxs-lookup"><span data-stu-id="51f4e-176">For more information, see <xref:security/authorization/introduction>.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="51f4e-177">当用户选择时，将显示登录窗体**登录**访问要求进行身份验证的页面时将被重定向或链接。</span><span class="sxs-lookup"><span data-stu-id="51f4e-177">The Login form is displayed when users select the **Log in** link or are redirected when accessing a page that requires authentication.</span></span> <span data-ttu-id="51f4e-178">当用户提交窗体上的登录页中， `AccountController` `Login`调用操作。</span><span class="sxs-lookup"><span data-stu-id="51f4e-178">When the user submits the form on the Login page, the `AccountController` `Login` action is called.</span></span>

<span data-ttu-id="51f4e-179">`Login`操作调用`PasswordSignInAsync`上`_signInManager`对象 (提供给`AccountController`通过依赖关系注入)。</span><span class="sxs-lookup"><span data-stu-id="51f4e-179">The `Login` action calls `PasswordSignInAsync` on the `_signInManager` object (provided to `AccountController` by dependency injection).</span></span>

[!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_login&highlight=13-14)]

<span data-ttu-id="51f4e-180">基本 (`Controller`或`PageModel`) 类公开`User`属性。</span><span class="sxs-lookup"><span data-stu-id="51f4e-180">The base (`Controller` or `PageModel`) class exposes a `User` property.</span></span> <span data-ttu-id="51f4e-181">例如，`User.Claims`可以枚举才能做出授权决定。</span><span class="sxs-lookup"><span data-stu-id="51f4e-181">For example, `User.Claims` can be enumerated to make authorization decisions.</span></span>

::: moniker-end

### <a name="log-out"></a><span data-ttu-id="51f4e-182">注销</span><span class="sxs-lookup"><span data-stu-id="51f4e-182">Log out</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="51f4e-183">**注销**链接调用`LogoutModel.OnPost`操作。</span><span class="sxs-lookup"><span data-stu-id="51f4e-183">The **Log out** link invokes the `LogoutModel.OnPost` action.</span></span> 

[!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/Logout.cshtml.cs)]

<span data-ttu-id="51f4e-184">[SignOutAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.signoutasync#Microsoft_AspNetCore_Identity_SignInManager_1_SignOutAsync)清除存储在 cookie 中的用户的声明。</span><span class="sxs-lookup"><span data-stu-id="51f4e-184">[SignOutAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.signoutasync#Microsoft_AspNetCore_Identity_SignInManager_1_SignOutAsync) clears the user's claims stored in a cookie.</span></span> <span data-ttu-id="51f4e-185">在调用后不重定向`SignOutAsync`或者在用户会**不**已注销。</span><span class="sxs-lookup"><span data-stu-id="51f4e-185">Don't redirect after calling `SignOutAsync` or the user will **not** be signed out.</span></span>

<span data-ttu-id="51f4e-186">中指定 post *Pages/Shared/_LoginPartial.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="51f4e-186">Post is specified in the *Pages/Shared/_LoginPartial.cshtml*:</span></span>

[!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/_LoginPartial.cshtml?highlight=10)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

   <span data-ttu-id="51f4e-187">单击**注销**链接调用`LogOut`操作。</span><span class="sxs-lookup"><span data-stu-id="51f4e-187">Clicking the **Log out** link calls the `LogOut` action.</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_logout&highlight=7)]

   <span data-ttu-id="51f4e-188">上述代码调用`_signInManager.SignOutAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="51f4e-188">The preceding code calls the `_signInManager.SignOutAsync` method.</span></span> <span data-ttu-id="51f4e-189">`SignOutAsync`方法将清除用户的声明存储在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="51f4e-189">The `SignOutAsync` method clears the user's claims stored in a cookie.</span></span>

::: moniker-end

## <a name="test-identity"></a><span data-ttu-id="51f4e-190">测试标识</span><span class="sxs-lookup"><span data-stu-id="51f4e-190">Test Identity</span></span>

<span data-ttu-id="51f4e-191">默认 web 项目模板允许匿名访问主页。</span><span class="sxs-lookup"><span data-stu-id="51f4e-191">The default web project templates allow anonymous access to the home pages.</span></span> <span data-ttu-id="51f4e-192">若要测试标识，将添加[ `[Authorize]` ](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute)到关于页面。</span><span class="sxs-lookup"><span data-stu-id="51f4e-192">To test Identity, add [`[Authorize]`](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute) to the About page.</span></span>

[!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/About.cshtml.cs)]

<span data-ttu-id="51f4e-193">如果你登录，请注销。运行应用并选择**有关**链接。</span><span class="sxs-lookup"><span data-stu-id="51f4e-193">If you are signed in, sign out. Run the app and select the **About** link.</span></span> <span data-ttu-id="51f4e-194">你将重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="51f4e-194">You are redirected to the login page.</span></span>

::: moniker range=">= aspnetcore-2.1"

### <a name="explore-identity"></a><span data-ttu-id="51f4e-195">了解标识</span><span class="sxs-lookup"><span data-stu-id="51f4e-195">Explore Identity</span></span>

<span data-ttu-id="51f4e-196">若要更详细地了解标识：</span><span class="sxs-lookup"><span data-stu-id="51f4e-196">To explore Identity in more detail:</span></span>

* [<span data-ttu-id="51f4e-197">创建完整的标识 UI 源</span><span class="sxs-lookup"><span data-stu-id="51f4e-197">Create full identity UI source</span></span>](xref:security/authentication/scaffold-identity#create-full-identity-ui-source)
* <span data-ttu-id="51f4e-198">检查每个页面和单步执行调试器的源。</span><span class="sxs-lookup"><span data-stu-id="51f4e-198">Examine the source of each page and step through the debugger.</span></span>

::: moniker-end

## <a name="identity-components"></a><span data-ttu-id="51f4e-199">标识组件</span><span class="sxs-lookup"><span data-stu-id="51f4e-199">Identity Components</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="51f4e-200">中包含所有标识依赖 NuGet 包[Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)。</span><span class="sxs-lookup"><span data-stu-id="51f4e-200">All the Identity dependent NuGet packages are included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>

::: moniker-end

<span data-ttu-id="51f4e-201">标识将主包是[Microsoft.AspNetCore.Identity](https://www.nuget.org/packages/Microsoft.AspNetCore.Identity/)。</span><span class="sxs-lookup"><span data-stu-id="51f4e-201">The primary package for Identity is [Microsoft.AspNetCore.Identity](https://www.nuget.org/packages/Microsoft.AspNetCore.Identity/).</span></span> <span data-ttu-id="51f4e-202">此包包含 ASP.NET Core 标识的核心接口集，是 `Microsoft.AspNetCore.Identity.EntityFrameworkCore` 提供的。</span><span class="sxs-lookup"><span data-stu-id="51f4e-202">This package contains the core set of interfaces for ASP.NET Core Identity, and is included by `Microsoft.AspNetCore.Identity.EntityFrameworkCore`.</span></span>

## <a name="migrating-to-aspnet-core-identity"></a><span data-ttu-id="51f4e-203">迁移到 ASP.NET Core 标识</span><span class="sxs-lookup"><span data-stu-id="51f4e-203">Migrating to ASP.NET Core Identity</span></span>

<span data-ttu-id="51f4e-204">有关详细信息和指南迁移现有的标识存储，请参阅[迁移身份验证和标识](xref:migration/identity)。</span><span class="sxs-lookup"><span data-stu-id="51f4e-204">For more information and guidance on migrating your existing Identity store, see [Migrate Authentication and Identity](xref:migration/identity).</span></span>

## <a name="setting-password-strength"></a><span data-ttu-id="51f4e-205">设置密码强度</span><span class="sxs-lookup"><span data-stu-id="51f4e-205">Setting password strength</span></span>

<span data-ttu-id="51f4e-206">请参阅[配置](#pw)有关设置的最小密码要求的示例。</span><span class="sxs-lookup"><span data-stu-id="51f4e-206">See [Configuration](#pw) for a sample that sets the minimum password requirements.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51f4e-207">后续步骤</span><span class="sxs-lookup"><span data-stu-id="51f4e-207">Next Steps</span></span>

* [<span data-ttu-id="51f4e-208">配置标识</span><span class="sxs-lookup"><span data-stu-id="51f4e-208">Configure Identity</span></span>](xref:security/authentication/identity-configuration)
* <xref:security/authorization/secure-data>
* <xref:security/authentication/add-user-data>
* <xref:security/authentication/identity-enable-qrcodes>
* <xref:migration/identity>
* <xref:security/authentication/accconfirm>
* <xref:security/authentication/2fa>
* <xref:host-and-deploy/web-farm>
