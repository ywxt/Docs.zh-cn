---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
title: 部署具有 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 的 ASP.NET Web 应用程序： 疑难解答 (12 的 12) |Microsoft 文档
author: tdykstra
description: 这一系列的教程演示如何部署 （发布） ASP.NET web 应用程序项目，它通过使用 Visual Stu 包含 SQL Server Compact 数据库...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: 3fc23eed-921d-4d46-a610-a2d156e4bd03
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
msc.type: authoredcontent
ms.openlocfilehash: 2a8342f026498a7cf3ff4a3c158ed177c15b7111
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30890380"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-troubleshooting-12-of-12"></a><span data-ttu-id="9f1a5-103">部署具有 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 的 ASP.NET Web 应用程序： 疑难解答 (12 的 12)</span><span class="sxs-lookup"><span data-stu-id="9f1a5-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Troubleshooting (12 of 12)</span></span>
====================
<span data-ttu-id="9f1a5-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="9f1a5-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="9f1a5-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="9f1a5-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="9f1a5-106">这一系列的教程演示如何部署 （发布） ASP.NET web 应用程序项目，它通过使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 中包含 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="9f1a5-107">如果你安装 Web 发布更新，也可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="9f1a5-108">有关序列的简介，请参阅[序列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="9f1a5-109">显示部署功能后，将 Visual Studio 2012 RC 版本中推出，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并演示如何将部署到 Windows Azure 网站的教程，请参阅[的 ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


<span data-ttu-id="9f1a5-110">本页介绍通过使用 Visual Studio 部署 ASP.NET web 应用程序时可能出现的一些常见问题。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-110">This page describes some common problems that may arise when you deploy an ASP.NET web application by using Visual Studio.</span></span> <span data-ttu-id="9f1a5-111">每个提供了一个或多个可能的原因和相应的解决方案。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-111">For each one, one or more possible causes and corresponding solutions are provided.</span></span>

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a><span data-ttu-id="9f1a5-112">服务器错误 '/' 应用程序-中当前的自定义错误设置防止错误的详细信息其他人远程查看</span><span class="sxs-lookup"><span data-stu-id="9f1a5-112">Server Error in '/' Application - Current Custom Error Settings Prevent Details of the Error from Being Viewed Remotely</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-113">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-113">Scenario</span></span>

<span data-ttu-id="9f1a5-114">部署到远程主机的站点之后, 你将收到错误消息，提及的 Web.config 文件中的 customErrors 设置，但并不指示错误的实际原因是：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-114">After deploying a site to a remote host, you get an error message that mentions the customErrors setting in the Web.config file but doesn't indicate what the actual cause of the error was:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample1.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-115">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-115">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-116">默认情况下，ASP.NET 仅在本地计算机上运行 web 应用程序时显示详细的错误信息。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-116">By default, ASP.NET shows detailed error information only when your web application is running on the local computer.</span></span> <span data-ttu-id="9f1a5-117">通常你不想要在 web 应用程序是在 Internet 上公开提供的因为黑客可能能够使用此信息来查找应用程序中的漏洞时显示详细的错误信息。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-117">Generally you don't want to display detailed error information when your web application is publicly available over the Internet, because hackers may be able to use this information to find vulnerabilities in the application.</span></span> <span data-ttu-id="9f1a5-118">但是，当要部署的站点或更新到站点，有时内容将会出错，您需要先获取实际错误消息。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-118">However, when you are deploying a site or updates to a site, sometimes something will go wrong and you need to get the actual error message.</span></span>

<span data-ttu-id="9f1a5-119">若要启用要在远程主机上运行时显示详细的错误消息的应用程序，编辑 Web.config 文件以设置`customErrors`模式关闭、 重新部署应用程序，并运行一次，应用程序：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-119">To enable the application to display detailed error messages when it runs on the remote host, edit the Web.config file to set `customErrors` mode off, redeploy the application, and run the application again:</span></span>

1. <span data-ttu-id="9f1a5-120">如果应用程序 Web.config 文件具有`customErrors`中的元素`system.web`元素中，更改`mode`属性为"关闭"。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-120">If the application Web.config file has a `customErrors` element in the `system.web` element, change the `mode` attribute to "off".</span></span> <span data-ttu-id="9f1a5-121">否则，添加`customErrors`中的元素`system.web`具有元素`mode`属性设置为"off"，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-121">Otherwise add a `customErrors` element in the `system.web` element with the `mode` attribute set to "off", as shown in the following example:</span></span>

    [!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample2.xml?highlight=3)]
2. <span data-ttu-id="9f1a5-122">部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-122">Deploy the application.</span></span>
3. <span data-ttu-id="9f1a5-123">运行应用程序并重复执行任何你此前导致发生错误。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-123">Run the application and repeat whatever you did earlier that caused the error to occur.</span></span> <span data-ttu-id="9f1a5-124">现在，你可以看到什么是实际错误消息。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-124">Now you can see what the actual error message is.</span></span>
4. <span data-ttu-id="9f1a5-125">在纠正错误后，将还原原始`customErrors`设置并重新部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-125">When you have resolved the error, restore the original `customErrors` setting and redeploy the application.</span></span>

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a><span data-ttu-id="9f1a5-126">访问被拒绝网页中使用 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="9f1a5-126">Access is Denied in a Web Page that Uses SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-127">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-127">Scenario</span></span>

<span data-ttu-id="9f1a5-128">在部署使用 SQL Server Compact 的站点访问数据库的已部署站点中运行某个页面时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-128">When you deploy a site that uses SQL Server Compact and you run a page in the deployed site that accesses the database, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-129">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-129">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-130">服务器上的网络服务帐户需要能够读取 SQL 服务 Compact 中的本机二进制文件*bin\amd64*或*bin\x86*文件夹中，但它没有读取这些文件夹的权限。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-130">The NETWORK SERVICE account on the server needs to be able to read SQL Service Compact native binaries that are in the *bin\amd64* or *bin\x86* folder, but it does not have read permissions for those folders.</span></span> <span data-ttu-id="9f1a5-131">设置在读取网络服务的权限*bin*文件夹，同时确保扩展的子文件夹的权限。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-131">Set read permission for NETWORK SERVICE on the *bin* folder, making sure to extend the permissions to subfolders.</span></span>

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a><span data-ttu-id="9f1a5-132">无法读取配置文件由于权限不足而</span><span class="sxs-lookup"><span data-stu-id="9f1a5-132">Cannot Read Configuration File Due to Insufficient Permissions</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-133">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-133">Scenario</span></span>

<span data-ttu-id="9f1a5-134">当你单击 Visual Studio 发布按钮以应用程序部署到 IIS 在本地计算机，发布失败和**输出**窗口将显示一条错误消息类似于此：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-134">When you click the Visual Studio publish button to deploy an application to IIS on your local machine, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample4.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-135">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-135">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-136">若要使用一次单击将发布到 IIS 在本地计算机上，你必须具有管理员权限运行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-136">To use one-click publish to IIS on your local machine, you must be running Visual Studio with administrator permissions.</span></span> <span data-ttu-id="9f1a5-137">关闭 Visual Studio 并重新启动它具有管理员权限。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-137">Close Visual Studio and restart it with administrator permissions.</span></span>

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a><span data-ttu-id="9f1a5-138">无法连接到目标计算机...使用指定的进程</span><span class="sxs-lookup"><span data-stu-id="9f1a5-138">Could Not Connect to the Destination Computer ... Using the Specified Process</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-139">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-139">Scenario</span></span>

<span data-ttu-id="9f1a5-140">当你单击 Visual Studio 发布按钮以部署应用程序，发布失败和**输出**窗口将显示一条错误消息类似于此：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-140">When you click the Visual Studio publish button to deploy an application, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample5.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-141">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-141">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-142">代理服务器中断与目标服务器的通信。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-142">A proxy server is interrupting communication with the destination server.</span></span> <span data-ttu-id="9f1a5-143">从 Windows 控制面板或 Internet Explorer 中，选择**Internet 选项**和选择**连接**选项卡。在**互联**对话框中，单击**LAN 设置**。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-143">From the Windows Control Panel or in Internet Explorer, select **Internet Options** and select the **Connections** tab. In the **Internet Properties** dialog box, click **LAN Settings**.</span></span> <span data-ttu-id="9f1a5-144">在**局域网 (LAN) 设置**对话框中，清除**自动检测设置**复选框。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-144">In the **Local Area Network (LAN) Settings** dialog box, clear the **Automatically detect settings** checkbox.</span></span> <span data-ttu-id="9f1a5-145">然后再次单击发布按钮。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-145">Then click the publish button again.</span></span>

<span data-ttu-id="9f1a5-146">如果问题仍然存在，请与系统管理员联系，以确定什么可通过代理或防火墙设置。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-146">If the problem persists, contact your system administrator to determine what can be done with proxy or firewall settings.</span></span> <span data-ttu-id="9f1a5-147">因为 Web 部署为 Web 管理服务部署 (8172); 使用非标准端口仍然出现该问题对于其他连接，Web 部署使用端口 80。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-147">The problem happens because Web Deploy uses a non-standard port for Web Management Service deployment (8172); for other connections, Web Deploy uses port 80.</span></span> <span data-ttu-id="9f1a5-148">当将部署到第三方托管提供商时，你通常使用 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-148">When you are deploying to a third-party hosting provider, you are typically using the Web Management Service.</span></span>

## <a name="default-net-40-application-pool-does-not-exist"></a><span data-ttu-id="9f1a5-149">默认.NET 4.0 的应用程序池不存在</span><span class="sxs-lookup"><span data-stu-id="9f1a5-149">Default .NET 4.0 Application Pool Does Not Exist</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-150">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-150">Scenario</span></span>

<span data-ttu-id="9f1a5-151">当你部署的应用程序需要.NET Framework 4 时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-151">When you deploy an application that requires the .NET Framework 4, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample6.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-152">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-152">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-153">ASP.NET 4 未安装在 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-153">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="9f1a5-154">如果您要部署到的服务器是开发计算机，并且在其上安装 Visual Studio 2010，ASP.NET 4 的计算机上安装，但可能未安装在 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-154">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="9f1a5-155">在服务器上要部署到，打开提升的命令提示符并安装在 IIS 中的 ASP.NET 4 中，通过运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-155">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample7.cmd)]

<span data-ttu-id="9f1a5-156">你可能还需要手动设置默认应用程序池的.NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-156">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="9f1a5-157">有关详细信息，请参阅[作为测试环境部署到 IIS](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-157">For more information, see the [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) tutorial.</span></span>

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a><span data-ttu-id="9f1a5-158">初始化字符串的格式不符合从索引 0 处开始的规范。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-158">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-159">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-159">Scenario</span></span>

<span data-ttu-id="9f1a5-160">部署应用程序使用一次单击后发布，当你运行的页访问数据库获得以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-160">After you deploy an application using one-click publish, when you run a page that accesses the database you get the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample8.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-161">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-161">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-162">打开*Web.config*文件中的已部署的站点和检查连接字符串值开头`$(ReplacableToken_`，下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-162">Open the *Web.config* file in the deployed site and check to see whether the connection string values begin with `$(ReplacableToken_`, as in the following example:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample9.xml)]

<span data-ttu-id="9f1a5-163">如果连接字符串看上去像此示例中，编辑项目文件并添加以下属性`PropertyGroup`是适用于所有生成配置的元素：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-163">If the connection strings look like this example, edit the project file and add the following property to the `PropertyGroup` element that is for all build configurations:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample10.xml)]

<span data-ttu-id="9f1a5-164">然后重新部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-164">Then redeploy the application.</span></span>

## <a name="http-500-internal-server-error"></a><span data-ttu-id="9f1a5-165">HTTP 500 内部服务器错误</span><span class="sxs-lookup"><span data-stu-id="9f1a5-165">HTTP 500 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-166">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-166">Scenario</span></span>

<span data-ttu-id="9f1a5-167">运行已部署的站点时，你将看到以下错误消息，没有特定信息，该值指示错误的原因：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-167">When you run the deployed site, you see the following error message without specific information indicating the cause of the error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample11.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-168">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-168">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-169">有许多原因的 500 错误，但如果按照这些教程的一个可能原因是可将一个 XML 元素放入错误的位置中的 XML 转换文件之一。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-169">There are many causes of 500 errors, but one possible cause if you are following these tutorials is that you put an XML element in the wrong place in one of the XML transformation files.</span></span> <span data-ttu-id="9f1a5-170">例如，你会遇到此错误，如果你将插入的转换`<location>`元素下的`<system.web>`而不是直接在`<configuration>`。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-170">For example, you would get this error if you put the transformation that inserts a `<location>` element under `<system.web>` instead of directly under `<configuration>`.</span></span> <span data-ttu-id="9f1a5-171">在这种情况下的解决方案是更正 XML 转换文件并重新部署。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-171">The solution in that case is to correct the XML transformation file and redeploy.</span></span>

## <a name="http-50021-internal-server-error"></a><span data-ttu-id="9f1a5-172">HTTP 500.21 内部服务器错误</span><span class="sxs-lookup"><span data-stu-id="9f1a5-172">HTTP 500.21 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-173">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-173">Scenario</span></span>

<span data-ttu-id="9f1a5-174">运行已部署的站点时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-174">When you run the deployed site, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample12.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-175">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-175">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-176">你已为其部署 ASP.NET 4 中，但 ASP.NET 4 未注册在 IIS 中在服务器的目标站点。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-176">The site you have deployed targets ASP.NET 4, but ASP.NET 4 is not registered in IIS on the server.</span></span> <span data-ttu-id="9f1a5-177">在服务器上打开提升的命令提示符，并通过运行以下命令来注册 ASP.NET 4:</span><span class="sxs-lookup"><span data-stu-id="9f1a5-177">On the server open an elevated command prompt and register ASP.NET 4 by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample13.cmd)]

<span data-ttu-id="9f1a5-178">你可能还需要手动设置默认应用程序池的.NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-178">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="9f1a5-179">有关详细信息，请参阅[作为测试环境部署到 IIS](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-179">For more information, see the [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) tutorial.</span></span>

## <a name="login-failed-opening-sql-server-express-database-in-appdata"></a><span data-ttu-id="9f1a5-180">登录失败打开 SQL Server Express 数据库中应用\_数据</span><span class="sxs-lookup"><span data-stu-id="9f1a5-180">Login Failed Opening SQL Server Express Database in App\_Data</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-181">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-181">Scenario</span></span>

<span data-ttu-id="9f1a5-182">您提供更新*Web.config*文件连接字符串以指向 SQL Server Express 数据库作为 *.mdf*文件在你*应用\_数据*文件夹中和第一个运行应用程序，你看到以下错误消息的时间：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-182">You updated the *Web.config* file connection string to point to a SQL Server Express database as an *.mdf* file in your *App\_Data* folder, and the first time you run the application you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample14.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-183">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-183">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-184">名称 *.mdf*文件不能匹配任何已曾经存在你计算机的 SQL Server Express 数据库的名称，即使你删除 *.mdf*先前存在的数据库文件。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-184">The name of the *.mdf* file cannot match the name of any SQL Server Express database that has ever existed on your computer, even if you deleted the *.mdf* file of the previously existing database.</span></span> <span data-ttu-id="9f1a5-185">更改的名称 *.mdf*从未为数据库名称和更改使用的名称的文件*Web.config*文件以使用新名称。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-185">Change the name of the *.mdf* file to a name that has never been used as a database name and change the *Web.config* file to use the new name.</span></span> <span data-ttu-id="9f1a5-186">作为替代方法，你可以使用[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)删除先前存在的 SQL Server Express 数据库。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-186">As an alternative, you can use [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete previously existing SQL Server Express databases.</span></span>

## <a name="model-compatibility-cannot-be-checked"></a><span data-ttu-id="9f1a5-187">模型兼容性无法检查</span><span class="sxs-lookup"><span data-stu-id="9f1a5-187">Model Compatibility Cannot be Checked</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-188">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-188">Scenario</span></span>

<span data-ttu-id="9f1a5-189">您提供更新*Web.config*文件连接字符串以指向新的 SQL Server Express 数据库，并运行应用程序首次你看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-189">You updated the *Web.config* file connection string to point to a new SQL Server Express database, and the first time you run the application you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample15.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-190">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-190">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-191">如果你在计算机上，数据库可能已存在与某些表之前，已曾经使用 Web.config 文件中放置的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-191">If the database name you put in the Web.config file was ever used before on your computer, a database might already exist with some tables in it.</span></span> <span data-ttu-id="9f1a5-192">选择尚未使用在之前的计算机和更改的新名称*Web.config*文件以点以使用此新的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-192">Select a new name that has not been used on your computer before and change the *Web.config* file to point to use this new database name.</span></span> <span data-ttu-id="9f1a5-193">作为替代方法，你可以使用[SQL Server Express 实用工具](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990)或[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)删除现有数据库。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-193">As an alternative, you can use [SQL Server Express Utility](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) or [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete the existing database.</span></span>

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a><span data-ttu-id="9f1a5-194">SQL 错误时的脚本尝试创建用户或角色</span><span class="sxs-lookup"><span data-stu-id="9f1a5-194">SQL Error When a Script Attempts to Create Users or Roles</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-195">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-195">Scenario</span></span>

<span data-ttu-id="9f1a5-196">您要使用在上配置的数据库部署**打包/发布 SQL**选项卡上，在部署过程中运行的 SQL 脚本包括 Create User 或创建角色命令和脚本执行失败时执行这些命令。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-196">You are using database deployment configured on the **Package/Publish SQL** tab, SQL scripts that run during deployment include Create User or Create Role commands, and script execution fails when those commands are executed.</span></span> <span data-ttu-id="9f1a5-197">你可能会看到更多详细消息，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-197">You might see more detailed messages, such as the following:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample16.cmd)]

