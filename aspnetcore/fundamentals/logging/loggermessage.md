---
title: "在 ASP.NET Core 中使用 LoggerMessage 的高性能日志记录"
author: guardrex
description: "了解如何使用 LoggerMessage 功能（对于高性能日志记录方案，该功能比记录器扩展方法需要的对象分配少）创建可缓存的委托。"
manager: wpickett
ms.author: riande
ms.date: 11/03/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/logging/loggermessage
ms.openlocfilehash: b155826b5047e88a79d9e339d7bca8885a79006d
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="high-performance-logging-with-loggermessage-in-aspnet-core"></a><span data-ttu-id="8bc87-103">在 ASP.NET Core 中使用 LoggerMessage 的高性能日志记录</span><span class="sxs-lookup"><span data-stu-id="8bc87-103">High-performance logging with LoggerMessage in ASP.NET Core</span></span>

<span data-ttu-id="8bc87-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="8bc87-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="8bc87-105">[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) 功能创建可缓存的委托，该功能比[记录器扩展方法](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions)（例如 `LogInformation`、`LogDebug` 和 `LogError`）需要的对象分配和计算开销少。</span><span class="sxs-lookup"><span data-stu-id="8bc87-105">[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) features create cacheable delegates that require fewer object allocations and reduced computational overhead than [logger extension methods](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions), such as `LogInformation`, `LogDebug`, and `LogError`.</span></span> <span data-ttu-id="8bc87-106">对于高性能日志记录方案，请使用 `LoggerMessage` 模式。</span><span class="sxs-lookup"><span data-stu-id="8bc87-106">For high-performance logging scenarios, use the `LoggerMessage` pattern.</span></span>

<span data-ttu-id="8bc87-107">与记录器扩展方法相比，`LoggerMessage` 具有以下性能优势：</span><span class="sxs-lookup"><span data-stu-id="8bc87-107">`LoggerMessage` provides the following performance advantages over Logger extension methods:</span></span>

* <span data-ttu-id="8bc87-108">记录器扩展方法需要将值类型（例如 `int`）“装箱”（转换）到 `object` 中。</span><span class="sxs-lookup"><span data-stu-id="8bc87-108">Logger extension methods require "boxing" (converting) value types, such as `int`, into `object`.</span></span> <span data-ttu-id="8bc87-109">`LoggerMessage` 模式使用带强类型参数的静态 `Action` 字段和扩展方法来避免装箱。</span><span class="sxs-lookup"><span data-stu-id="8bc87-109">The `LoggerMessage` pattern avoids boxing by using static `Action` fields and extension methods with strongly-typed parameters.</span></span>
* <span data-ttu-id="8bc87-110">记录器扩展方法每次写入日志消息时必须分析消息模板（命名的格式字符串）。</span><span class="sxs-lookup"><span data-stu-id="8bc87-110">Logger extension methods must parse the message template (named format string) every time a log message is written.</span></span> <span data-ttu-id="8bc87-111">如果已定义消息，那么 `LoggerMessage` 只需分析一次模板即可。</span><span class="sxs-lookup"><span data-stu-id="8bc87-111">`LoggerMessage` only requires parsing a template once when the message is defined.</span></span>

<span data-ttu-id="8bc87-112">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="8bc87-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="8bc87-113">此示例应用通过基本引号跟踪系统演示 `LoggerMessage` 功能。</span><span class="sxs-lookup"><span data-stu-id="8bc87-113">The sample app demonstrates `LoggerMessage` features with a basic quote tracking system.</span></span> <span data-ttu-id="8bc87-114">此应用使用内存中数据库添加和删除引号。</span><span class="sxs-lookup"><span data-stu-id="8bc87-114">The app adds and deletes quotes using an in-memory database.</span></span> <span data-ttu-id="8bc87-115">发生这些操作时，通过 `LoggerMessage` 模式生成日志消息。</span><span class="sxs-lookup"><span data-stu-id="8bc87-115">As these operations occur, log messages are generated using the `LoggerMessage` pattern.</span></span>

## <a name="loggermessagedefine"></a><span data-ttu-id="8bc87-116">LoggerMessage.Define</span><span class="sxs-lookup"><span data-stu-id="8bc87-116">LoggerMessage.Define</span></span>

