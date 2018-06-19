---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 页模型 |Microsoft 文档
author: microsoft
description: 在 ASP.NET 中 1.x，开发人员必须内联代码模型与代码隐藏代码模型之间选择。 无法使用任一 Src attr 实现代码隐藏...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: fda85ec03f845cafa7720382bf85652937932c44
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30891290"
---
<a name="the-aspnet-20-page-model"></a><span data-ttu-id="66f5e-104">ASP.NET 2.0 页模型</span><span class="sxs-lookup"><span data-stu-id="66f5e-104">The ASP.NET 2.0 Page Model</span></span>
====================
<span data-ttu-id="66f5e-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="66f5e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="66f5e-106">在 ASP.NET 中 1.x，开发人员必须内联代码模型与代码隐藏代码模型之间选择。</span><span class="sxs-lookup"><span data-stu-id="66f5e-106">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="66f5e-107">无法使用 Src 属性或的代码隐藏文件属性来实现代码隐藏@Page指令。</span><span class="sxs-lookup"><span data-stu-id="66f5e-107">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="66f5e-108">在 ASP.NET 2.0 中，开发人员仍之间进行选择内联代码和代码隐藏，但已对代码隐藏模型的重大增强功能。</span><span class="sxs-lookup"><span data-stu-id="66f5e-108">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>


<span data-ttu-id="66f5e-109">在 ASP.NET 中 1.x，开发人员必须内联代码模型与代码隐藏代码模型之间选择。</span><span class="sxs-lookup"><span data-stu-id="66f5e-109">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="66f5e-110">无法使用 Src 属性或的代码隐藏文件属性来实现代码隐藏@Page指令。</span><span class="sxs-lookup"><span data-stu-id="66f5e-110">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="66f5e-111">在 ASP.NET 2.0 中，开发人员仍之间进行选择内联代码和代码隐藏，但已对代码隐藏模型的重大增强功能。</span><span class="sxs-lookup"><span data-stu-id="66f5e-111">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

## <a name="improvements-in-the-code-behind-model"></a><span data-ttu-id="66f5e-112">代码隐藏模型中的改进</span><span class="sxs-lookup"><span data-stu-id="66f5e-112">Improvements in the Code-Behind Model</span></span>

<span data-ttu-id="66f5e-113">若要完全了解在 ASP.NET 2.0 中的代码隐藏模型中的更改，其最大努力快速查看模型存在于 ASP.NET 1.x。</span><span class="sxs-lookup"><span data-stu-id="66f5e-113">In order to fully understand the changes in the code-behind model in ASP.NET 2.0, its best to quickly review the model as it existed in ASP.NET 1.x.</span></span>

## <a name="the-code-behind-model-in-aspnet-1x"></a><span data-ttu-id="66f5e-114">在 ASP.NET 中的代码隐藏模型 1.x</span><span class="sxs-lookup"><span data-stu-id="66f5e-114">The Code-Behind Model in ASP.NET 1.x</span></span>

<span data-ttu-id="66f5e-115">在 ASP.NET 中 1.x，代码隐藏模型包含个的 ASPX 文件 （该 web 窗体） 和包含程序代码的代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-115">In ASP.NET 1.x, the code-behind model consisted of an ASPX file (the Webform) and a code-behind file containing programming code.</span></span> <span data-ttu-id="66f5e-116">两个文件连接使用@Page指令 ASPX 文件中。</span><span class="sxs-lookup"><span data-stu-id="66f5e-116">The two files were connected using the @Page directive in the ASPX file.</span></span> <span data-ttu-id="66f5e-117">ASPX 页上的每个控件具有相应声明的代码隐藏文件中为实例变量。</span><span class="sxs-lookup"><span data-stu-id="66f5e-117">Each control on the ASPX page had a corresponding declaration in the code-behind file as an instance variable.</span></span> <span data-ttu-id="66f5e-118">代码隐藏文件还包含事件绑定的代码，并生成必需的 Visual Studio 设计器代码。</span><span class="sxs-lookup"><span data-stu-id="66f5e-118">The code-behind file also contained code for event binding and generated code necessary for the Visual Studio designer.</span></span> <span data-ttu-id="66f5e-119">此模型效果相当不错，但因为 ASPX 页中的每个 ASP.NET 元素所需的代码隐藏文件中的相应代码，没有代码和内容没有真正分离。</span><span class="sxs-lookup"><span data-stu-id="66f5e-119">This model worked fairly well, but because every ASP.NET element in the ASPX page required corresponding code in the code-behind file, there was no true separation of code and content.</span></span> <span data-ttu-id="66f5e-120">例如，如果设计器添加到 Visual Studio IDE 之外的 ASPX 文件新的服务器控件，该应用程序将会破坏由于缺少该控件的声明，因此在代码隐藏文件中。</span><span class="sxs-lookup"><span data-stu-id="66f5e-120">For example, if a designer added a new server control to an ASPX file outside of the Visual Studio IDE, the application would break due to the absence of a declaration for that control in the code-behind file.</span></span>

## <a name="the-code-behind-model-in-aspnet-20"></a><span data-ttu-id="66f5e-121">ASP.NET 2.0 中的代码隐藏模型</span><span class="sxs-lookup"><span data-stu-id="66f5e-121">The Code-Behind Model in ASP.NET 2.0</span></span>

<span data-ttu-id="66f5e-122">ASP.NET 2.0 大大改进了此模型。</span><span class="sxs-lookup"><span data-stu-id="66f5e-122">ASP.NET 2.0 greatly improves upon this model.</span></span> <span data-ttu-id="66f5e-123">在 ASP.NET 2.0 中，代码隐藏实现使用新*分部类*ASP.NET 2.0 中提供。</span><span class="sxs-lookup"><span data-stu-id="66f5e-123">In ASP.NET 2.0, code-behind is implemented using the new *partial classes* provided in ASP.NET 2.0.</span></span> <span data-ttu-id="66f5e-124">在 ASP.NET 2.0 中的代码隐藏类是定义为分部类，这意味着它包含仅的类定义的一部分。</span><span class="sxs-lookup"><span data-stu-id="66f5e-124">The code-behind class in ASP.NET 2.0 is definied as a partial class meaning that it contains only part of the class definition.</span></span> <span data-ttu-id="66f5e-125">使用 ASPX 页，在运行时或在预编译网站的 ASP.NET 2.0 动态生成的类定义的其余部分。</span><span class="sxs-lookup"><span data-stu-id="66f5e-125">The remaining part of the class definition is dynamically generated by ASP.NET 2.0 using the ASPX page at runtime or when the Web site is precompiled.</span></span> <span data-ttu-id="66f5e-126">代码隐藏文件和 ASPX 页面之间的链接则仍会建立使用 @ Page 指令。</span><span class="sxs-lookup"><span data-stu-id="66f5e-126">The link between the code-behind file and the ASPX page is still established using the @ Page directive.</span></span> <span data-ttu-id="66f5e-127">但是，而不是一个代码隐藏或 Src 特性中，ASP.NET 2.0 现在使用同属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-127">However, instead of a CodeBehind or Src attribute, ASP.NET 2.0 now uses the CodeFile attribute.</span></span> <span data-ttu-id="66f5e-128">Inherits 特性也用于指定页的类名称。</span><span class="sxs-lookup"><span data-stu-id="66f5e-128">The Inherits attribute is also used to specify the class name for the page.</span></span>

<span data-ttu-id="66f5e-129">典型的 @ Page 指令可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="66f5e-129">A typical @ Page directive might look like this:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

<span data-ttu-id="66f5e-130">ASP.NET 2.0 代码隐藏文件中的典型类定义可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="66f5e-130">A typical class definition in an ASP.NET 2.0 code-behind file might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="66f5e-131">C# 和 Visual Basic 是唯一的托管的语言当前支持分部类。</span><span class="sxs-lookup"><span data-stu-id="66f5e-131">C# and Visual Basic are the only managed languages that currently support partial classes.</span></span> <span data-ttu-id="66f5e-132">因此，使用 J# 开发人员将不能在 ASP.NET 2.0 中使用代码隐藏模型。</span><span class="sxs-lookup"><span data-stu-id="66f5e-132">Therefore, developers using J# will not be able to use the code-behind model in ASP.NET 2.0.</span></span>


<span data-ttu-id="66f5e-133">新模型可增强代码隐藏模型，因为开发人员现在将具有包含他们创建的代码的代码文件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-133">The new model enhances the code-behind model because developers will now have code files that contain only the code that they have created.</span></span> <span data-ttu-id="66f5e-134">它还提供的代码和内容 true 分离因为有代码隐藏文件中的没有实例变量声明。</span><span class="sxs-lookup"><span data-stu-id="66f5e-134">It also provides for a true separation of code and content because there are no instance variable declarations in the code-behind file.</span></span>

> [!NOTE]
> <span data-ttu-id="66f5e-135">ASPX 页的分部类是事件绑定发生，因为 Visual Basic 开发人员可以使用代码隐藏文件中的句柄关键字将事件绑定实现略微的性能增加。</span><span class="sxs-lookup"><span data-stu-id="66f5e-135">Because the partial class for the ASPX page is where event binding takes place, Visual Basic developers can realize a slight performance increase by using the Handles keyword in code-behind to bind events.</span></span> <span data-ttu-id="66f5e-136">C# 包含没有等效的关键字。</span><span class="sxs-lookup"><span data-stu-id="66f5e-136">C# has no equivalent keyword.</span></span>


## <a name="new--page-directive-attributes"></a><span data-ttu-id="66f5e-137">新的 @ 页面指令属性</span><span class="sxs-lookup"><span data-stu-id="66f5e-137">New @ Page Directive Attributes</span></span>

<span data-ttu-id="66f5e-138">ASP.NET 2.0 将许多新特性添加到 @ Page 指令。</span><span class="sxs-lookup"><span data-stu-id="66f5e-138">ASP.NET 2.0 adds many new attributes to the @ Page directive.</span></span> <span data-ttu-id="66f5e-139">以下属性是 ASP.NET 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="66f5e-139">The following attributes are new in ASP.NET 2.0.</span></span>

## <a name="async"></a><span data-ttu-id="66f5e-140">Async</span><span class="sxs-lookup"><span data-stu-id="66f5e-140">Async</span></span>

<span data-ttu-id="66f5e-141">异步属性，可配置页后，可以以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="66f5e-141">The Async attribute allows you to configure page to be executed asynchronously.</span></span> <span data-ttu-id="66f5e-142">也包括此模块的更高版本中的异步页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-142">Well cover asynchronous pages later in this module.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="66f5e-143">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="66f5e-143">AsyncTimeout</span></span>

<span data-ttu-id="66f5e-144">指定异步页的超时值。</span><span class="sxs-lookup"><span data-stu-id="66f5e-144">Specified the timeout for asynchronous pages.</span></span> <span data-ttu-id="66f5e-145">默认值为 45 秒。</span><span class="sxs-lookup"><span data-stu-id="66f5e-145">The default is 45 seconds.</span></span>

## <a name="codefile"></a><span data-ttu-id="66f5e-146">CodeFile</span><span class="sxs-lookup"><span data-stu-id="66f5e-146">CodeFile</span></span>

<span data-ttu-id="66f5e-147">同属性是对 Visual Studio 2002/2003 中的代码隐藏属性替代。</span><span class="sxs-lookup"><span data-stu-id="66f5e-147">The CodeFile attribute is the replacement for the CodeBehind attribute in Visual Studio 2002/2003.</span></span>

### <a name="codefilebaseclass"></a><span data-ttu-id="66f5e-148">CodeFileBaseClass</span><span class="sxs-lookup"><span data-stu-id="66f5e-148">CodeFileBaseClass</span></span>

<span data-ttu-id="66f5e-149">在要从单个基类派生的多个页的情况下使用 CodeFileBaseClass 属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-149">The CodeFileBaseClass attribute is used in cases where you want multiple pages to derive from a single base class.</span></span> <span data-ttu-id="66f5e-150">由于在 ASP.NET 中，如果没有此特性的分部类的实现使用共享的公共字段来引用在 ASPX 页面中声明的控件的基类将不正常工作，因为 ASP。网编译引擎将自动创建基于页中的控件的新成员。</span><span class="sxs-lookup"><span data-stu-id="66f5e-150">Because of the implementation of partial classes in ASP.NET, without this attribute, a base class that uses shared common fields to reference controls declared in an ASPX page would not work properly because ASP.NETs compilation engine will automatically create new members based on controls in the page.</span></span> <span data-ttu-id="66f5e-151">因此，如果你需要一个公共基类在 ASP.NET 中的两个或多个页面，你将需要定义 CodeFileBaseClass 属性中指定基类，然后是每个页类派生自该基类。</span><span class="sxs-lookup"><span data-stu-id="66f5e-151">Therefore, if you want a common base class for two or more pages in ASP.NET, you will need to define specify your base class in the CodeFileBaseClass attribute and then derive each pages class from that base class.</span></span> <span data-ttu-id="66f5e-152">使用此特性时，则也需要同属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-152">The CodeFile attribute is also required when this attribute is used.</span></span>

## <a name="compilationmode"></a><span data-ttu-id="66f5e-153">CompilationMode</span><span class="sxs-lookup"><span data-stu-id="66f5e-153">CompilationMode</span></span>

