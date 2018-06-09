---
uid: identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
title: 用于将密码和其他敏感数据部署到 ASP.NET 和 Azure App Service 的最佳做法 |Microsoft 文档
author: Rick-Anderson
description: 本教程演示如何在代码可以安全地存储和访问安全信息。 最重要的一点是你应永远不会存储密码或其他服务...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/21/2015
ms.topic: article
ms.assetid: 97902c66-cb61-4d11-be52-73f962f2db0a
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
msc.type: authoredcontent
ms.openlocfilehash: 995d9a088e3095f36a01d2adb19ec08e6a6d1b3e
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "28033016"
---
<a name="best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure-app-service"></a><span data-ttu-id="d56db-104">密码和其他敏感数据部署到 ASP.NET 和 Azure App Service 的最佳做法</span><span class="sxs-lookup"><span data-stu-id="d56db-104">Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service</span></span>
====================
<span data-ttu-id="d56db-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="d56db-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="d56db-106">本教程演示如何在代码可以安全地存储和访问安全信息。</span><span class="sxs-lookup"><span data-stu-id="d56db-106">This tutorial shows how your code can securely store and access secure information.</span></span> <span data-ttu-id="d56db-107">最重要的一点是你应永远不会将密码或其他敏感数据存储在源代码中，且你不应在开发和测试模式下使用生产机密。</span><span class="sxs-lookup"><span data-stu-id="d56db-107">The most important point is you should never store passwords or other sensitive data in source code, and you shouldn't use production secrets in development and test mode.</span></span>
> 
> <span data-ttu-id="d56db-108">示例代码是一个简单的 web 作业控制台应用程序和需要访问数据库连接字符串密码，Twilio，Google 和 SendGrid 安全密钥的 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="d56db-108">The sample code is a simple WebJob console app and a ASP.NET MVC app that needs access to a database connection string password, Twilio, Google and SendGrid secure keys.</span></span>
> 
> <span data-ttu-id="d56db-109">在本地设置和 PHP 还提到。</span><span class="sxs-lookup"><span data-stu-id="d56db-109">On premise settings and PHP is also mentioned.</span></span>


- [<span data-ttu-id="d56db-110">使用在开发环境中的密码</span><span class="sxs-lookup"><span data-stu-id="d56db-110">Working with passwords in the development environment</span></span>](#pwd)
- [<span data-ttu-id="d56db-111">处理在开发环境中的连接字符串</span><span class="sxs-lookup"><span data-stu-id="d56db-111">Working with connection strings in the development environment</span></span>](#con)
- [<span data-ttu-id="d56db-112">Web 作业的控制台应用</span><span class="sxs-lookup"><span data-stu-id="d56db-112">WebJobs console apps</span></span>](#wj)
- [<span data-ttu-id="d56db-113">部署到 Azure 的机密</span><span class="sxs-lookup"><span data-stu-id="d56db-113">Deploying secrets to Azure</span></span>](#da)
- [<span data-ttu-id="d56db-114">本地和 PHP 说明</span><span class="sxs-lookup"><span data-stu-id="d56db-114">Notes for On-Premise and PHP</span></span>](#not)
- [<span data-ttu-id="d56db-115">其他资源</span><span class="sxs-lookup"><span data-stu-id="d56db-115">Additional Resources</span></span>](#addRes)

<a id="pwd"></a>
## <a name="working-with-passwords-in-the-development-environment"></a><span data-ttu-id="d56db-116">使用在开发环境中的密码</span><span class="sxs-lookup"><span data-stu-id="d56db-116">Working with passwords in the development environment</span></span>

<span data-ttu-id="d56db-117">教程经常显示敏感数据源的代码中，希望应永远不会将敏感数据存储在源代码中需要注意。</span><span class="sxs-lookup"><span data-stu-id="d56db-117">Tutorials frequently show sensitive data in source code, hopefully with a caveat that you should never store sensitive data in source code.</span></span> <span data-ttu-id="d56db-118">例如，我[ASP.NET MVC 5 应用程序与 SMS 和电子邮件 2FA](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)教程演示中的以下*web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="d56db-118">For example, my [ASP.NET MVC 5 app with SMS and email 2FA](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) tutorial shows the following in the *web.config* file:</span></span>

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample1.xml)]

<span data-ttu-id="d56db-119">*Web.config*文件是源代码，因此这些机密永远不会存储在该文件。</span><span class="sxs-lookup"><span data-stu-id="d56db-119">The *web.config* file is source code, so these secrets should never be stored in that file.</span></span> <span data-ttu-id="d56db-120">幸运的是，`<appSettings>`元素具有`file`允许你指定外部文件包含敏感应用程序配置设置的属性。</span><span class="sxs-lookup"><span data-stu-id="d56db-120">Fortunately, the `<appSettings>` element has a `file` attribute that allows you to specify an external file that contains sensitive app config settings.</span></span> <span data-ttu-id="d56db-121">只要外部文件未签入源树，可以移到外部文件的所有机密。</span><span class="sxs-lookup"><span data-stu-id="d56db-121">You can move all your secrets to an external file as long as the external file is not checked into your source tree.</span></span> <span data-ttu-id="d56db-122">例如，在下列标记中，该文件*AppSettingsSecrets.config*包含所有应用程序机密：</span><span class="sxs-lookup"><span data-stu-id="d56db-122">For example, in the following markup, the file *AppSettingsSecrets.config* contains all the app secrets:</span></span>

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample2.xml)]

<span data-ttu-id="d56db-123">外部文件中的标记 (*AppSettingsSecrets.config*在此示例中)，在中找到的相同标记*web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="d56db-123">The markup in the external file (*AppSettingsSecrets.config* in this sample), is the same markup found in the *web.config* file:</span></span>

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample3.xml)]

