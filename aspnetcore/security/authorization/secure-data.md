---
title: "使用受授权的用户数据创建 ASP.NET Core 应用"
author: rick-anderson
description: "了解如何创建使用受授权的用户数据的 Razor 页应用。 包括 HTTPS、 身份验证、 安全性、 ASP.NET 核心标识。"
manager: wpickett
ms.author: riande
ms.date: 01/24/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/secure-data
ms.openlocfilehash: e186adef2e72f852543a92ddce0e82be2a3bcd12
ms.sourcegitcommit: 809ee4baf8bf7b4cae9e366ecae29de1037d2bbb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="create-an-aspnet-core-app-with-user-data-protected-by-authorization"></a><span data-ttu-id="9eb1a-104">使用受授权的用户数据创建 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="9eb1a-104">Create an ASP.NET Core app with user data protected by authorization</span></span>

<span data-ttu-id="9eb1a-105">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Joe Audette](https://twitter.com/joeaudette)</span><span class="sxs-lookup"><span data-stu-id="9eb1a-105">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Joe Audette](https://twitter.com/joeaudette)</span></span>

<span data-ttu-id="9eb1a-106">本教程演示如何使用受授权的用户数据创建 ASP.NET 核心 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-106">This tutorial shows how to create an ASP.NET Core web app with user data protected by authorization.</span></span> <span data-ttu-id="9eb1a-107">它显示的身份验证的 （注册） 的用户的联系人列表已创建。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-107">It displays a list of contacts that authenticated (registered) users have created.</span></span> <span data-ttu-id="9eb1a-108">有三个安全组：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-108">There are three security groups:</span></span>

* <span data-ttu-id="9eb1a-109">**注册用户**可以查看所有已批准的数据并可以编辑/删除其自己的数据。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-109">**Registered users** can view all the approved data and can edit/delete their own data.</span></span>
* <span data-ttu-id="9eb1a-110">**管理器**可以批准或拒绝联系人数据。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-110">**Managers** can approve or reject contact data.</span></span> <span data-ttu-id="9eb1a-111">仅批准的联系人是对用户可见。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-111">Only approved contacts are visible to users.</span></span>
* <span data-ttu-id="9eb1a-112">**管理员**可以批准/拒绝和编辑/删除任何数据。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-112">**Administrators** can approve/reject and edit/delete any data.</span></span>

<span data-ttu-id="9eb1a-113">在下图中，用户 Rick (`rick@example.com`) 登录。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-113">In the following image, user Rick (`rick@example.com`) is signed in.</span></span> <span data-ttu-id="9eb1a-114">Rick 只能查看被批准的联系人和**编辑**/**删除**/**新建**他联系人的链接。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-114">Rick can only view approved contacts and **Edit**/**Delete**/**Create New** links for his contacts.</span></span> <span data-ttu-id="9eb1a-115">仅最新的记录，创建由 Rick，显示**编辑**和**删除**链接。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-115">Only the last record, created by Rick, displays **Edit** and **Delete** links.</span></span> <span data-ttu-id="9eb1a-116">其他用户不会看到的最新记录，直到经理或管理员的状态更改为"已批准"。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-116">Other users won't see the last record until a manager or administrator changes the status to "Approved".</span></span>

![映像所述前面](secure-data/_static/rick.png)

<span data-ttu-id="9eb1a-118">在下图中，`manager@contoso.com`进行签名和管理员角色中：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-118">In the following image, `manager@contoso.com` is signed in and in the managers role:</span></span>

![映像所述前面](secure-data/_static/manager1.png)

<span data-ttu-id="9eb1a-120">下图显示了管理器的联系人的详细信息视图：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-120">The following image shows the managers details view of a contact:</span></span>

![映像所述前面](secure-data/_static/manager.png)

<span data-ttu-id="9eb1a-122">**批准**和**拒绝**按钮仅显示经理和管理员。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-122">The **Approve** and **Reject** buttons are only displayed for managers and administrators.</span></span>

<span data-ttu-id="9eb1a-123">在下图中，`admin@contoso.com`进行签名和管理员角色中：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-123">In the following image, `admin@contoso.com` is signed in and in the administrators role:</span></span>

![映像所述前面](secure-data/_static/admin.png)

<span data-ttu-id="9eb1a-125">管理员具有所有权限。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-125">The administrator has all privileges.</span></span> <span data-ttu-id="9eb1a-126">她可以读取、 编辑或删除任何联系人，并更改联系人的状态。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-126">She can read/edit/delete any contact and change the status of contacts.</span></span>

<span data-ttu-id="9eb1a-127">应用程序由[基架](xref:tutorials/first-mvc-app-xplat/adding-model#scaffold-the-moviecontroller)以下`Contact`模型：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-127">The app was created by [scaffolding](xref:tutorials/first-mvc-app-xplat/adding-model#scaffold-the-moviecontroller) the following `Contact` model:</span></span>

[!code-csharp[Main](secure-data/samples/starter2/Models/Contact.cs?name=snippet1)]

<span data-ttu-id="9eb1a-128">该示例包含以下授权处理程序：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-128">The sample contains the following authorization handlers:</span></span>

* <span data-ttu-id="9eb1a-129">`ContactIsOwnerAuthorizationHandler`： 可确保用户只能编辑其数据。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-129">`ContactIsOwnerAuthorizationHandler`: Ensures that a user can only edit their data.</span></span>
* <span data-ttu-id="9eb1a-130">`ContactManagerAuthorizationHandler`： 允许管理器批准或拒绝联系人。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-130">`ContactManagerAuthorizationHandler`: Allows managers to approve or reject contacts.</span></span>
* <span data-ttu-id="9eb1a-131">`ContactAdministratorsAuthorizationHandler`： 允许管理员批准或拒绝联系人，还可以编辑/删除联系人。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-131">`ContactAdministratorsAuthorizationHandler`: Allows administrators to approve or reject contacts and to edit/delete contacts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9eb1a-132">系统必备</span><span class="sxs-lookup"><span data-stu-id="9eb1a-132">Prerequisites</span></span>

<span data-ttu-id="9eb1a-133">本教程被高级。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-133">This tutorial is advanced.</span></span> <span data-ttu-id="9eb1a-134">你应熟悉：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-134">You should be familiar with:</span></span>

* [<span data-ttu-id="9eb1a-135">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="9eb1a-135">ASP.NET Core</span></span>](xref:tutorials/first-mvc-app/start-mvc)
* [<span data-ttu-id="9eb1a-136">身份验证</span><span class="sxs-lookup"><span data-stu-id="9eb1a-136">Authentication</span></span>](xref:security/authentication/index)
* [<span data-ttu-id="9eb1a-137">帐户确认和密码恢复</span><span class="sxs-lookup"><span data-stu-id="9eb1a-137">Account Confirmation and Password Recovery</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="9eb1a-138">授权</span><span class="sxs-lookup"><span data-stu-id="9eb1a-138">Authorization</span></span>](xref:security/authorization/index)
* [<span data-ttu-id="9eb1a-139">Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="9eb1a-139">Entity Framework Core</span></span>](xref:data/ef-mvc/intro)

<span data-ttu-id="9eb1a-140">请参阅[此 PDF 文件](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf)ASP.NET 核心 MVC 版本。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-140">See [this PDF file](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf) for the ASP.NET Core MVC version.</span></span> <span data-ttu-id="9eb1a-141">本教程的 ASP.NET 核心 1.1 版本是[这](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data)文件夹。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-141">The ASP.NET Core 1.1 version of this tutorial is in [this](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data) folder.</span></span> <span data-ttu-id="9eb1a-142">ASP.NET 核心示例是在 1.1[示例](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2)。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-142">The 1.1 ASP.NET Core sample is in the [samples](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2).</span></span>

## <a name="the-starter-and-completed-app"></a><span data-ttu-id="9eb1a-143">初学者和已完成应用程序</span><span class="sxs-lookup"><span data-stu-id="9eb1a-143">The starter and completed app</span></span>

<span data-ttu-id="9eb1a-144">[下载](xref:tutorials/index#how-to-download-a-sample)[完成](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2)应用。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-144">[Download](xref:tutorials/index#how-to-download-a-sample) the [completed](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2) app.</span></span> <span data-ttu-id="9eb1a-145">[测试](#test-the-completed-app)已完成的应用程序使你熟悉其安全功能。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-145">[Test](#test-the-completed-app) the completed app so you become familiar with its security features.</span></span>

### <a name="the-starter-app"></a><span data-ttu-id="9eb1a-146">初学者应用</span><span class="sxs-lookup"><span data-stu-id="9eb1a-146">The starter app</span></span>

<span data-ttu-id="9eb1a-147">[下载](xref:tutorials/index#how-to-download-a-sample)[初学者](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2)应用。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-147">[Download](xref:tutorials/index#how-to-download-a-sample) the [starter](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2) app.</span></span>

<span data-ttu-id="9eb1a-148">运行应用，点击**ContactManager**链接，并验证是否可以创建、 编辑和删除联系人。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-148">Run the app, tap the **ContactManager** link, and verify you can create, edit, and delete a contact.</span></span>

## <a name="secure-user-data"></a><span data-ttu-id="9eb1a-149">保护用户数据</span><span class="sxs-lookup"><span data-stu-id="9eb1a-149">Secure user data</span></span>

<span data-ttu-id="9eb1a-150">下列各节具有所有主要的步骤以创建安全的用户数据应用。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-150">The following sections have all the major steps to create the secure user data app.</span></span> <span data-ttu-id="9eb1a-151">你可能会发现已完成的项目是指很有帮助。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-151">You may find it helpful to refer to the completed project.</span></span>

### <a name="tie-the-contact-data-to-the-user"></a><span data-ttu-id="9eb1a-152">将向用户的联系人数据</span><span class="sxs-lookup"><span data-stu-id="9eb1a-152">Tie the contact data to the user</span></span>

<span data-ttu-id="9eb1a-153">使用 ASP.NET[标识](xref:security/authentication/identity)用户 ID，以确保用户可以编辑其数据，而非其他用户数据。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-153">Use the ASP.NET [Identity](xref:security/authentication/identity) user ID to ensure users can edit their data, but not other users data.</span></span> <span data-ttu-id="9eb1a-154">添加`OwnerID`和`ContactStatus`到`Contact`模型：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-154">Add `OwnerID` and `ContactStatus` to the `Contact` model:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Models/Contact.cs?name=snippet1&highlight=5-6,16-999)]

<span data-ttu-id="9eb1a-155">`OwnerID` 是从用户的 ID`AspNetUser`表中[标识](xref:security/authentication/identity)数据库。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-155">`OwnerID` is the user's ID from the `AspNetUser` table in the [Identity](xref:security/authentication/identity) database.</span></span> <span data-ttu-id="9eb1a-156">`Status`字段确定是否可由常规用户查看联系人。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-156">The `Status` field determines if a contact is viewable by general users.</span></span>

<span data-ttu-id="9eb1a-157">创建一个新迁移并更新数据库：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-157">Create a new migration and update the database:</span></span>

```console
dotnet ef migrations add userID_Status
dotnet ef database update
```

### <a name="require-https-and-authenticated-users"></a><span data-ttu-id="9eb1a-158">需要 HTTPS 和经过身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="9eb1a-158">Require HTTPS and authenticated users</span></span>

<span data-ttu-id="9eb1a-159">添加[IHostingEnvironment](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment)到`Startup`:</span><span class="sxs-lookup"><span data-stu-id="9eb1a-159">Add [IHostingEnvironment](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) to `Startup`:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Startup.cs?name=snippet_env)]