<span data-ttu-id="66f5e-154">此属性允许你设置的 ASPX 页 CompilationMode 属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-154">This attribute allows you to set the CompilationMode property of the ASPX page.</span></span> <span data-ttu-id="66f5e-155">CompilationMode 属性是一个包含的值的枚举**始终**，**自动**，和**从不**。</span><span class="sxs-lookup"><span data-stu-id="66f5e-155">The CompilationMode property is an enumeration containing the values **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="66f5e-156">默认值是**始终**。</span><span class="sxs-lookup"><span data-stu-id="66f5e-156">The default is **Always**.</span></span> <span data-ttu-id="66f5e-157">**自动**设置将阻止 ASP.NET 动态尽可能编译页面。</span><span class="sxs-lookup"><span data-stu-id="66f5e-157">The **Auto** setting will prevent ASP.NET from dynamically compiling the page if possible.</span></span> <span data-ttu-id="66f5e-158">从动态编译排除页提高性能。</span><span class="sxs-lookup"><span data-stu-id="66f5e-158">Excluding pages from dynamic compilation increases performance.</span></span> <span data-ttu-id="66f5e-159">但是，如果不对此页包含必须编译该代码，将引发错误时浏览页面。</span><span class="sxs-lookup"><span data-stu-id="66f5e-159">However, if a page that is excluded contains that code that must be compiled, an error will be thrown when the page is browsed.</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="66f5e-160">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="66f5e-160">EnableEventValidation</span></span>

<span data-ttu-id="66f5e-161">此属性指定验证回发和回调事件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-161">This attribute specifies whether or not postback and callback events are validated.</span></span> <span data-ttu-id="66f5e-162">启用后，自变量以回发或回调事件会检查以确保它们源自最初呈现这些服务器控件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-162">When this is enabled, arguments to postback or callback events are checked to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="66f5e-163">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="66f5e-163">EnableTheming</span></span>

<span data-ttu-id="66f5e-164">此属性指定在页面上使用了 ASP.NET 主题。</span><span class="sxs-lookup"><span data-stu-id="66f5e-164">This attribute specifies whether or not ASP.NET themes are used on a page.</span></span> <span data-ttu-id="66f5e-165">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="66f5e-165">The default is **false**.</span></span> <span data-ttu-id="66f5e-166">中介绍了 ASP.NET 主题[模块 10](profiles-themes-and-web-parts.md)。</span><span class="sxs-lookup"><span data-stu-id="66f5e-166">ASP.NET themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="linepragmas"></a><span data-ttu-id="66f5e-167">LinePragmas</span><span class="sxs-lookup"><span data-stu-id="66f5e-167">LinePragmas</span></span>

<span data-ttu-id="66f5e-168">此属性指定是否应在编译过程中添加行杂注。</span><span class="sxs-lookup"><span data-stu-id="66f5e-168">This attribute specifies whether line pragmas should be added during compilation.</span></span> <span data-ttu-id="66f5e-169">行杂注是调试器用于标记代码的特定部分的选项。</span><span class="sxs-lookup"><span data-stu-id="66f5e-169">Line pragmas are options used by debuggers to mark specific sections of code.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="66f5e-170">MaintainScrollPositionOnPostback</span><span class="sxs-lookup"><span data-stu-id="66f5e-170">MaintainScrollPositionOnPostback</span></span>

<span data-ttu-id="66f5e-171">此属性指定 JavaScript 注入到页以便保持之间回发的滚动位置。</span><span class="sxs-lookup"><span data-stu-id="66f5e-171">This attribute specifies whether or not JavaScript is injected into the page in order to maintain scroll position between postbacks.</span></span> <span data-ttu-id="66f5e-172">此属性是**false**默认情况下。</span><span class="sxs-lookup"><span data-stu-id="66f5e-172">This attribute is **false** by default.</span></span>

<span data-ttu-id="66f5e-173">此属性时**true**，ASP.NET 将添加&lt;脚本&gt;块在回发时，如下所示：</span><span class="sxs-lookup"><span data-stu-id="66f5e-173">When this attribute is **true**, ASP.NET will add a &lt;script&gt; block on postback that looks like this:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

<span data-ttu-id="66f5e-174">请注意，此脚本块 src WebResource.axd。</span><span class="sxs-lookup"><span data-stu-id="66f5e-174">Note that the src for this script block is WebResource.axd.</span></span> <span data-ttu-id="66f5e-175">此资源不是物理路径。</span><span class="sxs-lookup"><span data-stu-id="66f5e-175">This resource is not a physical path.</span></span> <span data-ttu-id="66f5e-176">当请求此脚本时，ASP.NET 将动态生成脚本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-176">When this script is requested, ASP.NET dynamically builds the script.</span></span>

### <a name="masterpagefile"></a><span data-ttu-id="66f5e-177">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="66f5e-177">MasterPageFile</span></span>

<span data-ttu-id="66f5e-178">此属性指定当前页的主控页文件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-178">This attribute specifies the master page file for the current page.</span></span> <span data-ttu-id="66f5e-179">路径可以是相对或绝对。</span><span class="sxs-lookup"><span data-stu-id="66f5e-179">The path can be relative or absolute.</span></span> <span data-ttu-id="66f5e-180">中介绍了母版页[模块 4](master-pages.md)。</span><span class="sxs-lookup"><span data-stu-id="66f5e-180">Master pages are covered in [Module 4](master-pages.md).</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="66f5e-181">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="66f5e-181">StyleSheetTheme</span></span>

<span data-ttu-id="66f5e-182">此属性允许你重写由 ASP.NET 2.0 主题定义的用户界面外观属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-182">This attribute allows you to override user-interface appearance properties defined by an ASP.NET 2.0 theme.</span></span> <span data-ttu-id="66f5e-183">主题中介绍了[模块 10](profiles-themes-and-web-parts.md)。</span><span class="sxs-lookup"><span data-stu-id="66f5e-183">Themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="theme"></a><span data-ttu-id="66f5e-184">主题</span><span class="sxs-lookup"><span data-stu-id="66f5e-184">Theme</span></span>

<span data-ttu-id="66f5e-185">指定的页面主题。</span><span class="sxs-lookup"><span data-stu-id="66f5e-185">Specifies the theme for the page.</span></span> <span data-ttu-id="66f5e-186">如果没有为 StyleSheetTheme 属性指定一个值，主题属性将替代应用于这些控件在页上的所有样式。</span><span class="sxs-lookup"><span data-stu-id="66f5e-186">If a value is not specified for the StyleSheetTheme attribute, the Theme attribute overrides all styles applied to controls on the page.</span></span>

## <a name="title"></a><span data-ttu-id="66f5e-187">标题</span><span class="sxs-lookup"><span data-stu-id="66f5e-187">Title</span></span>

<span data-ttu-id="66f5e-188">设置页的标题。</span><span class="sxs-lookup"><span data-stu-id="66f5e-188">Sets the title for the page.</span></span> <span data-ttu-id="66f5e-189">此处指定的值将出现在&lt;标题&gt;呈现页面上的元素。</span><span class="sxs-lookup"><span data-stu-id="66f5e-189">The value specified here will appear in the &lt;title&gt; element of the rendered page.</span></span>

### <a name="viewstateencryptionmode"></a><span data-ttu-id="66f5e-190">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="66f5e-190">ViewStateEncryptionMode</span></span>

<span data-ttu-id="66f5e-191">设置 ViewStateEncryptionMode 枚举的值。</span><span class="sxs-lookup"><span data-stu-id="66f5e-191">Sets the value for the ViewStateEncryptionMode enumeration.</span></span> <span data-ttu-id="66f5e-192">可用值有**始终**，**自动**，和**从不**。</span><span class="sxs-lookup"><span data-stu-id="66f5e-192">The available values are **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="66f5e-193">默认值是**自动**。当此属性设置为值为**自动**，加密视图状态是一个请求，则通过调用**RegisterRequiresViewStateEncryption**方法。</span><span class="sxs-lookup"><span data-stu-id="66f5e-193">The default value is **Auto**. When this attribute is set to a value of **Auto**, viewstate is encrypted is a control requests it by calling the **RegisterRequiresViewStateEncryption** method.</span></span>

## <a name="setting-public-property-values-via-the--page-directive"></a><span data-ttu-id="66f5e-194">设置公共属性的值通过 @ 页指令</span><span class="sxs-lookup"><span data-stu-id="66f5e-194">Setting Public Property Values via the @ Page Directive</span></span>

<span data-ttu-id="66f5e-195">ASP.NET 2.0 中的 @ Page 指令的另一个新功能是能够设置基类的公共属性的初始值。</span><span class="sxs-lookup"><span data-stu-id="66f5e-195">Another new capability of the @ Page directive in ASP.NET 2.0 is the ability to set the initial value of public properties of a base class.</span></span> <span data-ttu-id="66f5e-196">假设，例如，你具有的公共属性调用**SomeText**在您的基类和你意愿它，以初始化为**Hello**加载页时。</span><span class="sxs-lookup"><span data-stu-id="66f5e-196">Suppose, for example, that you have a public property called **SomeText** in your base class and you d like it to be initialized to **Hello** when a page is loaded.</span></span> <span data-ttu-id="66f5e-197">你可以完成此操作通过只需在 @ Page 指令中设置的值如下所示：</span><span class="sxs-lookup"><span data-stu-id="66f5e-197">You can accomplish this by simply setting the value in the @ Page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

<span data-ttu-id="66f5e-198">**SomeText** @ Page 指令的特性到基类中设置 SomeText 属性的初始值*Hello ！*。</span><span class="sxs-lookup"><span data-stu-id="66f5e-198">The **SomeText** attribute of the @ Page directive sets the initial value of the SomeText property in the base class to *Hello!*.</span></span> <span data-ttu-id="66f5e-199">下面的视频是基类使用 @ 页面指令中设置的公共属性的初始值的演练。</span><span class="sxs-lookup"><span data-stu-id="66f5e-199">The video below is a walkthrough of setting the initial value of a public property in a base class using the @ Page directive.</span></span>


![](the-asp-net-2-0-page-model/_static/image1.png)


[<span data-ttu-id="66f5e-200">打开全屏幕视频</span><span class="sxs-lookup"><span data-stu-id="66f5e-200">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/setprop1.wmv)


## <a name="new-public-properties-of-the-page-class"></a><span data-ttu-id="66f5e-201">页类的新公共属性</span><span class="sxs-lookup"><span data-stu-id="66f5e-201">New Public Properties of the Page Class</span></span>

<span data-ttu-id="66f5e-202">以下公共属性是 ASP.NET 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="66f5e-202">The following public properties are new in ASP.NET 2.0.</span></span>

## <a name="apprelativetemplatesourcedirectory"></a><span data-ttu-id="66f5e-203">AppRelativeTemplateSourceDirectory</span><span class="sxs-lookup"><span data-stu-id="66f5e-203">AppRelativeTemplateSourceDirectory</span></span>

<span data-ttu-id="66f5e-204">返回的页面或控件的相对于应用程序路径。</span><span class="sxs-lookup"><span data-stu-id="66f5e-204">Returns the application-relative path to the page or control.</span></span> <span data-ttu-id="66f5e-205">例如，对于在位于页的页http://app/folder/page.aspx，该属性返回 ~ / 文件夹 /。</span><span class="sxs-lookup"><span data-stu-id="66f5e-205">For example, for a page located at http://app/folder/page.aspx, the property returns ~/folder/.</span></span>

## <a name="apprelativevirtualpath"></a><span data-ttu-id="66f5e-206">AppRelativeVirtualPath</span><span class="sxs-lookup"><span data-stu-id="66f5e-206">AppRelativeVirtualPath</span></span>

<span data-ttu-id="66f5e-207">返回的页面或控件的相对虚拟目录路径。</span><span class="sxs-lookup"><span data-stu-id="66f5e-207">Returns the relative virtual directory path to the page or control.</span></span> <span data-ttu-id="66f5e-208">例如对于在位于页的页http://app/folder/page.aspx，该属性返回 ~ / folder/page.aspx。</span><span class="sxs-lookup"><span data-stu-id="66f5e-208">For example for a page located at http://app/folder/page.aspx, the property returns ~/folder/page.aspx.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="66f5e-209">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="66f5e-209">AsyncTimeout</span></span>

<span data-ttu-id="66f5e-210">获取或设置用于异步页处理的超时值。</span><span class="sxs-lookup"><span data-stu-id="66f5e-210">Gets or sets the timeout used for asynchronous page handling.</span></span> <span data-ttu-id="66f5e-211">（异步页将在后面进行介绍此模块。）</span><span class="sxs-lookup"><span data-stu-id="66f5e-211">(Asynchronous pages will be covered later in this module.)</span></span>

## <a name="clientquerystring"></a><span data-ttu-id="66f5e-212">ClientQueryString</span><span class="sxs-lookup"><span data-stu-id="66f5e-212">ClientQueryString</span></span>

