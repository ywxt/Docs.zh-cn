---
title: "有关 ASP.NET 核心的 razor 语法参考"
author: rick-anderson
description: "了解如何将基于服务器的代码嵌入到网页的 Razor 标记语法。"
keywords: "ASP.NET 核心，Razor，Razor 指令"
ms.author: riande
manager: wpickett
ms.date: 10/18/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/razor
ms.openlocfilehash: 6df769069fce52755a57d8404f88203a652a1ab9
ms.sourcegitcommit: a3e88639a6bcf8fb4d634036dac93130c464a097
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="razor-syntax-for-aspnet-core"></a><span data-ttu-id="645d5-104">ASP.NET 核心的 razor 语法</span><span class="sxs-lookup"><span data-stu-id="645d5-104">Razor syntax for ASP.NET Core</span></span>

<span data-ttu-id="645d5-105">通过[Rick Anderson](https://twitter.com/RickAndMSFT)， [Luke Latham](https://github.com/guardrex)， [Taylor Mullen](https://twitter.com/ntaylormullen)，和[Dan Vicarel](https://github.com/Rabadash8820)</span><span class="sxs-lookup"><span data-stu-id="645d5-105">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Luke Latham](https://github.com/guardrex),  [Taylor Mullen](https://twitter.com/ntaylormullen), and [Dan Vicarel](https://github.com/Rabadash8820)</span></span>

<span data-ttu-id="645d5-106">Razor 是用于将基于服务器的代码嵌入到网页的标记的语法。</span><span class="sxs-lookup"><span data-stu-id="645d5-106">Razor is a markup syntax for embedding server-based code into webpages.</span></span> <span data-ttu-id="645d5-107">Razor 语法组成 Razor 标记、 C# 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="645d5-107">The Razor syntax consists of Razor markup, C#, and HTML.</span></span> <span data-ttu-id="645d5-108">通常包含 Razor 文件具有*.cshtml*文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="645d5-108">Files containing Razor generally have a *.cshtml* file extension.</span></span>

## <a name="rendering-html"></a><span data-ttu-id="645d5-109">呈现 HTML</span><span class="sxs-lookup"><span data-stu-id="645d5-109">Rendering HTML</span></span>

<span data-ttu-id="645d5-110">默认 Razor 语言为 HTML。</span><span class="sxs-lookup"><span data-stu-id="645d5-110">The default Razor language is HTML.</span></span> <span data-ttu-id="645d5-111">呈现 HTML Razor 标记是呈现 HTML 中，某一 HTML 文件没有什么不同。</span><span class="sxs-lookup"><span data-stu-id="645d5-111">Rendering HTML from Razor markup is no different than rendering HTML from an HTML file.</span></span>  <span data-ttu-id="645d5-112">HTML 标记中的*.cshtml* Razor 文件呈现服务器保持不变。</span><span class="sxs-lookup"><span data-stu-id="645d5-112">HTML markup in *.cshtml* Razor files is rendered by the server unchanged.</span></span>

## <a name="razor-syntax"></a><span data-ttu-id="645d5-113">Razor 语法</span><span class="sxs-lookup"><span data-stu-id="645d5-113">Razor syntax</span></span>

<span data-ttu-id="645d5-114">Razor 支持 C#，并使用`@`转换到 C# 的 HTML 中的符号。</span><span class="sxs-lookup"><span data-stu-id="645d5-114">Razor supports C# and uses the `@` symbol to transition from HTML to C#.</span></span> <span data-ttu-id="645d5-115">Razor C# 表达式的计算结果，并将它们呈现的 HTML 输出中。</span><span class="sxs-lookup"><span data-stu-id="645d5-115">Razor evaluates C# expressions and renders them in the HTML output.</span></span>

<span data-ttu-id="645d5-116">当`@`符号后跟[Razor 保留关键字](#razor-reserved-keywords)，它可以转换为 Razor 特定于标记。</span><span class="sxs-lookup"><span data-stu-id="645d5-116">When an `@` symbol is followed by a [Razor reserved keyword](#razor-reserved-keywords), it transitions into Razor-specific markup.</span></span> <span data-ttu-id="645d5-117">否则，它将转换为纯 C#。</span><span class="sxs-lookup"><span data-stu-id="645d5-117">Otherwise, it transitions into plain C#.</span></span>

<span data-ttu-id="645d5-118">要转义`@`符号在 Razor 标记中，请使用第二个`@`符号：</span><span class="sxs-lookup"><span data-stu-id="645d5-118">To escape an `@` symbol in Razor markup, use a second `@` symbol:</span></span>

```cshtml
<p>@@Username</p>
```

<span data-ttu-id="645d5-119">代码以 HTML 格式呈现与单个`@`符号：</span><span class="sxs-lookup"><span data-stu-id="645d5-119">The code is rendered in HTML with a single `@` symbol:</span></span>

```html
<p>@Username</p>
```

<span data-ttu-id="645d5-120">HTML 特性和内容包含电子邮件地址不处理`@`转换字符的形式的符号。</span><span class="sxs-lookup"><span data-stu-id="645d5-120">HTML attributes and content containing email addresses don't treat the `@` symbol as a transition character.</span></span> <span data-ttu-id="645d5-121">下面的示例中的电子邮件地址是不触及 Razor 分析：</span><span class="sxs-lookup"><span data-stu-id="645d5-121">The email addresses in the following example are untouched by Razor parsing:</span></span>

```cshtml
<a href="mailto:Support@contoso.com">Support@contoso.com</a>
```

## <a name="implicit-razor-expressions"></a><span data-ttu-id="645d5-122">隐式 Razor 表达式</span><span class="sxs-lookup"><span data-stu-id="645d5-122">Implicit Razor expressions</span></span>

<span data-ttu-id="645d5-123">隐式 Razor 表达式开头`@`跟 C# 代码：</span><span class="sxs-lookup"><span data-stu-id="645d5-123">Implicit Razor expressions start with `@` followed by C# code:</span></span>

```cshtml
<p>@DateTime.Now</p>
<p>@DateTime.IsLeapYear(2016)</p>
```

<span data-ttu-id="645d5-124">除了 C#`await`关键字，隐式表达式不能包含空格。</span><span class="sxs-lookup"><span data-stu-id="645d5-124">With the exception of the C# `await` keyword, implicit expressions must not contain spaces.</span></span> <span data-ttu-id="645d5-125">如果 C# 语句已清除结束，则可以混合空格：</span><span class="sxs-lookup"><span data-stu-id="645d5-125">If the C# statement has a clear ending, spaces can be intermingled:</span></span>

```cshtml
<p>@await DoSomething("hello", "world")</p>
```

<span data-ttu-id="645d5-126">隐式表达式**无法**包含 C# 泛型，括号内的字符作为 (`<>`) 都会被解释为 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="645d5-126">Implicit expressions **cannot** contain C# generics, as the characters inside the brackets (`<>`) are interpreted as an HTML tag.</span></span> <span data-ttu-id="645d5-127">下面的代码是**不**有效：</span><span class="sxs-lookup"><span data-stu-id="645d5-127">The following code is **not** valid:</span></span>

```cshtml
<p>@GenericMethod<int>()</p>
```

<span data-ttu-id="645d5-128">前面的代码生成编译器错误类似于以下项之一：</span><span class="sxs-lookup"><span data-stu-id="645d5-128">The preceding code generates a compiler error similar to one of the following:</span></span>

 * <span data-ttu-id="645d5-129">未关闭的"int"元素。</span><span class="sxs-lookup"><span data-stu-id="645d5-129">The "int" element was not closed.</span></span>  <span data-ttu-id="645d5-130">所有元素都必须为自结束或具有匹配的结束标记。</span><span class="sxs-lookup"><span data-stu-id="645d5-130">All elements must be either self-closing or have a matching end tag.</span></span>
 *  <span data-ttu-id="645d5-131">无法将方法组 GenericMethod 为非委托 object 类型的转换。</span><span class="sxs-lookup"><span data-stu-id="645d5-131">Cannot convert method group 'GenericMethod' to non-delegate type 'object'.</span></span> <span data-ttu-id="645d5-132">是否希望调用的方法？</span><span class="sxs-lookup"><span data-stu-id="645d5-132">Did you intend to invoke the method?\`</span></span> 
 
<span data-ttu-id="645d5-133">泛型方法调用必须包装在[显式 Razor 表达式](#explicit-razor-expressions)或[Razor 代码块](#razor-code-blocks)。</span><span class="sxs-lookup"><span data-stu-id="645d5-133">Generic method calls must be wrapped in an [explicit Razor expression](#explicit-razor-expressions) or a [Razor code block](#razor-code-blocks).</span></span>

## <a name="explicit-razor-expressions"></a><span data-ttu-id="645d5-134">显式 Razor 表达式</span><span class="sxs-lookup"><span data-stu-id="645d5-134">Explicit Razor expressions</span></span>

<span data-ttu-id="645d5-135">显式 Razor 表达式组成`@`与平衡括号的符号。</span><span class="sxs-lookup"><span data-stu-id="645d5-135">Explicit Razor expressions consist of an `@` symbol with balanced parenthesis.</span></span> <span data-ttu-id="645d5-136">若要呈现最后一周的时间，请使用以下 Razor 标记：</span><span class="sxs-lookup"><span data-stu-id="645d5-136">To render last week's time, the following Razor markup is used:</span></span>

```cshtml
<p>Last week this time: @(DateTime.Now - TimeSpan.FromDays(7))</p>
```

<span data-ttu-id="645d5-137">中的任何内容`@()`括号是计算并呈现到输出。</span><span class="sxs-lookup"><span data-stu-id="645d5-137">Any content within the `@()` parenthesis is evaluated and rendered to the output.</span></span>

<span data-ttu-id="645d5-138">在上一节中所述的隐式表达式通常不能包含空格。</span><span class="sxs-lookup"><span data-stu-id="645d5-138">Implicit expressions, described in the previous section, generally can't contain spaces.</span></span> <span data-ttu-id="645d5-139">在下面的代码中，从当前时间中减去不一周：</span><span class="sxs-lookup"><span data-stu-id="645d5-139">In the following code, one week isn't subtracted from the current time:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact.cshtml?range=17)]

<span data-ttu-id="645d5-140">代码将以下 HTML 呈现：</span><span class="sxs-lookup"><span data-stu-id="645d5-140">The code renders the following HTML:</span></span>

```html
<p>Last week: 7/7/2016 4:39:52 PM - TimeSpan.FromDays(7)</p>
```

<span data-ttu-id="645d5-141">显式表达式可以用于将文本与表达式结果串联起来：</span><span class="sxs-lookup"><span data-stu-id="645d5-141">Explicit expressions can be used to concatenate text with an expression result:</span></span>

```cshtml
@{
    var joe = new Person("Joe", 33);
}

<p>Age@(joe.Age)</p>
```

<span data-ttu-id="645d5-142">如果没有显式的表达式，`<p>Age@joe.Age</p>`视为电子邮件地址，和`<p>Age@joe.Age</p>`呈现。</span><span class="sxs-lookup"><span data-stu-id="645d5-142">Without the explicit expression, `<p>Age@joe.Age</p>` is treated as an email address, and `<p>Age@joe.Age</p>` is rendered.</span></span> <span data-ttu-id="645d5-143">在作为显式表达式，写入时`<p>Age33</p>`呈现。</span><span class="sxs-lookup"><span data-stu-id="645d5-143">When written as an explicit expression, `<p>Age33</p>` is rendered.</span></span>


<span data-ttu-id="645d5-144">显式表达式可以用于呈现输出中的泛型方法*.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="645d5-144">Explicit expressions can be used to render output from generic methods in *.cshtml* files.</span></span> <span data-ttu-id="645d5-145">在隐式表达式中，括号内的字符 (`<>`) 都会被解释为 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="645d5-145">In an implicit expression, the characters inside the brackets (`<>`) are interpreted as an HTML tag.</span></span> <span data-ttu-id="645d5-146">以下标记是**不**有效 Razor:</span><span class="sxs-lookup"><span data-stu-id="645d5-146">The following markup is **not** valid Razor:</span></span>

```cshtml
<p>@GenericMethod<int>()</p>
```

<span data-ttu-id="645d5-147">前面的代码生成编译器错误类似于以下项之一：</span><span class="sxs-lookup"><span data-stu-id="645d5-147">The preceding code generates a compiler error similar to one of the following:</span></span>

 * <span data-ttu-id="645d5-148">未关闭的"int"元素。</span><span class="sxs-lookup"><span data-stu-id="645d5-148">The "int" element was not closed.</span></span>  <span data-ttu-id="645d5-149">所有元素都必须为自结束或具有匹配的结束标记。</span><span class="sxs-lookup"><span data-stu-id="645d5-149">All elements must be either self-closing or have a matching end tag.</span></span>
 *  <span data-ttu-id="645d5-150">无法将方法组 GenericMethod 为非委托 object 类型的转换。</span><span class="sxs-lookup"><span data-stu-id="645d5-150">Cannot convert method group 'GenericMethod' to non-delegate type 'object'.</span></span> <span data-ttu-id="645d5-151">是否希望调用的方法？</span><span class="sxs-lookup"><span data-stu-id="645d5-151">Did you intend to invoke the method?\`</span></span> 
 
 <span data-ttu-id="645d5-152">以下标记显示正确的方式写入此代码。</span><span class="sxs-lookup"><span data-stu-id="645d5-152">The following markup shows the correct way write this code.</span></span>  <span data-ttu-id="645d5-153">作为显式表达式编写的代码：</span><span class="sxs-lookup"><span data-stu-id="645d5-153">The code is written as an explicit expression:</span></span>

```cshtml
<p>@(GenericMethod<int>())</p>
```

## <a name="expression-encoding"></a><span data-ttu-id="645d5-154">表达式编码</span><span class="sxs-lookup"><span data-stu-id="645d5-154">Expression encoding</span></span>

<span data-ttu-id="645d5-155">C# 表达式，其计算结果为字符串是 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="645d5-155">C# expressions that evaluate to a string are HTML encoded.</span></span> <span data-ttu-id="645d5-156">C# 表达式的计算结果为`IHtmlContent`呈现直接通过`IHtmlContent.WriteTo`。</span><span class="sxs-lookup"><span data-stu-id="645d5-156">C# expressions that evaluate to `IHtmlContent` are rendered directly through `IHtmlContent.WriteTo`.</span></span> <span data-ttu-id="645d5-157">C# 表达式不计算结果为`IHtmlContent`转换为字符串`ToString`它们在呈现之前进行编码。</span><span class="sxs-lookup"><span data-stu-id="645d5-157">C# expressions that don't evaluate to `IHtmlContent` are converted to a string by `ToString` and encoded before they're rendered.</span></span>

```cshtml
@("<span>Hello World</span>")
```

<span data-ttu-id="645d5-158">代码将以下 HTML 呈现：</span><span class="sxs-lookup"><span data-stu-id="645d5-158">The code renders the following HTML:</span></span>

```html
&lt;span&gt;Hello World&lt;/span&gt;
```

<span data-ttu-id="645d5-159">HTML 的浏览器所示：</span><span class="sxs-lookup"><span data-stu-id="645d5-159">The HTML is shown in the browser as:</span></span>

```
<span>Hello World</span>
```

<span data-ttu-id="645d5-160">`HtmlHelper.Raw`输出没有编码，但呈现为 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="645d5-160">`HtmlHelper.Raw` output isn't encoded but rendered as HTML markup.</span></span>

> [!WARNING]
> <span data-ttu-id="645d5-161">使用`HtmlHelper.Raw`未净化的用户输入会带来安全风险。</span><span class="sxs-lookup"><span data-stu-id="645d5-161">Using `HtmlHelper.Raw` on unsanitized user input is a security risk.</span></span> <span data-ttu-id="645d5-162">用户输入可能包含恶意 JavaScript 或其他攻击。</span><span class="sxs-lookup"><span data-stu-id="645d5-162">User input might contain malicious JavaScript or other exploits.</span></span> <span data-ttu-id="645d5-163">对用户输入会很困难。</span><span class="sxs-lookup"><span data-stu-id="645d5-163">Sanitizing user input is difficult.</span></span> <span data-ttu-id="645d5-164">避免使用`HtmlHelper.Raw`需要用户输入。</span><span class="sxs-lookup"><span data-stu-id="645d5-164">Avoid using `HtmlHelper.Raw` with user input.</span></span>

```cshtml
@Html.Raw("<span>Hello World</span>")
```

<span data-ttu-id="645d5-165">代码将以下 HTML 呈现：</span><span class="sxs-lookup"><span data-stu-id="645d5-165">The code renders the following HTML:</span></span>

```html
<span>Hello World</span>
```

## <a name="razor-code-blocks"></a><span data-ttu-id="645d5-166">Razor 代码块</span><span class="sxs-lookup"><span data-stu-id="645d5-166">Razor code blocks</span></span>

<span data-ttu-id="645d5-167">Razor 代码块开头`@`，并且通过包括`{}`。</span><span class="sxs-lookup"><span data-stu-id="645d5-167">Razor code blocks start with `@` and are enclosed by `{}`.</span></span> <span data-ttu-id="645d5-168">与不同的是表达式，C# 代码块内的代码不呈现。</span><span class="sxs-lookup"><span data-stu-id="645d5-168">Unlike expressions, C# code inside code blocks isn't rendered.</span></span> <span data-ttu-id="645d5-169">代码块和在视图中的表达式共享相同的作用域和按顺序定义：</span><span class="sxs-lookup"><span data-stu-id="645d5-169">Code blocks and expressions in a view share the same scope and are defined in order:</span></span>

```cshtml
@{
    var quote = "The future depends on what you do today. - Mahatma Gandhi";
}

<p>@quote</p>

@{
    quote = "Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.";
}

<p>@quote</p>
```

<span data-ttu-id="645d5-170">代码将以下 HTML 呈现：</span><span class="sxs-lookup"><span data-stu-id="645d5-170">The code renders the following HTML:</span></span>

```html
<p>The future depends on what you do today. - Mahatma Gandhi</p>
<p>Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.</p>
```

### <a name="implicit-transitions"></a><span data-ttu-id="645d5-171">隐式转换</span><span class="sxs-lookup"><span data-stu-id="645d5-171">Implicit transitions</span></span>

<span data-ttu-id="645d5-172">代码块中的默认语言为 C# 中，而是 Razor 页可以转换回 HTML:</span><span class="sxs-lookup"><span data-stu-id="645d5-172">The default language in a code block is C#, but the Razor Page can transition back to HTML:</span></span>

```cshtml
@{
    var inCSharp = true;
    <p>Now in HTML, was in C# @inCSharp</p>
}
```

### <a name="explicit-delimited-transition"></a><span data-ttu-id="645d5-173">带分隔符的显式转换</span><span class="sxs-lookup"><span data-stu-id="645d5-173">Explicit delimited transition</span></span>

<span data-ttu-id="645d5-174">若要定义的子部分的应呈现的 HTML 代码块，周围呈现的字符与 Razor **\<文本 >**标记：</span><span class="sxs-lookup"><span data-stu-id="645d5-174">To define a subsection of a code block that should render HTML, surround the characters for rendering with the Razor **\<text>** tag:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <text>Name: @person.Name</text>
}
```

<span data-ttu-id="645d5-175">使用此方法来呈现不包围的 HTML 标记的 HTML。</span><span class="sxs-lookup"><span data-stu-id="645d5-175">Use this approach to render HTML that isn't surrounded by an HTML tag.</span></span> <span data-ttu-id="645d5-176">没有 HTML 或 Razor 标记，Razor 运行时错误时发生。</span><span class="sxs-lookup"><span data-stu-id="645d5-176">Without an HTML or Razor tag, a Razor runtime error occurs.</span></span>

<span data-ttu-id="645d5-177">**\<文本 >**标记可用于在呈现内容时控制空白：</span><span class="sxs-lookup"><span data-stu-id="645d5-177">The **\<text>** tag is useful to control whitespace when rendering content:</span></span>

* <span data-ttu-id="645d5-178">仅之间的内容**\<文本 >**标记的呈现。</span><span class="sxs-lookup"><span data-stu-id="645d5-178">Only the content between the **\<text>** tag is rendered.</span></span> 
* <span data-ttu-id="645d5-179">之前或之后有空格**\<文本 >**的 HTML 输出中将显示标记。</span><span class="sxs-lookup"><span data-stu-id="645d5-179">No whitespace before or after the **\<text>** tag appears in the HTML output.</span></span>

### <a name="explicit-line-transition-with-"></a><span data-ttu-id="645d5-180">显式行转换与 @:</span><span class="sxs-lookup"><span data-stu-id="645d5-180">Explicit Line Transition with @:</span></span>

<span data-ttu-id="645d5-181">若要在代码块内以 html 格式呈现整个行的其余内容，使用`@:`语法：</span><span class="sxs-lookup"><span data-stu-id="645d5-181">To render the rest of an entire line as HTML inside a code block, use the `@:` syntax:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    @:Name: @person.Name
}
```

<span data-ttu-id="645d5-182">而无需`@:`在代码中，生成 Razor 运行时错误。</span><span class="sxs-lookup"><span data-stu-id="645d5-182">Without the `@:` in the code,  a Razor runtime error is generated.</span></span>

<span data-ttu-id="645d5-183">警告： 额外`@`Razor 文件中的字符会导致编译器错误语句在块中更高版本。</span><span class="sxs-lookup"><span data-stu-id="645d5-183">Warning: Extra `@` characters in a Razor file can cause  cause compiler errors at statements later in the block.</span></span> <span data-ttu-id="645d5-184">这些编译器错误可能很难了解因为实际错误发生之前所报告的错误。</span><span class="sxs-lookup"><span data-stu-id="645d5-184">These compiler errors can be difficult to understand because the actual error occurs before the reported error.</span></span>  <span data-ttu-id="645d5-185">组合到单个代码块的多个隐式/显式表达式后，此错误很常见。</span><span class="sxs-lookup"><span data-stu-id="645d5-185">This error is common after combining multiple implicit/explicit expressions into a single code block.</span></span>

## <a name="control-structures"></a><span data-ttu-id="645d5-186">控件结构</span><span class="sxs-lookup"><span data-stu-id="645d5-186">Control Structures</span></span>

<span data-ttu-id="645d5-187">控制结构是一种扩展的代码块。</span><span class="sxs-lookup"><span data-stu-id="645d5-187">Control structures are an extension of code blocks.</span></span> <span data-ttu-id="645d5-188">所有方面的代码块 （过渡到标记中，内联 C#） 也都适用于以下结构：</span><span class="sxs-lookup"><span data-stu-id="645d5-188">All aspects of code blocks (transitioning to markup, inline C#) also apply to the following structures:</span></span>

### <a name="conditionals-if-else-if-else-and-switch"></a><span data-ttu-id="645d5-189">条件语句@if，否则; 否则，和@switch</span><span class="sxs-lookup"><span data-stu-id="645d5-189">Conditionals @if, else if, else, and @switch</span></span>

<span data-ttu-id="645d5-190">`@if`当代码运行时的控件：</span><span class="sxs-lookup"><span data-stu-id="645d5-190">`@if` controls when code runs:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
```

<span data-ttu-id="645d5-191">`else`和`else if`不需要`@`符号：</span><span class="sxs-lookup"><span data-stu-id="645d5-191">`else` and `else if` don't require the `@` symbol:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
else if (value >= 1337)
{
    <p>The value is large.</p>
}
else
{
    <p>The value is odd and small.</p>
}
```

<span data-ttu-id="645d5-192">以下标记显示如何使用交换语句：</span><span class="sxs-lookup"><span data-stu-id="645d5-192">The following markup shows how to use a switch statement:</span></span>

```cshtml
@switch (value)
{
    case 1:
        <p>The value is 1!</p>
        break;
    case 1337:
        <p>Your number is 1337!</p>
        break;
    default:
        <p>Your number wasn't 1 or 1337.</p>
        break;
}
```

### <a name="looping-for-foreach-while-and-do-while"></a><span data-ttu-id="645d5-193">循环@for， @foreach， @while，和@do时</span><span class="sxs-lookup"><span data-stu-id="645d5-193">Looping @for, @foreach, @while, and @do while</span></span>

<span data-ttu-id="645d5-194">模板化 HTML 可以呈现包含循环的控制语句。</span><span class="sxs-lookup"><span data-stu-id="645d5-194">Templated HTML can be rendered with looping control statements.</span></span>  <span data-ttu-id="645d5-195">若要呈现的人员列表：</span><span class="sxs-lookup"><span data-stu-id="645d5-195">To render a list of people:</span></span>

```cshtml
@{
    var people = new Person[]
    {
          new Person("Weston", 33),
          new Person("Johnathon", 41),
          ...
    };
}
```

<span data-ttu-id="645d5-196">支持以下循环语句：</span><span class="sxs-lookup"><span data-stu-id="645d5-196">The following looping statements are supported:</span></span>

`@for`

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@foreach`

```cshtml
@foreach (var person in people)
{
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@while`

```cshtml
@{ var i = 0; }
@while (i < people.Length)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
}
```

`@do while`

```cshtml
@{ var i = 0; }
@do
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
} while (i < people.Length);
```

### <a name="compound-using"></a><span data-ttu-id="645d5-197">复合@using</span><span class="sxs-lookup"><span data-stu-id="645d5-197">Compound @using</span></span>

<span data-ttu-id="645d5-198">在 C# 中，`using`语句用于确保释放对象。</span><span class="sxs-lookup"><span data-stu-id="645d5-198">In C#, a `using` statement is used to ensure an object is disposed.</span></span> <span data-ttu-id="645d5-199">在 Razor，相同的机制用于创建包含其他内容的 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="645d5-199">In Razor, the same mechanism is used to create HTML Helpers that contain additional content.</span></span> <span data-ttu-id="645d5-200">在下面的代码中，HTML 帮助器呈现窗体标记与`@using`语句：</span><span class="sxs-lookup"><span data-stu-id="645d5-200">In the following code, HTML Helpers render a form tag with the `@using` statement:</span></span>


```cshtml
@using (Html.BeginForm())
{
    <div>
        email:
        <input type="email" id="Email" value="">
        <button>Register</button>
    </div>
}
```

<span data-ttu-id="645d5-201">可以使用执行作用域级操作[标记帮助程序](xref:mvc/views/tag-helpers/intro)。</span><span class="sxs-lookup"><span data-stu-id="645d5-201">Scope-level actions can be performed with [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

### <a name="try-catch-finally"></a><span data-ttu-id="645d5-202">@trycatch，finally</span><span class="sxs-lookup"><span data-stu-id="645d5-202">@try, catch, finally</span></span>

<span data-ttu-id="645d5-203">异常处理是类似于 C#:</span><span class="sxs-lookup"><span data-stu-id="645d5-203">Exception handling is similar to C#:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact7.cshtml)]

### <a name="lock"></a>@lock

<span data-ttu-id="645d5-204">Razor 具有的功能来保护与 lock 语句的关键部分：</span><span class="sxs-lookup"><span data-stu-id="645d5-204">Razor has the capability to protect critical sections with lock statements:</span></span>

```cshtml
@lock (SomeLock)
{
    // Do critical section work
}
```

### <a name="comments"></a><span data-ttu-id="645d5-205">注释</span><span class="sxs-lookup"><span data-stu-id="645d5-205">Comments</span></span>

<span data-ttu-id="645d5-206">Razor 支持 C# 和 HTML 注释：</span><span class="sxs-lookup"><span data-stu-id="645d5-206">Razor supports C# and HTML comments:</span></span>

```cshtml
@{
    /* C# comment */
    // Another C# comment
}
<!-- HTML comment -->
```

<span data-ttu-id="645d5-207">代码将以下 HTML 呈现：</span><span class="sxs-lookup"><span data-stu-id="645d5-207">The code renders the following HTML:</span></span>

```html
<!-- HTML comment -->
```

<span data-ttu-id="645d5-208">在呈现网页之前，将服务器中删除 razor 注释。</span><span class="sxs-lookup"><span data-stu-id="645d5-208">Razor comments are removed by the server before the webpage is rendered.</span></span> <span data-ttu-id="645d5-209">使用 razor`@*  *@`来分隔注释。</span><span class="sxs-lookup"><span data-stu-id="645d5-209">Razor uses `@*  *@` to delimit comments.</span></span> <span data-ttu-id="645d5-210">下面的代码是加上注释，因此服务器不呈现任何标记：</span><span class="sxs-lookup"><span data-stu-id="645d5-210">The following code is commented out, so the server doesn't render any markup:</span></span>

```cshtml
@*
    @{
        /* C# comment */
        // Another C# comment
    }
    <!-- HTML comment -->
*@
```

## <a name="directives"></a><span data-ttu-id="645d5-211">指令</span><span class="sxs-lookup"><span data-stu-id="645d5-211">Directives</span></span>

<span data-ttu-id="645d5-212">保留的关键字以下的隐式表达式由表示 razor 指令`@`符号。</span><span class="sxs-lookup"><span data-stu-id="645d5-212">Razor directives are represented by implicit expressions with reserved keywords following the `@` symbol.</span></span> <span data-ttu-id="645d5-213">指令通常会更改的方式视图分析或启用不同的功能。</span><span class="sxs-lookup"><span data-stu-id="645d5-213">A directive typically changes the way a view is parsed or enables different functionality.</span></span>

<span data-ttu-id="645d5-214">了解如何 Razor 生成视图的代码，使更易于理解指令的工作方式。</span><span class="sxs-lookup"><span data-stu-id="645d5-214">Understanding how Razor generates code for a view makes it easier to understand how directives work.</span></span>

[!code-html[Main](razor/sample/Views/Home/Contact8.cshtml)]

<span data-ttu-id="645d5-215">在代码中生成类似于下面的类：</span><span class="sxs-lookup"><span data-stu-id="645d5-215">The code generates a class similar to the following:</span></span>

```csharp
public class _Views_Something_cshtml : RazorPage<dynamic>
{
    public override async Task ExecuteAsync()
    {
        var output = "Getting old ain't for wimps! - Anonymous";

        WriteLiteral("/r/n<div>Quote of the Day: ");
        Write(output);
        WriteLiteral("</div>");
    }
}
```

<span data-ttu-id="645d5-216">在本文中，部分中更高版本[查看生成的视图的 Razor C# 类](#viewing-the-razor-c-class-generated-for-a-view)说明如何查看此生成的类。</span><span class="sxs-lookup"><span data-stu-id="645d5-216">Later in this article, the section [Viewing the Razor C# class generated for a view](#viewing-the-razor-c-class-generated-for-a-view) explains how to view this generated class.</span></span>

### <a name="using"></a>@using

<span data-ttu-id="645d5-217">`@using`指令添加 C#`using`指令到生成的视图：</span><span class="sxs-lookup"><span data-stu-id="645d5-217">The `@using` directive adds the C# `using` directive to the generated view:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact9.cshtml)]

### <a name="model"></a>@model

<span data-ttu-id="645d5-218">`@model`指令指定的模型传递到视图类型：</span><span class="sxs-lookup"><span data-stu-id="645d5-218">The `@model` directive specifies the type of the model passed to a view:</span></span>

```cshtml
@model TypeNameOfModel
```

<span data-ttu-id="645d5-219">在 ASP.NET 核心 MVC 应用程序使用单个用户帐户创建*Views/Account/Login.cshtml*视图包含以下模型声明：</span><span class="sxs-lookup"><span data-stu-id="645d5-219">In an ASP.NET Core MVC app created with individual user accounts, the *Views/Account/Login.cshtml* view contains the following model declaration:</span></span>

```cshtml
@model LoginViewModel
```

<span data-ttu-id="645d5-220">生成的类继承自`RazorPage<dynamic>`:</span><span class="sxs-lookup"><span data-stu-id="645d5-220">The class generated inherits from `RazorPage<dynamic>`:</span></span>

```csharp
public class _Views_Account_Login_cshtml : RazorPage<LoginViewModel>
```

<span data-ttu-id="645d5-221">Razor 公开`Model`属性访问的模型传递给视图：</span><span class="sxs-lookup"><span data-stu-id="645d5-221">Razor exposes a `Model` property for accessing the model passed to the view:</span></span>

```cshtml
<div>The Login Email: @Model.Email</div>
```

<span data-ttu-id="645d5-222">`@model`指令指定此属性的类型。</span><span class="sxs-lookup"><span data-stu-id="645d5-222">The `@model` directive specifies the type of this property.</span></span> <span data-ttu-id="645d5-223">指令指定`T`中`RazorPage<T>`，生成类，派生自的视图。</span><span class="sxs-lookup"><span data-stu-id="645d5-223">The directive specifies the `T` in `RazorPage<T>` that the generated class that the view derives from.</span></span> <span data-ttu-id="645d5-224">如果`@model`指令不会指定，`Model`属性属于类型`dynamic`。</span><span class="sxs-lookup"><span data-stu-id="645d5-224">If  the `@model` directive iisn't specified, the `Model` property is of type `dynamic`.</span></span> <span data-ttu-id="645d5-225">模型的值从控制器传递到该视图。</span><span class="sxs-lookup"><span data-stu-id="645d5-225">The value of the model is passed from the controller to the view.</span></span> <span data-ttu-id="645d5-226">有关详细信息，请参阅 [强类型模型和@model关键字。</span><span class="sxs-lookup"><span data-stu-id="645d5-226">For more information, see [Strongly typed models and the @model keyword.</span></span>

### <a name="inherits"></a>@inherits

<span data-ttu-id="645d5-227">`@inherits`指令提供的视图继承的类的完全控制：</span><span class="sxs-lookup"><span data-stu-id="645d5-227">The `@inherits` directive provides  full control of the class the view inherits:</span></span>

```cshtml
@inherits TypeNameOfClassToInheritFrom
```

<span data-ttu-id="645d5-228">下面的代码是自定义的 Razor 页类型：</span><span class="sxs-lookup"><span data-stu-id="645d5-228">The following code is a custom Razor page type:</span></span>

[!code-csharp[Main](razor/sample/Classes/CustomRazorPage.cs)]

<span data-ttu-id="645d5-229">`CustomText`视图中显示：</span><span class="sxs-lookup"><span data-stu-id="645d5-229">The `CustomText` is displayed in a view:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact10.cshtml)]

<span data-ttu-id="645d5-230">代码将以下 HTML 呈现：</span><span class="sxs-lookup"><span data-stu-id="645d5-230">The code renders the following HTML:</span></span>

```html
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

 <span data-ttu-id="645d5-231">`@model`和`@inherits`可以在同一个视图中使用。</span><span class="sxs-lookup"><span data-stu-id="645d5-231">`@model` and `@inherits` can be used in the same view.</span></span>  <span data-ttu-id="645d5-232">`@inherits`可以采用*_ViewImports.cshtml*视图导入的文件：</span><span class="sxs-lookup"><span data-stu-id="645d5-232">`@inherits` can be in a *_ViewImports.cshtml* file that the view imports:</span></span>

[!code-cshtml[Main](razor/sample/Views/_ViewImportsModel.cshtml)]

<span data-ttu-id="645d5-233">下面的代码是强类型化视图的一个示例：</span><span class="sxs-lookup"><span data-stu-id="645d5-233">The following code is an example of a strongly-typed view:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Login1.cshtml)]

<span data-ttu-id="645d5-234">如果"rick@contoso.com"传递在模型中，视图将生成以下的 HTML 标记：</span><span class="sxs-lookup"><span data-stu-id="645d5-234">If "rick@contoso.com" is passed in the model, the view generates the following HTML markup:</span></span>

```html
<div>The Login Email: rick@contoso.com</div>
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

### <a name="inject"></a>@inject


<span data-ttu-id="645d5-235">`@inject`指令，Razor 页后，可以将从服务注入[服务容器](xref:fundamentals/dependency-injection)到视图。</span><span class="sxs-lookup"><span data-stu-id="645d5-235">The `@inject` directive enables the Razor Page to inject a service from the [service container](xref:fundamentals/dependency-injection) into a view.</span></span> <span data-ttu-id="645d5-236">有关详细信息，请参阅[到视图的依赖关系注入](xref:mvc/views/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="645d5-236">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span>

### <a name="functions"></a>@functions

<span data-ttu-id="645d5-237">`@functions`指令，Razor 页后，可以将函数级内容添加到视图：</span><span class="sxs-lookup"><span data-stu-id="645d5-237">The `@functions` directive enables a Razor Page to add function-level content to a view:</span></span>

```cshtml
@functions { // C# Code }
```

<span data-ttu-id="645d5-238">例如:</span><span class="sxs-lookup"><span data-stu-id="645d5-238">For example:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact6.cshtml)]

