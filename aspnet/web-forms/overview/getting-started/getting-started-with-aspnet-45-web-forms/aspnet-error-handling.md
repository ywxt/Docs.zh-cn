---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET 错误处理 |Microsoft Docs
author: Erikre
description: 本教程系列将指导您学习生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: aspnetcontent
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 8d6c19be7c77079b870261d1c4cf0ea62e0e2fd6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807585"
---
<a name="aspnet-error-handling"></a><span data-ttu-id="8470b-103">ASP.NET 错误处理</span><span class="sxs-lookup"><span data-stu-id="8470b-103">ASP.NET Error Handling</span></span>
====================
<span data-ttu-id="8470b-104">通过[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="8470b-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="8470b-105">[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="8470b-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="8470b-106">此教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="8470b-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="8470b-107">Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)可随附于本系列教程。</span><span class="sxs-lookup"><span data-stu-id="8470b-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="8470b-108">在本教程中，您将修改 Wingtip Toys 示例应用程序，包括错误处理和错误日志记录。</span><span class="sxs-lookup"><span data-stu-id="8470b-108">In this tutorial, you will modify the Wingtip Toys sample application to include error handling and error logging.</span></span> <span data-ttu-id="8470b-109">错误处理将允许应用程序适当地处理错误并相应地显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="8470b-109">Error handling will allow the application to gracefully handle errors and display error messages accordingly.</span></span> <span data-ttu-id="8470b-110">错误日志记录将允许您查找和修复已发生的错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-110">Error logging will allow you to find and fix errors that have occurred.</span></span> <span data-ttu-id="8470b-111">本教程上一教程为基础"URL 路由"，并为 Wingtip Toys 教程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="8470b-111">This tutorial builds on the previous tutorial "URL Routing" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="8470b-112">你将学习：</span><span class="sxs-lookup"><span data-stu-id="8470b-112">What you'll learn:</span></span>

- <span data-ttu-id="8470b-113">如何添加全局错误处理的应用程序的配置。</span><span class="sxs-lookup"><span data-stu-id="8470b-113">How to add global error handling to the application's configuration.</span></span>
- <span data-ttu-id="8470b-114">如何添加错误处理在应用程序、 页面和代码级别。</span><span class="sxs-lookup"><span data-stu-id="8470b-114">How to add error handling at the application, page, and code levels.</span></span>
- <span data-ttu-id="8470b-115">如何记录供以后查看的错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-115">How to log errors for later review.</span></span>
- <span data-ttu-id="8470b-116">如何显示错误消息，不会危及安全性。</span><span class="sxs-lookup"><span data-stu-id="8470b-116">How to display error messages that do not compromise security.</span></span>
- <span data-ttu-id="8470b-117">如何实现错误记录模块和处理程序 (ELMAH) 错误日志记录。</span><span class="sxs-lookup"><span data-stu-id="8470b-117">How to implement Error Logging Modules and Handlers (ELMAH) error logging.</span></span>

## <a name="overview"></a><span data-ttu-id="8470b-118">概述</span><span class="sxs-lookup"><span data-stu-id="8470b-118">Overview</span></span>

<span data-ttu-id="8470b-119">ASP.NET 应用程序必须能够处理在一致的方式执行期间发生的错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-119">ASP.NET applications must be able to handle errors that occur during execution in a consistent manner.</span></span> <span data-ttu-id="8470b-120">ASP.NET 使用公共语言运行时 (CLR)，它提供一种方法向应用程序错误通知以统一的方式。</span><span class="sxs-lookup"><span data-stu-id="8470b-120">ASP.NET uses the common language runtime (CLR), which provides a way of notifying applications of errors in a uniform way.</span></span> <span data-ttu-id="8470b-121">出现错误时，将引发异常。</span><span class="sxs-lookup"><span data-stu-id="8470b-121">When an error occurs, an exception is thrown.</span></span> <span data-ttu-id="8470b-122">例外情况是任何错误、 条件或应用程序遇到的意外的行为。</span><span class="sxs-lookup"><span data-stu-id="8470b-122">An exception is any error, condition, or unexpected behavior that an application encounters.</span></span>

<span data-ttu-id="8470b-123">在 .NET Framework 中，异常是从 `System.Exception` 类继承的对象。</span><span class="sxs-lookup"><span data-stu-id="8470b-123">In the .NET Framework, an exception is an object that inherits from the `System.Exception` class.</span></span> <span data-ttu-id="8470b-124">异常引发自发生问题的代码区域。</span><span class="sxs-lookup"><span data-stu-id="8470b-124">An exception is thrown from an area of code where a problem has occurred.</span></span> <span data-ttu-id="8470b-125">异常调用堆栈中向上传递给该应用程序提供代码来处理异常的其中一个位置。</span><span class="sxs-lookup"><span data-stu-id="8470b-125">The exception is passed up the call stack to a place where the application provides code to handle the exception.</span></span> <span data-ttu-id="8470b-126">如果应用程序不处理异常，强制浏览器显示的错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-126">If the application does not handle the exception, the browser is forced to display the error details.</span></span>

<span data-ttu-id="8470b-127">最佳做法是，处理中的代码级别中的错误`Try` / `Catch` / `Finally`内你的代码块中。</span><span class="sxs-lookup"><span data-stu-id="8470b-127">As a best practice, handle errors in at the code level in `Try`/`Catch`/`Finally` blocks within your code.</span></span> <span data-ttu-id="8470b-128">请尝试将这些块，以便用户可以更正出现的上下文中的问题。</span><span class="sxs-lookup"><span data-stu-id="8470b-128">Try to place these blocks so that the user can correct problems in the context in which they occur.</span></span> <span data-ttu-id="8470b-129">如果错误处理块太远而从发生错误，变得更加困难，为用户提供所需来解决该问题的信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-129">If the error handling blocks are too far away from where the error occurred, it becomes more difficult to provide users with the information they need to fix the problem.</span></span>

### <a name="exception-class"></a><span data-ttu-id="8470b-130">异常类</span><span class="sxs-lookup"><span data-stu-id="8470b-130">Exception Class</span></span>

<span data-ttu-id="8470b-131">异常类是异常从中继承的基类。</span><span class="sxs-lookup"><span data-stu-id="8470b-131">The Exception class is the base class from which exceptions inherit.</span></span> <span data-ttu-id="8470b-132">大多数异常对象是异常类的一些派生类的实例，如`SystemException`类，`IndexOutOfRangeException`类，或`ArgumentNullException`类。</span><span class="sxs-lookup"><span data-stu-id="8470b-132">Most exception objects are instances of some derived class of the Exception class, such as the `SystemException` class, the `IndexOutOfRangeException` class, or the `ArgumentNullException` class.</span></span> <span data-ttu-id="8470b-133">异常类具有属性，如`StackTrace`属性，`InnerException`属性，并`Message`属性，提供有关已发生的错误的特定信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-133">The Exception class has properties, such as the `StackTrace` property, the `InnerException` property, and the `Message` property, that provide specific information about the error that has occurred.</span></span>

### <a name="exception-inheritance-hierarchy"></a><span data-ttu-id="8470b-134">异常继承层次结构</span><span class="sxs-lookup"><span data-stu-id="8470b-134">Exception Inheritance Hierarchy</span></span>

<span data-ttu-id="8470b-135">运行时有一组基本的异常派生自`SystemException`时遇到异常，将引发运行时的类。</span><span class="sxs-lookup"><span data-stu-id="8470b-135">The runtime has a base set of exceptions deriving from the `SystemException` class that the runtime throws when an exception is encountered.</span></span> <span data-ttu-id="8470b-136">从异常类，如继承的类的大多数`IndexOutOfRangeException`类和`ArgumentNullException`类中，不实现其他成员。</span><span class="sxs-lookup"><span data-stu-id="8470b-136">Most of the classes that inherit from the Exception class, such as the `IndexOutOfRangeException` class and the `ArgumentNullException` class, do not implement additional members.</span></span> <span data-ttu-id="8470b-137">因此，最重要的异常的信息可在层次结构的异常、 异常名称和异常所含的信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-137">Therefore, the most important information for an exception can be found in the hierarchy of exceptions, the exception name, and the information contained in the exception.</span></span>

### <a name="exception-handling-hierarchy"></a><span data-ttu-id="8470b-138">异常处理层次结构</span><span class="sxs-lookup"><span data-stu-id="8470b-138">Exception Handling Hierarchy</span></span>

<span data-ttu-id="8470b-139">在 ASP.NET Web 窗体应用程序，可以基于特定处理层次结构处理异常。</span><span class="sxs-lookup"><span data-stu-id="8470b-139">In an ASP.NET Web Forms application, exceptions can be handled based on a specific handling hierarchy.</span></span> <span data-ttu-id="8470b-140">可以在以下级别上处理的异常：</span><span class="sxs-lookup"><span data-stu-id="8470b-140">An exception can be handled at the following levels:</span></span>

- <span data-ttu-id="8470b-141">应用程序级别</span><span class="sxs-lookup"><span data-stu-id="8470b-141">Application level</span></span>
- <span data-ttu-id="8470b-142">页级别</span><span class="sxs-lookup"><span data-stu-id="8470b-142">Page level</span></span>
- <span data-ttu-id="8470b-143">代码级别</span><span class="sxs-lookup"><span data-stu-id="8470b-143">Code level</span></span>

<span data-ttu-id="8470b-144">当应用程序处理异常时，可以检索，向用户显示有关异常的异常类中继承的其他信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-144">When an application handles exceptions, additional information about the exception that is inherited from the Exception class can often be retrieved and displayed to the user.</span></span> <span data-ttu-id="8470b-145">除了应用程序、 页面和代码级别，还可以处理在 HTTP 模块级别和通过使用 IIS 自定义处理程序的异常。</span><span class="sxs-lookup"><span data-stu-id="8470b-145">In addition to application, page, and code level, you can also handle exceptions at the HTTP module level and by using an IIS custom handler.</span></span>

### <a name="application-level-error-handling"></a><span data-ttu-id="8470b-146">应用程序级别错误处理</span><span class="sxs-lookup"><span data-stu-id="8470b-146">Application Level Error Handling</span></span>

<span data-ttu-id="8470b-147">通过修改应用程序的配置或添加，您可以处理应用程序级别的默认错误`Application_Error`处理程序中的*Global.asax*在应用程序文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-147">You can handle default errors at the application level either by modifying your application's configuration or by adding an `Application_Error` handler in the *Global.asax* file of your application.</span></span>

<span data-ttu-id="8470b-148">可以通过添加处理默认错误和 HTTP 错误`customErrors`部分*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-148">You can handle default errors and HTTP errors by adding a `customErrors` section to the *Web.config* file.</span></span> <span data-ttu-id="8470b-149">`customErrors`部分允许您指定将重定向到用户，发生错误时的默认页。</span><span class="sxs-lookup"><span data-stu-id="8470b-149">The `customErrors` section allows you to specify a default page that users will be redirected to when an error occurs.</span></span> <span data-ttu-id="8470b-150">它还允许您指定的特定状态代码错误的各个页面。</span><span class="sxs-lookup"><span data-stu-id="8470b-150">It also allows you to specify individual pages for specific status code errors.</span></span>

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

<span data-ttu-id="8470b-151">遗憾的是，当使用配置将用户重定向到其他页面时，您不具有所发生的错误的详细信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-151">Unfortunately, when you use the configuration to redirect the user to a different page, you do not have the details of the error that occurred.</span></span>

<span data-ttu-id="8470b-152">但是，您可以捕获任意位置出现的错误在应用程序中通过将代码添加到`Application_Error`处理程序中的*Global.asax*文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-152">However, you can trap errors that occur anywhere in your application by adding code to the `Application_Error` handler in the *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a><span data-ttu-id="8470b-153">页面级别错误事件处理</span><span class="sxs-lookup"><span data-stu-id="8470b-153">Page Level Error Event Handling</span></span>

<span data-ttu-id="8470b-154">页面级别处理程序使用户返回到页上出现错误，但由于没有维持控件的实例，将不再有任何内容页上。</span><span class="sxs-lookup"><span data-stu-id="8470b-154">A page-level handler returns the user to the page where the error occurred, but because instances of controls are not maintained, there will no longer be anything on the page.</span></span> <span data-ttu-id="8470b-155">若要向应用程序的用户提供错误详细信息，必须专门将写入错误详细信息页。</span><span class="sxs-lookup"><span data-stu-id="8470b-155">To provide the error details to the user of the application, you must specifically write the error details to the page.</span></span>

<span data-ttu-id="8470b-156">记录未处理的错误，或若要将用户转到可以显示有用信息的页面，通常会使用页级错误处理程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-156">You would typically use a page-level error handler to log unhandled errors or to take the user to a page that can display helpful information.</span></span>

<span data-ttu-id="8470b-157">此代码示例演示在 ASP.NET Web 页中的错误事件的处理程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-157">This code example shows a handler for the Error event in an ASP.NET Web page.</span></span> <span data-ttu-id="8470b-158">此处理程序捕获不能处理中的所有异常`try` / `catch`页中的块。</span><span class="sxs-lookup"><span data-stu-id="8470b-158">This handler catches all exceptions that are not already handled within `try`/`catch` blocks in the page.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

<span data-ttu-id="8470b-159">处理错误后，您必须清除它通过调用`ClearError`的服务器对象的方法 (`HttpServerUtility`类)，否则你将看到以前发生了错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-159">After you handle an error, you must clear it by calling the `ClearError` method of the Server object (`HttpServerUtility` class), otherwise you will see an error that has previously occurred.</span></span>

### <a name="code-level-error-handling"></a><span data-ttu-id="8470b-160">代码级别错误处理</span><span class="sxs-lookup"><span data-stu-id="8470b-160">Code Level Error Handling</span></span>

<span data-ttu-id="8470b-161">Try-catch 语句由 try 块跟一个或多个 catch 子句，指定不同异常的处理程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-161">The try-catch statement consists of a try block followed by one or more catch clauses, which specify handlers for different exceptions.</span></span> <span data-ttu-id="8470b-162">时引发异常，公共语言运行时 (CLR) 查找处理此异常的 catch 语句。</span><span class="sxs-lookup"><span data-stu-id="8470b-162">When an exception is thrown, the common language runtime (CLR) looks for the catch statement that handles this exception.</span></span> <span data-ttu-id="8470b-163">如果当前正在执行的方法不包含 catch 块，则 CLR 会查看调用当前方法中，依次类推，在调用堆栈上的方法。</span><span class="sxs-lookup"><span data-stu-id="8470b-163">If the currently executing method does not contain a catch block, the CLR looks at the method that called the current method, and so on, up the call stack.</span></span> <span data-ttu-id="8470b-164">如果不找到任何 catch 块，则 CLR 向用户显示一条未处理的异常消息，并停止执行程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-164">If no catch block is found, then the CLR displays an unhandled exception message to the user and stops execution of the program.</span></span>

<span data-ttu-id="8470b-165">下面的代码示例演示常见的使用方法`try` / `catch` / `finally`来处理错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-165">The following code example shows a common way of using `try`/`catch`/`finally` to handle errors.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

<span data-ttu-id="8470b-166">在上述代码中，try 块包含需要避免可能的异常的代码。</span><span class="sxs-lookup"><span data-stu-id="8470b-166">In the above code, the try block contains the code that needs to be guarded against a possible exception.</span></span> <span data-ttu-id="8470b-167">直到引发异常或已成功完成块将执行此块。</span><span class="sxs-lookup"><span data-stu-id="8470b-167">The block is executed until either an exception is thrown or the block is completed successfully.</span></span> <span data-ttu-id="8470b-168">如果任一`FileNotFoundException`异常或`IOException`发生的异常，将执行转移到另一页。</span><span class="sxs-lookup"><span data-stu-id="8470b-168">If either a `FileNotFoundException` exception or an `IOException` exception occurs, the execution is transferred to a different page.</span></span> <span data-ttu-id="8470b-169">然后，在包含的代码执行块最后，无论是否出错。</span><span class="sxs-lookup"><span data-stu-id="8470b-169">Then, the code contained in the finally block is executed, whether an error occurred or not.</span></span>

## <a name="adding-error-logging-support"></a><span data-ttu-id="8470b-170">添加错误日志记录支持</span><span class="sxs-lookup"><span data-stu-id="8470b-170">Adding Error Logging Support</span></span>

<span data-ttu-id="8470b-171">添加错误处理 Wingtip Toys 示例应用程序之前, 中，您将添加错误日志记录支持通过添加`ExceptionUtility`类来*逻辑*文件夹。</span><span class="sxs-lookup"><span data-stu-id="8470b-171">Before adding error handling to the Wingtip Toys sample application, you will add error logging support by adding an `ExceptionUtility` class to the *Logic* folder.</span></span> <span data-ttu-id="8470b-172">通过执行此操作，请在每次应用程序处理错误，错误详细信息将添加到错误日志文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-172">By doing this, each time the application handles an error, the error details will be added to the error log file.</span></span>

1. <span data-ttu-id="8470b-173">右键单击*逻辑*文件夹，然后选择**添加** - &gt; **新项**。</span><span class="sxs-lookup"><span data-stu-id="8470b-173">Right-click the *Logic* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="8470b-174">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="8470b-174">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="8470b-175">选择**Visual C#**  - &gt; **代码**在左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="8470b-175">Select the **Visual C#** -&gt; **Code** templates group on the left.</span></span> <span data-ttu-id="8470b-176">然后，选择**类**从中间列表并将其命名**ExceptionUtility.cs**。</span><span class="sxs-lookup"><span data-stu-id="8470b-176">Then, select **Class**from the middle list and name it **ExceptionUtility.cs**.</span></span>
3. <span data-ttu-id="8470b-177">选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="8470b-177">Choose **Add**.</span></span> <span data-ttu-id="8470b-178">显示新类文件中。</span><span class="sxs-lookup"><span data-stu-id="8470b-178">The new class file is displayed.</span></span>
4. <span data-ttu-id="8470b-179">将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="8470b-179">Replace the existing code with the following:</span></span>  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

<span data-ttu-id="8470b-180">异常发生时，可以通过调用写入到的异常错误日志文件异常`LogException`方法。</span><span class="sxs-lookup"><span data-stu-id="8470b-180">When an exception occurs, the exception can be written to an exception log file by calling the `LogException` method.</span></span> <span data-ttu-id="8470b-181">此方法采用两个参数、 异常对象和一个包含有关异常的源的详细信息的字符串。</span><span class="sxs-lookup"><span data-stu-id="8470b-181">This method takes two parameters, the exception object and a string containing details about the source of the exception.</span></span> <span data-ttu-id="8470b-182">异常错误日志写入到*errorlog.txt 中*中的文件*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="8470b-182">The exception log is written to the *ErrorLog.txt* file in the *App\_Data* folder.</span></span>

### <a name="adding-an-error-page"></a><span data-ttu-id="8470b-183">添加一个错误页面</span><span class="sxs-lookup"><span data-stu-id="8470b-183">Adding an Error Page</span></span>

<span data-ttu-id="8470b-184">Wingtip Toys 示例应用程序，在一页将用于显示错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-184">In the Wingtip Toys sample application, one page will be used to display errors.</span></span> <span data-ttu-id="8470b-185">错误页用于向站点的用户显示一条安全错误消息。</span><span class="sxs-lookup"><span data-stu-id="8470b-185">The error page is designed to show a secure error message to users of the site.</span></span> <span data-ttu-id="8470b-186">但是，如果用户是发出 HTTP 请求的计算机上本地提供代码所在的开发人员，其他错误详细信息将显示在错误页。</span><span class="sxs-lookup"><span data-stu-id="8470b-186">However, if the user is a developer making an HTTP request that is being served locally on the machine where the code lives, additional error details will be displayed on the error page.</span></span>

1. <span data-ttu-id="8470b-187">右键单击项目名称 (**Wingtip Toys**) 中**解决方案资源管理器**，然后选择**添加** - &gt; **新项**.</span><span class="sxs-lookup"><span data-stu-id="8470b-187">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="8470b-188">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="8470b-188">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="8470b-189">选择**Visual C#**  - &gt; **Web**在左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="8470b-189">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="8470b-190">从中间列表中选择**包含母版页的 Web 窗体**，并将其命名**ErrorPage.aspx**。</span><span class="sxs-lookup"><span data-stu-id="8470b-190">From the middle list, select **Web Form with Master Page**,and name it **ErrorPage.aspx**.</span></span>
3. <span data-ttu-id="8470b-191">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="8470b-191">Click **Add**.</span></span>
4. <span data-ttu-id="8470b-192">选择*Site.Master*另存为母版页文件，然后选择**确定**。</span><span class="sxs-lookup"><span data-stu-id="8470b-192">Select the *Site.Master* file as the master page, and then choose **OK**.</span></span>
5. <span data-ttu-id="8470b-193">使用以下内容替换现有标记：</span><span class="sxs-lookup"><span data-stu-id="8470b-193">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. <span data-ttu-id="8470b-194">隐藏代码的现有代码替换为 (*ErrorPage.aspx.cs*) 以使其显示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8470b-194">Replace the existing code of the code-behind (*ErrorPage.aspx.cs*) so that it appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

<span data-ttu-id="8470b-195">当显示错误页时，`Page_Load`执行事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-195">When the error page is displayed, the `Page_Load` event handler is executed.</span></span> <span data-ttu-id="8470b-196">在`Page_Load`处理程序，确定已先处理该错误的位置。</span><span class="sxs-lookup"><span data-stu-id="8470b-196">In the `Page_Load` handler, the location of where the error was first handled is determined.</span></span> <span data-ttu-id="8470b-197">然后，发生的最后一个错误由调用`GetLastError`服务器对象的方法。</span><span class="sxs-lookup"><span data-stu-id="8470b-197">Then, the last error that occurred is determined by call the `GetLastError` method of the Server object.</span></span> <span data-ttu-id="8470b-198">如果异常不再存在，则创建一般异常。</span><span class="sxs-lookup"><span data-stu-id="8470b-198">If the exception no longer exists, a generic exception is created.</span></span> <span data-ttu-id="8470b-199">然后，如果本地发出 HTTP 请求，会显示所有错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-199">Then, if the HTTP request was made locally, all error details are shown.</span></span> <span data-ttu-id="8470b-200">在这种情况下，仅运行 web 应用程序的本地计算机将看到这些错误的详细信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-200">In this case, only the local machine running the web application will see these error details.</span></span> <span data-ttu-id="8470b-201">已显示的错误信息后，错误将添加到日志文件，并从服务器中清除该错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-201">After the error information has been displayed, the error is added to the log file and the error is cleared from the server.</span></span>

### <a name="displaying-unhandled-error-messages-for-the-application"></a><span data-ttu-id="8470b-202">应用程序显示未处理的错误消息</span><span class="sxs-lookup"><span data-stu-id="8470b-202">Displaying Unhandled Error Messages for the Application</span></span>

<span data-ttu-id="8470b-203">通过添加`customErrors`部分*Web.config*文件中，可以快速处理整个应用程序发生的简单错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-203">By adding a `customErrors` section to the *Web.config* file, you can quickly handle simple errors that occur throughout the application.</span></span> <span data-ttu-id="8470b-204">此外可以指定如何处理错误基于其状态代码值，例如 404-找不到文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-204">You can also specify how to handle errors based on their status code value, such as 404 - File not found.</span></span>

#### <a name="update-the-configuration"></a><span data-ttu-id="8470b-205">更新配置</span><span class="sxs-lookup"><span data-stu-id="8470b-205">Update the Configuration</span></span>

<span data-ttu-id="8470b-206">通过添加更新的配置`customErrors`部分*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-206">Update the configuration by adding a `customErrors` section to the *Web.config* file.</span></span>

1. <span data-ttu-id="8470b-207">在中**解决方案资源管理器**，找到并打开*Web.config* Wingtip Toys 示例应用程序根目录的文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-207">In **Solution Explorer**, find and open the *Web.config* file at the root of the Wingtip Toys sample application.</span></span>
2. <span data-ttu-id="8470b-208">添加`customErrors`部分*Web.config*文件内`<system.web>`节点，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8470b-208">Add the `customErrors` section to the *Web.config* file within the `<system.web>` node as follows:</span></span>   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. <span data-ttu-id="8470b-209">保存*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-209">Save the *Web.config* file.</span></span>

<span data-ttu-id="8470b-210">`customErrors`部分指定的模式，它被设置为"开启"。</span><span class="sxs-lookup"><span data-stu-id="8470b-210">The `customErrors` section specifies the mode, which is set to "On".</span></span> <span data-ttu-id="8470b-211">它还指定`defaultRedirect`，它将告诉哪一页时出错时要导航到应用程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-211">It also specifies the `defaultRedirect`, which tells the application which page to navigate to when an error occurs.</span></span> <span data-ttu-id="8470b-212">此外，您添加了一个特定的错误元素，指定如何处理 404 错误，找不到页面时。</span><span class="sxs-lookup"><span data-stu-id="8470b-212">In addition, you have added a specific error element that specifies how to handle a 404 error when a page is not found.</span></span> <span data-ttu-id="8470b-213">稍后在本教程中，你将添加额外的错误处理，将捕获的应用程序级别的错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-213">Later in this tutorial, you will add additional error handling that will capture the details of an error at the application level.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="8470b-214">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="8470b-214">Running the Application</span></span>

<span data-ttu-id="8470b-215">可以运行应用程序现在以查看更新的路由。</span><span class="sxs-lookup"><span data-stu-id="8470b-215">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="8470b-216">按**F5**运行 Wingtip Toys 示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-216">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="8470b-217">在浏览器将打开并显示*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="8470b-217">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="8470b-218">以下 URL 输入到浏览器 (请务必使用**你**端口号):</span><span class="sxs-lookup"><span data-stu-id="8470b-218">Enter the following URL into the browser (be sure to use **your** port number):</span></span>  
    `https://localhost:44300/NoPage.aspx`
3. <span data-ttu-id="8470b-219">审阅*ErrorPage.aspx*浏览器中显示。</span><span class="sxs-lookup"><span data-stu-id="8470b-219">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 错误处理-找不到页面错误](aspnet-error-handling/_static/image1.png)

