---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: "JSON 和 ASP.NET Web API 中的 XML 序列化 |Microsoft 文档"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/30/2012
ms.topic: article
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: b1fcaf70cc38d73da0a454764520197b97f34b26
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="ec140-102">JSON 和 ASP.NET Web API 中的 XML 序列化</span><span class="sxs-lookup"><span data-stu-id="ec140-102">JSON and XML Serialization in ASP.NET Web API</span></span>
====================
<span data-ttu-id="ec140-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ec140-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ec140-104">本指南介绍了 ASP.NET Web API 中的 JSON 和 XML 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="ec140-104">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="ec140-105">在 ASP.NET Web API 中，*媒体类型格式化程序*是一个对象，可以：</span><span class="sxs-lookup"><span data-stu-id="ec140-105">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="ec140-106">读取 CLR 对象从 HTTP 消息正文</span><span class="sxs-lookup"><span data-stu-id="ec140-106">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="ec140-107">CLR 对象写入 HTTP 消息正文</span><span class="sxs-lookup"><span data-stu-id="ec140-107">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="ec140-108">Web API 提供对 JSON 和 XML 的媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="ec140-108">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="ec140-109">默认情况下，框架将这些格式化程序插入到管道。</span><span class="sxs-lookup"><span data-stu-id="ec140-109">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="ec140-110">客户端可以在 HTTP 请求的 Accept 标头中请求 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="ec140-110">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="ec140-111">内容</span><span class="sxs-lookup"><span data-stu-id="ec140-111">Contents</span></span>

