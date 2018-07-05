---
title: 帐户确认和 ASP.NET Core 中的密码恢复
author: rick-anderson
description: 了解如何生成使用电子邮件确认及密码重置功能的 ASP.NET Core 应用程序。
ms.author: riande
ms.date: 2/11/2018
uid: security/authentication/accconfirm
ms.openlocfilehash: 12265903f60ff6d62befc445434db025c244c178
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803267"
---
# <a name="account-confirmation-and-password-recovery-in-aspnet-core"></a>帐户确认和 ASP.NET Core 中的密码恢复

作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Joe Audette](https://twitter.com/joeaudette)

本教程演示了如何生成具有电子邮件确认及密码重置的 ASP.NET Core 应用。 本教程是**不**开头主题。 您应熟悉：

* [ASP.NET Core](xref:tutorials/first-mvc-app/start-mvc)
* [身份验证](xref:security/authentication/index)
* [Entity Framework Core](xref:data/ef-mvc/intro)

请参阅[此 PDF 文件](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf)的 ASP.NET Core MVC 1.1 和 2.x 版本。

## <a name="prerequisites"></a>系统必备

[!INCLUDE [](~/includes/net-core-prereqs.md)]

## <a name="create-a-new-aspnet-core-project-with-the-net-core-cli"></a>使用.NET Core CLI 创建新的 ASP.NET Core 项目

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

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

* `--auth Individual` 指定单个用户帐户的项目模板。
* 在 Windows 中，添加`-uld`选项。 它指定应使用 LocalDB 而不是 SQLite。
* 运行`new mvc --help`以获取有关此命令的帮助。

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

如果使用 CLI 或 SQLite，运行以下命令在命令窗口中：

```console
dotnet new mvc --auth Individual
```

* `--auth Individual` 指定单个用户帐户的项目模板。
* 在 Windows 中，添加`-uld`选项。 它指定应使用 LocalDB 而不是 SQLite。
* 运行`new mvc --help`以获取有关此命令的帮助。

---

或者，你可以使用 Visual Studio 创建新的 ASP.NET Core 项目：

* 在 Visual Studio 中，创建一个新**Web 应用程序**项目。
* 选择**ASP.NET Core 2.0**。 **.NET Core**选择在下图中，但你可以选择 **.NET Framework**。
* 选择**更改身份验证**并将设置为**单个用户帐户**。
* 保留默认值**用户的存储帐户中应用**。

![显示"单个用户帐户 radio"选择新建项目对话框](accconfirm/_static/2.png)

## <a name="test-new-user-registration"></a>测试新的用户注册

运行该应用程序中，选择**注册**链接，并注册用户。 按照运行 Entity Framework Core 迁移的说明。 在此情况下，电子邮件的唯一验证是使用[[EmailAddress]](/dotnet/api/system.componentmodel.dataannotations.emailaddressattribute)属性。 提交后注册，登录到应用程序。 稍后在本教程中，以便验证其电子邮件之后才将新用户无法登录更新代码。

## <a name="view-the-identity-database"></a>查看标识数据库

请参阅[ASP.NET Core MVC 项目中使用的 SQLite](xref:tutorials/first-mvc-app-xplat/working-with-sql)有关说明如何查看 SQLite 数据库。

对于 Visual Studio:

* 从**视图**菜单中，选择**SQL Server 对象资源管理器**(SSOX)。
* 导航到 **(localdb) MSSQLLocalDB (SQL Server 13)**。 右键单击**dbo。AspNetUsers** > **查看数据**:

![在 AspNetUsers 表中 SQL Server 对象资源管理器的上下文菜单](accconfirm/_static/ssox.png)

请注意此表的`EmailConfirmed`字段是`False`。

您可能想要再次在下一步中使用此电子邮件，该应用将发送确认电子邮件时。 右键单击行并选择**删除**。 删除电子邮件别名便于您在以下步骤。

---

## <a name="require-https"></a>要求使用 HTTPS

请参阅[要求使用 HTTPS](xref:security/enforcing-ssl)。

<a name="prevent-login-at-registration"></a>
## <a name="require-email-confirmation"></a>需要电子邮件确认

它是最佳做法以确认新的用户注册的电子邮件地址。 电子邮件确认可帮助以验证它们没有模拟其他人 （即，他们尚未注册与其他人的电子邮件）。 假设有论坛，并且您想阻止"yli@example.com"中注册为"nolivetto@contoso.com"。 而无需电子邮件确认"nolivetto@contoso.com"可能会从您的应用程序收到不需要的电子邮件。 假设用户意外地注册为"ylo@example.com"和"yli"的拼写错误的重视。 它们将无法使用密码恢复，因为此应用没有其正确的电子邮件。 电子邮件确认从智能机器人提供有限的保护。 电子邮件确认不提供保护，免受恶意用户的与许多电子邮件帐户。

你通常想要发布到网站的任何数据，有已确认的电子邮件之前阻止新用户。

更新`ConfigureServices`需要确认电子邮件：

[!code-csharp[](accconfirm/sample/WebPWrecover/Startup.cs?name=snippet1&highlight=12-17)]

`config.SignIn.RequireConfirmedEmail = true;` 可防止已注册的用户登录之前确认其电子邮件。

### <a name="configure-email-provider"></a>配置电子邮件提供商

在本教程中，使用 SendGrid 发送电子邮件。 你需要一个 SendGrid 帐户和密钥用于发送电子邮件。 可以使用其他电子邮件提供商。 ASP.NET Core 2.x 包括`System.Net.Mail`，这允许你从你的应用程序发送电子邮件。 我们建议你使用 SendGrid 或另一个电子邮件服务发送电子邮件。 SMTP 很难保护并正确设置。

[选项模式](xref:fundamentals/configuration/options)用于访问用户帐户和密钥设置。 有关详细信息，请参阅[配置](xref:fundamentals/configuration/index)。

创建一个类来提取的安全电子邮件键。 此示例中，对于`AuthMessageSenderOptions`中创建类*Services/AuthMessageSenderOptions.cs*文件：

[!code-csharp[](accconfirm/sample/WebPWrecover/Services/AuthMessageSenderOptions.cs?name=snippet1)]

设置`SendGridUser`并`SendGridKey`与[机密管理器工具](xref:security/app-secrets)。 例如：

```console
C:\WebAppl\src\WebApp1>dotnet user-secrets set SendGridUser RickAndMSFT
info: Successfully saved SendGridUser = RickAndMSFT to the secret store.
```

在 Windows 中，机密管理器存储中的键/值对*secrets.json*文件中`%APPDATA%/Microsoft/UserSecrets/<WebAppName-userSecretsId>`目录。

内容*secrets.json*未加密文件。 *Secrets.json*文件如下所示 (`SendGridKey`删除值。)

 ```json
  {
    "SendGridUser": "RickAndMSFT",
    "SendGridKey": "<key removed>"
  }
  ```

### <a name="configure-startup-to-use-authmessagesenderoptions"></a>将启动要使用 AuthMessageSenderOptions 配置

添加`AuthMessageSenderOptions`到服务容器的末尾`ConfigureServices`中的方法*Startup.cs*文件：

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](accconfirm/sample/WebPWrecover/Startup.cs?name=snippet2&highlight=28)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](accconfirm/sample/WebApp1/Startup.cs?name=snippet1&highlight=26)]