<span data-ttu-id="d56db-124">ASP.NET 运行时将包含中的标记的外部文件的内容合并&lt;appSettings&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="d56db-124">The ASP.NET runtime merges the contents of the external file with the markup in &lt;appSettings&gt; element.</span></span> <span data-ttu-id="d56db-125">如果找不到指定的文件，运行时将忽略的文件属性。</span><span class="sxs-lookup"><span data-stu-id="d56db-125">The runtime ignores the file attribute if the specified file cannot be found.</span></span>

> [!WARNING]
> <span data-ttu-id="d56db-126">安全-不要添加你*机密.config*文件添加到项目，或将其签入源代码管理。</span><span class="sxs-lookup"><span data-stu-id="d56db-126">Security - Do not add your *secrets .config* file to your project or check it into source control.</span></span> <span data-ttu-id="d56db-127">默认情况下，Visual Studio 会将设置`Build Action`到`Content`，这意味着文件部署。</span><span class="sxs-lookup"><span data-stu-id="d56db-127">By default, Visual Studio sets the `Build Action` to `Content`, which means the file is deployed.</span></span> <span data-ttu-id="d56db-128">有关详细信息请参阅[为什么不我的项目文件夹中的文件的所有部署呢？](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment)</span><span class="sxs-lookup"><span data-stu-id="d56db-128">For more information see [Why don't all of the files in my project folder get deployed?](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment)</span></span> <span data-ttu-id="d56db-129">尽管可以使用任何扩展*机密.config*文件，则最好使其保持 *.config*，如配置文件不由 IIS 提供。</span><span class="sxs-lookup"><span data-stu-id="d56db-129">Although you can use any extension for the *secrets .config* file, it's best to keep it *.config*, as config files are not served by IIS.</span></span> <span data-ttu-id="d56db-130">此外请注意， *AppSettingsSecrets.config*文件是从两个目录级别向上*web.config*文件，因此它完全不足解决方案目录。</span><span class="sxs-lookup"><span data-stu-id="d56db-130">Notice also that the *AppSettingsSecrets.config* file is two directory levels up from the *web.config* file, so it's completely out of the solution directory.</span></span> <span data-ttu-id="d56db-131">将外解决方案目录，该文件移&quot;git 添加\*&quot;不会将其添加到你的存储库。</span><span class="sxs-lookup"><span data-stu-id="d56db-131">By moving the file out of the solution directory, &quot;git add \*&quot; won't add it to your repository.</span></span>


<a id="con"></a>
## <a name="working-with-connection-strings-in-the-development-environment"></a><span data-ttu-id="d56db-132">处理在开发环境中的连接字符串</span><span class="sxs-lookup"><span data-stu-id="d56db-132">Working with connection strings in the development environment</span></span>

<span data-ttu-id="d56db-133">Visual Studio 将创建使用的新 ASP.NET 项目[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d56db-133">Visual Studio creates new ASP.NET projects that use [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="d56db-134">专为开发环境创建 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="d56db-134">LocalDB was created specifically for the development environment.</span></span> <span data-ttu-id="d56db-135">它不需要密码，因此你不需要执行任何操作来避免机密被签入到源代码。</span><span class="sxs-lookup"><span data-stu-id="d56db-135">It doesn't require a password, therefore you don't need to do anything to prevent secrets from being checked into your source code.</span></span> <span data-ttu-id="d56db-136">一些开发团队使用需要密码的完整版本的 SQL Server （或其他 DBMS）。</span><span class="sxs-lookup"><span data-stu-id="d56db-136">Some development teams use the full versions of SQL Server (or other DBMS) that require a password.</span></span>

<span data-ttu-id="d56db-137">你可以使用`configSource`属性来替换整个`<connectionStrings>`标记。</span><span class="sxs-lookup"><span data-stu-id="d56db-137">You can use the `configSource` attribute to replace the entire `<connectionStrings>` markup.</span></span> <span data-ttu-id="d56db-138">与不同`<appSettings>``file`合并标记的属性`configSource`特性将取代标记。</span><span class="sxs-lookup"><span data-stu-id="d56db-138">Unlike the `<appSettings>` `file` attribute that merges the markup, the `configSource` attribute replaces the markup.</span></span> <span data-ttu-id="d56db-139">下面的标记演示`configSource`属性中*web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="d56db-139">The following markup shows the `configSource` attribute in the *web.config* file:</span></span>

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample4.xml?highlight=1)]

