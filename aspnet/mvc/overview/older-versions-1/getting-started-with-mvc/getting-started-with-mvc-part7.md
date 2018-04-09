---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: 将验证添加到模型 |Microsoft 文档
author: shanselman
description: 这是初学者本教程介绍 ASP.NET MVC 的基础知识。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 78dd6bdd81fcb51a3a21a8f1ee12b4b2bfc37db5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="adding-validation-to-the-model"></a><span data-ttu-id="4bc9a-104">添加到模型的验证</span><span class="sxs-lookup"><span data-stu-id="4bc9a-104">Adding Validation to the Model</span></span>
====================
<span data-ttu-id="4bc9a-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="4bc9a-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="4bc9a-106">这是初学者本教程介绍 ASP.NET MVC 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="4bc9a-107">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="4bc9a-108">请访问[ASP.NET MVC 学习中心](../../../index.md)若要查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="4bc9a-109">在本部分中我们将实现启用我们的应用程序中的输入的验证所需的支持。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-109">In this section we are going to implement the support necessary to enable input validation within our application.</span></span> <span data-ttu-id="4bc9a-110">我们将确保我们数据库内容始终是正确的并且在它们尝试并输入影片数据，这是无效时向最终用户提供有用的错误消息。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-110">We'll ensure that our database content is always correct, and provide helpful error messages to end users when they try and enter Movie data which is not valid.</span></span> <span data-ttu-id="4bc9a-111">我们将首先通过将一些验证逻辑添加到影片类。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-111">We'll begin by adding a little validation logic to the Movie class.</span></span>

<span data-ttu-id="4bc9a-112">右键单击模型文件夹，然后选择添加类。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-112">Right click on the Model folder and select Add Class.</span></span> <span data-ttu-id="4bc9a-113">将你类影片。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-113">Name your class Movie.</span></span>

<span data-ttu-id="4bc9a-114">当我们在前面创建电影实体模型时，IDE 将创建电影类。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-114">When we created the Movie Entity Model earlier, the IDE created a Movie class.</span></span> <span data-ttu-id="4bc9a-115">事实上，电影类的一部分，可以在一个文件，部分位于另一个。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-115">In fact, part of the Movie class can be in one file and part in another.</span></span> <span data-ttu-id="4bc9a-116">这称为分部类。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-116">This is called a Partial Class.</span></span> <span data-ttu-id="4bc9a-117">我们将从另一个文件扩展电影类。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-117">We're going to extend the Movie class from another file.</span></span>

<span data-ttu-id="4bc9a-118">我们将使用某些属性，将为系统验证提示创建部分电影类，指向"合作者类"。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-118">We'll create a partial movie class that points to a "buddy class" with some attributes that will give validation hints to the system.</span></span> <span data-ttu-id="4bc9a-119">我们将标题和价格为必选、 标记，还部署价格是在某个特定范围内。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-119">We'll mark the Title and Price as Required, and also insist that the Price be within a certain range.</span></span> <span data-ttu-id="4bc9a-120">右键单击 Models 文件夹，然后选择添加类。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-120">Right click the Models folder and select Add Class.</span></span> <span data-ttu-id="4bc9a-121">将你的类电影，然后单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-121">Name your class Movie and Click the OK button.</span></span> <span data-ttu-id="4bc9a-122">下面是我们部分的电影类看起来类似。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-122">Here's what our partial Movie class looks like.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

<span data-ttu-id="4bc9a-123">重新运行你的应用程序并尝试输入制定价格超过 100 影片。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-123">Re-Run your application and try to enter a movie with a price over 100.</span></span> <span data-ttu-id="4bc9a-124">已提交了表单之后，你将收到错误。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-124">You'll get an error after you've submitted the form.</span></span> <span data-ttu-id="4bc9a-125">错误将捕获在服务器端，并发送窗体后发生。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-125">The error is caught on the server side and occurs after the Form is POSTed.</span></span> <span data-ttu-id="4bc9a-126">请注意如何 ASP.NET MVC 的内置 HTML 帮助器已足够智能，可显示错误消息和维护为我们在文本框中元素的值：</span><span class="sxs-lookup"><span data-stu-id="4bc9a-126">Notice how ASP.NET MVC's built-in HTML helpers were smart enough to display the error message and maintain the values for us within the textbox elements:</span></span>

