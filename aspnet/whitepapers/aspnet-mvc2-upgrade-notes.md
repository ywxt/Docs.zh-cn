---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: 升级到 ASP.NET MVC 2 的 ASP.NET MVC 1.0 应用程序 |Microsoft Docs
author: rick-anderson
description: 本文档描述了如何将手动和一个向导升级到 ASP.NET MVC 2 的 ASP.NET MVC 1.0 应用程序。 本文档中也有 d...
ms.author: aspnetcontent
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: fe1696cd8f98f2ff253d385b62a6bcd74b536d33
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823866"
---
<a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a><span data-ttu-id="5e425-104">升级到 ASP.NET MVC 2 的 ASP.NET MVC 1.0 应用程序</span><span class="sxs-lookup"><span data-stu-id="5e425-104">Upgrading an ASP.NET MVC 1.0 Application to ASP.NET MVC 2</span></span>
====================
> <span data-ttu-id="5e425-105">本文档描述了如何将手动和一个向导升级到 ASP.NET MVC 2 的 ASP.NET MVC 1.0 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5e425-105">This document describes both how to upgrade manually and with a wizard an ASP.NET MVC 1.0 Application to ASP.NET MVC 2.</span></span> <span data-ttu-id="5e425-106">本文档也是可用于[下载](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)</span><span class="sxs-lookup"><span data-stu-id="5e425-106">This document is also available for [Download](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)</span></span>


## <a name="introduction"></a><span data-ttu-id="5e425-107">介绍</span><span class="sxs-lookup"><span data-stu-id="5e425-107">Introduction</span></span>

<span data-ttu-id="5e425-108">ASP.NET MVC 2 可以在同一台服务器上的与 ASP.NET MVC 1.0 并行安装。</span><span class="sxs-lookup"><span data-stu-id="5e425-108">ASP.NET MVC 2 can be installed side by side with ASP.NET MVC 1.0 on the same server.</span></span> <span data-ttu-id="5e425-109">这样，应用程序开发人员灵活地选择何时将升级到 ASP.NET MVC 2 的 ASP.NET MVC 1.0 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5e425-109">This gives application developers flexibility in choosing when to upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2.</span></span>

<span data-ttu-id="5e425-110">Visual Studio 2010 包括一个向导使用 ASP.NET MVC 2 的 Visual Studio 2008 构建 ASP.NET MVC 1.0 中的现有项目的升级。</span><span class="sxs-lookup"><span data-stu-id="5e425-110">Visual Studio 2010 includes a wizard that upgrades existing ASP.NET MVC 1.0 projects built with Visual Studio 2008 to ASP.NET MVC 2.</span></span> <span data-ttu-id="5e425-111">在 Visual Studio 2010 中打开 ASP.NET MVC 1.0 项目启动升级向导。</span><span class="sxs-lookup"><span data-stu-id="5e425-111">The upgrade wizard is initiated by opening an ASP.NET MVC 1.0 project in Visual Studio 2010.</span></span>

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a><span data-ttu-id="5e425-112">面向 Visual Studio 2008 SP1 上的 ASP.NET MVC 1.0 升级向导</span><span class="sxs-lookup"><span data-stu-id="5e425-112">Upgrade Wizard for ASP.NET MVC 1.0 on Visual Studio 2008 SP1</span></span>

<span data-ttu-id="5e425-113">若要升级到 Visual Studio 2008 SP1 中的 ASP.NET MVC 2 的 ASP.NET MVC 1.0 应用程序，使用 （不受支持） MvcAppConverter 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5e425-113">To upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2 in Visual Studio 2008 SP1, use the (unsupported) MvcAppConverter application.</span></span> <span data-ttu-id="5e425-114">您可以从以下 URL 下载此应用程序：</span><span class="sxs-lookup"><span data-stu-id="5e425-114">You can download this application from the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a><span data-ttu-id="5e425-115">将 ASP.NET MVC 1.0 项目手动升级</span><span class="sxs-lookup"><span data-stu-id="5e425-115">Manually Upgrading an ASP.NET MVC 1.0 Project</span></span>

<span data-ttu-id="5e425-116">若要手动升级到版本 2 现有的 ASP.NET MVC 1.0 应用程序，请按照下列步骤：</span><span class="sxs-lookup"><span data-stu-id="5e425-116">To manually upgrade an existing ASP.NET MVC 1.0 application to version 2, follow these steps:</span></span>

