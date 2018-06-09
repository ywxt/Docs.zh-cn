---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: 更改为在 ASP.NET Identity 中的用户的主要密钥 |Microsoft 文档
author: tfitzmac
description: 在 Visual Studio 2013 中，默认 web 应用程序使用用户帐户的密钥的字符串值。 ASP.NET 标识使你能够更改的一种...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/30/2014
ms.topic: article
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 79812efb4de2461fad3765d6005bbd20393e62b2
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "26498226"
---
<a name="change-primary-key-for-users-in-aspnet-identity"></a><span data-ttu-id="15a68-104">更改主键在 ASP.NET Identity 中的用户</span><span class="sxs-lookup"><span data-stu-id="15a68-104">Change Primary Key for Users in ASP.NET Identity</span></span>
====================
<span data-ttu-id="15a68-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="15a68-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="15a68-106">在 Visual Studio 2013 中，默认 web 应用程序使用用户帐户的密钥的字符串值。</span><span class="sxs-lookup"><span data-stu-id="15a68-106">In Visual Studio 2013, the default web application uses a string value for the key for user accounts.</span></span> <span data-ttu-id="15a68-107">ASP.NET 标识可以更改键以满足你的数据要求的类型。</span><span class="sxs-lookup"><span data-stu-id="15a68-107">ASP.NET Identity enables you to change the type of the key to meet your data requirements.</span></span> <span data-ttu-id="15a68-108">例如，可以更改从字符串键的类型为整数。</span><span class="sxs-lookup"><span data-stu-id="15a68-108">For example, you can change the type of the key from a string to an integer.</span></span>
> 
> <span data-ttu-id="15a68-109">本主题说明如何开始时使用默认 web 应用程序，并将用户帐户密钥更改为整数。</span><span class="sxs-lookup"><span data-stu-id="15a68-109">This topic shows how to start with the default web application and change the user account key to an integer.</span></span> <span data-ttu-id="15a68-110">可以使用相同的修改要在你的项目中实现任何类型的密钥。</span><span class="sxs-lookup"><span data-stu-id="15a68-110">You can use the same modifications to implement any type of key in your project.</span></span> <span data-ttu-id="15a68-111">它演示如何在默认 web 应用程序中进行这些更改，但你无法应用到自定义应用程序类似的修改。</span><span class="sxs-lookup"><span data-stu-id="15a68-111">It shows how to make these changes in the default web application, but you could apply similar modifications to a customized application.</span></span> <span data-ttu-id="15a68-112">它显示当使用 MVC 或 Web 窗体时需要的更改。</span><span class="sxs-lookup"><span data-stu-id="15a68-112">It shows the changes needed when working with MVC or Web Forms.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="15a68-113">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="15a68-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="15a68-114">Visual Studio 2013 Update 2 （或更高版本）</span><span class="sxs-lookup"><span data-stu-id="15a68-114">Visual Studio 2013 with Update 2 (or later)</span></span>
> - <span data-ttu-id="15a68-115">ASP.NET 标识 2.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="15a68-115">ASP.NET Identity 2.1 or later</span></span>


<span data-ttu-id="15a68-116">若要执行的步骤在本教程中，必须具有 Visual Studio 2013 Update 2 （或更高版本），并从 ASP.NET Web 应用程序模板创建的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="15a68-116">To perform the steps in this tutorial, you must have Visual Studio 2013 Update 2 (or later), and a web application created from the ASP.NET Web Application template.</span></span> <span data-ttu-id="15a68-117">在 Update 3 中更改模板。</span><span class="sxs-lookup"><span data-stu-id="15a68-117">The template changed in Update 3.</span></span> <span data-ttu-id="15a68-118">本主题说明如何更改 Update 2 和 Update 3 中的模板。</span><span class="sxs-lookup"><span data-stu-id="15a68-118">This topic shows how to change the template in Update 2 and Update 3.</span></span>

<span data-ttu-id="15a68-119">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="15a68-119">This topic contains the following sections:</span></span>

