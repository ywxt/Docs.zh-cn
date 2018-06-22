---
title: 帐户确认和 ASP.NET Core 中的密码恢复
author: rick-anderson
description: 了解如何生成使用电子邮件确认及密码重置功能的 ASP.NET Core 应用程序。
ms.author: riande
ms.date: 2/11/2018
uid: security/authentication/accconfirm
ms.openlocfilehash: db41dd47518fa8b35c006b3291068e7724cf6cca
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275075"
---
# <a name="account-confirmation-and-password-recovery-in-aspnet-core"></a><span data-ttu-id="373a1-103">帐户确认和 ASP.NET Core 中的密码恢复</span><span class="sxs-lookup"><span data-stu-id="373a1-103">Account confirmation and password recovery in ASP.NET Core</span></span>

<span data-ttu-id="373a1-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Joe Audette](https://twitter.com/joeaudette)</span><span class="sxs-lookup"><span data-stu-id="373a1-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Joe Audette](https://twitter.com/joeaudette)</span></span>

<span data-ttu-id="373a1-105">本教程演示了如何生成具有电子邮件确认及密码重置的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="373a1-105">This tutorial shows you how to build an ASP.NET Core app with email confirmation and password reset.</span></span> <span data-ttu-id="373a1-106">本教程是**不**开头主题。</span><span class="sxs-lookup"><span data-stu-id="373a1-106">This tutorial is **not** a beginning topic.</span></span> <span data-ttu-id="373a1-107">你应熟悉：</span><span class="sxs-lookup"><span data-stu-id="373a1-107">You should be familiar with:</span></span>

* [<span data-ttu-id="373a1-108">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="373a1-108">ASP.NET Core</span></span>](xref:tutorials/first-mvc-app/start-mvc)
* [<span data-ttu-id="373a1-109">身份验证</span><span class="sxs-lookup"><span data-stu-id="373a1-109">Authentication</span></span>](xref:security/authentication/index)
* [<span data-ttu-id="373a1-110">帐户确认和密码恢复</span><span class="sxs-lookup"><span data-stu-id="373a1-110">Account Confirmation and Password Recovery</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="373a1-111">Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="373a1-111">Entity Framework Core</span></span>](xref:data/ef-mvc/intro)

<span data-ttu-id="373a1-112">请参阅[此 PDF 文件](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf)的 ASP.NET 核心 MVC 1.1 和 2.x 版本。</span><span class="sxs-lookup"><span data-stu-id="373a1-112">See [this PDF file](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf) for the ASP.NET Core MVC 1.1 and 2.x versions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="373a1-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="373a1-113">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs.md)]

## <a name="create-a-new-aspnet-core-project-with-the-net-core-cli"></a><span data-ttu-id="373a1-114">使用.NET 核心 CLI 创建新的 ASP.NET Core 项目</span><span class="sxs-lookup"><span data-stu-id="373a1-114">Create a new ASP.NET Core project with the .NET Core CLI</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="373a1-115">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="373a1-115">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new webapp --auth Individual -o WebPWrecover
cd WebPWrecover
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new razor --auth Individual -o WebPWrecover
cd WebPWrecover
```

::: moniker-end

* <span data-ttu-id="373a1-117">`--auth Individual` 指定的单个用户帐户项目模板。</span><span class="sxs-lookup"><span data-stu-id="373a1-117">`--auth Individual` specifies the Individual User Accounts project template.</span></span>
* <span data-ttu-id="373a1-118">在 Windows 上，添加`-uld`选项。</span><span class="sxs-lookup"><span data-stu-id="373a1-118">On Windows, add the `-uld` option.</span></span> <span data-ttu-id="373a1-119">它指定应而不是 SQLite 使用 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="373a1-119">It specifies LocalDB should be used instead of SQLite.</span></span>
* <span data-ttu-id="373a1-120">运行`new mvc --help`以获取有关此命令帮助。</span><span class="sxs-lookup"><span data-stu-id="373a1-120">Run `new mvc --help` to get help on this command.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="373a1-121">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="373a1-121">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="373a1-122">如果你使用 CLI 或 SQLite，运行以下命令在命令窗口中：</span><span class="sxs-lookup"><span data-stu-id="373a1-122">If you're using the CLI or SQLite, run the following in a command window:</span></span>

```console
dotnet new mvc --auth Individual
```

* <span data-ttu-id="373a1-123">`--auth Individual` 指定的单个用户帐户项目模板。</span><span class="sxs-lookup"><span data-stu-id="373a1-123">`--auth Individual` specifies the Individual User Accounts project template.</span></span>
* <span data-ttu-id="373a1-124">在 Windows 上，添加`-uld`选项。</span><span class="sxs-lookup"><span data-stu-id="373a1-124">On Windows, add the `-uld` option.</span></span> <span data-ttu-id="373a1-125">它指定应而不是 SQLite 使用 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="373a1-125">It specifies LocalDB should be used instead of SQLite.</span></span>
* <span data-ttu-id="373a1-126">运行`new mvc --help`以获取有关此命令帮助。</span><span class="sxs-lookup"><span data-stu-id="373a1-126">Run `new mvc --help` to get help on this command.</span></span>

---

<span data-ttu-id="373a1-127">或者，你可以使用 Visual Studio 创建新的 ASP.NET Core 项目：</span><span class="sxs-lookup"><span data-stu-id="373a1-127">Alternatively, you can create a new ASP.NET Core project with Visual Studio:</span></span>

* <span data-ttu-id="373a1-128">在 Visual Studio 中，创建一个新**Web 应用程序**项目。</span><span class="sxs-lookup"><span data-stu-id="373a1-128">In Visual Studio, create a new **Web Application** project.</span></span>
* <span data-ttu-id="373a1-129">选择**ASP.NET Core 2.0**。</span><span class="sxs-lookup"><span data-stu-id="373a1-129">Select **ASP.NET Core 2.0**.</span></span> <span data-ttu-id="373a1-130">**.NET 核心**选择在下图中，但你可以选择 **.NET Framework**。</span><span class="sxs-lookup"><span data-stu-id="373a1-130">**.NET Core** is selected in the following image, but you can select **.NET Framework**.</span></span>
* <span data-ttu-id="373a1-131">选择**更改身份验证**并将设置为**单个用户帐户**。</span><span class="sxs-lookup"><span data-stu-id="373a1-131">Select **Change Authentication** and set to **Individual User Accounts**.</span></span>
* <span data-ttu-id="373a1-132">保留默认值**存储用户帐户在应用程序**。</span><span class="sxs-lookup"><span data-stu-id="373a1-132">Keep the default **Store user accounts in-app**.</span></span>

![显示"单个用户帐户单选"所选的新建项目对话框](accconfirm/_static/2.png)

## <a name="test-new-user-registration"></a><span data-ttu-id="373a1-134">测试新的用户注册</span><span class="sxs-lookup"><span data-stu-id="373a1-134">Test new user registration</span></span>

<span data-ttu-id="373a1-135">运行应用程序中，选择**注册**链接，并注册用户。</span><span class="sxs-lookup"><span data-stu-id="373a1-135">Run the app, select the **Register** link, and register a user.</span></span> <span data-ttu-id="373a1-136">按照运行实体框架核心迁移的说明。</span><span class="sxs-lookup"><span data-stu-id="373a1-136">Follow the instructions to run Entity Framework Core migrations.</span></span> <span data-ttu-id="373a1-137">此时，电子邮件的唯一验证是使用[[EmailAddress]](/dotnet/api/system.componentmodel.dataannotations.emailaddressattribute)属性。</span><span class="sxs-lookup"><span data-stu-id="373a1-137">At this point, the only validation on the email is with the [[EmailAddress]](/dotnet/api/system.componentmodel.dataannotations.emailaddressattribute) attribute.</span></span> <span data-ttu-id="373a1-138">提交注册之后, 你登录到应用程序。</span><span class="sxs-lookup"><span data-stu-id="373a1-138">After submitting the registration, you are logged into the app.</span></span> <span data-ttu-id="373a1-139">更高版本在教程中，这样，直到其电子邮件已验证新的用户无法登录时将更新代码。</span><span class="sxs-lookup"><span data-stu-id="373a1-139">Later in the tutorial, the code is updated so new users can't log in until their email has been validated.</span></span>

## <a name="view-the-identity-database"></a><span data-ttu-id="373a1-140">查看标识数据库</span><span class="sxs-lookup"><span data-stu-id="373a1-140">View the Identity database</span></span>

<span data-ttu-id="373a1-141">请参阅[ASP.NET 核心 MVC 项目中使用的 SQLite](xref:tutorials/first-mvc-app-xplat/working-with-sql)有关说明如何查看 SQLite 数据库。</span><span class="sxs-lookup"><span data-stu-id="373a1-141">See [Work with SQLite in an ASP.NET Core MVC project](xref:tutorials/first-mvc-app-xplat/working-with-sql) for instructions on how to view the SQLite database.</span></span>

<span data-ttu-id="373a1-142">Visual studio:</span><span class="sxs-lookup"><span data-stu-id="373a1-142">For Visual Studio:</span></span>

* <span data-ttu-id="373a1-143">从**视图**菜单上，选择**SQL Server 对象资源管理器**(SSOX)。</span><span class="sxs-lookup"><span data-stu-id="373a1-143">From the **View** menu, select **SQL Server Object Explorer** (SSOX).</span></span>
* <span data-ttu-id="373a1-144">导航到 **(localdb) MSSQLLocalDB (SQL Server 13)**。</span><span class="sxs-lookup"><span data-stu-id="373a1-144">Navigate to **(localdb)MSSQLLocalDB(SQL Server 13)**.</span></span> <span data-ttu-id="373a1-145">右键单击**dbo。AspNetUsers** > **查看数据**:</span><span class="sxs-lookup"><span data-stu-id="373a1-145">Right-click on **dbo.AspNetUsers** > **View Data**:</span></span>

![在 AspNetUsers 表中 SQL Server 对象资源管理器的上下文菜单](accconfirm/_static/ssox.png)

<span data-ttu-id="373a1-147">请注意表的`EmailConfirmed`字段是`False`。</span><span class="sxs-lookup"><span data-stu-id="373a1-147">Note the table's `EmailConfirmed` field is `False`.</span></span>

<span data-ttu-id="373a1-148">你可能想要再次在下一步中使用此电子邮件，当应用程序发送确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="373a1-148">You might want to use this email again in the next step when the app sends a confirmation email.</span></span> <span data-ttu-id="373a1-149">右键单击行并选择**删除**。</span><span class="sxs-lookup"><span data-stu-id="373a1-149">Right-click on the row and select **Delete**.</span></span> <span data-ttu-id="373a1-150">删除的电子邮件别名便于您在以下步骤。</span><span class="sxs-lookup"><span data-stu-id="373a1-150">Deleting the email alias makes it easier in the following steps.</span></span>

---

## <a name="require-https"></a><span data-ttu-id="373a1-151">需要 HTTPS</span><span class="sxs-lookup"><span data-stu-id="373a1-151">Require HTTPS</span></span>

<span data-ttu-id="373a1-152">请参阅[需要 HTTPS](xref:security/enforcing-ssl)。</span><span class="sxs-lookup"><span data-stu-id="373a1-152">See [Require HTTPS](xref:security/enforcing-ssl).</span></span>

<a name="prevent-login-at-registration"></a>
## <a name="require-email-confirmation"></a><span data-ttu-id="373a1-153">需要电子邮件确认</span><span class="sxs-lookup"><span data-stu-id="373a1-153">Require email confirmation</span></span>

<span data-ttu-id="373a1-154">它是一种最佳做法以确认新的用户注册的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="373a1-154">It's a best practice to confirm the email of a new user registration.</span></span> <span data-ttu-id="373a1-155">电子邮件确认有助于验证它们不模拟其他人 （即，它们尚未注册与其他人的电子邮件）。</span><span class="sxs-lookup"><span data-stu-id="373a1-155">Email confirmation helps to verify they're not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="373a1-156">假设有论坛，并且你想阻止"yli@example.com"发件人将注册为"nolivetto@contoso.com"。</span><span class="sxs-lookup"><span data-stu-id="373a1-156">Suppose you had a discussion forum, and you wanted to prevent "yli@example.com" from registering as "nolivetto@contoso.com".</span></span> <span data-ttu-id="373a1-157">而无需电子邮件确认"nolivetto@contoso.com"无法接收来自您的应用程序不需要的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="373a1-157">Without email confirmation, "nolivetto@contoso.com" could receive unwanted email from your app.</span></span> <span data-ttu-id="373a1-158">假设用户意外注册为"ylo@example.com"和未注意到"yli"的拼写错误。</span><span class="sxs-lookup"><span data-stu-id="373a1-158">Suppose the user accidentally registered as "ylo@example.com" and hadn't noticed the misspelling of "yli".</span></span> <span data-ttu-id="373a1-159">它们将无法使用恢复密码，因为此应用程序没有正确的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="373a1-159">They wouldn't be able to use password recovery because the app doesn't have their correct email.</span></span> <span data-ttu-id="373a1-160">电子邮件确认从机器人提供有限的保护。</span><span class="sxs-lookup"><span data-stu-id="373a1-160">Email confirmation provides only limited protection from bots.</span></span> <span data-ttu-id="373a1-161">电子邮件确认不免受恶意用户的多个电子邮件帐户与提供保护。</span><span class="sxs-lookup"><span data-stu-id="373a1-161">Email confirmation doesn't provide protection from malicious users with many email accounts.</span></span>

<span data-ttu-id="373a1-162">你通常想要使不能在有确认电子邮件之前发布到网站的任何数据的新用户。</span><span class="sxs-lookup"><span data-stu-id="373a1-162">You generally want to prevent new users from posting any data to your web site before they have a confirmed email.</span></span>

<span data-ttu-id="373a1-163">更新`ConfigureServices`需要确认电子邮件：</span><span class="sxs-lookup"><span data-stu-id="373a1-163">Update `ConfigureServices` to require a confirmed email:</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover/Startup.cs?name=snippet1&highlight=12-17)]

<span data-ttu-id="373a1-164">`config.SignIn.RequireConfirmedEmail = true;` 防止已注册的用户登录，直到其电子邮件进行确认。</span><span class="sxs-lookup"><span data-stu-id="373a1-164">`config.SignIn.RequireConfirmedEmail = true;` prevents registered users from logging in until their email is confirmed.</span></span>

### <a name="configure-email-provider"></a><span data-ttu-id="373a1-165">配置电子邮件提供商</span><span class="sxs-lookup"><span data-stu-id="373a1-165">Configure email provider</span></span>

<span data-ttu-id="373a1-166">在本教程中，使用 SendGrid 发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="373a1-166">In this tutorial, SendGrid is used to send email.</span></span> <span data-ttu-id="373a1-167">你需要一个 SendGrid 帐户和密钥用于发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="373a1-167">You need a SendGrid account and key to send email.</span></span> <span data-ttu-id="373a1-168">你可以使用其他电子邮件提供商。</span><span class="sxs-lookup"><span data-stu-id="373a1-168">You can use other email providers.</span></span> <span data-ttu-id="373a1-169">ASP.NET 核心 2.x 包括`System.Net.Mail`，这允许你从你的应用程序发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="373a1-169">ASP.NET Core 2.x includes `System.Net.Mail`, which allows you to send email from your app.</span></span> <span data-ttu-id="373a1-170">我们建议你使用 SendGrid 或另一个电子邮件服务发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="373a1-170">We recommend you use SendGrid or another email service to send email.</span></span> <span data-ttu-id="373a1-171">SMTP 很难保护并正确设置。</span><span class="sxs-lookup"><span data-stu-id="373a1-171">SMTP is difficult to secure and set up correctly.</span></span>

<span data-ttu-id="373a1-172">[选项模式](xref:fundamentals/configuration/options)用于访问的用户帐户和密钥设置。</span><span class="sxs-lookup"><span data-stu-id="373a1-172">The [Options pattern](xref:fundamentals/configuration/options) is used to access the user account and key settings.</span></span> <span data-ttu-id="373a1-173">有关详细信息，请参阅[配置](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="373a1-173">For more information, see [configuration](xref:fundamentals/configuration/index).</span></span>

<span data-ttu-id="373a1-174">创建一个类以提取安全的电子邮件密钥。</span><span class="sxs-lookup"><span data-stu-id="373a1-174">Create a class to fetch the secure email key.</span></span> <span data-ttu-id="373a1-175">对于此示例，`AuthMessageSenderOptions`中创建类*Services/AuthMessageSenderOptions.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="373a1-175">For this sample, the `AuthMessageSenderOptions` class is created in the *Services/AuthMessageSenderOptions.cs* file:</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover/Services/AuthMessageSenderOptions.cs?name=snippet1)]

<span data-ttu-id="373a1-176">设置`SendGridUser`和`SendGridKey`与[机密管理器工具](xref:security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="373a1-176">Set the `SendGridUser` and `SendGridKey` with the [secret-manager tool](xref:security/app-secrets).</span></span> <span data-ttu-id="373a1-177">例如：</span><span class="sxs-lookup"><span data-stu-id="373a1-177">For example:</span></span>

```console
C:\WebAppl\src\WebApp1>dotnet user-secrets set SendGridUser RickAndMSFT
info: Successfully saved SendGridUser = RickAndMSFT to the secret store.
```

<span data-ttu-id="373a1-178">在 Windows 上，密钥管理器存储中的键/值对*secrets.json*文件中`%APPDATA%/Microsoft/UserSecrets/<WebAppName-userSecretsId>`目录。</span><span class="sxs-lookup"><span data-stu-id="373a1-178">On Windows, Secret Manager stores keys/value pairs in a *secrets.json* file in the `%APPDATA%/Microsoft/UserSecrets/<WebAppName-userSecretsId>` directory.</span></span>

<span data-ttu-id="373a1-179">内容*secrets.json*文件未加密。</span><span class="sxs-lookup"><span data-stu-id="373a1-179">The contents of the *secrets.json* file aren't encrypted.</span></span> <span data-ttu-id="373a1-180">*Secrets.json*文件如下所示 (`SendGridKey`值已删除。)</span><span class="sxs-lookup"><span data-stu-id="373a1-180">The *secrets.json* file is shown below (the `SendGridKey` value has been removed.)</span></span>

 ```json
  {
    "SendGridUser": "RickAndMSFT",
    "SendGridKey": "<key removed>"
  }
  ```

### <a name="configure-startup-to-use-authmessagesenderoptions"></a><span data-ttu-id="373a1-181">配置启动要使用 AuthMessageSenderOptions</span><span class="sxs-lookup"><span data-stu-id="373a1-181">Configure startup to use AuthMessageSenderOptions</span></span>

<span data-ttu-id="373a1-182">添加`AuthMessageSenderOptions`到末尾的服务容器`ConfigureServices`中的方法*Startup.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="373a1-182">Add `AuthMessageSenderOptions` to the service container at the end of the `ConfigureServices` method in the *Startup.cs* file:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="373a1-183">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="373a1-183">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](accconfirm/sample/WebPWrecover/Startup.cs?name=snippet2&highlight=28)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="373a1-184">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="373a1-184">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](accconfirm/sample/WebApp1/Startup.cs?name=snippet1&highlight=26)]

---

### <a name="configure-the-authmessagesender-class"></a><span data-ttu-id="373a1-185">配置 AuthMessageSender 类</span><span class="sxs-lookup"><span data-stu-id="373a1-185">Configure the AuthMessageSender class</span></span>

<span data-ttu-id="373a1-186">本教程演示如何添加通过电子邮件通知[SendGrid](https://sendgrid.com/)，但是你可以发送电子邮件使用 SMTP 和其他机制。</span><span class="sxs-lookup"><span data-stu-id="373a1-186">This tutorial shows how to add email notifications through [SendGrid](https://sendgrid.com/), but you can send email using SMTP and other mechanisms.</span></span>

<span data-ttu-id="373a1-187">安装`SendGrid`NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="373a1-187">Install the `SendGrid` NuGet package:</span></span>

* <span data-ttu-id="373a1-188">从命令行：</span><span class="sxs-lookup"><span data-stu-id="373a1-188">From the command line:</span></span>

    `dotnet add package SendGrid`

* <span data-ttu-id="373a1-189">从程序包管理器控制台中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="373a1-189">From the Package Manager Console, enter the following command:</span></span>

  `Install-Package SendGrid`

<span data-ttu-id="373a1-190">请参阅[免费开始使用 SendGrid](https://sendgrid.com/free/)注册一个免费的 SendGrid 帐户。</span><span class="sxs-lookup"><span data-stu-id="373a1-190">See [Get Started with SendGrid for Free](https://sendgrid.com/free/) to register for a free SendGrid account.</span></span>

#### <a name="configure-sendgrid"></a><span data-ttu-id="373a1-191">配置了 SendGrid</span><span class="sxs-lookup"><span data-stu-id="373a1-191">Configure SendGrid</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="373a1-192">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="373a1-192">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="373a1-193">若要配置 SendGrid，添加类似于以下的代码*Services/EmailSender.cs*:</span><span class="sxs-lookup"><span data-stu-id="373a1-193">To configure SendGrid, add code similar to the following in *Services/EmailSender.cs*:</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover/Services/EmailSender.cs)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="373a1-194">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="373a1-194">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

* <span data-ttu-id="373a1-195">中添加代码*Services/MessageServices.cs*类似于以下配置 SendGrid:</span><span class="sxs-lookup"><span data-stu-id="373a1-195">Add code in *Services/MessageServices.cs* similar to the following to configure SendGrid:</span></span>

[!code-csharp[](accconfirm/sample/WebApp1/Services/MessageServices.cs)]

---

## <a name="enable-account-confirmation-and-password-recovery"></a><span data-ttu-id="373a1-196">启用帐户确认和密码恢复</span><span class="sxs-lookup"><span data-stu-id="373a1-196">Enable account confirmation and password recovery</span></span>

<span data-ttu-id="373a1-197">已为帐户确认和密码恢复代码的模板。</span><span class="sxs-lookup"><span data-stu-id="373a1-197">The template has the code for account confirmation and password recovery.</span></span> <span data-ttu-id="373a1-198">查找`OnPostAsync`中的方法*Pages/Account/Register.cshtml.cs*。</span><span class="sxs-lookup"><span data-stu-id="373a1-198">Find the `OnPostAsync` method in *Pages/Account/Register.cshtml.cs*.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="373a1-199">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="373a1-199">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="373a1-200">可防止新注册的用户自动登录通过注释掉以下行：</span><span class="sxs-lookup"><span data-stu-id="373a1-200">Prevent newly registered users from being automatically logged on by commenting out the following line:</span></span>

```csharp
await _signInManager.SignInAsync(user, isPersistent: false);
```

<span data-ttu-id="373a1-201">突出显示的已更改行还会显示完整的方法：</span><span class="sxs-lookup"><span data-stu-id="373a1-201">The complete method is shown with the changed line highlighted:</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover/Pages/Account/Register.cshtml.cs?highlight=16&name=snippet_Register)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="373a1-202">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="373a1-202">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="373a1-203">若要启用帐户确认后，取消注释以下代码：</span><span class="sxs-lookup"><span data-stu-id="373a1-203">To enable account confirmation, uncomment the following code:</span></span>

[!code-csharp[](accconfirm/sample/WebApp1/Controllers/AccountController.cs?highlight=16-25&name=snippet_Register)]

<span data-ttu-id="373a1-204">**注意：** 代码将阻止新注册的用户自动登录通过注释掉以下行：</span><span class="sxs-lookup"><span data-stu-id="373a1-204">**Note:** The code is preventing a newly registered user from being automatically logged on by commenting out the following line:</span></span>

```csharp
//await _signInManager.SignInAsync(user, isPersistent: false);
```

<span data-ttu-id="373a1-205">通过对取消注释中的代码中启用密码恢复`ForgotPassword`操作*controllers/Accountcontroller.cs*:</span><span class="sxs-lookup"><span data-stu-id="373a1-205">Enable password recovery by uncommenting the code in the `ForgotPassword` action of *Controllers/AccountController.cs*:</span></span>

[!code-csharp[](accconfirm/sample/WebApp1/Controllers/AccountController.cs?highlight=17-23&name=snippet_ForgotPassword)]

<span data-ttu-id="373a1-206">取消注释中的窗体元素*Views/Account/ForgotPassword.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="373a1-206">Uncomment the form element in *Views/Account/ForgotPassword.cshtml*.</span></span> <span data-ttu-id="373a1-207">你可能想要删除`<p> For more information on how to enable reset password ... </p>`元素，它包含此文章的链接。</span><span class="sxs-lookup"><span data-stu-id="373a1-207">You might want to remove the `<p> For more information on how to enable reset password ... </p>` element, which contains a link to this article.</span></span>

[!code-cshtml[](accconfirm/sample/WebApp1/Views/Account/ForgotPassword.cshtml?highlight=7-10,12,28)]

---

## <a name="register-confirm-email-and-reset-password"></a><span data-ttu-id="373a1-208">注册、 确认电子邮件，以及重置密码</span><span class="sxs-lookup"><span data-stu-id="373a1-208">Register, confirm email, and reset password</span></span>

<span data-ttu-id="373a1-209">运行该 web 应用，并测试帐户确认和密码恢复流。</span><span class="sxs-lookup"><span data-stu-id="373a1-209">Run the web app, and test the account confirmation and password recovery flow.</span></span>

* <span data-ttu-id="373a1-210">运行应用并注册新的用户</span><span class="sxs-lookup"><span data-stu-id="373a1-210">Run the app and register a new user</span></span>

  ![Web 应用程序帐户注册视图](accconfirm/_static/loginaccconfirm1.png)

* <span data-ttu-id="373a1-212">检查你的帐户确认链接的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="373a1-212">Check your email for the account confirmation link.</span></span> <span data-ttu-id="373a1-213">请参阅[调试电子邮件](#debug)如果你不会获得电子邮件。</span><span class="sxs-lookup"><span data-stu-id="373a1-213">See [Debug email](#debug) if you don't get the email.</span></span>
* <span data-ttu-id="373a1-214">单击链接以确认你的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="373a1-214">Click the link to confirm your email.</span></span>
* <span data-ttu-id="373a1-215">登录你的电子邮件和密码。</span><span class="sxs-lookup"><span data-stu-id="373a1-215">Log in with your email and password.</span></span>
* <span data-ttu-id="373a1-216">注销。</span><span class="sxs-lookup"><span data-stu-id="373a1-216">Log off.</span></span>

### <a name="view-the-manage-page"></a><span data-ttu-id="373a1-217">查看管理页</span><span class="sxs-lookup"><span data-stu-id="373a1-217">View the manage page</span></span>

<span data-ttu-id="373a1-218">在浏览器中选择你的用户名：![用户同名的浏览器窗口](accconfirm/_static/un.png)</span><span class="sxs-lookup"><span data-stu-id="373a1-218">Select your user name in the browser: ![browser window with user name](accconfirm/_static/un.png)</span></span>

<span data-ttu-id="373a1-219">你可能需要展开导航栏，以查看用户名称。</span><span class="sxs-lookup"><span data-stu-id="373a1-219">You might need to expand the navbar to see user name.</span></span>

![导航栏](accconfirm/_static/x.png)

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="373a1-221">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="373a1-221">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="373a1-222">管理页显示与**配置文件**选定选项卡。</span><span class="sxs-lookup"><span data-stu-id="373a1-222">The manage page is displayed with the **Profile** tab selected.</span></span> <span data-ttu-id="373a1-223">**电子邮件**显示一个复选框，表明电子邮件已确认。</span><span class="sxs-lookup"><span data-stu-id="373a1-223">The **Email** shows a check box indicating the email has been confirmed.</span></span>

![管理页](accconfirm/_static/rick2.png)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="373a1-225">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="373a1-225">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="373a1-226">这在教程后面部分提到。</span><span class="sxs-lookup"><span data-stu-id="373a1-226">This is mentioned later in the tutorial.</span></span>
<span data-ttu-id="373a1-227">![管理页](accconfirm/_static/rick2.png)</span><span class="sxs-lookup"><span data-stu-id="373a1-227">![manage page](accconfirm/_static/rick2.png)</span></span>

---

### <a name="test-password-reset"></a><span data-ttu-id="373a1-228">测试密码重置</span><span class="sxs-lookup"><span data-stu-id="373a1-228">Test password reset</span></span>

* <span data-ttu-id="373a1-229">如果你要登录，选择**注销**。</span><span class="sxs-lookup"><span data-stu-id="373a1-229">If you're logged in, select **Logout**.</span></span>
* <span data-ttu-id="373a1-230">选择**登录**链接并选择**忘记了密码？** 链接。</span><span class="sxs-lookup"><span data-stu-id="373a1-230">Select the **Log in** link and select the **Forgot your password?** link.</span></span>
* <span data-ttu-id="373a1-231">输入用于注册帐户的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="373a1-231">Enter the email you used to register the account.</span></span>
* <span data-ttu-id="373a1-232">发送一封电子邮件包含要重置密码的链接。</span><span class="sxs-lookup"><span data-stu-id="373a1-232">An email with a link to reset your password is sent.</span></span> <span data-ttu-id="373a1-233">请检查你的电子邮件，单击链接以重置密码。</span><span class="sxs-lookup"><span data-stu-id="373a1-233">Check your email and click the link to reset your password.</span></span> <span data-ttu-id="373a1-234">你的密码已成功重置后，你可以登录你的电子邮件和新密码。</span><span class="sxs-lookup"><span data-stu-id="373a1-234">After your password has been successfully reset, you can log in with your email and new password.</span></span>

<a name="debug"></a>

### <a name="debug-email"></a><span data-ttu-id="373a1-235">调试电子邮件</span><span class="sxs-lookup"><span data-stu-id="373a1-235">Debug email</span></span>

<span data-ttu-id="373a1-236">如果无法获取电子邮件工作：</span><span class="sxs-lookup"><span data-stu-id="373a1-236">If you can't get email working:</span></span>

* <span data-ttu-id="373a1-237">创建[控制台应用程序发送电子邮件](https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html)。</span><span class="sxs-lookup"><span data-stu-id="373a1-237">Create a [console app to send email](https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html).</span></span>
* <span data-ttu-id="373a1-238">查看[电子邮件活动](https://sendgrid.com/docs/User_Guide/email_activity.html)页。</span><span class="sxs-lookup"><span data-stu-id="373a1-238">Review the [Email Activity](https://sendgrid.com/docs/User_Guide/email_activity.html) page.</span></span>
* <span data-ttu-id="373a1-239">请检查垃圾邮件文件夹。</span><span class="sxs-lookup"><span data-stu-id="373a1-239">Check your spam folder.</span></span>
* <span data-ttu-id="373a1-240">请尝试其他电子邮件提供程序 （Microsoft、 Yahoo、 Gmail 等） 上的另一个电子邮件别名</span><span class="sxs-lookup"><span data-stu-id="373a1-240">Try another email alias on a different email provider (Microsoft, Yahoo, Gmail, etc.)</span></span>
* <span data-ttu-id="373a1-241">尝试发送到不同的电子邮件帐户。</span><span class="sxs-lookup"><span data-stu-id="373a1-241">Try sending to different email accounts.</span></span>

<span data-ttu-id="373a1-242">**最佳安全方案**是**不**使用生产中测试和开发的机密。</span><span class="sxs-lookup"><span data-stu-id="373a1-242">**A security best practice** is to **not** use production secrets in test and development.</span></span> <span data-ttu-id="373a1-243">如果将应用发布到 Azure，你可以设置 SendGrid 机密与 Azure Web 应用门户中的应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="373a1-243">If you publish the app to Azure, you can set the SendGrid secrets as application settings in the Azure Web App portal.</span></span> <span data-ttu-id="373a1-244">配置系统设置以从环境变量中读取项。</span><span class="sxs-lookup"><span data-stu-id="373a1-244">The configuration system is set up to read keys from environment variables.</span></span>

## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="373a1-245">合并社交和本地登录帐户</span><span class="sxs-lookup"><span data-stu-id="373a1-245">Combine social and local login accounts</span></span>

<span data-ttu-id="373a1-246">若要完成此部分，必须先启用外部身份验证提供程序。</span><span class="sxs-lookup"><span data-stu-id="373a1-246">To complete this section, you must first enable an external authentication provider.</span></span> <span data-ttu-id="373a1-247">请参阅[Facebook、 Google、 和外部提供程序身份验证](xref:security/authentication/social/index)。</span><span class="sxs-lookup"><span data-stu-id="373a1-247">See [Facebook, Google, and external provider authentication](xref:security/authentication/social/index).</span></span>

<span data-ttu-id="373a1-248">你可以通过单击电子邮件链接组合本地和社交帐户。</span><span class="sxs-lookup"><span data-stu-id="373a1-248">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="373a1-249">按以下顺序"RickAndMSFT@gmail.com"首先创建为本地登录名; 但是，你可以创建帐户作为的社交登录名，然后再添加本地登录名。</span><span class="sxs-lookup"><span data-stu-id="373a1-249">In the following sequence, "RickAndMSFT@gmail.com" is first created as a local login; however, you can create the account as a social login first, then add a local login.</span></span>

![Web 应用程序：RickAndMSFT@gmail.com身份验证的用户](accconfirm/_static/rick.png)

<span data-ttu-id="373a1-251">单击**管理**链接。</span><span class="sxs-lookup"><span data-stu-id="373a1-251">Click on the **Manage** link.</span></span> <span data-ttu-id="373a1-252">请注意与此帐户关联 0 外部 （社交登录名）。</span><span class="sxs-lookup"><span data-stu-id="373a1-252">Note the 0 external (social logins) associated with this account.</span></span>

![管理视图](accconfirm/_static/manage.png)

<span data-ttu-id="373a1-254">单击另一个登录服务的链接，接受应用程序请求。</span><span class="sxs-lookup"><span data-stu-id="373a1-254">Click the link to another login service and accept the app requests.</span></span> <span data-ttu-id="373a1-255">下图中，在 Facebook 是外部身份验证提供程序：</span><span class="sxs-lookup"><span data-stu-id="373a1-255">In the following image, Facebook is the external authentication provider:</span></span>

![管理外部登录名视图列出 Facebook](accconfirm/_static/fb.png)

<span data-ttu-id="373a1-257">已经合并两个帐户。</span><span class="sxs-lookup"><span data-stu-id="373a1-257">The two accounts have been combined.</span></span> <span data-ttu-id="373a1-258">现在可以使用任一帐户登录。</span><span class="sxs-lookup"><span data-stu-id="373a1-258">You are able to log on with either account.</span></span> <span data-ttu-id="373a1-259">你可能希望添加本地帐户，以防其社交登录身份验证服务已关闭，或更有可能已丢失到其社交帐户访问你用户。</span><span class="sxs-lookup"><span data-stu-id="373a1-259">You might want your users to add local accounts in case their social login authentication service is down, or more likely they've lost access to their social account.</span></span>

## <a name="enable-account-confirmation-after-a-site-has-users"></a><span data-ttu-id="373a1-260">启用帐户确认后某个站点具有用户</span><span class="sxs-lookup"><span data-stu-id="373a1-260">Enable account confirmation after a site has users</span></span>

<span data-ttu-id="373a1-261">启用站点上与用户的帐户确认锁定更改所有现有用户。</span><span class="sxs-lookup"><span data-stu-id="373a1-261">Enabling account confirmation on a site with users locks out all the existing users.</span></span> <span data-ttu-id="373a1-262">现有用户被锁定，因为他们的帐户不确认。</span><span class="sxs-lookup"><span data-stu-id="373a1-262">Existing users are locked out because their accounts aren't confirmed.</span></span> <span data-ttu-id="373a1-263">若要解决现有用户锁定，请使用以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="373a1-263">To work around existing user lockout, use one of the following approaches:</span></span>

* <span data-ttu-id="373a1-264">更新数据库，将标记为正在确认的所有现有用户。</span><span class="sxs-lookup"><span data-stu-id="373a1-264">Update the database to mark all existing users as being confirmed.</span></span>
* <span data-ttu-id="373a1-265">确认正在退出用户。</span><span class="sxs-lookup"><span data-stu-id="373a1-265">Confirm exiting users.</span></span> <span data-ttu-id="373a1-266">例如，批处理-发送电子邮件中的标注确认链接。</span><span class="sxs-lookup"><span data-stu-id="373a1-266">For example, batch-send emails with confirmation links.</span></span>
