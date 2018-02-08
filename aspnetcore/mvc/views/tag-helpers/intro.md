---
title: "ASP.NET Core 中的标记帮助程序"
author: rick-anderson
description: "了解标记帮助程序的定义及其在 ASP.NET Core 中的用法。"
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 7/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/intro
ms.openlocfilehash: 939eccd45ec437f379fb9349c24246cc0683528b
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-tag-helpers-in-aspnet-core"></a><span data-ttu-id="5052c-103">ASP.NET Core 中标记帮助程序的介绍</span><span class="sxs-lookup"><span data-stu-id="5052c-103">Introduction to Tag Helpers in ASP.NET Core</span></span> 

<span data-ttu-id="5052c-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5052c-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="what-are-tag-helpers"></a><span data-ttu-id="5052c-105">什么是标记帮助程序？</span><span class="sxs-lookup"><span data-stu-id="5052c-105">What are Tag Helpers?</span></span>

<span data-ttu-id="5052c-106">标记帮助程序使服务器端代码可以在 Razor 文件中参与创建和呈现 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="5052c-106">Tag Helpers enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span> <span data-ttu-id="5052c-107">例如，内置 `ImageTagHelper` 可以将版本号追加到映像名称。</span><span class="sxs-lookup"><span data-stu-id="5052c-107">For example, the built-in `ImageTagHelper` can append a version number to the image name.</span></span> <span data-ttu-id="5052c-108">每当映像发生变化时，服务器都会为映像生成一个新的唯一版本，因此客户端总能获得当前映像（而不是过时的缓存映像）。</span><span class="sxs-lookup"><span data-stu-id="5052c-108">Whenever the image changes, the server generates a new unique version for the image, so clients are guaranteed to get the current image (instead of a stale cached image).</span></span> <span data-ttu-id="5052c-109">有多种常见任务（例如创建窗体、链接，加载资产等）的内置标记帮助程序，公共 GitHub 存储库和 NuGet 包中甚至还有更多可用标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="5052c-109">There are many built-in Tag Helpers for common tasks - such as creating forms, links, loading assets and more - and even more available in public GitHub repositories and as NuGet packages.</span></span> <span data-ttu-id="5052c-110">标记帮助程序使用 C# 创建，基于元素名称、属性名称或父标记以 HTML 元素为目标。</span><span class="sxs-lookup"><span data-stu-id="5052c-110">Tag Helpers are authored in C#, and they target HTML elements based on element name, attribute name, or parent tag.</span></span> <span data-ttu-id="5052c-111">例如，应用 `LabelTagHelper` 属性时，内置 `LabelTagHelper` 可以 HTML `<label>` 元素为目标。</span><span class="sxs-lookup"><span data-stu-id="5052c-111">For example, the built-in `LabelTagHelper` can target the HTML `<label>` element when the `LabelTagHelper` attributes are applied.</span></span> <span data-ttu-id="5052c-112">如果熟悉 [ HTML 帮助程序](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers)，则标记帮助程序将减少 Razor 视图中 HTML 和 C# 之间的显式转换。</span><span class="sxs-lookup"><span data-stu-id="5052c-112">If you're familiar with [HTML Helpers](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers), Tag Helpers reduce the explicit transitions between HTML and C# in Razor views.</span></span> <span data-ttu-id="5052c-113">在很多情况下，HTML 帮助程序为特定标记帮助程序提供了一种替代方法，但标记帮助程序不会替代 HTML 帮助程序，且并非每个 HTML 帮助程序都有对应的标记帮助程序，认识到这点也很重要。</span><span class="sxs-lookup"><span data-stu-id="5052c-113">In many cases, HTML Helpers provide an alternative approach to a specific Tag Helper, but it's important to recognize that Tag Helpers don't replace HTML Helpers and there's not a Tag Helper for each HTML Helper.</span></span> <span data-ttu-id="5052c-114">[标记帮助程序与 HTML 帮助程序的比较](#tag-helpers-compared-to-html-helpers)更详细地介绍了两者之间的差异。</span><span class="sxs-lookup"><span data-stu-id="5052c-114">[Tag Helpers compared to HTML Helpers](#tag-helpers-compared-to-html-helpers) explains the differences in more detail.</span></span>

## <a name="what-tag-helpers-provide"></a><span data-ttu-id="5052c-115">标记帮助程序的功能</span><span class="sxs-lookup"><span data-stu-id="5052c-115">What Tag Helpers provide</span></span>

<span data-ttu-id="5052c-116">**HTML 友好开发体验** 在多数情况下，使用标记帮助程序的 Razor 标记看起来像是标准 HTML。</span><span class="sxs-lookup"><span data-stu-id="5052c-116">**An HTML-friendly development experience** For the most part, Razor markup using Tag Helpers looks like standard HTML.</span></span> <span data-ttu-id="5052c-117">熟悉 HTML/CSS/JavaScript 的前端设计师，无需学习 C# Razor 语法即可编辑 Razor。</span><span class="sxs-lookup"><span data-stu-id="5052c-117">Front-end designers conversant with HTML/CSS/JavaScript can edit Razor without learning C# Razor syntax.</span></span>

