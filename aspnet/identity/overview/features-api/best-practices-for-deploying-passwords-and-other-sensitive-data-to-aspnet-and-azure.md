---
uid: identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
title: 密码和其他敏感数据部署到 ASP.NET 和 Azure 应用服务的最佳做法 |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何在代码可以安全地存储和访问安全信息。 最重要的一点是您应该永远不会存储密码或其他服务...
ms.author: riande
ms.date: 05/21/2015
ms.assetid: 97902c66-cb61-4d11-be52-73f962f2db0a
msc.legacyurl: /identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
msc.type: authoredcontent
ms.openlocfilehash: 8b5d6bf9fad72218341e4e0b90144da01abea3aa
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577531"
---
<a name="best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure-app-service"></a><span data-ttu-id="63850-104">密码和其他敏感数据部署到 ASP.NET 和 Azure 应用服务的最佳实践</span><span class="sxs-lookup"><span data-stu-id="63850-104">Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service</span></span>
====================
<span data-ttu-id="63850-105">通过[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="63850-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="63850-106">本教程演示如何在代码可以安全地存储和访问安全信息。</span><span class="sxs-lookup"><span data-stu-id="63850-106">This tutorial shows how your code can securely store and access secure information.</span></span> <span data-ttu-id="63850-107">最重要的一点是您应永远不会将密码或其他敏感数据存储在源代码中，并且不应在开发和测试模式下使用生产机密。</span><span class="sxs-lookup"><span data-stu-id="63850-107">The most important point is you should never store passwords or other sensitive data in source code, and you shouldn't use production secrets in development and test mode.</span></span>
> 
> <span data-ttu-id="63850-108">示例代码是一个简单的 web 作业控制台应用和需要访问数据库连接字符串密码，Twilio，Google 和 SendGrid 安全密钥的 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="63850-108">The sample code is a simple WebJob console app and a ASP.NET MVC app that needs access to a database connection string password, Twilio, Google and SendGrid secure keys.</span></span>
> 
> <span data-ttu-id="63850-109">在本地设置和 PHP 还将提到。</span><span class="sxs-lookup"><span data-stu-id="63850-109">On premise settings and PHP is also mentioned.</span></span>


- [<span data-ttu-id="63850-110">使用开发环境中的密码</span><span class="sxs-lookup"><span data-stu-id="63850-110">Working with passwords in the development environment</span></span>](#pwd)
- [<span data-ttu-id="63850-111">处理在开发环境中的连接字符串</span><span class="sxs-lookup"><span data-stu-id="63850-111">Working with connection strings in the development environment</span></span>](#con)
- [<span data-ttu-id="63850-112">Web 作业的控制台应用</span><span class="sxs-lookup"><span data-stu-id="63850-112">WebJobs console apps</span></span>](#wj)
- [<span data-ttu-id="63850-113">将机密部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="63850-113">Deploying secrets to Azure</span></span>](#da)
- [<span data-ttu-id="63850-114">在本地和 PHP 的说明</span><span class="sxs-lookup"><span data-stu-id="63850-114">Notes for On-Premise and PHP</span></span>](#not)
- [<span data-ttu-id="63850-115">其他资源</span><span class="sxs-lookup"><span data-stu-id="63850-115">Additional Resources</span></span>](#addRes)

<a id="pwd"></a>
## <a name="working-with-passwords-in-the-development-environment"></a><span data-ttu-id="63850-116">使用开发环境中的密码</span><span class="sxs-lookup"><span data-stu-id="63850-116">Working with passwords in the development environment</span></span>

<span data-ttu-id="63850-117">教程经常在源代码中，希望使用需要特别注意应永远不会将敏感数据存储在源代码中显示的敏感数据。</span><span class="sxs-lookup"><span data-stu-id="63850-117">Tutorials frequently show sensitive data in source code, hopefully with a caveat that you should never store sensitive data in source code.</span></span> <span data-ttu-id="63850-118">例如，我[ASP.NET MVC 5 应用程序使用 SMS 和电子邮件 2FA](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)教程演示中的以下*web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="63850-118">For example, my [ASP.NET MVC 5 app with SMS and email 2FA](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) tutorial shows the following in the *web.config* file:</span></span>

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample1.xml)]

<span data-ttu-id="63850-119">*Web.config*文件是源代码，因此这些机密应永远不会存储在该文件中。</span><span class="sxs-lookup"><span data-stu-id="63850-119">The *web.config* file is source code, so these secrets should never be stored in that file.</span></span> <span data-ttu-id="63850-120">幸运的是，`<appSettings>`元素具有`file`可以指定外部文件包含敏感应用程序配置设置的属性。</span><span class="sxs-lookup"><span data-stu-id="63850-120">Fortunately, the `<appSettings>` element has a `file` attribute that allows you to specify an external file that contains sensitive app config settings.</span></span> <span data-ttu-id="63850-121">只要外部文件未签入到源树，可以转到外部文件的所有机密。</span><span class="sxs-lookup"><span data-stu-id="63850-121">You can move all your secrets to an external file as long as the external file is not checked into your source tree.</span></span> <span data-ttu-id="63850-122">例如，在下列标记中，该文件*AppSettingsSecrets.config*包含所有应用程序机密：</span><span class="sxs-lookup"><span data-stu-id="63850-122">For example, in the following markup, the file *AppSettingsSecrets.config* contains all the app secrets:</span></span>

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample2.xml)]

<span data-ttu-id="63850-123">外部文件中的标记 (*AppSettingsSecrets.config*在此示例中) 中, 找到相同的标记*web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="63850-123">The markup in the external file (*AppSettingsSecrets.config* in this sample), is the same markup found in the *web.config* file:</span></span>

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample3.xml)]

<span data-ttu-id="63850-124">ASP.NET 运行时将外部文件中的标记的内容合并&lt;appSettings&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="63850-124">The ASP.NET runtime merges the contents of the external file with the markup in &lt;appSettings&gt; element.</span></span> <span data-ttu-id="63850-125">如果找不到指定的文件，运行时将忽略文件属性。</span><span class="sxs-lookup"><span data-stu-id="63850-125">The runtime ignores the file attribute if the specified file cannot be found.</span></span>

> [!WARNING]
> <span data-ttu-id="63850-126">安全性-不添加你*机密.config*文件添加到你的项目或将其签入源代码管理。</span><span class="sxs-lookup"><span data-stu-id="63850-126">Security - Do not add your *secrets .config* file to your project or check it into source control.</span></span> <span data-ttu-id="63850-127">默认情况下，Visual Studio 将设置`Build Action`到`Content`，这意味着该文件部署。</span><span class="sxs-lookup"><span data-stu-id="63850-127">By default, Visual Studio sets the `Build Action` to `Content`, which means the file is deployed.</span></span> <span data-ttu-id="63850-128">有关详细信息请参阅[不为什么部署所有我的项目文件夹中的文件？](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment)</span><span class="sxs-lookup"><span data-stu-id="63850-128">For more information see [Why don't all of the files in my project folder get deployed?](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment)</span></span> <span data-ttu-id="63850-129">尽管可以使用任何适用于扩展*机密.config*文件，它是让它 *.config*，如配置文件不是由 IIS。</span><span class="sxs-lookup"><span data-stu-id="63850-129">Although you can use any extension for the *secrets .config* file, it's best to keep it *.config*, as config files are not served by IIS.</span></span> <span data-ttu-id="63850-130">另请注意*AppSettingsSecrets.config*文件是从两个目录级别向上*web.config*文件，因此它完全不受解决方案目录。</span><span class="sxs-lookup"><span data-stu-id="63850-130">Notice also that the *AppSettingsSecrets.config* file is two directory levels up from the *web.config* file, so it's completely out of the solution directory.</span></span> <span data-ttu-id="63850-131">将解决方案目录中，从文件移&quot;git 添加\*&quot;不会将其添加到你的存储库。</span><span class="sxs-lookup"><span data-stu-id="63850-131">By moving the file out of the solution directory, &quot;git add \*&quot; won't add it to your repository.</span></span>


<a id="con"></a>
## <a name="working-with-connection-strings-in-the-development-environment"></a><span data-ttu-id="63850-132">处理在开发环境中的连接字符串</span><span class="sxs-lookup"><span data-stu-id="63850-132">Working with connection strings in the development environment</span></span>

<span data-ttu-id="63850-133">Visual Studio 将创建使用新 ASP.NET 项目[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)。</span><span class="sxs-lookup"><span data-stu-id="63850-133">Visual Studio creates new ASP.NET projects that use [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="63850-134">LocalDB 被创建专门针对开发环境。</span><span class="sxs-lookup"><span data-stu-id="63850-134">LocalDB was created specifically for the development environment.</span></span> <span data-ttu-id="63850-135">它不需要密码，因此你无需执行任何操作来防止机密签入源代码。</span><span class="sxs-lookup"><span data-stu-id="63850-135">It doesn't require a password, therefore you don't need to do anything to prevent secrets from being checked into your source code.</span></span> <span data-ttu-id="63850-136">一些开发团队使用需要密码的完整版本的 SQL Server （或其他 DBMS）。</span><span class="sxs-lookup"><span data-stu-id="63850-136">Some development teams use the full versions of SQL Server (or other DBMS) that require a password.</span></span>

<span data-ttu-id="63850-137">可以使用`configSource`属性来替换整个`<connectionStrings>`标记。</span><span class="sxs-lookup"><span data-stu-id="63850-137">You can use the `configSource` attribute to replace the entire `<connectionStrings>` markup.</span></span> <span data-ttu-id="63850-138">与不同`<appSettings>``file`合并标记中，属性`configSource`特性将取代标记。</span><span class="sxs-lookup"><span data-stu-id="63850-138">Unlike the `<appSettings>` `file` attribute that merges the markup, the `configSource` attribute replaces the markup.</span></span> <span data-ttu-id="63850-139">下面的标记演示`configSource`中的属性*web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="63850-139">The following markup shows the `configSource` attribute in the *web.config* file:</span></span>

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample4.xml?highlight=1)]

> [!NOTE]
> <span data-ttu-id="63850-140">如果使用`configSource`属性如上所示将您的连接字符串移动到外部文件，并让 Visual Studio 创建新的 web 站点，它将无法检测到您使用的是数据库，并不会获得配置数据库的选项时您 publish 到 Azure，从 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="63850-140">If you use the `configSource` attribute as shown above to move your connection strings to an external file, and have Visual Studio create a new web site, it won't be able to detect you are using a database, and you won't get the option of configuring the database when you publish to Azure from Visual Studio.</span></span> <span data-ttu-id="63850-141">如果使用的`configSource`属性，可以使用 PowerShell 创建和部署你的网站和数据库，也可以创建 web 站点和数据库在门户中发布之前。</span><span class="sxs-lookup"><span data-stu-id="63850-141">If you are using the `configSource` attribute, you can use PowerShell to create and deploy your web site and database, or you can create the web site and the database in the portal before you publish.</span></span> <span data-ttu-id="63850-142">[新建 AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)脚本将创建一个新的 web 站点和数据库。</span><span class="sxs-lookup"><span data-stu-id="63850-142">The [New-AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) script will create a new web site and database.</span></span>


> [!WARNING]
> <span data-ttu-id="63850-143">安全性-与不同*AppSettingsSecrets.config*文件中，外部连接字符串文件必须在相同的目录作为根*web.config*文件，因此您必须采取预防措施以确保你不将其签入源代码存储库。</span><span class="sxs-lookup"><span data-stu-id="63850-143">Security - Unlike the *AppSettingsSecrets.config* file, the external connection strings file must be in the same directory as the root *web.config* file, so you'll have to take precautions to ensure you don't check it into your source repository.</span></span>


> [!NOTE]
> <span data-ttu-id="63850-144">**机密文件上的安全警告：** 最佳做法是使用测试和开发中的生产机密。</span><span class="sxs-lookup"><span data-stu-id="63850-144">**Security Warning on secrets file:** A best practice is to not use production secrets in test and development.</span></span> <span data-ttu-id="63850-145">使用生产环境中测试或开发的密码泄漏这些机密。</span><span class="sxs-lookup"><span data-stu-id="63850-145">Using production passwords in test or development leaks those secrets.</span></span>


<a id="wj"></a>
## <a name="webjobs-console-apps"></a><span data-ttu-id="63850-146">Web 作业的控制台应用</span><span class="sxs-lookup"><span data-stu-id="63850-146">WebJobs console apps</span></span>

<span data-ttu-id="63850-147">*App.config*文件使用的控制台应用程序不支持相对路径，但它支持绝对路径。</span><span class="sxs-lookup"><span data-stu-id="63850-147">The *app.config* file used by a console app doesn't support relative paths, but it does support absolute paths.</span></span> <span data-ttu-id="63850-148">可以使用绝对路径移出您的项目目录的机密。</span><span class="sxs-lookup"><span data-stu-id="63850-148">You can use an absolute path to move your secrets out of your project directory.</span></span> <span data-ttu-id="63850-149">以下标记显示了中的机密*C:\secrets\AppSettingsSecrets.config*文件和中的非敏感数据*app.config*文件。</span><span class="sxs-lookup"><span data-stu-id="63850-149">The following markup shows the secrets in the *C:\secrets\AppSettingsSecrets.config* file, and non sensitive data in the *app.config* file.</span></span>

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample5.xml?highlight=2)]