- [<span data-ttu-id="ec140-112">JSON 媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="ec140-112">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="ec140-113">只读属性</span><span class="sxs-lookup"><span data-stu-id="ec140-113">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="ec140-114">日期</span><span class="sxs-lookup"><span data-stu-id="ec140-114">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="ec140-115">缩进</span><span class="sxs-lookup"><span data-stu-id="ec140-115">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="ec140-116">Camel 大小写形式</span><span class="sxs-lookup"><span data-stu-id="ec140-116">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="ec140-117">匿名和弱类型化对象</span><span class="sxs-lookup"><span data-stu-id="ec140-117">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="ec140-118">XML 媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="ec140-118">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="ec140-119">只读属性</span><span class="sxs-lookup"><span data-stu-id="ec140-119">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="ec140-120">日期</span><span class="sxs-lookup"><span data-stu-id="ec140-120">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="ec140-121">缩进</span><span class="sxs-lookup"><span data-stu-id="ec140-121">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="ec140-122">设置每个类型 XML 序列化程序</span><span class="sxs-lookup"><span data-stu-id="ec140-122">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="ec140-123">删除 JSON 或 XML 格式化程序</span><span class="sxs-lookup"><span data-stu-id="ec140-123">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="ec140-124">处理循环对象引用</span><span class="sxs-lookup"><span data-stu-id="ec140-124">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="ec140-125">测试对象序列化</span><span class="sxs-lookup"><span data-stu-id="ec140-125">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="ec140-126">JSON 媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="ec140-126">JSON Media-Type Formatter</span></span>

<span data-ttu-id="ec140-127">JSON 格式由**JsonMediaTypeFormatter**类。</span><span class="sxs-lookup"><span data-stu-id="ec140-127">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="ec140-128">默认情况下， **JsonMediaTypeFormatter**使用[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)库来执行序列化。</span><span class="sxs-lookup"><span data-stu-id="ec140-128">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="ec140-129">Json.NET 是一个第三方开源项目。</span><span class="sxs-lookup"><span data-stu-id="ec140-129">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="ec140-130">如果你愿意，你可以配置**JsonMediaTypeFormatter**类以使用**DataContractJsonSerializer**而不是 Json.NET。</span><span class="sxs-lookup"><span data-stu-id="ec140-130">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="ec140-131">为此，请设置**UseDataContractJsonSerializer**属性**true**:</span><span class="sxs-lookup"><span data-stu-id="ec140-131">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="ec140-132">JSON 序列化</span><span class="sxs-lookup"><span data-stu-id="ec140-132">JSON Serialization</span></span>

<span data-ttu-id="ec140-133">本部分介绍一些特定行为的 JSON 格式化程序，使用默认[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)序列化程序。</span><span class="sxs-lookup"><span data-stu-id="ec140-133">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="ec140-134">这并不意味着要 Json.NET library; 的综合文档有关详细信息，请参阅[Json.NET 文档](http://james.newtonking.com/projects/json/help/)。</span><span class="sxs-lookup"><span data-stu-id="ec140-134">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="ec140-135">什么获取序列化？</span><span class="sxs-lookup"><span data-stu-id="ec140-135">What Gets Serialized?</span></span>

<span data-ttu-id="ec140-136">默认情况下，所有公共属性和字段的序列化 JSON 中包括。</span><span class="sxs-lookup"><span data-stu-id="ec140-136">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="ec140-137">若要忽略的属性或字段，来修饰它与**JsonIgnore**属性。</span><span class="sxs-lookup"><span data-stu-id="ec140-137">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="ec140-138">如果你愿意&quot;参加&quot;方法，请修饰的类具有**DataContract**属性。</span><span class="sxs-lookup"><span data-stu-id="ec140-138">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="ec140-139">如果存在此属性，则将忽略成员，除非它们具有**DataMember**。</span><span class="sxs-lookup"><span data-stu-id="ec140-139">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="ec140-140">你还可以使用**DataMember**序列化私有成员。</span><span class="sxs-lookup"><span data-stu-id="ec140-140">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="ec140-141">只读属性</span><span class="sxs-lookup"><span data-stu-id="ec140-141">Read-Only Properties</span></span>

<span data-ttu-id="ec140-142">默认情况下，只读属性进行序列化。</span><span class="sxs-lookup"><span data-stu-id="ec140-142">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="ec140-143">日期</span><span class="sxs-lookup"><span data-stu-id="ec140-143">Dates</span></span>

<span data-ttu-id="ec140-144">默认情况下，Json.NET 日期中写入[ISO 8601](http://www.w3.org/TR/NOTE-datetime)格式。</span><span class="sxs-lookup"><span data-stu-id="ec140-144">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="ec140-145">UTC （协调世界时） 中的日期是编写使用"Z"后缀的。</span><span class="sxs-lookup"><span data-stu-id="ec140-145">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="ec140-146">本地时间的日期包括时区偏移量。</span><span class="sxs-lookup"><span data-stu-id="ec140-146">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="ec140-147">例如:</span><span class="sxs-lookup"><span data-stu-id="ec140-147">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="ec140-148">默认情况下，Json.NET 保留时区。</span><span class="sxs-lookup"><span data-stu-id="ec140-148">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="ec140-149">您可以替代此设置 DateTimeZoneHandling 属性：</span><span class="sxs-lookup"><span data-stu-id="ec140-149">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="ec140-150">如果你希望使用[Microsoft JSON 日期格式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb)(`"\/Date(ticks)\/"`) 而不是 ISO 8601 设置**DateFormatHandling**上序列化程序设置的属性：</span><span class="sxs-lookup"><span data-stu-id="ec140-150">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="ec140-151">缩进</span><span class="sxs-lookup"><span data-stu-id="ec140-151">Indenting</span></span>

<span data-ttu-id="ec140-152">若要编写缩进的 JSON，设置**格式**将设置为**当**:</span><span class="sxs-lookup"><span data-stu-id="ec140-152">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="ec140-153">Camel 大小写形式</span><span class="sxs-lookup"><span data-stu-id="ec140-153">Camel Casing</span></span>

<span data-ttu-id="ec140-154">若要编写 JSON 属性名以 camel 大小写形式，而无需更改你的数据模型，设置**CamelCasePropertyNamesContractResolver**上序列化程序：</span><span class="sxs-lookup"><span data-stu-id="ec140-154">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="ec140-155">匿名和弱类型化对象</span><span class="sxs-lookup"><span data-stu-id="ec140-155">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="ec140-156">操作方法可以返回匿名对象，其序列化为 JSON。</span><span class="sxs-lookup"><span data-stu-id="ec140-156">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="ec140-157">例如:</span><span class="sxs-lookup"><span data-stu-id="ec140-157">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="ec140-158">响应消息正文将包含以下 JSON:</span><span class="sxs-lookup"><span data-stu-id="ec140-158">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="ec140-159">如果你的 web API 接收松散结构从客户端的 JSON 对象，你可以反序列化请求正文为**Newtonsoft.Json.Linq.JObject**类型。</span><span class="sxs-lookup"><span data-stu-id="ec140-159">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="ec140-160">但是，则通常最好使用强类型化的数据对象。</span><span class="sxs-lookup"><span data-stu-id="ec140-160">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="ec140-161">然后，你无需自行，分析数据，获得模型验证的优点。</span><span class="sxs-lookup"><span data-stu-id="ec140-161">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="ec140-162">XML 序列化程序不支持匿名类型或**JObject**实例。</span><span class="sxs-lookup"><span data-stu-id="ec140-162">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="ec140-163">如果你将这些功能用于将 JSON 数据，您应该从管道中，删除 XML 格式化程序，如本文后面所述。</span><span class="sxs-lookup"><span data-stu-id="ec140-163">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="ec140-164">XML 媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="ec140-164">XML Media-Type Formatter</span></span>

<span data-ttu-id="ec140-165">XML 格式由**XmlMediaTypeFormatter**类。</span><span class="sxs-lookup"><span data-stu-id="ec140-165">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="ec140-166">默认情况下， **XmlMediaTypeFormatter**使用**DataContractSerializer**类来执行序列化。</span><span class="sxs-lookup"><span data-stu-id="ec140-166">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="ec140-167">如果你愿意，你可以配置**XmlMediaTypeFormatter**使用**XmlSerializer**而不是**DataContractSerializer**。</span><span class="sxs-lookup"><span data-stu-id="ec140-167">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="ec140-168">为此，请设置**UseXmlSerializer**属性**true**:</span><span class="sxs-lookup"><span data-stu-id="ec140-168">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="ec140-169">**XmlSerializer**类支持的类型，而不集较小**DataContractSerializer**，但提供更好地控制生成的 XML。</span><span class="sxs-lookup"><span data-stu-id="ec140-169">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="ec140-170">请考虑使用**XmlSerializer**如果你需要以匹配现有 XML 架构。</span><span class="sxs-lookup"><span data-stu-id="ec140-170">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="ec140-171">XML 序列化</span><span class="sxs-lookup"><span data-stu-id="ec140-171">XML Serialization</span></span>

<span data-ttu-id="ec140-172">本部分介绍一些特定行为的 XML 格式化程序，使用默认**DataContractSerializer**。</span><span class="sxs-lookup"><span data-stu-id="ec140-172">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="ec140-173">默认情况下，DataContractSerializer 的行为，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ec140-173">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="ec140-174">进行序列化所有公共读/写属性和字段。</span><span class="sxs-lookup"><span data-stu-id="ec140-174">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="ec140-175">若要忽略的属性或字段，来修饰它与**IgnoreDataMember**属性。</span><span class="sxs-lookup"><span data-stu-id="ec140-175">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="ec140-176">不序列化私有和受保护成员。</span><span class="sxs-lookup"><span data-stu-id="ec140-176">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="ec140-177">只读属性不会序列化。</span><span class="sxs-lookup"><span data-stu-id="ec140-177">Read-only properties are not serialized.</span></span> <span data-ttu-id="ec140-178">（但是，只读集合属性的内容进行序列化。）</span><span class="sxs-lookup"><span data-stu-id="ec140-178">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="ec140-179">类声明中显示的完全相同，将用 XML 编写类和成员名称。</span><span class="sxs-lookup"><span data-stu-id="ec140-179">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="ec140-180">使用默认 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="ec140-180">A default XML namespace is used.</span></span>

<span data-ttu-id="ec140-181">如果你需要更好地控制序列化，可以按照与类声明**DataContract**属性。</span><span class="sxs-lookup"><span data-stu-id="ec140-181">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="ec140-182">当存在此属性时，类序列，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ec140-182">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="ec140-183">&quot;选择加入&quot;方法： 属性和字段，默认情况下不序列化。</span><span class="sxs-lookup"><span data-stu-id="ec140-183">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="ec140-184">要序列化的属性或字段，来修饰它与**DataMember**属性。</span><span class="sxs-lookup"><span data-stu-id="ec140-184">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="ec140-185">要序列化的私有或受保护的成员，来修饰它与**DataMember**属性。</span><span class="sxs-lookup"><span data-stu-id="ec140-185">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="ec140-186">只读属性不会序列化。</span><span class="sxs-lookup"><span data-stu-id="ec140-186">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="ec140-187">若要更改的类名在 XML 中的显示方式，设置*名称*中的参数**DataContract**属性。</span><span class="sxs-lookup"><span data-stu-id="ec140-187">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="ec140-188">若要更改成员名称在 XML 中的显示方式，设置*名称*中的参数**DataMember**属性。</span><span class="sxs-lookup"><span data-stu-id="ec140-188">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="ec140-189">若要更改的 XML 命名空间，设置*Namespace*中的参数**DataContract**类。</span><span class="sxs-lookup"><span data-stu-id="ec140-189">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="ec140-190">只读属性</span><span class="sxs-lookup"><span data-stu-id="ec140-190">Read-Only Properties</span></span>

<span data-ttu-id="ec140-191">只读属性不会序列化。</span><span class="sxs-lookup"><span data-stu-id="ec140-191">Read-only properties are not serialized.</span></span> <span data-ttu-id="ec140-192">只读属性包含支持私有字段，你可以将标记具有的私有字段**DataMember**属性。</span><span class="sxs-lookup"><span data-stu-id="ec140-192">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="ec140-193">此方法要求**DataContract**类中的属性。</span><span class="sxs-lookup"><span data-stu-id="ec140-193">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="ec140-194">日期</span><span class="sxs-lookup"><span data-stu-id="ec140-194">Dates</span></span>

<span data-ttu-id="ec140-195">日期是采用 ISO 8601 格式编写的。</span><span class="sxs-lookup"><span data-stu-id="ec140-195">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="ec140-196">例如， &quot;2012年-05-23T20:21:37.9116538Z&quot;。</span><span class="sxs-lookup"><span data-stu-id="ec140-196">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="ec140-197">缩进</span><span class="sxs-lookup"><span data-stu-id="ec140-197">Indenting</span></span>

<span data-ttu-id="ec140-198">若要编写缩进的 XML，设置**缩进**属性**true**:</span><span class="sxs-lookup"><span data-stu-id="ec140-198">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="ec140-199">设置每个类型 XML 序列化程序</span><span class="sxs-lookup"><span data-stu-id="ec140-199">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="ec140-200">你可以为不同的 CLR 类型设置不同的 XML 序列化程序。</span><span class="sxs-lookup"><span data-stu-id="ec140-200">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="ec140-201">例如，你可能需要的特定数据对象**XmlSerializer**为了向后兼容。</span><span class="sxs-lookup"><span data-stu-id="ec140-201">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="ec140-202">你可以使用**XmlSerializer**此对象，并继续使用**DataContractSerializer**对于其他类型。</span><span class="sxs-lookup"><span data-stu-id="ec140-202">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="ec140-203">若要设置为特定类型的 XML 序列化程序，调用**SetSerializer**。</span><span class="sxs-lookup"><span data-stu-id="ec140-203">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="ec140-204">你可以指定**XmlSerializer**或派生自的任何对象**XmlObjectSerializer**。</span><span class="sxs-lookup"><span data-stu-id="ec140-204">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="ec140-205">删除 JSON 或 XML 格式化程序</span><span class="sxs-lookup"><span data-stu-id="ec140-205">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="ec140-206">如果不想要使用它们，可以从列表中的格式化程序，删除 JSON 格式化程序或 XML 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="ec140-206">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="ec140-207">若要这样做的主要原因如下：</span><span class="sxs-lookup"><span data-stu-id="ec140-207">The main reasons to do this are:</span></span>

- <span data-ttu-id="ec140-208">若要限制你对某个特定媒体类型的 web API 响应。</span><span class="sxs-lookup"><span data-stu-id="ec140-208">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="ec140-209">例如，你可能决定支持仅将 JSON 响应，并且删除 XML 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="ec140-209">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="ec140-210">若要将自定义格式化程序替换默认的格式化程序。</span><span class="sxs-lookup"><span data-stu-id="ec140-210">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="ec140-211">例如，你无法将 JSON 格式化程序替换自己的 JSON 格式化程序的自定义实现。</span><span class="sxs-lookup"><span data-stu-id="ec140-211">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="ec140-212">下面的代码演示如何删除默认格式化程序。</span><span class="sxs-lookup"><span data-stu-id="ec140-212">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="ec140-213">调用此成员，从你**应用程序\_启动**Global.asax 中定义的方法。</span><span class="sxs-lookup"><span data-stu-id="ec140-213">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="ec140-214">处理循环对象引用</span><span class="sxs-lookup"><span data-stu-id="ec140-214">Handling Circular Object References</span></span>

<span data-ttu-id="ec140-215">默认情况下，JSON 和 XML 格式化程序编写的所有对象作为值。</span><span class="sxs-lookup"><span data-stu-id="ec140-215">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="ec140-216">如果两个属性引用同一对象，或格式化程序两次在集合中显示相同的对象，如果将序列化对象两次。</span><span class="sxs-lookup"><span data-stu-id="ec140-216">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="ec140-217">如果这是特定问题对象图包含循环，因为它检测到循环关系图中时，序列化程序将引发异常。</span><span class="sxs-lookup"><span data-stu-id="ec140-217">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="ec140-218">请考虑下列对象模型和控制器。</span><span class="sxs-lookup"><span data-stu-id="ec140-218">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="ec140-219">调用此操作将导致格式化程序引发了异常，都会转换为状态代码 500 （内部服务器错误） 响应客户端。</span><span class="sxs-lookup"><span data-stu-id="ec140-219">Invoking this action will cause the formatter to thrown an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="ec140-220">若要保留 JSON 中的对象引用，以下代码添加到**应用程序\_启动**Global.asax 文件中的方法：</span><span class="sxs-lookup"><span data-stu-id="ec140-220">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="ec140-221">现在的控制器操作将返回类似如下所示的 JSON:</span><span class="sxs-lookup"><span data-stu-id="ec140-221">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="ec140-222">请注意，序列化程序将添加&quot;$id&quot;到这两个对象的属性。</span><span class="sxs-lookup"><span data-stu-id="ec140-222">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="ec140-223">此外，检测到 Employee.Department 属性创建一个循环，因此它将该值替换为一个对象引用: {&quot;$ref&quot;:&quot;1&quot;}。</span><span class="sxs-lookup"><span data-stu-id="ec140-223">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="ec140-224">对象引用不是标准 json 格式的。</span><span class="sxs-lookup"><span data-stu-id="ec140-224">Object references are not standard in JSON.</span></span> <span data-ttu-id="ec140-225">使用此功能之前，请考虑你的客户端是否将能够分析结果。</span><span class="sxs-lookup"><span data-stu-id="ec140-225">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="ec140-226">它可能是更好的做法只需从关系图删除周期。</span><span class="sxs-lookup"><span data-stu-id="ec140-226">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="ec140-227">例如，在此示例中不真正需要返回到部门员工的链接。</span><span class="sxs-lookup"><span data-stu-id="ec140-227">For example, the link from Employee back to Department is not really needed in this example.</span></span>


<span data-ttu-id="ec140-228">若要保留在 XML 中的对象引用，必须有两个选项。</span><span class="sxs-lookup"><span data-stu-id="ec140-228">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="ec140-229">更简单的选项是添加`[DataContract(IsReference=true)]`到模型类。</span><span class="sxs-lookup"><span data-stu-id="ec140-229">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="ec140-230">*IsReference*参数使对象引用。</span><span class="sxs-lookup"><span data-stu-id="ec140-230">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="ec140-231">请记住， **DataContract**选择加入，使序列化，因此你还需要添加**DataMember**属性的属性：</span><span class="sxs-lookup"><span data-stu-id="ec140-231">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="ec140-232">现在格式化程序将生成类似的 XML 如下：</span><span class="sxs-lookup"><span data-stu-id="ec140-232">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="ec140-233">如果你想要避免在模型类上的属性，则另一个选项： 创建新的类型的特定**DataContractSerializer**实例并设置*preserveObjectReferences*到**true**构造函数中。</span><span class="sxs-lookup"><span data-stu-id="ec140-233">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="ec140-234">然后将设置此实例为每个类型序列化程序在 XML 媒体类型格式化程序上。</span><span class="sxs-lookup"><span data-stu-id="ec140-234">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="ec140-235">以下代码演示如何执行此操作：</span><span class="sxs-lookup"><span data-stu-id="ec140-235">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="ec140-236">测试对象序列化</span><span class="sxs-lookup"><span data-stu-id="ec140-236">Testing Object Serialization</span></span>

<span data-ttu-id="ec140-237">设计你的 web API 时，它可用于测试你的数据对象将序列化。</span><span class="sxs-lookup"><span data-stu-id="ec140-237">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="ec140-238">你可以执行此操作而无需创建控制器或调用的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="ec140-238">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