<span data-ttu-id="9f1a5-198">如果你已配置中的数据库部署时会发生此错误**发布 Web**向导而不是**打包/发布 SQL**选项卡上，创建中的线程[配置和部署](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)论坛和解决方案将添加到此故障排除的页面。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-198">If this error occurs when you have configured database deployment in the **Publish Web** wizard rather than the **Package/Publish SQL** tab, create a thread in the [Configuration and Deployment](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) forum, and the solution will be added to this troubleshooting page.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-199">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-199">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-200">用来执行部署的用户帐户没有权限来创建用户或角色。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-200">The user account you are using to perform deployment does not have permission to create users or roles.</span></span> <span data-ttu-id="9f1a5-201">例如，托管公司可能将分配`db_datareader`， `db_datawriter`，和`db_ddladmin`到它为你设置的用户帐户的角色。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-201">For example, the hosting company might assign the `db_datareader`, `db_datawriter`, and `db_ddladmin` roles to the user account that it sets up for you.</span></span> <span data-ttu-id="9f1a5-202">这些是足够有关创建大多数的数据库对象，而不是创建用户或角色。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-202">These are sufficient for creating most database objects, but not for creating users or roles.</span></span> <span data-ttu-id="9f1a5-203">若要避免错误的一种方法是通过从数据库部署中排除用户和角色。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-203">One way to avoid the error is by excluding users and roles from database deployment.</span></span> <span data-ttu-id="9f1a5-204">你可以执行此操作通过编辑`PreSource`数据库的元素的自动生成脚本，以使它包括以下属性：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-204">You can do this by editing the `PreSource` element for the database's automatically generated script so that it includes the following attributes:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample17.cmd)]

