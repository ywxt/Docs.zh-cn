---
title: Azure Active Directory B2C ASP.NET Core中使用云身份验证
author: camsoper
description: 了解如何设置与 ASP.NET Core的 Azure Active Directory B2C 身份验证。
ms.date: 01/25/2018
ms.custom: mvc
uid: security/authentication/azure-ad-b2c
ms.openlocfilehash: caadeec57272ee2823452ed7c4b91e7aca07c3f4
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36272417"
---
# <a name="cloud-authentication-with-azure-active-directory-b2c-in-aspnet-core"></a><span data-ttu-id="9a48b-103">Azure Active Directory B2C ASP.NET Core中使用云身份验证</span><span class="sxs-lookup"><span data-stu-id="9a48b-103">Cloud authentication with Azure Active Directory B2C in ASP.NET Core</span></span>

<span data-ttu-id="9a48b-104">作者：[Cam Soper](https://twitter.com/camsoper)</span><span class="sxs-lookup"><span data-stu-id="9a48b-104">By [Cam Soper](https://twitter.com/camsoper)</span></span>

<span data-ttu-id="9a48b-105">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C) 是为 web 和移动应用的云标识管理解决方案。</span><span class="sxs-lookup"><span data-stu-id="9a48b-105">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C) is a cloud identity management solution for web and mobile apps.</span></span> <span data-ttu-id="9a48b-106">服务提供用于在云中和本地托管的应用的身份验证。</span><span class="sxs-lookup"><span data-stu-id="9a48b-106">The service provides authentication for apps hosted in the cloud and on-premises.</span></span> <span data-ttu-id="9a48b-107">身份验证类型包括个人帐户，社交网络帐户，以及联合企业帐户。</span><span class="sxs-lookup"><span data-stu-id="9a48b-107">Authentication types include individual accounts, social network accounts, and federated enterprise accounts.</span></span> <span data-ttu-id="9a48b-108">此外，Azure AD B2C 可以提供以最小配置多因素身份验证。</span><span class="sxs-lookup"><span data-stu-id="9a48b-108">Additionally, Azure AD B2C can provide multi-factor authentication with minimal configuration.</span></span>

> [!TIP]
> <span data-ttu-id="9a48b-109">Azure Active Directory (Azure AD) Azure AD B2C 包括单独的产品。</span><span class="sxs-lookup"><span data-stu-id="9a48b-109">Azure Active Directory (Azure AD) Azure AD B2C are separate product offerings.</span></span> <span data-ttu-id="9a48b-110">Azure AD 租户表示是一个组织，而 Azure AD B2C 租户表示标识要用于信赖方应用程序的集合。</span><span class="sxs-lookup"><span data-stu-id="9a48b-110">An Azure AD tenant represents an organization, while an Azure AD B2C tenant represents a collection of identities to be used with relying party applications.</span></span> <span data-ttu-id="9a48b-111">若要了解详细信息，请参阅[Azure AD B2C： 常见问题 (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs)。</span><span class="sxs-lookup"><span data-stu-id="9a48b-111">To learn more, see [Azure AD B2C: Frequently asked questions (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs).</span></span>

<span data-ttu-id="9a48b-112">在本教程中，学习如何：</span><span class="sxs-lookup"><span data-stu-id="9a48b-112">In this tutorial, learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9a48b-113">创建 Azure Active Directory B2C 租户</span><span class="sxs-lookup"><span data-stu-id="9a48b-113">Create an Azure Active Directory B2C tenant</span></span>
> * <span data-ttu-id="9a48b-114">在 Azure AD B2C 注册某个应用程序</span><span class="sxs-lookup"><span data-stu-id="9a48b-114">Register an app in Azure AD B2C</span></span>
> * <span data-ttu-id="9a48b-115">使用 Visual Studio 创建 ASP.NET Core web 应用配置为使用 Azure AD B2C 租户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="9a48b-115">Use Visual Studio to create an ASP.NET Core web app configured to use the Azure AD B2C tenant for authentication</span></span>
> * <span data-ttu-id="9a48b-116">配置控制 Azure AD B2C 租户的行为的策略</span><span class="sxs-lookup"><span data-stu-id="9a48b-116">Configure policies controlling the behavior of the Azure AD B2C tenant</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a48b-117">系统必备</span><span class="sxs-lookup"><span data-stu-id="9a48b-117">Prerequisites</span></span>

<span data-ttu-id="9a48b-118">对于本演练具备以下条件：</span><span class="sxs-lookup"><span data-stu-id="9a48b-118">The following are required for this walkthrough:</span></span>

* [<span data-ttu-id="9a48b-119">Microsoft Azure 订阅</span><span class="sxs-lookup"><span data-stu-id="9a48b-119">Microsoft Azure subscription</span></span>](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)
* <span data-ttu-id="9a48b-120">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) （任意版本）</span><span class="sxs-lookup"><span data-stu-id="9a48b-120">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) (any edition)</span></span>

