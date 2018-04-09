---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 提供 CRUD （创建、 读取、 更新、 删除） 数据窗体条目支持 |Microsoft 文档
author: microsoft
description: 第 5 步演示如何通过启用用于编辑、 创建和删除晚餐也为它的支持，让我们进一步 DinnersController 类。
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: bd906282db5c620476966ffbe09cecb5ade66ee4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="provide-crud-create-read-update-delete-data-form-entry-support"></a><span data-ttu-id="9dd53-103">提供 CRUD （创建、 读取、 更新、 删除） 数据窗体条目支持</span><span class="sxs-lookup"><span data-stu-id="9dd53-103">Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support</span></span>
====================
<span data-ttu-id="9dd53-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9dd53-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="9dd53-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="9dd53-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="9dd53-106">这是一个免费的步骤 5 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，查找步程取如何生成一个较小，但完成，使用 ASP.NET MVC 1 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9dd53-106">This is step 5 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="9dd53-107">第 5 步演示如何通过启用用于编辑、 创建和删除晚餐也为它的支持，让我们进一步 DinnersController 类。</span><span class="sxs-lookup"><span data-stu-id="9dd53-107">Step 5 shows how to take our DinnersController class further by enable support for editing, creating and deleting Dinners with it as well.</span></span>
> 
> <span data-ttu-id="9dd53-108">如果你使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="9dd53-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a><span data-ttu-id="9dd53-109">NerdDinner 步骤 5： 创建、 更新、 删除窗体方案</span><span class="sxs-lookup"><span data-stu-id="9dd53-109">NerdDinner Step 5: Create, Update, Delete Form Scenarios</span></span>

<span data-ttu-id="9dd53-110">我们已引入控制器和视图，并介绍如何使用它们来在站点上实现晚餐的详细信息列表/体验。</span><span class="sxs-lookup"><span data-stu-id="9dd53-110">We've introduced controllers and views, and covered how to use them to implement a listing/details experience for Dinners on site.</span></span> <span data-ttu-id="9dd53-111">我们的下一步将是采取进一步的我们 DinnersController 类和启用用于编辑、 创建和删除晚餐也为它的支持。</span><span class="sxs-lookup"><span data-stu-id="9dd53-111">Our next step will be to take our DinnersController class further and enable support for editing, creating and deleting Dinners with it as well.</span></span>

### <a name="urls-handled-by-dinnerscontroller"></a><span data-ttu-id="9dd53-112">Url 由 DinnersController 处理</span><span class="sxs-lookup"><span data-stu-id="9dd53-112">URLs handled by DinnersController</span></span>

<span data-ttu-id="9dd53-113">我们之前添加到实现支持两个 Url 的 DinnersController 的操作方法： */Dinners*和*/Dinners/详细信息 / [id]*。</span><span class="sxs-lookup"><span data-stu-id="9dd53-113">We previously added action methods to DinnersController that implemented support for two URLs: */Dinners* and */Dinners/Details/[id]*.</span></span>

| <span data-ttu-id="9dd53-114">**URL**</span><span class="sxs-lookup"><span data-stu-id="9dd53-114">**URL**</span></span> | <span data-ttu-id="9dd53-115">**VERB**</span><span class="sxs-lookup"><span data-stu-id="9dd53-115">**VERB**</span></span> | <span data-ttu-id="9dd53-116">**目的**</span><span class="sxs-lookup"><span data-stu-id="9dd53-116">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9dd53-117">*/Dinners/*</span><span class="sxs-lookup"><span data-stu-id="9dd53-117">*/Dinners/*</span></span> | <span data-ttu-id="9dd53-118">GET</span><span class="sxs-lookup"><span data-stu-id="9dd53-118">GET</span></span> | <span data-ttu-id="9dd53-119">显示即将到来的晚餐 HTML 列表。</span><span class="sxs-lookup"><span data-stu-id="9dd53-119">Display an HTML list of upcoming dinners.</span></span> |
| <span data-ttu-id="9dd53-120">*/Dinners/Details/[id]*</span><span class="sxs-lookup"><span data-stu-id="9dd53-120">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="9dd53-121">GET</span><span class="sxs-lookup"><span data-stu-id="9dd53-121">GET</span></span> | <span data-ttu-id="9dd53-122">显示有关特定 dinner 详细信息。</span><span class="sxs-lookup"><span data-stu-id="9dd53-122">Display details about a specific dinner.</span></span> |

<span data-ttu-id="9dd53-123">我们现在将操作方法来实现三个其他 Url: <em>/Dinners/编辑 / [id]、 / 晚餐/创建、</em>和<em>/Dinners/删除 / [id]</em>。</span><span class="sxs-lookup"><span data-stu-id="9dd53-123">We will now add action methods to implement three additional URLs: <em>/Dinners/Edit/[id], /Dinners/Create,</em>and<em>/Dinners/Delete/[id]</em>.</span></span> <span data-ttu-id="9dd53-124">这些 Url 将启用对编辑现有晚餐，创建新晚餐和删除晚餐支持。</span><span class="sxs-lookup"><span data-stu-id="9dd53-124">These URLs will enable support for editing existing Dinners, creating new Dinners, and deleting Dinners.</span></span>

<span data-ttu-id="9dd53-125">我们将支持使用这些新的 Url 的 HTTP GET 和 HTTP POST 谓词交互。</span><span class="sxs-lookup"><span data-stu-id="9dd53-125">We will support both HTTP GET and HTTP POST verb interactions with these new URLs.</span></span> <span data-ttu-id="9dd53-126">HTTP GET 请求到这些 Url 将显示数据 （使用在"编辑"的情况下的 Dinner 数据填充窗体，在"创建"的情况下的空白窗体和删除确认屏幕中，在"删除"的情况下） 的初始 HTML 视图。</span><span class="sxs-lookup"><span data-stu-id="9dd53-126">HTTP GET requests to these URLs will display the initial HTML view of the data (a form populated with the Dinner data in the case of "edit", a blank form in the case of "create", and a delete confirmation screen in the case of "delete").</span></span> <span data-ttu-id="9dd53-127">对这些 Url 的 HTTP POST 请求将保存/更新/删除 Dinner 数据中我们 DinnerRepository （和从那里到数据库）。</span><span class="sxs-lookup"><span data-stu-id="9dd53-127">HTTP POST requests to these URLs will save/update/delete the Dinner data in our DinnerRepository (and from there to the database).</span></span>

| <span data-ttu-id="9dd53-128">**URL**</span><span class="sxs-lookup"><span data-stu-id="9dd53-128">**URL**</span></span> | <span data-ttu-id="9dd53-129">**VERB**</span><span class="sxs-lookup"><span data-stu-id="9dd53-129">**VERB**</span></span> | <span data-ttu-id="9dd53-130">**目的**</span><span class="sxs-lookup"><span data-stu-id="9dd53-130">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9dd53-131">*/Dinners/Edit/[id]*</span><span class="sxs-lookup"><span data-stu-id="9dd53-131">*/Dinners/Edit/[id]*</span></span> | <span data-ttu-id="9dd53-132">GET</span><span class="sxs-lookup"><span data-stu-id="9dd53-132">GET</span></span> | <span data-ttu-id="9dd53-133">显示可编辑 HTML 窗体使用 Dinner 数据进行填充。</span><span class="sxs-lookup"><span data-stu-id="9dd53-133">Display an editable HTML form populated with Dinner data.</span></span> |
| <span data-ttu-id="9dd53-134">发布</span><span class="sxs-lookup"><span data-stu-id="9dd53-134">POST</span></span> | <span data-ttu-id="9dd53-135">将窗体更改保存到数据库特定 Dinner 为。</span><span class="sxs-lookup"><span data-stu-id="9dd53-135">Save the form changes for a particular Dinner to the database.</span></span> |
| <span data-ttu-id="9dd53-136">*/Dinners/Create*</span><span class="sxs-lookup"><span data-stu-id="9dd53-136">*/Dinners/Create*</span></span> | <span data-ttu-id="9dd53-137">GET</span><span class="sxs-lookup"><span data-stu-id="9dd53-137">GET</span></span> | <span data-ttu-id="9dd53-138">显示允许用户定义新晚餐空 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="9dd53-138">Display an empty HTML form that allows users to define new Dinners.</span></span> |
| <span data-ttu-id="9dd53-139">发布</span><span class="sxs-lookup"><span data-stu-id="9dd53-139">POST</span></span> | <span data-ttu-id="9dd53-140">创建新的 Dinner 并将其保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="9dd53-140">Create a new Dinner and save it in the database.</span></span> |
| <span data-ttu-id="9dd53-141">*/Dinners/Delete/[id]*</span><span class="sxs-lookup"><span data-stu-id="9dd53-141">*/Dinners/Delete/[id]*</span></span> | <span data-ttu-id="9dd53-142">GET</span><span class="sxs-lookup"><span data-stu-id="9dd53-142">GET</span></span> | <span data-ttu-id="9dd53-143">显示删除确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="9dd53-143">Display delete confirmation screen.</span></span> |
| <span data-ttu-id="9dd53-144">发布</span><span class="sxs-lookup"><span data-stu-id="9dd53-144">POST</span></span> | <span data-ttu-id="9dd53-145">从数据库中删除指定的 dinner。</span><span class="sxs-lookup"><span data-stu-id="9dd53-145">Deletes the specified dinner from the database.</span></span> |

### <a name="edit-support"></a><span data-ttu-id="9dd53-146">编辑支持</span><span class="sxs-lookup"><span data-stu-id="9dd53-146">Edit Support</span></span>

<span data-ttu-id="9dd53-147">让我们首先将实现"编辑"方案。</span><span class="sxs-lookup"><span data-stu-id="9dd53-147">Let's begin by implementing the "edit" scenario.</span></span>

#### <a name="the-http-get-edit-action-method"></a><span data-ttu-id="9dd53-148">HTTP GET 编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="9dd53-148">The HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="9dd53-149">我们将开始通过实现我们编辑操作方法的 HTTP"GET"行为。</span><span class="sxs-lookup"><span data-stu-id="9dd53-149">We'll start by implementing the HTTP "GET" behavior of our edit action method.</span></span> <span data-ttu-id="9dd53-150">此方法将调用时*/Dinners/编辑 / [id]*请求 URL。</span><span class="sxs-lookup"><span data-stu-id="9dd53-150">This method will be invoked when the */Dinners/Edit/[id]* URL is requested.</span></span> <span data-ttu-id="9dd53-151">我们实现将如下所示：</span><span class="sxs-lookup"><span data-stu-id="9dd53-151">Our implementation will look like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

