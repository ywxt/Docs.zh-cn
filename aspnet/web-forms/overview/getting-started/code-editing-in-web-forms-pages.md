---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: 在 Visual Studio 2013 的 ASP.NET Web 窗体的代码编辑 |Microsoft 文档
author: Erikre
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/03/2014
ms.topic: article
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 79b10df04432490d6338dadb8f7ddd36192beb3e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a><span data-ttu-id="3ccad-102">在 Visual Studio 2013 中的代码编辑 ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="3ccad-102">Code Editing ASP.NET Web Forms in Visual Studio 2013</span></span>
====================
<span data-ttu-id="3ccad-103">通过[艾力克 Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="3ccad-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="3ccad-104">在许多 ASP.NET Web 窗体页中，你可以编写在 Visual Basic、 C# 中，或另一种语言的代码。</span><span class="sxs-lookup"><span data-stu-id="3ccad-104">In many ASP.NET Web Form pages, you write code in Visual Basic, C#, or another language.</span></span> <span data-ttu-id="3ccad-105">Visual Studio 中的代码编辑器可帮助您快速编写代码，同时帮助您避免错误。</span><span class="sxs-lookup"><span data-stu-id="3ccad-105">The code editor in Visual Studio can help you write code quickly while helping you avoid errors.</span></span> <span data-ttu-id="3ccad-106">此外，该编辑器还提供使你可以创建可重用的代码的方法来帮助减少你需要执行的工作量。</span><span class="sxs-lookup"><span data-stu-id="3ccad-106">In addition, the editor provides ways for you to create reusable code to help reduce the amount of work you need to do.</span></span>

<span data-ttu-id="3ccad-107">本演练阐释了 Visual Studio 代码编辑器的各种功能。</span><span class="sxs-lookup"><span data-stu-id="3ccad-107">This walkthrough illustrates various features of the Visual Studio code editor.</span></span>

<span data-ttu-id="3ccad-108">在本演练中，你将学会如何执行以下任务：</span><span class="sxs-lookup"><span data-stu-id="3ccad-108">During this walkthrough, you will learn how to:</span></span>

- <span data-ttu-id="3ccad-109">更正内联编码错误。</span><span class="sxs-lookup"><span data-stu-id="3ccad-109">Correct inline coding errors.</span></span>
- <span data-ttu-id="3ccad-110">重构和重命名代码。</span><span class="sxs-lookup"><span data-stu-id="3ccad-110">Refactor and rename code.</span></span>
- <span data-ttu-id="3ccad-111">重命名的变量和对象。</span><span class="sxs-lookup"><span data-stu-id="3ccad-111">Rename variables and objects.</span></span>
- <span data-ttu-id="3ccad-112">插入代码段。</span><span class="sxs-lookup"><span data-stu-id="3ccad-112">Insert code snippets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ccad-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="3ccad-113">Prerequisites</span></span>


<span data-ttu-id="3ccad-114">若要完成本演练，你将需要：</span><span class="sxs-lookup"><span data-stu-id="3ccad-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="3ccad-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="3ccad-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="3ccad-116">自动安装.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="3ccad-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="3ccad-117">Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 for Web 将通常被称为 Visual Studio 在本教程系列整个。</span><span class="sxs-lookup"><span data-stu-id="3ccad-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="3ccad-118">如果你使用的 Visual Studio，本演练假定你所选**Web 开发**设置的集合，首次启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3ccad-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="3ccad-119">有关详细信息，请参阅[如何： 选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3ccad-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

  <span data-ttu-id="3ccad-120">Visual Studio 和 ASP.NET 的介绍，请参阅[在 Visual Studio 2013 中创建一个基本的 ASP.NET 4.5 Web 窗体页面](creating-a-basic-web-forms-page.md)。</span><span class="sxs-lookup"><span data-stu-id="3ccad-120">For an introduction to Visual Studio and ASP.NET, see [Creating a basic ASP.NET 4.5 Web Forms page in Visual Studio 2013](creating-a-basic-web-forms-page.md).</span></span>   
 

## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="3ccad-121">创建 Web 应用程序项目和页面</span><span class="sxs-lookup"><span data-stu-id="3ccad-121">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="3ccad-122">在演练本部分，将创建一个 Web 应用程序项目，并向其添加一个新页。</span><span class="sxs-lookup"><span data-stu-id="3ccad-122">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="3ccad-123">创建 Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="3ccad-123">To create a Web application project</span></span>

1. <span data-ttu-id="3ccad-124">打开 Microsoft Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3ccad-124">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="3ccad-125">在“文件”菜单上，选择“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="3ccad-125">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="3ccad-126">![文件菜单](code-editing-in-web-forms-pages/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3ccad-126">![File Menu](code-editing-in-web-forms-pages/_static/image1.png)</span></span>

    <span data-ttu-id="3ccad-127">此时将出现 “新建项目” 对话框。</span><span class="sxs-lookup"><span data-stu-id="3ccad-127">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="3ccad-128">选择**模板** - &gt; **Visual C#**  - &gt; **Web**左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="3ccad-128">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="3ccad-129">选择**ASP.NET Web 应用程序**中心列中的模板。</span><span class="sxs-lookup"><span data-stu-id="3ccad-129">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="3ccad-130">命名你的项目***BasicWebApp***单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="3ccad-130">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="3ccad-131">![新建项目对话框](code-editing-in-web-forms-pages/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="3ccad-131">![New Project dialog box](code-editing-in-web-forms-pages/_static/image2.png)</span></span>
6. <span data-ttu-id="3ccad-132">接下来，选择**Web 窗体**模板，然后单击**确定**按钮以创建该项目。</span><span class="sxs-lookup"><span data-stu-id="3ccad-132">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="3ccad-133">![新建 ASP.NET 项目对话框](code-editing-in-web-forms-pages/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="3ccad-133">![New ASP.NET Project dialog box](code-editing-in-web-forms-pages/_static/image3.png)</span></span>  

    <span data-ttu-id="3ccad-134">Visual Studio 创建新的项目包含在基于 Web 窗体模板的预构建的功能。</span><span class="sxs-lookup"><span data-stu-id="3ccad-134">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span>


## <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="3ccad-135">创建新的 ASP.NET Web 窗体页</span><span class="sxs-lookup"><span data-stu-id="3ccad-135">Creating a new ASP.NET Web Forms Page</span></span>


<span data-ttu-id="3ccad-136">当你创建新的 Web 窗体应用程序使用**ASP.NET Web 应用程序**项目模板中，Visual Studio 将添加一个名为的 ASP.NET 页 （Web 窗体页） *Default.aspx*，以及为多个其他文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="3ccad-136">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="3ccad-137">你可以使用*Default.aspx*页为 Web 应用程序主页的步骤。</span><span class="sxs-lookup"><span data-stu-id="3ccad-137">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="3ccad-138">但是，对于本演练，你将创建和使用新的页。</span><span class="sxs-lookup"><span data-stu-id="3ccad-138">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="3ccad-139">要添加到 Web 应用程序页</span><span class="sxs-lookup"><span data-stu-id="3ccad-139">To add a page to the Web application</span></span>


1. <span data-ttu-id="3ccad-140">在**解决方案资源管理器**，右键单击 Web 应用程序名称 (在本教程中的应用程序名称**BasicWebSite**)，然后单击**添加** - &gt;**新项**。</span><span class="sxs-lookup"><span data-stu-id="3ccad-140">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="3ccad-141">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="3ccad-141">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="3ccad-142">选择**Visual C#**  - &gt; **Web**左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="3ccad-142">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="3ccad-143">然后，选择**Web 窗体**从中间列表并将其命名*FirstWebPage.aspx*。</span><span class="sxs-lookup"><span data-stu-id="3ccad-143">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="3ccad-144">![添加新项对话框](code-editing-in-web-forms-pages/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="3ccad-144">![Add New Item dialog box](code-editing-in-web-forms-pages/_static/image4.png)</span></span>
3. <span data-ttu-id="3ccad-145">单击**添加**将 Web 窗体页添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="3ccad-145">Click **Add** to add the Web Forms page to your project.</span></span>  
 <span data-ttu-id="3ccad-146">Visual Studio 将创建新的页，并将其打开。</span><span class="sxs-lookup"><span data-stu-id="3ccad-146">Visual Studio creates the new page and opens it.</span></span>
4. <span data-ttu-id="3ccad-147">接下来，将此新的页设置为默认启动页。</span><span class="sxs-lookup"><span data-stu-id="3ccad-147">Next, set this new page as the default startup page.</span></span> <span data-ttu-id="3ccad-148">在**解决方案资源管理器**，右键单击名为的新页*FirstWebPage.aspx*和选择**设为起始页**。</span><span class="sxs-lookup"><span data-stu-id="3ccad-148">In **Solution Explorer**, right-click the new page named *FirstWebPage.aspx* and select **Set As Start Page**.</span></span> <span data-ttu-id="3ccad-149">在下次运行此应用程序以测试我们的进度，你将自动看到此浏览器中的新页。</span><span class="sxs-lookup"><span data-stu-id="3ccad-149">The next time you run this application to test our progress, you will automatically see this new page in the browser.</span></span>


## <a name="correcting-inline-coding-errors"></a><span data-ttu-id="3ccad-150">更正内联编码错误</span><span class="sxs-lookup"><span data-stu-id="3ccad-150">Correcting Inline Coding Errors</span></span>


<span data-ttu-id="3ccad-151">Visual Studio 中的代码编辑器可帮助你避免错误，因为你编写代码，并且如果进行了错误，代码编辑器可帮助你更正此错误。</span><span class="sxs-lookup"><span data-stu-id="3ccad-151">The code editor in Visual Studio helps you to avoid errors as you write code, and if you have made an error, the code editor helps you to correct the error.</span></span> <span data-ttu-id="3ccad-152">在演练本部分，你将编写说明在编辑器中的错误更正功能的代码的行。</span><span class="sxs-lookup"><span data-stu-id="3ccad-152">In this part of the walkthrough, you will write a line of code that illustrate the error correction features in the editor.</span></span>

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a><span data-ttu-id="3ccad-153">若要更正 Visual Studio 中的简单编码错误</span><span class="sxs-lookup"><span data-stu-id="3ccad-153">To correct simple coding errors in Visual Studio</span></span>


1. <span data-ttu-id="3ccad-154">在**设计**视图中，双击空白页后，可以创建的处理程序**负载**页的事件。</span><span class="sxs-lookup"><span data-stu-id="3ccad-154">In **Design** view, double-click the blank page to create a handler for the **Load** event for the page.</span></span>   
   <span data-ttu-id="3ccad-155">你使用事件处理程序仅作为的位置来编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="3ccad-155">You are using the event handler only as a place to write some code.</span></span>
2. <span data-ttu-id="3ccad-156">内部处理程序中，键入以下行，其中包含了错误和按**ENTER**:</span><span class="sxs-lookup"><span data-stu-id="3ccad-156">Inside the handler, type the following line that contains an error and press **ENTER**:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   <span data-ttu-id="3ccad-157">当你按**ENTER**，代码编辑器中将绿色和红色下划线 (通常会调用&quot;波浪&quot;行) 下的代码有问题的区域。</span><span class="sxs-lookup"><span data-stu-id="3ccad-157">When you press **ENTER**, the code editor places green and red underlines (commonly call &quot;squiggly&quot; lines) under areas of the code that have issues.</span></span> <span data-ttu-id="3ccad-158">绿色下划线指示警告。</span><span class="sxs-lookup"><span data-stu-id="3ccad-158">A green underline indicates a warning.</span></span> <span data-ttu-id="3ccad-159">红色下划线指示必须修复错误。</span><span class="sxs-lookup"><span data-stu-id="3ccad-159">A red underline indicates an error that you must fix.</span></span> 

    <span data-ttu-id="3ccad-160">将鼠标指针停留在`myStr`若要查看工具提示，告诉你有关该警告。</span><span class="sxs-lookup"><span data-stu-id="3ccad-160">Hold the mouse pointer over `myStr` to see a tooltip that tells you about the warning.</span></span> <span data-ttu-id="3ccad-161">此外，将鼠标指针悬停红色的下划线，以查看错误消息。</span><span class="sxs-lookup"><span data-stu-id="3ccad-161">Also, hold your mouse pointer over the red underline to see the error message.</span></span>

    <span data-ttu-id="3ccad-162">下图显示带下划线的代码。</span><span class="sxs-lookup"><span data-stu-id="3ccad-162">The following image shows the code with the underlines.</span></span>

    <span data-ttu-id="3ccad-163">![在设计视图中的欢迎文本](code-editing-in-web-forms-pages/_static/image5.png "在设计视图中的欢迎文本")</span><span class="sxs-lookup"><span data-stu-id="3ccad-163">![Welcome text in Design view](code-editing-in-web-forms-pages/_static/image5.png "Welcome text in Design view")</span></span>  
   <span data-ttu-id="3ccad-164">必须通过添加分号修复错误`;`至行尾。</span><span class="sxs-lookup"><span data-stu-id="3ccad-164">The error must be fixed by adding a semicolon `;` to the end of the line.</span></span> <span data-ttu-id="3ccad-165">警告只会通知您，尚未使用`myStr`尚未变量。</span><span class="sxs-lookup"><span data-stu-id="3ccad-165">The warning simply notifies you that you haven't used the `myStr` variable yet.</span></span>  

    > [!NOTE] 
    > 
    > <span data-ttu-id="3ccad-166">查看你当前的代码，通过选择格式 Visual Studio 中的设置**工具** - &gt; **选项** - &gt; **字体和颜色**。</span><span class="sxs-lookup"><span data-stu-id="3ccad-166">You view your current code formatting settings in Visual Studio by selecting **Tools** -&gt; **Options** -&gt; **Fonts and Colors**.</span></span>


## <a name="refactoring-and-renaming"></a><span data-ttu-id="3ccad-167">重构和重命名</span><span class="sxs-lookup"><span data-stu-id="3ccad-167">Refactoring and Renaming</span></span>

<span data-ttu-id="3ccad-168">重构是一种软件方法涉及重构代码以使其更易于理解和维护，同时保留其功能。</span><span class="sxs-lookup"><span data-stu-id="3ccad-168">Refactoring is a software methodology that involves restructuring your code to make it easier to understand and to maintain, while preserving its functionality.</span></span> <span data-ttu-id="3ccad-169">一个简单的示例可能是在从数据库中获取数据的事件处理程序中编写代码。</span><span class="sxs-lookup"><span data-stu-id="3ccad-169">A simple example might be that you write code in an event handler to get data from a database.</span></span> <span data-ttu-id="3ccad-170">开发你的页面，你发现你需要从多个不同的处理程序访问数据。</span><span class="sxs-lookup"><span data-stu-id="3ccad-170">As you develop your page, you discover that you need to access the data from several different handlers.</span></span> <span data-ttu-id="3ccad-171">因此，通过在页中创建数据访问方法，并在处理程序中插入对方法的调用重构页的代码。</span><span class="sxs-lookup"><span data-stu-id="3ccad-171">Therefore, you refactor the page's code by creating a data-access method in the page and inserting calls to the method in the handlers.</span></span>

<span data-ttu-id="3ccad-172">代码编辑器中包括可帮助你执行各种重构任务的工具。</span><span class="sxs-lookup"><span data-stu-id="3ccad-172">The code editor includes tools to help you perform various refactoring tasks.</span></span> <span data-ttu-id="3ccad-173">在本演练中，将使用两个重构的方法： 重命名变量以及提取方法。</span><span class="sxs-lookup"><span data-stu-id="3ccad-173">In this walkthrough, you will work with two refactoring techniques: renaming variables and extracting methods.</span></span> <span data-ttu-id="3ccad-174">其他重构选项包括封装字段、 局部变量提升为方法参数和管理方法参数。</span><span class="sxs-lookup"><span data-stu-id="3ccad-174">Other refactoring options include encapsulating fields, promoting local variables to method parameters, and managing method parameters.</span></span> <span data-ttu-id="3ccad-175">这些重构选项的可用性取决于代码中的位置。</span><span class="sxs-lookup"><span data-stu-id="3ccad-175">The availability of these refactoring options depends on the location in the code.</span></span>

### <a name="refactoring-code"></a><span data-ttu-id="3ccad-176">重构代码</span><span class="sxs-lookup"><span data-stu-id="3ccad-176">Refactoring Code</span></span>

<span data-ttu-id="3ccad-177">常见的重构方案是创建 （提取） 位于另一个成员，如方法的代码中的方法。</span><span class="sxs-lookup"><span data-stu-id="3ccad-177">A common refactoring scenario is to create (extract) a method from code that is inside another member, such as a method.</span></span> <span data-ttu-id="3ccad-178">这会减少原始成员的大小，并使提取的代码可重用。</span><span class="sxs-lookup"><span data-stu-id="3ccad-178">This reduces the size of the original member and makes the extracted code reusable.</span></span>

<span data-ttu-id="3ccad-179">在演练本部分，你将编写一些简单的代码，然后从中提取方法。</span><span class="sxs-lookup"><span data-stu-id="3ccad-179">In this part of the walkthrough, you will write some simple code, and then extract a method from it.</span></span> <span data-ttu-id="3ccad-180">重构支持 C# 中，因此你将创建使用 C# 作为编程语言的页面。</span><span class="sxs-lookup"><span data-stu-id="3ccad-180">Refactoring is supported for C#, so you will create a page that uses C# as its programming language.</span></span>

### <a name="to-extract-a-method-in-a-c-page"></a><span data-ttu-id="3ccad-181">若要提取的 C# 页中的方法</span><span class="sxs-lookup"><span data-stu-id="3ccad-181">To extract a method in a C# page</span></span>

1. <span data-ttu-id="3ccad-182">切换到**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="3ccad-182">Switch to **Design** view.</span></span>
2. <span data-ttu-id="3ccad-183">在**工具箱**，从**标准**选项卡上，拖动[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)拖到页面上的控件。</span><span class="sxs-lookup"><span data-stu-id="3ccad-183">In the **Toolbox**, from the **Standard** tab, drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page.</span></span>
3. <span data-ttu-id="3ccad-184">双击**按钮**控件创建的处理程序其[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件，然后添加以下突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="3ccad-184">Double-click the **Button** control to create a handler for its [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event, and then add the following highlighted code:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   <span data-ttu-id="3ccad-185">该代码创建**ArrayList**对象，使用循环包含值，加载它，然后使用另一个循环显示的内容**ArrayList**对象。</span><span class="sxs-lookup"><span data-stu-id="3ccad-185">The code creates an **ArrayList** object, uses a loop to load it with values, and then uses another loop to display the contents of the **ArrayList** object.</span></span>
4. <span data-ttu-id="3ccad-186">按**CTRL + F5**以运行此页面，然后单击**按钮**若要确保你看到以下输出：</span><span class="sxs-lookup"><span data-stu-id="3ccad-186">Press **CTRL+F5** to run the page, and then click the **button** to make sure that you see the following output:</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. <span data-ttu-id="3ccad-187">返回到代码编辑器中，，然后选择事件处理程序中的的以下行。</span><span class="sxs-lookup"><span data-stu-id="3ccad-187">Return to the code editor, and then select the following lines in the event handler.</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. <span data-ttu-id="3ccad-188">右键单击所选内容，单击**重构**，然后选择**提取方法**。</span><span class="sxs-lookup"><span data-stu-id="3ccad-188">Right-click the selection, click **Refactor**, and then choose **Extract Method**.</span></span> 

    <span data-ttu-id="3ccad-189">**提取方法**对话框随即出现。</span><span class="sxs-lookup"><span data-stu-id="3ccad-189">The **Extract Method** dialog box appears.</span></span>
7. <span data-ttu-id="3ccad-190">在**新方法名称**框中，键入**DisplayArray**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="3ccad-190">In the **New Method Name** box, type **DisplayArray**, and then click **OK**.</span></span> 

    <span data-ttu-id="3ccad-191">代码编辑器中创建一个名为的新方法`DisplayArray`，并将放到中的新方法的调用**单击**循环最初的处理程序。</span><span class="sxs-lookup"><span data-stu-id="3ccad-191">The code editor creates a new method named `DisplayArray`, and puts a call to the new method in the **Click** handler where the loop was originally.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. <span data-ttu-id="3ccad-192">按**CTRL + F5**再次，运行此页并单击**按钮**。</span><span class="sxs-lookup"><span data-stu-id="3ccad-192">Press **CTRL+F5** to run the page again, and click the **button**.</span></span>

    <span data-ttu-id="3ccad-193">此页面的功能相同像以前一样。</span><span class="sxs-lookup"><span data-stu-id="3ccad-193">The page functions the same as it did before.</span></span> <span data-ttu-id="3ccad-194">`DisplayArray`方法现在可以从任何位置的调用中的页类。</span><span class="sxs-lookup"><span data-stu-id="3ccad-194">The `DisplayArray` method can now be call from anywhere in the page class.</span></span>

## <a name="renaming-variables"></a><span data-ttu-id="3ccad-195">重命名变量</span><span class="sxs-lookup"><span data-stu-id="3ccad-195">Renaming Variables</span></span>

<span data-ttu-id="3ccad-196">时要使用变量，以及对象时，你可能想要将其重命名后它们将已在你的代码中引用。</span><span class="sxs-lookup"><span data-stu-id="3ccad-196">When you work with variables, as well as objects, you might want to rename them after they are already referenced in your code.</span></span> <span data-ttu-id="3ccad-197">但是，重命名的变量和对象可以导致中断如果错过了重命名其中一个引用的代码。</span><span class="sxs-lookup"><span data-stu-id="3ccad-197">However, renaming variables and objects can cause the code to break if you miss renaming one of the references.</span></span> <span data-ttu-id="3ccad-198">因此，你可以使用重构来执行重命名。</span><span class="sxs-lookup"><span data-stu-id="3ccad-198">Therefore, you can use refactoring to perform the renaming.</span></span>

### <a name="to-use-refactoring-to-rename-a-variable"></a><span data-ttu-id="3ccad-199">若要使用重构重命名变量</span><span class="sxs-lookup"><span data-stu-id="3ccad-199">To use refactoring to rename a variable</span></span>


1. <span data-ttu-id="3ccad-200">在**单击**事件处理程序中，找到以下行：</span><span class="sxs-lookup"><span data-stu-id="3ccad-200">In the **Click** event handler, locate the following line:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. <span data-ttu-id="3ccad-201">右键单击变量名称`alist`，选择**重构**，然后选择**重命名**。</span><span class="sxs-lookup"><span data-stu-id="3ccad-201">Right-click the variable name `alist`, choose **Refactor**, and then choose **Rename**.</span></span>

    <span data-ttu-id="3ccad-202">**重命名**对话框随即出现。</span><span class="sxs-lookup"><span data-stu-id="3ccad-202">The **Rename** dialog box appears.</span></span>
3. <span data-ttu-id="3ccad-203">在**新名称**框中，键入**ArrayList1**并确保**预览引用更改**选中复选框。</span><span class="sxs-lookup"><span data-stu-id="3ccad-203">In the **New name** box, type **ArrayList1** and make sure the **Preview reference changes** checkbox has been selected.</span></span> <span data-ttu-id="3ccad-204">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="3ccad-204">Then click **OK**.</span></span>

    <span data-ttu-id="3ccad-205">**预览更改**对话框出现，并显示一个树，它包含指向要重命名的变量的所有引用。</span><span class="sxs-lookup"><span data-stu-id="3ccad-205">The **Preview Changes** dialog box appears, and displays a tree that contains all references to the variable that you are renaming.</span></span>
4. <span data-ttu-id="3ccad-206">单击**应用**关闭**预览更改**对话框。</span><span class="sxs-lookup"><span data-stu-id="3ccad-206">Click **Apply** to close the **Preview Changes** dialog box.</span></span>

    <span data-ttu-id="3ccad-207">特定于所选实例引用的变量将重命名。</span><span class="sxs-lookup"><span data-stu-id="3ccad-207">The variables that refer specifically to the instance that you selected are renamed.</span></span> <span data-ttu-id="3ccad-208">但是，请注意，变量`alist`以下行中不会重命名。</span><span class="sxs-lookup"><span data-stu-id="3ccad-208">Note, however, that the variable `alist` in the following line is not renamed.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    <span data-ttu-id="3ccad-209">变量`alist`此行中不重命名，因为它不表示该变量的值相同`alist`你重命名。</span><span class="sxs-lookup"><span data-stu-id="3ccad-209">The variable `alist` in this line is not renamed because it does not represent the same value as the variable `alist` that you renamed.</span></span> <span data-ttu-id="3ccad-210">变量`alist`中`DisplayArray`声明为该方法的局部变量。</span><span class="sxs-lookup"><span data-stu-id="3ccad-210">The variable `alist` in the `DisplayArray` declaration is a local variable for that method.</span></span> <span data-ttu-id="3ccad-211">这表明使用重构重命名变量是不同于只需在编辑器中; 执行查找和替换操作重构重命名变量的了解，它正在使用的变量的语义。</span><span class="sxs-lookup"><span data-stu-id="3ccad-211">This illustrates that using refactoring to rename variables is different than simply performing a find-and-replace action in the editor; refactoring renames variables with knowledge of the semantics of the variable that it is working with.</span></span>


## <a name="inserting-snippets"></a><span data-ttu-id="3ccad-212">插入代码段</span><span class="sxs-lookup"><span data-stu-id="3ccad-212">Inserting Snippets</span></span>

<span data-ttu-id="3ccad-213">由于有很多 Web 窗体开发人员经常需要执行的编码任务，该代码编辑器还提供代码段或预编写的代码块的库。</span><span class="sxs-lookup"><span data-stu-id="3ccad-213">Because there are many coding tasks that Web Forms developers frequently need to perform, the code editor provides a library of snippets, or blocks of prewritten code.</span></span> <span data-ttu-id="3ccad-214">你可以将这些代码段插入你的页面。</span><span class="sxs-lookup"><span data-stu-id="3ccad-214">You can insert these snippets into your page.</span></span>

<span data-ttu-id="3ccad-215">使用 Visual Studio 中的每种语言有中插入代码段的方式的细微差异。</span><span class="sxs-lookup"><span data-stu-id="3ccad-215">Each language that you use in Visual Studio has slight differences in the way you insert code snippets.</span></span> <span data-ttu-id="3ccad-216">有关插入代码段的信息，请参阅[Visual Basic IntelliSense 代码段](https://msdn.microsoft.com/library/18yz4be4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3ccad-216">For information about inserting snippets, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx).</span></span> <span data-ttu-id="3ccad-217">有关插入代码段 Visual C# 中的信息，请参阅[Visual C# 代码片段](https://msdn.microsoft.com/library/z41h7fat.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3ccad-217">For information about inserting snippets in Visual C#, see [Visual C# Code Snippets](https://msdn.microsoft.com/library/z41h7fat.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ccad-218">后续步骤</span><span class="sxs-lookup"><span data-stu-id="3ccad-218">Next Steps</span></span>

<span data-ttu-id="3ccad-219">本演练为更正你的代码中的错误、 代码重构、 重命名变量，和将代码段插入到你的代码演示了 Visual Studio 2010 代码编辑器的基本功能。</span><span class="sxs-lookup"><span data-stu-id="3ccad-219">This walkthrough has illustrated the basic features of the Visual Studio 2010 code editor for correcting errors in your code, refactoring code, renaming variables, and inserting code snippets into your code.</span></span> <span data-ttu-id="3ccad-220">在编辑器中的其他功能可以使快速而简单的应用程序开发。</span><span class="sxs-lookup"><span data-stu-id="3ccad-220">Additional features in the editor can make application development fast and easy.</span></span> <span data-ttu-id="3ccad-221">例如，你可能希望：</span><span class="sxs-lookup"><span data-stu-id="3ccad-221">For example, you might want to:</span></span>

- <span data-ttu-id="3ccad-222">了解有关 IntelliSense，如修改 IntelliSense 选项，管理代码段，以及搜索联机代码段的功能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="3ccad-222">Learn more about the features of IntelliSense, such as modifying IntelliSense options, managing code snippets, and searching for code snippets online.</span></span> <span data-ttu-id="3ccad-223">有关详细信息，请参阅[使用 IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3ccad-223">For more information, see [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx).</span></span>
- <span data-ttu-id="3ccad-224">了解如何创建你自己的代码段。</span><span class="sxs-lookup"><span data-stu-id="3ccad-224">Learn how to create your own code snippets.</span></span> <span data-ttu-id="3ccad-225">有关详细信息，请参阅[创建和使用 IntelliSense 代码段](https://msdn.microsoft.com/library/ms165392.aspx)</span><span class="sxs-lookup"><span data-stu-id="3ccad-225">For more information, see [Creating and Using IntelliSense Code Snippets](https://msdn.microsoft.com/library/ms165392.aspx)</span></span>
- <span data-ttu-id="3ccad-226">了解有关 IntelliSense 代码段，如自定义代码段和故障排除的 Visual Basic 特定功能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="3ccad-226">Learn more about the Visual Basic-specific features of IntelliSense code snippets, such as customizing the snippets and troubleshooting.</span></span> <span data-ttu-id="3ccad-227">有关详细信息，请参阅[Visual Basic IntelliSense 代码段](https://msdn.microsoft.com/library/18yz4be4.aspx)</span><span class="sxs-lookup"><span data-stu-id="3ccad-227">For more information, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx)</span></span>
- <span data-ttu-id="3ccad-228">了解有关 C# 的特定功能的 IntelliSense，例如重构和代码片段。</span><span class="sxs-lookup"><span data-stu-id="3ccad-228">Learn more about the C#-specific features of IntelliSense, such as refactoring and code snippets.</span></span> <span data-ttu-id="3ccad-229">有关详细信息，请参阅[Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3ccad-229">For more information, see [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).</span></span>
