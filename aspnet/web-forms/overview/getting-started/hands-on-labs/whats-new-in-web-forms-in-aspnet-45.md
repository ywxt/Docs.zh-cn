---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: 在 ASP.NET 4.5 中新增 Web 窗体 |Microsoft Docs
author: rick-anderson
description: ASP.NET Web 窗体的新版本引入了大量专注于处理数据时改善用户体验的改进。 在以前版本的...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 4e8c8f303851b7f1a01744cab58e27a9b37127a6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389226"
---
<a name="whats-new-in-web-forms-in-aspnet-45"></a><span data-ttu-id="f3d93-104">什么是在 ASP.NET 4.5 Web 窗体中的新增功能</span><span class="sxs-lookup"><span data-stu-id="f3d93-104">What's New in Web Forms in ASP.NET 4.5</span></span>
====================
<span data-ttu-id="f3d93-105">通过[Web 训练营团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="f3d93-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="f3d93-106">ASP.NET Web 窗体的新版本引入了大量专注于处理数据时改善用户体验的改进。</span><span class="sxs-lookup"><span data-stu-id="f3d93-106">The new version of ASP.NET Web Forms introduces a number of improvements focused on improving user experience when working with data.</span></span>
> 
> <span data-ttu-id="f3d93-107">在以前版本的 Web 窗体，使用数据绑定发出对象成员的值时，您可以使用数据绑定表达式的 bind （） 或 eval （）。</span><span class="sxs-lookup"><span data-stu-id="f3d93-107">In previous versions of Web Forms, when using data-binding to emit the value of an object member, you used the data-binding expressions Bind() or Eval().</span></span> <span data-ttu-id="f3d93-108">在新的 ASP.NET 版本中，您就能够声明一个控件要通过使用新的 ItemType 属性绑定到的数据类型。</span><span class="sxs-lookup"><span data-stu-id="f3d93-108">In the new version of ASP.NET, you are able to declare what type of data a control is going to be bound to by using a new ItemType property.</span></span> <span data-ttu-id="f3d93-109">设置此属性以便可以使用强类型化变量来接收 Visual Studio 开发体验，如 IntelliSense、 成员导航和编译时检查的全部益处。</span><span class="sxs-lookup"><span data-stu-id="f3d93-109">Setting this property will enable you to use a strongly-typed variable to receive the full benefits of the Visual Studio development experience, such as IntelliSense, member navigation, and compile-time checking.</span></span>
> 
> <span data-ttu-id="f3d93-110">数据绑定控件中，现在还可以指定你自己自定义的方法，用于选择、 更新、 删除和插入数据，从而简化页面控件和应用程序逻辑之间的交互。</span><span class="sxs-lookup"><span data-stu-id="f3d93-110">With the data-bound controls, you can now also specify your own custom methods for selecting, updating, deleting and inserting data, simplifying the interaction between the page controls and your application logic.</span></span> <span data-ttu-id="f3d93-111">另外，模型绑定功能已被添加到 ASP.NET 中，这意味着您可以从页的数据直接映射到方法类型参数。</span><span class="sxs-lookup"><span data-stu-id="f3d93-111">Additionally, model binding capabilities have been added to ASP.NET, which means you can map data from the page directly into method type parameters.</span></span>
> 
> <span data-ttu-id="f3d93-112">验证用户输入还应简化了 Web 窗体的最新版本。</span><span class="sxs-lookup"><span data-stu-id="f3d93-112">Validating user input should also be easier with the latest version of Web Forms.</span></span> <span data-ttu-id="f3d93-113">现在，你可以批注与从验证特性在模型类**System.ComponentModel.DataAnnotations**命名空间和所有站点都控制的请求验证用户输入使用该信息。</span><span class="sxs-lookup"><span data-stu-id="f3d93-113">You can now annotate your model classes with validation attributes from the **System.ComponentModel.DataAnnotations** namespace and request that all your site controls validate user input using that information.</span></span> <span data-ttu-id="f3d93-114">在 Web 窗体中的客户端验证现与 jQuery，提供清理器客户端代码和非介入式 JavaScript 功能集成。</span><span class="sxs-lookup"><span data-stu-id="f3d93-114">Client-side validation in Web Forms is now integrated with jQuery, providing cleaner client-side code and unobtrusive JavaScript features.</span></span>
> 
> <span data-ttu-id="f3d93-115">在请求验证区域中，已得到改进以方便您来有选择地关闭应用程序的特定部分的请求验证或读取未经验证的请求数据。</span><span class="sxs-lookup"><span data-stu-id="f3d93-115">In the request validation area, improvements have been made to make it easier to selectively turn off request validation for specific parts of your applications or read invalidated request data.</span></span>
> 
> <span data-ttu-id="f3d93-116">某些已得到改进 Web 窗体服务器控件能够充分利用 HTML5 的新功能：</span><span class="sxs-lookup"><span data-stu-id="f3d93-116">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>
> 
> - <span data-ttu-id="f3d93-117">TextBox 控件将 TextMode 属性已更新以支持电子邮件、 datetime 等新的 HTML5 输入的类型。</span><span class="sxs-lookup"><span data-stu-id="f3d93-117">The TextMode property of the TextBox control has been updated to support the new HTML5 input types like email, datetime, and so on.</span></span>
> - <span data-ttu-id="f3d93-118">FileUpload 控件现在支持从支持此 HTML5 功能的浏览器上传多个文件。</span><span class="sxs-lookup"><span data-stu-id="f3d93-118">The FileUpload control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
> - <span data-ttu-id="f3d93-119">验证程序控件现在支持验证 HTML5 输入的元素。</span><span class="sxs-lookup"><span data-stu-id="f3d93-119">Validator controls now support validating HTML5 input elements.</span></span>
> - <span data-ttu-id="f3d93-120">了现在表示 URL 的属性的新 HTML5 元素支持 runat =&quot;server&quot;。</span><span class="sxs-lookup"><span data-stu-id="f3d93-120">New HTML5 elements that have attributes that represent a URL now support runat=&quot;server&quot;.</span></span> <span data-ttu-id="f3d93-121">因此，您可以使用 ASP.NET 约定中 URL 路径，如 ~ 运算符来表示应用程序根目录 (例如，&lt;视频 runat =&quot;服务器&quot;src =&quot;~/myVideo.wmv&quot; &gt; &lt;/视频&gt;)。</span><span class="sxs-lookup"><span data-stu-id="f3d93-121">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat=&quot;server&quot; src=&quot;~/myVideo.wmv&quot;&gt;&lt;/video&gt;).</span></span>
> - <span data-ttu-id="f3d93-122">已修复的 UpdatePanel 控件，以便支持发布 HTML5 输入的字段。</span><span class="sxs-lookup"><span data-stu-id="f3d93-122">The UpdatePanel control has been fixed to support posting HTML5 input fields.</span></span>
> 
> <span data-ttu-id="f3d93-123">官方 ASP.NET 门户中可以找到 ASP.NET WebForms 4.5 中的新功能的更多示例： [What's New in ASP.NET 4.5 和 Visual Studio 2012](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)</span><span class="sxs-lookup"><span data-stu-id="f3d93-123">In the official ASP.NET portal you can find more examples of the new features in ASP.NET WebForms 4.5: [What's New in ASP.NET 4.5 and Visual Studio 2012](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)</span></span>
> 
> <span data-ttu-id="f3d93-124">在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="f3d93-124">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>


<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="f3d93-125">目标</span><span class="sxs-lookup"><span data-stu-id="f3d93-125">Objectives</span></span>

<span data-ttu-id="f3d93-126">在本动手实验，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="f3d93-126">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="f3d93-127">使用强类型化数据绑定表达式</span><span class="sxs-lookup"><span data-stu-id="f3d93-127">Use strongly-typed data-binding expressions</span></span>
- <span data-ttu-id="f3d93-128">在 Web 窗体中使用新的模型绑定功能</span><span class="sxs-lookup"><span data-stu-id="f3d93-128">Use new model binding features in Web Forms</span></span>
- <span data-ttu-id="f3d93-129">将值提供程序用于将页面数据映射到代码隐藏方法</span><span class="sxs-lookup"><span data-stu-id="f3d93-129">Use value providers for mapping page data to code-behind methods</span></span>
- <span data-ttu-id="f3d93-130">用户输入验证中使用数据注释</span><span class="sxs-lookup"><span data-stu-id="f3d93-130">Use Data Annotations for user input validation</span></span>
- <span data-ttu-id="f3d93-131">在 Web 窗体中执行 advange unobstrusive 使用 jQuery 的客户端验证</span><span class="sxs-lookup"><span data-stu-id="f3d93-131">Take advange of unobstrusive client-side validation with jQuery in Web Forms</span></span>
- <span data-ttu-id="f3d93-132">实现粒度请求验证</span><span class="sxs-lookup"><span data-stu-id="f3d93-132">Implement granular request validation</span></span>
- <span data-ttu-id="f3d93-133">实现在 Web 窗体中处理的异步页面</span><span class="sxs-lookup"><span data-stu-id="f3d93-133">Implement asynchronous page processing in Web Forms</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="f3d93-134">系统必备</span><span class="sxs-lookup"><span data-stu-id="f3d93-134">Prerequisites</span></span>

<span data-ttu-id="f3d93-135">必须具有要完成本实验的以下项：</span><span class="sxs-lookup"><span data-stu-id="f3d93-135">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="f3d93-136">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="f3d93-136">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="f3d93-137">安装</span><span class="sxs-lookup"><span data-stu-id="f3d93-137">Setup</span></span>

<span data-ttu-id="f3d93-138">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="f3d93-138">**Installing Code Snippets**</span></span>