<span data-ttu-id="9eb1a-160">在`ConfigureServices`方法*Startup.cs*文件中，添加[RequireHttpsAttribute](/aspnet/core/api/microsoft.aspnetcore.mvc.requirehttpsattribute)授权筛选器：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-160">In the `ConfigureServices` method of the *Startup.cs* file, add the [RequireHttpsAttribute](/aspnet/core/api/microsoft.aspnetcore.mvc.requirehttpsattribute) authorization filter:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Startup.cs?name=snippet_SSL&highlight=10-999)]

<span data-ttu-id="9eb1a-161">如果你使用 Visual Studio，则启用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-161">If you're using Visual Studio, enable HTTPS.</span></span>

<span data-ttu-id="9eb1a-162">若要将 HTTP 请求重定向到 HTTPS，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-162">To redirect HTTP requests to HTTPS, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span> <span data-ttu-id="9eb1a-163">如果你使用 Visual Studio Code 或不包括为支持 HTTPS 的测试证书的本地平台上测试：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-163">If you're using Visual Studio Code or testing on a local platform that doesn't include a test certificate for HTTPS:</span></span>

  <span data-ttu-id="9eb1a-164">设置`"LocalTest:skipSSL": true`中*appsettings。Developement.json*文件。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-164">Set `"LocalTest:skipSSL": true` in the *appsettings.Developement.json* file.</span></span>