<a id="da"></a>
## <a name="deploying-secrets-to-azure"></a><span data-ttu-id="63850-150">将机密部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="63850-150">Deploying secrets to Azure</span></span>

<span data-ttu-id="63850-151">将 web 应用部署到 Azure 中，当*AppSettingsSecrets.config*文件不会将部署 （这是所需）。</span><span class="sxs-lookup"><span data-stu-id="63850-151">When you deploy your web app to Azure, the *AppSettingsSecrets.config* file won't be deployed (that's what you want).</span></span> <span data-ttu-id="63850-152">可以转到[Azure 管理门户](https://azure.microsoft.com/services/management-portal/)和手动设置这些设置，若要执行此操作：</span><span class="sxs-lookup"><span data-stu-id="63850-152">You could go to the [Azure Management Portal](https://azure.microsoft.com/services/management-portal/) and set them manually, to do that:</span></span>

1. <span data-ttu-id="63850-153">转到[ https://portal.azure.com ](https://portal.azure.com)，并使用你的 Azure 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="63850-153">Go to [https://portal.azure.com](https://portal.azure.com), and sign in with your Azure credentials.</span></span>
2. <span data-ttu-id="63850-154">单击**浏览&gt;Web 应用**，然后单击你的 web 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="63850-154">Click **Browse &gt; Web Apps**, then click the name of your web app.</span></span>
3. <span data-ttu-id="63850-155">单击**的所有设置&gt;应用程序设置**。</span><span class="sxs-lookup"><span data-stu-id="63850-155">Click **All settings &gt; Application settings**.</span></span>

<span data-ttu-id="63850-156">**应用设置**并**连接字符串**值会重写中的相同设置*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="63850-156">The **app settings** and **connection string** values override the same settings in the *web.config* file.</span></span> <span data-ttu-id="63850-157">在本示例中，我们未部署这些设置到 Azure，但如果这些密钥处于*web.config*文件中，在门户上显示的设置将优先。</span><span class="sxs-lookup"><span data-stu-id="63850-157">In our example, we did not deploy these settings to Azure, but if these keys were in the *web.config* file, the settings shown on the portal would take precedence.</span></span>

<span data-ttu-id="63850-158">最佳做法是按照[DevOps 工作流](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md)并用[Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) (或另一个框架[Chef](http://www.opscode.com/chef/)或[Puppet](http://puppetlabs.com/puppet/what-is-puppet)) 到自动执行在 Azure 中设置这些值。</span><span class="sxs-lookup"><span data-stu-id="63850-158">A best practice is to follow a [DevOps workflow](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md) and use [Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) (or another framework such as [Chef](http://www.opscode.com/chef/) or [Puppet](http://puppetlabs.com/puppet/what-is-puppet)) to automate setting these values in Azure.</span></span> <span data-ttu-id="63850-159">使用以下 PowerShell 脚本[Export-clixml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk)导出到磁盘加密的机密：</span><span class="sxs-lookup"><span data-stu-id="63850-159">The following PowerShell script uses [Export-CliXml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk) to export the encrypted secrets to disk:</span></span>

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample6.ps1)]

<span data-ttu-id="63850-160">在上述脚本中，Name 是名称的机密密钥，如&quot;FB\_AppSecret&quot;或"twittersecret"。</span><span class="sxs-lookup"><span data-stu-id="63850-160">In the script above, ‘Name' is the name of the secret key, such as ‘&quot;FB\_AppSecret&quot; or "TwitterSecret".</span></span> <span data-ttu-id="63850-161">您可以查看你的浏览器中的脚本创建的".credential"文件。</span><span class="sxs-lookup"><span data-stu-id="63850-161">You can view the ".credential" file created by the script in your browser.</span></span> <span data-ttu-id="63850-162">下面的代码段将测试每个凭据文件，并设置命名的 web 应用的机密：</span><span class="sxs-lookup"><span data-stu-id="63850-162">The snippet below tests each of the credential files and sets the secrets for the named web app:</span></span>

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample7.ps1)]