<span data-ttu-id="645d5-239">代码生成以下的 HTML 标记：</span><span class="sxs-lookup"><span data-stu-id="645d5-239">The code generates the following HTML markup:</span></span>

```html
<div>From method: Hello</div>
```

<span data-ttu-id="645d5-240">下面的代码是生成的 Razor C# 类：</span><span class="sxs-lookup"><span data-stu-id="645d5-240">The following code is the generated Razor C# class:</span></span>

[!code-csharp[Main](razor/sample/Classes/Views_Home_Test_cshtml.cs?range=1-19)]

### <a name="section"></a>@section

<span data-ttu-id="645d5-241">`@section`结合使用指令[布局](xref:mvc/views/layout)以启用要呈现的 HTML 页面的不同部分中的内容视图。</span><span class="sxs-lookup"><span data-stu-id="645d5-241">The `@section` directive is used in conjunction with the [layout](xref:mvc/views/layout) to enable views to render content in different parts of the HTML page.</span></span> <span data-ttu-id="645d5-242">有关详细信息，请参阅[部分](xref:mvc/views/layout#layout-sections-label)。</span><span class="sxs-lookup"><span data-stu-id="645d5-242">For more information, see [Sections](xref:mvc/views/layout#layout-sections-label).</span></span>

## <a name="tag-helpers"></a><span data-ttu-id="645d5-243">标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="645d5-243">Tag Helpers</span></span>

<span data-ttu-id="645d5-244">有三个指令属于[标记帮助程序](xref:mvc/views/tag-helpers/intro)。</span><span class="sxs-lookup"><span data-stu-id="645d5-244">There are three directives that pertain to [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

| <span data-ttu-id="645d5-245">指令</span><span class="sxs-lookup"><span data-stu-id="645d5-245">Directive</span></span> | <span data-ttu-id="645d5-246">函数</span><span class="sxs-lookup"><span data-stu-id="645d5-246">Function</span></span> |
| --------- | -------- |
| [@addTagHelper](xref:mvc/views/tag-helpers/intro#add-helper-label) | <span data-ttu-id="645d5-247">使得标记帮助程序适用于一个视图。</span><span class="sxs-lookup"><span data-stu-id="645d5-247">Makes Tag Helpers available to a view.</span></span> |
| [@removeTagHelper](xref:mvc/views/tag-helpers/intro#remove-razor-directives-label) | <span data-ttu-id="645d5-248">删除之前从视图添加标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="645d5-248">Removes Tag Helpers previously added from a view.</span></span> |
| [@tagHelperPrefix](xref:mvc/views/tag-helpers/intro#prefix-razor-directives-label) | <span data-ttu-id="645d5-249">指定要启用标记帮助器支持，并若要使标记帮助器使用显式标记前缀。</span><span class="sxs-lookup"><span data-stu-id="645d5-249">Specifies a tag prefix to enable Tag Helper support and to make Tag Helper usage explicit.</span></span> |

## <a name="razor-reserved-keywords"></a><span data-ttu-id="645d5-250">Razor 保留关键字</span><span class="sxs-lookup"><span data-stu-id="645d5-250">Razor reserved keywords</span></span>

### <a name="razor-keywords"></a><span data-ttu-id="645d5-251">Razor 关键字</span><span class="sxs-lookup"><span data-stu-id="645d5-251">Razor keywords</span></span>

* <span data-ttu-id="645d5-252">页 （需要 ASP.NET Core 2.0 及更高版本）</span><span class="sxs-lookup"><span data-stu-id="645d5-252">page (Requires ASP.NET Core 2.0 and later)</span></span>
* <span data-ttu-id="645d5-253">函数</span><span class="sxs-lookup"><span data-stu-id="645d5-253">functions</span></span>
* <span data-ttu-id="645d5-254">继承</span><span class="sxs-lookup"><span data-stu-id="645d5-254">inherits</span></span>
* <span data-ttu-id="645d5-255">模型</span><span class="sxs-lookup"><span data-stu-id="645d5-255">model</span></span>
* <span data-ttu-id="645d5-256">section</span><span class="sxs-lookup"><span data-stu-id="645d5-256">section</span></span>
* <span data-ttu-id="645d5-257">（当前不支持 ASP.NET Core） 的帮助器</span><span class="sxs-lookup"><span data-stu-id="645d5-257">helper (Not currently supported by ASP.NET Core)</span></span>

<span data-ttu-id="645d5-258">与转义 razor 关键字`@(Razor Keyword)`(例如， `@(functions)`)。</span><span class="sxs-lookup"><span data-stu-id="645d5-258">Razor keywords are escaped with `@(Razor Keyword)` (for example, `@(functions)`).</span></span>

### <a name="c-razor-keywords"></a><span data-ttu-id="645d5-259">C# Razor 关键字</span><span class="sxs-lookup"><span data-stu-id="645d5-259">C# Razor keywords</span></span>

* <span data-ttu-id="645d5-260">大小写</span><span class="sxs-lookup"><span data-stu-id="645d5-260">case</span></span>
* <span data-ttu-id="645d5-261">do</span><span class="sxs-lookup"><span data-stu-id="645d5-261">do</span></span>
* <span data-ttu-id="645d5-262">default</span><span class="sxs-lookup"><span data-stu-id="645d5-262">default</span></span>
* <span data-ttu-id="645d5-263">for</span><span class="sxs-lookup"><span data-stu-id="645d5-263">for</span></span>
* <span data-ttu-id="645d5-264">foreach</span><span class="sxs-lookup"><span data-stu-id="645d5-264">foreach</span></span>
* <span data-ttu-id="645d5-265">if</span><span class="sxs-lookup"><span data-stu-id="645d5-265">if</span></span>
* <span data-ttu-id="645d5-266">else</span><span class="sxs-lookup"><span data-stu-id="645d5-266">else</span></span>
* <span data-ttu-id="645d5-267">锁定</span><span class="sxs-lookup"><span data-stu-id="645d5-267">lock</span></span>
* <span data-ttu-id="645d5-268">switch</span><span class="sxs-lookup"><span data-stu-id="645d5-268">switch</span></span>
* <span data-ttu-id="645d5-269">try</span><span class="sxs-lookup"><span data-stu-id="645d5-269">try</span></span>
* <span data-ttu-id="645d5-270">catch</span><span class="sxs-lookup"><span data-stu-id="645d5-270">catch</span></span>
* <span data-ttu-id="645d5-271">finally</span><span class="sxs-lookup"><span data-stu-id="645d5-271">finally</span></span>
* <span data-ttu-id="645d5-272">using</span><span class="sxs-lookup"><span data-stu-id="645d5-272">using</span></span>
* <span data-ttu-id="645d5-273">while</span><span class="sxs-lookup"><span data-stu-id="645d5-273">while</span></span>

<span data-ttu-id="645d5-274">C# Razor 关键字必须使用双转义`@(@C# Razor Keyword)`(例如， `@(@case)`)。</span><span class="sxs-lookup"><span data-stu-id="645d5-274">C# Razor keywords must be double-escaped with `@(@C# Razor Keyword)` (for example, `@(@case)`).</span></span> <span data-ttu-id="645d5-275">第一个`@`转义 Razor 分析器。</span><span class="sxs-lookup"><span data-stu-id="645d5-275">The first `@` escapes the Razor parser.</span></span> <span data-ttu-id="645d5-276">第二个`@`转义 C# 分析器。</span><span class="sxs-lookup"><span data-stu-id="645d5-276">The second `@` escapes the C# parser.</span></span>

### <a name="reserved-keywords-not-used-by-razor"></a><span data-ttu-id="645d5-277">不使用 Razor 的保留的关键字</span><span class="sxs-lookup"><span data-stu-id="645d5-277">Reserved keywords not used by Razor</span></span>

* <span data-ttu-id="645d5-278">namespace</span><span class="sxs-lookup"><span data-stu-id="645d5-278">namespace</span></span>
* <span data-ttu-id="645d5-279">类</span><span class="sxs-lookup"><span data-stu-id="645d5-279">class</span></span>

## <a name="viewing-the-razor-c-class-generated-for-a-view"></a><span data-ttu-id="645d5-280">查看生成的视图的 Razor C# 类</span><span class="sxs-lookup"><span data-stu-id="645d5-280">Viewing the Razor C# class generated for a view</span></span>

<span data-ttu-id="645d5-281">将下面的类添加到 ASP.NET 核心 MVC 项目：</span><span class="sxs-lookup"><span data-stu-id="645d5-281">Add the following class to the ASP.NET Core MVC project:</span></span>

[!code-csharp[Main](razor/sample/Utilities/CustomTemplateEngine.cs)]

<span data-ttu-id="645d5-282">重写`RazorTemplateEngine`添加通过与 MVC`CustomTemplateEngine`类：</span><span class="sxs-lookup"><span data-stu-id="645d5-282">Override the `RazorTemplateEngine` added by MVC with the `CustomTemplateEngine` class:</span></span>

[!code-csharp[Main](razor/sample/Startup.cs?highlight=4&range=10-14)]

<span data-ttu-id="645d5-283">在上设置断点`return csharpDocument`的语句`CustomTemplateEngine`。</span><span class="sxs-lookup"><span data-stu-id="645d5-283">Set a break point on the `return csharpDocument` statement of `CustomTemplateEngine`.</span></span> <span data-ttu-id="645d5-284">当在断点处停止程序执行时，查看值`generatedCode`。</span><span class="sxs-lookup"><span data-stu-id="645d5-284">When program execution stops at the break point, view the value of `generatedCode`.</span></span>

![GeneratedCode 文本可视化工具视图](razor/_static/tvr.png)

## <a name="view-lookups-and-case-sensitivity"></a><span data-ttu-id="645d5-286">视图的查找，并区分大小写</span><span class="sxs-lookup"><span data-stu-id="645d5-286">View lookups and case sensitivity</span></span>

<span data-ttu-id="645d5-287">Razor 视图引擎视图执行区分大小写的查找。</span><span class="sxs-lookup"><span data-stu-id="645d5-287">The Razor view engine performs case-sensitive lookups for views.</span></span> <span data-ttu-id="645d5-288">但是，由基础文件系统确定实际查找：</span><span class="sxs-lookup"><span data-stu-id="645d5-288">However, the actual lookup is determined by the underlying file system:</span></span>

* <span data-ttu-id="645d5-289">文件基于的源：</span><span class="sxs-lookup"><span data-stu-id="645d5-289">File based source:</span></span> 
  * <span data-ttu-id="645d5-290">在操作系统上使用区分大小写的文件系统 (例如，Windows)，物理文件提供程序查找是区分大小写的。</span><span class="sxs-lookup"><span data-stu-id="645d5-290">On operating systems with case insensitive file systems (for example, Windows), physical file provider lookups are case insensitive.</span></span> <span data-ttu-id="645d5-291">例如，`return View("Test")`与匹配的结果将导致*/Views/Home/Test.cshtml*， */Views/home/test.cshtml*，和任何其他大小写变体。</span><span class="sxs-lookup"><span data-stu-id="645d5-291">For example, `return View("Test")` results in matches for */Views/Home/Test.cshtml*, */Views/home/test.cshtml*, and any other casing variant.</span></span>
  * <span data-ttu-id="645d5-292">在区分大小写的文件系统 (例如，Linux，OSX，且`EmbeddedFileProvider`)，查找是区分大小写。</span><span class="sxs-lookup"><span data-stu-id="645d5-292">On case-sensitive file systems (for example, Linux, OSX, and with `EmbeddedFileProvider`), lookups are case-sensitive.</span></span> <span data-ttu-id="645d5-293">例如，`return View("Test")`专门匹配*/Views/Home/Test.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="645d5-293">For example, `return View("Test")` specifically matches */Views/Home/Test.cshtml*.</span></span>
* <span data-ttu-id="645d5-294">预编译视图： 使用 ASP.NET Core 2.0 及更高版本，查找预编译视图是在所有操作系统上不区分。</span><span class="sxs-lookup"><span data-stu-id="645d5-294">Precompiled views: With ASP.NET Core 2.0 and later, looking up precompiled views is case insensitive on all operating systems.</span></span> <span data-ttu-id="645d5-295">行为是在 Windows 上的物理文件提供程序的行为相同。</span><span class="sxs-lookup"><span data-stu-id="645d5-295">The behavior is identical to physical file provider's behavior on Windows.</span></span> <span data-ttu-id="645d5-296">如果两个预编译的视图仅大小写不同，查找的结果是不确定的。</span><span class="sxs-lookup"><span data-stu-id="645d5-296">If two precompiled views differ only in case, the result of lookup is non-deterministic.</span></span>

<span data-ttu-id="645d5-297">开发人员建议以匹配的文件和目录名称的大小写的大小写：</span><span class="sxs-lookup"><span data-stu-id="645d5-297">Developers are encouraged to match the casing of file and directory names to the casing of:</span></span>

    * <span data-ttu-id="645d5-298">区域、 控制器和操作名称。</span><span class="sxs-lookup"><span data-stu-id="645d5-298">Area, controller, and action names.</span></span> 
    * <span data-ttu-id="645d5-299">Razor 的页数。</span><span class="sxs-lookup"><span data-stu-id="645d5-299">Razor Pages.</span></span>
    
<span data-ttu-id="645d5-300">匹配用例以确保部署找到其视图而不考虑基础文件系统。</span><span class="sxs-lookup"><span data-stu-id="645d5-300">Matching case ensures the deployments find their views regardless of the underlying file system.</span></span>
