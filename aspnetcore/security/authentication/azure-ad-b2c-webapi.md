---
title: "云身份验证中的 web Api 与 Azure Active Directory B2C"
author: camsoper
description: "了解如何设置与 ASP.NET 核心 Web API 的 Azure Active Directory B2C 身份验证。 测试已通过身份验证的 web API 与 Postman。"
ms.author: casoper
manager: wpickett
ms.date: 01/25/2018
ms.topic: tutorial
ms.technology: aspnet
ms.prod: asp.net-core
ms.custom: mvc
uid: security/authentication/azure-ad-b2c-webapi
ms.openlocfilehash: c79f1152afd2f55f53bf5deb9208fa5b4d5ef64d
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="cloud-authentication-in-web-apis-with-azure-active-directory-b2c"></a><span data-ttu-id="68c5f-104">云身份验证中的 web Api 与 Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="68c5f-104">Cloud authentication in web APIs with Azure Active Directory B2C</span></span>

<span data-ttu-id="68c5f-105">作者：[Cam Soper](https://twitter.com/camsoper)</span><span class="sxs-lookup"><span data-stu-id="68c5f-105">By [Cam Soper](https://twitter.com/camsoper)</span></span>

<span data-ttu-id="68c5f-106">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C) 是为 web 和移动应用的云标识管理解决方案。</span><span class="sxs-lookup"><span data-stu-id="68c5f-106">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C) is a cloud identity management solution for web and mobile apps.</span></span> <span data-ttu-id="68c5f-107">服务提供用于在云中和本地托管的应用的身份验证。</span><span class="sxs-lookup"><span data-stu-id="68c5f-107">The service provides authentication for apps hosted in the cloud and on-premises.</span></span> <span data-ttu-id="68c5f-108">身份验证类型包括包括个人帐户，社交网络帐户和联合企业帐户。</span><span class="sxs-lookup"><span data-stu-id="68c5f-108">Authentication types include include individual accounts, social network accounts, and federated enterprise accounts.</span></span> <span data-ttu-id="68c5f-109">此外，Azure AD B2C 可以提供以最小配置多因素身份验证。</span><span class="sxs-lookup"><span data-stu-id="68c5f-109">Additionally, Azure AD B2C can provide multi-factor authentication with minimal configuration.</span></span>