### <a name="require-authenticated-users"></a><span data-ttu-id="9eb1a-165">要求经过身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="9eb1a-165">Require authenticated users</span></span>

<span data-ttu-id="9eb1a-166">设置默认身份验证策略以要求用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-166">Set the default authentication policy to require users to be authenticated.</span></span> <span data-ttu-id="9eb1a-167">你可以选择不在与 Razor 页、 控制器或操作方法级别的身份验证`[AllowAnonymous]`属性。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-167">You can opt out of authentication at the Razor Page, controller, or action method level with the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="9eb1a-168">设置默认身份验证策略以要求用户进行身份验证保护新添加的 Razor 页和控制器。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-168">Setting the default authentication policy to require users to be authenticated protects newly added Razor Pages and controllers.</span></span> <span data-ttu-id="9eb1a-169">默认情况下所需的身份验证为比依赖于新控制器和 Razor 页，以包含更安全`[Authorize]`属性。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-169">Having authentication required by default is safer than relying on new controllers and Razor Pages to include the `[Authorize]` attribute.</span></span> 

<span data-ttu-id="9eb1a-170">与所有用户进行身份验证，要求[AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_)和[AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage?view=aspnetcore-2.0)调用不是必需的。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-170">With the requirement of all users authenticated, the [AuthorizeFolder](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_AuthorizeFolder_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_String_System_String_) and [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage?view=aspnetcore-2.0) calls are not required.</span></span>

<span data-ttu-id="9eb1a-171">更新`ConfigureServices`有以下更改：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-171">Update `ConfigureServices` with the following changes:</span></span>

* <span data-ttu-id="9eb1a-172">注释掉`AuthorizeFolder`和`AuthorizePage`。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-172">Comment out `AuthorizeFolder` and `AuthorizePage`.</span></span>
* <span data-ttu-id="9eb1a-173">设置默认身份验证策略以要求用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-173">Set the default authentication policy to require users to be authenticated.</span></span>

[!code-csharp[Main](secure-data/samples/final2/Startup.cs?name=snippet_defaultPolicy&highlight=23-27,31-999)]

<span data-ttu-id="9eb1a-174">添加[AllowAnonymous](/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute)到索引中，因此匿名用户可以获取有关站点的信息，然后它们注册的有关，和联系人页面。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-174">Add [AllowAnonymous](/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute) to the Index, About, and Contact pages so anonymous users can get information about the site before they register.</span></span> 

[!code-csharp[Main](secure-data/samples/final2/Pages/Index.cshtml.cs?name=snippet&highlight=2)]

