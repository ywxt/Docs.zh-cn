---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
title: 向模型添加验证 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 5d9a2999-fcc4-4c45-a018-271fddf74a3b
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 47c3f16d4592d2f61c6f1c3c1988e3622cb84a00
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384798"
---
<a name="adding-validation-to-the-model"></a><span data-ttu-id="32c45-104">向模型添加验证</span><span class="sxs-lookup"><span data-stu-id="32c45-104">Adding Validation to the Model</span></span>
====================
<span data-ttu-id="32c45-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="32c45-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="32c45-106">本教程中的更新的版本是可用[此处](../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="32c45-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="32c45-107">它是更安全、 更易于遵循，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="32c45-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="32c45-108">在本部分中，你将添加到的验证逻辑`Movie`模型，并确保每次用户尝试创建或编辑电影使用应用程序时，强制的验证规则。</span><span class="sxs-lookup"><span data-stu-id="32c45-108">In this section you'll add validation logic to the `Movie` model, and you'll ensure that the validation rules are enforced any time a user attempts to create or edit a movie using the application.</span></span>

## <a name="keeping-things-dry"></a><span data-ttu-id="32c45-109">DRY 地保管东西</span><span class="sxs-lookup"><span data-stu-id="32c45-109">Keeping Things DRY</span></span>

<span data-ttu-id="32c45-110">ASP.NET MVC 的核心设计原则之一是 DRY (&quot;不要自我重复&quot;)。</span><span class="sxs-lookup"><span data-stu-id="32c45-110">One of the core design tenets of ASP.NET MVC is DRY (&quot;Don't Repeat Yourself&quot;).</span></span> <span data-ttu-id="32c45-111">ASP.NET MVC 支持你指定的功能或行为只有一次，然后让它应用到整个应用程序中。</span><span class="sxs-lookup"><span data-stu-id="32c45-111">ASP.NET MVC encourages you to specify functionality or behavior only once, and then have it be reflected everywhere in an application.</span></span> <span data-ttu-id="32c45-112">这可以减少需要编写的代码量，并使您编写更少容易出错且更易于维护的代码。</span><span class="sxs-lookup"><span data-stu-id="32c45-112">This reduces the amount of code you need to write and makes the code you do write less error prone and easier to maintain.</span></span>

<span data-ttu-id="32c45-113">由 ASP.NET MVC 和 Entity Framework Code First 提供的验证支持是 DRY 原则在操作中的一个极好示例。</span><span class="sxs-lookup"><span data-stu-id="32c45-113">The validation support provided by ASP.NET MVC and Entity Framework Code First is a great example of the DRY principle in action.</span></span> <span data-ttu-id="32c45-114">在一个位置 （在模型类中） 以声明方式指定验证规则和规则所有位置强制执行应用程序中。</span><span class="sxs-lookup"><span data-stu-id="32c45-114">You can declaratively specify validation rules in one place (in the model class) and the rules are enforced everywhere in the application.</span></span>

<span data-ttu-id="32c45-115">让我们看看电影应用程序中，您就可以充分利用此验证支持。</span><span class="sxs-lookup"><span data-stu-id="32c45-115">Let's look at how you can take advantage of this validation support in the movie application.</span></span>

## <a name="adding-validation-rules-to-the-movie-model"></a><span data-ttu-id="32c45-116">向电影模型添加验证规则</span><span class="sxs-lookup"><span data-stu-id="32c45-116">Adding Validation Rules to the Movie Model</span></span>

<span data-ttu-id="32c45-117">您将首先添加到某些验证逻辑`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="32c45-117">You'll begin by adding some validation logic to the `Movie` class.</span></span>

<span data-ttu-id="32c45-118">打开 Movie.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="32c45-118">Open the *Movie.cs* file.</span></span> <span data-ttu-id="32c45-119">添加`using`语句引用的文件的顶部[ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间：</span><span class="sxs-lookup"><span data-stu-id="32c45-119">Add a `using` statement at the top of the file that references the [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

<span data-ttu-id="32c45-120">请注意，命名空间不包含`System.Web`。</span><span class="sxs-lookup"><span data-stu-id="32c45-120">Notice the namespace does not contain `System.Web`.</span></span> <span data-ttu-id="32c45-121">DataAnnotations 提供一组内置验证特性，可以以声明方式应用于任何类或属性。</span><span class="sxs-lookup"><span data-stu-id="32c45-121">DataAnnotations provides a built-in set of validation attributes that you can apply declaratively to any class or property.</span></span>

<span data-ttu-id="32c45-122">现在，更新`Movie`类，以充分利用内置[ `Required` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)， [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)，并且[ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)验证特性.</span><span class="sxs-lookup"><span data-stu-id="32c45-122">Now update the `Movie` class to take advantage of the built-in [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), and [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) validation attributes.</span></span> <span data-ttu-id="32c45-123">使用以下代码作为应用特性的位置的示例。</span><span class="sxs-lookup"><span data-stu-id="32c45-123">Use the following code as an example of where to apply the attributes.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs?highlight=4,10,13,17)]

<span data-ttu-id="32c45-124">运行应用程序，则也会收到以下运行的时错误：</span><span class="sxs-lookup"><span data-stu-id="32c45-124">Run the application and you will again get the following run time error:</span></span>

<span data-ttu-id="32c45-125">***创建数据库后，支持 MovieDBContext 上下文的模型已更改。请考虑使用 Code First 迁移来更新数据库 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269))。***</span><span class="sxs-lookup"><span data-stu-id="32c45-125">***The model backing the 'MovieDBContext' context has changed since the database was created. Consider using Code First Migrations to update the database ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).***</span></span>

<span data-ttu-id="32c45-126">我们将使用迁移来更新架构。</span><span class="sxs-lookup"><span data-stu-id="32c45-126">We will use migrations to update the schema.</span></span> <span data-ttu-id="32c45-127">生成解决方案，然后打开**程序包管理器控制台**窗口并输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="32c45-127">Build the solution, and then open the **Package Manager Console** window and enter the following commands:</span></span>

[!code-console[Main](adding-validation-to-the-model/samples/sample3.cmd)]

<span data-ttu-id="32c45-128">此命令完成后，Visual Studio 会打开定义新的类文件`DbMIgration`派生类指定的名称 (*AddDataAnnotationsMig*)，然后在`Up`方法您可以看到更新的代码架构的约束。</span><span class="sxs-lookup"><span data-stu-id="32c45-128">When this command finishes, Visual Studio opens the class file that defines the new `DbMIgration` derived class with the name specified (*AddDataAnnotationsMig*), and in the `Up` method you can see the code that updates the schema constraints.</span></span> <span data-ttu-id="32c45-129">`Title`并`Genre`字段不再可以为 null （即，您必须输入一个值） 和`Rating`字段具有最大长度为 5。</span><span class="sxs-lookup"><span data-stu-id="32c45-129">The `Title` and `Genre` fields are no longer nullable (that is, you must enter a value) and the `Rating` field has a maximum length of 5.</span></span>

<span data-ttu-id="32c45-130">验证特性指定要对应用这些特性的模型属性强制执行的行为。</span><span class="sxs-lookup"><span data-stu-id="32c45-130">The validation attributes specify behavior that you want to enforce on the model properties they are applied to.</span></span> <span data-ttu-id="32c45-131">`Required`属性指示属性必须具有一个值; 在此示例中，电影已具有值`Title`， `ReleaseDate`， `Genre`，和`Price`属性才有效。</span><span class="sxs-lookup"><span data-stu-id="32c45-131">The `Required` attribute indicates that a property must have a value; in this sample, a movie has to have values for the `Title`, `ReleaseDate`, `Genre`, and `Price` properties in order to be valid.</span></span> <span data-ttu-id="32c45-132">`Range` 特性将值限制在指定范围内。</span><span class="sxs-lookup"><span data-stu-id="32c45-132">The `Range` attribute constrains a value to within a specified range.</span></span> <span data-ttu-id="32c45-133">`StringLength` 特性使你能够设置字符串属性的最大长度，以及可选的最小长度。</span><span class="sxs-lookup"><span data-stu-id="32c45-133">The `StringLength` attribute lets you set the maximum length of a string property, and optionally its minimum length.</span></span> <span data-ttu-id="32c45-134">内部类型 (如`decimal, int, float, DateTime`) 所需的默认值，而无须`Required`属性。</span><span class="sxs-lookup"><span data-stu-id="32c45-134">Intrinsic types (such as `decimal, int, float, DateTime`) are required by default and don't need the `Required` attribute.</span></span>

<span data-ttu-id="32c45-135">代码首先确保之前应用程序将更改保存在数据库中实施的 model 类指定的验证规则。</span><span class="sxs-lookup"><span data-stu-id="32c45-135">Code First ensures that the validation rules you specify on a model class are enforced before the application saves changes in the database.</span></span> <span data-ttu-id="32c45-136">例如，下面的代码将引发异常时`SaveChanges`调用方法，因为所需的几个`Movie`缺少属性值，价格为零 （即不在有效范围内）。</span><span class="sxs-lookup"><span data-stu-id="32c45-136">For example, the code below will throw an exception when the `SaveChanges` method is called, because several required `Movie` property values are missing and the price is zero (which is out of the valid range).</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs?highlight=7-8)]

<span data-ttu-id="32c45-137">具有自动强制执行由.NET Framework 的验证规则有助于使您的应用程序更可靠。</span><span class="sxs-lookup"><span data-stu-id="32c45-137">Having validation rules automatically enforced by the .NET Framework helps make your application more robust.</span></span> <span data-ttu-id="32c45-138">同时它能确保你无法忘记验证某些内容，并防止你无意中将错误数据导入数据库。</span><span class="sxs-lookup"><span data-stu-id="32c45-138">It also ensures that you can't forget to validate something and inadvertently let bad data into the database.</span></span>

<span data-ttu-id="32c45-139">以下是列出了已更新的完整代码*Movie.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="32c45-139">Here's a complete code listing for the updated *Movie.cs* file:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a><span data-ttu-id="32c45-140">验证错误在 ASP.NET MVC 中的 UI</span><span class="sxs-lookup"><span data-stu-id="32c45-140">Validation Error UI in ASP.NET MVC</span></span>

<span data-ttu-id="32c45-141">重新运行该应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="32c45-141">Re-run the application and navigate to the */Movies* URL.</span></span>

<span data-ttu-id="32c45-142">单击**创建新**链接以添加新电影。</span><span class="sxs-lookup"><span data-stu-id="32c45-142">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="32c45-143">填写表单的某些无效的值，然后单击**创建**按钮。</span><span class="sxs-lookup"><span data-stu-id="32c45-143">Fill out the form with some invalid values and then click the **Create** button.</span></span>

![8_validationErrors](adding-validation-to-the-model/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="32c45-145">若要支持 jQuery 验证的非英语区域设置，请使用逗号 (&quot;，&quot;) 必须包含小数点， *globalize.js*和您的特定*cultures/globalize.cultures.js*文件 (从[ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 和 JavaScript 使用`Globalize.parseFloat`。</span><span class="sxs-lookup"><span data-stu-id="32c45-145">to support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="32c45-146">下面的代码演示对 Views\Movies\Edit.cshtml 文件用于修改&quot;-FR&quot;区域性：</span><span class="sxs-lookup"><span data-stu-id="32c45-146">The following code shows the modifications to the Views\Movies\Edit.cshtml file to work with the &quot;fr-FR&quot; culture:</span></span>


[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

<span data-ttu-id="32c45-147">请注意如何在窗体具有自动使用红色边框颜色突出显示的文本框包含无效的数据和已发出每个适当的验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="32c45-147">Notice how the form has automatically used a red border color to highlight the text boxes that contain invalid data and has emitted an appropriate validation error message next to each one.</span></span> <span data-ttu-id="32c45-148">客户端（使用 JavaScript 和 jQuery）和服务器端（若用户禁用 JavaScript）都必定会遇到这些错误。</span><span class="sxs-lookup"><span data-stu-id="32c45-148">The errors are enforced both client-side (using JavaScript and jQuery) and server-side (in case a user has JavaScript disabled).</span></span>

<span data-ttu-id="32c45-149">一个实际优点是不需要更改任何一行中的代码`MoviesController`类中或在*Create.cshtml*来启用此验证 UI 的视图。</span><span class="sxs-lookup"><span data-stu-id="32c45-149">A real benefit is that you didn't need to change a single line of code in the `MoviesController` class or in the *Create.cshtml* view in order to enable this validation UI.</span></span> <span data-ttu-id="32c45-150">在本教程前面创建的控制器和视图会自动选取验证规则，这些规则是通过在 `Movie` 模型类的属性上使用验证特性所指定的。</span><span class="sxs-lookup"><span data-stu-id="32c45-150">The controller and views you created earlier in this tutorial automatically picked up the validation rules that you specified by using validation attributes on the properties of the `Movie` model class.</span></span>

<span data-ttu-id="32c45-151">您可能已经注意到的属性`Title`并`Genre`，不强制执行所需的属性，直到在提交表单 (命中**创建**按钮)，或输入字段中输入文本并将其删除。</span><span class="sxs-lookup"><span data-stu-id="32c45-151">You might have noticed for the properties `Title` and `Genre`, the required attribute is not enforced until you submit the form (hit the **Create** button), or enter text into the input field and removed it.</span></span> <span data-ttu-id="32c45-152">字段即最初为空 （如 Create 视图上的字段），并且具有所需的属性和任何其他验证属性，可以执行以下操作来触发验证：</span><span class="sxs-lookup"><span data-stu-id="32c45-152">For a field which is initially empty (such as the fields on the Create view) and which has only the required attribute and no other validation attributes, you can do the following to trigger validation:</span></span>

1. <span data-ttu-id="32c45-153">字段中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="32c45-153">Tab into the field.</span></span>
2. <span data-ttu-id="32c45-154">输入一些文本。</span><span class="sxs-lookup"><span data-stu-id="32c45-154">Enter some text.</span></span>
3. <span data-ttu-id="32c45-155">退出选项卡。</span><span class="sxs-lookup"><span data-stu-id="32c45-155">Tab out.</span></span>
4. <span data-ttu-id="32c45-156">返回到该字段的选项卡。</span><span class="sxs-lookup"><span data-stu-id="32c45-156">Tab back into the field.</span></span>
5. <span data-ttu-id="32c45-157">删除的文本。</span><span class="sxs-lookup"><span data-stu-id="32c45-157">Remove the text.</span></span>
6. <span data-ttu-id="32c45-158">退出选项卡。</span><span class="sxs-lookup"><span data-stu-id="32c45-158">Tab out.</span></span>

<span data-ttu-id="32c45-159">上面的顺序将触发所需的验证，而不会达到提交按钮。</span><span class="sxs-lookup"><span data-stu-id="32c45-159">The above sequence will trigger the required validation without hitting the submit button.</span></span> <span data-ttu-id="32c45-160">只需点击提交按钮而无需输入的任何字段都将触发客户端验证。</span><span class="sxs-lookup"><span data-stu-id="32c45-160">Simply hitting the submit button without entering any of the fields will trigger client side validation.</span></span> <span data-ttu-id="32c45-161">存在客户端验证错误时，不会将表单数据发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="32c45-161">The form data is not sent to the server until there are no client side validation errors.</span></span> <span data-ttu-id="32c45-162">可以通过 HTTP Post 方法中放置一个断点或使用测试这[fiddler 工具](http://fiddler2.com/fiddler2/)或 IE 9 [F12 开发人员工具](https://msdn.microsoft.com/ie/aa740478)。</span><span class="sxs-lookup"><span data-stu-id="32c45-162">You can test this by putting a break point in the HTTP Post method or using the [fiddler tool](http://fiddler2.com/fiddler2/) or the IE 9 [F12 developer tools](https://msdn.microsoft.com/ie/aa740478).</span></span>

![](adding-validation-to-the-model/_static/image2.png)

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a><span data-ttu-id="32c45-163">如何在中进行验证创建查看和创建操作方法</span><span class="sxs-lookup"><span data-stu-id="32c45-163">How Validation Occurs in the Create View and Create Action Method</span></span>

<span data-ttu-id="32c45-164">你可能想知道在不对控制器或视图中的代码进行任何更新的情况下，验证 UI 是如何生成的。</span><span class="sxs-lookup"><span data-stu-id="32c45-164">You might wonder how the validation UI was generated without any updates to the code in the controller or views.</span></span> <span data-ttu-id="32c45-165">下一步列表显示什么`Create`中的方法`MovieController`类看起来像。</span><span class="sxs-lookup"><span data-stu-id="32c45-165">The next listing shows what the `Create` methods in the `MovieController` class look like.</span></span> <span data-ttu-id="32c45-166">它们是如何在本教程前面创建它们相比没有变化。</span><span class="sxs-lookup"><span data-stu-id="32c45-166">They're unchanged from how you created them earlier in this tutorial.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs?highlight=12,15)]

<span data-ttu-id="32c45-167">第一个 (HTTP GET) `Create` 操作方法显示初始的“创建”表单。</span><span class="sxs-lookup"><span data-stu-id="32c45-167">The first (HTTP GET) `Create` action method displays the initial Create form.</span></span> <span data-ttu-id="32c45-168">第二个 (`[HttpPost]`) 版本处理表单发布。</span><span class="sxs-lookup"><span data-stu-id="32c45-168">The second (`[HttpPost]`) version handles the form post.</span></span> <span data-ttu-id="32c45-169">第二个 `Create` 方法（`HttpPost` 版本）调用 `ModelState.IsValid` 以检查电影是否有任何验证错误。</span><span class="sxs-lookup"><span data-stu-id="32c45-169">The second `Create` method (The `HttpPost` version) calls `ModelState.IsValid` to check whether the movie has any validation errors.</span></span> <span data-ttu-id="32c45-170">调用此方法将评估已应用于对象的任何验证特性。</span><span class="sxs-lookup"><span data-stu-id="32c45-170">Calling this method evaluates any validation attributes that have been applied to the object.</span></span> <span data-ttu-id="32c45-171">如果对象有验证错误，则 `Create` 方法会重新显示此表单。</span><span class="sxs-lookup"><span data-stu-id="32c45-171">If the object has validation errors, the `Create` method re-displays the form.</span></span> <span data-ttu-id="32c45-172">如果没有错误，此方法则将新电影保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="32c45-172">If there are no errors, the method saves the new movie in the database.</span></span> <span data-ttu-id="32c45-173">在我们的电影示例中我们将使用**窗体不会发布到服务器时有验证错误在客户端; 上检测到第二个** `Create`**永远不会调用方法**。</span><span class="sxs-lookup"><span data-stu-id="32c45-173">In our movie example we are using, **the form is not posted to the server when their are validation errors detected on the client side; the second** `Create`**method is never called**.</span></span> <span data-ttu-id="32c45-174">如果在浏览器中禁用 JavaScript，请禁用客户端验证和 HTTP POST`Create`方法调用`ModelState.IsValid`检查电影是否有任何验证错误。</span><span class="sxs-lookup"><span data-stu-id="32c45-174">If you disable JavaScript in your browser, client validation is disabled and the HTTP POST `Create` method calls `ModelState.IsValid` to check whether the movie has any validation errors.</span></span>

<span data-ttu-id="32c45-175">可以在 `HttpPost Create` 方法中设置断点，并验证方法从未被调用，客户端验证在检测到存在验证错误时不会提交表单数据。</span><span class="sxs-lookup"><span data-stu-id="32c45-175">You can set a break point in the `HttpPost Create` method and verify the method is never called, client side validation will not submit the form data when validation errors are detected.</span></span> <span data-ttu-id="32c45-176">如果在浏览器中禁用 JavaScript，然后提交错误的表单，将触发断点。</span><span class="sxs-lookup"><span data-stu-id="32c45-176">If you disable JavaScript in your browser, then submit the form with errors, the break point will be hit.</span></span> <span data-ttu-id="32c45-177">在没有 JavaScript 的情况下仍然可以进行完整的验证。</span><span class="sxs-lookup"><span data-stu-id="32c45-177">You still get full validation without JavaScript.</span></span> <span data-ttu-id="32c45-178">下图显示了如何禁用 Internet Explorer 中的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="32c45-178">The following image shows how to disable JavaScript in Internet Explorer.</span></span>

![](adding-validation-to-the-model/_static/image3.png)

![](adding-validation-to-the-model/_static/image4.png)

<span data-ttu-id="32c45-179">以下图片显示如何在 FireFox 浏览器中禁用 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="32c45-179">The following image shows how to disable JavaScript in the FireFox browser.</span></span>

![](adding-validation-to-the-model/_static/image5.png)

<span data-ttu-id="32c45-180">下图显示了如何使用 Chrome 浏览器中禁用 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="32c45-180">The following image shows how to disable JavaScript with the Chrome browser.</span></span>

![](adding-validation-to-the-model/_static/image6.png)

<span data-ttu-id="32c45-181">下面是*Create.cshtml*基架在本教程前面部分中的视图模板。</span><span class="sxs-lookup"><span data-stu-id="32c45-181">Below is the *Create.cshtml* view template that you scaffolded earlier in the tutorial.</span></span> <span data-ttu-id="32c45-182">以上所示的操作方法使用它来显示初始表单，并在发生错误时重新显示此表单。</span><span class="sxs-lookup"><span data-stu-id="32c45-182">It's used by the action methods shown above both to display the initial form and to redisplay it in the event of an error.</span></span>

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample8.cshtml?highlight=22-23,30-31,38-39,46-47)]

<span data-ttu-id="32c45-183">请注意代码如何使用`Html.EditorFor`帮助器输出`<input>`每个元素`Movie`属性。</span><span class="sxs-lookup"><span data-stu-id="32c45-183">Notice how the code uses an `Html.EditorFor` helper to output the `<input>` element for each `Movie` property.</span></span> <span data-ttu-id="32c45-184">此帮助器旁边是对的调用`Html.ValidationMessageFor`帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="32c45-184">Next to this helper is a call to the `Html.ValidationMessageFor` helper method.</span></span> <span data-ttu-id="32c45-185">这两个帮助器方法使用由控制器传递给视图的模型对象 (在这种情况下，`Movie`对象)。</span><span class="sxs-lookup"><span data-stu-id="32c45-185">These two helper methods work with the model object that's passed by the controller to the view (in this case, a `Movie` object).</span></span> <span data-ttu-id="32c45-186">它们会自动查找适当的模型和显示错误消息中指定的验证特性。</span><span class="sxs-lookup"><span data-stu-id="32c45-186">They automatically look for validation attributes specified on the model and display error messages as appropriate.</span></span>

<span data-ttu-id="32c45-187">有关此方法非常令人愉快的是，在控制器和创建视图模板都不知道任何有关强制实施的实际验证规则或显示的特定错误消息。</span><span class="sxs-lookup"><span data-stu-id="32c45-187">What's really nice about this approach is that neither the controller nor the Create view template knows anything about the actual validation rules being enforced or about the specific error messages displayed.</span></span> <span data-ttu-id="32c45-188">仅可在 `Movie` 类中指定验证规则和错误字符串。</span><span class="sxs-lookup"><span data-stu-id="32c45-188">The validation rules and the error strings are specified only in the `Movie` class.</span></span> <span data-ttu-id="32c45-189">这些相同的验证规则自动应用于编辑视图和任何其他视图模板可能会创建用于编辑模型中。</span><span class="sxs-lookup"><span data-stu-id="32c45-189">These same validation rules are automatically applied to the Edit view and any other views templates you might create that edit your model.</span></span>

<span data-ttu-id="32c45-190">如果你想要以后更改验证逻辑，就可以做到在同一个位置通过向模型添加验证特性 (在此示例中，`movie`类)。</span><span class="sxs-lookup"><span data-stu-id="32c45-190">If you want to change the validation logic later, you can do so in exactly one place by adding validation attributes to the model (in this example, the `movie` class).</span></span> <span data-ttu-id="32c45-191">无需担心对应用程序的不同部分所强制执行规则的方式不一致 - 所有验证逻辑都将定义在一个位置并用于整个应用程序。</span><span class="sxs-lookup"><span data-stu-id="32c45-191">You won't have to worry about different parts of the application being inconsistent with how the rules are enforced — all validation logic will be defined in one place and used everywhere.</span></span> <span data-ttu-id="32c45-192">这使代码非常简洁，并且更易于维护和改进。</span><span class="sxs-lookup"><span data-stu-id="32c45-192">This keeps the code very clean, and makes it easy to maintain and evolve.</span></span> <span data-ttu-id="32c45-193">这意味着对 DRY 原则的完全遵守。</span><span class="sxs-lookup"><span data-stu-id="32c45-193">And it means that you'll be fully honoring the DRY principle.</span></span>

## <a name="adding-formatting-to-the-movie-model"></a><span data-ttu-id="32c45-194">将格式添加到电影模型</span><span class="sxs-lookup"><span data-stu-id="32c45-194">Adding Formatting to the Movie Model</span></span>

<span data-ttu-id="32c45-195">打开 Movie.cs 文件并检查 `Movie` 类。</span><span class="sxs-lookup"><span data-stu-id="32c45-195">Open the *Movie.cs* file and examine the `Movie` class.</span></span> <span data-ttu-id="32c45-196">[ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间提供除了一组内置验证特性的格式设置属性。</span><span class="sxs-lookup"><span data-stu-id="32c45-196">The [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provides formatting attributes in addition to the built-in set of validation attributes.</span></span> <span data-ttu-id="32c45-197">我们已应用[ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)发布日期和价格字段的枚举值。</span><span class="sxs-lookup"><span data-stu-id="32c45-197">We've already applied a [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) enumeration value to the release date and to the price fields.</span></span> <span data-ttu-id="32c45-198">下面的代码演示`ReleaseDate`并`Price`具有适当[ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="32c45-198">The following code shows the `ReleaseDate` and `Price` properties with the appropriate [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

<span data-ttu-id="32c45-199">[ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性不是验证特性，它们用于告知如何呈现的 HTML 的视图引擎。</span><span class="sxs-lookup"><span data-stu-id="32c45-199">The [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attributes are not validation attributes, they are used to tell the view engine how to render the HTML.</span></span> <span data-ttu-id="32c45-200">在上述示例中，`DataType.Date`属性不包括时间显示为日期，电影日期。</span><span class="sxs-lookup"><span data-stu-id="32c45-200">In the example above, the `DataType.Date` attribute displays the movie dates as dates only, without time.</span></span> <span data-ttu-id="32c45-201">例如，以下[ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性不验证数据的格式：</span><span class="sxs-lookup"><span data-stu-id="32c45-201">For example, the following [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attributes don't validate the format of the data:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

<span data-ttu-id="32c45-202">上面列出的特性仅提供提示帮助视图引擎设置数据的格式 (如提供属性和&lt;&gt; url 并&lt;a =&quot;mailto:EmailAddress.com&quot; &gt;电子邮件。</span><span class="sxs-lookup"><span data-stu-id="32c45-202">The attributes listed above only provide hints for the view engine to format the data (and supply attributes such as &lt;a&gt; for URL's and &lt;a href=&quot;mailto:EmailAddress.com&quot;&gt; for email.</span></span> <span data-ttu-id="32c45-203">可以使用[正则表达式](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)特性验证数据的格式。</span><span class="sxs-lookup"><span data-stu-id="32c45-203">You can use the [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) attribute to validate the format of the data.</span></span>

<span data-ttu-id="32c45-204">一种方法来使用`DataType`属性，您可以显式设置[ `DataFormatString` ](https://msdn.microsoft.com/library/system.string.format.aspx)值。</span><span class="sxs-lookup"><span data-stu-id="32c45-204">An alternative approach to using the `DataType` attributes, you could explicitly set a [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) value.</span></span> <span data-ttu-id="32c45-205">下面的代码演示了日期格式字符串的发行日期属性 (即&quot;d&quot;)。</span><span class="sxs-lookup"><span data-stu-id="32c45-205">The following code shows the release date property with a date format string (namely, &quot;d&quot;).</span></span> <span data-ttu-id="32c45-206">将此位置用于指定你不想为时间发布日期的一部分。</span><span class="sxs-lookup"><span data-stu-id="32c45-206">You'd use this to specify that you don't want to time as part of the release date.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample11.cs)]

<span data-ttu-id="32c45-207">完整`Movie`类如下所示。</span><span class="sxs-lookup"><span data-stu-id="32c45-207">The complete `Movie` class is shown below.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample12.cs)]

<span data-ttu-id="32c45-208">运行应用程序，并浏览到`Movies`控制器。</span><span class="sxs-lookup"><span data-stu-id="32c45-208">Run the application and browse to the `Movies` controller.</span></span> <span data-ttu-id="32c45-209">发布日期和价格可以很好地进行格式化。</span><span class="sxs-lookup"><span data-stu-id="32c45-209">The release date and price are nicely formatted.</span></span> <span data-ttu-id="32c45-210">下图显示的发布日期和使用价格&quot;-FR&quot;与区域性。</span><span class="sxs-lookup"><span data-stu-id="32c45-210">The image below shows the release date and price using &quot;fr-FR&quot; as the culture.</span></span>

![8_format_SM](adding-validation-to-the-model/_static/image7.png)

<span data-ttu-id="32c45-212">下图显示了与默认区域性 （美国英语） 显示的相同数据。</span><span class="sxs-lookup"><span data-stu-id="32c45-212">The image below shows the same data displayed with the default culture (English US).</span></span>

![](adding-validation-to-the-model/_static/image8.png)

<span data-ttu-id="32c45-213">在本系列的下一部分中，我们将回顾应用程序，并对自动生成的 `Details` 和 `Delete` 方法进行一些改进。</span><span class="sxs-lookup"><span data-stu-id="32c45-213">In the next part of the series, we'll review the application and make some improvements to the automatically generated `Details` and `Delete` methods.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="32c45-214">[上一页](adding-a-new-field-to-the-movie-model-and-table.md)
> [下一页](examining-the-details-and-delete-methods.md)</span><span class="sxs-lookup"><span data-stu-id="32c45-214">[Previous](adding-a-new-field-to-the-movie-model-and-table.md)
[Next](examining-the-details-and-delete-methods.md)</span></span>
