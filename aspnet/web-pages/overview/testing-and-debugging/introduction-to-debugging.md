---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: 调试 ASP.NET Web 简介页 (Razor) 站点 |Microsoft 文档
author: tfitzmac
description: 调试是查找和修复错误，在你的代码页中的过程。 本章展示的一些工具和技术可用于调试和 analyz...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: c28d63acda6e585f4aa64f294049c1790faac850
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a><span data-ttu-id="8e82b-104">调试 ASP.NET Web 简介页 (Razor) 站点</span><span class="sxs-lookup"><span data-stu-id="8e82b-104">Introduction to Debugging ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="8e82b-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8e82b-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8e82b-106">此文章介绍了调试在 ASP.NET Web 页 (Razor) 网站中的页的各种方法。</span><span class="sxs-lookup"><span data-stu-id="8e82b-106">This article explains various ways to debug pages in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="8e82b-107">调试是查找和修复错误，在你的代码页中的过程。</span><span class="sxs-lookup"><span data-stu-id="8e82b-107">Debugging is the process of finding and fixing errors in your code pages.</span></span>
> 
> <span data-ttu-id="8e82b-108">**你将学习：**</span><span class="sxs-lookup"><span data-stu-id="8e82b-108">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="8e82b-109">如何显示信息，可帮助分析和调试页。</span><span class="sxs-lookup"><span data-stu-id="8e82b-109">How to display information that helps analyze and debug pages.</span></span>
> - <span data-ttu-id="8e82b-110">如何使用调试工具在 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="8e82b-110">How to use debugging tools in Visual Studio.</span></span>
>   
> 
> <span data-ttu-id="8e82b-111">这些是文章中引入的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="8e82b-111">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="8e82b-112">`ServerInfo`帮助器。</span><span class="sxs-lookup"><span data-stu-id="8e82b-112">The `ServerInfo` helper.</span></span>
> - <span data-ttu-id="8e82b-113">`ObjectInfo` 帮助器。</span><span class="sxs-lookup"><span data-stu-id="8e82b-113">`ObjectInfo` helper.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="8e82b-114">软件版本</span><span class="sxs-lookup"><span data-stu-id="8e82b-114">Software versions</span></span>
> 
> 
> - <span data-ttu-id="8e82b-115">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="8e82b-115">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="8e82b-116">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="8e82b-116">Visual Studio 2013</span></span>
>   
> 
> <span data-ttu-id="8e82b-117">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="8e82b-117">This tutorial also works with ASP.NET Web Pages 2.</span></span> <span data-ttu-id="8e82b-118">你可以使用 WebMatrix 3，但不是支持集成的调试器。</span><span class="sxs-lookup"><span data-stu-id="8e82b-118">You can use WebMatrix 3 but the integrated debugger is not supported.</span></span>


