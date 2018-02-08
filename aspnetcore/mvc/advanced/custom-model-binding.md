---
title: "自定义模型绑定"
author: ardalis
description: "自定义 ASP.NET Core MVC 中的模型绑定。"
manager: wpickett
ms.author: riande
ms.date: 04/10/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/advanced/custom-model-binding
ms.openlocfilehash: 313bc586a1c313f0bf5d8f413a4b082ffc2b7f0c
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="custom-model-binding"></a><span data-ttu-id="3d8ac-103">自定义模型绑定</span><span class="sxs-lookup"><span data-stu-id="3d8ac-103">Custom Model Binding</span></span>

<span data-ttu-id="3d8ac-104">作者：[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="3d8ac-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="3d8ac-105">通过模型绑定，控制器操作可直接使用模型类型（作为方法参数传入）而不是 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-105">Model binding allows controller actions to work directly with model types (passed in as method arguments), rather than HTTP requests.</span></span> <span data-ttu-id="3d8ac-106">由模型绑定器处理传入的请求数据和应用程序模型之间的映射。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-106">Mapping between incoming request data and application models is handled by model binders.</span></span> <span data-ttu-id="3d8ac-107">开发人员可以通过实现自定义模型绑定器来扩展内置的模型绑定功能（尽管通常不需要编写自己的提供程序）。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-107">Developers can extend the built-in model binding functionality by implementing custom model binders (though typically, you don't need to write your own provider).</span></span>

[<span data-ttu-id="3d8ac-108">查看或下载 GitHub 中的示例</span><span class="sxs-lookup"><span data-stu-id="3d8ac-108">View or download sample from GitHub</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-model-binding/)

## <a name="default-model-binder-limitations"></a><span data-ttu-id="3d8ac-109">默认模型绑定器限制</span><span class="sxs-lookup"><span data-stu-id="3d8ac-109">Default model binder limitations</span></span>

<span data-ttu-id="3d8ac-110">默认模型绑定器支持大多数常见的 .NET Core 数据类型，能够满足大部分开发人员的需求。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-110">The default model binders support most of the common .NET Core data types and should meet most developers\` needs.</span></span> <span data-ttu-id="3d8ac-111">他们希望将基于文本的输入从请求直接绑定到模型类型。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-111">They expect to bind text-based input from the request directly to model types.</span></span> <span data-ttu-id="3d8ac-112">绑定输入之前，可能需要对其进行转换。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-112">You might need to transform the input prior to binding it.</span></span> <span data-ttu-id="3d8ac-113">例如，当拥有某个可以用来查找模型数据的键时。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-113">For example, when you have a key that can be used to look up model data.</span></span> <span data-ttu-id="3d8ac-114">基于该键，用户可以使用自定义模型绑定器来获取数据。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-114">You can use a custom model binder to fetch data based on the key.</span></span>

## <a name="model-binding-review"></a><span data-ttu-id="3d8ac-115">模型绑定查看</span><span class="sxs-lookup"><span data-stu-id="3d8ac-115">Model binding review</span></span>

<span data-ttu-id="3d8ac-116">模型绑定为其操作对象的类型使用特定定义。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-116">Model binding uses specific definitions for the types it operates on.</span></span> <span data-ttu-id="3d8ac-117">简单类型转换自输入中的单个字符串。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-117">A *simple type* is converted from a single string in the input.</span></span> <span data-ttu-id="3d8ac-118">复杂类型转换自多个输入值。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-118">A *complex type* is converted from multiple input values.</span></span> <span data-ttu-id="3d8ac-119">框架基于是否存在 `TypeConverter` 来确定差异。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-119">The framework determines the difference based on the existence of a `TypeConverter`.</span></span> <span data-ttu-id="3d8ac-120">如果简单 `string` -> `SomeType` 映射不需要外部资源，建议创建类型转换器。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-120">We recommended you create a type converter if you have a simple `string` -> `SomeType` mapping that doesn't require external resources.</span></span>

<span data-ttu-id="3d8ac-121">创建自己的自定义模型绑定器之前，有必要查看现有模型绑定器的实现方式。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-121">Before creating your own custom model binder, it's worth reviewing how existing model binders are implemented.</span></span> <span data-ttu-id="3d8ac-122">考虑使用 [ByteArrayModelBinder](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.modelbinding.binders.bytearraymodelbinder)，它可将 base64 编码的字符串转换为字节数组。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-122">Consider the [ByteArrayModelBinder](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.modelbinding.binders.bytearraymodelbinder) which can be used to convert base64-encoded strings into byte arrays.</span></span> <span data-ttu-id="3d8ac-123">字节数组通常存储为文件或数据库 BLOB 字段。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-123">The byte arrays are often stored as files or database BLOB fields.</span></span>

### <a name="working-with-the-bytearraymodelbinder"></a><span data-ttu-id="3d8ac-124">使用 ByteArrayModelBinder</span><span class="sxs-lookup"><span data-stu-id="3d8ac-124">Working with the ByteArrayModelBinder</span></span>

<span data-ttu-id="3d8ac-125">Base64 编码的字符串可用来表示二进制数据。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-125">Base64-encoded strings can be used to represent binary data.</span></span> <span data-ttu-id="3d8ac-126">例如，下图可编码为一个字符串。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-126">For example, the following image can be encoded as a string.</span></span>

<span data-ttu-id="3d8ac-127">![dotnet 机器人](custom-model-binding/images/bot.png "dotnet 机器人")</span><span class="sxs-lookup"><span data-stu-id="3d8ac-127">![dotnet bot](custom-model-binding/images/bot.png "dotnet bot")</span></span>

<span data-ttu-id="3d8ac-128">如下显示了编码字符串的一小部分：</span><span class="sxs-lookup"><span data-stu-id="3d8ac-128">A small portion of the encoded string is shown in the following image:</span></span>

<span data-ttu-id="3d8ac-129">![编码的 dotnet 机器人](custom-model-binding/images/encoded-bot.png "编码的 dotnet 机器人")</span><span class="sxs-lookup"><span data-stu-id="3d8ac-129">![dotnet bot encoded](custom-model-binding/images/encoded-bot.png "dotnet bot encoded")</span></span>

<span data-ttu-id="3d8ac-130">按照[示例的自述文件](https://github.com/aspnet/Docs/blob/master/aspnetcore/mvc/advanced/custom-model-binding/sample/CustomModelBindingSample/README.md)中的说明将 base64 编码的字符串转换为文件。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-130">Follow the instructions in the [sample's README](https://github.com/aspnet/Docs/blob/master/aspnetcore/mvc/advanced/custom-model-binding/sample/CustomModelBindingSample/README.md) to convert the base64-encoded string into a file.</span></span>

<span data-ttu-id="3d8ac-131">ASP.NET Core MVC 可以采用 base64 编码的字符串，并使用 `ByteArrayModelBinder` 将其转换为字节数组。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-131">ASP.NET Core MVC can take a base64-encoded strings and use a `ByteArrayModelBinder` to convert it into a byte array.</span></span> <span data-ttu-id="3d8ac-132">实现 [IModelBinderProvider](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.modelbinding.imodelbinderprovider) 的 [ByteArrayModelBinderProvider](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.modelbinding.binders.bytearraymodelbinderprovider) 将 `byte[]` 参数映射到 `ByteArrayModelBinder`：</span><span class="sxs-lookup"><span data-stu-id="3d8ac-132">The [ByteArrayModelBinderProvider](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.modelbinding.binders.bytearraymodelbinderprovider) which implements [IModelBinderProvider](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.modelbinding.imodelbinderprovider) maps `byte[]` arguments to `ByteArrayModelBinder`:</span></span>

```csharp
public IModelBinder GetBinder(ModelBinderProviderContext context)
{
    if (context == null)
    {
        throw new ArgumentNullException(nameof(context));
    }

    if (context.Metadata.ModelType == typeof(byte[]))
    {
        return new ByteArrayModelBinder();
    }

    return null;
}
```

<span data-ttu-id="3d8ac-133">创建自己的自定义模型绑定器时，可实现自己的 `IModelBinderProvider` 类型，或使用 [ModelBinderAttribute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.modelbinderattribute)。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-133">When creating your own custom model binder, you can implement your own `IModelBinderProvider` type, or use the [ModelBinderAttribute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.modelbinderattribute).</span></span>

<span data-ttu-id="3d8ac-134">以下示例显示如何使用 `ByteArrayModelBinder` 将 base64 编码的字符串转换为 `byte[]`，并将结果保存到文件中：</span><span class="sxs-lookup"><span data-stu-id="3d8ac-134">The following example shows how to use `ByteArrayModelBinder` to convert a base64-encoded string to a `byte[]` and save the result to a file:</span></span>

[!code-csharp[Main](custom-model-binding/sample/CustomModelBindingSample/Controllers/ImageController.cs?name=post1&highlight=3)]

<span data-ttu-id="3d8ac-135">可以使用 [Postman](https://www.getpostman.com/) 等工具将 base64 编码的字符串发布到此 api 方法：</span><span class="sxs-lookup"><span data-stu-id="3d8ac-135">You can POST a base64-encoded string to this api method using a tool like [Postman](https://www.getpostman.com/):</span></span>

<span data-ttu-id="3d8ac-136">![postman](custom-model-binding/images/postman.png "postman")</span><span class="sxs-lookup"><span data-stu-id="3d8ac-136">![postman](custom-model-binding/images/postman.png "postman")</span></span>

<span data-ttu-id="3d8ac-137">只要绑定器可以将请求数据绑定到相应命名的属性或参数，模型绑定就会成功。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-137">As long as the binder can bind request data to appropriately named properties or arguments, model binding will succeed.</span></span> <span data-ttu-id="3d8ac-138">以下示例演示如何将 `ByteArrayModelBinder` 与 视图模型结合使用：</span><span class="sxs-lookup"><span data-stu-id="3d8ac-138">The following example shows how to use `ByteArrayModelBinder` with a view model:</span></span>

[!code-csharp[Main](custom-model-binding/sample/CustomModelBindingSample/Controllers/ImageController.cs?name=post2&highlight=2)]

## <a name="custom-model-binder-sample"></a><span data-ttu-id="3d8ac-139">自定义模型绑定器示例</span><span class="sxs-lookup"><span data-stu-id="3d8ac-139">Custom model binder sample</span></span>

<span data-ttu-id="3d8ac-140">在本部分中，我们将实现具有以下功能的自定义模型绑定器：</span><span class="sxs-lookup"><span data-stu-id="3d8ac-140">In this section we'll implement a custom model binder that:</span></span>

- <span data-ttu-id="3d8ac-141">将传入的请求数据转换为强类型键参数。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-141">Converts incoming request data into strongly typed key arguments.</span></span>
- <span data-ttu-id="3d8ac-142">使用 Entity Framework Core 来提取关联的实体。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-142">Uses Entity Framework Core to fetch the associated entity.</span></span>
- <span data-ttu-id="3d8ac-143">将关联的实体作为自变量传递给操作方法。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-143">Passes the associated entity as an argument to the action method.</span></span>

<span data-ttu-id="3d8ac-144">以下示例在 `Author` 模型上使用 `ModelBinder` 属性：</span><span class="sxs-lookup"><span data-stu-id="3d8ac-144">The following sample uses the `ModelBinder` attribute on the `Author` model:</span></span>

[!code-csharp[Main](custom-model-binding/sample/CustomModelBindingSample/Data/Author.cs?highlight=10)]

<span data-ttu-id="3d8ac-145">在前面的代码中，`ModelBinder` 属性指定应当用于绑定 `Author` 操作参数的 `IModelBinder` 的类型。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-145">In the preceding code, the `ModelBinder` attribute specifies the type of `IModelBinder` that should be used to bind `Author` action parameters.</span></span> 

<span data-ttu-id="3d8ac-146">通过 Entity Framework Core 和 `authorId` 提取数据源中的实体，可使用 `AuthorEntityBinder` 来绑定 `Author` 参数：</span><span class="sxs-lookup"><span data-stu-id="3d8ac-146">The `AuthorEntityBinder` is used to bind an `Author` parameter by fetching the entity from a data source using Entity Framework Core and an `authorId`:</span></span>

[!code-csharp[Main](custom-model-binding/sample/CustomModelBindingSample/Binders/AuthorEntityBinder.cs?name=demo)]

<span data-ttu-id="3d8ac-147">以下代码显示如何在操作方法中使用 `AuthorEntityBinder`：</span><span class="sxs-lookup"><span data-stu-id="3d8ac-147">The following code shows how to use the `AuthorEntityBinder` in an action method:</span></span>

[!code-csharp[Main](custom-model-binding/sample/CustomModelBindingSample/Controllers/BoundAuthorsController.cs?name=demo2&highlight=2)]

<span data-ttu-id="3d8ac-148">可使用 `ModelBinder` 属性将 `AuthorEntityBinder` 应用于不使用默认约定的参数：</span><span class="sxs-lookup"><span data-stu-id="3d8ac-148">The `ModelBinder` attribute can be used to apply the `AuthorEntityBinder` to parameters that don't use default conventions:</span></span>

[!code-csharp[Main](custom-model-binding/sample/CustomModelBindingSample/Controllers/BoundAuthorsController.cs?name=demo1&highlight=2)]

<span data-ttu-id="3d8ac-149">在此示例中，由于参数的名称不是默认的 `authorId`，因此使用 `ModelBinder` 属性在参数上指定该名称。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-149">In this example, since the name of the argument isn't the default `authorId`, it's specified on the parameter using `ModelBinder` attribute.</span></span> <span data-ttu-id="3d8ac-150">请注意，比起在操作方法中查找实体，控制器和操作方法都得到了简化。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-150">Note that both the controller and action method are simplified compared to looking up the entity in the action method.</span></span> <span data-ttu-id="3d8ac-151">使用 Entity Framework Core 获取创建者的逻辑会移动到模型绑定器。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-151">The logic to fetch the author using Entity Framework Core is moved to the model binder.</span></span> <span data-ttu-id="3d8ac-152">如果有几种方法绑定到创建者模型，就能得到很大程度的简化，并且有助于遵循 [DRY 原则](http://deviq.com/don-t-repeat-yourself/)。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-152">This can be considerable simplification when you have several methods that bind to the author model, and can help you to follow the [DRY principle](http://deviq.com/don-t-repeat-yourself/).</span></span>

<span data-ttu-id="3d8ac-153">可以将 `ModelBinder` 属性应用到各个模型属性（例如视图模型上）或操作方法参数，以便为该类型或操作指定某一模型绑定器或模型名称。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-153">You can apply the `ModelBinder` attribute to individual model properties (such as on a viewmodel) or to action method parameters to specify a certain model binder or model name for just that type or action.</span></span>

### <a name="implementing-a-modelbinderprovider"></a><span data-ttu-id="3d8ac-154">实现 ModelBinderProvider</span><span class="sxs-lookup"><span data-stu-id="3d8ac-154">Implementing a ModelBinderProvider</span></span>

<span data-ttu-id="3d8ac-155">可以实现 `IModelBinderProvider`，而不是应用属性。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-155">Instead of applying an attribute, you can implement `IModelBinderProvider`.</span></span> <span data-ttu-id="3d8ac-156">这就是内置框架绑定器的实现方式。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-156">This is how the built-in framework binders are implemented.</span></span> <span data-ttu-id="3d8ac-157">指定绑定器所操作的类型时，指定它生成的参数的类型，而不是绑定器接受的输入。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-157">When you specify the type your binder operates on, you specify the type of argument it produces, **not** the input your binder accepts.</span></span> <span data-ttu-id="3d8ac-158">以下绑定器提供程序适用于 `AuthorEntityBinder`。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-158">The following binder provider works with the `AuthorEntityBinder`.</span></span> <span data-ttu-id="3d8ac-159">将其添加到 MVC 提供程序的集合中时，无需在 `Author` 或 `Author` 类型参数上使用 `ModelBinder` 属性。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-159">When it's added to MVC's collection of providers, you don't need to use the `ModelBinder` attribute on `Author` or `Author` typed parameters.</span></span>

[!code-csharp[Main](custom-model-binding/sample/CustomModelBindingSample/Binders/AuthorEntityBinderProvider.cs?highlight=17-20)]

> <span data-ttu-id="3d8ac-160">注意：上述代码返回 `BinderTypeModelBinder`。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-160">Note: The preceding code returns a `BinderTypeModelBinder`.</span></span> <span data-ttu-id="3d8ac-161">`BinderTypeModelBinder` 充当模型绑定器中心，并提供依赖关系注入 (DI)。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-161">`BinderTypeModelBinder` acts as a factory for model binders and provides dependency injection (DI).</span></span> <span data-ttu-id="3d8ac-162">`AuthorEntityBinder` 需要 DI 来访问 EF Core。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-162">The `AuthorEntityBinder` requires DI to access EF Core.</span></span> <span data-ttu-id="3d8ac-163">如果模型绑定器需要 DI 中的服务，请使用 `BinderTypeModelBinder`。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-163">Use `BinderTypeModelBinder` if your model binder requires services from DI.</span></span>

<span data-ttu-id="3d8ac-164">若要使用自定义模型绑定器提供程序，请将其添加到 `ConfigureServices` 中：</span><span class="sxs-lookup"><span data-stu-id="3d8ac-164">To use a custom model binder provider, add it in `ConfigureServices`:</span></span>

[!code-csharp[Main](custom-model-binding/sample/CustomModelBindingSample/Startup.cs?name=callout&highlight=5-9)]

<span data-ttu-id="3d8ac-165">评估模型绑定器时，按顺序检查提供程序的集合。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-165">When evaluating model binders, the collection of providers is examined in order.</span></span> <span data-ttu-id="3d8ac-166">使用返回绑定器的第一个提供程序。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-166">The first provider that returns a binder is used.</span></span>

<span data-ttu-id="3d8ac-167">下图显示调试程序中的默认模型绑定器。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-167">The following image shows the default model binders from the debugger.</span></span>

<span data-ttu-id="3d8ac-168">![默认模型绑定器](custom-model-binding/images/default-model-binders.png "默认模型绑定器")</span><span class="sxs-lookup"><span data-stu-id="3d8ac-168">![default model binders](custom-model-binding/images/default-model-binders.png "default model binders")</span></span>

<span data-ttu-id="3d8ac-169">向集合的末尾添加提供程序，可能会导致在调用自定义绑定器之前调用内置模型绑定器。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-169">Adding your provider to the end of the collection may result in a built-in model binder being called before your custom binder has a chance.</span></span> <span data-ttu-id="3d8ac-170">在此示例中，向集合的开头添加自定义提供程序，确保它用于 `Author` 操作参数。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-170">In this example, the custom provider is added to the beginning of the collection to ensure it's used for `Author` action arguments.</span></span>

[!code-csharp[Main](custom-model-binding/sample/CustomModelBindingSample/Startup.cs?name=callout&highlight=5-9)]

## <a name="recommendations-and-best-practices"></a><span data-ttu-id="3d8ac-171">建议和最佳做法</span><span class="sxs-lookup"><span data-stu-id="3d8ac-171">Recommendations and best practices</span></span>

<span data-ttu-id="3d8ac-172">自定义模型绑定：</span><span class="sxs-lookup"><span data-stu-id="3d8ac-172">Custom model binders:</span></span>
- <span data-ttu-id="3d8ac-173">不应尝试设置状态代码或返回结果（例如 404 Not Found）。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-173">Shouldn't attempt to set status codes or return results (for example, 404 Not Found).</span></span> <span data-ttu-id="3d8ac-174">如果模型绑定失败，那么该操作方法本身的[操作筛选器](xref:mvc/controllers/filters)或逻辑会处理失败。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-174">If model binding fails, an [action filter](xref:mvc/controllers/filters) or logic within the action method itself should handle the failure.</span></span>
- <span data-ttu-id="3d8ac-175">对于消除操作方法中的重复代码和跨领域问题最为有用。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-175">Are most useful for eliminating repetitive code and cross-cutting concerns from action methods.</span></span>
- <span data-ttu-id="3d8ac-176">通常不应用其将字符串转换为自定义类型，而应选择用 [`TypeConverter`](https://docs.microsoft.com//dotnet/api/system.componentmodel.typeconverter) 来完成此操作。</span><span class="sxs-lookup"><span data-stu-id="3d8ac-176">Typically shouldn't be used to convert a string into a custom type, a [`TypeConverter`](https://docs.microsoft.com//dotnet/api/system.componentmodel.typeconverter) is usually a better option.</span></span>
