---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: ASP.NET Web 窗体 Visual Studio 2013 中编辑代码 |Microsoft Docs
author: Erikre
description: ''
ms.author: aspnetcontent
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: c8f0184ffcec0a988dc8bc814e16936c173659c7
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815968"
---
<a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a><span data-ttu-id="e22d9-102">在 Visual Studio 2013 中的代码编辑 ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="e22d9-102">Code Editing ASP.NET Web Forms in Visual Studio 2013</span></span>
====================
<span data-ttu-id="e22d9-103">通过[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="e22d9-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="e22d9-104">在许多 ASP.NET Web 窗体页中，您编写 Visual Basic、 C# 中，或另一种语言中的代码。</span><span class="sxs-lookup"><span data-stu-id="e22d9-104">In many ASP.NET Web Form pages, you write code in Visual Basic, C#, or another language.</span></span> <span data-ttu-id="e22d9-105">Visual Studio 中的代码编辑器可帮助您快速编写代码，同时又能避免错误。</span><span class="sxs-lookup"><span data-stu-id="e22d9-105">The code editor in Visual Studio can help you write code quickly while helping you avoid errors.</span></span> <span data-ttu-id="e22d9-106">此外，该编辑器还提供为您创建可重用代码的方式来帮助减少需要执行的工作量。</span><span class="sxs-lookup"><span data-stu-id="e22d9-106">In addition, the editor provides ways for you to create reusable code to help reduce the amount of work you need to do.</span></span>

<span data-ttu-id="e22d9-107">本演练说明了各种功能的 Visual Studio 代码编辑器。</span><span class="sxs-lookup"><span data-stu-id="e22d9-107">This walkthrough illustrates various features of the Visual Studio code editor.</span></span>

<span data-ttu-id="e22d9-108">在本演练中，你将学会如何执行以下任务：</span><span class="sxs-lookup"><span data-stu-id="e22d9-108">During this walkthrough, you will learn how to:</span></span>

- <span data-ttu-id="e22d9-109">更正内联编码错误。</span><span class="sxs-lookup"><span data-stu-id="e22d9-109">Correct inline coding errors.</span></span>
- <span data-ttu-id="e22d9-110">重构和重命名的代码。</span><span class="sxs-lookup"><span data-stu-id="e22d9-110">Refactor and rename code.</span></span>
- <span data-ttu-id="e22d9-111">重命名的变量和对象。</span><span class="sxs-lookup"><span data-stu-id="e22d9-111">Rename variables and objects.</span></span>
- <span data-ttu-id="e22d9-112">插入代码段。</span><span class="sxs-lookup"><span data-stu-id="e22d9-112">Insert code snippets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e22d9-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="e22d9-113">Prerequisites</span></span>


<span data-ttu-id="e22d9-114">若要完成本演练，你将需要：</span><span class="sxs-lookup"><span data-stu-id="e22d9-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="e22d9-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="e22d9-116">会自动安装.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="e22d9-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="e22d9-117">Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 for Web 将通常称为 Visual Studio 在整个教程系列中。</span><span class="sxs-lookup"><span data-stu-id="e22d9-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="e22d9-118">如果使用的 Visual Studio，本演练假定你所选**Web 开发**的设置集合，首次启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e22d9-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="e22d9-119">有关详细信息，请参阅[如何： 选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

  <span data-ttu-id="e22d9-120">Visual Studio 和 ASP.NET 的介绍，请参阅[在 Visual Studio 2013 中创建一个基本的 ASP.NET 4.5 Web 窗体页面](creating-a-basic-web-forms-page.md)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-120">For an introduction to Visual Studio and ASP.NET, see [Creating a basic ASP.NET 4.5 Web Forms page in Visual Studio 2013](creating-a-basic-web-forms-page.md).</span></span>   
 

## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="e22d9-121">创建 Web 应用程序项目和页面</span><span class="sxs-lookup"><span data-stu-id="e22d9-121">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="e22d9-122">在本演练的此部分中，将创建 Web 应用程序项目，并向其添加一个新页面。</span><span class="sxs-lookup"><span data-stu-id="e22d9-122">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="e22d9-123">若要创建 Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="e22d9-123">To create a Web application project</span></span>

1. <span data-ttu-id="e22d9-124">打开 Microsoft Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e22d9-124">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="e22d9-125">在“文件”菜单上，选择“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="e22d9-125">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="e22d9-126">![文件菜单](code-editing-in-web-forms-pages/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e22d9-126">![File Menu](code-editing-in-web-forms-pages/_static/image1.png)</span></span>

    <span data-ttu-id="e22d9-127">此时将出现 “新建项目” 对话框。</span><span class="sxs-lookup"><span data-stu-id="e22d9-127">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="e22d9-128">选择**模板** - &gt; **Visual C#**  - &gt; **Web**在左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="e22d9-128">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="e22d9-129">选择**ASP.NET Web 应用程序**在中心列中的模板。</span><span class="sxs-lookup"><span data-stu-id="e22d9-129">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="e22d9-130">将项目命名***BasicWebApp***然后单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="e22d9-130">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="e22d9-131">![新建项目对话框](code-editing-in-web-forms-pages/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="e22d9-131">![New Project dialog box](code-editing-in-web-forms-pages/_static/image2.png)</span></span>
6. <span data-ttu-id="e22d9-132">接下来，选择**Web 窗体**模板，然后单击**确定**按钮创建项目。</span><span class="sxs-lookup"><span data-stu-id="e22d9-132">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="e22d9-133">![新建 ASP.NET 项目对话框](code-editing-in-web-forms-pages/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e22d9-133">![New ASP.NET Project dialog box](code-editing-in-web-forms-pages/_static/image3.png)</span></span>  

    <span data-ttu-id="e22d9-134">Visual Studio 创建新的项目，包括基于 Web 窗体模板的预生成的功能。</span><span class="sxs-lookup"><span data-stu-id="e22d9-134">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span>


## <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="e22d9-135">创建新的 ASP.NET Web 窗体页</span><span class="sxs-lookup"><span data-stu-id="e22d9-135">Creating a new ASP.NET Web Forms Page</span></span>


<span data-ttu-id="e22d9-136">当您创建新的 Web 窗体应用程序使用**ASP.NET Web 应用程序**项目模板，Visual Studio 将添加名为的 ASP.NET 页 （Web 窗体页） *Default.aspx*，以及其他多个文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="e22d9-136">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="e22d9-137">可以使用*Default.aspx*为 Web 应用程序主页的页。</span><span class="sxs-lookup"><span data-stu-id="e22d9-137">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="e22d9-138">但是，对于本演练中，将创建和使用新的页面。</span><span class="sxs-lookup"><span data-stu-id="e22d9-138">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="e22d9-139">若要添加到 Web 应用程序页</span><span class="sxs-lookup"><span data-stu-id="e22d9-139">To add a page to the Web application</span></span>


1. <span data-ttu-id="e22d9-140">在中**解决方案资源管理器**，右键单击 Web 应用程序名称 (在本教程中的应用程序名称是**BasicWebSite**)，然后单击**添加** - &gt;**新项**。</span><span class="sxs-lookup"><span data-stu-id="e22d9-140">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="e22d9-141">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="e22d9-141">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="e22d9-142">选择**Visual C#**  - &gt; **Web**在左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="e22d9-142">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="e22d9-143">然后，选择**Web 窗体**从中间列表并将其命名*FirstWebPage.aspx*。</span><span class="sxs-lookup"><span data-stu-id="e22d9-143">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="e22d9-144">![添加新项对话框](code-editing-in-web-forms-pages/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="e22d9-144">![Add New Item dialog box](code-editing-in-web-forms-pages/_static/image4.png)</span></span>
3. <span data-ttu-id="e22d9-145">单击**添加**将 Web 窗体页添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="e22d9-145">Click **Add** to add the Web Forms page to your project.</span></span>  
 <span data-ttu-id="e22d9-146">Visual Studio 创建新页面，并将其打开。</span><span class="sxs-lookup"><span data-stu-id="e22d9-146">Visual Studio creates the new page and opens it.</span></span>
4. <span data-ttu-id="e22d9-147">接下来，将此新的页设置为默认启动页。</span><span class="sxs-lookup"><span data-stu-id="e22d9-147">Next, set this new page as the default startup page.</span></span> <span data-ttu-id="e22d9-148">在中**解决方案资源管理器**，右键单击名为的新页*FirstWebPage.aspx* ，然后选择**设为起始页**。</span><span class="sxs-lookup"><span data-stu-id="e22d9-148">In **Solution Explorer**, right-click the new page named *FirstWebPage.aspx* and select **Set As Start Page**.</span></span> <span data-ttu-id="e22d9-149">在下次运行此应用程序以测试我们的进度，将会自动看到此新页在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="e22d9-149">The next time you run this application to test our progress, you will automatically see this new page in the browser.</span></span>


## <a name="correcting-inline-coding-errors"></a><span data-ttu-id="e22d9-150">更正内联编码错误</span><span class="sxs-lookup"><span data-stu-id="e22d9-150">Correcting Inline Coding Errors</span></span>


<span data-ttu-id="e22d9-151">Visual Studio 中的代码编辑器可帮助你避免错误，因为你编写代码，并且进行了错误，代码编辑器可帮助你更正此错误。</span><span class="sxs-lookup"><span data-stu-id="e22d9-151">The code editor in Visual Studio helps you to avoid errors as you write code, and if you have made an error, the code editor helps you to correct the error.</span></span> <span data-ttu-id="e22d9-152">在本演练的此部分中，您将编写一行代码，用于演示在编辑器中的错误更正功能。</span><span class="sxs-lookup"><span data-stu-id="e22d9-152">In this part of the walkthrough, you will write a line of code that illustrate the error correction features in the editor.</span></span>

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a><span data-ttu-id="e22d9-153">若要更正 Visual Studio 中的简单编码错误</span><span class="sxs-lookup"><span data-stu-id="e22d9-153">To correct simple coding errors in Visual Studio</span></span>


1. <span data-ttu-id="e22d9-154">在中**设计**视图中，双击空白页后，可以创建一个处理程序**负载**事件页。</span><span class="sxs-lookup"><span data-stu-id="e22d9-154">In **Design** view, double-click the blank page to create a handler for the **Load** event for the page.</span></span>   
   <span data-ttu-id="e22d9-155">使用仅作为一个位置的事件处理程序编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="e22d9-155">You are using the event handler only as a place to write some code.</span></span>
2. <span data-ttu-id="e22d9-156">在处理程序中，键入以下行，其中包含了错误并按**ENTER**:</span><span class="sxs-lookup"><span data-stu-id="e22d9-156">Inside the handler, type the following line that contains an error and press **ENTER**:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   <span data-ttu-id="e22d9-157">当您按下**ENTER**，在代码编辑器将绿色和红色下划线 (通常会调用&quot;波浪&quot;行) 下的代码有问题的区域。</span><span class="sxs-lookup"><span data-stu-id="e22d9-157">When you press **ENTER**, the code editor places green and red underlines (commonly call &quot;squiggly&quot; lines) under areas of the code that have issues.</span></span> <span data-ttu-id="e22d9-158">绿色下划线指示警告。</span><span class="sxs-lookup"><span data-stu-id="e22d9-158">A green underline indicates a warning.</span></span> <span data-ttu-id="e22d9-159">一条红色下划线指示一个错误，则必须修复。</span><span class="sxs-lookup"><span data-stu-id="e22d9-159">A red underline indicates an error that you must fix.</span></span> 

    <span data-ttu-id="e22d9-160">将鼠标指针停留在`myStr`以查看工具提示，告诉你有关该警告。</span><span class="sxs-lookup"><span data-stu-id="e22d9-160">Hold the mouse pointer over `myStr` to see a tooltip that tells you about the warning.</span></span> <span data-ttu-id="e22d9-161">此外，将鼠标指针悬停以查看错误消息的红色下划线。</span><span class="sxs-lookup"><span data-stu-id="e22d9-161">Also, hold your mouse pointer over the red underline to see the error message.</span></span>

    <span data-ttu-id="e22d9-162">下图显示了带下划线的代码。</span><span class="sxs-lookup"><span data-stu-id="e22d9-162">The following image shows the code with the underlines.</span></span>

    <span data-ttu-id="e22d9-163">![在设计视图中的欢迎文本](code-editing-in-web-forms-pages/_static/image5.png "在设计视图中的欢迎文本")</span><span class="sxs-lookup"><span data-stu-id="e22d9-163">![Welcome text in Design view](code-editing-in-web-forms-pages/_static/image5.png "Welcome text in Design view")</span></span>  
   <span data-ttu-id="e22d9-164">必须通过添加分号来解决该错误`;`至行尾。</span><span class="sxs-lookup"><span data-stu-id="e22d9-164">The error must be fixed by adding a semicolon `;` to the end of the line.</span></span> <span data-ttu-id="e22d9-165">此警告只是通知尚未使用过`myStr`尚未变量。</span><span class="sxs-lookup"><span data-stu-id="e22d9-165">The warning simply notifies you that you haven't used the `myStr` variable yet.</span></span>  

    > [!NOTE] 
    > 
    > <span data-ttu-id="e22d9-166">查看当前代码格式设置在 Visual Studio 中的通过选择**工具** - &gt; **选项** - &gt; **字体和颜色**。</span><span class="sxs-lookup"><span data-stu-id="e22d9-166">You view your current code formatting settings in Visual Studio by selecting **Tools** -&gt; **Options** -&gt; **Fonts and Colors**.</span></span>


## <a name="refactoring-and-renaming"></a><span data-ttu-id="e22d9-167">重构和重命名</span><span class="sxs-lookup"><span data-stu-id="e22d9-167">Refactoring and Renaming</span></span>

<span data-ttu-id="e22d9-168">重构是一种软件方法涉及重构代码，使其更易于理解和维护，同时保留其功能。</span><span class="sxs-lookup"><span data-stu-id="e22d9-168">Refactoring is a software methodology that involves restructuring your code to make it easier to understand and to maintain, while preserving its functionality.</span></span> <span data-ttu-id="e22d9-169">一个简单的示例可能是从数据库获取数据的事件处理程序中编写代码。</span><span class="sxs-lookup"><span data-stu-id="e22d9-169">A simple example might be that you write code in an event handler to get data from a database.</span></span> <span data-ttu-id="e22d9-170">开发您的页面时，您发现您需要从多个不同的处理程序访问数据。</span><span class="sxs-lookup"><span data-stu-id="e22d9-170">As you develop your page, you discover that you need to access the data from several different handlers.</span></span> <span data-ttu-id="e22d9-171">因此，通过在页面中创建数据访问方法并将对方法的调用插入的处理程序中重构页面的代码。</span><span class="sxs-lookup"><span data-stu-id="e22d9-171">Therefore, you refactor the page's code by creating a data-access method in the page and inserting calls to the method in the handlers.</span></span>

<span data-ttu-id="e22d9-172">在代码编辑器包括可帮助你执行各种任务，重构工具。</span><span class="sxs-lookup"><span data-stu-id="e22d9-172">The code editor includes tools to help you perform various refactoring tasks.</span></span> <span data-ttu-id="e22d9-173">在本演练中，将使用两种重构的方法： 重命名变量和提取方法。</span><span class="sxs-lookup"><span data-stu-id="e22d9-173">In this walkthrough, you will work with two refactoring techniques: renaming variables and extracting methods.</span></span> <span data-ttu-id="e22d9-174">其他重构选项包括封装字段、 局部变量提升为方法参数，以及管理方法参数。</span><span class="sxs-lookup"><span data-stu-id="e22d9-174">Other refactoring options include encapsulating fields, promoting local variables to method parameters, and managing method parameters.</span></span> <span data-ttu-id="e22d9-175">这些重构选项的可用性取决于代码中的位置。</span><span class="sxs-lookup"><span data-stu-id="e22d9-175">The availability of these refactoring options depends on the location in the code.</span></span>

### <a name="refactoring-code"></a><span data-ttu-id="e22d9-176">重构代码</span><span class="sxs-lookup"><span data-stu-id="e22d9-176">Refactoring Code</span></span>

<span data-ttu-id="e22d9-177">常见的重构方案是创建 （提取） 从另一个成员，如方法内部的代码的方法。</span><span class="sxs-lookup"><span data-stu-id="e22d9-177">A common refactoring scenario is to create (extract) a method from code that is inside another member, such as a method.</span></span> <span data-ttu-id="e22d9-178">这会减少原始成员的大小，并使提取的代码可重用。</span><span class="sxs-lookup"><span data-stu-id="e22d9-178">This reduces the size of the original member and makes the extracted code reusable.</span></span>

<span data-ttu-id="e22d9-179">在本演练的此部分中，将编写一些简单代码，，然后从其提取方法。</span><span class="sxs-lookup"><span data-stu-id="e22d9-179">In this part of the walkthrough, you will write some simple code, and then extract a method from it.</span></span> <span data-ttu-id="e22d9-180">重构支持 C# 中，因此将创建使用 C# 作为编程语言的网页。</span><span class="sxs-lookup"><span data-stu-id="e22d9-180">Refactoring is supported for C#, so you will create a page that uses C# as its programming language.</span></span>

### <a name="to-extract-a-method-in-a-c-page"></a><span data-ttu-id="e22d9-181">若要提取的 C# 页面中的方法</span><span class="sxs-lookup"><span data-stu-id="e22d9-181">To extract a method in a C# page</span></span>

1. <span data-ttu-id="e22d9-182">切换到**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="e22d9-182">Switch to **Design** view.</span></span>
2. <span data-ttu-id="e22d9-183">在中**工具箱**，从**标准**选项卡上，拖动[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件拖到页面。</span><span class="sxs-lookup"><span data-stu-id="e22d9-183">In the **Toolbox**, from the **Standard** tab, drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page.</span></span>
3. <span data-ttu-id="e22d9-184">双击**按钮**控件创建的处理程序及其[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件，然后添加以下突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="e22d9-184">Double-click the **Button** control to create a handler for its [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event, and then add the following highlighted code:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   <span data-ttu-id="e22d9-185">该代码会创建**ArrayList**对象，使用循环加载具有值，然后再使用另一个循环中显示的内容**ArrayList**对象。</span><span class="sxs-lookup"><span data-stu-id="e22d9-185">The code creates an **ArrayList** object, uses a loop to load it with values, and then uses another loop to display the contents of the **ArrayList** object.</span></span>
4. <span data-ttu-id="e22d9-186">按**CTRL + F5**以运行此页面，然后单击**按钮**以确保你看到以下输出：</span><span class="sxs-lookup"><span data-stu-id="e22d9-186">Press **CTRL+F5** to run the page, and then click the **button** to make sure that you see the following output:</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. <span data-ttu-id="e22d9-187">返回到代码编辑器，然后选择事件处理程序中的的以下行。</span><span class="sxs-lookup"><span data-stu-id="e22d9-187">Return to the code editor, and then select the following lines in the event handler.</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. <span data-ttu-id="e22d9-188">右键单击所选内容中，单击**重构**，然后选择**提取方法**。</span><span class="sxs-lookup"><span data-stu-id="e22d9-188">Right-click the selection, click **Refactor**, and then choose **Extract Method**.</span></span> 

    <span data-ttu-id="e22d9-189">**提取方法**对话框随即出现。</span><span class="sxs-lookup"><span data-stu-id="e22d9-189">The **Extract Method** dialog box appears.</span></span>
7. <span data-ttu-id="e22d9-190">在中**新的方法名称**框中，键入**DisplayArray**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="e22d9-190">In the **New Method Name** box, type **DisplayArray**, and then click **OK**.</span></span> 

    <span data-ttu-id="e22d9-191">在代码编辑器创建名为的新方法`DisplayArray`，并将对中的新方法的调用放**单击**循环最初的处理程序。</span><span class="sxs-lookup"><span data-stu-id="e22d9-191">The code editor creates a new method named `DisplayArray`, and puts a call to the new method in the **Click** handler where the loop was originally.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. <span data-ttu-id="e22d9-192">按**CTRL + F5**页上再次运行，并单击**按钮**。</span><span class="sxs-lookup"><span data-stu-id="e22d9-192">Press **CTRL+F5** to run the page again, and click the **button**.</span></span>

    <span data-ttu-id="e22d9-193">此页面的功能相同就像以前一样。</span><span class="sxs-lookup"><span data-stu-id="e22d9-193">The page functions the same as it did before.</span></span> <span data-ttu-id="e22d9-194">`DisplayArray`方法现在可以从任何位置调用页类中。</span><span class="sxs-lookup"><span data-stu-id="e22d9-194">The `DisplayArray` method can now be call from anywhere in the page class.</span></span>

## <a name="renaming-variables"></a><span data-ttu-id="e22d9-195">重命名变量</span><span class="sxs-lookup"><span data-stu-id="e22d9-195">Renaming Variables</span></span>

<span data-ttu-id="e22d9-196">使用变量，以及对象时，你可能想要重命名它们后它们已在代码中引用。</span><span class="sxs-lookup"><span data-stu-id="e22d9-196">When you work with variables, as well as objects, you might want to rename them after they are already referenced in your code.</span></span> <span data-ttu-id="e22d9-197">但是，重命名的变量和对象可能导致代码中断如果错过了重命名其中一个引用。</span><span class="sxs-lookup"><span data-stu-id="e22d9-197">However, renaming variables and objects can cause the code to break if you miss renaming one of the references.</span></span> <span data-ttu-id="e22d9-198">因此，您可以使用重构来执行重命名。</span><span class="sxs-lookup"><span data-stu-id="e22d9-198">Therefore, you can use refactoring to perform the renaming.</span></span>

### <a name="to-use-refactoring-to-rename-a-variable"></a><span data-ttu-id="e22d9-199">若要使用重构重命名变量</span><span class="sxs-lookup"><span data-stu-id="e22d9-199">To use refactoring to rename a variable</span></span>


1. <span data-ttu-id="e22d9-200">在中**单击**事件处理程序中，找到以下行：</span><span class="sxs-lookup"><span data-stu-id="e22d9-200">In the **Click** event handler, locate the following line:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. <span data-ttu-id="e22d9-201">右键单击变量名`alist`，选择**重构**，然后选择**重命名**。</span><span class="sxs-lookup"><span data-stu-id="e22d9-201">Right-click the variable name `alist`, choose **Refactor**, and then choose **Rename**.</span></span>

    <span data-ttu-id="e22d9-202">**重命名**对话框随即出现。</span><span class="sxs-lookup"><span data-stu-id="e22d9-202">The **Rename** dialog box appears.</span></span>
3. <span data-ttu-id="e22d9-203">在中**新的名称**框中，键入**ArrayList1** ，并确保**预览引用更改**选中复选框。</span><span class="sxs-lookup"><span data-stu-id="e22d9-203">In the **New name** box, type **ArrayList1** and make sure the **Preview reference changes** checkbox has been selected.</span></span> <span data-ttu-id="e22d9-204">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="e22d9-204">Then click **OK**.</span></span>

    <span data-ttu-id="e22d9-205">**预览更改**对话框随即出现，并显示一个树，它包含要重命名的变量对所有引用。</span><span class="sxs-lookup"><span data-stu-id="e22d9-205">The **Preview Changes** dialog box appears, and displays a tree that contains all references to the variable that you are renaming.</span></span>
4. <span data-ttu-id="e22d9-206">单击**Apply**以关闭**预览更改**对话框。</span><span class="sxs-lookup"><span data-stu-id="e22d9-206">Click **Apply** to close the **Preview Changes** dialog box.</span></span>

    <span data-ttu-id="e22d9-207">特定于所选实例引用的变量进行重命名。</span><span class="sxs-lookup"><span data-stu-id="e22d9-207">The variables that refer specifically to the instance that you selected are renamed.</span></span> <span data-ttu-id="e22d9-208">但请注意，该变量`alist`以下行中未重命名。</span><span class="sxs-lookup"><span data-stu-id="e22d9-208">Note, however, that the variable `alist` in the following line is not renamed.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    <span data-ttu-id="e22d9-209">在变量`alist`此行中不重命名，因为它不表示相同的值与变量`alist`您重命名为。</span><span class="sxs-lookup"><span data-stu-id="e22d9-209">The variable `alist` in this line is not renamed because it does not represent the same value as the variable `alist` that you renamed.</span></span> <span data-ttu-id="e22d9-210">在变量`alist`在`DisplayArray`声明为该方法的局部变量。</span><span class="sxs-lookup"><span data-stu-id="e22d9-210">The variable `alist` in the `DisplayArray` declaration is a local variable for that method.</span></span> <span data-ttu-id="e22d9-211">这说明了使用重构重命名变量是不同于只需在编辑器中执行查找和替换操作了解自己正在使用的变量的语义与重构重命名变量。</span><span class="sxs-lookup"><span data-stu-id="e22d9-211">This illustrates that using refactoring to rename variables is different than simply performing a find-and-replace action in the editor; refactoring renames variables with knowledge of the semantics of the variable that it is working with.</span></span>


## <a name="inserting-snippets"></a><span data-ttu-id="e22d9-212">插入代码段</span><span class="sxs-lookup"><span data-stu-id="e22d9-212">Inserting Snippets</span></span>

<span data-ttu-id="e22d9-213">由于有许多 Web 窗体开发人员经常需要执行的编码任务，代码编辑器提供了一个库的代码段或预先编写的代码块。</span><span class="sxs-lookup"><span data-stu-id="e22d9-213">Because there are many coding tasks that Web Forms developers frequently need to perform, the code editor provides a library of snippets, or blocks of prewritten code.</span></span> <span data-ttu-id="e22d9-214">可以将这些代码段插入您的页面。</span><span class="sxs-lookup"><span data-stu-id="e22d9-214">You can insert these snippets into your page.</span></span>

<span data-ttu-id="e22d9-215">在 Visual Studio 中使用每种语言已插入代码段的方式略有差异。</span><span class="sxs-lookup"><span data-stu-id="e22d9-215">Each language that you use in Visual Studio has slight differences in the way you insert code snippets.</span></span> <span data-ttu-id="e22d9-216">有关插入代码段的信息，请参阅[Visual Basic IntelliSense 代码段](https://msdn.microsoft.com/library/18yz4be4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-216">For information about inserting snippets, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx).</span></span> <span data-ttu-id="e22d9-217">有关插入代码段 Visual C# 中的信息，请参阅[Visual C# 代码片段](https://msdn.microsoft.com/library/z41h7fat.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-217">For information about inserting snippets in Visual C#, see [Visual C# Code Snippets](https://msdn.microsoft.com/library/z41h7fat.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e22d9-218">后续步骤</span><span class="sxs-lookup"><span data-stu-id="e22d9-218">Next Steps</span></span>

<span data-ttu-id="e22d9-219">本演练为更正代码中的错误、 重构代码、 重命名变量，并将代码段插入到你的代码演示了 Visual Studio 2010 代码编辑器的基本功能。</span><span class="sxs-lookup"><span data-stu-id="e22d9-219">This walkthrough has illustrated the basic features of the Visual Studio 2010 code editor for correcting errors in your code, refactoring code, renaming variables, and inserting code snippets into your code.</span></span> <span data-ttu-id="e22d9-220">在编辑器中的其他功能可以使应用程序开发快速而简单的。</span><span class="sxs-lookup"><span data-stu-id="e22d9-220">Additional features in the editor can make application development fast and easy.</span></span> <span data-ttu-id="e22d9-221">例如，你可能希望：</span><span class="sxs-lookup"><span data-stu-id="e22d9-221">For example, you might want to:</span></span>

- <span data-ttu-id="e22d9-222">详细了解 IntelliSense，如修改 IntelliSense 选项、 管理代码段，以及搜索代码代码段的功能。</span><span class="sxs-lookup"><span data-stu-id="e22d9-222">Learn more about the features of IntelliSense, such as modifying IntelliSense options, managing code snippets, and searching for code snippets online.</span></span> <span data-ttu-id="e22d9-223">有关详细信息，请参阅[使用 IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-223">For more information, see [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx).</span></span>
- <span data-ttu-id="e22d9-224">了解如何创建你自己的代码段。</span><span class="sxs-lookup"><span data-stu-id="e22d9-224">Learn how to create your own code snippets.</span></span> <span data-ttu-id="e22d9-225">有关详细信息，请参阅[创建和使用 IntelliSense 代码段](https://msdn.microsoft.com/library/ms165392.aspx)</span><span class="sxs-lookup"><span data-stu-id="e22d9-225">For more information, see [Creating and Using IntelliSense Code Snippets](https://msdn.microsoft.com/library/ms165392.aspx)</span></span>
- <span data-ttu-id="e22d9-226">了解有关 IntelliSense 代码段，如自定义代码段和故障排除的特定于 Visual Basic 的功能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e22d9-226">Learn more about the Visual Basic-specific features of IntelliSense code snippets, such as customizing the snippets and troubleshooting.</span></span> <span data-ttu-id="e22d9-227">有关详细信息，请参阅[Visual Basic IntelliSense 代码段](https://msdn.microsoft.com/library/18yz4be4.aspx)</span><span class="sxs-lookup"><span data-stu-id="e22d9-227">For more information, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx)</span></span>
- <span data-ttu-id="e22d9-228">了解有关 C# 的详细信息-的 IntelliSense、 重构和代码片段等的特定功能。</span><span class="sxs-lookup"><span data-stu-id="e22d9-228">Learn more about the C#-specific features of IntelliSense, such as refactoring and code snippets.</span></span> <span data-ttu-id="e22d9-229">有关详细信息，请参阅[Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-229">For more information, see [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).</span></span>
