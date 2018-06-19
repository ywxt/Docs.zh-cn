---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: 了解 ASP.NET AJAX 本地化 |Microsoft 文档
author: scottcate
description: 本地化是设计并将对特定的语言和区域性的支持集成到应用程序或应用程序组件的过程。 Mic...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/14/2008
ms.topic: article
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: 565b0294f57b784bc592b286b3d8b28504110415
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
ms.locfileid: "30888034"
---
<a name="understanding-aspnet-ajax-localization"></a><span data-ttu-id="d4ad3-104">了解 ASP.NET AJAX 本地化</span><span class="sxs-lookup"><span data-stu-id="d4ad3-104">Understanding ASP.NET AJAX Localization</span></span>
====================
<span data-ttu-id="d4ad3-105">通过[Scott 类别](https://github.com/scottcate)</span><span class="sxs-lookup"><span data-stu-id="d4ad3-105">by [Scott Cate](https://github.com/scottcate)</span></span>

[<span data-ttu-id="d4ad3-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="d4ad3-106">Download PDF</span></span>](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> <span data-ttu-id="d4ad3-107">本地化是设计并将对特定的语言和区域性的支持集成到应用程序或应用程序组件的过程。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-107">Localization is the process of designing and integrating support for a specific language and culture into an application or an application component.</span></span> <span data-ttu-id="d4ad3-108">Microsoft ASP.NET 平台提供广泛支持用于本地化为标准的 ASP.NET 应用程序通过集成标准.NET 本地化模型;Microsoft AJAX Framework 利用集成的模型，以支持将在其中执行本地化的各种方案。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-108">The Microsoft ASP.NET platform provides extensive support for localization for standard ASP.NET applications by integrating the standard .NET localization model; the Microsoft AJAX Framework utilize the integrated model to support the diverse scenarios in which localization can be performed.</span></span>


## <a name="introduction"></a><span data-ttu-id="d4ad3-109">介绍</span><span class="sxs-lookup"><span data-stu-id="d4ad3-109">Introduction</span></span>

<span data-ttu-id="d4ad3-110">Microsoft ASP.NET 技术将的面向对象及事件驱动的编程模型，并将它具有已编译代码的好处结合在一起。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-110">Microsoft's ASP.NET technology brings an object-oriented and event-driven programming model and unites it with the benefits of compiled code.</span></span> <span data-ttu-id="d4ad3-111">但是，其服务器端处理模型具有很多这样的可以通过封装.NET Framework 中的 Microsoft AJAX 服务的 system.web.extensions 的引用命名空间中包括的新功能进行寻址的技术中的固有的几个缺点3.5。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-111">However, its server-side processing model has several drawbacks inherent in the technology, many of which can be addressed by the new features included in the System.Web.Extensions namespace, which encapsulates the Microsoft AJAX Services in the .NET Framework 3.5.</span></span> <span data-ttu-id="d4ad3-112">这些扩展使许多丰富的客户端功能，以前可为属于 ASP.NET 2.0 AJAX Extensions 中，但现在的 Framework 基类库的一部分。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-112">These extensions enable many rich client features, previously available as part of the ASP.NET 2.0 AJAX Extensions, but now part of the Framework Base Class Library.</span></span> <span data-ttu-id="d4ad3-113">控件和此命名空间中的功能而无需完整的页面刷新，能够访问 Web 服务通过客户端 （包括 ASP.NET 分析 API） 脚本，包括部分呈现页上，提供广泛的客户端 API 用于镜像的许多ASP.NET 服务器端控件集中所示控制方案。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-113">Controls and features in this namespace include partial rendering of pages without requiring a full page refresh, the ability to access Web Services via client script (including the ASP.NET profiling API), and an extensive client-side API designed to mirror many of the control schemes seen in the ASP.NET server-side control set.</span></span>

<span data-ttu-id="d4ad3-114">本白皮书检查中的 Microsoft AJAX Framework 和 Microsoft AJAX 脚本库，本地化支持并检查已集成支持 web 的本地化的业务需求的上下文中提供的本地化功能提供的.NET Framework 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-114">This whitepaper examines the localization features present in the Microsoft AJAX Framework and Microsoft AJAX Script Library, in the context of business need for localization support and reviewing already-integrated support for localization in web applications provided by the .NET Framework.</span></span> <span data-ttu-id="d4ad3-115">Microsoft AJAX 脚本库利用.resx 文件格式已由.NET 应用程序，它提供集成的 IDE 支持和可共享的资源类型。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-115">The Microsoft AJAX Script Library utilizes the .resx file format already used by .NET applications, which provides integrated IDE support and a shareable resource type.</span></span>

<span data-ttu-id="d4ad3-116">基于本白皮书在 Microsoft Visual Studio 2008 Beta 2 版本上。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-116">This whitepaper is based on the Beta 2 release of Microsoft Visual Studio 2008.</span></span> <span data-ttu-id="d4ad3-117">此白皮书还假定你将使用 Visual Studio 2008 中，不 Visual Web Developer Express，并且将提供根据 Visual Studio 的用户界面的演练。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-117">This whitepaper also assumes that you will be working with Visual Studio 2008, not Visual Web Developer Express, and will provide walkthroughs according to the user interface of Visual Studio.</span></span> <span data-ttu-id="d4ad3-118">一些代码示例将利用可能 Visual Web Developer 学习版中不可用的项目模板。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-118">Some code samples will utilize project templates that may be unavailable in Visual Web Developer Express.</span></span>

## <a name="the-need-for-localization"></a><span data-ttu-id="d4ad3-119">*对本地化的需求*</span><span class="sxs-lookup"><span data-stu-id="d4ad3-119">*The Need for Localization*</span></span>

<span data-ttu-id="d4ad3-120">特别是对于企业应用程序开发人员，组件开发人员能够创建可以识别区域文化和语言之间的差异的工具已变得越来越必要。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-120">Particularly for enterprise application developers and component developers, the ability to create tools that can be aware of the differences between cultures and languages has become increasingly necessary.</span></span> <span data-ttu-id="d4ad3-121">设计组件能够适应客户端的区域设置提高开发人员工作效率，缩短全局函数的一个组件适应所需的工作量。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-121">Designing components with the ability to adapt to the locale of the client increases developer productivity and reduces the amount of work required for the adaptation of a component to function globally.</span></span>

<span data-ttu-id="d4ad3-122">本地化是设计并将对特定的语言和区域性的支持集成到应用程序或应用程序组件的过程。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-122">Localization is the process of designing and integrating support for a specific language and culture into an application or an application component.</span></span> <span data-ttu-id="d4ad3-123">Microsoft ASP.NET 平台提供广泛支持用于本地化为标准的 ASP.NET 应用程序通过集成标准.NET 本地化模型;Microsoft AJAX Framework 利用集成的模型，以支持将在其中执行本地化的各种方案。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-123">The Microsoft ASP.NET platform provides extensive support for localization for standard ASP.NET applications by integrating the standard .NET localization model; the Microsoft AJAX Framework utilize the integrated model to support the diverse scenarios in which localization can be performed.</span></span> <span data-ttu-id="d4ad3-124">通过正在部署到附属程序集，或通过利用静态文件系统结构来，也可以借助 Microsoft AJAX 框架，本地化脚本。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-124">With the Microsoft AJAX Framework, scripts can either be localized by being deployed into satellite assemblies, or by utilizing a static file system structure.</span></span>

## <a name="embedding-scripts-with-satellite-assemblies"></a><span data-ttu-id="d4ad3-125">*嵌入附属程序集使用的脚本*</span><span class="sxs-lookup"><span data-stu-id="d4ad3-125">*Embedding Scripts with Satellite Assemblies*</span></span>

<span data-ttu-id="d4ad3-126">与标准的.NET Framework 本地化策略一致，资源可以包含在附属程序集。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-126">Consistent with the standard .NET Framework localization strategy, resources can be included in satellite assemblies.</span></span> <span data-ttu-id="d4ad3-127">附属程序集具有多项优点通过传统的资源包含在二进制文件的任何给定的本地化可以更新而更新更大的映像，可以只需通过安装到的附属程序集部署其他本地化信息而不会导致主项目程序集重新加载，可以部署的项目文件夹和附属程序集。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-127">Satellite assemblies provide several advantages over traditional resource inclusion in binaries - any given localization can be updated without updating the larger image, additional localizations can be deployed simply by installing satellite assemblies into the project folder, and satellite assemblies can be deployed without causing a reload of the main project assembly.</span></span> <span data-ttu-id="d4ad3-128">尤其是在 ASP.NET 项目，这将是有益的因为它可以显著减少所使用的增量更新的系统资源量，并按最小方式会中断生产网站使用情况。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-128">Particularly in ASP.NET projects, this is beneficial because it can significantly reduce the amount of system resources used by incremental updates, and minimally disrupts production website usage.</span></span>

<span data-ttu-id="d4ad3-129">脚本嵌入到程序集，它们包含在托管.resx （或编译.resources） 文件，都将包括在编译时程序集。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-129">Scripts are embedded into assemblies by including them in managed .resx (or compiled .resources) files, which are included into the assembly at compile-time.</span></span> <span data-ttu-id="d4ad3-130">然后，其资源可用于通过 AJAX 运行时生成代码，程序集级别属性通过脚本应用程序</span><span class="sxs-lookup"><span data-stu-id="d4ad3-130">Their resources are then made available to the script application through AJAX runtime-generated code, via assembly-level attributes</span></span>

<span data-ttu-id="d4ad3-131">*嵌入的脚本文件的命名约定*</span><span class="sxs-lookup"><span data-stu-id="d4ad3-131">*Naming Conventions for Embedded Script Files*</span></span>

<span data-ttu-id="d4ad3-132">Microsoft AJAX 框架脚本管理支持多种选项用于部署和测试脚本，并且提供了准则，以便这些选项。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-132">The Microsoft AJAX Framework script management supports a variety of options for use in deployment and testing of scripts, and guidelines are provided to facilitate these options.</span></span>

<span data-ttu-id="d4ad3-133">*为了便于调试：*</span><span class="sxs-lookup"><span data-stu-id="d4ad3-133">*To facilitate debugging:*</span></span>

<span data-ttu-id="d4ad3-134">版本 （生产） 脚本不应包含`.debug`文件名中的限定符。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-134">Release (production) scripts should not include the `.debug` qualifier in the filename.</span></span> <span data-ttu-id="d4ad3-135">脚本调试应包括用于`.debug`通配符 \* 和？。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-135">Scripts designed for debugging should include `.debug` in the filename.</span></span>

<span data-ttu-id="d4ad3-136">*为了便于本地化：*</span><span class="sxs-lookup"><span data-stu-id="d4ad3-136">*To facilitate localization:*</span></span>

<span data-ttu-id="d4ad3-137">非特定区域性脚本不应包含任何区域性标识符的文件的名称。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-137">Neutral-culture scripts should not include any culture identifier in the name of the file.</span></span> <span data-ttu-id="d4ad3-138">对于包含本地化的资源的脚本，应在文件名中指定的 ISO 语言代码。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-138">For scripts that contain localized resources, the ISO language code should be specified in the file name.</span></span> <span data-ttu-id="d4ad3-139">例如，`es-CO`西班牙语，哥伦比亚代表。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-139">For example, `es-CO` stands for Spanish, Columbia.</span></span>

<span data-ttu-id="d4ad3-140">下表总结了文件命名约定的示例：</span><span class="sxs-lookup"><span data-stu-id="d4ad3-140">The following table summarizes the file naming conventions with examples:</span></span>

| <span data-ttu-id="d4ad3-141">Filename</span><span class="sxs-lookup"><span data-stu-id="d4ad3-141">Filename</span></span> | <span data-ttu-id="d4ad3-142">含义</span><span class="sxs-lookup"><span data-stu-id="d4ad3-142">Meaning</span></span> |
| --- | --- |
| <span data-ttu-id="d4ad3-143">Script.js</span><span class="sxs-lookup"><span data-stu-id="d4ad3-143">Script.js</span></span> | <span data-ttu-id="d4ad3-144">一个发行版本的非特定于区域性的脚本。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-144">A release-version culture-neutral script.</span></span> |
| <span data-ttu-id="d4ad3-145">Script.debug.js</span><span class="sxs-lookup"><span data-stu-id="d4ad3-145">Script.debug.js</span></span> | <span data-ttu-id="d4ad3-146">一个调试版本的非特定于区域性的脚本。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-146">A debug-version culture-neutral script.</span></span> |
| <span data-ttu-id="d4ad3-147">Script.en-US.js</span><span class="sxs-lookup"><span data-stu-id="d4ad3-147">Script.en-US.js</span></span> | <span data-ttu-id="d4ad3-148">发行版适用于英语，美国脚本。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-148">A release version English, United States script.</span></span> |
| <span data-ttu-id="d4ad3-149">Script.debug.es-CO.js</span><span class="sxs-lookup"><span data-stu-id="d4ad3-149">Script.debug.es-CO.js</span></span> | <span data-ttu-id="d4ad3-150">调试版本西班牙语，哥伦比亚脚本。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-150">A debug-version Spanish, Columbia script.</span></span> |

## <a name="walkthrough-create-an-localized-embedded-script"></a><span data-ttu-id="d4ad3-151">演练： 创建本地化、 嵌入的脚本</span><span class="sxs-lookup"><span data-stu-id="d4ad3-151">Walkthrough: Create an Localized, Embedded Script</span></span>

<span data-ttu-id="d4ad3-152">*请注意： 本演练需要 Visual Studio 2008 的使用，因为 Visual Web Developer Express 不包括用于类库项目的项目模板。*</span><span class="sxs-lookup"><span data-stu-id="d4ad3-152">*Please note: this walkthrough requires the use of Visual Studio 2008 as Visual Web Developer Express does not include a project template for class library projects.*</span></span>

1. <span data-ttu-id="d4ad3-153">使用集成的 ASP.NET AJAX Extensions 中创建新的网站项目。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-153">Create a new Web Site project with ASP.NET AJAX Extensions integrated.</span></span> <span data-ttu-id="d4ad3-154">创建另一个项目，一个类库项目，调用 LocalizingResources 解决方案中。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-154">Create another project, a Class Library project, within the solution called LocalizingResources.</span></span>
2. <span data-ttu-id="d4ad3-155">添加到 LocalizingResources 项目中，调用 VerifyDeletion.js Jscript 文件以及称为 DeletionResources.resx 和 DeletionResources.es.resx.resx 资源文件。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-155">Add a Jscript file called VerifyDeletion.js to the LocalizingResources project, as well as .resx resources files called DeletionResources.resx and DeletionResources.es.resx.</span></span> <span data-ttu-id="d4ad3-156">前者将包含非特定于区域性的资源;后者将包含西班牙语语言资源。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-156">The former will contain culture-neutral resources; the latter will contain Spanish-language resources.</span></span>
3. <span data-ttu-id="d4ad3-157">将以下代码添加到 VerifyDeletion.js:</span><span class="sxs-lookup"><span data-stu-id="d4ad3-157">Add the following code to VerifyDeletion.js:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

<span data-ttu-id="d4ad3-158">对于熟悉 JavaScript 正则表达式语法中，单个正斜杠中的文本 （在前面的示例中，/FILENAME/ 是一个例子） 表示 RegExp 对象。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-158">For those unfamiliar with JavaScript Regex syntax, text within single forward slashes (in the previous example, /FILENAME/ is an example) denotes a RegExp object.</span></span> <span data-ttu-id="d4ad3-159">MSDN 库中包含大量的 JavaScript 参考，并在 JavaScript 本机对象上的资源可找到联机。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-159">The MSDN Library contains an extensive JavaScript reference, and resources on JavaScript native objects can be found online.</span></span>

1. <span data-ttu-id="d4ad3-160">将下面的资源字符串添加到 DeletionResources.resx:</span><span class="sxs-lookup"><span data-stu-id="d4ad3-160">Add the following resource strings to DeletionResources.resx:</span></span> 

    <span data-ttu-id="d4ad3-161">**VerifyDelete**： 是否确实要删除文件名？</span><span class="sxs-lookup"><span data-stu-id="d4ad3-161">**VerifyDelete**: Are you sure you want to delete FILENAME?</span></span>

    <span data-ttu-id="d4ad3-162">**删除**: FILENAME 已被删除。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-162">**Deleted**: FILENAME has been deleted.</span></span>

1. <span data-ttu-id="d4ad3-163">将下面的资源字符串添加到 DeletionResources.es.resx:</span><span class="sxs-lookup"><span data-stu-id="d4ad3-163">Add the following resource strings to DeletionResources.es.resx:</span></span> 

    <span data-ttu-id="d4ad3-164">**VerifyDelete**： 东部 seguro 汉阳 desee quitar FILENAME？</span><span class="sxs-lookup"><span data-stu-id="d4ad3-164">**VerifyDelete**: Est seguro que desee quitar FILENAME?</span></span>

    <span data-ttu-id="d4ad3-165">**删除**: FILENAME se ha quitado。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-165">**Deleted**: FILENAME se ha quitado.</span></span>
2. <span data-ttu-id="d4ad3-166">将以下代码行添加到 AssemblyInfo 文件：</span><span class="sxs-lookup"><span data-stu-id="d4ad3-166">Add the following lines of code to the AssemblyInfo file:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. <span data-ttu-id="d4ad3-167">向 LocalizingResources 项目中添加对 System.Web 和 System.Web.Extensions 的引用。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-167">Add references to System.Web and System.Web.Extensions to the LocalizingResources project.</span></span>
2. <span data-ttu-id="d4ad3-168">添加到 LocalizingResources 项目中的网站项目的引用。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-168">Add a reference to the LocalizingResources project from the Web Site project.</span></span>
3. <span data-ttu-id="d4ad3-169">在 default.aspx 中，在网站项目下，使用以下其他标记更新 ScriptManager 控件：</span><span class="sxs-lookup"><span data-stu-id="d4ad3-169">In default.aspx, under the Web Site project, update the ScriptManager control with the following additional markup:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. <span data-ttu-id="d4ad3-170">在 default.aspx 中，任何位置的页上，包括此标记：</span><span class="sxs-lookup"><span data-stu-id="d4ad3-170">In default.aspx, anywhere on the page, include this markup:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. <span data-ttu-id="d4ad3-171">按 F5。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-171">Press F5.</span></span> <span data-ttu-id="d4ad3-172">如果系统提示，请启用调试。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-172">If prompted, enable debugging.</span></span> <span data-ttu-id="d4ad3-173">当加载页时，按删除按钮。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-173">When the page is loaded, press the Delete button.</span></span> <span data-ttu-id="d4ad3-174">请注意，你会提示您在英语中 （除非默认情况下，你的计算机设置首选西班牙语语言资源） 进行确认。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-174">Note that you are prompted in English (unless your computer is set to prefer Spanish-language resources by default) for confirmation.</span></span>
2. <span data-ttu-id="d4ad3-175">关闭浏览器窗口，并返回到 default.aspx。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-175">Close the browser window and return to default.aspx.</span></span> <span data-ttu-id="d4ad3-176">在@Page标头指令，与 ES-ES 区域性和 UICulture 替换自动。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-176">In the @Page header directive, replace auto for Culture and UICulture with es-ES.</span></span> <span data-ttu-id="d4ad3-177">再次按 F5 以启动 web 浏览器中一次应用程序。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-177">Press F5 again to launch the web application in the browser again.</span></span> <span data-ttu-id="d4ad3-178">此时，请注意，提示您删除西班牙语文件：</span><span class="sxs-lookup"><span data-stu-id="d4ad3-178">This time, note that you are prompted to delete the file in Spanish:</span></span>


[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

<span data-ttu-id="d4ad3-179">([单击以查看实际尺寸的图像](understanding-asp-net-ajax-localization/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d4ad3-179">([Click to view full-size image](understanding-asp-net-ajax-localization/_static/image3.png))</span></span>


[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

<span data-ttu-id="d4ad3-180">([单击以查看实际尺寸的图像](understanding-asp-net-ajax-localization/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="d4ad3-180">([Click to view full-size image](understanding-asp-net-ajax-localization/_static/image6.png))</span></span>


<span data-ttu-id="d4ad3-181">请注意，对于本演练的几种变体。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-181">Note that there are several variations for this walkthrough.</span></span> <span data-ttu-id="d4ad3-182">例如，脚本不能注册与 ScriptManager 控件以编程方式在页面加载过程。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-182">For instance, scripts could be registered with the ScriptManager control programmatically during page load.</span></span>

## <a name="including-a-static-script-file-structure"></a><span data-ttu-id="d4ad3-183">*包括静态脚本文件结构*</span><span class="sxs-lookup"><span data-stu-id="d4ad3-183">*Including a Static Script File Structure*</span></span>

<span data-ttu-id="d4ad3-184">当使用静态的脚本文件进行部署，你丢失部分使用的固有的.NET 本地化方案的好处。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-184">When using static script files for deployment, you lose some of the benefits of using the inherent .NET localization scheme.</span></span> <span data-ttu-id="d4ad3-185">主要可见，则为，则会失去自动从包括脚本资源文件; 生成的类型在上面的演练中，例如，资源已公开的消息调用从 ScriptManager 控件自动生成类型。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-185">Primarily visible is that you lose the automatic type generated from including script resource files; in the above walkthrough, for example, resources were exposed by an automatically-generated type called Message from the ScriptManager control.</span></span>

<span data-ttu-id="d4ad3-186">有，但是，某些优点使用静态的脚本文件结构。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-186">There are, however, some benefits to using a static script file structure.</span></span> <span data-ttu-id="d4ad3-187">无需重新编译和重新部署附属程序集，就可以执行更新和静态文件结构的使用也可以重写嵌入的脚本，以将一个次要可能尚未发运的功能集成的组件。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-187">Updates can be performed without recompiling and redeploying satellite assemblies, and the use of a static file structure can also be done to override embedded script, to integrate a minor piece of functionality that may not have been shipped with a component.</span></span>

<span data-ttu-id="d4ad3-188">Microsoft 建议避免通过自动在项目编译期间生成你的脚本资源的版本控制问题。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-188">Microsoft recommends avoiding a version control issue by automatically generating your script resources during project compilation.</span></span> <span data-ttu-id="d4ad3-189">当维护大量的脚本代码基，它可能会变得越来越困难，以确保代码更改都会反映在每个本地化的脚本。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-189">When maintaining an extensive script code base, it can become increasingly difficult to ensure that code changes are reflected in each localized script.</span></span> <span data-ttu-id="d4ad3-190">作为替代方法，则可以只需保持一个逻辑脚本和多个本地化脚本，在生成项目时合并文件。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-190">As an alternative, you can simply maintain one logic script and multiple localization scripts, merging the files while building the project.</span></span>

<span data-ttu-id="d4ad3-191">由于不是资源，以声明方式包括，静态文件应为的脚本引用通过添加`<asp:ScriptElement>`元素的子级作为`<Scripts>`标记 ScriptManager 控件，或通过以编程方式添加`ScriptReference`对象到`Scripts`属性`ScriptManager`在运行时页面上的控件。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-191">Because there are not resources to declaratively include, static script files should be referenced either by adding `<asp:ScriptElement>` elements as a child of the `<Scripts>` tag of the ScriptManager control, or by programmatically adding `ScriptReference` objects to the `Scripts` property of the `ScriptManager` control on the page at runtime.</span></span>

## <a name="the-scriptmanager-and-its-role-in-localization"></a><span data-ttu-id="d4ad3-192">*ScriptManager 和本地化中的其角色*</span><span class="sxs-lookup"><span data-stu-id="d4ad3-192">*The ScriptManager and its Role in Localization*</span></span>

<span data-ttu-id="d4ad3-193">ScriptManager 使本地化应用程序的多个自动行为：</span><span class="sxs-lookup"><span data-stu-id="d4ad3-193">The ScriptManager enables several automatic behaviors for localized applications:</span></span>

- <span data-ttu-id="d4ad3-194">它将自动定位基于设置和命名约定; 的脚本文件例如，它将加载在调试模式下，启用了调试的脚本并加载本地化基于浏览器的用户界面选择的脚本。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-194">It automatically locates script files based on settings and naming conventions; for instance, it loads debug-enabled scripts when in debugging mode, and loads localized scripts based on the browser's user interface selection.</span></span>
- <span data-ttu-id="d4ad3-195">它使您能够定义区域性，包括自定义区域性。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-195">It enables the definition of cultures, including custom cultures.</span></span>
- <span data-ttu-id="d4ad3-196">它允许 HTTP 压缩的脚本文件。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-196">It enables the compression of script files over HTTP.</span></span>
- <span data-ttu-id="d4ad3-197">它将缓存脚本来高效地管理多请求。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-197">It caches scripts to efficiently manage many requests.</span></span>
- <span data-ttu-id="d4ad3-198">它将一个间接层添加到脚本中，其由管道它们通过加密的 URL。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-198">It adds a layer of indirection to scripts by piping them through an encrypted URL.</span></span>

<span data-ttu-id="d4ad3-199">以编程方式或通过声明性的标记，则可以将脚本引用添加到 ScriptManager 控件。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-199">Script references can be added to the ScriptManager control either programmatically or by declarative markup.</span></span> <span data-ttu-id="d4ad3-200">声明性的标记时特别有用在使用脚本中嵌入的程序集，而不是网站项目本身，如脚本的名称可能不会发生更改修订推送。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-200">Declarative markup is particularly useful when working with scripts embedded in assemblies other than the web site project itself, as the name of the script will likely not change as revisions are pushed through.</span></span>

## <a name="summary"></a><span data-ttu-id="d4ad3-201">总结</span><span class="sxs-lookup"><span data-stu-id="d4ad3-201">Summary</span></span>

<span data-ttu-id="d4ad3-202">随着 web 应用程序的增长来访问更大的受众，需要能够访问更广泛的区域性和社区变得内核数与业务模型电子商务 web 应用程序需要能够处理外货币，需要为其内容，但还其导航提示并在其他语言和公司的窗体字段需要知道这一需要是不仅可以存在内容管理系统可访问。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-202">As web applications grow to reach a larger audience, the need to be able to reach broader cultures and communities becomes core to a business model; e-commerce web applications need to be able to deal with foreign currencies, content management systems need to be able to not only present their content but also their navigation hints and form fields in other languages, and companies need to know that this need is accessible.</span></span>

<span data-ttu-id="d4ad3-203">.NET Framework 本质上支持丰富的本地化框架中，利用附属程序集和 XML 资源 (.resx) 文件提供统一的方式来查找资源字符串和图像。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-203">The .NET Framework intrinsically supports a rich localization framework, utilizing satellite assemblies and XML resource (.resx) files to present a uniform way to look up resource strings and images.</span></span> <span data-ttu-id="d4ad3-204">ASP.NET AJAX Extensions 中，包括 Microsoft AJAX Framework 和 Microsoft AJAX 脚本库，提供支持对此编程模型到客户端代码中，启用简单的资源字符串查找。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-204">The ASP.NET AJAX Extensions, including the Microsoft AJAX Framework and Microsoft AJAX Script Library, provide support for this programming model into client-side code, enabling easy resource string lookups.</span></span> <span data-ttu-id="d4ad3-205">附属程序集支持自动包含通过 ScriptResource.axd 的脚本资源 （实际的.js 文件），只要文件名遵守给定的命名方案。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-205">Satellite assemblies support the automatic inclusion of script resources (actual .js files) through ScriptResource.axd as long as the filenames follow a given naming scheme.</span></span> <span data-ttu-id="d4ad3-206">利用此支持，使用 ASP.NET AJAX Extensions 简化脚本的本地化和全球化应用程序。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-206">With this support, the ASP.NET AJAX Extensions simplify the localization of scripts and the globalization of applications.</span></span>

## <a name="bio"></a><span data-ttu-id="d4ad3-207">*Bio*</span><span class="sxs-lookup"><span data-stu-id="d4ad3-207">*Bio*</span></span>

<span data-ttu-id="d4ad3-208">Scott 类别自 1997 年以来处理与 Microsoft Web 技术，并且是 myKB.com 总裁 ([www.myKB.com](http://www.myKB.com)) 其中他专注于编写 ASP.NET 基于侧重于知识库软件解决方案的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d4ad3-208">Scott Cate has been working with Microsoft Web technologies since 1997 and is the President of myKB.com ([www.myKB.com](http://www.myKB.com)) where he specializes in writing ASP.NET based applications focused on Knowledge Base Software solutions.</span></span> <span data-ttu-id="d4ad3-209">可以通过在电子邮件联系 Scott [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com)或在其博客地址[ScottCate.com](http://ScottCate.com)</span><span class="sxs-lookup"><span data-stu-id="d4ad3-209">Scott can be contacted via email at [scott.cate@myKB.com](mailto:scott.cate@myKB.com) or his blog at [ScottCate.com](http://ScottCate.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d4ad3-210">[上一页](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
> [下一页](understanding-asp-net-ajax-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="d4ad3-210">[Previous](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
[Next](understanding-asp-net-ajax-web-services.md)</span></span>
