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
<a name="custom-mvc-template"></a>自定义 MVC 模板
====================
通过[3。jacques Eloff](https://github.com/joeloff)

MVC 3 Tools Update for Visual Studio 2010 的版本引入了用于 MVC 项目的单独的项目向导。 更改主要依靠两个因素。 首先，在 MVC 3 和附加视图引擎，如 Razor 的支持中的新模板的引入导致 overcrowding Visual Studio 中的新建项目对话框。 其次，客户必须一直期盼的扩展点和新的 MVC 项目向导将提供了我们对这些请求作出响应。

添加自定义模板是依赖于使用注册表来使新模板对 MVC 项目向导可见的艰辛旅程。 新模板的作者必须将其封装在 MSI 来确保将在安装时创建必要的注册表项。 另一个方法是使包含可用模板的 ZIP 文件，并让最终用户手动创建必需的注册表项。

前面提到的方法都不是理想选择，因此我们决定是使用提供的现有基础结构[VSIX](https://msdn.microsoft.com/library/ff363239.aspx)扩展以更简单地将作者、 分发和安装自定义 MVC 模板从 MVC 4 开始适用于 Visual Studio 2012。 这种方法提供的好处包括：

- VSIX 扩展包含支持不同的语言 （C# 和 Visual Basic） 的多个模板和多个视图引擎 （ASPX 和 Razor）。
- VSIX 扩展可以面向多个 Sku 的 Visual Studio 包括速成版 Sku。
- [Visual Studio 库](https://visualstudiogallery.msdn.microsoft.com/)便于分发给广泛的受众扩展。
- VSIX 扩展可以更轻松地创作的更正和对自定义模板的更新进行升级。

## <a name="prerequisites"></a>系统必备

- 用户需要熟悉创作项目模板，其中包括 vstemplate 文件等所需的标记。
- 用户将需要具有 Visual Studio Professional 和更高版本。 Express Sku 不支持创建 VSIX 项目。
- [Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668)安装。

## <a name="example"></a>示例

第一步是创建使用 C# 或 Visual Basic 的新 VSIX 项目。 选择**文件 > 新建项目**，然后单击**扩展性**在左窗格中，选择**VSIX 项目**。

![新建项目](custom-mvc-templates/_static/image1.jpg)

创建项目后，将打开 VSIX 设计器。

![项目设计器元数据](custom-mvc-templates/_static/image2.jpg)

在设计器可用于编辑某些安装扩展或浏览 Visual Studio 中已安装的扩展时，将向用户显示的扩展的常规属性 (**工具 > 扩展和更新**)。 完成后的常规信息，请单击**安装目标选项卡**。

![项目设计器的安装目标](custom-mvc-templates/_static/image3.jpg)

此选项卡用于指定 Sku 和版本的 Visual Studio 支持的扩展。 选中的复选框**的所有用户安装此 VSIX**若要启用每台计算机安装的 VSIX。 单击**新建**右侧添加其他 Sku 等 Web Developer Express (VWD) 按钮。

![添加新的安装目标](custom-mvc-templates/_static/image4.jpg)

如果您打算支持的所有专业和更高版本的 Sku （Professional、 Premium 和 Ultimate） 只需在系列中选择的最小 SKU **Microsoft.VisualStudio.Pro**。 请记住保存所有更改完成后安装目标。

![项目设计器的安装目标](custom-mvc-templates/_static/image5.jpg)

**资产**选项卡用于将所有内容文件添加到 VSIX。 由于 MVC 需要自定义元数据，因此将编辑而不是使用 VSIX 清单文件的原始 XML**资产**选项卡添加内容。 首先将模板内容添加到 VSIX 项目。 非常重要的文件夹及其内容的结构，镜像的项目布局。 下面的示例包含四个项目模板从基本的 MVC 项目模板派生的。 请确保包含你的项目模板 （ProjectTemplates 文件夹下的所有内容） 的所有文件都添加到**内容**itemgroup 在 VSIX 项目文件和每个项包含**CopyToOutputDirectory**并**IncludeInVsix**设置元数据，如下面的示例中所示。

&lt;Content Include=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;

&lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;

&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;

&lt;/Content&gt;

否则，IDE 将尝试生成 VSIX 和你可能会看到错误时进行编译模板的内容。 在模板中的代码文件通常包含特殊[模板参数](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx)Visual Studio 项目模板实例化并因此不能在 IDE 中编译时使用。

![“解决方案资源管理器”](custom-mvc-templates/_static/image6.jpg)

关闭 VSIX 设计器中，然后右键单击**source.extension.manifest**中的文件**解决方案资源管理器**，然后选择**打开**，然后选择**XML (文本） 编辑器**选项。

![打开对话框](custom-mvc-templates/_static/image7.jpg)

创建**&lt;资产&gt;** 元素，并添加**&lt;资产&gt;** 元素必须包括在 VSIX 中的每个文件。 **类型**属性的每个**&lt;资产&gt;** 元素必须设置为**Microsoft.VisualStudio.Mvc.Template**。 这是 MVC 的项目向导能够理解的自定义命名空间。 请参阅有关其他信息的结构和清单文件的布局 VSIX 2.0 架构文档。

只需将文件添加到 VSIX 不足以使用 MVC 向导注册模板。 您需要向 MVC 向导提供模板名称、 说明、 受支持的视图引擎和编程语言等信息。 此信息与相关联的自定义属性中携带**&lt;资产&gt;** 每个元素**vstemplate**文件。

&lt;Asset d:VsixSubPath=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;

Type=&quot;Microsoft.VisualStudio.Mvc.Template&quot;

d:Source=&quot;File&quot;

Path=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;

ProjectType=&quot;MVC&quot;

语言 =&quot;C#&quot;

ViewEngine=&quot;Aspx&quot;

TemplateId=&quot;MyMvcApplication&quot;

Title =&quot;自定义基本 Web 应用程序&quot;

说明 =&quot;自定义模板派生自基本 MVC web 应用程序 (Razor)&quot;

版本 =&quot;4.0&quot;/&gt;

下面是必须存在的自定义特性的说明：

- **ProjectType**必须设置为 MVC。
- **语言**指定模板支持的开发语言。 有效值为 C# 或 vb。
- **ViewEngine**指定如 Aspx 或 Razor 模板还支持在视图引擎。 可以指定此字段的自定义值。
- **TemplateId**用于对模板进行分组。 如果值匹配的现有模板 ID，它将重写以前注册到 MVC 向导的模板。
- **标题**指定显示在 MVC 向导下每个项目模板的简短描述。
- **说明**指定模板的更详细说明。

所有文件都添加到清单并保存它，您将注意到，之后**资产**设计器中的选项卡将显示所有文件，但未自定义属性都添加到**&lt;资产&gt;** 个元素**vstemplate**文件。

![项目设计器资产](custom-mvc-templates/_static/image8.jpg)

所有的就现在是编译 VSIX 项目并将其安装。

请确保 Visual Studio 的所有实例已都关闭的计算机上你想要测试此 VSIX 扩展。 Visual Studio 会扫描新的扩展在启动期间，因此如果 IDE 打开安装 VSIX 时将需要重新启动 Visual Studio。 在资源管理器中，双击 VSIX 文件，启动**VSIX 安装程序**，单击**安装**，然后启动 Visual Studio。

![VSIX 安装程序](custom-mvc-templates/_static/image9.jpg)

从菜单中选择**工具 > 扩展和更新**若要确认是否已安装扩展。 如果在扩展安装期间，VSIX 安装程序报告任何错误可以查看 VSIX 安装程序日志以了解更多信息。 通常在创建该日志 **%temp%** 安装扩展，例如在用户文件夹**C:\Users\Bob\AppData\Local\Temp**。

![扩展和更新](custom-mvc-templates/_static/image10.jpg)

关闭窗口后可以创建一个 MVC 4 项目以查看是否在 MVC 向导中显示新模板。

![新的 ASP.NET MVC 4 项目](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a>限制

1. MVC 向导不支持本地化的自定义模板。
2. 如果无法找到自定义模板，该向导将不会报告任何错误。 如果任何所需的自定义属性不存在，将只需从向导中排除该模板。