<span data-ttu-id="66f5e-213">返回所请求 URL 的查询字符串部分的只读属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-213">A read-only property that returns the query string portion of the requested URL.</span></span> <span data-ttu-id="66f5e-214">此值是 URL 编码。</span><span class="sxs-lookup"><span data-stu-id="66f5e-214">This value is URL encoded.</span></span> <span data-ttu-id="66f5e-215">HttpServerUtility 类的 UrlDecode 方法可用于对其进行解码。</span><span class="sxs-lookup"><span data-stu-id="66f5e-215">You can use the UrlDecode method of the HttpServerUtility class to decode it.</span></span>

## <a name="clientscript"></a><span data-ttu-id="66f5e-216">ClientScript</span><span class="sxs-lookup"><span data-stu-id="66f5e-216">ClientScript</span></span>

<span data-ttu-id="66f5e-217">此属性返回可以用于管理的客户端脚本的 ASP.NETs 发出 ClientScriptManager 对象。</span><span class="sxs-lookup"><span data-stu-id="66f5e-217">This property returns a ClientScriptManager object that can be used to manage ASP.NETs emission of client-side script.</span></span> <span data-ttu-id="66f5e-218">（ClientScriptManager 类介绍此模块中的更高版本中）。</span><span class="sxs-lookup"><span data-stu-id="66f5e-218">(The ClientScriptManager class is covered later in this module.)</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="66f5e-219">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="66f5e-219">EnableEventValidation</span></span>

<span data-ttu-id="66f5e-220">此属性控制启用事件验证回发和回调事件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-220">This property controls whether or not event validation is enabled for postback and callback events.</span></span> <span data-ttu-id="66f5e-221">启用时，自变量以回发或回调事件进行验证以确保它们源自最初呈现这些服务器控件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-221">When enabled, arguments to postback or callback events are verified to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="66f5e-222">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="66f5e-222">EnableTheming</span></span>

<span data-ttu-id="66f5e-223">此属性获取或设置一个布尔值，指定将 ASP.NET 2.0 主题应用到页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-223">This property gets or sets a Boolean that specifies whether or not an ASP.NET 2.0 theme applies to the page.</span></span>

## <a name="form"></a><span data-ttu-id="66f5e-224">窗体</span><span class="sxs-lookup"><span data-stu-id="66f5e-224">Form</span></span>

<span data-ttu-id="66f5e-225">此属性为 HtmlForm 对象返回 ASPX 页上的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="66f5e-225">This property returns the HTML form on the ASPX page as an HtmlForm object.</span></span>

## <a name="header"></a><span data-ttu-id="66f5e-226">Header</span><span class="sxs-lookup"><span data-stu-id="66f5e-226">Header</span></span>

<span data-ttu-id="66f5e-227">此属性返回对包含页眉的 HtmlHead 对象的引用。</span><span class="sxs-lookup"><span data-stu-id="66f5e-227">This property returns a reference to an HtmlHead object that contains the page header.</span></span> <span data-ttu-id="66f5e-228">可以使用返回的 HtmlHead 对象用于获取/设置样式表、 元标记，等等。</span><span class="sxs-lookup"><span data-stu-id="66f5e-228">You can use the returned HtmlHead object to get/set style sheets, Meta tags, etc.</span></span>

## <a name="idseparator"></a><span data-ttu-id="66f5e-229">IdSeparator</span><span class="sxs-lookup"><span data-stu-id="66f5e-229">IdSeparator</span></span>

<span data-ttu-id="66f5e-230">此只读属性获取用于分隔控件标识符，当 ASP.NET 生成页面上的控件的唯一 ID 的字符。</span><span class="sxs-lookup"><span data-stu-id="66f5e-230">This read-only property gets the character that is used to separate control identifiers when ASP.NET is building a unique ID for controls on a page.</span></span> <span data-ttu-id="66f5e-231">它不可直接通过代码使用。</span><span class="sxs-lookup"><span data-stu-id="66f5e-231">It is not intended to be used directly from your code.</span></span>

## <a name="isasync"></a><span data-ttu-id="66f5e-232">IsAsync</span><span class="sxs-lookup"><span data-stu-id="66f5e-232">IsAsync</span></span>

<span data-ttu-id="66f5e-233">此属性允许异步页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-233">This property allows for asynchronous pages.</span></span> <span data-ttu-id="66f5e-234">在此模块的后面部分讨论了异步页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-234">Asynchronous pages are discussed later in this module.</span></span>

## <a name="iscallback"></a><span data-ttu-id="66f5e-235">IsCallback</span><span class="sxs-lookup"><span data-stu-id="66f5e-235">IsCallback</span></span>

<span data-ttu-id="66f5e-236">此只读属性返回**true**如果页是回调的结果。</span><span class="sxs-lookup"><span data-stu-id="66f5e-236">This read-only property returns **true** if the page is the result of a call back.</span></span> <span data-ttu-id="66f5e-237">在此模块的后面部分讨论了回拨。</span><span class="sxs-lookup"><span data-stu-id="66f5e-237">Call backs are discussed later in this module.</span></span>

## <a name="iscrosspagepostback"></a><span data-ttu-id="66f5e-238">IsCrossPagePostBack</span><span class="sxs-lookup"><span data-stu-id="66f5e-238">IsCrossPagePostBack</span></span>

<span data-ttu-id="66f5e-239">此只读属性返回**true**如果页是跨页回发的一部分。</span><span class="sxs-lookup"><span data-stu-id="66f5e-239">This read-only property returns **true** if the page is part of a cross-page postback.</span></span> <span data-ttu-id="66f5e-240">在此模块的后面介绍跨页回发。</span><span class="sxs-lookup"><span data-stu-id="66f5e-240">Cross-page postbacks are covered later in this module.</span></span>

## <a name="items"></a><span data-ttu-id="66f5e-241">项</span><span class="sxs-lookup"><span data-stu-id="66f5e-241">Items</span></span>

<span data-ttu-id="66f5e-242">返回到 IDictionary 实例，其中包含存储在页上下文中的所有对象的引用。</span><span class="sxs-lookup"><span data-stu-id="66f5e-242">Returns a reference to an IDictionary instance that contains all objects stored in the pages context.</span></span> <span data-ttu-id="66f5e-243">你可以将项添加到此 IDictionary 对象，它们将可供你的整个生存期内上下文。</span><span class="sxs-lookup"><span data-stu-id="66f5e-243">You can add items to this IDictionary object and they will be available to you throughout the lifetime of the context.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="66f5e-244">MaintainScrollPositionOnPostBack</span><span class="sxs-lookup"><span data-stu-id="66f5e-244">MaintainScrollPositionOnPostBack</span></span>

<span data-ttu-id="66f5e-245">此属性控制 ASP.NET 发出维护页回发发生后滚动浏览器中的位置的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="66f5e-245">This property controls whether or not ASP.NET emits JavaScript that maintains the pages scroll position in the browser after a postback occurs.</span></span> <span data-ttu-id="66f5e-246">（此属性的详细信息已前面所述此模块。）</span><span class="sxs-lookup"><span data-stu-id="66f5e-246">(Details of this property were discussed earlier in this module.)</span></span>

## <a name="master"></a><span data-ttu-id="66f5e-247">master</span><span class="sxs-lookup"><span data-stu-id="66f5e-247">Master</span></span>

<span data-ttu-id="66f5e-248">此只读属性返回到已应用母版页的页面的母版页实例的引用。</span><span class="sxs-lookup"><span data-stu-id="66f5e-248">This read-only property returns a reference to the MasterPage instance for a page to which a master page has been applied.</span></span>

## <a name="masterpagefile"></a><span data-ttu-id="66f5e-249">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="66f5e-249">MasterPageFile</span></span>

<span data-ttu-id="66f5e-250">获取或设置页面的母版页文件名。</span><span class="sxs-lookup"><span data-stu-id="66f5e-250">Gets or sets the master page filename for the page.</span></span> <span data-ttu-id="66f5e-251">仅可以 PreInit 方法中设置此属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-251">This property can only be set in the PreInit method.</span></span>

## <a name="maxpagestatefieldlength"></a><span data-ttu-id="66f5e-252">MaxPageStateFieldLength</span><span class="sxs-lookup"><span data-stu-id="66f5e-252">MaxPageStateFieldLength</span></span>

<span data-ttu-id="66f5e-253">此属性获取或设置页状态的最大长度以字节为单位。</span><span class="sxs-lookup"><span data-stu-id="66f5e-253">This property gets or sets the maximum length for the pages state in bytes.</span></span> <span data-ttu-id="66f5e-254">如果该属性设置为正数，页面视图状态将分解成多个隐藏的字段，使其不超过指定的字节数。</span><span class="sxs-lookup"><span data-stu-id="66f5e-254">If the property is set to a positive number, the pages view state will be broken up into multiple hidden fields so that it doesnt exceed the number of bytes specified.</span></span> <span data-ttu-id="66f5e-255">如果该属性是负数，则的视图状态将不划分为区块中。</span><span class="sxs-lookup"><span data-stu-id="66f5e-255">If the property is a negative number, the view state will not be broken into chunks.</span></span>

## <a name="pageadapter"></a><span data-ttu-id="66f5e-256">PageAdapter</span><span class="sxs-lookup"><span data-stu-id="66f5e-256">PageAdapter</span></span>

<span data-ttu-id="66f5e-257">返回对修改请求的浏览器的页 PageAdapter 对象的引用。</span><span class="sxs-lookup"><span data-stu-id="66f5e-257">Returns a reference to the PageAdapter object that modifies the page for the requesting browser.</span></span>

## <a name="previouspage"></a><span data-ttu-id="66f5e-258">PreviousPage</span><span class="sxs-lookup"><span data-stu-id="66f5e-258">PreviousPage</span></span>

<span data-ttu-id="66f5e-259">Server.transfer 的调用或跨页回发的情况下均返回到以前的页面的引用。</span><span class="sxs-lookup"><span data-stu-id="66f5e-259">Returns a reference to the previous page in cases of a Server.Transfer or a cross-page postback.</span></span>

## <a name="skinid"></a><span data-ttu-id="66f5e-260">SkinID</span><span class="sxs-lookup"><span data-stu-id="66f5e-260">SkinID</span></span>

<span data-ttu-id="66f5e-261">指定要应用于页的 ASP.NET 2.0 外观。</span><span class="sxs-lookup"><span data-stu-id="66f5e-261">Specifies the ASP.NET 2.0 skin to apply to the page.</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="66f5e-262">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="66f5e-262">StyleSheetTheme</span></span>

<span data-ttu-id="66f5e-263">此属性获取或设置应用于页的样式表。</span><span class="sxs-lookup"><span data-stu-id="66f5e-263">This property gets or sets the style sheet that is applied to a page.</span></span>

## <a name="templatecontrol"></a><span data-ttu-id="66f5e-264">TemplateControl</span><span class="sxs-lookup"><span data-stu-id="66f5e-264">TemplateControl</span></span>

<span data-ttu-id="66f5e-265">返回到页包含控件的引用。</span><span class="sxs-lookup"><span data-stu-id="66f5e-265">Returns a reference to the containing control for the page.</span></span>

## <a name="theme"></a><span data-ttu-id="66f5e-266">主题</span><span class="sxs-lookup"><span data-stu-id="66f5e-266">Theme</span></span>

<span data-ttu-id="66f5e-267">获取或设置 ASP.NET 2.0 主题应用于页面的名称。</span><span class="sxs-lookup"><span data-stu-id="66f5e-267">Gets or sets the name of the ASP.NET 2.0 theme applied to the page.</span></span> <span data-ttu-id="66f5e-268">在 PreInit 方法之前，必须设置此值。</span><span class="sxs-lookup"><span data-stu-id="66f5e-268">This value must be set prior to the PreInit method.</span></span>

## <a name="title"></a><span data-ttu-id="66f5e-269">标题</span><span class="sxs-lookup"><span data-stu-id="66f5e-269">Title</span></span>

<span data-ttu-id="66f5e-270">此属性获取或设置页的标题，从页面标头中获得。</span><span class="sxs-lookup"><span data-stu-id="66f5e-270">This property gets or sets the title for the page as obtained from the pages header.</span></span>

## <a name="viewstateencryptionmode"></a><span data-ttu-id="66f5e-271">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="66f5e-271">ViewStateEncryptionMode</span></span>

<span data-ttu-id="66f5e-272">获取或设置页的 ViewStateEncryptionMode。</span><span class="sxs-lookup"><span data-stu-id="66f5e-272">Gets or sets the ViewStateEncryptionMode of the page.</span></span> <span data-ttu-id="66f5e-273">请参阅本模块前面的此属性的详细的讨论。</span><span class="sxs-lookup"><span data-stu-id="66f5e-273">See a detailed discussion of this property earlier in this module.</span></span>

## <a name="new-protected-properties-of-the-page-class"></a><span data-ttu-id="66f5e-274">页类的新的受保护的属性</span><span class="sxs-lookup"><span data-stu-id="66f5e-274">New Protected Properties of the Page Class</span></span>

<span data-ttu-id="66f5e-275">以下是 ASP.NET 2.0 中的页类的新的受保护的属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-275">The following are the new protected properties of the Page class in ASP.NET 2.0.</span></span>

## <a name="adapter"></a><span data-ttu-id="66f5e-276">适配器</span><span class="sxs-lookup"><span data-stu-id="66f5e-276">Adapter</span></span>

