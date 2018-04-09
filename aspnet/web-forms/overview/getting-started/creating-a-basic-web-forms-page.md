---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: 创建一个基本的 ASP.NET 4.5 Web 窗体页在 Visual Studio 2013 |Microsoft 文档
author: Erikre
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/03/2014
ms.topic: article
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: 0dbd3063c9be3564637fad34e60f62c1662dcc07
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="creating-a-basic-aspnet-45-web-forms-page-in-visual-studio-2013"></a><span data-ttu-id="79e9e-102">创建一个基本的 ASP.NET 4.5 Web 窗体页在 Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="79e9e-102">Creating a Basic ASP.NET 4.5 Web Forms Page in Visual Studio 2013</span></span>
====================
<span data-ttu-id="79e9e-103">通过[艾力克 Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="79e9e-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="79e9e-104">本演练为您提供的简介中的 Web 开发环境[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)并在[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="79e9e-104">This walkthrough provides you with an introduction to the Web development environment in [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) and in [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="79e9e-105">本演练指导您完成创建简单的 ASP.NET Web 窗体页，并阐释的创建一个新页面、 添加控件，以及编写代码的基本技术。</span><span class="sxs-lookup"><span data-stu-id="79e9e-105">This walkthrough guides you through creating a simple ASP.NET Web Forms page and illustrates the basic techniques of creating a new page, adding controls, and writing code.</span></span>

<span data-ttu-id="79e9e-106">本演练涉及以下任务：</span><span class="sxs-lookup"><span data-stu-id="79e9e-106">Tasks illustrated in this walkthrough include:</span></span>

- <span data-ttu-id="79e9e-107">创建文件系统 Web 窗体应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="79e9e-107">Creating a file system Web Forms application project.</span></span>
- <span data-ttu-id="79e9e-108">您熟悉 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="79e9e-108">Familiarizing yourself with Visual Studio.</span></span>
- <span data-ttu-id="79e9e-109">创建 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="79e9e-109">Creating an ASP.NET page.</span></span>
- <span data-ttu-id="79e9e-110">添加控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-110">Adding controls.</span></span>
- <span data-ttu-id="79e9e-111">添加事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="79e9e-111">Adding event handlers.</span></span>
- <span data-ttu-id="79e9e-112">运行和测试页上，从 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="79e9e-112">Running and testing a page from Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79e9e-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="79e9e-113">Prerequisites</span></span>


<span data-ttu-id="79e9e-114">若要完成本演练，你将需要：</span><span class="sxs-lookup"><span data-stu-id="79e9e-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="79e9e-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="79e9e-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="79e9e-116">自动安装.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="79e9e-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="79e9e-117">Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 for Web 将通常被称为 Visual Studio 在本教程系列整个。</span><span class="sxs-lookup"><span data-stu-id="79e9e-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="79e9e-118">如果你使用的 Visual Studio，本演练假定你所选**Web 开发**设置的集合，首次启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="79e9e-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="79e9e-119">有关详细信息，请参阅[如何： 选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="79e9e-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>


## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="79e9e-120">创建 Web 应用程序项目和页面</span><span class="sxs-lookup"><span data-stu-id="79e9e-120">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="79e9e-121">在演练本部分，将创建一个 Web 应用程序项目，并向其添加一个新页。</span><span class="sxs-lookup"><span data-stu-id="79e9e-121">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span> <span data-ttu-id="79e9e-122">你还将添加 HTML 文本，并在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="79e9e-122">You will also add HTML text and run the page in your browser.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="79e9e-123">创建 Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="79e9e-123">To create a Web application project</span></span>

1. <span data-ttu-id="79e9e-124">打开 Microsoft Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="79e9e-124">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="79e9e-125">在“文件”菜单上，选择“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="79e9e-125">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="79e9e-126">![文件菜单](creating-a-basic-web-forms-page/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="79e9e-126">![File Menu](creating-a-basic-web-forms-page/_static/image1.png)</span></span>

    <span data-ttu-id="79e9e-127">此时将出现 “新建项目” 对话框。</span><span class="sxs-lookup"><span data-stu-id="79e9e-127">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="79e9e-128">选择**模板** - &gt; **Visual C#**  - &gt; **Web**左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="79e9e-128">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="79e9e-129">选择**ASP.NET Web 应用程序**中心列中的模板。</span><span class="sxs-lookup"><span data-stu-id="79e9e-129">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="79e9e-130">命名你的项目***BasicWebApp***单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="79e9e-130">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="79e9e-131">![新建项目对话框](creating-a-basic-web-forms-page/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="79e9e-131">![New Project dialog box](creating-a-basic-web-forms-page/_static/image2.png)</span></span>
6. <span data-ttu-id="79e9e-132">接下来，选择**Web 窗体**模板，然后单击**确定**按钮以创建该项目。</span><span class="sxs-lookup"><span data-stu-id="79e9e-132">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="79e9e-133">![新建 ASP.NET 项目对话框](creating-a-basic-web-forms-page/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="79e9e-133">![New ASP.NET Project dialog box](creating-a-basic-web-forms-page/_static/image3.png)</span></span>  

    <span data-ttu-id="79e9e-134">Visual Studio 创建新的项目包含在基于 Web 窗体模板的预构建的功能。</span><span class="sxs-lookup"><span data-stu-id="79e9e-134">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span> <span data-ttu-id="79e9e-135">它不仅可为你提供*Home.aspx*页上， *About.aspx*页上， *Contact.aspx*页上，但还包括成员资格功能注册用户和保存其凭据，以便他们可以登录到你的网站。</span><span class="sxs-lookup"><span data-stu-id="79e9e-135">It not only provides you with a *Home.aspx* page, an *About.aspx* page, a *Contact.aspx* page, but also includes membership functionality that registers users and saves their credentials so that they can log in to your website.</span></span> <span data-ttu-id="79e9e-136">创建一个新页后，默认情况下 Visual Studio 将显示中的页**源**视图中，可以看到此页的 HTML 元素的位置。</span><span class="sxs-lookup"><span data-stu-id="79e9e-136">When a new page is created, by default Visual Studio displays the page in **Source** view, where you can see the page's HTML elements.</span></span> <span data-ttu-id="79e9e-137">下图显示将在中看到的内容**源**查看如果创建一个名为的新 Web 页*BasicWebApp.aspx*。</span><span class="sxs-lookup"><span data-stu-id="79e9e-137">The following illustration shows what you would see in **Source** view if you created a new Web page named *BasicWebApp.aspx*.</span></span>  
    <span data-ttu-id="79e9e-138">![源视图](creating-a-basic-web-forms-page/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="79e9e-138">![Source View](creating-a-basic-web-forms-page/_static/image4.png)</span></span>


### <a name="a-tour-of-the-visual-studio-web-development-environment"></a><span data-ttu-id="79e9e-139">介绍的 Visual Studio Web 开发环境</span><span class="sxs-lookup"><span data-stu-id="79e9e-139">A Tour of the Visual Studio Web Development Environment</span></span>


<span data-ttu-id="79e9e-140">通过修改页在继续之前，它可用于熟悉 Visual Studio 开发环境。</span><span class="sxs-lookup"><span data-stu-id="79e9e-140">Before you proceed by modifying the page, it is useful to familiarize yourself with the Visual Studio development environment.</span></span> <span data-ttu-id="79e9e-141">下图显示了 windows 和 Visual Studio 和 Visual Studio Express for Web 中可用的工具。</span><span class="sxs-lookup"><span data-stu-id="79e9e-141">The following illustration shows you the windows and tools that are available in Visual Studio and Visual Studio Express for Web.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="79e9e-142">下图显示的默认窗口和窗口位置。</span><span class="sxs-lookup"><span data-stu-id="79e9e-142">This diagram shows default windows and window locations.</span></span> <span data-ttu-id="79e9e-143">**视图**菜单，可以显示其他窗口和重新排列和调整大小以适合你的首选项。</span><span class="sxs-lookup"><span data-stu-id="79e9e-143">The **View** menu allows you to display additional windows, and to rearrange and resize windows to suit your preferences.</span></span> <span data-ttu-id="79e9e-144">如果已对窗口排列做出更改，你看到的内容将与此图不一致。</span><span class="sxs-lookup"><span data-stu-id="79e9e-144">If changes have already been made to the window arrangement, what you see will not match the illustration.</span></span>


 <span data-ttu-id="79e9e-145">在 Visual Studio 环境</span><span class="sxs-lookup"><span data-stu-id="79e9e-145">The Visual Studio environment</span></span>

![Visual Studio 环境](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a><span data-ttu-id="79e9e-147">熟悉 Web 设计器</span><span class="sxs-lookup"><span data-stu-id="79e9e-147">Familiarize yourself with the Web designer</span></span>

<span data-ttu-id="79e9e-148">检查上图中，并与文本匹配的以下列表中，用于描述了最常使用的窗口和工具。</span><span class="sxs-lookup"><span data-stu-id="79e9e-148">Examine the above illustration and match the text to the following list, which describes the most commonly used windows and tools.</span></span> <span data-ttu-id="79e9e-149">（不是所有 windows 和你看到此处列出的工具，只有都标记在上图中。）</span><span class="sxs-lookup"><span data-stu-id="79e9e-149">(Not all windows and tools that you see are listed here, only those marked in the preceding illustration.)</span></span>

- <span data-ttu-id="79e9e-150">工具栏。</span><span class="sxs-lookup"><span data-stu-id="79e9e-150">Toolbars.</span></span> <span data-ttu-id="79e9e-151">提供用于格式化文本、 查找文本等命令。</span><span class="sxs-lookup"><span data-stu-id="79e9e-151">Provide commands for formatting text, finding text, and so on.</span></span> <span data-ttu-id="79e9e-152">仅当你处理时，某些工具栏才可用**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-152">Some toolbars are available only when you are working in **Design** view.</span></span>
- <span data-ttu-id="79e9e-153">**解决方案资源管理器**窗口。</span><span class="sxs-lookup"><span data-stu-id="79e9e-153">**Solution Explorer** window.</span></span> <span data-ttu-id="79e9e-154">Web 应用程序中显示的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="79e9e-154">Displays the files and folders in your Web application.</span></span>
- <span data-ttu-id="79e9e-155">文档窗口。</span><span class="sxs-lookup"><span data-stu-id="79e9e-155">Document window.</span></span> <span data-ttu-id="79e9e-156">显示你正在使用选项卡式窗口的文档。</span><span class="sxs-lookup"><span data-stu-id="79e9e-156">Displays the documents you are working on in tabbed windows.</span></span> <span data-ttu-id="79e9e-157">你可以通过单击选项卡的文档之间切换。</span><span class="sxs-lookup"><span data-stu-id="79e9e-157">You can switch between documents by clicking tabs.</span></span>
- <span data-ttu-id="79e9e-158">**属性**窗口。</span><span class="sxs-lookup"><span data-stu-id="79e9e-158">**Properties** window.</span></span> <span data-ttu-id="79e9e-159">允许您更改页、 HTML 元素、 控件和其他对象的设置。</span><span class="sxs-lookup"><span data-stu-id="79e9e-159">Allows you to change settings for the page, HTML elements, controls, and other objects.</span></span>
- <span data-ttu-id="79e9e-160">查看选项卡。</span><span class="sxs-lookup"><span data-stu-id="79e9e-160">View tabs.</span></span> <span data-ttu-id="79e9e-161">向您提供同一文档的不同视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-161">Present you with different views of the same document.</span></span> <span data-ttu-id="79e9e-162">**设计**视图是附近的所见即所得的编辑图面。</span><span class="sxs-lookup"><span data-stu-id="79e9e-162">**Design** view is a near-WYSIWYG editing surface.</span></span> <span data-ttu-id="79e9e-163">**源**视图是 HTML 编辑器中的为页。</span><span class="sxs-lookup"><span data-stu-id="79e9e-163">**Source** view is the HTML editor for the page.</span></span> <span data-ttu-id="79e9e-164">**拆分**视图将同时显示**设计**视图和**源**文档视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-164">**Split** view displays both the **Design** view and the **Source** view for the document.</span></span> <span data-ttu-id="79e9e-165">您将使用**设计**和**源**稍后在本演练的视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-165">You will work with the **Design** and **Source** views later in this walkthrough.</span></span> <span data-ttu-id="79e9e-166">如果想要打开中的 Web 页**设计**查看，请在**工具**菜单上，单击**选项**，选择**HTML 设计器**节点，然后更改**起始页位置**选项。</span><span class="sxs-lookup"><span data-stu-id="79e9e-166">If you prefer to open Web pages in **Design** view, on the **Tools** menu, click **Options**, select the **HTML Designer** node, and change the **Start Pages In** option.</span></span>
- <span data-ttu-id="79e9e-167">**工具箱**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-167">**ToolBox**.</span></span> <span data-ttu-id="79e9e-168">提供控件和可以拖到你的页面上的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="79e9e-168">Provides controls and HTML elements that you can drag onto your page.</span></span> <span data-ttu-id="79e9e-169">**工具箱**元素进行分组的公共函数。</span><span class="sxs-lookup"><span data-stu-id="79e9e-169">**Toolbox** elements are grouped by common function.</span></span>
- <span data-ttu-id="79e9e-170">S **erver 资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-170">S **erver Explorer**.</span></span> <span data-ttu-id="79e9e-171">显示数据库连接。</span><span class="sxs-lookup"><span data-stu-id="79e9e-171">Displays database connections.</span></span> <span data-ttu-id="79e9e-172">如果服务器资源管理器不可见，请在视图菜单中，单击服务器资源管理器。</span><span class="sxs-lookup"><span data-stu-id="79e9e-172">If Server Explorer is not visible, on the View menu, click Server Explorer.</span></span>


### <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="79e9e-173">创建新的 ASP.NET Web 窗体页</span><span class="sxs-lookup"><span data-stu-id="79e9e-173">Creating a new ASP.NET Web Forms Page</span></span>


<span data-ttu-id="79e9e-174">当你创建新的 Web 窗体应用程序使用**ASP.NET Web 应用程序**项目模板中，Visual Studio 将添加一个名为的 ASP.NET 页 （Web 窗体页） *Default.aspx*，以及为多个其他文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="79e9e-174">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="79e9e-175">你可以使用*Default.aspx*页为 Web 应用程序主页的步骤。</span><span class="sxs-lookup"><span data-stu-id="79e9e-175">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="79e9e-176">但是，对于本演练，你将创建和使用新的页。</span><span class="sxs-lookup"><span data-stu-id="79e9e-176">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="79e9e-177">要添加到 Web 应用程序页</span><span class="sxs-lookup"><span data-stu-id="79e9e-177">To add a page to the Web application</span></span>


1. <span data-ttu-id="79e9e-178">关闭*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="79e9e-178">Close the *Default.aspx* page.</span></span> <span data-ttu-id="79e9e-179">若要执行此操作，单击显示的文件名称的选项卡，然后单击关闭选项。</span><span class="sxs-lookup"><span data-stu-id="79e9e-179">To do this, click the tab that displays the file name and then click the close option.</span></span>
2. <span data-ttu-id="79e9e-180">在**解决方案资源管理器**，右键单击 Web 应用程序名称 (在本教程中的应用程序名称**BasicWebSite**)，然后单击**添加** - &gt;**新项**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-180">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="79e9e-181">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="79e9e-181">The **Add New Item** dialog box is displayed.</span></span>
3. <span data-ttu-id="79e9e-182">选择**Visual C#**  - &gt; **Web**左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="79e9e-182">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="79e9e-183">然后，选择**Web 窗体**从中间列表并将其命名*FirstWebPage.aspx*。</span><span class="sxs-lookup"><span data-stu-id="79e9e-183">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="79e9e-184">![添加新项对话框](creating-a-basic-web-forms-page/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="79e9e-184">![Add New Item dialog box](creating-a-basic-web-forms-page/_static/image6.png)</span></span>
4. <span data-ttu-id="79e9e-185">单击**添加**将网页添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="79e9e-185">Click **Add** to add the web page to your project.</span></span>  
<span data-ttu-id="79e9e-186">Visual Studio 将创建新的页，并将其打开。</span><span class="sxs-lookup"><span data-stu-id="79e9e-186">Visual Studio creates the new page and opens it.</span></span>


### <a name="adding-html-to-the-page"></a><span data-ttu-id="79e9e-187">向页面添加 HTML</span><span class="sxs-lookup"><span data-stu-id="79e9e-187">Adding HTML to the Page</span></span>


<span data-ttu-id="79e9e-188">在演练本部分，你将添加一些静态文本页。</span><span class="sxs-lookup"><span data-stu-id="79e9e-188">In this part of the walkthrough, you will add some static text to the page.</span></span>

### <a name="to-add-text-to-the-page"></a><span data-ttu-id="79e9e-189">将文本添加到页面</span><span class="sxs-lookup"><span data-stu-id="79e9e-189">To add text to the page</span></span>


1. <span data-ttu-id="79e9e-190">在文档窗口的底部，单击**设计**选项卡以切换到**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-190">At the bottom of the document window, click the **Design** tab to switch to **Design** view.</span></span>

    <span data-ttu-id="79e9e-191">设计视图显示类似所见即所得的方式显示当前页。</span><span class="sxs-lookup"><span data-stu-id="79e9e-191">Design view displays the current page in a WYSIWYG-like way.</span></span> <span data-ttu-id="79e9e-192">此时，你没有任何文本或控件在页上，因此页是空白概述了矩形的虚线除外。</span><span class="sxs-lookup"><span data-stu-id="79e9e-192">At this point, you do not have any text or controls on the page, so the page is blank except for a dashed line that outlines a rectangle.</span></span> <span data-ttu-id="79e9e-193">将此矩形表示**div**页面上的元素。</span><span class="sxs-lookup"><span data-stu-id="79e9e-193">This rectangle represents a **div** element on the page.</span></span>
2. <span data-ttu-id="79e9e-194">概述由虚线该矩形内单击。</span><span class="sxs-lookup"><span data-stu-id="79e9e-194">Click inside the rectangle that is outlined by a dashed line.</span></span>
3. <span data-ttu-id="79e9e-195">类型**欢迎使用 Visual Web Developer**按**ENTER**两次。</span><span class="sxs-lookup"><span data-stu-id="79e9e-195">Type **Welcome to Visual Web Developer** and press **ENTER** twice.</span></span>

    <span data-ttu-id="79e9e-196">下图显示中键入的文本**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-196">The following illustration shows the text you typed in **Design** view.</span></span>

    <span data-ttu-id="79e9e-197">![在设计视图中的欢迎文本](creating-a-basic-web-forms-page/_static/image7.png "在设计视图中的欢迎文本")</span><span class="sxs-lookup"><span data-stu-id="79e9e-197">![Welcome text in Design view](creating-a-basic-web-forms-page/_static/image7.png "Welcome text in Design view")</span></span>
4. <span data-ttu-id="79e9e-198">切换到**源**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-198">Switch to **Source** view.</span></span>

    <span data-ttu-id="79e9e-199">你可以看到在 HTML**源**框中键入时创建的视图**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-199">You can see the HTML in **Source** view that you created when you typed in **Design** view.</span></span>  
    <span data-ttu-id="79e9e-200">![包含静态文本的网页](creating-a-basic-web-forms-page/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="79e9e-200">![Web Page with Static Text](creating-a-basic-web-forms-page/_static/image8.png)</span></span>


### <a name="running-the-page"></a><span data-ttu-id="79e9e-201">运行页</span><span class="sxs-lookup"><span data-stu-id="79e9e-201">Running the Page</span></span>


<span data-ttu-id="79e9e-202">通过将控件添加到页在继续之前，你可以先运行它。</span><span class="sxs-lookup"><span data-stu-id="79e9e-202">Before you proceed by adding controls to the page, you can first run it.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="79e9e-203">若要运行页面</span><span class="sxs-lookup"><span data-stu-id="79e9e-203">To run the page</span></span>


1. <span data-ttu-id="79e9e-204">在**解决方案资源管理器**，右键单击*FirstWebPage.aspx*和选择**设为起始页**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-204">In **Solution Explorer**, right-click *FirstWebPage.aspx* and select **Set as Start Page**.</span></span>
2. <span data-ttu-id="79e9e-205">按**CTRL + F5**运行页面。</span><span class="sxs-lookup"><span data-stu-id="79e9e-205">Press **CTRL+F5** to run the page.</span></span>

    <span data-ttu-id="79e9e-206">在浏览器中显示页面。</span><span class="sxs-lookup"><span data-stu-id="79e9e-206">The page is displayed in the browser.</span></span> <span data-ttu-id="79e9e-207">尽管你创建的页面有的文件名称扩展*.aspx*，它当前运行类似任何 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="79e9e-207">Although the page you created has a file-name extension of *.aspx*, it currently runs like any HTML page.</span></span>

    <span data-ttu-id="79e9e-208">若要在浏览器中显示页你还可以右键单击中的页**解决方案资源管理器**和选择**用浏览器查看**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-208">To display a page in the browser you can also right-click the page in **Solution Explorer** and select **View in Browser**.</span></span>
3. <span data-ttu-id="79e9e-209">关闭浏览器来停止 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="79e9e-209">Close the browser to stop the Web application.</span></span>


## <a name="adding-and-programming-controls"></a><span data-ttu-id="79e9e-210">添加和对控件进行编程</span><span class="sxs-lookup"><span data-stu-id="79e9e-210">Adding and Programming Controls</span></span>


<a id="sectionToggle1"></a>

<span data-ttu-id="79e9e-211">你现在将向页面添加服务器控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-211">You will now add server controls to the page.</span></span> <span data-ttu-id="79e9e-212">服务器控件，如按钮、 标签、 文本框中和其他熟悉的控件，提供 Web 窗体页面的典型窗体处理功能。</span><span class="sxs-lookup"><span data-stu-id="79e9e-212">Server controls, such as buttons, labels, text boxes, and other familiar controls, provide typical form-processing capabilities for your Web Forms pages.</span></span> <span data-ttu-id="79e9e-213">但是，你可以在服务器上，而不是客户端运行的代码与对控件进行编程。</span><span class="sxs-lookup"><span data-stu-id="79e9e-213">However, you can program the controls with code that runs on the server, rather than the client.</span></span>

<span data-ttu-id="79e9e-214">你将添加[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件，[文本框中](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件，和一个[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件到页，并编写代码来处理[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-214">You will add a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, a [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control, and a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control to the page and write code to handle the [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>

### <a name="to-add-controls-to-the-page"></a><span data-ttu-id="79e9e-215">若要将控件添加到页</span><span class="sxs-lookup"><span data-stu-id="79e9e-215">To add controls to the page</span></span>


1. <span data-ttu-id="79e9e-216">单击**设计**选项卡以切换到**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-216">Click the **Design** tab to switch to **Design** view.</span></span>
2. <span data-ttu-id="79e9e-217">将插入点放在末尾**欢迎使用 Visual Web Developer**文本并按**ENTER**五个或多个时间，以便在某些腾出空间**div**元素框。</span><span class="sxs-lookup"><span data-stu-id="79e9e-217">Put the insertion point at the end of the **Welcome to Visual Web Developer** text and press **ENTER** five or more times to make some room in the **div** element box.</span></span>
3. <span data-ttu-id="79e9e-218">在**工具箱**，展开**标准**组如果尚未展开。</span><span class="sxs-lookup"><span data-stu-id="79e9e-218">In the **Toolbox**, expand the **Standard** group if it is not already expanded.</span></span>  
<span data-ttu-id="79e9e-219">请注意，你可能需要展开**工具箱**窗口在左侧以查看它。</span><span class="sxs-lookup"><span data-stu-id="79e9e-219">Note that you may need to expand the **Toolbox** window on the left to view it.</span></span>
4. <span data-ttu-id="79e9e-220">拖动[文本框中](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件拖到页面上并将它的之中放**div**元素框具有**欢迎使用 Visual Web Developer**在第一行中。</span><span class="sxs-lookup"><span data-stu-id="79e9e-220">Drag a [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control onto the page and drop it in the middle of the **div** element box that has **Welcome to Visual Web Developer** in the first line.</span></span>
5. <span data-ttu-id="79e9e-221">拖动[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件拖到页面上，并将其放到右侧[文本框中](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-221">Drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page and drop it to the right of the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control.</span></span>
6. <span data-ttu-id="79e9e-222">拖动[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件拖到页面上并将它放在单独的行下面[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-222">Drag a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control onto the page and drop it on a separate line below the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>
7. <span data-ttu-id="79e9e-223">将插入点上述[文本框中](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控制，，然后键入**输入您的姓名：** 。</span><span class="sxs-lookup"><span data-stu-id="79e9e-223">Put the insertion point above the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control, and then type **Enter your name:** .</span></span>

    <span data-ttu-id="79e9e-224">此静态 HTML 文本标题是[文本框中](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-224">This static HTML text is the caption for the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control.</span></span> <span data-ttu-id="79e9e-225">可以混合使用静态 HTML 和同一页面上的服务器控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-225">You can mix static HTML and server controls on the same page.</span></span> <span data-ttu-id="79e9e-226">下图显示三个控件中的显示方式**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-226">The following illustration shows how the three controls appear in **Design** view.</span></span>

    <span data-ttu-id="79e9e-227">![在设计视图中的三个控件](creating-a-basic-web-forms-page/_static/image9.png "在设计视图中的三个控件")</span><span class="sxs-lookup"><span data-stu-id="79e9e-227">![Three controls in Design view](creating-a-basic-web-forms-page/_static/image9.png "Three controls in Design view")</span></span>


### <a name="setting-control-properties"></a><span data-ttu-id="79e9e-228">设置控件属性</span><span class="sxs-lookup"><span data-stu-id="79e9e-228">Setting Control Properties</span></span>


<span data-ttu-id="79e9e-229">Visual Studio 提供了各种方式来设置页上的控件的属性。</span><span class="sxs-lookup"><span data-stu-id="79e9e-229">Visual Studio offers you various ways to set the properties of controls on the page.</span></span> <span data-ttu-id="79e9e-230">在演练本部分，将属性设置中同时**设计**视图和**源**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-230">In this part of the walkthrough, you will set properties in both **Design** view and **Source** view.</span></span>

### <a name="to-set-control-properties"></a><span data-ttu-id="79e9e-231">若要设置控件属性</span><span class="sxs-lookup"><span data-stu-id="79e9e-231">To set control properties</span></span>


1. <span data-ttu-id="79e9e-232">第一次，显示**属性**通过从选择的 windows**视图**菜单-&gt; **其他窗口** - &gt; **属性窗口**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-232">First, display the **Properties** windows by selecting from the **View** menu -&gt; **Other Windows** -&gt; **Properies Window**.</span></span> <span data-ttu-id="79e9e-233">或者，你可以选择**F4**以显示**属性**窗口。</span><span class="sxs-lookup"><span data-stu-id="79e9e-233">You could alternatively select **F4** to display the **Properties** window.</span></span>
2. <span data-ttu-id="79e9e-234">选择[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件，然后在**属性**窗口中，设置的值**文本**到**显示名称**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-234">Select the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, and then in the **Properties** window, set the value of **Text** to **Display Name**.</span></span> <span data-ttu-id="79e9e-235">下图中所示，在设计器中，在按钮上显示您输入的文本。</span><span class="sxs-lookup"><span data-stu-id="79e9e-235">The text you entered appears on the button in the designer, as shown in the following illustration.</span></span>

    <span data-ttu-id="79e9e-236">![设置按钮文本](creating-a-basic-web-forms-page/_static/image10.png "设置按钮文本")</span><span class="sxs-lookup"><span data-stu-id="79e9e-236">![Set Button text](creating-a-basic-web-forms-page/_static/image10.png "Set Button text")</span></span>
3. <span data-ttu-id="79e9e-237">切换到**源**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-237">Switch to **Source** view.</span></span>

    <span data-ttu-id="79e9e-238">**源**视图显示在该 HTML 页上，包括 Visual Studio 已创建的服务器控件的元素。</span><span class="sxs-lookup"><span data-stu-id="79e9e-238">**Source** view displays the HTML for the page, including the elements that Visual Studio has created for the server controls.</span></span> <span data-ttu-id="79e9e-239">控件使用 HTML 类似的语法声明，只不过标记使用前缀**asp:**和的属性包括在**runat =&quot;服务器&quot;**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-239">Controls are declared using HTML-like syntax, except that the tags use the prefix **asp:** and include the attribute **runat=&quot;server&quot;**.</span></span>

    <span data-ttu-id="79e9e-240">控件属性被声明为属性。</span><span class="sxs-lookup"><span data-stu-id="79e9e-240">Control properties are declared as attributes.</span></span> <span data-ttu-id="79e9e-241">例如，如果设置[文本](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx)属性[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件中，在步骤 1 中，实际在设置**文本**在控件的标记中的属性。</span><span class="sxs-lookup"><span data-stu-id="79e9e-241">For example, when you set the [Text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx) property for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, in step 1, you were actually setting the **Text** attribute in the control's markup.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="79e9e-242">所有这些控件都位于**窗体**元素，它还具有属性**runat =&quot;服务器&quot;**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-242">All the controls are inside a **form** element, which also has the attribute **runat=&quot;server&quot;**.</span></span> <span data-ttu-id="79e9e-243">**Runat =&quot;服务器&quot;**属性和**asp:**前缀将对控件的标记控件标记，以便由进行处理 ASP.NET 在服务器上运行页面时。</span><span class="sxs-lookup"><span data-stu-id="79e9e-243">The **runat=&quot;server&quot;** attribute and the **asp:** prefix for control tags mark the controls so that they are processed by ASP.NET on the server when the page runs.</span></span> <span data-ttu-id="79e9e-244">外部的代码**&lt;形成 runat =&quot;服务器&quot;&gt;** 和**&lt;脚本 runat =&quot;服务器&quot;&gt;**元素原样发送到浏览器中，这正是 ASP.NET 代码必须在其开始标记中包含元素内**runat =&quot;服务器&quot;**属性。</span><span class="sxs-lookup"><span data-stu-id="79e9e-244">Code outside of **&lt;form runat=&quot;server&quot;&gt;** and **&lt;script runat=&quot;server&quot;&gt;** elements is sent unchanged to the browser, which is why the ASP.NET code must be inside an element whose opening tag contains the **runat=&quot;server&quot;** attribute.</span></span>
4. <span data-ttu-id="79e9e-245">接下来，将添加到的其他属性[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-245">Next, you will add an additional property to the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)  control.</span></span> <span data-ttu-id="79e9e-246">将插入点直接后的**asp： 标签**中 **&lt;asp： 标签&gt;**标记，然后按**空格键**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-246">Put the insertion point directly after **asp:Label** in the **&lt;asp:Label&gt;** tag, and then press **SPACEBAR**.</span></span>

    <span data-ttu-id="79e9e-247">下拉列表将出现，显示可用的属性，你可以为设置列表[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-247">A drop-down list appears that displays the list of available properties you can set for a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span> <span data-ttu-id="79e9e-248">此功能称为**IntelliSense**，可帮助你在**源**服务器控件、 HTML 元素和其他项的语法页面上的视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-248">This feature, referred to as **IntelliSense**, helps you in **Source** view with the syntax of server controls, HTML elements, and other items on the page.</span></span> <span data-ttu-id="79e9e-249">下图显示**IntelliSense**下拉列表[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-249">The following illustration shows the **IntelliSense** drop-down list for the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>

    <span data-ttu-id="79e9e-250">![IntelliSense 特性](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense 特性")</span><span class="sxs-lookup"><span data-stu-id="79e9e-250">![IntelliSense attributes](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense attributes")</span></span>
5. <span data-ttu-id="79e9e-251">选择**ForeColor**然后键入等号。</span><span class="sxs-lookup"><span data-stu-id="79e9e-251">Select **ForeColor** and then type an equal sign.</span></span>

    <span data-ttu-id="79e9e-252">IntelliSense 会显示颜色的列表。</span><span class="sxs-lookup"><span data-stu-id="79e9e-252">IntelliSense displays a list of colors.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="79e9e-253">可以显示**IntelliSense**随时通过按下的下拉列表**CTRL + J**查看代码时。</span><span class="sxs-lookup"><span data-stu-id="79e9e-253">You can display an **IntelliSense** drop-down list at any time by pressing **CTRL+J** when viewing code.</span></span>
6. <span data-ttu-id="79e9e-254">为选择颜色**[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)**控件的文本。</span><span class="sxs-lookup"><span data-stu-id="79e9e-254">Select a color for the **[Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** control's text.</span></span> <span data-ttu-id="79e9e-255">请确保选择是足够深，以便读取针对白色背景的颜色。</span><span class="sxs-lookup"><span data-stu-id="79e9e-255">Make sure you select a color that is dark enough to read against a white background.</span></span>

    <span data-ttu-id="79e9e-256">**ForeColor**属性已完成并且你已选择，包括右引号的颜色。</span><span class="sxs-lookup"><span data-stu-id="79e9e-256">The **ForeColor** attribute is completed with the color that you have selected, including the closing quotation mark.</span></span>


### <a name="programming-the-button-control"></a><span data-ttu-id="79e9e-257">编程按钮控件</span><span class="sxs-lookup"><span data-stu-id="79e9e-257">Programming the Button Control</span></span>


<span data-ttu-id="79e9e-258">对于本演练，你将编写读取用户在文本框中输入，并随后显示中的名称的名称的代码[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-258">For this walkthrough, you will write code that reads the name that the user enters into the text box and then displays the name in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>

### <a name="add-a-default-button-event-handler"></a><span data-ttu-id="79e9e-259">添加一个默认按钮事件处理程序</span><span class="sxs-lookup"><span data-stu-id="79e9e-259">Add a default button event handler</span></span>


1. <span data-ttu-id="79e9e-260">切换到**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-260">Switch to **Design** view.</span></span>
2. <span data-ttu-id="79e9e-261">双击[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-261">Double-click the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>

    <span data-ttu-id="79e9e-262">默认情况下，Visual Studio 切换到代码隐藏文件，并创建主干事件处理程序[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的默认事件[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-262">By default, Visual Studio switches to a code-behind file and creates a skeleton event handler for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control's default event, the [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event.</span></span> <span data-ttu-id="79e9e-263">代码隐藏文件 （如 C# 中) 在服务器代码中分隔 UI 标记 （如 HTML)。</span><span class="sxs-lookup"><span data-stu-id="79e9e-263">The code-behind file separates your UI markup (such as HTML) from your server code (such as C#).</span></span>   
   <span data-ttu-id="79e9e-264">游标位于添加为此事件处理程序的代码。</span><span class="sxs-lookup"><span data-stu-id="79e9e-264">The cursor is positioned to added code for this event handler.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="79e9e-265">双击中的控件**设计**视图只是其中一个的几种方法可以创建事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="79e9e-265">Double-clicking a control in **Design** view is just one of several ways you can create event handlers.</span></span>
3. <span data-ttu-id="79e9e-266">内部**Button1\_单击**事件处理程序中，键入**Label1**跟一个句点 (**。**)。</span><span class="sxs-lookup"><span data-stu-id="79e9e-266">Inside the **Button1\_Click** event handler, type **Label1** followed by a period (**.**).</span></span>

    <span data-ttu-id="79e9e-267">当你键入后的期间**ID**的标签 (**Label1**)，Visual Studio 将显示为可用成员列表[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件，如下所示图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-267">When you type the period after the **ID** of the label (**Label1**), Visual Studio displays a list of available members for the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control, as shown in the following illustration.</span></span> <span data-ttu-id="79e9e-268">成员通常的属性、 方法或事件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-268">A member commonly a property, method, or event.</span></span>

    <span data-ttu-id="79e9e-269">![在代码视图中的 IntelliSense](creating-a-basic-web-forms-page/_static/image12.png "代码视图中的 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="79e9e-269">![IntelliSense in Code view](creating-a-basic-web-forms-page/_static/image12.png "IntelliSense in Code view")</span></span>
4. <span data-ttu-id="79e9e-270">完成**单击**按钮以便它读取下面的代码示例中所示的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="79e9e-270">Finish the **Click** event handler for the button so that it reads as shown in the following code example.</span></span>

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. <span data-ttu-id="79e9e-271">切换回查看**源**你的 HTML 标记，请右键单击视图*FirstWebPage.aspx*中**解决方案资源管理器**并选择**视图标记**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-271">Switch back to viewing the **Source** view of your HTML markup by right-clicking *FirstWebPage.aspx* in the **Solution Explorer** and selecting **View Markup**.</span></span>
6. <span data-ttu-id="79e9e-272">滚动到 **&lt;asp： 按钮&gt;**元素。</span><span class="sxs-lookup"><span data-stu-id="79e9e-272">Scroll to the **&lt;asp:Button&gt;** element.</span></span> <span data-ttu-id="79e9e-273">请注意，  **&lt;asp： 按钮&gt;**元素现在具有属性**onclick =&quot;Button1\_单击&quot;**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-273">Note that the **&lt;asp:Button&gt;** element now has the attribute **onclick=&quot;Button1\_Click&quot;**.</span></span>

    <span data-ttu-id="79e9e-274">此属性将绑定按钮的[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)到上一步中编码的处理程序方法的事件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-274">This attribute binds the button's [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event to the handler method you coded in the previous step.</span></span>

    <span data-ttu-id="79e9e-275">事件处理程序方法可以具有任何名称;显示的名称是由 Visual Studio 创建的默认名称。</span><span class="sxs-lookup"><span data-stu-id="79e9e-275">Event handler methods can have any name; the name you see is the default name created by Visual Studio.</span></span> <span data-ttu-id="79e9e-276">重要的一点是，该名称用于**OnClick** HTML 中的特性必须与匹配的代码隐藏文件中定义的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="79e9e-276">The important point is that the name used for the **OnClick** attribute in the HTML must match the name of a method defined in the code-behind.</span></span>


### <a name="running-the-page"></a><span data-ttu-id="79e9e-277">运行页</span><span class="sxs-lookup"><span data-stu-id="79e9e-277">Running the Page</span></span>


<span data-ttu-id="79e9e-278">你现在可以测试页上的服务器控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-278">You can now test the server controls on the page.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="79e9e-279">若要运行页面</span><span class="sxs-lookup"><span data-stu-id="79e9e-279">To run the page</span></span>


1. <span data-ttu-id="79e9e-280">按**CTRL + F5**浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="79e9e-280">Press **CTRL+F5** to run the page in the browser.</span></span> <span data-ttu-id="79e9e-281">如果发生错误，重新检查上述步骤。</span><span class="sxs-lookup"><span data-stu-id="79e9e-281">If an error occurs, recheck the steps above.</span></span>
2. <span data-ttu-id="79e9e-282">在文本框中输入一个名称，然后单击**显示名称**按钮。</span><span class="sxs-lookup"><span data-stu-id="79e9e-282">Enter a name into the text box and click the **Display Name** button.</span></span>

    <span data-ttu-id="79e9e-283">您输入的名称显示在[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-283">The name you entered is displayed in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span> <span data-ttu-id="79e9e-284">请注意，当你单击按钮时，页面将被发送到 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="79e9e-284">Note that when you click the button, the page is posted to the Web server.</span></span> <span data-ttu-id="79e9e-285">ASP.NET 然后重新创建页上，运行你的代码 (在这种情况下，[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件处理程序将运行)，然后将新的页发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="79e9e-285">ASP.NET then recreates the page, runs your code (in this case, the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control's [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event handler runs), and then sends the new page to the browser.</span></span> <span data-ttu-id="79e9e-286">如果你观看浏览器中的状态栏，可以看到，页进行的往返过程到 Web 服务器每次你单击按钮。</span><span class="sxs-lookup"><span data-stu-id="79e9e-286">If you watch the status bar in the browser, you can see that the page is making a round trip to the Web server each time you click the button.</span></span>
3. <span data-ttu-id="79e9e-287">在浏览器中，查看你在正在运行的页上右键单击并选择的页面的源**查看源**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-287">In the browser, view the source of the page you are running by right-clicking on the page and selecting **View source**.</span></span>

    <span data-ttu-id="79e9e-288">在页的源代码，而无需任何服务器代码中看到 HTML。</span><span class="sxs-lookup"><span data-stu-id="79e9e-288">In the page source code, you see HTML without any server code.</span></span> <span data-ttu-id="79e9e-289">具体而言，你看不见**&lt;asp:&gt;**与你共事中的元素**源**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-289">Specifically, you do not see the **&lt;asp:&gt;** elements that you were working with in **Source** view.</span></span> <span data-ttu-id="79e9e-290">页运行时，ASP.NET 将处理服务器控件，并呈现到页执行的函数，表示控件的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="79e9e-290">When the page runs, ASP.NET processes the server controls and renders HTML elements to the page that perform the functions that represent the control.</span></span> <span data-ttu-id="79e9e-291">例如，  **&lt;asp： 按钮&gt;**控件呈现为 HTML **&lt;输入类型 =&quot;提交&quot;&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="79e9e-291">For example, the **&lt;asp:Button&gt;** control is rendered as the HTML **&lt;input type=&quot;submit&quot;&gt;** element.</span></span>
4. <span data-ttu-id="79e9e-292">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="79e9e-292">Close the browser.</span></span>


## <a name="working-with-additional-controls"></a><span data-ttu-id="79e9e-293">使用其他控件</span><span class="sxs-lookup"><span data-stu-id="79e9e-293">Working with Additional Controls</span></span>

<a id="sectionToggle2"></a>

<span data-ttu-id="79e9e-294">在本部分演练中，您将可以使用[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件，一次显示一个月的日期。</span><span class="sxs-lookup"><span data-stu-id="79e9e-294">In this part of the walkthrough, you will work with the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control, which displays dates a month at a time.</span></span> <span data-ttu-id="79e9e-295">[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件是一个更复杂比你一直在处理按钮、 文本框和标签控件，并阐明服务器控件的一些其他功能。</span><span class="sxs-lookup"><span data-stu-id="79e9e-295">The [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control is a more complex control than the button, text box, and label you have been working with and illustrates some further capabilities of server controls.</span></span>

<span data-ttu-id="79e9e-296">在本部分中，你将添加[System.Web.UI.WebControls.Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制到页并设置其格式。</span><span class="sxs-lookup"><span data-stu-id="79e9e-296">In this section, you will add a [System.Web.UI.WebControls.Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control to the page and format it.</span></span>

### <a name="to-add-a-calendar-control"></a><span data-ttu-id="79e9e-297">若要添加一个日历控件</span><span class="sxs-lookup"><span data-stu-id="79e9e-297">To add a Calendar control</span></span>


1. <span data-ttu-id="79e9e-298">在 Visual Studio 中，切换到**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-298">In Visual Studio, switch to **Design** view.</span></span>
2. <span data-ttu-id="79e9e-299">从**标准**部分**工具箱**，拖动[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件拖到页面上并将它放下面**div**元素，包含的其他控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-299">From the **Standard** section of the **Toolbox**, drag a [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control onto the page and drop it below the **div** element that contains the other controls.</span></span>

    <span data-ttu-id="79e9e-300">将显示日历的智能标记面板。</span><span class="sxs-lookup"><span data-stu-id="79e9e-300">The calendar's smart tag panel is displayed.</span></span> <span data-ttu-id="79e9e-301">该面板显示容易让你可以针对所选控件执行的最常见的任务的命令。</span><span class="sxs-lookup"><span data-stu-id="79e9e-301">The panel displays commands that make it easy for you to perform the most common tasks for the selected control.</span></span> <span data-ttu-id="79e9e-302">下图显示[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制在呈现**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-302">The following illustration shows the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control as rendered in **Design** view.</span></span>

    <span data-ttu-id="79e9e-303">![月历控件在设计视图中](creating-a-basic-web-forms-page/_static/image13.png "月历控件在设计视图中")</span><span class="sxs-lookup"><span data-stu-id="79e9e-303">![Calendar control in Design view](creating-a-basic-web-forms-page/_static/image13.png "Calendar control in Design view")</span></span>
3. <span data-ttu-id="79e9e-304">在智能标记面板中，选择**自动套用格式**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-304">In the smart tag panel, choose **Auto Format**.</span></span>

    <span data-ttu-id="79e9e-305">**自动套用格式**显示对话框，该编辑器可以为该日历选择一个格式设置方案。</span><span class="sxs-lookup"><span data-stu-id="79e9e-305">The **Auto Format** dialog box is displayed, which allows you to select a formatting scheme for the calendar.</span></span> <span data-ttu-id="79e9e-306">下图显示**自动套用格式**对话框[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-306">The following illustration shows the **Auto Format** dialog box for the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control.</span></span>

    <span data-ttu-id="79e9e-307">![自动套用格式对话框 （Calendar 控件）](creating-a-basic-web-forms-page/_static/image14.png "自动套用格式对话框 （Calendar 控件）")</span><span class="sxs-lookup"><span data-stu-id="79e9e-307">![Auto Format dialog box (Calendar control)](creating-a-basic-web-forms-page/_static/image14.png "Auto Format dialog box (Calendar control)")</span></span>
4. <span data-ttu-id="79e9e-308">从**选择一种方案**列表中，选择**简单**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="79e9e-308">From the **Select a scheme** list, select **Simple** and then click **OK**.</span></span>
5. <span data-ttu-id="79e9e-309">切换到**源**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-309">Switch to **Source** view.</span></span>

    <span data-ttu-id="79e9e-310">你可以看到 **&lt;asp： 日历&gt;**元素。</span><span class="sxs-lookup"><span data-stu-id="79e9e-310">You can see the **&lt;asp:Calendar&gt;** element.</span></span> <span data-ttu-id="79e9e-311">此元素是远远超过前面创建的简单控件的元素。</span><span class="sxs-lookup"><span data-stu-id="79e9e-311">This element is much longer than the elements for the simple controls you created earlier.</span></span> <span data-ttu-id="79e9e-312">它还包括子元素，如 **&lt;WeekEndDayStyle&gt;**，分别表示各种格式设置。</span><span class="sxs-lookup"><span data-stu-id="79e9e-312">It also includes subelements, such as **&lt;WeekEndDayStyle&gt;**, which represent various formatting settings.</span></span> <span data-ttu-id="79e9e-313">下图显示[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)中控制**源**视图。</span><span class="sxs-lookup"><span data-stu-id="79e9e-313">The following illustration shows the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control in **Source** view.</span></span> <span data-ttu-id="79e9e-314">(请参阅中的确切标记**源**视图可能与该图略有不同。)</span><span class="sxs-lookup"><span data-stu-id="79e9e-314">(The exact markup that you see in **Source** view might differ slightly from the illustration.)</span></span>

    <span data-ttu-id="79e9e-315">![月历控件在源视图中](creating-a-basic-web-forms-page/_static/image15.png "月历控件在源视图中")</span><span class="sxs-lookup"><span data-stu-id="79e9e-315">![Calendar control in Source view](creating-a-basic-web-forms-page/_static/image15.png "Calendar control in Source view")</span></span>


### <a name="programming-the-calendar-control"></a><span data-ttu-id="79e9e-316">编程日历控件</span><span class="sxs-lookup"><span data-stu-id="79e9e-316">Programming the Calendar Control</span></span>


<span data-ttu-id="79e9e-317">在本部分中，您将编程[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件来显示当前选定的日期。</span><span class="sxs-lookup"><span data-stu-id="79e9e-317">In this section, you will program the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control to display the currently selected date.</span></span>

### <a name="to-program-the-calendar-control"></a><span data-ttu-id="79e9e-318">日历控件编程</span><span class="sxs-lookup"><span data-stu-id="79e9e-318">To program the Calendar control</span></span>


1. <span data-ttu-id="79e9e-319">在**设计**视图中，双击[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-319">In **Design** view, double-click the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control.</span></span>

    <span data-ttu-id="79e9e-320">创建一个新的事件处理程序并将其显示在代码隐藏文件中名为*FirstWebPage.aspx.cs*。</span><span class="sxs-lookup"><span data-stu-id="79e9e-320">A new event handler is created and displayed in the code-behind file named *FirstWebPage.aspx.cs*.</span></span>
2. <span data-ttu-id="79e9e-321">完成[SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx)事件处理程序替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="79e9e-321">Finish the [SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx) event handler with the following code.</span></span>


~~~
[!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]


[!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]
~~~

 <span data-ttu-id="79e9e-322">上面的代码将标签控件的文本设置为所选日期的日历控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-322">The above code sets the text of the label control to the selected date of the calendar control.</span></span>


### <a name="running-the-page"></a><span data-ttu-id="79e9e-323">运行页</span><span class="sxs-lookup"><span data-stu-id="79e9e-323">Running the Page</span></span>


<span data-ttu-id="79e9e-324">你现在可以测试日历。</span><span class="sxs-lookup"><span data-stu-id="79e9e-324">You can now test the calendar.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="79e9e-325">若要运行页面</span><span class="sxs-lookup"><span data-stu-id="79e9e-325">To run the page</span></span>


1. <span data-ttu-id="79e9e-326">按**CTRL + F5**浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="79e9e-326">Press **CTRL+F5** to run the page in the browser.</span></span>
2. <span data-ttu-id="79e9e-327">单击日历中的日期。</span><span class="sxs-lookup"><span data-stu-id="79e9e-327">Click a date in the calendar.</span></span>

    <span data-ttu-id="79e9e-328">在显示你单击的日期[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="79e9e-328">The date you clicked is displayed in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>
3. <span data-ttu-id="79e9e-329">在浏览器中，查看页的源代码。</span><span class="sxs-lookup"><span data-stu-id="79e9e-329">In the browser, view the source code for the page.</span></span>

    <span data-ttu-id="79e9e-330">请注意，[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件呈现到页作为**表**，每一天都作为**td**元素。</span><span class="sxs-lookup"><span data-stu-id="79e9e-330">Note that the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control has been rendered to the page as a **table**, with each day as a **td** element.</span></span>
4. <span data-ttu-id="79e9e-331">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="79e9e-331">Close the browser.</span></span>


## <a name="next-steps"></a><span data-ttu-id="79e9e-332">后续步骤</span><span class="sxs-lookup"><span data-stu-id="79e9e-332">Next Steps</span></span>


<a id="nextStepsToggle"></a>

<span data-ttu-id="79e9e-333">本演练阐释了 Visual Studio 页设计器的基本功能。</span><span class="sxs-lookup"><span data-stu-id="79e9e-333">This walkthrough has illustrated the basic features of the Visual Studio page designer.</span></span> <span data-ttu-id="79e9e-334">现在，你已了解如何创建和编辑 Visual Studio 中的 Web 窗体页，你可能想要浏览其他功能。</span><span class="sxs-lookup"><span data-stu-id="79e9e-334">Now that you understand how to create and edit a Web Forms page in Visual Studio, you might want to explore other features.</span></span> <span data-ttu-id="79e9e-335">例如，你可能想要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="79e9e-335">For example, you might want to do the following:</span></span>

- <span data-ttu-id="79e9e-336">了解有关 ASP.NET Web 窗体的详细信息按照分步教程系列[Getting Started with ASP.NET 4.5 Web 窗体和 Visual Studio 2013](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="79e9e-336">Learn more about ASP.NET Web Forms by following the step-by-step tutorial series [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md).</span></span>
- <span data-ttu-id="79e9e-337">了解有关级联样式表 (CSS)。</span><span class="sxs-lookup"><span data-stu-id="79e9e-337">Learn more about Cascading style sheets (CSS).</span></span> <span data-ttu-id="79e9e-338">有关详细信息，请参阅[使用 CSS 概述](https://msdn.microsoft.com/library/bb398931.aspx)。</span><span class="sxs-lookup"><span data-stu-id="79e9e-338">For details, see [Working with CSS Overview](https://msdn.microsoft.com/library/bb398931.aspx).</span></span>
