---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: "ASP.NET Web API 中的绑定的参数 |Microsoft 文档"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/11/2013
ms.topic: article
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 5aa532137436922519c86246ebfa834910ac0d86
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="parameter-binding-in-aspnet-web-api"></a><span data-ttu-id="3348a-102">ASP.NET Web API 中的绑定的参数</span><span class="sxs-lookup"><span data-stu-id="3348a-102">Parameter Binding in ASP.NET Web API</span></span>
====================
<span data-ttu-id="3348a-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3348a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="3348a-104">在 Web API 在控制器上调用方法，它必须设置的参数，调用进程值*绑定*。</span><span class="sxs-lookup"><span data-stu-id="3348a-104">When Web API calls a method on a controller, it must set values for the parameters, a process called *binding*.</span></span> <span data-ttu-id="3348a-105">本文介绍了如何 Web API 绑定参数，以及如何自定义绑定过程。</span><span class="sxs-lookup"><span data-stu-id="3348a-105">This article describes how Web API binds parameters, and how you can customize the binding process.</span></span>

<span data-ttu-id="3348a-106">默认情况下，Web API 使用以下规则来将参数绑定：</span><span class="sxs-lookup"><span data-stu-id="3348a-106">By default, Web API uses the following rules to bind parameters:</span></span>

