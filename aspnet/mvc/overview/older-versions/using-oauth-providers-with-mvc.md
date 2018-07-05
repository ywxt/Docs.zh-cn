---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: 通过 MVC 4 使用 OAuth 提供程序 |Microsoft Docs
author: tfitzmac
description: 本教程演示如何构建 ASP.NET MVC 4 web 应用程序，使用户能够从 Facebo 之类的外部提供程序的凭据登录...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/19/2013
ms.topic: article
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: b023d3d78bd703db93deb2e23661c9041fe74694
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37372309"
---
<a name="using-oauth-providers-with-mvc-4"></a>通过 MVC 4 使用 OAuth 提供程序
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本教程演示如何构建 ASP.NET MVC 4 web 应用程序，使用户能够从外部提供程序，如 Facebook、 Twitter、 Microsoft 或 Google 凭据登录，然后将集成到这些提供程序的功能的一些应用web 应用程序。 为简单起见，本教程重点介绍使用来自 Facebook 的凭据。
> 
> 若要在 ASP.NET MVC 5 web 应用程序中使用外部凭据，请参阅[创建 ASP.NET MVC 5 应用程序使用 Facebook 和 Google OAuth2 和 OpenID 登录](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。
> 
> 启用这些凭据在您的网站中提供一个明显的优势，因为数以百万计的用户已获得与这些外部提供商的帐户。 这些用户可能更倾向于注册为您的网站，如果它们不需要创建和记住一组新的凭据。 此外，通过这些提供程序之一的用户已登录后，您可以将从提供程序的社交操作整合。


## <a name="what-youll-build"></a>你将生成

在本教程中有两个主要目标：

1. 使用户能够使用 OAuth 提供程序的凭据进行登录。
2. 从提供程序检索帐户信息并将该信息与你的站点的帐户注册集成。

虽然在本教程中的这些示例着重于将 Facebook 用作身份验证提供程序，你可修改代码以使用任何提供程序。 若要实现任何提供程序的步骤是非常类似于您将看到在本教程中的步骤。 只会注意到设置的显著区别时直接调用提供程序的 API。

## <a name="prerequisites"></a>系统必备

- [Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs)或[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)

Or

- Microsoft Visual Studio 2010 SP1 或[Visual Web Developer 速成版 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)
- [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)

此外，本主题假定你具有有关 ASP.NET MVC 和 Visual Studio 的基本知识。 如果您需要 ASP.NET MVC 4 简介，请参阅[ASP.NET MVC 4 简介](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)。

## <a name="create-the-project"></a>创建项目

在 Visual Studio 中新建 ASP.NET MVC 4 Web 应用程序，并将其命名&quot;OAuthMVC&quot;。 你可以面向.NET Framework 4.5 或 4。

![创建项目](using-oauth-providers-with-mvc/_static/image1.png)

在新建 ASP.NET MVC 4 项目窗口中，选择**Internet 应用程序**并保留**Razor**作为视图引擎。

![选择 Internet 应用程序](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a>启用提供程序

如果使用 Internet 应用程序模板创建的 MVC 4 web 应用程序，项目将创建具有名为 AuthConfig.cs 应用中的文件\_开始文件夹。

![AuthConfig 文件](using-oauth-providers-with-mvc/_static/image3.png)

AuthConfig 文件包含注册外部身份验证提供程序的客户端的代码。 默认情况下，此代码是加上注释，以便启用任何外部提供程序。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

必须取消注释此代码以使用外部身份验证客户端。 取消注释只想要包括在你的站点中的提供程序。 对于本教程，你将只启用 Facebook 凭据。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

请注意，在上面的示例中，该方法包含空字符串用于注册参数。 如果尝试运行应用程序现在，应用程序将引发参数异常，因为参数不允许使用空字符串。 若要提供有效的值，必须注册您的网站向外部提供程序，如在下一节中所示。

## <a name="registering-with-an-external-provider"></a>使用外部提供程序注册

用户进行身份验证使用外部提供程序的凭据，必须使用提供程序注册你的网站。 注册你的站点时，你将收到参数 （如密钥或 id 和密码） 来注册客户端时包括。 您必须有你想要使用的提供程序的帐户。

本教程不会不会显示所有使用这些提供程序进行注册，必须执行的步骤。 不执行这些步骤通常比较困难。 若要成功注册你的站点，请按照这些网站上提供的说明进行操作。 若要开始使用注册你的网站，请参阅有关在开发人员网站：

- [Facebook](https://developers.facebook.com/)
- [Google](https://developers.google.com/)
- [Microsoft](http://manage.dev.live.com/)
- [Twitter](https://dev.twitter.com/)

如果向 Facebook 注册你的网站，则可以提供&quot;localhost&quot;站点域和`&quot;http://localhost/&quot;`对于 URL，如下图中所示。 使用 localhost 适用于大多数提供程序，但当前不使用 Microsoft 提供程序。 对于 Microsoft 提供程序，必须包含有效的网站 URL。

![注册站点](using-oauth-providers-with-mvc/_static/image4.png)

在上图中，已删除的应用程序 id、 应用程序密码和联系人电子邮件的值。 实际注册你的站点时，这些值将会显示。 想要注意的应用程序 id 和应用机密的值，因为会将它们添加到你的应用程序。

## <a name="creating-test-users"></a>创建测试用户

如果您不介意使用现有的 Facebook 帐户来测试您的站点，则可以跳过本部分中。

为应用程序的 Facebook 应用程序管理页中，可以轻松创建测试用户。 您可以使用这些测试帐户登录到你的站点。 通过单击创建测试用户**角色**在左侧的导航窗格中单击链接**创建**链接。

![创建测试用户](using-oauth-providers-with-mvc/_static/image5.png)

Facebook 站点会自动创建测试帐户的请求数。

## <a name="adding-application-id-and-secret-from-the-provider"></a>从提供程序中添加应用程序 id 和机密

现在，已从 Facebook 中接收的 id 和密码，请返回到 AuthConfig 文件并将其添加作为参数值。 下面显示的值不是实际值。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a>外部凭据登录

这是所要执行的操作启用你的站点中的外部凭据。 运行你的应用程序并单击右上角的登录链接。 该模板会自动识别你已注册为提供程序的 Facebook 和提供程序包括一个按钮。 如果注册多个提供程序时，会自动包括为每个按钮。

![外部登录](using-oauth-providers-with-mvc/_static/image6.png)

本教程不介绍如何为外部提供程序自定义按钮中的日志。 该信息，请参阅[时使用 OAuth/OpenID 自定义登录 UI](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)。

单击 Facebook 按钮，能够使用 Facebook 凭据进行登录。 您选择其中一个外部提供程序，意味着，将重定向到该站点并且该服务以用户身份登录系统提示。

下图显示为 Facebook 登录屏幕。 它指出，使用的你的 Facebook 帐户登录到名为 oauthmvcexample 的站点。

![facebook 身份验证](using-oauth-providers-with-mvc/_static/image7.png)

使用 Facebook 凭据登录后, 一个页面将通知用户该站点将有权访问的基本信息。

![请求权限](using-oauth-providers-with-mvc/_static/image8.png)

选择后**转到应用**，用户必须注册为该站点。 用户使用 Facebook 凭据登录后，下图显示了注册页。 用户名称是通常使用与该提供程序的名称预先填充。

![register](using-oauth-providers-with-mvc/_static/image9.png)

单击**注册**以完成注册。 关闭浏览器。

您可以看到新的帐户已添加到数据库。 在服务器资源管理器中打开**DefaultConnection**数据库，打开**表**文件夹。

![数据库表](using-oauth-providers-with-mvc/_static/image10.png)

右键单击**UserProfile**表，然后选择**显示表数据**。

![显示数据](using-oauth-providers-with-mvc/_static/image11.png)

你将看到添加的新帐户。 查看中的数据**网页\_OAuthMembership**表。 你将看到与刚刚添加的帐户的外部提供程序相关的更多数据。

如果只想要启用外部身份验证，则已完成。 但是，您可以进一步将集成从提供程序的信息到新用户注册过程中，如以下各节中所示。

## <a name="create-models-for-additional-user-information"></a>创建模型的其他用户信息

您注意到在前面部分中，您不需要检索要处理的内置帐户注册任何其他信息。 但是，大多数外部提供程序传递有关用户的附加信息。 以下部分说明如何保留这些信息并将其保存到数据库。 具体而言，将保留用户的完整名称，用户的个人 web 页的 URI 的值和一个值，指示是否验证 Facebook 帐户。

将使用[Code First 迁移](https://msdn.microsoft.com/data/jj591621)添加用于存储其他用户信息的表。 要添加到现有数据库表，因此您首先需要创建当前数据库的快照。 通过创建当前数据库的快照，稍后可以创建包含新的表的迁移。 若要创建当前数据库的快照：

1. 打开**包管理器控制台**
2. 运行命令**启用迁移**
3. 运行命令**IgnoreChanges 添加迁移初始 –**
4. 运行命令**更新数据库**

现在，您将添加新属性。 在 Models 文件夹中，打开 AccountModels.cs 文件中，并查找 RegisterExternalLoginModel 类。 RegisterExternalLoginModel 类保存回来自身份验证提供程序的值。 添加命名 FullName 和链接，为以下突出显示部分的属性。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

此外在 AccountModels.cs，添加一个名为 ExtraUserInformation 的新类。 此类表示将在数据库中创建的新表。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

在 UsersContext 类中，添加突出显示的代码下面创建新的类的 DbSet 属性。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

现在您就可以创建新表。 再次，这一次打开包管理器控制台：

1. 运行命令**添加迁移 AddExtraUserInformation**
2. 运行命令**更新数据库**

在数据库中现在存在新表。

## <a name="retrieve-the-additional-data"></a>检索其他数据

有两种方法来检索其他用户数据。 第一种方法是保留用户数据传递回去，默认情况下，身份验证请求过程。 第二种方法是专门调用提供程序 API 和请求的详细信息。 FullName 和链接值都会自动传递回的 Facebook。 通过 Facebook API 调用检索值，该值指示是否验证 Facebook 帐户。 首先，将为 FullName 和链接，填充值，然后更高版本，你将获取已验证的值。

若要检索其他用户数据，请打开**AccountController.cs**中的文件**控制器**文件夹。

此文件包含日志记录、 注册和管理帐户的逻辑。 具体而言，请注意，调用的方法**ExternalLoginCallback**并**ExternalLoginConfirmation**。 在这些方法中，可以添加代码以自定义应用程序的外部登录操作。 第一行**ExternalLoginCallback**方法包含：

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

其他用户数据将传回到**ExtraData**的属性**AuthenticationResult**从返回的对象**VerifyAuthentication**方法。 Facebook 客户端包含中的以下值**ExtraData**属性：

- id
- name
- 链接
- 性别
- accesstoken

其他提供程序将 ExtraData 属性中具有类似但略有不同的数据。

如果用户是您的网站的新手，将检索某些其他数据，并将该数据传递给确认视图。 仅当用户不熟悉你的站点运行的方法中代码的最后一个块。 替换为以下行：

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

用下面这行：

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

此更改仅包括 FullName 和链接属性的值。

在中**ExternalLoginConfirmation**方法中，修改以下代码，突出显示的那样以保存其他用户信息。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a>调整视图

从提供程序检索其他用户数据将显示在注册页。

在中**视图**/**帐户**文件夹中，打开**ExternalLoginConfirmation.cshtml**。 以下用户名称与现有字段，为 FullName、 链接和 PictureLink 中添加字段。

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

你现基本准备好运行应用程序并注册一个新用户保存的其他信息。 必须具有与站点尚未注册一个帐户。 您可以使用不同的测试帐户，或删除中的行**UserProfile**并**网页\_OAuthMembership**你想要重复使用的帐户的表。 通过删除这些行，您需要确保重新注册了该帐户。

运行应用程序并注册新的用户。 请注意，这一次确认页包含更多的值。

![register](using-oauth-providers-with-mvc/_static/image12.png)

注册后，关闭浏览器。 请注意中的新值在数据库中查找**ExtraUserInformation**表。

## <a name="install-nuget-package-for-facebook-api"></a>安装用于 Facebook API NuGet 包

提供 Facebook [API](https://developers.facebook.com/docs/reference/apis/)可调用以执行操作。 通过将定向发送 HTTP 请求，或使用安装 NuGet 包，它方便了发送这些请求，可以调用 Facebook API。 使用 NuGet 包显示在本教程中，但安装 NuGet 包不重要。 本教程演示如何使用 Facebook C# SDK 包。 有其他帮助调用 Facebook API 的 NuGet 包。

从**管理 NuGet 包**windows 中，选择 Facebook C# SDK 包。

![安装包](using-oauth-providers-with-mvc/_static/image13.png)

将使用 Facebook C# SDK 调用的用户需要访问令牌的操作。 下一部分演示如何获取访问令牌。

## <a name="retrieve-access-token"></a>检索访问令牌

验证用户的凭据后最外部提供程序传递回访问令牌。 此访问令牌是非常重要，因为它使你可以调用仅可供经过身份验证的用户的操作。 因此，检索和存储访问令牌时非常重要您想要提供更多的功能。

根据外部提供程序，访问令牌可能只在有限是时间的有效。 若要确保您有一个有效的访问令牌，您将检索它每次用户登录，并将其存储为会话值而不是将其保存到数据库。

在中**ExternalLoginCallback**方法，返回还传递访问令牌**ExtraData**属性**AuthenticationResult**对象。 添加到突出显示的代码**ExternalLoginCallback**以保存中的访问令牌**会话**对象。 每次用户使用 Facebook 帐户登录时运行此代码。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

虽然此示例从 Facebook 中检索访问令牌，可以通过相同的键名为从任何外部提供程序检索访问令牌&quot;accesstoken&quot;。

## <a name="logging-off"></a>注销

默认值**注销**方法记录用户从应用程序，但不会记录用户从外部提供程序。 若要从 Facebook，将用户登录，并防止令牌保持用户注销后，可以添加到以下突出显示的代码**注销**AccountController 中的方法。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

中提供的值`next`参数是要使用后用户已从 Facebook 注销的 URL。 在测试时在本地计算机上，将为你的本地网站提供正确的端口号。 在生产中，将提供一个默认页，例如 contoso.com。

## <a name="retrieve-user-information-that-requires-the-access-token"></a>检索需要访问令牌的用户信息

现在，存储的访问令牌并安装 Facebook C# SDK 包后，你可以使用它们一起以从 Facebook 中请求的其他用户信息。 在中**ExternalLoginConfirmation**方法中，创建的实例**FacebookClient**类通过将访问令牌的值传递。 请求的值**验证**当前经过身份验证的用户的属性。 **验证**属性指示是否 Facebook 已验证的帐户通过其他方式，如到移动电话发送短信。 在数据库中保存此值。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

再次需要删除用户，在数据库中的记录或使用其他 Facebook 帐户。

运行该应用程序，并注册新的用户。 看看**ExtraUserInformation**表以查看已验证属性的值。

## <a name="conclusion"></a>结束语

在本教程中，您可以创建与 Facebook 集成进行用户身份验证和注册数据的站点。 您学习了如何为 MVC 4 web 应用程序，以及如何自定义该默认行为设置的默认行为。

## <a name="related-topics"></a>相关主题

- [使用身份验证和 SQL 数据库创建 ASP.NET MVC 应用并将其部署到 Azure 应用服务](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
