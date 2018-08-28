---
title: 使用受授权的用户数据创建 ASP.NET Core 应用
author: rick-anderson
description: 了解如何使用受保护的授权的用户数据创建 Razor 页面应用。 包括 HTTPS、 身份验证、 安全性、 ASP.NET Core 标识。
ms.author: riande
ms.date: 7/24/2018
uid: security/authorization/secure-data
ms.openlocfilehash: ba59e8d6243965188397c4ba7a130eec42acfb91
ms.sourcegitcommit: 847cc1de5526ff42a7303491e6336c2dbdb45de4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43055875"
---
::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="258a4-104">请参阅[此 PDF](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf) ASP.NET Core MVC 版本。</span><span class="sxs-lookup"><span data-stu-id="258a4-104">See [this PDF](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf) for the ASP.NET Core MVC version.</span></span> <span data-ttu-id="258a4-105">本教程的 ASP.NET Core 1.1 版本是[这](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data)文件夹。</span><span class="sxs-lookup"><span data-stu-id="258a4-105">The ASP.NET Core 1.1 version of this tutorial is in [this](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data) folder.</span></span> <span data-ttu-id="258a4-106">ASP.NET Core 示例是在 1.1[示例](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2)。</span><span class="sxs-lookup"><span data-stu-id="258a4-106">The 1.1 ASP.NET Core sample is in the [samples](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2).</span></span>
::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="258a4-107">请参阅 [此 pdf] (https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_July16_18.pdf)</span><span class="sxs-lookup"><span data-stu-id="258a4-107">See the [this pdf] (https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_July16_18.pdf)</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

# <a name="create-an-aspnet-core-app-with-user-data-protected-by-authorization"></a><span data-ttu-id="258a4-108">使用受授权的用户数据创建 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="258a4-108">Create an ASP.NET Core app with user data protected by authorization</span></span>