<span data-ttu-id="f3d93-139">为方便起见，您将沿此实验室管理大部分是代码的可用作 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="f3d93-139">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="f3d93-140">若要安装运行的代码段 **.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="f3d93-140">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="f3d93-141">如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 c： 使用代码片段](#AppendixC)&quot;。</span><span class="sxs-lookup"><span data-stu-id="f3d93-141">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="f3d93-142">练习</span><span class="sxs-lookup"><span data-stu-id="f3d93-142">Exercises</span></span>

<span data-ttu-id="f3d93-143">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="f3d93-143">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="f3d93-144">练习 1： 模型绑定在 ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="f3d93-144">Exercise 1: Model Binding in ASP.NET Web Forms</span></span>](#Exercise1)
2. [<span data-ttu-id="f3d93-145">练习 2： 数据验证</span><span class="sxs-lookup"><span data-stu-id="f3d93-145">Exercise 2: Data Validation</span></span>](#Exercise2)
3. [<span data-ttu-id="f3d93-146">练习 3： 异步页处理在 ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="f3d93-146">Exercise 3: Asynchronous Page Processing in ASP.NET Web Forms</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="f3d93-147">每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="f3d93-147">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="f3d93-148">如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="f3d93-148">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="f3d93-149">估计的时间才能完成此实验： **60 分钟**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-149">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a><span data-ttu-id="f3d93-150">练习 1： 模型绑定在 ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="f3d93-150">Exercise 1: Model Binding in ASP.NET Web Forms</span></span>

<span data-ttu-id="f3d93-151">ASP.NET Web 窗体的新版本引入了一些侧重于改进体验，使用数据时的增强功能。</span><span class="sxs-lookup"><span data-stu-id="f3d93-151">The new version of ASP.NET Web Forms introduces a number of enhancements focused on improving the experience when working with data.</span></span> <span data-ttu-id="f3d93-152">在本练习中，将了解强类型化数据控件和模型绑定。</span><span class="sxs-lookup"><span data-stu-id="f3d93-152">Throughout this exercise, you will learn about strongly typed data-controls and model binding.</span></span>

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a><span data-ttu-id="f3d93-153">任务 1-使用强类型化的数据绑定</span><span class="sxs-lookup"><span data-stu-id="f3d93-153">Task 1 - Using Strongly-Typed Data-Bindings</span></span>

<span data-ttu-id="f3d93-154">在此任务中，您将发现的新强类型绑定 ASP.NET 4.5 中提供。</span><span class="sxs-lookup"><span data-stu-id="f3d93-154">In this task, you will discover the new strongly-typed bindings available in ASP.NET 4.5.</span></span>

1. <span data-ttu-id="f3d93-155">打开**开始**解决方案位于**源/Ex1-ModelBinding/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="f3d93-155">Open the **Begin** solution located at **Source/Ex1-ModelBinding/Begin/** folder.</span></span>

   1. <span data-ttu-id="f3d93-156">需要先下载某些缺少的 NuGet 包然后再继续。</span><span class="sxs-lookup"><span data-stu-id="f3d93-156">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f3d93-157">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-157">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f3d93-158">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="f3d93-158">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f3d93-159">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-159">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f3d93-160">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="f3d93-160">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f3d93-161">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="f3d93-161">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f3d93-162">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="f3d93-162">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f3d93-163">打开**Customers.aspx**页。</span><span class="sxs-lookup"><span data-stu-id="f3d93-163">Open the **Customers.aspx** page.</span></span> <span data-ttu-id="f3d93-164">置于主控件没有编号的列表，包括用于列出每个客户一个 repeater 控件。</span><span class="sxs-lookup"><span data-stu-id="f3d93-164">Place an unnumbered list in the main control and include a repeater control inside for listing each customer.</span></span> <span data-ttu-id="f3d93-165">Repeater 名称设置为**customersRepeater**如下面的代码中所示。</span><span class="sxs-lookup"><span data-stu-id="f3d93-165">Set the repeater name to **customersRepeater** as shown in the following code.</span></span>

    <span data-ttu-id="f3d93-166">在以前版本的 Web 窗体，如果使用数据绑定发出对象成员的值是数据绑定，您将使用数据绑定表达式，以及调用 Eval 方法，传递该成员的名称作为字符串。</span><span class="sxs-lookup"><span data-stu-id="f3d93-166">In previous versions of Web Forms, when using data-binding to emit the value of a member on an object you're data-binding to, you would use a data-binding expression, along with a call to the Eval method, passing in the name of the member as a string.</span></span>

    <span data-ttu-id="f3d93-167">在运行时，对 Eval 的这些调用将使用针对当前绑定对象的反射来读取的具有给定名称的成员的值和 html 格式显示结果。</span><span class="sxs-lookup"><span data-stu-id="f3d93-167">At runtime, these calls to Eval will use reflection against the currently bound object to read the value of the member with the given name, and display the result in the HTML.</span></span> <span data-ttu-id="f3d93-168">此方法可以非常轻松地针对任意、 unshaped 数据进行数据绑定。</span><span class="sxs-lookup"><span data-stu-id="f3d93-168">This approach makes it very easy to data-bind against arbitrary, unshaped data.</span></span>

    <span data-ttu-id="f3d93-169">遗憾的是，您会丢失的许多出色的开发时间体验在 Visual Studio 中，对成员名称、 对导航 （例如，请转到定义），和编译时检查的支持包括 IntelliSense 功能。</span><span class="sxs-lookup"><span data-stu-id="f3d93-169">Unfortunately, you lose many of the great development-time experience features in Visual Studio, including IntelliSense for member names, support for navigation (like Go To Definition), and compile-time checking.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. <span data-ttu-id="f3d93-170">打开**Customers.aspx.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="f3d93-170">Open the **Customers.aspx.cs** file.</span></span>
4. <span data-ttu-id="f3d93-171">添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="f3d93-171">Add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. <span data-ttu-id="f3d93-172">在中**页上\_负载**方法中，添加代码以填充客户列表使用 repeater。</span><span class="sxs-lookup"><span data-stu-id="f3d93-172">In the **Page\_Load** method, add code to populate the repeater with the list of customers.</span></span>

    <span data-ttu-id="f3d93-173">(代码段- *Web 窗体实验-Ex01-绑定的客户数据源*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-173">(Code Snippet - *Web Forms Lab - Ex01 - Bind Customers Data Source*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    <span data-ttu-id="f3d93-174">该解决方案使用 EntityFramework CodeFirst 以及创建和访问数据库。</span><span class="sxs-lookup"><span data-stu-id="f3d93-174">The solution uses EntityFramework together with CodeFirst to create and access the database.</span></span> <span data-ttu-id="f3d93-175">在下面的代码，customersRepeater 已绑定到从数据库中返回的所有客户实例化查询。</span><span class="sxs-lookup"><span data-stu-id="f3d93-175">In the following code, the customersRepeater is bound to a materialized query that returns all the customers from the database.</span></span>
6. <span data-ttu-id="f3d93-176">按**F5**若要运行解决方案并转到**客户**页以查看操作中的 repeater。</span><span class="sxs-lookup"><span data-stu-id="f3d93-176">Press **F5** to run the solution and go to the **Customers** page to see the repeater in action.</span></span> <span data-ttu-id="f3d93-177">因为该解决方案使用 CodeFirst，将创建并运行应用程序时，在本地 SQL Express 实例中填充数据库。</span><span class="sxs-lookup"><span data-stu-id="f3d93-177">As the solution is using CodeFirst, the database will be created and populated in your local SQL Express instance when running the application.</span></span>

    <span data-ttu-id="f3d93-178">![列出的客户可以 repeater](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "列出的客户可以 repeater")</span><span class="sxs-lookup"><span data-stu-id="f3d93-178">![Listing the customers with a repeater](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "Listing the customers with a repeater")</span></span>

    <span data-ttu-id="f3d93-179">*列出的客户可以 repeater*</span><span class="sxs-lookup"><span data-stu-id="f3d93-179">*Listing the customers with a repeater*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d93-180">在 Visual Studio 2012 中，IIS Express 是默认的 Web 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="f3d93-180">In Visual Studio 2012, IIS Express is the default Web development server.</span></span>
7. <span data-ttu-id="f3d93-181">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f3d93-181">Close the browser and go back to Visual Studio.</span></span>
8. <span data-ttu-id="f3d93-182">现在将为要使用强类型化的绑定的实现。</span><span class="sxs-lookup"><span data-stu-id="f3d93-182">Now replace the implementation to use strongly typed bindings.</span></span> <span data-ttu-id="f3d93-183">打开**Customers.aspx**页上，并使用新**ItemType**中继器设置中的属性**客户**类型作为绑定类型。</span><span class="sxs-lookup"><span data-stu-id="f3d93-183">Open the **Customers.aspx** page and use the new **ItemType** attribute in the repeater to set the **Customer** type as the binding type.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    <span data-ttu-id="f3d93-184">ItemType 属性，可声明哪些类型的数据控件将绑定到和允许您使用强类型绑定的数据绑定控件内。</span><span class="sxs-lookup"><span data-stu-id="f3d93-184">The ItemType property enables you to declare which type of data the control is going to be bound to and allows you to use strongly-typed binding inside the data-bound control.</span></span>
9. <span data-ttu-id="f3d93-185">将为 ItemTemplate 内容与下面的代码。</span><span class="sxs-lookup"><span data-stu-id="f3d93-185">Replace the ItemTemplate content with the following code.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    <span data-ttu-id="f3d93-186">与上述方法的一个缺点是对 eval （） 和 bind （） 的调用是后期绑定-这意味着传递字符串来表示属性名称。</span><span class="sxs-lookup"><span data-stu-id="f3d93-186">One downside with the above approaches is that the calls to Eval() and Bind() are late-bound - meaning you pass strings to represent the property names.</span></span> <span data-ttu-id="f3d93-187">这意味着您不能为成员名称也支持代码导航 （例如，请转到定义），不编译时检查支持使用 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="f3d93-187">This means you don't get Intellisense for the member names, support for code navigation (like Go To Definition), nor compile-time checking support.</span></span>

    <span data-ttu-id="f3d93-188">设置 ItemType 属性会导致两个新类型化的变量，在数据绑定表达式的作用域中生成：**项**并**BindItem**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-188">Setting the ItemType property causes two new typed variables to be generated in the scope of the data-binding expressions: **Item** and **BindItem**.</span></span> <span data-ttu-id="f3d93-189">可以在数据绑定表达式中使用这些强类型化的变量，并获取 Visual Studio 开发体验的全部益处。</span><span class="sxs-lookup"><span data-stu-id="f3d93-189">You can use these strongly typed variables in the data-binding expressions and get the full benefits of the Visual Studio development experience.</span></span>

    <span data-ttu-id="f3d93-190">&quot; **:** &quot;表达式中使用将自动进行 HTML 编码的输出以避免出现安全问题 （例如，跨站点脚本攻击）。</span><span class="sxs-lookup"><span data-stu-id="f3d93-190">The &quot;**:** &quot; used in the expression will automatically HTML-encode the output to avoid security issues (for example, cross-site scripting attacks).</span></span> <span data-ttu-id="f3d93-191">此表示法是自.NET 4 响应编写，但现在也会出现在数据绑定表达式。</span><span class="sxs-lookup"><span data-stu-id="f3d93-191">This notation was available since .NET 4 for response writing, but now is also available in data-binding expressions.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d93-192">项成员适用于单向绑定。</span><span class="sxs-lookup"><span data-stu-id="f3d93-192">The Item member works for one-way binding.</span></span> <span data-ttu-id="f3d93-193">如果你想要执行的双向绑定使用**BindItem**成员。</span><span class="sxs-lookup"><span data-stu-id="f3d93-193">If you want to perform two-way binding use the **BindItem** member.</span></span>

    <span data-ttu-id="f3d93-194">![中强类型绑定的 IntelliSense 支持](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "强类型化绑定中的 IntelliSense 支持")</span><span class="sxs-lookup"><span data-stu-id="f3d93-194">![IntelliSense support in strongly-typed binding](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "IntelliSense support in strongly-typed binding")</span></span>

    <span data-ttu-id="f3d93-195">*中强类型绑定的 IntelliSense 支持*</span><span class="sxs-lookup"><span data-stu-id="f3d93-195">*IntelliSense support in strongly-typed binding*</span></span>
10. <span data-ttu-id="f3d93-196">按**F5**若要运行解决方案，并转到客户页以确保按预期方式工作所做的更改。</span><span class="sxs-lookup"><span data-stu-id="f3d93-196">Press **F5** to run the solution and go to the Customers page to make sure the changes work as expected.</span></span>

    <span data-ttu-id="f3d93-197">![列出客户详细信息](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "列出客户详细信息")</span><span class="sxs-lookup"><span data-stu-id="f3d93-197">![Listing customer details](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "Listing customer details")</span></span>

    <span data-ttu-id="f3d93-198">*列出客户详细信息*</span><span class="sxs-lookup"><span data-stu-id="f3d93-198">*Listing customer details*</span></span>
11. <span data-ttu-id="f3d93-199">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f3d93-199">Close the browser and go back to Visual Studio.</span></span>

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a><span data-ttu-id="f3d93-200">任务 2-引入模型绑定在 Web 窗体</span><span class="sxs-lookup"><span data-stu-id="f3d93-200">Task 2 - Introducing Model Binding in Web Forms</span></span>

<span data-ttu-id="f3d93-201">在以前版本的 ASP.NET Web 窗体中，当您希望执行双向数据绑定，同时检索和更新数据，您需要使用数据源对象。</span><span class="sxs-lookup"><span data-stu-id="f3d93-201">In previous versions of ASP.NET Web Forms, when you wanted to perform two-way data-binding, both retrieving and updating data, you needed to use a Data Source object.</span></span> <span data-ttu-id="f3d93-202">这可能对象数据源、 SQL 数据源、 LINQ 数据源，等等。</span><span class="sxs-lookup"><span data-stu-id="f3d93-202">This could be an Object Data Source, a SQL Data Source, a LINQ Data Source and so on.</span></span> <span data-ttu-id="f3d93-203">但是如果你的方案所需的处理数据的自定义代码，您需要使用对象数据源，并且这将一些缺点。</span><span class="sxs-lookup"><span data-stu-id="f3d93-203">However if your scenario required custom code for handling the data, you needed to use the Object Data Source and this brought some drawbacks.</span></span> <span data-ttu-id="f3d93-204">例如，您需要避免使用复杂类型和您所需执行的验证逻辑时处理的异常。</span><span class="sxs-lookup"><span data-stu-id="f3d93-204">For example, you needed to avoid complex types and you needed to handle exceptions when executing validation logic.</span></span>

<span data-ttu-id="f3d93-205">在新版本的 ASP.NET Web 窗体数据绑定控件支持模型绑定。</span><span class="sxs-lookup"><span data-stu-id="f3d93-205">In the new version of ASP.NET Web Forms the data-bound controls support model binding.</span></span> <span data-ttu-id="f3d93-206">这意味着，您可以指定选择、 更新、 插入和删除要从代码隐藏文件或从另一个类调用逻辑的数据绑定控件中直接的方法。</span><span class="sxs-lookup"><span data-stu-id="f3d93-206">This means that you can specify select, update, insert and delete methods directly in the data-bound control to call logic from your code-behind file or from another class.</span></span>

<span data-ttu-id="f3d93-207">若要了解相关信息，您将使用 GridView 列出使用新的产品类别**SelectMethod**属性。</span><span class="sxs-lookup"><span data-stu-id="f3d93-207">To learn about this, you will use a GridView to list the product categories using the new **SelectMethod** attribute.</span></span> <span data-ttu-id="f3d93-208">此属性，可指定进行检索的 GridView 数据的方法。</span><span class="sxs-lookup"><span data-stu-id="f3d93-208">This attribute enables you to specify a method for retrieving the GridView data.</span></span>

1. <span data-ttu-id="f3d93-209">打开**Products.aspx**页上，包括**GridView**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-209">Open the **Products.aspx** page and include a **GridView**.</span></span> <span data-ttu-id="f3d93-210">若要使用强类型绑定，并启用排序和分页如下所示配置 GridView。</span><span class="sxs-lookup"><span data-stu-id="f3d93-210">Configure the GridView as shown below to use strongly-typed bindings and enable sorting and paging.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. <span data-ttu-id="f3d93-211">使用新**SelectMethod**属性可配置 GridView 调用**GetCategories**方法来选择的数据。</span><span class="sxs-lookup"><span data-stu-id="f3d93-211">Use the new **SelectMethod** attribute to configure the GridView to call a **GetCategories** method to select the data.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. <span data-ttu-id="f3d93-212">打开**Products.aspx.cs**代码隐藏文件，并添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="f3d93-212">Open the **Products.aspx.cs** code-behind file and add the following using statements.</span></span>

    <span data-ttu-id="f3d93-213">(代码段- *Web 窗体实验-Ex01-命名空间*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-213">(Code Snippet - *Web Forms Lab - Ex01 - Namespaces*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. <span data-ttu-id="f3d93-214">添加中的私有成员**产品**类，将分配的新实例**ProductsContext**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-214">Add a private member in the **Products** class and assign a new instance of **ProductsContext**.</span></span> <span data-ttu-id="f3d93-215">此属性将存储实体框架数据上下文，可用于连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="f3d93-215">This property will store the Entity Framework data context that enables you to connect to the database.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. <span data-ttu-id="f3d93-216">创建**GetCategories**方法来检索使用 LINQ 的类别的列表。</span><span class="sxs-lookup"><span data-stu-id="f3d93-216">Create a **GetCategories** method to retrieve the list of categories using LINQ.</span></span> <span data-ttu-id="f3d93-217">该查询将包括**产品**属性，以便 GridView 可以显示的每个类别的产品数量。</span><span class="sxs-lookup"><span data-stu-id="f3d93-217">The query will include the **Products** property so the GridView can show the amount of products for each category.</span></span> <span data-ttu-id="f3d93-218">请注意，该方法返回原始的 IQueryable 对象，表示查询的更高版本上执行的页面生命周期。</span><span class="sxs-lookup"><span data-stu-id="f3d93-218">Notice that the method returns a raw IQueryable object that represent the query to be executed later on the page lifecycle.</span></span>

    <span data-ttu-id="f3d93-219">(代码段- *Web 窗体实验-Ex01-GetCategories*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-219">(Code Snippet - *Web Forms Lab - Ex01 - GetCategories*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > <span data-ttu-id="f3d93-220">在以前版本的 ASP.NET Web 窗体，启用排序和分页使用您自己的存储库逻辑在数据源对象上下文中，需编写自定义代码和接收所需的所有参数。</span><span class="sxs-lookup"><span data-stu-id="f3d93-220">In previous versions of ASP.NET Web Forms, enabling sorting and paging using your own repository logic within an Object Data Source context, required to write your own custom code and receive all the necessary parameters.</span></span> <span data-ttu-id="f3d93-221">现在，如数据绑定方法可以返回 IQueryable，这表示查询仍要在执行，ASP.NET 可以修改查询以添加适当的排序和分页参数的处理。</span><span class="sxs-lookup"><span data-stu-id="f3d93-221">Now, as the data-binding methods can return IQueryable and this represents a query still to be executed, ASP.NET can take care of modifying the query to add the proper sorting and paging parameters.</span></span>
6. <span data-ttu-id="f3d93-222">按**F5**可开始调试网站并转到产品页。</span><span class="sxs-lookup"><span data-stu-id="f3d93-222">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="f3d93-223">你应看到 GridView 中填充了 GetCategories 方法返回的类别。</span><span class="sxs-lookup"><span data-stu-id="f3d93-223">You should see that the GridView is populated with the categories returned by the GetCategories method.</span></span>

    <span data-ttu-id="f3d93-224">![填充 GridView 使用模型绑定](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "填充 GridView 使用模型绑定")</span><span class="sxs-lookup"><span data-stu-id="f3d93-224">![Populating a GridView using model binding](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "Populating a GridView using model binding")</span></span>

    <span data-ttu-id="f3d93-225">*填充 GridView 使用模型绑定*</span><span class="sxs-lookup"><span data-stu-id="f3d93-225">*Populating a GridView using model binding*</span></span>
7. <span data-ttu-id="f3d93-226">按**SHIFT**+**F5**停止调试。</span><span class="sxs-lookup"><span data-stu-id="f3d93-226">Press **SHIFT**+**F5** Stop debugging.</span></span>

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a><span data-ttu-id="f3d93-227">任务 3-在模型绑定中的值提供程序</span><span class="sxs-lookup"><span data-stu-id="f3d93-227">Task 3 - Value Providers in Model Binding</span></span>

<span data-ttu-id="f3d93-228">模型绑定不仅可用于指定自定义方法以使用直接在数据绑定控件中，数据还可以将数据从页映射到从这些方法的参数。</span><span class="sxs-lookup"><span data-stu-id="f3d93-228">Model binding not only enables you to specify custom methods to work with your data directly in the data-bound control, but also allows you to map data from the page into parameters from these methods.</span></span> <span data-ttu-id="f3d93-229">在方法参数，可以使用值提供程序属性指定值的数据源。</span><span class="sxs-lookup"><span data-stu-id="f3d93-229">On the method parameter, you can use value provider attributes to specify the value's data source.</span></span> <span data-ttu-id="f3d93-230">例如：</span><span class="sxs-lookup"><span data-stu-id="f3d93-230">For example:</span></span>

- <span data-ttu-id="f3d93-231">在页上的控件</span><span class="sxs-lookup"><span data-stu-id="f3d93-231">Controls on the page</span></span>
- <span data-ttu-id="f3d93-232">查询字符串值</span><span class="sxs-lookup"><span data-stu-id="f3d93-232">Query string values</span></span>
- <span data-ttu-id="f3d93-233">查看数据</span><span class="sxs-lookup"><span data-stu-id="f3d93-233">View data</span></span>
- <span data-ttu-id="f3d93-234">会话状态</span><span class="sxs-lookup"><span data-stu-id="f3d93-234">Session state</span></span>
- <span data-ttu-id="f3d93-235">Cookie</span><span class="sxs-lookup"><span data-stu-id="f3d93-235">Cookies</span></span>
- <span data-ttu-id="f3d93-236">已发布的表单数据</span><span class="sxs-lookup"><span data-stu-id="f3d93-236">Posted form data</span></span>
- <span data-ttu-id="f3d93-237">视图状态</span><span class="sxs-lookup"><span data-stu-id="f3d93-237">View state</span></span>
- <span data-ttu-id="f3d93-238">也支持自定义值提供程序</span><span class="sxs-lookup"><span data-stu-id="f3d93-238">Custom value providers are supported as well</span></span>

<span data-ttu-id="f3d93-239">如果您使用过 ASP.NET MVC 4，您会注意到是类似的模型绑定支持。</span><span class="sxs-lookup"><span data-stu-id="f3d93-239">If you have used ASP.NET MVC 4, you will notice the model binding support is similar.</span></span> <span data-ttu-id="f3d93-240">实际上，这些功能是从 ASP.NET MVC 和移动到**System.Web**要再也在 Web 窗体上使用这些程序集。</span><span class="sxs-lookup"><span data-stu-id="f3d93-240">Indeed, these features were taken from ASP.NET MVC and moved into the **System.Web** assembly to be able to use them on Web Forms as well.</span></span>

<span data-ttu-id="f3d93-241">在此任务中，你将更新 GridView，其中的每个类别的产品量筛选其结果与模型绑定接收筛选器参数。</span><span class="sxs-lookup"><span data-stu-id="f3d93-241">In this task, you will update the GridView to filter its results by the amount of products for each category, receiving the filter parameter with model binding.</span></span>

1. <span data-ttu-id="f3d93-242">返回到**Products.aspx**页。</span><span class="sxs-lookup"><span data-stu-id="f3d93-242">Go back to the **Products.aspx** page.</span></span>
2. <span data-ttu-id="f3d93-243">在 GridView 的顶部，添加**标签**和一个**组合框**若要选择的每个类别的产品数量，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f3d93-243">At the top of the GridView, add a **Label** and a **ComboBox** to select the number of products for each category as shown below.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. <span data-ttu-id="f3d93-244">添加**要**到 GridView，其中包含所选的产品数量的任何类别时显示一条消息。</span><span class="sxs-lookup"><span data-stu-id="f3d93-244">Add an **EmptyDataTemplate** to the GridView to show a message when there are no categories with the selected number of products.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. <span data-ttu-id="f3d93-245">打开**Products.aspx.cs**隐藏代码，并添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="f3d93-245">Open the **Products.aspx.cs** code-behind and add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. <span data-ttu-id="f3d93-246">修改**GetCategories**方法来接收一个整数**minProductsCount**参数和筛选返回的结果。</span><span class="sxs-lookup"><span data-stu-id="f3d93-246">Modify the **GetCategories** method to receive an integer **minProductsCount** argument and filter the returned results.</span></span> <span data-ttu-id="f3d93-247">若要执行此操作，请使用以下代码替换方法。</span><span class="sxs-lookup"><span data-stu-id="f3d93-247">To do this, replace the method with the following code.</span></span>

    <span data-ttu-id="f3d93-248">(代码段- *Web 窗体实验-Ex01-GetCategories 2*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-248">(Code Snippet - *Web Forms Lab - Ex01 - GetCategories 2*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    <span data-ttu-id="f3d93-249">新 **[控制]** 特性，可以在**minProductsCount**参数将告知 ASP.NET 使用控件的页中，必须填充其值。</span><span class="sxs-lookup"><span data-stu-id="f3d93-249">The new **[Control]** attribute on the **minProductsCount** argument will let ASP.NET know its value must be populated using a control in the page.</span></span> <span data-ttu-id="f3d93-250">ASP.NET 将查找参数 (minProductsCount) 的名称匹配的任何控件，并执行必需的映射和转换，以控制值填充参数。</span><span class="sxs-lookup"><span data-stu-id="f3d93-250">ASP.NET will look for any control matching the name of the argument (minProductsCount) and perform the necessary mapping and conversion to fill the parameter with the control value.</span></span>

    <span data-ttu-id="f3d93-251">或者，该属性提供了可用于指定从何处获取此值控制的重载构造函数。</span><span class="sxs-lookup"><span data-stu-id="f3d93-251">Alternatively, the attribute provides an overloaded constructor that enables you to specify the control from where to get the value.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d93-252">数据绑定功能的一个目标是代码的减少需要编写的页交互量。</span><span class="sxs-lookup"><span data-stu-id="f3d93-252">One goal of the data-binding features is to reduce the amount of code that needs to be written for page interaction.</span></span> <span data-ttu-id="f3d93-253">除了 [控制] 值提供程序，可以在方法参数中使用其他模型绑定提供程序。</span><span class="sxs-lookup"><span data-stu-id="f3d93-253">Apart from the [Control] value provider, you can use other model-binding providers in your method parameters.</span></span> <span data-ttu-id="f3d93-254">任务简介中列出了其中一些。</span><span class="sxs-lookup"><span data-stu-id="f3d93-254">Some of them are listed in the task introduction.</span></span>
6. <span data-ttu-id="f3d93-255">按**F5**可开始调试网站并转到产品页。</span><span class="sxs-lookup"><span data-stu-id="f3d93-255">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="f3d93-256">在下拉列表中选择的产品数，并注意如何 GridView 现已更新。</span><span class="sxs-lookup"><span data-stu-id="f3d93-256">Select a number of products in the drop-down list and notice how the GridView is now updated.</span></span>

    <span data-ttu-id="f3d93-257">![筛选的下拉列表值 GridView](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "筛选的下拉列表值 GridView")</span><span class="sxs-lookup"><span data-stu-id="f3d93-257">![Filtering the GridView with a drop-down list value](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "Filtering the GridView with a drop-down list value")</span></span>

    <span data-ttu-id="f3d93-258">*筛选的下拉列表值 GridView*</span><span class="sxs-lookup"><span data-stu-id="f3d93-258">*Filtering the GridView with a drop-down list value*</span></span>
7. <span data-ttu-id="f3d93-259">停止调试。</span><span class="sxs-lookup"><span data-stu-id="f3d93-259">Stop debugging.</span></span>

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a><span data-ttu-id="f3d93-260">任务 4-使用模型绑定进行筛选</span><span class="sxs-lookup"><span data-stu-id="f3d93-260">Task 4 - Using Model Binding for Filtering</span></span>

<span data-ttu-id="f3d93-261">在本任务中，您将添加第二个子 GridView，其中显示所选类别中的产品。</span><span class="sxs-lookup"><span data-stu-id="f3d93-261">In this task, you will add a second, child GridView to show the products within the selected category.</span></span>

1. <span data-ttu-id="f3d93-262">打开**Products.aspx**页上，并更新类别 GridView 自动生成的选择按钮。</span><span class="sxs-lookup"><span data-stu-id="f3d93-262">Open the **Products.aspx** page and update the categories GridView to auto-generate the Select button.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. <span data-ttu-id="f3d93-263">添加另一个**GridView**名为**productsGrid**底部。</span><span class="sxs-lookup"><span data-stu-id="f3d93-263">Add a second **GridView** named **productsGrid** at the bottom.</span></span> <span data-ttu-id="f3d93-264">设置**ItemType**到**WebFormsLab.Model.Product**，则**DataKeyNames**到**ProductId**和**SelectMethod**到**GetProducts**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-264">Set the **ItemType** to **WebFormsLab.Model.Product**, the **DataKeyNames** to **ProductId** and the **SelectMethod** to **GetProducts**.</span></span> <span data-ttu-id="f3d93-265">设置**AutoGenerateColumns**到**false**和 ProductId、 ProductName、 说明和单价添加列。</span><span class="sxs-lookup"><span data-stu-id="f3d93-265">Set **AutoGenerateColumns** to **false** and add the columns for ProductId, ProductName, Description and UnitPrice.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. <span data-ttu-id="f3d93-266">打开**Products.aspx.cs**代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="f3d93-266">Open the **Products.aspx.cs** code-behind file.</span></span> <span data-ttu-id="f3d93-267">实现**GetProducts**方法以便接收来自 GridView 的类别的类别 ID 并筛选产品。</span><span class="sxs-lookup"><span data-stu-id="f3d93-267">Implement the **GetProducts** method to receive the category ID from the category GridView and filter the products.</span></span> <span data-ttu-id="f3d93-268">模型绑定将使用中的选定的行的参数值设置**categoriesGrid**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-268">Model binding will set the parameter value using the selected row in the **categoriesGrid**.</span></span> <span data-ttu-id="f3d93-269">由于参数名和控件名称不匹配，因此应控制值提供程序中指定的控件名称。</span><span class="sxs-lookup"><span data-stu-id="f3d93-269">Since the argument name and control name do not match, you should specify the name of the control in the Control value provider.</span></span>

    <span data-ttu-id="f3d93-270">(代码段- *Web 窗体实验-Ex01-GetProducts*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-270">(Code Snippet - *Web Forms Lab - Ex01 - GetProducts*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="f3d93-271">这种方法可以更方便地单元测试这些方法。</span><span class="sxs-lookup"><span data-stu-id="f3d93-271">This approach makes it easier to unit test these methods.</span></span> <span data-ttu-id="f3d93-272">不执行 Web 窗体位置，在单元测试上下文 [控制] 属性将不执行任何特定操作。</span><span class="sxs-lookup"><span data-stu-id="f3d93-272">On a unit test context, where Web Forms is not executing, the [Control] attribute will not perform any specific action.</span></span>
4. <span data-ttu-id="f3d93-273">打开**Products.aspx**页上，找到产品 GridView。</span><span class="sxs-lookup"><span data-stu-id="f3d93-273">Open the **Products.aspx** page and locate the products GridView.</span></span> <span data-ttu-id="f3d93-274">更新产品 GridView，其中显示用于编辑所选的产品的链接。</span><span class="sxs-lookup"><span data-stu-id="f3d93-274">Update the products GridView to show a link for editing the selected product.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. <span data-ttu-id="f3d93-275">打开**ProductDetails.aspx**页上的代码隐藏和替换**SelectProduct**用下面的代码的方法。</span><span class="sxs-lookup"><span data-stu-id="f3d93-275">Open the **ProductDetails.aspx** page code-behind and replace the **SelectProduct** method with the following code.</span></span>

    <span data-ttu-id="f3d93-276">(代码段- *Web 窗体实验-Ex01-SelectProduct 方法*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-276">(Code Snippet - *Web Forms Lab - Ex01 - SelectProduct Method*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="f3d93-277">请注意， **[QueryString]** 属性用于填充从查询字符串中的产品 id 参数的方法参数。</span><span class="sxs-lookup"><span data-stu-id="f3d93-277">Notice that the **[QueryString]** attribute is used to fill the method parameter from a productId parameter in the query string.</span></span>
6. <span data-ttu-id="f3d93-278">按**F5**可开始调试网站并转到产品页。</span><span class="sxs-lookup"><span data-stu-id="f3d93-278">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="f3d93-279">从 GridView 的类别中选择任何类别，请注意，更新产品 GridView。</span><span class="sxs-lookup"><span data-stu-id="f3d93-279">Select any category from the categories GridView and notice that the products GridView is updated.</span></span>

    <span data-ttu-id="f3d93-280">![显示从所选类别产品](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "显示从所选类别产品")</span><span class="sxs-lookup"><span data-stu-id="f3d93-280">![Showing products from the selected category](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "Showing products from the selected category")</span></span>

    <span data-ttu-id="f3d93-281">*显示从所选类别产品*</span><span class="sxs-lookup"><span data-stu-id="f3d93-281">*Showing products from the selected category*</span></span>
7. <span data-ttu-id="f3d93-282">单击**视图**产品打开 ProductDetails.aspx 页上的链接。</span><span class="sxs-lookup"><span data-stu-id="f3d93-282">Click the **View** link on a product to open the ProductDetails.aspx page.</span></span>

    <span data-ttu-id="f3d93-283">请注意页面正在使用 SelectMethod 使用 productId 将参数从查询字符串中检索产品。</span><span class="sxs-lookup"><span data-stu-id="f3d93-283">Notice that the page is retrieving the product with the SelectMethod using the productId parameter from the query string.</span></span>

    <span data-ttu-id="f3d93-284">![查看产品详细信息](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "查看产品详细信息")</span><span class="sxs-lookup"><span data-stu-id="f3d93-284">![Viewing the product details](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "Viewing the product details")</span></span>

    <span data-ttu-id="f3d93-285">*查看产品详细信息*</span><span class="sxs-lookup"><span data-stu-id="f3d93-285">*Viewing the product details*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d93-286">键入说明 （HTML） 的功能将在下一个练习中实现。</span><span class="sxs-lookup"><span data-stu-id="f3d93-286">The ability to type an HTML description will be implemented in the next exercise.</span></span>

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a><span data-ttu-id="f3d93-287">任务 5-使用模型绑定以执行更新操作</span><span class="sxs-lookup"><span data-stu-id="f3d93-287">Task 5 - Using Model Binding for Update Operations</span></span>

<span data-ttu-id="f3d93-288">在上一任务中，选择数据的主要使用模型绑定，在此任务中，您将学习如何在更新操作中使用模型绑定。</span><span class="sxs-lookup"><span data-stu-id="f3d93-288">In the previous task, you have used model binding mainly for selecting data, in this task you will learn how to use model binding in update operations.</span></span>

<span data-ttu-id="f3d93-289">你将更新的类别 GridView，以便用户可以更新类别。</span><span class="sxs-lookup"><span data-stu-id="f3d93-289">You will update the categories GridView to let the user update categories.</span></span>

1. <span data-ttu-id="f3d93-290">打开**Products.aspx**页上，并更新类别以自动生成编辑按钮并使用新的 GridView **UpdateMethod**属性来指定**UpdateCategory**方法来更新所选的项。</span><span class="sxs-lookup"><span data-stu-id="f3d93-290">Open the **Products.aspx** page and update the categories GridView to auto-generate the Edit button and use the new **UpdateMethod** attribute to specify an **UpdateCategory** method to update the selected item.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    <span data-ttu-id="f3d93-291">GridView 中的 DataKeyNames 属性定义哪些是唯一标识的模型绑定的对象的成员，因此，哪些是更新方法至少应接收的参数。</span><span class="sxs-lookup"><span data-stu-id="f3d93-291">The DataKeyNames attribute in the GridView define which are the members that uniquely identify the model-bound object and therefore, which are the parameters the update method should at least receive.</span></span>
2. <span data-ttu-id="f3d93-292">打开**Products.aspx.cs**代码隐藏文件，并实现**UpdateCategory**方法。</span><span class="sxs-lookup"><span data-stu-id="f3d93-292">Open the **Products.aspx.cs** code-behind file and implement the **UpdateCategory** method.</span></span> <span data-ttu-id="f3d93-293">该方法应接收要加载的当前类别、 填充 GridView 中的值，然后更新类别的类别 ID。</span><span class="sxs-lookup"><span data-stu-id="f3d93-293">The method should receive the category ID to load the current category, populate the values from the GridView and then update the category.</span></span>

    <span data-ttu-id="f3d93-294">(代码段- *Web 窗体实验-Ex01-UpdateCategory*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-294">(Code Snippet - *Web Forms Lab - Ex01 - UpdateCategory*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    <span data-ttu-id="f3d93-295">新**TryUpdateModel**中 Page 类的方法负责填充模型对象使用的页中的控件中的值。</span><span class="sxs-lookup"><span data-stu-id="f3d93-295">The new **TryUpdateModel** method in the Page class is responsible of populating the model object using the values from the controls in the page.</span></span> <span data-ttu-id="f3d93-296">在这种情况下，它将替换当前的 GridView 行编辑到更新后的值**类别**对象。</span><span class="sxs-lookup"><span data-stu-id="f3d93-296">In this case, it will replace the updated values from the current GridView row being edited into the **category** object.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d93-297">下一步练习将说明用于验证用户输入时编辑的对象数据 ModelState.IsValid 的使用情况。</span><span class="sxs-lookup"><span data-stu-id="f3d93-297">The next exercise will explain the usage of the ModelState.IsValid for validating the data entered by the user when editing the object.</span></span>
3. <span data-ttu-id="f3d93-298">运行网站并转到产品页。</span><span class="sxs-lookup"><span data-stu-id="f3d93-298">Run the site and go to the Products page.</span></span> <span data-ttu-id="f3d93-299">编辑类别。</span><span class="sxs-lookup"><span data-stu-id="f3d93-299">Edit a category.</span></span> <span data-ttu-id="f3d93-300">键入新名称，然后单击**更新**保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="f3d93-300">Type a new name and then click **Update** to persist the changes.</span></span>

    <span data-ttu-id="f3d93-301">![编辑类别](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "编辑类别")</span><span class="sxs-lookup"><span data-stu-id="f3d93-301">![Editing categories](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "Editing categories")</span></span>

    <span data-ttu-id="f3d93-302">*编辑类别*</span><span class="sxs-lookup"><span data-stu-id="f3d93-302">*Editing categories*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a><span data-ttu-id="f3d93-303">练习 2： 数据验证</span><span class="sxs-lookup"><span data-stu-id="f3d93-303">Exercise 2: Data Validation</span></span>

<span data-ttu-id="f3d93-304">在此练习中，您将学习在 ASP.NET 4.5 中的新数据验证功能。</span><span class="sxs-lookup"><span data-stu-id="f3d93-304">In this exercise, you will learn about the new data validation features in ASP.NET 4.5.</span></span> <span data-ttu-id="f3d93-305">将签出 Web 窗体中的新非介入式验证功能。</span><span class="sxs-lookup"><span data-stu-id="f3d93-305">You will check out the new unobtrusive validation features in Web Forms.</span></span> <span data-ttu-id="f3d93-306">将应用程序模型类中使用数据注释，用户输入验证，并最后，您将学习如何打开或关闭请求验证为在页面中的单个控件。</span><span class="sxs-lookup"><span data-stu-id="f3d93-306">You will use data annotations in the application model classes for user input validation, and finally, you will learn how to turn on or off request validation to individual controls in a page.</span></span>

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a><span data-ttu-id="f3d93-307">任务 1-非介入式验证</span><span class="sxs-lookup"><span data-stu-id="f3d93-307">Task 1 - Unobtrusive Validation</span></span>

<span data-ttu-id="f3d93-308">窗体的复杂数据包括验证程序往往会在页中，可以代表大约 60%的代码生成过多的 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="f3d93-308">Forms with complex data including validators tend to generate too much JavaScript code in the page, which can represent about 60% of the code.</span></span> <span data-ttu-id="f3d93-309">启用非介入式验证，使用 HTML 代码看起来更干净且整洁。</span><span class="sxs-lookup"><span data-stu-id="f3d93-309">With unobtrusive validation enabled, your HTML code will look cleaner and tidier.</span></span>

<span data-ttu-id="f3d93-310">在本部分中，您将启用非介入式验证在 ASP.NET 中要比较这两种配置生成的 HTML 代码。</span><span class="sxs-lookup"><span data-stu-id="f3d93-310">In this section, you will enable unobtrusive validation in ASP.NET to compare the HTML code generated by both configurations.</span></span>

1. <span data-ttu-id="f3d93-311">打开**Visual Studio 2012** ，然后打开**开始**解决方案位于**Source\Ex2 Validation\Begin**本实验的文件夹。</span><span class="sxs-lookup"><span data-stu-id="f3d93-311">Open **Visual Studio 2012** and open the **Begin** solution located in the **Source\Ex2-Validation\Begin** folder of this lab.</span></span> <span data-ttu-id="f3d93-312">或者，您可以从上一练习在现有解决方案上继续工作。</span><span class="sxs-lookup"><span data-stu-id="f3d93-312">Alternatively, you can continue working on your existing solution from the previous exercise.</span></span>

   1. <span data-ttu-id="f3d93-313">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="f3d93-313">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f3d93-314">为此，请在解决方案资源管理器中，单击**WebFormsLab**项目**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-314">To do this, in the Solution Explorer, click the **WebFormsLab** project **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f3d93-315">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="f3d93-315">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f3d93-316">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-316">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f3d93-317">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="f3d93-317">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f3d93-318">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="f3d93-318">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f3d93-319">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="f3d93-319">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f3d93-320">按**F5**启动 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f3d93-320">Press **F5** to start the web application.</span></span> <span data-ttu-id="f3d93-321">请转到客户页上，单击**添加新客户**链接。</span><span class="sxs-lookup"><span data-stu-id="f3d93-321">Go to the Customers page and click the **Add a New Customer** link.</span></span>
3. <span data-ttu-id="f3d93-322">在浏览器页上，右键单击并选择**查看源**选项打开的应用程序生成的 HTML 代码。</span><span class="sxs-lookup"><span data-stu-id="f3d93-322">Right-click on the browser page, and select **View Source** option to open the HTML code generated by the application.</span></span>

    <span data-ttu-id="f3d93-323">![显示页面的 HTML 代码](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "显示页面的 HTML 代码")</span><span class="sxs-lookup"><span data-stu-id="f3d93-323">![Showing the page HTML code](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "Showing the page HTML code")</span></span>

    <span data-ttu-id="f3d93-324">*显示页面的 HTML 代码*</span><span class="sxs-lookup"><span data-stu-id="f3d93-324">*Showing the page HTML code*</span></span>
4. <span data-ttu-id="f3d93-325">滚动浏览页的源代码，请注意，ASP.NET 注入了 JavaScript 代码和数据验证程序的页中执行验证并显示错误列表。</span><span class="sxs-lookup"><span data-stu-id="f3d93-325">Scroll through the page source code and notice that ASP.NET has injected JavaScript code and data validators in the page to perform the validations and show the error list.</span></span>

    <span data-ttu-id="f3d93-326">![验证 CustomerDetails 页面中的 JavaScript 代码](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "CustomerDetails 页中的验证 JavaScript 代码")</span><span class="sxs-lookup"><span data-stu-id="f3d93-326">![Validation JavaScript code in CustomerDetails page](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "Validation JavaScript code in CustomerDetails page")</span></span>

    <span data-ttu-id="f3d93-327">*验证 CustomerDetails 页面中的 JavaScript 代码*</span><span class="sxs-lookup"><span data-stu-id="f3d93-327">*Validation JavaScript code in CustomerDetails page*</span></span>
5. <span data-ttu-id="f3d93-328">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f3d93-328">Close the browser and go back to Visual Studio.</span></span>
6. <span data-ttu-id="f3d93-329">现在将启用非介入式验证。</span><span class="sxs-lookup"><span data-stu-id="f3d93-329">Now you will enable unobtrusive validation.</span></span> <span data-ttu-id="f3d93-330">打开**Web.Config**并找到**ValidationSettings:UnobtrusiveValidationMode**中的键**AppSettings**部分 **。**</span><span class="sxs-lookup"><span data-stu-id="f3d93-330">Open **Web.Config** and locate **ValidationSettings:UnobtrusiveValidationMode** key in the **AppSettings** section **.**</span></span> <span data-ttu-id="f3d93-331">将密钥值设置为**WebForms**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-331">Set the key value to **WebForms**.</span></span>

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > <span data-ttu-id="f3d93-332">此外可以设置此属性&quot;**页面\_负载**&quot;以防你想要启用非介入式验证仅对某些页面的事件。</span><span class="sxs-lookup"><span data-stu-id="f3d93-332">You can also set this property in the &quot;**Page\_Load**&quot; event in case you want to enable Unobtrusive Validation only for some pages.</span></span>
7. <span data-ttu-id="f3d93-333">打开**CustomerDetails.aspx**然后按**F5**启动 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f3d93-333">Open **CustomerDetails.aspx** and press **F5** to start the Web application.</span></span>
8. <span data-ttu-id="f3d93-334">按 F12 键以打开 IE 开发人员工具。</span><span class="sxs-lookup"><span data-stu-id="f3d93-334">Press the F12 key to open the IE developer tools.</span></span> <span data-ttu-id="f3d93-335">开发人员工具打开后，选择脚本选项卡。选择**CustomerDetails.aspx**从菜单和需要注意需的页面上运行 jQuery 的脚本已加载到浏览器中从本地站点。</span><span class="sxs-lookup"><span data-stu-id="f3d93-335">Once the developer tools is open, select the script tab. Select **CustomerDetails.aspx** from the menu and take note that the scripts required to run jQuery on the page have been loaded into the browser from the local site.</span></span>

    <span data-ttu-id="f3d93-336">![正在加载 jQuery JavaScript 文件直接从本地 IIS 服务器](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "加载 jQuery JavaScript 文件直接从本地 IIS 服务器")</span><span class="sxs-lookup"><span data-stu-id="f3d93-336">![Loading the jQuery JavaScript files directly from the local IIS server](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "Loading the jQuery JavaScript files directly from the local IIS server")</span></span>

    <span data-ttu-id="f3d93-337">*直接从本地 IIS 服务器加载 jQuery JavaScript 文件*</span><span class="sxs-lookup"><span data-stu-id="f3d93-337">*Loading the jQuery JavaScript files directly from the local IIS server*</span></span>
9. <span data-ttu-id="f3d93-338">关闭浏览器以返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f3d93-338">Close the browser to return to Visual Studio.</span></span> <span data-ttu-id="f3d93-339">打开**Site.Master**再次文件，找到**ScriptManager**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-339">Open the **Site.Master** file again and locate the **ScriptManager**.</span></span> <span data-ttu-id="f3d93-340">将属性添加**EnableCdn**属性的值**True**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-340">Add the attribute **EnableCdn** property with the value **True**.</span></span> <span data-ttu-id="f3d93-341">这将强制 jQuery 加载从在线的 URL，而不在本地站点的 URL。</span><span class="sxs-lookup"><span data-stu-id="f3d93-341">This will force jQuery to be loaded from the online URL, not from the local site's URL.</span></span>
10. <span data-ttu-id="f3d93-342">打开**CustomerDetails.aspx** Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="f3d93-342">Open **CustomerDetails.aspx** in Visual Studio.</span></span> <span data-ttu-id="f3d93-343">按 F5 键以运行该站点。</span><span class="sxs-lookup"><span data-stu-id="f3d93-343">Press the F5 key to run the site.</span></span> <span data-ttu-id="f3d93-344">Internet Explorer 打开后，按 F12 键以打开开发人员工具。</span><span class="sxs-lookup"><span data-stu-id="f3d93-344">Once Internet Explorer opens, press the F12 key to open the developer tools.</span></span> <span data-ttu-id="f3d93-345">选择**脚本**选项卡，然后再看一下拉列表。</span><span class="sxs-lookup"><span data-stu-id="f3d93-345">Select the **Script** tab, and then take a look at the drop-down list.</span></span> <span data-ttu-id="f3d93-346">请注意不能再从本地站点，而是在线 jQuery CDN 加载 jQuery JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="f3d93-346">Note the jQuery JavaScript files are no longer being loaded from the local site, but rather from the online jQuery CDN.</span></span>

    <span data-ttu-id="f3d93-347">![正在加载 jQuery JavaScript 文件从 CDN](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "加载 jQuery JavaScript 文件从 CDN")</span><span class="sxs-lookup"><span data-stu-id="f3d93-347">![Loading the jQuery JavaScript files from the CDN](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "Loading the jQuery JavaScript files from the CDN")</span></span>

    <span data-ttu-id="f3d93-348">*加载从 CDN 的 jQuery JavaScript 文件*</span><span class="sxs-lookup"><span data-stu-id="f3d93-348">*Loading the jQuery JavaScript files from the CDN*</span></span>
11. <span data-ttu-id="f3d93-349">打开 HTML 页的源代码再次在浏览器中使用查看源选项。</span><span class="sxs-lookup"><span data-stu-id="f3d93-349">Open the HTML page source code again using the View source option in the browser.</span></span> <span data-ttu-id="f3d93-350">请注意，通过启用非介入式验证 ASP.NET 已替换为插入的 JavaScript 代码的数据-\*属性。</span><span class="sxs-lookup"><span data-stu-id="f3d93-350">Notice that by enabling the unobtrusive validation ASP.NET has replaced the injected JavaScript code with data- \*attributes.</span></span>

    <span data-ttu-id="f3d93-351">![非介入式验证代码](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "非介入式验证代码")</span><span class="sxs-lookup"><span data-stu-id="f3d93-351">![Unobtrusive validation code](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "Unobtrusive validation code")</span></span>

    <span data-ttu-id="f3d93-352">*非介入式验证代码*</span><span class="sxs-lookup"><span data-stu-id="f3d93-352">*Unobtrusive validation code*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d93-353">在此示例中，您已了解如何验证摘要的数据注释已简化为只需少量 HTML 和 JavaScript 行。</span><span class="sxs-lookup"><span data-stu-id="f3d93-353">In this example, you saw how a validation summary with Data annotations was simplified to only a few HTML and JavaScript lines.</span></span> <span data-ttu-id="f3d93-354">以前，而不进行非介入式验证，您添加更多验证控件越大 JavaScript 验证代码将会增长。</span><span class="sxs-lookup"><span data-stu-id="f3d93-354">Previously, without unobtrusive validation, the more validation controls you add, the bigger your JavaScript validation code will grow.</span></span>

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a><span data-ttu-id="f3d93-355">任务 2-验证模型的数据注释</span><span class="sxs-lookup"><span data-stu-id="f3d93-355">Task 2 - Validating the Model with Data Annotations</span></span>

<span data-ttu-id="f3d93-356">ASP.NET 4.5 引入了 Web 窗体的数据批注验证。</span><span class="sxs-lookup"><span data-stu-id="f3d93-356">ASP.NET 4.5 introduces data annotations validation for Web Forms.</span></span> <span data-ttu-id="f3d93-357">而不是让每个输入的验证控件，您现在可以在模型类中定义的约束，并使用它们跨所有 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f3d93-357">Instead of having a validation control on each input, you can now define constraints in your model classes and use them across all your web application.</span></span> <span data-ttu-id="f3d93-358">在本部分中，将了解如何使用数据注释来验证新建/编辑客户窗体。</span><span class="sxs-lookup"><span data-stu-id="f3d93-358">In this section, you will learn how to use data annotations for validating a new/edit customer form.</span></span>

1. <span data-ttu-id="f3d93-359">打开**CustomerDetail.aspx**页。</span><span class="sxs-lookup"><span data-stu-id="f3d93-359">Open **CustomerDetail.aspx** page.</span></span> <span data-ttu-id="f3d93-360">请注意，客户名字和中的第二个名称**EditItemTemplate**并**InsertItemTemplate**部分通过 RequiredFieldValidator 控件进行验证。</span><span class="sxs-lookup"><span data-stu-id="f3d93-360">Notice that the customer first name and second name in the **EditItemTemplate** and **InsertItemTemplate** sections are validated using a RequiredFieldValidator controls.</span></span> <span data-ttu-id="f3d93-361">每个验证程序是关联到某个特定条件，因此您需要作为条件来检查包含任意多个验证程序。</span><span class="sxs-lookup"><span data-stu-id="f3d93-361">Each validator is associated to a particular condition, so you need to include as many validators as conditions to check.</span></span>
2. <span data-ttu-id="f3d93-362">添加数据批注验证 Customer 模型类。</span><span class="sxs-lookup"><span data-stu-id="f3d93-362">Add data annotations to validate the Customer model class.</span></span> <span data-ttu-id="f3d93-363">打开**Customer.cs**类**模型**文件夹和*修饰*使用数据注释特性的每个属性。</span><span class="sxs-lookup"><span data-stu-id="f3d93-363">Open **Customer.cs** class in the **Model** folder and *decorate* each property using data annotation attributes.</span></span>

    <span data-ttu-id="f3d93-364">(代码段- *Web 窗体实验-Ex02-数据批注*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-364">(Code Snippet - *Web Forms Lab - Ex02 - Data Annotations*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > <span data-ttu-id="f3d93-365">.NET framework 4.5 已扩展现有的数据批注集合。</span><span class="sxs-lookup"><span data-stu-id="f3d93-365">.NET Framework 4.5 has extended the existing data annotation collection.</span></span> <span data-ttu-id="f3d93-366">以下是一些可以使用的数据批注: [CreditCard]，[Phone] [EmailAddress] [区域] [比较] [Url]，[FileExtensions]，[Required]、[Key]，[正则表达式]。</span><span class="sxs-lookup"><span data-stu-id="f3d93-366">These are some of the data annotations you can use: [CreditCard], [Phone], [EmailAddress], [Range], [Compare], [Url], [FileExtensions], [Required], [Key], [RegularExpression].</span></span>
    > 
    > <span data-ttu-id="f3d93-367">一些用法示例：</span><span class="sxs-lookup"><span data-stu-id="f3d93-367">Some usage examples:</span></span>
    > 
    > [Key]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > <span data-ttu-id="f3d93-369">此外可以定义自己的错误消息中的每个属性。</span><span class="sxs-lookup"><span data-stu-id="f3d93-369">You can also define your own error messages within each attribute.</span></span>
3. <span data-ttu-id="f3d93-370">打开**CustomerDetails.aspx**和 FormView 控件在 EditItemTemplate InsertItemTemplate 部分中删除的第一个和最后一个名称字段的所有 RequiredFieldvalidators。</span><span class="sxs-lookup"><span data-stu-id="f3d93-370">Open **CustomerDetails.aspx** and remove all the RequiredFieldvalidators for the first and last name fields in the in EditItemTemplate and InsertItemTemplate sections of the FormView control.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > <span data-ttu-id="f3d93-371">使用数据注释的一个优点是不会在应用程序页面中重复验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="f3d93-371">One advantage of using data annotations is that validation logic is not duplicated in your application pages.</span></span> <span data-ttu-id="f3d93-372">您在模型中，定义一次，并使用它跨所有操作数据的应用程序页。</span><span class="sxs-lookup"><span data-stu-id="f3d93-372">You define it once in the model, and use it across all the application pages that manipulate data.</span></span>
4. <span data-ttu-id="f3d93-373">打开**CustomerDetails.aspx**代码隐藏和找到 SaveCustomer 方法。</span><span class="sxs-lookup"><span data-stu-id="f3d93-373">Open **CustomerDetails.aspx** code-behind and locate the SaveCustomer method.</span></span> <span data-ttu-id="f3d93-374">此方法调用时插入新客户，并接收客户参数来自 FormView 控件值。</span><span class="sxs-lookup"><span data-stu-id="f3d93-374">This method is called when inserting a new customer and receives the Customer parameter from the FormView control values.</span></span> <span data-ttu-id="f3d93-375">当页面控件与参数对象发生之间的映射，ASP.NET 将执行针对所有数据批注的模型验证特性和 ModelState 字典填充遇到的错误，如果有的话。</span><span class="sxs-lookup"><span data-stu-id="f3d93-375">When the mapping between the page controls and the parameter object occurrs, ASP.NET will execute the model validation against all the data annotation attributes and fill the ModelState dictionary with the errors encountered, if any.</span></span>

    <span data-ttu-id="f3d93-376">ModelState.IsValid 将仅返回 true，如果执行验证后，您在模型上的所有字段都是有效。</span><span class="sxs-lookup"><span data-stu-id="f3d93-376">The ModelState.IsValid will only return true if all the fields on your model are valid after performing the validation.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. <span data-ttu-id="f3d93-377">添加**ValidationSummary** CustomerDetails 页后，可以显示的模型错误的列表末尾处的控件。</span><span class="sxs-lookup"><span data-stu-id="f3d93-377">Add a **ValidationSummary** control at the end of the CustomerDetails page to show the list of model errors.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    <span data-ttu-id="f3d93-378">**ShowModelStateErrors**是 ValidationSummary 上的新属性来控制，在设置为**true**，控件将显示 ModelState 字典中的错误。</span><span class="sxs-lookup"><span data-stu-id="f3d93-378">The **ShowModelStateErrors** is a new property on the ValidationSummary control that when set to **true**, the control will show the errors from the ModelState dictionary.</span></span> <span data-ttu-id="f3d93-379">这些错误来自数据批注验证。</span><span class="sxs-lookup"><span data-stu-id="f3d93-379">These errors come from the data annotations validation.</span></span>
6. <span data-ttu-id="f3d93-380">按**F5**运行 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f3d93-380">Press **F5** to run the Web application.</span></span> <span data-ttu-id="f3d93-381">完成窗体的某些错误值，然后单击**保存**执行验证。</span><span class="sxs-lookup"><span data-stu-id="f3d93-381">Complete the form with some erroneous values and click **Save** to execute validation.</span></span> <span data-ttu-id="f3d93-382">请注意，错误摘要在底部。</span><span class="sxs-lookup"><span data-stu-id="f3d93-382">Notice the error summary at the bottom.</span></span>

    <span data-ttu-id="f3d93-383">![使用数据注释验证](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "使用数据注释验证")</span><span class="sxs-lookup"><span data-stu-id="f3d93-383">![Validation with Data Annotations](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "Validation with Data Annotations")</span></span>

    <span data-ttu-id="f3d93-384">*使用数据注释验证*</span><span class="sxs-lookup"><span data-stu-id="f3d93-384">*Validation with Data Annotations*</span></span>

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a><span data-ttu-id="f3d93-385">任务 3-处理自定义数据库错误的 ModelState</span><span class="sxs-lookup"><span data-stu-id="f3d93-385">Task 3 - Handling Custom Database Errors with ModelState</span></span>

<span data-ttu-id="f3d93-386">在以前版本的 Web 窗体，如太长字符串或唯一键冲突的数据库错误处理可能涉及在存储库代码中引发异常，然后处理在您的后台代码显示错误，异常。</span><span class="sxs-lookup"><span data-stu-id="f3d93-386">In previous version of Web Forms, handling database errors such as a too long string or a unique key violation could involve throwing exceptions in your repository code and then handling the exceptions on your code-behind to display an error.</span></span> <span data-ttu-id="f3d93-387">非常高的代码需要做相对简单的事。</span><span class="sxs-lookup"><span data-stu-id="f3d93-387">A great amount of code is required to do something relatively simple.</span></span>

<span data-ttu-id="f3d93-388">在 Web 窗体 4.5 ModelState 对象可以用于以一致的方式在页面上，从您的模型或从数据库中，显示的错误。</span><span class="sxs-lookup"><span data-stu-id="f3d93-388">In Web Forms 4.5, the ModelState object can be used to display the errors on the page, either from your model or from the database, in a consistent manner.</span></span>

<span data-ttu-id="f3d93-389">在本任务中，将添加代码以正确处理数据库异常，并使用 ModelState 对象向用户显示相应的消息。</span><span class="sxs-lookup"><span data-stu-id="f3d93-389">In this task, you will add code to properly handle database exceptions and show the appropriate message to the user using the ModelState object.</span></span>

1. <span data-ttu-id="f3d93-390">当应用程序仍在运行时，尝试更新使用重复的值的类别的名称。</span><span class="sxs-lookup"><span data-stu-id="f3d93-390">While the application is still running, try to update the name of a category using a duplicated value.</span></span>

    <span data-ttu-id="f3d93-391">![具有重复名称更新类别](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "具有重复名称更新类别")</span><span class="sxs-lookup"><span data-stu-id="f3d93-391">![Updating a category with a duplicated name](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "Updating a category with a duplicated name")</span></span>

    <span data-ttu-id="f3d93-392">*具有重复名称更新类别*</span><span class="sxs-lookup"><span data-stu-id="f3d93-392">*Updating a category with a duplicated name*</span></span>

    <span data-ttu-id="f3d93-393">请注意，由于会引发异常&quot;唯一&quot;约束**CategoryName**列。</span><span class="sxs-lookup"><span data-stu-id="f3d93-393">Notice that an exception is thrown due to the &quot;unique&quot; constraint of the **CategoryName** column.</span></span>

    <span data-ttu-id="f3d93-394">![重复的类别名称的异常](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "重复的类别名称的异常")</span><span class="sxs-lookup"><span data-stu-id="f3d93-394">![Exception for duplicated category names](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "Exception for duplicated category names")</span></span>

    <span data-ttu-id="f3d93-395">*重复的类别名称的异常*</span><span class="sxs-lookup"><span data-stu-id="f3d93-395">*Exception for duplicated category names*</span></span>
2. <span data-ttu-id="f3d93-396">停止调试。</span><span class="sxs-lookup"><span data-stu-id="f3d93-396">Stop debugging.</span></span> <span data-ttu-id="f3d93-397">在中**Products.aspx.cs**代码隐藏文件，update **UpdateCategory**方法以处理数据库引发的异常。Savechanges （） 方法调用并添加一个错误， **ModelState**对象。</span><span class="sxs-lookup"><span data-stu-id="f3d93-397">In the **Products.aspx.cs** code-behind file, update the **UpdateCategory** method to handle the exceptions thrown by the db.SaveChanges() method call and add an error to the **ModelState** object.</span></span>

    <span data-ttu-id="f3d93-398">新**TryUpdateModel**方法更新使用窗体数据由用户提供从数据库检索到的类别对象。</span><span class="sxs-lookup"><span data-stu-id="f3d93-398">The new **TryUpdateModel** method updates the category object retrieved from the database using the form data provided by the user.</span></span>

    <span data-ttu-id="f3d93-399">(代码段- *Web 窗体实验-Ex02-UpdateCategory 处理错误*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-399">(Code Snippet - *Web Forms Lab - Ex02 - UpdateCategory Handle Errors*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > <span data-ttu-id="f3d93-400">理想情况下，需要确定 DbUpdateException 的原因并检查是否违反唯一键约束的根本原因。</span><span class="sxs-lookup"><span data-stu-id="f3d93-400">Ideally, you would have to identify the cause of the DbUpdateException and check if the root cause is the violation of a unique key constraint.</span></span>
3. <span data-ttu-id="f3d93-401">打开**Products.aspx**并添加**ValidationSummary**如下类别 GridView，其中显示的模型错误的列表控件。</span><span class="sxs-lookup"><span data-stu-id="f3d93-401">Open **Products.aspx** and add a **ValidationSummary** control below the categories GridView to show the list of model errors.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. <span data-ttu-id="f3d93-402">运行网站并转到产品页。</span><span class="sxs-lookup"><span data-stu-id="f3d93-402">Run the site and go to the Products page.</span></span> <span data-ttu-id="f3d93-403">尝试更新使用的重复的值的类别的名称。</span><span class="sxs-lookup"><span data-stu-id="f3d93-403">Try to update the name of a category using an duplicated value.</span></span>

    <span data-ttu-id="f3d93-404">请注意，处理异常和错误消息显示在**ValidationSummary**控件。</span><span class="sxs-lookup"><span data-stu-id="f3d93-404">Notice that the exception was handled and the error message appears in the **ValidationSummary** control.</span></span>

    <span data-ttu-id="f3d93-405">![复制类别错误](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "重复类别错误")</span><span class="sxs-lookup"><span data-stu-id="f3d93-405">![Duplicated category error](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "Duplicated category error")</span></span>

    <span data-ttu-id="f3d93-406">*重复的类别错误*</span><span class="sxs-lookup"><span data-stu-id="f3d93-406">*Duplicated category error*</span></span>

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a><span data-ttu-id="f3d93-407">任务 4-请求 ASP.NET Web 窗体 4.5 中的验证</span><span class="sxs-lookup"><span data-stu-id="f3d93-407">Task 4 - Request Validation in ASP.NET Web Forms 4.5</span></span>

<span data-ttu-id="f3d93-408">在 ASP.NET 请求验证功能提供了一定的默认保护免受跨站点脚本 (XSS) 攻击。</span><span class="sxs-lookup"><span data-stu-id="f3d93-408">The request validation feature in ASP.NET provides a certain level of default protection against cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="f3d93-409">在以前版本的 ASP.NET，请求验证默认情况下已启用，仅可以禁用整个页面。</span><span class="sxs-lookup"><span data-stu-id="f3d93-409">In previous versions of ASP.NET, request validation was enabled by default and could only be disabled for an entire page.</span></span> <span data-ttu-id="f3d93-410">使用 ASP.NET Web 窗体的新版本现在可以禁用单个控件请求验证、 执行延迟请求验证或访问未经过验证的请求数据 （请小心，如果这样做 ！）。</span><span class="sxs-lookup"><span data-stu-id="f3d93-410">With the new version of ASP.NET Web Forms you can now disable the request validation for a single control, perform lazy request validation or access un-validated request data (be careful if you do so!).</span></span>

1. <span data-ttu-id="f3d93-411">按**Ctrl + F5**启动网站，而不进行调试，转到产品页。</span><span class="sxs-lookup"><span data-stu-id="f3d93-411">Press **Ctrl+F5** to start the site without debugging and go to the Products page.</span></span> <span data-ttu-id="f3d93-412">选择一个类别，然后单击**编辑**上的任何产品的链接。</span><span class="sxs-lookup"><span data-stu-id="f3d93-412">Select a category and then click the **Edit** link on any of the products.</span></span>
2. <span data-ttu-id="f3d93-413">键入包含具有潜在危险的内容，例如包括 HTML 标记的说明。</span><span class="sxs-lookup"><span data-stu-id="f3d93-413">Type a description containing potentially dangerous content, for instance including HTML tags.</span></span> <span data-ttu-id="f3d93-414">注意由于请求验证引发的异常。</span><span class="sxs-lookup"><span data-stu-id="f3d93-414">Take notice of the exception thrown due to the request validation.</span></span>

    <span data-ttu-id="f3d93-415">![编辑与具有潜在危险的内容的产品](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "编辑产品具有潜在危险的内容")</span><span class="sxs-lookup"><span data-stu-id="f3d93-415">![Editing a product with potentially dangerous content](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "Editing a product with potentially dangerous content")</span></span>

    <span data-ttu-id="f3d93-416">*编辑产品具有潜在危险的内容*</span><span class="sxs-lookup"><span data-stu-id="f3d93-416">*Editing a product with potentially dangerous content*</span></span>

    <span data-ttu-id="f3d93-417">![因请求验证而引发的异常](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "因请求验证而引发的异常")</span><span class="sxs-lookup"><span data-stu-id="f3d93-417">![Exception thrown due to request validation](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "Exception thrown due to request validation")</span></span>

    <span data-ttu-id="f3d93-418">*因请求验证而引发的异常*</span><span class="sxs-lookup"><span data-stu-id="f3d93-418">*Exception thrown due to request validation*</span></span>
3. <span data-ttu-id="f3d93-419">关闭页，并在 Visual Studio 中，按**SHIFT + F5**以停止调试。</span><span class="sxs-lookup"><span data-stu-id="f3d93-419">Close the page and, in Visual Studio, press **SHIFT+F5** to stop debugging.</span></span>
4. <span data-ttu-id="f3d93-420">打开**ProductDetails.aspx**页上，找到**说明**文本框中。</span><span class="sxs-lookup"><span data-stu-id="f3d93-420">Open the **ProductDetails.aspx** page and locate the **Description** TextBox.</span></span>
5. <span data-ttu-id="f3d93-421">添加新**ValidateRequestMode**属性设置为文本框中并将其值设置为**禁用**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-421">Add the new **ValidateRequestMode** property to the TextBox and set its value to **Disabled**.</span></span>

    <span data-ttu-id="f3d93-422">新**ValidateRequestMode**特性，您可以禁用每个控件上精细地请求验证。</span><span class="sxs-lookup"><span data-stu-id="f3d93-422">The new **ValidateRequestMode** attribute allows you to disable the request validation granularly on each control.</span></span> <span data-ttu-id="f3d93-423">当你想要使用的输入的可能接收 HTML 代码，但想要保留的页的其余部分使用的验证时，这很有用。</span><span class="sxs-lookup"><span data-stu-id="f3d93-423">This is useful when you want to use an input that may receive HTML code, but want to keep the validation working for the rest of the page.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. <span data-ttu-id="f3d93-424">按**F5**运行 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f3d93-424">Press **F5** to run the web application.</span></span> <span data-ttu-id="f3d93-425">再次打开编辑产品页，并完成包括 HTML 标记的产品说明。</span><span class="sxs-lookup"><span data-stu-id="f3d93-425">Open the edit product page again and complete a product description including HTML tags.</span></span> <span data-ttu-id="f3d93-426">请注意，可以现在将 HTML 内容添加到说明。</span><span class="sxs-lookup"><span data-stu-id="f3d93-426">Notice that you can now add HTML content to the description.</span></span>

    <span data-ttu-id="f3d93-427">![请求验证的产品说明禁用](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "请求验证已禁用的产品说明")</span><span class="sxs-lookup"><span data-stu-id="f3d93-427">![Request validation disabled for the product description](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "Request validation disabled for the product description")</span></span>

    <span data-ttu-id="f3d93-428">*请求验证已禁用的产品说明*</span><span class="sxs-lookup"><span data-stu-id="f3d93-428">*Request validation disabled for the product description*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d93-429">应在生产应用程序中，清理输入的用户名，以确保输入唯一安全的 HTML 标记的 HTML 代码 (例如，有没有&lt;脚本&gt;标记)。</span><span class="sxs-lookup"><span data-stu-id="f3d93-429">In a production application, you should sanitize the HTML code entered by the user to make sure only safe HTML tags are entered (for example, there are no &lt;script&gt; tags).</span></span> <span data-ttu-id="f3d93-430">若要执行此操作，可以使用[Microsoft Web Protection Library](https://www.nuget.org/packages/AntiXSS)。</span><span class="sxs-lookup"><span data-stu-id="f3d93-430">To do this, you can use [Microsoft Web Protection Library](https://www.nuget.org/packages/AntiXSS).</span></span>
7. <span data-ttu-id="f3d93-431">再次编辑该产品。</span><span class="sxs-lookup"><span data-stu-id="f3d93-431">Edit the product again.</span></span> <span data-ttu-id="f3d93-432">在名称字段中键入 HTML 代码，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-432">Type HTML code in the Name field and click **Save**.</span></span> <span data-ttu-id="f3d93-433">请注意，说明字段中仅禁用请求验证并重新字段的其余部分仍验证针对具有潜在危险的内容。</span><span class="sxs-lookup"><span data-stu-id="f3d93-433">Notice that Request Validation is only disabled for the Description field and the rest of the fields re still validated against the potentially dangerous content.</span></span>

    <span data-ttu-id="f3d93-434">![请求验证其余字段中启用](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "请求验证其余字段中启用")</span><span class="sxs-lookup"><span data-stu-id="f3d93-434">![Request validation enabled in the rest of the fields](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "Request validation enabled in the rest of the fields")</span></span>

    <span data-ttu-id="f3d93-435">*在其余字段中启用请求验证*</span><span class="sxs-lookup"><span data-stu-id="f3d93-435">*Request validation enabled in the rest of the fields*</span></span>

    <span data-ttu-id="f3d93-436">ASP.NET Web 窗体 4.5 包括新的请求验证模式下惰式执行请求验证。</span><span class="sxs-lookup"><span data-stu-id="f3d93-436">ASP.NET Web Forms 4.5 includes a new request validation mode to perform request validation lazily.</span></span> <span data-ttu-id="f3d93-437">请求验证模式设置为**4.5**，如果一段代码访问*Request.Form [&quot;密钥&quot;]*，ASP.NET 4.5 请求验证将仅触发器请求验证该窗体集合中的特定元素。</span><span class="sxs-lookup"><span data-stu-id="f3d93-437">With the request validation mode set to **4.5**, if a piece of code accesses *Request.Form[&quot;key&quot;]*, ASP.NET 4.5's request validation will only trigger request validation for that specific element in the form collection.</span></span>

    <span data-ttu-id="f3d93-438">此外，ASP.NET 4.5 现在包括核心编码例程从 Microsoft ANTI-XSS 库版本 4.0。</span><span class="sxs-lookup"><span data-stu-id="f3d93-438">Additionally, ASP.NET 4.5 now includes core encoding routines from the Microsoft Anti-XSS Library v4.0.</span></span> <span data-ttu-id="f3d93-439">防 XSS 编码例程所实现的新*AntiXssEncoder*类型位于新**System.Web.Security.AntiXss**命名空间。</span><span class="sxs-lookup"><span data-stu-id="f3d93-439">The Anti-XSS encoding routines are implemented by the new *AntiXssEncoder* type found in the new **System.Web.Security.AntiXss** namespace.</span></span> <span data-ttu-id="f3d93-440">与**encoderType**配置为使用的参数*AntiXssEncoder*，自动编码在 ASP.NET 中使用新的编码例程，所有输出。</span><span class="sxs-lookup"><span data-stu-id="f3d93-440">With the **encoderType** parameter configured to use *AntiXssEncoder*, all output encoding within ASP.NET automatically uses the new encoding routines.</span></span>
8. <span data-ttu-id="f3d93-441">ASP.NET 4.5 请求验证还支持对请求数据未经过验证的访问。</span><span class="sxs-lookup"><span data-stu-id="f3d93-441">ASP.NET 4.5 request validation also supports un-validated access to request data.</span></span> <span data-ttu-id="f3d93-442">ASP.NET 4.5 中添加到新集合属性**HttpRequest**对象调用**Unvalidated**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-442">ASP.NET 4.5 adds a new collection property to the **HttpRequest** object called **Unvalidated**.</span></span> <span data-ttu-id="f3d93-443">导航到**HttpRequest.Unvalidated**有权访问的所有请求数据，包括窗体、 Querystring、 Cookie、 Url 和等等的公共部分。</span><span class="sxs-lookup"><span data-stu-id="f3d93-443">When you navigate into **HttpRequest.Unvalidated** you have access to all of the common pieces of request data, including Forms, QueryStrings, Cookies, URLs, and so on.</span></span>

    <span data-ttu-id="f3d93-444">![Request.Unvalidated 对象](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "Request.Unvalidated 对象")</span><span class="sxs-lookup"><span data-stu-id="f3d93-444">![Request.Unvalidated object](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "Request.Unvalidated object")</span></span>

    <span data-ttu-id="f3d93-445">*Request.Unvalidated 对象*</span><span class="sxs-lookup"><span data-stu-id="f3d93-445">*Request.Unvalidated object*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d93-446">**请谨慎使用 HttpRequest.Unvalidated 属性 ！**</span><span class="sxs-lookup"><span data-stu-id="f3d93-446">**Please use the HttpRequest.Unvalidated property with caution!**</span></span> <span data-ttu-id="f3d93-447">请确保仔细对原始请求数据，以确保危险文本未往返和呈现回毫无戒心的客户执行自定义验证 ！</span><span class="sxs-lookup"><span data-stu-id="f3d93-447">Make sure you carefully perform custom validation on the raw request data to ensure that dangerous text is not round-tripped and rendered back to unsuspecting customers!</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a><span data-ttu-id="f3d93-448">练习 3： 异步页处理在 ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="f3d93-448">Exercise 3: Asynchronous Page Processing in ASP.NET Web Forms</span></span>

<span data-ttu-id="f3d93-449">在此练习中，将向你介绍新的异步页处理 ASP.NET Web 窗体中的功能。</span><span class="sxs-lookup"><span data-stu-id="f3d93-449">In this exercise, you will be introduced to the new asynchronous page processing features in ASP.NET Web Forms.</span></span>

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a><span data-ttu-id="f3d93-450">任务 1-更新产品详细信息页面上传并显示图像</span><span class="sxs-lookup"><span data-stu-id="f3d93-450">Task 1 - Updating the Product Details Page to Upload and Show Images</span></span>

<span data-ttu-id="f3d93-451">在本任务中，你将更新产品详细信息页，以允许用户指定产品的图像 URL 并将其显示在只读视图。</span><span class="sxs-lookup"><span data-stu-id="f3d93-451">In this task, you will update the product details page to allow the user to specify an image URL for the product and display it in the read-only view.</span></span> <span data-ttu-id="f3d93-452">通过以同步方式下载，将创建指定的图像的本地副本。</span><span class="sxs-lookup"><span data-stu-id="f3d93-452">You will create a local copy of the specified image by downloading it synchronously.</span></span> <span data-ttu-id="f3d93-453">在下一任务中，你将更新此实现，使其以异步方式工作。</span><span class="sxs-lookup"><span data-stu-id="f3d93-453">In the next task, you will update this implementation to make it work asynchronously.</span></span>

1. <span data-ttu-id="f3d93-454">打开**Visual Studio 2012**并加载**开始**解决方案位于**Source\Ex3 Async\Begin**从本实验的文件夹。</span><span class="sxs-lookup"><span data-stu-id="f3d93-454">Open **Visual Studio 2012** and load the **Begin** solution located in **Source\Ex3-Async\Begin** from this lab's folder.</span></span> <span data-ttu-id="f3d93-455">或者，您可以从上一练习在现有解决方案上继续工作。</span><span class="sxs-lookup"><span data-stu-id="f3d93-455">Alternatively, you can continue working on your existing solution from the previous exercises.</span></span>

   1. <span data-ttu-id="f3d93-456">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="f3d93-456">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f3d93-457">为此，请在解决方案资源管理器中，单击**WebFormsLab**项目，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-457">To do this, in the Solution Explorer, click the **WebFormsLab** project and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f3d93-458">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="f3d93-458">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f3d93-459">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-459">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f3d93-460">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="f3d93-460">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f3d93-461">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="f3d93-461">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f3d93-462">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="f3d93-462">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f3d93-463">打开**ProductDetails.aspx**页上源，以显示产品图像的 FormView 的 ItemTemplate 中添加一个字段。</span><span class="sxs-lookup"><span data-stu-id="f3d93-463">Open the **ProductDetails.aspx** page source and add a field in the FormView's ItemTemplate to show the product image.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. <span data-ttu-id="f3d93-464">添加字段以在 FormView 的 EditTemplate 中指定图像 URL。</span><span class="sxs-lookup"><span data-stu-id="f3d93-464">Add a field to specify the image URL in the FormView's EditTemplate.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. <span data-ttu-id="f3d93-465">打开**ProductDetails.aspx.cs**代码隐藏文件，并添加以下命名空间指令。</span><span class="sxs-lookup"><span data-stu-id="f3d93-465">Open the **ProductDetails.aspx.cs** code-behind file and add the following namespace directives.</span></span>

    <span data-ttu-id="f3d93-466">(代码段- *Web 窗体实验室-Ex03-命名空间*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-466">(Code Snippet - *Web Forms Lab - Ex03 - Namespaces*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. <span data-ttu-id="f3d93-467">创建**UpdateProductImage**方法将远程图像存储在本地**映像**文件夹，然后更新 product 实体与新的图像位置值。</span><span class="sxs-lookup"><span data-stu-id="f3d93-467">Create an **UpdateProductImage** method to store remote images in the local **Images** folder and update the product entity with the new image location value.</span></span>

    <span data-ttu-id="f3d93-468">(代码段- *Web 窗体实验室-Ex03-UpdateProductImage*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-468">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. <span data-ttu-id="f3d93-469">更新**UpdateProduct**方法来调用**UpdateProductImage**方法。</span><span class="sxs-lookup"><span data-stu-id="f3d93-469">Update the **UpdateProduct** method to call the **UpdateProductImage** method.</span></span>

    <span data-ttu-id="f3d93-470">(代码段- *Web 窗体实验室-Ex03-UpdateProductImage 调用*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-470">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage Call*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. <span data-ttu-id="f3d93-471">运行应用程序并尝试上传的映像的产品。</span><span class="sxs-lookup"><span data-stu-id="f3d93-471">Run the application and try to upload an image for a product.</span></span> <span data-ttu-id="f3d93-472">例如，可以使用 Office 剪贴画中的以下映像 URL: [[http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)</span><span class="sxs-lookup"><span data-stu-id="f3d93-472">For example, you can use the following image URL from Office Clip Arts: [[http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)</span></span>

    <span data-ttu-id="f3d93-473">![设置产品的映像](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "设置产品的图像")</span><span class="sxs-lookup"><span data-stu-id="f3d93-473">![Setting an image for a product](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "Setting an image for a product")</span></span>

    <span data-ttu-id="f3d93-474">*设置产品的图像*</span><span class="sxs-lookup"><span data-stu-id="f3d93-474">*Setting an image for a product*</span></span>

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a><span data-ttu-id="f3d93-475">任务 2-添加异步处理到产品详细信息页</span><span class="sxs-lookup"><span data-stu-id="f3d93-475">Task 2 - Adding Asynchronous Processing to the Product Details Page</span></span>

<span data-ttu-id="f3d93-476">在本任务中，你将更新产品详细信息页，使其以异步方式工作。</span><span class="sxs-lookup"><span data-stu-id="f3d93-476">In this task, you will update the product details page to make it work asynchronously.</span></span> <span data-ttu-id="f3d93-477">将使用 ASP.NET 4.5 异步页处理，从而提高长时间运行任务-映像下载过程的性能。</span><span class="sxs-lookup"><span data-stu-id="f3d93-477">You will enhance a long running task - the image download process - by using ASP.NET 4.5 asynchronous page processing.</span></span>

<span data-ttu-id="f3d93-478">Web 应用程序中的异步方法可用于优化 ASP.NET 线程池的使用的方式。</span><span class="sxs-lookup"><span data-stu-id="f3d93-478">Asynchronous methods in web applications can be used to optimize the way ASP.NET thread pools are used.</span></span> <span data-ttu-id="f3d93-479">在 ASP.NET 中存在是有限的数量的不顾及在线程池中的线程请求，因此时所有线程都处于忙碌状态，, ASP.NET 开始拒绝新请求、 发送应用程序错误消息并将你的站点不可用。</span><span class="sxs-lookup"><span data-stu-id="f3d93-479">In ASP.NET there are a limited number of threads in the thread pool for attending requests, thus, when all the threads are busy, ASP.NET starts to reject new requests, sends application error messages and makes your site unavailable.</span></span>

<span data-ttu-id="f3d93-480">在网站上耗时的操作都非常适合进行异步编程，因为它们所分配的线程占用很长时间。</span><span class="sxs-lookup"><span data-stu-id="f3d93-480">Time-consuming operations on your web site are great candidates for asynchronous programming because they occupy the assigned thread for a long time.</span></span> <span data-ttu-id="f3d93-481">这包括长时间运行的请求，具有大量不同的元素的页和页需要脱机操作中，将此类查询的数据库或访问外部 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="f3d93-481">This includes long running requests, pages with lots of different elements and pages that require offline operations, such querying a database or accessing an external web server.</span></span> <span data-ttu-id="f3d93-482">优点是处理页面时，这些操作使用异步方法，如果线程被释放并返回到线程池，用于处理新的页面请求。</span><span class="sxs-lookup"><span data-stu-id="f3d93-482">The advantage is that if you use asynchronous methods for these operations, while the page is processing, the thread is freed and returned to the thread pool and can be used to attend to a new page request.</span></span> <span data-ttu-id="f3d93-483">这意味着，页面才会开始在线程池从一个线程中处理和异步处理完成后，可能会完成在一个不同的处理。</span><span class="sxs-lookup"><span data-stu-id="f3d93-483">This means, the page will start processing in one thread from the thread pool and might complete processing in a different one, after the async processing completes.</span></span>

1. <span data-ttu-id="f3d93-484">打开**ProductDetails.aspx**页。</span><span class="sxs-lookup"><span data-stu-id="f3d93-484">Open the **ProductDetails.aspx** page.</span></span> <span data-ttu-id="f3d93-485">添加**异步**属性中**页面**元素并将其设置为**true**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-485">Add the **Async** attribute in the **Page** element and set it to **true**.</span></span> <span data-ttu-id="f3d93-486">此属性告知 ASP.NET 实现 IHttpAsyncHandler 接口。</span><span class="sxs-lookup"><span data-stu-id="f3d93-486">This attribute tells ASP.NET to implement the IHttpAsyncHandler interface.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. <span data-ttu-id="f3d93-487">要显示的线程正在运行页的详细信息的页的底部添加一个标签。</span><span class="sxs-lookup"><span data-stu-id="f3d93-487">Add a Label at the bottom of the page to show the details of the threads running the page.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. <span data-ttu-id="f3d93-488">打开**ProductDetails.aspx.cs**并添加以下命名空间指令。</span><span class="sxs-lookup"><span data-stu-id="f3d93-488">Open up **ProductDetails.aspx.cs** and add the following namespace directives.</span></span>

    <span data-ttu-id="f3d93-489">(代码段- *Web 窗体实验室-Ex03-命名空间 2*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-489">(Code Snippet - *Web Forms Lab - Ex03 - Namespaces 2*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. <span data-ttu-id="f3d93-490">修改**UpdateProductImage**方法以下载具有一个异步任务的图像。</span><span class="sxs-lookup"><span data-stu-id="f3d93-490">Modify the **UpdateProductImage** method to download the image with an asynchronous task.</span></span> <span data-ttu-id="f3d93-491">将替换**WebClient** **DownloadFile**方法替换**DownloadFileTaskAsync**方法，包括**await**关键字。</span><span class="sxs-lookup"><span data-stu-id="f3d93-491">You will replace the **WebClient** **DownloadFile** method with the **DownloadFileTaskAsync** method and include the **await** keyword.</span></span>

    <span data-ttu-id="f3d93-492">(代码段- *Web 窗体实验室-Ex03-UpdateProductImage 异步*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-492">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage Async*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    <span data-ttu-id="f3d93-493">RegisterAsyncTask 注册新的页面异步任务要执行的另一个线程。</span><span class="sxs-lookup"><span data-stu-id="f3d93-493">The RegisterAsyncTask registers a new page asynchronous task to be executed in a different thread.</span></span> <span data-ttu-id="f3d93-494">它将接收要执行的任务 (t) 的 lambda 表达式。</span><span class="sxs-lookup"><span data-stu-id="f3d93-494">It receives a lambda expression with the Task (t) to be executed.</span></span> <span data-ttu-id="f3d93-495">**Await**中的关键字**DownloadFileTaskAsync**方法将转换后，将异步调用的回调方法的剩余部分**DownloadFileTaskAsync**方法完成。</span><span class="sxs-lookup"><span data-stu-id="f3d93-495">The **await** keyword in the **DownloadFileTaskAsync** method converts the remainder of the method into a callback that is invoked asynchronously after the **DownloadFileTaskAsync** method has completed.</span></span> <span data-ttu-id="f3d93-496">ASP.NET 将恢复自动维护所有原始 HTTP 请求值的方法的执行。</span><span class="sxs-lookup"><span data-stu-id="f3d93-496">ASP.NET will resume the execution of the method by automatically maintaining all the HTTP request original values.</span></span> <span data-ttu-id="f3d93-497">在.NET 4.5 中的新异步编程模型，可编写异步代码，看上去非常类似于同步代码，并让编译器处理回调函数或延续代码的复杂性。</span><span class="sxs-lookup"><span data-stu-id="f3d93-497">The new asynchronous programming model in .NET 4.5 enables you to write asynchronous code that looks very much like synchronous code, and let the compiler handle the complications of callback functions or continuation code.</span></span>
    > [!NOTE]
    > <span data-ttu-id="f3d93-498">RegisterAsyncTask 和 PageAsyncTask 自.NET 2.0 以来已可用。</span><span class="sxs-lookup"><span data-stu-id="f3d93-498">RegisterAsyncTask and PageAsyncTask were already available since .NET 2.0.</span></span> <span data-ttu-id="f3d93-499">Await 关键字新从.NET 4.5 的异步编程模型，可与.NET WebClient 对象的新 TaskAsync 方法一起使用。</span><span class="sxs-lookup"><span data-stu-id="f3d93-499">The await keyword is new from the .NET 4.5 asynchronous programming model and can be used together with the new TaskAsync methods from the .NET WebClient object.</span></span>
5. <span data-ttu-id="f3d93-500">添加代码以显示的线程的代码在其启动和完成执行。</span><span class="sxs-lookup"><span data-stu-id="f3d93-500">Add code to display the threads on which the code started and finished executing.</span></span> <span data-ttu-id="f3d93-501">若要执行此操作，更新**UpdateProductImage**用下面的代码的方法。</span><span class="sxs-lookup"><span data-stu-id="f3d93-501">To do this, update the **UpdateProductImage** method with the following code.</span></span>

    <span data-ttu-id="f3d93-502">(代码段- *Web 窗体实验室-Ex03-显示线程*)</span><span class="sxs-lookup"><span data-stu-id="f3d93-502">(Code Snippet - *Web Forms Lab - Ex03 - Show threads*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. <span data-ttu-id="f3d93-503">打开网站的**Web.config**文件。</span><span class="sxs-lookup"><span data-stu-id="f3d93-503">Open the web site's **Web.config** file.</span></span> <span data-ttu-id="f3d93-504">添加以下 appSetting 变量。</span><span class="sxs-lookup"><span data-stu-id="f3d93-504">Add the following appSetting variable.</span></span>

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. <span data-ttu-id="f3d93-505">按**F5**运行应用程序并将该产品的图像上传。</span><span class="sxs-lookup"><span data-stu-id="f3d93-505">Press **F5** to run the application and upload an image for the product.</span></span> <span data-ttu-id="f3d93-506">请注意，启动和完成的代码可能不同的线程 ID。</span><span class="sxs-lookup"><span data-stu-id="f3d93-506">Notice the threads ID where the code started and finished may be different.</span></span> <span data-ttu-id="f3d93-507">这是因为从 ASP.NET 线程池的单独线程上运行的异步任务。</span><span class="sxs-lookup"><span data-stu-id="f3d93-507">This is because asynchronous tasks run on a separate thread from ASP.NET thread pool.</span></span> <span data-ttu-id="f3d93-508">完成任务后，ASP.NET 将任务放回队列中，并将分配任何可用的线程。</span><span class="sxs-lookup"><span data-stu-id="f3d93-508">When the task completes, ASP.NET puts the task back in the queue and assigns any of the available threads.</span></span>

    <span data-ttu-id="f3d93-509">![以异步方式下载图像](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "异步下载图像")</span><span class="sxs-lookup"><span data-stu-id="f3d93-509">![Downloading an image asynchronously](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "Downloading an image asynchronously")</span></span>

    <span data-ttu-id="f3d93-510">*以异步方式下载图像*</span><span class="sxs-lookup"><span data-stu-id="f3d93-510">*Downloading an image asynchronously*</span></span>

> [!NOTE]
> <span data-ttu-id="f3d93-511">此外，您可以此应用程序部署到 Azure 的以下[附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署](#AppendixB)。</span><span class="sxs-lookup"><span data-stu-id="f3d93-511">Additionally, you can deploy this application to Azure following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="f3d93-512">总结</span><span class="sxs-lookup"><span data-stu-id="f3d93-512">Summary</span></span>

<span data-ttu-id="f3d93-513">在此动手实验中，已分析并演示以下概念：</span><span class="sxs-lookup"><span data-stu-id="f3d93-513">In this hands-on lab, the following concepts have been addressed and demonstrated:</span></span>

- <span data-ttu-id="f3d93-514">使用强类型化数据绑定表达式</span><span class="sxs-lookup"><span data-stu-id="f3d93-514">Use strongly-typed data-binding expressions</span></span>
- <span data-ttu-id="f3d93-515">在 Web 窗体中使用新的模型绑定功能</span><span class="sxs-lookup"><span data-stu-id="f3d93-515">Use new model binding features in Web Forms</span></span>
- <span data-ttu-id="f3d93-516">将值提供程序用于将页面数据映射到代码隐藏方法</span><span class="sxs-lookup"><span data-stu-id="f3d93-516">Use value providers for mapping page data to code-behind methods</span></span>
- <span data-ttu-id="f3d93-517">用户输入验证中使用数据注释</span><span class="sxs-lookup"><span data-stu-id="f3d93-517">Use Data Annotations for user input validation</span></span>
- <span data-ttu-id="f3d93-518">在 Web 窗体中执行 advange unobstrusive 使用 jQuery 的客户端验证</span><span class="sxs-lookup"><span data-stu-id="f3d93-518">Take advange of unobstrusive client-side validation with jQuery in Web Forms</span></span>
- <span data-ttu-id="f3d93-519">实现粒度请求验证</span><span class="sxs-lookup"><span data-stu-id="f3d93-519">Implement granular request validation</span></span>
- <span data-ttu-id="f3d93-520">实现在 Web 窗体中处理的异步页面</span><span class="sxs-lookup"><span data-stu-id="f3d93-520">Implement asynchronous page processing in Web Forms</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="f3d93-521">附录 a： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="f3d93-521">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="f3d93-522">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="f3d93-522">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="f3d93-523">以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="f3d93-523">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="f3d93-524">转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="f3d93-524">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="f3d93-525">或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="f3d93-525">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="f3d93-526">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-526">Click on **Install Now**.</span></span> <span data-ttu-id="f3d93-527">如果还没有**Web 平台安装程序**将重定向以下载并安装。</span><span class="sxs-lookup"><span data-stu-id="f3d93-527">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="f3d93-528">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="f3d93-528">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="f3d93-529">![安装 Visual Studio Express](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="f3d93-529">![Install Visual Studio Express](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="f3d93-530">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="f3d93-530">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="f3d93-531">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="f3d93-531">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    <span data-ttu-id="f3d93-533">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="f3d93-533">*Accepting the license terms*</span></span>
5. <span data-ttu-id="f3d93-534">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="f3d93-534">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    <span data-ttu-id="f3d93-536">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="f3d93-536">*Installation progress*</span></span>
6. <span data-ttu-id="f3d93-537">安装完成后，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-537">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    <span data-ttu-id="f3d93-539">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="f3d93-539">*Installation completed*</span></span>
7. <span data-ttu-id="f3d93-540">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="f3d93-540">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="f3d93-541">若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="f3d93-541">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    <span data-ttu-id="f3d93-543">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="f3d93-543">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="f3d93-544">附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="f3d93-544">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="f3d93-545">本附录将演示如何从 Azure 门户创建新的网站和发布应用程序获取按照本实验中，利用 Azure 提供的 Web 部署发布功能。</span><span class="sxs-lookup"><span data-stu-id="f3d93-545">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="f3d93-546">任务 1-从 Azure 门户创建新的 Web 站点</span><span class="sxs-lookup"><span data-stu-id="f3d93-546">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="f3d93-547">转到[Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="f3d93-547">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d93-548">借助 Azure 可以免费托管 10 个 ASP.NET 网站，然后随着流量增长情况。</span><span class="sxs-lookup"><span data-stu-id="f3d93-548">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="f3d93-549">你可以注册[此处](http://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="f3d93-549">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="f3d93-550">![登录到 Windows Azure 门户](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "登录到 Windows Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="f3d93-550">![Log on to Windows Azure portal](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="f3d93-551">*登录到门户*</span><span class="sxs-lookup"><span data-stu-id="f3d93-551">*Log on to the Portal*</span></span>
2. <span data-ttu-id="f3d93-552">单击**新建**命令栏上。</span><span class="sxs-lookup"><span data-stu-id="f3d93-552">Click **New** on the command bar.</span></span>

    <span data-ttu-id="f3d93-553">![创建新的 Web 站点](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "创建新的 Web 站点")</span><span class="sxs-lookup"><span data-stu-id="f3d93-553">![Creating a new Web Site](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="f3d93-554">*创建新的 Web 站点*</span><span class="sxs-lookup"><span data-stu-id="f3d93-554">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="f3d93-555">单击**计算** | **网站**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-555">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="f3d93-556">然后选择**快速创建**选项。</span><span class="sxs-lookup"><span data-stu-id="f3d93-556">Then select **Quick Create** option.</span></span> <span data-ttu-id="f3d93-557">为新网站提供可用的 URL，然后单击**创建网站**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-557">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d93-558">Azure 是可以控制和管理在云中运行的 web 应用程序的主机。</span><span class="sxs-lookup"><span data-stu-id="f3d93-558">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="f3d93-559">快速创建选项，可部署到 Azure 门户外部的已完成的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f3d93-559">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="f3d93-560">它不包括用于设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="f3d93-560">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="f3d93-561">![创建新的网站使用快速创建](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "创建新的网站使用快速创建")</span><span class="sxs-lookup"><span data-stu-id="f3d93-561">![Creating a new Web Site using Quick Create](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="f3d93-562">*创建新的网站使用快速创建*</span><span class="sxs-lookup"><span data-stu-id="f3d93-562">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="f3d93-563">等到新**网站**创建。</span><span class="sxs-lookup"><span data-stu-id="f3d93-563">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="f3d93-564">创建网站后，单击下面的链接**URL**列。</span><span class="sxs-lookup"><span data-stu-id="f3d93-564">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="f3d93-565">检查新的 Web 站点正常工作。</span><span class="sxs-lookup"><span data-stu-id="f3d93-565">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="f3d93-566">![浏览到新的 web 站点](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "浏览到新的 web 站点")</span><span class="sxs-lookup"><span data-stu-id="f3d93-566">![Browsing to the new web site](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="f3d93-567">*浏览到新的 web 站点*</span><span class="sxs-lookup"><span data-stu-id="f3d93-567">*Browsing to the new web site*</span></span>

    <span data-ttu-id="f3d93-568">![正在运行的网站](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "正在运行的网站")</span><span class="sxs-lookup"><span data-stu-id="f3d93-568">![Web site running](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "Web site running")</span></span>

    <span data-ttu-id="f3d93-569">*正在运行的网站*</span><span class="sxs-lookup"><span data-stu-id="f3d93-569">*Web site running*</span></span>
6. <span data-ttu-id="f3d93-570">返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。</span><span class="sxs-lookup"><span data-stu-id="f3d93-570">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="f3d93-571">![打开网站管理页](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="f3d93-571">![Opening the web site management pages](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="f3d93-572">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="f3d93-572">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="f3d93-573">在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。</span><span class="sxs-lookup"><span data-stu-id="f3d93-573">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d93-574">*发布配置文件*包含所有发布到 Azure 的 web 应用程序为每个启用的发布方法所需的信息。</span><span class="sxs-lookup"><span data-stu-id="f3d93-574">The *publish profile* contains all of the information required to publish a web application to Azure for each enabled publication method.</span></span> <span data-ttu-id="f3d93-575">发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="f3d93-575">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="f3d93-576">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="f3d93-576">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="f3d93-577">![正在下载网站发布配置文件](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="f3d93-577">![Downloading the web site publish profile](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="f3d93-578">*正在下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="f3d93-578">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="f3d93-579">下载发布配置文件到已知位置。</span><span class="sxs-lookup"><span data-stu-id="f3d93-579">Download the publish profile file to a known location.</span></span> <span data-ttu-id="f3d93-580">进一步在此练习中将了解如何使用此文件发布到 Azure 的 web 应用程序从 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f3d93-580">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="f3d93-581">![保存发布配置文件](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="f3d93-581">![Saving the publish profile file](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "Saving the publish profile")</span></span>

    <span data-ttu-id="f3d93-582">*保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="f3d93-582">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="f3d93-583">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="f3d93-583">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="f3d93-584">如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="f3d93-584">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="f3d93-585">如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="f3d93-585">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="f3d93-586">用于存储应用程序数据库，将需要 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="f3d93-586">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="f3d93-587">可以从在 Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**.</span><span class="sxs-lookup"><span data-stu-id="f3d93-587">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="f3d93-588">如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。</span><span class="sxs-lookup"><span data-stu-id="f3d93-588">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="f3d93-589">请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="f3d93-589">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="f3d93-590">不创建数据库，因为它将在后面的阶段中创建。</span><span class="sxs-lookup"><span data-stu-id="f3d93-590">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="f3d93-591">![SQL 数据库服务器仪表板](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database 服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="f3d93-591">![SQL Database Server Dashboard](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="f3d93-592">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="f3d93-592">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="f3d93-593">在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-593">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="f3d93-594">若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框中，然后单击![add-client-ip-address-ok-button](whats-new-in-web-forms-in-aspnet-45/_static/image39.png)按钮。</span><span class="sxs-lookup"><span data-stu-id="f3d93-594">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) button.</span></span>

    ![添加客户端 IP 地址](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    <span data-ttu-id="f3d93-596">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="f3d93-596">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="f3d93-597">一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。</span><span class="sxs-lookup"><span data-stu-id="f3d93-597">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认更改](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    <span data-ttu-id="f3d93-599">*确认更改*</span><span class="sxs-lookup"><span data-stu-id="f3d93-599">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="f3d93-600">任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布</span><span class="sxs-lookup"><span data-stu-id="f3d93-600">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="f3d93-601">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="f3d93-601">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="f3d93-602">在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-602">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="f3d93-603">![发布应用程序](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="f3d93-603">![Publishing the Application](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "Publishing the Application")</span></span>

    <span data-ttu-id="f3d93-604">*发布此网站*</span><span class="sxs-lookup"><span data-stu-id="f3d93-604">*Publishing the web site*</span></span>
2. <span data-ttu-id="f3d93-605">导入发布配置文件保存在第一个任务。</span><span class="sxs-lookup"><span data-stu-id="f3d93-605">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="f3d93-606">![导入发布配置文件](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="f3d93-606">![Importing the publish profile](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "Importing the publish profile")</span></span>

    <span data-ttu-id="f3d93-607">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="f3d93-607">*Importing publish profile*</span></span>
3. <span data-ttu-id="f3d93-608">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-608">Click **Validate Connection**.</span></span> <span data-ttu-id="f3d93-609">验证完成后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-609">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d93-610">请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。</span><span class="sxs-lookup"><span data-stu-id="f3d93-610">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="f3d93-611">![验证连接](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "验证连接")</span><span class="sxs-lookup"><span data-stu-id="f3d93-611">![Validating connection](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "Validating connection")</span></span>

    <span data-ttu-id="f3d93-612">*验证连接*</span><span class="sxs-lookup"><span data-stu-id="f3d93-612">*Validating connection*</span></span>
4. <span data-ttu-id="f3d93-613">在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="f3d93-613">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="f3d93-614">![Web 部署配置](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="f3d93-614">![Web deploy configuration](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web deploy configuration")</span></span>

    <span data-ttu-id="f3d93-615">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="f3d93-615">*Web deploy configuration*</span></span>
5. <span data-ttu-id="f3d93-616">配置数据库连接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3d93-616">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="f3d93-617">在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。</span><span class="sxs-lookup"><span data-stu-id="f3d93-617">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="f3d93-618">在中**用户名**键入服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="f3d93-618">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="f3d93-619">在中**密码**键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="f3d93-619">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="f3d93-620">键入新的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="f3d93-620">Type a new database name.</span></span>

     <span data-ttu-id="f3d93-621">![配置目标连接字符串](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="f3d93-621">![Configuring destination connection string](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="f3d93-622">*配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="f3d93-622">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="f3d93-623">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="f3d93-623">Then click **OK**.</span></span> <span data-ttu-id="f3d93-624">当系统提示你创建数据库时，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-624">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="f3d93-625">![创建数据库](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="f3d93-625">![Creating the database](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "Creating the database string")</span></span>

    <span data-ttu-id="f3d93-626">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="f3d93-626">*Creating the database*</span></span>
7. <span data-ttu-id="f3d93-627">将用于连接到 Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。</span><span class="sxs-lookup"><span data-stu-id="f3d93-627">The connection string you will use to connect to SQL Database in Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="f3d93-628">然后，单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-628">Then click **Next**.</span></span>

    <span data-ttu-id="f3d93-629">![连接字符串指向 SQL 数据库](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "指向 SQL 数据库连接字符串")</span><span class="sxs-lookup"><span data-stu-id="f3d93-629">![Connection string pointing to SQL Database](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="f3d93-630">*连接字符串指向 SQL 数据库*</span><span class="sxs-lookup"><span data-stu-id="f3d93-630">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="f3d93-631">在中**预览版**页上，单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-631">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="f3d93-632">![Web 应用程序发布](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="f3d93-632">![Publishing the web application](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "Publishing the web application")</span></span>

    <span data-ttu-id="f3d93-633">*Web 应用程序发布*</span><span class="sxs-lookup"><span data-stu-id="f3d93-633">*Publishing the web application*</span></span>
9. <span data-ttu-id="f3d93-634">在发布过程完成后，在默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="f3d93-634">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="f3d93-635">附录 c： 使用代码片段</span><span class="sxs-lookup"><span data-stu-id="f3d93-635">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="f3d93-636">使用代码段，可以轻松获得相关所需的所有代码。</span><span class="sxs-lookup"><span data-stu-id="f3d93-636">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="f3d93-637">实验室文档将告诉您完全何时可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="f3d93-637">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="f3d93-638">![使用 Visual Studio 代码段代码插入到你的项目](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "使用 Visual Studio 代码段代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="f3d93-638">![Using Visual Studio code snippets to insert code into your project](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="f3d93-639">*使用 Visual Studio 代码段代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="f3d93-639">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="f3d93-640">***若要添加代码段使用键盘 (仅限 C#)***</span><span class="sxs-lookup"><span data-stu-id="f3d93-640">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="f3d93-641">将光标置于要插入的代码。</span><span class="sxs-lookup"><span data-stu-id="f3d93-641">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="f3d93-642">开始键入代码片段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="f3d93-642">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="f3d93-643">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="f3d93-643">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="f3d93-644">选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。</span><span class="sxs-lookup"><span data-stu-id="f3d93-644">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="f3d93-645">按 Tab 键两次，以在光标位置插入代码段。</span><span class="sxs-lookup"><span data-stu-id="f3d93-645">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="f3d93-646">![开始键入代码段名称](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="f3d93-646">![Start typing the snippet name](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "Start typing the snippet name")</span></span>

<span data-ttu-id="f3d93-647">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="f3d93-647">*Start typing the snippet name*</span></span>

<span data-ttu-id="f3d93-648">![按 tab 键以选择突出显示代码段](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="f3d93-648">![Press Tab to select the highlighted snippet](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="f3d93-649">*按 tab 键以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="f3d93-649">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="f3d93-650">![再次按 Tab 和代码段将 expand](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "再次按 Tab 和代码段将扩展")</span><span class="sxs-lookup"><span data-stu-id="f3d93-650">![Press Tab again and the snippet will expand](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="f3d93-651">*再次按 Tab 和代码段将扩展*</span><span class="sxs-lookup"><span data-stu-id="f3d93-651">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="f3d93-652">***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。</span><span class="sxs-lookup"><span data-stu-id="f3d93-652">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="f3d93-653">右键单击你想要插入的代码片段。</span><span class="sxs-lookup"><span data-stu-id="f3d93-653">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="f3d93-654">选择**插入代码段**跟**我的代码片段**。</span><span class="sxs-lookup"><span data-stu-id="f3d93-654">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="f3d93-655">通过单击选择列表中中的相关代码片段。</span><span class="sxs-lookup"><span data-stu-id="f3d93-655">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="f3d93-656">![右键单击你想要插入代码段和选择插入代码段](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "右键单击你想要插入代码段和选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="f3d93-656">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="f3d93-657">*右键单击你想要插入代码段和选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="f3d93-657">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="f3d93-658">![通过单击选择列表中中的相关代码片段](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "通过单击选择列表中中的相关代码片段")</span><span class="sxs-lookup"><span data-stu-id="f3d93-658">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="f3d93-659">*通过单击选择列表中中的相关代码片段*</span><span class="sxs-lookup"><span data-stu-id="f3d93-659">*Pick the relevant snippet from the list, by clicking on it*</span></span>