<span data-ttu-id="9dd53-152">上面的代码使用 DinnerRepository 检索 Dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="9dd53-152">The code above uses the DinnerRepository to retrieve a Dinner object.</span></span> <span data-ttu-id="9dd53-153">它随后将呈现使用 Dinner 对象的视图模板。</span><span class="sxs-lookup"><span data-stu-id="9dd53-153">It then renders a View template using the Dinner object.</span></span> <span data-ttu-id="9dd53-154">因为我们尚未显式传递到的模板名称*View()*帮助器方法，它将使用基于约定的默认路径来解析视图模板： /Views/Dinners/Edit.aspx。</span><span class="sxs-lookup"><span data-stu-id="9dd53-154">Because we haven't explicitly passed a template name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Edit.aspx.</span></span>

<span data-ttu-id="9dd53-155">让我们现在创建此视图模板。</span><span class="sxs-lookup"><span data-stu-id="9dd53-155">Let's now create this view template.</span></span> <span data-ttu-id="9dd53-156">我们将编辑方法内右键单击并选择"添加视图"上下文菜单命令来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="9dd53-156">We will do this by right-clicking within the Edit method and selecting the "Add View" context menu command:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

<span data-ttu-id="9dd53-157">在"添加视图"对话框中，我们将指示我们 Dinner 对象传递给其模型中，我们查看模板和选择自动基架"编辑"的模板：</span><span class="sxs-lookup"><span data-stu-id="9dd53-157">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to auto-scaffold an "Edit" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

<span data-ttu-id="9dd53-158">当我们单击"添加"按钮时，Visual Studio 将在"\Views\Dinners"目录中为我们添加新的"Edit.aspx"视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="9dd53-158">When we click the "Add" button, Visual Studio will add a new "Edit.aspx" view template file for us within the "\Views\Dinners" directory.</span></span> <span data-ttu-id="9dd53-159">它还将打开代码编辑器 – 使用初始"编辑"基架实现类似下面填充内部的新"Edit.aspx"视图模板：</span><span class="sxs-lookup"><span data-stu-id="9dd53-159">It will also open up the new "Edit.aspx" view template within the code-editor – populated with an initial "Edit" scaffold implementation like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

<span data-ttu-id="9dd53-160">让我们进行到默认"的编辑"基架生成，一些更改，并将编辑视图模板更新为具有下列内容 （这将删除几个我们不需要公开的属性）：</span><span class="sxs-lookup"><span data-stu-id="9dd53-160">Let's make a few changes to the default "edit" scaffold generated, and update the edit view template to have the content below (which removes a few of the properties we don't want to expose):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

<span data-ttu-id="9dd53-161">当我们运行的应用程序和请求*"/ 晚餐/编辑/1"*我们将看到以下页面的 URL:</span><span class="sxs-lookup"><span data-stu-id="9dd53-161">When we run the application and request the *"/Dinners/Edit/1"* URL we will see the following page:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

<span data-ttu-id="9dd53-162">由我们视图生成的 HTML 标记类似于下面。</span><span class="sxs-lookup"><span data-stu-id="9dd53-162">The HTML markup generated by our view looks like below.</span></span> <span data-ttu-id="9dd53-163">这一点与标准 HTML –&lt;窗体&gt;执行到 HTTP POST 的元素*/Dinners/Edit/1* URL 时"保存"&lt;输入类型 ="提交"/&gt;推送按钮。</span><span class="sxs-lookup"><span data-stu-id="9dd53-163">It is standard HTML – with a &lt;form&gt; element that performs an HTTP POST to the */Dinners/Edit/1* URL when the "Save" &lt;input type="submit"/&gt; button is pushed.</span></span> <span data-ttu-id="9dd53-164">对 HTML&lt;输入类型 ="text"/&gt;元素已被为每个可编辑属性的输出：</span><span class="sxs-lookup"><span data-stu-id="9dd53-164">A HTML &lt;input type="text"/&gt; element has been output for each editable property:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a><span data-ttu-id="9dd53-165">Html.BeginForm() 和 Html.TextBox() Html 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="9dd53-165">Html.BeginForm() and Html.TextBox() Html Helper Methods</span></span>

<span data-ttu-id="9dd53-166">我们"Edit.aspx"视图模板正在使用的一些"Html 帮助程序"方法： Html.ValidationSummary()、 Html.BeginForm()、 Html.TextBox() 和 Html.ValidationMessage()。</span><span class="sxs-lookup"><span data-stu-id="9dd53-166">Our "Edit.aspx" view template is using several "Html Helper" methods: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), and Html.ValidationMessage().</span></span> <span data-ttu-id="9dd53-167">除了为我们的 HTML 标记生成，这些帮助器方法提供了内置的错误处理和验证支持。</span><span class="sxs-lookup"><span data-stu-id="9dd53-167">In addition to generating HTML markup for us, these helper methods provide built-in error handling and validation support.</span></span>

##### <a name="htmlbeginform-helper-method"></a><span data-ttu-id="9dd53-168">Html.BeginForm() 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="9dd53-168">Html.BeginForm() helper method</span></span>

<span data-ttu-id="9dd53-169">Html.BeginForm() 帮助程序方法是 HTML 输出内容是什么&lt;窗体&gt;我们标记中的元素。</span><span class="sxs-lookup"><span data-stu-id="9dd53-169">The Html.BeginForm() helper method is what output the HTML &lt;form&gt; element in our markup.</span></span> <span data-ttu-id="9dd53-170">我们 Edit.aspx 视图模板中你将注意到，我们要将应用的 C#"using"语句时使用此方法。</span><span class="sxs-lookup"><span data-stu-id="9dd53-170">In our Edit.aspx view template you'll notice that we are applying a C# "using" statement when using this method.</span></span> <span data-ttu-id="9dd53-171">左大括号指示的开头&lt;窗体&gt;内容和右大括号是什么指示的末尾&lt;窗体窗体&gt;元素：</span><span class="sxs-lookup"><span data-stu-id="9dd53-171">The open curly brace indicates the beginning of the &lt;form&gt; content, and the closing curly brace is what indicates the end of the &lt;/form&gt; element:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

<span data-ttu-id="9dd53-172">或者，如果你发现的"using"语句接近自然如下方案，你可以使用 Html.BeginForm() 和 Html.EndForm() 组合 （后者执行相同的操作）：</span><span class="sxs-lookup"><span data-stu-id="9dd53-172">Alternatively, if you find the "using" statement approach unnatural for a scenario like this, you can use a Html.BeginForm() and Html.EndForm() combination (which does the same thing):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

<span data-ttu-id="9dd53-173">不带任何参数调用 Html.BeginForm() 将导致输出对当前请求的 URL 执行 HTTP POST 的窗体元素。</span><span class="sxs-lookup"><span data-stu-id="9dd53-173">Calling Html.BeginForm() without any parameters will cause it to output a form element that does an HTTP-POST to the current request's URL.</span></span> <span data-ttu-id="9dd53-174">它是为何我们编辑视图生成*&lt;形成操作 ="/ 晚餐/编辑/1"方法 ="post"&gt;* 元素。</span><span class="sxs-lookup"><span data-stu-id="9dd53-174">That is why our Edit view generates a *&lt;form action="/Dinners/Edit/1" method="post"&gt;* element.</span></span> <span data-ttu-id="9dd53-175">我们无法具有或者传递显式参数给 Html.BeginForm() 如果我们想要发布到另一个 URL。</span><span class="sxs-lookup"><span data-stu-id="9dd53-175">We could have alternatively passed explicit parameters to Html.BeginForm() if we wanted to post to a different URL.</span></span>

##### <a name="htmltextbox-helper-method"></a><span data-ttu-id="9dd53-176">Html.TextBox() 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="9dd53-176">Html.TextBox() helper method</span></span>

<span data-ttu-id="9dd53-177">我们 Edit.aspx 视图使用 Html.TextBox() 帮助器方法来输出&lt;输入类型 ="text"/&gt;元素：</span><span class="sxs-lookup"><span data-stu-id="9dd53-177">Our Edit.aspx view uses the Html.TextBox() helper method to output &lt;input type="text"/&gt; elements:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

<span data-ttu-id="9dd53-178">上面的 Html.TextBox() 方法将采用的单个参数 – 正在使用指定的 id/名称属性&lt;输入类型 ="text"/&gt;到输出，以及要导入从文本框中的值的模型属性的元素。</span><span class="sxs-lookup"><span data-stu-id="9dd53-178">The Html.TextBox() method above takes a single parameter – which is being used to specify both the id/name attributes of the &lt;input type="text"/&gt; element to output, as well as the model property to populate the textbox value from.</span></span> <span data-ttu-id="9dd53-179">例如，我们传递到编辑视图的 Dinner 对象有".NET Future"，"Title"属性值，因此我们 Html.TextBox("Title") 方法调用输出： *&lt;输入的 id ="Title"名称 ="Title"type ="text"value =".NET Future"/&gt;*.</span><span class="sxs-lookup"><span data-stu-id="9dd53-179">For example, the Dinner object we passed to the Edit view had a "Title" property value of ".NET Futures", and so our Html.TextBox("Title") method call output: *&lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.</span></span>

<span data-ttu-id="9dd53-180">或者，我们可以使用第一个 Html.TextBox() 参数来指定 id/名称的元素，然后显式将传递中要用作第二个参数的值：</span><span class="sxs-lookup"><span data-stu-id="9dd53-180">Alternatively, we can use the first Html.TextBox() parameter to specify the id/name of the element, and then explicitly pass in the value to use as a second parameter:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

<span data-ttu-id="9dd53-181">通常，我们将需要执行的输出值的自定义格式设置。</span><span class="sxs-lookup"><span data-stu-id="9dd53-181">Often we'll want to perform custom formatting on the value that is output.</span></span> <span data-ttu-id="9dd53-182">内置于.NET string.format （) 静态方法可用于这些方案。</span><span class="sxs-lookup"><span data-stu-id="9dd53-182">The String.Format() static method built-into .NET is useful for these scenarios.</span></span> <span data-ttu-id="9dd53-183">我们 Edit.aspx 视图模板使用此设置的格式 EventDate 值 （这是类型为 DateTime 的），因此它不会显示时间 （秒）：</span><span class="sxs-lookup"><span data-stu-id="9dd53-183">Our Edit.aspx view template is using this to format the EventDate value (which is of type DateTime) so that it doesn't show seconds for the time:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