<span data-ttu-id="9f1a5-205">有关如何编辑`PreSource`元素在项目文件中，请参阅[如何： 编辑项目文件中的部署设置](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-205">For information about how to edit the `PreSource` element in the project file, see [How to: Edit Deployment Settings in the Project File](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx).</span></span> <span data-ttu-id="9f1a5-206">如果用户或开发数据库中的角色需要将位于目标数据库中，请与你托管提供商联系以获取帮助。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-206">If the users or roles in your development database need to be in the destination database, contact your hosting provider for assistance.</span></span>

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a><span data-ttu-id="9f1a5-207">SQL Server 超时错误时在部署过程中运行自定义脚本</span><span class="sxs-lookup"><span data-stu-id="9f1a5-207">SQL Server Timeout Error When Running Custom Scripts During Deployment</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-208">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-208">Scenario</span></span>

<span data-ttu-id="9f1a5-209">您指定了自定义 SQL 脚本以在部署期间，运行，并且当 Web 部署运行它们时，它们的超时时间。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-209">You have specified custom SQL scripts to run during deployment, and when Web Deploy runs them, they time out.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-210">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-210">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-211">运行具有不同的事务模式的多个脚本可能导致超时错误。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-211">Running multiple scripts that have different transaction modes can cause time-out errors.</span></span> <span data-ttu-id="9f1a5-212">默认情况下自动生成的脚本运行在事务中，但自定义脚本不这样做。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-212">By default, automatically generated scripts run in a transaction, but custom scripts do not.</span></span> <span data-ttu-id="9f1a5-213">如果你选择**抽取数据和/或从现有数据库的架构**选项**打包/发布 SQL**选项卡上，如果你添加自定义 SQL 脚本，必须更改某些脚本上的事务设置，以便所有脚本都使用相同的事务设置。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-213">If you select the **Pull data and/or schema from an existing database** option on the **Package/Publish SQL** tab, and if you add a custom SQL script, you must change transaction settings on some scripts so that all scripts use the same transaction settings.</span></span> <span data-ttu-id="9f1a5-214">有关详细信息，请参阅[如何： 部署数据库与 Web 应用程序项目](https://msdn.microsoft.com/library/dd465343.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-214">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343.aspx).</span></span>

