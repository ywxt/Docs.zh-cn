---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: 更改用户在 ASP.NET 标识中的主键 |Microsoft Docs
author: tfitzmac
description: 在 Visual Studio 2013 中，默认 web 应用程序使用的用户帐户的密钥的字符串值。 ASP.NET 标识，您可以更改的类型...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/30/2014
ms.topic: article
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.technology: ''
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 20e6b86f50a6ea62f188ae592e0b302c7ef77177
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37373323"
---
<a name="change-primary-key-for-users-in-aspnet-identity"></a>更改用户在 ASP.NET 标识中的主键
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 在 Visual Studio 2013 中，默认 web 应用程序使用的用户帐户的密钥的字符串值。 ASP.NET 标识，可更改以满足您的数据要求的键的类型。 例如，可以更改从字符串的键类型为整数。
> 
> 本主题说明如何开始使用默认的 web 应用程序并将用户帐户密钥更改为整数。 可以使用相同的修改以在项目中实现任何类型的密钥。 它演示了如何在默认 web 应用程序中进行这些更改，但您可以应用到自定义应用程序类似的修改。 它显示了在使用 MVC 或 Web 窗体时需要的更改。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - Visual Studio 2013 Update 2 （或更高版本）
> - ASP.NET 标识 2.1 或更高版本


若要在本教程中执行的步骤，必须具有 Visual Studio 2013 Update 2 （或更高版本），并从 ASP.NET Web 应用程序模板创建的 web 应用程序。 在 Update 3 中发生更改的模板。 本主题演示如何更改在 Update 2 和 Update 3 中的模板。

本主题包含以下各节：