<span data-ttu-id="8bc87-117">[Define（LogLevel、EventId、字符串）](/dotnet/api/microsoft.extensions.logging.loggermessage.define)创建用于记录消息的 `Action` 委托。</span><span class="sxs-lookup"><span data-stu-id="8bc87-117">[Define(LogLevel, EventId, String)](/dotnet/api/microsoft.extensions.logging.loggermessage.define) creates an `Action` delegate for logging a message.</span></span> <span data-ttu-id="8bc87-118">`Define` 重载允许向命名的格式字符串（模板）传递最多六个类型参数。</span><span class="sxs-lookup"><span data-stu-id="8bc87-118">`Define` overloads permit passing up to six type parameters to a named format string (template).</span></span>

## <a name="loggermessagedefinescope"></a><span data-ttu-id="8bc87-119">LoggerMessage.DefineScope</span><span class="sxs-lookup"><span data-stu-id="8bc87-119">LoggerMessage.DefineScope</span></span>

<span data-ttu-id="8bc87-120">[DefineScope（字符串）](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope)创建一个用于定义[日志作用域](xref:fundamentals/logging/index#log-scopes)的 `Func` 委托。</span><span class="sxs-lookup"><span data-stu-id="8bc87-120">[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) creates a `Func` delegate for defining a [log scope](xref:fundamentals/logging/index#log-scopes).</span></span> <span data-ttu-id="8bc87-121">`DefineScope` 重载允许向命名的格式字符串（模板）传递最多三个类型参数。</span><span class="sxs-lookup"><span data-stu-id="8bc87-121">`DefineScope` overloads permit passing up to three type parameters to a named format string (template).</span></span>

## <a name="message-template-named-format-string"></a><span data-ttu-id="8bc87-122">消息模板（命名的格式字符串）</span><span class="sxs-lookup"><span data-stu-id="8bc87-122">Message template (named format string)</span></span>

<span data-ttu-id="8bc87-123">提供给 `Define` 和 `DefineScope` 方法的字符串是一个模板，而不是内插字符串。</span><span class="sxs-lookup"><span data-stu-id="8bc87-123">The string provided to the `Define` and `DefineScope` methods is a template and not an interpolated string.</span></span> <span data-ttu-id="8bc87-124">占位符按照指定类型的顺序填充。</span><span class="sxs-lookup"><span data-stu-id="8bc87-124">Placeholders are filled in the order that the types are specified.</span></span> <span data-ttu-id="8bc87-125">模板中的占位符名称在各个模板中应当具备描述性和一致性。</span><span class="sxs-lookup"><span data-stu-id="8bc87-125">Placeholder names in the template should be descriptive and consistent across templates.</span></span> <span data-ttu-id="8bc87-126">它们在结构化的日志数据中充当属性名称。</span><span class="sxs-lookup"><span data-stu-id="8bc87-126">They serve as property names within structured log data.</span></span> <span data-ttu-id="8bc87-127">对于占位符名称，建议使用[帕斯卡拼写法](/dotnet/standard/design-guidelines/capitalization-conventions)。</span><span class="sxs-lookup"><span data-stu-id="8bc87-127">We recommend [Pascal casing](/dotnet/standard/design-guidelines/capitalization-conventions) for placeholder names.</span></span> <span data-ttu-id="8bc87-128">例如：`{Count}`、`{FirstName}`。</span><span class="sxs-lookup"><span data-stu-id="8bc87-128">For example, `{Count}`, `{FirstName}`.</span></span>

## <a name="implementing-loggermessagedefine"></a><span data-ttu-id="8bc87-129">实现 LoggerMessage.Define</span><span class="sxs-lookup"><span data-stu-id="8bc87-129">Implementing LoggerMessage.Define</span></span>

<span data-ttu-id="8bc87-130">每条日志消息都是一个 `Action`，保存在由 `LoggerMessage.Define` 创建的静态字段中。</span><span class="sxs-lookup"><span data-stu-id="8bc87-130">Each log message is an `Action` held in a static field created by `LoggerMessage.Define`.</span></span> <span data-ttu-id="8bc87-131">例如，示例应用创建一个字段来为索引页 (Internal/LoggerExtensions.cs) 描述 GET 请求的日志消息：</span><span class="sxs-lookup"><span data-stu-id="8bc87-131">For example, the sample app creates a field to describe a log message for a GET request for the Index page (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet1)]

