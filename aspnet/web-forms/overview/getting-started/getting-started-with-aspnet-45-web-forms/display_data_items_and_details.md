---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 显示数据项和详细信息 |Microsoft Docs
author: Erikre
description: 本教程系列将指导您学习生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: aspnetcontent
ms.date: 09/08/2014
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 083f7182416012c85f05db255fcab4d8e535b52a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820342"
---
<a name="display-data-items-and-details"></a>显示数据项和详细信息
====================
通过[Erik Reitan](https://github.com/Erikre)

[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 此教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。 Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)可随附于本系列教程。


本教程介绍如何显示数据项和使用 ASP.NET Web 窗体和 Entity Framework Code First 数据项详细信息。 本教程基于上一教程"UI 和导航"，而是 Wingtip Toy 存储教程系列的一部分。 完成本教程后，你将能够查看产品上*ProductsList.aspx*页，以及详细信息上的各个产品*ProductDetails.aspx*页。

## <a name="what-youll-learn"></a>你将学习：

- 如何添加数据控件用于显示数据库中的产品。
- 如何连接到所选数据的数据控件。
- 如何添加用来显示产品详细信息，从数据库的数据控件。
- 了解如何从查询字符串中检索值并使用该值来限制从数据库中检索的数据。

### <a name="these-are-the-features-introduced-in-the-tutorial"></a>以下是本教程中引入的功能：

- 模型绑定
- 值提供程序

## <a name="adding-a-data-control-to-display-products"></a>添加用来显示产品的数据控件

当数据绑定到服务器控件，有几个不同选项，可以使用。 最常用的选项包括添加数据源控件、 添加代码，或使用模型绑定。

### <a name="using-a-data-source-control-to-bind-data"></a>使用数据源控件以将数据绑定

添加数据源控件，可将数据源控件链接到显示的数据的控件。 此方法允许你以声明方式服务器端控件直接连接到数据源，而不是使用编程方法。

### <a name="coding-by-hand-to-bind-data"></a>手动编写代码以将数据绑定

添加通过手动代码涉及到读取的值、 检查 null 值、 尝试将其转换为适当的类型、 检查转换是否成功，和最后，在查询中使用的值。 当您需要保留对数据访问逻辑的完全控制时，可以使用此方法。

### <a name="using-model-binding-to-bind-data"></a>使用模型绑定将数据绑定

使用模型绑定，可将使用很少的代码的结果绑定，并使你能够重复使用在整个应用程序的功能。 模型绑定的目标是简化使用代码为中心的数据访问逻辑，同时保留一个丰富的数据绑定框架的好处。

## <a name="displaying-products"></a>显示产品

在本教程中，您将使用模型绑定将数据绑定。 若要配置以使用模型绑定选择数据的数据控件，设置控件的`SelectMethod`属性设置为在页面的代码中方法的名称。 数据控件在页生命周期中的适当时间调用的方法，并自动将绑定返回的数据。 无需显式调用`DataBind`方法。

使用以下步骤，将修改中的标记*ProductList.aspx*页，以便可显示产品。

1. 在中**解决方案资源管理器**，打开*ProductList.aspx*页。
2. 现有标记替换为以下标记：   

    [!code-aspx[Main](display_data_items_and_details/samples/sample1.aspx)]

此代码使用**ListView**控件命名为"productList"若要显示的产品。

[!code-aspx[Main](display_data_items_and_details/samples/sample2.aspx)]

**ListView**控件通过使用模板和样式定义的格式显示数据。 它可用于任何重复结构中的数据。 这**ListView**示例只是显示了从数据库中，但是可以让用户可以编辑、 插入和删除数据，并进行排序和页面数据，不需代码的数据。

通过设置`ItemType`中的属性**ListView**控件，数据绑定表达式`Item`可用和控件将成为强类型化。 在上一教程中所述，可以选择使用 IntelliSense，例如，指定的项对象的详细信息`ProductName`:

![显示数据的项和详细信息-IntelliSense](display_data_items_and_details/_static/image1.png)

此外，您使用模型绑定程序指定`SelectMethod`值。 此值 (`GetProducts`) 将对应于将添加到代码隐藏来显示产品下一步中的方法。

### <a name="adding-code-to-display-products"></a>添加代码以显示产品

在此步骤中，将添加代码以填充**ListView**产品数据库中的数据的控件。 该代码将支持通过单个类别，以及显示所有产品都显示产品。

1. 在中**解决方案资源管理器**，右键单击*ProductList.aspx* ，然后单击**查看代码**。
2. 中的现有代码替换*ProductList.aspx.cs*文件使用以下代码：   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

此代码演示`GetProducts`引用的方法`ItemType`属性**ListView**控制*ProductList.aspx*页。 若要将结果限制为在数据库中的特定类别，该代码将设置`categoryId`值从查询字符串值传递给*ProductList.aspx*时页*ProductList.aspx*页导航到。 `QueryStringAttribute`类中`System.Web.ModelBinding`命名空间用于检索查询字符串变量 id 的值。这会指示要尝试将值绑定到查询字符串中的模型绑定`categoryId`在运行时参数。

有效的类别作为查询字符串传递给页上，当查询的结果被限制为匹配数据库中这些产品`categoryId`值。 例如，如果到 URL *ProductsList.aspx*页是以下：

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

页面仅显示产品其中`category`等于`1`。

导航到时，如果没有查询字符串包含*ProductList.aspx*页上，将显示所有产品。

这些方法的值的源嘿 *值提供程序*(如*查询字符串*)，指示要使用的值提供程序的参数属性称为值提供程序属性 (如"`id`")。 ASP.NET Web 窗体应用程序，例如查询字符串、 cookie、 窗体值、 控件、 视图状态，会话状态和配置文件属性中包含值提供程序和所有典型的资源，用户输入的相应属性。 此外可以编写自定义值提供程序。

### <a name="running-the-application"></a>运行应用程序

运行应用程序现在，请参阅如何查看所有产品或只是一组有限的按类别的产品。

1. 在中**解决方案资源管理器**，右键单击*Default.aspx*页，然后选择**用浏览器查看**。  
 在浏览器将打开并显示*Default.aspx*页。
2. 选择**汽车**产品类别导航菜单中。  
 *ProductList.aspx*显示仅"Cars"类别中包含的产品显示页。 稍后在本教程中，将显示产品详细信息。  

    ![显示数据的项和详细信息-汽车](display_data_items_and_details/_static/image2.png)
3. 选择**产品**从顶部导航菜单。  
 同样， *ProductList.aspx*页将显示，但这次它显示了产品的完整列表。   

    ![显示数据的项和详细信息-产品](display_data_items_and_details/_static/image3.png)
4. 关闭浏览器并返回到 Visual Studio。

### <a name="adding-a-data-control-to-display-product-details"></a>添加一个数据控件来显示产品详细信息

接下来，将修改中的标记*ProductDetails.aspx*以便页面可以显示各个产品的信息添加上一教程中的页。

1. 在中**解决方案资源管理器**，打开*ProductDetails.aspx*页。
2. 现有标记替换为以下标记：   

    [!code-aspx[Main](display_data_items_and_details/samples/sample5.aspx)]

此代码使用**FormView**控件来显示有关单个产品的详细信息。 此标记使用方法，如用于显示数据中的那些*ProductList.aspx*页。 **FormView**控件用于从数据源一次显示一条记录。 当你使用**FormView**控件，您创建模板来显示和编辑数据绑定值。 这些模板包含，绑定表达式和格式设置用于定义控件的外观和功能的窗体。

若要连接到数据库的更高版本的标记，必须添加到其他代码*ProductDetails.aspx*代码。

1. 在中**解决方案资源管理器**，右键单击*ProductDetails.aspx* ，然后单击**查看代码**。  
   *ProductDetails.aspx.cs*文件将会显示。
2. 用下面的代码替换现有代码：   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

此代码检查"`productID`"查询字符串值。 如果找到有效的查询字符串值，则将显示匹配的产品。 如果不找到任何查询字符串，或查询字符串值无效，没有任何产品显示在*ProductDetails.aspx*页。

### <a name="running-the-application"></a>运行应用程序

现在可以运行应用程序以查看显示的各个产品根据产品的 id。

1. 按**F5**在 Visual Studio 运行应用程序中。  
 在浏览器将打开并显示*Default.aspx*页。
2. 从类别导航菜单中选择"船"。  
 *ProductList.aspx*显示页。
3. 从产品列表中选择"纸张船"产品。  
 *ProductDetails.aspx*显示页。   

    ![显示数据的项和详细信息-产品](display_data_items_and_details/_static/image4.png)
4. 关闭浏览器。

## <a name="summary"></a>总结

在本教程中的一系列已添加标记和代码以显示产品列表并显示产品详细信息。 在此过程介绍了有关强类型化的数据控件、 模型绑定和值提供程序。 在下一步的教程中，你将在 Wingtip Toys 示例应用程序中添加购物车。

## <a name="additional-resources"></a>其他资源

[检索和使用模型绑定和 web 窗体显示数据](../../presenting-and-managing-data/model-binding/retrieving-data.md)

> [!div class="step-by-step"]
> [上一页](ui_and_navigation.md)
> [下一页](shopping-cart.md)
