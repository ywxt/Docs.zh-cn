---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API 中的参数绑定 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 07/11/2013
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 97785db962691c25bac03f904924321af2f6b500
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37810077"
---
<a name="parameter-binding-in-aspnet-web-api"></a><span data-ttu-id="f971a-102">ASP.NET Web API 中的参数绑定</span><span class="sxs-lookup"><span data-stu-id="f971a-102">Parameter Binding in ASP.NET Web API</span></span>
====================
<span data-ttu-id="f971a-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f971a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="f971a-104">Web API 在控制器上调用方法时，必须设置参数的值，此过程称为“绑定”。</span><span class="sxs-lookup"><span data-stu-id="f971a-104">When Web API calls a method on a controller, it must set values for the parameters, a process called *binding*.</span></span> <span data-ttu-id="f971a-105">本文介绍了 Web API 如何绑定参数，以及你如何自定义绑定过程。	
</span><span class="sxs-lookup"><span data-stu-id="f971a-105">This article describes how Web API binds parameters, and how you can customize the binding process.</span></span>

<span data-ttu-id="f971a-106">默认情况下，Web API 使用以下规则进行参数绑定：</span><span class="sxs-lookup"><span data-stu-id="f971a-106">By default, Web API uses the following rules to bind parameters:</span></span>