<span data-ttu-id="9eb1a-175">添加`[AllowAnonymous]`到[LoginModel 和 RegisterModel](https://github.com/aspnet/templating/issues/238)。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-175">Add `[AllowAnonymous]` to the [LoginModel and RegisterModel](https://github.com/aspnet/templating/issues/238).</span></span>

### <a name="configure-the-test-account"></a><span data-ttu-id="9eb1a-176">配置测试帐户</span><span class="sxs-lookup"><span data-stu-id="9eb1a-176">Configure the test account</span></span>

<span data-ttu-id="9eb1a-177">`SeedData`类将创建两个帐户： 管理员和管理员。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-177">The `SeedData` class creates two accounts: administrator and manager.</span></span> <span data-ttu-id="9eb1a-178">使用[机密管理器工具](xref:security/app-secrets)设置这些帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-178">Use the [Secret Manager tool](xref:security/app-secrets) to set a password for these accounts.</span></span> <span data-ttu-id="9eb1a-179">从项目目录设置密码 (目录包含*Program.cs*):</span><span class="sxs-lookup"><span data-stu-id="9eb1a-179">Set the password from the project directory (the directory containing *Program.cs*):</span></span>

```console
dotnet user-secrets set SeedUserPW <PW>
```

<span data-ttu-id="9eb1a-180">更新`Main`使用测试密码：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-180">Update `Main` to use the test password:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Program.cs?name=snippet)]

### <a name="create-the-test-accounts-and-update-the-contacts"></a><span data-ttu-id="9eb1a-181">创建测试帐户和更新联系人</span><span class="sxs-lookup"><span data-stu-id="9eb1a-181">Create the test accounts and update the contacts</span></span>

<span data-ttu-id="9eb1a-182">更新`Initialize`中的方法`SeedData`类，以创建测试帐户：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-182">Update the `Initialize` method in the `SeedData` class to create the test accounts:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Data/SeedData.cs?name=snippet_Initialize)]

<span data-ttu-id="9eb1a-183">添加管理员的用户 ID 和`ContactStatus`向联系人。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-183">Add the administrator user ID and `ContactStatus` to the contacts.</span></span> <span data-ttu-id="9eb1a-184">先创建一个"已提交"和一个"已拒绝"的联系人。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-184">Make one of the contacts "Submitted" and one "Rejected".</span></span> <span data-ttu-id="9eb1a-185">将用户 ID 和状态添加到所有联系人。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-185">Add the user ID and status to all the contacts.</span></span> <span data-ttu-id="9eb1a-186">只能有一个联系人是所示：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-186">Only one contact is shown:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Data/SeedData.cs?name=snippet1&highlight=17,18)]

## <a name="create-owner-manager-and-administrator-authorization-handlers"></a><span data-ttu-id="9eb1a-187">创建所有者、 管理器中，和管理员授权处理程序</span><span class="sxs-lookup"><span data-stu-id="9eb1a-187">Create owner, manager, and administrator authorization handlers</span></span>

<span data-ttu-id="9eb1a-188">创建`ContactIsOwnerAuthorizationHandler`类*授权*文件夹。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-188">Create a `ContactIsOwnerAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="9eb1a-189">`ContactIsOwnerAuthorizationHandler`验证对资源进行操作的用户拥有的资源。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-189">The `ContactIsOwnerAuthorizationHandler` verifies that the user acting on a resource owns the resource.</span></span>

[!code-csharp[Main](secure-data/samples/final2/Authorization/ContactIsOwnerAuthorizationHandler.cs)]

