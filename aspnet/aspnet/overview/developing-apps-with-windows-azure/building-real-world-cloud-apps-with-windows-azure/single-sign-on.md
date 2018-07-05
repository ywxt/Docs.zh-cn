---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: 单一登录 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
ms.technology: ''
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 213b8fe091bcac7f55fd62ab305c77fcbc5a77ad
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374375"
---
<a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="34982-104">单一登录 （使用 Azure 构建实际云应用）</span><span class="sxs-lookup"><span data-stu-id="34982-104">Single Sign-On (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="34982-105">通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="34982-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="34982-106">[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="34982-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="34982-107">**构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="34982-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="34982-108">它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="34982-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="34982-109">有关电子书的信息，请参阅[的第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="34982-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="34982-110">有很多安全问题，需考虑当正在开发云应用程序，但这一系列的情况下，我们将着眼于只是一个： 单一登录。</span><span class="sxs-lookup"><span data-stu-id="34982-110">There are many security issues to think about when you're developing a cloud app, but for this series we'll focus on just one: single sign-on.</span></span> <span data-ttu-id="34982-111">问题人们经常问这是:"我要主要构建应用我的公司; 员工如何托管这些应用在云中，同时让他们能够使用相同的安全模型，我的员工了解它们的运行应用时使用的本地环境中托管的防火墙内？"</span><span class="sxs-lookup"><span data-stu-id="34982-111">A question people often ask is this: "I'm primarily building apps for the employees of my company; how do I host these apps in the cloud and still enable them to use the same security model that my employees know and use in the on-premises environment when they're running apps that are hosted inside the firewall?"</span></span> <span data-ttu-id="34982-112">我们启用此方案的方法之一是名为 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="34982-112">One of the ways we enable this scenario is called Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="34982-113">Azure AD，可使企业业务线 (LOB) 应用程序可通过 Internet，并且它使您能够将这些应用提供给业务合作伙伴。</span><span class="sxs-lookup"><span data-stu-id="34982-113">Azure AD enables you to make enterprise line-of-business (LOB) apps available over the Internet, and it enables you to make these apps available to business partners as well.</span></span>

## <a name="introduction-to-azure-ad"></a><span data-ttu-id="34982-114">Azure AD 简介</span><span class="sxs-lookup"><span data-stu-id="34982-114">Introduction to Azure AD</span></span>

<span data-ttu-id="34982-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/)提供了[Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx)在云中。</span><span class="sxs-lookup"><span data-stu-id="34982-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) provides [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) in the cloud.</span></span> <span data-ttu-id="34982-116">主要功能包括：</span><span class="sxs-lookup"><span data-stu-id="34982-116">Key features include the following:</span></span>

- <span data-ttu-id="34982-117">它与在本地 Active Directory 集成。</span><span class="sxs-lookup"><span data-stu-id="34982-117">It integrates with on-premises Active Directory.</span></span>
- <span data-ttu-id="34982-118">这样，与您的应用程序的单一登录。</span><span class="sxs-lookup"><span data-stu-id="34982-118">It enables single sign-on with your apps.</span></span>
- <span data-ttu-id="34982-119">它支持开放标准，例如[SAML](http://en.wikipedia.org/wiki/SAML_2.0)， [Ws-fed](http://en.wikipedia.org/wiki/WS-Federation)，并[OAuth 2.0](http://oauth.net/2/)。</span><span class="sxs-lookup"><span data-stu-id="34982-119">It supports open standards such as [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-Fed](http://en.wikipedia.org/wiki/WS-Federation), and [OAuth 2.0](http://oauth.net/2/).</span></span>
- <span data-ttu-id="34982-120">它支持企业[Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx)。</span><span class="sxs-lookup"><span data-stu-id="34982-120">It supports Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx).</span></span>

<span data-ttu-id="34982-121">假设您有用于使员工能够登录到 Intranet 应用程序的本地 Windows Server Active Directory 环境：</span><span class="sxs-lookup"><span data-stu-id="34982-121">Suppose you have an on-premises Windows Server Active Directory environment that you use to enable employees to sign on to Intranet apps:</span></span>

![](single-sign-on/_static/image1.png)

<span data-ttu-id="34982-122">什么 Azure AD，您可以执行是在云中创建一个目录。</span><span class="sxs-lookup"><span data-stu-id="34982-122">What Azure AD enables you to do is create a directory in the cloud.</span></span> <span data-ttu-id="34982-123">它是一项免费功能且易于设置。</span><span class="sxs-lookup"><span data-stu-id="34982-123">It's a free feature and easy to set up.</span></span>

<span data-ttu-id="34982-124">它可以是完全独立于你的本地 Active Directory;您可以将任何人都希望在它和 Internet 应用程序进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="34982-124">It can be entirely independent from your on-premises Active Directory; you can put anyone you want in it and authenticate them in Internet apps.</span></span>

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

<span data-ttu-id="34982-126">也可以将它集成与你的本地 AD。</span><span class="sxs-lookup"><span data-stu-id="34982-126">Or you can integrate it with your on-premises AD.</span></span>

![AD 和 WAAD 集成](single-sign-on/_static/image3.png)

<span data-ttu-id="34982-128">现在可以进行本地身份验证的所有雇员可以还进行身份都验证通过 Internet-而无需打开防火墙或者部署你的数据中心中的任何新服务器。</span><span class="sxs-lookup"><span data-stu-id="34982-128">Now all the employees who can authenticate on-premises can also authenticate over the Internet – without you having to open up a firewall or deploy any new servers in your data center.</span></span> <span data-ttu-id="34982-129">您可以继续利用所有现有 Active Directory 环境的了解和使用其目前用于提供有关功能的内部应用单一登录。</span><span class="sxs-lookup"><span data-stu-id="34982-129">You can continue to leverage all the existing Active Directory environment that you know and use today to give your internal apps single-sign on capability.</span></span>

<span data-ttu-id="34982-130">后所做的 AD 和 Azure AD 之间的连接，您还可以启用你的 web 应用和移动设备进行身份验证你的员工在云中，你可以启用第三方应用，例如 Office 365、 SalesForce.com 或 Google 应用以接受你员工的凭据。</span><span class="sxs-lookup"><span data-stu-id="34982-130">Once you've made this connection between AD and Azure AD, you can also enable your web apps and your mobile devices to authenticate your employees in the cloud, and you can enable third-party apps, such as Office 365, SalesForce.com, or Google apps, to accept your employees' credentials.</span></span> <span data-ttu-id="34982-131">如果你使用 Office 365，你在设置了与 Azure AD 由于 Office 365 使用 Azure AD 进行身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="34982-131">If you're using Office 365, you're already set up with Azure AD because Office 365 uses Azure AD for authentication and authorization.</span></span>

![第三方应用](single-sign-on/_static/image4.png)

<span data-ttu-id="34982-133">此方法的优点是的每当你的组织添加或删除用户，或在用户更改密码，则使用你当前使用的本地环境中的同一个进程。</span><span class="sxs-lookup"><span data-stu-id="34982-133">The beauty of this approach is that any time your organization adds or deletes a user, or a user changes a password, you use the same process that you use today in your on-premises environment.</span></span> <span data-ttu-id="34982-134">所有的你的本地 AD 的更改会自动传播到云环境。</span><span class="sxs-lookup"><span data-stu-id="34982-134">All of your on-premises AD changes are automatically propagated to the cloud environment.</span></span>

<span data-ttu-id="34982-135">如果你的公司使用或移动到 Office 365，值得高兴的，则必须自动设置因为 Office 365 使用 Azure AD 进行身份验证的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="34982-135">If your company is using or moving to Office 365, the good news is that you'll have Azure AD set up automatically because Office 365 uses Azure AD for authentication.</span></span> <span data-ttu-id="34982-136">因此，可以轻松地使用自己的应用程序中相同 Office 365 使用的身份验证。</span><span class="sxs-lookup"><span data-stu-id="34982-136">So you can easily use in your own apps the same authentication that Office 365 uses.</span></span>

## <a name="set-up-an-azure-ad-tenant"></a><span data-ttu-id="34982-137">设置 Azure AD 租户</span><span class="sxs-lookup"><span data-stu-id="34982-137">Set up an Azure AD tenant</span></span>

<span data-ttu-id="34982-138">Azure AD 目录称为一个 Azure AD[租户](https://technet.microsoft.com/library/jj573650.aspx)，而且设置租户非常简单。</span><span class="sxs-lookup"><span data-stu-id="34982-138">an Azure AD directory is called an Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx), and setting up a tenant is pretty easy.</span></span> <span data-ttu-id="34982-139">我们将展示如何它通过 Azure 管理门户以阐明这些概念，但当然等其他门户函数还可以执行它通过使用脚本或管理 API。</span><span class="sxs-lookup"><span data-stu-id="34982-139">We'll show you how it's done in the Azure Management Portal in order to illustrate the concepts, but of course like the other portal functions you can also do it by using a script or management API.</span></span>

<span data-ttu-id="34982-140">在管理门户中单击 Active Directory 选项卡。</span><span class="sxs-lookup"><span data-stu-id="34982-140">In the management portal click the Active Directory tab.</span></span>

![在门户中的 WAAD](single-sign-on/_static/image5.png)

<span data-ttu-id="34982-142">自动为你的 Azure 帐户，具有一个 Azure AD 租户，可以单击**添加**页后，可以创建其他目录底部的按钮。</span><span class="sxs-lookup"><span data-stu-id="34982-142">You automatically have one Azure AD tenant for your Azure account, and you can click the **Add** button at the bottom of the page to create additional directories.</span></span> <span data-ttu-id="34982-143">建议一个用于测试环境，另一个用于生产，例如。</span><span class="sxs-lookup"><span data-stu-id="34982-143">You might want one for a test environment and one for production, for example.</span></span> <span data-ttu-id="34982-144">仔细考虑命名新目录。</span><span class="sxs-lookup"><span data-stu-id="34982-144">Think carefully about what you name a new directory.</span></span> <span data-ttu-id="34982-145">如果你使用你的目录的名称以及如何将您再次为其中一个的用户，可能会造成混淆的名称。</span><span class="sxs-lookup"><span data-stu-id="34982-145">If you use your name for the directory and then you use your name again for one of the users, that can be confusing.</span></span>

![添加目录](single-sign-on/_static/image6.png)

<span data-ttu-id="34982-147">该门户的完全支持创建、 删除和管理此环境中的用户。</span><span class="sxs-lookup"><span data-stu-id="34982-147">The portal has full support for creating, deleting, and managing users within this environment.</span></span> <span data-ttu-id="34982-148">例如，若要添加用户转到**用户**选项卡，单击**添加用户**按钮。</span><span class="sxs-lookup"><span data-stu-id="34982-148">For example, to add a user go to the **Users** tab and click the **Add User** button.</span></span>

![添加用户按钮](single-sign-on/_static/image7.png)

![添加用户对话框](single-sign-on/_static/image8.png)

<span data-ttu-id="34982-151">您可以创建仅在此目录中存在的新用户或可以为此目录中或注册的用户或另一个 Azure AD 目录中的用户注册 Microsoft 帐户，为此目录中的用户。</span><span class="sxs-lookup"><span data-stu-id="34982-151">You can create a new user who exists only in this directory, or you can register a Microsoft Account as a user in this directory, or register or a user from another Azure AD directory as a user in this directory.</span></span> <span data-ttu-id="34982-152">（在真实的目录，默认域为 ContosoTest.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="34982-152">(In a real directory, the default domain would be ContosoTest.onmicrosoft.com.</span></span> <span data-ttu-id="34982-153">您还可以使用您自己选择，如 contoso.com 的域。）</span><span class="sxs-lookup"><span data-stu-id="34982-153">You can also use a domain of your own choosing, like contoso.com.)</span></span>

![用户类型](single-sign-on/_static/image9.png)

![添加用户对话框](single-sign-on/_static/image10.png)

<span data-ttu-id="34982-156">可以将用户分配到角色。</span><span class="sxs-lookup"><span data-stu-id="34982-156">You can assign the user to a role.</span></span>

![用户配置文件](single-sign-on/_static/image11.png)

<span data-ttu-id="34982-158">并使用一个临时密码创建帐户。</span><span class="sxs-lookup"><span data-stu-id="34982-158">And the account is created with a temporary password.</span></span>

![临时密码](single-sign-on/_static/image12.png)

<span data-ttu-id="34982-160">这种方式创建的用户立即可以登录到 web 应用使用此云目录。</span><span class="sxs-lookup"><span data-stu-id="34982-160">The users you create this way can immediately log in to your web apps using this cloud directory.</span></span>

<span data-ttu-id="34982-161">什么是适用于企业单一登录，不过，是**目录集成**选项卡：</span><span class="sxs-lookup"><span data-stu-id="34982-161">What's great for enterprise single sign-on, though, is the **Directory Integration** tab:</span></span>

![目录集成选项卡](single-sign-on/_static/image13.png)

<span data-ttu-id="34982-163">如果启用目录集成，并[下载的工具，](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)，可以同步与现有的本地 Active Directory，你已在组织内部使用此云目录。</span><span class="sxs-lookup"><span data-stu-id="34982-163">If you enable directory integration, and [download a tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), you can sync this cloud directory with your existing on-premises Active Directory that you're already using inside your organization.</span></span> <span data-ttu-id="34982-164">然后的所有用户存储在你的目录中将显示在此云目录。</span><span class="sxs-lookup"><span data-stu-id="34982-164">Then all of the users stored in your directory will show up in this cloud directory.</span></span> <span data-ttu-id="34982-165">你的云应用现在可以验证所有员工使用其现有的 Active Directory 凭据。</span><span class="sxs-lookup"><span data-stu-id="34982-165">Your cloud apps can now authenticate all of your employees using their existing Active Directory credentials.</span></span> <span data-ttu-id="34982-166">这是所有免费 – 同步工具和 Azure AD 本身和。</span><span class="sxs-lookup"><span data-stu-id="34982-166">And all this is free – both the sync tool and Azure AD itself.</span></span>

<span data-ttu-id="34982-167">该工具是一个向导，是易于使用，因为这些屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="34982-167">The tool is a wizard that is easy to use, as you can see from these screen shots.</span></span> <span data-ttu-id="34982-168">这些不是完整的说明，只是一个示例显示基本过程。</span><span class="sxs-lookup"><span data-stu-id="34982-168">These are not complete instructions, just an example showing you the basic process.</span></span> <span data-ttu-id="34982-169">更多详细说明-将执行操作的 it 信息，请参阅中的链接[资源](#resources)本章末尾部分。</span><span class="sxs-lookup"><span data-stu-id="34982-169">For more detailed how-to-do-it information, see the links in the [Resources](#resources) section at the end of the chapter.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image14.png)

<span data-ttu-id="34982-171">单击**下一步**，然后输入你的 Azure Active Directory 凭据。</span><span class="sxs-lookup"><span data-stu-id="34982-171">Click **Next**, and then enter your Azure Active Directory credentials.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image15.png)

<span data-ttu-id="34982-173">单击**下一步**，然后输入你的本地 AD 凭据。</span><span class="sxs-lookup"><span data-stu-id="34982-173">Click **Next**, and then enter your on-premises AD credentials.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image16.png)

<span data-ttu-id="34982-175">单击**下一步**，，然后指明你想要在云中存储的 AD 密码哈希值。</span><span class="sxs-lookup"><span data-stu-id="34982-175">Click **Next**, and then indicate if you want to store a hash of your AD passwords in the cloud.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image17.png)