<span data-ttu-id="4bc9a-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4bc9a-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span></span>

<span data-ttu-id="4bc9a-128">这非常适用，但如果我们无法将告诉用户在客户端立即之前服务器获取涉及, 那就太好。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-128">This works great, but it'd be nice if we could tell the user on the client-side, immediately, before the server gets involved.</span></span>

<span data-ttu-id="4bc9a-129">让我们启用使用 JavaScript 某些客户端验证。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-129">Let's enable some client-side validation with JavaScript.</span></span>

## <a name="adding-client-side-validation"></a><span data-ttu-id="4bc9a-130">添加客户端验证</span><span class="sxs-lookup"><span data-stu-id="4bc9a-130">Adding Client-Side Validation</span></span>

<span data-ttu-id="4bc9a-131">由于我们电影类已有一些验证特性，我们将只需将几个 JavaScript 文件添加到我们 Create.aspx 视图模板和添加一行代码以启用客户端验证做好准备。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-131">Since our Movie class already has some validation attributes, we'll just need to add a few JavaScript files to our Create.aspx View template and add a line of code to enable client-side validation to take place.</span></span>

<span data-ttu-id="4bc9a-132">在中 VWD 转我们视图/电影文件夹，并打开 Create.aspx。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-132">From within VWD go our Views/Movie folder and open up Create.aspx.</span></span>

<span data-ttu-id="4bc9a-133">打开解决方案资源管理器中的脚本文件夹并将其拖到中的以下三个脚本&lt;头&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-133">Open up the Scripts folder in the Solution Explorer and drag the following three scripts to within the &lt;head&gt; tag.</span></span>

- <span data-ttu-id="4bc9a-134">MicrosoftAjax.js</span><span class="sxs-lookup"><span data-stu-id="4bc9a-134">MicrosoftAjax.js</span></span>
- <span data-ttu-id="4bc9a-135">MicrosoftMvcValidation.js</span><span class="sxs-lookup"><span data-stu-id="4bc9a-135">MicrosoftMvcValidation.js</span></span>

<span data-ttu-id="4bc9a-136">你想要按此顺序显示这些脚本文件。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-136">You want these script files to appear in this order.</span></span>

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

<span data-ttu-id="4bc9a-137">此外，将添加 Html.BeginForm 上面这一行：</span><span class="sxs-lookup"><span data-stu-id="4bc9a-137">Also, add this single line above the Html.BeginForm:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

<span data-ttu-id="4bc9a-138">下面是在 IDE 中所示的代码。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-138">Here's the code shown within the IDE.</span></span>

<span data-ttu-id="4bc9a-139">[![电影-Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="4bc9a-139">[![Movies - Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span></span>

<span data-ttu-id="4bc9a-140">运行你的应用程序和再次访问 /Movies/Create 并单击创建而无需输入任何数据。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-140">Run your application and visit /Movies/Create again, and click Create without entering any data.</span></span> <span data-ttu-id="4bc9a-141">错误消息显示立即不带闪存，我们将关联与发送数据的页面一直退回到服务器。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-141">The error messages appear immediately without the page flash that we associate with sending data all the way back to the server.</span></span> <span data-ttu-id="4bc9a-142">这是因为 ASP.NET MVC 现在验证上同时的输入 （使用 JavaScript） 客户端和服务器上。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-142">This is because ASP.NET MVC is now validating the input on both the client (using JavaScript) and on the server.</span></span>

<span data-ttu-id="4bc9a-143">[![创建的 Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="4bc9a-143">[![Create - Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span></span>

<span data-ttu-id="4bc9a-144">这看起来很好 ！</span><span class="sxs-lookup"><span data-stu-id="4bc9a-144">This is looking good!</span></span> <span data-ttu-id="4bc9a-145">让我们现在添加到数据库的一个其他列。</span><span class="sxs-lookup"><span data-stu-id="4bc9a-145">Let's now add one additional column to the database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4bc9a-146">[上一页](getting-started-with-mvc-part6.md)
> [下一页](getting-started-with-mvc-part8.md)</span><span class="sxs-lookup"><span data-stu-id="4bc9a-146">[Previous](getting-started-with-mvc-part6.md)
[Next](getting-started-with-mvc-part8.md)</span></span>
