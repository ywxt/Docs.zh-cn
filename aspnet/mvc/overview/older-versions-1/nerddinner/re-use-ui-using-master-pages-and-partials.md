---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 重复使用 UI 使用母版页和部分 |Microsoft Docs
author: microsoft
description: 步骤 7 中我们的视图模板以消除代码重复，使用分部视图模板和母版页探讨我们可以将应用 DRY 原则的方式。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 0da32e6ac38f10df6e581517989b3b1fd2f2328c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830210"
---
<a name="re-use-ui-using-master-pages-and-partials"></a><span data-ttu-id="d656f-103">重复使用 UI 使用母版页和部分</span><span class="sxs-lookup"><span data-stu-id="d656f-103">Re-use UI Using Master Pages and Partials</span></span>
====================
<span data-ttu-id="d656f-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d656f-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="d656f-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="d656f-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="d656f-106">这是一种免费的步骤 7 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="d656f-106">This is step 7 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="d656f-107">步骤 7 中我们的视图模板以消除代码重复，使用分部视图模板和母版页探讨我们可以将应用"DRY 原则"的方式。</span><span class="sxs-lookup"><span data-stu-id="d656f-107">Step 7 looks at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication, using partial view templates and master pages.</span></span>
> 
> <span data-ttu-id="d656f-108">如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="d656f-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-7-partials-and-master-pages"></a><span data-ttu-id="d656f-109">NerdDinner 步骤 7： 分区和母版页</span><span class="sxs-lookup"><span data-stu-id="d656f-109">NerdDinner Step 7: Partials and Master Pages</span></span>

<span data-ttu-id="d656f-110">一个 ASP.NET MVC 包含内容的设计理念是"执行不自我重复"原则 （通常称为"模拟"）。</span><span class="sxs-lookup"><span data-stu-id="d656f-110">One of the design philosophies ASP.NET MVC embraces is the "Do Not Repeat Yourself" principle (commonly referred to as "DRY").</span></span> <span data-ttu-id="d656f-111">DRY 设计可帮助消除重复的代码和逻辑，最终使应用程序更快构建更容易维护。</span><span class="sxs-lookup"><span data-stu-id="d656f-111">A DRY design helps eliminate the duplication of code and logic, which ultimately makes applications faster to build and easier to maintain.</span></span>

<span data-ttu-id="d656f-112">我们已经看到 DRY 原则应用于多个我们 NerdDinner 的方案。</span><span class="sxs-lookup"><span data-stu-id="d656f-112">We've already seen the DRY principle applied in several of our NerdDinner scenarios.</span></span> <span data-ttu-id="d656f-113">几个示例： 在我们的模型层，使它能够跨这两个编辑强制执行并在控制器; 中创建方案中实现我们的验证逻辑我们重新编辑、 详细信息和删除操作方法; 在使用"NotFound"查看模板我们使用我们的视图模板，而不需要显式指定的名称，当我们调用 View() 帮助器方法; 时使用的约定的命名模式我们重新将 DinnerFormViewModel 类用于这两个编辑和创建操作方案。</span><span class="sxs-lookup"><span data-stu-id="d656f-113">A few examples: our validation logic is implemented within our model layer, which enables it to be enforced across both edit and create scenarios in our controller; we are re-using the "NotFound" view template across the Edit, Details and Delete action methods; we are using a convention- naming pattern with our view templates, which eliminates the need to explicitly specify the name when we call the View() helper method; and we are re-using the DinnerFormViewModel class for both Edit and Create action scenarios.</span></span>

<span data-ttu-id="d656f-114">让我们现在看看我们可以将应用"DRY 原则"的方式在我们的视图模板，以及消除出现代码重复。</span><span class="sxs-lookup"><span data-stu-id="d656f-114">Let's now look at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication there as well.</span></span>

### <a name="re-visiting-our-edit-and-create-view-templates"></a><span data-ttu-id="d656f-115">重新访问我们的编辑和创建视图模板</span><span class="sxs-lookup"><span data-stu-id="d656f-115">Re-visiting our Edit and Create View Templates</span></span>

