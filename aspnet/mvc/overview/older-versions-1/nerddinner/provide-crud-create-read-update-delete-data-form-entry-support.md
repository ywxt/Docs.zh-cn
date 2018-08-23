---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 提供 CRUD （创建、 读取、 更新、 删除） 数据窗体输入支持 |Microsoft Docs
author: microsoft
description: 步骤 5 显示了如何通过启用支持编辑、 创建和使用它删除 Dinners 也使我们的 DinnersController 类进一步。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 45d74249a34fc7e37e9776a398615d2f613a7582
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824239"
---
<a name="provide-crud-create-read-update-delete-data-form-entry-support"></a><span data-ttu-id="5e392-103">提供 CRUD （创建、 读取、 更新、 删除） 数据窗体输入支持</span><span class="sxs-lookup"><span data-stu-id="5e392-103">Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support</span></span>
====================
<span data-ttu-id="5e392-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5e392-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="5e392-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="5e392-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="5e392-106">这是一种免费的步骤 5 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5e392-106">This is step 5 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="5e392-107">步骤 5 显示了如何通过启用支持编辑、 创建和使用它删除 Dinners 也使我们的 DinnersController 类进一步。</span><span class="sxs-lookup"><span data-stu-id="5e392-107">Step 5 shows how to take our DinnersController class further by enable support for editing, creating and deleting Dinners with it as well.</span></span>
> 
> <span data-ttu-id="5e392-108">如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="5e392-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a><span data-ttu-id="5e392-109">NerdDinner 步骤 5： 创建、 更新、 删除窗体方案</span><span class="sxs-lookup"><span data-stu-id="5e392-109">NerdDinner Step 5: Create, Update, Delete Form Scenarios</span></span>

<span data-ttu-id="5e392-110">我们引入了控制器和视图，并介绍如何使用它们来在站点上实现 Dinners 的列表/详细信息体验。</span><span class="sxs-lookup"><span data-stu-id="5e392-110">We've introduced controllers and views, and covered how to use them to implement a listing/details experience for Dinners on site.</span></span> <span data-ttu-id="5e392-111">下一步将采取进一步的我们的 DinnersController 类，并启用对编辑、 创建和使用它还删除 Dinners 的支持。</span><span class="sxs-lookup"><span data-stu-id="5e392-111">Our next step will be to take our DinnersController class further and enable support for editing, creating and deleting Dinners with it as well.</span></span>

### <a name="urls-handled-by-dinnerscontroller"></a><span data-ttu-id="5e392-112">由 DinnersController 的 Url</span><span class="sxs-lookup"><span data-stu-id="5e392-112">URLs handled by DinnersController</span></span>

<span data-ttu-id="5e392-113">我们之前添加操作方法向 DinnersController 实现对两个 Url 的支持： */Dinners*并 */Dinners/详细信息 / [id]*。</span><span class="sxs-lookup"><span data-stu-id="5e392-113">We previously added action methods to DinnersController that implemented support for two URLs: */Dinners* and */Dinners/Details/[id]*.</span></span>

| <span data-ttu-id="5e392-114">**URL**</span><span class="sxs-lookup"><span data-stu-id="5e392-114">**URL**</span></span> | <span data-ttu-id="5e392-115">**VERB**</span><span class="sxs-lookup"><span data-stu-id="5e392-115">**VERB**</span></span> | <span data-ttu-id="5e392-116">**目的**</span><span class="sxs-lookup"><span data-stu-id="5e392-116">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5e392-117">*/Dinners/*</span><span class="sxs-lookup"><span data-stu-id="5e392-117">*/Dinners/*</span></span> | <span data-ttu-id="5e392-118">GET</span><span class="sxs-lookup"><span data-stu-id="5e392-118">GET</span></span> | <span data-ttu-id="5e392-119">显示即将到来的 dinners 的 HTML 列表。</span><span class="sxs-lookup"><span data-stu-id="5e392-119">Display an HTML list of upcoming dinners.</span></span> |
| <span data-ttu-id="5e392-120">*/Dinners/Details/[id]*</span><span class="sxs-lookup"><span data-stu-id="5e392-120">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="5e392-121">GET</span><span class="sxs-lookup"><span data-stu-id="5e392-121">GET</span></span> | <span data-ttu-id="5e392-122">显示有关特定 dinner 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="5e392-122">Display details about a specific dinner.</span></span> |

<span data-ttu-id="5e392-123">我们现在将操作方法来实现三个其他 Url: <em>/Dinners/编辑 / [id]、 / Dinners/创建、</em>并<em>/Dinners/Delete / [id]</em>。</span><span class="sxs-lookup"><span data-stu-id="5e392-123">We will now add action methods to implement three additional URLs: <em>/Dinners/Edit/[id], /Dinners/Create,</em>and<em>/Dinners/Delete/[id]</em>.</span></span> <span data-ttu-id="5e392-124">这些 Url 将启用对编辑现有 Dinners，创建新 Dinners 和删除 Dinners 的支持。</span><span class="sxs-lookup"><span data-stu-id="5e392-124">These URLs will enable support for editing existing Dinners, creating new Dinners, and deleting Dinners.</span></span>

<span data-ttu-id="5e392-125">我们将支持与这些新的 Url 的 HTTP GET 和 HTTP POST 谓词交互。</span><span class="sxs-lookup"><span data-stu-id="5e392-125">We will support both HTTP GET and HTTP POST verb interactions with these new URLs.</span></span> <span data-ttu-id="5e392-126">HTTP GET 请求到以下 Url 将显示数据 （使用在"编辑"的情况下的 Dinner 数据填充窗体，在"创建"的情况下的空白窗体和在"删除"的情况下删除确认屏幕） 的初始 HTML 视图。</span><span class="sxs-lookup"><span data-stu-id="5e392-126">HTTP GET requests to these URLs will display the initial HTML view of the data (a form populated with the Dinner data in the case of "edit", a blank form in the case of "create", and a delete confirmation screen in the case of "delete").</span></span> <span data-ttu-id="5e392-127">这些 url 的 HTTP POST 请求将保存/更新/删除 Dinner 数据中我们 DinnerRepository （和从数据库到）。</span><span class="sxs-lookup"><span data-stu-id="5e392-127">HTTP POST requests to these URLs will save/update/delete the Dinner data in our DinnerRepository (and from there to the database).</span></span>

| <span data-ttu-id="5e392-128">**URL**</span><span class="sxs-lookup"><span data-stu-id="5e392-128">**URL**</span></span> | <span data-ttu-id="5e392-129">**VERB**</span><span class="sxs-lookup"><span data-stu-id="5e392-129">**VERB**</span></span> | <span data-ttu-id="5e392-130">**目的**</span><span class="sxs-lookup"><span data-stu-id="5e392-130">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5e392-131">*/Dinners/Edit/[id]*</span><span class="sxs-lookup"><span data-stu-id="5e392-131">*/Dinners/Edit/[id]*</span></span> | <span data-ttu-id="5e392-132">GET</span><span class="sxs-lookup"><span data-stu-id="5e392-132">GET</span></span> | <span data-ttu-id="5e392-133">显示可编辑 HTML 窗体使用 Dinner 数据填充。</span><span class="sxs-lookup"><span data-stu-id="5e392-133">Display an editable HTML form populated with Dinner data.</span></span> |
| <span data-ttu-id="5e392-134">发布</span><span class="sxs-lookup"><span data-stu-id="5e392-134">POST</span></span> | <span data-ttu-id="5e392-135">保存到数据库的晚餐窗体更改。</span><span class="sxs-lookup"><span data-stu-id="5e392-135">Save the form changes for a particular Dinner to the database.</span></span> |
| <span data-ttu-id="5e392-136">*/Dinners/Create*</span><span class="sxs-lookup"><span data-stu-id="5e392-136">*/Dinners/Create*</span></span> | <span data-ttu-id="5e392-137">GET</span><span class="sxs-lookup"><span data-stu-id="5e392-137">GET</span></span> | <span data-ttu-id="5e392-138">显示一个空的 HTML 窗体，用户可定义新 Dinners。</span><span class="sxs-lookup"><span data-stu-id="5e392-138">Display an empty HTML form that allows users to define new Dinners.</span></span> |
| <span data-ttu-id="5e392-139">发布</span><span class="sxs-lookup"><span data-stu-id="5e392-139">POST</span></span> | <span data-ttu-id="5e392-140">创建新的 Dinner 并将其保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="5e392-140">Create a new Dinner and save it in the database.</span></span> |
| <span data-ttu-id="5e392-141">*/Dinners/Delete/[id]*</span><span class="sxs-lookup"><span data-stu-id="5e392-141">*/Dinners/Delete/[id]*</span></span> | <span data-ttu-id="5e392-142">GET</span><span class="sxs-lookup"><span data-stu-id="5e392-142">GET</span></span> | <span data-ttu-id="5e392-143">显示删除确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="5e392-143">Display delete confirmation screen.</span></span> |
| <span data-ttu-id="5e392-144">发布</span><span class="sxs-lookup"><span data-stu-id="5e392-144">POST</span></span> | <span data-ttu-id="5e392-145">从数据库中删除指定的 dinner。</span><span class="sxs-lookup"><span data-stu-id="5e392-145">Deletes the specified dinner from the database.</span></span> |

### <a name="edit-support"></a><span data-ttu-id="5e392-146">编辑支持</span><span class="sxs-lookup"><span data-stu-id="5e392-146">Edit Support</span></span>

<span data-ttu-id="5e392-147">让我们首先将实现"编辑"方案。</span><span class="sxs-lookup"><span data-stu-id="5e392-147">Let's begin by implementing the "edit" scenario.</span></span>

#### <a name="the-http-get-edit-action-method"></a><span data-ttu-id="5e392-148">HTTP GET 编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="5e392-148">The HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="5e392-149">我们将首先实现我们的编辑操作方法的 HTTP"GET"行为。</span><span class="sxs-lookup"><span data-stu-id="5e392-149">We'll start by implementing the HTTP "GET" behavior of our edit action method.</span></span> <span data-ttu-id="5e392-150">此方法将调用何时 */Dinners/编辑 / [id]* 请求 URL。</span><span class="sxs-lookup"><span data-stu-id="5e392-150">This method will be invoked when the */Dinners/Edit/[id]* URL is requested.</span></span> <span data-ttu-id="5e392-151">我们的实现将如下所示：</span><span class="sxs-lookup"><span data-stu-id="5e392-151">Our implementation will look like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

