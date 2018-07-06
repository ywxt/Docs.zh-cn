---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb
title: 限制数据修改功能基于用户 (VB) |Microsoft Docs
author: rick-anderson
description: 允许用户编辑数据的 web 应用程序，在不同的用户帐户可能具有不同数据编辑权限。 在本教程中我们将介绍如何 t...
ms.author: aspnetcontent
ms.date: 07/17/2006
ms.assetid: 9dc264a6-feb8-474b-8b91-008c50708065
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb
msc.type: authoredcontent
ms.openlocfilehash: 23e23c288ccceab7f7e1c07aa9a902bef4045de0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37836799"
---
<a name="limiting-data-modification-functionality-based-on-the-user-vb"></a>限制基于用户 (VB) 的数据修改功能
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_23_VB.exe)或[下载 PDF](limiting-data-modification-functionality-based-on-the-user-vb/_static/datatutorial23vb1.pdf)

> 允许用户编辑数据的 web 应用程序，在不同的用户帐户可能具有不同数据编辑权限。 在本教程中我们将介绍如何动态调整基于来访的用户的数据修改功能。


## <a name="introduction"></a>介绍

许多 web 应用程序支持用户帐户，并提供不同的选项、 报表和基于登录用户的功能。 例如，与我们的教程我们可能想要允许用户登录到有关其产品的其名称和每个单元，数量的网站和更新的常规信息可能是-以及供应商信息，例如其公司名称、 供应商公司地址、 联系人的信息和等等。 此外，我们可能想要从我们公司的人员包括一些用户帐户，以便他们可以登录和更新产品信息一样上纸、 单位再订购量，等等。 我们的 web 应用程序可能还允许匿名用户访问 （用户未登录），但将它们限制为只需查看的数据。 与此类用户帐户中的系统位置，我们将在我们的 ASP.NET 页面提供插入、 编辑和删除功能适用于当前登录的用户希望数据 Web 控件。

在本教程中我们将介绍如何动态调整基于来访的用户的数据修改功能。 具体而言，我们将创建一个 GridView，列出的供应商提供的产品以及可编辑 DetailsView 中显示的供应商信息的页面。 如果用户访问的页面是从我们的公司，他们可以： 查看供应商 s 的任何信息;编辑其地址;和编辑任何产品的供应商提供的信息。 如果，但是，用户是从特定的公司，他们可以只查看和编辑他们自己的地址信息和只能编辑不标记为已停止使用其产品。


[![我们的公司中的用户可以编辑任何供应商的信息](limiting-data-modification-functionality-based-on-the-user-vb/_static/image2.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image1.png)

**图 1**： 从我们公司可以编辑任何供应商的信息的用户 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image3.png))


[![中的特定供应商仅可以查看和编辑其信息的用户](limiting-data-modification-functionality-based-on-the-user-vb/_static/image5.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image4.png)

**图 2**： 从特定供应商可以仅查看和编辑其信息的用户 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image6.png))


让我们来开始 ！

> [!NOTE]
> ASP.NET 2.0 成员身份系统提供用于创建、 管理和验证用户帐户的标准化的可扩展平台。 由于超出这些教程的作用域的成员资格系统检查，本教程中改为"fakes"成员身份通过允许匿名访问者可以选择它们是否来自特定供应商或从我们的公司。 有关成员身份的详细信息，请参阅我[检查 ASP.NET 2.0 s 成员资格、 角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)文章系列。


## <a name="step-1-allowing-the-user-to-specify-their-access-rights"></a>步骤 1： 允许用户指定他们的访问权限

在实际的 web 应用程序中，用户的帐户信息将包括是否它们的工作为我们的公司或特定供应商和用户登录到站点后会将可从我们的 ASP.NET 页面以编程方式访问此信息。 作为用户级帐户信息通过配置文件系统中，或通过某些自定义方式，可以通过 ASP.NET 2.0 角色系统，捕获此信息。