<span data-ttu-id="8bc87-132">对于 `Action`，指定：</span><span class="sxs-lookup"><span data-stu-id="8bc87-132">For the `Action`, specify:</span></span>

* <span data-ttu-id="8bc87-133">日志级别。</span><span class="sxs-lookup"><span data-stu-id="8bc87-133">The log level.</span></span>
* <span data-ttu-id="8bc87-134">具有静态扩展方法名称的唯一事件标识符 ([EventId](/dotnet/api/microsoft.extensions.logging.eventid))。</span><span class="sxs-lookup"><span data-stu-id="8bc87-134">A unique event identifier ([EventId](/dotnet/api/microsoft.extensions.logging.eventid)) with the name of the static extension method.</span></span>
* <span data-ttu-id="8bc87-135">消息模板（命名的格式字符串）。</span><span class="sxs-lookup"><span data-stu-id="8bc87-135">The message template (named format string).</span></span> 

<span data-ttu-id="8bc87-136">对示例应用的索引页的请求设置：</span><span class="sxs-lookup"><span data-stu-id="8bc87-136">A request for the Index page of the sample app sets the:</span></span>

* <span data-ttu-id="8bc87-137">将日志级别设置为 `Information`。</span><span class="sxs-lookup"><span data-stu-id="8bc87-137">Log level to `Information`.</span></span>
* <span data-ttu-id="8bc87-138">将事件 ID 设置为具有 `IndexPageRequested` 方法名称的 `1`。</span><span class="sxs-lookup"><span data-stu-id="8bc87-138">Event id to `1` with the name of the `IndexPageRequested` method.</span></span>
* <span data-ttu-id="8bc87-139">将消息模板（命名的格式字符串）设置为字符串。</span><span class="sxs-lookup"><span data-stu-id="8bc87-139">Message template (named format string) to a string.</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet5)]

<span data-ttu-id="8bc87-140">结构化日志记录存储可以使用事件名称（当它获得事件 ID 时）来丰富日志记录。</span><span class="sxs-lookup"><span data-stu-id="8bc87-140">Structured logging stores may use the event name when it's supplied with the event id to enrich logging.</span></span> <span data-ttu-id="8bc87-141">例如，[Serilog](https://github.com/serilog/serilog-extensions-logging) 使用该事件名称。</span><span class="sxs-lookup"><span data-stu-id="8bc87-141">For example, [Serilog](https://github.com/serilog/serilog-extensions-logging) uses the event name.</span></span>

<span data-ttu-id="8bc87-142">通过强类型扩展方法调用 `Action`。</span><span class="sxs-lookup"><span data-stu-id="8bc87-142">The `Action` is invoked through a strongly-typed extension method.</span></span> <span data-ttu-id="8bc87-143">`IndexPageRequested` 方法在示例应用中记录索引页 GET 请求的消息：</span><span class="sxs-lookup"><span data-stu-id="8bc87-143">The `IndexPageRequested` method logs a message for an Index page GET request in the sample app:</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet9)]

<span data-ttu-id="8bc87-144">在 Pages/Index.cshtml.cs 的 `OnGetAsync` 方法中，在记录器上调用 `IndexPageRequested`：</span><span class="sxs-lookup"><span data-stu-id="8bc87-144">`IndexPageRequested` is called on the logger in the `OnGetAsync` method in *Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[Main](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3)]

<span data-ttu-id="8bc87-145">检查应用的控制台输出：</span><span class="sxs-lookup"><span data-stu-id="8bc87-145">Inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[1]
      => RequestId:0HL90M6E7PHK4:00000001 RequestPath:/ => /Index
      GET request for Index page