<span data-ttu-id="5e392-152">上面的代码使用 DinnerRepository 检索 Dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="5e392-152">The code above uses the DinnerRepository to retrieve a Dinner object.</span></span> <span data-ttu-id="5e392-153">然后，它将呈现视图模板使用 Dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="5e392-153">It then renders a View template using the Dinner object.</span></span> <span data-ttu-id="5e392-154">因为我们尚未显式传递到的模板名称*View()* 帮助器方法，它将使用的约定，其默认路径来解析视图模板： /Views/Dinners/Edit.aspx。</span><span class="sxs-lookup"><span data-stu-id="5e392-154">Because we haven't explicitly passed a template name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Edit.aspx.</span></span>

<span data-ttu-id="5e392-155">让我们现在创建此视图模板。</span><span class="sxs-lookup"><span data-stu-id="5e392-155">Let's now create this view template.</span></span> <span data-ttu-id="5e392-156">我们将编辑方法内右键单击并选择"添加视图"上下文菜单命令来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="5e392-156">We will do this by right-clicking within the Edit method and selecting the "Add View" context menu command:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

<span data-ttu-id="5e392-157">在"添加视图"对话框中，我们将指示我们 Dinner 对象传递给视图模板作为它的模型，并选择"编辑"的模板自动基架：</span><span class="sxs-lookup"><span data-stu-id="5e392-157">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to auto-scaffold an "Edit" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

<span data-ttu-id="5e392-158">当我们单击"添加"按钮时，Visual Studio 将"\Views\Dinners"目录中为我们添加新的"Edit.aspx"视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="5e392-158">When we click the "Add" button, Visual Studio will add a new "Edit.aspx" view template file for us within the "\Views\Dinners" directory.</span></span> <span data-ttu-id="5e392-159">它还会打开新的"Edit.aspx"视图模板代码的编辑器 – 填充初始"的编辑"基架实现如下下面内：</span><span class="sxs-lookup"><span data-stu-id="5e392-159">It will also open up the new "Edit.aspx" view template within the code-editor – populated with an initial "Edit" scaffold implementation like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

<span data-ttu-id="5e392-160">让我们进行一些更改到默认"的编辑"基架生成，并更新具有以下内容 （从而删除几个我们不想要公开的属性） 的编辑视图模板：</span><span class="sxs-lookup"><span data-stu-id="5e392-160">Let's make a few changes to the default "edit" scaffold generated, and update the edit view template to have the content below (which removes a few of the properties we don't want to expose):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

<span data-ttu-id="5e392-161">当我们运行的应用程序和请求 *"/ Dinners/编辑/1"* 我们将看到以下页面的 URL:</span><span class="sxs-lookup"><span data-stu-id="5e392-161">When we run the application and request the *"/Dinners/Edit/1"* URL we will see the following page:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

<span data-ttu-id="5e392-162">视图生成的 HTML 标记类似于下面。</span><span class="sxs-lookup"><span data-stu-id="5e392-162">The HTML markup generated by our view looks like below.</span></span> <span data-ttu-id="5e392-163">这一点与标准 HTML –&lt;窗体&gt;执行 HTTP POST 到的元素 */Dinners/Edit/1* URL 时"保存" &lt;type ="提交"/&gt;按钮。</span><span class="sxs-lookup"><span data-stu-id="5e392-163">It is standard HTML – with a &lt;form&gt; element that performs an HTTP POST to the */Dinners/Edit/1* URL when the "Save" &lt;input type="submit"/&gt; button is pushed.</span></span> <span data-ttu-id="5e392-164">在 HTML &lt;type ="text"/&gt;元素已为每个可编辑的属性的输出：</span><span class="sxs-lookup"><span data-stu-id="5e392-164">A HTML &lt;input type="text"/&gt; element has been output for each editable property:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a><span data-ttu-id="5e392-165">Html.BeginForm() 和 Html.TextBox() 的 Html 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="5e392-165">Html.BeginForm() and Html.TextBox() Html Helper Methods</span></span>

<span data-ttu-id="5e392-166">我们"Edit.aspx"视图模板正在使用的多个"的 Html 帮助器"方法： Html.ValidationSummary()、 Html.BeginForm()、 Html.TextBox() 和 Html.ValidationMessage()。</span><span class="sxs-lookup"><span data-stu-id="5e392-166">Our "Edit.aspx" view template is using several "Html Helper" methods: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), and Html.ValidationMessage().</span></span> <span data-ttu-id="5e392-167">除了为我们生成的 HTML 标记，这些帮助器方法提供了内置的错误处理和验证支持。</span><span class="sxs-lookup"><span data-stu-id="5e392-167">In addition to generating HTML markup for us, these helper methods provide built-in error handling and validation support.</span></span>

##### <a name="htmlbeginform-helper-method"></a><span data-ttu-id="5e392-168">Html.BeginForm() 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="5e392-168">Html.BeginForm() helper method</span></span>

<span data-ttu-id="5e392-169">Html.BeginForm() 帮助程序方法是 HTML 输出内容是什么&lt;窗体&gt;我们标记中的元素。</span><span class="sxs-lookup"><span data-stu-id="5e392-169">The Html.BeginForm() helper method is what output the HTML &lt;form&gt; element in our markup.</span></span> <span data-ttu-id="5e392-170">我们 Edit.aspx 视图模板中您会注意到，我们要将应用的 C#"using"语句时使用此方法。</span><span class="sxs-lookup"><span data-stu-id="5e392-170">In our Edit.aspx view template you'll notice that we are applying a C# "using" statement when using this method.</span></span> <span data-ttu-id="5e392-171">左大括号指示的开头&lt;窗体&gt;内容和右大括号是所指示的结束&lt;/&gt;元素：</span><span class="sxs-lookup"><span data-stu-id="5e392-171">The open curly brace indicates the beginning of the &lt;form&gt; content, and the closing curly brace is what indicates the end of the &lt;/form&gt; element:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

<span data-ttu-id="5e392-172">或者，如果你发现"using"语句方法不自然的此类方案，您可以使用 Html.BeginForm() 和 Html.EndForm() 的组合 （这会执行相同的操作）：</span><span class="sxs-lookup"><span data-stu-id="5e392-172">Alternatively, if you find the "using" statement approach unnatural for a scenario like this, you can use a Html.BeginForm() and Html.EndForm() combination (which does the same thing):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

<span data-ttu-id="5e392-173">不带任何参数调用 Html.BeginForm() 会让其输出到当前请求的 URL 执行 HTTP POST 的窗体元素。</span><span class="sxs-lookup"><span data-stu-id="5e392-173">Calling Html.BeginForm() without any parameters will cause it to output a form element that does an HTTP-POST to the current request's URL.</span></span> <span data-ttu-id="5e392-174">编辑视图生成的它是为什么*&lt;表单操作 ="/ Dinners/编辑/1"方法 ="post"&gt;* 元素。</span><span class="sxs-lookup"><span data-stu-id="5e392-174">That is why our Edit view generates a *&lt;form action="/Dinners/Edit/1" method="post"&gt;* element.</span></span> <span data-ttu-id="5e392-175">我们无法具有或者传递显式参数给 Html.BeginForm() 如果我们想要发布到不同的 URL。</span><span class="sxs-lookup"><span data-stu-id="5e392-175">We could have alternatively passed explicit parameters to Html.BeginForm() if we wanted to post to a different URL.</span></span>

##### <a name="htmltextbox-helper-method"></a><span data-ttu-id="5e392-176">Html.TextBox() 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="5e392-176">Html.TextBox() helper method</span></span>

<span data-ttu-id="5e392-177">Edit.aspx 视图使用 Html.TextBox() 帮助器方法来输出&lt;type ="text"/&gt;元素：</span><span class="sxs-lookup"><span data-stu-id="5e392-177">Our Edit.aspx view uses the Html.TextBox() helper method to output &lt;input type="text"/&gt; elements:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

<span data-ttu-id="5e392-178">上面的 Html.TextBox() 方法采用单个参数 – 用于指定的 id/name 特性&lt;type ="text"/&gt;输出，以及要填充的文本框值的模型属性的元素。</span><span class="sxs-lookup"><span data-stu-id="5e392-178">The Html.TextBox() method above takes a single parameter – which is being used to specify both the id/name attributes of the &lt;input type="text"/&gt; element to output, as well as the model property to populate the textbox value from.</span></span> <span data-ttu-id="5e392-179">例如，我们传递给编辑视图的 Dinner 对象具有".NET Future"的"Title"属性值，因此我们 Html.TextBox("Title") 方法调用输出： *&lt;输入的 id ="Title"名称 ="Title"type ="text"value =".NET Futures"/&gt;*.</span><span class="sxs-lookup"><span data-stu-id="5e392-179">For example, the Dinner object we passed to the Edit view had a "Title" property value of ".NET Futures", and so our Html.TextBox("Title") method call output: *&lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.</span></span>

<span data-ttu-id="5e392-180">或者，我们可以使用第一个 Html.TextBox() 参数来指定 id/名称的元素，并显式传递值中要用作第二个参数：</span><span class="sxs-lookup"><span data-stu-id="5e392-180">Alternatively, we can use the first Html.TextBox() parameter to specify the id/name of the element, and then explicitly pass in the value to use as a second parameter:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

<span data-ttu-id="5e392-181">通常，我们需要执行的输出值的自定义格式设置。</span><span class="sxs-lookup"><span data-stu-id="5e392-181">Often we'll want to perform custom formatting on the value that is output.</span></span> <span data-ttu-id="5e392-182">内置于.NET string.format （) 的静态方法可用于这些方案。</span><span class="sxs-lookup"><span data-stu-id="5e392-182">The String.Format() static method built-into .NET is useful for these scenarios.</span></span> <span data-ttu-id="5e392-183">我们 Edit.aspx 视图模板使用此 EventDate 值 （这是类型为 DateTime 的） 的格式设置，以便它不会显示时间 （秒）：</span><span class="sxs-lookup"><span data-stu-id="5e392-183">Our Edit.aspx view template is using this to format the EventDate value (which is of type DateTime) so that it doesn't show seconds for the time:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