<span data-ttu-id="8470b-221">当请求*NoPage.aspx*页上，不存在，则错误页将显示简单的错误消息和详细的错误信息如果提供了更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-221">When you request the *NoPage.aspx* page, which does not exist, the error page will show the simple error message and the detailed error information if additional details are available.</span></span> <span data-ttu-id="8470b-222">但是，如果用户请求从远程位置不存在页，则错误页将只会以红色显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="8470b-222">However, if the user requested a non-existent page from a remote location, the error page would only show the error message in red.</span></span>

### <a name="including-an-exception-for-testing-purposes"></a><span data-ttu-id="8470b-223">出于测试目的包括异常</span><span class="sxs-lookup"><span data-stu-id="8470b-223">Including an Exception for Testing Purposes</span></span>

<span data-ttu-id="8470b-224">若要验证你的应用程序的运行时出现错误的方式发生，在 ASP.NET 中特意创建错误条件。</span><span class="sxs-lookup"><span data-stu-id="8470b-224">To verify how your application will function when an error occurs, you can deliberately create error conditions in ASP.NET.</span></span> <span data-ttu-id="8470b-225">在 Wingtip Toys 示例应用程序，将加载默认页面以查看会发生什么情况时引发测试异常。</span><span class="sxs-lookup"><span data-stu-id="8470b-225">In the Wingtip Toys sample application, you will throw a test exception when the default page loads to see what happens.</span></span>