```

<span data-ttu-id="8bc87-146">要将参数传递给日志消息，创建静态字段时最多定义六种类型。</span><span class="sxs-lookup"><span data-stu-id="8bc87-146">To pass parameters to a log message, define up to six types when creating the static field.</span></span> <span data-ttu-id="8bc87-147">通过为 `Action` 字段定义 `string` 类型来添加引号时，示例应用会记录一个字符串：</span><span class="sxs-lookup"><span data-stu-id="8bc87-147">The sample app logs a string when adding a quote by defining a `string` type for the `Action` field:</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet2)]

<span data-ttu-id="8bc87-148">委托的日志消息模板从提供的类型接收其占位符值。</span><span class="sxs-lookup"><span data-stu-id="8bc87-148">The delegate's log message template receives its placeholder values from the types provided.</span></span> <span data-ttu-id="8bc87-149">示例应用定义一个委托，用于在 quote 参数是 `string` 的位置添加引号：</span><span class="sxs-lookup"><span data-stu-id="8bc87-149">The sample app defines a delegate for adding a quote where the quote parameter is a `string`:</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet6)]

<span data-ttu-id="8bc87-150">用于添加引号的静态扩展方法 `QuoteAdded` 接收 quote 参数值并将其传递给 `Action` 委托：</span><span class="sxs-lookup"><span data-stu-id="8bc87-150">The static extension method for adding a quote, `QuoteAdded`, receives the quote argument value and passes it to the `Action` delegate:</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet10)]

<span data-ttu-id="8bc87-151">在索引页的页面模型 (Pages/Index.cshtml.cs) 中，调用 `QuoteAdded` 来记录消息：</span><span class="sxs-lookup"><span data-stu-id="8bc87-151">In the Index page's page model (*Pages/Index.cshtml.cs*), `QuoteAdded` is called to log the message:</span></span>

[!code-csharp[Main](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet3&highlight=6)]

<span data-ttu-id="8bc87-152">检查应用的控制台输出：</span><span class="sxs-lookup"><span data-stu-id="8bc87-152">Inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[2]
      => RequestId:0HL90M6E7PHK5:0000000A RequestPath:/ => /Index
      Quote added (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand')
```

<span data-ttu-id="8bc87-153">本示例应用实现用于删除引号的 `try`&ndash;`catch` 模式。</span><span class="sxs-lookup"><span data-stu-id="8bc87-153">The sample app implements a `try`&ndash;`catch` pattern for quote deletion.</span></span> <span data-ttu-id="8bc87-154">为成功的删除操作记录提示性信息。</span><span class="sxs-lookup"><span data-stu-id="8bc87-154">An informational message is logged for a successful delete operation.</span></span> <span data-ttu-id="8bc87-155">引发异常时，为删除操作记录错误消息。</span><span class="sxs-lookup"><span data-stu-id="8bc87-155">An error message is logged for a delete operation when an exception is thrown.</span></span> <span data-ttu-id="8bc87-156">针对未成功的删除操作，日志消息包括异常堆栈跟踪 (Internal/LoggerExtensions.cs)：</span><span class="sxs-lookup"><span data-stu-id="8bc87-156">The log message for the unsuccessful delete operation includes the exception stack trace (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet3)]

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet7)]

<span data-ttu-id="8bc87-157">请注意异常如何传递到 `QuoteDeleteFailed` 中的委托：</span><span class="sxs-lookup"><span data-stu-id="8bc87-157">Note how the exception is passed to the delegate in `QuoteDeleteFailed`:</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet11)]

<span data-ttu-id="8bc87-158">在索引页的页面模型中，成功删除引号时会在记录器上调用 `QuoteDeleted` 方法。</span><span class="sxs-lookup"><span data-stu-id="8bc87-158">In the page model for the Index page, a successful quote deletion calls the `QuoteDeleted` method on the logger.</span></span> <span data-ttu-id="8bc87-159">如果找不到要删除的引号，则会引发 `ArgumentNullException`。</span><span class="sxs-lookup"><span data-stu-id="8bc87-159">When a quote isn't found for deletion, an `ArgumentNullException` is thrown.</span></span> <span data-ttu-id="8bc87-160">通过 `try`&ndash;`catch` 语句捕获异常，并在 `catch` 块 (Pages/Index.cshtml.cs) 中调用记录器上的 `QuoteDeleteFailed` 方法来记录异常：</span><span class="sxs-lookup"><span data-stu-id="8bc87-160">The exception is trapped by the `try`&ndash;`catch` statement and logged by calling the `QuoteDeleteFailed` method on the logger in the `catch` block (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[Main](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet5&highlight=14,18)]

