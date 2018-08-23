---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: 了解 ASP.NET AJAX 本地化 |Microsoft Docs
author: scottcate
description: 本地化是设计并将对特定语言和区域性的支持集成到应用程序或应用程序组件的过程。 Mic...
ms.author: riande
ms.date: 03/14/2008
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: 86cbf150708f1db711b40ccbc25345afeb3e542a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832893"
---
<a name="understanding-aspnet-ajax-localization"></a><span data-ttu-id="1daa6-104">了解 ASP.NET AJAX 本地化</span><span class="sxs-lookup"><span data-stu-id="1daa6-104">Understanding ASP.NET AJAX Localization</span></span>
====================
<span data-ttu-id="1daa6-105">通过[Scott Cate](https://github.com/scottcate)</span><span class="sxs-lookup"><span data-stu-id="1daa6-105">by [Scott Cate](https://github.com/scottcate)</span></span>

[<span data-ttu-id="1daa6-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="1daa6-106">Download PDF</span></span>](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> <span data-ttu-id="1daa6-107">本地化是设计并将对特定语言和区域性的支持集成到应用程序或应用程序组件的过程。</span><span class="sxs-lookup"><span data-stu-id="1daa6-107">Localization is the process of designing and integrating support for a specific language and culture into an application or an application component.</span></span> <span data-ttu-id="1daa6-108">Microsoft ASP.NET 平台通过集成标准.NET 本地化模型; 为标准 ASP.NET 应用程序的本地化提供广泛支持Microsoft AJAX 框架利用集成的模型，以支持可在其中执行本地化的各种方案。</span><span class="sxs-lookup"><span data-stu-id="1daa6-108">The Microsoft ASP.NET platform provides extensive support for localization for standard ASP.NET applications by integrating the standard .NET localization model; the Microsoft AJAX Framework utilize the integrated model to support the diverse scenarios in which localization can be performed.</span></span>


## <a name="introduction"></a><span data-ttu-id="1daa6-109">介绍</span><span class="sxs-lookup"><span data-stu-id="1daa6-109">Introduction</span></span>

<span data-ttu-id="1daa6-110">Microsoft 的 ASP.NET 技术带来了面向对象和事件驱动的编程模型，并将其与已编译的代码的好处结合在一起。</span><span class="sxs-lookup"><span data-stu-id="1daa6-110">Microsoft's ASP.NET technology brings an object-oriented and event-driven programming model and unites it with the benefits of compiled code.</span></span> <span data-ttu-id="1daa6-111">但是，其服务器端处理模型有几个缺点固有的技术，其中很多可以通过 System.Web.Extensions 命名空间，它封装在.NET Framework 中的 Microsoft AJAX 服务中包括的新功能进行寻址3.5。</span><span class="sxs-lookup"><span data-stu-id="1daa6-111">However, its server-side processing model has several drawbacks inherent in the technology, many of which can be addressed by the new features included in the System.Web.Extensions namespace, which encapsulates the Microsoft AJAX Services in the .NET Framework 3.5.</span></span> <span data-ttu-id="1daa6-112">使用这些扩展，许多丰富的客户端功能，以前为 ASP.NET 2.0 AJAX Extensions 的一部分，但现在的 Framework 基类库的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="1daa6-112">These extensions enable many rich client features, previously available as part of the ASP.NET 2.0 AJAX Extensions, but now part of the Framework Base Class Library.</span></span> <span data-ttu-id="1daa6-113">控件和此命名空间中的功能而无需整页刷新，客户端脚本 （包括 ASP.NET 分析 API），通过访问 Web 服务的功能包括部分呈现的页和扩展的客户端的 API 设计要镜像的许多了解在 ASP.NET 服务器端控件集中控制方案。</span><span class="sxs-lookup"><span data-stu-id="1daa6-113">Controls and features in this namespace include partial rendering of pages without requiring a full page refresh, the ability to access Web Services via client script (including the ASP.NET profiling API), and an extensive client-side API designed to mirror many of the control schemes seen in the ASP.NET server-side control set.</span></span>

<span data-ttu-id="1daa6-114">本白皮书将检查中的 Microsoft AJAX Framework 和 Microsoft AJAX 脚本库，用于本地化支持和进行审阅已集成 web 中的本地化支持业务需求的上下文中存在的本地化功能提供的.NET Framework 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1daa6-114">This whitepaper examines the localization features present in the Microsoft AJAX Framework and Microsoft AJAX Script Library, in the context of business need for localization support and reviewing already-integrated support for localization in web applications provided by the .NET Framework.</span></span> <span data-ttu-id="1daa6-115">Microsoft AJAX 脚本库利用.resx 文件格式已由.NET 应用程序，它提供了集成的 IDE 支持和可共享的资源类型。</span><span class="sxs-lookup"><span data-stu-id="1daa6-115">The Microsoft AJAX Script Library utilizes the .resx file format already used by .NET applications, which provides integrated IDE support and a shareable resource type.</span></span>

<span data-ttu-id="1daa6-116">此白皮书基于在 Microsoft Visual Studio 2008 Beta 2 版本上。</span><span class="sxs-lookup"><span data-stu-id="1daa6-116">This whitepaper is based on the Beta 2 release of Microsoft Visual Studio 2008.</span></span> <span data-ttu-id="1daa6-117">本白皮书还假定你将使用 Visual Studio 2008 中，不 Visual Web Developer 速成版，并且将提供根据 Visual Studio 的用户界面的演练。</span><span class="sxs-lookup"><span data-stu-id="1daa6-117">This whitepaper also assumes that you will be working with Visual Studio 2008, not Visual Web Developer Express, and will provide walkthroughs according to the user interface of Visual Studio.</span></span> <span data-ttu-id="1daa6-118">一些代码示例将使用可能是在 Visual Web Developer 速成版中不可用的项目模板。</span><span class="sxs-lookup"><span data-stu-id="1daa6-118">Some code samples will utilize project templates that may be unavailable in Visual Web Developer Express.</span></span>

## <a name="the-need-for-localization"></a><span data-ttu-id="1daa6-119">*需要本地化*</span><span class="sxs-lookup"><span data-stu-id="1daa6-119">*The Need for Localization*</span></span>

<span data-ttu-id="1daa6-120">特别是对于企业应用程序开发人员和组件开发人员，创建可以随时了解区域性和语言之间的差异的工具的功能已成为越来越有必要。</span><span class="sxs-lookup"><span data-stu-id="1daa6-120">Particularly for enterprise application developers and component developers, the ability to create tools that can be aware of the differences between cultures and languages has become increasingly necessary.</span></span> <span data-ttu-id="1daa6-121">设计组件能够适应客户端的区域设置提高了开发人员工作效率并减少组件的自适应的全局函数所需的工作量。</span><span class="sxs-lookup"><span data-stu-id="1daa6-121">Designing components with the ability to adapt to the locale of the client increases developer productivity and reduces the amount of work required for the adaptation of a component to function globally.</span></span>

<span data-ttu-id="1daa6-122">本地化是设计并将对特定语言和区域性的支持集成到应用程序或应用程序组件的过程。</span><span class="sxs-lookup"><span data-stu-id="1daa6-122">Localization is the process of designing and integrating support for a specific language and culture into an application or an application component.</span></span> <span data-ttu-id="1daa6-123">Microsoft ASP.NET 平台通过集成标准.NET 本地化模型; 为标准 ASP.NET 应用程序的本地化提供广泛支持Microsoft AJAX 框架利用集成的模型，以支持可在其中执行本地化的各种方案。</span><span class="sxs-lookup"><span data-stu-id="1daa6-123">The Microsoft ASP.NET platform provides extensive support for localization for standard ASP.NET applications by integrating the standard .NET localization model; the Microsoft AJAX Framework utilize the integrated model to support the diverse scenarios in which localization can be performed.</span></span> <span data-ttu-id="1daa6-124">正在部署到附属程序集中，或使用静态文件系统结构，也可以使用 Microsoft AJAX 框架，本地化脚本。</span><span class="sxs-lookup"><span data-stu-id="1daa6-124">With the Microsoft AJAX Framework, scripts can either be localized by being deployed into satellite assemblies, or by utilizing a static file system structure.</span></span>

## <a name="embedding-scripts-with-satellite-assemblies"></a><span data-ttu-id="1daa6-125">*将脚本嵌入附属程序集*</span><span class="sxs-lookup"><span data-stu-id="1daa6-125">*Embedding Scripts with Satellite Assemblies*</span></span>

<span data-ttu-id="1daa6-126">与标准.NET Framework 本地化策略保持一致，资源可以包含在附属程序集。</span><span class="sxs-lookup"><span data-stu-id="1daa6-126">Consistent with the standard .NET Framework localization strategy, resources can be included in satellite assemblies.</span></span> <span data-ttu-id="1daa6-127">附属程序集提供几项优势通过传统的资源包含在二进制文件的任何给定的本地化可以更新而不更新可查看大图像，可以只需通过安装附属程序集到部署其他本地化信息项目文件夹和附属程序集可以部署而不会导致主项目程序集的重新加载。</span><span class="sxs-lookup"><span data-stu-id="1daa6-127">Satellite assemblies provide several advantages over traditional resource inclusion in binaries - any given localization can be updated without updating the larger image, additional localizations can be deployed simply by installing satellite assemblies into the project folder, and satellite assemblies can be deployed without causing a reload of the main project assembly.</span></span> <span data-ttu-id="1daa6-128">特别是在 ASP.NET 项目中，此功能非常有用，它可以显著减少增量更新所使用的系统资源的数量和最小日志会中断生产网站使用情况。</span><span class="sxs-lookup"><span data-stu-id="1daa6-128">Particularly in ASP.NET projects, this is beneficial because it can significantly reduce the amount of system resources used by incremental updates, and minimally disrupts production website usage.</span></span>

<span data-ttu-id="1daa6-129">脚本嵌入到程序集将这些命令包含在管理.resx （或编译.resources） 文件，都将包括在编译时程序集。</span><span class="sxs-lookup"><span data-stu-id="1daa6-129">Scripts are embedded into assemblies by including them in managed .resx (or compiled .resources) files, which are included into the assembly at compile-time.</span></span> <span data-ttu-id="1daa6-130">其资源然后都提供给脚本的应用程序通过 AJAX 运行时生成的代码，通过程序集级别属性</span><span class="sxs-lookup"><span data-stu-id="1daa6-130">Their resources are then made available to the script application through AJAX runtime-generated code, via assembly-level attributes</span></span>

<span data-ttu-id="1daa6-131">*对于嵌入的脚本文件命名约定*</span><span class="sxs-lookup"><span data-stu-id="1daa6-131">*Naming Conventions for Embedded Script Files*</span></span>

<span data-ttu-id="1daa6-132">Microsoft AJAX Framework 脚本管理支持在部署和测试的脚本中使用的各种选项并提供指导原则以促进这些选项。</span><span class="sxs-lookup"><span data-stu-id="1daa6-132">The Microsoft AJAX Framework script management supports a variety of options for use in deployment and testing of scripts, and guidelines are provided to facilitate these options.</span></span>

<span data-ttu-id="1daa6-133">*为了便于调试：*</span><span class="sxs-lookup"><span data-stu-id="1daa6-133">*To facilitate debugging:*</span></span>

<span data-ttu-id="1daa6-134">发行 （生产） 脚本不应包含`.debug`文件名中的限定符。</span><span class="sxs-lookup"><span data-stu-id="1daa6-134">Release (production) scripts should not include the `.debug` qualifier in the filename.</span></span> <span data-ttu-id="1daa6-135">此演示适合对于调试应包含的脚本`.debug`文件名中。</span><span class="sxs-lookup"><span data-stu-id="1daa6-135">Scripts designed for debugging should include `.debug` in the filename.</span></span>

<span data-ttu-id="1daa6-136">*为了便于本地化：*</span><span class="sxs-lookup"><span data-stu-id="1daa6-136">*To facilitate localization:*</span></span>

<span data-ttu-id="1daa6-137">非特定区域性的脚本不应包括的文件的名称的任何区域性标识符。</span><span class="sxs-lookup"><span data-stu-id="1daa6-137">Neutral-culture scripts should not include any culture identifier in the name of the file.</span></span> <span data-ttu-id="1daa6-138">对于包含本地化的资源的脚本，应在文件名中指定 ISO 语言代码。</span><span class="sxs-lookup"><span data-stu-id="1daa6-138">For scripts that contain localized resources, the ISO language code should be specified in the file name.</span></span> <span data-ttu-id="1daa6-139">例如，`es-CO`代表西班牙语 （哥伦比亚）。</span><span class="sxs-lookup"><span data-stu-id="1daa6-139">For example, `es-CO` stands for Spanish, Columbia.</span></span>

<span data-ttu-id="1daa6-140">下表总结了文件命名约定的示例：</span><span class="sxs-lookup"><span data-stu-id="1daa6-140">The following table summarizes the file naming conventions with examples:</span></span>

| <span data-ttu-id="1daa6-141">Filename</span><span class="sxs-lookup"><span data-stu-id="1daa6-141">Filename</span></span> | <span data-ttu-id="1daa6-142">含义</span><span class="sxs-lookup"><span data-stu-id="1daa6-142">Meaning</span></span> |
| --- | --- |
| <span data-ttu-id="1daa6-143">Script.js</span><span class="sxs-lookup"><span data-stu-id="1daa6-143">Script.js</span></span> | <span data-ttu-id="1daa6-144">一个发行版本的非特定于区域性的脚本。</span><span class="sxs-lookup"><span data-stu-id="1daa6-144">A release-version culture-neutral script.</span></span> |
| <span data-ttu-id="1daa6-145">Script.debug.js</span><span class="sxs-lookup"><span data-stu-id="1daa6-145">Script.debug.js</span></span> | <span data-ttu-id="1daa6-146">一个调试版本的非特定于区域性的脚本。</span><span class="sxs-lookup"><span data-stu-id="1daa6-146">A debug-version culture-neutral script.</span></span> |
| <span data-ttu-id="1daa6-147">Script.en-US.js</span><span class="sxs-lookup"><span data-stu-id="1daa6-147">Script.en-US.js</span></span> | <span data-ttu-id="1daa6-148">发行版适用于英语，美国脚本。</span><span class="sxs-lookup"><span data-stu-id="1daa6-148">A release version English, United States script.</span></span> |
| <span data-ttu-id="1daa6-149">Script.debug.es-CO.js</span><span class="sxs-lookup"><span data-stu-id="1daa6-149">Script.debug.es-CO.js</span></span> | <span data-ttu-id="1daa6-150">调试版本西班牙语，哥伦比亚脚本。</span><span class="sxs-lookup"><span data-stu-id="1daa6-150">A debug-version Spanish, Columbia script.</span></span> |

## <a name="walkthrough-create-an-localized-embedded-script"></a><span data-ttu-id="1daa6-151">演练： 创建本地化的嵌入式脚本</span><span class="sxs-lookup"><span data-stu-id="1daa6-151">Walkthrough: Create an Localized, Embedded Script</span></span>

<span data-ttu-id="1daa6-152">*请注意： 本演练需要 Visual Studio 2008 的使用，因为 Visual Web Developer 速成版不包括用于类库项目的项目模板。*</span><span class="sxs-lookup"><span data-stu-id="1daa6-152">*Please note: this walkthrough requires the use of Visual Studio 2008 as Visual Web Developer Express does not include a project template for class library projects.*</span></span>

1. <span data-ttu-id="1daa6-153">使用集成的 ASP.NET AJAX Extensions 中创建新网站项目。</span><span class="sxs-lookup"><span data-stu-id="1daa6-153">Create a new Web Site project with ASP.NET AJAX Extensions integrated.</span></span> <span data-ttu-id="1daa6-154">创建另一个项目，一个类库项目，名为 LocalizingResources 解决方案中。</span><span class="sxs-lookup"><span data-stu-id="1daa6-154">Create another project, a Class Library project, within the solution called LocalizingResources.</span></span>
2. <span data-ttu-id="1daa6-155">将添加到 LocalizingResources 项目名 VerifyDeletion.js 的 Jscript 文件，以及名为 DeletionResources.resx 和 DeletionResources.es.resx.resx 资源文件。</span><span class="sxs-lookup"><span data-stu-id="1daa6-155">Add a Jscript file called VerifyDeletion.js to the LocalizingResources project, as well as .resx resources files called DeletionResources.resx and DeletionResources.es.resx.</span></span> <span data-ttu-id="1daa6-156">前者将包含非特定区域性的资源;后一种将包含西班牙语语言资源。</span><span class="sxs-lookup"><span data-stu-id="1daa6-156">The former will contain culture-neutral resources; the latter will contain Spanish-language resources.</span></span>
3. <span data-ttu-id="1daa6-157">将以下代码添加到 VerifyDeletion.js:</span><span class="sxs-lookup"><span data-stu-id="1daa6-157">Add the following code to VerifyDeletion.js:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

<span data-ttu-id="1daa6-158">熟悉 JavaScript 正则表达式语法中，在单个正斜杠的文本 （在上一示例中，/FILENAME/ 是一个例子） 表示的 RegExp 对象。</span><span class="sxs-lookup"><span data-stu-id="1daa6-158">For those unfamiliar with JavaScript Regex syntax, text within single forward slashes (in the previous example, /FILENAME/ is an example) denotes a RegExp object.</span></span> <span data-ttu-id="1daa6-159">MSDN 库中包含大量的 JavaScript 引用，并可以在线找到 JavaScript 本机对象上的资源。</span><span class="sxs-lookup"><span data-stu-id="1daa6-159">The MSDN Library contains an extensive JavaScript reference, and resources on JavaScript native objects can be found online.</span></span>

1. <span data-ttu-id="1daa6-160">将以下资源字符串添加到 DeletionResources.resx:</span><span class="sxs-lookup"><span data-stu-id="1daa6-160">Add the following resource strings to DeletionResources.resx:</span></span> 

    <span data-ttu-id="1daa6-161">**VerifyDelete**： 是否确实要删除文件名？</span><span class="sxs-lookup"><span data-stu-id="1daa6-161">**VerifyDelete**: Are you sure you want to delete FILENAME?</span></span>

    <span data-ttu-id="1daa6-162">**删除**： 文件名已被删除。</span><span class="sxs-lookup"><span data-stu-id="1daa6-162">**Deleted**: FILENAME has been deleted.</span></span>

1. <span data-ttu-id="1daa6-163">将以下资源字符串添加到 DeletionResources.es.resx:</span><span class="sxs-lookup"><span data-stu-id="1daa6-163">Add the following resource strings to DeletionResources.es.resx:</span></span> 

    <span data-ttu-id="1daa6-164">**VerifyDelete**： 美国东部时间 seguro que desee quitar 文件名？</span><span class="sxs-lookup"><span data-stu-id="1daa6-164">**VerifyDelete**: Est seguro que desee quitar FILENAME?</span></span>

    <span data-ttu-id="1daa6-165">**删除**: FILENAME se ha quitado。</span><span class="sxs-lookup"><span data-stu-id="1daa6-165">**Deleted**: FILENAME se ha quitado.</span></span>
2. <span data-ttu-id="1daa6-166">将以下代码行添加到程序集信息文件：</span><span class="sxs-lookup"><span data-stu-id="1daa6-166">Add the following lines of code to the AssemblyInfo file:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. <span data-ttu-id="1daa6-167">向 LocalizingResources 项目中添加对 System.Web 和 System.Web.Extensions 的引用。</span><span class="sxs-lookup"><span data-stu-id="1daa6-167">Add references to System.Web and System.Web.Extensions to the LocalizingResources project.</span></span>
2. <span data-ttu-id="1daa6-168">添加对 LocalizingResources 项目中的网站项目的引用。</span><span class="sxs-lookup"><span data-stu-id="1daa6-168">Add a reference to the LocalizingResources project from the Web Site project.</span></span>
3. <span data-ttu-id="1daa6-169">在 default.aspx 中，在网站项目下，使用以下其他标记中更新 ScriptManager 控件：</span><span class="sxs-lookup"><span data-stu-id="1daa6-169">In default.aspx, under the Web Site project, update the ScriptManager control with the following additional markup:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. <span data-ttu-id="1daa6-170">在 default.aspx 中，任意位置在页上，包括此标记：</span><span class="sxs-lookup"><span data-stu-id="1daa6-170">In default.aspx, anywhere on the page, include this markup:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. <span data-ttu-id="1daa6-171">按 F5。</span><span class="sxs-lookup"><span data-stu-id="1daa6-171">Press F5.</span></span> <span data-ttu-id="1daa6-172">如果系统提示，请启用调试。</span><span class="sxs-lookup"><span data-stu-id="1daa6-172">If prompted, enable debugging.</span></span> <span data-ttu-id="1daa6-173">加载页面时，按删除按钮。</span><span class="sxs-lookup"><span data-stu-id="1daa6-173">When the page is loaded, press the Delete button.</span></span> <span data-ttu-id="1daa6-174">请注意，您会提示您在英语中 （除非默认情况下，您的计算机设置为首选西班牙语语言资源） 进行确认。</span><span class="sxs-lookup"><span data-stu-id="1daa6-174">Note that you are prompted in English (unless your computer is set to prefer Spanish-language resources by default) for confirmation.</span></span>
2. <span data-ttu-id="1daa6-175">关闭浏览器窗口并返回到 default.aspx。</span><span class="sxs-lookup"><span data-stu-id="1daa6-175">Close the browser window and return to default.aspx.</span></span> <span data-ttu-id="1daa6-176">在@Page标头指令，使用 ES-ES 区域性和 UICulture 替换为自动。</span><span class="sxs-lookup"><span data-stu-id="1daa6-176">In the @Page header directive, replace auto for Culture and UICulture with es-ES.</span></span> <span data-ttu-id="1daa6-177">按 F5 再次启动 web 浏览器中一次应用程序。</span><span class="sxs-lookup"><span data-stu-id="1daa6-177">Press F5 again to launch the web application in the browser again.</span></span> <span data-ttu-id="1daa6-178">这一次，请注意，系统会提示删除在西班牙语中的文件：</span><span class="sxs-lookup"><span data-stu-id="1daa6-178">This time, note that you are prompted to delete the file in Spanish:</span></span>


[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

<span data-ttu-id="1daa6-179">([单击此项可查看原尺寸图像](understanding-asp-net-ajax-localization/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1daa6-179">([Click to view full-size image](understanding-asp-net-ajax-localization/_static/image3.png))</span></span>


[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

<span data-ttu-id="1daa6-180">([单击此项可查看原尺寸图像](understanding-asp-net-ajax-localization/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="1daa6-180">([Click to view full-size image](understanding-asp-net-ajax-localization/_static/image6.png))</span></span>


<span data-ttu-id="1daa6-181">请注意，在本演练中的多个变体。</span><span class="sxs-lookup"><span data-stu-id="1daa6-181">Note that there are several variations for this walkthrough.</span></span> <span data-ttu-id="1daa6-182">例如，脚本不能注册使用 ScriptManager 控件以编程方式在页面加载过程。</span><span class="sxs-lookup"><span data-stu-id="1daa6-182">For instance, scripts could be registered with the ScriptManager control programmatically during page load.</span></span>

## <a name="including-a-static-script-file-structure"></a><span data-ttu-id="1daa6-183">*包括静态脚本文件结构*</span><span class="sxs-lookup"><span data-stu-id="1daa6-183">*Including a Static Script File Structure*</span></span>

<span data-ttu-id="1daa6-184">当使用静态脚本文件进行部署，您会失去一些使用固有的.NET 本地化方案的好处。</span><span class="sxs-lookup"><span data-stu-id="1daa6-184">When using static script files for deployment, you lose some of the benefits of using the inherent .NET localization scheme.</span></span> <span data-ttu-id="1daa6-185">主要可见，则是你将失去包括脚本资源文件; 从生成的自动类型在上面的演练，例如，资源已公开由称为消息从 ScriptManager 控件自动生成类型。</span><span class="sxs-lookup"><span data-stu-id="1daa6-185">Primarily visible is that you lose the automatic type generated from including script resource files; in the above walkthrough, for example, resources were exposed by an automatically-generated type called Message from the ScriptManager control.</span></span>

<span data-ttu-id="1daa6-186">有，但是，到使用静态脚本文件结构的一些好处。</span><span class="sxs-lookup"><span data-stu-id="1daa6-186">There are, however, some benefits to using a static script file structure.</span></span> <span data-ttu-id="1daa6-187">可以执行更新而无需重新编译和重新部署附属程序集，并使用静态文件结构也可以重写嵌入的脚本，以将一次要项可能尚未装运的功能与组件相集成。</span><span class="sxs-lookup"><span data-stu-id="1daa6-187">Updates can be performed without recompiling and redeploying satellite assemblies, and the use of a static file structure can also be done to override embedded script, to integrate a minor piece of functionality that may not have been shipped with a component.</span></span>

<span data-ttu-id="1daa6-188">Microsoft 建议避免通过自动在项目编译期间生成的脚本资源的版本控制问题。</span><span class="sxs-lookup"><span data-stu-id="1daa6-188">Microsoft recommends avoiding a version control issue by automatically generating your script resources during project compilation.</span></span> <span data-ttu-id="1daa6-189">维护大量的脚本代码基，它会变为越来越困难，以确保代码更改会反映在每个本地化的脚本。</span><span class="sxs-lookup"><span data-stu-id="1daa6-189">When maintaining an extensive script code base, it can become increasingly difficult to ensure that code changes are reflected in each localized script.</span></span> <span data-ttu-id="1daa6-190">或者，您可以只需维护一个逻辑脚本和多个本地化脚本，生成项目的同时合并文件。</span><span class="sxs-lookup"><span data-stu-id="1daa6-190">As an alternative, you can simply maintain one logic script and multiple localization scripts, merging the files while building the project.</span></span>

<span data-ttu-id="1daa6-191">由于不是以声明方式包含的资源，应包含文件的静态脚本引用通过添加`<asp:ScriptElement>`元素作为子级`<Scripts>`标记的 ScriptManager 控件，或以编程方式添加`ScriptReference`对象向`Scripts`属性的`ScriptManager`在运行时页面上的控件。</span><span class="sxs-lookup"><span data-stu-id="1daa6-191">Because there are not resources to declaratively include, static script files should be referenced either by adding `<asp:ScriptElement>` elements as a child of the `<Scripts>` tag of the ScriptManager control, or by programmatically adding `ScriptReference` objects to the `Scripts` property of the `ScriptManager` control on the page at runtime.</span></span>

## <a name="the-scriptmanager-and-its-role-in-localization"></a><span data-ttu-id="1daa6-192">*ScriptManager 和本地化中的其角色*</span><span class="sxs-lookup"><span data-stu-id="1daa6-192">*The ScriptManager and its Role in Localization*</span></span>

<span data-ttu-id="1daa6-193">ScriptManager 使本地化的应用程序的多个自动行为：</span><span class="sxs-lookup"><span data-stu-id="1daa6-193">The ScriptManager enables several automatic behaviors for localized applications:</span></span>

- <span data-ttu-id="1daa6-194">它会自动查找基于设置和命名约定; 的脚本文件例如，它将加载在调试模式下，启用了调试的脚本，并加载本地化基于浏览器的用户界面选择的脚本。</span><span class="sxs-lookup"><span data-stu-id="1daa6-194">It automatically locates script files based on settings and naming conventions; for instance, it loads debug-enabled scripts when in debugging mode, and loads localized scripts based on the browser's user interface selection.</span></span>
- <span data-ttu-id="1daa6-195">它使您能够定义包括自定义区域性的区域性。</span><span class="sxs-lookup"><span data-stu-id="1daa6-195">It enables the definition of cultures, including custom cultures.</span></span>
- <span data-ttu-id="1daa6-196">它支持通过 HTTP 的脚本文件的压缩。</span><span class="sxs-lookup"><span data-stu-id="1daa6-196">It enables the compression of script files over HTTP.</span></span>
- <span data-ttu-id="1daa6-197">它将缓存脚本来有效地管理多个请求。</span><span class="sxs-lookup"><span data-stu-id="1daa6-197">It caches scripts to efficiently manage many requests.</span></span>
- <span data-ttu-id="1daa6-198">它将一个间接层添加到脚本中，其通过管道通过加密的 URL。</span><span class="sxs-lookup"><span data-stu-id="1daa6-198">It adds a layer of indirection to scripts by piping them through an encrypted URL.</span></span>

<span data-ttu-id="1daa6-199">可以将脚本引用添加到 ScriptManager 控件，通过编程方式或声明性标记。</span><span class="sxs-lookup"><span data-stu-id="1daa6-199">Script references can be added to the ScriptManager control either programmatically or by declarative markup.</span></span> <span data-ttu-id="1daa6-200">声明性标记时，尤其是使用脚本中嵌入的程序集，而不是网站项目本身，如脚本的名称可能不会更改如修订推送。</span><span class="sxs-lookup"><span data-stu-id="1daa6-200">Declarative markup is particularly useful when working with scripts embedded in assemblies other than the web site project itself, as the name of the script will likely not change as revisions are pushed through.</span></span>

## <a name="summary"></a><span data-ttu-id="1daa6-201">总结</span><span class="sxs-lookup"><span data-stu-id="1daa6-201">Summary</span></span>

<span data-ttu-id="1daa6-202">随着 web 应用程序扩大受众更大，需要能够访问更广泛的区域性和社区将成为核心的业务模型;电子商务 web 应用程序需要能够处理外币，内容管理系统要求是其内容，但还其导航提示和其他语言和公司中的窗体字段需要知道这种需求不仅能存在可访问。</span><span class="sxs-lookup"><span data-stu-id="1daa6-202">As web applications grow to reach a larger audience, the need to be able to reach broader cultures and communities becomes core to a business model; e-commerce web applications need to be able to deal with foreign currencies, content management systems need to be able to not only present their content but also their navigation hints and form fields in other languages, and companies need to know that this need is accessible.</span></span>

<span data-ttu-id="1daa6-203">.NET Framework 本质上支持的丰富本地化框架，利用附属程序集和 XML 资源 (.resx) 文件以提供统一的方法来查找资源字符串和图像。</span><span class="sxs-lookup"><span data-stu-id="1daa6-203">The .NET Framework intrinsically supports a rich localization framework, utilizing satellite assemblies and XML resource (.resx) files to present a uniform way to look up resource strings and images.</span></span> <span data-ttu-id="1daa6-204">ASP.NET AJAX 扩展，其中包括 Microsoft AJAX Framework 和 Microsoft AJAX 脚本库中，为提供支持这一编程模型到客户端代码中，启用简单的资源字符串查找。</span><span class="sxs-lookup"><span data-stu-id="1daa6-204">The ASP.NET AJAX Extensions, including the Microsoft AJAX Framework and Microsoft AJAX Script Library, provide support for this programming model into client-side code, enabling easy resource string lookups.</span></span> <span data-ttu-id="1daa6-205">只要文件名遵循给定的命名方案，附属程序集支持自动包含通过 ScriptResource.axd 脚本资源 （实际的.js 文件）。</span><span class="sxs-lookup"><span data-stu-id="1daa6-205">Satellite assemblies support the automatic inclusion of script resources (actual .js files) through ScriptResource.axd as long as the filenames follow a given naming scheme.</span></span> <span data-ttu-id="1daa6-206">利用此支持，ASP.NET AJAX Extensions 简化脚本的本地化和全球化应用程序。</span><span class="sxs-lookup"><span data-stu-id="1daa6-206">With this support, the ASP.NET AJAX Extensions simplify the localization of scripts and the globalization of applications.</span></span>

## <a name="bio"></a><span data-ttu-id="1daa6-207">*个人简介*</span><span class="sxs-lookup"><span data-stu-id="1daa6-207">*Bio*</span></span>

<span data-ttu-id="1daa6-208">Scott Cate 自 1997 年以来一直致力于 Microsoft Web 技术和 myKB.com 总裁 ([www.myKB.com](http://www.myKB.com)) 专门负责编写 ASP.NET 基于侧重于知识库软件解决方案的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1daa6-208">Scott Cate has been working with Microsoft Web technologies since 1997 and is the President of myKB.com ([www.myKB.com](http://www.myKB.com)) where he specializes in writing ASP.NET based applications focused on Knowledge Base Software solutions.</span></span> <span data-ttu-id="1daa6-209">可以通过电子邮件联系 Scott [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com)或他的博客[ScottCate.com](http://ScottCate.com)</span><span class="sxs-lookup"><span data-stu-id="1daa6-209">Scott can be contacted via email at [scott.cate@myKB.com](mailto:scott.cate@myKB.com) or his blog at [ScottCate.com](http://ScottCate.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1daa6-210">[上一页](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
> [下一页](understanding-asp-net-ajax-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="1daa6-210">[Previous](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
[Next](understanding-asp-net-ajax-web-services.md)</span></span>