1. <span data-ttu-id="8470b-226">打开的代码隐藏*Default.aspx* Visual Studio 中的页。</span><span class="sxs-lookup"><span data-stu-id="8470b-226">Open the code-behind of the *Default.aspx* page in Visual Studio.</span></span>   
   <span data-ttu-id="8470b-227">*Default.aspx.cs* ，将显示代码隐藏页。</span><span class="sxs-lookup"><span data-stu-id="8470b-227">The *Default.aspx.cs* code-behind page will be displayed.</span></span>
2. <span data-ttu-id="8470b-228">在`Page_Load`处理程序中，添加代码，以便该处理程序出现，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8470b-228">In the `Page_Load` handler, add code so that the handler appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

<span data-ttu-id="8470b-229">就可以创建各种不同类型的异常。</span><span class="sxs-lookup"><span data-stu-id="8470b-229">It is possible to create various different types of exceptions.</span></span> <span data-ttu-id="8470b-230">在上述代码中，将创建`InvalidOperationException`时*Default.aspx*加载页面。</span><span class="sxs-lookup"><span data-stu-id="8470b-230">In the above code, you are creating an `InvalidOperationException` when the *Default.aspx* page is loaded.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="8470b-231">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="8470b-231">Running the Application</span></span>

<span data-ttu-id="8470b-232">可以运行应用程序以查看应用程序如何处理异常。</span><span class="sxs-lookup"><span data-stu-id="8470b-232">You can run the application to see how the application handles the exception.</span></span>