<span data-ttu-id="8bc87-161">成功删除引号时，检查应用的控制台输出：</span><span class="sxs-lookup"><span data-stu-id="8bc87-161">When a quote is successfully deleted, inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:00000016 RequestPath:/ => /Index
      Quote deleted (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand' Id = 1)
```

<span data-ttu-id="8bc87-162">引号删除失败时，检查应用的控制台输出。</span><span class="sxs-lookup"><span data-stu-id="8bc87-162">When quote deletion fails, inspect the app's console output.</span></span> <span data-ttu-id="8bc87-163">请注意，异常包括在日志消息中：</span><span class="sxs-lookup"><span data-stu-id="8bc87-163">Note that the exception is included in the log message:</span></span>

```console
fail: LoggerMessageSample.Pages.IndexModel[5]
      => RequestId:0HL90M6E7PHK5:00000010 RequestPath:/ => /Index
      Quote delete failed (Id = 999)
System.ArgumentNullException: Value cannot be null.
Parameter name: entity
   at Microsoft.EntityFrameworkCore.Utilities.Check.NotNull[T](T value, String parameterName)
   at Microsoft.EntityFrameworkCore.DbContext.Remove[TEntity](TEntity entity)
   at Microsoft.EntityFrameworkCore.Internal.InternalDbSet`1.Remove(TEntity entity)
   at LoggerMessageSample.Pages.IndexModel.<OnPostDeleteQuoteAsync>d__14.MoveNext() in 
      <PATH>\sample\Pages\Index.cshtml.cs:line 87
```

## <a name="implementing-loggermessagedefinescope"></a><span data-ttu-id="8bc87-164">实现 LoggerMessage.DefineScope</span><span class="sxs-lookup"><span data-stu-id="8bc87-164">Implementing LoggerMessage.DefineScope</span></span>

<span data-ttu-id="8bc87-165">使用 [DefineScope（字符串）](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope)方法定义一个[日志作用域](xref:fundamentals/logging/index#log-scopes)，以应用到一系列日志消息中。</span><span class="sxs-lookup"><span data-stu-id="8bc87-165">Define a [log scope](xref:fundamentals/logging/index#log-scopes) to apply to a series of log messages using the [DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) method.</span></span>

<span data-ttu-id="8bc87-166">示例应用含有一个“全部清除”按钮，用于删除数据库中的所有引号。</span><span class="sxs-lookup"><span data-stu-id="8bc87-166">The sample app has a **Clear All** button for deleting all of the quotes in the database.</span></span> <span data-ttu-id="8bc87-167">通过一次删除一个引号来将其删除。</span><span class="sxs-lookup"><span data-stu-id="8bc87-167">The quotes are deleted by removing them one at a time.</span></span> <span data-ttu-id="8bc87-168">每当删除一个引号时，都会在记录器上调用 `QuoteDeleted` 方法。</span><span class="sxs-lookup"><span data-stu-id="8bc87-168">Each time a quote is deleted, the `QuoteDeleted` method is called on the logger.</span></span> <span data-ttu-id="8bc87-169">在这些日志消息中会添加一个日志作用域。</span><span class="sxs-lookup"><span data-stu-id="8bc87-169">A log scope is added to these log messages.</span></span>

<span data-ttu-id="8bc87-170">在控制台记录器选项中启用 `IncludeScopes`：</span><span class="sxs-lookup"><span data-stu-id="8bc87-170">Enable `IncludeScopes` in the console logger options:</span></span>

[!code-csharp[Main](loggermessage/sample/Program.cs?name=snippet1&highlight=22)]

<span data-ttu-id="8bc87-171">在 ASP.NET Core 2.0 应用中需要设置 `IncludeScopes` 来启用日志作用域。</span><span class="sxs-lookup"><span data-stu-id="8bc87-171">Setting `IncludeScopes` is required in ASP.NET Core 2.0 apps to enable log scopes.</span></span> <span data-ttu-id="8bc87-172">通过 appsettings 配置文件来设置 `IncludeScopes` 是针对 ASP.NET Core 2.1 版本计划的一项功能。</span><span class="sxs-lookup"><span data-stu-id="8bc87-172">Setting `IncludeScopes` via *appsettings* configuration files is a feature that's planned for the ASP.NET Core 2.1 release.</span></span>

<span data-ttu-id="8bc87-173">示例应用清除其他提供程序并添加筛选器来减少日志记录输出。</span><span class="sxs-lookup"><span data-stu-id="8bc87-173">The sample app clears other providers and adds filters to reduce the logging output.</span></span> <span data-ttu-id="8bc87-174">这样便可更加轻松地查看演示 `LoggerMessage` 功能的示例的日志消息。</span><span class="sxs-lookup"><span data-stu-id="8bc87-174">This makes it easier to see the sample's log messages that demonstrate `LoggerMessage` features.</span></span>

<span data-ttu-id="8bc87-175">要创建日志作用域，请添加一个字段来保存该作用域的 `Func` 委托。</span><span class="sxs-lookup"><span data-stu-id="8bc87-175">To create a log scope, add a field to hold a `Func` delegate for the scope.</span></span> <span data-ttu-id="8bc87-176">示例应用创建一个名为 `_allQuotesDeletedScope` (Internal/LoggerExtensions.cs) 的字段：</span><span class="sxs-lookup"><span data-stu-id="8bc87-176">The sample app creates a field called `_allQuotesDeletedScope` (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet4)]

<span data-ttu-id="8bc87-177">使用 `DefineScope` 来创建委托。</span><span class="sxs-lookup"><span data-stu-id="8bc87-177">Use `DefineScope` to create the delegate.</span></span> <span data-ttu-id="8bc87-178">调用委托时最多可以指定三种类型作为模板参数使用。</span><span class="sxs-lookup"><span data-stu-id="8bc87-178">Up to three types can be specified for use as template arguments when the delegate is invoked.</span></span> <span data-ttu-id="8bc87-179">示例应用使用包含删除的引号数量的消息模板（`int` 类型）：</span><span class="sxs-lookup"><span data-stu-id="8bc87-179">The sample app uses a message template that includes the number of deleted quotes (an `int` type):</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet8)]

