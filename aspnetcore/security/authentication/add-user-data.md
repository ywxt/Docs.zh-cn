---
title: 添加、 下载和删除标识到 ASP.NET 核心项目中的自定义用户数据
author: rick-anderson
description: 了解如何在 ASP.NET Core 项目中添加到标识的自定义用户数据。 删除每个 GDPR 数据。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 6/16/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/add-user-data
ms.openlocfilehash: 3ebb709cc40f6c2477ac57325d035b9b461e2eaf
ms.sourcegitcommit: 0d6f151e69c159d776ed0142773279e645edbc0a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2018
ms.locfileid: "35414989"
---
# <a name="add-download-and-delete-custom-user-data-to-identity-in-an-aspnet-core-project"></a><span data-ttu-id="32411-104">添加、 下载和删除标识到 ASP.NET 核心项目中的自定义用户数据</span><span class="sxs-lookup"><span data-stu-id="32411-104">Add, download, and delete custom user data to Identity in an ASP.NET Core project</span></span>

<span data-ttu-id="32411-105">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="32411-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="32411-106">这篇文章演示如何：</span><span class="sxs-lookup"><span data-stu-id="32411-106">This article shows how to:</span></span>

* <span data-ttu-id="32411-107">将自定义用户数据添加到 ASP.NET 核心 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="32411-107">Add custom user data to an ASP.NET Core web app.</span></span>
* <span data-ttu-id="32411-108">修饰具有自定义用户数据模型[PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1)属性，以便它自动下载和删除。</span><span class="sxs-lookup"><span data-stu-id="32411-108">Decorate the custom user data model with the [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1) attribute so it's automatically available for download and deletion.</span></span> <span data-ttu-id="32411-109">使能够下载和删除这些数据可帮助满足[GDPR](xref:security/gdpr)要求。</span><span class="sxs-lookup"><span data-stu-id="32411-109">Making the data able to be downloaded and deleted helps meet [GDPR](xref:security/gdpr) requirements.</span></span>

<span data-ttu-id="32411-110">项目示例将创建从 Razor 页 web 应用，但了 ASP.NET 核心 MVC web 应用的类似的说明。</span><span class="sxs-lookup"><span data-stu-id="32411-110">The project sample is created from a Razor Pages web app, but the instructions are similar for a ASP.NET Core MVC web app.</span></span>

<span data-ttu-id="32411-111">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="32411-111">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32411-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="32411-112">Prerequisites</span></span>