> [!NOTE]
> <span data-ttu-id="d56db-140">如果你使用`configSource`特性如上所示将连接字符串移到外部文件，并且具有 Visual Studio 创建新的网站，它将无法检测你正在使用数据库，并且你不会获得配置数据库的选项时你 publish 到 Azure，从 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d56db-140">If you use the `configSource` attribute as shown above to move your connection strings to an external file, and have Visual Studio create a new web site, it won't be able to detect you are using a database, and you won't get the option of configuring the database when you publish to Azure from Visual Studio.</span></span> <span data-ttu-id="d56db-141">如果你使用`configSource`属性，可以使用 PowerShell 创建和部署你的网站和数据库，或者你可以创建网站和数据库在门户中发布之前。</span><span class="sxs-lookup"><span data-stu-id="d56db-141">If you are using the `configSource` attribute, you can use PowerShell to create and deploy your web site and database, or you can create the web site and the database in the portal before you publish.</span></span> <span data-ttu-id="d56db-142">[新建 AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)脚本将创建一个新的网站和数据库。</span><span class="sxs-lookup"><span data-stu-id="d56db-142">The [New-AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) script will create a new web site and database.</span></span>


> [!WARNING]
> <span data-ttu-id="d56db-143">安全-与不同*AppSettingsSecrets.config*文件中，外部连接字符串文件必须是作为根相同的目录中*web.config*文件，因此你将需要采取预防措施来确保你不将其签入源代码存储库。</span><span class="sxs-lookup"><span data-stu-id="d56db-143">Security - Unlike the *AppSettingsSecrets.config* file, the external connection strings file must be in the same directory as the root *web.config* file, so you'll have to take precautions to ensure you don't check it into your source repository.</span></span>