<span data-ttu-id="d656f-116">目前我们正在使用两个不同的视图模板-"Edit.aspx"和"Create.aspx"– 显示我们 Dinner 窗体 UI。</span><span class="sxs-lookup"><span data-stu-id="d656f-116">Currently we are using two different view templates – "Edit.aspx" and "Create.aspx" – to display our Dinner form UI.</span></span> <span data-ttu-id="d656f-117">这些快速直观的比较突出显示相似程度。</span><span class="sxs-lookup"><span data-stu-id="d656f-117">A quick visual comparison of them highlights how similar they are.</span></span> <span data-ttu-id="d656f-118">下面是创建窗体如下所示：</span><span class="sxs-lookup"><span data-stu-id="d656f-118">Below is what the create form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

<span data-ttu-id="d656f-119">而以下是我们"的编辑"窗体如下所示：</span><span class="sxs-lookup"><span data-stu-id="d656f-119">And here is what our "Edit" form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

<span data-ttu-id="d656f-120">不大同小异的程度有吗？</span><span class="sxs-lookup"><span data-stu-id="d656f-120">Not much of a difference is there?</span></span> <span data-ttu-id="d656f-121">以外的标题和页眉文本，窗体布局和输入控件是相同的。</span><span class="sxs-lookup"><span data-stu-id="d656f-121">Other than the title and header text, the form layout and input controls are identical.</span></span>

<span data-ttu-id="d656f-122">如果我们打开"Edit.aspx"和"Create.aspx"视图模板，我们会发现它们包含相同的窗体布局和输入控件的代码。</span><span class="sxs-lookup"><span data-stu-id="d656f-122">If we open up the "Edit.aspx" and "Create.aspx" view templates we'll find that they contain identical form layout and input control code.</span></span> <span data-ttu-id="d656f-123">这种重复意味着我们最终有两次只要我们引入或更改新的 Dinner 属性-不正常时，才进行更改。</span><span class="sxs-lookup"><span data-stu-id="d656f-123">This duplication means we end up having to make changes twice anytime we introduce or change a new Dinner property - which is not good.</span></span>

### <a name="using-partial-view-templates"></a><span data-ttu-id="d656f-124">使用分部视图模板</span><span class="sxs-lookup"><span data-stu-id="d656f-124">Using Partial View Templates</span></span>

<span data-ttu-id="d656f-125">ASP.NET MVC 支持的功能来定义可用于封装视图呈现逻辑的页面的一个子部分的"分部视图"模板。</span><span class="sxs-lookup"><span data-stu-id="d656f-125">ASP.NET MVC supports the ability to define "partial view" templates that can be used to encapsulate view rendering logic for a sub-portion of a page.</span></span> <span data-ttu-id="d656f-126">"分区"一次，定义视图呈现逻辑的有用方法，然后重新使用它在多个位置跨应用程序。</span><span class="sxs-lookup"><span data-stu-id="d656f-126">"Partials" provide a useful way to define view rendering logic once, and then re-use it in multiple places across an application.</span></span>

<span data-ttu-id="d656f-127">若要帮助"DRY 向上"我们 Edit.aspx 和 Create.aspx 视图模板重复数据删除，我们可以创建一个名为"DinnerForm.ascx"，用于封装窗体布局和输入的元素共有的分部视图模板。</span><span class="sxs-lookup"><span data-stu-id="d656f-127">To help "DRY-up" our Edit.aspx and Create.aspx view template duplication, we can create a partial view template named "DinnerForm.ascx" that encapsulates the form layout and input elements common to both.</span></span> <span data-ttu-id="d656f-128">我们将为此，我们/视图/Dinners 目录上右键单击并选择"添加-&gt;视图"菜单命令：</span><span class="sxs-lookup"><span data-stu-id="d656f-128">We'll do this by right-clicking on our /Views/Dinners directory and choosing the "Add-&gt;View" menu command:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

<span data-ttu-id="d656f-129">这将显示"添加视图"对话框。</span><span class="sxs-lookup"><span data-stu-id="d656f-129">This will display the "Add View" dialog.</span></span> <span data-ttu-id="d656f-130">我们将命名为我们想要创建"DinnerForm"，选择"创建分部视图"复选框在对话框中，并指示，我们会将它传递 DinnerFormViewModel 类的新视图：</span><span class="sxs-lookup"><span data-stu-id="d656f-130">We'll name the new view we want to create "DinnerForm", select the "Create a partial view" checkbox within the dialog, and indicate that we will pass it a DinnerFormViewModel class:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