> [!WARNING]
> <span data-ttu-id="63850-163">安全性-不包含密码或其他机密在 PowerShell 脚本中，执行这样的失败操作使用的 PowerShell 脚本以将敏感数据部署的目的。</span><span class="sxs-lookup"><span data-stu-id="63850-163">Security - Don't include passwords or other secrets in the PowerShell script, doing so defeats the purpose of using a PowerShell script to deploy sensitive data.</span></span> <span data-ttu-id="63850-164">[Get-credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet 提供了一种安全机制来获取密码。</span><span class="sxs-lookup"><span data-stu-id="63850-164">The [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet provides a secure mechanism to obtain a password.</span></span> <span data-ttu-id="63850-165">使用 UI 提示可以防止泄露密码。</span><span class="sxs-lookup"><span data-stu-id="63850-165">Using a UI prompt can prevent leaking a password.</span></span>


### <a name="deploying-db-connection-strings"></a><span data-ttu-id="63850-166">部署数据库连接字符串</span><span class="sxs-lookup"><span data-stu-id="63850-166">Deploying DB connection strings</span></span>

<span data-ttu-id="63850-167">DB 连接字符串为应用设置的相似方式进行处理。</span><span class="sxs-lookup"><span data-stu-id="63850-167">DB connection strings are handled similarly to app settings.</span></span> <span data-ttu-id="63850-168">如果部署 web 应用从 Visual Studio 时，将为你配置的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="63850-168">If you deploy your web app from Visual Studio, the connection string will be configured for you.</span></span> <span data-ttu-id="63850-169">可以在门户中对此进行验证。</span><span class="sxs-lookup"><span data-stu-id="63850-169">You can verify this in the portal.</span></span> <span data-ttu-id="63850-170">设置连接字符串的建议的方法是使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="63850-170">The recommended way to set the connection string is with PowerShell.</span></span> <span data-ttu-id="63850-171">有关 PowerShell 脚本的示例创建网站和数据库，并设置连接字符串在网站中，下载[新建 AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)从[Azure 脚本库](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)。</span><span class="sxs-lookup"><span data-stu-id="63850-171">For an example of a PowerShell script the creates a website and database and sets the connection string in the website, download [New-AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) from the [Azure Script library](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure).</span></span>

