---
uid: whitepapers/denied-access-to-iis-directories
title: ASP.NET 拒绝了对 IIS 目录的访问 |Microsoft 文档
author: rick-anderson
description: 该白皮书介绍了你必须执行的操作如果对 ASP.NET 应用程序的请求将返回错误，"拒绝访问 DirectoryName 目录。 未能 s...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: d95423776a6b58fc67ae6c791685543dadd2480c
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
<a name="aspnet-denied-access-to-iis-directories"></a><span data-ttu-id="88e35-104">ASP.NET 拒绝了对 IIS 目录的访问</span><span class="sxs-lookup"><span data-stu-id="88e35-104">ASP.NET Denied Access to IIS Directories</span></span>
====================
> <span data-ttu-id="88e35-105">该白皮书介绍了如果向 ASP.NET 应用程序发出的请求将返回错误，必须执行"拒绝访问*DirectoryName*目录。</span><span class="sxs-lookup"><span data-stu-id="88e35-105">This whitepaper describes what you must do if a request to your ASP.NET application returns the error, "Denied Access to *DirectoryName* directory.</span></span> <span data-ttu-id="88e35-106">无法开始监视的目录更改。"</span><span class="sxs-lookup"><span data-stu-id="88e35-106">Failed to start monitoring directory changes."</span></span>
> 
> <span data-ttu-id="88e35-107">适用于 ASP.NET 1.0 和 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="88e35-107">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>


<span data-ttu-id="88e35-108">ASP.NET V1 RTM 现在运行在使用较低特权 windows 帐户的注册为本地计算机上的"ASPNET"帐户。</span><span class="sxs-lookup"><span data-stu-id="88e35-108">ASP.NET V1 RTM now runs using a less privileged windows account - registered as the "ASPNET" account on a local machine.</span></span>

<span data-ttu-id="88e35-109">在某些情况下系统锁定状态，此帐户可能不是由默认具有读取安全访问的网站内容目录、 应用程序根目录中或网站根目录。</span><span class="sxs-lookup"><span data-stu-id="88e35-109">On some locked down systems, this account may not by default have read security access to a website's content directories, the application root directory, or the web site root directory.</span></span> <span data-ttu-id="88e35-110">在这种情况下从给定的 web 应用程序请求页时将收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="88e35-110">In this case you will receive the following error when requesting pages from a given web application:</span></span>

![](denied-access-to-iis-directories/_static/image1.jpg)

<span data-ttu-id="88e35-111">若要解决此问题将需要更改相应目录的安全权限。</span><span class="sxs-lookup"><span data-stu-id="88e35-111">To fix this you will need to change the security permissions on the appropriate directories.</span></span>

<span data-ttu-id="88e35-112">具体而言，ASP.NET 需要读取、 执行和列出网站根 ASPNET 帐户访问权限 (例如： c:\inetpub\wwwroot 或可能已在 IIS 中配置的任何备用站点目录)，内容的目录和应用程序根目录下若要监视的配置文件更改。</span><span class="sxs-lookup"><span data-stu-id="88e35-112">Specifically, ASP.NET requires read, execute, and list access for the ASPNET account for the web site root (for example: c:\inetpub\wwwroot or any alternative site directory you may have configured in IIS), the content directory and the application root directory in order to monitor for configuration file changes.</span></span> <span data-ttu-id="88e35-113">与 IIS 管理工具 （inetmgr） 访问） 中的应用程序虚拟目录关联的文件夹路径相对应的应用程序根目录。</span><span class="sxs-lookup"><span data-stu-id="88e35-113">The application root corresponds to the folder path associated with the application virtual directory in the IIS Administration tool (inetmgr).</span></span>

<span data-ttu-id="88e35-114">例如，考虑下的 wwwroot 文件夹的以下应用程序层次结构。</span><span class="sxs-lookup"><span data-stu-id="88e35-114">For example, consider the following application hierarchy under the wwwroot folder.</span></span>

`C:\inetpub\wwwroot\myapp\default.aspx`