<span data-ttu-id="9eb1a-190">`ContactIsOwnerAuthorizationHandler`调用[上下文。成功](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.succeed#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_Succeed_Microsoft_AspNetCore_Authorization_IAuthorizationRequirement_)当前经过身份验证的用户是否联系人的所有者。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-190">The `ContactIsOwnerAuthorizationHandler` calls [context.Succeed](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.succeed#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_Succeed_Microsoft_AspNetCore_Authorization_IAuthorizationRequirement_) if the current authenticated user is the contact owner.</span></span> <span data-ttu-id="9eb1a-191">授权处理程序通常：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-191">Authorization handlers generally:</span></span>

* <span data-ttu-id="9eb1a-192">返回`context.Succeed`满足的要求。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-192">Return `context.Succeed` when the requirements are met.</span></span>
* <span data-ttu-id="9eb1a-193">返回`Task.CompletedTask`当不满足要求。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-193">Return `Task.CompletedTask` when requirements aren't met.</span></span> <span data-ttu-id="9eb1a-194">`Task.CompletedTask` 既不成功或失败&mdash;它允许运行其他授权处理程序。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-194">`Task.CompletedTask` is neither success or failure&mdash;it allows other authorization handlers to run.</span></span>

<span data-ttu-id="9eb1a-195">如果你需要显式失败，返回[上下文。失败](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.fail)。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-195">If you need to explicitly fail, return [context.Fail](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.fail).</span></span>

<span data-ttu-id="9eb1a-196">该应用让联系人所有者到编辑/删除/创建其自己的数据。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-196">The app allows contact owners to edit/delete/create their own data.</span></span> <span data-ttu-id="9eb1a-197">`ContactIsOwnerAuthorizationHandler` 不需要请检查在要求参数中传递的操作。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-197">`ContactIsOwnerAuthorizationHandler` doesn't need to check the operation passed in the requirement parameter.</span></span>

### <a name="create-a-manager-authorization-handler"></a><span data-ttu-id="9eb1a-198">创建管理器授权处理程序</span><span class="sxs-lookup"><span data-stu-id="9eb1a-198">Create a manager authorization handler</span></span>

<span data-ttu-id="9eb1a-199">创建`ContactManagerAuthorizationHandler`类*授权*文件夹。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-199">Create a `ContactManagerAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="9eb1a-200">`ContactManagerAuthorizationHandler`验证用户对资源进行操作是一个管理器。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-200">The `ContactManagerAuthorizationHandler` verifies the user acting on the resource is a manager.</span></span> <span data-ttu-id="9eb1a-201">只有经理可以批准或拒绝内容更改 （新的或已更改的）。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-201">Only managers can approve or reject content changes (new or changed).</span></span>

[!code-csharp[Main](secure-data/samples/final2/Authorization/ContactManagerAuthorizationHandler.cs)]

### <a name="create-an-administrator-authorization-handler"></a><span data-ttu-id="9eb1a-202">创建一个管理员授权处理程序</span><span class="sxs-lookup"><span data-stu-id="9eb1a-202">Create an administrator authorization handler</span></span>

<span data-ttu-id="9eb1a-203">创建`ContactAdministratorsAuthorizationHandler`类*授权*文件夹。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-203">Create a `ContactAdministratorsAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="9eb1a-204">`ContactAdministratorsAuthorizationHandler`验证对资源进行操作的用户是管理员。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-204">The `ContactAdministratorsAuthorizationHandler` verifies the user acting on the resource is an administrator.</span></span> <span data-ttu-id="9eb1a-205">管理员可以执行所有操作。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-205">Administrator can do all operations.</span></span>

[!code-csharp[Main](secure-data/samples/final2/Authorization/ContactAdministratorsAuthorizationHandler.cs)]

## <a name="register-the-authorization-handlers"></a><span data-ttu-id="9eb1a-206">注册的授权处理程序</span><span class="sxs-lookup"><span data-stu-id="9eb1a-206">Register the authorization handlers</span></span>

<span data-ttu-id="9eb1a-207">必须为注册服务使用实体框架核心[依赖关系注入](xref:fundamentals/dependency-injection)使用[AddScoped](/aspnet/core/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions)。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-207">Services using Entity Framework Core must be registered for [dependency injection](xref:fundamentals/dependency-injection) using [AddScoped](/aspnet/core/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions).</span></span> <span data-ttu-id="9eb1a-208">`ContactIsOwnerAuthorizationHandler`使用 ASP.NET Core[标识](xref:security/authentication/identity)，这基于实体框架核心。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-208">The `ContactIsOwnerAuthorizationHandler` uses ASP.NET Core [Identity](xref:security/authentication/identity), which is built on Entity Framework Core.</span></span> <span data-ttu-id="9eb1a-209">注册服务集合的处理程序，因此要对其可供`ContactsController`通过[依赖关系注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-209">Register the handlers with the service collection so they're available to the `ContactsController` through [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="9eb1a-210">将以下代码添加到末尾`ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="9eb1a-210">Add the following code to the end of `ConfigureServices`:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Startup.cs?name=ConfigureServices&highlight=41-999)]

<span data-ttu-id="9eb1a-211">`ContactAdministratorsAuthorizationHandler` 和`ContactManagerAuthorizationHandler`添加为单一实例。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-211">`ContactAdministratorsAuthorizationHandler` and `ContactManagerAuthorizationHandler` are added as singletons.</span></span> <span data-ttu-id="9eb1a-212">它们是单一实例，因为它们不使用 EF 和所需的所有信息都，请参阅`Context`参数`HandleRequirementAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-212">They're singletons because they don't use EF and all the information needed is in the `Context` parameter of the `HandleRequirementAsync` method.</span></span>

## <a name="support-authorization"></a><span data-ttu-id="9eb1a-213">支持授权</span><span class="sxs-lookup"><span data-stu-id="9eb1a-213">Support authorization</span></span>

<span data-ttu-id="9eb1a-214">在本部分中，你将更新 Razor 的网页，并添加操作要求类。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-214">In this section, you update the Razor Pages and add an operations requirements class.</span></span>

### <a name="review-the-contact-operations-requirements-class"></a><span data-ttu-id="9eb1a-215">查看联系人的操作要求类</span><span class="sxs-lookup"><span data-stu-id="9eb1a-215">Review the contact operations requirements class</span></span>

<span data-ttu-id="9eb1a-216">查看`ContactOperations`类。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-216">Review the `ContactOperations` class.</span></span> <span data-ttu-id="9eb1a-217">此类包含要求应用程序支持：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-217">This class contains the requirements the app supports:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Authorization/ContactOperations.cs)]

### <a name="create-a-base-class-for-the-razor-pages"></a><span data-ttu-id="9eb1a-218">创建用于 Razor 页面的基类</span><span class="sxs-lookup"><span data-stu-id="9eb1a-218">Create a base class for the Razor Pages</span></span>

<span data-ttu-id="9eb1a-219">创建一个包含在联系人 Razor 页中所使用的服务的基本类。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-219">Create a base class that contains the services used in the contacts Razor Pages.</span></span> <span data-ttu-id="9eb1a-220">基的类将该初始化代码放在一个位置：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-220">The base class puts that initialization code in one location:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/DI_BasePageModel.cs)]

<span data-ttu-id="9eb1a-221">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-221">The preceding code:</span></span>

* <span data-ttu-id="9eb1a-222">将添加`IAuthorizationService`服务访问的授权处理程序。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-222">Adds the `IAuthorizationService` service to access to the authorization handlers.</span></span>
* <span data-ttu-id="9eb1a-223">添加标识`UserManager`服务。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-223">Adds the Identity `UserManager` service.</span></span>
* <span data-ttu-id="9eb1a-224">添加 `ApplicationDbContext`。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-224">Add the `ApplicationDbContext`.</span></span>