<span data-ttu-id="66f5e-277">返回对呈现在设备上的页 ControlAdapter 的引用请求它。</span><span class="sxs-lookup"><span data-stu-id="66f5e-277">Returns a reference to the ControlAdapter that renders the page on the device that requested it.</span></span>

## <a name="asyncmode"></a><span data-ttu-id="66f5e-278">AsyncMode</span><span class="sxs-lookup"><span data-stu-id="66f5e-278">AsyncMode</span></span>

<span data-ttu-id="66f5e-279">此属性指示以异步方式处理页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-279">This property indicates whether or not the page is processed asynchronously.</span></span> <span data-ttu-id="66f5e-280">它旨在用于由运行时并不直接在代码中。</span><span class="sxs-lookup"><span data-stu-id="66f5e-280">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="clientidseparator"></a><span data-ttu-id="66f5e-281">ClientIDSeparator</span><span class="sxs-lookup"><span data-stu-id="66f5e-281">ClientIDSeparator</span></span>

<span data-ttu-id="66f5e-282">此属性返回时为控件创建唯一的客户端 Id 用作分隔符的字符。</span><span class="sxs-lookup"><span data-stu-id="66f5e-282">This property returns the character used as a separator when creating unique client IDs for controls.</span></span> <span data-ttu-id="66f5e-283">它旨在用于由运行时并不直接在代码中。</span><span class="sxs-lookup"><span data-stu-id="66f5e-283">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="pagestatepersister"></a><span data-ttu-id="66f5e-284">PageStatePersister</span><span class="sxs-lookup"><span data-stu-id="66f5e-284">PageStatePersister</span></span>

<span data-ttu-id="66f5e-285">此属性返回的页面 PageStatePersister 对象。</span><span class="sxs-lookup"><span data-stu-id="66f5e-285">This property returns the PageStatePersister object for the page.</span></span> <span data-ttu-id="66f5e-286">此属性主要由 ASP.NET 控件开发人员使用。</span><span class="sxs-lookup"><span data-stu-id="66f5e-286">This property is primarily used by ASP.NET control developers.</span></span>

## <a name="uniquefilepathsuffix"></a><span data-ttu-id="66f5e-287">UniqueFilePathSuffix</span><span class="sxs-lookup"><span data-stu-id="66f5e-287">UniqueFilePathSuffix</span></span>

<span data-ttu-id="66f5e-288">此属性返回唯一 suffic 追加到缓存浏览器的文件路径。</span><span class="sxs-lookup"><span data-stu-id="66f5e-288">This property returns a unique suffic that is appended to the file path for caching browsers.</span></span> <span data-ttu-id="66f5e-289">默认值是\_ \_ufps = 和 6 位数。</span><span class="sxs-lookup"><span data-stu-id="66f5e-289">The default value is \_\_ufps= and a 6-digit number.</span></span>

## <a name="new-public-methods-for-the-page-class"></a><span data-ttu-id="66f5e-290">页类的新公共方法</span><span class="sxs-lookup"><span data-stu-id="66f5e-290">New Public Methods for the Page Class</span></span>

<span data-ttu-id="66f5e-291">以下的公共方法不熟悉 ASP.NET 2.0 中的页类。</span><span class="sxs-lookup"><span data-stu-id="66f5e-291">The following public methods are new to the Page class in ASP.NET 2.0.</span></span>

## <a name="addonprerendercompleteasync"></a><span data-ttu-id="66f5e-292">AddOnPreRenderCompleteAsync</span><span class="sxs-lookup"><span data-stu-id="66f5e-292">AddOnPreRenderCompleteAsync</span></span>

<span data-ttu-id="66f5e-293">此方法注册异步页执行的事件处理程序委托。</span><span class="sxs-lookup"><span data-stu-id="66f5e-293">This method registers event handler delegates for asynchronous page execution.</span></span> <span data-ttu-id="66f5e-294">在此模块的后面部分讨论了异步页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-294">Asynchronous pages are discussed later in this module.</span></span>

## <a name="applystylesheetskin"></a><span data-ttu-id="66f5e-295">ApplyStyleSheetSkin</span><span class="sxs-lookup"><span data-stu-id="66f5e-295">ApplyStyleSheetSkin</span></span>

<span data-ttu-id="66f5e-296">适用于页的页样式表中的属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-296">Applies the properties in a pages style sheet to the page.</span></span>

## <a name="executeregisteredasynctasks"></a><span data-ttu-id="66f5e-297">ExecuteRegisteredAsyncTasks</span><span class="sxs-lookup"><span data-stu-id="66f5e-297">ExecuteRegisteredAsyncTasks</span></span>

<span data-ttu-id="66f5e-298">此方法朋友异步任务。</span><span class="sxs-lookup"><span data-stu-id="66f5e-298">This method beings an asynchronous task.</span></span>

### <a name="getvalidators"></a><span data-ttu-id="66f5e-299">GetValidators</span><span class="sxs-lookup"><span data-stu-id="66f5e-299">GetValidators</span></span>

<span data-ttu-id="66f5e-300">如果未指定，则返回的验证程序指定的验证组或默认验证组的集合。</span><span class="sxs-lookup"><span data-stu-id="66f5e-300">Returns a collection of validators for the specified validation group or the default validation group if none is specified.</span></span>

## <a name="registerasynctask"></a><span data-ttu-id="66f5e-301">RegisterAsyncTask</span><span class="sxs-lookup"><span data-stu-id="66f5e-301">RegisterAsyncTask</span></span>

<span data-ttu-id="66f5e-302">此方法注册新的异步任务。</span><span class="sxs-lookup"><span data-stu-id="66f5e-302">This method registers a new async task.</span></span> <span data-ttu-id="66f5e-303">在此模块的后面介绍异步页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-303">Asynchronous pages are covered later in this module.</span></span>

## <a name="registerrequirescontrolstate"></a><span data-ttu-id="66f5e-304">RegisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="66f5e-304">RegisterRequiresControlState</span></span>

<span data-ttu-id="66f5e-305">此方法是告诉 ASP.NET 必须保留的页控件状态。</span><span class="sxs-lookup"><span data-stu-id="66f5e-305">This method tells ASP.NET that the pages control state must be persisted.</span></span>

## <a name="registerrequiresviewstateencryption"></a><span data-ttu-id="66f5e-306">RegisterRequiresViewStateEncryption</span><span class="sxs-lookup"><span data-stu-id="66f5e-306">RegisterRequiresViewStateEncryption</span></span>

<span data-ttu-id="66f5e-307">此方法会告知 ASP.NET 页面视图状态，需要加密。</span><span class="sxs-lookup"><span data-stu-id="66f5e-307">This method tells ASP.NET that the pages viewstate requires encryption.</span></span>

## <a name="resolveclienturl"></a><span data-ttu-id="66f5e-308">ResolveClientUrl</span><span class="sxs-lookup"><span data-stu-id="66f5e-308">ResolveClientUrl</span></span>

<span data-ttu-id="66f5e-309">返回可以用于图像，等等的客户端请求的相对 URL。</span><span class="sxs-lookup"><span data-stu-id="66f5e-309">Returns a relative URL that can be used for client requests for images, etc.</span></span>

## <a name="setfocus"></a><span data-ttu-id="66f5e-310">SetFocus</span><span class="sxs-lookup"><span data-stu-id="66f5e-310">SetFocus</span></span>

<span data-ttu-id="66f5e-311">此方法将焦点设置到最初加载页面时指定的控件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-311">This method will set the focus to the control that is specified when the page is initially loaded.</span></span>

## <a name="unregisterrequirescontrolstate"></a><span data-ttu-id="66f5e-312">UnregisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="66f5e-312">UnregisterRequiresControlState</span></span>

<span data-ttu-id="66f5e-313">此方法将为不再需要控制状态持久性传递给它的控件中注销。</span><span class="sxs-lookup"><span data-stu-id="66f5e-313">This method will unregister the control that is passed to it as no longer requiring control state persistence.</span></span>

## <a name="changes-to-the-page-lifecycle"></a><span data-ttu-id="66f5e-314">对页生命周期的更改</span><span class="sxs-lookup"><span data-stu-id="66f5e-314">Changes to the Page Lifecycle</span></span>

<span data-ttu-id="66f5e-315">在 ASP.NET 2.0 中的页生命周期尚未发生显著变化，但有一些你应注意的新方法。</span><span class="sxs-lookup"><span data-stu-id="66f5e-315">The page lifecycle in ASP.NET 2.0 hasnt changed dramatically, but there are some new methods that you should be aware of.</span></span> <span data-ttu-id="66f5e-316">下面列出了 ASP.NET 2.0 页面生命周期。</span><span class="sxs-lookup"><span data-stu-id="66f5e-316">The ASP.NET 2.0 page lifecycle is outlined below.</span></span>

## <a name="preinit-new-in-aspnet-20"></a><span data-ttu-id="66f5e-317">PreInit （新在 ASP.NET 2.0)</span><span class="sxs-lookup"><span data-stu-id="66f5e-317">PreInit (New in ASP.NET 2.0)</span></span>

<span data-ttu-id="66f5e-318">PreInit 事件是开发人员可以访问的生命周期中的最早阶段。</span><span class="sxs-lookup"><span data-stu-id="66f5e-318">The PreInit event is the earliest stage in the lifecycle that a developer can access.</span></span> <span data-ttu-id="66f5e-319">此事件添加使可以以编程方式更改 ASP.NET 2.0 主题、 母版页、 访问 ASP.NET 2.0 配置文件等的属性。如果在回发状态，一定要认识到，Viewstate 已不尚未应用于控件此时生命周期中。</span><span class="sxs-lookup"><span data-stu-id="66f5e-319">The addition of this event makes it possible to programmatically change ASP.NET 2.0 themes, master pages, access properties for an ASP.NET 2.0 profile, etc. If you are in a postback state, its important to realize that Viewstate has not yet been applied to controls at this point in the lifecycle.</span></span> <span data-ttu-id="66f5e-320">因此，如果在此阶段，开发人员更改控件的属性，它将可能覆盖页生命周期中更高版本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-320">Therefore, if a developer changes a property of a control at this stage, it will likely be overwritten later in the pages lifecycle.</span></span>

## <a name="init"></a><span data-ttu-id="66f5e-321">Init</span><span class="sxs-lookup"><span data-stu-id="66f5e-321">Init</span></span>

<span data-ttu-id="66f5e-322">从 ASP.NET 未更改 Init 事件 1.x。</span><span class="sxs-lookup"><span data-stu-id="66f5e-322">The Init event has not changed from ASP.NET 1.x.</span></span> <span data-ttu-id="66f5e-323">这是你想要读取或初始化在页面上的控件的属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-323">This is where you would want to read or initialize properties of controls on your page.</span></span> <span data-ttu-id="66f5e-324">在此阶段、 母版页、 主题，等已应用到页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-324">At this stage, master pages, themes, etc. are already applied to the page.</span></span>

## <a name="initcomplete-new-in-20"></a><span data-ttu-id="66f5e-325">InitComplete （中的新增 2.0)</span><span class="sxs-lookup"><span data-stu-id="66f5e-325">InitComplete (New in 2.0)</span></span>

<span data-ttu-id="66f5e-326">在页初始化阶段的末尾，调用 InitComplete 事件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-326">The InitComplete event is called at the end of the pages initialization stage.</span></span> <span data-ttu-id="66f5e-327">此时在其生命周期，可以访问控件在页上，但尚未填充其状态。</span><span class="sxs-lookup"><span data-stu-id="66f5e-327">At this point in the lifecycle, you can access controls on the page, but their state has not yet been populated.</span></span>

## <a name="preload-new-in-20"></a><span data-ttu-id="66f5e-328">（2.0 中的新） 预加载</span><span class="sxs-lookup"><span data-stu-id="66f5e-328">PreLoad (New in 2.0)</span></span>

<span data-ttu-id="66f5e-329">在应用所有的回发数据后和页之前，将调用此事件\_负载。</span><span class="sxs-lookup"><span data-stu-id="66f5e-329">This event is called after all postback data has been applied and just prior to Page\_Load.</span></span>

## <a name="load"></a><span data-ttu-id="66f5e-330">Load</span><span class="sxs-lookup"><span data-stu-id="66f5e-330">Load</span></span>

<span data-ttu-id="66f5e-331">从 ASP.NET 未更改的 Load 事件 1.x。</span><span class="sxs-lookup"><span data-stu-id="66f5e-331">The Load event has not changed from ASP.NET 1.x.</span></span>

## <a name="loadcomplete-new-in-20"></a><span data-ttu-id="66f5e-332">LoadComplete （中的新增 2.0)</span><span class="sxs-lookup"><span data-stu-id="66f5e-332">LoadComplete (New in 2.0)</span></span>

<span data-ttu-id="66f5e-333">LoadComplete 事件是页负载阶段中的最后一个事件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-333">The LoadComplete event is the last event in the pages load stage.</span></span> <span data-ttu-id="66f5e-334">在此阶段，所有的回发和视图状态数据已应用到页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-334">At this stage, all postback and viewstate data has been applied to the page.</span></span>

## <a name="prerender"></a><span data-ttu-id="66f5e-335">PreRender</span><span class="sxs-lookup"><span data-stu-id="66f5e-335">PreRender</span></span>