<span data-ttu-id="88e35-115">对于此示例中，ASPNET 帐户需要为 myapp 和的 wwwroot 目录中的内容定义的以上的读取的权限。</span><span class="sxs-lookup"><span data-stu-id="88e35-115">For this example, the ASPNET account needs the read permissions defined above for content in both the myapp and the wwwroot directory.</span></span> <span data-ttu-id="88e35-116">在根文件夹上的单一继承的 ACL 可以 （可选） 如果也使用为这两个目录，则它们在嵌套。</span><span class="sxs-lookup"><span data-stu-id="88e35-116">A single inherited ACL on the root folder can also be optionally used for both directories if they're nested.</span></span>

<span data-ttu-id="88e35-117">若要添加到目录的权限，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="88e35-117">To add permissions to a directory, perform the following steps:</span></span>

- <span data-ttu-id="88e35-118">使用 Windows 资源管理器，导航到目录</span><span class="sxs-lookup"><span data-stu-id="88e35-118">Using the Windows explorer, navigate to the directory</span></span>
- <span data-ttu-id="88e35-119">右键单击相应的目录文件夹，然后选择"属性"</span><span class="sxs-lookup"><span data-stu-id="88e35-119">Right click on the directory folder and choose "Properties"</span></span>
- <span data-ttu-id="88e35-120">导航到属性对话框的"安全"选项卡</span><span class="sxs-lookup"><span data-stu-id="88e35-120">Navigate to the "Security" tab on the property dialog</span></span>
- <span data-ttu-id="88e35-121">单击"添加"按钮并输入计算机名称后跟 ASPNET 帐户名称。</span><span class="sxs-lookup"><span data-stu-id="88e35-121">Click the "Add" button and enter the machine name followed by the ASPNET account name.</span></span> <span data-ttu-id="88e35-122">例如，在计算机上名为"webdev"，将输入 webdev\ASPNET 并按"确定"。</span><span class="sxs-lookup"><span data-stu-id="88e35-122">For example, on a machine named "webdev", you would enter webdev\ASPNET and hit "OK".</span></span>
- <span data-ttu-id="88e35-123">确保 ASPNET 帐户具有"读取&amp;执行"，"列出文件夹内容"，并选中"读取"复选框。</span><span class="sxs-lookup"><span data-stu-id="88e35-123">Ensure that the ASPNET account has the "Read &amp; Execute", "List Folder Contents", and "Read" checkboxes checked.</span></span>
- <span data-ttu-id="88e35-124">点击确定以关闭对话框并保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="88e35-124">Hit OK to dismiss the dialog and save the changes.</span></span>

![](denied-access-to-iis-directories/_static/image2.jpg)

<span data-ttu-id="88e35-125">如果需要，可以将脚本或附带的"cacls.exe"工具用于 Windows 自动这些更改。</span><span class="sxs-lookup"><span data-stu-id="88e35-125">If desired, these changes can be automated using scripts or the "cacls.exe" tool that ships with Windows.</span></span> <span data-ttu-id="88e35-126">有关 ASPNET 帐户的详细信息，请参阅[常见问题文档](https://go.microsoft.com/fwlink/?LinkId=5828)。</span><span class="sxs-lookup"><span data-stu-id="88e35-126">For more information on the ASPNET account, please see the [FAQ document](https://go.microsoft.com/fwlink/?LinkId=5828).</span></span>

<span data-ttu-id="88e35-127">如果给定的 web 应用程序依赖于具有写入或修改到特定文件夹或文件的权限，这可以通过在相同的过程并检查"写入"和/或"修改"复选框来授予。</span><span class="sxs-lookup"><span data-stu-id="88e35-127">If a given web application relies on having write or modify permissions to a particular folder or file, this can be granted by following the same procedure and checking the "Write" and/or "Modify" checkboxes.</span></span>

<span data-ttu-id="88e35-128">在计算机上，允许每个人或用户组，对这些目录 （这是默认配置） 读取访问，将会遇到任何问题，不需要上述步骤。</span><span class="sxs-lookup"><span data-stu-id="88e35-128">On machines that allow Everyone or the Users group read access to these directories (which is the default configuration), no issues will be encountered and the above steps will not be required.</span></span>