- <span data-ttu-id="3348a-107">如果参数为"简单"的类型，Web API 将尝试从 URI 中获取的值。</span><span class="sxs-lookup"><span data-stu-id="3348a-107">If the parameter is a "simple" type, Web API tries to get the value from the URI.</span></span> <span data-ttu-id="3348a-108">简单类型包括.NET[基元类型](https://msdn.microsoft.com/library/system.type.isprimitive.aspx)(**int**， **bool**， **double**，依此类推)，加上**TimeSpan**， **DateTime**， **Guid**，**十进制**，和**字符串**，*加上*任何类型具有可以从字符串转换的类型转换器。</span><span class="sxs-lookup"><span data-stu-id="3348a-108">Simple types include the .NET [primitive types](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, and so forth), plus **TimeSpan**, **DateTime**, **Guid**, **decimal**, and **string**, *plus* any type with a type converter that can convert from a string.</span></span> <span data-ttu-id="3348a-109">（有关详细信息的类型转换器更高版本。）</span><span class="sxs-lookup"><span data-stu-id="3348a-109">(More about type converters later.)</span></span>
- <span data-ttu-id="3348a-110">为复杂类型，Web API 尝试从消息正文中读取值时，使用[媒体类型格式化程序](media-formatters.md)。</span><span class="sxs-lookup"><span data-stu-id="3348a-110">For complex types, Web API tries to read the value from the message body, using a [media-type formatter](media-formatters.md).</span></span>

<span data-ttu-id="3348a-111">例如，以下是典型的 Web API 控制器方法：</span><span class="sxs-lookup"><span data-stu-id="3348a-111">For example, here is a typical Web API controller method:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="3348a-112">*Id*参数是&quot;简单&quot;类型，因此 Web API 尝试于请求 URI 中获取的值。</span><span class="sxs-lookup"><span data-stu-id="3348a-112">The *id* parameter is a &quot;simple&quot; type, so Web API tries to get the value from the request URI.</span></span> <span data-ttu-id="3348a-113">*项*参数是一个复杂类型，因此 Web API 使用的媒体类型格式化程序以从请求正文中读取值。</span><span class="sxs-lookup"><span data-stu-id="3348a-113">The *item* parameter is a complex type, so Web API uses a media-type formatter to read the value from the request body.</span></span>

<span data-ttu-id="3348a-114">若要从 URI 中获取一个值，Web API，查找路线数据和 URI 查询字符串中。</span><span class="sxs-lookup"><span data-stu-id="3348a-114">To get a value from the URI, Web API looks in the route data and the URI query string.</span></span> <span data-ttu-id="3348a-115">路由系统分析 URI 和匹配到某个路由时，填充路线数据。</span><span class="sxs-lookup"><span data-stu-id="3348a-115">The route data is populated when the routing system parses the URI and matches it to a route.</span></span> <span data-ttu-id="3348a-116">有关详细信息，请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="3348a-116">For more information, see [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span>

<span data-ttu-id="3348a-117">在本文的其余部分，我将展示如何自定义模型绑定过程。</span><span class="sxs-lookup"><span data-stu-id="3348a-117">In the rest of this article, I'll show how you can customize the model binding process.</span></span> <span data-ttu-id="3348a-118">对于复杂类型，但是，考虑使用只要有可能的媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="3348a-118">For complex types, however, consider using media-type formatters whenever possible.</span></span> <span data-ttu-id="3348a-119">HTTP 的关键原则在于，资源发送在消息正文中，使用内容协商指定的资源表示形式。</span><span class="sxs-lookup"><span data-stu-id="3348a-119">A key principle of HTTP is that resources are sent in the message body, using content negotiation to specify the representation of the resource.</span></span> <span data-ttu-id="3348a-120">为此，设计媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="3348a-120">Media-type formatters were designed for exactly this purpose.</span></span>

## <a name="using-fromuri"></a><span data-ttu-id="3348a-121">使用 [FromUri]</span><span class="sxs-lookup"><span data-stu-id="3348a-121">Using [FromUri]</span></span>

<span data-ttu-id="3348a-122">若要强制 Web API 以读取复杂类型的 URI 中，添加**[FromUri]**属性设为参数。</span><span class="sxs-lookup"><span data-stu-id="3348a-122">To force Web API to read a complex type from the URI, add the **[FromUri]** attribute to the parameter.</span></span> <span data-ttu-id="3348a-123">下面的示例定义`GeoPoint`类型，以及获取控制器方法`GeoPoint`从 URI。</span><span class="sxs-lookup"><span data-stu-id="3348a-123">The following example defines a `GeoPoint` type, along with a controller method that gets the `GeoPoint` from the URI.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="3348a-124">客户端可以将纬度和经度值放在查询字符串和 Web API 将使用它们来构造`GeoPoint`。</span><span class="sxs-lookup"><span data-stu-id="3348a-124">The client can put the Latitude and Longitude values in the query string and Web API will use them to construct a `GeoPoint`.</span></span> <span data-ttu-id="3348a-125">例如:</span><span class="sxs-lookup"><span data-stu-id="3348a-125">For example:</span></span>

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a><span data-ttu-id="3348a-126">使用 [FromBody]</span><span class="sxs-lookup"><span data-stu-id="3348a-126">Using [FromBody]</span></span>

<span data-ttu-id="3348a-127">若要强制 Web API 以从请求正文读取简单类型，添加**[FromBody]**属性设为参数：</span><span class="sxs-lookup"><span data-stu-id="3348a-127">To force Web API to read a simple type from the request body, add the **[FromBody]** attribute to the parameter:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="3348a-128">在此示例中，Web API 将使用媒体类型格式化程序读取的值*名称*从请求正文。</span><span class="sxs-lookup"><span data-stu-id="3348a-128">In this example, Web API will use a media-type formatter to read the value of *name* from the request body.</span></span> <span data-ttu-id="3348a-129">下面是一个示例客户端请求。</span><span class="sxs-lookup"><span data-stu-id="3348a-129">Here is an example client request.</span></span>

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

<span data-ttu-id="3348a-130">当参数具有 [FromBody] 时，Web API 使用的内容类型标头选择格式化程序。</span><span class="sxs-lookup"><span data-stu-id="3348a-130">When a parameter has [FromBody], Web API uses the Content-Type header to select a formatter.</span></span> <span data-ttu-id="3348a-131">在此示例中，内容类型是&quot;应用程序/json&quot;和请求正文是原始的 JSON 字符串 （不是一个 JSON 对象）。</span><span class="sxs-lookup"><span data-stu-id="3348a-131">In this example, the content type is &quot;application/json&quot; and the request body is a raw JSON string (not a JSON object).</span></span>

<span data-ttu-id="3348a-132">最多一个参数允许从消息正文中读取。</span><span class="sxs-lookup"><span data-stu-id="3348a-132">At most one parameter is allowed to read from the message body.</span></span> <span data-ttu-id="3348a-133">因此这不起作用：</span><span class="sxs-lookup"><span data-stu-id="3348a-133">So this will not work:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="3348a-134">此规则的原因是，请求正文可能存储在只读取一次的非缓冲的流。</span><span class="sxs-lookup"><span data-stu-id="3348a-134">The reason for this rule is that the request body might be stored in a non-buffered stream that can only be read once.</span></span>

## <a name="type-converters"></a><span data-ttu-id="3348a-135">类型转换器</span><span class="sxs-lookup"><span data-stu-id="3348a-135">Type Converters</span></span>

<span data-ttu-id="3348a-136">你可以将类视为简单类型，（以便 Web API 将尝试将其绑定从 URI） 的 Web API 通过创建**TypeConverter**并提供字符串转换。</span><span class="sxs-lookup"><span data-stu-id="3348a-136">You can make Web API treat a class as a simple type (so that Web API will try to bind it from the URI) by creating a **TypeConverter** and providing a string conversion.</span></span>

<span data-ttu-id="3348a-137">下面的代码演示`GeoPoint`类表示一个地理点，加上**TypeConverter** ，用于从字符串转换为将转换`GeoPoint`实例。</span><span class="sxs-lookup"><span data-stu-id="3348a-137">The following code shows a `GeoPoint` class that represents a geographical point, plus a **TypeConverter** that converts from strings to `GeoPoint` instances.</span></span> <span data-ttu-id="3348a-138">`GeoPoint`类用修饰**[TypeConverter]**特性以指定的类型转换器。</span><span class="sxs-lookup"><span data-stu-id="3348a-138">The `GeoPoint` class is decorated with a **[TypeConverter]** attribute to specify the type converter.</span></span> <span data-ttu-id="3348a-139">(此示例已由 Mike 停止的博客文章激发[如何将绑定到 MVC/WebAPI 中的操作签名中的自定义对象](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)。)</span><span class="sxs-lookup"><span data-stu-id="3348a-139">(This example was inspired by Mike Stall's blog post [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="3348a-140">现在 Web API 会将`GeoPoint`为简单类型，这意味着它将尝试将绑定`GeoPoint`URI 中的参数。</span><span class="sxs-lookup"><span data-stu-id="3348a-140">Now Web API will treat `GeoPoint` as a simple type, meaning it will try to bind `GeoPoint` parameters from the URI.</span></span> <span data-ttu-id="3348a-141">无需包括**[FromUri]**的参数。</span><span class="sxs-lookup"><span data-stu-id="3348a-141">You don't need to include **[FromUri]** on the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="3348a-142">客户端可以调用具有如下 URI 的方法：</span><span class="sxs-lookup"><span data-stu-id="3348a-142">The client can invoke the method with a URI like this:</span></span>

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a><span data-ttu-id="3348a-143">模型联编程序</span><span class="sxs-lookup"><span data-stu-id="3348a-143">Model Binders</span></span>

<span data-ttu-id="3348a-144">比类型转换器更灵活的选项是创建自定义模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="3348a-144">A more flexible option than a type converter is to create a custom model binder.</span></span> <span data-ttu-id="3348a-145">模型联编程序，与你拥有访问权限等 HTTP 请求、 操作说明和的原始值从路线数据。</span><span class="sxs-lookup"><span data-stu-id="3348a-145">With a model binder, you have access to things like the HTTP request, the action description, and the raw values from the route data.</span></span>

<span data-ttu-id="3348a-146">若要创建模型联编程序，实现**IModelBinder**接口。</span><span class="sxs-lookup"><span data-stu-id="3348a-146">To create a model binder, implement the **IModelBinder** interface.</span></span> <span data-ttu-id="3348a-147">此接口定义单个方法**BindModel**:</span><span class="sxs-lookup"><span data-stu-id="3348a-147">This interface defines a single method, **BindModel**:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

<span data-ttu-id="3348a-148">下面是模型联编程序`GeoPoint`对象。</span><span class="sxs-lookup"><span data-stu-id="3348a-148">Here is a model binder for `GeoPoint` objects.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="3348a-149">模型联编程序获取原始输入的值从*值提供程序*。</span><span class="sxs-lookup"><span data-stu-id="3348a-149">A model binder gets raw input values from a *value provider*.</span></span> <span data-ttu-id="3348a-150">这种设计将分隔两个不同的功能：</span><span class="sxs-lookup"><span data-stu-id="3348a-150">This design separates two distinct functions:</span></span>

- <span data-ttu-id="3348a-151">值提供程序获取 HTTP 请求，并填充键 / 值对的字典。</span><span class="sxs-lookup"><span data-stu-id="3348a-151">The value provider takes the HTTP request and populates a dictionary of key-value pairs.</span></span>
- <span data-ttu-id="3348a-152">模型联编程序使用此字典来填充模型。</span><span class="sxs-lookup"><span data-stu-id="3348a-152">The model binder uses this dictionary to populate the model.</span></span>

<span data-ttu-id="3348a-153">Web API 中的默认值提供程序从路由数据和查询字符串中获取值。</span><span class="sxs-lookup"><span data-stu-id="3348a-153">The default value provider in Web API gets values from the route data and the query string.</span></span> <span data-ttu-id="3348a-154">例如，如果的 URI 是`http://localhost/api/values/1?location=48,-122`，值提供程序创建以下的键 / 值对：</span><span class="sxs-lookup"><span data-stu-id="3348a-154">For example, if the URI is `http://localhost/api/values/1?location=48,-122`, the value provider creates the following key-value pairs:</span></span>

- <span data-ttu-id="3348a-155">id = &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="3348a-155">id = &quot;1&quot;</span></span>
- <span data-ttu-id="3348a-156">位置 = &quot;48,122&quot;</span><span class="sxs-lookup"><span data-stu-id="3348a-156">location = &quot;48,122&quot;</span></span>

<span data-ttu-id="3348a-157">(假设默认路由模板，这是&quot;api / {controller} / {id}&quot;。)</span><span class="sxs-lookup"><span data-stu-id="3348a-157">(I'm assuming the default route template, which is &quot;api/{controller}/{id}&quot;.)</span></span>

<span data-ttu-id="3348a-158">要绑定的参数的名称存储在**ModelBindingContext.ModelName**属性。</span><span class="sxs-lookup"><span data-stu-id="3348a-158">The name of the parameter to bind is stored in the **ModelBindingContext.ModelName** property.</span></span> <span data-ttu-id="3348a-159">模型联编程序看起来与此值在字典中的键。</span><span class="sxs-lookup"><span data-stu-id="3348a-159">The model binder looks for a key with this value in the dictionary.</span></span> <span data-ttu-id="3348a-160">如果值存在，并且可以转换为`GeoPoint`，模型联编程序将该绑定的值赋给**ModelBindingContext.Model**属性。</span><span class="sxs-lookup"><span data-stu-id="3348a-160">If the value exists and can be converted into a `GeoPoint`, the model binder assigns the bound value to the **ModelBindingContext.Model** property.</span></span>

<span data-ttu-id="3348a-161">请注意，模型联编程序不限于简单类型转换。</span><span class="sxs-lookup"><span data-stu-id="3348a-161">Notice that the model binder is not limited to a simple type conversion.</span></span> <span data-ttu-id="3348a-162">在此示例中，模型联编程序首先查找已知位置，表中，如果失败，它使用类型转换。</span><span class="sxs-lookup"><span data-stu-id="3348a-162">In this example, the model binder first looks in a table of known locations, and if that fails, it uses type conversion.</span></span>

<span data-ttu-id="3348a-163">**设置模型联编程序**</span><span class="sxs-lookup"><span data-stu-id="3348a-163">**Setting the Model Binder**</span></span>

<span data-ttu-id="3348a-164">有多种方法来设置模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="3348a-164">There are several ways to set a model binder.</span></span> <span data-ttu-id="3348a-165">首先，您可以添加**[ModelBinder]**属性设为参数。</span><span class="sxs-lookup"><span data-stu-id="3348a-165">First, you can add a **[ModelBinder]** attribute to the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

<span data-ttu-id="3348a-166">你还可以添加**[ModelBinder]**属性类型。</span><span class="sxs-lookup"><span data-stu-id="3348a-166">You can also add a **[ModelBinder]** attribute to the type.</span></span> <span data-ttu-id="3348a-167">Web API 将使用指定的模型联编程序为该类型的所有参数。</span><span class="sxs-lookup"><span data-stu-id="3348a-167">Web API will use the specified model binder for all parameters of that type.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="3348a-168">最后，你可以添加到模型联编程序提供程序**HttpConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="3348a-168">Finally, you can add a model-binder provider to the **HttpConfiguration**.</span></span> <span data-ttu-id="3348a-169">模型联编程序提供程序是只需创建模型联编程序的工厂类。</span><span class="sxs-lookup"><span data-stu-id="3348a-169">A model-binder provider is simply a factory class that creates a model binder.</span></span> <span data-ttu-id="3348a-170">你可以通过从派生创建提供程序[ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx)类。</span><span class="sxs-lookup"><span data-stu-id="3348a-170">You can create a provider by deriving from the [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) class.</span></span> <span data-ttu-id="3348a-171">但是，如果模型联编程序处理的单一类型，很容易地使用内置**SimpleModelBinderProvider**，为此用途设计的。</span><span class="sxs-lookup"><span data-stu-id="3348a-171">However, if your model binder handles a single type, it's easier to use the built-in **SimpleModelBinderProvider**, which is designed for this purpose.</span></span> <span data-ttu-id="3348a-172">下面的代码演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="3348a-172">The following code shows how to do this.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

<span data-ttu-id="3348a-173">使用模型绑定提供程序，你仍需要添加**[ModelBinder]**属性设为参数，以告知 Web API，它应使用模型联编程序和不格式化程序媒体类型。</span><span class="sxs-lookup"><span data-stu-id="3348a-173">With a model-binding provider, you still need to add the **[ModelBinder]** attribute to the parameter, to tell Web API that it should use a model binder and not a media-type formatter.</span></span> <span data-ttu-id="3348a-174">但是，现在你无需在属性中指定的一种模型联编程序：</span><span class="sxs-lookup"><span data-stu-id="3348a-174">But now you don't need to specify the type of model binder in the attribute:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a><span data-ttu-id="3348a-175">值在提供程序</span><span class="sxs-lookup"><span data-stu-id="3348a-175">Value Providers</span></span>

<span data-ttu-id="3348a-176">我所述模型联编程序从值提供程序中获取值。</span><span class="sxs-lookup"><span data-stu-id="3348a-176">I mentioned that a model binder gets values from a value provider.</span></span> <span data-ttu-id="3348a-177">若要编写一个自定义值提供程序，实现**IValueProvider**接口。</span><span class="sxs-lookup"><span data-stu-id="3348a-177">To write a custom value provider, implement the **IValueProvider** interface.</span></span> <span data-ttu-id="3348a-178">下面是在请求中提取 cookie 中的值示例：</span><span class="sxs-lookup"><span data-stu-id="3348a-178">Here is an example that pulls values from the cookies in the request:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

<span data-ttu-id="3348a-179">你还需要通过从派生来创建值提供程序工厂**ValueProviderFactory**类。</span><span class="sxs-lookup"><span data-stu-id="3348a-179">You also need to create a value provider factory by deriving from the **ValueProviderFactory** class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

<span data-ttu-id="3348a-180">添加到值提供程序工厂**HttpConfiguration** ，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3348a-180">Add the value provider factory to the **HttpConfiguration** as follows.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

<span data-ttu-id="3348a-181">Web API 编写的所有值提供程序，因此当模型联编程序调用**ValueProvider.GetValue**，模型联编程序从第一个值提供程序能够生成它接收的值。</span><span class="sxs-lookup"><span data-stu-id="3348a-181">Web API composes all of the value providers, so when a model binder calls **ValueProvider.GetValue**, the model binder receives the value from the first value provider that is able to produce it.</span></span>

<span data-ttu-id="3348a-182">或者，通过使用，在参数级别设置的值提供程序工厂**ValueProvider**特性，，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3348a-182">Alternatively, you can set the value provider factory at the parameter level by using the **ValueProvider** attribute, as follows:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

<span data-ttu-id="3348a-183">这将告知 Web API，以便使用指定的值提供程序工厂，使用模型绑定，并不是使用任何其他已注册的值提供程序。</span><span class="sxs-lookup"><span data-stu-id="3348a-183">This tells Web API to use model binding with the specified value provider factory, and not to use any of the other registered value providers.</span></span>

## <a name="httpparameterbinding"></a><span data-ttu-id="3348a-184">HttpParameterBinding</span><span class="sxs-lookup"><span data-stu-id="3348a-184">HttpParameterBinding</span></span>

<span data-ttu-id="3348a-185">模型联编程序是更多常规机制的特定实例。</span><span class="sxs-lookup"><span data-stu-id="3348a-185">Model binders are a specific instance of a more general mechanism.</span></span> <span data-ttu-id="3348a-186">如果你看一下**[ModelBinder]**属性中，你将看到它派生自抽象**ParameterBindingAttribute**类。</span><span class="sxs-lookup"><span data-stu-id="3348a-186">If you look at the **[ModelBinder]** attribute, you will see that it derives from the abstract **ParameterBindingAttribute** class.</span></span> <span data-ttu-id="3348a-187">此类定义一个方法， **GetBinding**，它将返回**HttpParameterBinding**对象：</span><span class="sxs-lookup"><span data-stu-id="3348a-187">This class defines a single method, **GetBinding**, which returns an **HttpParameterBinding** object:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

<span data-ttu-id="3348a-188">**HttpParameterBinding**负责参数绑定到一个值。</span><span class="sxs-lookup"><span data-stu-id="3348a-188">An **HttpParameterBinding** is responsible for binding a parameter to a value.</span></span> <span data-ttu-id="3348a-189">情况下**[ModelBinder]**，属性将返回**HttpParameterBinding**使用的实现**IModelBinder**若要执行实际绑定。</span><span class="sxs-lookup"><span data-stu-id="3348a-189">In the case of **[ModelBinder]**, the attribute returns an **HttpParameterBinding** implementation that uses an **IModelBinder** to perform the actual binding.</span></span> <span data-ttu-id="3348a-190">你还可以实现你自己**HttpParameterBinding**。</span><span class="sxs-lookup"><span data-stu-id="3348a-190">You can also implement your own **HttpParameterBinding**.</span></span>

<span data-ttu-id="3348a-191">例如，假设你想要获取从 Etag`if-match`和`if-none-match`在请求中的标头。</span><span class="sxs-lookup"><span data-stu-id="3348a-191">For example, suppose you want to get ETags from `if-match` and `if-none-match` headers in the request.</span></span> <span data-ttu-id="3348a-192">我们将开始通过定义一个类来表示 Etag。</span><span class="sxs-lookup"><span data-stu-id="3348a-192">We'll start by defining a class to represent ETags.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

<span data-ttu-id="3348a-193">我们还将定义一个枚举，以指示是否获取从 ETag`if-match`标头或`if-none-match`标头。</span><span class="sxs-lookup"><span data-stu-id="3348a-193">We'll also define an enumeration to indicate whether to get the ETag from the `if-match` header or the `if-none-match` header.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

<span data-ttu-id="3348a-194">下面是**HttpParameterBinding** ，从所需标头获取 ETag，并将其绑定到类型 ETag 的参数：</span><span class="sxs-lookup"><span data-stu-id="3348a-194">Here is an **HttpParameterBinding** that gets the ETag from the desired header and binds it to a parameter of type ETag:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

<span data-ttu-id="3348a-195">**ExecuteBindingAsync**方法执行绑定。</span><span class="sxs-lookup"><span data-stu-id="3348a-195">The **ExecuteBindingAsync** method does the binding.</span></span> <span data-ttu-id="3348a-196">在这种方法，添加到绑定的参数值**ActionArgument**字典中的**HttpActionContext**。</span><span class="sxs-lookup"><span data-stu-id="3348a-196">Within this method, add the bound parameter value to the **ActionArgument** dictionary in the **HttpActionContext**.</span></span>

> [!NOTE]
> <span data-ttu-id="3348a-197">如果你**ExecuteBindingAsync**方法读取请求消息的正文，请重写**WillReadBody**属性返回 true。</span><span class="sxs-lookup"><span data-stu-id="3348a-197">If your **ExecuteBindingAsync** method reads the body of the request message, override the **WillReadBody** property to return true.</span></span> <span data-ttu-id="3348a-198">请求正文可能只能读取一次，因此 Web API 会强制实现一个规则，最多其中一个绑定未缓冲的数据流可以读取消息正文。</span><span class="sxs-lookup"><span data-stu-id="3348a-198">The request body might be an unbuffered stream that can only be read once, so Web API enforces a rule that at most one binding can read the message body.</span></span>


<span data-ttu-id="3348a-199">要应用自定义**HttpParameterBinding**，您可以定义属性派生自**ParameterBindingAttribute**。</span><span class="sxs-lookup"><span data-stu-id="3348a-199">To apply a custom **HttpParameterBinding**, you can define an attribute that derives from **ParameterBindingAttribute**.</span></span> <span data-ttu-id="3348a-200">有关`ETagParameterBinding`，我们将定义两个属性，一个用于`if-match`标头和一个用于`if-none-match`标头。</span><span class="sxs-lookup"><span data-stu-id="3348a-200">For `ETagParameterBinding`, we'll define two attributes, one for `if-match` headers and one for `if-none-match` headers.</span></span> <span data-ttu-id="3348a-201">都派生自抽象基类。</span><span class="sxs-lookup"><span data-stu-id="3348a-201">Both derive from an abstract base class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

<span data-ttu-id="3348a-202">下面是使用一个控制器方法`[IfNoneMatch]`属性。</span><span class="sxs-lookup"><span data-stu-id="3348a-202">Here is a controller method that uses the `[IfNoneMatch]` attribute.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

<span data-ttu-id="3348a-203">除了**ParameterBindingAttribute**，没有用于添加自定义的另一个挂钩**HttpParameterBinding**。</span><span class="sxs-lookup"><span data-stu-id="3348a-203">Besides **ParameterBindingAttribute**, there is another hook for adding a custom **HttpParameterBinding**.</span></span> <span data-ttu-id="3348a-204">上**HttpConfiguration**对象， **ParameterBindingRules**属性是 anomymous 函数的类型的集合 (**HttpParameterDescriptor**  - &gt; **HttpParameterBinding**)。</span><span class="sxs-lookup"><span data-stu-id="3348a-204">On the **HttpConfiguration** object, the **ParameterBindingRules** property is a collection of anomymous functions of type (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**).</span></span> <span data-ttu-id="3348a-205">例如，可以添加任何 ETag 参数的 GET 方法使用的规则`ETagParameterBinding`与`if-none-match`:</span><span class="sxs-lookup"><span data-stu-id="3348a-205">For example, you could add a rule that any ETag parameter on a GET method uses `ETagParameterBinding` with `if-none-match`:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

<span data-ttu-id="3348a-206">该函数应返回`null`参数绑定不适用。</span><span class="sxs-lookup"><span data-stu-id="3348a-206">The function should return `null` for parameters where the binding is not applicable.</span></span>

## <a name="iactionvaluebinder"></a><span data-ttu-id="3348a-207">IActionValueBinder</span><span class="sxs-lookup"><span data-stu-id="3348a-207">IActionValueBinder</span></span>

<span data-ttu-id="3348a-208">由可插入的服务，控制整个参数绑定过程**IActionValueBinder**。</span><span class="sxs-lookup"><span data-stu-id="3348a-208">The entire parameter-binding process is controlled by a pluggable service, **IActionValueBinder**.</span></span> <span data-ttu-id="3348a-209">默认实现**IActionValueBinder**执行下列任务：</span><span class="sxs-lookup"><span data-stu-id="3348a-209">The default implementation of **IActionValueBinder** does the following:</span></span>

1. <span data-ttu-id="3348a-210">查找**ParameterBindingAttribute**的参数。</span><span class="sxs-lookup"><span data-stu-id="3348a-210">Look for a **ParameterBindingAttribute** on the parameter.</span></span> <span data-ttu-id="3348a-211">这包括**[FromBody]**， **[FromUri]**，和**[ModelBinder]**，或自定义属性。</span><span class="sxs-lookup"><span data-stu-id="3348a-211">This includes **[FromBody]**, **[FromUri]**, and **[ModelBinder]**, or custom attributes.</span></span>
2. <span data-ttu-id="3348a-212">否则，查找**HttpConfiguration.ParameterBindingRules**函数返回非 null **HttpParameterBinding**。</span><span class="sxs-lookup"><span data-stu-id="3348a-212">Otherwise, look in **HttpConfiguration.ParameterBindingRules** for a function that returns a non-null **HttpParameterBinding**.</span></span>
3. <span data-ttu-id="3348a-213">否则，请使用我以前所述的默认规则。</span><span class="sxs-lookup"><span data-stu-id="3348a-213">Otherwise, use the default rules that I described previously.</span></span> 

    - <span data-ttu-id="3348a-214">如果参数类型是"简单"，或者有 URI 中将绑定的类型转换器。</span><span class="sxs-lookup"><span data-stu-id="3348a-214">If the parameter type is "simple"or has a type converter, bind from the URI.</span></span> <span data-ttu-id="3348a-215">这相当于加上**[FromUri]**参数上的属性。</span><span class="sxs-lookup"><span data-stu-id="3348a-215">This is equivalent to putting the **[FromUri]** attribute on the parameter.</span></span>
    - <span data-ttu-id="3348a-216">否则，尝试从消息正文读取参数。</span><span class="sxs-lookup"><span data-stu-id="3348a-216">Otherwise, try to read the parameter from the message body.</span></span> <span data-ttu-id="3348a-217">这相当于加上**[FromBody]**的参数。</span><span class="sxs-lookup"><span data-stu-id="3348a-217">This is equivalent to putting **[FromBody]** on the parameter.</span></span>

<span data-ttu-id="3348a-218">如果你想要则无法将整个**IActionValueBinder**服务为自定义实现。</span><span class="sxs-lookup"><span data-stu-id="3348a-218">If you wanted, you could replace the entire **IActionValueBinder** service with a custom implementation.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3348a-219">其他资源</span><span class="sxs-lookup"><span data-stu-id="3348a-219">Additional Resources</span></span>

[<span data-ttu-id="3348a-220">自定义参数绑定示例</span><span class="sxs-lookup"><span data-stu-id="3348a-220">Custom Parameter Binding Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/CustomParameterBinding/ReadMe.txt)

<span data-ttu-id="3348a-221">Mike 停止写下了很好的博客文章有关 Web API 参数绑定：</span><span class="sxs-lookup"><span data-stu-id="3348a-221">Mike Stall wrote a good series of blog posts about Web API parameter binding:</span></span>

- [<span data-ttu-id="3348a-222">Web API 原理参数绑定</span><span class="sxs-lookup"><span data-stu-id="3348a-222">How Web API does Parameter Binding</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [<span data-ttu-id="3348a-223">Web API 的 MVC 样式参数绑定</span><span class="sxs-lookup"><span data-stu-id="3348a-223">MVC Style parameter binding for Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [<span data-ttu-id="3348a-224">如何将绑定到 MVC/Web API 中的操作签名中的自定义对象</span><span class="sxs-lookup"><span data-stu-id="3348a-224">How to bind to custom objects in action signatures in MVC/Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [<span data-ttu-id="3348a-225">如何在 Web API 中创建自定义值提供程序</span><span class="sxs-lookup"><span data-stu-id="3348a-225">How to create a custom value provider in Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [<span data-ttu-id="3348a-226">实质上的 web API 参数绑定</span><span class="sxs-lookup"><span data-stu-id="3348a-226">Web API Parameter binding under the hood</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