- [更改标识用户类中的键的类型](#userclass)
- [添加使用键类型的自定义的标识类](#customclass)
- [更改的上下文类和用户管理器使用的密钥类型](#context)
- [更改启动配置以使用密钥类型](#startup)
- [对于 MVC Update 2 中，更改 AccountController 来传递密钥类型](#mvcupdate2)
- [对于 MVC Update 3 中，更改 AccountController 和 ManageController 传递密钥类型](#mvcupdate3)
- [对于 Update 2 的 Web 窗体，更改帐户页面传递密钥类型](#webformsupdate2)
- [对于 Update 3 的 Web 窗体，更改帐户页面传递密钥类型](#webformsupdate3)
- [运行应用程序](#run)
- [其他资源](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a>更改标识用户类中的键的类型

在 ASP.NET Web 应用程序模板创建的项目中，指定 ApplicationUser 类将一个整数，用于用户帐户的密钥。 在 IdentityModels.cs，更改 ApplicationUser 类继承的类型为 IdentityUser **int** TKey 泛型形参。 你还传递其尚未实现三个自定义类的名称。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

已更改的密钥类型，但默认情况下，应用程序的其余部分仍假定该密钥是一个字符串。 您必须显式指示假定字符串的代码中的密钥的类型。

在中**ApplicationUser**类中，更改**GenerateUserIdentityAsync**方法以包括 int，如以下突出显示的代码中所示。 此更改不需要为 Web 窗体项目中使用 Update 3 模板。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a>添加使用键类型的自定义的标识类

其他标识类，如 IdentityUserRole、 IdentityUserClaim、 IdentityUserLogin、 IdentityRole、 UserStore、 RoleStore，要仍设置为使用字符串键。 创建指定键的一个整数这些类的新版本。 不需要提供这些类中的实现代码，主要是只需设置 int 作为键。

将以下类添加到 IdentityModels.cs 文件。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a>更改的上下文类和用户管理器使用的密钥类型

在 IdentityModels.cs，更改的定义**ApplicationDbContext**类，以使用新自定义类和一个**int**中突出显示的代码所示的键。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

ThrowIfV1Schema 参数不再有效的构造函数中。 更改构造函数，因此它未通过 ThrowIfV1Schema 值。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

打开 IdentityConfig.cs，并将更改**ApplicationUserManger**类，以使用新用户存储保留数据的类和一个**int**键。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

在 Update 3 模板中，则必须更改 ApplicationSignInManager 类。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a>更改启动配置以使用密钥类型

在 Startup.Auth.cs，替换 OnValidateIdentity 代码，为以下突出显示部分。 请注意，getUserIdCallback 定义中，将字符串值分析为整数。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

如果你的项目无法识别的通用实现**GetUserId**方法，您可能需要的 ASP.NET 标识 NuGet 包更新到版本 2.1

对使用 ASP.NET 标识的基础结构类做了大量的更改。 如果您尝试编译项目，您将注意到了很多错误。 幸运的是，剩余的错误的所有类似。 标识类需要一个整数的键，但控制器 （或 Web 窗体） 在传递字符串值。 在每种情况下，您需要通过调用转换为字符串和整数**GetUserId&lt;int&gt;**。 可以通过从编译错误列表，也可以按照以下更改。

剩余的更改取决于你要创建并且已安装 Visual Studio 中的哪种更新的项目的类型。 您可以直接转到相关部分通过以下链接

- [对于 MVC Update 2 中，更改 AccountController 来传递密钥类型](#mvcupdate2)
- [对于 MVC Update 3 中，更改 AccountController 和 ManageController 传递密钥类型](#mvcupdate3)
- [对于 Update 2 的 Web 窗体，更改帐户页面传递密钥类型](#webformsupdate2)
- [对于 Update 3 的 Web 窗体，更改帐户页面传递密钥类型](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a>对于 MVC Update 2 中，更改 AccountController 来传递密钥类型

打开 AccountController.cs 文件。 您需要更改以下方法。

**ConfirmEmail**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

**取消关联**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

**Manage(ManageUserViewModel)** 方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

**LinkLoginCallback**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

**RemoveAccountList**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

**HasPassword**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

现在可以[运行应用程序](#run)并注册一个新用户。

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a>对于 MVC Update 3 中，更改 AccountController 和 ManageController 传递密钥类型

打开 AccountController.cs 文件。 您需要更改下面的方法。

**ConfirmEmail**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

**SendCode**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

打开 ManageController.cs 文件。 您需要更改以下方法。

**索引**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

**RemoveLogin**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

**AddPhoneNumber**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

**EnableTwoFactorAuthentication**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

**DisableTwoFactorAuthentication**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

**VerifyPhoneNumber**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

**RemovePhoneNumber**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

**ChangePassword**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

**SetPassword**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

**ManageLogins**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

**LinkLoginCallback**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

**HasPassword**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

**HasPhoneNumber**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

现在可以[运行应用程序](#run)并注册一个新用户。

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a>对于 Update 2 的 Web 窗体，更改帐户页面传递密钥类型

对于 Update 2 的 Web 窗体，您需要更改的以下页面。

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

现在可以[运行应用程序](#run)并注册一个新用户。

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a>对于 Update 3 的 Web 窗体，更改帐户页面传递密钥类型

对于 Update 3 的 Web 窗体，您需要更改的以下页面。

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

**VerifyPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

**AddPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

**ManagePassword.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

**ManageLogins.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

**TwoFactorAuthenticationSignIn.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a>运行应用程序

你已完成所有对默认 Web 应用程序模板所需的更改。 运行应用程序并注册一个新用户。 注册用户之后，您将注意到 AspNetUsers 表已是一个整数 Id 列。

![新的主密钥](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

如果你之前已创建 ASP.NET 标识的表使用不同的主要密钥，你需要进行一些其他更改。 如果可能，只需删除现有数据库。 运行 web 应用程序并添加新用户时，数据库将使用正确的设计重新创建。 如果删除操作不可能，运行代码优先迁移来更改表。 但是，新的整数主键将不会将设置为在数据库中的 SQL 标识属性。 作为标识，必须手动设置 Id 列。

<a id="other"></a>
## <a name="other-resources"></a>其他资源

- [ASP.NET 标识的自定义存储提供程序概述](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [将现有网站从 SQL 成员身份迁移到 ASP.NET 标识](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [成员身份和用户配置文件到 ASP.NET 标识的通用提供程序数据迁移](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- [示例应用程序](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/ChangePK/readme.txt)具有已更改主键