---

### <a name="configure-the-authmessagesender-class"></a>配置 AuthMessageSender 类

本教程演示如何添加通过电子邮件通知[SendGrid](https://sendgrid.com/)，但是你可以发送电子邮件使用 SMTP 和其他机制。

安装`SendGrid`NuGet 包：

* 从命令行：

    `dotnet add package SendGrid`

* 从包管理器控制台中，输入以下命令：

  `Install-Package SendGrid`

请参阅[免费开始使用 SendGrid](https://sendgrid.com/free/)注册一个免费的 SendGrid 帐户。

#### <a name="configure-sendgrid"></a>配置 SendGrid

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

若要配置 SendGrid，添加类似于中的以下代码*Services/EmailSender.cs*:

[!code-csharp[](accconfirm/sample/WebPWrecover/Services/EmailSender.cs)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

* 将代码中的添加*Services/MessageServices.cs*类似于以下内容，以配置 SendGrid:

[!code-csharp[](accconfirm/sample/WebApp1/Services/MessageServices.cs)]

---

## <a name="enable-account-confirmation-and-password-recovery"></a>启用帐户确认和密码恢复

该模板具有帐户确认和密码恢复的代码。 查找`OnPostAsync`中的方法*Pages/Account/Register.cshtml.cs*。

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

禁止新注册的用户将自动记录通过注释掉以下行：

```csharp
await _signInManager.SignInAsync(user, isPersistent: false);
```

完整的方法与更改突出显示的行所示：

[!code-csharp[](accconfirm/sample/WebPWrecover/Pages/Account/Register.cshtml.cs?highlight=16&name=snippet_Register)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

若要启用帐户确认，请取消注释以下代码：

[!code-csharp[](accconfirm/sample/WebApp1/Controllers/AccountController.cs?highlight=16-25&name=snippet_Register)]

**注意：** 代码正在阻止新注册的用户自动记录的注释掉以下行：

```csharp
//await _signInManager.SignInAsync(user, isPersistent: false);
```

通过取消注释中的代码中启用密码恢复`ForgotPassword`的操作*controllers/Accountcontroller.cs*:

[!code-csharp[](accconfirm/sample/WebApp1/Controllers/AccountController.cs?highlight=17-23&name=snippet_ForgotPassword)]

取消注释中的窗体元素*Views/Account/ForgotPassword.cshtml*。 您可能想要删除`<p> For more information on how to enable reset password ... </p>`元素，它包含此文章的链接。

[!code-cshtml[](accconfirm/sample/WebApp1/Views/Account/ForgotPassword.cshtml?highlight=7-10,12,28)]

---

## <a name="register-confirm-email-and-reset-password"></a>注册、 确认电子邮件，和重置密码

运行 web 应用和测试的帐户确认和密码恢复流。

* 运行应用并注册一个新用户

  ![Web 应用程序帐户注册视图](accconfirm/_static/loginaccconfirm1.png)

* 检查你的帐户确认链接的电子邮件。 请参阅[调试电子邮件](#debug)如果没有收到电子邮件。
* 单击链接以确认你的电子邮件。
* 电子邮件和密码登录。
* 注销。

### <a name="view-the-manage-page"></a>查看管理页

在浏览器中选择你的用户名：![用户名的浏览器窗口](accconfirm/_static/un.png)

您可能需要展开导航栏以查看用户名称。

![导航栏](accconfirm/_static/x.png)

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

管理页显示与**配置文件**选定的选项卡。 **电子邮件**显示已确认一个复选框，表明该电子邮件。

![管理页](accconfirm/_static/rick2.png)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

这是本教程的后面所述。
![管理页](accconfirm/_static/rick2.png)

---

### <a name="test-password-reset"></a>测试密码重置

* 如果在登录，请选择**注销**。
* 选择**登录**链接，然后选择**忘记了密码？** 链接。
* 输入用于注册该帐户的电子邮件。
* 发送一封电子邮件包含用于重置密码的链接。 检查你的电子邮件，并单击链接以重置密码。 已成功重置密码后，可以登录你的电子邮件和新密码。

<a name="debug"></a>

### <a name="debug-email"></a>调试电子邮件

如果无法获取电子邮件工作：

* 创建[控制台应用以发送电子邮件](https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html)。
* 审阅[电子邮件活动](https://sendgrid.com/docs/User_Guide/email_activity.html)页。
* 请检查垃圾邮件文件夹。
* 请尝试其他电子邮件提供程序 （Microsoft、 Yahoo、 Gmail 等） 上的另一个电子邮件别名
* 尝试发送到不同的电子邮件帐户。

**最佳安全方案**设置为**不**中使用生产机密中测试和开发。 如果将应用发布到 Azure，可以为 Azure Web 应用门户中的应用程序设置来设置 SendGrid 机密。 配置系统设置以从环境变量读取密钥。

## <a name="combine-social-and-local-login-accounts"></a>合并的社交和本地登录帐户

若要完成本部分中，必须先启用外部身份验证提供程序。 请参阅[Facebook、 Google、 和外部提供程序身份验证](xref:security/authentication/social/index)。

您可以通过单击电子邮件链接组合本地和社交帐户。 按以下顺序"RickAndMSFT@gmail.com"首次创建为本地登录名; 但是，您可以创建帐户为社交登录名，然后添加本地登录名。

![Web 应用程序：RickAndMSFT@gmail.com用户通过身份验证](accconfirm/_static/rick.png)

单击**管理**链接。 请注意与此帐户关联的 0 外部 （社交登录名）。

![管理视图](accconfirm/_static/manage.png)

单击链接到另一个登录名服务，接受应用程序请求。 下图中，在 Facebook 是外部身份验证提供程序：

![管理你的外部登录名视图，其中列出 Facebook](accconfirm/_static/fb.png)

已合并两个帐户。 你将能够使用任一帐户登录。 您可能希望用户其社交登录身份验证服务发生故障，或已为其社交帐户无法访问更有可能的情况下添加本地帐户。

## <a name="enable-account-confirmation-after-a-site-has-users"></a>后一个站点中有用户启用帐户确认

与用户启用帐户确认站点上的阻止所有现有用户。 现有用户被锁定，因为不确认其帐户。 若要解决现有用户锁定，请使用以下方法之一：

* 更新要将标记为正在确认的所有现有用户的数据库。
* 确认现有用户。 例如，批的发送确认链接的电子邮件。