由于本教程的目的是演示调整根据登录用户的数据修改功能，并且并不意味着展示 ASP.NET 2.0 s 成员资格、 角色和配置文件系统，我们将使用进行非常简单的机制来确定用户访问页-从该用户可以指示是否他们应能够查看和编辑任何供应商或信息，或者，什么 DropDownList 的功能特定供应商的信息他们可以查看和编辑。 如果用户指出她可以查看和编辑所有供应商信息 （默认值），她可以翻页查看所有供应商、 编辑任何供应商的地址信息，并编辑名称和每个单位的所选的供应商提供的任何产品的数量。 如果用户指出她只能查看和编辑特定供应商，但是，然后她可以仅查看该一个供应商的详细信息和产品，并且只能更新名称和每个单位信息的产品数量*不*停用。

然后，在本教程中，我们第一步是创建此 DropDownList 并填充其供应商系统中。 打开`UserLevelAccess.aspx`页中`EditInsertDelete`文件夹中，添加 DropDownList 其`ID`属性设置为`Suppliers`，并将此 DropDownList 绑定到名为新 ObjectDataSource `AllSuppliersDataSource`。


[![创建名为 AllSuppliersDataSource 新 ObjectDataSource](limiting-data-modification-functionality-based-on-the-user-vb/_static/image8.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image7.png)

**图 3**： 创建新对象数据源命名`AllSuppliersDataSource`([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image9.png))


因为我们希望此 DropDownList 以包括所有供应商，配置要调用的 ObjectDataSource`SuppliersBLL`类的`GetSuppliers()`方法。 此外确保 ObjectDataSource s`Update()`方法映射到`SuppliersBLL`类的`UpdateSupplierAddress`方法中，为此 ObjectDataSource 将还使用我们将在步骤 2 中添加的 DetailsView。

完成 ObjectDataSource 向导后，通过配置完成的步骤`Suppliers`DropDownList，使之显示`CompanyName`数据字段，并使用`SupplierID`为每个值的数据字段`ListItem`。


[![配置供应商 DropDownList，若要使用的公司名称和供应商数据字段](limiting-data-modification-functionality-based-on-the-user-vb/_static/image11.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image10.png)

**图 4**： 配置`Suppliers`使用 DropDownList`CompanyName`并`SupplierID`数据字段 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image12.png))


此时，下拉列表列出了在数据库中的供应商的公司名称。 但是，我们还需要包括"显示/编辑所有供应商"选项向 DropDownList。 若要完成此操作，设置`Suppliers`DropDownList s`AppendDataBoundItems`属性设置为`true`，然后添加`ListItem`其`Text`属性是"显示/编辑所有供应商"和其值是`-1`。 这可以直接通过声明性标记或通过添加在设计器通过转到属性窗口，并单击 DropDownList s 中的省略号`Items`属性。

> [!NOTE]
> 回头[*母版/详细信息筛选与 DropDownList* ](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md)教程，了解将选择所有项目都添加到数据绑定 DropDownList 的更多详细讨论。


之后`AppendDataBoundItems`已设置属性和`ListItem`添加，DropDownList s 声明性标记应如下所示：


[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample1.aspx)]

通过浏览器查看时，图 5 显示了我们当前进度的屏幕截图。


[![供应商 DropDownList 包含显示所有列表项，以及一个用于每个供应商](limiting-data-modification-functionality-based-on-the-user-vb/_static/image14.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image13.png)

**图 5**: `Suppliers` DropDownList 包含显示所有`ListItem`，以及一个用于每个供应商 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image15.png))


由于我们想要用户具有更改其选择后立即更新用户界面，设置`Suppliers`DropDownList s`AutoPostBack`属性设置为`true`。 在步骤 2 中，我们将创建将显示供应商必须基于对 DropDownList 所选内容的信息的 DetailsView 控件。 然后，在步骤 3 中，我们将创建事件处理程序的此 DropDownList 的`SelectedIndexChanged`事件，我们将添加代码，将相应的供应商信息绑定到 DetailsView 基于所选的供应商。

