---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 母版页 |Microsoft Docs
author: microsoft
description: 成功的网站的关键组件之一是一致的外观。 在 ASP.NET 1.x 中，开发人员用于用户控件复制常见页 elem....
ms.author: aspnetcontent
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: 631aa39c51601f1ae843079d8cd930f77b1093ab
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819210"
---
<a name="master-pages"></a>母版页
====================
by [Microsoft](https://github.com/microsoft)

> 成功的网站的关键组件之一是一致的外观。 在 ASP.NET 1.x 中，开发人员使用用户控件在 Web 应用程序之间复制常见页面元素。 虽然这的确是一个可行的解决方案，则使用用户控件也有一些缺点。 例如，用户控件的位置的更改在站点之间要求对多个页面的更改。 用户控件也不会呈现在页面上插入后的设计视图中。


成功的网站的关键组件之一是一致的外观。 在 ASP.NET 1.x 中，开发人员使用用户控件在 Web 应用程序之间复制常见页面元素。 虽然这的确是一个可行的解决方案，则使用用户控件也有一些缺点。 例如，用户控件的位置的更改在站点之间要求对多个页面的更改。 用户控件也不会呈现在页面上插入后的设计视图中。

ASP.NET 2.0 引入了 Master 页作为维护一致的外观和感觉，一种方式以及您一会儿将看到，主页面表示用户控件方法上的一个显著的改进。

## <a name="why-master-pages"></a>为什么主页？

你可能想知道为什么主页面 ASP.NET 2.0 中需要。 毕竟，网站开发人员已在使用用户控件在 ASP.NET 1.x 共享页之间的内容区域。 实际原因有多种原因用户控件都是不太理想的解决方案，用于创建一个通用布局。

用户控件实际上不定义页面布局。 相反，它们定义的布局和页面的一个部分的功能。 这两者之间的差异非常重要，因为它使用户控制解决方案的可管理性要困难得多。 例如，当你想要更改您的页面上的用户控件的位置，必须编辑用户控件显示的实际页。 如果你有仅几个页面，但在大型站点中，它很快会变得站点管理噩梦，这会精确地 ！

使用用户控件，用于定义一个通用布局的另一个缺点是在 ASP.NET 中的体系结构中取得 root 权限。 如果更改用户控件的任何公共成员，它要求您重新编译所有页面，使用用户控件。 反过来，ASP.NET 将然后 re JIT 页面首次访问。 此操作，请再次重申，生成一个非可缩放的体系结构以及较大的站点的站点管理问题。

在 ASP.NET 2.0 中的主页面可以很好地解决这些问题 （和更多）。

## <a name="how-master-pages-work"></a>如何母版页的工作原理

母版页是类似于其他页面的模板。 应在其他页面 （即菜单、 边框等） 之间共享的页面元素添加到母版页。 当新页面添加到该站点时，可以将其关联与母版页。 调用页与母版页相关联**内容页**。 默认情况下，内容页面采用从母版页的外观。 但是，当创建主页面，可以定义内容页可以将其自己的内容替换为页面的部分。 这些部分都是使用 ASP.NET 2.0; 中引入的新控件定义**ContentPlaceHolder**控件。

主页面可以包含任意数量的 ContentPlaceHolder 控件 （或根本未。）在内容页上从 ContentPlaceHolder 控件内容的显示的内部**内容**控件、 ASP.NET 2.0 中的另一个新控件。 默认情况下，内容控件的内容页是空的以便可以提供自己的内容。 如果你想要使用内容控件在母版页中的内容，则可以执行将看到更高版本在此模块中。 内容控件映射到内容控件的 ContentPlaceHolderID 特性通过 ContentPlaceHolder 控件。 以下映射代码到 ContentPlaceHolder 控件在母版页上调用 mainBody 内容控件。

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> 您将经常听人们描述为基类的其他页面的母版页。 这是实际不适用。 母版页和内容页之间的关系不是继承。


**图 1**显示主控页和关联的内容页中 Visual Studio 2005 的显示方式。 可以看到在母版页和相应的 ContentPlaceHolder 控件内容的内容页中的控件。 请注意，外部 ContentPlaceHolder 的主页面内容可见，但在内容页中灰显。 仅将 ContentPlaceHolder 内的内容可以通过内容页所取代。 所有其他来自母版页的内容是不可变。


![母版页和其关联的内容页](master-pages/_static/image1.jpg)

**图 1**： 主控页和其关联的内容页


## <a name="creating-a-master-page"></a>创建主页面

若要创建新的主页面：

1. 打开 Visual Studio 2005 并创建新的 Web 站点。
2. 单击文件，新、 文件。
3. 从添加新项对话框中选择主文件，如中所示**图 2**。
4. 单击添加。


![创建一个新的主页面](master-pages/_static/image2.jpg)

**图 2**： 创建新的主页面


请注意，文件扩展名为母版页<em>.master</em>。 这是主页面与普通页不同的方法之一。 其他主要区别是替代@Page指令，母版页包含@Master指令。 切换到源视图的主页面，刚刚创建并查看代码。

默认情况下，新的主页面将具有一个 ContentPlaceHolder 控件。 在大多数情况下，它更有意义可以首先创建常见的页面元素然后插入 ContentPlaceHolder 控件在需要自定义内容的情况。 在这些情况下，开发人员将想要删除默认 ContentPlaceHolder 控件并插入新的开发页。 ContentPlaceHolder 控件不能调整大小，它们显示调整大小控点的情况。 自动根据它包含有一个例外; 的内容的 ContentPlaceHolder 控件大小如果如表格单元格将 ContentPlaceHolder 控件在是块元素内部，它将根据元素的大小调整大小。

## <a name="lab-1-working-with-master-pages"></a>实验室 1 使用母版页

在此实验中，将创建新的主页面，并定义三个 ContentPlaceHolder 控件。 然后，将创建新的内容页面，并替换为从至少其中一个 ContentPlaceHolder 控件的内容。

1. 创建主页面，并插入 ContentPlaceHolder 控件。 

    1. 创建新的主页面，如上文所述。
    2. 删除默认 ContentPlaceHolder 控件。
    3. 通过单击该控件的阴影上边框选择 ContentPlaceHolder 控件，然后按你键盘上的 DEL 键中删除它。
    4. 插入新表使用*标头和端*图 3 中所示的模板。 将宽度和高度更改为 90%，以使整个表设计器中可见。


![](master-pages/_static/image3.jpg)

**图 3**


1. 将光标置于表的每个单元格并设置*valign*属性设置为*顶部*。
2. 从工具箱中的表 （的标头单元格。） 的顶部单元插入 ContentPlaceHolder 控件
3. 当插入此 ContentPlaceHolder 控件时，您会注意到行的高度将几乎整个页面占用，如图 4 中所示。 不能胜，此时。


![作为 ContentPlaceHolder 相同单元中是空的空间](master-pages/_static/image1.gif)

**图 4**: ContentPlaceHolder 格中是空的空间


1. 将 ContentPlaceHolder 控件放在其他两个单元格。 一旦已插入其他 ContentPlaceHolder 控件，表格单元格的大小应为按预期的方式。 页面现在应如下所示中显示的页面**图 5**。


![与所有 ContentPlaceHolder 控件 Master。 请注意，标头单元格的单元格高度现在它应该是什么](master-pages/_static/image2.gif)

**图 5**： 与所有 ContentPlaceHolder 控件的母版。 请注意，标头单元格的单元格高度现在它应该是什么


1. 每三个 ContentPlaceHolder 控件中输入所选的某些文本。
2. 将为 exercise1.master 母版页。
3. 创建新的 Web 窗体并将其与 exercise1.master 母版页相关联。
4. 选择新建文件、 文件在 Visual Studio 2005 中。
5. 选择**Web 窗体**在添加新项对话框。
6. 请确保选中选择母版页复选框，如图 6 中所示。


![添加一个新的内容页](master-pages/_static/image3.gif)

**图 6**： 添加新的内容页面


1. 单击添加。
2. 选择 exercise1.master 在中，选择一个母版页对话框图 7 中所示。
3. 单击确定以添加新的内容页面。

新的内容页出现在 Visual Studio 为每个 ContentPlaceHolder 控件在母版页上的其中一个内容控件。 默认情况下，内容控件是空的以便可以添加自己的内容。 如果您可能喜欢它们使用 ContentPlaceHolder 控件在母版页上的内容，只需单击智能标记符号 （在右上角的控件的小黑色箭头），然后选择*默认为母版内容*从智能标记，如中所示**图 8**。 执行此操作时，菜单项将变为*创建自定义内容*。 此时，单击从母版页允许您定义该特定的内容控件的自定义内容中删除内容。


![设置默认为母版页的页面内容的内容控件](master-pages/_static/image4.gif)

**图 7**： 将内容控件设置为默认为母版页的页面内容


## <a name="connecting-master-page-and-content-pages"></a>连接母版页和内容页面

母版页和内容页之间的关联可以配置在四种不同方法之一：

- <strong>MasterPageFile</strong>属性的@Page指令
- 设置**Page.MasterPageFile**在代码中的属性。
- **&lt;页面&gt;** 应用程序配置文件 (web.config 应用程序的根文件夹中) 中的元素
- **&lt;页面&gt;** 子文件夹配置文件 (web.config 的子文件夹中) 中的元素

## <a name="masterpagefile-attribute"></a>MasterPageFile 特性

MasterPageFile 属性轻松应用于特定的 ASP.NET 页面的母版页。 它也是用来检查时应用主页面的方法**选择母版页**复选框为您在练习 1 中所做。

## <a name="setting-pagemasterpagefile-in-code"></a>在代码中设置 Page.MasterPageFile

通过在代码中设置的 MasterPageFile 属性，可以将特定母版页应用到你在运行时的内容。 这是你可能需要应用基于用户角色或某些其他条件的特定主页面非常有用。 MasterPageFile 属性必须设置 PreInit 方法中。 如果将其设置 PreInit 方法后，将引发 InvalidOperationException。 在其设置此属性页还必须具有一个内容控件为顶级控件的页。 否则将引发 HttpException MasterPageFile 属性设置时。

## <a name="using-the-ltpagesgt-element"></a>使用&lt;页面&gt;元素

通过将 masterPageFile 属性设置配置页面母版页&lt;页面&gt;web.config 文件的元素。 使用此方法时，请注意应用程序结构中较低级别的 web.config 文件来覆盖此设置。 在中设置任何 MasterPageFile 属性@Page指令还会覆盖此设置。 使用&lt;pages&gt;元素，可以轻松地创建<em>master</em>可重写如有必要在特定文件夹或文件中的母版页。

## <a name="properties-in-master-pages"></a>母版页中的属性

母版页上可以只需使这些属性中的母版页的公共公开属性。 例如，下面的代码定义一个名为 SomeProperty 属性：

[!code-csharp[Main](master-pages/samples/sample2.cs)]

若要从内容页访问 SomeProperty 属性，您将需要使用主属性如下所示：

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>嵌套母版页

母版页是确保在大型 Web 应用程序的常见的外观和感觉的完美解决方案。 但是，不常见具有大型网站共享一个公共接口的某些部分，而其他部分共享使用不同的接口。 若要解决这种需求，多个主页面是一个完美的解决方案。 但是，仍然无法解决这一事实，大型应用程序可能具有在所有页面之间共享某些组件 （如菜单，例如） 和仅在站点的某些部分之间共享其他组件。 对于该类型的情况下，嵌套的母版页可以很好地满足需要。 如您所见，普通的主页面组成一个母版页和内容页。 在嵌套的母版页的情况下，有两个主页面; 例如：父 master 和子 master。 子主页面也是内容页面，并且其主父母版页。

下面是典型的主页面的代码：

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

在嵌套母版页方案中，这将是父 master。 另一个主页面将作为其主页面，使用此页，该代码将如下所示：

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

请注意，在此方案中，子 master 还父级主页的内容页面。 所有子母版页的内容显示在内容控件，可从父 ContentPlaceHolder 控件获取其内容。

> [!NOTE]
> 设计器支持不可用于嵌套的母版页。 当你要开发使用嵌套的母版时，需要使用源视图。


此视频演示了如何使用嵌套的母版页。


![](master-pages/_static/image1.png)


[打开的全屏视频](master-pages/_static/nested1.wmv)


![选择母版页](master-pages/_static/image4.jpg)

**图 8**： 选择母版页
