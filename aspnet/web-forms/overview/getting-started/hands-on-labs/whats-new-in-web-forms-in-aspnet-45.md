---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: 在 ASP.NET 4.5 中新增 Web 窗体 |Microsoft Docs
author: rick-anderson
description: ASP.NET Web 窗体的新版本引入了大量专注于处理数据时改善用户体验的改进。 在以前版本的...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 54e0234d6f13ce62803dbe55a836414a93a207b2
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825998"
---
<a name="whats-new-in-web-forms-in-aspnet-45"></a>什么是在 ASP.NET 4.5 Web 窗体中的新增功能
====================
通过[Web 训练营团队](https://twitter.com/webcamps)

> ASP.NET Web 窗体的新版本引入了大量专注于处理数据时改善用户体验的改进。
> 
> 在以前版本的 Web 窗体，使用数据绑定发出对象成员的值时，您可以使用数据绑定表达式的 bind （） 或 eval （）。 在新的 ASP.NET 版本中，您就能够声明一个控件要通过使用新的 ItemType 属性绑定到的数据类型。 设置此属性以便可以使用强类型化变量来接收 Visual Studio 开发体验，如 IntelliSense、 成员导航和编译时检查的全部益处。
> 
> 数据绑定控件中，现在还可以指定你自己自定义的方法，用于选择、 更新、 删除和插入数据，从而简化页面控件和应用程序逻辑之间的交互。 另外，模型绑定功能已被添加到 ASP.NET 中，这意味着您可以从页的数据直接映射到方法类型参数。
> 
> 验证用户输入还应简化了 Web 窗体的最新版本。 现在，你可以批注与从验证特性在模型类**System.ComponentModel.DataAnnotations**命名空间和所有站点都控制的请求验证用户输入使用该信息。 在 Web 窗体中的客户端验证现与 jQuery，提供清理器客户端代码和非介入式 JavaScript 功能集成。
> 
> 在请求验证区域中，已得到改进以方便您来有选择地关闭应用程序的特定部分的请求验证或读取未经验证的请求数据。
> 
> 某些已得到改进 Web 窗体服务器控件能够充分利用 HTML5 的新功能：
> 
> - TextBox 控件将 TextMode 属性已更新以支持电子邮件、 datetime 等新的 HTML5 输入的类型。
> - FileUpload 控件现在支持从支持此 HTML5 功能的浏览器上传多个文件。
> - 验证程序控件现在支持验证 HTML5 输入的元素。
> - 了现在表示 URL 的属性的新 HTML5 元素支持 runat =&quot;server&quot;。 因此，您可以使用 ASP.NET 约定中 URL 路径，如 ~ 运算符来表示应用程序根目录 (例如，&lt;视频 runat =&quot;服务器&quot;src =&quot;~/myVideo.wmv&quot; &gt; &lt;/视频&gt;)。
> - 已修复的 UpdatePanel 控件，以便支持发布 HTML5 输入的字段。
> 
> 官方 ASP.NET 门户中可以找到 ASP.NET WebForms 4.5 中的新功能的更多示例： [What's New in ASP.NET 4.5 和 Visual Studio 2012](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)
> 
> 在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)。


<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验，您将学习如何：

- 使用强类型化数据绑定表达式
- 在 Web 窗体中使用新的模型绑定功能
- 将值提供程序用于将页面数据映射到代码隐藏方法
- 用户输入验证中使用数据注释
- 在 Web 窗体中执行 advange unobstrusive 使用 jQuery 的客户端验证
- 实现粒度请求验证
- 实现在 Web 窗体中处理的异步页面

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

必须具有要完成本实验的以下项：

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。

<a id="Setup"></a>
### <a name="setup"></a>安装

**安装代码片段**

为方便起见，您将沿此实验室管理大部分是代码的可用作 Visual Studio 代码段。 若要安装运行的代码段 **.\Source\Setup\CodeSnippets.vsi**文件。

如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 c： 使用代码片段](#AppendixC)&quot;。

<a id="Exercises"></a>
## <a name="exercises"></a>练习

本动手实验包括以下练习：

1. [练习 1： 模型绑定在 ASP.NET Web 窗体](#Exercise1)
2. [练习 2： 数据验证](#Exercise2)
3. [练习 3： 异步页处理在 ASP.NET Web 窗体](#Exercise3)

> [!NOTE]
> 每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。 如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。


估计的时间才能完成此实验： **60 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a>练习 1： 模型绑定在 ASP.NET Web 窗体

ASP.NET Web 窗体的新版本引入了一些侧重于改进体验，使用数据时的增强功能。 在本练习中，将了解强类型化数据控件和模型绑定。

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a>任务 1-使用强类型化的数据绑定

在此任务中，您将发现的新强类型绑定 ASP.NET 4.5 中提供。

1. 打开**开始**解决方案位于**源/Ex1-ModelBinding/开始/** 文件夹。

   1. 需要先下载某些缺少的 NuGet 包然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 打开**Customers.aspx**页。 置于主控件没有编号的列表，包括用于列出每个客户一个 repeater 控件。 Repeater 名称设置为**customersRepeater**如下面的代码中所示。

    在以前版本的 Web 窗体，如果使用数据绑定发出对象成员的值是数据绑定，您将使用数据绑定表达式，以及调用 Eval 方法，传递该成员的名称作为字符串。

    在运行时，对 Eval 的这些调用将使用针对当前绑定对象的反射来读取的具有给定名称的成员的值和 html 格式显示结果。 此方法可以非常轻松地针对任意、 unshaped 数据进行数据绑定。

    遗憾的是，您会丢失的许多出色的开发时间体验在 Visual Studio 中，对成员名称、 对导航 （例如，请转到定义），和编译时检查的支持包括 IntelliSense 功能。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. 打开**Customers.aspx.cs**文件。
4. 添加以下 using 语句。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. 在中**页上\_负载**方法中，添加代码以填充客户列表使用 repeater。

    (代码段- *Web 窗体实验-Ex01-绑定的客户数据源*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    该解决方案使用 EntityFramework CodeFirst 以及创建和访问数据库。 在下面的代码，customersRepeater 已绑定到从数据库中返回的所有客户实例化查询。
6. 按**F5**若要运行解决方案并转到**客户**页以查看操作中的 repeater。 因为该解决方案使用 CodeFirst，将创建并运行应用程序时，在本地 SQL Express 实例中填充数据库。

    ![列出的客户可以 repeater](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "列出的客户可以 repeater")

    *列出的客户可以 repeater*

    > [!NOTE]
    > 在 Visual Studio 2012 中，IIS Express 是默认的 Web 开发服务器。
7. 关闭浏览器并返回到 Visual Studio。
8. 现在将为要使用强类型化的绑定的实现。 打开**Customers.aspx**页上，并使用新**ItemType**中继器设置中的属性**客户**类型作为绑定类型。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    ItemType 属性，可声明哪些类型的数据控件将绑定到和允许您使用强类型绑定的数据绑定控件内。
9. 将为 ItemTemplate 内容与下面的代码。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    与上述方法的一个缺点是对 eval （） 和 bind （） 的调用是后期绑定-这意味着传递字符串来表示属性名称。 这意味着您不能为成员名称也支持代码导航 （例如，请转到定义），不编译时检查支持使用 Intellisense。

    设置 ItemType 属性会导致两个新类型化的变量，在数据绑定表达式的作用域中生成：**项**并**BindItem**。 可以在数据绑定表达式中使用这些强类型化的变量，并获取 Visual Studio 开发体验的全部益处。

    &quot; **:** &quot;表达式中使用将自动进行 HTML 编码的输出以避免出现安全问题 （例如，跨站点脚本攻击）。 此表示法是自.NET 4 响应编写，但现在也会出现在数据绑定表达式。

    > [!NOTE]
    > 项成员适用于单向绑定。 如果你想要执行的双向绑定使用**BindItem**成员。

    ![中强类型绑定的 IntelliSense 支持](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "强类型化绑定中的 IntelliSense 支持")

    *中强类型绑定的 IntelliSense 支持*
10. 按**F5**若要运行解决方案，并转到客户页以确保按预期方式工作所做的更改。

    ![列出客户详细信息](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "列出客户详细信息")

    *列出客户详细信息*
11. 关闭浏览器并返回到 Visual Studio。

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a>任务 2-引入模型绑定在 Web 窗体

在以前版本的 ASP.NET Web 窗体中，当您希望执行双向数据绑定，同时检索和更新数据，您需要使用数据源对象。 这可能对象数据源、 SQL 数据源、 LINQ 数据源，等等。 但是如果你的方案所需的处理数据的自定义代码，您需要使用对象数据源，并且这将一些缺点。 例如，您需要避免使用复杂类型和您所需执行的验证逻辑时处理的异常。

在新版本的 ASP.NET Web 窗体数据绑定控件支持模型绑定。 这意味着，您可以指定选择、 更新、 插入和删除要从代码隐藏文件或从另一个类调用逻辑的数据绑定控件中直接的方法。

若要了解相关信息，您将使用 GridView 列出使用新的产品类别**SelectMethod**属性。 此属性，可指定进行检索的 GridView 数据的方法。

1. 打开**Products.aspx**页上，包括**GridView**。 若要使用强类型绑定，并启用排序和分页如下所示配置 GridView。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. 使用新**SelectMethod**属性可配置 GridView 调用**GetCategories**方法来选择的数据。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. 打开**Products.aspx.cs**代码隐藏文件，并添加以下 using 语句。

    (代码段- *Web 窗体实验-Ex01-命名空间*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. 添加中的私有成员**产品**类，将分配的新实例**ProductsContext**。 此属性将存储实体框架数据上下文，可用于连接到数据库。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. 创建**GetCategories**方法来检索使用 LINQ 的类别的列表。 该查询将包括**产品**属性，以便 GridView 可以显示的每个类别的产品数量。 请注意，该方法返回原始的 IQueryable 对象，表示查询的更高版本上执行的页面生命周期。

    (代码段- *Web 窗体实验-Ex01-GetCategories*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > 在以前版本的 ASP.NET Web 窗体，启用排序和分页使用您自己的存储库逻辑在数据源对象上下文中，需编写自定义代码和接收所需的所有参数。 现在，如数据绑定方法可以返回 IQueryable，这表示查询仍要在执行，ASP.NET 可以修改查询以添加适当的排序和分页参数的处理。
6. 按**F5**可开始调试网站并转到产品页。 你应看到 GridView 中填充了 GetCategories 方法返回的类别。

    ![填充 GridView 使用模型绑定](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "填充 GridView 使用模型绑定")

    *填充 GridView 使用模型绑定*
7. 按**SHIFT**+**F5**停止调试。

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a>任务 3-在模型绑定中的值提供程序

模型绑定不仅可用于指定自定义方法以使用直接在数据绑定控件中，数据还可以将数据从页映射到从这些方法的参数。 在方法参数，可以使用值提供程序属性指定值的数据源。 例如：

- 在页上的控件
- 查询字符串值
- 查看数据
- 会话状态
- Cookie
- 已发布的表单数据
- 视图状态
- 也支持自定义值提供程序

如果您使用过 ASP.NET MVC 4，您会注意到是类似的模型绑定支持。 实际上，这些功能是从 ASP.NET MVC 和移动到**System.Web**要再也在 Web 窗体上使用这些程序集。

在此任务中，你将更新 GridView，其中的每个类别的产品量筛选其结果与模型绑定接收筛选器参数。

1. 返回到**Products.aspx**页。
2. 在 GridView 的顶部，添加**标签**和一个**组合框**若要选择的每个类别的产品数量，如下所示。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. 添加**要**到 GridView，其中包含所选的产品数量的任何类别时显示一条消息。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. 打开**Products.aspx.cs**隐藏代码，并添加以下 using 语句。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. 修改**GetCategories**方法来接收一个整数**minProductsCount**参数和筛选返回的结果。 若要执行此操作，请使用以下代码替换方法。

    (代码段- *Web 窗体实验-Ex01-GetCategories 2*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    新 **[控制]** 特性，可以在**minProductsCount**参数将告知 ASP.NET 使用控件的页中，必须填充其值。 ASP.NET 将查找参数 (minProductsCount) 的名称匹配的任何控件，并执行必需的映射和转换，以控制值填充参数。

    或者，该属性提供了可用于指定从何处获取此值控制的重载构造函数。

    > [!NOTE]
    > 数据绑定功能的一个目标是代码的减少需要编写的页交互量。 除了 [控制] 值提供程序，可以在方法参数中使用其他模型绑定提供程序。 任务简介中列出了其中一些。
6. 按**F5**可开始调试网站并转到产品页。 在下拉列表中选择的产品数，并注意如何 GridView 现已更新。

    ![筛选的下拉列表值 GridView](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "筛选的下拉列表值 GridView")

    *筛选的下拉列表值 GridView*
7. 停止调试。

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a>任务 4-使用模型绑定进行筛选

在本任务中，您将添加第二个子 GridView，其中显示所选类别中的产品。

1. 打开**Products.aspx**页上，并更新类别 GridView 自动生成的选择按钮。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. 添加另一个**GridView**名为**productsGrid**底部。 设置**ItemType**到**WebFormsLab.Model.Product**，则**DataKeyNames**到**ProductId**和**SelectMethod**到**GetProducts**。 设置**AutoGenerateColumns**到**false**和 ProductId、 ProductName、 说明和单价添加列。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. 打开**Products.aspx.cs**代码隐藏文件。 实现**GetProducts**方法以便接收来自 GridView 的类别的类别 ID 并筛选产品。 模型绑定将使用中的选定的行的参数值设置**categoriesGrid**。 由于参数名和控件名称不匹配，因此应控制值提供程序中指定的控件名称。

    (代码段- *Web 窗体实验-Ex01-GetProducts*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > 这种方法可以更方便地单元测试这些方法。 不执行 Web 窗体位置，在单元测试上下文 [控制] 属性将不执行任何特定操作。
4. 打开**Products.aspx**页上，找到产品 GridView。 更新产品 GridView，其中显示用于编辑所选的产品的链接。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. 打开**ProductDetails.aspx**页上的代码隐藏和替换**SelectProduct**用下面的代码的方法。

    (代码段- *Web 窗体实验-Ex01-SelectProduct 方法*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > 请注意， **[QueryString]** 属性用于填充从查询字符串中的产品 id 参数的方法参数。
6. 按**F5**可开始调试网站并转到产品页。 从 GridView 的类别中选择任何类别，请注意，更新产品 GridView。

    ![显示从所选类别产品](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "显示从所选类别产品")

    *显示从所选类别产品*
7. 单击**视图**产品打开 ProductDetails.aspx 页上的链接。

    请注意页面正在使用 SelectMethod 使用 productId 将参数从查询字符串中检索产品。

    ![查看产品详细信息](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "查看产品详细信息")

    *查看产品详细信息*

    > [!NOTE]
    > 键入说明 （HTML） 的功能将在下一个练习中实现。

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a>任务 5-使用模型绑定以执行更新操作

在上一任务中，选择数据的主要使用模型绑定，在此任务中，您将学习如何在更新操作中使用模型绑定。

你将更新的类别 GridView，以便用户可以更新类别。

1. 打开**Products.aspx**页上，并更新类别以自动生成编辑按钮并使用新的 GridView **UpdateMethod**属性来指定**UpdateCategory**方法来更新所选的项。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    GridView 中的 DataKeyNames 属性定义哪些是唯一标识的模型绑定的对象的成员，因此，哪些是更新方法至少应接收的参数。
2. 打开**Products.aspx.cs**代码隐藏文件，并实现**UpdateCategory**方法。 该方法应接收要加载的当前类别、 填充 GridView 中的值，然后更新类别的类别 ID。

    (代码段- *Web 窗体实验-Ex01-UpdateCategory*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    新**TryUpdateModel**中 Page 类的方法负责填充模型对象使用的页中的控件中的值。 在这种情况下，它将替换当前的 GridView 行编辑到更新后的值**类别**对象。

    > [!NOTE]
    > 下一步练习将说明用于验证用户输入时编辑的对象数据 ModelState.IsValid 的使用情况。
3. 运行网站并转到产品页。 编辑类别。 键入新名称，然后单击**更新**保存所做的更改。

    ![编辑类别](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "编辑类别")

    *编辑类别*

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a>练习 2： 数据验证

在此练习中，您将学习在 ASP.NET 4.5 中的新数据验证功能。 将签出 Web 窗体中的新非介入式验证功能。 将应用程序模型类中使用数据注释，用户输入验证，并最后，您将学习如何打开或关闭请求验证为在页面中的单个控件。

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a>任务 1-非介入式验证

窗体的复杂数据包括验证程序往往会在页中，可以代表大约 60%的代码生成过多的 JavaScript 代码。 启用非介入式验证，使用 HTML 代码看起来更干净且整洁。

在本部分中，您将启用非介入式验证在 ASP.NET 中要比较这两种配置生成的 HTML 代码。

1. 打开**Visual Studio 2012** ，然后打开**开始**解决方案位于**Source\Ex2 Validation\Begin**本实验的文件夹。 或者，您可以从上一练习在现有解决方案上继续工作。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 为此，请在解决方案资源管理器中，单击**WebFormsLab**项目**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 按**F5**启动 web 应用程序。 请转到客户页上，单击**添加新客户**链接。
3. 在浏览器页上，右键单击并选择**查看源**选项打开的应用程序生成的 HTML 代码。

    ![显示页面的 HTML 代码](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "显示页面的 HTML 代码")

    *显示页面的 HTML 代码*
4. 滚动浏览页的源代码，请注意，ASP.NET 注入了 JavaScript 代码和数据验证程序的页中执行验证并显示错误列表。

    ![验证 CustomerDetails 页面中的 JavaScript 代码](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "CustomerDetails 页中的验证 JavaScript 代码")

    *验证 CustomerDetails 页面中的 JavaScript 代码*
5. 关闭浏览器并返回到 Visual Studio。
6. 现在将启用非介入式验证。 打开**Web.Config**并找到**ValidationSettings:UnobtrusiveValidationMode**中的键**AppSettings**部分 **。** 将密钥值设置为**WebForms**。

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > 此外可以设置此属性&quot;**页面\_负载**&quot;以防你想要启用非介入式验证仅对某些页面的事件。
7. 打开**CustomerDetails.aspx**然后按**F5**启动 Web 应用程序。
8. 按 F12 键以打开 IE 开发人员工具。 开发人员工具打开后，选择脚本选项卡。选择**CustomerDetails.aspx**从菜单和需要注意需的页面上运行 jQuery 的脚本已加载到浏览器中从本地站点。

    ![正在加载 jQuery JavaScript 文件直接从本地 IIS 服务器](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "加载 jQuery JavaScript 文件直接从本地 IIS 服务器")

    *直接从本地 IIS 服务器加载 jQuery JavaScript 文件*
9. 关闭浏览器以返回到 Visual Studio。 打开**Site.Master**再次文件，找到**ScriptManager**。 将属性添加**EnableCdn**属性的值**True**。 这将强制 jQuery 加载从在线的 URL，而不在本地站点的 URL。
10. 打开**CustomerDetails.aspx** Visual Studio 中。 按 F5 键以运行该站点。 Internet Explorer 打开后，按 F12 键以打开开发人员工具。 选择**脚本**选项卡，然后再看一下拉列表。 请注意不能再从本地站点，而是在线 jQuery CDN 加载 jQuery JavaScript 文件。

    ![正在加载 jQuery JavaScript 文件从 CDN](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "加载 jQuery JavaScript 文件从 CDN")

    *加载从 CDN 的 jQuery JavaScript 文件*
11. 打开 HTML 页的源代码再次在浏览器中使用查看源选项。 请注意，通过启用非介入式验证 ASP.NET 已替换为插入的 JavaScript 代码的数据-\*属性。

    ![非介入式验证代码](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "非介入式验证代码")

    *非介入式验证代码*

    > [!NOTE]
    > 在此示例中，您已了解如何验证摘要的数据注释已简化为只需少量 HTML 和 JavaScript 行。 以前，而不进行非介入式验证，您添加更多验证控件越大 JavaScript 验证代码将会增长。

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a>任务 2-验证模型的数据注释

ASP.NET 4.5 引入了 Web 窗体的数据批注验证。 而不是让每个输入的验证控件，您现在可以在模型类中定义的约束，并使用它们跨所有 web 应用程序。 在本部分中，将了解如何使用数据注释来验证新建/编辑客户窗体。

1. 打开**CustomerDetail.aspx**页。 请注意，客户名字和中的第二个名称**EditItemTemplate**并**InsertItemTemplate**部分通过 RequiredFieldValidator 控件进行验证。 每个验证程序是关联到某个特定条件，因此您需要作为条件来检查包含任意多个验证程序。
2. 添加数据批注验证 Customer 模型类。 打开**Customer.cs**类**模型**文件夹和*修饰*使用数据注释特性的每个属性。

    (代码段- *Web 窗体实验-Ex02-数据批注*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > .NET framework 4.5 已扩展现有的数据批注集合。 以下是一些可以使用的数据批注: [CreditCard]，[Phone] [EmailAddress] [区域] [比较] [Url]，[FileExtensions]，[Required]、[Key]，[正则表达式]。
    > 
    > 一些用法示例：
    > 
    > [Key]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > 此外可以定义自己的错误消息中的每个属性。
3. 打开**CustomerDetails.aspx**和 FormView 控件在 EditItemTemplate InsertItemTemplate 部分中删除的第一个和最后一个名称字段的所有 RequiredFieldvalidators。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > 使用数据注释的一个优点是不会在应用程序页面中重复验证逻辑。 您在模型中，定义一次，并使用它跨所有操作数据的应用程序页。
4. 打开**CustomerDetails.aspx**代码隐藏和找到 SaveCustomer 方法。 此方法调用时插入新客户，并接收客户参数来自 FormView 控件值。 当页面控件与参数对象发生之间的映射，ASP.NET 将执行针对所有数据批注的模型验证特性和 ModelState 字典填充遇到的错误，如果有的话。

    ModelState.IsValid 将仅返回 true，如果执行验证后，您在模型上的所有字段都是有效。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. 添加**ValidationSummary** CustomerDetails 页后，可以显示的模型错误的列表末尾处的控件。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    **ShowModelStateErrors**是 ValidationSummary 上的新属性来控制，在设置为**true**，控件将显示 ModelState 字典中的错误。 这些错误来自数据批注验证。
6. 按**F5**运行 Web 应用程序。 完成窗体的某些错误值，然后单击**保存**执行验证。 请注意，错误摘要在底部。

    ![使用数据注释验证](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "使用数据注释验证")

    *使用数据注释验证*

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a>任务 3-处理自定义数据库错误的 ModelState

在以前版本的 Web 窗体，如太长字符串或唯一键冲突的数据库错误处理可能涉及在存储库代码中引发异常，然后处理在您的后台代码显示错误，异常。 非常高的代码需要做相对简单的事。

在 Web 窗体 4.5 ModelState 对象可以用于以一致的方式在页面上，从您的模型或从数据库中，显示的错误。

在本任务中，将添加代码以正确处理数据库异常，并使用 ModelState 对象向用户显示相应的消息。

1. 当应用程序仍在运行时，尝试更新使用重复的值的类别的名称。

    ![具有重复名称更新类别](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "具有重复名称更新类别")

    *具有重复名称更新类别*

    请注意，由于会引发异常&quot;唯一&quot;约束**CategoryName**列。

    ![重复的类别名称的异常](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "重复的类别名称的异常")

    *重复的类别名称的异常*
2. 停止调试。 在中**Products.aspx.cs**代码隐藏文件，update **UpdateCategory**方法以处理数据库引发的异常。Savechanges （） 方法调用并添加一个错误， **ModelState**对象。

    新**TryUpdateModel**方法更新使用窗体数据由用户提供从数据库检索到的类别对象。

    (代码段- *Web 窗体实验-Ex02-UpdateCategory 处理错误*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > 理想情况下，需要确定 DbUpdateException 的原因并检查是否违反唯一键约束的根本原因。
3. 打开**Products.aspx**并添加**ValidationSummary**如下类别 GridView，其中显示的模型错误的列表控件。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. 运行网站并转到产品页。 尝试更新使用的重复的值的类别的名称。

    请注意，处理异常和错误消息显示在**ValidationSummary**控件。

    ![复制类别错误](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "重复类别错误")

    *重复的类别错误*

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a>任务 4-请求 ASP.NET Web 窗体 4.5 中的验证

在 ASP.NET 请求验证功能提供了一定的默认保护免受跨站点脚本 (XSS) 攻击。 在以前版本的 ASP.NET，请求验证默认情况下已启用，仅可以禁用整个页面。 使用 ASP.NET Web 窗体的新版本现在可以禁用单个控件请求验证、 执行延迟请求验证或访问未经过验证的请求数据 （请小心，如果这样做 ！）。

1. 按**Ctrl + F5**启动网站，而不进行调试，转到产品页。 选择一个类别，然后单击**编辑**上的任何产品的链接。
2. 键入包含具有潜在危险的内容，例如包括 HTML 标记的说明。 注意由于请求验证引发的异常。

    ![编辑与具有潜在危险的内容的产品](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "编辑产品具有潜在危险的内容")

    *编辑产品具有潜在危险的内容*

    ![因请求验证而引发的异常](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "因请求验证而引发的异常")

    *因请求验证而引发的异常*
3. 关闭页，并在 Visual Studio 中，按**SHIFT + F5**以停止调试。
4. 打开**ProductDetails.aspx**页上，找到**说明**文本框中。
5. 添加新**ValidateRequestMode**属性设置为文本框中并将其值设置为**禁用**。

    新**ValidateRequestMode**特性，您可以禁用每个控件上精细地请求验证。 当你想要使用的输入的可能接收 HTML 代码，但想要保留的页的其余部分使用的验证时，这很有用。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. 按**F5**运行 web 应用程序。 再次打开编辑产品页，并完成包括 HTML 标记的产品说明。 请注意，可以现在将 HTML 内容添加到说明。

    ![请求验证的产品说明禁用](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "请求验证已禁用的产品说明")

    *请求验证已禁用的产品说明*

    > [!NOTE]
    > 应在生产应用程序中，清理输入的用户名，以确保输入唯一安全的 HTML 标记的 HTML 代码 (例如，有没有&lt;脚本&gt;标记)。 若要执行此操作，可以使用[Microsoft Web Protection Library](https://www.nuget.org/packages/AntiXSS)。
7. 再次编辑该产品。 在名称字段中键入 HTML 代码，然后单击**保存**。 请注意，说明字段中仅禁用请求验证并重新字段的其余部分仍验证针对具有潜在危险的内容。

    ![请求验证其余字段中启用](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "请求验证其余字段中启用")

    *在其余字段中启用请求验证*

    ASP.NET Web 窗体 4.5 包括新的请求验证模式下惰式执行请求验证。 请求验证模式设置为**4.5**，如果一段代码访问*Request.Form [&quot;密钥&quot;]*，ASP.NET 4.5 请求验证将仅触发器请求验证该窗体集合中的特定元素。

    此外，ASP.NET 4.5 现在包括核心编码例程从 Microsoft ANTI-XSS 库版本 4.0。 防 XSS 编码例程所实现的新*AntiXssEncoder*类型位于新**System.Web.Security.AntiXss**命名空间。 与**encoderType**配置为使用的参数*AntiXssEncoder*，自动编码在 ASP.NET 中使用新的编码例程，所有输出。
8. ASP.NET 4.5 请求验证还支持对请求数据未经过验证的访问。 ASP.NET 4.5 中添加到新集合属性**HttpRequest**对象调用**Unvalidated**。 导航到**HttpRequest.Unvalidated**有权访问的所有请求数据，包括窗体、 Querystring、 Cookie、 Url 和等等的公共部分。

    ![Request.Unvalidated 对象](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "Request.Unvalidated 对象")

    *Request.Unvalidated 对象*

    > [!NOTE]
    > **请谨慎使用 HttpRequest.Unvalidated 属性 ！** 请确保仔细对原始请求数据，以确保危险文本未往返和呈现回毫无戒心的客户执行自定义验证 ！

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a>练习 3： 异步页处理在 ASP.NET Web 窗体

在此练习中，将向你介绍新的异步页处理 ASP.NET Web 窗体中的功能。

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a>任务 1-更新产品详细信息页面上传并显示图像

在本任务中，你将更新产品详细信息页，以允许用户指定产品的图像 URL 并将其显示在只读视图。 通过以同步方式下载，将创建指定的图像的本地副本。 在下一任务中，你将更新此实现，使其以异步方式工作。

1. 打开**Visual Studio 2012**并加载**开始**解决方案位于**Source\Ex3 Async\Begin**从本实验的文件夹。 或者，您可以从上一练习在现有解决方案上继续工作。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 为此，请在解决方案资源管理器中，单击**WebFormsLab**项目，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 打开**ProductDetails.aspx**页上源，以显示产品图像的 FormView 的 ItemTemplate 中添加一个字段。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. 添加字段以在 FormView 的 EditTemplate 中指定图像 URL。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. 打开**ProductDetails.aspx.cs**代码隐藏文件，并添加以下命名空间指令。

    (代码段- *Web 窗体实验室-Ex03-命名空间*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. 创建**UpdateProductImage**方法将远程图像存储在本地**映像**文件夹，然后更新 product 实体与新的图像位置值。

    (代码段- *Web 窗体实验室-Ex03-UpdateProductImage*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. 更新**UpdateProduct**方法来调用**UpdateProductImage**方法。

    (代码段- *Web 窗体实验室-Ex03-UpdateProductImage 调用*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. 运行应用程序并尝试上传的映像的产品。 例如，可以使用 Office 剪贴画中的以下映像 URL: [[http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)

    ![设置产品的映像](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "设置产品的图像")

    *设置产品的图像*

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a>任务 2-添加异步处理到产品详细信息页

在本任务中，你将更新产品详细信息页，使其以异步方式工作。 将使用 ASP.NET 4.5 异步页处理，从而提高长时间运行任务-映像下载过程的性能。

Web 应用程序中的异步方法可用于优化 ASP.NET 线程池的使用的方式。 在 ASP.NET 中存在是有限的数量的不顾及在线程池中的线程请求，因此时所有线程都处于忙碌状态，, ASP.NET 开始拒绝新请求、 发送应用程序错误消息并将你的站点不可用。

在网站上耗时的操作都非常适合进行异步编程，因为它们所分配的线程占用很长时间。 这包括长时间运行的请求，具有大量不同的元素的页和页需要脱机操作中，将此类查询的数据库或访问外部 web 服务器。 优点是处理页面时，这些操作使用异步方法，如果线程被释放并返回到线程池，用于处理新的页面请求。 这意味着，页面才会开始在线程池从一个线程中处理和异步处理完成后，可能会完成在一个不同的处理。

1. 打开**ProductDetails.aspx**页。 添加**异步**属性中**页面**元素并将其设置为**true**。 此属性告知 ASP.NET 实现 IHttpAsyncHandler 接口。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. 要显示的线程正在运行页的详细信息的页的底部添加一个标签。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. 打开**ProductDetails.aspx.cs**并添加以下命名空间指令。

    (代码段- *Web 窗体实验室-Ex03-命名空间 2*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. 修改**UpdateProductImage**方法以下载具有一个异步任务的图像。 将替换**WebClient** **DownloadFile**方法替换**DownloadFileTaskAsync**方法，包括**await**关键字。

    (代码段- *Web 窗体实验室-Ex03-UpdateProductImage 异步*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    RegisterAsyncTask 注册新的页面异步任务要执行的另一个线程。 它将接收要执行的任务 (t) 的 lambda 表达式。 **Await**中的关键字**DownloadFileTaskAsync**方法将转换后，将异步调用的回调方法的剩余部分**DownloadFileTaskAsync**方法完成。 ASP.NET 将恢复自动维护所有原始 HTTP 请求值的方法的执行。 在.NET 4.5 中的新异步编程模型，可编写异步代码，看上去非常类似于同步代码，并让编译器处理回调函数或延续代码的复杂性。
    > [!NOTE]
    > RegisterAsyncTask 和 PageAsyncTask 自.NET 2.0 以来已可用。 Await 关键字新从.NET 4.5 的异步编程模型，可与.NET WebClient 对象的新 TaskAsync 方法一起使用。
5. 添加代码以显示的线程的代码在其启动和完成执行。 若要执行此操作，更新**UpdateProductImage**用下面的代码的方法。

    (代码段- *Web 窗体实验室-Ex03-显示线程*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. 打开网站的**Web.config**文件。 添加以下 appSetting 变量。

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. 按**F5**运行应用程序并将该产品的图像上传。 请注意，启动和完成的代码可能不同的线程 ID。 这是因为从 ASP.NET 线程池的单独线程上运行的异步任务。 完成任务后，ASP.NET 将任务放回队列中，并将分配任何可用的线程。

    ![以异步方式下载图像](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "异步下载图像")

    *以异步方式下载图像*

> [!NOTE]
> 此外，您可以此应用程序部署到 Azure 的以下[附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署](#AppendixB)。


* * *

<a id="Summary"></a>
## <a name="summary"></a>总结

在此动手实验中，已分析并演示以下概念：

- 使用强类型化数据绑定表达式
- 在 Web 窗体中使用新的模型绑定功能
- 将值提供程序用于将页面数据映射到代码隐藏方法
- 用户输入验证中使用数据注释
- 在 Web 窗体中执行 advange unobstrusive 使用 jQuery 的客户端验证
- 实现粒度请求验证
- 实现在 Web 窗体中处理的异步页面

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 a： 安装 Visual Studio Express 2012 for Web

你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**. 以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。

1. 转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Azure SDK</em>&quot;。
2. 单击**立即安装**。 如果还没有**Web 平台安装程序**将重定向以下载并安装。
3. 一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。

    ![安装 Visual Studio Express](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，然后单击**我接受**以继续。

    ![接受许可条款](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    *接受许可条款*
5. 等待，直到下载和安装过程完成。

    ![安装进度](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    *安装进度*
6. 安装完成后，单击**完成**。

    ![安装已完成](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    *安装已完成*
7. 单击**退出**以关闭 Web 平台安装程序。
8. 若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。

    ![VS Express for Web 磁贴](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    *VS Express for Web 磁贴*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署

本附录将演示如何从 Azure 门户创建新的网站和发布应用程序获取按照本实验中，利用 Azure 提供的 Web 部署发布功能。

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>任务 1-从 Azure 门户创建新的 Web 站点

1. 转到[Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。

    > [!NOTE]
    > 借助 Azure 可以免费托管 10 个 ASP.NET 网站，然后随着流量增长情况。 你可以注册[此处](http://aka.ms/aspnet-hol-azure)。

    ![登录到 Windows Azure 门户](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "登录到 Windows Azure 门户")

    *登录到门户*
2. 单击**新建**命令栏上。

    ![创建新的 Web 站点](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "创建新的 Web 站点")

    *创建新的 Web 站点*
3. 单击**计算** | **网站**。 然后选择**快速创建**选项。 为新网站提供可用的 URL，然后单击**创建网站**。

    > [!NOTE]
    > Azure 是可以控制和管理在云中运行的 web 应用程序的主机。 快速创建选项，可部署到 Azure 门户外部的已完成的 web 应用程序。 它不包括用于设置数据库的步骤。

    ![创建新的网站使用快速创建](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "创建新的网站使用快速创建")

    *创建新的网站使用快速创建*
4. 等到新**网站**创建。
5. 创建网站后，单击下面的链接**URL**列。 检查新的 Web 站点正常工作。

    ![浏览到新的 web 站点](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "浏览到新的 web 站点")

    *浏览到新的 web 站点*

    ![正在运行的网站](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "正在运行的网站")

    *正在运行的网站*
6. 返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。

    ![打开网站管理页](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "打开网站管理页")

    *打开网站管理页*
7. 在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。

    > [!NOTE]
    > *发布配置文件*包含所有发布到 Azure 的 web 应用程序为每个启用的发布方法所需的信息。 发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。 **Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Azure。

    ![正在下载网站发布配置文件](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "下载网站发布配置文件")

    *正在下载网站发布配置文件*
8. 下载发布配置文件到已知位置。 进一步在此练习中将了解如何使用此文件发布到 Azure 的 web 应用程序从 Visual Studio。

    ![保存发布配置文件](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "保存发布配置文件")

    *保存发布配置文件*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。 如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。

1. 用于存储应用程序数据库，将需要 SQL 数据库服务器。 可以从在 Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**. 如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。 请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。 不创建数据库，因为它将在后面的阶段中创建。

    ![SQL 数据库服务器仪表板](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database 服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。 若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框中，然后单击![add-client-ip-address-ok-button](whats-new-in-web-forms-in-aspnet-45/_static/image39.png)按钮。

    ![添加客户端 IP 地址](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    *添加客户端 IP 地址*
3. 一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。

    ![确认更改](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    *确认更改*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布

1. 返回到 ASP.NET MVC 4 解决方案。 在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。

    ![发布应用程序](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "发布应用程序")

    *发布此网站*
2. 导入发布配置文件保存在第一个任务。

    ![导入发布配置文件](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击**验证连接**。 验证完成后单击**下一步**。

    > [!NOTE]
    > 请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。

    ![验证连接](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "验证连接")

    *验证连接*
4. 在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。

    ![Web 部署配置](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web 部署配置")

    *Web 部署配置*
5. 配置数据库连接，如下所示：

   - 在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。
   - 在中**用户名**键入服务器管理员登录名。
   - 在中**密码**键入服务器管理员登录密码。
   - 键入新的数据库名称。

     ![配置目标连接字符串](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "配置目标连接字符串")

     *配置目标连接字符串*
6. 然后单击“确定” 。 当系统提示你创建数据库时，单击**是**。

    ![创建数据库](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。 然后，单击 **“下一步”**。

    ![连接字符串指向 SQL 数据库](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "指向 SQL 数据库连接字符串")

    *连接字符串指向 SQL 数据库*
8. 在中**预览版**页上，单击**发布**。

    ![Web 应用程序发布](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "发布 web 应用程序")

    *Web 应用程序发布*
9. 在发布过程完成后，在默认浏览器将打开已发布的网站。

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>附录 c： 使用代码片段

使用代码段，可以轻松获得相关所需的所有代码。 实验室文档将告诉您完全何时可以使用它们，如下图中所示。

![使用 Visual Studio 代码段代码插入到你的项目](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "使用 Visual Studio 代码段代码插入到你的项目")

*使用 Visual Studio 代码段代码插入到你的项目*

***若要添加代码段使用键盘 (仅限 C#)***

1. 将光标置于要插入的代码。
2. 开始键入代码片段名称 （不带空格或连字符）。
3. 观看作为 IntelliSense 显示匹配的代码段的名称。
4. 选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。
5. 按 Tab 键两次，以在光标位置插入代码段。

![开始键入代码段名称](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "开始键入代码段名称")

*开始键入代码段名称*

![按 tab 键以选择突出显示代码段](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "按选项卡以选择突出显示代码段")

*按 tab 键以选择突出显示代码段*

![再次按 Tab 和代码段将 expand](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "再次按 Tab 和代码段将扩展")

*再次按 Tab 和代码段将扩展*

***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。 右键单击你想要插入的代码片段。

1. 选择**插入代码段**跟**我的代码片段**。
2. 通过单击选择列表中中的相关代码片段。

![右键单击你想要插入代码段和选择插入代码段](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "右键单击你想要插入代码段和选择插入代码段")

*右键单击你想要插入代码段和选择插入代码段*

![通过单击选择列表中中的相关代码片段](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "通过单击选择列表中中的相关代码片段")

*通过单击选择列表中中的相关代码片段*