<span data-ttu-id="66f5e-336">如果您要用于 viewstate 正确维护的动态添加到页面的控件，PreRender 事件将是将它们添加的最后机会。</span><span class="sxs-lookup"><span data-stu-id="66f5e-336">If you would like for viewstate to be properly maintained for controls that are added to the page dynamically, the PreRender event is the last opportunity to add them.</span></span>

## <a name="prerendercomplete-new-in-20"></a><span data-ttu-id="66f5e-337">PreRenderComplete （中的新增 2.0)</span><span class="sxs-lookup"><span data-stu-id="66f5e-337">PreRenderComplete (New in 2.0)</span></span>

<span data-ttu-id="66f5e-338">在 PreRenderComplete 阶段中，所有控件已都添加到页，而该页已准备好呈现。</span><span class="sxs-lookup"><span data-stu-id="66f5e-338">At the PreRenderComplete stage, all controls have been added to the page and the page is ready to be rendered.</span></span> <span data-ttu-id="66f5e-339">PreRenderComplete 事件是保存的页面视图状态之前引发的最后一个事件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-339">The PreRenderComplete event is the last event raised before the pages viewstate is saved.</span></span>

## <a name="savestatecomplete-new-in-20"></a><span data-ttu-id="66f5e-340">SaveStateComplete （中的新增 2.0)</span><span class="sxs-lookup"><span data-stu-id="66f5e-340">SaveStateComplete (New in 2.0)</span></span>

<span data-ttu-id="66f5e-341">所有的页面视图状态和控制状态已保存后立即调用 SaveStateComplete 事件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-341">The SaveStateComplete event is called immediately after all page viewstate and control state has been saved.</span></span> <span data-ttu-id="66f5e-342">这是最后一个事件之前页面实际呈现到浏览器。</span><span class="sxs-lookup"><span data-stu-id="66f5e-342">This is the last event before the page is actually rendered to the browser.</span></span>

## <a name="render"></a><span data-ttu-id="66f5e-343">呈现</span><span class="sxs-lookup"><span data-stu-id="66f5e-343">Render</span></span>

<span data-ttu-id="66f5e-344">Render 方法不自从 ASP.NET 1.x。</span><span class="sxs-lookup"><span data-stu-id="66f5e-344">The Render method has not changed since ASP.NET 1.x.</span></span> <span data-ttu-id="66f5e-345">这是其中初始化 HtmlTextWriter 和页呈现到浏览器。</span><span class="sxs-lookup"><span data-stu-id="66f5e-345">This is where the HtmlTextWriter is initialized and the page is rendered to the browser.</span></span>

## <a name="cross-page-postback-in-aspnet-20"></a><span data-ttu-id="66f5e-346">在 ASP.NET 2.0 中的跨页回发</span><span class="sxs-lookup"><span data-stu-id="66f5e-346">Cross-Page Postback in ASP.NET 2.0</span></span>

<span data-ttu-id="66f5e-347">在 ASP.NET 中 1.x，需要为发送到相同的页的回发。</span><span class="sxs-lookup"><span data-stu-id="66f5e-347">In ASP.NET 1.x, postbacks were required to post to the same page.</span></span> <span data-ttu-id="66f5e-348">不允许跨页回发。</span><span class="sxs-lookup"><span data-stu-id="66f5e-348">Cross-page postbacks were not allowed.</span></span> <span data-ttu-id="66f5e-349">ASP.NET 2.0 增加了能够回发到 IButtonControl 接口通过不同的页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-349">ASP.NET 2.0 adds the ability to post back to a different page via the IButtonControl interface.</span></span> <span data-ttu-id="66f5e-350">实现新的 IButtonControl 接口 （按钮、 LinkButton 和 ImageButton 除了第三方自定义控件） 的任何控件可以利用通过 PostBackUrl 属性使用此新功能。</span><span class="sxs-lookup"><span data-stu-id="66f5e-350">Any control that implements the new IButtonControl interface (Button, LinkButton, and ImageButton in addition to third-party custom controls) can take advantage of this new functionality via the use of the PostBackUrl attribute.</span></span> <span data-ttu-id="66f5e-351">下面的代码演示回发到第二个页的按钮控件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-351">The following code shows a Button control that posts back to a second page.</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

<span data-ttu-id="66f5e-352">回发页面，启动回发页面时，可通过第二页上的 PreviousPage 属性访问。</span><span class="sxs-lookup"><span data-stu-id="66f5e-352">When the page is posted back, the Page that initiates the postback is accessible via the PreviousPage property on the second page.</span></span> <span data-ttu-id="66f5e-353">通过新的 web 窗体中实现此功能\_控件回发到其他页面时，ASP.NET 2.0 呈现到页的 DoPostBackWithOptions 客户端函数。</span><span class="sxs-lookup"><span data-stu-id="66f5e-353">This functionality is implemented via the new WebForm\_DoPostBackWithOptions client-side function that ASP.NET 2.0 renders to the page when a control posts back to a different page.</span></span> <span data-ttu-id="66f5e-354">通过发出将脚本保存到客户端新 WebResource.axd 处理程序提供了此 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="66f5e-354">This JavaScript function is provided by the new WebResource.axd handler which emits script to the client.</span></span>

<span data-ttu-id="66f5e-355">下面的视频是跨页回发的演练。</span><span class="sxs-lookup"><span data-stu-id="66f5e-355">The video below is a walkthrough of a cross-page postback.</span></span>


![](the-asp-net-2-0-page-model/_static/image2.png)


[<span data-ttu-id="66f5e-356">打开全屏幕视频</span><span class="sxs-lookup"><span data-stu-id="66f5e-356">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/xpage1.wmv)


## <a name="more-details-on-cross-page-postbacks"></a><span data-ttu-id="66f5e-357">在跨页回发的更多详细信息</span><span class="sxs-lookup"><span data-stu-id="66f5e-357">More Details on Cross-Page Postbacks</span></span>

### <a name="viewstate"></a><span data-ttu-id="66f5e-358">视图状态</span><span class="sxs-lookup"><span data-stu-id="66f5e-358">Viewstate</span></span>

<span data-ttu-id="66f5e-359">您可能已要求自己已发生 viewstate 从在跨页回发方案中的第一页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-359">You may have asked yourself already about what happens to the viewstate from the first page in a cross-page postback scenario.</span></span> <span data-ttu-id="66f5e-360">毕竟，不实现 IPostBackDataHandler 任何控件将持久保存其状态通过视图状态，因此有权在跨页回发的第二页上该控件的属性，你必须有权的页面的视图状态。</span><span class="sxs-lookup"><span data-stu-id="66f5e-360">After all, any control that does not implement IPostBackDataHandler will persist its state via viewstate, so to have access to the properties of that control on the second page of a cross-page postback, you must have access to the viewstate for the page.</span></span> <span data-ttu-id="66f5e-361">ASP.NET 2.0 负责的这种情况下，使用调用的第二页中的新隐藏的字段\_ \_PREVIOUSPAGE。</span><span class="sxs-lookup"><span data-stu-id="66f5e-361">ASP.NET 2.0 takes care of this scenario using a new hidden field in the second page called \_\_PREVIOUSPAGE.</span></span> <span data-ttu-id="66f5e-362">\_ \_PREVIOUSPAGE 窗体字段包含的第一页的视图状态，以便你可以访问的所有控件的属性中的第二页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-362">The \_\_PREVIOUSPAGE form field contains the viewstate for the first page so that you can have access to the properties of all controls in the second page.</span></span>

### <a name="circumventing-findcontrol"></a><span data-ttu-id="66f5e-363">也可以避开 FindControl</span><span class="sxs-lookup"><span data-stu-id="66f5e-363">Circumventing FindControl</span></span>

<span data-ttu-id="66f5e-364">在跨页回发的视频演练中，我将使用 FindControl 方法来获取对第一页上文本框控件的引用。</span><span class="sxs-lookup"><span data-stu-id="66f5e-364">In the video walkthrough of a cross-page postback, I used the FindControl method to get a reference to the TextBox control on the first page.</span></span> <span data-ttu-id="66f5e-365">该方法非常适用于该目的，但 FindControl 将占用大量资源，并且它需要编写附加代码。</span><span class="sxs-lookup"><span data-stu-id="66f5e-365">That method works well for that purpose, but FindControl is expensive and it requires writing additional code.</span></span> <span data-ttu-id="66f5e-366">幸运的是，ASP.NET 2.0 提供 FindControl 的替代项为此目的，将在许多方案中工作。</span><span class="sxs-lookup"><span data-stu-id="66f5e-366">Fortunately, ASP.NET 2.0 provides an alternative to FindControl for this purpose that will work in many scenarios.</span></span> <span data-ttu-id="66f5e-367">PreviousPageType 指令允许你通过使用类型名称或 VirtualPath 属性具有到以前的页面的强类型引用。</span><span class="sxs-lookup"><span data-stu-id="66f5e-367">The PreviousPageType directive allows you to have a strongly-typed reference to the previous page by using either the TypeName or the VirtualPath attribute.</span></span> <span data-ttu-id="66f5e-368">TypeName 属性，可指定前一页的类型，同时 VirtualPath 属性允许您以引用使用的虚拟路径的前一页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-368">The TypeName attribute allows you to specify the type of the previous page while the VirtualPath attribute allows you to refer to the previous page using a virtual path.</span></span> <span data-ttu-id="66f5e-369">设置 PreviousPageType 指令后，就必须公开控件，你想要允许使用公共属性的访问等。</span><span class="sxs-lookup"><span data-stu-id="66f5e-369">After you've set the PreviousPageType directive, you must then expose the controls, etc. to which you want to allow access using public properties.</span></span>

## <a name="lab-1-cross-page-postback"></a><span data-ttu-id="66f5e-370">实验室 1 跨页回发</span><span class="sxs-lookup"><span data-stu-id="66f5e-370">Lab 1 Cross-Page Postback</span></span>

<span data-ttu-id="66f5e-371">在本实验中，你将创建使用新的 ASP.NET 2.0 跨页面回发的功能的应用程序。</span><span class="sxs-lookup"><span data-stu-id="66f5e-371">In this lab, you will create an application that uses the new cross-page postback functionality of ASP.NET 2.0.</span></span>

1. <span data-ttu-id="66f5e-372">打开 Visual Studio 2005 并创建新的 ASP.NET Web 站点。</span><span class="sxs-lookup"><span data-stu-id="66f5e-372">Open Visual Studio 2005 and create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="66f5e-373">添加调用 page2.aspx 的新 web 窗体。</span><span class="sxs-lookup"><span data-stu-id="66f5e-373">Add a new Webform called page2.aspx.</span></span>
3. <span data-ttu-id="66f5e-374">在设计视图中打开 Default.aspx 并添加一个按钮控件和文本框控件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-374">Open the Default.aspx in Design view and add a Button control and a TextBox control.</span></span> 

    1. <span data-ttu-id="66f5e-375">为按钮控件指定的 ID**提交按钮**和文本框控件的 ID**用户名**。</span><span class="sxs-lookup"><span data-stu-id="66f5e-375">Give the Button control an ID of **SubmitButton** and the TextBox control an ID of **UserName**.</span></span>
    2. <span data-ttu-id="66f5e-376">设置为 page2.aspx 的按钮 PostBackUrl 属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-376">Set the PostBackUrl property of the Button to page2.aspx.</span></span>
4. <span data-ttu-id="66f5e-377">在源视图中打开 page2.aspx。</span><span class="sxs-lookup"><span data-stu-id="66f5e-377">Open page2.aspx in Source view.</span></span>
5. <span data-ttu-id="66f5e-378">添加 @ PreviousPageType 指令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="66f5e-378">Add a @ PreviousPageType directive as shown below:</span></span>
6. <span data-ttu-id="66f5e-379">将以下代码添加到页\_page2.aspx 的隐藏代码的负载：</span><span class="sxs-lookup"><span data-stu-id="66f5e-379">Add the following code to the Page\_Load of page2.aspx's code-behind:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. <span data-ttu-id="66f5e-380">通过在生成菜单上单击生成中生成项目。</span><span class="sxs-lookup"><span data-stu-id="66f5e-380">Build the project by clicking on Build on the Build menu.</span></span>
8. <span data-ttu-id="66f5e-381">将以下代码添加到 Default.aspx 代码隐藏：</span><span class="sxs-lookup"><span data-stu-id="66f5e-381">Add the following code to the code-behind for Default.aspx:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. <span data-ttu-id="66f5e-382">更改页\_中所示的 page2.aspx 负载：</span><span class="sxs-lookup"><span data-stu-id="66f5e-382">Change the Page\_Load in page2.aspx to the following:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. <span data-ttu-id="66f5e-383">生成项目。</span><span class="sxs-lookup"><span data-stu-id="66f5e-383">Build the project.</span></span>
11. <span data-ttu-id="66f5e-384">运行该项目。</span><span class="sxs-lookup"><span data-stu-id="66f5e-384">Run the project.</span></span>
12. <span data-ttu-id="66f5e-385">在文本框中输入你的名称，然后单击按钮。</span><span class="sxs-lookup"><span data-stu-id="66f5e-385">Enter your name in the TextBox and click the button.</span></span>
13. <span data-ttu-id="66f5e-386">结果是什么？</span><span class="sxs-lookup"><span data-stu-id="66f5e-386">What is the result?</span></span>