<span data-ttu-id="5052c-118">**用于创建 HTML 和 Razor 标记的丰富 IntelliSense 环境** 这与 HTML 帮助程序形成鲜明对比，HTML 帮助程序是 Razor 视图中标记的曾用服务器端创建方法。</span><span class="sxs-lookup"><span data-stu-id="5052c-118">**A rich IntelliSense environment for creating HTML and Razor markup** This is in sharp contrast to HTML Helpers, the previous approach to server-side creation of markup in Razor views.</span></span> <span data-ttu-id="5052c-119">[标记帮助程序与 HTML 帮助程序的比较](#tag-helpers-compared-to-html-helpers)更详细地介绍了两者之间的差异。</span><span class="sxs-lookup"><span data-stu-id="5052c-119">[Tag Helpers compared to HTML Helpers](#tag-helpers-compared-to-html-helpers) explains the differences in more detail.</span></span> <span data-ttu-id="5052c-120">[标记帮助程序的 IntelliSense 支持](#intellisense-support-for-tag-helpers)解释了 IntelliSense 环境。</span><span class="sxs-lookup"><span data-stu-id="5052c-120">[IntelliSense support for Tag Helpers](#intellisense-support-for-tag-helpers) explains the IntelliSense environment.</span></span> <span data-ttu-id="5052c-121">即使是熟悉 Razor C# 语法的开发人员，使用标记帮助程序也比编写 C# Razor 标记更高效。</span><span class="sxs-lookup"><span data-stu-id="5052c-121">Even developers experienced with Razor C# syntax are more productive using Tag Helpers than writing C# Razor markup.</span></span>

<span data-ttu-id="5052c-122">**使用仅在服务器上可用的信息，可提高生产力，并能生成更稳定、可靠和可维护的代码** 例如，过去更新映像时，必须在更改映像时更改映像名称。</span><span class="sxs-lookup"><span data-stu-id="5052c-122">**A way to make you more productive and able to produce more robust, reliable, and maintainable code using information only available on the server** For example, historically the mantra on updating images was to change the name of the image when you change the image.</span></span> <span data-ttu-id="5052c-123">出于性能原因，要主动缓存映像，而若不更改映像的名称，客户端就可能获得过时的副本。</span><span class="sxs-lookup"><span data-stu-id="5052c-123">Images should be aggressively cached for performance reasons, and unless you change the name of an image, you risk clients getting a stale copy.</span></span> <span data-ttu-id="5052c-124">以前，编辑完映像后，必须更改名称，而且需要更新 Web 应用中对该映像的每个引用。</span><span class="sxs-lookup"><span data-stu-id="5052c-124">Historically, after an image was edited, the name had to be changed and each reference to the image in the web app needed to be updated.</span></span> <span data-ttu-id="5052c-125">这不仅大费周章，还容易出错（可能会漏掉某个引用、意外输入错误的字符串等等）内置 `ImageTagHelper` 可自动执行此操作。</span><span class="sxs-lookup"><span data-stu-id="5052c-125">Not only is this very labor intensive, it's also error prone (you could miss a reference, accidentally enter the wrong string, etc.) The built-in `ImageTagHelper` can do this for you automatically.</span></span> <span data-ttu-id="5052c-126">`ImageTagHelper` 可将版本号追加到映像名称，这样每当映像出现更改时，服务器都会自动为该映像生成新的唯一版本。</span><span class="sxs-lookup"><span data-stu-id="5052c-126">The `ImageTagHelper` can append a version number to the image name, so whenever the image changes, the server automatically generates a new unique version for the image.</span></span> <span data-ttu-id="5052c-127">客户端总是能获得最新映像。</span><span class="sxs-lookup"><span data-stu-id="5052c-127">Clients are guaranteed to get the current image.</span></span> <span data-ttu-id="5052c-128">使用 `ImageTagHelper` 实质上是免费获得稳健性而节省劳动力。</span><span class="sxs-lookup"><span data-stu-id="5052c-128">This robustness and labor savings comes essentially free by using the `ImageTagHelper`.</span></span>

<span data-ttu-id="5052c-129">大多数内置标记帮助程序以现有 HTML 元素为目标，为该元素提供服务器端属性。</span><span class="sxs-lookup"><span data-stu-id="5052c-129">Most of the built-in Tag Helpers target existing HTML elements and provide server-side attributes for the element.</span></span> <span data-ttu-id="5052c-130">例如，Views/Account 文件夹中的许多视图都使用的 `<input>` 元素包含 `asp-for` 特性，它会将指定模型属性的名称提取到呈现的 HTML 中。</span><span class="sxs-lookup"><span data-stu-id="5052c-130">For example, the `<input>` element used in many of the views in the *Views/Account* folder contains the `asp-for` attribute, which extracts the name of the specified model property into the rendered HTML.</span></span> <span data-ttu-id="5052c-131">以下 Razor 标记：</span><span class="sxs-lookup"><span data-stu-id="5052c-131">The following Razor markup:</span></span>

```cshtml
<label asp-for="Email"></label>
```

<span data-ttu-id="5052c-132">生成以下 HTML：</span><span class="sxs-lookup"><span data-stu-id="5052c-132">Generates the following HTML:</span></span>

```cshtml
<label for="Email">Email</label>
```

<span data-ttu-id="5052c-133">通过 `LabelTagHelper` 中的 `For` 属性，可使用 `asp-for` 特性。</span><span class="sxs-lookup"><span data-stu-id="5052c-133">The `asp-for` attribute is made available by the `For` property in the `LabelTagHelper`.</span></span> <span data-ttu-id="5052c-134">请参阅[创作标记帮助程序](authoring.md)，获取详细信息。</span><span class="sxs-lookup"><span data-stu-id="5052c-134">See [Authoring Tag Helpers](authoring.md) for more information.</span></span>

## <a name="managing-tag-helper-scope"></a><span data-ttu-id="5052c-135">管理标记帮助程序作用域</span><span class="sxs-lookup"><span data-stu-id="5052c-135">Managing Tag Helper scope</span></span>

<span data-ttu-id="5052c-136">标记帮助程序作用域由 `@addTagHelper`、`@removeTagHelper` 和“!”选择退出字符联合控制。</span><span class="sxs-lookup"><span data-stu-id="5052c-136">Tag Helpers scope is controlled by a combination of `@addTagHelper`, `@removeTagHelper`, and the "!" opt-out character.</span></span>

<a name="add-helper-label"></a>

### <a name="addtaghelper-makes-tag-helpers-available"></a><span data-ttu-id="5052c-137">使用 `@addTagHelper` 添加标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="5052c-137">`@addTagHelper` makes Tag Helpers available</span></span>

<span data-ttu-id="5052c-138">如果创建名为 AuthoringTagHelpers的新 ASP.NET Core Web 应用（无身份验证），将向项目添加以下 Views/_ViewImports.cshtml 文件：</span><span class="sxs-lookup"><span data-stu-id="5052c-138">If you create a new ASP.NET Core web app named *AuthoringTagHelpers* (with no authentication), the following *Views/_ViewImports.cshtml* file will be added to your project:</span></span>

[!code-cshtml[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImportsCopy.cshtml?highlight=2&range=2-3)]

<span data-ttu-id="5052c-139">`@addTagHelper` 指令让视图可以使用标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="5052c-139">The `@addTagHelper` directive makes Tag Helpers available to the view.</span></span> <span data-ttu-id="5052c-140">在此示例中，视图文件是 Views/_ViewImports.cshtml，“Views”文件夹及其子目录中的所有视图文件都会默认继承它，使得标记帮助程序可用。</span><span class="sxs-lookup"><span data-stu-id="5052c-140">In this case, the view file is *Views/_ViewImports.cshtml*, which by default is inherited by all view files in the *Views* folder and sub-directories; making Tag Helpers available.</span></span> <span data-ttu-id="5052c-141">上面的代码使用通配符语法（“\*”），指定程序集 (Microsoft.AspNetCore.Mvc.TagHelpers) 中的所有标记帮助程序对于 Views 目录或子目录中的所有视图文件可用。</span><span class="sxs-lookup"><span data-stu-id="5052c-141">The code above uses the wildcard syntax ("\*") to specify that all Tag Helpers in the specified assembly (*Microsoft.AspNetCore.Mvc.TagHelpers*) will be available to every view file in the *Views* directory or sub-directory.</span></span> <span data-ttu-id="5052c-142">`@addTagHelper` 后第一个参数指定要加载的标记帮助程序（我们使用“\*”指定加载所有标记帮助程序），第二个参数“Microsoft.AspNetCore.Mvc.TagHelpers”指定包含标记帮助程序的程序集。</span><span class="sxs-lookup"><span data-stu-id="5052c-142">The first parameter after `@addTagHelper` specifies the Tag Helpers to load (we are using "\*" for all Tag Helpers), and the second parameter "Microsoft.AspNetCore.Mvc.TagHelpers" specifies the assembly containing the Tag Helpers.</span></span> <span data-ttu-id="5052c-143">Microsoft.AspNetCore.Mvc.TagHelpers 是内置 ASP.NET Core 标记帮助程序的程序集。</span><span class="sxs-lookup"><span data-stu-id="5052c-143">*Microsoft.AspNetCore.Mvc.TagHelpers* is the assembly for the built-in ASP.NET Core Tag Helpers.</span></span>

<span data-ttu-id="5052c-144">要公开此项目中的所有标记帮助程序（将创建名为 AuthoringTagHelpers 的程序集），可使用以下内容：</span><span class="sxs-lookup"><span data-stu-id="5052c-144">To expose all of the Tag Helpers in this project (which creates an assembly named *AuthoringTagHelpers*), you would use the following:</span></span>

[!code-cshtml[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImportsCopy.cshtml?highlight=3)]

<span data-ttu-id="5052c-145">如果项目包含具有默认命名空间 (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`) 的 `EmailTagHelper`，则可提供标记帮助程序的完全限定名称 (FQN)：</span><span class="sxs-lookup"><span data-stu-id="5052c-145">If your project contains an `EmailTagHelper` with the default namespace (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), you can provide the fully qualified name (FQN) of the Tag Helper:</span></span>

```cshtml
@using AuthoringTagHelpers
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
@addTagHelper AuthoringTagHelpers.TagHelpers.EmailTagHelper, AuthoringTagHelpers
```

<span data-ttu-id="5052c-146">若要使用 FQN 将标记帮助程序添加到视图，请首先添加 FQN (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`)，然后添加程序集名称 (AuthoringTagHelpers)。</span><span class="sxs-lookup"><span data-stu-id="5052c-146">To add a Tag Helper to a view using an FQN, you first add the FQN (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), and then the assembly name (*AuthoringTagHelpers*).</span></span> <span data-ttu-id="5052c-147">大多数开发人员更喜欢使用“\*”通配符语法。</span><span class="sxs-lookup"><span data-stu-id="5052c-147">Most developers prefer to use the  "\*" wildcard syntax.</span></span> <span data-ttu-id="5052c-148">使用通配符语法，可在 FQN 中插入通配符“\*”作为后缀。</span><span class="sxs-lookup"><span data-stu-id="5052c-148">The wildcard syntax allows you to insert the wildcard character "\*" as the suffix in an FQN.</span></span> <span data-ttu-id="5052c-149">例如，以下任何指令都将引入 `EmailTagHelper`：</span><span class="sxs-lookup"><span data-stu-id="5052c-149">For example, any of the following directives will bring in the `EmailTagHelper`:</span></span>

```cshtml
@addTagHelper AuthoringTagHelpers.TagHelpers.E*, AuthoringTagHelpers
@addTagHelper AuthoringTagHelpers.TagHelpers.Email*, AuthoringTagHelpers
```

<span data-ttu-id="5052c-150">如前所述，将 `@addTagHelper` 指令添加到 Views/_ViewImports.cshtml 文件，将使标记帮助程序对于 Views 目录及子目录中的所有视图文件可用。</span><span class="sxs-lookup"><span data-stu-id="5052c-150">As mentioned previously, adding the `@addTagHelper` directive to the *Views/_ViewImports.cshtml* file makes the Tag Helper available to all view files in the *Views* directory and sub-directories.</span></span> <span data-ttu-id="5052c-151">如果想选择仅对特定视图公开标记帮助程序，可在这些视图文件中使用 `@addTagHelper` 指令。</span><span class="sxs-lookup"><span data-stu-id="5052c-151">You can use the `@addTagHelper` directive in specific view files if you want to opt-in to exposing the Tag Helper to only those views.</span></span>

<a name="remove-razor-directives-label"></a>

### <a name="removetaghelper-removes-tag-helpers"></a><span data-ttu-id="5052c-152">`@removeTagHelper` 删除标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="5052c-152">`@removeTagHelper` removes Tag Helpers</span></span>

<span data-ttu-id="5052c-153">`@removeTagHelper` 与 `@addTagHelper` 具有相同的两个参数，它会删除之前添加的标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="5052c-153">The `@removeTagHelper` has the same two parameters as `@addTagHelper`, and it removes a Tag Helper that was previously added.</span></span> <span data-ttu-id="5052c-154">例如，应用于特定视图的 `@removeTagHelper` 会删除该视图中的指定标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="5052c-154">For example, `@removeTagHelper` applied to a specific view removes the specified Tag Helper from the view.</span></span> <span data-ttu-id="5052c-155">在 Views/Folder/_ViewImports.cshtml 文件中使用 `@removeTagHelper`，将从 Folder 中的所有视图删除指定的标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="5052c-155">Using `@removeTagHelper` in a *Views/Folder/_ViewImports.cshtml* file removes the specified Tag Helper from all of the views in *Folder*.</span></span>

### <a name="controlling-tag-helper-scope-with-the-viewimportscshtml-file"></a><span data-ttu-id="5052c-156">使用 _ViewImports.cshtml 文件控制标记帮助程序作用域</span><span class="sxs-lookup"><span data-stu-id="5052c-156">Controlling Tag Helper scope with the *_ViewImports.cshtml* file</span></span>

<span data-ttu-id="5052c-157">可将 _ViewImports.cshtml 添加到任何视图文件夹，视图引擎将同时应用该文件和 Views/_ViewImports.cshtml 文件中的指令。</span><span class="sxs-lookup"><span data-stu-id="5052c-157">You can add a *_ViewImports.cshtml* to any view folder, and the view engine applies the directives from both that file and the *Views/_ViewImports.cshtml* file.</span></span> <span data-ttu-id="5052c-158">如果为 Home 视图添加空的 Views/Home/_ViewImports.cshtml 文件，则不会发生任何更改，因为 _ViewImports.cshtml 文件是附加的。</span><span class="sxs-lookup"><span data-stu-id="5052c-158">If you added an empty *Views/Home/_ViewImports.cshtml* file for the *Home* views, there would be no change because the *_ViewImports.cshtml* file is additive.</span></span> <span data-ttu-id="5052c-159">添加到 Views/Home/_ViewImports.cshtml 文件（不在默认 Views/_ViewImports.cshtml 文件中）的任何 `@addTagHelper` 指令，都只会将这些标记帮助程序公开给 Home 文件夹中的视图。</span><span class="sxs-lookup"><span data-stu-id="5052c-159">Any `@addTagHelper` directives you add to the *Views/Home/_ViewImports.cshtml* file (that are not in the default *Views/_ViewImports.cshtml* file) would expose those Tag Helpers to views only in the *Home* folder.</span></span>

<a name="opt-out"></a>

### <a name="opting-out-of-individual-elements"></a><span data-ttu-id="5052c-160">选择退出各个元素</span><span class="sxs-lookup"><span data-stu-id="5052c-160">Opting out of individual elements</span></span>

<span data-ttu-id="5052c-161">使用标记帮助程序选择退出字符（“!”），可在元素级别禁用标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="5052c-161">You can disable a Tag Helper at the element level with the Tag Helper opt-out character ("!").</span></span> <span data-ttu-id="5052c-162">例如，使用标记帮助程序选择退出字符在 `<span>` 中禁用 `Email` 验证：</span><span class="sxs-lookup"><span data-stu-id="5052c-162">For example, `Email` validation is disabled in the `<span>` with the Tag Helper opt-out character:</span></span>

```cshtml
<!span asp-validation-for="Email" class="text-danger"></!span>
```

<span data-ttu-id="5052c-163">须将标记帮助程序选择退出字符应用于开始和结束标记。</span><span class="sxs-lookup"><span data-stu-id="5052c-163">You must apply the Tag Helper opt-out character to the opening and closing tag.</span></span> <span data-ttu-id="5052c-164">（将选择退出字符添加到开始标记时，Visual Studio 编辑器会自动为结束标记添加相应字符）。</span><span class="sxs-lookup"><span data-stu-id="5052c-164">(The Visual Studio editor automatically adds the opt-out character to the closing tag when you add one to the opening tag).</span></span> <span data-ttu-id="5052c-165">添加选择退出字符后，元素和标记帮助程序属性不再以独特字体显示。</span><span class="sxs-lookup"><span data-stu-id="5052c-165">After you add the opt-out character, the element and Tag Helper attributes are no longer displayed in a distinctive font.</span></span>

<a name="prefix-razor-directives-label"></a>

### <a name="using-taghelperprefix-to-make-tag-helper-usage-explicit"></a><span data-ttu-id="5052c-166">使用 `@tagHelperPrefix` 阐明标记帮助程序用途</span><span class="sxs-lookup"><span data-stu-id="5052c-166">Using `@tagHelperPrefix` to make Tag Helper usage explicit</span></span>

<span data-ttu-id="5052c-167">`@tagHelperPrefix` 指令可指定一个标记前缀字符串，以启用标记帮助程序支持并阐明标记帮助程序用途。</span><span class="sxs-lookup"><span data-stu-id="5052c-167">The `@tagHelperPrefix` directive allows you to specify a tag prefix string to enable Tag Helper support and to make Tag Helper usage explicit.</span></span> <span data-ttu-id="5052c-168">例如，可以将以下标记添加到 Views/_ViewImports.cshtml 文件：</span><span class="sxs-lookup"><span data-stu-id="5052c-168">For example, you could add the following markup to the *Views/_ViewImports.cshtml* file:</span></span>

```cshtml
@tagHelperPrefix th:
```
<span data-ttu-id="5052c-169">在以下代码图像中，标记帮助程序前缀设置为 `th:`，所以只有使用前缀 `th:` 的元素才支持标记帮助程序（可使用标记帮助程序的元素以独特字体显示）。</span><span class="sxs-lookup"><span data-stu-id="5052c-169">In the code image below, the Tag Helper prefix is set to `th:`, so only those elements using the prefix `th:` support Tag Helpers (Tag Helper-enabled elements have a distinctive font).</span></span> <span data-ttu-id="5052c-170">`<label>` 和 `<input>` 元素具有标记帮助程序前缀，可使用标记帮助程序，而 `<span>` 元素则相反。</span><span class="sxs-lookup"><span data-stu-id="5052c-170">The `<label>` and `<input>` elements have the Tag Helper prefix and are Tag Helper-enabled, while the `<span>` element doesn't.</span></span>

![图像](intro/_static/thp.png)

<span data-ttu-id="5052c-172">适用于 `@addTagHelper` 的层次结构规则也适用于 `@tagHelperPrefix`。</span><span class="sxs-lookup"><span data-stu-id="5052c-172">The same hierarchy rules that apply to `@addTagHelper` also apply to `@tagHelperPrefix`.</span></span>

## <a name="intellisense-support-for-tag-helpers"></a><span data-ttu-id="5052c-173">标记帮助程序的 Intellisense 支持</span><span class="sxs-lookup"><span data-stu-id="5052c-173">IntelliSense support for Tag Helpers</span></span>

<span data-ttu-id="5052c-174">在 Visual Studio 中创建新的 ASP.NET Web 应用时，会添加 NuGet 包“Microsoft.AspNetCore.Razor.Tools”。</span><span class="sxs-lookup"><span data-stu-id="5052c-174">When you create a new ASP.NET web app in Visual Studio, it adds the NuGet package "Microsoft.AspNetCore.Razor.Tools".</span></span> <span data-ttu-id="5052c-175">这是添加标记帮助程序工具的包。</span><span class="sxs-lookup"><span data-stu-id="5052c-175">This is the package that adds Tag Helper tooling.</span></span>

<span data-ttu-id="5052c-176">请考虑编写 HTML `<label>` 元素。</span><span class="sxs-lookup"><span data-stu-id="5052c-176">Consider writing an HTML `<label>` element.</span></span> <span data-ttu-id="5052c-177">只要在 Visual Studio 编辑器中输入 `<l`，IntelliSense 就会显示匹配的元素：</span><span class="sxs-lookup"><span data-stu-id="5052c-177">As soon as you enter `<l` in the Visual Studio editor, IntelliSense displays matching elements:</span></span>

![图像](intro/_static/label.png)

<span data-ttu-id="5052c-179">不仅会获得 HTML 帮助，还会有图标（下方带有“<>”的“@" symbol with "）</span><span class="sxs-lookup"><span data-stu-id="5052c-179">Not only do you get HTML help, but the icon (the "@" symbol with "<>" under it).</span></span>

![图像](intro/_static/tagSym.png)

<span data-ttu-id="5052c-181">将该元素标识为标记帮助程序的目标。</span><span class="sxs-lookup"><span data-stu-id="5052c-181">identifies the element as targeted by Tag Helpers.</span></span> <span data-ttu-id="5052c-182">纯 HTML 元素（如 `fieldset`）显示“<>”图标。</span><span class="sxs-lookup"><span data-stu-id="5052c-182">Pure HTML elements (such as the `fieldset`) display the "<>" icon.</span></span>

<span data-ttu-id="5052c-183">纯 HTML `<label>` 标记以棕色字体显示 HTML 标记（使用默认 Visual Studio 颜色主题时），以红色字体显示属性，并以蓝色字体显示属性值。</span><span class="sxs-lookup"><span data-stu-id="5052c-183">A pure HTML `<label>` tag displays the HTML tag (with the default Visual Studio color theme) in a brown font, the attributes in red, and the attribute values in blue.</span></span>

![图像](intro/_static/LableHtmlTag.png)

<span data-ttu-id="5052c-185">输入 `<label` 后，IntelliSense 会列出可用的 HTML/CSS 属性和以标记帮助程序为目标的属性：</span><span class="sxs-lookup"><span data-stu-id="5052c-185">After you enter `<label`, IntelliSense lists the available HTML/CSS attributes and the Tag Helper-targeted attributes:</span></span>

![图像](intro/_static/labelattr.png)

<span data-ttu-id="5052c-187">通过 IntelliSense 语句完成功能，按 Tab 键即可用选择的值完成语句：</span><span class="sxs-lookup"><span data-stu-id="5052c-187">IntelliSense statement completion allows you to enter the tab key to complete the statement with the selected value:</span></span>

![图像](intro/_static/stmtcomplete.png)

<span data-ttu-id="5052c-189">只要输入标记帮助程序属性，标记和属性字体就会更改。</span><span class="sxs-lookup"><span data-stu-id="5052c-189">As soon as a Tag Helper attribute is entered, the tag and attribute fonts change.</span></span> <span data-ttu-id="5052c-190">如果使用默认的 Visual Studio“蓝色”或“浅色”颜色主题，则字体是粗体紫色。</span><span class="sxs-lookup"><span data-stu-id="5052c-190">Using the default Visual Studio "Blue" or "Light" color theme, the font is bold purple.</span></span> <span data-ttu-id="5052c-191">如果使用“深色”主题，则字体为粗体青色。</span><span class="sxs-lookup"><span data-stu-id="5052c-191">If you're using the "Dark" theme the font is bold teal.</span></span> <span data-ttu-id="5052c-192">本文档中的图像在使用默认主题时截取的。</span><span class="sxs-lookup"><span data-stu-id="5052c-192">The images in this document were taken using the default theme.</span></span>

![图像](intro/_static/labelaspfor2.png)

<span data-ttu-id="5052c-194">可在双引号 ("") 内输入 Visual Studio CompleteWord 快捷方式（[默认值](https://docs.microsoft.com/visualstudio/ide/default-keyboard-shortcuts-in-visual-studio)为 Ctrl+空格键），即可使用 C#，就像在 C# 类中一样。</span><span class="sxs-lookup"><span data-stu-id="5052c-194">You can enter the Visual Studio *CompleteWord* shortcut (Ctrl +spacebar is the [default](https://docs.microsoft.com/visualstudio/ide/default-keyboard-shortcuts-in-visual-studio) inside the double quotes (""), and you are now in C#, just like you would be in a C# class.</span></span> <span data-ttu-id="5052c-195">IntelliSense 会显示页面模型上的所有方法和属性。</span><span class="sxs-lookup"><span data-stu-id="5052c-195">IntelliSense displays all the methods and properties on the page model.</span></span> <span data-ttu-id="5052c-196">由于属性类型是 `ModelExpression`，所以这些方法和属性可用。</span><span class="sxs-lookup"><span data-stu-id="5052c-196">The methods and properties are available because the property type is `ModelExpression`.</span></span> <span data-ttu-id="5052c-197">在下图中，我正在编辑 `Register` 视图，所以 `RegisterViewModel` 是可用的。</span><span class="sxs-lookup"><span data-stu-id="5052c-197">In the image below, I'm editing the `Register` view, so the `RegisterViewModel` is available.</span></span>

![图像](intro/_static/intellemail.png)

<span data-ttu-id="5052c-199">IntelliSense 会列出页面上模型可用的属性和方法。</span><span class="sxs-lookup"><span data-stu-id="5052c-199">IntelliSense lists the properties and methods available to the model on the page.</span></span> <span data-ttu-id="5052c-200">丰富 IntelliSense 环境可帮助选择 CSS 类：</span><span class="sxs-lookup"><span data-stu-id="5052c-200">The rich IntelliSense environment helps you select the CSS class:</span></span>

![图像](intro/_static/iclass.png)

![图像](intro/_static/intel3.png)

## <a name="tag-helpers-compared-to-html-helpers"></a><span data-ttu-id="5052c-203">标记帮助程序与 HTML 帮助程序的比较</span><span class="sxs-lookup"><span data-stu-id="5052c-203">Tag Helpers compared to HTML Helpers</span></span>

<span data-ttu-id="5052c-204">标记帮助程序附加到 Razor 视图中的 HTML 元素，[HTML 帮助程序](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers)是作为与 Razor 视图中 HTML 交织的方法被调用的。</span><span class="sxs-lookup"><span data-stu-id="5052c-204">Tag Helpers attach to HTML elements in Razor views, while [HTML Helpers](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers) are invoked as methods interspersed with HTML in Razor views.</span></span> <span data-ttu-id="5052c-205">请考虑下列 Razor 标记，它创建具有 CSS 类“caption”的 HTML 标签：</span><span class="sxs-lookup"><span data-stu-id="5052c-205">Consider the following Razor markup, which creates an HTML label with the CSS class "caption":</span></span>

```cshtml
@Html.Label("FirstName", "First Name:", new {@class="caption"})
```

<span data-ttu-id="5052c-206">艾特 (`@`) 符号告诉 Razor 这是代码的开始。</span><span class="sxs-lookup"><span data-stu-id="5052c-206">The at (`@`) symbol tells Razor this is the start of code.</span></span> <span data-ttu-id="5052c-207">接下来的两个参数（“FirstName”和“First Name:”）是字符串，所以 [IntelliSense](https://docs.microsoft.com/visualstudio/ide/using-intellisense) 无法提供帮助。</span><span class="sxs-lookup"><span data-stu-id="5052c-207">The next two parameters ("FirstName" and "First Name:") are strings, so [IntelliSense](https://docs.microsoft.com/visualstudio/ide/using-intellisense) can't help.</span></span> <span data-ttu-id="5052c-208">最后一个参数：</span><span class="sxs-lookup"><span data-stu-id="5052c-208">The last argument:</span></span>

```cshtml
new {@class="caption"}
```

<span data-ttu-id="5052c-209">是用于表示属性的匿名对象。</span><span class="sxs-lookup"><span data-stu-id="5052c-209">Is an anonymous object used to represent attributes.</span></span> <span data-ttu-id="5052c-210">由于 class 是 C# 中的保留关键字，因此要使用 `@` 符号强制 C# 将“@class=”解释为符号（属性名称）。</span><span class="sxs-lookup"><span data-stu-id="5052c-210">Because **class** is a reserved keyword in C#, you use the `@` symbol to force C# to interpret "@class=" as a symbol (property name).</span></span> <span data-ttu-id="5052c-211">对于前端设计师（熟悉 HTML/CSS/JavaScript 及其他客户端技术，但不熟悉 C# 和 Razor 的人），这行代码中大部分内容是陌生是。</span><span class="sxs-lookup"><span data-stu-id="5052c-211">To a front-end designer (someone familiar with HTML/CSS/JavaScript and other client technologies but not familiar with C# and Razor), most of the line is foreign.</span></span> <span data-ttu-id="5052c-212">必须在没有 IntelliSense 帮助的情况下编写整行代码。</span><span class="sxs-lookup"><span data-stu-id="5052c-212">The entire line must be authored with no help from IntelliSense.</span></span>

<span data-ttu-id="5052c-213">使用 `LabelTagHelper`，相同标记可以编写为：</span><span class="sxs-lookup"><span data-stu-id="5052c-213">Using the `LabelTagHelper`, the same markup can be written as:</span></span>

![图像](intro/_static/label2.png)

<span data-ttu-id="5052c-215">使用标记帮助程序版本，只要在 Visual Studio 编辑器中输入 `<l`，IntelliSense 就会显示匹配的元素：</span><span class="sxs-lookup"><span data-stu-id="5052c-215">With the Tag Helper version, as soon as you enter `<l` in the Visual Studio editor, IntelliSense displays matching elements:</span></span>

![图像](intro/_static/label.png)

<span data-ttu-id="5052c-217">IntelliSense 可帮助编写整行。</span><span class="sxs-lookup"><span data-stu-id="5052c-217">IntelliSense helps you write the entire line.</span></span> <span data-ttu-id="5052c-218">`LabelTagHelper` 也默认将 `asp-for` 属性值（“FirstName”）的内容设置为“First Name”：即在属性值中每个大写字母前添加一个空格，将驼峰式大小写的属性转换为由属性名称组成的语句。</span><span class="sxs-lookup"><span data-stu-id="5052c-218">The `LabelTagHelper` also defaults to setting the content of the `asp-for` attribute value ("FirstName") to "First Name"; It converts camel-cased properties to a sentence composed of the property name with a space where each new upper-case letter occurs.</span></span> <span data-ttu-id="5052c-219">在下列标记中：</span><span class="sxs-lookup"><span data-stu-id="5052c-219">In the following markup:</span></span>

![图像](intro/_static/label2.png)

<span data-ttu-id="5052c-221">生成：</span><span class="sxs-lookup"><span data-stu-id="5052c-221">generates:</span></span>

```cshtml
<label class="caption" for="FirstName">First Name</label>
```

<span data-ttu-id="5052c-222">如果将内容添加到 `<label>`，则不会使用由驼峰式大小写转换为语句式书写的内容。</span><span class="sxs-lookup"><span data-stu-id="5052c-222">The camel-cased to sentence-cased content isn't used if you add content to the `<label>`.</span></span> <span data-ttu-id="5052c-223">例如:</span><span class="sxs-lookup"><span data-stu-id="5052c-223">For example:</span></span>

![图像](intro/_static/1stName.png)

<span data-ttu-id="5052c-225">生成：</span><span class="sxs-lookup"><span data-stu-id="5052c-225">generates:</span></span>

```cshtml
<label class="caption" for="FirstName">Name First</label>
```

<span data-ttu-id="5052c-226">以下代码图像显示了由 Visual Studio 2015 包含的旧版 ASP.NET 4.5.x MVC 模板生成的 Views/Account/Register.cshtml Razor 视图的 Form 部分。</span><span class="sxs-lookup"><span data-stu-id="5052c-226">The following code image shows the Form portion of the *Views/Account/Register.cshtml* Razor view generated from the legacy ASP.NET 4.5.x MVC template included with Visual Studio 2015.</span></span>

![图像](intro/_static/regCS.png)

<span data-ttu-id="5052c-228">Visual Studio 编辑器以灰色背景显示 C# 代码。</span><span class="sxs-lookup"><span data-stu-id="5052c-228">The Visual Studio editor displays C# code with a grey background.</span></span> <span data-ttu-id="5052c-229">例如，`AntiForgeryToken` HTML 帮助程序：</span><span class="sxs-lookup"><span data-stu-id="5052c-229">For example, the `AntiForgeryToken` HTML Helper:</span></span>

```cshtml
@Html.AntiForgeryToken()
```

<span data-ttu-id="5052c-230">以灰色背景显示。</span><span class="sxs-lookup"><span data-stu-id="5052c-230">is displayed with a grey background.</span></span> <span data-ttu-id="5052c-231">Register 视图中的标记大部分是 C#。</span><span class="sxs-lookup"><span data-stu-id="5052c-231">Most of the markup in the Register view is C#.</span></span> <span data-ttu-id="5052c-232">将其与使用标记帮助程序的等效方法进行比较：</span><span class="sxs-lookup"><span data-stu-id="5052c-232">Compare that to the equivalent approach using Tag Helpers:</span></span>

![图像](intro/_static/regTH.png)

<span data-ttu-id="5052c-234">与 HTML 帮助程序方法相比，此标记更清晰，更容易阅读、编辑和维护。</span><span class="sxs-lookup"><span data-stu-id="5052c-234">The markup is much cleaner and easier to read, edit, and maintain than the HTML Helpers approach.</span></span> <span data-ttu-id="5052c-235">C# 代码会被减少至服务器需要知道的最小值。</span><span class="sxs-lookup"><span data-stu-id="5052c-235">The C# code is reduced to the minimum that the server needs to know about.</span></span> <span data-ttu-id="5052c-236">Visual Studio 编辑器以独特的字体显示标记帮助程序的目标标记。</span><span class="sxs-lookup"><span data-stu-id="5052c-236">The Visual Studio editor displays markup targeted by a Tag Helper in a distinctive font.</span></span>

<span data-ttu-id="5052c-237">请考虑 Email 组：</span><span class="sxs-lookup"><span data-stu-id="5052c-237">Consider the *Email* group:</span></span>

[!code-csharp[Main](intro/sample/Register.cshtml?range=12-18)]

<span data-ttu-id="5052c-238">每个“asp-”属性都有一个“Email”值，但是“Email”不是字符串。</span><span class="sxs-lookup"><span data-stu-id="5052c-238">Each of the "asp-" attributes has a value of "Email", but "Email" isn't a string.</span></span> <span data-ttu-id="5052c-239">在此上下文中，“Email”是 `RegisterViewModel` 的 C# 模型表达式属性。</span><span class="sxs-lookup"><span data-stu-id="5052c-239">In this context, "Email" is the C# model expression property for the `RegisterViewModel`.</span></span>

<span data-ttu-id="5052c-240">Visual Studio 编辑器可帮助编写注册窗体的标记帮助程序方法中的所有标记，而 Visual Studio 不会为 HTML 帮助程序方法中的大多数代码提供帮助。</span><span class="sxs-lookup"><span data-stu-id="5052c-240">The Visual Studio editor helps you write **all** of the markup in the Tag Helper approach of the register form, while Visual Studio provides no help for most of the code in the HTML Helpers approach.</span></span> <span data-ttu-id="5052c-241">[标记帮助程序的 IntelliSense 支持](#intellisense-support-for-tag-helpers)详细介绍了如何在 Visual Studio 编辑器中使用标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="5052c-241">[IntelliSense support for Tag Helpers](#intellisense-support-for-tag-helpers) goes into detail on working with Tag Helpers in the Visual Studio editor.</span></span>

## <a name="tag-helpers-compared-to-web-server-controls"></a><span data-ttu-id="5052c-242">标记帮助程序与 Web 服务器控件的比较</span><span class="sxs-lookup"><span data-stu-id="5052c-242">Tag Helpers compared to Web Server Controls</span></span>

* <span data-ttu-id="5052c-243">标记帮助程序不拥有与其相关的元素：它们只是参与元素和内容的呈现。</span><span class="sxs-lookup"><span data-stu-id="5052c-243">Tag Helpers don't own the element they're associated with; they simply participate in the rendering of the element and content.</span></span> <span data-ttu-id="5052c-244">ASP.NET [Web 服务器控件](https://msdn.microsoft.com/library/7698y1f0.aspx)在页面上进行声明和调用。</span><span class="sxs-lookup"><span data-stu-id="5052c-244">ASP.NET [Web Server controls](https://msdn.microsoft.com/library/7698y1f0.aspx) are declared and invoked on a page.</span></span>

* <span data-ttu-id="5052c-245">[Web 服务器控件](https://msdn.microsoft.com/library/zsyt68f1.aspx)具有可观的生命周期，因而难以进行开发和调试。</span><span class="sxs-lookup"><span data-stu-id="5052c-245">[Web Server controls](https://msdn.microsoft.com/library/zsyt68f1.aspx) have a non-trivial lifecycle that can make developing and debugging difficult.</span></span>

* <span data-ttu-id="5052c-246">通过 Web 服务器控件，可使用客户端控件向客户端文档对象模型 (DOM) 元素添加功能。</span><span class="sxs-lookup"><span data-stu-id="5052c-246">Web Server controls allow you to add functionality to the client Document Object Model (DOM) elements by using a client control.</span></span> <span data-ttu-id="5052c-247">标记帮助程序没有 DOM。</span><span class="sxs-lookup"><span data-stu-id="5052c-247">Tag Helpers have no DOM.</span></span>

* <span data-ttu-id="5052c-248">Web 服务器控件包括自动浏览器检测。</span><span class="sxs-lookup"><span data-stu-id="5052c-248">Web Server controls include automatic browser detection.</span></span> <span data-ttu-id="5052c-249">标记帮助程序不了解浏览器。</span><span class="sxs-lookup"><span data-stu-id="5052c-249">Tag Helpers have no knowledge of the browser.</span></span>

* <span data-ttu-id="5052c-250">通常不能撰写 Web 服务器控件时，多个标记帮助程序可作用于同一元素（请参阅[避免标记帮助程序冲突](https://docs.microsoft.com/aspnet/core/mvc/views/tag-helpers/authoring#avoiding-tag-helper-conflicts)）。</span><span class="sxs-lookup"><span data-stu-id="5052c-250">Multiple Tag Helpers can act on the same element (see [Avoiding Tag Helper conflicts](https://docs.microsoft.com/aspnet/core/mvc/views/tag-helpers/authoring#avoiding-tag-helper-conflicts) ) while you typically can't compose Web Server controls.</span></span>

* <span data-ttu-id="5052c-251">标记帮助程序可以修改其作用域内 HTML 元素的标记和内容，但不会直接修改页面上的其他内容。</span><span class="sxs-lookup"><span data-stu-id="5052c-251">Tag Helpers can modify the tag and content of HTML elements that they're scoped to, but don't directly modify anything else on a page.</span></span> <span data-ttu-id="5052c-252">Web 服务器控件的作用域较广，并且可以执行影响页面其他部分的操作，从而可能造成意想不到的副作用。</span><span class="sxs-lookup"><span data-stu-id="5052c-252">Web Server controls have a less specific scope and can perform actions that affect other parts of your page; enabling unintended side effects.</span></span>

* <span data-ttu-id="5052c-253">Web 服务器控件使用类型转换器将字符串转换为对象。</span><span class="sxs-lookup"><span data-stu-id="5052c-253">Web Server controls use type converters to convert strings into objects.</span></span> <span data-ttu-id="5052c-254">使用标记帮助程序时，本身就用 C# 语言工作，因此无需进行类型转换。</span><span class="sxs-lookup"><span data-stu-id="5052c-254">With Tag Helpers, you work natively in C#, so you don't need to do type conversion.</span></span>

* <span data-ttu-id="5052c-255">Web 服务器控件使用 [System.ComponentModel](https://docs.microsoft.com/dotnet/api/system.componentmodel) 实现组件和控件的运行时和设计时行为。</span><span class="sxs-lookup"><span data-stu-id="5052c-255">Web Server controls use [System.ComponentModel](https://docs.microsoft.com/dotnet/api/system.componentmodel) to implement the run-time and design-time behavior of components and controls.</span></span> <span data-ttu-id="5052c-256">`System.ComponentModel` 包括用于属性和类型转换器的实现、数据源绑定和组件授权的基类和接口。</span><span class="sxs-lookup"><span data-stu-id="5052c-256">`System.ComponentModel` includes the base classes and interfaces for implementing attributes and type converters, binding to data sources, and licensing components.</span></span> <span data-ttu-id="5052c-257">与通常派生自 `TagHelper` 的标记帮助程序相比，`TagHelper` 基类仅公开两个方法，即 `Process` 和 `ProcessAsync`。</span><span class="sxs-lookup"><span data-stu-id="5052c-257">Contrast that to Tag Helpers, which typically derive from `TagHelper`, and the `TagHelper` base class exposes only two methods, `Process` and `ProcessAsync`.</span></span>

## <a name="customizing-the-tag-helper-element-font"></a><span data-ttu-id="5052c-258">自定义标记帮助程序元素字体</span><span class="sxs-lookup"><span data-stu-id="5052c-258">Customizing the Tag Helper element font</span></span>

<span data-ttu-id="5052c-259">可以在“工具” > “选项” > “环境” > “字体和颜色”中自定义字体和着色：</span><span class="sxs-lookup"><span data-stu-id="5052c-259">You can customize the font and colorization from **Tools** > **Options** > **Environment** > **Fonts and Colors**:</span></span>

![图像](intro/_static/fontoptions2.png)

## <a name="additional-resources"></a><span data-ttu-id="5052c-261">其他资源</span><span class="sxs-lookup"><span data-stu-id="5052c-261">Additional resources</span></span>

* [<span data-ttu-id="5052c-262">创作标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="5052c-262">Authoring Tag Helpers</span></span>](xref:mvc/views/tag-helpers/authoring)
* [<span data-ttu-id="5052c-263">使用窗体</span><span class="sxs-lookup"><span data-stu-id="5052c-263">Working with Forms </span></span>](xref:mvc/views/working-with-forms)
* <span data-ttu-id="5052c-264">[GitHub 上的 TagHelperSamples](https://github.com/dpaquette/TagHelperSamples) 包含用于处理 [Bootstrap](http://getbootstrap.com/) 的标记帮助程序示例。</span><span class="sxs-lookup"><span data-stu-id="5052c-264">[TagHelperSamples on GitHub](https://github.com/dpaquette/TagHelperSamples) contains Tag Helper samples for working with [Bootstrap](http://getbootstrap.com/).</span></span>
* [<span data-ttu-id="5052c-265">使用窗体</span><span class="sxs-lookup"><span data-stu-id="5052c-265">Working with Forms </span></span>](xref:mvc/views/working-with-forms)
