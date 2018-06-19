---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
title: UI 和导航 |Microsoft 文档
author: Erikre
description: 本系列教程将教您生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 5c76891d-e515-4885-b576-76bd2c494efe
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
msc.type: authoredcontent
ms.openlocfilehash: d2d4101455a85c53e016e567c0cf1337642f1863
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30890237"
---
<a name="ui-and-navigation"></a><span data-ttu-id="5193b-103">UI 和导航</span><span class="sxs-lookup"><span data-stu-id="5193b-103">UI and Navigation</span></span>
====================
<span data-ttu-id="5193b-104">通过[艾力克 Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="5193b-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="5193b-105">[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="5193b-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="5193b-106">本系列教程将教您构建使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的 ASP.NET Web 窗体应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="5193b-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="5193b-107">Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)是可以附带本系列教程。</span><span class="sxs-lookup"><span data-stu-id="5193b-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="5193b-108">在本教程中，你将要修改默认 Web 应用程序以支持 Wingtip Toys 应用商店前端应用程序的功能的 UI。</span><span class="sxs-lookup"><span data-stu-id="5193b-108">In this tutorial, you will modify the UI of the default Web application to support features of the Wingtip Toys store front application.</span></span> <span data-ttu-id="5193b-109">此外，你将添加简单和数据绑定导航。</span><span class="sxs-lookup"><span data-stu-id="5193b-109">Also, you will add simple and data bound navigation.</span></span> <span data-ttu-id="5193b-110">本教程以前一教程"创建数据访问层"上构建，并为 Wingtip Toys 教程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="5193b-110">This tutorial builds on the previous tutorial "Create the Data Access Layer" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="5193b-111">你将学习：</span><span class="sxs-lookup"><span data-stu-id="5193b-111">What you'll learn:</span></span>

- <span data-ttu-id="5193b-112">如何更改 UI 以支持 Wingtip Toys 应用商店前端应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="5193b-112">How to change the UI to support features of the Wingtip Toys store front application.</span></span>
- <span data-ttu-id="5193b-113">如何配置包括页面导航中的 HTML5 元素。</span><span class="sxs-lookup"><span data-stu-id="5193b-113">How to configure an HTML5 element to include page navigation.</span></span>
- <span data-ttu-id="5193b-114">如何创建数据驱动的控件，若要导航到特定的产品数据。</span><span class="sxs-lookup"><span data-stu-id="5193b-114">How to create a data-driven control to navigate to specific product data.</span></span>
- <span data-ttu-id="5193b-115">如何显示来自数据库使用 Entity Framework Code First 创建的数据。</span><span class="sxs-lookup"><span data-stu-id="5193b-115">How to display data from a database created using Entity Framework Code First.</span></span>

<span data-ttu-id="5193b-116">ASP.NET Web 窗体，可以创建 Web 应用程序的动态内容。</span><span class="sxs-lookup"><span data-stu-id="5193b-116">ASP.NET Web Forms allow you to create dynamic content for your Web application.</span></span> <span data-ttu-id="5193b-117">每个 ASP.NET Web 页创建的方式类似到静态 HTML 网页上 （不包括基于服务器的处理页），但 ASP.NET Web 页包括额外的元素，ASP.NET 识别并处理页将运行时生成 HTML。</span><span class="sxs-lookup"><span data-stu-id="5193b-117">Each ASP.NET Web page is created in a manner similar to a static HTML Web page (a page that does not include server-based processing), but ASP.NET Web page includes extra elements that ASP.NET recognizes and processes to generate HTML when the page runs.</span></span>

<span data-ttu-id="5193b-118">与静态 HTML 页面 (*.htm*或 *.html*文件)，服务器担当`Web`通过读取文件并将其作为发送的请求-在浏览器。</span><span class="sxs-lookup"><span data-stu-id="5193b-118">With a static HTML page (*.htm* or *.html* file), the server fulfills a `Web` request by reading the file and sending it as-is to the browser.</span></span> <span data-ttu-id="5193b-119">有人与此相反，当请求 ASP.NET 网页 (*.aspx*文件)，该页在 Web 服务器上运行的程序。</span><span class="sxs-lookup"><span data-stu-id="5193b-119">In contrast, when someone requests an ASP.NET Web page (*.aspx* file), the page runs as a program on the Web server.</span></span> <span data-ttu-id="5193b-120">在运行页面时，它可以执行您的网站需要，包括计算值、 读取或写入数据库信息，或调用其他程序的任何任务。</span><span class="sxs-lookup"><span data-stu-id="5193b-120">While the page is running, it can perform any task that your Web site requires, including calculating values, reading or writing database information, or calling other programs.</span></span> <span data-ttu-id="5193b-121">作为其输出，该页面动态生成标记 （例如 HTML 中的元素），并将此动态输出发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="5193b-121">As its output, the page dynamically produces markup (such as elements in HTML) and sends this dynamic output to the browser.</span></span>

## <a name="modifying-the-ui"></a><span data-ttu-id="5193b-122">修改 UI</span><span class="sxs-lookup"><span data-stu-id="5193b-122">Modifying the UI</span></span>

<span data-ttu-id="5193b-123">你将通过修改继续本教程系列*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="5193b-123">You'll continue this tutorial series by modifying the *Default.aspx* page.</span></span> <span data-ttu-id="5193b-124">您将修改用于创建应用程序的默认模板已建立的 UI。</span><span class="sxs-lookup"><span data-stu-id="5193b-124">You will modify the UI that's already established by the default template used to create the application.</span></span> <span data-ttu-id="5193b-125">创建任何 Web 窗体应用程序时，你将执行的修改的类型是典型的。</span><span class="sxs-lookup"><span data-stu-id="5193b-125">The type of modifications you'll do are typical when creating any Web Forms application.</span></span> <span data-ttu-id="5193b-126">你将执行此更改的标题、 替换一些内容，并删除不需要的默认内容。</span><span class="sxs-lookup"><span data-stu-id="5193b-126">You'll do this by changing the title, replacing some content, and removing unneeded default content.</span></span>

1. <span data-ttu-id="5193b-127">打开或切换到*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="5193b-127">Open or switch to the *Default.aspx* page.</span></span>
2. <span data-ttu-id="5193b-128">如果在显示的页面**设计**视图中，切换到**源**视图。</span><span class="sxs-lookup"><span data-stu-id="5193b-128">If the page appears in **Design** view, switch to **Source** view.</span></span>
3. <span data-ttu-id="5193b-129">在中的页面顶部`@Page`指令，更改`Title`属性设为"欢迎"，如下所示在下面的黄色突出显示。</span><span class="sxs-lookup"><span data-stu-id="5193b-129">At the top of the page in the `@Page` directive, change the `Title` attribute to "Welcome", as shown highlighted in yellow below.</span></span> 

    [!code-aspx[Main](ui_and_navigation/samples/sample1.aspx?highlight=1)]
4. <span data-ttu-id="5193b-130">同样，在*Default.aspx*页上，将替换默认的内容中包含的所有`<asp:Content>`添加标记以便标记显示为下面。</span><span class="sxs-lookup"><span data-stu-id="5193b-130">Also on the *Default.aspx* page, replace all of the default content contained in the `<asp:Content>` tag so that the markup appears as below.</span></span> 

    [!code-aspx[Main](ui_and_navigation/samples/sample2.aspx)]
5. <span data-ttu-id="5193b-131">保存*Default.aspx*页上通过选择**保存 Default.aspx**从**文件**菜单。</span><span class="sxs-lookup"><span data-stu-id="5193b-131">Save the *Default.aspx* page by selecting **Save Default.aspx** from the **File** menu.</span></span>

   <span data-ttu-id="5193b-132">生成*Default.aspx*页将出现，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5193b-132">The resulting *Default.aspx* page will appear as follows:</span></span> 

[!code-aspx[Main](ui_and_navigation/samples/sample3.aspx)]

<span data-ttu-id="5193b-133">在示例中，设置`Title`属性`@Page`指令。</span><span class="sxs-lookup"><span data-stu-id="5193b-133">In the example, you have set the `Title` attribute of the `@Page` directive.</span></span> <span data-ttu-id="5193b-134">在浏览器中，服务器代码中显示 HTML 时`<%: Page.Title %>`解析为中包含的内容`Title`属性。</span><span class="sxs-lookup"><span data-stu-id="5193b-134">When the HTML is displayed in a browser, the server code `<%: Page.Title %>` resolves to the content contained in the `Title` attribute.</span></span>

<span data-ttu-id="5193b-135">该示例页面包括构成 ASP.NET 网页的基本元素。</span><span class="sxs-lookup"><span data-stu-id="5193b-135">The example page includes the basic elements that constitute an ASP.NET Web page.</span></span> <span data-ttu-id="5193b-136">此页包含静态文本，你可能可以在 HTML 页，以及特定于 ASP.NET 的元素。</span><span class="sxs-lookup"><span data-stu-id="5193b-136">The page contains static text as you might have in an HTML page, along with elements that are specific to ASP.NET.</span></span> <span data-ttu-id="5193b-137">中包含的内容*Default.aspx*将与母版页的内容，它将在本教程后面部分所述集成页。</span><span class="sxs-lookup"><span data-stu-id="5193b-137">The content contained in the *Default.aspx* page will be integrated with the master page content, which will be explained later in this tutorial.</span></span>

### <a name="page-directive"></a><span data-ttu-id="5193b-138">@Page 指令</span><span class="sxs-lookup"><span data-stu-id="5193b-138">@Page Directive</span></span>

<span data-ttu-id="5193b-139">ASP.NET Web 窗体通常包含允许你指定的页的页属性和配置信息的指令。</span><span class="sxs-lookup"><span data-stu-id="5193b-139">ASP.NET Web Forms usually contain directives that allow you to specify page properties and configuration information for the page.</span></span> <span data-ttu-id="5193b-140">指令用作 asp.net 说明有关如何为进程页面，但它们不会呈现到浏览器发送的标记的一部分。</span><span class="sxs-lookup"><span data-stu-id="5193b-140">The directives are used by ASP.NET as instructions for how to process the page, but they are not rendered as part of the markup that is sent to the browser.</span></span>

<span data-ttu-id="5193b-141">最常使用的指令`@Page`指令，该对话框可以指定多个配置选项页，其中包括：</span><span class="sxs-lookup"><span data-stu-id="5193b-141">The most commonly used directive is the `@Page` directive, which allows you to specify many configuration options for the page, including the following:</span></span>

1. <span data-ttu-id="5193b-142">编程语言在页中，如 C# 代码的服务器。</span><span class="sxs-lookup"><span data-stu-id="5193b-142">The server programming language for code in the page, such as C#.</span></span>
2. <span data-ttu-id="5193b-143">该页是否是用服务器代码直接在页中，这称为单文件页，页，或者它是否是在单独的类文件，称为代码隐藏页中使用代码页。</span><span class="sxs-lookup"><span data-stu-id="5193b-143">Whether the page is a page with server code directly in the page, which is called a single-file page, or whether it is a page with code in a separate class file, which is called a code-behind page.</span></span>
3. <span data-ttu-id="5193b-144">是否页都有关联的母版页，并因此会被视为内容页。</span><span class="sxs-lookup"><span data-stu-id="5193b-144">Whether the page has an associated master page and should therefore be treated as a content page.</span></span>
4. <span data-ttu-id="5193b-145">调试和跟踪选项。</span><span class="sxs-lookup"><span data-stu-id="5193b-145">Debugging and tracing options.</span></span>

<span data-ttu-id="5193b-146">如果不包括`@Page`指令在页中，或如果该指令不包括特定设置，将从继承设置*Web.config*配置文件或从*Machine.config*配置文件。</span><span class="sxs-lookup"><span data-stu-id="5193b-146">If you do not include an `@Page` directive in the page, or if the directive does not include a specific setting, a setting will be inherited from the *Web.config* configuration file or from the *Machine.config* configuration file.</span></span> <span data-ttu-id="5193b-147">*Machine.config*文件提供对所有应用程序的计算机上运行的其他配置设置。</span><span class="sxs-lookup"><span data-stu-id="5193b-147">The *Machine.config* file provides additional configuration settings to all applications running on a machine.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5193b-148">*Machine.config*还提供有关所有可能的配置设置的详细信息。</span><span class="sxs-lookup"><span data-stu-id="5193b-148">The *Machine.config* also provides details about all possible configuration settings.</span></span>


### <a name="web-server-controls"></a><span data-ttu-id="5193b-149">Web 服务器控件</span><span class="sxs-lookup"><span data-stu-id="5193b-149">Web Server Controls</span></span>

<span data-ttu-id="5193b-150">在大多数的 ASP.NET Web 窗体应用程序，你将添加允许用户与页面，如按钮、 文本框、 列表和等等交互的控件。</span><span class="sxs-lookup"><span data-stu-id="5193b-150">In most ASP.NET Web Forms applications, you will add controls that allow the user to interact with the page, such as buttons, text boxes, lists, and so on.</span></span> <span data-ttu-id="5193b-151">这些 Web 服务器控件都类似于 HTML 按钮和输入的元素。</span><span class="sxs-lookup"><span data-stu-id="5193b-151">These Web server controls are similar to HTML buttons and input elements.</span></span> <span data-ttu-id="5193b-152">但是，它们进行处理在服务器上，让你能够使用服务器代码设置其属性。</span><span class="sxs-lookup"><span data-stu-id="5193b-152">However, they are processed on the server, allowing you to use server code to set their properties.</span></span> <span data-ttu-id="5193b-153">这些控件还引发你可以在服务器代码中处理的事件。</span><span class="sxs-lookup"><span data-stu-id="5193b-153">These controls also raise events that you can handle in server code.</span></span>

<span data-ttu-id="5193b-154">服务器控件使用 ASP.NET 识别运行页面时的特殊语法。</span><span class="sxs-lookup"><span data-stu-id="5193b-154">Server controls use a special syntax that ASP.NET recognizes when the page runs.</span></span> <span data-ttu-id="5193b-155">ASP.NET 服务器控件的标记名称开头`asp:`前缀。</span><span class="sxs-lookup"><span data-stu-id="5193b-155">The tag name for ASP.NET server controls starts with an `asp:` prefix.</span></span> <span data-ttu-id="5193b-156">这使 ASP.NET 可以识别并处理这些服务器控件。</span><span class="sxs-lookup"><span data-stu-id="5193b-156">This allows ASP.NET to recognize and process these server controls.</span></span> <span data-ttu-id="5193b-157">如果控件不是.NET Framework 的一部分，前缀可能有所不同。</span><span class="sxs-lookup"><span data-stu-id="5193b-157">The prefix might be different if the control is not part of the .NET Framework.</span></span> <span data-ttu-id="5193b-158">除了`asp:`前缀，ASP.NET 服务器控件还包括`runat="server"`属性和`ID`，你可以使用引用服务器代码中的控件。</span><span class="sxs-lookup"><span data-stu-id="5193b-158">In addition to the `asp:` prefix, ASP.NET server controls also include the `runat="server"` attribute and an `ID` that you can use to reference the control in server code.</span></span>

<span data-ttu-id="5193b-159">页运行时，ASP.NET 标识服务器控件，并运行的代码，这些控件与相关联。</span><span class="sxs-lookup"><span data-stu-id="5193b-159">When the page runs, ASP.NET identifies the server controls and runs the code that is associated with those controls.</span></span> <span data-ttu-id="5193b-160">在浏览器中显示时，很多控件呈现到页一些 HTML 或其他标记。</span><span class="sxs-lookup"><span data-stu-id="5193b-160">Many controls render some HTML or other markup into the page when it is displayed in a browser.</span></span>

### <a name="server-code"></a><span data-ttu-id="5193b-161">服务器代码</span><span class="sxs-lookup"><span data-stu-id="5193b-161">Server Code</span></span>

<span data-ttu-id="5193b-162">大多数 ASP.NET Web 窗体应用程序包括在页处理时，在服务器运行的代码。</span><span class="sxs-lookup"><span data-stu-id="5193b-162">Most ASP.NET Web Forms applications include code that runs on the server when the page is processed.</span></span> <span data-ttu-id="5193b-163">如上所述，服务器代码可以用于执行各种操作，例如将数据添加到 ListView 控件。</span><span class="sxs-lookup"><span data-stu-id="5193b-163">As mentioned above, server code can be used to do a variety of things, such as adding data to a ListView control.</span></span> <span data-ttu-id="5193b-164">ASP.NET 支持的许多语言包括 C#、 Visual Basic、 J# 中，和其他人在服务器上运行。</span><span class="sxs-lookup"><span data-stu-id="5193b-164">ASP.NET supports many languages to run on the server, including C#, Visual Basic, J#, and others.</span></span>

<span data-ttu-id="5193b-165">ASP.NET 支持用于编写用于网页的服务器代码的两个模型。</span><span class="sxs-lookup"><span data-stu-id="5193b-165">ASP.NET supports two models for writing server code for a Web page.</span></span> <span data-ttu-id="5193b-166">在单文件模型中，页的代码是在脚本元素，其中包括开始标记中`runat="server"`属性。</span><span class="sxs-lookup"><span data-stu-id="5193b-166">In the single-file model, the code for the page is in a script element where the opening tag includes the `runat="server"` attribute.</span></span> <span data-ttu-id="5193b-167">或者，你可以在单独的类文件中，称为代码隐藏模型创建页的代码。</span><span class="sxs-lookup"><span data-stu-id="5193b-167">Alternatively, you can create the code for the page in a separate class file, which is referred to as the code-behind model.</span></span> <span data-ttu-id="5193b-168">在这种情况下，ASP.NET Web 窗体页通常不包含服务器代码。</span><span class="sxs-lookup"><span data-stu-id="5193b-168">In this case, the ASP.NET Web Forms page generally contains no server code.</span></span> <span data-ttu-id="5193b-169">相反，`@Page`指令包含的信息的链接 *.aspx*与其关联的代码隐藏文件的页。</span><span class="sxs-lookup"><span data-stu-id="5193b-169">Instead, the `@Page` directive includes information that links the *.aspx* page with its associated code-behind file.</span></span>

<span data-ttu-id="5193b-170">`CodeBehind`属性中包含`@Page`指令指定单独的类文件的名称和`Inherits`特性指定对应于页的代码隐藏文件中的类的名称。</span><span class="sxs-lookup"><span data-stu-id="5193b-170">The `CodeBehind` attribute contained in the `@Page` directive specifies the name of the separate class file, and the `Inherits` attribute specifies the name of the class within the code-behind file that corresponds to the page.</span></span>

### <a name="updating-the-master-page"></a><span data-ttu-id="5193b-171">更新母版页</span><span class="sxs-lookup"><span data-stu-id="5193b-171">Updating the Master Page</span></span>

<span data-ttu-id="5193b-172">在 ASP.NET Web 窗体、 主控页，可以在你的应用程序中创建一致的布局的页。</span><span class="sxs-lookup"><span data-stu-id="5193b-172">In ASP.NET Web Forms, master pages allow you to create a consistent layout for the pages in your application.</span></span> <span data-ttu-id="5193b-173">使用单个母版页定义应用程序中的外观和感觉和所需的所有页 （或一组页） 的标准行为。</span><span class="sxs-lookup"><span data-stu-id="5193b-173">A single master page defines the look and feel and standard behavior that you want for all of the pages (or a group of pages) in your application.</span></span> <span data-ttu-id="5193b-174">然后可以创建包含你想要显示，如上文所述的内容的各个内容页。</span><span class="sxs-lookup"><span data-stu-id="5193b-174">You can then create individual content pages that contain the content you want to display, as explained above.</span></span> <span data-ttu-id="5193b-175">当用户请求内容页时，ASP.NET 会将其合并以生成将主控页的布局与内容页中的内容相结合的输出与该母版页。</span><span class="sxs-lookup"><span data-stu-id="5193b-175">When users request the content pages, ASP.NET merges them with the master page to produce output that combines the layout of the master page with the content from the content page.</span></span>

<span data-ttu-id="5193b-176">新站点需要要显示每一页上的单个徽标。</span><span class="sxs-lookup"><span data-stu-id="5193b-176">The new site needs a single logo to display on every page.</span></span> <span data-ttu-id="5193b-177">若要添加此徽标，你可以修改母版页上的 HTML。</span><span class="sxs-lookup"><span data-stu-id="5193b-177">To add this logo, you can modify the HTML on the master page.</span></span>

1. <span data-ttu-id="5193b-178">在**解决方案资源管理器**，找到并打开**Site.Master**页。</span><span class="sxs-lookup"><span data-stu-id="5193b-178">In **Solution Explorer**, find and open the **Site.Master** page.</span></span>
2. <span data-ttu-id="5193b-179">如果该页面的是**设计**视图中，切换到**源**视图。</span><span class="sxs-lookup"><span data-stu-id="5193b-179">If the page is in **Design** view, switch to **Source** view.</span></span>
3. <span data-ttu-id="5193b-180">更新母版页由**修改或添加**以黄色突出显示的标记：</span><span class="sxs-lookup"><span data-stu-id="5193b-180">Update the master page by **modifying or adding** the markup highlighted in yellow:</span></span> 

    [!code-aspx[Main](ui_and_navigation/samples/sample4.aspx?highlight=9,49,76-81,87)]

<span data-ttu-id="5193b-181">以下 HTML 将显示名为映像*logo.jpg*从*映像*稍后将添加的 Web 应用程序的文件夹。</span><span class="sxs-lookup"><span data-stu-id="5193b-181">This HTML will display the image named *logo.jpg* from the *Images* folder of the Web application, which you'll add later.</span></span> <span data-ttu-id="5193b-182">使用母版页的页显示时在浏览器中，将显示的徽标。</span><span class="sxs-lookup"><span data-stu-id="5193b-182">When a page that uses the master page is displayed in a browser, the logo will be displayed.</span></span> <span data-ttu-id="5193b-183">如果用户单击徽标，用户将向后定位到*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="5193b-183">If a user clicks on the logo, the user will navigate back to the *Default.aspx* page.</span></span> <span data-ttu-id="5193b-184">HTML 定位点标记`<a>`包装映像服务器控件，并允许图像的链接的一部分。</span><span class="sxs-lookup"><span data-stu-id="5193b-184">The HTML anchor tag `<a>` wraps the image server control and allows the image to be included as part of the link.</span></span> <span data-ttu-id="5193b-185">`href`属性定位点标记指定的根目录"`~/`"作为链接位置的网站。</span><span class="sxs-lookup"><span data-stu-id="5193b-185">The `href` attribute for the anchor tag specifies the root "`~/`" of the Web site as the link location.</span></span> <span data-ttu-id="5193b-186">默认情况下， *Default.aspx*页将显示当用户导航到 Web 站点的根目录。</span><span class="sxs-lookup"><span data-stu-id="5193b-186">By default, the *Default.aspx* page is displayed when the user navigates to the root of the Web site.</span></span> <span data-ttu-id="5193b-187">**映像**`<asp:Image>`服务器控件包括添加属性，如`BorderStyle`，，呈现为 HTML 浏览器中显示时。</span><span class="sxs-lookup"><span data-stu-id="5193b-187">The **Image** `<asp:Image>` server control includes addition properties, such as `BorderStyle`, that render as HTML when displayed in a browser.</span></span>

### <a name="master-pages"></a><span data-ttu-id="5193b-188">母版页</span><span class="sxs-lookup"><span data-stu-id="5193b-188">Master Pages</span></span>

<span data-ttu-id="5193b-189">母版页为具有扩展.master 的 ASP.NET 文件 (例如， *Site.Master*) 有一个可以包含静态文本、 HTML 元素和服务器控件的预定义布局。</span><span class="sxs-lookup"><span data-stu-id="5193b-189">A master page is an ASP.NET file with the extension .master (for example, *Site.Master*) with a predefined layout that can include static text, HTML elements, and server controls.</span></span> <span data-ttu-id="5193b-190">母版页由特殊`@Master`替换的指令`@Page`适用于普通的指令 *.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="5193b-190">The master page is identified by a special `@Master` directive that replaces the `@Page` directive that is used for ordinary *.aspx* pages.</span></span>

<span data-ttu-id="5193b-191">除了`@Master`指令，主控页还包含的所有页，顶层的 HTML 元素例如`html`， `head`，和`form`。</span><span class="sxs-lookup"><span data-stu-id="5193b-191">In addition to the `@Master` directive, the master page also contains all of the top-level HTML elements for a page, such as `html`, `head`, and `form`.</span></span> <span data-ttu-id="5193b-192">例如，在前面添加主页面上的情况下，你使用 HTML`table`对于布局，`img`公司徽标、 静态文本和服务器控件以处理你的站点的公共成员身份的元素。</span><span class="sxs-lookup"><span data-stu-id="5193b-192">For example, on the master page you added above, you use an HTML `table` for the layout, an `img` element for the company logo, static text, and server controls to handle common membership for your site.</span></span> <span data-ttu-id="5193b-193">作为你母版页的一部分，可以使用任何 HTML 和 ASP.NET 的任何元素。</span><span class="sxs-lookup"><span data-stu-id="5193b-193">You can use any HTML and any ASP.NET elements as part of your master page.</span></span>

<span data-ttu-id="5193b-194">除了静态文本和控件，将出现在所有页上，该主页面还包括一个或多个**ContentPlaceHolder**控件。</span><span class="sxs-lookup"><span data-stu-id="5193b-194">In addition to static text and controls that will appear on all pages, the master page also includes one or more **ContentPlaceHolder** controls.</span></span> <span data-ttu-id="5193b-195">这些占位符控件定义的区域会显示可替换的内容。</span><span class="sxs-lookup"><span data-stu-id="5193b-195">These placeholder controls define regions where replaceable content will appear.</span></span> <span data-ttu-id="5193b-196">反过来，可替换的内容定义在内容页中，如*Default.aspx*，使用**内容**服务器控件。</span><span class="sxs-lookup"><span data-stu-id="5193b-196">In turn, the replaceable content is defined in content pages, such as *Default.aspx*, using the **Content** server control.</span></span>

#### <a name="adding-image-files"></a><span data-ttu-id="5193b-197">添加图像文件</span><span class="sxs-lookup"><span data-stu-id="5193b-197">Adding Image Files</span></span>

<span data-ttu-id="5193b-198">徽标图像引用更高版本，以及所有产品映像，必须添加到 Web 应用程序，以便在浏览器中显示该项目时，可以看到它们。</span><span class="sxs-lookup"><span data-stu-id="5193b-198">The logo image that is referenced above, along with all the product images, must be added to the Web application so that they can be seen when the project is displayed in a browser.</span></span>

#### <a name="download-from-msdn-samples-site"></a><span data-ttu-id="5193b-199">从 MSDN 示例站点下载：</span><span class="sxs-lookup"><span data-stu-id="5193b-199">Download from MSDN Samples site:</span></span>

<span data-ttu-id="5193b-200">[Getting Started with ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="5193b-200">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span>

<span data-ttu-id="5193b-201">下载内容还包括中的资源*WingtipToys 资产*用于创建示例应用程序的文件夹。</span><span class="sxs-lookup"><span data-stu-id="5193b-201">The download includes resources in the *WingtipToys-Assets* folder that are used to create the sample application.</span></span>

1. <span data-ttu-id="5193b-202">如果你尚未这样做，下载压缩的示例文件从 MSDN 示例站点使用上面的链接。</span><span class="sxs-lookup"><span data-stu-id="5193b-202">If you haven't already done so, download the compressed sample files using the above link from the MSDN Samples site.</span></span>
2. <span data-ttu-id="5193b-203">下载完成后，打开.zip 文件并将内容复制到您的计算机上的本地文件夹。</span><span class="sxs-lookup"><span data-stu-id="5193b-203">Once downloaded, open the .zip file and copy the contents to a local folder on your machine.</span></span>
3. <span data-ttu-id="5193b-204">查找和打开*WingtipToys 资产*文件夹。</span><span class="sxs-lookup"><span data-stu-id="5193b-204">Find and open the *WingtipToys-Assets* folder.</span></span>
4. <span data-ttu-id="5193b-205">通过拖放，复制*目录*从您的本地文件夹中的 Web 应用程序项目的根文件夹**解决方案资源管理器**的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5193b-205">By dragging and dropping, copy the *Catalog* folder from your local folder to the root of the Web application project in the **Solution Explorer** of Visual Studio.</span></span> 

    ![UI 和导航-复制文件](ui_and_navigation/_static/image1.png)
5. <span data-ttu-id="5193b-207">接下来，创建一个名为的新文件夹*映像*通过右键单击**WingtipToys**项目中**解决方案资源管理器**并选择**添加** - &gt; **新文件夹**。</span><span class="sxs-lookup"><span data-stu-id="5193b-207">Next, create a new folder named *Images* by right-clicking the **WingtipToys** project in **Solution Explorer** and selecting **Add** -&gt; **New Folder**.</span></span>
6. <span data-ttu-id="5193b-208">复制*logo.jpg*文件从*WingtipToys 资产*文件夹中的**文件资源管理器**到*映像*的 Web 应用程序的文件夹项目中**解决方案资源管理器**的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5193b-208">Copy the *logo.jpg* file from the *WingtipToys-Assets* folder in **File Explorer** to the *Images* folder of the Web application project in **Solution Explorer** of Visual Studio.</span></span>
7. <span data-ttu-id="5193b-209">单击**显示所有文件**顶部的选项**解决方案资源管理器**更新的文件的列表，如果你看不到新文件。</span><span class="sxs-lookup"><span data-stu-id="5193b-209">Click the **Show All Files** option at the top of **Solution Explorer** to update the list of files if you don't see the new files.</span></span>  
  
    <span data-ttu-id="5193b-210">**解决方案资源管理器**现在显示更新的项目文件。</span><span class="sxs-lookup"><span data-stu-id="5193b-210">**Solution Explorer** now shows the updated project files.</span></span> 

    ![UI 和导航的解决方案资源管理器](ui_and_navigation/_static/image2.png)

### <a name="adding-pages"></a><span data-ttu-id="5193b-212">添加网页</span><span class="sxs-lookup"><span data-stu-id="5193b-212">Adding Pages</span></span>

<span data-ttu-id="5193b-213">在添加之前导航到 Web 应用程序，你将首先添加你将导航到的两个新页。</span><span class="sxs-lookup"><span data-stu-id="5193b-213">Before adding navigation to the Web application, you'll first add two new pages that you'll navigate to.</span></span> <span data-ttu-id="5193b-214">稍后在本教程系列中，你将在这些新的页面上显示产品和产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="5193b-214">Later in this tutorial series, you'll display products and product details on these new pages.</span></span>

1. <span data-ttu-id="5193b-215">在**解决方案资源管理器**，右键单击**WingtipToys**，单击**添加**，然后单击**新项**。</span><span class="sxs-lookup"><span data-stu-id="5193b-215">In **Solution Explorer**, right-click **WingtipToys**, click **Add**, and then click **New Item**.</span></span>   
 <span data-ttu-id="5193b-216">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="5193b-216">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="5193b-217">选择**Visual C#**  - &gt; **Web**左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="5193b-217">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="5193b-218">然后，选择**包含母版页的 Web 窗体**从中间列表并将其命名*ProductList.aspx*。</span><span class="sxs-lookup"><span data-stu-id="5193b-218">Then, select **Web Form with Master Page** from the middle list and name it *ProductList.aspx*.</span></span> 

    ![UI 和导航的添加新项对话框](ui_and_navigation/_static/image3.png)
3. <span data-ttu-id="5193b-220">选择**Site.Master**要附加到新创建的主控页 *.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="5193b-220">Select **Site.Master** to attach the master page to the newly created *.aspx* page.</span></span> 

    ![UI 和导航-选择母版页](ui_and_navigation/_static/image4.png)
4. <span data-ttu-id="5193b-222">添加名为另一个页面*ProductDetails.aspx*按照相同的步骤。</span><span class="sxs-lookup"><span data-stu-id="5193b-222">Add an additional page named *ProductDetails.aspx* by following these same steps.</span></span>

### <a name="updating-bootstrap"></a><span data-ttu-id="5193b-223">更新 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="5193b-223">Updating Bootstrap</span></span>

<span data-ttu-id="5193b-224">Visual Studio 2013 项目模板使用[Bootstrap](http://getbootstrap.com/)，由 Twitter 的布局和主题框架。</span><span class="sxs-lookup"><span data-stu-id="5193b-224">The Visual Studio 2013 project templates use [Bootstrap](http://getbootstrap.com/), a layout and theming framework created by Twitter.</span></span> <span data-ttu-id="5193b-225">Bootstrap 使用 CSS3 提供响应灵敏的设计，这意味着布局可以动态调整以适应不同的浏览器窗口大小。</span><span class="sxs-lookup"><span data-stu-id="5193b-225">Bootstrap uses CSS3 to provide responsive design, which means layouts can dynamically adapt to different browser window sizes.</span></span> <span data-ttu-id="5193b-226">Bootstrap 的主题功能还可用于轻松地影响应用程序的外观和行为的更改。</span><span class="sxs-lookup"><span data-stu-id="5193b-226">You can also use Bootstrap's theming feature to easily effect a change in the application's look and feel.</span></span> <span data-ttu-id="5193b-227">默认情况下，Visual Studio 2013 中的 ASP.NET Web 应用程序模板包括 Bootstrap 作为 NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="5193b-227">By default, the ASP.NET Web Application template in Visual Studio 2013 includes Bootstrap as a NuGet package.</span></span>

<span data-ttu-id="5193b-228">在本教程中，你将替换的 Bootstrap CSS 文件来更改 Wingtip Toys 应用程序的外观和感觉。</span><span class="sxs-lookup"><span data-stu-id="5193b-228">In this tutorial, you will change look and feel of the Wingtip Toys application by replacing the Bootstrap CSS files.</span></span>

1. <span data-ttu-id="5193b-229">在**解决方案资源管理器**，打开*内容*文件夹。</span><span class="sxs-lookup"><span data-stu-id="5193b-229">In **Solution Explorer**, open the *Content* folder.</span></span>
2. <span data-ttu-id="5193b-230">右键单击*bootstrap.css*文件并将其命名为*bootstrap original.css*。</span><span class="sxs-lookup"><span data-stu-id="5193b-230">Right-click the *bootstrap.css* file and rename it to *bootstrap-original.css*.</span></span>
3. <span data-ttu-id="5193b-231">重命名*bootstrap.min.css*到*bootstrap original.min.css*。</span><span class="sxs-lookup"><span data-stu-id="5193b-231">Rename the *bootstrap.min.css* to *bootstrap-original.min.css*.</span></span>
4. <span data-ttu-id="5193b-232">在**解决方案资源管理器**，右键单击*内容*文件夹，然后选择**在文件资源管理器中打开文件夹**。</span><span class="sxs-lookup"><span data-stu-id="5193b-232">In **Solution Explorer**, right-click the *Content* folder and select **Open Folder in File Explorer**.</span></span>  
   <span data-ttu-id="5193b-233">将显示文件资源管理器。</span><span class="sxs-lookup"><span data-stu-id="5193b-233">The File Explorer will be displayed.</span></span> <span data-ttu-id="5193b-234">会将下载的 bootstrap CSS 文件保存到此位置。</span><span class="sxs-lookup"><span data-stu-id="5193b-234">You will save a downloaded bootstrap CSS files to this location.</span></span>
5. <span data-ttu-id="5193b-235">在浏览器中，转到[ http://Bootswatch.com ](http://bootswatch.com/)。</span><span class="sxs-lookup"><span data-stu-id="5193b-235">In your browser, go to [http://Bootswatch.com](http://bootswatch.com/).</span></span>
6. <span data-ttu-id="5193b-236">滚动浏览器窗口，直到看到 Cerulean 主题。</span><span class="sxs-lookup"><span data-stu-id="5193b-236">Scroll the browser window until you see the Cerulean theme.</span></span> 

    ![UI 和导航-Cerulean 主题](ui_and_navigation/_static/image5.png)
7. <span data-ttu-id="5193b-238">下载同时*bootstrap.css*文件和*bootstrap.min.css*文件为*内容*文件夹。</span><span class="sxs-lookup"><span data-stu-id="5193b-238">Download both the *bootstrap.css* file and the *bootstrap.min.css* file to the *Content* folder.</span></span> <span data-ttu-id="5193b-239">使用中显示的内容文件夹的路径**文件资源管理器**以前打开的窗口。</span><span class="sxs-lookup"><span data-stu-id="5193b-239">Use the path to the content folder that is displayed in the **File Explorer** window that you previously opened.</span></span>
8. <span data-ttu-id="5193b-240">在**Visual Studio**顶部**解决方案资源管理器**，选择**显示所有文件**选项以显示新的文件的内容文件夹中。</span><span class="sxs-lookup"><span data-stu-id="5193b-240">In **Visual Studio** at the top of **Solution Explorer**, select the **Show All Files** option to display the new files in the Content folder.</span></span> 

    ![UI 和导航的解决方案资源管理器](ui_and_navigation/_static/image6.png)

   <span data-ttu-id="5193b-242">你将看到两个新 CSS 文件中的**内容**文件夹中，但请注意，每个文件名旁边的图标灰显。这意味着，该文件尚未尚未添加到项目。</span><span class="sxs-lookup"><span data-stu-id="5193b-242">You will see the two new CSS files in the **Content** folder, but notice that the icon next to each file name is grayed out. This means that the file has not yet been added to the project.</span></span>
9. <span data-ttu-id="5193b-243">右键单击*bootstrap.css*和*bootstrap.min.css*文件，然后选择**包括在项目**。</span><span class="sxs-lookup"><span data-stu-id="5193b-243">Right-click the *bootstrap.css* and the *bootstrap.min.css* files and select **Include In Project**.</span></span>   
   <span data-ttu-id="5193b-244">本教程中稍后运行 Wingtip Toys 应用程序时，将显示新的用户界面。</span><span class="sxs-lookup"><span data-stu-id="5193b-244">When you run the Wingtip Toys application later in this tutorial, the new UI will be displayed.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5193b-245">ASP.NET Web 应用程序模板使用*Bundle.config*在项目存储的 Bootstrap CSS 文件的路径的根目录的文件。</span><span class="sxs-lookup"><span data-stu-id="5193b-245">The ASP.NET Web Application template uses the *Bundle.config* file at the root of the project to store the path of the Bootstrap CSS files.</span></span>


### <a name="modifying-the-default-navigation"></a><span data-ttu-id="5193b-246">修改默认导航</span><span class="sxs-lookup"><span data-stu-id="5193b-246">Modifying the Default Navigation</span></span>

<span data-ttu-id="5193b-247">可通过更改中的无序的导航列表元素修改应用程序中的每一页的默认导航*Site.Master*页。</span><span class="sxs-lookup"><span data-stu-id="5193b-247">The default navigation for every page in the application can be modified by changing the unordered navigation list element that's in the *Site.Master* page.</span></span>

1. <span data-ttu-id="5193b-248">在**解决方案资源管理器**，找到并打开*Site.Master*页。</span><span class="sxs-lookup"><span data-stu-id="5193b-248">In **Solution Explorer**, locate and open the *Site.Master* page.</span></span>
2. <span data-ttu-id="5193b-249">添加以到未经排序的列表如下所示的黄色突出显示的其他导航链接：</span><span class="sxs-lookup"><span data-stu-id="5193b-249">Add the additional navigation link highlighted in yellow to the unordered list shown below:</span></span>   

    [!code-html[Main](ui_and_navigation/samples/sample5.html?highlight=5)]

<span data-ttu-id="5193b-250">正如您可以看到上述 HTML 中，修改每个行项`<li>`包含的定位点标记`<a>`的链接`href`属性。</span><span class="sxs-lookup"><span data-stu-id="5193b-250">As you can see in the above HTML, you modified each line item `<li>` containing an anchor tag `<a>` with a link `href` attribute.</span></span> <span data-ttu-id="5193b-251">每个`href`指向 Web 应用程序中的页。</span><span class="sxs-lookup"><span data-stu-id="5193b-251">Each `href` points to a page in the Web application.</span></span> <span data-ttu-id="5193b-252">在浏览器中，当用户单击这些链接之一 (如**产品**)，它们将导航到中包含的页`href`(如**ProductList.aspx**)。</span><span class="sxs-lookup"><span data-stu-id="5193b-252">In the browser, when a user clicks on one of these links (such as **Products**), they will navigate to the page contained in the `href` (such as **ProductList.aspx**).</span></span> <span data-ttu-id="5193b-253">在本教程末尾，将运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="5193b-253">You will run the application at the end of this tutorial.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5193b-254">波形符 (`~`) 字符用于指定`href`路径匹配位置始于项目的根目录。</span><span class="sxs-lookup"><span data-stu-id="5193b-254">The tilde (`~`) character is used to specify that the `href` path begins at the root of the project.</span></span>


### <a name="adding-a-data-control-to-display-navigation-data"></a><span data-ttu-id="5193b-255">添加一个数据控件来显示导航数据</span><span class="sxs-lookup"><span data-stu-id="5193b-255">Adding a Data Control to Display Navigation Data</span></span>

<span data-ttu-id="5193b-256">接下来，你将添加一个控件来显示所有数据库中的类别。</span><span class="sxs-lookup"><span data-stu-id="5193b-256">Next, you'll add a control to display all of the categories from the database.</span></span> <span data-ttu-id="5193b-257">每个类别将作为一个链接到*ProductList.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="5193b-257">Each category will act as a link to the *ProductList.aspx* page.</span></span> <span data-ttu-id="5193b-258">当用户单击浏览器中的类别链接时，它们将导航到产品页并查看仅与所选类别关联的产品。</span><span class="sxs-lookup"><span data-stu-id="5193b-258">When a user clicks on a category link in the browser, they will navigate to the products page and see only the products associated with the selected category.</span></span>

<span data-ttu-id="5193b-259">你将使用**ListView**控件来显示数据库中包含的所有类别。</span><span class="sxs-lookup"><span data-stu-id="5193b-259">You'll use a **ListView** control to display all the categories contained in the database.</span></span> <span data-ttu-id="5193b-260">若要添加**ListView**到母版页的控件：</span><span class="sxs-lookup"><span data-stu-id="5193b-260">To add a **ListView** control to the master page:</span></span>

1. <span data-ttu-id="5193b-261">在*Site.Master*页上，添加以下突出显示`<div>`元素**后**`<div>`元素，其中包含`id="TitleContent"`你先前添加：</span><span class="sxs-lookup"><span data-stu-id="5193b-261">In the *Site.Master* page, add the following highlighted `<div>` element **after** the `<div>` element containing the `id="TitleContent"` that you added earlier:</span></span>  

    [!code-aspx[Main](ui_and_navigation/samples/sample6.aspx?highlight=7-21)]

<span data-ttu-id="5193b-262">此代码将显示从数据库的所有类别。</span><span class="sxs-lookup"><span data-stu-id="5193b-262">This code will display all the categories from the database.</span></span> <span data-ttu-id="5193b-263">**ListView**控件将每个类别名称显示为链接文本，并包括指向的*ProductList.aspx*包含查询字符串值包含页面`ID`的类别。</span><span class="sxs-lookup"><span data-stu-id="5193b-263">The **ListView** control displays each category name as link text and includes a link to the *ProductList.aspx* page with a query-string value containing the `ID` of the category.</span></span> <span data-ttu-id="5193b-264">通过设置`ItemType`中的属性**ListView**控制，数据绑定表达式`Item`内可用时`ItemTemplate`节点和控件将成为强类型。</span><span class="sxs-lookup"><span data-stu-id="5193b-264">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available within the `ItemTemplate` node and the control becomes strongly typed.</span></span> <span data-ttu-id="5193b-265">你可以选择的详细信息`Item`对象使用 IntelliSense，例如，指定`CategoryName`。</span><span class="sxs-lookup"><span data-stu-id="5193b-265">You can select details of the `Item` object using IntelliSense, such as specifying the `CategoryName`.</span></span> <span data-ttu-id="5193b-266">此代码包含在容器内`<%#: %>`标记数据绑定表达式。</span><span class="sxs-lookup"><span data-stu-id="5193b-266">This code is contained inside the container `<%#: %>` that marks a data-binding expression.</span></span> <span data-ttu-id="5193b-267">通过将 （:） 添加到末尾`<%#`前缀，数据绑定表达式的结果经过 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="5193b-267">By adding the (:) to the end of the `<%#` prefix, the result of the data-binding expression is HTML-encoded.</span></span> <span data-ttu-id="5193b-268">如果结果为 HTML 编码，你的应用程序更好地抵御跨站点脚本注入 (XSS) 和 HTML 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="5193b-268">When the result is HTML-encoded, your application is better protected against cross-site script injection (XSS) and HTML injection attacks.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5193b-269">**Tip**</span><span class="sxs-lookup"><span data-stu-id="5193b-269">**Tip**</span></span>
> 
> <span data-ttu-id="5193b-270">通过键入在开发过程中添加代码，可以将某些对象的有效成员找到因为强类型数据控件显示可用的成员，基于智能感知。</span><span class="sxs-lookup"><span data-stu-id="5193b-270">When you add code by typing during development, you can be certain that a valid member of an object is found because strongly typed data controls show the available members based on IntelliSense.</span></span> <span data-ttu-id="5193b-271">键入代码，例如属性、 方法和对象时，IntelliSense 将提供相应上下文的代码选择。</span><span class="sxs-lookup"><span data-stu-id="5193b-271">IntelliSense offers context-appropriate code choices as you type code, such as properties, methods, and objects.</span></span>


<span data-ttu-id="5193b-272">在下一步，你将实现`GetCategories`方法来检索数据。</span><span class="sxs-lookup"><span data-stu-id="5193b-272">In the next step, you will implement the `GetCategories` method to retrieve data.</span></span>

### <a name="linking-the-data-control-to-the-database"></a><span data-ttu-id="5193b-273">将数据控件链接到数据库</span><span class="sxs-lookup"><span data-stu-id="5193b-273">Linking the Data Control to the Database</span></span>

<span data-ttu-id="5193b-274">数据控件中显示数据之前，你需要将数据控件链接到数据库。</span><span class="sxs-lookup"><span data-stu-id="5193b-274">Before you can display data in the data control, you need to link the data control to the database.</span></span> <span data-ttu-id="5193b-275">若要使该链接，你可以修改代码隐藏的*Site.Master.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="5193b-275">To make the link, you can modify the code behind of the *Site.Master.cs* file.</span></span>

1. <span data-ttu-id="5193b-276">在**解决方案资源管理器**，右键单击*Site.Master*页，然后单击**查看代码**。</span><span class="sxs-lookup"><span data-stu-id="5193b-276">In **Solution Explorer**, right-click the *Site.Master* page and then click **View Code**.</span></span> <span data-ttu-id="5193b-277">*Site.Master.cs*在编辑器中打开文件。</span><span class="sxs-lookup"><span data-stu-id="5193b-277">The *Site.Master.cs* file is opened in the editor.</span></span>
2. <span data-ttu-id="5193b-278">附近的开头*Site.Master.cs*文件中，添加两个其他命名空间，以便所有包含的命名空间显示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5193b-278">Near the beginning of the *Site.Master.cs* file, add two additional namespaces so that all the included namespaces appear as follows:</span></span>  

    [!code-csharp[Main](ui_and_navigation/samples/sample7.cs?highlight=8-9)]
3. <span data-ttu-id="5193b-279">添加突出显示`GetCategories`方法之后`Page_Load`事件处理程序，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5193b-279">Add the highlighted `GetCategories` method after the `Page_Load` event handler as follows:</span></span>  

    [!code-csharp[Main](ui_and_navigation/samples/sample8.cs?highlight=6-11)]

<span data-ttu-id="5193b-280">使用母版页的任何页面加载浏览器中时，将执行上面的代码。</span><span class="sxs-lookup"><span data-stu-id="5193b-280">The above code is executed when any page that uses the master page is loaded in the browser.</span></span> <span data-ttu-id="5193b-281">`ListView`本教程中前面添加的控件 （名为"任一个"） 使用模型绑定来选择数据。</span><span class="sxs-lookup"><span data-stu-id="5193b-281">The `ListView` control (named "categoryList") that you added earlier in this tutorial uses model binding to select data.</span></span> <span data-ttu-id="5193b-282">中的标记`ListView`你设置的控件的控件`SelectMethod`属性`GetCategories`上面所示的方法。</span><span class="sxs-lookup"><span data-stu-id="5193b-282">In the markup of the `ListView` control you set the control's `SelectMethod` property to the `GetCategories` method, shown above.</span></span> <span data-ttu-id="5193b-283">`ListView`控制调用`GetCategories`方法在适当的时间在页生命周期，并自动将绑定返回的数据。</span><span class="sxs-lookup"><span data-stu-id="5193b-283">The `ListView` control calls the `GetCategories` method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="5193b-284">你将了解有关数据绑定在下一教程中的详细信息。</span><span class="sxs-lookup"><span data-stu-id="5193b-284">You will learn more about binding data in the next tutorial.</span></span>

### <a name="running-the-application-and-creating-the-database"></a><span data-ttu-id="5193b-285">运行应用程序和创建数据库</span><span class="sxs-lookup"><span data-stu-id="5193b-285">Running the Application and Creating the Database</span></span>

<span data-ttu-id="5193b-286">本系列教程中前面创建的初始值设定项类 （名为"ProductDatabaseInitializer"） 和指定中的此类*global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="5193b-286">Earlier in this tutorial series you created an initializer class (named "ProductDatabaseInitializer") and specified this class in the *global.asax.cs* file.</span></span> <span data-ttu-id="5193b-287">实体框架应用程序运行的第一个时间，因为时将生成数据库`Application_Start`方法中包含*global.asax.cs*文件将调用初始值设定项类。</span><span class="sxs-lookup"><span data-stu-id="5193b-287">The Entity Framework will generate the database when the application is run the first time because the `Application_Start` method contained in the *global.asax.cs* file will call the initializer class.</span></span> <span data-ttu-id="5193b-288">初始值设定项类将使用的模型类 (`Category`和`Product`) 之前在本系列教程来创建数据库中添加。</span><span class="sxs-lookup"><span data-stu-id="5193b-288">The initializer class will use the model classes (`Category` and `Product`) that you added earlier in this tutorial series to create the database.</span></span>

1. <span data-ttu-id="5193b-289">在**解决方案资源管理器**，右键单击*Default.aspx*页，选择**设为起始页**。</span><span class="sxs-lookup"><span data-stu-id="5193b-289">In **Solution Explorer**, right-click the *Default.aspx* page and select **Set As Start Page**.</span></span>
2. <span data-ttu-id="5193b-290">在 Visual Studio 中按**F5**。</span><span class="sxs-lookup"><span data-stu-id="5193b-290">In Visual Studio press **F5**.</span></span>   
 <span data-ttu-id="5193b-291">需要一些时间来在此首次运行期间设置的所有内容。</span><span class="sxs-lookup"><span data-stu-id="5193b-291">It will take a little time to set everything up during this first run.</span></span>   
    <span data-ttu-id="5193b-292">![UI 和导航-浏览器窗口](ui_and_navigation/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5193b-292">![UI and Navigation - Browser Windows](ui_and_navigation/_static/image7.png)</span></span>  
 <span data-ttu-id="5193b-293">运行应用程序时，将编译应用程序和数据库名为*wingtiptoys.mdf*将在其中创建*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="5193b-293">When you run the application, the application will be compiled and the database named *wingtiptoys.mdf* will be created in the *App\_Data* folder.</span></span> <span data-ttu-id="5193b-294">在浏览器中，你将看到类别导航菜单。</span><span class="sxs-lookup"><span data-stu-id="5193b-294">In the browser, you will see a category navigation menu.</span></span> <span data-ttu-id="5193b-295">此菜单是通过从数据库检索类别生成的。</span><span class="sxs-lookup"><span data-stu-id="5193b-295">This menu was generated by retrieving the categories from the database.</span></span> <span data-ttu-id="5193b-296">在下一步的教程中，你将实现导航。</span><span class="sxs-lookup"><span data-stu-id="5193b-296">In the next tutorial, you will implement the navigation.</span></span>
3. <span data-ttu-id="5193b-297">关闭浏览器来停止正在运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5193b-297">Close the browser to stop the running application.</span></span>

### <a name="reviewing-the-database"></a><span data-ttu-id="5193b-298">查看数据库</span><span class="sxs-lookup"><span data-stu-id="5193b-298">Reviewing the Database</span></span>

<span data-ttu-id="5193b-299">打开*Web.config*文件并查看连接字符串部分。</span><span class="sxs-lookup"><span data-stu-id="5193b-299">Open the *Web.config* file and look at the connection string section.</span></span> <span data-ttu-id="5193b-300">你可以看到，`AttachDbFilename`连接字符串中的值指向`DataDirectory`为 Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="5193b-300">You can see that the `AttachDbFilename` value in the connection string points to the `DataDirectory` for the Web application project.</span></span> <span data-ttu-id="5193b-301">值`|DataDirectory|`是保留的值，表示*应用\_数据*项目中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="5193b-301">The value `|DataDirectory|` is a reserved value that represents the *App\_Data* folder in the project.</span></span> <span data-ttu-id="5193b-302">此文件夹是已从实体类创建的数据库所在的位置。</span><span class="sxs-lookup"><span data-stu-id="5193b-302">This folder is where the database that was created from your entity classes is located.</span></span>

[!code-xml[Main](ui_and_navigation/samples/sample9.xml)]

> [!NOTE] 
> 
> <span data-ttu-id="5193b-303">如果*应用\_数据*文件夹是不可见，或如果文件夹为空，则选择**刷新**图标，然后**显示所有文件**顶部图标**解决方案资源管理器**窗口。</span><span class="sxs-lookup"><span data-stu-id="5193b-303">If the *App\_Data* folder is not visible or if the folder is empty, select the **Refresh** icon and then the **Show All Files** icon at the top of the **Solution Explorer** window.</span></span> <span data-ttu-id="5193b-304">展开的宽度**解决方案资源管理器**windows 可能需要显示所有可用的图标。</span><span class="sxs-lookup"><span data-stu-id="5193b-304">Expanding the width of the **Solution Explorer** windows may be required to show all available icons.</span></span>


<span data-ttu-id="5193b-305">现在你可以检查中包含的数据*wingtiptoys.mdf*数据库文件使用**服务器资源管理器**窗口。</span><span class="sxs-lookup"><span data-stu-id="5193b-305">Now you can inspect the data contained in the *wingtiptoys.mdf* database file by using the **Server Explorer** window.</span></span>

1. <span data-ttu-id="5193b-306">展开*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="5193b-306">Expand the *App\_Data* folder.</span></span> <span data-ttu-id="5193b-307">如果*应用\_数据*文件夹是不可见，请参阅上面的说明。</span><span class="sxs-lookup"><span data-stu-id="5193b-307">If the *App\_Data* folder is not visible, see the note above.</span></span>
2. <span data-ttu-id="5193b-308">如果*wingtiptoys.mdf*数据库文件不可见，选择**刷新**图标，然后**显示所有文件**顶部的图标**解决方案资源管理器**窗口。</span><span class="sxs-lookup"><span data-stu-id="5193b-308">If the *wingtiptoys.mdf* database file is not visible, select the **Refresh** icon and then the **Show All Files** icon at the top of the **Solution Explorer** window.</span></span>
3. <span data-ttu-id="5193b-309">右键单击*wingtiptoys.mdf*数据库文件并选择**打开**。</span><span class="sxs-lookup"><span data-stu-id="5193b-309">Right-click the *wingtiptoys.mdf* database file and select **Open**.</span></span>  
    <span data-ttu-id="5193b-310">**服务器资源管理器**显示。</span><span class="sxs-lookup"><span data-stu-id="5193b-310">**Server Explorer** is displayed.</span></span> 

    ![UI 和导航-服务器资源管理器](ui_and_navigation/_static/image8.png)
4. <span data-ttu-id="5193b-312">展开*表*文件夹。</span><span class="sxs-lookup"><span data-stu-id="5193b-312">Expand the *Tables* folder.</span></span>
5. <span data-ttu-id="5193b-313">右键单击**产品**表，然后选择**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="5193b-313">Right-click the **Products**table and select **Show Table Data**.</span></span>  
 <span data-ttu-id="5193b-314">**产品**显示表。</span><span class="sxs-lookup"><span data-stu-id="5193b-314">The **Products** table is displayed.</span></span> 

    ![UI 和导航的产品表](ui_and_navigation/_static/image9.png)
6. <span data-ttu-id="5193b-316">此视图允许你查看和修改中的数据**产品**手动表。</span><span class="sxs-lookup"><span data-stu-id="5193b-316">This view lets you see and modify the data in the **Products** table by hand.</span></span>
7. <span data-ttu-id="5193b-317">关闭**产品**表窗口。</span><span class="sxs-lookup"><span data-stu-id="5193b-317">Close the **Products** table window.</span></span>
8. <span data-ttu-id="5193b-318">在**服务器资源管理器**，右键单击**产品**再次表，然后选择**打开表定义**。</span><span class="sxs-lookup"><span data-stu-id="5193b-318">In the **Server Explorer**, right-click the **Products** table again and select **Open Table Definition**.</span></span>  
 <span data-ttu-id="5193b-319">数据设计为**产品**显示表。</span><span class="sxs-lookup"><span data-stu-id="5193b-319">The data design for the **Products** table is displayed.</span></span> 

    ![UI 和导航-产品设计](ui_and_navigation/_static/image10.png)
9. <span data-ttu-id="5193b-321">在**T-SQL**选项卡上，你将看到用于创建表的 SQL DDL 语句。</span><span class="sxs-lookup"><span data-stu-id="5193b-321">In the **T-SQL** tab you will see the SQL DDL statement that was used to create the table.</span></span> <span data-ttu-id="5193b-322">你还可以使用中的用户界面**设计**选项卡以修改架构。</span><span class="sxs-lookup"><span data-stu-id="5193b-322">You can also use the UI in the **Design** tab to modify the schema.</span></span>
10. <span data-ttu-id="5193b-323">在**服务器资源管理器**，右键单击**WingtipToys**数据库并选择**关闭连接**。</span><span class="sxs-lookup"><span data-stu-id="5193b-323">In the **Server Explorer**, right-click **WingtipToys** database and select **Close Connection**.</span></span>   
 <span data-ttu-id="5193b-324">通过从 Visual Studio 将数据库分离，将能够更高版本在本教程系列中修改数据库架构。</span><span class="sxs-lookup"><span data-stu-id="5193b-324">By detaching the database from Visual Studio, the database schema will be able to be modified later in this tutorial series.</span></span>
11. <span data-ttu-id="5193b-325">返回到**解决方案资源管理器**通过选择**解决方案资源管理器**选项卡底部的**服务器资源管理器**窗口。</span><span class="sxs-lookup"><span data-stu-id="5193b-325">Return to **Solution Explorer**by selecting the **Solution Explorer** tab at the bottom of the **Server Explorer** window.</span></span>

## <a name="summary"></a><span data-ttu-id="5193b-326">总结</span><span class="sxs-lookup"><span data-stu-id="5193b-326">Summary</span></span>

<span data-ttu-id="5193b-327">在本教程中的序列已添加一些基本 UI、 图形、 页和导航。</span><span class="sxs-lookup"><span data-stu-id="5193b-327">In this tutorial of the series you have added some basic UI, graphics, pages, and navigation.</span></span> <span data-ttu-id="5193b-328">此外，你已运行的 Web 应用程序，从你在前面的教程中添加的数据类创建数据库。</span><span class="sxs-lookup"><span data-stu-id="5193b-328">Additionally, you ran the Web application, which created the database from the data classes that you added in the previous tutorial.</span></span> <span data-ttu-id="5193b-329">你还查看的内容*产品*通过直接查看数据库的数据库的表。</span><span class="sxs-lookup"><span data-stu-id="5193b-329">You also viewed the contents of the *Products* table of the database by viewing the database directly.</span></span> <span data-ttu-id="5193b-330">在下一步的教程中，将显示数据项和从数据库的详细信息。</span><span class="sxs-lookup"><span data-stu-id="5193b-330">In the next tutorial, you'll display data items and details from the database.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5193b-331">其他资源</span><span class="sxs-lookup"><span data-stu-id="5193b-331">Additional Resources</span></span>

<span data-ttu-id="5193b-332">[ASP.NET 网页编程简介](https://msdn.microsoft.com/library/ms178125.aspx) </span><span class="sxs-lookup"><span data-stu-id="5193b-332">[Introduction to Programming ASP.NET Web Pages](https://msdn.microsoft.com/library/ms178125.aspx) </span></span>  
<span data-ttu-id="5193b-333">[ASP.NET Web 服务器控件概述](https://msdn.microsoft.com/library/zsyt68f1.aspx) </span><span class="sxs-lookup"><span data-stu-id="5193b-333">[ASP.NET Web Server Controls Overview](https://msdn.microsoft.com/library/zsyt68f1.aspx) </span></span>  
[<span data-ttu-id="5193b-334">CSS 教程</span><span class="sxs-lookup"><span data-stu-id="5193b-334">CSS Tutorial</span></span>](http://www.w3schools.com/css/default.asp)

> [!div class="step-by-step"]
> <span data-ttu-id="5193b-335">[上一页](create_the_data_access_layer.md)
> [下一页](display_data_items_and_details.md)</span><span class="sxs-lookup"><span data-stu-id="5193b-335">[Previous](create_the_data_access_layer.md)
[Next](display_data_items_and_details.md)</span></span>
