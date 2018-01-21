---
title: "依赖关系注入到视图"
author: ardalis
description: 
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/dependency-injection
ms.openlocfilehash: cade61b1ebdb2b845b07117384475638c0227f7f
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="dependency-injection-into-views"></a><span data-ttu-id="31e3c-102">依赖关系注入到视图</span><span class="sxs-lookup"><span data-stu-id="31e3c-102">Dependency injection into views</span></span>

<span data-ttu-id="31e3c-103">通过[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="31e3c-103">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="31e3c-104">ASP.NET 核心支持[依赖关系注入](xref:fundamentals/dependency-injection)到视图。</span><span class="sxs-lookup"><span data-stu-id="31e3c-104">ASP.NET Core supports [dependency injection](xref:fundamentals/dependency-injection) into views.</span></span> <span data-ttu-id="31e3c-105">这可用于查看特定服务，例如本地化或仅对填充视图元素是必需的数据。</span><span class="sxs-lookup"><span data-stu-id="31e3c-105">This can be useful for view-specific services, such as localization or data required only for populating view elements.</span></span> <span data-ttu-id="31e3c-106">你应尝试维护[关注点分离](http://deviq.com/separation-of-concerns/)之间控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="31e3c-106">You should try to maintain [separation of concerns](http://deviq.com/separation-of-concerns/) between your controllers and views.</span></span> <span data-ttu-id="31e3c-107">您的视图显示的数据的大多数应传递在中，从控制器中。</span><span class="sxs-lookup"><span data-stu-id="31e3c-107">Most of the data your views display should be passed in from the controller.</span></span>

<span data-ttu-id="31e3c-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/dependency-injection/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="31e3c-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/dependency-injection/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="a-simple-example"></a><span data-ttu-id="31e3c-109">一个简单的示例</span><span class="sxs-lookup"><span data-stu-id="31e3c-109">A Simple Example</span></span>

<span data-ttu-id="31e3c-110">你可以将服务注入到视图使用`@inject`指令。</span><span class="sxs-lookup"><span data-stu-id="31e3c-110">You can inject a service into a view using the `@inject` directive.</span></span> <span data-ttu-id="31e3c-111">你可以将`@inject`作为将属性添加到你的视图，并填充使用 DI 的属性。</span><span class="sxs-lookup"><span data-stu-id="31e3c-111">You can think of `@inject` as adding a property to your view, and populating the property using DI.</span></span>

<span data-ttu-id="31e3c-112">语法`@inject`:`@inject <type> <name>`</span><span class="sxs-lookup"><span data-stu-id="31e3c-112">The syntax for `@inject`: `@inject <type> <name>`</span></span>

<span data-ttu-id="31e3c-113">一个示例`@inject`中操作：</span><span class="sxs-lookup"><span data-stu-id="31e3c-113">An example of `@inject` in action:</span></span>

[!code-csharp[Main](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Views/ToDo/Index.cshtml?highlight=4,5,15,16,17)]

<span data-ttu-id="31e3c-114">此视图显示的列表`ToDoItem`实例，以及显示总体统计信息的摘要。</span><span class="sxs-lookup"><span data-stu-id="31e3c-114">This view displays a list of `ToDoItem` instances, along with a summary showing overall statistics.</span></span> <span data-ttu-id="31e3c-115">填充摘要从插入`StatisticsService`。</span><span class="sxs-lookup"><span data-stu-id="31e3c-115">The summary is populated from the injected `StatisticsService`.</span></span> <span data-ttu-id="31e3c-116">此服务注册中的依赖关系注入`ConfigureServices`中*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="31e3c-116">This service is registered for dependency injection in `ConfigureServices` in *Startup.cs*:</span></span>

[!code-csharp[Main](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Startup.cs?highlight=6,7&range=15-22)]

<span data-ttu-id="31e3c-117">`StatisticsService`的一套中执行某些计算`ToDoItem`实例，它通过存储库访问：</span><span class="sxs-lookup"><span data-stu-id="31e3c-117">The `StatisticsService` performs some calculations on the set of `ToDoItem` instances, which it accesses via a repository:</span></span>

[!code-csharp[Main](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Model/Services/StatisticsService.cs?highlight=15,20,26)]

<span data-ttu-id="31e3c-118">示例存储库使用的内存中集合。</span><span class="sxs-lookup"><span data-stu-id="31e3c-118">The sample repository uses an in-memory collection.</span></span> <span data-ttu-id="31e3c-119">上面所示的实现 （运行所有内存中的数据上） 不建议用于大、 远程访问数据集。</span><span class="sxs-lookup"><span data-stu-id="31e3c-119">The implementation shown above (which operates on all of the data in memory) is not recommended for large, remotely accessed data sets.</span></span>

<span data-ttu-id="31e3c-120">该示例显示绑定到此视图的模型和视图中注入服务中的数据：</span><span class="sxs-lookup"><span data-stu-id="31e3c-120">The sample displays data from the model bound to the view and the service injected into the view:</span></span>

![若要查看列出总的项，完成项、 平均优先级别和使用其优先级别和布尔值，用于指示完成任务的列表。](dependency-injection/_static/screenshot.png)

## <a name="populating-lookup-data"></a><span data-ttu-id="31e3c-122">填充查找数据</span><span class="sxs-lookup"><span data-stu-id="31e3c-122">Populating Lookup Data</span></span>

<span data-ttu-id="31e3c-123">视图注入可用于填充用户界面元素，如下拉列表中的选项。</span><span class="sxs-lookup"><span data-stu-id="31e3c-123">View injection can be useful to populate options in UI elements, such as dropdown lists.</span></span> <span data-ttu-id="31e3c-124">请考虑用户配置文件窗体，其中包含用于指定性别、 状态和其他首选项的选项。</span><span class="sxs-lookup"><span data-stu-id="31e3c-124">Consider a user profile form that includes options for specifying gender, state, and other preferences.</span></span> <span data-ttu-id="31e3c-125">呈现表单使用标准的 MVC 方法需要控制器来请求每个选项，这些组的数据访问服务，然后填充模型，或`ViewBag`与每个组的选项来绑定。</span><span class="sxs-lookup"><span data-stu-id="31e3c-125">Rendering such a form using a standard MVC approach would require the controller to request data access services for each of these sets of options, and then populate a model or `ViewBag` with each set of options to be bound.</span></span>

<span data-ttu-id="31e3c-126">另一种方法直接将服务注入视图以获取选项。</span><span class="sxs-lookup"><span data-stu-id="31e3c-126">An alternative approach injects services directly into the view to obtain the options.</span></span> <span data-ttu-id="31e3c-127">这将减少所需的控制器上，将此视图元素构造逻辑移入视图本身的代码量。</span><span class="sxs-lookup"><span data-stu-id="31e3c-127">This minimizes the amount of code required by the controller, moving this view element construction logic into the view itself.</span></span> <span data-ttu-id="31e3c-128">要显示的配置文件编辑窗体的控制器操作只需将配置文件实例传递窗体：</span><span class="sxs-lookup"><span data-stu-id="31e3c-128">The controller action to display a profile editing form only needs to pass the form the profile instance:</span></span>

[!code-csharp[Main](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Controllers/ProfileController.cs?highlight=9,19)]

<span data-ttu-id="31e3c-129">用于更新这些首选项的 HTML 窗体包括有关三个属性的下拉列表中：</span><span class="sxs-lookup"><span data-stu-id="31e3c-129">The HTML form used to update these preferences includes dropdown lists for three of the properties:</span></span>

![更新配置文件视图与窗体允许的名称、 性别、 状态和喜爱的颜色的条目。](dependency-injection/_static/updateprofile.png)

<span data-ttu-id="31e3c-131">这些列表是通过注入视图的服务来填充：</span><span class="sxs-lookup"><span data-stu-id="31e3c-131">These lists are populated by a service that has been injected into the view:</span></span>

[!code-csharp[Main](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Views/Profile/Index.cshtml?highlight=4,16,17,21,22,26,27)]

<span data-ttu-id="31e3c-132">`ProfileOptionsService`是 UI 级服务，旨在提供所需的此窗体数据：</span><span class="sxs-lookup"><span data-stu-id="31e3c-132">The `ProfileOptionsService` is a UI-level service designed to provide just the data needed for this form:</span></span>

[!code-csharp[Main](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Model/Services/ProfileOptionsService.cs?highlight=7,13,24)]

>[!TIP]
> <span data-ttu-id="31e3c-133">不要忘记将注册的类型将请求中的依赖关系注入通过`ConfigureServices`中的方法*Startup.cs*。</span><span class="sxs-lookup"><span data-stu-id="31e3c-133">Don't forget to register types you will request through dependency injection in the  `ConfigureServices` method in *Startup.cs*.</span></span>

## <a name="overriding-services"></a><span data-ttu-id="31e3c-134">重写服务</span><span class="sxs-lookup"><span data-stu-id="31e3c-134">Overriding Services</span></span>

<span data-ttu-id="31e3c-135">除了将注入新服务，此方法还可以使用重写以前插入的页面上的服务。</span><span class="sxs-lookup"><span data-stu-id="31e3c-135">In addition to injecting new services, this technique can also be used to override previously injected services on a page.</span></span> <span data-ttu-id="31e3c-136">下图显示的所有可用字段在第一个示例中使用的页上：</span><span class="sxs-lookup"><span data-stu-id="31e3c-136">The figure below shows all of the fields available on the page used in the first example:</span></span>

![在类型化 Intellisense 上下文菜单中的 @ 符号列出 Html，组件、 StatsService，和 Url 字段](dependency-injection/_static/razor-fields.png)

<span data-ttu-id="31e3c-138">如你所见，包括默认字段`Html`， `Component`，和`Url`(以及`StatsService`我们插入)。</span><span class="sxs-lookup"><span data-stu-id="31e3c-138">As you can see, the default fields include `Html`, `Component`, and `Url` (as well as the `StatsService` that we injected).</span></span> <span data-ttu-id="31e3c-139">如果实例，你想要将替换为你自己的默认 HTML 帮助器，则可以轻松地执行因此使用`@inject`:</span><span class="sxs-lookup"><span data-stu-id="31e3c-139">If for instance you wanted to replace the default HTML Helpers with your own, you could easily do so using `@inject`:</span></span>

[!code-html[Main](../../mvc/views/dependency-injection/sample/src/ViewInjectSample/Views/Helper/Index.cshtml?highlight=3,11)]

<span data-ttu-id="31e3c-140">如果你想要扩展现有的服务，可以在继承自或包装的现有实现替换为你自己时只需使用此方法。</span><span class="sxs-lookup"><span data-stu-id="31e3c-140">If you want to extend existing services, you can simply use this technique while inheriting from or wrapping the existing implementation with your own.</span></span>

## <a name="see-also"></a><span data-ttu-id="31e3c-141">请参阅</span><span class="sxs-lookup"><span data-stu-id="31e3c-141">See Also</span></span>

* <span data-ttu-id="31e3c-142">人 Simon Timms 博客：[使查找数据进入你的视图](http://blog.simontimms.com/2015/06/09/getting-lookup-data-into-you-view/)</span><span class="sxs-lookup"><span data-stu-id="31e3c-142">Simon Timms Blog: [Getting Lookup Data Into Your View](http://blog.simontimms.com/2015/06/09/getting-lookup-data-into-you-view/)</span></span>