[!INCLUDE [](~/includes/2.1-SDK.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="32411-113">创建 Razor Web 应用</span><span class="sxs-lookup"><span data-stu-id="32411-113">Create a Razor web app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="32411-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32411-114">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="32411-115">从 Visual Studio“文件”菜单中选择“新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="32411-115">From the Visual Studio **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="32411-116">将项目**WebApp1**如果您希望与其匹配的命名空间[下载示例](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample)代码。</span><span class="sxs-lookup"><span data-stu-id="32411-116">Name the project **WebApp1** if you want to it match the namespace of the [download sample](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample) code.</span></span>
* <span data-ttu-id="32411-117">选择**ASP.NET 核心 Web 应用程序** > **确定**</span><span class="sxs-lookup"><span data-stu-id="32411-117">Select **ASP.NET Core Web Application** > **OK**</span></span>
* <span data-ttu-id="32411-118">选择**ASP.NET 核心 2.1**下拉列表中</span><span class="sxs-lookup"><span data-stu-id="32411-118">Select **ASP.NET Core 2.1** in the dropdown</span></span>
* <span data-ttu-id="32411-119">选择**Web 应用程序**  > **确定**</span><span class="sxs-lookup"><span data-stu-id="32411-119">Select **Web Application**  > **OK**</span></span>
* <span data-ttu-id="32411-120">生成并运行该项目。</span><span class="sxs-lookup"><span data-stu-id="32411-120">Build and run the project.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="32411-121">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="32411-121">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet new webapp -o WebApp1
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

---

## <a name="run-the-identity-scaffolder"></a><span data-ttu-id="32411-122">运行标识基架</span><span class="sxs-lookup"><span data-stu-id="32411-122">Run the Identity scaffolder</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="32411-123">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32411-123">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="32411-124">从**解决方案资源管理器**，右键单击该项目 >**添加** > **新建基架项**。</span><span class="sxs-lookup"><span data-stu-id="32411-124">From **Solution Explorer**, right-click on the project > **Add** > **New Scaffolded Item**.</span></span>
* <span data-ttu-id="32411-125">从左窗格**添加基架**对话框中，选择**标识** > **添加**。</span><span class="sxs-lookup"><span data-stu-id="32411-125">From the left pane of the **Add Scaffold** dialog, select **Identity** > **ADD**.</span></span>
* <span data-ttu-id="32411-126">在**添加标识**对话框中，以下选项：</span><span class="sxs-lookup"><span data-stu-id="32411-126">In the **ADD Identity** dialog, the following options:</span></span>
  * <span data-ttu-id="32411-127">选择现有的布局文件 *~/Pages/Shared/_Layout.cshtml*</span><span class="sxs-lookup"><span data-stu-id="32411-127">Select your existing layout  file  *~/Pages/Shared/_Layout.cshtml*</span></span>
  * <span data-ttu-id="32411-128">选择要重写的以下文件：</span><span class="sxs-lookup"><span data-stu-id="32411-128">Select the following files to override:</span></span>
    * <span data-ttu-id="32411-129">**帐户/注册**</span><span class="sxs-lookup"><span data-stu-id="32411-129">**Account/Register**</span></span>
    * <span data-ttu-id="32411-130">**帐户/管理/索引**</span><span class="sxs-lookup"><span data-stu-id="32411-130">**Account/Manage/Index**</span></span>
  * <span data-ttu-id="32411-131">选择**+** 按钮以创建一个新**数据上下文类**。</span><span class="sxs-lookup"><span data-stu-id="32411-131">Select the **+** button to create a new **Data context class**.</span></span> <span data-ttu-id="32411-132">接受类型 (**WebApp1.Models.WebApp1Context**如果名为项目**WebApp1**)。</span><span class="sxs-lookup"><span data-stu-id="32411-132">Accept the type (**WebApp1.Models.WebApp1Context** if you named the project **WebApp1**).</span></span>
  * <span data-ttu-id="32411-133">选择**+** 按钮以创建一个新**用户类**。</span><span class="sxs-lookup"><span data-stu-id="32411-133">Select the **+** button to create a new **User class**.</span></span> <span data-ttu-id="32411-134">接受类型 (**WebApp1User**如果名为项目**WebApp1**) >**添加**。</span><span class="sxs-lookup"><span data-stu-id="32411-134">Accept the type (**WebApp1User** if you named the project **WebApp1**) > **Add**.</span></span>
* <span data-ttu-id="32411-135">选择**添加**。</span><span class="sxs-lookup"><span data-stu-id="32411-135">Select **ADD**.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="32411-136">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="32411-136">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="32411-137">如果以前尚未安装 ASP.NET 基架，请立即进行安装：</span><span class="sxs-lookup"><span data-stu-id="32411-137">If you have not previously installed the ASP.NET scaffolder, install it now:</span></span>

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

<span data-ttu-id="32411-138">添加对的包引用[Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/)项目 (.csproj) 文件。</span><span class="sxs-lookup"><span data-stu-id="32411-138">Add a package reference to [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) to the project (.csproj) file.</span></span> <span data-ttu-id="32411-139">在项目目录中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="32411-139">Run the following command in the project directory:</span></span>

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

<span data-ttu-id="32411-140">运行以下命令以列出标识基架选项：</span><span class="sxs-lookup"><span data-stu-id="32411-140">Run the following command to list the Identity scaffolder options:</span></span>

```cli
dotnet aspnet-codegenerator identity -h
```

<span data-ttu-id="32411-141">在项目文件夹中，运行标识基架：</span><span class="sxs-lookup"><span data-stu-id="32411-141">In the project folder, run the Identity scaffolder:</span></span>

```cli
dotnet aspnet-codegenerator identity -u WebApp1User -fi Account.Register;Account.Manage.Index
```

-------------

<span data-ttu-id="32411-142">按照中的说明[迁移、 UseAuthentication 和布局](xref:security/authentication/scaffold-identity#efm)以执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="32411-142">Follow the instruction in [Migrations, UseAuthentication, and layout](xref:security/authentication/scaffold-identity#efm) to perform the following steps:</span></span>

* <span data-ttu-id="32411-143">创建迁移并更新数据库。</span><span class="sxs-lookup"><span data-stu-id="32411-143">Create a migration and update the database.</span></span>
* <span data-ttu-id="32411-144">将 `UseAuthentication` 添加到 `Startup.Configure`。</span><span class="sxs-lookup"><span data-stu-id="32411-144">Add `UseAuthentication` to `Startup.Configure`.</span></span>
* <span data-ttu-id="32411-145">添加`<partial name="_LoginPartial" />`布局文件。</span><span class="sxs-lookup"><span data-stu-id="32411-145">Add `<partial name="_LoginPartial" />` to the layout file.</span></span>
* <span data-ttu-id="32411-146">测试应用：</span><span class="sxs-lookup"><span data-stu-id="32411-146">Test the app:</span></span>
  * <span data-ttu-id="32411-147">注册用户</span><span class="sxs-lookup"><span data-stu-id="32411-147">Register a user</span></span>
  * <span data-ttu-id="32411-148">选择新的用户名称 (旁边**注销**链接)。</span><span class="sxs-lookup"><span data-stu-id="32411-148">Select the new user name (next to the **Logout** link).</span></span> <span data-ttu-id="32411-149">你可能需要展开该窗口或选择要显示的用户名和其他链接的导航栏图标。</span><span class="sxs-lookup"><span data-stu-id="32411-149">You might need to expand the window or select the navigation bar icon to show the user name and other links.</span></span>
  * <span data-ttu-id="32411-150">选择**个人数据**选项卡。</span><span class="sxs-lookup"><span data-stu-id="32411-150">Select the **Personal Data** tab.</span></span>
  * <span data-ttu-id="32411-151">选择**下载**按钮，然后检查*PersonalData.json*文件。</span><span class="sxs-lookup"><span data-stu-id="32411-151">Select the **Download** button and examined the *PersonalData.json* file.</span></span>
  * <span data-ttu-id="32411-152">测试**删除**按钮，删除已登录用户。</span><span class="sxs-lookup"><span data-stu-id="32411-152">Test the **Delete** button, which deletes the logged on user.</span></span>

## <a name="add-custom-user-data-to-the-identity-db"></a><span data-ttu-id="32411-153">将自定义用户数据添加到标识数据库</span><span class="sxs-lookup"><span data-stu-id="32411-153">Add custom user data to the Identity DB</span></span>

<span data-ttu-id="32411-154">更新`IdentityUser`派生类与自定义属性。</span><span class="sxs-lookup"><span data-stu-id="32411-154">Update the `IdentityUser` derived class with custom properties.</span></span> <span data-ttu-id="32411-155">如果名为你的项目 WebApp1 时，该文件名为*Areas/Identity/Data/WebApp1User.cs*。</span><span class="sxs-lookup"><span data-stu-id="32411-155">If you named your project WebApp1, the file is named *Areas/Identity/Data/WebApp1User.cs*.</span></span> <span data-ttu-id="32411-156">替换为以下代码更新文件：</span><span class="sxs-lookup"><span data-stu-id="32411-156">Update the file with the following code:</span></span>

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Data/WebApp1User.cs)]

<span data-ttu-id="32411-157">使用修饰属性， [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1)属性：</span><span class="sxs-lookup"><span data-stu-id="32411-157">Properties decorated with the [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1) attribute are:</span></span>

* <span data-ttu-id="32411-158">删除时*Areas/Identity/Pages/Account/Manage/DeletePersonalData.cshtml* Razor 页调用`UserManager.Delete`。</span><span class="sxs-lookup"><span data-stu-id="32411-158">Deleted when the *Areas/Identity/Pages/Account/Manage/DeletePersonalData.cshtml* Razor Page calls `UserManager.Delete`.</span></span>
* <span data-ttu-id="32411-159">包含在下载的数据通过*Areas/Identity/Pages/Account/Manage/DownloadPersonalData.cshtml* Razor 页。</span><span class="sxs-lookup"><span data-stu-id="32411-159">Included in the downloaded data by the *Areas/Identity/Pages/Account/Manage/DownloadPersonalData.cshtml* Razor Page.</span></span>

### <a name="update-the-accountmanageindexcshtml-page"></a><span data-ttu-id="32411-160">更新 Account/Manage/Index.cshtml 页</span><span class="sxs-lookup"><span data-stu-id="32411-160">Update the Account/Manage/Index.cshtml page</span></span>

<span data-ttu-id="32411-161">更新`InputModel`中*Areas/Identity/Pages/Account/Manage/Index.cshtml.cs*替换为以下突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="32411-161">Update the `InputModel` in *Areas/Identity/Pages/Account/Manage/Index.cshtml.cs* with the following highlighted code:</span></span>

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Pages/Account/Manage/Index.cshtml.cs?name=snippet&highlight=28-36,63-64,87-95,120)]

