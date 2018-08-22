---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: 了解项目文件 |Microsoft Docs
author: jrjlee
description: Microsoft Build Engine (MSBuild) 项目文件位于生成和部署过程的核心。 本主题开头为 MSBuild 的概念性概述...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: 114dd21002ef41627f3a101c0197a85fd5208887
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824424"
---
<a name="understanding-the-project-file"></a><span data-ttu-id="426b1-104">了解项目文件</span><span class="sxs-lookup"><span data-stu-id="426b1-104">Understanding the Project File</span></span>
====================
<span data-ttu-id="426b1-105">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="426b1-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="426b1-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="426b1-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="426b1-107">Microsoft Build Engine (MSBuild) 项目文件位于生成和部署过程的核心。</span><span class="sxs-lookup"><span data-stu-id="426b1-107">Microsoft Build Engine (MSBuild) project files lie at the heart of the build and deployment process.</span></span> <span data-ttu-id="426b1-108">本主题开头的 MSBuild 和项目文件的概念性概述。</span><span class="sxs-lookup"><span data-stu-id="426b1-108">This topic starts with a conceptual overview of MSBuild and the project file.</span></span> <span data-ttu-id="426b1-109">它描述当您使用的项目文件，其效果通过举例说明如何使用项目文件来部署实际的应用程序时将遇到的关键组件。</span><span class="sxs-lookup"><span data-stu-id="426b1-109">It describes the key components you'll come across when you work with project files, and it works through an example of how you can use project files to deploy real-world applications.</span></span>
> 
> <span data-ttu-id="426b1-110">你将学习：</span><span class="sxs-lookup"><span data-stu-id="426b1-110">What you'll learn:</span></span>
> 
> - <span data-ttu-id="426b1-111">MSBuild 如何使用 MSBuild 项目文件来生成项目。</span><span class="sxs-lookup"><span data-stu-id="426b1-111">How MSBuild uses MSBuild project files to build projects.</span></span>
> - <span data-ttu-id="426b1-112">如何 MSBuild 集成与部署技术，如 Internet 信息服务 (IIS) Web 部署工具 （Web 部署）。</span><span class="sxs-lookup"><span data-stu-id="426b1-112">How MSBuild integrates with deployment technologies, like the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span>
> - <span data-ttu-id="426b1-113">如何了解项目文件的关键组件。</span><span class="sxs-lookup"><span data-stu-id="426b1-113">How to understand the key components of a project file.</span></span>
> - <span data-ttu-id="426b1-114">如何使用项目文件生成和部署复杂的应用程序。</span><span class="sxs-lookup"><span data-stu-id="426b1-114">How you can use project files to build and deploy complex applications.</span></span>


## <a name="msbuild-and-the-project-file"></a><span data-ttu-id="426b1-115">MSBuild 和项目文件</span><span class="sxs-lookup"><span data-stu-id="426b1-115">MSBuild and the Project File</span></span>

<span data-ttu-id="426b1-116">当你创建并在 Visual Studio 中生成解决方案时，Visual Studio 使用 MSBuild 生成解决方案中的每个项目。</span><span class="sxs-lookup"><span data-stu-id="426b1-116">When you create and build solutions in Visual Studio, Visual Studio uses MSBuild to build each project in your solution.</span></span> <span data-ttu-id="426b1-117">每个 Visual Studio 项目包含一个 MSBuild 项目文件，反映项目的类型的文件扩展名与&#x2014;例如，C# 项目 (.csproj)、 Visual Basic.NET 项目 (.vbproj) 或数据库项目 (.dbproj)。</span><span class="sxs-lookup"><span data-stu-id="426b1-117">Every Visual Studio project includes an MSBuild project file, with a file extension that reflects the type of project&#x2014;for example, a C# project (.csproj), a Visual Basic.NET project (.vbproj), or a database project (.dbproj).</span></span> <span data-ttu-id="426b1-118">若要生成项目时，MSBuild 必须处理与项目关联的项目文件。</span><span class="sxs-lookup"><span data-stu-id="426b1-118">In order to build a project, MSBuild must process the project file associated with the project.</span></span> <span data-ttu-id="426b1-119">项目文件是包含所有信息和说明 MSBuild 需生成项目，如要包括平台要求、 版本控制信息、 web 服务器或数据库服务器设置的内容的 XML 文档和必须执行的任务。</span><span class="sxs-lookup"><span data-stu-id="426b1-119">The project file is an XML document that contains all the information and instructions that MSBuild needs in order to build your project, like the content to include, the platform requirements, versioning information, web server or database server settings, and the tasks that must be performed.</span></span>