<span data-ttu-id="258a4-109">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Joe Audette](https://twitter.com/joeaudette)</span><span class="sxs-lookup"><span data-stu-id="258a4-109">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Joe Audette](https://twitter.com/joeaudette)</span></span>

<span data-ttu-id="258a4-110">本教程演示如何使用受授权的用户数据创建 ASP.NET Core web 应用。</span><span class="sxs-lookup"><span data-stu-id="258a4-110">This tutorial shows how to create an ASP.NET Core web app with user data protected by authorization.</span></span> <span data-ttu-id="258a4-111">它显示的身份验证 （注册） 的用户的联系人列表已创建。</span><span class="sxs-lookup"><span data-stu-id="258a4-111">It displays a list of contacts that authenticated (registered) users have created.</span></span> <span data-ttu-id="258a4-112">有三个安全组：</span><span class="sxs-lookup"><span data-stu-id="258a4-112">There are three security groups:</span></span>

* <span data-ttu-id="258a4-113">**注册用户**可以查看所有已批准的数据还可以编辑/删除其自己的数据。</span><span class="sxs-lookup"><span data-stu-id="258a4-113">**Registered users** can view all the approved data and can edit/delete their own data.</span></span>
* <span data-ttu-id="258a4-114">**管理器**可以批准或拒绝的联系人数据。</span><span class="sxs-lookup"><span data-stu-id="258a4-114">**Managers** can approve or reject contact data.</span></span> <span data-ttu-id="258a4-115">仅已批准的联系人是对用户可见。</span><span class="sxs-lookup"><span data-stu-id="258a4-115">Only approved contacts are visible to users.</span></span>
* <span data-ttu-id="258a4-116">**管理员**可以批准/拒绝和编辑/删除的任何数据。</span><span class="sxs-lookup"><span data-stu-id="258a4-116">**Administrators** can approve/reject and edit/delete any data.</span></span>

<span data-ttu-id="258a4-117">在下图中，用户 Rick (`rick@example.com`) 登录。</span><span class="sxs-lookup"><span data-stu-id="258a4-117">In the following image, user Rick (`rick@example.com`) is signed in.</span></span> <span data-ttu-id="258a4-118">Rick 只能查看允许的联系人和**编辑**/**删除**/**新建**其联系人的链接。</span><span class="sxs-lookup"><span data-stu-id="258a4-118">Rick can only view approved contacts and **Edit**/**Delete**/**Create New** links for his contacts.</span></span> <span data-ttu-id="258a4-119">只有最后一个记录，创建由 Rick，显示**编辑**并**删除**链接。</span><span class="sxs-lookup"><span data-stu-id="258a4-119">Only the last record, created by Rick, displays **Edit** and **Delete** links.</span></span> <span data-ttu-id="258a4-120">其他用户不会看到的最后一个记录，直到经理或管理员的状态更改为"已批准"。</span><span class="sxs-lookup"><span data-stu-id="258a4-120">Other users won't see the last record until a manager or administrator changes the status to "Approved".</span></span>

![前面的图像描述](secure-data/_static/rick.png)

<span data-ttu-id="258a4-122">在下图中，`manager@contoso.com`在和中的管理器角色进行签名：</span><span class="sxs-lookup"><span data-stu-id="258a4-122">In the following image, `manager@contoso.com` is signed in and in the managers role:</span></span>

![前面的图像描述](secure-data/_static/manager1.png)

<span data-ttu-id="258a4-124">下图显示在管理器的联系人的详细信息视图：</span><span class="sxs-lookup"><span data-stu-id="258a4-124">The following image shows the managers details view of a contact:</span></span>

![前面的图像描述](secure-data/_static/manager.png)

<span data-ttu-id="258a4-126">**批准**并**拒绝**按钮仅显示经理和管理员。</span><span class="sxs-lookup"><span data-stu-id="258a4-126">The **Approve** and **Reject** buttons are only displayed for managers and administrators.</span></span>

<span data-ttu-id="258a4-127">在下图中，`admin@contoso.com`进行签名和管理员角色中：</span><span class="sxs-lookup"><span data-stu-id="258a4-127">In the following image, `admin@contoso.com` is signed in and in the administrators role:</span></span>

![前面的图像描述](secure-data/_static/admin.png)

<span data-ttu-id="258a4-129">管理员具有所有权限。</span><span class="sxs-lookup"><span data-stu-id="258a4-129">The administrator has all privileges.</span></span> <span data-ttu-id="258a4-130">她可以读取、 编辑或删除任何联系，并更改联系人的状态。</span><span class="sxs-lookup"><span data-stu-id="258a4-130">She can read/edit/delete any contact and change the status of contacts.</span></span>

<span data-ttu-id="258a4-131">通过创建该应用[基架](xref:tutorials/first-mvc-app-xplat/adding-model#scaffold-the-moviecontroller)以下`Contact`模型：</span><span class="sxs-lookup"><span data-stu-id="258a4-131">The app was created by [scaffolding](xref:tutorials/first-mvc-app-xplat/adding-model#scaffold-the-moviecontroller) the following `Contact` model:</span></span>

[!code-csharp[](secure-data/samples/starter2.1/Models/Contact.cs?name=snippet)]

<span data-ttu-id="258a4-132">此示例包含以下授权处理程序：</span><span class="sxs-lookup"><span data-stu-id="258a4-132">The sample contains the following authorization handlers:</span></span>

* <span data-ttu-id="258a4-133">`ContactIsOwnerAuthorizationHandler`： 可确保用户只能编辑其数据。</span><span class="sxs-lookup"><span data-stu-id="258a4-133">`ContactIsOwnerAuthorizationHandler`: Ensures that a user can only edit their data.</span></span>
* <span data-ttu-id="258a4-134">`ContactManagerAuthorizationHandler`： 允许经理批准或拒绝的联系人。</span><span class="sxs-lookup"><span data-stu-id="258a4-134">`ContactManagerAuthorizationHandler`: Allows managers to approve or reject contacts.</span></span>
* <span data-ttu-id="258a4-135">`ContactAdministratorsAuthorizationHandler`： 允许管理员可以批准或拒绝联系人并将编辑/删除联系人。</span><span class="sxs-lookup"><span data-stu-id="258a4-135">`ContactAdministratorsAuthorizationHandler`: Allows administrators to approve or reject contacts and to edit/delete contacts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="258a4-136">系统必备</span><span class="sxs-lookup"><span data-stu-id="258a4-136">Prerequisites</span></span>

<span data-ttu-id="258a4-137">本教程被高级。</span><span class="sxs-lookup"><span data-stu-id="258a4-137">This tutorial is advanced.</span></span> <span data-ttu-id="258a4-138">您应熟悉：</span><span class="sxs-lookup"><span data-stu-id="258a4-138">You should be familiar with:</span></span>

* [<span data-ttu-id="258a4-139">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="258a4-139">ASP.NET Core</span></span>](xref:tutorials/first-mvc-app/start-mvc)
* [<span data-ttu-id="258a4-140">身份验证</span><span class="sxs-lookup"><span data-stu-id="258a4-140">Authentication</span></span>](xref:security/authentication/index)
* [<span data-ttu-id="258a4-141">帐户确认和密码恢复</span><span class="sxs-lookup"><span data-stu-id="258a4-141">Account Confirmation and Password Recovery</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="258a4-142">授权</span><span class="sxs-lookup"><span data-stu-id="258a4-142">Authorization</span></span>](xref:security/authorization/index)
* [<span data-ttu-id="258a4-143">Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="258a4-143">Entity Framework Core</span></span>](xref:data/ef-mvc/intro)

<span data-ttu-id="258a4-144">对于本教程中的下载代码需要 ASP.NET Core 2.2 preview 1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="258a4-144">The download code as for this tutorial requires ASP.NET Core 2.2 preview 1 or later.</span></span> <span data-ttu-id="258a4-145">请参阅[此 GitHub 问题](https://github.com/aspnet/Identity/issues/1813#issuecomment-394543909)的解决办法。</span><span class="sxs-lookup"><span data-stu-id="258a4-145">See [this GitHub issue](https://github.com/aspnet/Identity/issues/1813#issuecomment-394543909) for a work-around.</span></span>

## <a name="the-starter-and-completed-app"></a><span data-ttu-id="258a4-146">Starter 和已完成应用程序</span><span class="sxs-lookup"><span data-stu-id="258a4-146">The starter and completed app</span></span>

<span data-ttu-id="258a4-147">[下载](xref:tutorials/index#how-to-download-a-sample)[完成](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2)应用。</span><span class="sxs-lookup"><span data-stu-id="258a4-147">[Download](xref:tutorials/index#how-to-download-a-sample) the [completed](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2) app.</span></span> <span data-ttu-id="258a4-148">[测试](#test-the-completed-app)已完成的应用，使你熟悉其安全功能。</span><span class="sxs-lookup"><span data-stu-id="258a4-148">[Test](#test-the-completed-app) the completed app so you become familiar with its security features.</span></span>

### <a name="the-starter-app"></a><span data-ttu-id="258a4-149">入门级应用</span><span class="sxs-lookup"><span data-stu-id="258a4-149">The starter app</span></span>

<span data-ttu-id="258a4-150">[下载](xref:tutorials/index#how-to-download-a-sample)[初学者](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2)应用。</span><span class="sxs-lookup"><span data-stu-id="258a4-150">[Download](xref:tutorials/index#how-to-download-a-sample) the [starter](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2) app.</span></span>

<span data-ttu-id="258a4-151">运行应用，点击**ContactManager**链接，并验证是否可以创建、 编辑和删除联系人。</span><span class="sxs-lookup"><span data-stu-id="258a4-151">Run the app, tap the **ContactManager** link, and verify you can create, edit, and delete a contact.</span></span>

## <a name="secure-user-data"></a><span data-ttu-id="258a4-152">保护用户数据</span><span class="sxs-lookup"><span data-stu-id="258a4-152">Secure user data</span></span>

<span data-ttu-id="258a4-153">以下部分介绍了所有主要的步骤以创建安全的用户数据应用程序。</span><span class="sxs-lookup"><span data-stu-id="258a4-153">The following sections have all the major steps to create the secure user data app.</span></span> <span data-ttu-id="258a4-154">您可能会发现引用的已完成项目很有帮助。</span><span class="sxs-lookup"><span data-stu-id="258a4-154">You may find it helpful to refer to the completed project.</span></span>

### <a name="tie-the-contact-data-to-the-user"></a><span data-ttu-id="258a4-155">将绑定到用户的联系人数据</span><span class="sxs-lookup"><span data-stu-id="258a4-155">Tie the contact data to the user</span></span>

<span data-ttu-id="258a4-156">使用 ASP.NET[标识](xref:security/authentication/identity)用户 ID，以确保用户可以编辑其数据，而不是其他用户数据。</span><span class="sxs-lookup"><span data-stu-id="258a4-156">Use the ASP.NET [Identity](xref:security/authentication/identity) user ID to ensure users can edit their data, but not other users data.</span></span> <span data-ttu-id="258a4-157">添加`OwnerID`并`ContactStatus`到`Contact`模型：</span><span class="sxs-lookup"><span data-stu-id="258a4-157">Add `OwnerID` and `ContactStatus` to the `Contact` model:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Models/Contact.cs?name=snippet1&highlight=5-6,16-999)]

<span data-ttu-id="258a4-158">`OwnerID` 是从用户的 ID`AspNetUser`表中[标识](xref:security/authentication/identity)数据库。</span><span class="sxs-lookup"><span data-stu-id="258a4-158">`OwnerID` is the user's ID from the `AspNetUser` table in the [Identity](xref:security/authentication/identity) database.</span></span> <span data-ttu-id="258a4-159">`Status`字段确定是否可由普通用户查看联系人。</span><span class="sxs-lookup"><span data-stu-id="258a4-159">The `Status` field determines if a contact is viewable by general users.</span></span>

<span data-ttu-id="258a4-160">创建新的迁移并更新数据库：</span><span class="sxs-lookup"><span data-stu-id="258a4-160">Create a new migration and update the database:</span></span>

```console
dotnet ef migrations add userID_Status
dotnet ef database update
```

### <a name="add-role-services-to-identity"></a><span data-ttu-id="258a4-161">将角色服务添加到标识</span><span class="sxs-lookup"><span data-stu-id="258a4-161">Add Role services to Identity</span></span>

<span data-ttu-id="258a4-162">追加[AddRoles](/dotnet/api/microsoft.aspnetcore.identity.identitybuilder.addroles#Microsoft_AspNetCore_Identity_IdentityBuilder_AddRoles__1)添加角色服务：</span><span class="sxs-lookup"><span data-stu-id="258a4-162">Append [AddRoles](/dotnet/api/microsoft.aspnetcore.identity.identitybuilder.addroles#Microsoft_AspNetCore_Identity_IdentityBuilder_AddRoles__1) to add Role services:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Startup.cs?name=snippet2&highlight=12)]

### <a name="require-authenticated-users"></a><span data-ttu-id="258a4-163">需要身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="258a4-163">Require authenticated users</span></span>

<span data-ttu-id="258a4-164">设置默认身份验证策略以要求用户进行身份验证：</span><span class="sxs-lookup"><span data-stu-id="258a4-164">Set the default authentication policy to require users to be authenticated:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Startup.cs?name=snippet&highlight=17-99)] 

 <span data-ttu-id="258a4-165">可以选择在 Razor 页面、 控制器或操作方法级别使用的身份验证禁用`[AllowAnonymous]`属性。</span><span class="sxs-lookup"><span data-stu-id="258a4-165">You can opt out of authentication at the Razor Page, controller, or action method level with the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="258a4-166">设置默认身份验证策略以要求用户进行身份验证来保护新添加的 Razor 页面和控制器。</span><span class="sxs-lookup"><span data-stu-id="258a4-166">Setting the default authentication policy to require users to be authenticated protects newly added Razor Pages and controllers.</span></span> <span data-ttu-id="258a4-167">默认情况下所需的身份验证是比依赖于新的控制器和 Razor 页，以包含更安全`[Authorize]`属性。</span><span class="sxs-lookup"><span data-stu-id="258a4-167">Having authentication required by default is more secure than relying on new controllers and Razor Pages to include the `[Authorize]` attribute.</span></span>

<span data-ttu-id="258a4-168">添加[AllowAnonymous](/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute)到索引中，因此匿名用户可以获取有关站点的信息注册有关，和联系人页面。</span><span class="sxs-lookup"><span data-stu-id="258a4-168">Add [AllowAnonymous](/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute) to the Index, About, and Contact pages so anonymous users can get information about the site before they register.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Index.cshtml.cs?highlight=1,6)]