<span data-ttu-id="32411-162">更新*Areas/Identity/Pages/Account/Manage/Index.cshtml*替换为以下突出显示的标记：</span><span class="sxs-lookup"><span data-stu-id="32411-162">Update the *Areas/Identity/Pages/Account/Manage/Index.cshtml* with the following highlighted markup:</span></span>

[!code-html[Main](add-user-data/sample/Areas/Identity/Pages/Account/Manage/Index.cshtml?highlight=34-41)]

### <a name="update-the-accountregistercshtml-page"></a><span data-ttu-id="32411-163">更新 Account/Register.cshtml 页</span><span class="sxs-lookup"><span data-stu-id="32411-163">Update the Account/Register.cshtml page</span></span>

<span data-ttu-id="32411-164">更新`InputModel`中*Areas/Identity/Pages/Account/Register.cshtml.cs*替换为以下突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="32411-164">Update the `InputModel` in *Areas/Identity/Pages/Account/Register.cshtml.cs* with the following highlighted code:</span></span>

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Pages/Account/Register.cshtml.cs?name=snippet&highlight=8-16,43,44)]

<span data-ttu-id="32411-165">更新*Areas/Identity/Pages/Account/Register.cshtml*替换为以下突出显示的标记：</span><span class="sxs-lookup"><span data-stu-id="32411-165">Update the *Areas/Identity/Pages/Account/Register.cshtml* with the following highlighted markup:</span></span>

