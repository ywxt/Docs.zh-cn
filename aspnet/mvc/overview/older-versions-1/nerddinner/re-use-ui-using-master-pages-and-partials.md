---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 重用使用母版页和它们的 UI |Microsoft 文档
author: microsoft
description: 在我们查看模板，以消除代码重复，使用分部视图模板和主控页内，第 7 步考察我们可以将干原则应用的方式。
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: ade655f3a4a429360b678d02fb564ac9cf255d42
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="re-use-ui-using-master-pages-and-partials"></a><span data-ttu-id="a1504-103">重用使用母版页和它们的 UI</span><span class="sxs-lookup"><span data-stu-id="a1504-103">Re-use UI Using Master Pages and Partials</span></span>
====================
<span data-ttu-id="a1504-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a1504-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="a1504-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="a1504-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="a1504-106">这是一个免费的步骤 7 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，查找步程取如何生成一个较小，但完成，使用 ASP.NET MVC 1 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a1504-106">This is step 7 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="a1504-107">在我们查看模板，以消除代码重复，使用分部视图模板和主控页内，第 7 步考察我们可以将"干原则"应用的方式。</span><span class="sxs-lookup"><span data-stu-id="a1504-107">Step 7 looks at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication, using partial view templates and master pages.</span></span>
> 
> <span data-ttu-id="a1504-108">如果你使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="a1504-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-7-partials-and-master-pages"></a><span data-ttu-id="a1504-109">NerdDinner 步骤 7： 它们并母版页</span><span class="sxs-lookup"><span data-stu-id="a1504-109">NerdDinner Step 7: Partials and Master Pages</span></span>

<span data-ttu-id="a1504-110">ASP.NET MVC 涵盖的设计理念之一是"执行不重复自己"原则 （通常称为"模拟"）。</span><span class="sxs-lookup"><span data-stu-id="a1504-110">One of the design philosophies ASP.NET MVC embraces is the "Do Not Repeat Yourself" principle (commonly referred to as "DRY").</span></span> <span data-ttu-id="a1504-111">干设计可帮助消除重复代码和逻辑，最终会使应用程序来生成更快且更易维护。</span><span class="sxs-lookup"><span data-stu-id="a1504-111">A DRY design helps eliminate the duplication of code and logic, which ultimately makes applications faster to build and easier to maintain.</span></span>

<span data-ttu-id="a1504-112">我们已经了解应用在了几个我们 NerdDinner 方案原则。</span><span class="sxs-lookup"><span data-stu-id="a1504-112">We've already seen the DRY principle applied in several of our NerdDinner scenarios.</span></span> <span data-ttu-id="a1504-113">几个示例： 我们验证逻辑实现在我们的模型层，这使它能够跨这两个编辑会强制执行并在我们控制器; 中创建方案我们将编辑、 详细信息和删除操作方法; 跨重新使用"NotFound"视图模板我们将通过我们的视图模板，从而无需显式指定的名称，当我们调用 View() 帮助器方法; 时使用的约定的命名模式我们重新将 DinnerFormViewModel 类用于这两个编辑和创建操作方案。</span><span class="sxs-lookup"><span data-stu-id="a1504-113">A few examples: our validation logic is implemented within our model layer, which enables it to be enforced across both edit and create scenarios in our controller; we are re-using the "NotFound" view template across the Edit, Details and Delete action methods; we are using a convention- naming pattern with our view templates, which eliminates the need to explicitly specify the name when we call the View() helper method; and we are re-using the DinnerFormViewModel class for both Edit and Create action scenarios.</span></span>

<span data-ttu-id="a1504-114">让我们现在看一下我们可以将"干原则"应用的方式在我们查看模板以及消除存在代码重复。</span><span class="sxs-lookup"><span data-stu-id="a1504-114">Let's now look at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication there as well.</span></span>

### <a name="re-visiting-our-edit-and-create-view-templates"></a><span data-ttu-id="a1504-115">重新访问我们的编辑和创建视图模板</span><span class="sxs-lookup"><span data-stu-id="a1504-115">Re-visiting our Edit and Create View Templates</span></span>