<span data-ttu-id="5e392-184">Html.TextBox() 的第三个参数 （可选） 用于输出其他 HTML 特性。</span><span class="sxs-lookup"><span data-stu-id="5e392-184">A third parameter to Html.TextBox() can optionally be used to output additional HTML attributes.</span></span> <span data-ttu-id="5e392-185">的以下代码段演示如何呈现其他大小 ="30"属性和 class ="mycssclass"属性上&lt;输入类型 ="text"/&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="5e392-185">The code-snippet below demonstrates how to render an additional size="30" attribute and a class="mycssclass" attribute on the &lt;input type="text"/&gt; element.</span></span> <span data-ttu-id="5e392-186">请注意，我们如何转义的类属性使用名称"@" character because "类"是保留的关键字在 C# 中：</span><span class="sxs-lookup"><span data-stu-id="5e392-186">Note how we are escaping the name of the class attribute using a "@" character because "class" is a reserved keyword in C#:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a><span data-ttu-id="5e392-187">实现 HTTP POST 编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="5e392-187">Implementing the HTTP-POST Edit Action Method</span></span>

<span data-ttu-id="5e392-188">现在，我们实现我们编辑操作方法的 HTTP GET 版本。</span><span class="sxs-lookup"><span data-stu-id="5e392-188">We now have the HTTP-GET version of our Edit action method implemented.</span></span> <span data-ttu-id="5e392-189">当用户请求 */Dinners/Edit/1*他们收到如下所示的 HTML 页面的 URL:</span><span class="sxs-lookup"><span data-stu-id="5e392-189">When a user requests the */Dinners/Edit/1* URL they receive an HTML page like the following:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

<span data-ttu-id="5e392-190">按"保存"按钮会导致窗体发布到 */Dinners/Edit/1* URL，并将其提交 HTML&lt;输入&gt;窗体上使用 HTTP POST 谓词值。</span><span class="sxs-lookup"><span data-stu-id="5e392-190">Pressing the "Save" button causes a form post to the */Dinners/Edit/1* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span> <span data-ttu-id="5e392-191">现在让我们来实现我们编辑操作方法-保存 Dinner 将处理的 HTTP POST 行为。</span><span class="sxs-lookup"><span data-stu-id="5e392-191">Let's now implement the HTTP POST behavior of our edit action method – which will handle saving the Dinner.</span></span>

<span data-ttu-id="5e392-192">我们将首先将重载的"编辑"操作方法添加到对其具有"AcceptVerbs"属性，指示它将处理 HTTP POST 方案我们 DinnersController:</span><span class="sxs-lookup"><span data-stu-id="5e392-192">We'll begin by adding an overloaded "Edit" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

<span data-ttu-id="5e392-193">当 [AcceptVerbs] 特性应用于重载的操作方法时，ASP.NET MVC 将自动处理将请求调度到相应的操作方法，具体取决于传入的 HTTP 谓词。</span><span class="sxs-lookup"><span data-stu-id="5e392-193">When the [AcceptVerbs] attribute is applied to overloaded action methods, ASP.NET MVC automatically handles dispatching requests to the appropriate action method depending on the incoming HTTP verb.</span></span> <span data-ttu-id="5e392-194">HTTP POST 请求到<em>/Dinners/编辑 / [id]</em> Url 将转到上面的编辑方法，同时对所有其他 HTTP 谓词请求<em>/Dinners/编辑 / [id]</em>Url 将转到第一个编辑方法我们实现 （它未不具有 [AcceptVerbs] 特性）。</span><span class="sxs-lookup"><span data-stu-id="5e392-194">HTTP POST requests to <em>/Dinners/Edit/[id]</em> URLs will go to the above Edit method, while all other HTTP verb requests to <em>/Dinners/Edit/[id]</em>URLs will go to the first Edit method we implemented (which did not have an [AcceptVerbs] attribute).</span></span>

| <span data-ttu-id="5e392-195">**端主题： 为什么通过 HTTP 谓词区分？**</span><span class="sxs-lookup"><span data-stu-id="5e392-195">**Side Topic: Why differentiate via HTTP verbs?**</span></span> |
| --- |
| <span data-ttu-id="5e392-196">您可能会问 – 为什么是我们使用一个 URL 并且个性化的 HTTP 谓词通过其行为？</span><span class="sxs-lookup"><span data-stu-id="5e392-196">You might ask – why are we using a single URL and differentiating its behavior via the HTTP verb?</span></span> <span data-ttu-id="5e392-197">为什么不只是具有两个不同的 Url 可以加载和保存的编辑更改？</span><span class="sxs-lookup"><span data-stu-id="5e392-197">Why not just have two separate URLs to handle loading and saving edit changes?</span></span> <span data-ttu-id="5e392-198">例如： /Dinners/编辑 / [id] 若要显示初始表单和 /Dinners/保存 / [id] 来处理窗体发布，将其保存？</span><span class="sxs-lookup"><span data-stu-id="5e392-198">For example: /Dinners/Edit/[id] to display the initial form and /Dinners/Save/[id] to handle the form post to save it?</span></span> <span data-ttu-id="5e392-199">与发布两个不同的 Url 的缺点是，在其中我们发布到 /Dinners/Save/2，，然后需要重新 HTML 窗体显示由于输入错误的情况下，最终用户将最终 （因为这是在其浏览器地址栏中拥有 Dinners/保存/2 URLURL 发布到窗体)。</span><span class="sxs-lookup"><span data-stu-id="5e392-199">The downside with publishing two separate URLs is that in cases where we post to /Dinners/Save/2, and then need to redisplay the HTML form because of an input error, the end-user will end up having the /Dinners/Save/2 URL in their browser's address bar (since that was the URL the form posted to).</span></span> <span data-ttu-id="5e392-200">如果最终用户创建一个书签，本页 redisplayed 到用户浏览器的收藏夹列表，或复制/粘贴该 URL 和电子邮件发送给朋友，它们将得到保存 （因为该 URL 依赖于 post 值） 不会在将来工作的 URL。</span><span class="sxs-lookup"><span data-stu-id="5e392-200">If the end-user bookmarks this redisplayed page to their browser favorites list, or copy/pastes the URL and emails it to a friend, they will end up saving a URL that won't work in the future (since that URL depends on post values).</span></span> <span data-ttu-id="5e392-201">通过公开一个 URL (例如： /Dinners/Edit/[id]) 并且个性化的处理它的 HTTP 谓词，它是安全的最终用户可以编辑页面加入书签和/或将 URL 发送给其他人。</span><span class="sxs-lookup"><span data-stu-id="5e392-201">By exposing a single URL (like: /Dinners/Edit/[id]) and differentiating the processing of it by HTTP verb, it is safe for end-users to bookmark the edit page and/or send the URL to others.</span></span> |

#### <a name="retrieving-form-post-values"></a><span data-ttu-id="5e392-202">检索窗体发布值</span><span class="sxs-lookup"><span data-stu-id="5e392-202">Retrieving Form Post Values</span></span>

<span data-ttu-id="5e392-203">有多种方式我们就可以访问发布窗体中"的编辑"我们 HTTP POST 方法的参数。</span><span class="sxs-lookup"><span data-stu-id="5e392-203">There are a variety of ways we can access posted form parameters within our HTTP POST "Edit" method.</span></span> <span data-ttu-id="5e392-204">一个简单的方法是只需使用控制器基类上的请求属性来访问窗体集合和直接检索已发布的值：</span><span class="sxs-lookup"><span data-stu-id="5e392-204">One simple approach is to just use the Request property on the Controller base class to access the form collection and retrieve the posted values directly:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

<span data-ttu-id="5e392-205">不过，尤其是后我们将添加错误处理逻辑，上述方法是有些繁琐。</span><span class="sxs-lookup"><span data-stu-id="5e392-205">The above approach is a little verbose, though, especially once we add error handling logic.</span></span>

<span data-ttu-id="5e392-206">一个更好的方法了这种情况，可以利用内置*UpdateModel()* 控制器基类上的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="5e392-206">A better approach for this scenario is to leverage the built-in *UpdateModel()* helper method on the Controller base class.</span></span> <span data-ttu-id="5e392-207">它支持更新的属性，我们将它使用传入的窗体参数传递的对象。</span><span class="sxs-lookup"><span data-stu-id="5e392-207">It supports updating the properties of an object we pass it using the incoming form parameters.</span></span> <span data-ttu-id="5e392-208">它使用反射来确定对对象的属性名称会自动将转换并将值分配给这些客户端提交的输入值。</span><span class="sxs-lookup"><span data-stu-id="5e392-208">It uses reflection to determine the property names on the object, and then automatically converts and assigns values to them based on the input values submitted by the client.</span></span>

<span data-ttu-id="5e392-209">我们可以使用 UpdateModel() 方法来简化使用此代码我们 HTTP POST 编辑操作：</span><span class="sxs-lookup"><span data-stu-id="5e392-209">We could use the UpdateModel() method to simplify our HTTP-POST Edit Action using this code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

<span data-ttu-id="5e392-210">我们现在可以访问 */Dinners/Edit/1* URL，并更改我们 Dinner 标题：</span><span class="sxs-lookup"><span data-stu-id="5e392-210">We can now visit the */Dinners/Edit/1* URL, and change the title of our Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

<span data-ttu-id="5e392-211">当我们单击"保存"按钮时，我们将执行窗体发布到我们的编辑操作，并更新后的值将保留在数据库中。</span><span class="sxs-lookup"><span data-stu-id="5e392-211">When we click the "Save" button, we'll perform a form post to our Edit action, and the updated values will be persisted in the database.</span></span> <span data-ttu-id="5e392-212">我们将随后重定向到详细信息 URL 为 Dinner （这将显示新保存的值）：</span><span class="sxs-lookup"><span data-stu-id="5e392-212">We will then be redirected to the Details URL for the Dinner (which will display the newly saved values):</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a><span data-ttu-id="5e392-213">处理编辑错误</span><span class="sxs-lookup"><span data-stu-id="5e392-213">Handling Edit Errors</span></span>

