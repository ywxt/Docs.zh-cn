---
uid: identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
title: 开发 ASP.NET 应用与 Azure Active Directory |Microsoft Docs
author: Rick-Anderson
description: Microsoft ASP.NET tools for Azure Active Directory 可以轻松地为托管在 Azure 上的 web 应用程序启用身份验证。 可以使用 Azure 身份验证...
ms.author: riande
ms.date: 08/14/2014
ms.assetid: 457d7eaf-ee76-4ceb-9082-c7c1721435ad
msc.legacyurl: /identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
msc.type: authoredcontent
ms.openlocfilehash: e2df906d220d738c45006de8b3c92e157ca9e57e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824452"
---
<a name="developing-aspnet-apps-with-azure-active-directory"></a>使用 Azure Active Directory 开发 ASP.NET 应用
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

Microsoft ASP.NET 工具为 Azure Active Directory 简化了为托管的 web 应用启用身份验证[Azure](https://www.windowsazure.com/home/features/web-sites/)。 可以使用 Azure 身份验证从您的组织，从你的本地 Active Directory 同步的公司帐户或在自定义 Azure Active Directory 域中创建用户的 Office 365 用户进行身份验证。 启用 Windows Azure 身份验证，可配置你的应用程序使用单个用户进行身份验证[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)租户。

本教程将演示如何创建 ASP.NET 应用程序配置为登录[Azure Active Directory](https://msdn.microsoft.com/library/azure/mt168838.aspx) (Azure AD)。 此外将了解如何调用图形 API 以获取有关当前登录的用户信息以及如何部署到 Azure 应用程序。

## <a name="prerequisites"></a>系统必备

1. [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express)或[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)。
2. [Visual Studio 2013 Update 4](https://www.microsoft.com/download/details.aspx?id=44921) -Update 3 或更高版本是必需的。
3. 一个 Azure 帐户。 [单击此处](https://azure.microsoft.com/pricing/free-trial/)免费试用版，如果还没有一个帐户。

## <a name="add-a-global-administrator-to-your-active-directory"></a>将全局管理员添加到你的 Active Directory

1. 登录到[Azure 管理门户](https://manage.windowsazure.com/)。
2. 包含的所有 Azure 帐户**默认目录**-单击它，然后单击**用户**在页面顶部的选项卡 （请参阅下图所示）。
3. 单击添加用户。  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image1.png)
4. 创建与新的用户**全局管理员**角色。 单击**用户**从顶部菜单中，然后单击**添加用户**命令栏上的按钮。
5. 在中**添加用户**对话框中，输入新用户的名称，然后单击右箭头。  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image2.png)
6. 输入用户名称，并将角色设置为**全局管理员**。 全局管理员的密码恢复目的而需要的备用电子邮件地址。 在您完成之后，单击右箭头。  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image3.png)
7. 在对话框的下一页上，单击**创建**。 将为新用户创建临时密码，并将其显示在对话框中。   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image4.png)  
  
   保存密码，你将需要在首次登录后更改密码。 下图显示了新的管理员帐户。 您必须使用 Azure Active Directory 登录到您的应用程序，不还显示此页上的 Microsoft 帐户。  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image5.png)

## <a name="create-an-aspnet-application"></a>创建 ASP.NET 应用程序