1. <span data-ttu-id="8470b-233">按**CTRL + F5**运行 Wingtip Toys 示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-233">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="8470b-234">应用程序将引发 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="8470b-234">The application throws the InvalidOperationException.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="8470b-235">必须按下**CTRL + F5**而不会中断到代码以在 Visual Studio 中查看该错误的源中显示的页。</span><span class="sxs-lookup"><span data-stu-id="8470b-235">You must press **CTRL+F5** to display the page without breaking into the code to view the source of the error in Visual Studio.</span></span>
2. <span data-ttu-id="8470b-236">审阅*ErrorPage.aspx*浏览器中显示。</span><span class="sxs-lookup"><span data-stu-id="8470b-236">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 错误处理的错误页](aspnet-error-handling/_static/image2.png)

<span data-ttu-id="8470b-238">正如您所看到错误详细信息中，已捕获异常`customError`主题中*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-238">As you can see in the error details, the exception was trapped by the `customError` section in the *Web.config* file.</span></span>

### <a name="adding-application-level-error-handling"></a><span data-ttu-id="8470b-239">添加应用程序级别的错误处理</span><span class="sxs-lookup"><span data-stu-id="8470b-239">Adding Application-Level Error Handling</span></span>

<span data-ttu-id="8470b-240">而不是异常使用陷阱`customErrors`主题中*Web.config*文件中，获得有关异常的一些信息，其中您可以捕获应用程序级别的错误并检索错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-240">Rather than trap the exception using the `customErrors` section in the *Web.config* file, where you gain little information about the exception, you can trap the error at the application level and retrieve error details.</span></span>