<span data-ttu-id="9f1a5-215">如果你已配置事务设置，以便所有都相同，但仍遇到此错误，可能的解决方法是单独运行这些脚本。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-215">If you have configured transaction settings so that all are the same but still get this error, a possible workaround is to run the scripts separately.</span></span> <span data-ttu-id="9f1a5-216">在**数据库脚本**网格中的**打包/发布**SQL 选项卡上，将其清除**包括**会导致超时错误，该脚本的复选框然后发布项目。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-216">In the **Database Scripts** grid in the **Package/Publish** SQL tab, clear the **Include** check box for the script that causes the timeout error, then publish the project.</span></span> <span data-ttu-id="9f1a5-217">然后转回**数据库脚本**网格中，选择该脚本**包括**复选框，然后清除**包括**其他脚本对应的复选框。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-217">Then go back into the **Database Scripts** grid, select that script's **Include** check box, and clear the **Include** check boxes for the other scripts.</span></span> <span data-ttu-id="9f1a5-218">然后再次发布该项目。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-218">Then publish the project again.</span></span> <span data-ttu-id="9f1a5-219">发布时，此次运行时仅选择自定义的脚本。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-219">This time when you publish, only the selected custom script runs.</span></span>

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a><span data-ttu-id="9f1a5-220">站点清单的流数据尚不可用</span><span class="sxs-lookup"><span data-stu-id="9f1a5-220">Stream Data of Site Manifest Is Not Yet Available</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-221">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-221">Scenario</span></span>