<a id="not"></a>
## <a name="notes-for-php"></a><span data-ttu-id="63850-172">用于 PHP 的说明</span><span class="sxs-lookup"><span data-stu-id="63850-172">Notes for PHP</span></span>

<span data-ttu-id="63850-173">由于两个键 / 值对**应用设置**并**连接字符串**存储在 Azure 应用服务上的环境变量使用任何 web 应用程序框架 （如 PHP) 可以轻松的开发人员检索这些值。</span><span class="sxs-lookup"><span data-stu-id="63850-173">Since the key-value pairs for both **app settings** and **connection strings** are stored in environment variables on Azure App Service, developers that use any web app frameworks (such as PHP) can easily retrieve these values.</span></span> <span data-ttu-id="63850-174">请参阅 Stefan Schackow [Windows Azure 网站： 应用程序字符串和连接字符串的工作](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)博客文章，其中显示了 PHP 代码段以读取应用程序设置和连接字符串。</span><span class="sxs-lookup"><span data-stu-id="63850-174">See Stefan Schackow's [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) blog post which shows a PHP snippet to read app settings and connection strings.</span></span>

## <a name="notes-for-on-premises-servers"></a><span data-ttu-id="63850-175">在本地服务器的说明</span><span class="sxs-lookup"><span data-stu-id="63850-175">Notes for on-premises servers</span></span>