<span data-ttu-id="d656f-131">当我们单击"添加"按钮时，Visual Studio 将创建一个新"DinnerForm.ascx"视图模板为我们"\Views\Dinners"目录中。</span><span class="sxs-lookup"><span data-stu-id="d656f-131">When we click the "Add" button, Visual Studio will create a new "DinnerForm.ascx" view template for us within the "\Views\Dinners" directory.</span></span>

<span data-ttu-id="d656f-132">我们可以再复制/粘贴重复窗体布局 / 我们新的"DinnerForm.ascx"的分部视图模板中输入从我们 Edit.aspx/ Create.aspx 视图模板的控件代码：</span><span class="sxs-lookup"><span data-stu-id="d656f-132">We can then copy/paste the duplicate form layout / input control code from our Edit.aspx/ Create.aspx view templates into our new "DinnerForm.ascx" partial view template:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

<span data-ttu-id="d656f-133">然后，我们可以更新我们编辑和创建的视图模板，调用 DinnerForm 局部模板，并消除窗体重复。</span><span class="sxs-lookup"><span data-stu-id="d656f-133">We can then update our Edit and Create view templates to call the DinnerForm partial template and eliminate the form duplication.</span></span> <span data-ttu-id="d656f-134">可以为此，我们调用 Html.RenderPartial("DinnerForm") 我们视图模板中：</span><span class="sxs-lookup"><span data-stu-id="d656f-134">We can do this by calling Html.RenderPartial("DinnerForm") within our view templates:</span></span>

##### <a name="createaspx"></a><span data-ttu-id="d656f-135">Create.aspx</span><span class="sxs-lookup"><span data-stu-id="d656f-135">Create.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a><span data-ttu-id="d656f-136">Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="d656f-136">Edit.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

<span data-ttu-id="d656f-137">您可以显式限定调用 Html.RenderPartial 时所需的部分模板的路径 (例如: ~ Views/Dinners/DinnerForm.ascx")。</span><span class="sxs-lookup"><span data-stu-id="d656f-137">You can explicitly qualify the path of the partial template you want when calling Html.RenderPartial (for example: ~Views/Dinners/DinnerForm.ascx").</span></span> <span data-ttu-id="d656f-138">在上述代码中，不过，我们是利用在 ASP.NET MVC 中的基于约定的命名模式，只需指定"DinnerForm"作为分部呈现的名称。</span><span class="sxs-lookup"><span data-stu-id="d656f-138">In our code above, though, we are taking advantage of the convention-based naming pattern within ASP.NET MVC, and just specifying "DinnerForm" as the name of the partial to render.</span></span> <span data-ttu-id="d656f-139">当我们执行此操作 ASP.NET MVC 将查找基于约定的 views 目录中的第一行 （这将是/视图/Dinners DinnersController)。</span><span class="sxs-lookup"><span data-stu-id="d656f-139">When we do this ASP.NET MVC will look first in the convention-based views directory (for DinnersController this would be /Views/Dinners).</span></span> <span data-ttu-id="d656f-140">如果找不到局部模板那里它然后看它在 /Views/Shared 目录中。</span><span class="sxs-lookup"><span data-stu-id="d656f-140">If it doesn't find the partial template there it will then look for it in the /Views/Shared directory.</span></span>

<span data-ttu-id="d656f-141">只需分部视图的名称调用 Html.RenderPartial() 时，ASP.NET MVC 将传递到分部视图调用视图模板所使用的相同模型和 ViewData 字典对象。</span><span class="sxs-lookup"><span data-stu-id="d656f-141">When Html.RenderPartial() is called with just the name of the partial view, ASP.NET MVC will pass to the partial view the same Model and ViewData dictionary objects used by the calling view template.</span></span> <span data-ttu-id="d656f-142">此外，有的 Html.RenderPartial()，可以传递其他模型对象和/或要使用的分部视图的 ViewData 字典的重载的版本。</span><span class="sxs-lookup"><span data-stu-id="d656f-142">Alternatively, there are overloaded versions of Html.RenderPartial() that enable you to pass an alternate Model object and/or ViewData dictionary for the partial view to use.</span></span> <span data-ttu-id="d656f-143">这非常有用的情况下，您只希望传递完整模型视图的子集。</span><span class="sxs-lookup"><span data-stu-id="d656f-143">This is useful for scenarios where you only want to pass a subset of the full Model/ViewModel.</span></span>