<span data-ttu-id="9dd53-184">Html.TextBox() 的第三个参数 （可选） 可用来输出 HTML 的其他属性。</span><span class="sxs-lookup"><span data-stu-id="9dd53-184">A third parameter to Html.TextBox() can optionally be used to output additional HTML attributes.</span></span> <span data-ttu-id="9dd53-185">的以下代码段演示如何呈现其他大小 ="30"的属性和类 ="mycssclass"属性上&lt;输入类型 ="text"/&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="9dd53-185">The code-snippet below demonstrates how to render an additional size="30" attribute and a class="mycssclass" attribute on the &lt;input type="text"/&gt; element.</span></span> <span data-ttu-id="9dd53-186">请注意，我们如何转义的类属性使用名称"@" character because "类"是保留的关键字在 C# 中：</span><span class="sxs-lookup"><span data-stu-id="9dd53-186">Note how we are escaping the name of the class attribute using a "@" character because "class" is a reserved keyword in C#:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a><span data-ttu-id="9dd53-187">实现 HTTP POST 编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="9dd53-187">Implementing the HTTP-POST Edit Action Method</span></span>

<span data-ttu-id="9dd53-188">我们现在有了我们的编辑操作方法中实现的 HTTP GET 版本。</span><span class="sxs-lookup"><span data-stu-id="9dd53-188">We now have the HTTP-GET version of our Edit action method implemented.</span></span> <span data-ttu-id="9dd53-189">当用户请求*/Dinners/Edit/1*它们接收 HTML 页如下所示的 URL:</span><span class="sxs-lookup"><span data-stu-id="9dd53-189">When a user requests the */Dinners/Edit/1* URL they receive an HTML page like the following:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

<span data-ttu-id="9dd53-190">按"保存"按钮会导致窗体发送到*/Dinners/Edit/1* URL，并在提交 HTML&lt;输入&gt;窗体中使用 HTTP POST 谓词的值。</span><span class="sxs-lookup"><span data-stu-id="9dd53-190">Pressing the "Save" button causes a form post to the */Dinners/Edit/1* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span> <span data-ttu-id="9dd53-191">让我们现在实现我们编辑操作方法 – 它将处理保存 Dinner 的 HTTP POST 行为。</span><span class="sxs-lookup"><span data-stu-id="9dd53-191">Let's now implement the HTTP POST behavior of our edit action method – which will handle saving the Dinner.</span></span>

<span data-ttu-id="9dd53-192">我们将首先通过将重载"的编辑"操作方法添加到对其具有"AcceptVerbs"属性，该值指示它将处理 HTTP POST 方案我们 DinnersController:</span><span class="sxs-lookup"><span data-stu-id="9dd53-192">We'll begin by adding an overloaded "Edit" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

<span data-ttu-id="9dd53-193">当 [AcceptVerbs] 特性应用于重载的操作方法中时，ASP.NET MVC 将自动处理调度到适当的操作方法，具体取决于传入的 HTTP 谓词的请求。</span><span class="sxs-lookup"><span data-stu-id="9dd53-193">When the [AcceptVerbs] attribute is applied to overloaded action methods, ASP.NET MVC automatically handles dispatching requests to the appropriate action method depending on the incoming HTTP verb.</span></span> <span data-ttu-id="9dd53-194">HTTP POST 请求到<em>/Dinners/编辑 / [id]</em> Url 将转到上述的编辑方法，对所有其他 HTTP 谓词请求时<em>/Dinners/编辑 / [id]</em>Url 将转到第一个的编辑方法我们实现 （其未不具有 [AcceptVerbs] 属性）。</span><span class="sxs-lookup"><span data-stu-id="9dd53-194">HTTP POST requests to <em>/Dinners/Edit/[id]</em> URLs will go to the above Edit method, while all other HTTP verb requests to <em>/Dinners/Edit/[id]</em>URLs will go to the first Edit method we implemented (which did not have an [AcceptVerbs] attribute).</span></span>

| <span data-ttu-id="9dd53-195">**通过 HTTP 谓词为什么区分端主题内容:？**</span><span class="sxs-lookup"><span data-stu-id="9dd53-195">**Side Topic: Why differentiate via HTTP verbs?**</span></span> |
| --- |
| <span data-ttu-id="9dd53-196">您可能会问 – 为何我们使用单一 URL 和区分的 HTTP 谓词通过其行为？</span><span class="sxs-lookup"><span data-stu-id="9dd53-196">You might ask – why are we using a single URL and differentiating its behavior via the HTTP verb?</span></span> <span data-ttu-id="9dd53-197">为何不让两个单独的 Url 来处理加载和保存编辑的更改？</span><span class="sxs-lookup"><span data-stu-id="9dd53-197">Why not just have two separate URLs to handle loading and saving edit changes?</span></span> <span data-ttu-id="9dd53-198">例如： /Dinners/编辑 / [id] 以显示初始窗体和 /Dinners/保存 / [id] 来处理窗体发布请求，以将其保存？</span><span class="sxs-lookup"><span data-stu-id="9dd53-198">For example: /Dinners/Edit/[id] to display the initial form and /Dinners/Save/[id] to handle the form post to save it?</span></span> <span data-ttu-id="9dd53-199">与发布的两个单独 Url 的缺点是在其中我们发布到 /Dinners/Save/2，，然后需要重新 HTML 窗体显示由于输入错误的情况下，最终的最终用户将得到 （因为这是在其浏览器的地址栏中具有晚餐/保存/2 URLURL 发布到窗体)。</span><span class="sxs-lookup"><span data-stu-id="9dd53-199">The downside with publishing two separate URLs is that in cases where we post to /Dinners/Save/2, and then need to redisplay the HTML form because of an input error, the end-user will end up having the /Dinners/Save/2 URL in their browser's address bar (since that was the URL the form posted to).</span></span> <span data-ttu-id="9dd53-200">如果最终用户创建一个书签，本页 redisplayed 到其浏览器收藏夹列表中，或复制/粘贴 URL 和电子邮件将其发送给友元，它们将结束保存将不起作用将来 （因为该 URL 取决于发送值） 的 URL。</span><span class="sxs-lookup"><span data-stu-id="9dd53-200">If the end-user bookmarks this redisplayed page to their browser favorites list, or copy/pastes the URL and emails it to a friend, they will end up saving a URL that won't work in the future (since that URL depends on post values).</span></span> <span data-ttu-id="9dd53-201">通过公开单一 URL (例如： /Dinners/Edit/[id]) 并且区分处理它的 HTTP 谓词，则可以为最终用户若要编辑页面加入书签和/或将 URL 发送给他人安全。</span><span class="sxs-lookup"><span data-stu-id="9dd53-201">By exposing a single URL (like: /Dinners/Edit/[id]) and differentiating the processing of it by HTTP verb, it is safe for end-users to bookmark the edit page and/or send the URL to others.</span></span> |

#### <a name="retrieving-form-post-values"></a><span data-ttu-id="9dd53-202">检索窗体发送值</span><span class="sxs-lookup"><span data-stu-id="9dd53-202">Retrieving Form Post Values</span></span>

<span data-ttu-id="9dd53-203">有多种方式我们就可以访问发布窗体中"的编辑"我们 HTTP POST 方法的参数。</span><span class="sxs-lookup"><span data-stu-id="9dd53-203">There are a variety of ways we can access posted form parameters within our HTTP POST "Edit" method.</span></span> <span data-ttu-id="9dd53-204">一个简单方法是只使用控制器基类上请求属性来访问窗体集合和直接检索已发布的值：</span><span class="sxs-lookup"><span data-stu-id="9dd53-204">One simple approach is to just use the Request property on the Controller base class to access the form collection and retrieve the posted values directly:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

<span data-ttu-id="9dd53-205">上面的方法是稍有详细信息; 不过，尤其是一旦我们添加错误处理逻辑。</span><span class="sxs-lookup"><span data-stu-id="9dd53-205">The above approach is a little verbose, though, especially once we add error handling logic.</span></span>

<span data-ttu-id="9dd53-206">一个更好的方法的这种情况下是利用内置*UpdateModel()*控制器基类上的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="9dd53-206">A better approach for this scenario is to leverage the built-in *UpdateModel()* helper method on the Controller base class.</span></span> <span data-ttu-id="9dd53-207">它支持更新我们将它使用传入的窗体参数传递的对象的属性。</span><span class="sxs-lookup"><span data-stu-id="9dd53-207">It supports updating the properties of an object we pass it using the incoming form parameters.</span></span> <span data-ttu-id="9dd53-208">它使用反射来确定对象的属性名称然后自动将转换并向其客户端提交的输入值为基础的分配值。</span><span class="sxs-lookup"><span data-stu-id="9dd53-208">It uses reflection to determine the property names on the object, and then automatically converts and assigns values to them based on the input values submitted by the client.</span></span>

<span data-ttu-id="9dd53-209">我们无法使用 UpdateModel() 方法来简化使用此代码我们 HTTP POST 编辑操作：</span><span class="sxs-lookup"><span data-stu-id="9dd53-209">We could use the UpdateModel() method to simplify our HTTP-POST Edit Action using this code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

<span data-ttu-id="9dd53-210">我们现在可以访问*/Dinners/Edit/1* URL，以及更改我们 Dinner 标题：</span><span class="sxs-lookup"><span data-stu-id="9dd53-210">We can now visit the */Dinners/Edit/1* URL, and change the title of our Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

<span data-ttu-id="9dd53-211">当我们单击"保存"按钮时，我们使用以下方法将执行窗体发布到我们的编辑操作，并更新后的值将保留在数据库中。</span><span class="sxs-lookup"><span data-stu-id="9dd53-211">When we click the "Save" button, we'll perform a form post to our Edit action, and the updated values will be persisted in the database.</span></span> <span data-ttu-id="9dd53-212">我们将然后重定向到详细信息 URL 为 Dinner （这将显示新保存的值）：</span><span class="sxs-lookup"><span data-stu-id="9dd53-212">We will then be redirected to the Details URL for the Dinner (which will display the newly saved values):</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a><span data-ttu-id="9dd53-213">处理编辑错误</span><span class="sxs-lookup"><span data-stu-id="9dd53-213">Handling Edit Errors</span></span>