<span data-ttu-id="8bc87-180">为日志消息提供一种静态扩展方法。</span><span class="sxs-lookup"><span data-stu-id="8bc87-180">Provide a static extension method for the log message.</span></span> <span data-ttu-id="8bc87-181">包含已命名属性的任何类型参数（这些参数出现在消息模板中）。</span><span class="sxs-lookup"><span data-stu-id="8bc87-181">Include any type parameters for named properties that appear in the message template.</span></span> <span data-ttu-id="8bc87-182">示例应用采用引号的 `count`，以删除并返回 `_allQuotesDeletedScope`：</span><span class="sxs-lookup"><span data-stu-id="8bc87-182">The sample app takes in a `count` of quotes to delete and returns `_allQuotesDeletedScope`:</span></span>

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet12)]

<span data-ttu-id="8bc87-183">该作用域将日志记录扩展调用包装在 `using` 块中：</span><span class="sxs-lookup"><span data-stu-id="8bc87-183">The scope wraps the logging extension calls in a `using` block:</span></span>

[!code-csharp[Main](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet4&highlight=5-6,14)]

<span data-ttu-id="8bc87-184">检查应用控制台输出中的日志消息。</span><span class="sxs-lookup"><span data-stu-id="8bc87-184">Inspect the log messages in the app's console output.</span></span> <span data-ttu-id="8bc87-185">以下结果显示删除的三个引号，以及包含的日志作用域消息：</span><span class="sxs-lookup"><span data-stu-id="8bc87-185">The following result shows three quotes deleted with the log scope message included:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 1' Id = 2)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 2' Id = 3)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 3' Id = 4)
```

## <a name="see-also"></a><span data-ttu-id="8bc87-186">请参阅</span><span class="sxs-lookup"><span data-stu-id="8bc87-186">See also</span></span>

* [<span data-ttu-id="8bc87-187">日志记录</span><span class="sxs-lookup"><span data-stu-id="8bc87-187">Logging</span></span>](xref:fundamentals/logging/index)