### <a name="configure-the-test-account"></a><span data-ttu-id="258a4-169">配置测试帐户</span><span class="sxs-lookup"><span data-stu-id="258a4-169">Configure the test account</span></span>

<span data-ttu-id="258a4-170">`SeedData`类创建两个帐户： 管理员和管理员。</span><span class="sxs-lookup"><span data-stu-id="258a4-170">The `SeedData` class creates two accounts: administrator and manager.</span></span> <span data-ttu-id="258a4-171">使用[机密管理器工具](xref:security/app-secrets)设置这些帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="258a4-171">Use the [Secret Manager tool](xref:security/app-secrets) to set a password for these accounts.</span></span> <span data-ttu-id="258a4-172">从项目目录中设置密码 (目录包含*Program.cs*):</span><span class="sxs-lookup"><span data-stu-id="258a4-172">Set the password from the project directory (the directory containing *Program.cs*):</span></span>

```console
dotnet user-secrets set SeedUserPW <PW>
```

<span data-ttu-id="258a4-173">如果未指定强密码，将引发异常时`SeedData.Initialize`调用。</span><span class="sxs-lookup"><span data-stu-id="258a4-173">If a strong password is not specified, an exception is thrown when `SeedData.Initialize` is called.</span></span>

<span data-ttu-id="258a4-174">更新`Main`使用测试密码：</span><span class="sxs-lookup"><span data-stu-id="258a4-174">Update `Main` to use the test password:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Program.cs?name=snippet)]