<span data-ttu-id="5e392-214">我们当前的 HTTP POST 实现 works 微调 – 除非有错误。</span><span class="sxs-lookup"><span data-stu-id="5e392-214">Our current HTTP-POST implementation works fine – except when there are errors.</span></span>

<span data-ttu-id="5e392-215">当用户编辑窗体的一个错误，我们需要确保窗体将重新显示信息性错误消息，指导他们要修复此错误。</span><span class="sxs-lookup"><span data-stu-id="5e392-215">When a user makes a mistake editing a form, we need to make sure that the form is redisplayed with an informative error message that guides them to fix it.</span></span> <span data-ttu-id="5e392-216">这包括最终用户在其中发布输入不正确的情况下 (例如： 的格式不正确的日期字符串)，如事例以及输入的格式是否有效，但没有业务规则冲突。</span><span class="sxs-lookup"><span data-stu-id="5e392-216">This includes cases where an end-user posts incorrect input (for example: a malformed date string), as well as cases where the input format is valid but there is a business rule violation.</span></span> <span data-ttu-id="5e392-217">出现错误时在窗体应保留输入的数据最初输入，以便他们不需要手动重新填充其更改的用户。</span><span class="sxs-lookup"><span data-stu-id="5e392-217">When errors occur the form should preserve the input data the user originally entered so that they don't have to refill their changes manually.</span></span> <span data-ttu-id="5e392-218">窗体已成功完成之前，应根据需要多次重复此过程。</span><span class="sxs-lookup"><span data-stu-id="5e392-218">This process should repeat as many times as necessary until the form successfully completes.</span></span>

<span data-ttu-id="5e392-219">ASP.NET MVC 包括一些不错的内置功能，可使错误处理和窗体起简单。</span><span class="sxs-lookup"><span data-stu-id="5e392-219">ASP.NET MVC includes some nice built-in features that make error handling and form redisplay easy.</span></span> <span data-ttu-id="5e392-220">若要查看操作中的这些功能，让我们使用以下代码更新我们的编辑操作方法：</span><span class="sxs-lookup"><span data-stu-id="5e392-220">To see these features in action let's update our Edit action method with the following code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

