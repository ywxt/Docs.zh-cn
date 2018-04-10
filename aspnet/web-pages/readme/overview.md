---
uid: web-pages/readme/overview
title: WebMatrix 自述文件 |Microsoft 文档
author: rick-anderson
description: WebMatrix 和 ASP.NET Web 页 (Razor) 1.0 版本自述文件
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/06/2011
ms.topic: article
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: c65ee58b8c13b0b4acb6e7c9b631c8235e791506
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
---
<a name="webmatrix-readme"></a><span data-ttu-id="521e3-103">WebMatrix Readme</span><span class="sxs-lookup"><span data-stu-id="521e3-103">WebMatrix Readme</span></span>
====================
<span data-ttu-id="521e3-104">2011 年 1 月 13日</span><span class="sxs-lookup"><span data-stu-id="521e3-104">13 January 2011</span></span>

## <a name="contents"></a><span data-ttu-id="521e3-105">内容</span><span class="sxs-lookup"><span data-stu-id="521e3-105">Contents</span></span>

> [!NOTE]
> <span data-ttu-id="521e3-106">本自述文件适用于 1.0 版本的 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="521e3-106">This readme applies to the 1.0 release of WebMatrix.</span></span>


- [<span data-ttu-id="521e3-107">概述</span><span class="sxs-lookup"><span data-stu-id="521e3-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="521e3-108">安装</span><span class="sxs-lookup"><span data-stu-id="521e3-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="521e3-109">如何发布应用程序</span><span class="sxs-lookup"><span data-stu-id="521e3-109">How to Publish Applications</span></span>](#InstructionsForPublishingApplications)
- [<span data-ttu-id="521e3-110">更改和问题</span><span class="sxs-lookup"><span data-stu-id="521e3-110">Changes and Issues</span></span>](#ChangesAndIssues)

    - [<span data-ttu-id="521e3-111">WebMatrix 1.0 安装</span><span class="sxs-lookup"><span data-stu-id="521e3-111">WebMatrix 1.0 Installation</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="521e3-112">ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="521e3-112">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="521e3-113">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="521e3-113">WebMatrix</span></span>](#Known_Issues_WebMatrix)
    - [<span data-ttu-id="521e3-114">IIS Express</span><span class="sxs-lookup"><span data-stu-id="521e3-114">IIS Express</span></span>](#Known_Issues_IISExpress)
    - [<span data-ttu-id="521e3-115">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="521e3-115">SQL Server Compact</span></span>](#Known_Issues_SQLServerCompact)
    - [<span data-ttu-id="521e3-116">安装应用程序</span><span class="sxs-lookup"><span data-stu-id="521e3-116">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="521e3-117">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="521e3-117">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
- [<span data-ttu-id="521e3-118">有关详细信息</span><span class="sxs-lookup"><span data-stu-id="521e3-118">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="521e3-119">概述</span><span class="sxs-lookup"><span data-stu-id="521e3-119">Overview</span></span>

> <span data-ttu-id="521e3-120">Microsoft WebMatrix 1.0 是一个免费 web 开发堆栈，以分钟为单位安装。</span><span class="sxs-lookup"><span data-stu-id="521e3-120">Microsoft WebMatrix 1.0 is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="521e3-121">它与数据库和编程框架创建单一的集成体验集成的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="521e3-121">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="521e3-122">你可以使用 WebMatrix 来简化的方法的代码、 测试和发布你自己的 ASP.NET 或 PHP 网站，或你可以使用 WebMatrix 启动使用如 DotNetNuke、 Umbraco、 WordPress、 Joomla 的常用的开源应用程序的新网站。</span><span class="sxs-lookup"><span data-stu-id="521e3-122">You can use WebMatrix to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="521e3-123">WebMatrix 使用相同的功能强大的 web 服务器、 数据库引擎和运行你的网站在 internet 上，从而可以从开发到生产环境的转换平滑无缝的框架环境。</span><span class="sxs-lookup"><span data-stu-id="521e3-123">WebMatrix uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>


<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="521e3-124">安装</span><span class="sxs-lookup"><span data-stu-id="521e3-124">Installation</span></span>

> <span data-ttu-id="521e3-125">若要安装 WebMatrix 1.0，必须首先安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="521e3-125">To install WebMatrix 1.0, you must first install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="521e3-126">安装 Web 平台安装程序后，可用于安装 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="521e3-126">After you've installed the Web Platform Installer, you can use it to install WebMatrix.</span></span>
> 
> <span data-ttu-id="521e3-127">如果在安装过程中遇到问题，请参阅[Microsoft Web 平台安装程序的故障排除问题](https://go.microsoft.com/fwlink/?LinkId=196212)。</span><span class="sxs-lookup"><span data-stu-id="521e3-127">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>


<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a><span data-ttu-id="521e3-128">如何发布应用程序</span><span class="sxs-lookup"><span data-stu-id="521e3-128">How to Publish Applications</span></span>

> <span data-ttu-id="521e3-129">请参阅[发布应用程序的分步说明](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="521e3-129">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>


<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a><span data-ttu-id="521e3-130">更改和问题</span><span class="sxs-lookup"><span data-stu-id="521e3-130">Changes and Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a><span data-ttu-id="521e3-131">WebMatrix 1.0 安装问题</span><span class="sxs-lookup"><span data-stu-id="521e3-131">WebMatrix 1.0 Installation Issues</span></span>

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="521e3-132">问题： WebMatrix 1.0 是仅在支持 Microsoft.NET Framework 4 的平台上可用</span><span class="sxs-lookup"><span data-stu-id="521e3-132">Issue: WebMatrix 1.0 is available only on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="521e3-133">.NET Framework 版本 4 是必需的 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="521e3-133">The .NET Framework version 4 is required for WebMatrix.</span></span> <span data-ttu-id="521e3-134">在某些情况下，WebMatrix 1.0 安装程序将让你尝试在不受支持的配置集的一部分的平台上安装。</span><span class="sxs-lookup"><span data-stu-id="521e3-134">In certain cases, the WebMatrix 1.0 installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="521e3-135">具体而言，不带 SP1 更新的 Windows Vista 将你可以开始安装 WebMatrix 中，但该.NET Framework 4 组件将失败并阻止你安装。</span><span class="sxs-lookup"><span data-stu-id="521e3-135">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="521e3-136">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-136">**Workaround**</span></span>  
> <span data-ttu-id="521e3-137">安装上受支持的平台，其中包括：</span><span class="sxs-lookup"><span data-stu-id="521e3-137">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="521e3-138">Windows 7</span><span class="sxs-lookup"><span data-stu-id="521e3-138">Windows 7</span></span>
> - <span data-ttu-id="521e3-139">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="521e3-139">Windows Server 2008</span></span>
> - <span data-ttu-id="521e3-140">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="521e3-140">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="521e3-141">Windows Vista SP1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="521e3-141">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="521e3-142">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="521e3-142">Windows XP SP3</span></span>
> - <span data-ttu-id="521e3-143">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="521e3-143">Windows Server 2003 SP2</span></span>


#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="521e3-144">问题： 无法安装 WebMatrix 1.0，如果没有 Microsoft Visual Studio 2008 SP1 的情况下已安装 Microsoft Visual Studio 2008</span><span class="sxs-lookup"><span data-stu-id="521e3-144">Issue: Cannot install WebMatrix 1.0 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="521e3-145">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-145">**Workaround**</span></span>  
> <span data-ttu-id="521e3-146">安装[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en)从 Microsoft 下载中心获取。</span><span class="sxs-lookup"><span data-stu-id="521e3-146">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>


#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="521e3-147">问题： SQL Server Compact 4.0 某些程序集未安装在 GAC 中</span><span class="sxs-lookup"><span data-stu-id="521e3-147">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="521e3-148">在 64 位计算机上安装 SQL Server Compact 4.0 和计算机具有仅.NET Framework 3.5 SP1 客户端安装配置文件时，SQL Server Compact 4.0 的托管程序集不会放置在全局程序集缓存 (GAC)。</span><span class="sxs-lookup"><span data-stu-id="521e3-148">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="521e3-149">未安装在 GAC 中的托管程序集是：</span><span class="sxs-lookup"><span data-stu-id="521e3-149">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="521e3-150">*System.Data.SqlServerCe.dll* （ADO.NET 提供程序）</span><span class="sxs-lookup"><span data-stu-id="521e3-150">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="521e3-151">*System.Data.SqlServerCe.Entity.dll* （ADO.NET 实体框架）</span><span class="sxs-lookup"><span data-stu-id="521e3-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="521e3-152">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-152">**Workaround**</span></span>  
> <span data-ttu-id="521e3-153">卸载 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="521e3-153">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="521e3-154">下载并安装.NET Framework 3.5 SP1 的完整版本，从以下位置：</span><span class="sxs-lookup"><span data-stu-id="521e3-154">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="521e3-155">Microsoft.NET Framework 3.5 Service pack 1 （完全包）</span><span class="sxs-lookup"><span data-stu-id="521e3-155">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="521e3-156">然后重新安装 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="521e3-156">Then reinstall SQL Server Compact 4.0.</span></span>


#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="521e3-157">问题： 无法卸载 SQL Server Compact 使用命令行</span><span class="sxs-lookup"><span data-stu-id="521e3-157">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="521e3-158">卸载 SQL Server Compact 使用命令行选项不在此版本中无效。</span><span class="sxs-lookup"><span data-stu-id="521e3-158">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="521e3-159">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-159">**Workaround**</span></span>  
> <span data-ttu-id="521e3-160">使用*程序和功能*Windows 控制面板卸载 Microsoft SQL Server Compact 4.0 中。</span><span class="sxs-lookup"><span data-stu-id="521e3-160">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>


<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="521e3-161">ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="521e3-161">ASP.NET Web Pages</span></span>

<span data-ttu-id="521e3-162">文档本部分介绍的新增功能、 更改和 1.0 版本的 ASP.NET Web Pages 使用 Razor 语法的已知的问题。</span><span class="sxs-lookup"><span data-stu-id="521e3-162">This section of the document describes new features, changes, and known issues with the 1.0 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="521e3-163">新功能</span><span class="sxs-lookup"><span data-stu-id="521e3-163">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="521e3-164">更改</span><span class="sxs-lookup"><span data-stu-id="521e3-164">Changes</span></span>](#Changes)
- [<span data-ttu-id="521e3-165">问题</span><span class="sxs-lookup"><span data-stu-id="521e3-165">Issues</span></span>](#Issues)

#### <a id="NewFeatures"></a>  <span data-ttu-id="521e3-166">新功能</span><span class="sxs-lookup"><span data-stu-id="521e3-166">New Features</span></span>

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a><span data-ttu-id="521e3-167">配置设置添加禁用包管理器的新增内容：</span><span class="sxs-lookup"><span data-stu-id="521e3-167">New: Configuration setting added to disable the package manager</span></span>

> <span data-ttu-id="521e3-168">一个新`asp:AdminManagerEnabled`密钥是可用于`<appSettings>`中的元素*web.config*文件，可让你完全禁用程序包管理器。</span><span class="sxs-lookup"><span data-stu-id="521e3-168">A new `asp:AdminManagerEnabled` key is available for the `<appSettings>` element in the *web.config* file, which lets you completely disable the package manager.</span></span> <span data-ttu-id="521e3-169">此元素的默认值为 true，这意味着，如果它不包括在*web.config*是否启用了文件，包管理器。</span><span class="sxs-lookup"><span data-stu-id="521e3-169">The default value for this element is true, meaning that if it is not included in the *web.config* file, the package manager is enabled.</span></span> <span data-ttu-id="521e3-170">若要禁用的程序包管理器，以下将元素添加到*web.config*在网站的根目录中的文件：</span><span class="sxs-lookup"><span data-stu-id="521e3-170">To disable the package manager, add the following element to the *web.config* file in the root of the website:</span></span>
> 
> [!code-xml[Main](overview/samples/sample1.xml)]


#### <a id="Changes"></a>  <span data-ttu-id="521e3-171">更改</span><span class="sxs-lookup"><span data-stu-id="521e3-171">Changes</span></span>

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a><span data-ttu-id="521e3-172">重命名为"asp: AdminFolderVirtualPath"的更改:"webPages:AdminFolderVirtualPath"密钥</span><span class="sxs-lookup"><span data-stu-id="521e3-172">Change: "webPages:AdminFolderVirtualPath" key renamed to "asp:AdminFolderVirtualPath"</span></span>

> <span data-ttu-id="521e3-173">`webPages:AdminFolderVirtualPath`可以添加到的密钥*web.config*文件，以指定包管理器的位置具有已重命名为使用`asp:`命名空间而不是`webPages`命名空间。</span><span class="sxs-lookup"><span data-stu-id="521e3-173">The `webPages:AdminFolderVirtualPath` key that can be added to the *web.config* file to specify the location of the package manager has been renamed to use the `asp:` namespace instead of the `webPages` namespace.</span></span> <span data-ttu-id="521e3-174">如果你已使用此元素，必须在配置文件中时将它重命名。</span><span class="sxs-lookup"><span data-stu-id="521e3-174">If you have used this element, you must rename it in the configuration file.</span></span>


#### <a id="Issues"></a>  <span data-ttu-id="521e3-175">已知的问题</span><span class="sxs-lookup"><span data-stu-id="521e3-175">Known Issues</span></span>

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a><span data-ttu-id="521e3-176">问题： 不再识别的成员资格用户的密码</span><span class="sxs-lookup"><span data-stu-id="521e3-176">Issue: Passwords for membership users no longer recognized</span></span>

> <span data-ttu-id="521e3-177">用于创建和存储成员身份 （登录名） 密码算法已更改为更安全。</span><span class="sxs-lookup"><span data-stu-id="521e3-177">The algorithm for creating and storing membership (login) passwords has been changed to be more secure.</span></span> <span data-ttu-id="521e3-178">因此，将不识别为成员 （用户） 创建的 ASP.NET Razor 的 Beta 版本中存储的密码。</span><span class="sxs-lookup"><span data-stu-id="521e3-178">As a result, the passwords stored for members (users) created in Beta versions of ASP.NET Razor will not be recognized.</span></span> 
> 
> <span data-ttu-id="521e3-179">**解决方法**站点尚未放到生产环境，如果从成员资格数据库中删除用户记录。</span><span class="sxs-lookup"><span data-stu-id="521e3-179">**Workaround** If the site has not yet been put into production, remove the user records from the membership database.</span></span> <span data-ttu-id="521e3-180">如果实时数据库，以编程方式重新生成成员资格数据库中的现有密码。</span><span class="sxs-lookup"><span data-stu-id="521e3-180">If database is live, programmatically regenerate existing passwords in the membership database.</span></span>


#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="521e3-181">问题： 意外的行为时使用的成员身份的自定义用户表</span><span class="sxs-lookup"><span data-stu-id="521e3-181">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="521e3-182">若要初始化的成员资格提供程序的 ASP.NET Razor 网站，你可以调用`WebSecurity.InitializeDatabaseConnection`方法。</span><span class="sxs-lookup"><span data-stu-id="521e3-182">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="521e3-183">(在 WebMatrix 中，入门站点模板包括对在此方法的调用 *\_AppStart.cshtml*文件。)如果`autoCreateTables`此方法的参数设置为 true (默认情况下，它设置为 true 的入门站点模板中)，并且如果无法识别的表名称传递给方法 （第二个参数），该方法不会引发错误。</span><span class="sxs-lookup"><span data-stu-id="521e3-183">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="521e3-184">相反，它会自动创建表。</span><span class="sxs-lookup"><span data-stu-id="521e3-184">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="521e3-185">这可能会造成问题，如果你想要使用的成员身份的自定义用户表，但传递到的错误的表名称`WebSecurity.InitializeDatabaseConnection`方法。</span><span class="sxs-lookup"><span data-stu-id="521e3-185">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="521e3-186">因为该方法不会默认情况下引发错误如果您指定的表不存在，而且它改为创建一个新表，则应用程序可以似乎无法正常工作。</span><span class="sxs-lookup"><span data-stu-id="521e3-186">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="521e3-187">但是，依赖于自定义用户表 （和在其中的字段） 的应用程序代码可能最终失败，意外错误。</span><span class="sxs-lookup"><span data-stu-id="521e3-187">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="521e3-188">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-188">**Workaround**</span></span>  
> <span data-ttu-id="521e3-189">请确保名称传递中`InitializeDatabaseConnection`方法匹配项的用户配置文件表中成员资格数据库中，或确保`autoCreateTables`参数设置为 false。</span><span class="sxs-lookup"><span data-stu-id="521e3-189">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>


#### <a name="issue-error-message-the-admin-module-requires-access-to-appdata"></a><span data-ttu-id="521e3-190">问题： 错误消息"管理员模块需要访问 ~/App\_数据"</span><span class="sxs-lookup"><span data-stu-id="521e3-190">Issue: Error message "The Admin Module requires access to ~/App\_Data"</span></span>

> <span data-ttu-id="521e3-191">在某些情况下，尝试创建用户，或以其他方式处理 ASP.NET 成员资格系统可能会导致页后，可以显示错误*该管理员模块需要访问 ~/App\_数据*。</span><span class="sxs-lookup"><span data-stu-id="521e3-191">Under some circumstances, trying to create users or otherwise work with the ASP.NET membership system can cause the page to display the error *The Admin Module requires access to ~/App\_Data*.</span></span> <span data-ttu-id="521e3-192">发生这种情况是如果 IIS 或 IIS Express 下运行的帐户不具有权限才能创建和写入*应用\_数据*网站根下的文件夹。</span><span class="sxs-lookup"><span data-stu-id="521e3-192">This occurs if the account that IIS or IIS Express is running under does not have permissions to create and write to the *App\_Data* folder under the website root.</span></span> 
> 
> <span data-ttu-id="521e3-193">**解决方法**手动创建*应用\_数据*网站的文件夹。</span><span class="sxs-lookup"><span data-stu-id="521e3-193">**Workaround** Manually create an *App\_Data* folder for the website.</span></span> <span data-ttu-id="521e3-194">请确保应用程序 （通常网络服务） 下运行的 Windows 帐户具有读/写权限的应用程序的根文件夹和子文件夹，例如，应用程序\_数据。</span><span class="sxs-lookup"><span data-stu-id="521e3-194">Then make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as App\_Data.</span></span> <span data-ttu-id="521e3-195">知识库文章中提供了更多详细的信息[SQL Server Express 用户实例化和 ASP.net Web 应用程序项目问题](https://support.microsoft.com/kb/2002980)。</span><span class="sxs-lookup"><span data-stu-id="521e3-195">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>


#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="521e3-196">问题:"无法生成 SQL Server 的用户实例"错误</span><span class="sxs-lookup"><span data-stu-id="521e3-196">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="521e3-197">如果 WebMatrix Web 应用程序使用 SQL Server Express 和 Windows 7 或 Windows Server 2008 R2 上运行 IIS 7.5，可能会看到一个错误，指示 SQL Server 无法在运行时检索用户的本地应用程序路径。</span><span class="sxs-lookup"><span data-stu-id="521e3-197">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="521e3-198">**解决方法**请确保应用程序 （通常网络服务） 下运行的 Windows 帐户如具有读/写权限的应用程序的根文件夹和子文件夹*应用\_数据*.</span><span class="sxs-lookup"><span data-stu-id="521e3-198">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="521e3-199">知识库文章中提供了更多详细的信息[SQL Server Express 用户实例化和 ASP.net Web 应用程序项目问题](https://support.microsoft.com/kb/2002980)。</span><span class="sxs-lookup"><span data-stu-id="521e3-199">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>


#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a><span data-ttu-id="521e3-200">问题： 包含包管理器资源或包管理器密码的文件是 servable 下 IIS 6.0 及更早版本</span><span class="sxs-lookup"><span data-stu-id="521e3-200">Issue: Files that contains package-manager resources or package-manager passwords are servable under IIS 6.0 and earlier</span></span>

> <span data-ttu-id="521e3-201">如果你部署的 ASP.NET Web 页 (Razor) 应用程序使用 RC2 版本中，生成和应用程序包含*password.txt*或*packagesources.txt*文件下*/App\_数据/admin*，IIS 6.0 将处理该文件，如果请求，可能要公开你的包管理器实例的密码。</span><span class="sxs-lookup"><span data-stu-id="521e3-201">If you deploy an ASP.NET Web Pages (Razor) application that was built using the RC2 release, and if the application contains a *password.txt* or *packagesources.txt* file under */App\_Data/admin*, IIS 6.0 will serve the file if requested, potentially exposing the passwords for your package manager instance.</span></span> 
> 
> <span data-ttu-id="521e3-202">**解决方法**重命名*password.txt*或*packagesources.txt*文件为*password.config*或*packagesources.config*.默认情况下，IIS 6.0 不适用于具有文件*.config*扩展。</span><span class="sxs-lookup"><span data-stu-id="521e3-202">**Workaround** Rename the *password.txt* or *packagesources.txt* file to *password.config* or *packagesources.config*. By default, IIS 6.0 does not serve files that have the *.config* extension.</span></span> <span data-ttu-id="521e3-203">(在 IIS 7 中，在任何文件*应用\_数据*文件夹提供服务，因此不需要重命名文件。)</span><span class="sxs-lookup"><span data-stu-id="521e3-203">(In IIS 7, no files in the *App\_Data* folder are served, so you do not need to rename the files.)</span></span>


#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a><span data-ttu-id="521e3-204">问题： 卸载使用 Beta 3 版本安装的包不会完全删除包组件</span><span class="sxs-lookup"><span data-stu-id="521e3-204">Issue: Uninstalling packages installed using the Beta 3 release does not completely remove package components</span></span>

> <span data-ttu-id="521e3-205">如果你安装包在 Beta 3 版本中使用程序包管理器，然后尝试使用当前版本卸载它，未完全卸载包。</span><span class="sxs-lookup"><span data-stu-id="521e3-205">If you installed a package using the package manager in the Beta 3 release and then try to uninstall it using the current release, the package is not completely uninstalled.</span></span> <span data-ttu-id="521e3-206">使用包管理器的**卸载**按钮删除某些组件，但会导致包的库的代码并不能更新*package.config*文件。</span><span class="sxs-lookup"><span data-stu-id="521e3-206">Using the package manager's **Uninstall** button removes some components, but leaves the package's library code and does not update the *package.config* file.</span></span>
> 
> <span data-ttu-id="521e3-207">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="521e3-207">**Workaround** </span></span>  
> <span data-ttu-id="521e3-208">执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="521e3-208">Perform these steps:</span></span>  
> 1. <span data-ttu-id="521e3-209">删除*应用\_Data\packages*文件夹。</span><span class="sxs-lookup"><span data-stu-id="521e3-209">Delete the *App\_Data\packages* folder.</span></span> <span data-ttu-id="521e3-210">这将删除所有包。</span><span class="sxs-lookup"><span data-stu-id="521e3-210">This removes all packages.</span></span>   
> 2. <span data-ttu-id="521e3-211">删除*packages.config*在网站的根目录中的文件。</span><span class="sxs-lookup"><span data-stu-id="521e3-211">Delete the *packages.config* file in the root of the website.</span></span>


#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a><span data-ttu-id="521e3-212">问题： 在 Visual Studio 中，调用的基于 web 的程序包管理器使应用程序脱机</span><span class="sxs-lookup"><span data-stu-id="521e3-212">Issue: In Visual Studio, invoking the web-based package manager takes the application offline</span></span>

> <span data-ttu-id="521e3-213">如果你在 Visual Studio (不 WebMatrix) 中工作，并使用*\_管理员*启动包管理器，Visual Studio 的功能使应用程序脱机，并发布*应用\_offline.htm*到网站根目录中，这使你能够使用包管理器。</span><span class="sxs-lookup"><span data-stu-id="521e3-213">If you are working in Visual Studio (not WebMatrix) and use the *\_admin* functionality to start the package manager, Visual Studio takes the application offline and posts the *app\_offline.htm* into the website root, which disrupts your ability to use the package manager.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="521e3-214">尽管使用基于 web 的程序包管理器界面时，通常会看到此行为，但相同的行为发生如果添加、 删除或修改中的任何文件*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="521e3-214">Although you would most typically see this behavior when using the web-based package manager interface, the same behavior occurs if you add, remove, or modify any files in the *App\_Data* folder.</span></span>
> 
> <span data-ttu-id="521e3-215">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="521e3-215">**Workaround** </span></span>  
> <span data-ttu-id="521e3-216">若要使用 Visual Studio 中的包，而不是基于 web 的程序包管理器使用 NuGet 扩展。</span><span class="sxs-lookup"><span data-stu-id="521e3-216">To work with packages in Visual Studio, use the NuGet extension instead of the web-based package manager.</span></span> <span data-ttu-id="521e3-217">有关信息，请参阅[NuGet 文档](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="521e3-217">For information, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span> <span data-ttu-id="521e3-218">如果你正在使用中的其他文件*应用\_数据*文件夹，请考虑在其他位置来避免此问题保留这些文件。</span><span class="sxs-lookup"><span data-stu-id="521e3-218">If you are working with other files in the *App\_Data* folder, consider keeping the files elsewhere to avoid this issue.</span></span> <span data-ttu-id="521e3-219">如果不可行，删除*应用\_offline.htm*手动文件，或者等待，直到站点重新联机自动 （默认为在 30 秒后）。</span><span class="sxs-lookup"><span data-stu-id="521e3-219">If that's not practical, delete the *app\_offline.htm* file manually or wait until the site comes back online automatically (by default, after 30 seconds).</span></span>


#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="521e3-220">问题： Visual Studio IntelliSense 和项目模板仅在 ASP.NET MVC 3 版本中可用</span><span class="sxs-lookup"><span data-stu-id="521e3-220">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="521e3-221">安装 ASP.NET 网页不还安装 tools for Visual Studio 的 ASP.NET Web Pages 应用程序的智能感知和项目模板等。</span><span class="sxs-lookup"><span data-stu-id="521e3-221">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="521e3-222">**解决方法**若要使用 Visual Studio 中的 ASP.NET Web Pages 应用智能感知和项目模板，ASP.NET MVC 3 RC 通过 Web 平台安装程序的安装或[独立安装程序](https://go.microsoft.com/fwlink/?LinkID=191797)。</span><span class="sxs-lookup"><span data-stu-id="521e3-222">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>


#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="521e3-223">问题： 读取源或其他通过代理服务器的外部数据</span><span class="sxs-lookup"><span data-stu-id="521e3-223">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="521e3-224">如果运行站点的服务器位于代理服务器后面，你可能需要配置中的代理信息*web.config*为了能够读取来自你的站点之外的信息的文件。</span><span class="sxs-lookup"><span data-stu-id="521e3-224">If the server running the site is behind a proxy server, you might need to configure proxy information in the *web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="521e3-225">例如，如果你使用`ReCaptcha`帮助器，帮助器与 reCAPTCHA 服务通信，但可能会阻止由你的代理服务器。</span><span class="sxs-lookup"><span data-stu-id="521e3-225">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="521e3-226">同样，使用在 ASP.NET Web 页中，如源包管理器使用的源可能需要代理配置。</span><span class="sxs-lookup"><span data-stu-id="521e3-226">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="521e3-227">如果你遇到中使用的外部服务或使用源的包的问题，将以下元素放入应用程序的根*web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="521e3-227">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *web.config* file:</span></span>
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> <span data-ttu-id="521e3-228">有关配置代理服务器的详细信息，请参阅[&lt;代理&gt;元素 （网络设置）](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN 网站上。</span><span class="sxs-lookup"><span data-stu-id="521e3-228">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>


#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="521e3-229">问题： 卸载.NET Framework 版本 4 禁用带有 Razor 语法的 ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="521e3-229">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="521e3-230">如果你卸载.NET Framework 版本 4，然后重新安装它，将禁用使用 Razor 语法的 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="521e3-230">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="521e3-231">与页*.cshtml*扩展可能无法正常运行。</span><span class="sxs-lookup"><span data-stu-id="521e3-231">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="521e3-232">ASP.NET Web Pages 机根目录中注册程序集*web.config*文件，并删除.NET Framework 中删除该文件。</span><span class="sxs-lookup"><span data-stu-id="521e3-232">ASP.NET Web Pages registers an assembly in the machine root *web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="521e3-233">重新安装.NET Framework 安装新版本的配置文件中，但不会添加 ASP.NET 网页的程序集引用。</span><span class="sxs-lookup"><span data-stu-id="521e3-233">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="521e3-234">**解决方法**后重新安装.NET Framework，请重新安装 ASP.NET 网页使用 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="521e3-234">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="521e3-235">这将添加到下面的元素*web.config*机根目录，这通常是在以下位置中的文件：</span><span class="sxs-lookup"><span data-stu-id="521e3-235">This adds the following element to the *web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]


#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="521e3-236">问题： 无扩展名的 Url 未找到 IIS 7 或 IIS 7.5 上的.cshtml/.vbhtml 文件</span><span class="sxs-lookup"><span data-stu-id="521e3-236">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="521e3-237">在 IIS 7 或 IIS 7.5 上，如下所示 URL 的请求不能找到页具有*.cshtml*或*.vbhtml*扩展：</span><span class="sxs-lookup"><span data-stu-id="521e3-237">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="521e3-238">由于 URL 重写未启用默认情况下为 IIS 7 或 IIS 7.5，因此会出现此问题。</span><span class="sxs-lookup"><span data-stu-id="521e3-238">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="521e3-239">很可能的方案是，你看不见问题时测试使用本地 IIS Express，但在将你的网站部署到托管的网站时，会遇到它。</span><span class="sxs-lookup"><span data-stu-id="521e3-239">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="521e3-240">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-240">**Workaround**</span></span>
> 
> - <span data-ttu-id="521e3-241">如果你可以控制在服务器计算机，在服务器计算机上安装的更新中所述[有可用启用某些 IIS 7.0 或 IIS 7.5 的处理程序，来处理请求其 Url 不要以句点结尾的更新](https://support.microsoft.com/kb/980368)。</span><span class="sxs-lookup"><span data-stu-id="521e3-241">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="521e3-242">如果您没有对服务器计算机的控制 （例如，您要部署到托管网站），将以下代码添加到网站的*web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="521e3-242">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *web.config* file:</span></span> 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]


#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="521e3-243">问题： 应用程序部署到不具有 SQL Server Compact 安装的计算机</span><span class="sxs-lookup"><span data-stu-id="521e3-243">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="521e3-244">其中 SQL Server Compact 未安装的计算机上可以运行的应用程序包括 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="521e3-244">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="521e3-245">Microsoft WebMatrix 1.0 自动为你复制这些二进制文件，并执行相应*web.config*文件转换。</span><span class="sxs-lookup"><span data-stu-id="521e3-245">Microsoft WebMatrix 1.0 automatically copies these binaries for you and performs the appropriate *web.config* file transforms.</span></span>
> 
> <span data-ttu-id="521e3-246">**解决方法**如果你需要将这些文件复制并使*web.config*文件更改手动，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="521e3-246">**Workaround** If you need to copy these files and make the *web.config* file changes manually, do the following:</span></span>
> 
> 1. <span data-ttu-id="521e3-247">将复制到的数据库引擎程序集*Bin*文件夹 （和子文件夹） 的目标计算机上的应用程序：</span><span class="sxs-lookup"><span data-stu-id="521e3-247">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span>  
> 
>    - <span data-ttu-id="521e3-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span><span class="sxs-lookup"><span data-stu-id="521e3-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span></span>  
>        <span data-ttu-id="521e3-249">**to** *\Bin*</span><span class="sxs-lookup"><span data-stu-id="521e3-249">**to** *\Bin*</span></span>
>    - <span data-ttu-id="521e3-250">复制<em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\</em><strong><em>到</em></strong>\Bin\x86\*</span><span class="sxs-lookup"><span data-stu-id="521e3-250">Copy <em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\</em><strong><em>to</em></strong>\Bin\x86\*</span></span>
>    - <span data-ttu-id="521e3-251">复制<em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\</em>\* <strong>到</strong><em>\Bin\amd64</em></span><span class="sxs-lookup"><span data-stu-id="521e3-251">Copy <em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\</em>\* <strong>to</strong><em>\Bin\amd64</em></span></span>
> 
> 2. <span data-ttu-id="521e3-252">在网站的根文件夹中创建或打开*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="521e3-252">In the root folder of the website, create or open a *web.config* file.</span></span> <span data-ttu-id="521e3-253">(在 WebMatrix 1.0 中，此文件类型是如果你单击可用**所有**中**选择文件类型**对话框。)</span><span class="sxs-lookup"><span data-stu-id="521e3-253">(In WebMatrix 1.0, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="521e3-254">添加以下元素的子级`<configuration>`元素 (而不是在`<system.web>`元素):</span><span class="sxs-lookup"><span data-stu-id="521e3-254">Add the following element as a child of the `<configuration>` element (not inside the `<system.web>` element):</span></span>
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]


#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="521e3-255">问题:"数据库"和"WebGrid"帮助程序中不起作用中等信任在 Visual Basic 中</span><span class="sxs-lookup"><span data-stu-id="521e3-255">Issue: "Database" and "WebGrid" helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="521e3-256">如果你使用的 Visual Basic (创建*.vbhtml*文件)，则`Database`和`WebGrid`如果应用程序设置为使用中等信任帮助器将无法工作。</span><span class="sxs-lookup"><span data-stu-id="521e3-256">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="521e3-257">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-257">**Workaround**</span></span>  
> <span data-ttu-id="521e3-258">如果你使用 Visual Studio 2010，你可以通过安装 Service Pack 1 发行版来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="521e3-258">If you use Visual Studio 2010, you can resolve this problem by installing the Service Pack 1 release.</span></span> <span data-ttu-id="521e3-259">可用的 SP1 版本的最终版本之前，你可以下载从 SP1 Beta 版本[Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) Microsoft Download Center 上的页。</span><span class="sxs-lookup"><span data-stu-id="521e3-259">Until the final version of the SP1 release is available, you can download the Beta version of SP1 from the [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) page on the Microsoft Download Center.</span></span>   
>   
> <span data-ttu-id="521e3-260">如果这不可行，或如果不使用 Visual Studio 2010，则可以暂时设置用于完全信任的应用程序。</span><span class="sxs-lookup"><span data-stu-id="521e3-260">If this is not practical, or if you do not use Visual Studio 2010, you can temporarily set the application to use Full Trust.</span></span>


#### <a name="issue-applicationpart-resources-are-externally-accessible"></a><span data-ttu-id="521e3-261">问题:"ApplicationPart"资源是从外部访问</span><span class="sxs-lookup"><span data-stu-id="521e3-261">Issue: "ApplicationPart" resources are externally accessible</span></span>

> <span data-ttu-id="521e3-262">如果程序集包含派生自的对象`ApplicationPart`类，程序集的资源公开的`ResourceRouteHandler`类。</span><span class="sxs-lookup"><span data-stu-id="521e3-262">If an assembly contains objects that derives from the `ApplicationPart` class, that assembly's resources are exposed by the `ResourceRouteHandler` class.</span></span> <span data-ttu-id="521e3-263">以下列 URL 为例：</span><span class="sxs-lookup"><span data-stu-id="521e3-263">For example, consider the following URL:</span></span>  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> <span data-ttu-id="521e3-264">此请求下载中的资源字符串的所有*System.Web.WebPages.Administration.dll*程序集。</span><span class="sxs-lookup"><span data-stu-id="521e3-264">This request downloads all of the resource strings in the *System.Web.WebPages.Administration.dll* assembly.</span></span> <span data-ttu-id="521e3-265">下载的所有嵌入的资源 （甚至那些不应为静态内容提供）。</span><span class="sxs-lookup"><span data-stu-id="521e3-265">All of the embedded resources (even those that are not intended to be served as static content) are downloaded.</span></span> <span data-ttu-id="521e3-266">如果嵌入的资源包含敏感信息，这可以是一个安全风险。</span><span class="sxs-lookup"><span data-stu-id="521e3-266">If the embedded resources contain sensitive information, this can represent a security risk.</span></span> 
> 
> <span data-ttu-id="521e3-267">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="521e3-267">**Workaround** </span></span>  
> <span data-ttu-id="521e3-268">如果你创建**ApplicationPart**对象，请确保与该关联的嵌入的资源**ApplicationPart**对象的程序集不包含敏感信息。</span><span class="sxs-lookup"><span data-stu-id="521e3-268">If you create an **ApplicationPart** object, make sure that the embedded resources associated with that **ApplicationPart** object's assembly do not contain sensitive information.</span></span>


<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a><span data-ttu-id="521e3-269">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="521e3-269">WebMatrix</span></span>

> [!NOTE]
> <span data-ttu-id="521e3-270">WebMatrix 安装问题的信息，请参阅[WebMatrix 安装问题](#Known_Issues_Installation)本文档前面的。</span><span class="sxs-lookup"><span data-stu-id="521e3-270">For information about installation issues for WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>


<span data-ttu-id="521e3-271">文档本部分介绍 WebMatrix 开发环境的已知的问题。</span><span class="sxs-lookup"><span data-stu-id="521e3-271">This section of the document describes known issues for the WebMatrix development environment.</span></span>

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a><span data-ttu-id="521e3-272">问题： 用户名或密码的 web.config 文件中的数据库连接字符串中的更改不会反映在数据库工作区</span><span class="sxs-lookup"><span data-stu-id="521e3-272">Issue: Changes in the username or password of a database connection string in a web.config file are not reflected in the Databases workspace</span></span>

> <span data-ttu-id="521e3-273">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-273">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="521e3-274">在*web.config*文件中，更改连接字符串中的数据库名称 （例如，将"1"添加到它）。</span><span class="sxs-lookup"><span data-stu-id="521e3-274">In the *web.config* file, change the database name in the connection string (for example, add "1" to it).</span></span>
> 2. <span data-ttu-id="521e3-275">保存*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="521e3-275">Save the *web.config* file.</span></span>
> 3. <span data-ttu-id="521e3-276">单击**数据库**和刷新。</span><span class="sxs-lookup"><span data-stu-id="521e3-276">Click **Databases** and refresh.</span></span>
> 4. <span data-ttu-id="521e3-277">更改中的连接字符串中的数据库名称*web.config*回原始的数据库名称的文件。</span><span class="sxs-lookup"><span data-stu-id="521e3-277">Change the database name in the connection string in the *web.config* file back to the original database name.</span></span>
> 5. <span data-ttu-id="521e3-278">保存*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="521e3-278">Save the *web.config* file.</span></span>
> 6. <span data-ttu-id="521e3-279">单击**数据库**和刷新。</span><span class="sxs-lookup"><span data-stu-id="521e3-279">Click **Databases** and refresh.</span></span>


#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a><span data-ttu-id="521e3-280">问题： 无法删除文件夹创建的 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="521e3-280">Issue: Folders created by WebMatrix cannot be deleted</span></span>

> <span data-ttu-id="521e3-281">如果使用提升的权限运行 WebMatrix (即你开始使用 WebMatrix**以管理员身份运行**Windows 中的选项)，不能使用 Windows 资源管理器删除创建的 WebMatrix 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="521e3-281">If WebMatrix is running using elevated permissions (that is, you started WebMatrix using the **Run as Administrator** option in Windows), folders that are created by WebMatrix cannot be deleted using Windows Explorer.</span></span>
> 
> <span data-ttu-id="521e3-282">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-282">**Workaround**</span></span>  
> <span data-ttu-id="521e3-283">运行 Windows 资源管理器使用提升的权限。</span><span class="sxs-lookup"><span data-stu-id="521e3-283">Run Windows Explorer using elevated permissions.</span></span> <span data-ttu-id="521e3-284">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="521e3-284">Follow these steps:</span></span>  
> 
> 1. <span data-ttu-id="521e3-285">在 Windows 中，单击**启动**。</span><span class="sxs-lookup"><span data-stu-id="521e3-285">In Windows, click **Start**.</span></span>
> 2. <span data-ttu-id="521e3-286">输入"Windows 资源管理器"，然后右键单击的项**Windows 资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="521e3-286">Enter "Windows Explorer" and right-click the entry for **Windows Explorer**.</span></span>
> 3. <span data-ttu-id="521e3-287">单击**以管理员身份运行**。</span><span class="sxs-lookup"><span data-stu-id="521e3-287">Click **Run as Administrator**.</span></span> <span data-ttu-id="521e3-288">然后，你可以删除这些文件夹。</span><span class="sxs-lookup"><span data-stu-id="521e3-288">You can then delete the folders.</span></span>


#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="521e3-289">问题： WebMatrix 1.0 不能执行某些任务需要提升权限</span><span class="sxs-lookup"><span data-stu-id="521e3-289">Issue: WebMatrix 1.0 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="521e3-290">WebMatrix 1.0 程序无法执行某些任务，需要提升，例如在以下情况下安装其他组件：</span><span class="sxs-lookup"><span data-stu-id="521e3-290">WebMatrix 1.0 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="521e3-291">在 Windows Vista 或 Windows 7，使用不具备管理员权限的帐户登录和用户帐户控制 (UAC) 处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="521e3-291">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="521e3-292">您正在使用 Microsoft Windows XP 或 Microsoft Windows Server 2003。</span><span class="sxs-lookup"><span data-stu-id="521e3-292">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="521e3-293">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-293">**Workaround**</span></span>  
> <span data-ttu-id="521e3-294">在 WebMatrix 1.0 中的大多数任务不需要管理权限。</span><span class="sxs-lookup"><span data-stu-id="521e3-294">Most tasks in WebMatrix 1.0 do not require administrative permission.</span></span> <span data-ttu-id="521e3-295">对于那些确实，你可以执行该操作作为管理员，或请按照下列步骤：</span><span class="sxs-lookup"><span data-stu-id="521e3-295">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="521e3-296">在 Windows Vista 或 Windows 7 上，启用 UAC。</span><span class="sxs-lookup"><span data-stu-id="521e3-296">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="521e3-297">在 Windows XP 中，将用户添加到管理员安全组。</span><span class="sxs-lookup"><span data-stu-id="521e3-297">On Windows XP, add the user to the Administrators security group.</span></span>


#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="521e3-298">问题:"从 Web 库的站点"处于禁用状态</span><span class="sxs-lookup"><span data-stu-id="521e3-298">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="521e3-299">**站点从 Web 库**如果未安装 Web 平台安装程序 3.0 选项被禁用。</span><span class="sxs-lookup"><span data-stu-id="521e3-299">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="521e3-300">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-300">**Workaround**</span></span>  
> <span data-ttu-id="521e3-301">安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="521e3-301">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>


#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="521e3-302">问题： Google Chrome 不能作为运行选项</span><span class="sxs-lookup"><span data-stu-id="521e3-302">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="521e3-303">在浏览器的列表中不显示 Google Chrome**运行**上**主页**选项卡。</span><span class="sxs-lookup"><span data-stu-id="521e3-303">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="521e3-304">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-304">**Workaround**</span></span>  
> <span data-ttu-id="521e3-305">某些版本的 Google Chrome 并不能注册正确与 Windows 中的默认程序功能。</span><span class="sxs-lookup"><span data-stu-id="521e3-305">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="521e3-306">一种解决方法，启动 Google Chrome 中，单击*自定义和控制 Google Chrome*菜单上，单击*选项*，然后单击*请 Google Chrome 我默认浏览器*。</span><span class="sxs-lookup"><span data-stu-id="521e3-306">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>


#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="521e3-307">问题:"外键"对话框中不允许输入为主键</span><span class="sxs-lookup"><span data-stu-id="521e3-307">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="521e3-308">**外键**对话框中不允许你从主键表中输入的主键名称。</span><span class="sxs-lookup"><span data-stu-id="521e3-308">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="521e3-309">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-309">**Workaround**</span></span>  
> <span data-ttu-id="521e3-310">这是有意。</span><span class="sxs-lookup"><span data-stu-id="521e3-310">This is intentional.</span></span> <span data-ttu-id="521e3-311">不需要输入主键表的主键的名称。</span><span class="sxs-lookup"><span data-stu-id="521e3-311">You do not need to enter the name of the primary key from the primary key table.</span></span>


#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a><span data-ttu-id="521e3-312">问题： IntelliSense 不能在 WebMatrix 的 Razor 语法、 C# 或 Visual Basic</span><span class="sxs-lookup"><span data-stu-id="521e3-312">Issue: IntelliSense is not available in WebMatrix for Razor syntax, C#, or Visual Basic</span></span>

> <span data-ttu-id="521e3-313">在 WebMatrix 中用于 HTML 和 CSS 支持 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="521e3-313">IntelliSense is supported in WebMatrix for HTML and CSS.</span></span> <span data-ttu-id="521e3-314">但是，它也无法供其他语言。</span><span class="sxs-lookup"><span data-stu-id="521e3-314">However, it is not available for other languages.</span></span> 
> 
> <span data-ttu-id="521e3-315">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="521e3-315">**Workaround** </span></span>  
> <span data-ttu-id="521e3-316">无。</span><span class="sxs-lookup"><span data-stu-id="521e3-316">None.</span></span>


#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a><span data-ttu-id="521e3-317">问题： 用于 HTML 和 CSS IntelliSense 建议不是上下文相关的元素</span><span class="sxs-lookup"><span data-stu-id="521e3-317">Issue: IntelliSense for HTML and CSS suggests elements that are not contextually appropriate</span></span>

> <span data-ttu-id="521e3-318">在 WebMatrix 中标记的 IntelliSense 支持使用 HTML [XHTML 1.0 Transitional 架构](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional)和 CSS 使用[CSS 2.1 架构](http://www.w3.org/TR/CSS2/)。</span><span class="sxs-lookup"><span data-stu-id="521e3-318">IntelliSense for markup in WebMatrix supports HTML using the [XHTML 1.0 Transitional schema](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) and CSS using the [CSS 2.1 schema](http://www.w3.org/TR/CSS2/).</span></span> <span data-ttu-id="521e3-319">IntelliSense 基于这些特定的架构，因为某些标记、 属性可能不适合用于当前页或样式定义建议。</span><span class="sxs-lookup"><span data-stu-id="521e3-319">Because IntelliSense is based on these specific schemas, certain tags, attributes, or properties might be suggested that are not appropriate for the current page or style definition.</span></span> <span data-ttu-id="521e3-320">为 HTML，它还可能导致意外的建议，在内容中，可能会被解释为格式不正确 XHTML （例如，当未关闭标记）。</span><span class="sxs-lookup"><span data-stu-id="521e3-320">For HTML, it can also lead to unexpected suggestions in content that might be interpreted as malformed XHTML (for example, when tags are not closed).</span></span> <span data-ttu-id="521e3-321">此问题可能会更明显，如果插入点位于一个不完整的标记;在这种情况下，IntelliSense 可能建议新开始标记，或提供其他不正确的建议。</span><span class="sxs-lookup"><span data-stu-id="521e3-321">This issue might be more noticeable if the insertion point is inside an incomplete tag; in that case, IntelliSense might suggest new opening tags or offer other incorrect suggestions.</span></span> 
> 
> <span data-ttu-id="521e3-322">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="521e3-322">**Workaround** </span></span>  
> <span data-ttu-id="521e3-323">对于 HTML，请确保你正在在格式正确，完成 XHTML 页面内。</span><span class="sxs-lookup"><span data-stu-id="521e3-323">For HTML, make sure that you are working within a well-formed, complete XHTML page.</span></span> <span data-ttu-id="521e3-324">针对 CSS，目前没有解决方法。</span><span class="sxs-lookup"><span data-stu-id="521e3-324">For CSS, there is no workaround.</span></span>


#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a><span data-ttu-id="521e3-325">问题： IntelliSense 不会被调用键入时</span><span class="sxs-lookup"><span data-stu-id="521e3-325">Issue: IntelliSense is not invoked while you type</span></span>

> <span data-ttu-id="521e3-326">有时，如 HTML 或 CSS 在编辑器中输入可能不调用 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="521e3-326">At times, IntelliSense might not be invoked as HTML or CSS is being entered in the editor.</span></span> <span data-ttu-id="521e3-327">具体而言，这可能会发生时插入点，则直接旁边另一个元素或在文件末尾。</span><span class="sxs-lookup"><span data-stu-id="521e3-327">In particular, this might happen when the insertion point is directly next to another element or at the end of a file.</span></span> 
> 
> <span data-ttu-id="521e3-328">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="521e3-328">**Workaround** </span></span>  
> <span data-ttu-id="521e3-329">请确保没有绕插入点的空白和插入点不在文件末尾。</span><span class="sxs-lookup"><span data-stu-id="521e3-329">Make sure that there is whitespace around the insertion point and that the insertion point is not at the end of a file.</span></span> <span data-ttu-id="521e3-330">你也可以通过按 Ctrl + Space 手动调用 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="521e3-330">You can also invoke IntelliSense manually by pressing Ctrl+Space.</span></span>


#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a><span data-ttu-id="521e3-331">问题： 没有用户界面是可用于禁用 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="521e3-331">Issue: No UI is available for disabling IntelliSense</span></span>

> <span data-ttu-id="521e3-332">WebMatrix 1.0 允许禁用 IntelliSense 的任何 UI 或笔势。</span><span class="sxs-lookup"><span data-stu-id="521e3-332">WebMatrix 1.0 provides no UI or gesture for disabling IntelliSense.</span></span> 
> 
> <span data-ttu-id="521e3-333">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="521e3-333">**Workaround** </span></span>  
> <span data-ttu-id="521e3-334">启动 WebMatrix 使用以下命令，其中包括禁用 IntelliSense 的交换机：</span><span class="sxs-lookup"><span data-stu-id="521e3-334">Start WebMatrix using the following command, which includes a switch that disables IntelliSense:</span></span>  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`


<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a><span data-ttu-id="521e3-335">IIS Express</span><span class="sxs-lookup"><span data-stu-id="521e3-335">IIS Express</span></span>

<span data-ttu-id="521e3-336">IIS Express 具有其自己的自述文件，它是可通过以下 URL:</span><span class="sxs-lookup"><span data-stu-id="521e3-336">IIS Express has its own readme file, which is available at the following URL:</span></span>

[<span data-ttu-id="521e3-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="521e3-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span></span>](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a><span data-ttu-id="521e3-338">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="521e3-338">SQL Server Compact</span></span>

<span data-ttu-id="521e3-339">SQL Server Compact 具有其自己的自述文件，它是可通过以下 URL:</span><span class="sxs-lookup"><span data-stu-id="521e3-339">SQL Server Compact has its own readme file, which is available at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

<span data-ttu-id="521e3-340">有关涉及 WebMatrix 的一部分安装 SQL Server Compact 的问题的信息，请参阅[WebMatrix 安装问题](#Known_Issues_Installation)本文档前面的。</span><span class="sxs-lookup"><span data-stu-id="521e3-340">For information about issues that involve installing SQL Server Compact as part of WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

### <a id="Known_Issues_Installing_Applications"></a>  <span data-ttu-id="521e3-341">安装应用程序</span><span class="sxs-lookup"><span data-stu-id="521e3-341">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="521e3-342">问题： 安装应用程序可能需要长时间如果用户的 My Documents 文件夹重定向到网络共享</span><span class="sxs-lookup"><span data-stu-id="521e3-342">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="521e3-343">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-343">**Workaround**</span></span>  
> <span data-ttu-id="521e3-344">无。</span><span class="sxs-lookup"><span data-stu-id="521e3-344">None.</span></span> <span data-ttu-id="521e3-345">应用程序可能需要一段时间才能安装，但将正确安装。</span><span class="sxs-lookup"><span data-stu-id="521e3-345">The application might take a while to install, but will install correctly.</span></span>


### <a id="Known_Issues_Publishing_Applications"></a>  <span data-ttu-id="521e3-346">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="521e3-346">Publishing Applications</span></span>

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a><span data-ttu-id="521e3-347">发布 SQL Compact 数据库时需要问题:"无法获得的权限"错误</span><span class="sxs-lookup"><span data-stu-id="521e3-347">Issue: "Required permissions cannot be acquired" error when publishing a SQL Compact Database</span></span>

> <span data-ttu-id="521e3-348">WebMatrix 不完全支持为 SQL Server Compact 的支持的二进制文件部署到正在运行.NET Framework 版本 3.5 使用中等信任配置的服务器。</span><span class="sxs-lookup"><span data-stu-id="521e3-348">WebMatrix does not fully support deploying supporting binaries for SQL Server Compact to a server that is running .NET Framework version 3.5 with a medium trust configuration.</span></span>
> 
> <span data-ttu-id="521e3-349">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-349">**Workaround**</span></span>  
> <span data-ttu-id="521e3-350">首选的解决方法是在服务器上安装.NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="521e3-350">The preferred workaround is to install the .NET Framework 4 on the server.</span></span> <span data-ttu-id="521e3-351">或者，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="521e3-351">Alternatively, do the following:</span></span>
> 
> 1. <span data-ttu-id="521e3-352">添加到下列元素`SecurityClasses`主题中*Web\_MediumTrust.config*文件：</span><span class="sxs-lookup"><span data-stu-id="521e3-352">Add the following elements to the `SecurityClasses` section in *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. <span data-ttu-id="521e3-353">创建一个新权限集*Web\_MediumTrust.config*文件所需的以下权限：</span><span class="sxs-lookup"><span data-stu-id="521e3-353">Create a new permission set in the *Web\_MediumTrust.config* file with the following required permissions:</span></span>
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. <span data-ttu-id="521e3-354">应用将权限设置为 SQL Server Compact 通过将以下元素放入*Web\_MediumTrust.config*文件：</span><span class="sxs-lookup"><span data-stu-id="521e3-354">Apply the permission set to SQL Server Compact by putting the following elements in the *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample8.html)]


#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a><span data-ttu-id="521e3-355">问题： 库和 PhpBB web 应用程序在发布后显示"服务不可用"错误</span><span class="sxs-lookup"><span data-stu-id="521e3-355">Issue: Gallery and PhpBB web applications display a "Service is unavailable" error after publishing</span></span>

> <span data-ttu-id="521e3-356">在某些情况下，发布的应用程序将导致"服务不可用"错误。</span><span class="sxs-lookup"><span data-stu-id="521e3-356">Under some circumstances, publishing an application causes a "service is unavailable" error.</span></span>
> 
> <span data-ttu-id="521e3-357">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-357">**Workaround**</span></span>  
> <span data-ttu-id="521e3-358">在 WebMatrix 中，添加一个反斜杠 (\)到中的服务器名称的末尾**发布设置**窗口，然后将发布再次将应用程序。</span><span class="sxs-lookup"><span data-stu-id="521e3-358">In WebMatrix, add a backslash (\) to the end of the server name in the **Publish Settings** window and then publish the application again.</span></span>


#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a><span data-ttu-id="521e3-359">问题： Moodle 网站布局和链接后中断发布</span><span class="sxs-lookup"><span data-stu-id="521e3-359">Issue: Moodle website layout and links are broken after publishing</span></span>

> <span data-ttu-id="521e3-360">发布 Moodle 应用程序后，应用程序无法正常工作。</span><span class="sxs-lookup"><span data-stu-id="521e3-360">After you publish a Moodle application, the application does not work correctly.</span></span>
> 
> <span data-ttu-id="521e3-361">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-361">**Workaround**</span></span>  
> <span data-ttu-id="521e3-362">在 WebMatrix 中，将斜杠 （/） 添加到末尾**站点名称**字段**发布设置**窗口，然后将发布再次将应用程序。</span><span class="sxs-lookup"><span data-stu-id="521e3-362">In WebMatrix, add a slash (/) to the end of the **Site Name** field in the **Publish Settings** window and then publish the application again.</span></span>


#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a><span data-ttu-id="521e3-363">问题： 发布 nopCommerce 失败，出现数据库错误</span><span class="sxs-lookup"><span data-stu-id="521e3-363">Issue: Publishing nopCommerce fails with a database error</span></span>

> <span data-ttu-id="521e3-364">发布 nopCommerce 失败并报告数据库错误，如"插入 nop\_日志表失败。"</span><span class="sxs-lookup"><span data-stu-id="521e3-364">Publishing nopCommerce fails and reports a database error like "Insert into the nop\_log table failed."</span></span>
> 
> <span data-ttu-id="521e3-365">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-365">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="521e3-366">在 WebMatrix 中，单击**运行**以启动 nopCommerce 本地。</span><span class="sxs-lookup"><span data-stu-id="521e3-366">In WebMatrix, click **Run** to launch nopCommerce locally.</span></span>
> 2. <span data-ttu-id="521e3-367">登录到管理页。</span><span class="sxs-lookup"><span data-stu-id="521e3-367">Log into the administration page.</span></span>
> 3. <span data-ttu-id="521e3-368">单击**系统**菜单。</span><span class="sxs-lookup"><span data-stu-id="521e3-368">Click the **System** menu.</span></span>
> 4. <span data-ttu-id="521e3-369">单击**日志**选项。</span><span class="sxs-lookup"><span data-stu-id="521e3-369">Click the **Log** option.</span></span>
> 5. <span data-ttu-id="521e3-370">单击**清除日志**按钮。</span><span class="sxs-lookup"><span data-stu-id="521e3-370">Click the **Clear Log** button.</span></span>
> 6. <span data-ttu-id="521e3-371">再次发布 nopCommerce。</span><span class="sxs-lookup"><span data-stu-id="521e3-371">Publish nopCommerce again.</span></span>


#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a><span data-ttu-id="521e3-372">问题： 当你下载的已发布的站点 Silverstripe CMS 显示"HTTP 500 PHP FCGI 错误"</span><span class="sxs-lookup"><span data-stu-id="521e3-372">Issue: Silverstripe CMS displays a "HTTP 500 PHP FCGI Error" when you download a published site</span></span>

> <span data-ttu-id="521e3-373">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-373">**Workaround**</span></span>  
> <span data-ttu-id="521e3-374">单击后**下载发布站点**，跳过`silverstripe-cache/manifest_main`中**发布预览**。</span><span class="sxs-lookup"><span data-stu-id="521e3-374">After you click **Download published site**, skip `silverstripe-cache/manifest_main` in **Publish Preview**.</span></span> <span data-ttu-id="521e3-375">此文件用于缓存目的，并且是特定于每台计算机。</span><span class="sxs-lookup"><span data-stu-id="521e3-375">This file is used for caching purposes and is specific to each computer.</span></span>


#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a><span data-ttu-id="521e3-376">问题： 从属文本显示"服务器错误 '/' 应用程序中"时下载已发布的站点</span><span class="sxs-lookup"><span data-stu-id="521e3-376">Issue: Subtext displays "Server Error in '/' Application" when you download a published site</span></span>

> <span data-ttu-id="521e3-377">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-377">**Workaround**</span></span>  
> <span data-ttu-id="521e3-378">打开站点的*web.config*文件并将替换 SQL Server 管理员凭据 （"sa"凭据） 的用户 ID 和数据库连接字符串中的密码。</span><span class="sxs-lookup"><span data-stu-id="521e3-378">Open the site's *web.config* file and replace the user ID and password in the database connection string with the SQL Server administrator credentials (the "sa" credentials).</span></span>
> 
> <span data-ttu-id="521e3-379">或者，遵循这些步骤，才能让你登录时所用的用户帐户`db_owner`权限：</span><span class="sxs-lookup"><span data-stu-id="521e3-379">Alternatively, follow these steps in order to give the user account you are logged in with `db_owner` permissions:</span></span>
> 
> 1. <span data-ttu-id="521e3-380">安装 SQL Server Management Studio 使用 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="521e3-380">Install SQL Server Management Studio using the Web Platform Installer.</span></span>
> 2. <span data-ttu-id="521e3-381">连接到本地的 SQL Server Express 实例 (默认情况下， `.\SQLEXPRESS`)。</span><span class="sxs-lookup"><span data-stu-id="521e3-381">Connect to the local SQL Server Express instance (by default, `.\SQLEXPRESS`).</span></span>
> 3. <span data-ttu-id="521e3-382">单击**数据库** &gt; *[localSubtextDatabase]* &gt; **安全** &gt; **用户**&gt; *[localSubtextUser*] (默认值是`subtextuser`]，右键单击，然后单击**属性**。</span><span class="sxs-lookup"><span data-stu-id="521e3-382">Click **Databases** &gt; *[localSubtextDatabase]* &gt; **Security** &gt; **Users** &gt; *[localSubtextUser*] (default is `subtextuser`], right-click, and click **Properties**.</span></span>
> 4. <span data-ttu-id="521e3-383">选择**db\_所有者**角色成员资格部分中。</span><span class="sxs-lookup"><span data-stu-id="521e3-383">Select **db\_owner** in the role membership section.</span></span>


#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="521e3-384">问题： 站点可能无法在发布如果"目标 URL"字段不 http:// 或 https:// 开头的前缀后</span><span class="sxs-lookup"><span data-stu-id="521e3-384">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="521e3-385">在**发布设置**对话框中，如果目标 URL 不以开头`http://`或`https://`，在部署之后，站点可能不工作。</span><span class="sxs-lookup"><span data-stu-id="521e3-385">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="521e3-386">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-386">**Workaround**</span></span>  
> <span data-ttu-id="521e3-387">请确保在发布站点时中的目标 URL 之前**发布设置**对话框开头`http://`或`https://`。</span><span class="sxs-lookup"><span data-stu-id="521e3-387">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>


#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="521e3-388">问题： 发布 MySQL 数据库失败，出现错误"未能发布数据库。</span><span class="sxs-lookup"><span data-stu-id="521e3-388">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="521e3-389">可能的原因是远程数据库无法运行脚本。"</span><span class="sxs-lookup"><span data-stu-id="521e3-389">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="521e3-390">多种原因可能会导致错误。</span><span class="sxs-lookup"><span data-stu-id="521e3-390">The error can occur for a number of reasons.</span></span> <span data-ttu-id="521e3-391">你可以看到此错误的原因之一是如果数据库脚本包含单引号字符 （'） 和目标 MySQL 数据库的默认字符集不为 utf-8。</span><span class="sxs-lookup"><span data-stu-id="521e3-391">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="521e3-392">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-392">**Workaround**</span></span>  
> <span data-ttu-id="521e3-393">设置的默认字符集远程 MySQL 数据库为 utf-8。</span><span class="sxs-lookup"><span data-stu-id="521e3-393">Set the default character set for the remote MySQL database to UTF-8.</span></span>


#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a><span data-ttu-id="521e3-394">问题： 某些链接中是不可见 DotNetNuke 后发布或从其下载站点</span><span class="sxs-lookup"><span data-stu-id="521e3-394">Issue: Some links are not visible in DotNetNuke after publishing or downloading the site</span></span>

> <span data-ttu-id="521e3-395">如果发布或下载 DotNetNuke 站点时，你可能需要清除缓存以获取要在站点上显示的新链接。</span><span class="sxs-lookup"><span data-stu-id="521e3-395">If you publish or download a DotNetNuke site, you might need to clear the cache to get the new links to appear on the site.</span></span>
> 
> <span data-ttu-id="521e3-396">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-396">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="521e3-397">"主机"以登录。</span><span class="sxs-lookup"><span data-stu-id="521e3-397">Log in as "Host".</span></span>
> 2. <span data-ttu-id="521e3-398">转到的主机菜单并选择**主机设置**。</span><span class="sxs-lookup"><span data-stu-id="521e3-398">Go to the host menu and select **Host Settings**.</span></span>
> 3. <span data-ttu-id="521e3-399">向下和下的滚动**高级设置**，展开**性能设置**。</span><span class="sxs-lookup"><span data-stu-id="521e3-399">Scroll down and under **Advanced Settings**, expand **Performance Settings**.</span></span>
> 4. <span data-ttu-id="521e3-400">单击**清除缓存**页的链接。</span><span class="sxs-lookup"><span data-stu-id="521e3-400">Click the **Clear Cache** link for pages.</span></span>
> 5. <span data-ttu-id="521e3-401">转到页面底部，重新启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="521e3-401">Go to the bottom of the page and restart the application.</span></span>


#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a><span data-ttu-id="521e3-402">问题： 一些链接 AtomSite 中的可能会中断后你下载的已发布的站点</span><span class="sxs-lookup"><span data-stu-id="521e3-402">Issue: Some links in AtomSite are broken after you download a published site</span></span>

> <span data-ttu-id="521e3-403">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-403">**Workaround**</span></span>  
> <span data-ttu-id="521e3-404">在*service.config*文件， *users.config*文件，以及所有*.xml*文件，将 URL 字符串 (例如， `http://myhost.com/atomsite`) 替换为本地 (例如， `http://localhost:1239`).</span><span class="sxs-lookup"><span data-stu-id="521e3-404">In the *service.config* file, *users.config* file, and all *.xml* files, replace the URL string (for example, `http://myhost.com/atomsite`) with the local one (for example, `http://localhost:1239`).</span></span>


#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a><span data-ttu-id="521e3-405">问题： WordPress 等基于 MySQL 的应用程序不能发布，并将数据库错误报告</span><span class="sxs-lookup"><span data-stu-id="521e3-405">Issue: MySQL-based applications like WordPress fail to publish and report a database error</span></span>

> <span data-ttu-id="521e3-406">默认情况下，WebMatrix utf-8 字符集安装 MySQL。</span><span class="sxs-lookup"><span data-stu-id="521e3-406">By default, WebMatrix installs MySQL with the UTF-8 character set.</span></span> <span data-ttu-id="521e3-407">如果你将 MySQL 安装在你自己和设置的字符不是 utf-8 （例如，它是 Latin1），数据库的发布过程可能会失败。</span><span class="sxs-lookup"><span data-stu-id="521e3-407">If you install MySQL on your own, and the character set is not UTF-8 (for example, it is Latin1), the publish process for databases might fail.</span></span>
> 
> <span data-ttu-id="521e3-408">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-408">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="521e3-409">更改为 utf-8 的 MySQL 的字符集。</span><span class="sxs-lookup"><span data-stu-id="521e3-409">Change the character set for MySQL to UTF-8.</span></span> <span data-ttu-id="521e3-410">(有关详细信息，请参阅[服务器字符集和排序规则](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html)MySQL 网站上。)</span><span class="sxs-lookup"><span data-stu-id="521e3-410">(For details, see [Server Character Set and Collation](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) on the MySQL website.)</span></span>
> 2. <span data-ttu-id="521e3-411">重新安装应用程序。</span><span class="sxs-lookup"><span data-stu-id="521e3-411">Reinstall the application.</span></span>
> 3. <span data-ttu-id="521e3-412">重新发布应用程序。</span><span class="sxs-lookup"><span data-stu-id="521e3-412">Republish the application.</span></span>


#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a><span data-ttu-id="521e3-413">问题:"下载发布站点"具有基于浏览器的安装程序的应用程序失败</span><span class="sxs-lookup"><span data-stu-id="521e3-413">Issue: "Download published site" fails for applications that have browser-based setup</span></span>

> <span data-ttu-id="521e3-414">某些应用程序 (例如，Kentico CMS) 要求你在浏览器中启动它们以执行安装后安装程序，如创建数据库。</span><span class="sxs-lookup"><span data-stu-id="521e3-414">Some applications (for example, Kentico CMS) require you to launch them in the browser in order to perform post-installation setup such as creating a database.</span></span> <span data-ttu-id="521e3-415">如果你发布此类应用程序，而不完成基于浏览器的安装程序，尝试从远程服务器下载相同的站点将失败。</span><span class="sxs-lookup"><span data-stu-id="521e3-415">If you publish an application like this without completing the browser-based setup, attempting to download the same site from a remote server will fail.</span></span>
> 
> <span data-ttu-id="521e3-416">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-416">**Workaround**</span></span>  
> <span data-ttu-id="521e3-417">在将站点发布之前完成基于浏览器的设置。</span><span class="sxs-lookup"><span data-stu-id="521e3-417">Finish browser-based setup before publishing the site.</span></span>


#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a><span data-ttu-id="521e3-418">问题:"下载发布站点"失败，出现数据库错误 DotNetNuke 和 Kooboo CMS</span><span class="sxs-lookup"><span data-stu-id="521e3-418">Issue: "Download published site" fails with a database error for DotNetNuke and Kooboo CMS</span></span>

> <span data-ttu-id="521e3-419">如果你尝试从服务器下载的应用程序，您必须在数据库连接字符串中的管理员凭据**发布设置**对话框中，你可能会看到发布日志中的以下错误：</span><span class="sxs-lookup"><span data-stu-id="521e3-419">If you try to download an application from a server and you have administrator credentials in the database connection string in the **Publish Settings** dialog, you might see the following error in the publish log:</span></span>
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> <span data-ttu-id="521e3-420">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="521e3-420">**Workaround**</span></span>  
> <span data-ttu-id="521e3-421">如果可行，重新发布该网站 （或将其发布） 的数据库使用非管理员凭据。</span><span class="sxs-lookup"><span data-stu-id="521e3-421">If practical, republish the site (or have it published) using non-administrator credentials for the database.</span></span>


<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="521e3-422">更多信息</span><span class="sxs-lookup"><span data-stu-id="521e3-422">For More Information</span></span>

<span data-ttu-id="521e3-423">有关 WebMatrix 1.0 的详细信息，请参阅以下网站：</span><span class="sxs-lookup"><span data-stu-id="521e3-423">For more information about WebMatrix 1.0, see the following websites:</span></span>

- [<span data-ttu-id="521e3-424">IIS.net</span><span class="sxs-lookup"><span data-stu-id="521e3-424">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="521e3-425">ASP.NET 2.0</span><span class="sxs-lookup"><span data-stu-id="521e3-425">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="521e3-426">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="521e3-426">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

<span data-ttu-id="521e3-427">© 2011 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="521e3-427">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="521e3-428">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="521e3-428">All Rights Reserved.</span></span> <span data-ttu-id="521e3-429">[使用条款](https://msdn.microsoft.cos/cc300389.aspx)。</span><span class="sxs-lookup"><span data-stu-id="521e3-429">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