### <a name="update-the-createmodel"></a><span data-ttu-id="9eb1a-225">更新 CreateModel</span><span class="sxs-lookup"><span data-stu-id="9eb1a-225">Update the CreateModel</span></span>

<span data-ttu-id="9eb1a-226">更新创建页模型构造函数以使用`DI_BasePageModel`基类：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-226">Update the create page model constructor to use the `DI_BasePageModel` base class:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/Create.cshtml.cs?name=snippetCtor)]

<span data-ttu-id="9eb1a-227">更新`CreateModel.OnPostAsync`方法：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-227">Update the `CreateModel.OnPostAsync` method to:</span></span>

* <span data-ttu-id="9eb1a-228">添加到的用户 ID`Contact`模型。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-228">Add the user ID to the `Contact` model.</span></span>
* <span data-ttu-id="9eb1a-229">调用授权处理程序，以验证用户有权创建联系人。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-229">Call the authorization handler to verify the user has permission to create contacts.</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/Create.cshtml.cs?name=snippet_Create)]

### <a name="update-the-indexmodel"></a><span data-ttu-id="9eb1a-230">更新 IndexModel</span><span class="sxs-lookup"><span data-stu-id="9eb1a-230">Update the IndexModel</span></span>

<span data-ttu-id="9eb1a-231">更新`OnGetAsync`方法，以便仅被批准的联系人显示在常规用户：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-231">Update the `OnGetAsync` method so only approved contacts are shown to general users:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/Index.cshtml.cs?name=snippet)]

### <a name="update-the-editmodel"></a><span data-ttu-id="9eb1a-232">更新 EditModel</span><span class="sxs-lookup"><span data-stu-id="9eb1a-232">Update the EditModel</span></span>

<span data-ttu-id="9eb1a-233">添加授权处理程序以验证用户拥有联系人。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-233">Add an authorization handler to verify the user owns the contact.</span></span> <span data-ttu-id="9eb1a-234">正在验证资源授权，因为`[Authorize]`属性不足够。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-234">Because resource authorization is being validated, the `[Authorize]` attribute is not enough.</span></span> <span data-ttu-id="9eb1a-235">评估属性时，此应用程序没有对资源的访问。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-235">The app doesn't have access to the resource when attributes are evaluated.</span></span> <span data-ttu-id="9eb1a-236">基于资源的授权必须是命令性。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-236">Resource-based authorization must be imperative.</span></span> <span data-ttu-id="9eb1a-237">一旦应用程序有权访问该资源，通过在页模型中加载或加载内处理程序本身，则必须执行检查。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-237">Checks must be performed once the app has access to the resource, either by loading it in the page model or by loading it within the handler itself.</span></span> <span data-ttu-id="9eb1a-238">你经常访问的资源，通过传入的资源键。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-238">You frequently access the resource by passing in the resource key.</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/Edit.cshtml.cs?name=snippet)]

### <a name="update-the-deletemodel"></a><span data-ttu-id="9eb1a-239">更新 DeleteModel</span><span class="sxs-lookup"><span data-stu-id="9eb1a-239">Update the DeleteModel</span></span>

<span data-ttu-id="9eb1a-240">更新删除页模型，使用授权处理程序来验证用户对联系人拥有删除权限。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-240">Update the delete page model to use the authorization handler to verify the user has delete permission on the contact.</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/Delete.cshtml.cs?name=snippet)]

## <a name="inject-the-authorization-service-into-the-views"></a><span data-ttu-id="9eb1a-241">将授权服务注入到视图</span><span class="sxs-lookup"><span data-stu-id="9eb1a-241">Inject the authorization service into the views</span></span>

<span data-ttu-id="9eb1a-242">目前，UI 显示编辑和删除用户无法修改的数据的链接。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-242">Currently, the UI shows edit and delete links for data the user can't modify.</span></span> <span data-ttu-id="9eb1a-243">用户界面是通过将授权处理程序应用于视图固定的。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-243">The UI is fixed by applying the authorization handler to the views.</span></span>

<span data-ttu-id="9eb1a-244">插入中的授权服务*Views/_ViewImports.cshtml*文件以便它可供所有视图：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-244">Inject the authorization service in the *Views/_ViewImports.cshtml* file so it's available to all views:</span></span>

[!code-cshtml[Main](secure-data/samples/final2/Pages/_ViewImports.cshtml?highlight=6-9)]

<span data-ttu-id="9eb1a-245">前面的标记添加了多种`using`语句。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-245">The preceding markup adds several `using` statements.</span></span>

<span data-ttu-id="9eb1a-246">更新**编辑**和**删除**链接*Pages/Contacts/Index.cshtml*以便它们在仅呈现具有适当权限的用户：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-246">Update the **Edit** and **Delete** links in *Pages/Contacts/Index.cshtml* so they're only rendered for users with the appropriate permissions:</span></span>

[!code-cshtml[Main](secure-data/samples/final2/Pages/Contacts/Index.cshtml?highlight=34-36,64-999)]