<span data-ttu-id="5e392-221">上面的代码类似于我们以前的实现 – 只是我们现在包装在 try/catch 错误处理块围绕我们的工作。</span><span class="sxs-lookup"><span data-stu-id="5e392-221">The above code is similar to our previous implementation – except that we are now wrapping a try/catch error handling block around our work.</span></span> <span data-ttu-id="5e392-222">调用 UpdateModel()，或在我们尝试并保存 DinnerRepository （这将引发异常，如果我们尝试保存的 Dinner 对象是无效的由于我们的模型中的规则冲突），如果发生异常时将我们 catch 错误处理块执行。</span><span class="sxs-lookup"><span data-stu-id="5e392-222">If an exception occurs either when calling UpdateModel(), or when we try and save the DinnerRepository (which will raise an exception if the Dinner object we are trying to save is invalid because of a rule violation within our model), our catch error handling block will execute.</span></span> <span data-ttu-id="5e392-223">在其中我们循环访问 Dinner 对象中存在任何规则冲突，并将其添加到 ModelState 对象 （我们将稍后讨论）。</span><span class="sxs-lookup"><span data-stu-id="5e392-223">Within it we loop over any rule violations that exist in the Dinner object and add them to a ModelState object (which we'll discuss shortly).</span></span> <span data-ttu-id="5e392-224">然后，我们重新显示该视图。</span><span class="sxs-lookup"><span data-stu-id="5e392-224">We then redisplay the view.</span></span>

<span data-ttu-id="5e392-225">若要查看此工作让我们重新运行该应用程序，编辑 Dinner，并将其更改为具有空标题，EventDate"BOGUS"，并使用美国国家/地区值为英国电话号码。</span><span class="sxs-lookup"><span data-stu-id="5e392-225">To see this working let's re-run the application, edit a Dinner, and change it to have an empty Title, an EventDate of "BOGUS", and use a UK phone number with a country value of USA.</span></span> <span data-ttu-id="5e392-226">当我们按"保存"按钮时我们编辑 HTTP POST 方法将不能保存 Dinner （因为有错误） 以及将重新显示该窗体：</span><span class="sxs-lookup"><span data-stu-id="5e392-226">When we press the "Save" button our HTTP POST Edit method will not be able to save the Dinner (because there are errors) and will redisplay the form:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

<span data-ttu-id="5e392-227">我们的应用程序具有适当的错误体验。</span><span class="sxs-lookup"><span data-stu-id="5e392-227">Our application has a decent error experience.</span></span> <span data-ttu-id="5e392-228">具有无效的输入的文本元素突出显示为红色，并向最终用户有关其显示验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="5e392-228">The text elements with the invalid input are highlighted in red, and validation error messages are displayed to the end user about them.</span></span> <span data-ttu-id="5e392-229">在窗体还保留用户最初输入 – 的输入的数据，以便他们无需重新填充任何内容。</span><span class="sxs-lookup"><span data-stu-id="5e392-229">The form is also preserving the input data the user originally entered – so that they don't have to refill anything.</span></span>

<span data-ttu-id="5e392-230">如何，您可能会问，这发生一样？</span><span class="sxs-lookup"><span data-stu-id="5e392-230">How, you might ask, did this occur?</span></span> <span data-ttu-id="5e392-231">如何没有 Title、 EventDate 和 contactphone 文本框以红色突出显示本身并知道要输出的最初输入的用户值？</span><span class="sxs-lookup"><span data-stu-id="5e392-231">How did the Title, EventDate, and ContactPhone textboxes highlight themselves in red and know to output the originally entered user values?</span></span> <span data-ttu-id="5e392-232">和如何未显示错误消息获取顶部列表中？</span><span class="sxs-lookup"><span data-stu-id="5e392-232">And how did error messages get displayed in the list at the top?</span></span> <span data-ttu-id="5e392-233">值得高兴的是，这并不发生变魔术一样-而是因为我们使用一些内置的 ASP.NET MVC 功能，使输入的验证和错误处理方案轻松。</span><span class="sxs-lookup"><span data-stu-id="5e392-233">The good news is that this didn't occur by magic - rather it was because we used some of the built-in ASP.NET MVC features that make input validation and error handling scenarios easy.</span></span>

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a><span data-ttu-id="5e392-234">了解 ModelState 和验证的 HTML 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="5e392-234">Understanding ModelState and the Validation HTML Helper Methods</span></span>

<span data-ttu-id="5e392-235">控制器类具有一个"ModelState"属性集合，它提供了一种方法，以指示错误存在与传递给视图的模型对象。</span><span class="sxs-lookup"><span data-stu-id="5e392-235">Controller classes have a "ModelState" property collection which provides a way to indicate that errors exist with a model object being passed to a View.</span></span> <span data-ttu-id="5e392-236">ModelState 集合中的错误条目与问题标识模型属性的名称 (例如:"Title"、"EventDate"或"ContactPhone")，并允许指定的用户友好错误消息 (例如:"标题是必需的")。</span><span class="sxs-lookup"><span data-stu-id="5e392-236">Error entries within the ModelState collection identify the name of the model property with the issue (for example: "Title", "EventDate", or "ContactPhone"), and allow a human-friendly error message to be specified (for example: "Title is required").</span></span>

<span data-ttu-id="5e392-237">*UpdateModel()* 帮助器方法尝试将窗体值分配给模型对象的属性时遇到错误时自动填充 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="5e392-237">The *UpdateModel()* helper method automatically populates the ModelState collection when it encounters errors while trying to assign form values to properties on the model object.</span></span> <span data-ttu-id="5e392-238">例如，我们的 Dinner 对象 EventDate 属性是 DateTime 类型。</span><span class="sxs-lookup"><span data-stu-id="5e392-238">For example, our Dinner object's EventDate property is of type DateTime.</span></span> <span data-ttu-id="5e392-239">当 UpdateModel() 方法不能为其分配的字符串值"BOGUS"，在上述方案中时，UpdateModel() 方法添加到表示分配错误的错误的 ModelState 集合的一个条目发生与该属性。</span><span class="sxs-lookup"><span data-stu-id="5e392-239">When the UpdateModel() method was unable to assign the string value "BOGUS" to it in the scenario above, the UpdateModel() method added an entry to the ModelState collection indicating an assignment error had occurred with that property.</span></span>

<span data-ttu-id="5e392-240">开发人员还可以编写代码以显式添加到 ModelState 集合错误条目，像我们在下面我们"捕获"错误处理块内，这使用基于中活动的规则冲突项填充 ModelState 集合Dinner 对象：</span><span class="sxs-lookup"><span data-stu-id="5e392-240">Developers can also write code to explicitly add error entries into the ModelState collection like we are doing below within our "catch" error handling block, which is populating the ModelState collection with entries based on the active Rule Violations in the Dinner object:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a><span data-ttu-id="5e392-241">与 ModelState 的 html 帮助器集成</span><span class="sxs-lookup"><span data-stu-id="5e392-241">Html Helper Integration with ModelState</span></span>

<span data-ttu-id="5e392-242">呈现输出时，HTML 帮助器方法-如 Html.TextBox()-检查 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="5e392-242">HTML helper methods - like Html.TextBox() - check the ModelState collection when rendering output.</span></span> <span data-ttu-id="5e392-243">如果存在错误的项，它们呈现用户输入值和 CSS 错误类。</span><span class="sxs-lookup"><span data-stu-id="5e392-243">If an error for the item exists, they render the user-entered value and a CSS error class.</span></span>

<span data-ttu-id="5e392-244">例如，"编辑"视图中我们使用 Html.TextBox() 帮助器方法呈现的我们的 Dinner 对象 EventDate:</span><span class="sxs-lookup"><span data-stu-id="5e392-244">For example, in our "Edit" view we are using the Html.TextBox() helper method to render the EventDate of our Dinner object:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

<span data-ttu-id="5e392-245">错误方案中呈现视图时，Html.TextBox() 方法将检查以查看是否存在与我们的 Dinner 对象"EventDate"属性相关联的任何错误的 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="5e392-245">When the view was rendered in the error scenario, the Html.TextBox() method checked the ModelState collection to see if there were any errors associated with the "EventDate" property of our Dinner object.</span></span> <span data-ttu-id="5e392-246">当不确定时出错它将呈现提交的用户输入 ("BOGUS") 作为值，并添加 css 错误类中的，以便&lt;type ="textbox"/&gt;它生成的标记：</span><span class="sxs-lookup"><span data-stu-id="5e392-246">When it determined that there was an error it rendered the submitted user input ("BOGUS") as the value, and added a css error class to the &lt;input type="textbox"/&gt; markup it generated:</span></span>

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

<span data-ttu-id="5e392-247">您可以自定义要查找但是您希望 css 错误类的外观。</span><span class="sxs-lookup"><span data-stu-id="5e392-247">You can customize the appearance of the css error class to look however you want.</span></span> <span data-ttu-id="5e392-248">中定义的默认 CSS 错误类 –"输入的验证错误"– *\content\site.css*样式表和看起来如下所示：</span><span class="sxs-lookup"><span data-stu-id="5e392-248">The default CSS error class – "input-validation-error" – is defined in the *\content\site.css* stylesheet and looks like below:</span></span>

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

<span data-ttu-id="5e392-249">此 CSS 规则是什么导致我们无效的输入的元素，如下面突出显示：</span><span class="sxs-lookup"><span data-stu-id="5e392-249">This CSS rule is what caused our invalid input elements to be highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a><span data-ttu-id="5e392-250">Html.ValidationMessage() 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="5e392-250">Html.ValidationMessage() Helper Method</span></span>

<span data-ttu-id="5e392-251">Html.ValidationMessage() 帮助器方法可用于输出与特定的模型属性关联的 ModelState 错误消息：</span><span class="sxs-lookup"><span data-stu-id="5e392-251">The Html.ValidationMessage() helper method can be used to output the ModelState error message associated with a particular model property:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

<span data-ttu-id="5e392-252">上述代码输出：  *&lt;/><span class ="字段的验证错误"&gt;是无效的值 BOGUS &lt; /s p a n&gt;*</span><span class="sxs-lookup"><span data-stu-id="5e392-252">The above code outputs: *&lt;span class="field-validation-error"&gt; The value ‘BOGUS' is invalid&lt;/span&gt;*</span></span>

<span data-ttu-id="5e392-253">Html.ValidationMessage() 帮助器方法还支持允许开发人员重写为显示的错误文本消息的第二个参数：</span><span class="sxs-lookup"><span data-stu-id="5e392-253">The Html.ValidationMessage() helper method also supports a second parameter that allows developers to override the error text message that is displayed:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

<span data-ttu-id="5e392-254">上述代码输出：  <em>&lt;/><span class ="字段的验证错误"&gt;\*&lt;/s p a n&gt;</em>而不是时出现错误时，将提供的默认错误文本EventDate 属性。</span><span class="sxs-lookup"><span data-stu-id="5e392-254">The above code outputs: <em>&lt;span class="field-validation-error"&gt;\*&lt;/span&gt;</em>instead of the default error text when an error is present for the EventDate property.</span></span>

##### <a name="htmlvalidationsummary-helper-method"></a><span data-ttu-id="5e392-255">Html.ValidationSummary() 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="5e392-255">Html.ValidationSummary() Helper Method</span></span>

<span data-ttu-id="5e392-256">Html.ValidationSummary() 帮助器方法可用于呈现摘要错误消息，伴随&lt;ul&gt;&lt;li /&gt;&lt;/u l&gt;消息中的所有详细的错误列表ModelState 集合：</span><span class="sxs-lookup"><span data-stu-id="5e392-256">The Html.ValidationSummary() helper method can be used to render a summary error message, accompanied by a &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; list of all detailed error messages in the ModelState collection:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

<span data-ttu-id="5e392-257">Html.ValidationSummary() 帮助程序方法采用一个可选的字符串参数 – 用于定义要显示详细的错误列表上方的摘要错误消息：</span><span class="sxs-lookup"><span data-stu-id="5e392-257">The Html.ValidationSummary() helper method takes an optional string parameter – which defines a summary error message to display above the list of detailed errors:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

<span data-ttu-id="5e392-258">您可以选择使用 CSS 来重写错误列表如下所示。</span><span class="sxs-lookup"><span data-stu-id="5e392-258">You can optionally use CSS to override what the error list looks like.</span></span>

#### <a name="using-a-addruleviolations-helper-method"></a><span data-ttu-id="5e392-259">使用 AddRuleViolations 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="5e392-259">Using a AddRuleViolations Helper Method</span></span>

<span data-ttu-id="5e392-260">我们的初始 HTTP POST 编辑实现使用它的 catch 块中的 foreach 语句循环访问 Dinner 对象的规则冲突，并将其添加到控制器的 ModelState 集合：</span><span class="sxs-lookup"><span data-stu-id="5e392-260">Our initial HTTP-POST Edit implementation used a foreach statement within its catch block to loop over the Dinner object's Rule Violations and add them to the controller's ModelState collection:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

<span data-ttu-id="5e392-261">我们可以使此代码通过添加"ControllerHelpers"小更加清晰明确到 NerdDinner 项目中，类，实现"AddRuleViolations"扩展方法在其中将一个帮助器方法添加到 ASP.NET MVC ModelStateDictionary 类。</span><span class="sxs-lookup"><span data-stu-id="5e392-261">We can make this code a little cleaner by adding a "ControllerHelpers" class to the NerdDinner project, and implement an "AddRuleViolations" extension method within it that adds a helper method to the ASP.NET MVC ModelStateDictionary class.</span></span> <span data-ttu-id="5e392-262">此扩展方法可以封装填充 ModelStateDictionary RuleViolation 错误的列表所需的逻辑：</span><span class="sxs-lookup"><span data-stu-id="5e392-262">This extension method can encapsulate the logic necessary to populate the ModelStateDictionary with a list of RuleViolation errors:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

<span data-ttu-id="5e392-263">然后，我们可以更新我们编辑 HTTP POST 操作方法使用此扩展方法来填充我们 Dinner 规则冲突的 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="5e392-263">We can then update our HTTP-POST Edit action method to use this extension method to populate the ModelState collection with our Dinner Rule Violations.</span></span>

#### <a name="complete-edit-action-method-implementations"></a><span data-ttu-id="5e392-264">完成编辑操作的方法实现</span><span class="sxs-lookup"><span data-stu-id="5e392-264">Complete Edit Action Method Implementations</span></span>

<span data-ttu-id="5e392-265">下面的代码实现了所有我们的编辑方案所需的控制器逻辑：</span><span class="sxs-lookup"><span data-stu-id="5e392-265">The code below implements all of the controller logic necessary for our Edit scenario:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

<span data-ttu-id="5e392-266">我们的编辑实现好处是，我们的控制器类和视图模板都不必须完全了解特定验证或通过我们的 Dinner 模型强制实施的业务规则。</span><span class="sxs-lookup"><span data-stu-id="5e392-266">The nice thing about our Edit implementation is that neither our Controller class nor our View template has to know anything about the specific validation or business rules being enforced by our Dinner model.</span></span> <span data-ttu-id="5e392-267">我们可以将其他规则在将来添加到我们的模型并不需要对我们的控制器或视图以使其支持进行任何代码更改。</span><span class="sxs-lookup"><span data-stu-id="5e392-267">We can add additional rules to our model in the future and do not have to make any code changes to our controller or view in order for them to be supported.</span></span> <span data-ttu-id="5e392-268">这为我们提供了灵活地可以方便地改进我们的应用程序要求在将来使用最少代码更改。</span><span class="sxs-lookup"><span data-stu-id="5e392-268">This provides us with the flexibility to easily evolve our application requirements in the future with a minimum of code changes.</span></span>

### <a name="create-support"></a><span data-ttu-id="5e392-269">创建的支持</span><span class="sxs-lookup"><span data-stu-id="5e392-269">Create Support</span></span>

<span data-ttu-id="5e392-270">我们已实现我们的 DinnersController 类的"编辑"行为。</span><span class="sxs-lookup"><span data-stu-id="5e392-270">We've finished implementing the "Edit" behavior of our DinnersController class.</span></span> <span data-ttu-id="5e392-271">让我们继续操作，以便可对其 – 这将使用户能够添加新 Dinners"创建"支持。</span><span class="sxs-lookup"><span data-stu-id="5e392-271">Let's now move on to implement the "Create" support on it – which will enable users to add new Dinners.</span></span>

#### <a name="the-http-get-create-action-method"></a><span data-ttu-id="5e392-272">HTTP GET 创建操作方法</span><span class="sxs-lookup"><span data-stu-id="5e392-272">The HTTP-GET Create Action Method</span></span>

<span data-ttu-id="5e392-273">我们将首先实现 HTTP"GET"行为的我们创建操作方法。</span><span class="sxs-lookup"><span data-stu-id="5e392-273">We'll begin by implementing the HTTP "GET" behavior of our create action method.</span></span> <span data-ttu-id="5e392-274">在有人访问时，将调用此方法 */Dinners/创建*URL。</span><span class="sxs-lookup"><span data-stu-id="5e392-274">This method will be called when someone visits the */Dinners/Create* URL.</span></span> <span data-ttu-id="5e392-275">我们的实现如下所示：</span><span class="sxs-lookup"><span data-stu-id="5e392-275">Our implementation looks like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

<span data-ttu-id="5e392-276">上面的代码创建一个新的 Dinner 对象，并分配其 EventDate 属性设置为在将来的一周。</span><span class="sxs-lookup"><span data-stu-id="5e392-276">The code above creates a new Dinner object, and assigns its EventDate property to be one week in the future.</span></span> <span data-ttu-id="5e392-277">然后，它将呈现一个视图，它基于新的 Dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="5e392-277">It then renders a View that is based on the new Dinner object.</span></span> <span data-ttu-id="5e392-278">因为我们尚未显式传递将名称传递给*View()* 帮助器方法，它将使用的约定，其默认路径来解析视图模板： /Views/Dinners/Create.aspx。</span><span class="sxs-lookup"><span data-stu-id="5e392-278">Because we haven't explicitly passed a name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Create.aspx.</span></span>

<span data-ttu-id="5e392-279">让我们现在创建此视图模板。</span><span class="sxs-lookup"><span data-stu-id="5e392-279">Let's now create this view template.</span></span> <span data-ttu-id="5e392-280">我们可以创建操作方法内右键单击并选择"添加视图"上下文菜单命令来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="5e392-280">We can do this by right-clicking within the Create action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="5e392-281">在"添加视图"对话框中，我们将指示我们要将 Dinner 对象传递给视图模板，然后选择自动基架"创建"模板：</span><span class="sxs-lookup"><span data-stu-id="5e392-281">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to the view template, and choose to auto-scaffold a "Create" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

<span data-ttu-id="5e392-282">当我们单击"添加"按钮时，Visual Studio 会将新的基架基于"Create.aspx"视图保存到"\Views\Dinners"目录，并在 IDE 中打开它：</span><span class="sxs-lookup"><span data-stu-id="5e392-282">When we click the "Add" button, Visual Studio will save a new scaffold-based "Create.aspx" view to the "\Views\Dinners" directory, and open it up within the IDE:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

<span data-ttu-id="5e392-283">让我们对我们而言，到默认"创建"基架生成的文件已进行一些更改，并向上修改要看到如下所示：</span><span class="sxs-lookup"><span data-stu-id="5e392-283">Let's make a few changes to the default "create" scaffold file that was generated for us, and modify it up to look like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

<span data-ttu-id="5e392-284">现在，当我们运行我们的应用程序和访问权限和 *"/ Dinners/创建"* 它会从我们创建的操作实现呈现 UI 中的，如下面的浏览器中的 URL:</span><span class="sxs-lookup"><span data-stu-id="5e392-284">And now when we run our application and access the *"/Dinners/Create"* URL within the browser it will render UI like below from our Create action implementation:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a><span data-ttu-id="5e392-285">创建实现 HTTP POST 操作方法</span><span class="sxs-lookup"><span data-stu-id="5e392-285">Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="5e392-286">我们已实现我们创建操作方法的 HTTP GET 版本。</span><span class="sxs-lookup"><span data-stu-id="5e392-286">We have the HTTP-GET version of our Create action method implemented.</span></span> <span data-ttu-id="5e392-287">当用户单击"保存"按钮时它会执行窗体发布到 */Dinners/创建*URL，并将其提交 HTML&lt;输入&gt;窗体上使用 HTTP POST 谓词值。</span><span class="sxs-lookup"><span data-stu-id="5e392-287">When a user clicks the "Save" button it performs a form post to the */Dinners/Create* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span>

<span data-ttu-id="5e392-288">让我们现在实现 HTTP POST 行为的我们创建操作方法。</span><span class="sxs-lookup"><span data-stu-id="5e392-288">Let's now implement the HTTP POST behavior of our create action method.</span></span> <span data-ttu-id="5e392-289">我们将首先将重载的"创建"操作方法添加到对其具有"AcceptVerbs"属性，指示它将处理 HTTP POST 方案我们 DinnersController:</span><span class="sxs-lookup"><span data-stu-id="5e392-289">We'll begin by adding an overloaded "Create" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

<span data-ttu-id="5e392-290">有多种方式可以访问已发布的表单参数中我们的 HTTP POST 启用"创建"方法。</span><span class="sxs-lookup"><span data-stu-id="5e392-290">There are a variety of ways we can access the posted form parameters within our HTTP-POST enabled "Create" method.</span></span>

<span data-ttu-id="5e392-291">一种方法是创建一个新的 Dinner 对象，然后使用*UpdateModel()* 帮助器方法 （如我们所做的编辑操作） 要使用已发布的表单值填充它。</span><span class="sxs-lookup"><span data-stu-id="5e392-291">One approach is to create a new Dinner object and then use the *UpdateModel()* helper method (like we did with the Edit action) to populate it with the posted form values.</span></span> <span data-ttu-id="5e392-292">我们然后可以将其添加到我们 DinnerRepository、 将其保存到数据库，并将用户重定向到我们的详细信息操作以显示新创建的 Dinner 使用下面的代码：</span><span class="sxs-lookup"><span data-stu-id="5e392-292">We can then add it to our DinnerRepository, persist it to the database, and redirect the user to our Details action to show the newly created Dinner using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

<span data-ttu-id="5e392-293">或者，我们可以使用一种方法还有我们采用 Dinner 对象作为方法参数的 create （） 操作方法。</span><span class="sxs-lookup"><span data-stu-id="5e392-293">Alternatively, we can use an approach where we have our Create() action method take a Dinner object as a method parameter.</span></span> <span data-ttu-id="5e392-294">ASP.NET MVC 将自动为我们实例化一个新的 Dinner 对象、 填充其属性使用窗体的输入，并将其传递给我们的操作方法：</span><span class="sxs-lookup"><span data-stu-id="5e392-294">ASP.NET MVC will then automatically instantiate a new Dinner object for us, populate its properties using the form inputs, and pass it to our action method:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

<span data-ttu-id="5e392-295">我们上面的操作方法验证，Dinner 对象成功填充窗体发布值与通过检查 ModelState.IsValid 属性。</span><span class="sxs-lookup"><span data-stu-id="5e392-295">Our action method above verifies that the Dinner object has been successfully populated with the form post values by checking the ModelState.IsValid property.</span></span> <span data-ttu-id="5e392-296">这将返回 false，如果有输入转换问题 (例如： EventDate 属性"BOGUS"的字符串)，并且如果有任何问题我们操作方法重新显示该窗体。</span><span class="sxs-lookup"><span data-stu-id="5e392-296">This will return false if there are input conversion issues (for example: a string of "BOGUS" for the EventDate property), and if there are any issues our action method redisplays the form.</span></span>

<span data-ttu-id="5e392-297">如果输入的值都有效，操作方法就尝试添加并将新的 Dinner 保存到 DinnerRepository。</span><span class="sxs-lookup"><span data-stu-id="5e392-297">If the input values are valid, then the action method attempts to add and save the new Dinner to the DinnerRepository.</span></span> <span data-ttu-id="5e392-298">它包装这项工作在 try/catch 块内的，并重新显示该窗体，如果有任何业务规则冲突 （这会导致 dinnerRepository.Save() 方法来引发异常）。</span><span class="sxs-lookup"><span data-stu-id="5e392-298">It wraps this work within a try/catch block and redisplays the form if there are any business rule violations (which would cause the dinnerRepository.Save() method to raise an exception).</span></span>

<span data-ttu-id="5e392-299">若要查看此错误处理操作中的行为，我们可以请求 */Dinners/创建*URL 和有关新 Dinner 的详细信息，请填写。</span><span class="sxs-lookup"><span data-stu-id="5e392-299">To see this error handling behavior in action, we can request the */Dinners/Create* URL and fill out details about a new Dinner.</span></span> <span data-ttu-id="5e392-300">输入不正确或值将导致创建窗体以重新显示如以下突出显示的错误：</span><span class="sxs-lookup"><span data-stu-id="5e392-300">Incorrect input or values will cause the create form to be redisplayed with the errors highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

<span data-ttu-id="5e392-301">请注意，我们创建窗体如何遵循确切相同验证和业务规则作为我们的编辑窗体。</span><span class="sxs-lookup"><span data-stu-id="5e392-301">Notice how our Create form is honoring the exact same validation and business rules as our Edit form.</span></span> <span data-ttu-id="5e392-302">这是因为我们验证和业务规则在模型中，定义和未嵌入在 UI 或应用程序的控制器中。</span><span class="sxs-lookup"><span data-stu-id="5e392-302">This is because our validation and business rules were defined in the model, and were not embedded within the UI or controller of the application.</span></span> <span data-ttu-id="5e392-303">这意味着我们可以稍后更改/改进我们验证或在单个的业务规则放置，并将它们应用于整个应用程序。</span><span class="sxs-lookup"><span data-stu-id="5e392-303">This means we can later change/evolve our validation or business rules in a single place and have them apply throughout our application.</span></span> <span data-ttu-id="5e392-304">我们不会更改任何代码中的我们编辑或创建操作方法来自动接受任何新的规则或对现有的修改。</span><span class="sxs-lookup"><span data-stu-id="5e392-304">We will not have to change any code within either our Edit or Create action methods to automatically honor any new rules or modifications to existing ones.</span></span>

<span data-ttu-id="5e392-305">我们修复输入的值并单击"保存"按钮时同样，我们加入 DinnerRepository 将成功，并且新 Dinner 将添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="5e392-305">When we fix the input values and click the "Save" button again, our addition to the DinnerRepository will succeed, and a new Dinner will be added to the database.</span></span> <span data-ttu-id="5e392-306">我们随后重定向到 */Dinners/详细信息 / [id]* URL – 其中我们将提供有关新创建的 Dinner 的详细信息：</span><span class="sxs-lookup"><span data-stu-id="5e392-306">We will then be redirected to the */Dinners/Details/[id]* URL – where we will be presented with details about the newly created Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a><span data-ttu-id="5e392-307">删除支持</span><span class="sxs-lookup"><span data-stu-id="5e392-307">Delete Support</span></span>

<span data-ttu-id="5e392-308">让我们现在添加到我们 DinnersController 的"删除"支持。</span><span class="sxs-lookup"><span data-stu-id="5e392-308">Let's now add "Delete" support to our DinnersController.</span></span>

#### <a name="the-http-get-delete-action-method"></a><span data-ttu-id="5e392-309">HTTP GET Delete 操作方法</span><span class="sxs-lookup"><span data-stu-id="5e392-309">The HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="5e392-310">我们将首先实现我们的 delete 操作方法的 HTTP GET 行为。</span><span class="sxs-lookup"><span data-stu-id="5e392-310">We'll begin by implementing the HTTP GET behavior of our delete action method.</span></span> <span data-ttu-id="5e392-311">在有人访问时，将会调用此方法 */Dinners/Delete / [id]* URL。</span><span class="sxs-lookup"><span data-stu-id="5e392-311">This method will get called when someone visits the */Dinners/Delete/[id]* URL.</span></span> <span data-ttu-id="5e392-312">下面是实现：</span><span class="sxs-lookup"><span data-stu-id="5e392-312">Below is the implementation:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

<span data-ttu-id="5e392-313">尝试检索 Dinner 要删除的操作方法。</span><span class="sxs-lookup"><span data-stu-id="5e392-313">The action method attempts to retrieve the Dinner to be deleted.</span></span> <span data-ttu-id="5e392-314">如果 Dinner 存在，则呈现视图基于 Dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="5e392-314">If the Dinner exists it renders a View based on the Dinner object.</span></span> <span data-ttu-id="5e392-315">如果对象不存在 （或已被删除） 它返回一个视图，它将呈现"NotFound"查看我们以前为我们的"详细信息"操作方法创建的模板。</span><span class="sxs-lookup"><span data-stu-id="5e392-315">If the object doesn't exist (or has already been deleted) it returns a View that renders the "NotFound" view template we created earlier for our "Details" action method.</span></span>

<span data-ttu-id="5e392-316">我们可以创建"删除"查看模板的 Delete 操作方法内右键单击并选择"添加视图"上下文菜单命令。</span><span class="sxs-lookup"><span data-stu-id="5e392-316">We can create the "Delete" view template by right-clicking within the Delete action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="5e392-317">在"添加视图"对话框中，我们将指示我们 Dinner 对象传递给视图模板作为它的模型，并选择创建一个空的模板：</span><span class="sxs-lookup"><span data-stu-id="5e392-317">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to create an empty template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

<span data-ttu-id="5e392-318">当我们单击"添加"按钮时，Visual Studio 将我们"\Views\Dinners"目录中为我们添加新的"Delete.aspx"视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="5e392-318">When we click the "Add" button, Visual Studio will add a new "Delete.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="5e392-319">我们将向模板来实现删除确认屏幕中添加一些 HTML 和代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="5e392-319">We'll add some HTML and code to the template to implement a delete confirmation screen like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

<span data-ttu-id="5e392-320">上面的代码显示的标题，Dinner 要删除，然后输出&lt;窗体&gt;执行 POST 到 /Dinners/Delete / [id] URL，如果最终用户单击"删除"按钮中的元素。</span><span class="sxs-lookup"><span data-stu-id="5e392-320">The code above displays the title of the Dinner to be deleted, and outputs a &lt;form&gt; element that does a POST to the /Dinners/Delete/[id] URL if the end-user clicks the "Delete" button within it.</span></span>

<span data-ttu-id="5e392-321">当我们运行我们的应用程序和访问 *"/ Dinners/Delete / [id]"* URL 有效 Dinner 对象它呈现用户界面与下面类似：</span><span class="sxs-lookup"><span data-stu-id="5e392-321">When we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it renders UI like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| <span data-ttu-id="5e392-322">**端主题： 我们为何做一个帖子？**</span><span class="sxs-lookup"><span data-stu-id="5e392-322">**Side Topic: Why are we doing a POST?**</span></span> |
| --- |
| <span data-ttu-id="5e392-323">您可能会问 – 我们为何做通过创建的工作量&lt;窗体&gt;我们删除确认屏幕中？</span><span class="sxs-lookup"><span data-stu-id="5e392-323">You might ask – why did we go through the effort of creating a &lt;form&gt; within our Delete confirmation screen?</span></span> <span data-ttu-id="5e392-324">为什么不直接使用标准的超链接链接到操作方法执行实际删除操作？</span><span class="sxs-lookup"><span data-stu-id="5e392-324">Why not just use a standard hyperlink to link to an action method that does the actual delete operation?</span></span> <span data-ttu-id="5e392-325">原因是因为我们想要小心操作以防范 web 爬网程序，搜索引擎发现了 Url 和无意中导致当他们单击链接时要删除的数据。</span><span class="sxs-lookup"><span data-stu-id="5e392-325">The reason is because we want to be careful to guard against web-crawlers and search engines discovering our URLs and inadvertently causing data to be deleted when they follow the links.</span></span> <span data-ttu-id="5e392-326">基于 HTTP GET 的 Url 被视为"安全"才能访问/爬网，并且它们应该遵循 HTTP POST 的。</span><span class="sxs-lookup"><span data-stu-id="5e392-326">HTTP-GET based URLs are considered "safe" for them to access/crawl, and they are supposed to not follow HTTP-POST ones.</span></span> <span data-ttu-id="5e392-327">很好的规则是，请确保您始终将放在破坏性或数据修改操作背后的 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="5e392-327">A good rule is to make sure you always put destructive or data modifying operations behind HTTP-POST requests.</span></span> |

#### <a name="implementing-the-http-post-delete-action-method"></a><span data-ttu-id="5e392-328">实现 HTTP POST Delete 操作方法</span><span class="sxs-lookup"><span data-stu-id="5e392-328">Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="5e392-329">现在，我们实现我们 Delete 操作方法的 HTTP GET 版本显示删除确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="5e392-329">We now have the HTTP-GET version of our Delete action method implemented which displays a delete confirmation screen.</span></span> <span data-ttu-id="5e392-330">当最终用户单击"删除"按钮时它将执行到窗体发布 */Dinners/Dinner / [id]* URL。</span><span class="sxs-lookup"><span data-stu-id="5e392-330">When an end user clicks the "Delete" button it will perform a form post to the */Dinners/Dinner/[id]* URL.</span></span>

<span data-ttu-id="5e392-331">让我们现在实现的 HTTP"POST"行为的 delete 操作方法使用下面的代码：</span><span class="sxs-lookup"><span data-stu-id="5e392-331">Let's now implement the HTTP "POST" behavior of the delete action method using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

<span data-ttu-id="5e392-332">我们删除操作方法的 HTTP POST 版本尝试检索要删除的 dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="5e392-332">The HTTP-POST version of our Delete action method attempts to retrieve the dinner object to delete.</span></span> <span data-ttu-id="5e392-333">如果它找不到它 （因为它已被删除） 将呈现"NotFound"模板。</span><span class="sxs-lookup"><span data-stu-id="5e392-333">If it can't find it (because it has already been deleted) it renders our "NotFound" template.</span></span> <span data-ttu-id="5e392-334">如果找到 Dinner，它可以从 DinnerRepository 删除它。</span><span class="sxs-lookup"><span data-stu-id="5e392-334">If it finds the Dinner, it deletes it from the DinnerRepository.</span></span> <span data-ttu-id="5e392-335">然后，它将呈现"已删除"模板。</span><span class="sxs-lookup"><span data-stu-id="5e392-335">It then renders a "Deleted" template.</span></span>

<span data-ttu-id="5e392-336">若要实现我们将在操作方法中右键单击并选择"添加视图"上下文菜单的"已删除"模板。</span><span class="sxs-lookup"><span data-stu-id="5e392-336">To implement the "Deleted" template we'll right-click in the action method and choose the "Add View" context menu.</span></span> <span data-ttu-id="5e392-337">我们将命名为"已删除"视图，并将它是一个空的模板 （并且不采用强类型化模型对象）。</span><span class="sxs-lookup"><span data-stu-id="5e392-337">We'll name our view "Deleted" and have it be an empty template (and not take a strongly-typed model object).</span></span> <span data-ttu-id="5e392-338">然后，我们将向其中添加一些 HTML 内容：</span><span class="sxs-lookup"><span data-stu-id="5e392-338">We'll then add some HTML content to it:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

<span data-ttu-id="5e392-339">现在，当我们运行我们的应用程序和访问权限和 *"/ Dinners/Delete / [id]"* URL 有效 dinner 对象，它会呈现我们 Dinner 删除确认屏幕类似如下：</span><span class="sxs-lookup"><span data-stu-id="5e392-339">And now when we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it will render our Dinner delete confirmation screen like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

<span data-ttu-id="5e392-340">当我们单击"删除"按钮时它将执行到 HTTP POST */Dinners/Delete / [id]* URL，这将删除 Dinner 从我们的数据库，并显示"已删除"视图模板：</span><span class="sxs-lookup"><span data-stu-id="5e392-340">When we click the "Delete" button it will perform an HTTP-POST to the */Dinners/Delete/[id]* URL, which will delete the Dinner from our database, and display our "Deleted" view template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a><span data-ttu-id="5e392-341">模型绑定安全性</span><span class="sxs-lookup"><span data-stu-id="5e392-341">Model Binding Security</span></span>

<span data-ttu-id="5e392-342">我们已经讨论了两种不同方式使用内置的 ASP.NET MVC 模型绑定功能。</span><span class="sxs-lookup"><span data-stu-id="5e392-342">We've discussed two different ways to use the built-in model-binding features of ASP.NET MVC.</span></span> <span data-ttu-id="5e392-343">首先使用 UpdateModel() 方法来更新现有的模型对象，属性和第二个使用对作为操作方法参数传递中的模型对象的 ASP.NET MVC 支持。</span><span class="sxs-lookup"><span data-stu-id="5e392-343">The first using the UpdateModel() method to update properties on an existing model object, and the second using ASP.NET MVC's support for passing model objects in as action method parameters.</span></span> <span data-ttu-id="5e392-344">这两种方法是非常强大和极其有用。</span><span class="sxs-lookup"><span data-stu-id="5e392-344">Both of these techniques are very powerful and extremely useful.</span></span>

<span data-ttu-id="5e392-345">这种能力还提供了责任。</span><span class="sxs-lookup"><span data-stu-id="5e392-345">This power also brings with it responsibility.</span></span> <span data-ttu-id="5e392-346">很重要的始终是有关安全性的警惕用户如果接受任何用户输入，并且这也是 true 时将对象绑定到窗体输入。</span><span class="sxs-lookup"><span data-stu-id="5e392-346">It is important to always be paranoid about security when accepting any user input, and this is also true when binding objects to form input.</span></span> <span data-ttu-id="5e392-347">应为请注意，始终 HTML 编码以避免 HTML 和 JavaScript 注入攻击，并请注意 SQL 注入式攻击的任何用户输入值 (注意： 我们在我们的应用程序，它会自动将编码参数，防止这些使用 LINQ to SQL类型的攻击）。</span><span class="sxs-lookup"><span data-stu-id="5e392-347">You should be careful to always HTML encode any user-entered values to avoid HTML and JavaScript injection attacks, and be careful of SQL injection attacks (note: we are using LINQ to SQL for our application, which automatically encodes parameters to prevent these types of attacks).</span></span> <span data-ttu-id="5e392-348">永远不应依赖于客户端验证独立的并始终使用服务器端验证，可防止黑客试图向你发送虚假的值来。</span><span class="sxs-lookup"><span data-stu-id="5e392-348">You should never rely on client-side validation alone, and always employ server-side validation to guard against hackers attempting to send you bogus values.</span></span>

<span data-ttu-id="5e392-349">要确保你考虑使用 ASP.NET MVC 的绑定功能时的一个额外的安全项是要绑定的对象的作用域。</span><span class="sxs-lookup"><span data-stu-id="5e392-349">One additional security item to make sure you think about when using the binding features of ASP.NET MVC is the scope of the objects you are binding.</span></span> <span data-ttu-id="5e392-350">具体而言，你想要确保你了解你允许将绑定，并确保只允许那些实际上应为要更新的最终用户可更新的属性的属性的安全隐患。</span><span class="sxs-lookup"><span data-stu-id="5e392-350">Specifically, you want to make sure you understand the security implications of the properties you are allowing to be bound, and make sure you only allow those properties that really should be updatable by an end-user to be updated.</span></span>

<span data-ttu-id="5e392-351">默认情况下，UpdateModel() 方法将尝试更新对模型对象与传入的窗体参数值匹配的所有属性。</span><span class="sxs-lookup"><span data-stu-id="5e392-351">By default, the UpdateModel() method will attempt to update all properties on the model object that match incoming form parameter values.</span></span> <span data-ttu-id="5e392-352">同样，为操作方法参数还默认传递的对象可以具有所有通过窗体参数设置其属性。</span><span class="sxs-lookup"><span data-stu-id="5e392-352">Likewise, objects passed as action method parameters also by default can have all of their properties set via form parameters.</span></span>

#### <a name="locking-down-binding-on-a-per-usage-basis"></a><span data-ttu-id="5e392-353">锁定在每个使用情况的基础上的绑定</span><span class="sxs-lookup"><span data-stu-id="5e392-353">Locking down binding on a per-usage basis</span></span>

<span data-ttu-id="5e392-354">你可以通过提供一个显式"include 列表"的可更新的属性来锁定在每个使用情况的基础上的绑定策略。</span><span class="sxs-lookup"><span data-stu-id="5e392-354">You can lock down the binding policy on a per-usage basis by providing an explicit "include list" of properties that can be updated.</span></span> <span data-ttu-id="5e392-355">这可以通过将额外的字符串数组参数传递给 UpdateModel() 类似方法的下方：</span><span class="sxs-lookup"><span data-stu-id="5e392-355">This can be done by passing an extra string array parameter to the UpdateModel() method like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

<span data-ttu-id="5e392-356">此外为操作方法参数传递的对象支持 [Bind] 属性，它使一个"include 列表"的允许使用属性来指定类似如下：</span><span class="sxs-lookup"><span data-stu-id="5e392-356">Objects passed as action method parameters also support a [Bind] attribute that enables an "include list" of allowed properties to be specified like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a><span data-ttu-id="5e392-357">锁定类型基础上的绑定</span><span class="sxs-lookup"><span data-stu-id="5e392-357">Locking down binding on a type basis</span></span>

<span data-ttu-id="5e392-358">你可以锁定在每种类型的基础上的绑定规则。</span><span class="sxs-lookup"><span data-stu-id="5e392-358">You can also lock down the binding rules on a per-type basis.</span></span> <span data-ttu-id="5e392-359">这允许您一次，指定绑定规则，然后让其在所有控制器和操作方法适合所有情况 （包括 UpdateModel 和操作方法参数方案）。</span><span class="sxs-lookup"><span data-stu-id="5e392-359">This allows you to specify the binding rules once, and then have them apply in all scenarios (including both UpdateModel and action method parameter scenarios) across all controllers and action methods.</span></span>

<span data-ttu-id="5e392-360">通过添加到类型上的 [Bind] 属性或通过注册 （适用于其中的类型不属于你的方案） 的应用程序的 Global.asax 文件中，可以自定义每种类型的绑定规则。</span><span class="sxs-lookup"><span data-stu-id="5e392-360">You can customize the per-type binding rules by adding a [Bind] attribute onto a type, or by registering it within the Global.asax file of the application (useful for scenarios where you don't own the type).</span></span> <span data-ttu-id="5e392-361">然后，可以使用的绑定属性的 Include 和 Exclude 属性来控制哪些属性是可绑定为特定类或接口。</span><span class="sxs-lookup"><span data-stu-id="5e392-361">You can then use the Bind attribute's Include and Exclude properties to control which properties are bindable for the particular class or interface.</span></span>

<span data-ttu-id="5e392-362">我们将 Dinner 类在 NerdDinner 应用程序中，使用这种方法，并将 [Bind] 属性添加到它的可绑定属性的列表限制到以下：</span><span class="sxs-lookup"><span data-stu-id="5e392-362">We'll use this technique for the Dinner class in our NerdDinner application, and add a [Bind] attribute to it that restricts the list of bindable properties to the following:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

<span data-ttu-id="5e392-363">请注意，我们不允许 Rsvp 集合操作通过绑定，也不我们允许 DinnerID 或 HostedBy 属性通过绑定设置。</span><span class="sxs-lookup"><span data-stu-id="5e392-363">Notice we are not allowing the RSVPs collection to be manipulated via binding, nor are we allowing the DinnerID or HostedBy properties to be set via binding.</span></span> <span data-ttu-id="5e392-364">出于安全原因我们将改为仅控制这些特定属性使用在我们的操作方法中的显式代码。</span><span class="sxs-lookup"><span data-stu-id="5e392-364">For security reasons we'll instead only manipulate these particular properties using explicit code within our action methods.</span></span>

### <a name="crud-wrap-up"></a><span data-ttu-id="5e392-365">CRUD 总结</span><span class="sxs-lookup"><span data-stu-id="5e392-365">CRUD Wrap-Up</span></span>

<span data-ttu-id="5e392-366">ASP.NET MVC 包括大量内置功能，帮助实现窗体发布方案。</span><span class="sxs-lookup"><span data-stu-id="5e392-366">ASP.NET MVC includes a number of built-in features that help with implementing form posting scenarios.</span></span> <span data-ttu-id="5e392-367">我们使用了各种各样的这些功能在我们 DinnerRepository 之上提供 CRUD UI 支持。</span><span class="sxs-lookup"><span data-stu-id="5e392-367">We used a variety of these features to provide CRUD UI support on top of our DinnerRepository.</span></span>

<span data-ttu-id="5e392-368">我们使用的专注于模型的方法来实现我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5e392-368">We are using a model-focused approach to implement our application.</span></span> <span data-ttu-id="5e392-369">这意味着，我们所有的验证和业务规则中我们的模型层 – 而不是在我们的控制器或视图定义逻辑。</span><span class="sxs-lookup"><span data-stu-id="5e392-369">This means that all our validation and business rule logic is defined within our model layer – and not within our controllers or views.</span></span> <span data-ttu-id="5e392-370">我们的控制器类和我们的视图模板都不知道我们 Dinner model 类通过强制实施的特定业务规则有关的任何信息。</span><span class="sxs-lookup"><span data-stu-id="5e392-370">Neither our Controller class nor our View templates know anything about the specific business rules being enforced by our Dinner model class.</span></span>

<span data-ttu-id="5e392-371">这将使我们的应用程序体系结构保持干净，并使其更易于测试。</span><span class="sxs-lookup"><span data-stu-id="5e392-371">This will keep our application architecture clean and make it easier to test.</span></span> <span data-ttu-id="5e392-372">我们可以将更多的业务规则在将来添加到我们的模型层和*无需进行任何代码更改*到我们的控制器或视图以使其支持。</span><span class="sxs-lookup"><span data-stu-id="5e392-372">We can add additional business rules to our model layer in the future and *not have to make any code changes* to our Controller or View in order for them to be supported.</span></span> <span data-ttu-id="5e392-373">这将向我们提供了大量的改进和更改在将来，我们的应用程序的灵活性。</span><span class="sxs-lookup"><span data-stu-id="5e392-373">This is going to provide us with a great deal of agility to evolve and change our application in the future.</span></span>

<span data-ttu-id="5e392-374">我们 DinnersController 现在使 Dinner 列表/详细信息，以及创建、 编辑和删除支持。</span><span class="sxs-lookup"><span data-stu-id="5e392-374">Our DinnersController now enables Dinner listings/details, as well as create, edit and delete support.</span></span> <span data-ttu-id="5e392-375">类的完整代码可在下文：</span><span class="sxs-lookup"><span data-stu-id="5e392-375">The complete code for the class can be found below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a><span data-ttu-id="5e392-376">下一步</span><span class="sxs-lookup"><span data-stu-id="5e392-376">Next Step</span></span>

<span data-ttu-id="5e392-377">现在，我们有我们 DinnersController 类中实现的基本 CRUD （创建、 读取、 更新和删除） 支持。</span><span class="sxs-lookup"><span data-stu-id="5e392-377">We now have basic CRUD (Create, Read, Update and Delete) support implement within our DinnersController class.</span></span>

<span data-ttu-id="5e392-378">让我们现在看一下如何使用 ViewData 和 ViewModel 类要在窗体上启用更丰富的 UI。</span><span class="sxs-lookup"><span data-stu-id="5e392-378">Let's now look at how we can use ViewData and ViewModel classes to enable even richer UI on our forms.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5e392-379">[上一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [下一页](use-viewdata-and-implement-viewmodel-classes.md)</span><span class="sxs-lookup"><span data-stu-id="5e392-379">[Previous](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
[Next](use-viewdata-and-implement-viewmodel-classes.md)</span></span>