## <a name="step-2-adding-a-detailsview-control"></a>步骤 2： 添加 DetailsView 控件

让我们来使用 DetailsView 显示供应商信息。 为了让用户可以查看和编辑所有供应商的人员，DetailsView 就将支持分页，从而允许用户一次单步执行供应商信息一条记录。 如果用户适用于特定供应商，但是，DetailsView 将显示仅该特定供应商的信息，并且不会包括分页界面。 在任一情况下，DetailsView 需要允许用户编辑供应商的地址、 城市和国家/地区字段。

向下页面添加 DetailsView`Suppliers`下拉列表中，设置其`ID`属性设置为`SupplierDetails`，并将其绑定到`AllSuppliersDataSource`在上一步中创建对象数据源。 接下来，请从 DetailsView s 智能标记的启用分页和启用编辑复选框。

> [!NOTE]
> 如果 don t 看到智能的 DetailsView s 中的启用编辑选项标记它 s 因为未映射的 ObjectDataSource s`Update()`方法`SuppliersBLL`类的`UpdateSupplierAddress`方法。 请花费片刻时间以返回并进行此配置更改，此后启用编辑选项应会出现在 DetailsView s 智能标记。


由于`SuppliersBLL`类 s`UpdateSupplierAddress`方法只接受四个参数- `supplierID`， `address`， `city`，和`country`-修改 DetailsView 的 BoundFields 以便`CompanyName`和`Phone`BoundFields 是只读的。 此外，删除`SupplierID`BoundField 完全。 最后， `AllSuppliersDataSource` ObjectDataSource 当前具有其`OldValuesParameterFormatString`属性设置为`original_{0}`。 请花费片刻时间从声明性语法完全删除此属性设置或将其设置为默认值为`{0}`。

配置后`SupplierDetails`DetailsView 和`AllSuppliersDataSource`ObjectDataSource，我们将具有以下声明性标记：


[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample2.aspx)]

现在可以通过分页 DetailsView 和可更新的所选供应商的地址信息，而不考虑中所做的选择`Suppliers`DropDownList （请参阅图 6）。


[![可以查看任何供应商的信息，并更新其地址](limiting-data-modification-functionality-based-on-the-user-vb/_static/image17.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image16.png)

**图 6**: Any 供应商可以查看信息，并更新其地址 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image18.png))


## <a name="step-3-displaying-only-the-selected-supplier-s-information"></a>步骤 3： 显示所选供应商的 s 信息

我们的页面当前显示的信息而不考虑特定供应商是否已从选择的所有供应商`Suppliers`DropDownList。 为了显示只是所选的供应商的供应商信息，我们需要将另一个对象数据源添加到我们的页面，一个用于检索有关特定供应商的信息。

将新对象数据源添加到页上，其命名为`SingleSupplierDataSource`。 从其智能标记上，单击配置数据源链接并让其使用`SuppliersBLL`类的`GetSupplierBySupplierID(supplierID)`方法。 如同`AllSuppliersDataSource`ObjectDataSource，具有`SingleSupplierDataSource`ObjectDataSource s`Update()`方法映射到`SuppliersBLL`类的`UpdateSupplierAddress`方法。


[![配置 SingleSupplierDataSource ObjectDataSource 使用 GetSupplierBySupplierID(supplierID) 方法](limiting-data-modification-functionality-based-on-the-user-vb/_static/image20.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image19.png)

**图 7**： 配置`SingleSupplierDataSource`使用 ObjectDataSource`GetSupplierBySupplierID(supplierID)`方法 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image21.png))


接下来，我们重新提示指定的参数源`GetSupplierBySupplierID(supplierID)`s 方法`supplierID`输入的参数。 由于我们想要显示的信息从下拉列表中，使用所选的供应商`Suppliers`DropDownList 的`SelectedValue`作为参数源属性。