<span data-ttu-id="a1504-116">当前，我们将使用两个不同的视图模板 –"Edit.aspx"和"Create.aspx"– 来显示我们 Dinner 窗体 UI。</span><span class="sxs-lookup"><span data-stu-id="a1504-116">Currently we are using two different view templates – "Edit.aspx" and "Create.aspx" – to display our Dinner form UI.</span></span> <span data-ttu-id="a1504-117">突出显示了其中的快速 visual 比较，它们是如何类似。</span><span class="sxs-lookup"><span data-stu-id="a1504-117">A quick visual comparison of them highlights how similar they are.</span></span> <span data-ttu-id="a1504-118">下面是创建窗体如下所示：</span><span class="sxs-lookup"><span data-stu-id="a1504-118">Below is what the create form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

<span data-ttu-id="a1504-119">和下面是我们"的编辑"窗体的外观：</span><span class="sxs-lookup"><span data-stu-id="a1504-119">And here is what our "Edit" form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

<span data-ttu-id="a1504-120">有了不大部分差异？</span><span class="sxs-lookup"><span data-stu-id="a1504-120">Not much of a difference is there?</span></span> <span data-ttu-id="a1504-121">以外的标题和标头的文本，窗体布局和输入控件是相同的。</span><span class="sxs-lookup"><span data-stu-id="a1504-121">Other than the title and header text, the form layout and input controls are identical.</span></span>

<span data-ttu-id="a1504-122">如果我们打开"Edit.aspx"和"Create.aspx"查看模板我们就会发现它们包含相同的窗体的布局和输入控件的代码。</span><span class="sxs-lookup"><span data-stu-id="a1504-122">If we open up the "Edit.aspx" and "Create.aspx" view templates we'll find that they contain identical form layout and input control code.</span></span> <span data-ttu-id="a1504-123">这种重复意味着我们结束，无需进行更改的任何我们引入或更改的是一个新的 Dinner 属性-是不好的时候两次。</span><span class="sxs-lookup"><span data-stu-id="a1504-123">This duplication means we end up having to make changes twice anytime we introduce or change a new Dinner property - which is not good.</span></span>

### <a name="using-partial-view-templates"></a><span data-ttu-id="a1504-124">使用分部视图模板</span><span class="sxs-lookup"><span data-stu-id="a1504-124">Using Partial View Templates</span></span>

<span data-ttu-id="a1504-125">ASP.NET MVC 支持能够定义可以用于封装视图呈现逻辑的页面的一个子部分的"分部视图"模板。</span><span class="sxs-lookup"><span data-stu-id="a1504-125">ASP.NET MVC supports the ability to define "partial view" templates that can be used to encapsulate view rendering logic for a sub-portion of a page.</span></span> <span data-ttu-id="a1504-126">"它们"提供有用的方式来一次，定义视图呈现逻辑，然后重新使用它在多个位置跨应用程序。</span><span class="sxs-lookup"><span data-stu-id="a1504-126">"Partials" provide a useful way to define view rendering logic once, and then re-use it in multiple places across an application.</span></span>

<span data-ttu-id="a1504-127">为了帮助"干型"我们 Edit.aspx 和 Create.aspx 视图模板重复，我们可以创建一个名为"DinnerForm.ascx"，用于封装窗体布局和公用的输入的元素的分部视图模板。</span><span class="sxs-lookup"><span data-stu-id="a1504-127">To help "DRY-up" our Edit.aspx and Create.aspx view template duplication, we can create a partial view template named "DinnerForm.ascx" that encapsulates the form layout and input elements common to both.</span></span> <span data-ttu-id="a1504-128">我们需要执行此操作我们/视图/晚餐目录上右键单击并选择"添加-&gt;视图"菜单命令：</span><span class="sxs-lookup"><span data-stu-id="a1504-128">We'll do this by right-clicking on our /Views/Dinners directory and choosing the "Add-&gt;View" menu command:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

<span data-ttu-id="a1504-129">这将显示"添加视图"对话框。</span><span class="sxs-lookup"><span data-stu-id="a1504-129">This will display the "Add View" dialog.</span></span> <span data-ttu-id="a1504-130">我们将新视图命名为我们想要创建"DinnerForm"，选中"创建了分部视图"复选框在对话框中，并指示，我们会将它传递 DinnerFormViewModel 类：</span><span class="sxs-lookup"><span data-stu-id="a1504-130">We'll name the new view we want to create "DinnerForm", select the "Create a partial view" checkbox within the dialog, and indicate that we will pass it a DinnerFormViewModel class:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