以下步骤使用[Visual Studio Express 2013 for Web](https://www.microsoft.com/download/details.aspx?id=40747)，并要求[Visual Studio 2013 Update 3](https://www.microsoft.com/download/details.aspx?id=43721)。

1. 在 Visual Studio 中，单击**文件**，然后**新项目**。 上**新的项目**对话框中，选择 Visual C# Web 项目从左侧菜单中，然后单击**确定**。 您可能还想要取消选中**向项目添加 Application Insights**如果你不想让您的应用程序的功能。
2. 在中**新建 ASP.NET 项目**对话框中，选择**MVC**，然后单击**更改身份验证**。   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image6.png)
3. 上**更改身份验证**对话框中，选择**组织帐户**。 这些选项可用于自动注册到 Azure AD 的应用程序，以及自动配置你的应用程序来与 Azure AD 集成。 无需使用**更改身份验证**对话框来注册和配置您的应用程序，但它可以更轻松。 如果将 Visual Studio 2012 为例，可以仍手动在 Azure 管理门户中注册应用程序和更新其配置以与 Azure AD 集成。  
   在下拉列表菜单中，选择**云-单个组织**并**单一登录，读取目录数据**。 为 Azure AD 目录，例如 （在下图中） 输入的域*aricka0yahoo.onmicrosoft.com*，然后单击**确定**。 可以在 azure 门户上的默认目录从域选项卡中获取的域名 （请参阅下的下一步图）。   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image7.png)  
  
   下图显示了在 Azure 门户中的域名。  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image8.png)  

    > [!NOTE]
    > 你可以选择配置将通过单击 Azure AD 中注册应用程序 ID URI**更多选项**。 应用 ID URI 是应用程序，这是 Azure AD 中注册，该应用程序用于与 Azure AD 通信时自身标识的唯一标识符。 有关应用程序 ID URI 和已注册应用程序的其他属性的详细信息，请参阅[本主题](https://msdn.microsoft.com/library/azure/dn499820.aspx#BKMK_Registering)。 通过单击应用 ID URI 字段下方的复选框，您还可以选择在使用相同的应用 ID URI 的 Azure AD 中覆盖现有注册。
4. 单击后**确定**，将显示一个登录对话框，而需要使用全局管理员帐户 （不与你的订阅关联的 Microsoft 帐户） 登录。 如果之前创建一个新的管理员帐户，将所需更改密码并再次使用新密码，然后登录。   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image9.png)
5. 您已成功通过身份验证后，**新建 ASP.NET 项目**对话框将显示身份验证选项 (**组织**) 并将新的应用程序的位置的目录注册 (*aricka0yahoo.onmicrosoft.com*图所示)。 此信息下，选择标记为复选框**在云中托管**。 如果选中此复选框，此项目将作为 Azure web 应用预配，并将启用进行轻松发布更高版本。 单击 **“确定”**。   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image10.png)
6. **配置 Azure 网站**将出现对话框，使用的是自动生成的站点名称和区域。 另请注意您当前登录对话框中的帐户。 你想要确保此帐户是一个 Azure 订阅附加到，通常是 Microsoft 帐户。

    > [!NOTE]
    > 此项目需要数据库。 您需要选择一个现有的数据库，或创建一个新。 需要一个数据库，因为该项目已使用本地数据库文件来存储少量的身份验证配置数据。 在部署到 Azure 网站应用程序时，此数据库不被打包在一起部署，因此需要选择一个可访问位于云中。 单击 **“确定”**。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image11.png)