## <a name="asynchronous-pages-in-aspnet-20"></a><span data-ttu-id="66f5e-387">在 ASP.NET 2.0 中的异步页</span><span class="sxs-lookup"><span data-stu-id="66f5e-387">Asynchronous Pages in ASP.NET 2.0</span></span>

<span data-ttu-id="66f5e-388">在 ASP.NET 中的许多争用问题而引起的 （如 Web 服务或数据库调用） 的外部调用、 文件 IO 延迟等的延迟。当针对 ASP.NET 应用程序发出请求时，ASP.NET 将使用一种与其工作线程来处理该请求。</span><span class="sxs-lookup"><span data-stu-id="66f5e-388">Many contention problems in ASP.NET are caused by latency of external calls (such as Web service or database calls), file IO latency, etc. When a request is made against an ASP.NET application, ASP.NET uses one of its worker threads to service that request.</span></span> <span data-ttu-id="66f5e-389">该请求拥有该线程，直到完成该请求并发送响应。</span><span class="sxs-lookup"><span data-stu-id="66f5e-389">That request owns that thread until the request is complete and the response has been sent.</span></span> <span data-ttu-id="66f5e-390">ASP.NET 2.0 试图通过添加功能以异步方式执行页解决这些类型的问题的延迟问题。</span><span class="sxs-lookup"><span data-stu-id="66f5e-390">ASP.NET 2.0 seeks to resolve latency issues with these types of issues by adding the capability to execute pages asynchronously.</span></span> <span data-ttu-id="66f5e-391">这意味着工作线程可以启动请求，然后移交其他执行的另一个线程，从而快速返回到可用线程池。</span><span class="sxs-lookup"><span data-stu-id="66f5e-391">That means that a worker thread can start the request and then hand off additional execution to another thread, thereby returning to the available thread pool quickly.</span></span> <span data-ttu-id="66f5e-392">完成后的文件 IO、 数据库调用等，从要完成该请求的线程池获得新线程。</span><span class="sxs-lookup"><span data-stu-id="66f5e-392">When the file IO, database call, etc. has completed, a new thread is obtained from the thread pool to finish the request.</span></span>

<span data-ttu-id="66f5e-393">在进行异步执行的页的第一步是设置**异步**页面指令属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="66f5e-393">The first step in making a page execute asynchronously is to set the **Async** attribute of the page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

<span data-ttu-id="66f5e-394">此属性是告诉 ASP.NET，若要实现页 IHttpAsyncHandler。</span><span class="sxs-lookup"><span data-stu-id="66f5e-394">This attribute tells ASP.NET to implement the IHttpAsyncHandler for the page.</span></span>

<span data-ttu-id="66f5e-395">下一步是要在之前 PreRender 页生命周期中的点调用 AddOnPreRenderCompleteAsync 方法。</span><span class="sxs-lookup"><span data-stu-id="66f5e-395">The next step is to call the AddOnPreRenderCompleteAsync method at a point in the lifecycle of the page prior to PreRender.</span></span> <span data-ttu-id="66f5e-396">(通常在页中调用此方法\_负载。)AddOnPreRenderCompleteAsync 方法采用两个参数;BeginEventHandler 和 EndEventHandler。</span><span class="sxs-lookup"><span data-stu-id="66f5e-396">(This method is typically called in Page\_Load.) The AddOnPreRenderCompleteAsync method takes two parameters; a BeginEventHandler and an EndEventHandler.</span></span> <span data-ttu-id="66f5e-397">BeginEventHandler 返回 IAsyncResult 然后传递给 EndEventHandler 作为参数。</span><span class="sxs-lookup"><span data-stu-id="66f5e-397">The BeginEventHandler returns an IAsyncResult which is then passed as a parameter to the EndEventHandler.</span></span>

<span data-ttu-id="66f5e-398">以下视频是异步页请求的演练。</span><span class="sxs-lookup"><span data-stu-id="66f5e-398">The video below is a walkthrough of an asynchronous page request.</span></span>


![](the-asp-net-2-0-page-model/_static/image3.png)


[<span data-ttu-id="66f5e-399">打开全屏幕视频</span><span class="sxs-lookup"><span data-stu-id="66f5e-399">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/async1.wmv)


> [!NOTE]
> <span data-ttu-id="66f5e-400">直到完成 EndEventHandler 异步页不会呈现到浏览器中。</span><span class="sxs-lookup"><span data-stu-id="66f5e-400">An async page does not render to the browser until the EndEventHandler has completed.</span></span> <span data-ttu-id="66f5e-401">毫无疑问，但一些开发人员将将视为类似于异步回调的异步请求。</span><span class="sxs-lookup"><span data-stu-id="66f5e-401">No doubt but that some developers will think of async requests as being similar to async callbacks.</span></span> <span data-ttu-id="66f5e-402">请务必意识到它们不是。</span><span class="sxs-lookup"><span data-stu-id="66f5e-402">It's important to realize that they are not.</span></span> <span data-ttu-id="66f5e-403">异步请求到的好处是，可以为新请求提供服务，从而减少了由于 IO 绑定的争用，等等的线程池返回第一个工作线程。</span><span class="sxs-lookup"><span data-stu-id="66f5e-403">The benefit to asynchronous requests is that the first worker thread can be returned to the thread pool to service new requests, thereby reducing contention due to being IO bound, etc.</span></span>


## <a name="script-callbacks-in-aspnet-20"></a><span data-ttu-id="66f5e-404">在 ASP.NET 2.0 中的脚本回调</span><span class="sxs-lookup"><span data-stu-id="66f5e-404">Script Callbacks in ASP.NET 2.0</span></span>

<span data-ttu-id="66f5e-405">Web 开发人员一直始终在寻找种方法可避免闪烁与回调相关联。</span><span class="sxs-lookup"><span data-stu-id="66f5e-405">Web developers have always looked for ways to prevent the flickering associated with a callback.</span></span> <span data-ttu-id="66f5e-406">在 ASP.NET 中 1.x，SmartNavigation 避免闪烁，最常用方法但 SmartNavigation 由于客户端上其实现的复杂性为一些开发人员带来问题。</span><span class="sxs-lookup"><span data-stu-id="66f5e-406">In ASP.NET 1.x, SmartNavigation was the most common method for avoiding flickering, but SmartNavigation caused problems for some developers because of the complexity of its implementation on the client.</span></span> <span data-ttu-id="66f5e-407">ASP.NET 2.0，解决此问题与脚本回调。</span><span class="sxs-lookup"><span data-stu-id="66f5e-407">ASP.NET 2.0 addresses this issue with script callbacks.</span></span> <span data-ttu-id="66f5e-408">脚本回调利用 XMLHttp 针对通过 JavaScript 的 Web 服务器发出请求。</span><span class="sxs-lookup"><span data-stu-id="66f5e-408">Script callbacks utilize XMLHttp to make requests against the Web server via JavaScript.</span></span> <span data-ttu-id="66f5e-409">XMLHttp 请求返回 XML 数据然后可操纵通过浏览器的 dom。</span><span class="sxs-lookup"><span data-stu-id="66f5e-409">The XMLHttp request returns XML data that can then be manipulated via the browser's DOM.</span></span> <span data-ttu-id="66f5e-410">用户从新 WebResource.axd 处理程序的情况下，XMLHttp 代码处于隐藏状态。</span><span class="sxs-lookup"><span data-stu-id="66f5e-410">XMLHttp code is hidden from the user by the new WebResource.axd handler.</span></span>

<span data-ttu-id="66f5e-411">有几个步骤所需配置 ASP.NET 2.0 中的脚本回调。</span><span class="sxs-lookup"><span data-stu-id="66f5e-411">There are several steps that are necessary in order to configure a script callback in ASP.NET 2.0.</span></span>

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a><span data-ttu-id="66f5e-412">步骤 1： 实现 ICallbackEventHandler 接口</span><span class="sxs-lookup"><span data-stu-id="66f5e-412">Step 1 : Implement the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="66f5e-413">为了使 ASP.NET 可以将你的页面识别为参与脚本回调，则必须实现 ICallbackEventHandler 接口。</span><span class="sxs-lookup"><span data-stu-id="66f5e-413">In order for ASP.NET to recognize your page as participating in a script callback, you must implement the ICallbackEventHandler interface.</span></span> <span data-ttu-id="66f5e-414">你可以执行此操作的代码隐藏文件中如下所示：</span><span class="sxs-lookup"><span data-stu-id="66f5e-414">You can do this in your code-behind file like so:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

<span data-ttu-id="66f5e-415">你也可以这样做因此使用 @ 实现指令类似：</span><span class="sxs-lookup"><span data-stu-id="66f5e-415">You can also do this using the @ Implements directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

<span data-ttu-id="66f5e-416">使用内联 ASP.NET 代码时，你通常将使用 @ 实现指令。</span><span class="sxs-lookup"><span data-stu-id="66f5e-416">You would typically use the @ Implements directive when using inline ASP.NET code.</span></span>

## <a name="step-2--call-getcallbackeventreference"></a><span data-ttu-id="66f5e-417">步骤 2： 调用 GetCallbackEventReference</span><span class="sxs-lookup"><span data-stu-id="66f5e-417">Step 2 : Call GetCallbackEventReference</span></span>

<span data-ttu-id="66f5e-418">如前所述，XMLHttp 调用将封装在 WebResource.axd 处理程序。</span><span class="sxs-lookup"><span data-stu-id="66f5e-418">As mentioned previously, the XMLHttp call is encapsulated in the WebResource.axd handler.</span></span> <span data-ttu-id="66f5e-419">ASP.NET 页面呈现时，将添加对 web 窗体的调用\_DoCallback，WebResource.axd 由提供的客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-419">When your page is rendered, ASP.NET will add a call to WebForm\_DoCallback, a client script that is provided by WebResource.axd.</span></span> <span data-ttu-id="66f5e-420">该 web 窗体\_DoCallback 函数将替换\_ \_doPostBack 回调函数。</span><span class="sxs-lookup"><span data-stu-id="66f5e-420">The WebForm\_DoCallback function replaces the \_\_doPostBack function for a callback.</span></span> <span data-ttu-id="66f5e-421">请记住， \_ \_doPostBack 以编程方式提交页上的表单。</span><span class="sxs-lookup"><span data-stu-id="66f5e-421">Remember that \_\_doPostBack programmatically submits the form on the page.</span></span> <span data-ttu-id="66f5e-422">你希望在回调方案中，因此阻止回发， \_ \_doPostBack 不满足要求。</span><span class="sxs-lookup"><span data-stu-id="66f5e-422">In a callback scenario, you want to prevent a postback, so \_\_doPostBack will not suffice.</span></span>

> [!NOTE]
> <span data-ttu-id="66f5e-423">\_\_doPostBack 仍呈现到客户端脚本回调方案中的页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-423">\_\_doPostBack is still rendered to the page in a client script callback scenario.</span></span> <span data-ttu-id="66f5e-424">但是，它不用于回调。</span><span class="sxs-lookup"><span data-stu-id="66f5e-424">However, it's not used for the callback.</span></span>


<span data-ttu-id="66f5e-425">该 web 窗体的自变量\_DoCallback 客户端函数提供通过服务器端功能通常会在页中调用的 GetCallbackEventReference\_负载。</span><span class="sxs-lookup"><span data-stu-id="66f5e-425">The arguments for the WebForm\_DoCallback client-side function are provided via the server-side function GetCallbackEventReference which would normally be called in Page\_Load.</span></span> <span data-ttu-id="66f5e-426">典型调用 GetCallbackEventReference 可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="66f5e-426">A typical call to GetCallbackEventReference might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="66f5e-427">在这种情况下，cm 是 ClientScriptManager 的一个实例。</span><span class="sxs-lookup"><span data-stu-id="66f5e-427">In this case, cm is an instance of ClientScriptManager.</span></span> <span data-ttu-id="66f5e-428">ClientScriptManager 类将在此模块的后面进行介绍。</span><span class="sxs-lookup"><span data-stu-id="66f5e-428">The ClientScriptManager class will be covered later in this module.</span></span>


<span data-ttu-id="66f5e-429">有多个重载的版本的 GetCallbackEventReference。</span><span class="sxs-lookup"><span data-stu-id="66f5e-429">There are several overloaded versions of GetCallbackEventReference.</span></span> <span data-ttu-id="66f5e-430">在这种情况下，自变量如下所示：</span><span class="sxs-lookup"><span data-stu-id="66f5e-430">In this case, the arguments are as follows:</span></span>

`this`

<span data-ttu-id="66f5e-431">对调用 GetCallbackEventReference 控件的引用。</span><span class="sxs-lookup"><span data-stu-id="66f5e-431">A reference to the control where GetCallbackEventReference is being called.</span></span> <span data-ttu-id="66f5e-432">在这种情况下，它是本身的页。</span><span class="sxs-lookup"><span data-stu-id="66f5e-432">In this case, it's the page itself.</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