1. <span data-ttu-id="5e425-117">进行备份的现有项目。</span><span class="sxs-lookup"><span data-stu-id="5e425-117">Make a backup of the existing project.</span></span>
2. <span data-ttu-id="5e425-118">在文本编辑器中，打开项目文件 （.csproj 或.vbproj 文件扩展名的文件） 并查找 ProjectTypeGuid 元素。</span><span class="sxs-lookup"><span data-stu-id="5e425-118">In a text editor, open the project file (the file with the .csproj or .vbproj file extension) and find the ProjectTypeGuid element.</span></span> <span data-ttu-id="5e425-119">作为该元素的值，将为 GUID {603c0e0b-db56-11dc-be95-000d561079b0} 与 {F85E285D-A4E0-4152-9332-AB1D724D3325}。</span><span class="sxs-lookup"><span data-stu-id="5e425-119">As the value of that element, replace the GUID {603c0e0b-db56-11dc-be95-000d561079b0} with {F85E285D-A4E0-4152-9332-AB1D724D3325}.</span></span> <span data-ttu-id="5e425-120">完成后，该元素的值应如下所示：</span><span class="sxs-lookup"><span data-stu-id="5e425-120">When you are done, the value of that element should be as follows:</span></span> 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. <span data-ttu-id="5e425-121">在 Web 应用程序根文件夹中，编辑 Web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="5e425-121">In the Web application root folder, edit the Web.config file.</span></span> <span data-ttu-id="5e425-122">搜索 System.Web.Mvc，版本 = 1.0.0.0 和所有实例都替换为 System.Web.Mvc，版本 = 2.0.0.0。</span><span class="sxs-lookup"><span data-stu-id="5e425-122">Search for System.Web.Mvc, Version=1.0.0.0 and replace all instances with System.Web.Mvc, Version=2.0.0.0.</span></span>
4. <span data-ttu-id="5e425-123">对于位于 Views 文件夹中的 Web.config 文件重复上述步骤。</span><span class="sxs-lookup"><span data-stu-id="5e425-123">Repeat the previous step for the Web.config file located in the Views folder.</span></span>
5. <span data-ttu-id="5e425-124">打开该项目使用 Visual Studio 中，然后在**解决方案资源管理器**，展开**引用**节点。</span><span class="sxs-lookup"><span data-stu-id="5e425-124">Open the project using Visual Studio, and in **Solution Explorer**, expand the **References** node.</span></span> <span data-ttu-id="5e425-125">删除对 System.Web.Mvc （其指向 1.0 版程序集） 的引用。</span><span class="sxs-lookup"><span data-stu-id="5e425-125">Delete the reference to System.Web.Mvc (which points to the version 1.0 assembly).</span></span> <span data-ttu-id="5e425-126">添加对 System.Web.Mvc (v2.0.0.0) 的引用。</span><span class="sxs-lookup"><span data-stu-id="5e425-126">Add a reference to System.Web.Mvc (v2.0.0.0).</span></span>
6. <span data-ttu-id="5e425-127">将下面的 bindingRedirect 元素添加到 Web.config 文件中的配置部分下的应用程序根目录：</span><span class="sxs-lookup"><span data-stu-id="5e425-127">Add the following bindingRedirect element to the Web.config file in the application root under the configuraton section:</span></span>   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. <span data-ttu-id="5e425-128">创建新的空 ASP.NET MVC 2 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5e425-128">Create a new empty ASP.NET MVC 2 application.</span></span> <span data-ttu-id="5e425-129">从新的 Scripts 文件夹的应用程序的现有应用程序的 Scripts 文件夹中复制的文件。</span><span class="sxs-lookup"><span data-stu-id="5e425-129">Copy the files from the Scripts folder of the new application into the Scripts folder of the existing application.</span></span>
8. <span data-ttu-id="5e425-130">更新现有的应用-™ s Site.css 文件中的 CSS 样式定义的 CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="5e425-130">Update the existing applicationâ€™s CSS file with the CSS style definitions in the Site.css file.</span></span>
9. <span data-ttu-id="5e425-131">编译该应用程序并运行它。</span><span class="sxs-lookup"><span data-stu-id="5e425-131">Compile the application and run it.</span></span> <span data-ttu-id="5e425-132">如果出现任何错误，请参阅的重大更改的部分[What's New in ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038)页。</span><span class="sxs-lookup"><span data-stu-id="5e425-132">If any errors occur, refer to the Breaking Changes section of the [What's New in ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) page.</span></span>
