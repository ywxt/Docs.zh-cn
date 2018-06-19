---
uid: web-api/overview/security/external-authentication-services
title: 与 ASP.NET Web API 的外部身份验证服务 (C#) |Microsoft 文档
author: rmcmurray
description: 描述如何在 ASP.NET Web API 中使用外部身份验证服务。
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2013
ms.topic: article
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: 406a85db7055910cb7a4e15fec8ef68dff5a19dc
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30876262"
---
<a name="external-authentication-services-with-aspnet-web-api-c"></a><span data-ttu-id="d61d4-103">与 ASP.NET Web API 的外部身份验证服务 (C#)</span><span class="sxs-lookup"><span data-stu-id="d61d4-103">External Authentication Services with ASP.NET Web API (C#)</span></span>
====================
<span data-ttu-id="d61d4-104">通过[Robert McMurray](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="d61d4-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="d61d4-105">Visual Studio 2013 和 ASP.NET 4.5.1 展开的安全选项[单页面应用程序](../../../single-page-application/index.md)(SPA) 和[Web API](../../index.md)服务与外部身份验证服务，包括数种集成OAuth/OpenID 和社交媒体身份验证服务： Microsoft 帐户、 Twitter、 Facebook 和 Google。</span><span class="sxs-lookup"><span data-stu-id="d61d4-105">Visual Studio 2013 and ASP.NET 4.5.1 expand the security options for [Single Page Applications](../../../single-page-application/index.md) (SPA) and [Web API](../../index.md) services to integrate with external authentication services, which include several OAuth/OpenID and social media authentication services: Microsoft Accounts, Twitter, Facebook, and Google.</span></span>

### <a name="in-this-walkthrough"></a><span data-ttu-id="d61d4-106">在本演练中</span><span class="sxs-lookup"><span data-stu-id="d61d4-106">In This Walkthrough</span></span>

- [<span data-ttu-id="d61d4-107">使用外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="d61d4-107">Using External Authentication Services</span></span>](#USING)
- [<span data-ttu-id="d61d4-108">创建示例 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="d61d4-108">Creating the Sample Web Application</span></span>](#SAMPLE)
- [<span data-ttu-id="d61d4-109">启用 Facebook 身份验证</span><span class="sxs-lookup"><span data-stu-id="d61d4-109">Enabling Facebook Authentication</span></span>](#FACEBOOK)
- [<span data-ttu-id="d61d4-110">启用 Google 身份验证</span><span class="sxs-lookup"><span data-stu-id="d61d4-110">Enabling Google Authentication</span></span>](#GOOGLE)
- [<span data-ttu-id="d61d4-111">启用 Microsoft 身份验证</span><span class="sxs-lookup"><span data-stu-id="d61d4-111">Enabling Microsoft Authentication</span></span>](#MICROSOFT)
- [<span data-ttu-id="d61d4-112">启用 Twitter 身份验证</span><span class="sxs-lookup"><span data-stu-id="d61d4-112">Enabling Twitter Authentication</span></span>](#TWITTER)
- [<span data-ttu-id="d61d4-113">其他信息</span><span class="sxs-lookup"><span data-stu-id="d61d4-113">Additional Information</span></span>](#MOREINFO)

    - [<span data-ttu-id="d61d4-114">组合外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="d61d4-114">Combining External Authentication Services</span></span>](#COMBINE)
    - [<span data-ttu-id="d61d4-115">配置 IIS Express 以使用完全限定的域名</span><span class="sxs-lookup"><span data-stu-id="d61d4-115">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>](#FQDN)
    - [<span data-ttu-id="d61d4-116">如何获取 Microsoft 身份验证的应用程序设置</span><span class="sxs-lookup"><span data-stu-id="d61d4-116">How to Obtain your Application Settings for Microsoft Authentication</span></span>](#OBTAIN)
    - [<span data-ttu-id="d61d4-117">可选： 禁用本地注册</span><span class="sxs-lookup"><span data-stu-id="d61d4-117">Optional: Disable Local Registration</span></span>](#DISABLE)

### <a name="prerequisites"></a><span data-ttu-id="d61d4-118">系统必备</span><span class="sxs-lookup"><span data-stu-id="d61d4-118">Prerequisites</span></span>

<span data-ttu-id="d61d4-119">若要按照本演练中的示例，你需要具备以下：</span><span class="sxs-lookup"><span data-stu-id="d61d4-119">To follow the examples in this walkthrough, you need to have the following:</span></span>

- <span data-ttu-id="d61d4-120">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d61d4-120">Visual Studio 2013</span></span>
- <span data-ttu-id="d61d4-121">为至少一个以下外部身份验证服务帐户：</span><span class="sxs-lookup"><span data-stu-id="d61d4-121">An account for at least one of the following external authentication services:</span></span>

    - <span data-ttu-id="d61d4-122">Google 用户帐户</span><span class="sxs-lookup"><span data-stu-id="d61d4-122">A Google user account</span></span>
    - <span data-ttu-id="d61d4-123">开发人员帐户使用应用程序标识符和个以下的社交媒体身份验证服务的密钥：</span><span class="sxs-lookup"><span data-stu-id="d61d4-123">A developer account with the application identifier and secret key for one of the following social media authentication services:</span></span>

        - <span data-ttu-id="d61d4-124">Microsoft 帐户 ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span><span class="sxs-lookup"><span data-stu-id="d61d4-124">Microsoft Accounts ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span></span>
        - <span data-ttu-id="d61d4-125">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span><span class="sxs-lookup"><span data-stu-id="d61d4-125">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span></span>
        - <span data-ttu-id="d61d4-126">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span><span class="sxs-lookup"><span data-stu-id="d61d4-126">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span></span>

<a id="USING"></a>
## <a name="using-external-authentication-services"></a><span data-ttu-id="d61d4-127">使用外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="d61d4-127">Using External Authentication Services</span></span>

<span data-ttu-id="d61d4-128">丰富的 web 开发人员帮助以减少开发当前可用的外部身份验证服务创建新的 web 应用程序的时间。</span><span class="sxs-lookup"><span data-stu-id="d61d4-128">The abundance of external authentication services that are currently available to web developers help to reduce development time when creating new web applications.</span></span> <span data-ttu-id="d61d4-129">Web 用户通常具有多个现有帐户用于常用 web 服务和社交媒体网站，因此当身份验证的服务从外部 web 服务或社交媒体网站 web 应用程序实现的情况下，它将保存的开发时间，将所创建的身份验证实现已用。</span><span class="sxs-lookup"><span data-stu-id="d61d4-129">Web users typically have several existing accounts for popular web services and social media websites, therefore when a web application implements the authentication services from an external web service or social media website, it saves the development time that would have been spent creating an authentication implementation.</span></span> <span data-ttu-id="d61d4-130">使用外部身份验证服务将保存最终用户，从无需创建 web 应用程序，另一个帐户以及无需记住另一个用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="d61d4-130">Using an external authentication service saves end users from having to create another account for your web application, and also from having to remember another username and password.</span></span>

<span data-ttu-id="d61d4-131">在过去，开发人员有两个选项： 创建自己的身份验证实现，或了解如何将外部身份验证服务集成到其应用程序。</span><span class="sxs-lookup"><span data-stu-id="d61d4-131">In the past, developers have had two choices: create their own authentication implementation, or learn how to integrate an external authentication service into their applications.</span></span> <span data-ttu-id="d61d4-132">在最基本级别下, 图展示了简单的请求流正在从配置为使用外部身份验证服务的 web 应用程序请求信息的用户代理 （web 浏览器）：</span><span class="sxs-lookup"><span data-stu-id="d61d4-132">At the most basic level, the following diagram illustrates a simple request flow for a user agent (web browser) that is requesting information from a web application that is configured to use an external authentication service:</span></span>

<span data-ttu-id="d61d4-133">[![](external-authentication-services/_static/image2.png "单击以展开映像")](external-authentication-services/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-133">[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)</span></span>

<span data-ttu-id="d61d4-134">在前面的图中，情况下，用户代理 （或在此示例中的 web 浏览器） 发出请求的 web 应用程序，将 web 浏览器重定向到外部身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="d61d4-134">In the preceding diagram, the user agent (or web browser in this example) makes a request to a web application, which redirects the web browser to an external authentication service.</span></span> <span data-ttu-id="d61d4-135">用户代理会将其凭据发送到外部身份验证服务，并重如果用户代理已成功通过身份验证，外部身份验证服务将定向到使用某种形式的原始的 web 应用程序的用户代理标记其用户代理将发送到 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="d61d4-135">The user agent sends its credentials to the external authentication service, and if the user agent has successfully authenticated, the external authentication service will redirect the user agent to the original web application with some form of token which the user agent will send to the web application.</span></span> <span data-ttu-id="d61d4-136">Web 应用程序将使用该令牌来验证用户代理已成功验证外部身份验证服务和 web 应用程序可能使用该标记来收集有关用户代理的详细信息。</span><span class="sxs-lookup"><span data-stu-id="d61d4-136">The web application will use the token to verify that the user agent has been successfully authenticated by the external authentication service, and the web application may use the token to gather more information about the user agent.</span></span> <span data-ttu-id="d61d4-137">应用程序完成处理用户代理的信息，该 web 应用程序将返回为用户代理基于其授权设置适当的响应。</span><span class="sxs-lookup"><span data-stu-id="d61d4-137">Once the application is done processing the user agent's information, the web application will return the appropriate response to the user agent based on its authorization settings.</span></span>

<span data-ttu-id="d61d4-138">在此第二个示例中，用户代理与 web 应用程序和外部授权服务器协商和 web 应用程序执行与要检索有关用户的其他信息的外部授权服务器的其他通信代理：</span><span class="sxs-lookup"><span data-stu-id="d61d4-138">In this second example, the user agent negotiates with the web application and external authorization server, and the web application performs additional communication with the external authorization server to retrieve additional information about the user agent:</span></span>

<span data-ttu-id="d61d4-139">[![](external-authentication-services/_static/image4.png "单击以展开映像")](external-authentication-services/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-139">[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)</span></span>

<span data-ttu-id="d61d4-140">Visual Studio 2013 和 ASP.NET 4.5.1 与外部身份验证服务的集成更轻松地进行开发人员通过提供以下身份验证服务的内置集成：</span><span class="sxs-lookup"><span data-stu-id="d61d4-140">Visual Studio 2013 and ASP.NET 4.5.1 make integration with external authentication services easier for developers by providing built-in integration for the following authentication services:</span></span>

- <span data-ttu-id="d61d4-141">Facebook</span><span class="sxs-lookup"><span data-stu-id="d61d4-141">Facebook</span></span>
- <span data-ttu-id="d61d4-142">google</span><span class="sxs-lookup"><span data-stu-id="d61d4-142">Google</span></span>
- <span data-ttu-id="d61d4-143">Microsoft 帐户 （Windows Live ID 帐户）</span><span class="sxs-lookup"><span data-stu-id="d61d4-143">Microsoft Accounts (Windows Live ID accounts)</span></span>
- <span data-ttu-id="d61d4-144">twitter</span><span class="sxs-lookup"><span data-stu-id="d61d4-144">Twitter</span></span>

<span data-ttu-id="d61d4-145">在本演练中的示例将演示如何通过使用 Visual Studio 2013 附带的新 ASP.NET Web 应用程序模板来配置每个支持的外部身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="d61d4-145">The examples in this walkthrough will demonstrate how to configure each of the supported external authentication services by using the new ASP.NET Web Application template that ships with Visual Studio 2013.</span></span>

> [!NOTE]
> <span data-ttu-id="d61d4-146">如有必要，你可能需要将你的 FQDN 添加到外部身份验证服务的设置。</span><span class="sxs-lookup"><span data-stu-id="d61d4-146">If necessary, you may need to add your FQDN to the settings for your external authentication service.</span></span> <span data-ttu-id="d61d4-147">此要求基于安全约束，对于某些外部身份验证服务，这需要在应用程序设置要与你的客户端使用的 FQDN 匹配的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="d61d4-147">This requirement is based on security constraints for some external authentication services which require the FQDN in your application settings to match the FQDN that is used by your clients.</span></span> <span data-ttu-id="d61d4-148">（此步骤将会有很大为每个外部身份验证服务; 你将需要参考的文档以查看这是否需要每个外部身份验证服务以及如何配置这些设置。）如果你需要配置 IIS Express 以用于测试此环境中使用 FQDN，请参阅[配置 IIS Express，以使用完全限定的域名](#FQDN)在本演练后面的部分。</span><span class="sxs-lookup"><span data-stu-id="d61d4-148">(The steps for this will vary greatly for each external authentication service; you will need to consult the documentation for each external authentication service to see if this is required and how to configure these settings.) If you need to configure IIS Express to use an FQDN for testing this environment, see the [Configuring IIS Express to use a Fully Qualified Domain Name](#FQDN) section later in this walkthrough.</span></span>


<a id="SAMPLE"></a>
## <a name="creating-a-sample-web-application"></a><span data-ttu-id="d61d4-149">创建示例 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="d61d4-149">Creating a Sample Web Application</span></span>

<span data-ttu-id="d61d4-150">以下步骤将引导你完成创建示例应用程序使用 ASP.NET Web 应用程序模板，并将为每个外部身份验证服务稍后在本演练中使用此示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="d61d4-150">The following steps will lead you through creating a sample application by using the ASP.NET Web Application template, and you will use this sample application for each of the external authentication services later in this walkthrough.</span></span>

<span data-ttu-id="d61d4-151">启动 Visual Studio 2013 选择**新项目**从开始页。</span><span class="sxs-lookup"><span data-stu-id="d61d4-151">Start Visual Studio 2013 select **New Project** from the Start page.</span></span> <span data-ttu-id="d61d4-152">或从**文件**菜单上，选择**新建**然后**项目**。</span><span class="sxs-lookup"><span data-stu-id="d61d4-152">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="d61d4-153">[![](external-authentication-services/_static/image6.png "单击以展开映像")](external-authentication-services/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-153">[![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png)</span></span>

<span data-ttu-id="d61d4-154">当**新项目**显示对话框中，选择**已安装****模板**展开**Visual C#**。</span><span class="sxs-lookup"><span data-stu-id="d61d4-154">When the **New Project** dialog box is displayed, select **Installed** **Templates** and expand **Visual C#**.</span></span> <span data-ttu-id="d61d4-155">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="d61d4-155">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="d61d4-156">在项目模板列表中，选择**ASP.NET Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="d61d4-156">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="d61d4-157">输入你的项目的名称，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="d61d4-157">Enter a name for your project and click **OK**.</span></span>

<span data-ttu-id="d61d4-158">[![](external-authentication-services/_static/image8.png "单击以展开映像")](external-authentication-services/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-158">[![](external-authentication-services/_static/image8.png "Click to Expand the Image")](external-authentication-services/_static/image7.png)</span></span>

<span data-ttu-id="d61d4-159">当**新建 ASP.NET 项目**将显示选择**SPA**模板，然后单击**创建项目**。</span><span class="sxs-lookup"><span data-stu-id="d61d4-159">When the **New ASP.NET Project** is displayed, select the **SPA** template and click **Create Project**.</span></span>

<span data-ttu-id="d61d4-160">[![](external-authentication-services/_static/image10.png "单击以展开映像")](external-authentication-services/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-160">[![](external-authentication-services/_static/image10.png "Click to Expand the Image")](external-authentication-services/_static/image9.png)</span></span>

<span data-ttu-id="d61d4-161">与 Visual Studio 2013 的等待创建你的项目。</span><span class="sxs-lookup"><span data-stu-id="d61d4-161">Wait as Visual Studio 2013 creates your project.</span></span>

<span data-ttu-id="d61d4-162">[![](external-authentication-services/_static/image12.png "单击以展开映像")](external-authentication-services/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-162">[![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png)</span></span>

<span data-ttu-id="d61d4-163">完成后创建您的项目的 Visual Studio 2013，打开*Startup.Auth.cs*文件将位于**应用\_启动**文件夹。</span><span class="sxs-lookup"><span data-stu-id="d61d4-163">When Visual Studio 2013 has finished creating your project, open the *Startup.Auth.cs* file that is located in the **App\_Start** folder.</span></span>

<span data-ttu-id="d61d4-164">[![](external-authentication-services/_static/image14.png "单击以展开映像")](external-authentication-services/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-164">[![](external-authentication-services/_static/image14.png "Click to Expand the Image")](external-authentication-services/_static/image13.png)</span></span>

<span data-ttu-id="d61d4-165">首次创建项目时，没有任何外部身份验证服务中启用*Startup.Auth.cs*文件; 以下展示你的代码可能与的类似，针对在哪里突出显示部分中，您将启用外部身份验证服务和任何相关的设置，才能使用 ASP.NET 应用程序的 Microsoft 帐户、 Twitter、 Facebook 或 Google 身份验证：</span><span class="sxs-lookup"><span data-stu-id="d61d4-165">When you first create the project, none of the external authentication services are enabled in *Startup.Auth.cs* file; the following illustrates what your code might resemble, with the sections highlighted for where you would enable an external authentication service and any relevant settings in order to use Microsoft Accounts, Twitter, Facebook, or Google authentication with your ASP.NET application:</span></span>

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

<span data-ttu-id="d61d4-166">按 F5 生成和调试 web 应用程序时，它将显示登录屏幕，你将看到已定义没有外部身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="d61d4-166">When you press F5 to build and debug your web application, it will display a login screen where you will see that no external authentication services have been defined.</span></span>

<span data-ttu-id="d61d4-167">[![](external-authentication-services/_static/image16.png "单击以展开映像")](external-authentication-services/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-167">[![](external-authentication-services/_static/image16.png "Click to Expand the Image")](external-authentication-services/_static/image15.png)</span></span>

<span data-ttu-id="d61d4-168">在以下部分中，你将学习如何来启用每个使用 Visual Studio 2013 中的 ASP.NET 提供的外部身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="d61d4-168">In the following sections, you will learn how to enable each of the external authentication services that are provided with ASP.NET in Visual Studio 2013.</span></span>

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a><span data-ttu-id="d61d4-169">启用 Facebook 身份验证</span><span class="sxs-lookup"><span data-stu-id="d61d4-169">Enabling Facebook Authentication</span></span>

<span data-ttu-id="d61d4-170">使用 Facebook 身份验证要求你创建 Facebook 开发人员帐户，并且你的项目需要的应用程序 ID 和密钥从 Facebook 才能正常。</span><span class="sxs-lookup"><span data-stu-id="d61d4-170">Using Facebook authentication requires you to create a Facebook developer account, and your project will require an application ID and secret key from Facebook in order to function.</span></span> <span data-ttu-id="d61d4-171">有关创建 Facebook 开发人员帐户，并获取你的应用程序 ID 和机密密钥的信息，请参阅[ https://go.microsoft.com/fwlink/?LinkID=252166 ](https://go.microsoft.com/fwlink/?LinkID=252166)。</span><span class="sxs-lookup"><span data-stu-id="d61d4-171">For information about creating a Facebook developer account and obtaining your application ID and secret key, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="d61d4-172">你一次获取你的应用程序 ID 和机密密钥，使用以下步骤来启用 web 应用程序的 Facebook 身份验证：</span><span class="sxs-lookup"><span data-stu-id="d61d4-172">Once you have obtained your application ID and secret key, use the following steps to enable Facebook authentication for your web application:</span></span>

1. <span data-ttu-id="d61d4-173">在 Visual Studio 2013 中打开你的项目时，打开*Startup.Auth.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="d61d4-173">When your project is open in Visual Studio 2013, open the *Startup.Auth.cs* file:</span></span>

    <span data-ttu-id="d61d4-174">[![](external-authentication-services/_static/image18.png "单击以展开映像")](external-authentication-services/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-174">[![](external-authentication-services/_static/image18.png "Click to Expand the Image")](external-authentication-services/_static/image17.png)</span></span>
2. <span data-ttu-id="d61d4-175">查找代码的突出显示的部分：</span><span class="sxs-lookup"><span data-stu-id="d61d4-175">Locate the highlighted section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. <span data-ttu-id="d61d4-176">删除&quot; // &quot;字符，取消注释的代码中，突出显示的行，然后添加你的应用程序 ID 和机密密钥。</span><span class="sxs-lookup"><span data-stu-id="d61d4-176">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="d61d4-177">一旦你已添加这些参数，则可以重新编译你的项目：</span><span class="sxs-lookup"><span data-stu-id="d61d4-177">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. <span data-ttu-id="d61d4-178">按 F5 以在 web 浏览器中打开 web 应用程序时，你将看到 Facebook 已被定义为外部身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="d61d4-178">When you press F5 to open your web application in your web browser, you will see that Facebook has been defined as an external authentication service:</span></span>

    <span data-ttu-id="d61d4-179">[![](external-authentication-services/_static/image20.png "单击以展开映像")](external-authentication-services/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-179">[![](external-authentication-services/_static/image20.png "Click to Expand the Image")](external-authentication-services/_static/image19.png)</span></span>
5. <span data-ttu-id="d61d4-180">当你单击**Facebook**按钮，你的浏览器将重定向到 Facebook 登录页：</span><span class="sxs-lookup"><span data-stu-id="d61d4-180">When you click the **Facebook** button, your browser will be redirected to the Facebook login page:</span></span>

    <span data-ttu-id="d61d4-181">[![](external-authentication-services/_static/image22.png "单击以展开映像")](external-authentication-services/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-181">[![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)</span></span>
6. <span data-ttu-id="d61d4-182">输入你的 Facebook 凭据并单击后**登录**，web 浏览器将重定向回 web 应用程序，这会提示你输入**用户名**你想要将与相关联你Facebook 帐户：</span><span class="sxs-lookup"><span data-stu-id="d61d4-182">After you enter your Facebook credentials and click **Log in**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Facebook account:</span></span>

    <span data-ttu-id="d61d4-183">[![](external-authentication-services/_static/image24.png "单击以展开映像")](external-authentication-services/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-183">[![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)</span></span>
7. <span data-ttu-id="d61d4-184">在输入你的用户名并单击后**注册**按钮，你的 web 应用程序将显示默认值**主页**为你的 Facebook 帐户：</span><span class="sxs-lookup"><span data-stu-id="d61d4-184">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Facebook account:</span></span>

    <span data-ttu-id="d61d4-185">[![](external-authentication-services/_static/image26.png "单击以展开映像")](external-authentication-services/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-185">[![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)</span></span>

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a><span data-ttu-id="d61d4-186">启用 Google 身份验证</span><span class="sxs-lookup"><span data-stu-id="d61d4-186">Enabling Google Authentication</span></span>

<span data-ttu-id="d61d4-187">Google 是迄今最简单的方法的外部身份验证服务中启用，因为它不需要开发人员帐户，也不要求应用程序 ID 或密钥等其他外部身份验证服务的其他信息需要。</span><span class="sxs-lookup"><span data-stu-id="d61d4-187">Google is by far the easiest of the external authentication services to enable because it doesn't require a developer account, nor does it require additional information like your application ID or secret key as the other external authentication services necessitate.</span></span>

<span data-ttu-id="d61d4-188">若要启用 web 应用程序的 Google 身份验证，请使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="d61d4-188">To enable Google authentication for your web application, use the following steps:</span></span>

1. <span data-ttu-id="d61d4-189">在 Visual Studio 2013 中打开你的项目时，打开*Startup.Auth.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="d61d4-189">When your project is open in Visual Studio 2013, open the *Startup.Auth.cs* file:</span></span>

    <span data-ttu-id="d61d4-190">[![](external-authentication-services/_static/image28.png "单击以展开映像")](external-authentication-services/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-190">[![](external-authentication-services/_static/image28.png "Click to Expand the Image")](external-authentication-services/_static/image27.png)</span></span>
2. <span data-ttu-id="d61d4-191">查找代码的突出显示的部分：</span><span class="sxs-lookup"><span data-stu-id="d61d4-191">Locate the highlighted section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. <span data-ttu-id="d61d4-192">删除&quot; // &quot;字符来取消注释的代码中，突出显示的行，然后重新编译你的项目：</span><span class="sxs-lookup"><span data-stu-id="d61d4-192">Remove the &quot;//&quot; characters to uncomment the highlighted line of code, and then recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. <span data-ttu-id="d61d4-193">按 F5 以在 web 浏览器中打开 web 应用程序时，你将看到 Google 已被定义为外部身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="d61d4-193">When you press F5 to open your web application in your web browser, you will see that Google has been defined as an external authentication service:</span></span>

    <span data-ttu-id="d61d4-194">[![](external-authentication-services/_static/image30.png "单击以展开映像")](external-authentication-services/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-194">[![](external-authentication-services/_static/image30.png "Click to Expand the Image")](external-authentication-services/_static/image29.png)</span></span>
5. <span data-ttu-id="d61d4-195">当你单击**Google**按钮，你的浏览器将重定向到 Google 登录页：</span><span class="sxs-lookup"><span data-stu-id="d61d4-195">When you click the **Google** button, your browser will be redirected to the Google login page:</span></span>

    <span data-ttu-id="d61d4-196">[![](external-authentication-services/_static/image32.png "单击以展开映像")](external-authentication-services/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-196">[![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)</span></span>
6. <span data-ttu-id="d61d4-197">输入你的 Google 凭据并单击后**登录**，Google 将提示你验证你的 web 应用程序有权访问你的 Google 帐户：</span><span class="sxs-lookup"><span data-stu-id="d61d4-197">After you enter your Google credentials and click **Sign in**, Google will prompt you to verify that your web application has permissions to access your Google account:</span></span>

    <span data-ttu-id="d61d4-198">[![](external-authentication-services/_static/image34.png "单击以展开映像")](external-authentication-services/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-198">[![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)</span></span>
7. <span data-ttu-id="d61d4-199">当你单击**接受**，web 浏览器将重定向回 web 应用程序，这会提示你输入**用户名**你想要将与你的 Google 帐户相关联：</span><span class="sxs-lookup"><span data-stu-id="d61d4-199">When you click **Accept**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Google account:</span></span>

    <span data-ttu-id="d61d4-200">[![](external-authentication-services/_static/image36.png "单击以展开映像")](external-authentication-services/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-200">[![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)</span></span>
8. <span data-ttu-id="d61d4-201">在输入你的用户名并单击后**注册**按钮，你的 web 应用程序将显示默认值**主页**为你的 Google 帐户：</span><span class="sxs-lookup"><span data-stu-id="d61d4-201">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Google account:</span></span>

    <span data-ttu-id="d61d4-202">[![](external-authentication-services/_static/image38.png "单击以展开映像")](external-authentication-services/_static/image37.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-202">[![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)</span></span>

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a><span data-ttu-id="d61d4-203">启用 Microsoft 身份验证</span><span class="sxs-lookup"><span data-stu-id="d61d4-203">Enabling Microsoft Authentication</span></span>

<span data-ttu-id="d61d4-204">Microsoft 身份验证要求你创建开发人员帐户，并且它才能正常需要客户端 ID 和客户端密钥。</span><span class="sxs-lookup"><span data-stu-id="d61d4-204">Microsoft authentication requires you to create a developer account, and it requires a client ID and client secret in order to function.</span></span> <span data-ttu-id="d61d4-205">有关创建 Microsoft 开发人员帐户，并获取你的客户端 ID 和客户端密钥的信息，请参阅[ https://go.microsoft.com/fwlink/?LinkID=144070 ](https://go.microsoft.com/fwlink/?LinkID=144070)。</span><span class="sxs-lookup"><span data-stu-id="d61d4-205">For information about creating a Microsoft developer account and obtaining your client ID and client secret, see [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span></span>

<span data-ttu-id="d61d4-206">你一次获取你的使用者密钥和使用者机密，使用以下步骤来启用 web 应用程序的 Microsoft 身份验证：</span><span class="sxs-lookup"><span data-stu-id="d61d4-206">Once you have obtained your consumer key and consumer secret, use the following steps to enable Microsoft authentication for your web application:</span></span>

1. <span data-ttu-id="d61d4-207">在 Visual Studio 2013 中打开你的项目时，打开*Startup.Auth.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="d61d4-207">When your project is open in Visual Studio 2013, open the *Startup.Auth.cs* file:</span></span>

    <span data-ttu-id="d61d4-208">[![](external-authentication-services/_static/image40.png "单击以展开映像")](external-authentication-services/_static/image39.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-208">[![](external-authentication-services/_static/image40.png "Click to Expand the Image")](external-authentication-services/_static/image39.png)</span></span>
2. <span data-ttu-id="d61d4-209">查找代码的突出显示的部分：</span><span class="sxs-lookup"><span data-stu-id="d61d4-209">Locate the highlighted section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. <span data-ttu-id="d61d4-210">删除&quot; // &quot;字符，取消注释的代码中，突出显示的行，然后添加你的客户端 ID 和客户端密钥。</span><span class="sxs-lookup"><span data-stu-id="d61d4-210">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your client ID and client secret.</span></span> <span data-ttu-id="d61d4-211">一旦你已添加这些参数，则可以重新编译你的项目：</span><span class="sxs-lookup"><span data-stu-id="d61d4-211">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. <span data-ttu-id="d61d4-212">按 F5 以在 web 浏览器中打开 web 应用程序时，你将看到 Microsoft 已被定义为外部身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="d61d4-212">When you press F5 to open your web application in your web browser, you will see that Microsoft has been defined as an external authentication service:</span></span>

    <span data-ttu-id="d61d4-213">[![](external-authentication-services/_static/image42.png "单击以展开映像")](external-authentication-services/_static/image41.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-213">[![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)</span></span>
5. <span data-ttu-id="d61d4-214">当你单击**Microsoft**按钮，你的浏览器将重定向到 Microsoft 登录页：</span><span class="sxs-lookup"><span data-stu-id="d61d4-214">When you click the **Microsoft** button, your browser will be redirected to the Microsoft login page:</span></span>

    <span data-ttu-id="d61d4-215">[![](external-authentication-services/_static/image44.png "单击以展开映像")](external-authentication-services/_static/image43.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-215">[![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)</span></span>
6. <span data-ttu-id="d61d4-216">输入你的 Microsoft 凭据并单击后**登录**，系统将提示你验证你的 web 应用程序有权访问你的 Microsoft 帐户：</span><span class="sxs-lookup"><span data-stu-id="d61d4-216">After you enter your Microsoft credentials and click **Sign in**, you will be prompted to verify that your web application has permissions to access your Microsoft account:</span></span>

    <span data-ttu-id="d61d4-217">[![](external-authentication-services/_static/image46.png "单击以展开映像")](external-authentication-services/_static/image45.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-217">[![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)</span></span>
7. <span data-ttu-id="d61d4-218">当你单击**是**，web 浏览器将重定向回 web 应用程序，这会提示你输入**用户名**你想要将与你的 Microsoft 帐户相关联：</span><span class="sxs-lookup"><span data-stu-id="d61d4-218">When you click **Yes**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Microsoft account:</span></span>

    <span data-ttu-id="d61d4-219">[![](external-authentication-services/_static/image48.png "单击以展开映像")](external-authentication-services/_static/image47.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-219">[![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)</span></span>
8. <span data-ttu-id="d61d4-220">在输入你的用户名并单击后**注册**按钮，你的 web 应用程序将显示默认值**主页**你的 Microsoft 帐户：</span><span class="sxs-lookup"><span data-stu-id="d61d4-220">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Microsoft account:</span></span>

    <span data-ttu-id="d61d4-221">[![](external-authentication-services/_static/image50.png "单击以展开映像")](external-authentication-services/_static/image49.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-221">[![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)</span></span>

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a><span data-ttu-id="d61d4-222">启用 Twitter 身份验证</span><span class="sxs-lookup"><span data-stu-id="d61d4-222">Enabling Twitter Authentication</span></span>

<span data-ttu-id="d61d4-223">Twitter 身份验证要求你创建开发人员帐户，并且它才能正常需要使用者密钥和使用者机密。</span><span class="sxs-lookup"><span data-stu-id="d61d4-223">Twitter authentication requires you to create a developer account, and it requires a consumer key and consumer secret in order to function.</span></span> <span data-ttu-id="d61d4-224">有关创建 Twitter 开发人员帐户和获取使用者密钥和使用者机密的信息，请参阅[ https://go.microsoft.com/fwlink/?LinkID=252166 ](https://go.microsoft.com/fwlink/?LinkID=252166)。</span><span class="sxs-lookup"><span data-stu-id="d61d4-224">For information about creating a Twitter developer account and obtaining your consumer key and consumer secret, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="d61d4-225">你一次获取你的使用者密钥和使用者机密，请使用以下步骤启用 web 应用程序的 Twitter 身份验证：</span><span class="sxs-lookup"><span data-stu-id="d61d4-225">Once you have obtained your consumer key and consumer secret, use the following steps to enable Twitter authentication for your web application:</span></span>

1. <span data-ttu-id="d61d4-226">在 Visual Studio 2013 中打开你的项目时，打开*Startup.Auth.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="d61d4-226">When your project is open in Visual Studio 2013, open the *Startup.Auth.cs* file:</span></span>

    <span data-ttu-id="d61d4-227">[![](external-authentication-services/_static/image52.png "单击以展开映像")](external-authentication-services/_static/image51.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-227">[![](external-authentication-services/_static/image52.png "Click to Expand the Image")](external-authentication-services/_static/image51.png)</span></span>
2. <span data-ttu-id="d61d4-228">查找代码的突出显示的部分：</span><span class="sxs-lookup"><span data-stu-id="d61d4-228">Locate the highlighted section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. <span data-ttu-id="d61d4-229">删除&quot; // &quot;字符，取消注释的代码中，突出显示的行，然后添加你的使用者密钥和使用者机密。</span><span class="sxs-lookup"><span data-stu-id="d61d4-229">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your consumer key and consumer secret.</span></span> <span data-ttu-id="d61d4-230">一旦你已添加这些参数，则可以重新编译你的项目：</span><span class="sxs-lookup"><span data-stu-id="d61d4-230">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. <span data-ttu-id="d61d4-231">按 F5 以在 web 浏览器中打开 web 应用程序时，你将看到 Twitter 已被定义为外部身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="d61d4-231">When you press F5 to open your web application in your web browser, you will see that Twitter has been defined as an external authentication service:</span></span>

    <span data-ttu-id="d61d4-232">[![](external-authentication-services/_static/image54.png "单击以展开映像")](external-authentication-services/_static/image53.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-232">[![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)</span></span>
5. <span data-ttu-id="d61d4-233">当你单击**Twitter**按钮，你的浏览器将重定向到 Twitter 登录页：</span><span class="sxs-lookup"><span data-stu-id="d61d4-233">When you click the **Twitter** button, your browser will be redirected to the Twitter login page:</span></span>

    <span data-ttu-id="d61d4-234">[![](external-authentication-services/_static/image56.png "单击以展开映像")](external-authentication-services/_static/image55.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-234">[![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)</span></span>
6. <span data-ttu-id="d61d4-235">输入你的 Twitter 凭据并单击后**Authorize 应用**，web 浏览器将重定向回 web 应用程序，这会提示你输入**用户名**你想要将与相关联你的 Twitter 帐户：</span><span class="sxs-lookup"><span data-stu-id="d61d4-235">After you enter your Twitter credentials and click **Authorize app**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Twitter account:</span></span>

    <span data-ttu-id="d61d4-236">[![](external-authentication-services/_static/image58.png "单击以展开映像")](external-authentication-services/_static/image57.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-236">[![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)</span></span>
7. <span data-ttu-id="d61d4-237">在输入你的用户名并单击后**注册**按钮，你的 web 应用程序将显示默认值**主页**为你的 Twitter 帐户：</span><span class="sxs-lookup"><span data-stu-id="d61d4-237">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Twitter account:</span></span>

    <span data-ttu-id="d61d4-238">[![](external-authentication-services/_static/image60.png "单击以展开映像")](external-authentication-services/_static/image59.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-238">[![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)</span></span>

<a id="MOREINFO"></a>
## <a name="additional-information"></a><span data-ttu-id="d61d4-239">其他信息</span><span class="sxs-lookup"><span data-stu-id="d61d4-239">Additional Information</span></span>

<span data-ttu-id="d61d4-240">有关创建使用 OAuth 和 OpenID 应用程序的其他信息，请参阅以下 Url:</span><span class="sxs-lookup"><span data-stu-id="d61d4-240">For additional information about creating applications that use OAuth and OpenID, see the following URLs:</span></span>

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a><span data-ttu-id="d61d4-241">组合外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="d61d4-241">Combining External Authentication Services</span></span>

<span data-ttu-id="d61d4-242">用于提高灵活性，你可以在同一时间定义多个外部身份验证服务-这允许你的 web 应用程序的用户使用从任何启用的外部身份验证服务的帐户：</span><span class="sxs-lookup"><span data-stu-id="d61d4-242">For greater flexibility, you can define multiple external authentication services at the same time - this allows your web application's users to use an account from any of the enabled external authentication services:</span></span>

<span data-ttu-id="d61d4-243">[![](external-authentication-services/_static/image62.png "单击以展开映像")](external-authentication-services/_static/image61.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-243">[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)</span></span>

<a id="FQDN"></a>
### <a name="configuring-iis-express-to-use-a-fully-qualified-domain-name"></a><span data-ttu-id="d61d4-244">配置 IIS Express 以使用完全限定的域名</span><span class="sxs-lookup"><span data-stu-id="d61d4-244">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>

<span data-ttu-id="d61d4-245">某些外部身份验证提供程序不支持使用这样的 HTTP 地址来测试你的应用程序`http://localhost:port/`。</span><span class="sxs-lookup"><span data-stu-id="d61d4-245">Some external authentication providers do not support testing your application by using an HTTP address like `http://localhost:port/`.</span></span> <span data-ttu-id="d61d4-246">若要解决此问题，可以将完全限定的域名名称 (FQDN) 的静态映射添加到你的主机文件，并在 Visual Studio 2013 中以进行测试/调试使用 FQDN 配置项目的选项。</span><span class="sxs-lookup"><span data-stu-id="d61d4-246">To work around this issue, you can add a static Fully Qualified Domain Name (FQDN) mapping to your HOSTS file and configure your project options in Visual Studio 2013 to use the FQDN for testing/debugging.</span></span> <span data-ttu-id="d61d4-247">为此，请使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="d61d4-247">To do so, use the following steps:</span></span>

- <span data-ttu-id="d61d4-248">添加静态 FQDN 映射你的主机文件：</span><span class="sxs-lookup"><span data-stu-id="d61d4-248">Add a static FQDN mapping your HOSTS file:</span></span>

  1. <span data-ttu-id="d61d4-249">打开提升的命令提示符窗口中。</span><span class="sxs-lookup"><span data-stu-id="d61d4-249">Open an elevated command prompt in Windows.</span></span>
  2. <span data-ttu-id="d61d4-250">键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="d61d4-250">Type the following command:</span></span>

      <span data-ttu-id="d61d4-251"><kbd>notepad %WinDir%\system32\drivers\etc\hosts</kbd></span><span class="sxs-lookup"><span data-stu-id="d61d4-251"><kbd>notepad %WinDir%\system32\drivers\etc\hosts</kbd></span></span>
  3. <span data-ttu-id="d61d4-252">类似于以下条目添加到主机文件中：</span><span class="sxs-lookup"><span data-stu-id="d61d4-252">Add an entry like the following to the HOSTS file:</span></span>

      <span data-ttu-id="d61d4-253"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span><span class="sxs-lookup"><span data-stu-id="d61d4-253"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span></span>
  4. <span data-ttu-id="d61d4-254">保存并关闭你的主机文件。</span><span class="sxs-lookup"><span data-stu-id="d61d4-254">Save and close your HOSTS file.</span></span>

- <span data-ttu-id="d61d4-255">配置 Visual Studio 项目以使用 FQDN:</span><span class="sxs-lookup"><span data-stu-id="d61d4-255">Configure your Visual Studio project to use the FQDN:</span></span>

  1. <span data-ttu-id="d61d4-256">在 Visual Studio 2013 中打开你的项目时，单击**项目**菜单，然后选择你的项目的属性。</span><span class="sxs-lookup"><span data-stu-id="d61d4-256">When your project is open in Visual Studio 2013, click the **Project** menu, and then select your project's properties.</span></span> <span data-ttu-id="d61d4-257">例如，你可以选择**WebApplication1 属性**。</span><span class="sxs-lookup"><span data-stu-id="d61d4-257">For example, you might select **WebApplication1 Properties**.</span></span>
  2. <span data-ttu-id="d61d4-258">选择**Web**选项卡。</span><span class="sxs-lookup"><span data-stu-id="d61d4-258">Select the **Web** tab.</span></span>
  3. <span data-ttu-id="d61d4-259">输入你的 FQDN 为<strong>项目 Url</strong>。</span><span class="sxs-lookup"><span data-stu-id="d61d4-259">Enter your FQDN for the <strong>Project Url</strong>.</span></span> <span data-ttu-id="d61d4-260">例如，将输入<kbd> <http://www.wingtiptoys.com> </kbd> ，如果已添加到你的主机文件的 FQDN 映射。</span><span class="sxs-lookup"><span data-stu-id="d61d4-260">For example, you would enter <kbd><http://www.wingtiptoys.com></kbd> if that was the FQDN mapping that you added to your HOSTS file.</span></span>

- <span data-ttu-id="d61d4-261">配置 IIS Express 以使用你的应用程序的 FQDN:</span><span class="sxs-lookup"><span data-stu-id="d61d4-261">Configure IIS Express to use the FQDN for your application:</span></span>

    1. <span data-ttu-id="d61d4-262">打开提升的命令提示符窗口中。</span><span class="sxs-lookup"><span data-stu-id="d61d4-262">Open an elevated command prompt in Windows.</span></span>
    2. <span data-ttu-id="d61d4-263">键入以下命令以更改为 IIS Express 文件夹：</span><span class="sxs-lookup"><span data-stu-id="d61d4-263">Type the following command to change to your IIS Express folder:</span></span>

        <span data-ttu-id="d61d4-264"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span><span class="sxs-lookup"><span data-stu-id="d61d4-264"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span></span>
    3. <span data-ttu-id="d61d4-265">键入以下命令以将 FQDN 添加到你的应用程序：</span><span class="sxs-lookup"><span data-stu-id="d61d4-265">Type the following command to add the FQDN to your application:</span></span>

        <span data-ttu-id="d61d4-266"><kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='\*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span><span class="sxs-lookup"><span data-stu-id="d61d4-266"><kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='\*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span></span>

  <span data-ttu-id="d61d4-267">其中**WebApplication1**是你的项目的名称和**bindingInformation**包含你想要用于测试的端口号和 FQDN。</span><span class="sxs-lookup"><span data-stu-id="d61d4-267">Where **WebApplication1** is the name of your project and **bindingInformation** contains the port number and FQDN that you want to use for your testing.</span></span>

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a><span data-ttu-id="d61d4-268">如何获取 Microsoft 身份验证的应用程序设置</span><span class="sxs-lookup"><span data-stu-id="d61d4-268">How to Obtain your Application Settings for Microsoft Authentication</span></span>

<span data-ttu-id="d61d4-269">链接到 Windows Live 进行 Microsoft 身份验证的应用程序是一个简单的过程。</span><span class="sxs-lookup"><span data-stu-id="d61d4-269">Linking an application to Windows Live for Microsoft Authentication is a simple process.</span></span> <span data-ttu-id="d61d4-270">如果已未链接到 Windows Live 应用程序，你可以使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="d61d4-270">If you have not already linked an application to Windows Live, you can use the following steps:</span></span>

1. <span data-ttu-id="d61d4-271">浏览到[ https://go.microsoft.com/fwlink/?LinkID=144070 ](https://go.microsoft.com/fwlink/?LinkID=144070)并输入你的 Microsoft 帐户名和密码出现提示时，然后单击**登录**:</span><span class="sxs-lookup"><span data-stu-id="d61d4-271">Browse to [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) and enter your Microsoft account name and password when prompted, then click **Sign in**:</span></span>

    <span data-ttu-id="d61d4-272">[![](external-authentication-services/_static/image64.png "单击以展开映像")](external-authentication-services/_static/image63.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-272">[![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png)</span></span>
2. <span data-ttu-id="d61d4-273">输入的名称和出现提示时，应用程序的语言，然后单击**我接受**:</span><span class="sxs-lookup"><span data-stu-id="d61d4-273">Enter the name and language of your application when prompted, and then click **I accept**:</span></span>

    <span data-ttu-id="d61d4-274">[![](external-authentication-services/_static/image66.png "单击以展开映像")](external-authentication-services/_static/image65.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-274">[![](external-authentication-services/_static/image66.png "Click to Expand the Image")](external-authentication-services/_static/image65.png)</span></span>
3. <span data-ttu-id="d61d4-275">上**API 设置**你的应用程序页上，输入你的应用程序和复制的重定向域**客户端 ID**和**客户端机密**为你的项目，然后单击**保存**:</span><span class="sxs-lookup"><span data-stu-id="d61d4-275">On the **API Settings** page for your application, enter the redirect domain for your application and copy the **Client ID** and **Client secret** for your project, and then click **Save**:</span></span>

    <span data-ttu-id="d61d4-276">[![](external-authentication-services/_static/image68.png "单击以展开映像")](external-authentication-services/_static/image67.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-276">[![](external-authentication-services/_static/image68.png "Click to Expand the Image")](external-authentication-services/_static/image67.png)</span></span>

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a><span data-ttu-id="d61d4-277">可选： 禁用本地注册</span><span class="sxs-lookup"><span data-stu-id="d61d4-277">Optional: Disable Local Registration</span></span>

<span data-ttu-id="d61d4-278">当前的 ASP.NET 本地注册功能不会阻止自动的程序 （机器人） 创建帐户; 的成员例如，通过使用一种 bot 防护和验证的技术，如[CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)。</span><span class="sxs-lookup"><span data-stu-id="d61d4-278">The current ASP.NET local registration functionality does not prevent automated programs (bots) from creating member accounts; for example, by using a bot-prevention and validation technology like [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md).</span></span> <span data-ttu-id="d61d4-279">因此，应删除的登录页上的本地登录窗体和注册链接。</span><span class="sxs-lookup"><span data-stu-id="d61d4-279">Because of this, you should remove the local login form and registration link on the login page.</span></span> <span data-ttu-id="d61d4-280">为此，请打开 *\_Login.cshtml*在项目中，页，然后注释掉的行本地登录面板和注册链接。</span><span class="sxs-lookup"><span data-stu-id="d61d4-280">To do so, open the *\_Login.cshtml* page in your project, and then comment out the lines for the local login panel and the registration link.</span></span> <span data-ttu-id="d61d4-281">则结果页应如下所示下面的代码示例：</span><span class="sxs-lookup"><span data-stu-id="d61d4-281">The resulting page should look like the following code sample:</span></span>

[!code-html[Main](external-authentication-services/samples/sample10.html)]

<span data-ttu-id="d61d4-282">一旦已禁用本地登录面板和注册链接，登录页将仅显示已启用的外部身份验证提供程序：</span><span class="sxs-lookup"><span data-stu-id="d61d4-282">Once the local login panel and the registration link have been disabled, your login page will only display the external authentication providers that you have enabled:</span></span>

<span data-ttu-id="d61d4-283">[![](external-authentication-services/_static/image70.png "单击以展开映像")](external-authentication-services/_static/image69.png)</span><span class="sxs-lookup"><span data-stu-id="d61d4-283">[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)</span></span>
