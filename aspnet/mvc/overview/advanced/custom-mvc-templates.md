---
uid: mvc/overview/advanced/custom-mvc-templates
title: 自定义 MVC 模板 |Microsoft 文档
author: joeloff
description: 创建模板作为 VSIX 扩展。
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/10/2012
ms.topic: article
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: c3ddd4e341511f520927e924b25d890088adb69e
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "28034602"
---
<a name="custom-mvc-template"></a><span data-ttu-id="9f015-103">自定义 MVC 模板</span><span class="sxs-lookup"><span data-stu-id="9f015-103">Custom MVC Template</span></span>
====================
<span data-ttu-id="9f015-104">通过[Jacques Eloff](https://github.com/joeloff)</span><span class="sxs-lookup"><span data-stu-id="9f015-104">by [Jacques Eloff](https://github.com/joeloff)</span></span>

<span data-ttu-id="9f015-105">对于 Visual Studio 2010 的 MVC 3 Tools 更新版本引入了单独的项目向导的 MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="9f015-105">The release of MVC 3 Tools Update for Visual Studio 2010 introduced a separate project wizard for MVC projects.</span></span> <span data-ttu-id="9f015-106">之所以更改是两个因素。</span><span class="sxs-lookup"><span data-stu-id="9f015-106">The change was driven by two factors.</span></span> <span data-ttu-id="9f015-107">首先，在 MVC 3 和支持的其他视图引擎，如 Razor 的新模板的引入导致 overcrowding Visual Studio 中的新建项目对话框。</span><span class="sxs-lookup"><span data-stu-id="9f015-107">First, the introduction of new templates in MVC 3 and support for additional view engines such as Razor lead to overcrowding the New Project dialog in Visual Studio.</span></span> <span data-ttu-id="9f015-108">其次，必须一直客户要求提供扩展点和新的 MVC 项目向导将提供我们机会响应这些请求。</span><span class="sxs-lookup"><span data-stu-id="9f015-108">Second, customers had been asking for extensibility points and the new MVC project wizard would afford us the opportunity to respond to these requests.</span></span>

<span data-ttu-id="9f015-109">添加自定义模板时棘手的过程依赖于使用注册表来使新模板对 MVC 项目向导可见。</span><span class="sxs-lookup"><span data-stu-id="9f015-109">Adding custom templates was an arduous process that relied on using the registry to make new templates visible to the MVC project wizard.</span></span> <span data-ttu-id="9f015-110">新模板的作者必须将其包装在 MSI，确保将在安装时创建必要的注册表项。</span><span class="sxs-lookup"><span data-stu-id="9f015-110">The author of a new template had to wrap it inside an MSI to ensure that the necessary registry entries would be created at install time.</span></span> <span data-ttu-id="9f015-111">替代项是确保包含可用模板的 ZIP 文件并且没有最终用户手动创建必需的注册表项。</span><span class="sxs-lookup"><span data-stu-id="9f015-111">The alternative was to make a ZIP file containing the template available and have the end-user create the required registry entries by hand.</span></span>

<span data-ttu-id="9f015-112">前面提到的方法都不能是理想的因此，我们决定利用提供的现有基础结构的某些[VSIX](https://msdn.microsoft.com/library/ff363239.aspx)扩展要更加方便会作者，分发和安装自定义从 MVC 4 开始的 MVC 模板Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="9f015-112">Neither of the aforementioned approaches is ideal so we decided to leverage some of the existing infrastructure provided by [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) extensions to make it easier to author, distribute and install custom MVC templates starting with MVC 4 for Visual Studio 2012.</span></span> <span data-ttu-id="9f015-113">此方法提供的好处包括：</span><span class="sxs-lookup"><span data-stu-id="9f015-113">Some of the benefits provided by this approach are:</span></span>

- <span data-ttu-id="9f015-114">在 VSIX 扩展可以包含多个模板，它们支持不同的语言 （C# 和 Visual Basic） 和多个视图引擎 （ASPX 和 Razor）。</span><span class="sxs-lookup"><span data-stu-id="9f015-114">A VSIX extension can contain multiple templates that support different languages (C# and Visual Basic) and multiple view engines (ASPX and Razor).</span></span>
- <span data-ttu-id="9f015-115">在 VSIX 扩展可以面向多个 Sku 的 Visual Studio 包括 Express Sku。</span><span class="sxs-lookup"><span data-stu-id="9f015-115">A VSIX extension can target multiple SKUs of Visual Studio including Express SKUs.</span></span>
- <span data-ttu-id="9f015-116">[Visual Studio 库](https://visualstudiogallery.msdn.microsoft.com/)促进分发给广泛的受众的扩展。</span><span class="sxs-lookup"><span data-stu-id="9f015-116">The [Visual Studio Gallery](https://visualstudiogallery.msdn.microsoft.com/) facilitates distributing the extension to a wide audience.</span></span>
- <span data-ttu-id="9f015-117">使其更轻松地创作更正和更新到自定义模板，可以升级 VSIX 扩展。</span><span class="sxs-lookup"><span data-stu-id="9f015-117">VSIX extensions can be upgraded making it easier to author corrections and updates to your custom templates.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f015-118">系统必备</span><span class="sxs-lookup"><span data-stu-id="9f015-118">Prerequisites</span></span>

- <span data-ttu-id="9f015-119">用户需要熟悉创作项目模板，其中包括所需的标记 vstemplate 文件，等等。</span><span class="sxs-lookup"><span data-stu-id="9f015-119">Users need to be familiar with authoring project templates, including the required markup for vstemplate files, etc.</span></span>
- <span data-ttu-id="9f015-120">用户将需要具有 Visual Studio 专业版和更高的版本。</span><span class="sxs-lookup"><span data-stu-id="9f015-120">Users will need to have Visual Studio Professional and higher installed.</span></span> <span data-ttu-id="9f015-121">Express Sku 不支持创建 VSIX 项目。</span><span class="sxs-lookup"><span data-stu-id="9f015-121">Express SKUs do not support creating VSIX projects.</span></span>
- <span data-ttu-id="9f015-122">[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668)安装。</span><span class="sxs-lookup"><span data-stu-id="9f015-122">[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) installed.</span></span>

## <a name="example"></a><span data-ttu-id="9f015-123">示例</span><span class="sxs-lookup"><span data-stu-id="9f015-123">Example</span></span>

<span data-ttu-id="9f015-124">第一步是创建使用 C# 或 Visual Basic 的新 VSIX 项目。</span><span class="sxs-lookup"><span data-stu-id="9f015-124">The first step is to create a new VSIX project using either C# or Visual Basic.</span></span> <span data-ttu-id="9f015-125">选择**文件 > 新建项目**，然后单击**扩展性**在左窗格中，选择**VSIX 项目**。</span><span class="sxs-lookup"><span data-stu-id="9f015-125">Select **File > New Project**, then click **Extensibility** in the left pane and select the **VSIX Project**.</span></span>

![新建项目](custom-mvc-templates/_static/image1.jpg)

<span data-ttu-id="9f015-127">创建项目后，将打开 VSIX 设计器。</span><span class="sxs-lookup"><span data-stu-id="9f015-127">After the project is created, the VSIX designer will be opened.</span></span>

![项目设计器元数据](custom-mvc-templates/_static/image2.jpg)

<span data-ttu-id="9f015-129">设计器可以用于编辑某些时它们安装扩展或浏览已安装的扩展 Visual Studio 中向用户显示的扩展的常规属性 (**工具 > 扩展和更新**)。</span><span class="sxs-lookup"><span data-stu-id="9f015-129">The designer can be used to edit some of the general properties of the extension that will be shown to users when they install the extension or browse the installed extensions in Visual Studio (**Tools > Extensions and Updates**).</span></span> <span data-ttu-id="9f015-130">完成后单击的常规信息**安装目标选项卡**。</span><span class="sxs-lookup"><span data-stu-id="9f015-130">Once you have completed the general information click on the **Install Targets tab**.</span></span>

![项目设计器的安装目标](custom-mvc-templates/_static/image3.jpg)

<span data-ttu-id="9f015-132">此选项卡用于指定的 Sku 和由你的扩展支持版本的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9f015-132">This tab is used to specify the SKUs and versions of Visual Studio that are supported by your extension.</span></span> <span data-ttu-id="9f015-133">选中的复选框**的所有用户安装此 VSIX**若要启用每台计算机安装的 VSIX。</span><span class="sxs-lookup"><span data-stu-id="9f015-133">Select the checkbox for **This VSIX is installed for all users** to enable per-machine installs of the VSIX.</span></span> <span data-ttu-id="9f015-134">单击**新建**右侧添加其他 Sku 如 Web 开发人员 Express (VWD) 按钮。</span><span class="sxs-lookup"><span data-stu-id="9f015-134">Click on the **New** button on the right to add additional SKUs such as Web Developer Express (VWD).</span></span>

![添加新的安装目标](custom-mvc-templates/_static/image4.jpg)

<span data-ttu-id="9f015-136">如果你想要支持所有专业版和更高版本的 Sku （Professional、 Premium 和 Ultimate） 只需在系列中，选择最小 SKU **Microsoft.VisualStudio.Pro**。</span><span class="sxs-lookup"><span data-stu-id="9f015-136">If you intend to support all the Professional and higher SKUs (Professional, Premium and Ultimate) you only need to select the minimum SKU in the family, **Microsoft.VisualStudio.Pro**.</span></span> <span data-ttu-id="9f015-137">请记住保存所有更改完成后安装的目标。</span><span class="sxs-lookup"><span data-stu-id="9f015-137">Remember to save all your changes once you have completed the Install Targets.</span></span>

![项目设计器的安装目标](custom-mvc-templates/_static/image5.jpg)

<span data-ttu-id="9f015-139">**资产**选项卡用于将所有内容文件添加到 VSIX。</span><span class="sxs-lookup"><span data-stu-id="9f015-139">The **Assets** tab is used to add all your content files to the VSIX.</span></span> <span data-ttu-id="9f015-140">因为 MVC 需要自定义元数据将编辑而不是使用 VSIX 清单文件的原始 XML**资产**选项卡添加内容。</span><span class="sxs-lookup"><span data-stu-id="9f015-140">Since MVC requires custom metadata you will be editing the raw XML of the VSIX manifest file instead of using the **Assets** tab to add content.</span></span> <span data-ttu-id="9f015-141">首先，通过添加到 VSIX 项目的模板内容。</span><span class="sxs-lookup"><span data-stu-id="9f015-141">Start by adding the template contents to the VSIX project.</span></span> <span data-ttu-id="9f015-142">很重要的文件夹和内容的结构镜像项目的布局。</span><span class="sxs-lookup"><span data-stu-id="9f015-142">It is important that the structure of the folder and the contents mirror the layout of the project.</span></span> <span data-ttu-id="9f015-143">下面的示例包含从基本的 MVC 项目模板派生的四个项目模板。</span><span class="sxs-lookup"><span data-stu-id="9f015-143">The example below contains four project templates that were derived from the Basic MVC project template.</span></span> <span data-ttu-id="9f015-144">请确保构成你的项目模板 （ProjectTemplates 文件夹下的所有内容） 的所有文件将都添加到**内容**o u p 在 VSIX 项目文件和每个项包含**CopyToOutputDirectory**和**IncludeInVsix**设置元数据，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="9f015-144">Make sure that all the files that comprise your project template (everything underneath the ProjectTemplates folder) are added to the **Content** itemgroup in the VSIX project file and that each item contains the **CopyToOutputDirectory** and **IncludeInVsix** metadata set as shown in the example below.</span></span>

<span data-ttu-id="9f015-145">&lt;Content Include=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="9f015-145">&lt;Content Include=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span></span>

<span data-ttu-id="9f015-146">&lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;</span><span class="sxs-lookup"><span data-stu-id="9f015-146">&lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;</span></span>

<span data-ttu-id="9f015-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span><span class="sxs-lookup"><span data-stu-id="9f015-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span></span>

<span data-ttu-id="9f015-148">&lt;/Content&gt;</span><span class="sxs-lookup"><span data-stu-id="9f015-148">&lt;/Content&gt;</span></span>

<span data-ttu-id="9f015-149">否则，IDE 将尝试时生成 VSIX 并可能会看到如下错误编译模板的内容。</span><span class="sxs-lookup"><span data-stu-id="9f015-149">If not, the IDE will try to compile the contents of the template when you build the VSIX and you will likely see an error.</span></span> <span data-ttu-id="9f015-150">通常，在模板中的代码文件包含特殊[模板参数](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx)时项目模板实例化并因此不能在 IDE 中编译使用 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9f015-150">Code files in templates often contain special [template parameters](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) used by Visual Studio when the project template is instantiated and therefore cannot be compiled in the IDE.</span></span>

![“解决方案资源管理器”](custom-mvc-templates/_static/image6.jpg)

<span data-ttu-id="9f015-152">关闭 VSIX 设计器中，然后右键单击**source.extension.manifest**文件中**解决方案资源管理器**和选择**打开**选择**XML (文本） 编辑器**选项。</span><span class="sxs-lookup"><span data-stu-id="9f015-152">Close the VSIX designer, then right click on the **source.extension.manifest** file in **Solution Explorer** and select **Open With** and choose the **XML (Text) Editor** option.</span></span>

![打开与对话框](custom-mvc-templates/_static/image7.jpg)

<span data-ttu-id="9f015-154">创建**&lt;资产&gt;** 元素和添加**&lt;资产&gt;** 必须包括在 VSIX 每个文件的元素。</span><span class="sxs-lookup"><span data-stu-id="9f015-154">Create an **&lt;Assets&gt;** element and add an **&lt;Asset&gt;** element for each file that must be included in the VSIX.</span></span> <span data-ttu-id="9f015-155">**类型**每个属性**&lt;资产&gt;** 元素必须设置为**Microsoft.VisualStudio.Mvc.Template**。</span><span class="sxs-lookup"><span data-stu-id="9f015-155">The **Type** attribute of each **&lt;Asset&gt;** element must be set to **Microsoft.VisualStudio.Mvc.Template**.</span></span> <span data-ttu-id="9f015-156">这是 MVC 的项目向导理解的自定义命名空间。</span><span class="sxs-lookup"><span data-stu-id="9f015-156">This is a custom namespace that only the MVC project wizard understands.</span></span> <span data-ttu-id="9f015-157">请参阅有关其他信息的结构和清单文件布局的 VSIX 2.0 架构文档。</span><span class="sxs-lookup"><span data-stu-id="9f015-157">Refer to the VSIX 2.0 Schema documentation for additional information on the structure and layout of the manifest file.</span></span>

<span data-ttu-id="9f015-158">只需将文件添加到 VSIX 不足以使用 MVC 向导注册模板。</span><span class="sxs-lookup"><span data-stu-id="9f015-158">Just adding the files to the VSIX is not sufficient to register the templates with the MVC wizard.</span></span> <span data-ttu-id="9f015-159">你需要向 MVC 向导提供如模板名称、 描述、 受支持的视图引擎和编程语言的信息。</span><span class="sxs-lookup"><span data-stu-id="9f015-159">You need to provide information such as the template name, description, supported view engines and programming language to the MVC wizard.</span></span> <span data-ttu-id="9f015-160">与相关联的自定义特性中携带有此信息**&lt;资产&gt;** 每个元素**vstemplate**文件。</span><span class="sxs-lookup"><span data-stu-id="9f015-160">This information is carried in custom attributes associated with the **&lt;Asset&gt;** element for each **vstemplate** file.</span></span>

<span data-ttu-id="9f015-161">&lt;Asset d:VsixSubPath=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span><span class="sxs-lookup"><span data-stu-id="9f015-161">&lt;Asset d:VsixSubPath=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span></span>

<span data-ttu-id="9f015-162">Type=&quot;Microsoft.VisualStudio.Mvc.Template&quot;</span><span class="sxs-lookup"><span data-stu-id="9f015-162">Type=&quot;Microsoft.VisualStudio.Mvc.Template&quot;</span></span>

<span data-ttu-id="9f015-163">d:Source=&quot;File&quot;</span><span class="sxs-lookup"><span data-stu-id="9f015-163">d:Source=&quot;File&quot;</span></span>

<span data-ttu-id="9f015-164">Path=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span><span class="sxs-lookup"><span data-stu-id="9f015-164">Path=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span></span>

<span data-ttu-id="9f015-165">ProjectType=&quot;MVC&quot;</span><span class="sxs-lookup"><span data-stu-id="9f015-165">ProjectType=&quot;MVC&quot;</span></span>

<span data-ttu-id="9f015-166">语言 =&quot;C#&quot;</span><span class="sxs-lookup"><span data-stu-id="9f015-166">Language=&quot;C#&quot;</span></span>

<span data-ttu-id="9f015-167">ViewEngine=&quot;Aspx&quot;</span><span class="sxs-lookup"><span data-stu-id="9f015-167">ViewEngine=&quot;Aspx&quot;</span></span>

<span data-ttu-id="9f015-168">TemplateId=&quot;MyMvcApplication&quot;</span><span class="sxs-lookup"><span data-stu-id="9f015-168">TemplateId=&quot;MyMvcApplication&quot;</span></span>

<span data-ttu-id="9f015-169">标题 =&quot;自定义基本 Web 应用程序&quot;</span><span class="sxs-lookup"><span data-stu-id="9f015-169">Title=&quot;Custom Basic Web Application&quot;</span></span>

<span data-ttu-id="9f015-170">说明 =&quot;自定义模板派生自基本 MVC web 应用程序 (Razor)&quot;</span><span class="sxs-lookup"><span data-stu-id="9f015-170">Description=&quot;A custom template derived from a Basic MVC web application (Razor)&quot;</span></span>

<span data-ttu-id="9f015-171">版本 =&quot;4.0&quot;/&gt;</span><span class="sxs-lookup"><span data-stu-id="9f015-171">Version=&quot;4.0&quot;/&gt;</span></span>

<span data-ttu-id="9f015-172">下面是必须存在的自定义属性的说明：</span><span class="sxs-lookup"><span data-stu-id="9f015-172">Below is an explanation of the custom attributes that must be present:</span></span>

- <span data-ttu-id="9f015-173">**ProjectType**必须设置为 MVC。</span><span class="sxs-lookup"><span data-stu-id="9f015-173">**ProjectType** must be set to MVC.</span></span>
- <span data-ttu-id="9f015-174">**语言**指定模板支持的开发语言。</span><span class="sxs-lookup"><span data-stu-id="9f015-174">**Language** designates the development language supported by the template.</span></span> <span data-ttu-id="9f015-175">有效值为 C# 或 VB.</span><span class="sxs-lookup"><span data-stu-id="9f015-175">Valid values are either C# or VB.</span></span>
- <span data-ttu-id="9f015-176">**ViewEngine**指定支持的模板，例如 Aspx 或 Razor 视图引擎。</span><span class="sxs-lookup"><span data-stu-id="9f015-176">**ViewEngine** designates the view engine supported by the template such as Aspx or Razor.</span></span> <span data-ttu-id="9f015-177">你可以指定此字段的自定义值。</span><span class="sxs-lookup"><span data-stu-id="9f015-177">You can specify a custom value for this field.</span></span>
- <span data-ttu-id="9f015-178">**TemplateId**用于对模板进行分组。</span><span class="sxs-lookup"><span data-stu-id="9f015-178">**TemplateId** is used for grouping the templates.</span></span> <span data-ttu-id="9f015-179">如果值与匹配的现有模板 ID，它将重写使用 MVC 向导以前注册的模板。</span><span class="sxs-lookup"><span data-stu-id="9f015-179">If the value matches an existing template ID it will be override templates previously registered with the MVC wizard.</span></span>
- <span data-ttu-id="9f015-180">**标题**指定下每个项目模板 MVC 向导中显示的简短描述。</span><span class="sxs-lookup"><span data-stu-id="9f015-180">**Title** designates the short description displayed in the MVC wizard beneath each project template.</span></span>
- <span data-ttu-id="9f015-181">**说明**指定模板的更详细说明。</span><span class="sxs-lookup"><span data-stu-id="9f015-181">**Description** designates a more verbose description of the template.</span></span>

<span data-ttu-id="9f015-182">所有的文件添加到清单并保存它，你将注意到，后**资产**设计器中的选项卡将显示所有文件，但不是的自定义特性添加到**&lt;资产&gt;** 元素**vstemplate**文件。</span><span class="sxs-lookup"><span data-stu-id="9f015-182">After you have added all the files to the manifest and saved it, you will notice that the **Assets** tab in the designer will display all the files, but not the custom attributes you added to the **&lt;Asset&gt;** elements for the **vstemplate** files.</span></span>

![项目设计器资产](custom-mvc-templates/_static/image8.jpg)

<span data-ttu-id="9f015-184">所有这些剩下现在是编译 VSIX 项目并将其安装。</span><span class="sxs-lookup"><span data-stu-id="9f015-184">All that remains now is to compile the VSIX project and install it.</span></span>

<span data-ttu-id="9f015-185">请确保在计算机上的 Visual Studio 的所有实例均已都关闭的你想要测试此 VSIX 扩展。</span><span class="sxs-lookup"><span data-stu-id="9f015-185">Make sure that all instances of Visual Studio are closed on the machine where you intend to test the VSIX extension.</span></span> <span data-ttu-id="9f015-186">Visual Studio 扫描的新扩展在启动期间，因此如果 IDE 打开安装 VSIX 时你将需要重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9f015-186">Visual Studio scans for new extensions during startup, so if the IDE is open while installing a VSIX you will need to restart Visual Studio.</span></span> <span data-ttu-id="9f015-187">在资源管理器中，双击该 VSIX 文件以启动**VSIX Installer**，单击**安装**，然后启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9f015-187">In Explorer, double click on the VSIX file to launch the **VSIX Installer**, click **Install** and then launch Visual Studio.</span></span>

![VSIX 安装程序](custom-mvc-templates/_static/image9.jpg)

<span data-ttu-id="9f015-189">从菜单中，选择**工具 > 扩展和更新**若要确认你的扩展已安装。</span><span class="sxs-lookup"><span data-stu-id="9f015-189">From the menu, select **Tools > Extensions and Updates** to confirm that your extension was installed.</span></span> <span data-ttu-id="9f015-190">如果 VSIX 安装扩展的安装过程中报告任何错误，则可以查看 VSIX 安装程序日志以了解更多信息。</span><span class="sxs-lookup"><span data-stu-id="9f015-190">If the VSIX Installer reported any errors during the installation of the extension you can view the VSIX Installer log for more information.</span></span> <span data-ttu-id="9f015-191">通常在创建日志 **%temp%** 文件夹的用户安装该扩展，例如**C:\Users\Bob\AppData\Local\Temp**。</span><span class="sxs-lookup"><span data-stu-id="9f015-191">The log is usually created in the **%temp%** folder of the user that installed the extension, for example **C:\Users\Bob\AppData\Local\Temp**.</span></span>

![扩展和更新](custom-mvc-templates/_static/image10.jpg)

<span data-ttu-id="9f015-193">关闭窗口后可以创建 MVC 4 项目以查看是否在 MVC 向导中显示新模板。</span><span class="sxs-lookup"><span data-stu-id="9f015-193">After closing the window you can create an MVC 4 project to see whether your new templates are shown in the MVC wizard.</span></span>

![新的 ASP.NET MVC 4 项目](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a><span data-ttu-id="9f015-195">限制</span><span class="sxs-lookup"><span data-stu-id="9f015-195">Limitations</span></span>

1. <span data-ttu-id="9f015-196">MVC 向导不支持本地化的自定义模板。</span><span class="sxs-lookup"><span data-stu-id="9f015-196">The MVC wizard does not support localized custom templates.</span></span>
2. <span data-ttu-id="9f015-197">未能查找自定义模板，该向导将不会报告任何错误。</span><span class="sxs-lookup"><span data-stu-id="9f015-197">The wizard will not report any errors if it fails to locate custom templates.</span></span> <span data-ttu-id="9f015-198">如果任何所需的自定义属性都不存在，将只需从向导中排除该模板。</span><span class="sxs-lookup"><span data-stu-id="9f015-198">If any of the required custom attributes are absent, the template would simply be excluded from the Wizard.</span></span>