> [!TIP]
> <span data-ttu-id="68c5f-110">Azure Active Directory (Azure AD) Azure AD B2C 包括单独的产品。</span><span class="sxs-lookup"><span data-stu-id="68c5f-110">Azure Active Directory (Azure AD) Azure AD B2C are separate product offerings.</span></span> <span data-ttu-id="68c5f-111">Azure AD 租户表示是一个组织，而 Azure AD B2C 租户表示标识要用于信赖方应用程序的集合。</span><span class="sxs-lookup"><span data-stu-id="68c5f-111">An Azure AD tenant represents an organization, while an Azure AD B2C tenant represents a collection of identities to be used with relying party applications.</span></span> <span data-ttu-id="68c5f-112">若要了解详细信息，请参阅[Azure AD B2C： 常见问题 (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs)。</span><span class="sxs-lookup"><span data-stu-id="68c5f-112">To learn more, see [Azure AD B2C: Frequently asked questions (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs).</span></span>

<span data-ttu-id="68c5f-113">由于 web Api 具有没有用户界面，因此它们无法将用户重定向到 Azure AD B2C 等安全令牌服务。</span><span class="sxs-lookup"><span data-stu-id="68c5f-113">Since web APIs have no user interface, they're unable to redirect the user to a secure token service like Azure AD B2C.</span></span> <span data-ttu-id="68c5f-114">相反，API 是具有已用户进行身份验证与 Azure AD B2C 将调用应用程序中传递的持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="68c5f-114">Instead, the API is passed a bearer token from the calling app, which has already authenticated the user with Azure AD B2C.</span></span> <span data-ttu-id="68c5f-115">API 然后验证该令牌而无需直接用户交互。</span><span class="sxs-lookup"><span data-stu-id="68c5f-115">The API then validates the token without direct user interaction.</span></span>

<span data-ttu-id="68c5f-116">在本教程中，学习如何：</span><span class="sxs-lookup"><span data-stu-id="68c5f-116">In this tutorial, learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="68c5f-117">创建 Azure Active Directory B2C 租户。</span><span class="sxs-lookup"><span data-stu-id="68c5f-117">Create an Azure Active Directory B2C tenant.</span></span>
> * <span data-ttu-id="68c5f-118">在 Azure AD B2C 中注册 Web API。</span><span class="sxs-lookup"><span data-stu-id="68c5f-118">Register a Web API in Azure AD B2C.</span></span>
> * <span data-ttu-id="68c5f-119">使用 Visual Studio 创建 Web API 配置为使用 Azure AD B2C 租户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="68c5f-119">Use Visual Studio to create a Web API configured to use the Azure AD B2C tenant for authentication.</span></span>
> * <span data-ttu-id="68c5f-120">配置策略控制的 Azure AD B2C 租户的行为。</span><span class="sxs-lookup"><span data-stu-id="68c5f-120">Configure policies controlling the behavior of the Azure AD B2C tenant.</span></span>
> * <span data-ttu-id="68c5f-121">使用 Postman 以模拟 web 应用将其提供一个登录对话框中，检索令牌，并使用它来对 web API 发出请求。</span><span class="sxs-lookup"><span data-stu-id="68c5f-121">Use Postman to simulate a web app which presents a login dialog, retrieves a token, and uses it to make a request against the web API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68c5f-122">系统必备</span><span class="sxs-lookup"><span data-stu-id="68c5f-122">Prerequisites</span></span>

<span data-ttu-id="68c5f-123">对于本演练具备以下条件：</span><span class="sxs-lookup"><span data-stu-id="68c5f-123">The following are required for this walkthrough:</span></span>

* [<span data-ttu-id="68c5f-124">Microsoft Azure 订阅</span><span class="sxs-lookup"><span data-stu-id="68c5f-124">Microsoft Azure subscription</span></span>](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)
* <span data-ttu-id="68c5f-125">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) （任意版本）</span><span class="sxs-lookup"><span data-stu-id="68c5f-125">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) (any edition)</span></span>
* [<span data-ttu-id="68c5f-126">Postman</span><span class="sxs-lookup"><span data-stu-id="68c5f-126">Postman</span></span>](https://www.getpostman.com/postman)

## <a name="create-the-azure-active-directory-b2c-tenant"></a><span data-ttu-id="68c5f-127">创建 Azure Active Directory B2C 租户</span><span class="sxs-lookup"><span data-stu-id="68c5f-127">Create the Azure Active Directory B2C tenant</span></span>

<span data-ttu-id="68c5f-128">创建 Azure AD B2C 租户[文档中所述](/azure/active-directory-b2c/active-directory-b2c-get-started)。</span><span class="sxs-lookup"><span data-stu-id="68c5f-128">Create an Azure AD B2C tenant [as described in the documentation](/azure/active-directory-b2c/active-directory-b2c-get-started).</span></span> <span data-ttu-id="68c5f-129">出现提示时，将租户与 Azure 订阅相关联是可选的出于本教程。</span><span class="sxs-lookup"><span data-stu-id="68c5f-129">When prompted, associating the tenant with an Azure subscription is optional for this tutorial.</span></span>

## <a name="configure-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="68c5f-130">配置注册或登录策略</span><span class="sxs-lookup"><span data-stu-id="68c5f-130">Configure a sign-up or sign-in policy</span></span>

<span data-ttu-id="68c5f-131">使用到的 Azure AD B2C 文档中的步骤[创建注册或登录策略](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy)。</span><span class="sxs-lookup"><span data-stu-id="68c5f-131">Use the steps in the Azure AD B2C documentation to [create a sign-up or sign-in policy](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy).</span></span> <span data-ttu-id="68c5f-132">命名策略时**SiUpIn**。</span><span class="sxs-lookup"><span data-stu-id="68c5f-132">Name the policy **SiUpIn**.</span></span>  <span data-ttu-id="68c5f-133">使用的文档中提供的示例值**标识提供程序**，**注册属性**，和**应用程序声明**。</span><span class="sxs-lookup"><span data-stu-id="68c5f-133">Use the example values provided in the documentation for **Identity providers**, **Sign-up attributes**, and **Application claims**.</span></span> <span data-ttu-id="68c5f-134">使用**立即运行**是可选的按钮以测试策略，如文档中所述。</span><span class="sxs-lookup"><span data-stu-id="68c5f-134">Using the **Run now** button to test the policy as described in the documentation is optional.</span></span>

## <a name="register-the-api-in-azure-ad-b2c"></a><span data-ttu-id="68c5f-135">在 Azure AD B2C 注册 API</span><span class="sxs-lookup"><span data-stu-id="68c5f-135">Register the API in Azure AD B2C</span></span>

<span data-ttu-id="68c5f-136">新创建的 Azure AD B2C 租户中注册你的 API 使用[文档中的步骤](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-api)下**注册 web API**部分。</span><span class="sxs-lookup"><span data-stu-id="68c5f-136">In the newly created Azure AD B2C tenant, register your API using [the steps in the documentation](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-api) under the **Register a web API** section.</span></span>

<span data-ttu-id="68c5f-137">使用以下值：</span><span class="sxs-lookup"><span data-stu-id="68c5f-137">Use the following values:</span></span>

| <span data-ttu-id="68c5f-138">设置</span><span class="sxs-lookup"><span data-stu-id="68c5f-138">Setting</span></span>                       | <span data-ttu-id="68c5f-139">“值”</span><span class="sxs-lookup"><span data-stu-id="68c5f-139">Value</span></span>               | <span data-ttu-id="68c5f-140">说明</span><span class="sxs-lookup"><span data-stu-id="68c5f-140">Notes</span></span>                                                                                  |
|-------------------------------|---------------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="68c5f-141">**名称**</span><span class="sxs-lookup"><span data-stu-id="68c5f-141">**Name**</span></span>                      | <span data-ttu-id="68c5f-142">*&lt;API 名称&gt;*</span><span class="sxs-lookup"><span data-stu-id="68c5f-142">*&lt;API name&gt;*</span></span>  | <span data-ttu-id="68c5f-143">输入**名称**描述你的应用对使用者的应用。</span><span class="sxs-lookup"><span data-stu-id="68c5f-143">Enter a **Name** for the app that describes your app to consumers.</span></span>                     |
| <span data-ttu-id="68c5f-144">**包括 web 应用程序/web API**</span><span class="sxs-lookup"><span data-stu-id="68c5f-144">**Include web app / web API**</span></span> | <span data-ttu-id="68c5f-145">是</span><span class="sxs-lookup"><span data-stu-id="68c5f-145">Yes</span></span>                 |                                                                                        |
| <span data-ttu-id="68c5f-146">**允许隐式流**</span><span class="sxs-lookup"><span data-stu-id="68c5f-146">**Allow implicit flow**</span></span>       | <span data-ttu-id="68c5f-147">是</span><span class="sxs-lookup"><span data-stu-id="68c5f-147">Yes</span></span>                 |                                                                                        |
| <span data-ttu-id="68c5f-148">**回复 URL**</span><span class="sxs-lookup"><span data-stu-id="68c5f-148">**Reply URL**</span></span>                 | `https://localhost` | <span data-ttu-id="68c5f-149">答复 Url 是 Azure AD B2C 其中返回您的应用程序请求的任何令牌的终结点。</span><span class="sxs-lookup"><span data-stu-id="68c5f-149">Reply URLs are endpoints where Azure AD B2C returns any tokens that your app requests.</span></span> |
| <span data-ttu-id="68c5f-150">**应用程序 ID URI**</span><span class="sxs-lookup"><span data-stu-id="68c5f-150">**App ID URI**</span></span>                | <span data-ttu-id="68c5f-151">*api*</span><span class="sxs-lookup"><span data-stu-id="68c5f-151">*api*</span></span>               | <span data-ttu-id="68c5f-152">URI 不需要解析为物理地址。</span><span class="sxs-lookup"><span data-stu-id="68c5f-152">The URI doesn't need to resolve to a physical address.</span></span> <span data-ttu-id="68c5f-153">它只需是唯一的。</span><span class="sxs-lookup"><span data-stu-id="68c5f-153">It only needs to be unique.</span></span>     |
| <span data-ttu-id="68c5f-154">**包括本机客户端**</span><span class="sxs-lookup"><span data-stu-id="68c5f-154">**Include native client**</span></span>     | <span data-ttu-id="68c5f-155">否</span><span class="sxs-lookup"><span data-stu-id="68c5f-155">No</span></span>                  |                                                                                        |

<span data-ttu-id="68c5f-156">注册 API 后，将显示在租户中的应用和 Api 的列表。</span><span class="sxs-lookup"><span data-stu-id="68c5f-156">After the API is registered, the list of apps and APIs in the tenant is displayed.</span></span> <span data-ttu-id="68c5f-157">选择刚刚注册的 API。</span><span class="sxs-lookup"><span data-stu-id="68c5f-157">Select the API that was just registered.</span></span> <span data-ttu-id="68c5f-158">选择**复制**右侧的图标**应用程序 ID**字段可将它复制到剪贴板。</span><span class="sxs-lookup"><span data-stu-id="68c5f-158">Select the **Copy** icon to the right of the **Application ID** field to copy it to the clipboard.</span></span> <span data-ttu-id="68c5f-159">选择**发布作用域**和验证默认*user_impersonation*作用域是存在。</span><span class="sxs-lookup"><span data-stu-id="68c5f-159">Select **Published scopes** and verify the default *user_impersonation* scope is present.</span></span>

## <a name="create-an-aspnet-core-app-in-visual-studio-2017"></a><span data-ttu-id="68c5f-160">在 Visual Studio 2017 年 1 中创建 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="68c5f-160">Create an ASP.NET Core app in Visual Studio 2017</span></span>

<span data-ttu-id="68c5f-161">Visual Studio Web 应用程序模板可以配置为使用 Azure AD B2C 租户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="68c5f-161">The Visual Studio Web Application template can be configured to use the Azure AD B2C tenant for authentication.</span></span>

<span data-ttu-id="68c5f-162">在 Visual Studio 中：</span><span class="sxs-lookup"><span data-stu-id="68c5f-162">In Visual Studio:</span></span>

1. <span data-ttu-id="68c5f-163">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="68c5f-163">Create a new ASP.NET Core Web Application.</span></span> 
2. <span data-ttu-id="68c5f-164">选择**Web API**从模板列表中。</span><span class="sxs-lookup"><span data-stu-id="68c5f-164">Select **Web API** from the list of templates.</span></span>
3. <span data-ttu-id="68c5f-165">选择**更改身份验证**按钮。</span><span class="sxs-lookup"><span data-stu-id="68c5f-165">Select the **Change Authentication** button.</span></span>
    
    ![更改身份验证按钮](./azure-ad-b2c-webapi/change-auth-button.png)

4. <span data-ttu-id="68c5f-167">在**更改身份验证**对话框中，选择**单个用户帐户**，然后选择**连接到现有用户存储在云中**下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="68c5f-167">In the **Change Authentication** dialog, select **Individual User Accounts**, and then select **Connect to an existing user store in the cloud** in the dropdown.</span></span> 
    
    ![更改身份验证对话框](./azure-ad-b2c-webapi/change-auth-dialog.png)

5. <span data-ttu-id="68c5f-169">完成窗体具有以下值：</span><span class="sxs-lookup"><span data-stu-id="68c5f-169">Complete the form with the following values:</span></span>
    
    | <span data-ttu-id="68c5f-170">设置</span><span class="sxs-lookup"><span data-stu-id="68c5f-170">Setting</span></span>                       | <span data-ttu-id="68c5f-171">“值”</span><span class="sxs-lookup"><span data-stu-id="68c5f-171">Value</span></span>                                                 |
    |-------------------------------|-------------------------------------------------------|
    | <span data-ttu-id="68c5f-172">**域名**</span><span class="sxs-lookup"><span data-stu-id="68c5f-172">**Domain Name**</span></span>               | <span data-ttu-id="68c5f-173">*&lt;B2C 租户的域名&gt;*</span><span class="sxs-lookup"><span data-stu-id="68c5f-173">*&lt;the domain name of your B2C tenant&gt;*</span></span>          |
    | <span data-ttu-id="68c5f-174">**应用程序 ID**</span><span class="sxs-lookup"><span data-stu-id="68c5f-174">**Application ID**</span></span>            | <span data-ttu-id="68c5f-175">*&lt;粘贴剪贴板中的应用程序 ID&gt;*</span><span class="sxs-lookup"><span data-stu-id="68c5f-175">*&lt;paste the Application ID from the clipboard&gt;*</span></span> |
    | <span data-ttu-id="68c5f-176">**注册或登录策略**</span><span class="sxs-lookup"><span data-stu-id="68c5f-176">**Sign-up or sign-in policy**</span></span> | `B2C_1_SiUpIn`                                        |
    
    <span data-ttu-id="68c5f-177">选择**确定**关闭**更改身份验证**对话框。</span><span class="sxs-lookup"><span data-stu-id="68c5f-177">Select **OK** to close the **Change Authentication** dialog.</span></span> <span data-ttu-id="68c5f-178">选择**确定**创建 web 应用。</span><span class="sxs-lookup"><span data-stu-id="68c5f-178">Select **OK** to create the web app.</span></span>

<span data-ttu-id="68c5f-179">Visual Studio 使用名为的控制器中创建 web API *ValuesController.cs*返回 GET 请求的硬编码值。</span><span class="sxs-lookup"><span data-stu-id="68c5f-179">Visual Studio creates the web API with a controller named *ValuesController.cs* that returns hard-coded values for GET requests.</span></span> <span data-ttu-id="68c5f-180">类用修饰[Authorize 属性](xref:security/authorization/simple)，因此所有请求都需要身份验证。</span><span class="sxs-lookup"><span data-stu-id="68c5f-180">The class is decorated with the [Authorize attribute](xref:security/authorization/simple), so all requests require authentication.</span></span>

## <a name="run-the-web-api"></a><span data-ttu-id="68c5f-181">运行 web API</span><span class="sxs-lookup"><span data-stu-id="68c5f-181">Run the web API</span></span>

<span data-ttu-id="68c5f-182">在 Visual Studio 中，运行 API。</span><span class="sxs-lookup"><span data-stu-id="68c5f-182">In Visual Studio, run the API.</span></span> <span data-ttu-id="68c5f-183">Visual Studio 将启动浏览器指向的 API 根 URL。</span><span class="sxs-lookup"><span data-stu-id="68c5f-183">Visual Studio launches a browser pointed at the API's root URL.</span></span> <span data-ttu-id="68c5f-184">请注意地址栏中中的 URL 并将在后台运行的 API。</span><span class="sxs-lookup"><span data-stu-id="68c5f-184">Note the URL in the address bar, and leave the API running in the background.</span></span>

> [!NOTE] <span data-ttu-id="68c5f-185">由于没有为根 URL 定义无控制器，浏览器将显示 404 （找不到页） 错误。</span><span class="sxs-lookup"><span data-stu-id="68c5f-185">Since there is no controller defined for the root URL, the browser displays a 404 (page not found) error.</span></span> <span data-ttu-id="68c5f-186">这是预期行为。</span><span class="sxs-lookup"><span data-stu-id="68c5f-186">This is expected behavior.</span></span>

## <a name="use-postman-to-get-a-token-and-test-the-api"></a><span data-ttu-id="68c5f-187">使用 Postman 来获取令牌和测试 API</span><span class="sxs-lookup"><span data-stu-id="68c5f-187">Use Postman to get a token and test the API</span></span>

<span data-ttu-id="68c5f-188">[Postman](https://getpostman.com/postman)是用于测试的工具 web Api。</span><span class="sxs-lookup"><span data-stu-id="68c5f-188">[Postman](https://getpostman.com/postman) is a tool for testing web APIs.</span></span> <span data-ttu-id="68c5f-189">对于本教程，Postman 模拟的 web 应用程序访问 web API 代表该用户。</span><span class="sxs-lookup"><span data-stu-id="68c5f-189">For this tutorial, Postman simulates a web app that accesses the web API on the user's behalf.</span></span>

### <a name="register-postman-as-a-web-app"></a><span data-ttu-id="68c5f-190">为 web 应用注册 Postman</span><span class="sxs-lookup"><span data-stu-id="68c5f-190">Register Postman as a web app</span></span>

<span data-ttu-id="68c5f-191">由于 Postman 模拟的 web 应用程序可以从 Azure AD B2C 租户获取令牌，则必须注册在租户中为 web 应用。</span><span class="sxs-lookup"><span data-stu-id="68c5f-191">Since Postman simulates a web app that can obtain tokens from the Azure AD B2C tenant, it must be registered in the tenant as a web app.</span></span> <span data-ttu-id="68c5f-192">注册使用 Postman[文档中的步骤](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app)下**注册 web 应用**部分。</span><span class="sxs-lookup"><span data-stu-id="68c5f-192">Register Postman using [the steps in the documentation](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app) under the **Register a web app** section.</span></span> <span data-ttu-id="68c5f-193">在停止**创建 web 应用程序客户端密钥**部分。</span><span class="sxs-lookup"><span data-stu-id="68c5f-193">Stop at the **Create a web app client secret** section.</span></span> <span data-ttu-id="68c5f-194">出于本教程中，无需客户端密钥。</span><span class="sxs-lookup"><span data-stu-id="68c5f-194">A client secret isn't required for this tutorial.</span></span> 

<span data-ttu-id="68c5f-195">使用以下值：</span><span class="sxs-lookup"><span data-stu-id="68c5f-195">Use the following values:</span></span>

| <span data-ttu-id="68c5f-196">设置</span><span class="sxs-lookup"><span data-stu-id="68c5f-196">Setting</span></span>                       | <span data-ttu-id="68c5f-197">“值”</span><span class="sxs-lookup"><span data-stu-id="68c5f-197">Value</span></span>                            | <span data-ttu-id="68c5f-198">说明</span><span class="sxs-lookup"><span data-stu-id="68c5f-198">Notes</span></span>                           |
|-------------------------------|----------------------------------|---------------------------------|
| <span data-ttu-id="68c5f-199">**名称**</span><span class="sxs-lookup"><span data-stu-id="68c5f-199">**Name**</span></span>                      | <span data-ttu-id="68c5f-200">Postman</span><span class="sxs-lookup"><span data-stu-id="68c5f-200">Postman</span></span>                          |                                 |
| <span data-ttu-id="68c5f-201">**包括 web 应用程序/web API**</span><span class="sxs-lookup"><span data-stu-id="68c5f-201">**Include web app / web API**</span></span> | <span data-ttu-id="68c5f-202">是</span><span class="sxs-lookup"><span data-stu-id="68c5f-202">Yes</span></span>                              |                                 |
| <span data-ttu-id="68c5f-203">**允许隐式流**</span><span class="sxs-lookup"><span data-stu-id="68c5f-203">**Allow implicit flow**</span></span>       | <span data-ttu-id="68c5f-204">是</span><span class="sxs-lookup"><span data-stu-id="68c5f-204">Yes</span></span>                              |                                 |
| <span data-ttu-id="68c5f-205">**回复 URL**</span><span class="sxs-lookup"><span data-stu-id="68c5f-205">**Reply URL**</span></span>                 | `https://getpostman.com/postman` |                                 |
| <span data-ttu-id="68c5f-206">**应用程序 ID URI**</span><span class="sxs-lookup"><span data-stu-id="68c5f-206">**App ID URI**</span></span>                | <span data-ttu-id="68c5f-207">*&lt;将保留为空&gt;*</span><span class="sxs-lookup"><span data-stu-id="68c5f-207">*&lt;leave blank&gt;*</span></span>            | <span data-ttu-id="68c5f-208">无需进行本教程。</span><span class="sxs-lookup"><span data-stu-id="68c5f-208">Not required for this tutorial.</span></span> |
| <span data-ttu-id="68c5f-209">**包括本机客户端**</span><span class="sxs-lookup"><span data-stu-id="68c5f-209">**Include native client**</span></span>     | <span data-ttu-id="68c5f-210">否</span><span class="sxs-lookup"><span data-stu-id="68c5f-210">No</span></span>                               |                                 |

<span data-ttu-id="68c5f-211">新注册的 web 应用程序需要访问 web API 代表该用户的权限。</span><span class="sxs-lookup"><span data-stu-id="68c5f-211">The newly registered web app needs permission to access the web API on the user's behalf.</span></span>  

1. <span data-ttu-id="68c5f-212">选择**Postman**的应用，然后选择列表中**API 访问**从左侧菜单。</span><span class="sxs-lookup"><span data-stu-id="68c5f-212">Select **Postman** in the list of apps and then select **API access** from the menu on the left.</span></span>
2. <span data-ttu-id="68c5f-213">选择**+ 添加**。</span><span class="sxs-lookup"><span data-stu-id="68c5f-213">Select **+ Add**.</span></span>
3. <span data-ttu-id="68c5f-214">在**选择 API**下拉列表中，选择 web API 的名称。</span><span class="sxs-lookup"><span data-stu-id="68c5f-214">In the **Select API** dropdown, select the name of the web API.</span></span>
4. <span data-ttu-id="68c5f-215">在**选择作用域**下拉列表中，确保选中所有作用域。</span><span class="sxs-lookup"><span data-stu-id="68c5f-215">In the **Select Scopes** dropdown, ensure all scopes are selected.</span></span>
5. <span data-ttu-id="68c5f-216">选择**确定**。</span><span class="sxs-lookup"><span data-stu-id="68c5f-216">Select **Ok**.</span></span>

<span data-ttu-id="68c5f-217">请注意 Postman 应用的应用程序 ID，因为它需获取的持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="68c5f-217">Note the Postman app's Application ID, as it's required to obtain a bearer token.</span></span>

### <a name="create-a-postman-request"></a><span data-ttu-id="68c5f-218">创建 Postman 请求</span><span class="sxs-lookup"><span data-stu-id="68c5f-218">Create a Postman request</span></span>

<span data-ttu-id="68c5f-219">启动 Postman。</span><span class="sxs-lookup"><span data-stu-id="68c5f-219">Launch Postman.</span></span> <span data-ttu-id="68c5f-220">默认情况下，显示 Postman**新建**时启动的对话框。</span><span class="sxs-lookup"><span data-stu-id="68c5f-220">By default, Postman displays the **Create New** dialog upon launching.</span></span> <span data-ttu-id="68c5f-221">如果未显示对话框中，选择**+ 新建**在左上角的按钮。</span><span class="sxs-lookup"><span data-stu-id="68c5f-221">If the dialog isn't displayed, select the **+ New** button in the upper left.</span></span>

<span data-ttu-id="68c5f-222">从**新建**对话框：</span><span class="sxs-lookup"><span data-stu-id="68c5f-222">From the **Create New** dialog:</span></span>

1. <span data-ttu-id="68c5f-223">选择**请求**。</span><span class="sxs-lookup"><span data-stu-id="68c5f-223">Select **Request**.</span></span>
    
    ![请求按钮](./azure-ad-b2c-webapi/postman-create-new.png)

2. <span data-ttu-id="68c5f-225">输入*获取值*中**请求名称**框。</span><span class="sxs-lookup"><span data-stu-id="68c5f-225">Enter *Get Values* in the **Request name** box.</span></span>
3. <span data-ttu-id="68c5f-226">选择**+ 创建集合**以创建用于存储请求新的集合。</span><span class="sxs-lookup"><span data-stu-id="68c5f-226">Select **+ Create Collection** to create a new collection for storing the request.</span></span> <span data-ttu-id="68c5f-227">命名集合*ASP.NET Core 教程*，然后选择复选标记。</span><span class="sxs-lookup"><span data-stu-id="68c5f-227">Name the collection *ASP.NET Core tutorials* and then select the checkmark.</span></span>
    
    ![创建新集合](./azure-ad-b2c-webapi/postman-create-collection.png)

4. <span data-ttu-id="68c5f-229">选择**将保存到 ASP.NET 核心教程**按钮。</span><span class="sxs-lookup"><span data-stu-id="68c5f-229">Select the **Save to ASP.NET Core tutorials** button.</span></span>

### <a name="test-the-web-api-withoutauthentication"></a><span data-ttu-id="68c5f-230">测试 web API withoutauthentication</span><span class="sxs-lookup"><span data-stu-id="68c5f-230">Test the web API withoutauthentication</span></span>

<span data-ttu-id="68c5f-231">若要验证 web API 需要身份验证，首先请无身份验证的请求。</span><span class="sxs-lookup"><span data-stu-id="68c5f-231">To verify that the web API requires authentication, first make a request without authentication.</span></span>

1. <span data-ttu-id="68c5f-232">在**输入请求 URL**框中，输入的 URL `ValuesController`。</span><span class="sxs-lookup"><span data-stu-id="68c5f-232">In the **Enter request URL** box, enter the URL for `ValuesController`.</span></span> <span data-ttu-id="68c5f-233">URL 是显示在浏览器中使用的相同**api/值**追加。</span><span class="sxs-lookup"><span data-stu-id="68c5f-233">The URL is the same as displayed in the browser with **api/values** appended.</span></span> <span data-ttu-id="68c5f-234">示例将`https://localhost:44375/api/values`。</span><span class="sxs-lookup"><span data-stu-id="68c5f-234">An example would be `https://localhost:44375/api/values`.</span></span>
2. <span data-ttu-id="68c5f-235">选择**发送**按钮。</span><span class="sxs-lookup"><span data-stu-id="68c5f-235">Select the **Send** button.</span></span>
3. <span data-ttu-id="68c5f-236">请注意响应的状态是*401 未授权*。</span><span class="sxs-lookup"><span data-stu-id="68c5f-236">Note the status of the response is *401 Unauthorized*.</span></span>

    ![401 未授权的响应](./azure-ad-b2c-webapi/postman-401-status.png)

### <a name="obtain-a-bearer-token"></a><span data-ttu-id="68c5f-238">获取的持有者令牌</span><span class="sxs-lookup"><span data-stu-id="68c5f-238">Obtain a bearer token</span></span>

<span data-ttu-id="68c5f-239">要对 web API 进行身份验证的请求，持有者令牌是必需的。</span><span class="sxs-lookup"><span data-stu-id="68c5f-239">To make an authenticated request to the web API, a bearer token is required.</span></span> <span data-ttu-id="68c5f-240">Postman 使得容易登录到 Azure AD B2C 租户并获取的令牌。</span><span class="sxs-lookup"><span data-stu-id="68c5f-240">Postman makes it easy to sign in to the Azure AD B2C tenant and obtain a token.</span></span>

1. <span data-ttu-id="68c5f-241">上**授权**选项卡上，在**类型**下拉列表中，选择**OAuth 2.0**。</span><span class="sxs-lookup"><span data-stu-id="68c5f-241">On the **Authorization** tab, in the **TYPE** dropdown, select **OAuth 2.0**.</span></span> <span data-ttu-id="68c5f-242">在**授权将数据添加到**下拉列表中，选择**请求标头**。</span><span class="sxs-lookup"><span data-stu-id="68c5f-242">In the **Add authorization data to** dropdown, select **Request Headers**.</span></span> <span data-ttu-id="68c5f-243">选择**获取新访问令牌**。</span><span class="sxs-lookup"><span data-stu-id="68c5f-243">Select **Get New Access Token**.</span></span>
    
    ![使用设置的授权选项卡](./azure-ad-b2c-webapi/postman-auth-tab.png)

2. <span data-ttu-id="68c5f-245">完成**获取新访问令牌**，如下所示的对话框：</span><span class="sxs-lookup"><span data-stu-id="68c5f-245">Complete the **GET NEW ACCESS TOKEN** dialog as follows:</span></span>
    
    | <span data-ttu-id="68c5f-246">设置</span><span class="sxs-lookup"><span data-stu-id="68c5f-246">Setting</span></span>                   | <span data-ttu-id="68c5f-247">“值”</span><span class="sxs-lookup"><span data-stu-id="68c5f-247">Value</span></span>                                                                                         | <span data-ttu-id="68c5f-248">说明</span><span class="sxs-lookup"><span data-stu-id="68c5f-248">Notes</span></span>                                                                                      |
    |---------------------------|-----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
    | <span data-ttu-id="68c5f-249">**标记名称**</span><span class="sxs-lookup"><span data-stu-id="68c5f-249">**Token Name**</span></span>            | <span data-ttu-id="68c5f-250">*&lt;标记名称&gt;*</span><span class="sxs-lookup"><span data-stu-id="68c5f-250">*&lt;token name&gt;*</span></span>                                                                          | <span data-ttu-id="68c5f-251">输入该令牌的描述性名称。</span><span class="sxs-lookup"><span data-stu-id="68c5f-251">Enter a descriptive name for the token.</span></span>                                                    |
    | <span data-ttu-id="68c5f-252">**授予类型构建的**</span><span class="sxs-lookup"><span data-stu-id="68c5f-252">**Grant Type**</span></span>            | <span data-ttu-id="68c5f-253">隐式</span><span class="sxs-lookup"><span data-stu-id="68c5f-253">Implicit</span></span>                                                                                      |                                                                                            |
    | <span data-ttu-id="68c5f-254">**回调 URL**</span><span class="sxs-lookup"><span data-stu-id="68c5f-254">**Callback URL**</span></span>          | `https://getpostman.com/postman`                                                              |                                                                                            |
    | <span data-ttu-id="68c5f-255">**身份验证 URL**</span><span class="sxs-lookup"><span data-stu-id="68c5f-255">**Auth URL**</span></span>              | `https://login.microsoftonline.com/<tenant domain name>/oauth2/v2.0/authorize?p=B2C_1_SiUpIn` | <span data-ttu-id="68c5f-256">替换*&lt;租户域名&gt;*与租户的域名，而无需命令的尖括号。</span><span class="sxs-lookup"><span data-stu-id="68c5f-256">Replace *&lt;tenant domain name&gt;* with the tenant's domain name without angle brackets.</span></span> |
    | <span data-ttu-id="68c5f-257">**客户端 ID**</span><span class="sxs-lookup"><span data-stu-id="68c5f-257">**Client ID**</span></span>             | <span data-ttu-id="68c5f-258">*&lt;输入 Postman 应用<b>应用程序 ID</b>&gt;*</span><span class="sxs-lookup"><span data-stu-id="68c5f-258">*&lt;enter the Postman app's <b>Application ID</b>&gt;*</span></span>                                       |                                                                                            |
    | <span data-ttu-id="68c5f-259">**客户端密钥**</span><span class="sxs-lookup"><span data-stu-id="68c5f-259">**Client Secret**</span></span>         | <span data-ttu-id="68c5f-260">*&lt;将保留为空&gt;*</span><span class="sxs-lookup"><span data-stu-id="68c5f-260">*&lt;leave blank&gt;*</span></span>                                                                         |                                                                                            |
    | <span data-ttu-id="68c5f-261">**范围**</span><span class="sxs-lookup"><span data-stu-id="68c5f-261">**Scope**</span></span>                 | `https://<tenant domain name>/api/user_impersonation openid offline_access`                   | <span data-ttu-id="68c5f-262">替换*&lt;租户域名&gt;*与租户的域名，而无需命令的尖括号。</span><span class="sxs-lookup"><span data-stu-id="68c5f-262">Replace *&lt;tenant domain name&gt;* with the tenant's domain name without angle brackets.</span></span> |
    | <span data-ttu-id="68c5f-263">**客户端身份验证**</span><span class="sxs-lookup"><span data-stu-id="68c5f-263">**Client Authentication**</span></span> | <span data-ttu-id="68c5f-264">在正文中发送客户端凭据</span><span class="sxs-lookup"><span data-stu-id="68c5f-264">Send client credentials in body</span></span>                                                               |                                                                                            |
    
3. <span data-ttu-id="68c5f-265">选择**令牌请求**按钮。</span><span class="sxs-lookup"><span data-stu-id="68c5f-265">Select the **Request Token** button.</span></span>

4. <span data-ttu-id="68c5f-266">Postman 打开包含 Azure AD B2C 租户的登录对话框中的新窗口中。</span><span class="sxs-lookup"><span data-stu-id="68c5f-266">Postman opens a new window containing the Azure AD B2C tenant's sign in dialog.</span></span> <span data-ttu-id="68c5f-267">使用现有帐户登录 （如果已创建一个测试策略） 或选择**立即注册**创建新帐户。</span><span class="sxs-lookup"><span data-stu-id="68c5f-267">Sign in with an existing account (if one was created testing the policies) or select **Sign up now** to create a new account.</span></span> <span data-ttu-id="68c5f-268">**忘记了密码？**链接用于重置忘记了的密码。</span><span class="sxs-lookup"><span data-stu-id="68c5f-268">The **Forgot your password?** link is used to reset a forgotten password.</span></span>

5. <span data-ttu-id="68c5f-269">已成功登录后，该窗口将关闭与**管理访问令牌**此时将显示对话框。</span><span class="sxs-lookup"><span data-stu-id="68c5f-269">After successfully signing in, the window closes and the **MANAGE ACCESS TOKENS** dialog appears.</span></span> <span data-ttu-id="68c5f-270">向下的滚动到底部并选择**使用令牌**按钮。</span><span class="sxs-lookup"><span data-stu-id="68c5f-270">Scroll down to the bottom and select the **Use Token** button.</span></span>
    
    ![在哪里可以找到"使用令牌"按钮](./azure-ad-b2c-webapi/postman-access-token.png)

### <a name="test-the-web-api-with-authentication"></a><span data-ttu-id="68c5f-272">测试身份验证与 web API</span><span class="sxs-lookup"><span data-stu-id="68c5f-272">Test the web API with authentication</span></span>

<span data-ttu-id="68c5f-273">选择**发送**按钮以重新发送请求。</span><span class="sxs-lookup"><span data-stu-id="68c5f-273">Select the **Send** button to send the request again.</span></span> <span data-ttu-id="68c5f-274">此时，响应状态是*200 确定*JSON 负载且在响应上可见**正文**选项卡。</span><span class="sxs-lookup"><span data-stu-id="68c5f-274">This time, the response status is *200 OK* and the JSON payload is visible on the response **Body** tab.</span></span>
    
![负载和成功状态](./azure-ad-b2c-webapi/postman-success.png)

## <a name="next-steps"></a><span data-ttu-id="68c5f-276">后续步骤</span><span class="sxs-lookup"><span data-stu-id="68c5f-276">Next steps</span></span>

<span data-ttu-id="68c5f-277">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="68c5f-277">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="68c5f-278">创建 Azure Active Directory B2C 租户。</span><span class="sxs-lookup"><span data-stu-id="68c5f-278">Create an Azure Active Directory B2C tenant.</span></span>
> * <span data-ttu-id="68c5f-279">在 Azure AD B2C 中注册 Web API。</span><span class="sxs-lookup"><span data-stu-id="68c5f-279">Register a Web API in Azure AD B2C.</span></span>
> * <span data-ttu-id="68c5f-280">使用 Visual Studio 创建 Web API 配置为使用 Azure AD B2C 租户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="68c5f-280">Use Visual Studio to create a Web API configured to use the Azure AD B2C tenant for authentication.</span></span>
> * <span data-ttu-id="68c5f-281">配置策略控制的 Azure AD B2C 租户的行为。</span><span class="sxs-lookup"><span data-stu-id="68c5f-281">Configure policies controlling the behavior of the Azure AD B2C tenant.</span></span>
> * <span data-ttu-id="68c5f-282">使用 Postman 以模拟 web 应用将其提供一个登录对话框中，检索令牌，并使用它来对 web API 发出请求。</span><span class="sxs-lookup"><span data-stu-id="68c5f-282">Use Postman to simulate a web app which presents a login dialog, retrieves a token, and uses it to make a request against the web API.</span></span>

<span data-ttu-id="68c5f-283">在继续学习到开发你的 API:</span><span class="sxs-lookup"><span data-stu-id="68c5f-283">Continue developing your API by learning to:</span></span>

* <span data-ttu-id="68c5f-284">[保护 web 应用使用 Azure AD B2C 的 ASP.NET Core](xref:security/authentication/azure-ad-b2c)。</span><span class="sxs-lookup"><span data-stu-id="68c5f-284">[Secure an ASP.NET Core web app using Azure AD B2C](xref:security/authentication/azure-ad-b2c).</span></span>
* <span data-ttu-id="68c5f-285">[从使用 Azure AD B2C 的.NET web 应用程序调用.NET web API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="68c5f-285">[Call a .NET web API from a .NET web app using Azure AD B2C](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet).</span></span>
* <span data-ttu-id="68c5f-286">[自定义 Azure AD B2C 用户界面](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization)。</span><span class="sxs-lookup"><span data-stu-id="68c5f-286">[Customize the Azure AD B2C user interface](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization).</span></span>
* <span data-ttu-id="68c5f-287">[配置密码复杂性要求](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity)。</span><span class="sxs-lookup"><span data-stu-id="68c5f-287">[Configure password complexity requirements](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity).</span></span>
* <span data-ttu-id="68c5f-288">[启用多因素身份验证](/azure/active-directory-b2c/active-directory-b2c-reference-mfa)。</span><span class="sxs-lookup"><span data-stu-id="68c5f-288">[Enable multi-factor authentication](/azure/active-directory-b2c/active-directory-b2c-reference-mfa).</span></span>
* <span data-ttu-id="68c5f-289">配置其他标识提供程序，例如[Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app)， [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app)， [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app)， [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app)， [Twitter](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app)，和其他人。</span><span class="sxs-lookup"><span data-stu-id="68c5f-289">Configure additional identity providers, such as [Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app), [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app), [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app), [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app), [Twitter](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app), and others.</span></span>
* <span data-ttu-id="68c5f-290">[使用 Azure AD Graph API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet)从 Azure AD B2C 租户中检索其他用户信息，例如组成员身份。</span><span class="sxs-lookup"><span data-stu-id="68c5f-290">[Use the Azure AD Graph API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet) to retrieve additional user information, such as group membership, from the Azure AD B2C tenant.</span></span>