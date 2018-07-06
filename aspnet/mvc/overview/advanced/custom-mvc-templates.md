---
uid: mvc/overview/advanced/custom-mvc-templates
title: 自定义 MVC 模板 |Microsoft Docs
author: joeloff
description: 创建一个模板作为 VSIX 扩展。
ms.author: aspnetcontent
ms.date: 12/10/2012
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: 67cb01e0fae036f01b1851695ae5a4358136d28e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809772"
---
<a name="custom-mvc-template"></a><span data-ttu-id="9950f-103">自定义 MVC 模板</span><span class="sxs-lookup"><span data-stu-id="9950f-103">Custom MVC Template</span></span>
====================
<span data-ttu-id="9950f-104">通过[3。jacques Eloff](https://github.com/joeloff)</span><span class="sxs-lookup"><span data-stu-id="9950f-104">by [Jacques Eloff](https://github.com/joeloff)</span></span>

<span data-ttu-id="9950f-105">MVC 3 Tools Update for Visual Studio 2010 的版本引入了用于 MVC 项目的单独的项目向导。</span><span class="sxs-lookup"><span data-stu-id="9950f-105">The release of MVC 3 Tools Update for Visual Studio 2010 introduced a separate project wizard for MVC projects.</span></span> <span data-ttu-id="9950f-106">更改主要依靠两个因素。</span><span class="sxs-lookup"><span data-stu-id="9950f-106">The change was driven by two factors.</span></span> <span data-ttu-id="9950f-107">首先，在 MVC 3 和附加视图引擎，如 Razor 的支持中的新模板的引入导致 overcrowding Visual Studio 中的新建项目对话框。</span><span class="sxs-lookup"><span data-stu-id="9950f-107">First, the introduction of new templates in MVC 3 and support for additional view engines such as Razor lead to overcrowding the New Project dialog in Visual Studio.</span></span> <span data-ttu-id="9950f-108">其次，客户必须一直期盼的扩展点和新的 MVC 项目向导将提供了我们对这些请求作出响应。</span><span class="sxs-lookup"><span data-stu-id="9950f-108">Second, customers had been asking for extensibility points and the new MVC project wizard would afford us the opportunity to respond to these requests.</span></span>

<span data-ttu-id="9950f-109">添加自定义模板是依赖于使用注册表来使新模板对 MVC 项目向导可见的艰辛旅程。</span><span class="sxs-lookup"><span data-stu-id="9950f-109">Adding custom templates was an arduous process that relied on using the registry to make new templates visible to the MVC project wizard.</span></span> <span data-ttu-id="9950f-110">新模板的作者必须将其封装在 MSI 来确保将在安装时创建必要的注册表项。</span><span class="sxs-lookup"><span data-stu-id="9950f-110">The author of a new template had to wrap it inside an MSI to ensure that the necessary registry entries would be created at install time.</span></span> <span data-ttu-id="9950f-111">另一个方法是使包含可用模板的 ZIP 文件，并让最终用户手动创建必需的注册表项。</span><span class="sxs-lookup"><span data-stu-id="9950f-111">The alternative was to make a ZIP file containing the template available and have the end-user create the required registry entries by hand.</span></span>

<span data-ttu-id="9950f-112">前面提到的方法都不是理想选择，因此我们决定是使用提供的现有基础结构[VSIX](https://msdn.microsoft.com/library/ff363239.aspx)扩展以更简单地将作者、 分发和安装自定义 MVC 模板从 MVC 4 开始适用于 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="9950f-112">Neither of the aforementioned approaches is ideal so we decided to leverage some of the existing infrastructure provided by [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) extensions to make it easier to author, distribute and install custom MVC templates starting with MVC 4 for Visual Studio 2012.</span></span> <span data-ttu-id="9950f-113">这种方法提供的好处包括：</span><span class="sxs-lookup"><span data-stu-id="9950f-113">Some of the benefits provided by this approach are:</span></span>

- <span data-ttu-id="9950f-114">VSIX 扩展包含支持不同的语言 （C# 和 Visual Basic） 的多个模板和多个视图引擎 （ASPX 和 Razor）。</span><span class="sxs-lookup"><span data-stu-id="9950f-114">A VSIX extension can contain multiple templates that support different languages (C# and Visual Basic) and multiple view engines (ASPX and Razor).</span></span>
- <span data-ttu-id="9950f-115">VSIX 扩展可以面向多个 Sku 的 Visual Studio 包括速成版 Sku。</span><span class="sxs-lookup"><span data-stu-id="9950f-115">A VSIX extension can target multiple SKUs of Visual Studio including Express SKUs.</span></span>
- <span data-ttu-id="9950f-116">[Visual Studio 库](https://visualstudiogallery.msdn.microsoft.com/)便于分发给广泛的受众扩展。</span><span class="sxs-lookup"><span data-stu-id="9950f-116">The [Visual Studio Gallery](https://visualstudiogallery.msdn.microsoft.com/) facilitates distributing the extension to a wide audience.</span></span>
- <span data-ttu-id="9950f-117">VSIX 扩展可以更轻松地创作的更正和对自定义模板的更新进行升级。</span><span class="sxs-lookup"><span data-stu-id="9950f-117">VSIX extensions can be upgraded making it easier to author corrections and updates to your custom templates.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9950f-118">系统必备</span><span class="sxs-lookup"><span data-stu-id="9950f-118">Prerequisites</span></span>

- <span data-ttu-id="9950f-119">用户需要熟悉创作项目模板，其中包括 vstemplate 文件等所需的标记。</span><span class="sxs-lookup"><span data-stu-id="9950f-119">Users need to be familiar with authoring project templates, including the required markup for vstemplate files, etc.</span></span>
- <span data-ttu-id="9950f-120">用户将需要具有 Visual Studio Professional 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="9950f-120">Users will need to have Visual Studio Professional and higher installed.</span></span> <span data-ttu-id="9950f-121">Express Sku 不支持创建 VSIX 项目。</span><span class="sxs-lookup"><span data-stu-id="9950f-121">Express SKUs do not support creating VSIX projects.</span></span>
- <span data-ttu-id="9950f-122">[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668)安装。</span><span class="sxs-lookup"><span data-stu-id="9950f-122">[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) installed.</span></span>

## <a name="example"></a><span data-ttu-id="9950f-123">示例</span><span class="sxs-lookup"><span data-stu-id="9950f-123">Example</span></span>

<span data-ttu-id="9950f-124">第一步是创建使用 C# 或 Visual Basic 的新 VSIX 项目。</span><span class="sxs-lookup"><span data-stu-id="9950f-124">The first step is to create a new VSIX project using either C# or Visual Basic.</span></span> <span data-ttu-id="9950f-125">选择**文件 > 新建项目**，然后单击**扩展性**在左窗格中，选择**VSIX 项目**。</span><span class="sxs-lookup"><span data-stu-id="9950f-125">Select **File > New Project**, then click **Extensibility** in the left pane and select the **VSIX Project**.</span></span>

![新建项目](custom-mvc-templates/_static/image1.jpg)

<span data-ttu-id="9950f-127">创建项目后，将打开 VSIX 设计器。</span><span class="sxs-lookup"><span data-stu-id="9950f-127">After the project is created, the VSIX designer will be opened.</span></span>

![项目设计器元数据](custom-mvc-templates/_static/image2.jpg)

<span data-ttu-id="9950f-129">在设计器可用于编辑某些安装扩展或浏览 Visual Studio 中已安装的扩展时，将向用户显示的扩展的常规属性 (**工具 > 扩展和更新**)。</span><span class="sxs-lookup"><span data-stu-id="9950f-129">The designer can be used to edit some of the general properties of the extension that will be shown to users when they install the extension or browse the installed extensions in Visual Studio (**Tools > Extensions and Updates**).</span></span> <span data-ttu-id="9950f-130">完成后的常规信息，请单击**安装目标选项卡**。</span><span class="sxs-lookup"><span data-stu-id="9950f-130">Once you have completed the general information click on the **Install Targets tab**.</span></span>

![项目设计器的安装目标](custom-mvc-templates/_static/image3.jpg)

<span data-ttu-id="9950f-132">此选项卡用于指定 Sku 和版本的 Visual Studio 支持的扩展。</span><span class="sxs-lookup"><span data-stu-id="9950f-132">This tab is used to specify the SKUs and versions of Visual Studio that are supported by your extension.</span></span> <span data-ttu-id="9950f-133">选中的复选框**的所有用户安装此 VSIX**若要启用每台计算机安装的 VSIX。</span><span class="sxs-lookup"><span data-stu-id="9950f-133">Select the checkbox for **This VSIX is installed for all users** to enable per-machine installs of the VSIX.</span></span> <span data-ttu-id="9950f-134">单击**新建**右侧添加其他 Sku 等 Web Developer Express (VWD) 按钮。</span><span class="sxs-lookup"><span data-stu-id="9950f-134">Click on the **New** button on the right to add additional SKUs such as Web Developer Express (VWD).</span></span>

![添加新的安装目标](custom-mvc-templates/_static/image4.jpg)

<span data-ttu-id="9950f-136">如果您打算支持的所有专业和更高版本的 Sku （Professional、 Premium 和 Ultimate） 只需在系列中选择的最小 SKU **Microsoft.VisualStudio.Pro**。</span><span class="sxs-lookup"><span data-stu-id="9950f-136">If you intend to support all the Professional and higher SKUs (Professional, Premium and Ultimate) you only need to select the minimum SKU in the family, **Microsoft.VisualStudio.Pro**.</span></span> <span data-ttu-id="9950f-137">请记住保存所有更改完成后安装目标。</span><span class="sxs-lookup"><span data-stu-id="9950f-137">Remember to save all your changes once you have completed the Install Targets.</span></span>

![项目设计器的安装目标](custom-mvc-templates/_static/image5.jpg)

<span data-ttu-id="9950f-139">**资产**选项卡用于将所有内容文件添加到 VSIX。</span><span class="sxs-lookup"><span data-stu-id="9950f-139">The **Assets** tab is used to add all your content files to the VSIX.</span></span> <span data-ttu-id="9950f-140">由于 MVC 需要自定义元数据，因此将编辑而不是使用 VSIX 清单文件的原始 XML**资产**选项卡添加内容。</span><span class="sxs-lookup"><span data-stu-id="9950f-140">Since MVC requires custom metadata you will be editing the raw XML of the VSIX manifest file instead of using the **Assets** tab to add content.</span></span> <span data-ttu-id="9950f-141">首先将模板内容添加到 VSIX 项目。</span><span class="sxs-lookup"><span data-stu-id="9950f-141">Start by adding the template contents to the VSIX project.</span></span> <span data-ttu-id="9950f-142">非常重要的文件夹及其内容的结构，镜像的项目布局。</span><span class="sxs-lookup"><span data-stu-id="9950f-142">It is important that the structure of the folder and the contents mirror the layout of the project.</span></span> <span data-ttu-id="9950f-143">下面的示例包含四个项目模板从基本的 MVC 项目模板派生的。</span><span class="sxs-lookup"><span data-stu-id="9950f-143">The example below contains four project templates that were derived from the Basic MVC project template.</span></span> <span data-ttu-id="9950f-144">请确保包含你的项目模板 （ProjectTemplates 文件夹下的所有内容） 的所有文件都添加到**内容**itemgroup 在 VSIX 项目文件和每个项包含**CopyToOutputDirectory**并**IncludeInVsix**设置元数据，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="9950f-144">Make sure that all the files that comprise your project template (everything underneath the ProjectTemplates folder) are added to the **Content** itemgroup in the VSIX project file and that each item contains the **CopyToOutputDirectory** and **IncludeInVsix** metadata set as shown in the example below.</span></span>

<span data-ttu-id="9950f-145">&lt;Content Include=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="9950f-145">&lt;Content Include=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span></span>

<span data-ttu-id="9950f-146">&lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;</span><span class="sxs-lookup"><span data-stu-id="9950f-146">&lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;</span></span>

<span data-ttu-id="9950f-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span><span class="sxs-lookup"><span data-stu-id="9950f-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span></span>

<span data-ttu-id="9950f-148">&lt;/Content&gt;</span><span class="sxs-lookup"><span data-stu-id="9950f-148">&lt;/Content&gt;</span></span>

<span data-ttu-id="9950f-149">否则，IDE 将尝试生成 VSIX 和你可能会看到错误时进行编译模板的内容。</span><span class="sxs-lookup"><span data-stu-id="9950f-149">If not, the IDE will try to compile the contents of the template when you build the VSIX and you will likely see an error.</span></span> <span data-ttu-id="9950f-150">在模板中的代码文件通常包含特殊[模板参数](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx)Visual Studio 项目模板实例化并因此不能在 IDE 中编译时使用。</span><span class="sxs-lookup"><span data-stu-id="9950f-150">Code files in templates often contain special [template parameters](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) used by Visual Studio when the project template is instantiated and therefore cannot be compiled in the IDE.</span></span>

![“解决方案资源管理器”](custom-mvc-templates/_static/image6.jpg)

<span data-ttu-id="9950f-152">关闭 VSIX 设计器中，然后右键单击**source.extension.manifest**中的文件**解决方案资源管理器**，然后选择**打开**，然后选择**XML (文本） 编辑器**选项。</span><span class="sxs-lookup"><span data-stu-id="9950f-152">Close the VSIX designer, then right click on the **source.extension.manifest** file in **Solution Explorer** and select **Open With** and choose the **XML (Text) Editor** option.</span></span>

![打开对话框](custom-mvc-templates/_static/image7.jpg)

<span data-ttu-id="9950f-154">创建**&lt;资产&gt;** 元素，并添加**&lt;资产&gt;** 元素必须包括在 VSIX 中的每个文件。</span><span class="sxs-lookup"><span data-stu-id="9950f-154">Create an **&lt;Assets&gt;** element and add an **&lt;Asset&gt;** element for each file that must be included in the VSIX.</span></span> <span data-ttu-id="9950f-155">**类型**属性的每个**&lt;资产&gt;** 元素必须设置为**Microsoft.VisualStudio.Mvc.Template**。</span><span class="sxs-lookup"><span data-stu-id="9950f-155">The **Type** attribute of each **&lt;Asset&gt;** element must be set to **Microsoft.VisualStudio.Mvc.Template**.</span></span> <span data-ttu-id="9950f-156">这是 MVC 的项目向导能够理解的自定义命名空间。</span><span class="sxs-lookup"><span data-stu-id="9950f-156">This is a custom namespace that only the MVC project wizard understands.</span></span> <span data-ttu-id="9950f-157">请参阅有关其他信息的结构和清单文件的布局 VSIX 2.0 架构文档。</span><span class="sxs-lookup"><span data-stu-id="9950f-157">Refer to the VSIX 2.0 Schema documentation for additional information on the structure and layout of the manifest file.</span></span>

<span data-ttu-id="9950f-158">只需将文件添加到 VSIX 不足以使用 MVC 向导注册模板。</span><span class="sxs-lookup"><span data-stu-id="9950f-158">Just adding the files to the VSIX is not sufficient to register the templates with the MVC wizard.</span></span> <span data-ttu-id="9950f-159">您需要向 MVC 向导提供模板名称、 说明、 受支持的视图引擎和编程语言等信息。</span><span class="sxs-lookup"><span data-stu-id="9950f-159">You need to provide information such as the template name, description, supported view engines and programming language to the MVC wizard.</span></span> <span data-ttu-id="9950f-160">此信息与相关联的自定义属性中携带**&lt;资产&gt;** 每个元素**vstemplate**文件。</span><span class="sxs-lookup"><span data-stu-id="9950f-160">This information is carried in custom attributes associated with the **&lt;Asset&gt;** element for each **vstemplate** file.</span></span>

<span data-ttu-id="9950f-161">&lt;Asset d:VsixSubPath=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span><span class="sxs-lookup"><span data-stu-id="9950f-161">&lt;Asset d:VsixSubPath=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span></span>

<span data-ttu-id="9950f-162">Type=&quot;Microsoft.VisualStudio.Mvc.Template&quot;</span><span class="sxs-lookup"><span data-stu-id="9950f-162">Type=&quot;Microsoft.VisualStudio.Mvc.Template&quot;</span></span>

<span data-ttu-id="9950f-163">d:Source=&quot;File&quot;</span><span class="sxs-lookup"><span data-stu-id="9950f-163">d:Source=&quot;File&quot;</span></span>

<span data-ttu-id="9950f-164">Path=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span><span class="sxs-lookup"><span data-stu-id="9950f-164">Path=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span></span>

<span data-ttu-id="9950f-165">ProjectType=&quot;MVC&quot;</span><span class="sxs-lookup"><span data-stu-id="9950f-165">ProjectType=&quot;MVC&quot;</span></span>

<span data-ttu-id="9950f-166">语言 =&quot;C#&quot;</span><span class="sxs-lookup"><span data-stu-id="9950f-166">Language=&quot;C#&quot;</span></span>

<span data-ttu-id="9950f-167">ViewEngine=&quot;Aspx&quot;</span><span class="sxs-lookup"><span data-stu-id="9950f-167">ViewEngine=&quot;Aspx&quot;</span></span>

<span data-ttu-id="9950f-168">TemplateId=&quot;MyMvcApplication&quot;</span><span class="sxs-lookup"><span data-stu-id="9950f-168">TemplateId=&quot;MyMvcApplication&quot;</span></span>

<span data-ttu-id="9950f-169">Title =&quot;自定义基本 Web 应用程序&quot;</span><span class="sxs-lookup"><span data-stu-id="9950f-169">Title=&quot;Custom Basic Web Application&quot;</span></span>

<span data-ttu-id="9950f-170">说明 =&quot;自定义模板派生自基本 MVC web 应用程序 (Razor)&quot;</span><span class="sxs-lookup"><span data-stu-id="9950f-170">Description=&quot;A custom template derived from a Basic MVC web application (Razor)&quot;</span></span>

<span data-ttu-id="9950f-171">版本 =&quot;4.0&quot;/&gt;</span><span class="sxs-lookup"><span data-stu-id="9950f-171">Version=&quot;4.0&quot;/&gt;</span></span>

<span data-ttu-id="9950f-172">下面是必须存在的自定义特性的说明：</span><span class="sxs-lookup"><span data-stu-id="9950f-172">Below is an explanation of the custom attributes that must be present:</span></span>

- <span data-ttu-id="9950f-173">**ProjectType**必须设置为 MVC。</span><span class="sxs-lookup"><span data-stu-id="9950f-173">**ProjectType** must be set to MVC.</span></span>
- <span data-ttu-id="9950f-174">**语言**指定模板支持的开发语言。</span><span class="sxs-lookup"><span data-stu-id="9950f-174">**Language** designates the development language supported by the template.</span></span> <span data-ttu-id="9950f-175">有效值为 C# 或 vb。</span><span class="sxs-lookup"><span data-stu-id="9950f-175">Valid values are either C# or VB.</span></span>
- <span data-ttu-id="9950f-176">**ViewEngine**指定如 Aspx 或 Razor 模板还支持在视图引擎。</span><span class="sxs-lookup"><span data-stu-id="9950f-176">**ViewEngine** designates the view engine supported by the template such as Aspx or Razor.</span></span> <span data-ttu-id="9950f-177">可以指定此字段的自定义值。</span><span class="sxs-lookup"><span data-stu-id="9950f-177">You can specify a custom value for this field.</span></span>
- <span data-ttu-id="9950f-178">**TemplateId**用于对模板进行分组。</span><span class="sxs-lookup"><span data-stu-id="9950f-178">**TemplateId** is used for grouping the templates.</span></span> <span data-ttu-id="9950f-179">如果值匹配的现有模板 ID，它将重写以前注册到 MVC 向导的模板。</span><span class="sxs-lookup"><span data-stu-id="9950f-179">If the value matches an existing template ID it will be override templates previously registered with the MVC wizard.</span></span>
- <span data-ttu-id="9950f-180">**标题**指定显示在 MVC 向导下每个项目模板的简短描述。</span><span class="sxs-lookup"><span data-stu-id="9950f-180">**Title** designates the short description displayed in the MVC wizard beneath each project template.</span></span>
- <span data-ttu-id="9950f-181">**说明**指定模板的更详细说明。</span><span class="sxs-lookup"><span data-stu-id="9950f-181">**Description** designates a more verbose description of the template.</span></span>

<span data-ttu-id="9950f-182">所有文件都添加到清单并保存它，您将注意到，之后**资产**设计器中的选项卡将显示所有文件，但未自定义属性都添加到**&lt;资产&gt;** 个元素**vstemplate**文件。</span><span class="sxs-lookup"><span data-stu-id="9950f-182">After you have added all the files to the manifest and saved it, you will notice that the **Assets** tab in the designer will display all the files, but not the custom attributes you added to the **&lt;Asset&gt;** elements for the **vstemplate** files.</span></span>

![项目设计器资产](custom-mvc-templates/_static/image8.jpg)

<span data-ttu-id="9950f-184">所有的就现在是编译 VSIX 项目并将其安装。</span><span class="sxs-lookup"><span data-stu-id="9950f-184">All that remains now is to compile the VSIX project and install it.</span></span>

<span data-ttu-id="9950f-185">请确保 Visual Studio 的所有实例已都关闭的计算机上你想要测试此 VSIX 扩展。</span><span class="sxs-lookup"><span data-stu-id="9950f-185">Make sure that all instances of Visual Studio are closed on the machine where you intend to test the VSIX extension.</span></span> <span data-ttu-id="9950f-186">Visual Studio 会扫描新的扩展在启动期间，因此如果 IDE 打开安装 VSIX 时将需要重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9950f-186">Visual Studio scans for new extensions during startup, so if the IDE is open while installing a VSIX you will need to restart Visual Studio.</span></span> <span data-ttu-id="9950f-187">在资源管理器中，双击 VSIX 文件，启动**VSIX 安装程序**，单击**安装**，然后启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9950f-187">In Explorer, double click on the VSIX file to launch the **VSIX Installer**, click **Install** and then launch Visual Studio.</span></span>

![VSIX 安装程序](custom-mvc-templates/_static/image9.jpg)

<span data-ttu-id="9950f-189">从菜单中选择**工具 > 扩展和更新**若要确认是否已安装扩展。</span><span class="sxs-lookup"><span data-stu-id="9950f-189">From the menu, select **Tools > Extensions and Updates** to confirm that your extension was installed.</span></span> <span data-ttu-id="9950f-190">如果在扩展安装期间，VSIX 安装程序报告任何错误可以查看 VSIX 安装程序日志以了解更多信息。</span><span class="sxs-lookup"><span data-stu-id="9950f-190">If the VSIX Installer reported any errors during the installation of the extension you can view the VSIX Installer log for more information.</span></span> <span data-ttu-id="9950f-191">通常在创建该日志 **%temp%** 安装扩展，例如在用户文件夹**C:\Users\Bob\AppData\Local\Temp**。</span><span class="sxs-lookup"><span data-stu-id="9950f-191">The log is usually created in the **%temp%** folder of the user that installed the extension, for example **C:\Users\Bob\AppData\Local\Temp**.</span></span>

![扩展和更新](custom-mvc-templates/_static/image10.jpg)

<span data-ttu-id="9950f-193">关闭窗口后可以创建一个 MVC 4 项目以查看是否在 MVC 向导中显示新模板。</span><span class="sxs-lookup"><span data-stu-id="9950f-193">After closing the window you can create an MVC 4 project to see whether your new templates are shown in the MVC wizard.</span></span>

![新的 ASP.NET MVC 4 项目](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a><span data-ttu-id="9950f-195">限制</span><span class="sxs-lookup"><span data-stu-id="9950f-195">Limitations</span></span>

1. <span data-ttu-id="9950f-196">MVC 向导不支持本地化的自定义模板。</span><span class="sxs-lookup"><span data-stu-id="9950f-196">The MVC wizard does not support localized custom templates.</span></span>
2. <span data-ttu-id="9950f-197">如果无法找到自定义模板，该向导将不会报告任何错误。</span><span class="sxs-lookup"><span data-stu-id="9950f-197">The wizard will not report any errors if it fails to locate custom templates.</span></span> <span data-ttu-id="9950f-198">如果任何所需的自定义属性不存在，将只需从向导中排除该模板。</span><span class="sxs-lookup"><span data-stu-id="9950f-198">If any of the required custom attributes are absent, the template would simply be excluded from the Wizard.</span></span>
