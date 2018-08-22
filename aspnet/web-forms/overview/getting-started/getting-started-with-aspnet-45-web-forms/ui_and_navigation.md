---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
title: 用户界面和导航 |Microsoft Docs
author: Erikre
description: 本教程系列将指导您学习生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 5c76891d-e515-4885-b576-76bd2c494efe
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
msc.type: authoredcontent
ms.openlocfilehash: 55c659cbaf48dbb02dc34e013242443d4fbd8845
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830068"
---
<a name="ui-and-navigation"></a>用户界面和导航
====================
通过[Erik Reitan](https://github.com/Erikre)

[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 此教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。 Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)可随附于本系列教程。


在本教程中，您将修改默认的 Web 应用程序，以支持功能的 Wingtip Toys 应用商店前端应用程序的 UI。 此外，您将添加简单和数据绑定导航。 本教程基于上一教程"创建数据访问层"，而是 Wingtip Toys 教程系列的一部分。

## <a name="what-youll-learn"></a>你将学习：

- 如何更改 UI 以支持 Wingtip Toys 应用商店前端应用程序的功能。
- 如何配置要包括页面导航的 HTML5 元素。
- 如何创建数据驱动的控件，以导航到特定产品数据。
- 如何显示使用 Entity Framework Code First 创建数据库中的数据。

ASP.NET Web 窗体允许您创建的 Web 应用程序的动态内容。 每个 ASP.NET 网页创建方式类似于静态 HTML Web 页面 （不包括基于服务器的处理的页），但 ASP.NET 网页包括 ASP.NET 识别并处理生成的 HTML 页在运行时的额外元素。

与静态 HTML 页面 (*.htm*或 *.html*文件)，服务器担当`Web`通过读取文件并将其作为发送的请求-在浏览器。 与此相反，当有人请求 ASP.NET 网页 (*.aspx*文件)，该页面作为程序运行在 Web 服务器上。 运行页面时，它可以执行需要你的网站，其中包括计算值、 读取或写入数据库的信息，或调用其他程序的任何任务。 作为其输出页面动态生成标记 （例如 HTML 中的元素），并将此动态输出发送到浏览器。

## <a name="modifying-the-ui"></a>修改 UI

您将通过修改继续本教程系列*Default.aspx*页。 您将修改用于创建应用程序的默认模板已建立的 UI。 创建任何 Web 窗体应用程序时，是典型的修改需要执行的操作类型。 将为此，将更改标题，替换某些内容，并删除不需要的默认的内容。

1. 打开或切换到*Default.aspx*页。
2. 如果在显示的页面**设计**视图中，切换到**源**视图。
3. 在页面顶部`@Page`指令，更改`Title`中下面的黄色突出显示"Welcome"属性。 

    [!code-aspx[Main](ui_and_navigation/samples/sample1.aspx?highlight=1)]
4. 同样，在*Default.aspx*页上，将替换默认的内容中包含的所有`<asp:Content>`标记，以便标记显示为如下。 

    [!code-aspx[Main](ui_and_navigation/samples/sample2.aspx)]
5. 保存*Default.aspx*页上通过选择**保存 Default.aspx**从**文件**菜单。

   得到*Default.aspx*页将出现，如下所示： 

[!code-aspx[Main](ui_and_navigation/samples/sample3.aspx)]

在示例中，设置`Title`属性的`@Page`指令。 当在浏览器中，服务器代码中显示 HTML`<%: Page.Title %>`解析为中包含的内容`Title`属性。

此示例页包含构成 ASP.NET 网页的基本元素。 页包含静态文本，如你可能在 HTML 页中，以及特定于 ASP.NET 的元素。 中包含的内容*Default.aspx*页将与主页面内容，这将在本教程的后面进行说明集成。

### <a name="page-directive"></a>@Page 指令

ASP.NET Web 窗体通常包含允许您指定的页的页属性和配置信息的指令。 指令被用作 ASP.NET 说明有关如何为进程页上，但它们将不呈现为发送到浏览器的标记的一部分。

最常使用的指令是`@Page`指令，允许您指定的页上，其中包括多个配置选项：

1. 编程语言在页中，如 C# 代码的服务器。
2. 该页是否是通过直接在页中，这称为单文件页，服务器代码页，或者它是否在单独的类文件，称为代码隐藏页中使用代码页。
3. 是否该页具有关联的主页面，因此会被视为内容页。
4. 调试和跟踪选项。

如果不包括`@Page`指令在页中，或如果该指令不包括特定的设置，将设置继承自*Web.config*配置文件或从*Machine.config*配置文件。 *Machine.config*文件提供了其他配置设置应用于所有应用程序的计算机上运行。

> [!NOTE] 
> 
> *Machine.config*还提供了有关所有可能的配置设置的详细信息。


### <a name="web-server-controls"></a>Web 服务器控件

在大多数 ASP.NET Web 窗体应用程序，您将添加允许用户与页面，例如按钮、 文本框、 列表等交互的控件。 这些 Web 服务器控件都类似于 HTML 按钮和输入的元素。 但是，它们会处理在服务器上，您可以使用服务器代码来设置其属性。 这些控件也引发了可以在服务器代码中处理的事件。

服务器控件使用 ASP.NET 识别运行页面时的特殊语法。 ASP.NET 服务器控件的标记名称开头`asp:`前缀。 这使 ASP.NET 可以识别和处理这些服务器控件。 前缀可能不同，如果该控件不是.NET Framework 的一部分。 除了`asp:`前缀，ASP.NET 服务器控件还包括`runat="server"`属性和一个`ID`可用于引用在服务器代码中的控件。

页运行时，ASP.NET 标识的服务器控件，并运行的代码，这些控件与相关联。 许多控件将呈现某些 HTML 或其他标记在页面的浏览器中显示时。

### <a name="server-code"></a>服务器代码

大多数 ASP.NET Web 窗体应用程序包含在页处理时，在服务器运行的代码。 如上所述，服务器代码可以用于执行各种操作，如将数据添加到 ListView 控件。 ASP.NET 支持多种语言包括 C#、 Visual Basic、 J# 和其他服务器上运行。

ASP.NET 支持用于编写用于网页的服务器代码的两个模型。 在单个文件模型中，页的代码是在脚本元素的开始标记，其中包括`runat="server"`属性。 或者，您可以在单独的类文件，称为代码隐藏模型中创建页的代码。 在这种情况下，ASP.NET Web 窗体页通常包含无服务器代码。 相反，`@Page`指令中包含链接的信息 *.aspx*与其关联的代码隐藏文件的页。

`CodeBehind`属性中包含`@Page`指令指定单独的类文件的名称和`Inherits`属性指定对应于页的代码隐藏文件中的类的名称。

### <a name="updating-the-master-page"></a>更新母版页

在 ASP.NET Web 窗体，母版页允许你在应用程序中创建一致的页面布局。 使用单个母版页定义应用程序中的外观和感觉和所需的所有页面 （或一组页） 的标准行为。 然后可以创建包含要显示，如上文所述的内容的各个内容页。 当用户请求内容的页面时，ASP.NET 会将它们合并与母版页以生成将主控页的布局与内容页中的内容相结合的输出。

新的站点需要要显示每一页上的一个徽标。 若要添加此徽标，您可以修改在母版页上的 HTML。

1. 在中**解决方案资源管理器**，找到并打开**Site.Master**页。
2. 如果在页处于**设计**视图中，切换到**源**视图。
3. 更新通过母版页**修改或添加**以黄色突出显示的标记： 

    [!code-aspx[Main](ui_and_navigation/samples/sample4.aspx?highlight=9,49,76-81,87)]

此 HTML 将显示名为图像*logo.jpg*从*映像*稍后将添加的 Web 应用程序的文件夹。 当使用母版页的页面在浏览器中显示时，将显示徽标。 如果用户单击在徽标上时，用户将导航回*Default.aspx*页。 HTML 定位点标记`<a>`包装映像服务器控件，并允许将图像作为链接的一部分。 `href`属性 (attribute) 的定位点标记指定的根"`~/`"作为链接位置的 Web 站点。 默认情况下*Default.aspx*用户导航到网站的根目录，会显示页面。 **图像**`<asp:Image>`服务器控件包括添加属性，如`BorderStyle`，呈现为 HTML 时浏览器中显示的。

### <a name="master-pages"></a>母版页

主页面是 ASP.NET 与扩展.master 文件 (例如， *Site.Master*) 具有预定义布局可以包括静态文本、 HTML 元素和服务器控件。 主页面由一种特殊`@Master`指令将替换`@Page`用于普通的指令 *.aspx*页。

除了`@Master`指令，主页面还包含的所有顶级 HTML 元素的页上，例如`html`， `head`，和`form`。 例如，在前面添加主页面上，则使用对应的 HTML`table`布局，`img`公司徽标、 静态文本和服务器控件能够处理你的站点的公共成员身份的元素。 作为到母版页的一部分，可以使用任何 HTML 和 ASP.NET 的任何元素。

除了静态文本和控件将显示所有页，主页面还包括一个或多个**ContentPlaceHolder**控件。 这些占位符控件定义会显示可更换部件内容的区域。 反过来，可更换部件内容中定义内容页面，如*Default.aspx*，并使用**内容**服务器控件。

#### <a name="adding-image-files"></a>添加图像文件

徽标图像引用更高版本，以及所有产品映像，必须添加到 Web 应用程序，以便在浏览器中显示该项目时，可以看到它们。

#### <a name="download-from-msdn-samples-site"></a>从 MSDN 示例站点下载：

[开始使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)

此下载文件包括中的资源*WingtipToys 资产*用于创建示例应用程序的文件夹。

1. 如果尚未这样做，下载压缩的示例文件从 MSDN 示例网站使用上面的链接。
2. 下载完成后，打开.zip 文件，并将内容复制到你的计算机上的本地文件夹。
3. 找到并打开*WingtipToys 资产*文件夹。
4. 通过拖放，将复制*目录*从您的本地文件夹中的 Web 应用程序项目的根文件夹**解决方案资源管理器**的 Visual Studio。 

    ![UI 和导航-复制文件](ui_and_navigation/_static/image1.png)
5. 接下来，创建名为的新文件夹*映像*通过右击**WingtipToys**项目**解决方案资源管理器**，然后选择**添加** - &gt; **新文件夹**。
6. 复制*logo.jpg*文件从*WingtipToys 资产*文件夹中的**文件资源管理器**到*映像*Web 应用程序文件夹项目中**解决方案资源管理器**的 Visual Studio。
7. 单击**显示所有文件**顶部的选项**解决方案资源管理器**要更新的文件列表，如果看不到新文件。  
  
    **解决方案资源管理器**现在显示已更新的项目文件。 

    ![用户界面和导航的解决方案资源管理器](ui_and_navigation/_static/image2.png)

### <a name="adding-pages"></a>添加页

添加导航到之前的 Web 应用程序，你将首先添加将导航到的两个新页。 稍后在本系列教程中将这些新页上显示产品和产品详细信息。

1. 在中**解决方案资源管理器**，右键单击**WingtipToys**，单击**添加**，然后单击**新项**。   
 随即出现“添加新项”对话框。
2. 选择**Visual C#**  - &gt; **Web**在左侧的模板组。 然后，选择**包含母版页的 Web 窗体**从中间列表并将其命名*ProductList.aspx*。 

    ![用户界面和导航的添加新项对话框](ui_and_navigation/_static/image3.png)
3. 选择**Site.Master**附加到新创建的母版页 *.aspx*页。 

    ![UI 和导航-选择母版页](ui_and_navigation/_static/image4.png)
4. 添加名为的其他页*ProductDetails.aspx*按照上述相同步骤。

### <a name="updating-bootstrap"></a>正在更新 Bootstrap

使用 Visual Studio 2013 项目模板[Bootstrap](http://getbootstrap.com/)，创建的 Twitter 的布局和主题框架。 Bootstrap 使用 CSS3 提供响应式设计，这意味着布局可以动态地适应不同的浏览器窗口大小。 Bootstrap 的主题功能还可用于轻松地影响应用程序的外观和行为的更改。 默认情况下，Visual Studio 2013 中的 ASP.NET Web 应用程序模板包括 Bootstrap 作为 NuGet 包。

在本教程中，您将通过替换 Bootstrap CSS 文件来更改 Wingtip Toys 应用程序的外观和感觉。

1. 在中**解决方案资源管理器**，打开*内容*文件夹。
2. 右键单击*bootstrap.css*文件，并为其重命名*bootstrap original.css*。
3. 重命名*bootstrap.min.css*到*bootstrap original.min.css*。
4. 在中**解决方案资源管理器**，右键单击*内容*文件夹，然后选择**在文件资源管理器中打开文件夹**。  
   将显示在文件资源管理器。 会将下载的 bootstrap CSS 文件保存到此位置。
5. 在浏览器中，转到[ https://bootswatch.com/3/ ](https://bootswatch.com/3/)。
6. 滚动浏览器窗口，直到看到 Cerulean 主题。 

    ![UI 和导航-Cerulean 主题](ui_and_navigation/_static/image5.png)
7. 同时下载*bootstrap.css*文件并*bootstrap.min.css*文件发送到*内容*文件夹。 使用中显示的内容文件夹的路径**文件资源管理器**以前打开的窗口。
8. 在中**Visual Studio**顶部**解决方案资源管理器**，选择**显示所有文件**选项以显示新文件的内容文件夹中。 

    ![用户界面和导航的解决方案资源管理器](ui_and_navigation/_static/image6.png)

   您将看到两个新 CSS 文件中的**内容**文件夹中，但请注意，每个文件名称旁边的图标将灰显。这意味着，该文件尚未尚未添加到项目。
9. 右键单击*bootstrap.css*并*bootstrap.min.css*文件，然后选择**包括在项目**。   
   本教程中稍后运行 Wingtip Toys 应用程序时，将显示新的用户界面。

> [!NOTE] 
> 
> ASP.NET Web 应用程序模板使用*Bundle.config*项目来存储 Bootstrap CSS 文件的路径的根目录下的文件。


### <a name="modifying-the-default-navigation"></a>修改默认导航

可以通过更改中的无序的导航列表元素修改应用程序中每一页的默认导航*Site.Master*页。

1. 在中**解决方案资源管理器**，找到并打开*Site.Master*页。
2. 添加到未排序列表如下所示的黄色突出显示的其他导航链接：   

    [!code-html[Main](ui_and_navigation/samples/sample5.html?highlight=5)]

正如您所看到上述 HTML 中，修改每个行项`<li>`包含一个定位点标记`<a>`的链接`href`属性。 每个`href`指向 Web 应用程序中的页。 在浏览器中，当用户单击这些链接之一 (如**产品**)，它们将导航到页面中包含`href`(如**ProductList.aspx**)。 本教程结束时，将运行该应用程序。

> [!NOTE] 
> 
> 波形符 (`~`) 字符用于指定`href`在项目的根目录开始的路径。


### <a name="adding-a-data-control-to-display-navigation-data"></a>添加数据控件以显示导航数据

接下来，你将添加一个控件以显示所有数据库中的类别。 每个类别将充当一个指向*ProductList.aspx*页。 当用户单击浏览器中的类别链接时，它们将导航到产品页，查看仅与所选类别关联的产品。

将使用**ListView**控件来显示数据库中包含的所有类别。 若要添加**ListView**到母版页的控件：

1. 在中*Site.Master*页上，添加以下突出显示`<div>`元素**后**`<div>`元素，其中包含`id="TitleContent"`前面添加：  

    [!code-aspx[Main](ui_and_navigation/samples/sample6.aspx?highlight=7-21)]

此代码将显示数据库中的所有类别。 **ListView**控件显示为链接文本的每个类别名称和包含的链接*ProductList.aspx*带有查询字符串值包含页`ID`的类别。 通过设置`ItemType`中的属性**ListView**控件，数据绑定表达式`Item`中有可用`ItemTemplate`节点和控件将成为强类型化。 可以选择的详细信息`Item`对象使用 IntelliSense，例如，指定`CategoryName`。 此代码包含在容器内`<%#: %>`标记数据绑定表达式。 通过将 （:） 添加到末尾`<%#`前缀，数据绑定表达式的结果是 HTML 编码。 如果结果为 HTML 编码，您的应用程序更有效抵御跨站点脚本注入 (XSS) 和 HTML 注入攻击。

> [!NOTE] 
> 
> **提示**
> 
> 时通过键入在开发过程中添加代码，您可以确定对象的有效成员找到因为强类型数据控件显示可用成员基于智能感知。 IntelliSense 提供了你键入代码，例如属性、 方法和对象选择相应上下文的代码。


在下一步，您将实现`GetCategories`方法来检索数据。

### <a name="linking-the-data-control-to-the-database"></a>将数据控件链接到数据库

您可以在数据控件中显示数据之前，需要将数据控件链接到该数据库。 若要使该链接，可以修改的代码隐藏*Site.Master.cs*文件。

1. 在中**解决方案资源管理器**，右键单击*Site.Master*页，然后单击**查看代码**。 *Site.Master.cs*在编辑器中打开文件。
2. 附近的开头*Site.Master.cs*文件中，添加两个其他命名空间，以便所有包括的命名空间显示，如下所示：  

    [!code-csharp[Main](ui_and_navigation/samples/sample7.cs?highlight=8-9)]
3. 添加突出显示`GetCategories`方法之后`Page_Load`事件处理程序，如下所示：  

    [!code-csharp[Main](ui_and_navigation/samples/sample8.cs?highlight=6-11)]

在浏览器中加载任何使用母版页的页面时执行上面的代码。 `ListView`在本教程前面添加的控件 (名为"categoryList") 使用模型绑定选择数据。 中的标记`ListView`设置控件的控件`SelectMethod`属性设置为`GetCategories`上面所示的方法。 `ListView`控制调用`GetCategories`方法在适当的时间在页生命周期并自动将绑定返回的数据。 您将了解有关下一步的教程中将数据绑定的详细信息。

### <a name="running-the-application-and-creating-the-database"></a>运行应用程序和创建数据库

之前在本系列教程创建一个初始值设定项类 （名为"ProductDatabaseInitializer"） 和指定在此类*global.asax.cs*文件。 实体框架将生成数据库时应用程序运行第一次，因为`Application_Start`方法中包含*global.asax.cs*文件将调用初始值设定项类。 初始值设定项类将使用的模型类 (`Category`和`Product`) 前面在本教程系列中创建的数据库中添加。

1. 在中**解决方案资源管理器**，右键单击*Default.aspx*页，然后选择**设为起始页**。
2. 在 Visual Studio 中按**F5**。   
 需要一些时间来完成所有设置在首次运行此过程。   
    ![用户界面和导航的浏览器 Windows](ui_and_navigation/_static/image7.png)  
 在运行该应用程序时，将编译该应用程序和数据库名为*wingtiptoys.mdf*将在其中创建*应用\_数据*文件夹。 在浏览器中，将看到类别导航菜单。 此菜单是通过从数据库检索类别生成的。 在下一步的教程中，您将实现导航。
3. 关闭浏览器会停止运行的应用程序。

### <a name="reviewing-the-database"></a>查看数据库

打开*Web.config*文件，并查看连接字符串部分。 你可以看到`AttachDbFilename`连接字符串中的值指向`DataDirectory`为 Web 应用程序项目。 该值`|DataDirectory|`是保留的值，表示*应用程序\_数据*项目文件夹中的。 此文件夹是从实体类创建的数据库所在的位置。

[!code-xml[Main](ui_and_navigation/samples/sample9.xml)]

> [!NOTE] 
> 
> 如果*应用程序\_数据*文件夹是不可见或如果文件夹为空，选择**刷新**图标，然后**显示所有文件**顶部图标**解决方案资源管理器**窗口。 扩展的宽度**解决方案资源管理器**windows 所要显示的所有可用的图标。


现在可以检查中包含的数据*wingtiptoys.mdf*使用的数据库文件**服务器资源管理器**窗口。

1. 展开*应用程序\_数据*文件夹。 如果*应用程序\_数据*文件夹是不可见，请参阅上面的说明。
2. 如果*wingtiptoys.mdf*数据库文件不可见，请选择**刷新**图标，然后**显示所有文件**顶部的图标**解决方案资源管理器**窗口。
3. 右键单击*wingtiptoys.mdf*数据库文件，然后选择**打开**。  
    **服务器资源管理器**显示。 

    ![UI 和导航-服务器资源管理器](ui_and_navigation/_static/image8.png)
4. 展开*表*文件夹。
5. 右键单击**产品**表，然后选择**显示表数据**。  
 **产品**显示表。 

    ![用户界面和导航的 Products 表](ui_and_navigation/_static/image9.png)
6. 此视图允许你查看和修改中的数据**产品**手动表。
7. 关闭**产品**表窗口。
8. 在中**服务器资源管理器**，右键单击**产品**再次表，然后选择**打开表定义**。  
 有关设计数据**产品**显示表。 

    ![UI 和导航-产品设计](ui_and_navigation/_static/image10.png)
9. 在中**T-SQL**选项卡上，您将看到用于创建表 SQL DDL 语句。 此外可以使用中的用户界面**设计**选项卡以修改架构。
10. 在中**服务器资源管理器**，右键单击**WingtipToys**数据库并选择**关闭连接**。   
 通过将数据库从 Visual Studio 分离，将能够更高版本在本系列教程中修改数据库架构。
11. 返回到**解决方案资源管理器**通过选择**解决方案资源管理器**选项卡的底部**服务器资源管理器**窗口。

## <a name="summary"></a>总结

在本教程中的一系列您添加了一些基本的用户界面、 图形、 页和导航。 此外，在运行 Web 应用程序，从上一教程中添加的数据类创建数据库。 您还可以查看的内容*产品*通过直接查看数据库的数据库的表。 在下一步的教程中，将显示数据项和从数据库的详细信息。

## <a name="additional-resources"></a>其他资源

[ASP.NET 网页编程简介](https://msdn.microsoft.com/library/ms178125.aspx)   
[ASP.NET Web 服务器控件概述](https://msdn.microsoft.com/library/zsyt68f1.aspx)   
[CSS 教程](http://www.w3schools.com/css/default.asp)

> [!div class="step-by-step"]
> [上一页](create_the_data_access_layer.md)
> [下一页](display_data_items_and_details.md)