7. 将创建项目，并且你的身份验证选项和 web 应用选项将自动配置与该项目。 此过程完成后，通过按下以本地方式运行该项目 **^ F5**。 你将需要使用你的组织帐户登录。 为前面创建的帐户提供的用户名和密码，然后单击**登录**。   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image12.png)
8. 成功登录后，ASP.NET 站点会显示，你已通过在页面右上角显示用户名身份验证。  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image13.png)  
  
   如果收到错误：  
   值不能为 null 或为空。 参数名称： linkText   
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image14.png)  
  
   请参阅[调试](#dbg)本教程结尾部分。

## <a name="basics-of-the-graph-api"></a>图形 API 的基础知识

[Graph API](https://msdn.microsoft.com/library/azure/hh974476.aspx)是用来在 Azure AD 目录中执行 CRUD 和其他对象操作的编程接口。 如果在 Visual Studio 2013 中创建一个新项目时选择一个用于身份验证的组织帐户选项，你的应用程序将已配置为调用图形 API。 本部分简要介绍 Graph API 的工作原理。

1. 在运行的应用程序，单击顶部的登录用户名称页面右上角。 这将转到用户配置文件页上，这是在主页控制器上的操作。 您会注意到表中包含前面创建的管理员帐户相关的用户信息。 此信息存储在你的目录，并调用图形 API 在页面加载时检索此信息。   
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image15.png)
2. 返回到 Visual Studio 并展开**控制器**文件夹，然后打开**HomeController.cs**文件。 你将看到**UserProfile()** 包含用于检索令牌，然后调用图形 API 的代码的操作。 下面被复制此代码： 

    [!code-csharp[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample1.cs?highlight=22)]

    若要调用 Graph API，首先需要检索令牌。 当检索令牌时，必须在对 Graph API 的所有后续请求的 Authorization 标头中附加其字符串值。 上面的代码的大部分处理向 Azure AD 获取的令牌进行身份验证，使用该令牌调用图形 API，然后转换响应，以便它可以在视图中显示的详细信息。

    有关讨论最相关的部分是以下突出显示的行： `UserProfile profile = JsonConvert.DeserializeObject<UserProfile>(responseString);`。 此行表示的用户，它具有 JSON 响应中反序列化并在视图中显示的名称。

    您可以调用图形 API 使用 HttpClient 自己并处理原始数据，但更简单的方法是使用[Graph 客户端库可通过 NuGet](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/)。 客户端库处理原始 HTTP 请求和返回数据的转换，并使其更容易使用 Graph API 在.NET 环境中处理。 请参阅上相关的 Graph API 代码示例[GitHub。](https://github.com/AzureADSamples)

## <a name="deploy-the-application-to-azure"></a>部署到 Azure 应用程序

以下步骤将演示如何部署到 Azure 应用程序。 在前面步骤中，将新项目连接与 web 应用在 Azure 上，以便随时可在几个步骤中发布。

1. 在 Visual Studio 中，右键单击项目并选择**发布**。 **发布 Web**对话框将显示与每个已配置的设置。 单击**下一步**按钮以转到**设置**页。 系统可能会提示进行身份验证;请确保使用你的 Azure 订阅帐户 （通常是 Microsoft 帐户） 而不是前面创建的组织帐户进行验证。  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image16.png)
2. 检查**启用组织身份验证**选项。 在中**域**字段中，输入目录的域。 从**访问级别**下拉列表中，选择**单一登录，读取目录数据**。 您会注意到已填入以前所用的数据库**数据库**部分。 单击“发布” 。  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image17.png)
3. Visual Studio 将开始部署你的网站，然后将出现一个新的浏览器窗口。 您可能会提示进行身份验证到你的目录中再一次。 一旦您已通过身份验证，你将重定向到 Azure 上新发布的网站。  
  
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image18.png)

<a id="dbg"></a>
## <a name="debugging-the-app"></a>调试应用

如果收到以下错误：   
 值不能为 null 或为空。 参数名称： linkText   
   
![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image19.png)  
  

中的代码替换*views/shared\\_LoginPartial.cshtml*具有以下文件：

[!code-cshtml[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample2.cshtml?highlight=1-8,15-16)]

运行应用程序中后, 如果登录的用户显示"Null 用户"，请注销，并使用前面创建的 Active Directory 帐户重新登录。

若要遵循的精彩教程是 Rick Rainey[深入了解： Azure 网站和组织使用 Azure AD 的身份验证](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)。

## <a name="more-information"></a>详细信息

- [深入探讨： Azure 网站和组织使用 Azure AD 的身份验证](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)
- [Azure AD Graph API 概述](https://msdn.microsoft.com/library/azure/hh974476.aspx)
- [Azure AD 中的身份验证方案](https://msdn.microsoft.com/library/azure/dn499820.aspx)
- [GitHub 上的 azure AD 代码示例](https://github.com/AzureADSamples)
