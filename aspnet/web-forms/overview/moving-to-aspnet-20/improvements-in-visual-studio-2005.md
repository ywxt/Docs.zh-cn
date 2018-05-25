---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Visual Studio 2005 中的改进 |Microsoft 文档
author: microsoft
description: Visual Studio 2005 提供 Web 应用程序开发人员的改进和增强功能，Web 项目的长列表。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: aafc59980e807677d6023110d324365ce92bb5fc
ms.sourcegitcommit: d8aa1d314891e981460b5e5c912afb730adbb3ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2018
---
<a name="improvements-in-visual-studio-2005"></a><span data-ttu-id="6072c-103">Visual Studio 2005 中的改进</span><span class="sxs-lookup"><span data-stu-id="6072c-103">Improvements in Visual Studio 2005</span></span>
====================
<span data-ttu-id="6072c-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6072c-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6072c-105">Visual Studio 2005 提供 Web 应用程序开发人员的改进和增强功能，Web 项目的长列表。</span><span class="sxs-lookup"><span data-stu-id="6072c-105">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span>


<span data-ttu-id="6072c-106">Visual Studio 2005 提供 Web 应用程序开发人员的改进和增强功能，Web 项目的长列表。</span><span class="sxs-lookup"><span data-stu-id="6072c-106">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span> <span data-ttu-id="6072c-107">具有强大的功能与 Visual Studio.NET 2002年和 2003年，许多投诉中包括的 Web 项目已处理的方式。</span><span class="sxs-lookup"><span data-stu-id="6072c-107">As powerful as Visual Studio .NET 2002 and 2003 are, there were many complaints in the way that Web projects were handled.</span></span> <span data-ttu-id="6072c-108">Visual Studio 2005 将大量新功能添加为了解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="6072c-108">Visual Studio 2005 adds a significant number of new features in order to address these complaints.</span></span> <span data-ttu-id="6072c-109">有关这些喜欢 Visual Studio.NET 2003 中处理的 Web 应用程序的编译方式，请参见[Web 应用程序项目](https://go.microsoft.com/fwlink/?LinkId=57870)。</span><span class="sxs-lookup"><span data-stu-id="6072c-109">For those who prefer the way that Visual Studio .NET 2003 handled compilation of Web applications, see [Web Application Projects](https://go.microsoft.com/fwlink/?LinkId=57870).</span></span>

<span data-ttu-id="6072c-110">在此模块中，也包含 Web 项目创建、 管理和开发中的改进。</span><span class="sxs-lookup"><span data-stu-id="6072c-110">In this module, well cover improvements in Web project creation, management, and development.</span></span> <span data-ttu-id="6072c-111">在更高版本的模块，涵盖了很好地生成 Web 项目并将它们部署中的改进。</span><span class="sxs-lookup"><span data-stu-id="6072c-111">In a later module, well cover improvements in building Web projects and deploying them.</span></span>

## <a name="frontpage-server-extensions"></a><span data-ttu-id="6072c-112">FrontPage 服务器扩展</span><span class="sxs-lookup"><span data-stu-id="6072c-112">FrontPage Server Extensions</span></span>

<span data-ttu-id="6072c-113">Visual Studio.NET 2002年和 2003年所需在框上才能创建或构建 Web 项目的 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="6072c-113">Visual Studio .NET 2002 and 2003 required FrontPage Server Extensions on the box in order to create or build Web projects.</span></span> <span data-ttu-id="6072c-114">开发人员未之间进行选择两种不同的访问模式 （FrontPage 服务器扩展或文件访问模式），这两种使用 FrontPage 服务器扩展来执行任务，例如在 IIS 等设置的应用程序根目录。</span><span class="sxs-lookup"><span data-stu-id="6072c-114">Developers did have a choice between two different access modes (FrontPage Server Extensions or File access mode), both used FrontPage Server Extensions to perform tasks such as setting the application root in IIS, etc.</span></span>

<span data-ttu-id="6072c-115">Visual Studio 2005 中移除而言，对于本地项目依赖于 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="6072c-115">Visual Studio 2005 removes the reliance on FrontPage Server Extensions for local projects.</span></span> <span data-ttu-id="6072c-116">Visual Studio 2005 现在访问 IIS 元数据库直接而不是使用 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="6072c-116">Visual Studio 2005 now accesses the IIS metabase directly instead of using the FrontPage Server Extensions.</span></span> <span data-ttu-id="6072c-117">Visual Studio 2005 还将添加对 FTP 这允许远程项目访问而无需 FrontPage 服务器扩展的支持。</span><span class="sxs-lookup"><span data-stu-id="6072c-117">Visual Studio 2005 also adds support for FTP which allows for remote project access without requiring FrontPage Server Extensions.</span></span>

<span data-ttu-id="6072c-118">对于那些开发人员想要在其项目中使用 FrontPage 服务器扩展，该选项是仍然可用。</span><span class="sxs-lookup"><span data-stu-id="6072c-118">For those developers who want to use FrontPage Server Extensions in their projects, the option is still available.</span></span> <span data-ttu-id="6072c-119">但是，基于强的 ASP.NET 开发人员社区反馈，它不是一项要求。</span><span class="sxs-lookup"><span data-stu-id="6072c-119">However, based upon strong feedback from the ASP.NET developer community, it is not a requirement.</span></span>

> [!NOTE]
> <span data-ttu-id="6072c-120">FrontPage 服务器扩展插件是仍然需要远程项目创建、 打开，等等。</span><span class="sxs-lookup"><span data-stu-id="6072c-120">FrontPage Server Extensions are still required for remote project creation, opening, etc.</span></span>


## <a name="aspnet-development-server"></a><span data-ttu-id="6072c-121">ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="6072c-121">ASP.NET Development Server</span></span>

<span data-ttu-id="6072c-122">Visual Studio 2005 附带了新的 Web 服务器称为 ASP.NET 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="6072c-122">Visual Studio 2005 ships with a new Web server called ASP.NET Development Server.</span></span> <span data-ttu-id="6072c-123">（此 Web 服务器以前称为 Cassini。）</span><span class="sxs-lookup"><span data-stu-id="6072c-123">(This Web server was previously known as Cassini.)</span></span>

<span data-ttu-id="6072c-124">有很多好处的 ASP.NET 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="6072c-124">There are several benefits of the ASP.NET Development Server.</span></span>

- <span data-ttu-id="6072c-125">现可能非管理员用于开发和调试针对 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="6072c-125">It is now possible for non-Administrators to develop and debug against a Web server.</span></span>
- <span data-ttu-id="6072c-126">ASP.NET Development Server 动态映射虚拟目录到的任何位置允许灵活项目位置的文件系统中。</span><span class="sxs-lookup"><span data-stu-id="6072c-126">The ASP.NET Development Server dynamically maps virtual directories to any location in the file system allowing for flexible project locations.</span></span>
- <span data-ttu-id="6072c-127">现在，已在使用 IIS 在 Windows XP Professional 上的用户将能够创建新的 Web 应用程序将不会影响其默认网站在 IIS 中的文件或文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="6072c-127">Users on Windows XP Professional who are already using IIS will now be able to create new Web applications that will not affect the file or folder structure of their Default Web Site in IIS.</span></span>

<span data-ttu-id="6072c-128">充分利用 ASP.NET 开发服务器不需要任何特殊的配置。</span><span class="sxs-lookup"><span data-stu-id="6072c-128">No special configuration is required to take advantage of the ASP.NET Development Server.</span></span> <span data-ttu-id="6072c-129">调试或浏览文件系统承载的 Web 项目后，Visual Studio 2005 在随机端口，以请求提供服务上将自动启动 ASP.NET Development Server 的实例。</span><span class="sxs-lookup"><span data-stu-id="6072c-129">When a Web project that is hosted on the file system is debugged or browsed, Visual Studio 2005 will automatically start an instance of the ASP.NET Development Server on a random port to service the request.</span></span>

<span data-ttu-id="6072c-130">在 ASP.NET 开发服务器上更高版本在此模块将在详细信息。</span><span class="sxs-lookup"><span data-stu-id="6072c-130">More information will be covered on the ASP.NET Development Server later in this module.</span></span>

## <a name="improved-file-management"></a><span data-ttu-id="6072c-131">增强对文件管理</span><span class="sxs-lookup"><span data-stu-id="6072c-131">Improved File Management</span></span>

<span data-ttu-id="6072c-132">在 Visual Studio 2002 和 2003年中，项目文件 (对于 VB.NET.vbproj) 和 C# 中为.csproj 存储在 Web 应用程序中的所有文件的信息。</span><span class="sxs-lookup"><span data-stu-id="6072c-132">In Visual Studio 2002 and 2003, a project file (.vbproj for VB.NET and .csproj for C#) stored information on all files in the Web application.</span></span> <span data-ttu-id="6072c-133">解决方案资源管理器显示取决于项目文件中的文件信息。</span><span class="sxs-lookup"><span data-stu-id="6072c-133">The Solution Explorer display is based upon the file information in the project file.</span></span> <span data-ttu-id="6072c-134">因此，解决方案资源管理器通常将在其中使用外部编辑器的情况下显示不准确的信息。</span><span class="sxs-lookup"><span data-stu-id="6072c-134">Because of this, the Solution Explorer would often display inaccurate information in cases where external editors were used.</span></span> <span data-ttu-id="6072c-135">Visual Studio 2002 和 2003年将通常覆盖文件更改，或者不会显示文件的最新版本。</span><span class="sxs-lookup"><span data-stu-id="6072c-135">Visual Studio 2002 and 2003 would often overwrite file changes or not display the most recent version of files.</span></span>

<span data-ttu-id="6072c-136">Visual Studio 2005 项目文件进行消失。</span><span class="sxs-lookup"><span data-stu-id="6072c-136">Visual Studio 2005 does away with the project file.</span></span> <span data-ttu-id="6072c-137">相反，它直接从磁盘，从而导致准确显示你的项目中的文件读取的文件和文件夹信息。</span><span class="sxs-lookup"><span data-stu-id="6072c-137">Instead, it reads the file and folder information directly from the disk, resulting in an accurate display of the files in your project.</span></span> <span data-ttu-id="6072c-138">在 Visual Studio 2002 和 2003年引用文件夹不表示 Web 应用程序中的实际文件夹，因为 Visual Studio 2005 还会从解决方案资源管理器中删除引用文件夹。</span><span class="sxs-lookup"><span data-stu-id="6072c-138">Because the References folder in Visual Studio 2002 and 2003 does not represent an actual folder in your Web application, Visual Studio 2005 also removes the References folder from Solution Explorer.</span></span> <span data-ttu-id="6072c-139">若要访问 Visual Studio 2005 中的项目的引用，你应使用项目属性页。</span><span class="sxs-lookup"><span data-stu-id="6072c-139">To access the references for your project in Visual Studio 2005, you should use the Property pages for the project.</span></span>

## <a name="creating-web-projects"></a><span data-ttu-id="6072c-140">创建 Web 项目</span><span class="sxs-lookup"><span data-stu-id="6072c-140">Creating Web Projects</span></span>

<span data-ttu-id="6072c-141">Web 开发人员在 Visual Studio 2005 中有许多可用于项目创建的新选项。</span><span class="sxs-lookup"><span data-stu-id="6072c-141">Web developers have many new options available for project creation in Visual Studio 2005.</span></span> <span data-ttu-id="6072c-142">网站文件系统中现在在任何位置创建，然后可以调试或浏览使用新的 ASP.NET 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="6072c-142">Web sites can now be created anywhere in the file system and can then be debugged or browsed using the new ASP.NET Development Server.</span></span> <span data-ttu-id="6072c-143">开发人员还可以创建新的网站使用 FTP。</span><span class="sxs-lookup"><span data-stu-id="6072c-143">Developers can also create new Web sites using FTP.</span></span>

<span data-ttu-id="6072c-144">若要查看在 Visual Studio 2005 中创建 Web 项目的视频演练，请单击此处。</span><span class="sxs-lookup"><span data-stu-id="6072c-144">Click here to view a video walkthrough of creating Web projects in Visual Studio 2005.</span></span>


![](improvements-in-visual-studio-2005/_static/image1.png)


[<span data-ttu-id="6072c-145">打开全屏幕视频</span><span class="sxs-lookup"><span data-stu-id="6072c-145">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)


### <a name="file-system-projects"></a><span data-ttu-id="6072c-146">文件系统项目</span><span class="sxs-lookup"><span data-stu-id="6072c-146">File System Projects</span></span>

<span data-ttu-id="6072c-147">正如你看到视频演练中，你可以选择在本地计算机上或远程位置通过文件共享上文件系统上创建网站。</span><span class="sxs-lookup"><span data-stu-id="6072c-147">As you saw in the video walkthrough, you can choose to create Web sites on the file system either on the local machine or on a remote location via a file share.</span></span> <span data-ttu-id="6072c-148">在文件系统创建的网站的浏览和调试使用 ASP.NET 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="6072c-148">Web sites that are created on the file system are browsed and debugged using the ASP.NET Development Server.</span></span>

> [!NOTE]
> <span data-ttu-id="6072c-149">ASP.NET 开发服务器可能会导致某些混淆的客户。</span><span class="sxs-lookup"><span data-stu-id="6072c-149">The ASP.NET Development Server may cause some confusion for customers.</span></span> <span data-ttu-id="6072c-150">如果 IISs 目录结构 (即 c: / inetpub/wwwroot) 中的文件系统上创建 Web 项目，则将仍可通过 ASP.NET 开发服务器在从 Visual Studio 2005 内启动时浏览网站。</span><span class="sxs-lookup"><span data-stu-id="6072c-150">If a Web project is created on the file system in IISs directory structure (i.e. c:/inetpub/wwwroot), the Web site will still be browsed via the ASP.NET Development Server when launched from within Visual Studio 2005.</span></span> <span data-ttu-id="6072c-151">因此，任何 IIS 配置 （即身份验证方法） 不适用。</span><span class="sxs-lookup"><span data-stu-id="6072c-151">Therefore, any IIS configuration (i.e. authentication methods) is not applicable.</span></span>


<span data-ttu-id="6072c-152">大量还会删除默认 web 项目中的系统开销通过仅包括 Default.aspx 页、 default.cs 文件和应用程序/_Data 文件夹。</span><span class="sxs-lookup"><span data-stu-id="6072c-152">The default web project also removes a lot of the overhead by only includes a Default.aspx page, default.cs file, and an App/_Data folder.</span></span> <span data-ttu-id="6072c-153">需要添加 web.config 和特殊文件夹 (即应用程序/_code)。</span><span class="sxs-lookup"><span data-stu-id="6072c-153">The web.config and special folders (i.e. app/_code) are added as they are needed.</span></span> <span data-ttu-id="6072c-154">你的 web 项目仅包括的文件和你需要的文件夹。</span><span class="sxs-lookup"><span data-stu-id="6072c-154">Your web project only includes the files and folders that you need.</span></span>

### <a name="http-projects"></a><span data-ttu-id="6072c-155">HTTP 项目</span><span class="sxs-lookup"><span data-stu-id="6072c-155">HTTP Projects</span></span>

<span data-ttu-id="6072c-156">HTTP 项目可以是本地 IIS 网站上或远程网站上创建的项目。</span><span class="sxs-lookup"><span data-stu-id="6072c-156">HTTP projects can either be projects that are created on a local IIS Web site or on a remote Web site.</span></span> <span data-ttu-id="6072c-157">默认项目位置`http://localhost`。</span><span class="sxs-lookup"><span data-stu-id="6072c-157">The default project location is `http://localhost`.</span></span> <span data-ttu-id="6072c-158">如果单击浏览按钮时，有两个 HTTP 选项： 本地 IIS 和远程站点。</span><span class="sxs-lookup"><span data-stu-id="6072c-158">If you click the Browse button, there are two HTTP options: Local IIS and Remote Site.</span></span> <span data-ttu-id="6072c-159">在这两个选项中的主要区别是 web 站点的信息在其中显示在选择位置对话框中和如何将文件复制到 Web 服务器的方法。</span><span class="sxs-lookup"><span data-stu-id="6072c-159">The main difference in these two options is the method in which the web site information is displayed in the Choose Location dialog and in how the files are copied to the Web server.</span></span>

<span data-ttu-id="6072c-160">本地 IIS 选项从本地计算机上的元数据库读取站点信息并将文件复制使用文件系统。</span><span class="sxs-lookup"><span data-stu-id="6072c-160">The Local IIS option reads the site information from the metabase on the local machine and files are copied using the file system.</span></span> <span data-ttu-id="6072c-161">远程站点选项使用 FrontPage 服务器扩展和站点信息和文件将复制使用 HTTP，FrontPage 服务器扩展 RPC 调用。</span><span class="sxs-lookup"><span data-stu-id="6072c-161">The Remote Site option uses the FrontPage Server Extensions and the site information and files are copied using HTTP and FrontPage Server Extensions RPC calls.</span></span>

> [!NOTE]
> <span data-ttu-id="6072c-162">Vs###/_tmp.htm 文件和 get/_aspx/_ver.aspx 不再用于确定版本信息。</span><span class="sxs-lookup"><span data-stu-id="6072c-162">The vs###/_tmp.htm file and get/_aspx/_ver.aspx are no longer used to determine version information.</span></span>


<span data-ttu-id="6072c-163">默认 HTTP 选项是本地 IIS。</span><span class="sxs-lookup"><span data-stu-id="6072c-163">The default HTTP option is Local IIS.</span></span> <span data-ttu-id="6072c-164">此选项读取 IIS 元数据库，若要确定哪些站点可用，并要在其中创建内容的位置。</span><span class="sxs-lookup"><span data-stu-id="6072c-164">This option reads the IIS Metabase to determine which sites are available and the location in which to create content.</span></span> <span data-ttu-id="6072c-165">可以通过在树视图中选择该选择不同的文件夹或虚拟目录。</span><span class="sxs-lookup"><span data-stu-id="6072c-165">You can select a different folder or virtual directory by selecting it in the tree view.</span></span> <span data-ttu-id="6072c-166">你可以还创建一个新的虚拟目录，将标记为应用程序的文件夹，以及从该对话框中删除现有的虚拟目录。</span><span class="sxs-lookup"><span data-stu-id="6072c-166">You can also create a new virtual directory, mark folders as applications, as well as delete existing virtual directories from this dialog box.</span></span>


![选择位置对话框](improvements-in-visual-studio-2005/_static/image1.gif)

<span data-ttu-id="6072c-168">**图 1**: 选择位置对话框</span><span class="sxs-lookup"><span data-stu-id="6072c-168">**Figure 1**: The Choose Location Dialog</span></span>


<span data-ttu-id="6072c-169">与不同在早期版本的 Visual Studio 中，如果你检查**使用安全套接字层**复选框和 SSL 证书与您在浏览的 URL 不匹配，你将看到一个安全警报的对话框，询问你是否你将要处理。</span><span class="sxs-lookup"><span data-stu-id="6072c-169">Unlike in earlier versions of Visual Studio, if you check the **Use Secure Sockets Layer** checkbox and the SSL certificate does not match the URL you are browsing, you will be presented with a Security Alert dialog asking you if you would like to proceed.</span></span> <span data-ttu-id="6072c-170">使用 Visual Studio.NET 2003 中，如果证书不是一个匹配，创建项目将失败。</span><span class="sxs-lookup"><span data-stu-id="6072c-170">Using Visual Studio .NET 2003, if the certificate was not a matching one, creating the project would fail.</span></span>


![安全警报的有关 SSL 证书](improvements-in-visual-studio-2005/_static/image2.gif)

<span data-ttu-id="6072c-172">**图 2**： 有关 SSL 证书的安全警报</span><span class="sxs-lookup"><span data-stu-id="6072c-172">**Figure 2**: Security Alert Regarding SSL Certificate</span></span>


### <a name="note-on-host-headers"></a><span data-ttu-id="6072c-173">有关主机头的说明</span><span class="sxs-lookup"><span data-stu-id="6072c-173">Note on Host Headers</span></span>

<span data-ttu-id="6072c-174">如果要在一个绑定到特定 IP 的站点创建 Web 应用程序，你将需要确保配置主机标头。</span><span class="sxs-lookup"><span data-stu-id="6072c-174">If you are creating a Web application on a site bound to a specific IP, you will need to ensure that a host header is configured.</span></span> <span data-ttu-id="6072c-175">否则，Visual Studio 将创建以下站点`http://localhost`，但站点处于浏览或从 IDE 中调试时，IP 地址将无法正确解析。</span><span class="sxs-lookup"><span data-stu-id="6072c-175">Otherwise, Visual Studio will create the site at `http://localhost`, but the IP address will not resolve correctly when the site is browsed or debugged from within the IDE.</span></span>

<span data-ttu-id="6072c-176">如果选择远程站点选项，该对话框会更改，以便您可以输入新的 Web 站点的目标 URL。</span><span class="sxs-lookup"><span data-stu-id="6072c-176">If you select the Remote Site option, the dialog changes to allow you to enter the destination URL for the new Web site.</span></span> <span data-ttu-id="6072c-177">此 URL 必须是已启用 FrontPage 服务器扩展的服务器上。</span><span class="sxs-lookup"><span data-stu-id="6072c-177">This URL must be on a server that has the FrontPage Server Extensions enabled.</span></span> <span data-ttu-id="6072c-178">如果你想要使用你本地 Web 服务器上使用 FrontPage 服务器扩展，你可以使用远程站点选项并指定本地 URL。</span><span class="sxs-lookup"><span data-stu-id="6072c-178">If you want to work with your local Web server using the FrontPage Server Extensions, you can use the Remote Site option and specify a local URL.</span></span>


![在远程服务器上创建网站](improvements-in-visual-studio-2005/_static/image1.jpg)

<span data-ttu-id="6072c-180">**图 3**： 在远程服务器上创建网站</span><span class="sxs-lookup"><span data-stu-id="6072c-180">**Figure 3**: Creating a Web Site on a Remote Server</span></span>


<span data-ttu-id="6072c-181">如果不匹配的 SSL 证书，请在通过 SSL，远程站点上创建应用程序，确认对话框时，略有不同于使用本地 IIS 选项时显示的对话框。</span><span class="sxs-lookup"><span data-stu-id="6072c-181">When creating an application on a remote site via SSL, if the SSL certificate does not match, the confirmation dialog is slightly different than the dialog displayed when using the Local IIS option.</span></span>


![远程站点安全警报](improvements-in-visual-studio-2005/_static/image3.gif)

<span data-ttu-id="6072c-183">**图 4**： 远程站点安全警报</span><span class="sxs-lookup"><span data-stu-id="6072c-183">**Figure 4**: The Remote Site Security Alert</span></span>


<a id="_Toc116100243"></a>

#### <a name="ftp"></a><span data-ttu-id="6072c-184">FTP</span><span class="sxs-lookup"><span data-stu-id="6072c-184">FTP</span></span>

<span data-ttu-id="6072c-185">Visual Studio 2005 中引入了用于创建通过 FTP 的网站的选项。</span><span class="sxs-lookup"><span data-stu-id="6072c-185">Visual Studio 2005 introduces the option to create Web sites via FTP.</span></span> <span data-ttu-id="6072c-186">当你使用此选项时，IDE 的用户临时文件夹中本地创建文件，然后使用 FTP 将文件移到的 FTP 位置。</span><span class="sxs-lookup"><span data-stu-id="6072c-186">When you use this option, the IDE creates the files locally in the users temp folder and then uses FTP to move the files to the FTP location.</span></span>

> [!NOTE]
> <span data-ttu-id="6072c-187">临时文件夹位置是 c: / Documents and Settings /&lt;用户&gt;/本地设置/Temp/VWDWebCache/&lt;服务器&gt;/_&lt;应用程序名称&gt;</span><span class="sxs-lookup"><span data-stu-id="6072c-187">The temp folder location is c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>


<span data-ttu-id="6072c-188">使用 FTP 选项时，你将显示选择位置对话框。</span><span class="sxs-lookup"><span data-stu-id="6072c-188">When using the FTP option, you will be presented with a Choose Location dialog.</span></span> <span data-ttu-id="6072c-189">在此对话框，如下所示输入所需的 FTP 连接信息。</span><span class="sxs-lookup"><span data-stu-id="6072c-189">You enter the required FTP connection information into this dialog as shown below.</span></span>


![选择 ftp 位置对话框](improvements-in-visual-studio-2005/_static/image2.jpg)

<span data-ttu-id="6072c-191">**图 5**: 选择 ftp 位置对话框</span><span class="sxs-lookup"><span data-stu-id="6072c-191">**Figure 5**: The Choose Location Dialog for FTP</span></span>


## <a name="lab-setup-ftp-site-and-create-a-project"></a><span data-ttu-id="6072c-192">实验室： 设置 FTP 站点，并创建一个项目</span><span class="sxs-lookup"><span data-stu-id="6072c-192">Lab: Setup FTP site and create a project</span></span>

<span data-ttu-id="6072c-193">以下步骤配置的 FTP 站点，使用户具有只有他们可以通过 FTP 上载到的位置。</span><span class="sxs-lookup"><span data-stu-id="6072c-193">The following steps configure the FTP site so that a user has a location that only they can upload to via FTP.</span></span>

### <a name="install-the-ftp-service"></a><span data-ttu-id="6072c-194">安装 FTP 服务</span><span class="sxs-lookup"><span data-stu-id="6072c-194">Install the FTP Service</span></span>

1. <span data-ttu-id="6072c-195">打开添加或删除程序，选择添加/删除 Windows 组件</span><span class="sxs-lookup"><span data-stu-id="6072c-195">Open Add Remove Programs, select Add/Remove Windows Components</span></span>
2. <span data-ttu-id="6072c-196">选择 Internet 信息服务 （Windows 2003 上的应用程序服务器），然后单击**详细信息**。</span><span class="sxs-lookup"><span data-stu-id="6072c-196">Select Internet Information Services (Application Server on Windows 2003) and click **Details**.</span></span>
3. <span data-ttu-id="6072c-197">检查**文件传输协议 (FTP) 服务**单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="6072c-197">Check **File Transfer Protocol (FTP) Service** and click **OK**.</span></span>
4. <span data-ttu-id="6072c-198">单击**下一步**安装 FTP 服务。</span><span class="sxs-lookup"><span data-stu-id="6072c-198">Click **Next** to install the FTP service.</span></span>

### <a name="create-a-new-folder-for-content"></a><span data-ttu-id="6072c-199">为内容创建一个新文件夹</span><span class="sxs-lookup"><span data-stu-id="6072c-199">Create a New Folder for Content</span></span>

1. <span data-ttu-id="6072c-200">在 Windows 资源管理器，创建一个名为的新文件夹**User1** c: / inetpub/wwwroot 内。</span><span class="sxs-lookup"><span data-stu-id="6072c-200">In Windows Explorer, create a new folder called **User1** inside of c:/inetpub/wwwroot.</span></span>

#### <a name="configure-folders-and-permissions-on-folders"></a><span data-ttu-id="6072c-201">在文件夹上配置文件夹和权限。</span><span class="sxs-lookup"><span data-stu-id="6072c-201">Configure folders and permissions on folders.</span></span>

1. <span data-ttu-id="6072c-202">从管理工具打开 Internet 信息服务管理单元中。</span><span class="sxs-lookup"><span data-stu-id="6072c-202">Open the Internet Information Services snap-in from Administrative Tools.</span></span> <span data-ttu-id="6072c-203">现在，你将有计算机名称节点下的 FTP 站点文件夹。</span><span class="sxs-lookup"><span data-stu-id="6072c-203">You will now have an FTP Sites folder under the computer name node.</span></span>
2. <span data-ttu-id="6072c-204">展开**FTP 站点**。</span><span class="sxs-lookup"><span data-stu-id="6072c-204">Expand **FTP Sites**.</span></span>
3. <span data-ttu-id="6072c-205">右键单击**默认 FTP 站点**，选择**新建**，然后**虚拟目录**，然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="6072c-205">Right-click the **Default FTP Site**, select **New**, then **Virtual Directory**, then click **Next**.</span></span>
4. <span data-ttu-id="6072c-206">输入**User1**虚拟目录名称然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="6072c-206">Enter **User1** for the virtual directory name and click **Next**.</span></span>
5. <span data-ttu-id="6072c-207">输入**c: / inetpub/wwwroot/User1**的路径和单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="6072c-207">Enter **c:/inetpub/wwwroot/User1** for the path and click **Next**.</span></span>
6. <span data-ttu-id="6072c-208">单击**下一步**然后**完成**以完成向导。</span><span class="sxs-lookup"><span data-stu-id="6072c-208">Click **Next** and then **Finish** to complete the wizard.</span></span>
7. <span data-ttu-id="6072c-209">右键单击**User1**默认 FTP 站点，然后选择下的虚拟目录**属性**。</span><span class="sxs-lookup"><span data-stu-id="6072c-209">Right-click the **User1** virtual directory under Default FTP Site and select **Properties**.</span></span>
8. <span data-ttu-id="6072c-210">检查**编写**复选框，然后单击**确定**关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="6072c-210">Check the **Write** checkbox and click **OK** to close the dialog.</span></span>
9. <span data-ttu-id="6072c-211">右键单击**默认 FTP 站点**和选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="6072c-211">Right-click **Default FTP Site** and select **Properties**.</span></span>
10. <span data-ttu-id="6072c-212">上**安全帐户**选项卡上，取消选中**允许匿名连接**。</span><span class="sxs-lookup"><span data-stu-id="6072c-212">On the **Security Accounts** tab, uncheck **Allow Anonymous Connections**.</span></span>
11. <span data-ttu-id="6072c-213">单击**是**询问您是否要继续对话框中。</span><span class="sxs-lookup"><span data-stu-id="6072c-213">Click **Yes** in the dialog asking if you want to continue.</span></span>
12. <span data-ttu-id="6072c-214">单击**确定**关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="6072c-214">Click **OK** to close the dialog.</span></span>
13. <span data-ttu-id="6072c-215">展开**Default Web Site**下**网站**节点。</span><span class="sxs-lookup"><span data-stu-id="6072c-215">Expand the **Default Web Site** under the **Web Sites** node.</span></span>
14. <span data-ttu-id="6072c-216">右键单击**User1**目录，然后选择**属性**</span><span class="sxs-lookup"><span data-stu-id="6072c-216">Right-click the **User1** directory and select **Properties**</span></span>
15. <span data-ttu-id="6072c-217">在**应用程序设置**部分中，单击**创建**将标记为应用程序的文件夹。</span><span class="sxs-lookup"><span data-stu-id="6072c-217">In the **Application Settings** section, click **Create** to mark the folder as an application.</span></span>
16. <span data-ttu-id="6072c-218">单击**确定**关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="6072c-218">Click **OK** to close the dialog.</span></span>
17. <span data-ttu-id="6072c-219">关闭 Internet Information Services 管理单元。</span><span class="sxs-lookup"><span data-stu-id="6072c-219">Close the Internet Information Services snap-in.</span></span>

### <a name="create-web-project"></a><span data-ttu-id="6072c-220">创建 web 项目</span><span class="sxs-lookup"><span data-stu-id="6072c-220">Create web project</span></span>

1. <span data-ttu-id="6072c-221">打开 Visual Studio 2005。</span><span class="sxs-lookup"><span data-stu-id="6072c-221">Open Visual Studio 2005.</span></span>
2. <span data-ttu-id="6072c-222">从**文件**菜单上，选择**新网站**。</span><span class="sxs-lookup"><span data-stu-id="6072c-222">From the **File** menu, select **New Web Site**.</span></span>
3. <span data-ttu-id="6072c-223">在**位置**下拉列表中，选择**FTP**。</span><span class="sxs-lookup"><span data-stu-id="6072c-223">In the **Location** dropdown, select **FTP**.</span></span>
4. <span data-ttu-id="6072c-224">单击“浏览” 。</span><span class="sxs-lookup"><span data-stu-id="6072c-224">Click **Browse**.</span></span>
5. <span data-ttu-id="6072c-225">输入**localhost**中**服务器**文本框。</span><span class="sxs-lookup"><span data-stu-id="6072c-225">Enter **localhost** in the **Server** textbox.</span></span>
6. <span data-ttu-id="6072c-226">输入**User1**在目录文本框中。</span><span class="sxs-lookup"><span data-stu-id="6072c-226">Enter **User1** in the Directory textbox.</span></span>
7. <span data-ttu-id="6072c-227">单击**打开**。</span><span class="sxs-lookup"><span data-stu-id="6072c-227">Click **Open**.</span></span> <span data-ttu-id="6072c-228">FTP 位置将输入到新建网站对话框。</span><span class="sxs-lookup"><span data-stu-id="6072c-228">The FTP location will be entered into the New Web Site dialog.</span></span>
8. <span data-ttu-id="6072c-229">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="6072c-229">Click **OK**.</span></span>
9. <span data-ttu-id="6072c-230">取消选中**匿名登录**在 FTP 登录对话框中，输入你的凭据，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="6072c-230">Uncheck **Anonymous log on** in the FTP Log On dialog, enter your credentials, and click **OK**.</span></span>
10. <span data-ttu-id="6072c-231">项目的 URL 是什么？</span><span class="sxs-lookup"><span data-stu-id="6072c-231">What is the URL for the project?</span></span> <span data-ttu-id="6072c-232">（该项目的 URL 将显示在解决方案资源管理器。）</span><span class="sxs-lookup"><span data-stu-id="6072c-232">(The URL for the project will be displayed in Solution Explorer.)</span></span>
11. <span data-ttu-id="6072c-233">从**生成**菜单上，选择**生成网站**或**生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="6072c-233">From the **Build** menu, select **Build Web Site** or **Build Solution**.</span></span>
12. <span data-ttu-id="6072c-234">右键单击解决方案资源管理器中的 Default.aspx，然后选择**用浏览器查看**。</span><span class="sxs-lookup"><span data-stu-id="6072c-234">Right-click on Default.aspx in Solution Explorer and select **View in Browser**.</span></span>
13. <span data-ttu-id="6072c-235">在要求提供网站 URL 对话框中，输入`http://localhost/user1`的 URL，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="6072c-235">In the Web Site URL Required dialog, enter `http://localhost/user1` for the URL and click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="6072c-236">如果你收到错误，表示无法加载类型 /_Default，请确保您的网站和不早期版本上运行 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="6072c-236">If you get a error indicating an inability to load the type /_Default, make sure that you are running ASP.NET 2.0 on your Web site and not an earlier version.</span></span> <span data-ttu-id="6072c-237">你可以从在 Internet 信息服务中的 ASP.NET 选项卡来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="6072c-237">You can do that from the ASP.NET tab in Internet Information Services.</span></span>


## <a name="opening-web-projects"></a><span data-ttu-id="6072c-238">打开 Web 项目</span><span class="sxs-lookup"><span data-stu-id="6072c-238">Opening Web Projects</span></span>

<span data-ttu-id="6072c-239">打开 Web 项目是类似于创建项目。</span><span class="sxs-lookup"><span data-stu-id="6072c-239">Opening Web projects is similar to creating projects.</span></span> <span data-ttu-id="6072c-240">下列各节调出区域以跟踪出有关 IDE 中工作时。</span><span class="sxs-lookup"><span data-stu-id="6072c-240">The following sections call out areas to keep an eye out for while working within the IDE.</span></span> <span data-ttu-id="6072c-241">它还介绍了与使用 HTTP 和 FTP 的 Web 项目的工作。</span><span class="sxs-lookup"><span data-stu-id="6072c-241">It also covers working with Web projects using HTTP and FTP.</span></span>

<span data-ttu-id="6072c-242">若要打开 Web 项目，请从文件菜单中选择打开网站。</span><span class="sxs-lookup"><span data-stu-id="6072c-242">To open a Web project, select Open Web Site from the File menu.</span></span> <span data-ttu-id="6072c-243">系统将提示您提供以前涵盖相同选择位置对话框，并可以供你使用相同的四个选项： 文件系统、 本地 IIS、 FTP 和远程站点。</span><span class="sxs-lookup"><span data-stu-id="6072c-243">You will be prompted with the same Choose Location dialog covered previously and you have the same four options available to you: File System, Local IIS, FTP, and Remote Site.</span></span>

<a id="_Toc116100245"></a>

## <a name="file-system"></a><span data-ttu-id="6072c-244">文件系统</span><span class="sxs-lookup"><span data-stu-id="6072c-244">File System</span></span>

<span data-ttu-id="6072c-245">如上所述此模块中，Visual Studio 将无法再使用项目文件。</span><span class="sxs-lookup"><span data-stu-id="6072c-245">As indicated previously in this module, Visual Studio no longer uses a project file.</span></span> <span data-ttu-id="6072c-246">因此，如果你选择从文件系统中打开的网站，实际上可以选择你想，任何文件夹，即使你选择的文件夹不作为最初在 Visual Studio 中的 Web 项目创建。</span><span class="sxs-lookup"><span data-stu-id="6072c-246">Therefore, if you choose to open a Web site from the file system, you actually have the option of choosing any folder that you wish, even if the folder you choose was not created as a Web project initially in Visual Studio.</span></span> <span data-ttu-id="6072c-247">例如，你可以选择打开作为网站的我的文档文件夹和 Visual Studio 将不假思索地将其打开并显示你的文件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6072c-247">For example, you can choose to open the My Documents folder as a Web site and Visual Studio will happily open it and display your files as shown below.</span></span>


![我作为网站打开的文档](improvements-in-visual-studio-2005/_static/image3.jpg)

<span data-ttu-id="6072c-249">**图 6**:*我的文档*作为网站打开</span><span class="sxs-lookup"><span data-stu-id="6072c-249">**Figure 6**: *My Documents* Opened As a Web Site</span></span>


<span data-ttu-id="6072c-250">因为 Visual Studio 将仅创建其他文件和文件夹在必要时，没有其他文件或文件夹将添加到你打开的位置。</span><span class="sxs-lookup"><span data-stu-id="6072c-250">Because Visual Studio only creates additional files and folders when necessary, no additional files or folders are added to the location you open.</span></span> <span data-ttu-id="6072c-251">此体系结构的副作用是，它会阻止你嵌套网站文件系统上。</span><span class="sxs-lookup"><span data-stu-id="6072c-251">A side-effect of this architecture is that it prevents you from nesting Web sites on the file system.</span></span> <span data-ttu-id="6072c-252">例如，考虑以下目录结构。</span><span class="sxs-lookup"><span data-stu-id="6072c-252">For example, consider the following directory structure.</span></span>

<span data-ttu-id="6072c-253">在 c: / MyWebSite 的 web 项目</span><span class="sxs-lookup"><span data-stu-id="6072c-253">Web project at C:/MyWebSite</span></span>

<span data-ttu-id="6072c-254">在 c: / MyWebSite/嵌套的另一个 web 项目</span><span class="sxs-lookup"><span data-stu-id="6072c-254">Another web project at C:/MyWebSite/Nested</span></span>

<span data-ttu-id="6072c-255">打开位于 c: / MyWebSite 的网站时，嵌套文件夹将显示为该应用程序的一个子文件夹中。</span><span class="sxs-lookup"><span data-stu-id="6072c-255">When you open the Web site at c:/MyWebSite, the Nested folder will appear as a sub-folder of that application.</span></span>

<a id="_Toc116100246"></a>

## <a name="http"></a><span data-ttu-id="6072c-256">HTTP</span><span class="sxs-lookup"><span data-stu-id="6072c-256">HTTP</span></span>

<span data-ttu-id="6072c-257">在打开时通过 HTTP 的网站，将读取设置，通过 IIS 元数据库 (本地 IIS) 或使用 FrontPage 服务器扩展 （远程站点。）如果有嵌套的 web 应用程序，这些是还显示与将它们标识为应用程序的图标。</span><span class="sxs-lookup"><span data-stu-id="6072c-257">When opening Web sites via HTTP, settings are read either from the IIS metabase (Local IIS) or using FrontPage Server Extensions (Remote Site.) If there are nested web applications, these are displayed as well with an icon identifying them as an application.</span></span> <span data-ttu-id="6072c-258">如果你熟悉使用 FrontPage 中 web 应用程序，Visual Studio 2005 中的行为非常相似。</span><span class="sxs-lookup"><span data-stu-id="6072c-258">If you are familiar with working with web applications in FrontPage, the behavior in Visual Studio 2005 is similar.</span></span>

<span data-ttu-id="6072c-259">即使 Visual Studio 将显示在 IDE 中当前打开的应用程序下嵌套的应用程序的图标，它将不允许你展开它们以查看其内容。</span><span class="sxs-lookup"><span data-stu-id="6072c-259">Even though Visual Studio will display an icon for applications that are nested beneath the application that is currently opened within the IDE, it will not allow you to expand them to see their content.</span></span> <span data-ttu-id="6072c-260">但是，可以双击它们以打开它们。</span><span class="sxs-lookup"><span data-stu-id="6072c-260">You can, however, double-click on them to open them.</span></span> <span data-ttu-id="6072c-261">执行操作时，你将显示一个对话框，提示您打开 web 应用程序 （并替换当前打开的解决方案），也添加到当前解决方案的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6072c-261">When you do, you will be presented with a dialog prompting you to either open the web application (and replace the currently open solution) or add the Web application to your current solution.</span></span>


![双击一个嵌套的应用程序图标展示了此对话框](improvements-in-visual-studio-2005/_static/image4.jpg)

<span data-ttu-id="6072c-263">**图 7**： 双击嵌套的应用程序图标展示了此对话框</span><span class="sxs-lookup"><span data-stu-id="6072c-263">**Figure 7**: Double-clicking a nested application icon presents you with this dialog</span></span>


<a id="_Toc116100247"></a>

## <a name="ftp-site"></a><span data-ttu-id="6072c-264">FTP 站点</span><span class="sxs-lookup"><span data-stu-id="6072c-264">FTP Site</span></span>

<span data-ttu-id="6072c-265">当你打开通过 FTP 站点时，文件所有本地复制到临时文件夹。</span><span class="sxs-lookup"><span data-stu-id="6072c-265">When you open a site via FTP, the files are all copied locally to your temp folder.</span></span> <span data-ttu-id="6072c-266">本地存储位置的完整路径显示在项目属性窗格中，并使用以下格式进行创建。</span><span class="sxs-lookup"><span data-stu-id="6072c-266">The full path for the local storage location is displayed in the Properties pane for the project and is created using the following format.</span></span>

<span data-ttu-id="6072c-267">C: / Documents and Settings /&lt;用户&gt;/本地设置/Temp/VWDWebCache/&lt;服务器&gt;/_&lt;应用程序名称&gt;</span><span class="sxs-lookup"><span data-stu-id="6072c-267">C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="6072c-268">使用 FTP 时，Visual Studio 将需要指定你的项目的基 URL，以便你可以浏览它，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6072c-268">When using FTP, Visual Studio will need to specify the base URL for your project so that you can browse it as shown below.</span></span> <span data-ttu-id="6072c-269">如果未指定基 URL，Visual Studio 会要求您为其第一次尝试浏览网站中的页。</span><span class="sxs-lookup"><span data-stu-id="6072c-269">If you do not specify a base URL, Visual Studio will ask you for it the first time you attempt to browse a page in the Web site.</span></span>


![为 FTP 站点指定的基 URL](improvements-in-visual-studio-2005/_static/image5.jpg)

<span data-ttu-id="6072c-271">**图 8**： 为 FTP 站点指定的基 URL</span><span class="sxs-lookup"><span data-stu-id="6072c-271">**Figure 8**: Specifying a Base URL for FTP Sites</span></span>


## <a name="improvements-in-compilation"></a><span data-ttu-id="6072c-272">在编译中的改进</span><span class="sxs-lookup"><span data-stu-id="6072c-272">Improvements in Compilation</span></span>

<span data-ttu-id="6072c-273">使用 Visual Studio 2005 中的 Web 应用程序是显著比以前版本更快。</span><span class="sxs-lookup"><span data-stu-id="6072c-273">Working with Web applications in Visual Studio 2005 is noticeably faster than previous versions.</span></span> <span data-ttu-id="6072c-274">这是因为在没有小部分编译体系结构中的更改。</span><span class="sxs-lookup"><span data-stu-id="6072c-274">This is due in no small part to the changes in compilation architecture.</span></span>

<span data-ttu-id="6072c-275">在 Visual Studio 2002 和 2003年中，Web 应用程序进行了编译到驻留在 /bin 文件夹中的一个主要的程序集。</span><span class="sxs-lookup"><span data-stu-id="6072c-275">In Visual Studio 2002 and 2003, Web applications were compiled into one primary assembly residing in the /bin folder.</span></span> <span data-ttu-id="6072c-276">在 Visual Studio 2005 中，已添加的应用程序/_Code 文件夹。</span><span class="sxs-lookup"><span data-stu-id="6072c-276">In Visual Studio 2005, an App/_Code folder was added.</span></span> <span data-ttu-id="6072c-277">类和其他非 UI 代码添加到应用程序/_Code 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="6072c-277">Classes and other non-UI code are added to the App/_Code folder.</span></span> <span data-ttu-id="6072c-278">Visual Studio 生成项目，应用程序/_Code 文件夹中的所有文件都编译为单个 App/_Code.dll 文件中。</span><span class="sxs-lookup"><span data-stu-id="6072c-278">When Visual Studio builds the project, all files in the App/_Code folder are compiled into a single App/_Code.dll file.</span></span> <span data-ttu-id="6072c-279">此更改的结果是，随后生成要短得比在早期版本中。</span><span class="sxs-lookup"><span data-stu-id="6072c-279">The result of this change is that subsequent builds are much faster than in previous versions.</span></span>

> [!NOTE]
> <span data-ttu-id="6072c-280">MSBuild 命令行实用工具还可用来生成 ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6072c-280">The MSBuild command line utility can also be used to build ASP.NET Web applications.</span></span> <span data-ttu-id="6072c-281">该工具将在模块 9 中介绍。</span><span class="sxs-lookup"><span data-stu-id="6072c-281">That tool will be covered in module 9.</span></span>


<span data-ttu-id="6072c-282">另一编译增强功能是在生成菜单上的新生成页选项。</span><span class="sxs-lookup"><span data-stu-id="6072c-282">Another compilation enhancement is the new Build Page option on the Build menu.</span></span> <span data-ttu-id="6072c-283">此功能允许开发人员，以便可以更快地编译更改重新生成仅在当前网页 （连同，过程中，和依赖项）。</span><span class="sxs-lookup"><span data-stu-id="6072c-283">This feature allows a developer to rebuild only the current page (along with, of course, and dependencies) so that changes can be compiled more quickly.</span></span> <span data-ttu-id="6072c-284">由于 C# 不提供的更新 IntelliSense 等目的的后台编译，它们将起到极大从此功能受益因为这可以使 intellisense 只需重新生成单个页面快速更新。</span><span class="sxs-lookup"><span data-stu-id="6072c-284">Because C# does not offer background compilation for purposes of updating IntelliSense, etc., they will benefit immensely from this feature because it will allow for IntelliSense to be updated quickly by simply rebuilding a single page.</span></span>

<span data-ttu-id="6072c-285">一个项目的生成属性，可以配置执行的启动页前发生的生成的类型。</span><span class="sxs-lookup"><span data-stu-id="6072c-285">The Build properties for a project allow you to configure the type of build that occurs before the startup page is executed.</span></span> <span data-ttu-id="6072c-286">开发人员可以选择仅生成当前页，以便 Visual Studio 可以开始在代码更改后更快地调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="6072c-286">Developers can choose to only build the current page so that Visual Studio can start debugging applications more quickly after code changes.</span></span>


![生成页开始操作](improvements-in-visual-studio-2005/_static/image6.jpg)

<span data-ttu-id="6072c-288">**图 9**： 生成页开始操作</span><span class="sxs-lookup"><span data-stu-id="6072c-288">**Figure 9**: The Build Page Start Action</span></span>


<span data-ttu-id="6072c-289">到 Visual Studio 和 ASP.NET 体系结构的另一个很好的增强功能的编辑区域中，并继续。</span><span class="sxs-lookup"><span data-stu-id="6072c-289">Another great enhancement to Visual Studio and the ASP.NET architecture is in the area of edit and continue.</span></span> <span data-ttu-id="6072c-290">在 Visual Studio 2005 中，开发人员可以开始调试项目，而无需分离调试器对项目进行代码更改。</span><span class="sxs-lookup"><span data-stu-id="6072c-290">In Visual Studio 2005, developers can start debugging a project and make code changes on the project without detaching the debugger.</span></span> <span data-ttu-id="6072c-291">事实上，你可以按原义开始调试项目、 添加新的类，将代码添加到该类、 将代码添加到你创建此类的新实例的页和执行类，所有操作都无分离调试器的方法。</span><span class="sxs-lookup"><span data-stu-id="6072c-291">In fact, you can literally start debugging a project, add a new class, add code to that class, add code to your page that creates a new instance of that class and execute a method of the class, all without detaching the debugger.</span></span> <span data-ttu-id="6072c-292">执行新的代码都按其原义易如反掌刷新浏览器 ！</span><span class="sxs-lookup"><span data-stu-id="6072c-292">Executing the new code is literally as easy as refreshing the browser!</span></span>

<span data-ttu-id="6072c-293">单击此处可查看视频演练编辑和继续在 Visual Studio 2005 中的功能。</span><span class="sxs-lookup"><span data-stu-id="6072c-293">Click here to see a video walkthrough of the edit and continue feature in Visual Studio 2005.</span></span>


![](improvements-in-visual-studio-2005/_static/image2.png)


[<span data-ttu-id="6072c-294">打开全屏幕视频</span><span class="sxs-lookup"><span data-stu-id="6072c-294">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)


<span data-ttu-id="6072c-295">可靠的编辑并继续在 ASP.NET 2.0 中的功能和 Visual Studio 2005 是由于 ASP.NET 应用程序的体系结构更改。</span><span class="sxs-lookup"><span data-stu-id="6072c-295">The robust edit and continue functionality in ASP.NET 2.0 and Visual Studio 2005 is due to an architectural change for ASP.NET applications.</span></span> <span data-ttu-id="6072c-296">在 ASP.NET 中 1.x，在 Visual Studio 2002/2003 中创建的应用程序编译到 /bin 文件夹中存储的主程序集中。</span><span class="sxs-lookup"><span data-stu-id="6072c-296">In ASP.NET 1.x, applications created in Visual Studio 2002/2003 were compiled into a primary assembly that was stored in the /bin folder.</span></span> <span data-ttu-id="6072c-297">所有类，页，等的应用程序已编译成一个 DLL。</span><span class="sxs-lookup"><span data-stu-id="6072c-297">All classes, pages, etc. for the application were compiled into that one DLL.</span></span> <span data-ttu-id="6072c-298">然后在运行时，ASP.NET 将编译的所有控件、 标记和在的页内的 ASP.NET 代码，并将这些 Dll 复制到 ASP.NET 临时文件夹。</span><span class="sxs-lookup"><span data-stu-id="6072c-298">Then at runtime, ASP.NET would compile all of the controls, markup, and ASP.NET code within pages and copy those DLLs into the ASP.NET temporary folder.</span></span>

<span data-ttu-id="6072c-299">使用 ASP.NET 2.0 中，这两个编译模型概述上面 （一个用于 Visual Studio），另一个用于 ASP.NET 在运行时的 Visual Studio 2005 中已合并到一个通用的编译模型。</span><span class="sxs-lookup"><span data-stu-id="6072c-299">In Visual Studio 2005 using ASP.NET 2.0, the two compilation models outline above (one for Visual Studio and one for ASP.NET at runtime) have been merged into one common compilation model.</span></span> <span data-ttu-id="6072c-300">这意味着，所有编译问题现在都捕获在开发阶段而不是在运行时。</span><span class="sxs-lookup"><span data-stu-id="6072c-300">That means that all compilation issues are now caught during the development stage instead of at runtime.</span></span> <span data-ttu-id="6072c-301">它还允许为设计器和功能，如用户控件和母版页的 IntelliSense 支持。</span><span class="sxs-lookup"><span data-stu-id="6072c-301">It also allows for designer and IntelliSense support for features such as user controls and master pages.</span></span>

<span data-ttu-id="6072c-302">若要查看用户控件的设计器支持的视频演练，请单击此处。</span><span class="sxs-lookup"><span data-stu-id="6072c-302">Click here to see a video walkthrough of designer support for user controls.</span></span>


![](improvements-in-visual-studio-2005/_static/image3.png)


[<span data-ttu-id="6072c-303">打开全屏幕视频</span><span class="sxs-lookup"><span data-stu-id="6072c-303">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)


> [!NOTE]
> <span data-ttu-id="6072c-304">从页面中，删除用户控件时@Register指令保留在标记中，并且应手动删除以避免分析器错误，如果从网站中删除用户控件。</span><span class="sxs-lookup"><span data-stu-id="6072c-304">When a user control is removed from a page, the @Register directive remains in the markup and should be removed manually in order to avoid parser errors if the user control is deleted from the Web site.</span></span>


<span data-ttu-id="6072c-305">Visual Studio 编译模型中的另一个改进是发布网站功能。</span><span class="sxs-lookup"><span data-stu-id="6072c-305">Another improvement in the Visual Studio compilation model is the Publish Web Site feature.</span></span> <span data-ttu-id="6072c-306">因为发布功能对预编译网站，开发人员可以享受的无需编译任何按需添加的性能。</span><span class="sxs-lookup"><span data-stu-id="6072c-306">Because the Publish feature precompiles the Web site, developers can enjoy the added performance of not having to compile anything on demand.</span></span> <span data-ttu-id="6072c-307">它还预编译的应用程序/_Code 文件夹中的所有源代码为 DLL，以便在没有源代码必须进行部署。</span><span class="sxs-lookup"><span data-stu-id="6072c-307">It also precompiles all source code in the App/_Code folder into a DLL so that no source code has to be deployed.</span></span>


![发布网站对话框](improvements-in-visual-studio-2005/_static/image7.jpg)

<span data-ttu-id="6072c-309">**图 10**： 发布 Web 站点对话框</span><span class="sxs-lookup"><span data-stu-id="6072c-309">**Figure 10**: The Publish Web Site Dialog</span></span>


> [!NOTE]
> <span data-ttu-id="6072c-310">Aspnet/_compile.exe 实用工具还可以使用预编译的 ASP.NET Web 应用。</span><span class="sxs-lookup"><span data-stu-id="6072c-310">The aspnet/_compile.exe utility can also be used to pre-compile an ASP.NET Web application.</span></span> <span data-ttu-id="6072c-311">该工具将在模块 9 中介绍。</span><span class="sxs-lookup"><span data-stu-id="6072c-311">That tool will be covered in module 9.</span></span>


<span data-ttu-id="6072c-312">当你发布网站，预编译的文件存储在临时 ASP.NET 文件的文件夹如下所示。</span><span class="sxs-lookup"><span data-stu-id="6072c-312">When you Publish a Web site, the precompiled files are stored in the Temporary ASP.NET Files folder as shown below.</span></span> <span data-ttu-id="6072c-313">文件都具有*为.compiled*文件扩展名是特定的 Dll 定义的依赖项的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="6072c-313">Files with a *.compiled* file extension are XML files that define dependencies for particular DLLs.</span></span> <span data-ttu-id="6072c-314">任何 web 窗体或用户控件被编译为开头的随机 Dll*应用 /_Web /_*。</span><span class="sxs-lookup"><span data-stu-id="6072c-314">Any Webform or user controls are compiled into random DLLs that begin with *App/_Web/_*.</span></span>

<span data-ttu-id="6072c-315">如果你离开*允许可更新此预编译的网站*选中复选框，内部 Webforms 和用户控件的标记将不会预编译为 DLL，允许你在部署后进行更改。</span><span class="sxs-lookup"><span data-stu-id="6072c-315">If you leave the *Allow this precompiled site to be updatable* checkbox checked, markup inside of your Webforms and user controls will not be pre-compiled into a DLL allowing you to make changes after deployment.</span></span> <span data-ttu-id="6072c-316">如果你想要锁定标记，以便不允许对部署的内容的更改，请取消选中此框。</span><span class="sxs-lookup"><span data-stu-id="6072c-316">If you would prefer to lock down the markup so that changes to the deployed content are not allowed, uncheck this box.</span></span>

<span data-ttu-id="6072c-317">*使用固定命名和单个页程序集*复选框，您可以禁用批处理编译，以便每个页面会编译成程序集具有固定名称。</span><span class="sxs-lookup"><span data-stu-id="6072c-317">The *Use fixed naming and single page assemblies* checkbox allows you to disable batch compilation so that each page is compiled into a fixed-named assembly.</span></span> <span data-ttu-id="6072c-318">将此框保留为未选中允许你利用批处理编译。</span><span class="sxs-lookup"><span data-stu-id="6072c-318">Leaving this box unchecked allows you to take advantage of batch compilation.</span></span>

<span data-ttu-id="6072c-319">*启用强命名在预编译的程序集*复选框可将强名称你预编译的程序集。</span><span class="sxs-lookup"><span data-stu-id="6072c-319">The *Enable strong naming on precompiled assemblies* checkbox allows you to strong-name your precompiled assemblies.</span></span>

> [!NOTE]
> <span data-ttu-id="6072c-320">在 ASP.NET 中 1.x，强名称的程序集必须安装到全局程序集缓存 (GAC) 中。</span><span class="sxs-lookup"><span data-stu-id="6072c-320">In ASP.NET 1.x, strong-named assemblies had to be installed into the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="6072c-321">在 ASP.NET 2.0 中，则不需要具有强名称程序集安装到 GAC。</span><span class="sxs-lookup"><span data-stu-id="6072c-321">In ASP.NET 2.0, you are not required to install strong-named assemblies into the GAC.</span></span>


![ASP.NET 应用程序预编译的文件](improvements-in-visual-studio-2005/_static/image8.jpg)

<span data-ttu-id="6072c-323">**图 11**: ASP.NET 应用程序预编译的文件</span><span class="sxs-lookup"><span data-stu-id="6072c-323">**Figure 11**: An ASP.NET Applications Pre-Compiled Files</span></span>


> [!NOTE]
> <span data-ttu-id="6072c-324">在上面的应用中，没有 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="6072c-324">In the application above, there was no web.config file.</span></span> <span data-ttu-id="6072c-325">如果没有过，它将调用了*PrecompiledApp.config*站点过程之后发布 Web。</span><span class="sxs-lookup"><span data-stu-id="6072c-325">If there had been, it would have been called *PrecompiledApp.config* after the Publish Web site process.</span></span>


## <a name="improvements-in-deployment"></a><span data-ttu-id="6072c-326">部署中的改进</span><span class="sxs-lookup"><span data-stu-id="6072c-326">Improvements in Deployment</span></span>

<span data-ttu-id="6072c-327">作为 Visual Studio 2002 和 2003，Visual Studio 2005 提供的复制项目功能。</span><span class="sxs-lookup"><span data-stu-id="6072c-327">As with Visual Studio 2002 and 2003, Visual Studio 2005 offers a Copy Project feature.</span></span> <span data-ttu-id="6072c-328">但是，该功能在 Visual Studio 2005 中已得到增强，并为现在称为复制网站。</span><span class="sxs-lookup"><span data-stu-id="6072c-328">However, the feature has been beefed up in Visual Studio 2005 and is now called Copy Web Site.</span></span>

<span data-ttu-id="6072c-329">复制网站对话框中被划分为左的框架和右侧的框架。</span><span class="sxs-lookup"><span data-stu-id="6072c-329">The Copy Web Site dialog is split into a left frame and a right frame.</span></span> <span data-ttu-id="6072c-330">左的框架中称为源 Web 站点，右栏中称为远程网站。</span><span class="sxs-lookup"><span data-stu-id="6072c-330">The left frame is called the Source Web Site and the right frame is called the Remote Web Site.</span></span> <span data-ttu-id="6072c-331">可能混淆一些开发人员的一点是，在右栏中显示的站点不一定是远程站点。</span><span class="sxs-lookup"><span data-stu-id="6072c-331">One thing that may confuse some developers is that the site displayed in the right frame is not necessarily a remote site.</span></span> <span data-ttu-id="6072c-332">这可能是在本地文件系统上或在 IIS 的本地实例上的站点。</span><span class="sxs-lookup"><span data-stu-id="6072c-332">It could be a site on the local file system or on the local instance of IIS.</span></span> <span data-ttu-id="6072c-333">此外，显示在左框架中的站点不一定源 Web 站点因为对话框允许你从远程网站上发布*到*源 Web 站点。</span><span class="sxs-lookup"><span data-stu-id="6072c-333">Additionally, the site displayed in the left frame is not necessarily the source Web site because the dialog allows you to publish from the remote Web site *to* the source Web site.</span></span>

<span data-ttu-id="6072c-334">如果要将项目复制到远程网站，该站点必须具有在其上安装的 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="6072c-334">If you are copying a project to a remote Web site, that site must have the FrontPage Server Extensions installed on it.</span></span> <span data-ttu-id="6072c-335">如果没有，你将需要使用 FTP 进行连接。</span><span class="sxs-lookup"><span data-stu-id="6072c-335">If it does not, you will need to connect using FTP.</span></span> <span data-ttu-id="6072c-336">另一方面，如果将项目复制到本地 IIS 实例，则不需要 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="6072c-336">On the other hand, if you are copying a project to the local IIS instance, FrontPage Server Extensions are not required.</span></span>

> [!NOTE]
> <span data-ttu-id="6072c-337">如果你尝试在本地 IIS 实例上创建新网站，且安装 FrontPage 2002 Server Extensions，你将获取错误消息，告诉你，创建网站不支持在 SharePoint 服务器上。</span><span class="sxs-lookup"><span data-stu-id="6072c-337">If you try to create a new Web site on the local IIS instance and the FrontPage 2002 Server Extensions are installed, you will get an error message telling you that creating Web sites is not supported on a SharePoint server.</span></span> <span data-ttu-id="6072c-338">在这种情况下，你可以选择安装 FrontPage 2000 服务器扩展或删除 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="6072c-338">In that case, you have the option of installing the FrontPage 2000 Server Extensions or removing the FrontPage Server Extensions.</span></span>


<span data-ttu-id="6072c-339">有关复制网站功能的视频演练，请单击此处。</span><span class="sxs-lookup"><span data-stu-id="6072c-339">Click here for a video walkthrough of the Copy Web Site feature.</span></span>


![](improvements-in-visual-studio-2005/_static/image4.png)


[<span data-ttu-id="6072c-340">打开全屏幕视频</span><span class="sxs-lookup"><span data-stu-id="6072c-340">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/copysite1.wmv)


## <a name="improvements-in-debugging"></a><span data-ttu-id="6072c-341">在调试中的改进</span><span class="sxs-lookup"><span data-stu-id="6072c-341">Improvements in Debugging</span></span>

<span data-ttu-id="6072c-342">有四个重要改进调试 Visual Studio 2005 中。</span><span class="sxs-lookup"><span data-stu-id="6072c-342">There are four key improvements in debugging in Visual Studio 2005.</span></span>

- <span data-ttu-id="6072c-343">以非管理员身份在进行本地调试有可能在初始状态。</span><span class="sxs-lookup"><span data-stu-id="6072c-343">Debugging locally as a non-administrator is possible out of the box.</span></span>
- <span data-ttu-id="6072c-344">Compilation 元素的调试属性现 false 默认情况下。</span><span class="sxs-lookup"><span data-stu-id="6072c-344">The Debug attribute for the Compilation element is now false by default.</span></span>
- <span data-ttu-id="6072c-345">远程调试设置和配置是比之前更。</span><span class="sxs-lookup"><span data-stu-id="6072c-345">Remote debugging setup and configuration is easier than before.</span></span>
- <span data-ttu-id="6072c-346">现在可以通过 FTP 位置打开的网站进行调试。</span><span class="sxs-lookup"><span data-stu-id="6072c-346">You can now debug a Web site opened via an FTP location.</span></span>

## <a name="debugging-as-a-non-administrator"></a><span data-ttu-id="6072c-347">以非管理员身份调试</span><span class="sxs-lookup"><span data-stu-id="6072c-347">Debugging as a Non-Administrator</span></span>

<span data-ttu-id="6072c-348">添加 ASP.NET 开发服务器允许非管理员可以轻松地调试现成的 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6072c-348">The addition of the ASP.NET Development Server allows non-administrators to easily debug ASP.NET applications right out of the box.</span></span> <span data-ttu-id="6072c-349">调试本地文件系统上运行的 ASP.NET 应用程序时, Visual Studio 将启动登录的用户的上下文中的 ASP.NET 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="6072c-349">When an ASP.NET application running on the local file system is debugged, Visual Studio launches the ASP.NET Development Server under the context of the logged-on user.</span></span> <span data-ttu-id="6072c-350">然后，该用户可以调试该应用程序无需任何其他配置。</span><span class="sxs-lookup"><span data-stu-id="6072c-350">That user can then debug that application without any additional configuration.</span></span>

## <a name="debug-is-false-by-default"></a><span data-ttu-id="6072c-351">调试为 False 默认情况下</span><span class="sxs-lookup"><span data-stu-id="6072c-351">Debug is False by Default</span></span>

<span data-ttu-id="6072c-352">在 ASP.NET 中 1.x*调试*属性中*编译*web.config 文件元素设置为*true*默认情况下。</span><span class="sxs-lookup"><span data-stu-id="6072c-352">In ASP.NET 1.x, the *debug* attribute in the *compilation* element of the web.config file was set to *true* by default.</span></span> <span data-ttu-id="6072c-353">始终具有已以下建议开发人员将此属性设置为*false*之前应用程序部署到生产环境，但是，由于大多数开发人员完全不了解将调试属性设置为保留的后果为 true，它们只需从左其作为-是。</span><span class="sxs-lookup"><span data-stu-id="6072c-353">It has always been recommended that developers set this attribute to *false* before deploying an application to production, but because most developers don't fully understand the consequences of leaving the debug attribute set to true, they simply left it as-is.</span></span>

<span data-ttu-id="6072c-354">最严重的问题与具有调试属性设置为 true 是，它会禁用 ASP.NETs 批处理编译模型。</span><span class="sxs-lookup"><span data-stu-id="6072c-354">The most severe problem with having the debug attribute set to true is that it disables ASP.NETs batch compilation model.</span></span> <span data-ttu-id="6072c-355">因此，每个页面会编译成单独的 DLL。</span><span class="sxs-lookup"><span data-stu-id="6072c-355">Therefore, each page is compiled into a separate DLL.</span></span> <span data-ttu-id="6072c-356">如果 Web 应用程序包含数千个页面 （不前所未有的通过任何方式），它表示该应用程序将创建若干个千位小 Dll。</span><span class="sxs-lookup"><span data-stu-id="6072c-356">If a Web application consists of thousands of pages (not unheard of by any means), that means several thousand small DLLs will be created by that application.</span></span> <span data-ttu-id="6072c-357">虽然这些 Dll 很小，它们不是加载到内存中的任何特定位置。</span><span class="sxs-lookup"><span data-stu-id="6072c-357">While these DLLs are small in size, they are not loaded into any particular location in memory.</span></span> <span data-ttu-id="6072c-358">因此，它们在系统内存中导致碎片，并且可参与 OutOfMemoryException 匹配项。</span><span class="sxs-lookup"><span data-stu-id="6072c-358">Therefore, they cause fragmentation in system memory and can contribute to OutOfMemoryException occurrences.</span></span>

<span data-ttu-id="6072c-359">在 ASP.NET 2.0 中，默认情况下调试属性设置为 false。</span><span class="sxs-lookup"><span data-stu-id="6072c-359">In ASP.NET 2.0, the debug attribute is set to false by default.</span></span> <span data-ttu-id="6072c-360">如你已经看到，当开发人员调试 ASP.NET 应用程序在 Visual Studio 2005 中，系统会提示他们添加启用了调试的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="6072c-360">As you have already seen, when a developer debugs an ASP.NET application in Visual Studio 2005, they are prompted to add a web.config file with debugging enabled.</span></span> <span data-ttu-id="6072c-361">这样做会导致在 ASP.NET 中存在的相同缺点 1.x，但现在开发人员清楚地发出警告，该属性应重置为 false 然后再移动到生产应用程序。</span><span class="sxs-lookup"><span data-stu-id="6072c-361">Doing so incurs the same drawbacks that were present in ASP.NET 1.x, but now the developer is clearly warned that the attribute should be reset to false before moving the application to production.</span></span>

## <a name="remote-debugging-setup-and-configuration"></a><span data-ttu-id="6072c-362">远程调试设置和配置</span><span class="sxs-lookup"><span data-stu-id="6072c-362">Remote Debugging Setup and Configuration</span></span>

<span data-ttu-id="6072c-363">在 Visual Studio 2002/2003 中，远程调试依赖于计算机调试管理器 (mdm.exe) 和 vs7jit.exe 过程。</span><span class="sxs-lookup"><span data-stu-id="6072c-363">In Visual Studio 2002/2003, remote debugging relied on the Machine Debug Manager (mdm.exe) and the vs7jit.exe process.</span></span> <span data-ttu-id="6072c-364">正因如此，解决远程调试的问题通常是客户黑色框和它通常不是更好的产品支持部门联系。</span><span class="sxs-lookup"><span data-stu-id="6072c-364">Because of that, troubleshooting remote debugging problems was often a black box for customers and it was often not much better for PSS.</span></span>

<span data-ttu-id="6072c-365">Visual Studio 2005 中移除而言，依赖于在 mdm.exe 和 vs7jit.exe 过程。</span><span class="sxs-lookup"><span data-stu-id="6072c-365">Visual Studio 2005 removes the reliance on the mdm.exe and vs7jit.exe processes.</span></span> <span data-ttu-id="6072c-366">相反，它现在使用远程调试监视器服务 (msvsmon.exe)。</span><span class="sxs-lookup"><span data-stu-id="6072c-366">Instead, it now uses the Remote Debug Monitor service (msvsmon.exe.)</span></span>

<span data-ttu-id="6072c-367">远程调试 Visual Studio 2005 中的要求是非常简单。</span><span class="sxs-lookup"><span data-stu-id="6072c-367">The requirement for debugging in Visual Studio 2005 remotely is quite simple.</span></span> <span data-ttu-id="6072c-368">你需要在调试之前在远程服务器上运行 msvsmon.exe。</span><span class="sxs-lookup"><span data-stu-id="6072c-368">You need to run msvsmon.exe on the remote server prior to debugging.</span></span> <span data-ttu-id="6072c-369">你可以从 Visual Studio CD 安装远程调试监视器或只需运行 msvsmon.exe 从共享不会在所有 Web 服务器上安装任何内容。</span><span class="sxs-lookup"><span data-stu-id="6072c-369">You can install the Remote Debug Monitor from the Visual Studio CD or you can simply run msvsmon.exe from a share without installing anything at all on the Web server.</span></span>

<span data-ttu-id="6072c-370">当你运行 msvsmon.exe 时，则很可能将抱怨有关端口被阻止进行远程调试。</span><span class="sxs-lookup"><span data-stu-id="6072c-370">When you run msvsmon.exe, it is likely that it will complain about ports being blocked for remote debugging.</span></span> <span data-ttu-id="6072c-371">幸运的是，你可以轻松地取消阻止端口，从警告对话框中的权限如下所示。</span><span class="sxs-lookup"><span data-stu-id="6072c-371">Fortunately, you can easily unblock the ports from right within the warning dialog as shown below.</span></span>


![Windows 防火墙处于阻止远程调试的通知](improvements-in-visual-studio-2005/_static/image9.jpg)

<span data-ttu-id="6072c-373">**图 12**： 通知 Windows 防火墙，则阻止远程调试</span><span class="sxs-lookup"><span data-stu-id="6072c-373">**Figure 12**: Notification that Windows Firewall is Blocking Remote Debugging</span></span>


<span data-ttu-id="6072c-374">你已取消阻止后调试所需的端口，你将看到远程调试监视器，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6072c-374">Once you have unblocked the ports necessary for debugging, you will see the Remote Debugging Monitor as shown below.</span></span> <span data-ttu-id="6072c-375">此接口，从你可以监视连接并更改轻松地调试权限。</span><span class="sxs-lookup"><span data-stu-id="6072c-375">From this interface, you can monitor connections and change debugging permissions easily.</span></span>


![远程调试监视器](improvements-in-visual-studio-2005/_static/image10.jpg)

<span data-ttu-id="6072c-377">**图 13**： 远程调试监视器</span><span class="sxs-lookup"><span data-stu-id="6072c-377">**Figure 13**: The Remote Debugging Monitor</span></span>


<span data-ttu-id="6072c-378">还有可能远程调试 Web 应用程序通过 FTP 打开。</span><span class="sxs-lookup"><span data-stu-id="6072c-378">It is also possible to remotely debug a Web application opened via FTP.</span></span> <span data-ttu-id="6072c-379">步骤是方式与之前介绍的相同。</span><span class="sxs-lookup"><span data-stu-id="6072c-379">The steps are the same as those previously covered.</span></span> <span data-ttu-id="6072c-380">但是，你将需要指定用于浏览 FTP 项目此模块中前面所述的基 URL。</span><span class="sxs-lookup"><span data-stu-id="6072c-380">However, you will need to specify a base URL for browsing the FTP project as outlined earlier in this module.</span></span>

## <a name="lab-2"></a><span data-ttu-id="6072c-381">Lab 2</span><span class="sxs-lookup"><span data-stu-id="6072c-381">Lab 2</span></span>

## <a name="remote-debugging-with-visual-studio-2005"></a><span data-ttu-id="6072c-382">使用 Visual Studio 2005 的远程调试</span><span class="sxs-lookup"><span data-stu-id="6072c-382">Remote Debugging with Visual Studio 2005</span></span>

<span data-ttu-id="6072c-383">此实验室将引导你完成使用 Visual Studio 2005 的远程调试。</span><span class="sxs-lookup"><span data-stu-id="6072c-383">This lab will walk you through remote debugging with Visual Studio 2005.</span></span>

<span data-ttu-id="6072c-384">有关本实验的视频演练，请单击此处。</span><span class="sxs-lookup"><span data-stu-id="6072c-384">Click here for a video walkthrough of this lab.</span></span>


![](improvements-in-visual-studio-2005/_static/image5.png)


[<span data-ttu-id="6072c-385">打开全屏幕视频</span><span class="sxs-lookup"><span data-stu-id="6072c-385">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/remdebug1.wmv)


<span data-ttu-id="6072c-386">此实验室要求你拥有两台计算机，一个正在运行的 Visual Studio 2005 和其他正在运行 IIS 5 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="6072c-386">This lab requires you to have two machines, one running Visual Studio 2005 and the other running IIS 5 or greater.</span></span>

1. <span data-ttu-id="6072c-387">打开 Visual Studio 2005 并在远程服务器上创建新网站。</span><span class="sxs-lookup"><span data-stu-id="6072c-387">Open Visual Studio 2005 and create a new Web site on the remote server.</span></span>

> [!NOTE]
> <span data-ttu-id="6072c-388">远程 IIS 实例上或通过 FTP，可以创建网站。</span><span class="sxs-lookup"><span data-stu-id="6072c-388">You can create the Web site on a remote IIS instance or via FTP.</span></span>


1. <span data-ttu-id="6072c-389">在远程 Web 服务器上，使用 UNC 路径的开发计算机上找到 msvsmon.exe 并执行它。</span><span class="sxs-lookup"><span data-stu-id="6072c-389">From the remote Web server, locate msvsmon.exe on the development machine using a UNC path and execute it.</span></span>  
 <span data-ttu-id="6072c-390">Msvsmon.exe 的默认位置是 //server/c$/Program 文件/Microsoft Visual Studio 8/Common7/IDE/远程调试器/x86。</span><span class="sxs-lookup"><span data-stu-id="6072c-390">The default location for msvsmon.exe is //server/c$/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.</span></span>
2. <span data-ttu-id="6072c-391">如果系统提示您取消阻止端口进行远程调试，这样做。</span><span class="sxs-lookup"><span data-stu-id="6072c-391">If prompted to unblock ports for remote debugging, do so.</span></span>
3. <span data-ttu-id="6072c-392">从开发计算机上，打开 Default.aspx 代码隐藏和页/（_l） 方法中设置断点。</span><span class="sxs-lookup"><span data-stu-id="6072c-392">From the development machine, open the code-behind for Default.aspx and set a breakpoint in the Page/_Load method.</span></span>
4. <span data-ttu-id="6072c-393">从开发计算机开始调试。</span><span class="sxs-lookup"><span data-stu-id="6072c-393">Start debugging from the development machine.</span></span>

<span data-ttu-id="6072c-394">你应按预期方式命中该断点。</span><span class="sxs-lookup"><span data-stu-id="6072c-394">You should hit the breakpoint as expected.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="6072c-395">ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="6072c-395">ASP.NET Development Server</span></span>

<span data-ttu-id="6072c-396">如我们前面已经讨论过，Visual Studio 2005 附带称为 ASP.NET 开发服务器的 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="6072c-396">As weve already discussed, Visual Studio 2005 ships with a Web server called the ASP.NET Development Server.</span></span> <span data-ttu-id="6072c-397">（ASP.NET 开发服务器有时称为 Cassini。）此 Web 服务器是一种方便的方式浏览和调试 Web 应用程序在文件系统上运行。</span><span class="sxs-lookup"><span data-stu-id="6072c-397">(The ASP.NET Development Server is sometimes referred to as Cassini.) This Web server is a convenient means to browse and debug Web applications running on the file system.</span></span>

<span data-ttu-id="6072c-398">ASP.NET 开发服务器是受限制的 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="6072c-398">The ASP.NET Development Server is a restricted Web server.</span></span> <span data-ttu-id="6072c-399">它不允许远程连接，因此它不允许任何请求启动 Web 服务器的用户以外的任何用户。</span><span class="sxs-lookup"><span data-stu-id="6072c-399">It does not allow remote connections, it does not allow any requests from any user other than the user who started the Web server.</span></span> <span data-ttu-id="6072c-400">它还没有为 ASP 页面提供服务的功能。</span><span class="sxs-lookup"><span data-stu-id="6072c-400">It also does not have the capability of serving ASP pages.</span></span> <span data-ttu-id="6072c-401">仅 ASP.NET 资源和 HTML 资源 （包括图像、 CSS 文件等） 进行处理。</span><span class="sxs-lookup"><span data-stu-id="6072c-401">Only ASP.NET resources and HTML resources (including images, CSS files, etc.) are served.</span></span>

<span data-ttu-id="6072c-402">可以通过运行位于 c:/Windows/Microsoft.NET/Framework/v2.0./ WebDev.WebServer.exe 文件通过命令行启动 ASP.NET Development Server*/* /  */*/\*.</span><span class="sxs-lookup"><span data-stu-id="6072c-402">The ASP.NET Development Server can be launched via the command line by running the WebDev.WebServer.exe file located at c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/\*.</span></span> <span data-ttu-id="6072c-403">以下对话框显示可用的参数。</span><span class="sxs-lookup"><span data-stu-id="6072c-403">The following dialog displays the parameters that are available.</span></span>


![](improvements-in-visual-studio-2005/_static/image11.jpg)

<span data-ttu-id="6072c-404">**图 14**</span><span class="sxs-lookup"><span data-stu-id="6072c-404">**Figure 14**</span></span>


> [!NOTE]
> <span data-ttu-id="6072c-405">ASP.NET Development Server 不支持通过命令行显式启动时。</span><span class="sxs-lookup"><span data-stu-id="6072c-405">The ASP.NET Development Server is not supported when launched explicitly via the command line.</span></span>