[![使用供应商 DropDownList 作为供应商 Id 参数源](limiting-data-modification-functionality-based-on-the-user-vb/_static/image23.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image22.png)

**图 8**： 使用`Suppliers`作为 DropDownList`supplierID`参数源 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image24.png))


即使使用添加此第二个 ObjectDataSource，DetailsView 控件当前已配置为始终使用`AllSuppliersDataSource`对象数据源。 我们需要添加逻辑以调整数据源使用的具体取决于 DetailsView `Suppliers` DropDownList 项选择。 若要实现此目的，创建`SelectedIndexChanged`供应商 DropDownList 的事件处理程序。 通过双击设计器中的 DropDownList 可以非常轻松地创建此功能。 此事件处理程序需要能够确定要使用哪些数据源，必须重新绑定到 DetailsView 数据。 这是使用以下代码来实现：


[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample3.vb)]

事件处理程序开始通过确定是否选择了"显示/编辑所有供应商"选项。 如果是，它会设置`SupplierDetails`DetailsView s`DataSourceID`到`AllSuppliersDataSource`，并返回到供应商提供的集中的第一条记录的用户，通过设置`PageIndex`属性设为 0。 如果，但是，用户已选择特定供应商，从下拉列表中，DetailsView s`DataSourceID`分配给`SingleSuppliersDataSource`。 无论什么数据源使用，`SuppliersDetails`模式下恢复回只读模式和数据重新绑定到 DetailsView 通过调用`SuppliersDetails`控制的`DataBind()`方法。

使用就地此事件处理程序，DetailsView 控件现在显示所选的供应商，除非选择了"显示/编辑所有供应商"选项，所有供应商可以在这种情况下进行查看通过分页界面。 图 9 显示的页选择了;"显示/编辑所有供应商"选项请注意，分页界面，这样就允许用户访问和更新任何供应商。 图 10 显示与所选佳佳供应商的页。 仅佳佳的信息在此情况下是可查看和编辑。


[![您可以查看和编辑所有供应商信息](limiting-data-modification-functionality-based-on-the-user-vb/_static/image26.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image25.png)

**图 9**： 所有供应商的信息可以查看和编辑 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image27.png))


[![仅将所选供应商的信息都可以查看和编辑](limiting-data-modification-functionality-based-on-the-user-vb/_static/image29.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image28.png)

**图 10**： 仅选择供应商的信息可以查看和编辑 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image30.png))


> [!NOTE]
> 对于本教程，DropDownList 和 DetailsView 控件 s`EnableViewState`必须设置为`true`（默认值） 因为 DropDownList s`SelectedIndex`和 DetailsView 的`DataSourceID`属性的更改必须记住在回发之间。


## <a name="step-4-listing-the-suppliers-products-in-an-editable-gridview"></a>步骤 4： 列出了所有可编辑的 GridView 中的供应商产品

在 DetailsView 完成的情况下，我们下一步是包含可编辑的 GridView，其中列出了所选的供应商提供的那些产品。 此 GridView 应允许对唯一编辑`ProductName`和`QuantityPerUnit`字段。 此外，如果用户访问的页面是从特定供应商，它应仅允许将这些产品的更新*不*停止使用。 若要完成此我们将需要首先将添加的重载`ProductsBLL`类 s`UpdateProducts`采用的方法只需`ProductID`， `ProductName`，和`QuantityPerUnit`作为输入的字段。 我们已在许多教程，事先阶梯完成此过程让 s 只需查看下面的代码，应将其添加到`ProductsBLL`:


[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample4.vb)]

使用此我们准备就绪后添加 GridView 控件和其关联的 ObjectDataSource 重载创建， 向页面添加一个新的 GridView、 设置其`ID`属性设置为`ProductsBySupplier`，并将其配置为使用名为新 ObjectDataSource `ProductsBySupplierDataSource`。 因为我们希望此 GridView，其中列出所选的供应商的那些产品，使用`ProductsBLL`类的`GetProductsBySupplierID(supplierID)`方法。 此外将映射`Update()`方法对新`UpdateProduct`我们刚刚创建的重载。