## <a name="create-the-azure-active-directory-b2c-tenant"></a><span data-ttu-id="9a48b-121">创建 Azure Active Directory B2C 租户</span><span class="sxs-lookup"><span data-stu-id="9a48b-121">Create the Azure Active Directory B2C tenant</span></span>

<span data-ttu-id="9a48b-122">创建 Azure Active Directory B2C 租户[文档中所述](/azure/active-directory-b2c/active-directory-b2c-get-started)。</span><span class="sxs-lookup"><span data-stu-id="9a48b-122">Create an Azure Active Directory B2C tenant [as described in the documentation](/azure/active-directory-b2c/active-directory-b2c-get-started).</span></span> <span data-ttu-id="9a48b-123">出现提示时，将租户与 Azure 订阅相关联是可选的出于本教程。</span><span class="sxs-lookup"><span data-stu-id="9a48b-123">When prompted, associating the tenant with an Azure subscription is optional for this tutorial.</span></span>

## <a name="register-the-app-in-azure-ad-b2c"></a><span data-ttu-id="9a48b-124">在 Azure AD B2C 中注册应用程序</span><span class="sxs-lookup"><span data-stu-id="9a48b-124">Register the app in Azure AD B2C</span></span>

<span data-ttu-id="9a48b-125">新创建的 Azure AD B2C 租户中注册你的应用使用[文档中的步骤](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app)下**注册 web 应用**部分。</span><span class="sxs-lookup"><span data-stu-id="9a48b-125">In the newly created Azure AD B2C tenant, register your app using [the steps in the documentation](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app) under the **Register a web app** section.</span></span> <span data-ttu-id="9a48b-126">在停止**创建 web 应用程序客户端密钥**部分。</span><span class="sxs-lookup"><span data-stu-id="9a48b-126">Stop at the **Create a web app client secret** section.</span></span> <span data-ttu-id="9a48b-127">出于本教程中，无需客户端密钥。</span><span class="sxs-lookup"><span data-stu-id="9a48b-127">A client secret isn't required for this tutorial.</span></span> 

<span data-ttu-id="9a48b-128">使用以下值：</span><span class="sxs-lookup"><span data-stu-id="9a48b-128">Use the following values:</span></span>