<span data-ttu-id="9dd53-214">我们当前的 HTTP POST 实现能够正常微调 – 除非有错误。</span><span class="sxs-lookup"><span data-stu-id="9dd53-214">Our current HTTP-POST implementation works fine – except when there are errors.</span></span>

<span data-ttu-id="9dd53-215">当用户进行编辑窗体的一个错误时，我们需要确保窗体将重新显示使用的将引导他们修复此错误的详细的错误消息。</span><span class="sxs-lookup"><span data-stu-id="9dd53-215">When a user makes a mistake editing a form, we need to make sure that the form is redisplayed with an informative error message that guides them to fix it.</span></span> <span data-ttu-id="9dd53-216">这包括最终用户，并且其中文章不正确的输入的情况下 (例如： 的格式不正确的日期字符串)，如以及情况的输入的格式是否有效，但没有业务规则冲突。</span><span class="sxs-lookup"><span data-stu-id="9dd53-216">This includes cases where an end-user posts incorrect input (for example: a malformed date string), as well as cases where the input format is valid but there is a business rule violation.</span></span> <span data-ttu-id="9dd53-217">如果出现错误窗体应保留输入的数据最初输入，以便他们不需要手动重填其更改的用户。</span><span class="sxs-lookup"><span data-stu-id="9dd53-217">When errors occur the form should preserve the input data the user originally entered so that they don't have to refill their changes manually.</span></span> <span data-ttu-id="9dd53-218">窗体成功完成之前，应根据需要多次重复此过程。</span><span class="sxs-lookup"><span data-stu-id="9dd53-218">This process should repeat as many times as necessary until the form successfully completes.</span></span>

<span data-ttu-id="9dd53-219">ASP.NET MVC 包括一些很好的内置功能，用于简化错误处理和窗体重新显示。</span><span class="sxs-lookup"><span data-stu-id="9dd53-219">ASP.NET MVC includes some nice built-in features that make error handling and form redisplay easy.</span></span> <span data-ttu-id="9dd53-220">若要查看操作中的这些功能，让我们更新我们的编辑操作方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="9dd53-220">To see these features in action let's update our Edit action method with the following code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