[!code-html[Main](add-user-data/sample/Areas/Identity/Pages/Account/Register.cshtml?highlight=16-25)]

<span data-ttu-id="32411-166">生成项目。</span><span class="sxs-lookup"><span data-stu-id="32411-166">Build the project.</span></span>

### <a name="add-a-migration-for-the-custom-user-data"></a><span data-ttu-id="32411-167">添加自定义用户数据的迁移</span><span class="sxs-lookup"><span data-stu-id="32411-167">Add a migration for the custom user data</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="32411-168">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32411-168">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="32411-169">在 Visual Studio**程序包管理器控制台**:</span><span class="sxs-lookup"><span data-stu-id="32411-169">In the Visual Studio **Package Manager Console**:</span></span>

```PMC
Add-Migration CustomUserData
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="32411-170">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="32411-170">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet ef migrations add CustomUserData
dotnet ef database update
```

------

## <a name="test-create-view-download-delete-custom-user-data"></a><span data-ttu-id="32411-171">测试创建、 查看、 下载、 删除自定义用户数据</span><span class="sxs-lookup"><span data-stu-id="32411-171">Test create, view, download, delete custom user data</span></span>

<span data-ttu-id="32411-172">测试应用：</span><span class="sxs-lookup"><span data-stu-id="32411-172">Test the app:</span></span>

* <span data-ttu-id="32411-173">注册新的用户。</span><span class="sxs-lookup"><span data-stu-id="32411-173">Register a new user.</span></span>
* <span data-ttu-id="32411-174">查看自定义用户数据`/Identity/Account/Manage`页。</span><span class="sxs-lookup"><span data-stu-id="32411-174">View the custom user data on the `/Identity/Account/Manage` page.</span></span>
* <span data-ttu-id="32411-175">下载并查看来自用户个人数据`/Identity/Account/Manage/PersonalData`页。</span><span class="sxs-lookup"><span data-stu-id="32411-175">Download and view the users personal data from the `/Identity/Account/Manage/PersonalData` page.</span></span>