<span data-ttu-id="a1504-131">当我们单击"添加"按钮时，Visual Studio 将创建新"DinnerForm.ascx"视图模板为我们"\Views\Dinners"目录中。</span><span class="sxs-lookup"><span data-stu-id="a1504-131">When we click the "Add" button, Visual Studio will create a new "DinnerForm.ascx" view template for us within the "\Views\Dinners" directory.</span></span>

<span data-ttu-id="a1504-132">我们可以然后复制/粘贴重复窗体布局 / 我们新的"DinnerForm.ascx"分部视图模板中输入从我们 Edit.aspx/ Create.aspx 查看模板的控件代码：</span><span class="sxs-lookup"><span data-stu-id="a1504-132">We can then copy/paste the duplicate form layout / input control code from our Edit.aspx/ Create.aspx view templates into our new "DinnerForm.ascx" partial view template:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

<span data-ttu-id="a1504-133">然后，我们可以更新我们编辑和创建视图模板，以调用 DinnerForm 部分模板并消除窗体重复。</span><span class="sxs-lookup"><span data-stu-id="a1504-133">We can then update our Edit and Create view templates to call the DinnerForm partial template and eliminate the form duplication.</span></span> <span data-ttu-id="a1504-134">我们可以通过调用 Html.RenderPartial("DinnerForm") 实现此我们视图模板中：</span><span class="sxs-lookup"><span data-stu-id="a1504-134">We can do this by calling Html.RenderPartial("DinnerForm") within our view templates:</span></span>

##### <a name="createaspx"></a><span data-ttu-id="a1504-135">Create.aspx</span><span class="sxs-lookup"><span data-stu-id="a1504-135">Create.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a><span data-ttu-id="a1504-136">Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="a1504-136">Edit.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

<span data-ttu-id="a1504-137">你可以显式限定调用 Html.RenderPartial 时所需的部分模板的路径 (例如: ~ Views/Dinners/DinnerForm.ascx")。</span><span class="sxs-lookup"><span data-stu-id="a1504-137">You can explicitly qualify the path of the partial template you want when calling Html.RenderPartial (for example: ~Views/Dinners/DinnerForm.ascx").</span></span> <span data-ttu-id="a1504-138">在上面代码中，不过，我们将利用基于约定的命名模式在 ASP.NET MVC 并只需指定"DinnerForm"作为分部呈现的名称。</span><span class="sxs-lookup"><span data-stu-id="a1504-138">In our code above, though, we are taking advantage of the convention-based naming pattern within ASP.NET MVC, and just specifying "DinnerForm" as the name of the partial to render.</span></span> <span data-ttu-id="a1504-139">我们执行此操作 ASP.NET MVC 将查找基于约定的 views 目录中的第一行 （这将是/视图/晚餐 DinnersController)。</span><span class="sxs-lookup"><span data-stu-id="a1504-139">When we do this ASP.NET MVC will look first in the convention-based views directory (for DinnersController this would be /Views/Dinners).</span></span> <span data-ttu-id="a1504-140">如果找不到的部分的模板存在它随后将查找为其在 /Views/Shared 目录中。</span><span class="sxs-lookup"><span data-stu-id="a1504-140">If it doesn't find the partial template there it will then look for it in the /Views/Shared directory.</span></span>

<span data-ttu-id="a1504-141">当只分部视图的名称与调用 Html.RenderPartial() 时，ASP.NET MVC 将传递给分部视图相同的模型和 ViewData 字典的对象由调用的视图模板。</span><span class="sxs-lookup"><span data-stu-id="a1504-141">When Html.RenderPartial() is called with just the name of the partial view, ASP.NET MVC will pass to the partial view the same Model and ViewData dictionary objects used by the calling view template.</span></span> <span data-ttu-id="a1504-142">或者，有的 Html.RenderPartial() 重载使您能够通过将其他模型对象和/或要使用的分部视图的 ViewData 字典的版本。</span><span class="sxs-lookup"><span data-stu-id="a1504-142">Alternatively, there are overloaded versions of Html.RenderPartial() that enable you to pass an alternate Model object and/or ViewData dictionary for the partial view to use.</span></span> <span data-ttu-id="a1504-143">这非常有用的情况下，你仅希望传递完整模型/视图模型的子集。</span><span class="sxs-lookup"><span data-stu-id="a1504-143">This is useful for scenarios where you only want to pass a subset of the full Model/ViewModel.</span></span>