1. <span data-ttu-id="8470b-241">在中**解决方案资源管理器**，找到并打开*Global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-241">In **Solution Explorer**, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="8470b-242">添加**应用程序\_错误**处理程序，使其显示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8470b-242">Add an **Application\_Error** handler so that it appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

<span data-ttu-id="8470b-243">在应用程序中发生错误时`Application_Error`调用处理程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-243">When an error occurs in the application, the `Application_Error` handler is called.</span></span> <span data-ttu-id="8470b-244">此处理程序中的最后一个异常检索并查看。</span><span class="sxs-lookup"><span data-stu-id="8470b-244">In this handler, the last exception is retrieved and reviewed.</span></span> <span data-ttu-id="8470b-245">如果异常为未处理，并且该异常包含内部异常详细信息 (即，`InnerException`不为 null)，该应用程序来将执行转移到错误页并显示异常详细信息的位置。</span><span class="sxs-lookup"><span data-stu-id="8470b-245">If the exception was unhandled and the exception contains inner-exception details (that is, `InnerException` is not null), the application transfers execution to the error page where the exception details are displayed.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="8470b-246">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="8470b-246">Running the Application</span></span>

<span data-ttu-id="8470b-247">可以运行应用程序以查看通过处理应用程序级别的异常提供的其他错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-247">You can run the application to see the additional error details provided by handling the exception at the application level.</span></span>

1. <span data-ttu-id="8470b-248">按**CTRL + F5**运行 Wingtip Toys 示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-248">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="8470b-249">应用程序将引发`InvalidOperationException`。</span><span class="sxs-lookup"><span data-stu-id="8470b-249">The application throws the `InvalidOperationException` .</span></span>
2. <span data-ttu-id="8470b-250">审阅*ErrorPage.aspx*浏览器中显示。</span><span class="sxs-lookup"><span data-stu-id="8470b-250">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 错误处理的应用程序级别错误](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a><span data-ttu-id="8470b-252">添加页面级别的错误处理</span><span class="sxs-lookup"><span data-stu-id="8470b-252">Adding Page-Level Error Handling</span></span>

<span data-ttu-id="8470b-253">您可以添加页面级别的错误处理到一个页面是通过添加`ErrorPage`归于`@Page`指令的页上，或通过添加`Page_Error`到页面的代码隐藏的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-253">You can add page-level error handling to a page either by using adding an `ErrorPage` attribute to the `@Page` directive of the page, or by adding a `Page_Error` event handler to the code-behind of a page.</span></span> <span data-ttu-id="8470b-254">在本部分中，您将添加`Page_Error`事件处理程序会将传输到执行*ErrorPage.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="8470b-254">In this section, you will add a `Page_Error` event handler that will transfer execution to the *ErrorPage.aspx* page.</span></span>

1. <span data-ttu-id="8470b-255">在中**解决方案资源管理器**，找到并打开*Default.aspx.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-255">In **Solution Explorer**, find and open the *Default.aspx.cs* file.</span></span>
2. <span data-ttu-id="8470b-256">添加`Page_Error`处理程序，以便代码隐藏显示为遵循：</span><span class="sxs-lookup"><span data-stu-id="8470b-256">Add a `Page_Error` handler so that the code-behind appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

<span data-ttu-id="8470b-257">在页上，发生错误时`Page_Error`调用事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-257">When an error occurs on the page, the `Page_Error` event handler is called.</span></span> <span data-ttu-id="8470b-258">此处理程序中的最后一个异常检索并查看。</span><span class="sxs-lookup"><span data-stu-id="8470b-258">In this handler, the last exception is retrieved and reviewed.</span></span> <span data-ttu-id="8470b-259">如果`InvalidOperationException`发生，`Page_Error`事件处理程序来将执行转移到错误页并显示异常详细信息的位置。</span><span class="sxs-lookup"><span data-stu-id="8470b-259">If an `InvalidOperationException` occurs, the `Page_Error` event handler transfers execution to the error page where the exception details are displayed.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="8470b-260">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="8470b-260">Running the Application</span></span>

<span data-ttu-id="8470b-261">可以运行应用程序现在以查看更新的路由。</span><span class="sxs-lookup"><span data-stu-id="8470b-261">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="8470b-262">按**CTRL + F5**运行 Wingtip Toys 示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-262">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="8470b-263">应用程序将引发`InvalidOperationException`。</span><span class="sxs-lookup"><span data-stu-id="8470b-263">The application throws the `InvalidOperationException` .</span></span>
2. <span data-ttu-id="8470b-264">审阅*ErrorPage.aspx*浏览器中显示。</span><span class="sxs-lookup"><span data-stu-id="8470b-264">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 错误处理的页级别的错误](aspnet-error-handling/_static/image4.png)
3. <span data-ttu-id="8470b-266">关闭浏览器窗口中。</span><span class="sxs-lookup"><span data-stu-id="8470b-266">Close your browser window.</span></span>

### <a name="removing-the-exception-used-for-testing"></a><span data-ttu-id="8470b-267">删除用于测试的异常</span><span class="sxs-lookup"><span data-stu-id="8470b-267">Removing the Exception Used for Testing</span></span>

<span data-ttu-id="8470b-268">若要允许 Wingtip Toys 示例应用程序，而不引发的异常在本教程前面部分添加函数，请删除该异常。</span><span class="sxs-lookup"><span data-stu-id="8470b-268">To allow the Wingtip Toys sample application to function without throwing the exception you added earlier in this tutorial, remove the exception.</span></span>

1. <span data-ttu-id="8470b-269">打开的代码隐藏*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="8470b-269">Open the code-behind of the *Default.aspx* page.</span></span>
2. <span data-ttu-id="8470b-270">在`Page_Load`处理程序中，删除引发异常，以便该处理程序出现，如下所示的代码：</span><span class="sxs-lookup"><span data-stu-id="8470b-270">In the `Page_Load` handler, remove the code that throws the exception so that the handler appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a><span data-ttu-id="8470b-271">添加代码级别的错误日志记录</span><span class="sxs-lookup"><span data-stu-id="8470b-271">Adding Code-Level Error Logging</span></span>

<span data-ttu-id="8470b-272">在本教程前面所述，可以添加 try/catch 语句，尝试运行一段代码并处理第一个出现的错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-272">As mentioned earlier in this tutorial, you can add try/catch statements to attempt to run a section of code and handle the first error that occurs.</span></span> <span data-ttu-id="8470b-273">在此示例中，将仅写入错误详细信息的错误日志文件，以便可以稍后查看错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-273">In this example, you will only write the error details to the error log file so that the error can be reviewed later.</span></span>

1. <span data-ttu-id="8470b-274">在中**解决方案资源管理器**，在*逻辑*文件夹中，找到并打开*PayPalFunctions.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-274">In **Solution Explorer**, in the *Logic* folder, find and open the *PayPalFunctions.cs* file.</span></span>
2. <span data-ttu-id="8470b-275">更新`HttpCall`方法以便，代码显示为如下所示：</span><span class="sxs-lookup"><span data-stu-id="8470b-275">Update the `HttpCall` method so that the code appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