<span data-ttu-id="9dd53-221">上面的代码类似于我们以前的实现 – 只是我们现在我们工作周围包装 try/catch 错误处理块。</span><span class="sxs-lookup"><span data-stu-id="9dd53-221">The above code is similar to our previous implementation – except that we are now wrapping a try/catch error handling block around our work.</span></span> <span data-ttu-id="9dd53-222">当调用 UpdateModel()，或者当我们尝试和保存 DinnerRepository （这将引发的异常，我们正在尝试进行保存的 Dinner 对象是否无效，由于我们的模型中的规则冲突），如果发生异常时将我们 catch 错误处理块执行。</span><span class="sxs-lookup"><span data-stu-id="9dd53-222">If an exception occurs either when calling UpdateModel(), or when we try and save the DinnerRepository (which will raise an exception if the Dinner object we are trying to save is invalid because of a rule violation within our model), our catch error handling block will execute.</span></span> <span data-ttu-id="9dd53-223">在其中我们循环 Dinner 对象中存在任何规则冲突，并将它们添加到 ModelState 对象 （其中，我们将讨论很快）。</span><span class="sxs-lookup"><span data-stu-id="9dd53-223">Within it we loop over any rule violations that exist in the Dinner object and add them to a ModelState object (which we'll discuss shortly).</span></span> <span data-ttu-id="9dd53-224">然后，我们重新显示视图。</span><span class="sxs-lookup"><span data-stu-id="9dd53-224">We then redisplay the view.</span></span>

<span data-ttu-id="9dd53-225">若要查看此工作让我们重新运行该应用程序，编辑 Dinner，并将其更改为具有空标题，"BOGUS"EventDate 和美国国家/地区值中使用英国电话号码。</span><span class="sxs-lookup"><span data-stu-id="9dd53-225">To see this working let's re-run the application, edit a Dinner, and change it to have an empty Title, an EventDate of "BOGUS", and use a UK phone number with a country value of USA.</span></span> <span data-ttu-id="9dd53-226">当我们按"保存"按钮时我们的 HTTP POST 编辑方法中将不能保存 Dinner （因为有错误） 并将重新显示窗体：</span><span class="sxs-lookup"><span data-stu-id="9dd53-226">When we press the "Save" button our HTTP POST Edit method will not be able to save the Dinner (because there are errors) and will redisplay the form:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

<span data-ttu-id="9dd53-227">我们的应用程序具有大错误体验。</span><span class="sxs-lookup"><span data-stu-id="9dd53-227">Our application has a decent error experience.</span></span> <span data-ttu-id="9dd53-228">具有无效的输入的文本元素将突出显示为红色，并验证错误消息显示给最终用户有关它们的信息。</span><span class="sxs-lookup"><span data-stu-id="9dd53-228">The text elements with the invalid input are highlighted in red, and validation error messages are displayed to the end user about them.</span></span> <span data-ttu-id="9dd53-229">窗体还保留用户最初输入 – 的输入的数据，以便它们无需重新填充任何内容。</span><span class="sxs-lookup"><span data-stu-id="9dd53-229">The form is also preserving the input data the user originally entered – so that they don't have to refill anything.</span></span>

<span data-ttu-id="9dd53-230">如何操作，您可能会问，这发生？</span><span class="sxs-lookup"><span data-stu-id="9dd53-230">How, you might ask, did this occur?</span></span> <span data-ttu-id="9dd53-231">如何未标题、 EventDate，和 ContactPhone 文本框中突出显示本身以红色并知道要输出最初输入的用户值？</span><span class="sxs-lookup"><span data-stu-id="9dd53-231">How did the Title, EventDate, and ContactPhone textboxes highlight themselves in red and know to output the originally entered user values?</span></span> <span data-ttu-id="9dd53-232">和如何未错误消息显示在顶部列表中？</span><span class="sxs-lookup"><span data-stu-id="9dd53-232">And how did error messages get displayed in the list at the top?</span></span> <span data-ttu-id="9dd53-233">好消息是这未发生魔法-而不是它是因为我们使用的一些内置的 ASP.NET MVC 功能用于简化输入的验证和错误处理方案。</span><span class="sxs-lookup"><span data-stu-id="9dd53-233">The good news is that this didn't occur by magic - rather it was because we used some of the built-in ASP.NET MVC features that make input validation and error handling scenarios easy.</span></span>

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a><span data-ttu-id="9dd53-234">了解 ModelState 和验证的 HTML 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="9dd53-234">Understanding ModelState and the Validation HTML Helper Methods</span></span>

<span data-ttu-id="9dd53-235">控制器类具有一个"ModelState"属性集合，提供了方法，以指示错误存在与传递到视图的模型对象。</span><span class="sxs-lookup"><span data-stu-id="9dd53-235">Controller classes have a "ModelState" property collection which provides a way to indicate that errors exist with a model object being passed to a View.</span></span> <span data-ttu-id="9dd53-236">ModelState 集合中的错误项标识有问题的模型属性的名称 (例如:"标题"、"EventDate"或"ContactPhone")，并允许指定的用户友好错误消息 (例如:"标题是必需的")。</span><span class="sxs-lookup"><span data-stu-id="9dd53-236">Error entries within the ModelState collection identify the name of the model property with the issue (for example: "Title", "EventDate", or "ContactPhone"), and allow a human-friendly error message to be specified (for example: "Title is required").</span></span>

<span data-ttu-id="9dd53-237">*UpdateModel()*时它在尝试将窗体值分配给模型对象的属性时遇到错误后，帮助器方法将自动填充 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="9dd53-237">The *UpdateModel()* helper method automatically populates the ModelState collection when it encounters errors while trying to assign form values to properties on the model object.</span></span> <span data-ttu-id="9dd53-238">例如，我们 Dinner 对象 EventDate 属性是类型为 DateTime。</span><span class="sxs-lookup"><span data-stu-id="9dd53-238">For example, our Dinner object's EventDate property is of type DateTime.</span></span> <span data-ttu-id="9dd53-239">无法在上述方案中向其分配的字符串值"BOGUS"UpdateModel() 方法时，UpdateModel() 方法添加到指示分配错误 ModelState 集合的项出现在与该属性。</span><span class="sxs-lookup"><span data-stu-id="9dd53-239">When the UpdateModel() method was unable to assign the string value "BOGUS" to it in the scenario above, the UpdateModel() method added an entry to the ModelState collection indicating an assignment error had occurred with that property.</span></span>

<span data-ttu-id="9dd53-240">开发人员还可以编写代码以显式添加到 ModelState 集合的错误条目，像我们正在下面我们"捕获"错误处理块内，这使用基于中活动的规则冲突的条目填充 ModelState 集合Dinner 对象：</span><span class="sxs-lookup"><span data-stu-id="9dd53-240">Developers can also write code to explicitly add error entries into the ModelState collection like we are doing below within our "catch" error handling block, which is populating the ModelState collection with entries based on the active Rule Violations in the Dinner object:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a><span data-ttu-id="9dd53-241">与 ModelState 的 html 帮助程序集成</span><span class="sxs-lookup"><span data-stu-id="9dd53-241">Html Helper Integration with ModelState</span></span>

<span data-ttu-id="9dd53-242">呈现输出时，Html.TextBox()-等的 HTML 帮助器方法检查 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="9dd53-242">HTML helper methods - like Html.TextBox() - check the ModelState collection when rendering output.</span></span> <span data-ttu-id="9dd53-243">如果存在错误项，它们呈现的用户输入的值和 CSS 错误类。</span><span class="sxs-lookup"><span data-stu-id="9dd53-243">If an error for the item exists, they render the user-entered value and a CSS error class.</span></span>

<span data-ttu-id="9dd53-244">例如，在我们"的编辑"视图中我们将使用 Html.TextBox() 帮助器方法来呈现我们 Dinner 对象 EventDate:</span><span class="sxs-lookup"><span data-stu-id="9dd53-244">For example, in our "Edit" view we are using the Html.TextBox() helper method to render the EventDate of our Dinner object:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

<span data-ttu-id="9dd53-245">当视图已呈现在错误的方案中时，Html.TextBox() 方法检查 ModelState 集合，以查看是否存在任何与我们 Dinner 对象的"EventDate"属性相关联的错误。</span><span class="sxs-lookup"><span data-stu-id="9dd53-245">When the view was rendered in the error scenario, the Html.TextBox() method checked the ModelState collection to see if there were any errors associated with the "EventDate" property of our Dinner object.</span></span> <span data-ttu-id="9dd53-246">当时出现错误来确定它呈现提交的用户输入 ("BOGUS") 作为值，并添加到 css 错误类&lt;输入类型 ="textbox"/&gt;它生成的标记：</span><span class="sxs-lookup"><span data-stu-id="9dd53-246">When it determined that there was an error it rendered the submitted user input ("BOGUS") as the value, and added a css error class to the &lt;input type="textbox"/&gt; markup it generated:</span></span>

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

<span data-ttu-id="9dd53-247">你可以自定义要查找但是希望 css 错误类的外观。</span><span class="sxs-lookup"><span data-stu-id="9dd53-247">You can customize the appearance of the css error class to look however you want.</span></span> <span data-ttu-id="9dd53-248">在中定义了默认的 CSS 错误类 –"输入的验证错误"– *\content\site.css*样式表，如下所示与下面类似：</span><span class="sxs-lookup"><span data-stu-id="9dd53-248">The default CSS error class – "input-validation-error" – is defined in the *\content\site.css* stylesheet and looks like below:</span></span>

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

<span data-ttu-id="9dd53-249">此 CSS 规则是什么导致我们无效的输入的元素，如下面突出显示：</span><span class="sxs-lookup"><span data-stu-id="9dd53-249">This CSS rule is what caused our invalid input elements to be highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a><span data-ttu-id="9dd53-250">Html.ValidationMessage() Helper Method</span><span class="sxs-lookup"><span data-stu-id="9dd53-250">Html.ValidationMessage() Helper Method</span></span>

<span data-ttu-id="9dd53-251">Html.ValidationMessage() 帮助器方法可以用于输出与特定模型属性关联的 ModelState 错误消息：</span><span class="sxs-lookup"><span data-stu-id="9dd53-251">The Html.ValidationMessage() helper method can be used to output the ModelState error message associated with a particular model property:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

<span data-ttu-id="9dd53-252">上面的代码将输出：  *&lt;class ="字段验证错误"&gt; BOGUS 的值无效&lt;/&gt;*</span><span class="sxs-lookup"><span data-stu-id="9dd53-252">The above code outputs: *&lt;span class="field-validation-error"&gt; The value ‘BOGUS' is invalid&lt;/span&gt;*</span></span>

<span data-ttu-id="9dd53-253">Html.ValidationMessage() 帮助器方法还支持允许开发人员重写将显示错误文本消息的第二个参数：</span><span class="sxs-lookup"><span data-stu-id="9dd53-253">The Html.ValidationMessage() helper method also supports a second parameter that allows developers to override the error text message that is displayed:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

<span data-ttu-id="9dd53-254">上面的代码将输出：  <em>&lt;class ="字段验证错误"&gt;\*&lt;/&gt;</em>而不是为存在错误时的默认错误文本EventDate 属性。</span><span class="sxs-lookup"><span data-stu-id="9dd53-254">The above code outputs: <em>&lt;span class="field-validation-error"&gt;\*&lt;/span&gt;</em>instead of the default error text when an error is present for the EventDate property.</span></span>

##### <a name="htmlvalidationsummary-helper-method"></a><span data-ttu-id="9dd53-255">Html.ValidationSummary() Helper Method</span><span class="sxs-lookup"><span data-stu-id="9dd53-255">Html.ValidationSummary() Helper Method</span></span>

<span data-ttu-id="9dd53-256">Html.ValidationSummary() 帮助器方法可以用于呈现错误消息摘要，伴随&lt;ul&gt;&lt;li /&gt;&lt;u l&gt;消息中的所有详细的错误的列表ModelState 集合：</span><span class="sxs-lookup"><span data-stu-id="9dd53-256">The Html.ValidationSummary() helper method can be used to render a summary error message, accompanied by a &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; list of all detailed error messages in the ModelState collection:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

<span data-ttu-id="9dd53-257">Html.ValidationSummary() 帮助程序方法采用一个可选的字符串参数 – 定义要显示详细的错误列表上方的摘要的错误消息：</span><span class="sxs-lookup"><span data-stu-id="9dd53-257">The Html.ValidationSummary() helper method takes an optional string parameter – which defines a summary error message to display above the list of detailed errors:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

<span data-ttu-id="9dd53-258">你可以选择使用 CSS 重写错误列表如下所示。</span><span class="sxs-lookup"><span data-stu-id="9dd53-258">You can optionally use CSS to override what the error list looks like.</span></span>

#### <a name="using-a-addruleviolations-helper-method"></a><span data-ttu-id="9dd53-259">使用一个 AddRuleViolations 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="9dd53-259">Using a AddRuleViolations Helper Method</span></span>

<span data-ttu-id="9dd53-260">我们初始 HTTP POST 编辑实现使用其 catch 块中的 foreach 语句循环访问 Dinner 对象的规则冲突，并将其添加到控制器的 ModelState 集合：</span><span class="sxs-lookup"><span data-stu-id="9dd53-260">Our initial HTTP-POST Edit implementation used a foreach statement within its catch block to loop over the Dinner object's Rule Violations and add them to the controller's ModelState collection:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

<span data-ttu-id="9dd53-261">我们会使此代码通过添加"ControllerHelpers"少清洗磁带到 NerdDinner 项目中，类，实现"AddRuleViolations"扩展方法中，添加到 ASP.NET MVC ModelStateDictionary 类的一个帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="9dd53-261">We can make this code a little cleaner by adding a "ControllerHelpers" class to the NerdDinner project, and implement an "AddRuleViolations" extension method within it that adds a helper method to the ASP.NET MVC ModelStateDictionary class.</span></span> <span data-ttu-id="9dd53-262">此扩展方法可以封装填充 ModelStateDictionary RuleViolation 错误的列表所需的逻辑：</span><span class="sxs-lookup"><span data-stu-id="9dd53-262">This extension method can encapsulate the logic necessary to populate the ModelStateDictionary with a list of RuleViolation errors:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

<span data-ttu-id="9dd53-263">然后，我们可以更新我们 HTTP POST 编辑操作方法以使用此扩展方法来填充具有我们 Dinner 规则冲突的 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="9dd53-263">We can then update our HTTP-POST Edit action method to use this extension method to populate the ModelState collection with our Dinner Rule Violations.</span></span>

#### <a name="complete-edit-action-method-implementations"></a><span data-ttu-id="9dd53-264">完成编辑操作方法实现</span><span class="sxs-lookup"><span data-stu-id="9dd53-264">Complete Edit Action Method Implementations</span></span>

<span data-ttu-id="9dd53-265">下面的代码实现了所有我们编辑的方案所需的控制器逻辑：</span><span class="sxs-lookup"><span data-stu-id="9dd53-265">The code below implements all of the controller logic necessary for our Edit scenario:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

<span data-ttu-id="9dd53-266">有关我们编辑实现很棒是我们控制器类和我们的视图模板都不需一无所知特定验证或通过我们的 Dinner 模型强制实施业务规则。</span><span class="sxs-lookup"><span data-stu-id="9dd53-266">The nice thing about our Edit implementation is that neither our Controller class nor our View template has to know anything about the specific validation or business rules being enforced by our Dinner model.</span></span> <span data-ttu-id="9dd53-267">我们可以将其他规则在将来添加到我们的模型，而不需要对我们控制器或以使其必须支持的视图进行任何代码更改。</span><span class="sxs-lookup"><span data-stu-id="9dd53-267">We can add additional rules to our model in the future and do not have to make any code changes to our controller or view in order for them to be supported.</span></span> <span data-ttu-id="9dd53-268">这为我们提供了灵活地可以方便地改进我们应用程序要求在将来使用最少的代码更改。</span><span class="sxs-lookup"><span data-stu-id="9dd53-268">This provides us with the flexibility to easily evolve our application requirements in the future with a minimum of code changes.</span></span>

### <a name="create-support"></a><span data-ttu-id="9dd53-269">创建支持</span><span class="sxs-lookup"><span data-stu-id="9dd53-269">Create Support</span></span>

<span data-ttu-id="9dd53-270">我们已经完成了实现我们 DinnersController 类的"编辑"行为。</span><span class="sxs-lookup"><span data-stu-id="9dd53-270">We've finished implementing the "Edit" behavior of our DinnersController class.</span></span> <span data-ttu-id="9dd53-271">让我们现在转上它 – 它将使用户能够添加新晚餐实现的"创建"支持。</span><span class="sxs-lookup"><span data-stu-id="9dd53-271">Let's now move on to implement the "Create" support on it – which will enable users to add new Dinners.</span></span>

#### <a name="the-http-get-create-action-method"></a><span data-ttu-id="9dd53-272">HTTP GET 创建操作方法</span><span class="sxs-lookup"><span data-stu-id="9dd53-272">The HTTP-GET Create Action Method</span></span>

<span data-ttu-id="9dd53-273">我们将首先通过实现的 HTTP"GET"行为我们创建操作方法。</span><span class="sxs-lookup"><span data-stu-id="9dd53-273">We'll begin by implementing the HTTP "GET" behavior of our create action method.</span></span> <span data-ttu-id="9dd53-274">在有人访问时，将调用此方法*/晚餐/创建*URL。</span><span class="sxs-lookup"><span data-stu-id="9dd53-274">This method will be called when someone visits the */Dinners/Create* URL.</span></span> <span data-ttu-id="9dd53-275">我们实现如下所示：</span><span class="sxs-lookup"><span data-stu-id="9dd53-275">Our implementation looks like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

<span data-ttu-id="9dd53-276">上面的代码创建一个新的 Dinner 对象，并将分配其 EventDate 属性设置为在将来的一周。</span><span class="sxs-lookup"><span data-stu-id="9dd53-276">The code above creates a new Dinner object, and assigns its EventDate property to be one week in the future.</span></span> <span data-ttu-id="9dd53-277">它随后将呈现基于新的 Dinner 对象的视图。</span><span class="sxs-lookup"><span data-stu-id="9dd53-277">It then renders a View that is based on the new Dinner object.</span></span> <span data-ttu-id="9dd53-278">因为我们尚未显式传递到名称*View()*帮助器方法，它将使用基于约定的默认路径来解析视图模板： /Views/Dinners/Create.aspx。</span><span class="sxs-lookup"><span data-stu-id="9dd53-278">Because we haven't explicitly passed a name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Create.aspx.</span></span>

<span data-ttu-id="9dd53-279">让我们现在创建此视图模板。</span><span class="sxs-lookup"><span data-stu-id="9dd53-279">Let's now create this view template.</span></span> <span data-ttu-id="9dd53-280">我们可以在创建操作方法内右键单击并选择"添加视图"上下文菜单命令来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="9dd53-280">We can do this by right-clicking within the Create action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="9dd53-281">在"添加视图"对话框将指示我们将 Dinner 对象传递给视图模板，并选择"创建"模板自动基架：</span><span class="sxs-lookup"><span data-stu-id="9dd53-281">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to the view template, and choose to auto-scaffold a "Create" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

<span data-ttu-id="9dd53-282">当我们单击"添加"按钮时，会将新的基架基于"Create.aspx"视图保存到"\Views\Dinners"目录中，Visual Studio 并将其在 IDE 中打开它：</span><span class="sxs-lookup"><span data-stu-id="9dd53-282">When we click the "Add" button, Visual Studio will save a new scaffold-based "Create.aspx" view to the "\Views\Dinners" directory, and open it up within the IDE:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

<span data-ttu-id="9dd53-283">让我们对我们而言，默认"的创建"基架已生成文件进行一些更改，并对其进行修改设置为类似于下面：</span><span class="sxs-lookup"><span data-stu-id="9dd53-283">Let's make a few changes to the default "create" scaffold file that was generated for us, and modify it up to look like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

<span data-ttu-id="9dd53-284">现在当我们运行我们的应用程序和访问时和*"/ 晚餐/创建"*以及浏览器，它会从我们创建操作实现呈现类似下面的 UI 中的 URL:</span><span class="sxs-lookup"><span data-stu-id="9dd53-284">And now when we run our application and access the *"/Dinners/Create"* URL within the browser it will render UI like below from our Create action implementation:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a><span data-ttu-id="9dd53-285">创建实现 HTTP POST 操作方法</span><span class="sxs-lookup"><span data-stu-id="9dd53-285">Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="9dd53-286">我们有我们创建的操作方法中实现的 HTTP GET 版本。</span><span class="sxs-lookup"><span data-stu-id="9dd53-286">We have the HTTP-GET version of our Create action method implemented.</span></span> <span data-ttu-id="9dd53-287">当用户单击"保存"按钮时它会执行窗体发送到*/晚餐/创建*URL，并在提交 HTML&lt;输入&gt;窗体中使用 HTTP POST 谓词的值。</span><span class="sxs-lookup"><span data-stu-id="9dd53-287">When a user clicks the "Save" button it performs a form post to the */Dinners/Create* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span>

<span data-ttu-id="9dd53-288">让我们现在实现的 HTTP POST 行为的我们创建操作方法。</span><span class="sxs-lookup"><span data-stu-id="9dd53-288">Let's now implement the HTTP POST behavior of our create action method.</span></span> <span data-ttu-id="9dd53-289">我们将首先通过将重载的"创建"操作方法添加到对其具有"AcceptVerbs"属性，该值指示它将处理 HTTP POST 方案我们 DinnersController:</span><span class="sxs-lookup"><span data-stu-id="9dd53-289">We'll begin by adding an overloaded "Create" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

<span data-ttu-id="9dd53-290">有多种方式我们就可以在我们 HTTP POST 启用"创建"方法内访问的已发布的窗体参数。</span><span class="sxs-lookup"><span data-stu-id="9dd53-290">There are a variety of ways we can access the posted form parameters within our HTTP-POST enabled "Create" method.</span></span>

<span data-ttu-id="9dd53-291">一种方法是创建新的 Dinner 对象，然后使用*UpdateModel()*帮助器方法 （例如，我们使用编辑操作所做的那样） 使用已发布的窗体值其进行填充。</span><span class="sxs-lookup"><span data-stu-id="9dd53-291">One approach is to create a new Dinner object and then use the *UpdateModel()* helper method (like we did with the Edit action) to populate it with the posted form values.</span></span> <span data-ttu-id="9dd53-292">我们然后可以将其添加到我们 DinnerRepository、 将其保存到数据库，并将用户重定向到我们的详细信息操作以显示新创建的 Dinner 使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="9dd53-292">We can then add it to our DinnerRepository, persist it to the database, and redirect the user to our Details action to show the newly created Dinner using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

<span data-ttu-id="9dd53-293">或者，我们可以使用一种方法还有我们需要 Dinner 对象作为方法参数的 create （） 操作方法。</span><span class="sxs-lookup"><span data-stu-id="9dd53-293">Alternatively, we can use an approach where we have our Create() action method take a Dinner object as a method parameter.</span></span> <span data-ttu-id="9dd53-294">ASP.NET MVC 将然后自动实例化新 Dinner 对象，为我们、 填充其属性使用的窗体输入，并将其传递给我们操作方法：</span><span class="sxs-lookup"><span data-stu-id="9dd53-294">ASP.NET MVC will then automatically instantiate a new Dinner object for us, populate its properties using the form inputs, and pass it to our action method:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

<span data-ttu-id="9dd53-295">上述我们操作方法验证，Dinner 对象具有已成功的值填充填充窗体 post 通过检查 ModelState.IsValid 属性。</span><span class="sxs-lookup"><span data-stu-id="9dd53-295">Our action method above verifies that the Dinner object has been successfully populated with the form post values by checking the ModelState.IsValid property.</span></span> <span data-ttu-id="9dd53-296">这将返回 false，如果没有输入转换问题 (例如： EventDate 属性的"BOGUS"的字符串)，如果有任何问题我们操作方法重新显示窗体和。</span><span class="sxs-lookup"><span data-stu-id="9dd53-296">This will return false if there are input conversion issues (for example: a string of "BOGUS" for the EventDate property), and if there are any issues our action method redisplays the form.</span></span>

<span data-ttu-id="9dd53-297">如果输入的值在有效时，操作方法就尝试添加并将新 Dinner 保存到 DinnerRepository。</span><span class="sxs-lookup"><span data-stu-id="9dd53-297">If the input values are valid, then the action method attempts to add and save the new Dinner to the DinnerRepository.</span></span> <span data-ttu-id="9dd53-298">它包装在一个 try/catch 块为此工作，并显示窗体，如果有任何业务规则冲突 （从而导致 dinnerRepository.Save() 方法来引发异常）。</span><span class="sxs-lookup"><span data-stu-id="9dd53-298">It wraps this work within a try/catch block and redisplays the form if there are any business rule violations (which would cause the dinnerRepository.Save() method to raise an exception).</span></span>

<span data-ttu-id="9dd53-299">若要查看此错误处理操作中的行为，我们可以请求*/晚餐/创建*URL 和新 Dinner 有关的详细信息，请填写。</span><span class="sxs-lookup"><span data-stu-id="9dd53-299">To see this error handling behavior in action, we can request the */Dinners/Create* URL and fill out details about a new Dinner.</span></span> <span data-ttu-id="9dd53-300">输入不正确或值将导致创建窗体，以重新显示与下面类似突出显示的错误：</span><span class="sxs-lookup"><span data-stu-id="9dd53-300">Incorrect input or values will cause the create form to be redisplayed with the errors highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

<span data-ttu-id="9dd53-301">请注意如何我们创建窗体遵守精确相同验证和业务规则为我们编辑窗体。</span><span class="sxs-lookup"><span data-stu-id="9dd53-301">Notice how our Create form is honoring the exact same validation and business rules as our Edit form.</span></span> <span data-ttu-id="9dd53-302">这是因为我们验证规则和业务规则已定义在模型中，并且未嵌入在 UI 或应用程序的控制器中。</span><span class="sxs-lookup"><span data-stu-id="9dd53-302">This is because our validation and business rules were defined in the model, and were not embedded within the UI or controller of the application.</span></span> <span data-ttu-id="9dd53-303">这意味着我们可以稍后更改/发展我们验证或业务规则在单个放置，并将它们应用于整个应用程序。</span><span class="sxs-lookup"><span data-stu-id="9dd53-303">This means we can later change/evolve our validation or business rules in a single place and have them apply throughout our application.</span></span> <span data-ttu-id="9dd53-304">我们将无需更改一个内部的任何代码我们编辑或创建操作的方法来自动接受任何新的规则或对现有文件的修改。</span><span class="sxs-lookup"><span data-stu-id="9dd53-304">We will not have to change any code within either our Edit or Create action methods to automatically honor any new rules or modifications to existing ones.</span></span>

<span data-ttu-id="9dd53-305">当我们解决的输入的值并单击"保存"按钮时试，我们添加到 DinnerRepository 将成功，并且新 Dinner 将添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="9dd53-305">When we fix the input values and click the "Save" button again, our addition to the DinnerRepository will succeed, and a new Dinner will be added to the database.</span></span> <span data-ttu-id="9dd53-306">我们然后定向到*/Dinners/详细信息 / [id]* URL – 其中我们将提供有关新创建的 Dinner 的详细信息：</span><span class="sxs-lookup"><span data-stu-id="9dd53-306">We will then be redirected to the */Dinners/Details/[id]* URL – where we will be presented with details about the newly created Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a><span data-ttu-id="9dd53-307">Delete 支持</span><span class="sxs-lookup"><span data-stu-id="9dd53-307">Delete Support</span></span>

<span data-ttu-id="9dd53-308">让我们现在添加到我们 DinnersController 的"删除"支持。</span><span class="sxs-lookup"><span data-stu-id="9dd53-308">Let's now add "Delete" support to our DinnersController.</span></span>

#### <a name="the-http-get-delete-action-method"></a><span data-ttu-id="9dd53-309">HTTP GET Delete 操作方法</span><span class="sxs-lookup"><span data-stu-id="9dd53-309">The HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="9dd53-310">我们将首先通过实现我们删除操作方法的 HTTP GET 行为。</span><span class="sxs-lookup"><span data-stu-id="9dd53-310">We'll begin by implementing the HTTP GET behavior of our delete action method.</span></span> <span data-ttu-id="9dd53-311">在有人访问时，将会调用此方法*/Dinners/删除 / [id]* URL。</span><span class="sxs-lookup"><span data-stu-id="9dd53-311">This method will get called when someone visits the */Dinners/Delete/[id]* URL.</span></span> <span data-ttu-id="9dd53-312">下面是实现：</span><span class="sxs-lookup"><span data-stu-id="9dd53-312">Below is the implementation:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

<span data-ttu-id="9dd53-313">尝试检索 Dinner 要删除的操作方法。</span><span class="sxs-lookup"><span data-stu-id="9dd53-313">The action method attempts to retrieve the Dinner to be deleted.</span></span> <span data-ttu-id="9dd53-314">如果 Dinner 存在呈现视图基于 Dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="9dd53-314">If the Dinner exists it renders a View based on the Dinner object.</span></span> <span data-ttu-id="9dd53-315">如果对象不存在 （或已删除） 它返回呈现"NotFound"视图查看我们在我们的"详细信息"操作方法前面创建的模板。</span><span class="sxs-lookup"><span data-stu-id="9dd53-315">If the object doesn't exist (or has already been deleted) it returns a View that renders the "NotFound" view template we created earlier for our "Details" action method.</span></span>

<span data-ttu-id="9dd53-316">我们可以在删除操作方法内右键单击并选择"添加视图"上下文菜单命令来创建"删除"查看模板。</span><span class="sxs-lookup"><span data-stu-id="9dd53-316">We can create the "Delete" view template by right-clicking within the Delete action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="9dd53-317">在"添加视图"对话框中，我们将指示我们 Dinner 对象传递给其模型中，我们查看模板，并选择创建一个空的模板：</span><span class="sxs-lookup"><span data-stu-id="9dd53-317">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to create an empty template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

<span data-ttu-id="9dd53-318">当我们单击"添加"按钮时，Visual Studio 将我们"\Views\Dinners"目录中为我们添加新的"Delete.aspx"视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="9dd53-318">When we click the "Add" button, Visual Studio will add a new "Delete.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="9dd53-319">我们将向模板来实现删除确认屏幕中添加一些 HTML 和代码与下面类似：</span><span class="sxs-lookup"><span data-stu-id="9dd53-319">We'll add some HTML and code to the template to implement a delete confirmation screen like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

<span data-ttu-id="9dd53-320">上面的代码显示要删除的 Dinner 和输出的标题&lt;窗体&gt;对 /Dinners/删除 / [id] URL 执行 POST，如果最终用户单击"删除"按钮在其中的元素。</span><span class="sxs-lookup"><span data-stu-id="9dd53-320">The code above displays the title of the Dinner to be deleted, and outputs a &lt;form&gt; element that does a POST to the /Dinners/Delete/[id] URL if the end-user clicks the "Delete" button within it.</span></span>

<span data-ttu-id="9dd53-321">当我们运行我们的应用程序和访问*"/ 晚餐/删除 / [id]"* URL 有效 Dinner 对象它呈现用户界面与下面类似：</span><span class="sxs-lookup"><span data-stu-id="9dd53-321">When we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it renders UI like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| <span data-ttu-id="9dd53-322">**端主题内容： 我们为什么做 POST？**</span><span class="sxs-lookup"><span data-stu-id="9dd53-322">**Side Topic: Why are we doing a POST?**</span></span> |
| --- |
| <span data-ttu-id="9dd53-323">您可能会问 – 为何我们未向演示创建的工作量&lt;窗体&gt;我们删除确认屏幕中？</span><span class="sxs-lookup"><span data-stu-id="9dd53-323">You might ask – why did we go through the effort of creating a &lt;form&gt; within our Delete confirmation screen?</span></span> <span data-ttu-id="9dd53-324">为什么不直接使用标准的超链接来链接到操作方法，可执行实际的删除操作？</span><span class="sxs-lookup"><span data-stu-id="9dd53-324">Why not just use a standard hyperlink to link to an action method that does the actual delete operation?</span></span> <span data-ttu-id="9dd53-325">原因是因为我们想要小心地将其避免出现爬网程序，并搜索引擎发现了 Url 和无意中导致数据被删除时它们遵循以下链接。</span><span class="sxs-lookup"><span data-stu-id="9dd53-325">The reason is because we want to be careful to guard against web-crawlers and search engines discovering our URLs and inadvertently causing data to be deleted when they follow the links.</span></span> <span data-ttu-id="9dd53-326">HTTP GET 基于 Url 被视为"安全"，以帮助用户访问/爬网，并且它们应该不遵循 HTTP POST 的。</span><span class="sxs-lookup"><span data-stu-id="9dd53-326">HTTP-GET based URLs are considered "safe" for them to access/crawl, and they are supposed to not follow HTTP-POST ones.</span></span> <span data-ttu-id="9dd53-327">种好的做法是确保你始终将放破坏性或 HTTP POST 请求背后的数据修改操作。</span><span class="sxs-lookup"><span data-stu-id="9dd53-327">A good rule is to make sure you always put destructive or data modifying operations behind HTTP-POST requests.</span></span> |

#### <a name="implementing-the-http-post-delete-action-method"></a><span data-ttu-id="9dd53-328">实现 HTTP POST Delete 操作方法</span><span class="sxs-lookup"><span data-stu-id="9dd53-328">Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="9dd53-329">我们现在有实现我们 Delete 操作方法的 HTTP GET 版本后者将显示删除确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="9dd53-329">We now have the HTTP-GET version of our Delete action method implemented which displays a delete confirmation screen.</span></span> <span data-ttu-id="9dd53-330">当最终用户单击"删除"按钮时它将执行到窗体发布请求*/Dinners/Dinner / [id]* URL。</span><span class="sxs-lookup"><span data-stu-id="9dd53-330">When an end user clicks the "Delete" button it will perform a form post to the */Dinners/Dinner/[id]* URL.</span></span>

<span data-ttu-id="9dd53-331">让我们现在实现的 HTTP"发布"行为的使用下面的代码的删除操作方法：</span><span class="sxs-lookup"><span data-stu-id="9dd53-331">Let's now implement the HTTP "POST" behavior of the delete action method using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

<span data-ttu-id="9dd53-332">我们 Delete 操作方法的 HTTP POST 版本尝试检索要删除的 dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="9dd53-332">The HTTP-POST version of our Delete action method attempts to retrieve the dinner object to delete.</span></span> <span data-ttu-id="9dd53-333">如果它找不到它 （因为它已被删除） 呈现我们"NotFound"的模板。</span><span class="sxs-lookup"><span data-stu-id="9dd53-333">If it can't find it (because it has already been deleted) it renders our "NotFound" template.</span></span> <span data-ttu-id="9dd53-334">如果找到 Dinner，它可以从 DinnerRepository 删除它。</span><span class="sxs-lookup"><span data-stu-id="9dd53-334">If it finds the Dinner, it deletes it from the DinnerRepository.</span></span> <span data-ttu-id="9dd53-335">它随后将呈现已删除"模板。</span><span class="sxs-lookup"><span data-stu-id="9dd53-335">It then renders a "Deleted" template.</span></span>

<span data-ttu-id="9dd53-336">若要实现我们将操作方法中右键单击并选择"添加视图"上下文菜单的"已删除"模板。</span><span class="sxs-lookup"><span data-stu-id="9dd53-336">To implement the "Deleted" template we'll right-click in the action method and choose the "Add View" context menu.</span></span> <span data-ttu-id="9dd53-337">我们将我们的视图已删除"命名，使其成为空模板 （且不会强类型模型对象）。</span><span class="sxs-lookup"><span data-stu-id="9dd53-337">We'll name our view "Deleted" and have it be an empty template (and not take a strongly-typed model object).</span></span> <span data-ttu-id="9dd53-338">然后，我们将向其添加一些 HTML 内容：</span><span class="sxs-lookup"><span data-stu-id="9dd53-338">We'll then add some HTML content to it:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

<span data-ttu-id="9dd53-339">现在当我们运行我们的应用程序和访问时和*"/ 晚餐/删除 / [id]"*类似下面的对象，它会呈现我们 Dinner 删除确认有效 Dinner URL 屏幕：</span><span class="sxs-lookup"><span data-stu-id="9dd53-339">And now when we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it will render our Dinner delete confirmation screen like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

<span data-ttu-id="9dd53-340">单击"删除"按钮时它将执行到 HTTP POST */Dinners/删除 / [id]* URL，这将删除 Dinner 从我们的数据库，并显示我们已删除"查看模板：</span><span class="sxs-lookup"><span data-stu-id="9dd53-340">When we click the "Delete" button it will perform an HTTP-POST to the */Dinners/Delete/[id]* URL, which will delete the Dinner from our database, and display our "Deleted" view template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a><span data-ttu-id="9dd53-341">模型绑定安全性</span><span class="sxs-lookup"><span data-stu-id="9dd53-341">Model Binding Security</span></span>

<span data-ttu-id="9dd53-342">我们已讨论了两种不同方式使用 ASP.NET MVC 的内置模型绑定功能。</span><span class="sxs-lookup"><span data-stu-id="9dd53-342">We've discussed two different ways to use the built-in model-binding features of ASP.NET MVC.</span></span> <span data-ttu-id="9dd53-343">首先使用 UpdateModel() 方法来更新现有模型对象的属性和第二个使用 ASP.NET MVC 将作为操作方法参数传递中的模型对象的支持。</span><span class="sxs-lookup"><span data-stu-id="9dd53-343">The first using the UpdateModel() method to update properties on an existing model object, and the second using ASP.NET MVC's support for passing model objects in as action method parameters.</span></span> <span data-ttu-id="9dd53-344">这两种技术是非常强大和非常有用。</span><span class="sxs-lookup"><span data-stu-id="9dd53-344">Both of these techniques are very powerful and extremely useful.</span></span>

<span data-ttu-id="9dd53-345">此 power 也会与其责任。</span><span class="sxs-lookup"><span data-stu-id="9dd53-345">This power also brings with it responsibility.</span></span> <span data-ttu-id="9dd53-346">必须始终为需要保持警惕有关安全，如果接受任何用户输入，并也是如此时将对象绑定到窗体输入。</span><span class="sxs-lookup"><span data-stu-id="9dd53-346">It is important to always be paranoid about security when accepting any user input, and this is also true when binding objects to form input.</span></span> <span data-ttu-id="9dd53-347">应注意到 HTML 始终对任何用户输入的值，以避免 HTML 和 JavaScript 注入攻击，并小心 SQL 注入式攻击进行编码 (请注意： 我们将使用 LINQ to SQL 对于我们的应用程序，它自动将编码参数以防止这些类型的攻击）。</span><span class="sxs-lookup"><span data-stu-id="9dd53-347">You should be careful to always HTML encode any user-entered values to avoid HTML and JavaScript injection attacks, and be careful of SQL injection attacks (note: we are using LINQ to SQL for our application, which automatically encodes parameters to prevent these types of attacks).</span></span> <span data-ttu-id="9dd53-348">永远不应依赖于客户端验证单独出现时，并始终使用服务器端验证若要防止黑客尝试发送伪造的值。</span><span class="sxs-lookup"><span data-stu-id="9dd53-348">You should never rely on client-side validation alone, and always employ server-side validation to guard against hackers attempting to send you bogus values.</span></span>

<span data-ttu-id="9dd53-349">请确保你考虑使用 ASP.NET MVC 的绑定功能时的一个额外的安全项目是你正在绑定的对象的作用域。</span><span class="sxs-lookup"><span data-stu-id="9dd53-349">One additional security item to make sure you think about when using the binding features of ASP.NET MVC is the scope of the objects you are binding.</span></span> <span data-ttu-id="9dd53-350">具体而言，你想要确保你了解你允许将以可绑定，并确保仅允许那些实际上应为可更新最终用户要更新的属性的属性的安全含义。</span><span class="sxs-lookup"><span data-stu-id="9dd53-350">Specifically, you want to make sure you understand the security implications of the properties you are allowing to be bound, and make sure you only allow those properties that really should be updatable by an end-user to be updated.</span></span>

<span data-ttu-id="9dd53-351">默认情况下，UpdateModel() 方法将尝试更新模型对象传入的窗体参数值相匹配的所有属性。</span><span class="sxs-lookup"><span data-stu-id="9dd53-351">By default, the UpdateModel() method will attempt to update all properties on the model object that match incoming form parameter values.</span></span> <span data-ttu-id="9dd53-352">同样，为操作方法参数也默认传递的对象会有所有窗体参数通过设置其属性。</span><span class="sxs-lookup"><span data-stu-id="9dd53-352">Likewise, objects passed as action method parameters also by default can have all of their properties set via form parameters.</span></span>

#### <a name="locking-down-binding-on-a-per-usage-basis"></a><span data-ttu-id="9dd53-353">锁定按每个使用量付费的绑定</span><span class="sxs-lookup"><span data-stu-id="9dd53-353">Locking down binding on a per-usage basis</span></span>

<span data-ttu-id="9dd53-354">您可以通过提供显式"包括列表"可更新的属性的锁定按每个使用量付费的绑定策略。</span><span class="sxs-lookup"><span data-stu-id="9dd53-354">You can lock down the binding policy on a per-usage basis by providing an explicit "include list" of properties that can be updated.</span></span> <span data-ttu-id="9dd53-355">这可以通过将的额外字符串数组参数传递给 UpdateModel() 类似方法下：</span><span class="sxs-lookup"><span data-stu-id="9dd53-355">This can be done by passing an extra string array parameter to the UpdateModel() method like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

<span data-ttu-id="9dd53-356">对象作为参数传递，操作方法还支持启用"包括列表"的允许属性，如下面指定的 [绑定] 特性：</span><span class="sxs-lookup"><span data-stu-id="9dd53-356">Objects passed as action method parameters also support a [Bind] attribute that enables an "include list" of allowed properties to be specified like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a><span data-ttu-id="9dd53-357">锁定基于类型的绑定</span><span class="sxs-lookup"><span data-stu-id="9dd53-357">Locking down binding on a type basis</span></span>

<span data-ttu-id="9dd53-358">您可以锁定根据每种类型的绑定规则。</span><span class="sxs-lookup"><span data-stu-id="9dd53-358">You can also lock down the binding rules on a per-type basis.</span></span> <span data-ttu-id="9dd53-359">这允许您一次，指定绑定规则，然后将它们在所有方案 （包括 UpdateModel 和操作方法参数方案） 中应用所有控制器和操作方法。</span><span class="sxs-lookup"><span data-stu-id="9dd53-359">This allows you to specify the binding rules once, and then have them apply in all scenarios (including both UpdateModel and action method parameter scenarios) across all controllers and action methods.</span></span>

<span data-ttu-id="9dd53-360">通过添加到一种类型，[绑定] 属性或注册 （适用于您自己的类型的方案） 应用程序的 Global.asax 文件中，你可以自定义每种类型的绑定规则。</span><span class="sxs-lookup"><span data-stu-id="9dd53-360">You can customize the per-type binding rules by adding a [Bind] attribute onto a type, or by registering it within the Global.asax file of the application (useful for scenarios where you don't own the type).</span></span> <span data-ttu-id="9dd53-361">然后，你可以使用绑定属性的包含和排除属性来控制哪些属性是可绑定为特定类或接口。</span><span class="sxs-lookup"><span data-stu-id="9dd53-361">You can then use the Bind attribute's Include and Exclude properties to control which properties are bindable for the particular class or interface.</span></span>

<span data-ttu-id="9dd53-362">我们将使用此方法来 Dinner 类进行中我们 NerdDinner 的应用程序，并将 [绑定] 特性添加到它的可绑定属性的列表限制到以下：</span><span class="sxs-lookup"><span data-stu-id="9dd53-362">We'll use this technique for the Dinner class in our NerdDinner application, and add a [Bind] attribute to it that restricts the list of bindable properties to the following:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

<span data-ttu-id="9dd53-363">请注意我们不允许 RSVPs 集合要操作通过绑定，也不我们允许 DinnerID 或 HostedBy 属性，以通过绑定设置。</span><span class="sxs-lookup"><span data-stu-id="9dd53-363">Notice we are not allowing the RSVPs collection to be manipulated via binding, nor are we allowing the DinnerID or HostedBy properties to be set via binding.</span></span> <span data-ttu-id="9dd53-364">出于安全原因我们将改为仅操作使用我们的操作方法中的显式代码这些特定属性。</span><span class="sxs-lookup"><span data-stu-id="9dd53-364">For security reasons we'll instead only manipulate these particular properties using explicit code within our action methods.</span></span>

### <a name="crud-wrap-up"></a><span data-ttu-id="9dd53-365">CRUD 总结</span><span class="sxs-lookup"><span data-stu-id="9dd53-365">CRUD Wrap-Up</span></span>

<span data-ttu-id="9dd53-366">ASP.NET MVC 包括许多内置功能，可帮助完成实现发布方案的窗体。</span><span class="sxs-lookup"><span data-stu-id="9dd53-366">ASP.NET MVC includes a number of built-in features that help with implementing form posting scenarios.</span></span> <span data-ttu-id="9dd53-367">我们使用了各种各样的这些功能在我们 DinnerRepository 之上提供 CRUD UI 支持。</span><span class="sxs-lookup"><span data-stu-id="9dd53-367">We used a variety of these features to provide CRUD UI support on top of our DinnerRepository.</span></span>

<span data-ttu-id="9dd53-368">我们将使用的模型已设定焦点的方法来实现我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="9dd53-368">We are using a model-focused approach to implement our application.</span></span> <span data-ttu-id="9dd53-369">这意味着，我们的验证和业务规则在我们的模型层 – 以及不中我们控制器或视图定义逻辑。</span><span class="sxs-lookup"><span data-stu-id="9dd53-369">This means that all our validation and business rule logic is defined within our model layer – and not within our controllers or views.</span></span> <span data-ttu-id="9dd53-370">我们控制器类和我们查看模板都不知道任何有关由我们 Dinner 模型类强制实施的特定业务规则。</span><span class="sxs-lookup"><span data-stu-id="9dd53-370">Neither our Controller class nor our View templates know anything about the specific business rules being enforced by our Dinner model class.</span></span>

<span data-ttu-id="9dd53-371">这将使我们的应用程序体系结构清理并使它可以轻松地测试。</span><span class="sxs-lookup"><span data-stu-id="9dd53-371">This will keep our application architecture clean and make it easier to test.</span></span> <span data-ttu-id="9dd53-372">我们可以在将来向我们的模型层添加更多的业务规则和*无需进行任何代码更改*到我们的控制器或视图，以使其支持。</span><span class="sxs-lookup"><span data-stu-id="9dd53-372">We can add additional business rules to our model layer in the future and *not have to make any code changes* to our Controller or View in order for them to be supported.</span></span> <span data-ttu-id="9dd53-373">这将向我们提供了极大的灵活性发展和更改在将来，我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="9dd53-373">This is going to provide us with a great deal of agility to evolve and change our application in the future.</span></span>

<span data-ttu-id="9dd53-374">我们 DinnersController 现在使 Dinner 列表/详细信息，以及创建、 编辑和 delete 支持。</span><span class="sxs-lookup"><span data-stu-id="9dd53-374">Our DinnersController now enables Dinner listings/details, as well as create, edit and delete support.</span></span> <span data-ttu-id="9dd53-375">类的完整代码可在下面找到：</span><span class="sxs-lookup"><span data-stu-id="9dd53-375">The complete code for the class can be found below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a><span data-ttu-id="9dd53-376">下一步</span><span class="sxs-lookup"><span data-stu-id="9dd53-376">Next Step</span></span>

<span data-ttu-id="9dd53-377">我们现在有我们 DinnersController 类中实现的基本 CRUD （创建、 读取、 更新和删除） 支持。</span><span class="sxs-lookup"><span data-stu-id="9dd53-377">We now have basic CRUD (Create, Read, Update and Delete) support implement within our DinnersController class.</span></span>

<span data-ttu-id="9dd53-378">让我们现在看一下如何我们可以使用 ViewData 和 ViewModel 类我们窗体上启用甚至更丰富的 UI。</span><span class="sxs-lookup"><span data-stu-id="9dd53-378">Let's now look at how we can use ViewData and ViewModel classes to enable even richer UI on our forms.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9dd53-379">[上一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [下一页](use-viewdata-and-implement-viewmodel-classes.md)</span><span class="sxs-lookup"><span data-stu-id="9dd53-379">[Previous](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
[Next](use-viewdata-and-implement-viewmodel-classes.md)</span></span>