<span data-ttu-id="9f1a5-222">当你要安装包使用*deploy.cmd*文件`t`（测试） 选项，请参阅以下的错误消息：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-222">When you are installing a package using the *deploy.cmd* file with the `t` (test) option, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample18.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-223">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-223">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-224">错误消息表示命令无法生成测试报告。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-224">The error message means that the command cannot produce a test report.</span></span> <span data-ttu-id="9f1a5-225">但是，如果你使用运行该命令可能会`y`（实际安装） 选项。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-225">However, the command might run if you use the `y` (actual installation) option.</span></span> <span data-ttu-id="9f1a5-226">此消息仅指示在测试模式下运行该命令的问题。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-226">The message indicates only that there is a problem with running the command in test mode.</span></span>

## <a name="this-application-requires-managedruntimeversion-v40"></a><span data-ttu-id="9f1a5-227">此应用程序需要 ManagedRuntimeVersion v4.0</span><span class="sxs-lookup"><span data-stu-id="9f1a5-227">This Application Requires ManagedRuntimeVersion v4.0</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-228">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-228">Scenario</span></span>

<span data-ttu-id="9f1a5-229">当你尝试部署时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-229">When you attempt to deploy, you see the following error message:</span></span>

 <span data-ttu-id="9f1a5-230">错误： 流数据的 sitemanifest/dbFullSql [@path= C:\TEMP\AdventureWorksGrant.sql']/sqlScript 尚不可用。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-230">Error: The stream data of 'sitemanifest/dbFullSql[@path='C:\TEMP\AdventureWorksGrant.sql']/sqlScript' is not yet available.</span></span> <span data-ttu-id="9f1a5-231">你正在使用的应用程序池具有 managedRuntimeVersion 属性设置为 v2.0。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-231">The application pool that you are trying to use has the 'managedRuntimeVersion' property set to 'v2.0'.</span></span> <span data-ttu-id="9f1a5-232">此应用程序需要 v4.0。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-232">This application requires 'v4.0'.</span></span> 

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-233">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-233">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-234">ASP.NET 4 未安装在 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-234">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="9f1a5-235">如果您要部署到的服务器是开发计算机，并且在其上安装 Visual Studio 2010，ASP.NET 4 的计算机上安装，但可能未安装在 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-235">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="9f1a5-236">在服务器上要部署到，打开提升的命令提示符并安装在 IIS 中的 ASP.NET 4 中，通过运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-236">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample19.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a><span data-ttu-id="9f1a5-237">无法将 Microsoft.Web.Deployment.DeploymentProviderOptions 强制转换</span><span class="sxs-lookup"><span data-stu-id="9f1a5-237">Unable to cast Microsoft.Web.Deployment.DeploymentProviderOptions</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-238">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-238">Scenario</span></span>

<span data-ttu-id="9f1a5-239">在部署包时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-239">When you are deploying a package, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample20.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-240">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-240">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-241">你尝试部署从 IIS 管理器中使用 Web 部署 1.1 UI 到已安装的 Web 部署 2.0 的服务器。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-241">You are trying to deploy from IIS Manager using the Web Deploy 1.1 UI to a server that has Web Deploy 2.0 installed.</span></span> <span data-ttu-id="9f1a5-242">如果你使用 IIS 的远程管理工具来部署通过导入包中，检查**新提供的功能**建立连接时的对话框。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-242">If you are using the IIS Remote Administration Tool to deploy by importing a package, check the **New Features Available** dialog box when you establish the connection.</span></span> <span data-ttu-id="9f1a5-243">（此对话框中可能才会显示一次当首次建立连接。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-243">(This dialog box might only be shown once when the connection is first established.</span></span> <span data-ttu-id="9f1a5-244">若要清除连接并重新启动，关闭 IIS 管理器并它再次启动通过输入`inetmgr /reset`在命令提示符下。)如果列出的功能之一是**Web 部署 UI**，并且它有一个版本号低于 8，您要部署到的服务器可能必须 1.1 和 2.0 版的 Web 部署安装。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-244">To clear the connection and start over, close IIS Manager and start it up again by entering `inetmgr /reset` at the command prompt.) If one of the features listed is **Web Deploy UI**, and it has a version number lower than 8, the server you are deploying to might have both 1.1 and 2.0 versions of Web Deploy installed.</span></span> <span data-ttu-id="9f1a5-245">若要从具有 2.0 安装的客户端部署，服务器必须仅 Web Deploy 2.0 安装。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-245">To deploy from a client that has 2.0 installed, the server must have only Web Deploy 2.0 installed.</span></span> <span data-ttu-id="9f1a5-246">你将需要联系托管提供商若要解决此问题。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-246">You will have to contact your hosting provider to resolve this problem.</span></span>

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a><span data-ttu-id="9f1a5-247">无法加载 SQL Server Compact 的本机组件</span><span class="sxs-lookup"><span data-stu-id="9f1a5-247">Unable to load the native components of SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-248">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-248">Scenario</span></span>