<span data-ttu-id="8470b-276">上面的代码调用`LogException`方法中包含的`ExceptionUtility`类。</span><span class="sxs-lookup"><span data-stu-id="8470b-276">The above code calls the `LogException` method that is contained in the `ExceptionUtility` class.</span></span> <span data-ttu-id="8470b-277">您添加*ExceptionUtility.cs*类的文件*逻辑*此前在本教程中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8470b-277">You added the *ExceptionUtility.cs* class file to the *Logic* folder earlier in this tutorial.</span></span> <span data-ttu-id="8470b-278">`LogException` 方法采用两个参数。</span><span class="sxs-lookup"><span data-stu-id="8470b-278">The `LogException` method takes two parameters.</span></span> <span data-ttu-id="8470b-279">第一个参数是异常对象。</span><span class="sxs-lookup"><span data-stu-id="8470b-279">The first parameter is the exception object.</span></span> <span data-ttu-id="8470b-280">第二个参数是一个字符串，用来识别错误的源。</span><span class="sxs-lookup"><span data-stu-id="8470b-280">The second parameter is a string used to recognize the source of the error.</span></span>

### <a name="inspecting-the-error-logging-information"></a><span data-ttu-id="8470b-281">检查错误日志记录信息</span><span class="sxs-lookup"><span data-stu-id="8470b-281">Inspecting the Error Logging Information</span></span>

<span data-ttu-id="8470b-282">正如前面提到的可以使用错误日志以确定应首先修复应用程序中的错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-282">As mentioned previously, you can use the error log to determine which errors in your application should be fixed first.</span></span> <span data-ttu-id="8470b-283">当然，将记录已捕获和写入错误日志的错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-283">Of course, only errors that have been trapped and written to the error log will be recorded.</span></span>

1. <span data-ttu-id="8470b-284">在中**解决方案资源管理器**，找到并打开*errorlog.txt 中*文件中*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="8470b-284">In **Solution Explorer**, find and open the *ErrorLog.txt* file in the *App\_Data* folder.</span></span>   
 <span data-ttu-id="8470b-285">可能需要选择"**显示所有文件**"选项或"**刷新**"顶部的选项**解决方案资源管理器**以查看*errorlog.txt 中*文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-285">You may need to select the "**Show All Files**" option or the "**Refresh**" option from the top of **Solution Explorer** to see the *ErrorLog.txt* file.</span></span>