| <span data-ttu-id="d656f-144">**端主题： 为什么&lt;%%&gt;而不是&lt;%= %&gt;？**</span><span class="sxs-lookup"><span data-stu-id="d656f-144">**Side Topic: Why &lt;% %&gt; instead of &lt;%= %&gt;?**</span></span> |
| --- |
| <span data-ttu-id="d656f-145">您可能已经注意到上面的代码具有细微优势之一是，我们将使用&lt;%%&gt;而不是阻止&lt;%= %&gt;阻止调用 Html.RenderPartial() 时。</span><span class="sxs-lookup"><span data-stu-id="d656f-145">One of the subtle things you might have noticed with the code above is that we are using a &lt;% %&gt; block instead of a &lt;%= %&gt; block when calling Html.RenderPartial().</span></span> <span data-ttu-id="d656f-146">&lt;%= %&gt;在 ASP.NET 中的块指示开发人员希望呈现指定的值 (例如： &lt;%="Hello"%&gt;将会呈现"Hello")。</span><span class="sxs-lookup"><span data-stu-id="d656f-146">&lt;%= %&gt; blocks in ASP.NET indicate that a developer wants to render a specified value (for example: &lt;%= "Hello" %&gt; would render "Hello").</span></span> <span data-ttu-id="d656f-147">&lt;%%&gt;块改为指示开发人员想要执行的代码，并且必须显式完成任何呈现的输出中的 (例如： &lt;%response.write("hello")%&gt;。</span><span class="sxs-lookup"><span data-stu-id="d656f-147">&lt;% %&gt; blocks instead indicate that the developer wants to execute code, and that any rendered output within them must be done explicitly (for example: &lt;% Response.Write("Hello") %&gt;.</span></span> <span data-ttu-id="d656f-148">我们将使用的原因&lt;%%&gt;上述我们 Html.RenderPartial 代码块是因为 Html.RenderPartial() 方法不会返回一个字符串，而是将输出直接向调用的视图模板内容的输出流。</span><span class="sxs-lookup"><span data-stu-id="d656f-148">The reason we are using a &lt;% %&gt; block with our Html.RenderPartial code above is because the Html.RenderPartial() method doesn't return a string, and instead outputs the content directly to the calling view template's output stream.</span></span> <span data-ttu-id="d656f-149">这样做效率由于性能原因，并且这样就无需创建一个临时的 （可能非常大） 字符串对象。</span><span class="sxs-lookup"><span data-stu-id="d656f-149">It does this for performance efficiency reasons, and by doing so it avoids the need to create a (potentially very large) temporary string object.</span></span> <span data-ttu-id="d656f-150">这可减少内存使用量并提高应用程序的整体吞吐量。</span><span class="sxs-lookup"><span data-stu-id="d656f-150">This reduces memory usage and improves overall application throughput.</span></span> <span data-ttu-id="d656f-151">一个常见的错误时使用 Html.RenderPartial() 是忘了内时调用的末尾添加分号&lt;%%&gt;块。</span><span class="sxs-lookup"><span data-stu-id="d656f-151">One common mistake when using Html.RenderPartial() is to forget to add a semi-colon at the end of the call when it is within a &lt;% %&gt; block.</span></span> <span data-ttu-id="d656f-152">例如，此代码将导致编译器错误： &lt;%html.renderpartial("dinnerform")%&gt;而是需要编写： &lt;%html.renderpartial("dinnerform"); %&gt;这是因为&lt;%%&gt;块都是自包含的代码语句，并使用 C# 代码语句需要使用分号终止时。</span><span class="sxs-lookup"><span data-stu-id="d656f-152">For example, this code will cause a compiler error: &lt;% Html.RenderPartial("DinnerForm") %&gt; You instead need to write: &lt;% Html.RenderPartial("DinnerForm"); %&gt; This is because &lt;% %&gt; blocks are self-contained code statements, and when using C# code statements need to be terminated with a semi-colon.</span></span> |

### <a name="using-partial-view-templates-to-clarify-code"></a><span data-ttu-id="d656f-153">使用分部视图模板以阐明代码</span><span class="sxs-lookup"><span data-stu-id="d656f-153">Using Partial View Templates to Clarify Code</span></span>

<span data-ttu-id="d656f-154">我们创建了"DinnerForm"的分部视图模板，以避免重复多个位置中的视图呈现逻辑。</span><span class="sxs-lookup"><span data-stu-id="d656f-154">We created the "DinnerForm" partial view template to avoid duplicating view rendering logic in multiple places.</span></span> <span data-ttu-id="d656f-155">这是创建分部视图模板的最常见原因。</span><span class="sxs-lookup"><span data-stu-id="d656f-155">This is the most common reason to create partial view templates.</span></span>

<span data-ttu-id="d656f-156">有时仍最好创建分部视图，即使它们在一个位置被调用。</span><span class="sxs-lookup"><span data-stu-id="d656f-156">Sometimes it still makes sense to create partial views even when they are only being called in a single place.</span></span> <span data-ttu-id="d656f-157">非常复杂的视图模板经常成为更易于阅读其视图呈现逻辑是提取和分区到一个或多也名为模板部分。</span><span class="sxs-lookup"><span data-stu-id="d656f-157">Very complicated view templates can often become much easier to read when their view rendering logic is extracted and partitioned into one or more well named partial templates.</span></span>

<span data-ttu-id="d656f-158">例如，考虑下面的代码段从我们的项目 （其中我们将稍后查看） 中的 Site.master 文件。</span><span class="sxs-lookup"><span data-stu-id="d656f-158">For example, consider the below code-snippet from the Site.master file in our project (which we will be looking at shortly).</span></span> <span data-ttu-id="d656f-159">代码是相对简单直接读取 – 部分原因是因为用于显示登录/注销的逻辑链接顶部屏幕的右侧封装在"LogOnUserControl"部分中：</span><span class="sxs-lookup"><span data-stu-id="d656f-159">The code is relatively straight-forward to read – partly because the logic to display a login/logout link at the top right of the screen is encapsulated within the "LogOnUserControl" partial:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

<span data-ttu-id="d656f-160">每当您发现自己会混淆尝试了解视图模板中的 html/代码标记，请考虑是否它不会就更为明显，如果它的某些提取并重构为抢眼的分部视图。</span><span class="sxs-lookup"><span data-stu-id="d656f-160">Whenever you find yourself getting confused trying to understand the html/code markup within a view-template, consider whether it wouldn't be clearer if some of it was extracted and refactored into well-named partial views.</span></span>

### <a name="master-pages"></a><span data-ttu-id="d656f-161">母版页</span><span class="sxs-lookup"><span data-stu-id="d656f-161">Master Pages</span></span>

<span data-ttu-id="d656f-162">除了支持分部视图，ASP.NET MVC 还支持创建可用于定义常见的布局和站点的顶级 html 的"母版页"模板的功能。</span><span class="sxs-lookup"><span data-stu-id="d656f-162">In addition to supporting partial views, ASP.NET MVC also supports the ability to create "master page" templates that can be used to define the common layout and top-level html of a site.</span></span> <span data-ttu-id="d656f-163">内容的占位符控件然后添加到母版页来标识可重写或"由填充的"视图可更换部件区域。</span><span class="sxs-lookup"><span data-stu-id="d656f-163">Content placeholder controls can then be added to the master page to identify replaceable regions that can be overridden or "filled in" by views.</span></span> <span data-ttu-id="d656f-164">这提供了非常有效 （DRY） 方法将一个通用布局应用跨应用程序。</span><span class="sxs-lookup"><span data-stu-id="d656f-164">This provides a very effective (and DRY) way to apply a common layout across an application.</span></span>

<span data-ttu-id="d656f-165">默认情况下，新的 ASP.NET MVC 项目具有自动添加到它们的主页面模板。</span><span class="sxs-lookup"><span data-stu-id="d656f-165">By default, new ASP.NET MVC projects have a master page template automatically added to them.</span></span> <span data-ttu-id="d656f-166">此母版页是名为"Site.master"和存在于 \Views\Shared\ 文件夹：</span><span class="sxs-lookup"><span data-stu-id="d656f-166">This master page is named "Site.master" and lives within the \Views\Shared\ folder:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

<span data-ttu-id="d656f-167">默认 Site.master 文件类似于下面。</span><span class="sxs-lookup"><span data-stu-id="d656f-167">The default Site.master file looks like below.</span></span> <span data-ttu-id="d656f-168">它定义外部站点，以及用于在顶部导航菜单的 html。</span><span class="sxs-lookup"><span data-stu-id="d656f-168">It defines the outer html of the site, along with a menu for navigation at the top.</span></span> <span data-ttu-id="d656f-169">它包含两个可替换内容占位符控件 – 一个为标题，以及另一个用于应替换为一个页面的主要内容：</span><span class="sxs-lookup"><span data-stu-id="d656f-169">It contains two replaceable content placeholder controls – one for the title, and the other for where the primary content of a page should be replaced:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

<span data-ttu-id="d656f-170">我们已经创建了 NerdDinner 应用程序 （"列出"、"详细信息"、"编辑"、"创建"、"NotFound"等） 的视图模板的所有具有已在基于此 Site.master 模板。</span><span class="sxs-lookup"><span data-stu-id="d656f-170">All of the view templates we've created for our NerdDinner application ("List", "Details", "Edit", "Create", "NotFound", etc) have been based on this Site.master template.</span></span> <span data-ttu-id="d656f-171">通过默认情况下添加到顶部的"MasterPageFile"属性会指示这一点&lt;%@ 页 %&gt;指令时我们创建了我们使用"添加视图"对话框的视图：</span><span class="sxs-lookup"><span data-stu-id="d656f-171">This is indicated via the "MasterPageFile" attribute that was added by default to the top &lt;% @ Page %&gt; directive when we created our views using the "Add View" dialog:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

<span data-ttu-id="d656f-172">这意味着，我们可以更改 Site.master 内容，并且有所做的更改自动进行应用，而且使用时我们呈现任何我们视图模板。</span><span class="sxs-lookup"><span data-stu-id="d656f-172">What this means is that we can change the Site.master content, and have the changes automatically be applied and used when we render any of our view templates.</span></span>

<span data-ttu-id="d656f-173">让我们更新我们 Site.master 标头部分，以便我们的应用程序的标头"NerdDinner"而不是"My MVC Application"。</span><span class="sxs-lookup"><span data-stu-id="d656f-173">Let's update our Site.master's header section so that the header of our application is "NerdDinner" instead of "My MVC Application".</span></span> <span data-ttu-id="d656f-174">让我们还更新我们导航菜单使第一个选项卡是"查找 Dinner"（由了 HomeController 的 index （） 操作方法处理），然后添加名为"主机 Dinner"（由 DinnersController 的 create （） 操作方法处理） 的新选项卡：</span><span class="sxs-lookup"><span data-stu-id="d656f-174">Let's also update our navigation menu so that the first tab is "Find a Dinner" (handled by the HomeController's Index() action method), and let's add a new tab called "Host a Dinner" (handled by the DinnersController's Create() action method):</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