<span data-ttu-id="63850-176">如果您要部署到的本地 web 服务器，可帮助通过安全的机密[加密配置文件的配置节](https://msdn.microsoft.com/library/ff647398.aspx)。</span><span class="sxs-lookup"><span data-stu-id="63850-176">If you are deploying to on-premises web servers, you can help secure secrets by [encrypting the configuration sections of configuration files](https://msdn.microsoft.com/library/ff647398.aspx).</span></span> <span data-ttu-id="63850-177">或者，可以使用相同的方法，建议为 Azure 网站： 在配置文件中保留开发设置和使用生产设置环境变量值。</span><span class="sxs-lookup"><span data-stu-id="63850-177">As an alternative, you can use the same approach recommended for Azure Websites: keep development settings in configuration files, and use environment variable values for production settings.</span></span> <span data-ttu-id="63850-178">在这种情况下，但是，你已将会自动在 Azure 网站中的功能的应用程序代码： 从环境变量中检索设置并使用这些值来替代配置文件设置，或使用配置文件设置时找不到环境变量。</span><span class="sxs-lookup"><span data-stu-id="63850-178">In this case, however, you have to write application code for functionality that is automatic in Azure Websites: retrieve settings from environment variables and use those values in place of configuration file settings, or use configuration file settings when environment variables are not found.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="63850-179">其他资源</span><span class="sxs-lookup"><span data-stu-id="63850-179">Additional Resources</span></span>

<span data-ttu-id="63850-180">有关 PowerShell 的示例脚本可创建 web 应用 + 数据库中，设置连接字符串 + 应用程序设置、 下载[新建 AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)从[Azure 脚本库](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)。</span><span class="sxs-lookup"><span data-stu-id="63850-180">For an example of a PowerShell script that creates a web app + database, sets the connection string + app settings, download [New-AzureWebsitewithDB.ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) from the [Azure Script library](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure).</span></span> 

<span data-ttu-id="63850-181">请参阅 Stefan Schackow [Windows Azure 网站： 如何应用程序字符串和连接字符串的工作](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)</span><span class="sxs-lookup"><span data-stu-id="63850-181">See Stefan Schackow's [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)</span></span>


<span data-ttu-id="63850-182">特别感谢 Barry Dorrans ( [ @blowdart ](https://twitter.com/blowdart) ) 和 Carlos Farre 对进行了审阅。</span><span class="sxs-lookup"><span data-stu-id="63850-182">Special thanks to Barry Dorrans ( [@blowdart](https://twitter.com/blowdart) ) and Carlos Farre for reviewing.</span></span>
