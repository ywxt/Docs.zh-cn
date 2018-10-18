---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: ASP.NET Web 窗体 Visual Studio 2013 中编辑代码 |Microsoft Docs
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 670f81ca1ef9923575cb2fee1747f06f426963d8
ms.sourcegitcommit: f43f430a166a7ec137fcad12ded0372747227498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2018
ms.locfileid: "49391214"
---
<a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a>在 Visual Studio 2013 中的代码编辑 ASP.NET Web 窗体
====================
通过[Erik Reitan](https://github.com/Erikre)

在许多 ASP.NET Web 窗体页中，您编写 Visual Basic、 C# 中，或另一种语言中的代码。 Visual Studio 中的代码编辑器可帮助您快速编写代码，同时又能避免错误。 此外，该编辑器还提供为您创建可重用代码的方式来帮助减少需要执行的工作量。

本演练说明了各种功能的 Visual Studio 代码编辑器。

在本演练中，你将学会如何执行以下任务：

- 更正内联编码错误。
- 重构和重命名的代码。
- 重命名的变量和对象。
- 插入代码段。

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

在本演练的此部分中，将创建 Web 应用程序项目，并向其添加一个新页面。

### <a name="to-create-a-web-application-project"></a>若要创建 Web 应用程序项目

1. 打开 Microsoft Visual Studio。
2. 在“文件”菜单上，选择“新建项目”。  
    ![文件菜单](code-editing-in-web-forms-pages/_static/image1.png)

    此时将出现 “新建项目” 对话框。
3. 选择**模板** - &gt; **Visual C#**  - &gt; **Web**在左侧的模板组。
4. 选择**ASP.NET Web 应用程序**在中心列中的模板。
5. 将项目命名***BasicWebApp***然后单击**确定**按钮。   
![新建项目对话框](code-editing-in-web-forms-pages/_static/image2.png)
6. 接下来，选择**Web 窗体**模板，然后单击**确定**按钮创建项目。  
![新建 ASP.NET 项目对话框](code-editing-in-web-forms-pages/_static/image3.png)  

    Visual Studio 创建新的项目，包括基于 Web 窗体模板的预生成的功能。


## <a name="creating-a-new-aspnet-web-forms-page"></a>创建新的 ASP.NET Web 窗体页


当您创建新的 Web 窗体应用程序使用**ASP.NET Web 应用程序**项目模板，Visual Studio 将添加名为的 ASP.NET 页 （Web 窗体页） *Default.aspx*，以及其他多个文件和文件夹。 可以使用*Default.aspx*为 Web 应用程序主页的页。 但是，对于本演练中，将创建和使用新的页面。

### <a name="to-add-a-page-to-the-web-application"></a>若要添加到 Web 应用程序页


1. 在中**解决方案资源管理器**，右键单击 Web 应用程序名称 (在本教程中的应用程序名称是**BasicWebSite**)，然后单击**添加** - &gt;**新项**。   
随即出现“添加新项”对话框。
2. 选择**Visual C#**  - &gt; **Web**在左侧的模板组。 然后，选择**Web 窗体**从中间列表并将其命名*FirstWebPage.aspx*。   
    ![添加新项对话框](code-editing-in-web-forms-pages/_static/image4.png)
3. 单击**添加**将 Web 窗体页添加到你的项目。  
 Visual Studio 创建新页面，并将其打开。
4. 接下来，将此新的页设置为默认启动页。 在中**解决方案资源管理器**，右键单击名为的新页*FirstWebPage.aspx* ，然后选择**设为起始页**。 在下次运行此应用程序以测试我们的进度，将会自动看到此新页在浏览器中。


## <a name="correcting-inline-coding-errors"></a>更正内联编码错误


Visual Studio 中的代码编辑器可帮助你避免错误，因为你编写代码，并且进行了错误，代码编辑器可帮助你更正此错误。 在本演练的此部分中，您将编写一行代码，用于演示在编辑器中的错误更正功能。

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a>若要更正 Visual Studio 中的简单编码错误


1. 在中**设计**视图中，双击空白页后，可以创建一个处理程序**负载**事件页。   
   使用仅作为一个位置的事件处理程序编写一些代码。
2. 在处理程序中，键入以下行，其中包含了错误并按**ENTER**:

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   当您按下**ENTER**，在代码编辑器将绿色和红色下划线 (通常会调用&quot;波浪&quot;行) 下的代码有问题的区域。 绿色下划线指示警告。 一条红色下划线指示一个错误，则必须修复。 

    将鼠标指针停留在`myStr`以查看工具提示，告诉你有关该警告。 此外，将鼠标指针悬停以查看错误消息的红色下划线。

    下图显示了带下划线的代码。

    ![在设计视图中的欢迎文本](code-editing-in-web-forms-pages/_static/image5.png "在设计视图中的欢迎文本")  
   必须通过添加分号来解决该错误`;`至行尾。 此警告只是通知尚未使用过`myStr`尚未变量。  

    > [!NOTE] 
    > 
    > 查看当前代码格式设置在 Visual Studio 中的通过选择**工具** - &gt; **选项** - &gt; **字体和颜色**。


## <a name="refactoring-and-renaming"></a>重构和重命名

重构是一种软件方法涉及重构代码，使其更易于理解和维护，同时保留其功能。 一个简单的示例可能是从数据库获取数据的事件处理程序中编写代码。 开发您的页面时，您发现您需要从多个不同的处理程序访问数据。 因此，通过在页面中创建数据访问方法并将对方法的调用插入的处理程序中重构页面的代码。

在代码编辑器包括可帮助你执行各种任务，重构工具。 在本演练中，将使用两种重构的方法： 重命名变量和提取方法。 其他重构选项包括封装字段、 局部变量提升为方法参数，以及管理方法参数。 这些重构选项的可用性取决于代码中的位置。

### <a name="refactoring-code"></a>重构代码

常见的重构方案是创建 （提取） 从另一个成员，如方法内部的代码的方法。 这会减少原始成员的大小，并使提取的代码可重用。

在本演练的此部分中，将编写一些简单代码，，然后从其提取方法。 重构支持 C# 中，因此将创建使用 C# 作为编程语言的网页。

### <a name="to-extract-a-method-in-a-c-page"></a>若要提取的 C# 页面中的方法

1. 切换到**设计**视图。
2. 在中**工具箱**，从**标准**选项卡上，拖动[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件拖到页面。
3. 双击**按钮**控件创建的处理程序及其[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件，然后添加以下突出显示的代码：

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   该代码会创建**ArrayList**对象，使用循环加载具有值，然后再使用另一个循环中显示的内容**ArrayList**对象。
4. 按**CTRL + F5**以运行此页面，然后单击**按钮**以确保你看到以下输出：   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. 返回到代码编辑器，然后选择事件处理程序中的的以下行。   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. 右键单击所选内容中，单击**重构**，然后选择**提取方法**。 

    **提取方法**对话框随即出现。
7. 在中**新的方法名称**框中，键入**DisplayArray**，然后单击**确定**。 

    在代码编辑器创建名为的新方法`DisplayArray`，并将对中的新方法的调用放**单击**循环最初的处理程序。

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. 按**CTRL + F5**页上再次运行，并单击**按钮**。

    此页面的功能相同就像以前一样。 `DisplayArray`方法现在可以从任何位置调用页类中。

## <a name="renaming-variables"></a>重命名变量

使用变量，以及对象时，你可能想要重命名它们后它们已在代码中引用。 但是，重命名的变量和对象可能导致代码中断如果错过了重命名其中一个引用。 因此，您可以使用重构来执行重命名。

### <a name="to-use-refactoring-to-rename-a-variable"></a>若要使用重构重命名变量


1. 在中**单击**事件处理程序中，找到以下行：

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. 右键单击变量名`alist`，选择**重构**，然后选择**重命名**。

    **重命名**对话框随即出现。
3. 在中**新的名称**框中，键入**ArrayList1** ，并确保**预览引用更改**选中复选框。 然后单击“确定” 。

    **预览更改**对话框随即出现，并显示一个树，它包含要重命名的变量对所有引用。
4. 单击**Apply**以关闭**预览更改**对话框。

    特定于所选实例引用的变量进行重命名。 但请注意，该变量`alist`以下行中未重命名。

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    在变量`alist`此行中不重命名，因为它不表示相同的值与变量`alist`您重命名为。 在变量`alist`在`DisplayArray`声明为该方法的局部变量。 这说明了使用重构重命名变量是不同于只需在编辑器中执行查找和替换操作了解自己正在使用的变量的语义与重构重命名变量。


## <a name="inserting-snippets"></a>插入代码段

由于有许多 Web 窗体开发人员经常需要执行的编码任务，代码编辑器提供了一个库的代码段或预先编写的代码块。 可以将这些代码段插入您的页面。

在 Visual Studio 中使用每种语言已插入代码段的方式略有差异。 有关插入代码段的信息，请参阅[Visual Basic IntelliSense 代码段](https://msdn.microsoft.com/library/18yz4be4.aspx)。 有关插入代码段 Visual C# 中的信息，请参阅[Visual C# 代码片段](https://msdn.microsoft.com/library/z41h7fat.aspx)。

## <a name="next-steps"></a>后续步骤

本演练为更正代码中的错误、 重构代码、 重命名变量，并将代码段插入到你的代码演示了 Visual Studio 2010 代码编辑器的基本功能。 在编辑器中的其他功能可以使应用程序开发快速而简单的。 例如，你可能希望：

- 详细了解 IntelliSense，如修改 IntelliSense 选项、 管理代码段，以及搜索代码代码段的功能。 有关详细信息，请参阅[使用 IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx)。
- 了解如何创建你自己的代码段。 有关详细信息，请参阅[创建和使用 IntelliSense 代码段](https://msdn.microsoft.com/library/ms165392.aspx)
- 了解有关 IntelliSense 代码段，如自定义代码段和故障排除的特定于 Visual Basic 的功能的详细信息。 有关详细信息，请参阅[Visual Basic IntelliSense 代码段](https://msdn.microsoft.com/library/18yz4be4.aspx)
- 了解有关 C# 的详细信息-的 IntelliSense、 重构和代码片段等的特定功能。 有关详细信息，请参阅[Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)。