<span data-ttu-id="9f1a5-249">运行已部署的站点时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-249">When you run the deployed site, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample21.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-250">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-250">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-251">已部署的站点并没有*amd64*和*x86*使用本机的程序集，该应用程序下的子文件夹*bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-251">The deployed site does not have *amd64* and *x86* subfolders with the native assemblies in them under the application's *bin* folder.</span></span> <span data-ttu-id="9f1a5-252">在上 SQL Server Compact 安装的计算机，本机程序集位于*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-252">On a computer that has SQL Server Compact installed, the native assemblies are located in *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*.</span></span> <span data-ttu-id="9f1a5-253">到正确的文件夹中的 Visual Studio 项目中获取正确的文件的最佳方法是安装 NuGet SqlServerCompact 包。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-253">The best way to get the correct files into the correct folders in a Visual Studio project is to install the NuGet SqlServerCompact package.</span></span> <span data-ttu-id="9f1a5-254">包安装添加后期生成脚本，以将复制到本机程序集*amd64*和*x86*。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-254">Package installation adds a post-build script to copy the native assemblies into *amd64* and *x86*.</span></span> <span data-ttu-id="9f1a5-255">为了使这些部署，但是，必须手动将其包含在项目中。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-255">In order for these to be deployed, however, you have to manually include them in the project.</span></span> <span data-ttu-id="9f1a5-256">有关详细信息，请参阅[部署 SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-256">For more information, see the [Deploying SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a><span data-ttu-id="9f1a5-257">部署 Entity Framework Code First 的应用程序后，"路径不是有效的"错误</span><span class="sxs-lookup"><span data-stu-id="9f1a5-257">"Path is not valid" error after deploying an Entity Framework Code First application</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-258">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-258">Scenario</span></span>

<span data-ttu-id="9f1a5-259">部署应用程序，如 SQL Server Compact 后者将其数据库存储在应用程序中的文件使用 Entity Framework Code First 迁移和 DBMS\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-259">You deploy an application that uses Entity Framework Code First Migrations and a DBMS such as SQL Server Compact which stores its database in a file in the App\_Data folder.</span></span> <span data-ttu-id="9f1a5-260">必须配置为在第一个部署之后创建数据库的 Code First 迁移。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-260">You have Code First Migrations configured to create the database after your first deployment.</span></span> <span data-ttu-id="9f1a5-261">当你运行应用程序可以一条错误消息如下例所示：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-261">When you run the application you get an error message like the following example:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample22.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-262">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-262">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-263">代码首先尝试创建数据库，但应用\_数据文件夹不存在。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-263">Code First is attempting to create the database but the App\_Data folder does not exist.</span></span> <span data-ttu-id="9f1a5-264">未有任何文件*应用\_数据*文件夹时部署，或者与您选择**排除应用\_数据**上**打包/发布 Web**选项卡**项目属性**窗口。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-264">Either you didn't have any files in the *App\_Data* folder when you deployed, or you selected **Exclude App\_Data** on the **Package/Publish Web** tab of the **Project Properties** window.</span></span> <span data-ttu-id="9f1a5-265">如果要复制到服务器的文件夹中不有任何文件，在部署过程不会在服务器上创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-265">The deployment process won't create a folder on the server if there are no files in the folder to be copied to the server.</span></span> <span data-ttu-id="9f1a5-266">如果您已经有站点中设置的数据库，在部署过程将删除的文件和*应用\_数据*文件夹本身如果你选择**删除目标位置的其他文件**中发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-266">If you already had the database set up in the site, the deployment process will delete the files and the *App\_Data* folder itself if you selected **Remove additional files at destination** in the publish profile.</span></span> <span data-ttu-id="9f1a5-267">若要解决此问题，将占位符文件，如中的.txt 文件*应用\_数据*文件夹，请确保你没有**排除应用\_数据**选择，并重新部署。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-267">To solve the problem, put a placeholder file such as a .txt file in the *App\_Data* folder, make sure you do not have **Exclude App\_Data** selected, and redeploy.</span></span> 

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a><span data-ttu-id="9f1a5-268">"不能使用已分开其基础 RCW 的 COM 对象"。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-268">"COM object that has been separated from its underlying RCW cannot be used."</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-269">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-269">Scenario</span></span>

<span data-ttu-id="9f1a5-270">你已成功使用一键式发布来部署你的应用程序，然后你启动遇到此错误：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-270">You have been successfully using one-click publish to deploy your application and then you start getting this error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample23.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-271">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-271">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-272">关闭和重新启动 Visual Studio 通常是所有需要来解决此错误。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-272">Closing and restarting Visual Studio is usually all that is required to resolve this error.</span></span>

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a><span data-ttu-id="9f1a5-273">部署失败由于用户凭据用于发布没有 setACL 颁发机构</span><span class="sxs-lookup"><span data-stu-id="9f1a5-273">Deployment Fails Because User Credentials Used for Publishing Don't Have setACL Authority</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-274">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-274">Scenario</span></span>

<span data-ttu-id="9f1a5-275">发布将失败并出错类型的值，该值指示你没有设置文件夹权限 （所使用的用户帐户没有 setACL 机构） 的授权。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-275">Publishing fails with an error that indicates you don't have authority to set folder permissions (the user account you are using doesn't have setACL authority).</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-276">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-276">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-277">默认情况下，Visual Studio 集对站点的根文件夹的读取权限和写应用程序权限\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-277">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="9f1a5-278">如果您知道站点文件夹上的默认权限是否正确，并且不需要设置，则禁用此行为通过添加**&lt;IncludeSetACLProviderOn 目标&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 到发布配置文件 （以影响一个配置文件） 或 （要影响的所有配置文件） 的 wpp.targets 文件。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-278">If you know that the default permissions on site folders are correct and do not need to be set, you disable this behavior by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="9f1a5-279">有关如何编辑这些文件的信息，请参阅[如何： 编辑配置文件 (.pubxml) 文件中的部署设置](https://msdn.microsoft.com/library/ff398069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-279">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span> 

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a><span data-ttu-id="9f1a5-280">当应用程序尝试写入到应用程序文件夹时，访问被拒绝错误</span><span class="sxs-lookup"><span data-stu-id="9f1a5-280">Access Denied Errors when the Application Tries to Write to an Application Folder</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-281">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-281">Scenario</span></span>

<span data-ttu-id="9f1a5-282">你的应用程序错误时它将尝试创建或编辑的文件中的一个应用程序文件夹中，因为它不具有该文件夹的写权限。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-282">Your application errors when it tries to create or edit a file in one of the application folders, because it does not have write authority for that folder.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-283">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-283">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-284">默认情况下，Visual Studio 集对站点的根文件夹的读取权限和写应用程序权限\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-284">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="9f1a5-285">如果你的应用程序需要的子文件夹的写访问权限，则可以设置为该文件夹的权限中所示[设置文件夹权限](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)和[将部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-285">If your application needs write access to a sub-folder, you can set permissions for that folder as shown in the [Setting Folder Permissions](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md) and [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorials.</span></span> <span data-ttu-id="9f1a5-286">如果你的应用程序需要的站点的根文件夹的写访问权限，则必须防止它在根文件夹上设置只读访问权限，通过添加**&lt;IncludeSetACLProviderOn 目标&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 到发布配置文件 （以影响一个配置文件） 或 （要影响的所有配置文件） 的 wpp.targets 文件。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-286">If your application needs write access to the root folder of the site, you have to prevent it from setting read-only access on the root folder by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="9f1a5-287">有关如何编辑这些文件的信息，请参阅[如何： 编辑配置文件 (.pubxml) 文件中的部署设置](https://msdn.microsoft.com/library/ff398069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-287">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span> <a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a><span data-ttu-id="9f1a5-288">配置错误的 targetFramework 特性引用晚于安装的.NET Framework 版本的版本</span><span class="sxs-lookup"><span data-stu-id="9f1a5-288">Configuration Error - targetFramework attribute references a version that is later than the installed version of the .NET Framework</span></span>

### <a name="scenario"></a><span data-ttu-id="9f1a5-289">方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-289">Scenario</span></span>

<span data-ttu-id="9f1a5-290">已成功发布的 web 项目是面向 ASP.NET 4.5，但当你运行应用程序 (与`customErrors`模式设置为"关闭"Web.config 文件中) 收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-290">You successfully published a web project that targets ASP.NET 4.5, but when you run the application (with the `customErrors` mode set to "off" in the Web.config file) you get the following error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample24.cmd)]

<span data-ttu-id="9f1a5-291">错误页的源错误框突出从 Web.config 的以下行显示为错误的原因：</span><span class="sxs-lookup"><span data-stu-id="9f1a5-291">The Source Error box of the error page highlights the following line from Web.config as the cause of the error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample25.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="9f1a5-292">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="9f1a5-292">Possible Cause and Solution</span></span>

<span data-ttu-id="9f1a5-293">服务器不支持 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-293">The server does not support ASP.NET 4.5.</span></span> <span data-ttu-id="9f1a5-294">联系托管提供商来确定何时及是否可添加对 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-294">Contact the hosting provider to determine when and if support for ASP.NET 4.5 can be added.</span></span> <span data-ttu-id="9f1a5-295">如果升级服务器不是一个选项，则必须部署面向 4 或更早版本的 ASP.NET web 项目相反。如果将 ASP.NET 4 或更早版本的 web 项目部署到相同的目标中，选择**删除目标位置的其他文件**上的复选框**设置**选项卡**发布 Web**向导。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-295">If upgrading the server is not an option, you have to deploy a web project that targets ASP.NET 4 or earlier instead.If you deploy an ASP.NET 4 or earlier web project to the same destination, select the **Remove additional files at destination** check box on the **Settings** tab of the **Publish Web** wizard.</span></span> <span data-ttu-id="9f1a5-296">如果你未选中**删除目标位置的其他文件**，你将继续获取配置错误页。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-296">If you don't select **Remove additional files at destination**, you will continue to get the Configuration Error page.</span></span>

<span data-ttu-id="9f1a5-297">项目**属性**windows 包含目标框架下拉列表，但你不能解决此问题通过只需更改，从 **.NET Framework 4.5**到 **.NET Framework 4**.</span><span class="sxs-lookup"><span data-stu-id="9f1a5-297">The project **Properties** windows includes a Target framework drop-down list, but you can't resolve this problem by just changing that from **.NET Framework 4.5** to **.NET Framework 4**.</span></span> <span data-ttu-id="9f1a5-298">如果你将目标框架更改为更早版本的 framework 版本时，项目将仍具有对的更高版本的 framework 版本的程序集的引用，而不会运行。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-298">If you change the target framework to an earlier framework version, the project will still have references to the later framework version's assemblies and will not run.</span></span> <span data-ttu-id="9f1a5-299">你必须手动更改这些引用，或创建新的项目面向.NET Framework 4 或更早版本。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-299">You have to manually change those references or create a new project that targets .NET Framework 4 or earlier.</span></span> <span data-ttu-id="9f1a5-300">有关详细信息，请参阅[.NET Framework 面向网站](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="9f1a5-300">For more information, see [.NET Framework Targeting for Web Sites](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9f1a5-301">上一篇</span><span class="sxs-lookup"><span data-stu-id="9f1a5-301">Previous</span></span>](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
