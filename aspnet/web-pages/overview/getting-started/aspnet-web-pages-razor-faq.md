---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET 网页 (Razor) 常见问题 |Microsoft Docs
author: Rick-Anderson
description: 本文列出了一些有关 ASP.NET Web Pages (Razor) 和 WebMatrix 的常见问题。 软件版本使用教程 ASP.NET Web Pages 中 (R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 27bfbe782455a5f8cf5096953c91712988b8dcab
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021048"
---
<a name="aspnet-web-pages-razor-faq"></a><span data-ttu-id="60e5e-104">ASP.NET 网页 (Razor) 常见问题解答</span><span class="sxs-lookup"><span data-stu-id="60e5e-104">ASP.NET Web Pages (Razor) FAQ</span></span>
====================
<span data-ttu-id="60e5e-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="60e5e-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> > [!NOTE] 
> > <span data-ttu-id="60e5e-106">WebMatrix 是不再建议将其作为一个集成的开发环境为 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="60e5e-106">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="60e5e-107">使用[Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio)或[Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="60e5e-107">Use [Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
>
> <span data-ttu-id="60e5e-108">本文列出了一些有关 ASP.NET Web Pages (Razor) 和 WebMatrix 的常见问题。</span><span class="sxs-lookup"><span data-stu-id="60e5e-108">This article lists some frequently asked questions about ASP.NET Web Pages (Razor) and WebMatrix.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="60e5e-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="60e5e-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="60e5e-110">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="60e5e-110">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="60e5e-111">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="60e5e-111">Visual Studio 2013</span></span>
> - <span data-ttu-id="60e5e-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="60e5e-112">WebMatrix 3</span></span>
>   
> 
> <span data-ttu-id="60e5e-113">本教程也适用于 ASP.NET Web Pages 2、 WebMatrix 2 和 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="60e5e-113">This tutorial also works with ASP.NET Web Pages 2, WebMatrix 2, and Visual Studio 2012.</span></span>


- [<span data-ttu-id="60e5e-114">ASP.NET 网页、 ASP.NET Web 窗体和 ASP.NET MVC 之间的区别是什么？</span><span class="sxs-lookup"><span data-stu-id="60e5e-114">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [<span data-ttu-id="60e5e-115">是否要使用 Web 页需要 WebMatrix？</span><span class="sxs-lookup"><span data-stu-id="60e5e-115">Do I need WebMatrix in order to work with Web Pages?</span></span>](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [<span data-ttu-id="60e5e-116">可以使用 Web Pages 页上的 ASP.NET Web 窗体控件？</span><span class="sxs-lookup"><span data-stu-id="60e5e-116">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [<span data-ttu-id="60e5e-117">可以将 ASP.NET Web Pages 站点部署而无需使用 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="60e5e-117">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [<span data-ttu-id="60e5e-118">我是否必须使用 WebSecurity 帮助器来支持登录名？</span><span class="sxs-lookup"><span data-stu-id="60e5e-118">Do I have to use the WebSecurity helper to support logins?</span></span>](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [<span data-ttu-id="60e5e-119">ASP.NET Web Pages 是否支持 HTML5？</span><span class="sxs-lookup"><span data-stu-id="60e5e-119">Does ASP.NET Web Pages support HTML5?</span></span>](#Does_ASP.NET_Web_Pages_support_HTML5)
- [<span data-ttu-id="60e5e-120">可以使用 JavaScript 和 jQuery 网页？</span><span class="sxs-lookup"><span data-stu-id="60e5e-120">Can I use JavaScript and jQuery with Web Pages?</span></span>](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [<span data-ttu-id="60e5e-121">其他资源</span><span class="sxs-lookup"><span data-stu-id="60e5e-121">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="60e5e-122">有关错误和其他问题的问题，请参阅[ASP.NET Web Pages (Razor) 疑难解答指南](https://go.microsoft.com/fwlink/?LinkId=253001)。</span><span class="sxs-lookup"><span data-stu-id="60e5e-122">For questions about errors and other issues, see the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a><span data-ttu-id="60e5e-123">ASP.NET 网页、 ASP.NET Web 窗体和 ASP.NET MVC 之间的区别是什么？</span><span class="sxs-lookup"><span data-stu-id="60e5e-123">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>

<span data-ttu-id="60e5e-124">这三个用于创建动态 web 应用程序的 ASP.NET 技术：</span><span class="sxs-lookup"><span data-stu-id="60e5e-124">All three are ASP.NET technologies for creating dynamic web applications:</span></span>

- <span data-ttu-id="60e5e-125">ASP.NET Web Pages 主要介绍在将动态 （服务器端） 代码和数据库访问权限添加到 HTML 页面和功能简单且轻量语法。</span><span class="sxs-lookup"><span data-stu-id="60e5e-125">ASP.NET Web Pages focuses on adding dynamic (server-side) code and database access to HTML pages, and features simple and lightweight syntax.</span></span>
- <span data-ttu-id="60e5e-126">ASP.NET Web 窗体基于页面对象模型和传统的窗口类型的控件 （按钮、 列表等）。</span><span class="sxs-lookup"><span data-stu-id="60e5e-126">ASP.NET Web Forms is based on a page object model and traditional window-type controls (buttons, lists, etc.).</span></span> <span data-ttu-id="60e5e-127">Web 窗体使用的是为那些使用基于客户端 （Windows 窗体） 开发过熟悉的基于事件的模型。</span><span class="sxs-lookup"><span data-stu-id="60e5e-127">Web Forms uses an event-based model that's familiar to those who've worked with client-based (Windows forms) development.</span></span>
- <span data-ttu-id="60e5e-128">ASP.NET MVC 实现的 ASP.NET 模型-视图-控制器模式。</span><span class="sxs-lookup"><span data-stu-id="60e5e-128">ASP.NET MVC implements the model-view-controller pattern for ASP.NET.</span></span> <span data-ttu-id="60e5e-129">重点是"关注点分离"（处理、 数据和 UI 层）。</span><span class="sxs-lookup"><span data-stu-id="60e5e-129">The emphasis is on "separation of concerns" (processing, data, and UI layers).</span></span>

<span data-ttu-id="60e5e-130">所有这三种框架完全支持，并且继续由 ASP.NET 团队开发。</span><span class="sxs-lookup"><span data-stu-id="60e5e-130">All three frameworks are fully supported and continue to be developed by the ASP.NET team.</span></span> <span data-ttu-id="60e5e-131">一般情况下，若要使用哪个框架的选择取决于您的背景和 ASP.NET 的体验。</span><span class="sxs-lookup"><span data-stu-id="60e5e-131">In general, the choice of which framework to use depends on your background and experience with ASP.NET.</span></span>

<span data-ttu-id="60e5e-132">ASP.NET Web Pages 特别旨在简化人员已经知道要将服务器处理添加到其页面的 HTML。</span><span class="sxs-lookup"><span data-stu-id="60e5e-132">ASP.NET Web Pages in particular was designed to make it easy for people who already know HTML to add server processing to their pages.</span></span> <span data-ttu-id="60e5e-133">有关学生、 业余爱好者，一般情况下人员谁是编程新手，它是一个不错的选择。</span><span class="sxs-lookup"><span data-stu-id="60e5e-133">It's a good choice for students, hobbyists, people in general who are new to programming.</span></span> <span data-ttu-id="60e5e-134">它还可以使用非 ASP.NET web 技术过开发人员的理想选择。</span><span class="sxs-lookup"><span data-stu-id="60e5e-134">It can also be a good choice for developers who have experience with non-ASP.NET web technologies.</span></span>

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a><span data-ttu-id="60e5e-135">是否要使用 Web 页需要 WebMatrix？</span><span class="sxs-lookup"><span data-stu-id="60e5e-135">Do I need WebMatrix in order to work with Web Pages?</span></span>

<span data-ttu-id="60e5e-136">不是。</span><span class="sxs-lookup"><span data-stu-id="60e5e-136">No.</span></span> <span data-ttu-id="60e5e-137">WebMatrix 是不再建议将其作为一个集成的开发环境为 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="60e5e-137">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="60e5e-138">使用[Visual Studio](program-asp-net-web-pages-in-visual-studio.md)或[Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="60e5e-138">Use [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>

<span data-ttu-id="60e5e-139">如果不想要使用 Visual Studio 或 Visual Studio Code，则可以安装使用单独的组件产品[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="60e5e-139">If you don't want to use either Visual Studio or Visual Studio Code, you can install the component products individually using [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span> <span data-ttu-id="60e5e-140">需要以下产品：</span><span class="sxs-lookup"><span data-stu-id="60e5e-140">You need the following products:</span></span>

- <span data-ttu-id="60e5e-141">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="60e5e-141">Microsoft .NET Framework 4.5</span></span>
- <span data-ttu-id="60e5e-142">ASP.NET MVC 5 （它将安装的 ASP.NET Web Pages 框架）</span><span class="sxs-lookup"><span data-stu-id="60e5e-142">ASP.NET MVC 5 (which installs the ASP.NET Web Pages framework as well)</span></span>
- <span data-ttu-id="60e5e-143">IIS Express （web 服务器）</span><span class="sxs-lookup"><span data-stu-id="60e5e-143">IIS Express (the web server)</span></span>
- <span data-ttu-id="60e5e-144">Microsoft SQL Server Compact 4.0 （数据库）</span><span class="sxs-lookup"><span data-stu-id="60e5e-144">Microsoft SQL Server Compact 4.0 (the database)</span></span>

<span data-ttu-id="60e5e-145">可以使用文本编辑器来编辑 *.cshtml* (或 *.vbhtml*) 页。</span><span class="sxs-lookup"><span data-stu-id="60e5e-145">You can use a text editor to edit *.cshtml* (or *.vbhtml*) pages.</span></span>

<span data-ttu-id="60e5e-146">管理 SQL Server Compact 数据库 (*.sdf*文件) 而不是很难的工具。</span><span class="sxs-lookup"><span data-stu-id="60e5e-146">Managing SQL Server Compact databases (*.sdf* files) without a tool is a bit harder.</span></span> <span data-ttu-id="60e5e-147">用于管理 visual Studio containds 工具 *.sdf*数据库。</span><span class="sxs-lookup"><span data-stu-id="60e5e-147">Visual Studio containds tools for managing *.sdf* databases.</span></span> <span data-ttu-id="60e5e-148">此外可以在代码中执行许多 SQL Server 管理任务来运行 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="60e5e-148">You can also run SQL commands in code to perform many SQL Server management tasks.</span></span>

<span data-ttu-id="60e5e-149">若要测试 *.cshtml*页，而不使用集成的开发环境 (IDE)，您可以将其部署到实时的服务器。</span><span class="sxs-lookup"><span data-stu-id="60e5e-149">To test *.cshtml* pages without using an integrated development environment (IDE), you can deploy them to a live server.</span></span> <span data-ttu-id="60e5e-150">(请参阅[可以将 ASP.NET Web Pages 站点部署而无需使用 WebMatrix？](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))</span><span class="sxs-lookup"><span data-stu-id="60e5e-150">(See [Can I deploy an ASP.NET Web Pages site without using WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))</span></span>

### <a name="running-iis-express-without-using-an-ide"></a><span data-ttu-id="60e5e-151">正在运行的 IIS Express，而无需使用 IDE</span><span class="sxs-lookup"><span data-stu-id="60e5e-151">Running IIS Express without using an IDE</span></span>

<span data-ttu-id="60e5e-152">如果您为 web 服务器的计算机上安装 IIS Express，可以使用的页进行测试。</span><span class="sxs-lookup"><span data-stu-id="60e5e-152">If you install IIS Express on your computer as a web server, you can use that to test the pages.</span></span> <span data-ttu-id="60e5e-153">您可以从命令行运行 IIS Express，并将其与特定的端口号。</span><span class="sxs-lookup"><span data-stu-id="60e5e-153">You can run IIS Express from the command line and associate it with a specific port number.</span></span> <span data-ttu-id="60e5e-154">然后指定该端口在请求时 *.cshtml*在浏览器中的文件。</span><span class="sxs-lookup"><span data-stu-id="60e5e-154">You then specify that port when you request *.cshtml* files in your browser.</span></span>

<span data-ttu-id="60e5e-155">在 Windows 中，使用管理员特权打开命令提示符处，并将更改为*C:\Program Files\IIS Express。*</span><span class="sxs-lookup"><span data-stu-id="60e5e-155">In Windows, open a command prompt with administrator privileges and change to *C:\Program Files\IIS Express.*</span></span> <span data-ttu-id="60e5e-156">(对于 64 位系统，使用文件夹*C:\Program Files (x86) \IIS Express。)* 然后输入以下命令，到您的网站使用的实际路径：</span><span class="sxs-lookup"><span data-stu-id="60e5e-156">(For 64-bit systems, use the folder *C:\Program Files (x86)\IIS Express.)* Then enter the following command, using the actual path to your site:</span></span>

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

<span data-ttu-id="60e5e-157">可以使用任何其他进程不已保留的端口号。</span><span class="sxs-lookup"><span data-stu-id="60e5e-157">You can use any port number that isn't already reserved by some other process.</span></span> <span data-ttu-id="60e5e-158">（以上 1024年的端口号是通常免费的。）有关`path`值，请使用网站文件夹的路径位置 *.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="60e5e-158">(Port numbers above 1024 are typically free.) For the `path` value, use the path of the website folder where the *.cshtml* files are.</span></span>

<span data-ttu-id="60e5e-159">在运行此命令以设置 IIS Express 以提供您的页面后，可以打开浏览器并浏览到 *.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="60e5e-159">After you run this command to set up IIS Express to serve your pages, you can open a browser and browse to a *.cshtml* file.</span></span> <span data-ttu-id="60e5e-160">使用 URL 如下所示：</span><span class="sxs-lookup"><span data-stu-id="60e5e-160">Use a URL like the following:</span></span>

`http://localhost:35896/default.cshtml`

<span data-ttu-id="60e5e-161">对于 IIS Express 命令行选项的帮助，请输入`iisexpress.exe /?`在命令行。</span><span class="sxs-lookup"><span data-stu-id="60e5e-161">For help with IIS Express command line options, enter `iisexpress.exe /?` at the command line.</span></span>

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a><span data-ttu-id="60e5e-162">可以使用 Web Pages 页上的 ASP.NET Web 窗体控件？</span><span class="sxs-lookup"><span data-stu-id="60e5e-162">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>

<span data-ttu-id="60e5e-163">不是。</span><span class="sxs-lookup"><span data-stu-id="60e5e-163">No.</span></span> <span data-ttu-id="60e5e-164">Web 窗体控件，例如[复选框](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox)控件，[验证控件](https://msdn.microsoft.com/library/bwd43d0x)，并[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview)控制仅在 Web 窗体页中的工作 (*.aspx*文件)。</span><span class="sxs-lookup"><span data-stu-id="60e5e-164">Web Forms controls like the [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) control, the [validation controls](https://msdn.microsoft.com/library/bwd43d0x), and the [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) control only work in Web Forms pages (*.aspx* files).</span></span> <span data-ttu-id="60e5e-165">这些控件需要 Web 窗体页框架。</span><span class="sxs-lookup"><span data-stu-id="60e5e-165">These controls require the Web Forms page framework.</span></span>

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a><span data-ttu-id="60e5e-166">可以将 ASP.NET Web Pages 站点部署而无需使用 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="60e5e-166">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>

<span data-ttu-id="60e5e-167">可以。</span><span class="sxs-lookup"><span data-stu-id="60e5e-167">Yes.</span></span> <span data-ttu-id="60e5e-168">您可以手动网站文件复制到一台服务器 （通常通过使用 FTP）。</span><span class="sxs-lookup"><span data-stu-id="60e5e-168">You can manually copy website files to a server (typically by using FTP).</span></span> <span data-ttu-id="60e5e-169">如果执行手动复制，您还必须复制支持 SQL Server Compact （数据库） 的文件。</span><span class="sxs-lookup"><span data-stu-id="60e5e-169">If you perform a manual copy, you also have to copy the files that support SQL Server Compact (the database).</span></span> <span data-ttu-id="60e5e-170">有关详细信息，请参阅博客文章[部署 Web Pages 应用程序而无需一种工具](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)。</span><span class="sxs-lookup"><span data-stu-id="60e5e-170">For details, see the blog entry [Deploying Web Pages applications without a tool](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).</span></span>

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a><span data-ttu-id="60e5e-171">我是否必须使用 WebSecurity 帮助器来支持登录名？</span><span class="sxs-lookup"><span data-stu-id="60e5e-171">Do I have to use the WebSecurity helper to support logins?</span></span>

<span data-ttu-id="60e5e-172">不是。</span><span class="sxs-lookup"><span data-stu-id="60e5e-172">No.</span></span> <span data-ttu-id="60e5e-173">`SimpleMembership`是一部分的 ASP.NET Web Pages 的提供程序是一种方法。</span><span class="sxs-lookup"><span data-stu-id="60e5e-173">The `SimpleMembership` provider that is part of ASP.NET Web Pages is one option.</span></span> <span data-ttu-id="60e5e-174">此外，还提供的安全提供程序是 ASP.NET （即你可能习惯于使用 Web 窗体中） 的一部分。</span><span class="sxs-lookup"><span data-stu-id="60e5e-174">The security providers that are part of ASP.NET (that you might be used to working with in Web Forms) are also available.</span></span> <span data-ttu-id="60e5e-175">例如，您可以使用窗体身份验证 ASP.NET Web Pages 中只需像在 Web 窗体中。</span><span class="sxs-lookup"><span data-stu-id="60e5e-175">For example, you can use forms authentication in ASP.NET Web Pages just as you would in Web Forms.</span></span> <span data-ttu-id="60e5e-176">为举例说明如何使用窗体身份验证，请参阅 Microsoft 支持文章[How To Implement Forms-Based 身份验证在您的 ASP.NET 应用程序通过使用 C#.NET](https://support.microsoft.com/kb/301240)。</span><span class="sxs-lookup"><span data-stu-id="60e5e-176">For one example of how to use forms authentication, see the Microsoft Support article [How To Implement Forms-Based Authentication in Your ASP.NET Application by Using C#.NET](https://support.microsoft.com/kb/301240).</span></span> <span data-ttu-id="60e5e-177">若要下载一个简单的示例，请参阅[ASP.NET 版本的"登录名&amp;密码](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)。</span><span class="sxs-lookup"><span data-stu-id="60e5e-177">To download a simple example, see [ASP.NET version of "Login &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).</span></span>

<span data-ttu-id="60e5e-178">有关如何使用 Windows 身份验证的信息，请参阅博客文章[使用 Windows 身份验证在 ASP.NET Web Pages](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)。</span><span class="sxs-lookup"><span data-stu-id="60e5e-178">For information about how to use Windows authentication, see the blog post [Using Windows authentication in ASP.NET Web Pages](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).</span></span>

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a><span data-ttu-id="60e5e-179">ASP.NET Web Pages 是否支持 HTML5？</span><span class="sxs-lookup"><span data-stu-id="60e5e-179">Does ASP.NET Web Pages support HTML5?</span></span>

<span data-ttu-id="60e5e-180">可以。</span><span class="sxs-lookup"><span data-stu-id="60e5e-180">Yes.</span></span> <span data-ttu-id="60e5e-181">创建使用 ASP.NET Web Pages 页 (*.cshtml*或 *.vbhtml*页) 是实质上是 HTML 页面，其中还包含之前呈现页面的服务器，运行的代码。</span><span class="sxs-lookup"><span data-stu-id="60e5e-181">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are essentially HTML pages that also contain code that runs on the server, before the page is rendered.</span></span> <span data-ttu-id="60e5e-182">只要用户的浏览器支持 HTML5，您可以使用中的 HTML5 元素 *.cshtml*或 *.vbhtml*页。</span><span class="sxs-lookup"><span data-stu-id="60e5e-182">As long as the user's browser supports HTML5, you can use HTML5 elements in a *.cshtml* or *.vbhtml* page.</span></span>

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a><span data-ttu-id="60e5e-183">可以使用 JavaScript 和 jQuery 网页？</span><span class="sxs-lookup"><span data-stu-id="60e5e-183">Can I use JavaScript and jQuery with Web Pages?</span></span>

<span data-ttu-id="60e5e-184">当然可以。</span><span class="sxs-lookup"><span data-stu-id="60e5e-184">Absolutely.</span></span> <span data-ttu-id="60e5e-185">创建使用 ASP.NET Web Pages 页 (*.cshtml*或 *.vbhtml*页) 的服务器代码只是 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="60e5e-185">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are just HTML pages with server code in them.</span></span> <span data-ttu-id="60e5e-186">因此，可以执行使用 JavaScript 或 jQuery 通过普通的 HTML 页面的任何内容还可以执行 *.cshtml*或 *.vbhtml*页。</span><span class="sxs-lookup"><span data-stu-id="60e5e-186">Therefore, anything you can do in a normal HTML page by using JavaScript or jQuery you can also do in a *.cshtml* or *.vbhtml* page.</span></span>

<span data-ttu-id="60e5e-187">**入门网站**模板在 WebMatrix 中的包含的众多 jQuery 库。</span><span class="sxs-lookup"><span data-stu-id="60e5e-187">The **Starter Site** template in WebMatrix contains a number of jQuery libraries.</span></span> <span data-ttu-id="60e5e-188">如果你使用该模板创建一个站点*脚本*文件夹包含 jQuery core 库 (*jquery 1.6.2.js)* 和适用于 jQuery 验证库 (*jquery.validate.js*，等等。)。</span><span class="sxs-lookup"><span data-stu-id="60e5e-188">If you create a site by using that template, the *Scripts* folder contains a jQuery core library (*jquery-1.6.2.js)* and libraries for jQuery validation (*jquery.validate.js*, etc.).</span></span>

<span data-ttu-id="60e5e-189">下面是一些演示了如何使用 jQuery 与 ASP.NET Web Pages 的博客文章：</span><span class="sxs-lookup"><span data-stu-id="60e5e-189">Here are some blog posts that illustrate ways to use jQuery with ASP.NET Web Pages:</span></span>

- <span data-ttu-id="60e5e-190">[通过将 jQuery 的精华内容添加到 ASP.NET Web Pages 使用 WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) Rachel appel</span><span class="sxs-lookup"><span data-stu-id="60e5e-190">[Adding jQuery Goodness to ASP.NET Web Pages using WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) by Rachel Appel</span></span>
- <span data-ttu-id="60e5e-191">[5 分钟： WebMatrix + jQuery UI + json 和 jQuery 模板](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/)通过 Jonas Eriksson</span><span class="sxs-lookup"><span data-stu-id="60e5e-191">[5 min: WebMatrix + jQuery UI + json + jQuery templates](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) by Jonas Eriksson</span></span>
- <span data-ttu-id="60e5e-192">[WebMatrix 和 jQuery 窗体](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)由 Mike Brind</span><span class="sxs-lookup"><span data-stu-id="60e5e-192">[WebMatrix And jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) by Mike Brind</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="60e5e-193">其他资源</span><span class="sxs-lookup"><span data-stu-id="60e5e-193">Additional Resources</span></span>


[<span data-ttu-id="60e5e-194">ASP.NET 网页 (Razor) 疑难解答指南</span><span class="sxs-lookup"><span data-stu-id="60e5e-194">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)

<span data-ttu-id="60e5e-195">[WebMatrix 和 ASP.NET Web Pages 论坛](https://forums.asp.net/1224.aspx/1?WebMatrix)ASP.NET 网站上</span><span class="sxs-lookup"><span data-stu-id="60e5e-195">[WebMatrix and ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix) on the ASP.NET website</span></span>
