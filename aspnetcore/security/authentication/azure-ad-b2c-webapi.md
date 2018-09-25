---
title: 中的 web Api 与 Azure Active Directory B2C 中 ASP.NET Core 云身份验证
author: camsoper
description: 了解如何设置与 ASP.NET Core Web API 的 Azure Active Directory B2C 身份验证。 经过身份验证的 web API 使用 Postman 进行测试。
ms.author: casoper
ms.date: 09/21/2018
ms.custom: mvc
uid: security/authentication/azure-ad-b2c-webapi
ms.openlocfilehash: 0efc95f508ef84d2728f503f1edd886ce6ae7a79
ms.sourcegitcommit: 4d5f8680d68b39c411b46c73f7014f8aa0f12026
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "47028253"
---
# <a name="cloud-authentication-in-web-apis-with-azure-active-directory-b2c-in-aspnet-core"></a><span data-ttu-id="2c094-104">中的 web Api 与 Azure Active Directory B2C 中 ASP.NET Core 云身份验证</span><span class="sxs-lookup"><span data-stu-id="2c094-104">Cloud authentication in web APIs with Azure Active Directory B2C in ASP.NET Core</span></span>

<span data-ttu-id="2c094-105">作者：[Cam Soper](https://twitter.com/camsoper)</span><span class="sxs-lookup"><span data-stu-id="2c094-105">By [Cam Soper](https://twitter.com/camsoper)</span></span>

<span data-ttu-id="2c094-106">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C) 是云标识管理解决方案，适用于 web 和移动应用。</span><span class="sxs-lookup"><span data-stu-id="2c094-106">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C) is a cloud identity management solution for web and mobile apps.</span></span> <span data-ttu-id="2c094-107">该服务提供用于在云中和本地托管的应用的身份验证。</span><span class="sxs-lookup"><span data-stu-id="2c094-107">The service provides authentication for apps hosted in the cloud and on-premises.</span></span> <span data-ttu-id="2c094-108">身份验证类型包括个人帐户，社交网络帐户和联合企业帐户。</span><span class="sxs-lookup"><span data-stu-id="2c094-108">Authentication types include individual accounts, social network accounts, and federated enterprise accounts.</span></span> <span data-ttu-id="2c094-109">此外，Azure AD B2C 可以提供最小配置多重身份验证。</span><span class="sxs-lookup"><span data-stu-id="2c094-109">Additionally, Azure AD B2C can provide multi-factor authentication with minimal configuration.</span></span>