[![配置对象数据源以使用刚刚创建的 UpdateProduct 重载](limiting-data-modification-functionality-based-on-the-user-vb/_static/image32.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image31.png)

**图 11**： 配置为使用 ObjectDataSource`UpdateProduct`重载只是创建 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image33.png))


我们重新提示你选择的参数源`GetProductsBySupplierID(supplierID)`s 方法`supplierID`输入的参数。 由于我们想要显示的产品的供应商中 DetailsView，使用所选`SuppliersDetails`DetailsView 控件的`SelectedValue`作为参数源属性。


[![SuppliersDetails DetailsView 的 SelectedValue 属性用作参数源](limiting-data-modification-functionality-based-on-the-user-vb/_static/image35.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image34.png)

**图 12**： 使用`SuppliersDetails`DetailsView s`SelectedValue`作为参数源属性 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image36.png))


返回到 GridView，删除所有的 GridView 字段除外`ProductName`， `QuantityPerUnit`，并`Discontinued`、 标记`Discontinued`CheckBoxField 为只读的。 另外，检查 GridView s 智能标记中的启用编辑选项。 在进行这些更改后，GridView 和 ObjectDataSource 的声明性标记应类似于下面：


[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample5.aspx)]

与我们以前的 Objectdatasource 这一个 s 一样`OldValuesParameterFormatString`属性设置为`original_{0}`，尝试更新产品的名称或单位数量时，这将导致问题。 从声明性语法中完全删除此属性或将其设置为其默认值， `{0}`。

完成此配置后，我们的页面现在列出在 GridView 中选定的供应商提供的产品 （请参阅图 13）。 目前*任何*可以更新产品的名称或每个单位的数量。 但是，我们需要更新我们的页面逻辑，以便对用户与特定供应商相关联的停产的产品禁止的此类功能。 我们将解决此步骤 5 中的最后一个部分。


[![显示所选供应商提供的产品](limiting-data-modification-functionality-based-on-the-user-vb/_static/image38.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image37.png)

**图 13**： 显示产品的所选供应商提供 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image39.png))


> [!NOTE]
> 添加了此可编辑的 GridView `Suppliers` DropDownList 的`SelectedIndexChanged`应更新事件处理程序，以返回到只读状态的 GridView。 否则，如果在编辑产品信息选择不同的供应商，则新的供应商 GridView 中相应的索引也将可编辑。 若要防止此情况，只需设置 GridView s`EditIndex`属性设置为`-1`中`SelectedIndexChanged`事件处理程序。


此外，请注意，它是重要 GridView 的视图状态是启用 （默认行为）。 如果设置 GridView s`EnableViewState`属性设置为`false`，运行的并发用户无意中删除或编辑记录风险。 请参阅[警告： 禁用并发问题与 ASP.NET 2.0 Gridview/DetailsView/FormViews 该支持编辑和/或删除和其视图状态](http://scottonwriting.net/sowblog/posts/10054.aspx)有关详细信息。

## <a name="step-5-disallow-editing-for-discontinued-products-when-showedit-all-suppliers-is-not-selected"></a>步骤 5： 在不停止使用产品时显示/编辑所有供应商为未选中允许编辑

虽然`ProductsBySupplier`GridView 已经完全正常运行，它当前授予过多访问权限是从特定供应商的用户。 每个我们的业务规则，此类用户不应能够更新停产的产品。 若要强制实施这种情况，我们可以隐藏 （或禁用） 停产的产品页面的用户的供应商提供访问时使用这些 GridView 行中的编辑按钮。

创建事件处理程序的 GridView s`RowDataBound`事件。 在此事件处理程序需要确定用户是否为关联与特定的供应商，这对于本教程，可以将通过检查来确定供应商 DropDownList 的`SelectedValue`属性-如果它是 s 以外的值为-1，则为用户与特定供应商相关联。 对于此类用户，然后需要确定产品已停止使用。 我们可以获得的引用，对实际`ProductRow`实例的行绑定的 GridView 通过`e.Row.DataItem`属性，如中所述[ *GridView 的页脚中显示摘要信息*](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md)本教程。 如果产品缺货，我们可以获得对 GridView s CommandField 使用在上一教程中讨论的技术中的编辑按钮的以编程方式引用[*添加客户端的确认时删除*](adding-client-side-confirmation-when-deleting-vb.md). 一旦我们有我们然后可以隐藏或禁用该按钮的引用。


[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample6.vb)]

