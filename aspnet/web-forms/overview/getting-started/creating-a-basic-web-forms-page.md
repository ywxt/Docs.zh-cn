---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: 使用 Visual Studio 2013 创建一个基本的 ASP.NET 4.5 Web 窗体页面
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: eb1a4632caf00097012bd1757da44016a076630f
ms.sourcegitcommit: f43f430a166a7ec137fcad12ded0372747227498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2018
ms.locfileid: "49391279"
---
# <a name="using-visual-studio-2013-to-create-a-basic-aspnet-45-web-forms-page"></a>使用 Visual Studio 2013 创建一个基本的 ASP.NET 4.5 Web 窗体页面

=== 通过[Erik Reitan](https://github.com/Erikre)

[!INCLUDE[](~/includes/rp.md)]

本演练为您提供的简介中的 Web 开发环境[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)并在[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。 本演练指导您创建一个简单的 ASP.NET Web 窗体页面，并说明了创建新的页面、 添加控件，以及编写代码的基本技术。

本演练涉及以下任务：

- 创建一个文件系统 Web 窗体应用程序项目。
- 您熟悉 Visual Studio。
- 创建一个 ASP.NET 页。
- 添加控件。
- 添加事件处理程序。
- 运行和测试 Visual Studio 中的一页。

## <a name="prerequisites"></a>系统必备

若要完成本演练，你将需要：

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。 会自动安装.NET Framework。 

    > [!NOTE] 
    > 
    > Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 for Web 将通常称为 Visual Studio 在整个教程系列中。  
    >   
    > 如果使用的 Visual Studio，本演练假定你所选**Web 开发**的设置集合，首次启动 Visual Studio。 有关详细信息，请参阅[如何： 选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。


## <a name="creating-a-web-application-project-and-a-page"></a>创建 Web 应用程序项目和页面

<a id="sectionToggle0"></a>

在本演练的此部分中，将创建 Web 应用程序项目，并向其添加一个新页面。 此外将添加 HTML 文本，并在浏览器中运行页面。

### <a name="to-create-a-web-application-project"></a>若要创建 Web 应用程序项目

1. 打开 Microsoft Visual Studio。
2. 在“文件”菜单上，选择“新建项目”。  
    ![文件菜单](creating-a-basic-web-forms-page/_static/image1.png)

    此时将出现 “新建项目” 对话框。
3. 选择**模板** - &gt; **Visual C#**  - &gt; **Web**在左侧的模板组。
4. 选择**ASP.NET Web 应用程序**在中心列中的模板。
5. 将项目命名***BasicWebApp***然后单击**确定**按钮。   
![新建项目对话框](creating-a-basic-web-forms-page/_static/image2.png)
6. 接下来，选择**Web 窗体**模板，然后单击**确定**按钮创建项目。  
![新建 ASP.NET 项目对话框](creating-a-basic-web-forms-page/_static/image3.png)  

    Visual Studio 创建新的项目，包括基于 Web 窗体模板的预生成的功能。 它不仅提供了与您*Home.aspx*页上， *About.aspx*页上， *Contact.aspx*页上，但还包括注册用户，并将保存的成员资格功能其凭据，以便他们可以登录到你的网站。 创建一个新页面时，默认情况下 Visual Studio 将显示在页面**源**视图中，可以看到此页的 HTML 元素的位置。 下图显示了您在中会看到**源**查看如果你创建一个名为的新 Web 页*BasicWebApp.aspx*。  
    ![源视图](creating-a-basic-web-forms-page/_static/image4.png)


### <a name="a-tour-of-the-visual-studio-web-development-environment"></a>Visual Studio Web 开发环境教程


通过修改页面继续操作之前，最好您熟悉 Visual Studio 开发环境。 下图显示了 windows 和 Visual Studio 和 Visual Studio Express for Web 中提供的工具。

> [!NOTE] 
> 
> 下图显示的默认窗口和窗口位置。 **视图**菜单允许您以显示其他窗口，并重新排列和调整大小以适合您的首选项。 如果已为窗口排列方式进行更改，您看到的内容将与该图不匹配。


 在 Visual Studio 环境

![Visual Studio 环境](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a>熟悉 Web 设计器

检查上图中，并匹配到以下列表中，文本窗口和工具，它描述了最常使用。 （不是所有 windows 和，请参阅此处列出的工具，只有标记都为在上图中。）

- 工具栏。 提供用于格式化文本、 查找文本等命令。 仅当您正在使用时，某些工具栏才可用**设计**视图。
- **解决方案资源管理器**窗口。 在 Web 应用程序中显示的文件和文件夹。
- 文档窗口。 显示您正在努力在选项卡式窗口中的文档。 可以通过单击选项卡在文档之间进行切换。
- **属性**窗口。 可以更改的页面、 HTML 元素、 控件和其他对象的设置。
- 查看选项卡。 提供在同一文档的不同视图。 **设计**视图是附近 WYSIWYG 编辑图面。 **源**视图是页面的 HTML 编辑器。 **拆分**视图显示两者**设计**视图和**源**文档视图。 您可以使用**设计**并**源**稍后在本演练的视图。 如果您想打开中的网页**设计**查看，请在**工具**菜单中，单击**选项**，选择**HTML 设计器**节点，然后更改**起始页位置**选项。
- **工具箱**。 提供控件和 HTML 元素，您可以拖放到您的页面。 **工具箱**元素进行分组的公共函数。
- S**服务器资源管理器**。 显示数据库连接。 如果服务器资源管理器不可见，请在视图菜单上单击服务器资源管理器。


### <a name="creating-a-new-aspnet-web-forms-page"></a>创建新的 ASP.NET Web 窗体页


当您创建新的 Web 窗体应用程序使用**ASP.NET Web 应用程序**项目模板，Visual Studio 将添加名为的 ASP.NET 页 （Web 窗体页） *Default.aspx*，以及其他多个文件和文件夹。 可以使用*Default.aspx*为 Web 应用程序主页的页。 但是，对于本演练中，将创建和使用新的页面。

### <a name="to-add-a-page-to-the-web-application"></a>若要添加到 Web 应用程序页


1. 关闭*Default.aspx*页。 若要执行此操作，单击显示文件名称的选项卡，然后单击关闭选项。
2. 在中**解决方案资源管理器**，右键单击 Web 应用程序名称 (在本教程中的应用程序名称是**BasicWebSite**)，然后单击**添加** - &gt;**新项**。   
随即出现“添加新项”对话框。
3. 选择**Visual C#**  - &gt; **Web**在左侧的模板组。 然后，选择**Web 窗体**从中间列表并将其命名*FirstWebPage.aspx*。   
    ![添加新项对话框](creating-a-basic-web-forms-page/_static/image6.png)
4. 单击**添加**将 web 页面添加到你的项目。  
Visual Studio 创建新页面，并将其打开。


### <a name="adding-html-to-the-page"></a>将 HTML 添加到页面


在本演练的此部分中，将向页面添加一些静态文本。

### <a name="to-add-text-to-the-page"></a>若要将文本添加到页面


1. 在文档窗口的底部，单击**设计**选项卡以切换到**设计**视图。

    设计视图中显示的当前页的类似所见即所得的方式。 此时，你没有任何文本或控件的页上，因此页是空白勾勒出矩形轮廓的虚线除外。 表示此矩形**div**页上的元素。
2. 虚线所概述的矩形内部单击。
3. 类型**欢迎使用 Visual Web Developer**然后按**ENTER**两次。

    下图显示了在您键入的文本**设计**视图。

    ![在设计视图中的欢迎文本](creating-a-basic-web-forms-page/_static/image7.png "在设计视图中的欢迎文本")
4. 切换到**源**视图。

    您可以看到在 HTML**源**中键入时创建的视图**设计**视图。  
    ![包含静态文本的网页](creating-a-basic-web-forms-page/_static/image8.png)


### <a name="running-the-page"></a>运行页面


通过将控件添加到页面继续操作之前，您可以首先运行它。

### <a name="to-run-the-page"></a>若要运行页


1. 在中**解决方案资源管理器**，右键单击*FirstWebPage.aspx* ，然后选择**设为起始页**。
2. 按**CTRL + F5**以运行该页。

    在浏览器中显示的页。 尽管你创建的页面具有的文件扩展名 *.aspx*，它当前在运行任何 HTML 页面所示。

    要在浏览器中显示的页面也可以右键单击中的页**解决方案资源管理器**，然后选择**用浏览器查看**。
3. 关闭浏览器来停止 Web 应用程序。


## <a name="adding-and-programming-controls"></a>添加和控件进行编程


<a id="sectionToggle1"></a>

现在将到页服务器控件。 服务器控件，如按钮、 标签、 文本框、 文本框和其他熟悉的控件，提供 Web 窗体页面的典型窗体处理功能。 但是，可以使用在服务器上，而不是客户端运行的代码对控件进行编程。

您将添加[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件，[文本框](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件，和一个[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)到页面控件，并编写代码来处理[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件。

### <a name="to-add-controls-to-the-page"></a>若要将控件添加到页面


1. 单击**设计**选项卡以切换到**设计**视图。
2. 将插入点放在末尾**欢迎使用 Visual Web Developer**文本，然后按**ENTER**五次或多次以留出一些空间中的**div**元素。
3. 在中**工具箱**，展开**标准**如果尚未展开组。  
请注意，可能需要展开**工具箱**窗口左侧查看它。
4. 拖动[文本框中](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件拖动到页面并将其中间的放**div**元素中具有**欢迎使用 Visual Web Developer**中的第一行。
5. 拖动[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件拖动到页面并将其放到右侧[文本框中](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件。
6. 拖动[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件拖到页面并将其放在单独的行下面[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件。
7. 将插入点定位上述[文本框](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件，然后键入**输入您的姓名：** 。

    此静态 HTML 文本是标题[文本框中](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件。 可以混合使用静态 HTML 和同一页面上的服务器控件。 下图显示了三个控件中的显示方式**设计**视图。

    ![在设计视图中的三个控件](creating-a-basic-web-forms-page/_static/image9.png "在设计视图中的三个控件")


### <a name="setting-control-properties"></a>设置控件属性


Visual Studio 提供了各种方法来设置页上的控件的属性。 在本演练的此部分中，您将在这种设置属性**设计**视图和**源**视图。

### <a name="to-set-control-properties"></a>若要设置控件属性


1. 首先，显示**属性**窗口中的，选择从**视图**菜单&gt;**其他 Windows**  - &gt; **属性窗口**。 或者，您可以选择**F4**以显示**属性**窗口。
2. 选择[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件，然后在**属性**窗口中，设置的值**文本**到**显示名称**。 下图中所示，在设计器中，按钮上显示您输入的文本。

    ![设置按钮文本](creating-a-basic-web-forms-page/_static/image10.png "设置按钮文本")
3. 切换到**源**视图。

    **源**视图显示该页面，其中包括 Visual Studio 已创建服务器控件的元素的 HTML。 控件使用类似于 HTML 的语法声明，只不过标记使用前缀**asp:** 和包含该特性**runat =&quot;server&quot;**。

    控件属性被声明为属性。 例如，设置[文本](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx)属性[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件，在步骤 1 中，实际在设置**文本**控件的标记中的属性。

    > [!NOTE] 
    > 
    > 所有控件都都位于**窗体**元素，它还具有特性**runat =&quot;server&quot;**。 **Runat =&quot;服务器&quot;** 属性并**asp:** 前缀将对控件标记将控件标记，以便它们是由 ASP.NET 在服务器上处理运行时。 外部的代码**&lt;形成 runat =&quot;服务器&quot;&gt;** 并**&lt;脚本 runat =&quot;server&quot; &gt;** 元素发送到浏览器中，这就是原因 ASP.NET 代码必须位于其开始标记中包含的元素不变**runat =&quot;服务器&quot;** 属性。
4. 接下来，将添加到一个附加属性[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。 将插入点直接后的**asp: Label**中**&lt;asp: Label&gt;** 标记，并将然后按**空格键**。

    将显示下拉列表，显示为可以设置的可用属性的列表[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。 此功能，称为**智能感知**，可以帮助您应对**源**页面上的语法的服务器控件、 HTML 元素和其他项的视图。 如下图所示**智能感知**下拉列表[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。

    ![IntelliSense 特性](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense 特性")
5. 选择**ForeColor** ，然后键入一个等号。

    IntelliSense 将显示一个颜色列表。

    > [!NOTE] 
    > 
    > 可以显示**智能感知**随时通过按下的下拉列表**CTRL + J**查看代码时。
6. 选择的颜色**[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** 控件的文本。 请确保选择足够深，以便读取在白色背景的颜色。

    **ForeColor**属性已完成，但已选择，包括右引号后面的颜色。


### <a name="programming-the-button-control"></a>编程的按钮控件


对于本演练，你将编写代码，用于读取用户在文本框中输入并随后显示中的名称的名称[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。

### <a name="add-a-default-button-event-handler"></a>添加默认按钮事件处理程序


1. 切换到**设计**视图。
2. 双击[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件。

    默认情况下，Visual Studio 切换到代码隐藏文件，并创建主干事件处理程序[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的默认事件[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件。 代码隐藏文件 （如 C# 中) 在服务器代码分离开来 UI 标记 （例如 HTML)。   
   游标位于添加此事件处理程序代码。

    > [!NOTE] 
    > 
    > 双击中的控件**设计**视图只会是一种方式可以创建事件处理程序。
3. 内部**Button1\_单击**事件处理程序中，键入**Label1**跟一个句点 (**。**)。

    当您键入超过这个有效期之后**ID**标签的 (**Label1**)，Visual Studio 将显示为可用成员列表[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控制，请在下面的示例所示图。 成员通常的属性、 方法或事件。

    ![代码视图中的 IntelliSense](creating-a-basic-web-forms-page/_static/image12.png "代码视图中的 IntelliSense")
4. 完成**单击**按钮使其内容如下面的代码示例中所示的事件处理程序。

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. 切换回查看**源**视图通过右键单击你的 HTML 标记*FirstWebPage.aspx*中**解决方案资源管理器**并选择**视图标记**。
6. 滚动到**&lt;: Button&gt;** 元素。 请注意， **&lt;: Button&gt;** 元素现在具有特性**onclick =&quot;Button1\_单击&quot;**。

    此属性将绑定的按钮[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)到上一步中编码的处理程序方法的事件。

    事件处理程序方法可以具有任何名称;显示的名称是由 Visual Studio 创建的默认名称。 重要的一点是，该名称将用于**OnClick** HTML 中的属性必须匹配在代码隐藏中定义的方法的名称。


### <a name="running-the-page"></a>运行页面


现在可以测试页上的服务器控件。

### <a name="to-run-the-page"></a>若要运行页


1. 按**CTRL + F5**以在浏览器中运行该页。 如果发生错误，重新检查上述步骤。
2. 在文本框中输入一个名称，然后单击**显示名称**按钮。

    您输入的名称显示在[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。 请注意，当单击按钮时，页面将被发送到 Web 服务器。 ASP.NET 然后重新创建该页，运行你的代码 (在这种情况下，[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件处理程序将运行)，然后将新页发送到浏览器。 如果你观看在浏览器中的状态栏，可以看到，页面往返到 Web 服务器每次单击按钮。
3. 在浏览器中，查看正在运行的页上右键单击并选择页面的源代码**查看源**。

    在页的源代码，可以看到 HTML 而无需任何服务器代码。 具体而言，未看到**&lt;asp:&gt;** 你正在使用中的元素**源**视图。 页运行时，ASP.NET 会处理服务器控件，并呈现到页的 HTML 元素，可执行表示控件的功能。 例如， **&lt;: Button&gt;** 控件呈现为 HTML **&lt;输入类型 =&quot;提交&quot;&gt;** 元素。
4. 关闭浏览器。


## <a name="working-with-additional-controls"></a>中的其他控件

<a id="sectionToggle2"></a>

在本演练的此部分中，您可以使用[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件，用于一次显示一个月的日期。 [日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件是一个更复杂比你一直使用的按钮、 文本框中和标签控件，并说明了服务器控件的一些其他功能。

在本部分中，您将添加[System.Web.UI.WebControls.Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制对页面并设置其格式。

### <a name="to-add-a-calendar-control"></a>若要添加一个日历控件


1. 在 Visual Studio 中，切换到**设计**视图。
2. 从**标准**一部分**工具箱**，拖动[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)拖放到页面上控制**div**元素，包含其他控件。

    显示日历的智能标记面板。 面板将显示命令，可以轻松为选定的控件执行的最常见任务。 如下图所示[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制中呈现**设计**视图。

    ![月历控件在设计视图](creating-a-basic-web-forms-page/_static/image13.png "月历控件在设计视图")
3. 在智能标记面板中，选择**自动套用格式**。

    **自动套用格式**显示对话框，该编辑器可以为该日历选择一个格式设置方案。 如下图所示**自动套用格式**对话框[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件。

    ![自动格式对话框 （Calendar 控件）](creating-a-basic-web-forms-page/_static/image14.png "自动套用格式对话框 （Calendar 控件）")
4. 从**选择一种方案**列表中，选择**简单**，然后单击**确定**。
5. 切换到**源**视图。

    您可以看到 **&lt;asp： 日历&gt;** 元素。 此元素是远远超过前面创建的简单控件的元素。 它还包括子元素，如 **&lt;WeekEndDayStyle&gt;**，这表示各种格式设置。 如下图所示[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制**源**视图。 (请参阅中的确切标记**源**视图可能略有不同的图。)

    ![月历控件在源视图](creating-a-basic-web-forms-page/_static/image15.png "月历控件在源视图中")


### <a name="programming-the-calendar-control"></a>日历控件编程


在本部分中，将编程[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件来显示当前选定的日期。

### <a name="to-program-the-calendar-control"></a>日历控件编程


1. 在中**设计**视图中，双击[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件。

    创建新的事件处理程序并将其显示在代码隐藏文件中名为*FirstWebPage.aspx.cs*。
2. 完成[SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx)事件处理程序替换下面的代码。

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]


    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]

    上面的代码中设置为所选日期的日历控件的标签控件的文本。


### <a name="running-the-page"></a>运行页面


现在可以测试日历。

### <a name="to-run-the-page"></a>若要运行页


1. 按**CTRL + F5**以在浏览器中运行该页。
2. 单击日历中的日期。

    在显示你单击的日期[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控件。
3. 在浏览器中查看页面的源代码。

    请注意，[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制呈现给页面**表**，为每个日期**td**元素。
4. 关闭浏览器。


## <a name="next-steps"></a>后续步骤


<a id="nextStepsToggle"></a>

本演练演示了 Visual Studio 页面设计器的基本功能。 现在，你已了解如何创建和编辑 Visual Studio 中的 Web 窗体页，您可能想要探索其他功能。 例如，你可能想要执行以下操作：

- 按照以下分步教程系列中了解有关 ASP.NET Web 窗体的详细信息[Getting Started with ASP.NET 4.5 Web 窗体和 Visual Studio 2013](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。
- 了解有关级联样式表 (CSS) 的详细信息。 有关详细信息，请参阅[使用 CSS 概述](https://msdn.microsoft.com/library/bb398931.aspx)。
