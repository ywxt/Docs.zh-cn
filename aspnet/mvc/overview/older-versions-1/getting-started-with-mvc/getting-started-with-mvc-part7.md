---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: 向模型添加验证 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 1a8c186d5a6b00aaf1061bb4025f4f062203a7df
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37402975"
---
<a name="adding-validation-to-the-model"></a><span data-ttu-id="5ba37-104">向模型添加验证</span><span class="sxs-lookup"><span data-stu-id="5ba37-104">Adding Validation to the Model</span></span>
====================
<span data-ttu-id="5ba37-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="5ba37-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="5ba37-106">这是介绍 ASP.NET MVC 的基础知识初学者教程。</span><span class="sxs-lookup"><span data-stu-id="5ba37-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="5ba37-107">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="5ba37-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="5ba37-108">请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="5ba37-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="5ba37-109">在本部分中我们要实现启用我们的应用程序中的输入的验证所需的支持。</span><span class="sxs-lookup"><span data-stu-id="5ba37-109">In this section we are going to implement the support necessary to enable input validation within our application.</span></span> <span data-ttu-id="5ba37-110">我们将确保我们的数据库内容始终是正确的并且它们尝试并输入电影数据无效时向最终用户提供有用的错误消息。</span><span class="sxs-lookup"><span data-stu-id="5ba37-110">We'll ensure that our database content is always correct, and provide helpful error messages to end users when they try and enter Movie data which is not valid.</span></span> <span data-ttu-id="5ba37-111">我们将开始将少量验证逻辑添加到电影类。</span><span class="sxs-lookup"><span data-stu-id="5ba37-111">We'll begin by adding a little validation logic to the Movie class.</span></span>

<span data-ttu-id="5ba37-112">右键单击模型文件夹并选择添加类。</span><span class="sxs-lookup"><span data-stu-id="5ba37-112">Right click on the Model folder and select Add Class.</span></span> <span data-ttu-id="5ba37-113">命名您的类的电影。</span><span class="sxs-lookup"><span data-stu-id="5ba37-113">Name your class Movie.</span></span>

<span data-ttu-id="5ba37-114">当我们在前面创建的电影实体模型时，IDE 将创建 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="5ba37-114">When we created the Movie Entity Model earlier, the IDE created a Movie class.</span></span> <span data-ttu-id="5ba37-115">事实上，可以在一个文件，将在另一部分是电影类的一部分。</span><span class="sxs-lookup"><span data-stu-id="5ba37-115">In fact, part of the Movie class can be in one file and part in another.</span></span> <span data-ttu-id="5ba37-116">这被称为一个分部类。</span><span class="sxs-lookup"><span data-stu-id="5ba37-116">This is called a Partial Class.</span></span> <span data-ttu-id="5ba37-117">我们将从另一个文件扩展 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="5ba37-117">We're going to extend the Movie class from another file.</span></span>

<span data-ttu-id="5ba37-118">我们将使用将验证提示给系统一些属性，指向"合作者类"创建部分 movie 类。</span><span class="sxs-lookup"><span data-stu-id="5ba37-118">We'll create a partial movie class that points to a "buddy class" with some attributes that will give validation hints to the system.</span></span> <span data-ttu-id="5ba37-119">我们将标记的 Title 和价格为必需的并还坚持的价格为某范围内。</span><span class="sxs-lookup"><span data-stu-id="5ba37-119">We'll mark the Title and Price as Required, and also insist that the Price be within a certain range.</span></span> <span data-ttu-id="5ba37-120">右键单击 Models 文件夹，然后选择添加类。</span><span class="sxs-lookup"><span data-stu-id="5ba37-120">Right click the Models folder and select Add Class.</span></span> <span data-ttu-id="5ba37-121">命名您的类的电影，然后单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="5ba37-121">Name your class Movie and Click the OK button.</span></span> <span data-ttu-id="5ba37-122">下面是我们部分的 Movie 类如下所示的内容。</span><span class="sxs-lookup"><span data-stu-id="5ba37-122">Here's what our partial Movie class looks like.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

<span data-ttu-id="5ba37-123">重新运行你的应用程序并尝试输入的电影价格超过 100。</span><span class="sxs-lookup"><span data-stu-id="5ba37-123">Re-Run your application and try to enter a movie with a price over 100.</span></span> <span data-ttu-id="5ba37-124">已提交表单后，将会出错。</span><span class="sxs-lookup"><span data-stu-id="5ba37-124">You'll get an error after you've submitted the form.</span></span> <span data-ttu-id="5ba37-125">错误捕获在服务器端和发送窗体后发生。</span><span class="sxs-lookup"><span data-stu-id="5ba37-125">The error is caught on the server side and occurs after the Form is POSTed.</span></span> <span data-ttu-id="5ba37-126">请注意如何 ASP.NET MVC 内置 HTML 帮助程序已不够智能，无法显示错误消息和维护为我们在文本框中元素的值：</span><span class="sxs-lookup"><span data-stu-id="5ba37-126">Notice how ASP.NET MVC's built-in HTML helpers were smart enough to display the error message and maintain the values for us within the textbox elements:</span></span>