### <a name="create-the-test-accounts-and-update-the-contacts"></a><span data-ttu-id="258a4-175">创建测试帐户和更新联系人</span><span class="sxs-lookup"><span data-stu-id="258a4-175">Create the test accounts and update the contacts</span></span>

<span data-ttu-id="258a4-176">更新`Initialize`中的方法`SeedData`类，以创建测试帐户：</span><span class="sxs-lookup"><span data-stu-id="258a4-176">Update the `Initialize` method in the `SeedData` class to create the test accounts:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Data/SeedData.cs?name=snippet_Initialize)]

<span data-ttu-id="258a4-177">添加管理员用户 ID 和`ContactStatus`到联系人。</span><span class="sxs-lookup"><span data-stu-id="258a4-177">Add the administrator user ID and `ContactStatus` to the contacts.</span></span> <span data-ttu-id="258a4-178">先创建一个"已提交"和一个"已拒绝"的联系人。</span><span class="sxs-lookup"><span data-stu-id="258a4-178">Make one of the contacts "Submitted" and one "Rejected".</span></span> <span data-ttu-id="258a4-179">将用户 ID 和状态添加到所有联系人。</span><span class="sxs-lookup"><span data-stu-id="258a4-179">Add the user ID and status to all the contacts.</span></span> <span data-ttu-id="258a4-180">只能有一个联系人所示：</span><span class="sxs-lookup"><span data-stu-id="258a4-180">Only one contact is shown:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Data/SeedData.cs?name=snippet1&highlight=17,18)]

## <a name="create-owner-manager-and-administrator-authorization-handlers"></a><span data-ttu-id="258a4-181">创建所有者、 经理和管理员授权处理程序</span><span class="sxs-lookup"><span data-stu-id="258a4-181">Create owner, manager, and administrator authorization handlers</span></span>

<span data-ttu-id="258a4-182">创建`ContactIsOwnerAuthorizationHandler`类中*授权*文件夹。</span><span class="sxs-lookup"><span data-stu-id="258a4-182">Create a `ContactIsOwnerAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="258a4-183">`ContactIsOwnerAuthorizationHandler`验证对资源进行操作的用户拥有的资源。</span><span class="sxs-lookup"><span data-stu-id="258a4-183">The `ContactIsOwnerAuthorizationHandler` verifies that the user acting on a resource owns the resource.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactIsOwnerAuthorizationHandler.cs)]

<span data-ttu-id="258a4-184">`ContactIsOwnerAuthorizationHandler`调用[上下文。成功](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.succeed#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_Succeed_Microsoft_AspNetCore_Authorization_IAuthorizationRequirement_)当前经过身份验证的用户是否联系所有者。</span><span class="sxs-lookup"><span data-stu-id="258a4-184">The `ContactIsOwnerAuthorizationHandler` calls [context.Succeed](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.succeed#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_Succeed_Microsoft_AspNetCore_Authorization_IAuthorizationRequirement_) if the current authenticated user is the contact owner.</span></span> <span data-ttu-id="258a4-185">授权处理程序通常：</span><span class="sxs-lookup"><span data-stu-id="258a4-185">Authorization handlers generally:</span></span>

* <span data-ttu-id="258a4-186">返回`context.Succeed`满足的要求。</span><span class="sxs-lookup"><span data-stu-id="258a4-186">Return `context.Succeed` when the requirements are met.</span></span>
* <span data-ttu-id="258a4-187">返回`Task.CompletedTask`时不符合要求。</span><span class="sxs-lookup"><span data-stu-id="258a4-187">Return `Task.CompletedTask` when requirements aren't met.</span></span> <span data-ttu-id="258a4-188">`Task.CompletedTask` 既不成功或失败&mdash;它允许运行其他授权处理程序。</span><span class="sxs-lookup"><span data-stu-id="258a4-188">`Task.CompletedTask` is neither success or failure&mdash;it allows other authorization handlers to run.</span></span>

<span data-ttu-id="258a4-189">如果你需要将显式失败，返回[上下文。失败](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.fail)。</span><span class="sxs-lookup"><span data-stu-id="258a4-189">If you need to explicitly fail, return [context.Fail](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.fail).</span></span>

<span data-ttu-id="258a4-190">应用程序允许联系所有者到编辑/删除/创建他们自己的数据。</span><span class="sxs-lookup"><span data-stu-id="258a4-190">The app allows contact owners to edit/delete/create their own data.</span></span> <span data-ttu-id="258a4-191">`ContactIsOwnerAuthorizationHandler` 不需要检查要求参数中传递该操作。</span><span class="sxs-lookup"><span data-stu-id="258a4-191">`ContactIsOwnerAuthorizationHandler` doesn't need to check the operation passed in the requirement parameter.</span></span>

### <a name="create-a-manager-authorization-handler"></a><span data-ttu-id="258a4-192">创建管理器授权处理程序</span><span class="sxs-lookup"><span data-stu-id="258a4-192">Create a manager authorization handler</span></span>

<span data-ttu-id="258a4-193">创建`ContactManagerAuthorizationHandler`类中*授权*文件夹。</span><span class="sxs-lookup"><span data-stu-id="258a4-193">Create a `ContactManagerAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="258a4-194">`ContactManagerAuthorizationHandler`验证对资源进行操作的用户是管理员。</span><span class="sxs-lookup"><span data-stu-id="258a4-194">The `ContactManagerAuthorizationHandler` verifies the user acting on the resource is a manager.</span></span> <span data-ttu-id="258a4-195">只有经理们才可以批准或拒绝内容的更改 （新的或已更改）。</span><span class="sxs-lookup"><span data-stu-id="258a4-195">Only managers can approve or reject content changes (new or changed).</span></span>

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactManagerAuthorizationHandler.cs)]

