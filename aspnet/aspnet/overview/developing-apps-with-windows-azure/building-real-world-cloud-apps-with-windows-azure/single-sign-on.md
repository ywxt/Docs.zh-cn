---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: 单一登录 （使用 Azure 构建真实世界云应用） |Microsoft 文档
author: MikeWasson
description: 构建真实世界云应用程序与 Azure 的电子书基于由 Scott Guthrie 的演示。 它还说明了 13 模式和实践，他可以...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 82f2f99154d94074b03d580a0f491053d6f53bde
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="2bb5b-104">单一登录 （使用 Azure 构建真实世界云应用）</span><span class="sxs-lookup"><span data-stu-id="2bb5b-104">Single Sign-On (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="2bb5b-105">通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="2bb5b-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="2bb5b-106">[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="2bb5b-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="2bb5b-107">**构建真实世界云应用程序与 Azure**电子书基于由 Scott Guthrie 的演示。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="2bb5b-108">它还说明了 13 模式和实践，从而帮助你为成功开发适用于云中的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="2bb5b-109">有关电子书的信息，请参阅[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="2bb5b-110">有很多安全问题，可考虑时，你要开发云应用程序，但这一系列我们将重点仅仅一个： 单一登录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-110">There are many security issues to think about when you're developing a cloud app, but for this series we'll focus on just one: single sign-on.</span></span> <span data-ttu-id="2bb5b-111">问题人经常询问的这是:"我要主要构建应用的我的公司; 员工如何承载这些应用程序在云中并仍使其能够使用相同的安全模型，我的员工知道它们正在运行应用程序时，在本地环境中使用托管防火墙内部？"</span><span class="sxs-lookup"><span data-stu-id="2bb5b-111">A question people often ask is this: "I'm primarily building apps for the employees of my company; how do I host these apps in the cloud and still enable them to use the same security model that my employees know and use in the on-premises environment when they're running apps that are hosted inside the firewall?"</span></span> <span data-ttu-id="2bb5b-112">一种我们启用此方案的称为 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-112">One of the ways we enable this scenario is called Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="2bb5b-113">Azure AD，可使企业业务线 (LOB) 应用可通过 Internet，并且它使您能够为业务合作伙伴也提供这些应用。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-113">Azure AD enables you to make enterprise line-of-business (LOB) apps available over the Internet, and it enables you to make these apps available to business partners as well.</span></span>

## <a name="introduction-to-azure-ad"></a><span data-ttu-id="2bb5b-114">Azure AD 简介</span><span class="sxs-lookup"><span data-stu-id="2bb5b-114">Introduction to Azure AD</span></span>

<span data-ttu-id="2bb5b-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/)提供[Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx)在云中。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) provides [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) in the cloud.</span></span> <span data-ttu-id="2bb5b-116">主要功能包括：</span><span class="sxs-lookup"><span data-stu-id="2bb5b-116">Key features include the following:</span></span>

- <span data-ttu-id="2bb5b-117">它与本地 Active Directory 集成。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-117">It integrates with on-premises Active Directory.</span></span>
- <span data-ttu-id="2bb5b-118">它使与你的应用程序的单一登录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-118">It enables single sign-on with your apps.</span></span>
- <span data-ttu-id="2bb5b-119">它支持开放标准，如[SAML](http://en.wikipedia.org/wiki/SAML_2.0)，[的是 Ws-fed](http://en.wikipedia.org/wiki/WS-Federation)，和[OAuth 2.0](http://oauth.net/2/)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-119">It supports open standards such as [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-Fed](http://en.wikipedia.org/wiki/WS-Federation), and [OAuth 2.0](http://oauth.net/2/).</span></span>
- <span data-ttu-id="2bb5b-120">它支持企业[Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-120">It supports Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx).</span></span>

<span data-ttu-id="2bb5b-121">假设你有使用以使员工能够登录到 Intranet 应用程序的本地 Windows Server Active Directory 环境：</span><span class="sxs-lookup"><span data-stu-id="2bb5b-121">Suppose you have an on-premises Windows Server Active Directory environment that you use to enable employees to sign on to Intranet apps:</span></span>

![](single-sign-on/_static/image1.png)

<span data-ttu-id="2bb5b-122">新增功能 Azure AD，您可以执行是在云中创建一个目录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-122">What Azure AD enables you to do is create a directory in the cloud.</span></span> <span data-ttu-id="2bb5b-123">它是免费功能且易于设置。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-123">It's a free feature and easy to set up.</span></span>

<span data-ttu-id="2bb5b-124">它可以是完全独立于你的本地 Active Directory;你可以放置任何人都想在其中和 Internet 应用程序进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-124">It can be entirely independent from your on-premises Active Directory; you can put anyone you want in it and authenticate them in Internet apps.</span></span>

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

<span data-ttu-id="2bb5b-126">也可以将它与你在本地 AD。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-126">Or you can integrate it with your on-premises AD.</span></span>

![AD 和 WAAD 集成](single-sign-on/_static/image3.png)

<span data-ttu-id="2bb5b-128">现在可以进行本地身份验证的所有员工可以还进行身份都验证通过 Internet – 您无需打开防火墙或部署你的数据中心中的任何新服务器。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-128">Now all the employees who can authenticate on-premises can also authenticate over the Internet – without you having to open up a firewall or deploy any new servers in your data center.</span></span> <span data-ttu-id="2bb5b-129">你可以继续利用所有现有 Active Directory 环境，您了解并使用其目前用于提供有关功能的内部应用单一登录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-129">You can continue to leverage all the existing Active Directory environment that you know and use today to give your internal apps single-sign on capability.</span></span>

<span data-ttu-id="2bb5b-130">一旦你所做此 AD 与 Azure AD 之间的连接，你还可以启用你的 web 应用和移动设备进行身份验证你的员工在云中，并且你可以启用第三方应用程序，如 Office 365、 SalesForce.com 或 Google 应用，以接受你员工的凭据。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-130">Once you've made this connection between AD and Azure AD, you can also enable your web apps and your mobile devices to authenticate your employees in the cloud, and you can enable third-party apps, such as Office 365, SalesForce.com, or Google apps, to accept your employees' credentials.</span></span> <span data-ttu-id="2bb5b-131">如果你使用 Office 365，你在已设置与 Azure AD 因为 Office 365 使用 Azure AD 进行身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-131">If you're using Office 365, you're already set up with Azure AD because Office 365 uses Azure AD for authentication and authorization.</span></span>

![第三方应用程序](single-sign-on/_static/image4.png)

<span data-ttu-id="2bb5b-133">此方法的优点是的只要你的组织将添加或删除用户，或者用户更改密码，则使用在你的本地环境中现在使用的相同流程。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-133">The beauty of this approach is that any time your organization adds or deletes a user, or a user changes a password, you use the same process that you use today in your on-premises environment.</span></span> <span data-ttu-id="2bb5b-134">所有的本地 AD 更改会自动传播到云环境。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-134">All of your on-premises AD changes are automatically propagated to the cloud environment.</span></span>

<span data-ttu-id="2bb5b-135">如果使用或移动到 Office 365 好消息你的公司，必须自动设置因为 Office 365 使用 Azure AD 进行身份验证的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-135">If your company is using or moving to Office 365, the good news is that you'll have Azure AD set up automatically because Office 365 uses Azure AD for authentication.</span></span> <span data-ttu-id="2bb5b-136">因此你可以轻松地使用你自己的应用程序中的 Office 365 使用的相同身份验证。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-136">So you can easily use in your own apps the same authentication that Office 365 uses.</span></span>

## <a name="set-up-an-azure-ad-tenant"></a><span data-ttu-id="2bb5b-137">设置 Azure AD 租户</span><span class="sxs-lookup"><span data-stu-id="2bb5b-137">Set up an Azure AD tenant</span></span>

<span data-ttu-id="2bb5b-138">Azure AD 目录调用 Azure AD[租户](https://technet.microsoft.com/library/jj573650.aspx)，而且设置租户非常简单。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-138">an Azure AD directory is called an Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx), and setting up a tenant is pretty easy.</span></span> <span data-ttu-id="2bb5b-139">我们将介绍您如何它为了在 Azure 管理门户中阐释的概念，但这是当然的与其他门户函数类似你还可以执行它通过使用脚本或管理 API。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-139">We'll show you how it's done in the Azure Management Portal in order to illustrate the concepts, but of course like the other portal functions you can also do it by using a script or management API.</span></span>

<span data-ttu-id="2bb5b-140">在管理门户中单击 Active Directory 选项卡。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-140">In the management portal click the Active Directory tab.</span></span>

![在门户中的 WAAD](single-sign-on/_static/image5.png)

<span data-ttu-id="2bb5b-142">自动为你的 Azure 帐户，拥有一个 Azure AD 租户，可以单击**添加**页后，可以创建其他目录底部的按钮。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-142">You automatically have one Azure AD tenant for your Azure account, and you can click the **Add** button at the bottom of the page to create additional directories.</span></span> <span data-ttu-id="2bb5b-143">需要一个用于测试环境，一个用于生产，例如。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-143">You might want one for a test environment and one for production, for example.</span></span> <span data-ttu-id="2bb5b-144">请仔细考虑有关命名新目录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-144">Think carefully about what you name a new directory.</span></span> <span data-ttu-id="2bb5b-145">如果你使用你目录的名称，然后你使用你再次对其中一个名称的用户，可能容易引起混淆。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-145">If you use your name for the directory and then you use your name again for one of the users, that can be confusing.</span></span>

![添加目录](single-sign-on/_static/image6.png)

<span data-ttu-id="2bb5b-147">门户具有用于创建、 删除和管理此环境中的用户的完整支持。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-147">The portal has full support for creating, deleting, and managing users within this environment.</span></span> <span data-ttu-id="2bb5b-148">例如，若要添加用户转到**用户**选项卡，单击**添加用户**按钮。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-148">For example, to add a user go to the **Users** tab and click the **Add User** button.</span></span>

![添加用户按钮](single-sign-on/_static/image7.png)

![添加用户对话框](single-sign-on/_static/image8.png)

<span data-ttu-id="2bb5b-151">你可以创建仅在此目录中存在的新用户，或可以为此目录中的用户作为此目录中或注册中的用户或用户从另一个 Azure AD 目录中注册 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-151">You can create a new user who exists only in this directory, or you can register a Microsoft Account as a user in this directory, or register or a user from another Azure AD directory as a user in this directory.</span></span> <span data-ttu-id="2bb5b-152">（在真实的目录，默认域为 ContosoTest.onmicrosoft.com。你还可以使用你自己选择，如 contoso.com 的域。）</span><span class="sxs-lookup"><span data-stu-id="2bb5b-152">(In a real directory, the default domain would be ContosoTest.onmicrosoft.com. You can also use a domain of your own choosing, like contoso.com.)</span></span>

![用户类型](single-sign-on/_static/image9.png)

![添加用户对话框](single-sign-on/_static/image10.png)

<span data-ttu-id="2bb5b-155">你可以为用户分配角色。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-155">You can assign the user to a role.</span></span>

![用户配置文件](single-sign-on/_static/image11.png)

<span data-ttu-id="2bb5b-157">并使用一个临时密码创建帐户。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-157">And the account is created with a temporary password.</span></span>

![临时密码](single-sign-on/_static/image12.png)

<span data-ttu-id="2bb5b-159">以此方式创建的用户立即可以登录到你的 web 应用使用此云目录所造成。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-159">The users you create this way can immediately log in to your web apps using this cloud directory.</span></span>

<span data-ttu-id="2bb5b-160">什么是非常适合企业单一登录，不过，是**目录集成**选项卡：</span><span class="sxs-lookup"><span data-stu-id="2bb5b-160">What's great for enterprise single sign-on, though, is the **Directory Integration** tab:</span></span>

![目录集成选项卡](single-sign-on/_static/image13.png)

<span data-ttu-id="2bb5b-162">如果你启用目录集成和[下载的工具，](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)，你可以同步与你现有的本地 Active Directory，你已在组织内部使用此云目录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-162">If you enable directory integration, and [download a tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), you can sync this cloud directory with your existing on-premises Active Directory that you're already using inside your organization.</span></span> <span data-ttu-id="2bb5b-163">然后所有存储在你的目录中的用户将显示在此云目录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-163">Then all of the users stored in your directory will show up in this cloud directory.</span></span> <span data-ttu-id="2bb5b-164">你的云应用现在可以验证所有员工使用其现有的 Active Directory 凭据。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-164">Your cloud apps can now authenticate all of your employees using their existing Active Directory credentials.</span></span> <span data-ttu-id="2bb5b-165">以及所有这些操作的可用 – 同步工具和 Azure AD 本身。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-165">And all this is free – both the sync tool and Azure AD itself.</span></span>

<span data-ttu-id="2bb5b-166">该工具是一个是易于使用，可从这些屏幕截图中看到的向导。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-166">The tool is a wizard that is easy to use, as you can see from these screen shots.</span></span> <span data-ttu-id="2bb5b-167">这些不是完整的说明，只是一个示例显示基本过程。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-167">These are not complete instructions, just an example showing you the basic process.</span></span> <span data-ttu-id="2bb5b-168">有关更详细操作方法-到-执行-it 信息，请参阅中的链接[资源](#resources)章结尾部分。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-168">For more detailed how-to-do-it information, see the links in the [Resources](#resources) section at the end of the chapter.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image14.png)

<span data-ttu-id="2bb5b-170">单击**下一步**，然后输入你的 Azure Active Directory 凭据。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-170">Click **Next**, and then enter your Azure Active Directory credentials.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image15.png)

<span data-ttu-id="2bb5b-172">单击**下一步**，然后输入你的本地 AD 凭据。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-172">Click **Next**, and then enter your on-premises AD credentials.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image16.png)

<span data-ttu-id="2bb5b-174">单击**下一步**，然后表示如果你想要在云中存储的 AD 密码哈希值。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-174">Click **Next**, and then indicate if you want to store a hash of your AD passwords in the cloud.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image17.png)

<span data-ttu-id="2bb5b-176">你可以在云中存储密码哈希是单向哈希;实际密码永远不会存储在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-176">The password hash that you can store in the cloud is a one-way hash; actual passwords are never stored in Azure AD.</span></span> <span data-ttu-id="2bb5b-177">如果你决定对在云中存储哈希，你将需要使用[Active Directory 联合身份验证服务](https://technet.microsoft.com/library/hh831502.aspx)(ADFS)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-177">If you decide against storing hashes in the cloud, you'll have to use [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span></span> <span data-ttu-id="2bb5b-178">也有[其他因素时，应考虑选择是否使用 ADFS](https://technet.microsoft.com/library/jj573653.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-178">There are also [other factors to consider when choosing whether or not to use ADFS](https://technet.microsoft.com/library/jj573653.aspx).</span></span> <span data-ttu-id="2bb5b-179">ADFS 选项需要几个其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-179">The ADFS option requires a few additional configuration steps.</span></span>

<span data-ttu-id="2bb5b-180">如果您选择将哈希存储在云中，完毕后，此工具将启动同步目录，单击时**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-180">If you choose to store hashes in the cloud, you're done, and the tool starts synchronizing directories when you click **Next**.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image18.png)

<span data-ttu-id="2bb5b-182">并在几分钟内已完成。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-182">And in a few minutes you're done.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image19.png)

<span data-ttu-id="2bb5b-184">只需在组织中在 Windows 2003 或更高版本的一个域控制器上运行此。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-184">You only have to run this on one domain controller in the organization, on Windows 2003 or higher.</span></span> <span data-ttu-id="2bb5b-185">而无需重新启动。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-185">And no need to reboot.</span></span> <span data-ttu-id="2bb5b-186">当完毕后，你的所有用户都位于云中，你可以从任何 web 或移动应用程序，使用 SAML、 OAuth、 或的是 Ws-fed 的单一登录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-186">When you're done, all of your users are in the cloud and you can do single sign-on from any web or mobile application, using SAML, OAuth, or WS-Fed.</span></span>

<span data-ttu-id="2bb5b-187">有时我们获取要求这是有关如何安全 – Microsoft 使用它自己敏感业务数据？</span><span class="sxs-lookup"><span data-stu-id="2bb5b-187">Sometimes we get asked about how secure this is – does Microsoft use it for their own sensitive business data?</span></span> <span data-ttu-id="2bb5b-188">和问题的回答是是执行操作。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-188">And the answer is yes we do.</span></span> <span data-ttu-id="2bb5b-189">例如，如果你转到内部 Microsoft SharePoint 站点在[ https://microsoft.sharepoint.com/ ](https://microsoft.sharepoint.com/)，你让系统提示你登录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-189">For example, if you go to the internal Microsoft SharePoint site at [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), you get prompted to log in.</span></span>

![Office 365 登录](single-sign-on/_static/image20.png)

<span data-ttu-id="2bb5b-191">Microsoft 已启用 ADFS，因此当你输入 Microsoft ID，你获取重定向到 ADFS 登录页。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-191">Microsoft has enabled ADFS, so when you enter a Microsoft ID, you get redirected to an ADFS log-in page.</span></span>

![ADFS 登录](single-sign-on/_static/image21.png)

<span data-ttu-id="2bb5b-193">和后输入存储在内部 Microsoft AD 帐户的凭据后，你有权访问此内部应用程序。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-193">And once you enter credentials stored in an internal Microsoft AD account, you have access to this internal application.</span></span>

![MS SharePoint 站点](single-sign-on/_static/image22.png)

<span data-ttu-id="2bb5b-195">主要是因为我们已经有 ADFS 设置 Azure AD 变为可用，但登录过程将通过在云中的 Azure AD 目录之前，我们将使用 AD 在登录服务器。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-195">We're using an AD sign-in server mainly because we already had ADFS set up before Azure AD became available, but the log-in process is going through an Azure AD directory in the cloud.</span></span> <span data-ttu-id="2bb5b-196">我们将我们重要文档、 源代码管理、 性能管理文件、 销售报表、 和的详细信息，在云中，并且要使用此确切的同一个解决方案来确保它们的安全。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-196">We put our important documents, source control, performance management files, sales reports, and more, in the cloud and are using this exact same solution to secure them.</span></span>

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a><span data-ttu-id="2bb5b-197">创建一个 ASP.NET 应用程序使用 Azure AD 进行单一登录</span><span class="sxs-lookup"><span data-stu-id="2bb5b-197">Create an ASP.NET app that uses Azure AD for single sign-on</span></span>

<span data-ttu-id="2bb5b-198">Visual Studio 使极为简便地创建应用程序使用 Azure AD 进行单一登录，你可从几个屏幕截图中看到。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-198">Visual Studio makes it really easy to create an app that uses Azure AD for single sign-on, as you can see from a few screen shots.</span></span>

<span data-ttu-id="2bb5b-199">当你创建一个新的 ASP.NET 应用，MVC 或 Web 窗体的默认身份验证方法是 ASP.NET 标识。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-199">When you create a new ASP.NET application, either MVC or Web Forms, the default authentication method is ASP.NET Identity.</span></span> <span data-ttu-id="2bb5b-200">若要将程序更改为 Azure AD，请单击**更改身份验证**按钮。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-200">To change that to Azure AD, you click a **Change Authentication** button.</span></span>

![更改身份验证](single-sign-on/_static/image23.png)

<span data-ttu-id="2bb5b-202">选择组织帐户，输入你的域名，然后选择单一登录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-202">Select Organizational Accounts, enter your domain name, and then select Single Sign On.</span></span>

![配置身份验证对话框](single-sign-on/_static/image24.png)

<span data-ttu-id="2bb5b-204">也可以提供应用程序读取或读/写目录数据的权限。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-204">You can also give the app read or read/write permission for directory data.</span></span> <span data-ttu-id="2bb5b-205">如果你这样做，它可以使用[Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx)若要查找用户的电话号码，了解它们是否在办公室中，当最后一个记录，等等。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-205">If you do that, it can use the [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) to look up users' phone number, find out if they're in the office, when they last logged on, etc.</span></span>

<span data-ttu-id="2bb5b-206">这就是你所要做的所有 Visual Studio 会要求提供的凭据为你的 Azure AD 租户的管理员，然后配置你的项目和 Azure AD 租户的新应用程序。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-206">That's all you have to do - Visual Studio asks for the credentials for an administrator for your Azure AD tenant, and then it configures both your project and your Azure AD tenant for the new application.</span></span>

<span data-ttu-id="2bb5b-207">运行项目时，你将看到在登录页面，并在你的 Azure AD 目录中可以使用的用户凭据登录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-207">When you run the project, you'll see a sign-in page, and you can sign in with credentials of a user in your Azure AD directory.</span></span>

![组织帐户登录](single-sign-on/_static/image25.png)

![登录](single-sign-on/_static/image26.png)

<span data-ttu-id="2bb5b-210">将应用程序部署到 Azure 时，所要做时，选择**启用组织身份验证**复选框，然后再一次 Visual Studio 将负责为你的所有配置。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-210">When you deploy the app to Azure, all you have to do is select an **Enable Organizational Authentication** check box, and once again Visual Studio takes care of all the configuration for you.</span></span>

![发布网站](single-sign-on/_static/image27.png)

<span data-ttu-id="2bb5b-212">这些屏幕截图来自演示如何生成使用 Azure AD 身份验证的应用程序的完整分步教程：[开发的 ASP.NET 应用程序与 Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-212">These screen shots come from a complete step-by-step tutorial that shows how to build an app that uses Azure AD authentication: [Developing ASP.NET Apps with Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span></span>

## <a name="summary"></a><span data-ttu-id="2bb5b-213">总结</span><span class="sxs-lookup"><span data-stu-id="2bb5b-213">Summary</span></span>

<span data-ttu-id="2bb5b-214">在本章你了解 Azure Active Directory、 Visual Studio 和 ASP.NET，使其容易安装在你组织的用户的 Internet 应用程序中的单一登录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-214">In this chapter you saw that Azure Active Directory, Visual Studio, and ASP.NET, make it easy to set up single sign-on in Internet applications for your organization's users.</span></span> <span data-ttu-id="2bb5b-215">你的用户可在 Internet 应用程序使用他们用于登录在内部网络中使用 Active Directory 的相同凭据登录。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-215">Your users can sign on in Internet apps using the same credentials they use to sign on using Active Directory in your internal network.</span></span>

<span data-ttu-id="2bb5b-216">[下一章](data-storage-options.md)考察可用于云应用程序的数据存储选项。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-216">The [next chapter](data-storage-options.md) looks at the data storage options available for a cloud app.</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="2bb5b-217">资源</span><span class="sxs-lookup"><span data-stu-id="2bb5b-217">Resources</span></span>

<span data-ttu-id="2bb5b-218">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="2bb5b-218">For more information, see the following resources:</span></span>

- <span data-ttu-id="2bb5b-219">[Azure Active Directory 文档](https://docs.microsoft.com/azure/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-219">[Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="2bb5b-220">有关 windowsazure.com 站点上的 Azure AD 文档门户页面。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-220">Portal page for Azure AD documentation on the windowsazure.com site.</span></span> <span data-ttu-id="2bb5b-221">分步教程，请参阅**开发**部分。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-221">For step by step tutorials, see the **Develop** section.</span></span>
- <span data-ttu-id="2bb5b-222">[Azure 多因素身份验证](https://docs.microsoft.com/azure/multi-factor-authentication/)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-222">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/).</span></span> <span data-ttu-id="2bb5b-223">有关在 Azure 中的多因素身份验证的文档的门户页。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-223">Portal page for documentation about multi-factor authentication in Azure.</span></span>
- <span data-ttu-id="2bb5b-224">[组织帐户身份验证选项](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-224">[Organizational account authentication options](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions).</span></span> <span data-ttu-id="2bb5b-225">在 Visual Studio 2013 新项目对话框中的 Azure AD 身份验证选项的说明。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-225">Explanation of the Azure AD authentication options in the Visual Studio 2013 new-project dialog.</span></span>
- <span data-ttu-id="2bb5b-226">[Microsoft 模式和实践-联合标识模式](https://msdn.microsoft.com/library/dn589790.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-226">[Microsoft Patterns and Practices - Federated Identity Pattern](https://msdn.microsoft.com/library/dn589790.aspx).</span></span>
- <span data-ttu-id="2bb5b-227">[如何： 安装 Azure Active Directory 同步工具](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-227">[HowTo: Install the Azure Active Directory Sync Tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span></span>
- <span data-ttu-id="2bb5b-228">[Active Directory 联合身份验证服务 2.0 内容导航图](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-228">[Active Directory Federation Services 2.0 Content Map](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span></span> <span data-ttu-id="2bb5b-229">链接到有关 ADFS 2.0 的文档。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-229">Links to documentation about ADFS 2.0.</span></span>
- <span data-ttu-id="2bb5b-230">[Windows Azure AD 应用程序中基于角色的和基于 ACL 的授权](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-230">[Role-Based and ACL-Based Authorization in a Windows Azure AD Application](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span></span> <span data-ttu-id="2bb5b-231">示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-231">Sample application.</span></span>
- <span data-ttu-id="2bb5b-232">[Azure Active Directory Graph API 博客](https://blogs.msdn.com/b/aadgraphteam/)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-232">[Azure Active Directory Graph API blog](https://blogs.msdn.com/b/aadgraphteam/).</span></span>
- <span data-ttu-id="2bb5b-233">[访问控制中 BYOD 和混合标识基础结构中的目录集成](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-233">[Access Control in BYOD and Directory Integration in a Hybrid Identity Infrastructure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span></span> <span data-ttu-id="2bb5b-234">技术 Ed 2014 会话视频通过 Gayana Bagdasaryan。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-234">Tech Ed 2014 session video by Gayana Bagdasaryan.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2bb5b-235">[上一页](web-development-best-practices.md)
> [下一页](data-storage-options.md)</span><span class="sxs-lookup"><span data-stu-id="2bb5b-235">[Previous](web-development-best-practices.md)
[Next](data-storage-options.md)</span></span>