> [!NOTE]
> <span data-ttu-id="d56db-144">**机密文件上的安全警告：** 一种最佳做法是不使用生产中测试和开发的机密。</span><span class="sxs-lookup"><span data-stu-id="d56db-144">**Security Warning on secrets file:** A best practice is to not use production secrets in test and development.</span></span> <span data-ttu-id="d56db-145">使用在测试或开发的生产密码泄漏这些机密。</span><span class="sxs-lookup"><span data-stu-id="d56db-145">Using production passwords in test or development leaks those secrets.</span></span>


<a id="wj"></a>
## <a name="webjobs-console-apps"></a><span data-ttu-id="d56db-146">Web 作业的控制台应用</span><span class="sxs-lookup"><span data-stu-id="d56db-146">WebJobs console apps</span></span>

<span data-ttu-id="d56db-147">*App.config*文件使用的控制台应用程序不支持相对路径，但它支持绝对路径。</span><span class="sxs-lookup"><span data-stu-id="d56db-147">The *app.config* file used by a console app doesn't support relative paths, but it does support absolute paths.</span></span> <span data-ttu-id="d56db-148">绝对路径可用于您的机密信息中移出你的项目目录。</span><span class="sxs-lookup"><span data-stu-id="d56db-148">You can use an absolute path to move your secrets out of your project directory.</span></span> <span data-ttu-id="d56db-149">以下标记显示中的机密*C:\secrets\AppSettingsSecrets.config*文件和中的非敏感数据*app.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d56db-149">The following markup shows the secrets in the *C:\secrets\AppSettingsSecrets.config* file, and non sensitive data in the *app.config* file.</span></span>

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample5.xml?highlight=2)]

<a id="da"></a>
## <a name="deploying-secrets-to-azure"></a><span data-ttu-id="d56db-150">部署到 Azure 的机密</span><span class="sxs-lookup"><span data-stu-id="d56db-150">Deploying secrets to Azure</span></span>

<span data-ttu-id="d56db-151">当你的 web 应用部署到 Azure， *AppSettingsSecrets.config*文件不会将部署 （这是你想得到）。</span><span class="sxs-lookup"><span data-stu-id="d56db-151">When you deploy your web app to Azure, the *AppSettingsSecrets.config* file won't be deployed (that's what you want).</span></span> <span data-ttu-id="d56db-152">无法转到[Azure 管理门户](https://azure.microsoft.com/services/management-portal/)和手动设置这些设置，以执行此操作：</span><span class="sxs-lookup"><span data-stu-id="d56db-152">You could go to the [Azure Management Portal](https://azure.microsoft.com/services/management-portal/) and set them manually, to do that:</span></span>

1. <span data-ttu-id="d56db-153">转到[ https://portal.azure.com ](https://portal.azure.com)，并使用你的 Azure 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="d56db-153">Go to [https://portal.azure.com](https://portal.azure.com), and sign in with your Azure credentials.</span></span>
2. <span data-ttu-id="d56db-154">单击**浏览&gt;Web Apps**，然后单击你的 web 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="d56db-154">Click **Browse &gt; Web Apps**, then click the name of your web app.</span></span>
3. <span data-ttu-id="d56db-155">单击**所有设置&gt;应用程序设置**。</span><span class="sxs-lookup"><span data-stu-id="d56db-155">Click **All settings &gt; Application settings**.</span></span>

<span data-ttu-id="d56db-156">**应用设置**和**连接字符串**值重写中的相同设置*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d56db-156">The **app settings** and **connection string** values override the same settings in the *web.config* file.</span></span> <span data-ttu-id="d56db-157">在本示例中，我们未不将这些设置部署到 Azure，但如果这些注册表项中*web.config*文件，在门户上显示的设置将优先。</span><span class="sxs-lookup"><span data-stu-id="d56db-157">In our example, we did not deploy these settings to Azure, but if these keys were in the *web.config* file, the settings shown on the portal would take precedence.</span></span>

<span data-ttu-id="d56db-158">最佳做法是按照[DevOps 工作流](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md)并用[Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) (或另一个框架[Chef](http://www.opscode.com/chef/)或[Puppet](http://puppetlabs.com/puppet/what-is-puppet)) 到自动执行在 Azure 中设置这些值。</span><span class="sxs-lookup"><span data-stu-id="d56db-158">A best practice is to follow a [DevOps workflow](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md) and use [Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) (or another framework such as [Chef](http://www.opscode.com/chef/) or [Puppet](http://puppetlabs.com/puppet/what-is-puppet)) to automate setting these values in Azure.</span></span> <span data-ttu-id="d56db-159">以下 PowerShell 脚本使用[Export-clixml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk)导出到磁盘的加密的机密：</span><span class="sxs-lookup"><span data-stu-id="d56db-159">The following PowerShell script uses [Export-CliXml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk) to export the encrypted secrets to disk:</span></span>

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample6.ps1)]

<span data-ttu-id="d56db-160">在上述脚本中，Name 是的名称的密钥，如&quot;FB\_AppSecret&quot;或"TwitterSecret"。</span><span class="sxs-lookup"><span data-stu-id="d56db-160">In the script above, ‘Name' is the name of the secret key, such as ‘&quot;FB\_AppSecret&quot; or "TwitterSecret".</span></span> <span data-ttu-id="d56db-161">你可以查看你的浏览器中的脚本创建的".credential"文件。</span><span class="sxs-lookup"><span data-stu-id="d56db-161">You can view the ".credential" file created by the script in your browser.</span></span> <span data-ttu-id="d56db-162">下面的代码段的凭据文件的每个测试，并将设置为指定的 web 应用的机密：</span><span class="sxs-lookup"><span data-stu-id="d56db-162">The snippet below tests each of the credential files and sets the secrets for the named web app:</span></span>

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample7.ps1)]