<span data-ttu-id="66f5e-433">将从客户端代码中向服务器端事件传递一个字符串参数。</span><span class="sxs-lookup"><span data-stu-id="66f5e-433">A string argument that will be passed from the client-side code to the server-side event.</span></span> <span data-ttu-id="66f5e-434">在这种情况下，将下拉列表中的值传递的 Im 调用 ddlCompany。</span><span class="sxs-lookup"><span data-stu-id="66f5e-434">In this case, Im passing the value of a dropdown called ddlCompany.</span></span>

`ShowCompanyName`

<span data-ttu-id="66f5e-435">将在从服务器端回调事件返回的值接受 （作为字符串） 的客户端函数名称。</span><span class="sxs-lookup"><span data-stu-id="66f5e-435">The name of the client-side function that will accept the return value (as string) from the server-side callback event.</span></span> <span data-ttu-id="66f5e-436">服务器端回调成功后，将仅调用此函数。</span><span class="sxs-lookup"><span data-stu-id="66f5e-436">This function will only be called when the server-side callback is successful.</span></span> <span data-ttu-id="66f5e-437">因此，为了可靠性，通常建议使用 GetCallbackEventReference 采用指定要执行发生错误时的客户端函数的名称的附加字符串自变量的重载的版本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-437">Therefore, for the sake of robustness, it is generally recommended to use the overloaded version of GetCallbackEventReference that takes an additional string argument specifying the name of a client-side function to execute in the event of an error.</span></span>

`null`

<span data-ttu-id="66f5e-438">表示它到服务器在回调之前启动的客户端函数的字符串。</span><span class="sxs-lookup"><span data-stu-id="66f5e-438">A string representing a client-side function that it initiated before the callback to the server.</span></span> <span data-ttu-id="66f5e-439">在这种情况下，没有此类脚本，因此该参数为 null。</span><span class="sxs-lookup"><span data-stu-id="66f5e-439">In this case, there is no such script, so the argument is null.</span></span>

`true`

<span data-ttu-id="66f5e-440">一个布尔值，指定以异步方式执行回调。</span><span class="sxs-lookup"><span data-stu-id="66f5e-440">A Boolean specifying whether or not to conduct the callback asynchronously.</span></span>

<span data-ttu-id="66f5e-441">Web 窗体调用\_DoCallback 客户端上的会将这些参数传递。</span><span class="sxs-lookup"><span data-stu-id="66f5e-441">The call to WebForm\_DoCallback on the client will pass these arguments.</span></span> <span data-ttu-id="66f5e-442">因此，客户端上呈现此页面，该代码将看起来如下所示：</span><span class="sxs-lookup"><span data-stu-id="66f5e-442">Therefore, when this page is rendered on the client, that code will look like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

<span data-ttu-id="66f5e-443">请注意，客户端上函数的签名稍有不同。</span><span class="sxs-lookup"><span data-stu-id="66f5e-443">Notice that the signature of the function on the client is a bit different.</span></span> <span data-ttu-id="66f5e-444">客户端函数会将 5 个字符串和一个布尔值传递。</span><span class="sxs-lookup"><span data-stu-id="66f5e-444">The client-side function passes 5 strings and a Boolean.</span></span> <span data-ttu-id="66f5e-445">（这是 null，在上面的示例中） 的其他字符串包含客户端函数将处理从服务器端回调的任何错误。</span><span class="sxs-lookup"><span data-stu-id="66f5e-445">The additional string (which is null in the above example) contains the client-side function that will handle any errors from the server-side callback.</span></span>

## <a name="step-3--hook-the-client-side-control-event"></a><span data-ttu-id="66f5e-446">步骤 3： 挂钩的客户端控件事件</span><span class="sxs-lookup"><span data-stu-id="66f5e-446">Step 3 : Hook the Client-Side Control Event</span></span>

<span data-ttu-id="66f5e-447">请注意，上面的 GetCallbackEventReference 的返回值分配给字符串变量。</span><span class="sxs-lookup"><span data-stu-id="66f5e-447">Notice that the return value of GetCallbackEventReference above was assigned to a string variable.</span></span> <span data-ttu-id="66f5e-448">该字符串用于挂钩启动回调的控件的客户端事件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-448">That string is used to hook a client-side event for the control that initiates the callback.</span></span> <span data-ttu-id="66f5e-449">在此示例中，回调可由下拉列表中的页上，因此我想要挂钩*OnChange*事件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-449">In this example, the callback is initiated by a dropdown on the page, so I want to hook the *OnChange* event.</span></span>

<span data-ttu-id="66f5e-450">若要将连接客户端事件，只需添加一个处理程序到客户端标记，如下所示：</span><span class="sxs-lookup"><span data-stu-id="66f5e-450">To hook the client-side event, simply add a handler to the client-side markup as follows:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

<span data-ttu-id="66f5e-451">回想一下， *cbRef*是 GetCallbackEventReference 调用的返回值。</span><span class="sxs-lookup"><span data-stu-id="66f5e-451">Recall that *cbRef* is the return value from the call to GetCallbackEventReference.</span></span> <span data-ttu-id="66f5e-452">它包含对 web 窗体的调用\_DoCallback 上面所示。</span><span class="sxs-lookup"><span data-stu-id="66f5e-452">It contains the call to WebForm\_DoCallback that was shown above.</span></span>

## <a name="step-4--register-the-client-side-script"></a><span data-ttu-id="66f5e-453">步骤 4： 注册客户端脚本</span><span class="sxs-lookup"><span data-stu-id="66f5e-453">Step 4 : Register the Client-Side Script</span></span>

<span data-ttu-id="66f5e-454">回想一下，GetCallbackEventReference 调用指定客户端脚本调用**ShowCompanyName**服务器端回调成功时将执行。</span><span class="sxs-lookup"><span data-stu-id="66f5e-454">Recall that the call to GetCallbackEventReference specified that a client-side script called **ShowCompanyName** would be executed when the server-side callback succeeds.</span></span> <span data-ttu-id="66f5e-455">该脚本需要添加到页面使用的 ClientScriptManager 实例。</span><span class="sxs-lookup"><span data-stu-id="66f5e-455">That script needs to be added to the page using a ClientScriptManager instance.</span></span> <span data-ttu-id="66f5e-456">（ClientScriptManager 类将是此模块中的更高版本的讨论。）因此不要该类似：</span><span class="sxs-lookup"><span data-stu-id="66f5e-456">(The ClientScriptManager class will be dicussed later in this module.) You do that like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a><span data-ttu-id="66f5e-457">步骤 5： 调用的方法的 ICallbackEventHandler 接口</span><span class="sxs-lookup"><span data-stu-id="66f5e-457">Step 5 : Call the Methods of the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="66f5e-458">ICallbackEventHandler 包含两个方法，你需要在你的代码中实现。</span><span class="sxs-lookup"><span data-stu-id="66f5e-458">The ICallbackEventHandler contains two methods that you need to implement in your code.</span></span> <span data-ttu-id="66f5e-459">它们是**RaiseCallbackEvent**和**GetCallbackEvent**。</span><span class="sxs-lookup"><span data-stu-id="66f5e-459">They are **RaiseCallbackEvent** and **GetCallbackEvent**.</span></span>

<span data-ttu-id="66f5e-460">**RaiseCallbackEvent**采用字符串作为自变量和返回任何内容。</span><span class="sxs-lookup"><span data-stu-id="66f5e-460">**RaiseCallbackEvent** takes a string as an argument and returns nothing.</span></span> <span data-ttu-id="66f5e-461">字符串自变量传递与 web 窗体的客户端调用\_DoCallback。</span><span class="sxs-lookup"><span data-stu-id="66f5e-461">The string argument is passed from the client-side call to WebForm\_DoCallback.</span></span> <span data-ttu-id="66f5e-462">在这种情况下，该值是*值*调用 ddlCompany 下拉列表中的属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-462">In this case, that value is the *value* attribute of the dropdown called ddlCompany.</span></span> <span data-ttu-id="66f5e-463">应将你的服务器端代码置于 RaiseCallbackEvent 方法。</span><span class="sxs-lookup"><span data-stu-id="66f5e-463">Your server-side code should be placed in the RaiseCallbackEvent method.</span></span> <span data-ttu-id="66f5e-464">例如，如果你的回调 WebRequest 针对外部资源，该代码应放置在 RaiseCallbackEvent。</span><span class="sxs-lookup"><span data-stu-id="66f5e-464">For example, if your callback is making a WebRequest against an external resource, that code should be placed in RaiseCallbackEvent.</span></span>

<span data-ttu-id="66f5e-465">**GetCallbackEvent**负责处理返回给客户端的回调。</span><span class="sxs-lookup"><span data-stu-id="66f5e-465">**GetCallbackEvent** is responsible for processing the return of the callback to the client.</span></span> <span data-ttu-id="66f5e-466">它不采用任何参数并返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="66f5e-466">It takes no arguments and returns a string.</span></span> <span data-ttu-id="66f5e-467">它将返回的字符串将作为参数传递给客户端函数中，在这种情况下*ShowCompanyName*。</span><span class="sxs-lookup"><span data-stu-id="66f5e-467">The string that it returns will be passed as an argument to the client-side function, in this case *ShowCompanyName*.</span></span>

<span data-ttu-id="66f5e-468">完成上述步骤后，你就可以在 ASP.NET 2.0 中执行脚本回调。</span><span class="sxs-lookup"><span data-stu-id="66f5e-468">Once you have completed the above steps, you are ready to perform a script callback in ASP.NET 2.0.</span></span>


![](the-asp-net-2-0-page-model/_static/image4.png)


[<span data-ttu-id="66f5e-469">打开全屏幕视频</span><span class="sxs-lookup"><span data-stu-id="66f5e-469">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/callback1.wmv)


<span data-ttu-id="66f5e-470">中支持使 XMLHttp 调用任何浏览器支持在 ASP.NET 中的脚本回调。</span><span class="sxs-lookup"><span data-stu-id="66f5e-470">Script callbacks in ASP.NET are supported in any browser that supports making XMLHttp calls.</span></span> <span data-ttu-id="66f5e-471">中包括所有现代浏览器中使用今天。</span><span class="sxs-lookup"><span data-stu-id="66f5e-471">That includes all of the modern browsers in use today.</span></span> <span data-ttu-id="66f5e-472">Internet Explorer 使用 XMLHttp ActiveX 对象，而其他浏览器 （包括即将到来的 IE 7） 使用的内部 XMLHttp 对象。</span><span class="sxs-lookup"><span data-stu-id="66f5e-472">Internet Explorer uses the XMLHttp ActiveX object while other modern browsers (including the upcoming IE 7) use an intrinsic XMLHttp object.</span></span> <span data-ttu-id="66f5e-473">若要以编程方式确定是否浏览器支持回调，则可以使用**Request.Browser.SupportCallback**属性。</span><span class="sxs-lookup"><span data-stu-id="66f5e-473">To programmatically determine if a browser supports callbacks, you can use the **Request.Browser.SupportCallback** property.</span></span> <span data-ttu-id="66f5e-474">此属性将返回**true**如果请求的客户端支持脚本回调。</span><span class="sxs-lookup"><span data-stu-id="66f5e-474">This property will return **true** if the requesting client supports script callbacks.</span></span>

## <a name="working-with-client-script-in-aspnet-20"></a><span data-ttu-id="66f5e-475">使用 ASP.NET 2.0 中的客户端脚本</span><span class="sxs-lookup"><span data-stu-id="66f5e-475">Working with Client Script in ASP.NET 2.0</span></span>

<span data-ttu-id="66f5e-476">通过使用 ClientScriptManager 类情况下，ASP.NET 2.0 中的客户端脚本进行管理。</span><span class="sxs-lookup"><span data-stu-id="66f5e-476">Client scripts in ASP.NET 2.0 are managed via the use of the ClientScriptManager class.</span></span> <span data-ttu-id="66f5e-477">将跟踪 ClientScriptManager 类的使用类型和名称的客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-477">The ClientScriptManager class keeps track of client scripts using a type and a name.</span></span> <span data-ttu-id="66f5e-478">这可以防止同一个脚本以编程方式插入页面上一次以上。</span><span class="sxs-lookup"><span data-stu-id="66f5e-478">This prevents the same script from being programmatically inserted on a page more than once.</span></span>

> [!NOTE]
> <span data-ttu-id="66f5e-479">脚本已成功注册在页面上后，任何后续尝试注册同一脚本只需将导致不正在注册第二次的脚本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-479">After a script has been successfully registered on a page, any subsequent attempt to register the same script will simply result in the script not being registered a second time.</span></span> <span data-ttu-id="66f5e-480">添加任何重复的脚本，并且未发生任何异常。</span><span class="sxs-lookup"><span data-stu-id="66f5e-480">No duplicate scripts are added and no exception occurs.</span></span> <span data-ttu-id="66f5e-481">若要避免不必要的计算，还有一些可用于确定，以便不尝试多次注册，是否已注册脚本的方法。</span><span class="sxs-lookup"><span data-stu-id="66f5e-481">To avoid unnecessary computation, there are methods that you can use to determine if a script is already registered so that you do not attempt to register it more than once.</span></span>


<span data-ttu-id="66f5e-482">应为所有当前的 ASP.NET 开发人员熟悉 ClientScriptManager 的方法：</span><span class="sxs-lookup"><span data-stu-id="66f5e-482">The methods of the ClientScriptManager should be familiar to all current ASP.NET developers:</span></span>