- <span data-ttu-id="f971a-107">如果参数为“简单”类型，Web API 会尝试从 URI 中获取值。</span><span class="sxs-lookup"><span data-stu-id="f971a-107">If the parameter is a "simple" type, Web API tries to get the value from the URI.</span></span> <span data-ttu-id="f971a-108">简单类型包括 .NET[基元类型](https://msdn.microsoft.com/library/system.type.isprimitive.aspx)（**int**、 **bool**、 **double**等），以及 **TimeSpan**、**DateTime**、**Guid**、**decimal** 和 **string**，此外还有**借助类型转换器即可从字符串进行转换的类型。</span><span class="sxs-lookup"><span data-stu-id="f971a-108">Simple types include the .NET [primitive types](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, and so forth), plus **TimeSpan**, **DateTime**, **Guid**, **decimal**, and **string**, *plus* any type with a type converter that can convert from a string.</span></span> <span data-ttu-id="f971a-109">（稍后介绍有关类型转换器的详细信息。）</span><span class="sxs-lookup"><span data-stu-id="f971a-109">(More about type converters later.)</span></span>
- <span data-ttu-id="f971a-110">对于复杂类型，Web API 尝试使用[媒体类型格式化程序](media-formatters.md)从消息正文中读取值。</span><span class="sxs-lookup"><span data-stu-id="f971a-110">For complex types, Web API tries to read the value from the message body, using a [media-type formatter](media-formatters.md).</span></span>

<span data-ttu-id="f971a-111">例如，下面是典型的 Web API 控制器方法：</span><span class="sxs-lookup"><span data-stu-id="f971a-111">For example, here is a typical Web API controller method:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="f971a-112">*Id* 参数是&quot;简单&quot;类型，因此 Web API 尝试从请求 URI 中获取值。</span><span class="sxs-lookup"><span data-stu-id="f971a-112">The *id* parameter is a &quot;simple&quot; type, so Web API tries to get the value from the request URI.</span></span> <span data-ttu-id="f971a-113">*item* 参数是复杂类型，因此 Web API 使用媒体类型格式化程序从请求正文中读取值。</span><span class="sxs-lookup"><span data-stu-id="f971a-113">The *item* parameter is a complex type, so Web API uses a media-type formatter to read the value from the request body.</span></span>

<span data-ttu-id="f971a-114">为了从 URI 中获取值，Web API 会在路由数据和 URI 查询字符串中进行查找。</span><span class="sxs-lookup"><span data-stu-id="f971a-114">To get a value from the URI, Web API looks in the route data and the URI query string.</span></span> <span data-ttu-id="f971a-115">路由系统分析 URI 并将其与某个路由匹配时，会填充路由数据。</span><span class="sxs-lookup"><span data-stu-id="f971a-115">The route data is populated when the routing system parses the URI and matches it to a route.</span></span> <span data-ttu-id="f971a-116">有关详细信息，请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="f971a-116">For more information, see [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span>

<span data-ttu-id="f971a-117">本文其余部分介绍如何自定义模型绑定过程。</span><span class="sxs-lookup"><span data-stu-id="f971a-117">In the rest of this article, I'll show how you can customize the model binding process.</span></span> <span data-ttu-id="f971a-118">但是，对于复杂类型，请尽可能使用媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="f971a-118">For complex types, however, consider using media-type formatters whenever possible.</span></span> <span data-ttu-id="f971a-119">HTTP 的关键原则在于，资源在消息正文中发送，同时使用内容协商来指定资源表示形式。</span><span class="sxs-lookup"><span data-stu-id="f971a-119">A key principle of HTTP is that resources are sent in the message body, using content negotiation to specify the representation of the resource.</span></span> <span data-ttu-id="f971a-120">媒体类型格式化程序正是专为此而设计的。
</span><span class="sxs-lookup"><span data-stu-id="f971a-120">Media-type formatters were designed for exactly this purpose.</span></span>

## <a name="using-fromuri"></a><span data-ttu-id="f971a-121">使用 [FromUri]</span><span class="sxs-lookup"><span data-stu-id="f971a-121">Using [FromUri]</span></span>

<span data-ttu-id="f971a-122">若要强制 Web API 从 URI 读取复杂类型，请向参数添加 **[FromUri]** 特性。</span><span class="sxs-lookup"><span data-stu-id="f971a-122">To force Web API to read a complex type from the URI, add the **[FromUri]** attribute to the parameter.</span></span> <span data-ttu-id="f971a-123">下面的示例定义 `GeoPoint` 类型，以及从 URI 获取 `GeoPoint` 的控制器方法。</span><span class="sxs-lookup"><span data-stu-id="f971a-123">The following example defines a `GeoPoint` type, along with a controller method that gets the `GeoPoint` from the URI.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="f971a-124">客户端可以将纬度和经度值放在查询字符串中，Web API 会使用它们来构造`GeoPoint`。</span><span class="sxs-lookup"><span data-stu-id="f971a-124">The client can put the Latitude and Longitude values in the query string and Web API will use them to construct a `GeoPoint`.</span></span> <span data-ttu-id="f971a-125">例如：</span><span class="sxs-lookup"><span data-stu-id="f971a-125">For example:</span></span>

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a><span data-ttu-id="f971a-126">使用 [FromBody]</span><span class="sxs-lookup"><span data-stu-id="f971a-126">Using [FromBody]</span></span>

<span data-ttu-id="f971a-127">若要强制 Web API 从请求正文读取简单类型，请向参数添加 **[FromBody]** 特性：</span><span class="sxs-lookup"><span data-stu-id="f971a-127">To force Web API to read a simple type from the request body, add the **[FromBody]** attribute to the parameter:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="f971a-128">在此示例中，Web API 会使用媒体类型格式化程序从请求正文读取 *name* 的值。下面是一个客户端请求示例。</span><span class="sxs-lookup"><span data-stu-id="f971a-128">In this example, Web API will use a media-type formatter to read the value of *name* from the request body.</span></span> <span data-ttu-id="f971a-129">下面是示例客户端请求。</span><span class="sxs-lookup"><span data-stu-id="f971a-129">Here is an example client request.</span></span>

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

<span data-ttu-id="f971a-130">当参数具有 [FromBody] 时，Web API 使用 Content-Type 标头来选择格式化程序。</span><span class="sxs-lookup"><span data-stu-id="f971a-130">When a parameter has [FromBody], Web API uses the Content-Type header to select a formatter.</span></span> <span data-ttu-id="f971a-131">在此示例中，内容类型是 &quot;application/json&quot;，请求正文是原始的 JSON 字符串（不是 JSON 对象）。</span><span class="sxs-lookup"><span data-stu-id="f971a-131">In this example, the content type is &quot;application/json&quot; and the request body is a raw JSON string (not a JSON object).</span></span>

<span data-ttu-id="f971a-132">最多允许一个参数从消息正文中读取。因此以下代码不起作用：</span><span class="sxs-lookup"><span data-stu-id="f971a-132">At most one parameter is allowed to read from the message body.</span></span> <span data-ttu-id="f971a-133">因此这不起作用：</span><span class="sxs-lookup"><span data-stu-id="f971a-133">So this will not work:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="f971a-134">之所以实施此规则，是因为请求正文可能存储在只能读取一次的非缓冲流中。</span><span class="sxs-lookup"><span data-stu-id="f971a-134">The reason for this rule is that the request body might be stored in a non-buffered stream that can only be read once.</span></span>

## <a name="type-converters"></a><span data-ttu-id="f971a-135">类型转换器</span><span class="sxs-lookup"><span data-stu-id="f971a-135">Type Converters</span></span>

<span data-ttu-id="f971a-136">可以创建 **TypeConverter** 并提供字符串转换，让 Web API 将一个类视为简单类型（这样 Web API 就会尝试将其从 URI 绑定）。</span><span class="sxs-lookup"><span data-stu-id="f971a-136">You can make Web API treat a class as a simple type (so that Web API will try to bind it from the URI) by creating a **TypeConverter** and providing a string conversion.</span></span>

<span data-ttu-id="f971a-137">下面的代码演示一个表示地理点的 `GeoPoint` 类，以及一个可以从字符串转换为 **实例的**TypeConverter`GeoPoint`。</span><span class="sxs-lookup"><span data-stu-id="f971a-137">The following code shows a `GeoPoint` class that represents a geographical point, plus a **TypeConverter** that converts from strings to `GeoPoint` instances.</span></span> <span data-ttu-id="f971a-138">`GeoPoint` 类使用可指定类型转换器的 **[TypeConverter]** 特性来修饰。</span><span class="sxs-lookup"><span data-stu-id="f971a-138">The `GeoPoint` class is decorated with a **[TypeConverter]** attribute to specify the type converter.</span></span> <span data-ttu-id="f971a-139">此示例借鉴了 Mike Stall 的博文 [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)（如何在 MVC/WebAPI 中绑定到操作签名中的自定义对象）。）</span><span class="sxs-lookup"><span data-stu-id="f971a-139">(This example was inspired by Mike Stall's blog post [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="f971a-140">现在 Web API 会将 `GeoPoint` 视为简单类型，这意味着它会尝试从 URI 绑定`GeoPoint` 类型的参数。</span><span class="sxs-lookup"><span data-stu-id="f971a-140">Now Web API will treat `GeoPoint` as a simple type, meaning it will try to bind `GeoPoint` parameters from the URI.</span></span> <span data-ttu-id="f971a-141">不需要在参数中包括 **[FromUri]**。</span><span class="sxs-lookup"><span data-stu-id="f971a-141">You don't need to include **[FromUri]** on the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="f971a-142">客户端可以调用具有如下的 URI 的方法：</span><span class="sxs-lookup"><span data-stu-id="f971a-142">The client can invoke the method with a URI like this:</span></span>

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a><span data-ttu-id="f971a-143">模型绑定器</span><span class="sxs-lookup"><span data-stu-id="f971a-143">Model Binders</span></span>

<span data-ttu-id="f971a-144">类型转换器更灵活的选项是创建自定义模型绑定器。</span><span class="sxs-lookup"><span data-stu-id="f971a-144">A more flexible option than a type converter is to create a custom model binder.</span></span> <span data-ttu-id="f971a-145">可以通过模型绑定器访问 HTTP 请求、操作说明、路由数据中的原始值等内容。</span><span class="sxs-lookup"><span data-stu-id="f971a-145">With a model binder, you have access to things like the HTTP request, the action description, and the raw values from the route data.</span></span>

<span data-ttu-id="f971a-146">创建模型绑定器需要实现 **IModelBinder** 接口。</span><span class="sxs-lookup"><span data-stu-id="f971a-146">To create a model binder, implement the **IModelBinder** interface.</span></span> <span data-ttu-id="f971a-147">此接口定义单个方法，即 **BindModel**：
</span><span class="sxs-lookup"><span data-stu-id="f971a-147">This interface defines a single method, **BindModel**:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

<span data-ttu-id="f971a-148">下面是 `GeoPoint` 对象的模型绑定器。</span><span class="sxs-lookup"><span data-stu-id="f971a-148">Here is a model binder for `GeoPoint` objects.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="f971a-149">模型绑定器从值提供程序获取原始输入值。</span><span class="sxs-lookup"><span data-stu-id="f971a-149">A model binder gets raw input values from a *value provider*.</span></span> <span data-ttu-id="f971a-150">这种设计可以将两种不同的功能分隔开：</span><span class="sxs-lookup"><span data-stu-id="f971a-150">This design separates two distinct functions:</span></span>

- <span data-ttu-id="f971a-151">值提供程序获取 HTTP 请求，并填充的键 / 值对的字典。</span><span class="sxs-lookup"><span data-stu-id="f971a-151">The value provider takes the HTTP request and populates a dictionary of key-value pairs.</span></span>
- <span data-ttu-id="f971a-152">模型绑定器使用此字典来填充模型。</span><span class="sxs-lookup"><span data-stu-id="f971a-152">The model binder uses this dictionary to populate the model.</span></span>

<span data-ttu-id="f971a-153">Web API 中的默认值提供程序获取路由数据和查询字符串中的值。</span><span class="sxs-lookup"><span data-stu-id="f971a-153">The default value provider in Web API gets values from the route data and the query string.</span></span> <span data-ttu-id="f971a-154">例如，如果 URI 是`http://localhost/api/values/1?location=48,-122`，值提供程序创建以下键 / 值对：</span><span class="sxs-lookup"><span data-stu-id="f971a-154">For example, if the URI is `http://localhost/api/values/1?location=48,-122`, the value provider creates the following key-value pairs:</span></span>

- <span data-ttu-id="f971a-155">id = &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="f971a-155">id = &quot;1&quot;</span></span>
- <span data-ttu-id="f971a-156">位置 = &quot;48,122&quot;</span><span class="sxs-lookup"><span data-stu-id="f971a-156">location = &quot;48,122&quot;</span></span>

<span data-ttu-id="f971a-157">(假设默认路由模板，这是&quot;api / {controller} / {id}&quot;。)</span><span class="sxs-lookup"><span data-stu-id="f971a-157">(I'm assuming the default route template, which is &quot;api/{controller}/{id}&quot;.)</span></span>

<span data-ttu-id="f971a-158">要绑定的参数的名称存储在 **ModelBindingContext.ModelName** 属性中。</span><span class="sxs-lookup"><span data-stu-id="f971a-158">The name of the parameter to bind is stored in the **ModelBindingContext.ModelName** property.</span></span> <span data-ttu-id="f971a-159">模型绑定器会在字典中查找包含此值的键。</span><span class="sxs-lookup"><span data-stu-id="f971a-159">The model binder looks for a key with this value in the dictionary.</span></span> <span data-ttu-id="f971a-160">如果此值存在，并且可以转换为 `GeoPoint`，模型绑定器会将绑定的值赋给 **ModelBindingContext.Model** 属性。</span><span class="sxs-lookup"><span data-stu-id="f971a-160">If the value exists and can be converted into a `GeoPoint`, the model binder assigns the bound value to the **ModelBindingContext.Model** property.</span></span>

<span data-ttu-id="f971a-161">请注意，模型绑定器不限于简单类型转换。</span><span class="sxs-lookup"><span data-stu-id="f971a-161">Notice that the model binder is not limited to a simple type conversion.</span></span> <span data-ttu-id="f971a-162">模型绑定器首先在包含已知位置的表中进行查找，如果失败，则会使用类型转换。
</span><span class="sxs-lookup"><span data-stu-id="f971a-162">In this example, the model binder first looks in a table of known locations, and if that fails, it uses type conversion.</span></span>

<span data-ttu-id="f971a-163">**设置模型绑定器**</span><span class="sxs-lookup"><span data-stu-id="f971a-163">**Setting the Model Binder**</span></span>

<span data-ttu-id="f971a-164">可以通过多种方法来设置模型绑定器。</span><span class="sxs-lookup"><span data-stu-id="f971a-164">There are several ways to set a model binder.</span></span> <span data-ttu-id="f971a-165">可以向参数添加 **[ModelBinder]** 特性</span><span class="sxs-lookup"><span data-stu-id="f971a-165">First, you can add a **[ModelBinder]** attribute to the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

<span data-ttu-id="f971a-166">也可以向类型添加 **[ModelBinder]** 特性。</span><span class="sxs-lookup"><span data-stu-id="f971a-166">You can also add a **[ModelBinder]** attribute to the type.</span></span> <span data-ttu-id="f971a-167">Web API 会对该类型的所有参数使用指定的模型绑定器。
</span><span class="sxs-lookup"><span data-stu-id="f971a-167">Web API will use the specified model binder for all parameters of that type.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="f971a-168">最后，可以将模型绑定器提供程序添加到 **HttpConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="f971a-168">Finally, you can add a model-binder provider to the **HttpConfiguration**.</span></span> <span data-ttu-id="f971a-169">模型绑定器提供程序只是一个用于创建模型绑定器的工厂类。</span><span class="sxs-lookup"><span data-stu-id="f971a-169">A model-binder provider is simply a factory class that creates a model binder.</span></span> <span data-ttu-id="f971a-170">可以通过从 [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) 类派生来创建提供程序。</span><span class="sxs-lookup"><span data-stu-id="f971a-170">You can create a provider by deriving from the [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) class.</span></span> <span data-ttu-id="f971a-171">但是，如果模型绑定器处理的是单一类型，则更简单的方法是使用内置的 **SimpleModelBinderProvider**，后者是专为此而设计的。</span><span class="sxs-lookup"><span data-stu-id="f971a-171">However, if your model binder handles a single type, it's easier to use the built-in **SimpleModelBinderProvider**, which is designed for this purpose.</span></span> <span data-ttu-id="f971a-172">下面的代码演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="f971a-172">The following code shows how to do this.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

<span data-ttu-id="f971a-173">使用模型绑定提供程序时，仍需向参数添加 **[ModelBinder]** 特性，目的是告知 Web API 使用模型绑定器，而不是使用媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="f971a-173">With a model-binding provider, you still need to add the **[ModelBinder]** attribute to the parameter, to tell Web API that it should use a model binder and not a media-type formatter.</span></span> <span data-ttu-id="f971a-174">不过，现在无需在特性中指定模型绑定器的类型：</span><span class="sxs-lookup"><span data-stu-id="f971a-174">But now you don't need to specify the type of model binder in the attribute:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a><span data-ttu-id="f971a-175">值提供程序</span><span class="sxs-lookup"><span data-stu-id="f971a-175">Value Providers</span></span>

<span data-ttu-id="f971a-176">前面提到过，模型绑定器从值提供程序中获取值。</span><span class="sxs-lookup"><span data-stu-id="f971a-176">I mentioned that a model binder gets values from a value provider.</span></span> <span data-ttu-id="f971a-177">若要编写自定义值提供程序，请实现 **IValueProvider** 接口。</span><span class="sxs-lookup"><span data-stu-id="f971a-177">To write a custom value provider, implement the **IValueProvider** interface.</span></span> <span data-ttu-id="f971a-178">以下示例演示了如何在请求中从 Cookie 提取值：</span><span class="sxs-lookup"><span data-stu-id="f971a-178">Here is an example that pulls values from the cookies in the request:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

<span data-ttu-id="f971a-179">您还需要创建值提供程序工厂通过派生自**ValueProviderFactory**类。</span><span class="sxs-lookup"><span data-stu-id="f971a-179">You also need to create a value provider factory by deriving from the **ValueProviderFactory** class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

<span data-ttu-id="f971a-180">添加到值提供程序工厂**HttpConfiguration** ，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f971a-180">Add the value provider factory to the **HttpConfiguration** as follows.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

<span data-ttu-id="f971a-181">Web API 编写所有值提供程序，因此模型绑定器在调用 **ValueProvider.GetValue** 时，会从第一个能够生成该值的值提供程序接收值。</span><span class="sxs-lookup"><span data-stu-id="f971a-181">Web API composes all of the value providers, so when a model binder calls **ValueProvider.GetValue**, the model binder receives the value from the first value provider that is able to produce it.</span></span>

<span data-ttu-id="f971a-182">或者，通过使用，在参数级别设置值提供程序工厂**ValueProvider**属性，按如下所示：</span><span class="sxs-lookup"><span data-stu-id="f971a-182">Alternatively, you can set the value provider factory at the parameter level by using the **ValueProvider** attribute, as follows:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

<span data-ttu-id="f971a-183">这将告知 Web API 使用模型绑定使用指定的值提供程序工厂，而不使用任何其他已注册的值提供程序。</span><span class="sxs-lookup"><span data-stu-id="f971a-183">This tells Web API to use model binding with the specified value provider factory, and not to use any of the other registered value providers.</span></span>

## <a name="httpparameterbinding"></a><span data-ttu-id="f971a-184">HttpParameterBinding</span><span class="sxs-lookup"><span data-stu-id="f971a-184">HttpParameterBinding</span></span>

<span data-ttu-id="f971a-185">模型绑定器是一个演示较通用机制的具体实例。</span><span class="sxs-lookup"><span data-stu-id="f971a-185">Model binders are a specific instance of a more general mechanism.</span></span> <span data-ttu-id="f971a-186">如果查看 **[ModelBinder]** 特性，你会发现它派生自抽象类 **ParameterBindingAttribute**。</span><span class="sxs-lookup"><span data-stu-id="f971a-186">If you look at the **[ModelBinder]** attribute, you will see that it derives from the abstract **ParameterBindingAttribute** class.</span></span> <span data-ttu-id="f971a-187">此类定义的单个方法 **GetBinding** 可返回 **HttpParameterBinding** 对象：</span><span class="sxs-lookup"><span data-stu-id="f971a-187">This class defines a single method, **GetBinding**, which returns an **HttpParameterBinding** object:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

<span data-ttu-id="f971a-188">**HttpParameterBinding** 负责将参数绑定到值。</span><span class="sxs-lookup"><span data-stu-id="f971a-188">An **HttpParameterBinding** is responsible for binding a parameter to a value.</span></span> <span data-ttu-id="f971a-189">如果使用 **[ModelBinder]**，此特性会返回一个 **HttpParameterBinding** 实现，该实现使用 **IModelBinder** 执行实际的绑定。</span><span class="sxs-lookup"><span data-stu-id="f971a-189">In the case of **[ModelBinder]**, the attribute returns an **HttpParameterBinding** implementation that uses an **IModelBinder** to perform the actual binding.</span></span> <span data-ttu-id="f971a-190">你还可以实现你自己的**HttpParameterBinding**。</span><span class="sxs-lookup"><span data-stu-id="f971a-190">You can also implement your own **HttpParameterBinding**.</span></span>

<span data-ttu-id="f971a-191">例如，假设你想要获取从 Etag`if-match`和`if-none-match`中请求的标头。</span><span class="sxs-lookup"><span data-stu-id="f971a-191">For example, suppose you want to get ETags from `if-match` and `if-none-match` headers in the request.</span></span> <span data-ttu-id="f971a-192">我们将首先定义一个类来表示 Etag。</span><span class="sxs-lookup"><span data-stu-id="f971a-192">We'll start by defining a class to represent ETags.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

<span data-ttu-id="f971a-193">我们还将定义一个枚举，指示是从 `if-match` 标头还是从 `if-none-match` 标头获取 ETag。
</span><span class="sxs-lookup"><span data-stu-id="f971a-193">We'll also define an enumeration to indicate whether to get the ETag from the `if-match` header or the `if-none-match` header.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

<span data-ttu-id="f971a-194">下面是一个 **HttpParameterBinding**，该类从所需标头获取 ETag，并将其绑定到类型为 ETag 的参数：</span><span class="sxs-lookup"><span data-stu-id="f971a-194">Here is an **HttpParameterBinding** that gets the ETag from the desired header and binds it to a parameter of type ETag:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

<span data-ttu-id="f971a-195">**ExecuteBindingAsync**方法执行绑定。</span><span class="sxs-lookup"><span data-stu-id="f971a-195">The **ExecuteBindingAsync** method does the binding.</span></span> <span data-ttu-id="f971a-196">在此方法中，将绑定的参数值添加到**ActionArgument**字典中的**HttpActionContext**。</span><span class="sxs-lookup"><span data-stu-id="f971a-196">Within this method, add the bound parameter value to the **ActionArgument** dictionary in the **HttpActionContext**.</span></span>

> [!NOTE]
> <span data-ttu-id="f971a-197">如果你**ExecuteBindingAsync**方法读取请求消息的正文，请重写**WillReadBody**属性返回 true。</span><span class="sxs-lookup"><span data-stu-id="f971a-197">If your **ExecuteBindingAsync** method reads the body of the request message, override the **WillReadBody** property to return true.</span></span> <span data-ttu-id="f971a-198">请求正文可能只能读取一次，因此 Web API 实施规则，最多一个绑定未缓冲的数据流可以读取消息正文。</span><span class="sxs-lookup"><span data-stu-id="f971a-198">The request body might be an unbuffered stream that can only be read once, so Web API enforces a rule that at most one binding can read the message body.</span></span>


<span data-ttu-id="f971a-199">要应用自定义**HttpParameterBinding**，可以定义从派生的特性**ParameterBindingAttribute**。</span><span class="sxs-lookup"><span data-stu-id="f971a-199">To apply a custom **HttpParameterBinding**, you can define an attribute that derives from **ParameterBindingAttribute**.</span></span> <span data-ttu-id="f971a-200">有关`ETagParameterBinding`，我们将定义两个属性，一个用于`if-match`标头和一个用于`if-none-match`标头。</span><span class="sxs-lookup"><span data-stu-id="f971a-200">For `ETagParameterBinding`, we'll define two attributes, one for `if-match` headers and one for `if-none-match` headers.</span></span> <span data-ttu-id="f971a-201">都派生自抽象基类的类。</span><span class="sxs-lookup"><span data-stu-id="f971a-201">Both derive from an abstract base class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

<span data-ttu-id="f971a-202">下面是使用控制器方法`[IfNoneMatch]`属性。</span><span class="sxs-lookup"><span data-stu-id="f971a-202">Here is a controller method that uses the `[IfNoneMatch]` attribute.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

<span data-ttu-id="f971a-203">除了**ParameterBindingAttribute**，没有用于添加自定义的另一个挂钩**HttpParameterBinding**。</span><span class="sxs-lookup"><span data-stu-id="f971a-203">Besides **ParameterBindingAttribute**, there is another hook for adding a custom **HttpParameterBinding**.</span></span> <span data-ttu-id="f971a-204">上**HttpConfiguration**对象， **ParameterBindingRules**属性是集合类型的 anomymous 函数 (**HttpParameterDescriptor**  - &gt; **HttpParameterBinding**)。</span><span class="sxs-lookup"><span data-stu-id="f971a-204">On the **HttpConfiguration** object, the **ParameterBindingRules** property is a collection of anomymous functions of type (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**).</span></span> <span data-ttu-id="f971a-205">例如，可以添加任何 ETag 参数的 GET 方法上使用的规则`ETagParameterBinding`与`if-none-match`:</span><span class="sxs-lookup"><span data-stu-id="f971a-205">For example, you could add a rule that any ETag parameter on a GET method uses `ETagParameterBinding` with `if-none-match`:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

<span data-ttu-id="f971a-206">该函数应返回`null`参数绑定不适用。</span><span class="sxs-lookup"><span data-stu-id="f971a-206">The function should return `null` for parameters where the binding is not applicable.</span></span>

## <a name="iactionvaluebinder"></a><span data-ttu-id="f971a-207">IActionValueBinder</span><span class="sxs-lookup"><span data-stu-id="f971a-207">IActionValueBinder</span></span>

<span data-ttu-id="f971a-208">可插入的服务，由控制整个参数绑定过程**IActionValueBinder**。</span><span class="sxs-lookup"><span data-stu-id="f971a-208">The entire parameter-binding process is controlled by a pluggable service, **IActionValueBinder**.</span></span> <span data-ttu-id="f971a-209">默认实现**IActionValueBinder**执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="f971a-209">The default implementation of **IActionValueBinder** does the following:</span></span>

1. <span data-ttu-id="f971a-210">寻找**ParameterBindingAttribute**的参数。</span><span class="sxs-lookup"><span data-stu-id="f971a-210">Look for a **ParameterBindingAttribute** on the parameter.</span></span> <span data-ttu-id="f971a-211">这包括 **[FromBody]**， **[FromUri]**，并 **[ModelBinder]**，或自定义属性。</span><span class="sxs-lookup"><span data-stu-id="f971a-211">This includes **[FromBody]**, **[FromUri]**, and **[ModelBinder]**, or custom attributes.</span></span>
2. <span data-ttu-id="f971a-212">否则，在中，请**HttpConfiguration.ParameterBindingRules**函数返回非 null **HttpParameterBinding**。</span><span class="sxs-lookup"><span data-stu-id="f971a-212">Otherwise, look in **HttpConfiguration.ParameterBindingRules** for a function that returns a non-null **HttpParameterBinding**.</span></span>
3. <span data-ttu-id="f971a-213">否则，使用我先前介绍的默认规则。</span><span class="sxs-lookup"><span data-stu-id="f971a-213">Otherwise, use the default rules that I described previously.</span></span> 

    - <span data-ttu-id="f971a-214">如果参数类型为"简单"或具有从 URI 绑定的类型转换器。</span><span class="sxs-lookup"><span data-stu-id="f971a-214">If the parameter type is "simple"or has a type converter, bind from the URI.</span></span> <span data-ttu-id="f971a-215">这相当于将放 **[FromUri]** 参数上的属性。</span><span class="sxs-lookup"><span data-stu-id="f971a-215">This is equivalent to putting the **[FromUri]** attribute on the parameter.</span></span>
    - <span data-ttu-id="f971a-216">否则，尝试从消息正文读取参数。</span><span class="sxs-lookup"><span data-stu-id="f971a-216">Otherwise, try to read the parameter from the message body.</span></span> <span data-ttu-id="f971a-217">这相当于将放 **[FromBody]** 的参数。</span><span class="sxs-lookup"><span data-stu-id="f971a-217">This is equivalent to putting **[FromBody]** on the parameter.</span></span>

<span data-ttu-id="f971a-218">如果您希望，您可以替换为整个**IActionValueBinder**服务为自定义实现。</span><span class="sxs-lookup"><span data-stu-id="f971a-218">If you wanted, you could replace the entire **IActionValueBinder** service with a custom implementation.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f971a-219">其他资源</span><span class="sxs-lookup"><span data-stu-id="f971a-219">Additional Resources</span></span>

[<span data-ttu-id="f971a-220">自定义参数绑定示例</span><span class="sxs-lookup"><span data-stu-id="f971a-220">Custom Parameter Binding Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/CustomParameterBinding/ReadMe.txt)

<span data-ttu-id="f971a-221">Mike Stall 编写了有关 Web API 参数绑定的很好的一系列博客文章：</span><span class="sxs-lookup"><span data-stu-id="f971a-221">Mike Stall wrote a good series of blog posts about Web API parameter binding:</span></span>

- [<span data-ttu-id="f971a-222">Web API 如何执行参数绑定</span><span class="sxs-lookup"><span data-stu-id="f971a-222">How Web API does Parameter Binding</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [<span data-ttu-id="f971a-223">MVC 样式 Web api 的参数绑定</span><span class="sxs-lookup"><span data-stu-id="f971a-223">MVC Style parameter binding for Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [<span data-ttu-id="f971a-224">如何将绑定到 MVC/Web API 中的操作签名中的自定义对象</span><span class="sxs-lookup"><span data-stu-id="f971a-224">How to bind to custom objects in action signatures in MVC/Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [<span data-ttu-id="f971a-225">如何在 Web API 中创建的自定义值提供程序</span><span class="sxs-lookup"><span data-stu-id="f971a-225">How to create a custom value provider in Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [<span data-ttu-id="f971a-226">实质上的 web API 参数绑定</span><span class="sxs-lookup"><span data-stu-id="f971a-226">Web API Parameter binding under the hood</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