<span data-ttu-id="426b1-120">MSBuild 项目文件基于[MSBuild XML 架构](https://msdn.microsoft.com/library/5dy88c2e.aspx)，因此生成过程是完全开放和透明。</span><span class="sxs-lookup"><span data-stu-id="426b1-120">MSBuild project files are based on the [MSBuild XML schema](https://msdn.microsoft.com/library/5dy88c2e.aspx), and as a result the build process is entirely open and transparent.</span></span> <span data-ttu-id="426b1-121">此外，您不需要安装 Visual Studio 才能使用 MSBuild 引擎&#x2014;MSBuild.exe 可执行文件是.NET Framework 的一部分，可以从命令提示符下运行。</span><span class="sxs-lookup"><span data-stu-id="426b1-121">In addition, you don't need to install Visual Studio in order to use the MSBuild engine&#x2014;the MSBuild.exe executable is part of the .NET Framework, and you can run it from a command prompt.</span></span> <span data-ttu-id="426b1-122">作为开发人员，您可以编写您自己的 MSBuild 项目文件，使用 MSBuild XML 架构，来实施复杂的细化控制如何生成和部署你的项目。</span><span class="sxs-lookup"><span data-stu-id="426b1-122">As a developer, you can craft your own MSBuild project files, using the MSBuild XML schema, to impose sophisticated and fine-grained control over how your projects are built and deployed.</span></span> <span data-ttu-id="426b1-123">这些自定义项目文件的工作方式与 Visual Studio 会自动生成的项目文件完全相同。</span><span class="sxs-lookup"><span data-stu-id="426b1-123">These custom project files work in exactly the same way as the project files that Visual Studio generates automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="426b1-124">此外可以与 Team Build 服务 Team Foundation Server (TFS) 中使用 MSBuild 项目文件。</span><span class="sxs-lookup"><span data-stu-id="426b1-124">You can also use MSBuild project files with the Team Build service in Team Foundation Server (TFS).</span></span> <span data-ttu-id="426b1-125">例如，在持续集成 (CI) 方案中的项目文件可用于自动部署到测试环境时签入新代码。</span><span class="sxs-lookup"><span data-stu-id="426b1-125">For example, you can use project files in continuous integration (CI) scenarios to automate deployment to a test environment when new code is checked in.</span></span> <span data-ttu-id="426b1-126">有关详细信息，请参阅[用于自动执行 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="426b1-126">For more information, see [Configuring Team Foundation Server for Automated Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span>


### <a name="project-file-naming-conventions"></a><span data-ttu-id="426b1-127">项目文件命名约定</span><span class="sxs-lookup"><span data-stu-id="426b1-127">Project File Naming Conventions</span></span>

<span data-ttu-id="426b1-128">在创建您自己的项目文件时，可以使用任何您喜欢的文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="426b1-128">When you create your own project files, you can use any file extension you like.</span></span> <span data-ttu-id="426b1-129">但是，若要使他人可以轻松地了解你的解决方案，应使用这些常见约定：</span><span class="sxs-lookup"><span data-stu-id="426b1-129">However, to make your solutions easier for others to understand, you should use these common conventions:</span></span>

- <span data-ttu-id="426b1-130">创建生成的项目的项目文件时，请使用.proj 扩展。</span><span class="sxs-lookup"><span data-stu-id="426b1-130">Use the .proj extension when you create a project file that builds projects.</span></span>
- <span data-ttu-id="426b1-131">在创建要导入到其他项目文件的可重用的项目文件时，请使用.targets 扩展名。</span><span class="sxs-lookup"><span data-stu-id="426b1-131">Use the .targets extension when you create a reusable project file to import into other project files.</span></span> <span data-ttu-id="426b1-132">文件扩展名为.targets 通常不生成任何内容本身，而是只需包含可以导入到.proj 文件的说明。</span><span class="sxs-lookup"><span data-stu-id="426b1-132">Files with a .targets extension typically don't build anything themselves, they simply contain instructions that you can import into your .proj files.</span></span>

### <a name="integration-with-deployment-technologies"></a><span data-ttu-id="426b1-133">与部署技术的集成</span><span class="sxs-lookup"><span data-stu-id="426b1-133">Integration with Deployment Technologies</span></span>

<span data-ttu-id="426b1-134">如果您使用过 ASP.NET web 应用程序和 ASP.NET MVC web 应用程序，如 web 应用程序项目在 Visual Studio 2010 中，您就知道这些项目包括用于打包和部署到目标环境的 web 应用程序的内置支持。</span><span class="sxs-lookup"><span data-stu-id="426b1-134">If you've worked with web application projects in Visual Studio 2010, like ASP.NET web applications and ASP.NET MVC web applications, you'll know that these projects include built-in support for packaging and deploying the web application to a target environment.</span></span> <span data-ttu-id="426b1-135">**属性**页这些项目包括**打包/发布 Web**并**打包/发布 SQL**可用于配置的选项卡如何的组件在打包和部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="426b1-135">The **Properties** pages for these projects include **Package/Publish Web** and **Package/Publish SQL** tabs that you can use to configure how the components of your application are packaged and deployed.</span></span> <span data-ttu-id="426b1-136">下面的示例演示**打包/发布 Web**选项卡：</span><span class="sxs-lookup"><span data-stu-id="426b1-136">This shows the **Package/Publish Web** tab:</span></span>

![](understanding-the-project-file/_static/image1.png)

<span data-ttu-id="426b1-137">这些功能背后的基础技术称为 Web 发布管道 (WPP) 作为。</span><span class="sxs-lookup"><span data-stu-id="426b1-137">The underlying technology behind these capabilities is known as the Web Publishing Pipeline (WPP).</span></span> <span data-ttu-id="426b1-138">WPP 实质上是将 MSBuild 和[Web 部署](https://go.microsoft.com/?linkid=9805122)一起，以 web 应用程序提供完整的生成、 包和部署过程。</span><span class="sxs-lookup"><span data-stu-id="426b1-138">The WPP essentially brings MSBuild and [Web Deploy](https://go.microsoft.com/?linkid=9805122) together to provide a complete build, package, and deployment process for your web applications.</span></span>

<span data-ttu-id="426b1-139">好消息是您可以充分利用 WPP 提供创建 web 项目的自定义项目文件时的集成点。</span><span class="sxs-lookup"><span data-stu-id="426b1-139">The good news is that you can take advantage of the integration points that the WPP provides when you create custom project files for web projects.</span></span> <span data-ttu-id="426b1-140">可以在项目文件中，可用于生成项目、 创建 web 部署包，并通过单个项目文件和 MSBuild 的单个调用远程服务器上安装这些包包含部署说明。</span><span class="sxs-lookup"><span data-stu-id="426b1-140">You can include deployment instructions in your project file, which allows you to build your projects, create web deployment packages, and install these packages on remote servers through a single project file and a single call to MSBuild.</span></span> <span data-ttu-id="426b1-141">作为生成过程的一部分，你还可以调用任何其他可执行文件。</span><span class="sxs-lookup"><span data-stu-id="426b1-141">You can also call any other executables as part of your build process.</span></span> <span data-ttu-id="426b1-142">例如，可以运行 VSDBCMD.exe 命令行工具来部署数据库架构文件。</span><span class="sxs-lookup"><span data-stu-id="426b1-142">For example, you can run the VSDBCMD.exe command-line tool to deploy a database from a schema file.</span></span> <span data-ttu-id="426b1-143">本主题的过程中，你将看到如何，您可以充分利用这些功能，以满足您的企业部署方案的要求。</span><span class="sxs-lookup"><span data-stu-id="426b1-143">Over the course of this topic, you'll see how you can take advantage of these capabilities to meet the requirements of your enterprise deployment scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="426b1-144">Web 应用程序部署过程的工作原理的详细信息，请参阅[ASP.NET Web 应用程序项目部署概述](https://msdn.microsoft.com/library/dd394698.aspx)。</span><span class="sxs-lookup"><span data-stu-id="426b1-144">For more information on how the web application deployment process works, see [ASP.NET Web Application Project Deployment Overview](https://msdn.microsoft.com/library/dd394698.aspx).</span></span>


## <a name="the-anatomy-of-a-project-file"></a><span data-ttu-id="426b1-145">项目文件的剖析</span><span class="sxs-lookup"><span data-stu-id="426b1-145">The Anatomy of a Project File</span></span>

<span data-ttu-id="426b1-146">查看更多详细信息中的生成过程之前，它是值得花一些时间来熟悉 MSBuild 项目文件的基本结构。</span><span class="sxs-lookup"><span data-stu-id="426b1-146">Before you look at the build process in more detail, it's worth taking a few moments to familiarize yourself with the basic structure of an MSBuild project file.</span></span> <span data-ttu-id="426b1-147">本部分提供查看、 编辑或创建项目文件时，将会遇到的常见元素的概述。</span><span class="sxs-lookup"><span data-stu-id="426b1-147">This section provides an overview of the more common elements that you'll encounter when you review, edit, or create a project file.</span></span> <span data-ttu-id="426b1-148">具体而言，你将学习：</span><span class="sxs-lookup"><span data-stu-id="426b1-148">In particular, you'll learn:</span></span>

- <span data-ttu-id="426b1-149">如何使用*属性*管理生成过程的变量。</span><span class="sxs-lookup"><span data-stu-id="426b1-149">How to use *properties* to manage variables for the build process.</span></span>
- <span data-ttu-id="426b1-150">如何使用*项*来确定生成过程的输入，这类似于代码文件。</span><span class="sxs-lookup"><span data-stu-id="426b1-150">How to use *items* to identify the inputs to the build process, like code files.</span></span>
- <span data-ttu-id="426b1-151">如何使用*目标*并*任务*以便执行指令到 MSBuild，使用*属性*并*项*中其他位置定义项目文件中。</span><span class="sxs-lookup"><span data-stu-id="426b1-151">How to use *targets* and *tasks* to provide execution instructions to MSBuild, using *properties* and *items* defined elsewhere in the project file.</span></span>

<span data-ttu-id="426b1-152">这显示了一个 MSBuild 项目文件中的主要元素之间的关系：</span><span class="sxs-lookup"><span data-stu-id="426b1-152">This shows the relationship between the key elements in an MSBuild project file:</span></span>

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a><span data-ttu-id="426b1-153">Project 元素</span><span class="sxs-lookup"><span data-stu-id="426b1-153">The Project Element</span></span>

<span data-ttu-id="426b1-154">[项目](https://msdn.microsoft.com/library/bcxfsh87.aspx)元素是每个项目文件的根元素。</span><span class="sxs-lookup"><span data-stu-id="426b1-154">The [Project](https://msdn.microsoft.com/library/bcxfsh87.aspx) element is the root element of every project file.</span></span> <span data-ttu-id="426b1-155">除了标识项目文件的 XML 架构**项目**元素可以包含特性来指定生成过程的入口点。</span><span class="sxs-lookup"><span data-stu-id="426b1-155">In addition to identifying the XML schema for the project file, the **Project** element can include attributes to specify the entry points for the build process.</span></span> <span data-ttu-id="426b1-156">例如，在[联系人管理器示例解决方案](the-contact-manager-solution.md)，则*Publish.proj*文件指定生成应该通过调用名为目标来启动**FullPublish**。</span><span class="sxs-lookup"><span data-stu-id="426b1-156">For example, in the [Contact Manager sample solution](the-contact-manager-solution.md), the *Publish.proj* file specifies that the build should start by calling the target named **FullPublish**.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]


### <a name="properties-and-conditions"></a><span data-ttu-id="426b1-157">属性和条件</span><span class="sxs-lookup"><span data-stu-id="426b1-157">Properties and Conditions</span></span>

<span data-ttu-id="426b1-158">项目文件通常需要提供了大量的信息，以便成功地生成和部署你的项目的不同部分。</span><span class="sxs-lookup"><span data-stu-id="426b1-158">A project file typically needs to provide lots of different pieces of information in order to successfully build and deploy your projects.</span></span> <span data-ttu-id="426b1-159">这条信息可能包括服务器名称、 连接字符串、 凭据、 生成配置、 源和目标文件路径和想要包括支持自定义的任何其他信息。</span><span class="sxs-lookup"><span data-stu-id="426b1-159">These pieces of information could include server names, connection strings, credentials, build configurations, source and destination file paths, and any other information you want to include to support customization.</span></span> <span data-ttu-id="426b1-160">在项目文件中，属性必须定义内[PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx)元素。</span><span class="sxs-lookup"><span data-stu-id="426b1-160">In a project file, properties must be defined within a [PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx) element.</span></span> <span data-ttu-id="426b1-161">MSBuild 属性包括键-值对。</span><span class="sxs-lookup"><span data-stu-id="426b1-161">MSBuild properties consist of key-value pairs.</span></span> <span data-ttu-id="426b1-162">内**PropertyGroup**元素，元素名称定义的属性键和元素内容定义的属性值。</span><span class="sxs-lookup"><span data-stu-id="426b1-162">Within the **PropertyGroup** element, the element name defines the property key and the content of the element defines the property value.</span></span> <span data-ttu-id="426b1-163">例如，可以定义名为的属性**ServerName**并**ConnectionString**来存储静态服务器名称和连接字符串。</span><span class="sxs-lookup"><span data-stu-id="426b1-163">For example, you could define properties named **ServerName** and **ConnectionString** to store a static server name and connection string.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]


<span data-ttu-id="426b1-164">若要检索的属性值，则使用格式<strong>$(</strong><em>PropertyName</em><strong>)</strong><em>。</em>例如，若要检索的值<strong>ServerName</strong>属性，你需要键入：</span><span class="sxs-lookup"><span data-stu-id="426b1-164">To retrieve a property value, you use the format <strong>$(</strong><em>PropertyName</em><strong>)</strong><em>.</em>For example, to retrieve the value of the <strong>ServerName</strong> property, you would type:</span></span>


[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]


> [!NOTE]
> <span data-ttu-id="426b1-165">你将看到示例说明了如何以及何时使用本主题后面的属性值。</span><span class="sxs-lookup"><span data-stu-id="426b1-165">You'll see examples of how and when to use property values later in this topic.</span></span>


<span data-ttu-id="426b1-166">在项目文件中嵌入的静态属性形式的信息并不总是理想的方法来管理生成过程。</span><span class="sxs-lookup"><span data-stu-id="426b1-166">Embedding information as static properties in a project file is not always the ideal approach to managing the build process.</span></span> <span data-ttu-id="426b1-167">在很多情况下，你将想要从其他源中获取信息或鼓励用户提供命令提示符中的信息。</span><span class="sxs-lookup"><span data-stu-id="426b1-167">In a lot of scenarios, you'll want to obtain the information from other sources or empower the user to provide the information from the command prompt.</span></span> <span data-ttu-id="426b1-168">MSBuild，可作为命令行参数指定任何属性值。</span><span class="sxs-lookup"><span data-stu-id="426b1-168">MSBuild allows you to specify any property value as a command-line parameter.</span></span> <span data-ttu-id="426b1-169">例如，用户可以提供的值**ServerName**时他或她 MSBuild.exe 从命令行运行。</span><span class="sxs-lookup"><span data-stu-id="426b1-169">For example, the user could provide a value for **ServerName** when he or she runs MSBuild.exe from the command line.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]


> [!NOTE]
> <span data-ttu-id="426b1-170">有关参数和可用于 MSBuild.exe 的开关的详细信息，请参阅[MSBuild 命令行参考](https://msdn.microsoft.com/library/ms164311.aspx)。</span><span class="sxs-lookup"><span data-stu-id="426b1-170">For more information on the arguments and switches you can use with MSBuild.exe, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>


<span data-ttu-id="426b1-171">可以使用相同的属性语法以获取环境变量和内置项目属性的值。</span><span class="sxs-lookup"><span data-stu-id="426b1-171">You can use the same property syntax to obtain the values of environment variables and built-in project properties.</span></span> <span data-ttu-id="426b1-172">许多常用的属性的定义，并且它们通过包括相关参数名称使用你的项目文件。</span><span class="sxs-lookup"><span data-stu-id="426b1-172">Lots of commonly used properties are defined for you, and you can use them in your project files by including the relevant parameter name.</span></span> <span data-ttu-id="426b1-173">例如，若要检索的当前项目平台&#x2014;例如 **x86** 或 **AnyCpu**&#x2014;可以包括 **$(Platform)** 中的属性引用你的项目文件。</span><span class="sxs-lookup"><span data-stu-id="426b1-173">For example, to retrieve the current project platform&#x2014;for example, **x86** or **AnyCpu**&#x2014;you can include the **$(Platform)** property reference in your project file.</span></span> <span data-ttu-id="426b1-174">有关详细信息，请参阅[用于生成命令和属性的宏](https://msdn.microsoft.com/library/c02as0cs.aspx)，[常用的 MSBuild 项目属性](https://msdn.microsoft.com/library/bb629394.aspx)，并[保留属性](https://msdn.microsoft.com/library/ms164309.aspx)。</span><span class="sxs-lookup"><span data-stu-id="426b1-174">For more information, see [Macros for Build Commands and Properties](https://msdn.microsoft.com/library/c02as0cs.aspx), [Common MSBuild Project Properties](https://msdn.microsoft.com/library/bb629394.aspx), and [Reserved Properties](https://msdn.microsoft.com/library/ms164309.aspx).</span></span>

<span data-ttu-id="426b1-175">属性通常用于结合*条件*。</span><span class="sxs-lookup"><span data-stu-id="426b1-175">Properties are often used in conjunction with *conditions*.</span></span> <span data-ttu-id="426b1-176">支持大多数 MSBuild 元素**条件**属性，它允许您指定 MSBuild 应在其评估该元素的条件。</span><span class="sxs-lookup"><span data-stu-id="426b1-176">Most MSBuild elements support the **Condition** attribute, which lets you specify the criteria upon which MSBuild should evaluate the element.</span></span> <span data-ttu-id="426b1-177">例如，考虑此属性定义：</span><span class="sxs-lookup"><span data-stu-id="426b1-177">For example, consider this property definition:</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]


<span data-ttu-id="426b1-178">当 MSBuild 处理此属性定义时，它首先会检查以查看是否 **$(OutputRoot)** 属性值为可用。</span><span class="sxs-lookup"><span data-stu-id="426b1-178">When MSBuild processes this property definition, it first checks to see whether an **$(OutputRoot)** property value is available.</span></span> <span data-ttu-id="426b1-179">如果属性值为空&#x2014;换而言之，用户未为此属性提供值&#x2014;条件计算结果为 **true** 和属性值设置为 **...\Publish\Out** 。如果用户已为此属性提供一个值，该条件计算结果为**false**和不使用静态属性值。</span><span class="sxs-lookup"><span data-stu-id="426b1-179">If the property value is blank&#x2014;in other words, the user hasn't provided a value for this property&#x2014;the condition evaluates to **true** and the property value is set to **..\Publish\Out**. If the user has provided a value for this property, the condition evaluates to **false** and the static property value is not used.</span></span>

<span data-ttu-id="426b1-180">可以在其中指定条件的不同方式的详细信息，请参阅[MSBuild 条件](https://msdn.microsoft.com/library/7szfhaft.aspx)。</span><span class="sxs-lookup"><span data-stu-id="426b1-180">For more information on the different ways in which you can specify conditions, see [MSBuild Conditions](https://msdn.microsoft.com/library/7szfhaft.aspx).</span></span>

### <a name="items-and-item-groups"></a><span data-ttu-id="426b1-181">项目和项组</span><span class="sxs-lookup"><span data-stu-id="426b1-181">Items and Item Groups</span></span>

<span data-ttu-id="426b1-182">重要的项目文件的角色之一是定义生成过程的输入。</span><span class="sxs-lookup"><span data-stu-id="426b1-182">One of the important roles of the project file is to define the inputs to the build process.</span></span> <span data-ttu-id="426b1-183">通常情况下，这些输入是文件&#x2014;的代码文件、 配置文件、 命令文件和任何其他需要处理或将作为复制的文件生成过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="426b1-183">Typically, these inputs are files&#x2014;code files, configuration files, command files, and any other files that you need to process or copy as part of the build process.</span></span> <span data-ttu-id="426b1-184">在 MSBuild 项目架构中，由这些输入[项](https://msdn.microsoft.com/library/ms164283.aspx)元素。</span><span class="sxs-lookup"><span data-stu-id="426b1-184">In the MSBuild project schema, these inputs are represented by [Item](https://msdn.microsoft.com/library/ms164283.aspx) elements.</span></span> <span data-ttu-id="426b1-185">在项目文件中，项目必须定义内[ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx)元素。</span><span class="sxs-lookup"><span data-stu-id="426b1-185">In a project file, items must be defined within an [ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx) element.</span></span> <span data-ttu-id="426b1-186">就像**属性**元素，您可以命名**项**元素你的喜好。</span><span class="sxs-lookup"><span data-stu-id="426b1-186">Just like **Property** elements, you can name an **Item** element however you like.</span></span> <span data-ttu-id="426b1-187">但是，必须指定**Include**属性标识的文件或项所表示的通配符。</span><span class="sxs-lookup"><span data-stu-id="426b1-187">However, you must specify an **Include** attribute to identify the file or wildcard that the item represents.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]


<span data-ttu-id="426b1-188">通过指定多个**项**具有相同名称的元素，要有效地创建的资源的命名的列表。</span><span class="sxs-lookup"><span data-stu-id="426b1-188">By specifying multiple **Item** elements with the same name, you're effectively creating a named list of resources.</span></span> <span data-ttu-id="426b1-189">若要了解此操作的好方法是若要查看在 Visual Studio 将创建的项目文件之一。</span><span class="sxs-lookup"><span data-stu-id="426b1-189">A good way to see this in action is to take a look inside one of the project files that Visual Studio creates.</span></span> <span data-ttu-id="426b1-190">例如， *ContactManager.Mvc.csproj*示例解决方案文件中的包括大量的项组，每个都有多个具有相同的名称**项**元素。</span><span class="sxs-lookup"><span data-stu-id="426b1-190">For example, the *ContactManager.Mvc.csproj* file in the sample solution includes a lot of item groups, each with several identically named **Item** elements.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]


<span data-ttu-id="426b1-191">这样一来，在项目文件指示 MSBuild 构造需要相同的方式处理的文件的列表&#x2014;**引用**列表包含必须在位置，以便成功生成程序集**编译**列表包括必须编译的代码文件和**内容**列表提供一些资源，必须复制不变。</span><span class="sxs-lookup"><span data-stu-id="426b1-191">In this way, the project file is instructing MSBuild to construct lists of files that need to be processed in the same way&#x2014;the **Reference** list includes assemblies that must be in place for a successful build, the **Compile** list includes code files that must be compiled, and the **Content** list includes resources that must be copied unaltered.</span></span> <span data-ttu-id="426b1-192">我们将介绍如何生成过程引用和使用本主题后面的这些项。</span><span class="sxs-lookup"><span data-stu-id="426b1-192">We'll look at how the build process references and uses these items later in this topic.</span></span>

<span data-ttu-id="426b1-193">此外可以包含项元素[ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx)子元素。</span><span class="sxs-lookup"><span data-stu-id="426b1-193">Item elements can also include [ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx) child elements.</span></span> <span data-ttu-id="426b1-194">这是用户定义的键 / 值对，实质上是表示特定于该项目的属性。</span><span class="sxs-lookup"><span data-stu-id="426b1-194">These are user-defined key-value pairs and essentially represent properties that are specific to that item.</span></span> <span data-ttu-id="426b1-195">例如，大量**编译**项目文件中的项元素包括**DependentUpon**子元素。</span><span class="sxs-lookup"><span data-stu-id="426b1-195">For example, a lot of the **Compile** item elements in the project file include **DependentUpon** child elements.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]


> [!NOTE]
> <span data-ttu-id="426b1-196">除了用户创建的项元数据，在创建的各种常见元数据分配的所有项。</span><span class="sxs-lookup"><span data-stu-id="426b1-196">In addition to user-created item metadata, all items are assigned various common metadata on creation.</span></span> <span data-ttu-id="426b1-197">有关详细信息，请参阅[常见项元数据](https://msdn.microsoft.com/library/ms164313.aspx)。</span><span class="sxs-lookup"><span data-stu-id="426b1-197">For more information, see [Well-known Item Metadata](https://msdn.microsoft.com/library/ms164313.aspx).</span></span>


<span data-ttu-id="426b1-198">您可以创建**ItemGroup**根级别中的元素**项目**元素或在特定于**目标**元素。</span><span class="sxs-lookup"><span data-stu-id="426b1-198">You can create **ItemGroup** elements within the root-level **Project** element or within specific **Target** elements.</span></span> <span data-ttu-id="426b1-199">**ItemGroup**元素还支持**条件**，你可以定制根据项目配置或平台等条件生成过程的输入的属性。</span><span class="sxs-lookup"><span data-stu-id="426b1-199">**ItemGroup** elements also support **Condition** attributes, which lets you tailor the inputs to the build process according to conditions like the project configuration or platform.</span></span>

### <a name="targets-and-tasks"></a><span data-ttu-id="426b1-200">目标和任务</span><span class="sxs-lookup"><span data-stu-id="426b1-200">Targets and Tasks</span></span>

<span data-ttu-id="426b1-201">在 MSBuild 架构中，[任务](https://msdn.microsoft.com/library/77f2hx1s.aspx)元素表示的各个生成指令 （或任务）。</span><span class="sxs-lookup"><span data-stu-id="426b1-201">In the MSBuild schema, a [Task](https://msdn.microsoft.com/library/77f2hx1s.aspx) element represents an individual build instruction (or task).</span></span> <span data-ttu-id="426b1-202">MSBuild 包括大量预定义的任务。</span><span class="sxs-lookup"><span data-stu-id="426b1-202">MSBuild includes a multitude of predefined tasks.</span></span> <span data-ttu-id="426b1-203">例如：</span><span class="sxs-lookup"><span data-stu-id="426b1-203">For example:</span></span>

- <span data-ttu-id="426b1-204">**复制**任务将文件复制到新位置。</span><span class="sxs-lookup"><span data-stu-id="426b1-204">The **Copy** task copies files to a new location.</span></span>
- <span data-ttu-id="426b1-205">**Csc**任务调用 Visual C# 编译器。</span><span class="sxs-lookup"><span data-stu-id="426b1-205">The **Csc** task invokes the Visual C# compiler.</span></span>
- <span data-ttu-id="426b1-206">**Vbc**任务调用 Visual Basic 编译器。</span><span class="sxs-lookup"><span data-stu-id="426b1-206">The **Vbc** task invokes the Visual Basic compiler.</span></span>
- <span data-ttu-id="426b1-207">**Exec**任务运行指定的程序。</span><span class="sxs-lookup"><span data-stu-id="426b1-207">The **Exec** task runs a specified program.</span></span>
- <span data-ttu-id="426b1-208">**消息**任务将一条消息写入到一个记录器。</span><span class="sxs-lookup"><span data-stu-id="426b1-208">The **Message** task writes a message to a logger.</span></span>

> [!NOTE]
> <span data-ttu-id="426b1-209">现成可用的任务的完整详细信息，请参阅[MSBuild 任务参考](https://msdn.microsoft.com/library/7z253716.aspx)。</span><span class="sxs-lookup"><span data-stu-id="426b1-209">For full details of the tasks that are available out of the box, see [MSBuild Task Reference](https://msdn.microsoft.com/library/7z253716.aspx).</span></span> <span data-ttu-id="426b1-210">有关详细信息的任务，包括如何创建您自己的自定义任务，请参阅[MSBuild 任务](https://msdn.microsoft.com/library/ms171466.aspx)。</span><span class="sxs-lookup"><span data-stu-id="426b1-210">For more information on tasks, including how to create your own custom tasks, see [MSBuild Tasks](https://msdn.microsoft.com/library/ms171466.aspx).</span></span>


<span data-ttu-id="426b1-211">任务必须始终包含在[目标](https://msdn.microsoft.com/library/t50z2hka.aspx)元素。</span><span class="sxs-lookup"><span data-stu-id="426b1-211">Tasks must always be contained within [Target](https://msdn.microsoft.com/library/t50z2hka.aspx) elements.</span></span> <span data-ttu-id="426b1-212">一个**目标**元素是一组按顺序执行的一个或多个任务和项目文件可以包含多个目标。</span><span class="sxs-lookup"><span data-stu-id="426b1-212">A **Target** element is a set of one or more tasks that are executed sequentially, and a project file can contain multiple targets.</span></span> <span data-ttu-id="426b1-213">当你想要运行一个任务或一组任务时，请调用包含它们的目标。</span><span class="sxs-lookup"><span data-stu-id="426b1-213">When you want to run a task, or a set of tasks, you invoke the target that contains them.</span></span> <span data-ttu-id="426b1-214">例如，假设您有一个简单的项目文件，将消息记录。</span><span class="sxs-lookup"><span data-stu-id="426b1-214">For example, suppose you have a simple project file that logs a message.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]


<span data-ttu-id="426b1-215">你可以通过调用从命令行中，目标 **/t** 开关指定目标。</span><span class="sxs-lookup"><span data-stu-id="426b1-215">You can invoke the target from the command line, by using the **/t** switch to specify the target.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]


<span data-ttu-id="426b1-216">或者，可以添加**DefaultTargets**归于**项目**元素，指定你想要调用的目标。</span><span class="sxs-lookup"><span data-stu-id="426b1-216">Alternatively, you can add a **DefaultTargets** attribute to the **Project** element, to specify the targets that you want to invoke.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]


<span data-ttu-id="426b1-217">在这种情况下，您不必指定命令行中的目标。</span><span class="sxs-lookup"><span data-stu-id="426b1-217">In this case, you don't need to specify the target from the command line.</span></span> <span data-ttu-id="426b1-218">您可以只需指定项目文件中，并调用 MSBuild **FullPublish**为您的目标。</span><span class="sxs-lookup"><span data-stu-id="426b1-218">You can simply specify the project file, and MSBuild will invoke the **FullPublish** target for you.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]


<span data-ttu-id="426b1-219">目标和任务可以包括**条件**属性。</span><span class="sxs-lookup"><span data-stu-id="426b1-219">Both targets and tasks can include **Condition** attributes.</span></span> <span data-ttu-id="426b1-220">在这种情况下，您可以选择忽略整个目标或单个任务，如果满足某些条件时。</span><span class="sxs-lookup"><span data-stu-id="426b1-220">As such, you can choose to omit entire targets or individual tasks if certain conditions are met.</span></span>

<span data-ttu-id="426b1-221">通常情况下，当您创建有用的任务和目标，将需要对属性和已在项目文件中其他位置定义的项，请参阅：</span><span class="sxs-lookup"><span data-stu-id="426b1-221">Generally speaking, when you create useful tasks and targets, you'll need to refer to the properties and items that you've defined elsewhere in the project file:</span></span>

- <span data-ttu-id="426b1-222">若要使用的属性值，请键入<strong>$(</strong><em>PropertyName</em><strong>)</strong>，其中<em>PropertyName</em>的名称<strong>属性</strong>元素或参数的名称。</span><span class="sxs-lookup"><span data-stu-id="426b1-222">To use a property value, type <strong>$(</strong><em>PropertyName</em><strong>)</strong>, where <em>PropertyName</em> is the name of the <strong>Property</strong> element or the name of the parameter.</span></span>
- <span data-ttu-id="426b1-223">若要使用的项，请键入<strong>@(</strong><em>ItemName</em><strong>)</strong>，其中<em>ItemName</em>的名称<strong>项</strong>元素。</span><span class="sxs-lookup"><span data-stu-id="426b1-223">To use an item, type <strong>@(</strong><em>ItemName</em><strong>)</strong>, where <em>ItemName</em> is the name of the <strong>Item</strong> element.</span></span>

> [!NOTE]
> <span data-ttu-id="426b1-224">请记住，是否具有相同名称创建多个项，你正在生成列表。</span><span class="sxs-lookup"><span data-stu-id="426b1-224">Remember that if you create multiple items with the same name, you're building a list.</span></span> <span data-ttu-id="426b1-225">与此相反，如果具有相同名称创建多个属性，您提供的最后一个属性值将覆盖任何以前的属性具有相同名称&#x2014;属性可以仅包含单个值。</span><span class="sxs-lookup"><span data-stu-id="426b1-225">In contrast, if you create multiple properties with the same name, the last property value you provide will overwrite any previous properties with the same name&#x2014;a property can only contain a single value.</span></span>


<span data-ttu-id="426b1-226">例如，在*Publish.proj*文件中的示例解决方案中，看一看**BuildProjects**目标。</span><span class="sxs-lookup"><span data-stu-id="426b1-226">For example, in the *Publish.proj* file in the sample solution, take a look at the **BuildProjects** target.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]


<span data-ttu-id="426b1-227">在此示例中，您可以观察这些关键点：</span><span class="sxs-lookup"><span data-stu-id="426b1-227">In this sample, you can observe these key points:</span></span>

- <span data-ttu-id="426b1-228">如果**BuildingInTeamBuild**参数指定了和的值为**true**，此目标中的任务都不会执行。</span><span class="sxs-lookup"><span data-stu-id="426b1-228">If the **BuildingInTeamBuild** parameter is specified and has a value of **true**, none of the tasks within this target will be executed.</span></span>
- <span data-ttu-id="426b1-229">目标包含的单一实例[MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx)任务。</span><span class="sxs-lookup"><span data-stu-id="426b1-229">The target contains a single instance of the [MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx) task.</span></span> <span data-ttu-id="426b1-230">此任务可以生成其他 MSBuild 项目。</span><span class="sxs-lookup"><span data-stu-id="426b1-230">This task lets you build other MSBuild projects.</span></span>
- <span data-ttu-id="426b1-231">**ProjectsToBuild**项传递给任务。</span><span class="sxs-lookup"><span data-stu-id="426b1-231">The **ProjectsToBuild** item is passed to the task.</span></span> <span data-ttu-id="426b1-232">此项可以表示项目或解决方案文件，所有已定义的一系列**ProjectsToBuild**项的项组中的元素。</span><span class="sxs-lookup"><span data-stu-id="426b1-232">This item could represent a list of project or solution files, all defined by **ProjectsToBuild** item elements within an item group.</span></span> <span data-ttu-id="426b1-233">在这种情况下， **ProjectsToBuild**项引用的单一解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="426b1-233">In this case, the **ProjectsToBuild** item refers to a single solution file.</span></span>

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- <span data-ttu-id="426b1-234">属性值传递给**MSBuild**任务包括参数名为**OutputRoot**并**配置**。</span><span class="sxs-lookup"><span data-stu-id="426b1-234">The property values passed to the **MSBuild** task include parameters named **OutputRoot** and **Configuration**.</span></span> <span data-ttu-id="426b1-235">如果未为如果它们提供参数值或静态属性值设置。</span><span class="sxs-lookup"><span data-stu-id="426b1-235">These are set to parameter values if they are provided, or static property values if they are not.</span></span>

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

<span data-ttu-id="426b1-236">您还可以看到**MSBuild**任务调用名为的目标**生成**。</span><span class="sxs-lookup"><span data-stu-id="426b1-236">You can also see that the **MSBuild** task invokes a target named **Build**.</span></span> <span data-ttu-id="426b1-237">这是一个广泛应用于 Visual Studio 项目文件，并且可以向你在自定义项目文件，如的几个内置目标**构建**，**清理**，**重新生成**，并**发布**。</span><span class="sxs-lookup"><span data-stu-id="426b1-237">This is one of several built-in targets that are widely used in Visual Studio project files and are available to you in your custom project files, like **Build**, **Clean**, **Rebuild**, and **Publish**.</span></span> <span data-ttu-id="426b1-238">您将学习有关使用目标和任务，来控制生成过程中，以及有关的详细信息**MSBuild**任务具体而言，本主题中的更高版本。</span><span class="sxs-lookup"><span data-stu-id="426b1-238">You'll learn more about using targets and tasks to control the build process, and about the **MSBuild** task in particular, later in this topic.</span></span>

> [!NOTE]
> <span data-ttu-id="426b1-239">在目标上的详细信息，请参阅[MSBuild 目标](https://msdn.microsoft.com/library/ms171462.aspx)。</span><span class="sxs-lookup"><span data-stu-id="426b1-239">For more information on targets, see [MSBuild Targets](https://msdn.microsoft.com/library/ms171462.aspx).</span></span>


## <a name="splitting-project-files-to-support-multiple-environments"></a><span data-ttu-id="426b1-240">拆分项目文件，以支持多个环境</span><span class="sxs-lookup"><span data-stu-id="426b1-240">Splitting Project Files to Support Multiple Environments</span></span>

<span data-ttu-id="426b1-241">假设你想要能够将解决方案部署到多个环境，如测试服务器、 过渡平台和生产环境。</span><span class="sxs-lookup"><span data-stu-id="426b1-241">Suppose you want to be able to deploy a solution to multiple environments, like test servers, staging platforms, and production environments.</span></span> <span data-ttu-id="426b1-242">配置可能差别很大这些环境之间&#x2014;不只是根据服务器名称、 连接字符串等，但也可能会在凭据、 安全设置和其他因素的很多方面。</span><span class="sxs-lookup"><span data-stu-id="426b1-242">The configuration may vary substantially between these environments&#x2014;not just in terms of server names, connection strings, and so on, but also potentially in terms of credentials, security settings, and lots of other factors.</span></span> <span data-ttu-id="426b1-243">如果需要定期执行此操作，不真正便利，若要编辑项目文件中的多个属性，每次切换目标环境。</span><span class="sxs-lookup"><span data-stu-id="426b1-243">If you need to do this regularly, it's not really expedient to edit multiple properties in your project file every time you switch the target environment.</span></span> <span data-ttu-id="426b1-244">也不是一个理想的解决方案需要的属性值提供给生成过程的无限列表。</span><span class="sxs-lookup"><span data-stu-id="426b1-244">Nor is it an ideal solution to require an endless list of property values to be provided to the build process.</span></span>

<span data-ttu-id="426b1-245">幸运的是一种替代方法。</span><span class="sxs-lookup"><span data-stu-id="426b1-245">Fortunately there is an alternative.</span></span> <span data-ttu-id="426b1-246">MSBuild，可跨多个项目文件拆分生成配置。</span><span class="sxs-lookup"><span data-stu-id="426b1-246">MSBuild lets you split your build configuration across multiple project files.</span></span> <span data-ttu-id="426b1-247">若要查看此工作原理，在示例解决方案中，请注意，有两个自定义项目文件：</span><span class="sxs-lookup"><span data-stu-id="426b1-247">To see how this works, in the sample solution, notice that there are two custom project files:</span></span>

- <span data-ttu-id="426b1-248">*Publish.proj*，它包含属性、 项和普遍适用于所有环境的目标是。</span><span class="sxs-lookup"><span data-stu-id="426b1-248">*Publish.proj*, which contains properties, items, and targets that are common to all environments.</span></span>
- <span data-ttu-id="426b1-249">*Env Dev.proj*，其中包含特定于开发人员环境的属性。</span><span class="sxs-lookup"><span data-stu-id="426b1-249">*Env-Dev.proj*, which contains properties that are specific to a developer environment.</span></span>

<span data-ttu-id="426b1-250">现在请注意， *Publish.proj*文件包含[导入](https://msdn.microsoft.com/library/92x05xfs.aspx)元素中的，紧跟在左括号下方**项目**标记。</span><span class="sxs-lookup"><span data-stu-id="426b1-250">Now notice that the *Publish.proj* file includes an [Import](https://msdn.microsoft.com/library/92x05xfs.aspx) element, immediately beneath the opening **Project** tag.</span></span>


[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]


<span data-ttu-id="426b1-251">**导入**元素用于将另一个 MSBuild 项目文件的内容导入当前的 MSBuild 项目文件。</span><span class="sxs-lookup"><span data-stu-id="426b1-251">The **Import** element is used to import the contents of another MSBuild project file into the current MSBuild project file.</span></span> <span data-ttu-id="426b1-252">在这种情况下， **TargetEnvPropsFile**参数提供了你想要导入的项目文件的文件名。</span><span class="sxs-lookup"><span data-stu-id="426b1-252">In this case, the **TargetEnvPropsFile** parameter provides the filename of the project file you want to import.</span></span> <span data-ttu-id="426b1-253">运行 MSBuild 时，可以为此参数提供值。</span><span class="sxs-lookup"><span data-stu-id="426b1-253">You can provide a value for this parameter when you run MSBuild.</span></span>


[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]


<span data-ttu-id="426b1-254">这有效地将两个文件的内容合并到单个项目文件。</span><span class="sxs-lookup"><span data-stu-id="426b1-254">This effectively merges the contents of the two files into a single project file.</span></span> <span data-ttu-id="426b1-255">使用此方法，可以创建一个项目文件包含通用的生成配置和多个包含特定于环境的属性的补充项目文件。</span><span class="sxs-lookup"><span data-stu-id="426b1-255">Using this approach, you can create one project file containing your universal build configuration and multiple supplementary project files containing environment-specific properties.</span></span> <span data-ttu-id="426b1-256">因此，只需运行命令的不同参数值，你可以将你的解决方案部署到不同环境。</span><span class="sxs-lookup"><span data-stu-id="426b1-256">As a result, simply running a command with a different parameter value lets you deploy your solution to a different environment.</span></span>

![](understanding-the-project-file/_static/image3.png)

<span data-ttu-id="426b1-257">拆分项目文件以这种方式是遵循一个好办法。</span><span class="sxs-lookup"><span data-stu-id="426b1-257">Splitting your project files in this way is a good practice to follow.</span></span> <span data-ttu-id="426b1-258">它允许开发人员通过运行单个命令，同时避免了重复的通用生成属性跨多个项目文件将部署到多个环境。</span><span class="sxs-lookup"><span data-stu-id="426b1-258">It allows developers to deploy to multiple environments by running a single command, while avoiding the duplication of universal build properties across multiple project files.</span></span>

> [!NOTE]
> <span data-ttu-id="426b1-259">有关如何自定义服务器环境的特定于环境的项目文件的指南，请参阅[配置目标环境的部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="426b1-259">For guidance on how to customize the environment-specific project files for your own server environments, see [Configuring Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>


## <a name="conclusion"></a><span data-ttu-id="426b1-260">结束语</span><span class="sxs-lookup"><span data-stu-id="426b1-260">Conclusion</span></span>

<span data-ttu-id="426b1-261">本主题提供对 MSBuild 项目文件的常规介绍，并介绍了如何创建您自己的自定义项目文件来控制生成过程。</span><span class="sxs-lookup"><span data-stu-id="426b1-261">This topic provided a general introduction to MSBuild project files and explained how you can create your own custom project files to control the build process.</span></span> <span data-ttu-id="426b1-262">它还引入了将项目文件拆分为通用生成说明和特定于环境的生成属性，以轻松地生成并部署到多个目标的项目的概念。</span><span class="sxs-lookup"><span data-stu-id="426b1-262">It also introduced the concept of splitting project files into universal build instructions and environment-specific build properties, to make it easy to build and deploy projects to multiple destinations.</span></span>

<span data-ttu-id="426b1-263">下一主题[了解构建过程](understanding-the-build-process.md)，提供了更详细地了解如何通过引导您完成实际的复杂性级别部署的解决方案使用为控件生成和部署的项目文件。</span><span class="sxs-lookup"><span data-stu-id="426b1-263">The next topic, [Understanding the Build Process](understanding-the-build-process.md), provides more insight into how you can use project files to control build and deployment by walking you through the deployment of a solution with a realistic level of complexity.</span></span>

## <a name="further-reading"></a><span data-ttu-id="426b1-264">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="426b1-264">Further Reading</span></span>

<span data-ttu-id="426b1-265">项目文件和 WPP 的更深入介绍，请参阅[内部 Microsoft 生成引擎： 使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 和 William Bartholomew，ISBN: 978-0-7356-4524-0。</span><span class="sxs-lookup"><span data-stu-id="426b1-265">For a more in-depth introduction to project files and the WPP, see [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://amzn.com/0735645248) by Sayed Ibrahim Hashimi and William Bartholomew, ISBN: 978-0-7356-4524-0.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="426b1-266">[上一页](setting-up-the-contact-manager-solution.md)
> [下一页](understanding-the-build-process.md)</span><span class="sxs-lookup"><span data-stu-id="426b1-266">[Previous](setting-up-the-contact-manager-solution.md)
[Next](understanding-the-build-process.md)</span></span>