2. <span data-ttu-id="8470b-286">查看 Visual Studio 中显示的错误日志：</span><span class="sxs-lookup"><span data-stu-id="8470b-286">Review the error log displayed in Visual Studio:</span></span> 

    ![ASP.NET 错误处理-errorlog.txt 中](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a><span data-ttu-id="8470b-288">安全的错误消息</span><span class="sxs-lookup"><span data-stu-id="8470b-288">Safe Error Messages</span></span>

<span data-ttu-id="8470b-289">它是**值得注意**，当你的应用程序显示错误消息时，它不应该泄露恶意用户可能会有所攻击你的应用程序中的信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-289">It is **important to note** that when your application displays error messages, it should not give away information that a malicious user might find helpful in attacking your application.</span></span> <span data-ttu-id="8470b-290">例如，如果你的应用程序未成功尝试写入数据库，它不应显示错误消息，包括它所使用的用户名。</span><span class="sxs-lookup"><span data-stu-id="8470b-290">For example, if your application unsuccessfully tries to write in to a database, it should not display an error message that includes the user name it is using.</span></span> <span data-ttu-id="8470b-291">出于此原因，以红色的一般性错误消息显示给用户。</span><span class="sxs-lookup"><span data-stu-id="8470b-291">For this reason, a generic error message in red is displayed to the user.</span></span> <span data-ttu-id="8470b-292">向开发人员在本地计算机上仅显示所有其他错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="8470b-292">All additional error details are only displayed to the developer on the local machine.</span></span>

## <a name="using-elmah"></a><span data-ttu-id="8470b-293">使用 ELMAH</span><span class="sxs-lookup"><span data-stu-id="8470b-293">Using ELMAH</span></span>

<span data-ttu-id="8470b-294">ELMAH （错误日志记录模块和处理程序） 是插入到作为 NuGet 包的 ASP.NET 应用程序错误日志记录功能。</span><span class="sxs-lookup"><span data-stu-id="8470b-294">ELMAH (Error Logging Modules and Handlers) is an error logging facility that you plug into your ASP.NET application as a NuGet package.</span></span> <span data-ttu-id="8470b-295">ELMAH 提供以下功能：</span><span class="sxs-lookup"><span data-stu-id="8470b-295">ELMAH provides the following capabilities:</span></span>

- <span data-ttu-id="8470b-296">未经处理的异常日志记录功能。</span><span class="sxs-lookup"><span data-stu-id="8470b-296">Logging of unhandled exceptions.</span></span>
- <span data-ttu-id="8470b-297">若要查看整个日志记录未处理异常的网页。</span><span class="sxs-lookup"><span data-stu-id="8470b-297">A web page to view the entire log of recoded unhandled exceptions.</span></span>
- <span data-ttu-id="8470b-298">若要查看的每个完整的详细信息的网页记录异常。</span><span class="sxs-lookup"><span data-stu-id="8470b-298">A web page to view the full details of each logged exception.</span></span>
- <span data-ttu-id="8470b-299">它发生的时间在每个错误的电子邮件通知。</span><span class="sxs-lookup"><span data-stu-id="8470b-299">An email notification of each error at the time it occurs.</span></span>
- <span data-ttu-id="8470b-300">从日志的最后 15 个错误的 RSS 源。</span><span class="sxs-lookup"><span data-stu-id="8470b-300">An RSS feed of the last 15 errors from the log.</span></span>

<span data-ttu-id="8470b-301">可以在使用 ELMAH 之前，必须安装它。</span><span class="sxs-lookup"><span data-stu-id="8470b-301">Before you can work with the ELMAH, you must install it.</span></span> <span data-ttu-id="8470b-302">这很容易使用*NuGet*程序包安装程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-302">This is easy using the *NuGet* package installer.</span></span> <span data-ttu-id="8470b-303">如本系列教程前面所述，NuGet 将是 Visual Studio 扩展，它可以更轻松地安装和更新的开放源代码库和 Visual Studio 中的工具。</span><span class="sxs-lookup"><span data-stu-id="8470b-303">As mentioned earlier in this tutorial series, NuGet is a Visual Studio extension that makes it easy to install and update open source libraries and tools in Visual Studio.</span></span>

1. <span data-ttu-id="8470b-304">Visual Studio 中，从**工具**菜单中，选择**库程序包管理器** - &gt; **为解决方案管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="8470b-304">Within Visual Studio, from the **Tools** menu, select **Library Package Manager** -&gt; **Manage NuGet Packages for Solution**.</span></span> 

    ![ASP.NET 错误处理的管理解决方案的 NuGet 包](aspnet-error-handling/_static/image6.png)
2. <span data-ttu-id="8470b-306">**管理 NuGet 包**Visual Studio 中将显示对话框。</span><span class="sxs-lookup"><span data-stu-id="8470b-306">The **Manage NuGet Packages** dialog box is displayed within Visual Studio.</span></span>
3. <span data-ttu-id="8470b-307">在中**管理 NuGet 包**对话框框中，展开**联机**在左侧，然后选择**nuget.org**。然后，找到并安装**ELMAH**包从联机可用包列表。</span><span class="sxs-lookup"><span data-stu-id="8470b-307">In the **Manage NuGet Packages** dialog box, expand **Online** on the left, and then select **nuget.org**. Then, find and install the **ELMAH** package from the list of available packages online.</span></span> 

    ![ASP.NET 错误处理-ELMA NuGet 包](aspnet-error-handling/_static/image7.png)
4. <span data-ttu-id="8470b-309">需要具有 internet 连接才能下载包。</span><span class="sxs-lookup"><span data-stu-id="8470b-309">You will need to have an internet connection to download the package.</span></span>
5. <span data-ttu-id="8470b-310">在中**选择项目**对话框框中，请确保**WingtipToys**选择已选中，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="8470b-310">In the **Select Projects** dialog box, make sure the **WingtipToys** selection is selected, and then click **OK**.</span></span> 

    ![ASP.NET 错误处理的选择项目对话框](aspnet-error-handling/_static/image8.png)
6. <span data-ttu-id="8470b-312">单击**关闭**中**管理 NuGet 包**必要的对话框。</span><span class="sxs-lookup"><span data-stu-id="8470b-312">Click **Close** in **the Manage NuGet Packages** dialog box if needed.</span></span>
7. <span data-ttu-id="8470b-313">如果 Visual Studio 请求重新加载任何打开的文件，选择"**全是**"。</span><span class="sxs-lookup"><span data-stu-id="8470b-313">If Visual Studio requests that you reload any open files, select "**Yes to All**".</span></span>
8. <span data-ttu-id="8470b-314">ELMAH 包本身中添加条目*Web.config*根目录下的项目文件。</span><span class="sxs-lookup"><span data-stu-id="8470b-314">The ELMAH package adds entries for itself in the *Web.config* file at the root of your project.</span></span> <span data-ttu-id="8470b-315">如果 Visual Studio 会要求你如果你想要重新加载修改后*Web.config*文件中，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="8470b-315">If Visual Studio asks you if you want to reload the modified *Web.config* file, click **Yes**.</span></span>

<span data-ttu-id="8470b-316">ELMAH 现已准备好存储出现的任何未处理的错误。</span><span class="sxs-lookup"><span data-stu-id="8470b-316">ELMAH is now ready to store any unhandled errors that occur.</span></span>

### <a name="viewing-the-elmah-log"></a><span data-ttu-id="8470b-317">查看 ELMAH 日志</span><span class="sxs-lookup"><span data-stu-id="8470b-317">Viewing the ELMAH Log</span></span>

<span data-ttu-id="8470b-318">查看 ELMAH 日志非常容易，但首先您将创建将在 ELMAH 日志中记录的未处理的异常。</span><span class="sxs-lookup"><span data-stu-id="8470b-318">Viewing the ELMAH log is easy, but first you will create an unhandled exception that will be recorded in the ELMAH log.</span></span>

1. <span data-ttu-id="8470b-319">按**CTRL + F5**运行 Wingtip Toys 示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="8470b-319">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>
2. <span data-ttu-id="8470b-320">若要写入的 ELMAH 日志未处理的异常，请导航到以下 URL （使用端口号） 在浏览器中：</span><span class="sxs-lookup"><span data-stu-id="8470b-320">To write an unhandled exception to the ELMAH log, navigate in your browser to the following URL (using your port number):</span></span>  
    <span data-ttu-id="8470b-321">`https://localhost:44300/NoPage.aspx` 将显示错误页。</span><span class="sxs-lookup"><span data-stu-id="8470b-321">`https://localhost:44300/NoPage.aspx` The error page will be displayed.</span></span>
3. <span data-ttu-id="8470b-322">若要显示的 ELMAH 日志，请导航到以下 URL （使用端口号） 在浏览器中：</span><span class="sxs-lookup"><span data-stu-id="8470b-322">To display the ELMAH log, navigate in your browser to the following URL (using your port number):</span></span>  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET 错误处理-ELMAH 错误日志](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a><span data-ttu-id="8470b-324">总结</span><span class="sxs-lookup"><span data-stu-id="8470b-324">Summary</span></span>

<span data-ttu-id="8470b-325">在本教程中，你已了解如何在应用程序级别、 页面级别中，而代码级别的错误处理。</span><span class="sxs-lookup"><span data-stu-id="8470b-325">In this tutorial, you have learned about handling errors at the application level, the page level, and the code level.</span></span> <span data-ttu-id="8470b-326">您还学习了如何记录处理和未经处理的错误，供以后查看。</span><span class="sxs-lookup"><span data-stu-id="8470b-326">You have also learned how to log handled and unhandled errors for later review.</span></span> <span data-ttu-id="8470b-327">您添加了 ELMAH 实用工具提供异常日志记录和使用 NuGet 的应用程序的通知。</span><span class="sxs-lookup"><span data-stu-id="8470b-327">You added the ELMAH utility to provide exception logging and notification to your application using NuGet.</span></span> <span data-ttu-id="8470b-328">此外，你已了解如何安全错误消息的重要性。</span><span class="sxs-lookup"><span data-stu-id="8470b-328">Additionally, you have learned about the importance of safe error messages.</span></span>

## <a name="tutorial-series-conclusion"></a><span data-ttu-id="8470b-329">系列教程结束</span><span class="sxs-lookup"><span data-stu-id="8470b-329">Tutorial Series Conclusion</span></span>

<span data-ttu-id="8470b-330">*感谢您的随笔。我希望本系列教程帮助您成为更熟悉 ASP.NET Web 窗体。如果你需要有关在 ASP.NET 4.5 和 Visual Studio 2013 中可用的 Web 窗体功能的详细信息，请参阅* [*ASP.NET 和 Web Tools for Visual Studio 2013 发行说明*](../../../../visual-studio/overview/2013/release-notes.md)*.此外，一定要看一看本教程中所述* ***后续步骤****部分和 defintely 试用* [*免费 Azure 试用版*](https://azure.microsoft.com/pricing/free-trial/)*.*</span><span class="sxs-lookup"><span data-stu-id="8470b-330">*Thanks for following along. I hope this set of tutorials helped you become more familiar with ASP.NET Web Forms. If you need more information about Web Forms features available in ASP.NET 4.5 and Visual Studio 2013, see* [*ASP.NET and Web Tools for Visual Studio 2013 Release Notes*](../../../../visual-studio/overview/2013/release-notes.md)*. Also, be sure to take a look at the tutorial mentioned in the* ***Next Steps****section and defintely try out the* [*free Azure trial*](https://azure.microsoft.com/pricing/free-trial/)*.*</span></span>

![谢谢-Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a><span data-ttu-id="8470b-332">后续步骤</span><span class="sxs-lookup"><span data-stu-id="8470b-332">Next Steps</span></span>

<span data-ttu-id="8470b-333">了解有关部署到 Microsoft Azure web 应用程序的详细信息，请参阅[将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET Web 窗体应用部署到 Azure 网站](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="8470b-333">Learn more about deploying your web application to Microsoft Azure, see [Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to an Azure Web Site](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/).</span></span>

## <a name="free-trial"></a><span data-ttu-id="8470b-334">免费试用版</span><span class="sxs-lookup"><span data-stu-id="8470b-334">Free Trial</span></span>

[<span data-ttu-id="8470b-335">Microsoft Azure-免费试用版</span><span class="sxs-lookup"><span data-stu-id="8470b-335">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)  
 <span data-ttu-id="8470b-336">你的网站发布到 Microsoft Azure 将节省时间、 维护和支出。</span><span class="sxs-lookup"><span data-stu-id="8470b-336">Publishing your website to Microsoft Azure will save you time, maintenance and expense.</span></span> <span data-ttu-id="8470b-337">它是一个到 web 应用部署到 Azure 的快速过程。</span><span class="sxs-lookup"><span data-stu-id="8470b-337">It's a quick process to deploying your web app to Azure.</span></span> <span data-ttu-id="8470b-338">当你需要进行维护和监视你的 web 应用时，Azure 提供了各种各样的工具和服务。</span><span class="sxs-lookup"><span data-stu-id="8470b-338">When you need to maintain and monitor your web app, Azure offers a variety of tools and services.</span></span> <span data-ttu-id="8470b-339">管理数据、 通讯、 标识、 备份、 消息传递、 媒体和在 Azure 中的性能。</span><span class="sxs-lookup"><span data-stu-id="8470b-339">Manage data, traffic, identity, backups, messaging, media and performance in Azure.</span></span> <span data-ttu-id="8470b-340">和所有这些都非常经济高效的方法中提供。</span><span class="sxs-lookup"><span data-stu-id="8470b-340">And, all of this is provided in a very cost effective approach.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8470b-341">其他资源</span><span class="sxs-lookup"><span data-stu-id="8470b-341">Additional Resources</span></span>

<span data-ttu-id="8470b-342">[ASP.NET 运行状况监视的日志记录错误详细信息](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md) </span><span class="sxs-lookup"><span data-stu-id="8470b-342">[Logging Error Details with ASP.NET Health Monitoring](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md) </span></span>  
[<span data-ttu-id="8470b-343">ELMAH</span><span class="sxs-lookup"><span data-stu-id="8470b-343">ELMAH</span></span>](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a><span data-ttu-id="8470b-344">致谢</span><span class="sxs-lookup"><span data-stu-id="8470b-344">Acknowledgements</span></span>

<span data-ttu-id="8470b-345">我想要感谢下列人员进行本系列教程的内容的重要贡献的人：</span><span class="sxs-lookup"><span data-stu-id="8470b-345">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="8470b-346">Alberto Poblacion、 MVP &amp; MCT、 西班牙</span><span class="sxs-lookup"><span data-stu-id="8470b-346">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="8470b-347">[Alex Thissen，荷兰](http://blog.alexthissen.nl/)(twitter: [ @alexthissen ](http://twitter.com/alexthissen))</span><span class="sxs-lookup"><span data-stu-id="8470b-347">[Alex Thissen, Netherlands](http://blog.alexthissen.nl/) (twitter: [@alexthissen](http://twitter.com/alexthissen))</span></span>
- [<span data-ttu-id="8470b-348">Andre Tournier，USA</span><span class="sxs-lookup"><span data-stu-id="8470b-348">Andre Tournier, USA</span></span>](http://andret503.wordpress.com/)
- <span data-ttu-id="8470b-349">Apurva Joshi Microsoft</span><span class="sxs-lookup"><span data-stu-id="8470b-349">Apurva Joshi, Microsoft</span></span>
- [<span data-ttu-id="8470b-350">Bojan Vrhovnik，斯洛文尼亚</span><span class="sxs-lookup"><span data-stu-id="8470b-350">Bojan Vrhovnik, Slovenia</span></span>](http://twitter.com/bvrhovnik)
- <span data-ttu-id="8470b-351">[Bruno Sonnino，巴西](http://msmvps.com/blogs/bsonnino)(twitter: [ @bsonnino ](http://twitter.com/bsonnino))</span><span class="sxs-lookup"><span data-stu-id="8470b-351">[Bruno Sonnino, Brazil](http://msmvps.com/blogs/bsonnino) (twitter: [@bsonnino](http://twitter.com/bsonnino))</span></span>
- [<span data-ttu-id="8470b-352">Carlos dos Santos 巴西</span><span class="sxs-lookup"><span data-stu-id="8470b-352">Carlos dos Santos, Brazil</span></span>](http://www.carloscds.net/)
- <span data-ttu-id="8470b-353">[Dave Campbell，USA](http://www.wynapse.com/) (twitter: [ @windowsdevnews ](http://twitter.com/windowsdevnews))</span><span class="sxs-lookup"><span data-stu-id="8470b-353">[Dave Campbell, USA](http://www.wynapse.com/) (twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))</span></span>
- <span data-ttu-id="8470b-354">[Jon Galloway、 Microsoft](https://weblogs.asp.net/jgalloway) (twitter: [ @jongalloway ](http://twitter.com/jongalloway))</span><span class="sxs-lookup"><span data-stu-id="8470b-354">[Jon Galloway, Microsoft](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- <span data-ttu-id="8470b-355">[Michael 音号，USA](http://www.930solutions.com/) (twitter: [ @mrsharps ](http://twitter.com/mrsharps))</span><span class="sxs-lookup"><span data-stu-id="8470b-355">[Michael Sharps, USA](http://www.930solutions.com/) (twitter: [@mrsharps](http://twitter.com/mrsharps))</span></span>
- <span data-ttu-id="8470b-356">Mike 教皇</span><span class="sxs-lookup"><span data-stu-id="8470b-356">Mike Pope</span></span>
- <span data-ttu-id="8470b-357">[Mitchel 卖家，USA](http://www.mitchelsellers.com/) (twitter: [ @MitchelSellers ](http://twitter.com/MitchelSellers))</span><span class="sxs-lookup"><span data-stu-id="8470b-357">[Mitchel Sellers, USA](http://www.mitchelsellers.com/) (twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))</span></span>
- [<span data-ttu-id="8470b-358">Paul Cociuba Microsoft</span><span class="sxs-lookup"><span data-stu-id="8470b-358">Paul Cociuba, Microsoft</span></span>](http://linqto.me/Links/pcociuba)
- [<span data-ttu-id="8470b-359">Paulo Morgado 葡萄牙</span><span class="sxs-lookup"><span data-stu-id="8470b-359">Paulo Morgado, Portugal</span></span>](http://paulomorgado.net/)
- [<span data-ttu-id="8470b-360">Pranav rastogi 撰写 Microsoft</span><span class="sxs-lookup"><span data-stu-id="8470b-360">Pranav Rastogi, Microsoft</span></span>](https://blogs.msdn.com/b/pranav_rastogi)
- [<span data-ttu-id="8470b-361">Tim Ammann Microsoft</span><span class="sxs-lookup"><span data-stu-id="8470b-361">Tim Ammann, Microsoft</span></span>](https://blogs.iis.net/timamm/default.aspx)
- [<span data-ttu-id="8470b-362">Tom Dykstra Microsoft</span><span class="sxs-lookup"><span data-stu-id="8470b-362">Tom Dykstra, Microsoft</span></span>](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a><span data-ttu-id="8470b-363">社区贡献</span><span class="sxs-lookup"><span data-stu-id="8470b-363">Community Contributions</span></span>

- <span data-ttu-id="8470b-364">Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))</span><span class="sxs-lookup"><span data-stu-id="8470b-364">Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))</span></span>  
  <span data-ttu-id="8470b-365">Visual Studio 2012 相关 MSDN 上的代码示例：[导航 Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)</span><span class="sxs-lookup"><span data-stu-id="8470b-365">Visual Studio 2012 related code sample on MSDN: [Navigation Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)</span></span>
- <span data-ttu-id="8470b-366">James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))</span><span class="sxs-lookup"><span data-stu-id="8470b-366">James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))</span></span>  
  <span data-ttu-id="8470b-367">Visual Studio 2012 相关 MSDN 上的代码示例：[在 Visual Basic 中的 ASP.NET 4.5 Web 窗体教程系列](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)</span><span class="sxs-lookup"><span data-stu-id="8470b-367">Visual Studio 2012 related code sample on MSDN: [ASP.NET 4.5 Web Forms Tutorial Series in Visual Basic](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)</span></span>
- <span data-ttu-id="8470b-368">Andrielle Azevedo-Microsoft 技术受众参与者 (twitter: @driazevedo)</span><span class="sxs-lookup"><span data-stu-id="8470b-368">Andrielle Azevedo - Microsoft Technical Audience Contributor (twitter: @driazevedo)</span></span>  
  <span data-ttu-id="8470b-369">Visual Studio 2012 翻译： [Iniciando com Visão Geral 的 ASP.NET Web 窗体 4.5-Parte 1-Introdução e](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)</span><span class="sxs-lookup"><span data-stu-id="8470b-369">Visual Studio 2012 translation: [Iniciando com ASP.NET Web Forms 4.5 - Parte 1 - Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8470b-370">上一篇</span><span class="sxs-lookup"><span data-stu-id="8470b-370">Previous</span></span>](url-routing.md)
