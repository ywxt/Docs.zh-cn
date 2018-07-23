---
uid: web-api/overview/security/external-authentication-services
title: 使用 ASP.NET Web API 的外部身份验证服务 (C#) |Microsoft Docs
author: rmcmurray
description: 介绍如何在 ASP.NET Web API 中使用外部身份验证服务。
ms.author: aspnetcontent
ms.date: 06/26/2013
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: fe821384a195e69c102aad95e534d543de705a00
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37822779"
---
<a name="external-authentication-services-with-aspnet-web-api-c"></a><span data-ttu-id="71ac3-103">使用 ASP.NET Web API 的外部身份验证服务 (C#)</span><span class="sxs-lookup"><span data-stu-id="71ac3-103">External Authentication Services with ASP.NET Web API (C#)</span></span>
====================
<span data-ttu-id="71ac3-104">通过[Robert McMurray](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="71ac3-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="71ac3-105">Visual Studio 2013 和 ASP.NET 4.5.1 展开的安全选项[单页面应用程序](../../../single-page-application/index.md)(SPA) 和[Web API](../../index.md)服务与外部身份验证服务，包含多个集成OAuth/OpenID 和社交身份验证服务： Microsoft 帐户、 Twitter、 Facebook 和 Google。</span><span class="sxs-lookup"><span data-stu-id="71ac3-105">Visual Studio 2013 and ASP.NET 4.5.1 expand the security options for [Single Page Applications](../../../single-page-application/index.md) (SPA) and [Web API](../../index.md) services to integrate with external authentication services, which include several OAuth/OpenID and social media authentication services: Microsoft Accounts, Twitter, Facebook, and Google.</span></span>

### <a name="in-this-walkthrough"></a><span data-ttu-id="71ac3-106">在本演练中</span><span class="sxs-lookup"><span data-stu-id="71ac3-106">In This Walkthrough</span></span>

- [<span data-ttu-id="71ac3-107">使用外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="71ac3-107">Using External Authentication Services</span></span>](#USING)
- [<span data-ttu-id="71ac3-108">创建示例 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="71ac3-108">Creating the Sample Web Application</span></span>](#SAMPLE)
- [<span data-ttu-id="71ac3-109">启用 Facebook 身份验证</span><span class="sxs-lookup"><span data-stu-id="71ac3-109">Enabling Facebook Authentication</span></span>](#FACEBOOK)
- [<span data-ttu-id="71ac3-110">启用 Google 身份验证</span><span class="sxs-lookup"><span data-stu-id="71ac3-110">Enabling Google Authentication</span></span>](#GOOGLE)
- [<span data-ttu-id="71ac3-111">启用 Microsoft 身份验证</span><span class="sxs-lookup"><span data-stu-id="71ac3-111">Enabling Microsoft Authentication</span></span>](#MICROSOFT)
- [<span data-ttu-id="71ac3-112">启用 Twitter 身份验证</span><span class="sxs-lookup"><span data-stu-id="71ac3-112">Enabling Twitter Authentication</span></span>](#TWITTER)
- [<span data-ttu-id="71ac3-113">其他信息</span><span class="sxs-lookup"><span data-stu-id="71ac3-113">Additional Information</span></span>](#MOREINFO)

    - [<span data-ttu-id="71ac3-114">合并外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="71ac3-114">Combining External Authentication Services</span></span>](#COMBINE)
    - [<span data-ttu-id="71ac3-115">配置 IIS Express 以使用完全限定的域名</span><span class="sxs-lookup"><span data-stu-id="71ac3-115">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>](#FQDN)
    - [<span data-ttu-id="71ac3-116">如何获取 Microsoft 身份验证应用程序设置</span><span class="sxs-lookup"><span data-stu-id="71ac3-116">How to Obtain your Application Settings for Microsoft Authentication</span></span>](#OBTAIN)
    - [<span data-ttu-id="71ac3-117">可选： 禁用本地注册</span><span class="sxs-lookup"><span data-stu-id="71ac3-117">Optional: Disable Local Registration</span></span>](#DISABLE)

### <a name="prerequisites"></a><span data-ttu-id="71ac3-118">系统必备</span><span class="sxs-lookup"><span data-stu-id="71ac3-118">Prerequisites</span></span>

<span data-ttu-id="71ac3-119">若要按照本演练中的示例，需要具备以下：</span><span class="sxs-lookup"><span data-stu-id="71ac3-119">To follow the examples in this walkthrough, you need to have the following:</span></span>

- <span data-ttu-id="71ac3-120">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="71ac3-120">Visual Studio 2013</span></span>
- <span data-ttu-id="71ac3-121">至少一个以下外部身份验证服务帐户：</span><span class="sxs-lookup"><span data-stu-id="71ac3-121">An account for at least one of the following external authentication services:</span></span>

    - <span data-ttu-id="71ac3-122">Google 用户帐户</span><span class="sxs-lookup"><span data-stu-id="71ac3-122">A Google user account</span></span>
    - <span data-ttu-id="71ac3-123">具有应用程序标识符和一个以下社交媒体身份验证服务的机密密钥的开发人员帐户：</span><span class="sxs-lookup"><span data-stu-id="71ac3-123">A developer account with the application identifier and secret key for one of the following social media authentication services:</span></span>

        - <span data-ttu-id="71ac3-124">Microsoft 帐户 ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span><span class="sxs-lookup"><span data-stu-id="71ac3-124">Microsoft Accounts ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span></span>
        - <span data-ttu-id="71ac3-125">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span><span class="sxs-lookup"><span data-stu-id="71ac3-125">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span></span>
        - <span data-ttu-id="71ac3-126">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span><span class="sxs-lookup"><span data-stu-id="71ac3-126">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span></span>

<a id="USING"></a>
## <a name="using-external-authentication-services"></a><span data-ttu-id="71ac3-127">使用外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="71ac3-127">Using External Authentication Services</span></span>

<span data-ttu-id="71ac3-128">丰富的 web 开发人员帮助以减少开发到当前可用的外部身份验证服务时创建新的 web 应用程序的时间。</span><span class="sxs-lookup"><span data-stu-id="71ac3-128">The abundance of external authentication services that are currently available to web developers help to reduce development time when creating new web applications.</span></span> <span data-ttu-id="71ac3-129">Web 用户通常具有多个现有帐户用于流行的 web 服务和社交媒体网站，因此时身份验证的服务从外部 web 服务或社交媒体网站 web 应用程序实现，从而节省了开发时间，将已耗费创建身份验证实现。</span><span class="sxs-lookup"><span data-stu-id="71ac3-129">Web users typically have several existing accounts for popular web services and social media websites, therefore when a web application implements the authentication services from an external web service or social media website, it saves the development time that would have been spent creating an authentication implementation.</span></span> <span data-ttu-id="71ac3-130">使用外部身份验证服务将保存最终用户无需创建 web 应用程序，另一个帐户以及无需记住另一个用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="71ac3-130">Using an external authentication service saves end users from having to create another account for your web application, and also from having to remember another username and password.</span></span>

<span data-ttu-id="71ac3-131">在过去，开发人员已有两个选择： 创建自己的身份验证实现，或了解如何将外部身份验证服务集成到其应用程序。</span><span class="sxs-lookup"><span data-stu-id="71ac3-131">In the past, developers have had two choices: create their own authentication implementation, or learn how to integrate an external authentication service into their applications.</span></span> <span data-ttu-id="71ac3-132">在最基本的级别下, 图说明一个简单的请求流用户代理 （web 浏览器） 配置为使用外部身份验证服务的 web 应用程序请求的信息：</span><span class="sxs-lookup"><span data-stu-id="71ac3-132">At the most basic level, the following diagram illustrates a simple request flow for a user agent (web browser) that is requesting information from a web application that is configured to use an external authentication service:</span></span>

<span data-ttu-id="71ac3-133">[![](external-authentication-services/_static/image2.png "单击此项可展开图像")](external-authentication-services/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-133">[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)</span></span>

<span data-ttu-id="71ac3-134">在上图中，用户代理 （或在此示例中的 web 浏览器） 向发出请求的 web 应用程序，web 浏览器重定向到外部身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="71ac3-134">In the preceding diagram, the user agent (or web browser in this example) makes a request to a web application, which redirects the web browser to an external authentication service.</span></span> <span data-ttu-id="71ac3-135">用户代理将其凭据发送到外部身份验证服务和外部身份验证服务的用户代理已成功通过身份验证，如果将重用户代理定向到使用某种形式的原始 web 应用程序的令牌用户代理将发送到 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="71ac3-135">The user agent sends its credentials to the external authentication service, and if the user agent has successfully authenticated, the external authentication service will redirect the user agent to the original web application with some form of token which the user agent will send to the web application.</span></span> <span data-ttu-id="71ac3-136">Web 应用程序将使用该令牌来验证用户代理已成功验证外部身份验证服务和 web 应用程序可能会使用该标记来收集有关用户代理的详细信息。</span><span class="sxs-lookup"><span data-stu-id="71ac3-136">The web application will use the token to verify that the user agent has been successfully authenticated by the external authentication service, and the web application may use the token to gather more information about the user agent.</span></span> <span data-ttu-id="71ac3-137">完成应用程序处理用户代理的信息，web 应用程序将返回到用户代理基于其授权设置适当的响应。</span><span class="sxs-lookup"><span data-stu-id="71ac3-137">Once the application is done processing the user agent's information, the web application will return the appropriate response to the user agent based on its authorization settings.</span></span>

<span data-ttu-id="71ac3-138">在此第二个示例中，与 web 应用程序和外部授权服务器协商用户代理和 web 应用程序执行外部授权服务器来检索有关用户的其他信息与其他通信代理：</span><span class="sxs-lookup"><span data-stu-id="71ac3-138">In this second example, the user agent negotiates with the web application and external authorization server, and the web application performs additional communication with the external authorization server to retrieve additional information about the user agent:</span></span>

<span data-ttu-id="71ac3-139">[![](external-authentication-services/_static/image4.png "单击此项可展开图像")](external-authentication-services/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-139">[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)</span></span>

<span data-ttu-id="71ac3-140">Visual Studio 2013 和 ASP.NET 4.5.1 与外部身份验证服务的集成更轻松地进行开发人员通过提供以下身份验证服务的内置集成：</span><span class="sxs-lookup"><span data-stu-id="71ac3-140">Visual Studio 2013 and ASP.NET 4.5.1 make integration with external authentication services easier for developers by providing built-in integration for the following authentication services:</span></span>

- <span data-ttu-id="71ac3-141">Facebook</span><span class="sxs-lookup"><span data-stu-id="71ac3-141">Facebook</span></span>
- <span data-ttu-id="71ac3-142">Google</span><span class="sxs-lookup"><span data-stu-id="71ac3-142">Google</span></span>
- <span data-ttu-id="71ac3-143">Microsoft 帐户 （Windows Live ID 帐户）</span><span class="sxs-lookup"><span data-stu-id="71ac3-143">Microsoft Accounts (Windows Live ID accounts)</span></span>
- <span data-ttu-id="71ac3-144">Twitter</span><span class="sxs-lookup"><span data-stu-id="71ac3-144">Twitter</span></span>

<span data-ttu-id="71ac3-145">在本演练中的示例将演示如何使用 Visual Studio 2013 使用随附的新 ASP.NET Web 应用程序模板配置的每个受支持的外部身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="71ac3-145">The examples in this walkthrough will demonstrate how to configure each of the supported external authentication services by using the new ASP.NET Web Application template that ships with Visual Studio 2013.</span></span>

> [!NOTE]
> <span data-ttu-id="71ac3-146">如有必要，您可能需要将你的 FQDN 添加到外部身份验证服务的设置。</span><span class="sxs-lookup"><span data-stu-id="71ac3-146">If necessary, you may need to add your FQDN to the settings for your external authentication service.</span></span> <span data-ttu-id="71ac3-147">此要求基于安全约束，某些外部身份验证服务，这需要你的应用程序设置中的 FQDN，以匹配你的客户端使用的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="71ac3-147">This requirement is based on security constraints for some external authentication services which require the FQDN in your application settings to match the FQDN that is used by your clients.</span></span> <span data-ttu-id="71ac3-148">（此步骤将大不相同的每个外部身份验证服务; 你将需要参考的文档以查看这是否是必须每个外部身份验证服务以及如何配置这些设置。）如果你需要配置 IIS Express 以用于测试此环境中使用 FQDN，请参阅[配置 IIS Express 以使用完全限定的域名](#FQDN)本演练后面的部分。</span><span class="sxs-lookup"><span data-stu-id="71ac3-148">(The steps for this will vary greatly for each external authentication service; you will need to consult the documentation for each external authentication service to see if this is required and how to configure these settings.) If you need to configure IIS Express to use an FQDN for testing this environment, see the [Configuring IIS Express to use a Fully Qualified Domain Name](#FQDN) section later in this walkthrough.</span></span>


<a id="SAMPLE"></a>
## <a name="creating-a-sample-web-application"></a><span data-ttu-id="71ac3-149">创建示例 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="71ac3-149">Creating a Sample Web Application</span></span>

<span data-ttu-id="71ac3-150">以下步骤将引导用户创建的示例应用程序使用 ASP.NET Web 应用程序模板，并将为每个外部身份验证服务稍后在本演练使用此示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="71ac3-150">The following steps will lead you through creating a sample application by using the ASP.NET Web Application template, and you will use this sample application for each of the external authentication services later in this walkthrough.</span></span>

<span data-ttu-id="71ac3-151">启动 Visual Studio 2013 选择**新的项目**从起始页。</span><span class="sxs-lookup"><span data-stu-id="71ac3-151">Start Visual Studio 2013 select **New Project** from the Start page.</span></span> <span data-ttu-id="71ac3-152">或者，从**文件**菜单中，选择**新建**，然后**项目**。</span><span class="sxs-lookup"><span data-stu-id="71ac3-152">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="71ac3-153">[![](external-authentication-services/_static/image6.png "单击此项可展开图像")](external-authentication-services/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-153">[![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png)</span></span>

<span data-ttu-id="71ac3-154">当**新的项目**对话框中，选择**已安装****模板**展开**Visual C#**。</span><span class="sxs-lookup"><span data-stu-id="71ac3-154">When the **New Project** dialog box is displayed, select **Installed** **Templates** and expand **Visual C#**.</span></span> <span data-ttu-id="71ac3-155">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="71ac3-155">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="71ac3-156">在项目模板列表中选择**ASP.NET Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="71ac3-156">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="71ac3-157">输入你的项目的名称，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="71ac3-157">Enter a name for your project and click **OK**.</span></span>

<span data-ttu-id="71ac3-158">[![](external-authentication-services/_static/image8.png "单击此项可展开图像")](external-authentication-services/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-158">[![](external-authentication-services/_static/image8.png "Click to Expand the Image")](external-authentication-services/_static/image7.png)</span></span>

<span data-ttu-id="71ac3-159">当**新建 ASP.NET 项目**的显示，请选择**SPA**模板，然后单击**创建项目**。</span><span class="sxs-lookup"><span data-stu-id="71ac3-159">When the **New ASP.NET Project** is displayed, select the **SPA** template and click **Create Project**.</span></span>

<span data-ttu-id="71ac3-160">[![](external-authentication-services/_static/image10.png "单击此项可展开图像")](external-authentication-services/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-160">[![](external-authentication-services/_static/image10.png "Click to Expand the Image")](external-authentication-services/_static/image9.png)</span></span>

<span data-ttu-id="71ac3-161">等待与 Visual Studio 2013 创建你的项目。</span><span class="sxs-lookup"><span data-stu-id="71ac3-161">Wait as Visual Studio 2013 creates your project.</span></span>

<span data-ttu-id="71ac3-162">[![](external-authentication-services/_static/image12.png "单击此项可展开图像")](external-authentication-services/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-162">[![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png)</span></span>

<span data-ttu-id="71ac3-163">完成后创建你的项目的 Visual Studio 2013，打开*Startup.Auth.cs*文件，位于**应用\_启动**文件夹。</span><span class="sxs-lookup"><span data-stu-id="71ac3-163">When Visual Studio 2013 has finished creating your project, open the *Startup.Auth.cs* file that is located in the **App\_Start** folder.</span></span>

<span data-ttu-id="71ac3-164">[![](external-authentication-services/_static/image14.png "单击此项可展开图像")](external-authentication-services/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-164">[![](external-authentication-services/_static/image14.png "Click to Expand the Image")](external-authentication-services/_static/image13.png)</span></span>

<span data-ttu-id="71ac3-165">当你首次创建项目时，没有任何外部身份验证服务中启用*Startup.Auth.cs*文件; 下面将说明如何在代码可能类似于，有关在何处突出显示部分会启用此功能外部身份验证服务和任何相关设置才能在 ASP.NET 应用程序中使用 Microsoft 帐户、 Twitter、 Facebook 或 Google 身份验证：</span><span class="sxs-lookup"><span data-stu-id="71ac3-165">When you first create the project, none of the external authentication services are enabled in *Startup.Auth.cs* file; the following illustrates what your code might resemble, with the sections highlighted for where you would enable an external authentication service and any relevant settings in order to use Microsoft Accounts, Twitter, Facebook, or Google authentication with your ASP.NET application:</span></span>

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

<span data-ttu-id="71ac3-166">按 F5 以生成和调试 web 应用程序时，它将显示登录屏幕，你将看到尚未定义任何外部身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="71ac3-166">When you press F5 to build and debug your web application, it will display a login screen where you will see that no external authentication services have been defined.</span></span>

<span data-ttu-id="71ac3-167">[![](external-authentication-services/_static/image16.png "单击此项可展开图像")](external-authentication-services/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-167">[![](external-authentication-services/_static/image16.png "Click to Expand the Image")](external-authentication-services/_static/image15.png)</span></span>

<span data-ttu-id="71ac3-168">在以下部分中，将了解如何启用每个使用 Visual Studio 2013 中的 ASP.NET 提供的外部身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="71ac3-168">In the following sections, you will learn how to enable each of the external authentication services that are provided with ASP.NET in Visual Studio 2013.</span></span>

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a><span data-ttu-id="71ac3-169">启用 Facebook 身份验证</span><span class="sxs-lookup"><span data-stu-id="71ac3-169">Enabling Facebook Authentication</span></span>

<span data-ttu-id="71ac3-170">使用 Facebook 身份验证要求你创建 Facebook 开发人员帐户，并且你的项目将需要应用程序 ID 和机密密钥从 Facebook 的函数。</span><span class="sxs-lookup"><span data-stu-id="71ac3-170">Using Facebook authentication requires you to create a Facebook developer account, and your project will require an application ID and secret key from Facebook in order to function.</span></span> <span data-ttu-id="71ac3-171">有关创建 Facebook 开发人员帐户和获取应用程序 ID 和机密密钥的信息，请参阅[ https://go.microsoft.com/fwlink/?LinkID=252166 ](https://go.microsoft.com/fwlink/?LinkID=252166)。</span><span class="sxs-lookup"><span data-stu-id="71ac3-171">For information about creating a Facebook developer account and obtaining your application ID and secret key, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="71ac3-172">你一次获取你的应用程序 ID 和机密密钥，请使用以下步骤启用 web 应用程序的 Facebook 身份验证：</span><span class="sxs-lookup"><span data-stu-id="71ac3-172">Once you have obtained your application ID and secret key, use the following steps to enable Facebook authentication for your web application:</span></span>

1. <span data-ttu-id="71ac3-173">在 Visual Studio 2013 中打开你的项目时，打开*Startup.Auth.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="71ac3-173">When your project is open in Visual Studio 2013, open the *Startup.Auth.cs* file:</span></span>

    <span data-ttu-id="71ac3-174">[![](external-authentication-services/_static/image18.png "单击此项可展开图像")](external-authentication-services/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-174">[![](external-authentication-services/_static/image18.png "Click to Expand the Image")](external-authentication-services/_static/image17.png)</span></span>
2. <span data-ttu-id="71ac3-175">查找代码的突出显示的部分：</span><span class="sxs-lookup"><span data-stu-id="71ac3-175">Locate the highlighted section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. <span data-ttu-id="71ac3-176">删除&quot; // &quot;字符以取消注释的代码中，突出显示的行，然后添加你的应用程序 ID 和机密密钥。</span><span class="sxs-lookup"><span data-stu-id="71ac3-176">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="71ac3-177">添加这些参数后，可以重新编译你的项目：</span><span class="sxs-lookup"><span data-stu-id="71ac3-177">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. <span data-ttu-id="71ac3-178">按 F5 以在 web 浏览器中打开 web 应用程序时，你将看到 Facebook 已被定义为外部身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="71ac3-178">When you press F5 to open your web application in your web browser, you will see that Facebook has been defined as an external authentication service:</span></span>

    <span data-ttu-id="71ac3-179">[![](external-authentication-services/_static/image20.png "单击此项可展开图像")](external-authentication-services/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-179">[![](external-authentication-services/_static/image20.png "Click to Expand the Image")](external-authentication-services/_static/image19.png)</span></span>
5. <span data-ttu-id="71ac3-180">当您单击**Facebook**按钮，在浏览器将重定向到 Facebook 登录页：</span><span class="sxs-lookup"><span data-stu-id="71ac3-180">When you click the **Facebook** button, your browser will be redirected to the Facebook login page:</span></span>

    <span data-ttu-id="71ac3-181">[![](external-authentication-services/_static/image22.png "单击此项可展开图像")](external-authentication-services/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-181">[![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)</span></span>
6. <span data-ttu-id="71ac3-182">输入你的 Facebook 凭据并单击后**登录**，在 web 浏览器将重定向回到 web 应用程序，这会提示您输入**用户名**你想要将与相关联你Facebook 帐户：</span><span class="sxs-lookup"><span data-stu-id="71ac3-182">After you enter your Facebook credentials and click **Log in**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Facebook account:</span></span>

    <span data-ttu-id="71ac3-183">[![](external-authentication-services/_static/image24.png "单击此项可展开图像")](external-authentication-services/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-183">[![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)</span></span>
7. <span data-ttu-id="71ac3-184">在输入您的用户名称并单击后**注册**按钮，web 应用程序将显示默认**主页**为你的 Facebook 帐户：</span><span class="sxs-lookup"><span data-stu-id="71ac3-184">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Facebook account:</span></span>

    <span data-ttu-id="71ac3-185">[![](external-authentication-services/_static/image26.png "单击此项可展开图像")](external-authentication-services/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-185">[![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)</span></span>

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a><span data-ttu-id="71ac3-186">启用 Google 身份验证</span><span class="sxs-lookup"><span data-stu-id="71ac3-186">Enabling Google Authentication</span></span>

<span data-ttu-id="71ac3-187">Google 是到目前为止最简单的方法的外部身份验证服务来启用，因为它不需要开发人员帐户，也不要求应用程序 ID 或密钥等与其他外部身份验证服务的其他信息导致用。</span><span class="sxs-lookup"><span data-stu-id="71ac3-187">Google is by far the easiest of the external authentication services to enable because it doesn't require a developer account, nor does it require additional information like your application ID or secret key as the other external authentication services necessitate.</span></span>

<span data-ttu-id="71ac3-188">若要启用 web 应用程序的 Google 身份验证，请使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="71ac3-188">To enable Google authentication for your web application, use the following steps:</span></span>

1. <span data-ttu-id="71ac3-189">在 Visual Studio 2013 中打开你的项目时，打开*Startup.Auth.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="71ac3-189">When your project is open in Visual Studio 2013, open the *Startup.Auth.cs* file:</span></span>

    <span data-ttu-id="71ac3-190">[![](external-authentication-services/_static/image28.png "单击此项可展开图像")](external-authentication-services/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-190">[![](external-authentication-services/_static/image28.png "Click to Expand the Image")](external-authentication-services/_static/image27.png)</span></span>
2. <span data-ttu-id="71ac3-191">查找代码的突出显示的部分：</span><span class="sxs-lookup"><span data-stu-id="71ac3-191">Locate the highlighted section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. <span data-ttu-id="71ac3-192">删除&quot; // &quot;字符以取消注释的代码中，突出显示的行，然后重新编译你的项目：</span><span class="sxs-lookup"><span data-stu-id="71ac3-192">Remove the &quot;//&quot; characters to uncomment the highlighted line of code, and then recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. <span data-ttu-id="71ac3-193">按 F5 以在 web 浏览器中打开 web 应用程序时，你将看到 Google 已被定义为外部身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="71ac3-193">When you press F5 to open your web application in your web browser, you will see that Google has been defined as an external authentication service:</span></span>

    <span data-ttu-id="71ac3-194">[![](external-authentication-services/_static/image30.png "单击此项可展开图像")](external-authentication-services/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-194">[![](external-authentication-services/_static/image30.png "Click to Expand the Image")](external-authentication-services/_static/image29.png)</span></span>
5. <span data-ttu-id="71ac3-195">当您单击**Google**按钮，在浏览器将重定向到 Google 登录页：</span><span class="sxs-lookup"><span data-stu-id="71ac3-195">When you click the **Google** button, your browser will be redirected to the Google login page:</span></span>

    <span data-ttu-id="71ac3-196">[![](external-authentication-services/_static/image32.png "单击此项可展开图像")](external-authentication-services/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-196">[![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)</span></span>
6. <span data-ttu-id="71ac3-197">输入你的 Google 凭据并单击后**登录**，Google 将提示你验证你的 web 应用程序有权访问你的 Google 帐户：</span><span class="sxs-lookup"><span data-stu-id="71ac3-197">After you enter your Google credentials and click **Sign in**, Google will prompt you to verify that your web application has permissions to access your Google account:</span></span>

    <span data-ttu-id="71ac3-198">[![](external-authentication-services/_static/image34.png "单击此项可展开图像")](external-authentication-services/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-198">[![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)</span></span>
7. <span data-ttu-id="71ac3-199">当您单击**Accept**，在 web 浏览器将重定向回到 web 应用程序，这会提示您输入**用户名**你想要将与你的 Google 帐户相关联：</span><span class="sxs-lookup"><span data-stu-id="71ac3-199">When you click **Accept**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Google account:</span></span>

    <span data-ttu-id="71ac3-200">[![](external-authentication-services/_static/image36.png "单击此项可展开图像")](external-authentication-services/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-200">[![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)</span></span>
8. <span data-ttu-id="71ac3-201">在输入您的用户名称并单击后**注册**按钮，web 应用程序将显示默认**主页**为你的 Google 帐户：</span><span class="sxs-lookup"><span data-stu-id="71ac3-201">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Google account:</span></span>

    <span data-ttu-id="71ac3-202">[![](external-authentication-services/_static/image38.png "单击此项可展开图像")](external-authentication-services/_static/image37.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-202">[![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)</span></span>

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a><span data-ttu-id="71ac3-203">启用 Microsoft 身份验证</span><span class="sxs-lookup"><span data-stu-id="71ac3-203">Enabling Microsoft Authentication</span></span>

<span data-ttu-id="71ac3-204">Microsoft 身份验证要求你创建开发人员帐户，并且它需要客户端 ID 和客户端机密才能正常。</span><span class="sxs-lookup"><span data-stu-id="71ac3-204">Microsoft authentication requires you to create a developer account, and it requires a client ID and client secret in order to function.</span></span> <span data-ttu-id="71ac3-205">有关创建 Microsoft 开发人员帐户和获取客户端 ID 和客户端机密的信息，请参阅[ https://go.microsoft.com/fwlink/?LinkID=144070 ](https://go.microsoft.com/fwlink/?LinkID=144070)。</span><span class="sxs-lookup"><span data-stu-id="71ac3-205">For information about creating a Microsoft developer account and obtaining your client ID and client secret, see [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span></span>

<span data-ttu-id="71ac3-206">你一次获取使用者密钥和使用者机密，请使用以下步骤启用 web 应用程序的 Microsoft 身份验证：</span><span class="sxs-lookup"><span data-stu-id="71ac3-206">Once you have obtained your consumer key and consumer secret, use the following steps to enable Microsoft authentication for your web application:</span></span>

1. <span data-ttu-id="71ac3-207">在 Visual Studio 2013 中打开你的项目时，打开*Startup.Auth.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="71ac3-207">When your project is open in Visual Studio 2013, open the *Startup.Auth.cs* file:</span></span>

    <span data-ttu-id="71ac3-208">[![](external-authentication-services/_static/image40.png "单击此项可展开图像")](external-authentication-services/_static/image39.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-208">[![](external-authentication-services/_static/image40.png "Click to Expand the Image")](external-authentication-services/_static/image39.png)</span></span>
2. <span data-ttu-id="71ac3-209">查找代码的突出显示的部分：</span><span class="sxs-lookup"><span data-stu-id="71ac3-209">Locate the highlighted section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. <span data-ttu-id="71ac3-210">删除&quot; // &quot;字符以取消注释的代码中，突出显示的行，然后添加你的客户端 ID 和客户端机密。</span><span class="sxs-lookup"><span data-stu-id="71ac3-210">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your client ID and client secret.</span></span> <span data-ttu-id="71ac3-211">添加这些参数后，可以重新编译你的项目：</span><span class="sxs-lookup"><span data-stu-id="71ac3-211">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. <span data-ttu-id="71ac3-212">按 F5 以在 web 浏览器中打开 web 应用程序时，你将看到 Microsoft 已被定义为外部身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="71ac3-212">When you press F5 to open your web application in your web browser, you will see that Microsoft has been defined as an external authentication service:</span></span>

    <span data-ttu-id="71ac3-213">[![](external-authentication-services/_static/image42.png "单击此项可展开图像")](external-authentication-services/_static/image41.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-213">[![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)</span></span>
5. <span data-ttu-id="71ac3-214">当您单击**Microsoft**按钮，在浏览器将重定向到 Microsoft 登录页：</span><span class="sxs-lookup"><span data-stu-id="71ac3-214">When you click the **Microsoft** button, your browser will be redirected to the Microsoft login page:</span></span>

    <span data-ttu-id="71ac3-215">[![](external-authentication-services/_static/image44.png "单击此项可展开图像")](external-authentication-services/_static/image43.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-215">[![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)</span></span>
6. <span data-ttu-id="71ac3-216">输入 Microsoft 凭据并单击后**登录**，系统会提示以验证你的 web 应用程序有权访问你的 Microsoft 帐户：</span><span class="sxs-lookup"><span data-stu-id="71ac3-216">After you enter your Microsoft credentials and click **Sign in**, you will be prompted to verify that your web application has permissions to access your Microsoft account:</span></span>

    <span data-ttu-id="71ac3-217">[![](external-authentication-services/_static/image46.png "单击此项可展开图像")](external-authentication-services/_static/image45.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-217">[![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)</span></span>
7. <span data-ttu-id="71ac3-218">当您单击**是**，在 web 浏览器将重定向回到 web 应用程序，这会提示您输入**用户名**你想要将与你的 Microsoft 帐户相关联：</span><span class="sxs-lookup"><span data-stu-id="71ac3-218">When you click **Yes**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Microsoft account:</span></span>

    <span data-ttu-id="71ac3-219">[![](external-authentication-services/_static/image48.png "单击此项可展开图像")](external-authentication-services/_static/image47.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-219">[![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)</span></span>
8. <span data-ttu-id="71ac3-220">在输入您的用户名称并单击后**注册**按钮，web 应用程序将显示默认**主页**你的 Microsoft 帐户：</span><span class="sxs-lookup"><span data-stu-id="71ac3-220">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Microsoft account:</span></span>

    <span data-ttu-id="71ac3-221">[![](external-authentication-services/_static/image50.png "单击此项可展开图像")](external-authentication-services/_static/image49.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-221">[![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)</span></span>

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a><span data-ttu-id="71ac3-222">启用 Twitter 身份验证</span><span class="sxs-lookup"><span data-stu-id="71ac3-222">Enabling Twitter Authentication</span></span>

<span data-ttu-id="71ac3-223">Twitter 身份验证要求你创建开发人员帐户，并且它需要使用者密钥和使用者机密才能正常。</span><span class="sxs-lookup"><span data-stu-id="71ac3-223">Twitter authentication requires you to create a developer account, and it requires a consumer key and consumer secret in order to function.</span></span> <span data-ttu-id="71ac3-224">有关创建 Twitter 开发人员帐户并获取使用者密钥和使用者机密的信息，请参阅[ https://go.microsoft.com/fwlink/?LinkID=252166 ](https://go.microsoft.com/fwlink/?LinkID=252166)。</span><span class="sxs-lookup"><span data-stu-id="71ac3-224">For information about creating a Twitter developer account and obtaining your consumer key and consumer secret, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="71ac3-225">你一次获取使用者密钥和使用者机密，请使用以下步骤启用 Twitter 身份验证 web 应用程序：</span><span class="sxs-lookup"><span data-stu-id="71ac3-225">Once you have obtained your consumer key and consumer secret, use the following steps to enable Twitter authentication for your web application:</span></span>

1. <span data-ttu-id="71ac3-226">在 Visual Studio 2013 中打开你的项目时，打开*Startup.Auth.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="71ac3-226">When your project is open in Visual Studio 2013, open the *Startup.Auth.cs* file:</span></span>

    <span data-ttu-id="71ac3-227">[![](external-authentication-services/_static/image52.png "单击此项可展开图像")](external-authentication-services/_static/image51.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-227">[![](external-authentication-services/_static/image52.png "Click to Expand the Image")](external-authentication-services/_static/image51.png)</span></span>
2. <span data-ttu-id="71ac3-228">查找代码的突出显示的部分：</span><span class="sxs-lookup"><span data-stu-id="71ac3-228">Locate the highlighted section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. <span data-ttu-id="71ac3-229">删除&quot; // &quot;字符，取消注释的代码中，突出显示的行，并添加使用者密钥和使用者机密。</span><span class="sxs-lookup"><span data-stu-id="71ac3-229">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your consumer key and consumer secret.</span></span> <span data-ttu-id="71ac3-230">添加这些参数后，可以重新编译你的项目：</span><span class="sxs-lookup"><span data-stu-id="71ac3-230">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. <span data-ttu-id="71ac3-231">按 F5 以在 web 浏览器中打开 web 应用程序时，你将看到 Twitter 已被定义为外部身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="71ac3-231">When you press F5 to open your web application in your web browser, you will see that Twitter has been defined as an external authentication service:</span></span>

    <span data-ttu-id="71ac3-232">[![](external-authentication-services/_static/image54.png "单击此项可展开图像")](external-authentication-services/_static/image53.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-232">[![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)</span></span>
5. <span data-ttu-id="71ac3-233">当您单击**Twitter**按钮，在浏览器将重定向到 Twitter 登录页：</span><span class="sxs-lookup"><span data-stu-id="71ac3-233">When you click the **Twitter** button, your browser will be redirected to the Twitter login page:</span></span>

    <span data-ttu-id="71ac3-234">[![](external-authentication-services/_static/image56.png "单击此项可展开图像")](external-authentication-services/_static/image55.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-234">[![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)</span></span>
6. <span data-ttu-id="71ac3-235">输入你的 Twitter 凭据，然后单击后**授权应用**，在 web 浏览器将重定向回到 web 应用程序，这会提示您输入**用户名**你想要将与相关联你的 Twitter 帐户：</span><span class="sxs-lookup"><span data-stu-id="71ac3-235">After you enter your Twitter credentials and click **Authorize app**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Twitter account:</span></span>

    <span data-ttu-id="71ac3-236">[![](external-authentication-services/_static/image58.png "单击此项可展开图像")](external-authentication-services/_static/image57.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-236">[![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)</span></span>
7. <span data-ttu-id="71ac3-237">在输入您的用户名称并单击后**注册**按钮，web 应用程序将显示默认**主页**使用 Twitter 帐户：</span><span class="sxs-lookup"><span data-stu-id="71ac3-237">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Twitter account:</span></span>

    <span data-ttu-id="71ac3-238">[![](external-authentication-services/_static/image60.png "单击此项可展开图像")](external-authentication-services/_static/image59.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-238">[![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)</span></span>

<a id="MOREINFO"></a>
## <a name="additional-information"></a><span data-ttu-id="71ac3-239">其他信息</span><span class="sxs-lookup"><span data-stu-id="71ac3-239">Additional Information</span></span>

<span data-ttu-id="71ac3-240">有关创建使用 OAuth 和 OpenID 的应用程序的其他信息，请参阅以下 Url:</span><span class="sxs-lookup"><span data-stu-id="71ac3-240">For additional information about creating applications that use OAuth and OpenID, see the following URLs:</span></span>

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a><span data-ttu-id="71ac3-241">合并外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="71ac3-241">Combining External Authentication Services</span></span>

<span data-ttu-id="71ac3-242">为更大的灵活性，可以在同一时间定义多个外部身份验证服务-这允许你的 web 应用程序的用户使用来自任何启用的外部身份验证服务的帐户：</span><span class="sxs-lookup"><span data-stu-id="71ac3-242">For greater flexibility, you can define multiple external authentication services at the same time - this allows your web application's users to use an account from any of the enabled external authentication services:</span></span>

<span data-ttu-id="71ac3-243">[![](external-authentication-services/_static/image62.png "单击此项可展开图像")](external-authentication-services/_static/image61.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-243">[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)</span></span>

<a id="FQDN"></a>
### <a name="configuring-iis-express-to-use-a-fully-qualified-domain-name"></a><span data-ttu-id="71ac3-244">配置 IIS Express 以使用完全限定的域名</span><span class="sxs-lookup"><span data-stu-id="71ac3-244">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>

<span data-ttu-id="71ac3-245">某些外部身份验证提供程序不支持使用类似的 HTTP 地址来测试你的应用程序`http://localhost:port/`。</span><span class="sxs-lookup"><span data-stu-id="71ac3-245">Some external authentication providers do not support testing your application by using an HTTP address like `http://localhost:port/`.</span></span> <span data-ttu-id="71ac3-246">若要解决此问题，可以添加到主机文件的完全限定域名 (FQDN) 的静态映射并在 Visual Studio 2013 中要用于 FQDN 测试/调试配置项目的选项。</span><span class="sxs-lookup"><span data-stu-id="71ac3-246">To work around this issue, you can add a static Fully Qualified Domain Name (FQDN) mapping to your HOSTS file and configure your project options in Visual Studio 2013 to use the FQDN for testing/debugging.</span></span> <span data-ttu-id="71ac3-247">为此，请使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="71ac3-247">To do so, use the following steps:</span></span>

- <span data-ttu-id="71ac3-248">添加映射的主机文件的静态 FQDN:</span><span class="sxs-lookup"><span data-stu-id="71ac3-248">Add a static FQDN mapping your HOSTS file:</span></span>

  1. <span data-ttu-id="71ac3-249">在 Windows 中打开提升的命令提示符。</span><span class="sxs-lookup"><span data-stu-id="71ac3-249">Open an elevated command prompt in Windows.</span></span>
  2. <span data-ttu-id="71ac3-250">键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="71ac3-250">Type the following command:</span></span>

      <span data-ttu-id="71ac3-251"><kbd>记事本 %WinDir%\system32\drivers\etc\hosts</kbd></span><span class="sxs-lookup"><span data-stu-id="71ac3-251"><kbd>notepad %WinDir%\system32\drivers\etc\hosts</kbd></span></span>
  3. <span data-ttu-id="71ac3-252">类似于以下条目添加到主机文件中：</span><span class="sxs-lookup"><span data-stu-id="71ac3-252">Add an entry like the following to the HOSTS file:</span></span>

      <span data-ttu-id="71ac3-253"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span><span class="sxs-lookup"><span data-stu-id="71ac3-253"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span></span>
  4. <span data-ttu-id="71ac3-254">保存并关闭 HOSTS 文件。</span><span class="sxs-lookup"><span data-stu-id="71ac3-254">Save and close your HOSTS file.</span></span>

- <span data-ttu-id="71ac3-255">将 Visual Studio 项目配置为使用 FQDN:</span><span class="sxs-lookup"><span data-stu-id="71ac3-255">Configure your Visual Studio project to use the FQDN:</span></span>

  1. <span data-ttu-id="71ac3-256">在 Visual Studio 2013 中打开你的项目时，单击**项目**菜单，然后选择你的项目的属性。</span><span class="sxs-lookup"><span data-stu-id="71ac3-256">When your project is open in Visual Studio 2013, click the **Project** menu, and then select your project's properties.</span></span> <span data-ttu-id="71ac3-257">例如，可以选择**WebApplication1 属性**。</span><span class="sxs-lookup"><span data-stu-id="71ac3-257">For example, you might select **WebApplication1 Properties**.</span></span>
  2. <span data-ttu-id="71ac3-258">选择**Web**选项卡。</span><span class="sxs-lookup"><span data-stu-id="71ac3-258">Select the **Web** tab.</span></span>
  3. <span data-ttu-id="71ac3-259">输入的 FQDN<strong>项目 Url</strong>。</span><span class="sxs-lookup"><span data-stu-id="71ac3-259">Enter your FQDN for the <strong>Project Url</strong>.</span></span> <span data-ttu-id="71ac3-260">例如，应输入<kbd> <http://www.wingtiptoys.com> </kbd> ，如果已添加到主机文件的 FQDN 映射。</span><span class="sxs-lookup"><span data-stu-id="71ac3-260">For example, you would enter <kbd><http://www.wingtiptoys.com></kbd> if that was the FQDN mapping that you added to your HOSTS file.</span></span>

- <span data-ttu-id="71ac3-261">配置 IIS Express 以使用 FQDN 作为你的应用程序：</span><span class="sxs-lookup"><span data-stu-id="71ac3-261">Configure IIS Express to use the FQDN for your application:</span></span>

    1. <span data-ttu-id="71ac3-262">在 Windows 中打开提升的命令提示符。</span><span class="sxs-lookup"><span data-stu-id="71ac3-262">Open an elevated command prompt in Windows.</span></span>
    2. <span data-ttu-id="71ac3-263">键入以下命令以将更改为在 IIS Express 的文件夹：</span><span class="sxs-lookup"><span data-stu-id="71ac3-263">Type the following command to change to your IIS Express folder:</span></span>

        <span data-ttu-id="71ac3-264"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span><span class="sxs-lookup"><span data-stu-id="71ac3-264"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span></span>
    3. <span data-ttu-id="71ac3-265">键入以下命令以将 FQDN 添加到你的应用程序：</span><span class="sxs-lookup"><span data-stu-id="71ac3-265">Type the following command to add the FQDN to your application:</span></span>

        <span data-ttu-id="71ac3-266"><kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='\*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span><span class="sxs-lookup"><span data-stu-id="71ac3-266"><kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='\*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span></span>

  <span data-ttu-id="71ac3-267">其中**WebApplication1**是你的项目的名称和**bindingInformation**包含你想要用于测试的端口号和 FQDN。</span><span class="sxs-lookup"><span data-stu-id="71ac3-267">Where **WebApplication1** is the name of your project and **bindingInformation** contains the port number and FQDN that you want to use for your testing.</span></span>

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a><span data-ttu-id="71ac3-268">如何获取 Microsoft 身份验证应用程序设置</span><span class="sxs-lookup"><span data-stu-id="71ac3-268">How to Obtain your Application Settings for Microsoft Authentication</span></span>

<span data-ttu-id="71ac3-269">链接到 Windows Live 进行 Microsoft 身份验证的应用程序是一个简单的过程。</span><span class="sxs-lookup"><span data-stu-id="71ac3-269">Linking an application to Windows Live for Microsoft Authentication is a simple process.</span></span> <span data-ttu-id="71ac3-270">如果已链接到 Windows Live 应用程序，可以使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="71ac3-270">If you have not already linked an application to Windows Live, you can use the following steps:</span></span>

1. <span data-ttu-id="71ac3-271">浏览到[ https://go.microsoft.com/fwlink/?LinkID=144070 ](https://go.microsoft.com/fwlink/?LinkID=144070)并输入你的 Microsoft 帐户名和密码出现提示时，然后单击**登录**:</span><span class="sxs-lookup"><span data-stu-id="71ac3-271">Browse to [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) and enter your Microsoft account name and password when prompted, then click **Sign in**:</span></span>

    <span data-ttu-id="71ac3-272">[![](external-authentication-services/_static/image64.png "单击此项可展开图像")](external-authentication-services/_static/image63.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-272">[![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png)</span></span>
2. <span data-ttu-id="71ac3-273">输入的名称和出现提示时，应用程序的语言，然后单击**我接受**:</span><span class="sxs-lookup"><span data-stu-id="71ac3-273">Enter the name and language of your application when prompted, and then click **I accept**:</span></span>

    <span data-ttu-id="71ac3-274">[![](external-authentication-services/_static/image66.png "单击此项可展开图像")](external-authentication-services/_static/image65.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-274">[![](external-authentication-services/_static/image66.png "Click to Expand the Image")](external-authentication-services/_static/image65.png)</span></span>
3. <span data-ttu-id="71ac3-275">上**API 设置**为应用程序页上，输入你的应用程序和副本的重定向域**客户端 ID**并**客户端机密**为你的项目，然后单击**保存**:</span><span class="sxs-lookup"><span data-stu-id="71ac3-275">On the **API Settings** page for your application, enter the redirect domain for your application and copy the **Client ID** and **Client secret** for your project, and then click **Save**:</span></span>

    <span data-ttu-id="71ac3-276">[![](external-authentication-services/_static/image68.png "单击此项可展开图像")](external-authentication-services/_static/image67.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-276">[![](external-authentication-services/_static/image68.png "Click to Expand the Image")](external-authentication-services/_static/image67.png)</span></span>

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a><span data-ttu-id="71ac3-277">可选： 禁用本地注册</span><span class="sxs-lookup"><span data-stu-id="71ac3-277">Optional: Disable Local Registration</span></span>

<span data-ttu-id="71ac3-278">当前 ASP.NET 本地注册功能不会阻止自动的程序 （机器人） 帐户; 创建成员例如，通过使用智能机器人应用程序防护和验证等技术[CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)。</span><span class="sxs-lookup"><span data-stu-id="71ac3-278">The current ASP.NET local registration functionality does not prevent automated programs (bots) from creating member accounts; for example, by using a bot-prevention and validation technology like [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md).</span></span> <span data-ttu-id="71ac3-279">因此，应删除的登录页上的本地登录窗体和注册链接。</span><span class="sxs-lookup"><span data-stu-id="71ac3-279">Because of this, you should remove the local login form and registration link on the login page.</span></span> <span data-ttu-id="71ac3-280">若要执行此操作，打开 *\_Login.cshtml*在项目中，页上，然后注释掉本地登录面板和注册链接的行。</span><span class="sxs-lookup"><span data-stu-id="71ac3-280">To do so, open the *\_Login.cshtml* page in your project, and then comment out the lines for the local login panel and the registration link.</span></span> <span data-ttu-id="71ac3-281">在生成的页面应如下面的代码示例所示：</span><span class="sxs-lookup"><span data-stu-id="71ac3-281">The resulting page should look like the following code sample:</span></span>

[!code-html[Main](external-authentication-services/samples/sample10.html)]

<span data-ttu-id="71ac3-282">一旦已禁用本地登录面板和注册链接，您的登录页将仅显示已启用的外部身份验证提供程序：</span><span class="sxs-lookup"><span data-stu-id="71ac3-282">Once the local login panel and the registration link have been disabled, your login page will only display the external authentication providers that you have enabled:</span></span>

<span data-ttu-id="71ac3-283">[![](external-authentication-services/_static/image70.png "单击此项可展开图像")](external-authentication-services/_static/image69.png)</span><span class="sxs-lookup"><span data-stu-id="71ac3-283">[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)</span></span>