### <a name="create-an-administrator-authorization-handler"></a><span data-ttu-id="258a4-196">创建管理员授权处理程序</span><span class="sxs-lookup"><span data-stu-id="258a4-196">Create an administrator authorization handler</span></span>

<span data-ttu-id="258a4-197">创建`ContactAdministratorsAuthorizationHandler`类中*授权*文件夹。</span><span class="sxs-lookup"><span data-stu-id="258a4-197">Create a `ContactAdministratorsAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="258a4-198">`ContactAdministratorsAuthorizationHandler`验证对资源进行操作的用户是管理员。</span><span class="sxs-lookup"><span data-stu-id="258a4-198">The `ContactAdministratorsAuthorizationHandler` verifies the user acting on the resource is an administrator.</span></span> <span data-ttu-id="258a4-199">管理员可以执行所有操作。</span><span class="sxs-lookup"><span data-stu-id="258a4-199">Administrator can do all operations.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactAdministratorsAuthorizationHandler.cs)]

## <a name="register-the-authorization-handlers"></a><span data-ttu-id="258a4-200">注册授权处理程序</span><span class="sxs-lookup"><span data-stu-id="258a4-200">Register the authorization handlers</span></span>

<span data-ttu-id="258a4-201">必须为注册服务使用 Entity Framework Core[依赖关系注入](xref:fundamentals/dependency-injection)使用[AddScoped](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions)。</span><span class="sxs-lookup"><span data-stu-id="258a4-201">Services using Entity Framework Core must be registered for [dependency injection](xref:fundamentals/dependency-injection) using [AddScoped](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions).</span></span> <span data-ttu-id="258a4-202">`ContactIsOwnerAuthorizationHandler`使用 ASP.NET Core[标识](xref:security/authentication/identity)，这基于实体框架核心。</span><span class="sxs-lookup"><span data-stu-id="258a4-202">The `ContactIsOwnerAuthorizationHandler` uses ASP.NET Core [Identity](xref:security/authentication/identity), which is built on Entity Framework Core.</span></span> <span data-ttu-id="258a4-203">注册服务集合的处理程序，以便它们可供`ContactsController`通过[依赖关系注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="258a4-203">Register the handlers with the service collection so they're available to the `ContactsController` through [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="258a4-204">将以下代码添加到末尾`ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="258a4-204">Add the following code to the end of `ConfigureServices`:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Startup.cs?name=snippet_defaultPolicy&highlight=27-99)]