> [!WARNING]
> <span data-ttu-id="9eb1a-247">隐藏来自没有更改数据的权限的用户的链接不安全应用程序。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-247">Hiding links from users that don't have permission to change data doesn't secure the app.</span></span> <span data-ttu-id="9eb1a-248">隐藏链接进行应用程序更加友好的用户显示唯一有效的链接。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-248">Hiding links makes the app more user-friendly by displaying only valid links.</span></span> <span data-ttu-id="9eb1a-249">用户可以 hack 生成的 Url 来调用编辑和删除在它们自己的数据的操作。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-249">Users can hack the generated URLs to invoke edit and delete operations on data they don't own.</span></span> <span data-ttu-id="9eb1a-250">Razor 页或控制器必须强制执行访问检查，以保护数据。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-250">The Razor Page or controller must enforce access checks to secure the data.</span></span>

### <a name="update-details"></a><span data-ttu-id="9eb1a-251">更新详细信息</span><span class="sxs-lookup"><span data-stu-id="9eb1a-251">Update Details</span></span>

<span data-ttu-id="9eb1a-252">更新的详细信息视图，以便经理可以批准或拒绝联系人：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-252">Update the details view so managers can approve or reject contacts:</span></span>

[!code-cshtml[Main](secure-data/samples/final2/Pages/Contacts/Details.cshtml?range=48-999)]

<span data-ttu-id="9eb1a-253">更新详细信息页模型：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-253">Update the details page model:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/Details.cshtml.cs?name=snippet)]

## <a name="test-the-completed-app"></a><span data-ttu-id="9eb1a-254">测试已完成的应用程序</span><span class="sxs-lookup"><span data-stu-id="9eb1a-254">Test the completed app</span></span>

<span data-ttu-id="9eb1a-255">如果你使用 Visual Studio Code 或不包括为支持 HTTPS 的测试证书的本地平台上测试：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-255">If you're using Visual Studio Code or testing on a local platform that doesn't include a test certificate for HTTPS:</span></span>

* <span data-ttu-id="9eb1a-256">设置`"LocalTest:skipSSL": true`中*appsettings。Developement.json*文件中跳过 HTTPS 要求。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-256">Set `"LocalTest:skipSSL": true` in the *appsettings.Developement.json* file to skip the HTTPS requirement.</span></span> <span data-ttu-id="9eb1a-257">跳过仅在开发计算机上的 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-257">Skip HTTPS only on a development machine.</span></span>

<span data-ttu-id="9eb1a-258">如果应用了联系人：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-258">If the app has contacts:</span></span>

* <span data-ttu-id="9eb1a-259">删除中的所有记录`Contact`表。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-259">Delete all the records in the `Contact` table.</span></span>
* <span data-ttu-id="9eb1a-260">重新启动应用植入到数据库。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-260">Restart the app to seed the database.</span></span>

<span data-ttu-id="9eb1a-261">浏览联系人注册用户。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-261">Register a user for browsing the contacts.</span></span>

<span data-ttu-id="9eb1a-262">若要测试已完成的应用程序的简单方法是以启动三个不同的浏览器 （或 incognito/InPrivate 版本）。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-262">An easy way to test the completed app is to launch three different browsers (or incognito/InPrivate versions).</span></span> <span data-ttu-id="9eb1a-263">一个在浏览器中注册一个新用户 (例如， `test@example.com`)。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-263">In one browser, register a new user (for example, `test@example.com`).</span></span> <span data-ttu-id="9eb1a-264">登录到每个浏览器了不同的用户。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-264">Sign in to each browser with a different user.</span></span> <span data-ttu-id="9eb1a-265">验证以下操作：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-265">Verify the following operations:</span></span>

* <span data-ttu-id="9eb1a-266">已注册的用户可以查看所有已批准的联系人数据。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-266">Registered users can view all the approved contact data.</span></span>
* <span data-ttu-id="9eb1a-267">已注册的用户可以编辑/删除其自己的数据。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-267">Registered users can edit/delete their own data.</span></span>
* <span data-ttu-id="9eb1a-268">经理可以批准或拒绝联系人数据。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-268">Managers can approve or reject contact data.</span></span> <span data-ttu-id="9eb1a-269">`Details`视图显示**批准**和**拒绝**按钮。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-269">The `Details` view shows **Approve** and **Reject** buttons.</span></span>
* <span data-ttu-id="9eb1a-270">管理员可以批准/拒绝和编辑/删除任何数据。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-270">Administrators can approve/reject and edit/delete any data.</span></span>

| <span data-ttu-id="9eb1a-271">“用户”</span><span class="sxs-lookup"><span data-stu-id="9eb1a-271">User</span></span>| <span data-ttu-id="9eb1a-272">选项</span><span class="sxs-lookup"><span data-stu-id="9eb1a-272">Options</span></span> |
| ------------ | ---------|
| test@example.com | <span data-ttu-id="9eb1a-273">可以编辑/删除自己的数据</span><span class="sxs-lookup"><span data-stu-id="9eb1a-273">Can edit/delete own data</span></span> |
| manager@contoso.com | <span data-ttu-id="9eb1a-274">可以批准/拒绝和编辑/删除拥有数据</span><span class="sxs-lookup"><span data-stu-id="9eb1a-274">Can approve/reject and edit/delete own data</span></span> |
| admin@contoso.com | <span data-ttu-id="9eb1a-275">可以编辑/删除和批准/拒绝的所有数据</span><span class="sxs-lookup"><span data-stu-id="9eb1a-275">Can edit/delete and approve/reject all data</span></span>|