> [!TIP]
> <span data-ttu-id="2c094-110">Azure Active Directory (Azure AD) 和 Azure AD B2C 是单独的产品产品/服务。</span><span class="sxs-lookup"><span data-stu-id="2c094-110">Azure Active Directory (Azure AD) and Azure AD B2C are separate product offerings.</span></span> <span data-ttu-id="2c094-111">Azure AD 租户表示组织，而 Azure AD B2C 租户表示与信赖方应用程序将使用的集合。</span><span class="sxs-lookup"><span data-stu-id="2c094-111">An Azure AD tenant represents an organization, while an Azure AD B2C tenant represents a collection of identities to be used with relying party applications.</span></span> <span data-ttu-id="2c094-112">若要了解详细信息，请参阅[Azure AD B2C： 常见问题 (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs)。</span><span class="sxs-lookup"><span data-stu-id="2c094-112">To learn more, see [Azure AD B2C: Frequently asked questions (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs).</span></span>

<span data-ttu-id="2c094-113">由于 web Api 有没有用户界面，因此它们无法将用户重定向到安全令牌服务等 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="2c094-113">Since web APIs have no user interface, they're unable to redirect the user to a secure token service like Azure AD B2C.</span></span> <span data-ttu-id="2c094-114">相反，API 是具有已验证了用户与 Azure AD B2C 将调用应用程序中传递的持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="2c094-114">Instead, the API is passed a bearer token from the calling app, which has already authenticated the user with Azure AD B2C.</span></span> <span data-ttu-id="2c094-115">API 会验证该令牌而无需直接用户交互。</span><span class="sxs-lookup"><span data-stu-id="2c094-115">The API then validates the token without direct user interaction.</span></span>

<span data-ttu-id="2c094-116">在本教程中，学习如何：</span><span class="sxs-lookup"><span data-stu-id="2c094-116">In this tutorial, learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2c094-117">创建 Azure Active Directory B2C 租户。</span><span class="sxs-lookup"><span data-stu-id="2c094-117">Create an Azure Active Directory B2C tenant.</span></span>
> * <span data-ttu-id="2c094-118">在 Azure AD B2C 中注册 Web API。</span><span class="sxs-lookup"><span data-stu-id="2c094-118">Register a Web API in Azure AD B2C.</span></span>
> * <span data-ttu-id="2c094-119">使用 Visual Studio 来创建 Web API 配置为使用 Azure AD B2C 租户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="2c094-119">Use Visual Studio to create a Web API configured to use the Azure AD B2C tenant for authentication.</span></span>
> * <span data-ttu-id="2c094-120">配置控制的 Azure AD B2C 租户行为的策略。</span><span class="sxs-lookup"><span data-stu-id="2c094-120">Configure policies controlling the behavior of the Azure AD B2C tenant.</span></span>
> * <span data-ttu-id="2c094-121">使用 Postman 来模拟一个 web 应用，用于显示登录对话框中，检索令牌，并使用它来对 web API 发出请求。</span><span class="sxs-lookup"><span data-stu-id="2c094-121">Use Postman to simulate a web app which presents a login dialog, retrieves a token, and uses it to make a request against the web API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c094-122">系统必备</span><span class="sxs-lookup"><span data-stu-id="2c094-122">Prerequisites</span></span>

<span data-ttu-id="2c094-123">本演练需要以下项：</span><span class="sxs-lookup"><span data-stu-id="2c094-123">The following are required for this walkthrough:</span></span>

* [<span data-ttu-id="2c094-124">Microsoft Azure 订阅</span><span class="sxs-lookup"><span data-stu-id="2c094-124">Microsoft Azure subscription</span></span>](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)
* <span data-ttu-id="2c094-125">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) （任何版本）</span><span class="sxs-lookup"><span data-stu-id="2c094-125">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) (any edition)</span></span>
* [<span data-ttu-id="2c094-126">Postman</span><span class="sxs-lookup"><span data-stu-id="2c094-126">Postman</span></span>](https://www.getpostman.com/postman)

## <a name="create-the-azure-active-directory-b2c-tenant"></a><span data-ttu-id="2c094-127">创建 Azure Active Directory B2C 租户</span><span class="sxs-lookup"><span data-stu-id="2c094-127">Create the Azure Active Directory B2C tenant</span></span>

<span data-ttu-id="2c094-128">创建一个 Azure AD B2C 租户[文档中所述](/azure/active-directory-b2c/active-directory-b2c-get-started)。</span><span class="sxs-lookup"><span data-stu-id="2c094-128">Create an Azure AD B2C tenant [as described in the documentation](/azure/active-directory-b2c/active-directory-b2c-get-started).</span></span> <span data-ttu-id="2c094-129">出现提示时，将租户与 Azure 订阅相关联是可选的用于本教程。</span><span class="sxs-lookup"><span data-stu-id="2c094-129">When prompted, associating the tenant with an Azure subscription is optional for this tutorial.</span></span>

## <a name="configure-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="2c094-130">配置注册或登录策略</span><span class="sxs-lookup"><span data-stu-id="2c094-130">Configure a sign-up or sign-in policy</span></span>

<span data-ttu-id="2c094-131">使用到的 Azure AD B2C 文档中的步骤[创建注册或登录策略](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy)。</span><span class="sxs-lookup"><span data-stu-id="2c094-131">Use the steps in the Azure AD B2C documentation to [create a sign-up or sign-in policy](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy).</span></span> <span data-ttu-id="2c094-132">将策略命名**SiUpIn**。</span><span class="sxs-lookup"><span data-stu-id="2c094-132">Name the policy **SiUpIn**.</span></span>  <span data-ttu-id="2c094-133">使用提供的文档中的示例值**标识提供者**，**注册属性**，并**应用程序声明**。</span><span class="sxs-lookup"><span data-stu-id="2c094-133">Use the example values provided in the documentation for **Identity providers**, **Sign-up attributes**, and **Application claims**.</span></span> <span data-ttu-id="2c094-134">使用**立即运行**是可选的按钮以测试策略，如文档中所述。</span><span class="sxs-lookup"><span data-stu-id="2c094-134">Using the **Run now** button to test the policy as described in the documentation is optional.</span></span>

## <a name="register-the-api-in-azure-ad-b2c"></a><span data-ttu-id="2c094-135">在 Azure AD B2C 中注册 API</span><span class="sxs-lookup"><span data-stu-id="2c094-135">Register the API in Azure AD B2C</span></span>

<span data-ttu-id="2c094-136">在新创建的 Azure AD B2C 租户中注册 API 通过[文档中的步骤](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-api)下**注册 web API**部分。</span><span class="sxs-lookup"><span data-stu-id="2c094-136">In the newly created Azure AD B2C tenant, register your API using [the steps in the documentation](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-api) under the **Register a web API** section.</span></span>

<span data-ttu-id="2c094-137">使用以下值：</span><span class="sxs-lookup"><span data-stu-id="2c094-137">Use the following values:</span></span>

| <span data-ttu-id="2c094-138">设置</span><span class="sxs-lookup"><span data-stu-id="2c094-138">Setting</span></span>                       | <span data-ttu-id="2c094-139">“值”</span><span class="sxs-lookup"><span data-stu-id="2c094-139">Value</span></span>               | <span data-ttu-id="2c094-140">说明</span><span class="sxs-lookup"><span data-stu-id="2c094-140">Notes</span></span>                                                                                  |
|-------------------------------|---------------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="2c094-141">**名称**</span><span class="sxs-lookup"><span data-stu-id="2c094-141">**Name**</span></span>                      | <span data-ttu-id="2c094-142">*&lt;API 名称&gt;*</span><span class="sxs-lookup"><span data-stu-id="2c094-142">*&lt;API name&gt;*</span></span>  | <span data-ttu-id="2c094-143">输入**名称**描述你的应用向使用者的应用。</span><span class="sxs-lookup"><span data-stu-id="2c094-143">Enter a **Name** for the app that describes your app to consumers.</span></span>                     |
| <span data-ttu-id="2c094-144">**包括 web 应用 /web API**</span><span class="sxs-lookup"><span data-stu-id="2c094-144">**Include web app / web API**</span></span> | <span data-ttu-id="2c094-145">是</span><span class="sxs-lookup"><span data-stu-id="2c094-145">Yes</span></span>                 |                                                                                        |
| <span data-ttu-id="2c094-146">**允许隐式流**</span><span class="sxs-lookup"><span data-stu-id="2c094-146">**Allow implicit flow**</span></span>       | <span data-ttu-id="2c094-147">是</span><span class="sxs-lookup"><span data-stu-id="2c094-147">Yes</span></span>                 |                                                                                        |
| <span data-ttu-id="2c094-148">**回复 URL**</span><span class="sxs-lookup"><span data-stu-id="2c094-148">**Reply URL**</span></span>                 | `https://localhost` | <span data-ttu-id="2c094-149">回复 Url 属于终结点，Azure AD B2C 在其中返回应用请求的任何令牌。</span><span class="sxs-lookup"><span data-stu-id="2c094-149">Reply URLs are endpoints where Azure AD B2C returns any tokens that your app requests.</span></span> |
| <span data-ttu-id="2c094-150">**应用程序 ID URI**</span><span class="sxs-lookup"><span data-stu-id="2c094-150">**App ID URI**</span></span>                | <span data-ttu-id="2c094-151">*api*</span><span class="sxs-lookup"><span data-stu-id="2c094-151">*api*</span></span>               | <span data-ttu-id="2c094-152">该 URI 不需要解析为物理地址。</span><span class="sxs-lookup"><span data-stu-id="2c094-152">The URI doesn't need to resolve to a physical address.</span></span> <span data-ttu-id="2c094-153">它只需是唯一的。</span><span class="sxs-lookup"><span data-stu-id="2c094-153">It only needs to be unique.</span></span>     |
| <span data-ttu-id="2c094-154">**包含本机客户端**</span><span class="sxs-lookup"><span data-stu-id="2c094-154">**Include native client**</span></span>     | <span data-ttu-id="2c094-155">否</span><span class="sxs-lookup"><span data-stu-id="2c094-155">No</span></span>                  |                                                                                        |

<span data-ttu-id="2c094-156">注册 API 后，将显示在租户中的应用和 Api 的列表。</span><span class="sxs-lookup"><span data-stu-id="2c094-156">After the API is registered, the list of apps and APIs in the tenant is displayed.</span></span> <span data-ttu-id="2c094-157">选择刚注册的 API。</span><span class="sxs-lookup"><span data-stu-id="2c094-157">Select the API that was just registered.</span></span> <span data-ttu-id="2c094-158">选择**副本**右侧的图标**应用程序 ID**字段以将其复制到剪贴板。</span><span class="sxs-lookup"><span data-stu-id="2c094-158">Select the **Copy** icon to the right of the **Application ID** field to copy it to the clipboard.</span></span> <span data-ttu-id="2c094-159">选择**发布的作用域**，并验证默认*user_impersonation*作用域是存在。</span><span class="sxs-lookup"><span data-stu-id="2c094-159">Select **Published scopes** and verify the default *user_impersonation* scope is present.</span></span>

## <a name="create-an-aspnet-core-app-in-visual-studio-2017"></a><span data-ttu-id="2c094-160">在 Visual Studio 2017 年 1 中创建 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="2c094-160">Create an ASP.NET Core app in Visual Studio 2017</span></span>

<span data-ttu-id="2c094-161">Visual Studio Web 应用程序模板可以配置为使用 Azure AD B2C 租户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="2c094-161">The Visual Studio Web Application template can be configured to use the Azure AD B2C tenant for authentication.</span></span>

<span data-ttu-id="2c094-162">在 Visual Studio 中：</span><span class="sxs-lookup"><span data-stu-id="2c094-162">In Visual Studio:</span></span>

1. <span data-ttu-id="2c094-163">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2c094-163">Create a new ASP.NET Core Web Application.</span></span> 
2. <span data-ttu-id="2c094-164">选择**Web API**从模板列表。</span><span class="sxs-lookup"><span data-stu-id="2c094-164">Select **Web API** from the list of templates.</span></span>
3. <span data-ttu-id="2c094-165">选择**更改身份验证**按钮。</span><span class="sxs-lookup"><span data-stu-id="2c094-165">Select the **Change Authentication** button.</span></span>

    ![更改身份验证按钮](./azure-ad-b2c-webapi/change-auth-button.png)

4. <span data-ttu-id="2c094-167">在中**更改身份验证**对话框中，选择**单个用户帐户**，然后选择**连接到现有用户存储在云中**下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="2c094-167">In the **Change Authentication** dialog, select **Individual User Accounts**, and then select **Connect to an existing user store in the cloud** in the dropdown.</span></span> 

    ![更改身份验证对话框](./azure-ad-b2c-webapi/change-auth-dialog.png)

5. <span data-ttu-id="2c094-169">完成窗体具有以下值：</span><span class="sxs-lookup"><span data-stu-id="2c094-169">Complete the form with the following values:</span></span>

    | <span data-ttu-id="2c094-170">设置</span><span class="sxs-lookup"><span data-stu-id="2c094-170">Setting</span></span>                       | <span data-ttu-id="2c094-171">“值”</span><span class="sxs-lookup"><span data-stu-id="2c094-171">Value</span></span>                                                 |
    |-------------------------------|-------------------------------------------------------|
    | <span data-ttu-id="2c094-172">**域名**</span><span class="sxs-lookup"><span data-stu-id="2c094-172">**Domain Name**</span></span>               | <span data-ttu-id="2c094-173">*&lt;在 B2C 租户的域名&gt;*</span><span class="sxs-lookup"><span data-stu-id="2c094-173">*&lt;the domain name of your B2C tenant&gt;*</span></span>          |
    | <span data-ttu-id="2c094-174">**应用程序 ID**</span><span class="sxs-lookup"><span data-stu-id="2c094-174">**Application ID**</span></span>            | <span data-ttu-id="2c094-175">*&lt;粘贴剪贴板中的应用程序 ID&gt;*</span><span class="sxs-lookup"><span data-stu-id="2c094-175">*&lt;paste the Application ID from the clipboard&gt;*</span></span> |
    | <span data-ttu-id="2c094-176">**注册或登录策略**</span><span class="sxs-lookup"><span data-stu-id="2c094-176">**Sign-up or sign-in policy**</span></span> | `B2C_1_SiUpIn`                                        |

    <span data-ttu-id="2c094-177">选择**确定**以关闭**更改身份验证**对话框。</span><span class="sxs-lookup"><span data-stu-id="2c094-177">Select **OK** to close the **Change Authentication** dialog.</span></span> <span data-ttu-id="2c094-178">选择**确定**创建 web 应用。</span><span class="sxs-lookup"><span data-stu-id="2c094-178">Select **OK** to create the web app.</span></span>

<span data-ttu-id="2c094-179">Visual Studio 创建 web API 的具有控制器名为*ValuesController.cs*返回硬编码值的 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="2c094-179">Visual Studio creates the web API with a controller named *ValuesController.cs* that returns hard-coded values for GET requests.</span></span> <span data-ttu-id="2c094-180">类用修饰[Authorize 属性](xref:security/authorization/simple)，因此所有请求都需要身份验证。</span><span class="sxs-lookup"><span data-stu-id="2c094-180">The class is decorated with the [Authorize attribute](xref:security/authorization/simple), so all requests require authentication.</span></span>

## <a name="run-the-web-api"></a><span data-ttu-id="2c094-181">运行 web API</span><span class="sxs-lookup"><span data-stu-id="2c094-181">Run the web API</span></span>

<span data-ttu-id="2c094-182">在 Visual Studio 中，运行 API。</span><span class="sxs-lookup"><span data-stu-id="2c094-182">In Visual Studio, run the API.</span></span> <span data-ttu-id="2c094-183">Visual Studio 启动浏览器指向 API 的根 URL。</span><span class="sxs-lookup"><span data-stu-id="2c094-183">Visual Studio launches a browser pointed at the API's root URL.</span></span> <span data-ttu-id="2c094-184">请注意地址栏中的 URL 并将在后台运行的 API。</span><span class="sxs-lookup"><span data-stu-id="2c094-184">Note the URL in the address bar, and leave the API running in the background.</span></span>

> [!NOTE]
> <span data-ttu-id="2c094-185">由于没有为根 URL 定义没有控制器，浏览器可能显示 404 （找不到页） 错误。</span><span class="sxs-lookup"><span data-stu-id="2c094-185">Since there is no controller defined for the root URL, the browser may display a 404 (page not found) error.</span></span> <span data-ttu-id="2c094-186">这是预期行为。</span><span class="sxs-lookup"><span data-stu-id="2c094-186">This is expected behavior.</span></span>

## <a name="use-postman-to-get-a-token-and-test-the-api"></a><span data-ttu-id="2c094-187">使用 Postman 来获取令牌，并测试 API</span><span class="sxs-lookup"><span data-stu-id="2c094-187">Use Postman to get a token and test the API</span></span>

<span data-ttu-id="2c094-188">[Postman](https://getpostman.com/postman)是工具用于测试 web Api。</span><span class="sxs-lookup"><span data-stu-id="2c094-188">[Postman](https://getpostman.com/postman) is a tool for testing web APIs.</span></span> <span data-ttu-id="2c094-189">对于本教程，Postman 模拟访问 web API 代表该用户的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2c094-189">For this tutorial, Postman simulates a web app that accesses the web API on the user's behalf.</span></span>

### <a name="register-postman-as-a-web-app"></a><span data-ttu-id="2c094-190">注册为 web 应用的 Postman</span><span class="sxs-lookup"><span data-stu-id="2c094-190">Register Postman as a web app</span></span>

<span data-ttu-id="2c094-191">Postman 模拟可以从 Azure AD B2C 租户获取令牌的 web 应用，因为它必须注册在租户中为 web 应用。</span><span class="sxs-lookup"><span data-stu-id="2c094-191">Since Postman simulates a web app that can obtain tokens from the Azure AD B2C tenant, it must be registered in the tenant as a web app.</span></span> <span data-ttu-id="2c094-192">注册使用 Postman[文档中的步骤](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app)下**注册 web 应用**部分。</span><span class="sxs-lookup"><span data-stu-id="2c094-192">Register Postman using [the steps in the documentation](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app) under the **Register a web app** section.</span></span> <span data-ttu-id="2c094-193">在停止**创建 web 应用客户端机密**部分。</span><span class="sxs-lookup"><span data-stu-id="2c094-193">Stop at the **Create a web app client secret** section.</span></span> <span data-ttu-id="2c094-194">本教程不需要客户端机密。</span><span class="sxs-lookup"><span data-stu-id="2c094-194">A client secret isn't required for this tutorial.</span></span> 

<span data-ttu-id="2c094-195">使用以下值：</span><span class="sxs-lookup"><span data-stu-id="2c094-195">Use the following values:</span></span>

| <span data-ttu-id="2c094-196">设置</span><span class="sxs-lookup"><span data-stu-id="2c094-196">Setting</span></span>                       | <span data-ttu-id="2c094-197">“值”</span><span class="sxs-lookup"><span data-stu-id="2c094-197">Value</span></span>                            | <span data-ttu-id="2c094-198">说明</span><span class="sxs-lookup"><span data-stu-id="2c094-198">Notes</span></span>                           |
|-------------------------------|----------------------------------|---------------------------------|
| <span data-ttu-id="2c094-199">**名称**</span><span class="sxs-lookup"><span data-stu-id="2c094-199">**Name**</span></span>                      | <span data-ttu-id="2c094-200">Postman</span><span class="sxs-lookup"><span data-stu-id="2c094-200">Postman</span></span>                          |                                 |
| <span data-ttu-id="2c094-201">**包括 web 应用 /web API**</span><span class="sxs-lookup"><span data-stu-id="2c094-201">**Include web app / web API**</span></span> | <span data-ttu-id="2c094-202">是</span><span class="sxs-lookup"><span data-stu-id="2c094-202">Yes</span></span>                              |                                 |
| <span data-ttu-id="2c094-203">**允许隐式流**</span><span class="sxs-lookup"><span data-stu-id="2c094-203">**Allow implicit flow**</span></span>       | <span data-ttu-id="2c094-204">是</span><span class="sxs-lookup"><span data-stu-id="2c094-204">Yes</span></span>                              |                                 |
| <span data-ttu-id="2c094-205">**回复 URL**</span><span class="sxs-lookup"><span data-stu-id="2c094-205">**Reply URL**</span></span>                 | `https://getpostman.com/postman` |                                 |
| <span data-ttu-id="2c094-206">**应用程序 ID URI**</span><span class="sxs-lookup"><span data-stu-id="2c094-206">**App ID URI**</span></span>                | <span data-ttu-id="2c094-207">*&lt;将保留为空&gt;*</span><span class="sxs-lookup"><span data-stu-id="2c094-207">*&lt;leave blank&gt;*</span></span>            | <span data-ttu-id="2c094-208">对于本教程不被必需。</span><span class="sxs-lookup"><span data-stu-id="2c094-208">Not required for this tutorial.</span></span> |
| <span data-ttu-id="2c094-209">**包含本机客户端**</span><span class="sxs-lookup"><span data-stu-id="2c094-209">**Include native client**</span></span>     | <span data-ttu-id="2c094-210">否</span><span class="sxs-lookup"><span data-stu-id="2c094-210">No</span></span>                               |                                 |

<span data-ttu-id="2c094-211">新注册的 web 应用需要访问 web API 代表该用户的权限。</span><span class="sxs-lookup"><span data-stu-id="2c094-211">The newly registered web app needs permission to access the web API on the user's behalf.</span></span>  

1. <span data-ttu-id="2c094-212">选择**Postman**的应用程序，然后选择列表中**API 访问**在左侧菜单中。</span><span class="sxs-lookup"><span data-stu-id="2c094-212">Select **Postman** in the list of apps and then select **API access** from the menu on the left.</span></span>
2. <span data-ttu-id="2c094-213">选择 **+ 添加**。</span><span class="sxs-lookup"><span data-stu-id="2c094-213">Select **+ Add**.</span></span>
3. <span data-ttu-id="2c094-214">在中**选择 API**下拉列表中，选择 web API 的名称。</span><span class="sxs-lookup"><span data-stu-id="2c094-214">In the **Select API** dropdown, select the name of the web API.</span></span>
4. <span data-ttu-id="2c094-215">在中**选择作用域**下拉列表中，确保选中所有作用域。</span><span class="sxs-lookup"><span data-stu-id="2c094-215">In the **Select Scopes** dropdown, ensure all scopes are selected.</span></span>
5. <span data-ttu-id="2c094-216">选择**确定**。</span><span class="sxs-lookup"><span data-stu-id="2c094-216">Select **Ok**.</span></span>

<span data-ttu-id="2c094-217">请注意 Postman 应用的应用程序 ID，因为它所需获取持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="2c094-217">Note the Postman app's Application ID, as it's required to obtain a bearer token.</span></span>

### <a name="create-a-postman-request"></a><span data-ttu-id="2c094-218">创建 Postman 请求</span><span class="sxs-lookup"><span data-stu-id="2c094-218">Create a Postman request</span></span>

<span data-ttu-id="2c094-219">启动 Postman。</span><span class="sxs-lookup"><span data-stu-id="2c094-219">Launch Postman.</span></span> <span data-ttu-id="2c094-220">默认情况下，显示 Postman**创建新**对话框后启动。</span><span class="sxs-lookup"><span data-stu-id="2c094-220">By default, Postman displays the **Create New** dialog upon launching.</span></span> <span data-ttu-id="2c094-221">如果未显示对话框中，选择 **+ 新建**在左上角的按钮。</span><span class="sxs-lookup"><span data-stu-id="2c094-221">If the dialog isn't displayed, select the **+ New** button in the upper left.</span></span>

<span data-ttu-id="2c094-222">从**创建新**对话框：</span><span class="sxs-lookup"><span data-stu-id="2c094-222">From the **Create New** dialog:</span></span>

1. <span data-ttu-id="2c094-223">选择**请求**。</span><span class="sxs-lookup"><span data-stu-id="2c094-223">Select **Request**.</span></span>

    ![请求按钮](./azure-ad-b2c-webapi/postman-create-new.png)

2. <span data-ttu-id="2c094-225">输入*获取值*中**请求名称**框。</span><span class="sxs-lookup"><span data-stu-id="2c094-225">Enter *Get Values* in the **Request name** box.</span></span>
3. <span data-ttu-id="2c094-226">选择 **+ 创建集合**若要创建用于存储请求新的集合。</span><span class="sxs-lookup"><span data-stu-id="2c094-226">Select **+ Create Collection** to create a new collection for storing the request.</span></span> <span data-ttu-id="2c094-227">命名集合*ASP.NET Core 教程*，然后选择复选标记。</span><span class="sxs-lookup"><span data-stu-id="2c094-227">Name the collection *ASP.NET Core tutorials* and then select the checkmark.</span></span>

    ![创建新的集合](./azure-ad-b2c-webapi/postman-create-collection.png)

4. <span data-ttu-id="2c094-229">选择**将保存到 ASP.NET Core 教程**按钮。</span><span class="sxs-lookup"><span data-stu-id="2c094-229">Select the **Save to ASP.NET Core tutorials** button.</span></span>

### <a name="test-the-web-api-without-authentication"></a><span data-ttu-id="2c094-230">测试 web API 而无需身份验证</span><span class="sxs-lookup"><span data-stu-id="2c094-230">Test the web API without authentication</span></span>

<span data-ttu-id="2c094-231">若要验证 web API 需要身份验证，首先请不带身份验证的请求。</span><span class="sxs-lookup"><span data-stu-id="2c094-231">To verify that the web API requires authentication, first make a request without authentication.</span></span>

1. <span data-ttu-id="2c094-232">在中**输入请求 URL**框中，输入的 URL `ValuesController`。</span><span class="sxs-lookup"><span data-stu-id="2c094-232">In the **Enter request URL** box, enter the URL for `ValuesController`.</span></span> <span data-ttu-id="2c094-233">URL 是使用浏览器中显示的相同**api/values**追加。</span><span class="sxs-lookup"><span data-stu-id="2c094-233">The URL is the same as displayed in the browser with **api/values** appended.</span></span> <span data-ttu-id="2c094-234">一个示例是`https://localhost:44375/api/values`。</span><span class="sxs-lookup"><span data-stu-id="2c094-234">An example would be `https://localhost:44375/api/values`.</span></span>
2. <span data-ttu-id="2c094-235">选择**发送**按钮。</span><span class="sxs-lookup"><span data-stu-id="2c094-235">Select the **Send** button.</span></span>
3. <span data-ttu-id="2c094-236">请注意响应的状态是*401 未授权*。</span><span class="sxs-lookup"><span data-stu-id="2c094-236">Note the status of the response is *401 Unauthorized*.</span></span>

    ![401 未授权的响应](./azure-ad-b2c-webapi/postman-401-status.png)

> [!IMPORTANT]
> <span data-ttu-id="2c094-238">如果收到"无法获取任何响应"错误，可能需要禁用中的 SSL 证书验证[Postman 设置](https://learning.getpostman.com/docs/postman/launching_postman/settings)。</span><span class="sxs-lookup"><span data-stu-id="2c094-238">If you get a "Could not get any response" error, you may need to disable SSL certificate verification in the [Postman settings](https://learning.getpostman.com/docs/postman/launching_postman/settings).</span></span> 
 
### <a name="obtain-a-bearer-token"></a><span data-ttu-id="2c094-239">获取持有者令牌</span><span class="sxs-lookup"><span data-stu-id="2c094-239">Obtain a bearer token</span></span>

<span data-ttu-id="2c094-240">若要向 web API 发出的经过身份验证的请求，持有者令牌是必需的。</span><span class="sxs-lookup"><span data-stu-id="2c094-240">To make an authenticated request to the web API, a bearer token is required.</span></span> <span data-ttu-id="2c094-241">Postman 可轻松地登录到 Azure AD B2C 租户并获取的令牌。</span><span class="sxs-lookup"><span data-stu-id="2c094-241">Postman makes it easy to sign in to the Azure AD B2C tenant and obtain a token.</span></span>

1. <span data-ttu-id="2c094-242">上**授权**选项卡上，在**类型**下拉列表中，选择**OAuth 2.0**。</span><span class="sxs-lookup"><span data-stu-id="2c094-242">On the **Authorization** tab, in the **TYPE** dropdown, select **OAuth 2.0**.</span></span> <span data-ttu-id="2c094-243">在中**授权将数据添加到**下拉列表中，选择**请求标头**。</span><span class="sxs-lookup"><span data-stu-id="2c094-243">In the **Add authorization data to** dropdown, select **Request Headers**.</span></span> <span data-ttu-id="2c094-244">选择**获取新访问令牌**。</span><span class="sxs-lookup"><span data-stu-id="2c094-244">Select **Get New Access Token**.</span></span>

    ![使用设置的授权选项卡](./azure-ad-b2c-webapi/postman-auth-tab.png)

2. <span data-ttu-id="2c094-246">完成**获取新访问令牌**，如下所示的对话框：</span><span class="sxs-lookup"><span data-stu-id="2c094-246">Complete the **GET NEW ACCESS TOKEN** dialog as follows:</span></span>


   |                <span data-ttu-id="2c094-247">设置</span><span class="sxs-lookup"><span data-stu-id="2c094-247">Setting</span></span>                 |                                             <span data-ttu-id="2c094-248">“值”</span><span class="sxs-lookup"><span data-stu-id="2c094-248">Value</span></span>                                             |                                                                                                                                    <span data-ttu-id="2c094-249">说明</span><span class="sxs-lookup"><span data-stu-id="2c094-249">Notes</span></span>                                                                                                                                     |
   |----------------------------------------|-----------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |      <span data-ttu-id="2c094-250"><strong>令牌名称</strong></span><span class="sxs-lookup"><span data-stu-id="2c094-250"><strong>Token Name</strong></span></span>       |                                  <span data-ttu-id="2c094-251"><em>&lt;令牌名称&gt;</em></span><span class="sxs-lookup"><span data-stu-id="2c094-251"><em>&lt;token name&gt;</em></span></span>                                  |                                                                                                                   <span data-ttu-id="2c094-252">输入令牌的描述性名称。</span><span class="sxs-lookup"><span data-stu-id="2c094-252">Enter a descriptive name for the token.</span></span>                                                                                                                    |
   |      <span data-ttu-id="2c094-253"><strong>授权类型</strong></span><span class="sxs-lookup"><span data-stu-id="2c094-253"><strong>Grant Type</strong></span></span>       |                                           <span data-ttu-id="2c094-254">隐式</span><span class="sxs-lookup"><span data-stu-id="2c094-254">Implicit</span></span>                                            |                                                                                                                                                                                                                                                                              |
   |     <span data-ttu-id="2c094-255"><strong>回调 URL</strong></span><span class="sxs-lookup"><span data-stu-id="2c094-255"><strong>Callback URL</strong></span></span>      |                               `https://getpostman.com/postman`                                |                                                                                                                                                                                                                                                                              |
   |       <span data-ttu-id="2c094-256"><strong>身份验证 URL</strong></span><span class="sxs-lookup"><span data-stu-id="2c094-256"><strong>Auth URL</strong></span></span>        | `https://login.microsoftonline.com/tfp/<tenant domain name>/B2C_1_SiUpIn/oauth2/v2.0/authorize` |                                                                                                  <span data-ttu-id="2c094-257">替换<em>&lt;租户域名&gt;</em>与租户的域名。</span><span class="sxs-lookup"><span data-stu-id="2c094-257">Replace <em>&lt;tenant domain name&gt;</em> with the tenant's domain name.</span></span>                                                                                                  |
   |       <span data-ttu-id="2c094-258"><strong>客户端 ID</strong></span><span class="sxs-lookup"><span data-stu-id="2c094-258"><strong>Client ID</strong></span></span>       |                <span data-ttu-id="2c094-259"><em>&lt;输入 Postman 应用<b>应用程序 ID</b>&gt;</em></span><span class="sxs-lookup"><span data-stu-id="2c094-259"><em>&lt;enter the Postman app's <b>Application ID</b>&gt;</em></span></span>                 |                                                                                                                                                                                                                                                                              |
   |         <span data-ttu-id="2c094-260"><strong>范围</strong></span><span class="sxs-lookup"><span data-stu-id="2c094-260"><strong>Scope</strong></span></span>         |         `https://<tenant domain name>/<api>/user_impersonation openid offline_access`         | <span data-ttu-id="2c094-261">替换<em>&lt;租户域名&gt;</em>与租户的域名。</span><span class="sxs-lookup"><span data-stu-id="2c094-261">Replace <em>&lt;tenant domain name&gt;</em> with the tenant's domain name.</span></span> <span data-ttu-id="2c094-262">替换<em>&lt;api&gt;</em>替换应用程序 ID URI 在 web API 时提供首次注册 (在这种情况下， `api`)。</span><span class="sxs-lookup"><span data-stu-id="2c094-262">Replace <em>&lt;api&gt;</em> with the App ID URI you gave the web API when you first registered it (in this case, `api`).</span></span> <span data-ttu-id="2c094-263">Url 模式是： <em>https://{tenant}.onmicrosoft.com/{api-id-uri}/{scope 名称}</em>。</span><span class="sxs-lookup"><span data-stu-id="2c094-263">The pattern for the URL is: <em>https://{tenant}.onmicrosoft.com/{api-id-uri}/{scope name}</em>.</span></span> |
   |         <span data-ttu-id="2c094-264"><strong>状态</strong></span><span class="sxs-lookup"><span data-stu-id="2c094-264"><strong>State</strong></span></span>         |                                 <span data-ttu-id="2c094-265"><em>&lt;将保留为空&gt;</em></span><span class="sxs-lookup"><span data-stu-id="2c094-265"><em>&lt;leave blank&gt;</em></span></span>                                  |                                                                                                                                                                                                                                                                              |
   | <span data-ttu-id="2c094-266"><strong>客户端身份验证</strong></span><span class="sxs-lookup"><span data-stu-id="2c094-266"><strong>Client Authentication</strong></span></span> |                                <span data-ttu-id="2c094-267">在正文中发送客户端凭据</span><span class="sxs-lookup"><span data-stu-id="2c094-267">Send client credentials in body</span></span>                                |                                                                                                                                                                                                                                                                              |


3. <span data-ttu-id="2c094-268">选择**请求令牌**按钮。</span><span class="sxs-lookup"><span data-stu-id="2c094-268">Select the **Request Token** button.</span></span>

4. <span data-ttu-id="2c094-269">Postman 会打开一个包含 Azure AD B2C 租户的登录对话框中的新窗口。</span><span class="sxs-lookup"><span data-stu-id="2c094-269">Postman opens a new window containing the Azure AD B2C tenant's sign in dialog.</span></span> <span data-ttu-id="2c094-270">（如果已经创建了一个测试策略） 的现有帐户登录，或选择**立即注册**若要创建新帐户。</span><span class="sxs-lookup"><span data-stu-id="2c094-270">Sign in with an existing account (if one was created testing the policies) or select **Sign up now** to create a new account.</span></span> <span data-ttu-id="2c094-271">**忘记了密码？** 链接用于重置忘记的密码。</span><span class="sxs-lookup"><span data-stu-id="2c094-271">The **Forgot your password?** link is used to reset a forgotten password.</span></span>

5. <span data-ttu-id="2c094-272">已成功登录后，在窗口关闭并**管理访问令牌**此时将显示对话框。</span><span class="sxs-lookup"><span data-stu-id="2c094-272">After successfully signing in, the window closes and the **MANAGE ACCESS TOKENS** dialog appears.</span></span> <span data-ttu-id="2c094-273">向下的滚动到底部，选择**使用令牌**按钮。</span><span class="sxs-lookup"><span data-stu-id="2c094-273">Scroll down to the bottom and select the **Use Token** button.</span></span>

    ![在哪里可以找到"使用令牌"按钮](./azure-ad-b2c-webapi/postman-access-token.png)

### <a name="test-the-web-api-with-authentication"></a><span data-ttu-id="2c094-275">测试 web API 身份验证</span><span class="sxs-lookup"><span data-stu-id="2c094-275">Test the web API with authentication</span></span>

<span data-ttu-id="2c094-276">选择**发送**按钮再次发送该请求。</span><span class="sxs-lookup"><span data-stu-id="2c094-276">Select the **Send** button to send the request again.</span></span> <span data-ttu-id="2c094-277">这一次，响应状态是*200 确定*，并在响应上可见的 JSON 有效负载**正文**选项卡。</span><span class="sxs-lookup"><span data-stu-id="2c094-277">This time, the response status is *200 OK* and the JSON payload is visible on the response **Body** tab.</span></span>

![有效负载和成功状态](./azure-ad-b2c-webapi/postman-success.png)

## <a name="next-steps"></a><span data-ttu-id="2c094-279">后续步骤</span><span class="sxs-lookup"><span data-stu-id="2c094-279">Next steps</span></span>

<span data-ttu-id="2c094-280">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="2c094-280">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2c094-281">创建 Azure Active Directory B2C 租户。</span><span class="sxs-lookup"><span data-stu-id="2c094-281">Create an Azure Active Directory B2C tenant.</span></span>
> * <span data-ttu-id="2c094-282">在 Azure AD B2C 中注册 Web API。</span><span class="sxs-lookup"><span data-stu-id="2c094-282">Register a Web API in Azure AD B2C.</span></span>
> * <span data-ttu-id="2c094-283">使用 Visual Studio 来创建 Web API 配置为使用 Azure AD B2C 租户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="2c094-283">Use Visual Studio to create a Web API configured to use the Azure AD B2C tenant for authentication.</span></span>
> * <span data-ttu-id="2c094-284">配置控制的 Azure AD B2C 租户行为的策略。</span><span class="sxs-lookup"><span data-stu-id="2c094-284">Configure policies controlling the behavior of the Azure AD B2C tenant.</span></span>
> * <span data-ttu-id="2c094-285">使用 Postman 来模拟一个 web 应用，用于显示登录对话框中，检索令牌，并使用它来对 web API 发出请求。</span><span class="sxs-lookup"><span data-stu-id="2c094-285">Use Postman to simulate a web app which presents a login dialog, retrieves a token, and uses it to make a request against the web API.</span></span>

<span data-ttu-id="2c094-286">继续通过学习开发你的 API:</span><span class="sxs-lookup"><span data-stu-id="2c094-286">Continue developing your API by learning to:</span></span>

* <span data-ttu-id="2c094-287">[保护 web 应用使用 Azure AD B2C 的 ASP.NET Core](xref:security/authentication/azure-ad-b2c)。</span><span class="sxs-lookup"><span data-stu-id="2c094-287">[Secure an ASP.NET Core web app using Azure AD B2C](xref:security/authentication/azure-ad-b2c).</span></span>
* <span data-ttu-id="2c094-288">[从.NET web 应用中使用 Azure AD B2C 调用.NET web API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="2c094-288">[Call a .NET web API from a .NET web app using Azure AD B2C](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet).</span></span>
* <span data-ttu-id="2c094-289">[自定义 Azure AD B2C 用户界面](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization)。</span><span class="sxs-lookup"><span data-stu-id="2c094-289">[Customize the Azure AD B2C user interface](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization).</span></span>
* <span data-ttu-id="2c094-290">[配置密码复杂性要求](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity)。</span><span class="sxs-lookup"><span data-stu-id="2c094-290">[Configure password complexity requirements](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity).</span></span>
* <span data-ttu-id="2c094-291">[启用多重身份验证](/azure/active-directory-b2c/active-directory-b2c-reference-mfa)。</span><span class="sxs-lookup"><span data-stu-id="2c094-291">[Enable multi-factor authentication](/azure/active-directory-b2c/active-directory-b2c-reference-mfa).</span></span>
* <span data-ttu-id="2c094-292">配置其他标识提供者，例如[Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app)， [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app)， [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app)， [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app)， [Twitter](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app)，等等。</span><span class="sxs-lookup"><span data-stu-id="2c094-292">Configure additional identity providers, such as [Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app), [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app), [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app), [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app), [Twitter](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app), and others.</span></span>
* <span data-ttu-id="2c094-293">[使用 Azure AD Graph API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet)从 Azure AD B2C 租户中检索其他用户信息，例如组成员身份。</span><span class="sxs-lookup"><span data-stu-id="2c094-293">[Use the Azure AD Graph API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet) to retrieve additional user information, such as group membership, from the Azure AD B2C tenant.</span></span>