<span data-ttu-id="d656f-175">当我们保存 Site.master 文件并刷新浏览器将介绍我们标头更改显示于我们的应用程序中的所有视图。</span><span class="sxs-lookup"><span data-stu-id="d656f-175">When we save the Site.master file and refresh our browser we'll see our header changes show up across all views within our application.</span></span> <span data-ttu-id="d656f-176">例如：</span><span class="sxs-lookup"><span data-stu-id="d656f-176">For example:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

<span data-ttu-id="d656f-177">且 */Dinners/编辑 / [id]* URL:</span><span class="sxs-lookup"><span data-stu-id="d656f-177">And with the */Dinners/Edit/[id]* URL:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a><span data-ttu-id="d656f-178">下一步</span><span class="sxs-lookup"><span data-stu-id="d656f-178">Next Step</span></span>

<span data-ttu-id="d656f-179">分区和主页面提供了非常灵活的选项，可使您能够完全组织视图。</span><span class="sxs-lookup"><span data-stu-id="d656f-179">Partials and master pages provide very flexible options that enable you to cleanly organize views.</span></span> <span data-ttu-id="d656f-180">您会发现它们可以帮助你避免重复视图内容 / 编码，并使视图模板更易于阅读和维护。</span><span class="sxs-lookup"><span data-stu-id="d656f-180">You'll find that they help you avoid duplicating view content/ code, and make your view templates easier to read and maintain.</span></span>

<span data-ttu-id="d656f-181">现在让我们重新访问我们之前生成的列表方案并启用可缩放的分页支持。</span><span class="sxs-lookup"><span data-stu-id="d656f-181">Let's now revisit the listing scenario we built earlier and enable scalable paging support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d656f-182">[上一页](use-viewdata-and-implement-viewmodel-classes.md)
> [下一页](implement-efficient-data-paging.md)</span><span class="sxs-lookup"><span data-stu-id="d656f-182">[Previous](use-viewdata-and-implement-viewmodel-classes.md)
[Next](implement-efficient-data-paging.md)</span></span>
