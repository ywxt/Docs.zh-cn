---
uid: visual-studio/overview/2012/windows-azure-authentication
title: Windows Azure 身份验证 |Microsoft Docs
author: Rick-Anderson
description: Microsoft ASP.NET tools for Windows Azure Active Directory 可以轻松地为托管 Windows Azure 网站上的 web 应用程序启用身份验证...
ms.author: aspnetcontent
ms.date: 02/20/2013
ms.assetid: a3cef801-a54b-4ebd-93c3-55764e2e14b1
msc.legacyurl: /visual-studio/overview/2012/windows-azure-authentication
msc.type: authoredcontent
ms.openlocfilehash: e3443fb627dc8d7d5011341828556b4c13836170
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37812804"
---
<a name="windows-azure-authentication"></a>Windows Azure 身份验证
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> Microsoft ASP.NET 工具为 Windows Azure Active Directory 简化为上托管的 web 应用程序启用身份验证[Windows Azure Web Sites](https://www.windowsazure.com/home/features/web-sites/)。 可以使用 Windows Azure 身份验证从您的组织，从你的本地 Active Directory 同步的公司帐户或在自定义 Windows Azure Active Directory 域中创建用户的 Office 365 用户进行身份验证。 启用 Windows Azure 身份验证，可配置你的应用程序使用单个用户进行身份验证[Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)租户。
> 
> 对于云服务中的 web 角色不支持 ASP.NET Windows Azure 身份验证工具，但我们计划将来的版本中执行此操作。 [Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF) 支持在 Windows Azure web 角色中。
> 
> 有关如何设置你的本地 Active Directory 和 Windows Azure Active Directory 租户之间的同步的详细信息请参阅[使用 AD FS 2.0 实现和管理单一登录](https://technet.microsoft.com/library/jj205462.aspx)。
> 
> Windows Azure Active Directory 是目前只有[免费预览服务](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。


## <a name="requirements"></a>要求：

- Visual Studio 2012 或[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)
- [Web 工具扩展适用于 Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409)或[Web 工具扩展的 Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)
- [Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306)或[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a>使用 Visual Studio 2012 中创建 ASP.NET Web 应用程序

您可以使用 Visual Studio 2012 创建的任何 Web 应用程序，本教程使用 ASP.NET MVC intranet 模板。

1. 创建新 ASP.NET MVC 4 Intranet 应用程序并接受所有默认值。 (它必须是 In **tra** net 而不是在**次**net 项目)。  
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a>启用 Window Azure 身份验证 （如果你是全局管理员的原则）

如果没有现有的 Windows Azure Active Directory 租户 （例如，通过现有的 Office 365 帐户） 可以通过注册来创建新租户[新的 Windows Azure Active Directory 帐户](http://g.microsoftonline.com/0AX00en/5)。

1. 从项目菜单中选择**启用 Windows Azure 身份验证**:  
  
   ![](windows-azure-authentication/_static/image2.png)

2. 为 Windows Azure Active Directory 租户 (例如，contoso.onmicrosoft.com) 输入域，然后单击**启用**:

![](windows-azure-authentication/_static/image3.png)

3. 中的 Web 身份验证对话框登录到 Windows Azure Active Directory 租户管理员的身份：  
  
   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a>通过非管理员的原则来启用 Window Azure

如果您没有 Windows Azure Active Directory 租户的全局管理员特权，可以取消选中预配应用程序复选框。

![](windows-azure-authentication/_static/image6.png)

该对话框将显示**域**，**应用程序主体 Id**并**回复 URL**为预配使用 Azure Active Directory 应用程序所需的原则。 您需要将此信息提供给具有足够的特权来设置应用程序的人员。 请参阅[如何实现与 Windows Azure Active Directory 的 ASP.NET 应用程序的单一登录](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)有关如何使用 cmdlet 来手动创建服务主体的详细信息。  
已成功预配应用程序，你可以单击**继续使用所选的设置更新 web.config**。 如果你想要继续开发应用程序，同时等待发生这种情况，可以单击预配**接近记住项目文件中的设置**。 下一次调用启用 Windows Azure 身份验证并取消选中预配复选框，您将看到相同的设置，可以单击**继续**，然后单击，**应用这些设置在 web.config**.

1. 当你的应用程序配置为 Windows Azure 身份验证并使用 Windows Azure Active Directory 预配时，等待。
2. 一旦为应用程序启用了 Windows Azure 身份验证，请单击**关闭：** 

    ![](windows-azure-authentication/_static/image7.png)
3. 按 F5 运行应用程序。 你应会自动获取重定向到登录页。 使用目录原则用户凭据登录到应用程序...  

    ![](windows-azure-authentication/_static/image1.jpg)
4. 因为你的应用程序当前使用的自签名的测试证书将从该证书不由受信任的证书颁发机构颁发的浏览器中收到警告。

    此警告可以安全地忽略在本地开发期间通过单击**继续浏览此网站：** 

    ![](windows-azure-authentication/_static/image8.png)
5. 现在已成功登录到使用 Windows Azure 身份验证的应用程序 ！

    ![](windows-azure-authentication/_static/image2.jpg)

启用 Windows Azure 身份验证到您的应用程序进行以下更改：

- 防跨站点请求伪造 ([CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) 类 (*应用\_Start\AntiXsrfConfig.cs* ) 添加到你的项目。
- NuGet 包`System.IdentityModel.Tokens.ValidatingIssuerNameRegistry`添加到你的项目。
- 在应用程序中的 Windows Identity Foundation 设置将配置为接受来自 Windows Azure Active Directory 租户的安全令牌。 单击下面以查看所做的更改的扩展的视图图像*Web.config*文件。  
  
     ![](windows-azure-authentication/_static/image9.png)
- 在 Windows Azure Active Directory 租户中的应用程序的服务主体将其预配。
- 启用 HTTPS。

## <a name="deploy-the-application-to-windows-azure"></a>部署到 Windows Azure 应用程序

有关完整说明，请参阅[ASP.NET Web 应用程序到 Windows Azure 网站部署](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)。

若要发布使用 Windows Azure 身份验证到 Azure 网站的应用程序：

1. 右键单击你的应用程序并选择**发布：** 

    ![](windows-azure-authentication/_static/image3.jpg)
2. 从发布 Web 对话框中下载并导入发布配置文件的 Azure Web 站点。

    ![](windows-azure-authentication/_static/image4.jpg)
3. **连接**选项卡显示**目标 URL** （公共面向在应用程序的 URL)。 单击**验证连接**要测试连接：

    ![](windows-azure-authentication/_static/image5.jpg)
4. 如果已发布到此 Azure 网站之前，请考虑检查**删除目标处的其他文件**完全发布设置，以确保你的应用程序。 请注意**启用 Windows Azure 身份验证**复选框，则 slected。  

    ![](windows-azure-authentication/_static/image10.png)
5. 可选： 在**预览版**选项卡上单击**开始预览**以查看部署的文件。

    ![](windows-azure-authentication/_static/image6.jpg)
6. 单击**发布。**

    系统将提示您为目标主机启用 Windows Azure 身份验证。 单击**启用**以继续：

    ![](windows-azure-authentication/_static/image11.png)
7. 输入你的 Windows Azure Active Directory 租户管理员凭据：

    ![](windows-azure-authentication/_static/image7.jpg)
8. 你的应用程序已成功发布后，浏览器将打开到已发布的网站。

    > [!NOTE]
    > 它可能需要最多 5 分钟 （通常必须更少） 为目标主机的启用 Windows Azure 身份验证后要使用 Windows Azure Active Directory 完全设置应用程序。 当你首次运行应用程序如果收到错误 ACS50001： 找不到名称 [realm] 的信赖方，然后等待几分钟，并重试运行一次应用程序。
9. 出现提示时，请为你的目录中的用户登录：

    ![](windows-azure-authentication/_static/image8.jpg)
10. 现在已成功登录到你的 Azure 托管应用程序使用 Windows Azure 身份验证。  
  
     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a>已知问题

#### <a name="role-based-authorization-fails-when-using-windows-azure-authenticationopop"></a>基于角色的授权失败时使用 Windows Azure 身份验证 < o:p >< / o:p >

Windows Azure 身份验证当前不提供必要的角色声明，以便可以执行基于角色的授权。 必须从 Windows Azure Active Directory。 < o:p >< 手动检索经过身份验证的用户的角色 / o:p >

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-stsopop"></a>浏览到包含 Windows Azure 身份验证会导致错误的应用程序"ACS20016 登录用户 (live.com) 的域不匹配任何允许的域的 STS"< o:p >< / o:p >

如果已登录到 Microsoft 帐户 （例如 hotmail.com、 live.com、 outlook.com） 并尝试访问的应用程序启用了 Windows Azure 身份验证，因为可能会收到 400 错误响应你的 Microsoft 帐户的域无法识别由 Windows Azure Active Directory。 若要登录到应用程序，从注销你的 Microsoft 帐户第一次。 < o:p >< / o:p >

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificateopop"></a>登录到 Windows Azure 身份验证启用包含的应用程序和 X509CertificateValidationMode 以外无导致证书验证错误的 accounts.accesscontrol.windows.net 证书 < o:p >< / o:p >

证书验证不是必需的并应处于禁用状态。 颁发者证书的指纹验证 WSFederationAuthenticationModule。 < o:p >< / o:p >

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-stsopop"></a>尝试启用 Windows Azure 身份验证时将 Web 身份验证对话框会显示错误"ACS20016： 登录用户 (contoso.onmicrosoft.com) 的域与此 STS 的允许的任何域不匹配。"< o:p >< / o:p >

当你之前已成功登录使用相同的 Visual Studio 进程内不同的 Windows Azure Active Directory 帐户，会看到此错误。 从指定的帐户注销或重启 Visual Studio。 如果你以前在中记录并选择"使我保持登录"选项则可能需要清除浏览器 cookie。 < o:p >< / o:p >

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message-opop"></a>ACS20012： 请求不是有效的 WS 联合身份验证协议消息 < o:p >< / o:p >

如果已登录到 Azure 服务之一的某个其他 Microsoft ID，则可能发生此问题。 使用专用浏览器窗口中，例如在 IE 中的 InPrivate 或 chrome Incognito 或清除所有 cookie。 < o:p >< / o:p >

## <a name="additional-resources"></a>其他资源

- [Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci
- [Windows Azure 功能： 标识](https://docs.microsoft.com/azure/active-directory/)
- [TechNet: Windows Azure Active Directory](https://technet.microsoft.com/library/hh967619.aspx)
- [Windows Azure Active Directory： 开发适用于你的组织应用](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [Windows Azure Active Directory： 开发适用于多个组织应用](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [如何实现与 Windows Azure Active Directory 的单一登录](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- [单一登录使用 Windows Azure Active Directory： 深入探讨](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx)– Vittorio Bertocci
- [使用 AD FS 2.0 实现和管理单一登录](https://technet.microsoft.com/library/jj205462.aspx)