- [<span data-ttu-id="15a68-120">更改标识用户类中的键的类型</span><span class="sxs-lookup"><span data-stu-id="15a68-120">Change the type of the key in the Identity user class</span></span>](#userclass)
- [<span data-ttu-id="15a68-121">添加使用键类型的自定义的标识类</span><span class="sxs-lookup"><span data-stu-id="15a68-121">Add customized Identity classes that use the key type</span></span>](#customclass)
- [<span data-ttu-id="15a68-122">更改的上下文类和用户管理器使用的键类型</span><span class="sxs-lookup"><span data-stu-id="15a68-122">Change the context class and user manager to use the key type</span></span>](#context)
- [<span data-ttu-id="15a68-123">要使用的键类型的更改启动配置</span><span class="sxs-lookup"><span data-stu-id="15a68-123">Change start-up configuration to use the key type</span></span>](#startup)
- [<span data-ttu-id="15a68-124">对于 MVC Update 2 中，更改 AccountController 中传递的键类型</span><span class="sxs-lookup"><span data-stu-id="15a68-124">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="15a68-125">对于 MVC Update 3 中，更改 AccountController 并 ManageController 传递的键类型</span><span class="sxs-lookup"><span data-stu-id="15a68-125">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="15a68-126">对于带 Update 2 的 Web 窗体，更改帐户页面以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="15a68-126">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="15a68-127">对于带更新 3 的 Web 窗体，更改帐户页面以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="15a68-127">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)
- [<span data-ttu-id="15a68-128">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="15a68-128">Run application</span></span>](#run)
- [<span data-ttu-id="15a68-129">其他资源</span><span class="sxs-lookup"><span data-stu-id="15a68-129">Other resources</span></span>](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a><span data-ttu-id="15a68-130">更改标识用户类中的键的类型</span><span class="sxs-lookup"><span data-stu-id="15a68-130">Change the type of the key in the Identity user class</span></span>

<span data-ttu-id="15a68-131">在 ASP.NET Web 应用程序模板创建的项目中，指定 ApplicationUser 类将用于用户帐户的密钥的一个整数。</span><span class="sxs-lookup"><span data-stu-id="15a68-131">In your project created from the ASP.NET Web Application template, specify that the ApplicationUser class uses an integer for the key for user accounts.</span></span> <span data-ttu-id="15a68-132">在 IdentityModels.cs，更改 ApplicationUser 类继承的类型为 IdentityUser **int**为 TKey 泛型参数。</span><span class="sxs-lookup"><span data-stu-id="15a68-132">In IdentityModels.cs, change the ApplicationUser class to inherit from IdentityUser that has a type of **int** for the TKey generic parameter.</span></span> <span data-ttu-id="15a68-133">你还传递的三个自定义类，该类尚未实现的名称。</span><span class="sxs-lookup"><span data-stu-id="15a68-133">You also pass the names of three customized class which you have not implemented yet.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

<span data-ttu-id="15a68-134">您已更改的键的类型，但默认情况下，应用程序的其余部分仍假定密钥是一个字符串。</span><span class="sxs-lookup"><span data-stu-id="15a68-134">You have changed the type of the key, but, by default, the rest of the application still assumes the key is a string.</span></span> <span data-ttu-id="15a68-135">你必须显式指示假定字符串的代码中的键的类型。</span><span class="sxs-lookup"><span data-stu-id="15a68-135">You must explicitly indicate the type of the key in code that assumes a string.</span></span>

<span data-ttu-id="15a68-136">在**ApplicationUser**类中，更改**GenerateUserIdentityAsync**方法以包括 int，如下面的突出显示代码中所示。</span><span class="sxs-lookup"><span data-stu-id="15a68-136">In the **ApplicationUser** class, change the **GenerateUserIdentityAsync** method to include int, as shown in the highlighted code below.</span></span> <span data-ttu-id="15a68-137">此更改不需要对于具有 Update 3 模板的 Web 窗体项目。</span><span class="sxs-lookup"><span data-stu-id="15a68-137">This change is not necessary for Web Forms projects with the Update 3 template.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a><span data-ttu-id="15a68-138">添加使用键类型的自定义的标识类</span><span class="sxs-lookup"><span data-stu-id="15a68-138">Add customized Identity classes that use the key type</span></span>

<span data-ttu-id="15a68-139">其他标识类，如 IdentityUserRole、 IdentityUserClaim、 IdentityUserLogin、 IdentityRole、 UserStore、 RoleStore，要仍设置为使用字符串密钥。</span><span class="sxs-lookup"><span data-stu-id="15a68-139">The other Identity classes, such as IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, are still set up to use a string key.</span></span> <span data-ttu-id="15a68-140">创建指定键的一个整数这些类的新的版本。</span><span class="sxs-lookup"><span data-stu-id="15a68-140">Create new versions of these classes that specify an integer for the key.</span></span> <span data-ttu-id="15a68-141">不需要提供这些类中的多实现代码，你主要只通过以下方式设置 int 作为键。</span><span class="sxs-lookup"><span data-stu-id="15a68-141">You do not need to provide much implementation code in these classes, you are primarily just setting int as the key.</span></span>

<span data-ttu-id="15a68-142">将以下类添加到你 IdentityModels.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="15a68-142">Add the following classes to your IdentityModels.cs file.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a><span data-ttu-id="15a68-143">更改的上下文类和用户管理器使用的键类型</span><span class="sxs-lookup"><span data-stu-id="15a68-143">Change the context class and user manager to use the key type</span></span>

<span data-ttu-id="15a68-144">在 IdentityModels.cs，更改的定义**ApplicationDbContext**类以使用新自定义类和**int**的键，如突出显示的代码中所示。</span><span class="sxs-lookup"><span data-stu-id="15a68-144">In IdentityModels.cs, change the definition of the **ApplicationDbContext** class to use your new customized classes and an **int** for the key, as shown in the highlighted code.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

<span data-ttu-id="15a68-145">ThrowIfV1Schema 参数不再在构造函数中有效。</span><span class="sxs-lookup"><span data-stu-id="15a68-145">The ThrowIfV1Schema parameter is no longer valid in the constructor.</span></span> <span data-ttu-id="15a68-146">更改构造函数，因此未通过 ThrowIfV1Schema 值。</span><span class="sxs-lookup"><span data-stu-id="15a68-146">Change the constructor so it does not pass a ThrowIfV1Schema value.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

<span data-ttu-id="15a68-147">打开 IdentityConfig.cs，并将更改**ApplicationUserManger**类以使用你的新用户存储保留数据的类和**int**键。</span><span class="sxs-lookup"><span data-stu-id="15a68-147">Open IdentityConfig.cs, and change the **ApplicationUserManger** class to use your new user store class for persisting data and an **int** for the key.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

<span data-ttu-id="15a68-148">在 Update 3 模板中，你必须更改 ApplicationSignInManager 类。</span><span class="sxs-lookup"><span data-stu-id="15a68-148">In the Update 3 template, you must change the ApplicationSignInManager class.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a><span data-ttu-id="15a68-149">要使用的键类型的更改启动配置</span><span class="sxs-lookup"><span data-stu-id="15a68-149">Change start-up configuration to use the key type</span></span>

<span data-ttu-id="15a68-150">在 Startup.Auth.cs，替换 OnValidateIdentity 代码，则为以下突出显示部分。</span><span class="sxs-lookup"><span data-stu-id="15a68-150">In Startup.Auth.cs, replace the OnValidateIdentity code, as highlighted below.</span></span> <span data-ttu-id="15a68-151">请注意 getUserIdCallback 定义中，将字符串值分析为整数。</span><span class="sxs-lookup"><span data-stu-id="15a68-151">Notice that the getUserIdCallback definition, parses the string value into an integer.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

<span data-ttu-id="15a68-152">如果你的项目无法识别的通用实现**GetUserId**方法，你可能需要更新到版本 2.1 ASP.NET 标识 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="15a68-152">If your project does not recognize the generic implementation of the **GetUserId** method, you may need to update the ASP.NET Identity NuGet package to version 2.1</span></span>

<span data-ttu-id="15a68-153">您已经更改了大量使用 ASP.NET 标识的基础结构类。</span><span class="sxs-lookup"><span data-stu-id="15a68-153">You have made a lot of changes to the infrastructure classes used by ASP.NET Identity.</span></span> <span data-ttu-id="15a68-154">如果你尝试编译该项目，你将注意到了很多错误。</span><span class="sxs-lookup"><span data-stu-id="15a68-154">If you try compiling the project, you will notice a lot of errors.</span></span> <span data-ttu-id="15a68-155">幸运的是，剩余的错误是所有类似。</span><span class="sxs-lookup"><span data-stu-id="15a68-155">Fortunately, the remaining errors are all similar.</span></span> <span data-ttu-id="15a68-156">标识类需要整数的键，但需要的控制器 （或 Web 窗体） 传递一个字符串值。</span><span class="sxs-lookup"><span data-stu-id="15a68-156">The Identity class expects an integer for the key, but the controller (or Web Form) is passing a string value.</span></span> <span data-ttu-id="15a68-157">在每种情况下，你需要通过调用从一个字符串和整数转换**GetUserId&lt;int&gt;**。</span><span class="sxs-lookup"><span data-stu-id="15a68-157">In each case, you need to convert from a string to and integer by calling **GetUserId&lt;int&gt;**.</span></span> <span data-ttu-id="15a68-158">你可以通过编译错误列表处理，或按照下面的更改。</span><span class="sxs-lookup"><span data-stu-id="15a68-158">You can either work through the error list from compilation or follow the changes below.</span></span>

<span data-ttu-id="15a68-159">剩余的更改取决于你要创建并且已安装在 Visual Studio 中的哪种更新的项目的类型。</span><span class="sxs-lookup"><span data-stu-id="15a68-159">The remaining changes depend on the type of project you are creating and which update you have installed in Visual Studio.</span></span> <span data-ttu-id="15a68-160">你可以直接转到通过以下链接的相关部分</span><span class="sxs-lookup"><span data-stu-id="15a68-160">You can go directly to the relevant section through the following links</span></span>

- [<span data-ttu-id="15a68-161">对于 MVC Update 2 中，更改 AccountController 中传递的键类型</span><span class="sxs-lookup"><span data-stu-id="15a68-161">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="15a68-162">对于 MVC Update 3 中，更改 AccountController 并 ManageController 传递的键类型</span><span class="sxs-lookup"><span data-stu-id="15a68-162">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="15a68-163">对于带 Update 2 的 Web 窗体，更改帐户页面以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="15a68-163">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="15a68-164">对于带更新 3 的 Web 窗体，更改帐户页面以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="15a68-164">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a><span data-ttu-id="15a68-165">对于 MVC Update 2 中，更改 AccountController 中传递的键类型</span><span class="sxs-lookup"><span data-stu-id="15a68-165">For MVC with Update 2, change the AccountController to pass the key type</span></span>

<span data-ttu-id="15a68-166">打开 AccountController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="15a68-166">Open the AccountController.cs file.</span></span> <span data-ttu-id="15a68-167">你需要更改以下方法。</span><span class="sxs-lookup"><span data-stu-id="15a68-167">You need to change the following methods.</span></span>

<span data-ttu-id="15a68-168">**ConfirmEmail**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-168">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

<span data-ttu-id="15a68-169">**取消关联**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-169">**Disassociate** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

<span data-ttu-id="15a68-170">**Manage(ManageUserViewModel)** 方法</span><span class="sxs-lookup"><span data-stu-id="15a68-170">**Manage(ManageUserViewModel)** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

<span data-ttu-id="15a68-171">**LinkLoginCallback**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-171">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

<span data-ttu-id="15a68-172">**RemoveAccountList**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-172">**RemoveAccountList** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

<span data-ttu-id="15a68-173">**HasPassword**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-173">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

<span data-ttu-id="15a68-174">你现在可以[运行该应用程序](#run)并注册新的用户。</span><span class="sxs-lookup"><span data-stu-id="15a68-174">You can now [run the application](#run) and register a new user.</span></span>

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a><span data-ttu-id="15a68-175">对于 MVC Update 3 中，更改 AccountController 并 ManageController 传递的键类型</span><span class="sxs-lookup"><span data-stu-id="15a68-175">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>

<span data-ttu-id="15a68-176">打开 AccountController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="15a68-176">Open the AccountController.cs file.</span></span> <span data-ttu-id="15a68-177">你需要更改以下方法。</span><span class="sxs-lookup"><span data-stu-id="15a68-177">You need to change the following method.</span></span>

<span data-ttu-id="15a68-178">**ConfirmEmail**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-178">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

<span data-ttu-id="15a68-179">**SendCode**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-179">**SendCode** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

<span data-ttu-id="15a68-180">打开 ManageController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="15a68-180">Open the ManageController.cs file.</span></span> <span data-ttu-id="15a68-181">你需要更改以下方法。</span><span class="sxs-lookup"><span data-stu-id="15a68-181">You need to change the following methods.</span></span>

<span data-ttu-id="15a68-182">**索引**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-182">**Index** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

<span data-ttu-id="15a68-183">**RemoveLogin**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-183">**RemoveLogin** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

<span data-ttu-id="15a68-184">**AddPhoneNumber**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-184">**AddPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

<span data-ttu-id="15a68-185">**EnableTwoFactorAuthentication**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-185">**EnableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

<span data-ttu-id="15a68-186">**DisableTwoFactorAuthentication**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-186">**DisableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

<span data-ttu-id="15a68-187">**VerifyPhoneNumber**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-187">**VerifyPhoneNumber** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

<span data-ttu-id="15a68-188">**RemovePhoneNumber**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-188">**RemovePhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

<span data-ttu-id="15a68-189">**ChangePassword**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-189">**ChangePassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

<span data-ttu-id="15a68-190">**SetPassword**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-190">**SetPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

<span data-ttu-id="15a68-191">**ManageLogins**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-191">**ManageLogins** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

<span data-ttu-id="15a68-192">**LinkLoginCallback**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-192">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

<span data-ttu-id="15a68-193">**HasPassword**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-193">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

<span data-ttu-id="15a68-194">**HasPhoneNumber**方法</span><span class="sxs-lookup"><span data-stu-id="15a68-194">**HasPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

<span data-ttu-id="15a68-195">你现在可以[运行该应用程序](#run)并注册新的用户。</span><span class="sxs-lookup"><span data-stu-id="15a68-195">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="15a68-196">对于带 Update 2 的 Web 窗体，更改帐户页面以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="15a68-196">For Web Forms with Update 2, change Account pages to pass the key type</span></span>

<span data-ttu-id="15a68-197">对于带 Update 2 的 Web 窗体，你需要更改的以下页面。</span><span class="sxs-lookup"><span data-stu-id="15a68-197">For Web Forms with Update 2, you need to change the following pages.</span></span>

<span data-ttu-id="15a68-198">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="15a68-198">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

<span data-ttu-id="15a68-199">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="15a68-199">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

<span data-ttu-id="15a68-200">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="15a68-200">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

<span data-ttu-id="15a68-201">你现在可以[运行该应用程序](#run)并注册新的用户。</span><span class="sxs-lookup"><span data-stu-id="15a68-201">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="15a68-202">对于带更新 3 的 Web 窗体，更改帐户页面以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="15a68-202">For Web Forms with Update 3, change Account pages to pass the key type</span></span>

<span data-ttu-id="15a68-203">对于带更新 3 的 Web 窗体，你需要更改的以下页面。</span><span class="sxs-lookup"><span data-stu-id="15a68-203">For Web Forms with Update 3, you need to change the following pages.</span></span>

<span data-ttu-id="15a68-204">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="15a68-204">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

<span data-ttu-id="15a68-205">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="15a68-205">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

<span data-ttu-id="15a68-206">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="15a68-206">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

<span data-ttu-id="15a68-207">**VerifyPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="15a68-207">**VerifyPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

<span data-ttu-id="15a68-208">**AddPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="15a68-208">**AddPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

<span data-ttu-id="15a68-209">**ManagePassword.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="15a68-209">**ManagePassword.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

<span data-ttu-id="15a68-210">**ManageLogins.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="15a68-210">**ManageLogins.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

<span data-ttu-id="15a68-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="15a68-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a><span data-ttu-id="15a68-212">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="15a68-212">Run application</span></span>

<span data-ttu-id="15a68-213">你已完成所有到默认 Web 应用程序模板所需的更改。</span><span class="sxs-lookup"><span data-stu-id="15a68-213">You have finished all of the required changes to the default Web Application template.</span></span> <span data-ttu-id="15a68-214">运行应用程序并注册新的用户。</span><span class="sxs-lookup"><span data-stu-id="15a68-214">Run the application and register a new user.</span></span> <span data-ttu-id="15a68-215">注册用户之后，你将注意到 AspNetUsers 表具有是一个整数的 Id 列。</span><span class="sxs-lookup"><span data-stu-id="15a68-215">After registering the user, you will notice that the AspNetUsers table has an Id column that is an integer.</span></span>

![新的主密钥](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

<span data-ttu-id="15a68-217">如果你之前已创建 ASP.NET 标识表具有不同的主键值，你需要进行一些附加更改。</span><span class="sxs-lookup"><span data-stu-id="15a68-217">If you have previously created the ASP.NET Identity tables with a different primary key, you need to make some additional changes.</span></span> <span data-ttu-id="15a68-218">如果可能，只需删除现有数据库。</span><span class="sxs-lookup"><span data-stu-id="15a68-218">If possible, just delete the existing database.</span></span> <span data-ttu-id="15a68-219">运行 web 应用程序以及添加新用户时，将与正确设计重新创建该数据库。</span><span class="sxs-lookup"><span data-stu-id="15a68-219">The database will be re-created with the correct design when you run the web application and add a new user.</span></span> <span data-ttu-id="15a68-220">如果删除不可能，运行代码优先迁移来更改表。</span><span class="sxs-lookup"><span data-stu-id="15a68-220">If deletion is not possible, run code first migrations to change the tables.</span></span> <span data-ttu-id="15a68-221">但是，新整数主键将不会将设置为在数据库中的 SQL 标识属性。</span><span class="sxs-lookup"><span data-stu-id="15a68-221">However, the new integer primary key will not be set up as a SQL IDENTITY property in the database.</span></span> <span data-ttu-id="15a68-222">作为标识，必须手动设置 Id 列。</span><span class="sxs-lookup"><span data-stu-id="15a68-222">You must manually set the Id column as an IDENTITY.</span></span>

<a id="other"></a>
## <a name="other-resources"></a><span data-ttu-id="15a68-223">其他资源</span><span class="sxs-lookup"><span data-stu-id="15a68-223">Other resources</span></span>

- [<span data-ttu-id="15a68-224">ASP.NET 标识的自定义存储提供程序概述</span><span class="sxs-lookup"><span data-stu-id="15a68-224">Overview of Custom Storage Providers for ASP.NET Identity</span></span>](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [<span data-ttu-id="15a68-225">将现有网站从 SQL 成员身份迁移到 ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="15a68-225">Migrating an Existing Website from SQL Membership to ASP.NET Identity</span></span>](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [<span data-ttu-id="15a68-226">将通用提供程序的数据迁移的成员身份和到 ASP.NET 标识的用户配置文件</span><span class="sxs-lookup"><span data-stu-id="15a68-226">Migrating Universal Provider Data for Membership and User Profiles to ASP.NET Identity</span></span>](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- <span data-ttu-id="15a68-227">[示例应用程序](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/ChangePK/readme.txt)具有已更改的主关键字</span><span class="sxs-lookup"><span data-stu-id="15a68-227">[Sample application](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/ChangePK/readme.txt) with changed primary key</span></span>