## <a name="registerclientscriptblock"></a><span data-ttu-id="66f5e-483">RegisterClientScriptBlock</span><span class="sxs-lookup"><span data-stu-id="66f5e-483">RegisterClientScriptBlock</span></span>

<span data-ttu-id="66f5e-484">此方法将脚本添加到所呈现的页面的顶部。</span><span class="sxs-lookup"><span data-stu-id="66f5e-484">This method adds a script to the top of the rendered page.</span></span> <span data-ttu-id="66f5e-485">这可用于添加将在客户端显式调用的函数。</span><span class="sxs-lookup"><span data-stu-id="66f5e-485">This is useful for adding functions that will be explicitly called on the client.</span></span>

<span data-ttu-id="66f5e-486">有两个重载的版本，此方法。</span><span class="sxs-lookup"><span data-stu-id="66f5e-486">There are two overloaded versions of this method.</span></span> <span data-ttu-id="66f5e-487">三个四个自变量是在它们之间常见。</span><span class="sxs-lookup"><span data-stu-id="66f5e-487">Three of four arguments are common among them.</span></span> <span data-ttu-id="66f5e-488">它们是：</span><span class="sxs-lookup"><span data-stu-id="66f5e-488">They are:</span></span>

`type (string)`

<span data-ttu-id="66f5e-489">***类型***自变量标识脚本的类型。</span><span class="sxs-lookup"><span data-stu-id="66f5e-489">The ***type*** argument identifies a type for the script.</span></span> <span data-ttu-id="66f5e-490">它通常是一个好办法使用页面的类型 （这。类型的 GetType())。</span><span class="sxs-lookup"><span data-stu-id="66f5e-490">It is generally a good idea to use the page's type (this.GetType()) for the type.</span></span>

`key (string)`

<span data-ttu-id="66f5e-491">***密钥***自变量是脚本的用户定义键。</span><span class="sxs-lookup"><span data-stu-id="66f5e-491">The ***key*** argument is a user-defined key for the script.</span></span> <span data-ttu-id="66f5e-492">这应是唯一的每个脚本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-492">This should be unique for each script.</span></span> <span data-ttu-id="66f5e-493">如果你尝试添加具有相同的键和类型的已添加脚本的脚本，将不会添加它。</span><span class="sxs-lookup"><span data-stu-id="66f5e-493">If you attempt to add a script with the same key and type of an already added script, it will not be added.</span></span>

`script (string)`

<span data-ttu-id="66f5e-494">***脚本***自变量是一个包含要添加的实际脚本字符串。</span><span class="sxs-lookup"><span data-stu-id="66f5e-494">The ***script*** argument is a string containing the actual script to add.</span></span> <span data-ttu-id="66f5e-495">建议使用 StringBuilder 创建脚本，然后使用 StringBuilder 上的 tostring （） 方法来分配***脚本***自变量。</span><span class="sxs-lookup"><span data-stu-id="66f5e-495">It's recommended that you use a StringBuilder to create the script and then use the ToString() method on the StringBuilder to assign the ***script*** argument.</span></span>

<span data-ttu-id="66f5e-496">如果你使用重载的 RegisterClientScriptBlock 仅使用三个参数，则必须包含脚本元素 (&lt;脚本&gt;和&lt;/&gt;) 在你的脚本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-496">If you use the overloaded RegisterClientScriptBlock that only takes three arguments, you must include script elements (&lt;script&gt; and &lt;/script&gt;) in your script.</span></span>

<span data-ttu-id="66f5e-497">你可以选择使用 RegisterClientScriptBlock 采用第四个参数的重载。</span><span class="sxs-lookup"><span data-stu-id="66f5e-497">You may choose to use the overload of RegisterClientScriptBlock that takes a fourth argument.</span></span> <span data-ttu-id="66f5e-498">第四个参数是一个布尔值，指定 ASP.NET 应为您添加脚本元素。</span><span class="sxs-lookup"><span data-stu-id="66f5e-498">The fourth argument is a Boolean that specifies whether or not ASP.NET should add script elements for you.</span></span> <span data-ttu-id="66f5e-499">如果此参数为**true**，你的脚本不应包含的脚本元素显式。</span><span class="sxs-lookup"><span data-stu-id="66f5e-499">If this argument is **true**, your script should not include the script elements explicitly.</span></span>

<span data-ttu-id="66f5e-500">IsClientScriptBlockRegistered 方法用于确定是否已注册的脚本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-500">Use the IsClientScriptBlockRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="66f5e-501">这样您就可以避免尝试重新注册已注册的脚本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-501">This allows you to avoid an attempt to re-register a script that has already been registered.</span></span>

### <a name="registerclientscriptinclude-new-in-20"></a><span data-ttu-id="66f5e-502">RegisterClientScriptInclude （中的新增 2.0)</span><span class="sxs-lookup"><span data-stu-id="66f5e-502">RegisterClientScriptInclude (New in 2.0)</span></span>

<span data-ttu-id="66f5e-503">RegisterClientScriptInclude 标记创建的脚本块链接到外部脚本文件。</span><span class="sxs-lookup"><span data-stu-id="66f5e-503">The RegisterClientScriptInclude tag creates a script block that links to an external script file.</span></span> <span data-ttu-id="66f5e-504">它具有两个重载。</span><span class="sxs-lookup"><span data-stu-id="66f5e-504">It has two overloads.</span></span> <span data-ttu-id="66f5e-505">其中一个使用密钥和 URL。</span><span class="sxs-lookup"><span data-stu-id="66f5e-505">One takes a key and a URL.</span></span> <span data-ttu-id="66f5e-506">第二个将添加指定的类型的第三个自变量。</span><span class="sxs-lookup"><span data-stu-id="66f5e-506">The second adds a third argument specifying the type.</span></span>

<span data-ttu-id="66f5e-507">例如，下面的代码生成一个脚本块链接到 jsfunctions.js 在应用程序的脚本文件夹的根目录中：</span><span class="sxs-lookup"><span data-stu-id="66f5e-507">For example, the following code generates a script block that links to jsfunctions.js in the root of the scripts folder of the application:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

<span data-ttu-id="66f5e-508">此代码生成所呈现的页面中的以下代码：</span><span class="sxs-lookup"><span data-stu-id="66f5e-508">This code produces the following code in the rendered page:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> <span data-ttu-id="66f5e-509">脚本块呈现在页的底部。</span><span class="sxs-lookup"><span data-stu-id="66f5e-509">The script block is rendered at the bottom of the page.</span></span>


<span data-ttu-id="66f5e-510">IsClientScriptIncludeRegistered 方法用于确定是否已注册的脚本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-510">Use the IsClientScriptIncludeRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="66f5e-511">这样您就可以避免尝试重新注册的脚本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-511">This allows you to avoid an attempt to re-register a script.</span></span>

## <a name="registerstartupscript"></a><span data-ttu-id="66f5e-512">RegisterStartupScript</span><span class="sxs-lookup"><span data-stu-id="66f5e-512">RegisterStartupScript</span></span>

<span data-ttu-id="66f5e-513">RegisterStartupScript 方法采用与 RegisterClientScriptBlock 方法相同的参数。</span><span class="sxs-lookup"><span data-stu-id="66f5e-513">The RegisterStartupScript method takes the same arguments as the RegisterClientScriptBlock method.</span></span> <span data-ttu-id="66f5e-514">在页面加载后但 OnLoad 客户端事件之前，将执行注册 RegisterStartupScript 脚本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-514">A script registered with RegisterStartupScript executes after the page loads but before the OnLoad client-side event.</span></span> <span data-ttu-id="66f5e-515">在 1.X RegisterStartupScript 与已注册的脚本已被放只需在关闭前&lt;窗体窗体&gt;标记时与 RegisterClientScriptBlock 已注册的脚本已被放在打开后立即&lt;窗体&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="66f5e-515">In 1.X, scripts registered with RegisterStartupScript were placed just before the closing &lt;/form&gt; tag while scripts registered with RegisterClientScriptBlock were placed immediately after the opening &lt;form&gt; tag.</span></span> <span data-ttu-id="66f5e-516">在 ASP.NET 2.0 中，同时位于立即在关闭前&lt;窗体窗体&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="66f5e-516">In ASP.NET 2.0, both are placed immediately before the closing &lt;/form&gt; tag.</span></span>

> [!NOTE]
> <span data-ttu-id="66f5e-517">如果对 RegisterStartupScript 注册了一个函数，该函数将不会执行，直到显式需在客户端代码中调用它即可。</span><span class="sxs-lookup"><span data-stu-id="66f5e-517">If you register a function with RegisterStartupScript, that function will not execute until you explicitly call it in client-side code.</span></span>


<span data-ttu-id="66f5e-518">使用 IsStartupScriptRegistered 方法确定是否已注册脚本，从而避免尝试重新注册的脚本。</span><span class="sxs-lookup"><span data-stu-id="66f5e-518">Use the IsStartupScriptRegistered method to determine if a script has already been registered and avoid an attempt to re-register a script.</span></span>

## <a name="other-clientscriptmanager-methods"></a><span data-ttu-id="66f5e-519">其他 ClientScriptManager 方法</span><span class="sxs-lookup"><span data-stu-id="66f5e-519">Other ClientScriptManager Methods</span></span>

<span data-ttu-id="66f5e-520">以下是一些 ClientScriptManager 类的其他有用方法。</span><span class="sxs-lookup"><span data-stu-id="66f5e-520">Here are some of the other useful methods of the ClientScriptManager class.</span></span>


|  <span data-ttu-id="66f5e-521"><strong>GetCallbackEventReference</strong></span><span class="sxs-lookup"><span data-stu-id="66f5e-521"><strong>GetCallbackEventReference</strong></span></span>   |                                                 <span data-ttu-id="66f5e-522">请参阅本模块前面的脚本回调。</span><span class="sxs-lookup"><span data-stu-id="66f5e-522">See script callbacks earlier in this module.</span></span>                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <span data-ttu-id="66f5e-523"><strong>GetPostBackClientHyperlink</strong></span><span class="sxs-lookup"><span data-stu-id="66f5e-523"><strong>GetPostBackClientHyperlink</strong></span></span>  |                <span data-ttu-id="66f5e-524">获取 JavaScript 参考 (javascript:&lt;调用&gt;) 可以用于从客户端事件发布。</span><span class="sxs-lookup"><span data-stu-id="66f5e-524">Gets a JavaScript reference (javascript:&lt;call&gt;) that can be used to post back from a client-side event.</span></span>                 |
|  <span data-ttu-id="66f5e-525"><strong>GetPostBackEventReference</strong></span><span class="sxs-lookup"><span data-stu-id="66f5e-525"><strong>GetPostBackEventReference</strong></span></span>   |                                   <span data-ttu-id="66f5e-526">获取可用于启动重新从客户端 post 的字符串。</span><span class="sxs-lookup"><span data-stu-id="66f5e-526">Gets a string that can be used to initiate a post back from the client.</span></span>                                    |
|      <span data-ttu-id="66f5e-527"><strong>GetWebResourceUrl</strong></span><span class="sxs-lookup"><span data-stu-id="66f5e-527"><strong>GetWebResourceUrl</strong></span></span>       | <span data-ttu-id="66f5e-528">返回到嵌入到程序集中的资源的 URL。</span><span class="sxs-lookup"><span data-stu-id="66f5e-528">Returns a URL to a resource that is embedded in an assembly.</span></span> <span data-ttu-id="66f5e-529">必须与结合使用<strong>RegisterClientScriptResource</strong>。</span><span class="sxs-lookup"><span data-stu-id="66f5e-529">Must be used in conjunction with <strong>RegisterClientScriptResource</strong>.</span></span> |
| <span data-ttu-id="66f5e-530"><strong>RegisterClientScriptResource</strong></span><span class="sxs-lookup"><span data-stu-id="66f5e-530"><strong>RegisterClientScriptResource</strong></span></span> |     <span data-ttu-id="66f5e-531">注册页的 Web 资源。</span><span class="sxs-lookup"><span data-stu-id="66f5e-531">Registers a Web resource with the page.</span></span> <span data-ttu-id="66f5e-532">这些是资源嵌入程序集中并由新 WebResource.axd 处理程序处理。</span><span class="sxs-lookup"><span data-stu-id="66f5e-532">These are resources embedded in an assembly and handled by the new WebResource.axd handler.</span></span>      |
|     <span data-ttu-id="66f5e-533"><strong>RegisterHiddenField</strong></span><span class="sxs-lookup"><span data-stu-id="66f5e-533"><strong>RegisterHiddenField</strong></span></span>      |                                                 <span data-ttu-id="66f5e-534">注册页的隐藏的表单域。</span><span class="sxs-lookup"><span data-stu-id="66f5e-534">Registers a hidden form field with the page.</span></span>                                                 |
|  <span data-ttu-id="66f5e-535"><strong>RegisterOnSubmitStatement</strong></span><span class="sxs-lookup"><span data-stu-id="66f5e-535"><strong>RegisterOnSubmitStatement</strong></span></span>   |                                  <span data-ttu-id="66f5e-536">注册在提交 HTML 表单时执行的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="66f5e-536">Registers client-side code that executes when the HTML form is submitted.</span></span>                                   |