> [!WARNING]
> <span data-ttu-id="d56db-163">安全-不包含密码或其他机密信息在 PowerShell 脚本中，执行这样的破坏使用 PowerShell 脚本部署敏感数据的用途。</span><span class="sxs-lookup"><span data-stu-id="d56db-163">Security - Don't include passwords or other secrets in the PowerShell script, doing so defeats the purpose of using a PowerShell script to deploy sensitive data.</span></span> <span data-ttu-id="d56db-164">[Get-credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet 提供了获取密码的安全机制。</span><span class="sxs-lookup"><span data-stu-id="d56db-164">The [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet provides a secure mechanism to obtain a password.</span></span> <span data-ttu-id="d56db-165">使用 UI 提示可能会阻止泄露密码。</span><span class="sxs-lookup"><span data-stu-id="d56db-165">Using a UI prompt can prevent leaking a password.</span></span>


### <a name="deploying-db-connection-strings"></a><span data-ttu-id="d56db-166">部署数据库连接字符串</span><span class="sxs-lookup"><span data-stu-id="d56db-166">Deploying DB connection strings</span></span>

<span data-ttu-id="d56db-167">DB 连接字符串被处理方法类似于应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="d56db-167">DB connection strings are handled similarly to app settings.</span></span> <span data-ttu-id="d56db-168">如果部署 web 应用从 Visual Studio 时，将为你配置的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d56db-168">If you deploy your web app from Visual Studio, the connection string will be configured for you.</span></span> <span data-ttu-id="d56db-169">你可以在门户中对此进行验证。</span><span class="sxs-lookup"><span data-stu-id="d56db-169">You can verify this in the portal.</span></span> <span data-ttu-id="d56db-170">设置连接字符串的建议的方法是使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d56db-170">The recommended way to set the connection string is with PowerShell.</span></span> <span data-ttu-id="d56db-171">有关 PowerShell 脚本的示例创建一个网站和数据库，并设置连接字符串在网站中，下载[新建 AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)从[Azure 脚本库](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)。</span><span class="sxs-lookup"><span data-stu-id="d56db-171">For an example of a PowerShell script the creates a website and database and sets the connection string in the website, download [New-AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) from the [Azure Script library](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure).</span></span>