<span data-ttu-id="5ba37-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5ba37-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span></span>

<span data-ttu-id="5ba37-128">这非常有用，但如果我们可以告诉用户在客户端立即获取涉及服务器之前很好。</span><span class="sxs-lookup"><span data-stu-id="5ba37-128">This works great, but it'd be nice if we could tell the user on the client-side, immediately, before the server gets involved.</span></span>

<span data-ttu-id="5ba37-129">让我们来启用 JavaScript 与某些客户端验证。</span><span class="sxs-lookup"><span data-stu-id="5ba37-129">Let's enable some client-side validation with JavaScript.</span></span>

## <a name="adding-client-side-validation"></a><span data-ttu-id="5ba37-130">添加客户端验证</span><span class="sxs-lookup"><span data-stu-id="5ba37-130">Adding Client-Side Validation</span></span>

<span data-ttu-id="5ba37-131">由于我们的 Movie 类已具有一些验证特性，我们将只需将几个 JavaScript 文件添加到我们 Create.aspx 视图模板和添加一行代码以启用客户端验证，才能开始。</span><span class="sxs-lookup"><span data-stu-id="5ba37-131">Since our Movie class already has some validation attributes, we'll just need to add a few JavaScript files to our Create.aspx View template and add a line of code to enable client-side validation to take place.</span></span>

<span data-ttu-id="5ba37-132">从内部 VWD 转我们的电影视图/文件夹并打开 Create.aspx。</span><span class="sxs-lookup"><span data-stu-id="5ba37-132">From within VWD go our Views/Movie folder and open up Create.aspx.</span></span>

<span data-ttu-id="5ba37-133">打开解决方案资源管理器中的脚本文件夹并拖动到中的以下三个脚本&lt;head&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="5ba37-133">Open up the Scripts folder in the Solution Explorer and drag the following three scripts to within the &lt;head&gt; tag.</span></span>

- <span data-ttu-id="5ba37-134">MicrosoftAjax.js</span><span class="sxs-lookup"><span data-stu-id="5ba37-134">MicrosoftAjax.js</span></span>
- <span data-ttu-id="5ba37-135">MicrosoftMvcValidation.js</span><span class="sxs-lookup"><span data-stu-id="5ba37-135">MicrosoftMvcValidation.js</span></span>

<span data-ttu-id="5ba37-136">你想要按此顺序显示这些脚本文件。</span><span class="sxs-lookup"><span data-stu-id="5ba37-136">You want these script files to appear in this order.</span></span>

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

<span data-ttu-id="5ba37-137">此外，添加上述 Html.BeginForm 这一行：</span><span class="sxs-lookup"><span data-stu-id="5ba37-137">Also, add this single line above the Html.BeginForm:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

<span data-ttu-id="5ba37-138">下面是在 IDE 中所示的代码。</span><span class="sxs-lookup"><span data-stu-id="5ba37-138">Here's the code shown within the IDE.</span></span>

<span data-ttu-id="5ba37-139">[![电影-Microsoft Visual Web Developer 2010 速成版 (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5ba37-139">[![Movies - Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span></span>

<span data-ttu-id="5ba37-140">运行应用程序并再次，访问 /Movies/Create 并单击创建而无需输入任何数据。</span><span class="sxs-lookup"><span data-stu-id="5ba37-140">Run your application and visit /Movies/Create again, and click Create without entering any data.</span></span> <span data-ttu-id="5ba37-141">错误消息会立即显示没有页面闪存，我们将与相关联发送数据的情况下按原路返回到服务器。</span><span class="sxs-lookup"><span data-stu-id="5ba37-141">The error messages appear immediately without the page flash that we associate with sending data all the way back to the server.</span></span> <span data-ttu-id="5ba37-142">这是因为 ASP.NET MVC 现在验证的输入上 （使用 JavaScript） 的客户端和服务器上。</span><span class="sxs-lookup"><span data-stu-id="5ba37-142">This is because ASP.NET MVC is now validating the input on both the client (using JavaScript) and on the server.</span></span>

<span data-ttu-id="5ba37-143">[![创建的 Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="5ba37-143">[![Create - Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span></span>

<span data-ttu-id="5ba37-144">这看起来不错 ！</span><span class="sxs-lookup"><span data-stu-id="5ba37-144">This is looking good!</span></span> <span data-ttu-id="5ba37-145">现在让我们添加一个附加列到数据库。</span><span class="sxs-lookup"><span data-stu-id="5ba37-145">Let's now add one additional column to the database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5ba37-146">[上一页](getting-started-with-mvc-part6.md)
> [下一页](getting-started-with-mvc-part8.md)</span><span class="sxs-lookup"><span data-stu-id="5ba37-146">[Previous](getting-started-with-mvc-part6.md)
[Next](getting-started-with-mvc-part8.md)</span></span>