| <span data-ttu-id="a1504-144">**端主题内容： 为什么&lt;%%&gt;而不是&lt;%= %&gt;？**</span><span class="sxs-lookup"><span data-stu-id="a1504-144">**Side Topic: Why &lt;% %&gt; instead of &lt;%= %&gt;?**</span></span> |
| --- |
| <span data-ttu-id="a1504-145">你可能已经注意到使用上面的代码的细微项目之一是，我们将使用&lt;%%&gt;阻止而不是&lt;%= %&gt;阻止调用 Html.RenderPartial() 时。</span><span class="sxs-lookup"><span data-stu-id="a1504-145">One of the subtle things you might have noticed with the code above is that we are using a &lt;% %&gt; block instead of a &lt;%= %&gt; block when calling Html.RenderPartial().</span></span> <span data-ttu-id="a1504-146">&lt;%= %&gt; ASP.NET 中的块指示开发人员想要呈现指定的值 (例如： &lt;%="Hello"%&gt;将会呈现"Hello")。</span><span class="sxs-lookup"><span data-stu-id="a1504-146">&lt;%= %&gt; blocks in ASP.NET indicate that a developer wants to render a specified value (for example: &lt;%= "Hello" %&gt; would render "Hello").</span></span> <span data-ttu-id="a1504-147">&lt;%%&gt;块而是指示开发人员想要执行的代码，并且必须显式完成任何呈现其中的输出 (例如： &lt;%response.write("hello")%&gt;。</span><span class="sxs-lookup"><span data-stu-id="a1504-147">&lt;% %&gt; blocks instead indicate that the developer wants to execute code, and that any rendered output within them must be done explicitly (for example: &lt;% Response.Write("Hello") %&gt;.</span></span> <span data-ttu-id="a1504-148">我们将使用的原因&lt;%%&gt;代码块替换上述我们 Html.RenderPartial 代码是因为 Html.RenderPartial() 方法不返回一个字符串，并改为输出调用的视图模板直接将内容的输出流。</span><span class="sxs-lookup"><span data-stu-id="a1504-148">The reason we are using a &lt;% %&gt; block with our Html.RenderPartial code above is because the Html.RenderPartial() method doesn't return a string, and instead outputs the content directly to the calling view template's output stream.</span></span> <span data-ttu-id="a1504-149">这是为了效率提高性能，并通过执行操作，因此它可以避免需要创建一个 （可能非常大） 的临时字符串对象。</span><span class="sxs-lookup"><span data-stu-id="a1504-149">It does this for performance efficiency reasons, and by doing so it avoids the need to create a (potentially very large) temporary string object.</span></span> <span data-ttu-id="a1504-150">这可减少内存使用量并提高应用程序的总体吞吐量。</span><span class="sxs-lookup"><span data-stu-id="a1504-150">This reduces memory usage and improves overall application throughput.</span></span> <span data-ttu-id="a1504-151">在使用 Html.RenderPartial() 即将忘记中时调用的末尾添加分号时的一种常见错误&lt;%%&gt;块。</span><span class="sxs-lookup"><span data-stu-id="a1504-151">One common mistake when using Html.RenderPartial() is to forget to add a semi-colon at the end of the call when it is within a &lt;% %&gt; block.</span></span> <span data-ttu-id="a1504-152">例如，此代码将导致编译器错误： &lt;%html.renderpartial("dinnerform")%&gt;需要改为编写： &lt;%html.renderpartial("dinnerform"); %&gt;这是因为&lt;%%&gt;块都是自包含的代码语句，并使用 C# 代码语句需要使用分号终止时。</span><span class="sxs-lookup"><span data-stu-id="a1504-152">For example, this code will cause a compiler error: &lt;% Html.RenderPartial("DinnerForm") %&gt; You instead need to write: &lt;% Html.RenderPartial("DinnerForm"); %&gt; This is because &lt;% %&gt; blocks are self-contained code statements, and when using C# code statements need to be terminated with a semi-colon.</span></span> |

### <a name="using-partial-view-templates-to-clarify-code"></a><span data-ttu-id="a1504-153">使用分部视图模板以阐明代码</span><span class="sxs-lookup"><span data-stu-id="a1504-153">Using Partial View Templates to Clarify Code</span></span>

<span data-ttu-id="a1504-154">我们创建了"DinnerForm"分部视图模板，以避免重复多个位置中的视图呈现逻辑。</span><span class="sxs-lookup"><span data-stu-id="a1504-154">We created the "DinnerForm" partial view template to avoid duplicating view rendering logic in multiple places.</span></span> <span data-ttu-id="a1504-155">这是创建分部视图模板的最常见原因。</span><span class="sxs-lookup"><span data-stu-id="a1504-155">This is the most common reason to create partial view templates.</span></span>

<span data-ttu-id="a1504-156">有时，仍有必要创建分部视图，即使它们正在单个位置被调用。</span><span class="sxs-lookup"><span data-stu-id="a1504-156">Sometimes it still makes sense to create partial views even when they are only being called in a single place.</span></span> <span data-ttu-id="a1504-157">非常复杂的视图模板通常可能变得更易读在提取、 分区到一个或多也名为模板的部分其视图呈现逻辑。</span><span class="sxs-lookup"><span data-stu-id="a1504-157">Very complicated view templates can often become much easier to read when their view rendering logic is extracted and partitioned into one or more well named partial templates.</span></span>

<span data-ttu-id="a1504-158">例如，考虑下面我们项目 （该我们将很快考察） 中的 Site.master 文件中的代码段。</span><span class="sxs-lookup"><span data-stu-id="a1504-158">For example, consider the below code-snippet from the Site.master file in our project (which we will be looking at shortly).</span></span> <span data-ttu-id="a1504-159">代码是比较直接的操作读取 – 部分原因逻辑来显示登录/注销链接顶部屏幕的右侧封装在"LogOnUserControl"部分：</span><span class="sxs-lookup"><span data-stu-id="a1504-159">The code is relatively straight-forward to read – partly because the logic to display a login/logout link at the top right of the screen is encapsulated within the "LogOnUserControl" partial:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

<span data-ttu-id="a1504-160">每当你发现自己感到迷惑尝试了解视图模板中的 html/代码标记，请考虑是否它不是清楚地了解如果部分内容成功提取并重构为正确命名分部视图。</span><span class="sxs-lookup"><span data-stu-id="a1504-160">Whenever you find yourself getting confused trying to understand the html/code markup within a view-template, consider whether it wouldn't be clearer if some of it was extracted and refactored into well-named partial views.</span></span>

### <a name="master-pages"></a><span data-ttu-id="a1504-161">母版页</span><span class="sxs-lookup"><span data-stu-id="a1504-161">Master Pages</span></span>

<span data-ttu-id="a1504-162">除了支持分部视图，ASP.NET MVC 还支持能够创建用于定义常用布局和顶级 html 的站点的"母版页"模板。</span><span class="sxs-lookup"><span data-stu-id="a1504-162">In addition to supporting partial views, ASP.NET MVC also supports the ability to create "master page" templates that can be used to define the common layout and top-level html of a site.</span></span> <span data-ttu-id="a1504-163">内容的占位符控件然后，可以添加到主页后，可以确定可替换区域可以重写或"已填写"视图。</span><span class="sxs-lookup"><span data-stu-id="a1504-163">Content placeholder controls can then be added to the master page to identify replaceable regions that can be overridden or "filled in" by views.</span></span> <span data-ttu-id="a1504-164">这提供了将通用布局应用跨应用程序的非常有效 （和干） 方法。</span><span class="sxs-lookup"><span data-stu-id="a1504-164">This provides a very effective (and DRY) way to apply a common layout across an application.</span></span>

<span data-ttu-id="a1504-165">默认情况下，新的 ASP.NET MVC 项目具有母版页模板自动添加到它们。</span><span class="sxs-lookup"><span data-stu-id="a1504-165">By default, new ASP.NET MVC projects have a master page template automatically added to them.</span></span> <span data-ttu-id="a1504-166">此母版页是名为"Site.master"和生活 \Views\Shared\ 文件夹中：</span><span class="sxs-lookup"><span data-stu-id="a1504-166">This master page is named "Site.master" and lives within the \Views\Shared\ folder:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

<span data-ttu-id="a1504-167">默认 Site.master 文件类似于下面。</span><span class="sxs-lookup"><span data-stu-id="a1504-167">The default Site.master file looks like below.</span></span> <span data-ttu-id="a1504-168">它定义的站点，以及在顶部导航菜单的外部 html。</span><span class="sxs-lookup"><span data-stu-id="a1504-168">It defines the outer html of the site, along with a menu for navigation at the top.</span></span> <span data-ttu-id="a1504-169">它包含两个可替换内容占位符控件 – 一个用于标题、，另一个用于应替换为主要内容的页面：</span><span class="sxs-lookup"><span data-stu-id="a1504-169">It contains two replaceable content placeholder controls – one for the title, and the other for where the primary content of a page should be replaced:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

<span data-ttu-id="a1504-170">我们已为我们 NerdDinner 的应用程序 （"列表"、"详细信息"、"编辑"、"创建"、"NotFound"等） 创建的视图模板的所有具有已在基于此 Site.master 模板。</span><span class="sxs-lookup"><span data-stu-id="a1504-170">All of the view templates we've created for our NerdDinner application ("List", "Details", "Edit", "Create", "NotFound", etc) have been based on this Site.master template.</span></span> <span data-ttu-id="a1504-171">这通过已按默认添加到顶部的"MasterPageFile"属性指示&lt;%@ 页 %&gt;指令我们创建我们视图使用"添加视图"对话框时：</span><span class="sxs-lookup"><span data-stu-id="a1504-171">This is indicated via the "MasterPageFile" attribute that was added by default to the top &lt;% @ Page %&gt; directive when we created our views using the "Add View" dialog:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

<span data-ttu-id="a1504-172">这意味着，我们可以更改 Site.master 内容，并且具有所做的更改自动被应用，并且使用当我们呈现任何我们查看模板。</span><span class="sxs-lookup"><span data-stu-id="a1504-172">What this means is that we can change the Site.master content, and have the changes automatically be applied and used when we render any of our view templates.</span></span>

<span data-ttu-id="a1504-173">让我们更新我们 Site.master 标头部分，以便我们的应用程序的标头"NerdDinner"而不是"My MVC Application"。</span><span class="sxs-lookup"><span data-stu-id="a1504-173">Let's update our Site.master's header section so that the header of our application is "NerdDinner" instead of "My MVC Application".</span></span> <span data-ttu-id="a1504-174">让我们还更新我们导航菜单使第一个选项卡为"查找 Dinner"（由 HomeController 的 index （） 操作方法），并让我们添加名为"主机 Dinner"（由 DinnersController 的 create （） 操作方法） 的新选项卡：</span><span class="sxs-lookup"><span data-stu-id="a1504-174">Let's also update our navigation menu so that the first tab is "Find a Dinner" (handled by the HomeController's Index() action method), and let's add a new tab called "Host a Dinner" (handled by the DinnersController's Create() action method):</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