<a id="not"></a>
## <a name="notes-for-php"></a><span data-ttu-id="d56db-172">For PHP 的说明</span><span class="sxs-lookup"><span data-stu-id="d56db-172">Notes for PHP</span></span>

<span data-ttu-id="d56db-173">由于两个键 / 值对**应用设置**和**连接字符串**存储在 Azure App Service 上的环境变量使用任何 web 应用程序框架 （如 PHP) 可以轻松的开发人员检索这些值。</span><span class="sxs-lookup"><span data-stu-id="d56db-173">Since the key-value pairs for both **app settings** and **connection strings** are stored in environment variables on Azure App Service, developers that use any web app frameworks (such as PHP) can easily retrieve these values.</span></span> <span data-ttu-id="d56db-174">请参阅 Stefan Schackow [Windows Azure 网站： 应用程序字符串和连接字符串的工作原理](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)博客文章，其中显示了 PHP 代码段以读取应用程序设置和连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d56db-174">See Stefan Schackow's [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) blog post which shows a PHP snippet to read app settings and connection strings.</span></span>

## <a name="notes-for-on-premises-servers"></a><span data-ttu-id="d56db-175">说明在本地服务器</span><span class="sxs-lookup"><span data-stu-id="d56db-175">Notes for on-premises servers</span></span>

<span data-ttu-id="d56db-176">如果将部署到本地 web 服务器，你可以帮助通过安全机密[加密配置文件的配置节](https://msdn.microsoft.com/library/ff647398.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d56db-176">If you are deploying to on-premises web servers, you can help secure secrets by [encrypting the configuration sections of configuration files](https://msdn.microsoft.com/library/ff647398.aspx).</span></span> <span data-ttu-id="d56db-177">作为替代方法，你可以使用相同的方法为 Azure 网站建议： 将开发设置保留在配置文件，并为生产设置中使用环境变量值。</span><span class="sxs-lookup"><span data-stu-id="d56db-177">As an alternative, you can use the same approach recommended for Azure Websites: keep development settings in configuration files, and use environment variable values for production settings.</span></span> <span data-ttu-id="d56db-178">在这种情况下，但是，你需要编写实现的功能自动在 Azure 网站中的应用程序代码： 从环境变量中检索设置并使用这些值来代替配置文件设置，或者使用配置文件设置时找不到环境变量。</span><span class="sxs-lookup"><span data-stu-id="d56db-178">In this case, however, you have to write application code for functionality that is automatic in Azure Websites: retrieve settings from environment variables and use those values in place of configuration file settings, or use configuration file settings when environment variables are not found.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="d56db-179">其他资源</span><span class="sxs-lookup"><span data-stu-id="d56db-179">Additional Resources</span></span>

<span data-ttu-id="d56db-180">有关的 PowerShell 示例脚本创建 web 应用 + 数据库，设置连接字符串 + 应用设置、 下载[新建 AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)从[Azure 脚本库](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)。</span><span class="sxs-lookup"><span data-stu-id="d56db-180">For an example of a PowerShell script that creates a web app + database, sets the connection string + app settings, download [New-AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) from the [Azure Script library](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure).</span></span> 

<span data-ttu-id="d56db-181">请参阅 Stefan Schackow [Windows Azure 网站： 如何应用程序字符串和连接字符串的工作](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)</span><span class="sxs-lookup"><span data-stu-id="d56db-181">See Stefan Schackow's [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)</span></span>


<span data-ttu-id="d56db-182">特别感谢 Barry Dorrans ( [ @blowdart ](https://twitter.com/blowdart) ) 和 Carlos Farre 以评审。</span><span class="sxs-lookup"><span data-stu-id="d56db-182">Special thanks to Barry Dorrans ( [@blowdart](https://twitter.com/blowdart) ) and Carlos Farre for reviewing.</span></span>
