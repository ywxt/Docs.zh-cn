---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: 创建一个基本的 ASP.NET 4.5 Web 窗体页在 Visual Studio 2013 |Microsoft Docs
author: Erikre
description: ''
ms.author: aspnetcontent
ms.date: 03/03/2014
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: 9646aaf6d5ea13b062dbb979b0f1c759716eb7ab
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842884"
---
<a name="creating-a-basic-aspnet-45-web-forms-page-in-visual-studio-2013"></a><span data-ttu-id="2193f-102">创建一个基本的 ASP.NET 4.5 Web 窗体页在 Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2193f-102">Creating a Basic ASP.NET 4.5 Web Forms Page in Visual Studio 2013</span></span>
====================
<span data-ttu-id="2193f-103">通过[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="2193f-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="2193f-104">本演练为您提供的简介中的 Web 开发环境[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)并在[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="2193f-104">This walkthrough provides you with an introduction to the Web development environment in [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) and in [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="2193f-105">本演练指导您创建一个简单的 ASP.NET Web 窗体页面，并说明了创建新的页面、 添加控件，以及编写代码的基本技术。</span><span class="sxs-lookup"><span data-stu-id="2193f-105">This walkthrough guides you through creating a simple ASP.NET Web Forms page and illustrates the basic techniques of creating a new page, adding controls, and writing code.</span></span>

<span data-ttu-id="2193f-106">本演练涉及以下任务：</span><span class="sxs-lookup"><span data-stu-id="2193f-106">Tasks illustrated in this walkthrough include:</span></span>

- <span data-ttu-id="2193f-107">创建一个文件系统 Web 窗体应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="2193f-107">Creating a file system Web Forms application project.</span></span>
- <span data-ttu-id="2193f-108">您熟悉 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="2193f-108">Familiarizing yourself with Visual Studio.</span></span>
- <span data-ttu-id="2193f-109">创建一个 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="2193f-109">Creating an ASP.NET page.</span></span>
- <span data-ttu-id="2193f-110">添加控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-110">Adding controls.</span></span>
- <span data-ttu-id="2193f-111">添加事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="2193f-111">Adding event handlers.</span></span>
- <span data-ttu-id="2193f-112">运行和测试 Visual Studio 中的一页。</span><span class="sxs-lookup"><span data-stu-id="2193f-112">Running and testing a page from Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2193f-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="2193f-113">Prerequisites</span></span>


<span data-ttu-id="2193f-114">若要完成本演练，你将需要：</span><span class="sxs-lookup"><span data-stu-id="2193f-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="2193f-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="2193f-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="2193f-116">会自动安装.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="2193f-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="2193f-117">Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 for Web 将通常称为 Visual Studio 在整个教程系列中。</span><span class="sxs-lookup"><span data-stu-id="2193f-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="2193f-118">如果使用的 Visual Studio，本演练假定你所选**Web 开发**的设置集合，首次启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="2193f-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="2193f-119">有关详细信息，请参阅[如何： 选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2193f-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>


## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="2193f-120">创建 Web 应用程序项目和页面</span><span class="sxs-lookup"><span data-stu-id="2193f-120">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="2193f-121">在本演练的此部分中，将创建 Web 应用程序项目，并向其添加一个新页面。</span><span class="sxs-lookup"><span data-stu-id="2193f-121">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span> <span data-ttu-id="2193f-122">此外将添加 HTML 文本，并在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="2193f-122">You will also add HTML text and run the page in your browser.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="2193f-123">若要创建 Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="2193f-123">To create a Web application project</span></span>

1. <span data-ttu-id="2193f-124">打开 Microsoft Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="2193f-124">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="2193f-125">在“文件”菜单上，选择“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="2193f-125">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="2193f-126">![文件菜单](creating-a-basic-web-forms-page/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2193f-126">![File Menu](creating-a-basic-web-forms-page/_static/image1.png)</span></span>

    <span data-ttu-id="2193f-127">此时将出现 “新建项目” 对话框。</span><span class="sxs-lookup"><span data-stu-id="2193f-127">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="2193f-128">选择**模板** - &gt; **Visual C#**  - &gt; **Web**在左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="2193f-128">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="2193f-129">选择**ASP.NET Web 应用程序**在中心列中的模板。</span><span class="sxs-lookup"><span data-stu-id="2193f-129">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="2193f-130">将项目命名***BasicWebApp***然后单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="2193f-130">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="2193f-131">![新建项目对话框](creating-a-basic-web-forms-page/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="2193f-131">![New Project dialog box](creating-a-basic-web-forms-page/_static/image2.png)</span></span>
6. <span data-ttu-id="2193f-132">接下来，选择**Web 窗体**模板，然后单击**确定**按钮创建项目。</span><span class="sxs-lookup"><span data-stu-id="2193f-132">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="2193f-133">![新建 ASP.NET 项目对话框](creating-a-basic-web-forms-page/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2193f-133">![New ASP.NET Project dialog box](creating-a-basic-web-forms-page/_static/image3.png)</span></span>  

    <span data-ttu-id="2193f-134">Visual Studio 创建新的项目，包括基于 Web 窗体模板的预生成的功能。</span><span class="sxs-lookup"><span data-stu-id="2193f-134">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span> <span data-ttu-id="2193f-135">它不仅提供了与您*Home.aspx*页上， *About.aspx*页上， *Contact.aspx*页上，但还包括注册用户，并将保存的成员资格功能其凭据，以便他们可以登录到你的网站。</span><span class="sxs-lookup"><span data-stu-id="2193f-135">It not only provides you with a *Home.aspx* page, an *About.aspx* page, a *Contact.aspx* page, but also includes membership functionality that registers users and saves their credentials so that they can log in to your website.</span></span> <span data-ttu-id="2193f-136">创建一个新页面时，默认情况下 Visual Studio 将显示在页面**源**视图中，可以看到此页的 HTML 元素的位置。</span><span class="sxs-lookup"><span data-stu-id="2193f-136">When a new page is created, by default Visual Studio displays the page in **Source** view, where you can see the page's HTML elements.</span></span> <span data-ttu-id="2193f-137">下图显示了您在中会看到**源**查看如果你创建一个名为的新 Web 页*BasicWebApp.aspx*。</span><span class="sxs-lookup"><span data-stu-id="2193f-137">The following illustration shows what you would see in **Source** view if you created a new Web page named *BasicWebApp.aspx*.</span></span>  
    <span data-ttu-id="2193f-138">![源视图](creating-a-basic-web-forms-page/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="2193f-138">![Source View](creating-a-basic-web-forms-page/_static/image4.png)</span></span>


### <a name="a-tour-of-the-visual-studio-web-development-environment"></a><span data-ttu-id="2193f-139">Visual Studio Web 开发环境教程</span><span class="sxs-lookup"><span data-stu-id="2193f-139">A Tour of the Visual Studio Web Development Environment</span></span>


<span data-ttu-id="2193f-140">通过修改页面继续操作之前，最好您熟悉 Visual Studio 开发环境。</span><span class="sxs-lookup"><span data-stu-id="2193f-140">Before you proceed by modifying the page, it is useful to familiarize yourself with the Visual Studio development environment.</span></span> <span data-ttu-id="2193f-141">下图显示了 windows 和 Visual Studio 和 Visual Studio Express for Web 中提供的工具。</span><span class="sxs-lookup"><span data-stu-id="2193f-141">The following illustration shows you the windows and tools that are available in Visual Studio and Visual Studio Express for Web.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2193f-142">下图显示的默认窗口和窗口位置。</span><span class="sxs-lookup"><span data-stu-id="2193f-142">This diagram shows default windows and window locations.</span></span> <span data-ttu-id="2193f-143">**视图**菜单允许您以显示其他窗口，并重新排列和调整大小以适合您的首选项。</span><span class="sxs-lookup"><span data-stu-id="2193f-143">The **View** menu allows you to display additional windows, and to rearrange and resize windows to suit your preferences.</span></span> <span data-ttu-id="2193f-144">如果已为窗口排列方式进行更改，您看到的内容将与该图不匹配。</span><span class="sxs-lookup"><span data-stu-id="2193f-144">If changes have already been made to the window arrangement, what you see will not match the illustration.</span></span>


 <span data-ttu-id="2193f-145">在 Visual Studio 环境</span><span class="sxs-lookup"><span data-stu-id="2193f-145">The Visual Studio environment</span></span>

![Visual Studio 环境](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a><span data-ttu-id="2193f-147">熟悉 Web 设计器</span><span class="sxs-lookup"><span data-stu-id="2193f-147">Familiarize yourself with the Web designer</span></span>

<span data-ttu-id="2193f-148">检查上图中，并匹配到以下列表中，文本窗口和工具，它描述了最常使用。</span><span class="sxs-lookup"><span data-stu-id="2193f-148">Examine the above illustration and match the text to the following list, which describes the most commonly used windows and tools.</span></span> <span data-ttu-id="2193f-149">（不是所有 windows 和，请参阅此处列出的工具，只有标记都为在上图中。）</span><span class="sxs-lookup"><span data-stu-id="2193f-149">(Not all windows and tools that you see are listed here, only those marked in the preceding illustration.)</span></span>

- <span data-ttu-id="2193f-150">工具栏。</span><span class="sxs-lookup"><span data-stu-id="2193f-150">Toolbars.</span></span> <span data-ttu-id="2193f-151">提供用于格式化文本、 查找文本等命令。</span><span class="sxs-lookup"><span data-stu-id="2193f-151">Provide commands for formatting text, finding text, and so on.</span></span> <span data-ttu-id="2193f-152">仅当您正在使用时，某些工具栏才可用**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-152">Some toolbars are available only when you are working in **Design** view.</span></span>
- <span data-ttu-id="2193f-153">**解决方案资源管理器**窗口。</span><span class="sxs-lookup"><span data-stu-id="2193f-153">**Solution Explorer** window.</span></span> <span data-ttu-id="2193f-154">在 Web 应用程序中显示的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="2193f-154">Displays the files and folders in your Web application.</span></span>
- <span data-ttu-id="2193f-155">文档窗口。</span><span class="sxs-lookup"><span data-stu-id="2193f-155">Document window.</span></span> <span data-ttu-id="2193f-156">显示您正在努力在选项卡式窗口中的文档。</span><span class="sxs-lookup"><span data-stu-id="2193f-156">Displays the documents you are working on in tabbed windows.</span></span> <span data-ttu-id="2193f-157">可以通过单击选项卡在文档之间进行切换。</span><span class="sxs-lookup"><span data-stu-id="2193f-157">You can switch between documents by clicking tabs.</span></span>
- <span data-ttu-id="2193f-158">**属性**窗口。</span><span class="sxs-lookup"><span data-stu-id="2193f-158">**Properties** window.</span></span> <span data-ttu-id="2193f-159">可以更改的页面、 HTML 元素、 控件和其他对象的设置。</span><span class="sxs-lookup"><span data-stu-id="2193f-159">Allows you to change settings for the page, HTML elements, controls, and other objects.</span></span>
- <span data-ttu-id="2193f-160">查看选项卡。</span><span class="sxs-lookup"><span data-stu-id="2193f-160">View tabs.</span></span> <span data-ttu-id="2193f-161">提供在同一文档的不同视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-161">Present you with different views of the same document.</span></span> <span data-ttu-id="2193f-162">**设计**视图是附近 WYSIWYG 编辑图面。</span><span class="sxs-lookup"><span data-stu-id="2193f-162">**Design** view is a near-WYSIWYG editing surface.</span></span> <span data-ttu-id="2193f-163">**源**视图是页面的 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="2193f-163">**Source** view is the HTML editor for the page.</span></span> <span data-ttu-id="2193f-164">**拆分**视图显示两者**设计**视图和**源**文档视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-164">**Split** view displays both the **Design** view and the **Source** view for the document.</span></span> <span data-ttu-id="2193f-165">您可以使用**设计**并**源**稍后在本演练的视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-165">You will work with the **Design** and **Source** views later in this walkthrough.</span></span> <span data-ttu-id="2193f-166">如果您想打开中的网页**设计**查看，请在**工具**菜单中，单击**选项**，选择**HTML 设计器**节点，然后更改**起始页位置**选项。</span><span class="sxs-lookup"><span data-stu-id="2193f-166">If you prefer to open Web pages in **Design** view, on the **Tools** menu, click **Options**, select the **HTML Designer** node, and change the **Start Pages In** option.</span></span>
- <span data-ttu-id="2193f-167">**工具箱**。</span><span class="sxs-lookup"><span data-stu-id="2193f-167">**ToolBox**.</span></span> <span data-ttu-id="2193f-168">提供控件和 HTML 元素，您可以拖放到您的页面。</span><span class="sxs-lookup"><span data-stu-id="2193f-168">Provides controls and HTML elements that you can drag onto your page.</span></span> <span data-ttu-id="2193f-169">**工具箱**元素进行分组的公共函数。</span><span class="sxs-lookup"><span data-stu-id="2193f-169">**Toolbox** elements are grouped by common function.</span></span>
- <span data-ttu-id="2193f-170">S**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="2193f-170">S **erver Explorer**.</span></span> <span data-ttu-id="2193f-171">显示数据库连接。</span><span class="sxs-lookup"><span data-stu-id="2193f-171">Displays database connections.</span></span> <span data-ttu-id="2193f-172">如果服务器资源管理器不可见，请在视图菜单上单击服务器资源管理器。</span><span class="sxs-lookup"><span data-stu-id="2193f-172">If Server Explorer is not visible, on the View menu, click Server Explorer.</span></span>


### <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="2193f-173">创建新的 ASP.NET Web 窗体页</span><span class="sxs-lookup"><span data-stu-id="2193f-173">Creating a new ASP.NET Web Forms Page</span></span>


<span data-ttu-id="2193f-174">当您创建新的 Web 窗体应用程序使用**ASP.NET Web 应用程序**项目模板，Visual Studio 将添加名为的 ASP.NET 页 （Web 窗体页） *Default.aspx*，以及其他多个文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="2193f-174">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="2193f-175">可以使用*Default.aspx*为 Web 应用程序主页的页。</span><span class="sxs-lookup"><span data-stu-id="2193f-175">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="2193f-176">但是，对于本演练中，将创建和使用新的页面。</span><span class="sxs-lookup"><span data-stu-id="2193f-176">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="2193f-177">若要添加到 Web 应用程序页</span><span class="sxs-lookup"><span data-stu-id="2193f-177">To add a page to the Web application</span></span>


1. <span data-ttu-id="2193f-178">关闭*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="2193f-178">Close the *Default.aspx* page.</span></span> <span data-ttu-id="2193f-179">若要执行此操作，单击显示文件名称的选项卡，然后单击关闭选项。</span><span class="sxs-lookup"><span data-stu-id="2193f-179">To do this, click the tab that displays the file name and then click the close option.</span></span>
2. <span data-ttu-id="2193f-180">在中**解决方案资源管理器**，右键单击 Web 应用程序名称 (在本教程中的应用程序名称是**BasicWebSite**)，然后单击**添加** - &gt;**新项**。</span><span class="sxs-lookup"><span data-stu-id="2193f-180">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="2193f-181">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="2193f-181">The **Add New Item** dialog box is displayed.</span></span>
3. <span data-ttu-id="2193f-182">选择**Visual C#**  - &gt; **Web**在左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="2193f-182">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="2193f-183">然后，选择**Web 窗体**从中间列表并将其命名*FirstWebPage.aspx*。</span><span class="sxs-lookup"><span data-stu-id="2193f-183">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="2193f-184">![添加新项对话框](creating-a-basic-web-forms-page/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="2193f-184">![Add New Item dialog box](creating-a-basic-web-forms-page/_static/image6.png)</span></span>
4. <span data-ttu-id="2193f-185">单击**添加**将 web 页面添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="2193f-185">Click **Add** to add the web page to your project.</span></span>  
<span data-ttu-id="2193f-186">Visual Studio 创建新页面，并将其打开。</span><span class="sxs-lookup"><span data-stu-id="2193f-186">Visual Studio creates the new page and opens it.</span></span>


### <a name="adding-html-to-the-page"></a><span data-ttu-id="2193f-187">将 HTML 添加到页面</span><span class="sxs-lookup"><span data-stu-id="2193f-187">Adding HTML to the Page</span></span>


<span data-ttu-id="2193f-188">在本演练的此部分中，将向页面添加一些静态文本。</span><span class="sxs-lookup"><span data-stu-id="2193f-188">In this part of the walkthrough, you will add some static text to the page.</span></span>

### <a name="to-add-text-to-the-page"></a><span data-ttu-id="2193f-189">若要将文本添加到页面</span><span class="sxs-lookup"><span data-stu-id="2193f-189">To add text to the page</span></span>


1. <span data-ttu-id="2193f-190">在文档窗口的底部，单击**设计**选项卡以切换到**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-190">At the bottom of the document window, click the **Design** tab to switch to **Design** view.</span></span>

    <span data-ttu-id="2193f-191">设计视图中显示的当前页的类似所见即所得的方式。</span><span class="sxs-lookup"><span data-stu-id="2193f-191">Design view displays the current page in a WYSIWYG-like way.</span></span> <span data-ttu-id="2193f-192">此时，你没有任何文本或控件的页上，因此页是空白勾勒出矩形轮廓的虚线除外。</span><span class="sxs-lookup"><span data-stu-id="2193f-192">At this point, you do not have any text or controls on the page, so the page is blank except for a dashed line that outlines a rectangle.</span></span> <span data-ttu-id="2193f-193">表示此矩形**div**页上的元素。</span><span class="sxs-lookup"><span data-stu-id="2193f-193">This rectangle represents a **div** element on the page.</span></span>
2. <span data-ttu-id="2193f-194">虚线所概述的矩形内部单击。</span><span class="sxs-lookup"><span data-stu-id="2193f-194">Click inside the rectangle that is outlined by a dashed line.</span></span>
3. <span data-ttu-id="2193f-195">类型**欢迎使用 Visual Web Developer**然后按**ENTER**两次。</span><span class="sxs-lookup"><span data-stu-id="2193f-195">Type **Welcome to Visual Web Developer** and press **ENTER** twice.</span></span>

    <span data-ttu-id="2193f-196">下图显示了在您键入的文本**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-196">The following illustration shows the text you typed in **Design** view.</span></span>

    <span data-ttu-id="2193f-197">![在设计视图中的欢迎文本](creating-a-basic-web-forms-page/_static/image7.png "在设计视图中的欢迎文本")</span><span class="sxs-lookup"><span data-stu-id="2193f-197">![Welcome text in Design view](creating-a-basic-web-forms-page/_static/image7.png "Welcome text in Design view")</span></span>
4. <span data-ttu-id="2193f-198">切换到**源**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-198">Switch to **Source** view.</span></span>

    <span data-ttu-id="2193f-199">您可以看到在 HTML**源**中键入时创建的视图**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-199">You can see the HTML in **Source** view that you created when you typed in **Design** view.</span></span>  
    <span data-ttu-id="2193f-200">![包含静态文本的网页](creating-a-basic-web-forms-page/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="2193f-200">![Web Page with Static Text](creating-a-basic-web-forms-page/_static/image8.png)</span></span>


### <a name="running-the-page"></a><span data-ttu-id="2193f-201">运行页面</span><span class="sxs-lookup"><span data-stu-id="2193f-201">Running the Page</span></span>


<span data-ttu-id="2193f-202">通过将控件添加到页面继续操作之前，您可以首先运行它。</span><span class="sxs-lookup"><span data-stu-id="2193f-202">Before you proceed by adding controls to the page, you can first run it.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="2193f-203">若要运行页</span><span class="sxs-lookup"><span data-stu-id="2193f-203">To run the page</span></span>


1. <span data-ttu-id="2193f-204">在中**解决方案资源管理器**，右键单击*FirstWebPage.aspx* ，然后选择**设为起始页**。</span><span class="sxs-lookup"><span data-stu-id="2193f-204">In **Solution Explorer**, right-click *FirstWebPage.aspx* and select **Set as Start Page**.</span></span>
2. <span data-ttu-id="2193f-205">按**CTRL + F5**以运行该页。</span><span class="sxs-lookup"><span data-stu-id="2193f-205">Press **CTRL+F5** to run the page.</span></span>

    <span data-ttu-id="2193f-206">在浏览器中显示的页。</span><span class="sxs-lookup"><span data-stu-id="2193f-206">The page is displayed in the browser.</span></span> <span data-ttu-id="2193f-207">尽管你创建的页面具有的文件扩展名 *.aspx*，它当前在运行任何 HTML 页面所示。</span><span class="sxs-lookup"><span data-stu-id="2193f-207">Although the page you created has a file-name extension of *.aspx*, it currently runs like any HTML page.</span></span>

    <span data-ttu-id="2193f-208">要在浏览器中显示的页面也可以右键单击中的页**解决方案资源管理器**，然后选择**用浏览器查看**。</span><span class="sxs-lookup"><span data-stu-id="2193f-208">To display a page in the browser you can also right-click the page in **Solution Explorer** and select **View in Browser**.</span></span>
3. <span data-ttu-id="2193f-209">关闭浏览器来停止 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2193f-209">Close the browser to stop the Web application.</span></span>


## <a name="adding-and-programming-controls"></a><span data-ttu-id="2193f-210">添加和控件进行编程</span><span class="sxs-lookup"><span data-stu-id="2193f-210">Adding and Programming Controls</span></span>


<a id="sectionToggle1"></a>

<span data-ttu-id="2193f-211">现在将到页服务器控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-211">You will now add server controls to the page.</span></span> <span data-ttu-id="2193f-212">服务器控件，如按钮、 标签、 文本框、 文本框和其他熟悉的控件，提供 Web 窗体页面的典型窗体处理功能。</span><span class="sxs-lookup"><span data-stu-id="2193f-212">Server controls, such as buttons, labels, text boxes, and other familiar controls, provide typical form-processing capabilities for your Web Forms pages.</span></span> <span data-ttu-id="2193f-213">但是，可以使用在服务器上，而不是客户端运行的代码对控件进行编程。</span><span class="sxs-lookup"><span data-stu-id="2193f-213">However, you can program the controls with code that runs on the server, rather than the client.</span></span>

<span data-ttu-id="2193f-214">您将添加[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件，[文本框](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件，和一个[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)到页面控件，并编写代码来处理[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-214">You will add a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, a [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control, and a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control to the page and write code to handle the [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>

### <a name="to-add-controls-to-the-page"></a><span data-ttu-id="2193f-215">若要将控件添加到页面</span><span class="sxs-lookup"><span data-stu-id="2193f-215">To add controls to the page</span></span>


1. <span data-ttu-id="2193f-216">单击**设计**选项卡以切换到**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-216">Click the **Design** tab to switch to **Design** view.</span></span>
2. <span data-ttu-id="2193f-217">将插入点放在末尾**欢迎使用 Visual Web Developer**文本，然后按**ENTER**五次或多次以留出一些空间中的**div**元素。</span><span class="sxs-lookup"><span data-stu-id="2193f-217">Put the insertion point at the end of the **Welcome to Visual Web Developer** text and press **ENTER** five or more times to make some room in the **div** element box.</span></span>
3. <span data-ttu-id="2193f-218">在中**工具箱**，展开**标准**如果尚未展开组。</span><span class="sxs-lookup"><span data-stu-id="2193f-218">In the **Toolbox**, expand the **Standard** group if it is not already expanded.</span></span>  
<span data-ttu-id="2193f-219">请注意，可能需要展开**工具箱**窗口左侧查看它。</span><span class="sxs-lookup"><span data-stu-id="2193f-219">Note that you may need to expand the **Toolbox** window on the left to view it.</span></span>
4. <span data-ttu-id="2193f-220">拖动[文本框中](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件拖动到页面并将其中间的放**div**元素中具有**欢迎使用 Visual Web Developer**中的第一行。</span><span class="sxs-lookup"><span data-stu-id="2193f-220">Drag a [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control onto the page and drop it in the middle of the **div** element box that has **Welcome to Visual Web Developer** in the first line.</span></span>
5. <span data-ttu-id="2193f-221">拖动[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件拖动到页面并将其放到右侧[文本框中](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-221">Drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page and drop it to the right of the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control.</span></span>
6. <span data-ttu-id="2193f-222">拖动[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件拖到页面并将其放在单独的行下面[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-222">Drag a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control onto the page and drop it on a separate line below the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>
7. <span data-ttu-id="2193f-223">将插入点定位上述[文本框](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件，然后键入**输入您的姓名：** 。</span><span class="sxs-lookup"><span data-stu-id="2193f-223">Put the insertion point above the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control, and then type **Enter your name:** .</span></span>

    <span data-ttu-id="2193f-224">此静态 HTML 文本是标题[文本框中](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-224">This static HTML text is the caption for the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control.</span></span> <span data-ttu-id="2193f-225">可以混合使用静态 HTML 和同一页面上的服务器控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-225">You can mix static HTML and server controls on the same page.</span></span> <span data-ttu-id="2193f-226">下图显示了三个控件中的显示方式**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-226">The following illustration shows how the three controls appear in **Design** view.</span></span>

    <span data-ttu-id="2193f-227">![在设计视图中的三个控件](creating-a-basic-web-forms-page/_static/image9.png "在设计视图中的三个控件")</span><span class="sxs-lookup"><span data-stu-id="2193f-227">![Three controls in Design view](creating-a-basic-web-forms-page/_static/image9.png "Three controls in Design view")</span></span>


### <a name="setting-control-properties"></a><span data-ttu-id="2193f-228">设置控件属性</span><span class="sxs-lookup"><span data-stu-id="2193f-228">Setting Control Properties</span></span>


<span data-ttu-id="2193f-229">Visual Studio 提供了各种方法来设置页上的控件的属性。</span><span class="sxs-lookup"><span data-stu-id="2193f-229">Visual Studio offers you various ways to set the properties of controls on the page.</span></span> <span data-ttu-id="2193f-230">在本演练的此部分中，您将在这种设置属性**设计**视图和**源**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-230">In this part of the walkthrough, you will set properties in both **Design** view and **Source** view.</span></span>

### <a name="to-set-control-properties"></a><span data-ttu-id="2193f-231">若要设置控件属性</span><span class="sxs-lookup"><span data-stu-id="2193f-231">To set control properties</span></span>


1. <span data-ttu-id="2193f-232">首先，显示**属性**窗口中的，选择从**视图**菜单&gt;**其他 Windows**  - &gt; **属性窗口**。</span><span class="sxs-lookup"><span data-stu-id="2193f-232">First, display the **Properties** windows by selecting from the **View** menu -&gt; **Other Windows** -&gt; **Properies Window**.</span></span> <span data-ttu-id="2193f-233">或者，您可以选择**F4**以显示**属性**窗口。</span><span class="sxs-lookup"><span data-stu-id="2193f-233">You could alternatively select **F4** to display the **Properties** window.</span></span>
2. <span data-ttu-id="2193f-234">选择[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件，然后在**属性**窗口中，设置的值**文本**到**显示名称**。</span><span class="sxs-lookup"><span data-stu-id="2193f-234">Select the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, and then in the **Properties** window, set the value of **Text** to **Display Name**.</span></span> <span data-ttu-id="2193f-235">下图中所示，在设计器中，按钮上显示您输入的文本。</span><span class="sxs-lookup"><span data-stu-id="2193f-235">The text you entered appears on the button in the designer, as shown in the following illustration.</span></span>

    <span data-ttu-id="2193f-236">![设置按钮文本](creating-a-basic-web-forms-page/_static/image10.png "设置按钮文本")</span><span class="sxs-lookup"><span data-stu-id="2193f-236">![Set Button text](creating-a-basic-web-forms-page/_static/image10.png "Set Button text")</span></span>
3. <span data-ttu-id="2193f-237">切换到**源**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-237">Switch to **Source** view.</span></span>

    <span data-ttu-id="2193f-238">**源**视图显示该页面，其中包括 Visual Studio 已创建服务器控件的元素的 HTML。</span><span class="sxs-lookup"><span data-stu-id="2193f-238">**Source** view displays the HTML for the page, including the elements that Visual Studio has created for the server controls.</span></span> <span data-ttu-id="2193f-239">控件使用类似于 HTML 的语法声明，只不过标记使用前缀**asp:** 和包含该特性**runat =&quot;server&quot;**。</span><span class="sxs-lookup"><span data-stu-id="2193f-239">Controls are declared using HTML-like syntax, except that the tags use the prefix **asp:** and include the attribute **runat=&quot;server&quot;**.</span></span>

    <span data-ttu-id="2193f-240">控件属性被声明为属性。</span><span class="sxs-lookup"><span data-stu-id="2193f-240">Control properties are declared as attributes.</span></span> <span data-ttu-id="2193f-241">例如，设置[文本](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx)属性[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件，在步骤 1 中，实际在设置**文本**控件的标记中的属性。</span><span class="sxs-lookup"><span data-stu-id="2193f-241">For example, when you set the [Text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx) property for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, in step 1, you were actually setting the **Text** attribute in the control's markup.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="2193f-242">所有控件都都位于**窗体**元素，它还具有特性**runat =&quot;server&quot;**。</span><span class="sxs-lookup"><span data-stu-id="2193f-242">All the controls are inside a **form** element, which also has the attribute **runat=&quot;server&quot;**.</span></span> <span data-ttu-id="2193f-243">**Runat =&quot;服务器&quot;** 属性并**asp:** 前缀将对控件标记将控件标记，以便它们是由 ASP.NET 在服务器上处理运行时。</span><span class="sxs-lookup"><span data-stu-id="2193f-243">The **runat=&quot;server&quot;** attribute and the **asp:** prefix for control tags mark the controls so that they are processed by ASP.NET on the server when the page runs.</span></span> <span data-ttu-id="2193f-244">外部的代码**&lt;形成 runat =&quot;服务器&quot;&gt;** 并**&lt;脚本 runat =&quot;server&quot; &gt;** 元素发送到浏览器中，这就是原因 ASP.NET 代码必须位于其开始标记中包含的元素不变**runat =&quot;服务器&quot;** 属性。</span><span class="sxs-lookup"><span data-stu-id="2193f-244">Code outside of **&lt;form runat=&quot;server&quot;&gt;** and **&lt;script runat=&quot;server&quot;&gt;** elements is sent unchanged to the browser, which is why the ASP.NET code must be inside an element whose opening tag contains the **runat=&quot;server&quot;** attribute.</span></span>
4. <span data-ttu-id="2193f-245">接下来，将添加到一个附加属性[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-245">Next, you will add an additional property to the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)  control.</span></span> <span data-ttu-id="2193f-246">将插入点直接后的**asp: Label**中**&lt;asp: Label&gt;** 标记，并将然后按**空格键**。</span><span class="sxs-lookup"><span data-stu-id="2193f-246">Put the insertion point directly after **asp:Label** in the **&lt;asp:Label&gt;** tag, and then press **SPACEBAR**.</span></span>

    <span data-ttu-id="2193f-247">将显示下拉列表，显示为可以设置的可用属性的列表[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-247">A drop-down list appears that displays the list of available properties you can set for a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span> <span data-ttu-id="2193f-248">此功能，称为**智能感知**，可以帮助您应对**源**页面上的语法的服务器控件、 HTML 元素和其他项的视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-248">This feature, referred to as **IntelliSense**, helps you in **Source** view with the syntax of server controls, HTML elements, and other items on the page.</span></span> <span data-ttu-id="2193f-249">如下图所示**智能感知**下拉列表[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-249">The following illustration shows the **IntelliSense** drop-down list for the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>

    <span data-ttu-id="2193f-250">![IntelliSense 特性](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense 特性")</span><span class="sxs-lookup"><span data-stu-id="2193f-250">![IntelliSense attributes](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense attributes")</span></span>
5. <span data-ttu-id="2193f-251">选择**ForeColor** ，然后键入一个等号。</span><span class="sxs-lookup"><span data-stu-id="2193f-251">Select **ForeColor** and then type an equal sign.</span></span>

    <span data-ttu-id="2193f-252">IntelliSense 将显示一个颜色列表。</span><span class="sxs-lookup"><span data-stu-id="2193f-252">IntelliSense displays a list of colors.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="2193f-253">可以显示**智能感知**随时通过按下的下拉列表**CTRL + J**查看代码时。</span><span class="sxs-lookup"><span data-stu-id="2193f-253">You can display an **IntelliSense** drop-down list at any time by pressing **CTRL+J** when viewing code.</span></span>
6. <span data-ttu-id="2193f-254">选择的颜色**[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** 控件的文本。</span><span class="sxs-lookup"><span data-stu-id="2193f-254">Select a color for the **[Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** control's text.</span></span> <span data-ttu-id="2193f-255">请确保选择足够深，以便读取在白色背景的颜色。</span><span class="sxs-lookup"><span data-stu-id="2193f-255">Make sure you select a color that is dark enough to read against a white background.</span></span>

    <span data-ttu-id="2193f-256">**ForeColor**属性已完成，但已选择，包括右引号后面的颜色。</span><span class="sxs-lookup"><span data-stu-id="2193f-256">The **ForeColor** attribute is completed with the color that you have selected, including the closing quotation mark.</span></span>


### <a name="programming-the-button-control"></a><span data-ttu-id="2193f-257">编程的按钮控件</span><span class="sxs-lookup"><span data-stu-id="2193f-257">Programming the Button Control</span></span>


<span data-ttu-id="2193f-258">对于本演练，你将编写代码，用于读取用户在文本框中输入并随后显示中的名称的名称[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-258">For this walkthrough, you will write code that reads the name that the user enters into the text box and then displays the name in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>

### <a name="add-a-default-button-event-handler"></a><span data-ttu-id="2193f-259">添加默认按钮事件处理程序</span><span class="sxs-lookup"><span data-stu-id="2193f-259">Add a default button event handler</span></span>


1. <span data-ttu-id="2193f-260">切换到**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-260">Switch to **Design** view.</span></span>
2. <span data-ttu-id="2193f-261">双击[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-261">Double-click the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>

    <span data-ttu-id="2193f-262">默认情况下，Visual Studio 切换到代码隐藏文件，并创建主干事件处理程序[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的默认事件[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件。</span><span class="sxs-lookup"><span data-stu-id="2193f-262">By default, Visual Studio switches to a code-behind file and creates a skeleton event handler for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control's default event, the [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event.</span></span> <span data-ttu-id="2193f-263">代码隐藏文件 （如 C# 中) 在服务器代码分离开来 UI 标记 （例如 HTML)。</span><span class="sxs-lookup"><span data-stu-id="2193f-263">The code-behind file separates your UI markup (such as HTML) from your server code (such as C#).</span></span>   
   <span data-ttu-id="2193f-264">游标位于添加此事件处理程序代码。</span><span class="sxs-lookup"><span data-stu-id="2193f-264">The cursor is positioned to added code for this event handler.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="2193f-265">双击中的控件**设计**视图只会是一种方式可以创建事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="2193f-265">Double-clicking a control in **Design** view is just one of several ways you can create event handlers.</span></span>
3. <span data-ttu-id="2193f-266">内部**Button1\_单击**事件处理程序中，键入**Label1**跟一个句点 (**。**)。</span><span class="sxs-lookup"><span data-stu-id="2193f-266">Inside the **Button1\_Click** event handler, type **Label1** followed by a period (**.**).</span></span>

    <span data-ttu-id="2193f-267">当您键入超过这个有效期之后**ID**标签的 (**Label1**)，Visual Studio 将显示为可用成员列表[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控制，请在下面的示例所示图。</span><span class="sxs-lookup"><span data-stu-id="2193f-267">When you type the period after the **ID** of the label (**Label1**), Visual Studio displays a list of available members for the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control, as shown in the following illustration.</span></span> <span data-ttu-id="2193f-268">成员通常的属性、 方法或事件。</span><span class="sxs-lookup"><span data-stu-id="2193f-268">A member commonly a property, method, or event.</span></span>

    <span data-ttu-id="2193f-269">![代码视图中的 IntelliSense](creating-a-basic-web-forms-page/_static/image12.png "代码视图中的 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="2193f-269">![IntelliSense in Code view](creating-a-basic-web-forms-page/_static/image12.png "IntelliSense in Code view")</span></span>
4. <span data-ttu-id="2193f-270">完成**单击**按钮使其内容如下面的代码示例中所示的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="2193f-270">Finish the **Click** event handler for the button so that it reads as shown in the following code example.</span></span>

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. <span data-ttu-id="2193f-271">切换回查看**源**视图通过右键单击你的 HTML 标记*FirstWebPage.aspx*中**解决方案资源管理器**并选择**视图标记**。</span><span class="sxs-lookup"><span data-stu-id="2193f-271">Switch back to viewing the **Source** view of your HTML markup by right-clicking *FirstWebPage.aspx* in the **Solution Explorer** and selecting **View Markup**.</span></span>
6. <span data-ttu-id="2193f-272">滚动到**&lt;: Button&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="2193f-272">Scroll to the **&lt;asp:Button&gt;** element.</span></span> <span data-ttu-id="2193f-273">请注意， **&lt;: Button&gt;** 元素现在具有特性**onclick =&quot;Button1\_单击&quot;**。</span><span class="sxs-lookup"><span data-stu-id="2193f-273">Note that the **&lt;asp:Button&gt;** element now has the attribute **onclick=&quot;Button1\_Click&quot;**.</span></span>

    <span data-ttu-id="2193f-274">此属性将绑定的按钮[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)到上一步中编码的处理程序方法的事件。</span><span class="sxs-lookup"><span data-stu-id="2193f-274">This attribute binds the button's [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event to the handler method you coded in the previous step.</span></span>

    <span data-ttu-id="2193f-275">事件处理程序方法可以具有任何名称;显示的名称是由 Visual Studio 创建的默认名称。</span><span class="sxs-lookup"><span data-stu-id="2193f-275">Event handler methods can have any name; the name you see is the default name created by Visual Studio.</span></span> <span data-ttu-id="2193f-276">重要的一点是，该名称将用于**OnClick** HTML 中的属性必须匹配在代码隐藏中定义的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="2193f-276">The important point is that the name used for the **OnClick** attribute in the HTML must match the name of a method defined in the code-behind.</span></span>


### <a name="running-the-page"></a><span data-ttu-id="2193f-277">运行页面</span><span class="sxs-lookup"><span data-stu-id="2193f-277">Running the Page</span></span>


<span data-ttu-id="2193f-278">现在可以测试页上的服务器控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-278">You can now test the server controls on the page.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="2193f-279">若要运行页</span><span class="sxs-lookup"><span data-stu-id="2193f-279">To run the page</span></span>


1. <span data-ttu-id="2193f-280">按**CTRL + F5**以在浏览器中运行该页。</span><span class="sxs-lookup"><span data-stu-id="2193f-280">Press **CTRL+F5** to run the page in the browser.</span></span> <span data-ttu-id="2193f-281">如果发生错误，重新检查上述步骤。</span><span class="sxs-lookup"><span data-stu-id="2193f-281">If an error occurs, recheck the steps above.</span></span>
2. <span data-ttu-id="2193f-282">在文本框中输入一个名称，然后单击**显示名称**按钮。</span><span class="sxs-lookup"><span data-stu-id="2193f-282">Enter a name into the text box and click the **Display Name** button.</span></span>

    <span data-ttu-id="2193f-283">您输入的名称显示在[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-283">The name you entered is displayed in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span> <span data-ttu-id="2193f-284">请注意，当单击按钮时，页面将被发送到 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="2193f-284">Note that when you click the button, the page is posted to the Web server.</span></span> <span data-ttu-id="2193f-285">ASP.NET 然后重新创建该页，运行你的代码 (在这种情况下，[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件处理程序将运行)，然后将新页发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="2193f-285">ASP.NET then recreates the page, runs your code (in this case, the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control's [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event handler runs), and then sends the new page to the browser.</span></span> <span data-ttu-id="2193f-286">如果你观看在浏览器中的状态栏，可以看到，页面往返到 Web 服务器每次单击按钮。</span><span class="sxs-lookup"><span data-stu-id="2193f-286">If you watch the status bar in the browser, you can see that the page is making a round trip to the Web server each time you click the button.</span></span>
3. <span data-ttu-id="2193f-287">在浏览器中，查看正在运行的页上右键单击并选择页面的源代码**查看源**。</span><span class="sxs-lookup"><span data-stu-id="2193f-287">In the browser, view the source of the page you are running by right-clicking on the page and selecting **View source**.</span></span>

    <span data-ttu-id="2193f-288">在页的源代码，可以看到 HTML 而无需任何服务器代码。</span><span class="sxs-lookup"><span data-stu-id="2193f-288">In the page source code, you see HTML without any server code.</span></span> <span data-ttu-id="2193f-289">具体而言，未看到**&lt;asp:&gt;** 你正在使用中的元素**源**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-289">Specifically, you do not see the **&lt;asp:&gt;** elements that you were working with in **Source** view.</span></span> <span data-ttu-id="2193f-290">页运行时，ASP.NET 会处理服务器控件，并呈现到页的 HTML 元素，可执行表示控件的功能。</span><span class="sxs-lookup"><span data-stu-id="2193f-290">When the page runs, ASP.NET processes the server controls and renders HTML elements to the page that perform the functions that represent the control.</span></span> <span data-ttu-id="2193f-291">例如， **&lt;: Button&gt;** 控件呈现为 HTML **&lt;输入类型 =&quot;提交&quot;&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="2193f-291">For example, the **&lt;asp:Button&gt;** control is rendered as the HTML **&lt;input type=&quot;submit&quot;&gt;** element.</span></span>
4. <span data-ttu-id="2193f-292">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="2193f-292">Close the browser.</span></span>


## <a name="working-with-additional-controls"></a><span data-ttu-id="2193f-293">中的其他控件</span><span class="sxs-lookup"><span data-stu-id="2193f-293">Working with Additional Controls</span></span>

<a id="sectionToggle2"></a>

<span data-ttu-id="2193f-294">在本演练的此部分中，您可以使用[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件，用于一次显示一个月的日期。</span><span class="sxs-lookup"><span data-stu-id="2193f-294">In this part of the walkthrough, you will work with the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control, which displays dates a month at a time.</span></span> <span data-ttu-id="2193f-295">[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件是一个更复杂比你一直使用的按钮、 文本框中和标签控件，并说明了服务器控件的一些其他功能。</span><span class="sxs-lookup"><span data-stu-id="2193f-295">The [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control is a more complex control than the button, text box, and label you have been working with and illustrates some further capabilities of server controls.</span></span>

<span data-ttu-id="2193f-296">在本部分中，您将添加[System.Web.UI.WebControls.Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制对页面并设置其格式。</span><span class="sxs-lookup"><span data-stu-id="2193f-296">In this section, you will add a [System.Web.UI.WebControls.Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control to the page and format it.</span></span>

### <a name="to-add-a-calendar-control"></a><span data-ttu-id="2193f-297">若要添加一个日历控件</span><span class="sxs-lookup"><span data-stu-id="2193f-297">To add a Calendar control</span></span>


1. <span data-ttu-id="2193f-298">在 Visual Studio 中，切换到**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-298">In Visual Studio, switch to **Design** view.</span></span>
2. <span data-ttu-id="2193f-299">从**标准**一部分**工具箱**，拖动[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)拖放到页面上控制**div**元素，包含其他控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-299">From the **Standard** section of the **Toolbox**, drag a [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control onto the page and drop it below the **div** element that contains the other controls.</span></span>

    <span data-ttu-id="2193f-300">显示日历的智能标记面板。</span><span class="sxs-lookup"><span data-stu-id="2193f-300">The calendar's smart tag panel is displayed.</span></span> <span data-ttu-id="2193f-301">面板将显示命令，可以轻松为选定的控件执行的最常见任务。</span><span class="sxs-lookup"><span data-stu-id="2193f-301">The panel displays commands that make it easy for you to perform the most common tasks for the selected control.</span></span> <span data-ttu-id="2193f-302">如下图所示[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制中呈现**设计**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-302">The following illustration shows the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control as rendered in **Design** view.</span></span>

    <span data-ttu-id="2193f-303">![月历控件在设计视图](creating-a-basic-web-forms-page/_static/image13.png "月历控件在设计视图")</span><span class="sxs-lookup"><span data-stu-id="2193f-303">![Calendar control in Design view](creating-a-basic-web-forms-page/_static/image13.png "Calendar control in Design view")</span></span>
3. <span data-ttu-id="2193f-304">在智能标记面板中，选择**自动套用格式**。</span><span class="sxs-lookup"><span data-stu-id="2193f-304">In the smart tag panel, choose **Auto Format**.</span></span>

    <span data-ttu-id="2193f-305">**自动套用格式**显示对话框，该编辑器可以为该日历选择一个格式设置方案。</span><span class="sxs-lookup"><span data-stu-id="2193f-305">The **Auto Format** dialog box is displayed, which allows you to select a formatting scheme for the calendar.</span></span> <span data-ttu-id="2193f-306">如下图所示**自动套用格式**对话框[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-306">The following illustration shows the **Auto Format** dialog box for the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control.</span></span>

    <span data-ttu-id="2193f-307">![自动格式对话框 （Calendar 控件）](creating-a-basic-web-forms-page/_static/image14.png "自动套用格式对话框 （Calendar 控件）")</span><span class="sxs-lookup"><span data-stu-id="2193f-307">![Auto Format dialog box (Calendar control)](creating-a-basic-web-forms-page/_static/image14.png "Auto Format dialog box (Calendar control)")</span></span>
4. <span data-ttu-id="2193f-308">从**选择一种方案**列表中，选择**简单**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="2193f-308">From the **Select a scheme** list, select **Simple** and then click **OK**.</span></span>
5. <span data-ttu-id="2193f-309">切换到**源**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-309">Switch to **Source** view.</span></span>

    <span data-ttu-id="2193f-310">您可以看到 **&lt;asp： 日历&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="2193f-310">You can see the **&lt;asp:Calendar&gt;** element.</span></span> <span data-ttu-id="2193f-311">此元素是远远超过前面创建的简单控件的元素。</span><span class="sxs-lookup"><span data-stu-id="2193f-311">This element is much longer than the elements for the simple controls you created earlier.</span></span> <span data-ttu-id="2193f-312">它还包括子元素，如 **&lt;WeekEndDayStyle&gt;**，这表示各种格式设置。</span><span class="sxs-lookup"><span data-stu-id="2193f-312">It also includes subelements, such as **&lt;WeekEndDayStyle&gt;**, which represent various formatting settings.</span></span> <span data-ttu-id="2193f-313">如下图所示[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制**源**视图。</span><span class="sxs-lookup"><span data-stu-id="2193f-313">The following illustration shows the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control in **Source** view.</span></span> <span data-ttu-id="2193f-314">(请参阅中的确切标记**源**视图可能略有不同的图。)</span><span class="sxs-lookup"><span data-stu-id="2193f-314">(The exact markup that you see in **Source** view might differ slightly from the illustration.)</span></span>

    <span data-ttu-id="2193f-315">![月历控件在源视图](creating-a-basic-web-forms-page/_static/image15.png "月历控件在源视图中")</span><span class="sxs-lookup"><span data-stu-id="2193f-315">![Calendar control in Source view](creating-a-basic-web-forms-page/_static/image15.png "Calendar control in Source view")</span></span>


### <a name="programming-the-calendar-control"></a><span data-ttu-id="2193f-316">日历控件编程</span><span class="sxs-lookup"><span data-stu-id="2193f-316">Programming the Calendar Control</span></span>


<span data-ttu-id="2193f-317">在本部分中，将编程[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件来显示当前选定的日期。</span><span class="sxs-lookup"><span data-stu-id="2193f-317">In this section, you will program the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control to display the currently selected date.</span></span>

### <a name="to-program-the-calendar-control"></a><span data-ttu-id="2193f-318">日历控件编程</span><span class="sxs-lookup"><span data-stu-id="2193f-318">To program the Calendar control</span></span>


1. <span data-ttu-id="2193f-319">在中**设计**视图中，双击[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-319">In **Design** view, double-click the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control.</span></span>

    <span data-ttu-id="2193f-320">创建新的事件处理程序并将其显示在代码隐藏文件中名为*FirstWebPage.aspx.cs*。</span><span class="sxs-lookup"><span data-stu-id="2193f-320">A new event handler is created and displayed in the code-behind file named *FirstWebPage.aspx.cs*.</span></span>
2. <span data-ttu-id="2193f-321">完成[SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx)事件处理程序替换下面的代码。</span><span class="sxs-lookup"><span data-stu-id="2193f-321">Finish the [SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx) event handler with the following code.</span></span>

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]


    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]

    <span data-ttu-id="2193f-322">上面的代码中设置为所选日期的日历控件的标签控件的文本。</span><span class="sxs-lookup"><span data-stu-id="2193f-322">The above code sets the text of the label control to the selected date of the calendar control.</span></span>


### <a name="running-the-page"></a><span data-ttu-id="2193f-323">运行页面</span><span class="sxs-lookup"><span data-stu-id="2193f-323">Running the Page</span></span>


<span data-ttu-id="2193f-324">现在可以测试日历。</span><span class="sxs-lookup"><span data-stu-id="2193f-324">You can now test the calendar.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="2193f-325">若要运行页</span><span class="sxs-lookup"><span data-stu-id="2193f-325">To run the page</span></span>


1. <span data-ttu-id="2193f-326">按**CTRL + F5**以在浏览器中运行该页。</span><span class="sxs-lookup"><span data-stu-id="2193f-326">Press **CTRL+F5** to run the page in the browser.</span></span>
2. <span data-ttu-id="2193f-327">单击日历中的日期。</span><span class="sxs-lookup"><span data-stu-id="2193f-327">Click a date in the calendar.</span></span>

    <span data-ttu-id="2193f-328">在显示你单击的日期[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="2193f-328">The date you clicked is displayed in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>
3. <span data-ttu-id="2193f-329">在浏览器中查看页面的源代码。</span><span class="sxs-lookup"><span data-stu-id="2193f-329">In the browser, view the source code for the page.</span></span>

    <span data-ttu-id="2193f-330">请注意，[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制呈现给页面**表**，为每个日期**td**元素。</span><span class="sxs-lookup"><span data-stu-id="2193f-330">Note that the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control has been rendered to the page as a **table**, with each day as a **td** element.</span></span>
4. <span data-ttu-id="2193f-331">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="2193f-331">Close the browser.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2193f-332">后续步骤</span><span class="sxs-lookup"><span data-stu-id="2193f-332">Next Steps</span></span>


<a id="nextStepsToggle"></a>

<span data-ttu-id="2193f-333">本演练演示了 Visual Studio 页面设计器的基本功能。</span><span class="sxs-lookup"><span data-stu-id="2193f-333">This walkthrough has illustrated the basic features of the Visual Studio page designer.</span></span> <span data-ttu-id="2193f-334">现在，你已了解如何创建和编辑 Visual Studio 中的 Web 窗体页，您可能想要探索其他功能。</span><span class="sxs-lookup"><span data-stu-id="2193f-334">Now that you understand how to create and edit a Web Forms page in Visual Studio, you might want to explore other features.</span></span> <span data-ttu-id="2193f-335">例如，你可能想要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="2193f-335">For example, you might want to do the following:</span></span>

- <span data-ttu-id="2193f-336">按照以下分步教程系列中了解有关 ASP.NET Web 窗体的详细信息[Getting Started with ASP.NET 4.5 Web 窗体和 Visual Studio 2013](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2193f-336">Learn more about ASP.NET Web Forms by following the step-by-step tutorial series [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md).</span></span>
- <span data-ttu-id="2193f-337">了解有关级联样式表 (CSS) 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="2193f-337">Learn more about Cascading style sheets (CSS).</span></span> <span data-ttu-id="2193f-338">有关详细信息，请参阅[使用 CSS 概述](https://msdn.microsoft.com/library/bb398931.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2193f-338">For details, see [Working with CSS Overview](https://msdn.microsoft.com/library/bb398931.aspx).</span></span>