<span data-ttu-id="a1504-175">当我们保存 Site.master 文件并刷新我们浏览器，我们将看到我们标头更改显示在我们的应用程序中的所有视图。</span><span class="sxs-lookup"><span data-stu-id="a1504-175">When we save the Site.master file and refresh our browser we'll see our header changes show up across all views within our application.</span></span> <span data-ttu-id="a1504-176">例如：</span><span class="sxs-lookup"><span data-stu-id="a1504-176">For example:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

<span data-ttu-id="a1504-177">与*/Dinners/编辑 / [id]* URL:</span><span class="sxs-lookup"><span data-stu-id="a1504-177">And with the */Dinners/Edit/[id]* URL:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a><span data-ttu-id="a1504-178">下一步</span><span class="sxs-lookup"><span data-stu-id="a1504-178">Next Step</span></span>

<span data-ttu-id="a1504-179">它们和主控页提供了非常灵活的选项，您可以完全组织视图。</span><span class="sxs-lookup"><span data-stu-id="a1504-179">Partials and master pages provide very flexible options that enable you to cleanly organize views.</span></span> <span data-ttu-id="a1504-180">你将找到它们可以帮助你避免重复视图内容 / 编码，并使你的视图模板更易于读取和维护。</span><span class="sxs-lookup"><span data-stu-id="a1504-180">You'll find that they help you avoid duplicating view content/ code, and make your view templates easier to read and maintain.</span></span>

<span data-ttu-id="a1504-181">让我们现在重新考虑我们之前生成的列表方案，并启用可缩放的分页支持。</span><span class="sxs-lookup"><span data-stu-id="a1504-181">Let's now revisit the listing scenario we built earlier and enable scalable paging support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a1504-182">[上一页](use-viewdata-and-implement-viewmodel-classes.md)
> [下一页](implement-efficient-data-paging.md)</span><span class="sxs-lookup"><span data-stu-id="a1504-182">[Previous](use-viewdata-and-implement-viewmodel-classes.md)
[Next](implement-efficient-data-paging.md)</span></span>