<span data-ttu-id="9eb1a-276">在管理员的浏览器中创建一个联系人。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-276">Create a contact in the administrator's browser.</span></span> <span data-ttu-id="9eb1a-277">将删除该 URL 复制和编辑从管理员的联系信息。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-277">Copy the URL for delete and edit from the administrator contact.</span></span> <span data-ttu-id="9eb1a-278">将这些链接粘贴到测试用户的浏览器以验证测试用户无法执行这些操作。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-278">Paste these links into the test user's browser to verify the test user can't perform these operations.</span></span>

## <a name="create-the-starter-app"></a><span data-ttu-id="9eb1a-279">创建初学者应用</span><span class="sxs-lookup"><span data-stu-id="9eb1a-279">Create the starter app</span></span>

* <span data-ttu-id="9eb1a-280">创建名为"ContactManager"Razor 页应用</span><span class="sxs-lookup"><span data-stu-id="9eb1a-280">Create a Razor Pages app named "ContactManager"</span></span>

  * <span data-ttu-id="9eb1a-281">创建应用程序与**单个用户帐户**。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-281">Create the app with **Individual User Accounts**.</span></span>
  * <span data-ttu-id="9eb1a-282">请将其命名"ContactManager"使你的命名空间匹配示例中使用的命名空间。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-282">Name it "ContactManager" so your namespace matches the namespace used in the sample.</span></span>

  ```console
  dotnet new razor -o ContactManager -au Individual -uld
  ```

  * <span data-ttu-id="9eb1a-283">`-uld` 指定而不是 SQLite LocalDB</span><span class="sxs-lookup"><span data-stu-id="9eb1a-283">`-uld` specifies LocalDB instead of SQLite</span></span>

* <span data-ttu-id="9eb1a-284">添加以下`Contact`模型：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-284">Add the following `Contact` model:</span></span>

  [!code-csharp[Main](secure-data/samples/starter2/Models/Contact.cs?name=snippet1)]

* <span data-ttu-id="9eb1a-285">基架`Contact`模型：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-285">Scaffold the `Contact` model:</span></span>

```console
dotnet aspnet-codegenerator razorpage -m Contact -udl -dc ApplicationDbContext -outDir Pages\Contacts --referenceScriptLibraries
```

* <span data-ttu-id="9eb1a-286">更新**ContactManager**中锚定*Pages/_Layout.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-286">Update the **ContactManager** anchor in the *Pages/_Layout.cshtml* file:</span></span>

```cshtml
<a asp-page="/Contacts/Index" class="navbar-brand">ContactManager</a>
```

* <span data-ttu-id="9eb1a-287">构建基架初始迁移并更新数据库：</span><span class="sxs-lookup"><span data-stu-id="9eb1a-287">Scaffold the initial migration and update the database:</span></span>

```console
dotnet ef migrations add initial
dotnet ef database update
```

* <span data-ttu-id="9eb1a-288">测试应用程序通过创建、 编辑和删除联系人</span><span class="sxs-lookup"><span data-stu-id="9eb1a-288">Test the app by creating, editing, and deleting a contact</span></span>

### <a name="seed-the-database"></a><span data-ttu-id="9eb1a-289">设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="9eb1a-289">Seed the database</span></span>

<span data-ttu-id="9eb1a-290">添加`SeedData`类到*数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-290">Add the `SeedData` class to the *Data* folder.</span></span> <span data-ttu-id="9eb1a-291">如果你已下载示例，你可以复制*SeedData.cs*文件为*数据*初学者项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-291">If you've downloaded the sample, you can copy the *SeedData.cs* file to the *Data* folder of the starter project.</span></span>

<span data-ttu-id="9eb1a-292">调用`SeedData.Initialize`从`Main`:</span><span class="sxs-lookup"><span data-stu-id="9eb1a-292">Call `SeedData.Initialize` from `Main`:</span></span>

[!code-csharp[Main](secure-data/samples/starter2/Program.cs?name=snippet)]

<span data-ttu-id="9eb1a-293">测试应用程序设定种子的数据库。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-293">Test that the app seeded the database.</span></span> <span data-ttu-id="9eb1a-294">如果在联系人中数据库的任何行，不能运行 seed 方法。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-294">If there are any rows in the contact DB, the seed method doesn't run.</span></span>

<a name="secure-data-add-resources-label"></a>

### <a name="additional-resources"></a><span data-ttu-id="9eb1a-295">其他资源</span><span class="sxs-lookup"><span data-stu-id="9eb1a-295">Additional resources</span></span>

* <span data-ttu-id="9eb1a-296">[ASP.NET 核心授权实验室](https://github.com/blowdart/AspNetAuthorizationWorkshop)。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-296">[ASP.NET Core Authorization Lab](https://github.com/blowdart/AspNetAuthorizationWorkshop).</span></span> <span data-ttu-id="9eb1a-297">在本教程中引入的安全功能，此实验室将进入更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="9eb1a-297">This lab goes into more detail on the security features introduced in this tutorial.</span></span>
* [<span data-ttu-id="9eb1a-298">在 ASP.NET Core 中的授权： 基于声明的和自定义的简单，角色</span><span class="sxs-lookup"><span data-stu-id="9eb1a-298">Authorization in ASP.NET Core: Simple, role, claims-based, and custom</span></span>](xref:security/authorization/index)
* [<span data-ttu-id="9eb1a-299">基于自定义策略的授权</span><span class="sxs-lookup"><span data-stu-id="9eb1a-299">Custom policy-based authorization</span></span>](xref:security/authorization/policies)