| <span data-ttu-id="9a48b-129">设置</span><span class="sxs-lookup"><span data-stu-id="9a48b-129">Setting</span></span>                       | <span data-ttu-id="9a48b-130">“值”</span><span class="sxs-lookup"><span data-stu-id="9a48b-130">Value</span></span>                     | <span data-ttu-id="9a48b-131">说明</span><span class="sxs-lookup"><span data-stu-id="9a48b-131">Notes</span></span>                                                                                                                                                                                              |
|-------------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a48b-132">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a48b-132">**Name**</span></span>                      | <span data-ttu-id="9a48b-133">*&lt;应用程序名称&gt;*</span><span class="sxs-lookup"><span data-stu-id="9a48b-133">*&lt;app name&gt;*</span></span>        | <span data-ttu-id="9a48b-134">输入**名称**描述你的应用对使用者的应用。</span><span class="sxs-lookup"><span data-stu-id="9a48b-134">Enter a **Name** for the app that describes your app to consumers.</span></span>                                                                                                                                 |
| <span data-ttu-id="9a48b-135">**包括 web 应用程序/web API**</span><span class="sxs-lookup"><span data-stu-id="9a48b-135">**Include web app / web API**</span></span> | <span data-ttu-id="9a48b-136">是</span><span class="sxs-lookup"><span data-stu-id="9a48b-136">Yes</span></span>                       |                                                                                                                                                                                                    |
| <span data-ttu-id="9a48b-137">**允许隐式流**</span><span class="sxs-lookup"><span data-stu-id="9a48b-137">**Allow implicit flow**</span></span>       | <span data-ttu-id="9a48b-138">是</span><span class="sxs-lookup"><span data-stu-id="9a48b-138">Yes</span></span>                       |                                                                                                                                                                                                    |
| <span data-ttu-id="9a48b-139">**回复 URL**</span><span class="sxs-lookup"><span data-stu-id="9a48b-139">**Reply URL**</span></span>                 | `https://localhost:44300` | <span data-ttu-id="9a48b-140">答复 Url 是 Azure AD B2C 其中返回您的应用程序请求的任何令牌的终结点。</span><span class="sxs-lookup"><span data-stu-id="9a48b-140">Reply URLs are endpoints where Azure AD B2C returns any tokens that your app requests.</span></span> <span data-ttu-id="9a48b-141">Visual Studio 提供要使用的答复 URL。</span><span class="sxs-lookup"><span data-stu-id="9a48b-141">Visual Studio provides the Reply URL to use.</span></span> <span data-ttu-id="9a48b-142">现在，输入`https://localhost:44300`完成窗体。</span><span class="sxs-lookup"><span data-stu-id="9a48b-142">For now, enter `https://localhost:44300` to complete the form.</span></span> |
| <span data-ttu-id="9a48b-143">**应用程序 ID URI**</span><span class="sxs-lookup"><span data-stu-id="9a48b-143">**App ID URI**</span></span>                | <span data-ttu-id="9a48b-144">将保留为空</span><span class="sxs-lookup"><span data-stu-id="9a48b-144">Leave blank</span></span>               | <span data-ttu-id="9a48b-145">无需进行本教程。</span><span class="sxs-lookup"><span data-stu-id="9a48b-145">Not required for this tutorial.</span></span>                                                                                                                                                                    |
| <span data-ttu-id="9a48b-146">**包括本机客户端**</span><span class="sxs-lookup"><span data-stu-id="9a48b-146">**Include native client**</span></span>     | <span data-ttu-id="9a48b-147">否</span><span class="sxs-lookup"><span data-stu-id="9a48b-147">No</span></span>                        |                                                                                                                                                                                                    |