<span data-ttu-id="258a4-205">`ContactAdministratorsAuthorizationHandler` 和`ContactManagerAuthorizationHandler`添加为单一实例。</span><span class="sxs-lookup"><span data-stu-id="258a4-205">`ContactAdministratorsAuthorizationHandler` and `ContactManagerAuthorizationHandler` are added as singletons.</span></span> <span data-ttu-id="258a4-206">它们是单一实例，因为它们不使用 EF 和所需的所有信息都位于`Context`参数的`HandleRequirementAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="258a4-206">They're singletons because they don't use EF and all the information needed is in the `Context` parameter of the `HandleRequirementAsync` method.</span></span>

## <a name="support-authorization"></a><span data-ttu-id="258a4-207">支持授权</span><span class="sxs-lookup"><span data-stu-id="258a4-207">Support authorization</span></span>

<span data-ttu-id="258a4-208">在本部分中，将更新 Razor 页面和添加操作要求类。</span><span class="sxs-lookup"><span data-stu-id="258a4-208">In this section, you update the Razor Pages and add an operations requirements class.</span></span>

### <a name="review-the-contact-operations-requirements-class"></a><span data-ttu-id="258a4-209">查看联系人操作要求类</span><span class="sxs-lookup"><span data-stu-id="258a4-209">Review the contact operations requirements class</span></span>

<span data-ttu-id="258a4-210">查看`ContactOperations`类。</span><span class="sxs-lookup"><span data-stu-id="258a4-210">Review the `ContactOperations` class.</span></span> <span data-ttu-id="258a4-211">此类包含要求应用支持：</span><span class="sxs-lookup"><span data-stu-id="258a4-211">This class contains the requirements the app supports:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactOperations.cs)]

### <a name="create-a-base-class-for-the-contacts-razor-pages"></a><span data-ttu-id="258a4-212">创建联系人 Razor 页面的基类</span><span class="sxs-lookup"><span data-stu-id="258a4-212">Create a base class for the Contacts Razor Pages</span></span>

<span data-ttu-id="258a4-213">创建一个包含在联系人 Razor 页面使用的服务的基类。</span><span class="sxs-lookup"><span data-stu-id="258a4-213">Create a base class that contains the services used in the contacts Razor Pages.</span></span> <span data-ttu-id="258a4-214">基类将初始化代码放在一个位置：</span><span class="sxs-lookup"><span data-stu-id="258a4-214">The base class puts the initialization code in one location:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/DI_BasePageModel.cs)]

<span data-ttu-id="258a4-215">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="258a4-215">The preceding code:</span></span>

* <span data-ttu-id="258a4-216">添加`IAuthorizationService`服务对授权处理程序的访问权限。</span><span class="sxs-lookup"><span data-stu-id="258a4-216">Adds the `IAuthorizationService` service to access to the authorization handlers.</span></span>
* <span data-ttu-id="258a4-217">将标识添加`UserManager`服务。</span><span class="sxs-lookup"><span data-stu-id="258a4-217">Adds the Identity `UserManager` service.</span></span>
* <span data-ttu-id="258a4-218">添加 `ApplicationDbContext`。</span><span class="sxs-lookup"><span data-stu-id="258a4-218">Add the `ApplicationDbContext`.</span></span>

### <a name="update-the-createmodel"></a><span data-ttu-id="258a4-219">更新 CreateModel</span><span class="sxs-lookup"><span data-stu-id="258a4-219">Update the CreateModel</span></span>

<span data-ttu-id="258a4-220">更新创建页面模型构造函数以使用`DI_BasePageModel`基类：</span><span class="sxs-lookup"><span data-stu-id="258a4-220">Update the create page model constructor to use the `DI_BasePageModel` base class:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Create.cshtml.cs?name=snippetCtor)]

<span data-ttu-id="258a4-221">更新`CreateModel.OnPostAsync`方法：</span><span class="sxs-lookup"><span data-stu-id="258a4-221">Update the `CreateModel.OnPostAsync` method to:</span></span>

* <span data-ttu-id="258a4-222">添加到的用户 ID`Contact`模型。</span><span class="sxs-lookup"><span data-stu-id="258a4-222">Add the user ID to the `Contact` model.</span></span>
* <span data-ttu-id="258a4-223">调用授权处理程序，以验证用户有权创建联系人。</span><span class="sxs-lookup"><span data-stu-id="258a4-223">Call the authorization handler to verify the user has permission to create contacts.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Create.cshtml.cs?name=snippet_Create)]

### <a name="update-the-indexmodel"></a><span data-ttu-id="258a4-224">更新 IndexModel</span><span class="sxs-lookup"><span data-stu-id="258a4-224">Update the IndexModel</span></span>

<span data-ttu-id="258a4-225">更新`OnGetAsync`方法，以便仅被批准的联系人显示为普通用户：</span><span class="sxs-lookup"><span data-stu-id="258a4-225">Update the `OnGetAsync` method so only approved contacts are shown to general users:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Index.cshtml.cs?name=snippet)]

### <a name="update-the-editmodel"></a><span data-ttu-id="258a4-226">更新 EditModel</span><span class="sxs-lookup"><span data-stu-id="258a4-226">Update the EditModel</span></span>

<span data-ttu-id="258a4-227">添加授权处理程序以验证的用户拥有联系人。</span><span class="sxs-lookup"><span data-stu-id="258a4-227">Add an authorization handler to verify the user owns the contact.</span></span> <span data-ttu-id="258a4-228">正在验证资源授权，因为`[Authorize]`属性不能满足。</span><span class="sxs-lookup"><span data-stu-id="258a4-228">Because resource authorization is being validated, the `[Authorize]` attribute is not enough.</span></span> <span data-ttu-id="258a4-229">评估属性时，应用程序不具有对资源的访问。</span><span class="sxs-lookup"><span data-stu-id="258a4-229">The app doesn't have access to the resource when attributes are evaluated.</span></span> <span data-ttu-id="258a4-230">基于资源的授权必须是命令性。</span><span class="sxs-lookup"><span data-stu-id="258a4-230">Resource-based authorization must be imperative.</span></span> <span data-ttu-id="258a4-231">应用程序页面模型中加载或加载处理程序本身内获得资源的访问权限，则必须执行检查。</span><span class="sxs-lookup"><span data-stu-id="258a4-231">Checks must be performed once the app has access to the resource, either by loading it in the page model or by loading it within the handler itself.</span></span> <span data-ttu-id="258a4-232">您经常访问的资源，通过传入的资源键。</span><span class="sxs-lookup"><span data-stu-id="258a4-232">You frequently access the resource by passing in the resource key.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Edit.cshtml.cs?name=snippet)]

### <a name="update-the-deletemodel"></a><span data-ttu-id="258a4-233">更新 DeleteModel</span><span class="sxs-lookup"><span data-stu-id="258a4-233">Update the DeleteModel</span></span>

<span data-ttu-id="258a4-234">更新要使用授权处理程序来验证用户具有 delete 权限 contact 上的删除页面模型。</span><span class="sxs-lookup"><span data-stu-id="258a4-234">Update the delete page model to use the authorization handler to verify the user has delete permission on the contact.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Delete.cshtml.cs?name=snippet)]

## <a name="inject-the-authorization-service-into-the-views"></a><span data-ttu-id="258a4-235">将授权服务注入到视图</span><span class="sxs-lookup"><span data-stu-id="258a4-235">Inject the authorization service into the views</span></span>

<span data-ttu-id="258a4-236">目前，此 UI 显示编辑和删除的用户无法修改的联系人的链接。</span><span class="sxs-lookup"><span data-stu-id="258a4-236">Currently, the UI shows edit and delete links for contacts the user can't modify.</span></span>

<span data-ttu-id="258a4-237">注入中的授权服务*views/_viewimports.cshtml*文件，以便它可供所有视图：</span><span class="sxs-lookup"><span data-stu-id="258a4-237">Inject the authorization service in the *Views/_ViewImports.cshtml* file so it's available to all views:</span></span>

[!code-cshtml[](secure-data/samples/final2.1/Pages/_ViewImports.cshtml?highlight=6-99)]

<span data-ttu-id="258a4-238">上述标记添加了多种`using`语句。</span><span class="sxs-lookup"><span data-stu-id="258a4-238">The preceding markup adds several `using` statements.</span></span>

<span data-ttu-id="258a4-239">更新**编辑**并**删除**中的链接*Pages/Contacts/Index.cshtml*以便仅在呈现具有适当权限的用户：</span><span class="sxs-lookup"><span data-stu-id="258a4-239">Update the **Edit** and **Delete** links in *Pages/Contacts/Index.cshtml* so they're only rendered for users with the appropriate permissions:</span></span>

[!code-cshtml[](secure-data/samples/final2.1/Pages/Contacts/Index.cshtml?highlight=34-36,62-999)]

> [!WARNING]
> <span data-ttu-id="258a4-240">隐藏用户没有权限更改的数据中的链接不会保护应用。</span><span class="sxs-lookup"><span data-stu-id="258a4-240">Hiding links from users that don't have permission to change data doesn't secure the app.</span></span> <span data-ttu-id="258a4-241">隐藏链接使应用更加友好的用户显示唯一有效的链接。</span><span class="sxs-lookup"><span data-stu-id="258a4-241">Hiding links makes the app more user-friendly by displaying only valid links.</span></span> <span data-ttu-id="258a4-242">用户可以 hack 生成的 Url 以调用编辑和删除操作上不拥有的数据。</span><span class="sxs-lookup"><span data-stu-id="258a4-242">Users can hack the generated URLs to invoke edit and delete operations on data they don't own.</span></span> <span data-ttu-id="258a4-243">Razor 页面或控制器必须强制执行访问检查，以保护数据。</span><span class="sxs-lookup"><span data-stu-id="258a4-243">The Razor Page or controller must enforce access checks to secure the data.</span></span>

### <a name="update-details"></a><span data-ttu-id="258a4-244">更新详细信息</span><span class="sxs-lookup"><span data-stu-id="258a4-244">Update Details</span></span>

<span data-ttu-id="258a4-245">更新的详细信息视图，使管理员可以批准或拒绝联系人：</span><span class="sxs-lookup"><span data-stu-id="258a4-245">Update the details view so managers can approve or reject contacts:</span></span>

[!code-cshtml[](secure-data/samples/final2.1/Pages/Contacts/Details.cshtml?name=snippet)]

<span data-ttu-id="258a4-246">更新详细信息页模型：</span><span class="sxs-lookup"><span data-stu-id="258a4-246">Update the details page model:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Details.cshtml.cs?name=snippet)]

## <a name="test-the-completed-app"></a><span data-ttu-id="258a4-247">测试已完成的应用程序</span><span class="sxs-lookup"><span data-stu-id="258a4-247">Test the completed app</span></span>

<span data-ttu-id="258a4-248">如果应用了联系人：</span><span class="sxs-lookup"><span data-stu-id="258a4-248">If the app has contacts:</span></span>

* <span data-ttu-id="258a4-249">删除中的所有记录`Contact`表。</span><span class="sxs-lookup"><span data-stu-id="258a4-249">Delete all the records in the `Contact` table.</span></span>
* <span data-ttu-id="258a4-250">重新启动应用以设定数据库种子。</span><span class="sxs-lookup"><span data-stu-id="258a4-250">Restart the app to seed the database.</span></span>

<span data-ttu-id="258a4-251">浏览联系人注册用户。</span><span class="sxs-lookup"><span data-stu-id="258a4-251">Register a user for browsing the contacts.</span></span>

<span data-ttu-id="258a4-252">测试已完成的应用程序的简单方法是启动三个不同的浏览器 （或 incognito/InPrivate 版本）。</span><span class="sxs-lookup"><span data-stu-id="258a4-252">An easy way to test the completed app is to launch three different browsers (or incognito/InPrivate versions).</span></span> <span data-ttu-id="258a4-253">在一个浏览器中注册一个新用户 (例如， `test@example.com`)。</span><span class="sxs-lookup"><span data-stu-id="258a4-253">In one browser, register a new user (for example, `test@example.com`).</span></span> <span data-ttu-id="258a4-254">登录到每个浏览器使用不同的用户。</span><span class="sxs-lookup"><span data-stu-id="258a4-254">Sign in to each browser with a different user.</span></span> <span data-ttu-id="258a4-255">验证以下操作：</span><span class="sxs-lookup"><span data-stu-id="258a4-255">Verify the following operations:</span></span>

* <span data-ttu-id="258a4-256">已注册的用户可以查看所有已批准的联系人数据。</span><span class="sxs-lookup"><span data-stu-id="258a4-256">Registered users can view all the approved contact data.</span></span>
* <span data-ttu-id="258a4-257">已注册的用户可以编辑/删除其自己的数据。</span><span class="sxs-lookup"><span data-stu-id="258a4-257">Registered users can edit/delete their own data.</span></span>
* <span data-ttu-id="258a4-258">经理可以批准或拒绝的联系人数据。</span><span class="sxs-lookup"><span data-stu-id="258a4-258">Managers can approve or reject contact data.</span></span> <span data-ttu-id="258a4-259">`Details`视图视图将显示**批准**并**拒绝**按钮。</span><span class="sxs-lookup"><span data-stu-id="258a4-259">The `Details` view shows **Approve** and **Reject** buttons.</span></span>
* <span data-ttu-id="258a4-260">管理员可以批准/拒绝和编辑/删除的任何数据。</span><span class="sxs-lookup"><span data-stu-id="258a4-260">Administrators can approve/reject and edit/delete any data.</span></span>

| <span data-ttu-id="258a4-261">“用户”</span><span class="sxs-lookup"><span data-stu-id="258a4-261">User</span></span>| <span data-ttu-id="258a4-262">选项</span><span class="sxs-lookup"><span data-stu-id="258a4-262">Options</span></span> |
| ------------ | ---------|
| test@example.com | <span data-ttu-id="258a4-263">可以编辑/删除自己的数据</span><span class="sxs-lookup"><span data-stu-id="258a4-263">Can edit/delete own data</span></span> |
| manager@contoso.com | <span data-ttu-id="258a4-264">可以批准/拒绝和编辑/删除拥有的数据</span><span class="sxs-lookup"><span data-stu-id="258a4-264">Can approve/reject and edit/delete own data</span></span> |
| admin@contoso.com | <span data-ttu-id="258a4-265">可以编辑/删除和批准/拒绝的所有数据</span><span class="sxs-lookup"><span data-stu-id="258a4-265">Can edit/delete and approve/reject all data</span></span>|

<span data-ttu-id="258a4-266">在管理员的浏览器中创建联系人。</span><span class="sxs-lookup"><span data-stu-id="258a4-266">Create a contact in the administrator's browser.</span></span> <span data-ttu-id="258a4-267">删除 URL 复制并编辑从管理员的联系信息。</span><span class="sxs-lookup"><span data-stu-id="258a4-267">Copy the URL for delete and edit from the administrator contact.</span></span> <span data-ttu-id="258a4-268">将下面的链接粘贴到测试用户的浏览器以验证测试用户不能执行这些操作。</span><span class="sxs-lookup"><span data-stu-id="258a4-268">Paste these links into the test user's browser to verify the test user can't perform these operations.</span></span>

## <a name="create-the-starter-app"></a><span data-ttu-id="258a4-269">创建入门级应用</span><span class="sxs-lookup"><span data-stu-id="258a4-269">Create the starter app</span></span>

* <span data-ttu-id="258a4-270">创建名为"ContactManager"Razor 页面应用</span><span class="sxs-lookup"><span data-stu-id="258a4-270">Create a Razor Pages app named "ContactManager"</span></span>
   * <span data-ttu-id="258a4-271">创建包含应用**单个用户帐户**。</span><span class="sxs-lookup"><span data-stu-id="258a4-271">Create the app with **Individual User Accounts**.</span></span>
   * <span data-ttu-id="258a4-272">它命名为"ContactManager"使命名空间匹配的示例中使用的命名空间。</span><span class="sxs-lookup"><span data-stu-id="258a4-272">Name it "ContactManager" so the namespace matches the namespace used in the sample.</span></span>
   * <span data-ttu-id="258a4-273">`-uld` 指定 LocalDB，而不是 SQLite</span><span class="sxs-lookup"><span data-stu-id="258a4-273">`-uld` specifies LocalDB instead of SQLite</span></span>

  ```console
  dotnet new webapp -o ContactManager -au Individual -uld
  ```

* <span data-ttu-id="258a4-274">添加*Models\Contact.cs*:</span><span class="sxs-lookup"><span data-stu-id="258a4-274">Add *Models\Contact.cs*:</span></span>

  [!code-csharp[](secure-data/samples/starter2.1/Models/Contact.cs?name=snippet1)]

* <span data-ttu-id="258a4-275">基架`Contact`模型。</span><span class="sxs-lookup"><span data-stu-id="258a4-275">Scaffold the `Contact` model.</span></span>
* <span data-ttu-id="258a4-276">创建初始迁移并更新数据库：</span><span class="sxs-lookup"><span data-stu-id="258a4-276">Create initial migration and update the database:</span></span>

```console
dotnet aspnet-codegenerator razorpage -m Contact -udl -dc ApplicationDbContext -outDir Pages\Contacts --referenceScriptLibraries
dotnet ef database drop -f
dotnet ef migrations add initial
dotnet ef database update
```

* <span data-ttu-id="258a4-277">更新**ContactManager**中的定位点*pages/_layout.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="258a4-277">Update the **ContactManager** anchor in the *Pages/_Layout.cshtml* file:</span></span>

```cshtml
<a asp-page="/Contacts/Index" class="navbar-brand">ContactManager</a>
```

* <span data-ttu-id="258a4-278">测试应用程序的创建、 编辑和删除联系人</span><span class="sxs-lookup"><span data-stu-id="258a4-278">Test the app by creating, editing, and deleting a contact</span></span>

### <a name="seed-the-database"></a><span data-ttu-id="258a4-279">设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="258a4-279">Seed the database</span></span>

<span data-ttu-id="258a4-280">添加[SeedData](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2.1/Data/SeedData.cs)类来*数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="258a4-280">Add the [SeedData](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2.1/Data/SeedData.cs) class to the *Data* folder.</span></span>

<span data-ttu-id="258a4-281">调用`SeedData.Initialize`从`Main`:</span><span class="sxs-lookup"><span data-stu-id="258a4-281">Call `SeedData.Initialize` from `Main`:</span></span>

[!code-csharp[](secure-data/samples/starter2.1/Program.cs?name=snippet)]

<span data-ttu-id="258a4-282">测试应用程序设定数据库种子。</span><span class="sxs-lookup"><span data-stu-id="258a4-282">Test that the app seeded the database.</span></span> <span data-ttu-id="258a4-283">如果联系人 DB 中有任何行，则不会运行 seed 方法。</span><span class="sxs-lookup"><span data-stu-id="258a4-283">If there are any rows in the contact DB, the seed method doesn't run.</span></span>

<a name="secure-data-add-resources-label"></a>

### <a name="additional-resources"></a><span data-ttu-id="258a4-284">其他资源</span><span class="sxs-lookup"><span data-stu-id="258a4-284">Additional resources</span></span>

* <span data-ttu-id="258a4-285">[ASP.NET Core 授权实验室](https://github.com/blowdart/AspNetAuthorizationWorkshop)。</span><span class="sxs-lookup"><span data-stu-id="258a4-285">[ASP.NET Core Authorization Lab](https://github.com/blowdart/AspNetAuthorizationWorkshop).</span></span> <span data-ttu-id="258a4-286">此实验室进入的安全功能，本教程中介绍的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="258a4-286">This lab goes into more detail on the security features introduced in this tutorial.</span></span>
* [<span data-ttu-id="258a4-287">在 ASP.NET Core 中的授权： 基于声明的和自定义的简单，角色</span><span class="sxs-lookup"><span data-stu-id="258a4-287">Authorization in ASP.NET Core: Simple, role, claims-based, and custom</span></span>](xref:security/authorization/index)
* [<span data-ttu-id="258a4-288">基于自定义策略的授权</span><span class="sxs-lookup"><span data-stu-id="258a4-288">Custom policy-based authorization</span></span>](xref:security/authorization/policies)

::: moniker-end