与此事件处理程序中的位置，访问此页以用户身份的特定供应商提供已不再使用这些产品是不可编辑，作为编辑按钮是隐藏这些产品。 例如，Chef Anton 的秋葵组合是新奥尔良 Cajun 带来快乐供应商已中止的产品。 当针对此特定供应商访问的页面，此产品的编辑按钮隐藏的建立直通连接，（请参阅图 14）。 但是，当访问使用"显示/编辑所有供应商"，编辑按钮是可用 （请参阅图 15）。


[![Chef Anton s 秋葵汤编辑按钮处于隐藏状态的特定于供应商的用户](limiting-data-modification-functionality-based-on-the-user-vb/_static/image41.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image40.png)

**图 14**: Chef Anton s 秋葵汤编辑按钮处于隐藏状态的特定于供应商的用户 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image42.png))


[![显示/编辑所有供应商用户，对于 Chef Anton s 秋葵汤编辑按钮会显示](limiting-data-modification-functionality-based-on-the-user-vb/_static/image44.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image43.png)

**图 15**： 用于显示/编辑所有供应商用户、 Chef Anton s 秋葵组合会显示编辑按钮 ([单击以查看实际尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image45.png))


## <a name="checking-for-access-rights-in-the-business-logic-layer"></a>检查业务逻辑层中的访问权限

在本教程中的 ASP.NET 页面处理用户可以看到什么信息方面的所有逻辑，他可以更新哪些产品。 理想情况下，此逻辑还会出现在业务逻辑层。 例如，`SuppliersBLL`类 s`GetSuppliers()`方法 （它将返回所有供应商） 可能会进行检查，以确保当前登录的用户是*不*与某个特定供应商相关联。 同样，`UpdateSupplierAddress`方法可能包括检查以确保当前登录的用户是我们公司工作的 （并因此可以更新所有供应商地址信息） 或与之关联的数据更新的供应商。

因为在我们的教程用户的权限由在页上，BLL 类不能访问 DropDownList 没有包含此类的 BLL 层检查。 使用成员资格系统或 （例如 Windows 身份验证），由 ASP.NET 提供的扩展-全新的身份验证方案之一时当前登录可以从 BLL，从而使此类访问用户 s 上访问信息和角色信息权限检查可能在演示文稿和 BLL 层。

## <a name="summary"></a>总结

提供用户帐户的大多数站点需要自定义数据修改界面根据登录用户。 管理用户可能能够删除和编辑任何记录，而非管理用户可能会限制为仅更新或删除他们自己创建的记录。 其他类似的情况可能是，数据 Web 控件，ObjectDataSource，和业务逻辑层类可进行扩展以添加或拒绝基于已登录用户的某些功能。 在本教程中我们已了解如何限制可查看和编辑的数据，具体取决于用户是否与特定供应商相关联，或如果它们的工作为我们的公司。

本教程最后，我们对插入、 更新和删除数据使用 GridView、 DetailsView 和 FormView 控件执行的检查。 从开始下一教程，我们要将注意力转移到添加分页和排序的支持。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [上一篇](adding-client-side-confirmation-when-deleting-vb.md)