<span data-ttu-id="8e82b-119">排除的错误和问题在代码中的一个重要方面是在第一个位置中避免它们。</span><span class="sxs-lookup"><span data-stu-id="8e82b-119">An important aspect of troubleshooting errors and problems in your code is to avoid them in the first place.</span></span> <span data-ttu-id="8e82b-120">你可以执行该操作通过将放在有可能导致到的错误代码部分`try/catch`块。</span><span class="sxs-lookup"><span data-stu-id="8e82b-120">You can do that by putting sections of your code that are likely to cause errors into `try/catch` blocks.</span></span> <span data-ttu-id="8e82b-121">有关详细信息，请参阅部分处理中的错误[ASP.NET Web 编程使用 Razor 语法的简介](https://go.microsoft.com/fwlink/?LinkId=202890)。</span><span class="sxs-lookup"><span data-stu-id="8e82b-121">For more information, see the section on handling errors in [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890).</span></span>

<span data-ttu-id="8e82b-122">`ServerInfo`帮助程序是一个诊断工具，将概述有关承载你的页面的 web 服务器环境的信息。</span><span class="sxs-lookup"><span data-stu-id="8e82b-122">The `ServerInfo` helper is a diagnostic tool that gives you an overview of information about the web server environment that hosts your page.</span></span> <span data-ttu-id="8e82b-123">它还显示当浏览器请求页时发送的 HTTP 请求信息。</span><span class="sxs-lookup"><span data-stu-id="8e82b-123">It also shows you HTTP request information that's sent when a browser requests the page.</span></span> <span data-ttu-id="8e82b-124">`ServerInfo`帮助器将显示当前的用户标识，发出了请求、 的浏览器的类型，依此类推。</span><span class="sxs-lookup"><span data-stu-id="8e82b-124">The `ServerInfo` helper displays the current user identity, the type of browser that made the request, and so on.</span></span> <span data-ttu-id="8e82b-125">这种信息可以帮助你解决常见的问题。</span><span class="sxs-lookup"><span data-stu-id="8e82b-125">This kind of information can help you troubleshoot common issues.</span></span>

1. <span data-ttu-id="8e82b-126">创建一个名为的新 web 页*ServerInfo.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="8e82b-126">Create a new web page named *ServerInfo.cshtml*.</span></span>
2. <span data-ttu-id="8e82b-127">在页结束时，只在关闭前`</body>`标记中，添加`@ServerInfo.GetHtml()`:</span><span class="sxs-lookup"><span data-stu-id="8e82b-127">At the end of the page, just before the closing `</body>` tag, add `@ServerInfo.GetHtml()`:</span></span>

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    <span data-ttu-id="8e82b-128">你可以添加`ServerInfo`页中的任意位置的代码。</span><span class="sxs-lookup"><span data-stu-id="8e82b-128">You can add the `ServerInfo` code anywhere in the page.</span></span> <span data-ttu-id="8e82b-129">但将其添加在结束会保留其输出独立于其他页面内容，这样，就更易读。</span><span class="sxs-lookup"><span data-stu-id="8e82b-129">But adding it at the end will keep its output separate from your other page content, which makes it easier to read.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="8e82b-130">**重要**网页移到生产服务器之前，应从你的 web 页面删除诊断的任何代码。</span><span class="sxs-lookup"><span data-stu-id="8e82b-130">**Important** You should remove any diagnostic code from your web pages before you move web pages to a production server.</span></span> <span data-ttu-id="8e82b-131">这适用于`ServerInfo`帮助程序，以及这篇文章涉及将代码添加到页上的其他诊断技术。</span><span class="sxs-lookup"><span data-stu-id="8e82b-131">This applies to the `ServerInfo` helper as well as the other diagnostic techniques in this article that involve adding code to a page.</span></span> <span data-ttu-id="8e82b-132">因为这种类型的信息可能会给了恶意企图的人员有用，你不希望您的网站访问者，以在服务器和类似详细信息，查看有关你的服务器名称、 用户名称、 路径信息。</span><span class="sxs-lookup"><span data-stu-id="8e82b-132">You don't want your website visitors to see information about your server name, user names, paths on your server, and similar details, because this type of information might be useful to people with malicious intent.</span></span>
3. <span data-ttu-id="8e82b-133">保存页并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="8e82b-133">Save the page and run it in a browser.</span></span>

    ![调试 1](introduction-to-debugging/_static/image1.jpg)

    <span data-ttu-id="8e82b-135">`ServerInfo`帮助器页中显示的信息的四个表：</span><span class="sxs-lookup"><span data-stu-id="8e82b-135">The `ServerInfo` helper displays four tables of information in the page:</span></span>

   - <span data-ttu-id="8e82b-136">服务器配置。</span><span class="sxs-lookup"><span data-stu-id="8e82b-136">Server Configuration.</span></span> <span data-ttu-id="8e82b-137">本部分提供有关托管的 web 服务器，包括计算机名称、 你正在运行的 ASP.NET、 域名和服务器时间的版本信息。</span><span class="sxs-lookup"><span data-stu-id="8e82b-137">This section provides information about the hosting web server, including computer name, the version of ASP.NET you're running, the domain name, and server time.</span></span>
   - <span data-ttu-id="8e82b-138">ASP.NET 服务器变量。</span><span class="sxs-lookup"><span data-stu-id="8e82b-138">ASP.NET Server Variables.</span></span> <span data-ttu-id="8e82b-139">本部分提供有关的许多的 HTTP 协议详细信息 （调用 HTTP 变量） 的详细信息并值是每个网页请求的一部分。</span><span class="sxs-lookup"><span data-stu-id="8e82b-139">This section provides details about the many HTTP protocol details (called HTTP variables) and values that are part of each web page request.</span></span>
   - <span data-ttu-id="8e82b-140">HTTP 运行时信息。</span><span class="sxs-lookup"><span data-stu-id="8e82b-140">HTTP Runtime Information.</span></span> <span data-ttu-id="8e82b-141">本部分提供有关的详细信息的 Microsoft.NET Framework 下运行的 web 页、 路径、 有关缓存中，依次类推的详细信息的版本。</span><span class="sxs-lookup"><span data-stu-id="8e82b-141">This section provides details about that the version of the Microsoft .NET Framework that your web page is running under, the path, details about the cache, and so on.</span></span> <span data-ttu-id="8e82b-142">(正如你在中学到[ASP.NET Web 编程使用 Razor 语法的简介](https://go.microsoft.com/fwlink/?LinkId=202890)、 使用 Razor 语法基于 Microsoft 的 ASP.NET web 服务器技术，它本身基于广泛的软件的 ASP.NET Web Pages开发库中调用.NET Framework。）</span><span class="sxs-lookup"><span data-stu-id="8e82b-142">(As you learned in [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890), ASP.NET Web Pages using the Razor syntax are built on Microsoft's ASP.NET web server technology, which is itself built on an extensive software development library called the .NET Framework.)</span></span>
   - <span data-ttu-id="8e82b-143">环境变量。</span><span class="sxs-lookup"><span data-stu-id="8e82b-143">Environment Variables.</span></span> <span data-ttu-id="8e82b-144">本部分提供的 web 服务器上的所有本地环境变量及其值的列表。</span><span class="sxs-lookup"><span data-stu-id="8e82b-144">This section provides a list of all the local environment variables and their values on the web server.</span></span>

     <span data-ttu-id="8e82b-145">所有服务器和请求信息的完整说明不在本文的范围，但你可以看到，`ServerInfo`帮助程序返回了大量的诊断信息。</span><span class="sxs-lookup"><span data-stu-id="8e82b-145">A full description of all the server and request information is beyond the scope of this article, but you can see that the `ServerInfo` helper returns a lot of diagnostic information.</span></span> <span data-ttu-id="8e82b-146">有关值的详细信息，`ServerInfo`返回时，请参阅[识别环境变量](https://technet.microsoft.com/library/dd560744(WS.10).aspx)Microsoft TechNet 网站上和[IIS 服务器变量](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)MSDN 网站上。</span><span class="sxs-lookup"><span data-stu-id="8e82b-146">For more information about the values that `ServerInfo` returns, see [Recognized Environment Variables](https://technet.microsoft.com/library/dd560744(WS.10).aspx) on the Microsoft TechNet website and [IIS Server Variables](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) on the MSDN website.</span></span>

## <a name="embedding-output-expressions-to-display-page-values"></a><span data-ttu-id="8e82b-147">嵌入输出表达式，以显示页值</span><span class="sxs-lookup"><span data-stu-id="8e82b-147">Embedding Output Expressions to Display Page Values</span></span>

<span data-ttu-id="8e82b-148">若要查看你的代码中发生的情况的另一种方法是将输出表达式嵌入在页中。</span><span class="sxs-lookup"><span data-stu-id="8e82b-148">Another way to see what's happening in your code is to embed output expressions in the page.</span></span> <span data-ttu-id="8e82b-149">如您所知，可以通过添加类似于直接输出变量的值`@myVariable`或`@(subTotal * 12)`到页。</span><span class="sxs-lookup"><span data-stu-id="8e82b-149">As you know, you can directly output the value of a variable by adding something like `@myVariable` or `@(subTotal * 12)` to the page.</span></span> <span data-ttu-id="8e82b-150">以进行调试，你可以在代码中，在关键点将这些输出表达式。</span><span class="sxs-lookup"><span data-stu-id="8e82b-150">For debugging, you can place these output expressions at strategic points in your code.</span></span> <span data-ttu-id="8e82b-151">这可以运行你的页面时，请参阅关键变量或计算的结果的值。</span><span class="sxs-lookup"><span data-stu-id="8e82b-151">This enables you to see the value of key variables or the result of calculations when your page runs.</span></span> <span data-ttu-id="8e82b-152">当你已完成调试，可以删除表达式或注释掉这些。此过程说明了使用嵌入式的表达式来帮助调试页面的典型方式。</span><span class="sxs-lookup"><span data-stu-id="8e82b-152">When you're done debugging, you can remove the expressions or comment them out. This procedure illustrates a typical way to use embedded expressions to help debug a page.</span></span>

1. <span data-ttu-id="8e82b-153">创建名为的新 WebMatrix 页*OutputExpression.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="8e82b-153">Create a new WebMatrix page that's named *OutputExpression.cshtml*.</span></span>
2. <span data-ttu-id="8e82b-154">将页面内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="8e82b-154">Replace the page content with the following:</span></span>

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    <span data-ttu-id="8e82b-155">该示例使用`switch`用于检查的值的语句`weekday`变量，然后显示它是不同的输出消息，具体取决于一周中的哪一天。</span><span class="sxs-lookup"><span data-stu-id="8e82b-155">The example uses a `switch` statement to check the value of the `weekday` variable and then display a different output message depending on which day of the week it is.</span></span> <span data-ttu-id="8e82b-156">在示例中，`if`中第一个代码块的块任意更改通过将一天添加到当前周日期值的日期是星期几。</span><span class="sxs-lookup"><span data-stu-id="8e82b-156">In the example, the `if` block within the first code block arbitrarily changes the day of the week by adding one day to the current weekday value.</span></span> <span data-ttu-id="8e82b-157">这是用于说明目的引入错误。</span><span class="sxs-lookup"><span data-stu-id="8e82b-157">This is an error introduced for illustration purposes.</span></span>
3. <span data-ttu-id="8e82b-158">保存页并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="8e82b-158">Save the page and run it in a browser.</span></span>

    <span data-ttu-id="8e82b-159">为错误的日期是星期几，该页显示消息。</span><span class="sxs-lookup"><span data-stu-id="8e82b-159">The page displays the message for the wrong day of the week.</span></span> <span data-ttu-id="8e82b-160">任何日期是星期几它实际上是，将看到更高版本的一天的消息。</span><span class="sxs-lookup"><span data-stu-id="8e82b-160">Whatever day of the week it actually is, you'll see the message for one day later.</span></span> <span data-ttu-id="8e82b-161">尽管在这种情况下你知道为什么消息处于关闭状态 （因为代码有意设置不正确的日期值），实际上通常很难知道其中事情的进展状况错误代码中。</span><span class="sxs-lookup"><span data-stu-id="8e82b-161">Although in this case you know why the message is off (because the code deliberately sets the incorrect day value), in reality it's often hard to know where things are going wrong in the code.</span></span> <span data-ttu-id="8e82b-162">若要调试，你需要了解所发生的情况的键的对象和变量的值如`weekday`。</span><span class="sxs-lookup"><span data-stu-id="8e82b-162">To debug, you need to find out what's happening to the value of key objects and variables such as `weekday`.</span></span>
4. <span data-ttu-id="8e82b-163">将输出表达式添加的方法是插入`@weekday`在代码中的注释指示的两个位置所示。</span><span class="sxs-lookup"><span data-stu-id="8e82b-163">Add output expressions by inserting `@weekday` as shown in the two places indicated by comments in the code.</span></span> <span data-ttu-id="8e82b-164">这些输出表达式将显示变量的值在该点在代码执行。</span><span class="sxs-lookup"><span data-stu-id="8e82b-164">These output expressions will display the values of the variable at that point in the code execution.</span></span>

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. <span data-ttu-id="8e82b-165">保存并在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="8e82b-165">Save and run the page in a browser.</span></span>

    <span data-ttu-id="8e82b-166">页面显示实际日期是星期几首先，然后将结果添加一天，然后从生成的消息的更新日期是星期几`switch`语句。</span><span class="sxs-lookup"><span data-stu-id="8e82b-166">The page displays the real day of the week first, then the updated day of the week that results from adding one day, and then the resulting message from the `switch` statement.</span></span> <span data-ttu-id="8e82b-167">从两个变量的表达式输出 (`@weekday`) 具有天之间没有空格，因为您没有添加任何 HTML`<p>`输出; 标记表达式可以只供测试。</span><span class="sxs-lookup"><span data-stu-id="8e82b-167">The output from the two variable expressions (`@weekday`) has no spaces between the days because you didn't add any HTML `<p>` tags to the output; the expressions are just for testing.</span></span>

    ![调试 2](introduction-to-debugging/_static/image2.jpg)

    <span data-ttu-id="8e82b-169">现在，你可以查看错误所在。</span><span class="sxs-lookup"><span data-stu-id="8e82b-169">Now you can see where the error is.</span></span> <span data-ttu-id="8e82b-170">当你第一次显示`weekday`变量中的代码，它显示正确的日期。</span><span class="sxs-lookup"><span data-stu-id="8e82b-170">When you first display the `weekday` variable in the code, it shows the correct day.</span></span> <span data-ttu-id="8e82b-171">当你显示它的第二个时间之后,`if`在代码块中，在一天处于关闭状态的一个。</span><span class="sxs-lookup"><span data-stu-id="8e82b-171">When you display it the second time, after the `if` block in the code, the day is off by one.</span></span> <span data-ttu-id="8e82b-172">因此，您知道工作日变量的第一个和第二个外观之间发生了内容。</span><span class="sxs-lookup"><span data-stu-id="8e82b-172">So you know that something has happened between the first and second appearance of the weekday variable.</span></span> <span data-ttu-id="8e82b-173">如果这是一个真正的 bug，这种方法可帮助你缩小问题的原因的代码的位置。</span><span class="sxs-lookup"><span data-stu-id="8e82b-173">If this were a real bug, this kind of approach would help you narrow down the location of the code that's causing the problem.</span></span>
6. <span data-ttu-id="8e82b-174">修复在页中的代码，删除你添加的两个输出表达式，并删除更改日期是星期几的代码。</span><span class="sxs-lookup"><span data-stu-id="8e82b-174">Fix the code in the page by removing the two output expressions you added, and removing the code that changes the day of the week.</span></span> <span data-ttu-id="8e82b-175">完成剩余块的代码类似于下面的示例：</span><span class="sxs-lookup"><span data-stu-id="8e82b-175">The remaining, complete block of code looks like the following example:</span></span>

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. <span data-ttu-id="8e82b-176">在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="8e82b-176">Run the page in a browser.</span></span> <span data-ttu-id="8e82b-177">此时会显示正确的消息显示为实际日期是星期几。</span><span class="sxs-lookup"><span data-stu-id="8e82b-177">This time you see the correct message displayed for the actual day of the week.</span></span>

## <a name="using-the-objectinfo-helper-to-display-object-values"></a><span data-ttu-id="8e82b-178">使用 ObjectInfo 帮助器来显示对象值</span><span class="sxs-lookup"><span data-stu-id="8e82b-178">Using the ObjectInfo Helper to Display Object Values</span></span>

<span data-ttu-id="8e82b-179">`ObjectInfo`帮助器显示类型和每个对象传递给它的值。</span><span class="sxs-lookup"><span data-stu-id="8e82b-179">The `ObjectInfo` helper displays the type and the value of each object you pass to it.</span></span> <span data-ttu-id="8e82b-180">可用来在代码中 （如你在前面的示例的输出表达式），查看变量和对象的值加上你可以看到的数据类型有关对象的信息。</span><span class="sxs-lookup"><span data-stu-id="8e82b-180">You can use it to view the value of variables and objects in your code (like you did with output expressions in the previous example), plus you can see data type information about the object.</span></span>

1. <span data-ttu-id="8e82b-181">打开名为的文件*OutputExpression.cshtml*之前创建。</span><span class="sxs-lookup"><span data-stu-id="8e82b-181">Open the file named *OutputExpression.cshtml* that you created earlier.</span></span>
2. <span data-ttu-id="8e82b-182">将替换为以下代码块中页的所有代码：</span><span class="sxs-lookup"><span data-stu-id="8e82b-182">Replace all code in the page with the following block of code:</span></span>

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. <span data-ttu-id="8e82b-183">保存并在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="8e82b-183">Save and run the page in a browser.</span></span>

    ![调试-4](introduction-to-debugging/_static/image3.jpg)

    <span data-ttu-id="8e82b-185">在此示例中，`ObjectInfo`帮助器将显示两个项：</span><span class="sxs-lookup"><span data-stu-id="8e82b-185">In this example, the `ObjectInfo` helper displays two items:</span></span>

   - <span data-ttu-id="8e82b-186">类型。</span><span class="sxs-lookup"><span data-stu-id="8e82b-186">The type.</span></span> <span data-ttu-id="8e82b-187">对于第一个变量，该类型是`DayOfWeek`。</span><span class="sxs-lookup"><span data-stu-id="8e82b-187">For the first variable, the type is `DayOfWeek`.</span></span> <span data-ttu-id="8e82b-188">对于第二个变量，该类型是`String`。</span><span class="sxs-lookup"><span data-stu-id="8e82b-188">For the second variable, the type is `String`.</span></span>
   - <span data-ttu-id="8e82b-189">值。</span><span class="sxs-lookup"><span data-stu-id="8e82b-189">The value.</span></span> <span data-ttu-id="8e82b-190">在这种情况下，因为你已在页中显示的问候语变量的值，值再次显示当你将变量传递到`ObjectInfo`。</span><span class="sxs-lookup"><span data-stu-id="8e82b-190">In this case, because you already display the value of the greeting variable in the page, the value is displayed again when you pass the variable to `ObjectInfo`.</span></span>

     <span data-ttu-id="8e82b-191">对于更复杂的对象，`ObjectInfo`帮助器可以显示详细信息&#8212;基本上，它可以在其中显示的类型和的所有对象的属性的值。</span><span class="sxs-lookup"><span data-stu-id="8e82b-191">For more complex objects, the `ObjectInfo` helper can display more information &#8212; basically, it can display the types and values of all of an object's properties.</span></span>

## <a name="using-debugging-tools-in-visual-studio"></a><span data-ttu-id="8e82b-192">使用 Visual Studio 中的调试工具</span><span class="sxs-lookup"><span data-stu-id="8e82b-192">Using Debugging Tools in Visual Studio</span></span>

<span data-ttu-id="8e82b-193">对于更全面的调试体验，使用 Visual Studio 2013 或免费[Visual Studio Express 2013 for Web](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-2013-express)。</span><span class="sxs-lookup"><span data-stu-id="8e82b-193">For a more comprehensive debugging experience, use Visual Studio 2013 or the free [Visual Studio Express 2013 for Web](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-2013-express).</span></span> <span data-ttu-id="8e82b-194">使用 Visual Studio，可以在你想要检查的行在代码中设置断点。</span><span class="sxs-lookup"><span data-stu-id="8e82b-194">With Visual Studio, you can set a breakpoint in your code at the line that you want to inspect.</span></span>

![设置断点](introduction-to-debugging/_static/image1.png)

<span data-ttu-id="8e82b-196">当你测试 web 站点时，正在执行的代码都将在断点处暂停。</span><span class="sxs-lookup"><span data-stu-id="8e82b-196">When you test the web site, the executing code halts at the breakpoint.</span></span>

![到达断点](introduction-to-debugging/_static/image2.png)

<span data-ttu-id="8e82b-198">你可以检查变量和单步执行代码--逐行的当前值。</span><span class="sxs-lookup"><span data-stu-id="8e82b-198">You can examine the current values of the variables, and step through the code line-by-line.</span></span>

![请参阅值](introduction-to-debugging/_static/image3.png)

<span data-ttu-id="8e82b-200">有关使用 Visual Studio 中集成的调试器来调试 ASP.NET Razor 页的信息，请参阅[编程 ASP.NET Web 页 (Razor) 使用 Visual Studio](https://go.microsoft.com/fwlink/?LinkId=205854)。</span><span class="sxs-lookup"><span data-stu-id="8e82b-200">For information about using the integrated debugger in Visual Studio to debug ASP.NET Razor pages, see [Programming ASP.NET Web Pages (Razor) Using Visual Studio](https://go.microsoft.com/fwlink/?LinkId=205854).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e82b-201">其他资源</span><span class="sxs-lookup"><span data-stu-id="8e82b-201">Additional Resources</span></span>

- [<span data-ttu-id="8e82b-202">使用 Visual Studio 编程 ASP.NET Web 页 (Razor)</span><span class="sxs-lookup"><span data-stu-id="8e82b-202">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>](https://go.microsoft.com/fwlink/?LinkId=205854)
- <span data-ttu-id="8e82b-203">[IIS 服务器变量](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)(MSDN)</span><span class="sxs-lookup"><span data-stu-id="8e82b-203">[IIS Server Variables](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) (MSDN)</span></span>
- <span data-ttu-id="8e82b-204">[识别环境变量](https://technet.microsoft.com/library/dd560744(WS.10).aspx)(TechNet)</span><span class="sxs-lookup"><span data-stu-id="8e82b-204">[Recognized Environment Variables](https://technet.microsoft.com/library/dd560744(WS.10).aspx) (TechNet)</span></span>
