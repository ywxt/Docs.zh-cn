---
uid: visual-studio/overview/2012/windows-azure-authentication
title: Windows Azure 身份验证 |Microsoft 文档
author: Rick-Anderson
description: Microsoft ASP.NET tools for Windows Azure Active Directory 可以简单，以使托管 Windows Azure 网站上的 web 应用程序的身份验证...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2013
ms.topic: article
ms.assetid: a3cef801-a54b-4ebd-93c3-55764e2e14b1
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2012/windows-azure-authentication
msc.type: authoredcontent
ms.openlocfilehash: 09cb37ceb0132958a48f5f3a5d52dc46c6f0a78d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="windows-azure-authentication"></a><span data-ttu-id="d55c3-103">Windows Azure 身份验证</span><span class="sxs-lookup"><span data-stu-id="d55c3-103">Windows Azure Authentication</span></span>
====================
<span data-ttu-id="d55c3-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="d55c3-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="d55c3-105">Microsoft ASP.NET 工具为 Windows Azure Active Directory 可以很容易地为上托管的 web 应用程序启用身份验证[Windows Azure 网站](https://www.windowsazure.com/home/features/web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="d55c3-105">Microsoft ASP.NET tools for Windows Azure Active Directory makes it simple to enable authentication for web applications hosted on [Windows Azure Web Sites](https://www.windowsazure.com/home/features/web-sites/).</span></span> <span data-ttu-id="d55c3-106">可以使用 Windows Azure 身份验证从组织、 从本地 Active Directory 同步的公司帐户或用户在你自己的自定义 Windows Azure Active Directory 域中创建的 Office 365 用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="d55c3-106">You can use Windows Azure Authentication to authenticate Office 365 users from your organization, corporate accounts synced from your on-premise Active Directory or users created in your own custom Windows Azure Active Directory domain.</span></span> <span data-ttu-id="d55c3-107">启用 Windows Azure 身份验证配置你的应用程序使用单个的用户进行身份验证[Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)租户。</span><span class="sxs-lookup"><span data-stu-id="d55c3-107">Enabling Windows Azure Authentication configures your application to authenticate users using a single [Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) tenant.</span></span>
> 
> <span data-ttu-id="d55c3-108">对于云服务中的 web 角色不支持 ASP.NET Windows Azure 身份验证工具，但我们计划在将来的版本中这样做。</span><span class="sxs-lookup"><span data-stu-id="d55c3-108">The ASP.NET Windows Azure Authentication tool is not supported for web roles in a cloud service but we plan to do so in a future release.</span></span> <span data-ttu-id="d55c3-109">[Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF) 支持在 Windows Azure web 角色。</span><span class="sxs-lookup"><span data-stu-id="d55c3-109">[Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF) is supported in Windows Azure web roles.</span></span>
> 
> <span data-ttu-id="d55c3-110">有关如何设置您的本地 Active Directory 和 Windows Azure Active Directory 租户之间的同步的详细信息请参阅[使用 AD FS 2.0 实现和管理单一登录](https://technet.microsoft.com/library/jj205462.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d55c3-110">For details on how to setup synchronization between your on-premise Active Directory and your Windows Azure Active Directory tenant please see [Use AD FS 2.0 to implement and manage single sign-on](https://technet.microsoft.com/library/jj205462.aspx).</span></span>
> 
> <span data-ttu-id="d55c3-111">Windows Azure Active Directory 是目前只有[免费预览版 service](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="d55c3-111">Windows Azure Active Directory is currently available as a [free preview service](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>


## <a name="requirements"></a><span data-ttu-id="d55c3-112">要求：</span><span class="sxs-lookup"><span data-stu-id="d55c3-112">Requirements:</span></span>

- <span data-ttu-id="d55c3-113">Visual Studio 2012 or [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)</span><span class="sxs-lookup"><span data-stu-id="d55c3-113">Visual Studio 2012 or [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)</span></span>
- <span data-ttu-id="d55c3-114">[Web 工具扩展 Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409)或[Web 工具扩展 for Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="d55c3-114">[Web Tools Extensions for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409) or [Web Tools Extensions for Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)</span></span>
- <span data-ttu-id="d55c3-115">[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306)或[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)</span><span class="sxs-lookup"><span data-stu-id="d55c3-115">[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306) or [Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)</span></span>

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a><span data-ttu-id="d55c3-116">使用 Visual Studio 2012 创建的 ASP.NET Web 应用</span><span class="sxs-lookup"><span data-stu-id="d55c3-116">Create an ASP.NET Web Application with Visual Studio 2012</span></span>

<span data-ttu-id="d55c3-117">你可以使用 Visual Studio 2012 创建任何 Web 应用程序，本教程使用 ASP.NET MVC intranet 模板。</span><span class="sxs-lookup"><span data-stu-id="d55c3-117">You can create any Web Application with Visual Studio 2012, this tutorial uses the ASP.NET MVC intranet template.</span></span>

1. <span data-ttu-id="d55c3-118">创建新的 ASP.NET MVC 4 Intranet 应用程序，接受所有默认值。</span><span class="sxs-lookup"><span data-stu-id="d55c3-118">Create a new ASP.NET MVC 4 Intranet Application and accept all the defaults.</span></span> <span data-ttu-id="d55c3-119">(它必须是 In**遍历**net 而不是在**ter** net 项目)。</span><span class="sxs-lookup"><span data-stu-id="d55c3-119">(It must be an In **tra** net and not In **ter** net project).</span></span>  
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a><span data-ttu-id="d55c3-120">启用窗口 Azure 身份验证 （如果你是原则全局管理员）</span><span class="sxs-lookup"><span data-stu-id="d55c3-120">Enable Window Azure Authentication (When you are a Global Administrator of the Tenet)</span></span>

<span data-ttu-id="d55c3-121">如果你没有现有的 Windows Azure Active Directory 租户 （例如，通过现有 Office 365 帐户） 可以通过注册创建新租户[新的 Windows Azure Active Directory 帐户](http://g.microsoftonline.com/0AX00en/5)。</span><span class="sxs-lookup"><span data-stu-id="d55c3-121">If you do not have an existing Windows Azure Active Directory tenant (For example, through an existing Office 365 account) you can create a new tenant by signing up for a [new Windows Azure Active Directory account](http://g.microsoftonline.com/0AX00en/5).</span></span>

1. <span data-ttu-id="d55c3-122">从项目菜单上选择**启用 Windows Azure 身份验证**:</span><span class="sxs-lookup"><span data-stu-id="d55c3-122">From the Project menu select **Enable Windows Azure Authentication**:</span></span>  
  
   ![](windows-azure-authentication/_static/image2.png)

2. <span data-ttu-id="d55c3-123">为你的 Windows Azure Active Directory 租户 (例如，contoso.onmicrosoft.com) 输入域，然后单击**启用**:</span><span class="sxs-lookup"><span data-stu-id="d55c3-123">Enter the domain for your Windows Azure Active Directory tenant (for example, contoso.onmicrosoft.com) and click **Enable**:</span></span>

![](windows-azure-authentication/_static/image3.png)

3. <span data-ttu-id="d55c3-124">Web 身份验证对话框在登录中作为 Windows Azure Active Directory 租户的管理员：</span><span class="sxs-lookup"><span data-stu-id="d55c3-124">In the Web Authentication dialog sign in as an administrator for your Windows Azure Active Directory tenant:</span></span>  
  
   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a><span data-ttu-id="d55c3-125">启用非管理员的原则 Window Azure</span><span class="sxs-lookup"><span data-stu-id="d55c3-125">Enable Window Azure by a non-administrator of the Tenet</span></span>

<span data-ttu-id="d55c3-126">如果你没有 Windows Azure Active Directory 租户全局管理员特权，可以取消选中复选框设置应用程序。</span><span class="sxs-lookup"><span data-stu-id="d55c3-126">If you do not have Global Administrator privilege for your Windows Azure Active Directory tenant, you can uncheck the checkbox for provisioning the application.</span></span>

![](windows-azure-authentication/_static/image6.png)

<span data-ttu-id="d55c3-127">该对话框将显示**域**，**应用程序主体 Id**和**答复 URL**其所需的设置与 Azure Active Directory 应用程序原则。</span><span class="sxs-lookup"><span data-stu-id="d55c3-127">The dialog will display the **Domain**, **Application Principal Id** and **Reply URL** which are required for provisioning the application with an Azure Active Directory tenet.</span></span> <span data-ttu-id="d55c3-128">你需要将此信息提供给具有足够的特权来设置应用程序的人员。</span><span class="sxs-lookup"><span data-stu-id="d55c3-128">You need to give this information to someone who has sufficient privilege to provision the application.</span></span> <span data-ttu-id="d55c3-129">请参阅[如何实现与 Windows Azure Active Directory 的 ASP.NET 应用程序的单一登录](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)有关如何使用 cmdlet 来手动创建服务主体的详细信息。</span><span class="sxs-lookup"><span data-stu-id="d55c3-129">See[How to implement single sign-on with Windows Azure Active Directory - ASP.NET Application](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) for details on how to use cmdlet to create the service principal manually.</span></span>  
<span data-ttu-id="d55c3-130">一旦成功设置应用程序后，你可以单击**继续使用所选设置更新 web.config**。</span><span class="sxs-lookup"><span data-stu-id="d55c3-130">Once the application has been successfully provisioned, you can click on **Continue to update web.config with the selected settings**.</span></span> <span data-ttu-id="d55c3-131">如果你想要在继续开发应用程序同时等待预配，发生这种情况，你可以单击**接近记住项目文件中的设置**。</span><span class="sxs-lookup"><span data-stu-id="d55c3-131">If you want to continue developing the application while waiting for provisioning to happen, you can click **Close to remember the settings in project file**.</span></span> <span data-ttu-id="d55c3-132">下一次调用启用 Windows Azure 身份验证并取消选中设置复选框，你将看到相同的设置，可以单击**继续**，然后单击，**应用这些设置在 web.config**.</span><span class="sxs-lookup"><span data-stu-id="d55c3-132">The next time you invoke Enable Windows Azure Authentication and uncheck the provisioning checkbox, you will see the same settings and you can click **Continue**, then click, **Apply these settings in web.config**.</span></span>

1. <span data-ttu-id="d55c3-133">为 Windows Azure 身份验证配置你的应用程序并将其设置与 Windows Azure Active Directory 请稍候。</span><span class="sxs-lookup"><span data-stu-id="d55c3-133">Wait while your application is configured for Windows Azure Authentication and provisioned with Windows Azure Active Directory.</span></span>
2. <span data-ttu-id="d55c3-134">Windows Azure 身份验证启用你的应用程序后，单击**关闭：**</span><span class="sxs-lookup"><span data-stu-id="d55c3-134">Once Windows Azure Authentication has been enabled for your application, click **Close:**</span></span> 

    ![](windows-azure-authentication/_static/image7.png)
3. <span data-ttu-id="d55c3-135">按 F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="d55c3-135">Hit F5 to run your application.</span></span> <span data-ttu-id="d55c3-136">你应自动获取重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="d55c3-136">You should automatically get redirected to login page.</span></span> <span data-ttu-id="d55c3-137">使用目录原则用户凭据登录到应用程序...</span><span class="sxs-lookup"><span data-stu-id="d55c3-137">Use the directory tenet user credentials to login to the application..</span></span>  

    ![](windows-azure-authentication/_static/image1.jpg)
4. <span data-ttu-id="d55c3-138">因为你的应用程序当前使用的自签名的测试证书你将收到一条警告，来自的浏览器的证书不由受信任的证书颁发机构颁发。</span><span class="sxs-lookup"><span data-stu-id="d55c3-138">Because your application is currently using a self-signed test certificate you will receive a warning from the browser that the certificate was not issued by a trusted certificate authority.</span></span>

    <span data-ttu-id="d55c3-139">忽略此警告可以安全地在本地开发期间通过单击**继续访问此网站：**</span><span class="sxs-lookup"><span data-stu-id="d55c3-139">This warning can be safely ignored during local development by clicking **Continue to this website:**</span></span> 

    ![](windows-azure-authentication/_static/image8.png)
5. <span data-ttu-id="d55c3-140">你现在已成功登录到你使用 Windows Azure 身份验证的应用程序 ！</span><span class="sxs-lookup"><span data-stu-id="d55c3-140">You have now successfully logged in to your application using Windows Azure Authentication!</span></span>

    ![](windows-azure-authentication/_static/image2.jpg)

<span data-ttu-id="d55c3-141">启用 Windows Azure 身份验证将为你的应用程序做出以下更改：</span><span class="sxs-lookup"><span data-stu-id="d55c3-141">Enabling Windows Azure authentication makes the following changes to your application:</span></span>

- <span data-ttu-id="d55c3-142">防跨站点请求伪造 ([CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) 类 (*应用\_Start\AntiXsrfConfig.cs* ) 添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="d55c3-142">An Anti-Cross-Site Request Forgery ([CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) class ( *App\_Start\AntiXsrfConfig.cs* ) is added to your project.</span></span>
- <span data-ttu-id="d55c3-143">NuGet 包`System.IdentityModel.Tokens.ValidatingIssuerNameRegistry`添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="d55c3-143">The NuGet packages `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` is added to your project.</span></span>
- <span data-ttu-id="d55c3-144">你的应用程序中的 Windows Identity Foundation 设置将配置为接受来自 Windows Azure Active Directory 租户的安全令牌。</span><span class="sxs-lookup"><span data-stu-id="d55c3-144">Windows Identity Foundation settings in your application will be configured to accept security tokens from your Windows Azure Active Directory tenant.</span></span> <span data-ttu-id="d55c3-145">单击下图所示，若要查看对所做的更改的扩展的视图*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d55c3-145">Click on the image below to see an expanded view of the changes made to the *Web.config* file.</span></span>  
  
     ![](windows-azure-authentication/_static/image9.png)
- <span data-ttu-id="d55c3-146">将设置你的 Windows Azure Active Directory 租户中的应用程序服务主体。</span><span class="sxs-lookup"><span data-stu-id="d55c3-146">A service principal for your application in your Windows Azure Active Directory tenant will be provisioned.</span></span>
- <span data-ttu-id="d55c3-147">启用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d55c3-147">HTTPS is enabled.</span></span>

## <a name="deploy-the-application-to-windows-azure"></a><span data-ttu-id="d55c3-148">部署到 Windows Azure 应用程序</span><span class="sxs-lookup"><span data-stu-id="d55c3-148">Deploy the application to Windows Azure</span></span>

<span data-ttu-id="d55c3-149">有关完整说明，请参阅[部署 ASP.NET Web 应用程序到 Windows Azure 网站](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="d55c3-149">For complete instructions, see [Deploying an ASP.NET Web Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span>

<span data-ttu-id="d55c3-150">若要发布使用 Windows Azure 身份验证到 Azure 网站的应用程序：</span><span class="sxs-lookup"><span data-stu-id="d55c3-150">To publish an application using Windows Azure Authentication to an Azure Web Site:</span></span>

1. <span data-ttu-id="d55c3-151">右键单击你的应用程序并选择**发布：**</span><span class="sxs-lookup"><span data-stu-id="d55c3-151">Right click on your application and select **Publish:**</span></span> 

    ![](windows-azure-authentication/_static/image3.jpg)
2. <span data-ttu-id="d55c3-152">从发布 Web 对话框中，下载并导入发布配置文件为你 Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="d55c3-152">From the Publish Web dialog download and import a publishing profile for your Azure Web Site.</span></span>

    ![](windows-azure-authentication/_static/image4.jpg)
3. <span data-ttu-id="d55c3-153">**连接**选项卡上显示**目标 URL** (你的应用程序的公共面向 URL)。</span><span class="sxs-lookup"><span data-stu-id="d55c3-153">The **Connection** tab shows the **Destination URL** (the public facing URL for your application).</span></span> <span data-ttu-id="d55c3-154">单击**验证连接**来测试连接：</span><span class="sxs-lookup"><span data-stu-id="d55c3-154">Click **Validate Connection** to test your connection:</span></span>

    ![](windows-azure-authentication/_static/image5.jpg)
4. <span data-ttu-id="d55c3-155">如果你已将发布到此 Azure 网站之前，请考虑检查**删除目标位置的其他文件**完全发布设置，以确保你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d55c3-155">If you have published to this Azure Web Site previously consider checking the **Remove additional files at destination** setting to ensure your application publishes cleanly.</span></span> <span data-ttu-id="d55c3-156">请注意**启用 Windows Azure 身份验证**复选框，则 slected。</span><span class="sxs-lookup"><span data-stu-id="d55c3-156">Notice the **Enable Windows Azure Authentication** check box is slected.</span></span>  

    ![](windows-azure-authentication/_static/image10.png)
5. <span data-ttu-id="d55c3-157">可选： 在**预览**选项卡上单击**开始预览**若要查看部署的文件。</span><span class="sxs-lookup"><span data-stu-id="d55c3-157">Optional: On the **Preview** tab click **Start Preview** to see the files deployed.</span></span>

    ![](windows-azure-authentication/_static/image6.jpg)
6. <span data-ttu-id="d55c3-158">单击**发布。**</span><span class="sxs-lookup"><span data-stu-id="d55c3-158">Click **Publish.**</span></span>

    <span data-ttu-id="d55c3-159">将提示你为目标主机启用 Windows Azure 身份验证。</span><span class="sxs-lookup"><span data-stu-id="d55c3-159">You will be prompted to enable Windows Azure Authentication for the target host.</span></span> <span data-ttu-id="d55c3-160">单击**启用**继续：</span><span class="sxs-lookup"><span data-stu-id="d55c3-160">Click **Enable** to continue:</span></span>

    ![](windows-azure-authentication/_static/image11.png)
7. <span data-ttu-id="d55c3-161">为你的 Windows Azure Active Directory 租户中输入你的管理员凭据：</span><span class="sxs-lookup"><span data-stu-id="d55c3-161">Enter your administrator credentials for your Windows Azure Active Directory tenant:</span></span>

    ![](windows-azure-authentication/_static/image7.jpg)
8. <span data-ttu-id="d55c3-162">你的应用程序已成功发布后，浏览器将打开到已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="d55c3-162">Once your application has been successfully published, a browser will open to the published web site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d55c3-163">它可能需要应用程序，才能完全与 Windows Azure Active Directory 设置为目标主机中启用 Windows Azure 身份验证后最多 5 分钟 （通常必须更少）。</span><span class="sxs-lookup"><span data-stu-id="d55c3-163">It may take up to five minutes (typically must less) for your application to be fully provisioned with Windows Azure Active Directory after enabling Windows Azure Authentication for the target host.</span></span> <span data-ttu-id="d55c3-164">当你首次运行你的应用程序如果您收到错误 ACS50001： 找不到名称 [领域] 的信赖方，然后等待几分钟，并重试运行一次，应用程序。</span><span class="sxs-lookup"><span data-stu-id="d55c3-164">When you first run your application if you receive error ACS50001: Relying party with name ‘[realm]' was not found, then wait a few minutes and try running the application again.</span></span>
9. <span data-ttu-id="d55c3-165">出现提示时，请为你的目录中的用户登录：</span><span class="sxs-lookup"><span data-stu-id="d55c3-165">When prompted, log in as a user in your directory:</span></span>

    ![](windows-azure-authentication/_static/image8.jpg)
10. <span data-ttu-id="d55c3-166">您现在已成功登录到你的 Azure 托管应用程序使用 Windows Azure 身份验证。</span><span class="sxs-lookup"><span data-stu-id="d55c3-166">You have now successfully logged into your Azure hosted application using Windows Azure Authentication.</span></span>  
  
     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a><span data-ttu-id="d55c3-167">已知问题</span><span class="sxs-lookup"><span data-stu-id="d55c3-167">Known Issues</span></span>

#### <a name="role-based-authorization-fails-when-using-windows-azure-authenticationopop"></a><span data-ttu-id="d55c3-168">使用 Windows Azure 身份验证 < o:p >< 时，基于角色的授权失败 / o:p ></span><span class="sxs-lookup"><span data-stu-id="d55c3-168">Role-based authorization fails when using Windows Azure Authentication<o:p></o:p></span></span>

<span data-ttu-id="d55c3-169">Windows Azure 身份验证当前不提供必需的角色声明，以便可以执行基于角色的授权。</span><span class="sxs-lookup"><span data-stu-id="d55c3-169">Windows Azure Authentication does not currently provide the necessary role claim so that role-based authorization can be performed.</span></span> <span data-ttu-id="d55c3-170">经过身份验证的用户的角色必须手动从检索 Windows Azure Active Directory。 < o:p >< / o:p ></span><span class="sxs-lookup"><span data-stu-id="d55c3-170">The role of the authenticated user must be manually retrieved from Windows Azure Active Directory.<o:p></o:p></span></span>

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-stsopop"></a><span data-ttu-id="d55c3-171">浏览到错误中的 Windows Azure 身份验证结果的应用程序"在已登录用户 (live.com) 的域的不匹配任何 ACS20016 允许此域 STS"< o:p >< / o:p ></span><span class="sxs-lookup"><span data-stu-id="d55c3-171">Browsing to an application with Windows Azure Authentication results in the error "ACS20016 The domain of the logged in user (live.com) does not match any allowed domain of this STS"<o:p></o:p></span></span>

<span data-ttu-id="d55c3-172">如果您已登录到 Microsoft 帐户 （例如 hotmail.com、 live.com、 outlook.com） 并尝试访问的应用程序启用了 Windows Azure 身份验证你可能会收到 400 错误响应，因为你的 Microsoft 帐户的域无法识别 Windows Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="d55c3-172">If you are already logged in to a Microsoft Account (for example hotmail.com, live.com, outlook.com) and you attempt to access an application that has enabled Windows Azure Authentication you may get a 400 error response because the domain of your Microsoft Account is not recognized by Windows Azure Active Directory.</span></span> <span data-ttu-id="d55c3-173">若要登录到应用程序，从注销你的 Microsoft 帐户第一次。 < o:p >< / o:p ></span><span class="sxs-lookup"><span data-stu-id="d55c3-173">To log into the application, log out from your Microsoft Account first.<o:p></o:p></span></span>

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificateopop"></a><span data-ttu-id="d55c3-174">登录到 Windows Azure 身份验证启用的应用程序和 X509CertificateValidationMode 以外无导致 accounts.accesscontrol.windows.net 证书 < o:p >< 的证书验证错误 / o:p ></span><span class="sxs-lookup"><span data-stu-id="d55c3-174">Logging into an application with Windows Azure Authentication enabled and a X509CertificateValidationMode other than None results in certificate validation errors for the accounts.accesscontrol.windows.net certificate<o:p></o:p></span></span>

<span data-ttu-id="d55c3-175">证书验证不是必需的并应处于已禁用。</span><span class="sxs-lookup"><span data-stu-id="d55c3-175">Certificate validation is not required and should be left disabled.</span></span> <span data-ttu-id="d55c3-176">颁发者证书的指纹验证。 WSFederationAuthenticationModule。 < o:p >< / o:p ></span><span class="sxs-lookup"><span data-stu-id="d55c3-176">The thumbprint of the issuer certificate is validated by the WSFederationAuthenticationModule.<o:p></o:p></span></span>

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-stsopop"></a><span data-ttu-id="d55c3-177">尝试启用 Windows Azure 身份验证时将 Web 身份验证对话框会显示错误"ACS20016： 在已登录用户 (contoso.onmicrosoft.com) 的域的此 STS 任何允许的域不匹配。"< o:p >< / o:p ></span><span class="sxs-lookup"><span data-stu-id="d55c3-177">When attempting to enable Windows Azure Authentication the Web Authentication dialog shows the error "ACS20016: The domain of the logged in user (contoso.onmicrosoft.com) does not match any allowed domain of this STS."<o:p></o:p></span></span>

<span data-ttu-id="d55c3-178">当你之前已成功登录使用相同的 Visual Studio 进程内不同的 Windows Azure Active Directory 帐户时，可能会看到此错误。</span><span class="sxs-lookup"><span data-stu-id="d55c3-178">You may see this error when you have previously successfully logged in using a different Windows Azure Active Directory account from within the same Visual Studio process.</span></span> <span data-ttu-id="d55c3-179">从指定的帐户注销或重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d55c3-179">Log out from the specified account or restart Visual Studio.</span></span> <span data-ttu-id="d55c3-180">如果您以前记录在中，选择"使我保持登录中"选项则可能需要清除浏览器 cookie。 < o:p >< / o:p ></span><span class="sxs-lookup"><span data-stu-id="d55c3-180">If you previously logged in and selected the option to "Keep me signed in" then you may need to clear your browser cookies.<o:p></o:p></span></span>

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message-opop"></a><span data-ttu-id="d55c3-181">ACS20012： 请求不是有效的 WS 联合身份验证协议消息 < o:p >< / o:p ></span><span class="sxs-lookup"><span data-stu-id="d55c3-181">ACS20012: The request is not a valid WS-Federation protocol message <o:p></o:p></span></span>

<span data-ttu-id="d55c3-182">如果你已登录到 Azure 服务之一的某些其他 Microsoft ID，也可能发生。</span><span class="sxs-lookup"><span data-stu-id="d55c3-182">This can happen if you are already logged in with some other Microsoft ID to one of the Azure services.</span></span> <span data-ttu-id="d55c3-183">使用专用浏览器窗口，例如在 IE 中的 InPrivate 或 Incognito Chrome 中的，或清除所有 cookie。</span><span class="sxs-lookup"><span data-stu-id="d55c3-183">Use Private browser window like InPrivate in IE or Incognito in Chrome or clear all the cookies.</span></span> <span data-ttu-id="d55c3-184"><o:p></o:p></span><span class="sxs-lookup"><span data-stu-id="d55c3-184"><o:p></o:p></span></span>

## <a name="additional-resources"></a><span data-ttu-id="d55c3-185">其他资源</span><span class="sxs-lookup"><span data-stu-id="d55c3-185">Additional Resources</span></span>

- <span data-ttu-id="d55c3-186">[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci</span><span class="sxs-lookup"><span data-stu-id="d55c3-186">[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci</span></span>
- [<span data-ttu-id="d55c3-187">Windows Azure 功能： 标识</span><span class="sxs-lookup"><span data-stu-id="d55c3-187">Windows Azure Features: Identity</span></span>](https://docs.microsoft.com/azure/active-directory/)
- [<span data-ttu-id="d55c3-188">TechNet: Windows Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d55c3-188">TechNet: Windows Azure Active Directory</span></span>](https://technet.microsoft.com/library/hh967619.aspx)
- [<span data-ttu-id="d55c3-189">Windows Azure Active Directory： 为你的组织中开发应用程序</span><span class="sxs-lookup"><span data-stu-id="d55c3-189">Windows Azure Active Directory: Develop Apps for your organization</span></span>](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [<span data-ttu-id="d55c3-190">Windows Azure Active Directory： 为多个组织中开发应用程序</span><span class="sxs-lookup"><span data-stu-id="d55c3-190">Windows Azure Active Directory: Develop Apps for multiple organizations</span></span>](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [<span data-ttu-id="d55c3-191">如何实现与 Windows Azure Active Directory 的单一登录</span><span class="sxs-lookup"><span data-stu-id="d55c3-191">How to implement single sign-on with Windows Azure Active Directory</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- <span data-ttu-id="d55c3-192">[单一登录与 Windows Azure Active Directory： 深入了解如何](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx)– Vittorio Bertocci</span><span class="sxs-lookup"><span data-stu-id="d55c3-192">[Single Sign-On with Windows Azure Active Directory: a Deep Dive](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) – Vittorio Bertocci</span></span>
- [<span data-ttu-id="d55c3-193">使用 AD FS 2.0 实现和管理单一登录</span><span class="sxs-lookup"><span data-stu-id="d55c3-193">Use AD FS 2.0 to implement and manage single sign-on</span></span>](https://technet.microsoft.com/library/jj205462.aspx)