> [!WARNING]
> <span data-ttu-id="9a48b-148">如果设置非 localhost 答复 URL，请注意[了允许的答复 URL 列表中的约束](/azure/active-directory-b2c/active-directory-b2c-app-registration#choosing-a-web-app-or-api-reply-url)。</span><span class="sxs-lookup"><span data-stu-id="9a48b-148">If setting up a non-localhost Reply URL, be aware of the [constraints on what is allowed in the Reply URL list](/azure/active-directory-b2c/active-directory-b2c-app-registration#choosing-a-web-app-or-api-reply-url).</span></span> 

<span data-ttu-id="9a48b-149">注册应用后，显示的租户中的应用列表。</span><span class="sxs-lookup"><span data-stu-id="9a48b-149">After the app is registered, the list of apps in the tenant is displayed.</span></span> <span data-ttu-id="9a48b-150">选择刚刚注册的应用。</span><span class="sxs-lookup"><span data-stu-id="9a48b-150">Select the app that was just registered.</span></span> <span data-ttu-id="9a48b-151">选择**复制**右侧的图标**应用程序 ID**字段可将它复制到剪贴板。</span><span class="sxs-lookup"><span data-stu-id="9a48b-151">Select the **Copy** icon to the right of the **Application ID** field to copy it to the clipboard.</span></span>

<span data-ttu-id="9a48b-152">执行任何操作的详细信息在此时，可以在 Azure AD B2C 租户中配置，但使浏览器窗口保持打开状态。</span><span class="sxs-lookup"><span data-stu-id="9a48b-152">Nothing more can be configured in the Azure AD B2C tenant at this time, but leave the browser window open.</span></span> <span data-ttu-id="9a48b-153">创建 ASP.NET Core 应用后，没有更多的配置。</span><span class="sxs-lookup"><span data-stu-id="9a48b-153">There is more configuration after the ASP.NET Core app is created.</span></span>

## <a name="create-an-aspnet-core-app-in-visual-studio-2017"></a><span data-ttu-id="9a48b-154">在 Visual Studio 2017 年 1 中创建 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="9a48b-154">Create an ASP.NET Core app in Visual Studio 2017</span></span>

<span data-ttu-id="9a48b-155">Visual Studio Web 应用程序模板可以配置为使用 Azure AD B2C 租户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9a48b-155">The Visual Studio Web Application template can be configured to use the Azure AD B2C tenant for authentication.</span></span>

<span data-ttu-id="9a48b-156">在 Visual Studio 中：</span><span class="sxs-lookup"><span data-stu-id="9a48b-156">In Visual Studio:</span></span>

1. <span data-ttu-id="9a48b-157">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a48b-157">Create a new ASP.NET Core Web Application.</span></span> 
2. <span data-ttu-id="9a48b-158">选择**Web 应用程序**从模板列表中。</span><span class="sxs-lookup"><span data-stu-id="9a48b-158">Select **Web Application** from the list of templates.</span></span>
3. <span data-ttu-id="9a48b-159">选择**更改身份验证**按钮。</span><span class="sxs-lookup"><span data-stu-id="9a48b-159">Select the **Change Authentication** button.</span></span>
    
    ![更改身份验证按钮](./azure-ad-b2c/_static/changeauth.png)

4. <span data-ttu-id="9a48b-161">在**更改身份验证**对话框中，选择**单个用户帐户**，然后选择**连接到现有用户存储在云中**下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="9a48b-161">In the **Change Authentication** dialog, select **Individual User Accounts**, and then select **Connect to an existing user store in the cloud** in the dropdown.</span></span> 
    
    ![更改身份验证对话框](./azure-ad-b2c/_static/changeauthdialog.png)

5. <span data-ttu-id="9a48b-163">完成窗体具有以下值：</span><span class="sxs-lookup"><span data-stu-id="9a48b-163">Complete the form with the following values:</span></span>
    
    | <span data-ttu-id="9a48b-164">设置</span><span class="sxs-lookup"><span data-stu-id="9a48b-164">Setting</span></span>                       | <span data-ttu-id="9a48b-165">“值”</span><span class="sxs-lookup"><span data-stu-id="9a48b-165">Value</span></span>                                                 |
    |-------------------------------|-------------------------------------------------------|
    | <span data-ttu-id="9a48b-166">**域名**</span><span class="sxs-lookup"><span data-stu-id="9a48b-166">**Domain Name**</span></span>               | <span data-ttu-id="9a48b-167">*&lt;B2C 租户的域名&gt;*</span><span class="sxs-lookup"><span data-stu-id="9a48b-167">*&lt;the domain name of your B2C tenant&gt;*</span></span>          |
    | <span data-ttu-id="9a48b-168">**应用程序 ID**</span><span class="sxs-lookup"><span data-stu-id="9a48b-168">**Application ID**</span></span>            | <span data-ttu-id="9a48b-169">*&lt;粘贴剪贴板中的应用程序 ID&gt;*</span><span class="sxs-lookup"><span data-stu-id="9a48b-169">*&lt;paste the Application ID from the clipboard&gt;*</span></span> |
    | <span data-ttu-id="9a48b-170">**回调路径**</span><span class="sxs-lookup"><span data-stu-id="9a48b-170">**Callback Path**</span></span>             | <span data-ttu-id="9a48b-171">*&lt;使用默认值&gt;*</span><span class="sxs-lookup"><span data-stu-id="9a48b-171">*&lt;use the default value&gt;*</span></span>                       |
    | <span data-ttu-id="9a48b-172">**注册或登录策略**</span><span class="sxs-lookup"><span data-stu-id="9a48b-172">**Sign-up or sign-in policy**</span></span> | `B2C_1_SiUpIn`                                        |
    | <span data-ttu-id="9a48b-173">**重置密码策略**</span><span class="sxs-lookup"><span data-stu-id="9a48b-173">**Reset password policy**</span></span>     | `B2C_1_SSPR`                                          |
    | <span data-ttu-id="9a48b-174">**编辑配置文件策略**</span><span class="sxs-lookup"><span data-stu-id="9a48b-174">**Edit profile policy**</span></span>       | <span data-ttu-id="9a48b-175">*&lt;将保留为空&gt;*</span><span class="sxs-lookup"><span data-stu-id="9a48b-175">*&lt;leave blank&gt;*</span></span>                                 |
    
    <span data-ttu-id="9a48b-176">选择**复制**旁边链接**答复 URI**将答复 URI 复制到剪贴板。</span><span class="sxs-lookup"><span data-stu-id="9a48b-176">Select the **Copy** link next to **Reply URI** to copy the Reply URI to the clipboard.</span></span> <span data-ttu-id="9a48b-177">选择**确定**关闭**更改身份验证**对话框。</span><span class="sxs-lookup"><span data-stu-id="9a48b-177">Select **OK** to close the **Change Authentication** dialog.</span></span> <span data-ttu-id="9a48b-178">选择**确定**创建 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9a48b-178">Select **OK** to create the web app.</span></span>

## <a name="finish-the-b2c-app-registration"></a><span data-ttu-id="9a48b-179">完成 B2C 应用程序注册</span><span class="sxs-lookup"><span data-stu-id="9a48b-179">Finish the B2C app registration</span></span>

<span data-ttu-id="9a48b-180">返回到 B2C 应用程序属性仍处于打开状态的浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="9a48b-180">Return to the browser window with the B2C app properties still open.</span></span> <span data-ttu-id="9a48b-181">更改临时**答复 URL**从 Visual Studio 指定更早版本的值复制。</span><span class="sxs-lookup"><span data-stu-id="9a48b-181">Change the temporary **Reply URL** specified earlier to the value copied from Visual Studio.</span></span> <span data-ttu-id="9a48b-182">选择**保存**在窗口的顶部。</span><span class="sxs-lookup"><span data-stu-id="9a48b-182">Select **Save** at the top of the window.</span></span>

> [!TIP]
> <span data-ttu-id="9a48b-183">如果未复制的答复 URL，在 web 项目属性中，使用调试选项卡的 SSL 地址并追加**CallbackPath**值从*appsettings.json*。</span><span class="sxs-lookup"><span data-stu-id="9a48b-183">If you didn't copy the Reply URL, use the SSL address from the Debug tab in the web project properties, and append the **CallbackPath** value from *appsettings.json*.</span></span>

## <a name="configure-policies"></a><span data-ttu-id="9a48b-184">配置策略</span><span class="sxs-lookup"><span data-stu-id="9a48b-184">Configure policies</span></span>

<span data-ttu-id="9a48b-185">使用到的 Azure AD B2C 文档中的步骤[创建注册或登录策略](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy)，，然后[创建密码重置策略](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-password-reset-policy)。</span><span class="sxs-lookup"><span data-stu-id="9a48b-185">Use the steps in the Azure AD B2C documentation to [create a sign-up or sign-in policy](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy), and then [create a password reset policy](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-password-reset-policy).</span></span> <span data-ttu-id="9a48b-186">使用的文档中提供的示例值**标识提供程序**，**注册属性**，和**应用程序声明**。</span><span class="sxs-lookup"><span data-stu-id="9a48b-186">Use the example values provided in the documentation for **Identity providers**, **Sign-up attributes**, and **Application claims**.</span></span> <span data-ttu-id="9a48b-187">使用**立即运行**是可选的按钮以测试这些策略，如文档中所述。</span><span class="sxs-lookup"><span data-stu-id="9a48b-187">Using the **Run now** button to test the policies as described in the documentation is optional.</span></span>

> [!WARNING]
> <span data-ttu-id="9a48b-188">确保策略名称严格按说明在文档中，并与这些策略中使用**更改身份验证**Visual Studio 中的对话框。</span><span class="sxs-lookup"><span data-stu-id="9a48b-188">Ensure the policy names are exactly as described in the documentation, as those policies were used in the **Change Authentication** dialog in Visual Studio.</span></span> <span data-ttu-id="9a48b-189">策略名称可以验证在*appsettings.json*。</span><span class="sxs-lookup"><span data-stu-id="9a48b-189">The policy names can be verified in *appsettings.json*.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="9a48b-190">运行应用</span><span class="sxs-lookup"><span data-stu-id="9a48b-190">Run the app</span></span>

<span data-ttu-id="9a48b-191">在 Visual Studio 中，按**F5**生成并运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a48b-191">In Visual Studio, press **F5** to build and run the app.</span></span> <span data-ttu-id="9a48b-192">Web 应用启动后，选择**登录**。</span><span class="sxs-lookup"><span data-stu-id="9a48b-192">After the web app launches, select **Sign in**.</span></span>

![登录到应用](./azure-ad-b2c/_static/signin.png)

<span data-ttu-id="9a48b-194">浏览器将重定向到 Azure AD B2C 租户。</span><span class="sxs-lookup"><span data-stu-id="9a48b-194">The browser redirects to the Azure AD B2C tenant.</span></span> <span data-ttu-id="9a48b-195">使用现有帐户登录 （如果已创建一个测试策略） 或选择**立即注册**创建新帐户。</span><span class="sxs-lookup"><span data-stu-id="9a48b-195">Sign in with an existing account (if one was created testing the policies) or select **Sign up now** to create a new account.</span></span> <span data-ttu-id="9a48b-196">**忘记了密码？** 链接用于重置忘记了的密码。</span><span class="sxs-lookup"><span data-stu-id="9a48b-196">The **Forgot your password?** link is used to reset a forgotten password.</span></span>

![Azure AD B2C 登录](./azure-ad-b2c/_static/b2csts.png)

<span data-ttu-id="9a48b-198">已成功登录后，浏览器将重定向到 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9a48b-198">After successfully signing in, the browser redirects to the web app.</span></span>

![成功](./azure-ad-b2c/_static/success.png)

## <a name="next-steps"></a><span data-ttu-id="9a48b-200">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9a48b-200">Next steps</span></span>

<span data-ttu-id="9a48b-201">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="9a48b-201">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9a48b-202">创建 Azure Active Directory B2C 租户</span><span class="sxs-lookup"><span data-stu-id="9a48b-202">Create an Azure Active Directory B2C tenant</span></span>
> * <span data-ttu-id="9a48b-203">在 Azure AD B2C 注册某个应用程序</span><span class="sxs-lookup"><span data-stu-id="9a48b-203">Register an app in Azure AD B2C</span></span>
> * <span data-ttu-id="9a48b-204">使用 Visual Studio 创建 ASP.NET Core Web 应用程序配置为使用 Azure AD B2C 租户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="9a48b-204">Use Visual Studio to create an ASP.NET Core Web Application configured to use the Azure AD B2C tenant for authentication</span></span>
> * <span data-ttu-id="9a48b-205">配置控制 Azure AD B2C 租户的行为的策略</span><span class="sxs-lookup"><span data-stu-id="9a48b-205">Configure policies controlling the behavior of the Azure AD B2C tenant</span></span>

<span data-ttu-id="9a48b-206">现在，ASP.NET Core 应用程序配置为使用 Azure AD B2C 进行身份验证， [Authorize 属性](xref:security/authorization/simple)可用来保护你的应用。</span><span class="sxs-lookup"><span data-stu-id="9a48b-206">Now that the ASP.NET Core app is configured to use Azure AD B2C for authentication, the [Authorize attribute](xref:security/authorization/simple) can be used to secure your app.</span></span> <span data-ttu-id="9a48b-207">在继续开发你的应用到学习：</span><span class="sxs-lookup"><span data-stu-id="9a48b-207">Continue developing your app by learning to:</span></span>

* <span data-ttu-id="9a48b-208">[自定义 Azure AD B2C 用户界面](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization)。</span><span class="sxs-lookup"><span data-stu-id="9a48b-208">[Customize the Azure AD B2C user interface](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization).</span></span>
* <span data-ttu-id="9a48b-209">[配置密码复杂性要求](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity)。</span><span class="sxs-lookup"><span data-stu-id="9a48b-209">[Configure password complexity requirements](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity).</span></span>
* <span data-ttu-id="9a48b-210">[启用多因素身份验证](/azure/active-directory-b2c/active-directory-b2c-reference-mfa)。</span><span class="sxs-lookup"><span data-stu-id="9a48b-210">[Enable multi-factor authentication](/azure/active-directory-b2c/active-directory-b2c-reference-mfa).</span></span>
* <span data-ttu-id="9a48b-211">配置其他标识提供程序，例如[Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app)， [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app)， [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app)， [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app)， [Twitter](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app)，和其他人。</span><span class="sxs-lookup"><span data-stu-id="9a48b-211">Configure additional identity providers, such as [Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app), [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app), [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app), [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app), [Twitter](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app), and others.</span></span>
* <span data-ttu-id="9a48b-212">[使用 Azure AD Graph API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet)从 Azure AD B2C 租户中检索其他用户信息，例如组成员身份。</span><span class="sxs-lookup"><span data-stu-id="9a48b-212">[Use the Azure AD Graph API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet) to retrieve additional user information, such as group membership, from the Azure AD B2C tenant.</span></span>
* <span data-ttu-id="9a48b-213">[保护 web API 使用 Azure AD B2C 的 ASP.NET Core](xref:security/authentication/azure-ad-b2c-webapi)。</span><span class="sxs-lookup"><span data-stu-id="9a48b-213">[Secure an ASP.NET Core web API using Azure AD B2C](xref:security/authentication/azure-ad-b2c-webapi).</span></span>
* <span data-ttu-id="9a48b-214">[从使用 Azure AD B2C 的.NET web 应用程序调用.NET web API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="9a48b-214">[Call a .NET web API from a .NET web app using Azure AD B2C](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet).</span></span>