<span data-ttu-id="34982-177">可以在云中存储密码哈希是单向哈希;实际的密码永远不会存储在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="34982-177">The password hash that you can store in the cloud is a one-way hash; actual passwords are never stored in Azure AD.</span></span> <span data-ttu-id="34982-178">如果又决定不将哈希值存储在云中，你必须使用[Active Directory 联合身份验证服务](https://technet.microsoft.com/library/hh831502.aspx)(ADFS)。</span><span class="sxs-lookup"><span data-stu-id="34982-178">If you decide against storing hashes in the cloud, you'll have to use [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span></span> <span data-ttu-id="34982-179">此外，还有[时要考虑其他因素选择是否使用 ADFS](https://technet.microsoft.com/library/jj573653.aspx)。</span><span class="sxs-lookup"><span data-stu-id="34982-179">There are also [other factors to consider when choosing whether or not to use ADFS](https://technet.microsoft.com/library/jj573653.aspx).</span></span> <span data-ttu-id="34982-180">ADFS 选项需要几个其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="34982-180">The ADFS option requires a few additional configuration steps.</span></span>

<span data-ttu-id="34982-181">如果您选择将哈希值存储在云中，完成后，该工具启动时单击同步目录**下一步**。</span><span class="sxs-lookup"><span data-stu-id="34982-181">If you choose to store hashes in the cloud, you're done, and the tool starts synchronizing directories when you click **Next**.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image18.png)

<span data-ttu-id="34982-183">在几分钟内就大功告成了。</span><span class="sxs-lookup"><span data-stu-id="34982-183">And in a few minutes you're done.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image19.png)

<span data-ttu-id="34982-185">只需运行此组织，在 Windows 2003 或更高版本中的一个域控制器上。</span><span class="sxs-lookup"><span data-stu-id="34982-185">You only have to run this on one domain controller in the organization, on Windows 2003 or higher.</span></span> <span data-ttu-id="34982-186">且无需重新启动。</span><span class="sxs-lookup"><span data-stu-id="34982-186">And no need to reboot.</span></span> <span data-ttu-id="34982-187">当完成，你的所有用户都位于云中，可以执行从任何 web 或移动应用程序，使用 SAML、 OAuth 或 WS 联合身份验证的单一登录。</span><span class="sxs-lookup"><span data-stu-id="34982-187">When you're done, all of your users are in the cloud and you can do single sign-on from any web or mobile application, using SAML, OAuth, or WS-Fed.</span></span>

<span data-ttu-id="34982-188">有时我们有人问这是有关如何安全 – 没有 Microsoft 用于它自己的敏感业务数据？</span><span class="sxs-lookup"><span data-stu-id="34982-188">Sometimes we get asked about how secure this is – does Microsoft use it for their own sensitive business data?</span></span> <span data-ttu-id="34982-189">和答案为的是我们执行操作。</span><span class="sxs-lookup"><span data-stu-id="34982-189">And the answer is yes we do.</span></span> <span data-ttu-id="34982-190">例如，如果转到内部 Microsoft SharePoint 站点[ https://microsoft.sharepoint.com/ ](https://microsoft.sharepoint.com/)，会提示登录。</span><span class="sxs-lookup"><span data-stu-id="34982-190">For example, if you go to the internal Microsoft SharePoint site at [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), you get prompted to log in.</span></span>

![Office 365 登录](single-sign-on/_static/image20.png)

<span data-ttu-id="34982-192">Microsoft 已启用 ADFS，因此当您进入 Microsoft ID，您重定向到 ADFS 登录页。</span><span class="sxs-lookup"><span data-stu-id="34982-192">Microsoft has enabled ADFS, so when you enter a Microsoft ID, you get redirected to an ADFS log-in page.</span></span>

![ADFS 登录](single-sign-on/_static/image21.png)

<span data-ttu-id="34982-194">和后输入凭据存储在内部 Microsoft AD 帐户后，您可以访问到此内部应用程序。</span><span class="sxs-lookup"><span data-stu-id="34982-194">And once you enter credentials stored in an internal Microsoft AD account, you have access to this internal application.</span></span>

![MS SharePoint 站点](single-sign-on/_static/image22.png)

<span data-ttu-id="34982-196">主要是因为我们已经有 Azure AD 变得可用，但在云中的 Azure AD 目录正处于登录过程前设置 ADFS，我们将使用 AD 在登录服务器。</span><span class="sxs-lookup"><span data-stu-id="34982-196">We're using an AD sign-in server mainly because we already had ADFS set up before Azure AD became available, but the log-in process is going through an Azure AD directory in the cloud.</span></span> <span data-ttu-id="34982-197">我们将我们的重要文档、 源代码管理、 性能管理文件、 销售报表和详细信息，在云中，并将此确切的同一个解决方案来保护它们。</span><span class="sxs-lookup"><span data-stu-id="34982-197">We put our important documents, source control, performance management files, sales reports, and more, in the cloud and are using this exact same solution to secure them.</span></span>

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a><span data-ttu-id="34982-198">创建使用 Azure AD 进行单一登录的 ASP.NET 应用</span><span class="sxs-lookup"><span data-stu-id="34982-198">Create an ASP.NET app that uses Azure AD for single sign-on</span></span>

<span data-ttu-id="34982-199">Visual Studio 可以十分轻松地创建的应用程序使用 Azure AD 进行单一登录，您可以看到从几个屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="34982-199">Visual Studio makes it really easy to create an app that uses Azure AD for single sign-on, as you can see from a few screen shots.</span></span>

<span data-ttu-id="34982-200">创建一个新 ASP.NET 应用程序，MVC 或 Web 窗体时的默认身份验证方法是 ASP.NET 标识。</span><span class="sxs-lookup"><span data-stu-id="34982-200">When you create a new ASP.NET application, either MVC or Web Forms, the default authentication method is ASP.NET Identity.</span></span> <span data-ttu-id="34982-201">若要更改到 Azure AD，请单击**更改身份验证**按钮。</span><span class="sxs-lookup"><span data-stu-id="34982-201">To change that to Azure AD, you click a **Change Authentication** button.</span></span>

![更改身份验证](single-sign-on/_static/image23.png)

<span data-ttu-id="34982-203">选择组织帐户，输入你的域名，并选择单一登录。</span><span class="sxs-lookup"><span data-stu-id="34982-203">Select Organizational Accounts, enter your domain name, and then select Single Sign On.</span></span>

![配置身份验证对话框](single-sign-on/_static/image24.png)

<span data-ttu-id="34982-205">您可以还授予应用程序读取或读/写权限的目录数据。</span><span class="sxs-lookup"><span data-stu-id="34982-205">You can also give the app read or read/write permission for directory data.</span></span> <span data-ttu-id="34982-206">如果这样做，它可以使用[Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx)若要查找用户的电话号码，了解它们是否在办公室中，当最后一个记录，等等。</span><span class="sxs-lookup"><span data-stu-id="34982-206">If you do that, it can use the [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) to look up users' phone number, find out if they're in the office, when they last logged on, etc.</span></span>

<span data-ttu-id="34982-207">这就是您需要做的所有 Visual Studio 会要求输入凭据的 Azure AD 租户的管理员，然后配置你的项目和新的应用程序在 Azure AD 租户。</span><span class="sxs-lookup"><span data-stu-id="34982-207">That's all you have to do - Visual Studio asks for the credentials for an administrator for your Azure AD tenant, and then it configures both your project and your Azure AD tenant for the new application.</span></span>

<span data-ttu-id="34982-208">运行项目时，你将看到在登录页，并在 Azure AD 目录中可以使用的用户的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="34982-208">When you run the project, you'll see a sign-in page, and you can sign in with credentials of a user in your Azure AD directory.</span></span>

![组织帐户登录](single-sign-on/_static/image25.png)

![登录](single-sign-on/_static/image26.png)

<span data-ttu-id="34982-211">当应用部署到 Azure 时，只需是选择**启用组织身份验证**复选框，然后再一次 Visual Studio 负责为您的所有配置。</span><span class="sxs-lookup"><span data-stu-id="34982-211">When you deploy the app to Azure, all you have to do is select an **Enable Organizational Authentication** check box, and once again Visual Studio takes care of all the configuration for you.</span></span>

![发布 Web](single-sign-on/_static/image27.png)

<span data-ttu-id="34982-213">这些屏幕截图来自演示了如何生成使用 Azure AD 身份验证的应用程序的完整分步教程：[与 Azure Active Directory 开发 ASP.NET 应用程序](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="34982-213">These screen shots come from a complete step-by-step tutorial that shows how to build an app that uses Azure AD authentication: [Developing ASP.NET Apps with Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span></span>

## <a name="summary"></a><span data-ttu-id="34982-214">总结</span><span class="sxs-lookup"><span data-stu-id="34982-214">Summary</span></span>

<span data-ttu-id="34982-215">这一章中您可以看到，Azure Active Directory、 Visual Studio 和 ASP.NET，使其易于设置组织的用户的 Internet 应用程序中的单一登录。</span><span class="sxs-lookup"><span data-stu-id="34982-215">In this chapter you saw that Azure Active Directory, Visual Studio, and ASP.NET, make it easy to set up single sign-on in Internet applications for your organization's users.</span></span> <span data-ttu-id="34982-216">你的用户可以使用他们用于登录在您的内部网络中使用 Active Directory 的相同凭据的 Internet 应用程序中登录。</span><span class="sxs-lookup"><span data-stu-id="34982-216">Your users can sign on in Internet apps using the same credentials they use to sign on using Active Directory in your internal network.</span></span>

<span data-ttu-id="34982-217">[接下来的章节](data-storage-options.md)查看可用于云应用程序的数据存储选项。</span><span class="sxs-lookup"><span data-stu-id="34982-217">The [next chapter](data-storage-options.md) looks at the data storage options available for a cloud app.</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="34982-218">资源</span><span class="sxs-lookup"><span data-stu-id="34982-218">Resources</span></span>

<span data-ttu-id="34982-219">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="34982-219">For more information, see the following resources:</span></span>

- <span data-ttu-id="34982-220">[Azure Active Directory 文档](https://docs.microsoft.com/azure/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="34982-220">[Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="34982-221">Windowsazure.com 站点上的 Azure AD 文档的门户页。</span><span class="sxs-lookup"><span data-stu-id="34982-221">Portal page for Azure AD documentation on the windowsazure.com site.</span></span> <span data-ttu-id="34982-222">有关分步教程，请参阅**开发**部分。</span><span class="sxs-lookup"><span data-stu-id="34982-222">For step by step tutorials, see the **Develop** section.</span></span>
- <span data-ttu-id="34982-223">[Azure 多重身份验证](https://docs.microsoft.com/azure/multi-factor-authentication/)。</span><span class="sxs-lookup"><span data-stu-id="34982-223">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/).</span></span> <span data-ttu-id="34982-224">有关在 Azure 中的多重身份验证的文档的门户页。</span><span class="sxs-lookup"><span data-stu-id="34982-224">Portal page for documentation about multi-factor authentication in Azure.</span></span>
- <span data-ttu-id="34982-225">[组织帐户身份验证选项](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)。</span><span class="sxs-lookup"><span data-stu-id="34982-225">[Organizational account authentication options](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions).</span></span> <span data-ttu-id="34982-226">在 Visual Studio 2013 新项目对话框中的 Azure AD 身份验证选项的说明。</span><span class="sxs-lookup"><span data-stu-id="34982-226">Explanation of the Azure AD authentication options in the Visual Studio 2013 new-project dialog.</span></span>
- <span data-ttu-id="34982-227">[Microsoft 模式和实践-联合身份模式](https://msdn.microsoft.com/library/dn589790.aspx)。</span><span class="sxs-lookup"><span data-stu-id="34982-227">[Microsoft Patterns and Practices - Federated Identity Pattern](https://msdn.microsoft.com/library/dn589790.aspx).</span></span>
- <span data-ttu-id="34982-228">[如何： 安装 Azure Active Directory Sync 工具](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)。</span><span class="sxs-lookup"><span data-stu-id="34982-228">[HowTo: Install the Azure Active Directory Sync Tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span></span>
- <span data-ttu-id="34982-229">[Active Directory 联合身份验证服务 2.0 内容导航图](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)。</span><span class="sxs-lookup"><span data-stu-id="34982-229">[Active Directory Federation Services 2.0 Content Map](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span></span> <span data-ttu-id="34982-230">链接到有关 ADFS 2.0 的文档。</span><span class="sxs-lookup"><span data-stu-id="34982-230">Links to documentation about ADFS 2.0.</span></span>
- <span data-ttu-id="34982-231">[Windows Azure AD 应用程序中基于角色的和基于 ACL 的授权](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)。</span><span class="sxs-lookup"><span data-stu-id="34982-231">[Role-Based and ACL-Based Authorization in a Windows Azure AD Application](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span></span> <span data-ttu-id="34982-232">示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="34982-232">Sample application.</span></span>
- <span data-ttu-id="34982-233">[Azure Active Directory 图形 API 博客](https://blogs.msdn.com/b/aadgraphteam/)。</span><span class="sxs-lookup"><span data-stu-id="34982-233">[Azure Active Directory Graph API blog](https://blogs.msdn.com/b/aadgraphteam/).</span></span>
- <span data-ttu-id="34982-234">[访问控制在 BYOD 和混合标识基础结构中的目录集成](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)。</span><span class="sxs-lookup"><span data-stu-id="34982-234">[Access Control in BYOD and Directory Integration in a Hybrid Identity Infrastructure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span></span> <span data-ttu-id="34982-235">Tech Ed 2014 会话视频通过 Gayana Bagdasaryan。</span><span class="sxs-lookup"><span data-stu-id="34982-235">Tech Ed 2014 session video by Gayana Bagdasaryan.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="34982-236">[上一页](web-development-best-practices.md)
> [下一页](data-storage-options.md)</span><span class="sxs-lookup"><span data-stu-id="34982-236">[Previous](web-development-best-practices.md)
[Next](data-storage-options.md)</span></span>
